
```js
#!/usr/bin/env node
var lbs = require('node-qqwry');
var OpenCC = require('opencc');
// var opencc = new OpenCC('s2t.json');
// var opencc = new OpenCC('s2tw.json');
var opencc = new OpenCC('s2twp.json');
var CSV = require('csv-string');

var λ= function(ipAddress) {
  var data = CSV.parse(opencc.convertSync(lbs.getAddress(ipAddress)));
  return data[0];
};

console.log(λ('60.199.160.236'));  // => [ '臺灣省', '臺灣固網股份有限公司' ]
console.log(λ('106.155.177.79'));  // => [ '日本', '' ]
console.log(λ('168.95.1.1'));      // => [ '臺灣省', '中華電信DNS伺服器' ]
console.log(λ('210.242.247.177')); // => [ '臺灣省', '中華電信' ]
console.log(λ('8.8.8.8'));         // => [ '美國', '加利福尼亞州山景市谷歌公司DNS伺服器' ]
console.log(λ('210.59.230.60'));   // => [ '臺灣省', '中華電信' ]
```

```js
#!/usr/bin/env node
var fs = require('fs');
var lbs = require('node-qqwry');
var OpenCC = require('opencc');
var CSV = require('csv-string');
var readline = require('readline');
var ip = require('ip');

// var opencc = new OpenCC('s2t.json');
// var opencc = new OpenCC('s2tw.json');
var opencc = new OpenCC('s2twp.json');

var λ= function(ipAddress) {
  var data = CSV.parse(opencc.convertSync(lbs.getAddress(ipAddress)));
  return data[0];
};

var rl = readline.createInterface({
  input:  fs.createReadStream('./somefile.txt'),
  output: process.stdout,
  terminal: false
});

rl.on("line", function (line){
  if (ip.isPrivate(line)) {
    console.log("ip.isPrivate");
  } else {
    var geoip = require('geoip-lite');
    var geo = geoip.lookup( line );
    var country = geo.country;
    var city = geo.city;
    var data = λ(line);
    data.push(line,country,city);
  //  console.log(λ(line), geo);  
    console.log(data);
  }
}).on('close', function() {
  process.exit(0);
});
~~~