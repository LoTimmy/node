![](http://kriskowal.github.io/q/q.png)

### 安裝 {#installing}

```
shell> npm install q
```

```js
var fs = require('fs');

fs.readFile('message.txt', 'utf8', function (err, data) {
  if (err) throw err;
  console.log(data);
});

console.log('Complete!');
```

```js
step1(function (value1) {
    step2(value1, function(value2) {
        step3(value2, function(value3) {
            step4(value3, function(value4) {
                // Do something with value4 
            });
        });
    });
});
```

```js
Q.fcall(promisedStep1)
.then(promisedStep2)
.then(promisedStep3)
.then(promisedStep4)
.then(function (value4) {
    // Do something with value4 
})
.catch(function (error) {
    // Handle any error from all above steps 
})
.done();
```

---
```js
var fs = require('fs');
var Q = require('q');

Q.nfcall(fs.readFile, 'message.txt', 'utf8')
  .then(function(data) { console.log(data); })
  .fail(function (error) { console.log(data); })
  .done();
```

```js
var Q = require('q');
Q('Complete!').then(console.log);
```

#### :books: 參考網站：
- [q](https://www.npmjs.com/package/q)
