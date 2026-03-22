---
title: 前端开发严格规范
applyTo: "src/**/*.{ts,js,vue}"
description: "Use when: 前端开发、页面改动、路由改动、样式改动、需求实现。严格按需求文档执行，禁止私自扩展页面/交互。"
---

## 总原则
- 先需求后实现：未明确写入需求文档的功能一律不做。
- 禁止擅自扩展：禁止新增页面、弹窗、筛选项、动画、主题、流程分支，除非需求文档明确要求。
- 变更最小化：优先在现有组件与路由内做最小改动，避免重构式改写。

## 需求映射
- 编码前必须形成“需求条目 -> 代码变更点”映射。
- 每个需求条目至少对应一个可验证实现点（组件、路由、状态、接口调用之一）。
- 若需求存在歧义，默认采用最小实现，不主动增加额外 UX。

## 代码结构与命名
- 组件命名使用 PascalCase，管理页按 `*Management.vue` 组织。
- 优先使用 `<script setup lang="ts">` 与 Composition API。
- 路由使用 `meta.requiresAuth` 标识受保护页面，并与 Keycloak 守卫逻辑保持一致。

## 样式与设计系统
- 仅使用现有样式分层：`src/assets/base.css` 与 `src/assets/main.css`。
- 不引入新的设计语言（颜色体系、字体体系、阴影体系）除非需求明确。

## 交付门禁
- 提交前必须提供：
	- 需求覆盖清单（已实现/未实现/不适用）。
	- 风险与假设清单。
	- 验证结果（构建、关键流程手测）。

## 文档模板引用
- 开发输入模板：`.github/templates/development-input-template.md`
- 开发输出模板：`.github/templates/development-output-template.md`
