`產生器` (`Generator`)

```js
"use strict";
function* gen() {
  yield 1;
  yield 2;
  yield 3;
}

var g = gen(); // "Generator { }"

console.log(g.next().value); // 1
console.log(g.next().value); // 2
console.log(g.next().value); // 3
```

`Recursion` `遞迴`

`遞迴`是一種重要的程式設計技巧，可以**使函式呼叫其本身**。
階乘計算就是一個例子。 數字之階乘 n 是藉由乘以 1 * 2 * 3 *… n 來計算。

```js
"use strict";
let factorial = num => {
// function factorial(num) {
  // If the number is less than 0, reject it.
  if (num < 0) {
    return -1;
  } else if (num == 0) {
    // If the number is 0, its factorial is 1.
    return 1;
  }
  var tmp = num;
  while (num-- > 2) {
    tmp *= num;
  }
  return tmp;
}

var result = factorial(8);
console.log(result);
```

#### :books: 參考網站：
- [遞迴 (JavaScript)](https://msdn.microsoft.com/zh-tw/library/wwbyhkx4(v=vs.94).aspx)
