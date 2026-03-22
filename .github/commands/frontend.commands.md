---
title: 前端高级工作流命令
---

## 开发流程命令
- 初始化：`npm install`
- 开发：`npm run dev`
- 构建：`npm run build`
- 预览：`npm run preview`

## 质量门禁命令
- 类型检查：`npx tsc --noEmit`
- 代码检查：`npx eslint src --ext .ts,.vue`
- 格式检查：`npx prettier --check "src/**/*.{ts,vue,css,md}"`

## 交付前命令顺序
1. `npx tsc --noEmit`
2. `npm run build`
3. 执行手工回归（按模板记录）

## 文档联动
- 开发前填写：`.github/templates/development-input-template.md`
- 开发后填写：`.github/templates/development-output-template.md`
