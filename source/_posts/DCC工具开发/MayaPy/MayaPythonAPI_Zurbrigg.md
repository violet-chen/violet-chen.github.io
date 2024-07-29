---
title: MayaPythonAPI_Zurbrigg
tags: MayaPy
categories: DCC工具开发
abbrlink: 621674d5
date: 2023-08-29 03:57:00
---
<meta name="referrer" content="no-referrer" />

[Maya Python OpenMaya 教学第一卷 Zurbrigg - Maya Python API (Volume1)_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1MG4y1W7oH/)<br />[00_introduction_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1ge4y1H7wy?p=1&vd_source=b1de3fe38e887eb40fc55a5485724480)<br />[Maya Python OpenMaya 教学第三卷 Zurbrigg - Maya Python API (Volume3)_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1ye4y1r7Yv/)
<a name="lj7rs"></a>
# 第一卷
<a name="hJDLu"></a>
## Maya API的应用场景:
maya api 主要应用于扩展maya，例如它可以用来为maya添加新的：节点，命令，工具，发射器等<br />当需要遍历很多数据时，使用maya api 要比maya command要快很多<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1667383421121-2ac3d043-5149-48d8-891e-ce6e905f4252.png#averageHue=%230a0a0a&clientId=u9187013c-10f8-4&from=paste&height=644&id=u3947ac1b&originHeight=580&originWidth=557&originalType=binary&ratio=1&rotation=0&showTitle=false&size=93832&status=done&style=none&taskId=u9e3feeec-c18c-4ec6-b6fd-08c68cfaa93&title=&width=618.8889052838459)
<a name="ojBpd"></a>
## C++的利与弊与python的利与弊
<a name="NizdK"></a>
### C++
左边是好处，右边是坏处<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1667460561714-02cc79bc-5a09-4d66-ae5b-4b14952c5fa9.png#averageHue=%23070707&clientId=u7c600ae3-8851-4&from=paste&height=450&id=uef85ad53&originHeight=405&originWidth=1576&originalType=binary&ratio=1&rotation=0&showTitle=false&size=137560&status=done&style=none&taskId=ua2aeee3a-e970-4573-81f2-14523c3abaa&title=&width=1751.1111574997149)
<a name="UJU6c"></a>
### python
左边是好处，右边是坏处<br /> ![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1667460536414-c4f0fd77-9fb9-41cd-a74c-e00835523e53.png#averageHue=%23070707&clientId=u7c600ae3-8851-4&from=paste&height=411&id=uc30849e2&originHeight=370&originWidth=1463&originalType=binary&ratio=1&rotation=0&showTitle=false&size=119984&status=done&style=none&taskId=u34a04e09-3889-467a-9564-6e9e0908df3&title=&width=1625.555598618073)
<a name="JEY1o"></a>
## api2.0与api1.0的一些区别
api2.0：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1667463343036-0b4a6649-ed06-4c3e-8202-5373d1f8462d.png#averageHue=%232a2b27&clientId=u7c600ae3-8851-4&from=paste&height=48&id=wST9g&originHeight=43&originWidth=333&originalType=binary&ratio=1&rotation=0&showTitle=false&size=14164&status=done&style=none&taskId=u18be0ca0-c1b6-4516-9fec-fb2da4c89af&title=&width=370.00000980165294)<br />api1.0：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1667463365727-46e6f487-7ebd-4849-a895-5b83867057b0.png#averageHue=%232b2c2a&clientId=u7c600ae3-8851-4&from=paste&height=49&id=uf79a2471&originHeight=44&originWidth=286&originalType=binary&ratio=1&rotation=0&showTitle=false&size=12305&status=done&style=none&taskId=ube2ab404-30cb-49ac-9062-8f80bc9e075&title=&width=317.77778619601423)

api2.0自带MFnPlugin方法，而api1.0没有MFnPlugin方法，api1.0需要额外导入OpenMayaMPx模块来使用这个模块的MFnPlugin，MPxNode，MPxCommand等方法

<a name="ctKU8"></a>
## 脚本(scripts)与插件(plugin)的区别
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1667464768035-cae1e0b8-6c17-4c09-8690-5441abfb36ab.png#averageHue=%23060606&clientId=u7c600ae3-8851-4&from=paste&height=573&id=u01c321c5&originHeight=516&originWidth=1601&originalType=binary&ratio=1&rotation=0&showTitle=false&size=193951&status=done&style=none&taskId=u88d271e3-3583-4dac-843e-bc4ff1b0da5&title=&width=1778.8889360133526)

<a name="Y4Hry"></a>
## 一种简单的让maya识别到自定义插件的方式
在maya的版本文档下新建一个plug-ins文件夹，将插件放到这个文件夹下。<br />这种方式虽然简单，但是有个缺点是如果有多个版本的maya，那么需要在每个版本的maya文件夹下都要新建plug-ins文件夹。
<a name="sVFQs"></a>
# ![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1667464831496-229a0aaa-265e-4126-93bd-cb14db98d2a9.png#averageHue=%23eae4ce&clientId=u7c600ae3-8851-4&from=paste&height=344&id=u5f2fcb0a&originHeight=310&originWidth=496&originalType=binary&ratio=1&rotation=0&showTitle=false&size=77486&status=done&style=none&taskId=u2e7496e4-e5e6-44d4-8cc4-adfe38f0d22&title=&width=551.1111257105701)
<a name="JXzvq"></a>
## 写maya插件的模板
```python
# coding: utf-8
import maya.api.OpenMaya as om
import maya.cmds as cmds

def maya_useNewAPI():
    """ 告知maya，使用的是maya api 2.0 """
    pass

def initializePlugin(plugin): 
    """ 插件加载时执行这个函数"""
    vendor = "RuiChen"  # 插件制作人的名字
    version = "1.0.0"  # 插件的版本

    om.MFnPlugin(plugin, vendor, version)  # 定义插件

def uninitializePlugin(plugin):
    """ 插件取消加载时执行这个函数"""
    pass

if __name__ == '__main__':
    """ 注册后，在maya脚本编辑器中的使用方法 """
    plugin_name = "empty_plugin.py"  # 插件的文件名
    # 如果插件加载了就先取消加载插件
    cmds.evalDeferred('if cmds.pluginInfo("{0}", q=True, loaded=True): cmds.unloadPlugin("{0}")'.format(plugin_name))
    # 如果插件没有加载就加载插件
    cmds.evalDeferred('if not cmds.pluginInfo("{0}", q=True, loaded=True): cmds.loadPlugin("{0}")'.format(plugin_name))

```
<a name="dJth8"></a>
## Hello World
<a name="k9ZiZ"></a>
### HelloWorld命令
```python
# coding: utf-8
import maya.api.OpenMaya as om
import maya.cmds as cmds


def maya_useNewAPI():
    pass


class HelloWorldCmd(om.MPxCommand):
    COMMAND_NAME = "HelloWorld"

    def __init__(self):
        super(HelloWorldCmd, self).__init__()

    def doIt(self, args):
        """ 执行的命令 """
        print("Hello, World!")

    @classmethod
    def creator(cls):
        """ 注册maya命令时使用的方法，用来得到类的实例 """
        return HelloWorldCmd()


def initializePlugin(plugin):
    """ 插件加载时执行这个函数"""
    vendor = "RuiChen"  # 插件制作人的名字
    version = "1.0.0"  # 插件的版本

    plugin_fn = om.MFnPlugin(plugin, vendor, version)  # 定义插件

    try:
        # 向maya注册一个新命令,第一个参数是命令的名字，第二个参数是类的实例
        plugin_fn.registerCommand(HelloWorldCmd.COMMAND_NAME, HelloWorldCmd.creator)
    except:
        om.MGlobal.displayError("Failed to register command: {0}".format(HelloWorldCmd.COMMAND_NAME))  # 注册失败时输出


def uninitializePlugin(plugin):
    """ 插件取消加载时执行这个函数 """
    plugin_fn = om.MFnPlugin(plugin)
    try:
        plugin_fn.deregisterCommand(HelloWorldCmd.COMMAND_NAME)  # 取消注册新命令
    except:
        om.MGlobal.displayError("Failed to deregister command: {0}".format(HelloWorldCmd.COMMAND_NAME))  # 取消注册失败时输出


if __name__ == '__main__':
    """ 注册后，在maya脚本编辑器中的使用方法 """
    plugin_name = "command_01_HelloWorld.py"  # 插件的文件名
    # 如果插件加载了就先取消加载插件
    cmds.evalDeferred(
        'if cmds.pluginInfo("{0}", q=True, loaded=True): cmds.unloadPlugin("{0}")'.format(plugin_name))
    # 如果插件没有加载就加载插件
    cmds.evalDeferred(
        'if not cmds.pluginInfo("{0}", q=True, loaded=True): cmds.loadPlugin("{0}")'.format(plugin_name))

```
<a name="YBdwl"></a>
### HelloWorld节点
这里是创建一个helloworld节点，创建节点后会在maya界面上绘制字体<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1667802585667-f2101105-470f-4ada-aa46-9822ecb9f68d.png#averageHue=%23494848&clientId=u559e9f03-b86e-4&from=paste&height=1276&id=uc1059362&originHeight=1148&originWidth=2431&originalType=binary&ratio=1&rotation=0&showTitle=false&size=101624&status=done&style=none&taskId=ua9341f0d-6724-40be-9c6f-c75be391c03&title=&width=2701.1111826661213)
```python
# coding: utf-8
import maya.api.OpenMaya as om
import maya.api.OpenMayaUI as omui
import maya.api.OpenMayaRender as omr

import maya.cmds as cmds


def maya_useNewAPI():
    """ 告知maya，使用的是maya api 2.0 """
    pass


class HelloWorldNode(omui.MPxLocatorNode):
    TYPE_NAME = "helloworld"
    TYPE_ID = om.MTypeId(0x0007f7f7)
    DRAW_CLASSIFICATION = "drawdb/geometry/helloworld"
    DRAW_REGISTRANT_ID = "HelloWorldNode"

    def __init__(self):
        super(HelloWorldNode, self).__init__()

    @classmethod
    def creator(cls):
        return HelloWorldNode()

    @classmethod
    def initialize(cls):
        pass


class HelloWorldDrawOverride(omr.MPxDrawOverride):
    NAME = "HelloWorldDrawOverride"

    def __init__(self, obj):
        super(HelloWorldDrawOverride, self).__init__(obj, None, False)

    def prepareForDraw(self, obj_path, camera_path, frame_context, old_data):
        pass

    def supportedDrawAPIs(self):
        return omr.MRenderer.kAllDevices

    def hasUIDrawables(self):
        return True

    def addUIDrawables(self, obj_path, draw_manager, frame_context, data):
        draw_manager.beginDrawable()
        draw_manager.text2d(om.MPoint(100, 100), "Hello World")
        draw_manager.endDrawable()

    @classmethod
    def creator(cls, obj):
        return HelloWorldDrawOverride(obj)


def initializePlugin(plugin):
    """ 插件加载时执行这个函数"""
    vendor = "RuiChen"  # 插件制作人的名字
    version = "1.0.0"  # 插件的版本

    plugin_fn = om.MFnPlugin(plugin, vendor, version)  # 定义插件
    try:
        plugin_fn.registerNode(HelloWorldNode.TYPE_NAME,
                               HelloWorldNode.TYPE_ID,
                               HelloWorldNode.creator,
                               HelloWorldNode.initialize,
                               om.MPxNode.kLocatorNode,
                               HelloWorldNode.DRAW_CLASSIFICATION)
    except:
        om.MGlobal.displayError("Failed to register node: {0}".format(HelloWorldNode.TYPE_NAME))

    try:
        omr.MDrawRegistry.registerDrawOverrideCreator(HelloWorldNode.DRAW_CLASSIFICATION,
                                                      HelloWorldNode.DRAW_REGISTRANT_ID,
                                                      HelloWorldDrawOverride.creator)
    except:
        om.MGlobal.displayError("Failed to register draw override: {0}".format(HelloWorldDrawOverride.NAME))


def uninitializePlugin(plugin):
    """ 插件取消加载时执行这个函数"""
    plugin_fn = om.MFnPlugin(plugin)
    try:
        omr.MDrawRegistry.deregisterDrawOverrideCreator(HelloWorldNode.DRAW_CLASSIFICATION,
                                                        HelloWorldNode.DRAW_REGISTRANT_ID)
    except:
        om.MGlobal.displayError("Failed to deregister draw override: {0}".format(HelloWorldDrawOverride.NAME))

    try:
        plugin_fn.deregisterNode(HelloWorldNode.TYPE_ID)
    except:
        om.MGlobal.displayError("Failed to deregister node: {0}".format(HelloWorldNode.TYPE_NAME))


if __name__ == '__main__':
    """ 注册后，在maya脚本编辑器中的使用方法 """
    plugin_name = "hello_world_node.py"  # 插件的文件名
    # 如果插件加载了就先取消加载插件
    cmds.evalDeferred('if cmds.pluginInfo("{0}", q=True, loaded=True): cmds.unloadPlugin("{0}")'.format(plugin_name))
    # 如果插件没有加载就加载插件
    cmds.evalDeferred('if not cmds.pluginInfo("{0}", q=True, loaded=True): cmds.loadPlugin("{0}")'.format(plugin_name))

    cmds.evalDeferred('cmds.createNode("helloworld")')

```

<a name="WjwE1"></a>
## maya官方给的maya python api示例
首先下载maya开发者工具包，下载压缩后在devkitBase\devkit\plug-ins\scripted目录下可以看到各种示例![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668756899011-a00cc1a7-62fa-4227-a20e-6fe3d5068eda.png#averageHue=%23f8f5f2&clientId=ubf5ae5a3-31c1-4&from=paste&height=361&id=u9826c00d&originHeight=325&originWidth=414&originalType=binary&ratio=1&rotation=0&showTitle=false&size=32253&status=done&style=none&taskId=u4195e815-ad0b-4071-ad90-33cf4da6b01&title=&width=460.0000121858388)py开头的是使用了maya api 2.0的，其他的是使用了maya api 1.0
<a name="uhzNA"></a>
## maya api 基础
maya api 的四种对象类型：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668757424116-5bcafdfe-528a-4e28-8fa2-2776830786e9.png#averageHue=%230d0d0d&clientId=ubf5ae5a3-31c1-4&from=paste&height=413&id=u45e06f43&originHeight=372&originWidth=580&originalType=binary&ratio=1&rotation=0&showTitle=false&size=72263&status=done&style=none&taskId=u053e978a-be3a-4a87-a7ae-c7da6792118&title=&width=644.4444615163925)
<a name="HbQrQ"></a>
### MObject
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668757463577-ad1d2012-8326-4cc5-964f-d200e864d8df.png#averageHue=%23090909&clientId=ubf5ae5a3-31c1-4&from=paste&height=403&id=u9adfb691&originHeight=363&originWidth=1570&originalType=binary&ratio=1&rotation=0&showTitle=false&size=161345&status=done&style=none&taskId=uf9c7c238-452a-4b07-99fc-c108395de57&title=&width=1744.4444906564418)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668757486229-d8d55a9b-9ed9-427e-b4f9-dbc750251b5c.png#averageHue=%230c0c0b&clientId=ubf5ae5a3-31c1-4&from=paste&height=410&id=u0e624a36&originHeight=369&originWidth=1066&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36840&status=done&style=none&taskId=ub45130b7-7469-4383-8eb9-4a6fd153b6a&title=&width=1184.4444758215077)
<a name="tMLbr"></a>
### MFunction Sets
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668757603504-98b7ab6a-d4b5-4ce1-8b20-a299684d5ec0.png#averageHue=%230b0b0b&clientId=ubf5ae5a3-31c1-4&from=paste&height=591&id=uad6c347e&originHeight=532&originWidth=1925&originalType=binary&ratio=1&rotation=0&showTitle=false&size=306154&status=done&style=none&taskId=uccd13f10-394d-439a-8bc6-fb894fb2726&title=&width=2138.8889455500957)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668757617546-3e41599a-3c85-452f-aae5-766cc0d5f2d6.png#averageHue=%23030202&clientId=ubf5ae5a3-31c1-4&from=paste&height=478&id=u0f7b9081&originHeight=430&originWidth=1776&originalType=binary&ratio=1&rotation=0&showTitle=false&size=46137&status=done&style=none&taskId=ua8760436-76aa-44bc-b289-a533db449ec&title=&width=1973.3333856088157)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668758099121-90c8c82c-9144-4d07-aecb-96a98029ce5b.png#averageHue=%231e1c1b&clientId=ubf5ae5a3-31c1-4&from=paste&height=79&id=u65220e11&originHeight=71&originWidth=532&originalType=binary&ratio=1&rotation=0&showTitle=false&size=6738&status=done&style=none&taskId=ubcb16715-4419-4be2-b065-d292f84cce0&title=&width=591.1111267702083)
<a name="NvbOz"></a>
### Wrappers
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668757981249-0896516f-f88c-4e6a-b7a1-46a246eaf888.png#averageHue=%230c0c0c&clientId=ubf5ae5a3-31c1-4&from=paste&height=376&id=ud54245f5&originHeight=338&originWidth=1849&originalType=binary&ratio=1&rotation=0&showTitle=false&size=174631&status=done&style=none&taskId=u2c4ab016-58db-4b1f-8dd6-42237e46897&title=&width=2054.4444988686378)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668758001529-b6d25d43-aa16-4772-97bc-678e0f7ecf63.png#averageHue=%230b0b0a&clientId=ubf5ae5a3-31c1-4&from=paste&height=333&id=u28555cfc&originHeight=300&originWidth=1268&originalType=binary&ratio=1&rotation=0&showTitle=false&size=24703&status=done&style=none&taskId=u88125d2c-7024-4d98-85e4-d1edf78d038&title=&width=1408.8889262116995)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668758189352-8278e833-5834-4667-a300-ee18231c5229.png#averageHue=%23131313&clientId=ubf5ae5a3-31c1-4&from=paste&height=140&id=cbPpA&originHeight=126&originWidth=887&originalType=binary&ratio=1&rotation=0&showTitle=false&size=57056&status=done&style=none&taskId=u066e4b64-97b5-4f52-b7a4-b3ca8870621&title=&width=985.5555816638624)<br />迭代器也被认为是wrappers<br />迭代器类的名字前缀为MIt
<a name="XEXAt"></a>
### Proxies
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668758333101-5714a52d-bbac-4735-b67a-23c698a726b1.png#averageHue=%230a0a0a&clientId=ubf5ae5a3-31c1-4&from=paste&height=259&id=ue6ceda73&originHeight=233&originWidth=1552&originalType=binary&ratio=1&rotation=0&showTitle=false&size=109960&status=done&style=none&taskId=u2eebbf2f-1478-4212-bbf9-bfafbbeb365&title=&width=1724.444490126623)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668758345822-91311951-6d7e-4d36-834c-44a765d10526.png#averageHue=%230a0908&clientId=ubf5ae5a3-31c1-4&from=paste&height=239&id=ub00deaaf&originHeight=215&originWidth=1076&originalType=binary&ratio=1&rotation=0&showTitle=false&size=21372&status=done&style=none&taskId=u71a901fd-8fb6-438c-80d4-12ed3ebc05c&title=&width=1195.5555872269626)
<a name="tRBiS"></a>
### 举例
遍历当前maya选择的对象，根据对象是否拥有对应的函数集来输出调用函数集的功能所得到的值
```python
import maya.api.OpenMaya as om
selection = om.MGlobal.getActiveSelectionList()
for i in range(selection.length()):
    if i > 0:
        print("--------")
    obj = selection.getDependNode(i) # Return an MObject
    print("API Type: {0}".format(obj.apiTypeStr))

    if obj.hasFn(om.MFn.kDependencyNode):  # 检查这个MObject是否能够使用这个函数集
        
        depend_fn = om.MFnDependencyNode(obj)  # 将这个函数集附加到obj上
        print("Dependency Node: {0}".format(depend_fn.name()))

    if obj.hasFn(om.MFn.kTransform):
        transform_fn = om.MFnTransform(obj)
        print("Translation: {0}".format(transform_fn.translation(om.MSpace.kTransform)))
    
    elif obj.hasFn(om.MFn.kMesh):
        mesh_fn = om.MFnMesh(obj)
        print("Mesh Vertices: {0}".format(mesh_fn.getVertices()))

    elif obj.hasFn(om.MFn.kCamera):
        camera_fn = om.MFnCamera(obj)
        print("Clipping Planes: {0}, {1}".format(camera_fn.nearClippingPlane, camera_fn.farClippingPlane))


```
如果选择一个方盒子和一个摄像机，输出的内容：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668760680105-a0eeb9d2-e575-4f3b-9924-ddf512182d37.png#averageHue=%23363433&clientId=ubf5ae5a3-31c1-4&from=paste&height=122&id=u425096dc&originHeight=110&originWidth=240&originalType=binary&ratio=1&rotation=0&showTitle=false&size=4711&status=done&style=none&taskId=u8d5c9f77-07fa-4b88-8cca-88e143fe2dc&title=&width=266.66667373092105)
<a name="jnx97"></a>
## Dependence Graph（DG）
<a name="Ccttp"></a>
### DG的介绍与特点
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668761163618-33e7c611-7817-405a-9b2b-766b1d533440.png#averageHue=%230b0b0b&clientId=ubf5ae5a3-31c1-4&from=paste&height=810&id=XyC36&originHeight=729&originWidth=2096&originalType=binary&ratio=1&rotation=0&showTitle=false&size=414736&status=done&style=none&taskId=u42990e71-5a65-49d2-9e9c-a64e8f0d39f&title=&width=2328.888950583377)<br />Dependency Graph(DG)是一个基于节点的体系架构，它为创建maya场景提供了基本构建块<br />它有以下四种特点<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668761342892-93171d7e-a642-433e-aa4c-9b510cd2c498.png#averageHue=%230c0b0a&clientId=ubf5ae5a3-31c1-4&from=paste&height=476&id=uf3b601db&originHeight=428&originWidth=922&originalType=binary&ratio=1&rotation=0&showTitle=false&size=33498&status=done&style=none&taskId=ufcbe683c-7f8b-4354-ad6c-9c4062777e0&title=&width=1024.444471582955)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668761150642-0a80b927-5a60-49c4-b027-bca05a8d6836.png#averageHue=%23272726&clientId=ubf5ae5a3-31c1-4&from=paste&height=1327&id=u257632d5&originHeight=1194&originWidth=2432&originalType=binary&ratio=1&rotation=0&showTitle=false&size=879147&status=done&style=none&taskId=u4d62cf75-96a3-4cf7-ab48-e7cdc920b51&title=&width=2702.2222938066666)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668761551913-c037888d-c7cc-4033-b3e1-81f92089bc8f.png#averageHue=%230e0e0e&clientId=ubf5ae5a3-31c1-4&from=paste&height=841&id=u3a92f826&originHeight=757&originWidth=2401&originalType=binary&ratio=1&rotation=0&showTitle=false&size=610510&status=done&style=none&taskId=u7848e4b9-2ffc-492c-b063-76f725fa1c8&title=&width=2667.777848449756)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668761571232-3ad31dae-60a3-41d3-bb34-e32524d77b3f.png#averageHue=%230a0909&clientId=ubf5ae5a3-31c1-4&from=paste&height=704&id=uf1c750fd&originHeight=634&originWidth=2308&originalType=binary&ratio=1&rotation=0&showTitle=false&size=75814&status=done&style=none&taskId=ub881fa28-d2f8-4bb6-a522-6288ca49625&title=&width=2564.444512379024)
<a name="fboq8"></a>
### DG如何使用Push-Pull模型更新
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668761923835-c285aae6-d84e-439f-8f0d-612828fc6232.png#averageHue=%230e0e0e&clientId=ubf5ae5a3-31c1-4&from=paste&height=536&id=ue98daa24&originHeight=482&originWidth=2212&originalType=binary&ratio=1&rotation=0&showTitle=false&size=352674&status=done&style=none&taskId=u69e78de1-ae03-47ae-b798-4d361c6c080&title=&width=2457.777842886656)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668761946640-9119250d-ba52-4918-a15e-f01ab34b43cf.png#averageHue=%23111010&clientId=ubf5ae5a3-31c1-4&from=paste&height=470&id=u98338a51&originHeight=423&originWidth=1166&originalType=binary&ratio=1&rotation=0&showTitle=false&size=45255&status=done&style=none&taskId=u50686900-2519-45e8-a38e-e5d12bc4f14&title=&width=1295.555589876058)<br />[https://www.bilibili.com/video/BV1MG4y1W7oH?t=388.5](https://www.bilibili.com/video/BV1MG4y1W7oH?t=388.5)<br />1.例如这是一个DG结构，绿色代表这些节点都是干净的（clean），然后如果A发生改变，那么A节点就会变成脏的（dirty）状态，A节点变成了dirty状态，那么它会影响C和D都变成dirty状态<br />2.当maya要需要用到D时，发现D时dirty状态，那么它就从D出发然后追溯到A，然后更新A后，A变成了干净的状态就可以将C，D变成干净的状态了，都变成绿色后maya就可以刷新视口完成更新。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668762261343-90336c63-2aa9-44d0-bc1f-99d398d94eed.png#averageHue=%23050505&clientId=ubf5ae5a3-31c1-4&from=paste&height=423&id=u52c2d5b0&originHeight=381&originWidth=1013&originalType=binary&ratio=1&rotation=0&showTitle=false&size=77999&status=done&style=none&taskId=uaef480b3-53a1-42ff-a51b-827f01eb71c&title=&width=1125.555585372596)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668762472151-9a16e2d6-12b9-42df-a940-ce73ec65bf69.png#averageHue=%23100404&clientId=ubf5ae5a3-31c1-4&from=paste&height=452&id=ub2f38869&originHeight=407&originWidth=1500&originalType=binary&ratio=1&rotation=0&showTitle=false&size=95134&status=done&style=none&taskId=u298a6611-a2fe-4325-bc6a-39517ffabb6&title=&width=1666.6667108182567)
<a name="MfY5i"></a>
### 总结
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668762937405-0f83ed9e-427f-4338-a3ce-494525a8a6c7.png#averageHue=%230e0e0e&clientId=ubf5ae5a3-31c1-4&from=paste&height=683&id=u3f2f378f&originHeight=615&originWidth=1945&originalType=binary&ratio=1&rotation=0&showTitle=false&size=387777&status=done&style=none&taskId=u161273b9-8008-4861-b0af-daa93ecbb3d&title=&width=2161.111168361006)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668762950877-b186a562-aba5-47d0-b25e-182a33fcee83.png#averageHue=%23100f0e&clientId=ubf5ae5a3-31c1-4&from=paste&height=598&id=u299e3928&originHeight=538&originWidth=915&originalType=binary&ratio=1&rotation=0&showTitle=false&size=51259&status=done&style=none&taskId=u2ed88ca5-47bb-49b9-a4d2-ade9399bc5b&title=&width=1016.6666935991365)
<a name="s9UG4"></a>
## 自定义节点
<a name="nay0M"></a>
### 节点介绍
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668763130944-71ddc6f1-a5e5-4b4e-a5e6-c13d2bd1b7cf.png#averageHue=%2333302d&clientId=ubf5ae5a3-31c1-4&from=paste&height=1257&id=u554ce68a&originHeight=1131&originWidth=1662&originalType=binary&ratio=1&rotation=0&showTitle=false&size=369196&status=done&style=none&taskId=u496f3ed9-acd8-47e8-a191-c4822f0f9cc&title=&width=1846.6667155866282)
<a name="RSfdh"></a>
### 节点属性
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668763156514-602afe94-bd9f-4395-a23e-31c35d42d1f2.png#averageHue=%230a0a0a&clientId=ubf5ae5a3-31c1-4&from=paste&height=469&id=u008121fa&originHeight=422&originWidth=1405&originalType=binary&ratio=1&rotation=0&showTitle=false&size=162964&status=done&style=none&taskId=u2de4073e-e3fb-45b3-8f54-939757f8681&title=&width=1561.1111524664336)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668763177599-8d85e678-ca47-447e-8218-84b8e95bb9b9.png#averageHue=%230b0a09&clientId=ubf5ae5a3-31c1-4&from=paste&height=397&id=ucccb7b5c&originHeight=357&originWidth=888&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36218&status=done&style=none&taskId=u9053fc41-a882-4584-85c7-e31979437ed&title=&width=986.6666928044078)
<a name="dCqhu"></a>
### 计算方法
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668763493087-be9e5958-073a-4d4f-8745-67beb60079f4.png#averageHue=%23090909&clientId=ubf5ae5a3-31c1-4&from=paste&height=790&id=u3f359d80&originHeight=711&originWidth=2147&originalType=binary&ratio=1&rotation=0&showTitle=false&size=347598&status=done&style=none&taskId=u8a0afed6-383d-45ce-abce-b3a3bfc647e&title=&width=2385.555618751198)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668763520618-8b0d60cc-ab2b-4d15-bd61-1acb88ceb292.png#averageHue=%230a0a09&clientId=ubf5ae5a3-31c1-4&from=paste&height=733&id=u6e998dca&originHeight=660&originWidth=1554&originalType=binary&ratio=1&rotation=0&showTitle=false&size=57469&status=done&style=none&taskId=ue7713662-7819-46ca-bd4c-c15af6ccb71&title=&width=1726.6667124077137)
<a name="GbyfY"></a>
### 依赖属性
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668763577672-f2f0b925-b1e7-4329-be7d-7a46ba7d99d1.png#averageHue=%230e0e0e&clientId=ubf5ae5a3-31c1-4&from=paste&height=524&id=ub2f2148a&originHeight=472&originWidth=1586&originalType=binary&ratio=1&rotation=0&showTitle=false&size=277578&status=done&style=none&taskId=u14099266-66c8-433c-8417-51bb93f46b7&title=&width=1762.22226890517)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668763600580-5b7607ca-bd27-4cd4-910a-91b54913d0e2.png#averageHue=%23100e0d&clientId=ubf5ae5a3-31c1-4&from=paste&height=477&id=uc529be08&originHeight=429&originWidth=1062&originalType=binary&ratio=1&rotation=0&showTitle=false&size=50290&status=done&style=none&taskId=u3f261be0-8e8e-4667-9953-dada8358768&title=&width=1180.0000312593256)
<a name="aw0a0"></a>
### 修改属性
修改属性有三种方法
<a name="LB0eE"></a>
#### 使用plug修改属性
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668764346831-80c6083d-1b75-4ee4-8523-de7845605fa8.png#averageHue=%23c8cdd2&clientId=ubf5ae5a3-31c1-4&from=paste&height=283&id=ue57d47a7&originHeight=255&originWidth=1505&originalType=binary&ratio=1&rotation=0&showTitle=false&size=277460&status=done&style=none&taskId=u0c705406-6e6d-400e-a75f-4fe35e0d483&title=&width=1672.222266520984)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1668764372359-5063c355-c623-4f55-bba6-bcd44af70080.png#averageHue=%23cbd4db&clientId=ubf5ae5a3-31c1-4&from=paste&height=128&id=BcXTq&originHeight=115&originWidth=1490&originalType=binary&ratio=1&rotation=0&showTitle=false&size=30751&status=done&style=none&taskId=u167cfc41-ddfe-4f75-bfa3-ae848c87d6c&title=&width=1655.5555994128015)<br /> 
```python
import maya.api.OpenMaya as om
node_name = "pCube1"
attribute_name = "translateY"

selection_list = om.MSelectionList()
selection_list.add(node_name)

obj = selection_list.getDependNode(0)

if obj.hasFn(om.MFn.kTransform):
    transform_fn = om.MFnTransform(obj)
    
    plug = transform_fn.findPlug(attribute_name,False)  # 获取pCube的translateY的plug对象，False的含义在以后的章节讲
    
    attribute_value = plug.asDouble()  # 得到plug对应的数据
    print("{0}: {1}".format(plug, attribute_value))  #  这里输出plug虽然是pCube1.translateY，但是plug并不是字符串，plug覆盖了string方法，使其输出内容改变了。
   
    plug.setDouble(2.0)

```
```python
import maya.api.OpenMaya as om
node_name = "pCube1"
attribute_name = "translate"

selection_list = om.MSelectionList()
selection_list.add(node_name)

obj = selection_list.getDependNode(0)

if obj.hasFn(om.MFn.kTransform):
    transform_fn = om.MFnTransform(obj)
    
    plug = transform_fn.findPlug(attribute_name,False) 
    
    if plug.isCompound: # 判断插头是否是复合类型
        for i in range(plug.numChildren()): # 遍历插头的子项
            child_plug = plug.child(i)
            
            attribute_value = child_plug.asDouble()
            print("{0}: {1}".format(child_plug, attribute_value))
    
```
<a name="BLunB"></a>
#### 利用函数集自带的修改属性的方法
```python
import maya.api.OpenMaya as om
node_name = "pCube1"
attribute_name = "translate"

selection_list = om.MSelectionList()
selection_list.add(node_name)

obj = selection_list.getDependNode(0)

if obj.hasFn(om.MFn.kTransform):
    transform_fn = om.MFnTransform(obj)
    
    translation = transform_fn.translation(om.MSpace.kTransform)
    translation[1] = 3.0
    transform_fn.setTranslation(translation, om.MSpace.kTransform)
    
```
<a name="mDfst"></a>
### 创建自定义节点所需要的基础
<a name="qK48a"></a>
#### MPxNode
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669002338612-6cd488a2-a0b5-4a42-b533-029835e1112c.png#averageHue=%231f1d1b&clientId=u7be5ff65-fd52-4&from=paste&height=67&id=ua2b59691&originHeight=60&originWidth=778&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9484&status=done&style=none&taskId=u274c2a12-21b4-46a3-881f-b36d77cc888&title=&width=864.4444673444024)<br />HelloWorld节点用到的MPxLocatorNode class是MPxNode派生的。
<a name="XbsyV"></a>
#### initializePlugin()
任何新的自定义节点都需要在maya中注册，然后才能使用。<br />注册是在initializePlugin() 函数内使用MPxPlugin.registerNode()<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669002627571-0a9ab6a7-7bbd-4c42-8c41-fc59d6722fb8.png#averageHue=%23151515&clientId=u7be5ff65-fd52-4&from=paste&height=58&id=uf14fa594&originHeight=52&originWidth=1066&originalType=binary&ratio=1&rotation=0&showTitle=false&size=35968&status=done&style=none&taskId=u657637d1-41cc-41a0-9128-eeef564d1a5&title=&width=1184.4444758215077)
<a name="MyqhV"></a>
#### MPxPlugin.registerNode()
注册方法需要节点的名字，一个唯一的ID，创建的方法，初始化的方法。![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669002669128-8f96557a-60bb-4d22-be51-bf52257e5bca.png#averageHue=%230d0d0d&clientId=u7be5ff65-fd52-4&from=paste&height=258&id=vNpME&originHeight=232&originWidth=672&originalType=binary&ratio=1&rotation=0&showTitle=false&size=65799&status=done&style=none&taskId=ud60b7ac1-1cea-4b59-b4c0-73a5de343ec&title=&width=746.666686446579)
<a name="GWIJg"></a>
#### creator()
creator()用来返回一个类的新实例
<a name="FAjY7"></a>
#### initialize()
initialize()有三个作用：1.初始化所有的节点属性2.添加或修改节点的属性都在这个方法内3.只有当加载plugin时调用![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669002823683-177350b5-96c4-456d-8562-86a2638a561e.png#averageHue=%230b0b0b&clientId=u7be5ff65-fd52-4&from=paste&height=271&id=u3cb4080a&originHeight=244&originWidth=857&originalType=binary&ratio=1&rotation=0&showTitle=false&size=72938&status=done&style=none&taskId=u92e4ec28-6dbe-4706-b9dc-9dd8dd76224&title=&width=952.2222474474972)
<a name="Qkry9"></a>
#### 注：
creator()与initialize()方法可以用不同的函数名，creator与initialize是通用的容易表示的。只是一个命名约定
<a name="fYVC7"></a>
#### Compute()
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669003318484-4b8a7b71-6973-4ff7-947a-830df396d988.png#averageHue=%23060606&clientId=u7be5ff65-fd52-4&from=paste&height=139&id=u04fdd6a7&originHeight=125&originWidth=581&originalType=binary&ratio=1&rotation=0&showTitle=false&size=22040&status=done&style=none&taskId=u43cd17f4-c28f-4042-917c-cff5389dad0&title=&width=645.555572656938)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669003311035-561243ea-01cd-4745-a747-bbbd6c869d1b.png#averageHue=%230a0a0a&clientId=u7be5ff65-fd52-4&from=paste&height=326&id=u4c983ea9&originHeight=293&originWidth=1555&originalType=binary&ratio=1&rotation=0&showTitle=false&size=153631&status=done&style=none&taskId=u0966b6f8-eb7f-4450-96f8-afad2cdf399&title=&width=1727.7778235482592)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669003340185-5a47b13d-570c-4674-bc43-9e24cab712ac.png#averageHue=%23080706&clientId=u7be5ff65-fd52-4&from=paste&height=317&id=u1d2aebb6&originHeight=285&originWidth=956&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36827&status=done&style=none&taskId=u1d83cf90-56ee-431f-b3d5-10d667e9e17&title=&width=1062.2222503615021)
<a name="oQ8aa"></a>
#### postConstructor()
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669007286665-679ae1fc-3e15-4f05-93d6-9790d1ef97da.png#averageHue=%230b0b0b&clientId=u7be5ff65-fd52-4&from=paste&height=183&id=u2e060501&originHeight=165&originWidth=1357&originalType=binary&ratio=1&rotation=0&showTitle=false&size=81307&status=done&style=none&taskId=u23c02b7c-84aa-43d3-9395-a55adeea4a8&title=&width=1507.7778177202495)<br />当创建节点后调用
<a name="vw2qD"></a>
#### connectionMade() 和 connectionBroken()
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669007312866-0ed526c4-0327-4ec1-bff2-2d33ac61b0ce.png#averageHue=%230e0e0e&clientId=u7be5ff65-fd52-4&from=paste&height=194&id=ufb500e38&originHeight=175&originWidth=1053&originalType=binary&ratio=1&rotation=0&showTitle=false&size=80662&status=done&style=none&taskId=uca63225e-eaf7-44b3-a444-baf2f71ae79&title=&width=1170.0000309944162)<br />当节点连接状态发生改变时调用
<a name="tX12q"></a>
### 举例：自定义一个简单的数学节点
节点功能：将两个数相乘并输出结果值<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669019508238-3c8534af-9ab0-4dcf-8d15-a91eb495d03e.png#averageHue=%2347cd89&clientId=u7be5ff65-fd52-4&from=paste&height=223&id=u361e46aa&originHeight=201&originWidth=290&originalType=binary&ratio=1&rotation=0&showTitle=false&size=11821&status=done&style=none&taskId=ue94ba214-cf36-495e-b391-f5fb74ba7b1&title=&width=322.22223075819625)
```python
# coding: utf-8
import maya.api.OpenMaya as om
import maya.cmds as cmds

def maya_useNewAPI():
    """ 这个函数告诉了maya这个插件生成,并且生成的对象使用maya python api 2.0 """
    pass

class MutiplyNode(om.MPxNode):
    TYPE_NAME = "multiplynode"
    TYPE_ID = om.MTypeId(0x0007F7F8)
    # 提前声明节点的属性
    multiplier_obj = None
    multiplicand_obj = None
    product_obj = None

    def __init__(self):
        super(MutiplyNode, self).__init__()

    def compute(self, plug, data):
        """_summary_

        Args:
            plug (_type_): 当plug是dirty状态时,会传过来,要求更新
            data (_type_): data提供了读取和写入节点属性值的方法
        """
        if plug == MutiplyNode.product_obj:

            multiplier = data.inputValue(MutiplyNode.multiplier_obj).asInt()  # 获取multiplier_obj对象的输入的属性值
            multiplicand = data.inputValue(MutiplyNode.multiplicand_obj).asDouble()  # 获取multiplicand_obj对象的输入的属性值
            product = multiplier * multiplicand 

            product_data_handle = data.outputValue(MutiplyNode.product_obj)  # 获取product_obj对象的输出数据对象
            product_data_handle.setDouble(product)  # 设置product_obj对象的输出数据

            data.setClean(plug) # 将plug设置为clean状态


    @classmethod
    def creator(cls):
        return MutiplyNode()
    
    @classmethod
    def initialize(cls):
        numeric_attr = om.MFnNumericAttribute() # 创建一个用来设置数字系列属性的对象

        cls.multiplier_obj = numeric_attr.create("multiplier", "mul", om.MFnNumericData.kInt, 2)  # 属性长名，属性短名，属性数字类型，属性初始值
        numeric_attr.keyable = True # 设置属性可以key关键帧(这样属性就能出现在channel box中)
        numeric_attr.readable = False  #  设置属性没有输出引脚(其他属性不能读它)

        cls.multiplicand_obj = numeric_attr.create("multiplicand", "mulc", om.MFnNumericData.kDouble, 0.0)
        numeric_attr.keyable = True
        numeric_attr.readable = False

        cls.product_obj = numeric_attr.create("product", "prod", om.MFnNumericData.kDouble, 0.0)
        numeric_attr.writable = False #  设置属性没有输入引脚(其他属性不能直接写入它)
        
        # 添加属性
        cls.addAttribute(cls.multiplier_obj)
        cls.addAttribute(cls.multiplicand_obj)
        cls.addAttribute(cls.product_obj)
        # 设置属性影响
        cls.attributeAffects(cls.multiplier_obj, cls.product_obj)
        cls.attributeAffects(cls.multiplicand_obj, cls.product_obj)

def initializePlugin(plugin):
    """
    加载插件时执行此函数
    plugin: MObject用于使用MFnPlugin函数集注册插件
    """
    
    vendor = "RuiChen"
    version = "1.0.0"

    plugin_fn = om.MFnPlugin(plugin, vendor, version)
    try:
        plugin_fn.registerNode(MutiplyNode.TYPE_NAME,
                               MutiplyNode.TYPE_ID,
                               MutiplyNode.creator,
                               MutiplyNode.initialize,
                               om.MPxNode.kDependNode)
    except:
        om.MGlobal.displayError("Failed to register node: {0}".format(MutiplyNode.TYPE_NAME))

def uninitializePlugin(plugin):
    """
    取消加载插件时执行此函数
    plugin: MObject用于使用MFnPlugin函数集取消注册插件
    """    
    plugin_fn = om.MFnPlugin(plugin)
    try:
        plugin_fn.deregisterNode(MutiplyNode.TYPE_ID)
    except:
        om.MGlobal.displayError("Failed to deregister node: {0}".format(MutiplyNode.TYPE_NAME))

if __name__ == "__main__":
    """
    测试时使用
    """

    cmds.file(new=True, force=True)

    plugin_name = "multiply_node.py"

    cmds.evalDeferred('if cmds.pluginInfo("{0}", q=True, loaded=True): cmds.unloadPlugin("{0}")'.format(plugin_name))
    cmds.evalDeferred('if not cmds.pluginInfo("{0}", q=True, loaded=True): cmds.loadPlugin("{0}")'.format(plugin_name))
    
    cmds.evalDeferred('cmds.createNode("multiplynode")')
```
<a name="ql0oW"></a>
### 常用的调节属性的性质
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669019751794-e5111da0-4859-4dfe-a62b-719679fbd182.png#averageHue=%23090909&clientId=u7be5ff65-fd52-4&from=paste&height=392&id=u50257840&originHeight=353&originWidth=1175&originalType=binary&ratio=1&rotation=0&showTitle=false&size=120633&status=done&style=none&taskId=u96983a3b-dfa4-4300-94c2-b3ff711bd18&title=&width=1305.5555901409675)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669021067015-08a0e8e9-ae26-4a71-a0ca-9619d6aadb83.png#averageHue=%2320201f&clientId=u7be5ff65-fd52-4&from=paste&height=38&id=u79fd4fa9&originHeight=34&originWidth=814&originalType=binary&ratio=1&rotation=0&showTitle=false&size=11256&status=done&style=none&taskId=uae7d5d33-e785-4763-b450-46250892805&title=&width=904.4444684040405)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669019819465-9ccfd5b8-c99e-489c-8787-de360afaed0e.png#averageHue=%2320201e&clientId=u7be5ff65-fd52-4&from=paste&height=30&id=CaH2B&originHeight=27&originWidth=822&originalType=binary&ratio=1&rotation=0&showTitle=false&size=12052&status=done&style=none&taskId=uaa18bb8b-e8a9-4979-a92d-bac25b0aa99&title=&width=913.3333575284046)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669019987165-8c835b41-f49c-4b51-a3ce-0c5eac417ae6.png#averageHue=%23090909&clientId=u7be5ff65-fd52-4&from=paste&height=236&id=ub49b112e&originHeight=212&originWidth=1242&originalType=binary&ratio=1&rotation=0&showTitle=false&size=78468&status=done&style=none&taskId=u51f4de9d-ef27-46b3-9636-fbf3e5cc3af&title=&width=1380.0000365575165)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669020148684-13a906e4-90af-4aa5-be15-78c439099d50.png#averageHue=%23090909&clientId=u7be5ff65-fd52-4&from=paste&height=381&id=ua1e6055b&originHeight=343&originWidth=938&originalType=binary&ratio=1&rotation=0&showTitle=false&size=106315&status=done&style=none&taskId=ud409e366-f25b-499a-8cb3-2d6f9954e59&title=&width=1042.222249831683)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669020240602-493c3bfb-adc5-4f6f-99bc-59f2eb102aa2.png#averageHue=%230a0a0a&clientId=u7be5ff65-fd52-4&from=paste&height=322&id=u54535e8d&originHeight=290&originWidth=1279&originalType=binary&ratio=1&rotation=0&showTitle=false&size=137679&status=done&style=none&taskId=u52d3524f-76ee-41c8-b248-5b8402b55c9&title=&width=1421.1111487577)<br />channelBox不需要设置为True，因为设置keyable为True就完全不需要设置channelBox为True了。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669020628591-1294d6b3-d1fe-4fc4-96f4-095d47712df7.png#averageHue=%230e0e0e&clientId=u7be5ff65-fd52-4&from=paste&height=228&id=uff0e5a0f&originHeight=205&originWidth=980&originalType=binary&ratio=1&rotation=0&showTitle=false&size=73712&status=done&style=none&taskId=ub7b18945-e62f-4627-82b3-29888a0c6ca&title=&width=1088.8889177345943)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669020736102-fee13889-7dbd-452a-be70-796b0c54f0f1.png#averageHue=%23090909&clientId=u7be5ff65-fd52-4&from=paste&height=346&id=u93dfa081&originHeight=311&originWidth=627&originalType=binary&ratio=1&rotation=0&showTitle=false&size=60795&status=done&style=none&taskId=u9c9b59e9-d647-4c5d-8282-17dfe382f18&title=&width=696.6666851220313)
<a name="bj2ZA"></a>
### 举例：自定义一个车轮节点
<a name="TMm86"></a>
#### 数学原理：
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669176071940-be455bbf-e9bb-4cfb-8c7d-e0ade10a5a1a.png#averageHue=%23030303&clientId=ua5409086-db96-4&from=paste&height=879&id=u646b328b&originHeight=791&originWidth=2353&originalType=binary&ratio=1&rotation=0&showTitle=false&size=184127&status=done&style=none&taskId=uaf267bee-530f-4f2d-b5a5-482826ee31f&title=&width=2614.444513703572)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669275903674-f01c8af3-35a6-4b12-b856-5fd11fafd372.png#averageHue=%233f3e3d&clientId=uab71ef87-eb1c-4&from=paste&height=450&id=uf1f8a322&originHeight=405&originWidth=316&originalType=binary&ratio=1&rotation=0&showTitle=false&size=31129&status=done&style=none&taskId=uc7d49f3b-b9ed-4391-a948-f9f64c62a59&title=&width=351.11112041237936)
<a name="DuEqW"></a>
#### 代码
```python
# coding: utf-8
import maya.api.OpenMaya as om
import maya.cmds as cmds

def maya_useNewAPI():
    """ 这个函数告诉了maya这个插件生成,并且生成的对象使用maya python api 2.0 """
    pass

class RollingNode(om.MPxNode):
    TYPE_NAME = "rollingnode"
    TYPE_ID = om.MTypeId(0x0007F7F9)
    # 提前声明节点的属性
    distance_obj = None
    radius_obj = None
    rotation_obj = None

    def __init__(self):
        super(RollingNode, self).__init__()

    def compute(self, plug, data):
        """_summary_

        Args:
            plug (_type_): 当plug是dirty状态时,会传过来,要求更新
            data (_type_): data提供了读取和写入节点属性值的方法
        """
        if plug == RollingNode.rotation_obj:

            distance = data.inputValue(RollingNode.distance_obj).asDouble()
            radius = data.inputValue(RollingNode.radius_obj).asDouble()
            if radius==0:
                rotation = 0
            else:
                rotation = distance / radius

            rotation_data_handle = data.outputValue(RollingNode.rotation_obj)
            rotation_data_handle.setDouble(rotation)

            data.setClean(plug)

    @classmethod
    def creator(cls):
        return RollingNode()
    
    @classmethod
    def initialize(cls):
        numeric_attr = om.MFnNumericAttribute() # 创建一个针对数字属性的函数集

        cls.distance_obj = numeric_attr.create("distance", "dis", om.MFnNumericData.kDouble, 0.0)  # 属性长名，属性短名，属性数字类型，属性初始值
        numeric_attr.keyable = True # 设置属性可以key关键帧(这样属性就能出现在channel box中)
        numeric_attr.readable = False  #  设置属性没有输出引脚(其他属性不能读它)

        cls.radius_obj = numeric_attr.create("radius", "rad", om.MFnNumericData.kDouble, 0.0)
        numeric_attr.keyable = True
        numeric_attr.readable = False

        unit_attr = om.MFnUnitAttribute()  # 创建一个针对单位属性的函数集

        cls.rotation_obj = unit_attr.create("rotation", "rot", om.MFnUnitAttribute.kAngle, 0.0)
        
        # unit_attr.writable = False #  设置属性没有输入引脚(其他属性不能直接写入它)
        
        # 添加属性
        cls.addAttribute(cls.distance_obj)
        cls.addAttribute(cls.radius_obj)
        cls.addAttribute(cls.rotation_obj)
        # 设置属性影响
        cls.attributeAffects(cls.distance_obj, cls.rotation_obj)
        cls.attributeAffects(cls.radius_obj, cls.rotation_obj)

def initializePlugin(plugin):
    """
    加载插件时执行此函数
    plugin: MObject用于使用MFnPlugin函数集注册插件
    """
    
    vendor = "RuiChen"
    version = "1.0.0"

    plugin_fn = om.MFnPlugin(plugin, vendor, version)
    try:
        plugin_fn.registerNode(RollingNode.TYPE_NAME,
                               RollingNode.TYPE_ID,
                               RollingNode.creator,
                               RollingNode.initialize,
                               om.MPxNode.kDependNode)
    except:
        om.MGlobal.displayError("Failed to register node: {0}".format(RollingNode.TYPE_NAME))

def uninitializePlugin(plugin):
    """
    取消加载插件时执行此函数
    plugin: MObject用于使用MFnPlugin函数集取消注册插件
    """    
    plugin_fn = om.MFnPlugin(plugin)
    try:
        plugin_fn.deregisterNode(RollingNode.TYPE_ID)
    except:
        om.MGlobal.displayError("Failed to deregister node: {0}".format(RollingNode.TYPE_NAME))

if __name__ == "__main__":
    """
    测试时使用
    """

    cmds.file(new=True, force=True)

    plugin_name = "rolling_node.py"

    cmds.evalDeferred('if cmds.pluginInfo("{0}", q=True, loaded=True): cmds.unloadPlugin("{0}")'.format(plugin_name)) # 取消加载插件
    cmds.evalDeferred('if not cmds.pluginInfo("{0}", q=True, loaded=True): cmds.loadPlugin("{0}")'.format(plugin_name))  # 加载插件
    
    cmds.evalDeferred('cmds.createNode("rollingnode")')

    #cmds.evalDeferred(cmds.file("D:/ZhangRuiChen/zrctest/test.ma",o=True,f=True))
```
<a name="nd1Lv"></a>
## 自定义命令
<a name="f37a4"></a>
### 需要的函数
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669276191832-65919398-6691-44ce-bbfc-b786f0d57db8.png#averageHue=%230e0e0e&clientId=uab71ef87-eb1c-4&from=paste&height=522&id=ua468bd22&originHeight=470&originWidth=1569&originalType=binary&ratio=1&rotation=0&showTitle=false&size=281820&status=done&style=none&taskId=u6a8fe328-ef18-45f7-aeb7-d103140d049&title=&width=1743.3333795158965)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669276232949-4b119564-f25d-4d0d-a359-cee351324e5f.png#averageHue=%230e0d0c&clientId=uab71ef87-eb1c-4&from=paste&height=492&id=oSROO&originHeight=443&originWidth=965&originalType=binary&ratio=1&rotation=0&showTitle=false&size=56721&status=done&style=none&taskId=u451750ca-16d5-4f92-8197-4855bb2330b&title=&width=1072.2222506264118)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669276363671-fac83a4e-d68e-4f5b-9a03-88eaec3c83c5.png#averageHue=%23060606&clientId=uab71ef87-eb1c-4&from=paste&height=581&id=u9aa85282&originHeight=523&originWidth=1568&originalType=binary&ratio=1&rotation=0&showTitle=false&size=192253&status=done&style=none&taskId=u64c636cd-f138-4976-9314-505ae075449&title=&width=1742.222268375351)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669278221295-f94858a1-b33c-4aea-943b-48dcaa816caf.png#averageHue=%23080706&clientId=uab71ef87-eb1c-4&from=paste&height=458&id=u42255ea5&originHeight=412&originWidth=895&originalType=binary&ratio=1&rotation=0&showTitle=false&size=42139&status=done&style=none&taskId=uab215eb9-62a5-458e-a642-87b020a1b1d&title=&width=994.4444707882265)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669276507022-eaf4aa20-a034-4950-b8ec-8c17a566c63c.png#averageHue=%23080808&clientId=uab71ef87-eb1c-4&from=paste&height=712&id=u820ea853&originHeight=641&originWidth=1506&originalType=binary&ratio=1&rotation=0&showTitle=false&size=258176&status=done&style=none&taskId=uc5112f50-bb7c-450e-b1d5-f222042dc58&title=&width=1673.3333776615295)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669276519908-13c30975-8158-4102-94ea-aae068fd6ca4.png#averageHue=%23070605&clientId=uab71ef87-eb1c-4&from=paste&height=608&id=uf6f553ea&originHeight=547&originWidth=891&originalType=binary&ratio=1&rotation=0&showTitle=false&size=51499&status=done&style=none&taskId=u582aa433-4a9c-4ff8-89d1-9de5356c257&title=&width=990.0000262260444)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669277248587-3065461c-a73a-4930-9f36-5527e8510456.png#averageHue=%23080808&clientId=uab71ef87-eb1c-4&from=paste&height=367&id=MZ5PS&originHeight=330&originWidth=1566&originalType=binary&ratio=1&rotation=0&showTitle=false&size=142467&status=done&style=none&taskId=u11da2dc7-0fe7-4350-8c2a-bf63bf32d74&title=&width=1740.00004609426)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669277259591-72c884bb-e983-4357-a732-04d7c378bbe4.png#averageHue=%23080706&clientId=uab71ef87-eb1c-4&from=paste&height=317&id=ej8Ow&originHeight=285&originWidth=1040&originalType=binary&ratio=1&rotation=0&showTitle=false&size=32132&status=done&style=none&taskId=u922a51ff-fc9f-4906-a0ae-f4379cef6e8&title=&width=1155.5555861673245)
<a name="GiOc2"></a>
### 堆栈
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669277069508-5854ed27-7f25-4813-9f30-20d89614b42f.png#averageHue=%230a0a0a&clientId=uab71ef87-eb1c-4&from=paste&height=540&id=u2b02ebda&originHeight=486&originWidth=1517&originalType=binary&ratio=1&rotation=0&showTitle=false&size=196983&status=done&style=none&taskId=u866b468d-4173-4666-ac88-9a7b163e4b5&title=&width=1685.5556002075302)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669277119960-0391684d-d8a7-4501-a7e9-f558d591621a.png#averageHue=%23090807&clientId=uab71ef87-eb1c-4&from=paste&height=363&id=u17b6ca56&originHeight=327&originWidth=1425&originalType=binary&ratio=1&rotation=0&showTitle=false&size=40443&status=done&style=none&taskId=u78f7c831-2ff9-4576-b00d-9ff9d96ffa2&title=&width=1583.3333752773437)
<a name="J5Af1"></a>
### 举例：
创建一个命令，这个命令用来设置选择的一个物体的位置
```python
# coding: utf-8
import maya.api.OpenMaya as om
import maya.cmds as cmds


def maya_useNewAPI():
    """ 告知maya,使用的是maya api 2.0 """
    pass


class SimpleCmd(om.MPxCommand):
    COMMAND_NAME = "SimpleCmd"
    # 定义命令的标志
    TRANSLATE_FLAG = ["-t", "-translate", (om.MSyntax.kDouble,om.MSyntax.kDouble,om.MSyntax.kDouble)]
    VERSION_FLAG = ["-v", "-version"]

    def __init__(self):
        super(SimpleCmd, self).__init__()

        self.undoable = False  # 初始设置命令不能撤回

    def doIt(self, arg_list):
        """ 
        doIt 通常用来进行执行redoIt的初始设置以及检查
        doIt 在使用命令时只调用一次
        """

        try:
            arg_db = om.MArgDatabase(self.syntax(), arg_list) # 创建对象解析语法与参数
        except:
            self.displayError("Error parsing arguments")
            raise
        
        selection_list = arg_db.getObjectList()

        self.selected_obj = selection_list.getDependNode(0)
        # om.MFn为所有API类型提供常量的静态类
        # om.MSpace 提供坐标空间常量的静态类。
        if self.selected_obj.apiType() != om.MFn.kTransform:
            raise RuntimeError("This command requires a transform node")
        
        self.edit = arg_db.isEdit
        self.query = arg_db.isQuery

        self.translate = arg_db.isFlagSet(SimpleCmd.TRANSLATE_FLAG[0]) # 判断语法中是否有这个flag
        if self.translate:
            transform_fn = om.MFnTransform(self.selected_obj)
            self.orig_translation = transform_fn.translation(om.MSpace.kTransform)  

            if self.edit:
                self.new_translation = [arg_db.flagArgumentDouble(SimpleCmd.TRANSLATE_FLAG[0],0),
                                        arg_db.flagArgumentDouble(SimpleCmd.TRANSLATE_FLAG[0],1),
                                        arg_db.flagArgumentDouble(SimpleCmd.TRANSLATE_FLAG[0],2)]
                self.undoable = True

        self.version = arg_db.isFlagSet(SimpleCmd.VERSION_FLAG[0])

        self.redoIt()

    def undoIt(self):
        transform_fn = om.MFnTransform(self.selected_obj)
        transform_fn.setTranslation(om.MVector(self.orig_translation),om.MSpace.kTransform)

    def redoIt(self):
        transform_fn = om.MFnTransform(self.selected_obj)

        if self.query:
            if self.translate:
                self.setResult(self.orig_translation)
            else:
                raise RuntimeError("Flag does not support query")
        
        elif self.edit:
            if self.translate:
                transform_fn.setTranslation(om.MVector(self.new_translation),om.MSpace.kTransform)
            else:
                raise RuntimeError("Flag does not support edit")
        
        elif self.version:
            self.setResult("1.0.0")
        else:
            self.setResult(transform_fn.name())

    def isUndoable(self):
        return self.undoable

    @classmethod
    def creator(cls):
        """ 注册maya命令时使用的方法，用来得到类的实例 """
        return SimpleCmd()

    @classmethod
    def create_syntax(cls):

        syntax = om.MSyntax()

        syntax.enableEdit = True
        syntax.enableQuery = True

        syntax.addFlag(*cls.TRANSLATE_FLAG) # 这里*的意思是解包，相当于将列表的中括号去掉
        syntax.addFlag(*cls.VERSION_FLAG)

        # 设置要传递给命令的对象的类型和数量
        syntax.setObjectType(om.MSyntax.kSelectionList, 1, 1) 
        # 如果设置为True，那么当命令行上没有提供对象时，Maya将传递当前选择。默认为False。
        syntax.useSelectionAsDefault(True)

        return syntax


def initializePlugin(plugin):
    """ 插件加载时执行这个函数"""
    vendor = "RuiChen"  # 插件制作人的名字
    version = "1.0.0"  # 插件的版本

    plugin_fn = om.MFnPlugin(plugin, vendor, version)  # 定义插件

    try:
        # 向maya注册一个新命令,第一个参数是命令的名字，第二个参数是类的实例, 第三个参数是命令的语法
        plugin_fn.registerCommand(SimpleCmd.COMMAND_NAME, SimpleCmd.creator, SimpleCmd.create_syntax)
    except:
        om.MGlobal.displayError("Failed to register command: {0}".format(SimpleCmd.COMMAND_NAME))  # 注册失败时输出


def uninitializePlugin(plugin):
    """ 插件取消加载时执行这个函数 """
    plugin_fn = om.MFnPlugin(plugin)
    try:
        plugin_fn.deregisterCommand(SimpleCmd.COMMAND_NAME)  # 取消注册新命令
    except:
        om.MGlobal.displayError("Failed to deregister command: {0}".format(SimpleCmd.COMMAND_NAME))  # 取消注册失败时输出


if __name__ == '__main__':
    cmds.file(new=True, force=True)

    plugin_name = "simple_cmd.py"  # 插件的文件名
    # 如果插件加载了就先取消加载插件
    cmds.evalDeferred(
        'if cmds.pluginInfo("{0}", q=True, loaded=True): cmds.unloadPlugin("{0}")'.format(plugin_name))
    # 如果插件没有加载就加载插件
    cmds.evalDeferred(
        'if not cmds.pluginInfo("{0}", q=True, loaded=True): cmds.loadPlugin("{0}")'.format(plugin_name))

    cmds.evalDeferred('cmds.polyCube()')
```

<a name="R6LW8"></a>
# 第二卷
<a name="alXzd"></a>
## 变形器
<a name="N6AYF"></a>
### 变形器的介绍
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669355834333-997f0cfd-4fd2-4e73-bd1c-268e45820c36.png#averageHue=%230a0a0a&clientId=u5f664d41-9059-4&from=paste&height=758&id=uab4bc6b9&originHeight=682&originWidth=1588&originalType=binary&ratio=1&rotation=0&showTitle=false&size=274633&status=done&style=none&taskId=ua74619f1-ec8a-4eaa-8110-9a3b7e20e55&title=&width=1764.4444911862608)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669355868141-c9c2dee3-b484-44bf-8984-361fdbba321a.png#averageHue=%23070606&clientId=u5f664d41-9059-4&from=paste&height=428&id=ue3d09ce8&originHeight=385&originWidth=1554&originalType=binary&ratio=1&rotation=0&showTitle=false&size=39023&status=done&style=none&taskId=ua7fbf361-57ec-4ce9-a4c2-5fbaa8bf153&title=&width=1726.6667124077137)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669355993057-27a8882a-9859-48e7-9188-f17fc91a795e.png#averageHue=%23131110&clientId=u5f664d41-9059-4&from=paste&height=108&id=u3c57da12&originHeight=97&originWidth=961&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9633&status=done&style=none&taskId=udaa97a37-5c2a-44da-9674-14cf2cfa0a0&title=&width=1067.7778060642297)
<a name="iE55s"></a>
### MPxDeformerNode
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669356025407-d53cd6b6-cbdb-4fcb-b805-7cde5540ac42.png#averageHue=%230d0d0d&clientId=u5f664d41-9059-4&from=paste&height=642&id=u12951ebb&originHeight=578&originWidth=1550&originalType=binary&ratio=1&rotation=0&showTitle=false&size=288740&status=done&style=none&taskId=ud226216a-3c77-4f3b-a01a-eb27fb1868a&title=&width=1722.2222678455319)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669356050081-1d8d4016-947b-4c8b-8ee7-3a43518a50e2.png#averageHue=%23080706&clientId=u5f664d41-9059-4&from=paste&height=410&id=oaJRJ&originHeight=369&originWidth=1419&originalType=binary&ratio=1&rotation=0&showTitle=false&size=40168&status=done&style=none&taskId=ubb6dc37b-0067-4213-b570-9fedf41763e&title=&width=1576.6667084340706)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669356550372-1e916526-0fe3-4a99-b450-007141338fc0.png#averageHue=%230b0b0b&clientId=u5f664d41-9059-4&from=paste&height=553&id=u690eee88&originHeight=498&originWidth=1517&originalType=binary&ratio=1&rotation=0&showTitle=false&size=241699&status=done&style=none&taskId=u526e405c-7ee6-4763-8500-dbb1b88be8a&title=&width=1685.5556002075302)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669356634899-5dae2046-df65-429d-8805-ee447cfa25f5.png#averageHue=%230c0b0a&clientId=u5f664d41-9059-4&from=paste&height=373&id=ufaf9dabb&originHeight=336&originWidth=1092&originalType=binary&ratio=1&rotation=0&showTitle=false&size=31029&status=done&style=none&taskId=uda7bd747-a134-4d48-9472-b734da07645&title=&width=1213.3333654756907)<br />deform方法是由compute方法自动调用的
<a name="d052s"></a>
### MPxDeformerNode Attributes
MPxDeformerNode 自带的属性:<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669357128617-3053f189-10f7-4efc-90c7-36e5861d26fa.png#averageHue=%230b0b0b&clientId=u5f664d41-9059-4&from=paste&height=596&id=u242d61b4&originHeight=536&originWidth=1403&originalType=binary&ratio=1&rotation=0&showTitle=false&size=184275&status=done&style=none&taskId=u07543215-b9eb-480e-b6f8-dac44166d44&title=&width=1558.8889301853426)
<a name="GBDH8"></a>
### 提醒
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669357196384-b048f1b1-8fa0-449b-ad53-429b20da40e0.png#averageHue=%230d0d0d&clientId=u5f664d41-9059-4&from=paste&height=347&id=u7f7dfbd9&originHeight=312&originWidth=1471&originalType=binary&ratio=1&rotation=0&showTitle=false&size=186140&status=done&style=none&taskId=u50f233d0-1224-441d-83cd-f3d14e582f9&title=&width=1634.4444877424369)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669357212850-8737f12b-dac4-40f2-b8b1-90288f0f14f1.png#averageHue=%230f0d0c&clientId=u5f664d41-9059-4&from=paste&height=312&id=u1fbdea20&originHeight=281&originWidth=939&originalType=binary&ratio=1&rotation=0&showTitle=false&size=37218&status=done&style=none&taskId=u7b0303b6-7335-4ecb-8665-f04bd4fce06&title=&width=1043.3333609722285)
<a name="oqCbJ"></a>
### 创建变形器节点的三个举例
<a name="Z2V6L"></a>
#### basicdeformernode
创建一个名字叫basicdeformernode的变形器（遍历顶点，每隔一个顶点，改变顶点的位置）<br />然后可以通过cmds.deformer(typ="basicdeformernode")为选择的物体添加变形节点<br />变形使用的函数：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669601246904-9401a1e9-a3b4-49c8-8e47-581c3165cbfb.png#averageHue=%23ffffff&clientId=u62d82c1e-27cd-4&from=paste&height=441&id=u259ef204&originHeight=397&originWidth=572&originalType=binary&ratio=1&rotation=0&showTitle=false&size=25233&status=done&style=none&taskId=uf6e5ff20-e0c1-4fb5-9c36-f9c27b99539&title=&width=635.5555723920285)
```python
# coding: utf-8
import maya.OpenMaya as om
import maya.OpenMayaMPx as ommpx
import maya.cmds as cmds

class BasicDeformerNode(ommpx.MPxDeformerNode):

    TYPE_NAME = "basicdeformernode"
    TYPE_ID = om.MTypeId(0x0007F7FC)

    def __init__(self):
        super(BasicDeformerNode, self).__init__()

    def deform(self, data_block, geo_iter, matrix, multi_index):
        
        envelope = data_block.inputValue(self.envelope).asFloat() # 总权重

        if envelope == 0:
            return
        
        geo_iter.reset() # 重置迭代器
        while not geo_iter.isDone():

            if geo_iter.index() % 2 == 0:
                pt = geo_iter.position()
                # 局部空间
                # pt.x += (0.2*envelope)

                # 世界空间
                pt = pt * matrix * 0.1

                geo_iter.setPosition(pt)

            geo_iter.next()    
        
    @classmethod
    def creator(cls):
        return BasicDeformerNode()
    
    @classmethod
    def initialize(cls):
        pass

def initializePlugin(plugin):
    """ 插件加载时执行这个函数"""
    vendor = "RuiChen"  # 插件制作人的名字
    version = "1.0.0"  # 插件的版本

    plugin_fn = ommpx.MFnPlugin(plugin, vendor, version)  # 定义插件

    try:
        plugin_fn.registerNode(BasicDeformerNode.TYPE_NAME,
                               BasicDeformerNode.TYPE_ID,
                               BasicDeformerNode.creator,
                               BasicDeformerNode.initialize,
                               ommpx.MPxNode.kDeformerNode)
    except:
        om.MGlobal.displayError("Failed to register node: {0}".format(BasicDeformerNode.TYPE_NAME))

def uninitializePlugin(plugin):
    """ 插件取消加载时执行这个函数"""
    plugin_fn = ommpx.MFnPlugin(plugin)
    try:
        plugin_fn.deregisterNode(BasicDeformerNode.TYPE_ID)
    except:
        om.MGlobal.displayError("Failed to deregister node: {0}".format(BasicDeformerNode.TYPE_NAME))

if __name__ == '__main__':
    cmds.file(new=True,f=True)
    plugin_name = "basic_deformer_node.py"  # 插件的文件名
    # 如果插件加载了就先取消加载插件
    cmds.evalDeferred(
        'if cmds.pluginInfo("{0}", q=True, loaded=True): cmds.unloadPlugin("{0}")'.format(plugin_name))
    # 如果插件没有加载就加载插件
    cmds.evalDeferred(
        'if not cmds.pluginInfo("{0}", q=True, loaded=True): cmds.loadPlugin("{0}")'.format(plugin_name))
    cmds.evalDeferred('cmds.file("C:/Users/Adiministrator/Destop/test.ma",o=True,f=True)')
    cmds.evalDeferred('cmds.select("nurbsPlane1"); cmds.deformer(typ="basicdeformernode")')
```

<a name="AfQbY"></a>
#### blenddeformernode
```python
# coding: utf-8
import maya.OpenMaya as om
import maya.OpenMayaMPx as ommpx
import maya.cmds as cmds

class BlendDeformerNode(ommpx.MPxDeformerNode):

    TYPE_NAME = "blenddeformernode"
    TYPE_ID = om.MTypeId(0x0007F7FD)

    def __init__(self):
        super(BlendDeformerNode, self).__init__()

    def deform(self, data_block, geo_iter, matrix, multi_index):
        """
            变形的逻辑
        Args:
            data_block (_type_): 数据块
            geo_iter (_type_): 针对geometry的顶点迭代器
            matrix (_type_): 世界空间的矩阵
            multi_index (_type_): _description_
        """
        # envelope是MPxDeformerNode类自带的属性
        envelope = data_block.inputValue(self.envelope).asFloat() # 获取控制整体权重值的值
        if envelope == 0:
            return    

        blend_weight = data_block.inputValue(self.blend_weight).asFloat() # 获取混合的权重值
        if blend_weight == 0:
            return

        target_mesh = data_block.inputValue(self.blend_mesh).asMesh()  # 获取目标mesh
        if target_mesh.isNull():
            return

        target_points = om.MPointArray() # 定义一个接受目标mesh所有点的数组

        target_mesh_fn = om.MFnMesh(target_mesh) # 定义一个目标mesh的函数集
        target_mesh_fn.getPoints(target_points) # 使用函数集的方法将点放入到点数组中

        global_weight = blend_weight * envelope  # 得到总的权重值

        geo_iter.reset() # 重置迭代器
        while not geo_iter.isDone():
            
            source_pt = geo_iter.position()
            target_pt = target_points[geo_iter.index()]

            source_weight = self.weightValue(data_block, multi_index, geo_iter.index()) # 获取绘制的权重值

            final_pt = source_pt + ((target_pt - source_pt) * global_weight * source_weight)


            geo_iter.setPosition(final_pt)
            
            geo_iter.next()    
        
    @classmethod
    def creator(cls):
        return BlendDeformerNode()
    
    @classmethod
    def initialize(cls):
        
        typed_attr = om.MFnTypedAttribute()
        cls.blend_mesh = typed_attr.create("blendMesh", "bMesh", om.MFnData.kMesh)

        numeric_attr = om.MFnNumericAttribute()
        cls.blend_weight = numeric_attr.create("blendWeight", "bWeight", om.MFnNumericData.kFloat, 0.0)
        numeric_attr.setKeyable(True)
        numeric_attr.setMin(0.0)
        numeric_attr.setMax(1.0)

        cls.addAttribute(cls.blend_mesh)
        cls.addAttribute(cls.blend_weight)

        #变形器节点具有默认的outputGeom属性，因此我们没必要再创建一个输出的属性，我们可以直接利用这个默认的outputGemo属性
        output_geom = ommpx.cvar.MPxGeometryFilter_outputGeom  

        cls.attributeAffects(cls.blend_mesh, output_geom)
        cls.attributeAffects(cls.blend_weight,output_geom)

def initializePlugin(plugin):
    """ 插件加载时执行这个函数"""
    vendor = "RuiChen"  # 插件制作人的名字
    version = "1.0.0"  # 插件的版本

    plugin_fn = ommpx.MFnPlugin(plugin, vendor, version)  # 定义插件

    try:
        plugin_fn.registerNode(BlendDeformerNode.TYPE_NAME,
                               BlendDeformerNode.TYPE_ID,
                               BlendDeformerNode.creator,
                               BlendDeformerNode.initialize,
                               ommpx.MPxNode.kDeformerNode)
    except:
        om.MGlobal.displayError("Failed to register node: {0}".format(BlendDeformerNode.TYPE_NAME))
    
    cmds.makePaintable(BlendDeformerNode.TYPE_NAME, "weights", attrType="multiFloat", shapeMode = "deformer") # 使其能绘制权重

def uninitializePlugin(plugin):
    """ 插件取消加载时执行这个函数"""
    cmds.makePaintable(BlendDeformerNode.TYPE_NAME, "weights",remove=True) # 移除使其能绘制权重
    plugin_fn = ommpx.MFnPlugin(plugin)
    try:
        plugin_fn.deregisterNode(BlendDeformerNode.TYPE_ID)
    except:
        om.MGlobal.displayError("Failed to deregister node: {0}".format(BlendDeformerNode.TYPE_NAME))
    
if __name__ == '__main__':
    cmds.file(new=True,f=True)
    plugin_name = "blend_deformer_node.py"  # 插件的文件名
    # 如果插件加载了就先取消加载插件
    cmds.evalDeferred(
        'if cmds.pluginInfo("{0}", q=True, loaded=True): cmds.unloadPlugin("{0}")'.format(plugin_name))
    # 如果插件没有加载就加载插件
    cmds.evalDeferred(
        'if not cmds.pluginInfo("{0}", q=True, loaded=True): cmds.loadPlugin("{0}")'.format(plugin_name))
    cmds.evalDeferred('cmds.file("D:/ZhangRuiChen/zrctest/blend_test.ma",o=True,f=True)')
    cmds.evalDeferred('cmds.select("sourceSphere"); cmds.deformer(typ="blenddeformernode")')
    cmds.evalDeferred('cmds.connectAttr("deformerTargetShape.outMesh", "blenddeformernode1.blendMesh", force=True)')

```
<a name="WKWiJ"></a>
#### attractordeformernode
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669885141889-8034d785-9229-4f17-b298-f544e314d66c.png#averageHue=%236c6c6c&clientId=uc34e0430-0983-4&from=paste&height=526&id=ubc0d0e8f&originHeight=473&originWidth=310&originalType=binary&ratio=1&rotation=0&showTitle=false&size=29030&status=done&style=none&taskId=uae417cc9-9c77-4b0c-a221-7143d9e847d&title=&width=344.4444535691064)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669949631088-6257e607-fd16-41e0-9671-0b43342621e1.png#averageHue=%233a3938&clientId=u706cb6cd-4e7a-4&from=paste&height=334&id=u61cce788&originHeight=301&originWidth=983&originalType=binary&ratio=1&rotation=0&showTitle=false&size=44627&status=done&style=none&taskId=ub33502f4-1fd1-4a61-bed4-6f5f6b0764f&title=&width=1092.2222511562309)

```python
# coding: utf-8
import maya.OpenMaya as om
import maya.OpenMayaMPx as ommpx
import maya.cmds as cmds

class AttractorDeformerNode(ommpx.MPxDeformerNode):

    TYPE_NAME = "attractordeformernode"
    TYPE_ID = om.MTypeId(0x0007F7FE)

    MAX_ANGLE = 0.5 * 3.14159265 # 90度

    def __init__(self):
        super(AttractorDeformerNode, self).__init__()

    def deform(self, data_block, geo_iter, world_matrix, multi_index):
        """
            变形的逻辑
        Args:
            data_block (_type_): 数据块
            geo_iter (_type_): 针对geometry的顶点迭代器
            matrix (_type_): 世界空间的矩阵
            multi_index (_type_): geom_index
        """
        # envelope是MPxDeformerNode类自带的属性
        envelope = data_block.inputValue(self.envelope).asFloat() # 获取控制整体权重值的值
        if envelope == 0:
            return    
        
        max_distance = data_block.inputValue(AttractorDeformerNode.max_distance).asFloat()
        if max_distance == 0:
            return

        target_position = data_block.inputValue(AttractorDeformerNode.target_position).asFloatVector()
        target_position = om.MPoint(target_position) * world_matrix.inverse() # 将目标位置转换为局部空间下的数值
        target_position = om.MFloatVector(target_position) # 获取目标位置在局部空间下的floatVector

        input_handle = data_block.outputArrayValue(self.input) # 使用outputArray代替inputArray以避免重新计算（外网翻译）
        input_handle.jumpToElement(multi_index)
        input_element_handle = input_handle.outputValue()

        input_geom = input_element_handle.child(self.inputGeom).asMesh()
        mesh_fn = om.MFnMesh(input_geom)

        normals = om.MFloatVectorArray()  # 用来存取inputgeom的顶点的所有浮点法线
        mesh_fn.getVertexNormals(False, normals) # False的作用是不要average normal


        geo_iter.reset()
        while not geo_iter.isDone():
            # 顶点迭代器所获取的位置都是在局部空间下的位置
            pt_local = geo_iter.position()

            target_vector = target_position - om.MFloatVector(pt_local)

            distance = target_vector.length()

            if distance <= max_distance:

                normal = normals[geo_iter.index()] # 局部空间下的顶点的法线浮点向量

                angle = normal.angle(target_vector)  # 顶点的法线与顶点与目标点的向量之间的角度
                if angle <= AttractorDeformerNode.MAX_ANGLE:

                    offset = target_vector * ((max_distance-distance)/max_distance)

                    new_pt_local = pt_local + om.MVector(offset)  # 局部空间下的新顶点位置

                    geo_iter.setPosition(new_pt_local)

            geo_iter.next()

    def accessoryAttribute(self):
        """ 返回要辅助修改的属性 """
        return AttractorDeformerNode.target_position
    
    def accessoryNodeSetup(self, dag_modifier):
        """ dag_modifier用于执行节点创建和连接操作 """
        locator = dag_modifier.createNode("locator")

        locator_fn = om.MFnDependencyNode(locator)
        locator_translate_plug = locator_fn.findPlug("translate", False) # False意思是不需要networkplug，networkplug意思是在DG中建立连接的属性

        target_position_plug = om.MPlug(self.thisMObject(), AttractorDeformerNode.target_position)  # 获取变形器的target_position的plug
        dag_modifier.connect(locator_translate_plug, target_position_plug)

        # 将定位器得位置设置在output_geom的位置
        # 这里的output_geom指的是shape节点
        # parent指的是transform节点，因为只有transform节点才有xyz坐标
        output_geom_plug = om.MPlug(self.thisMObject(), self.outputGeom)
        mPlugArray2 = om.MPlugArray()
        output_geom_plug[0].connectedTo(mPlugArray2,False,True)
        output_geom_obj = mPlugArray2[0].node()
        output_geom_fn = om.MFnDagNode(output_geom_obj)
        parent_obj = output_geom_fn.parent(0)
        parent_fn = om.MFnDependencyNode(parent_obj)
        parent_translate_plug = parent_fn.findPlug("translate",False)
        parent_translate_x_handle = parent_translate_plug.child(0).asFloat()
        parent_translate_y_handle = parent_translate_plug.child(1).asFloat()
        parent_translate_z_handle = parent_translate_plug.child(2).asFloat()
    
        locator_translate_plug.child(0).setFloat(parent_translate_x_handle)
        locator_translate_plug.child(1).setFloat(parent_translate_y_handle)
        locator_translate_plug.child(2).setFloat(parent_translate_z_handle)

        

        
        
    @classmethod
    def creator(cls):
        return AttractorDeformerNode()
    
    @classmethod
    def initialize(cls):
        
        numeric_attr = om.MFnNumericAttribute()
        cls.max_distance = numeric_attr.create("maximumDistance", "maxDist", om.MFnNumericData.kFloat, 1.0)
        numeric_attr.setKeyable(True)
        numeric_attr.setMin(0.0)
        numeric_attr.setMax(2.0)

        cls.target_position = numeric_attr.createPoint("targetPosition", "targetPos")
        numeric_attr.setKeyable(True)

        cls.addAttribute(cls.max_distance)
        cls.addAttribute(cls.target_position)

        #变形器节点具有默认的outputGeom属性，因此我们没必要再创建一个输出的属性，我们可以直接利用这个默认的outputGemo属性
        output_geom = ommpx.cvar.MPxGeometryFilter_outputGeom  

        cls.attributeAffects(cls.max_distance, output_geom)
        cls.attributeAffects(cls.target_position,output_geom)

def initializePlugin(plugin):
    """ 插件加载时执行这个函数"""
    vendor = "RuiChen"  # 插件制作人的名字
    version = "1.0.0"  # 插件的版本

    plugin_fn = ommpx.MFnPlugin(plugin, vendor, version)  # 定义插件

    try:
        plugin_fn.registerNode(AttractorDeformerNode.TYPE_NAME,
                               AttractorDeformerNode.TYPE_ID,
                               AttractorDeformerNode.creator,
                               AttractorDeformerNode.initialize,
                               ommpx.MPxNode.kDeformerNode)
    except:
        om.MGlobal.displayError("Failed to register node: {0}".format(AttractorDeformerNode.TYPE_NAME))
    
    cmds.makePaintable(AttractorDeformerNode.TYPE_NAME, "weights", attrType="multiFloat", shapeMode = "deformer") # 使其能绘制权重

def uninitializePlugin(plugin):
    """ 插件取消加载时执行这个函数"""
    cmds.makePaintable(AttractorDeformerNode.TYPE_NAME, "weights",remove=True) # 移除使其能绘制权重
    plugin_fn = ommpx.MFnPlugin(plugin)
    try:
        plugin_fn.deregisterNode(AttractorDeformerNode.TYPE_ID)
    except:
        om.MGlobal.displayError("Failed to deregister node: {0}".format(AttractorDeformerNode.TYPE_NAME))
    
if __name__ == '__main__':
    cmds.file(new=True,f=True)
    plugin_name = "attractor_deformer_node.py"  # 插件的文件名
    # 如果插件加载了就先取消加载插件
    cmds.evalDeferred(
        'if cmds.pluginInfo("{0}", q=True, loaded=True): cmds.unloadPlugin("{0}")'.format(plugin_name))
    # 如果插件没有加载就加载插件
    cmds.evalDeferred(
        'if not cmds.pluginInfo("{0}", q=True, loaded=True): cmds.loadPlugin("{0}")'.format(plugin_name))

    cmds.evalDeferred('cmds.file("D:/ZhangRuiChen/zrctest/attractor_test.ma",o=True,f=True)')
    cmds.evalDeferred('cmds.select("pSphere1"); cmds.deformer(typ="attractordeformernode")')
    #cmds.evalDeferred('cmds.connectAttr("locator1.translate","attractordeformernode1.targetPosition",f=True)')
```
<a name="ChJzT"></a>
## CallBack
<a name="wF8X2"></a>
### CallBack介绍
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669972488001-309540ae-07bb-4005-9919-aa1bcbcd5249.png#averageHue=%23090909&clientId=u706cb6cd-4e7a-4&from=paste&height=607&id=uf36b7ab6&originHeight=546&originWidth=1583&originalType=binary&ratio=1&rotation=0&showTitle=false&size=232144&status=done&style=none&taskId=u09bba1cb-0e33-41f0-acb0-9d7fd113a9e&title=&width=1758.8889354835335)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669972508805-3935a541-c38a-41c7-bff5-a896383060c3.png#averageHue=%23070606&clientId=u706cb6cd-4e7a-4&from=paste&height=451&id=u73d5f3e5&originHeight=406&originWidth=1488&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36769&status=done&style=none&taskId=uc8872394-a571-4aba-9dc3-eed480c8e03&title=&width=1653.3333771317104)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669972555239-dc7a204c-e356-4a26-98cd-78eecc67203a.png#averageHue=%230a0a0a&clientId=u706cb6cd-4e7a-4&from=paste&height=316&id=u54239874&originHeight=284&originWidth=1421&originalType=binary&ratio=1&rotation=0&showTitle=false&size=121474&status=done&style=none&taskId=u2df6defd-ff08-4b87-aa18-24fdac8740e&title=&width=1578.8889307151617)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669972581861-96ac13e4-dc9c-432e-a38c-9fc0e0cb561d.png#averageHue=%230c0b0a&clientId=u706cb6cd-4e7a-4&from=paste&height=289&id=u05ef04b1&originHeight=260&originWidth=773&originalType=binary&ratio=1&rotation=0&showTitle=false&size=24062&status=done&style=none&taskId=u37fb79ad-66a9-4f9c-a91f-07d85da429f&title=&width=858.8889116416749)
<a name="pdr4V"></a>
### CallBack vs ScriptJobs
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669973658033-4c79b1d1-9452-4ef8-a6e6-8c4718c15060.png#averageHue=%23090909&clientId=u706cb6cd-4e7a-4&from=paste&height=322&id=udb20517a&originHeight=290&originWidth=1535&originalType=binary&ratio=1&rotation=0&showTitle=false&size=123374&status=done&style=none&taskId=u72d56818-e005-4259-9bcc-2d2f92de29f&title=&width=1705.5556007373493)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669973698429-03371990-4d28-4a58-a840-c328a893017d.png#averageHue=%230b0a09&clientId=u706cb6cd-4e7a-4&from=paste&height=268&id=u4d182dee&originHeight=241&originWidth=903&originalType=binary&ratio=1&rotation=0&showTitle=false&size=25522&status=done&style=none&taskId=u9eca8eda-559f-496e-8fca-521a2573681&title=&width=1003.3333599125905)
<a name="zUZUZ"></a>
### MMessage
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669974320245-42120466-d32c-4ecf-9172-d2c20ed0e2a0.png#averageHue=%230a0a0a&clientId=u706cb6cd-4e7a-4&from=paste&height=487&id=u0a033b4e&originHeight=438&originWidth=1473&originalType=binary&ratio=1&rotation=0&showTitle=false&size=183961&status=done&style=none&taskId=u2e9e4661-09ea-4df6-8dc8-1b3973d71ac&title=&width=1636.666710023528)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669974341909-a7a9ab9a-696e-4401-a3d7-be2bf57cb093.png#averageHue=%230c0b0a&clientId=u706cb6cd-4e7a-4&from=paste&height=300&id=u78fb9785&originHeight=270&originWidth=1078&originalType=binary&ratio=1&rotation=0&showTitle=false&size=26516&status=done&style=none&taskId=u43a6d480-5105-4ad5-9240-28951bb8ef4&title=&width=1197.7778095080537)<br />详情：[https://help.autodesk.com/view/MAYAUL/2018/ENU/?guid=__py_ref_class_open_maya_1_1_m_message_html](https://help.autodesk.com/view/MAYAUL/2018/ENU/?guid=__py_ref_class_open_maya_1_1_m_message_html)<br />点击才能展开<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670232926009-a9fd1da3-d7b6-4e73-9bf9-68474c984507.png#averageHue=%23faf6f5&clientId=u042c0c24-ff4e-4&from=paste&height=286&id=ud08fa497&originHeight=257&originWidth=641&originalType=binary&ratio=1&rotation=0&showTitle=false&size=16912&status=done&style=none&taskId=u3e5a6d1b-d291-46be-8ba8-811380b34b6&title=&width=712.2222410896683)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670229085571-d2f1e418-55d9-4202-9e96-d148aafe3e9d.png#averageHue=%23f7f8fb&clientId=u042c0c24-ff4e-4&from=paste&height=1050&id=u24d41402&originHeight=945&originWidth=526&originalType=binary&ratio=1&rotation=0&showTitle=false&size=57798&status=done&style=none&taskId=ua93d13aa-78bc-45ba-95ae-93c0e8cd56a&title=&width=584.4444599269353)<br />MEventMessage：在发生添加的全局事件时执行（例如场景被打开，选择发生变化，事件发生改变）时添加callback<br />MSceneMessage: 场景事件添加callback<br />MTimmerMessage: 在特定的事件间隔内调用一个函数
<a name="cQifq"></a>
### 管理回调函数
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670223085104-a250a1fb-6b2d-41ba-9713-e5c5985ab042.png#averageHue=%230d0d0d&clientId=u042c0c24-ff4e-4&from=paste&height=313&id=ud2c5aefb&originHeight=282&originWidth=1098&originalType=binary&ratio=1&rotation=0&showTitle=false&size=128211&status=done&style=none&taskId=ue9e1910f-2311-4995-8b0f-700b4ea080c&title=&width=1220.0000323189638)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670223097855-5501613c-244e-40a0-b503-020f648889c5.png#averageHue=%230e0d0b&clientId=u042c0c24-ff4e-4&from=paste&height=297&id=u0aace71e&originHeight=267&originWidth=637&originalType=binary&ratio=1&rotation=0&showTitle=false&size=26408&status=done&style=none&taskId=u7b4bc1df-cfdb-4f6e-aa82-d153ca7ae91&title=&width=707.7777965274863)
<a name="IArRy"></a>
### 获取MEventMessage的事件名字
import maya.api.OpenMaya as om<br />om.MEventMessage.getEventNames()<br />其中常用的事件：<br />deleteAll，undoSupressed（撤销后的返回），undo（撤销），timeChanged（时间轴变化）<br />其他事件的解释可以通过scriptjob命令的帮助文档找到:<br />[https://help.autodesk.com/view/MAYAUL/2018/ENU/?guid=__CommandsPython_index_html](https://help.autodesk.com/view/MAYAUL/2018/ENU/?guid=__CommandsPython_index_html)
<a name="Du513"></a>
### 举例：
MEventMessage<br />MSceneMessage<br />MConditionMessage<br />MUiMessage<br />MTimerMessage
```python
# coding: utf-8
import maya.api.OpenMaya as om
import maya.api.OpenMayaAnim as oma
import maya.api.OpenMayaUI as omui
import maya.cmds as cmds

def maya_useNewAPI():
    """ 告知maya,使用的是maya api 2.0 """
    pass

callback_ids = [] # 定义全局变量存放callback_id

def on_new_scene(client_data):
    """ 当新场景加载时调用,client_data为调用这个函数时传递的参数(可以为None) """
    print("New Scene opened")

def on_time_changed(client_data):
    """ 当时间轴发生改变时调用 """
    print("Time changed: {0}".format(oma.MAnimControl.currentTime().asUnits(om.MTime.uiUnit()))) # 输出当前时间轴的帧数

def on_selection_changed(client_data):
    """ 当选择发生改变时调用 """
    print("Selection changed")

def before_import(client_data):
    """ 导入前执行 """
    print("Import pre-processing")

def after_import(client_data):
    """ 导入后执行 """
    print("Import post-processing")

def on_viewport_changed(model_panel,*args):
    """ 在指定的视口面板处切换相机时调用 """
    print("Camera changed in model panel {0}".format(model_panel))

def on_playing_back_state_changed(is_playing, client_data):
    """ 当使用播放键预览拍屏时调用 """
    print("Playing state changed: {0}".format(is_playing))

def on_timer_fired(elapsed_time, previous_execution_time, client_data):
    """ 
    定时器调用此函数,每经过设定的秒数就调用一次这个函数
    Args:
        elapsed_time (float): 设定的秒数
        previous_execution_time (_type_): 以前的运行的时间，为了防止此函数还没执行完就再次被调用
        client_data (_type_): 用户自定义的参数,可以不传递
    """
    print("Timer fired")

def initializePlugin(plugin): 
    """ 插件加载时执行这个函数"""
    global callback_ids # 调用全局变量
    vendor = "RuiChen"  # 插件制作人的名字
    version = "1.0.0"  # 插件的版本
    # 注册回调，参数为事件类型名，回调函数，还有第三个参数可选（传递给回调函数的参数），返回值为回调函数id
    callback_ids.append(om.MEventMessage.addEventCallback("NewSceneOpened", on_new_scene)) 
    callback_ids.append(om.MEventMessage.addEventCallback("timeChanged", on_time_changed))
    callback_ids.append(om.MEventMessage.addEventCallback("SelectionChanged", on_selection_changed))

    callback_ids.append(om.MSceneMessage.addCallback(om.MSceneMessage.kBeforeImport, before_import))
    callback_ids.append(om.MSceneMessage.addCallback(om.MSceneMessage.kAfterImport, after_import))

    callback_ids.append(om.MConditionMessage.addConditionCallback("playingBack", on_playing_back_state_changed))
    
    callback_ids.append(omui.MUiMessage.addCameraChangedCallback("modelPanel4", on_viewport_changed))

    callback_ids.append(om.MTimerMessage.addTimerCallback(2.5, on_timer_fired))

    om.MFnPlugin(plugin, vendor, version)  # 定义插件

def uninitializePlugin(plugin):
    """ 插件取消加载时执行这个函数"""
    global callback_ids
    om.MEventMessage.removeCallbacks(callback_ids)
    callback_ids = []

if __name__ == '__main__':
    """ 注册后,在maya脚本编辑器中的使用方法 """
    plugin_name = "callback_example.py"  # 插件的文件名
    # 如果插件加载了就先取消加载插件
    cmds.evalDeferred('if cmds.pluginInfo("{0}", q=True, loaded=True): cmds.unloadPlugin("{0}")'.format(plugin_name))
    # 如果插件没有加载就加载插件
    cmds.evalDeferred('if not cmds.pluginInfo("{0}", q=True, loaded=True): cmds.loadPlugin("{0}")'.format(plugin_name))

```
<a name="laIwQ"></a>
## 遍历dag
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670292234464-c3d01a0b-ccd6-4ee8-852f-e5389fdf7752.png#averageHue=%23080808&clientId=ud856797a-7bad-4&from=paste&height=459&id=ua4023119&originHeight=413&originWidth=1567&originalType=binary&ratio=1&rotation=0&showTitle=false&size=167105&status=done&style=none&taskId=uce053f01-334d-4e15-8de8-78aa1e79a3e&title=&width=1741.1111572348054)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670292256216-69999efc-8d41-4710-ab15-1a985a9c8152.png#averageHue=%23060605&clientId=ud856797a-7bad-4&from=paste&height=424&id=u89628321&originHeight=382&originWidth=1411&originalType=binary&ratio=1&rotation=0&showTitle=false&size=39794&status=done&style=none&taskId=uc546536e-6fbf-4060-808a-c47acbfc2d3&title=&width=1567.7778193097067)
<a name="cFSBy"></a>
### 什么是dag
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670292398236-03017c4c-8d5f-4f10-b6d0-91592fe0db6b.png#averageHue=%230a0a0a&clientId=ud856797a-7bad-4&from=paste&height=610&id=u0bc3b1bf&originHeight=549&originWidth=1436&originalType=binary&ratio=1&rotation=0&showTitle=false&size=221882&status=done&style=none&taskId=uc50a015a-a103-4472-b546-08929a1fe2c&title=&width=1595.5555978233442)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670292460174-2d433e3c-e8f9-4689-9ec2-571f1fcbd908.png#averageHue=%230e0e0e&clientId=ud856797a-7bad-4&from=paste&height=58&id=uec348313&originHeight=52&originWidth=1490&originalType=binary&ratio=1&rotation=0&showTitle=false&size=42870&status=done&style=none&taskId=ubd55d0a7-b5fe-426b-b234-1d7cd44798d&title=&width=1655.5555994128015)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670292422966-d1c5fd82-cc5b-41cb-b937-675af3cfc63e.png#averageHue=%230b0a0a&clientId=ud856797a-7bad-4&from=paste&height=566&id=u6bf9b251&originHeight=509&originWidth=910&originalType=binary&ratio=1&rotation=0&showTitle=false&size=47642&status=done&style=none&taskId=u319e8271-3a6f-4646-8a16-f5d6cd7fb55&title=&width=1011.111137896409)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670292473901-af9cd6c3-52b3-41bd-9e80-ae83a553ea5b.png#averageHue=%230f0c0a&clientId=ud856797a-7bad-4&from=paste&height=51&id=u7343d157&originHeight=46&originWidth=808&originalType=binary&ratio=1&rotation=0&showTitle=false&size=6927&status=done&style=none&taskId=u30d89d08-9196-49be-965b-c1985fb545f&title=&width=897.7778015607676)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670293619209-ed47aed6-aeb7-43e5-8dbd-1333230b98dc.png#averageHue=%23454545&clientId=ud856797a-7bad-4&from=paste&height=886&id=u65792787&originHeight=797&originWidth=1623&originalType=binary&ratio=1&rotation=0&showTitle=false&size=321869&status=done&style=none&taskId=uc9cf94af-62f9-4940-99b1-c4c33239cc7&title=&width=1803.3333811053535)
<a name="fAnTI"></a>
### DG vs DAG 
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670293830064-e4d086ae-db35-4015-a039-1dcab37c54ac.png#averageHue=%23111111&clientId=ud856797a-7bad-4&from=paste&height=869&id=u1b0787ac&originHeight=782&originWidth=1578&originalType=binary&ratio=1&rotation=0&showTitle=false&size=266546&status=done&style=none&taskId=u8128643d-cd26-48d6-9a51-cc55757311d&title=&width=1753.333379780806)<br />DG:<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670293934734-671f858a-c3d3-4606-b322-07be4b8f1c9f.png#averageHue=%23181614&clientId=ud856797a-7bad-4&from=paste&height=149&id=ucf7299e1&originHeight=134&originWidth=430&originalType=binary&ratio=1&rotation=0&showTitle=false&size=10145&status=done&style=none&taskId=ud7190181-f6e4-41be-b488-d30ed0c2252&title=&width=477.7777904345669)<br />DAG:<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670293952304-026248cd-50f0-4949-951e-a39832dc47e3.png#averageHue=%23130f0c&clientId=ud856797a-7bad-4&from=paste&height=100&id=ue9c857d9&originHeight=90&originWidth=250&originalType=binary&ratio=1&rotation=0&showTitle=false&size=4254&status=done&style=none&taskId=ubcad7d02-6ea2-47b5-b3f5-933558275f6&title=&width=277.7777851363761)
<a name="RT5I8"></a>
### 遍历dag的常用api class
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670293997068-3d94d62f-ce6b-4fad-8699-234e64ee6427.png#averageHue=%230b0b0b&clientId=ud856797a-7bad-4&from=paste&height=492&id=u072129c2&originHeight=443&originWidth=735&originalType=binary&ratio=1&rotation=0&showTitle=false&size=88990&status=done&style=none&taskId=u9be385a2-bef2-46da-aeb5-f318ec6b27c&title=&width=816.6666883009457)
<a name="xZdiD"></a>
### MItDag
[https://help.autodesk.com/view/MAYAUL/2019/CHS/?guid=Maya_SDK_MERGED_cpp_ref_class_m_it_dag_html](https://help.autodesk.com/view/MAYAUL/2019/CHS/?guid=Maya_SDK_MERGED_cpp_ref_class_m_it_dag_html)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670294064469-4920d97b-6f92-41f7-8771-e73e0bd0a24b.png#averageHue=%23090909&clientId=ud856797a-7bad-4&from=paste&height=563&id=uc63fdefe&originHeight=507&originWidth=1585&originalType=binary&ratio=1&rotation=0&showTitle=false&size=190360&status=done&style=none&taskId=u7aee5de1-3dca-4924-9a7c-3f19d2cadfc&title=&width=1761.1111577646245)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670294104355-c1a8787c-e8ce-45ae-a79f-181ac15dbbb6.png#averageHue=%23080707&clientId=ud856797a-7bad-4&from=paste&height=417&id=ub9109e3b&originHeight=375&originWidth=1095&originalType=binary&ratio=1&rotation=0&showTitle=false&size=38847&status=done&style=none&taskId=u378de64f-b571-4dad-b4d4-8f7454d5c9f&title=&width=1216.6666988973273)
<a name="OAENk"></a>
### MFnDagNode
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670294341336-eeaea299-9516-44bb-90b8-7258f819f2f4.png#averageHue=%23080808&clientId=ud856797a-7bad-4&from=paste&height=793&id=u7c73b66b&originHeight=714&originWidth=1566&originalType=binary&ratio=1&rotation=0&showTitle=false&size=238697&status=done&style=none&taskId=u1e08df4c-cfb5-41fc-aa9b-a26535552c0&title=&width=1740.00004609426)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670294373623-54804cd2-b2ee-41d9-a6ee-d750d503ea32.png#averageHue=%23070706&clientId=ud856797a-7bad-4&from=paste&height=408&id=u3504b445&originHeight=367&originWidth=1248&originalType=binary&ratio=1&rotation=0&showTitle=false&size=33475&status=done&style=none&taskId=u06d5765d-56e5-4db6-ae66-63805df8373&title=&width=1386.6667034007894)
<a name="Utj5z"></a>
### MDagPath 和 MDagPathArray
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670294577548-ccb4d943-8d92-4b42-a7cc-80dfcd04dc72.png#averageHue=%230a0a0a&clientId=ud856797a-7bad-4&from=paste&height=674&id=u90f42400&originHeight=607&originWidth=1605&originalType=binary&ratio=1&rotation=0&showTitle=false&size=222042&status=done&style=none&taskId=u4908e162-454a-4240-a318-c2e4648060e&title=&width=1783.3333805755344)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670294597971-19963ec7-1a5e-4e38-a0fa-669fbd475fbe.png#averageHue=%23090808&clientId=ud856797a-7bad-4&from=paste&height=468&id=u4739d8f8&originHeight=421&originWidth=1069&originalType=binary&ratio=1&rotation=0&showTitle=false&size=37094&status=done&style=none&taskId=u17d10d7a-1de6-423b-b8c0-24bb9f4b714&title=&width=1187.7778092431442)
<a name="UO1pS"></a>
### 代码举例
```python
# coding:utf-8
import maya.api.OpenMaya as om
selection_list = om.MGlobal.getActiveSelectionList()  # 获取当前选择的对象并为其创建列表
traversal_type = om.MItDag.kBreadthFirst # 遍历方式为广度优先（默认是深度优先）
filter_type = om.MFn.kMesh # 过滤器设置，只遍历kMesh类型
dag_iter = om.MItDag(traversal_type,filter_type) # 创建迭代器，并指定遍历方式和遍历类型

if not selection_list.isEmpty():
    
    dag_fn = om.MFnDagNode(selection_list.getDependNode(0))

    #print("Child:")
    for i in range(dag_fn.childCount()):
        child_obj = dag_fn.child(i)
        child_fn = om.MFnDagNode(child_obj)
        #print(child_fn.fullPathName())

    #print("Parent:")
    for i in range(dag_fn.parentCount()):
        parent_obj = dag_fn.parent(i)
        parent_fn = om.MFnDagNode(parent_obj)
        #print(parent_fn.fullPathName())

    # 如果场景中有选择的物体，那么就以选择的物体为迭代起始点
    dag_iter.reset(selection_list.getDependNode(0),traversal_type,filter_type) 
    while not dag_iter.isDone():
        # print(dag_iter.partialPathName()) # 输出短名
        # print(dag_iter.fullPathName()) # 输出长名
        # dag_path = dag_iter.getPath() # 获取dagpath对象
        # print(dag_path.fullPathName()) # 输出dagpath对象的长名

        # 迭代器遍历类型为kmesh，然后通过类型为kmesh的shape节点得到父节点transform的名字
        shape_obj = dag_iter.currentItem()
        dag_fn = om.MFnDagNode(shape_obj)
        dag_fn = om.MFnDagNode(shape_obj)
        for i in range(dag_fn.parentCount()):
            parent_fn = om.MFnDagNode(dag_fn.parent(i))
            print(parent_fn.fullPathName())

        dag_iter.next()
```

<a name="PhLMD"></a>
## contexts（工具，以下所有的上下文的翻译统统理解为工具）
<a name="dRb2V"></a>
### 什么是contexts
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670314380302-2759dcb4-96c9-4b21-9356-2d53238597ff.png#averageHue=%230b0b0b&clientId=u7f1d3d8f-5941-4&from=paste&height=644&id=u323f8700&originHeight=580&originWidth=1516&originalType=binary&ratio=1&rotation=0&showTitle=false&size=293536&status=done&style=none&taskId=u14d47ef0-7d15-46bb-8a52-644ef70c433&title=&width=1684.4444890669847)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670314393717-42515b83-5815-4197-b73f-f52b2c2db5f5.png#averageHue=%230a0908&clientId=u7f1d3d8f-5941-4&from=paste&height=459&id=uc33a7326&originHeight=413&originWidth=1193&originalType=binary&ratio=1&rotation=0&showTitle=false&size=57581&status=done&style=none&taskId=u3cf547d7-c0b4-4678-9c6f-8a34ee1998a&title=&width=1325.5555906707866)
<a name="qWk3F"></a>
### contexts class
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670320855146-146a11fe-e7a9-411e-b1d9-d58b9c330cfa.png#averageHue=%2312110f&clientId=u7f1d3d8f-5941-4&from=paste&height=79&id=u8728caa8&originHeight=71&originWidth=845&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9417&status=done&style=none&taskId=ufbbfce46-4d32-4de2-b7f7-32074698e2e&title=&width=938.8889137609511)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670314506168-9e976551-b9c4-40d3-9154-05c98c1261e7.png#averageHue=%23070707&clientId=u7f1d3d8f-5941-4&from=paste&height=553&id=u536dda83&originHeight=498&originWidth=1560&originalType=binary&ratio=1&rotation=0&showTitle=false&size=130220&status=done&style=none&taskId=u1b19bdfe-5338-4feb-aa95-eef5717db4e&title=&width=1733.3333792509868)
<a name="yasrt"></a>
#### MPxContext
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670314566636-98b3ea1e-9d0c-4747-bb35-2218020358f4.png#averageHue=%230a0a0a&clientId=u7f1d3d8f-5941-4&from=paste&height=748&id=ud98b9990&originHeight=673&originWidth=1505&originalType=binary&ratio=1&rotation=0&showTitle=false&size=271852&status=done&style=none&taskId=uc86eae1f-512d-4354-8966-b6dab1fdb16&title=&width=1672.222266520984)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670314628131-bfae171b-b57a-41c5-a45e-615dcc82baae.png#averageHue=%23090808&clientId=u7f1d3d8f-5941-4&from=paste&height=531&id=uefea2edf&originHeight=478&originWidth=944&originalType=binary&ratio=1&rotation=0&showTitle=false&size=47400&status=done&style=none&taskId=uf3a88e84-bc4a-4608-8a60-c833daa9f4b&title=&width=1048.8889166749561)
<a name="EjDvf"></a>
#### MPxContextCommand
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670314724095-6febfa93-6eea-4fc6-9105-afd449a494eb.png#averageHue=%230b0b0b&clientId=u7f1d3d8f-5941-4&from=paste&height=522&id=uf02ad2a6&originHeight=470&originWidth=1468&originalType=binary&ratio=1&rotation=0&showTitle=false&size=199346&status=done&style=none&taskId=ueac65ccb-dd00-44e2-8fd6-2d7f77603f7&title=&width=1631.1111543208003)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670314741398-3373638b-1a47-4bf9-8867-5d284b8de65b.png#averageHue=%23090807&clientId=u7f1d3d8f-5941-4&from=paste&height=380&id=u18854ee7&originHeight=342&originWidth=1117&originalType=binary&ratio=1&rotation=0&showTitle=false&size=34098&status=done&style=none&taskId=uf0c2fafe-41ed-4817-b2bc-f16806ad7f9&title=&width=1241.1111439893284)
<a name="Bg5Ad"></a>
#### MPxToolCommand
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670314838409-43a977bf-405b-4c77-9730-aedb1ff303fd.png#averageHue=%230a0a0a&clientId=u7f1d3d8f-5941-4&from=paste&height=803&id=ucc5b9b9d&originHeight=723&originWidth=1596&originalType=binary&ratio=1&rotation=0&showTitle=false&size=321569&status=done&style=none&taskId=u0e8c7561-12c9-40fc-aca5-44a8e6b6c3b&title=&width=1773.333380310625)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670314882771-837d3d6a-b70e-4d2e-a8a9-17717a3f045a.png#averageHue=%23080707&clientId=u7f1d3d8f-5941-4&from=paste&height=631&id=u3381456a&originHeight=568&originWidth=1060&originalType=binary&ratio=1&rotation=0&showTitle=false&size=48382&status=done&style=none&taskId=u4dd9e33c-e430-4e3f-b520-0b5d969ade2&title=&width=1177.7778089782346)
<a name="WebzE"></a>
### 限制
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670315161425-a8ef71e2-6d09-4adb-8efe-1f147b239d59.png#averageHue=%230a0a0a&clientId=u7f1d3d8f-5941-4&from=paste&height=774&id=uea1d0fe0&originHeight=697&originWidth=1517&originalType=binary&ratio=1&rotation=0&showTitle=false&size=288780&status=done&style=none&taskId=u0358ebe1-b9eb-488c-9e69-a825fba52d6&title=&width=1685.5556002075302)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670315219263-813cdfbd-9de5-4e6c-a69e-4447059f2732.png#averageHue=%23080807&clientId=u7f1d3d8f-5941-4&from=paste&height=583&id=uba1e83d3&originHeight=525&originWidth=1466&originalType=binary&ratio=1&rotation=0&showTitle=false&size=57377&status=done&style=none&taskId=ue52ba2c5-7e30-4a13-a220-8e1f35b8355&title=&width=1628.8889320397095)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670315514778-102a372c-5ec9-4310-a356-34a085abdc54.png#averageHue=%230b0b0b&clientId=u7f1d3d8f-5941-4&from=paste&height=877&id=uacd4817c&originHeight=789&originWidth=1576&originalType=binary&ratio=1&rotation=0&showTitle=false&size=373584&status=done&style=none&taskId=u9d104a94-f5d6-4217-81a8-c5092cd5ead&title=&width=1751.1111574997149)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670315560657-f135614b-2a7f-4e37-aeb6-c08ecf020f6e.png#averageHue=%23070606&clientId=u7f1d3d8f-5941-4&from=paste&height=827&id=u9b5dc5f0&originHeight=744&originWidth=1552&originalType=binary&ratio=1&rotation=0&showTitle=false&size=90249&status=done&style=none&taskId=u1155dc37-d283-4e88-ba8a-914ffc61b0c&title=&width=1724.444490126623)
<a name="aHpYe"></a>
### 举例
<a name="jLo8j"></a>
#### context工具模板
```python
# coding: utf-8
# 此插件只适用于maya2020及以上版本
import maya.api.OpenMaya as om
import maya.api.OpenMayaUI as omui
import maya.cmds as cmds
import os

def maya_useNewAPI():
    """ 告知maya,使用的是maya api 2.0 """
    pass

class SimpleContext(omui.MPxContext):

    TITLE = "Simple Context"

    HELP_TEXT = "<insert help text here>"

    def __init__(self):
        super(SimpleContext, self).__init__()

        self.setTitleString(SimpleContext.TITLE)
        plugin_dir_path = os.path.dirname(cmds.pluginInfo("template_context.py",p=True,q=True))  
        self.setImage(plugin_dir_path + "/icons/icon_windows.png", omui.MPxContext.kImage1) # 设置工具的图标
    
    def helpSlateHasChanged(self, event):
        self.setHelpString(SimpleContext.HELP_TEXT)

    def toolOnSetup(self, event):
        """ 工具加载时执行 """
        print("toolOnSetup")

    def toolOffCleanup(self):
        """ 取消工具加载时执行(在使用工具的同时创建模型maya会自动先取消加载工具再自动加载工具) """
        print("toolOffCleanup")
    
    def doPress(self, event, draw_manager, frame_context):
        """ 按下键时执行 """
        mouse_button = event.mouseButton()  # 获取鼠标的按键

        if mouse_button == omui.MEvent.kLeftMouse:
            # 如果按下鼠标左键执行
            print("Left mouse button pressed") 
        elif mouse_button == omui.MEvent.kMiddleMouse:
            # 如果按下鼠标中键执行
            print("Middle mouse button pressed")
    
    def doRelease(self, event, draw_manager, frame_context):
        """ 松开键时执行 """
        print("Mouse button released")
    
    def doDrag(self, event, draw_manager, frame_context):
        """ 按住鼠标左键并进行移动时执行 """
        print("Mouse drag")
    
    def completeAction(self):
        """ 按下enter键时执行 """
        print("Complete action (enter/return key pressed)")
    
    def deleteAction(self):
        """ 按下delete键或者backspace键时执行 """
        print("Delete action (backspace/delete key pressed)")
    
    def abortAction(self):
        """ 按下esc键时执行 """
        print("Abort action (escape key pressed)")

class SimpleContextCmd(omui.MPxContextCommand):

        COMMAND_NAME = "rcSimpleCtx"

        def __init__(self):
            super(SimpleContextCmd, self).__init__()
        
        def makeObj(self):
            return SimpleContext()
        
        @classmethod
        def creator(cls):
            return SimpleContextCmd()

def initializePlugin(plugin): 
    """ 插件加载时执行这个函数"""
    vendor = "RuiChen"  # 插件制作人的名字
    version = "1.0.0"  # 插件的版本

    plugin_fn = om.MFnPlugin(plugin, vendor, version)  # 定义插件
    try:
        plugin_fn.registerContextCommand(SimpleContextCmd.COMMAND_NAME, SimpleContextCmd.creator)
    except:
        om.MGlobal.displayError("Failed to register context command: {0}".format(SimpleContextCmd.COMMAND_NAME))

def uninitializePlugin(plugin):
    """ 插件取消加载时执行这个函数"""
    plugin_fn = om.MFnPlugin(plugin)
    try:
        plugin_fn.deregisterContextCommand(SimpleContextCmd.COMMAND_NAME)
    except:
        om.MGlobal.displayError("Failed to deregister context command: {0}".format(SimpleContextCmd.COMMAND_NAME))

if __name__ == '__main__':
    """ 注册后,在maya脚本编辑器中的使用方法 """
    cmds.file(new=True,force=True)

    plugin_name = "template_context.py"  # 插件的文件名

    # 如果插件加载了就先取消加载插件
    cmds.evalDeferred('if cmds.pluginInfo("{0}", q=True, loaded=True): cmds.unloadPlugin("{0}")'.format(plugin_name))
    # 如果插件没有加载就加载插件
    cmds.evalDeferred('if not cmds.pluginInfo("{0}", q=True, loaded=True): cmds.loadPlugin("{0}")'.format(plugin_name))

    cmds.evalDeferred('context = cmds.rcSimpleCtx(); cmds.setToolTo(context)')

```
<a name="filnU"></a>
#### custom select 工具
```python
# coding: utf-8
# 此插件只适用于maya2020及以上版本
# 插件介绍: 使用context时按ctrl键框选只选择mesh,按ctrl+shift键时只选择light，不按只框选就全选择
import maya.api.OpenMaya as om
import maya.api.OpenMayaUI as omui
import maya.cmds as cmds
import os

def maya_useNewAPI():
    """ 告知maya,使用的是maya api 2.0 """
    pass

class CustomSelectContext(omui.MPxContext):

    TITLE = "Custom Select Context"

    HELP_TEXT = "Ctrl to select only meshes. Ctrl+Shift to select only lights."

    def __init__(self):
        super(CustomSelectContext, self).__init__()

        self.setTitleString(CustomSelectContext.TITLE)
        plugin_dir_path = os.path.dirname(cmds.pluginInfo("custom_select_context.py",p=True,q=True))  
        self.setImage(plugin_dir_path + "/icons/icon_windows.png", omui.MPxContext.kImage1) # 设置工具的图标
        test_file_path = plugin_dir_path + "/test_scene/custom_select_context_test.ma"
    
    def helpStateHasChanged(self, event):
        """ 在左下角显示帮助 """
        self.setHelpString(CustomSelectContext.HELP_TEXT)

    def toolOnSetup(self, event):
        """ 工具加载时执行 """
        print("toolOnSetup")

    def toolOffCleanup(self):
        """ 取消工具加载时执行(在使用工具的同时创建模型maya会自动先取消加载工具再自动加载工具) """
        print("toolOffCleanup")
    
    def doPress(self, event, draw_manager, frame_context):
        """ 按下键时执行 """
        self.viewport_start_pos = event.position

        self.light_only = False # 用来判断是否只选择灯光类型
        self.meshes_only = False # 用来判断是否只选择mesh类型

        if event.isModifierControl():
            if event.isModifierShift():
                self.light_only = True  # 当ctrl和shift键同时按下时为True
            else:
                self.meshes_only = True  # 当ctrl键按下时为True
            
    def doRelease(self, event, draw_manager, frame_context):
        """ 松开键时执行 """
        self.viewport_end_pos = event.position

        initial_selection = om.MGlobal.getActiveSelectionList() # 获取场景中已经选择的对象的列表

        om.MGlobal.selectFromScreen(self.viewport_start_pos[0], self.viewport_start_pos[1],
                                    self.viewport_end_pos[0], self.viewport_end_pos[1],
                                    om.MGlobal.kReplaceList) # 根据矩形框选择矩形中的对象（这个命令所进行的选择不会进入undo堆栈，因此需要通过其他命令设置正常的堆栈）
        
        selection_list = om.MGlobal.getActiveSelectionList() # 获取通过矩形框选中的对象的列表

        if self.light_only or self.meshes_only:
            for i in reversed(range(selection_list.length())):
                obj = selection_list.getDependNode(i)
                shape = om.MFnDagNode(obj).child(0)

                if self.light_only and not shape.hasFn(om.MFn.kLight): # 如果shape节点是light类型
                    selection_list.remove(i)
                elif self.meshes_only and not shape.hasFn(om.MFn.kMesh): # 如果shape节点是mesh类型
                    selection_list.remove(i)

        om.MGlobal.setActiveSelectionList(initial_selection, om.MGlobal.kReplaceList) # 首先选择场景中之前已经选择的列表
        om.MGlobal.selectCommand(selection_list, om.MGlobal.kReplaceList)  # 通过调用内置的maya选择命令来选择，并且让maya负责维护堆栈
    
    def doDrag(self, event, draw_manager, frame_context):
        """ 按住鼠标左键并进行移动时执行 """
        self.viewport_end_pos = event.position

        self.draw_selection_rectangle(draw_manager,
                                      self.viewport_start_pos[0],self.viewport_start_pos[1],
                                      self.viewport_end_pos[0],self.viewport_start_pos[1],
                                      self.viewport_end_pos[0],self.viewport_end_pos[1],
                                      self.viewport_start_pos[0],self.viewport_end_pos[1])

    def draw_selection_rectangle(self, draw_manager, x0, y0, x1, y1, x2, y2, x3, y3):
        """ 根据鼠标拖拽的范围进行矩形绘制 """
        draw_manager.beginDrawable() # 开始绘制
        draw_manager.setLineWidth(1.0) # 设置绘制线的宽度
        draw_manager.setColor(om.MColor((1.0, 0.0, 0.0))) # 设置绘制的颜色（颜色数值是一个集合）

        draw_manager.line2d(om.MPoint(x0,y0),om.MPoint(x1,y1))
        draw_manager.line2d(om.MPoint(x1,y1),om.MPoint(x2,y2))
        draw_manager.line2d(om.MPoint(x2,y2),om.MPoint(x3,y3))
        draw_manager.line2d(om.MPoint(x3,y3),om.MPoint(x0,y0))

        draw_manager.endDrawable() # 结束绘制


class CustomSelectContextCmd(omui.MPxContextCommand):

        COMMAND_NAME = "rcCustomSelectCtx"

        def __init__(self):
            super(CustomSelectContextCmd, self).__init__()
        
        def makeObj(self):
            return CustomSelectContext()
        
        @classmethod
        def creator(cls):
            return CustomSelectContextCmd()

def initializePlugin(plugin): 
    """ 插件加载时执行这个函数"""
    vendor = "RuiChen"  # 插件制作人的名字
    version = "1.0.0"  # 插件的版本

    plugin_fn = om.MFnPlugin(plugin, vendor, version)  # 定义插件
    try:
        plugin_fn.registerContextCommand(CustomSelectContextCmd.COMMAND_NAME, CustomSelectContextCmd.creator)
    except:
        om.MGlobal.displayError("Failed to register context command: {0}".format(CustomSelectContextCmd.COMMAND_NAME))

def uninitializePlugin(plugin):
    """ 插件取消加载时执行这个函数"""
    plugin_fn = om.MFnPlugin(plugin)
    try:
        plugin_fn.deregisterContextCommand(CustomSelectContextCmd.COMMAND_NAME)
    except:
        om.MGlobal.displayError("Failed to deregister context command: {0}".format(CustomSelectContextCmd.COMMAND_NAME))

if __name__ == '__main__':
    """ 注册后,在maya脚本编辑器中的使用方法 """
    cmds.file(new=True,force=True)

    plugin_dir_path = os.path.dirname(cmds.pluginInfo("custom_select_context.py",p=True,q=True)) 
    test_file_path = plugin_dir_path + "/test_scene/custom_select_context_test.ma"

    plugin_name = "custom_select_context.py"  # 插件的文件名

    # 如果插件加载了就先取消加载插件
    cmds.evalDeferred('if cmds.pluginInfo("{0}", q=True, loaded=True): cmds.unloadPlugin("{0}")'.format(plugin_name))
    # 如果插件没有加载就加载插件
    cmds.evalDeferred('if not cmds.pluginInfo("{0}", q=True, loaded=True): cmds.loadPlugin("{0}")'.format(plugin_name))
    cmds.evalDeferred('cmds.file(test_file_path,o=True,f=True)')
    cmds.evalDeferred('context = cmds.rcCustomSelectCtx(); cmds.setToolTo(context)')

```
<a name="zOgx0"></a>
#### 创建骨骼工具
```python
# coding: utf-8
# 此插件只适用于maya2020及以上版本
import maya.api.OpenMaya as om
import maya.api.OpenMayaUI as omui
import maya.cmds as cmds
import os

def maya_useNewAPI():
    """ 告知maya,使用的是maya api 2.0 """
    pass

class JointCreateContext(omui.MPxContext):

    TITLE = "JointCreate Context"

    HELP_TEXT = ["Select first joint location",
                 "Select second joint location",
                 "Select final joint location",
                 "Press Enter to complete"]

    def __init__(self):
        super(JointCreateContext, self).__init__()

        self.setTitleString(JointCreateContext.TITLE)
        plugin_dir_path = os.path.dirname(cmds.pluginInfo("joint_create_context.py",p=True,q=True))  
        self.setImage(plugin_dir_path + "/icons/icon_windows.png", omui.MPxContext.kImage1) # 设置工具的图标

        self.state = 0 # 判断通过工具选择的对象的个数
        self.context_selection = om.MSelectionList() # 通过工具选择的对象的列表
    
    def helpStateHasChanged(self, event):
        self.update_help_string()
    
    def update_help_string(self):
        self.setHelpString(JointCreateContext.HELP_TEXT[self.state])

    def toolOnSetup(self, event):
        """ 工具加载时执行 """
        om.MGlobal.selectCommand(om.MSelectionList()) # 确保工具刚开始使用时是一个健康的选择状态
        self.reset_state()

    def toolOffCleanup(self):
        """ 取消工具加载时执行(在使用工具的同时创建模型maya会自动先取消加载工具再自动加载工具) """
        self.reset_state()
    
    def doRelease(self, event, draw_manager, frame_context):
        """ 松开键时执行 """
        if self.state >= 0 and self.state < 3:
            om.MGlobal.selectFromScreen(event.position[0], event.position[1],event.position[0],event.position[1],om.MGlobal.kReplaceList)

            active_selection = om.MGlobal.getActiveSelectionList() # 获取当前选择的物体
            if active_selection.length() == 1:
                self.context_selection.merge(active_selection) # 使用merge方法防止重复的对象出现在context_selection中

            om.MGlobal.setActiveSelectionList(self.context_selection) # 更改当前选择的物体

            self.update_state
    
    def completeAction(self):
        """ 按下enter键时执行 """
        selection_count = self.context_selection.length()
        if selection_count == 3:
            om.MGlobal.setActiveSelectionList(om.MSelectionList())

            for i in range(selection_count):
                transform_fn = om.MFnTransform(self.context_selection.getDependNode(i))

                cmds.joint(position = transform_fn.translation(om.MSpace.kTransform))
                cmds.delete(transform_fn.name())
            
            cmds.select(clear=True)
            self.reset_state()
        
        else:
            om.MGlobal.displayError("Three objects must be selected")
    
    def deleteAction(self):
        """ 按下delete键或者backspace键时执行 """
        selection_count = self.context_selection.length()
        if selection_count > 0:
            self.context_selection.remove(selection_count - 1)

            om.MGlobal.setActiveSelectionList(self.context_selection)

            self.update_state()
    
    def abortAction(self):
        """ 按下esc键时执行 """
        self.reset_state()

    def update_state(self):
        """ 更新状态 """
        self.state = self.context_selection.length()

        self.update_help_string()
    
    def reset_state(self):
        """ 重置状态 """
        om.MGlobal.setActiveSelectionList(om.MSelectionList())

        self.context_selection.clear()
        self.update_state

class JointCreateContextCmd(omui.MPxContextCommand):

        COMMAND_NAME = "rcJointCreateCtx"

        def __init__(self):
            super(JointCreateContextCmd, self).__init__()
        
        def makeObj(self):
            return JointCreateContext()
        
        @classmethod
        def creator(cls):
            return JointCreateContextCmd()

def initializePlugin(plugin): 
    """ 插件加载时执行这个函数"""
    vendor = "RuiChen"  # 插件制作人的名字
    version = "1.0.0"  # 插件的版本

    plugin_fn = om.MFnPlugin(plugin, vendor, version)  # 定义插件
    try:
        plugin_fn.registerContextCommand(JointCreateContextCmd.COMMAND_NAME, JointCreateContextCmd.creator)
    except:
        om.MGlobal.displayError("Failed to register context command: {0}".format(JointCreateContextCmd.COMMAND_NAME))

def uninitializePlugin(plugin):
    """ 插件取消加载时执行这个函数"""
    plugin_fn = om.MFnPlugin(plugin)
    try:
        plugin_fn.deregisterContextCommand(JointCreateContextCmd.COMMAND_NAME)
    except:
        om.MGlobal.displayError("Failed to deregister context command: {0}".format(JointCreateContextCmd.COMMAND_NAME))

if __name__ == '__main__':
    """ 注册后,在maya脚本编辑器中的使用方法 """
    cmds.file(new=True,force=True)
    plugin_dir_path = os.path.dirname(cmds.pluginInfo("joint_create_context.py",p=True,q=True)) 
    test_file_path = plugin_dir_path + "/test_scene/joint_create_context_test.ma"

    plugin_name = "joint_create_context.py"  # 插件的文件名

    # 如果插件加载了就先取消加载插件
    cmds.evalDeferred('if cmds.pluginInfo("{0}", q=True, loaded=True): cmds.unloadPlugin("{0}")'.format(plugin_name))
    # 如果插件没有加载就加载插件
    cmds.evalDeferred('if not cmds.pluginInfo("{0}", q=True, loaded=True): cmds.loadPlugin("{0}")'.format(plugin_name))
    cmds.evalDeferred('cmds.file(test_file_path,o=True,f=True)')
    cmds.evalDeferred('context = cmds.rcJointCreateCtx(); cmds.setToolTo(context)')

```
<a name="nmCaZ"></a>
#### 各种绘制举例
```python
# coding: utf-8
# 此插件只适用于maya2020及以上版本
import maya.api.OpenMaya as om
import maya.api.OpenMayaUI as omui
import maya.cmds as cmds
import os

def maya_useNewAPI():
    """ 告知maya,使用的是maya api 2.0 """
    pass

class SimpleContext(omui.MPxContext):

    TITLE = "Simple Context"

    HELP_TEXT = "<insert help text here>"

    def __init__(self):
        super(SimpleContext, self).__init__()

        self.setTitleString(SimpleContext.TITLE)
        plugin_dir_path = os.path.dirname(cmds.pluginInfo("draw_persistence_example_context.py",p=True,q=True))  
        self.setImage(plugin_dir_path + "/icons/icon_windows.png", omui.MPxContext.kImage1) # 设置工具的图标 
    
    def helpStateHasChanged(self, event):
        self.setHelpString(SimpleContext.HELP_TEXT)

    def toolOnSetup(self, event):
        """ 工具加载时执行 """
        print("toolOnSetup")

    def toolOffCleanup(self):
        """ 取消工具加载时执行(在使用工具的同时创建模型maya会自动先取消加载工具再自动加载工具) """
        print("toolOffCleanup")
    
    def doPress(self, event, draw_manager, frame_context):
        """ 按下键时执行 """
        mouse_button = event.mouseButton()  # 获取鼠标的按键

        if mouse_button == omui.MEvent.kLeftMouse:
            # 如果按下鼠标左键执行
            print("Left mouse button pressed") 
        elif mouse_button == omui.MEvent.kMiddleMouse:
            # 如果按下鼠标中键执行
            print("Middle mouse button pressed")
    
    def doRelease(self, event, draw_manager, frame_context):
        """ 松开键时执行 """
        print("Mouse button released")
    
    def doDrag(self, event, draw_manager, frame_context):
        """ 按住鼠标左键并进行移动时执行 """
        print("Mouse drag")
    
    def completeAction(self):
        """ 按下enter键时执行 """
        print("Complete action (enter/return key pressed)")
    
    def deleteAction(self):
        """ 按下delete键或者backspace键时执行 """
        print("Delete action (backspace/delete key pressed)")
    
    def abortAction(self):
        """ 按下esc键时执行 """
        print("Abort action (escape key pressed)")
    
    def doPtrMoved(self, event, draw_manager, frame_context):
        """ 当鼠标移动并且没有按下鼠标按钮时执行 """
        self.position = om.MPoint(event.position)
        # self.draw_circle(event, draw_manager)
        self.draw_info(draw_manager, frame_context)

    def drawFeedback(self, draw_manager, frame_context):
        """ 无论执行什么操作都会始终执行绘制 """
        # self.draw_sphere(draw_manager)
        # self.draw_info(draw_manager, frame_context) # 在这个函数中执行绘制text有显示的bug，不推荐使用
        pass

    def draw_circle(self, event, draw_manager):
        """ 在鼠标指针的位置处绘制圆形 """
        center = om.MPoint(event.position)
        radius = 20
        
        draw_manager.beginDrawable()
        draw_manager.circle2d(center, radius, True)
        draw_manager.endDrawable()
    
    def draw_sphere(self, draw_manager):
        """ 在坐标原点绘制一个半径为5cm的圆球 """
        draw_manager.beginDrawable()
        draw_manager.sphere(om.MPoint(0,0), 5)
        draw_manager.endDrawable()
    
    def draw_info(self, draw_manager, frame_context):
        """ 在视口左上角绘制文字信息 """
        viewport_height = frame_context.getViewportDimensions()[3]

        info_position = om.MPoint(20, viewport_height - 20)
        text = "Mouse pos: {0}, {1}".format(self.position.x, self.position.y)

        draw_manager.beginDrawable()
        draw_manager.text2d(info_position, text)
        draw_manager.endDrawable()

class SimpleContextCmd(omui.MPxContextCommand):

        COMMAND_NAME = "rcSimpleCtx"

        def __init__(self):
            super(SimpleContextCmd, self).__init__()
        
        def makeObj(self):
            return SimpleContext()
        
        @classmethod
        def creator(cls):
            return SimpleContextCmd()

def initializePlugin(plugin): 
    """ 插件加载时执行这个函数"""
    vendor = "RuiChen"  # 插件制作人的名字
    version = "1.0.0"  # 插件的版本

    plugin_fn = om.MFnPlugin(plugin, vendor, version)  # 定义插件
    try:
        plugin_fn.registerContextCommand(SimpleContextCmd.COMMAND_NAME, SimpleContextCmd.creator)
    except:
        om.MGlobal.displayError("Failed to register context command: {0}".format(SimpleContextCmd.COMMAND_NAME))

def uninitializePlugin(plugin):
    """ 插件取消加载时执行这个函数"""
    plugin_fn = om.MFnPlugin(plugin)
    try:
        plugin_fn.deregisterContextCommand(SimpleContextCmd.COMMAND_NAME)
    except:
        om.MGlobal.displayError("Failed to deregister context command: {0}".format(SimpleContextCmd.COMMAND_NAME))

if __name__ == '__main__':
    """ 注册后,在maya脚本编辑器中的使用方法 """
    cmds.file(new=True,force=True)

    plugin_name = "draw_persistence_example_context.py"  # 插件的文件名

    # 如果插件加载了就先取消加载插件
    cmds.evalDeferred('if cmds.pluginInfo("{0}", q=True, loaded=True): cmds.unloadPlugin("{0}")'.format(plugin_name))
    # 如果插件没有加载就加载插件
    cmds.evalDeferred('if not cmds.pluginInfo("{0}", q=True, loaded=True): cmds.loadPlugin("{0}")'.format(plugin_name))

    cmds.evalDeferred('context = cmds.rcSimpleCtx(); cmds.setToolTo(context)')

```
<a name="y0TKk"></a>
# 第三卷
<a name="mPC43"></a>
## Locators（可参考HelloWorldNode）
<a name="L8NWI"></a>
### MPxLocatorNode
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670824784593-b4e2aa98-d50f-45e4-abea-b3f7a774eece.png#averageHue=%230b0b0b&clientId=u0fb33782-733b-4&from=paste&height=562&id=u38288abb&originHeight=506&originWidth=1113&originalType=binary&ratio=1&rotation=0&showTitle=false&size=141834&status=done&style=none&taskId=u297df3fd-7477-4bdf-9932-2e82aad8e03&title=&width=1236.6666994271463)
<a name="t7d3P"></a>
### MPxDrawOverride（VP2.0）
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670824823422-3d2a2cad-30cd-4e17-963c-2128659f31cb.png#averageHue=%230b0b0b&clientId=u0fb33782-733b-4&from=paste&height=532&id=u11b5804e&originHeight=479&originWidth=1509&originalType=binary&ratio=1&rotation=0&showTitle=false&size=197495&status=done&style=none&taskId=u6f2950a7-2835-4757-bed7-59ba1cbfff1&title=&width=1676.666711083166)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670824872793-3e8e184c-6dc4-4370-bfc6-8eccc2aafa5b.png#averageHue=%230c0b0a&clientId=u0fb33782-733b-4&from=paste&height=328&id=uacb92293&originHeight=295&originWidth=1042&originalType=binary&ratio=1&rotation=0&showTitle=false&size=33544&status=done&style=none&taskId=u0bc92d29-62bd-46dc-84d6-27e74402a71&title=&width=1157.7778084484155)
<a name="xbGCL"></a>
### 代码举例
<a name="z2Xy5"></a>
#### 创建带形状变形器，通过更改序号改变定位器的形状
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670928053999-00cb576f-99ea-468c-b2a7-064038a8aafe.png#averageHue=%23545353&clientId=uaca77ae3-2815-4&from=paste&height=719&id=uc070a55d&originHeight=647&originWidth=1214&originalType=binary&ratio=1&rotation=0&showTitle=false&size=35937&status=done&style=none&taskId=ue639a515-b28b-4461-a1ba-db5b1dc486c&title=&width=1348.8889246222423)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670928061330-bde1870c-6966-4420-b47b-7e98ece72314.png#averageHue=%23535353&clientId=uaca77ae3-2815-4&from=paste&height=590&id=uc5b9d692&originHeight=531&originWidth=1203&originalType=binary&ratio=1&rotation=0&showTitle=false&size=26767&status=done&style=none&taskId=u0dfebbe0-bd33-4164-9f7f-6277ed2cf7a&title=&width=1336.6667020762418)
```python
# coding: utf-8
import maya.api.OpenMaya as om
import maya.api.OpenMayaUI as omui
import maya.api.OpenMayaRender as omr

import maya.cmds as cmds


def maya_useNewAPI():
    """ 告知maya,使用的是maya api 2.0 """
    pass


class SimpleLocatorNode(omui.MPxLocatorNode):
    TYPE_NAME = "simplelocator"
    TYPE_ID = om.MTypeId(0x0007F7FE)
    DRAW_CLASSIFICATION = "drawdb/geometry/simplelocator"
    DRAW_REGISTRANT_ID = "SimpleLocatorNode"

    def __init__(self):
        super(SimpleLocatorNode, self).__init__()

    @classmethod
    def creator(cls):
        return SimpleLocatorNode()

    @classmethod
    def initialize(cls):
        numeric_attr = om.MFnNumericAttribute()

        cls.shape_index_obj = numeric_attr.create("shapeIndex", "si", om.MFnNumericData.kInt, 0)
        numeric_attr.setMin(0)
        numeric_attr.setMax(2)

        cls.addAttribute(cls.shape_index_obj)

class SimpleLocatorUserData(om.MUserData):
    """ 创建MUserData类使其对象能够将数据在prepareForDraw与addUIDrawables之间相互传递  """
    def __init(self, deleteAfterUse = False):  # 设置为使用数据后不删除数据
        super(SimpleLocatorUserData, self).__init__(deleteAfterUse)

        self.shape_index = 0
        self.wireframe_color = om.MColor((1.0, 1.0, 1.0))  # 线框颜色

class SimpleLocatorDrawOverride(omr.MPxDrawOverride):
    NAME = "SimpleLocatorDrawOverride"

    def __init__(self, obj):
        super(SimpleLocatorDrawOverride, self).__init__(obj, None, True)  # 第一个参数是maya object,第二个参数是绘制是callback函数,第三个参数是默认为True,为True时将会将此标志位dirty状态，因此可以持续更新,建议为True,除非遇到了性能问题可以为False

    def supportedDrawAPIs(self):
        return omr.MRenderer.kAllDevices

    def hasUIDrawables(self):
        return True

    def prepareForDraw(self, obj_path, camera_path, frame_context, old_data):
        """ 在使用绘制图形的方法之前,使用这个方法来将数据检索与缓存 """
        data = old_data
        if not data:
            data = SimpleLocatorUserData()

        locator_obj = obj_path.node()
        node_fn = om.MFnDependencyNode(locator_obj)

        data.shape_index = node_fn.findPlug("shapeIndex", False).asInt()

        display_status = omr.MGeometryUtilities.displayStatus(obj_path)
        if display_status == omr.MGeometryUtilities.kDormant:  
            data.wireframe_color = om.MColor((0.0, 0.1, 0.0)) # 当节点处于未选中状态时设置颜色为深绿色
        else:
            data.wireframe_color = omr.MGeometryUtilities.wireframeColor(obj_path)  # 其他状态按照maya的标准来设置线框颜色

        return data

    def addUIDrawables(self, obj_path, draw_manager, frame_context, data):
        """ 绘制图形的方法

        Args:
            obj_path (_type_): 指向正在绘制的对象的路径,这里是指locator节点
            draw_manager (_type_): 用于绘制简单的几何图形
            frame_context (_type_): 包含当前渲染框架的一些全局信息
            data (_type_): 用户创建的数据对象,存储缓存数据,类型为MUserDataObject
        """
        draw_manager.beginDrawable()

        draw_manager.setColor(data.wireframe_color)

        if data.shape_index == 0: # 绘制圆形
            draw_manager.circle(om.MPoint(0.0, 0.0, 0.0), om.MVector(0.0, 1.0, 0.0), 1, False)
        elif data.shape_index == 1: # 绘制矩形
            draw_manager.rect(om.MPoint(0.0, 0.0, 0.0), om.MVector(0.0, 0.0, 1.0), om.MVector(0.0, 1.0, 0.0), 1.0, 1.0, False)
        elif data.shape_index == 2: # 绘制三角形
            point_array = om.MPointArray([(-1.0, 0.0, -1.0), (0.0, 0.0, 1.0),(1.0, 0.0, -1.0),(-1.0, 0.0, -1.0)])
            draw_manager.lineStrip(point_array, False)

        draw_manager.endDrawable()

    @classmethod
    def creator(cls, obj):
        return SimpleLocatorDrawOverride(obj)


def initializePlugin(plugin):
    """ 插件加载时执行这个函数"""
    vendor = "RuiChen"  # 插件制作人的名字
    version = "1.0.0"  # 插件的版本

    plugin_fn = om.MFnPlugin(plugin, vendor, version)  # 定义插件
    try:
        plugin_fn.registerNode(SimpleLocatorNode.TYPE_NAME,
                               SimpleLocatorNode.TYPE_ID,
                               SimpleLocatorNode.creator,
                               SimpleLocatorNode.initialize,
                               om.MPxNode.kLocatorNode,
							   SimpleLocatorNode.DRAW_CLASSIFICATION)
    except:
        om.MGlobal.displayError("Failed to register node: {0}".format(SimpleLocatorNode.TYPE_NAME))

    try:
        omr.MDrawRegistry.registerDrawOverrideCreator(SimpleLocatorNode.DRAW_CLASSIFICATION,
                                                      SimpleLocatorNode.DRAW_REGISTRANT_ID,
                                                      SimpleLocatorDrawOverride.creator)
    except:
        om.MGlobal.displayError("Failed to register draw override: {0}".format(SimpleLocatorDrawOverride.NAME))


def uninitializePlugin(plugin):
    """ 插件取消加载时执行这个函数"""
    plugin_fn = om.MFnPlugin(plugin)
    try:
        omr.MDrawRegistry.deregisterDrawOverrideCreator(SimpleLocatorNode.DRAW_CLASSIFICATION,
                                                        SimpleLocatorNode.DRAW_REGISTRANT_ID)
    except:
        om.MGlobal.displayError("Failed to deregister draw override: {0}".format(SimpleLocatorDrawOverride.NAME))

    try:
        plugin_fn.deregisterNode(SimpleLocatorNode.TYPE_ID)
    except:
        om.MGlobal.displayError("Failed to deregister node: {0}".format(SimpleLocatorNode.TYPE_NAME))


if __name__ == '__main__':
    """ 注册后,在maya脚本编辑器中的使用方法 """
    cmds.file(new=True,f=True)

    plugin_name = "simple_locator_node.py"  # 插件的文件名
    # 如果插件加载了就先取消加载插件
    cmds.evalDeferred('if cmds.pluginInfo("{0}", q=True, loaded=True): cmds.unloadPlugin("{0}")'.format(plugin_name))
    # 如果插件没有加载就加载插件
    cmds.evalDeferred('if not cmds.pluginInfo("{0}", q=True, loaded=True): cmds.loadPlugin("{0}")'.format(plugin_name))

    cmds.evalDeferred('cmds.createNode("simplelocator")')


```
<a name="ANATJ"></a>
#### 测量两个网格体的距离的定位器

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670928161742-d22eb865-d937-45aa-9c8a-2e3abdf0886d.png#averageHue=%235c5c5c&clientId=uaca77ae3-2815-4&from=paste&height=352&id=u10c1c9ed&originHeight=317&originWidth=743&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9114&status=done&style=none&taskId=u9189b8ad-021b-4a51-be13-9a89b8cf206&title=&width=825.5555774253097)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670928211727-341226e9-16d0-4861-9ca7-9c2b4fdf4444.png#averageHue=%23403f3f&clientId=uaca77ae3-2815-4&from=paste&height=349&id=u45f8f19c&originHeight=314&originWidth=690&originalType=binary&ratio=1&rotation=0&showTitle=false&size=27137&status=done&style=none&taskId=ua5d7643a-88f6-4aa3-9bc2-a3527437368&title=&width=766.6666869763981)
```python
# coding: utf-8
# 不适用于2018及以下版本
import maya.api.OpenMaya as om
import maya.api.OpenMayaUI as omui
import maya.api.OpenMayaRender as omr


import maya.cmds as cmds



def maya_useNewAPI():
    """ 告知maya,使用的是maya api 2.0 """
    pass



class DistanceBetweenLocator(omui.MPxLocatorNode):
    TYPE_NAME = "distanceBetweenLocator"
    TYPE_ID = om.MTypeId(0x0007F7FD)
    DRAW_CLASSIFICATION = "drawdb/geometry/distancebetweenlocator"
    DRAW_REGISTRANT_ID = "DistanceBetweenLocator"


    point1_obj = None
    point2_obj = None
    distance_obj = None


    def __init__(self):
        super(DistanceBetweenLocator, self).__init__()
    
    def compute(self, plug, data):
        point1 = om.MPoint(data.inputValue(self.point1_obj).asFloatVector()) # 得到MPoint对象
        point2 = om.MPoint(data.inputValue(self.point2_obj).asFloatVector())


        distance = point1.distanceTo(point2) # 使用MPoint的计算距离的方法


        data.outputValue(self.distance_obj).setDouble(distance)


        data.setClean(plug) # 使plug变成干净的状态


    @classmethod
    def creator(cls):
        return DistanceBetweenLocator()


    @classmethod
    def initialize(cls):
        numeric_attr = om.MFnNumericAttribute()


        cls.point1_obj = numeric_attr.createPoint("point1", "p1")
        numeric_attr.readable = False
        numeric_attr.keyable = True


        cls.point2_obj = numeric_attr.createPoint("point2", "p2")
        numeric_attr.readable = False
        numeric_attr.keyable = True


        cls.distance_obj = numeric_attr.create("distance", "dist", om.MFnNumericData.kDouble, 0.0)
        numeric_attr.writable = False


        cls.addAttribute(cls.point1_obj)
        cls.addAttribute(cls.point2_obj)
        cls.addAttribute(cls.distance_obj)


        cls.attributeAffects(cls.point1_obj, cls.distance_obj)
        cls.attributeAffects(cls.point2_obj, cls.distance_obj)


class DistanceBetweenUserData(om.MUserData):


    def __init(self, deleteAfterUse = False):
        super(DistanceBetweenUserData, self).__init__(deleteAfterUse)


        self.distance = 0
        self.point1 = om.MPoint()
        self.point2 = om.MPoint()


class DistanceBetweenDrawOverride(omr.MPxDrawOverride):
    """ 负责在视口中绘制几何图形 """
    NAME = "DistanceBetweenDrawOverride"


    def __init__(self, obj):
        super(DistanceBetweenDrawOverride, self).__init__(obj, None, False) # 第一个参数是maya object,第二个参数是绘制是callback函数,第三个参数是默认为True,为True时将会将此标志位dirty状态，因此可以持续更新,建议为True,除非遇到了性能问题可以为False


    def refineSelectionPath(self, select_info, hit_item, path, components, obj_mask):
        """ 重新定义选择，使绘制的几何图形不能够被选中 """
        return False


    def supportedDrawAPIs(self):
        """ 让maya知道支持哪个图形api,kAllDevices指的是使用OpenGL and Direct X 11"""
        return omr.MRenderer.kAllDevices


    def hasUIDrawables(self):
        """ 表示使用addUIDrawables方法来绘制图形 """
        return True


    def prepareForDraw(self, obj_path, camera_path, frame_context, old_data):
        """ 在使用绘制图形的方法之前,使用这个方法来将数据检索与缓存 """
        data = old_data
        if not data:
            data = DistanceBetweenUserData()


        node_fn = om.MFnDependencyNode(obj_path.node())


        data.point1 = om.MPoint(node_fn.findPlug("point1X", False).asDouble(),
                                node_fn.findPlug("point1Y", False).asDouble(),
                                node_fn.findPlug("point1Z", False).asDouble())


        data.point2 = om.MPoint(node_fn.findPlug("point2X", False).asDouble(),
                                node_fn.findPlug("point2Y", False).asDouble(),
                                node_fn.findPlug("point2Z", False).asDouble())


        data.distance = node_fn.findPlug("distance", False).asDouble()
        
        return data


    def addUIDrawables(self, obj_path, draw_manager, frame_context, data):
        """ 绘制图形的方法


        Args:
            obj_path (_type_): 指向正在绘制的对象的路径,这里是指locator节点
            draw_manager (_type_): 用于绘制简单的几何图形
            frame_context (_type_): 包含当前渲染框架的一些全局信息
            data (_type_): 用户创建的数据对象,存储缓存数据
        """
        draw_manager.beginDrawable()
        
        draw_manager.setFontSize(14)
        draw_manager.setFontWeight(100)
        draw_manager.setColor(om.MColor((1.0, 0.5, 0.5)))


        pos = om.MPoint((om.MVector(data.point1) + om.MVector(data.point2))/2.0) # 得到两点之间的重点
        text = "{0:.3f}".format(data.distance)


        draw_manager.text(pos, text, omr.MUIDrawManager.kCenter)
        draw_manager.line(data.point1,data.point2)


        draw_manager.endDrawable()


    @classmethod
    def creator(cls, obj):
        return DistanceBetweenDrawOverride(obj)



def initializePlugin(plugin):
    """ 插件加载时执行这个函数"""
    vendor = "RuiChen"  # 插件制作人的名字
    version = "1.0.0"  # 插件的版本


    plugin_fn = om.MFnPlugin(plugin, vendor, version)  # 定义插件
    try:
        plugin_fn.registerNode(DistanceBetweenLocator.TYPE_NAME,
                               DistanceBetweenLocator.TYPE_ID,
                               DistanceBetweenLocator.creator,
                               DistanceBetweenLocator.initialize,
                               om.MPxNode.kLocatorNode,
                               DistanceBetweenLocator.DRAW_CLASSIFICATION)
    except:
        om.MGlobal.displayError("Failed to register node: {0}".format(DistanceBetweenLocator.TYPE_NAME))


    try:
        omr.MDrawRegistry.registerDrawOverrideCreator(DistanceBetweenLocator.DRAW_CLASSIFICATION,
                                                      DistanceBetweenLocator.DRAW_REGISTRANT_ID,
                                                      DistanceBetweenDrawOverride.creator)
    except:
        om.MGlobal.displayError("Failed to register draw override: {0}".format(DistanceBetweenDrawOverride.NAME))



def uninitializePlugin(plugin):
    """ 插件取消加载时执行这个函数"""
    plugin_fn = om.MFnPlugin(plugin)
    try:
        omr.MDrawRegistry.deregisterDrawOverrideCreator(DistanceBetweenLocator.DRAW_CLASSIFICATION,
                                                        DistanceBetweenLocator.DRAW_REGISTRANT_ID)
    except:
        om.MGlobal.displayError("Failed to deregister draw override: {0}".format(DistanceBetweenDrawOverride.NAME))


    try:
        plugin_fn.deregisterNode(DistanceBetweenLocator.TYPE_ID)
    except:
        om.MGlobal.displayError("Failed to deregister node: {0}".format(DistanceBetweenLocator.TYPE_NAME))


def rc_distance_between_test():
    cmds.setAttr("persp.translate", 3.5, 5.5, 10.0)
    cmds.setAttr("persp.rotate", -27.0, 19.0, 0.0)


    cube1 = cmds.polyCube()[0]
    cube2 = cmds.polyCube()[0]


    cmds.setAttr("{0}.translateX".format(cube1), -2.5)
    cmds.setAttr("{0}.translateX".format(cube2), 2.5)


    distance_locator = cmds.createNode("{0}".format(DistanceBetweenLocator.TYPE_NAME))


    cmds.connectAttr("{0}.translate".format(cube1),"{0}.point1".format(distance_locator))
    cmds.connectAttr("{0}.translate".format(cube2),"{0}.point2".format(distance_locator))


    cmds.select(distance_locator)





if __name__ == '__main__':


    cmds.file(new=True, force=True)


    """ 注册后,在maya脚本编辑器中的使用方法 """
    plugin_name = "distance_between_locator.py"  # 插件的文件名
    # 如果插件加载了就先取消加载插件
    cmds.evalDeferred('if cmds.pluginInfo("{0}", q=True, loaded=True): cmds.unloadPlugin("{0}")'.format(plugin_name))
    # 如果插件没有加载就加载插件
    cmds.evalDeferred('if not cmds.pluginInfo("{0}", q=True, loaded=True): cmds.loadPlugin("{0}")'.format(plugin_name))


    cmds.evalDeferred('rc_distance_between_test()')
```

<a name="bhu4x"></a>
### 设置自定义变形器节点在大纲处的图标以及节点编辑器中的图标

默认图标：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670915721160-2897f85d-23d1-4da0-b908-073f4a498ad3.png#averageHue=%234a4947&clientId=uaca77ae3-2815-4&from=paste&height=224&id=u00e4ba98&originHeight=202&originWidth=435&originalType=binary&ratio=1&rotation=0&showTitle=false&size=44175&status=done&style=none&taskId=u5efe4482-dfd4-46b5-b713-a5709e88b68&title=&width=483.3333461372944)<br />设置自定义图标：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670915626186-0dedd648-4117-4033-996f-d3cfebeaa7d8.png#averageHue=%23f4f0f0&clientId=uaca77ae3-2815-4&from=paste&height=309&id=u55d6291d&originHeight=278&originWidth=2056&originalType=binary&ratio=1&rotation=0&showTitle=false&size=146769&status=done&style=none&taskId=u430907cc-fccc-4cdb-8475-9e8c16155a4&title=&width=2284.444504961557)


![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670915685735-9cbb3ab8-60ee-425f-aaee-64bd6043d88a.png#averageHue=%23373636&clientId=uaca77ae3-2815-4&from=paste&height=586&id=ue61cf00e&originHeight=527&originWidth=1561&originalType=binary&ratio=1&rotation=0&showTitle=false&size=134322&status=done&style=none&taskId=u941b3c90-01ba-41f8-852b-0fe57b00d77&title=&width=1734.4444903915323)

<a name="ICWzV"></a>
### 自定义节点属性编辑器的排列模板
名字格式： AE + 节点名字 + Template<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1670998413353-26d9a2c7-905a-41a8-8014-f8856a348242.png#averageHue=%23fcfbfb&clientId=uaca77ae3-2815-4&from=paste&height=160&id=u7cf72e1c&originHeight=144&originWidth=841&originalType=binary&ratio=1&rotation=0&showTitle=false&size=10569&status=done&style=none&taskId=udaaeb6d3-9808-4518-94f7-a4de82fc5ed&title=&width=934.4444691987692)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671002285775-651ec0d7-129b-498e-8b3d-73b7059bb024.png#averageHue=%23413f3f&clientId=uaca77ae3-2815-4&from=paste&height=910&id=uedf888c6&originHeight=819&originWidth=2682&originalType=binary&ratio=1&rotation=0&showTitle=false&size=197038&status=done&style=none&taskId=ua342705b-c5da-4f06-ab25-1d2ed2f6eb9&title=&width=2980.000078943043)
```python
// distanceBetweenLocator节点在属性编辑器中的模板
// 在mel中不需要在意缩进，这里的缩进只是为了排版更好看而已
global proc AEdistanceBetweenLocatorTemplate(string $nodeName)
{
    editorTemplate -beginScrollLayout;
        
        editorTemplate -beginLayout "Distance Between Attributes" -collapse 0; //collapse 意思是展开，不折叠

            editorTemplate -addControl "point1";
            editorTemplate -addControl "point2";
            editorTemplate -addControl "minDistance";
            editorTemplate -addControl "maxDistance";

            AEaddRampControl($nodeName + ".colorRamp");
            AEaddRampControl($nodeName + ".curveRamp");

        editorTemplate -endLayout;

    editorTemplate -addExtraControls;
    editorTemplate -endScrollLayout;
}
// 刷新属性编辑器，便于快速看到代码改变带来的影响
refreshEditorTemplates; 
```
<a name="GS9oN"></a>
## 如何将单一功能的插件组合起来
之前的教程写插件都是写一个节点，命令，工具，但是一个插件功能往往包含这几个而不是单一的。因此这节课讲如何将它们组合起来。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671002908082-7d4cacc1-e487-44ba-a7ae-efa738c0738c.png#averageHue=%234e4d4d&clientId=uaca77ae3-2815-4&from=paste&height=589&id=u572c52c2&originHeight=530&originWidth=1056&originalType=binary&ratio=1&rotation=0&showTitle=false&size=258887&status=done&style=none&taskId=uf636dc9d-f8a2-44cd-a42e-cc119c2e58d&title=&width=1173.3333644160525)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671003972925-52e4ee7b-8749-49f0-a5c4-adf90b440a2a.png#averageHue=%232f2c29&clientId=uaca77ae3-2815-4&from=paste&height=783&id=u57719ee8&originHeight=705&originWidth=602&originalType=binary&ratio=1&rotation=0&showTitle=false&size=223814&status=done&style=none&taskId=u04d1646a-4660-41f1-b5e9-e78ae8f70e4&title=&width=668.8889066083937)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671004010290-e78014d7-5d18-4628-9c7c-5bcb91bddfcf.png#averageHue=%23212121&clientId=uaca77ae3-2815-4&from=paste&height=1046&id=ua9ae1ad0&originHeight=941&originWidth=1536&originalType=binary&ratio=1&rotation=0&showTitle=false&size=727699&status=done&style=none&taskId=u5f75e573-ad72-446a-996c-86981f697d1&title=&width=1706.6667118778946)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671004083035-035c41b0-5c84-4647-a8a4-f3caf7bc457d.png#averageHue=%23302d2a&clientId=uaca77ae3-2815-4&from=paste&height=487&id=uec481016&originHeight=438&originWidth=1467&originalType=binary&ratio=1&rotation=0&showTitle=false&size=313778&status=done&style=none&taskId=u289682d5-d3e7-4138-a0d0-3e070a43529&title=&width=1630.0000431802548)
<a name="Z0mEb"></a>
## 如何将文件功能分成多个文件使其更方便管理
[21_multifile_plugins_part1_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1ye4y1r7Yv?p=22&vd_source=b1de3fe38e887eb40fc55a5485724480)

<a name="NaikZ"></a>
## maya_modules
maya的module是一种共享多文件插件的方法
<a name="KygeB"></a>
### 简单的插件管理方式
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671085566693-242de11c-b079-407b-9ad9-b5629e1f57b7.png#averageHue=%23090909&clientId=uc9db9e09-998d-4&from=paste&height=474&id=u10ec219a&originHeight=999&originWidth=2302&originalType=binary&ratio=1&rotation=0&showTitle=false&size=446960&status=done&style=none&taskId=u14d3c7bc-c9b8-440e-a906-3239120e487&title=&width=1091.77783203125)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671085583642-e0336d04-41a2-4b39-86d4-5e935f755935.png#averageHue=%230a0a09&clientId=uc9db9e09-998d-4&from=paste&height=566&id=ua342f8b0&originHeight=960&originWidth=1313&originalType=binary&ratio=1&rotation=0&showTitle=false&size=74945&status=done&style=none&taskId=u51d14b57-8c0c-4c1e-a609-cc750826055&title=&width=773.885498046875)
<a name="LqOTk"></a>
### maya moudules的介绍

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671085676299-c57674c6-1f6f-4ee5-bcc2-60bd6e0a6fb0.png#averageHue=%230b0b0b&clientId=uc9db9e09-998d-4&from=paste&height=705&id=u5180ec1e&originHeight=1209&originWidth=2391&originalType=binary&ratio=1&rotation=0&showTitle=false&size=773548&status=done&style=none&taskId=uff00fa39-30b7-45ff-8814-4fb583a9506&title=&width=1393.666748046875)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671085698913-02ec178c-e03e-497d-a604-646e22f7edaa.png#averageHue=%23070706&clientId=uc9db9e09-998d-4&from=paste&height=499&id=uf3e91b3f&originHeight=992&originWidth=2166&originalType=binary&ratio=1&rotation=0&showTitle=false&size=107701&status=done&style=none&taskId=uf1ae4133-dc3a-49d9-b7ee-c0c722fb84a&title=&width=1089.6597900390625)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671085897512-879e9245-c9c2-4791-94ce-b97e769f6dea.png#averageHue=%23070707&clientId=uc9db9e09-998d-4&from=paste&height=546&id=ubbe1b506&originHeight=1160&originWidth=2317&originalType=binary&ratio=1&rotation=0&showTitle=false&size=501083&status=done&style=none&taskId=u51a1f977-673d-4d3a-8e2e-16257618636&title=&width=1090.4410400390625)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671085945440-91ba49c0-e5cc-4915-9a7c-0f8ec2202152.png#averageHue=%23060505&clientId=uc9db9e09-998d-4&from=paste&height=544&id=uc781249b&originHeight=490&originWidth=623&originalType=binary&ratio=1&rotation=0&showTitle=false&size=29185&status=done&style=none&taskId=ud20ce58b-f589-4c12-8bbe-b547c32c8fa&title=&width=692.2222405598492)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671086048276-89436e5a-f14e-4519-92c2-a82765897eef.png#averageHue=%23090909&clientId=uc9db9e09-998d-4&from=paste&height=614&id=u51148265&originHeight=1105&originWidth=2370&originalType=binary&ratio=1&rotation=0&showTitle=false&size=632215&status=done&style=none&taskId=ub78af419-6f55-40f7-9388-0486ff38c2c&title=&width=1317.33349609375)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671086097304-6d550613-068b-4541-9834-6b6a98e53b59.png#averageHue=%23100e0d&clientId=uc9db9e09-998d-4&from=paste&height=72&id=u65a6db8a&originHeight=65&originWidth=1018&originalType=binary&ratio=1&rotation=0&showTitle=false&size=12774&status=done&style=none&taskId=u13033f6e-a119-483f-8afa-1f1c19ccce7&title=&width=1131.1111410753235)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671086196037-6f4c580e-9d75-4d11-8bfa-74c19b3eaee4.png#averageHue=%23080808&clientId=uc9db9e09-998d-4&from=paste&height=509&id=u78836d3d&originHeight=957&originWidth=2394&originalType=binary&ratio=1&rotation=0&showTitle=false&size=491507&status=done&style=none&taskId=u7fffcc80-71f5-49fd-ae0c-1d322634ce6&title=&width=1274.000244140625)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671086210447-0fb7c8df-8a81-42d0-b2b9-9a1837e43ae5.png#averageHue=%23100f0d&clientId=uc9db9e09-998d-4&from=paste&height=91&id=uc3b16ff9&originHeight=82&originWidth=1103&originalType=binary&ratio=1&rotation=0&showTitle=false&size=14596&status=done&style=none&taskId=u29092a1d-5a81-46ef-b3f9-cc91b458fcb&title=&width=1225.5555880216914)
<a name="xPeit"></a>
### 使用创建moudules的步骤举例
<a name="Wywr1"></a>
#### 一个工具的所需内容放到一个文件夹里，在这个文件夹下创建一个mod文件
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671086906525-ecf3a55b-7fb2-45f8-970e-74b5a0e78433.png#averageHue=%23f6f0ee&clientId=uc9db9e09-998d-4&from=paste&height=258&id=u4b1ffb67&originHeight=232&originWidth=498&originalType=binary&ratio=1&rotation=0&showTitle=false&size=40431&status=done&style=none&taskId=u9ceb672d-5a22-4b0b-83ba-a0792fe994f&title=&width=553.3333479916612)

<a name="CEzh9"></a>
#### mod文件夹下添加这个工具
最后的./是相对路径<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671087583273-798c1a11-2f9a-4962-b7f4-64d87267d22f.png#averageHue=%231c1c1b&clientId=uc9db9e09-998d-4&from=paste&height=130&id=udbd71950&originHeight=117&originWidth=426&originalType=binary&ratio=1&rotation=0&showTitle=false&size=22000&status=done&style=none&taskId=u3fd26225-2368-4abe-a127-880bb47af8b&title=&width=473.3333458723849)

<a name="HHsqn"></a>
#### 在maya.env文件下添加mod：
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671087574805-d58f52d1-d084-47ae-9b85-13f2c55c7582.png#averageHue=%23fbfaf9&clientId=uc9db9e09-998d-4&from=paste&height=341&id=u16c56c7c&originHeight=307&originWidth=998&originalType=binary&ratio=1&rotation=0&showTitle=false&size=113257&status=done&style=none&taskId=u31848ebf-4e7b-411a-8224-e8cbbcac93e&title=&width=1108.8889182644134)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671087635395-42e2c798-9bc5-4375-a4e2-607c9f3a01b4.png#averageHue=%232a2625&clientId=uc9db9e09-998d-4&from=paste&height=286&id=u2a3ea13a&originHeight=257&originWidth=1176&originalType=binary&ratio=1&rotation=0&showTitle=false&size=163738&status=done&style=none&taskId=u64e5efb4-58b1-4f8f-8899-18ca8aaae3f&title=&width=1306.666701281513)
<a name="eq346"></a>
#### 检查工作
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671087702883-c89e5cb5-b753-4e3a-a0b8-7b846180b311.png#averageHue=%232a2a2a&clientId=uc9db9e09-998d-4&from=paste&height=194&id=u97c8351c&originHeight=175&originWidth=886&originalType=binary&ratio=1&rotation=0&showTitle=false&size=63681&status=done&style=none&taskId=u3904e6b9-7b09-488c-a7f5-7032e9edb68&title=&width=984.4444705233169)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1671087721464-4de9fa78-8fde-4dd4-8ecd-041f13c2e409.png#averageHue=%23747470&clientId=uc9db9e09-998d-4&from=paste&height=230&id=udf99d51b&originHeight=207&originWidth=262&originalType=binary&ratio=1&rotation=0&showTitle=false&size=46299&status=done&style=none&taskId=ue653480e-135e-44db-b10b-b1a737c00b5&title=&width=291.11111882292215)
