# viscous-orbit — 黏连轨道

可复用效果：一组卡片沿椭圆轨道运行，WebGL2 shader 把卡片渲染成互相黏连融合的流体（metaball），DOM 层同步渲染文字/图片内容。单文件演示见 `index.html`（双击打开，需 WebGL2）。

## 分层说明

| 层 | 内容 | 当前 Demo 取值 |
| --- | --- | --- |
| 效果本体（稳定能力） | 椭圆轨道几何 + SDF 黏连融合 + 前后景深 | — |
| 表现层（可变，CSS/CONFIG） | 配色、辉光强度、卡片内容（文字或图片） | 金色系（`CONFIG.colors`） |
| 行为层（可选，CONFIG） | 惯性旋转、拖拽、滚轮加速、点击吸附、鼠标熔化 | 全部开启 |

## 参数（`CONFIG`）

- `items`：轨道内容，最多 9 个；`image` 留空用文字卡片，填透明 PNG/WebP 路径自动切换为图片
- `ring`：
  - 几何：`radiusX/Y`（轨道半径比例）、`centerOffsetX/Y`（轨道中心偏移）、`step`（卡片角度间隔）
  - 透视：`backScale / frontScale / perspectivePower`（前后景深缩放曲线）
  - 运动：`autoSpeed`（自转速度）、`dragStrength / wheelStrength`（交互力度）、`damping`（惯性阻尼）、`snapDuration`（点击吸附时长）
  - 黏度：`viscosity`（基础 smin 平滑系数）、`cursorMelt / cursorReach`（鼠标附近黏度增强）、`glow`（辉光）
- `colors`：`bg / goldA / goldB / ivory`（shader uniform，0~1 RGB）

## 交互

拖拽旋转 · 滚轮加速 · 点击卡片吸附到前景 · 空格暂停 · 鼠标靠近增强黏连

## 实现要点

- 全屏三角形 fragment shader，无顶点缓冲；`smin` 平滑并集实现黏连，`uCursorMelt` 让黏度随鼠标距离局部变化
- DOM 与 WebGL 共用 `geometry(i)`：同一份几何同时喂 shader uniform 和 DOM transform，融合体与文字始终对齐
- `front = pow((cos(a)+1)/2, perspectivePower)` 统一驱动缩放、透明度、模糊、z-index、shader 着色
- 性能：DPR 上限 1.6，`dt` 上限 33ms，DOM 只动 transform/opacity/filter

## 来源

从 `07-pages/own-viscose-orbit/`（品牌展示母版）做减法抽出：移除了品牌中心文字、模式切换、HUD、badge、暗角等页面壳，只保留黏连轨道本体。配色、速度等可变表现保留在 CONFIG，不写进目录名。
