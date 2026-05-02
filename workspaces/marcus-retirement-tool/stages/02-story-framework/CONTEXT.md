# Stage 02: Story Framework

Write all narrative copy for the adventure. Stage 04 implements without writing a word.

## Inputs

| Source | File | Scope | Why |
|--------|------|-------|-----|
| Voice rules | `../01-voice-extraction/output/voice-rules.md` | Full document | All copy must match Marcus's voice |
| Marcus brief | `../../inputs/marcus-brief.md` | "How I Think About On Track" + "When the News Isn't Good" | Financial context + tone for difficult results |

## Process

### 1. Write Stage 0 — Pre-Entry

Frame the family status question as a camping trip opening. This screen appears before Stage A and sets the narrative voice + visual theme throughout.

Three choices:
| Choice | Label | Sets |
|--------|-------|------|
| Solo | "Just me and the trail" | narrative: "you" / visual: lone hiker |
| Partnered | "Two-person expedition" | narrative: "you and your partner" / visual: two hikers |
| Family | "Full family camp" | narrative: "your family" / visual: family camp |

Write: screen title, 1–2 sentence intro, 3 choice labels. Match Marcus's voice.

### 2. Write Stages A–E

One input per stage. For each stage write:
- **Title** (the stage beat)
- **Narrative text** (1–3 sentences, Marcus's voice, sets up the choice — not instructional)
- **Choice 1 label** and the slider default it sets
- **Choice 2 label** and the slider default it sets
- **Slider label** and unit

| Stage | Beat | Input | Choice 1 → slider default | Choice 2 → slider default |
|-------|------|-------|---------------------------|---------------------------|
| A | "Where are you on the trail?" | current age (years) | "Early trail" → 38 | "Mid-journey" → 50 |
| B | "What time do you need to make camp?" | target retirement age (years) | "Before sunset" → 62 | "Just before dark" → 67 |
| C | "How full is your supply pack?" | current savings ($) | "Light supplies" → $25,000 | "Well stocked" → $150,000 |
| D | "How fast are you moving?" | monthly savings ($/month) | "Steady pace" → $500 | "Pushing hard" → $2,000 |
| E | "How big is your camp?" | annual income ($/year) | "Lean camp" → $80,000 | "Full camp" → $180,000 |

Narrative text must naturally adapt to Stage 0 selection where it reads better (e.g., "you" vs. "you and your partner" vs. "your family").

### 3. Write End-State Messages — 3 Outcomes

Each outcome has a gradual campfire reveal. Write the **reveal sequence** as numbered lines that appear one at a time on screen.

**On track** (FV ≥ target):
- Story beat: peaceful arrival, fire lit and warm, night sky clear
- Emotional arc: earned calm — not celebration, not fanfare. Marcus doesn't throw parties.
- Write 3–4 reveal lines building from the trail moment → the number → what it means → the reassurance

**Slightly behind** (gap ≤ 15% of target):
- Story beat: dusk, fire just starting to catch, still time to adjust
- Emotional arc: honest about the gap, immediately pivots to the path forward
- Write 3–4 reveal lines: name the gap plainly → pivot fast to "here's what it takes"

**Significantly behind** (gap > 15% of target):
- Story beat: night falling fast — but fire IS possible, the embers are there
- Emotional arc: direct, salvageable — the result is a route adjustment, not a verdict
- Write 3–4 reveal lines: name it plainly → name it honestly → show the route

The end is always salvageable. Never leave someone on the screen with only a number.

### 4. Write Path-Forward Slider Templates

Used on the end screen for "slightly behind" and "significantly behind" outcomes. These are templates — Stage 04 fills in the calculated values at runtime.

```
Monthly savings slider label:
  "Move this to {{EXTRA_MONTHLY}}/month and you'll make camp with {{BUFFER}} to spare."

Retirement age slider label:
  "Two more years on the trail and you arrive with {{BUFFER_PLUS2}} to spare."
```

### 5. Specify Campfire Reveal Sequence

For each outcome, list the lines in order with a note on timing:
- Line 1: trail moment (1.0s delay before appearing)
- Line 2: the number (0.8s after Line 1)
- Line 3: what it means (0.8s after Line 2)
- Line 4: what's next (1.0s after Line 3)

## Audit

| Check | Pass Condition |
|-------|----------------|
| Stage 0 | Title + intro + 3 choice labels |
| All 5 stages (A–E) | Title + narrative + 2 choice labels + slider label |
| Voice match | Every line passes the voice-rules.md dos/don'ts |
| 3 end-state messages | All three present, each with campfire reveal sequence (3–4 lines) |
| Path-forward templates | Both templates present |
| Salvageable ending | Both "behind" outcomes pivot to path forward within 2 reveal lines |

## Outputs

| Artifact | Location | Format |
|----------|----------|--------|
| story-map.md | `output/story-map.md` | Structured document: Stage 0 → Stages A–E → End states (3) → Path-forward templates → Reveal timing |

**Human checkpoint:** Roc reviews and edits `output/story-map.md` directly before Stage 03 begins. Unchanged prose = accepted. Differences = intentional voice decisions.
