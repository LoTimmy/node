
![](http://i.imgur.com/KmXqk6Y.gif)

### 安裝 {#installing}

```
shell> npm install websocket
```

```js
var WebSocketServer = require('websocket').server;
var WebSocketClient = require('websocket').client;
var WebSocketFrame  = require('websocket').frame;
var WebSocketRouter = require('websocket').router;
var W3CWebSocket = require('websocket').w3cwebsocket;
```

```js
//  Created by Timmy on 2016/06/30.
//  Copyright (c) 2015年 Timmy. All rights reserved.
'use strict';

// 导入所需模块
const WebSocketServer = require('websocket').server;
const http = require('http');
 
var server = http.createServer(function(request, response) {
  console.log((new Date()) + ' Received request for ' + request.url);
  response.writeHead(404);
  response.end();
});

server.listen(8080, function() {
  console.log((new Date()) + ' Server is listening on port 8080');
});

wsServer = new WebSocketServer({
  httpServer: server,
  autoAcceptConnections: false
});

wsServer.on('request', function(request) {
  var connection = request.accept('echo-protocol', request.origin);
  console.log((new Date()) + ' Connection accepted.');
  connection.on('message', function(message) {
    if (message.type === 'utf8') {
      console.log('Received Message: ' + message.utf8Data);
      connection.sendUTF(message.utf8Data);
    }
    else if (message.type === 'binary') {
      console.log('Received Binary Message of ' + message.binaryData.length + ' bytes');
      connection.sendBytes(message.binaryData);
    }
  });
  connection.on('close', function(reasonCode, description) {
    console.log((new Date()) + ' Peer ' + connection.remoteAddress + ' disconnected.');
  });
});

```


```js
//  Created by Timmy on 2016/06/30.
//  Copyright (c) 2015年 Timmy. All rights reserved.
'use strict';

// 导入所需模块
var WebSocketClient = require('websocket').client;
 
var client = new WebSocketClient();
 
client.on('connectFailed', function(error) {
  console.log('Connect Error: ' + error.toString());
});
 
client.on('connect', function(connection) {
  console.log('WebSocket Client Connected');

  connection.on('error', function(error) {
    console.log("Connection Error: " + error.toString());
  });

  connection.on('close', function() {
    console.log('echo-protocol Connection Closed');
  });

  connection.on('message', function(message) {
    if (message.type === 'utf8') {
      console.log("Received: '" + message.utf8Data + "'");
    }
  });
    
  function sendNumber() {
    if (connection.connected) {
      var number = Math.round(Math.random() * 0xFFFFFF);
      connection.sendUTF(number.toString());
      setTimeout(sendNumber, 1000);
    }
  }
  sendNumber();
});
 
client.connect('ws://localhost:8080/', 'echo-protocol');

```

```html
<!DOCTYPE html>
<meta charset="utf-8" />
<title>WebSocket Test</title>
<script language="javascript" type="text/javascript">

  function init() {
    var wsUri = "ws://172.16.7.103:8080/";
    var websocket = new WebSocket(wsUri, 'echo-protocol');

    websocket.onmessage = function(evt) {
      console.log('RESPONSE: ' + evt.data);
    };

    websocket.onopen = function(evt) {
      console.log('CONNECTED');
      websocket.send('message');
    };

    websocket.onclose = function(evt) {
      console.log("DISCONNECTED");
    };

    websocket.onerror = function(evt) {
      console.log('ERROR: ' + evt.data);
    };
  }

  window.addEventListener("load", init, false);

</script>

<h2>WebSocket Test</h2>
  
```

```js
//  Created by Timmy on 2016/07/07.
//  Copyright (c) 2015年 Timmy. All rights reserved.
'use strict';

// 导入所需模块
const http = require('http');
const fs = require('fs');

fs.readFile('websocket.html', (err, data) => {
  if (err) throw err;

  // Create an HTTP server
  http.createServer( (req, res) => {
    res.writeHead(200, {'Content-Type': 'text/html'});
    res.write(data);
    res.end();
  }).listen(8000);

});
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>load demo</title>
  <style>
  body {
    font-size: 12px;
    font-family: Arial;
  }
  </style>
  <script src="https://code.jquery.com/jquery-1.10.2.js"></script>
  <script language="javascript" type="text/javascript">
    var host = "172.16.7.103";
    var port = 7379;
  
    function init() {
      if(typeof(WebSocket) == 'function') f = WebSocket;
      if(typeof(MozWebSocket) == 'function') f = MozWebSocket;
  
      var wsUri = "ws://"+host+":"+port+"/.json";
      var websocket = new f(wsUri);
  
      websocket.onmessage = function(evt) {
        console.log('RESPONSE: ' + evt.data);
        $( "p" ).text( 'RESPONSE: ' + evt.data );
      };
  
      websocket.onopen = function(evt) {
        console.log('CONNECTED');
  
  // websocket.send(JSON.stringify(["SET", "hello", "world"]));
  // websocket.send(JSON.stringify(["GET", "hello"]));
  
        websocket.send(JSON.stringify(["SUBSCRIBE", "second"]));
  
      };
  
      websocket.onclose = function(evt) {
        console.log("DISCONNECTED");
      };
  
      websocket.onerror = function(evt) {
        console.log('ERROR: ' + evt.data);
      };
    }
  
    window.addEventListener("load", init, false);
  </script>
</head>

<h2>WebSocket Test</h2>
<p></p>
  
```

#### :books: 參考網站：
- [websocket](https://www.npmjs.com/package/websocket)
- [Writing_WebSocket_client_applications](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API/Writing_WebSocket_client_applications)
- [echo](http://www.websocket.org/echo.html)