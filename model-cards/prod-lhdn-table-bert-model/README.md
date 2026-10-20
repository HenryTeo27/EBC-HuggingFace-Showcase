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

# LHDN Table Classifier · BERT · Production Snapshot

A production snapshot of the acceler-technology team's BERT classifier for LHDN table-related text. It preserves released model and tokenizer files separately from the development checkpoint.

**中文简介：** 团队 BERT 表格相关文本分类模型的生产快照，保存独立于开发仓库的发布版本。

## Purpose and model details

The model predicts a class from input text for the team's table-selection work. It does not directly read document images, detect table boundaries, or extract individual cells.

| Item | Value |
| --- | --- |
| Role | Production snapshot |
| Architecture | `BertForSequenceClassification` |
| Recorded source | `acceler-technology/dev-lhdn-table-bert-model` |
| Task setting | Single-label classification |
| Encoder layers / hidden size | 12 / 768 |
| Maximum input positions | 512 |
| Tokenizer | Lowercasing `BertTokenizer` |
| Saved Transformers version | 4.48.2 |

Sources: [config.json](https://huggingface.co/acceler-technology/prod-lhdn-table-bert-model/blob/main/config.json) and the saved tokenizer configuration. Use this repository's tokenizer with its weights. Confirm the training label map before interpreting predictions. The `prod` name identifies a release snapshot; it does not establish a current live deployment.

## Load the model

Install `torch` and `transformers` first.

```python
from transformers import AutoTokenizer, AutoModelForSequenceClassification

model_id = "acceler-technology/prod-lhdn-table-bert-model"
tokenizer = AutoTokenizer.from_pretrained(model_id)
model = AutoModelForSequenceClassification.from_pretrained(model_id)
model.eval()
```

This example loads the saved artifacts. Input preparation must match training. Long text needs a chunking or truncation policy within the 512-position limit.

## Project and limitations

Related project data is held in [lhdn-dataset](https://huggingface.co/datasets/acceler-technology/lhdn-dataset), which remains private. The exact training subset, full recipe, and quantitative evaluation results are not documented here.

Unfamiliar documents and text-extraction errors can change classification results. Review predictions before downstream use. The model does not determine tax or legal outcomes.

## Team and links

Developed within [acceler-technology](https://huggingface.co/acceler-technology). Henry ([HenryTeo27](https://huggingface.co/HenryTeo27)) led this project area, executed the data work, and participated in model training and technical discussions. [kwyong](https://huggingface.co/kwyong) handled model uploads.

[Project showcase](https://github.com/HenryTeo27/EBC-HuggingFace-Showcase) · [Development BERT model](https://huggingface.co/acceler-technology/dev-lhdn-table-bert-model)

A license has not been specified for this checkpoint. Public visibility alone does not grant unrestricted reuse rights.
