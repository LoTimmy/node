<img src="http://garthdb.com/img/jade_branding/jade-01.svg" width="20%" height="20%">

### 安裝 {#installing}

```
shell> npm install jade
shell> npm install jade -g

shell> npm install pug
```

```jade
doctype html
html(lang="en")
  head
    title= pageTitle
    script(type='text/javascript').
      if (foo) bar(1 + 5)
  body
    h1 Jade - node template engine
    #container.col
      if youAreUsingJade
        p You are amazing
      else
        p Get on it!
      p.
        Jade is a terse and simple templating language with a
        strong focus on performance and powerful features.
```
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Jade</title>
    <script type="text/javascript">
      if (foo) bar(1 + 5)
    </script> 
  </head>
  <body>
    <h1>Jade - node template engine</h1>
    <div id="container" class="col">
      <p>You are amazing</p>
      <p>Jade is a terse and simple templating language with a strong focus on performance and powerful features.</p>
    </div>
  </body>
</html>

```

---

<img src="https://camo.githubusercontent.com/a43de8ca816e78b1c2666f7696f449b2eeddbeca/68747470733a2f2f63646e2e7261776769742e636f6d2f7075676a732f7075672d6c6f676f2f656563343336636565386664396431373236643738333963626539396431663639343639326330632f5356472f7075672d66696e616c2d6c6f676f2d5f2d636f6c6f75722d3132382e737667" width="20%" height="20%">

`template.pug`

```jade
p #{name}'s Pug source code!
```
```js
const pug = require('pug');

// Compile the source code
const compiledFunction = pug.compileFile('template.pug');

// Render a set of data
console.log(compiledFunction({
  name: 'Timothy'
}));
// "<p>Timothy's Pug source code!</p>"

// Render another set of data
console.log(compiledFunction({
  name: 'Forbes'
}));
// "<p>Forbes's Pug source code!</p>"
```

---

### Attributes {#attributes}

```jade
a(href='google.com') Google
a(class='button' href='google.com') Google

input(
  type='checkbox'
  name='agreement'
  checked
)
```
```html
<a href="google.com">Google</a>
<a class="button" href="google.com">Google</a>

<input type="checkbox" name="agreement" checked="checked" />
```

```jade
a.button
.content

a#main-link
#content

div#foo(data-bar="foo")&attributes({'data-foo': 'bar'})
```
```html
<a class="button"></a>
<div class="content"></div>

<a id="main-link"></a>
<div id="content"></div>

<div id="foo" data-bar="foo" data-foo="bar"></div>
```
---

### Comments {#comments}

```jade
// just some paragraphs
p foo
p bar
```
```html
<!-- just some paragraphs-->
<p>foo</p>
<p>bar</p>
```

```jade
//- will not output within markup
p foo
p bar
```
```html
<p>foo</p>
<p>bar</p>
```

```jade
body
  //
    As much text as you want
    can go here.
```
```html
<body>
  <!--As much text as you want
can go here.-->
</body>
```

```jade
<!--[if IE 8]>
<html lang="en" class="lt-ie9">
<![endif]-->
<!--[if gt IE 8]><!-->
<html lang="en">
<!--<![endif]-->
```
```
<!--[if IE 8]>
<html lang="en" class="lt-ie9">
<![endif]-->
<!--[if gt IE 8]><!-->
<html lang="en">
<!--<![endif]-->
```

---

### Mixins {#mixins}
```jade
//- Declaration
mixin list
  ul
    li foo
    li bar
    li baz
//- Use
+list
+list
```
```html
<ul>
  <li>foo</li>
  <li>bar</li>
  <li>baz</li>
</ul>
<ul>
  <li>foo</li>
  <li>bar</li>
  <li>baz</li>
</ul>
```

```jade
mixin pet(name)
  li.pet= name
ul
  +pet('cat')
  +pet('dog')
  +pet('pig')
```
```html
<ul>
  <li class="pet">cat</li>
  <li class="pet">dog</li>
  <li class="pet">pig</li>
</ul>
```

```jade
mixin article(title)
  .article
    .article-wrapper
      h1= title
      if block
        block
      else
        p No content provided

+article('Hello world')

+article('Hello world')
  p This is my
  p Amazing article
```
```html
<div class="article">
  <div class="article-wrapper">
    <h1>Hello world</h1>
    <p>No content provided</p>
  </div>
</div>
<div class="article">
  <div class="article-wrapper">
    <h1>Hello world</h1>
    <p>This is my</p>
    <p>Amazing article</p>
  </div>
</div>
```

```jade
mixin link(href, name)
  //- attributes == {class: "btn"}
  a(class!=attributes.class href=href)= name

+link('/foo', 'foo')(class="btn")

mixin link(href, name)
  a(href=href)&attributes(attributes)= name

+link('/foo', 'foo')(class="btn")
```
```html
<a class="btn" href="/foo">foo</a>
```

```jade
mixin list(id, ...items)
  ul(id=id)
    each item in items
      li= item

+list('my-list', 1, 2, 3, 4)
```
```html
<ul id="my-list">
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
</ul>
```

---

#### :books: 參考網站：
- [jade](https://www.npmjs.com/package/jade)
- [pug](https://pugjs.org/api/getting-started.html)
- [pug](https://github.com/pugjs/pug)
- [attributes](https://pugjs.org/language/attributes.html)
