title: Backbone源码分析之Model
date: 2015-10-27 23:17:17
categories: 源码分析
tags: Backbone
---

Model（称之为模型），通常是一个应用的核心组成部分，前端的MVC设计模式源自于后端传统的MVC架构，  

引用一段 Backbone 官方对于模型的说明
>Models are the heart of any JavaScript application, containing the interactive data as well as a large part of the logic surrounding it: conversions, validations, computed properties, and access control. You extend Backbone.Model with your domain-specific methods, and Model provides a basic set of functionality for managing changes.

用大白话来解释就是说：“模型是所有Javascript应用的核心组成部分，它包括数据交互和与之相关的转换，
验证，属性操作，访问控制等逻辑处理部分。你可以使用自定义的方法扩展模型，并且模型提供了一套基础的
监听模型变化的方法”

下面我们就来看看Backbone源码中的模型相关的代码：

```js
var Model = Backbone.Model = function(attributes, options) {
  var attrs = attributes || {};
  options || (options = {});
  this.cid = _.uniqueId(this.cidPrefix);
  this.attributes = {};
  if (options.collection) this.collection = options.collection;
  if (options.parse) attrs = this.parse(attrs, options) || {};
  attrs = _.defaults({}, attrs, _.result(this, 'defaults'));
  this.set(attrs, options);
  this.changed = {};
  this.initialize.apply(this, arguments);
};
```

这是声明模型的代码，主要是

```js
_.extend(Model.prototype, Events, { ... });
```
这里使用Underscore.js中的extend方法为模型添加了Events事件和一些属性，Events我们会
单独拿出来分析，下面我们来看看为模型扩展了属性。
```js
//用来标识当前哪些属性被改变了，可以通过它找到那些在操作中被改变的属性
changed: null
```

```js
//模型验证失败后的返回信息
validationError: null,
// 判断模型是否验证通过
isValid: function(options) {
  return this._validate({}, _.defaults({validate: true}, options));
},

// 验证模型属性,通过则返回 `true` 否则触发 `invalid` 事件，返回错误信息
_validate: function(attrs, options) {
  if (!options.validate || !this.validate) return true;
  attrs = _.extend({}, this.attributes, attrs);
  var error = this.validationError = this.validate(attrs, options) || null;
  if (!error) return true;
  this.trigger('invalid', this, error, _.extend(options, {validationError: error}));
  return false;
}
```

```js
// 模型默认的id属性的字段名，可以根据需要自定义key值 e.g. _id
idAttribute: 'id'
```

```js
// cid为模型创建的时候赋予的id，改属性定义了id前缀
cidPrefix: 'c'
```

```js
// 模型初始化函数，可根据需要自己实现初始化逻辑
initialize: function(){}
```

```js
// 将模型转为JSON对象的方法，返回一个包含模型attributes的JSON对象
toJSON: function(options) {
  return _.clone(this.attributes);
}
```
