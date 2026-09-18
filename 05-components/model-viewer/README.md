# model-viewer — 3D 模型展台

可复用组件：GLB/glTF 模型的产品级展示台（相机预设、自动旋转、曝光、上传替换）。单文件演示见 `index.html`（双击打开，**需联网**加载 `<model-viewer>` 与演示模型）。

## 组件身份（稳定能力）

**3D 产品展台**：所有行为都委托给 Google `<model-viewer>` 的公开 API，本资产只有"预设 + 舞台美术 + 胶水"。四个机位预设（studio / hero / detail / static）、转速、曝光都是参数。

## 分层说明

| 层 | 内容 | 实现 |
| --- | --- | --- |
| 渲染本体 | GLB 渲染、相机控制、环境光、阴影 | 上游 `<model-viewer>`@4.3.1，不重写 |
| 表现层（可变） | 机位预设、曝光、转速、ambient 光晕、展示卡片 | `PRESETS` + CSS |
| 行为层（可选） | 自动旋转、拖拽/缩放、上传 GLB、相机复位 | 全部开启 |

## 机位预设（手感参数）

| 预设 | cameraOrbit | fov | 阴影 | 自转 | 用途 |
| --- | --- | --- | --- | --- | --- |
| studio | 35° 72° | 30° | .85/.82 | 开 | 默认棚拍感 |
| hero | 25° 68° | 25° | 1/.72 | 开 | 低角度英雄镜头 |
| detail | 42° 76° 80% | 20° | .72/.90 | 关 | 近景细节（长焦压缩） |
| static | 0° 75° | 30° | .82/.86 | 关 | 正面证件照 |

## 接口

```js
window.productModelViewer = {
  element, setPreset(name), setModel(src), setExposure(v), setAutoRotate(bool)
};
```

## 依赖

model-viewer@4.3.1（Google CDN，ES module）；演示模型为 modelviewer.dev 的 Chair.glb

## 实现要点

- **GLB 优先**：上传只收 `.glb`——单文件自包含；`.gltf` 常引用外部纹理/缓冲，容易缺资源
- 上传用 `URL.createObjectURL`，切换前 `revokeObjectURL` 旧地址防泄漏
- 相机复位后调 `jumpCameraToGoal()` 立即跳到目标位（否则等插值）
- 自定义进度条走 CSS 变量（`--progress-bar-color`），`::part(default-progress-bar)` 修圆角
- 舞台美术三件套：`.ambient` 光晕 + `.viewer-card` 玻璃底板 + 页面 vignette——与模型本体解耦

## 来源

自研资产（原 `product-stage-model-viewer.html`），2026-09 归档入 `05-components/`。
