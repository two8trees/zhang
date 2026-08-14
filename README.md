# zhang
### 自动化事实核查与多模态推理前沿文献

* AVERIMATEC: A Dataset for Automatic Verification of Image-Text Claims with Evidence from the Web (NeurIPS 2025)[cite: 2] [[Paper](#)] ![NeurIPS 2025](https://img.shields.io/badge/NeurIPS-2025-blue)
  * **文章内容**：现有的图文核查数据集多为合成数据且缺乏证据注释。[cite: 2] 这篇文章提出了 AVERIMATEC，一个包含1297个真实世界图文声明的数据集。[cite: 2] 它的亮点在于把复杂的核查结果背后的多模态推理过程拆解成了包含网络证据的问答（QA）对，并通过生成用于事实核查的证据搜寻问题，使用专家工具集（如反向图像搜索、网络搜索和视觉问答）来分别解决问题。[cite: 2]
  * **个人想法**：将复杂核查任务拆解并交给不同“专家工具”的设计非常有工程落地价值。[cite: 2] 这种模块化的思想非常契合微服务架构，后续我们在构建多模态核查系统时，可以考虑利用 Spring Boot 等框架将这些检索和视觉问答工具封装成独立的后端 API，让大模型充当调度中心按需调用，从而大幅提升系统的扩展性与执行效率。

* Document-level Claim Extraction and Decontextualisation for Fact-Checking (ACL 2024)[cite: 3] [[Paper](#)] ![ACL 2024](https://img.shields.io/badge/ACL-2024-red)
  * **文章内容**：从长文档中提取需要核查的声明是一项耗时的任务，而现有方法多局限于句子级别的提取。[cite: 3] 本文提出了一种“去语境化（decontextualisation）”的方法，通过识别文档核心句、提取模糊信息单元获取必要上下文，并利用 Seq2Seq 模型重写句子，让每一条提取出的声明在脱离上下文时也能被无歧义地理解。[cite: 3]
  * **个人想法**：“去语境化”作为核查的前置步骤切中了实际痛点，未消除指代歧义的文本直接输入模型极易引发事实幻觉。[cite: 3] 在研发 AI 模型训练数据溯源与隐私验证系统时，可以借鉴这种去语境化和核心句抽取的思路，确保上链的声明数据既具备独立语义，又能与原始文档保持严格的逻辑映射。结合 ZoKrates 的零知识证明，甚至可以探索如何在不泄露全文隐私的前提下，在链上验证抽取出的去语境化声明的真实来源。
