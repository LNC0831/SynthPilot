<div align="center">

# SynthPilot

**让 AI 真正参与 FPGA 开发。**<br>
**Bring AI into the FPGA development loop.**

[![PyPI](https://img.shields.io/pypi/v/synthpilot)](https://pypi.org/project/synthpilot/)
[![Python](https://img.shields.io/badge/python-3.10%2B-blue)](https://pypi.org/project/synthpilot/)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux-lightgrey)](https://pypi.org/project/synthpilot/)
[![License](https://img.shields.io/badge/license-proprietary-orange)](#license)
[![Stars](https://img.shields.io/github/stars/LNC0831/SynthPilot?style=social)](https://github.com/LNC0831/SynthPilot)

[Website](https://synthpilot.dev) · [Docs](https://synthpilot.dev/docs.html) · [Tool catalogs](#public-tool-catalogs) · [PyPI](https://pypi.org/project/synthpilot/) · [Changelog](CHANGELOG.md)

</div>

> **English** | [简体中文](#简体中文)

SynthPilot is a proprietary [Model Context Protocol](https://modelcontextprotocol.io)
server for FPGA development. It gives AI assistants such as Claude, Codex, Cursor, and
other MCP clients structured access to three EDA platforms:

- **AMD Vivado™**
- **TangDynasty® (TD)**
- **Intel® Quartus® Prime**

Choose one platform when the MCP server starts. Your verified Free, Pro, or Max license
then determines which tools are registered for that session. SynthPilot runs alongside
your EDA environment and does not upload your RTL or project sources.

## Platform status

| Platform | Public catalog | Current supported scope |
|---|---:|---|
| AMD Vivado™ | [510 tools](tools/vivado.md) | Mature local workflow; Remote Vivado over SSH is available in **Beta** |
| TangDynasty® (TD) | [102 tools](tools/anlogic.md) | Windows runtime; representative TD 6.2.1 project and bitstream flow verified |
| Intel® Quartus® Prime | [24 tools](tools/quartus.md) | Windows Lite 25.1 clean-session flow verified; Standard, Pro, and Linux vendor-live matrices remain in validation |

Windows and Linux wheels are published on PyPI. Platform-specific EDA execution still
depends on the vendor software and acceptance scope stated above.

## Public tool catalogs

The public catalogs show each tool's purpose, category, plan, operation type, and a
coarse parameter overview. They are generated from the product registry and intentionally
do not publish the proprietary execution implementation. The live MCP schema remains the
authority for exact arguments.

- [AMD Vivado tool catalog](tools/vivado.md)
- [TangDynasty tool catalog](tools/anlogic.md)
- [Intel Quartus tool catalog](tools/quartus.md)

Only the selected platform and the tools allowed by the active license are registered in
an MCP session; the three catalogs are not loaded together.

## Quick start

Install or upgrade SynthPilot:

```bash
uv tool install synthpilot --upgrade --refresh
```

Choose the EDA platform you want to use:

```bash
synthpilot setup --platform vivado
# or: synthpilot setup --platform anlogic
# or: synthpilot setup --platform quartus
```

`setup` handles supported discovery, license activation, MCP registration, and health
checks. Run the platform doctor when you need a bounded diagnosis:

```bash
synthpilot doctor --platform vivado
```

<details>
<summary>Manual MCP configuration</summary>

```jsonc
{
  "mcpServers": {
    "synthpilot": {
      "command": "synthpilot",
      "args": ["--platform", "vivado"]
    }
  }
}
```

Replace `vivado` with `anlogic` or `quartus`. Plan access comes from the activated
license, not from an MCP argument.
</details>

## Remote Vivado over SSH · Beta

SynthPilot can run the complete MCP process on a remote Linux development host and connect
to Vivado on that same machine. MCP uses OpenSSH stdio; the Vivado Tcl listener remains
loopback-only and is never exposed directly to the network.

```bash
synthpilot remote add lab vivado-lab
synthpilot remote doctor lab
synthpilot install-mcp --remote lab
```

The remote host must already have an activated SynthPilot installation and an interactive
Vivado session with the Tcl listener running. File paths refer to the remote filesystem.
SynthPilot does not start Vivado or synchronize source/project trees. The full remote
Linux + Vivado end-to-end live matrix is still under acceptance, so this capability is
currently labeled **Beta**.

→ [Remote Vivado setup guide](https://synthpilot.dev/docs.html#remote-vivado)

## How it fits together

```text
AI client (Claude / Codex / Cursor / other MCP client)
                         │
                    MCP stdio
                         ▼
                    SynthPilot
             ┌───────────┼───────────┐
             ▼           ▼           ▼
        AMD Vivado   TangDynasty   Intel Quartus
        local/SSH    managed TD    managed quartus_sh
```

The AI calls structured tools and receives bounded results such as status, timing,
utilization, reports, diagnostics, and build progress. Exact capabilities depend on the
selected platform and license.

## Editions

| | Free | Pro | Max |
|---|---|---|---|
| Core diagnostics and entry workflows | ✓ | ✓ | ✓ |
| Standard engineering workflows for the selected platform | Limited | ✓ | ✓ |
| Max-exclusive Vivado and TangDynasty capabilities | — | — | ✓ |
| Licensed devices | 1 | 2 | 3 |

Tool counts differ by platform. See the three public catalogs for exact Free, Pro, and Max
membership. Pricing, the trial offer, and team/offline/academic options are maintained on
[synthpilot.dev](https://synthpilot.dev).

## Skills and methodology

[oh-my-fpga](https://github.com/LNC0831/oh-my-fpga) is the free, open methodology layer
for named workflows such as timing closure, CDC review, and Zynq bring-up.

- **Claude Code:** `/plugin marketplace add LNC0831/oh-my-fpga`, then
  `/plugin install oh-my-fpga`
- **Codex, Cursor, Claude Desktop:** the same workflows are also available as built-in MCP
  prompts in SynthPilot 1.3.0 and later.

## Requirements

- Windows x64 or Linux x86_64 for the SynthPilot package
- A supported vendor EDA installation for the selected platform
- An MCP-capable AI client
- [uv](https://docs.astral.sh/uv/) for the recommended installation path

See the [website platform pages](https://synthpilot.dev/#platforms) for the current
vendor/version acceptance boundaries.

## Links

- Website and pricing: https://synthpilot.dev
- Documentation: https://synthpilot.dev/docs.html
- Public tool browser: https://synthpilot.dev/tools.html
- PyPI: https://pypi.org/project/synthpilot/
- oh-my-fpga: https://github.com/LNC0831/oh-my-fpga
- [Changelog](CHANGELOG.md)

## License

SynthPilot is a **proprietary commercial product**. This repository contains public
documentation and product catalogs only; the software is distributed through PyPI.
SynthPilot does not upload the RTL or project sources it processes.

AMD, the AMD logo, and Vivado are trademarks of Advanced Micro Devices, Inc.
TangDynasty is a registered trademark of Shanghai Anlogic Infotech Co., Ltd.
Intel, the Intel logo, and Quartus are trademarks of Intel Corporation or its subsidiaries.
SynthPilot is not affiliated with or endorsed by these companies.

The companion [oh-my-fpga](https://github.com/LNC0831/oh-my-fpga) project is separate and
MIT-licensed.

---

<a name="简体中文"></a>

## 简体中文

SynthPilot 是面向 FPGA 开发的专有商业 MCP 产品，让 Claude、Codex、Cursor 等 AI
客户端通过结构化工具参与真实工程流程。目前覆盖：

- **AMD Vivado™**
- **TangDynasty®（TD）**
- **Intel® Quartus® Prime**

每个 MCP 进程只选择一个 FPGA 平台；当前激活的 Free、Pro 或 Max 许可证决定本次会话
注册哪些工具。SynthPilot 在 EDA 环境旁运行，不上传 RTL 与工程源码。

### 平台状态

| 平台 | 公开目录 | 当前支持范围 |
|---|---:|---|
| AMD Vivado™ | [510 个工具](tools/vivado.md) | 成熟的本地工作流；SSH 远程 Vivado 为 **Beta** |
| TangDynasty®（TD） | [102 个工具](tools/anlogic.md) | Windows 运行时；TD 6.2.1 代表性工程与 bitstream 流程已验证 |
| Intel® Quartus® Prime | [24 个工具](tools/quartus.md) | Windows Lite 25.1 干净会话流程已验证；Standard、Pro 与 Linux 厂商真机矩阵仍在验收 |

Windows 与 Linux 安装包均已发布到 PyPI。具体 EDA 执行能力仍取决于厂商软件与上述验收范围。

### 公开工具目录

公开目录展示工具用途、分类、套餐、操作类型和参数概览，由产品注册表生成，但不公开专有
执行实现。精确参数以运行中的 MCP schema 为准。

- [AMD Vivado 工具目录](tools/vivado.md)
- [TangDynasty 工具目录](tools/anlogic.md)
- [Intel Quartus 工具目录](tools/quartus.md)

三个目录不会同时进入 MCP 上下文；运行时只注册所选平台及许可证允许的工具。

### 快速开始

```bash
uv tool install synthpilot --upgrade --refresh

synthpilot setup --platform vivado
# 或：synthpilot setup --platform anlogic
# 或：synthpilot setup --platform quartus
```

`setup` 完成支持范围内的平台发现、License 激活、MCP 注册与健康检查。诊断环境时运行：

```bash
synthpilot doctor --platform vivado
```

### SSH 远程 Vivado · Beta

SynthPilot 可以运行在远程 Linux 开发机上，并连接同一台机器中已经启动的 Vivado。
MCP 通过 OpenSSH stdio 传输，Vivado Tcl 端口保持只监听远程回环地址。

```bash
synthpilot remote add lab vivado-lab
synthpilot remote doctor lab
synthpilot install-mcp --remote lab
```

远程主机必须已经安装并激活 SynthPilot，Vivado 也必须在交互会话中启动并运行 Tcl
listener。工具路径都指向远程 Linux 文件系统；SynthPilot 不负责启动 Vivado，也不自动同步
源码或工程目录。完整的远程 Linux + Vivado 端到端真机矩阵仍在验收，因此当前标记为
**Beta**。

→ [远程 Vivado 配置文档](https://synthpilot.dev/docs.html#remote-vivado)

### 套餐

| | Free | Pro | Max |
|---|---|---|---|
| 基础诊断与入口流程 | ✓ | ✓ | ✓ |
| 所选平台的标准工程能力 | 有限 | ✓ | ✓ |
| Vivado 与 TangDynasty 的 Max 专属能力 | — | — | ✓ |
| 授权设备数 | 1 | 2 | 3 |

不同平台的工具数不同，准确的 Free、Pro、Max 归属请查看三份公开目录。定价、试用、团队、
离线与高校方案以 [synthpilot.dev](https://synthpilot.dev) 为准。

### 方法论

[oh-my-fpga](https://github.com/LNC0831/oh-my-fpga) 是独立、免费开源的方法论层，提供时序
收敛、CDC 审查、Zynq bring-up 等命名工作流。

### 环境要求

- SynthPilot 安装包支持 Windows x64 与 Linux x86_64
- 所选平台对应的厂商 EDA 环境
- 支持 MCP 的 AI 客户端
- 推荐使用 [uv](https://docs.astral.sh/uv/) 安装

### 相关链接

- 官网与定价：https://synthpilot.dev
- 使用文档：https://synthpilot.dev/docs.html
- 在线工具目录：https://synthpilot.dev/tools.html
- PyPI：https://pypi.org/project/synthpilot/
- oh-my-fpga：https://github.com/LNC0831/oh-my-fpga
- [更新日志](CHANGELOG.md)

### 授权与商标

SynthPilot 是**专有商业产品**。本仓库只包含公开文档与产品目录，软件经 PyPI 分发。
SynthPilot 不上传其处理的 RTL 或工程源码。

AMD、AMD 标识与 Vivado 是 Advanced Micro Devices, Inc. 的商标；TangDynasty 是上海安路
信息科技股份有限公司的注册商标；Intel、Intel 标识与 Quartus 是 Intel Corporation 或其
子公司的商标。SynthPilot 与上述公司不存在隶属或背书关系。

[oh-my-fpga](https://github.com/LNC0831/oh-my-fpga) 是独立的 MIT 开源项目。
