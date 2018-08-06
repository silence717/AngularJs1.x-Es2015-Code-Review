# AngularJs1.x + es2015 Code Review CheckList（初稿）

## 通用规则

### 命名
##### 变量和函数 使用 Camel 命名法 
```js
// 变量
var orderQuery = {};
// 函数
function stringFormat(source) {
    // do something
}
```
##### 常量使用全部大写字母，单词间使用下划线分隔命名方式
```js
const RED_BLACK_TYPE = {
	RED: 'red',
	CUSTOMER: 'customer',
	MOBILE: 'mobile',
	EMAIL: 'email',
	BLACK: 'customer',
	WHITE: 'white'
};
```
##### 函数名使用动宾短语
```js
function getData() {
    
}
```
##### getXXX函数一般都有返回值
```js
function getUrl() {
    return 'http://www.baidu.com'
}
```
##### 给变量赋值使用setXXX
```js
function setGateway(item) {
    this.selectGateway = item;
}
```
##### `boolean`类型的变量使用`is`或者`has`开头
```js
let isLoading = false;
let hasError = true;
```


### 注释

##### 文件：只有在入口文件有需要
```js
/*
 * @Author: fang.yang          // 无用
 * @Date: 2018-07-11 17:28:07  // 无用
 * @desc [红、黑名单公共服务]  // 有效，说明整个块是做什么用的
 * @interface [api doc链接]    // 如果是`loader.js`文件的话，便于查找对应api定义
 */
```

##### 函数：简单的就直接写函数描述。负责的包含参数说明，标明返回值。
```js
/**
 * 负责函数
 *
 * @param {string} p1 参数1的说明
 * @param {string} p2 参数2的说明，比较长
 *     那就换行了.
 * @param {number=} p3 参数3的说明（可选）
 * @return {Object} 返回值描述
*/
function foo(p1, p2, p3) {
    var p3 = p3 || 10;
    return {
        p1: p1,
        p2: p2,
        p3: p3
    };
}

// 设置黑名单
setBlackListClick() {
    // some code
}
```

##### 变量：独占一行    

bad
```js
const selectGatewayId = ''; // 选择的通道ID
```
good  
```js
// 选择的通道ID
const selectGatewayId = ''; 
```
### 其他
1. 使用editorconfig来覆盖本地的编辑器设置
2. 函数应该只做一件事情
3. 函数的调用方与被调用方靠近
4. 注释掉的代码直接删除，时间久了会忘记而不敢删除
5. 所有的代码 eslint 都通过
6. 对于其他开发者是否易于理解
7. 不能直接使用全局变量

## AngularJs 1.5.8  

1. DOM操作只出现在`directives`。Angular是通过指令声明添加在元素上。directive提供通过 compiler 和 link 访问元素。

2. 不能出现以`$`开头的命名。`$`前缀是AngularJS内部的保留。`$scope``$watch`等。
3. 自定义的依赖在内置依赖后面注入。
```js
function($rootScope, $timeout, MyDependency)
```
4. 使用`ng-src`代替`src`，使用`ng-href`代替`href`，`ng-style`代替`style`。
5. 使用`ng-cloak`或者`ng-bind`来绑定，避免直接使用`{{}}`造成页面抖动。
6. 使用`EventBus`通信机制，减少对框架和组件的依赖。
7. 使用 `{{ ::expression }}`在初始化之后，不会再改变。在表达式计算成一个非null的值之后，AngularJs会停止watch表达式。

8. `$watch`的表达式越简单越好。
9. `$watchCollection`避免深度监听。
10. 使用`ng-class`编写样式，css module的方式来编写。
11. 及时移除不需要的`$watch`。
```js
var unwatch = $scope.$watch("someKey", function(newValue, oldValue){
  //do sth...
  if(someCondition){
    //当不需要的时候,及时移除watch
    unwatch();
  }
});
```

## `ccms-nodes`项目节点目录组织

```js
coupon // 某个单独节点
    index.js           // 入口文件
    body.url.html      // 模板文件
    footer.url.html    // 弹框底部模板，尽可能使用公共的，特殊的就自己编写
    index.scss         // css
    loader.js          // api交互
    Controller.js      // 主业务逻辑
    mock.js            // 模拟数据管理
    其他               // 使用到的各种服务
```

## 参考规范

[Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript/blob/master/README.md)  
[clean code javascript](https://github.com/ryanmcdermott/clean-code-javascript)  
[AngularJs-Es2015编码风格指南](https://github.com/toddmotto/angularjs-styleguide/blob/master/i18n/zh-cn.md)  
[Google's JavaScript Style Gude](https://google.github.io/styleguide/javascriptguide.xml)

[AngularJS性能优化心得](https://github.com/atian25/blog/issues/5)


