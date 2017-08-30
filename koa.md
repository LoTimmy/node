
```
shell> npm install koa --save
shell> npm install koa@2 --save
```

#### :books: 參考網站：
- [koa](http://koajs.com/)

---

```js
//  Created by Timmy on 2016/1/1.
//  Copyright (c) 2015年 Timmy. All rights reserved.

const http = require('http');

const hostname = '127.0.0.1';
const port = 1337;

http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('Hello World\n');
}).listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```


```js
//  Created by Timmy on 2016/1/1.
//  Copyright (c) 2015年 Timmy. All rights reserved.
'use strict';

// 导入所需模块
const koa = require('koa');
const app = koa();
const logger = require('koa-logger');
const router = require('koa-route');
const parse = require('co-body');
const sleep = require('co-sleep');
const serve = require('koa-static');

app.use(logger());

app.use(serve(__dirname + '/public'));

app.use(router.get('/get', get));
app.use(router.post('/post', post));

function* get() {
  this.body = 'get';
}

function* post() {
  var body = yield parse.json(this);
  yield sleep(1000);
  this.body = body; 
}

app.use(function*() {
  this.body = 'Hello World';
});

app.listen(3000);
console.log('listening on port 3000');

```

```js
const bouncer = require('koa-bouncer');
app.use(bouncer.middleware());


const csrf = require('koa-csrf');
app.use(csrf());

```

```js
const compress = require('koa-compress');

app.use(compress({
  filter: function(content_type) {
    return /text/i.test(content_type)
  },
  threshold: 2048,
  flush: require('zlib').Z_SYNC_FLUSH
}));

```

```js
const koa = require('koa');
const send = require('koa-send');
const app = koa();

app.use(function*() {
  yield send(this, 'index.html');
});

app.listen(3000);
console.log('listening on port 3000');
```

```js
const mount = require('koa-mount');
const koa = require('koa');

function *hello(next){
  yield next;
  this.body = 'Hello';
}

function *world(next){
  yield next;
  this.body = 'World';
}

var app = koa();

app.use(mount('/hello', hello));
app.use(mount('/world', world));

app.listen(3000);
console.log('listening on port 3000');
```
#### :books: 參考網站：
- [koa-mount](https://github.com/koajs/mount)
- [koa-logger](https://www.npmjs.com/package/koa-logger)
- [koa-route](https://www.npmjs.com/package/koa-route)
- [koa-route](https://github.com/alexmingoia/koa-router)
- [co-body](https://www.npmjs.com/package/co-body)
- [co-sleep](https://www.npmjs.com/package/co-sleep)
- [koa-static](https://www.npmjs.com/package/koa-static)
- [koa-static](https://github.com/koajs/static)
- [koa-bouncer](https://github.com/danneu/koa-bouncer)
- [koa-send](https://github.com/koajs/send)

---
