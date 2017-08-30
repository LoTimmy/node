### 安裝 {#installing}

```
shell> npm install geocoder
```

```js
"use strict";

// 导入所需模块
const geocoder = require('geocoder');
 
// Geocoding 
geocoder.geocode("Atlanta, GA", function ( err, data ) {
  // do something with data 
});
```

```js
"use strict";

// 导入所需模块
const geocoder = require('geocoder');
const co = require('co');

function getGeocode(address, language) {
  return function(cb) {
    // geocoder.geocode(address, cb);
    // geocoder.geocode(address, cb, { language: 'zh-TW' });
    geocoder.geocode(address, cb, { language: language });
  }
}

co(function* () {
  console.log( yield getGeocode('Atlanta, GA') );
  console.log( yield getGeocode('Japan') );
  console.log( yield getGeocode('241台灣新北市三重區三和路四段191巷5號', 'zh-TW') );
});
```

```js
"use strict";

// 导入所需模块
const thunkify = require('thunkify');
const geocoder = require('geocoder');
const co = require('co');

const getGeocode = thunkify(function(address, cb) {
  geocoder.geocode(address, cb);
});

co(function*() {
  console.log(yield getGeocode('Atlanta, GA'));
  console.log(yield getGeocode('Japan'));
  console.log(yield getGeocode('241台灣新北市三重區三和路四段191巷5號'));
});
```

```js
//  Created by Timmy on 2015/2/24.
//  Copyright (c) 2015年 Timmy. All rights reserved.

// 导入所需模块
const geocoder = require('geocoder');

// import async to make control flow simplier
const async = require('async');
const _ = require('underscore');

async.series([
  function(callback){
    geocoder.geocode("241台灣新北市三重區三和路四段191巷5號 ", function ( err, data ) {
    //  console.log( JSON.stringify(data) );
      console.log( JSON.stringify(data , null, " ") );
      callback();
    }, { language: 'en' });
  },
  function(callback){
    geocoder.geocode("241台灣新北市三重區三和路四段191巷5號 ", function ( err, data ) {
      console.log( JSON.stringify(data , null, " ") );
//      console.log( JSON.stringify(data) );
      callback();
    }, { language: 'zh-TW' });
  }
]);
```

#### :books: 參考網站：
- [geocoder](https://www.npmjs.com/package/geocoder)
- [geocoding](https://developers.google.com/maps/documentation/geocoding/intro)