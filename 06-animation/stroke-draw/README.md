# stroke-draw — 描边绘制成形

可复用动效：SVG 路径逐笔描边画出（logo/签名/徽章成形）。单文件演示见 `index.html`（双击打开，**需联网**加载 Vivus）。

## 动效身份（稳定能力）

**stroke-draw**：用 `stroke-dasharray/dashoffset` 让路径"被画出来"。内置 4 个 SVG 形（monogram / signature / symbol / badge）是演示数据，描边色、时序是表现层参数。

## 分层说明

| 层 | 内容 | 实现 |
| --- | --- | --- |
| 引擎 | dashoffset 计时、Pathformer（把 polygon/circle/line/rect 转成 path） | 上游 Vivus@0.4.6，不重写 |
| 胶水层 | `StrokeDrawReveal` 类 | 本资产自写 |
| 表现层（可变） | 描边色、线宽、drop-shadow 辉光、内置 SVG 数据 | CSS 变量 + `SHAPES` |

## 实现要点

- **非 path 元素靠 Pathformer 转换**：Vivus 自带，所以 `<polygon>/<circle>/<line>/<rect>` 也能描边
- `vector-effect:non-scaling-stroke` 保证缩放时线宽不变
- 外层 `drop-shadow` 滤镜给描边加辉光（表现层，可关）

## 依赖

vivus@0.4.6（CDN）

## 变体（demos/）

- `demos/svg-line-drawing-anime.html`：anime.js 版 SVG 描线（Julian Garnier 官方 demo，inbox 收集，第三方 MIT）——与 Vivus 引擎版对照
- `demos/garden-scroll.html`：garden - draw-on-scroll — Brad Woods（https://codepen.io/bradwoods/pen/KKEVgZG）

## 相关资产

- `../slide-merge/` / `../clip-reveal/` / `../particle-assemble/`：logo 揭示系列的其他机制（对撞 / 遮罩 / 粒子聚合）

## 来源

自研资产（原 `logo-reveal-stroke-draw.html`），2026-09 归档入 `06-animation/`。
