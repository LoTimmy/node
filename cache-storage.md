### 安裝 {#installing}

```
shell> npm install cache-storage
```

```js
var http = require('http');
var publicIp = require('public-ip');

var Cache = require('cache-storage');
var FileStorage = require('cache-storage/Storage/FileSyncStorage');
var cache = new Cache(new FileStorage('./temp'), 'ipinfo');

publicIp(function (err, ip) {
    var myIP = ip;
    console.log(myIP);
    var data = cache.load(myIP);
    if (data === null) {
      var options = {
        hostname: 'ip-api.com',
        path: '/json/' + myIP
      };
      var req = http.request(options, function(res) {
        var str = '';
        res.on('data', function (chunk) {
          str += chunk;
        });
        res.on('end', function() {
          var jsonText = JSON.parse(str);
          data = cache.save(myIP, jsonText);
          console.log("cache.save");
          console.log(jsonText);
        });
      }).end();

    } else {
      console.log("cache.load");
      console.log(data);
    }

});
```

```js
var Cache = require('cache-storage');
var FileStorage = require('cache-storage/Storage/FileSyncStorage');
var cache = new Cache(new FileStorage('./temp'), 'ipinfo');

cache.clean('all');
```

#### :books: 參考網站：
- [cache-storage](https://www.npmjs.com/package/cache-storage)