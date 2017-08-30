![](http://i.imgur.com/6Jhn7qF.png)

![](https://github.com/NetEase/pomelo/wiki/images/webGameComp.png)
![](https://github.com/NetEase/pomelo/wiki/images/mmo-arch.png)
![](https://camo.githubusercontent.com/65e8947a811a64612b253fe9411a3b7c96aa0615/687474703a2f2f706f6d656c6f2e6e6574656173652e636f6d2f7265736f757263652f646f63756d656e74496d6167652f6c6f72646f66706f6d656c6f2f736572766572732e706e67)
![](http://i.imgur.com/QD7ajEX.png)

```
shell> apt-get install build-essential
shell> npm config set unsafe-perm true 
shell> npm install pomelo -g
```

```
shell> pomelo --help
shell> pomelo --version
```

```
shell> pomelo init ./HelloWorld
shell> cd HelloWorld
shell> sh npm-install.sh
```

```
shell> cd game-server
shell> pomelo start

shell> cd web-server
shell> node app
```

```
shell> cd game-server
shell> pomelo list
```

```
try to connect 127.0.0.1:3005
serverId           serverType pid  rss(M) heapTotal(M) heapUsed(M) uptime(m) 
connector-server-1 connector  2646 38.00  19.87        17.92       15.90     
master-server-1    master     2637 27.62  14.95        13.32       15.90     
```

```
shell> pomelo stop
shell> pomelo kill
```

```
HelloWorld/
├── game-server
│   ├── app
│   │   └── servers
│   │       └── connector
│   │           └── handler
│   │               └── entryHandler.js
│   ├── app.js
│   ├── app.js.mqtt
│   ├── app.js.sio
│   ├── app.js.sio.wss
│   ├── app.js.udp
│   ├── app.js.wss
│   ├── config
│   │   ├── adminServer.json
│   │   ├── adminUser.json
│   │   ├── clientProtos.json
│   │   ├── dictionary.json
│   │   ├── log4js.json
│   │   ├── master.json
│   │   ├── serverProtos.json
│   │   └── servers.json
│   ├── logs
│   └── package.json
├── npm-install.bat
├── npm-install.sh
├── shared
│   ├── server.crt
│   └── server.key
└── web-server
    ├── app.js
    ├── app.js.https
    ├── bin
    │   ├── component.bat
    │   └── component.sh
    ├── package.json
    └── public
        ├── css
        │   └── base.css
        ├── image
        │   ├── logo.png
        │   └── sp.png
        ├── index.html
        ├── index.html.sio
        └── js
            └── lib
                ├── build
                │   ├── build.js
                │   └── build.js.wss
                ├── component.json
                ├── local
                │   └── boot
                │       ├── component.json
                │       └── index.js
                ├── pomeloclient.js
                ├── pomeloclient.js.wss
                └── socket.io.js

18 directories, 38 files
```


```
shell> cd HelloWorld
shell> sh npm-install.sh
```

---

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>Pomelo</title>
    <meta http-equiv="content-type" content="text/html;charset=utf-8" />
    <meta http-equiv="content-style-type" content="text/css" />
    <meta http-equiv="content-scripte-type" content="text/javascript" />
    <link type="text/css" rel="stylesheet" href="css/base.css" />
    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1q8mTJOASx8j1Au+a5WDVnPi2lkFfwwEAa8hDDdjZlpLegxhjVME1fgjWPGmkzs7" crossorigin="anonymous">
    <script src="js/lib/build/build.js" type="text/javascript"></script>
    <script type="text/javascript">
      require('boot');
    </script> 
    <script type="text/javascript">
      var pomelo = window.pomelo;
      var host = "172.16.7.103";
      var port = "3010";
      function show() {
        pomelo.init({
          host: host,
          port: port,
          log: true
        }, function() {
        pomelo.request("connector.entryHandler.entry", "hello pomelo", function(data) {
            alert(data.msg);
          });
        });
      }
    </script>
  </head>
  <body>
      <div class="g-button">
        <input id="test" type="button" value="Test Game Server" onclick="show()"/>
      </div>
  </body>
</html>
```


```html
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8" />
  <title>
    Pomelo
  </title>
  <meta http-equiv="content-type" content="text/html;charset=utf-8" />
  <meta http-equiv="content-style-type" content="text/css" />
  <meta http-equiv="content-scripte-type" content="text/javascript" />
  <meta name="author" content="netease" />
  <meta name="version" content="1.0" />
  <meta name="keywords" content="pomelo" />
  <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1q8mTJOASx8j1Au+a5WDVnPi2lkFfwwEAa8hDDdjZlpLegxhjVME1fgjWPGmkzs7" crossorigin="anonymous">
  <script src="js/lib/build/build.js" type="text/javascript"></script>
  <script type="text/javascript">
    require('boot');
  </script>
  <script type="text/javascript">
    var pomelo = window.pomelo;
    var host = "172.16.7.103";
    // var port = "3010";
    var port = "3014";

    function show() {
      pomelo.init({
        host: host,
        port: port,
        log: true
      }, function () {
        /*
                pomelo.request("connector.entryHandler.entry", "hello pomelo", function(data) {
                    alert(data.msg);
                  });
                pomelo.request("connector.entryHandler.hello", "hello ", function(data) {
                    alert(data.msg);
                  });
        */
        pomelo.request("gate.gateHandler.queryEntry", "hello ", function (data) {
          alert(data.port);
          console.dir(data.msg);
        });
      });
    }
  </script>
</head>

<body>
  <div class="container">
    <p>
    </p>
    <p>
      <button class="btn btn-default" type="submit" onclick="show()">Test Game Server</button>
    </p>
  </div>
</body>

</html>
```

---

`connector.entryHandler.entry` → `app/servers/connector/handler/entryHandler.js`

```js
Handler.prototype.entry = function(msg, session, next) {
  next(null, {code: 200, msg: 'game server is ok.'});
};
```

```js
Handler.prototype.hello = function(msg, session, next) {
  console.log(msg);
  console.log(session);
  next(null, {code: 200, msg: 'Hello World!'});
};
```

```js
pomelo.request("connector.entryHandler.hello", "hello pomelo", function(data) {
            alert(data.msg);
          });
```

---

`gate.gateHandler.queryEntry` → app/servers/gate/handler/gateHandler.js

```js
module.exports = function(app) {
  return new Handler(app);
};

var Handler = function(app) {
  this.app = app;
};

Handler.prototype.queryEntry = function(msg, session, next) {

  var connectors = this.app.getServersByType('connector');
  var port = connectors[0].clientPort;
  var host = connectors[0].host;
  var length = connectors.length;

  // next(null, {code: 200, msg: connectors});
  next(null, { code: 200, host: host, port: port, msg: length });
};

```

---

`game-server/config/servers.json`

```json
{
  "development": {
    "connector": [
      { "id": "connector-server-1", "host": "172.16.7.103", "port": 3150, "clientPort": 3010, "frontend": true },
      { "id": "connector-server-2", "host": "172.16.7.103", "port": 3151, "clientPort": 3011, "frontend": true },
      { "id": "connector-server-3", "host": "172.16.7.103", "port": 3152, "clientPort": 3012, "frontend": true },
      { "id": "connector-server-4", "host": "172.16.7.103", "port": 3153, "clientPort": 3013, "frontend": true }
    ],
    "gate": [
      { "id": "gate-server-1", "host": "127.0.0.1", "clientPort": 3014, "frontend": true }
    ]
  },
  "production": {
    "connector": [
      { "id": "connector-server-1", "host": "127.0.0.1", "port": 3150, "clientHost": "172.16.7.103", "clientPort": 3010, "frontend": true }
    ],
    "gate": [
      { "id": "gate-server-1", "host": "127.0.0.1", "clientPort": 3014, "frontend": true }
    ]
  }
}
```

---

> 中國知名入口網站暨遊戲及網路服務供應商`網易` (`NetEase`)
> `網易`在中國提供了各種的網路服務，從入口網站、搜尋引擎、網路遊戲、電子郵件、電子商務、部落格到社交平台

---
#### :books: 參考網站：
- [pomelo](https://www.npmjs.com/package/pomelo)
- [HelloWorld](https://github.com/NetEase/pomelo/wiki/pomelo%E7%9A%84HelloWorld)
- [npm](https://docs.npmjs.com/misc/config)
- [LordOfPomelo 服务器介绍](https://github.com/NetEase/pomelo/wiki/Lordofpomelo-%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BB%8B%E7%BB%8D)