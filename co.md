`--harmony`
```
shell> node --v8-options | grep harmony
```
```
shell> node --harmony co.js
```

```
onerror
onclose
onopen
onmessage
```

---
```
shell> npm install co
shell> npm install co-fs
shell> npm install co-prompt

shell> npm install thunkify
```

---
```js
const co = require('co');

co(function *(){
  // resolve multiple promises in parallel 
  var a = Promise.resolve(1);
  var b = Promise.resolve(2);
  var c = Promise.resolve(3);
  var res = yield [a, b, c];
  console.log(res);  // => [1, 2, 3] 
}).catch(onerror);

co(function* () {
  return yield Promise.resolve(true);
}).then(function (val) {
  console.log(val);
}, function (err) {
  console.error(err.stack);
});

co(function* () {
  var res = yield [
    Promise.resolve(1),
    Promise.resolve(2),
    Promise.resolve(3),
  ];
  console.log(res); // => [1, 2, 3] 
}).catch(onerror);

co(function* () {
  var res = yield {
    1: Promise.resolve(1),
    2: Promise.resolve(2),
  };
  console.log(res); // => { 1: 1, 2: 2 } 
}).catch(onerror);

function onerror(err) {
  console.error(err.stack);
}
```

---

### thunkify

```js
function original(arguments, done) {
  // ...
  done(null, 'ok')
}

function thunkified(arguments) {
  return function(done) {
    original(arguments, done)
  }
}
```

```js
const thunkify = require('thunkify');
const fs = require('fs');

const readFile = thunkify(fs.readFile);
read('package.json', 'utf8')(function(err, str){
});
```

```js
const co = require('co');
const readFile = require('thunkify')(require('fs').readFile);

const sleep = require('thunkify')(function (ms, cb) {
  setTimeout(cb, ms);
});

co(function*() {
  yield sleep(3000);
  var packageData = JSON.parse(yield readFile('package.json', 'utf8'));
  console.log(packageData);
});
```

```js
const thunkify = require('thunkify');

var sleep = thunkify(function (ms, cb) {
  setTimeout(cb, ms);
});

console.log('sleep start...');
sleep(3000)(function () {
  console.log('3 seconds later...');
});
```

---
```js
const co = require('co');

function wait() {
  return new Promise( function (resolve, reject) {
    setTimeout(resolve, 1000);
  });
}

co(function* () {
  console.log("hello");
  yield wait();
  console.log("I am walking!");
  yield wait();
  console.log("goodBye");
}).catch(function(err){
  throw err;
});
```

---
```js
const arp = require('node-arp');
 
arp.getMAC('192.168.0.1', function(err, mac) {
  console.log(mac);
  arp.getMAC('192.168.0.2', function(err, mac) {
    console.log(mac);
  });    
});
```

```js
const arp = require('node-arp');

function getMAC(ipAddress) {
  return function(callback) {
    arp.getMAC(ipAddress, callback);
  }
}

getMAC('192.168.0.1')(function(err, mac){
  console.log(mac);
});
```

```js
const co = require('co');
const arp = require('node-arp');

function getMAC(ipAddress) {
  return function(callback) {
    arp.getMAC(ipAddress, callback);
  }
}

co(function* () {
  console.log( yield getMAC('192.168.42.1') );
}).catch(onerror);

function onerror(err) {
  console.error(err.stack);
}
```

```js
const co = require('co');
const arp = require('node-arp');
const thunkify = require('thunkify');

const getMAC=thunkify(arp.getMAC);

co(function* () {
  console.log( yield getMAC('192.168.42.1') );
}).catch(onerror);

function onerror(err) {
  console.error(err.stack);
}
```

---

```js
//  Created by Timmy on 2016/3/29.
//  Copyright (c) 2016年 Timmy. All rights reserved.
"use strict";

// 导入所需模块
const mysql = require('mysql');
const squel = require("squel");
const co = require('co');
const wrapper = require('co-mysql');

co(function*() {

  var pool = mysql.createPool({
    connectionLimit: 10,
    host: 'example.org',
    user: 'bob',
    password: 'secret'    
  });

  p = wrapper(pool);
  var rows = yield p.query('SELECT 1');
  console.log(rows);
  pool.end();

}).catch(onerror);

function onerror(err) {
  console.error(err.stack);
}
```


```js
//  Created by Timmy on 2016/3/29.
//  Copyright (c) 2016年 Timmy. All rights reserved.
"use strict";

// 导入所需模块
const co = require('co');
const sql = require('co-mssql');
const squel = require("squel");

co(function*() {

  var connection = new sql.Connection({
    user: '...',
    password: '...',
    server: 'localhost',
    database: '...'
  });

  // Query
  yield connection.connect();
  var request = new sql.Request(connection);
  var recordset = yield request.query('select 1 as number');
  console.dir(recordset);

  // Stored Procedure      
  var request = new sql.Request(connection);
  request.input('input_parameter', sql.Int, 10);
  request.output('output_parameter', sql.Int);
  var recordsets = yield request.execute('procedure_name');
  console.dir(recordsets);

});
```

```js
//  Created by Timmy on 2016/3/29.
//  Copyright (c) 2016年 Timmy. All rights reserved.
"use strict";

// 导入所需模块
let co = require("co");
let request = require("co-request");

```

#### :books: 參考網站：
- [co](https://www.npmjs.com/package/co)
- [node-thunkify](https://github.com/tj/node-thunkify)
- [thunkify](https://www.npmjs.com/package/thunkify)
- [co-mysql](https://www.npmjs.com/package/co-mysql)
- [co-mssql](https://www.npmjs.com/package/co-mssql)
- [co-fs](https://www.npmjs.com/package/co-fs)
- [co-prompt](https://www.npmjs.com/package/co-prompt)