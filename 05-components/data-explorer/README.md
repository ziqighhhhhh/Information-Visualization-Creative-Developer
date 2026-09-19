# data-explorer — 联动数据探索器

可复用组件：图表 + 数据表格 + 指标卡的**联动视图**——筛选、图表点击、表格行点击全部写入同一份状态，三视图同步刷新。单文件演示见 `index.html`（**需联网**加载依赖）。

## 组件身份（稳定能力）

**linked views**：多视图共享一份 filter state。"engine-standalone-v2" 这类版本/形态信息不进目录名；ECharts、Tabulator 是当前实现选型，可换。

## 分层说明

| 层 | 内容 | 实现 |
| --- | --- | --- |
| 状态核心 | `state`（year 等筛选维度）+ `filterRows()` 单一数据入口 | 自写，**所有交互只改 state，渲染统一走 filterRows** |
| 视图层（可换） | 趋势图、排名图、指标卡、数据网格 | ECharts 6.1.0 × 2 + Tabulator 6.5.3 |
| 聚合层 | `aggregateMonths()` / `aggregateMarkets()` | 自写纯函数 |
| 演示数据 | `pseudo(seed)` 伪随机数据生成器 | 换真实数据时替换 |

## 联动纪律（本资产的核心价值）

- **单一数据源**：任何交互（筛选器、bar 点击、行点击）→ 写 state → `filterRows()` → 重新聚合 → 三视图重渲
- bar 点击 = 反向筛选（点排名图的某个 market 即过滤到该 market）
- 表格列头自带 `headerFilter` 输入筛选，排序/调宽由 Tabulator 负责
- formatter 集中管理（money / margin / share / market），视图间数字格式一致

## 接口

ECharts：`trendOption(data)` / `rankingOption(data)` 返回配置；Tabulator：`initTable()`。换数据只需替换 DATA 生成部分与聚合维度。

## 依赖

echarts@6.1.0（jsdelivr）· tabulator-tables@6.5.3（unpkg）

## 变体（`demos/`）

- `demos/linked-views.html`：同栈同能力的另一视图组合——time range + ranking + market matrix + grid，并演示图表与表格行之间的 `linked-hover` 互相高亮。主演示（`index.html`）是 trend + ranking + 指标卡 + grid 的组合。

命名惯例：demo 文件名描述"视图组合特征"，能力仍归 `data-explorer`。

## 来源

自研资产（原 `data-explorer-engine-standalone-v2.html`），2026-09 归档入 `05-components/`。
