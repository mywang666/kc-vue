---
title: Git 提交与合并规范
applyTo: "**/*.{ts,js,vue,md,json,yml,yaml}"
description: "Use when: 代码提交、分支合并、PR 审查、发布前整理。"
---

## 分支策略
- `main`：稳定发布分支，禁止直接提交。
- `feature/<scope>-<topic>`：需求开发分支。
- `fix/<scope>-<topic>`：缺陷修复分支。
- `chore/<scope>-<topic>`：工程或配置调整分支。

## 提交规范（Conventional Commits）
- 格式：`type(scope): subject`
- type 允许：`feat` `fix` `refactor` `perf` `test` `docs` `chore` `build` `ci`
- subject 使用简明中文或英文，禁止空泛描述（如 update / modify）。

## 提交粒度
- 一个提交只做一类变更（功能、重构、文档分离）。
- 禁止将“需求实现 + 大规模格式化”混在同一次提交。
- 提交前确保可构建，且通过基本校验命令。

## 合并规范
- 采用 PR 合并，禁止直接 push 到 `main`。
- 至少通过：需求一致性检查、构建检查、关键路径回归。
- PR 描述必须附：需求编号、变更范围、风险、回滚方案。

## 严格限制
- 未完成需求输入模板与追踪矩阵，禁止发起合并。
- 出现需求外页面/交互扩展，PR 必须驳回。
