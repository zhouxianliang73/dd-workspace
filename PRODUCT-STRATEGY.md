# DD Deep Design · 产品战略（共识文档）

> 版本 1.1 · 与业务方口头对齐  
> 品牌核心：**DD Deep Design**  
> 协作产品：**选品中心**（`scheme-center` / `dd-design` / `1.html`）

---

## 1. 我们是谁

| 层级 | 内容 |
|------|------|
| **品牌** | DD Deep Design |
| **核心价值** | 设计 → 深化设计（服务价值优先） |
| **商业结果** | 价差/贸易利润可放大，但不是对外核心叙事 |
| **协作工具** | 选品中心：B 端项目前期设计协助 + 跟踪（销售发链接进入） |

---

## 2. 业务矩阵

### 获客：品类独立站（各自独立域名）

远期七个单品类域名；**Phase 1** 重点：

| 独立域名站 | 英文/定位 | channel 参数 | 与户外线关系 |
|------------|-----------|--------------|--------------|
| **户外阳台整体服务** | Outdoor Living | `outdoor-living` | 母叙事：别墅户外阳台一站式 |
| **户外厨房** | Outdoor Kitchen | `outdoor-kitchen` | 户外线子入口，**独立域名** |
| **法式家具（俄罗斯）** | French · Russia | `french-ru` | 独立站 |
| **俄罗斯活动家具** | Event · Russia | `event-ru` | 独立站 |
| **定制获客** | Custom Design | `custom` | 销售直链，设计服务优先 |

**户外说明：**

- 「阳台」= **别墅户外露台/庭院**（凉亭、烧烤、厨房），非公寓阳台。
- 前期户外厨房站与户外配套栏目可合并内容，但 **Outdoor Living 与 Outdoor Kitchen 两个独立域名** 均需保留。
- 户外整体叙事：**避免客户单品分散购买导致运费叠加，用整体设计扩大场景销售。**

### 协作：选品中心（一个产品、一个仓库）

- URL：`https://zhouxianliang73.github.io/dd-design/1.html`
- 进入方式：**销售发链接**（`?channel=…&invite=…`）
- 呈现规则：channel 决定可见 catalog 子集 + 默认报价模板 + 首页文案
- 后台 catalog 全量维护，前台按 channel 过滤

### 工具链

| 工具 | 角色 |
|------|------|
| 选品中心 | B 端协作主界面 |
| thor-quote | 算价（授权可见） |
| delivery-system | 对外交付文档 |
| supplier-selector | 项目内配套选型 |

---

## 3. 客户旅程

```
独立站（域名）触达 / 定制销售直链
        ↓ 销售发链接
选品中心（DD Deep Design · channel 上下文）
        ↓ 设计 / 沟通 / 清单
深化 → 算价 → 交付文档
        ↓
定制项目可衍生单品采购行项
```

---

## 4. 数据架构

```
catalog.json           全量 SKU
quote-templates.json   清单结构（kitchen / outdoor-scene / event / default）
channels.json          独立站 → 过滤规则 + 文案 + 默认模板
```

销售链接模板见：`scheme-center/SALES-LINKS.md`

---

## 5. Phase 1 交付清单

- [x] 战略文档（本文件）
- [x] `channels.json` + `1.html` channel 过滤与品牌
- [ ] Outdoor Living 独立站仓库 + 域名
- [ ] Outdoor Kitchen 独立站仓库 + 域名（可演进自 dd-deep-design）
- [ ] 法式(俄)、俄活动 独立站
- [ ] 选品中心：场景包清单、运费对比视图（v2）

---

## 6. 仓库映射（规划）

| 规划站点 | 建议 GitHub | 本地（规划） |
|----------|-------------|--------------|
| 营销/户外厨房 | dd-deep-design → 或新 `outdoor-kitchen` | `D:\DD-cursor\` 或新目录 |
| Outdoor Living | `outdoor-living`（新建） | `matrix/outdoor-living` |
| 选品中心 | dd-design | `scheme-center` |
| 俄活动 | `event-ru`（新建） | 待定 |
| 法式俄 | `french-ru`（新建） | 待定 |

更新台账：`_workspace/PROJECTS.yaml`
