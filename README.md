[English](README_EN.md) | 简体中文

# 个人 Claude 技能库

![版本](https://img.shields.io/badge/版本-1.0.0-blue) ![License](https://img.shields.io/badge/license-MIT-green) ![superpowers](https://img.shields.io/badge/基于-superpowers-purple)

基于 [superpowers](https://github.com/superpowers-ai/superpowers) 框架构建的个人 Claude Code 技能，在项目落地的基础上叠加因材施教能力。

---

## 技能列表

### `learner-profile` — 仓库分析建档

通过分析你的实际代码仓库，建立并维护准确的技术水平档案。首次使用时初始化，每完成一个项目后更新。

**用法：** 调用 `learner-profile` 技能，提供仓库路径即可。

---

### `mentor-overlay` — 因材施教带教层

会话带教叠加层。读取你的技术档案，在每次 superpowers 输出后追加个性化带教内容——第一优先级始终是项目落地，带教内容仅作补充。

**功能特性：**

| 功能 |
|------|
| 动态角色切换（前端架构师 / 后端工程师 / 数据库专家 / 平台工程师等） |
| 解释深度根据你在各技术的水平自动调整 |
| 每完成一个功能模块后进行阶段性考察 |
| 在项目 `docs/mentor-log.md` 中跟踪学习进度 |

**用法：** 在会话开始时与 `using-superpowers` 同时调用。

---

## 数据文件

以下文件在本地生成，不纳入此仓库追踪。

| 文件 | 用途 |
|------|------|
| `~/.claude/learner-profile/global-profile.md` | 全局技术水平评级表，始终保持紧凑（< 200 行） |
| `~/.claude/learner-profile/knowledge-map.md` | 跨项目知识点索引 |
| `{project}/docs/mentor-log.md` | 项目学习日志 |

---

## 工作流程

```
# 一次性初始化
调用 learner-profile → 提供仓库路径 → 生成 global-profile.md

# 每次新项目会话
using-superpowers 会话启动时自动触发
调用 mentor-overlay ← 读取画像，开启带教

# 每次项目完成后
调用 learner-profile → 提供项目路径 → 更新 global-profile.md
```

---

## 设计原则

- **第一优先级：** 项目落地——superpowers 工作流完整运行，不做任何干预。
- **第二优先级：** 因材施教——带教内容追加在 superpowers 输出之后。
- **可扩展架构：** 全局档案保持紧凑；详细日志留在项目目录，按需加载。
