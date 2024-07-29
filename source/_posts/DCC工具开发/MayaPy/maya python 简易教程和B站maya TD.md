---
title: maya python 简易教程和B站maya TD
tags: MayaPy
categories: DCC工具开发
abbrlink: 6161e39f
date: 2023-08-29 03:57:00
---
<meta name="referrer" content="no-referrer" />

<a name="Cn3Wb"></a>
# 开篇介绍
真正复杂的东西“东西”很少，但是复杂的“组合”却是很多。复杂的“组合”往往需要自己创造，发挥自己的想象力吧。
<a name="V9keO"></a>
# Unicode 字符串
在Python2中，普通字符串是以8位ASCII码进行存储的，而Unicode字符串则存储为16位unicode字符串，这样能够表示更多的字符集。使用的语法是在字符串前面加上前缀 **u**。<br />在Python3中，所有的字符串都是Unicode字符串。
<a name="fPmBt"></a>
# 第一个简单代码
```python
import maya.cmds as mc
def height(h):
    sel=mc.ls(sl=1)
    for i in range(0,len(sel)):
        mc.setAttr(sel[i]+'.ty',i*h)
height(0.5)
```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648435412615-7d9cfcf0-5bc5-45a1-8bc0-aab7de506efc.png#averageHue=%235e5e5e&clientId=u5321e486-8528-4&errorMessage=unknown%20error&from=paste&height=313&id=ucd073b72&originHeight=313&originWidth=661&originalType=binary&ratio=1&rotation=0&showTitle=false&size=5658&status=error&style=none&taskId=ucbd93dd6-cb00-4aa0-ac53-1a7a0bbd4d9&title=&width=661)
<a name="tmEhp"></a>
# 吸附工具
```python
import maya.cmds as mc
def snap():
    sel=mc.ls(sl=1)
    pos=mc.xform(sel[1],t=1,ws=1,q=1)
    mc.xform(sel[0],t=pos)
snap()
```
<a name="UrJcC"></a>
# 批量添加前缀后缀工具
```python
import maya.cmds as mc
def addpre(pre):
    for name in  mc.ls(sl=1) :
        mc.rename(name,pre+name)
addpre('mesh_')        
def adddis(dis):
    for name in  mc.ls(sl=1) :
        mc.rename(name,name+dis)
adddis('_low')
```
看了另一个教程的修改版本：<br />介绍一下：这个工具修改了之前添加前缀名工具的一个bug，就是当出现![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648708809664-a9489ba4-68c1-4885-96f7-15ab4db4986f.png#averageHue=%233b3a39&clientId=u4f45dca2-649f-4&errorMessage=unknown%20error&from=paste&height=114&id=uk7V9&originHeight=114&originWidth=134&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2692&status=error&style=none&taskId=ub4fb5101-f214-4f2d-ae15-896b0ec5306&title=&width=134)这种不同级别物体名字相同时依然可以正确的通过工具添加后缀。<br />思路就是通过长名判断oldName，然后通过shortname=name.split("|")[-1]命令得到短名，配合前后缀得到newName，**这样就不会出现一个名称有多个匹配对象的bug了**
```python
import maya.cmds as mc
def addpre(pre):
    for name in  mc.ls(sl=1,l=1) :
        shortname=name.split("|")[-1]
        mc.rename(name,pre+shortname)
addpre('mesh_')        
def adddis(dis):
    for name in  mc.ls(sl=1,l=1) :
        shortname=name.split("|")[-1]
        mc.rename(name,shortname+dis)
adddis('_low')
```
<a name="dJIOd"></a>
# 对文本进行操作
将当前所选择的物体的位置坐标导出成文本文件。
```python
import maya.cmds as mc

sel = mc.ls(sl=1)
info = []
info_str = ''
for i in sel:
    posx = mc.getAttr(i + '.tx')
    posy = mc.getAttr(i + '.ty')
    posz = mc.getAttr(i + '.tz')
    info.append([i, posx, posy, posz]) # 测试里面用元组也能正常使用，但教程是列表
for i in info:
    info_str = info_str + i[0] + '\r\nposx:' + str(i[1]) + '\r\nposy:' + str(i[2]) + '\r\nposz:' + str(
        i[3]) + '\r\n\r\n'
    f = open('D:\\posInfo.txt', 'w')  # w代表写入
    f.write(info_str)
    f.close()
```
最终结果是在d盘根目录生成一个posInfo文本文件，里面数值为选择的物体的参数属性![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648469718676-a9c60fd2-4a20-4db2-b33e-362b6e11a4b2.png#averageHue=%23fbfafa&clientId=u45bfbeec-9c64-4&errorMessage=unknown%20error&from=paste&height=756&id=u7577597b&originHeight=756&originWidth=718&originalType=binary&ratio=1&rotation=0&showTitle=false&size=21996&status=error&style=none&taskId=ua3ee56ad-8e15-4229-88c5-67a8b6e1e89&title=&width=718)
<a name="le37I"></a>
# 带窗口带输入框的加前缀名工具
```python
import maya.cmds as mc
def addpre(pre):
    for i in mc.ls(sl=1):
        mc.rename(i,pre+i)
mc.window()
mc.columnLayout()
a=mc.textField(tx='defalt')
mc.button(l='Press   Me',w=100,h=100,c="b=mc.textField(a,q=1,tx=1);addpre(b)") # c为command的缩写
mc.showWindow()
```
<a name="jCrpN"></a>
# 自动根据物体类型添加后缀名
思路是通过cmds.listRelatives(obj,children=1,fullPath=1) or []命令得到物体的子物体的名字（pCube1的子物体的名字为![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648712895301-90044fca-7014-49dc-b5db-aaae5963f07f.png#averageHue=%234b6a81&clientId=u4f45dca2-649f-4&errorMessage=unknown%20error&from=paste&height=46&id=ua86708c6&originHeight=46&originWidth=188&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2426&status=error&style=none&taskId=u509e639b-39d0-4dad-a71a-e763c398f53&title=&width=188)，joint没有子物体返回空列表）。![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648713269802-8c2bcf97-d9d4-4f8c-90ed-d4dc75bcd239.png#averageHue=%23ffffff&clientId=u4f45dca2-649f-4&errorMessage=unknown%20error&from=paste&height=101&id=uc8683ecb&originHeight=101&originWidth=296&originalType=binary&ratio=1&rotation=0&showTitle=false&size=8181&status=error&style=none&taskId=ua0afd779-e652-4f27-8718-b2f2abb607f&title=&width=296)有子物体的就判断子物体的类型，没有子物体的就判断物体本身的类型。之所以这样得到不同物体的类型是因为例如pCube通过objectType得到的类型为transform，而通过得到它的子物体（pCubeShape）得到的类型为mesh，能更好的区分。<br />如果想再细分物体类型（曲线，灯光等）就在下面加判断语句。
```python
# -*- coding:UTF-8 -*-

import maya.cmds as mc

SUFFIXES = {
    "mesh": "geo",
    "joint": "jnt",
    "camera": None
}
DEFAULT_SUFFIX = "grp"


def addSuffix(selection=False):
    sel = mc.ls(sl=selection, dag=1, l=1)
    if selection and not sel:  # 如果指定selection为True但是却没有选择物体时抛出异常。
        raise RuntimeError("You don't have anything selected! How dare you?!")

    sel.sort(key=len, reverse=1)  # 将列表按照元素个数由高到底排序
    for obj in sel:
        shortName = obj.split('|')[-1]  # 因为是长名的列表，这里取长名中的短名
        children = mc.listRelatives(obj, children=1,
                                    fullPath=1) or []  # 如果物体没有子物体不会返回空列表而是返回None，因此加个or[]实现如果是None就返回空列表的功能
        if len(children) == 1:
            child = children[0]  # 将列表变成字符串
            objType = mc.objectType(child)
        else:
            objType = mc.objectType(obj)
        suffix = SUFFIXES.get(objType, DEFAULT_SUFFIX)  # 根据objType获取对应添加的后缀名，如果没有找到对应的key那么就使用DEFAULT_SUFFIX

        if not suffix:  # 如果后缀名为None（类型为摄像机时）不添加后缀
            continue

        if obj.endswitch('_'+suffix):
            continue  # 如果已经添加了后缀，那么就不再进行添加后缀
        newName = "%s_%s" % (shortName, suffix)
        mc.rename(obj, newName)

```
改进版介绍： 将类型以及对应的后缀名通过字典存取，（通过字典存取的好处是，如果想要增加其他类型的后缀名可以直接针对字典进行操作而不需要再使用if语句判断了。）通过SUFFIXES.get(objType, DEFAULT_SUFFIX)获取对应的value，通过更改为函数形式，可以通过导入的方式，直接调用函数，并可以指定是否使用选择模式。
```python
import maya.cmds as mc

SUFFIXES = {
    "mesh": "geo",
    "joint": "jnt",
    "camera": None
}
DEFAULT_SUFFIX = "grp"


def addSuffix(selection=False):
    sel = mc.ls(sl=selection, dag=1, l=1)
    if selection and not sel:  # 如果指定selection为True但是却没有选择物体时抛出异常。
        raise RuntimeError("You don't have anything selected! How dare you?!")

    sel.sort(key=len, reverse=1)  # 将列表按照元素个数由高到底排序
    for obj in sel:
        shortName = obj.split('|')[-1]  # 因为是长名的列表，这里取长名中的短名
        children = mc.listRelatives(obj, children=1,
                                    fullPath=1) or []  # 如果物体没有子物体不会返回空列表而是返回None，因此加个or[]实现如果是None就返回空列表的功能
        if len(children) == 1:
            child = children[0] # 将列表变成字符串
            objType = mc.objectType(child)
        else:
            objType = mc.objectType(obj)
        suffix = SUFFIXES.get(objType, DEFAULT_SUFFIX)  # 根据objType获取对应添加的后缀名，如果没有找到对应的key那么就使用DEFAULT_SUFFIX

        if not suffix:  # 如果后缀名为None（类型为摄像机时）不添加后缀
            continue

        if obj.endswitch('_'+suffix):
            continue  # 如果已经添加了后缀，那么就不再进行添加后缀
        newName = "%s_%s" % (shortName, suffix)
        mc.rename(obj, newName)

```
<a name="kzeDE"></a>
# 齿轮工具
<a name="r1QzH"></a>
## 创建齿轮工具gearCreator
```python
import maya.cmds as mc


def createGear(teeth=10, length=0.3):
    spans = teeth * 2  # 面的数量是齿轮数量的2倍
    transform, constructor = mc.polyPipe(subdivisionsAxis=spans) 
    # mc.polyPipe 返回的是一个列表
    # transform是多边形的名字，constructor是构造器（调节多边形的属性）的名称
    sideFaces = range(spans * 2, spans * 3, 2) # 面的数字ID是spans*2和spans*3。
    mc.select(clear=True)
    for face in sideFaces:
        mc.select('%s.f[%s]' % (transform, face),add=True) # add=True的意思是加选
    extrude = mc.polyExtrudeFacet(localTranslateZ=length)[0] # 加一个[0]的作用就是将列表变成值
    return transform, constructor, extrude


createGear(teeth=20,length=1)

```
返回值：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648895714457-9f408014-8096-4e6d-8152-4fe3e9381160.png#averageHue=%232f302d&clientId=ude30dde1-d57a-4&errorMessage=unknown%20error&from=paste&height=52&id=u6b5b0f75&originHeight=52&originWidth=481&originalType=binary&ratio=1&rotation=0&showTitle=false&size=24509&status=error&style=none&taskId=u60495b84-a4bf-42ff-8e9f-a91d073d998&title=&width=481)

<a name="PRZTC"></a>
## 创建齿轮并可以修改齿轮
前言：<br />创建好的齿轮如果只是单纯的更改它的细分会造成：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648904364686-2f1bd957-e6d3-484a-82ea-bd23ff46fc11.png#averageHue=%23444241&clientId=ude30dde1-d57a-4&errorMessage=unknown%20error&from=paste&height=176&id=ue74d5d1b&originHeight=176&originWidth=253&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7643&status=error&style=none&taskId=ub72f5b86-ce02-43de-ae4f-66c59c44c18&title=&width=253)这种奇怪的效果<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648904385463-47ee46d2-239a-41a7-bea1-527fb335c0a1.png#averageHue=%23696969&clientId=ude30dde1-d57a-4&errorMessage=unknown%20error&from=paste&height=349&id=u229dd4ac&originHeight=349&originWidth=430&originalType=binary&ratio=1&rotation=0&showTitle=false&size=13416&status=error&style=none&taskId=u3a174a2a-9ff8-41e4-b528-699823a3d41&title=&width=430)，原因是因为上面的polyExtrudeFace1，因为polyExtrudeFace1挤出命令是根据获得齿轮中的面id（inputComponents）来执行挤出操作的，但是如果更改了细分数挤出命令节点就不知道要编辑哪个面了。<br />因此修改齿轮的思路就是：<br />首先将![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648904915251-25bcbf20-cc97-41f5-a236-911368dbf4aa.png#averageHue=%234b4645&clientId=ude30dde1-d57a-4&errorMessage=unknown%20error&from=paste&height=88&id=u6f8a71ac&originHeight=88&originWidth=189&originalType=binary&ratio=1&rotation=0&showTitle=false&size=3611&status=error&style=none&taskId=u59e7231b-7005-49e2-9502-ae0251e144c&title=&width=189)polyPipe1的细分以及长度根据数值更改<br />然后将polyExtrudeFace1的inputComponents属性进行更改使挤出命令节点能够正确识别细分后的面。<br />mc.setAttr('%s.inputComponents' % extrude, len(faceNames), *faceNames, typ="componentList")这个命令是重新设置inputComponents属性，len（faceNames）代表要进行操作的面的数量，*faceNames意思是将存取面ID的列表解开，最后指定类型为组件列表。
```python
import maya.cmds as mc


def createGear(teeth=10, length=0.3):
    spans = teeth * 2
    transform, constructor = mc.polyPipe(subdivisionsAxis=spans)
    sideFaces = range(spans * 2, spans * 3, 2)
    mc.select(clear=True)
    for face in sideFaces:
        mc.select('%s.f[%s]' % (transform, face), add=True)
    extrude = mc.polyExtrudeFacet(localTranslateZ=length)[0]
    mc.select(self.transform)
    return transform, constructor, extrude


def changeTeeth(constructor, extrude, teeth=10, length=0.3):
    spans = teeth * 2
    mc.polyPipe(constructor, edit=True, subdivisionsAxis=spans)
    sideFaces = range(spans * 2, spans * 3, 2)
    faceNames = []
    for face in sideFaces:
        faceName = 'f[%s]' % face
        faceNames.append(faceName)

    mc.setAttr('%s.inputComponents' % extrude, len(faceNames), *faceNames, typ="componentList")
    mc.polyExtrudeFacet(extrude, edit=True, localTranslateZ=length)


changeTeeth('polyPipe1', 'polyExtrudeFace1', teeth=20, length=0.1)

```
<a name="Bx7wC"></a>
## 使用类来实现齿轮工具
通过类实现就可以通过实例变量将创建齿轮函数与改变齿轮数量函数之间创建联系。
```python
import maya.cmds as mc


class Gear(object):
    def __init__(self):
        self.constructor = None
        self.transform = None
        self.extrude = None

    def createGear(self, teeth=10, length=0.3):
        spans = teeth * 2
        self.transform, self.constructor = mc.polyPipe(subdivisionsAxis=spans)
        sideFaces = range(spans * 2, spans * 3, 2)
        mc.select(clear=True)
        for face in sideFaces:
            mc.select('%s.f[%s]' % (self.transform, face), add=True)
        self.extrude = mc.polyExtrudeFacet(localTranslateZ=length)[0]
        mc.select(self.transform)

    def changeTeeth(self, teeth=10, length=0.3):
        spans = teeth * 2
        mc.polyPipe(self.constructor, edit=True, subdivisionsAxis=spans)
        sideFaces = range(spans * 2, spans * 3, 2)
        faceNames = []
        for face in sideFaces:
            faceName = 'f[%s]' % face
            faceNames.append(faceName)

        mc.setAttr('%s.inputComponents' % self.extrude, len(faceNames), *faceNames, typ="componentList")
        mc.polyExtrudeFacet(self.extrude, edit=True, localTranslateZ=length)


gear = Gear()
gear.createGear()
gear.changeTeeth(teeth=20, length=0.1)

```
<a name="dDbGA"></a>
## 带UI的创建齿轮工具
```python
import maya.cmds as mc


class Gear(object):
    def __init__(self):
        self.constructor = None
        self.transform = None
        self.extrude = None

    def createGear(self, teeth=10, length=0.3):
        spans = teeth * 2
        self.transform, self.constructor = mc.polyPipe(subdivisionsAxis=spans)
        sideFaces = range(spans * 2, spans * 3, 2)
        mc.select(clear=True)
        for face in sideFaces:
            mc.select('%s.f[%s]' % (self.transform, face), add=True)
        self.extrude = mc.polyExtrudeFacet(localTranslateZ=length)[0]

    def changeTeeth(self, teeth=10, length=0.3):
        spans = teeth * 2
        mc.polyPipe(self.constructor, edit=True, subdivisionsAxis=spans)
        sideFaces = range(spans * 2, spans * 3, 2)
        faceNames = []
        for face in sideFaces:
            faceName = 'f[%s]' % face
            faceNames.append(faceName)

        mc.setAttr('%s.inputComponents' % self.extrude, len(faceNames), *faceNames, typ="componentList")
        mc.polyExtrudeFacet(self.extrude, edit=True, localTranslateZ=length)


class GearWindow(object):
    windowName = "GearWindow"

    def __init__(self):
        self.gear = None

    def show(self):
        if mc.window(self.windowName, q=True, exists=True):
            mc.deleteUI(self.windowName)
        mc.window(self.windowName)

        self.buildUI()

        mc.showWindow()

    def buildUI(self):
        column = mc.columnLayout()
        mc.text(label="Use the slider to modify the gear")
        row = mc.rowLayout(numberOfColumns=4)
        self.label = mc.text(label="10")
        self.slider = mc.intSlider(min=5, max=30, value=10, step=1, dragCommand=self.modifyGear)  # 创建滑动条，拖动滑动条时调用函数
        mc.button(label="Make Gear", command=self.makeGear)
        mc.button(label="Reset", command=self.reset)  # 命令中调用函数不加括号是因为如果加了括号就直接使用函数了，而不是与按钮绑定。
        mc.setParent(column)
        mc.button(label="Close", command=self.close)

    def makeGear(self, *args):
        teeth = mc.intSlider(self.slider, q=True, value=True)
        self.gear = Gear()
        self.gear.createGear(teeth=teeth)

    def modifyGear(self, teeth):
        if self.gear:
            self.gear.changeTeeth(teeth=teeth)
        mc.text(self.label, edit=True, label=teeth)

    def reset(self, *args):
        # 使用*args是因为command调用此函数的同时会传入参数，因此使用*args来接收，但没必要使用
        self.gear = None
        mc.intSlider(self.slider, edit=True, value=10)
        mc.text(self.label, edit=True, label="10")

    def close(self, *args):
        mc.deleteUI(self.windowName)


GearWindow().show()

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1649151264550-f79c09d4-09aa-4082-ad30-3cf17a9c7cd5.png#averageHue=%236f6e6e&clientId=u9a09714e-8c52-4&errorMessage=unknown%20error&from=paste&height=129&id=u44751cef&originHeight=129&originWidth=272&originalType=binary&ratio=1&rotation=0&showTitle=false&size=6329&status=error&style=none&taskId=u94880517-8ed9-466e-9377-e569c31ad67&title=&width=272)<br />可以通过滑动条更改齿轮的齿的数量。

<a name="R0IJo"></a>
# 中间帧工具
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1649070276826-af0007fa-352f-495e-b50b-4a3030e9b159.png#averageHue=%23484746&clientId=uf3de0013-f84f-4&errorMessage=unknown%20error&from=paste&height=162&id=uf28e284b&originHeight=162&originWidth=431&originalType=binary&ratio=1&rotation=0&showTitle=false&size=37943&status=error&style=none&taskId=uee3130e3-f363-4829-af76-33a71ebf452&title=&width=431)<br />介绍一下这个工具，这个工具会读取当前时间轴左右两边的关键帧，利用滑块控件设置最左边的数值为当前时间轴的左边的帧的大小，最右边的数值为当前时间轴的右边的帧的大小。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1649070824178-d7f97c71-8d4e-4d80-a2dc-6a5c369c01a9.png#averageHue=%232c2c2b&clientId=uf3de0013-f84f-4&errorMessage=unknown%20error&from=paste&height=853&id=u32afe44d&originHeight=853&originWidth=1157&originalType=binary&ratio=1&rotation=0&showTitle=false&size=201961&status=error&style=none&taskId=ub6fd2b3f-16ae-4679-8ec2-f36c53eba6f&title=&width=1157)
<a name="lXIQT"></a>
## 无UI版
```python
import maya.cmds as mc


def tween(percentage, obj=None, attr=None, selection=True):
    if not obj and not selection:
        raise ValueError("No object given to tween")
    if not obj:
        obj = mc.ls(sl=True)[0]
    if not attr:
        # attrs为选择的物体的所有可以k帧的属性。
        attrs = mc.listAttr(obj, k=True)
    currentTime = mc.currentTime(q=True)
    for attr in attrs:
        attrFull = '%s.%s' % (obj, attr)  # 构建所有可以k帧的属性的长名
        keyframes = mc.keyframe(attrFull, q=True)  # 获得物体已经k帧的属性的帧数，没有k帧的属性为None
        if not keyframes:
            continue  # 对于没有k帧的属性跳过操作

        previousKeyframes = []  # 存取当前帧前的所有已经k帧的帧数列表
        for frame in keyframes:
            if frame < currentTime:
                previousKeyframes.append(frame)
        laterKeyframes = [frame for frame in keyframes if frame > currentTime]  # 通过列表生成式操作得到当前帧后的所有已经k帧的帧数列表

        if not previousKeyframes and not laterKeyframes:
            continue  # 如果当前帧的前面或者后面没帧的话不执行后面的操作

        if previousKeyframes:  # 得到离当前帧最近的左边帧数
            previousFrame = max(previousKeyframes)
        else:
            previousFrame = None

        nextFrame = min(laterKeyframes) if laterKeyframes else None  # 得到离当前帧最近的右边帧数

        previousValue = mc.getAttr(attrFull, time=previousFrame)  # 通过三目运算符得到离当前帧最近的左边帧数对应的值
        nextValue = mc.getAttr(attrFull, time=nextFrame)  # 得到离当前帧最近的右边帧数对应的值

        # 根据百分比设置当前帧的大小
        difference = nextValue - previousValue
        weightedDifference = (difference * percentage) / 100
        currentValue = previousValue + weightedDifference
        # 设置当前帧的数值
        mc.setKeyframe(attrFull, time=currentTime, value=currentValue)

```
调用时只需要使用tween(100) 其中100代表的是百分比。
<a name="z0lJ9"></a>
## 添加UI
```python
class TweenWindow(object):
    windowName = "TweenerWindow"

    def show(self):
        if mc.window(self.windowName, q=True, exists=True):
            mc.deleteUI(self.windowName)
        mc.window(self.windowName)

        self.buildUI()

        mc.showWindow()

    def buildUI(self):
        column = mc.columnLayout()
        mc.text(label="Use this slider to set the tween amount")
        row = mc.rowLayout(numberOfColumns=2)
        self.slider = mc.floatSlider(min=0, max=100, value=50, step=1, changeCommand=tween)  # 创建滑动条
        mc.button(label="Reset", command=self.reset)  # 命令中调用函数不加括号是因为如果加了括号就直接使用函数了，而不是与按钮绑定。
        mc.setParent(column)
        mc.button(label="Close", command=self.close)

    def reset(self,*args):
        # 使用*args是因为command调用此函数的同时会传入参数，因此使用*args来接收，但没必要使用
        mc.floatSlider(self.slider, edit=True, value=50)

    def close(self,*args):
        mc.deleteUI(self.windowName)
```
<a name="Ks6OD"></a>
## 组合并使用
```python
import maya.cmds as mc


def tween(percentage, obj=None, attr=None, selection=True):
    if not obj and not selection:
        raise ValueError("No object given to tween")
    if not obj:
        obj = mc.ls(sl=True)[0]
    if not attr:
        # attrs为选择的物体的所有可以k帧的属性。
        attrs = mc.listAttr(obj, k=True)
    currentTime = mc.currentTime(q=True)
    for attr in attrs:
        attrFull = '%s.%s' % (obj, attr)  # 构建所有可以k帧的属性的长名
        keyframes = mc.keyframe(attrFull, q=True)  # 获得物体已经k帧的属性的帧数，没有k帧的属性为None
        if not keyframes:
            continue  # 对于没有k帧的属性跳过操作

        previousKeyframes = []  # 存取当前帧前的所有已经k帧的帧数列表
        for frame in keyframes:
            if frame < currentTime:
                previousKeyframes.append(frame)
        laterKeyframes = [frame for frame in keyframes if frame > currentTime]  # 通过列表生成式操作得到当前帧后的所有已经k帧的帧数列表

        if not previousKeyframes and not laterKeyframes:
            continue  # 如果当前帧的前面或者后面没帧的话不执行后面的操作

        if previousKeyframes:  # 得到离当前帧最近的左边帧数
            previousFrame = max(previousKeyframes)
        else:
            previousFrame = None

        nextFrame = min(laterKeyframes) if laterKeyframes else None  # 通过三目运算符得到离当前帧最近的右边帧数

        previousValue = mc.getAttr(attrFull, time=previousFrame)  # 得到离当前帧最近的左边帧数对应的值
        nextValue = mc.getAttr(attrFull, time=nextFrame)  # 得到离当前帧最近的右边帧数对应的值

        # 根据百分比设置当前帧的大小
        difference = nextValue - previousValue
        weightedDifference = (difference * percentage) / 100
        currentValue = previousValue + weightedDifference
        # 设置当前帧的数值
        mc.setKeyframe(attrFull, time=currentTime, value=currentValue)


class TweenWindow(object):
    windowName = "TweenerWindow"

    def show(self):
        if mc.window(self.windowName, q=True, exists=True):
            mc.deleteUI(self.windowName)
        mc.window(self.windowName)

        self.buildUI()

        mc.showWindow()

    def buildUI(self):
        column = mc.columnLayout()
        mc.text(label="Use this slider to set the tween amount")
        row = mc.rowLayout(numberOfColumns=2)
        self.slider = mc.floatSlider(min=0, max=100, value=50, step=1, changeCommand=tween)  # 创建滑动条
        mc.button(label="Reset", command=self.reset)  # 命令中调用函数不加括号是因为如果加了括号就直接使用函数了，而不是与按钮绑定。
        mc.setParent(column)
        mc.button(label="Close", command=self.close)

    def reset(self, *args):
        # 使用*args是因为command调用此函数的同时会传入参数，因此使用*args来接收，但没必要使用
        mc.floatSlider(self.slider, edit=True, value=50)

    def close(self, *args):
        mc.deleteUI(self.windowName)


TweenWindow().show()

```

<a name="g313z"></a>
# contrary library UI（控制器库工具）
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1649488838209-6de22298-0a1a-4947-9e7b-b59382093e87.png#averageHue=%234e4e4b&clientId=u4fc22727-5a7f-4&errorMessage=unknown%20error&from=paste&height=356&id=ud7f2af05&originHeight=356&originWidth=325&originalType=binary&ratio=1&rotation=0&showTitle=false&size=48533&status=error&style=none&taskId=u8ff3f457-bf31-4385-a185-25f11393050&title=&width=325)将学习对文件的操作以及通过播放预览（playblast）命令得到缩略图，以及通过PySide2来完成UI的制作
<a name="D9DEb"></a>
## maya文件操作以及播放预览（playblast）
USERAPPDIR的路径是：C:\Users\Admin\Documents\maya<br />DIRECTORY的路径是：C:\Users\Admin\Documents\maya\controllerLibrary<br />**info的作用：调用方法时接收自定义的字典信息（不需要大括号）![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1649394075265-3eea7f0d-8a00-4f58-b4c8-598fab080321.png#averageHue=%23557f9c&clientId=ua5c7273c-270d-4&errorMessage=unknown%20error&from=paste&height=65&id=u19d521e4&originHeight=65&originWidth=552&originalType=binary&ratio=1&rotation=0&showTitle=false&size=33417&status=error&style=none&taskId=ua24a6fe0-f427-4e6d-a2a5-b93df0a0f1c&title=&width=552)然后以字典格式存储信息。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1649394139186-a48c31a0-60cb-48ce-a814-8aa69b7007e0.png#averageHue=%23444440&clientId=ua5c7273c-270d-4&errorMessage=unknown%20error&from=paste&height=36&id=u68d73616&originHeight=36&originWidth=364&originalType=binary&ratio=1&rotation=0&showTitle=false&size=18574&status=error&style=none&taskId=u518e121c-9fe6-41c9-96ec-e5671497e76&title=&width=364)

```python
from maya import cmds
import os
import json
import pprint

USERAPPDIR = cmds.internalVar(userAppDir=True)  # 此变量存的是maya的路径
DIRECTORY = os.path.join(USERAPPDIR, 'controllerLibrary')  # 此操作是在maya的路径下新增加一个controllerLibrary路径


# 使用os.path.join的好处是不需要担心不同操作系统的文件路径命名格式


def createDirectory(directory=DIRECTORY):
    if not os.path.exists(directory):
        os.mkdir(directory)  # 如果路径下没有文件夹就新建一个


class ControllerLibrary(dict):  # 将类继承自dict
    def save(self, name, directory=DIRECTORY, screenshot=True, **info):
        createDirectory(directory)
        path = os.path.join(directory, '%s.ma' % name)  # path为ma文件路径
        infoFile = os.path.join(directory, '%s.json' % name)  # infoFile为json文件路径
        # 为信息字典除了自定义的信息外，增加name和path的信息。
        info['name'] = name
        info['path'] = path

        cmds.file(rename=path)  # 选择保存ma文件路径以及规定名字
        if cmds.ls(selection=True):
            cmds.file(force=True, typ='mayaAscii', exportSelected=True)  # 为选择的物体创建文件
        else:
            cmds.file(save=True, typ='mayaAscii', force=True)  # 保存整个场景
        if screenshot:
            info['screenshot'] = self.saveScreenshot(name, directory=directory)
        with open(infoFile, 'w') as f:  # 安全地创建文件并执行写入操作
            json.dump(info, f, indent=4)  # 将info的信息转存到json文件中，并增加缩进为4，info为调用函数时自定义的信息

        self[name] = info  # 保存的同时更新对象字典，对象字典的格式：名字对应信息字典。

    def find(self, directory=DIRECTORY):  # 返回所有的ma文件名以及对应的文件路径（字典）
        if not os.path.exists(directory):
            return
        files = os.listdir(directory)  # 获取自定义库中的所有文件
        mayaFiles = [f for f in files if f.endswith('.ma')]  # 只获取ma格式的文件

        for ma in mayaFiles:
            name, ext = os.path.splitext(ma)  # 将名字和格式名分割开
            path = os.path.join(directory, ma)  # 得到ma格式文件路径
            infoFile = '%s.json' % name  # 对于所有保存的ma文件得到对应的json文件名
            if infoFile in files:  # 如果有对应json文件
                infoFile = os.path.join(directory, infoFile)  # 得到json文件路径

                with open(infoFile, 'r') as f:
                    info = json.load(f)  # 读取json数据
            else:
                info = {}  # 没有对应json文件的也给一个信息字典
            screenshot = '%s.jpg' % name
            if screenshot in files:  # 根据保存的截图根据名字进行匹配。
                info['screenshot'] = os.path.join(directory, screenshot)

            info['name'] = name
            info['path'] = path

            self[name] = info  # 将ma文件名字和路径一一对应（字典）

        pprint.pprint(self)  # 输出字典（pprint使输出更美观）

    def load(self, name):
        path = self[name]['path']  # 读取对象字典中的信息字典中的path
        cmds.file(path, i=True, usingNamespaces=False)

    def saveScreenshot(self, name, directory=DIRECTORY):
        path = os.path.join(directory, '%s.jpg' % name)

        cmds.viewFit()  # 相当于F快捷键
        cmds.setAttr('defaultRenderGlobals.imageFormat', 8)  # 将渲染格式的图像格式设置为jpeg
        # completeFilename参数控制保存路径名，forceOverwrite意思是如果重名的话就覆盖，format为格式，width和height控制大小（200宽高对应分辨率100*100因为默认拍屏百分比为50%）
        # showOrnaments为False时设置渲染成片时不显示模型视图装饰物（例如网格,视图名字），startTime=1，endTime=1表示只获取第一帧，viewer为False表示渲染出来后不立刻浏览。
        cmds.playblast(completeFilename=path, forceOverwrite=True, format='image', width=200, height=200,
                       showOrnaments=False, startTime=1, endTime=1, viewer=False)
        return path


```
<a name="ZxYs5"></a>
## PySide2 for maya
使用showUI方法时需要使用一个变量来接收showUI方法的值，不然会因为python的垃圾回收机制错误的将窗口删除而导致窗口一出现就消失。<br />get() 方法 Vs dict[key] 访问元素区别<br />**get(key) **方法在 key（键）不在字典中时，可以返回默认值 **None** 或者设置的默认值。<br />**dict[key]** 在 key（键）不在字典中时，会触发 **KeyError** 异常。<br /> 
```python
import json
import os
import pprint

from PySide2 import QtWidgets, QtCore, QtGui
from maya import cmds

USERAPPDIR = cmds.internalVar(userAppDir=True)  # 此变量存的是maya的路径
DIRECTORY = os.path.join(USERAPPDIR, 'controllerLibrary')  # 此操作是在maya的路径下新增加一个controllerLibrary路径


# 使用os.path.join的好处是不需要担心不同操作系统的文件路径命名格式


def createDirectory(directory=DIRECTORY):
    if not os.path.exists(directory):
        os.mkdir(directory)  # 如果路径下没有文件夹就新建一个


class ControllerLibrary(dict):  # 将类继承自dict
    def save(self, name, directory=DIRECTORY, screenshot=True, **info):
        createDirectory(directory)
        path = os.path.join(directory, '%s.ma' % name)  # path为ma文件路径
        infoFile = os.path.join(directory, '%s.json' % name)  # infoFile为json文件路径
        # 为信息字典除了自定义的信息外，增加name和path的信息。
        info['name'] = name
        info['path'] = path

        cmds.file(rename=path)  # 选择保存ma文件路径以及规定名字
        if cmds.ls(selection=True):
            cmds.file(force=True, typ='mayaAscii', exportSelected=True)  # 为选择的物体创建文件
        else:
            cmds.file(save=True, typ='mayaAscii', force=True)  # 保存整个场景
        if screenshot:
            info['screenshot'] = self.saveScreenshot(name, directory=directory)
        with open(infoFile, 'w') as f:  # 安全地创建文件并执行写入操作
            json.dump(info, f, indent=4)  # 将info的信息转存到json文件中，并增加缩进为4，info为调用函数时自定义的信息

        self[name] = info  # 保存的同时更新对象字典，对象字典的格式：名字对应信息字典。

    def find(self, directory=DIRECTORY):  # 返回所有的ma文件名以及对应的文件路径（字典）
        if not os.path.exists(directory):
            return
        files = os.listdir(directory)  # 获取自定义库中的所有文件
        mayaFiles = [f for f in files if f.endswith('.ma')]  # 只获取ma格式的文件

        for ma in mayaFiles:
            name, ext = os.path.splitext(ma)  # 将名字和格式名分割开
            path = os.path.join(directory, ma)  # 得到ma格式文件路径
            infoFile = '%s.json' % name  # 对于所有保存的ma文件得到对应的json文件名
            if infoFile in files:  # 如果有对应json文件
                infoFile = os.path.join(directory, infoFile)  # 得到json文件路径

                with open(infoFile, 'r') as f:
                    info = json.load(f)  # 读取json数据
            else:
                info = {}  # 没有对应json文件的也给一个信息字典
            screenshot = '%s.jpg' % name
            if screenshot in files:  # 根据保存的截图根据名字进行匹配。
                info['screenshot'] = os.path.join(directory, name)

            info['name'] = name
            info['path'] = path

            self[name] = info  # 将ma文件名字和路径一一对应（字典）

        pprint.pprint(self)  # 输出字典（pprint使输出更美观）

    def load(self, name):
        path = self[name]['path']  # 读取对象字典中的信息字典中的path
        cmds.file(path, i=True, usingNamespaces=False)

    def saveScreenshot(self, name, directory=DIRECTORY):
        path = os.path.join(directory, '%s.jpg' % name)

        cmds.viewFit()  # 相当于F快捷键
        cmds.setAttr('defaultRenderGlobals.imageFormat', 8)  # 将渲染格式的图像格式设置为jpeg
        # completeFilename参数控制保存路径名，forceOverwrite意思是如果重名的话就覆盖，format为格式，width和height控制大小（200宽高对应分辨率100*100因为默认拍屏百分比为50%）
        # showOrnaments为False时设置渲染成片时不显示模型视图装饰物（例如网格,视图名字），startTime=1，endTime=1表示只获取第一帧，viewer为False表示渲染出来后不立刻浏览。
        cmds.playblast(completeFilename=path, forceOverwrite=True, format='image', width=200, height=200,
                       showOrnaments=False, startTime=1, endTime=1, viewer=False)
        return path


class ControllerLibraryUI(QtWidgets.QDialog):
    def __init__(self):
        super(ControllerLibraryUI, self).__init__()

        self.setWindowFlags(QtCore.Qt.WindowStaysOnTopHint)  # 使窗口置顶

        self.setWindowTitle('Controller Library UI')
        # self.library 为ControllerLibrary类的实例
        self.library = ControllerLibrary()
        # 创建实例的同时会为实例增加UI并填充。
        self.buildUI()
        self.populate()

    def buildUI(self):

        layout = QtWidgets.QVBoxLayout(self) # layout为主布局（垂直）

        # 水平的子控件
        saveWidget = QtWidgets.QWidget()
        saveLayout = QtWidgets.QHBoxLayout(saveWidget)
        layout.addWidget(saveWidget)


        self.saveNameField = QtWidgets.QLineEdit()
        saveLayout.addWidget(self.saveNameField)

        saveBtn = QtWidgets.QPushButton('Save')
        saveBtn.clicked.connect(self.save)
        saveLayout.addWidget(saveBtn)

        size = 80
        buffer = 12
        self.listWidget = QtWidgets.QListWidget()
        self.listWidget.setViewMode(QtWidgets.QListWidget.IconMode)
        self.listWidget.setIconSize(QtCore.QSize(size, size))
        self.listWidget.setResizeMode(QtWidgets.QListWidget.Adjust)  # 使列表项能跟随窗口大小而自适应调整大小
        self.listWidget.setGridSize(QtCore.QSize(size + buffer, size + buffer))
        layout.addWidget(self.listWidget)

        btnWidget = QtWidgets.QWidget()
        btnLayout = QtWidgets.QHBoxLayout(btnWidget)
        layout.addWidget(btnWidget)

        importBtn = QtWidgets.QPushButton('Import')
        importBtn.clicked.connect(self.load)
        btnLayout.addWidget(importBtn)

        refreshBtn = QtWidgets.QPushButton('Refresh')
        refreshBtn.clicked.connect(self.populate)
        btnLayout.addWidget(refreshBtn)

        closeBtn = QtWidgets.QPushButton('Close')
        closeBtn.clicked.connect(self.close)
        btnLayout.addWidget(closeBtn)

    def populate(self):
        self.listWidget.clear()
        self.library.find()

        for name, info in self.library.items():
            item = QtWidgets.QListWidgetItem(name)
            self.listWidget.addItem(item)

            screenshot = info.get('screenshot')
            if screenshot:
                icon = QtGui.QIcon(screenshot)
                item.setIcon(icon)
            item.setToolTip(pprint.pformat(info))

    def load(self):
        currentItem = self.listWidget.currentItem()

        if not currentItem:
            return

        name = currentItem.text()
        self.library.load(name)

    def save(self):
        name = self.saveNameField.text()
        if not name.strip():
            cmds.warning("You must give a name!")
            return

        self.library.save(name)
        self.populate()
        self.saveNameField.setText('')


def showUI():
    ui = ControllerLibraryUI()
    ui.show()
    return ui

```
<a name="sHbvd"></a>
# lightingManager
源码：[https://github.com/dgovil/PythonForMayaSamples/blob/master/lightManager/lightManager.py](https://github.com/dgovil/PythonForMayaSamples/blob/master/lightManager/lightManager.py)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1665995561940-63e28faf-3177-44f9-9a0f-1f2b64cb1f86.png#averageHue=%23454545&clientId=u62ebb92f-db9d-4&from=paste&height=1358&id=uab4975ed&originHeight=1358&originWidth=546&originalType=binary&ratio=1&rotation=0&showTitle=false&size=20165&status=done&style=none&taskId=u74b9d9d5-b697-40d5-9be5-c5cea3f80ca&title=&width=546)
<a name="tTW9c"></a>
## 知识点：
<a name="Z6eUe"></a>
### partial函数
from functools import partial<br />通过partial可以通过一个已有的函数，快速创建出一个根据这个已有的函数扩展的新函数。<br />通过partial可以只使用一行代码就可以实现调用函数并传递参数来创建对应类型灯光。![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1650422509623-4979120e-8985-4ed7-9b47-5dd3a9c6af69.png#averageHue=%23312e2c&clientId=u6a4b9ddd-4b51-4&errorMessage=unknown%20error&from=paste&height=61&id=u7016d0f9&originHeight=61&originWidth=566&originalType=binary&ratio=1&rotation=0&showTitle=false&size=13681&status=error&style=none&taskId=uf0a5bb89-a32e-40f3-985d-dcad6e73343&title=&width=566)<br />partial函数的名字叫偏函数。<br />偏函数的使用是将一个旧函数，为其参数添加默认值然后得到一个默认使用刚才添加的默认值参数的新函数。<br />[偏函数](https://www.liaoxuefeng.com/wiki/1016959663602400/1017454145929440)
<a name="jRb49"></a>
### lambda函数
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1665994777469-d2a78757-d237-4699-a8df-a7145215fae8.png#averageHue=%23f6f4f2&clientId=u62ebb92f-db9d-4&from=paste&height=77&id=u2c795790&originHeight=77&originWidth=619&originalType=binary&ratio=1&rotation=0&showTitle=false&size=5845&status=done&style=none&taskId=ubaeb00f4-6c1d-4b4d-82f4-9079f0785ce&title=&width=619)<br />匿名函数的意思是他是一个函数，但是他没有名字，当然也可以把lambda的结果赋予一个变量，那么那个变量也就能变成一个函数了。<br />举例：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1665994912565-407b3933-446d-4e43-b2ae-d9fd1b674a9e.png#averageHue=%230f830d&clientId=u62ebb92f-db9d-4&from=paste&height=64&id=u9706c283&originHeight=64&originWidth=234&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2976&status=done&style=none&taskId=u3126f118-9da5-4472-958f-88aea428656&title=&width=234)<br />以这节课的代码举例：soloBtn.toggled.connect(lambda val: self.onSolo.emit(val))  当按钮被激活时就直接使用lambda函数，不需要再定义函数了，按钮被激活就传入True（也就是val，val是形参），然后方法是 self.onSolo.emit(val)  这里的onSolo是之前的自定义的信号，emit是发送的意思，意思是向槽发送的数值。当信号进行emit时，就会执行这个信号所连接的函数，并且发送emit的参数。
<a name="gZtXw"></a>
### isinstance函数与basestring函数
isinstance() 函数来判断一个对象是否是一个已知的类型，类似 type()。<br />_如果要判断两个类型是否相同推荐使用 isinstance()。_<br />isinstance(obj, basestring) 等价于 isinstance(obj, (str, unicode))。
<a name="vyT3q"></a>
### pynode
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1650423645383-fbd19826-10cf-48ca-ac9b-4e8c2cec5bb4.png#averageHue=%23292827&clientId=u6a4b9ddd-4b51-4&errorMessage=unknown%20error&from=paste&id=u02dbae2d&originHeight=387&originWidth=807&originalType=url&ratio=1&rotation=0&showTitle=false&size=207073&status=error&style=none&taskId=ua570155c-ecc6-40a7-9208-2713f0319e4&title=)<br />因此如果是在maya中通过鼠标点击创建的灯光需要通过PyNode转化成PyNode类型<br />if isinstance(light, basestring):<br />    light = pm.PyNode(light)  # 将不是通过pymel创建的灯光也转化为PyNode类型
<a name="VYqaK"></a>
### scrollWidget
![](https://cdn.nlark.com/yuque/0/2022/png/2623605/1650428346436-8a8a67df-65b7-4aed-993d-e6fff634c949.png#averageHue=%23fefaf6&clientId=u6a4b9ddd-4b51-4&errorMessage=unknown%20error&from=paste&id=udad06788&originHeight=540&originWidth=960&originalType=url&ratio=1&rotation=0&showTitle=false&status=error&style=none&taskId=u06b5caad-c08c-49bd-a8d7-c4bfe7aedf4&title=)
<a name="a4wGT"></a>
### 删除UI控件的方法
def deleteLight(self):<br />    # 当删除灯光的同时也需要删除控件<br />    self.setParent(None)<br />    self.setVisible(False)<br />    self.deleteLater()
<a name="KWcBc"></a>
### 获取控件中的所有子控件并操作
阅读saveLights函数
<a name="qOPno"></a>
### logging模块
[https://blog.csdn.net/liuskyter/article/details/102657142?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_title~default-1.pc_relevant_default&spm=1001.2101.3001.4242.2&utm_relevant_index=4](https://blog.csdn.net/liuskyter/article/details/102657142?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_title~default-1.pc_relevant_default&spm=1001.2101.3001.4242.2&utm_relevant_index=4)
<a name="Ufn9i"></a>
### 将Qt的UI窗口和MAYA绑定到一起（窗口可以内嵌到maya中）并可以设置停靠地点
详情看代码中的getMayaMainWindow()和getDock(name='LightingManagerDock')和deleteDock(name='LightingManagerDock')<br />其中LightingManagerDock代表为控件起的名字来代表控件。 name是一个变量，是为了方便查看以及方法内容的使用
<a name="U6I6w"></a>
### shadingNode和pointLight与spotLight命令的区别：
maya自带的命令pointLight 和 spotLight命令都可以直接使用生成对应的灯光，并且生成的灯光结果是一个shape类型的<br />而使用shadingNode命令可以生成areaLight与volumeLight，生成的灯光的结果是transform类型的，这导致了以后的通过它来获取灯光类型形成了障碍。
<a name="kQAxO"></a>
### 代码
```python
import os
from PySide2 import QtWidgets, QtCore
import pymel.core as pm
from functools import partial
from shiboken2 import wrapInstance
from maya import OpenMayaUI as omui
import logging  # 这是一种比使用print语句更好的记录输出的方式
import json
import time

logging.basicConfig()  # 使用默认设置日志级别与输出格式
logger = logging.getLogger('LightingManager')  # 创建一个日志器
logger.setLevel(logging.DEBUG)  # 设置日志器的级别


def getMayaMainWindow():  # 得到maya的主窗口
    win = omui.MQtUtil_mainWindow()  # 得到maya主窗口的内存地址
    # 使用wrapInstance方法将其转换为python可以理解的内容
    # 将它转换成QMainWindow
    ptr = wrapInstance(long(win), QtWidgets.QMainWindow)
    return ptr  # 返回maya主窗口这个QMainWindow


def getDock(name='LightingManagerDock'):
    deleteDock(name)  # 如果已经存在自定义的LightingManagerDock窗口就删除掉
    ctrl = pm.workspaceControl(name, dockToMainWindow=('right', True),
                               label='Lighting Manager')  # 在工作区的右区域生成一个窗口名字为变量name标题设置为label
    qtCtrl = omui.MQtUtil_findControl(ctrl)  # 使用OpenMayaUI API来获得与名称相关联的实际Qt小部件
    ptr = wrapInstance(long(qtCtrl), QtWidgets.QWidget)  # 使用wrapInstance将其转换为Python可以理解的内容，在本例中是一个QWidget
    return ptr  # 返回LightingManagerDock这个QWidget


def deleteDock(name='LightingManagerDock'):
    if pm.workspaceControl(name, q=True, exists=True):
        pm.deleteUI(name)


class LightManager(QtWidgets.QWidget):
    lightTypes = {
        "Point Light": pm.pointLight,
        "Spot Light": pm.spotLight,
        "Directional Light": pm.directionalLight,
        "Area Light": partial(pm.shadingNode, 'areaLight', asLight=True),
        "Volume Light": partial(pm.shadingNode, 'volumeLight', asLight=True)
    }

    def __init__(self, dock=True):
        if dock:
            parent = getDock()  # 默认将灯光信息的父窗口设置为dock
        else:
            deleteDock()  # 删除dock窗口
            # 尝试删除lightingManager窗口（父窗口为MayaMainWindow），如果不存在就记录日志。（不会中止程序）
            # 好处是既可以实现多次运行程序只生成一个窗口，也不会因为没生成过窗口而报错。
            try:
                pm.deleteUI('lightingManager')
            except:
                logger.debug('No previous UI exists')
            # 如果设置dock为False，那么就使用默认的将父窗口设置为maya主窗口，并将灯光信息存入到父窗口上面
            parent = QtWidgets.QDialog(parent=getMayaMainWindow())
            # 我们设置了它的名称，以便以后可以找到并删除它
            parent.setObjectName('lightingManager')
            parent.setWindowTitle('Lighting Manager')
            # 生成布局来存放灯光信息
            layout = QtWidgets.QVBoxLayout(parent)
        super(LightManager, self).__init__(parent=parent)
        self.buildUI()
        self.populate()

        self.parent().layout().addWidget(self)  # 将灯光信息存放到主窗口的布局中
        if not dock:
            parent.show()

    def populate(self):
        # 点击refresh按钮时调用，首先将滑动条控件中的内容清空，然后再根据场景灯光类型将场景灯光通过addLight方法向滑动条控件中添加灯光控件
        # 可以通过for循环配合self.findChildren(LightWidget)来删除控件，这里介绍了如何通过while循环删除控件

        while self.scrollLayout.count():
            widget = self.scrollLayout.takeAt(0).widget()
            if widget:
                # 之所以没有widget.setParent(None)这个操作是因为takeAt（0）已经执行了这个操作
                widget.setVisible(False)
                widget.deleteLater()
        for light in pm.ls(type=('areaLight', 'spotLight', 'pointLight', 'directionalLight', 'volumeLight')):
            self.addLight(light)

    def buildUI(self):
        layout = QtWidgets.QGridLayout(self)  # 为主窗口创建一个表格布局

        # 创建下拉列表框控件存放灯光种类，控件设置在主窗口的表格布局中
        self.lightTypeCB = QtWidgets.QComboBox()
        for lightType in sorted(self.lightTypes):
            self.lightTypeCB.addItem(lightType)
        layout.addWidget(self.lightTypeCB, 0, 0, 1, 2)

        # 按钮控件在主窗口的表格布局中
        createBtn = QtWidgets.QPushButton('Create')
        createBtn.clicked.connect(self.createLight)
        layout.addWidget(createBtn, 0, 2)

        # 创建一个QWidget对象scrollWidget用来存放滑动条
        scrollWidget = QtWidgets.QWidget()
        scrollWidget.setSizePolicy(QtWidgets.QSizePolicy.Maximum,
                                   QtWidgets.QSizePolicy.Maximum)  # 设置滑动条控件中的内容的水平与垂直方向大小策略
        self.scrollLayout = QtWidgets.QVBoxLayout(scrollWidget)  # 滑动条控件中有一个垂直布局用来存放灯光控件

        scrollArea = QtWidgets.QScrollArea()
        scrollArea.setWidgetResizable(True)
        scrollArea.setWidget(scrollWidget)
        layout.addWidget(scrollArea, 1, 0, 1, 3)

        saveBtn = QtWidgets.QPushButton('Save')
        saveBtn.clicked.connect(self.saveLights)
        layout.addWidget(saveBtn, 2, 0)

        importBtn = QtWidgets.QPushButton('Import')
        importBtn.clicked.connect(self.importLights)
        layout.addWidget(importBtn, 2, 1)

        refreshBtn = QtWidgets.QPushButton('Refresh')
        refreshBtn.clicked.connect(self.populate)
        layout.addWidget(refreshBtn, 2, 2)

    def saveLights(self):
        properties = {}  # 定义一个字典来存取灯光信息

        for lightWidget in self.findChildren(LightWidget):  # 遍历所有的灯光信息控件
            light = lightWidget.light
            transform = light.getTransform()

            properties[str(transform)] = {
                'translate': list(transform.translate.get()),  # 需要使用list格式json才能进行编码
                'rotation': list(transform.rotate.get()),  # # 需要使用list格式json才能进行编码
                'lightType': pm.objectType(light),  # 这里必须要使用shape类型的灯光节点才能够得到正确的lightType
                'intensity': light.intensity.get(),
                'color': light.color.get()
            }
            # 获取maya文档路径并向后添加一个lightManager路径赋予director
        director = self.getDirectory()
        # 创建json文件路径以及名字根据当前时间的格式（月日）来命名
        lightFile = os.path.join(director, 'lightFile_%s.json' % time.strftime('%m%d'))
        with open(lightFile, 'w') as f:
            json.dump(properties, f, indent=4)  # 将info的信息转存到json文件中，f为别名并增加缩进为4，info为调用函数时自定义的信息
        logger.info('Saving file to %s' % lightFile)  # 日志器输出保存的json文件的路径

    def getDirectory(self):
        director = os.path.join(pm.internalVar(userAppDir=True), 'lightManager')
        if not os.path.exists(director):  # 如果director路径中没有存在文件夹那么就生成对应的文件夹
            os.mkdir(director)
        return director

    def importLights(self):
        directory = self.getDirectory()
        # 打开一个文件浏览器，并定义文件浏览器的标题和目录
        # filename为一个元组 第一个元素为选中的文件的路径，第二个元素是空。（不包含文件夹中所有元素，也不是单独一个字符串）
        fileName = QtWidgets.QFileDialog.getOpenFileName(self, "Light Browser", directory)
        with open(fileName[0], 'r') as f:
            properties = json.load(f)

        for light, info in properties.items():  # light为灯光节点名字，info为信息字典
            lightType = info.get('lightType')  # 先找到json文件中的灯光类型
            for lt in self.lightTypes:  # 对于我们支持的每个light类型，我们检查它们是否与light类型匹配
                if ('%sLight' % lt.split()[0].lower()) == lightType:  # 如果找到对应的灯光类型就跳出循环后根据信息灯光
                    break
            else:
                # 如果没有找到对应的灯光类型就结束这一次循环进入下一个循环
                # logger是用来调试生成日志使用的，使用logger生成light和lightType来观察哪里出现了问题
                logger.info('Cannot find a corresponding light type for %s(%s)' % (light, lightType))
                continue
            # 调用方法得到光的shape节点
            light = self.createLight(lightType=lt)
            # 设置光的shape参数
            light.intensity.set(info.get('intensity'))
            light.color.set(info.get('color'))

            # 得到光的变换来设置它的参数
            transform = light.getTransform()
            transform.translate.set(info.get('translate'))
            transform.rotate.set(info.get('rotation'))  # 执行完之后进入下一个循环再次根据灯光类型生成灯光

        self.populate()  # 灯光生成完成之后，调用populate方法来刷新得到UI

    def createLight(self, lightType=None, add=True):  # 每使用一次create就调用LightWidget类创建灯光控件放置在滑动条控件中

        if not lightType:  # 如果没有指定lightType就根据列表框中的文字生成
            lightType = self.lightTypeCB.currentText()
        # 得到创建对应灯光类型的函数
        func = self.lightTypes[lightType]
        # 调用函数来创建灯光
        light = func()
        if add:
            self.addLight(light)
        return light

    def addLight(self, light):
        # 这将为给定的光源创建一个LightWidget，并将其添加到UI中
        # 首先我们创建LightWidget
        widget = LightWidget(light)
        # 然后，我们将小部件的onSolo信号连接到我们的方法中
        widget.onSolo.connect(self.onSolo)  # onSolo是信号，self.onSolo是槽
        # 最后，我们将其添加到scrollLayout
        self.scrollLayout.addWidget(widget)

    def onSolo(self, value):
        lightWidgets = self.findChildren(LightWidget)  # 得到所有LightWidget控件的列表
        for widget in lightWidgets:
            # 每个信号都让我们知道是谁发送的，我们可以通过sender()查询
            # 对于每个小部件，我们检查它是否是发送者
            if widget != self.sender():
                # 如果不是小部件，我们将禁用它
                widget.disableLight(value)


class LightWidget(QtWidgets.QWidget):
    onSolo = QtCore.Signal(bool)  # 自定义信号，接收bool类型的

    def __init__(self, light):
        super(LightWidget, self).__init__()
        if isinstance(light, basestring):
            light = pm.PyNode(light)  # 这里接收的light参数是通过create创建的灯光，因为创建灯光的方式不完全相同，因此都转换成pyNode的类型方便操作

        # 因为通过shadingNode命令生成的灯光返回是transform类型的
        # 如果要通过objectType命令反推灯光类型的名字需要通过shape类型的节点
        # 因此加一个判断，如果灯光的节点类型是transform类型就更改为shape类型
        if isinstance(light, pm.nodetypes.Transform):
            light = light.getShape()
        self.light = light
        self.buildUI()

    def buildUI(self):
        layout = QtWidgets.QGridLayout(self)

        self.name = QtWidgets.QCheckBox(str(self.light.getTransform()))  # 灯光的名字
        self.name.setChecked(self.light.getTransform().visibility.get())  # 根据灯光的可视性自动设置复选框的状态
        self.name.toggled.connect(
            lambda val: self.light.getTransform().visibility.set(val))  # 当复选框改变时调用lambda函数，传入val（0，1，2）然后返回冒号后面的内容
        layout.addWidget(self.name, 0, 0)

        soloBtn = QtWidgets.QPushButton('solo')
        soloBtn.setCheckable(True)
        soloBtn.toggled.connect(lambda val: self.onSolo.emit(val))  # 当solo按钮被按下时向onSolo信号发送val值（按下时为True，反之False）
        layout.addWidget(soloBtn, 0, 1)

        deleteBtn = QtWidgets.QPushButton('X')
        deleteBtn.clicked.connect(self.deleteLight)
        deleteBtn.setMaximumWidth(20)
        layout.addWidget(deleteBtn, 0, 2)

        intensity = QtWidgets.QSlider(QtCore.Qt.Horizontal)  # 创建水平滑块控件
        intensity.setMinimum(1)
        intensity.setMaximum(1000)
        intensity.setValue(self.light.intensity.get())
        intensity.valueChanged.connect(lambda val: self.light.intensity.set(val))
        layout.addWidget(intensity, 1, 0, 1, 2)

        self.colorBtn = QtWidgets.QPushButton()
        self.colorBtn.setMaximumWidth(20)
        self.colorBtn.setMinimumHeight(20)
        self.setButtonColor()
        self.colorBtn.clicked.connect(self.setColor)
        layout.addWidget(self.colorBtn, 1, 2)

    def setColor(self):
        lightColor = self.light.color.get()  # 得到灯光的颜色
        color = pm.colorEditor(rgbValue=lightColor)  # 调用maya的颜色编辑器，默认颜色为灯光颜色，color为我们期望的颜色
        # 通过pm.colorEditor颜色编辑器得到的颜色为字符串类型的，且字之间有空格，因此通过列表生成式以及split将rgba数值分别传递给rgba变量
        r, g, b, a = [float(c) for c in color.split()]
        color = (r, g, b)

        self.light.color.set(color)
        self.setButtonColor(color)

    def setButtonColor(self, color=None):
        if not color:
            # 如果没有设置按钮颜色，那么就自动获取对应灯光的颜色
            color = self.light.color.get()
        # 确保提供的颜色为3个项目的列表
        assert len(color) == 3, "You must provide a list of 3 colors"  # 通过assert 判断 len（color） 如果为False则报错为True则正常进行
        # maya里的数值为0~1，而我们需要0~255的数值来设置UI的颜色
        r, g, b = [c * 255 for c in color]
        # 通过类CSS的方法设置按钮的颜色
        self.colorBtn.setStyleSheet('background-color: rgba(%s, %s, %s, 1.0)' % (r, g, b))

    def disableLight(self, value):
        self.name.setChecked(not value)

    def deleteLight(self):
        # 当删除灯光的同时也需要删除控件
        # 前两行是防止python和Qt发生冲突而使用的
        # 理论上只需要第三行就可以了，第三行会自动执行前两行
        self.setParent(None)
        self.setVisible(False)
        self.deleteLater()
        pm.delete(self.light.getTransform())  # 需要删除变换层而不仅仅是形状层


LightManager()

```




