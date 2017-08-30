
```
shell> npm install express body-parser morgan   
shell> npm install passport
shell> npm install passport-local
shell> npm install express-session
```

```js
//  Created by Timmy on 2015/2/24.
//  Copyright (c) 2015年 Timmy. All rights reserved.

// 导入所需模块
var express = require('express');
var app = express();
var bodyParser = require('body-parser');
var morgan = require('morgan');
var path = require('path');
var session = require('express-session');
var passport = require('passport')
  , LocalStrategy = require('passport-local').Strategy
  , FacebookStrategy = require('passport-facebook').Strategy;


var user = {};
user.id = '0';
user.username = 'admin';
user.password = 'secret';

passport.serializeUser(function(user, done) {
  done(null, user.id);
});

passport.deserializeUser(function(id, done) {
  done(null, user);
});

passport.use(new LocalStrategy(function(username, password, done) {
  if (username === user.username && password === user.password) {
    done(null, user);
  } else {
    console.log('Invalid username or password.');
    done(null, false);
  }
}));

passport.use(new FacebookStrategy({
    clientID: 651663714936315,
    clientSecret: '8df95f614b62bd0e8451d9f6d1684a8c',
    callbackURL: "http://ssl.myserver.net.in/auth/facebook/callback"
  },
  function(accessToken, refreshToken, profile, done) {
      done(null, user);
  }
));


app.use(bodyParser.json()); // for parsing application/json
app.use(bodyParser.urlencoded({ extended: true })); // for parsing application/x-www-form-urlencoded

app.use(session({
  secret: 'keyboard cat',
  resave: true,
  saveUninitialized: true }));

app.use(passport.initialize());
app.use(passport.session());

app.get('/', function (req, res) {
  res.send('Welcome!');
});

app.get('/auth/facebook', passport.authenticate('facebook'));

app.get('/auth/facebook/callback',
  passport.authenticate('facebook', { successRedirect: '/',
                                      failureRedirect: '/login' }));

/*
app.get('/helloworld',
  function(req, res, next) {
    if (req.isAuthenticated()) return next();
   // res.sendStatus(401);
    res.redirect('/signin');
  },
  function(req, res) {
    res.send('Hello World!');
  });
*/

function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/signin');
}

// Account Info
app.get('/account', ensureAuthenticated, function(req, res){
  res.json({ user: req.user });
});

// Log Out
app.get('/logout', function(req, res){
  req.logout();
  res.redirect('/signin');
});

app.get('/signin', function (req, res) {
  res.sendFile(__dirname + '/public/signin.html');
});

// Log In
app.post('/login', passport.authenticate('local', { successRedirect: '/',
                                                    failureRedirect: '/signin' }));

app.use(morgan('combined'));
app.use(express.static('public'));

var api = require('./api');
app.use('/api', api);

var server = app.listen(1337, '0.0.0.0', function () {
  var host = server.address().address;
  var port = server.address().port;

  console.log('Example app listening at http://%s:%s', host, port);
});

```

```js
var users = [];
```

#### :books: 參考網站：

- [passport](http://passportjs.org/docs)
- [express-session](https://www.npmjs.com/package/express-session)
- [passport-pass](https://www.npmjs.com/package/passport-pass)
- [active-directory-devquickstarts-openidconnect-nodejs](https://azure.microsoft.com/zh-tw/documentation/articles/active-directory-devquickstarts-openidconnect-nodejs/)