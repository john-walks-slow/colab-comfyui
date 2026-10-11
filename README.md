# colab-comfyui

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/john-walks-slow/colab-comfyui/blob/main/selfserve-comfyui.ipynb)

**点开就能用的 ComfyUI 生图工作台，跑在 Google Colab 免费 T4 上。** 不用配环境、不用买显卡，
点「全部运行」等十分钟左右，画布直接嵌在页面里。

一共 10 个模型可选，默认只勾两个最核心的（约 14 GB）。勾了什么才下什么。

---

## 怎么用

**1. 点上面的 Colab badge**，登录 Google 账号（免费档即可）。

**2. 菜单里选「代码执行程序 → 全部运行」**，然后等。

- 第 1 格是配置，先扫一眼要不要改（默认就能跑）
- 约 10 分钟装完环境并开始后台下模型
- 画布出现在最后一格，直接在里面出图

**3. 第一次会弹一次「允许此笔记本访问」的提示** —— 这是 Colab 自己的确认框，点允许。

## 能改什么

都在第 1 格里，不用动代码。

**选模型**（勾选框）—— 默认只勾 `Illustrious` 和 `NoobAI`：

| 模型 | 适合 | 说明 |
| --- | --- | --- |
| **Illustrious-XL-v2.0** | 动漫 | 首推，生态最全 |
| **NoobAI-XL-1.1** | 动漫 | 值得一试，画风更活 |
| Animagine-XL-4.0 | 动漫 | 手感稳 |
| RealVisXL | 写实 | 真人写实 |
| FLUX.1-dev / schnell | 通用 | 质量高但慢 |
| FLUX.2-klein / Z-Image-Turbo / Anima-Turbo | 快速 | 步数少，几秒一张 |
| Chroma1-HD | 通用 | 新架构，值得试 |

**其他开关**

| 开关 | 默认 | 作用 |
| --- | --- | --- |
| `TUNNEL_MODE` | `off` | 只用内嵌画布。想让**手机等别的设备**也能开，改成 `quick`（不用任何账号，会打印一个临时网址） |
| `ENABLE_MANAGER` | `True` | 装 ComfyUI-Manager 和模型下载面板，可在界面里直接下模型/LoRA |
| `DRIVE_OUTPUT` | `False` | 把出图和设置存到 Google Drive。**会要求一次 Google 授权**，按官方说明每次新会话可能要重新授权 |
| `EXTRA_NODES` | 空 | 需要 ControlNet 时选 `controlnet`（会多花 5~13 分钟现场编译） |

## 可选的 Colab Secrets

左侧 🔑 里可以存两个密钥，都**不用**也能跑：

| 名字 | 用途 |
| --- | --- |
| `CIVITAI_TOKEN` | 在模型下载面板里下 Civitai 上需要登录的模型（Civitai 的 API key） |
| `HF_TOKEN` | 下 HuggingFace 上需要授权的模型，同时能消除未登录的限速警告 |

存的时候记得勾上 **Notebook access**。

## 出图存哪

默认只在 Colab 的临时磁盘上，**会话结束就没了**。要留存就在配置格里打开 `DRIVE_OUTPUT`，
出图会进 `MyDrive/imagegen/output`，LoRA 进 `MyDrive/imagegen/loras`。

> 模型权重**不建议**放 Drive：ComfyUI 用 mmap 读大文件，而 Drive 是网络挂载，会明显变慢。

## 已知限制

- **Colab 免费档的会话最长约 12 小时，空闲约 40 分钟就被回收。** 回收后环境和隧道都没了，
  从第 1 步重跑即可（约 10 分钟）。
- **T4 是 16 GB 显存、没有 fp8/bf16 硬件加速**，所以 8-bit 档走 GGUF 量化。
  想跑更大的模型请用 Colab 的付费档或换别的平台。
- 出图速度取决于选的模型：Turbo/Klein 档几秒一张，FLUX.1-dev 要一两分钟。
- **本项目只是把 ComfyUI 和一堆开源模型拼起来**，模型各自的许可证由各自作者决定，
  商用前请自行确认。

## License

本仓库（笔记本和使用说明）用 MIT。ComfyUI 本体、各自定义节点、以及所有模型权重
都是独立的第三方项目，遵循它们各自的许可证。
