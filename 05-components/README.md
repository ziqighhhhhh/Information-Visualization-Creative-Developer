# 05-components — 可复用组件

数据可视化 / 创意页面中反复出现的 UI 与数据组件。

## 存放什么

- 图例（分类图例、渐变色带、大小图例）
- Tooltip / 悬停信息卡
- 坐标轴、刻度、网格线
- 数据卡片、KPI 数字（含滚动计数）
- 控制器：筛选器、时间轴滑块、播放控件
- 图表主体之外的辅助元素

## 什么值得归档

- 在多个页面里出现过、样式稳定的组件
- API 设计得比较舒服的组件（明确输入输出）
- 解决过一致性问题的组件（如统一 Tooltip 的定位策略）

不值得归档：纯样式 demo、一次性的业务组件。

## 命名方式

**目录名描述稳定能力（组件是谁），不写可变表现。** 颜色、Dark/Light、Glow 属于 CSS 表现层；CountUp、Fade、Hover、Stagger 属于可选行为层——都写进代码和资产 README，不写进目录名。

`组件类型`，kebab-case，例如：

- `legend/`
- `tooltip/`
- `metric-card/`

反例：`metric-card-countup-dark`（countup 是可选行为、dark 是样式）。确有多个值得保留的变体时，在组件下建 `demos/`（如 `countup-dark.html`、`static-light.html`），不提前创建。

## 子目录建议包含

```
05-components/xxxx/
├── README.md      # 组件身份、表现层/行为层分层说明、接口、样式变量
├── index.html     # 最小演示
└── src/           # 实现代码（可选，单文件能装下就不建）
```
