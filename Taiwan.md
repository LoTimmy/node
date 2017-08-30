```
shell> npm install tw-air-quality
```

```js
//  Created by Timmy on 2016/1/1.
//  Copyright (c) 2015年 Timmy. All rights reserved.
'use strict';

const twAirQuality = require('tw-air-quality');

// query PM2.5 by city name 
twAirQuality.queryPm25ByCity('新店', function (value) {
  // success 
  console.log(value);
}, function () {
  // failed 
});

```

`三重`
`冬山`
`宜蘭`
`士林`

#### :books: 參考網站：
- [tw-air-quality](https://www.npmjs.com/package/tw-air-quality)
- [pm25](http://taqm.epa.gov.tw/pm25/tw/default.aspx)
- [懸浮粒子](https://zh.wikipedia.org/wiki/%E6%87%B8%E6%B5%AE%E7%B2%92%E5%AD%90)

---

```js
//  Created by Timmy on 2016/1/1.
//  Copyright (c) 2015年 Timmy. All rights reserved.
'use strict';

const romanize = require('romanize-names');

console.log(romanize('張懸')); // → Hsuan Chang
console.log(romanize('張懸', 'MPS-II')); // → Shiuan Jang
console.log(romanize('張懸', 'HANYU')); // → Syuan Jhang

console.log(romanize('秋木安')); // → Mu-An Chiu
console.log(romanize('秋木安', 'MPS-II')); // → Mu-An Chiou
console.log(romanize('秋木安', 'HANYU')); // → Mu-An Ciou

console.log(romanize('范姜峻宏')); // → Chun-Hung Fan Chiang
console.log(romanize('范姜峻宏', 'MPS-II')); // → Jiun-Hung Fan Jiang
console.log(romanize('范姜峻宏', 'HANYU')); // → Jyun-Hong Fan Jiang

```

#### :books: 參考網站：
- [romanize-names](https://www.npmjs.com/package/romanize-names)

---

```js
//  Created by Timmy on 2016/1/1.
//  Copyright (c) 2015年 Timmy. All rights reserved.
'use strict';

var iplookup = require('iplookup');
 
iplookup.getInfo('173.194.72.94', function (ret) {
    console.log(ret);
});
/*
// Return value will be a JSON data:
{ ip: '173.194.72.94',
  flag: 'http://dir.twseo.org/images/flags/us.gif',
  country: '美國 (United States)',
  shortName: 'us',
  city: 'Mountain View',
  latitude: '37.4192',
  longitude: '-122.0574' }
*/

```

#### :books: 參考網站：
- [iplookup](https://www.npmjs.com/package/iplookup)

---

```js
//  Created by Timmy on 2016/1/1.
//  Copyright (c) 2015年 Timmy. All rights reserved.
'use strict';
var constellation = require("node-constellation");
var cons1 = constellation(12, 19, "zh-cn"); // → 射手座
var cons2 = constellation(11, 14, "en");  // → Scorpio
var cons3 = constellation(1, 1, "zh-tw"); // → 摩羯座
```

#### :books: 參考網站：
- [node-constellation](https://www.npmjs.com/package/node-constellation)

---

```js
//  Created by Timmy on 2016/1/1.
//  Copyright (c) 2015年 Timmy. All rights reserved.
'use strict';

var mothersDay = require("mothers-day");
 
console.log(mothersDay(2015)); // → Sun May 10 2015 00:00:00 GMT+0800 (CST)
console.log(mothersDay(2016)); // → Sun May 08 2016 00:00:00 GMT+0800 (CST)

```

#### :books: 參考網站：
- [mothers-day](https://www.npmjs.com/package/mothers-day)
