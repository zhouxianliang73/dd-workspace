# DD 工作区元数据

此目录**不是业务站点**，存放项目组合管理文档。

| 文件 | 用途 |
|------|------|
| [PORTFOLIO.md](./PORTFOLIO.md) | 完整治理规范（命名、矩阵、Checklist） |
| [PROJECTS.yaml](./PROJECTS.yaml) | 项目台账（所有仓库一览） |
| [WORKFLOW.md](./WORKFLOW.md) | Git 新手日常命令 |

## 建议

在 GitHub 创建 **`dd-workspace`** 仓库，仅用于备份这些文档：

```powershell
cd D:\DD-cursor\_workspace
git init
git remote add origin https://github.com/zhouxianliang73/dd-workspace.git
git add .
git commit -m "init: portfolio governance docs"
git branch -M main
git push -u origin main
```

快速索引见上级目录 [WORKSPACE.md](../WORKSPACE.md)。
