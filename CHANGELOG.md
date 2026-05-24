# Changelog

所有版本变更记录遵循 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.0.0/) 规范。

---

## [1.0.0] - 2026-05-24

### 新增

- `learner-profile` 技能：通过分析 git 仓库建立用户技术水平档案
  - 支持六级水平评级（未涉及 / 入门 / 初级 / 中级 / 高级 / 专家）
  - 分析维度：语言分布、框架使用深度、代码质量指标、架构模式
  - 写入 `~/.claude/learner-profile/global-profile.md`（保持 < 200 行）
  - 更新 `~/.claude/learner-profile/knowledge-map.md` 跨项目索引

- `mentor-overlay` 技能：因材施教带教叠加层
  - 第一优先级保证：项目落地完全不受干预
  - 动态角色切换（6 个子系统对应角色）
  - 解释深度按用户水平自动调整（4 档）
  - 阶段性考察（完成功能模块后触发，每次 2 题）
  - 三档评估结果：已掌握 ✓ / 理解中 △ / 待巩固 ✗
  - 学习进度写入项目 `./docs/mentor-log.md`

- `examples/` 目录：`global-profile-sample.md` 和 `mentor-log-sample.md` 示例文件
- 中英双语 README（默认简体中文，提供 `README_EN.md` 英文版）
