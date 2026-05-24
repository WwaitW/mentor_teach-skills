简体中文 | [English](README_EN.md)

# Personal Claude Skills

Personal skills for Claude Code, built on top of the [superpowers](https://github.com/superpowers-ai/superpowers) framework. Adds personalized teaching capabilities on top of project delivery.

---

## Skills

### `learner-profile` — Repository Analysis & Profile Building

Analyzes your git repositories to build and maintain a personalized technical profile. Run once to initialize, then after each completed project to update.

**Usage:** Invoke the `learner-profile` skill and provide your repository paths.

---

### `mentor-overlay` — Personalized Teaching Overlay

A teaching overlay for superpowers sessions. Reads your learner profile and appends personalized mentoring content after each superpowers output — without interfering with project delivery. First priority is always project delivery.

**Features:**

| Feature |
|---------|
| Dynamic role switching (Frontend Architect / Backend Engineer / DBA / Platform Engineer / etc.) |
| Explanation depth adapts to your proficiency level per technology |
| Phase-based assessment after completing each feature module |
| Tracks learning progress in per-project `docs/mentor-log.md` |

**Usage:** Invoke at session start alongside `using-superpowers`.

---

## Data Files

These files are created locally and not tracked in this repo.

| File | Purpose |
|------|---------|
| `~/.claude/learner-profile/global-profile.md` | Global tech proficiency table, stays compact (< 200 lines) |
| `~/.claude/learner-profile/knowledge-map.md` | Cross-project knowledge index |
| `{project}/docs/mentor-log.md` | Per-project learning log |

---

## Workflow

```
# One-time setup
invoke learner-profile → provide repo paths → generates global-profile.md

# Each new project session
using-superpowers auto-triggers at session start
invoke mentor-overlay  ← reads your profile, enables teaching

# After completing a project
invoke learner-profile → provide project path → updates global-profile.md
```

---

## Design Principles

- **Priority 1:** Project delivery — superpowers workflow runs unmodified.
- **Priority 2:** Personalized teaching — mentor content appends after superpowers output.
- **Scalable architecture:** Global profile stays compact; detailed logs stay in project directories, loaded on demand.
