# Stage 01: Voice Extraction

Extract Marcus's voice from his brief. Every word in the final artifact traces back to this stage.

## Inputs

| Source | File | Scope | Why |
|--------|------|-------|-----|
| Marcus brief | `../../inputs/marcus-brief.md` | Full document | This IS the voice source — Marcus: "the way I'm talking to you in this brief is the way the tool should talk" |
| Brand voice skill | `../../skills/brand-voice/SKILL.md` | Guideline Generation Workflow + Voice Enforcement Framework | Process for extraction and output format |
| Guideline template | `../../skills/brand-voice/references/guideline-template.md` | Full document | Required output format for voice-rules.md |

## Process

Follow the **Guideline Generation Workflow** in `skills/brand-voice/SKILL.md`. Source material is `inputs/marcus-brief.md`. Skip discovery entirely.

1. **Read the brief as a voice sample** — not a client brief. Marcus explicitly says the brief is the voice reference.
2. **Synthesize** using the guideline template structure:
   - "We Are / We Are Not" table (minimum 4 rows, each with a supporting quote from the brief)
   - Voice constants (minimum 3, each anchored to the brief)
   - Tone-by-context matrix: good result / behind result / stage copy / path-forward copy
   - Terminology guide: must-use, preferred, avoid, never-use
   - Effective phrases lifted verbatim from the brief (minimum 5)
   - Anti-patterns: anything that sounds like a bank, not Marcus
3. **Add Interactive Voice Notes** section: how the voice adapts specifically for the camping trip adventure format (stage copy, choice labels, result reveals, path-forward sliders)
4. **Score confidence** per section (High/Medium/Low) based on how explicitly the brief supports each claim
5. **Flag open questions** — any voice ambiguity with a recommendation

The brief is highly explicit about voice. Most sections should score High confidence.

## Audit

| Check | Pass Condition |
|-------|----------------|
| Example phrases | 5 or more exact phrases lifted verbatim from the brief |
| Dos | 3+ specific patterns to replicate with examples |
| Don'ts | 3+ specific patterns to avoid with examples |
| Interactive voice notes | Present; explicitly covers short-form stage copy |

## Outputs

| Artifact | Location | Format |
|----------|----------|--------|
| voice-rules.md | `output/voice-rules.md` | Brand-voice skill format + Interactive Voice Notes section |

**Human checkpoint:** Review `output/voice-rules.md` before proceeding to Stage 02. Confirm dos/don'ts match how Marcus actually sounds in the brief.
