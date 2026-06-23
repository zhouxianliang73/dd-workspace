# DD 项目组合管理规范（Portfolio Governance）

> 版本 1.0 · 适用于 Deep Design 不锈钢定制业务  
> 本地路径：`D:\DD-cursor\_workspace\`  
> GitHub 建议仓库：`dd-workspace`（仅存文档，不部署 Pages）

---

## 一、核心原则（行业标准）

### 1. 一仓一产品（One Repo = One Deployable）

每个**可独立上线**的产品/站点 = **一个 GitHub 仓库** + **一个 GitHub Pages（或独立域名）**。

| 要做 | 不要做 |
|------|--------|
| 营销站、方案中心、报价、交付标准各自独立仓库 | 把所有 HTML 塞进一个大仓库 |
| 改哪个项目，进哪个目录，push 哪个仓库 | 在 OpenClaw/Cursor 里混改多个项目一次 commit |
| GitHub 作为唯一真相源（Source of Truth） | 只在本地改、不上传 |
| 本地 `D:\DD-cursor` 是**开发工作区**（文件夹容器） | 把子项目文件 commit 进营销站仓库 |

### 2. 工作区 ≠  Git 仓库

```
D:\DD-cursor\                 ← 文件夹（容器）
├── （根目录 .git）             ← 仅 = 营销站 dd-deep-design
├── scheme-center\.git         ← 独立 = dd-design
├── thor-quote\.git            ← 独立 = thor-quote
└── delivery-system\.git       ← 独立 = delivery-system
```

营销站根目录的 Git **只管理** `index.html`、`assets/`、`favicon.svg` 等营销站文件。  
子目录已在根 `.gitignore` 中排除，**永远不要** `git add scheme-center/`。

### 3. 数据流向（业务链路）

```
获客          方案/选品        报价           交付文档
  ↓              ↓              ↓              ↓
营销站  →   方案中心  →   THOR报价  →   交付标准
dd-deep     dd-design      thor-quote    delivery-system
```

后续矩阵项目（落地页、供应商工具等）是**侧向扩展**，不替代上述主链。

---

## 二、业务矩阵

### 核心层（Core）— 当前必须维护

| 代号 | 名称 | 本地目录 | GitHub | Pages | 职责 |
|------|------|----------|--------|-------|------|
| MKT | 营销站 | `D:\DD-cursor\`（根） | [dd-deep-design](https://github.com/zhouxianliang73/dd-deep-design) | [/dd-deep-design/](https://zhouxianliang73.github.io/dd-deep-design/) | 品牌、获客、户外厨房官网 |
| SC | 方案中心 | `scheme-center\` | [dd-design](https://github.com/zhouxianliang73/dd-design) | [/dd-design/](https://zhouxianliang73.github.io/dd-design/) | 项目方案、选品、catalog |
| TQ | THOR 报价 | `thor-quote\` | [thor-quote](https://github.com/zhouxianliang73/thor-quote) | [/thor-quote/](https://zhouxianliang73.github.io/thor-quote/) | 不锈钢橱柜报价引擎 |
| DS | 交付标准 | `delivery-system\` | [delivery-system](https://github.com/zhouxianliang73/delivery-system) | [/delivery-system/](https://zhouxianliang73.github.io/delivery-system/) | 对外交付文档模板 |

### 矩阵层（Matrix）— 围绕核心扩展

| 代号 | 名称 | 本地目录 | 状态 | 建议 GitHub 名 |
|------|------|----------|------|----------------|
| SS | 供应商选择器 | `supplier-selector\` | 本地有仓，无 remote | `supplier-selector` |
| OS | 户外方案站 | `outdoor-solutions独立站\` | 本地有仓，无 remote | `outdoor-solutions` |
| KL | 厨房落地页 | 未迁入 | 待定 | `kitchen-landing` |

**矩阵项目规则：**
- 新建时放在 `D:\DD-cursor\matrix\<项目名>\`（迁入后从根目录移入 matrix）
- 命名：小写 + 连字符（kebab-case），与 GitHub 仓库名一致
- 必须有 `README.md`（一句话说明用途 + Pages 链接）
- 上线前必须：建 GitHub 仓库 → push → 开 Pages → 登记到 `PROJECTS.yaml`

### 归档层（Archive）

废弃或暂停的项目移入 `D:\DD-cursor\_archive\`，**不删除**，仓库可设为 GitHub Archive。

---

## 三、命名规范

| 对象 | 规范 | 示例 |
|------|------|------|
| GitHub 仓库 | 小写 kebab-case | `delivery-system` |
| 本地文件夹 | 与仓库名一致（英文） | `delivery-system\` |
| 默认分支 | `main`（新仓库统一；旧仓库 `master` 可保留） | `main` |
| 静态站点入口 | 必须有 `index.html` | — |
| 大文件/内嵌图 | `.gitignore` 排除，或放 `assets/` 外链 | `delivery-page-template.html` |
| 提交信息 | 英文动词开头，简短 | `feat: add kitchen quote template` |

---

## 四、Git / GitHub 日常工作流

### 标准四步（每个项目相同）

```powershell
cd D:\DD-cursor\<项目目录>    # 1. 进入正确目录
git status                    # 2. 确认改对了仓库
git add .                     # 3. 暂存
git commit -m "说明改了什么"   # 4. 本地记录
git push origin main          # 5. 上传（分支名按项目：main 或 master）
```

### 改之前必问三句话

1. **我在哪个目录？**（`pwd` / 看终端路径）
2. **这是哪个 Git 仓库？**（`git remote -v`）
3. **改的是不是这个项目的文件？**

### 分支策略（现阶段简化版）

| 场景 | 做法 |
|------|------|
| 日常改静态页 | 直接在 `main`/`master` 改，push |
| 大改/试验 | 开 `dev` 或 `feat/xxx` 分支，合并后再 push main |
| GitHub Pages | 生产环境跟 `main`（或 `master`）走 |

> 团队扩大后再引入 PR Review；现阶段你是单人，保持简单即可。

---

## 五、OpenClaw 与 Cursor 分工

| 工具 | 适合 | 不适合 |
|------|------|--------|
| **OpenClaw** | 快速生成模板、文档草稿、一次性页面 | 长期维护、Git 版本管理 |
| **Cursor** | 日常开发、重构、多文件联动、push 部署 | 替代 GitHub 做版本存储 |
| **GitHub** | 备份、历史、线上部署、客户分享链接 | 在网页里改大段 HTML |

**迁移规则：** OpenClaw 产出 → 复制到对应项目目录 → 按规范 commit → push → **以 GitHub 为准**。

---

## 六、新项目上线 Checklist

```
[ ] 1. 确定层级：Core 还是 Matrix？
[ ] 2. GitHub 新建仓库（与文件夹同名）
[ ] 3. 本地 mkdir + git init（或 clone）
[ ] 4. 添加 index.html + README.md
[ ] 5. git remote add origin ...
[ ] 6. git push -u origin main
[ ] 7. Settings → Pages → main / root
[ ] 8. 根 .gitignore 加入该目录（若在 DD-cursor 下）
[ ] 9. 更新 _workspace/PROJECTS.yaml
[ ] 10. 更新 WORKSPACE.md 快速索引
```

---

## 七、共享资源（_shared）

各项目可有自己的 `_shared/`（CSS、组件）。**不要**做一个「全局 _shared 仓库」除非团队 ≥3 人。

复制策略：从 `thor-quote\_shared\` 复制到新项目，按需改，不强制同步。

---

## 八、当前待办（技术债清理）

| 优先级 | 事项 | 说明 |
|--------|------|------|
| P0 | 营销站切回 `master` 并清理 `gh-pages-fix` | 根仓库分支混乱 |
| P0 | push `scheme-center`（ahead 1 + catalog 未跟踪） | 线上缺最新数据 |
| P0 | push `thor-quote`（ahead 1 + 大量变更） | 确认删除是否 intentional |
| P1 | 建 `dd-workspace` 仓库，push `_workspace/` | 文档有远程备份 |
| P1 | `supplier-selector` / `outdoor-solutions` 建 remote 或移入 `_archive` | 避免无 remote 孤儿仓 |
| P2 | 统一旧仓库 default branch 为 `main` | thor-quote、dd-deep-design 仍是 master |
| P2 | 删除 `D:\CAB-sites` 重复备份 | 确认 DD-cursor 已 push 后 |

---

## 九、文件清单（本工作区元数据）

```
D:\DD-cursor\_workspace\
├── PORTFOLIO.md      ← 本文件（治理规范）
├── PROJECTS.yaml     ← 项目台账（机器可读）
├── WORKFLOW.md       ← 新手 Git 速查
└── README.md         ← 入口说明
```

此目录建议单独仓库 **`dd-workspace`**，与业务站点分离。
