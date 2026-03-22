# Copilot Workspace Instructions

## Architecture
- 技术栈：Vue 3 + TypeScript + Vite。
- 认证：Keycloak，配置文件在 `src/keycloak.ts`。
- 启动链路：`src/main.ts` 初始化 Keycloak 后挂载应用；`src/router.ts` 通过前置守卫做认证与 token 刷新。
- 根组件与路由出口：`src/App.vue` + `<RouterView />`。
- 主要目录：页面与通用组件在 `src/components/`，图标在 `src/components/icons/`，样式在 `src/assets/`。

## Build And Test
- 安装依赖：`npm install`
- 本地开发：`npm run dev`
- 生产构建：`npm run build`
- 构建预览：`npm run preview`
- 当前未集成测试框架（无 `npm run test`）。

## Conventions
- 组件命名使用 PascalCase，管理页组件按 `*Management.vue` 组织。
- 优先使用 `<script setup lang="ts">` 与 Composition API。
- 路由使用 `meta.requiresAuth` 标识受保护页面，并保持守卫逻辑与 Keycloak 一致。
- 样式分层：`src/assets/base.css`（基础变量/基线）与 `src/assets/main.css`（全局样式）。
- 使用 `@` 路径别名指向 `src/`。

## Pitfalls
- 复杂页面缺少集中式状态管理（未集成 Pinia/Vuex），跨组件数据流需谨慎设计。
- Keycloak 参数当前在代码中配置，部署环境切换时易出错，建议改为环境变量。
- 无自动化测试，改动路由守卫与认证流程时优先做手动回归验证。

## Example Prompts
- “在 `src/components/` 新增一个管理页面，并接入 `src/router.ts` 的受保护路由。”
- “把 `src/keycloak.ts` 的配置迁移到 `.env` 并更新初始化逻辑。”
- “为当前项目接入 Vitest，先覆盖 `src/router.ts` 的守卫行为。”
- “按现有样式结构，补充一个全局主题变量并在页面组件中使用。”

## Next Customizations
- 可创建 `.github/instructions/frontend.instructions.md`（`applyTo: "src/**/*.{vue,ts}"`）约束组件与路由改动规范。
- 可创建 `.github/instructions/auth.instructions.md`（`applyTo: "src/{main,router,keycloak}.ts"`）聚焦认证改动安全检查。
- 可创建 `.github/instructions/testing.instructions.md`（`applyTo: "src/**/*"`）规范后续测试补齐策略。