![](http://jshint.com/res/jshint.png) 

### 安裝 {#installing}

```
shell> npm install -g jshint
shell> jshint
```

```js
function main() {
  "use strict";
  return 'Hello, World!';
}

main();
```

`.jshintrc`
```json
{
  "strict" : true,
  "undef"   : true,
  "validthis" : true,
  "node"   : true,
  "esversion" : 6,
  "curly"  : true,
  "unused" : true
}
```

`Semicolon` [͵sɛmɪˋkolən] `分號`
`Expected` [ɪkˋspɛktɪd] `需要`

---

#### :books: 參考網站：

- [jshint](https://www.npmjs.com/package/jshint)
- [docs](http://jshint.com/docs/options/)
- [option-validthis-cant-be-used-in-a-global-scope](https://jslinterrors.com/option-validthis-cant-be-used-in-a-global-scope)
- [Strict_mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)

---

<img src="http://eslint.org/img/logo.svg" alt="eslint" width=58 height=58>

`ESLint`  

### 安裝 {#installing}

```
shell> npm install -g eslint
shell> eslint --init
```

`.eslintrc`
```json
{
  "rules": {
    "semi": ["error", "always"],
    "quotes": ["error", "single"]
  }
}
```

```
"eqeqeq": "off",
"eqeqeq": "warn"

"strict": "off"
"strict": "warn"
"strict": "error"

"curly": "error",
"quotes": ["error", "double"],
"quotes": ["error", "single"],

"indent": ["error", 4],
"linebreak-style": ["error", "unix"],
"semi": ["error", "always"],
"one-var": "off", // ["error", "never"]
"no-console": "off",
"no-cond-assign": ["error", "always"],
"no-inline-comments": "off",
"comma-dangle": ["error", "always"],

```

```json
{
  "extends": "google",
  "installedESLint": true
}
```

```
'use strict';
```

```
function doSomething() {
}
```

```
Complete!
```

#### :books: 參考網站：
- [eslint](http://eslint.org/)
- [quotes](http://eslint.org/docs/rules/quotes)
- [strict](http://eslint.org/docs/rules/strict)
- [code-conventions](http://eslint.org/docs/developer-guide/code-conventions)