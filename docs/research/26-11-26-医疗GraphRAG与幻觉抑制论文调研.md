# 26-11-26 医疗 GraphRAG 与幻觉抑制论文调研

## ① 威胁

1. **概念混淆风险**：容易把“大模型增强”窄化为“GraphRAG”，忽略学术界公认的**双向赋能框架**（`LLM → KG` 辅助建图/融合 vs. `KG → LLM` 检索增强/防幻觉），导致 30% 论文调研报告结构单薄。
2. **KG 不完备与隐式幻觉**：最新综述反复指出，医疗知识更新快、小规模图谱覆盖有限；当检索缺失时大模型会静默回退到参数记忆，产生难以察觉的事实漂移。
3. **子图噪声与上下文过载**：直接把 2~3 跳全量子图塞进 Prompt 会引入大量无关三元组，反而稀释注意力、降低问答准确率，必须做关系剪枝与 `LIMIT` 截断。
4. **评测指标失真**：传统文本指标（BLEU / ROUGE）无法衡量医学事实正确性，近期论文普遍强调事实一致性检验、幻觉率统计或结合 KG 约束的 LLM-as-a-Judge 评测。
5. **两人调研撞车风险**：课程明确要求 30% 论文调研报告**单独撰写提交**，若两人选题与文献池高度重叠容易被判雷同。

## ② 工具箱

### 2024–2026 核心英文综述与前沿论文（可直接用于 30% 调研报告）
1. **Agrawal et al. (NAACL 2024)** — *Can Knowledge Graphs Reduce Hallucinations in LLMs?: A Survey*（ACL Anthology）
   - 奠基性综述，将 KG 抑制幻觉方法划分为三大阶段：**预训练阶段注入**、**推理阶段增强（GraphRAG）**、**生成后事实核验**，非常适合搭建综述总分类框架。
2. **Reducing LLM Hallucinations with Knowledge Graphs: A Survey (2026)**
   - 系统梳理 KG 干预幻觉的检测机制、缓解范式与面向医疗/法律等高风险领域的评测基准。
3. **A Comprehensive Survey of Knowledge Graph-Augmented Generation (Graph-RAG) for Trustworthy Large Language Models (2026)**
   - 专门聚焦 GraphRAG 架构：图拓扑检索、实体关系抽取、子图路由剪枝，以及如何用可验证路径约束生成自由度。
4. **Rethinking Medical LLM Hallucinations: A System-Level Survey (2026)**
   - 指出医疗大模型幻觉是概率生成的结构性问题，仅靠提示词微调难以根治，必须通过结构化外部检索进行系统级风险治理。
5. **Factual Hallucination in Medical Large Language Models: Typology, Evaluation, and Systematic Governance (2026)**
   - 提出基于医疗知识图谱的细粒度幻觉分类框架与三层临床风险分层治理视角。
6. **前沿技术方向参考**：
   - **Ontology-Grounded GraphRAG**：将临床本体（如 RDF/OWL、ICD/SNOMED）作为硬约束注入推理大模型（如 DeepSeek-R1 / GPT-4）显著降低语义编造；
   - **Multi-Agent Graph Verification**（如 *CuraView*, 2026）：不仅用 GraphRAG 做检索，还引入校验环节对照子图检查临床回答中的安全冲突。

### 两人独立 30% 论文调研检索词与切入点拆分
- **同学 A（侧重 `LLM → KG` 构建与融合）**
  - 参考题目：《面向医疗健康领域的知识图谱自动构建与融合技术研究综述》
  - 中文检索词：`医疗知识图谱构建`、`大模型 实体关系抽取`、`医学知识融合 实体对齐`
  - 英文检索词：`LLM for Medical Knowledge Graph Construction`, `Biomedical Entity Resolution`, `Zero-shot Clinical Relation Extraction`
- **同学 B（侧重 `KG → LLM` 问答与防幻觉）**
  - 参考题目：《知识图谱增强大模型（GraphRAG）在医疗问答中的研究进展》
  - 中文检索词：`医疗知识图谱问答`、`知识图谱 大模型 幻觉抑制`、`GraphRAG 医疗问答`
  - 英文检索词：`Medical GraphRAG`, `Knowledge Graph Question Answering Healthcare`, `KG-augmented LLM Hallucination Mitigation`

### 综述报告推荐 4 段结构（3000~5000 字）
1. 引言（医疗问答高风险背景与纯 LLM 幻觉痛点）；
2. 核心方法分类进展（按技术路线分 2~3 节 + **1 张代表性论文横向对比表**）；
3. 现存挑战与开放问题（图谱不完备、子图噪声、评测体系）；
4. 对本课程常见病问答实践项目的启发（与 60% 实践形成闭环呼应）。
