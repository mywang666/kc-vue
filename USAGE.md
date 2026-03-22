# KC-Vue Copilot Customizations 使用文档

本项目在 `.github/` 下维护了指令、Agent、Skill、命令、模板、插件清单，用于规范前端交付与需求一致性。本文包含具体用法、注释说明与示例。

## 1. 快速开始（推荐顺序）
1. 读取总览：见 [.github/README.md](.github/README.md)
2. 填写输入文档：
    - [.github/templates/development-input-template.md](.github/templates/development-input-template.md)
    - [.github/templates/requirement-traceability-template.md](.github/templates/requirement-traceability-template.md)
3. 开发与验证：运行命令或使用命令面板（见第 5 节）
4. 填写输出文档：
    - [.github/templates/development-output-template.md](.github/templates/development-output-template.md)
    - [.github/templates/change-summary-template.md](.github/templates/change-summary-template.md)
    - [.github/templates/pr-merge-checklist-template.md](.github/templates/pr-merge-checklist-template.md)
5. 交付审查：使用 `frontend-review` Agent 做一致性审查

## 2. 指令层（Instructions）
这些文件会根据 `applyTo` 自动进入上下文，主要用于限制范围与规范执行。
- 前端开发约束： [.github/instructions/frontend.instructions.md](.github/instructions/frontend.instructions.md)
- 需求边界守卫： [.github/instructions/requirements-guard.instructions.md](.github/instructions/requirements-guard.instructions.md)
- Git 工作流规范： [.github/instructions/git-workflow.instructions.md](.github/instructions/git-workflow.instructions.md)
- 复杂项目规范： [.github/instructions/large-project.instructions.md](.github/instructions/large-project.instructions.md)

使用说明：
- 对 `src/**/*.{ts,js,vue}` 的改动会自动触发前端与需求守卫规则。
- 需求条目 >= 10 或受影响文件 >= 8 时，进入分批交付策略。

示例（说明性，不会直接执行）：
```text
当你请求“新增路由与页面”时，frontend.instructions 会要求先映射需求条目。
当你请求“上线前审查”时，git-workflow.instructions 会要求提交与合并规范。
```

逐项用法与注释：
- 前端开发约束（frontend.instructions）
   - 用途：限制 UI/交互扩展，要求最小改动。
   - 触发：修改 `src/**/*.{ts,js,vue}`。
   - 例子：
      ```text
      请求：增加页面筛选条件
      要求：必须来自需求文档，且不新增额外筛选项
      ```
- 需求边界守卫（requirements-guard.instructions）
   - 用途：强制列出需求条目与实现映射。
   - 触发：需求实现、功能变更、评审场景。
   - 例子：
      ```text
      需求条目：FR-02
      映射：src/components/OrderList.vue
      ```
- Git 工作流规范（git-workflow.instructions）
   - 用途：约束提交格式、PR 要素、分支策略。
   - 触发：提交、合并、发布前整理。
   - 例子：
      ```text
      feat(order): 新增状态筛选
      ```
- 复杂项目规范（large-project.instructions）
   - 用途：当需求多、文件多时要求分批交付。
   - 触发：需求条目 >= 10 或受影响文件 >= 8。
   - 例子：
      ```text
      Batch-1 主流程
      Batch-2 守卫与权限
      ```

## 3. Agent 层（Agents）
Agents 用于在对话中选择特定行为模式。
- `frontend`：需求驱动交付与前端实现主力（见 [.github/agents/frontend.agent.md](.github/agents/frontend.agent.md)）
- `frontend-review`：需求一致性审查与发布门禁（见 [.github/agents/frontend-review.agent.md](.github/agents/frontend-review.agent.md)）

使用方式：
- 在 Copilot Chat 中选择 Agent（或输入 `@frontend` / `@frontend-review`）。
- `frontend` 会自动加载关键指令，并优先调用需求驱动 Skill。

示例：
```text
@frontend 帮我按需求文档改造订单列表页，并输出需求覆盖矩阵。
@frontend-review 审查当前改动是否存在需求外扩展。
```

## 4. Skill 层（Skills）
Skills 是可按需调用的流程封装（在聊天中输入 `/skill-name`）。
- `/requirement-driven-delivery`：需求拆解与映射（见 [.github/skills/requirement-driven-delivery/SKILL.md](.github/skills/requirement-driven-delivery/SKILL.md)）
- `/frontend-component`：组件开发规范（见 [.github/skills/frontend-component/SKILL.md](.github/skills/frontend-component/SKILL.md)）
- `/frontend-testing`：测试与回归（见 [.github/skills/frontend-testing/SKILL.md](.github/skills/frontend-testing/SKILL.md)）
- `/frontend-performance`：性能优化流程（见 [.github/skills/frontend-performance/SKILL.md](.github/skills/frontend-performance/SKILL.md)）
- `/development-docs`：输入/输出文档化（见 [.github/skills/development-docs/SKILL.md](.github/skills/development-docs/SKILL.md)）

使用要点与示例：
- 需求拆解与映射：
   ```text
   /requirement-driven-delivery
   需求来源：PRD-2026-03
   目标：新增列表筛选（仅需求内字段）
   ```
- 组件开发：
   ```text
   /frontend-component
   需求条目：FR-02
   受影响组件：src/components/OrderList.vue
   ```
- 测试与回归：
   ```text
   /frontend-testing
   需求条目：FR-03
   风险点：路由守卫与登录态
   ```
- 性能优化：
   ```text
   /frontend-performance
   问题：首屏加载慢
   目标：FCP < 2.5s
   ```
- 文档化：
   ```text
   /development-docs
   输出：开发输入与交付输出模板
   ```

逐项用法与注释：
- requirement-driven-delivery
   - 作用：把需求条目拆解为实现点与验证方式。
   - 输出：需求覆盖矩阵、偏差说明。
   - 示例：
      ```text
      /requirement-driven-delivery
      需求条目：FR-01, FR-02
      验收：手测 + 构建
      ```
- frontend-component
   - 作用：指导组件改造与接口设计。
   - 输出：变更清单、验证清单。
   - 示例：
      ```text
      /frontend-component
      组件：src/components/OrderList.vue
      props/emits：显式类型
      ```
- frontend-testing
   - 作用：补齐回归与风险验证。
   - 输出：测试结果报告、未覆盖说明。
   - 示例：
      ```text
      /frontend-testing
      风险点：登录态、路由守卫
      ```
- frontend-performance
   - 作用：性能定位与最小优化。
   - 输出：性能变更说明、复测结论。
   - 示例：
      ```text
      /frontend-performance
      目标：首屏 2.5s 内
      ```
- development-docs
   - 作用：生成输入/输出文档骨架。
   - 输出：填写模板清单与注意事项。
   - 示例：
      ```text
      /development-docs
      交付输出：development-output-template
      ```

## 5. 命令层（Commands）
命令文件对应常用工作流（在聊天中输入 `/command-name` 或在终端执行）。
- `/frontend`：前端开发与质量门禁命令（见 [.github/commands/frontend.commands.md](.github/commands/frontend.commands.md)）
- `/frontend-gate`：交付门禁流程（见 [.github/commands/frontend-gate.commands.md](.github/commands/frontend-gate.commands.md)）
- `/git-workflow`：分支与提交规范（见 [.github/commands/git-workflow.commands.md](.github/commands/git-workflow.commands.md)）
- `/large-project`：复杂项目分批交付命令（见 [.github/commands/large-project.commands.md](.github/commands/large-project.commands.md)）

示例：
```text
/frontend-gate
/git-workflow
```

逐项用法与注释：
- /frontend
   - 说明：开发与质量命令集合。
   - 示例：
      ```text
      /frontend
      运行开发与构建命令
      ```
- /frontend-gate
   - 说明：门禁流程（输入 -> 构建 -> 输出 -> 审查）。
   - 示例：
      ```text
      /frontend-gate
      Gate-2: npx tsc --noEmit
      ```
- /git-workflow
   - 说明：分支、提交与合并约束。
   - 示例：
      ```text
      /git-workflow
      新建分支 + Conventional Commits
      ```
- /large-project
   - 说明：复杂项目分批计划与门禁。
   - 示例：
      ```text
      /large-project
      生成 Batch-1/2/3 计划
      ```

常用终端命令示例：
```bash
npm install
npm run dev
npx tsc --noEmit
npm run build
```

## 6. 模板层（Templates）
模板用于产出可审计的交付文档。
- 开发输入： [.github/templates/development-input-template.md](.github/templates/development-input-template.md)
- 需求追踪： [.github/templates/requirement-traceability-template.md](.github/templates/requirement-traceability-template.md)
- 开发输出： [.github/templates/development-output-template.md](.github/templates/development-output-template.md)
- 变更摘要： [.github/templates/change-summary-template.md](.github/templates/change-summary-template.md)
- 提交模板： [.github/templates/git-commit-template.md](.github/templates/git-commit-template.md)
- PR 合并清单： [.github/templates/pr-merge-checklist-template.md](.github/templates/pr-merge-checklist-template.md)
- 复杂项目计划： [.github/templates/large-project-plan-template.md](.github/templates/large-project-plan-template.md)
- 长上下文摘要： [.github/templates/long-context-summary-template.md](.github/templates/long-context-summary-template.md)

示例片段：
```text
FR-01 | 列表筛选 | src/components/OrderList.vue | 新增状态筛选 | 手测 | 完成
```

逐项用法与注释：
- development-input-template
   - 作用：记录需求来源、范围、风险。
   - 示例：
      ```text
      需求名称：订单列表优化
      In Scope：状态筛选
      Out of Scope：新页面
      ```
- requirement-traceability-template
   - 作用：需求到实现的映射与偏差记录。
   - 示例：
      ```text
      FR-02 | 筛选条件 | src/components/OrderList.vue | 新增下拉框 | 手测 | 完成
      ```
- development-output-template
   - 作用：交付汇总与验证结果。
   - 示例：
      ```text
      构建结果：通过（npm run build）
      手工回归：通过（登录 + 列表加载）
      ```
- change-summary-template
   - 作用：变更摘要、风险与回滚。
   - 示例：
      ```text
      风险等级：低
      回滚步骤：回退至上一个发布分支
      ```
- git-commit-template
   - 作用：规范提交说明与关联信息。
   - 示例：
      ```text
      feat(order): 新增状态筛选
      ```
- pr-merge-checklist-template
   - 作用：PR 合并前的核对清单。
   - 示例：
      ```text
      [x] 已完成需求追踪矩阵
      [x] 已通过 npx tsc --noEmit
      ```
- large-project-plan-template
   - 作用：复杂项目分批交付计划。
   - 示例：
      ```text
      Batch-1 | 主流程 | FR-01~FR-03 | src/... | 构建通过
      ```
- long-context-summary-template
   - 作用：长上下文约束摘要与决策记录。
   - 示例：
      ```text
      技术边界：不引入新状态管理
      禁止事项：不新增页面
      ```

## 7. 插件基线（Plugins）
插件要求见 [.github/plugins/frontend.plugins.md](.github/plugins/frontend.plugins.md)。

推荐安装：
```bash
code --install-extension Vue.volar
code --install-extension dbaeumer.vscode-eslint
code --install-extension esbenp.prettier-vscode
```

验证示例：
```bash
code --list-extensions
```

治理要点：
- 仅安装与当前技术栈相关插件。
- 避免引入多个格式化器导致基线冲突。

逐项用法与注释：
- Vue.volar
   - 作用：Vue 语言服务与类型提示。
   - 例子：
      ```bash
      code --install-extension Vue.volar
      ```
- dbaeumer.vscode-eslint
   - 作用：ESLint 代码检查。
   - 例子：
      ```bash
      code --install-extension dbaeumer.vscode-eslint
      ```
- esbenp.prettier-vscode
   - 作用：统一格式化风格。
   - 例子：
      ```bash
      code --install-extension esbenp.prettier-vscode
      ```
- christian-kohler.path-intellisense
   - 作用：路径补全与快速定位。
   - 例子：
      ```bash
      code --install-extension christian-kohler.path-intellisense
      ```
- eamodio.gitlens
   - 作用：Git 历史与 blame 信息增强。
   - 例子：
      ```bash
      code --install-extension eamodio.gitlens
      ```

## 8. 交付门禁（建议）
交付门禁参考 [.github/commands/frontend-gate.commands.md](.github/commands/frontend-gate.commands.md)：
1. Gate-1：完成输入模板与需求追踪矩阵
2. Gate-2：`npx tsc --noEmit` + `npm run build`
3. Gate-3：完成输出模板、变更摘要、PR 清单
4. Gate-4：使用 `frontend-review` Agent 审查
5. Gate-5：按 Git 工作流提交与合并

## 9. 常见问题
- Q：什么时候用 `frontend-review`？
   A：提交前、发布前、需求一致性复核时使用。
- Q：需求不清楚怎么办？
   A：默认最小实现，并在输出中写明“待确认问题”。
