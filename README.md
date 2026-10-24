# 课程实验报告写作 Skill

一套面向中文大学实验报告的写作规则，帮助 AI 说明方法选择、记录关键操作、解释图表结果，并写出有实际依据的实验思考。适用于 GIS、地理建模、WebGIS、科学计算和 C++ 等课程。

当前版本：**v0.2.0**。规则由 7 份历史报告归纳，提供者已核验关键内容；实际风格匹配仍需通过新稿反馈调整。它通过规则和例子引导写作，不涉及模型训练。

## 快速使用

让 AI 先读取 [Skill 入口](skills/course-lab-report/SKILL.md)，再提供本次题目、课程模板、数据、操作记录、截图或代码。可以直接使用下面的请求：

> 请先读取 skills/course-lab-report/SKILL.md 及当前任务需要的参考文件。根据本次题目、数据和图表组织实验报告，解释方法的理由、关键操作和结果含义。先从材料最充分的结果段写起，最后补齐目的与总结；缺少的事实不要补造。

在支持 `SKILL.md` 的工具中，将整个 `skills/course-lab-report` 文件夹放入该工具的技能目录，并保留 `references` 子目录。其他 AI 工具也可以直接读取或接收入口及参考文件。

本次课程要求和用户指定模板优先。若希望贴合自己的表达，可再提供同课程范文，让 AI 依据新样本调整规则。

## 与其他项目配合

本仓库负责个人写作规则；下面的项目按任务提供辅助能力。它们都是可选项，安装本仓库不会自动安装或启用第三方工具，也不代表与上游存在官方合作关系。

| 项目 | 在实验报告中的作用 | 本仓库提供的配合方式 |
|---|---|---|
| [Anthropic Skills](https://github.com/anthropics/skills) | 整理材料、协作起草、处理 Word/PDF、改进技能 | Claude Code 插件入口，以及与 `doc-coauthoring`、`skill-creator`、文档技能的分工 |
| [AnythingLLM](https://github.com/Mintplex-Labs/anything-llm) | 检索课程材料和历史范文 | 工作区系统提示词、知识库导入清单与检索检查 |
| [Humanizer](https://github.com/blader/humanizer) | 参考作者样本润色已有文本 | 保留作者语气及实验事实的调用方式，可用于英文段落 |
| [Scientific Agent Skills](https://github.com/K-Dense-AI/scientific-agent-skills) | 统计、地理分析、绘图和引用管理 | 按当前问题选择技能，分析结果回到本仓库的报告写法 |
| [Cherry Studio](https://github.com/CherryHQ/cherry-studio) | 管理写作助手、知识库和 Agent Skills | 助手提示词、知识库方案，以及本技能的导入和启用说明 |
| [Humanizer-zh](https://github.com/op7418/Humanizer-zh) | 修改中文空话、重复及模板化表达 | 一份保留事实、限定条件和个人写法的润色提示词 |

完整步骤见 **[六个项目的配合使用指南](docs/integrations.md)**。可以先使用本技能完成一小段报告，需要中文润色时再加入 Humanizer-zh；需要长期管理材料时再选择 AnythingLLM 或 Cherry Studio。

### 作为 Claude Code 插件使用

下面两行输入 **Claude Code 对话框**，不是 PowerShell：

```text
/plugin marketplace add mengyoutianji-ux/course-lab-report-skill
/plugin install course-lab-report@course-report-skills
```

完成界面中的安装并确认插件已启用后，可使用 `/course-lab-report:course-lab-report`，再附上本次材料。插件包含的仍是同一套写作规则。其他客户端请使用上面的技能文件夹方式或配合使用指南，不要直接套用这些 Claude Code 命令。

## 核心写法

1. 用当前任务或数据中的具体问题解释方法选择。
2. 操作段写清工具、输入、关键参数、输出和检查点。
3. 图表附近说明值得关注的数值、位置或变化。
4. 结果分析给出具体证据，再解释意义和适用范围。
5. 对照实验说明保持不变的条件与改变的因素。
6. 实验思考呈现判断如何被实际现象修正。
7. 用完整段落衔接思路，避免机械模板和重复总结。

例如，样本没有只写“删除短线可以改善数据”，而是进一步讨论真实等高线也可能形成短片段，因此删除后仍需检查并补线。这里学习的是“操作收益—可能误判—核查修正”的思考过程，具体阈值不能直接迁入新实验。

## 按课程选择结构

| 类型 | 参考组织方式 |
|---|---|
| GIS 软件操作 | 目的与数据 → 原理或路线 → 操作与过程分析 → 成果 → 问题与思考 |
| 地理建模与统计 | 问题与变量 → 方法条件 → 初步图形 → 主分析 → 必要对照或分组 → 有范围的结论 |
| WebGIS 系统设计 | 需求 → 架构与数据 → 关键实现 → 实际运行 → 测试与不足 |
| 科学计算 | 题目与输入 → 算法或公式 → 实现要点 → 数值表与曲线 → 误差解释或对照 |
| C++ 调试 | 环境与理论 → 断点、变量或调用栈观察 → 程序行为 → 输出或边界用例 → 改进方向 |

这些顺序可以按题目调整。摘要、目录、创新点、独立验证章节，以及字号、行距、纸型和表格配色，都不作为每份报告的统一要求。

## 文件导航

| 文件 | 内容 |
|---|---|
| [SKILL.md](skills/course-lab-report/SKILL.md) | 使用时机、优先顺序、核心规则及交付检查 |
| [writing-profile.md](skills/course-lab-report/references/writing-profile.md) | 写作习惯、课程适配和无法动笔时的起草入口 |
| [examples.md](skills/course-lab-report/references/examples.md) | 8 组匿名样本例证，以及一组试写比较 |
| [layout-and-sources.md](skills/course-lab-report/references/layout-and-sources.md) | 匿名样本说明、版式差异和格式选择规则 |
| [tool-cooperation.md](skills/course-lab-report/references/tool-cooperation.md) | 多个技能同时可用时的分工、交接和冲突处理 |
| [integrations.md](docs/integrations.md) | 六个相关项目的接入方法和官方来源 |
| [assistant-system.md](integrations/prompts/assistant-system.md) | 可粘贴到 AnythingLLM 或 Cherry Studio 的完整助手提示词 |
| [polish-zh.md](integrations/prompts/polish-zh.md) | 中文报告最后一轮润色请求 |
| [plugin.json](.claude-plugin/plugin.json) / [marketplace.json](.claude-plugin/marketplace.json) | Claude Code 插件元数据和安装入口 |

## 样本与事实的边界

公开内容包括规则、必要节选和版式记录。原始报告、全文提取、页面图像及本机审计文件不随仓库发布；样本以 S1—S7 标识。

旧样本中的数值、图号、软件版本和“测试通过”只属于对应历史实验。新报告的事实必须来自本次材料，不能为了模仿叙述而编造结果、错误经历或个人感受。

维护账号：[mengyoutianji-ux](https://github.com/mengyoutianji-ux)。
