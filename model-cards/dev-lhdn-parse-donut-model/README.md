---
library_name: transformers
pipeline_tag: image-to-text
base_model: naver-clova-ix/donut-base
tags:
  - donut
  - document-parsing
  - lhdn
  - ebc
---

# LHDN Document Parser · Donut · Development

A Donut-based document-image parser for the acceler-technology team's LHDN document-processing project. This repository holds the development checkpoint for the team's model training and iteration work.

**中文简介：** 团队用于 LHDN 文档图片解析的 Donut 开发模型，探索从页面图片生成文档内容的文本表示。

## Purpose and model details

Donut combines a visual encoder with a text decoder. It reads a document image and generates an output sequence without requiring a separate OCR model in the Donut architecture. PDF pages must first be rendered as images.

| Item | Value |
| --- | --- |
| Role | Development checkpoint |
| Architecture | `VisionEncoderDecoderModel` |
| Encoder / decoder | Donut Swin / mBART |
| Recorded base | `naver-clova-ix/donut-base` |
| Encoder image-size setting | `[1800, 1350]` |
| Saved Transformers version | 4.47.0 |

Source: [config.json](https://huggingface.co/acceler-technology/dev-lhdn-parse-donut-model/blob/main/config.json). Development and production snapshots have different image-size settings. Use this repository's processor alongside its weights.

## Load the model

Install `torch`, `transformers`, `sentencepiece`, and `pillow` first.

```python
from transformers import DonutProcessor, VisionEncoderDecoderModel

model_id = "acceler-technology/dev-lhdn-parse-donut-model"
processor = DonutProcessor.from_pretrained(model_id)
model = VisionEncoderDecoderModel.from_pretrained(model_id)
model.eval()
```

This is a loading example. The task prompt, image preparation, and output decoding must match the training setup. It is not a validated extraction demo.

## Project and limitations

Related project data is held in [lhdn-dataset](https://huggingface.co/datasets/acceler-technology/lhdn-dataset), which remains private. The model history records training iterations. The exact training subset, full recipe, and quantitative evaluation results are not documented here.

Poor scans and unfamiliar layouts can affect generated output. Check extracted values against the source document before use. The model does not determine tax or legal outcomes.

## Team and links

Developed within [acceler-technology](https://huggingface.co/acceler-technology). Henry ([HenryTeo27](https://huggingface.co/HenryTeo27)) led this project area, executed the data work, and participated in model training and technical discussions. [kwyong](https://huggingface.co/kwyong) handled model uploads.

[Project showcase](https://github.com/HenryTeo27/EBC-HuggingFace-Showcase) · [Production Donut snapshot](https://huggingface.co/acceler-technology/prod-lhdn-parse-donut-model)

A license has not been specified for this checkpoint. Check the checkpoint's and upstream model's terms before reuse.
