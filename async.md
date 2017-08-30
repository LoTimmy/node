
```js
var async = require('async');
var myArray = [1, 2, 3];

async.map(myArray, myFunc, function(err, results){
  console.log(results);
});

function myFunc(num, callback) {
  setTimeout(function(){
    callback(null, num * 3);
  }, 200);
}
```

---

```js
var async = require('async');

async.parallel([
  function(callback){
    setTimeout(function(){
      callback(null, 'one');
    }, 200);
  },
  function(callback){
    setTimeout(function(){
      callback(null, 'two');
    }, 100);
  }
],
function(err, results){
  console.log(results); // → ['one','two']
});
```

```js
var async = require('async');

async.parallel({
  one: function(callback){
    setTimeout(function(){
      callback(null, 1);
    }, 200);
  },
  two: function(callback){
    setTimeout(function(){
      callback(null, 2);
    }, 100);
  }
},
function(err, results) {
  console.log(results); // → {one: 1, two: 2}
});
```

---

```js
var async = require('async');

var cargo = async.cargo(function (tasks, callback) {
  for(var i=0; i<tasks.length; i++){
    console.log('hello ' + tasks[i].name);
  }
  callback();
}, 1);

cargo.push({name: 'foo'}, function (err) {
  console.log('finished processing foo');
});
cargo.push({name: 'bar'}, function (err) {
  console.log('finished processing bar');
});
cargo.push({name: 'baz'}, function (err) {
  console.log('finished processing baz');
});
```

---

```js
var async = require('async');

var myArray = ['Abel', 'Brad', 'Clair', 'David', 'Eric'];

async.each(myArray, function(item, done) {
  console.log(item);
  done();    
}, function(err){
  console.log('完成');
});

/*
Abel
Brad
Clair
David
Eric
完成
*/
```

```js
var async = require('async');

var myArray = ['Abel', 'Brad', 'Clair', 'David', 'Eric'];

async.eachSeries(myArray, function(item, done) {
  console.log(item);
  done();    
}, function(err){
  console.log('完成');
});

/*
Abel
Brad
Clair
David
Eric
完成
*/
```

---

```js
var async = require('async');
async.eachSeries(hugeArray, function iterator(item, callback) {
  //...
  async.setImmediate(function () {
      callback();
  });
}, function done() {
  //...
});
```

---

```js
var async = require('async');

async.series([
  function(next){
    console.log('one');
    next();
  },
  function(next){
    setTimeout(function(){
      console.log('two');
      next();
    }, 1000);
  },
  function(next){
    console.log('three');
    next();
  }
],
function(err){
  console.log('完成');
});
```

---

```js
var async = require('async');

async.series([
  function(callback){
    // do some stuff ...
    callback(null, 'one');
  },
  function(callback){
    // do some more stuff ...
    callback(null, 'two');
  }
],
// optional callback
function(err, results){
  // results is now equal to ['one', 'two']
});
```

```js
var async = require('async');

async.series({
  one: function(callback){
    setTimeout(function(){
      callback(null, 1);
    }, 200);
  },
  two: function(callback){
    setTimeout(function(){
      callback(null, 2);
    }, 100);
  }
},
function(err, results) {
  // results is now equal to: {one: 1, two: 2}
});
```

---

```js
var async = require('async');

async.waterfall([
  function(callback) {
    callback(null, 'one', 'two');
  },
  function(arg1, arg2, callback) {
    // arg1 now equals 'one' and arg2 now equals 'two' 
    callback(null, 'three');
  },
  function(arg1, callback) {
    // arg1 now equals 'three' 
    callback(null, 'done');
  }
], function (err, result) {
  // result now equals 'done' 
});

```
---

#### :books: 參考網站：
- [async](https://www.npmjs.com/package/async)
