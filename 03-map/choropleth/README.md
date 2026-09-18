# choropleth — 分级设色地图

可复用地图资产：世界地图底图 + 按类别给国家填色高亮。单文件演示见 `index.html`（双击打开，**需联网**加载 d3、topojson 与 world-atlas 数据）。

## 资产身份（稳定能力）

**choropleth**：用国家面填色表达类别/等级。当前 Demo 的内容是"市场分级（Core / Active / Potential）"，那是数据；暗色配色是表现层；点击聚焦是行为层——都可换。

## 分层说明

| 层 | 内容 | 当前 Demo 取值 |
| --- | --- | --- |
| 地图本体 | NaturalEarth1 投影 + Sphere/经纬网/国家底图 + zoom(1~5x) | 与 `../world-map/` 同一套底图配方 |
| 数据层（可变，`CONFIG`） | 国家分组：`core / active / potential`，用 **ISO 数字码** 匹配（抗命名差异） | 3+3+3 个国家 |
| 表现层（可变，CSS 变量） | 各类别填色、glow、底图配色 | 橙=core、金=active、蓝=potential |
| 行为层（可选） | 国家 hover tooltip（含类别状态）、点击聚焦并压暗他国、入场级联动画、Replay/Reset | 全部开启 |

## 接口（`CONFIG`）

```js
{
  atlasUrl,                          // TopoJSON 数据源
  core:      [{id:76,  name, note}], // ISO 数字码：Brazil 076, Saudi 682,
  active:    [{id:704, name, note}], // Vietnam 704, Singapore 702, UAE 784…
  potential: [{id:484, name, note}]  // Mexico 484, Kenya 404, Egypt 818…
}
```

增删类别：加一组数据 + 一条 CSS 类（`.country.xxx`）+ 图例 swatch 即可。

## 依赖

d3@7 · topojson-client@3 · world-atlas@2（CDN 数据）

## 实现要点（区别于 world-map 的配方）

- **类别匹配**：`feature.id`（ISO 数字码）→ `Map` 查表，比按国名匹配稳健
- **聚焦交互**：点击国家 → `geoPath.bounds` 计算包围盒 → 自适应缩放（上限 4.5）居中该国，同时其余国家 `opacity:.42` 压暗、该国加 `selectedGlow`
- **防杂乱策略**：只有 core 市场画常驻 label + 双层脉冲点（`geoPath.centroid` 定位），active/potential 只靠填色 + tooltip
- **入场级联**：国家淡入（i×3ms，上限 420ms）→ 脉冲点 backOut 弹入（470ms + i×100ms）→ 标签上浮（530ms + i×90ms）
- tooltip 带类别状态色点，未高亮国家也有兜底文案

## 相关资产

- `../world-map/`：同一底图配方的点线网络表达（节点+航线）
- `../flow-map/`：同一底图配方的流向动画表达（dash 流动 + 粒子包）
- 三个资产底图代码同源——**已出现 3 次，达到拆分阈值**，可考虑抽公共 basemap 模块。

## 来源

自研资产（原 `world-map-highlighted-markets.html`），2026-09 归档入 `03-map/`。
