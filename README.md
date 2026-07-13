# Reviewer Revision Workflow

这是一个面向中文作者的 Codex Skill 项目，用于将“审稿意见 + 作者修改计划”整理为可直接复制的中英文稿件修改内容与 Response to Reviewers。Skill 本体位于 [reviewer-revision-workflow](reviewer-revision-workflow)，发布或安装时以该目录为 Skill 根目录。所有原本写在 `AGENTS.md` 中的返修规则都已内置到 Skill；其他作者无需新建 `AGENTS.md`。

## 它做什么

该工作流将稿件修改和审稿回信明确分开：第一个 Agent 仅负责英文稿与中文稿的最小化修改文本以及准确插入锚点；第二个 Agent 仅负责重点改动加粗、包含 `Author action` 占位定位的英文回信与中文核对译文；主 Agent 只统筹并原样反馈结果，同时核对两部分的术语、事实和图表引用是否一致。

用户通常只需提供一条审稿意见和自己的拟修改方案。若问题复杂，可先要求讨论修改策略；确定后再进入可复制文本的生成。回信可结合原稿已有图表，或作者提供的图表、数据来增强说明的可读性。

## 默认文件名与替换映射

Skill 默认识别以下文件：`审稿意见修改建议.md`、`意见整理.docx`、`审稿回复提示词.txt`、`原稿英文.docx` 和 `原稿中文.docx`。这些只是默认映射，不是强制命名。实际项目可在开始时直接说明“英文稿为 `manuscript_v3.docx`、中文稿为 `中文稿_最新版.docx`”，Skill 会以该映射工作。若存在多个版本，先指定最新文件，避免把不同版本的稿件与回信混用。

`Response-to-Reviewers.docx` 是回信的目标文件；如文件名不同，也在映射中说明即可。

## 建议依赖与兼容性

如环境已安装 `nature-polishing`，Skill 会优先用它检查学术语言、论证边界和术语一致性；未安装时仍可使用本工作流。建议同时具备 DOCX 读取能力，以便定位最新稿件和已有图表。

在 Windows 项目中，使用者可在首轮指定 Python 或 Conda 环境；本项目的示例环境为 `D:\Anaconda3\envs\cu11.8t2`。Skill 会优先使用已指定环境，且不会自行下载新的 Python 依赖。读取纯文本时优先使用 UTF-8；PowerShell 向 Python 传递中文文件名时使用 Unicode 转义或等效的可靠方式，避免路径乱码。这些兼容规则已经内置，不要求使用者另建配置文件，也不要求所有 GitHub 使用者采用同一台电脑或同一个环境。

## 上下文与记忆

为避免多轮返修丢失已完成内容，当对话明显接近上下文上限或已累计多条意见时，Skill 会建议整理 `Reviewing memory.md`。只有作者同意后才创建或追加该文件；存在旧文件时只在原有格式基础上追加。归档后应上传最新中英文稿件，后续内容以新文件为准。

本工作流也保留“每次新会话重新确认规则”的做法。它有助于防止长期返修中规则被遗忘，但会增加每轮开场的篇幅；使用者可根据项目复杂度决定确认得多详细。

## 使用示例

```text
Use $reviewer-revision-workflow. English manuscript: manuscript_v3.docx;
Chinese manuscript: 中文稿_最新版.docx. Reviewer 2 commented: [paste comment].
I plan to add [your planned revision]. Please prepare the manuscript edits and response letter.
```

## 发布前

发布到 GitHub 前，建议补充合适的开源许可证，并在真实审稿意见上试用一次，确认默认文件映射、图表引用和 `Reviewing memory.md` 的格式符合你的习惯。
