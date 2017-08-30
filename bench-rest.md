
```
shell> npm install bench-rest
```

```js
var benchrest = require('bench-rest');

var flow = 'http://localhost:8000/';  // can use as simple single GET 

var flow = {
    main: [
      { post: 'http://localhost:8000/foo', headers: { 'Content-Type': 'application/json'}, body: '' },
      { get: 'http://localhost:8000/foo' }
    ]
  };

var runOptions = {
    limit: 10,     // concurrent connections 
    iterations: 100  // number of iterations to perform 
  };
  benchrest(flow, runOptions)
    .on('error', function (err, ctxName) { console.error('Failed in %s with err: ', ctxName, err); })
    .on('end', function (stats, errorCount) {
      console.log('error count: ', errorCount);
      console.log('stats', stats);
    });
```


```
net.ipv4.tcp_syncookies = 1
net.ipv4.tcp_tw_reuse = 1
net.ipv4.tcp_tw_recycle = 1
```

```
ulimit -n 63536
```

#### :books: 參考網站：
- [bench-rest](https://www.npmjs.com/package/bench-rest)
