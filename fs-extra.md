### 安裝 {#installing}

```
shell> npm install --save fs-extra
```

```js
var fs = require('fs-extra');
 
fs.copy('/tmp/myfile', '/tmp/mynewfile', function (err) {
  if (err) return console.error(err)
  console.log("success!")
});
 
try {
  fs.copySync('/tmp/myfile', '/tmp/mynewfile')
  console.log("success!")
} catch (err) {
  console.error(err)
}

fs.emptyDir('/tmp/some/dir', function (err) {
  if (!err) console.log('success!')
})

fs.readJson('./package.json', function (err, packageObj) {
  console.log(packageObj.version) // => 0.1.3 
})

fs.remove('/tmp/myfile', function (err) {
  if (err) return console.error(err)
 
  console.log('success!')
})
 
fs.removeSync('/home/jprichardson')
```

#### :books: 參考網站：
- [fs-extra](https://www.npmjs.com/package/fs-extra)
