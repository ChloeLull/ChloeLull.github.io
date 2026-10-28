# AstroPaper 博客维护说明

本文件是项目的主维护文档，也是后续 Codex、Claude 等编码代理的默认上下文。其他项目说明与本文件冲突时，以当前源码和本文件为准。

## 当前项目状态

- 基础主题：AstroPaper 6.1.0。
- 包管理器：npm；只维护 `package-lock.json`。
- 默认语言：简体中文 `zh-CN`，时区 `Asia/Shanghai`。
- 站点地址已配置为 `https://chloelull.github.io/`；标题、描述和作者仍为占位值。
- 部署仓库为 `ChloeLull/ChloeLull.github.io`，属于 GitHub 用户主页仓库，站点路径为根路径 `/`。
- 文章目录 `src/content/posts/` 当前为空，因此构建会提示 posts 集合为空。
- 已关闭 Astro 开发工具栏。
- Git 已初始化为 `main` 分支，但尚未创建首次提交。

## 开发与验证

开发服务器必须以后台模式启动：

```powershell
npm run astro -- dev --background --host 127.0.0.1 --port 4321
npm run astro -- dev status
npm run astro -- dev logs
npm run astro -- dev stop
```

本地地址：`http://127.0.0.1:4321/`。

提交或交付前执行：

```powershell
npm run format:check
npm run lint
npm run build
```

构建命令会依次执行 Astro 类型检查、静态构建、Pagefind 索引，并把搜索资源复制到 `public/pagefind/`。

## GitHub Pages 部署

- 远程仓库：`https://github.com/ChloeLull/ChloeLull.github.io`
- 公开地址：`https://chloelull.github.io/`
- 推送 `main` 后由 `.github/workflows/deploy.yml` 自动构建和发布。
- GitHub 仓库的 Pages 发布源必须选择 `GitHub Actions`。
- 由于这是 `ChloeLull.github.io` 用户主页仓库，Astro `base` 保持默认根路径 `/`。

## 配置入口

- 站点级配置：`astro-paper.config.ts`
- Astro 集成与构建配置：`astro.config.ts`
- 内容集合定义：`src/content.config.ts`
- 布局入口：`src/layouts/Layout.astro`
- 主题颜色：`src/styles/theme.css`
- 导航、焦点和通用样式：`src/styles/global.css`
- 中英文界面文案：`src/i18n/lang/`

站点配置包含 URL、标题、描述、作者、语言、时区、分页数量、搜索、归档、OG 图片和编辑链接。修改前先检查当前源码。

## 当前视觉规范

- 配色为冷调蓝灰，不再使用 Jadeite 绿色。
- 浅色背景 `#f5f8fb`，正文 `#1c2735`，主色 `#315f7d`。
- 深色背景 `#202936`，正文 `#e7edf3`，主色 `#82b8df`。
- 正文与应用 UI 使用 MiSans，并由小米官方 CDN 加载；离线时会回退到 `system-ui`。
- 激活导航使用全局定义的 `1px` 实线下划线。
- 颜色调整只修改 `src/styles/theme.css` 中的 CSS 变量，不复制旧主题页面或整套样式。

## 内容与搜索

- 新文章放在 `src/content/posts/`，支持 `.md` 和 `.mdx`。
- 必填 Frontmatter：`title`、`pubDatetime`、`description`。
- 图片放在 `src/assets/` 时由 Astro 优化；需要按原文件名直接发布的静态资源放在 `public/`。
- Pagefind 搜索只读取构建结果；文章更新后需要重新执行 `npm run build`。
- `public/pagefind/` 是构建生成目录，不提交到 Git。

## 明确约束

- RSS 功能已移除：不存在 RSS 图标、RSS 路由、RSS 自动发现或 `@astrojs/rss` 依赖，`/rss.xml` 必须保持 404。
- 不重新引入示例文章或废弃主题文件。
- 不删除 `.git`、`.gitignore` 或 `AGENTS.md`。
- `node_modules/`、`dist/`、`.astro/`、`public/pagefind/` 不进入 Git。
- 不以 `npm audit fix --force` 盲目处理依赖；当前 `satori` 有一个暂无修复版本的中等严重性审计项。

## Git

每个完成并验证通过的阶段单独提交。首次提交前检查：

- 构建、格式和 ESLint 通过；
- RSS 仍为 404；
- 构建产物和依赖目录未被暂存；
- `AGENTS.md` 中的状态与当前源码一致。

## Astro 文档

完整文档：https://docs.astro.build

相关任务开始前查阅：

- [路由](https://docs.astro.build/en/guides/routing/)
- [Astro 组件](https://docs.astro.build/en/basics/astro-components/)
- [框架组件](https://docs.astro.build/en/guides/framework-components/)
- [内容集合](https://docs.astro.build/en/guides/content-collections/)
- [样式](https://docs.astro.build/en/guides/styling/)
- [国际化](https://docs.astro.build/en/guides/internationalization/)
