# Personal Claude Skills / 个人 Claude 技能库

> Personal skills for Claude Code, built on top of the [superpowers](https://github.com/superpowers-ai/superpowers) framework.
>
> 基于 [superpowers](https://github.com/superpowers-ai/superpowers) 框架构建的个人 Claude Code 技能，在项目落地的基础上叠加因材施教能力。

---

## Skills / 技能列表

### `learner-profile` — Repository Analysis & Profile Building / 仓库分析建档

**EN:** Analyzes your git repositories to build and maintain a personalized technical profile. Run once to initialize, then after each completed project to update.

**中文：** 通过分析你的实际代码仓库，建立并维护准确的技术水平档案。首次使用时初始化，每完成一个项目后更新。

**Usage / 用法：** Invoke the `learner-profile` skill and provide your repository paths. / 调用 `learner-profile` 技能，提供仓库路径即可。

---

### `mentor-overlay` — Personalized Teaching Overlay / 因材施教带教层

**EN:** A teaching overlay for superpowers sessions. Reads your learner profile and appends personalized mentoring content after each superpowers output — without interfering with project delivery.

**中文：** 会话带教叠加层。读取你的技术档案，在每次 superpowers 输出后追加个性化带教内容——第一优先级始终是项目落地，带教内容仅作补充。

**Features / 功能特性：**

| Feature | 功能 |
|---------|------|
| Dynamic role switching (Frontend Architect / Backend Engineer / DBA / Platform Engineer / etc.) | 动态角色切换（前端架构师 / 后端工程师 / 数据库专家 / 平台工程师等） |
| Explanation depth adapts to your proficiency level per technology | 解释深度根据你在各技术的水平自动调整 |
| Phase-based assessment after completing each feature module | 每完成一个功能模块后进行阶段性考察 |
| Tracks learning progress in per-project `docs/mentor-log.md` | 在项目 `docs/mentor-log.md` 中跟踪学习进度 |

**Usage / 用法：** Invoke at session start alongside `using-superpowers`. / 在会话开始时与 `using-superpowers` 同时调用。

---

## Data Files / 数据文件

These files are created locally and not tracked in this repo. / 以下文件在本地生成，不纳入此仓库追踪。

| File / 文件 | Purpose / 用途 |
|------------|---------------|
| `~/.claude/learner-profile/global-profile.md` | Global tech proficiency table, stays compact (< 200 lines) / 全局技术水平评级表，始终保持紧凑（< 200 行） |
| `~/.claude/learner-profile/knowledge-map.md` | Cross-project knowledge index / 跨项目知识点索引 |
| `{project}/docs/mentor-log.md` | Per-project learning log / 项目学习日志 |

---

## Workflow / 工作流程

```
# One-time setup / 一次性初始化
invoke learner-profile → provide repo paths → generates global-profile.md
调用 learner-profile  → 提供仓库路径     → 生成 global-profile.md

# Each new project session / 每次新项目会话
invoke using-superpowers  ← auto-triggered at session start / 会话启动时自动触发
invoke mentor-overlay     ← reads your profile, enables teaching / 读取画像，开启带教

# After completing a project / 每次项目完成后
invoke learner-profile → provide project path → updates global-profile.md
调用 learner-profile  → 提供项目路径    → 更新 global-profile.md
```

---

## Design Principles / 设计原则

- **Priority 1 / 第一优先级：** Project delivery — superpowers workflow runs unmodified. / 项目落地——superpowers 工作流完整运行，不做任何干预。
- **Priority 2 / 第二优先级：** Personalized teaching — mentor content appends after superpowers output. / 因材施教——带教内容追加在 superpowers 输出之后。
- **Scalable architecture / 可扩展架构：** Global profile stays compact; detailed logs stay in project directories. / 全局档案保持紧凑；详细日志留在项目目录，按需加载。
