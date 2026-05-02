# Setup: Marcus Retirement Tool

This workspace is pre-configured for the Clief Notes Weekly Competition #2 entry. No questionnaire needed — all inputs come from Marcus's brief.

## Pre-Build Prerequisite

Before running Stage 01, install the brand-voice skill and bundle it into this workspace:

```
npx skills add https://github.com/anthropics/knowledge-work-plugins --skill brand-voice
```

Then copy the installed `SKILL.md` (and any `rules/` files) into `skills/brand-voice/`.

## Pipeline

```
[01 Voice] → [02 Story] → [03 Visual] → [04 Build] → [05 Writeup]
```

Each stage has a human checkpoint before the next stage begins.

## Visual References

Two palette reference SVGs live in `../../visual-ref/`:
- `export-2026-05-02 060958.svg` — dawn palette (Stages A–B)
- `export-2026-05-02 061210.svg` — dusk palette (Stages C–D–E)
- `export-2026-05-02 062457.svg` — campfire/evening colors (end reveal)

Palettes are pre-extracted into Stage 03's CONTEXT.md. You do not need to read the SVG files.

## Start Here

→ `stages/01-voice-extraction/CONTEXT.md`
