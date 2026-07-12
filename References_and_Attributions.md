# References & Attributions

Project Amore is built on the work of many researchers. This document credits the papers whose ideas the architecture draws on, and the software tools it relies on. It replaces the earlier third-party-license list, since the repository no longer ships code.

Two groups are kept separate, on purpose. **Core methods** are papers whose techniques are actually implemented in the architecture. **Considered directions** are papers referenced in the design notes as candidates or influences, but not part of the current build. Citations were checked against their sources in July 2026; the 2026 papers are cited as recorded in the project's own build specifications.

---

## Core methods — built into the architecture

### Sequence backbone (state-space models)

- **Albert Gu, Tri Dao.** *Mamba: Linear-Time Sequence Modeling with Selective State Spaces.* 2023. arXiv:2312.00752. — the selective state-space core of the recurrent stack.
- **Tri Dao, Albert Gu.** *Transformers are SSMs: Generalized Models and Efficient Algorithms Through Structured State Space Duality.* 2024. arXiv:2405.21060. — Mamba-2 / state-space duality.
- ***Mamba-3: Improved Sequence Modeling using State Space Principles.*** 2026. arXiv:2603.15569. — complex-valued state updates and the multi-input/multi-output (MIMO, "MiMo") formulation used per head.

### Attention & positional encoding

- **Songlin Yang, Bailin Wang, Yikang Shen, Rameswar Panda, Yoon Kim.** *Gated Linear Attention Transformers with Hardware-Efficient Training.* ICML 2024. arXiv:2312.06635. — gated linear attention (GLA), an attention-anchor mixer.
- **Shuangfei Zhai (Apple).** *Exclusive Self Attention.* 2026. arXiv:2603.09078. — exclusive self-attention (XSA), an attention-anchor mixer.
- **Kimi Team (Moonshot AI).** *Attention Residuals.* 2026. arXiv:2603.15031. — learned depth-wise aggregation of layer outputs; the paper's **Block AttnRes** is Amore's Block-AttnRes.
- **Jianlin Su, et al.** *RoFormer: Enhanced Transformer with Rotary Position Embedding.* 2021. arXiv:2104.09864. — rotary position embeddings (RoPE) in the attention anchors.

### Normalization

- **Biao Zhang, Rico Sennrich.** *Root Mean Square Layer Normalization.* NeurIPS 2019. arXiv:1910.07467. — RMSNorm, used throughout the stack.

### Optimization & scaling

- **Keller Jordan.** *Muon: An optimizer for hidden layers in neural networks.* 2024. https://kellerjordan.github.io/posts/muon/ (see also Liu et al., *Muon is Scalable for LLM Training*, arXiv:2502.16982). — the Newton–Schulz-orthogonalized momentum optimizer for 2-D weights.
- **Greg Yang, Edward J. Hu, et al.** *Tensor Programs V: Tuning Large Neural Networks via Zero-Shot Hyperparameter Transfer.* 2022. arXiv:2203.03466. — Maximal Update Parametrization (μP) for width transfer.

### Predictive coding & world models

- **Rajesh P. N. Rao, Dana H. Ballard.** *Predictive coding in the visual cortex: a functional interpretation of some extra-classical receptive-field effects.* Nature Neuroscience, 1999. — the predictive-coding principle behind P_soft (state driven by prediction error, not raw input).
- **Mahmoud Assran, Quentin Duval, Ishan Misra, Piotr Bojanowski, Pascal Vincent, Michael Rabbat, Yann LeCun, Nicolas Ballas.** *Self-Supervised Learning from Images with a Joint-Embedding Predictive Architecture (I-JEPA).* CVPR 2023. arXiv:2301.08243. — informs the JPCL latent-prediction sidecar.
- **Yann LeCun.** *A Path Towards Autonomous Machine Intelligence.* 2022. — the broader JEPA world-model vision.

### Memory

- **Guillaume Lample, Alexandre Sablayrolles, Marc'Aurelio Ranzato, Ludovic Denoyer, Hervé Jégou.** *Large Memory Layers with Product Keys.* NeurIPS 2019. arXiv:1907.05242. — product-key memory, the basis of FwPKM.
- **Jimmy Ba, Geoffrey Hinton, Volodymyr Mnih, Joel Z. Leibo, Catalin Ionescu.** *Using Fast Weights to Attend to the Recent Past.* NeurIPS 2016. arXiv:1610.06258. — fast-weight memory, the "Fw" in FwPKM.
- **Zhao & Jones (Sakana AI).** *Fast-weight Product Key Memory (FwPKM).* 2026. arXiv:2601.00671. — the formulation Amore's FwPKM follows directly.
- **DeepSeek.** *Conditional Memory via Scalable Lookup: A New Axis of Sparsity for Large Language Models (Engram).* 2026. arXiv:2601.07372. — conditional-memory / scalable-lookup sparsity.

### Safety & governance

- **Wei Zhao, et al.** *ClawGuard: A Runtime Security Framework for Tool-Augmented LLM Agents Against Indirect Prompt Injection.* 2026. arXiv:2604.11790. — the ClawGuard safety component is named after and follows this paper's pipeline.

---

## Considered directions & influences

Referenced in the design notes as candidates or influences; **not part of the current build.**

- **Ali Behrouz, Peilin Zhong, Vahab Mirrokni.** *Titans: Learning to Memorize at Test Time.* 2025. arXiv:2501.00663. — test-time neural long-term memory; a candidate for concretizing FwPKM.
- **Bernal Jiménez Gutiérrez, Yiheng Shu, Yu Gu, Michihiro Yasunaga, Yu Su.** *HippoRAG: Neurobiologically Inspired Long-Term Memory for Large Language Models.* NeurIPS 2024. arXiv:2405.14831. — knowledge-graph + Personalized PageRank retrieval, considered for Pegasus.
- **Soyeong Jeong, Jinheon Baek, Sukmin Cho, Sung Ju Hwang, Jong C. Park.** *Adaptive-RAG: Learning to Adapt Retrieval-Augmented Large Language Models through Question Complexity.* NAACL 2024. arXiv:2403.14403. — complexity-aware retrieval features considered for the retrieval gate.
- ***xMemory: Retrieval by Decoupling and Hierarchies.*** 2026. arXiv:2602.02007. — hierarchical agent memory, noted for possible future use.
- **Eric Wallace, Kai Xiao, Reimar Leike, Lilian Weng, Johannes Heidecke, Alex Beutel.** *The Instruction Hierarchy: Training LLMs to Prioritize Privileged Instructions.* 2024. arXiv:2404.13208. — privileged-instruction defense-in-depth, considered as a second layer behind ClawGuard.

---

## Software & tools

Used in building and training the system; not bundled in this repository.

- **PyTorch** (Meta) — BSD 3-Clause. Core tensor framework.
- **HuggingFace Transformers** — Apache 2.0. Model loading and tokenizer utilities.
- **mamba-ssm** (Tri Dao, Albert Gu) — Apache 2.0. Mamba-3 SSM kernels.

---

## Project Amore

All original code and documentation is the work of the author (ReconKatze / Azathoth), published for research and educational purposes. No separate open-source license is attached at this time.

Contact: projectamore26@gmail.com
