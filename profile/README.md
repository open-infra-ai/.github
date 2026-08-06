# AICL-Lab

面向 AI Infra（推理部署 / 推理加速方向）的工程作品集组织。五个主仓构成一条
「CUDA 基础 → Triton 算子 → kernel 深挖 → 推理运行时 → Serving 控制面」的能力链，
方法论与阅读顺序见 [cuda-kernel-academy/LEARNING_PATH.md](https://github.com/AICL-Lab/cuda-kernel-academy/blob/master/LEARNING_PATH.md)。

## 项目地图

| 仓库 | 定位 | 状态 |
|------|------|------|
| [tiny-llm](https://github.com/AICL-Lab/tiny-llm) | ⭐ 旗舰：CUDA C++ 推理引擎（W8A16 量化 / GGUF / KV Cache） | 开发中，见其 ROADMAP |
| [cuflash-attn](https://github.com/AICL-Lab/cuflash-attn) | 从零实现的 FlashAttention（前向+反向，多精度） | kernel 深度作品 |
| [cuda-kernel-academy](https://github.com/AICL-Lab/cuda-kernel-academy) | CUDA 系统学习路径（SGEMM 阶梯 → kernel 库 → 推理组件） | 维护模式 |
| [triton-fused-ops](https://github.com/AICL-Lab/triton-fused-ops) | Triton 融合算子 + 参考实现 + 差分测试 | 维护模式 |
| [paged-infer](https://github.com/AICL-Lab/paged-infer) | Rust 版 Serving 控制面（Paged KV + continuous batching） | 架构练习作品 |

## 工程原则

- **诚实的性能声明**：没有真实硬件测量的数字不写入文档
- **差分测试**：每个优化实现都有独立的参考实现做数值对比
- **不变量验证**：KV Cache 资源守恒、调度状态机等属性测试
