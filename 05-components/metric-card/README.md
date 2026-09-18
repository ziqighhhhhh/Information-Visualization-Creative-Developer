# metric-card — 指标卡

可复用指标卡组件。当前演示见 `index.html`（双击即可打开）。

## 组件身份（稳定能力）

`metric-card` 的稳定身份是：**一块突出展示单个指标的卡片**。内容可以是数字（KPI、统计值），也可以是文字（状态、结论）。这与颜色、动效无关。

## 分层说明

| 层 | 包含什么 | 例子 |
| --- | --- | --- |
| 组件本体 | 结构：标签区、主数值/文字区、描述区、图标位 | eyebrow + label + value + suffix + description |
| CSS 表现层（可变） | 颜色、背景、边框、圆角、Glow、Dark/Light | 当前 Demo 是 dark + amber glow |
| 行为层（可选） | CountUp、Fade、Hover、Stagger 等 | 当前 Demo 用了 CountUp + 入场 stagger + hover 上浮 |

表现层和行为层都是**可换、可关**的，不改变组件身份，因此不写进目录名。

## 当前 Demo 说明

`index.html` 是 dark 样式 + CountUp 数字滚动的一个具体搭配：

- 视觉：暗色玻璃拟态（`backdrop-filter` 模糊 + 半透明描边）、amber 强调色光晕、网格遮罩背景
- 行为：卡片入场（900ms outExpo）→ 高亮线展开（延迟 240ms）→ CountUp 数字滚动（1.5s），hover 上浮，支持 Replay
- 依赖：Anime.js 4.5.0 + CountUp.js 2.10.1（CDN），内置原生回退，离线可预览
- 尊重 `prefers-reduced-motion`

### 接口

内容与数值集中在 `metricConfig`，样式集中在 `:root` CSS 变量（`--bg` `--panel` `--line` `--text` `--muted` `--accent`），换文案改 config、换主题改变量即可。

## 结构约定

现阶段保持简单：`index.html` + `README.md`，**不为变体提前建目录**。

如果以后确实出现多个值得保留的不同 Demo，再建 `demos/` 子目录，命名描述"表现 + 行为"的组合，例如：

```
metric-card/
├── index.html          # 主演示（当前的 dark + countup 版本）
├── README.md
└── demos/              # 仅在确有多个值得保留的变体时创建
    ├── countup-dark.html
    └── static-light.html
```

## 潜在拆分方向（复用 2 次以上再拆）

- 网格遮罩背景 → `02-background/`
- 入场编排（卡片 blur-in + 高亮线 stagger）→ `06-animation/`
- 「CDN + 原生回退」的库加载模式

## 来源

自研演示，2026-09 归档入 `05-components/`。
