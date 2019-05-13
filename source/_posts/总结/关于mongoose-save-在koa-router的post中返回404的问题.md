---
title: 关于mongoose.save()在koa-router的post中返回404的问题
date: 2019-04-29 17:29:15
tags: [mongoose, koa]
---

## 问题代码

``` js
router.post('/signup', async (ctx, next) => {
  const data = ctx.request.body
  const user = {
    username: data.username,
    email: data.email,
    password: data.password
  }
  const newUser = new User(user);

  // express中的写法
  await newUser.save(err => {
    if (!err) {
      ctx.body = {
        code: 0,
        status: 200,
        message: '注册成功'
      }
    } else if (err.code === 11000) {
      ctx.body = {
        code: -1,
        status: 200,
        message: '此邮箱已注册'
      }
    } else {
      ctx.body = {
        code: 999,
        status: 200,
        message: '未知错误'
      }
    }
  })
})
```

上面的代码不行, postman中总是会显示 404 not found

然后尝试了

``` js
let code
await newUser.save(err => {
  if (!err) {
    code = 0
  } else if (err.code === 11000) {
    code = -1
  } else {
    code = 999
  }
})

console.log(code)
```

也不行, 打印一直是 undefined

后来有在网上看到 `let res = await newUser.save()`的写法, 但是koa会报错.

## 解决方法

花了一天时间, 终于想到可以用try catch来解决这个问题

``` js
router.post('/signup', async (ctx, next) => {
  const data = ctx.request.body
  const user = {
    username: data.username,
    email: data.email,
    password: data.password
  }
  const newUser = new User(user);

  try {
    let res = await newUser.save()
    if (res) {
      ctx.body = {
        code: 0,
        status: 200,
        message: '注册成功'
      }
    }
  }
  catch (err) {
    if (err.code === 11000) {
      ctx.body = {
        code: -1,
        status: 200,
        message: '此邮箱已注册'
      }
    } else {
      ctx.body = {
        code: 999,
        status: 200,
        message: '未知错误'
      }
    }
  }
})
```

这样终于可以在 postman 中正确的返回body了!
