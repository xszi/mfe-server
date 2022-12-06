## mfe-server

原来的服务是使用 egg 写的，本人将使用 express 改写

首先个人理解 express 和 egg 的区别：

- express 偏原生，灵活性更强，egg 高度封装，大部分组件插件中间件只能用 egg 二次封装那一套
- express 文件结构（mvc）一般按自己思路组织，而 egg 会建议官方给定的 mvc 文件结构
- context 上下文 和 回调 request，response，next
- 个人偏向于喜欢 express，一方面灵活一些，另一方面，像 webpack 和 vite 这些工程化打包工具都是使用 express 作为服务，所以学习了 express 之后可以更方的学习 webpack 和 vite 的原理

## menul

### 启动 mysql 数据库

```
cd d:\mysql8\bin
mysql -u root -p
```

### 关于跨域

前端反向代理（proxy）

```js
proxy: {
    '/api': 'http://localhost:3000'
}
```

后端设置可跨域

```js
app.use(
  cors({
    origin: "http://localhost:7000",
    credentials: true,
  })
);
// const corsOptions = {
//     origin: [
//       'http://www.example.com',
//       'http://localhost:8080',
//     ],
//     methods: 'GET,HEAD,PUT,PATCH,POST,DELETE,OPTIONS',
//     allowedHeaders: ['Content-Type', 'Authorization'],
//   };

//   app.use(cors(corsOptions));
```

前端 axios 请求：axios.defaults.withCredentials = true

### 关于 cookie 操作

如果后台设置 httpOnly: true，则前端 js 不能操作 cookie，即 domain.cookie 不能获取到，只能能浏览器自动带上。

### XSRF (跨站请求伪造)

调用后台接口请求返回一个 token，保存在 localstorage（可以设置过期时间）中，再通过请求 header 设置，把 token 带到后台进行身份验证。
比如：

```
{ header['x-token']: 'GSKDKLSLSAADSKLSLS' }
```
