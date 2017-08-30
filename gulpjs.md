<img src="https://pbs.twimg.com/profile_images/417078109075034112/iruTC031_400x400.png" width="100">

`gulpjs`

- **`gulp`** `[gʌlp]`

### 安裝 {#installing}

```
shell> npm install gulp -g
shell> gulp -v
[11:41:53] CLI version 3.9.1
```

### Hello world 範例 {#hello-world}

```
shell> mkdir gulp
shell> npm install gulp
shell> gulp -v
[11:44:29] CLI version 3.9.1
[11:44:29] Local version 3.9.1

shell> touch gulpfile.js
```

```
var gulp = require('gulp');
gulp.task('default', function() {
  console.log("Hello World!");
});
```

```
shell> gulp default
```
---

```
gulp.task('one', function(done) {
  // do stuff
  done();
});

gulp.task('two', function(done) {
  // do stuff
  done();
});

gulp.task('three', three);

function three(done) {
  done();
}
three.description = "This is the description of task three";
```

```
shell> gulp --tasks
shell> gulp --tasks-simple
```
---

```
shell> mkdir gulp
shell> npm init -y
shell> npm install --save-dev gulp gulp-concat gulp-uglify gulp-uglifycss gulp-imagemin gulp-size gulp-cache jshint gulp-jshint del
```

```
var gulp = require('gulp');
var concat = require('gulp-concat');
var uglify = require('gulp-uglify');
var uglifycss = require('gulp-uglifycss');
const imagemin = require('gulp-imagemin');
const jshint = require('gulp-jshint');
const size = require('gulp-size');
const del = require('del');
var cache = require('gulp-cache');
var sourcemaps = require('gulp-sourcemaps');

gulp.task('lint', function() {
  return gulp.src('src/js/*.js')
    .pipe(jshint())
    .pipe(jshint.reporter('default'));
});

gulp.task('clean', function() {
  return del(['dist']);
});

gulp.task('scripts', ['clean'], function() {
// gulp.task('scripts', function() {
  return gulp.src('src/js/*.js')
    .pipe(sourcemaps.init())
    .pipe(concat('all.js'))
    .pipe(sourcemaps.write())
    .pipe(uglify())
    .pipe(gulp.dest('dist/js'));
});

gulp.task('css', ['clean'], function() {
// gulp.task('css', function() {
  return gulp.src('src/styles/*.css')
    .pipe(concat('style.css'))
    .pipe(uglifycss())
    .pipe(gulp.dest('dist/css'));
});

gulp.task('images', ['clean'], () =>
// gulp.task('images', () =>
  //  gulp.src('src/images/*')
  gulp.src('src/images/**/*')
  // .pipe(imagemin())
  .pipe(cache(imagemin()))
  .pipe(size())
  .pipe(gulp.dest('dist/images'))
);

gulp.task('default', ['lint', 'scripts', 'css', 'images'], function() {
  return gulp.src('src/index.html')
    .pipe(gulp.dest('dist'));
});
```

#### :books: 參考網站：
- [gulpjs](http://gulpjs.com/)
- [gulpjs](https://github.com/gulpjs)
- [gulp](https://gulp.readme.io/docs)
- [plugins](http://gulpjs.com/plugins/)
- [gulp-concat](https://www.npmjs.com/package/gulp-concat)
- [gulp-uglify](https://www.npmjs.com/package/gulp-uglify/)
- [gulp-uglifycss](https://www.npmjs.com/package/gulp-uglifycss/)
- [gulp-imagemin](https://www.npmjs.com/package/gulp-imagemin/)
- [gulp-size](https://www.npmjs.com/package/gulp-size) 


### gulp-jshint {#gulp-jshint}

```
shell> npm install jshint gulp-jshint
```

```
const jshint = require('gulp-jshint');
const gulp   = require('gulp');

gulp.task('lint', function() {
  return gulp.src('./lib/*.js')
    .pipe(jshint())
    .pipe(jshint.reporter('default'));
});
```

```
const jshint = require('gulp-jshint');
const gulp   = require('gulp');
var cache = require('gulp-cache');

gulp.task('lint', function() {
  gulp.src('./lib/*.js')
    .pipe(cache(jshint('.jshintrc'), {
      key: makeHashKey,
      success: function(jshintedFile) {
        return jshintedFile.jshint.success;
      },
      value: function(jshintedFile) {
        return {
          jshint: jshintedFile.jshint
        };
      }
    }))
    .pipe(jshint.reporter('default'));
});

var jsHintVersion = '2.4.1',
  jshintOptions = fs.readFileSync('.jshintrc');

function makeHashKey(file) {
  return [file.contents.toString('utf8'), jshintVersion, jshintOptions].join('');
}
```

#### :books: 參考網站：
- [gulp-jshint](https://github.com/spalger/gulp-jshint)
- [jshint](http://jshint.com/install/)


### del {#del}

```
shell> npm install del
```

```
var gulp = require('gulp');
const del = require('del');

del(['tmp/*.js', '!tmp/unicorn.js']).then(paths => {
    console.log('Deleted files and folders:\n', paths.join('\n'));
});
```

#### :books: 參考網站：
- [del](https://www.npmjs.com/package/del)

### gulp-cache {#gulp-cache}

```
shell> npm install gulp-cache
```

```
var gulp = require('gulp');
const imagemin = require('gulp-imagemin');
var cache = require('gulp-cache');

gulp.task('images', () =>
    gulp.src('src/images/*')
        .pipe(cache(imagemin()))
        .pipe(size())
        .pipe(gulp.dest('dist/images'))
);
```

```
var gulp = require('gulp');
var cache = require('gulp-cache');
 
gulp.task('clear', function (done) {
  return cache.clearAll(done);
});
```

#### :books: 參考網站：
- [gulp-cache](https://www.npmjs.com/package/gulp-cache)

### gulp.watch {#gulp.watch}

```
gulp.watch('js/**/*.js', gulp.parallel('uglify', 'reload'));
```

#### :books: 參考網站：
- [gulp.watch](https://gulp.readme.io/docs/gulpwatchglob-opts-fn)

### gulp-sourcemaps {#gulp-sourcemaps}

```
var gulp = require('gulp');
var concat = require('gulp-concat');
var sourcemaps = require('gulp-sourcemaps');
 
gulp.task('javascript', function() {
  return gulp.src('src/**/*.js')
    .pipe(sourcemaps.init())
      .pipe(concat('all.js'))
    .pipe(sourcemaps.write())
    .pipe(gulp.dest('dist'));
});
```
#### :books: 參考網站：
- [gulp-sourcemaps](https://www.npmjs.com/package/gulp-sourcemaps)

---

### gulp-html-beautify {#gulp-html-beautify}
```
var gulp = require('gulp');
var htmlbeautify = require('gulp-html-beautify');

gulp.task('htmlbeautify', function() {
  var options = {
    "indent_size": 4,
  };
  gulp.src('./src/*.html')
    .pipe(htmlbeautify(options))
    .pipe(gulp.dest('./public/'))
});

```

#### :books: 參考網站：
- [gulp-html-beautify](https://www.npmjs.com/package/gulp-html-beautify)

---

### critical {#critical}
```js
var gulp = require('gulp');
var gutil = require('gulp-util');
var critical = require('critical').stream;

// Generate & Inline Critical-path CSS
gulp.task('critical', function () {
    return gulp.src('dist/*.html')
        .pipe(critical({base: 'dist/', inline: true, css: ['dist/styles/components.css','dist/styles/main.css']}))
        .on('error', function(err) { gutil.log(gutil.colors.red(err.message)); })
        .pipe(gulp.dest('dist'));
});
```

#### :books: 參考網站：
- https://github.com/addyosmani/critical

---

```js
var gulp = require('gulp')
var mjml = require('gulp-mjml')

gulp.task('default', function () {
  return gulp.src('./test.mjml')
    .pipe(mjml())
    .pipe(gulp.dest('./html'))
})
```

```js
var gulp = require('gulp')
var mjml = require('gulp-mjml')

// Require your own components if needed, and your mjmlEngine (possibly with options)
// require('./components')
var mjmlEngine = require('mjml')

gulp.task('default', function () {
  return gulp.src('./test.mjml')
    .pipe(mjml(mjmlEngine, {minify: true}))
    .pipe(gulp.dest('./html'))
})
```

#### :books: 參考網站：
- https://github.com/mjmlio/gulp-mjml

---

#### :books: 參考網站：
- [gulp-git](https://www.npmjs.com/package/gulp-git)
