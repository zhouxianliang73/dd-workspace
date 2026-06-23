# DD Deep Design · 统一后台数据（配置层）

> 不是独立数据库，而是 **选品中心仓库里的 JSON 配置文件** — 全业务线共享的「后台设置」。

## 原则

| 层 | 放什么 | 仓库 |
|----|--------|------|
| **门面** | 品类叙事、案例、留资、链到协作 | 各独立站（`outdoor-kitchen`、`outdoor-living`…） |
| **协作** | 选品、项目、沟通、清单 UI | `scheme-center` / `dd-design` |
| **配置（后台）** | 产品库、渠道、报价结构 | **同在 `scheme-center`**（现阶段） |
| **算价** | 系数与定价引擎 | `thor-quote` |
| **交付** | 对外交付 HTML 模板 | `delivery-system` |

独立站 **不复制** 产品 JSON；只链到选品中心并带上 `channel`。

## 三个核心文件（统一维护入口）

路径：`D:\DD-cursor\scheme-center\`

| 文件 | 作用 | 谁改 |
|------|------|------|
| **`catalog.json`** | 全量 SKU（家具、厨柜 k-*、户外…） | 产品/运营补数据 |
| **`channels.json`** | 独立站 / 销售入口 → 可见 SKU、文案、默认页、报价模板 id | 产品 + 开发 |
| **`quote-templates.json`** | 清单分组（厨柜 8 类、户外整体、活动快单…） | 产品 + 开发 |

### 新增独立站时

1. 在 `channels.json` 增加一个 channel（如 `outdoor-kitchen` 已存在）  
2. 在 `catalog.json` 补 SKU 或 `quoteSections`  
3. 如需新清单结构，在 `quote-templates.json` 加模板  
4. 独立站 `index.html` 按钮链到：  
   `https://zhouxianliang73.github.io/dd-design/1.html?channel=<id>`  
5. 更新 `SALES-LINKS.md` 与 `PROJECTS.yaml`

## 数据流

```
catalog.json（全量）
      │
      ▼ filter by channels.json[channel]
选品中心 1.html 展示子集
      │
      ├── quote-templates.json → 清单结构
      ├── thor-quote → 算价（授权）
      └── delivery-system → 交付文档
```

## 远期（不必现在做）

- 配置单独仓库 `dd-catalog` 或 CMS  
- 选品中心 `fetch` 远程 JSON  
- 客户 tier / 缴费门禁接账号系统  

现阶段：**改 JSON → push `dd-design` → 全渠道生效**（所有带 channel 的链接同步更新）。

## 相关文档

- 战略：[`PRODUCT-STRATEGY.md`](./PRODUCT-STRATEGY.md)  
- 销售链接：[`../scheme-center/SALES-LINKS.md`](../scheme-center/SALES-LINKS.md)
