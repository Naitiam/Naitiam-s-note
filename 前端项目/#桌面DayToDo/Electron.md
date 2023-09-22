## 项目搭建

碰壁无数，最后选择 [electron-vite](https://link.juejin.cn/?target=https%3A%2F%2Fcn.electron-vite.org%2F)

```
pnpm create @quick-start/electron
pnpm i
pnpm dev
```

```
✔ Project name: … <electron-app>
✔ Select a framework: › vue
✔ Add TypeScript? … No / Yes
✔ Add Electron updater plugin? … No / Yes
✔ Enable Electron download mirror proxy? … No / Yes

Scaffolding project in ./<electron-app>...
Done.
```

项目目录，`index.ts`  入口文件

```
electron-demo
├─build
│  └──...						# 与构建相关的文件，例如应用程序的图标文件等
├─out								# 构建生成的输出文件
│  ├─main						# 主进程相关的文件
│  │   └──index.ts
│  └─preload				# 预加载脚本相关的文件
│      └──index.ts
├─resources					# 资源文件
│  └──icon.png
├──src
│  ├──main					# 主进程
│  │  ├──index.ts
│  │  └──...
│  ├──preload				# 预加载脚本
│  │  ├──index.ts
│  │  └──...
│  └──renderer    	# 渲染器 with vue, react, etc.
│     ├──src
│     ├──index.html
│     └──...
├──electron.vite.config.ts		# 包含 Vite 构建工具针对 Electron 应用程序的特定配置
├──dev-app-update.yml					# 包含应用程序更新的相关配置
├──electron-builder.yml				# 包含 Electron 打包工具的配置选项
├──.editorconfig							# 为代码编辑器提供了一组统一的格式化规则和配置选项
├──.eslintignore
├──.eslintrc.cjs
├──.gitignore
├──.npmrc
├──.prettierignore
├──.prettierrc.yaml
├──package.json
└──pnpm-lock.yaml
```

创建成功后 *package.json* 中有如下配置

```
{
  "scripts": {
    "start": "electron-vite preview", // 开启 Electron 程序预览生产构建
    "dev": "electron-vite dev", // 开启开发服务和 Electron 程序
    ""build": "electron-vite build"// 为生产构建代码
  }
}
```





