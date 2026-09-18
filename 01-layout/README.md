# 01-layout — 布局骨架

页面级、结构性的布局方案。只收"决定了整页怎么组织"的东西。

## 存放什么

- 全屏画布布局（canvas + overlay UI 的分层结构）
- 固定/混合分栏布局（侧边栏 + 主视图、多面板仪表盘）
- 滚动叙事（scrollytelling）的章节框架
- 响应式 / 自适应断点方案
- 页面初始加载的骨架结构（loader → reveal）

## 什么值得归档

- 在 2 个以上完整页面里实际用过的布局结构
- 解决过具体痛点的布局（如"图表区如何与悬浮控制面板共存"）
- 整套布局里可复用的 CSS 模式（定位、层级、safe-area）

不值得归档：一次性的页面微调、只属于某个 demo 的硬编码尺寸。

## 命名方式

`布局特征-来源或场景`，kebab-case，例如：

- `fullscreen-canvas-overlay/`
- `scrollytelling-chapters/`
- `dashboard-sidebar-grid/`

## 子目录建议包含

```
01-layout/xxxx/
├── README.md      # 这个布局解决什么问题、关键实现思路、使用注意点
├── index.html     # 可独立打开的最小演示（能跑就行）
├── style.css      # 布局核心样式
└── screenshots/   # 可选：效果截图，方便日后快速回忆
```
