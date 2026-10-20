---
library_name: transformers
pipeline_tag: image-to-text
tags:
  - donut
  - document-parsing
  - lhdn
  - ebc
---

# LHDN Document Parser · Donut · Production Snapshot

A production snapshot of the acceler-technology team's Donut-based LHDN document parser. It preserves a released set of model weights and processing files separately from the development repository.

**中文简介：** 团队 Donut 文档图片解析模型的生产快照，保存一套独立于开发仓库的模型与处理配置。

## Purpose and model details

The model maps document page images to generated text representations. Its Donut Swin encoder reads the image, and its mBART decoder generates the output sequence. PDF pages need to be rendered as images before processing.

| Item | Value |
| --- | --- |
| Role | Production snapshot |
| Architecture | `VisionEncoderDecoderModel` |
| Encoder / decoder | Donut Swin / mBART |
| Recorded source | `acceler-technology/dev-lhdn-parse-donut-model` |
| Encoder image-size setting | `[1200, 2400]` |
| Saved Transformers version | 4.48.2 |

Source: [config.json](https://huggingface.co/acceler-technology/prod-lhdn-parse-donut-model/blob/main/config.json). Use this repository's processor and weights together. Its `prod` name identifies a release snapshot; it does not establish a current live deployment.

## Load the model

Install `torch`, `transformers`, `sentencepiece`, and `pillow` first.

```python
from transformers import DonutProcessor, VisionEncoderDecoderModel

model_id = "acceler-technology/prod-lhdn-parse-donut-model"
processor = DonutProcessor.from_pretrained(model_id)
model = VisionEncoderDecoderModel.from_pretrained(model_id)
model.eval()
```

This is a loading example. Use the task prompt, preprocessing, and decoding from the matching training setup before attempting inference.

## Project and limitations

Related project data is held in [lhdn-dataset](https://huggingface.co/datasets/acceler-technology/lhdn-dataset), which remains private. The exact training subset, full recipe, and quantitative evaluation results are not documented here.

Generated fields can be missing or incorrect, especially on unfamiliar layouts or poor scans. Check the format and values against the source document. The model does not determine tax or legal outcomes.

## Team and links

Developed within [acceler-technology](https://huggingface.co/acceler-technology). Henry ([HenryTeo27](https://huggingface.co/HenryTeo27)) led this project area, executed the data work, and participated in model training and technical discussions. [kwyong](https://huggingface.co/kwyong) handled model uploads.

[Project showcase](https://github.com/HenryTeo27/EBC-HuggingFace-Showcase) · [Development Donut model](https://huggingface.co/acceler-technology/dev-lhdn-parse-donut-model)

A license has not been specified for this checkpoint. Public visibility alone does not grant unrestricted reuse rights.
