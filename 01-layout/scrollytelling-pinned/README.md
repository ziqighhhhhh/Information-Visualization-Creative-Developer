# scrollytelling-pinned — 滚动叙事 · 钉住产品

可复用布局：产品视觉被 ScrollTrigger **pin** 在视口中，滚动驱动其连续变换（旋转/位移/缩放），步骤文案从旁经过。单文件演示见 `index.html`（**需联网**加载 GSAP）。

## 身份

scrollytelling 框架的**pin 媒介**实例。与 sticky 系不同：这里由 ScrollTrigger 直接接管 pin 与 scrub，变换是连续插值而非离散步骤切换。

## 共享骨架

同系列，但注意差异：`ScrollTrigger.create({pin:true, scrub:...})` 代替 CSS sticky；大量 `gsap.to` 挂 scrollTrigger 做 scrub 动画。

## 本资产特有

- **`ScrollTrigger.matchMedia`**：移动端降级布局（小屏取消 pin 或简化变换）——桌面/移动两套叙事节奏写在一处
- 纯 GSAP，无第三方视觉引擎：产品视觉是 DOM/CSS 合成

## 依赖

gsap@3.13 + ScrollTrigger（CDN）

## 相关资产

`../scrollytelling-network/` · `../scrollytelling-chart/` · `../scrollytelling-map/` · `../scrollytelling-comparison/`

## 来源

自研资产（原 `scroll-story-pinned-product-story.html`），2026-09 归档入 `01-layout/`。
