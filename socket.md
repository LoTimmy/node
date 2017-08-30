```js
var net = require('net');
var server = net.createServer(function(c) { //'connection' listener
  c.on('data', function(data) {
    c.write(data + '\n');
  });
  c.on('end', function() {
    console.log('client disconnected');
  });
  c.write('hello\r\n');
});

server.listen(8124, function() { //'listening' listener
  console.log('server bound');
});

```

```
shell> telnet localhost 8124
```

```js
var net = require('net');
var client = net.connect({port: 8124}, function() { //'connect' listener
  console.log('connected to server!');
  client.write('world!\r\n');
});
client.on('data', function(data) {
  console.log(data.toString());
  client.end();
});
client.on('end', function() {
  console.log('disconnected from server');
});
```


```js
var net = require('net');

var HOST = '0.0.0.0';
var PORT = 8124;

var server = net.createServer(function(c) { //'connection' listener
  server.getConnections(function(err, count) {
    console.log(count);
  });

  c.on('data', function(data) {
    c.write(data + '\n');
  });

  c.on('end', function() {
    console.log('client disconnected');
    server.getConnections(function(err, count) {
      console.log(count);
    });
  });

  c.write('hello\r\n');
});

server.listen(PORT, HOST, function() { //'listening' listener
  address = server.address();
  console.log("opened server on %j", address);
});

server.on('error', function (e) {
  if (e.code == 'EADDRINUSE') {
    console.log('Address in use, retrying...');
    setTimeout(function () {
      server.close();
      server.listen(PORT, HOST);
    }, 1000);
  }
});

server.on('connection', function(socket) {
  console.log(socket.remoteAddress + ':' + socket.remotePort);
});
```


```js
var net = require('net');
var moment = require('moment');

var myarray = [];

var server = net.createServer(function(c) { //'connection' listener
  myarray.push(c);

  server.getConnections(function(err, count) {
    console.log(count);
  });

  c.write("歡迎!" + c.remoteAddress + ":" + c.remotePort + "\n");

  myarray.forEach(function(element, index) {
    element.write(c.remoteAddress + ":" + c.remotePort + "\n");
  });

  c.on('data', function(data) {
  //  c.write(data + '\n');
    myarray.forEach(function(element, index) {
      element.write(c.remoteAddress + ":" + c.remotePort + " >" + data + "\n");
    });
  });

  c.on('end', function() {
    console.log('client disconnected');
    server.getConnections(function(err, count) {
      console.log(count);
    });
  });
});

var HOST = '0.0.0.0';
var PORT = 8124;

server.listen(PORT, HOST, function() { //'listening' listener
  address = server.address();
  console.log("opened server on %j", address);
});

server.on('error', function (e) {
  if (e.code == 'EADDRINUSE') {
    console.log('Address in use, retrying...');
    setTimeout(function () {
      server.close();
      server.listen(PORT, HOST);
    }, 1000);
  }
});

server.on('connection', function(socket) {
  console.log(socket.remoteAddress + ':' + socket.remotePort);
});

```


```
 EADDRINUSE [address in use]
 ECONNREFUSED [connection refused]
 EHOSTUNREACH [host unreachable]

 address_in_use = EADDRINUSE,
 connection_refused = ECONNREFUSED,
 host_unreachable = EHOSTUNREACH,


 "Address already in use." = EADDRINUSE
 "位址已在使用中。" = EADDRINUSE   

 file_exists = EEXIST,
 file_too_large = EFBIG,
 filename_too_long = ENAMETOOLONG,
```

#### :books: 參考網站：
- [errno 常數](https://msdn.microsoft.com/zh-tw/library/5814770t.aspx)
- [errc](https://msdn.microsoft.com/zh-tw/library/vstudio/ee372239(v=vs.110).aspx)
- [net](https://nodejs.org/api/net.html)