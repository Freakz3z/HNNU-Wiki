在 [OI-Wiki](https://oi-wiki.org/tools/git/) 中有对于 Git 的详细介绍，但笔者认为这些介绍过于复杂了，所以在这里简短介绍一下 Git。

> Git 可以在集成了 Git 的 IDE 中使用，也可以在cmd、powershell中使用。

# Git 简介

Git 是一个分布式版本控制系统，广泛用于源代码管理和协作开发。它允许多个开发者在同一项目上并行工作，同时跟踪和管理代码的历史更改。

[Git 下载](https://git-scm.com/downloads)

# 常用命令

## 1. 配置用户信息
在开始使用 Git 之前，通常需要设置你的用户名和邮箱：
```bash
git config --global user.name "Your Name"
```
```bash
git config --global user.email "your_email@example.com"
```

## 2. 创建和克隆仓库
- **创建新的 Git 仓库**：
  ```bash
  git init
  ```

- **克隆现有仓库**：
  ```bash
  git clone <repository-url>
  ```

## 3. 查看状态
- **查看当前工作目录和暂存区的状态**：
  ```bash
  git status
  ```

## 4. 添加和提交更改
- **将更改添加到暂存区**：
  ```bash
  git add <file>
  ```
  - 添加所有更改：
    ```bash
    git add .
    ```

- **提交更改**：
  ```bash
  git commit -m "Commit message"
  ```

## 5. 查看提交历史
- **查看提交记录**：
  ```bash
  git log
  ```

- **查看简洁的提交历史**：
  ```bash
  git log --oneline
  ```

## 6. 分支管理
- **查看所有分支**：
  ```bash
  git branch
  ```

- **创建新分支**：
  ```bash
  git branch <branch-name>
  ```

- **切换到另一个分支**：
  ```bash
  git checkout <branch-name>
  ```
  - 创建并切换到新分支（简写）：
    ```bash
    git checkout -b <branch-name>
    ```

- **删除分支**：
  ```bash
  git branch -d <branch-name>
  ```

## 7. 合并分支
- **将一个分支合并到当前分支**：
  ```bash
  git merge <branch-name>
  ```

## 8. 远程仓库管理
- **查看远程仓库**：
  ```bash
  git remote -v
  ```

- **添加远程仓库**：
  ```bash
  git remote add <remote-name> <repository-url>
  ```

- **推送更改到远程仓库**：
  ```bash
  git push <remote-name> <branch-name>
  ```

- **从远程仓库拉取更改**：
  ```bash
  git pull <remote-name> <branch-name>
  ```

- **获取远程仓库的更新**（不合并）：
  ```bash
  git fetch <remote-name>
  ```

## 9. 撤销操作
- **撤销暂存区的更改**：
  ```bash
  git reset <file>
  ```

- **撤销对工作目录的更改**（恢复到最后一次提交状态）：
  ```bash
  git checkout -- <file>
  ```

- **撤销最近的提交，但保留更改**：
  ```bash
  git reset HEAD~1
  ```

## 10. 标签管理
- **创建标签**：
  ```bash
  git tag -a <tag-name> -m "Tag message"
  ```

- **查看标签**：
  ```bash
  git tag
  ```

- **推送标签到远程**：
  ```bash
  git push <remote-name> <tag-name>
  ```

# Git 与 GitHub

```
echo "# example" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/Freakz3z/example.git
git push -u origin main
```

# 使用场景

* **软件开发**：广泛用于开源和商业软件项目的版本控制。
* **文档管理**：用于管理文档版本和变更。
* **团队协作**：支持多个开发者在同一项目上工作的工具。

> 个人使用Git较多的地方是将本地项目提交到Github仓库，例如本手册。以及快速进行版本回滚，这样就不会出现多次保存一个项目的情况。