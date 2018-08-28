## NW.js/Electron中使用JQuery

### 方法一 引入jquery后进行判断
```
<script src="https://code.jquery.com/jquery-2.2.0.min.js"></script>
<script>if (typeof module === 'object') {window.jQuery = window.$ = module.exports;};</script>
```

参考文献：https://segmentfault.com/q/1010000007597599


### 方法二 引入jQuery之前添加这段代码，用nodeRequire来使用node模块
```
  <script>
      window.nodeRequire = require;
        delete window.require;
        delete window.exports;
        delete window.module;
  </script>
  <script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>
```
参考文献：https://segmentfault.com/q/1010000007597599


### 方法三 安装jQuery模块

npm install jquery

引用jQuery
```
<script>window.$ = window.jQuery = require("jquery");</script>
```

### 方法四
优点

-Works for both browser and electron with the same code
-Fixes issues for ALL 3rd-party libraries (not just jQuery) without having to specify each one
-Script Build / Pack Friendly (i.e. Grunt / Gulp all scripts into vendor.js)
-Does NOT require node-integration to be false
```
  <!-- Insert this line above script imports  -->
  <script>if (typeof module === 'object') {window.module = module; module = undefined;}</script>
  <!-- normal script imports etc  -->
  <script src="js/jquery-3.2.1.min.js"></script>
  <!-- Insert this line after script imports -->
  <script>if (window.module) module = window.module;</script>
```
参考文献：https://stackoverflow.com/questions/32621988/electron-jquery-is-not-defined