# inbox — 待确认收集区

从 CodePen 自动收集的候选资产流程区。当前批次**已完成审查与分类**（2026-09）：

- 收集 101 件 → 人工审查（review.html）→ 保留 45 件 / 删除 56 件
- 保留的 45 件已按能力型命名规则分类入 `01-layout/`、`02-background/`、`04-effects/`、`05-components/`、`06-animation/`
- 每个资产 README 记录了原作、作者、许可（CodePen 公开 Pen 默认 MIT）与原链接

## 本目录保留的流程文件

- `review.html`：审查工具（逐件 iframe 预览 + 键盘决策 + 导出 decisions.json），下一批次复用
- `manifest.json`：本批次收集元数据（历史记录）
- `decisions.json`：本批次人工决策记录

## 下一批次流程

1. 运行收集脚本（CodePen popular 作者页，见会话记录）
2. 重新生成 review.html（嵌入新 manifest）
3. 人工审查导出 decisions.json
4. 按决策删除/分类
