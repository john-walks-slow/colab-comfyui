# colab-comfyui

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/john-walks-slow/colab-comfyui/blob/main/selfserve-comfyui.ipynb)

**点开就能用的 ComfyUI 生图工作台，跑在 Google Colab 免费 T4 上。** 点「全部运行」，画布会嵌在第 3/3 格。

## 快速开始

1. 点上面的 **Open in Colab**。
2. 菜单选择「代码执行程序 → 全部运行」。
3. 第 1 格选择模型和持久化选项；第 3/3 格打开 ComfyUI 画布。

默认只选择 Illustrious 和 NoobAI。模型、LoRA、节点和 Manager 都按配置格的选择安装。

## 主要选项

| 选项 | 默认 | 说明 |
| --- | --- | --- |
| `TUNNEL_MODE` | `off` | 使用 Colab 内嵌画布；改成 `quick` 或 `named` 才会额外开放公网地址 |
| `ENABLE_MANAGER` | `True` | 启用 Manager 和模型下载面板。公网入口开启时，拿到网址的人也能使用 Manager |
| `PERSIST_TO_DRIVE` | `False` | 把 output、user/workflows 和 models/loras 统一保存到 `MyDrive/imagegen/` |
| `EXTRA_NODES` | 空 | 按需安装 ControlNet 辅助节点；需要额外编译时间 |

开启 `PERSIST_TO_DRIVE` 后，第一次运行需要完成一次 Google Drive 授权。笔记本只把三个小而常变的目录放到 Drive：

```text
MyDrive/imagegen/
├── output/
├── user/
└── models/loras/
```

大模型权重仍放在 Colab 本地盘，避免网络挂载拖慢模型加载。Colab 运行时回收后的恢复步骤：重新打开本 Notebook，确认 `PERSIST_TO_DRIVE` 仍为 `True`，完成 Drive 授权，重跑第 1 格并等待安装/下载完成，再运行第 2 格和第 3/3 格。ComfyUI 本体、自定义节点和 checkpoint 仍需要在新运行时重新安装或下载；Drive 中的 output、user/workflows 和 LoRA 会继续保留。

## Civitai / Hugging Face

在 Colab 左侧 Secrets 中可选配置：

- `CIVITAI_TOKEN`：模型下载面板访问 Civitai
- `HF_TOKEN`：提高 Hugging Face 下载配额和速度

两个 Secret 都要勾选 **Notebook access**。

## 限制

Colab 免费运行时会回收，回收后本地模型和进程会消失；从第 1 格重新运行即可。模型权重、自定义节点和 ComfyUI 本体各自遵循其上游许可证。

## License

本仓库中的笔记本与说明使用 MIT。ComfyUI、自定义节点和模型权重由各自项目单独授权。
