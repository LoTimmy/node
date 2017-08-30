### 安裝 {#installing}

```
shell> npm install winston
```

```js
var winston = require('winston');

winston.log('info', 'Hello distributed log files!');
winston.info('Hello again distributed logs');

winston.add(winston.transports.File, { filename: 'somefile.log' });
winston.remove(winston.transports.Console);


var logger = new winston.Logger({
    level: 'info',
    transports: [
      new (winston.transports.Console)(),
      new (winston.transports.File)({ filename: 'somefile.log' })
    ]
  });

logger.log('info', 'test message %s', 'my string');
logger.log('info', 'test message %d', 123);
logger.log('info', 'test message %j', {number: 123}, {});

```

#### :books: 參考網站：
- [winston](https://www.npmjs.com/package/winston)