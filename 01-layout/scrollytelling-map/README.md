# scrollytelling-map — 滚动叙事 · 地图

可复用布局：sticky D3 地图 + 滚动步骤，步骤驱动地图"运镜"（投影参数/中心/缩放过渡）。单文件演示见 `index.html`（**需联网**加载依赖）。

## 身份

scrollytelling 框架的**地图媒介**实例：滚动即运镜——01 Global View 起，逐站飞抵。

## 共享骨架

同 `../scrollytelling-network/`：sticky 视觉 + `.step[data-step]` + ScrollTrigger。

## 本资产特有

- 媒介引擎：**D3 Geo + TopoJSON**（与 `../../03-map/` 三件套同栈）
- 步骤 = 相机状态：每步对应一组投影/中心/缩放，步骤切换时 D3 transition 平滑过渡
- 复用价值：把 `03-map` 的静态地图配方升级为叙事运镜

## 依赖

d3@7 · topojson-client@3 · gsap@3.13 + ScrollTrigger（CDN）

## 相关资产

- 同系列：`../scrollytelling-network/` · `../scrollytelling-chart/` · `../scrollytelling-comparison/` · `../scrollytelling-pinned/`
- 地图底图配方：`../../03-map/world-map/`

## 来源

自研资产（原 `scroll-story-scrollytelling-map.html`），2026-09 归档入 `01-layout/`。
