### css & js

- [基于display:table的CSS布局](http://www.frontopen.com/331.html)：如果我们为元素使用“display:table-cell;”属性，而不将其父容器设置为“display:table-row;”属性，浏览器会默认创建出一个表格行，就好像文档中真的存在一个被声明的表格行一样。

- [Table布局-display:table](http://www.css88.com/archives/6308)

  - table：指定对象作为块元素级的表格。类同于html标签`<table>`（CSS2）
  - inline-table：指定对象作为内联元素级的表格。类同于html标签`<table>`（CSS2）
  - table-caption：指定对象作为表格标题。类同于html标签`<caption>`（CSS2）
  - table-cell：指定对象作为表格单元格。类同于html标签`<td>`（CSS2）
  - table-row：指定对象作为表格行。类同于html标签`<tr>`（CSS2）
  - table-row-group：指定对象作为表格行组。类同于html标签`<tbody>`（CSS2）
  - table-column：指定对象作为表格列。类同于html标签`<col>`（CSS2）
  - table-column-group：指定对象作为表格列组显示。类同于html标签`<colgroup>`（CSS2）
  - table-header-group：指定对象作为表格标题组。类同于html标签`<thead>`（CSS2）
  - table-footer-group：指定对象作为表格脚注组。类同于html标签`<tfoot>`（CSS2）

- 几个 es6 的便捷写法：https://medium.com/dailyjs/7-hacks-for-es6-developers-4e24ff425d0b

- Array.map方法是并发执行的：

  ```
  // 打开 http://es6.ruanyifeng.com/#docs/promise ，再打开控制台，执行以下代码。
  // 从执行结果可以看出：
  //    map(callback)中的callback是`按数组顺序`、`并发`执行的，
  //    每个callback内部等待await返回后才结束执行

  let maps = [0,1,2,3,4,5,6,7,8,9];
  maps.map(async (el, idx) => {
      console.log('callback start: ', idx);
      const response = await fetch('http://es6.ruanyifeng.com/#docs/promise').then(() => {
          console.log('%cpromise done: %s', 'color: green', idx);
      });
      console.log('callback end: ', idx);
      return  null;
  });
  ```

- [js之对象序列化详解](http://www.cnblogs.com/craftsman-gao/p/5130567.html)，JSON.stringify 和 JSON.parse

- 序列化的目的是为了存储和传输，不准确地说：将对象状态信息转化为字符串

- [结构化克隆算法](https://developer.mozilla.org/zh-CN/docs/Web/Guide/API/DOM/The_structured_clone_algorithm) 与 JSON 序列化对比

### sass 、compass

- sass : http://www.w3cplus.com/sassguide/
- compass : http://www.ruanyifeng.com/blog/2012/11/compass.html
- Compass用法指南 : http://www.ruanyifeng.com/blog/2012/11/compass.html
- 使用Sass和Compass制作雪碧图：http://www.w3cplus.com/preprocessor/intermediate/spriting-with-sass-and-compass.html
- Compass重置模块位于样式表的前边，只要被引入就会执行global-reset这一混合器:http://www.ituring.com.cn/tupubarticle/713
- 图灵社区：<http://www.ituring.com.cn/tupubarticle/713>
- <http://www.cnblogs.com/laayoune/p/4105415.html>
- <https://ruby-china.org/topics/4396>
- How to structure a Sass project : <http://thesassway.com/beginner/how-to-structure-a-sass-project>
- e.g.《[Sass Twitter Bootstrap](https://github.com/jlong/sass-twitter-bootstrap/tree/master/lib)》
- e.g.《[Breakpoint](https://github.com/lesjames/breakpoint/tree/master/breakpoint)》
- e.g.《[Octopress](https://github.com/imathis/octopress/tree/master/.themes/classic/sass)》
- Sass Guidelines之一、二、三…：<http://www.w3cplus.com/preprocessor/sass-guidelin-part-1.html>

### Node

- exports 和 module.exports 的区别：

  > https://cnodejs.org/topic/5231a630101e574521e45ef8

  ```
  1、module.exports 初始值为一个空对象 {}
  2、exports 是指向的 module.exports 的引用
  3、require() 返回的是 module.exports 而不是 exports

  系统自动给 nodejs 文件增加2个变量 exports 和 module, module 又有一个属性 exports, 这个exports 属性指向一个空对象 {}; 同时 exports这个变量也指向了这个空对象{};

  于是就有了 exports => {} <= module.exports.

  这 2 个 exports 其实是没有直接关系的,唯一的关系是: 他们初始都指向同一个空对象{};

  module.exports = somethings 是对 module.exports 进行了覆盖，此时 module.exports 指向了新的内存块，而 exports 还是指向原来的内存块，module.exports 和 exports 的关系就断裂了
  ```

  > Node.js 官方文档的截图：
  > ![module exports exports](https://user-images.githubusercontent.com/1653891/36019882-9d4549d0-0dbb-11e8-9fbf-75098def200b.png)

- Node 路径：https://www.jianshu.com/p/aeb3d4318d07

  ```
    __dirname：    获得当前执行文件所在目录的完整目录名
    __filename：   获得当前执行文件的带有完整绝对路径的文件名
    process.cwd()：获得当前执行node命令时候的文件夹目录名
    ./：           不使用require时候，./与process.cwd()一样，使用require时候，与__dirname一样
  ```

- [前端扫盲-之打造一个Node命令行工具](http://www.imooc.com/article/3156)

### generator


- yield命令是异步两个阶段的分界线(http://www.ruanyifeng.com/blog/2015/04/generator.html)
- Generator 函数。它不同于普通函数，是可以暂停执行的，所以函数名之前要加星号，以示区别。
 - 调用 Generator 函数，会返回一个内部指针
 - 指针对象的 throw 方法抛出的错误，可以被函数体内的 try ... catch 代码块捕获


### webpack.config

- resolve：处理路径等（不准确描述）。用于帮助找到模块的绝对路径等等，[doc](https://doc.webpack-china.org/concepts/module-resolution)
- lodaer：处理模块。


### Babel 的 `Stage-X`

- [Stage 0](https://babeljs.io/docs/plugins/preset-stage-0/) - Strawman: just an idea, possible Babel plugin.
- [Stage 1](https://babeljs.io/docs/plugins/preset-stage-1/) - Proposal: this is worth working on.
- [Stage 2](https://babeljs.io/docs/plugins/preset-stage-2/) - Draft: initial spec.
- [Stage 3](https://babeljs.io/docs/plugins/preset-stage-3/) - Candidate: complete spec and initial browser implementations.
- Stage 4 - Finished: will be added to the next yearly release.
- see [here](https://babeljs.io/docs/plugins/#presets)

### js-bridge

Android平台Webview和JS的交互方式共有三种:

- ExposedJsApi：js直接调用java对象的方法；（同步）
- 重载chromeClient的prompt 截获方案；(异步)
- url截获+webview.loadUrl回调的方案；（异步）

为了和IOS保持一致的JSAPI，只能选用第三套方案；
> 来自：http://www.jianshu.com/p/90d1bee2f3c9

- https://github.com/lzyzsd/JsBridge/blob/master/library/src/main/java/com/github/lzyzsd/jsbridge/BridgeUtil.java

### PWA

- 什么是 PWA？https://lavas.baidu.com/mip/doc/README
- service worker
- app shell 
- app manifest
- push notification
- Background Sync

### 网络 & 存储

- 关于多路复用：https://baike.baidu.com/item/%E5%A4%9A%E8%B7%AF%E5%A4%8D%E7%94%A8/1180849?fr=aladdin
  - 频分多路复用
  - 时分多路复用
  - 码分多路复用
  - etc.
- 初识 HTTP 缓存：https://juejin.im/post/5a0937b0f265da431e164193
- [HttpRequest中常见的四种ContentType](https://www.cnblogs.com/xiaozong/p/5732332.html)


- 块存储、文件存储、对象存储这三者的本质差别是什么？：https://www.zhihu.com/question/21536660

### Other

- [《Koa2进阶学习笔记》](https://chenshenhai.github.io/koa2-note/)

- cjs-to-es6
- 安装 .ipa 到 simulator：1、xcode-select —install；2、xcrun simctl install booted xxx
- Weinre 全称 **We**b **In**spector **Re**mote
- 对于常见编译型语言来说，编译步骤分为：词法分析->语法分析->语义检查->代码优化->字节生成。
- 对于解释型语言来说，通过词法分析和语法分析得到语法树后，就可以开始解释执行了。js 是需要预编译的。
- [记一次“失利后”经过半年准备通过阿里社招的经历与感悟](https://juejin.im/post/5a76be55f265da4e9f6f7ded)
  - 源于业务并高于业务的沉淀，业务与技术相结合的深度
  - 技术沉淀：每周周末坚持沉淀自己
  - 博客：https://github.com/Aaaaaaaty/blog

- git cz 类型说明：
  - feat: 新功能(feature)
  - fix: 修复缺陷
  - docs: 仅文档更新
  - style: 不影响代码含义的变更，如空格、格式化、漏掉分号等
  - refactor: 重构，并未修复缺陷或添加功能
  - perf: 性能(performance)提升
  - test: 补充测试用例
  - chore: 改进构建过程或辅助工具，例如文档生成工具

- 在浏览器上做代理的两种方式：
  - webrequestblocking，修改请求，devtool中见到的是修改后的请求
  - pack代理，通过系统的代理协议，不修改请求，devtool中可见到原请求