# Git 新手速查（Deep Design 版）

## 每天开始工作

```powershell
# 打开 Cursor 前，确认今天要改哪个项目
notepad D:\DD-cursor\WORKSPACE.md
# 或
notepad D:\DD-cursor\_workspace\PROJECTS.yaml
```

## 四个核心项目的进入命令

```powershell
# 营销站
cd D:\DD-cursor
git remote -v    # 应显示 dd-deep-design

# 方案中心
cd D:\DD-cursor\scheme-center
git remote -v    # 应显示 dd-design

# THOR 报价
cd D:\DD-cursor\thor-quote
git remote -v    # 应显示 thor-quote

# 交付标准
cd D:\DD-cursor\delivery-system
git remote -v    # 应显示 delivery-system
```

## 保存并上线（通用）

```powershell
git status                           # 看改了什么
git add .                            # 全部暂存（或 git add 具体文件）
git commit -m "fix: 修正首页文案"     # 写清楚改了什么
git push origin main                 # master 项目把 main 换成 master
```

## 常见情况

### 第一次连接 GitHub（新项目）

```powershell
git init
git remote add origin https://github.com/zhouxianliang73/仓库名.git
git add .
git commit -m "init: 项目初始化"
git branch -M main
git push -u origin main
```

### push 被拒绝（远程有 README）

```powershell
git pull origin main --rebase
git push origin main
```

### 改错目录了怎么办

```powershell
# 在未 commit 前
git checkout -- .          # 撤销所有未暂存修改（谨慎！）
# 或进正确目录重新改
```

### 查看历史

```powershell
git log --oneline -10
```

## 不要做的事

- 不要在 `D:\DD-cursor` 根目录 `git add .` 时期望提交子项目
- 不要把 `.env`、密码、客户隐私 commit 上去
- 不要 `git push --force` 到 main/master（除非非常确定）
- 不要同时在 GitHub 网页和本地改同一文件（容易冲突）

## 客户分享链接

每个 Core 项目的 Pages 就是预览/交付链接，直接发 URL，无需发文件。

| 项目 | 链接 |
|------|------|
| 营销站 | https://zhouxianliang73.github.io/dd-deep-design/ |
| 方案中心 | https://zhouxianliang73.github.io/dd-design/ |
| THOR 报价 | https://zhouxianliang73.github.io/thor-quote/ |
| 交付标准 | https://zhouxianliang73.github.io/delivery-system/ |
