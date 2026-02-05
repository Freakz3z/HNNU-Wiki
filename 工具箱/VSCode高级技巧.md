# VS Code 高级技巧

VS Code 是目前最流行的代码编辑器之一。掌握这些高级技巧可以让你的开发效率提升数倍！

## 必装插件推荐

### 通用插件

```bash
# Chinese (Simplified) Language Pack
# 简体中文语言包
extension id=MS-CEINTL.vscode-language-pack-zh-hans

# Material Icon Theme
# 精美的文件图标主题
extension id=PKief.material-icon-theme

# Auto Rename Tag
# 自动重命名HTML/XML标签
extension id=formulahendry.auto-rename-tag

# Bracket Pair Colorizer
# 括号配对着色（内置）
# 设置中启用：editor.bracketPairColorization.enabled

# Error Lens
# 在代码行显示错误和警告
extension id=usernamehw.errorlens

# TODO Highlight
# 高亮显示 TODO 注释
extension id=wayou.vscode-todo-highlight

# Code Spell Checker
# 代码拼写检查
extension id=streetsidesoftware.code-spell-checker
```

### Python 开发

```bash
# Python
# Python 语言支持
extension id=ms-python.python

# Python Docstring Generator
# 自动生成文档字符串
extension id=njpwerner.autodocstring

# arepl
# Python 实时运行
extension id=almenon.arepl
```

### Web 开发

```bash
# Prettier
# 代码格式化
extension id=esbenp.prettier-vscode

# ESLint
# JavaScript 代码检查
extension id=dbaeumer.vscode-eslint

# Live Server
# 实时预览网页
extension id=ritwickdey.liveserver

# Auto Close Tag
# 自动关闭标签
extension id=formulahendry.auto-close-tag

# Path Intellisense
# 路径自动补全
extension id=christian-kohler.path-intellisense
```

### Git 工具

```bash
# GitLens
# Git 超级增强
extension id=eamodio.gitlens

# Git History
# Git 历史记录
extension id=donjayamanne.githistory

# GitHub Copilot
# AI 编程助手（付费）
extension id=GitHub.copilot
```

### 效率工具

```bash
# Markdown All in One
# Markdown 全能插件
extension id=yzhang.markdown-all-in-one

# Thunder Client
# API 测试工具（类似 Postman）
extension id=rangav.vscode-thunder-client

# Docker
# Docker 支持
extension id=ms-azuretools.vscode-docker

# Remote Development
# 远程开发（SSH、容器、WSL）
extension id=ms-vscode-remote.remote-containers
extension id=ms-vscode-remote.remote-ssh
extension id=ms-vscode-remote.remote-wsl
```

## 快捷键大全

### 通用快捷键

| 功能 | Windows/Linux | macOS |
|------|---------------|-------|
| 命令面板 | `Ctrl+Shift+P` | `Cmd+Shift+P` |
| 快速打开文件 | `Ctrl+P` | `Cmd+P` |
| 新建文件 | `Ctrl+N` | `Cmd+N` |
| 保存文件 | `Ctrl+S` | `Cmd+S` |
| 另存为 | `Ctrl+Shift+S` | `Cmd+Shift+S` |
| 关闭文件 | `Ctrl+W` | `Cmd+W` |
| 重新打开关闭的文件 | `Ctrl+Shift+T` | `Cmd+Shift+T` |

### 编辑快捷键

| 功能 | Windows/Linux | macOS |
|------|---------------|-------|
| 剪切行 | `Ctrl+X` | `Cmd+X` |
| 复制行 | `Ctrl+C` | `Cmd+C` |
| 粘贴 | `Ctrl+V` | `Cmd+V` |
| 移动行上下 | `Alt+↑/↓` | `Opt+↑/↓` |
| 复制行上下 | `Shift+Alt+↑/↓` | `Shift+Opt+↑/↓` |
| 删除行 | `Ctrl+Shift+K` | `Cmd+Shift+K` |
| 在上方插入行 | `Ctrl+Shift+Enter` | `Cmd+Shift+Enter` |
| 在下方插入行 | `Ctrl+Enter` | `Cmd+Enter` |
| 跳转到匹配的括号 | `Ctrl+Shift+\` | `Cmd+Shift+\` |

### 光标移动

| 功能 | Windows/Linux | macOS |
|------|---------------|-------|
| 移动到行首/尾 | `Home/End` | `Cmd+←/→` |
| 移动到文件首/尾 | `Ctrl+Home/End` | `Cmd+↑/↓` |
| 移动到单词左/右 | `Ctrl+←/→` | `Opt+←/→` |
| 向上/向下滚动 | `Ctrl+↑/↓` | `Cmd+↑/↓` |
| 扩展选区 | `Shift+方向键` | `Shift+方向键` |

### 多光标编辑

| 功能 | Windows/Linux | macOS |
|------|---------------|-------|
| 插入光标 | `Alt+Click` | `Opt+Click` |
| 在上面插入光标 | `Ctrl+Alt+↑` | `Cmd+Opt+↑` |
| 在下面插入光标 | `Ctrl+Alt+↓` | `Cmd+Opt+↓` |
| 跳转到下一个匹配项 | `Ctrl+D` | `Cmd+D` |
| 跳转到所有匹配项 | `Ctrl+Shift+L` | `Cmd+Shift+L` |
| 选中当前行 | `Ctrl+L` | `Cmd+L` |

## 高级编辑技巧

### 1. 多光标编辑

**场景：同时修改多个变量**

```python
# 原代码
name1 = "Alice"
name2 = "Bob"
name3 = "Charlie"

# 操作步骤：
# 1. 光标放在 "name1" 上
# 2. 按 Ctrl+D 选中 "name1"
# 3. 按 Ctrl+D 再次选中 "name2"
# 4. 按 Ctrl+D 再次选中 "name3"
# 5. 直接输入，所有光标同步修改
```

### 2. 列选择模式

```bash
# Windows/Linux: Shift+Alt+拖动鼠标
# macOS: Shift+Opt+拖动鼠标

# 场景：同时编辑多行的相同位置
```

### 3. 快速跳转和导航

```bash
# Ctrl+P (Cmd+P) 快速打开文件
# 输入文件名模糊搜索
# 支持 @ 符号跳转到符号
# 输入 "file.py@function" 直接跳转

# Ctrl+Shift+O (Cmd+Shift+O) 跳转到文件中的符号
# Ctrl+T (Cmd+T) 显示所有符号
```

### 4. 代码折叠

```bash
# Ctrl+Shift+[ (Cmd+Shift+[) 折叠
# Ctrl+Shift+] (Cmd+Shift+]) 展开
# Ctrl+K Ctrl+0 (Cmd+K Cmd+0) 折叠所有
# Ctrl+K Ctrl+J (Cmd+K Cmd+J) 展开所有
```

## 代码片段（Snippets）

### 创建自定义代码片段

1. 打开命令面板：`Ctrl+Shift+P` / `Cmd+Shift+P`
2. 输入"配置用户代码片段"
3. 选择语言（如 Python）

### Python 代码片段示例

```json
{
  "Header Template": {
    "prefix": "header",
    "description": "文件头注释",
    "body": [
      "#!/usr/bin/env python3",
      "# -*- coding: utf-8 -*-",
      "#",
      "# @File: ${TM_FILENAME}",
      "# @Author: Your Name",
      "# @Date: ${CURRENT_YEAR}-${CURRENT_MONTH}-${CURRENT_DATE}",
      ""
    ]
  },
  "Main Function": {
    "prefix": "main",
    "description": "创建主函数",
    "body": [
      "def main():",
      "    ${1:# TODO}",
      "",
      "",
      "if __name__ == '__main__':",
      "    main()"
    ]
  },
  "Print Debug": {
    "prefix": "pp",
    "description": "打印调试",
    "body": ["print(f'${1:var} = {$1}')"]
  }
}
```

### JavaScript 代码片段示例

```json
{
  "Console Log": {
    "prefix": "cl",
    "body": ["console.log('${1:message}', $1);"],
    "description": "打印日志"
  },
  "Arrow Function": {
    "prefix": "af",
    "body": ["const ${1:funcName} = ($2) => {", "\t$0", "};"],
    "description": "箭头函数"
  },
  "React Component": {
    "prefix": "rc",
    "body": [
      "import React from 'react';",
      "",
      "const ${1:ComponentName} = () => {",
      "  return (",
      "    <div>",
      "      $0",
      "    </div>",
      "  );",
      "};",
      "",
      "export default $1;"
    ],
    "description": "React 函数组件"
  }
}
```

### 代码片段变量

| 变量 | 说明 |
|------|------|
| `${TM_FILENAME}` | 文件名 |
| `${TM_FILENAME_BASE}` | 文件名（不含扩展名） |
| `${CURRENT_YEAR}` | 当前年份 |
| `${CURRENT_MONTH}` | 当前月份 |
| `${CURRENT_DATE}` | 当前日期 |
| `${1:placeholder}` | 光标位置1 |
| `${0}` | 最终光标位置 |

## 高级搜索

### 搜索和替换

```bash
# Ctrl+H (Cmd+H) 搜索替换
# Ctrl+Shift+H (Cmd+Shift+H) 全局搜索替换

# 正则表达式搜索
# 点击 .* 按钮启用正则

# 示例：删除所有 console.log
# 查找：console\.log\(.*\);
# 替换：留空
```

### 多文件搜索

```bash
# Ctrl+Shift+F (Cmd+Shift+F) 全局搜索
# Ctrl+Shift+H (Cmd+Shift+H) 全局替换

# 在搜索框中：
# include   - 包含的文件模式
# exclude   - 排除的文件模式
```

## 调试技巧

### 配置调试

创建 `.vscode/launch.json`：

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Python: Current File",
      "type": "debugpy",
      "request": "launch",
      "program": "${file}",
      "console": "integratedTerminal"
    },
    {
      "name": "Chrome: Launch",
      "type": "chrome",
      "request": "launch",
      "url": "http://localhost:8080",
      "webRoot": "${workspaceFolder}"
    }
  ]
}
```

### 调试快捷键

| 功能 | Windows/Linux | macOS |
|------|---------------|-------|
| 开始调试 | `F5` | `F5` |
| 设置断点 | `F9` | `F9` |
| 单步跳过 | `F10` | `F10` |
| 单步进入 | `F11` | `F11` |
| 单步跳出 | `Shift+F11` | `Shift+F11` |
| 继续执行 | `F5` | `F5` |
| 停止调试 | `Shift+F5` | `Shift+F5` |

## 终端使用

### 终端快捷键

| 功能 | Windows/Linux | macOS |
|------|---------------|-------|
| 新建终端 | `Ctrl+Shift+`` | `Cmd+Shift+`` |
| 切换终端 | `Ctrl+Shift+↑/↓` | `Cmd+Shift+↑/↓` |
| 分割终端 | `Ctrl+Shift+5` | `Cmd+Shift+5` |
| 关闭终端 | `Ctrl+Shift+W` | `Cmd+Shift+W` |

### 终端配置

```json
// settings.json
{
  "terminal.integrated.fontSize": 14,
  "terminal.integrated.fontFamily": "Fira Code",
  "terminal.integrated.shell.windows": "C:\\Windows\\System32\\wsl.exe",
  "terminal.integrated.shell.osx": "/bin/zsh",
  "terminal.integrated.shell.linux": "/bin/zsh"
}
```

## 工作区配置

### 推荐的 settings.json

```json
{
  // 编辑器
  "editor.fontSize": 14,
  "editor.tabSize": 2,
  "editor.insertSpaces": true,
  "editor.wordWrap": "on",
  "editor.minimap.enabled": true,
  "editor.formatOnSave": true,
  "editor.formatOnPaste": true,
  "editor.suggestSelection": "first",
  "editor.bracketPairColorization.enabled": true,
  "editor.guides.bracketPairs": true,

  // 文件
  "files.autoSave": "afterDelay",
  "files.autoSaveDelay": 1000,
  "files.exclude": {
    "**/__pycache__": true,
    "**/.git": true,
    "**/.DS_Store": true,
    "**/node_modules": true
  },

  // 主题
  "workbench.colorTheme": "One Dark Pro",
  "workbench.iconTheme": "material-icon-theme",

  // Python
  "python.defaultInterpreterPath": "/usr/bin/python3",
  "python.formatting.provider": "black",
  "python.linting.enabled": true,
  "python.linting.pylintEnabled": true,

  // 其他
  "telemetry.telemetryLevel": "off",
  "update.mode": "manual"
}
```

## Git 集成

### Git 快捷键

| 功能 | Windows/Linux | macOS |
|------|---------------|-------|
| 打开源代码管理 | `Ctrl+Shift+G` | `Cmd+Shift+G` |
| 提交 | `Ctrl+Enter` | `Cmd+Enter` |
| 推送 | `Ctrl+Shift+H` | `Cmd+Shift+H` |
| 拉取 | `Ctrl+Shift+L` | `Cmd+Shift+L` |
| 放弃更改 | `Ctrl+Shift+Backspace` | `Cmd+Shift+Backspace` |

### Git Lens 功能

- **代码注释** - 查看每行代码的最后修改人
- **代码历史** - 查看文件的修改历史
- **比较分支** - 可视化分支差异
- **仓库状态** - 查看提交和分支信息

## 性能优化

### 提升性能的设置

```json
{
  // 禁用不必要的功能
  "extensions.autoUpdate": false,
  "extensions.ignoreRecommendations": true,
  "git.enabled": true,
  "git.decorations.enabled": false,

  // 优化内存
  "files.watcherExclude": {
    "**/__pycache__/**": true,
    "**/node_modules/**": true,
    "**/.git/objects/**": true
  },

  // 禁用遥测
  "telemetry.telemetryLevel": "off"
}
```

### 禁用重文件

```json
{
  "files.exclude": {
    "**/.git": true,
    "**/.svn": true,
    "**/.hg": true,
    "**/CVS": true,
    "**/.DS_Store": true,
    "**/Thumbs.db": true,
    "**/node_modules": true
  },

  "search.exclude": {
    "**/node_modules": true,
    "**/bower_components": true,
    "**/dist": true,
    "**/build": true
  }
}
```

## 实用技巧

### 1. 命令面板技巧

```bash
# Ctrl+Shift+P (Cmd+Shift+P)

# 常用命令：
- 重载窗口: Reload Window
- 切换主题: Preferences: Color Theme
- 打开设置: Preferences: Open Settings
- 键盘快捷方式: Preferences: Keyboard Shortcuts
- 安装扩展: Install Extensions
```

### 2. 快速修复

```bash
# 光标放在错误上
# Ctrl+. (Cmd+.) 显示快速修复菜单
# 自动修复问题
```

### 3. 资源管理器操作

```bash
# Ctrl+B (Cmd+B) 切换侧边栏
# Ctrl+Shift+E (Cmd+Shift+E) 聚焦资源管理器
# 创建文件: a.txt
# 创建目录: dir/
```

### 4. 分屏编辑

```bash
# Ctrl+\ (Cmd+\) 分屏
# Ctrl+1/2/3 (Cmd+1/2/3) 切换编辑器组
# Ctrl+Alt+方向键 (Cmd+Opt+方向键) 移动编辑器
```

### 5. 任务和问题

```bash
# Ctrl+Shift+B (Cmd+Shift+B) 运行任务
# Ctrl+Shift+M (Cmd+Shift+M) 显示问题面板
```

## 键盘映射自定义

创建 `keybindings.json`：

```json
[
  {
    "key": "ctrl+d",
    "command": "editor.action.duplicateSelection"
  },
  {
    "key": "ctrl+shift+k",
    "command": "editor.action.deleteLines"
  },
  {
    "key": "ctrl+alt+down",
    "command": "editor.action.insertCursorBelow",
    "when": "editorTextFocus"
  }
]
```

## 远程开发

### SSH 远程连接

1. 安装 "Remote - SSH" 扩展
2. 配置 SSH 配置文件：

```bash
# ~/.ssh/config
Host myserver
    HostName 192.168.1.100
    User username
    Port 22
```

3. 连接：`Ctrl+Shift+P` -> "Remote-SSH: Connect to Host"

### 容器开发

```bash
# 安装 "Dev Containers" 扩展
# 在项目中创建 .devcontainer/devcontainer.json

{
  "name": "Python Dev",
  "image": "python:3.11",
  "extensions": [
    "ms-python.python",
    "ms-python.vscode-pylance"
  ],
  "settings": {
    "python.defaultInterpreterPath": "/usr/local/bin/python"
  }
}
```

## 学习资源

- [VS Code 官方文档](https://code.visualstudio.com/docs)
- [VS Code 技巧](https://vscodecandothat.com/)
- [VS Code Can Do That?](https://vscodecandothat.com/)

## 总结

掌握这些 VS Code 高级技巧，可以让你的开发效率倍增！建议：

1. **循序渐进** - 先掌握最常用的快捷键
2. **定期练习** - 每天使用1-2个新技巧
3. **自定义配置** - 根据自己的习惯调整
4. **关注更新** - VS Code 每月更新，关注新功能

祝你编程愉快！⚡
