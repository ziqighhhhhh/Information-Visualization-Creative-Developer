# 06-animation — 动效方案

动画与转场的配方库。这里归档"怎么动"，而不是"画什么"。

## 存放什么

- 转场方案（场景切换、页面进出）
- 入场动画（图表元素逐个出现、数字滚动、路径描绘）
- 滚动驱动动画（滚动进度 → 属性映射）
- 缓动曲线配方与手感参数（duration / easing / stagger）
- 微交互（hover、点击反馈、拖拽惯性）

## 什么值得归档

- 调好手感的参数组（README 里写清"为什么是这个数值"）
- 动效时序的编排模式（stagger 的节奏、时序重叠比例）
- 性能安全的动效写法（只动 transform / opacity 等）

不值得归档：没有任何调参思考的默认动画。

## 命名方式

`动效类型-触发方式或手感`，kebab-case，例如：

- `stagger-entrance-charts/`
- `scroll-driven-camera/`
- `hover-magnetic-button/`

## 子目录建议包含

```
06-animation/xxxx/
├── README.md      # 时序参数、手感说明、性能注意点
├── index.html     # 最小演示
└── src/           # 实现代码
```
