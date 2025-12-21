# XPilot

**AI 赋能，FPGA 开发新体验**

适用于 Vivado，用自然语言完成综合、实现、约束、仿真、下载等全流程操作。

------

## ✨ 功能特性

- 🚀 **178+ 工具** - 覆盖 FPGA 开发全流程
- 💬 **自然语言交互** - 告诉 AI "综合这个项目"，它就帮你完成
- ⚡ **一键安装** - 运行安装工具，3 分钟开始使用

------

## 📦 安装步骤

### 1. 运行安装工具

双击 `xpilot-setup.exe`，选择你的 Vivado 安装目录（如 `C:\Xilinx\Vivado\2023.1`）

### 2. 获取 License

访问 [https://xcdev.me](https://xcdev.me/)，填写邮箱免费获取 License Key

### 3. 配置 License

编辑 `config.yaml`，填入你的 License Key：

```yaml
license_key: "VMCP-XXXX-XXXX-XXXX"
```

### 4. 配置 AI 工具

#### Claude Desktop

编辑 `%APPDATA%\Claude\claude_desktop_config.json`：

```json
{
  "mcpServers": {
    "xpilot": {
      "command": "C:\\your\\path\\to\\xpilot.exe"
    }
  }
}
```

#### Cursor

在设置中添加 MCP Server，指向 `xpilot.exe`

### 5. 开始使用

1. 重启 Vivado
2. 打开 Claude Desktop 或 Cursor
3. 试试说："帮我打开 Vivado 项目" 或 "查看当前项目的资源使用情况"

------

## 📋 系统要求

| 项目     | 要求                     |
| -------- | ------------------------ |
| 操作系统 | Windows 10/11 64-bit     |
| Vivado   | 2018.1 或更高版本        |
| AI 工具  | Claude Desktop 或 Cursor |

------

## 📁 文件说明

```
xpilot-v1.0.0/
├── xpilot.exe          # 主程序
├── xpilot-setup.exe    # 安装工具
├── config.yaml         # 配置文件（填入 License Key）
└── README.md           # 说明文档
```

------

## ❓ 常见问题

**Q: Vivado 启动后没有看到 "XPilot Server: Started" 提示？**

A: 请确认安装工具选择了正确的 Vivado 版本目录，然后重启 Vivado。

**Q: 提示 License 验证失败？**

A: 请检查 `config.yaml` 中的 License Key 是否正确，确保网络连接正常。

**Q: 支持 Linux / Mac 吗？**

A: 目前仅支持 Windows，后续版本会考虑支持其他平台。

------

## 🔗 链接

- 官网：[https://xcdev.me](https://xcdev.me/)
- License 申请：https://xcdev.me/#license

------

## 📄 版本

v1.0.0 - 首次发布

------

**by Xiaochuan**