# Clip Timestamp Collector

Clip Timestamp Collector is a lightweight web app that helps streamers save time by letting viewers mark clip-worthy moments **during live streams**.

Instead of rewatching entire VODs, creators get a structured list of timestamps with short notes, generated live by their community.

---

## The Problem

Great moments happen live:
- Funny dialogue
- Big decisions
- Unexpected chaos

Most streamers either miss them or waste hours scrubbing VODs afterward.

---

## The Solution

Clip Timestamp Collector turns viewers into **moment spotters**.

- Streamer starts a session before going live
- Viewers click one button when something interesting happens
- The app records the timestamp relative to the stream start
- After the stream, the streamer reviews a clean list and clips faster

No bots. No APIs. No automation.

---

## MVP Scope (v1)

### Included
- Stream session creation
- Viewer timestamp submission with optional notes
- Streamer review dashboard
- Exportable timestamp list (copy / CSV)

### Explicitly Out of Scope
- Twitch / YouTube API integrations
- Authentication or user accounts
- Chat commands or bots
- Automated clipping
- AI or video analysis
- Mobile apps

This project intentionally prioritizes **speed, simplicity, and validation**.

---

## How It Works (High Level)

1. Streamer creates a session and shares the link
2. Viewers click “🔥 Clip Moment” during the stream
3. Each click saves a timestamp + short note
4. Streamer reviews the list after the stream
5. Clipping takes minutes instead of hours

---

## Status

Early MVP.

Actively being built and tested with a live gaming and streaming community to validate:
- Real usage during streams
- Time saved during post-stream clipping
- Willingness to reuse across multiple streams

---

## Philosophy

- Humans detect interesting moments better than algorithms
- Fewer features > more usage
- Manual before automated
- Validation before scale
