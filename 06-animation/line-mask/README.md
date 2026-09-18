# line-mask — 行遮罩入场

可复用动效：把标题按视觉行拆分，每行包一个 `overflow:hidden` 遮罩，行在遮罩内滑入。单文件演示见 `index.html`（双击打开，**需联网**加载 SplitType 与 Anime.js）。

## 动效身份（稳定能力）

**行级遮罩 reveal**：遮罩负责裁切，行负责运动——编辑感、高级感排版常用的入场方式。效果方向（rise / drop / slide / skew）和 stagger 方向（first / last / center）都是 CONFIG 选项，不是新资产。

## 与 `../split-text/` 的区别

| | split-text | line-mask（本资产） |
| --- | --- | --- |
| 动画单元 | 字 / 词 / 行（颗粒感） | 只按行（编辑感） |
| 遮罩 | 行自身 `overflow:hidden` | **独立的 `.line-mask` 包裹元素**（遮罩与运动分离） |
| 额外维度 | 拆分粒度 | stagger 方向（first/last/center）、skew 预设 |
| 适用 | 活泼、强调节奏的标题 | 社论式大标题、品牌宣言 |

两者同栈（SplitType + Anime.js），按场景选用。第三个同类资产：`../blur-focus/`（深度模型对焦，电影感）。

## 手感参数

- 主标题：`stagger:110`、`duration:920`、`delay:160`、`easeOutExpo`，staggerFrom 可选 first/last/center
- 辅助文案：kicker 单行轻入（560ms），正文 650ms、delay 650 错峰
- 遮罩用 `padding-bottom:.07em; margin-bottom:-.07em` 抵消——裁切但不压行高

## 接口

```js
createMaskLineReveal({
  target: ".reveal-headline",
  effect: "rise",          // rise | drop | slide | skew
  stagger: 110, duration: 920, delay: 0,
  easing: "easeOutExpo",
  staggerFrom: "first"     // first | last | center
});
```

## 依赖

split-type@0.3.4 · animejs@3.2.2（均 CDN）

## 实现要点

- **遮罩与运动分离**：JS 给 SplitType 生成的每个 `.line` 包一层 `.line-mask`，遮罩拥有裁切、行拥有 transform——两者职责分开，效果预设随便换不冲突
- **重放必须 revert**：重放前 `instance.revert()` 拆掉旧的拆分与遮罩，防 DOM 腐烂
- **先 set 再 animate**：`anime.set(lines, preset.from)` 写初始态，防首帧闪烁
- **resize 重拆**：行拆分依赖排版宽度，窗口变化后 revert 重拆再播（140ms 防抖）

## 来源

自研资产（原 `mask-line-reveal.html`），2026-09 归档入 `06-animation/`。
