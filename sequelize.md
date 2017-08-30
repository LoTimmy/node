### 安裝 {#installing}

```
npm install --save sequelize
npm install --save mysql
npm install --save sqlite3
npm install --save tedious // MSSQL
```

```js
var Sequelize = require('sequelize');

var sequelize = new Sequelize('database', 'username', 'password', {});
var sequelize = new Sequelize('my_database', 'john', 'doe', {
  host: 'localhost',
  dialect: 'mysql',
  port : '3306'
});

var Employee = sequelize.define('Employee', {
  name: { type: Sequelize.STRING },
  address: { type: Sequelize.STRING },
  flag: { 
    type: Sequelize.BOOLEAN, 
    allowNull: false, 
    defaultValue: true
  },
  title: { 
    type: Sequelize.STRING, 
    allowNull: false, 
    comment: "I'm a comment!"
  },
  description: {
    type: Sequelize.TEXT, 
    allowNull: true, 
    comment: "I'm a comment!"
  },
  myDate: { 
    type: Sequelize.DATE, 
    defaultValue: Sequelize.NOW, 
    comment: "I'm a comment!"
  }
}, {
  engine: 'MYISAM',
  comment: "I'm a table comment!" 
});

Employee.sync();
Employee.sync({force: true}) 

Employee
  .create({ name: 'John Doe', title: 'senior engineer' })
  .then(function(employee) {
    console.log(employee.get('name')); // John Doe (SENIOR ENGINEER)
    console.log(employee.get('title')); // SENIOR ENGINEER
  })

Employee
  .findAll({
  })
  .then(function(result) {
    console.log(result.count);
    console.log(result.rows);
  });
```

#### :books: 參考網站：
- [sequelize](http://docs.sequelizejs.com/en/latest/api/sequelize/)
- [sequelize](http://docs.sequelizejs.com/en/1.7.0/docs/usage/)
