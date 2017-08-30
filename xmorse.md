```
shell> npm install xmorse
```

```js
//  Created by Timmy on 2016/1/1.
//  Copyright (c) 2015年 Timmy. All rights reserved.
'use strict';

var xmorse = require('xmorse');

xmorse.encode('Hello, Xmorse!');
xmorse.encode('コンニチハ, セカイ!');
xmorse.encode('越过长城，走向世界');

// option 
var option = {
  space: ' ',
  long: '-',
  short: '*'
};
xmorse.encode('越过长城，走向世界', option);


xmorse.decode('../.-../---/...-/./-.--/---/..-/-/---/---/--...-....-...-/-..---..-.-----/---..-...--...-/-..----.--.....');
 
// option 
var option = {
  space: ' ',
  long: '-',
  short: '*'
};
xmorse.decode('*-** --- ***- *', option);
```

#### :books: 參考網站：

- [xmorse](https://www.npmjs.com/package/xmorse)
- [xmorse](https://github.com/hustcc/xmorse)

