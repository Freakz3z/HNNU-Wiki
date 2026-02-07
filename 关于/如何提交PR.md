# 如何提交 PR

提交 GitHub Pull Request（PR）是将你的代码变更合并到目标仓库的正式方式，通过 PR，你可以参与到本手册的制作与修改中。在阅读以下内容前，请保证你下载了 **Git**，详见 [Git的介绍](/工具箱/Git.md)。

以下是详细步骤：

---

### **1. Fork 目标仓库**

1. 访问目标仓库（如 `https://github.com/owner/repo`）。
2. 点击右上角的 **"Fork"**，将仓库复制到你的 GitHub 账号下。

---

### **2. 克隆你的 Fork 到本地**

```bash
git clone https://github.com/your-username/repo.git
cd repo
```

---

### **3. 添加远程上游仓库（可选但推荐）**

关联原始仓库，方便同步最新代码：

```bash
git remote add upstream https://github.com/owner/repo.git
```

---

### **4. 创建新分支**

基于最新代码创建分支，避免直接修改 `main/master`：

```bash
git checkout -b your-feature-branch
```

---

### **5. 修改代码并提交**

* 在本地完成代码修改后，提交变更：

  ```bash
  git add .
  git commit -m "描述你的变更（清晰且简洁）"
  ```

---

### **6. 推送分支到你的 Fork**

```bash
git push origin your-feature-branch
```

---

### **7. 创建 Pull Request**

1. 访问你的 Fork 仓库页面（`https://github.com/your-username/repo`）。
2. GitHub 通常会检测新分支并显示 **"Compare & pull request"** 按钮，点击它。
   * 如果没有自动提示，切换到你的分支后点击 **"Contribute" → "Open pull request"**。
3. 填写 PR 信息：
   * **标题**：简明概括变更（如 "Fix login page CSS"）。
   * **描述**：详细说明修改内容、原因（可引用相关 Issue）。
4. 选择 **目标仓库和分支**（如 `owner/repo:main`）。
5. 点击 **"Create pull request"**。

---

### **8. 等待审核**

* 维护者会审查代码，可能要求修改。根据反馈更新分支后，新的提交会自动添加到 PR。
* 如果目标仓库有 CI/CD，确保所有检查通过。

---

### **9. 同步最新代码（如需更新 PR）**

如果原始仓库有更新，同步到你的分支：

```bash
git fetch upstream
git rebase upstream/main  # 或 merge
git push -f origin your-feature-branch  # 强制推送（如果用了 rebase）
```

---

### **关键注意事项**

1. **分支规范**：遵循项目的分支命名规则（如 `fix/xxx`、`feat/xxx`）。
2. **提交信息**：清晰且符合项目约定（如 [Conventional Commits](https://www.conventionalcommits.org/)）。
3. **代码风格**：与目标仓库保持一致（缩进、注释等）。
4. **小规模 PR**：一个 PR 尽量只解决一个问题，便于审查。

---

完成！等待维护者合并即可。如果有问题，直接在 PR 评论区讨论。
