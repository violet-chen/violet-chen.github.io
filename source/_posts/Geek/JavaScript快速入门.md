---
title: JavaScript快速入门
tags: JavaScript
categories: Geek
abbrlink: c8a0ed40
date: 2023-12-10 14:52:00
---
> 教程链接:https://www.bilibili.com/video/BV11B4y1U7aH?p=2&vd_source=b1de3fe38e887eb40fc55a5485724480

# JavaScript的介绍
JavaScript是一种编程语言,JavaScript用于在浏览器中建立交互式网页,移动应用程序,实时网络应用程序,命令行工具,游戏.每个浏览器都有JavaScript引擎.将谷歌的引擎取出嵌入到cpp程序当中,这个cpp程序叫做Node.有了Node后可以在浏览器中运行JavaScript代码,把JavaScript代码发送给Node执行.所以JavaScript可以为网络和移动设备构建后端.JavaScript的运行环境叫Node.
# 第一次使用JavaScript测试
按F12进入控制台
![Alt text](image.png)
输入console.log("Hello World")进行日志打印
输入alert("Hello World")可以在页面中弹窗输出Hello World
# 搭建开发环境
使用vscode
1. 安装第三方库需要使用nodejs,如果没有nodejs就去官网下载:https://nodejs.org/en
2. 创建一个文件夹,里面先放一个index.html文件
3. 在index.html文件中输入!加上tab键即可生成html通用模板
4. 下载live server插件,live server是一个非常轻量级的web服务器,可以使用它为web应用程序提供服务, 下载好以后在html文件上面右键,点击Open with live server即可在浏览器中预览html
# 第一个JavaScript脚本
以下代码只需要关注body和/body中间的内容,其他的内容都是模板生成的.h1和/h1里的内容是浏览器的内容.script和/script中的内容是JavaScript脚本的内容,作用是输出HelloWorld日志,可以在浏览器网页中使用F12进入控制台中查看到.
![Alt text](image-1.png)
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>Hello World</h1>
    <script>
        // 打印Hello World日志
        console.log('Hello World');
    </script>
</body>
</html>
```
# 将JavaScript脚本放到单独的js文件中
刚才创建了index.html文件,然后将js代码写到了script字符段里面.还有另一种方法,那就是写到js文件中,然后在html文件中将js文件弄进来.
使用方法:
1.再创建一个index.js文件,文件名可以随意
2.将js代码放到index.js文件中
3.然后可以把
```html
<script>
    // 原html文件内容:
    console.log('Hello World');
</script>
```
修改为
```html
<script src="index.js"></script>
```
# JavaScript的语法
```js
// 定义一个字符串变量my_name1,并打印
let my_name1 = 'chen';
console.log(my_name);

// 定义一个字符串常量my_name2
const my_name2 = 'chen';

// 检测变量的类型
typeof my_name2;

// 创建一个对象,并修改其内容
let person = {
    name: 'chen',
    age: 22,
};
// 修改对象内容方法一:
person.name = 'ruichen';
// 修改对象内容方法二:
person['name'] = 'ruichen';
// 修改对象内容方法三:
my_name = 'name';
person[my_name] = 'ruichen';
// 输出对象的内容
console.log(person.name);

// 创建一个数组,数组也是一个对象
let selectedColors = ['red','blue'];
selectedColors[2] = 1;
console.log(selectedColors);

// 定义函数
function greet(name){
    console.log('Hello ' + name);
}
greet('ruichen');

// 定义有返回值的函数
function square(number){
    return number * nember;
}
console.log(square(2));
```


