# 基于Swagger开发API接口平台实践篇

## API 接口平台前端技术架构

前端为独立的 SPA APP ，使用 Vue 开发，UI 框架使用的是饿了么最近推出的 ElementUI。

构建工具选用的是 Webpack。

对了，ESlint 是基于 Airbnb 的规范，由于太严（变）格（态），导致我一度想放弃...

技术栈总得来说：VUE + ElementUI + Webpack

前端提供一个Web版视图用户定义和查看API文档（此处没图，因为还没做好。。。）

**这里最重要的就是将 Swagger 规范，翻译成可视化的界面。**

## API 接口平台后端技术架构

后端只用来提供 API ，采用的是比较熟悉的 Node.js + Express.js 模式。

数据库使用 Leancloud 提供的云端存储功能 LeanStorage 。（数据库一直是我的弱项，能不用自己弄就不自己弄~~）

后端提供 API 接受前端传入的参数，然后通过 LeanStorage 去 Leancloud 上面进行数据读取操作。

**这里最重要的就是根据前端数据生成JSON文档，供前端下载**

# 是不是太简单了。。。

