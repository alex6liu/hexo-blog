---
title: koa学习
date: 2019-04-22 14:45:29
tags: [koa, nodejs]
---
# koa 学习

## 洋葱模型
![](https://camo.githubusercontent.com/d80cf3b511ef4898bcde9a464de491fa15a50d06/68747470733a2f2f7261772e6769746875622e636f6d2f66656e676d6b322f6b6f612d67756964652f6d61737465722f6f6e696f6e2e706e67)

## Middleware
### Router
```koa-router``` [link](https://github.com/ZijianHe/koa-router)

#### 安装 
```npm install koa-router```

#### Basic Usage
``` js
var Koa = require('koa');
var Router = require('koa-router');

var app = new Koa();
var router = new Router();

router.get('/', (ctx, next) => {
  // ctx.router available
});

app
  .use(router.routes())
  .use(router.allowedMethods());
```

Additionaly, ```router.all()``` can be used to match against all methods.

#### 动态路由
```js
router.get('/:id', (ctx, next) => {
  console.log(ctx.params)
});
```

#### url传值
```js
router.get('/news', (ctx, next) => {
  console.log(ctx.query) // -> 推荐
  console.log(ctx.querystring)
  console.log(ctx.url)
  console.log(ctx.request.url)
  console.log(ctx.request.query)
});
```

#### 公共数据
``` js
app.use(async function (ctx) {
  ctx.state = {
    session: this.session,
    title: 'app'
  };
});
```

### ejs模板引擎
#### 安装
```npm i ejs koa-views```

#### Usage
``` js
const views = require('koa-views');
const path = require('path');

app.use(views(path.join(__dirname, '../views'), {
  extension: 'ejs'
}))

// app.use(views('views', { extension: 'ejs' })) // 后缀名ejs
// app.use(views('views', { map: {html: 'ejs' }})) // 后缀名html

// 在views文件夹下新建index.ejs
app.use(async function (ctx) {
  await ctx.render('index', {
    title: 'hello'
  });
});
```

#### ejs语法
##### 数据绑定
```<%= title %>```

##### for循环
list是绑定的数据

``` js
<% for(let i; i< list.length: i++) { %>
  <%= list[i] %>
<% } %>
```

##### 引入模板
``` js
// public/header.ejs
<h2>Header</h2>
```

``` js
<% include public/header.ejs %>
```

##### 绑定html数据
``` js
<%- html %>
```

### 获取post提交的数据
#### 原生
``` js
app.use( async ( ctx ) => {

  if ( ctx.url === '/' && ctx.method === 'GET' ) {
    // 当GET请求时候返回表单页面
    let html = `
      <h1>koa2 request post demo</h1>
      <form method="POST" action="/">
        <p>userName</p>
        <input name="userName" /><br/>
        <p>nickName</p>
        <input name="nickName" /><br/>
        <p>email</p>
        <input name="email" /><br/>
        <button type="submit">submit</button>
      </form>
    `
    ctx.body = html
  } else if ( ctx.url === '/' && ctx.method === 'POST' ) {
    // 当POST请求的时候，解析POST表单里的数据，并显示出来
    let postData = await parsePostData( ctx )
    ctx.body = postData
  } else {
    // 其他请求显示404
    ctx.body = '<h1>404！！！ o(╯□╰)o</h1>'
  }

// 解析上下文里node原生请求的POST参数
function parsePostData( ctx ) {
  return new Promise((resolve, reject) => {
    try {
      let postdata = "";
      ctx.req.addListener('data', (data) => {
        postdata += data
      })
      ctx.req.addListener("end",function(){
        let parseData = parseQueryStr( postdata )
        resolve( parseData )
      })
    } catch ( err ) {
      reject(err)
    }
  })
}

// 将POST请求参数字符串解析成JSON
function parseQueryStr( queryStr ) {
  let queryData = {}
  let queryStrList = queryStr.split('&')
  console.log( queryStrList )
  for (  let [ index, queryStr ] of queryStrList.entries()  ) {
    let itemList = queryStr.split('=')
    queryData[ itemList[0] ] = decodeURIComponent(itemList[1])
  }
  return queryData
}
```

#### koa-bodyparser中间件
```npm i koa-bodyparser```

``` js
const bodyParser = require('koa-bodyparser')

// 使用ctx.body解析中间件
app.use(bodyParser())

app.use( async ( ctx ) => {

  if ( ctx.url === '/' && ctx.method === 'GET' ) {
    // 当GET请求时候返回表单页面
    let html = `
      <h1>koa2 request post demo</h1>
      <form method="POST" action="/">
        <p>userName</p>
        <input name="userName" /><br/>
        <p>nickName</p>
        <input name="nickName" /><br/>
        <p>email</p>
        <input name="email" /><br/>
        <button type="submit">submit</button>
      </form>
    `
    ctx.body = html
  } else if ( ctx.url === '/' && ctx.method === 'POST' ) {
    // 当POST请求的时候，中间件koa-bodyparser解析POST表单里的数据，并显示出来
    let postData = ctx.request.body // -> 就是这一句
    ctx.body = postData
  } else {
    // 其他请求显示404
    ctx.body = '<h1>404！！！ o(╯□╰)o</h1>'
  }
})
```

### 静态资源
#### 原生
[link](https://github.com/ChenShenhai/koa2-note/blob/master/note/static/server.md)

#### 中间件
```koa-static```

``` js
const Koa = require('koa')
const path = require('path')
const static = require('koa-static')

const app = new Koa()

// 静态资源目录对于相对入口文件index.js的路径
const staticPath = './static'

app.use(static(
  path.join( __dirname,  staticPath)
))


app.use( async ( ctx ) => {
  ctx.body = 'hello world'
})

app.listen(3000, () => {
  console.log('[demo] static-use-middleware is starting at port 3000')
})
```

### art-template模板引擎
- 速度极快
- 支持ejs语法

#### 安装
```
npm install --save art-template koa-art-template
```

#### Usage
``` js
const Koa = require('koa');
const render = require('koa-art-template');

const app = new Koa();
render(app, {
  root: path.join(__dirname, 'view'),
  extname: '.art',
  debug: process.env.NODE_ENV !== 'production'
});

app.use(async function (ctx) {
  await ctx.render('user');
});

app.listen(8080);
```

#### syntax
[link](https://aui.github.io/art-template/docs/syntax.html)
``` js
{{value}}
```

## cookie
### 使用方法

koa提供了从上下文直接读取、写入cookie的方法
- ctx.cookies.get(name, [options]) 读取上下文请求中的cookie
- ctx.cookies.set(name, value, [options]) 在上下文中写入cookie

koa2 中操作的cookies是使用了npm的cookies模块，源码在[https://github.com/pillarjs/cookies](https://github.com/pillarjs/cookies)，所以在读写cookie的使用参数与该模块的使用一致。

### 例子代码
``` js
const Koa = require('koa')
const app = new Koa()

app.use( async ( ctx ) => {

  if ( ctx.url === '/index' ) {
    ctx.cookies.set(
      'cid', 
      'hello world',
      {
        domain: 'localhost',  // 写cookie所在的域名
        path: '/index',       // 写cookie所在的路径
        maxAge: 10 * 60 * 1000, // cookie有效时长
        expires: new Date('2017-02-15'),  // cookie失效时间
        httpOnly: false,  // 是否只用于http请求中获取
        overwrite: false  // 是否允许重写
      }
    )
    ctx.body = 'cookie is ok'
  } else {
    ctx.body = 'hello world' 
  }

})

app.listen(3000, () => {
  console.log('[demo] cookie is starting at port 3000')
})
```

## session
koa2原生功能只提供了cookie的操作，但是没有提供session操作。session就只用自己实现或者通过第三方中间件实现。在koa2中实现session的方案有一下几种
- 如果session数据量很小，可以直接存在内存中
- 如果session数据量很大，则需要存储介质存放session数据

### 数据库存储方案
- 将session存放在MySQL数据库中
- 需要用到中间件
    - koa-session-minimal 适用于koa2 的session中间件，提供存储介质的读写接口 。
    - koa-mysql-session 为koa-session-minimal中间件提供MySQL数据库的session数据读写操作。
    - 将sessionId和对应的数据存到数据库
- 将数据库的存储的sessionId存到页面的cookie中
- 根据cookie的sessionId去获取对于的session信息

### 例子代码
```js
const Koa = require('koa')
const session = require('koa-session-minimal')
const MysqlSession = require('koa-mysql-session')

const app = new Koa()

// 配置存储session信息的mysql
let store = new MysqlSession({
  user: 'root',
  password: 'abc123',
  database: 'koa_demo',
  host: '127.0.0.1',
})

// 存放sessionId的cookie配置
let cookie = {
  maxAge: '', // cookie有效时长
  expires: '',  // cookie失效时间
  path: '', // 写cookie所在的路径
  domain: '', // 写cookie所在的域名
  httpOnly: '', // 是否只用于http请求中获取
  overwrite: '',  // 是否允许重写
  secure: '',
  sameSite: '',
  signed: '',
  
}

// 使用session中间件
app.use(session({
  key: 'SESSION_ID',
  store: store,
  cookie: cookie
}))

app.use( async ( ctx ) => {

  // 设置session
  if ( ctx.url === '/set' ) {
    ctx.session = {
      user_id: Math.random().toString(36).substr(2),
      count: 0
    }
    ctx.body = ctx.session
  } else if ( ctx.url === '/' ) {

    // 读取session信息
    ctx.session.count = ctx.session.count + 1
    ctx.body = ctx.session
  } 
  
})

app.listen(3000)
console.log('[demo] session is starting at port 3000')
```

## 验证码
```npm install --save svg-captcha```

### Usage
``` js
var svgCaptcha = require('svg-captcha');

var captcha = svgCaptcha.create();
console.log(captcha);
// {data: '<svg.../svg>', text: 'abcd'}
```


with express
``` js
var svgCaptcha = require('svg-captcha');

app.get('/captcha', function (req, res) {
	var captcha = svgCaptcha.create();
	req.session.captcha = captcha.text;
	
	res.type('svg');
	res.status(200).send(captcha.data);
});
```

with koa
``` js
const captcha = svgCaptcha.create({
  size: 6,
  fontSize: 50,
  width: 100,
  height: 40,
  background: '#cc9966'
})

ctx.session.code = captcha.text
ctx.response.type = 'image/svg+xml'
ctx.body = captcha.data
```