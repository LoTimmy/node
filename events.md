
`a.js`
```js
var EventEmitter = require('events').EventEmitter;
module.exports = new EventEmitter();

setTimeout(function() {
  module.exports.emit('ready');
}, 5000);
```

`b.js`
```js
var EventEmitter = require('events').EventEmitter;
module.exports = new EventEmitter();

setTimeout(function() {
  module.exports.emit('ready');
}, 1000);
```

`main.js`
```js
var a = require('./a');
a.on('ready', function() {
  console.log('module a is ready');
});
```

```js
var EventEmitter = require('events').EventEmitter;
var ee = new EventEmitter();

ee.on('message', function (msg) {
    console.log(msg);
});

ee.emit('message', 'hello, world!');

ee.one('myevent', function () {
  console.log('myevent')
});
ee.emit('myevent');


ee.on('myevent1', function () {
    console.log('myevent1')
});
ee.on('myevent2', function () {
    console.log('myevent2')
});

ee.emit('myevent1');
ee.emit('myevent2');

```

```js
'use strict';
var EventEmitter = require('events');
var ee = new EventEmitter();

ee.on('message', function (msg) {
    console.log(msg);
});

ee.emit('message', 'hello, world!');

```

#### :books: 參考網站：
- [events](https://nodejs.org/api/events.html)
- [nodejs](https://nodejs.org/api/all.html)

