# kinetic-type — 动态字体

可复用动效：文字的**持续循环运动**（非一次性入场），附背景 marquee 跑马灯层。单文件演示见 `index.html`（双击打开，**需联网**加载 SplitType 与 Anime.js）。

## 动效身份（稳定能力）

**kinetic typography**：文字作为持续运动的视觉主体。四个运动程序（wave / punch / scatter / compress）是内部预设，拆分粒度（chars / words）、循环开关（once / loop）是 CONFIG 选项——都不是新资产。

## 与同类资产的区别

前三个同栈资产都是**一次性入场 reveal**；本资产是**循环运动程序**：

| | split-text | line-mask | blur-focus | kinetic-type（本资产） |
| --- | --- | --- | --- | --- |
| 类型 | 入场（一次） | 入场（一次） | 入场（一次） | **循环/持续** |
| 机制 | 位移 stagger | 行遮罩 | 深度对焦 | timeline 运动程序 |
| 场景 | 标题入场 | 社论标题 | 电影感聚焦 | 活动页、片头、高能 hero |

## 运动程序（手感记录）

- **wave**：translateY -16 + rotate -2° + scale 1.04 上下浮动，`easeInOutSine`，尾帧留白 260ms——平稳呼吸感
- **punch**：scale 1.28→.96→1 三段回弹，`easeOutBack`——打击感
- **scatter**：随机向量散开（±80px + blur 7px）→ easeOutExpo 聚合（from:center）→ 尾段 easeInCubic 上浮消散——聚合-消散循环
- **compress**：scaleX .55 压缩态 → 1.08 过冲 → 1 回稳（from:center）——弹性排版感

## 接口

```js
createKineticType({
  target: ".reveal-title",
  split: "chars",     // chars | words
  mode: "wave",       // wave | punch | scatter | compress
  loop: true,
  duration: 920, stagger: 34,
  easing: "easeInOutSine"
});
```

## 依赖

split-type@0.3.4 · animejs@3.2.2（均 CDN）

## 实现要点

- **timeline + 尾帧留白**：每个程序末尾 `.add({duration:N})` 插入空拍，循环时有节奏呼吸，不是无缝硬循环
- **scatter 的随机向量预生成**：先为每个元素生成随机偏移并存数组，`anime.set` 应用初始态，避免动画中随机数跳变
- **重放三件套**（与 split-text 相同）：`anime.remove(items)` + `anime.set` 归零所有通道 + SplitType `revert()`；resize 140ms 防抖重拆
- **背景 ticker**：anime 线性 loop `translateX 0→-36%`，16s；内容重复两遍以上即可无缝。opacity .055 做氛围层

## 潜在拆分方向

- ticker 跑马灯若再次复用 → 独立为 `06-animation/marquee/`
- 四个文字动效同栈同结构（registry/revert/resize 重拆/demo runner），**已达拆分阈值**，可考虑沉淀共享 SplitType 引擎封装

## 来源

自研资产（原 `kinetic-type.html`），2026-09 归档入 `06-animation/`。
