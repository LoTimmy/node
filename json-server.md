### 安裝 {#installing}

```
shell> npm install -g json-server
```

`db.json`
```json
{
  "posts": [{
    "id": 1,
    "title": "json-server",
    "author": "typicode"
  }],
  "comments": [{
    "id": 1,
    "body": "some comment",
    "postId": 1
  }],
  "profile": {
    "name": "typicode"
  }
}
```

`Start JSON Server`
```
shell> json-server --watch db.json
shell> json-server --watch db.json --port 3004

shell> json-server http://example.com/file.json
shell> json-server http://jsonplaceholder.typicode.com/db
```

`http://localhost:3000/posts/1`

```json
{ "id": 1, "title": "json-server", "author": "typicode" }
```

#### :books: 參考網站：
- [json-server](https://www.npmjs.com/package/json-server)
- [json-server](https://github.com/typicode/json-server)