
![](http://i.imgur.com/ZagBbq3.jpg)
![](http://i.imgur.com/K6LPzRw.png)

`1MB`
```
shell> openssl rand -out hello.txt -base64 $(( 2**20 ))
```

`1GB`
```
shell> openssl rand -out hello.txt -base64 $(( 2**30 ))
```

```js
const fs = require('fs');

var inp = fs.createReadStream('hello.txt');
var out = fs.createWriteStream('world.txt');
inp.pipe(out);
inp.pipe(process.stdout);
```

```js
const fs = require('fs');
var zlib = require('zlib');

var inp = fs.createReadStream('file.txt');
var gzip = zlib.createGzip();
var out = fs.createWriteStream('file.txt.gz');
inp.pipe(gzip).pipe(out);
```

```js
process.stdin.pipe(process.stdout);
```

```js
const fs = require('fs');

var file = fs.createWriteStream('example.txt');
file.write('hello, ');
file.end('world!');
```

---

```js
const fs = require('fs');

var ReadStream = fs.createReadStream('hello.txt', { flags: 'r', autoClose: true, highWaterMark: 1024 * 16 });
var WriteStream = fs.createWriteStream('world.txt', { flags: 'w' });

var myArray = [];
var x = new Boolean(false);


// ReadStream.on('data', (chunk) => {
ReadStream.on('data', function (chunk) {
  myArray.push(chunk);
  ReadStream.pause();
/*
  setTimeout(() => {
    ReadStream.resume();
  }, 100);
*/
  setTimeout(function(){
    ReadStream.resume();
  }, 100);

});

ReadStream.on('end', function () {
  x = true;
  console.log('Done.');

});

var timer = setInterval(function () {

  if (0 < myArray.length) {
      WriteStream.write(myArray.shift()); 
  } else {
    if (x) {
      clearInterval(timer);
      console.log('Done.');
    }
  }
}, 500);
```

#### :books: 參考網站：
- [stream](https://nodejs.org/api/stream.html)

---

```js
var Readable = require('stream').Readable;

var rs = new Readable;
rs.push('beep ');
rs.push('boop\n');
rs.push(null);

rs.pipe(process.stdout);
```

---

```js
process.stdin.on('data', function (buf) {
    console.log(buf);
});
process.stdin.on('end', function () {
    console.log('__END__');
});
```

```
shell> (echo beep; sleep 1; echo boop) | node app.js 
```

```
<Buffer 62 65 65 70 0a>
<Buffer 62 6f 6f 70 0a>
__END__
```

---

```js
var through = require('through2');
var fs = require('fs');
var stream = through(write, end);

function write(chunk, enc, callback) {
  this.push(chunk.toString().toUpperCase());
  callback();
}

function end (callback) {
  callback();
}

var readable = fs.createReadStream('hello.txt');
readable.pipe(stream).pipe(process.stdout);

// process.stdin.pipe(stream).pipe(process.stdout);
```

---
```js
const buf1 = Buffer.alloc(10);
const buf2 = Buffer.alloc(10, 1);
const buf3 = Buffer.allocUnsafe(10);
const buf4 = Buffer.from([1,2,3]);
const buf5 = Buffer.from('test');
const buf6 = Buffer.from('tést', 'utf8');

const buf = Buffer.from('hello world', 'ascii');
console.log(buf.toString('hex'));
console.log(buf.toString('base64'));

const str = '\u00bd + \u00bc = \u00be';
const str = "Node.js";

```

#### :books: 參考網站：

- [stream](https://nodejs.org/api/stream.html)
- [fs](https://nodejs.org/api/fs.html)
- [zlib](https://nodejs.org/api/zlib.html)
- [stream-handbook](https://github.com/substack/stream-handbook)
- [stream-handbook](https://github.com/jabez128/stream-handbook)