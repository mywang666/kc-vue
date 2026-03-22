# .github 高级前端配置总览

## 1. 指令层（Instructions）
- `instructions/frontend.instructions.md`：前端开发严格规范（需求优先、禁止随意扩展）
- `instructions/requirements-guard.instructions.md`：需求边界守卫
- `instructions/git-workflow.instructions.md`：Git 提交与合并规范
- `instructions/large-project.instructions.md`：复杂项目与大规模内容处理规范

## 2. Agent 层（Agents）
- `agents/frontend.agent.md`：高级前端交付 Agent
- `agents/frontend-review.agent.md`：前端需求一致性审查 Agent

## 3. Skill 层（Skills）
- `skills/frontend-component/SKILL.md`：组件开发流程
- `skills/frontend-testing/SKILL.md`：测试与回归流程
- `skills/frontend-performance/SKILL.md`：性能优化流程
- `skills/requirement-driven-delivery/SKILL.md`：需求驱动交付
- `skills/development-docs/SKILL.md`：输入输出文档化

## 4. 命令层（Commands）
- `commands/frontend.commands.md`：前端主流程命令
- `commands/frontend-gate.commands.md`：交付门禁命令
- `commands/git-workflow.commands.md`：Git 工作流命令
- `commands/large-project.commands.md`：复杂项目分批交付命令

## 5. 模板层（Templates）
- `templates/development-input-template.md`
- `templates/requirement-traceability-template.md`
- `templates/development-output-template.md`
- `templates/change-summary-template.md`
- `templates/git-commit-template.md`
- `templates/pr-merge-checklist-template.md`
- `templates/large-project-plan-template.md`
- `templates/long-context-summary-template.md`

## 6. 使用建议（推荐顺序）
1. 先填输入模板 + 需求追踪矩阵
2. 按门禁命令执行开发与验证
3. 填输出模板 + 变更摘要 + PR 合并清单
4. 审查 Agent 出具一致性结论后合并
