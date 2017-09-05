
```js
const XRegExp = require('xregexp');

const date = XRegExp('(?<year>  [0-9]{4}) -?  # year  \n\
                    (?<month> [0-9]{2}) -?  # month \n\
                    (?<day>   [0-9]{2})     # day   ', 'x');

let match = XRegExp.exec('2012-02-22', date);

// console.log(match.day);
console.log(match);  // ->
/*
[ '2012-02-22',
  '2012',
  '02',
  '22',
  index: 0,
  input: '2012-02-22',
  year: '2012',
  month: '02',
  day: '22' ]
*/

XRegExp.replace('2012-02-22', date, '${month}/${day}/${year}');

date.exec('2012-02-22').day;            // -> '22'
date.test('2012-02-22');                // -> true
'2012-02-22'.replace(date, '$2/$3/$1'); // -> '02/22/2012'


var time = XRegExp.build('(?x)^ {{hours}} ({{minutes}}) $', {
    hours: XRegExp.build('{{h12}} : | {{h24}}', {
        h12: /1[0-2]|0?[1-9]/,
        h24: /2[0-3]|[01][0-9]/
    }, 'x'),
    minutes: /^[0-5][0-9]$/
});

 
time.test('10:59');                  // -> true 
XRegExp.exec('10:59', time).minutes; // -> '59' 

XRegExp.union(['a+b*c', /(dogs)\1/, /(cats)\1/], 'i');
// -> /a\+b\*c|(dogs)\1|(cats)\2/i


var regex = XRegExp('^ \\d{1,2}      (?#month)' +
                    '/ \\d{1,2}      (?#day  )' +
                    '/ (\\d{2}){1,2} (?#year )', 'nx');

var isDate = regex.test('04/20/2008'); // -> true
 
```

#### :books: 參考網站：
- [xregexp](https://www.npmjs.com/package/xregexp)
- [xregexp](http://xregexp.com/)
