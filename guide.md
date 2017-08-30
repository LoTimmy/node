<img src="https://i-msdn.sec.s-msft.com/dynimg/IC736472.png" width="300">

---

```
shell> node --version
v4.1.1
```

```
shell> node -p process.versions
{ http_parser: '2.7.0',
  node: '6.9.1',
  v8: '5.1.281.84',
  uv: '1.9.1',
  zlib: '1.2.8',
  ares: '1.10.1-DEV',
  icu: '57.1',
  modules: '48',
  openssl: '1.0.2j' }
```

```
shell> node --v8-options 
```

- [process](https://nodejs.org/api/process.html)

---

**Specifying a Node.js Version**
```json
{
  "name": "myapp",
  "description": "a really cool app",
  "version": "1.0.0",
  "private": true,
  "engines": {
    "node": "4.1.1"
  }
}
```

```json
"engines": {
  "node": ">= 0.12.0"
}
```

**Specifying an Npm Version**
```json
{
  "name": "myapp",
  "description": "a really cool app",
  "version": "0.0.1",
  "private": true,
  "engines": {
    "npm": "2.1.x"
  }
}
```

---
```js
'use strict';
```
---

**布林值 (Boolean)**
```js
x = new Boolean(false);
if (x) {
  // this code is executed
}

x = false;
if (x) {
  // this code is not executed
}

x = true;
x = false;
```
---

**函數 (Function)**
```js
function myFunc() {
  console.log("foo");
}

myFunc(); // → "foo"

function calc_sales(units_a, units_b, units_c) {
   return units_a*79 + units_b * 129 + units_c * 699;
}

var mynumber = calc_sales( 1, 2, 3 );
console.log(mynumber);
```
---

**物件 (Object)**
```js
var myObj = new Object();
myObj.nickname = 'Jack';
myObj.registration_date = new Date(1995, 11, 25);
myObj.privileged_user = true; 
```

```js
var myObj = new Object();
myObj.name = "Fred";
myObj.count = 42;

delete myObj.name;
delete myObj["count"];

console.log(myObj);  // → {}
```

```js
var myObj = new Object();
console.log(myObj);  // → {}

myObj.name = "Fred";
myObj.toString = function() {
  return this.name;
} 

console.log(myObj.toString());  // → "Fred"
```

---

陣列 (Array)
```js
// Create an array.
var myArray = new Array();

myArray.nickname = 'Jack';
myArray.registration_date = new Date(1995, 11, 25);
myArray.privileged_user = true;
myArray[0] = 'Hello World!';

for (var i in myArray) {
  console.log( i + " = " + myArray[i] );
}

[2, 5, , 9].forEach(function(element, index) {
  console.log('a[' + index + '] = ' + element);
});
```

```js
// Create an array.
var fruits = ["Apple", "Banana"];
console.log(fruits.length); // → 2

var first = fruits[0]; // → "Apple"
var last = fruits[fruits.length - 1]; // → "Banana"

fruits.forEach(function(element, index) {
  console.log(element, index);
}); 

// → Apple 0
// → Banana 1

fruits.push("Orange");
console.log(fruits); // → [ 'Apple', 'Banana', 'Orange' ]

var popped = fruits.pop();
console.log(popped); // → "Orange"
console.log(fruits); // → [ 'Apple', 'Banana' ]

var shifted = fruits.shift(); 
console.log(shifted); // → "Apple"
console.log(fruits); // → [ 'Banana' ]

fruits.unshift("Pear");
console.log(fruits); // → [ 'Pear', 'Banana' ]


fruits.push("Peach"); // → [ 'Pear', 'Banana', 'Peach' ]
var idx = fruits.indexOf("Banana");  // → 1

var removed = fruits.splice(idx, 1);
console.log(removed); // → [ 'Banana' ]
console.log(fruits); // → [ 'Pear', 'Peach' ]

var cloned = fruits.slice();
console.log(removed); // → [ 'Pear', 'Peach' ]
```

```js
var alpha = ['a', 'b', 'c'],
    numeric = [1, 2, 3];

var alphaNumeric = alpha.concat(numeric);

console.log(alphaNumeric); // Result: ['a', 'b', 'c', 1, 2, 3]

var num1 = [1, 2, 3],
    num2 = [4, 5, 6],
    num3 = [7, 8, 9];

var nums = num1.concat(num2, num3);

console.log(nums); // Result: [1, 2, 3, 4, 5, 6, 7, 8, 9]

var alpha = ['a', 'b', 'c'];

var alphaNumeric = alpha.concat(1, [2, 3]);

console.log(alphaNumeric); 
// Result: ['a', 'b', 'c', 1, 2, 3]
```


```js
// Create an array.
var ar = new Array (10, 11, 12, 13, 14);

// Remove an element from the array.
delete ar[1];
console.log(ar); // → [ 10, , 12, 13, 14 ]
```

```js
// all following calls return true
Array.isArray([]);
Array.isArray([1]);
Array.isArray(new Array());
```

#### :books: 參考網站：
- [pop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)
- [shift](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/shift)
- [unshift](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift)
- [indexOf](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)
- [splice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)
- [slice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)
- [concat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat)
- [isArray](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray)

---

typeof
parseInt

```js
var mytext = '123';
console.log(typeof parseInt(mytext, 10)); // → "number"

parseInt("abc");     // → "NaN"
parseInt("12abc");   // → "12"
```

#### :books: 參考網站：
- [typeof 運算子 (JavaScript)](https://msdn.microsoft.com/zh-tw/library/259s7zc1(v=vs.94).aspx)
- [parseInt 函式 (JavaScript)](https://msdn.microsoft.com/zh-tw/library/x53yedee(v=vs.94).aspx)
- [parseFloat 函式 (JavaScript)](https://msdn.microsoft.com/zh-tw/library/d5hbbd4z(v=vs.94).aspx)

---
null
undefined

```js
var text = null;
console.log(text); // → null

var u;
console.log(u); // → undefined

console.log(typeof null); // object
console.log(typeof undefined); // undefined
```

---
條件 (三元) 運算子 (?:)

```
test ? expression1 : expression2
```
test 任何布林運算式。
expression1 如果 test 為 true，則傳回運算式。可以是逗號運算子。
expression2 如果 test 為 false，則傳回運算式。多個運算式可藉由逗號運算式連結。

```js
var status = (age >= 18) ? "adult" : "minor";
```

```js
var now = new Date();
var greeting = "Good" + ((now.getHours() > 17) ? " evening." : " day.");
```

上述範例會在下午 6 點後建立包含 "Good evening." 的字串。 使用 if...else 陳述式的同等程式碼看起來會像這樣：

```js
var now = new Date();
var greeting = "Good";
if (now.getHours() > 17)
   greeting += " evening.";
else
   greeting += " day.";
```

```js
if (err) console.log("Error: ", err);
```

#### :books: 參考網站：
- [條件 (三元) 運算子 (?:) (JavaScript)](https://msdn.microsoft.com/zh-tw/library/be21c7hw(v=vs.94).aspx)
- [Conditional_Operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)

---

JSON
```js
var myArray = [5, 2, 16, 4, 3, 18, 20];
var myObj = { nickname: 'Jack', "registration_date": new Date(1995, 11, 25), "privileged_user": true };


// JSON.stringify(): Object/Array → JSON  
var JavascriptObject = {name: "George", lastname: "Batalinski"};
var ValidJSON = JSON.stringify({name: "George", lastname: "Batalinski"});

// JSON.stringify(): JSON → Object/Array
var myArray = JSON.parse('[1, 5, "false"]');
var myObj = JSON.parse('{name: "George", lastname: "Batalinski"}');
```

---
```js
var mynumber = "99";
console.log(++mynumber); // → "100"
console.log(mynumber -1); // → "99"
console.log(1 -mynumber); // → "-99"
```

```js
var mynumber = "str99";
console.log(++mynumber); // → NaN
console.log(mynumber -1); // → NaN
console.log(1 -mynumber); // → NaN
```

---

```js
for(var i = 0; i < 10; i++) console.log(i);
for(var i = 0, j=10; i < 10; i++,j console.log(i*j);
```

```js
j=25;
for (i = 0; i < 10; i++, j++)
{
   k = i + j;
}
```
---
```js
if (x = y) {
}

if (x > 5) {
} else {
}

if (x > 5) {
} else if (x > 50) {
} else {
}
```

**閉包 (Closure)**
```js
var mynumber = 99;

function myFunc() {
  var mynumber = 9999;
  return mynumber;
}
console.log(mynumber); // → 99 
console.log(myFunc()); // → 9999


function makeAdder(x) {
  return function(y) {
    return x + y;
  };
}

var add5 = makeAdder(5);
var add10 = makeAdder(10);

console.log(add5(2));  // → 7
console.log(add10(2)); // → 12
```

---

<a name="elapsed"></a>
**Calculating elapsed time**

```js
// using Date objects
var start = Date.now();

// the event to time goes here:
doSomethingForALongTime();
var end = Date.now();
var elapsed = end - start; // elapsed time in milliseconds
```


```js
console.time('100-elements');
for (var i = 0; i < 100; i++) {
  ;
}
console.timeEnd('100-elements');
// prints 100-elements: 262ms
```

#### :books: 參考網站：
- [Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)

---

<a name="lambda"></a>

**Lambda**

> 函數f(x) = x * 2可匿名地表達為x -> x * 2
> (x -> x * 2)(2)以`JavaScript`來表達則為function(x) {return x * 2;}(2)

```js
(function() {
})();
```

```js
function(num) { return num * num; };
```

```js
console.log((function(num) { return num * num; })(2));
```

```js
var fn = function(num) { return num * num; };
console.log(fn(function(num) { return num + num; } (2))); // → 16
```

```js
console.log([1, 4, 9].map(function(num) { return num * num; })); // → [ 1, 16, 81 ]
```

#### :books: 參考網站：
- [map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

---

```
myString
myRe
myArray
myFalse 
myFunc
myObj

myboolean
mytext
mynumber
myobject
myarray
my-nodejs-app

doSomething();
doSomethingElse();
 
str 
newstr 
```
---
```js
var log = console.log.bind(console);
log('Hello World!');
```
---

```js
var createPet = function(name) {
  var sex;
  
  return {
    setName: function(newName) {
      name = newName;
    },
    
    getName: function() {
      return name;
    },
    
    getSex: function() {
      return sex;
    },
    
    setSex: function(newSex) {
      if(typeof newSex == "string" && (newSex.toLowerCase() == "male" || newSex.toLowerCase() == "female")) {
        sex = newSex;
      }
    }
  }
}

var pet = createPet("Vivie");
pet.getName();                  // → Vivie

pet.setName("Oliver");
pet.setSex("male");
pet.getSex();                   // → male
pet.getName();                  // → Oliver
```

---
```js
var myObj = {
  a: 37,
  f1: function(){
    console.log(this.a);
  }
};

myObj.f1(); // → 37

myObj.obj = {
  a: 111,
  f1: function(){
    console.log(this.a);
  }
};

myObj.obj.f1(); // → 111
```

```js
var a = 37;
var myObj = {
  a: 111,
  f1: function(){
    console.log(this.a);
    var self = this;
    var f2 = function(){ console.log(self.a); }
    f2();
  }
};

myObj.f1();
```

```js
var obj1 = {
  a: 37,
  f1: function(){
    console.log(this.a);
  }
};

var obj2 = {
  a: 111
};

obj1.f1.call(obj2); // → 111
```


```js
var eric = new Object();
eric.age = 33;
eric.sex = 'male';
console.log(eric); // → { age: 33, sex: 'male' }
```

```js
var eric = new Object();
eric.age = 33;
eric.sex = 'male';
eric.getSex = function() { return eric.sex; };
console.log(eric.getSex()); // → male
```

```js
var Person = function(name, age, sex) {
  this.name = name;
  this.age = age;
  this.sex = sex;
  this.getSex = function() { return this.sex; };
  this.sayHello = function(){ console.log('hello'); };
  this.sayGoodBye = function(){ console.log('goodBye'); };
  this.walk = function(){ console.log('I am walking!'); };
};

var eric = new Person('eric', 33, 'male');
console.log(eric); // → { name: 'eric', age: 33, sex: 'male', getSex: [Function] }

var wendy = new Person('wendy', 18, 'female');
console.log(wendy); // → { name: 'wendy', age: 18, sex: 'female', getSex: [Function] }

```

```js
var Person = function(name, age, sex) {
  this.name = name;
  this.age = age;
  this.sex = sex;
  this.getSex = function() { return this.sex; };
  this.sayHello = function(){ console.log('hello'); };
  this.sayGoodBye = function(){ console.log('goodBye'); };
  this.walk = function(){ console.log('I am walking!'); };
  this.doAction = function(){
    console.log(this.getSex());
    this.sayHello();
    this.walk();
    this.sayGoodBye();
  }; 
};

var eric = new Person('eric', 33, 'male');
eric.doAction();
```

```js
'use strict';
var util = require('util');

// 建構函式 (Constructor)
function Person() {
  this.name = 'N/A';
}

// Method
Person.prototype.SetName = function(name) {
  this.name = name;
}

// Method
Person.prototype.getSex = function() {
  return this.sex;
}

// Method
Person.prototype.greet = function() {
  console.log('Hi, I am ' + this.name);
};

// Method
Person.prototype.SayHello = function() {
  console.log("Hello, World!");
}

var Employee = function(name, title, sex, age) {
  Person.call(this);
  this.name = name;
  this.title = title;
  this.sex = sex;
  this.age = age;
};

var Customer = function(name) {
  Person.call(this);
  this.name = name;
};

util.inherits(Employee, Person);
util.inherits(Customer, Person);

Employee.prototype.greet = function() {
  console.log('Hi, I am ' + this.name + ', the ' + this.title);
};

var bob = new Employee('Bob', 'Builder', 'male', 33);
var joe = new Customer('Joe');
var rg = new Employee('Red Green', 'Handyman');


bob.greet();
rg.greet();

```

#### :books: 參考網站：
-  [prototype](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype)
- [this] (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
- [JavaScript 物件導向介紹](https://developer.mozilla.org/zh-TW/docs/JavaScript_物件導向介紹)
- [Introduction to Object-Oriented JavaScript](https://developer.mozilla.org/en-US/docs/Talk:JavaScript/Introduction_to_Object-Oriented_JavaScript)

---
```js
try {
  throw "myException";
}
catch(e) {
  logMyErrors(e);
}
```
---

```js
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

```js
var http = require("http");

http.createServer(function(request, response) {
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.write("Hello MSDN");
  response.end();
}).listen(8080);
```

---
```js
var x = 'Mozilla';
var empty = '';
console.log('Mozilla is ' + x.length + ' code units long');
// → "Mozilla is 7 code units long" 

console.log('The empty string has a length of ' + empty.length);
// → "The empty string has a length of 0"
```

---

#### :books: 參考網站：
- [length](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/length)

---
<a name="closure-compiler"></a>

```js:hello.js
// A simple function.
function hello(longName) {
  alert('Hello, ' + longName);
}
hello('New User');
```

```
shell> wget -q https://dl.google.com/closure-compiler/compiler-latest.zip
shell> unzip compiler-latest.zip
shell> java -jar compiler.jar --js hello.js --js_output_file hello-compiled.js
```

```js:hello-compiled.js
function hello(a){alert("Hello, "+a)}hello("New User");
```

#### :books: 參考網站：
- [Closure Compiler](https://developers.google.com/closure/compiler/docs/gettingstarted_app)

---

```js
var crypto = require('crypto');
var hashes = crypto.getHashes();
console.log(hashes);
var ciphers = crypto.getCiphers();
console.log(ciphers);
```

```js
var crypto = require('crypto');

// Encrypt using AES
function aes_encrypt(str, key_str) {
  var cipher = crypto.createCipher('aes192', key_str);
  var crypt_str = cipher.update(str, 'utf8', 'hex');
  crypt_str += cipher.final('hex');
  return crypt_str;
}

// Decrypt using AES
function aes_decrypt(crypt_str, key_str) {
  var decipher = crypto.createDecipher('aes192', key_str);
  var str = decipher.update(crypt_str, 'hex', 'utf8');
  str += decipher.final('utf8');
  return str;
}

var crypt_str = aes_encrypt('cleartext', 'my_secret_password'); 
console.log(crypt_str);

var str = aes_decrypt(crypt_str, 'my_secret_password'); 
console.log(str);
```

#### :books: 參考網站：
- [aes_encrypt](https://mariadb.com/kb/en/mariadb/aes_encrypt/)

---

```js
  if (err) throw err;
```

---

```js
function main() {
  return 'Hello, World!';
}

main();
```

---

#### `Iterator` `迭代器`

```js
function makeIterator(array){
    var nextIndex = 0;
    
    return {
       next: function(){
           return nextIndex < array.length ?
               {value: array[nextIndex++], done: false} :
               {done: true};
       }
    }
}

var it = makeIterator(['yo', 'ya']);
console.log(it.next().value); // 'yo'
console.log(it.next().value); // 'ya'
console.log(it.next().done);  // true

```

- [Iterators_and_Generators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators)

---

```
setInterval(function() {
  doSomething();
}, 1800000 * Math.random() + 1200000); // between 20 and 50 min
```

---

```js
function doSomething() {
  console.log("Hello World!");
}

doSomething();
```

```js
var doSomething = () => {
  console.log("Hello World!");
};

doSomething();
```

```js
var doSomething = () => console.log("Hello World!");

doSomething();
```

```js
var doSomething = function() {
  return "Hello World!";
}

var doSomething = () => "Hello World!";
console.log(doSomething());
```

```js
var func = function(x, y) {
  return x + y;
}

var func = (x, y) => x + y;
console.log(func(3, 5));
```

#### :books: 參考網站：
- [Arrow_functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

---

#### :books: 參考網站：
- [runnable](http://code.runnable.com/)
- [新版Node.js終於支援類別](http://www.ithome.com.tw/news/98663)
- [從ECMAScript看語言約束](http://www.ithome.com.tw/voice/89425)
- [Installing Node.js and Express](https://www.vultr.com/docs/installing-node-js-and-express)
- [非同步操作的多種模式](http://www.ithome.com.tw/node/82486)
- [Visual Studio也能寫Node.js，擴充套件NTVS 1.0正式版釋出](http://www.ithome.com.tw/news/94807)
- [建立 Node.js 和 MongoDB Web 服務](https://msdn.microsoft.com/zh-tw/library/dn754378.aspx)
- [try...- catch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch)
- [var](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)
- [Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)
- [function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)
- [Function](https://developer.mozilla.org/en-US/docs/Glossary/Function)
- [Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [for](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for)
- [for...in](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)
- [if...else](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else)
- [JSON.stringify()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)
- [JSON.parse()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)


