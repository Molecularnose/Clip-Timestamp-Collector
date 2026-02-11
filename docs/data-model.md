# MVP Data Model Notes

This document describes the minimal data model for the Clip Timestamp Collector MVP.
The goal is to keep the schema simple, validate usage, and avoid platform dependencies.

---

## Entities

### 1) Session
Represents one stream session where viewers can submit clip timestamps.

**Fields**
- `id` (string/uuid) — unique session identifier
- `title` (string) — human-friendly session name (e.g., “Witcher 3 – Act 1 Finale”)
- `game` (string) — game name (free text for MVP)
- `status` (enum: `active`, `paused`, `ended`) — current state of the session
- `created_at` (datetime)
- `updated_at` (datetime)

**Notes**
- For MVP, `game` is free text (no catalog).
- `status` controls whether viewers can submit timestamps.

---

### 2) Segment (for Start / Pause / Resume)
Represents an “active streaming period” inside a session.
A session can have multiple segments due to breaks or restarts.

**Fields**
- `id` (string/uuid)
- `session_id` (fk → Session.id)
- `index` (int) — 1, 2, 3… (order of segments)
- `start_time` (datetime) — when segment became active
- `end_time` (datetime, nullable) — when segment was paused/ended
- `created_at` (datetime)

**Notes**
- Exactly one segment should be `active` at a time per session.
- When the streamer clicks **Pause**, set `end_time`.
- When **Resume**, create a new segment with `index + 1`.

---

### 3) Timestamp
One viewer-submitted “clip moment”.

**Fields**
- `id` (string/uuid)
- `session_id` (fk → Session.id)
- `segment_id` (fk → Segment.id)
- `offset_seconds` (int) — seconds since segment start
- `offset_hms` (string) — cached display format (e.g., `01:12:34`)
- `note` (string, max 100 chars, nullable)
- `submitted_by` (string, nullable) — display name (optional MVP)
- `created_at` (datetime)

**Notes**
- Store `offset_seconds` as the source of truth.
- `offset_hms` is convenience for UI and exports.
- For MVP, `submitted_by` can be optional and unauthenticated.

---

## Rules / Constraints (MVP)

1. **Timestamp submission allowed only when**
   - `session.status == active`
   - and the current segment exists and has `end_time == null`

2. **Offset calculation**
   - `offset_seconds = now - segment.start_time`
   - Clamp at minimum 0

3. **Ordering**
   - Sort timestamps by: `(segment.index ASC, offset_seconds ASC)`

4. **Max note length**
   - 100 characters (hard limit)

---

## Export Format (MVP)

Export grouped by segment:

Example:
- `Segment 1 00:42:15 – Geralt insulted the Baron`
- `Segment 2 00:13:40 – O’Dimm smile`

CSV columns (suggested):
- `segment_index`
- `offset_hms`
- `note`
- `submitted_by`
- `created_at`
