# 与六个相关项目配合使用

核对日期：2026-10-24。本文提供基于上游文档的使用方法、可复制提示词和本仓库的 Claude Code 插件入口；各软件中的实际效果仍需用自己的材料验证。项目名称链接到各自上游，具体安装和界面以所用版本为准。

本仓库保存个人写作规则。文档工具整理材料，专业技能支持分析，润色技能修改已有文字，知识库帮助查找材料。它们可以按需配合，不需要全部安装。本仓库没有复制第三方技能源码，也没有把六个项目合并为一个软件。

## 先选择使用方式

| 当前需要 | 可以采用的组合 |
|---|---|
| 已经使用支持 Skills 的 AI，只想把报告写出来 | 本技能 + 本次题目和真实材料 |
| 需要逐节组织材料或处理 Word/PDF | 本技能 + Anthropic 的相关技能 |
| 要做统计、空间分析、计算或绘图 | 本技能 + Scientific Agent Skills 中相关且可用的技能 |
| 初稿已完成，想改中文表达 | 本技能 + Humanizer-zh |
| 有英文摘要或希望进一步参考作者语气 | 本技能 + Humanizer，提供对应语言的写作样本 |
| 希望图形界面长期管理范文和课程资料 | AnythingLLM 或 Cherry Studio + 本仓库的规则与提示词 |

这里的分工是本仓库针对课程报告的建议，不是上游项目对写作效果的保证。

## 1. Anthropic Skills：写作协作与文档处理

上游：[anthropics/skills](https://github.com/anthropics/skills)。其中 `doc-coauthoring` 可辅助组织和修改文档，`skill-creator` 可用于改进技能，文档技能可处理相应文件类型。按任务选择，本仓库继续负责个人表达习惯。

先安装本仓库插件。以下命令输入 **Claude Code 对话框**：

```text
/plugin marketplace add mengyoutianji-ux/course-lab-report-skill
/plugin install course-lab-report@course-report-skills
```

按界面完成安装和启用后，使用 `/course-lab-report:course-lab-report`。本仓库的 `.claude-plugin/plugin.json` 声明插件，`marketplace.json` 提供安装目录，实际技能在 `skills/course-lab-report` 中。参见 [Claude Code 插件文档](https://code.claude.com/docs/en/plugins-reference)。

需要 Anthropic 的相关技能时，再在 **Claude Code 对话框**使用上游提供的方式：

```text
/plugin marketplace add anthropics/skills
/plugin install example-skills@anthropic-agent-skills
/plugin install document-skills@anthropic-agent-skills
```

`example-skills` 和 `document-skills` 是两个可选插件；只安装任务需要的部分。安装与名称依据 [上游 README](https://github.com/anthropics/skills#using-in-claude-code)。

可发送：

> 请以 course-lab-report 的写法为主，先依据本次题目和材料整理证据。需要梳理结构时使用已启用的 doc-coauthoring，需要读取或生成文档时使用可用的文档技能。结果段解释具体证据，保留课程模板；不要为了填满结构而编造内容。

使用 `skill-creator` 修订规则时，输入已确认的修改意见和新样本；先比较现有规则与实际反馈，避免把一次任务的特殊格式变成所有课程的规定。

## 2. AnythingLLM：规则提示词与可检索材料

上游：[Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm)。采用“工作区提示词 + 文档”的方式，不把 Claude Code 的插件配置当作 AnythingLLM 插件导入。

1. 创建用于课程实验报告的工作区，并配置可用的模型。
2. 把 [assistant-system.md](../integrations/prompts/assistant-system.md) 的全文粘贴到工作区的系统提示词设置中。
3. 将 [writing-profile.md](../skills/course-lab-report/references/writing-profile.md) 和 [examples.md](../skills/course-lab-report/references/examples.md) 作为风格资料导入工作区。涉及排版时再加入 [layout-and-sources.md](../skills/course-lab-report/references/layout-and-sources.md)。
4. 长期复用的资料放入工作区的嵌入文档；本次题目、实际输出和截图按本次任务添加。检查解析文字是否完整，并区分旧样本和当前实验。
5. 如果关键风格规则经常未被检索到，可在上下文容量允许时固定较短的规则文档；固定前需要先完成嵌入。

聊天附件受会话范围限制，工作区嵌入文档才能跨会话复用；检索通常只提供相关片段。仅把 `SKILL.md` 当文档上传，并不等于每条规则都会进入每次回答，所以核心规则另放在系统提示词中。相关机制见 [AnythingLLM 文档使用说明](https://docs.anythingllm.com/chatting-with-documents/introduction)。

首次试写前可发送：

> 请依据已检索到的写作规则，说明“操作说明”和“实验思考”分别应写什么，并标出依据的文件或段落。随后只根据我提供的本次结果写一个分析段；缺少当前结果时不要引用旧范文中的数值来补齐。

## 3. Humanizer：已有文本的语气修改

上游：[blader/humanizer](https://github.com/blader/humanizer)。其说明支持提供作者样本辅助调整表达。可用于已有英文段落，也可按实际语言效果选择；中文报告可先采用下一节中的 Humanizer-zh。

按上游说明安装到当前客户端。在 Claude Code 使用插件安装时，以下命令输入 **Claude Code 对话框**；上游当前说明要求 Claude Code 2.1.142 或更新版本：

```text
/plugin marketplace add blader/humanizer
/plugin install humanizer@humanizer
```

启用后插件技能名为 `/humanizer:humanizer`；独立技能安装方式的名字可能不同，以客户端实际显示为准。参见 [Humanizer 安装与用法](https://github.com/blader/humanizer#installation)。

配合请求：

> 请先遵循 course-lab-report 中与本段相关的写法，再参考我提供的同语言样本，用 Humanizer 修改已有正文。保留事实、单位、公式、引用、实验条件与结论范围。只修改需要改善的表达，不添加经历或结果。发现事实疑点请单独指出。

## 4. Scientific Agent Skills：分析与图表能力

上游：[K-Dense-AI/scientific-agent-skills](https://github.com/K-Dense-AI/scientific-agent-skills)，原名 Claude Scientific Skills。按当前问题从上游目录中选择统计分析、地理空间分析、绘图或引用相关技能，并按各技能说明准备实际依赖。目录中的技能可用性，以当前客户端中已安装和启用的内容为准。

推荐交接方式：问题和数据 → 实际分析及检查 → 方法、参数和结果记录 → 按本仓库规则起草分析段。专业工具负责计算或核查，本技能负责解释“为什么这样做、结果说明什么、适用到哪里”。

可发送：

> 先判断本次地理建模问题需要哪种分析，只使用已可用且相关的专业技能。保留数据范围、变量单位、方法条件和实际输出，再按 course-lab-report 的风格写结果分析。不要把尚未运行的分析写成结果，也不要将相关解释成因果；篇章结构服从课程模板。

技能安装不等于其 Python 库、外部服务或数据已经可用。先验证当前任务所需的一项能力即可。官方目录和依赖说明见 [上游 README](https://github.com/K-Dense-AI/scientific-agent-skills#-getting-started)。

## 5. Cherry Studio：助手、知识库或直接使用技能

上游：[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)。可以根据当前版本选择两种方式。

**普通助手与知识库：** 创建“课程实验报告”助手，在编辑助手的 Prompt 中粘贴 [assistant-system.md](../integrations/prompts/assistant-system.md)。将写作规则和例证加入知识库，检查解析内容及检索结果，再在对话中选用该知识库，提供本次实验材料。助手提示词和知识库分别承担规则与资料的作用。见 [助手设置](https://cherryai.com/docs/en/cherrystudio/preview/chat/) 和 [知识库指南](https://cherryai.com/docs/en/knowledge-base/knowledge-base/)。

**支持 Agent Skills 的版本：** 在“设置 → Skills → 添加技能”选择本地导入，将整个 `skills/course-lab-report` 文件夹导入，保留 `references` 子目录。也可在 GitHub 导入入口提供本仓库的 [SKILL.md 链接](https://github.com/mengyoutianji-ux/course-lab-report-skill/blob/main/skills/course-lab-report/SKILL.md)，并检查参考文件是否一并可读；若未导入完整，改用本地文件夹。

导入后，确认全局开关已打开，再到“Work → Agent 菜单 → 编辑 → Skills”对所用 Agent 启用本技能。新消息中测试规则及参考文件能否被读取。界面步骤依据 [Cherry Studio 技能指南](https://cherryai.com/docs/en/advanced-basic/extensions/skills/)。

如果当前版本没有这些入口，先使用普通助手提示词和知识库方案；不需要为了采用本仓库规则而同时配置 MCP。

## 6. Humanizer-zh：中文报告最后一轮修改

上游：[op7418/Humanizer-zh](https://github.com/op7418/Humanizer-zh)。按照上游说明在当前客户端安装并启用后，使用 [polish-zh.md](../integrations/prompts/polish-zh.md)，补入课程要求、相关风格样本和待修改正文。

本仓库建议在事实和结果明确后使用它，重点改善重复、空泛和模板化表达。必要的连接词、对照条件、技术重复和有依据的第一人称应保留；修改不能把有限结论扩大为普遍结论。上游也明确其用途是中文编辑，不是判定作者身份或保证检测器结果。

## 用一个小任务核验

先确认当前客户端实际加载了规则，或知识库能找出相关段落。然后把下面的**虚构演示材料**交给助手试写，不能作为真实报告结果使用：

> 在相同的 30 个验证点上，方法 A 的 MAE 为 4.2 m，方法 B 的 MAE 为 3.6 m。两者使用相同数据和预处理，只改变插值方法。尚未进行显著性检验。请写一个简短结果分析段，并保留结论范围。

检查输出是否保留相同验证条件、单位和比较方向，能否围绕具体误差解释差异，同时没有虚构显著性检验或把结果推广到所有地区。再提供一小段自己的真实范文，检查句式、解释节奏和正式程度是否接近预期。

如果事实表达正确但语气不合适，调整写作规则或样本；如果找不到资料，先检查导入和检索；如果计算或文档处理未运行，不能把它记作验证通过。插件格式校验、资料检索和写作效果是不同层面的检查。

## 发布和更新

仓库仅公开匿名规则、必要节选、提示词和配置。个人原始报告和本次任务材料不随这些集成说明发布。上游软件按其各自许可和安装方式使用，本仓库不声明上游背书。

更新本仓库后，已复制到本地的技能、已粘贴的系统提示词以及知识库中的文档需要相应更新；它们不会因为 GitHub 文件变化就自动保持同步。
