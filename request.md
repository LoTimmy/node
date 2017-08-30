
### 安裝 {#installing}

```
shell> npm install request
shell> npm install progress
```

```js
const request = require('request');
request('http://www.google.com', function (error, response, body) {
  if (!error && response.statusCode == 200) {
    console.log(body) // Show the HTML for the Google homepage. 
  }
})
```

```js
const request = require('request');
const ProgressBar = require('progress');
const fs = require('fs');

var req = request('http://nodejs.org/dist/v0.10.28/node.exe');
var bar;

req
.on('data', function(chunk) {
  var len = parseInt(res.headers['content-length'], 10);
  bar = new ProgressBar('  downloading [:bar] :percent :etas', {
    complete: '=',
    incomplete: ' ',
    width: 20,
    total: len
  });
  bar.tick(chunk.length);
})
.on('end', function(err) {
    console.log(err)
})

```

```
  curl -X POST \
  -H "X-Parse-Application-Id: ${APPLICATION_ID}" \
  -H "X-Parse-REST-API-Key: ${REST_API_KEY}" \
  -H "Content-Type: application/json" \
  -d '{"score":1337,"playerName":"Sean Plott","cheatMode":false}' \
  https://api.parse.com/1/classes/GameScore
```

```js
const request = require('request');

var options = {
  uri: 'https://api.github.com/repos/request/request',
  method: 'POST',
  headers: {
    'User-Agent': 'request',
    'X-Parse-Application-Id': '',
    'X-Parse-REST-API-Key': '',
    'Content-Type': 'application/json'
  },
  json: {
    "username": "cooldude6",
    "password": "p_n7!-e8",
    "phone": "415-392-0202"
  }
};

function callback(error, response, body) {
  if (!error && response.statusCode == 200) {
    var info = JSON.parse(body);
  }
}

request(options, callback);
```

#### :books: 參考網站：

- [request](https://www.npmjs.com/package/request)
- [progress](https://www.npmjs.com/package/progress)
- http://parseplatform.github.io/docs/rest/guide/
