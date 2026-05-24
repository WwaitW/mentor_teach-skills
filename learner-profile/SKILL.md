---
name: learner-profile
description: Analyze git repositories to build and update a personalized user technical profile. Run once to initialize, then after each completed project to update the global profile.
---

# Learner Profile — 仓库分析建档

通过分析用户的实际代码仓库，建立并维护准确的技术水平档案。

## 何时使用

- 首次初始化：用户想建立学习档案
- 完成项目后：更新档案以反映新掌握的技能
- 当 `mentor-overlay` 报告"未找到档案"时

## 执行协议

### 第一步：收集仓库路径

询问用户：
> "请提供你的仓库路径（每行一个），我将分析它们来了解你的技术背景。"

等待用户提供路径列表后继续。

### 第二步：逐一分析仓库

对每个仓库路径，依次检查：

**1. 语言分布**
- 统计各语言文件数量和代码行数
- 识别主要语言和次要语言

**2. 框架/库使用深度**
- 扫描 package.json / requirements.txt / go.mod / pom.xml 等依赖文件
- 区分：基础用法（只用简单 API）vs 高级用法（自定义插件、高级配置、性能优化）
- 示例判断：只用 `useState` + `useEffect` → 初级 React；使用 `useMemo`/`useCallback`/自定义 Hook → 中级

**3. 代码质量指标**
- 错误处理：是否有 try/catch、错误边界、自定义错误类
- 测试覆盖：测试文件数量；测试内容是否只有 happy path 还是覆盖失败场景
- 代码组织：是否有清晰的职责分层，还是所有逻辑堆在一个文件
- 注释质量：注释解释"为什么"而不只是"做什么"

**4. 架构模式**
- 是否有分层架构（controller/service/repository）
- 状态管理模式（Redux / Zustand / 无状态管理）
- API 设计风格（REST / GraphQL / RPC）

### 第三步：推断各技术水平

| 水平   | 判断标准 |
|--------|---------|
| 未涉及 | 未在任何仓库中出现 |
| 入门   | 仅有教程级别用法；无错误处理；无测试 |
| 初级   | 代码可运行；有基础错误处理；仅覆盖正常流程 |
| 中级   | 处理边界情况；有测试；理解"为什么"不只是"怎么做" |
| 高级   | 使用高级模式；关注性能；测试覆盖失败场景 |
| 专家   | 框架级理解；扩展或贡献过库 |

### 第四步：写入 global-profile.md

写入路径：`~/.claude/learner-profile/global-profile.md`

**关键约束：更新已有条目，不追加重复行。文件保持 200 行以内。**

格式：
```
# 用户技术档案
最后更新：YYYY-MM-DD

## 技术栈水平
| 技术/领域        | 水平   | 最近项目          | 更新时间   |
|-----------------|--------|------------------|-----------|
| React           | 中级   | project-shop     | 2026-05   |
| Node.js         | 初级   | project-blog     | 2026-03   |
| SQL             | 入门   | project-blog     | 2026-03   |

## 编程习惯观察
- 倾向于：[从仓库观察到的编码风格，如"函数式优先"、"喜欢提前 return"]
- 薄弱点：[反复出现的问题模式，如"错误处理不完整"、"测试覆盖不足"]
- 优势：[值得肯定的模式，如"命名清晰"、"逻辑分层合理"]
```

### 第五步：更新 knowledge-map.md

追加到 `~/.claude/learner-profile/knowledge-map.md`：

```
## {project-name} — {YYYY-MM-DD}
- 路径：{repo-path}
- 主要技术：{技术1, 技术2, 技术3}
- 涵盖知识点：{概念1, 概念2, 概念3}
```

### 第六步：向用户汇报

汇报分析结果：
> "档案已更新。
> 分析了 N 个仓库，识别到以下技术水平：
> - React：中级（较上次提升）
> - SQL：入门（新增）
>
> 全局档案：`~/.claude/learner-profile/global-profile.md`
> 知识索引：`~/.claude/learner-profile/knowledge-map.md`"
