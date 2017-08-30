![](http://zeromq.wdfiles.com/local--files/admin:css/logo.gif)

![](http://i.imgur.com/9qzI8QR.jpg)

ØMQ

```
shell> brew install pkg-config
shell> brew install zeromq
```

---

```
shell> apt-get install libtool autoconf automake uuid-dev build-essential pkg-config
shell> git clone https://github.com/zeromq/libzmq
shell> ./autogen.sh && ./configure && make -j 4
shell> make check && make install && sudo ldconfig
```

```
shell> npm install zmq
```

package.json

```json
{
  "name": "application-name",
  "version": "0.0.1",
  "private": true,
  "dependencies": {
    "zmq": "*"
  }
}
```

#### :books: 參考網站：

- [zguide](http://zguide.zeromq.org/page:all)
- [debian](http://zeromq.org/distro:debian)
- [download](http://zeromq.org/area:download)

---

```js:test.js
var socket = zmq.socket('rep');
var socket = zmq.socket('req');

var sock = zmq.socket('dealer');
var socket = zmq.socket('push');
var socket = zmq.socket('pull');

var pub = zmq.socket('pub');
var sub = zmq.socket('sub');

var frontend = zmq.socket('router');
var backend = zmq.socket('dealer');

var xpub = zmq.socket('xpub');
var xsub = zmq.socket('xsub');
```

```:test.js
socket.bind('tcp://*:5555', function(err) {
});

socket.connect("tcp://localhost:5555");

socket.close();
```

```js
sock.bindSync('tcp://127.0.0.1:3000');
```

```js
socket.bind('tcp://192.168.1.100:5555');
socket.bind('tcp://eth0:5555');
socket.bind('tcp://*:5555');
```

```js
socket.bind('ipc:///tmp/zmq.sock');
socket.bind('inproc://somename');
```

```js
socket.send('World');

socket.send('kitty cats', ZMQ_SNDMORE);
socket.send('meow!');

sock.send(['kitty cats', 'meow!']);

sock.on('message', function(topic, message) {
  console.log('received a message related to:', topic, 'containing message:', message);
});

```

```js
```

---

![](https://github.com/imatix/zguide/raw/master/images/fig2.png)

hwserver.js
```js
//  Created by Timmy on 2016/6/14.
//  Copyright (c) 2015年 Timmy. All rights reserved.

// 导入所需模块
const zmq = require('zmq');
const socket = zmq.socket('rep');

socket.on('message', function(request) {
  console.log("Received request: [", request.toString(), "]");
  setTimeout(function() {
    socket.send("World");
  }, 1000);
});

socket.bind('tcp://*:5555', function(err) {
  if (err) {
    console.log(err);
  } else {
    console.log("Listening on 5555…");
  }
});

process.on('SIGINT', function() {
  socket.close();
});
```

hwclient.js
```js
//  Created by Timmy on 2016/6/14.
//  Copyright (c) 2015年 Timmy. All rights reserved.

// 导入所需模块
const zmq = require('zmq');
const socket = zmq.socket('req');

console.log("Connecting to hello world server…");

var x = 0;
socket.on("message", function(reply) {
  console.log("Received reply", x, ": [", reply.toString(), ']');
  x += 1;
  if (x === 10) {
    socket.close();
    process.exit(0);
  }
});

socket.connect("tcp://localhost:5555");

for (var i = 0; i < 10; i++) {
  console.log("Sending request", i, '…');
  socket.send("Hello");
}

process.on('SIGINT', function() {
  socket.close();
});
```

hwserver.c
```c
#include <zmq.h>
#include <stdio.h>
#include <unistd.h>
#include <string.h>
#include <assert.h>

int main (void)
{
    //  Socket to talk to clients
    void *context = zmq_ctx_new ();
    void *responder = zmq_socket (context, ZMQ_REP);
    int rc = zmq_bind (responder, "tcp://*:5555");
    assert (rc == 0);

    while (1) {
        char buffer [10];
        zmq_recv (responder, buffer, 10, 0);
        printf ("Received Hello\n");
        sleep (1);          //  Do some 'work'
        zmq_send (responder, "World", 5, 0);
    }
    return 0;
}
```

```
shell> gcc -o hwserver hwserver.c -lzmq
```

#### :books: 參考網站：
- [hwserver](http://zguide.zeromq.org/js:hwserver)
- [hwclient](http://zguide.zeromq.org/js:hwclient)

---

Push/Pull

producer.js
```js
//  Created by Timmy on 2016/6/14.
//  Copyright (c) 2015年 Timmy. All rights reserved.

// 导入所需模块
const zmq = require('zmq');
const sock = zmq.socket('push');

sock.bindSync('tcp://127.0.0.1:3000');
console.log('Producer bound to port 3000');
 
setInterval(function(){
  console.log('sending work');
  sock.send('some work');
}, 500);

process.on('SIGINT', function() {
  sock.close();
});
```

worker.js
```js
//  Created by Timmy on 2016/6/14.
//  Copyright (c) 2015年 Timmy. All rights reserved.

// 导入所需模块
const zmq = require('zmq');
const sock = zmq.socket('pull');

sock.connect('tcp://127.0.0.1:3000');
console.log('Worker connected to port 3000');
 
setInterval(function(){
  console.log('sending a multipart message envelope');
  sock.send(['kitty cats', 'meow!']);
}, 500);


process.on('SIGINT', function() {
  sock.close();
});
```

---

```js
//  Created by Timmy on 2016/6/14.
//  Copyright (c) 2015年 Timmy. All rights reserved.

// 导入所需模块
const zmq = require('zmq');
const pub = zmq.socket('pub');
const sub = zmq.socket('sub');

pub.bindSync('tcp://127.0.0.1:5555');
pub.bindSync('ipc:///tmp/zmq.sock');

setInterval(function(){
  pub.send('some work');
}, 500);

sub.connect('ipc:///tmp/zmq.sock');
sub.subscribe('');
sub.on('message', function(msg){
  console.log(msg.toString());
});

process.on('SIGINT', function() {
  pub.close();
});
```


```js
//  Created by Timmy on 2016/6/14.
//  Copyright (c) 2015年 Timmy. All rights reserved.

// 导入所需模块
const zmq = require('zmq');
const sub = zmq.socket('sub');

sub.connect('tcp://127.0.0.1:5555');
sub.subscribe('');
sub.on('message', function(msg){
  console.log(msg.toString());
});

process.on('SIGINT', function() {
  sub.close();
});
```


---



shell> pm2 ping                      # Ensure pm2 daemon has been launched
{ msg: 'pong' }




---

rpc.js

```js
/**
 * One server two clients
 */

const cluster = require('cluster');
const zmq = require('zmq');
var port = 'tcp://127.0.0.1:12345';

if (cluster.isMaster) {
  for (var i = 0; i < 2; i++) cluster.fork();
} else {
  var sock = zmq.socket('dealer');
  sock.connect(port);
}
```

---

#### :books: 參考網站：
- [zmq-soa](https://github.com/Casear/zmq-soa)	
- [ZMQ 的安全與架構 in Node.js](http://www.ithome.com.tw/video/102916)
- [protobufjs](https://www.npmjs.com/package/protobufjs)
- [protocol-buffers](https://www.npmjs.com/package/protocol-buffers)

test.proto
```
enum FOO {
  BAR = 1;
}
 
message Test {
  required float num  = 1;
  required string payload = 2;
}
 
message AnotherOne {
  repeated FOO list = 1;
}
```

```js
const protobuf = require('protocol-buffers');
const fs = require('fs');

var messages = protobuf(fs.readFileSync('test.proto'));

var buf = messages.Test.encode({
  num: 42,
  payload: 'hello world'
});

console.log(buf);

var obj = messages.Test.decode(buf);
console.log(obj);
```


```js
const ProtoBuf = require('protobufjs');
var messages = ProtoBuf.loadProtoFile('test.proto');

```


```js
const Buffer = require('buffer').Buffer;
const zlib = require('zlib');
const thunkify = require('thunkify');
const co = require('co');

var deflate = thunkify(zlib.deflate);
var unzip = thunkify(zlib.unzip);

co(function*() {
  var input = new Buffer('lorem ipsum dolor sit amet');
  var compressed = yield deflate(input);
  var output = yield unzip(compressed);
  console.log(compressed.toString('base64'));
//  console.log(compressed);
  console.log(output.toString());
//  console.log(output);
});

```

#### :books: 參考網站：
- [zlib](https://nodejs.org/api/zlib.html)
