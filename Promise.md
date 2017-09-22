![](https://i.imgur.com/t1nmuUG.png)

`Promise` 物件

> 提供一個機制來排程對尚未計算的值進行的工作。它是管理與非同步 API 互動的抽象概念。

`語法`

```js
var promise = new Promise(function(resolve, reject) { ... });

promise.then(onCompleted, onRejected);
promise.catch(onRejected)

Promise.resolve(x)
Promise.reject(r);

```

`參數`

```
promise
必要項。要對其指派承諾的變數名稱。
resolve
必要項。執行以表示承諾已順利完成的函式。
reject
選擇項。執行以表示已拒絕承諾並發生錯誤的函式。

promise
必要項。Promise 物件
onCompleted
必要項。承諾順利完成時要執行的「履行」處理常式函式。
onRejected
選擇項。要在拒絕承諾時執行的錯誤處理常式函式。
```

`備註`

```
承諾必須完成並具有值，或必須有原因的拒絕。完成或拒絕 (視何者先發生) 承諾時，會執行 Promise 物件的 then 方法。如果承諾順利完成，則會執行 then 方法的履行處理常式函式。如果已拒絕承諾，則會執行 then 方法 (或 catch 方法) 的錯誤處理常式函式。
```

下列範例示範如何呼叫會傳回承諾的函式 (timeout)。在 5000 毫秒逾時到期之後，會執行 then 方法的履行處理常式。
```js
let timeout = duration => {
  // function timeout(duration) {
  return new Promise((resolve, reject) => {
    // return new Promise(function(resolve, reject) {
    setTimeout(resolve, duration);
  });
};

// Note: This code uses arrow function syntax
var m = timeout(5000).then(() => {
  console.log("done!");
});

// Output (after 5 seconds):
// done!
```

```js
let timeout = duration => {
  return new Promise((resolve, reject) => {
    setTimeout(reject, duration);
  });
};

var p = timeout(5000)
  .then(() => {
    console.log("done!");
  })
  .catch(err => {
    console.log("error!");
  });

// Output (after five seconds):
// error!
```

```js
var p = Promise.resolve("success");
p.then(result => {
  console.log(result);
});

// Output:
// success
```

```js
var p = Promise.reject("failure");
p.catch(result => {
  console.log(result);
});

// Output:
// failure
```

- `pending` `擱置中`: initial state, neither `fulfilled` nor `rejected`.
- `fulfilled` `已經完成`: meaning that the operation completed successfully.
- `rejected` `已拒絕`: meaning that the operation failed.

`resolve` `解析`

```js
const myFirstPromise = new Promise((resolve, reject) => {
  // do something asynchronous which eventually calls either:
  //
  //   resolve(someValue); // fulfilled
  // or
  //   reject("failure reason"); // rejected
});
```

```js
let myFirstPromise = new Promise((resolve, reject) => {
  setTimeout(function(){
    resolve("Success!");
  }, 250);
});

myFirstPromise.then((successMessage) => {
  console.log("Yay! " + successMessage);
});
```

---

```js
// var b = true;
var b = false;

var p1 = new Promise(function (resolve, reject) {
  if (b) {
    resolve('Success!');
  } else {
    reject(Error('oh, no!'));
  }
});

var myFunc = function() {
  p1.then(function(value){
    console.log(value);
  })
  .catch(function(e) {
    console.log(e);
  })
};

myFunc();
```

```js
var doSomething = function(value) {
  return new Promise(function (resolve, reject) {
    resolve('Success!');
  });
};
```

```js
var doSomething = function(value) {
  return Promise.resolve('Success!');
};
```

#### :books: 參考網站：
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all
- https://msdn.microsoft.com/zh-tw/library/dn802826(v=vs.94).aspx

---

```js
"use strict";

const promisify = require("es6-promisify");
const fs = require("fs");

const stat = promisify(fs.stat);

stat("example.txt")
  .then(stats => {
    console.log("Got stats", stats);
  })
  .catch(err => {
    console.error("Yikes!", err);
  });
```
#### :books: 參考網站：
- https://www.npmjs.com/package/es6-promisify
