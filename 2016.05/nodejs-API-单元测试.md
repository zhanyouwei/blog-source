title: "nodejs API 单元测试"
date: 2015-09-06 23:07:15
categories: 前端
tags: node.js
---

### 9.8跟新
> 针对测试用例中用到的restler中间件，在使用过程中发现其对于请求参数中得Array类型会将其序列化为
带有索引标识的多个key-value类型，e.g.
```json
{
  "ary":[111,2222]
}
会被序列化为
{
  "ary[0]":111,
  "ary[1]":2222
}
```
所以建议将`restler`替换为`superagent`

------------------------------------

最近在尝试用node.js做后端服务器，专门用来提供API接口，今天就来分享一下正对node.js提供的restful API进行单元测试的方法。

### 配置测试环境
1. 配置gulpfile，没用过gulp？请移步[gulp官网](http://gulpjs.com/)
2. 安装测试工具mocha `npm install gulp-mocha --save-dev`
3. 编写测试task

  ```js
  gulp.task('test-api', function () {
    return gulp.src('test.js')
      .pipe(mocha())
      .once('error', function () {
        process.exit(1);
      })
      .once('end', function () {
        process.exit();
      });
  });
  ```
4. 在test.js中编写测试用例

  ```js
  var assert = require("assert");
  var rest = require("restler");//用来请求API接口的中间件
  var apiCtrl = require('../controllers/api');//api模块

  var baseUrl = 'http://localhost:9000/api';
  describe('this is description', function () {
    it('this is assert', function (done) {
      rest.get(baseUrl + '/testAPI/1').on('success', function (res) {
        assert(res.result === 1);
        done();
      });
    });
  });

  ```

以上就是搭建一个nodejs单元测试的简单用例。
简单描述一下就是，采用现有的mocha框架进行单元测试，再通过gulp集成测试环境，配置自动化测试用例，从而提高效率。
