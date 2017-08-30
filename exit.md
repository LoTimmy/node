### 安裝 {#installing}

```
shell> npm install exit
```

```js
//  Created by Timmy on 2016/06/29.
//  Copyright (c) 2015年 Timmy. All rights reserved.
'use strict';

// 导入所需模块
var exit = require('exit');
 
// These lines should appear in the output, EVEN ON WINDOWS. 
console.log("omg");
console.error("yay");
 
// process.exit(5); 
exit(5);
 
// These lines shouldn't appear in the output. 
console.log("wtf");
console.error("bro");
```

#### :books: 參考網站：
- [exit](https://www.npmjs.com/package/exit)