# Marcus Retirement Tool

Routes to the correct pipeline stage.

## Task Routing

| Task Type | Go To | Description |
|-----------|-------|-------------|
| Starting the pipeline | `stages/01-voice-extraction/CONTEXT.md` | Extract Marcus's voice from the brief |
| Voice done, starting story | `stages/02-story-framework/CONTEXT.md` | Build camping trip narrative and exact copy |
| Story done, starting design | `stages/03-visual-design/CONTEXT.md` | Produce CSS spec and SVG illustration briefs |
| Design done, building artifact | `stages/04-artifact-build/CONTEXT.md` | Build the single-file HTML artifact |
| Artifact approved, writing up | `stages/05-writeup/CONTEXT.md` | Write 100-word competition writeup |

## Shared Resources

| Resource | Location | Contains |
|----------|----------|---------|
| Marcus brief | `inputs/marcus-brief.md` | Client brief, voice reference, financial methodology |
| Brand voice skill | `skills/brand-voice/SKILL.md` | Voice extraction process and output format |
