<img src="https://hapijs.com/public/img/logo.svg" width="200">


### 安裝 {#installing}

```
shell> npm install hapi
shell> npm install hapi --save
```

---

### Creating a server

建立名為 `server.js` 的檔案，並新增下列程式碼：

```js
"use strict";

const Hapi = require("hapi");

const server = new Hapi.Server({
  host: "localhost",
  port: 8000
});

(async () => {
  try {
    await server.start();
    console.log(`Server running at: ${server.info.uri}`);
  } catch (err) {
    console.log(err);
  }
})();
```

使用下列指令來執行應用程式：

```
shell> node server.js
```

應用程式會啟動伺服器，並在埠 3000 接聽連線。
然後在瀏覽器中載入 `http://localhost:3000/`，以查看輸出。

---

### 基本路由 {#basic-routing}

> 路由是指判斷應用程式如何回應用戶端對特定端點的要求，而這個特定端點是一個 URI（或路徑）與一個特定的 HTTP 要求方法（GET、POST 等）。
> 每一個路由可以有一或多個處理程式函數，當路由相符時，就會執行這些函數。

path 是伺服器上的路徑。
method 是 HTTP 要求方法。
handler 是當路由相符時要執行的函數。

下列範例說明如何定義簡單的路由。

首頁中以 Hello World! 回應。

建立名為 `server.js` 的檔案，並新增下列程式碼：

```js
'use strict';

const Hapi = require('hapi');

const server = new Hapi.Server({
  host: "localhost",
  port: 8000
});

server.route({
  method: "GET",
  path: "/",
  handler: (request, h) => {
    return "Hello, world!";
  }
});

(async () => {
  try {
    await server.start();
    console.log(`Server running at: ${server.info.uri}`);
  } catch (err) {
    console.log(err);
  }
})();
```

```js
server.route({
  method: 'GET',
  path: '/{name}',
  handler: function(request, reply) {
    reply('Hello, ' + encodeURIComponent(request.params.name) + '!');
  }
});
```

---

### Creating static pages and content

```js
server.register(require('inert'), (err) => {
  if (err) {
    throw err;
  }

  server.route({
    method: 'GET',
    path: '/hello',
    handler: function(request, reply) {
      reply.file('./public/hello.html');
    }
  });
});
```

---

### Using plugins

```
shell> npm install --save good
shell> npm install --save good-console
shell> npm install --save good-squeeze
```

`server.js`

```js
'use strict';

const Hapi = require('hapi');
const Good = require('good');

const server = new Hapi.Server();
server.connection({ port: 3000, host: 'localhost' });


server.route({
  method: "GET",
  path: "/hello",
  handler: (request, h) => {
    return "hello world";
  }
});

server.route({
  method: "GET",
  path: "/{name}",
  handler: (request, h) => {
    return `Hello, ${encodeURIComponent(request.params.name)}!`;
  }
});

server.route({
  method: 'GET',
  path: '/',
  handler: function(request, reply) {
    reply('Hello, world!');
  }
});

server.register({
  register: Good,
  options: {
    reporters: {
      console: [{
        module: 'good-squeeze',
        name: 'Squeeze',
        args: [{
          response: '*',
          log: '*'
        }]
      }, {
        module: 'good-console'
      }, 'stdout']
    }
  }
}, (err) => {

  if (err) {
    throw err; // something bad happened loading the plugin
  }

  server.start((err) => {

    if (err) {
      throw err;
    }
    server.log('info', 'Server running at: ' + server.info.uri);
  });
});
```

```js
const plugin = {
  register: Good,
  options: {
    reporters: {
      console: [{
        module: 'good-squeeze',
        name: 'Squeeze',
        args: [{
          response: '*',
          log: '*'
        }]
      }, {
        module: 'good-console'
      }, 'stdout']
    }
  }
};


server.register(plugin, (err) => {
  server.start(() => {});
});

server.register(plugin, (err) => {
  if (err) {
    throw err; // something bad happened loading the plugin
  }

  server.start((err) => {
    if (err) {
      throw err;
    }
    server.log('info', 'Server running at: ' + server.info.uri);
  });
});
```

```
140625/143008.751, [log,info], data: Server running at: http://localhost:3000

140625/143205.774, [response], http://localhost:3000: get / {} 200 (10ms)
```


---

```
shell> npm install hapi-swagger --save
shell> npm install inert --save
shell> npm install vision --save 
```

```js
const Hapi = require('hapi');
const Inert = require('inert');
const Vision = require('vision');
const HapiSwagger = require('hapi-swagger');
const Joi = require('joi');

const server = new Hapi.Server();
server.connection({
  host: 'localhost',
  port: 3000
});

const options = {
  info: {
    'title': 'Test API Documentation',
    'version': '0.0.2',
  }
};

server.route({
  method: 'GET',
  path: '/{name}',
  config: {
    tags: ['api'],
    validate: {
      params: {
        name: Joi.string().required()
      },
    },
    handler: function(request, reply) {
      reply('Hello, ' + encodeURIComponent(request.params.name) + '!');
    }
  }
});

server.route({
  method: 'POST',
  path: '/items',
  config: {
    tags: ['api'],
    handler: (request, reply) => {
      reply('OK');
    },
    validate: {
      payload: Joi.object({
        a: Joi.number(),
        b: Joi.number()
      })
    }
  }
});

server.route({
  method: 'GET',
  path: '/items/{pageNo}',
  config: {
    handler: (request, reply) => {
      reply('OK');
    },
    tags: ['api'],
    validate: {
      params: {
        pageNo: Joi.number()
      },
      query: {
        search: Joi.string()
      },
      headers: Joi.object({
        'authorization': Joi.string().required()
      }).unknown()
    }
  }
});

server.register([
  Inert,
  Vision, {
    'register': HapiSwagger,
    'options': options
  }
], (err) => {
  server.start((err) => {
    if (err) {
      console.log(err);
    } else {
      console.log('Server running at:', server.info.uri);
    }
  });
});
```

`http://localhost:3000/documentation`

<img src="https://raw.github.com/hapijs/joi/master/images/joi.png" width="200">

#### :books: 參考網站：
- [hapi-swagger](https://github.com/glennjones/hapi-swagger)
- [usageguide](https://github.com/glennjones/hapi-swagger/blob/master/usageguide.md)

---

```js
server.route({
  method: 'POST',
  path: '/items',
  config: {
    tags: ['api'],
    handler: (request, reply) => {

    },
    validate: {
      payload: Joi.object({
        a: Joi.number(),
        b: Joi.number()
      })
    }
  }
});
```


```js
reply(request.payload.a);
reply('Hello, ' + encodeURIComponent(request.params.name) + '!');
```

---

<img src="https://camo.githubusercontent.com/575791dedbd0f604aeda72ab878464bf4b0f0a9f/68747470733a2f2f7261772e6769746875622e636f6d2f686170696a732f6a6f692f6d61737465722f696d616765732f76616c69646174696f6e2e706e67" width="200">

```js
username: Joi.string().alphanum().min(3).max(30).required(),
password: Joi.string().regex(/^[a-zA-Z0-9]{3,30}$/),
birthyear: Joi.number().integer().min(1900).max(2013),
email: Joi.string().email()
```

---


---

### hapi-auth-jwt2 {#hapi-auth-jwt2}

```
shell> npm install hapi
shell> npm install hapi-auth-jwt2 --save
```

`Generating Your Secret Key`

```
shell> node -e "console.log(require('crypto').randomBytes(256).toString('base64'));"
```

```js
const Hapi = require('hapi');
const Inert = require('inert');
const Vision = require('vision');
const HapiSwagger = require('hapi-swagger');
const Joi = require('joi');
const hapiAuthJWT = require('hapi-auth-jwt2');
const port = process.env.PORT || 3000;

const server = new Hapi.Server();
server.connection({
  host: 'localhost',
  port: port
});

const options = {
  info: {
    'title': 'Test API Documentation',
    'version': '0.0.2',
  }
};

var people = {
  1: {
    id: 1,
    name: 'John Doe'
  }
};

var secret = 'NeverShareYourSecret';

var validate = function(decoded, request, callback) {
  if (!people[decoded.id]) {
    return callback(null, false);
  } else {
    return callback(null, true);
  }
};

server.route({
  method: 'GET',
  path: '/{name}',
  config: {
    auth: false,
    tags: ['api'],
    validate: {
      params: {
        name: Joi.string().required()
      },
    },
    handler: function(request, reply) {
      reply('Hello, ' + encodeURIComponent(request.params.name) + '!');
    }
  }
});

server.route({
  method: 'POST',
  path: '/items',
  config: {
    tags: ['api'],
    handler: (request, reply) => {
      reply('OK');
    },
    validate: {
      payload: Joi.object({
        a: Joi.number(),
        b: Joi.number()
      }),
      headers: Joi.object({
        'authorization': Joi.string().required()
      }).unknown()

    }
  }
});

server.route({
  method: 'GET',
  path: '/items/{pageNo}',
  config: {
    handler: (request, reply) => {
      reply('OK');
    },
    tags: ['api'],
    validate: {
      params: {
        pageNo: Joi.number()
      },
      query: {
        search: Joi.string()
      },
      headers: Joi.object({
        'authorization': Joi.string().required()
      }).unknown()
    }
  }
});

server.register([
  Inert,
  Vision, {
    'register': HapiSwagger,
    'options': options
  },
  hapiAuthJWT
], (err) => {
  server.auth.strategy('jwt', 'jwt', {
    key: secret,
    validateFunc: validate,
    verifyOptions: {
      ignoreExpiration: true
    }
  });

  server.auth.default('jwt');

  server.start((err) => {
    if (err) {
      console.log(err);
    } else {
      console.log('Server running at:', server.info.uri);
    }
  });
});
```

```
shell> curl -H "Authorization: <TOKEN>" http://localhost:8000/restricted
```

```
shell> curl -X POST --header 'Content-Type: application/json' --header 'Accept: text/html' --header 'authorization: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNDkxODE5OTgzfQ.9NOyEW5zbZslW9Whs75p38OhtREh0G6bg1ZyJcHc6jw' -d '{
  "a": 0,
  "b": 0
}' 'http://192.168.1.55:3000/items'
```


`iat` `IssuedAt`


#### :books: 參考網站：
- https://jwt.io/
- [hapi-auth-jwt2](https://www.npmjs.com/package/hapi-auth-jwt2)
- [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken)
- https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims


---

### hapi-mongodb {#hapi-mongodb}

```
shell> npm install hapi-mongodb
shell> npm install hapi-mongodb --save
```

```js
const Hapi = require('hapi');
const Boom = require('boom');

const dbOpts = {
  url: 'mongodb://localhost:27017/test',
  settings: {
    poolSize: 10
  },
  decorate: true
};

const server = new Hapi.Server();

server.register({
  register: require('hapi-mongodb'),
  options: dbOpts
}, function(err) {
  if (err) {
    console.error(err);
    throw err;
  }

  server.route({
    method: 'GET',
    path: '/users/{id}',
    handler(request, reply) {
      const db = request.mongo.db;
      const ObjectID = request.mongo.ObjectID;

      db.collection('users').findOne({        _id: new ObjectID(request.params.id)      }, function(err, result) {

        if (err) {
          return reply(Boom.internal('Internal MongoDB error', err));
        }

        reply(result);
      });
    }
  });

  server.start(function() {
    console.log(`Server started at ${server.info.uri}`);
  });
});
```

```
const Hapi = require('hapi');
const Boom = require('boom');
const port = process.env.PORT || 5000;

const dbOpts = {
  url: 'mongodb://localhost:27017/automodules_development',
  settings: {
    poolSize: 10
  },
  decorate: true
};

const server = new Hapi.Server();
server.connection({
  port: port
});

server.register({
  register: require('hapi-mongodb'),
  options: dbOpts
}, function(err) {
  if (err) {
    console.error(err);
    throw err;
  }

  server.route({
    method: 'GET',
    path: '/test',
    handler(request, reply) {
      const db = request.mongo.db;

      db.collection('users').insertOne({
        name: 'John',
        age: 25,
        gender: 'boy'
      }, function(err, result) {
        if (err) {
          return reply(Boom.internal('Internal MongoDB error', err));
        }
        reply(result);
      });

    }
  });

  server.start(function() {
    console.log(`Server started at ${server.info.uri}`);
  });
});
```


#### :books: 參考網站：
- [hapi-mongodb](https://www.npmjs.com/package/hapi-mongodb)

---

```
var plugins = [
  {
    register: require('hapi-auth-basic')
  },
  {
    register: require('hapi-authorization'),
    options: {
      roles: ['OWNER', 'MANAGER', 'EMPLOYEE'] // Can also reference a function which returns an array of roles
    }
  }
];

server.register(plugins, function(err) {
      ...
```

---

- `Tutorials` `[tjuˋtorɪəl]` `教學課程` `tu・to・ri・als`

#### :books: 參考網站：
- [hapijs](https://hapijs.com/)
- [tutorials](https://hapijs.com/tutorials)
- [api](https://hapijs.com/api)
- https://github.com/hapijs/joi/blob/v10.4.1/API.md

