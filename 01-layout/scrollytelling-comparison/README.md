# scrollytelling-comparison — 滚动叙事 · 对比滑块

可复用布局：sticky 图像对比滑块 + 滚动步骤，滚动进度驱动滑块开合。单文件演示见 `index.html`（**需联网**加载依赖）。

## 身份

scrollytelling 框架的**对比媒介**实例。sticky 媒介是 `img-comparison-slider`（before/after），滚动步骤驱动其 `value`。

## 共享骨架

同 `../scrollytelling-network/`：sticky 视觉 + `.step[data-step]` + ScrollTrigger。

## 本资产特有

- 媒介引擎：**img-comparison-slider v8**（Web Component，含独立 CSS）
- **关键纪律**：GSAP 只驱动组件的公开 `value` 属性，不碰内部 DOM——"GSAP only drives its public `value` property during scroll states"
- 典型叙事：步骤推进 → 滑块从 100%（全 before）拉到 0%（全 after），配合文案讲解差异

## 依赖

img-comparison-slider@8（CSS + JS）· gsap@3.13 + ScrollTrigger（CDN）

## 相关资产

`../scrollytelling-network/` · `../scrollytelling-chart/` · `../scrollytelling-map/` · `../scrollytelling-pinned/`

## 来源

自研资产（原 `scroll-story-comparison-story.html`），2026-09 归档入 `01-layout/`。
