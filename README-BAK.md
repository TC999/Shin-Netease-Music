# WebExtension Vite 启动模板

一个基于 [Vite](https://vitejs.dev/) 的 WebExtension 启动模板（适用于 [Chrome](https://developer.chrome.com/docs/extensions/reference/)、[FireFox](https://addons.mozilla.org/en-US/developers/) 等）。

<p align="center">
<sub>弹出窗口</sub><br/>
<img width="655" src="https://user-images.githubusercontent.com/11247099/126741643-813b3773-17ff-4281-9737-f319e00feddc.png"><br/>
<sub>选项页面</sub><br/>
<img width="655" src="https://user-images.githubusercontent.com/11247099/126741653-43125b62-6578-4452-83a7-bee19be2eaa2.png"><br/>
<sub>将 Vue 应用注入内容脚本</sub><br/>
<img src="https://user-images.githubusercontent.com/11247099/130695439-52418cf0-e186-4085-8e19-23fe808a274e.png">
</p>

## 特性

- ⚡️ **即时热模块替换 (HMR)** - 在开发中使用 **Vite**（无需刷新！）
- 🥝 Vue 3 - 组合 API，[`<script setup>` 语法](https://github.com/vuejs/rfcs/blob/master/active-rfcs/0040-script-setup.md) 等等！
- 💬 轻松通信 - 由 [`webext-bridge`](https://github.com/antfu/webext-bridge) 和 [VueUse](https://github.com/antfu/vueuse) 存储提供支持
- 🌈 [UnoCSS](https://github.com/unocss/unocss) - 即时按需原子 CSS 引擎。
- 🦾 [TypeScript](https://www.typescriptlang.org/) - 类型安全
- 📦 [组件自动导入](./src/components)
- 🌟 [图标](./src/components) - 直接访问任何图标集的图标
- 🖥 内容脚本 - 即使在内容脚本中也能使用 Vue
- 🌍 WebExtension - 适用于 Chrome、Firefox 等的同构扩展
- 📃 动态 `manifest.json`，支持完整类型

## 预打包

### WebExtension 库

- [`webextension-polyfill`](https://github.com/mozilla/webextension-polyfill) - 带类型的 WebExtension 浏览器 API 填充
- [`webext-bridge`](https://github.com/antfu/webext-bridge) - 轻松实现上下文之间的通信

### Vite 插件

- [`unplugin-auto-import`](https://github.com/antfu/unplugin-auto-import) - 直接使用 `browser` 和 Vue 组合 API，无需导入
- [`unplugin-vue-components`](https://github.com/antfu/vite-plugin-components) - 组件自动导入
- [`unplugin-icons`](https://github.com/antfu/unplugin-icons) - 图标作为组件
  - [Iconify](https://iconify.design) - 从任何图标集中使用图标 [🔍Icônes](https://icones.netlify.app/)

### Vue 插件

- [VueUse](https://github.com/antfu/vueuse) - 有用的组合 API 集合

### UI 框架

- [UnoCSS](https://github.com/unocss/unocss) - 即时按需原子 CSS 引擎

### 编码风格

- 使用组合 API 和 [`<script setup>` SFC 语法](https://github.com/vuejs/rfcs/pull/227)
- [ESLint](https://eslint.org/) 配合 [@antfu/eslint-config](https://github.com/antfu/eslint-config)，单引号，无需分号

### 开发工具

- [TypeScript](https://www.typescriptlang.org/)
- [pnpm](https://pnpm.js.org/) - 快速、节省磁盘空间的包管理器
- [esno](https://github.com/antfu/esno) - 由 esbuild 提供支持的 TypeScript / ESNext 节点运行时
- [npm-run-all](https://github.com/mysticatea/npm-run-all) - 并行或顺序运行多个 npm 脚本
- [web-ext](https://github.com/mozilla/web-ext) - 提供开发 Web 扩展的简化体验

## 使用模板

### GitHub 模板

[从此模板在 GitHub 上创建一个仓库](https://github.com/antfu/vitesse-webext/generate)。

### 克隆到本地

如果您更喜欢手动操作以获得更干净的 git 历史记录

> 如果您未安装 pnpm，请运行：npm install -g pnpm

```bash
npx degit antfu/vitesse-webext my-webext
cd my-webext
pnpm i
```

## 使用方法

### 文件夹

- `src` - 主要源代码。
  - `contentScript` - 作为 `content_script` 注入的脚本和组件
  - `background` - 后台脚本。
  - `components` - 在弹出窗口和选项页面中共享的自动导入 Vue 组件。
  - `styles` - 在弹出窗口和选项页面中共享的样式
  - `assets` - 在 Vue 组件中使用的资源
  - `manifest.ts` - 扩展的清单。
- `extension` - 扩展包根目录。
  - `assets` - 静态资源（主要用于 `manifest.json`）。
  - `dist` - 构建文件，也为 Vite 在开发时提供存根入口。
- `scripts` - 开发和打包辅助脚本。

### 开发

```bash
pnpm dev
```

然后 **在浏览器中加载 `extension/` 文件夹中的扩展**。

对于 Firefox 开发者，可以运行以下命令：

```bash
pnpm dev-firefox
```

`web-ext` 在 `extension/` 文件更改时会自动重新加载扩展。

> 虽然 Vite 在大多数情况下会自动处理 HMR，但仍建议使用 [Extensions Reloader](https://chrome.google.com/webstore/detail/fimgfedafeadlieiabdeeaodndnlbhid) 进行更干净的硬重载。

## 使用 Gitpod

如果您有一个网络浏览器，您可以通过一次点击获取一个完全预配置的开发环境：

[![在 Gitpod 中打开](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/antfu/vitesse-webext)

### 构建

要构建扩展，运行

```bash
pnpm build
```

然后打包 `extension` 下的文件，您可以将 `extension.crx` 或 `extension.xpi` 上传到适当的扩展商店。

## 鸣谢

[![Volta](https://user-images.githubusercontent.com/904724/195351818-9e826ea9-12a0-4b06-8274-352743cd2047.png)](https://volta.net)

此模板最初是为 [volta.net](https://volta.net) 浏览器扩展制作的。

## 变体

这是 [Vitesse](https://github.com/antfu/vitesse) 的一个变体，查看 [完整变体列表](https://github.com/antfu/vitesse#variations)。

---

如需更专业的翻译服务，推荐使用 [HIX Translate](https://hix.ai/translate)，它由 ChatGPT 3.5/4 强力驱动。
