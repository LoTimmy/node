![](https://cldup.com/wpGXm1cWwB.png)

### 安裝 {#installing}

```
shell> mkdir myapp
shell> cd myapp

shell> npm init

shell> npm install express --save

shell> npm install express
```

```
shell> npm install body-parser --save
shell> npm install ​compression --save
shell> npm install morgan --save
shell> npm install hide-powered-by --save 
shell> npm install cors --save
shell> npm install vhost --save
shell> npm install forever -g
```

#### :books: 參考網站：
- [installing](http://expressjs.com/en/starter/installing.html)

---

### Hello world example {#hello-world-example}

建立名為 `server.js` 的檔案，並新增下列程式碼：

```js
'use strict';

const express = require('express');

// Constants
const PORT = 8080;

// App
const app = express();
/*
app.get('/', function (req, res) {
  res.send('Hello world\n');
});
*/

app.get('/', (req, res) => {
  res.send('Hello world\n');
});

app.listen(PORT);
console.log('Running on http://localhost:' + PORT);
```

使用下列指令來執行應用程式：

```
shell> node server.js
```

應用程式會啟動伺服器，並在埠 8080 接聽連線。
然後在瀏覽器中載入 `http://localhost:8080/`，以查看輸出。

---

### Express application generator {#express-application-generator}

``` 
shell> npm install -g express-generator

shell> express
shell> express -h

shell> express --view=pug myapp
shell> cd myapp
shell> npm install
```

使用下列指令來執行應用程式：

``` 
shell> npm start
```
應用程式會啟動伺服器，並在埠 3000 接聽連線。
然後在瀏覽器中載入 `http://localhost:3000/`，以查看輸出。

```
.
├── app.js
├── bin
│   └── www
├── package.json
├── public
│   ├── images
│   ├── javascripts
│   └── stylesheets
│       └── style.css
├── routes
│   ├── index.js
│   └── users.js
└── views
    ├── error.pug
    ├── index.pug
    └── layout.pug

7 directories, 9 files
```

#### :books: 參考網站：
- [express-generator](https://www.npmjs.com/package/express-generator)
- [Pug](https://pugjs.org/api/getting-started.html)

---

### Basic routing {#basic-routing}

```js
app.METHOD(PATH, HANDLER)
```

```js
app.get('/', function (req, res) {
  res.send('Hello World!')
})

app.post('/', function (req, res) {
  res.send('Got a POST request')
})

app.put('/user', function (req, res) {
  res.send('Got a PUT request at /user')
})

app.delete('/user', function (req, res) {
  res.send('Got a DELETE request at /user')
})
```
#### :books: 參考網站：
- [basic-routing](http://expressjs.com/en/starter/basic-routing.html)

---

### Serving static files in Express {#serving-static-files-in-express}

```js
app.use(express.static('public'))
```

```
http://localhost:3000/images/kitten.jpg
http://localhost:3000/css/style.css
http://localhost:3000/js/app.js
http://localhost:3000/images/bg.png
http://localhost:3000/hello.html
```

```js
app.use(express.static('public'))
app.use(express.static('files'))

```

```js
app.use('/static', express.static('public'))
```
```
http://localhost:3000/static/images/kitten.jpg
http://localhost:3000/static/css/style.css
http://localhost:3000/static/js/app.js
http://localhost:3000/static/images/bg.png
http://localhost:3000/static/hello.html
```

```js
app.use('/static', express.static(path.join(__dirname, 'public')));
app.use('/bower_components', express.static(path.join(__dirname, 'bower_components')));
```

```
app.use('/bower_components',  express.static(__dirname + '/bower_components'));
```


#### :books: 參考網站：
- [static-files](http://expressjs.com/en/starter/static-files.html)
---


### How do I handle 404 responses? {#how-do-i-handle-404-responses}

```js
app.use(function (req, res, next) {
  res.status(404).send("Sorry can't find that!")
})
```

### How do I setup an error handler? {#how-do-i-setup-an-error-handler}

```js
app.use(function (err, req, res, next) {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})
```


---


```js
app.get('/', function (req, res) {
  res.send('root')
})

app.get('/about', (req, res) => {
  res.send('about')
})

app.get('/random.text', (req, res) => {
  res.send('random.text')
})

app.get('/users/:userId/books/:bookId', (req, res) => {
  res.send(req.params)
})
```

---

`package.json`

```json
{
  "name": "application-name",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {
    "body-parser": "*",
    "errorhandler": "*",
    "express": "*",
    "express-session": "*",
    "jade": "*",
    "method-override": "*",
    "morgan": "*",
    "multer": "*",
    "serve-favicon": "*"
  }
}
```

---

```js
//  Created by Timmy on 2015/2/24.
//  Copyright (c) 2015年 Timmy. All rights reserved.

// 导入所需模块
const express = require('express');

const app = express(); // the main app
const admin = express(); // the sub app

app.set('trust proxy', 'loopback');

admin.get('/', function (req, res) {
  console.log(admin.mountpath); // /admin
  res.send('Admin Homepage');
})

app.use('/admin', admin); // mount the sub app
```

#### :books: 參考網站：
- [behind-proxies](http://expressjs.com/guide/behind-proxies.html)

---

```js
//  Created by Timmy on 2015/2/24.
//  Copyright (c) 2015年 Timmy. All rights reserved.
'use strict';

// 导入所需模块
// var app = require('express')();
const http = require('http');
const express = require('express');
const app = express();
const path = require('path');
const fs = require('fs');

const bodyParser = require('body-parser');
const favicon = require('serve-favicon');
const multer = require('multer');
const cors = require('cors');
const morgan = require('morgan');
const compression = require('compression'); // 採用 gzip 壓縮 

app.set('port', process.env.PORT || 3000);
app.use(bodyParser.json()); // for parsing application/json
app.use(bodyParser.urlencoded({ extended: true })); // for parsing application/x-www-form-urlencoded
app.use(multer()); // for parsing multipart/form-data
app.use(cors());
app.use(morgan('combined'));
app.use(favicon(__dirname + '/public/favicon.ico'));

// create a write stream (in append mode)
var accessLogStream = fs.createWriteStream(__dirname + '/access.log', {flags: 'a'});

// Gzip 壓縮可以大幅減少回應內文的大小，從而提高 Web 應用程式的速度。
app.use(compression());

// setup the logger
app.use(morgan('combined', {stream: accessLogStream}));

app.get('/products/:id', function(req, res, next){
  res.json({msg: 'This is CORS-enabled for all origins!'});
});

app.post('/', function (req, res) {
  console.log(req.body);
  res.json(req.body);
})

// respond with "Hello World!" on the homepage
app.get('/', function (req, res) {
  res.send('Hello World!');
});

/*
app.get('/', function(req, res){
  res.sendfile('index.html');
});
*/

var server = app.listen(app.get('port'), function() {
  console.log('Express server listening on port ' + app.get('port'));
});

```

---

```js
// respond with "Hello World!" on the homepage
app.get('/', function (req, res) {
  res.send('Hello World!');
});

// accept POST request on the homepage
app.post('/', function (req, res) {
  res.send('Got a POST request');
});

// accept PUT request at /user
app.put('/user', function (req, res) {
  res.send('Got a PUT request at /user');
});

// accept DELETE request at /user
app.delete('/user', function (req, res) {
  res.send('Got a DELETE request at /user');
});
```

```js
app.route('/book')
  .get(function(req, res) {
    res.send('Get a random book');
  })
  .post(function(req, res) {
    res.send('Add a book');
  })
  .put(function(req, res) {
    res.send('Update the book');
  });
```

---

```js
app.get('/example/a', function (req, res) {
  res.send('Hello from A!');
});
```

```js
var cb0 = function (req, res, next) {
  console.log('CB0');
  next();
}

var cb1 = function (req, res, next) {
  console.log('CB1');
  next();
}

var cb2 = function (req, res) {
  res.send('Hello from C!');
}

app.get('/example/c', [cb0, cb1, cb2]);
```

---

```js
//birds.js
var express = require('express');
var router = express.Router();

// middleware specific to this router
router.use(function timeLog(req, res, next) {
  console.log('Time: ', Date.now());
  next();
});
// define the home page route
router.get('/', function(req, res) {
  res.send('Birds home page');
});
// define the about route
router.get('/about', function(req, res) {
  res.send('About birds');
});

module.exports = router;
```

```js
//index.js
var birds = require('./birds');
...
app.use('/birds', birds);
```


```js
//index.js
app.get('/viewdirectory', require('./mymiddleware.js'))
```

```js
//mymiddleware.js
module.exports = function (req, res) {
  res.send('The views directory is ' + req.app.get('views'));
});
```

---

```
shell> forever start app.js
```

---

```
shell> curl -w '\n' -d '{"myKey":"myValue"}' -H "Content-Type: application/json" http://127.0.0.1:3000/
shell> curl -w '\n' -H "Origin: http://example.com" --verbose http://127.0.0.1:3000/
```

---

**`跨原始來源分享` (Cross-Origin Resource Sharing,`CORS`)**

```js
const cors = require('cors');
app.use(cors());
```

```
shell> curl -I http://127.0.0.1/
```

```
...
Access-Control-Allow-Origin: *
...
```


```js
var http = require('http');

// Create an HTTP server
var srv = http.createServer(function (req, res) {
  res.end(JSON.stringify({msg: "Hello, world"}));
});

srv.listen(1337, '0.0.0.0', function() {
  var host = srv.address().address;
  var port = srv.address().port;
  console.log('Example app listening at http://%s:%s', host, port);
});
```

```html
<!DOCTYPE HTML>
<html lang="zh-TW">
  <head>
    <title>Untitled</title>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <meta http-equiv="Cache-Control" content="no-cache">
    <meta http-equiv="Pragma" content="no-cache">
    <meta http-equiv="Expires" content="-1"/>
    <link rel="SHORTCUT ICON" href="//jquery.com/favicon.ico">
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"> 

    <!--Load the AJAX API-->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>

    <script type="text/javascript">
      // execute when the HTML file's (document object model: DOM) has loaded
      $(document).ready(function(){
        $.getJSON( "http://114.35.124.22:1337", function( data ) {
          $( "#msg" ).html(data.msg);
        });
      });
    </script>

    <style>
    </style>
  </head>

  <body>
    <p><span id="msg"></span></p>
  </body>
</html>
```

```js
var http = require('http');

// Create an HTTP server
var srv = http.createServer(function (req, res) {
  res.writeHead(200, {"Access-Control-Allow-Origin": "*"});
  res.end(JSON.stringify({msg: "This is CORS-enabled for all origins!"}));
});

srv.listen(1337, '0.0.0.0', function() {
  var host = srv.address().address;
  var port = srv.address().port;
  console.log('Example app listening at http://%s:%s', host, port);
});
```

```js
var app = require('express')();
var bodyParser = require('body-parser');
var cors = require('cors');
var cool = require('cool-ascii-faces');

app.use(bodyParser.json()); // for parsing application/json
app.use(cors());

app.get('/cool', function(req, res) {
  res.send(cool());
});

app.get('/', function (req, res) {
  res.json({msg: 'This is CORS-enabled for all origins!'});
});

app.listen(app.get('port'), function() {
  console.log('Node app is running on port', app.get('port'));
});

```

```js
var app = require('express')();
var bodyParser = require('body-parser');
var cors = require('cors'); 

app.use(bodyParser.json()); // for parsing application/json
app.use(cors());


app.use('/', express.static('public'));
// app.use(express.static(__dirname + '/public'));


var server = app.listen(1337, function () {
  var port = server.address().port;

  console.log("listening on port %s", port);
});
```

---

```
shell> npm install apidoc -g
shell> apidoc -i myapp/ -o apidoc/
```

**apidoc.json**

```json
{
  "name": "example",
  "version": "0.1.0",
  "description": "A basic apiDoc example"
}
```

**example.js**
```js

```

#### :books: 參考網站：
- [apidocjs](http://apidocjs.com/)

---

```
shell> npm install express-generator -g
shell> express todo
shell> npm install async --save
```

```json
{
  "name": "Todo",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "start": "node ./bin/www"
  },
  "description": "Building a Todo List application with DocumentDB",
  "author": {
    "name": "",
    "email": ""
  },

  "dependencies": {
    "async": "^0.9.0",
    "body-parser": "~1.10.2",
    "cookie-parser": "~1.3.3",
    "debug": "~2.1.1",
    "documentdb": "^0.9.3",
    "express": "~4.11.1",
    "jade": "~1.9.1",
    "morgan": "~1.5.1",
    "serve-favicon": "~2.2.0"
  }
}
```


#### :books: 參考網站：
- [documentdb-nodejs-application](https://azure.microsoft.com/en-us/documentation/articles/documentdb-nodejs-application/)

---
<a name="reverse-proxy"></a>

**reverse-proxy**

```
shell> npm install http-proxy --save
```

```js
var app = require('express')();
var httpProxy = require('http-proxy');

app.set('port', process.env.PORT || 8000); 
var proxy = httpProxy.createProxyServer();

app.all('/api/*', function(req, res, next) {
  req.url = req.url.slice(5);
  proxy.web(req, res, { target: 'http://mytarget.com:8080' }, function(e) { console.log(e) });
});

var server = app.listen(app.get('port'), function () {
  console.log('Ready');
});
```

#### :books: 參考網站：
- [http-proxy](https://www.npmjs.com/package/http-proxy)
- [express-http-proxy](https://www.npmjs.com/package/express-http-proxy)

---

<a name="ssl-certificate-self"></a>
**Creating a Self-Signed SSL Certificate**

```
shell> which openssl
/usr/bin/openssl

shell> openssl genrsa -out server.key 2048 # Generate private key
shell> openssl req -new -sha256 -key server.key -out server.csr  # Generate CSR
shell> openssl x509 -req -in server.csr -signkey server.key -out server.crt

shell> curl -kvI https://www.example.com
```

```
shell> openssl genrsa -out server.key 2048
shell> openssl req -new -x509 -key server.key -out server.crt -days 7305 -subj /CN=www.example.com
shell> openssl x509 -in server.crt -text -noout
```

#### :books: 參考網站：
- [tls](https://nodejs.org/api/tls.html)
- [ssl-certificate-self](https://devcenter.heroku.com/articles/ssl-certificate-self)
- [ssl-endpoint](https://devcenter.heroku.com/articles/ssl-endpoint)

---

```
public/
├── images
├── javascripts
└── stylesheets
    └── style.css

routes/
└── index.js

bin
└── www

views/
```

```css
/* style.css */

body {
  padding: 50px;
  font: 14px "Lucida Grande", Helvetica, Arial, sans-serif;
}

a {
  color: #00B7FF;
}

```

```json
package.json

{
  "name": "www",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "start": "node ./bin/www"
  },
  "dependencies": {
    "body-parser": "~1.13.2",
    "cookie-parser": "~1.3.5",
    "express": "~4.13.1",
    "morgan": "~1.6.1",
    "serve-favicon": "~2.3.0"
  }
}

```
```js
// index.js

var express = require('express');
var router = express.Router();

/* GET home page. */
router.get('/', function(req, res, next) {
  res.send('Konichiwa!');
});

module.exports = router;

```

```js
// app.js

var express = require('express');
var path = require('path');
var favicon = require('serve-favicon');
var logger = require('morgan');
var cookieParser = require('cookie-parser');
var bodyParser = require('body-parser');

var routes = require('./routes/index');
var app = express();


module.exports = app;
```

```js
var app = require('../app');
var http = require('http');

var port = normalizePort(process.env.PORT || '3000');
app.set('port', port);

server.listen(port);

function normalizePort(val) {
  var port = parseInt(val, 10);

  if (isNaN(port)) {
    // named pipe
    return val;
  }

  if (port >= 0) {
    // port number
    return port;
  }

  return false;
}


```

---

```js
res.status(403).end();
res.status(400).send('Bad Request');
res.status(404).sendFile('/absolute/path/to/404.png');

res.status(404).send('Sorry, we cannot find that!');

res.send({ some: 'json' });
res.send('<p>some html</p>');
res.status(500).json({ error: 'message' })
res.status(500).send({ error: 'something blew up' });
res.status(406).send('Not Acceptable');

res.cookie('rememberme', '1', { maxAge: 900000, httpOnly: true })


app.use(function(req, res){
  res.status(404).sendFile(__dirname + '/public/404.html');
});

/*
app.use(function(req, res, next) {
  res.status(404).send('Sorry cant find that!');
});
*/

app.use(function(err, req, res, next) {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});


app.use(express.static(__dirname + '/public'));
app.use(express.static(__dirname + '/files'));
app.use(express.static(__dirname + '/uploads'));

```

```js
  res.send('Hello World');
  res.send('Konichiwa!');

  res.send('Hello');
  res.send('OK');
  console.log('Ready');
  res.send('hello world');
```

```
encrypted.google.com
```

---

```
shell> openssl genrsa -out server.key 2048
shell> openssl req -new -x509 -key server.key -out server.crt -days 7305 -subj "/CN=172.16.7.103"
```

```
shell> openssl req -new -x509 -nodes -keyout server.key -out server.crt -days 7305 -subj "/CN=www.example.com"
shell> openssl s_server -www -cipher AES256-SHA -key server.key -cert server.crt    
```

```js
//  Created by Timmy on 2016/1/1.
//  Copyright (c) 2015年 Timmy. All rights reserved.
'use strict';

const https = require('https');
const express = require('express');
const fs = require('fs');

const options = {
  key: fs.readFileSync('server.key'),
  cert: fs.readFileSync('server.crt')
};

var app = express();
app.get('/', function(req, res){
  res.status(200).json({ error: 'message' })
});


https.createServer(options, app).listen(443, function(){
  console.log('Ready');
}); 
```


```
shell> curl 'https://172.16.7.103/' --verbose
```

```
* Hostname was NOT found in DNS cache
*   Trying 172.16.7.103...
* Connected to 172.16.7.103 (172.16.7.103) port 443 (#0)
* successfully set certificate verify locations:
*   CAfile: none
  CApath: /etc/ssl/certs
* SSLv3, TLS handshake, Client hello (1):
* SSLv3, TLS handshake, Server hello (2):
* SSLv3, TLS handshake, CERT (11):
* SSLv3, TLS alert, Server hello (2):
* SSL certificate problem: self signed certificate
* Closing connection 0
curl: (60) SSL certificate problem: self signed certificate
More details here: http://curl.haxx.se/docs/sslcerts.html

curl performs SSL certificate verification by default, using a "bundle"
 of Certificate Authority (CA) public keys (CA certs). If the default
 bundle file isn't adequate, you can specify an alternate file
 using the --cacert option.
If this HTTPS server uses a certificate signed by a CA represented in
 the bundle, the certificate verification probably failed due to a
 problem with the certificate (it might be expired, or the name might
 not match the domain name in the URL).
If you'd like to turn off curl's verification of the certificate, use
 the -k (or --insecure) option.
```

```
shell> openssl s_client -showcerts -connect 172.16.7.103:443 < /dev/null > server.crt
shell> curl --cacert server.crt https://172.16.7.103/ --verbose
```

```
shell> curl 'https://172.16.7.103/' --insecure
shell> curl 'https://172.16.7.103/' -k
shell> wget 'https://172.16.7.103' --no-check-certificate
```

#### :books: 參考網站：
- [https](https://nodejs.org/api/https.html)
- [s_client](https://www.openssl.org/docs/manmaster/apps/s_client.html)
- [s_server](https://www.openssl.org/docs/manmaster/apps/s_server.html)

---

```js
//  Created by Timmy on 2016/1/1.
//  Copyright (c) 2015年 Timmy. All rights reserved.
'use strict';

const express = require('express');

app.locals.title = 'My App';
app.locals.strftime = require('strftime');
app.locals.email = 'me@myapp.com';

app.locals({
  title: 'My App',
  email: 'me@myapp.com'
});

app.locals.title
// => 'My App'

app.locals.email
// => 'me@myapp.com'
```

---

```js
//  Created by Timmy on 2016/1/1.
//  Copyright (c) 2015年 Timmy. All rights reserved.
'use strict';

const express = require('express');
const hidePoweredBy = require('hide-powered-by'); // hidePoweredBy 會移除 X-Powered-By 標頭。

app.use(hidePoweredBy());
app.use(hidePoweredBy({ setTo: 'PHP 4.2.0' }));
app.disable('x-powered-by');
```

#### :books: 參考網站：
- [hide-powered-by](https://github.com/helmetjs/hide-powered-by)

---

#### :books: 參考網站：
- [api](http://expressjs.com/api.html)
- [https://nodejs.org/api/http.html](https://nodejs.org/api/http.html)
- [jquery](https://developers.google.com/speed/libraries/#jquery)
- [html](http://api.jquery.com/html/)
- [cors](https://www.npmjs.com/package/cors)
- [Access_control_CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS)
- [Server-Side_Access_Control](https://developer.mozilla.org/en-US/docs/Web/HTTP/Server-Side_Access_Control)
- [vhost](https://www.npmjs.com/package/vhost)
- [best-practice-performance](http://expressjs.com/en/advanced/best-practice-performance.html)
- [best-practice-performance](http://expressjs.com/zh-tw/advanced/best-practice-security.html)

#### :books: 參考網站：
- [method-override](https://github.com/expressjs/method-override)
- [multer](https://github.com/expressjs/multer)
- [migrating-4](http://expressjs.com/guide/migrating-4.html)
- [pm](http://expressjs.com/advanced/pm.html)
- [express](https://www.npmjs.com/package/express)
- [expressjs](http://expressjs.com/)
- [routing](http://expressjs.com/guide/routing.html)
- [Hello world](http://expressjs.com/starter/hello-world.html)
- [Basic routing](http://expressjs.com/starter/basic-routing.html)
- [Static files](http://expressjs.com/starter/static-files.html)
- [installing](http://expressjs.com/starter/installing.html)
- [api](http://expressjs.com/api.html)
- [forever](https://www.npmjs.com/package/forever)
- [nodejs-docker-webapp](https://nodejs.org/en/docs/guides/nodejs-docker-webapp/)

「`跨站偽造請求`」 (`Cross-Site Request Forgery，CSRF`)
