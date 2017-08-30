<img src="http://i.imgur.com/onUAoMT.png" width="100">

`npm - javascript package manager`

```
shell> npm install <package_name>
shell> npm install lodash
shell> npm install <package_name> --save
shell> npm install <package_name> --save-dev

shell> npm uninstall --save lodash

shell> npm install npm@latest -g

shell> npm i -g package

shell> npm init
shell> npm init --yes

shell> npm set init.author.email "wombat@npmjs.com"
shell> npm set init.author.name "ag_dubs"
shell> npm set init.license "MIT"

shell> npm outdated
shell> npm -v

shell> npm install -g jshint
shell> sudo npm install -g jshint

shell> npm uninstall -g jshint

shell> npm config list
shell> npm config ls -l
shell> npm config edit

shell> npm cache ls
shell> npm cache clean

shell> npm update -g jshint

shell> npm help npm
shell> npm help package.json
```

`Updating global packages`
```
shell> npm outdated -g --depth=0
shell> npm update -g
```

`package.json`
```json
{
  "name": "myapp",
  "description": "a really cool app",
  "version": "1.0.0",
  "private": true,
  "engines": {
    "node": "4.1.1"
  }
}
```


#### :books: 參考網站：
- [installing-node](https://docs.npmjs.com/getting-started/installing-node)
- [using-a-package.json](https://docs.npmjs.com/getting-started/using-a-package.json)
- [npm config](https://docs.npmjs.com/cli/config)
- https://docs.npmjs.com/files/package.json
- [npm ls](https://docs.npmjs.com/cli/ls)
- [installing-npm-packages-globally](https://docs.npmjs.com/getting-started/installing-npm-packages-globally)
- [updating-global-packages](https://docs.npmjs.com/getting-started/updating-global-packages)
- https://docs.npmjs.com/misc/coding-style
- [runkit](https://runkit.com/npm)
