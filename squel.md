```
shell> npm install squel
```

```js
var squel = require("squel");

// SELECT * FROM table 
squel.select().from("table").toString();

// SELECT `t1`.`id`, `t1`.`name` as "My name", `t1`.`started` as "Date" FROM table `t1` ORDER BY id ASC LIMIT 20 
squel.select({ autoQuoteFieldNames: true })
    .from("table", "t1")
    .field("t1.id")
    .field("t1.name", "My name")
    .field("t1.started", "Date")
    .order("id")
    .limit(20)
    .toString()
```

---

#### :books: 參考網站：
- [squel](https://hiddentao.github.io/squel/)
- [squel](https://www.npmjs.com/package/squel)
