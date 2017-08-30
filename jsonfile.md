### 安裝 {#installing}

```
shell> npm install jsonfile --save
```

```js
var jsonfile = require('jsonfile')
var util = require('util')
 
var file = '/tmp/data.json'
jsonfile.readFile(file, function(err, obj) {
  console.dir(obj)
})

```

#### :books: 參考網站：
- [jsonfile](https://www.npmjs.com/package/jsonfile)



