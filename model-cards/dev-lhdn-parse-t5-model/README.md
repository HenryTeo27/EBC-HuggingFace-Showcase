---
library_name: transformers
tags:
  - t5
  - text2text-generation
  - document-parsing
  - lhdn
  - ebc
---

# LHDN Text Parser · T5 · Development

A T5 model for the acceler-technology team's LHDN document-processing project. This development checkpoint explores converting document text into structured output, complementing the team's image-based Donut approach.

**中文简介：** 团队用于 LHDN 文档文本解析的 T5 开发模型，探索将文档文本转成结构化信息。

## Purpose and model details

T5 maps an input text sequence to an output text sequence. This repository's configuration includes an `extract_json` task setting with an output length of 512 tokens. Images and PDFs need a separate text-extraction step before this text model can process their content.

| Item | Value |
| --- | --- |
| Role | Development checkpoint |
| Architecture | `T5ForConditionalGeneration` |
| Encoder / decoder layers | 12 / 12 |
| Hidden size | 768 |
| Saved Transformers version | 4.52.4 |

Source: [config.json](https://huggingface.co/acceler-technology/dev-lhdn-parse-t5-model/blob/main/config.json). The upstream checkpoint is not identified in that configuration.

## Load the model

Install `torch`, `transformers`, and `sentencepiece` first.

```python
from transformers import AutoTokenizer, AutoModelForSeq2SeqLM

model_id = "acceler-technology/dev-lhdn-parse-t5-model"
tokenizer = AutoTokenizer.from_pretrained(model_id)
model = AutoModelForSeq2SeqLM.from_pretrained(model_id)
model.eval()
```

This example loads the saved artifacts. The input format, task prefix, and output schema must match the training setup. It is not a validated extraction demo.

## Project and limitations

Related project data is held in [lhdn-dataset](https://huggingface.co/datasets/acceler-technology/lhdn-dataset), which remains private. The exact training subset, full recipe, and quantitative evaluation results are not documented here. Check generated fields against the source document before use. The model does not determine tax or legal outcomes.

## Team and links

Developed within [acceler-technology](https://huggingface.co/acceler-technology). Henry ([HenryTeo27](https://huggingface.co/HenryTeo27)) led this project area, executed the data work, and participated in model training and technical discussions. [kwyong](https://huggingface.co/kwyong) handled model uploads.

[Project showcase](https://github.com/HenryTeo27/EBC-HuggingFace-Showcase) · [Donut development model](https://huggingface.co/acceler-technology/dev-lhdn-parse-donut-model) · [BERT development model](https://huggingface.co/acceler-technology/dev-lhdn-table-bert-model)

A license has not been specified for this checkpoint. Public visibility alone does not grant unrestricted reuse rights.
