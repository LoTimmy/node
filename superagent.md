### 安裝 {#installing}

```
shell> npm install superagent
```

```js
const request = require('superagent');

 request
   .get('/search')
   .end(function(err, res){

   });
```

```js
 request.post('/user')
   .set('Content-Type', 'application/json')
```


```js
const request = require('superagent');

request
   .post('/api/pet')
   .send({ name: 'Manny', species: 'cat' })
   .set('X-API-Key', 'foobar')
   .set('Accept', 'application/json')
   .end(function(err, res){
     if (err || !res.ok) {
       alert('Oh no! error');
     } else {
       alert('yay got ' + JSON.stringify(res.body));
     }
   });
```

```js
const request = require('superagent');

async function f1() {
  var x = await request('http://myip.dnsomatic.com/');
  return x;
}

async function f2() {
  var res = await f1();
  console.log(res.status);
  console.log(res.text);
}

f2();
```




```
var request = require('superagent');

async function getRequest() {
	let body = await request('http://www.google.com');
	return body;
}

async function run() {
	let result = await getRequest();
	console.log(result.text);
}

run();
```





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
- https://www.npmjs.com/package/superagent
- https://github.com/visionmedia/superagent
- http://visionmedia.github.io/superagent/



