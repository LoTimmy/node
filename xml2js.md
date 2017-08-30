### 安裝 {#installing}

```
shell> npm install faker
```

```js
var parseString = require('xml2js').parseString;
var xml = "<root>Hello xml2js!</root>"
parseString(xml, function (err, result) {
    console.dir(result); // → { root: 'Hello xml2js!' }
});

```

```js
var fs = require('fs'),
    xml2js = require('xml2js');
 
var parser = new xml2js.Parser();
fs.readFile(__dirname + '/foo.xml', function(err, data) {
    parser.parseString(data, function (err, result) {
        console.dir(result);
        console.log('Done');
    });
});
```

#### :books: 參考網站：
- [xml2js](https://www.npmjs.com/package/xml2js)
