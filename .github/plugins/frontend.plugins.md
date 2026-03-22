---
title: 前端插件基线与治理
---

## 基线插件
- `Vue.volar`：Vue 语言支持
- `dbaeumer.vscode-eslint`：ESLint 校验
- `esbenp.prettier-vscode`：格式化
- `christian-kohler.path-intellisense`：路径补全
- `eamodio.gitlens`：Git 增强

## 安装命令
- `code --install-extension Vue.volar`
- `code --install-extension dbaeumer.vscode-eslint`
- `code --install-extension esbenp.prettier-vscode`

## 治理规则
- 仅允许安装与当前技术栈相关插件。
- 禁止引入会改变代码风格基线的重复插件（如多个格式化器并行）。
- 插件变更需要记录在 `.github/templates/change-summary-template.md`。
