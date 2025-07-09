# Wezterm-Auto

一个用于在 WezTerm 中快速切换和管理多个项目的 macOS 自动化工具。

## 项目动机

作为开发者，经常需要在不同项目之间切换，传统的做法是手动打开终端、导航到项目目录、启动编辑器等。这个过程繁琐且重复。Wezterm-Auto 旨在简化这一工作流程，通过一条命令即可：

- 智能检测项目是否已经在 WezTerm 中打开
- 如果已打开，直接切换到对应的标签页
- 如果未打开，自动创建新的会话并启动 nvim
- 支持模糊搜索，快速定位项目目录

## 功能特性

### 🔍 智能项目检测
- 自动检测项目是否已在 WezTerm 中打开
- 精确匹配项目路径，避免误匹配

### 🚀 快速项目切换
- 如果项目已打开：直接激活对应的标签页并切换焦点
- 如果项目未打开：自动创建新标签页/窗口并启动 nvim

### 🔎 模糊搜索支持
- 支持完全匹配、前缀匹配和包含匹配
- 在 HOME 目录下智能搜索项目
- 优先级：完全匹配 > 前缀匹配 > 包含匹配

### 🖥️ 智能窗口管理
- 如果 WezTerm 未运行：自动启动并全屏显示
- 如果 WezTerm 已运行：在现有窗口中创建新标签页
- 自动设置窗口和标签页标题

## 安装与使用

### 安装
```bash
# 克隆项目
git clone <repository-url> ~/wezterm-auto
cd ~/wezterm-auto

# 创建符号链接到 ~/bin（确保 ~/bin 在 PATH 中）
ln -sf "$(pwd)/wezterm-auto" ~/bin/wezterm-auto
```

### 使用方法
```bash
# 使用完整路径
wezterm-auto ~/projects/my-app

# 使用相对路径
wezterm-auto ./my-project

# 使用模糊匹配（在 HOME 目录搜索）
wezterm-auto my-app    # 会找到 ~/my-app 或 ~/my-application
wezterm-auto blog      # 会找到 ~/blog 或 ~/my-blog
```

### 模糊匹配规则
1. **完全匹配**：优先查找完全匹配的目录名
2. **前缀匹配**：查找以输入开头的目录
3. **包含匹配**：查找包含输入字符串的目录

例如，输入 `blog` 时：
- 如果存在 `~/blog`，优先选择它
- 如果不存在但有 `~/blog-site`，选择它
- 最后才考虑 `~/my-blog` 等包含匹配

## 工作原理

### 核心流程
1. **路径解析**：使用模糊匹配算法解析用户输入的项目路径
2. **会话检测**：通过 `wezterm cli list` 检查项目是否已打开
3. **智能切换**：根据检测结果选择激活现有会话或创建新会话
4. **焦点管理**：使用 AppleScript 切换应用焦点和窗口状态

### 技术实现
- **WezTerm CLI**：使用 `wezterm cli` 命令管理窗口、标签页和面板
- **jq**：解析 JSON 格式的窗口信息
- **AppleScript**：实现 macOS 窗口焦点切换和全屏功能
- **Bash**：主要的脚本逻辑和系统调用

## 系统要求

- macOS 系统
- WezTerm 终端
- jq（JSON 处理工具）
- Neovim

## 项目结构

```
wezterm-auto/
├── wezterm-auto           # 主脚本文件
├── README.md              # 项目说明
├── CLAUDE.md              # 开发指南
└── wezterm-cli-docs/      # WezTerm CLI 文档参考
    └── cli/               # 各种 CLI 命令文档
```

## 开发说明

这个项目是在 Claude Code (Anthropic 的 AI 助手) 的协助下协作开发完成的。开发过程包括需求的迭代完善、实现和测试，最终创建了一个强大的 WezTerm 项目管理自动化工具。

## 贡献

欢迎提交 Issues 和 Pull Requests 来改进这个项目。