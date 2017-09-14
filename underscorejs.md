![](http://underscorejs.org/docs/images/underscore.png)

### 安裝 {#installing}

```
shell> npm install underscore
shell> npm install underscore.string
```

```js
const _ = require("underscore");
const s = require("underscore.string");
_.mixin(s.exports());

_.each([1, 2, 3], (element, index, array) => {
  console.log(element);
});

_.map([1, 2, 3], (num) => {
  console.log(num * 3);
});

var sum = _.reduce(
  [1, 2, 3],
  (memo, num) => {
    return memo + num;
  },
  0
);

var evens = _.filter([1, 2, 3, 4, 5, 6], num => num % 2 == 0);
var odds = _.reject([1, 2, 3, 4, 5, 6], num => num % 2 == 0);

var users = [
  { user: "barney", active: true },
  { user: "fred", active: false },
  { user: "pebbles", active: false }
];
console.log(_.where(users, { active: true }));

console.log(_.contains([1, 2, 3], 3));

var stooges = [
  { name: "moe", age: 40 },
  { name: "larry", age: 50 },
  { name: "curly", age: 60 }
];
console.log(_.pluck(stooges, "name")); // [ 'moe', 'larry', 'curly' ]
console.log(_.max(stooges, stooge => stooge.age)); // { name: 'curly', age: 60 }
console.log(_.min(stooges, stooge => stooge.age)); // { name: 'moe', age: 40 }
console.log(_.sortBy(stooges, "name")); 
/*
[ { name: 'curly', age: 60 },
  { name: 'larry', age: 50 },
  { name: 'moe', age: 40 } ]
*/

var numbers = [10, 5, 100, 2, 1000];
console.log(_.min(numbers));

console.log(_.sortBy([5, 4, 6, 3, 1, 2], num => num));

console.log(_.groupBy(["one", "two", "three"], "length")); // { '3': [ 'one', 'two' ], '5': [ 'three' ] }

console.log(_.countBy([1, 2, 3, 4, 5], num => (num % 2 == 0 ? "even" : "odd"))); // { odd: 3, even: 2 }

console.log(_.shuffle([1, 2, 3, 4, 5, 6]));
console.log(_.shuffle(_.pluck(stooges, "name")));

console.log(_.size({ one: 1, two: 2, three: 3 }));

console.log(_.range(10)); // [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
console.log(_.range(1, 11)); // [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ]
console.log(_.range(0, 30, 5)); // [0, 5, 10, 15, 20, 25]
console.log(_.range(0, -10, -1)); // [0, -1, -2, -3, -4, -5, -6, -7, -8, -9]

console.log(_.compact([0, 1, false, 2, "", 3]));
console.log(_.flatten([1, [2], [3, [[4]]]])); // [ 1, 2, 3, 4 ]


var func = function(greeting) {
  return greeting + ": " + this.name;
};
func = _.bind(func, { name: "moe" }, "hi");
func();
console.log(func());

var subtract = (a, b) => b - a;
sub5 = _.partial(subtract, 5);
console.log(sub5(20));

var fibonacci = _.memoize(
  n => (n < 2 ? n : fibonacci(n - 1) + fibonacci(n - 2))
);
console.log(fibonacci(10));

var log = _.bind(console.log, console);
_.delay(log, 1000, "logged later");

var throttled = _.throttle(() => {
  _(5).times(n => {
    console.log(n + ":" + new Date());
  });
}, 100);
throttled();
/*
0:Wed Sep 06 2017 16:14:17 GMT+0800 (CST)
1:Wed Sep 06 2017 16:14:17 GMT+0800 (CST)
2:Wed Sep 06 2017 16:14:17 GMT+0800 (CST)
3:Wed Sep 06 2017 16:14:17 GMT+0800 (CST)
4:Wed Sep 06 2017 16:14:17 GMT+0800 (CST)
*/

var initialize = _.once(() => {
  console.log("initialize");
});
initialize();
initialize();

var array = [1, 2, 3, 4];
var done = _.after(array.length, () => {
  console.log("done");
});
_.each(array, num => {
  console.log(num);
  done();
});

var hello = name => "hello: " + name;
hello = _.wrap(hello, func => "before, " + func("moe") + ", after");
console.log(hello());

var greet = name => "hi: " + name;
var exclaim = statement => statement.toUpperCase() + "!";
var welcome = _.compose(greet, exclaim);
console.log(welcome('moe'));

console.log(_.pick({ name: "moe", age: 50, userid: "moe1" }, "name", "age"));
console.log(_.omit({ name: "moe", age: 50, userid: "moe1" }, "userid"));

var iceCream = {flavor: "chocolate"};
console.log(_.defaults(iceCream, {flavor: "vanilla", sprinkles: "lots"}));

console.log(_.extend({ name: "moe" }, { age: 50 }));

console.log(_.keys({ one: 1, two: 2, three: 3 })); // [ 'one', 'two', 'three' ]
console.log(_.values({ one: 1, two: 2, three: 3 })); // [ 1, 2, 3 ]

_.random(0, 100);
_(3).times(n => console.log(n));

console.log(_.uniqueId("contact_")); // contact_1
console.log(_.uniqueId("contact_")); // contact_2
console.log(_.uniqueId("contact_")); // contact_3

var object = {cheese: 'crumpets', stuff: () =>  'nonsense' };
console.log(_.result(object, 'cheese'));
console.log(_.result(object, 'stuff'));
console.log(_.result(object, 'meat', 'ham'));

var compiled = _.template("hello: <%= name %>");
compiled({name: 'moe'});

_.templateSettings = {
  interpolate: /\{\{(.+?)\}\}/g
};
var template = _.template("Hello {{ name }}!");
template({name: "Mustache"});

var stooges = [
  { name: "curly", age: 25 },
  { name: "moe", age: 21 },
  { name: "larry", age: 23 }
];
var youngest = _.chain(stooges)
  .sortBy(stooge => stooge.age)
  .map(stooge => stooge.name + " is " + stooge.age)
  .first()
  .value();
console.log(youngest);

_.chain([1, 2, 3]).reverse().value(); // [3, 2, 1]

console.log(_.capitalize("foo Bar"));
console.log(_.titleize("my name is epeli"));

_.mixin({
  capitalize: function(string) {
    return string.charAt(0).toUpperCase() + string.substring(1).toLowerCase();
  }
});
_("fabio").capitalize();
```

#### :books: 參考網站：
- [underscore](http://underscorejs.org/)
- [underscore.string](http://gabceb.github.io/underscore.string.site/)
