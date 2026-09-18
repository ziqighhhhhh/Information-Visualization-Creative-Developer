# gradient-mesh — 网格渐变背景

可复用背景：WebGL mesh-gradient 动态渐变 + 调色层（vignette / 对比 / 噪点颗粒）。单文件演示见 `index.html`（双击打开，**需联网**加载引擎）。

## 资产身份（稳定能力）

**氛围渐变背景**——"Build atmosphere before content"。主题配色（ember / aurora / ocean / mono）和 seed 都是 CONFIG 里的表现层参数，不是新资产。

## 分层说明

| 层 | 内容 | 实现 |
| --- | --- | --- |
| 渲染本体 | WebGL mesh 渐变、动画循环、换色/换 seed | 上游引擎 mesh-gradient.js@0.0.5（esm.sh），**不重写 shader** |
| 表现层（可变，`CONFIG.themes`） | 四色主题、初始主题、seed | 当前 ember 默认 |
| 调色层（可变，CSS） | vignette + 明暗 grade + SVG 噪点颗粒（0.28s steps 抖动） | `.grade` / `.grain` |
| 胶水层 | `GradientMeshBackground` 类：init / setTheme / regenerate / getColors + `window.gradientMesh` 全局 API | 本资产自写 |

## 接口

```js
const background = new GradientMeshBackground({
  canvas, themes, theme: "ember", seed: 720
});
await background.init();
background.setTheme("aurora");
background.regenerate();            // 或传指定 seed
background.getColors();
// 页面内嵌时也可用 window.gradientMesh.{setTheme, regenerate, getColors}
```

主题即四色数组（亮 → 暗排列），加主题只往 `CONFIG.themes` 添一项。

## 依赖

mesh-gradient.js@0.0.5（esm.sh，ES module 引入）

## 实现要点

- **引擎不动、只包胶水**：上游渲染器保持完整，移植时只复制 wrapper 类 + CONFIG + `.grade`/`.grain` 两层 CSS
- **噪点颗粒**：内联 SVG `feTurbulence` data-URI + `steps(2)` 关键帧抖动，零图片请求
- **seed 可复现**：喜欢的构图记下 seed（status 栏会显示），`regenerate(seed)` 可精确还原

## 来源

自研资产（原 `gradient-mesh.html`），2026-09 归档入 `02-background/`。
