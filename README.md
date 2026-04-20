# LLM InferenceOps Hub

**LLM大模型推理服务部署专家** | v1.0.2

---

## 简介

LLM InferenceOps Hub 是一款专业的 LLM 推理服务部署技能，帮助用户解决任何关于大模型部署的问题。无论你是零基础小白、有一定基础的用户，还是处理复杂问题的高级工程师，都可以使用本技能获得权威、实用的解决方案。

## 核心特性

| 特性 | 说明 |
|------|------|
| 🤖 多框架支持 | vLLM、TensorRT-LLM、Ollama、llama.cpp、TGI、MindIE 等 |
| 💻 多硬件支持 | NVIDIA GPU、华为昇腾 NPU、CPU |
| 🌐 多平台支持 | AWS、GCP、Azure、阿里云、腾讯云、华为云 |
| 📋 权威信息 | 所有方案来自官方文档，确保准确可靠 |
| 🔄 自动更新 | 发布到 GitHub 后自动获取最新版本 |

## 适用对象

| 用户级别 | 描述 | 使用建议 |
|----------|------|----------|
| **零基础小白** | 完全不了解 LLM 部署 | 从环境准备开始，按顺序学习 |
| **有一定基础** | 了解基本概念但遇到实际问题 | 直接查阅问题诊断模板 |
| **高级用户** | 处理复杂故障和性能优化 | 使用故障排查和性能优化章节 |

## 支持的框架

### NVIDIA GPU

| 框架 | 适用场景 | 官方文档 |
|------|----------|----------|
| [vLLM](https://docs.vllm.ai/) | 入门首选，PagedAttention 优化 | https://docs.vllm.ai/ |
| [TensorRT-LLM](https://nvidia.github.io/TensorRT-LLM/) | 最高性能，生产环境 | https://nvidia.github.io/TensorRT-LLM/ |
| [llama.cpp](https://github.com/ggerganov/llama.cpp) | 轻量推理，CPU/GPU 通用 | https://github.com/ggerganov/llama.cpp |
| [TGI](https://huggingface.github.io/text-generation-inference/) | HuggingFace 模型 | https://huggingface.github.io/text-generation-inference/ |

### 华为昇腾 NPU

| 框架 | 适用场景 | 官方文档 |
|------|----------|----------|
| [vLLM-Ascend](https://github.com/vllm-project/vllm-ascend) | 与 vLLM API 兼容 | https://github.com/vllm-project/vllm-ascend |
| [MindIE](https://www.hiascend.com/document/detail/zh/mindie/100/mindieservice/) | 生产环境，华为官方 | https://www.hiascend.com/document/detail/zh/mindie/100/mindieservice/ |
| [MindSpore Transformers](https://www.mindspore.cn/mindformers/) | 快速验证，一键拉起 | https://www.mindspore.cn/mindformers/ |

## 硬件部署对照表

| 模型规模 | NVIDIA GPU | 昇腾 NPU | 推荐框架 (NVIDIA) | 推荐框架 (昇腾) |
|----------|-------------|----------|-------------------|-----------------|
| 7B | 1×RTX 3080+ | 1×Atlas 800I A2 | vLLM | vLLM-Ascend |
| 13B | 1×A100 40G | 1×Atlas 800I A2 | vLLM | MindIE |
| 34B | 2×A100 40G | 2×Atlas 800I A2 | vLLM + TP2 | MindIE + TP2 |
| 70B | 4×A100 80G | 4×Atlas 800I A2 | vLLM + TP4 | MindIE + TP4 |
| 100B+ | 8×A100 80G | 8×Atlas 800I A2 | TensorRT-LLM | MindIE 集群 |

## 快速开始

### 1. 识别你的问题类型

```
问题类型：
□ 环境配置 - 驱动、Docker、CUDA 安装
□ 模型下载 - HuggingFace/ModelScope 模型获取
□ 服务启动 - 部署和启动推理服务
□ 性能问题 - 速度慢、显存不足
□ API 调用 - OpenAI 兼容接口使用
□ 其他问题
```

### 2. 使用问诊模板

```
问题：[简要描述你的问题]
环境：操作系统 + GPU型号 + 显存
已尝试：[你尝试过的方案]
错误信息：[如有，粘贴完整的错误日志]
```

### 3. 获取解决方案

系统会根据你的问题类型和级别，提供：
- **小白**：详细的分步指导
- **有基础**：核心解决方案 + 可选深入内容
- **高级用户**：直接可用的命令和配置

## 常用命令速查

| 操作 | 命令 |
|------|------|
| 启动 vLLM 服务 | `docker run -d --gpus all -p 8000:8000 vllm/vllm-openai:latest --model {model}` |
| 检查 GPU 状态 | `nvidia-smi` |
| 查看容器日志 | `docker logs -f {container}` |
| 测试 API | `curl http://localhost:8000/v1/models` |
| 停止服务 | `docker stop {container}` |

## 常见错误代码

| 错误码 | 含义 | 解决方案 |
|--------|------|----------|
| E001 | 驱动未安装 | 安装 NVIDIA 驱动 |
| E002 | Docker 无 GPU 权限 | 配置 NVIDIA Container Toolkit |
| E003 | 端口被占用 | 更换端口或停止占用进程 |
| E004 | 显存不足 | 启用量化或减少 batch size |
| E005 | 模型下载失败 | 检查网络或使用镜像 |
| E006 | 权限不足 | 使用 sudo 或检查文件权限 |

## 权威信息来源

所有信息优先参照以下来源：

### 官方文档

**NVIDIA GPU**
- [vLLM Docs](https://docs.vllm.ai/)
- [vLLM 中文文档](https://docs.vllm.com.cn/)
- [TensorRT-LLM](https://nvidia.github.io/TensorRT-LLM/)
- [HuggingFace TGI](https://huggingface.github.io/text-generation-inference/)
- [NVIDIA CUDA](https://docs.nvidia.com/cuda/)

**华为昇腾 NPU**
- [vLLM-Ascend](https://github.com/vllm-project/vllm-ascend)
- [vLLM-Ascend 中文](https://docs.vllm.com.cn/projects/recipes/zh_CN/latest/index.html)
- [MindIE 昇腾推理引擎](https://www.hiascend.com/document/detail/zh/mindie/100/mindieservice/servicedev/mindie_service0015.html)
- [MindSpore Transformers](https://www.mindspore.cn/mindformers/docs/zh-CN/r1.5.0/usage/deployment.html)

**模型权重**
- [Kimi-K2.5 昇腾部署指南](https://ai.gitcode.com/Ascend-SACT/Kimi-K2.5-W4A8/blob/main/README.md)
- [Kimi-K2.5 HuggingFace](https://huggingface.co/moonshotai/Kimi-K2.5/tree/main)
- [Kimi-K2.5 ModelScope](https://modelscope.cn/models/moonshotai/Kimi-K2.5/files)

### 权威博客

- [vLLM Blog](https://blog.vllm.ai/)
- [HuggingFace Blog](https://huggingface.co/blog)
- [NVIDIA ML Blog](https://developer.nvidia.com/blog/category/machine-learning/)

### 社区资源

- [Reddit r/LocalLLaMA](https://reddit.com/r/LocalLLaMA)
- [LangChain Discord](https://discord.gg/lm-sys)

## 自动更新机制

本技能支持自动版本检查，确保用户始终使用最新版本。

### 更新流程

1. **启动时检查**：每次激活本技能时，自动检查版本
2. **版本对比**：如果发现新版本，提示用户更新
3. **无感更新**：更新内容直接加载，无需用户手动下载

### 版本发布

```bash
# 1. 更新版本号
# 编辑 version.json

# 2. 提交并推送
git add .
git commit -m "Release v1.0.x: [描述更新内容]"
git push
```

## 文件结构

```
LLM InferenceOps Hub/
├── SKILL.md           # 主技能文件（完整系统提示词和模板）
├── version.json       # 版本管理文件
├── prompts/
│   ├── auto-update.md    # 自动更新机制说明
│   └── quickstart.md      # 快速入门指南
└── README.md          # 本文件
```

## 核心原则

1. **绝对可用**：提供的每一个方案都必须经过验证，确保可用
2. **绝对权威**：所有信息都来自官方文档和最佳实践
3. **绝对清晰**：用最易懂的语言解释复杂概念
4. **绝对实用**：直接给出可执行的命令和配置

## 免责声明

本技能提供的信息基于公开的官方文档和社区最佳实践。在实施任何解决方案之前，请：

1. **验证兼容性**：确保与你的环境兼容
2. **备份数据**：重要操作前备份配置和数据
3. **测试环境**：生产环境部署前先在测试环境验证
4. **监控变化**：部署后持续监控系统状态

**作者不对因使用本技能提供的信息而造成的任何损失负责。**

---

**版本**: v1.0.2 | **更新日期**: 2026-04-20
