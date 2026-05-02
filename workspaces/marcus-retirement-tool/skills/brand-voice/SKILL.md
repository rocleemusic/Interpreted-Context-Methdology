---
name: brand-voice
description: Transforms brand source material into structured, enforceable voice guidelines. Core principle — "Voice is constant, tone flexes."
source: https://github.com/anthropics/knowledge-work-plugins/tree/main/partner-built/brand-voice
license: see source
---

# Brand Voice Skill

## Mission
Transform brand source material into structured guidelines with enforceable AI guardrails for consistent content generation.

Core design principle: **Voice is constant, tone flexes.**

## For This Workspace

Source material is `../../inputs/marcus-brief.md`. Skip discovery entirely — the brief IS the source. Go directly to guideline generation.

---

## Guideline Generation Workflow

Use this workflow in Stage 01 to produce `voice-rules.md`.

### Steps

1. **Source Identification** — Source is `inputs/marcus-brief.md`. Marcus explicitly says: "The way I'm talking to you in this brief is the way the tool should talk."

2. **Processing** — Read the brief as a voice sample. Extract:
   - Voice attributes (personality, values, identity)
   - Messaging themes
   - Terminology (preferred / prohibited)
   - Tone guidance
   - Effective phrases and anti-patterns

3. **Synthesis** — Produce structured guidelines:
   - "We Are / We Are Not" table (4+ rows minimum)
   - Voice constants (always true regardless of context)
   - Tone flexes (shifts by situation: good news vs. bad news, confident vs. uncertain)
   - Tone-by-context matrix (at minimum: on-track result, behind result, stage copy)
   - Terminology guide

4. **Confidence Scoring** — Rate each section High/Medium/Low based on how explicitly the brief supports it

5. **Open Questions** — Flag any voice ambiguities with a recommendation

6. **Quality Assurance** — Before saving:
   - 4+ "We Are / We Are Not" rows
   - 3+ voice constants with evidence from brief
   - 3+ tone contexts in matrix
   - No vague adjectives without anchoring examples

### Output format

See `references/guideline-template.md`.

---

## Voice Enforcement Framework

Use this in Stage 04 to self-validate generated copy before saving output.

### Loading Order

1. Session context (voice-rules.md from Stage 01 output)
2. `.claude/brand-voice-guidelines.md` if it exists
3. User input as fallback

### Enforcement Process

1. Analyze content type and audience
2. Apply voice constants (never change)
3. Flex tone by context (formality / energy / technical depth)
4. Generate content
5. Validate against "We Are / We Are Not"
6. Flag ambiguities as open questions

### Voice Dimensions

Voice constants — "We Are / We Are Not" pairs to extract from Marcus's brief and hold throughout:

| Voice | NOT |
|-------|-----|
| Confident | Arrogant |
| Approachable | Casual / sloppy |
| Direct | Blunt / aggressive |
| Human | Sterile / clinical |
| Honest | Evasive |

Tone flexes — three dimensions that shift by context:

| Dimension | Range |
|-----------|-------|
| Formality | High ↔ Low |
| Energy | High ↔ Warm/Low |
| Technical depth | High ↔ Low |

Context examples:
- Stage copy (adventure, short): Low formality, warm energy, low technical depth
- Good result reveal: Medium formality, warm energy, zero technical depth
- Bad result reveal: Medium formality, grounded low energy, low technical depth

---

## Quality Gates

- No rule depends on ambiguous adjectives alone — anchor each to a token, threshold, or example from Marcus's brief
- Every extracted attribute must have a supporting quote or phrase from the source
- Prefer consistency over one-off local optimizations
- Flag conflicts between voice and the camping trip metaphor context; resolve toward Marcus's voice
