---
title: Git 工作流命令
---

## 分支与提交
- 新建分支：`git checkout -b feature/<scope>-<topic>`
- 查看状态：`git status`
- 按块暂存：`git add -p`
- 提交：`git commit -m "feat(auth): 增加登录态路由校验"`

## 合并前检查
- 同步主干：`git fetch origin ; git rebase origin/main`
- 解决冲突后继续：`git rebase --continue`
- 本地校验：`npx tsc --noEmit ; npm run build`

## PR 前摘要
- 生成提交摘要：`git log --oneline -n 10`
- 查看变更文件：`git diff --name-only origin/main...HEAD`
