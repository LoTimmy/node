### 安裝 {#installing}

```
shell> npm install lodash
```

```js
const _ = require('lodash');
const Q = require('q');

_.assign({ 'a': 1 }, { 'b': 2 }, { 'c': 3 });
// → { 'a': 1, 'b': 2, 'c': 3 }
_.map([1, 2, 3], function(n) { return n * 3; });
// → [3, 6, 9]

var object = { 'a': { 'b': { 'c': 3 } } };

_.has(object, 'a'); // → true
_.has(object, 'a.b.c'); // → true
_.has(object, ['a', 'b', 'c']); // → true

var users = [
  { 'user': 'barney',  'age': 36 },
  { 'user': 'fred',    'age': 40 },
  { 'user': 'pebbles', 'age': 1 }
];

var users = [
  { 'user': 'barney',  'active': false },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': true }
];

var dict = { 'thirty': 30, 'forty': 40, 'fifty': 50 };

var array = [1];
var array = [1, 2];
var array = [1, 2, 3];

var other = _.concat(array, 2, [3], [[4]]);

_.union([2, 1], [4, 2], [1, 2]); // → [2, 1, 4]
_.uniq([2, 1, 2]); // → [2, 1]

var zipped = _.zip(['fred', 'barney'], [30, 40], [true, false]); // → [['fred', 30, true], ['barney', 40, false]]
_.unzip(zipped); // → [['fred', 'barney'], [30, 40], [true, false]]

Q(_.camelCase('__FOO_BAR__')).then(console.log);


_.camelCase('Foo Bar'); // → 'fooBar'
_.camelCase('--foo-bar--'); // → 'fooBar'
_.camelCase('__FOO_BAR__'); // → 'fooBar'

_.capitalize('FRED'); // → 'Fred'

_.kebabCase('Foo Bar'); // → 'foo-bar'
_.kebabCase('fooBar'); // → 'foo-bar'
_.kebabCase('__FOO_BAR__'); // → 'foo-bar'

_.lowerCase('--Foo-Bar--'); // → 'foo bar'
_.lowerCase('fooBar'); // → 'foo bar'
_.lowerCase('__FOO_BAR__'); // → 'foo bar'

_.lowerFirst('Fred'); // → 'fred'
_.lowerFirst('FRED'); // → 'fRED'

_.pad('abc', 8); // → '  abc   '
_.pad('abc', 8, '_-'); // → '_-abc_-_'
_.pad('abc', 3); // → 'abc'

_.padEnd('abc', 6); // → 'abc   '
_.padEnd('abc', 6, '_-'); // → 'abc_-_'
_.padEnd('abc', 3); // → 'abc'

_.padStart('abc', 6); // → '   abc'
_.padStart('abc', 6, '_-'); // → '_-_abc'
_.padStart('abc', 3); // → 'abc'

_.parseInt('08'); // → 8
_.map(['6', '08', '10'], _.parseInt); // → [6, 8, 10]

_.repeat('*', 3); // → '***'
_.repeat('abc', 2); // → 'abcabc'
_.repeat('abc', 0); // → ''

_.replace('Hi Fred', 'Fred', 'Barney'); // → 'Hi Barney'

_.snakeCase('Foo Bar'); // → 'foo_bar'
_.snakeCase('fooBar'); // → 'foo_bar'
_.snakeCase('--FOO-BAR--'); // → 'foo_bar'

_.startCase('--foo-bar--'); // → 'Foo Bar'
_.startCase('fooBar'); // → 'Foo Bar'
_.startCase('__FOO_BAR__'); // → 'FOO BAR'

['a', 'b', 'c'].join('~'); // → 'a~b~c'

_([1, 2]).forEach(function(value) {
  console.log(value);
}); // → Logs `1` then `2`.

_.forEach({ 'a': 1, 'b': 2 }, function(value, key) {
  console.log(key);
}); // → Logs 'a' then 'b' (iteration order is not guaranteed).

_.times(3, String); // → ['0', '1', '2']
_.times(4, _.constant(true)); // → [true, true, true, true]



_.isNull(null); // → true
_.isNull(undefined); // → false

_.isUndefined(window.missingVariable); // → true


_.random(0, 5); // → an integer between 0 and 5
_.random(5); // → also an integer between 0 and 5
_.random(5, true); // → a floating-point number between 0 and 5
_.random(1.2, 5.2); // → a floating-point number between 1.2 and 5.2


var compiled = _.template('hello <%= user %>!');
compiled({ 'user': 'fred' }); // → 'hello fred!'

var compiled = _.template('<b><%- value %></b>');
compiled({ 'value': '<script>' }); // → '<b>&lt;script&gt;</b>'

var compiled = _.template('<% _.forEach(users, function(user) { %><li><%- user %></li><% }); %>');
compiled({ 'users': ['fred', 'barney'] }); // → '<li>fred</li><li>barney</li>'

var compiled = _.template('<% print("hello " + user); %>!');
compiled({ 'user': 'barney' }); // → 'hello barney!'

var compiled = _.template('hello ${ user }!');
compiled({ 'user': 'pebbles' }); // → 'hello pebbles!'

_.toLower('--Foo-Bar--'); // → '--foo-bar--'
_.toLower('fooBar'); // → 'foobar'
_.toLower('__FOO_BAR__'); // → '__foo_bar__'

_.toUpper('--foo-bar--'); // → '--FOO-BAR--'
_.toUpper('fooBar'); // → 'FOOBAR'
_.toUpper('__foo_bar__'); // → '__FOO_BAR__'

_.trim('  abc  '); // → 'abc'
_.trim('-_-abc-_-', '_-'); // → 'abc'
_.map(['  foo  ', '  bar  '], _.trim); // → ['foo', 'bar']

_.trimEnd('  abc  '); // → '  abc'
_.trimEnd('-_-abc-_-', '_-'); // → '-_-abc'

_.trimStart('  abc  '); // → 'abc  '
_.trimStart('-_-abc-_-', '_-'); // → 'abc-_-'

_.upperCase('--foo-bar'); // → 'FOO BAR'
_.upperCase('fooBar'); // → 'FOO BAR'
_.upperCase('__foo_bar__'); // → 'FOO BAR'

_.upperFirst('fred'); // → 'Fred'
_.upperFirst('FRED'); // → 'FRED'

_.map({ 'a': 4, 'b': 8 }, square);
```

```js
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

var array =  _.map(users, 'user');
console.log(array);
```

```js
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];

_.filter(users, _.matches({ 'age': 40, 'active': false }));
// → [{ 'user': 'fred', 'age': 40, 'active': false }]
```

#### :books: 參考網站：

- [lodash](https://www.npmjs.com/package/lodash)
- [lodash](https://lodash.com/)
- [docs](https://lodash.com/docs)