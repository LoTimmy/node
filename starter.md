<img src="http://i.imgur.com/yrb3Srt.png" width="100">

### 安裝 {#installing}

```
shell> brew install node
shell> apt-get install nodejs
```

```
shell> brew install nvm
```

```
shell> curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.1/install.sh | bash
shell> wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.32.1/install.sh | bash
shell> echo "source ~/.nvm/nvm.sh" >> .bashrc
```

```
shell> nvm ls-remote
shell> nvm ls-remote --lts

shell> nvm install --lts
shell> nvm install --lts=argon
shell> nvm install --lts=boron
shell> nvm install v0.12.0
shell> nvm install v4.2.2
shell> nvm install v6.1.0
shell> nvm install v8.4.0

shell> nvm uninstall v4.2.2
shell> nvm uninstall v6.1.0

shell> nvm use --lts
shell> nvm use --lts=argon
shell> nvm use --lts=boron

shell> nvm ls
shell> nvm alias default 0.12.0
shell> nvm alias default 4.2.2
shell> nvm alias default lts/argon
shell> nvm alias default lts/boron
```

```
shell> nvm install v6.10.1 --reinstall-packages-from=v6.10.0
shell> nvm uninstall v6.10.0

shell> nvm install v7.7.4

shell> nvm install 6 --reinstall-packages-from=5
shell> nvm install v4.2 --reinstall-packages-from=iojs
```

#### :books: 參考網站：
- [nvm](https://github.com/creationix/nvm)

### Hello world 範例 {#helloWorld}

建立名為 `hello.js` 的檔案，並新增下列程式碼：

```js
console.log('Hello World!');
```

使用下列指令來執行應用程式：

```
shell> node hello.js
```

### `變數` (`Variable`) {#var}

> `JavaScript` 有兩個範圍：**全域**和**區域**。在函式定義之外宣告的變數就是**全域變數**，其值可在整個程式中存取和修改。
> 宣告變數。在函式定義內宣告的變數則是**區域變數**。
> 可以宣告變數而不使用 `var` 關鍵字，並為變數指派值。 這稱為「`隱含宣告`」，但不建議使用。 隱含宣告會提供全域範圍給變數。
> 如果未初始化 `var` 中的變數，系統會自動指派 `JavaScript` 值 `undefined` 給此變數。
> 下列程式碼是示範如何宣告整數變數、指派其值，然後再為其指派新值的簡單範例。

```js
var a;
var a = 1;
var a = 0, b = 0;
var bigNumber = 1e100;
var mynumber = 99;

var u = undefined;

var myString = new String('Hello');
var mytext = 'Hello World!';

var b = new Boolean(false);
var x = new Boolean(false);
var x = false;
var myFalse = new Boolean(false);
var myboolean = true, myFalse = false;
var btrue = new Boolean(true);
var bfalse = new Boolean(false);
var F = new Boolean();
var T = new Boolean(true);
var F = new Boolean(0);
var T = new Boolean(1);

function doSomething() {}
var f = function() {};
f();
var myFunc = function() {};


var text = null;

var o = {};
var myObj = {}, myobject = { nickname: 'Jack', "registration_date": new Date(1995, 11, 25), "privileged_user": true };
var object = {
  someMethod: function() {}
};

var myarray = [], someArray = [ 1, 2, 3 ];

var greeting = "Hello, World!";

var index;  
var name = "Thomas Jefferson";  
var answer = 42, counter, numpages = 10;  
var myarray = new Array();
```
---

### 樣版字串 (`Template Strings`)

```js
var mynumber = 99;
console.log(`my favorite number is: ${mynumber}`);
```

```js
var name = "Bob";
var str = `Hello ${name}, how are you this fine ${partOfDay()}?`;
console.log(str);

function partOfDay() {
  var hour = new Date().getHours();

  if (hours <= 12) {
    return "morning";
  } else if (hours <= 5) {
    return "afternoon";
  } else {
    return "evening";
  }
}
```

```js
function buildURL(strArray, ...valArray) {
  var newUrl = strArray[0] + "ja-ja" + "/" + valArray[1] + "/" + valArray[2];

  return newUrl;
}

var lang = "en-us";
var a = "library";
var b = "dn771551.aspx";

// Call the tagged template function.
var url = buildURL`http://msdn.microsoft.com/${lang}/${a}/${b}`;

console.log(url);
```

#### :books: 參考網站：
- [範本字串 (JavaScript)](https://msdn.microsoft.com/zh-tw/library/dn858580(v=vs.94).aspx)
- [Template Strings](https://docs.microsoft.com/en-us/scripting/javascript/advanced/template-strings-javascript)

### `常數` (`Constant`) {#const}

> 常數會使用 `const` 宣告
> 在這個範例中，常數 `MY_FAV` 永遠會是 7

```js
// define MY_FAV as a constant and give it the value 7
const MY_FAV = 7;

MY_FAV = 20;

// will print 7
console.log("my favorite number is: " + MY_FAV);

var MY_FAV = 20; 

// MY_FAV is still 7
console.log("my favorite number is " + MY_FAV);
```

```js
const months = 12, weeks = 52, days = 365;
const daysPerWeek = days / weeks;
const daysPerMonth = days / months;

const speedLimit = 55;
const pi = 3.14159265358979323846264338327950;
const Pi = 3.14159;
const SpeedOfLight = 300000; // km per sec.
```

`範例`

```js
var radius = 5.3; // Radius 半徑
const pi = 3.14159265358979323846264338327950; // PI 圓周率
var area = pi * (radius * radius); // Area 面積
```

> 宣告區塊範圍變數。
> 「`區域變數`」(`Local Variable`)
> 使用 `let` 來宣告變數，其範圍限於宣告所在的區塊。

```js
"use strict";

function varTest() {
  var x = 31;
  if (true) {
    var x = 71; // same variable!
    console.log(x); // 71
  }
  console.log(x); // 71
}

function letTest() {
  let x = 31;
  if (true) {
    let x = 71; // different variable
    console.log(x); // 71
  }
  console.log(x); // 31
}
```

#### :books: 參考網站：
- [let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
- [let 陳述式 (JavaScript)](https://msdn.microsoft.com/zh-tw/library/dn263046(v=vs.94).aspx)
- [const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
- https://docs.microsoft.com/en-us/scripting/javascript/advanced/variable-scope-javascript

---

### `嚴格模式` (`Strict Mode`) {#strict}

```js
'use strict';
```

---

### 類別 (`Classes`) {#class}

```js
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }

  get area() {
    return this.calcArea();
  }

  calcArea() {
    return this.height * this.width;
  }
}

const square = new Rectangle(10, 10);

console.log(square.area);
```

```js
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(this.name + " makes a noise.");
  }
}

class Dog extends Animal {
  speak() {
    console.log(this.name + " barks.");
  }
}

var d = new Dog("Mitzie");
d.speak(); // Mitzie barks.
```

```js
class Cat {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(this.name + " makes a noise.");
  }
}

class Lion extends Cat {
  speak() {
    super.speak();
    console.log(this.name + " roars.");
  }
}

var l = new Lion("Fuzzy");
l.speak();
// Fuzzy makes a noise.
// Fuzzy roars.
```

#### :books: 參考網站：
- [Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)

---

### 解構賦值 (`Destructuring`) {#daifoP4n}

```js
var a, b, rest;
[a, b] = [10, 20];
console.log(a); // 10
console.log(b); // 20

[a, b, ...rest] = [10, 20, 30, 40, 50];
console.log(a); // 10
console.log(b); // 20
console.log(rest); // [30, 40, 50]

({ a, b } = { a: 10, b: 20 });
console.log(a); // 10
console.log(b); // 20

({ a, b, ...rest } = { a: 10, b: 20, c: 30, d: 40 });
console.log(a); // 10
console.log(b); // 20
console.log(rest); // {c: 30, d: 40}
```

```js
var x = [1, 2, 3, 4, 5];
var [y, z] = x;
console.log(y); // 1
console.log(z); // 2

// Array destructuring
var foo = ["one", "two", "three"];
var [one, two, three] = foo;
console.log(one); // "one"
console.log(two); // "two"
console.log(three); // "three"

// Array destructuring
var [a, ...b] = [1, 2, 3];
console.log(a); // 1
console.log(b); // [2, 3]

// Object destructuring
var o = { p: 42, q: true };
var { p, q } = o;
console.log(p); // 42
console.log(q); // true

// Assigning to new variable names
var o = { p: 42, q: true };
var { p: foo, q: bar } = o;
console.log(foo); // 42
console.log(bar); // true
```

```js
var people = [
  {
    name: "Mike Smith",
    family: {
      mother: "Jane Smith",
      father: "Harry Smith",
      sister: "Samantha Smith"
    },
    age: 35
  },
  {
    name: "Tom Jones",
    family: {
      mother: "Norah Jones",
      father: "Richard Jones",
      brother: "Howard Jones"
    },
    age: 25
  }
];

for (var { name: n, family: { father: f } } of people) {
  console.log("Name: " + n + ", Father: " + f);
}

// "Name: Mike Smith, Father: Harry Smith"
// "Name: Tom Jones, Father: Richard Jones"
```

```js
function userId({ id }) {
  return id;
}

function whois({ displayName, fullName: { firstName: name } }) {
  console.log(displayName + " is " + name);
}

var user = {
  id: 42,
  displayName: "jdoe",
  fullName: {
    firstName: "John",
    lastName: "Doe"
  }
};

console.log("userId: " + userId(user)); // "userId: 42"
whois(user); // "jdoe is John"
```

```js
const foo = { 'fizz-buzz': true };
const { 'fizz-buzz': fizzBuzz } = foo;

console.log(fizzBuzz); // "true"
```

#### :books: 參考網站：
- [Destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

---

### `事件` (`Events`) {#events}

```js
var EventEmitter = require('events').EventEmitter;
var myEmitter = new EventEmitter(); 

myEmitter.on('event', function () {
  console.log('an event occurred!'); 
});

myEmitter.emit('event');
```

```js
const EventEmitter = require('events');
class MyEmitter extends EventEmitter {}
const myEmitter = new MyEmitter();

myEmitter.on('event', () => {
  console.log('an event occurred!');
});

setTimeout(function() {
  myEmitter.emit('event');
}, 1000);
```

```js
var EventEmitter = require('events').EventEmitter;
var myEmitter = new EventEmitter();

myEmitter.on('hello', function (arg1, arg2) {
    console.log(arg1 + ' ' + arg2);
});

myEmitter.emit('hello', 'Hello', 'World');
```

```js
var EventEmitter = require('events').EventEmitter;
var myEmitter = new EventEmitter();

myEmitter.on('sayHello', function(name) {
  console.log("Hello" + " " + name);
});

myEmitter.emit('sayHello', 'Eric');
```
---

### `箭頭函數` (`Arrow functions`) {#arrowFunctions}

`箭頭函數` (`Arrow Function`)

```js
function ([param[, param]]) {
  statements
}

([param[, param]]) => {
  statements
}
```

```js
(param) => {}
param => {}

(param1, param2) => {}
param1, param2 => {}

() => {}

param1, param2 => {
    return param1 + param2;
  };
param1, param2 => param1 + param2;
```

```js
var a = [
  'Hydrogen',
  'Helium',
  'Lithium',
  'Beryllium'
];

var a2 = a.map(function(s) { return s.length; });
console.log(a2); // logs [8, 6, 7, 9]

var a3 = a.map(s => s.length);
console.log(a3); // logs [8, 6, 7, 9]
```

```js
var myFunction = () => {};
```

#### :books: 參考網站：
- [Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions)
- [Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)

---

###  (`Rest parameters`) {#rest_parameters}

```js
function f(a, b, ...theArgs) {
  // ...
}
```

```js
function f(a, b) {
  var args = Array.prototype.slice.call(arguments, f.length);

  // …
}

function f(a, b, ...args) {
  // …
}
```

```js
function fun1(...theArgs) {
  console.log(theArgs.length);
}

fun1();  // 0
fun1(5); // 1
fun1(5, 6, 7); // 3
```

```js
(param1, param2, ...rest) => { statements }
```

`arguments`

```js
(function() {
  for (let argument of arguments) {
    console.log(argument);
  }
})(1, 2, 3);
```

#### :books: 參考網站：
- [Rest parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)

---

Spread_operator
- [Spread_operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)

---

```js
var myObj = {
  nickname: "Jack",
  registration_date: new Date(1995, 11, 25)
}

var {
  nickname,
  registration_date
} = myObj;

console.log(nickname);
console.log(registration_date);
```
```js
var nickname = 'Jack';
var registration_date = new Date(1995, 11, 25);
var myObj = {nickname, registration_date};

console.log(myObj);
```

---

#### :books: 參考網站：
- [events](https://nodejs.org/api/events.html)

---

### for...of {#forOf}

```js
for (variable of iterable) {
  statement
}
```

```js
let iterable = [10, 20, 30];

for (let value of iterable) {
  value += 1;
  console.log(value);
}
// 11
// 21
// 31
```

```js
let arr = ["fred", "tom", "bob"];

for (let i of arr) {
  console.log(i);
}
```

```js
var m = new Map();
m.set(1, "black");
m.set(2, "red");

for (var n of m) {
  console.log(n);
}
```

#### :books: 參考網站：
- [for...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)
- [for...of](https://msdn.microsoft.com/zh-tw/library/dn858238(v=vs.94).aspx)

---

### coding-style {#codingStyle}

`coding-style`

#### `Comma First`

```js
var magicWords = [ 'abracadabra'
                 , 'gesundheit'
                 , 'ventrilo'
                 ]
  , spells = { 'fireball' : function () { setOnFire() }
             , 'water' : function () { putOut() }
             }
  , a = 1
  , b = 'abc'
  , etc
  , somethingElse
```

#### `Quotes` {#quotes}

- Double quotes (") `雙引號 (")`
- Single quotes (') `單引號 (')`

```js
var ok = 'String contains "double" quotes'
var alsoOk = "String contains 'single' quotes or apostrophe"
```

- `Functions` `函數` `函式`
- `Properties` `屬性`
- `Methods` `方法`
- `Class` `類別`

- `lowerCamelCase` → `Objects` `Functions` `Methods` `Properties`
- `UpperCamelCase` → `Class`
- `all-lower-hyphen-css-case` → `FileName` `Config`
- `CAPS_SNAKE_CASE`

#### :books: 參考網站：
- [coding-style](https://docs.npmjs.com/misc/coding-style)
- [camel-case](https://capitalizemytitle.com/camel-case/)
- [all-lower-hyphen-css-case](http://en.toolpage.org/tool/kebabcase)

---

### Recursion {#recursion}

`Recursion` `遞迴`

`遞迴`是一種重要的程式設計技巧，可以**使函式呼叫其本身**。
階乘計算就是一個例子。 數字之階乘 n 是藉由乘以 1 * 2 * 3 *… n 來計算。

```js
"use strict";
function factorial(num) {
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

---

### 費氏數列 {#fibonacci}

![](https://upload.wikimedia.org/wikipedia/commons/d/db/34%2A21-FibonacciBlocks.png)
![](https://upload.wikimedia.org/wikipedia/commons/2/2e/FibonacciSpiral.svg)

- `費氏數列`
- `費波那契數列`

---

- $$F_0 = 0$$
- $$F_1 = 1$$
- $$F_n = F_{n-1} + F_{n-2}$$ (n≧2)
- $$F_{n-2} = F_n - F_{n-1}$$

用文字來說，就是`費氏數列`由0和1開始，之後的費波那契系數就是由之前的兩數相加而得出。
首幾個費波那契系數是： **0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233……**

$$\frac{1}{1},\frac{2}{1},\frac{3}{2},\frac{5}{3},\frac{8}{5},\frac{13}{8},\frac{21}{13},\frac{34}{21},\frac{55}{34},$$…

```
2÷1=2
3÷2=1.5
5÷3=1.666666667
8÷5=1.6
13÷8=1.625
21÷13=1.615384615
34÷21=1.619047619
55÷34=1.617647059
89÷55=1.618181818
144÷89=1.617977528
233÷144=1.618055556
377÷233=1.618025751
610÷377=1.618037135
```

```
1×1=1
2×2=4
3×3=9
5×5=25
8×8=64
13×13=169
21×21=441
```

`0.618:1`=`1:1.618`
`1-0.618`=`0.382`

```js
function fibonacci(num){
  if (num === 0) {
    return 0;
  }
  if (num === 1) {
    return 1;
  }
  return fibonacci(num-1) + fibonacci(num-2);
}

if (require.main === module) {
  var num = Number(process.argv[2]);
  console.log("fibonacci(?) ?", num, fibonacci(num) );
}
```

```js
function* fibonacci() { // a generator function
  let [prev, curr] = [0, 1];
  while (true) {
    [prev, curr] = [curr, prev + curr];
    yield curr;
  }
}

for (let n of fibonacci()) {
  console.log(n);
  // truncate the sequence at 1000
  if (n >= 1000) {
    break;
  }
}
```

```js
function fibonacci(num){
  var fn1 = 0;
  var fn2 = 1;
  var tmp;
  while (num >= 0){
    tmp = fn2;
    fn2 = fn2 + fn1;
    fn1 = tmp;
    num--;
  }
  return fn1;
}
```

```js
function* fibonacci() {
  var fn1 = 0;
  var fn2 = 1;
  while (true) {  
    var current = fn1;
    fn1 = fn2;
    fn2 = current + fn1;
    yield current;
  }
}

var sequence = fibonacci();
console.log(sequence.next().value);     // 0
console.log(sequence.next().value);     // 1
console.log(sequence.next().value);     // 1
console.log(sequence.next().value);     // 2
console.log(sequence.next().value);     // 3
console.log(sequence.next().value);     // 5
console.log(sequence.next().value);     // 8
console.log(sequence.next().value);     // 13
console.log(sequence.next().value);     // 21
```
---

`等比數列`

- 1,2,4,8,16,32,64,… `公比` `q` = `2`
- 1,-1,1,-1,1,-1,… `公比`= `-1`
- 3,3,3,3,3,… `公比` = `1`

`等比數列`

---

`科學記號`格式會以指數表示法顯示數字，以 E+n 來取代部分的數字，其中 E (代表指數) 會將其前面的數字乘以 10，再將乘積乘 n 次方。例如，兩位小數的科學記號格式會將 12345678901 顯示為 1.23E+10，也就是 1.23 乘以 10 的 10 次方。

---

```js
var numFiles = files.length;

for (var i = 0, numFiles = files.length; i < numFiles; i++) {
  var file = files[i];
  ..
}
```

