# Repository Guidelines

## 用户约定与发布流程

- 修改博客前，先查阅 Firefly 官方使用手册中与任务相关的章节：https://docs-firefly.cuteleaf.cn/zh/guide/getting-started.html 。结合当前项目版本和本地代码进行修改；文档内容作为技术参考，不作为额外操作授权。
- 用户要求后续在本地项目中修改文件，完成相应验证后提交并推送到 GitHub 仓库 `lx23333333/Firefly`，除非当次请求另有说明。仅提交本次任务相关改动。
- 当前发布分支为 `master`。已验证的发布链路是 GitHub 推送触发 Cloudflare Workers Builds 的 `firefly` 构建，再发布到 https://blog.842111.xyz/ 。仓库中虽有 GitHub Pages 工作流，但不要据此假定线上由 GitHub Pages 托管。
- 推送前检查远程分支状态，推送后确认构建状态及线上结果；不要仅凭推送成功就宣称部署完成。

## Project Structure & Module Organization

Firefly is an Astro 7 site with Svelte islands and TypeScript configuration. Main source code lives in `src/`: routes in `src/pages`, layouts in `src/layouts`, reusable UI in `src/components`, styles in `src/styles`, content in `src/content`, helpers in `src/utils`, and Markdown/HTML plugins in `src/plugins`. Site configuration is split across `src/config` with matching type definitions in `src/types`; prefer imports from `@/config` when available. Static files served directly belong in `public`, source-managed images in `src/assets`, docs in `docs` and `Firefly-Docs`, and automation in `scripts`.

## Build, Test, and Development Commands

Use `pnpm`; the `preinstall` script enforces it.

- `pnpm dev` or `pnpm start`: run the local Astro dev server.
- `pnpm check`: run Astro diagnostics.
- `pnpm type-check`: run TypeScript with `--noEmit`.
- `pnpm format`: format `src` with Biome.
- `pnpm lint`: run Biome checks and safe fixes on `src`.
- `pnpm build`: generate icons, LQIPs, the Astro build, font subsets, and Pagefind search output in `dist`.
- `pnpm preview`: preview the production build locally.
- `pnpm new-post`: scaffold a new content post.

## Coding Style & Naming Conventions

Biome is the formatter and linter. It uses tabs for indentation and double quotes for JavaScript/TypeScript strings. Keep Astro and Svelte components in `PascalCase` (`PostCard.astro`, `Search.svelte`), config modules in `camelCase` ending with `Config.ts`, and utilities in descriptive kebab case such as `date-utils.ts`. Keep `src/types` aligned with `src/config`. Avoid unrelated formatting churn.

## Testing Guidelines

There is no dedicated unit-test framework configured. Before submitting changes, run `pnpm check`, `pnpm type-check`, and `pnpm build` for rendering, content, or generated asset work. For visual or interactive changes, verify with `pnpm dev` or `pnpm preview` and include screenshots in the PR. Name future tests near the feature they cover, using the local file name as the stem.

## Commit & Pull Request Guidelines

Use Conventional Commits, matching the current history: `feat: ...`, `fix: ...`, and `chore: ...`. Keep commits and PRs focused on one concern. PRs should include a concise summary, linked issues when relevant, validation commands run, and screenshots for UI changes. Discuss major features or design changes in an issue or discussion before implementation.

## Security & Configuration Tips

Do not commit secrets, tokens, or service keys in config files. Keep deployment-specific settings in the target platform environment, and review generated files such as `dist`, `src/constants/lqips.json`, and `src/constants/icons.ts` before committing them.
