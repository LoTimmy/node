
~~~
#!/usr/bin/env node
var zhutil = require('zhutil');

console.log(zhutil.parseZHNumber('陸佰捌拾玖')); // => 689
console.log(zhutil.annotate(10987654321));      // => 109億8765萬4321
~~~