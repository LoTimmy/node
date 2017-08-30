
```
shell> npm install tape
```

`timing.js`
```js
const test = require('tape');

test('timing test', function (t) {
    t.plan(2);

    t.equal(typeof Date.now, 'function');
    var start = Date.now();

    setTimeout(function () {
        t.equal(Date.now() - start, 100);
    }, 100);
});

```

```
TAP version 13
# timing test
ok 1 should be equal
not ok 2 should be equal
  ---
    operator: equal
    expected: 100
    actual:   102
    at: null._onTimeout (/root/src/_tape/timing.js:10:11)
  ...

1..2
# tests 2
# pass  1
# fail  1
```

```js
const test = require('tape');
const tapSpec = require('tap-spec');

test.createStream()
  .pipe(tapSpec())
  .pipe(process.stdout);
```

```
  timing test

    ✔ should be equal

    ✖ should be equal
    ------------------
      operator: equal
      expected: 100
      actual:   102
      at: null._onTimeout (/root/src/_tape/timing.js:16:11)
```

```
'should return -1 when the value is not present'
'should save without error'
'respond with matching records'
'should return -1 unless present'
'should return the index when present'
'should not throw an error'
```

![](https://cloud.githubusercontent.com/assets/974723/7888261/03366236-05ec-11e5-9f94-d9c2707526b7.png)

#### :books: 參考網站：
- [tape](https://github.com/substack/tape)
- [tap-spec](https://github.com/scottcorgan/tap-spec)
