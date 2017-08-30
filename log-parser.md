
```js
var extractor = require('file-extractor');
var fs = require('fs');
var async = require('async');
var glob = require("glob");
var squel = require("squel").useFlavour('mysql');
var mysql = require('mysql');

var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'me',
  password : 'secret',
  database : 'my_db'
});
 
connection.connect();

var regex1 = //;
/*
var regex2 = //;
var regex3 = //;
*/

glob(__dirname + '*.log', '', function (er, files) {
  async.eachSeries(files, function iterator(file, callback) {
    var s = fs.createReadStream(file, {});

    extractor()
      .matches(regex1, function(m) {
        var sqlString = squel.insert()
          .into("test")
          .set("f1", m[1])
          .set("f2", m[2])
          .toString()
        // console.log(sqlString);
        connection.query(sqlString, function (err) {
          if (err) throw err;
        });
      })
/*
      .matches(regex2, function(m) {
      })
      .matches(regex3, function(m) {
      })
*/
      .on('end', function(){
        async.setImmediate(function () {
          callback();
        });
      }).start(s);

  }, function done() {
    console.log('完成');
    connection.end();
  });
});
```

```js
var fs = require('fs');

fs.createReadStream(file, {encoding: 'utf8'})
  .on("data", function(data){
    
    var re = /(.*)\n(.*))/m;
    var found = data.match(re);

    // console.log(found);
    console.log(found[1]);
  })
  .on("end", function(){
    console.log("完成");
  });

```

```js
var fs = require('fs');
var glob = require("glob");
var async = require('async');
var squel = require("squel").useFlavour('mysql');
var mysql = require('mysql');

var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'me',
  password : 'secret',
  database : 'my_db'
});
 
connection.connect();

glob(__dirname + '*.log', '', function (er, files) {
  async.eachSeries(files, function iterator(file, callback) {
    fs.createReadStream(file, {encoding: 'utf8'})
      .on("data", function(data){

        var re = /(.*)\n(.*))/m;
        var found = data.match(re);
        if (found !== null) {
          var sqlString = squel.insert()
            .into("test")
            .set("f1", found[1])
            .set("f2", found[2])
            .toString()
          // console.log(sqlString);
          connection.query(sqlString, function (err) {
            if (err) throw err;
          });
        }
/*        
        if (found === null) {
        } else {
          var sqlString = squel.insert()
            .into("test")
            .set("f1", found[1])
            .set("f2", found[2])
            .toString()
          // console.log(sqlString);
          connection.query(sqlString, function (err) {
            if (err) throw err;
          });
        }
*/
      })
      .on("end", function(){
        async.setImmediate(function () {
          callback();
        });
      });
  }, function done() {
    console.log('完成');
    connection.end();
  });
});

```

```js
var split = require('split');
var glob = require("glob");
var files = glob.GlobSync(__dirname + '*.log').found;
var mysql = require('mysql');

var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'me',
  password : 'secret',
  database : 'my_db'
});
 
connection.connect();

async.eachSeries(files, function iterator(file, callback) {

  fs.createReadStream(file, {encoding: 'utf8'})
    .pipe(split(/(\r?\n){2}/))
    .on("data", function(data){
      var re = /(.*)\n(.*))/m;
      var found = data.match(re);
      if (found !== null) {
        var sqlString = squel.insert()
          .into("test")
          .set("f1", found[1])
          .set("f2", found[2])
          .toString()
        // console.log(sqlString);
        connection.query(sqlString, function (err) {
          if (err) throw err;
        });
    })
    .on("end", function(){
      async.setImmediate(function () {
        callback();
      });
    });

}, function done() {
  console.log('完成');
  connection.end();
});

```

```js
var glob = require("glob");
var files = glob.GlobSync(__dirname + '*.log').found;

files.forEach(function(element, index) {
  console.log('a[' + index + '] = ' + element);
});
```

---

#### :books: 參考網站：
- [async](https://www.npmjs.com/package/async)
- [file-extractor](https://www.npmjs.com/package/file-extractor)
- [glob](https://www.npmjs.com/package/glob)
- [squel](https://www.npmjs.com/package/squel)
- [node-byline](https://github.com/jahewson/node-byline)
- [fs-finder](https://www.npmjs.com/package/fs-finder)
- [event-stream](https://www.npmjs.com/package/event-stream)
- [split](https://www.npmjs.com/package/split)