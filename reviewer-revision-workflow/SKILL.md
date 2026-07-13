---
name: reviewer-revision-workflow
description: "中文优先的自包含论文审稿返修与 Response to Reviewers 协作流程，无需另建 AGENTS.md。Use when the user provides reviewer comments, a revision plan, Chinese or English manuscripts, DOCX files, or asks to discuss, revise, translate, track, or finalize manuscript changes and reviewer responses. Produces bilingual, directly copyable manuscript edits and response-letter text with insertion anchors."
---

# Manuscript Revision and Reviewer Response Workflow

按照用户主导的修改计划，把审稿意见转化为可直接复制的中英文稿件修改文本和 Response to Reviewers 内容。此 Skill 自包含全部返修规则；使用者无需创建或提供 `AGENTS.md`。保持学术严谨、最小必要改动，并让稿件与回信对同一问题保持一致。

## 内置工作规则

1. 若环境中已安装 `nature-polishing`，优先调用它检查学术表达、论证边界和中英术语；未安装时，仍执行本 Skill 的最小改动、严谨表达和术语一致性要求。
2. 开始返修时，读取审稿意见、意见汇总、回复提示词、英文原稿和中文原稿，理解各文件用途后再处理审稿意见。默认文件映射见“文件与版本管理”；使用者可以替换为任何实际文件名。
3. 在每个新会话的首轮，先用简洁文字说明对本工作流的理解，再请用户提供第一条审稿意见。
4. 在可使用协作 Agent 的环境中，同时启动两个 Agent：Agent 1 只负责英文稿与中文稿的对应修改；Agent 2 只负责 `Response-to-Reviewers.docx` 的回信。主 Agent 只统筹、核对和反馈两个 Agent 的最终结果，不擅自润色、删改或改写。向用户反馈时，保留两个 Agent 的文本为可直接复制版本，并确保同一审稿问题的事实、术语、修改理由、图表编号和章节名称一致。
5. 对困难或复杂问题，先与用户讨论修改计划；在用户确认计划前，不生成最终稿件改动或回信。确认后再按两个 Agent 的职责分别完成。
6. 对通常的单条任务，接收“审稿人意见 + 用户拟修改方案”，同步交付稿件修改与审稿回信两个部分，而非只给建议。
7. 所有面向用户的实质性内容均提供英文可复制版本和中文核对版本；英文用于提交，中文用于作者确认。
8. Agent 1 必须尽可能少改动原文，保持学术语言严谨，不通过堆积字数来回应审稿意见。
9. 始终把用户现有文件视为可能已更新的版本；开始新一轮修改前确认使用的是最新中英文稿件。若多个候选文件无法判断，应请用户指定，不混用版本。
10. Agent 2 可结合原稿已有图表，或作者提供的图表和数据，写入有助于解释审稿意见的说明，以提高回信的可读性。
11. 在回信的 `Author action` 中，修改定位先使用 `In Section X, Page XX, lines XX-XX.` 形式。不要在没有定稿依据时猜测真实页码或行号；定稿后再补齐。
12. 当对话明显接近上下文上限，或已积累多条完成的审稿意见时，主动建议整理记录。只有用户同意后，才创建或更新 `Reviewing memory.md`；若文件已存在，读取既有格式后在末尾追加，绝不覆盖。归档后提醒用户上传最新中英文稿件，并以新文件为后续修改基准。
13. 每次新会话都逐项确认第 2–12 条仍然生效，避免长期返修时规则被淡化；确认可以简洁，但不得漏掉核心约定。

## 文件与版本管理

默认将以下文件分别视为审稿意见、意见汇总、回复要求、英文稿和中文稿：`审稿意见修改建议.md`、`意见整理.docx`、`审稿回复提示词.txt`、`原稿英文.docx`、`原稿中文.docx`。`Response-to-Reviewers.docx` 是回信目标文件。名称仅为默认映射；用户可在首轮声明实际文件，例如“英文稿为 `manuscript_v3.docx`”，随后始终按该映射工作。

按第 1 条执行 `nature-polishing` 的可用性检查。

## 执行模式

- 用户要求“讨论”“分析方案”或明确表示尚未决定如何修改时，进入讨论模式，只讨论修改计划、证据和回应策略。
- 用户提供一条审稿意见和拟修改方案时，进入执行模式，按下述双 Agent 分工生成最终文本。
- 用户要求补页码、行号、汇总修改或准备定稿时，进入定稿模式，补充真实定位并按用户同意更新记忆。

## 双 Agent 分工

向两个 Agent 提供相同的审稿意见、用户修改计划、最新稿件上下文、相关图表和本 Skill 的内置规则。不要把一个 Agent 的草稿交给另一个 Agent 重写。

### Agent 1：稿件修改

只编写英文原稿和中文原稿的对应修改内容。每一项必须提供英文可复制文本、中文可复制文本、修改类型（替换/插入/删除），以及准确的插入锚点。锚点必须给出英文稿和中文稿中修改位置前后的原文。保持原论文术语、数据、章节逻辑和学术语气。

### Agent 2：Response to Reviewers

只编写 `Response-to-Reviewers.docx` 的回信内容。提供英文可复制版本及中文核对译文，并用 `**粗体**` 标示回信中的重点改动、关键新增信息或核心澄清。善于使用原稿已有图表或作者提供图表，并准确保留图表编号和可核对的描述。每一条均附带 `Author action` 占位定位。

### 主 Agent：统筹反馈

不二次润色两个 Agent 的最终文本。按 [references/output-contract.md](references/output-contract.md) 的顺序并列反馈其结果，核对一致性；如发现不一致，明确列出差异并请用户决定，或让对应 Agent 重做。若当前环境不支持协作 Agent，说明原因，并严格按 Agent 1、Agent 2 的角色顺序完成同等内容。

## 交付要求

始终先给英文最终可复制文本，再给一一对应的中文核对文本。每条审稿意见都要同时包含稿件修改和回信内容，除非用户明确只要求其中一项。只使用原文前后句作为稿件定位锚点；直到用户提供定稿文件，才将 `XX-XX` 更新为真实行号。

## Windows、Python 与文本兼容

处理 Python 任务时，优先使用用户指定的 Python 或 Conda 环境；如果用户未指定，先确认环境，不自行安装依赖。读取纯文本时使用 UTF-8。PowerShell 向 Python 传递中文文件名时，使用 Unicode 转义或等效的可靠路径传递方式，避免中文路径变成问号。这些规则直接由本 Skill 提供，不依赖项目额外配置文件。

## 记忆与版本归档

仅在用户同意后，按 [references/output-contract.md](references/output-contract.md) 的条目结构追加 `Reviewing memory.md`。将新归档与已有条目保持同一标题层级和格式，并在定稿后补充真实页码和行号。
