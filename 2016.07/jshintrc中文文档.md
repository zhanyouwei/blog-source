# jshintrc 中文说明



`comelcase` 是否要求变量都使用驼峰命名

`curly` 是否要求 for/while/if 带花括号 

`eqeqeq` 是否强制使用严格等号

`strict` 是要求否以 strict 模式检查

`freeze` 是否阻止修改或拓展基本对象（Array、Date 等）的原型链, 原型链污染比较危险，默认打开

`immed` 是否要求自执行的方法使用括号括起

`indent` 指定缩进大小为 几 个空格

`latedef` 要求变量在使用前声明

`newcap` 要求构造函数大写

`noarg` 不允许使用 arguments.callee 和 arguments.caller，未来会被弃用

`noempty` 不允许空的代码快，默认关闭

`nonbsp` 不允许使用 "non-breaking whitespace"，这些字符在非 UTF8 页面会导致代码失效

`nonew` 阻止直接使用 new 调用构造函数的语句（不赋值对象）e.g.

```javascript
//ok
var a = new Animal();
//warn
new Animal();
```

`plusplus` 不允许使用 ++ 和 -- 运算符, 默认关闭

`quotmark` 字符串引号, 默认要求使用单引号

`undef` 提示未定义的变量, 未定义的变量会容易造成全局变量，建议开启

`trailing` 字符串不允许以空格加斜杠的形式来换行

```javascript
// OK
var str = 'Hello ' +
   'world';
// warn
var str = 'Hello \
    world';
```

`debug` 对代码中使用的 debugger 语句默认给出警告

`laxcomma` 写字面量时，逗号放前面给出警告

`unused` 提示未使用的变量，默认开启