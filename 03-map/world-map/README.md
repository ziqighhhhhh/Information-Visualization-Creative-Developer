# world-map — 世界地图

可复用地图资产：世界地图底图 + 节点/航线网络。单文件演示见 `index.html`（双击打开，**需联网**加载 d3、topojson 与 world-atlas 数据）。

## 资产身份（稳定能力）

**世界地图及其上的点-线网络表达**：国家底图、投影、经纬网格、节点（含脉冲）、大圆航线、缩放平移。当前 Demo 的内容是"全球网络（hub + markets）"，那是数据，不是身份；暗色橙光配色是表现层，可换。

## 分层说明

| 层 | 内容 | 当前 Demo 取值 |
| --- | --- | --- |
| 地图本体 | NaturalEarth1 投影 + Sphere/经纬网/国家底图 + zoom(1~5x) | — |
| 数据层（可变，`CONFIG`） | hub + markets 节点、大圆航线 | 广州 hub + 6 个市场 |
| 表现层（可变，CSS 变量） | 底图配色、航线/节点颜色、glow | 暗蓝底 + 橙航线 |
| 行为层（可选） | 国家 hover、节点 tooltip、点击节点聚焦缩放、入场动画、Replay/Reset | 全部开启 |

## 接口（`CONFIG`）

```js
{
  atlasUrl,            // TopoJSON 数据源（默认 world-atlas countries-110m）
  projection,          // 投影名（当前 NaturalEarth1）
  hub: {id,name,region,lon,lat},
  markets: [{id,name,region,lon,lat}, ...]
}
```

改数据只动 `CONFIG`；换主题只动 `:root` CSS 变量（`--bg --country --route --node` 等）。

## 依赖

| 库 | 版本 | 用途 |
| --- | --- | --- |
| d3 | 7 | 投影、zoom、过渡动画 |
| topojson-client | 3 | TopoJSON → GeoJSON |
| world-atlas | 2（CDN 数据） | countries-110m 底图 |

## 实现要点（值得记住的配方）

- **航线**：`d3.geoInterpolate` 生成大圆路径，三层描边叠加——模糊 glow（`feGaussianBlur`）+ 主线 + 亮色热线
- **节点**：双层脉冲环（`@keyframes pulse`，错相位 1.3s）+ hub 强化样式；label 用 `paint-order:stroke` 描边防压图
- **入场动画**：航线 `stroke-dashoffset` 描绘（180ms + i×55ms stagger，1350ms，easeCubicOut）→ 节点 `easeBackOut.overshoot(1.4)` 弹入（620ms + i×80ms）
- **交互**：节点点击聚焦（zoom.transform 平移缩放至该点，scale 2.6，900ms easeCubicInOut）；tooltip 跟随鼠标
- **工程细节**：`vector-effect:non-scaling-stroke` 防缩放变粗；resize 120ms 防抖重渲；loading 遮罩

## 潜在拆分方向（复用 2 次以上再拆）

- 航线三层描边 + dash 描绘入场 → `06-animation/`
- 节点 tooltip → `05-components/tooltip/`
- 径向渐变背景 + 暗角 → `02-background/`

## 来源

自研资产（原 `world-map-global-network.html`），2026-09 归档入 `03-map/`。
