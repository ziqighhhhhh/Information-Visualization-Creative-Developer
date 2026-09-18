# slide-merge — 对撞合并入场

可复用动效：两个元素（icon + wordmark）从两侧高速滑入、对撞、回弹定格为完整 lockup。单文件演示见 `index.html`（双击打开，**需联网**加载 Anime.js）。

## 动效身份（稳定能力）

**slide-merge**：对向滑入 → 撞击（flash + 横线爆开）→ 弹性 settle 的三段式合成。典型用于 logo lockup 揭示。速度档位（0.78 / 1 / 1.25）、残影数量（3 / 5 / 7）都是 CONFIG 参数。

## 手感参数（CONFIG）

| 参数 | 值 | 作用 |
| --- | --- | --- |
| `iconFromX / wordFromX` | ∓620px | 两侧起始距离 |
| `overshoot` | 24px | 过冲量（撞击感的来源） |
| `impactDuration` | 460ms | 滑入段（easeOutExpo） |
| `settleDuration` | 420ms | 回弹段（`easeOutElastic(1,.52)`） |
| `trailCount` | 5 | 残影层数 |

## 三段时序（timeline 偏移是精髓）

1. **滑入**（0 起）：两侧 blur(10px)→0 同步对进，终点落在 ±overshoot（不是 0）
2. **撞击**（`impactDuration*.73` 起）：中心 flash（scale .4→1.8）+ 横线 scaleX 爆开——在滑入完成**前**触发，才有"撞上"的同步感
3. **回弹**（`impactDuration*.82` 起）：elastic settle 到 0，与撞击段重叠——重叠率决定"撞击→回弹"的连贯性

## 残影实现（值得记住的技巧）

- **克隆真实渲染内容**：`buildGhosts()` 克隆资产 DOM（含上传的图片）生成 ghost 层，而不是画近似形状——换素材残影自动跟随
- 每层残影：延迟 `index*18ms`、时长 `+index*26ms`、blur `7+index*2px`、opacity `.22*ratio`——越远越慢越糊越淡，形成速度拖尾

## 接口

```js
createSlideMergeReveal({icon, wordmark, trailCount, speed});
// 或 window.logoReveal.play(...)
```

icon/wordmark 位支持上传图片（FileReader → dataURL），无图时用占位 SVG/文字。

## 依赖

animejs@3.2.2（CDN）

## 来源

自研资产（原 `preview.html`，Logo Reveal — Slide Merge），2026-09 归档入 `06-animation/`。
