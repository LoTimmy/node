### 安裝 {#installing}

```
shell> npm install --save nconf
```

```js
var path  = require('path');
var nconf = require('nconf');

nconf.use('file', { file: path.join(__dirname, 'config.json') });
nconf.load();
nconf.set('mssql:serverHost', '172.24.8.44'); // Server hostname or IP
nconf.set('mssql:serverPort', 1433);
nconf.set('mssql:userLogin', 'sa');    // User login
nconf.set('mssql:userPassword', ''); // User password

console.log(path.join(__dirname, 'config.json'));

var database = nconf.get('mssql');
console.dir(database);

nconf.save(function (err) {
});
```

`config.json`
```json
{
  "mssql": {
    "serverHost": "172.24.8.44",
    "serverPort": 1433,
    "userLogin": "sa",
    "userPassword": ""
  },
  "mysql": {
    "serverHost": "172.24.9.221",
    "serverPort": 3306,
    "userLogin": "root",
    "userPassword": ""
  }
}
```

#### :books: 參考網站：
- [nconf](https://www.npmjs.com/package/nconf)
