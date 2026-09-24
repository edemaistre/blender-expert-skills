# Changelog

## v0.1 (2026-09-24)

First release. 13 agent skills for Blender 5.2 LTS (tested on 5.2.1), distilled from about 200 expert videos (Blender Studio, Blender Conference 2019 to 2026, top instructors):

- `blender-expert` (router: execution channel, expert loop, review sheets `bx_review`, mesh audit `bx_audit`, live brushes `bx_gui`, Blender 5 API traps, bpy reliability)
- `blender-sculpting`, `blender-retopology`, `blender-uv-baking`, `blender-texturing-shading`, `blender-hair`, `blender-rigging`, `blender-animation`, `blender-previs-storyboard`, `blender-geometry-nodes`, `blender-lighting-rendering`, `blender-grease-pencil`, `blender-hard-surface`, each with a tested `bx_<domain>.py`.

Evidence at release: blind-graded written scenarios, with skills won 7 of 7 against the same model without them; execution tests better on retopology and bake + material, on par or better on sculpting after refactor, on par on a bouncing ball; all 12 test suites pass headless on Blender 5.2.1.

Known limits: headless sculpting reaches concept quality (finished surfaces need real brushes in a live session); hair-curve and Grease Pencil draw strokes cannot be scripted; procedural retopology still needs a human pass on the finest face loops.

Also in this release: SKILL.md descriptions quoted so the frontmatter is strict YAML (9 of 13 previously relied on lenient parsers).
