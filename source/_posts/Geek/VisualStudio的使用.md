---
title: VisualStudio的使用
tags: VisualStudio
categories: Geek
abbrlink: 7523acd8
date: 2023-08-29 03:57:00
---
<meta name="referrer" content="no-referrer" />

<a name="egV9D"></a>
# 好用的快捷键(有的需要安装番茄助手才能用)
alt+shift+o 全局搜索<br />alt+shift+f 查找引用<br />alt + o 在cpp和头文件之间相互跳转<br />ctrl +a + k + f 全选代码使代码变得整洁
ctrl+shift+d 翻译(需前往扩展下载translate扩展)
"/" 自动判断所选代码是带注释的还是不带注释的,然后为其添加或删除注释
ctrl+b 构建当前项目
ctrl+F5 调试当前项目
ctrl+shift+回车 从当前行切换到下一行(与VSCode的ctrl+回车一样)
ctrl+d 将当前行内容复制到下一行
ctrl+shift+空格  当光标在函数参数里面时,显示函数所需要的参数列表
ctrl+shift+s 保存(当与UE进行实时编程时用得到)
ctrl键加上+键或者-键可以进行前进和后退的操作,方便查看类的定义后返回原来的浏览位置

<a name="RWb6C"></a>
# Visual Assist番茄助手
首先推荐一个符号搜索插件 Visual Assist 也称番茄助手，下载安装方法自行搜索。
<a name="vMyYY"></a>
## 禁用使用中文注释时提示拼写错误的问题
![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1693216885933-989fe0c4-d03c-417e-b4dd-e945a5c17d56.png#averageHue=%23f1edea&clientId=uc9bedbdb-4582-4&from=paste&height=192&id=ufae31f36&originHeight=192&originWidth=728&originalType=binary&ratio=1&rotation=0&showTitle=false&size=13247&status=done&style=none&taskId=u3b89b7f3-2f06-47fb-a329-cfc0db170b6&title=&width=728)

<a name="z2Iwm"></a>
## 好用的使用方法
<a name="o5I7N"></a>
### 快速在cpp中创建头文件中声明的函数定义
在头文件中选择自己声明的函数名称，然后右键后点击Create Implementation即可快速在cpp中生成定义。<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/2623605/1693216147386-36de503f-be6c-427f-b799-9667ddbf1336.png#averageHue=%236f9070&clientId=uc9bedbdb-4582-4&from=paste&height=308&id=u6ebc902a&originHeight=308&originWidth=1156&originalType=binary&ratio=1&rotation=0&showTitle=false&size=46765&status=done&style=none&taskId=u9b52cbd7-5696-4e0a-9d6b-997a5b74c84&title=&width=1156)








