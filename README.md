# Blender Expert Skills (13 skills, 2026-09-24)

Agent skills that make Claude (Claude Code) or Codex work in Blender 5.2 like the experts in about 200 Blender videos (Blender Studio, Blender Conference, top instructors). Start with `blender-expert/SKILL.md` (the router).

## Install

From this repo (any Mac or Linux machine):
```bash
git clone https://github.com/edemaistre/blender-expert-skills.git ~/blender-expert-skills
for d in ~/blender-expert-skills/blender-*; do
  ln -sfn "$d" ~/.claude/skills/"$(basename "$d")"     # Claude Code
  ln -sfn "$d" ~/.agents/skills/"$(basename "$d")"     # Codex and other agents
done
```
Update later with `git -C ~/blender-expert-skills pull`. For a cloud or CI agent that only sees a project repo, copy the `blender-*` folders into that project's `.claude/skills/` (Claude Code) or `.agents/skills/` (Codex).

Manual alternative:
- Claude Code: copy the 13 `blender-*` folders into `~/.claude/skills/`.
- Codex and other agents that read the shared folder: copy them into `~/.agents/skills/`.
- New sessions pick them up automatically; ask for Blender work in plain words ("sculpt a stylized head", "retopo this AI mesh", "rig and animate this character").

## Requirements
- Blender 5.2 LTS (tested on 5.2.1). Python tools live in each skill's `scripts/` (`bx_*.py`); the router's `scripts/` (`bx_audit`, `bx_review`, `bx_gui`) are shared by the others, so keep all folders side by side.
- Headless runs: `blender --background --factory-startup --python-exit-code 1 --python script.py`. Real sculpt/paint brushes need a live Blender window (e.g. through an MCP bridge).

## Note
Paths such as `/Users/emmanuel/Developer/pro/2026-09-24 Blender Expert Skills/tests/...` inside the references point to the test evidence on the build machine. They are provenance only; the skills do not need them to run.
