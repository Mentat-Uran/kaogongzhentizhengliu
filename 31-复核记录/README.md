# 逐题独立复核记录

- 复核记录：1,597 条唯一题号。
- 固定题目内容 commit：`84ab93d4b64b61d897bece8a1c0a5bab06b4feb2`。
- 可计分：1,596 条（1,589 道单一答案，7 道多答案按完整集合评分）。
- 保留人工复核、不计分：1 条。
- 另有 6 条采用明确标注的编辑版计分；原题状态保存在 `originalPrompt`。
- 结构化逐题记录：[`复核记录.jsonl`](复核记录.jsonl)。

JSONL 一行对应一道题。`answer` 是当前计分版本的 `A`–`D` 单一选项；多答案题以 `acceptedAnswers` 保存完整答案集合。若 `activeVersion` 为 `editorial`，答案只对 `correctedStem`/`correctedOptions` 明确标注的编辑版有效；`originalPrompt` 单独保存原题状态、答案与计分资格，原题仍不确定时必须留空且不计分。`correctedExplanation` 给出独立推理或仍无法确定的具体原因，`relatedInfo` 补充考点与口径，`evidence` 保留固定题源路径、源 blob SHA、引用原图、复核依据及可用的外部数据来源。若为消除歧义而编辑了题目笔记正文，`reviewedNoteBlobSha`/`reviewedNoteSize`记录固定上游正文以外的当前正文摘要；原 `sourceBlobSha`/`sourceSize`仍保留固定上游来源。若修订了共享材料页，`reviewedMaterialPath`、`reviewedMaterialBlobSha`/`reviewedMaterialSize`记录当前材料正文摘要，`materialSourceBlobSha`/`materialSourceSize`保留原材料的固定上游摘要。

## 状态定义

- `resolved`：单一答案已核定。
- `confirmed`：独立复算确认单一答案。
- `genuine_multi_answer`：多个选项成立；`acceptedAnswers` 列出经核对的完整集合，应用按集合评分。
- `underdetermined`：现有题干或证据仍支持不止一种解释。
- `source_data_missing`：缺少必要原图、表格或原始数据。
- `source_prompt_incomplete`：题干或选项不完整。
- `official_self_contradiction`：官方答案或解析与题源数据复算结果冲突。
- `transcription_error`：题源转录错误妨碍唯一判定。

仅 `usable: true` 且答案为单一选项或完整 `acceptedAnswers` 集合的记录可计分。其他记录须保持 `answer: null`、`usable: false`。每题复核意见是独立审校，不代表考试机构官方勘误；真题和图片权利归属仍按仓库 LICENSE 与原始免责声明处理。
