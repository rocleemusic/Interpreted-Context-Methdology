# Stage 04: Artifact Build

Build the single-file HTML artifact. All design and copy decisions are already made. Implement.

## Inputs

| Source | File | Scope | Why |
|--------|------|-------|-----|
| Voice rules | `../01-voice-extraction/output/voice-rules.md` | Interactive voice notes | Verify tone during build |
| Story map | `../02-story-framework/output/story-map.md` | Full document | All copy, stage structure, reveal sequences |
| Design spec | `../03-visual-design/output/design-spec.md` | Full document | All CSS, component specs, SVG briefs |
| Bento skill | `../../../../page-ref/SKILL.md` | Component Rule Expectations + Quality Gates | Tells you how to read the design spec and what completeness looks like |

**design-spec.md follows Bento's Required Output Structure.** Read the Bento skill to understand what sections to expect: design intent → tokens → component anatomy/states/variants → accessibility criteria → anti-patterns → QA checklist. Use the QA checklist at the end of the build to self-review before saving output.

**Voice enforcement:** After generating any copy (stage narratives, result messages, choice labels, slider templates), run the Brand Voice Enforcement check from `skills/brand-voice/SKILL.md` before finalizing: apply voice constants → flex tone by context → validate against "We Are / We Are Not" → flag open questions. Copy in the artifact must pass this check.

## Tech Stack

Single HTML file. Vanilla JS. Bitter + Nunito via Google Fonts CDN (one `<link>` tag). All SVGs inline. No external JS libraries. No CSS frameworks. Deployable to GitHub Pages as-is.

## Image Behavior

- **Stages A–D:** Static image per stage. CSS `opacity` fade on stage transition.
- **Stage E:** Income slider maps to SVG camp elements live (JS `input` event interpolates `#camp-tent`, `#camp-gear` scale).
- **End reveal:** Night palette activates; campfire SVG animates in; reveal lines appear on schedule.

## Phase Transitions

Body gets one CSS class at a time:
- `phase-dawn` — Stages A, B
- `phase-dusk` — Stages C, D, E
- `phase-night` — End reveal

Phase transition: `transition: background-color 1.2s ease-in-out, color 0.8s ease-in-out` on `body`.

## Build Order

1. **`<head>` setup** — Google Fonts link (Bitter + Nunito), `<style>` block with all CSS variables from design-spec.md
2. **HTML structure** — All screens in the DOM with `display: none`; JS shows one at a time:
   - `#screen-entry` (Stage 0 — family status)
   - `#screen-a` through `#screen-e` (Stages A–E)
   - `#screen-result` (End reveal)
3. **Stage navigation JS** — Functions: `showScreen(id)`, `nextStage()`, `prevStage()`, `setChoice(stage, value)` (sets slider default + highlights button)
4. **Inline SVG illustrations** — One per stage from design-spec.md SVG briefs; Stage E SVG has named groups for JS interpolation
5. **Financial math module** — Pure functions, no side effects:

   ```js
   calcTarget(annualIncome)
     → 25 * (annualIncome * 0.8)

   calcFV(currentSavings, monthlySavings, yearsToRetirement)
     → currentSavings * Math.pow(1.07, n)
       + (monthlySavings * 12) * (Math.pow(1.07, n) - 1) / 0.07
     where n = yearsToRetirement

   calcGap(fv, target)
     → target - fv  (negative = surplus)

   calcGapRatio(fv, target)
     → (target - fv) / target

   calcExtraMonthlyNeeded(currentSavings, currentMonthly, n, target)
     → solve for PMT_annual in FV formula given FV = target
     → extra = (PMT_annual - currentMonthly * 12) / 12

   calcFVWithExtraYears(currentSavings, monthlySavings, n, extra)
     → calcFV(currentSavings, monthlySavings, n + extra)
   ```

6. **End screen** — On entering `#screen-result`:
   - Calculate outcome (on-track / slightly-behind / significantly-behind)
   - Show correct message from story-map.md
   - Schedule campfire reveal: each `.reveal-line` fades in on the timing from story-map.md
   - If behind: show `.path-forward` with two sliders; bind `input` events to recalculate FV + update result card live
7. **Campfire animation** — CSS `@keyframes campfire-flicker` as per design-spec.md; JS adds `.lit` class to campfire SVG on reveal start
8. **Mobile responsiveness** — Max-width container (480px centered), fluid sliders, base font size 16px
9. **Test all paths before saving output:**
   - On track: age 35, income $200K, savings $300K, monthly $3,000, target 65 → should show on-track message
   - Slightly behind: age 45, income $100K, savings $50K, monthly $800, target 65 → gap ≤ 15%
   - Significantly behind: age 52, income $80K, savings $20K, monthly $400, target 65 → gap > 15%
   - Stage E live: drag income slider → verify camp SVG scales
   - End screen: drag monthly savings slider → verify result card updates live

## Financial Math

```
Target     = 25 × (annualIncome × 0.8)
n          = targetRetirementAge − currentAge
FV         = currentSavings × (1.07)^n + (monthlySavings × 12) × [(1.07)^n − 1] / 0.07
Slightly behind:     FV < target AND (target − FV) / target ≤ 0.15
Significantly behind: (target − FV) / target > 0.15
Extra monthly:       solve PMT_annual s.t. FV = target; extra = (PMT_annual − monthlySavings×12) / 12
```

## Outputs

| Artifact | Location | Format |
|----------|----------|--------|
| index.html | `output/index.html` | Single self-contained HTML file |

**Human checkpoint:** Roc opens `output/index.html` in a browser. Check:
- [ ] All screens advance without errors
- [ ] All 3 outcome paths show the correct message
- [ ] Stage E income slider updates the camp SVG live
- [ ] End screen sliders recalculate the result in real time
- [ ] Reads correctly on mobile (or Chrome devtools mobile view at 390px)

When approved, copy `output/index.html` to `../../deliverables/index.html`.
