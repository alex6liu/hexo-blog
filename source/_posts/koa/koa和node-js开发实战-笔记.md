---
title: <koa和node.js开发实战>笔记
date: 2019-04-25 15:16:52
tags: ["koa", "nodejs", "笔记"]
---

## 2

### 2.2 Context对象

``` js
app.use(async ctx => {
  ctx; // 这是 Context
  ctx .request; //这是 Koa Request
  ctx.response; //这是 Koa Response
  this; //这也是 Context
  this.request; //这也是 Koa Request
  this .response; //这也是 Koa Response
));
```

#### ctx.request

``` js
ctx.response.body = {
  url: ctx. request. url, //获取请求 URL
  query: ctx.request.query, //获取解析的查询字符串
  querystring : ctx.request.querystring //获取原始查询字符串
}
```

随后在浏览器中访问 `http://localhost:3000/?search=koa&keywords=context`，便可以看到 一串字符串，如下所示 :

``` js
{
  'url':'/?search=koa&keywords=context',
  'query' : { 'search' : 'koa', 'keywords' : 'context' } ,
  'querystring':'search=koa&keywords=context'
}
```

POST请求的参数获取方式和 GET请求不同. 

Koa没有封装获取 POST请求参数的方 法，因此需要解析 Context 中的原生 Node.js请求对象 req, 或者使用 `koa-bodyparser`中间件

#### ctx.response

在实际开发中， 除设置一个请求的响应主体外， 往往还需要通过 `ctx.response.status` 设置请求状态，如 200, 404, 500 等。

通过 `ctx.response.type` 可以设置响应的 `Content-Type`, 如果响应内 容是 HTML 格式，则设置为 `ctx.response.type ='html'`;如果响应内容是一张 png 图片，则设置为 `ctx.response句pe ='1mage/png'`。显式地设置 `Content-Type`是因为浏览器默认 的 `Content-Type` 是 `text/plain`，如果 `Content-Type` 不对会发生解析错误。

通过`ctx.request.accepts()`函数来判断客户端期望的数据类型

通过 `ctx.response.body` 设置响应体内容

和 `ctx.request.accepts()`类似的一个方法是 `ctx.response.is(types...)`，它可以用来检查响应类型是否是所提供的类型之一，这对创建操纵响应的中间件特别有用 。

还有一个比较常用的方法是 `ctx.response.redirect(url, [alt])`，这个方法用于将状态码 302 重定 向到 URL，例如用 户登录后自动重定向到网站的首页。

#### ctx.state

`ctx.state` 是推荐 的命名空间，用于通过中间件传递信息和前端视图。类似 koa-views 这 些渲染 View层的中间件也会默认把 ctx.state里面的属性作为 View 的上下文传入。

#### ctx.cookies

ctx.cookies 用于获取和设置 Cookie

``` js
ctx.cookies.get(name, [optionsJ); //获取Cookie
ctx.cookies.set(name, value, [options]); // 设置Cookie
```

![](https://raw.githubusercontent.com/alex6liu/blog-images/master/koa/ctx.cookie.options.png)

#### ctx.throw

ctx.throw用于抛出错误，把错误信息返回给用户， 代码示例如下:

``` js
app.use(async (ctx) => {
  ctx.throw(500);
});
```

### 2.3 Koa的中间件

通过 app.use()函数来加载中间件。

中间件函数是一个带有 ctx 和 next 两个参数的简单函数。

ctx 就是之前章节介绍的上下文，封装了 Request 和 Response 等对象; next 用于把中间件的执行权交给下游的中间件。 在 next()之前使用 await 关键字是因为 next()会返回一个 Promise 对象，而在当前中间件中位 于 next()之后的代码会暂停执行，直到最后一个中间件执行完毕后，再自下而上依次执行每 个中间件中 next()之后的代码，类似于一种先进后出的堆枝结构。

![](https://raw.githubusercontent.com/alex6liu/blog-images/master/koa/onion.png)

下面通过具体代码来演示中间件的执行，如下所示:

``` js
app.use (async function (ctx, next) {
  console.log('one start');
  await next();
  console.log('one end');
));
app.use (async function (ctx, next) {
  console.log('two start');
  ctx.body = 'two';
  await next();
  console.log('two end');
)};
app.use (async function (ctx, next) {
  console.log('three start');
  await next();
  console.log('three end');
)};
```

这段代码中有 3个中间件， 执行结果如下:

``` js
one start
two start
three start
three end
two end
one end
```

如果想将多个中间件组合成一个单一的中间件, 便于重用或导出，可以使用`koa-compose`，代码如下:

``` js
const all = compose ([middlewarel, middleware2, middleware3]);
app.use(all);
```

如果一个中间件没有调用 `await next()`，又会发生什么情况呢? 答案是:后面的中间件将不会被执行。

#### 常用 Koa 中间件

- koa-bodyparser
- koa-router
- koa-static
- koa-views

## 3 路由

前端路由主要解决了两个问题:在页面不刷新的前提下实现 URL 的变化，以及捕捉URL的变化并执行相应的页面逻辑。

### RESTful 规范

REST 的全称是 Representational State Transfer，即表现层状态转移.

REST设计一般符合以下条件:

- 程序或应用的事物都应该被抽象为资源。
- 每个资源对应唯一的URI。(URI的全称是 UniformResource Identifier，即统一资源标识符，是一个用于标识某一互联网资源名称的字符串)
- 使用统一的接口对资源进行操作。
- 对资源的各种操作不会改变资源标识。
- 所有的操作都是无状态的。

在该场景中，需要完成对网站用户的新增、修改、删除和查看操作。在非RESTful架构中，一般被设计为如下所示:

``` js
https://api.test.com/addUser // POST方法，请求发送新增用户信息
https://api.test.com/deleteUser //POST方法，请求发送用户的 ID
```

而基于RESTful架构设计的 API，全局只提供唯一的URI: `https://api.test.com/users`

``` js
https://api.test.com/users // POST方法， 请求发送新增用户信息
https://api.test.com/users/:id // DELETE方法，用户ID是URI的一部分
https://api.test.com/users/:id // PUT方法，请求发送用户的信息, ID是 URI 的一部分
https://api.test.com/users/:id // GET方法，用户 ID是 URI 的一部分
```

GitHub的API设计被称为RESTful API教科书的典范，地址为`https://developer.github.com/v3/`。 同时，不得不提的是 GitHub v4 的 API 使用了全新的设计风格 GraphQL ，地址为 `https://developer.github.com/v4/`。 GraphQL 提供了一套完整描述，使客户端能够没有任何冗余地准确获得需要的数据。

### 用法

如果一条路由请求在 all()方法和其他方法中同时命中， 只有执行了 `await next()`，这条路由请求才会在 all()方法和其他方法中都起作用

在项目中， all()方法一般用来设置请求头，如设置过期时间、CORS (Cross-Origin Resource Sharing ，跨域资源共享)等，

``` js
//通过调用路由的名称 user，生成路由==”/users/3”
router.url('url', 3);
//通过调用路由的名称user，生成路由== ”/users/3”
router.url('user', { id: 3 ));
```

#### 命名路由

使用 `router.url()`方法可以在代码中根据路由名称和参数(可选)生成具体的 URL，而不用采用宇符串拼接的方式去生成 URL。

#### 嵌套路由

``` js
const forums = new Router ();
const posts = new Router ();
posts.get('/', function (ctx, next) {...});
posts.get('/:pid', function (ctx, next) {... });
forums.use('/forums/:fid/posts', posts.routes(), posts.allowedMethods());
//获取互联网版块列表的接口
// ”/forums/:fid/posts”=>”/forums/123/posts”
//获取互联网版块下某篇文章的接口
// ”/forums/:fid/posts/:pid”=> ”/forums/123/posts/123”
app.use(forums.routes());
```

#### 路由前缀

``` js
let router = new Router ({
  prefix:'/users'
});
//匹配路由”/users”
router.get('/',...);
//匹配路由” /users/:id”
router.get('/:id',...);
```

#### URL参数

``` js
router.get('/:category/:title', function (ctx, next) {
  // 响应请求'/programming/how-to-koa'
  console.log(ctx .params);
  //参数解析=> ( category: 'programming', title:'how-to-koa')
});
```

### 通过 koa-router实现接口的权限控制

常见鉴别用户权限的方式有两种，一种是广泛使用的 `Cookie-Based Authentication` (基于 Cookie 的认证模式)，另一种是 `Token-Based Authentication` (基于 Token 的认证模式) 。

本案例采用 Token 方式认证。 

Token 方式最大的 优点在于采用了无状态机制，在此基础上，可以实现天然的跨域支持、前后端分离等，同时降低了服务端开发和维护的成本 。

Token 方式的缺点在于服务器每次都需要对 Token 进行校验，这一步骤会对服务器产生运算压力 。 

另一方面，无状态 API 缺乏对用户流程或异常的控制，为了避免出现一些例如回放攻击的异常情况，应该设置较短的过期时间，且需要对密钥进行严格的保护 。对于具有复杂流程的高危场景(如支付等〉， 则要谨慎选择 Token 认证模式 。

在本案例中，选用 jsonwebtoken (以下简称 JWT)来实现 Token 的生成、校验和解码。Token 的中间件实现选择 `koa-jwt`。

``` js
const Koa = require('koa');
const Router = require('koa-router');
const bodyParser = require('koa-bodyparser');
const { sign } = require('jsonwebtoken');
const { secret } = require('./config');
const jwt = require('koa-jwt')({ secret });
const app = new Koa();
const router = new Router();
const detail = new Router();
app.use(bodyParser());

router
  .post('/api/login', async (ctx, next) => {
    const user = ctx.request.body;
    if (user && user.username) {
      let { username } = user;
      const token = sign({ username }, secret, { expiresIn: '1h' });
      ctx.body = {
        message: 'Get Token Success',
        code: 1,
        token
      };
    } else {
      ctx.body = {
        message: 'Param Error',
        code: -1
      };
    }
  })
  .get('/api/userInfo', jwt, async ctx => {
    ctx.body = {
      username: ctx.state.user.username
    };
  })
  .get('/api/adminInfo', jwt, admin, async ctx => {
    ctx.body = {
      username: ctx.state.user.username
    };


app.use(router.routes()).use(router.allowedMethods());
app.listen(3000, () => {
  console.log('app listening 3000...');
});
```

middleware/admin

``` js
module.exports = () => {
  return async (ctx, next) => {
    if (ctx.state.user.username === 'admin') {
      next()
    } else {
      ctx.body = {
        code: -1,
        message: 'Authentication Error'
      }
    }
  }
}
```

## 4 HTTP

### URI 和 URL

- URI: Uniform Resource Identifier (统一资源标识符)
- URL: Uniform Resource Locator (统一资源定位符〉

URL 是 URI的一个子集

一个完整的 URL 一般由7个部分组成，如下所示:

`scheme: [// [user [:password]@] host[:port]] [/path] [?query] [#fragment]`

- scheme:使用的协议，如 FTP (File Transfer Protocol)、 HTTP 等 。
- user[:password]: 表示访问资源的用户名和密码，常见于 FTP 协议中 。
- host:主机，如 IP 地址或域名。
- port:端口号，如 HTTP 默认为 80 端口 。
- path:访问资源的路径。
- query: 请求数据，以“?”开头。
- fragment: 定位锚点，以“#”开头，可用于快速定位网页对应的段落。

### 常用的 HTTP 状态码

HTTP 状态码主要包括 1** (消息)、 2**(成功)、 3**(重定向)、 4**(请求错误〉、 5** 和 6** (服务器错误)

![](https://raw.githubusercontent.com/alex6liu/blog-images/master/http/http.statuscode.png)

### 常用的请求方法

![](https://raw.githubusercontent.com/alex6liu/blog-images/master/http/http.request.png)

### 常用的 HTTP 首部字段

![](https://raw.githubusercontent.com/alex6liu/blog-images/master/http/http.header.png)

## 5 构建 Koa Web 应用

MVC 全名是 Model View Controller，即模型、视图、 控制器。

- Model: 负责数据访问
- Controller: 负责处理消息
- View: 负责显示数据

三层架构( 3-TierArchitecture )是一个分层式的架构设计理念，如有必要，也可以分为多层。

分层的设计理念契合了“高内聚低藕合” 的思想，在软件体系架构设计中是最常见、也是最重要的一种结构。

通常意义上的三层架构是将整个业务应用划分为 界面层( User Interface Layer)、业务逻辑层( Business Logic Layer)、数据访问层( Data Access Layer)

### 在 Koa 中实现 MVC

#### 分离Router

路由部分的代码可以分离成独立的文件，并根据项目结构放置在适当的位置，方便管理。本示例中，将路由部分的代码独立在 router.js文件中，并置于项目根目录下

``` js
|-- app.js
|-- router.js
```

router.js

``` js
const router = require('koa-router')();
const HomeController = require('./controller/home');
module.exports = (app) => {
  router.get('/', HomeController.index);
  router.get('/home', HomeController.home);
  router.get('/home/:id/:name', HomeController.homeParams);
  router.get('/user', HomeController.login);
  router.post('/user/register', HomeController.register);
  app.use(router.routes()).use(router.allowedMethods());
}
```

app.js

``` js
const Koa = require('koa');
const bodyParser = require('koa-bodyparser');
const app = new Koa();
const router = require('./router');
app.use(bodyParser());
router(app);
app.listen(3000, () => {
    console.log('server is running at http://localhost:3000');
});
```

#### 分离 controller

controller 负责存放响应 HTPP 请求的业务逻辑代码

controller/home.js

``` js
const HomeService = require('../service/home');
module.exports = {
    index: async (ctx, next) => {
        ctx.response.body = `<h1>index page</h1>`;
    },
    home: async (ctx, next) => {
        console.log(ctx.request.query);
        console.log(ctx.request.querystring);
        ctx.response.body = '<h1>HOME page</h1>';
    },
    homeParams: async (ctx, next) => {
        console.log(ctx.params);
        ctx.response.body = '<h1>HOME page /:id/:name</h1>';
    },
    login: async (ctx, next) => {
        ctx.response.body = `<form action="/user/register" method="post">
              <input name="name" type="text" placeholder="请输入用户名：ikcamp"/> 
              <br/>
              <input name="password" type="text" placeholder="请输入密码：123456"/>
              <br/> 
              <button>GoGoGo</button>
            </form>`;
    },
    register: async (ctx, next) => {
        let {name,password} = ctx.request.body;
        let data = await HomeService.register(name, password);
        ctx.response.body = data;

    }
}
```

业务层的代码分离成功之后，需要修改 router.js文件，在文件中引入 controller/home.js, 并以 home.js 中的函数作为 HTTP 请求的响应函数

**注意: 上面的router.js代码是分离后的**

在实际开发中，有时 Node.js 需要进行一些数据访问层的操作，如操作数据库、调用第三方接口获取数据等，因此需要分离出 Service 层来进行相应处理 。相应地，Controller 只需要进行业务逻辑部分的处理即可。

#### 分离 Service

service/home.js

``` js
module.exports = {
    register: async (name, pwd) => {
        let data;
        if (name == 'ikcamp' && pwd == '123456') {
            data = `Hello， ${name}！`;
        } else {
            data = '账号信息错误';
        }
        return data;
    }
}
```

**注意: 上面的 controller/home.js 代码也是分离后的**

至此，项目代码已经完成了基本的结构分离，得到的模块包括单独处理 HTTP 请求的路由文件 router.js、对 HTTP 请求进行响应的 Controller 文件，以及为 Controller 提供 Model 数据的 Service 文件。

### 模板引擎

目前，可以在 Node.js 中应用且比较成熟的模板引擎有很多，例如 EJS、 Jade (现己改 名为 Pug)、 Handlebars、 Nunjucks、 Swig等

根据自己的需求选择合适的模板引擎

`koa-views`

### 静态资源

在访问站点时，浏览器会接收到各种资源，常见的有 HTML、 JavaScript脚本文件、 css 样式表、 GIF 图片资源和 Flash

那么浏览器是通过什么方式区分不同的资源类型， 又是如何决定以什么形式来显示的呢?

答案是根据 MIMEType，也就是该资源的媒体类型。

![](https://raw.githubusercontent.com/alex6liu/blog-images/master/http/mime-type.png)

`koa-static`

### 其他常用开发技巧

#### `koa-json`

#### 使用 koa-multer 中间件实现文件上传

**注意: Multer 不会处理任何非 multipart/form-data 类型的表单数据**

``` js
canst koa = require('koa');
const multer = require ( 'koa-multer' );
const app = koa();
app.use(multer({dest : './uploads/'}));
app.listen(3000) ;
```

## 6 数据库

### 在Koa中应用MySQL数据库

在 Node.js 中， 一般采用 Sequelize 这个 ORM 类库来操作数据库。 Sequelize 支持多种数据库，如 PostgreSQL、 MySQL、 SQLite和 MSSQL。

`npm install sequelize -save`

``` js
const Sequelize = require('sequelize');
const sequelize = new Sequelize('databaseName'，'userName勺' 'password'，{
  host : 'localhost',
  dialect : 'mysql'
}};
sequelize.authenticate().then (()=>{
  console.log('Connected');
  }).catch(err=>{
    console.error ('Connect failed');
  });
```

提示:由于建立数据库连接存在成本，所以通常情况下会通过连接池来提升数据库的连接效率，以避免每次执行数据库操作时重复建立连接。Sequelize默认支持连接池，可以在创建连接时指定 pool 参数来修改默认的连接池设置。

通过 Sequelize，我们可以直接定义数据模型来创建数据表，而不必去数据库中使用 SQL 脚本创建。可以通过 define 方法定义模型

``` js
const Categoty = sequelize.define('category', {
  id : Sequelize.UUID,
  name: Sequelize.STRING
})

const Project = sequelize.define('project',{ // 定义Project模型
  name: {
    type: Sequelize.STRING,
    allowNull: false,
    unique : true
  },
  date: {
    type : Sequelize.DATE,
    defaultValue: Sequelize.NOW
})
```

Sequelize 会默认为创建的数据表自动创建 createdAt 和 updatedAt 字段。同时，Sequelize 也提供了配置项来禁用或修改这些字段

在定义模型时，也可以为字段定义 Getter和 Setter， 定义写入数据的规则

``` js
const Custom = sequelize.define('custom', {
  name: {
    type : Sequelize .STRING,
    get () { //定义 Getter，可以自定义获取数据
      const title = this.getDataValue('title');
      return `${this.getDataValue('name')} (${title})`
    }
  }
  title : {
    title : Sequelize.STRING,
    set (val) { //定义 Setter，可以在写入数据前处理数据
      this.setDataValue('title', val.toUpperCase())
    }
  }
}
```

#### 同步

可以通过 sync 方法将定义的模型同步到数据库中。既可以同步单个表，也可以同步全部表 

``` js
sequelize.sync().then(() => { //同步全部模型
  // done
}).catch(error => {
  // some error thrown
})
Product.sync() //同步单个数据表
Project.sync({ force: true }) //强制同步，当数据库中已经存在表时，清除已经存在的表
```

#### 查询

``` js
await Product.findAll(); // 查出 Product表中的所有数据

await Project.findAll({ // 查询 name和 date字段
  attributes: ['name', 'date']
})
```

``` js
const { Op } = require( 'sequelize' );
await Project.findAll({
  where: {
    name: {
      [Op.like]: 't%' //查询操作为like，值为以 t开头
    }
  }
})
```

### 在 Koa 中应用 MongoDB 数据库

在开发 Node.js 应用时， 一般借助 Mongoose 类库来访问数据库

### 在Koa中应用Redis数据库

`npm install redis -save`

## 7 单元测试

## 8 优化与部署

### 日志

`npm install log4js -save`

根据日志的用途， 一般可以将日志分为访问日志和应用日志

应用日志包括 debug、 info、 warn 和 error 等不同级别

### 部署

`npm install pm2@lastst -g`

