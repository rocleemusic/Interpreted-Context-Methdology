# Stage 03: Visual Design

Produce the complete visual spec for Stage 04. Every design decision is made here. Stage 04 builds; it does not design.

## Inputs

| Source | File | Scope | Why |
|--------|------|-------|-----|
| Voice rules | `../01-voice-extraction/output/voice-rules.md` | Tone section | Visual language must reinforce voice |
| Story map | `../02-story-framework/output/story-map.md` | Full document | Component and image specs depend on the copy structure |
| Bento skill | `../../../../page-ref/SKILL.md` | Guideline Authoring Workflow + Required Output Structure + Component Rule Expectations | Provides the spec authoring process and output format |

**Palettes are pre-extracted — do not read the visual-ref SVG files directly.**
**Bento's default color tokens (primary=#FAD4C0 etc.) and font (Inter) are overridden by our three-phase palette and Bitter/Nunito. Use Bento's process and structure; ignore its default values.**

## Pre-Extracted Palettes

Three-phase visual arc: Dawn (Stages A–B) → Dusk (Stages C–D–E) → Night (End reveal).
`#BC6246` is the golden thread — earth (dawn) → ember glow (dusk) → campfire (night).

### Dawn palette (Stages A–B, source: visual-ref/export-2026-05-02 060958.svg)
```css
--dawn-bg:      #DAE6D7;  /* pale sage */
--dawn-text:    #46531A;  /* dark olive */
--dawn-sky:     #9CB8BE;  /* muted teal */
--dawn-grass:   #A2AE56;  /* olive green */
--dawn-earth:   #BC6246;  /* terracotta ← golden thread */
--dawn-water:   #A5D1D8;  /* soft aqua */
```

### Dusk palette (Stages C–D–E, source: visual-ref/export-2026-05-02 061210.svg)
```css
--dusk-bg:      #F3E6DB;  /* warm cream */
--dusk-sun:     #FDDB9A;  /* golden yellow */
--dusk-sky:     #84DCE5;  /* bright aqua */
--dusk-text:    #545E43;  /* dark olive */
--dusk-ember:   #DC9E7C;  /* amber */
--dusk-thread:  #BC6246;  /* terracotta ← golden thread */
```

### Night palette (End reveal, source: visual-ref/export-2026-05-02 062457.svg + dark refs)
```css
--night-bg:     #2F1B3A;  /* deep purple sky */
--night-forest: #57896B;  /* forest green */
--night-slate:  #2D4152;  /* dark slate */
--night-mist:   #F5FCF6;  /* near-white mist */
--night-fire:   #BC6246;  /* campfire ember ← golden thread */
--night-flame:  #E26A40;  /* active flame */
--night-glow:   #EEB236;  /* campfire glow */
```

## Typography

- **Headings / story narrative:** Bitter (slab serif — sturdy, trail-guide feel)
- **Inputs / labels / numbers:** Nunito (rounded sans — friendly, readable on mobile)
- Both via Google Fonts CDN (one `<link>` tag, two font families)

## Process

Follow Bento's **Guideline Authoring Workflow** for generating design-spec.md:
1. Restate the design intent in one sentence
2. Define tokens and foundational constraints (use pre-extracted palettes below — not Bento defaults)
3. Specify component anatomy, states, variants, and interaction behavior
4. Include accessibility acceptance criteria (WCAG 2.2 AA, keyboard-first)
5. Add anti-patterns for this specific context (sterile bank UI patterns to avoid)
6. End with a QA checklist executable during Stage 04 code review

### 1. Produce full CSS variable set

Extend the palettes above with:
- Spacing scale: `--space-xs` (4px) through `--space-xl` (48px)
- Type scale: `--text-sm` (14px) through `--text-2xl` (32px)
- Component tokens: `--radius-card`, `--shadow-card`, `--border-choice`, `--transition-phase`

### 2. Spec UI components

For each component: colors used, spacing, border/radius, hover state, active state.

| Component | Purpose |
|-----------|---------|
| `.progress-tracker` | Dot + line strip across top; current stage dot filled, previous filled, future empty |
| `.choice-btn` | Two-option selection button per stage; clicking sets slider default and highlights button |
| `.slider-input` | Range `<input>` with custom thumb (square or rounded) + colored track |
| `.stage-card` | Full-screen wrapper for each stage; transitions with CSS fade |
| `.result-card` | End screen result container; shifts background on outcome |
| `.path-forward` | Container for the two behind-outcome live sliders |
| `.reveal-line` | Each line of the campfire reveal; starts hidden, fades in on schedule |

### 3. Spec inline SVG illustrations (one per stage)

Write a brief for each stage's SVG. Use only the palette colors for the applicable phase. Each SVG has two states: **default** (before choice) and **confirmed** (after Next button advances the stage).

| Stage | Phase | Default image | Confirmed image |
|-------|-------|---------------|-----------------|
| A | Dawn | Trail at sunrise, hiker at trailhead, mountain in distance | Hiker further up the trail, sun higher |
| B | Dawn | Wide sky, sun at mid-height, horizon with treeline | Sun angle shifts based on retirement age chosen |
| C | Dusk | Pack on ground, partly filled, warm afternoon light | Pack at correct fullness matching savings choice |
| D | Dusk | Hiker at steady walk, midday warmth | Hiker pace matches choice (ambling vs. striding) |
| E | Dusk | Small lean camp with minimal gear | Camp scales live with income slider (see Stage E note) |

**Stage E note:** The camp SVG must have JS-interpolatable elements. As the income slider moves, tent size / gear count scales proportionally. Name the SVG group elements: `#camp-tent`, `#camp-gear`, `#camp-fire-pit`. JS maps slider value → scale transform.

### 4. Spec 3 family-status visual variants

Stage 0 selection sets a body class that modifies all stage SVG hiker representations:
| Body class | Visual |
|------------|--------|
| `.party-solo` | Single hiker silhouette |
| `.party-duo` | Two hiker silhouettes side by side |
| `.party-family` | Two adult silhouettes + one smaller figure |

All stage SVGs should have a `<g class="hikers">` group that responds to these body classes via CSS.

### 5. Spec day → night transition

When Stage E advances to the end reveal:
- Body class changes from `phase-dusk` to `phase-night`
- `transition: background-color 1.2s ease-in-out, color 0.8s ease-in-out`
- Stars SVG overlay fades in (opacity 0 → 1, 1.5s delay)

### 6. Spec campfire reveal animation

End screen campfire SVG:
- Starts unlit: logs + stone circle, no flame
- On reveal start: flame SVG paths animate in (opacity 0 → 1, 0.6s ease)
- Flicker: `@keyframes campfire-flicker` on flame paths — subtle scale + opacity oscillation, loop
- Colors: `--night-fire` (#BC6246) base, `--night-flame` (#E26A40) mid, `--night-glow` (#EEB236) tip
- Glow effect: `filter: drop-shadow(0 0 8px var(--night-glow))`

## Outputs

| Artifact | Location | Format |
|----------|----------|--------|
| design-spec.md | `output/design-spec.md` | Sections: CSS Variables → Typography → Component Specs → SVG Briefs per stage → Family Variant Spec → Transition Spec → Campfire Animation Spec |

**Human checkpoint:** Roc reviews `output/design-spec.md` before Stage 04 begins.
