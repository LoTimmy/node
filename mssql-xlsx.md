
```js
var sql = require('mssql'); 
var S = require('string');
var AsciiTable = require('ascii-table');
var XlsxWriter = require('node-simple-xlsx'),
    writer = new XlsxWriter();

var config = {
  user: 'sa',
  password: 'secretsecret',
  server: '10.27.55.218', 
  database: 'mytest'
}

/*
TestData
MyTable 
MyTempTable
myFile.xlsx
*/

var connection = sql.connect(config, function(err) {
  if(err) throw err;

  var table = new AsciiTable('A Title');
  writer.setHeaders(['ProductID', 'ProductName', 'Price', 'ProductDescription']);

  var request = new sql.Request();
  request.stream = true; 
  request.query('select * from Products');

  request.on('recordset', function(columns) {
    // console.dir(columns);
  });

  request.on('row', function(row) {
   // console.dir(row);

    writer.addRow({
      'ProductID': row.ProductID,
      'ProductName': row.ProductName,
      'Price': S(row.Price).toString(),
      'ProductDescription': row.ProductDescription
    });

    table
      .setHeading('ProductID', 'ProductName', 'Price', 'ProductDescription')
      .addRow(row.ProductID, row.ProductName, (S(row.Price).isEmpty()?'':row.Price), (S(row.ProductDescription).isEmpty()?'':row.ProductDescription));
  });

  request.on('error', function(err) {
  });

  request.on('done', function(returnValue) {
    console.log(table.toString());

    writer.pack('myFile.xlsx', function (err) {
      if (err) {
        console.log('Error: ', err);
      } else {
        console.log('Done.');
      }
    });

    connection.close();
  });
});
```
