<div align="center">

# SynthPilot

**Talk to your AI. Watch it drive Vivado.**

[![PyPI](https://img.shields.io/pypi/v/synthpilot)](https://pypi.org/project/synthpilot/)
[![Python](https://img.shields.io/badge/python-3.10%2B-blue)](https://pypi.org/project/synthpilot/)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux-lightgrey)](https://pypi.org/project/synthpilot/)
[![License](https://img.shields.io/badge/license-proprietary-orange)](#license)
[![Stars](https://img.shields.io/github/stars/LNC0831/SynthPilot?style=social)](https://github.com/LNC0831/SynthPilot)

[Website](https://synthpilot.dev) · [Docs](https://synthpilot.dev/docs.html) · [PyPI](https://pypi.org/project/synthpilot/) · [Changelog](CHANGELOG.md)

</div>

> **English** | [简体中文](#简体中文)

SynthPilot is an [MCP](https://modelcontextprotocol.io) server that lets your AI assistant
(Claude, Cursor, Cline, …) **control Xilinx Vivado** for FPGA development — create projects,
write and lint RTL, run synthesis/implementation, close timing, configure IP & Block
Designs, run simulations, and program hardware — all by **describing what you want**, in
plain language.

It runs **locally**: your RTL never leaves your machine. **500+ tools** cover the whole
FPGA flow.

> *Used by engineers from **AMD**, **Tsinghua / Fudan / SJTU** and the **Chinese Academy of
> Sciences (CAS)**, FPGA vendor **Fudan Microelectronics (复旦微)**, and lidar leaders
> **Hesai (禾赛)** and **Benewake (北醒)**.*

## How it works

```
 AI editor (Claude / Cursor / Cline / …)
        │   MCP (stdio)
        ▼
   SynthPilot   ──TCP:9999──▶   Vivado (Tcl server)
```

The AI calls SynthPilot tools; SynthPilot drives Vivado over a local socket and returns
structured results (timing metrics, utilization, error summaries, waveforms …) back to the AI.

## See it in action

> You: *"Create an Artix-7 project, add this counter, run synthesis, and show me the timing."*
>
> The AI: `create_project` → `add_source_file` → `run_synthesis` → `report_timing_summary`
> → reports WNS/TNS and flags any failing paths — no Tcl, no wizard clicking.

## Quick start

```bash
pip install synthpilot          # or: uvx synthpilot@latest
synthpilot install              # auto-detect Vivado & install the Tcl server
synthpilot activate YOUR-KEY    # one-time license activation
```

Then point your MCP client at it:

```jsonc
{
  "mcpServers": {
    "synthpilot": { "command": "synthpilot" }
  }
}
```

Works with Claude Desktop / Claude Code, Cursor, Cline, and other MCP clients.

## Editions

| | Free | Pro | Max |
|---|---|---|---|
| Tools | **40** core | **~470** | **all 502** |
| Project / synth / impl / basic reports | ✅ | ✅ | ✅ |
| IP config · Block Design · Simulation · Linter · async runs | — | ✅ | ✅ |
| Devices | 1 | 2 | 3 |

Pricing, a **¥1 / 7-day trial**, and team / offline / academic editions are on
**[synthpilot.dev](https://synthpilot.dev)**.

## Requirements

- Xilinx Vivado 2018.1+ (Windows or Linux)
- An MCP-capable AI client
- Python 3.10+ (only if installing via `pip`/`uvx`)

## Links

- 🌐 Website & pricing — https://synthpilot.dev
- 📦 PyPI — https://pypi.org/project/synthpilot/
- 📖 Docs — https://synthpilot.dev/docs.html
- 🗒️ [Changelog](CHANGELOG.md)

## License

SynthPilot is a **proprietary** commercial product. This repository hosts its public
documentation and marketing materials only — the software itself is distributed via PyPI.
The RTL you process stays on your machine; SynthPilot does not upload your design sources.

---

<a name="简体中文"></a>

## 简体中文

**对你的 AI 说一句话,它替你操作 Vivado。**

SynthPilot 是一个 [MCP](https://modelcontextprotocol.io) 服务器,让你的 AI 助手(Claude、
Cursor、Cline…)用**自然语言**控制 Xilinx Vivado 做 FPGA 开发——建项目、写/查 RTL、
跑综合与实现、收敛时序、配置 IP 与 Block Design、跑仿真、烧录硬件。

**全程本地运行,你的 RTL 不出本机。500+ 工具**覆盖完整 FPGA 流程。

> *已被 **AMD**、**清华 / 复旦 / 上海交大** 与 **中科院(CAS)** 的工程师,国产 FPGA 厂商
> **复旦微**,以及激光雷达企业 **禾赛、北醒** 使用。*

### 工作原理

```
 AI 编辑器 (Claude / Cursor / Cline / …)
        │   MCP (stdio)
        ▼
   SynthPilot   ──TCP:9999──▶   Vivado (Tcl 服务器)
```

AI 调用 SynthPilot 的工具,SynthPilot 通过本地 socket 驱动 Vivado,并把结构化结果
(时序指标、资源利用、错误摘要、波形…)返回给 AI。

### 一个例子

> 你:*"建一个 Artix-7 工程,加入这个计数器,跑综合,把时序给我看看。"*
>
> AI:`create_project` → `add_source_file` → `run_synthesis` → `report_timing_summary`
> → 报告 WNS/TNS 并标出违例路径——不写 Tcl,不点向导。

### 快速开始

```bash
pip install synthpilot          # 或:uvx synthpilot@latest
synthpilot install              # 自动检测 Vivado 并安装 Tcl 服务器
synthpilot activate YOUR-KEY    # 一次性激活授权
```

然后在 MCP 客户端里配置:

```jsonc
{
  "mcpServers": {
    "synthpilot": { "command": "synthpilot" }
  }
}
```

支持 Claude Desktop / Claude Code、Cursor、Cline 等 MCP 客户端。

### 档位

| | 免费版 | Pro | Max |
|---|---|---|---|
| 工具数 | **40** 基础 | **约 470** | **全部 502** |
| 工程 / 综合 / 实现 / 基础报告 | ✅ | ✅ | ✅ |
| IP 配置 · Block Design · 仿真 · Linter · 异步执行 | — | ✅ | ✅ |
| 设备数 | 1 | 2 | 3 |

定价、**¥1 / 7 天试用**,以及团队 / 离线 / 高校版,见
**[synthpilot.dev](https://synthpilot.dev)**。

### 环境要求

- Xilinx Vivado 2018.1+(Windows 或 Linux)
- 一个支持 MCP 的 AI 客户端
- Python 3.10+(仅 `pip`/`uvx` 安装时需要)

### 链接

- 🌐 官网与定价 — https://synthpilot.dev
- 📦 PyPI — https://pypi.org/project/synthpilot/
- 📖 文档 — https://synthpilot.dev/docs.html
- 🗒️ [更新日志](CHANGELOG.md)

### 授权

SynthPilot 是**专有**商业产品。本仓库仅托管其公开文档与宣传材料,软件本体经 PyPI 分发。
你处理的 RTL 始终留在本机,SynthPilot 不上传你的设计源码。
