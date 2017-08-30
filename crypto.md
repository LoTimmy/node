
```js
var crypto = require('crypto');
var buf = crypto.randomBytes(32);
// var randomstring = buf.toString('hex').substr(0, 8); // → 3f549018
var randomstring = buf.toString('base64').substr(0, 8); // → idWxZoFX
console.log(randomstring);
```


```js
var crypto = require('crypto');
const secret = 'abcdefg';

// const cipher = crypto.createCipher('aes192', secret);
const cipher = crypto.createCipher('aes-256-cbc', secret);
let encrypted = cipher.update('some clear text data', 'utf8', 'hex');
encrypted += cipher.final('hex');
console.log(encrypted);

// const decipher = crypto.createDecipher('aes192', secret);
const decipher = crypto.createDecipher('aes-256-cbc', secret);
let decrypted = decipher.update(encrypted, 'hex', 'utf8');
decrypted += decipher.final('utf8');
console.log(decrypted);
```

```js
const ciphers = crypto.getCiphers();
console.log(ciphers); // ['aes-128-cbc', 'aes-128-ccm', ...]

const hashes = crypto.getHashes();
console.log(hashes); // ['DSA', 'DSA-SHA', 'DSA-SHA1', ...]
```

#### :books: 參考網站：
- [crypto](https://nodejs.org/api/crypto.html)
- [substr](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substr)