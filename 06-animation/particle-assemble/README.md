# particle-assemble — 粒子聚合成形

可复用动效：上千粒子从散场聚合为 logo/图形轮廓（也可反向散开）。单文件演示见 `index.html`（双击打开，**需联网**加载 Three.js、SVGLoader 与 Anime.js）。

## 动效身份（稳定能力）

**particle-assemble**：粒子群 → 目标形状的聚合/散开。粒子数、形状、运动方式（swirl 等）、配色都是 `CONFIG` 参数。

## 接口（`CONFIG`）

```js
{
  particleCount: 1500,
  shape: "mark",        // 目标形状（SVG 路径采样）
  motion: "swirl",      // 聚合运动方式
  colors: [0xff7a16, 0xffa23f, 0xffcc7d, 0xfff2df],
  pointSize: 10
}
```

核心函数：`assemble()` / `scatter()` / `setShape()`。

## 实现管线（值得记住的流程）

1. `parseSubPaths(svgText)`：解析 SVG 子路径
2. `buildTargetPositions()`：沿路径**采样**出粒子的目标坐标
3. `buildScatterPositions()` / `buildCurveOffsets()`：生成散点位与曲线偏移
4. `buildColors()` / `makeParticleTexture()`：配色 + 圆形粒子贴图（**用贴图保持 `THREE.PointsMaterial`，不写自定义 shader**）
5. `updateParticlePositions()` + Anime.js 驱动聚合/散开插值，`render()` 循环渲染

## 依赖

three.js r134（cdnjs）+ three SVGLoader（jsdelivr）+ animejs@3.2.2

## 性能注意

- `renderer.setPixelRatio(min(devicePixelRatio, 2))` 限制 DPR
- 粒子数 1500 是手感与性能的平衡点；移动端建议降到 ~800

## 相关资产

- `../slide-merge/` / `../stroke-draw/` / `../clip-reveal/`：logo 揭示系列的其他机制

## 来源

自研资产（原 `logo-reveal-particle-assemble.html`），2026-09 归档入 `06-animation/`。
