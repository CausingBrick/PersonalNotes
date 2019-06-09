#  ueditor1.4.3 去除自动保存提示

```js
1、ueditor.config.js，enableAutoSave的注释去掉并设置成false，saveInterval的注释也去掉设置成0；

2、修改ueditor.all.js，在'contentchange': function () {函数的第一行添加代码：

if (!me.getOpt('enableAutoSave')) {return;}
```



