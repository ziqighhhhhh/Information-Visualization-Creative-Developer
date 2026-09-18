# glow-field — 辉光氛围背景

可复用背景：shader 驱动的雾气辉光场（"let light behave like atmosphere"）。单文件演示见 `index.html`（双击打开，**需联网**加载 Three.js 与 Vanta FOG）。

## 资产身份（稳定能力）

**辉光氛围场**：光像大气一样缓慢流动、弥漫。预设（ember / aurora / ice / noir）、速度倍率、交互、噪点开关都是参数，不是新资产。

> 命名为 glow-field 而非 shader-glow："shader" 是实现手段，"辉光场"才是稳定身份。

## 分层说明

| 层 | 内容 | 实现 |
| --- | --- | --- |
| 渲染本体 | 雾状辉光 shader + 动画循环 | 上游 Vanta FOG（基于 Three.js r134），不重写 |
| 表现层（可变，`PRESETS`） | 四段色（highlight/midtone/lowlight/base）、blurFactor、zoom、speed | ember 默认 |
| 叠加层（可变，CSS） | `mix-blend-mode:screen` 中心光斑 + SVG 噪点 + vignette | `.glow-core` / `.grain` / `.grade` |
| 胶水层 | `ShaderGlowBackground` 类 + `window.shaderGlow` | 本资产自写 |

## 接口

```js
const bg = new ShaderGlowBackground({el:"#vanta-fog", preset:"ember", interaction:true});
bg.init();
bg.setPreset("ice");
bg.setSpeedMultiplier(1.65);   // 0.55 / 1 / 1.65 三档手感好
bg.setInteraction(false);      // 注意：内部 destroy + rebuild
bg.resize(); bg.destroy();
```

## 预设配方

| 预设 | 配色走向 | blur | zoom | speed | 气质 |
| --- | --- | --- | --- | --- | --- |
| ember | 橙余烬 | .72 | .78 | 1.15 | 暖、能量 |
| aurora | 青→紫极光 | .64 | .82 | .92 | 冷、流动 |
| ice | 冰蓝白 | .78 | .86 | .78 | 清透 |
| noir | 灰白 | .86 | .88 | .66 | 极简、慢 |

规律：**越克制越快模糊的预设，speed 越慢**——朦胧感和速度感成反比。

## 依赖

three.js r134（cdnjs）→ vanta.fog（jsdelivr），顺序不能反（Vanta 读全局 `THREE`）。

## 实现要点

- 与 `../dot-grid/` 同一套 Vanta 胶水模式：`setOptions()` 热更新预设/速度；交互开关是构造参数，必须 rebuild
- `_resolvedOptions()` 把预设与 speedMultiplier 合并后再下发，避免速度倍率被换预设时冲掉
- 中心光斑层用 `mix-blend-mode:screen`，只提亮不压暗
- `beforeunload` 里 `destroy()` 释放 WebGL 上下文

## 相关资产

- `../gradient-mesh/` / `../particle-field/` / `../dot-grid/`：同结构的背景三件套
- 四个背景资产同为「上游引擎 + 胶水层 + CSS 叠加层（grain/grade/vignette）」——叠加层配方已复用 4 次，**强烈建议下次抽共享片段**

## 来源

自研资产（原 `shader-glow.html`），2026-09 归档入 `02-background/`。
