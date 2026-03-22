---
title: 复杂项目分批交付命令
---

## 规划阶段
- 列出改动面：`git diff --name-only origin/main...HEAD`
- 按目录统计：`git diff --name-only origin/main...HEAD | sort`

## 分批实施建议
- Batch-1：核心主流程（页面主功能）
- Batch-2：守卫与权限（路由/认证）
- Batch-3：样式与体验（不改变需求范围）

## 每批次门禁
- `npx tsc --noEmit`
- `npm run build`
- 填写模板：输入/输出/追踪矩阵
