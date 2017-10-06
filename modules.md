`模組` (`Module`)

`a.js`
```js
module.exports = function() {
  console.log('a starting');
}
```

`b.js`
```js
module.exports = function() {
  console.log('b starting');
}
```

`main.js`
```js
var a = require('./a.js');
var b = require('./b.js');
a();
b();
console.log('main starting');

/* ==>
a starting
b starting 
main starting
*/
```

---

`a.js`
```js
'use strict';

module.exports = function (callback) {
  setTimeout( function() {
    console.log('a starting');
    return callback();
  }, 3000 );
}
```

`b.js`
```js
'use strict';

module.exports = function (callback) {
  setTimeout( function() {
    console.log('b starting');
    return callback();
  }, 1000 );
}
```

```js
var a = require('./a.js');
var b = require('./b.js');

a(function() {
  b(function() {
    console.log('main starting');
  });
});

/* ==>
a starting
b starting 
main starting
*/

```
```js
var async = require('async');
var a = require('./a.js');
var b = require('./b.js');

async.series([
  function(next){
    a(function() {
      next();
    })
  },
  function(next){
    b(function() {
      next();
    })
  }
],
function(err){
  console.log('main starting');
});

/* ==>
a starting
b starting 
main starting
*/

```

```
/**
 *
 *
 */
@param {String} flags
@param {String} description
@param {Function|Mixed} fn or default
@param {Mixed} defaultValue
@param {Array} argv
@param {Number} width
@param {Object} arg
@param {Boolean} arg
@param {Function} fn

```

#### :books: 參考網站：
- [modules](https://nodejs.org/api/modules.html)

