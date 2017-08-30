### 安裝 {#installing}

```
shell> npm install facebook-chat-api
```

---
```js
//  Created by Timmy on 2016/3/29.
//  Copyright (c) 2016年 Timmy. All rights reserved.
"use strict";

// 导入所需模块
const login = require("facebook-chat-api");
 
// Create simple echo bot 
login({email: "FB_EMAIL", password: "FB_PASSWORD"}, function callback (err, api) {
    if(err) return console.error(err);
 
    api.listen(function callback(err, message) {
        api.sendMessage(message.body, message.threadID);
    });
});
```

```js
//  Created by Timmy on 2016/3/29.
//  Copyright (c) 2016年 Timmy. All rights reserved.
"use strict";

// 导入所需模块
const login = require("facebook-chat-api");

login({email: "FB_EMAIL", password: "FB_PASSWORD"}, function callback (err, api) {
    if(err) return console.error(err);
 
    var yourID = 0000000000000;
    var msg = {body: "Hey!"};
    var msg = {body: "中文"};
    api.sendMessage(msg, yourID);
});
```

```js
//  Created by Timmy on 2016/3/29.
//  Copyright (c) 2016年 Timmy. All rights reserved.
"use strict";

// 导入所需模块
const login = require("facebook-chat-api");
const fs = require('fs');

login({email: "FB_EMAIL", password: "FB_PASSWORD"}, function callback (err, api) {
    if(err) return console.error(err);
 
    // Note this example uploads an image called image.jpg 
    var yourID = 0000000000000;
    var msg = {
      body: "Hey!",
      attachment: fs.createReadStream(__dirname + '/image.jpg')
    }
    api.sendMessage(msg, yourID);
});
```


`getFriendsList`
```js
login({email: "FB_EMAIL", password: "FB_PASSWORD"}, function callback (err, api) {
  if(err) return console.error(err);

  api.getFriendsList(function(err, data) {
    if(err) return console.error(err);

    console.log(data.length);
  });
});
```


```js
login({email: "FB_EMAIL", password: "FB_PASSWORD"}, function callback (err, api) {
    if(err) return console.error(err);

    api.getUserID("Marc Zuckerbot", function(err, data) {
        if(err) return callback(err);

        // Send the message to the best match (best by Facebook's criteria)
        var threadID = data[0].userID;
        api.sendMessage(msg, threadID);
    });
});
```


```js
//  Created by Timmy on 2016/3/29.
//  Copyright (c) 2016年 Timmy. All rights reserved.
"use strict";

// 导入所需模块
const login = require("facebook-chat-api");
const phonetic = require('phonetic');
const EventEmitter = require('events').EventEmitter;
const ee = new EventEmitter();

login({email: "FB_EMAIL", password: "FB_PASSWORD"}, function callback (err, api) {
    if(err) return console.error(err);

    ee.on('myevent1', function () {
      console.log('myevent1')
      api.sendMessage({body: phonetic.generate()}, 0000000000000);
    });
    
    setInterval(function() {
      ee.emit('myevent1');
  //  }, 1800000 * Math.random() + 1200000);
    }, 2000);
  
    api.listen(function callback(err, message) {
        console.log(message.senderID + ': ' + message.body);
        api.sendMessage(message.body, message.threadID);
    }); 
});     
```


```js
//  Created by Timmy on 2016/3/29.
//  Copyright (c) 2016年 Timmy. All rights reserved.
"use strict";

// 导入所需模块
const login = require("facebook-chat-api");
const koa = require('koa');
const EventEmitter = require('events').EventEmitter;
const parse = require('co-body');
const router = require('koa-route');
const phonetic = require('phonetic');
const app = koa();
const ee = new EventEmitter();
const moment = require('moment');
const weather = require('weather-js');

moment.locale('zh-tw');
app.use(router.post('/sendMessage', sendMessage));

function* sendMessage() {
  var body = yield parse.json(this);
  ee.emit('myevent1', body.msg);
  this.body = body;
} 

login({email: "FB_EMAIL", password: "FB_PASSWORD"}, function callback (err, api) {
  if (err) { return console.error(err); }
  
  ee.on('myevent1', function(msg) {
    api.sendMessage({ body: msg }, 0000000000000);
  });

  api.setOptions({listenEvents: true});

  api.listen(function(err, event) {
    if (err) { return console.error(err); }
    switch(event.type) {
      case "message":
      if(event.body === 'hi') { api.sendMessage("你好", event.threadID); }
      if(event.body === 'now') { api.sendMessage(moment().format('LLLL'), event.threadID); }
      if(event.body === 'weather') {
        weather.find({search: "T'aipei, Taiwan", degreeType: 'C'}, function(err, result) {
          if (err) { console.error(err); }
            api.sendMessage(JSON.stringify(result, null, 2), event.threadID);
        });
      }
      break;
    }
  });
});

app.listen(3000);
console.log('listening on port 3000');
```

#### :books: 參考網站：
- [facebook-chat-api](https://www.npmjs.com/package/facebook-chat-api)
- [DOCS](https://github.com/Schmavery/facebook-chat-api/blob/master/DOCS.md)
- [findmyfbid](http://findmyfbid.com/)