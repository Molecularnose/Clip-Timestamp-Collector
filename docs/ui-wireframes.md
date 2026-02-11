# UI Wireframe Placeholders (MVP)

This document describes the basic UI structure for the Clip Timestamp Collector MVP.
These are **layout and hierarchy placeholders**, not visual designs.

The goal is to minimize cognitive load and optimize for live-stream usage.

---

## 1) Viewer Interface (Timestamp Submission)

### Primary Goal
Allow viewers to submit a timestamp **as fast as possible** without disrupting the stream.

### Layout Priority (Top → Bottom)

1. **Session Context**
   - Session title
   - Game name
   - Session status (Active / Paused)

2. **Primary Action**
   - Large “🔥 Clip Moment” button
   - Must be immediately visible
   - One-tap friendly (mobile)

3. **Optional Note Input**
   - Collapsed by default
   - Max 100 characters
   - Placeholder: “What just happened?”

4. **Feedback State**
   - Confirmation message (“Moment saved”)
   - Reset to default state after submission

---

### Viewer Constraints
- No login required
- No navigation
- No scrolling required in normal use
- Works on mobile with one hand

---

## 2) Streamer Dashboard (Session Control + Review)

### Primary Goals
- Control session state
- Review timestamps efficiently after the stream

---

### A) Session Control Area (Top)

Elements:
- Session title
- Game name
- Current status indicator
- Action buttons:
  - Start
  - Pause
  - Resume
  - End

Rules:
- Only valid actions shown per state
- State changes must be explicit (no auto-switching)

---

### B) Timestamp Review Area (Main Content)

Layout:
- Timestamps grouped by segment
- Each entry shows:
  - Segment index
  - Offset time (HH:MM:SS)
  - Note text
  - Optional submitted-by label
  - “Clipped” checkbox (optional v1)

Ordering:
- Segment index ascending
- Offset time ascending

---

### C) Export Actions (Footer or Sidebar)

- Copy to clipboard
- Export CSV

These actions are only enabled when:
- Session state = ended

---

## 3) Empty & Edge States

### No Timestamps Yet
- Message: “No moments captured yet.”

### Session Paused
- Viewer UI shows:
  - “Timestamps paused — stream is on break.”

### Session Ended
- Viewer UI shows:
  - “This session has ended.”

---

## Design Principles

- One primary action per screen
- Clear session state visibility
- No hidden automation
- Clarity over cleverness
