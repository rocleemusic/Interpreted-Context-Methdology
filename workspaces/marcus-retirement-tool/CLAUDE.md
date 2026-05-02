# Marcus Retirement Tool

Produces a choose-your-own-adventure retirement calculator for Marcus's financial planning prospects, plus a 100-word competition writeup. Story metaphor: camping trip ("Will we make camp before dark?").

## Folder Map

```
marcus-retirement-tool/
├── CLAUDE.md              (you are here)
├── CONTEXT.md             (task routing)
├── setup/                 (onboarding and pipeline overview)
├── inputs/                (primary source material)
│   └── marcus-brief.md
├── skills/
│   └── brand-voice/       (voice extraction framework — install before Stage 01)
├── stages/
│   ├── 01-voice-extraction/
│   ├── 02-story-framework/
│   ├── 03-visual-design/
│   ├── 04-artifact-build/
│   └── 05-writeup/
└── deliverables/          (final outputs for competition submission)
```

## Triggers

| Keyword | Action |
|---------|--------|
| `setup` | Show pipeline overview and pre-build prerequisite, then point to Stage 01 |
| `status` | Scan stages/*/output/ for files; show completion state per stage |

## How `status` Works

Scan each `stages/NN-name/output/` folder. If it contains any file besides `.gitkeep`, the stage is **COMPLETE**. Otherwise **PENDING**.

```
[01 Voice] → [02 Story] → [03 Visual] → [04 Build] → [05 Writeup]
```

## Routing

| Task | Go To |
|------|-------|
| Extract Marcus's voice from brief | `stages/01-voice-extraction/CONTEXT.md` |
| Build camping trip story framework | `stages/02-story-framework/CONTEXT.md` |
| Create visual design spec | `stages/03-visual-design/CONTEXT.md` |
| Build the HTML artifact | `stages/04-artifact-build/CONTEXT.md` |
| Write competition writeup | `stages/05-writeup/CONTEXT.md` |

## Stage Handoffs

Each stage writes output to `stages/NN-name/output/`. The next stage reads from there. Never read backward through the pipeline.

## Primary Input

`inputs/marcus-brief.md` — source of truth for Marcus's voice, financial methodology, and problem definition.
