# light-flow — 光线流动

可复用效果：长曝光式的光线流动/光轨（长条光源沿透视方向流动，加速时视野畸变拉伸）。单文件演示见 `index.html`（双击打开，**需联网**加载上游引擎）。

## 效果身份（稳定能力）

**光线沿纵深方向的流动感**——长曝光车灯式光轨。这是归档这个资产的原因；页面壳、配色、文字都是可变的。

## 当前 Demo 的实现路径

不重写引擎，直接加载成熟上游实现 **Anemolo / Infinite-Lights**（[仓库](https://github.com/Anemolo/Infinite-Lights) · [官方演示](https://tympanus.net/Tutorials/InfiniteLights/)），只注入 `options` 配置（glue-programming 模式）。

依赖：jsDelivr GitHub CDN × 4（`three.min.js / postprocessing.min.js / InfiniteLights.js / Distortions.js`），离线不可用。

## 分层说明

| 层 | 内容 | 当前 Demo 取值 |
| --- | --- | --- |
| 效果本体 | 透视公路 + 双向流动光轨 + 加速 fov 畸变 | 由上游引擎提供 |
| 表现层（可变，`options.colors`） | 光轨配色、路面/背景色 | 橙金系（见下） |
| 行为层（可选，`options`） | 按住加速、fov 90→150、distortion 类型 | `LongRaceDistortion` |

## 控制"流动感"的关键参数

| 参数 | 作用 | 当前值 |
| --- | --- | --- |
| `movingAwaySpeed` / `movingCloserSpeed` | 双向流速（远去慢、迎面快 → 速度对比） | `[60,80]` / `[-120,-160]` |
| `carLightsLength` | 光轨长度（取路长 5~15%，决定"拖尾"感） | `[20, 60]` |
| `carLightsRadius` | 光轨粗细 | `[0.05, 0.14]` |
| `speedUp` / `fovSpeedUp` | 按住加速时的流速倍率与视野畸变 | `2` / `150` |
| `distortion` | 路面弯曲方式，可换 `mountain / LongRace / xy / turbulent / deep` | `LongRaceDistortion` |

## 配色配方（表现层，可换）

- 远去光轨：深橙阶梯 `0x7a2100 → 0xb83b00 → 0xff5a00`
- 迎面光轨：暖白核心 + 橙光晕 `0xfff2d8 → 0xffc16a → 0xff7a00`（避免全橙发平）
- 路面/背景压到近黑（`0x050505` 等），让光轨成为唯一视觉主体

## 使用注意

- 这是**配置适配**而非自有实现：要改引擎行为需 fork 上游；要在自有项目复用，需把上游 4 个 JS 落本地或换 bundler 引入
- 配色/速度等变体以后放 `demos/`（如 `blue.html`），不提前创建

## 来源

原文件 `infinite-lights-orange-baseline.html`。最初按页面归档，后明确价值在于光线流动能力，移入 `04-effects/light-flow/`。
