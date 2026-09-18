# blur-focus — 景深聚焦入场

可复用动效：文字从虚焦（blur + 微缩放 + 低位移）收敛到实焦，带聚焦方向控制。单文件演示见 `index.html`（双击打开，**需联网**加载 SplitType 与 Anime.js）。

## 动效身份（稳定能力）

**blur-to-sharp 聚焦**：核心价值不在"模糊"这个滤镜，而在**深度模型**——blur / translateY / scale / opacity 四个通道耦合联动，模拟镜头对焦。深度档位（soft / medium / deep）、聚焦方向（center / first / last / random）、拆分粒度（chars / words / lines）都是 CONFIG 选项。

## 与同类资产的区别

| | split-text | line-mask | blur-focus（本资产） |
| --- | --- | --- | --- |
| 核心机制 | 位移动感（rise/slide…） | 遮罩结构（行在 mask 内滑动） | 深度模型（四通道联动对焦） |
| 独有维度 | 拆分粒度 | 遮罩分离、stagger 方向 | 深度档位、聚焦方向（含 random） |
| 气质 | 活泼节奏 | 编辑排版 | 电影感、镜头感 |

三者同栈（SplitType + Anime.js），按场景选用；split-text 里的 `blur` 预设只是单通道模糊，不等于本资产的深度模型。

## 手感参数

- 深度档位：`soft{blur:7,y:8,scale:.985}` → `medium{15,16,.965}` → `deep{26,30,.925}`，opacity 随之 0.16→0.08→0
- 主标题：`stagger:28`、`duration:880`、`delay:120`、`easeOutExpo`，默认从 center 聚焦
- 辅助文案：soft 深度 + 词级 + 更小 stagger（24/18），delay 60/620 错峰
- **random 聚焦的实现**：Anime 没有 random stagger——先 shuffle 元素数组，再用 `from:"first"`（见 `orderItems()`）

## 接口

```js
createBlurFocusReveal({
  target: ".reveal-title",
  split: "chars",      // chars | words | lines
  from: "center",      // center | first | last | random
  depth: "medium",     // soft | medium | deep
  stagger: 28, duration: 880, delay: 0,
  easing: "easeOutExpo"
});
```

## 依赖

split-type@0.3.4 · animejs@3.2.2（均 CDN）

## 实现要点

- 与 `../split-text/` 相同的三条纪律：重放前 `revert()`、先 `anime.set` 初始态、resize 重拆（140ms 防抖）
- `filter` 动画开销高于纯 transform：deep 档位 + 长文本时注意，建议 chars 粒度控制文本长度

## 来源

自研资产（原 `preview.html`，Blur Focus Reveal），2026-09 归档入 `06-animation/`。
