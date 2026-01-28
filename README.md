# ohos-one-stop-build

[English](#english) | [中文](#中文)

---

## English

### Introduction

**ohos-one-stop-build** is a Claude Code Skill designed for HarmonyOS (OHOS) development. It provides a one-stop workflow to build, install, run HarmonyOS applications, and fetch device logs — all through a single command.

This skill enables Code Agents to automatically detect build errors and runtime issues, making HarmonyOS development more efficient and streamlined.

### Features

- **One-command workflow**: Build → Install → Run → Fetch Logs
- **Auto-detection**: Automatically locates `hvigorw` and `hdc` tools
- **Error recognition**: Code Agent can identify and analyze build/runtime errors
- **Flexible configuration**: Supports custom project paths, modules, and log settings
- **CLI-based**: Reproduces IDE "Run" behavior via command line

### Core Workflow

```bash
# 1. Build HAP
$HVIGORW assembleHap -p product=$PRODUCT -p module=$MODULE --daemon

# 2. Clear device logs
$HDC shell hilog -r

# 3. Install HAP
$HDC install -r "$HAP_PATH"

# 4. Stop existing app
$HDC shell aa force-stop $BUNDLE

# 5. Start app
$HDC shell aa start -a $ABILITY -b $BUNDLE

# 6. Fetch logs
$HDC shell hilog -v time -T $LOG_TAG -z $LOG_LINES
```

### Configuration

| Variable | Description | Example |
|----------|-------------|----------|
| PROJECT_ROOT | Project root directory | /path/to/project |
| HVIGORW | Path to hvigorw | /path/to/hvigorw |
| HDC | Path to hdc | /path/to/hdc |
| MODULE | Module name | entry |
| PRODUCT | Product name | default |
| BUNDLE | Bundle identifier | com.example.app |
| ABILITY | Entry ability | EntryAbility |
| HAP_PATH | HAP output path | entry/build/.../entry-default-unsigned.hap |
| LOG_TAG | Log filter tag | MyAppTag |
| LOG_LINES | Number of log lines | 500 |

### Use Cases

- One-command build/install/run on HarmonyOS
- Reproducing IDE "Run" behavior via CLI
- Clearing and fetching hilog after install/run
- Standardizing hvigorw + hdc workflows
- Automated CI/CD pipelines for HarmonyOS apps

### Troubleshooting

- **hvigorw not found**: Verify HVIGORW path or add to PATH
- **hdc not found**: Verify HDC path or add to PATH
- **No device**: Check `hdc list targets`
- **HAP missing**: Verify HAP_PATH after build
- **Signing warning**: Expected for unsigned debug HAP; configure signing if needed

---

## 中文

### 简介

**ohos-one-stop-build** 是一个专为鸿蒙 (HarmonyOS/OHOS) 开发设计的 Claude Code Skill。它提供一站式工作流，通过单个命令完成应用的构建、安装、运行和日志获取。

该 Skill 支持 Code Agent 自动识别编译报错和运行时问题，让鸿蒙开发更加高效便捷。

### 功能特性

- **一键式工作流**：构建 → 安装 → 运行 → 获取日志
- **自动检测**：自动定位 `hvigorw` 和 `hdc` 工具
- **错误识别**：Code Agent 可识别并分析编译/运行时错误
- **灵活配置**：支持自定义项目路径、模块和日志设置
- **命令行驱动**：通过 CLI 复现 IDE 的 "Run" 行为

### 核心工作流

```bash
# 1. 构建 HAP
$HVIGORW assembleHap -p product=$PRODUCT -p module=$MODULE --daemon

# 2. 清除设备日志
$HDC shell hilog -r

# 3. 安装 HAP
$HDC install -r "$HAP_PATH"

# 4. 停止现有应用
$HDC shell aa force-stop $BUNDLE

# 5. 启动应用
$HDC shell aa start -a $ABILITY -b $BUNDLE

# 6. 获取日志
$HDC shell hilog -v time -T $LOG_TAG -z $LOG_LINES
```

### 配置说明

| 变量 | 说明 | 示例 |
|------|------|------|
| PROJECT_ROOT | 项目根目录 | /path/to/project |
| HVIGORW | hvigorw 路径 | /path/to/hvigorw |
| HDC | hdc 路径 | /path/to/hdc |
| MODULE | 模块名称 | entry |
| PRODUCT | 产品名称 | default |
| BUNDLE | 包标识符 | com.example.app |
| ABILITY | 入口 Ability | EntryAbility |
| HAP_PATH | HAP 输出路径 | entry/build/.../entry-default-unsigned.hap |
| LOG_TAG | 日志过滤标签 | MyAppTag |
| LOG_LINES | 日志行数 | 500 |

### 使用场景

- 鸿蒙应用一键构建/安装/运行
- 通过 CLI 复现 IDE "Run" 行为
- 安装/运行后清除并获取 hilog
- 标准化 hvigorw + hdc 工作流
- 鸿蒙应用自动化 CI/CD 流水线

### 常见问题

- **找不到 hvigorw**：检查 HVIGORW 路径或添加到 PATH
- **找不到 hdc**：检查 HDC 路径或添加到 PATH
- **无设备**：检查 `hdc list targets`
- **HAP 缺失**：构建后检查 HAP_PATH
- **签名警告**：未签名的调试 HAP 会出现此警告，如需要请配置签名

---

## License

Internal use only

## Author

Created by vanicliu @ 2026-01-19
