### 安裝 {#installing}

```
shell> npm install forever -g
```

```
shell> forever start app.js
```

```
.
├── forever
│   └── development.json
└── index.js
```

```json

// forever/development.json
{
    "uid": "app",
    "append": true,
    "watch": true,
    "script": "index.js",
    "sourceDir": "/home/myuser/app"
}
```


```
shell> forever start ./forever/development.json
```

#### :books: 參考網站：
- [forever](https://www.npmjs.com/package/forever)