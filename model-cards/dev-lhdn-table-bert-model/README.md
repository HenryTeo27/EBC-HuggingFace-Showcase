---
library_name: transformers
pipeline_tag: text-classification
tags:
  - bert
  - document-processing
  - table-selection
  - lhdn
  - ebc
---

# LHDN Table Classifier · BERT · Development

A BERT text classifier for the table-selection part of the acceler-technology team's LHDN document-processing project. This development checkpoint supports the team's work on identifying relevant table-related text.

**中文简介：** 团队用于 LHDN 文档表格选择相关工作的 BERT 文本分类开发模型，输入是文本。

## Purpose and model details

The model encodes text and predicts a class. It provides a classification approach alongside the team's Donut image parser and T5 text parser. It does not directly detect table boundaries in an image or extract individual cells.

| Item | Value |
| --- | --- |
| Role | Development checkpoint |
| Architecture | `BertForSequenceClassification` |
| Task setting | Single-label classification |
| Encoder layers / hidden size | 12 / 768 |
| Maximum input positions | 512 |
| Tokenizer | Lowercasing `BertTokenizer` |
| Saved Transformers version | 4.52.4 |

Sources: [config.json](https://huggingface.co/acceler-technology/dev-lhdn-table-bert-model/blob/main/config.json) and the saved tokenizer configuration. Class meanings are not documented in the configuration; confirm the training label map before interpreting predictions.

## Load the model

Install `torch` and `transformers` first.

```python
from transformers import AutoTokenizer, AutoModelForSequenceClassification

model_id = "acceler-technology/dev-lhdn-table-bert-model"
tokenizer = AutoTokenizer.from_pretrained(model_id)
model = AutoModelForSequenceClassification.from_pretrained(model_id)
model.eval()
```

This example loads the model. Prepare input text as in training. Long text needs a chunking or truncation policy within the 512-position limit.

## Project and limitations

Related project data is held in [lhdn-dataset](https://huggingface.co/datasets/acceler-technology/lhdn-dataset), which remains private. The exact training subset, full recipe, and quantitative evaluation results are not documented here.

Unfamiliar documents and text-extraction errors can affect classification. Review predictions before downstream use. The model does not determine tax or legal outcomes.

## Team and links

Developed within [acceler-technology](https://huggingface.co/acceler-technology). Henry ([HenryTeo27](https://huggingface.co/HenryTeo27)) led this project area, executed the data work, and participated in model training and technical discussions. [kwyong](https://huggingface.co/kwyong) handled model uploads.

[Project showcase](https://github.com/HenryTeo27/EBC-HuggingFace-Showcase) · [Production BERT snapshot](https://huggingface.co/acceler-technology/prod-lhdn-table-bert-model)

A license has not been specified for this checkpoint. Public visibility alone does not grant unrestricted reuse rights.
