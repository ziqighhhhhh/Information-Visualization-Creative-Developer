# flow-map — 流向地图

可复用地图资产：世界地图底图 + 带**方向性流动动画**的航线网络。单文件演示见 `index.html`（双击打开，**需联网**加载 d3、topojson 与 world-atlas 数据）。

## 资产身份（稳定能力）

**flow-map**：在地图上表达"有方向、有流量"的流动关系。当前 Demo 的内容是全球贸易流（hub + routes），那是数据；橙色流光、暗底是表现层；暂停/聚焦是行为层——都可换。

## 分层说明

| 层 | 内容 | 当前 Demo 取值 |
| --- | --- | --- |
| 地图本体 | NaturalEarth1 投影 + Sphere/经纬网/国家底图 + zoom(1~5x) | 与 `../world-map/`、`../choropleth/` 同一底图配方 |
| 数据层（可变，`CONFIG`） | hub + routes，每条航线带 `volume`（流量）和 `speed` | 广州 hub + 6 条航线 |
| 表现层（可变，CSS 变量 / gradient） | 航线配色、glow、节点样式 | 橙→金渐变流光 |
| 行为层（可选） | dash 流动、粒子包、hover tooltip、点击聚焦、Pause/Replay/Reset | 全部开启 |

## 接口（`CONFIG`）

```js
{
  atlasUrl,
  hub: {id,name,region,lon,lat},
  routes: [{id,name,region,lon,lat, volume, speed}, ...]
  //                                  ↑描边宽度/粒子数  ↑流动速度
}
```

## 依赖

d3@7 · topojson-client@3 · world-atlas@2（CDN 数据）

## 实现要点（区别于 world-map / choropleth 的配方）

- **双层流动表达**：
  - SVG 层：`route-flow` 用 `stroke-dasharray:8 12` + `dashoffset` CSS 循环动画（`1.45/speed`s，按航线速度分频）
  - Canvas 层：粒子包沿路径运动——**D3 管几何，`getPointAtLength()` 取样，canvas 只画运动的光点**（粒子数 = volume/24，透明度按 `sin(π·t)` 两端淡入淡出）
- **数据驱动视觉**：`volume` 同时映射 glow 宽度、主线宽度、粒子数量与大小
- **入场衔接**：dash 描绘动画结束后，`route-flow` 的 `stroke-dasharray` 切换为 `8 12` 流动模式（在 `transition.on("end")` 里换），base 线则清除 dash
- 底图/节点/tooltip/聚焦/防抖与 `../world-map/` 同配方；粒子层用独立 canvas（z-index 在 SVG 之上、装饰层之下），DPR 上限 2

## 相关资产

- `../world-map/`：静态点线网络版（同 hub+routes 数据形状）
- `../choropleth/`：同底图的分级设色版
- 三个资产底图代码同源——**已出现 3 次，达到拆分阈值**。可考虑抽公共 basemap 模块（投影 fit、Sphere/graticule/country 绘制、zoom、loading、resize 防抖），抽完记得在三边 README 更新来源说明。

## 来源

自研资产（原 `world-map-animated-routes.html`），2026-09 归档入 `03-map/`。
