
### 安裝 {#installing}

```
shell> npm install --save redis
```

```js
'use strict';

// 导入所需模块
const redis = require("redis");

// const client = redis.createClient();
const client = redis.createClient('6379', '127.0.0.1');

client.on("error", function (err) {
    console.log("Error " + err);
});

client.set("string key", "string val", redis.print);

```

```
Error: Redis connection to 127.0.0.1:6379 failed - connect ECONNREFUSED 127.0.0.1:6379
```

---

```
shell> npm install fast-redis-cluster2 --save
```

```js
'use strict';

// 导入所需模块
const redisCluser = require('fast-redis-cluster2').clusterClient;

var opts = {
    host: '127.0.0.1',
    port: 7001,
    // auth: 'topsecretpassword',
    // useFallbackDriver: true,
};

//var opts = '127.0.0.1:7001';

var redis = new redisCluser.clusterInstance(opts, function (err) {
    if (err) throw new Error(err);
    console.log('Connected, cluster is fine and ready for using');
});

redis.on('ready', function(){
    console.log('Connected, cluster is fine and ready for using');
});

redis.on('error', function(err){
    console.log('Redis error', err);
});

redis.set('foo', 'bar2', function(err, resp){
    console.log('set command returns err: %s, resp: %s', err, resp);
});

redis.set('foo', 'bar3');

redis.get('foo', function(err, resp){
    console.log('get foo command returns err: %s, resp: %s', err, resp);
});

```

---

```
shell> npm install fast-redis-cluster2 --save
```

```js
'use strict';

const Redis = require('ioredis');
const redis = new Redis();

redis.set('foo', 'bar');
redis.get('foo', function (err, result) {
  console.log(result);
});

// Or using a promise if the last argument isn't a function
redis.get('foo').then(function (result) {
  console.log(result);
});

// Arguments to commands are flattened, so the following are the same:
redis.sadd('set', 1, 3, 5, 7);
redis.sadd('set', [1, 3, 5, 7]);

// All arguments are passed directly to the redis server:
redis.set('key', 100, 'EX', 10);

```

```js
'use strict';

const Redis = require('ioredis');

var cluster = new Redis.Cluster([{
  port: 6380,
  host: '127.0.0.1'
}, {
  port: 6381,
  host: '127.0.0.1'
}]);

cluster.set('foo', 'bar');
cluster.get('foo', function (err, res) {
  // res === 'bar'
});
```

```js
'use strict';

const Redis = require('ioredis');

var nodes = [
{  port: 6380,  host: '127.0.0.1' },
{  port: 6381,  host: '127.0.0.1' }
];

var cluster = new Redis.Cluster(nodes);

cluster.set('foo', 'bar');
cluster.get('foo', function (err, res) {
  // res === 'bar'
});
```

#### :books: 參考網站：
- [redis](https://github.com/NodeRedis/node_redis)
- [fast-redis-cluster2](https://github.com/h0x91b/fast-redis-cluster)
- [ioredis](https://github.com/luin/ioredis)
