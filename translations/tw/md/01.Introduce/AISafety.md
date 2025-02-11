# Phi-3 模型的 AI 安全性
Phi-3 系列模型是根据 [Microsoft Responsible AI Standard](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE5cmFl) 开发的，这是一套公司范围内的要求，基于以下六个原则：责任、透明、公平、可靠和安全、隐私和安全性以及包容性，这些构成了 [Microsoft 的 Responsible AI 原则](https://www.microsoft.com/ai/responsible-ai)。

和之前的 Phi-3 模型一样，我们采用了多方面的安全评估和安全后训练方法，并采取了额外措施以考虑本次发布的多语言能力。我们的安全训练和评估方法包括在多个语言和风险类别中的测试，详细信息请参考 [Phi-3 Safety Post-Training Paper](https://arxiv.org/abs/2407.13833)。虽然 Phi-3 模型受益于这种方法，开发者仍应应用负责任的 AI 最佳实践，包括映射、测量和缓解与其特定用例及文化和语言环境相关的风险。

## 最佳实践

和其他模型一样，Phi 系列模型也可能表现出不公平、不可靠或冒犯性的行为。

一些需要注意的 SLM 和 LLM 限制行为包括：

- **服务质量:** Phi 模型主要基于英文文本进行训练。非英文语言的表现会较差。在训练数据中代表性较低的英文变体，其表现可能会比标准美式英语差。
- **伤害的表现和刻板印象的延续:** 这些模型可能会过度或不足地代表某些群体，抹去某些群体的代表性，或强化贬低或负面的刻板印象。尽管进行了安全后训练，由于不同群体的代表性水平不同或训练数据中反映现实世界模式和社会偏见的负面刻板印象示例的普遍存在，这些限制仍可能存在。
- **不适当或冒犯性内容:** 这些模型可能会生成其他类型的不适当或冒犯性内容，这可能使其在没有针对具体用例的额外缓解措施的情况下不适合在敏感环境中部署。
- **信息可靠性:** 语言模型可能会生成无意义的内容或编造听起来合理但实际上不准确或过时的内容。
- **代码的有限范围:** Phi-3 训练数据的大部分基于 Python，并使用常见的包如 "typing, math, random, collections, datetime, itertools"。如果模型生成的 Python 脚本使用了其他包或其他语言的脚本，我们强烈建议用户手动验证所有 API 的使用。

开发者应应用负责任的 AI 最佳实践，并负责确保特定用例符合相关法律和法规（如隐私、贸易等）。

## 负责任的 AI 考虑

和其他语言模型一样，Phi 系列模型也可能表现出不公平、不可靠或冒犯性的行为。一些需要注意的限制行为包括：

**服务质量:** Phi 模型主要基于英文文本进行训练。非英文语言的表现会较差。在训练数据中代表性较低的英文变体，其表现可能会比标准美式英语差。

**伤害的表现和刻板印象的延续:** 这些模型可能会过度或不足地代表某些群体，抹去某些群体的代表性，或强化贬低或负面的刻板印象。尽管进行了安全后训练，由于不同群体的代表性水平不同或训练数据中反映现实世界模式和社会偏见的负面刻板印象示例的普遍存在，这些限制仍可能存在。

**不适当或冒犯性内容:** 这些模型可能会生成其他类型的不适当或冒犯性内容，这可能使其在没有针对具体用例的额外缓解措施的情况下不适合在敏感环境中部署。
信息可靠性: 语言模型可能会生成无意义的内容或编造听起来合理但实际上不准确或过时的内容。

**代码的有限范围:** Phi-3 训练数据的大部分基于 Python，并使用常见的包如 "typing, math, random, collections, datetime, itertools"。如果模型生成的 Python 脚本使用了其他包或其他语言的脚本，我们强烈建议用户手动验证所有 API 的使用。

开发者应应用负责任的 AI 最佳实践，并负责确保特定用例符合相关法律和法规（如隐私、贸易等）。需要考虑的重要领域包括：

**分配:** 模型可能不适用于可能对法律地位或资源或生活机会的分配（例如：住房、就业、信用等）产生重大影响的场景，除非经过进一步评估和额外的去偏技术。

**高风险场景:** 开发者应评估在高风险场景中使用模型的适用性，在这些场景中，不公平、不可靠或冒犯性的输出可能会非常昂贵或导致伤害。这包括在敏感或专家领域提供建议，这些领域对准确性和可靠性要求很高（例如：法律或健康建议）。应根据部署环境在应用层面实施额外的保障措施。

**错误信息:** 模型可能会生成不准确的信息。开发者应遵循透明度最佳实践，并告知终端用户他们正在与 AI 系统互动。在应用层面，开发者可以建立反馈机制和管道，将响应基于用例特定的、上下文信息，这种技术称为检索增强生成 (RAG)。

**有害内容的生成:** 开发者应评估输出的上下文，并使用适用于其用例的可用安全分类器或自定义解决方案。

**滥用:** 其他形式的滥用，如欺诈、垃圾邮件或恶意软件生成可能是可能的，开发者应确保他们的应用程序不违反适用的法律和法规。

### 微调和 AI 内容安全

在微调模型后，我们强烈建议利用 [Azure AI Content Safety](https://learn.microsoft.com/azure/ai-services/content-safety/overview) 措施来监控模型生成的内容，识别和阻止潜在的风险、威胁和质量问题。

![Phi3AISafety](../../../../translated_images/phi3aisafety.dc76a5bdb07ffc178e8e6d6be94d55a847ad1477d379bc28055823c777e3b06f.tw.png)

[Azure AI Content Safety](https://learn.microsoft.com/azure/ai-services/content-safety/overview) 支持文本和图像内容。它可以部署在云中、断开连接的容器中和边缘/嵌入式设备上。

## Azure AI Content Safety 概述

Azure AI Content Safety 不是一刀切的解决方案；它可以根据企业的特定政策进行定制。此外，其多语言模型使其能够同时理解多种语言。

![AIContentSafety](../../../../translated_images/AIcontentsafety.2319fe2f8154f2594e16643d4a4696100b7bb74af96b7a82b8f3327618d81122.tw.png)

- **Azure AI Content Safety**
- **Microsoft Developer**
- **5 视频**

Azure AI Content Safety 服务在应用程序和服务中检测有害的用户生成和 AI 生成内容。它包括文本和图像 API，允许您检测有害或不适当的材料。

[AI Content Safety 播放列表](https://www.youtube.com/playlist?list=PLlrxD0HtieHjaQ9bJjyp1T7FeCbmVcPkQ)

**免責聲明**：
本文件使用基於機器的AI翻譯服務進行翻譯。儘管我們努力確保準確性，但請注意，自動翻譯可能包含錯誤或不準確之處。應以原語言的原始文件為權威來源。對於關鍵信息，建議進行專業人工翻譯。我們對使用本翻譯可能產生的任何誤解或誤讀不承擔責任。