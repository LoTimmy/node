
```js
var exec = require('child_process').exec,
    child;

child = exec('cat *.js bad_file | wc -l',
  function (error, stdout, stderr) {
    console.log('stdout: ' + stdout);
    console.log('stderr: ' + stderr);
    if (error !== null) {
      console.log('exec error: ' + error);
    }
});
```

```js
const spawn = require('child_process').spawn;
const ls = spawn('ls', ['-lh', '/usr']);

ls.stdout.on('data', (data) => {
  console.log(`stdout: ${data}`);
});

ls.stderr.on('data', (data) => {
  console.log(`stderr: ${data}`);
});

ls.on('close', (code) => {
  console.log(`child process exited with code ${code}`);
});
```


```js
var proc = require('child_process');
var child = proc.spawn('ls', ['-lh', '/usr']);

child.stdout.on('data', (data) => {
  console.log(`stdout: ${data}`);
});
```

---

#### :books: 參考網站：
- [child_process](https://nodejs.org/api/child_process.html)
