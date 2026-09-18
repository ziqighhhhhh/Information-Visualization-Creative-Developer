# particle-field — 粒子场背景

可复用背景：环境粒子场（漂浮/连线/流动/尘埃四种气质）。单文件演示见 `index.html`（双击打开，**需联网**加载 tsParticles）。

## 资产身份（稳定能力）

**粒子氛围背景**——"Give empty space a pulse"。预设（ambient / constellation / stream / dust）、配色（warm / cool）、密度、交互开关都是 CONFIG 参数。

## 分层说明

| 层 | 内容 | 实现 |
| --- | --- | --- |
| 渲染本体 | 粒子渲染、运动、retina、交互、生命周期 | 上游 tsParticles v4（engine + slim bundle），不重写 |
| 表现层（可变，`CONFIG`） | 预设、双色板、密度倍率、鼠标排斥开关 | warm 默认 |
| 调色层（可变，CSS） | 径向渐变打底 + vignette grade + SVG 噪点颗粒 | `.grade` / `.grain`（与 `../gradient-mesh/` 同配方） |
| 胶水层 | `createPreset()` 配置工厂 + `ParticleField` 类 + `window.particleField` | 本资产自写 |

## 接口

```js
const field = new ParticleField({id, preset, colors, density, interaction});
await field.init();
await field.setPreset("constellation");
await field.setInteraction(false);
await field.setDensity(1.5);
```

## 预设配方（手感参数）

| 预设 | 数量 | 速度 | 特征 |
| --- | --- | --- | --- |
| ambient | 88×密度 | .38 | 无连线，慢漂浮，默认气质 |
| constellation | 74 | .48 | 连线（distance 138，opacity .13），星座感 |
| stream | 92 | 1.45 | 定向右流，数据流感 |
| dust | 150 | .22 | 极小极淡（opacity .05~.24），尘埃感 |

共性纪律：粒子尺寸 ≤2.4px、opacity ≤.62——背景必须保持"有存在感但不抢戏"。

## 依赖

@tsparticles/engine@4 + @tsparticles/slim@4（CDN；注意顺序：engine → slim → `loadSlim(tsParticles)`）

## 实现要点

- `fullScreen:false` + 透明背景，粒子层只作为 `.stage` 内的一层，调色层叠在上面
- 切换预设/密度走 `destroy() → load()` 重建，tsParticles 没有可靠的部分更新
- 鼠标交互 `detectsOn:"window"`，UI 层 `pointer-events:none` 不会挡住排斥效果

## 相关资产

- `../gradient-mesh/`：渐变氛围背景（同属"引擎 + 胶水 + 调色层"模式）
- `../dot-grid/`：点阵背景（结构感更强）
- `../glow-field/`：辉光氛围背景（Vanta FOG）

## 来源

自研资产（原 `particle-field-fixed.html`），2026-09 归档入 `02-background/`。
