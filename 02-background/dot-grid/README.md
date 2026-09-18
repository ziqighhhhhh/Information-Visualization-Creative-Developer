# dot-grid — 点阵背景

可复用背景：动态点阵（Vanta DOTS）+ 静态线网格 + 噪点 + vignette 的复合层。单文件演示见 `index.html`（双击打开，**需联网**加载 Three.js 与 Vanta）。

## 资产身份（稳定能力）

**点阵氛围背景**——"Structure with a little noise"：动态点阵提供结构，噪点和线网格提供质感。预设（precision / network / warm / minimal）、网格/噪点/交互开关都是参数，不是新资产。

## 分层说明

| 层 | 内容 | 实现 |
| --- | --- | --- |
| 渲染本体 | 动态点阵（可连线、鼠标视差） | 上游 Vanta DOTS（基于 Three.js r134），不重写 |
| 表现层（可变，`PRESETS`） | 点色/双色、间距、尺寸、是否连线 | precision 默认 |
| 叠加层（可变，CSS） | 64px 静态线网格（径向 mask 边缘渐隐）+ SVG 噪点 + vignette | `.line-grid` / `.noise` / `.grade` |
| 胶水层 | `NoiseGridBackground` 类 + `window.noiseGrid` | 本资产自写 |

## 接口

```js
const bg = new NoiseGridBackground({el:"#vanta-grid", preset:"precision", interaction:true});
bg.init();
bg.setPreset("network");      // Vanta setOptions 热更新
bg.setInteraction(false);     // 注意：内部是 destroy + rebuild
bg.resize(); bg.destroy();
```

## 预设配方

| 预设 | 点色 | 间距 | 连线 | 气质 |
| --- | --- | --- | --- | --- |
| precision | 蓝 + 橙点缀 | 27 | 否 | 精密、仪表盘 |
| network | 亮蓝 + 橙 | 31 | 是 | 网络连接 |
| warm | 橙 + 金 | 30 | 是 | 暖色品牌 |
| minimal | 灰蓝 | 34 | 否 | 极简克制 |

## 依赖

three.js r134（cdnjs）+ vanta.dots（jsdelivr）——Vanta 依赖全局 `THREE`，注意加载顺序。

## 实现要点

- **复合层思想**：动态层（Vanta）与静态层（线网格/噪点/vignette）分离——静态层纯 CSS 零开销，可独立开关
- **setOptions vs rebuild**：换预设用 `effect.setOptions()` 热更新；但交互开关（mouseControls）只在初始化时读取，必须 `destroy() → init()` 重建
- 线网格用 `mask-image` 径向渐隐，中心实、边缘虚
- `beforeunload` 里 `destroy()` 释放 WebGL 上下文

## 相关资产

- `../gradient-mesh/`：渐变氛围背景
- `../particle-field/`：粒子场背景（更"空"，本资产更"结构"）
- `../glow-field/`：辉光氛围背景（同属 Vanta 胶水模式）

## 来源

自研资产（原 `preview.html`，Noise Grid），2026-09 归档入 `02-background/`。
