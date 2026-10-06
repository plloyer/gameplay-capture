# gameplay-capture

Tooling to capture, slice, tag and index gameplay footage of existing games, as reference material for remakes. First target: **Battlezone Combat Commander**.

## Idea
Start from an existing game and modify it afterwards. What is missing is good capture of the original. This project builds:

1. **Baseline pack**: a human plays and records; the video is sliced into numbered clips, `TAGS.md` (detailed descriptions) and extracted PNG frames.
2. **Coverage checklist** (`COVERAGE.md`): screens, HUD states, units, weapons, menu flows, ticked off as clips cover them. Gaps become targets.
3. **Later**: a VISTA-style explorer agent (lossless frame archive, zoom, pixel read, persistent notes) whose goal is coverage, not winning.

Inspiration: *VISTA: A Visual Harness for Reasoning in an Interactive World* (arXiv 2610.02200).

## Pipeline (baseline)
1. ffprobe the video (duration, resolution).
2. Contact sheets (1 frame / 5 s, 3x3 at 640x360), map segments.
3. Refine boundaries with 1 fps strips.
4. Cut clips, always re-encoding (`libx264 -preset veryfast -crf 20`).
5. Write `TAGS.md`, extract frames (1 / 3 s, 1280 px; denser for fast action).
6. Verify durations and spot-check frames against tags.

## Handoff line for the build session
Read TAGS.md first, then load only the frame PNGs of the segment you are implementing. Re-extract a full-res frame from the matching .mp4 with ffmpeg if you need fine detail.

## Copyright
Captures come from a commercial game. **No footage, frames or game assets are committed here** (see `.gitignore`); they live privately elsewhere. This repo holds tooling and docs only.
