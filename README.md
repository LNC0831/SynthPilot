# SynthPilot

**Let AI build your FPGA designs.**

[![PyPI](https://img.shields.io/pypi/v/synthpilot)](https://pypi.org/project/synthpilot/)
[![Python](https://img.shields.io/badge/python-3.10+-blue)](https://www.python.org/)
[![Platform](https://img.shields.io/badge/platform-Windows%20x64-lightgrey)](https://www.synthpilot.dev)
[![License](https://img.shields.io/badge/license-proprietary-orange)](https://www.synthpilot.dev)

[English](#english) | [中文](#中文)

---

## English

### What is SynthPilot?

SynthPilot is an MCP (Model Context Protocol) server that gives AI assistants full control over AMD Vivado. With **414 tools** covering the entire FPGA development flow, you can create projects, run synthesis, analyze timing, configure IPs, build Block Designs, and program devices — all through natural language.

```
AI Tool (Claude / Cursor) ←—MCP (stdio)—→ SynthPilot ←—TCP:9999—→ Vivado (tcl_server)
```

### Quick Start

```bash
# 1. Install
pip install synthpilot

# 2. Get a free license at https://www.synthpilot.dev, then activate
synthpilot activate YOUR-LICENSE-KEY

# 3. Set up Vivado integration (restart Vivado after this step)
synthpilot install

# 4. Configure your MCP client (see below)
# 5. Open Vivado → start chatting with AI!
```

### MCP Configuration

<details>
<summary><strong>Claude Desktop</strong></summary>

Edit `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "synthpilot": {
      "command": "synthpilot"
    }
  }
}
```
</details>

<details>
<summary><strong>Claude Code</strong></summary>

Run in terminal:

```bash
claude mcp add synthpilot synthpilot
```

Or add to `.mcp.json`:

```json
{
  "mcpServers": {
    "synthpilot": {
      "command": "synthpilot"
    }
  }
}
```
</details>

<details>
<summary><strong>Cursor</strong></summary>

Add to Cursor MCP settings:

```json
{
  "mcpServers": {
    "synthpilot": {
      "command": "synthpilot"
    }
  }
}
```
</details>

> **Tip:** You can also use `uvx` for auto-isolated environments:
> ```json
> { "command": "uvx", "args": ["synthpilot"] }
> ```

### CLI Reference

| Command | Description |
|---------|-------------|
| `synthpilot` | Start MCP server (used by AI tools) |
| `synthpilot install [path]` | Auto-detect Vivado & install Tcl server |
| `synthpilot uninstall [path]` | Remove Tcl server from Vivado |
| `synthpilot activate <KEY>` | Activate license key |
| `synthpilot deactivate` | Deactivate license on this device |
| `synthpilot --version` | Show version |

### Features

| | Free | Pro | Max |
|---|---|---|---|
| **Tools** | 39 | 380 | All 414 |
| **Project & Synthesis** | ✅ | ✅ | ✅ |
| **Timing & Reports** | ✅ | ✅ | ✅ |
| **Device Programming** | ✅ | ✅ | ✅ |
| **IP Configuration** | — | ✅ | ✅ |
| **Block Design** | — | ✅ | ✅ |
| **Simulation & Debug** | — | ✅ | ✅ |
| **Linter** | — | ✅ | ✅ |
| **Custom Tcl** | — | — | ✅ |
| **Non-Project Mode** | — | — | ✅ |
| **HW Debug Runtime** | — | — | ✅ |
| **Devices** | 1 | 2 | 3 |

### Requirements

- Python 3.10+
- Windows x64
- AMD Vivado 2018.1+

### Links

- 📖 **Full Documentation:** [www.synthpilot.dev/docs.html](https://www.synthpilot.dev/docs.html)
- 🆓 **Get Free License:** [www.synthpilot.dev](https://www.synthpilot.dev)
- 📧 **Support:** support@synthpilot.dev
- 📋 **Issues:** [GitHub Issues](https://github.com/LNC0831/SynthPilot/issues)

---

## 中文

### SynthPilot 是什么？

SynthPilot 是一个 MCP (Model Context Protocol) 服务，让 AI 助手能够完整操控 AMD Vivado。提供 **414 个工具**，覆盖 FPGA 开发全流程 — 创建项目、运行综合、时序分析、IP 配置、Block Design、下载烧录，全部通过自然语言完成。

```
AI 工具 (Claude / Cursor) ←—MCP (stdio)—→ SynthPilot ←—TCP:9999—→ Vivado (tcl_server)
```

### 快速开始

```bash
# 1. 安装
pip install synthpilot

# 2. 在 https://www.synthpilot.dev 申请免费 License，然后激活
synthpilot activate YOUR-LICENSE-KEY

# 3. 配置 Vivado 集成（完成后需重启 Vivado）
synthpilot install

# 4. 配置 MCP 客户端（见下方）
# 5. 打开 Vivado → 开始和 AI 对话！
```

### MCP 配置

<details>
<summary><strong>Claude Desktop</strong></summary>

编辑 `claude_desktop_config.json`：

```json
{
  "mcpServers": {
    "synthpilot": {
      "command": "synthpilot"
    }
  }
}
```
</details>

<details>
<summary><strong>Claude Code</strong></summary>

在终端运行：

```bash
claude mcp add synthpilot synthpilot
```

或添加到 `.mcp.json`：

```json
{
  "mcpServers": {
    "synthpilot": {
      "command": "synthpilot"
    }
  }
}
```
</details>

<details>
<summary><strong>Cursor</strong></summary>

添加到 Cursor MCP 设置：

```json
{
  "mcpServers": {
    "synthpilot": {
      "command": "synthpilot"
    }
  }
}
```
</details>

> **提示：** 也可以使用 `uvx` 自动隔离环境：
> ```json
> { "command": "uvx", "args": ["synthpilot"] }
> ```

### CLI 命令

| 命令 | 说明 |
|------|------|
| `synthpilot` | 启动 MCP 服务（AI 工具调用） |
| `synthpilot install [路径]` | 自动检测 Vivado 并安装 Tcl 服务 |
| `synthpilot uninstall [路径]` | 从 Vivado 移除 Tcl 服务 |
| `synthpilot activate <KEY>` | 激活 License |
| `synthpilot deactivate` | 解绑当前设备 |
| `synthpilot --version` | 查看版本号 |

### 功能对比

| | Free 免费版 | Pro 专业版 | Max 旗舰版 |
|---|---|---|---|
| **工具数量** | 39 | 380 | 全部 414 |
| **项目 & 综合** | ✅ | ✅ | ✅ |
| **时序 & 报告** | ✅ | ✅ | ✅ |
| **下载烧录** | ✅ | ✅ | ✅ |
| **IP 配置** | — | ✅ | ✅ |
| **Block Design** | — | ✅ | ✅ |
| **仿真 & 调试** | — | ✅ | ✅ |
| **Linter** | — | ✅ | ✅ |
| **自定义 Tcl** | — | — | ✅ |
| **Non-Project Mode** | — | — | ✅ |
| **硬件调试运行时** | — | — | ✅ |
| **设备数量** | 1 | 2 | 3 |

### 系统要求

- Python 3.10+
- Windows x64
- AMD Vivado 2018.1+

### 相关链接

- 📖 **完整文档：** [www.synthpilot.dev/docs.html](https://www.synthpilot.dev/docs.html)
- 🆓 **获取免费 License：** [www.synthpilot.dev](https://www.synthpilot.dev)
- 📧 **技术支持：** support@synthpilot.dev
- 📋 **问题反馈：** [GitHub Issues](https://github.com/LNC0831/SynthPilot/issues)
