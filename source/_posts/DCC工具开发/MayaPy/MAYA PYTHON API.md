---
title: MAYA PYTHON API
tags: MayaPy
categories: DCC工具开发
abbrlink: 22a450bf
date: 2023-08-29 03:57:00
---
<meta name="referrer" content="no-referrer" />

<a name="hWfDw"></a>
# 第二集面向对象编程
<a name="Yl4GV"></a>
## 类，对象和模块。
类是一个蓝图，是一个数据的集合，根据类创建对象，也可以称为类的实例化，对象是基于类的结构的数据的集合，模块是类的集合。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1652688002940-a1974267-22d9-495d-aae0-641008d06936.png#averageHue=%23040404&clientId=ubc9b0c79-7263-4&from=paste&height=1053&id=ua1bf780d&originHeight=1053&originWidth=1896&originalType=binary&ratio=1&rotation=0&showTitle=false&size=328742&status=done&style=none&taskId=ubd677c03-9488-44b0-b709-4d689dfc8d4&title=&width=1896)
<a name="nk7Xj"></a>
# 第三集maya api 术语
<a name="cr2uH"></a>
## dag path
<a name="ziLh0"></a>
### dag=directed acyclic graph有向非循环图
树是一种很典型的有向非循环图<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1652699596042-6aaeb4ab-9afb-4154-9f27-c3d15287b097.png#averageHue=%23060606&clientId=ubc9b0c79-7263-4&from=paste&height=329&id=udd3d31e2&originHeight=329&originWidth=698&originalType=binary&ratio=1&rotation=0&showTitle=false&size=39256&status=done&style=none&taskId=u2f0e2232-493a-4e6d-9f27-b3da2a3a2de&title=&width=698)<br />在maya中创建的物体对象，具有两个节点，一个transform节点，一个shape节点，transform节点定义了变换（xyz位置）旋转，缩放，shape节点定义了物体的形状。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1652700326243-a5174551-88c6-4b61-a5be-9c91ae4b756b.png#averageHue=%23090909&clientId=ubc9b0c79-7263-4&from=paste&height=400&id=ua142ac27&originHeight=400&originWidth=627&originalType=binary&ratio=1&rotation=0&showTitle=false&size=52300&status=done&style=none&taskId=ub30c642c-09d7-4316-b567-c565d99ccf5&title=&width=627)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1652699848427-f10df377-7b87-40d1-b448-740740d1bed3.png#averageHue=%23101010&clientId=ubc9b0c79-7263-4&from=paste&height=397&id=u35dfc191&originHeight=397&originWidth=748&originalType=binary&ratio=1&rotation=0&showTitle=false&size=112043&status=done&style=none&taskId=u55df21c1-19d8-4749-b465-aeceb855cd0&title=&width=748)
<a name="JVrip"></a>
### dg=dependency graph依赖图
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1652700312066-20bf1573-864e-49b4-906e-e7fc57d46b41.png#averageHue=%23080808&clientId=ubc9b0c79-7263-4&from=paste&height=346&id=ud8cb707e&originHeight=346&originWidth=653&originalType=binary&ratio=1&rotation=0&showTitle=false&size=51000&status=done&style=none&taskId=u4f18b9f5-0a11-4d9f-b917-739e87b87d3&title=&width=653)

<a name="awTOD"></a>
### dag path
dag path是从根到特定对象的路径，没有dag path，maya就不知道那个特定对象在世界空间的哪里。<br />因为当一个物体是另一个物体的子物体时，它的原点坐标就会变成它的父物体的当前坐标位置。<br />maya是通过dag path获得这些位置的。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1652700814965-59307fc8-d171-42b0-8471-16a9f2da22b6.png#averageHue=%23050505&clientId=ubc9b0c79-7263-4&from=paste&height=685&id=uf368ccf8&originHeight=685&originWidth=1111&originalType=binary&ratio=1&rotation=0&showTitle=false&size=110716&status=done&style=none&taskId=ue6ff3450-0403-4c8f-979b-2f5622f4e73&title=&width=1111)

<a name="kLYbE"></a>
## MObject
MObject是model object的缩写 <br />MObject是可以访问maya的专门的处理程序，可以用来处理模型，渲染，灯光 <br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1652701657933-aff5a074-7a3d-4857-955d-34da4aa497b4.png#averageHue=%23080808&clientId=ubc9b0c79-7263-4&from=paste&height=573&id=u1f4a393f&originHeight=573&originWidth=533&originalType=binary&ratio=1&rotation=0&showTitle=false&size=65804&status=done&style=none&taskId=ua4265d9a-8176-4364-8418-075524338bd&title=&width=533)
<a name="NyMMB"></a>
## Selection List
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1652701682100-5b20f116-3eca-4d78-9a4c-94259c9a79c9.png#averageHue=%23070707&clientId=ubc9b0c79-7263-4&from=paste&height=1044&id=u590c24db&originHeight=1044&originWidth=812&originalType=binary&ratio=1&rotation=0&showTitle=false&size=157832&status=done&style=none&taskId=u57ad142d-da2c-4b90-b4cc-a1122ade833&title=&width=812)<br />方法有creating、add/remove、walking(遍历)等
<a name="bxYhz"></a>
## 案例![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1652704537426-f82d807a-e19f-4c62-aba3-3f9849253f2c.png#averageHue=%23060606&clientId=ubc9b0c79-7263-4&from=paste&height=947&id=u401852d7&originHeight=947&originWidth=1761&originalType=binary&ratio=1&rotation=0&showTitle=false&size=301614&status=done&style=none&taskId=ubbea4c4f-b64f-402a-afc9-f7614c69240&title=&width=1761)
说明：首先创建一个mSelectionList对象（mselectionList）（第一行），将obj放入到0的位置（第二行），然后创建一个mdagPath对象（mdagPath）（目前是空的）（第三行），然后将mSelectionList对象中的索引为0的obj的dagpath放入到MDagPath对象（mdagPath）中（现在mdagPath对象中拥有了obj的dagpath）（第四行），创建一个MObject对象（第五行），获得mSelectionList中索引为0的obj中的依赖节点给MObject对象（mobj）。<br />看那个手的图案下面有个obj我想大概意思是将obj对象与MObject对象建立关系，理解为指针就可以了。

**这里的pPlane1为maya中的模型名字**
```python
import maya.OpenMaya as OpenMaya

# 创建一个 Selection List
mSel = OpenMaya.MSelectionList()
mSel.add("pPlane1")
# 创建MObject和MDagPath
mObj = OpenMaya.MObject()
mDagPath = OpenMaya.MDagPath()
# 得到对象的依赖节点和dagpath
mSel.getDependNode(0,mObj)
mSel.getDagPath(0,mDagPath)

print mDagPath.fullPathName()
```
<a name="pumb7"></a>
# 第四集获取和更改场景物体的属性
<a name="EvmY2"></a>
## 先了解节点属性
例如创建一个平面，节点连接关系图如图所示：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653139370624-f7b45cda-1cca-4a78-a530-77f88d8264c0.png#averageHue=%231b1b1a&clientId=u2d7ef19d-2bd1-4&from=paste&height=139&id=ued529cf0&originHeight=139&originWidth=645&originalType=binary&ratio=1&rotation=0&showTitle=false&size=5563&status=done&style=none&taskId=ub5ab0927-cd65-4bfe-8636-7584c31e34e&title=&width=645)<br />然后双击黄色的线就弹出窗口这样就可以进行左边的属性与右边的属性进行连接![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653139420841-46b474e3-b2a1-4720-8b4d-6c66e15ac04f.png#averageHue=%23474746&clientId=u2d7ef19d-2bd1-4&from=paste&height=659&id=u88fda29a&originHeight=659&originWidth=536&originalType=binary&ratio=1&rotation=0&showTitle=false&size=40552&status=done&style=none&taskId=ubb4ba258-9610-434f-8f44-5611fe018de&title=&width=536)。
<a name="SVPTp"></a>
## MFnMesh
首先需要理解一下什么是MFn，MFn是model function  set 的缩写意思是模型函数集（函数集是函数的集合的意思）。<br />然后MFnMesh接受一个网格类型，然后可以执行创建，修改， 更改边，面，细分等方法<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653118356724-e388e6ea-ccd6-4d22-a66c-4d01885434a9.png#averageHue=%23080808&clientId=ub0d197af-217a-4&from=paste&height=550&id=u6ac57003&originHeight=550&originWidth=451&originalType=binary&ratio=1&rotation=0&showTitle=false&size=63501&status=done&style=none&taskId=uf26cc2ed-a649-45fd-a97b-44a8b5d4376&title=&width=451)
<a name="pDlxZ"></a>
## MFnDependencyNode
MFnDependencyNode有创建修改检索等功能 针对的是dependency graph,接受的是dependency node 类型<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653119744005-205832c4-b0cf-4cdd-a82e-b82b2088d0a9.png#averageHue=%23070707&clientId=ub0d197af-217a-4&from=paste&height=485&id=uf8b1b4b8&originHeight=485&originWidth=544&originalType=binary&ratio=1&rotation=0&showTitle=false&size=63258&status=done&style=none&taskId=u0d6260aa-5617-45f5-9fbd-995ed5ea16c&title=&width=544)
<a name="MPqKm"></a>
## MFnMesh和MFnDependencyNode接受的输入
它们接受的输入通常是MObject或者MDagPath（可以通过看官方文档查询）<br />这个上面的英语是 inputs to function set<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653137067965-99a6adbe-533c-49a1-9aab-45316b42eb99.png#averageHue=%23050505&clientId=u2d7ef19d-2bd1-4&from=paste&height=312&id=udc0ddb8b&originHeight=312&originWidth=584&originalType=binary&ratio=1&rotation=0&showTitle=false&size=33457&status=done&style=none&taskId=ubb669d48-c9d7-442c-9284-6246761f329&title=&width=584)<br />MFnMesh接受的输入是MObject或者MDagPath![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653137271876-e14e18bb-d4a4-4f32-adee-455bc9712134.png#averageHue=%23c0c4c3&clientId=u2d7ef19d-2bd1-4&from=paste&height=445&id=u8052b4e0&originHeight=445&originWidth=1811&originalType=binary&ratio=1&rotation=0&showTitle=false&size=443192&status=done&style=none&taskId=ud5c4c03c-743b-4b21-b9d3-07ee7e09333&title=&width=1811)<br />而MFnDependencyNode能接受的输入只有MObject![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653137320474-2d3143dd-78b9-4eb8-8976-148f0ed3c518.png#averageHue=%23ebeeee&clientId=u2d7ef19d-2bd1-4&from=paste&height=466&id=u270af4c1&originHeight=466&originWidth=1757&originalType=binary&ratio=1&rotation=0&showTitle=false&size=484057&status=done&style=none&taskId=ucfd650f7-fa6e-444d-83c6-801daa12f3e&title=&width=1757)<br />CSDN上的一些知识点：<br />API文档的坑：MStatus(其实是很多人没仔细看文档的锅……)<br />如果在学习python api前没有认真看过maya官方文档的相关文档，就会对api文档中的mstatus感觉困惑，这个东西是嘛，我们怎么用，为什么到处都是。我就说一句：api方法中的mstatus，你用python时候就当它不存在！是的，就是无视，这设计到maya软件的整体设计问题。Maya中的程序异常处理是使用的status code而非exception(早年C++异常处理的锅，大家都不敢用，吃性能还不讨好，但是现在maya想换也做不到了，历史包袱严重)，也就是说本身需要语言处理的事情，maya的系统自行设计了一套处理机制，而异常的消息传递，就是靠的status code，也就是mstatus，这也是maya api中mstatus无处不在的原因。但是python不需要啊！Python有完备的异常处理机制，干嘛用status code。所以python api就没有mstatus，我们也就不需要管它。


<a name="X0Jlh"></a>
## MPlug与MPlugArray
通过观看视频我理解的plug的意思应该就是模型对象的属性，分两种类型<br />network plug ： dependency node plug   意思是在DG中建立连接的属性<br />non-network plug ： user-defined plug 意思应该是用户自定义的属性，还没有建立连接。<br />看这里，一个节点有多种属性，然后如果我们要操控这些属性，需要通过这个手图案来管理属性，进行创建修改访问的操作。handle 代表了属性名字例如weight，height，subdivisionsWidth<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653139225937-9f5b0179-954e-42cf-bd38-157e612cb4d3.png#averageHue=%230b0b0b&clientId=u2d7ef19d-2bd1-4&from=paste&height=195&id=u458fb14d&originHeight=195&originWidth=304&originalType=binary&ratio=1&rotation=0&showTitle=false&size=23208&status=done&style=none&taskId=ub704ddab-6500-407a-bf78-1b5936dbd41&title=&width=304)<br />理解了plug的意思后，接下来理解plug array的意思：<br />plug array通过看了视频我理解的是：<br />一个节点的**plug array 是一个列表**，列表中存在着这个节点的所有连接，包括输入和输出。<br />例如pPlaneShape1的输入 pPlaneShpae1.inMesh是plug array中的一个值。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653139633802-5ace5d83-d835-45c6-b22f-32bb9fbf58b3.png#averageHue=%2358492a&clientId=u2d7ef19d-2bd1-4&from=paste&height=80&id=ucb03fadf&originHeight=80&originWidth=444&originalType=binary&ratio=1&rotation=0&showTitle=false&size=4719&status=done&style=none&taskId=ubff743ef-c8d3-4e18-8d37-dcd2238c6f3&title=&width=444)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653122997614-17c2ac9e-49e9-4153-aed1-2592f3e2f451.png#averageHue=%23040404&clientId=ub0d197af-217a-4&from=paste&height=837&id=u2f180fa3&originHeight=837&originWidth=1434&originalType=binary&ratio=1&rotation=0&showTitle=false&size=187902&status=done&style=none&taskId=udaedd2c0-2bde-4cb1-a2d5-946cb2d89f4&title=&width=1434)

<a name="F1xhz"></a>
## 案例
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653124553672-713aa0a8-831d-460a-b959-c45bf4d001d6.png#averageHue=%231b1a19&clientId=ub0d197af-217a-4&from=paste&height=700&id=DitNZ&originHeight=700&originWidth=1425&originalType=binary&ratio=1&rotation=0&showTitle=false&size=168236&status=done&style=none&taskId=u660f4a87-8fc5-4f47-a1bb-0a7d5ad6dce&title=&width=1425)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1669968246970-4e2f1fe8-5b2c-49d6-982f-0b388c7e14eb.png#averageHue=%23474746&clientId=u2cf0e87e-69bf-4&from=paste&height=481&id=ud3560693&originHeight=433&originWidth=1035&originalType=binary&ratio=1&rotation=0&showTitle=false&size=49763&status=done&style=none&taskId=u5d6b96d6-87f4-4716-876d-c28742f5fd5&title=&width=1150.000030464597)

```python
import maya.OpenMaya as OpenMaya

# 1.创建一个 Selection List并将场景物体添加至SelectionList
mSel = OpenMaya.MSelectionList()
mSel.add("pPlane1")
# 2.创建MObject和MDagPath
mObj = OpenMaya.MObject() # 创建一个空的mObj
mDagPath = OpenMaya.MDagPath()
# 3.得到对象的依赖节点和dag路径
mSel.getDependNode(0,mObj)
mSel.getDagPath(0,mDagPath)
print mDagPath.fullPathName() # 输出|pPlane1
# 4.Mesh function set 获得网格函数集
mFnMesh = OpenMaya.MFnMesh(mDagPath)
print mFnMesh.fullPathName() # 输出|pPlane1|pPlaneShape1
# 5.Dependency Node function set 获得依赖节点函数集
mFnDependNode = OpenMaya.MFnDependencyNode(mObj)
print mFnDependNode.name() # 输出pPlane1,pPlane1是模型的transform节点,它不需要dagpath因此只需要使用name方法就可以了
# 6.获取shape节点的所有连接
mPlugArray = OpenMaya.MPlugArray() # 创建一个MPlugArray对象来管理shape节点的输入输出
mFnMesh.getConnections(mPlugArray) 
mPlugArray.length() # 输出pPlaneShape1节点的连接个数 2
print mPlugArray[0].name() # 输出pPlaneShape1.instObjGroups[0] 它是shape节点的输出
print mPlugArray[1].name() # 输出pPlaneShape1.inMesh 它是shape节点的输入

mPlugArray2 = OpenMaya.MPlugArray() # 再创建一个MPlugArray对象来管理用来polyPlane节点的输入输出
mPlugArray[1].connectedTo(mPlugArray2,True,False) # 寻找mPlugArray[1]为目标的所有plug并存入mPlugArray2中，True，False意思是目标为True，源为False，意思是mPlugArray[1]是下游，不是上游
print mPlugArray2.length() # 输出1
# 不能使用：len(mPlugArray2)

print mPlugArray2[0].name() # 输出polyPlane1.output

mObj2 = mPlugArray2[0].node() # 得到MObject类型指向polyPlane1

mFnDependNode2 = OpenMaya.MFnDependencyNode(mObj2) # 为polyPlane1创建节点对象函数集
print mFnDependNode2.name() # 输出polyPlane1

mPlug_width = mFnDependNode2.findPlug("width") # 找到polyPlane1的width属性
mPlug_height = mFnDependNode2.findPlug("height") # 找到polyPlane1的height属性

print mPlug_width.asInt() # 输出polyPlane1的width的值
print mPlug_height.asInt() # 输出polyPlane1的height的值

mPlug_subWidth = mFnDependNode2.findPlug("subdivisionsWidth") # 找到polyPlane1的subdivisionsWidth属性
mPlug_subHeight = mFnDependNode2.findPlug("subdivisionsHeight") # # 找到polyPlane1的subdivisionsHeight属性
mPlug_subWidth.setInt(10) # 设置subdivisionsWidth值为10
mPlug_subHeight.setInt(10) # 设置subdivisionHeight值为10

print mPlug_subWidth.asInt() # 得到mPlug_subWidth的整数值并输出
print mPlug_subHeight.asInt() # 得到mPlug_subHeight的整数值并输出



```

<a name="WBcTy"></a>
# 第五集 命令通信流
**编写命令插件有三个重要的事情**<br />1、function 函数<br />2、initialization 初始化  /  registration 注册<br />3、 Un-initialization 取消初始化/ De-registration取消注册<br />**什么是initialization/registration，什么是Un-initialization/De-registration？**<br />给maya core发送内容叫initialization或者叫registration<br />从maya core 移除内容叫Un-initialization或者叫De-registration<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654567983120-7ae8bca6-3bc4-41ff-9d0b-3e9f64abd33f.png#averageHue=%23070707&clientId=ua5a358c9-400c-4&from=paste&height=542&id=u04d779ec&originHeight=542&originWidth=557&originalType=binary&ratio=1&rotation=0&showTitle=false&size=63659&status=done&style=none&taskId=u3d808fc5-a0af-4fc2-8269-ce4aa2c109f&title=&width=557)<br />**命令通信流**<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654568135472-a043ff60-8da1-4f98-8029-3db282de0623.png#averageHue=%236d6b5e&clientId=ua5a358c9-400c-4&from=paste&height=645&id=u81f06b24&originHeight=645&originWidth=654&originalType=binary&ratio=1&rotation=0&showTitle=false&size=154797&status=done&style=none&taskId=u92434028-1c71-4d50-a707-535c573e18b&title=&width=654)<br />流程：写了一个Class，然后根据Class创建对象，然后我们会赋予指向这个实例的指针（这对于注册这个命令插件是有很大帮助的），然后我们会要求maya生成一个Handle （MObject）抓住指针，然后这个handle会从maya core 中带来实例<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654568454024-b97c2b67-2df4-4955-a08c-ffd307bfd6a0.png#averageHue=%23030302&clientId=ua5a358c9-400c-4&from=paste&height=1322&id=u7f352b5f&originHeight=1322&originWidth=2569&originalType=binary&ratio=1&rotation=0&showTitle=false&size=266213&status=done&style=none&taskId=u660bc2f1-0754-4848-8c28-9696240a0ac&title=&width=2569)
<a name="tHYsJ"></a>
# 第六集 编写命令插件（跟第五集相关联）
目的：通过配合MPxCommand写一个命令，然后保存好并加载进maya的插件中以后，就可以通过maya.cmds直接使用这个命令。比如通过MpxCommand写了一个输出hello world的功能，写好保存加载好以后，就可以直接通过cmds使用那个功能来输出hello world。总之，这节课的目的就是教我们如何扩展maya的命令也就是编写命令插件。<br />经过上一集的介绍，我们也大概了解了maya的内部流程，因此我们通过这个流程来编写命令插件。<br />所需要的编写规范可以参考一下官方给的范例：[https://help.autodesk.com/view/MAYAUL/2019/CHS/?guid=Maya_SDK_MERGED_py_ref_scripted_2hello_world_cmd_8py_example_html](https://help.autodesk.com/view/MAYAUL/2019/CHS/?guid=Maya_SDK_MERGED_py_ref_scripted_2hello_world_cmd_8py_example_html)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654585168421-378f7b25-d83e-4a87-80af-5965c8c63712.png#averageHue=%23070707&clientId=ua5a358c9-400c-4&from=paste&height=611&id=uee806a44&originHeight=611&originWidth=1229&originalType=binary&ratio=1&rotation=0&showTitle=false&size=249000&status=done&style=none&taskId=u6daf5f25-c46a-443a-9d07-d90101fcb7a&title=&width=1229)
```python
# coding:utf-8
import maya.OpenMaya as OpenMaya
import maya.OpenMayaMPx as OpenMayaMPx  # 当制作自定义的命令时需要导入此类来制作
import sys  # 输出错误所需要的模块

commandName = "pluginCommand"  # 定义命令的名字


class pluginCommand(OpenMayaMPx.MPxCommand):  # 创建自定义的命令需要继承MPxCommand

    def __init__(self):
        OpenMayaMPx.MPxCommand.__init__(self) # 初始化此自定义类的同时也需要初始化MPxCommand

    def doIt(self, argList): # 为自定义的命令创建功能，argList意思是参数列表
        print "doIt..."


def cmdCreator():  # 为实例化的类创建指针
    return OpenMayaMPx.asMPxPtr(pluginCommand())


def initializePlugin(mobject):  # 初始化
    mplugin = OpenMayaMPx.MFnPlugin(mobject)  # maya准备mobject来创建一个针对Plugin的函数库
    try:
        mplugin.registerCommand(commandName, cmdCreator)  # 使用函数库中的注册命令，来注册我们自定义的命令，需要命令的名字和指向命令的指针
    except:
        sys.stderr.write("Failed to register command :" + commandName)  # 如果注册失败就输出错误


def uninitializePlugin(mobject):  # 取消初始化
    mplugin = OpenMayaMPx.MFnPlugin(mobject)
    try:
        mplugin.deregisterCommand(commandName)  # 使用函数库中的取消注册命令，只需要命令的名字不需要指针
    except:
        sys.stderr.write("Failed to de-register command:" + commandName)  # 失败就输出错误

```
代码完成后需要通过脚本编辑器将它们保存为脚本文件。<br />**通过UI加载这个脚本文件**<br />进入插件管理器，选择浏览，选择我们刚才保存的脚本文件。记载后就可以在脚本编辑器中使用这个自定义的命令了。<br />范例：<br />import maya.cmds as cmds<br />cmds.pluginCommand()<br />结果输出：doIt...<br />**通过python命令加载脚本文件**<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654591451689-7b0bff27-6b57-4778-a67a-301fae10a797.png#averageHue=%2344412a&clientId=ua5a358c9-400c-4&from=paste&height=104&id=uc6d364f2&originHeight=104&originWidth=990&originalType=binary&ratio=1&rotation=0&showTitle=false&size=83902&status=done&style=none&taskId=ufd5b8614-b788-4ca3-8fc6-e14187f8430&title=&width=990)<br />其中参数为脚本文件的路径
<a name="IqhGb"></a>
# 第七集 迭代器
一些概念在TD技能学院上面介绍了，这里就不介绍了。
```python
# coding:utf-8
# 实现打印出完整的场景层次结构
import maya.OpenMaya as OpenMaya

# 创建一个Dag迭代器，第一个参数指定迭代器的迭代类型是深度优先还是广度优先，第二个参数是指定迭代器迭代过滤类型，kInvalid意思是不过滤
dagIterator = OpenMaya.MItDag(OpenMaya.MItDag.kBreadthFirst, OpenMaya.MFn.kInvalid)
# 创建一个dagNode的函数库提供给dagNode类型的对象使用(目前为空)
dagNodeFn = OpenMaya.MFnDagNode()

while (not dagIterator.isDone()):
    currentObj = dagIterator.currentItem()  # currentObj代表着当前迭代对象类型为MObject
    depth = dagIterator.depth()  # depth代表着当前节点在DAG中相对于根节点的高度或深度
    dagNodeFn.setObject(currentObj)  # 为当前迭代对象提供函数库,函数库能够针对当前迭代对象使用方法

    name = dagNodeFn.name()  # 得到当前迭代对象的名字
    type = currentObj.apiTypeStr()  # 得到当前迭代对象的类型
    path = dagNodeFn.fullPathName()  # 返回一个字符串，表示从dag的根到此对象的完整路径。

    printOut = ""  # 定义一个printOut对象来当要输出信息的对象
    for i in range(0, depth):  # 根据当且迭代对象的深度为其增加相应个数的箭头来表示
        printOut += "------>"

    printOut += name + " : " + type  # 输出格式为名字加类型

    print printOut
    dagIterator.next()

```
再复习一下上一集的编写命令插件<br />将制作输出一个字符串命令改为输出当前场景的完整层次结构。<br />就是将print "doIt..."更改为这节的功能代码然后更改一下当时定义命令的名字。
```python
# coding:utf-8
import maya.OpenMaya as OpenMaya
import maya.OpenMayaMPx as OpenMayaMPx  # 当制作自定义的命令时需要导入此类来制作
import sys  # 输出错误所需要的模块

commandName = "printHierarchy"  # 定义命令的名字


class pluginCommand(OpenMayaMPx.MPxCommand):  # 创建自定义的命令需要继承MPxCommand

    def __init__(self):
        OpenMayaMPx.MPxCommand.__init__(self) # 初始化此自定义类的同时也需要初始化MPxCommand

    def doIt(self, argList): # 为自定义的命令创建功能，argList意思是参数列表
        # 创建一个Dag迭代器，第一个参数指定迭代器的迭代类型是深度优先还是广度优先，第二个参数是指定迭代器迭代过滤类型，kInvalid意思是不过滤
        dagIterator = OpenMaya.MItDag(OpenMaya.MItDag.kBreadthFirst, OpenMaya.MFn.kInvalid)
        # 创建一个dagNode的函数库提供给dagNode类型的对象使用(目前为空)
        dagNodeFn = OpenMaya.MFnDagNode()

        while (not dagIterator.isDone()):
            currentObj = dagIterator.currentItem()  # currentObj代表着当前迭代对象类型为MObject
            depth = dagIterator.depth()  # depth代表着当前节点在DAG中相对于根节点的高度或深度
            dagNodeFn.setObject(currentObj)  # 为当前迭代对象提供函数库,函数库能够针对当前迭代对象使用方法

            name = dagNodeFn.name()  # 得到当前迭代对象的名字
            type = currentObj.apiTypeStr()  # 得到当前迭代对象的类型
            path = dagNodeFn.fullPathName()  # 返回一个字符串，表示从dag的根到此对象的完整路径。

            printOut = ""  # 定义一个printOut对象来当要输出信息的对象
            for i in range(0, depth):  # 根据当且迭代对象的深度为其增加相应个数的箭头来表示
                printOut += "------>"

            printOut += name + " : " + type  # 输出格式为名字加类型

            print printOut
            dagIterator.next()


def cmdCreator():  # 为实例化的类创建指针
    return OpenMayaMPx.asMPxPtr(pluginCommand())


def initializePlugin(mobject):  # 初始化
    mplugin = OpenMayaMPx.MFnPlugin(mobject)  # maya准备mobject来创建一个针对Plugin的函数库
    try:
        mplugin.registerCommand(commandName, cmdCreator)  # 使用函数库中的注册命令，来注册我们自定义的命令，需要命令的名字和指向命令的指针
    except:
        sys.stderr.write("Failed to register command :" + commandName)  # 如果注册失败就输出错误


def uninitializePlugin(mobject):  # 取消初始化
    mplugin = OpenMayaMPx.MFnPlugin(mobject)
    try:
        mplugin.deregisterCommand(commandName)  # 使用函数库中的取消注册命令，只需要命令的名字不需要指针
    except:
        sys.stderr.write("Failed to de-register command:" + commandName)  # 失败就输出错误

```
<a name="KwVk8"></a>
# 第八集 带参数的自定义命令
命令与参数：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654654142735-9db6408b-637b-4325-b4e9-4582e9359024.png#averageHue=%23060606&clientId=ucf657a1b-3cc9-4&from=paste&height=412&id=ub91f598e&originHeight=412&originWidth=891&originalType=binary&ratio=1&rotation=0&showTitle=false&size=99488&status=done&style=none&taskId=ud0438dce-50e5-42e2-8c50-c3e4ee762b1&title=&width=891)
<a name="pOGMJ"></a>
## MSyntax和MArgDatabase
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654654751391-053205e6-58e7-4e4c-ab2a-6df862605f10.png#averageHue=%23070707&clientId=ucf657a1b-3cc9-4&from=paste&height=619&id=ub6dfa1c1&originHeight=619&originWidth=1046&originalType=binary&ratio=1&rotation=0&showTitle=false&size=275699&status=done&style=none&taskId=ue5932f12-e5c2-45db-af62-beff1bdc73e&title=&width=1046)<br />parsing：语法分析<br />storing：储存<br />retrieving：检索<br />通过MSyntax定义我们的脚本命令接受什么类型的flag还有arguments还有object，然后maya会判断这个传入的参数是否可以接受。<br />MArgDatabase是一个类，它可以分析储存与检索flag和flag arguments 和object<br />如果我们更加深入地了解MArgDatabase，我们会发现它派生了MArgParser类<br />通过MSyntax和MArgDatabase我们可以接受标志参数和对象并解析他们并存储他们，基于这些值我们可以执行某些操作。
<a name="PZWNj"></a>
## maya 的undo 和redo
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654657249311-83584b52-bb25-4c79-8b56-137deaba4407.png#averageHue=%23323131&clientId=ucf657a1b-3cc9-4&from=paste&height=415&id=ucf17a14b&originHeight=415&originWidth=1004&originalType=binary&ratio=1&rotation=0&showTitle=false&size=76752&status=done&style=none&taskId=u2b2f7b2f-3994-431d-bd2c-95ba9e19808&title=&width=1004)<br />maya在执行一个命令时，undo（撤销）框架下会存储相同的命令，当执行undo命令时，undo框架下的命令将会移动到redo框架上面。<br />当我们自己自定义一个命令时也要同时定义一个undo和redo函数。
<a name="vGebW"></a>
## 新增代码过程
1.首先在新建的命令类之外定义一个syntaxCreator函数，写一个MSyntax类的对象，为这个对象定义新增的标志（flag），然后返回这个对象。<br />2.在初始化注册函数中的注册方法中新增刚才定义的带标志的语法对象（通过synaxCreator函数来得到(不需要在函数后面加括号)）。![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654761391104-8b281824-2418-4e86-b894-7fd9095e2036.png#averageHue=%23040303&clientId=uf9589504-71a5-4&from=paste&height=958&id=u0f0c1ab2&originHeight=958&originWidth=1096&originalType=binary&ratio=1&rotation=0&showTitle=false&size=127693&status=done&style=none&taskId=uefb6751e-3248-484e-b28e-cbc46f0141f&title=&width=1096)<br />3.在命令类之内新建一个argmentParser（参数解析器）函数用来解析argList，通过MArgDatabase类中的方法，来判断传入的标志与参数。<br />4.在doIt函数中首先使用这个argmentParser函数来解析参数，然后根据参数的内容有无（默认参数为None）来决定执行redoIt（真正的实现执行功能的函数）,之所以使用将实现功能的命令都放到redoIt函数中是因为当我们执行了undo（撤销）操作后会调用undoIt函数，然后如果再使用redo（重做；取消撤销）操作后会执行redoIt函数，redo后就需要再次实现功能了，因此把功能命令都放到redoIt函数中，doIt函数调用redoIt就好了。<br />5.redoIt函数中的逻辑如下：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654783736392-7b1ddd64-5d06-4be1-bf55-6fb041a44c93.png#averageHue=%23080808&clientId=u5ef47344-949c-4&from=paste&height=462&id=uae6bc522&originHeight=462&originWidth=1183&originalType=binary&ratio=1&rotation=0&showTitle=false&size=180631&status=done&style=none&taskId=u6ccbf6f1-c885-4383-bde0-aa40fb9a37a&title=&width=1183)<br />首先读取所选择的物体，然后读取物体的点的位置信息，然后创建一个粒子发射系统，然后将粒子系统发射的粒子移动到物体点的位置上去。<br />6.定义isUndoable函数，返回True，意思是定义我们要新加的功能是可以撤销的。<br />7.定义undoIt函数，当我们执行撤销操作时会调用这个函数。<br />8.Maya api中MStatus的更新[https://zhuanlan.zhihu.com/p/508453168](https://zhuanlan.zhihu.com/p/508453168)<br />在2013后的版本中，Maya_api将MStatus从库中删除了，在编写脚本时要用python自带的异常捕获机制来代替。<br />若继续使用MStatus会报错‘module’ object has no attribute ‘MStatus’<br />简单的代替方法：<br />原：OpenMaya.MStatus.kUnKonwnParameter更改为return 'unknown'<br />原OpenMaya.MStatus.kSuccess的，直接删掉就好了。
<a name="FoNsq"></a>
## 全部代码

```python
# coding:utf-8
# 这个命令是制作特效，将顶点转换成粒子
import maya.OpenMaya as OpenMaya
import maya.OpenMayaMPx as OpenMayaMPx  # 当制作自定义的命令时需要导入此类来制作
import sys  # 输出错误所需要的模块
import maya.OpenMayaFX as OpenMayaFX

commandName = "vertexPartial"  # 定义命令的名字

kHelpFlag = "-h"
kHelpLongFlag = "-help"
kSparseFlag = "-s"
kSparseLongFlag = "-sparse"  # 这个标志用来控制每多少顶点生成一个粒子
helpMessage = "This command is used to attach a particle on each vertex of a poly mesh"


class pluginCommand(OpenMayaMPx.MPxCommand):  # 创建自定义的命令需要继承MPxCommand
    sparse = None

    def __init__(self):
        OpenMayaMPx.MPxCommand.__init__(self)  # 初始化此自定义类的同时也需要初始化MPxCommand

    def argumentParser(self, argList):  # 分析参数的作用
        syntax = self.syntax()  # 使用继承的MPxCommand中的函数
        parsedArguments = OpenMaya.MArgDatabase(syntax, argList)  # 创建MArgDatabase对象接收传入的参数
        if parsedArguments.isFlagSet(kSparseFlag):  # 判断传入的对应的标志
            self.sparse = parsedArguments.flagArgumentDouble(kSparseFlag, 0)  # flagArgumentDouble接收两个参数，第二个是序列

        if parsedArguments.isFlagSet(kSparseLongFlag):
            self.sparse = parsedArguments.flagArgumentDouble(kSparseFlag, 0)

        if parsedArguments.isFlagSet(kHelpFlag):  # 如果标志是help就输出帮助信息
            self.setResult(helpMessage)  # 返回输出帮助信息

        if parsedArguments.isFlagSet(kHelpLongFlag):
            self.setResult(helpMessage)

    def isUndoable(self):  # 设置为可以撤销的命令
        return True

    def undoIt(self):  # 执行撤销操作时的步骤
        print "undo"
        mFnDagNode = OpenMaya.MFnDagNode(self.mobj_particle)  # 为创建的粒子系统绑定函数库
        mDagMod = OpenMaya.MDagModifier()  # 创建一个用来更改Dag的对象
        mDagMod.deleteNode(mFnDagNode.parent(0))  # 删除通过redoIt函数创建的粒子系统的transform
        mDagMod.doIt()

    def redoIt(self):  # 这是主要实现功能的函数，放到redoIt是因为执行undo操作后如果再执行redo就会跳到这里，doit时也会使用这个redoIt函数
        mSel = OpenMaya.MSelectionList()
        mDagPath = OpenMaya.MDagPath()
        mFnMesh = OpenMaya.MFnMesh()
        OpenMaya.MGlobal.getActiveSelectionList(mSel)  # 使用全局方法中的获取选择的物体并添加到列表对象中的方法
        if mSel.length() >= 1:
            try:
                mSel.getDagPath(0, mDagPath)  # 获取列表中的物体的dagPath并赋值
                mFnMesh.setObject(mDagPath)  # 将物体与函数库绑定
            except:  # 如果选择的物体不是mesh那么会执行这个
                print "Select a poly mesh"
                return 'unknown'
        else:  # 如果没有选择物体会执行这个
            print "Select a poly mesh"
            return 'unknown'

        mPointArray = OpenMaya.MPointArray()  # 创建一个点的数组对象
        mFnMesh.getPoints(mPointArray, OpenMaya.MSpace.kWorld)  # 将物体的点的位置信息赋予数组，在世界空间下

        # create a particle system
        mFnParticle = OpenMayaFX.MFnParticleSystem()
        self.mobj_particle = mFnParticle.create()  # 通过粒子系统函数库中的create方法得到一个粒子发射器并且是Mobject类型并且是shape节点

        # To fix Maya bug
        mFnParticle = OpenMayaFX.MFnParticleSystem(self.mobj_particle)

        counter = 0  # 创建一个变量用来记录粒子个数
        # 在for循环中使用xrange和range功能是一样的，xrange是python2独有的方法，xrange更节省性能，xrange与range的区别是xrange生成的是生成器而range是列表
        for i in xrange(mPointArray.length()):
            if i % self.sparse == 0:  # 根据sparse的数值决定以多少顶点为单位发射粒子
                mFnParticle.emit(mPointArray[i])
                counter += 1
        print "Total Points :" + str(counter)
        mFnParticle.saveInitialState()  # 重置粒子的当前状态为初始状态

    def doIt(self, argList):  # 为自定义的命令创建功能，argList意思是参数列表
        self.argumentParser(argList)  # 执行命令前先通过参数诊断功能诊断一下参数
        if self.sparse != None:  # 如果给了sparse（标志）参数 那么就执行后面的命令
            self.redoIt()  # 之所以在doIt中使用redoIt是因为当我们执行undo操作后再redo操作时依然会执行我们的功能实现命令，因此将功能实现命令放到redoIt中


# creator
def cmdCreator():  # 为实例化的类创建指针
    return OpenMayaMPx.asMPxPtr(pluginCommand())


def syntaxCreator():
    # create MSyntax object
    syntax = OpenMaya.MSyntax()
    # collect/add the flags
    syntax.addFlag(kHelpFlag, kHelpLongFlag)  # 定义每个命令都需要的help标志（短名和长名，不需要定义接受的数据的类型）
    syntax.addFlag(kSparseFlag, kSparseLongFlag, OpenMaya.MSyntax.kDouble)  # 定义接受的flag以及接受的数据的类型
    # return MSyntax
    return syntax


# Initialize the script plug-in
def initializePlugin(mobject):
    mplugin = OpenMayaMPx.MFnPlugin(mobject)  # maya准备mobject来创建一个针对Plugin的函数库
    try:
        mplugin.registerCommand(commandName, cmdCreator, syntaxCreator)  # 使用函数库中的注册命令，来注册我们自定义的命令，需要命令的名字和指向命令的指针以及语法
    except:
        sys.stderr.write("Failed to register command :" + commandName)  # 如果注册失败就输出错误


# Uninitialize the scrip plug-in
def uninitializePlugin(mobject):  # 取消初始化
    mplugin = OpenMayaMPx.MFnPlugin(mobject)
    try:
        mplugin.deregisterCommand(commandName)  # 使用函数库中的取消注册命令，只需要命令的名字不需要指针
    except:
        sys.stderr.write("Failed to de-register command:" + commandName)  # 失败就输出错误

```
<a name="jU2gx"></a>
# 第九集  Dependency graph
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654827627060-a933b100-c7f9-4ea3-ae7b-b7fb1e48e9b2.png#averageHue=%23090909&clientId=uef2f4691-1f38-4&from=paste&height=155&id=u5d27acdc&originHeight=155&originWidth=285&originalType=binary&ratio=1&rotation=0&showTitle=false&size=18008&status=done&style=none&taskId=ucd91a86b-1ead-4ecb-a54d-34aac3ed40f&title=&width=285)
<a name="Fo3yF"></a>
## Dirty Propagation 、Push & Pull Mechanism、 Lazy Evaluation
这三个术语通过举例来理解：假如你必须洗衣服，然后走进洗衣房，你会看到那里有几个洗衣机几个干衣机和几个与干衣机相关的桶，它们上面还有计时器记录剩余的时间，你根据它们的剩余时间将它们标记为红色，当你真正去洗衣烘干放入桶中后你会将它们标记为绿色。这是Dirty propagation（红色）  以及 Push&Pull Mechanism（绿色），这个过程叫LazyEvaluation<br />这样的好处是，当我们做出更新节点的操作时，maya只会更新操作所需要的节点，而不会对其他节点做操作，不会更新场景中的所有节点，这样减轻了性能消耗。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654828197676-5bd1d138-a72c-404d-9e93-2e7977496007.png#averageHue=%23060606&clientId=uef2f4691-1f38-4&from=paste&height=704&id=u62b41d51&originHeight=704&originWidth=643&originalType=binary&ratio=1&rotation=0&showTitle=false&size=150878&status=done&style=none&taskId=u2704fddb-5503-45e7-a3a5-15124ea6154&title=&width=643)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654828293828-b4e1dd36-5ac9-4893-9634-5e521c4ce087.png#averageHue=%230c0c0c&clientId=uef2f4691-1f38-4&from=paste&height=743&id=uaaa775f5&originHeight=743&originWidth=687&originalType=binary&ratio=1&rotation=0&showTitle=false&size=153868&status=done&style=none&taskId=u653c2866-8142-4323-b419-00e4b94cb8f&title=&width=687)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654829047593-e83a4b91-8c03-447b-b015-1aaf5ace3807.png#averageHue=%230e0b0b&clientId=uef2f4691-1f38-4&from=paste&height=729&id=u51ce4810&originHeight=729&originWidth=599&originalType=binary&ratio=1&rotation=0&showTitle=false&size=136664&status=done&style=none&taskId=udf5fedaa-0711-4aa3-8a1b-f11c8382113&title=&width=599)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654829067445-7c407b6b-329f-45a6-bfeb-d1a22082f8a7.png#averageHue=%23050404&clientId=uef2f4691-1f38-4&from=paste&height=710&id=uc6032233&originHeight=710&originWidth=1277&originalType=binary&ratio=1&rotation=0&showTitle=false&size=216658&status=done&style=none&taskId=ud10c9a92-52c1-4968-8b86-796a12fa615&title=&width=1277)
<a name="wt2Ut"></a>
# 第十集 Writing Custom/DG Nodes
<a name="e08Na"></a>
## 什么是Dependency graph node：
就是一个节点，有数据，有连接接口，有处理数据的能力。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654831547814-0d6a39ed-e95e-49bb-9947-daa7ec027d30.png#averageHue=%23060606&clientId=uef2f4691-1f38-4&from=paste&height=412&id=u43e0607a&originHeight=412&originWidth=1173&originalType=binary&ratio=1&rotation=0&showTitle=false&size=112777&status=done&style=none&taskId=u6097b8ec-e312-4659-b6c1-e56bc862c05&title=&width=1173)
<a name="RTno9"></a>
## 设计一个Dependency graph node
设计一个Dependency graph node 的过程和创建一个自定义命令差不多：<br />自定义的类需要继承MPxNode，__init__以及compute函数（类似与doIt函数），compute函数为节点最核心的方法，我们所有的算法都要存到这里通过计算返回不同的结果。<br />然后类外需要定义的函数：<br />1.creator function 2.initialize函数（初始化属性）3.initialize plugin（注册） 4.uninitialize plugin（取消注册）<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654838003301-9b0a7b2e-04bb-4cdc-aaa7-0a3a467473d4.png#averageHue=%23080808&clientId=uef2f4691-1f38-4&from=paste&height=332&id=u85c8ba3e&originHeight=332&originWidth=1219&originalType=binary&ratio=1&rotation=0&showTitle=false&size=121376&status=done&style=none&taskId=u1797dd8c-2129-4843-9951-5d2ae8e6cb4&title=&width=1219)
<a name="m533a"></a>
## 针对不同的属性类型（数字，灯光，信息）使用不同的属性函数库
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654838073661-4256666b-70ce-477f-9f85-1e5eac5862ec.png#averageHue=%23ebebeb&clientId=uef2f4691-1f38-4&from=paste&height=1128&id=ue31e219c&originHeight=1128&originWidth=1277&originalType=binary&ratio=1&rotation=0&showTitle=false&size=253204&status=done&style=none&taskId=u1eab58d0-2417-437d-9052-74e81fe422a&title=&width=1277)
<a name="t1fWd"></a>
## initialize  函数的构建过程
首先创建一个MFnNumericAttribute函数库，通过这个函数库来创建属性并设置属性的名字初始值（传递给自定义类中创建的对应属性名字的MObject）然后定义特征（是否可读可写可存储可k关键帧），然后将属性绑定到节点上（因为通过MFn得到的属性是MObject类型）（因为我们的类继承了对应的MPx，因此使用继承的类中的addAttribute方法来讲MObject类型的属性附加到节点（类）上），最后设置电路（属性之间的联系，即定义输入（Input）输出（Output），通过使用继承的类中的attributeAffects方法，意思是方法内的属性参数，左边的属性影响右边的属性。Affects是影响的意思）<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654838266425-12951ed4-a954-41dd-b066-57260a918d47.png#averageHue=%230b0b0b&clientId=uef2f4691-1f38-4&from=paste&height=840&id=uc0bad8e7&originHeight=840&originWidth=1191&originalType=binary&ratio=1&rotation=0&showTitle=false&size=274344&status=done&style=none&taskId=ua08e7990-c545-48e2-94d0-a18f8a98b31&title=&width=1191)
<a name="hwfgy"></a>
## nodeInitializer函数中的create Attribute 创建属性的流程：
通过MFn创建MObject类型的属性，然后设置属性，有readable（设置此属性是否可读。如果一个属性是可读的，那么它可以用作依赖图连接中的源。），writable（如果是可写的，那么这个属性就可以作为其他属性的目标（下游）），storable（设置此属性是否可存储。如果属性是可存储的，那么当节点存储到文件中时，它将被写入。这应该只在节点创建者的初始化调用中调用。），keyable（设置此属性是否应接受关键帧数据。这应该只在节点创建者的初始化调用中调用。可键属性将由AutoKey和Set Keyframe UI进行键控。非键属性可以防止用户通过为键控提供的明显UI设置键。不可键性并不会阻碍向属性添加键。）我们也可以设置属性的最小值与最大值。通过使用函数集中的setMin和setMax来达到。<br />这是创建属性后的默认的设置的属性![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1655193938297-221ece78-d71e-4b8f-88b5-6c78d38175b0.png#averageHue=%23b7b4b1&clientId=u0e472ba4-a7b1-4&from=paste&height=284&id=u58f18f07&originHeight=284&originWidth=394&originalType=binary&ratio=1&rotation=0&showTitle=false&size=84002&status=done&style=none&taskId=u6292d689-ac98-4ffb-bd3f-6090e5290d2&title=&width=394)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654840493422-83974a11-93df-44da-b48a-c0528aeaa594.png#averageHue=%230c0c0c&clientId=uef2f4691-1f38-4&from=paste&height=600&id=ud30a105d&originHeight=600&originWidth=524&originalType=binary&ratio=1&rotation=0&showTitle=false&size=123043&status=done&style=none&taskId=u94299b19-503b-4c67-b24b-dceb2de27e7&title=&width=524)
<a name="Dsvjn"></a>
## 实例：制作一个轮子节点
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654838653486-dca0b8bd-61ca-4e3a-b3f9-b88b3cdf6eef.png#averageHue=%234f5a64&clientId=uef2f4691-1f38-4&from=paste&height=244&id=u96dabb16&originHeight=244&originWidth=732&originalType=binary&ratio=1&rotation=0&showTitle=false&size=127339&status=done&style=none&taskId=u177c778c-52b2-4d81-8ca6-424199a44c8&title=&width=732)<br />通过平移使轮子自动旋转<br />公式与节点大致形状：根据平移的距离来控制旋转的角度的多少（一个圆的周长的距离为360度）<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654838799385-9aebdb70-5728-4a13-b88b-d20f5b4614dd.png#averageHue=%230c0c0c&clientId=uef2f4691-1f38-4&from=paste&height=548&id=ub5bfe141&originHeight=548&originWidth=813&originalType=binary&ratio=1&rotation=0&showTitle=false&size=114294&status=done&style=none&taskId=u5f34f97b-578b-471d-829d-4670f09fab6&title=&width=813)<br />nodeId： 每个节点都应该有对应的ID来对应它，无论是maya的还是用户自定义的（UUID）
```python
# coding:utf-8
# 自定义一个节点，制作轮子效果
import maya.OpenMaya as OpenMaya
import maya.OpenMayaMPx as OpenMayaMPx  # 制作自定义的东西时需要的模块
import sys  # 输出错误所需要的模块

nodeName = "WheelNode"  # 定义节点的名字
nodeId = OpenMaya.MTypeId(0x100fff)


class WheelNode(OpenMayaMPx.MPxNode):
    # 创建MObject类型的输入输出
    inRadius = OpenMaya.MObject()
    inTranslate = OpenMaya.MObject()
    outRotate = OpenMaya.MObject()

    def __init__(self):
        OpenMayaMPx.MPxNode.__init__(self)

    def compute(self, plug, dataBlock):
        '''
        rotate = translate/(2*3.14*radius)*(-360)
        :param plug: 节点属性
        :param dataBlock:节点属性中的数据
        :return:
        '''
        if plug == WheelNode.outRotate:
            # 通过指向节点属性的指针得到指向数据块（dataBlock）上的值的指针
            dataHandleRadius = dataBlock.inputValue(WheelNode.inRadius)
            dataHandleTranslate = dataBlock.inputValue(WheelNode.inTranslate)

            inRadiusVal = dataHandleRadius.asFloat()
            inTranslateVal = dataHandleTranslate.asFloat()

            outRotate = float(inTranslateVal) / float(2 * 3.14 * inRadiusVal) * (-360)

            dataHandleRotate = dataBlock.outputValue(WheelNode.outRotate)

            dataHandleRotate.setFloat(outRotate)
            dataBlock.setClean(plug)

        else:
            return 'unknown'

    def doIt(self, argList):  # 为自定义的命令创建功能，argList意思是参数列表
        self.argumentParser(argList)  # 执行命令前先通过参数诊断功能诊断一下参数
        if self.sparse != None:  # 如果给了sparse（标志）参数 那么就执行后面的命令
            self.redoIt()  # 之所以在doIt中使用redoIt是因为当我们执行undo操作后再redo操作时依然会执行我们的功能实现命令，因此将功能实现命令放到redoIt中


def nodeCreator():
    return OpenMayaMPx.asMPxPtr(WheelNode())


def nodeInitializer():
    # 1. creating a function set for numeric attributes
    # 创建数字属性的函数集，因为我们的自定义属性是数字的，因此创建对应的函数集
    mFnAttr = OpenMaya.MFnNumericAttribute()

    # 2. create the attributes
    # # 创建translate属性，短名为t，数据类型为float，默认值为0.0，由自定义类中的inTranslate（MObject类型）来接收
    WheelNode.inTranslate = mFnAttr.create("translate", "t", OpenMaya.MFnNumericData.kFloat, 0.0)
    # 设置节点属性是否可读可写可储存可k帧
    # 其中readable，writable，storable是默认为1的也可以不写。
    mFnAttr.setReadable(1)
    mFnAttr.setWritable(1)
    mFnAttr.setStorable(1)
    mFnAttr.setKeyable(1)

    WheelNode.inRadius = mFnAttr.create("radius", "r", OpenMaya.MFnNumericData.kFloat, 0.0)
    mFnAttr.setReadable(1)
    mFnAttr.setWritable(1)
    mFnAttr.setStorable(1)
    mFnAttr.setKeyable(1)

    WheelNode.outRotate = mFnAttr.create("rotate", "rot", OpenMaya.MFnNumericData.kFloat)  # 因为是输出属性所以不能定义默认值
    mFnAttr.setReadable(1)
    mFnAttr.setWritable(0)
    mFnAttr.setStorable(0)
    mFnAttr.setKeyable(0)

    # 3. Attaching the attributes to the Node
    WheelNode.addAttribute(WheelNode.inRadius)
    WheelNode.addAttribute(WheelNode.inTranslate)
    WheelNode.addAttribute(WheelNode.outRotate)

    # 4. Design circuitry
    # 设计电路板，这里设计的是，inRadius和inTranslate均与outRotate进行连接
    WheelNode.attributeAffects(WheelNode.inRadius, WheelNode.outRotate)
    WheelNode.attributeAffects(WheelNode.inTranslate, WheelNode.outRotate)


# Initialize the script plug-in
def initializePlugin(mobject):
    mplugin = OpenMayaMPx.MFnPlugin(mobject)
    try:
        # 注册一个节点，第一个为节点名字，第二个为节点ID，第三个为创建节点指针的函数，第四个为节点初始化(定义节点的属性函数)，第五个为节点的分类（没有也不会报错，但是最好写上）
        mplugin.registerNode(nodeName, nodeId, nodeCreator, nodeInitializer, OpenMayaMPx.MPxNode.kDeformerNode)
    except:
        sys.stderr.write("Failed to register command :" + nodeName)  # 如果注册失败就输出错误


# Uninitialize the scrip plug-in
def uninitializePlugin(mobject):  # 取消初始化
    mplugin = OpenMayaMPx.MFnPlugin(mobject)
    try:
        mplugin.deregisterNode(nodeName)  # 使用函数库中的取消注册命令，只需要命令的名字不需要指针
    except:
        sys.stderr.write("Failed to de-register command:" + nodeName)  # 失败就输出错误

```
<a name="ZOBPy"></a>
## 创建自定义节点后的使用流程
通过这个命令加载自定义节点<br />import maya.cmds as cmds<br />cmds.loadPlugin(r'D:\ZhangRuiChen\pythonProject\wheelNode.py')<br />然后就可以在节点编辑器中通过自定义节点名字搜索到这个节点了。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654850231689-4d983292-0871-4ddc-8a89-a891ff062b9d.png#averageHue=%23353535&clientId=uef2f4691-1f38-4&from=paste&height=379&id=u71ae120e&originHeight=379&originWidth=930&originalType=binary&ratio=1&rotation=0&showTitle=false&size=54039&status=done&style=none&taskId=u8c0a18b0-116b-4de5-9260-4bfd35da862&title=&width=930)<br />这里的unitConversion1是当我们的WheelNode节点的Rotate属性连接到pCylinder1中的RotateZ上后maya自动生成的。<br />连接好后就可以实现功能了。
<a name="IA4tx"></a>
# 第十一集 Deformer 变形器
什么是变形器<br />变形器是一个节点，下图是一个变形器所必须带有的属性<br />Input是几何体的输入，envelope控制变形的程度，范围是0~1，为0时不变形，为1时完全按照变形器的计算来变形。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654954141595-9f886125-2bf0-4c0a-916e-f4fabc55a75a.png#averageHue=%23050505&clientId=u7e71c804-4cbe-4&from=paste&height=569&id=ub6e2995f&originHeight=569&originWidth=989&originalType=binary&ratio=1&rotation=0&showTitle=false&size=68092&status=done&style=none&taskId=u8d463e5d-a017-4bac-818a-1d58d371217&title=&width=989)<br />我们的物体内部存在两个东西，一个groupId，一个inputGeom（这个是我们需要的）<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654954411580-4d2ca110-7b7d-4a60-be86-d56acc21327b.png#averageHue=%230a0a0a&clientId=u7e71c804-4cbe-4&from=paste&height=406&id=u0afe2b74&originHeight=406&originWidth=422&originalType=binary&ratio=1&rotation=0&showTitle=false&size=73595&status=done&style=none&taskId=u4e8e7207-3ffd-4c98-b8c4-fba2e4fabc6&title=&width=422)<br />编写代码的框架：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654954490051-909892d3-7b1b-483a-a180-f16b6b087def.png#averageHue=%230c0c0c&clientId=u7e71c804-4cbe-4&from=paste&height=551&id=u3b9e0f86&originHeight=551&originWidth=383&originalType=binary&ratio=1&rotation=0&showTitle=false&size=95145&status=done&style=none&taskId=ube931fc2-1f40-4e38-8b18-9f55eaffd94&title=&width=383)
<a name="Iednj"></a>
# 第十二~十五集 编写自定义变形器
可以参考的网站[https://www.xingyulei.com/post/maya-api-deformer/](https://www.xingyulei.com/post/maya-api-deformer/)<br />自定义变形器的设计：<br />除默认自带的属性外，额外添加的自定义属性：amplitude（振幅，浮点型，范围是0~1），Displace（位移，浮点型，范围是0~10）<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1655193336188-7a98e85a-c013-4cb5-8432-d991431d7311.png#averageHue=%23151515&clientId=u0e472ba4-a7b1-4&from=paste&height=744&id=ufdb4ea8c&originHeight=744&originWidth=1032&originalType=binary&ratio=1&rotation=0&showTitle=false&size=133442&status=done&style=none&taskId=uedd49e5f-48eb-490e-92d3-21020b36bc9&title=&width=1032)<br />其中实现初始化功能的函数的内容步骤和自定义节点的步骤是相同的，有一点区别就是变形器节点具有默认的outputGeom属性，因此我们没必要再创建一个输出的属性，我们可以直接利用这个默认的outputGemo属性，那么怎么使用这个outputGemo属性呢？<br />教程中首先介绍了SWIG，然后使用了语句<br />SWIG - Simplified Wrapper Interface Generator 简化 包装器 接口 生成器   <br />是允许开发人员使用脚本语言包装C++代码的工具,因为maya核心是由C++编写的<br />Autodesk 为我们提供了一种使用swig使用这些属性的方法<br />通过这个语句:outputGemo = OpenMayaMPx.cvar.MPxDeformerNode_outputGeom
<a name="DrdaR"></a>
## 类中的deform函数的实现过程
从左到右依次是self,   dataBlock,    geoIterator,    matrix,    geometryIndex<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1655260910217-0fec322f-abc4-4d75-8b6a-28681c8e0621.png#averageHue=%23171616&clientId=uf5ec6e2c-c0bc-4&from=paste&height=240&id=u2b4fb92a&originHeight=240&originWidth=1944&originalType=binary&ratio=1&rotation=0&showTitle=false&size=118938&status=done&style=none&taskId=uf164ec2e-e1d7-48c4-909a-55534ee6ff1&title=&width=1944)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1655260672878-f903d98a-946d-45d1-b129-db85341c9766.png#averageHue=%23131212&clientId=uf5ec6e2c-c0bc-4&from=paste&height=1121&id=Eo736&originHeight=1121&originWidth=1264&originalType=binary&ratio=1&rotation=0&showTitle=false&size=264792&status=done&style=none&taskId=u9e14e773-0081-448e-8ed8-b33828939e3&title=&width=1264)<br />第一步将特殊的指针（dataHandileInputArray）指向变形器的Input数组，第二步通过geometryIndex跳到相应的元素，第三步（dataHandleInputElement）指向其中的特殊的dataBlock，第四步通过OpenMayaMPx.cvar.MPxDeformerNode_inputValue()找到它的inputGeom(变形器的默认节点)，然后通过.child方法将inputGeom的属性令dataHandleInputGeom指向。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1655263186190-461fec6c-6512-48b2-b371-a111eb09630c.png#averageHue=%23171717&clientId=uf5ec6e2c-c0bc-4&from=paste&height=1314&id=u471a85c9&originHeight=1314&originWidth=2587&originalType=binary&ratio=1&rotation=0&showTitle=false&size=798745&status=done&style=none&taskId=u7f3623cf-7ea3-47c4-baf3-7f8293186db&title=&width=2587)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1655265745683-7bb9b012-8a4e-478e-8ebf-835a8be69097.png#averageHue=%23191918&clientId=uf5ec6e2c-c0bc-4&from=paste&height=666&id=u0c4ee2e2&originHeight=666&originWidth=1288&originalType=binary&ratio=1&rotation=0&showTitle=false&size=314979&status=done&style=none&taskId=ua42216ec-9928-482c-852c-809b93056ed&title=&width=1288)
<a name="eP2I0"></a>
## 整体代码第一版
```python
# coding:utf-8
# 自定义一个变形器节点,通过调整ripple改变多边形的形状
import math

import maya.OpenMaya as OpenMaya
import maya.OpenMayaMPx as OpenMayaMPx  # 制作自定义的东西时需要的模块
import sys  # 输出错误所需要的模块

nodeName = "RippleDeformer"  # 定义节点的名字
nodeId = OpenMaya.MTypeId(0x102fff)


class Ripple(OpenMayaMPx.MPxDeformerNode):
    """
    Commands ----> MPxCommand
    Custom   ----> MPxNode
    Deformer ----> MPxDeformerNode
    """
    # 创建MObject类型的输入输出
    mObj_Displace = OpenMaya.MObject()
    mObj_Amplitude = OpenMaya.MObject()

    def __init__(self):
        OpenMayaMPx.MPxDeformerNode.__init__(self)

    def deform(self, dataBlock, geoIterator, matrix, geometryIndex):
        """
        变形器的核心参数
        :param dataBlock:数据块
        :param geoIterator: 迭代器，例如遍历一个几何体的所有顶点时用的到
        :param matrix: 矩阵   几何体的世界矩阵或受影响的网格
        :param geometryIndex: 几何索引，当使用多个几何体时，所有几何体都进入这个属性
        :return:
        """

        input = OpenMayaMPx.cvar.MPxGeometryFilter_input
        # 1. Attach a handle to input Array Attribute
        # 1. 为输入数组属性附加handle
        dataHandleInputArray = dataBlock.inputArrayValue(input)
        # 2. Jump to particular element
        # 2. 跳转到特定元素
        dataHandleInputArray.jumpToElement(geometryIndex)
        # 3. Attach a handle to specific data block
        # 3. 将handle附加到特定的数据块
        dataHandleInputElement = dataHandleInputArray.inputValue()
        # 4. Reach to the child - inputGeom
        inputGeom = OpenMayaMPx.cvar.MPxGeometryFilter_inputGeom
        dataHandleInputGeom = dataHandleInputElement.child(inputGeom)
        inMesh = dataHandleInputGeom.asMesh()
        # Envelope
        envelope = OpenMayaMPx.cvar.MPxGeometryFilter_envelope
        dataHandleEnvelope = dataBlock.inputValue(envelope)
        envelopeValue = dataHandleEnvelope.asFloat()
        # Amplitude
        dataHandleAmplitude = dataBlock.inputValue(Ripple.mObj_Amplitude)
        amplitudeValue = dataHandleAmplitude.asFloat()
        # Displace
        dataHandleDisplace = dataBlock.inputValue(Ripple.mObj_Displace)
        displaceValue = dataHandleDisplace.asFloat()

        mFloatVectorArray_normal = OpenMaya.MFloatVectorArray()  # 创建一个MFloatVectorArray的对象，getVertexNormals方法需要用到
        mFnMesh = OpenMaya.MFnMesh(inMesh)
        # 第一个参数是angleWeighted，如果angleWeighted设置为false，则返回环绕面法线的简单平均值。第三个参数是设置空间为对象空间
        mFnMesh.getVertexNormals(False, mFloatVectorArray_normal, OpenMaya.MSpace.kObject)

        while not geoIterator.isDone():
            pointPosition = geoIterator.position()

            pointPosition.x = pointPosition.x + math.sin(geoIterator.index() + displaceValue) * amplitudeValue * \
                              mFloatVectorArray_normal[geoIterator.index()].x * envelopeValue
            pointPosition.y = pointPosition.y + math.sin(geoIterator.index() + displaceValue) * amplitudeValue * \
                              mFloatVectorArray_normal[geoIterator.index()].y * envelopeValue
            pointPosition.z = pointPosition.z + math.sin(geoIterator.index() + displaceValue) * amplitudeValue * \
                              mFloatVectorArray_normal[geoIterator.index()].z * envelopeValue
            geoIterator.setPosition(pointPosition) 
            geoIterator.next()


def deformerCreator():
    nodePtr = OpenMayaMPx.asMPxPtr(Ripple())
    return nodePtr


def nodeInitializer():
    """
    写功能前先将流程写下来，然后每完成一个流程就标记一下那个流程
    Create Attributes  创建属性 - check
    Attach Attributes 附加属性 - check
    Design Circuitry 设计电路图 - check
    """
    # 1. creating a function set for numeric attributes
    # 创建数字属性的函数集，因为我们的自定义属性是数字的，因此创建对应的函数集
    mFnAttr = OpenMaya.MFnNumericAttribute()

    # 2. create the attributes
    # # 创建AttributeValue属性，短名为AttrVal，数据类型为float，默认值为0.0，由自定义类中的mObj_Amplitude（MObject类型）来接收
    Ripple.mObj_Amplitude = mFnAttr.create("AmplitudeValue", "AmplitudeVal", OpenMaya.MFnNumericData.kFloat, 0.0)
    mFnAttr.setKeyable(1)
    mFnAttr.setMin(0.0)
    mFnAttr.setMax(1.0)

    Ripple.mObj_Displace = mFnAttr.create("DisplaceValue", "DispVal", OpenMaya.MFnNumericData.kFloat, 0.0)
    mFnAttr.setKeyable(1)
    mFnAttr.setMin(0.0)
    mFnAttr.setMax(10.0)

    # 3. Attaching the attributes to the Node
    Ripple.addAttribute(Ripple.mObj_Amplitude)
    Ripple.addAttribute(Ripple.mObj_Displace)

    '''
    SWIG - Simplified Wrapper Interface Generator 简化 包装器 接口 生成器   
    是允许开发人员使用脚本语言包装C++代码的工具,因为maya核心是由C++编写的
    Autodesk 为我们提供了一种使用swig使用这些属性的方法
    '''
    outputGeom = OpenMayaMPx.cvar.MPxGeometryFilter_outputGeom

    # 4. Design circuitry
    Ripple.attributeAffects(Ripple.mObj_Amplitude, outputGeom)
    Ripple.attributeAffects(Ripple.mObj_Displace, outputGeom)


# Initialize the script plug-in
def initializePlugin(mobject):
    mplugin = OpenMayaMPx.MFnPlugin(mobject, "Violet", "1.0")  # maya准备mobject来创建一个针对Plugin的函数库,第二，三个参数为可选参数，分别代指编写人，版本号
    try:
        # 注册一个节点，第一个为节点名字，第二个为节点ID，第三个为创建节点指针的函数，第四个为节点初始化(定义节点的属性函数)，第五个为节点的分类（没有也不会报错，但是最好写上）
        mplugin.registerNode(nodeName, nodeId, nodeCreator, nodeInitializer)
    except:
        sys.stderr.write("Failed to register node: " + nodeName)  # 如果注册失败就输出错误
        raise


# Uninitialize the scrip plug-in
def uninitializePlugin(mobject):  # 取消初始化
    mplugin = OpenMayaMPx.MFnPlugin(mobject)
    try:
        mplugin.deregisterCommand(nodeId)  # 使用函数库中的取消注册命令，只需要命令的名字不需要指针
    except:
        sys.stderr.write("Failed to de-register node: " + nodeName)  # 失败就输出错误
        raise

```
<a name="sdAfs"></a>
## 优化后的代码
```python
# coding:utf-8
# 自定义一个变形器节点,通过调整ripple改变多边形的形状
import math

import maya.OpenMaya as OpenMaya
import maya.OpenMayaMPx as OpenMayaMPx  # 制作自定义的东西时需要的模块
import sys  # 输出错误所需要的模块

nodeName = "RippleDeformer"  # 定义节点的名字
nodeId = OpenMaya.MTypeId(0x102fff)


class Ripple(OpenMayaMPx.MPxDeformerNode):
    """
    Commands ----> MPxCommand
    Custom   ----> MPxNode
    Deformer ----> MPxDeformerNode
    """
    # 创建MObject类型的输入输出
    mObj_Displace = OpenMaya.MObject()
    mObj_Amplitude = OpenMaya.MObject()

    def __init__(self):
        OpenMayaMPx.MPxDeformerNode.__init__(self)

    def deform(self, dataBlock, geoIterator, matrix, geometryIndex):
        """
        变形器的核心参数
        :param dataBlock:数据块
        :param geoIterator: 迭代器，例如遍历一个几何体的所有顶点时用的到
        :param matrix: 矩阵   几何体的世界矩阵或受影响的网格
        :param geometryIndex: 几何索引，当使用多个几何体时，所有几何体都进入这个属性
        :return:
        """

        input = OpenMayaMPx.cvar.MPxGeometryFilter_input
        # 1. Attach a handle to input Array Attribute
        # 1. 为输入数组属性附加handle
        # 后来优化将inputArrayValue和inputValue都改为了output，可能是因为用output会自动检索最优路线吧
        dataHandleInputArray = dataBlock.outputArrayValue(input)
        # 2. Jump to particular element
        # 2. 跳转到特定元素
        dataHandleInputArray.jumpToElement(geometryIndex)
        # 3. Attach a handle to specific data block
        # 3. 将handle附加到特定的数据块
        dataHandleInputElement = dataHandleInputArray.outputValue()
        # 4. Reach to the child - inputGeom
        inputGeom = OpenMayaMPx.cvar.MPxGeometryFilter_inputGeom
        dataHandleInputGeom = dataHandleInputElement.child(inputGeom)
        inMesh = dataHandleInputGeom.asMesh()
        # Envelope
        envelope = OpenMayaMPx.cvar.MPxGeometryFilter_envelope
        dataHandleEnvelope = dataBlock.inputValue(envelope)
        envelopeValue = dataHandleEnvelope.asFloat()
        # Amplitude
        dataHandleAmplitude = dataBlock.inputValue(Ripple.mObj_Amplitude)
        amplitudeValue = dataHandleAmplitude.asFloat()
        # Displace
        dataHandleDisplace = dataBlock.inputValue(Ripple.mObj_Displace)
        displaceValue = dataHandleDisplace.asFloat()

        mFloatVectorArray_normal = OpenMaya.MFloatVectorArray()  # 创建一个MFloatVectorArray的对象，getVertexNormals方法需要用到
        mFnMesh = OpenMaya.MFnMesh(inMesh)
        # 第一个参数是angleWeighted，如果angleWeighted设置为false，则返回环绕面法线的简单平均值。第三个参数是设置空间为对象空间
        mFnMesh.getVertexNormals(False, mFloatVectorArray_normal, OpenMaya.MSpace.kObject)

        mPointArray_meshVert = OpenMaya.MPointArray()  # 创建一个空的存放点的数组
        while not geoIterator.isDone():
            pointPosition = geoIterator.position()

            pointPosition.x = pointPosition.x + math.sin(geoIterator.index() + displaceValue) * amplitudeValue * \
                              mFloatVectorArray_normal[geoIterator.index()].x * envelopeValue
            pointPosition.y = pointPosition.y + math.sin(geoIterator.index() + displaceValue) * amplitudeValue * \
                              mFloatVectorArray_normal[geoIterator.index()].y * envelopeValue
            pointPosition.z = pointPosition.z + math.sin(geoIterator.index() + displaceValue) * amplitudeValue * \
                              mFloatVectorArray_normal[geoIterator.index()].z * envelopeValue
            # geoIterator.setPosition(pointPosition)
            mPointArray_meshVert.append(pointPosition)
            geoIterator.next()
        geoIterator.setAllPosiions(mPointArray_meshVert)


def deformerCreator():
    nodePtr = OpenMayaMPx.asMPxPtr(Ripple())
    return nodePtr


def nodeInitializer():
    """
    写功能前先将流程写下来，然后每完成一个流程就标记一下那个流程
    Create Attributes  创建属性 - check
    Attach Attributes 附加属性 - check
    Design Circuitry 设计电路图 - check
    """
    # 1. creating a function set for numeric attributes
    # 创建数字属性的函数集，因为我们的自定义属性是数字的，因此创建对应的函数集
    mFnAttr = OpenMaya.MFnNumericAttribute()

    # 2. create the attributes
    # # 创建AttributeValue属性，短名为AttrVal，数据类型为float，默认值为0.0，由自定义类中的mObj_Amplitude（MObject类型）来接收
    Ripple.mObj_Amplitude = mFnAttr.create("AmplitudeValue", "AmplitudeVal", OpenMaya.MFnNumericData.kFloat, 0.0)
    mFnAttr.setKeyable(1)
    mFnAttr.setMin(0.0)
    mFnAttr.setMax(1.0)

    Ripple.mObj_Displace = mFnAttr.create("DisplaceValue", "DispVal", OpenMaya.MFnNumericData.kFloat, 0.0)
    mFnAttr.setKeyable(1)
    mFnAttr.setMin(0.0)
    mFnAttr.setMax(10.0)

    # 3. Attaching the attributes to the Node
    Ripple.addAttribute(Ripple.mObj_Amplitude)
    Ripple.addAttribute(Ripple.mObj_Displace)

    '''
    SWIG - Simplified Wrapper Interface Generator 简化 包装器 接口 生成器   
    是允许开发人员使用脚本语言包装C++代码的工具,因为maya核心是由C++编写的
    Autodesk 为我们提供了一种使用swig使用这些属性的方法
    '''
    outputGeom = OpenMayaMPx.cvar.MPxGeometryFilter_outputGeom

    # 4. Design circuitry
    Ripple.attributeAffects(Ripple.mObj_Amplitude, outputGeom)
    Ripple.attributeAffects(Ripple.mObj_Displace, outputGeom)


# Initialize the script plug-in
def initializePlugin(mobject):
    mplugin = OpenMayaMPx.MFnPlugin(mobject, "Violet", "1.0")  # maya准备mobject来创建一个针对Plugin的函数库,第二，三个参数为可选参数，分别代指编写人，版本号
    try:
        # 注册一个节点，第一个为节点名字，第二个为节点ID，第三个为创建节点指针的函数，第四个为节点初始化(定义节点的属性函数)，第五个为节点的分类（没有也不会报错，但是最好写上）
        mplugin.registerNode(nodeName, nodeId, deformerCreator, nodeInitializer, OpenMayaMPx.MPxNode.kDeformerNode)
    except:
        sys.stderr.write("Failed to register node: " + nodeName)  # 如果注册失败就输出错误
        raise


# Uninitialize the scrip plug-in
def uninitializePlugin(mobject):  # 取消初始化
    mplugin = OpenMayaMPx.MFnPlugin(mobject)
    try:
        mplugin.deregisterCommand(nodeId)  # 使用函数库中的取消注册命令，只需要命令的名字不需要指针
    except:
        sys.stderr.write("Failed to de-register node: " + nodeName)  # 失败就输出错误
        raise

```
<a name="YRcWy"></a>
## 增加了绘制功能的代码
增加绘制功能需要两个步骤，第一步是读取几何体的所有顶点，第二步是使用权重值去计算。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1655348913268-6601752e-a19d-44a1-a4e9-d8f0662e57ac.png#averageHue=%23050505&clientId=u17945a8c-e2a9-4&from=paste&height=645&id=u95c1b2a1&originHeight=645&originWidth=1808&originalType=binary&ratio=1&rotation=0&showTitle=false&size=188273&status=done&style=none&taskId=ud329f60f-40e9-496c-a07f-10985e09b94&title=&width=1808)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1655348400558-44f32f40-f000-4c88-b49f-cb8132434aef.png#averageHue=%23050505&clientId=u17945a8c-e2a9-4&from=paste&height=518&id=u4a540699&originHeight=518&originWidth=2038&originalType=binary&ratio=1&rotation=0&showTitle=false&size=187574&status=done&style=none&taskId=uc82cfbe0-632d-4c01-8170-8803373f817&title=&width=2038)<br />跟教程中的代码一样<br />教程中也就加了个weight = self.weightValue(dataBlock, geometryIndex, geoIterator.index())，然后通过weight来改变计算步骤，但是我的2018.5的版本maya无法实现绘制功能。<br />教程中有这个但是我的没有<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1655357981634-2f3303d0-0bf3-4d5a-95d7-2656a96385d0.png#averageHue=%23444f4d&clientId=u17945a8c-e2a9-4&from=paste&height=383&id=ub8800dc4&originHeight=383&originWidth=966&originalType=binary&ratio=1&rotation=0&showTitle=false&size=336840&status=done&style=none&taskId=uf5adc9f2-b610-4866-9b65-cf6505cbbcf&title=&width=966)
```python
# coding:utf-8
# 自定义一个变形器节点,通过调整ripple改变多边形的形状
import math

import maya.OpenMaya as OpenMaya
import maya.OpenMayaMPx as OpenMayaMPx  # 制作自定义的东西时需要的模块
import sys  # 输出错误所需要的模块

nodeName = "RippleDeformer"  # 定义节点的名字
nodeId = OpenMaya.MTypeId(0x102fff)


class Ripple(OpenMayaMPx.MPxDeformerNode):
    """
    Commands ----> MPxCommand
    Custom   ----> MPxNode
    Deformer ----> MPxDeformerNode
    """
    # 创建MObject类型的输入输出
    mObj_Displace = OpenMaya.MObject()
    mObj_Amplitude = OpenMaya.MObject()

    def __init__(self):
        OpenMayaMPx.MPxDeformerNode.__init__(self)

    def deform(self, dataBlock, geoIterator, matrix, geometryIndex):
        """
        变形器的核心参数
        :param dataBlock:数据块
        :param geoIterator: 迭代器，例如遍历一个几何体的所有顶点时用的到
        :param matrix: 矩阵   几何体的世界矩阵或受影响的网格
        :param geometryIndex: 几何索引，当使用多个几何体时，所有几何体都进入这个属性
        :return:
        """

        input = OpenMayaMPx.cvar.MPxGeometryFilter_input
        # 1. Attach a handle to input Array Attribute
        # 1. 为输入数组属性附加handle
        # 后来优化将inputArrayValue和inputValue都改为了output，可能是因为用output会自动检索最优路线吧
        dataHandleInputArray = dataBlock.outputArrayValue(input)
        # 2. Jump to particular element
        # 2. 跳转到特定元素
        dataHandleInputArray.jumpToElement(geometryIndex)
        # 3. Attach a handle to specific data block
        # 3. 将handle附加到特定的数据块
        dataHandleInputElement = dataHandleInputArray.outputValue()
        # 4. Reach to the child - inputGeom
        inputGeom = OpenMayaMPx.cvar.MPxGeometryFilter_inputGeom
        dataHandleInputGeom = dataHandleInputElement.child(inputGeom)
        inMesh = dataHandleInputGeom.asMesh()
        # Envelope
        envelope = OpenMayaMPx.cvar.MPxGeometryFilter_envelope
        dataHandleEnvelope = dataBlock.inputValue(envelope)
        envelopeValue = dataHandleEnvelope.asFloat()
        # Amplitude
        dataHandleAmplitude = dataBlock.inputValue(Ripple.mObj_Amplitude)
        amplitudeValue = dataHandleAmplitude.asFloat()
        # Displace
        dataHandleDisplace = dataBlock.inputValue(Ripple.mObj_Displace)
        displaceValue = dataHandleDisplace.asFloat()

        mFloatVectorArray_normal = OpenMaya.MFloatVectorArray()  # 创建一个MFloatVectorArray的对象，getVertexNormals方法需要用到
        mFnMesh = OpenMaya.MFnMesh(inMesh)
        # 第一个参数是angleWeighted，如果angleWeighted设置为false，则返回环绕面法线的简单平均值。第三个参数是设置空间为对象空间
        mFnMesh.getVertexNormals(False, mFloatVectorArray_normal, OpenMaya.MSpace.kObject)

        mPointArray_meshVert = OpenMaya.MPointArray()  # 创建一个空的存放点的数组
        while not geoIterator.isDone():

            pointPosition = geoIterator.position()
            weight = self.weightValue(dataBlock, geometryIndex, geoIterator.index())

            pointPosition.x = pointPosition.x + math.sin(geoIterator.index() + displaceValue) * amplitudeValue * \
                              mFloatVectorArray_normal[geoIterator.index()].x * weight * envelopeValue * 0.1
            pointPosition.y = pointPosition.y + math.sin(geoIterator.index() + displaceValue) * amplitudeValue * \
                              mFloatVectorArray_normal[geoIterator.index()].y * weight * envelopeValue * 0.1
            pointPosition.z = pointPosition.z + math.sin(geoIterator.index() + displaceValue) * amplitudeValue * \
                              mFloatVectorArray_normal[geoIterator.index()].z * weight * envelopeValue * 0.1
            # geoIterator.setPosition(pointPosition)
            mPointArray_meshVert.append(pointPosition)
            geoIterator.next()
        geoIterator.setAllPositions(mPointArray_meshVert)


def deformerCreator():
    nodePtr = OpenMayaMPx.asMPxPtr(Ripple())
    return nodePtr


def nodeInitializer():
    """
    写功能前先将流程写下来，然后每完成一个流程就标记一下那个流程
    Create Attributes  创建属性 - check
    Attach Attributes 附加属性 - check
    Design Circuitry 设计电路图 - check
    """
    # 1. creating a function set for numeric attributes
    # 创建数字属性的函数集，因为我们的自定义属性是数字的，因此创建对应的函数集
    mFnAttr = OpenMaya.MFnNumericAttribute()

    # 2. create the attributes
    # # 创建AttributeValue属性，短名为AttrVal，数据类型为float，默认值为0.0，由自定义类中的mObj_Amplitude（MObject类型）来接收
    Ripple.mObj_Amplitude = mFnAttr.create("AmplitudeValue", "AmplitudeVal", OpenMaya.MFnNumericData.kFloat, 0.0)
    mFnAttr.setKeyable(1)
    mFnAttr.setMin(0.0)
    mFnAttr.setMax(1.0)

    Ripple.mObj_Displace = mFnAttr.create("DisplaceValue", "DispVal", OpenMaya.MFnNumericData.kFloat, 0.0)
    mFnAttr.setKeyable(1)
    mFnAttr.setMin(0.0)
    mFnAttr.setMax(10.0)

    # 3. Attaching the attributes to the Node
    Ripple.addAttribute(Ripple.mObj_Amplitude)
    Ripple.addAttribute(Ripple.mObj_Displace)

    '''
    SWIG - Simplified Wrapper Interface Generator 简化 包装器 接口 生成器   
    是允许开发人员使用脚本语言包装C++代码的工具,因为maya核心是由C++编写的
    Autodesk 为我们提供了一种使用swig使用这些属性的方法
    '''
    outputGeom = OpenMayaMPx.cvar.MPxGeometryFilter_outputGeom

    # 4. Design circuitry
    Ripple.attributeAffects(Ripple.mObj_Amplitude, outputGeom)
    Ripple.attributeAffects(Ripple.mObj_Displace, outputGeom)


# Initialize the script plug-in
def initializePlugin(mobject):
    mplugin = OpenMayaMPx.MFnPlugin(mobject, "Violet", "1.0")  # maya准备mobject来创建一个针对Plugin的函数库,第二，三个参数为可选参数，分别代指编写人，版本号
    try:
        # 注册一个节点，第一个为节点名字，第二个为节点ID，第三个为创建节点指针的函数，第四个为节点初始化(定义节点的属性函数)，第五个为节点的分类（没有也不会报错，但是最好写上）
        mplugin.registerNode(nodeName, nodeId, deformerCreator, nodeInitializer, OpenMayaMPx.MPxNode.kDeformerNode)
    except:
        sys.stderr.write("Failed to register node: " + nodeName)  # 如果注册失败就输出错误
        raise


# Uninitialize the scrip plug-in
def uninitializePlugin(mobject):  # 取消初始化
    mplugin = OpenMayaMPx.MFnPlugin(mobject)
    try:
        mplugin.deregisterNode(nodeId)  # 使用函数库中的取消注册命令，只需要命令的名字不需要指针
    except:
        sys.stderr.write("Failed to de-register node: " + nodeName)  # 失败就输出错误
        raise

```
<a name="wFxjF"></a>
## 为自定义变形器添加辅助对象
什么是辅助对象/节点  Accessary object/nodes<br />创建它是为了方便用户使用变形功能用的。<br />辅助对象节点需要有两个特征：<br />1.它是帮助变形器变形的。2.当辅助对象被删除时，变形器节点也应当一起被删除<br />因为它是帮助变形器获得变形的，因此我们需要将它用在deformer函数中的transform中<br />为了实现当辅助对象被删除时，变形器也一起被删除，应当将辅助对象的世界度量属性与变形器节点的矩阵属性关联起来。<br />在本例中辅助节点就是一个定位器，可以通过定位器x轴的移动从而改变变形器中的变形效果。<br />添加过程：首先需要为变形器创建矩阵属性， 刚开始和之前的节点属性添加过程一样，在节点初始化中新建矩阵属性函数库，通过函数库创建属性（创建的同时由类中定义的空的MObject对象来接收）并设置权限（mFnMatrixAttr.setStorable(0)mFnMatrixAttr.setConnectable(1)），然后设计连接线路。初始化完成后在类中通过dataBlock得到指向数据的handle（MObject），然后通过这个handle得到Matrix的值。<br />然后为了完成创建辅助对象节点，我们需要定义Deformer类中的两个函数(AccessoryNodeSetup，AccessoryAttribute)。然后通过在变形器类中读取辅助对象的矩阵属性中的变换属性的值来改变变形器的算法，从而实现辅助对象影响变形效果。

1. AccessoryNodeSetup，这个函数是用来创建辅助对象物体，以及连接辅助对象的世界度量属性与变形器的矩阵属性

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1655432605455-522c19a4-857c-4f4d-8244-f17e2c19ab56.png#averageHue=%23040404&clientId=ub892ec0a-a81e-4&from=paste&height=506&id=u3071a54d&originHeight=506&originWidth=1394&originalType=binary&ratio=1&rotation=0&showTitle=false&size=114336&status=done&style=none&taskId=u6ae705cc-8421-471f-8a5e-7be26300feb&title=&width=1394)<br />属性之间的连接：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1655433502603-4bf82d23-95cf-4a15-b8a6-b51607a945dd.png#averageHue=%23040404&clientId=ub892ec0a-a81e-4&from=paste&height=1001&id=u972fcbec&originHeight=1001&originWidth=2359&originalType=binary&ratio=1&rotation=0&showTitle=false&size=423349&status=done&style=none&taskId=u57a561ed-8833-49e1-903c-cf8bc7a8373&title=&width=2359)<br />2.AccessoryAttribute，这个函数用来返回类中的MObject对象（Ripple.mObj_Matrix）<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1655432904503-ad1197bf-2ad1-4c5b-8f3f-660e93cddec9.png#averageHue=%23060606&clientId=ub892ec0a-a81e-4&from=paste&height=626&id=ua199e21a&originHeight=626&originWidth=910&originalType=binary&ratio=1&rotation=0&showTitle=false&size=111956&status=done&style=none&taskId=uc6d956e5-98f0-4a53-a093-e9070fa5e5a&title=&width=910)
```python
# coding:utf-8
# 自定义一个变形器节点,通过调整ripple改变多边形的形状
import math

import maya.OpenMaya as OpenMaya
import maya.OpenMayaMPx as OpenMayaMPx  # 制作自定义的东西时需要的模块
import sys  # 输出错误所需要的模块

nodeName = "RippleDeformer"  # 定义节点的名字
nodeId = OpenMaya.MTypeId(0x102fff)


class Ripple(OpenMayaMPx.MPxDeformerNode):
    """
    Commands ----> MPxCommand
    Custom   ----> MPxNode
    Deformer ----> MPxDeformerNode
    """
    # 创建MObject类型的输入输出
    mObj_Displace = OpenMaya.MObject()
    mObj_Amplitude = OpenMaya.MObject()
    mObj_Matrix = OpenMaya.MObject()

    def __init__(self):
        OpenMayaMPx.MPxDeformerNode.__init__(self)

    def deform(self, dataBlock, geoIterator, matrix, geometryIndex):
        """
        变形器的核心参数
        :param dataBlock:数据块
        :param geoIterator: 迭代器，例如遍历一个几何体的所有顶点时用的到
        :param matrix: 矩阵   几何体的世界矩阵或受影响的网格
        :param geometryIndex: 几何索引，当使用多个几何体时，所有几何体都进入这个属性
        :return:
        """

        input = OpenMayaMPx.cvar.MPxGeometryFilter_input
        # 1. Attach a handle to input Array Attribute
        # 1. 为输入数组属性附加handle
        # 后来优化将inputArrayValue和inputValue都改为了output，可能是因为用output会自动检索最优路线吧
        dataHandleInputArray = dataBlock.outputArrayValue(input)
        # 2. Jump to particular element
        # 2. 跳转到特定元素
        dataHandleInputArray.jumpToElement(geometryIndex)
        # 3. Attach a handle to specific data block
        # 3. 将handle附加到特定的数据块
        dataHandleInputElement = dataHandleInputArray.outputValue()
        # 4. Reach to the child - inputGeom
        inputGeom = OpenMayaMPx.cvar.MPxGeometryFilter_inputGeom
        dataHandleInputGeom = dataHandleInputElement.child(inputGeom)
        inMesh = dataHandleInputGeom.asMesh()
        # Envelope
        envelope = OpenMayaMPx.cvar.MPxGeometryFilter_envelope
        dataHandleEnvelope = dataBlock.inputValue(envelope)
        envelopeValue = dataHandleEnvelope.asFloat()
        # Amplitude
        dataHandleAmplitude = dataBlock.inputValue(Ripple.mObj_Amplitude)
        amplitudeValue = dataHandleAmplitude.asFloat()
        # Displace
        dataHandleDisplace = dataBlock.inputValue(Ripple.mObj_Displace)
        displaceValue = dataHandleDisplace.asFloat()
        # Matrix
        dataHandleMatrix = dataBlock.inputValue(Ripple.mObj_Matrix)
        matrixValue = dataHandleMatrix.asMatrix()

        # 从矩阵中读取变换信息
        mTransMatrix = OpenMaya.MTransformationMatrix(matrixValue)
        translationValue = mTransMatrix.getTranslation(OpenMaya.MSpace.kObject)

        mFloatVectorArray_normal = OpenMaya.MFloatVectorArray()  # 创建一个MFloatVectorArray的对象，getVertexNormals方法需要用到
        mFnMesh = OpenMaya.MFnMesh(inMesh)
        # 第一个参数是angleWeighted，如果angleWeighted设置为false，则返回环绕面法线的简单平均值。第三个参数是设置空间为对象空间
        mFnMesh.getVertexNormals(False, mFloatVectorArray_normal, OpenMaya.MSpace.kObject)

        mPointArray_meshVert = OpenMaya.MPointArray()  # 创建一个空的存放点的数组
        while not geoIterator.isDone():
            pointPosition = geoIterator.position()
            weight = self.weightValue(dataBlock, geometryIndex, geoIterator.index())

            pointPosition.x = pointPosition.x + math.sin(
                geoIterator.index() + displaceValue + translationValue[0]) * amplitudeValue * mFloatVectorArray_normal[
                                  geoIterator.index()].x * weight * envelopeValue * 0.1
            pointPosition.y = pointPosition.y + math.sin(
                geoIterator.index() + displaceValue + translationValue[0]) * amplitudeValue * mFloatVectorArray_normal[
                                  geoIterator.index()].y * weight * envelopeValue * 0.1
            pointPosition.z = pointPosition.z + math.sin(
                geoIterator.index() + displaceValue + translationValue[0]) * amplitudeValue * mFloatVectorArray_normal[
                                  geoIterator.index()].z * weight * envelopeValue * 0.1
            # geoIterator.setPosition(pointPosition)
            mPointArray_meshVert.append(pointPosition)
            geoIterator.next()
        geoIterator.setAllPositions(mPointArray_meshVert)

    def accessoryNodeSetup(self, dagModifier):
        # 1.创建辅助对象
        mObjLocator = dagModifier.createNode('locator')

        # 2.将辅助对象与变形器之间建立联系
        mFnDependLocator = OpenMaya.MFnDependencyNode(mObjLocator)
        mPlugWorld = mFnDependLocator.findPlug('worldMatrix')
        mObj_WorldAttr = mPlugWorld.attribute()

        mStatusConnect = dagModifier.connect(mObjLocator, mObj_WorldAttr, self.thisMObject(), Ripple.mObj_Matrix)
        return mStatusConnect  # 返回连接状态

    def accessoryAttribute(self):
        return Ripple.mObj_Matrix


def deformerCreator():
    nodePtr = OpenMayaMPx.asMPxPtr(Ripple())
    return nodePtr


def nodeInitializer():
    """
    写功能前先将流程写下来，然后每完成一个流程就标记一下那个流程
    Create Attributes  创建属性 - check
    Attach Attributes 附加属性 - check
    Design Circuitry 设计电路图 - check
    """
    # 1. creating a function set for numeric attributes
    # 创建数字属性的函数集，因为我们的自定义属性是数字的，因此创建对应的函数集
    mFnAttr = OpenMaya.MFnNumericAttribute()

    # 2. create the attributes
    # # 创建AttributeValue属性，短名为AttrVal，数据类型为float，默认值为0.0，由自定义类中的mObj_Amplitude（MObject类型）来接收
    Ripple.mObj_Amplitude = mFnAttr.create("AmplitudeValue", "AmplitudeVal", OpenMaya.MFnNumericData.kFloat, 0.0)
    mFnAttr.setKeyable(1)
    mFnAttr.setMin(0.0)
    mFnAttr.setMax(1.0)

    Ripple.mObj_Displace = mFnAttr.create("DisplaceValue", "DispVal", OpenMaya.MFnNumericData.kFloat, 0.0)
    mFnAttr.setKeyable(1)
    mFnAttr.setMin(0.0)
    mFnAttr.setMax(10.0)

    # 创建矩阵属性
    mFnMatrixAttr = OpenMaya.MFnMatrixAttribute()
    Ripple.mObj_Matrix = mFnMatrixAttr.create('MatrixAttribute', 'matAttr')
    mFnMatrixAttr.setStorable(0)
    mFnMatrixAttr.setConnectable(1)

    # 3. Attaching the attributes to the Node  # 添加属性到节点上
    Ripple.addAttribute(Ripple.mObj_Amplitude)
    Ripple.addAttribute(Ripple.mObj_Displace)
    Ripple.addAttribute(Ripple.mObj_Matrix)

    '''
    SWIG - Simplified Wrapper Interface Generator 简化 包装器 接口 生成器   
    是允许开发人员使用脚本语言包装C++代码的工具,因为maya核心是由C++编写的
    Autodesk 为我们提供了一种使用swig使用这些属性的方法
    '''
    outputGeom = OpenMayaMPx.cvar.MPxGeometryFilter_outputGeom

    # 4. Design circuitry  # 设计节点属性的连接
    Ripple.attributeAffects(Ripple.mObj_Amplitude, outputGeom)
    Ripple.attributeAffects(Ripple.mObj_Displace, outputGeom)
    Ripple.attributeAffects(Ripple.mObj_Matrix, outputGeom)


# Initialize the script plug-in
def initializePlugin(mobject):
    mplugin = OpenMayaMPx.MFnPlugin(mobject, "Violet", "1.0")  # maya准备mobject来创建一个针对Plugin的函数库,第二，三个参数为可选参数，分别代指编写人，版本号
    try:
        # 注册一个节点，第一个为节点名字，第二个为节点ID，第三个为创建节点指针的函数，第四个为节点初始化(定义节点的属性函数)，第五个为节点的分类（没有也不会报错，但是最好写上）
        mplugin.registerNode(nodeName, nodeId, deformerCreator, nodeInitializer, OpenMayaMPx.MPxNode.kDeformerNode)
    except:
        sys.stderr.write("Failed to register node: " + nodeName)  # 如果注册失败就输出错误
        raise


# Uninitialize the scrip plug-in
def uninitializePlugin(mobject):  # 取消初始化
    mplugin = OpenMayaMPx.MFnPlugin(mobject)
    try:
        mplugin.deregisterNode(nodeId)  # 使用函数库中的取消注册命令，只需要命令的名字不需要指针
    except:
        sys.stderr.write("Failed to de-register node: " + nodeName)  # 失败就输出错误
        raise

```
<a name="K5V9V"></a>
# 第十六集 创建自定义定位器
参考网站：[https://blog.csdn.net/u013148608/article/details/105694909](https://blog.csdn.net/u013148608/article/details/105694909)<br />因为新版本已经不支持这个了glRenderer = OpenMayaRender.MHardwareRenderer.theRenderer()，因此就这吧，看看就好。<br />步骤：1.定义定位器的形状2.定义边界框3.定义边界框边界的大小<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1655434694335-baa8031d-3036-4e93-ae91-207533fc49ef.png#averageHue=%23060606&clientId=ub892ec0a-a81e-4&from=paste&height=511&id=CWn3U&originHeight=511&originWidth=1206&originalType=binary&ratio=1&rotation=0&showTitle=false&size=121606&status=done&style=none&taskId=u26739e54-5b7f-4842-a6b6-5e0dfe2922f&title=&width=1206)
```python
# coding:utf-8
# 自定义一个节点，制作轮子效果
import maya.OpenMaya as OpenMaya
import maya.OpenMayaMPx as OpenMayaMPx  # 制作自定义的东西时需要的模块
import sys  # 输出错误所需要的模块
import maya.OpenMayaRender as OpenMayaRender

nodeName = "LeftFoot"  # 定义节点的名字
nodeId = OpenMaya.MTypeId(0x100fff)

glRenderer = OpenMayaRender.MHardwareRenderer.theRenderer()
glFT = glRenderer.glFunctionTable()  # 得到函数库指针


class LocatorNode(OpenMayaMPx.MPxLocatorNode):

    def __init__(self):
        OpenMayaMPx.MPxLocatorNode.__init__(self)

    def compute(self, plug, dataBlock):
        return OpenMaya.kUnknownParameter

    def draw(self, view, path, style, status):
        view.beginGL()
        # Pushed current State
        glFT.glPushAttrib(OpenMayaRender.MGL_CURRENT_BIT)
        # Enabled Blend mode （to enable transparency）
        glFT.glEnable(OpenMayaRender.MGL_BLEND)
        # Defined Blend function
        glFT.glBlendFunc(OpenMayaRender.MGL_SRC_ALPHA, OpenMayaRender.MGL_ONE_MINUS_SRC_ALPHA)

        # 定义shape在不同选择模式下对应的颜色
        if status == view.kActive:
            glFT.glColor4f(0.2, 0.5, 0.1, 0.3)
        elif status == view.kLead:
            glFT.glColor4f(0.5, 0.2, 0.1, 0.3)
        elif status == view.kDormant:
            glFT.glColor4f(0.1, 0.1, 0.1, 0.3)

        # Draw a shape
        glFT.glBegin()
        glFT.glVertex3f(-0.031, 0, -2.875)
        glFT.glVertex3f(-0.939, 0.1, -2.370)
        glFT.glVertex3f(-1.175, 0.2, -1.731)
        glFT.glVertex3f(-0.603, 0.3, 1.060)
        glFT.glVertex3f(-0.473, 0.3, 1.026)
        glFT.glVertex3f(-0.977, 0.2, -1.731)
        glFT.glVertex3f(-0.809, 0.1, -2.337)
        glFT.glVertex3f(-0.035, 0, -2.807)
        glFT.glEnd()
        # Draw a shape
        glFT.glBegin()
        glFT.glVertex3f(-0.587, 0.3, 1.33)
        glFT.glVertex3f(0.442, 0.3, 1.33)
        glFT.glVertex3f(0.442, 0.3, 1.92)
        glFT.glVertex3f(0.230, 0.3, 2.24)
        glFT.glVertex3f(-0.442, 0.3, 2.25)
        glFT.glVertex3f(-0.635, 0.3, 1.92)
        glFT.glVertex3f(-0.567, 0.3, 1.35)
        glFT.glEnd()

        # 定义文字在不同选择模式下对应的颜色
        if status == view.kActive:
            glFT.glColor4f(0.2, 0.5, 0.1, 1)
        elif status == view.kLead:
            glFT.glColor4f(0.5, 0.2, 0.1, 1)
        elif status == view.kDormant:
            glFT.glColor4f(0.1, 0.1, 0.1, 1)

        # 在0，0，0处绘制文字，对齐方式为向左对齐
        view.drawText("Left Foot", OpenMaya.MPoint(0, 0, 0), view.kLeft)

        # Disable Blend mode
        glFT.glDisable(OpenMayaRender.MGL_BLEND)
        # Restore the state
        glFT.glPopAttrib()
        view.endGL()


def nodeCreator():
    return OpenMayaMPx.asMPxPtr(LocatorNode())


def nodeInitializer():
    pass


# Initialize the script plug-in
def initializePlugin(mobject):
    mplugin = OpenMayaMPx.MFnPlugin(mobject, "Violet", "1.0")  # maya准备mobject来创建一个针对Plugin的函数库,第二，三个参数为可选参数，分别代指编写人，版本号
    try:
        # 注册一个节点，第一个为节点名字，第二个为节点ID，第三个为创建节点指针的函数，第四个为节点初始化(定义节点的属性函数)，第五个为节点的分类（没有也不会报错，但是最好写上）
        mplugin.registerNode(nodeName, nodeId, nodeCreator, nodeInitializer, OpenMayaMPx.MPxNode.kLocatorNode)
    except:
        sys.stderr.write("Failed to register node: " + nodeName)  # 如果注册失败就输出错误


# Uninitialize the scrip plug-in
def uninitializePlugin(mobject):  # 取消初始化
    mplugin = OpenMayaMPx.MFnPlugin(mobject)
    try:
        mplugin.deregisterCommand(nodeId)  # 使用函数库中的取消注册命令，只需要命令的名字不需要指针
    except:
        sys.stderr.write("Failed to de-register node: " + nodeName)  # 失败就输出错误

```
<a name="CiqwY"></a>
# 第十七~十九集 无缝IKFK混合与回调函数
先解释一下回调函数，回调函数可以理解为把函数当成变量传递给另一个函数，当变量的函数改变时也会同样的影响把函数当变量的那个函数。作为参数传递的那个函数叫做回调函数<br />我们通常通过MMessage来实现事件触发，当事件触发时会调用回调函数。<br />MMessage的种类与事件：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1655474585450-23dc0aae-bfe2-49f7-91f2-3472d0399f45.png#averageHue=%23080808&clientId=u12cb03d8-4911-4&from=paste&height=1080&id=u0168e800&originHeight=1080&originWidth=1920&originalType=binary&ratio=1&rotation=0&showTitle=false&size=675921&status=done&style=none&taskId=u915aca16-8e9c-4596-b6bc-1e221be0a76&title=&width=1920)

什么是IK FK ，IK是反向运动学，它是子关节影响父关节，FK是正向运动学，它是父关节影响子关节。<br />当我们制作IK时当添加了极向量约束时，我们将不能够通过父关节的旋转而影响子关节，因此制作一个在极向量约束的功能存在的情况下依然能够正确进行子关节影响父关节并且父关节也可以旋转影响子关节。![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1655451525648-15631070-d361-4cb5-bd07-2e58bd3f35da.png#averageHue=%2355606d&clientId=ub892ec0a-a81e-4&from=paste&height=467&id=u899fa463&originHeight=467&originWidth=1296&originalType=binary&ratio=1&rotation=0&showTitle=false&size=301680&status=done&style=none&taskId=uff6cc5ff-8a73-40c6-aa4b-532b25c2c9a&title=&width=1296)<br />这个功能制作的关键是当添加IK后，关节会出现一个属性IKBlend 这个属性为1时则子关节移动会影响父关节，父关节不能主动移动，当IKBlend属性为0时，子关节的移动就不会影响父关节，父关节的旋转会带动子关节。以及如果父关节旋转后中间的那个受极向量约束的定位器位置也应该随着改变。
<a name="QKLlY"></a>
## 代码实现细节
我们要制作一个节点来实现这些功能，因此使用最开始的自定义轮子节点来写代码。<br />将轮子结点复制过来后更改一下初始设置：更改节点名字，将类名通过shift+F6统一改成CVG，然后因为节点不需要属性以及算法，将compute函数和nodeInitializer函数内容统统改为pass<br />定义两个模式，一个是FK，一个是IK，默认模式是FK，当我们选择IK控制柄或者选择joint3，或者选择极向量控制器，都会使模式切换成IK。<br />模式为FK时IKBlend的值设为0，并且将极向量控制器设置为不显示，因为FK模式下用不到极向量控制器，模式为IK时IKBlend的值设为1.并将极向量控制器约束在joint2的位置上。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1655457511797-ad9fe3f2-fe5f-489d-95d3-b2252c40c416.png#averageHue=%23020202&clientId=ub892ec0a-a81e-4&from=paste&height=1373&id=u700e4900&originHeight=1373&originWidth=2547&originalType=binary&ratio=1&rotation=0&showTitle=false&size=427712&status=done&style=none&taskId=ucc4d2933-c7e0-4569-9e5a-35ac3b8644d&title=&width=2547)
```python
# coding:utf-8
# 自定义一个节点，制作轮子效果
import maya.OpenMaya as OpenMaya
import maya.OpenMayaMPx as OpenMayaMPx  # 制作自定义的东西时需要的模块
import sys  # 输出错误所需要的模块

nodeName = "CVGKNode"  # 定义节点的名字
nodeId = OpenMaya.MTypeId(0x100fff)


class CVG(OpenMayaMPx.MPxNode):
    idCallback = []  # 用来存放所有的回调函数

    joint1 = OpenMaya.MObject()
    joint2 = OpenMaya.MObject()
    joint3 = OpenMaya.MObject()

    activeEffector = OpenMaya.MObject()
    activeHandle = OpenMaya.MObject()
    activePoleVector = OpenMaya.MObject()
    activePoleVectorControl = OpenMaya.MObject()

    def __init__(self):
        OpenMayaMPx.MPxNode.__init__(self)
        # Event Callback  根据事件调用函数  这里添加的事件是当前选择改变时调用函数
        self.idCallback.append(OpenMaya.MEventMessage.addEventCallback("SelectionChanged", self.callbackFunc))
        # DG Callback  根据节点的改变调用函数  这里是节点移除时
        self.idCallback.append(OpenMaya.MDGMessage.addNodeRemovedCallback(self.remove, "dependNode"))

    def callbackFunc(self, *args):  # 当选择的物体发生改变时调用这个函数
        print "Callback Function"
        # 1. Find active selection in the scene 在场景中找到主动选择
        mSel = OpenMaya.MSelectionList()
        OpenMaya.MGlobal.getActiveSelectionList(mSel)  # 将选择的物体添加到列表中
        mItSelectionList = OpenMaya.MItSelectionList(mSel, OpenMaya.MFn.kDagNode)
        mode = "fk"

        mFnDependencyNode = OpenMaya.MFnDependencyNode()

        # 2. Find IK-Effector
        while not mItSelectionList.isDone():
            mObj = OpenMaya.MObject()
            mItSelectionList.getDependNode(mObj)
            # If effector itself is selected 如果效应器本身被选择
            if mObj.apiTypeStr() == "kIkEffector":
                self.activeEffector = mObj
                mode = "ik"
                break
            # If control curve is selected 如果选择控制曲线(极向量约束的那个)
            if self.activePoleVectorControl.apiTypeStr() != "kInvalid":
                if OpenMaya.MFnDependencyNode(mObj).name() == OpenMaya.MFnDependencyNode(
                        self.activePoleVectorControl).name():
                    mode = "ik"
                    break
            mFnDependencyNode.setObject(mObj)
            mPlugArray_joint = OpenMaya.MPlugArray()
            mFnDependencyNode.getConnections((mPlugArray_joint))
            # Check If effector is connected to selected object
            for i in xrange(mPlugArray_joint.length()):
                mPlug_joint = mPlugArray_joint[i]
                mPlugArray2 = OpenMaya.MPlugArray()
                mPlug_joint.connectedTo(mPlugArray2, True, True)
                mPlug2 = mPlugArray2[0]
                if mPlug2.node().apiTypeStr() == "kIkEffector":
                    self.activeEffector = mPlug2.node()
                    mode = "ik"
                    break
                mItSelectionList.next()
            # 3. Fink IK-Handle
            # print self.activeEffector.apiTypeStr()
            '''
            If IK-Effector is found then :
            - find IK-Handle
            '''
            if self.activeEffector.apiTypeStr() == "kIkEffector":
                mFnDependencyNode.setObject(self.activeEffector)
                mPlugArray_effector = OpenMaya.MPlugArray()
                mFnDependencyNode.getConnections(mPlugArray_effector)
                for i in xrange(mPlugArray_effector.length()):
                    mPlug_effector = mPlugArray_effector[i]
                    mPlugArray2 = OpenMaya.MPlugArray()
                    mPlug_effector.connectedTo(mPlugArray2, True, True)
                    mPlug2 = mPlugArray2[0]
                    if mPlug2.node().apiTypeStr() == "kIkHandle":
                        self.activeHandle = mPlug2.node()
                        break

                """
                If IK-Handle is found then:
                -find IK-Blend Plug
                -find IK-PoleVector
                """

            if self.activeHandle.apiTypeStr() == "kIkHandle":
                # 4. Find IK-Blend Plug
                mFnDependencyNodeHandle = OpenMaya.MFnDependencyNode(self.activeHandle)
                mPlug_blendAttr = mFnDependencyNodeHandle.findPlug("ikBlend")
                mAttr_blendAttr = mPlug_blendAttr.attribute()
                # mak IK-blend attribute "unKeyable" and hidden from Channel box
                mMFnAttribute = OpenMaya.MFnAttribute(mAttr_blendAttr)
                mMFnAttribute.setKeyable(0)
                mMFnAttribute.setChannelBox(0)

                # 5. Find Pole Vector Constraint
                mFnDependencyNode.setObject(self.activeHandle)
                mPlugArray_handle = OpenMaya.MPlugArray()
                mFnDependencyNode.getConnections(mPlugArray_handle)
                for i in xrange(mPlugArray_handle.length()):
                    mPlug_handle = mPlugArray_handle[i]
                    mPlugArray2 = OpenMaya.MPlugArray()
                    mPlug_handle.connectedTo(mPlugArray2, True, True)
                    mPlug2 = mPlugArray2[0]
                    if mPlug2.node().apiTypeStr() == "kPoleVectorConstraint":
                        self.activePoleVector = mPlug2.node()
                        break

                """
                If IK-PoleVector is found then:
                - find IK-PoleVector Control Curve
                """

                if self.activePoleVector.apiTypeStr() == "kPoleVectorConstraint":
                    # 6. Find Curve controlling Pole Vector
                    mFnDependencyNode.setObject(self.activePoleVector)
                    mPlugArray_handle = OpenMaya.MPlugArray()
                    mFnDependencyNode.getConnections(mPlugArray_handle)
                    for i in xrange(mPlugArray_handle.length()):
                        mPlug_handle = mPlugArray_handle[i]
                        mPlugArray2 = OpenMaya.MPlugArray()
                        mPlug_handle.connectedTo(mPlugArray2, True, True)
                        mPlug2 = mPlugArray2[0]
                        if mPlug2.node().apiTypeStr() == "kTransform":
                            self.activePoleVectorControl = mPlug2.node()
                            break

                    """
                    If IK-PoleVector Control Curve is found then:
                    - find middle joint of joint change, to whick this control should be attached.
                    """
                    if self.activePoleVectorControl.apiTypeStr() == "kTransform":
                        # 7. Find Joint2 of the chain.
                        # 7. a : find joint connected to IK-Effector - call it : Joint3
                        # 7. b : find joint connected to IK-Handle   - call it : Joint1
                        # 7. c : find joint connected to Joint1 and Joint3 - call it Joint2

                        # 7. a : find joint connected to IK-Effector - call it : Joint3
                        mFnDependencyNode.setObject(self.activeEffector)
                        mPlugArray_effector = OpenMaya.MPlugArray()
                        mFnDependencyNode.getConnections(mPlugArray_effector)
                        for i in xrange(mPlugArray_effector.length()):
                            mPlug_effector = mPlugArray_effector[i]
                            mPlugArray2 = OpenMaya.MPlugArray()
                            mPlug_effector.connectedTo(mPlugArray2,True,True)
                            mPlug2 = mPlugArray2[0]
                            if mPlug2.node().apiTypeStr() == "kJoint":
                                self.joint3 = mPlug2.node()
                                break
                        # b : find joint connected to IK-Handle   - call it : Joint1
                        mFnDependencyNode.setObject(self.activeHandle)
                        mPlugArray_handle = OpenMaya.MPlugArray()
                        mFnDependencyNode.getConnections(mPlugArray_handle)
                        for i in xrange(mPlugArray_handle.length()):
                            mPlug_handle = mPlugArray_handle[i]
                            mPlugArray2 = OpenMaya.MPlugArray()
                            mPlug_handle.connectedTo(mPlugArray2, True, True)
                            mPlug2 = mPlugArray2[0]
                            if mPlug2.node().apiTypeStr() == "kJoint":
                                self.joint1 = mPlug2.node()
                                break
                        # 7. c : find joint connected to Joint1 and Joint3 - call it Joint2
                        """
                        Find joints connected to Joint1 , and if any joint which is connected to Joint1 is also connected to Joint3
                        then it is Joint2
                        """
                        mObj_joint1Connections = OpenMaya.MObjectArray()
                        mObj_joint3Connections = OpenMaya.MObjectArray()

                        # Collect child Joints connected to Joint1
                        mFnDependencyNode.setObject(self.joint1)
                        mPlugArray_joint1 = OpenMaya.MPlugArray()
                        mPlug_joint1Scale = mFnDependencyNode.findPlug("scale")
                        mPlugArray_joint1 = OpenMaya.MPlugArray()
                        mPlug_joint1Scale.connectedTo(mPlugArray_joint1,True,True)
                        for i in xrange(mPlugArray_joint1.length()):
                            if mPlugArray_joint1[i].node().apiTypeStr() == "kJoint":
                                mObj_joint1Connections.append(mPlugArray_joint1[i].node())

                        # Collect parent Joints connected to Joint3
                        mFnDependencyNode.setObject(self.joint3)
                        mPlugArray_joint3 = OpenMaya.MPlugArray()
                        mPlug_joint3Scale = mFnDependencyNode.findPlug("inverseScale")
                        mPlugArray_joint3 = OpenMaya.MPlugArray()
                        mPlug_joint3Scale.connectedTo(mPlugArray_joint3,True,True)
                        for i in xrange(mPlugArray_joint3.length()):
                            if mPlugArray_joint3[i].node().apiTypeStr() == "kJoint":
                                mObj_joint3Connections.append(mPlugArray_joint3[i].node())

                        mFnDependencyNode_temp1 = OpenMaya.MFnDependencyNode()
                        mFnDependencyNode_temp3 = OpenMaya.MFnDependencyNode()

                        for i in xrange(mObj_joint3Connections.length()):
                            for j in xrange(mObj_joint3Connections.length()):

                                mFnDependencyNode_temp1.setObject(mObj_joint1Connections[i])
                                mFnDependencyNode_temp3.setObject(mObj_joint3Connections[j])
                                if mFnDependencyNode_temp1.name() == mFnDependencyNode_temp3.name():
                                    self.joint2 = mObj_joint3Connections[j]
                                    break




    def remove(self, *args):
        try:
            # check if this node exists in the scene  先检查这个节点在场景中是否存在
            # 尝试将通过我们自定义的CVG类的MObject传递给一个空的列表，如果出现错误就代表没有使用过，那么就删除回调函数。如果列表不为空那么就不进行其他操作。
            OpenMaya.MSelectionList.add(self.thisMObject())
        except:
            # Remove callback  移除回调函数
            for i in xrange(len(self.idCallback)):
                try:  # 尝试移除属于MEventMessage的回调函数
                    OpenMaya.MEventMessage.removeCallback(self.idCallback[i])
                except:
                    pass
                try:  # 常识移除属于MDGMessage的回调函数
                    OpenMaya.MDGMessage.removeCallback(self.idCallback[i])
                except:
                    pass

    def compute(self, plug, dataBlock):
        pass


def nodeCreator():
    return OpenMayaMPx.asMPxPtr(CVG())


def nodeInitializer():
    pass


# Initialize the script plug-in
def initializePlugin(mobject):
    mplugin = OpenMayaMPx.MFnPlugin(mobject, "Violet", "1.0")  # maya准备mobject来创建一个针对Plugin的函数库,第二，三个参数为可选参数，分别代指编写人，版本号
    try:
        # 注册一个节点，第一个为节点名字，第二个为节点ID，第三个为创建节点指针的函数，第四个为节点初始化(定义节点的属性函数)，第五个为节点的分类（没有也不会报错，但是最好写上）
        mplugin.registerNode(nodeName, nodeId, nodeCreator, nodeInitializer)
    except:
        sys.stderr.write("Failed to register node: " + nodeName)  # 如果注册失败就输出错误


# Uninitialize the scrip plug-in
def uninitializePlugin(mobject):  # 取消初始化
    mplugin = OpenMayaMPx.MFnPlugin(mobject)
    try:
        mplugin.deregisterCommand(nodeId)  # 使用函数库中的取消注册命令，只需要命令的名字不需要指针
    except:
        sys.stderr.write("Failed to de-register node: " + nodeName)  # 失败就输出错误

```
