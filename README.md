![](https://raw.githubusercontent.com/docker-library/docs/master/node/logo.png)

# Introduction

- `JavaScrip`在1995年5月問世。
- `JavaScript`在1996年進行標準化，第一個標準化版本`ECMA-262`於1997年採納，因為`Java`名稱上具有商標問題，`ECMA-262`採用了`ECMAScript`作為語言名稱，`JavaScript`此後成為了`ECMA-262`標準的實作語言，現在的瀏覽器，幾乎都能支援1999年發布的`ECMA-262`第三版以上的實作，又稱`ECMAScript 3`，對應的實作為`JavaScript 1.5`。
- 由於一些政治因素，`ECMAScript 4`發展意見發生分岐，原有規範中的一小部份是就現有功能作了改進，被發布為`ECMAScript 3.1`。後來`ECMAScript 4`被中止，`ECMAScript 3.1`被改名`ECMAScript 5`，並於2009年發布，後續2011年又發布了`ECMAscript 5.1`。
- `ECMAScript 5`的主要特點之一是可宣告`嚴格模式`（`Strict mode`），透過在程式碼中加入'use strict'字串，一些過去被認為不良實踐的語法就會無法使用，嚴格模式下有許多規範，是關於識別字名稱使用上的限制，像是沒有使用var宣告的變數無法使用，不能使用with，不能有重複的參數或特性名稱，不能與保留字或既存的識別字名稱衝突（像是arguments），eval函式評估出來的變數不能在外部使用等，很顯然地，這反映了過去語言在`範疇`（`Scope`）與`名稱空間`（`Namespace`）管理上過於鬆散，因而必須加強範疇與名稱空間管理上的約束。
- 像是`ECMAScript 5`之前，如果this沒有實際對象，也就是this實際上是null或undefined時，會自動轉換為全域物件，這又會造成許多誤判或誤用的問題，嚴格模式下禁止了這個行為，實際上，為了讓開發者能明確掌握this，函式新增了bind函式，可以讓你固定this的對象傳回新函式，讓this不會隨著呼叫者自動變換。在這之前，開發者為了要能更精確掌握this實際對象，避免不清不楚下發生問題，亦會明確地在使用call或apply函式時，指定this的對象。
- `JavaScript`之父`Brendan Eich`（音：艾可，德國姓）。`Brendan Eich`在1995年僅花了10天就開發出`JavaScript`。之所以命名使用了`Java`這四個字母，完全是行銷上考量，他想藉由`Java`的名氣使更多人注意到`JavaScript`。`Brendan Eich`想讓`JavaScript`乍看之下很像是`Java`，但是其實與`Java`非常不一樣。而`Java`和`JavaScript`雖然都屬於物件導向語言，語法和物件的繼承方式卻不同。`Brendan Eich`強調，其中一個很大的差異在於型別，`Java`是靜態型別，也就是說在撰寫`Java`程式碼時，開發者需要先定義變數的型別，`JavaScript`卻不需要，這使得`JavaScript`的程式在開發上，更為彈性且容易，不過這卻也是`JavaScript`的致命傷，動態型別使得`JavaScript`的執行效能受到影響。
- `Java`是由被`Oracle`買下的`Sun`發表，`JavaScript`則是由`Netscape`發表，原本名字叫`LiveScript`，因為`Netscape`在自己的瀏覽器支援`Java Applet`，`Java`又名氣大噪，就把`LiveScript`改名`JavaScript`一起打知名度。而`Netscape`後來把`JavaScript`提交給`ECMA`制定為國際標準，稱做`ECMAScript`，真正跟`JavaScript`是兄弟的是`Adobe Flash`的`ActionScript`和`Microsoft`的`JScript`，因為一樣都是依`ECMAScript`標準建制。
- **`Node.js`是一個可用來開發伺服器端網路應用程式的跨平台運作環境**，允許開發人員以各式`應用程式介面`（`API`）來撰寫應用程式，被視為是全球成長最快的`API`開發框架之一。
- 2009年釋出的`Node.js`為一開放源碼的跨平台運作環境，主要用來開發伺服器端的網路應用程式，包括`IBM`、`微軟`、`Yahoo`、`SAP`、`PayPal`或`GoDaddy`都是Node.js的用戶，雖然在2014年底時，`Node.js`社群因內部意見不合導致有人出走並另創了同類型的`io.js`，不過雙方在今年6月同意透過中立的`Node.js`基金會重新合併，並由`Linux`基金會負責管理。`Node.js 4.0`即是`Node.js`與`io.js`整併後的第一個產品，也是`Node.js`的第一個穩定版，版本別則自7月的0.12.7直接跳到4.0。`Node.js 4.0`採用與最新`Chrome`瀏覽器一致的4.5版V8 `JavaScript`引擎，亦建立了涵蓋`OS X`、`Windows`、`FreeBSD`與`SmartOS`等多種作業系統的測試叢集，並對`ARM`處理器有一流的支援，包含`ARM6`、`ARM7`與最新的64位元`ARM8`等處理器，意味著它已正式準備好要供應給業餘的科技愛好者及`ARM`伺服器用戶來使用。
- `ES6`是`JavaScript`現在2015年標準，與之前版本的語法及概念不同，有相當大的變動。
- 知名開發框架`Node.js`在2014年底鬧內鬨，最後分裂出了`io.js`，歷經了9個月的分手，社群重修舊好，兩個專案再次合併為`Node.js`，並全然納入`io.js`過去更新的程式碼，版本號從0.12一躍到了4.0，在2015年9月時，對外釋出`Node.js 4.0`正式版。這次的更新除了支援新`JavaScript`解析引擎V8外，也支援最新版本`ES6`（`ECMAScript6`）的`JavaScript`規格，另外，`Node.js`也在0.12版開始提供`長期支援`（`Long Term Support`，`LTS`）版本，顯示`Node.js`進入成熟發展階段。由於新版`JavaScript`解析引擎V8完全支援`ES6`的新功能，因此`Node.js`在搶先支援`ES6`後，也開始可以使用諸多`ES6`才有的新特色，像是習慣C++的開發者，在`Node.js`終於能夠使用`類別`（`Class`）。另外，`ES6`還支援了`Generator`，因此新版`Node.js`的開發者可以用更高效率的方法處理遞迴問題。`Node.js`經過一段時間的發展，逐漸趨於成熟與穩定，而提供長期支援版本便是一個重要的指標，因為企業能夠有計畫的掌握版本更新時程，`Node.js`每12個月會釋出一個長期支援版本，而這個版本會被維護18個月。另外，`Node.js 4.0`在效能上也有長足的進步，經國外開發者以`Apache HTTP`伺服器指標工具測試後，發現`Node.js 4.0`能比前一版本少用一半以上的記憶體，但仍維持同樣的效能。
- 網頁語言`JavaScript`不只用於前端網頁，進幾年越來越多伺服器端程式採用`Node.js`框架來開發後端需要的應用程式
- `Node.js`是基於`Google`所開發出名為`V8`的`JavaScript`引擎所創造出來的`Framework`。它特別的地方在於，一般由`JavaScript`開發出來的套件，通常都是應用在網路前端平臺上，像是`jQuery`等，而`Node.js`卻可以用來開發後端的應用程式。以往`JavaScript`都是運行在瀏覽器上，而`Node.js`的出現，可以將`JavaScript`變成一個通用平臺的語言使用，因此可以讓它做任何事情。而`Node.js`在伺服器應用上的效能不錯，反應速度也很快。`Python`及`Ruby`等語言在這方面的效率，就比不上`Node.js`了，而這也是它的優勢。
- `回呼` (`Callback`)，當實作程式出現許多重複流程，僅小部份需要特定實作時，可以將重複流程實作為樣版，而特定實作由呼叫者提供回呼物件或函式，例如對`JavaScript`的陣列排序可以寫為[1, 3, 2, 5, 4].sort(function(a, b) { return a - b; })。
- `NW.js`為一結合`Node.js`與`Chromium`專案的`JavaScript`應用程式開發框架，可用來打造支援`Windows`、`Mac OS X`與`Linux`的應用程式，有別於瀏覽器對`JavaScript`程式碼的沙箱執行限制，`NW.js`移除了相關的限制，並允許程式直接與作業系統互動。`NW.js`除了允許程式在不同的平台上運作之外，也讓開發人員更容易把網路程式轉成桌面程式。
- `NW.js`的最大優勢在於它所需的`.Net`或`Java`運行環境都已經安裝在各個系統上了。

- https://www.npmjs.com/package/nodemon
- https://www.npmjs.com/package/async
- https://www.npmjs.com/package/bcrypt-nodejs
- https://www.npmjs.com/package/bitgo
- https://www.npmjs.com/package/cheerio
- https://www.npmjs.com/package/clockwork
- https://www.npmjs.com/package/connect-mongo
- https://www.npmjs.com/package/dotenv
- https://www.npmjs.com/package/express
- https://www.npmjs.com/package/body-parser
- https://www.npmjs.com/package/express-session
- https://www.npmjs.com/package/morgan
- https://www.npmjs.com/package/compression
- https://www.npmjs.com/package/errorhandler
- https://www.npmjs.com/package/serve-favicon
- https://www.npmjs.com/package/node-sass-middleware
- https://www.npmjs.com/package/express-flash
- https://www.npmjs.com/package/fbgraph
- https://www.npmjs.com/package/github-api
- https://www.npmjs.com/package/mongoose
- https://www.npmjs.com/package/nodemailer
- https://www.npmjs.com/package/passport
- https://www.npmjs.com/package/passport-local
- https://www.npmjs.com/package/passport-facebook
- https://www.npmjs.com/package/passport-oauth
- https://www.npmjs.com/package/request
- https://www.npmjs.com/package/lodash
- https://www.npmjs.com/package/validator
- https://www.npmjs.com/package/geoip-lite
- http://numeraljs.com/
- https://filesizejs.com/
- https://github.com/bluesmoon/node-geoip

---

- http://realfavicongenerator.net/
- http://todc.github.io/todc-bootstrap/
- http://fontawesome.io/icons/
- http://framework7.io/
- https://github.com/rstacruz/nprogress
- http://github.hubspot.com/offline/docs/welcome/
- http://fabien-d.github.io/alertify.js/
- http://github.hubspot.com/drop/docs/welcome/
- http://dimsemenov.com/plugins/magnific-popup/