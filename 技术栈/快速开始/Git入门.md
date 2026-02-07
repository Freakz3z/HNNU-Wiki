# Git 入门指南

## 为什么需要 Git？

Git 是目前世界上最先进的**分布式版本控制系统**，是程序员必备技能。

**Git 的核心价值：**
1. **版本控制** - 记录每次修改，随时回退
2. **团队协作** - 多人开发同一项目
3. **代码备份** - 远程仓库托管代码
4. **分支管理** - 独立开发功能，互不影响
5. **开源贡献** - GitHub 上的项目都用 Git

**真实场景：**
- ❌ 没有 Git：`代码_final.py`、`代码_final2.py`、`代码_真的final.py`
- ✅ 有 Git：清晰的版本历史，随时回退

## 第一步：安装 Git

### Windows
1. 访问 [Git官网](https://git-scm.com/downloads)
2. 下载 Windows 安装包
3. 安装时保持默认选项（建议选择 VS Code 作为默认编辑器）
4. 验证安装：打开 Git Bash，输入 `git --version`

### macOS
```bash
# 方式一：使用 Homebrew
brew install git

# 方式二：安装 Xcode Command Line Tools（自带 Git）
xcode-select --install

# 验证安装
git --version
```

### Linux
```bash
# Ubuntu/Debian
sudo apt update
sudo apt install git

# CentOS/RHEL
sudo yum install git

# 验证安装
git --version
```

## 第二步：初始配置

安装完成后，需要先配置用户信息：

```bash
# 配置用户名（建议使用 GitHub 用户名）
git config --global user.name "你的名字"

# 配置邮箱（建议使用 GitHub 邮箱）
git config --global user.email "your.email@example.com"

# 查看配置
git config --global --list

# 设置默认分支名称为 main
git config --global init.defaultBranch main
```

**常用配置选项：**
```bash
# 设置 VS Code 为默认编辑器
git config --global core.editor "code --wait"

# 设置换行符（Windows 推荐）
git config --global core.autocrlf true

# 开启颜色显示
git config --global color.ui true
```

## 第三步：Git 基础概念

### Git 的三个区域

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│  工作区      │ ──> │  暂存区      │ ──> │  本地仓库    │
│ (Working)   │ add │ (Stage)     │commit│ (Repository)│
│             │     │             │     │             │
│ 你的文件     │     │ 准备提交的   │     │ 已提交的内容 │
└─────────────┘     └─────────────┘     └─────────────┘
```

**三个区域的说明：**
1. **工作区（Working Directory）**：你在电脑上看到的目录
2. **暂存区（Stage/Index）**：临时存放修改的地方
3. **本地仓库（Repository）**：永久保存版本历史的地方

### Git 工作流程

```
1. 修改文件
   ↓
2. git add（添加到暂存区）
   ↓
3. git commit（提交到本地仓库）
   ↓
4. git push（推送到远程仓库）
```

## 第四步：Git 基础命令

### 1. 创建仓库

```bash
# 初始化新仓库
git init

# 克隆远程仓库
git clone https://github.com/username/repo.git
```

### 2. 查看状态

```bash
# 查看仓库状态
git status

# 查看文件修改内容
git diff

# 查看已暂存的修改
git diff --staged

# 查看提交历史
git log

# 简洁的日志显示
git log --oneline

# 图形化显示分支历史
git log --graph --oneline --all
```

### 3. 添加和提交

```bash
# 添加指定文件到暂存区
git add filename.py

# 添加所有修改的文件
git add .

# 添加所有文件（包括删除）
git add -A

# 提交暂存区的修改
git commit -m "提交说明"

# 添加并提交（一步完成）
git commit -am "提交说明"
```

**提交信息规范：**
```bash
# 好的提交信息
git commit -m "feat: 添加用户登录功能"
git commit -m "fix: 修复密码验证bug"
git commit -m "docs: 更新README文档"

# 不好的提交信息
git commit -m "更新"
git commit -m "修改bug"
git commit -m "a"
```

### 4. 查看和回退

```bash
# 查看指定文件的修改历史
git log filename.py

# 查看某次提交的详细内容
git show 提交ID

# 回退到指定版本（保留工作区修改）
git reset --soft HEAD~1

# 回退到指定版本（取消暂存）
git reset --mixed HEAD~1

# 回退到指定版本（丢弃所有修改）⚠️
git reset --hard HEAD~1

# 恢复某个文件到指定版本
git checkout HEAD~1 filename.py
```

## 第五步：分支管理

### 为什么需要分支？

```
main（主分支）     feature/login（功能分支）
    │                    │
    │  ┌─────────────────┤
    │  │ 并行开发        │
    │  └─────────────────┤
    │                    │
    ○ ←────────────────── ○ （合并）
```

**分支的优势：**
- 多人协作互不影响
- 开发新功能不破坏主代码
- 易于实验和尝试

### 分支命令

```bash
# 查看所有分支
git branch

# 查看所有分支（包含远程）
git branch -a

# 创建新分支
git branch feature-login

# 切换到指定分支
git checkout feature-login

# 创建并切换到新分支（一步完成）
git checkout -b feature-login

# 切换回主分支
git checkout main

# 合并分支
git merge feature-login

# 删除已合并的分支
git branch -d feature-login

# 强制删除分支
git branch -D feature-login
```

### 实战：功能开发流程

```bash
# 1. 从主分支创建功能分支
git checkout main
git checkout -b feature-add-login

# 2. 在功能分支上开发
echo "登录功能代码" > login.py
git add login.py
git commit -m "feat: 添加用户登录功能"

# 3. 切换回主分支
git checkout main

# 4. 合并功能分支
git merge feature-add-login

# 5. 删除功能分支
git branch -d feature-add-login
```

## 第六步：远程仓库（GitHub/Gitee）

### 创建远程仓库

**GitHub：**
1. 访问 [GitHub](https://github.com/)
2. 点击右上角 "+" → "New repository"
3. 填写仓库名称、描述
4. 选择 Public 或 Private
5. 点击 "Create repository"

**Gitee（码云）：**
1. 访问 [Gitee](https://gitee.com/)
2. 点击右上角 "+" → "新建仓库"
3. 填写仓库信息
4. 点击 "创建"

### 连接远程仓库

```bash
# 查看远程仓库
git remote -v

# 添加远程仓库
git remote add origin https://github.com/username/repo.git

# 修改远程仓库地址
git remote set-url origin https://github.com/username/new-repo.git

# 删除远程仓库
git remote remove origin
```

### 推送和拉取

```bash
# 第一次推送（设置上游分支）
git push -u origin main

# 推送到远程仓库
git push

# 拉取远程更新
git pull

# 拉取远程更新但不合并
git fetch

# 拉取指定分支
git pull origin main
```

### 实战：完整工作流程

```bash
# 1. 克隆仓库
git clone https://github.com/username/repo.git
cd repo

# 2. 创建功能分支
git checkout -b feature-new

# 3. 修改文件
echo "新功能" > new_feature.py

# 4. 提交修改
git add new_feature.py
git commit -m "feat: 添加新功能"

# 5. 推送到远程
git push -u origin feature-new

# 6. 在 GitHub 上创建 Pull Request

# 7. 合并后更新主分支
git checkout main
git pull origin main

# 8. 删除本地功能分支
git branch -d feature-new
```

## 第七步：常见场景

### 场景1：修改了最后一个提交

```bash
# 发现提交信息写错了
git commit -m "feat: 添加登"
# 应该是"添加登录功能"

# 修改最后一次提交（不改变内容）
git commit --amend -m "feat: 添加登录功能"

# 修改最后一次提交（添加新文件）
git add forgotten_file.py
git commit --amend -m "feat: 添加登录功能"
```

### 场景2：暂存当前工作

```bash
# 临时切换分支，但当前有未提交的修改
git stash

# 切换到其他分支工作
git checkout other-branch

# 完成后切换回来
git checkout main

# 恢复暂存的工作
git stash pop

# 查看暂存列表
git stash list

# 删除暂存
git stash drop
```

### 场景3：撤销文件的修改

```bash
# 撤销工作区的修改（恢复到上次提交的状态）
git restore filename.py

# 撤销暂存区的修改（保留工作区）
git restore --staged filename.py

# 删除未跟踪的文件
git clean -f

# 删除未跟踪的文件和目录
git clean -fd
```

### 场景4：查看某文件的历史版本

```bash
# 查看文件的所有修改记录
git log --follow filename.py

# 查看指定版本的文件内容
git show 提交ID:filename.py

# 恢复文件到指定版本
git checkout 提交ID filename.py
```

## 第八步：忽略文件

### .gitignore 文件

在项目根目录创建 `.gitignore` 文件：

```gitignore
# Python
__pycache__/
*.py[cod]
*$py.class
*.so
.Python
venv/
env/
ENV/

# IDE
.vscode/
.idea/
*.swp
*.swo

# 系统文件
.DS_Store
Thumbs.db

# 项目特定
config.py
*.log
.env

# 临时文件
tmp/
temp/
```

**忽略文件模板：**
- [Python .gitignore](https://github.com/github/gitignore/blob/main/Python.gitignore)
- [Node.js .gitignore](https://github.com/github/gitignore/blob/main/Node.gitignore)
- [Visual Studio Code .gitignore](https://github.com/github/gitignore/blob/main/VisualStudioCode.gitignore)

## 第九步：团队协作

### Pull Request 工作流

```bash
# 1. Fork 原项目
# 在 GitHub 上点击 Fork 按钮

# 2. 克隆你 Fork 的仓库
git clone https://github.com/your-username/repo.git
cd repo

# 3. 添加上游仓库
git remote add upstream https://github.com/original-owner/repo.git

# 4. 创建功能分支
git checkout -b feature-new

# 5. 进行开发
# 修改文件...
git add .
git commit -m "feat: 添加新功能"

# 6. 推送到你的仓库
git push origin feature-new

# 7. 在 GitHub 上创建 Pull Request

# 8. 同步上游更新
git fetch upstream
git checkout main
git merge upstream/main

# 9. 推送到你的仓库
git push origin main
```

### 解决冲突

```bash
# 1. 拉取时遇到冲突
git pull origin main
# CONFLICT (content): Merge conflict in file.py

# 2. 手动解决冲突
# 打开文件，找到冲突标记：
# <<<<<<< HEAD
# 你的修改
# =======
# 别人的修改
# >>>>>>> origin/main

# 3. 编辑文件，保留需要的代码，删除冲突标记

# 4. 标记为已解决
git add file.py

# 5. 完成合并
git commit
```

## 第十步：实用技巧

### 查看命令别名

```bash
# 创建常用命令别名
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'

# 使用别名
git st        # 等同于 git status
git co main   # 等同于 git checkout main
```

### 查看漂亮的日志

```bash
# 单行显示
git log --oneline

# 图形化显示
git log --graph --oneline --decorate --all

# 自定义格式
git log --pretty=format:"%h - %an, %ar : %s" --graph

# 简短统计
git log --stat
```

### 搜索代码

```bash
# 搜索包含特定内容的提交
git log -S "function_name"

# 搜索提交信息
git log --grep="bug"

# 在代码中搜索
git grep "keyword"
```

### Git 钩子（自动化）

```bash
# 钩子目录
.git/hooks/

# 示例：提交前自动运行测试
# .git/hooks/pre-commit
#!/bin/bash
pytest

# 保存后需要添加执行权限
chmod +x .git/hooks/pre-commit
```

## 最佳实践

### ✅ 提交规范

```bash
# 提交信息格式
<type>(<scope>): <subject>

<body>

<footer>
```

**type 类型：**
- `feat`：新功能
- `fix`：修复bug
- `docs`：文档修改
- `style`：代码格式（不影响功能）
- `refactor`：重构
- `test`：添加测试
- `chore`：构建过程或辅助工具的变动

**示例：**
```bash
git commit -m "feat(auth): 添加用户登录功能"
git commit -m "fix(api): 修复用户列表查询bug"
git commit -m "docs(readme): 更新安装说明"
```

### ✅ 分支管理

```bash
# 主分支命名
main        # 生产环境
develop     # 开发环境

# 功能分支
feature/xxx # 新功能
bugfix/xxx  # bug修复
hotfix/xxx  # 紧急修复
```

### ✅ 代码审查

1. 所有修改通过分支进行
2. 使用 Pull Request 合并代码
3. 必须经过代码审查
4. 保持提交历史清晰

### ✅ 安全建议

1. **不要提交敏感信息**
   - 密码、API密钥
   - 配置文件中的私密信息
   - 使用 `.gitignore` 忽略

2. **定期备份**
   - 推送到远程仓库
   - 使用 GitHub/Gitee 双备份

3. **使用强密码和2FA**
   - GitHub 账号开启双重认证
   - 使用 SSH 而非 HTTPS

## 常见问题

### Q1: Git 和 GitHub 有什么区别？
**A**:
- **Git**：版本控制工具（软件）
- **GitHub**：代码托管平台（网站）
- 关系：类似 Word 和 Google Docs

### Q2: merge 和 rebase 有什么区别？
**A**:
- `merge`：保留完整历史，有合并提交
- `rebase`：线性历史，更清晰
- 建议：本地用 rebase，远程用 merge

### Q3: 如何撤销一次错误的提交？
**A**:
```bash
# 未推送到远程
git reset --hard HEAD~1

# 已推送到远程（危险！）
git reset --hard HEAD~1
git push -f  # 强制推送
```

### Q4: origin 和 upstream 有什么区别？
**A**:
- `origin`：你自己 Fork 的仓库
- `upstream`：原始仓库
- 用于开源项目贡献

### Q5: 如何清理 Git 历史？
**A**:
```bash
# 清理未引用的文件
git gc

# 清理大文件
git filter-branch --tree-filter 'rm -f path/to/large/file' HEAD
```

## 学习资源

### 官方资源
- [Git 官方文档](https://git-scm.com/doc)
- [Pro Git 中文版](https://git-scm.com/book/zh/v2)
- [GitHub Git 指南](https://guides.github.com/)

### 在线教程
- [廖雪峰 Git 教程](https://www.liaoxuefeng.com/wiki/896043488029600)
- [Git - 简明指南](https://rogerdudler.github.io/git-guide/index.zh.html)
- [Learn Git Branching](https://learngitbranching.js.org/)（交互式教程）

### 视频教程
- B站搜索：Git 入门教程
- 推荐：尚硅谷 Git 课程

### 实用工具
- [Oh My Zsh Git 插件](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins#git)
- [GitLens（VS Code 扩展）](https://gitlens.amod.io/)

## 下一步学习

1. **深入学习 Git**
   - Git 内部原理
   - 高级命令（rebase、cherry-pick）
   - Git 钩子自动化

2. **GitHub 进阶**
   - GitHub Actions CI/CD
   - GitHub Pages
   - 项目管理工具（Issues、Projects）

3. **团队协作**
   - Git Flow 工作流
   - 代码审查最佳实践
   - 多人协作技巧

---

**最后提醒**：
- 💡 多用 `git status` 查看状态
- 🎯 提交信息要清晰
- 📚 定期推送到远程备份
- 🚀 不要害怕用 Git，大胆尝试！

祝你 Git 学习愉快！🎉
