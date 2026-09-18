# 04-effects — 视觉效果

视觉"亮点"类资产：shader、粒子、辉光等制造视觉冲击的效果。

## 存放什么

- WebGL / shader 效果（glsl 片段）
- 粒子系统（跟随、爆炸、流动）
- 辉光、模糊、扭曲、色差等后处理
- 文字 / 图形特效（霓虹、描边、像素化、故障 glitch）
- 生成式图形（程序生成的装饰图案）

## 什么值得归档

- 完整的、可参数化复用的效果（README 里写清关键参数）
- 性能上有验证的实现（明确帧率与开销）
- 效果的组合配方（"辉光 + 噪点"怎么做）

不值得归档：从别处复制过来、自己没跑通理解过的代码。

## 命名方式

目录名只写稳定能力（效果类型），颜色、强度、速度等可变参数写进代码和资产 README，不写进目录名。

`效果类型`，kebab-case，例如：

- `glow-bloom/`
- `energy-ring/`
- `particles-mouse-follow/`
- `shader-liquid-distortion/`

反例：`orange-energy-ring-fast`（orange、fast 都是可变参数）。

## 子目录建议包含

```
04-effects/xxxx/
├── README.md      # 参数说明、性能注意点、适合的视觉场景
├── index.html     # 最小演示
└── src/           # 实现代码（js / glsl / css）
```
