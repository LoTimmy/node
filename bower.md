### 安裝 {#installing}

```
shell> npm install -g bower
shell> yarn global add bower
```

`Install with Bower`
```
shell> bower install <package>
```

```
shell> bower search jquery
shell> bower info  extjs

shell> bower install jquery
shell> bower install jquery --allow-root

shell> bower install bootstrap --allow-root
shell> bower install bootstrap-css --allow-root
shell> bower install font-awesome --allow-root

shell> bower install extjs#4.2.1-883 --allow-root

shell> bower install extjs --allow-root
shell> bower install cocos2d-html5

shell> bower install react --allow-root

shell> bower update jquery 

shell> bower uninstall jquery 
```

```
shell> bower init
shell> bower list
```

`.bowerrc`
```
{
  "directory": "app/bower_components/"
}
```

`bower.json`
```
{
  "name": "custom-bower-resolver",
  "version": "1.0.0",
  "dependencies": {
    "jquery": "^1.8.3",

  }
}
```

```html
<script src="bower_components/jquery/dist/jquery.min.js"></script>

<!--[if lt IE 9]>
    <script src="bower_components/html5shiv/dist/html5shiv.js"></script>
<![endif]-->
```


```
bower ESUDO         Cannot be run with sudo

Additional error details:
Since bower is a user command, there is no need to execute it with superuser permissions.
If you're having permission errors when using bower without sudo, please spend a few minutes learning more about how your system should work and make any necessary repairs.

http://www.joyent.com/blog/installing-node-and-npm
https://gist.github.com/isaacs/579814

You can however run a command with sudo using --allow-root option
```

```
shell> bower install loadcss --allow-root
```

```html
<head>
...
<script>
  // include loadCSS here...
  function loadCSS( href, before, media ){ ... }
  // load a file
  loadCSS( "path/to/mystylesheet.css" );
</script>
<noscript><link href="path/to/mystylesheet.css" rel="stylesheet"></noscript>
...
</head>
```

---

```
shell> bower install html5shiv --allow-root
shell> bower install respond --allow-root
```

```html
<!-- HTML5 shim and Respond.js for IE8 support of HTML5 elements and media queries -->
<!--[if lt IE 9]>
  <script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script>
  <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
<![endif]-->

<!--[if lt IE 9]>
  <script src="bower_components/html5shiv/dist/html5shiv.js"></script>
  <script src="bower_components/respond/dest/respond.min.js"></script>
<![endif]-->
```

#### :books: 參考網站：
- [html5shiv](https://github.com/afarkas/html5shiv)

---

#### :books: 參考網站：
- [bower](http://bower.io/)
- [bower](http://bower.io/docs/api/)
- [bower](http://learn.jquery.com/jquery-ui/environments/bower/)
