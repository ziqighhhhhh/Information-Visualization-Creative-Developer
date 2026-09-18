# clip-reveal — 裁切揭示

可复用动效：用 CSS `clip-path` 把资产（logo/图片/卡片）以擦除/扩散方式揭示出来。单文件演示见 `index.html`（双击打开，**需联网**加载 Anime.js）。

## 动效身份（稳定能力）

**clip-reveal**：clip-path 是真正的揭示原语，Anime.js 只负责计时插值。四个模式（wipe / center / iris / diagonal）× 四个方向（left / right / up / down）都是预设矩阵，不是新资产。

## 与 `../line-mask/` 的区别

| | line-mask | clip-reveal（本资产） |
| --- | --- | --- |
| 裁切原语 | `overflow:hidden` 包裹元素 | **`clip-path`（inset / circle / polygon）** |
| 对象 | 文字行 | 任意资产（logo、图片、卡片） |
| 形状能力 | 矩形 | 圆角矩形、圆形 iris、多边形斜切 |

## 预设矩阵（`PRESETS`）

- **wipe**：`inset` 单边擦除（带 `round 28px` 圆角）
- **center**：`inset` 从中心向四周扩（49.85% → 0）
- **iris**：`circle(0% → 74% at 50% 50%)` 圆形扩散
- **diagonal**：`polygon` 斜角扫入

加新模式 = 加一组 from/to clip-path，引擎不动。

## 接口

```js
// class MaskReveal（名字是历史遗留，原语是 clip-path）
CONFIG = { mode:"wipe", direction:"left", duration:950 };
```

`sanitize` 技巧：`svgToDataUrl()` 把内联 SVG 转 dataURL，让上传/替换素材走统一管线。

## 依赖

animejs@3.2.2（CDN）

## 实现要点

- `will-change:clip-path` 提前声明，clip-path 动画在合成层完成
- 底层光晕（`.asset-glow`）独立于裁切层，揭示时氛围已在场

## 相关资产

- `../slide-merge/` / `../stroke-draw/` / `../particle-assemble/`：logo 揭示系列的其他机制
- `../line-mask/`：文字行的遮罩 reveal

## 来源

自研资产（原 `preview.html`，Logo Reveal — Mask Reveal），2026-09 归档入 `06-animation/`。
