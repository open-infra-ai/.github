# open-infra-ai

个人维护者：[holtwood](https://github.com/holtwood) · C++ / CUDA / LLM inference systems

从可验证的 CUDA/Triton kernel 到真实权重推理与 Rust serving 控制面。

## 旗舰系统

**[paged-serving](https://github.com/open-infra-ai/paged-serving) 控制面**
通过受测试的同进程 C ABI 调用
**[tiny-llm](https://github.com/open-infra-ai/tiny-llm) 数据面**：

```text
HTTP/SSE → continuous batching → Paged KV/block tables
                                      ⇅ C ABI
                              GGUF/W8A16 → CUDA decode
```

这是一个端到端项目，用两个仓库表达控制面/数据面边界，不是两个孤立 demo。

## 深度与对照

| 角色 | 仓库 | 重点 | 状态 |
|------|------|------|------|
| CUDA 深挖 | [cuflash](https://github.com/open-infra-ai/cuflash) | FlashAttention 前后向、Tensor Core、FlashDecoding | stable |
| CUDA 基础 | [cuda-foundations](https://github.com/open-infra-ai/cuda-foundations) | SGEMM 优化阶梯与可复用推理组件 | stable |
| Triton 对照 | [trifuse](https://github.com/open-infra-ai/trifuse) | 融合算子、参考实现、`torch.library` | stable |
| 旗舰数据面 | [tiny-llm](https://github.com/open-infra-ai/tiny-llm) | 真实权重、量化、decode、KV、C ABI | active |
| 旗舰控制面 | [paged-serving](https://github.com/open-infra-ai/paged-serving) | 调度、Paged KV、HTTP/SSE、serving 评测 | active |

## 从哪里开始

- [组织地图与状态注册表](https://github.com/open-infra-ai/open-infra-ai)
- [可追溯证据与当前缺口](https://github.com/open-infra-ai/open-infra-ai/blob/master/docs/evidence-index.md)
- [完整学习路径](https://github.com/open-infra-ai/open-infra-ai/blob/master/LEARNING_PATH.md)
- [跨仓语义与 ABI 契约](https://github.com/open-infra-ai/open-infra-ai/blob/master/docs/cross-repo-contracts.md)

## 工程原则

- **可追溯性能证据**：数字绑定硬件、commit、复现命令、原始结果与限制
- **差分测试**：优化实现与独立参考实现做数值对比
- **不变量验证**：检查 KV Cache 资源守恒、调度状态机与跨语言布局
- **边界先于宣传**：CPU 参考、本地 smoke 和真实 GPU Serving 结果分开表述
