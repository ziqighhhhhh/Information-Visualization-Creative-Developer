# inbox — 待确认收集区

从 CodePen 自动收集的候选资产流程区。已完成两个批次：

| 批次 | 收集 | 保留 | 删除 | 状态 |
| --- | --- | --- | --- | --- |
| batch 1 | 101 | 44 (+1 unseen) | 56 | 已分类归档 |
| batch 2 | 110 | 40 | 70 | 已分类归档（应用了 batch 1 口味预筛） |

- 保留资产已按能力型命名规则分类入 `01-layout/`、`04-effects/`、`05-components/`、`06-animation/` 等
- 每个资产 README 记录原作、作者、许可与原链接
- 口味标准沉淀在 `references/collection-criteria.md`

## 本目录保留的流程文件

- `review.html` / `review-2.html`：各批次审查工具
- `manifest.json` / `manifest-2.json`：各批次收集元数据
- `decisions.json` / `decisions-2.json`：各批次人工决策记录

## 下一批次流程

1. 收集（CodePen popular 作者页，注意 429 限流——降速 ≥2.5s/件、oEmbed 单独慢速跑）
2. 生成 review-N.html（嵌入新 manifest，localStorage key 按批次区分）
3. 人工审查导出 decisions-N.json
4. 按决策删除/分类（历史批次决策可用来预筛回锅 pen）
