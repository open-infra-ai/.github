# open-infra-ai

个人维护者：[holtwood](https://github.com/holtwood) · C++ / CUDA / LLM inference systems

AI Infra 工程学习作品集组织：从 CUDA 内核到推理 serving 的完整能力链，
每个作品都有独立参考实现与差分验证。整体学习路径与方法论见
[LEARNING_PATH.md](https://github.com/open-infra-ai/open-infra-ai/blob/master/LEARNING_PATH.md)。

## 项目地图

| 层 | 仓库 | 定位 | 状态 |
|----|------|------|------|
| L1 | [cuda-foundations](https://github.com/open-infra-ai/cuda-foundations) | 从 SGEMM 到推理组件的系统性 CUDA 算子工程学习路径 | active |
| L1 | [triton-fused-ops](https://github.com/open-infra-ai/triton-fused-ops) | 精简 Triton 算子（RMSNorm+RoPE / GatedMLP / FA 前向 / SGEMM）+ torch.library 注册 | stable |
| L1 | [cuflash](https://github.com/open-infra-ai/cuflash) | 从零实现的 FlashAttention 前后向（FP16/BF16 WMMA + FlashDecoding） | stable |
| L2 | [tiny-llm](https://github.com/open-infra-ai/tiny-llm) | ⭐ CUDA C++ 推理引擎（W8A16 量化 / GGUF / 分页 KV），导出 C ABI | active |
| L3 | [paged-serving](https://github.com/open-infra-ai/paged-serving) | Rust Serving 控制面（Paged KV + continuous batching），经 C ABI 接 tiny-llm | active |
| L0 | [open-infra-ai](https://github.com/open-infra-ai/open-infra-ai) | meta 仓：landing、学习路径、跨仓契约、计划档案 | active |

阅读顺序：`cuda-foundations → triton-fused-ops → cuflash → tiny-llm → paged-serving`。

状态语义：`active` = 学习/演进中；`stable` = 作品完成，只修正确性 bug 与文档。
权威状态注册表在 [meta 仓 README](https://github.com/open-infra-ai/open-infra-ai)。

## 工程原则

- **诚实的性能声明**：没有真实硬件测量的数字不写入文档
- **差分测试**：每个优化实现都有独立的参考实现做数值对比
- **不变量验证**：KV Cache 资源守恒、调度状态机等属性测试
