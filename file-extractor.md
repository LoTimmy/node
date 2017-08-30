`extract.js`
```js
#!/usr/bin/env node
var extractor = require('file-extractor');
var fs = require('fs');

var s = fs.createReadStream(__dirname + '/sample.csv',{});
var regex1 = //;
var regex2 = //;
var regex3 = //;
extractor()
  .matches(regex1,function(m){
    console.log(m);
  })
  .matches(regex2,function(m){
    console.log(m);
  })
  .matches(regex3,function(m){
    console.log(m);
  }).on('end',function(){
    console.log('');
  }).start(s);

```

```js
var extractor = require('file-extractor');

extractor()
  .matches(/regex1/, cb1)
  .matches(/regex2/, cb2)
  .matches(/regex3/, cb3).watch('/var/log/*.log');
```

```js
var readLine = require('lei-stream').readLine;
 
readLine('./myfile.txt').go(function (data, next) {
  console.log(data);
  next();
}, function () {
  console.log('end');
});
```
```js
var fs = require('fs');
var readLine = require('lei-stream').readLine;
 
// readLineStream第一个参数为ReadStream实例，也可以为文件名 
var s = readLine(fs.createReadStream('./myfile.txt'), {
  // 换行符，默认\n 
  newline: '\n',
  // 是否自动读取下一行，默认false 
  autoNext: false,
  // 编码器，可以为函数或字符串（内置编码器：json，base64），默认null 
  encoding: function (data) {
    return JSON.parse(data);
  }
});
 
// 读取到一行数据时触发data事件 
s.on('data', function (data) {
  console.log(data);
  s.next();
});
 
// 流结束时触发end事件 
s.on('end', function () {
  console.log('end');
});
```

#### :books: 參考網站：
- [file-extractor](https://www.npmjs.com/package/file-extractor)
- [file-extractor](https://github.com/jcreigno/nodejs-file-extractor)
- [lei-stream](https://www.npmjs.com/package/lei-stream)