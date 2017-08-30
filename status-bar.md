
```js
var path = require('path');
var http = require('http');
var statusBar = require('status-bar');
 
var url = 'http://nodejs.org/dist/latest/node.exe';
var bar;
 
http.get(url, function (res) {
  bar = statusBar.create({ total: res.headers['content-length'] })
      .on('render', function (stats) {
        process.stdout.write(
            path.basename(url) + ' ' +
            this.format.storage(stats.currentSize) + ' ' +
            this.format.speed(stats.speed) + ' ' +
            this.format.time(stats.elapsedTime) + ' ' +
            this.format.time(stats.remainingTime) + ' [' +
            this.format.progressBar(stats.percentage) + '] ' +
            this.format.percentage(stats.percentage));
        process.stdout.cursorTo(0);
      });
  
  res.pipe(bar);
}).on('error', function (err) {
  if (bar) bar.cancel();
  console.error(err);
});
 
/*
It will print something like this:
 
node.exe    2.8 MiB  617.5K/s 00:06 00:07 [############············]  51%
*/
```

```
http://cachefly.cachefly.net/100mb.test
http://cachefly.cachefly.net/10mb.test
```

#### :books: 參考網站：
- [status-bar](https://www.npmjs.com/package/status-bar)