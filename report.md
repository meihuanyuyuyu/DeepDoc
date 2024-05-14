# 复杂文档分析

目前LLM在文档理解与问答方面没有充分利用布局信息，而布局信息对LLM的文档理解是至关重要的，文档切分与知识库的构建极大影响了LLM的预测精度。具体影响为：
1. 布局片段分割的过细会导致后续检索召回的结果残缺不准。
2. 布局片段分割过粗会导致输入噪音信息太多，回答不够精准。

现有文档布局的分析方案可分为目标检测+OCR识别与多模态大语言模型。

## 目标检测+OCR识别

layout analysis:
|solution|base model|trainable|
|---|---|---|
|paddle structure|PP-PicoDet(2021,轻量级模型)| Yes|
|unstructured|yolox(2021)|Yes|
|layoutparser|Faster R-CNN(2015)|Yes|
|NO

tsr:



### paddle structure
paddle structure系统包括layout Analysis、TSR、laytout recovery功能，以下是模型的具体组成：

|Layout Analysis|solution|base model|support fine-tune|model size|
|---|---|---|---|---|
||paddle-structureV1|YOLOv2(2016)|Yes|221MB|
||paddle-structureV2|PP-PicoDet(2021)|Yes|29.7MB|


|TSR|solution|base model|support fine-tune|model size|
|---|---|---|---|---|
||paddle-structureV1|TableRec-RARE(2021)|Yes|14.6MB|
||paddle-structureV2|SLANet(2022)|Yes|24.1MB|

[SLANet](https://arxiv.org/pdf/2210.05391v2)：
直接生成token和cell coordinates并拼接成html表示的表格。


### unstructured

提供OCR-based 与 Transformer-based models, 一共有4种具体的模型，分别是：
1. detectron2_onnx (2015，采用了Detectron2 Layout-parser中的模型，即Faster R-CNN)
2. yolox (2021, 特性小而快)
3. chipper（）
4. yolox_quantized


pipeline:

detection model -> OCR, and optionally table inference models.

### LayoutParser

文档解析的模型库，提供了在不同文档结构数据集上train好的Detectron2模型。