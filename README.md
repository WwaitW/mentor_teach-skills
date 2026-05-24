# Personal Claude Skills

Personal skills for Claude Code, built on top of the [superpowers](https://github.com/superpowers-ai/superpowers) framework.

## Skills

### `learner-profile`

Analyzes your git repositories to build and maintain a personalized technical profile. Run once to initialize, then after each completed project to update.

**Usage:** Invoke the `learner-profile` skill and provide your repository paths.

### `mentor-overlay`

A teaching overlay for superpowers sessions. Reads your learner profile and appends personalized mentoring content after each superpowers output — without interfering with project delivery.

**Features:**
- Dynamic role switching (Frontend Architect / Backend Engineer / DBA / Platform Engineer / etc.)
- Explanation depth adapts to your proficiency level per technology
- Phase-based assessment after completing each feature module
- Tracks learning progress in per-project `docs/mentor-log.md`

**Usage:** Invoke at session start alongside `using-superpowers`.

## Data Files

These files are created locally and not tracked in this repo:

- `~/.claude/learner-profile/global-profile.md` — your global tech proficiency table (stays compact, < 200 lines)
- `~/.claude/learner-profile/knowledge-map.md` — cross-project knowledge index
- `{project}/docs/mentor-log.md` — per-project learning log

## Workflow

```
# One-time setup
invoke learner-profile → provide repo paths → generates global-profile.md

# Each new project session
invoke using-superpowers  (auto-triggered at session start)
invoke mentor-overlay     (reads your profile, enables teaching)

# After completing a project
invoke learner-profile → provide project path → updates global-profile.md
```

## Installation

```bash
# Via Claude Code skills system
# Add to your skills directory or install from this repo
```
