# XPilot

**与 AI 协作，高效完成 FPGA 开发**

XPilot 是一个 MCP (Model Context Protocol) 服务，让 Claude Desktop、Cursor 等 AI 工具能够直接操作 Vivado，用自然语言完成综合、实现、约束、仿真、下载等全流程操作。

---

## ⚠️ 重要说明

1. **XPilot 是一个 MCP 服务**，它为 AI 工具提供与 Vivado 交互的能力
2. **需要配合支持 MCP 协议的 AI 工具使用**，如 Claude Desktop、Cursor 等
3. **AI 工具的订阅费用需用户自行承担**，与 XPilot 授权费用无关
4. **XPilot 不包含任何大语言模型**，仅提供 Vivado 操作接口服务

---

## ✨ 功能特性

- 🚀 **178+ 工具** - 覆盖 FPGA 开发全流程
- 💬 **自然语言交互** - 告诉 AI "综合这个项目"，它就帮你完成
- ⚡ **一键安装** - 运行安装工具，几分钟开始使用
- 🔒 **本地运行** - 代码和项目不会上传到云端

---

## 📦 安装步骤

### 第一步：运行安装工具

1. 双击 `xpilot-setup.exe`
2. 点击「浏览」选择 Vivado 安装目录（如 `C:\Xilinx\Vivado\2023.1`）
3. 点击「安装」，看到成功提示后关闭

> 安装工具会配置 Vivado 启动脚本，使 XPilot 随 Vivado 自动启动。

### 第二步：获取 License

1. 访问官网：https://www.xcdev.me
2. 输入邮箱，点击「获取 License Key」
3. 在邮箱中查收 License Key

### 第三步：配置 License

编辑 `config.yaml`，填入你的 License Key：

```yaml
license_key: "VMCP-XXXX-XXXX-XXXX"
```

### 第四步：配置 AI 工具

#### Claude Desktop

1. 打开文件资源管理器，地址栏输入 `%APPDATA%\Claude`
2. 编辑 `claude_desktop_config.json`：

```json
{
  "mcpServers": {
    "xpilot": {
      "command": "C:\\你的路径\\xpilot-v2.0.0\\xpilot.exe"
    }
  }
}
```

> 路径中的反斜杠需要写两个：`\\`

3. 保存后重启 Claude Desktop

#### Cursor

1. 打开设置（Ctrl + ,）
2. 搜索 "MCP"，添加 Server：
   - Name: `xpilot`
   - Command: `C:\你的路径\xpilot-v2.0.0\xpilot.exe`
3. 保存并重启 Cursor

### 第五步：开始使用

1. 启动 Vivado
2. 打开 Claude Desktop 或 Cursor
3. 试试说：
   - "帮我创建一个新项目"
   - "运行综合"
   - "查看资源使用报告"

---

## 📋 系统要求

| 项目 | 要求 |
|------|------|
| 操作系统 | Windows 10/11 64-bit |
| Vivado | 2018.1 或更高版本 |
| AI 工具 | Claude Desktop 或 Cursor（需单独订阅） |
| 网络 | 首次验证需联网 |

---

## 📁 文件说明

```
xpilot-v2.0.0/
├── xpilot.exe          # 主程序（MCP Server）
├── xpilot-setup.exe    # 安装工具
├── config.yaml         # 配置文件
└── README.md           # 本文档
```

---

## 🆓 版本区别

| 功能 | FREE 免费版 | PRO 专业版 |
|------|-------------|------------|
| 基础工具（项目管理、综合、实现、约束、下载） | ✅ ~30 个 | ✅ |
| IP 配置（Clocking Wizard, FIFO, BRAM） | ❌ | ✅ |
| Block Design（Zynq PS, AXI 外设） | ❌ | ✅ |
| Linter 代码检查 | ❌ | ✅ |
| 仿真工具 | ❌ | ✅ |
| 工具总数 | ~30 | 178+ |
| 价格 | 永久免费 | ¥25/月 或 ¥255/年 |

升级 Pro：https://www.xcdev.me/#pricing

---

## ❓ 常见问题

**Q: 安装工具提示找不到 Vivado？**

A: 请选择 Vivado 的版本目录，如 `C:\Xilinx\Vivado\2023.1`，不是 `C:\Xilinx`。

**Q: License 验证失败？**

A: 检查 `config.yaml` 中的 Key 是否正确，确保网络正常。

**Q: Claude Desktop 没识别到 XPilot？**

A: 检查 JSON 格式是否正确，路径是否用了双反斜杠 `\\`，然后重启 Claude Desktop。

**Q: 使用 Claude Desktop 需要付费吗？**

A: Claude Desktop 可免费使用但有用量限制，需更多用量可订阅 Claude Pro（与 XPilot 无关）。

**Q: 代码会上传到云端吗？**

A: 不会。XPilot 完全在本地运行。

**Q: 支持 Linux / Mac 吗？**

A: 目前仅支持 Windows，Linux 版本规划中。

---

## 🔧 故障排除

**Vivado 启动时没有 XPilot 日志？**

检查 Vivado 目录下 `scripts/Vivado_init.tcl` 是否有 XPilot 启动命令，没有则重新运行安装工具。

**AI 工具连接不上？**

1. 确保 Vivado 已启动
2. 检查任务管理器中是否有 `xpilot.exe` 进程
3. 重启 AI 工具

其他问题请提交 Issue：https://github.com/LNC0831/xpilot-vivado/issues

---

## 🔗 链接

- 官网：https://www.xcdev.me
- 文档：https://github.com/LNC0831/xpilot-vivado
- 问题反馈：https://github.com/LNC0831/xpilot-vivado/issues

---

## 📄 版本

- **v2.0.0** (2026-02) - 正式版
- **v1.0.0** (2025-12) - 内测版

---

**XPilot by Xiaochuan** · https://www.xcdev.me
