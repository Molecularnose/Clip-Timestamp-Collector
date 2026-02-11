# Basic Session Flow (MVP)

This document describes the basic lifecycle of a stream session in the Clip Timestamp Collector MVP.
The goal is to keep the flow predictable, resilient to real streaming behavior, and easy to understand.

---

## Session Lifecycle Overview

A session represents one live stream where viewers can submit clip timestamps.

States:
- `created`
- `active`
- `paused`
- `ended`

Only **active** sessions accept timestamps.

---

## 1) Create Session

**Who:** Streamer  
**When:** Before going live

**What happens**
- Streamer creates a new session
- Session is initialized in `created` state
- No timestamps can be submitted yet

**Purpose**
- Prepare the session
- Generate a shareable viewer link

---

## 2) Start Session

**Who:** Streamer  
**When:** Stream goes live

**What happens**
- Session state changes to `active`
- First segment is created
- Segment start time is recorded

**Rules**
- Exactly one segment is active at a time
- Viewers can now submit timestamps

---

## 3) Submit Timestamp (Viewer)

**Who:** Viewer  
**When:** Something clip-worthy happens

**What happens**
- Viewer clicks “🔥 Clip Moment”
- Optional short note is added
- Timestamp offset is calculated relative to the current segment start
- Timestamp is saved and ordered chronologically

**Constraints**
- Submission is only allowed while session is `active`
- Notes are limited to 100 characters

---

## 4) Pause Session

**Who:** Streamer  
**When:** BRB, break, or stream interruption

**What happens**
- Session state changes to `paused`
- Current segment is closed with an end time
- Timestamp submission is disabled

**Purpose**
- Prevent incorrect offsets during downtime

---

## 5) Resume Session

**Who:** Streamer  
**When:** Stream continues

**What happens**
- Session state returns to `active`
- A new segment is created
- Timestamp offsets reset relative to the new segment

---

## 6) End Session

**Who:** Streamer  
**When:** Stream is finished

**What happens**
- Session state changes to `ended`
- Timestamp submission is permanently disabled
- All segments are closed if still open

**Purpose**
- Lock the session for review and export

---

## Post-Stream Review Flow

After the session ends:
- Streamer reviews timestamps grouped by segment
- Marks items as clipped (optional)
- Exports the timestamp list for editing or descriptions

---

## Design Principles

- Streamer is always in control of session state
- Viewers never manage state
- No automatic detection or platform APIs
- Accuracy through simplicity, not automation
