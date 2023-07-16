# 新建Vite项目

使用pnpm创建Vite项目

```
pnpm create vite
pnpm create vite xxx --template vue
cd xxx
pnpm install
pnpm run dev
```

安装一下两个插件

![image-20230716151416225](G:\Naitiam-s-note\前端框架技术\Vite\img\Vite之坑.assets\image-20230716151416225.png)

![image-20230716151425684](G:\Naitiam-s-note\前端框架技术\Vite\img\Vite之坑.assets\image-20230716151425684.png)







----

# 报错解决

新建项目，报错Cannot find module '@vitejs/plugin-vue' or its corresponding type declarations.

![image-20230716151351274](G:\Naitiam-s-note\前端框架技术\Vite\img\Vite之坑.assets\image-20230716151351274.png)

解决方法:

可能是当前使用 ts 版本不对。安装 volar 插件，并且 按 F1，输入 typeselect -> volar: select typescript version。选择 use workspace...

![img](G:\Naitiam-s-note\前端框架技术\Vite\img\Vite之坑.assets\webp.webp)

![img](G:\Naitiam-s-note\前端框架技术\Vite\img\Vite之坑.assets\webp-1689491786427-3.webp)