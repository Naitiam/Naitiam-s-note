> [nestjs 英文官网]() 
>
> [nestjs 中文网](https://docs.nestjs.cn/) 

Nest (NestJS) 是一个用于构建高效、可扩展的 Node.js 服务器端应用程序的开发框架。它利用 JavaScript 的渐进增强的能力，使用并完全支持 TypeScript （仍然允许开发者使用纯 JavaScript 进行开发），并结合了 OOP （面向对象编程）、FP （函数式编程）和 FRP （函数响应式编程）。

在底层，Nest 构建在强大的 HTTP 服务器框架上，例如 Express （默认），并且还可以通过配置从而使用 Fastify ！

## 创建nestjs项目

```
pnpm i -g @nestjs/cli
nest new [项目名称]
```

启动

```
pnpm run start
# 自动重新编译并重新加载服务器
pnpm run start:dev 
```

`src` 目录结构

```
src
 ├── app.controller.spec.ts	# 带有单个路由的基本控制器示例。
 ├── app.controller.ts		# 对于基本控制器的单元测试样例
 ├── app.module.ts			# 应用程序的根模块。
 ├── app.service.ts			# 带有单个方法的基本服务
 └── main.ts				# 应用程序入口文件。它使用 NestFactory 用来创建 Nest 应用实例。
```

`nest --help`  查看所有 nestjs 命令

![image-20230809171611987](img/Untitled.assets/image-20230809171611987.png)

### 生成模板

```
# 一个个生成
nest g co demo		# 生成controller模板
nest g mo demo 		# 生成module模板
nest g s demo		# 生成service模板
# 直接生成一套CRUD，在src的demo目录下
nest g res demo
```

选择RESTful风格

![image-20230809184058336](img/Untitled.assets/image-20230809184058336.png)

开启项目测试页面输出

```
http://localhost:3000/demo/123
```

### 版本控制

*\src\main.ts* 开启版本控制

```
import { NestFactory } from '@nestjs/core';
import { VersioningType } from '@nestjs/common';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  // 开启版本控制
  app.enableVersioning({
    type: VersioningType.URI,
  });
  await app.listen(3000);
}
bootstrap();
```

*src\demo\demo.controller.ts*

```
@Controller({
  path: 'demo',
  version: '1',
})
```

通过在url中添加路径  `/v+版本号 ` 来访问，例如

```\
http://localhost:3000/v1/demo/123`
```

## Session

`HTTP session `提供了一个用于在不同请求间存储信息的方法，

安装需要的包(以及 `TypeScript` 用户需要的类型包)：

```
pnpm i express-session --save
pnpm i -D @types/express-session
```

 *\src\main.ts*  中将`express-session`配置为全局中间件

```
import * as session from 'express-session';
// somewhere in your initialization file
  app.use(
    session({
      secret: 'test',
      name: 'test.session',
      rolling: true,
      cookie: { maxAge: null },
    }),
  );
```

参数配置详解

| 参数    | 解释                                                         |
| ------- | ------------------------------------------------------------ |
| secret  | 加密该会话 ID`cookie`                                        |
| name    | 生成客户端cookie 的名字 默认 connect.sid                     |
| cookie  | 设置返回到前端 key 的属性，默认值为{ path: ‘/’, httpOnly: true, secure: false, maxAge: null }。 |
| rolling | 在每次请求时强行设置 cookie，这将重置 cookie 过期时间(默认:false) |






vite项目添加跨域 
