```js
"use strict";

/*
function resolveAfter2Seconds(x) {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve(x);
    }, 2000);
  });
}
*/

let resolveAfter2Seconds = x =>
  new Promise(resolve => {
    setTimeout(() => resolve(x), 2000);
  });

(async () => {
  let successMessage = await resolveAfter2Seconds("Success!");
  console.log("Yay! " + successMessage);
})();
```
