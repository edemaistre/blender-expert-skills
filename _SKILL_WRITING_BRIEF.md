# Skill-writing brief (read fully before writing)

## Goal
Turn the distilled expert notes into a skill that makes Claude Opus 5.5, driving Blender 5.2.1 LTS through Python, work like the experts in the source videos. Opus already knows textbook Blender (baseline answers: `tests/baseline/answers.md`, read the scenario for your domain to see what it already does well and where it is generic, untested or wrong). The skill must carry the EXPERT DELTA plus tested agent procedures, not a textbook.

## Inputs
- Your domain's notes and digests: `notes/<category>/` (digests are `_digest_*.md`; read ALL notes, not only digests).
- Version changes: `sources/blender-version-deltas.md` (authoritative for 5.2 API/UI facts).
- Shared toolkit already built and tested (use it, do not duplicate it):
  - `skills/blender-expert/scripts/bx_audit.py`: mesh audit (quads %, n-gons, poles, valence, manifold, flipped, self-intersections, symmetry, edge-length CV, fidelity to a high poly). `audit(obj, high=None)`, `verdict(report)`.
  - `skills/blender-expert/scripts/bx_review.py`: headless Workbench review sheet `review(objs, out_dir, views, modes)` with modes silhouette / matcap / wire / normals and views front/back/left/right/top/threequarter/low; `playblast(path)`; `turntable(obj, path)`.
  - `skills/blender-expert/scripts/bx_gui.py`: REAL Blender brushes in a live GUI session (MCP bridge): `set_view`, `activate_brush(mode, name)`, `stroke(mode, world_points, size, strength)`, `run(op, **kw)` for ops needing a 3D view, `set_paint_color`. Verified for sculpt, texture paint, weight paint, mask flood fill, dyntopo strokes.
  - `skills/blender-sculpting/scripts/bx_sculpt.py`: numpy brush equivalents for headless (draw, inflate, clay, layer, flatten, fill, scrape, pinch, crease, smooth, grab, mask), `union_remesh` blockouts, `voxel_remesh`, `ellipsoid`, `subdivide_to`.
  Read the docstrings of these files before writing.

## Output: `skills/blender-<domain>/`
```
SKILL.md                    core playbook, 1,200 to 2,200 words
references/expert-notes.md  the depth: principles and judgment by expert, with source + timestamp
references/procedures.md    tested bpy procedures (full code), each with "verified on 5.2.1" and the test script path
references/critique.md      the rubric the agent uses to judge its own output (what experts look at)
references/sources.md       every source video: expert, credential, URL, what it is best for, best timestamps
scripts/<module>.py         only if you add reusable, tested code (name it bx_<domain>.py)
```

### SKILL.md shape
```
---
name: blender-<domain>
description: Use when <triggers: tasks, symptoms, keywords an agent would search>. Third person, starts with "Use when", no workflow summary, under ~600 characters.
---
# <Title>

<2-3 sentences: what expert-level means in this domain and the core stance.>

**REQUIRED BACKGROUND:** blender-expert (execution channel, review loop, 5.2 API changes).

## Stance (the expert delta)
5 to 8 bullets, each a non-obvious rule with its reason, attributed ("Kaspar:", "Lampel:").

## Establish first
The inputs that change the plan (budget, target engine or render, style, deformation needs) and the default the agent assumes when the brief is silent.

## Workflow
Numbered stages in the order experts actually work. Each stage: goal, how (toolkit call or bpy operator, headless vs GUI), GATE: what must be true before moving on (measurable + visual).

## Numbers
Compact table of the concrete values experts use, with what they are relative to.

## Quality gates
Measurable in code (with the bx_audit / bx_review call or a snippet) and visual (which review views/modes, and what to look for).

## Common mistakes
Table: mistake | what it looks like | fix.

## Blender 5.2 notes
Only the version traps relevant here.

## References
One line per reference file saying when to load it.
```

## Rules
- Every bpy snippet you ship must run on the installed Blender 5.2.1: write a test script under `tests/code/blender-<domain>/`, run it with `blender --background --factory-startup --python <script>`, and keep the script. Mark anything you could only verify in GUI as "GUI only, not run headless". Remember: sculpt/paint strokes need a GUI session (use bx_gui); `paint.mask_flood_fill` and `sculpt.mesh_filter` crash headless.
- Attribute expert claims; mark your own additions [added]. Never invent numbers. When experts disagree, give the deciding condition.
- Keep it a flexible toolkit, not one rigid recipe: where experts offer alternatives (stylized vs realistic, games vs film), present them as options keyed to the brief.
- Descriptions trigger discovery: include the words users actually say (e.g. "sculpt a head", "retopo", "clean up an AI-generated mesh", "walk cycle", "rig this character").
- Link other skills by name only (e.g. "then blender-uv-baking"), never with @ paths.
- No em dashes anywhere. Plain, dense English.
- Write only inside `skills/blender-<domain>/` and `tests/code/blender-<domain>/` (plus temp files in `archive/tests/`).
- Final reply (under 200 words): files written, word count of SKILL.md, which snippets were verified, open questions.
