---
title: Koa+Taro搭建CMS
date: 2019-04-26 14:14:11
tags: ["koa", "taro"]
---

## 登录功能

使用 POST 请求

### 用户认证

## 注册功能

### 验证码

``` js
const svgCaptcha = require('svg-captcha');

// 生成验证码
const captcha = svgCaptcha.create();

router.get('/signup', async (ctx, next) => {
  ctx.status = 200;
  ctx.type = 'svg';
  ctx.body = captcha.data;
})
```

## dashboard