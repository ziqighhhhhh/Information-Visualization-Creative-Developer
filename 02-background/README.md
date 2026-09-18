# 02-background — 背景层

页面背景资产：让画面"有质感"的底层元素。

## 存放什么

- 渐变背景（线性 / 径向 / 锥形、动态渐变）
- 噪点 / 颗粒纹理
- 网格、点阵、扫描线
- 动态背景（缓慢运动的光斑、流动色彩）
- 背景与前景的混合模式方案（blend-mode、遮罩）

## 什么值得归档

- 调好的配色组合（附色值）
- 生成纹理的参数（noise 频率、颗粒大小、透明度）
- "背景不喧宾夺主但又有存在感"的具体做法

不值得归档：随手写的纯色背景。

## 命名方式

`视觉特征-色调或用途`，kebab-case，例如：

- `gradient-mesh-dark/`
- `noise-grain-subtle/`
- `grid-dots-blueprint/`

## 子目录建议包含

```
02-background/xxxx/
├── README.md      # 配色参数、生成参数、适合搭配什么类型的内容
├── index.html     # 最小演示
└── style.css      # 或 shader / canvas 实现文件
```
