![](https://nodemailer.com/nm_logo_200x136.png)

### 安裝 {#installing}

```
shell> npm install nodemailer --save
```

```js
'use strict';
const nodemailer = require('nodemailer');

let transporter = nodemailer.createTransport({
    service: 'gmail',
    auth: {
        user: 'gmail.user@gmail.com',
        pass: 'yourpass'
    }
});

let mailOptions = {
    from: '"Fred Foo 👻" <foo@blurdybloop.com>', // sender address
    to: 'bar@blurdybloop.com, baz@blurdybloop.com', // list of receivers
    subject: 'Hello ✔', // Subject line
    text: 'Hello world ?', // plain text body
    html: '<b>Hello world ?</b>' // html body
};

transporter.sendMail(mailOptions, (error, info) => {
    if (error) {
        return console.log(error);
    }
    console.log('Message %s sent: %s', info.messageId, info.response);
});
```

```js
'use strict';
const nodemailer = require('nodemailer');

let transporter = nodemailer.createTransport({
    service: 'gmail',
    auth: {
        user: 'gmail.user@gmail.com',
        pass: 'yourpass'
    }
});
```

---

```js
var message = {
    from: 'sender@server.com',
    to: 'receiver@sender.com',
    subject: 'Message title',
    text: 'Plaintext version of the message',
    html: '<p>HTML version of the message</p>'
};

var message = {
    ...,
    headers: {
        'My-Custom-Header': 'header value'
    },
    date: new Date('2000-01-01 00:00:00')
};

var htmlstream = fs.createReadStream('content.html');
transport.sendMail({html: htmlstream}, function(err){
    if(err){
        // check if htmlstream is still open and close it to clean up
    }
});
```
---

```js
let smtpConfig = {
    host: 'smtp.gmail.com',
    port: 587,
    secure: false, // upgrade later with STARTTLS
    auth: {
        user: 'user@gmail.com',
        pass: 'pass'
    }
};

let poolConfig = {
    pool: true,
    host: 'smtp.gmail.com',
    port: 465,
    secure: true, // use TLS
    auth: {
        user: 'user@gmail.com',
        pass: 'pass'
    }
};

transporter.verify(function(error, success) {
   if (error) {
        console.log(error);
   } else {
        console.log('Server is ready to take our messages');
   }
});
```

---

```js
'use strict';
const nodemailer = require('nodemailer');

let poolConfig = {
    pool: true,
    host: '192.168.2.93',
    port: 25,
    secure: false,
    ignoreTLS: true,
/*
    auth: {
        user: '',
        pass: ''
    }
*/
};

let transporter = nodemailer.createTransport(poolConfig);

transporter.verify(function(error, success) {
   if (error) {
        console.log(error);
   } else {
        console.log('Server is ready to take our messages');
   }
});
```


#### :books: 參考網站：
- [nodemailer](https://nodemailer.com/)
