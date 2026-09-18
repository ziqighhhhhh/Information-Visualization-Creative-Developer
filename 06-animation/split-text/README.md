# split-text — 文字拆分入场

可复用动效：把标题/段落拆成行、词、字，逐个/逐组 stagger 入场。单文件演示见 `index.html`（双击打开，**需联网**加载 SplitType 与 Anime.js）。

## 动效身份（稳定能力）

**拆分 + stagger 入场**。拆分粒度（chars / words / lines）和效果预设（rise / blur / scale / slide）都是 CONFIG 里的选项，不是新资产——本资产的 README 和代码注释都明确："styling variants are presets, not new folders"。

## 分层说明

| 层 | 内容 | 当前 Demo 取值 |
| --- | --- | --- |
| 动效本体 | SplitType 拆分 DOM + Anime.js stagger 动画 + `createTextReveal()` 胶水 API | — |
| 表现层（可变，CSS 变量） | 配色、字号、排版 | 暗底 + 橙色 eyebrow |
| 行为层（可变，`CONFIG`） | split 粒度、effect 预设、stagger/duration/delay/easing | chars + rise |

## 手感参数

- 主标题：`stagger:34`、`duration:760`、`delay:160`、`easeOutExpo`
- 辅助文案：词级拆分，参数更轻（`stagger:14~24`、`duration:580~620`、easeOutCubic），延迟错峰（80 / 540）形成先后层次
- 行容器 `overflow:hidden` + `padding-bottom:.06em`，保证 rise 效果从"遮罩内升起"且不裁切下行字母（descender）

## 接口

```js
createTextReveal({
  target: ".reveal-title",  // 选择器或元素
  split: "chars",           // chars | words | lines
  effect: "rise",           // rise | blur | scale | slide
  stagger: 34, duration: 760, delay: 0,
  easing: "easeOutExpo"
});
```

## 依赖

split-type@0.3.4 · animejs@3.2.2（均 CDN）

## 实现要点（容易踩坑的地方）

- **重放必须 revert**：SplitType 会改 DOM，重放前用 `splitRegistry` 记住实例并 `revert()`，否则反复动画后 DOM 嵌套腐烂
- **先 set 再 animate**：用 `anime.set(items, preset.from)` 直接写初始态，避免首帧闪烁
- **resize 要重拆**：line 拆分依赖排版宽度，窗口变化后需 revert 重拆再播（已做 140ms 防抖）
- **性能**：只对 transform/opacity/filter 做动画，元素带 `will-change`

## 相关资产

- `../line-mask/`：同栈的行级遮罩 reveal（编辑感）
- `../blur-focus/`：同栈的景深聚焦 reveal（电影感；注意它的 blur 是深度模型，强于本资产的 blur 预设）

split-text 管字/词/行的颗粒 stagger，line-mask 管行遮罩滑入，blur-focus 管对焦——按场景选用。

## 来源

自研资产（原 `split-text-reveal.html`），2026-09 归档入 `06-animation/`。
