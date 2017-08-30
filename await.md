<img src="http://i.imgur.com/hiqEWWn.png" alt="ansible" width=200>

```js
function resolveAfter2Seconds(x) {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve(x);
    }, 2000);
  });
}

async function f1() {
  var x = await resolveAfter2Seconds(10);
  console.log(x); // 10
}
f1();
```

```js
(async () => {
  await new Promise(resolve => setTimeout(resolve, 2000));
  console.log('Done.');   
})();
```

```
shell> node-v7.6.0-linux-x64/bin/node main.js
```

---

```js
const request = require('request');

(async () => {
  await new Promise(resolve => {
    request('http://myip.dnsomatic.com/', function (error, response, body) {
      if (!error && response.statusCode == 200) {
        console.log(body);
      }
    })
  }
  console.log('Done.');   
})();
```


#### :books: 參考網站：
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await
