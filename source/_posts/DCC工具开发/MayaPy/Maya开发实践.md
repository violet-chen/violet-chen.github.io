---
title: Maya开发实践
tags: MayaPy
categories: DCC工具开发
abbrlink: 14ce52f1
date: 2023-08-29 03:57:00
---
<meta name="referrer" content="no-referrer" />

<a name="n8BWl"></a>
# 第一节
<a name="tHDPL"></a>
## Maya帮助文档的查阅方法

![image.png](https://lyzz.top/file/40770)<br />第一个框住的是命令的名称，也可以叫他函数<br />第二个框住的是命令的标识与参数，只需要在其中找到自己需要的几个使用就可以了<br />第三个框住的是返回值<br />第四个框住的是与查询的命令相似的命令<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648298887735-1e30d740-1aa5-4c47-b499-823769712273.png#averageHue=%23f6f5f4&clientId=u72970d88-4bcf-4&from=paste&height=557&id=ub8a467f2&originHeight=557&originWidth=1510&originalType=binary&ratio=1&rotation=0&showTitle=false&size=56812&status=done&style=none&taskId=u2dda7fa0-d51f-4def-836a-563e746f48e&title=&width=1510)<br />Flags下面是命令的标识与参数的使用方法<br />最左边是每个标识的全称与简称，中间是标识所需要的参数的数量与类型，右边是标识的特性<br />标识的特性介绍：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648299084864-38a11f11-3738-4db3-a7ce-c34f544b486a.png#averageHue=%23a1a19d&clientId=u72970d88-4bcf-4&from=paste&height=456&id=u6bbdbe28&originHeight=456&originWidth=1708&originalType=binary&ratio=1&rotation=0&showTitle=false&size=329338&status=done&style=none&taskId=u498d9385-1785-41c1-8bce-ed4be7b74b4&title=&width=1708)<br />介绍一下M：例如设置球体半径，因为球体半径只有一个值，因此不能多次使用，但是创建曲线的时候，曲线由许多点构成，每个点都有不同的数值，在创建时可以多次使用他点位置的标识，然后跟上不同点的坐标，然后来创建一个曲线。<br />命令帮助文档的最下方是官方的帮助案例<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648299280163-7bbbd788-757d-4fb8-b1f2-c463e4046daf.png#averageHue=%23f3f3f3&clientId=u72970d88-4bcf-4&from=paste&height=213&id=ud1f66f23&originHeight=213&originWidth=605&originalType=binary&ratio=1&rotation=0&showTitle=false&size=8419&status=done&style=none&taskId=uc33f9dc5-72f4-4ded-be4a-dda3621ffa7&title=&width=605)
<a name="HuDs0"></a>
## 如何在maya中使用python
maya的命令在python中是以包的模式出现的。要使用maya的命令必须要先导入模块才能进行调用。<br />MEL命令与python命令在参数或者标识上调用的区别：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648299745648-a3385da8-444e-4ac2-b6de-7ef26f72a26e.png#averageHue=%23605e4f&clientId=u72970d88-4bcf-4&from=paste&height=955&id=u26ac150b&originHeight=955&originWidth=1844&originalType=binary&ratio=1&rotation=0&showTitle=false&size=481675&status=done&style=none&taskId=u12c00128-6c3f-4884-b0b2-9bba71a2170&title=&width=1844)
<a name="Q6Dig"></a>
# 第二节
<a name="x1FfQ"></a>
## 获取场景中的操作对象
在编程中，在确定对一个物体进行操作之前需要通过命令找到要操作的对象。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648345237495-517645ca-74ef-43a5-a6f2-f7542e62ecdb.png#averageHue=%23474744&clientId=ue82b3c53-47c5-4&from=paste&height=582&id=u49798923&originHeight=582&originWidth=1437&originalType=binary&ratio=1&rotation=0&showTitle=false&size=234325&status=done&style=none&taskId=u486e58b3-21cd-46f4-803d-da6397294b0&title=&width=1437)

1. 通过对象的名字获取单一物体
2. 通过类型获取一类物体
3. 通过UUID获取某一物体（在名字出现重复的情况下）

获取对象的命令：ls<br />mc.ls()返回的结果是场景中所有的节点名称的列表<br />mc.ls(sl=True)返回的结果是在窗口的选择的对象的名称  sl是selection的简称<br />mc.ls(typ=('mesh','nurbsCurve')) 作用是列举场景中的所有多边形和曲线两种类型的物体，typ是tpye的简称，因为type是python的关键字所以使用在maya中使用typ<br />ls命令列举的名字都是短名（物体本身的名字），为了防止出现重名的情况,通过long=True列举它们的长名<br />mc.ls(typ=('mesh','nurbsCurve'),long=True) 

如果想要列出指定类型的所有对象，但不列出该类型的后代对象。例如想要列举transform类型的对象（模型曲线等）但不想要列举由transform扩展出来的对象（例如骨骼）就可以通过**exactType（et）**<br />mc.ls(et='transform')<br />mc.ls(ext='transform')       # excludeType(ext) 列举除了transform类型外的所有物体<br />根据名字过滤物体：<br />mc.ls("*_cn_*")  # *号代表多个字母<br />mc.ls("blendShape??Set") # 一个?号代表一个字符<br />根据UUID选择物体：<br />UUID查询方法：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648347037508-2dca9d1b-e5f5-4580-821f-390623c21cac.png#averageHue=%234c4b4a&clientId=ue82b3c53-47c5-4&from=paste&height=466&id=u09e4f771&originHeight=466&originWidth=494&originalType=binary&ratio=1&rotation=0&showTitle=false&size=23392&status=done&style=none&taskId=ub65ca394-320a-4e77-bd84-da63feb45cd&title=&width=494)"<br />mc.("UUID的名字")<br />ls命令参数：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648347140198-39287a14-8575-4491-936a-cd3c0dd95df9.png#averageHue=%239cb0cc&clientId=ue82b3c53-47c5-4&from=paste&height=929&id=u220f1100&originHeight=929&originWidth=1735&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1248469&status=done&style=none&taskId=u319a3e4f-e320-4e4d-a8c3-302a842b37c&title=&width=1735)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648347152462-ba8b85e2-60af-4326-8624-c7c33db74c2a.png#averageHue=%2398adcb&clientId=ue82b3c53-47c5-4&from=paste&height=927&id=u2d696a29&originHeight=927&originWidth=1730&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1375151&status=done&style=none&taskId=ua7043b23-a9c8-43af-b3b8-6f7d3243bfe&title=&width=1730)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648347179521-2b39c4e1-679b-4fb4-8c8c-6d609e49df4c.png#averageHue=%239bb0cf&clientId=ue82b3c53-47c5-4&from=paste&height=929&id=u99c6f9eb&originHeight=929&originWidth=1732&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1121096&status=done&style=none&taskId=u92937644-7185-4c3e-8872-397860f66b6&title=&width=1732)
<a name="pOJGE"></a>
## rename命令
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648347220026-7e04c1af-745c-484f-b58b-44359d9bb392.png#averageHue=%23363636&clientId=ue82b3c53-47c5-4&from=paste&height=436&id=ub1721049&originHeight=436&originWidth=745&originalType=binary&ratio=1&rotation=0&showTitle=false&size=72460&status=done&style=none&taskId=uffedf7d1-fa1a-4ecd-9fde-ff5b5abcdae&title=&width=745)<br />批量重命名：
```python
import maya.cmds as mc
for shape in mc.ls(typ='mesh'):
    mc.rename(shape,'mesh_{0}'.format(shape))

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648351793548-74dc4039-5b32-45c7-98e3-5023af821ead.png#averageHue=%233f3e3d&clientId=ue82b3c53-47c5-4&from=paste&height=320&id=u78e52cbf&originHeight=320&originWidth=214&originalType=binary&ratio=1&rotation=0&showTitle=false&size=13931&status=done&style=none&taskId=u092ba3b2-1198-4d0a-8e1e-e6375914fdb&title=&width=214)
<a name="QgUf7"></a>
# 第三节获取与改变场景中的层级关系
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648356410300-86b3c513-619f-496e-8c04-acece4ec8855.png#averageHue=%233c3c3c&clientId=ue82b3c53-47c5-4&from=paste&height=694&id=u3ecf0d6c&originHeight=694&originWidth=798&originalType=binary&ratio=1&rotation=0&showTitle=false&size=117446&status=done&style=none&taskId=u118e4e36-0d75-4461-bfcd-4ca584c37a7&title=&width=798)<br />通过mc.listRelatives()命令可以处理层级关系<br />mc.listRelatives('Mery_grp',p=True) # 得到Mery_grp的父物体名字（只有一个）<br />mc.listRelatives('Mery_grp',c=True) # 得到Mery_grp的子物体名字（只得到“儿子”，没有“孙子”）<br />mc.listRelatives('Mery_grp',ad=True) # ad是allDescendents的简称，得到Mery_grp的所有子物体名字<br />mc.listRelatives('Mery_grp',ad=True,typ='joint') # 得到Mery_grp的所有子物体名字（只要joint类型的）<br />mc.listRelatives('Mery_grp',ad=True,typ='joint',f=True)# f是fullPath的简称，防止子物体有重名的情况，列举长名<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648357759713-7d694590-c2c2-4fc5-920b-89c4082f91a1.png#averageHue=%239fb2d0&clientId=ue82b3c53-47c5-4&from=paste&height=943&id=u275f16bc&originHeight=943&originWidth=1211&originalType=binary&ratio=1&rotation=0&showTitle=false&size=823384&status=done&style=none&taskId=u2e957dbd-7965-44f4-b29b-08101bc678c&title=&width=1211)
<a name="jLgLU"></a>
## 修改物体的层级关系
**parent命令：**<br />mc.parent('pSphere1','Mery_grp') # 讲pSphere1放到Mery_grp的下面
```python
import maya.cmds as mc
for obj in mc.ls(sl=True) :
    mc.parent(obj,'Mery_grp')
```
mc.parent('pSphere1',w=True) # w为world的缩写，这个命令的作用是将pSphere1放到世界层级的下边，这样pSphere1就没有任何父物体了。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648358668411-10975296-0945-48cc-923a-887143b1a08b.png#averageHue=%2397abc9&clientId=ue82b3c53-47c5-4&from=paste&height=929&id=ua58ef5f8&originHeight=929&originWidth=1726&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1362801&status=done&style=none&taskId=u4c5068ad-f4c4-448b-af42-8a890a9195a&title=&width=1726)<br />**group命令：**<br />mc.group(mc.ls(sl=True),name='ball_group') # 将选择的物体进行打组并起组的名字叫ball_group，第一个参数接收的是一个**列表**，因为mc.ls(sl=True)返回的就是一个列表，因此不需要再增加中括号了。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648358915022-c4f65ec7-b548-480a-bbaf-79850e5a820e.png#averageHue=%239aafd0&clientId=ue82b3c53-47c5-4&from=paste&height=676&id=u2764c4b1&originHeight=676&originWidth=1757&originalType=binary&ratio=1&rotation=0&showTitle=false&size=951958&status=done&style=none&taskId=ub347cb79-93ae-49ee-941d-e016c73d854&title=&width=1757)
<a name="OcFZc"></a>
# 第四节
<a name="KyKpU"></a>
## 获取与更改物体的属性
<a name="PCHmN"></a>
### move，rotate，scale命令，移动，旋转，缩放
| 命令 | 解释 |
| --- | --- |
| mc.move(0,1,0,'pCube1',r=True) | 将pCube1在y轴方向移动1个单位，r是relative的缩写，意思是自身坐标 |
| mc.move(0,1,0,'pCube1',a=True) | 将pCube1移动到世界坐标（0，1，0）的位置，a是absolute的缩写，意思是世界坐标 |
| mc.rotate(0,10,0,'pCube1',r=True) | 将pCube1在y轴方向旋转10度，r是relative的缩写，意思是自身坐标 |
| mc.rotate(0,1,0,'pCube1',a=True) | 将pCube1y轴的旋转属性值设置为10度，a是absolute的缩写，意思是世界坐标 |
| mc.scale(1,5,1,'pCube1',r=True) | 将pCube1在y轴方向放大5倍 |
| mc.scale(1,5,1,'pCube1',a=True) | 将pCube1的缩放属性设置为1，5，1 |

<a name="wwcRK"></a>
### xform命令（不能使用缩放），可以做绑定上的无缝切换
| 命令 | 解释 |
| --- | --- |
| _t = mc.xform('locator1',q=True,t=True) | 查询locator1的移动属性(transform)并将结果传入给变量_t （列表）,q是查询的意思 |
| mc.xform('locator2',t=_t ) | 将刚才定义的_t变量 的数值传递给locator2的移动属性,默认是以自身坐标空间改变 |
| _ro = mc.xform('locator1',q=True,ro=True) | 查询locator1的旋转属性(rotation)并将结果传入给变量_ro（列表） |
| mc.xform('locator2',ro=_ro ) | 将刚才定义的_t变量 的数值传递给locator2的旋转属性,默认是以自身坐标空间改变 |
| tt = mc.xform('locator1',q=True,t=True,ws=True) | ws为True意思是以世界坐标空间获取 |
| mc.xform('pSphere1',t=tt,ws=True) | 将locator1的世界坐标信息给pSphere1。 |


![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648371326540-67345798-b3f3-4d3e-baa7-051e0c87f255.png#averageHue=%23a6b7d4&clientId=ue82b3c53-47c5-4&from=paste&height=1016&id=u75eb237a&originHeight=1016&originWidth=1187&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1063536&status=done&style=none&taskId=ud9e586ee-3f09-42a0-a9d6-76f0d12f921&title=&width=1187)
<a name="D23lG"></a>
# 第五节常见节点、物体的创建
<a name="EOEC8"></a>
## 创建某一确定物体的命令
创建球体：
```python
import maya.cmds as mc
mc.polySphere(r=2,sx=5,sy=5) # 球体的半径为2，x，y的细分(subdivisions)都设置为5，
```
创建圆环曲线：
```python
import maya.cmds as mc
mc.circle(r=10,s=20,nr=(0,1,0)) # 圆环的半径为10，段数(sections)设置为20，法线为（0，1，0）
```
创建曲线：
```python
import maya.cmds as mc
mc.curve(d=1,p=[[0,0,0],[0,1,0],[0,1,1]]) # d（degree）的意思是曲率，p的意思是点
```
创建骨骼：
```python
import maya.cmds as mc
for i in range(10) :
    mc.joint(p=(0,i,0)) # 使用此命令创建骨骼时，新创建的骨骼默认设置为当前选择的对象的子物体
```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648378287550-9eef1c30-728b-4f9f-ae40-e560b6f199a3.png#averageHue=%23464646&clientId=ue82b3c53-47c5-4&from=paste&height=326&id=u50ff2ae1&originHeight=326&originWidth=431&originalType=binary&ratio=1&rotation=0&showTitle=false&size=19389&status=done&style=none&taskId=u6a82b080-ea3a-401b-a889-116731e654f&title=&width=431)
<a name="QqnpH"></a>
## 万能创建法 createNode
这个方法是创建节点使用的。可以创建的节点如下：<br />[https://help.autodesk.com/view/MAYAUL/2019/ENU/index.html?contextId=NODES-INDEX](https://help.autodesk.com/view/MAYAUL/2019/ENU/index.html?contextId=NODES-INDEX)
```python
import maya.cmds as mc
for i in range(10) :
    mc.createNode('joint') # 创建的骨骼都是在同一层级下，createNode只是单纯创造节点使用的
```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648379098018-a2a53c2a-96b0-401c-a3da-e27b052f6868.png#averageHue=%239db5db&clientId=ue82b3c53-47c5-4&from=paste&height=523&id=u649f1d70&originHeight=523&originWidth=1774&originalType=binary&ratio=1&rotation=0&showTitle=false&size=462176&status=done&style=none&taskId=u3889cc15-925b-4256-91a0-f4b8b3ea30b&title=&width=1774)
<a name="NOvug"></a>
# 第六节获取节点的类型和属性
<a name="RBCtN"></a>
### 获取选择物体的类型nodeType
import maya.cmds as mc <br />sel = mc.ls(sl=True)[0]<br />print mc.nodeType(sel)
<a name="r9jbq"></a>
### 获取物体所有属性listAttr
import maya.cmds as mc <br />print mc.listAttr('pCube1')

<a name="dSOPf"></a>
### 获取物体可k帧属性
import maya.cmds as mc <br />print mc.listAttr('pCube1',k=1)
<a name="bJWtt"></a>
### 获取物体自定义属性（ud）
import maya.cmds as mc<br />box = 'pCube1'<br />for attr in mc.listAttr(box, ud=True):<br />    print '{0}.{1}'.format(box, attr)
<a name="BX4Oi"></a>
### 查询属性getAttr（参数是名称加上点加上属性名）
import maya.cmds as mc <br />print mc.getAttr('pCube1.sy')
<a name="VYI9L"></a>
### 修改属性setAttr
import maya.cmds as mc <br />print mc.setAttr('pCube1.sy',1)<br />如果属性是字符串类型的（用户自定义的属性）![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648467132524-549002d8-f1ff-40c1-ad9f-6cffffd8990b.png#averageHue=%234e4e4e&clientId=ue4c50ca3-2f68-4&from=paste&height=564&id=u39635c7d&originHeight=564&originWidth=516&originalType=binary&ratio=1&rotation=0&showTitle=false&size=23790&status=done&style=none&taskId=u4f0ca81a-093d-4b41-9d60-cb9ee7fecdc&title=&width=516)<br />那么需要属性值是带引号的同时也需要在后面加一个typ='string'<br />举例<br />mc.setAttr('pCube1.str','1',typ='string')<br />mc.setAttr('pCube1.str','1',typ='string',l=True) # 赋值后并将属性锁定
<a name="pVg21"></a>
# 第七节连接属性、断开属性、属性联动
<a name="txwY9"></a>
## 常见的连接属性的方法
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648543031243-9bd5873c-9f8b-48d8-8fc0-05057912678f.png#averageHue=%23474646&clientId=u783b1c22-f3a3-4&from=paste&height=659&id=u307f7f96&originHeight=659&originWidth=536&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36194&status=done&style=none&taskId=ua1588174-0769-4654-9e5c-15c799dbdc8&title=&width=536)<br />左边的属性影响右边的属性。
<a name="OKwGF"></a>
## 连接属性 connectAttr命令
mc.connectAttr('pCube1.t','pSphere1.t') # 将pCube1的translate属性与pSphere1的translate属性连接起来<br />mc.connectAttr('pCube2.t','pSphere1.t') # 会提示错误，因为pSphere1已经处于连接状态<br />mc.connectAttr('pCube2.t','pSphere1.t'.f=True) # f是force的简写，代表强制连接pCube2与pSphere1。
<a name="ieC9p"></a>
## 断开属性 disconnectAttr命令
mc.disconnectAttr('pCube2.t','pSphere1.t')
<a name="FLqE8"></a>
# 第八节获取节点的连接关系
<a name="TkcQV"></a>
## 命令：listConnections 获取节点的连接信息
**可用参数：**<br />source 简称s 上游，来源<br />destination简称d 下游，目标 	<br />plugs 简称p 接口，返回连接的节点的属性的名字，参数为布尔类型（如果想要获取属性名字也可以通过connectionInfo命令获取）<br />type 简称t 根据类型返回节点信息<br />**举例：**mc.listConnections('blendColors1',s=True,d=False,p=True,t='lambert')
<a name="kHmPr"></a>
## 命令：connectionInfo 获取节点属性的连接信息
**可用参数：**<br />sourceFromDestination简称sfd，为True时返回上游属性（返回的是一个unicode）<br />destinationFromSource简称dfs，为True时返回下游属性（返回的是一个列表）<br />isSource不能用简称，因为is是关键词，为True时判断目标属性是否为上游属性（是否是用来输出的源）<br />isDestination不能用简称，因为id是关键词，为True时判断目标属性是否为下游属性<br />**举例：**<br />mc.connectionInfo('blendColors1.output',dfs=True)
<a name="w8SSs"></a>
# 第九节 约束
常见的约束：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648559948601-8b2bdb3d-a8ce-4045-b140-3c1b0c76d6b3.png#averageHue=%23535252&clientId=u17e0615e-ed5e-4&from=paste&height=312&id=u0ed1d8ee&originHeight=312&originWidth=247&originalType=binary&ratio=1&rotation=0&showTitle=false&size=11586&status=done&style=none&taskId=u2ae086d2-b2b3-4ea5-8217-05b7c06e503&title=&width=247)从上到下依此为，父子约束、点约束、旋转约束、缩放约束、目标约束、极向量约束。<br />这里介绍一下点约束、旋转约束、父子约束。
<a name="J5u4Y"></a>
## 点约束：pointConstraint
能使用命令调用的属性都包含在这里面![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648560223121-cd9181bb-4688-4ec9-bc62-a40afbbbe679.png#averageHue=%23525251&clientId=u17e0615e-ed5e-4&from=paste&height=389&id=u4f5359bc&originHeight=389&originWidth=562&originalType=binary&ratio=1&rotation=0&showTitle=false&size=14552&status=done&style=none&taskId=u2eb3d0ae-3318-4e1d-a103-eee6b445367&title=&width=562)<br />平时的约束操作：选择约束的物体然后再选择被约束的物体然后执行约束。<br />使用命令进行约束：mc.pointConstraint('pCube1','pSphere1')第一个为约束的物体，第二个为被约束的物体<br />保持偏移的情况下进行约束：mc.pointConstraint('pCube1','pSphere1',mo=True)  mo为maintaniOffset的缩写 <br />约束的同时赋予约束节点名字: mc.pointConstraint('pCube1','pSphere1',mo=True,n='ball_cons')<br />**约束信息的查询 **<br />查询一个被约束物体的约束节点名字：mc.pointConstraint('pSphere1',q=True,n=True)<br />查询一个被约束物体的约束物体名字（列表）：mc.pointConstraint('pSphere1',q=True,tl=True)  tl为targetList的简称<br />查询一个被约束物体的约束节点权重别名列表：mc.pointConstraint('pSphere1',q=True,wal=True) wal为weightAliasList的简称
<a name="ErPRh"></a>
## 旋转约束orientConstraint
跟点约束是一样的，就是把point改成orient 其他就都一样了
<a name="Vj3S0"></a>
## 父子约束parentConstraint
实例：利用控制器对骨骼进行约束<br />在实际运用中控制器（可以用曲线当控制器）的轴向要和骨骼的轴向一致。<br />因此可以先为控制器创建一个组，然后通过父子约束使骨骼约束控制器的组，这样控制器作为组的子物体就与骨骼轴向一致了，再将这个约束删除掉，再执行父子约束使控制器约束骨骼。就可以实现使控制器与骨骼轴向并且绑定到了一起。<br />代码实现：
```python
import maya.cmds as mc
jt1='joint1'
ctg='ctl_grp'
ctl='ctl'
mc.delete(mc.parentConstraint(jt1,ctg))
mc.parentConstraint(ctl,jt1)
```
<a name="jel5d"></a>
# 第十节 关键帧
<a name="OWGuS"></a>
## 设置关键帧setKeyframe



| 命令 | 执行效果 |
| --- | --- |
| mc.setKeyframe() | 为选择物体所有属性k帧 |
| mc.setKeyframe('pSphere1') | 为pSphere1所有属性k帧 |
| mc.setKeyframe('pSphere1',at='tx') | 为pSphere1的tx属性k帧 |
| mc.setKeyframe('pSphere1',at=['tx','ty']) | 为pSphere1的tx，ty属性k帧 |
| mc.setKeyframe('pSphere1',at=['tx','ty','r']) | 为pSphere1的tx，ty,rx,ry,rz属性k帧 |
| mc.setKeyframe('pSphere1',at=['tx','ty','r'],v=10) | 为pSphere1的tx，ty,rx,ry,rz属性k帧,并指定属性的值为10 |
| mc.setKeyframe('pSphere1',at=['tx','ty','r'],v=10,t=10) | 为pSphere1的tx，ty,rx,ry,rz属性在第10帧k帧,并指定属性的值为10 |

 可以通过此命令进行的实际案例举例：

1. 不通过Maya的导出动画工具，我们可以自定义导出类型，然后读进来，用这个命令给控制器赋值上动画，就可以做一个导出导入动画的工具了。
2. 让一个物体按照数学曲线来实现他的运动，例如让一个球沿着原点旋转，可以让这个球的X轴为正弦，Z轴为余弦的方式配合着来实现让球转圈的运动。
```python
import maya.cmds as mc
import math
for i in range(0,360) :
    x=math.sin(i*math.pi/180)*10 # 在程序中的数学计算默认是以弧度为单位进行运算的，因此将角度转换为弧度
    z=math.cos(i*math.pi/180)*10
    mc.setKeyframe('pSphere1',at='tx',t=i,v=x)
    mc.setKeyframe('pSphere1',at='tz',t=i,v=z)
```
<a name="kakFH"></a>
## 获取与编辑关键帧keyframe

| 命令 | 执行效果 |
| --- | --- |
| mc.keyframe('pSphere1',q=True,tc=True) | tc为timeChange的缩写，返回的是一个列表，记录着物体所有存在关键帧的时间 |
| mc.keyframe('pSphere1',q=True,vc=True) | vc为valueChange的缩写，返回的是一个列表，记录着物体所有存在关键帧的数值 |
| mc.keyframe('pSphere1',q=True,t=(101,101),at="tx",eval=True) | 得到pSphere1在101帧时tx属性的值 |


<a name="k1f0F"></a>
## 将物体的某一范围关键帧整体移动（编辑关键帧）
```python
import maya.cmds as mc
frame_tc=mc.keyframe('pSphere1',q=True,tc=True)
mc.keyframe('pSphere1',e=True,time=(min(frame_tc),max(frame_tc)),tc=5,r=True)
# 解释一下这些参数的意思，e代表开启编辑模式，time代表帧数的范围，tc代表移动的值(正为右，负为左)，r代表相对模式
```
执行前：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648723170267-6c854a51-c782-49a4-b0a1-32d16c7ba23a.png#averageHue=%23393838&clientId=u86956685-7471-4&from=paste&height=66&id=u7c89c0fb&originHeight=66&originWidth=536&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1816&status=done&style=none&taskId=u8295ef55-1fe0-41f0-9660-87cb00f4be5&title=&width=536)<br />执行后：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648723174130-111ce6c6-779d-47e9-828f-7baa674be086.png#averageHue=%233a3939&clientId=u86956685-7471-4&from=paste&height=74&id=ud07db9b7&originHeight=74&originWidth=520&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2146&status=done&style=none&taskId=uc6fefe1f-0eff-4bb9-b225-8e0664350eb&title=&width=520)

<a name="D3z5N"></a>
# 第十一节文件IO操作

| 命令 | 执行结果 |
| --- | --- |
| **file命令 ** | **处理文件与文件路径相关的** |
| mc.file(new=True) | 新建一个场景，如果没保存会无法执行 |
| mc.file(new=True,force=True) | 强制新建一个场景，没有保存的数据会清空且操作无法撤回。 |
| mc.file(rename='D:/ball.ma')<br />mc.file(save=True,typ='mayaAscii') | 这两行代码代表的意思为，第一行执行ctrl+s中的选择位置并命名指定格式的操作，第二行执行保存的操作（默认类型为mb格式，如果保存的类型为ma格式需要更改typ的参数为mayaAscii） |
| mc.file(save=True,typ='mayaAscii') | 对于已经创建好的场景可以直接执行保存的命令 |
| mc.file('D:/ball.ma',o=True,f=True) | 强制打开对应的路径场景(需要带后缀名) |
| mc.file(q=True,sn=True) | 查询场景的路径文件名（带路径名），sn是sceneName的缩写。 |
| mc.file(q=True,sn=True,shn=True) | 查询场景的文件名（不带路径名），shn是shortName的缩写 |
| mc.file('D:/ball_export.ma',ea=True,typ='mayaAscii') | 导出所有物体并指定路径文件名，ea是exportAll的缩写 |
| mc.file('D:/ball_export.ma',es=True,typ='mayaAscii') | 导出选中的物体并指定路径文件，es为exportSelected的缩写 |
| mc.file('D:/ball_export.ma',i=True,ns='ball') | 进行导入文件操作并提供命名空间为ball，加命名空间的名字是为了区分物体，i是import的缩写使用简称，因为import是python的关键字，ns是namespace 的缩写![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648779775166-df7053af-a760-4225-94b0-9548ece5265b.png#averageHue=%23525250&clientId=u693e63da-04bd-4&from=paste&height=34&id=ubfeb4c31&originHeight=34&originWidth=424&originalType=binary&ratio=1&rotation=0&showTitle=false&size=19004&status=done&style=none&taskId=u837a9d31-fa7c-4e26-8177-e261bb0a807&title=&width=424) |
| mc.file('D:/ball_export.ma',r=True,ns='ball') | 进行引用文件操作并提供命名空间为ball，r是reference的缩写。 |
| mc.file(q=True,r=True) | 查看当前场景引用的文件路径，返回的是一个列表 |
| mc.file('D:/ball_export.ma',r=True,ns='ball') | 查看当前场景中引用的D:/ball_export.ma文件中的引用文件路径，针对嵌套引用进行的操作 |
| **referenceQuery命令  ** | **查询引用文件的信息** |
| mc.referenceQuery('D:/ball_export.ma',n=True) | 查询引用文件的所有节点信息（列表） |
| mc.referenceQuery('ball:pSphere50',f=True) | 查询当前场景中的文件的文件路径，f为filename的缩写。 |
| mc.referenceQuery('D:/ball_export.ma{3}',isLoaded=True) | 查询当前场景中引用的第四个文件有没有加载进场景中。 |

<a name="hDKYL"></a>
# 第十二节maya界面编程
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648782901563-53023a75-6b89-44dc-acf6-9b09669ff4dc.png#averageHue=%23313332&clientId=u693e63da-04bd-4&from=paste&height=956&id=uabc08218&originHeight=956&originWidth=1229&originalType=binary&ratio=1&rotation=0&showTitle=false&size=115918&status=done&style=none&taskId=ubd402539-223c-4aaf-93bf-5c78d2339cd&title=&width=1229)

| 命令 | 执行结果 |
| --- | --- |
| wnd=mc.window()<br />mc.showWindow(wnd) | 创建一个简单的窗口<br />显示窗口 |
| wnd=mc.window(w=600,h=800，t='My Window') | 创建一个宽600高800标题为My Window的窗口 |

```python
import maya.cmds as mc
wnd_name='my_window' # 为窗口设置一个名字
if mc.window(wnd_name,q=True,ex=True):
    # 如果界面中出现已经打开的窗口，就先删掉窗口，再执行下面的语句（创建窗口）
    mc.deleteUI(wnd_name,wnd=True)
if mc.windowPref(wnd_name,q=True,ex=True):
    # Pref是preference(偏好)的简称，如果创建窗口后更改了窗口的大小，就会移除这个偏好设置，r为remove的简称。
    # 这个操作可以理解为初始化
    mc.windowPref(wnd_name,r=True)
# 生成一个窗口名称为wnd_name标题为My Window的窗口，用wnd来存取
wnd = mc.window(wnd_name,w=400,h=300,t='My Window')
mc.showWindow(wnd)
```

```python
import maya.cmds as mc
wnd_name='my_window'
if mc.window(wnd_name,q=True,ex=True):
    mc.deleteUI(wnd_name,wnd=True)
if mc.windowPref(wnd_name,q=True,ex=True):
    mc.windowPref(wnd_name,r=True)
wnd = mc.window(wnd_name,w=400,h=300,t='My Window')
mc.columnLayout() # 垂直布局
for i in range(10):
    mc.button(l='Button_{0}'.format(i),c='print {0}'.format(i)) # 按钮以及对应事件
mc.showWindow(wnd)
```
可以在帮助文档中的这一栏找到生成界面的操作命令![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648792828376-99f3cddb-467d-4bce-83c0-197aee119740.png#averageHue=%23e6e6e6&clientId=u693e63da-04bd-4&from=paste&height=148&id=u67bb6d10&originHeight=148&originWidth=192&originalType=binary&ratio=1&rotation=0&showTitle=false&size=3700&status=done&style=none&taskId=udb846596-45c4-4933-bca4-bfbdeb6b0b7&title=&width=192)
<a name="HaCXE"></a>
# 第十三节maya界面视图操作
| 命令 | 执行结果 |
| --- | --- |
| **mc.getPanel命令** | **获取面板** |
| mc.getPanel(all=True) | 获取maya中的所有面板名字列表，all为（allPanels的缩写） |
| mc.getPanel(vis=True) | 获取显示的面板名字列表（一般会包括脚本编辑面板和大纲面板），vis为（visiblePanels的缩写）![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648817058285-e3519439-fc5b-4e4e-ad72-1d4f6622f924.png#averageHue=%233b3a3a&clientId=u46a1ca6b-8b3c-4&from=paste&height=793&id=uf18f57ac&originHeight=793&originWidth=1894&originalType=binary&ratio=1&rotation=0&showTitle=false&size=123883&status=done&style=none&taskId=ub3d15eaa-8a32-4277-9838-375f0baf319&title=&width=1894) |
| mc.getPanel(typ='modelPanel') | 获取类型为modelPanel的面板，[u'modelPanel1', u'modelPanel2', u'modelPanel3', u'modelPanel4']<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648818332899-7f478f10-7af7-454e-bf62-461ac25a34f6.png#averageHue=%23535353&clientId=u46a1ca6b-8b3c-4&from=paste&height=511&id=u24518dfb&originHeight=511&originWidth=392&originalType=binary&ratio=1&rotation=0&showTitle=false&size=19137&status=done&style=none&taskId=u36b7d83b-6d6b-4d0c-b8b5-bc775d30801&title=&width=392)**无论对应不同面板对应视图是什****么，面板名都不会改变** |
| mc.getPanel(withFocus=True) | 获取当前激活的面板名字。（实时获取需要将代码变成工具后才能实时获取） |
| **mc.modePanel命令** | **编辑面板** |
| mc.modelPanel('modelPanel4',q=True,cam=True) | 查询modelPanel4面板的相机名字 |
| mc.modelPanel('modelPanel4',q=True,p=True) | 查询modelPanel4面板的父物体的名字 |
| mc.modelPanel('modelPanel4',e=True,cam='camera1') | 编辑modelPanel4面板，使其相机设置为camera1 |
| mc.modelPanel('modelPanel4',e=True,tearOff=True) | 将modelPanel4面板裁剪下来，![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648819167054-d406a702-6586-4f4f-ab30-5c4551609b53.png#averageHue=%23545453&clientId=u46a1ca6b-8b3c-4&from=paste&height=593&id=u4899d308&originHeight=593&originWidth=878&originalType=binary&ratio=1&rotation=0&showTitle=false&size=73520&status=done&style=none&taskId=ufaa052bf-201f-42a3-b5fe-9e6b515d95b&title=&width=878)<br />要想恢复默认面板点击这个![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648819187600-4bbfbc39-68f7-4c7b-b63c-a8912694e79e.png#averageHue=%23484646&clientId=u46a1ca6b-8b3c-4&from=paste&height=200&id=u7c2aa74f&originHeight=200&originWidth=106&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1825&status=done&style=none&taskId=ue175964b-a7a2-4f25-b659-8dc8178443c&title=&width=106) |
| **mc.modelEditor命令** | **针对视图面板进行编辑操作** |
| mc.modelEditor('modelPanel4',q=True,cam=True) | 获取modelPanel4面板中的摄像机名字 |
| mc.modelEditor('modelPanel4',e=True,j=False) | 编辑modelPanle4面板，取消骨骼的显示 |
| mc.modelEditor('modelPanel4',e=True,pm=False) | 编辑modelPanle4面板，取消多边形的显示 |
| mc.modelEditor('modelPanel4',e=True,xray=True) | 编辑modelPanle4面板，是物体以x光的样式显示![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648819832918-9880594a-dd75-4265-8d59-7606bd95b66f.png#averageHue=%23606060&clientId=u46a1ca6b-8b3c-4&from=paste&height=74&id=u0e3d76a3&originHeight=74&originWidth=101&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1940&status=done&style=none&taskId=u78fb911b-2b04-466a-ace9-1d7320d43b4&title=&width=101) |
| mc.modelEditor('modelPanel4',e=True,grid=False) | 编辑modelPanle4面板，取消网格的显示 |

<a name="YqPsv"></a>
# 第十四节 Maya ScriptJob 事件操作
<a name="KFZaj"></a>
## 时间变化事件
mc.scriptJob(tc='print "xxx"') 意思是当时间轴变化的时候会输出“xxx”<br />**每通过scriptJob创造一次事件后，会生成对应的ID来代表事件，如果重复使用scriptJob事件变化时，会产生多次事件操作，因此每创造一次事件操作后需要通过mc.scriptJob(kill=对应事件的ID)来删除掉。**
<a name="estH7"></a>
## 属性变化事件
mc.scriptJob(attributeChange=('pSphere1.tx','print "123"'))意思是当pSphere1的x坐标发生改变时就输出123<br />mc.scriptJob(killAll=True) 意思是删除所有变化事件
<a name="Rk562"></a>
## 节点变化事件
mc.scriptJob(nodeDeleted=('pSphere1','print "ball delete"')) 当pSphere1节点被删除时输出ball delete<br />mc.scriptJob(nodeNameChanged=('pSphere1','print "ball renamed"'))  当pSphere1节点名字改变时，输出ball renamed，**无论名字怎么变都能追踪到节点，但是无法追踪的更改后的名字。**如果需要追踪的更改后的名字需要用到api的知识。<br />mc.scriptJob(nodeNameChanged=('pSphere1','print "ball renamed"',permanent=True)) permanent是永久的意思，为True时代表这个事件不会被kill掉，只有关闭maya时才会kill掉。
<a name="Ziejv"></a>
## 根据条件是否成立进行的事件
mc.scriptJob(conditionTrue=('autoKeyframeState','print "auto key enable"') )如果开启自动关键帧，则输出auto key enable<br />mc.scriptJob(conditionFalse=('autoKeyframeState','print "auto key disable"') )如果关闭自动关键帧，则输出

mc.scriptJob(conditionFalse=('SomethingSelected',func) )如果选择了一个物体，则调用func函数（func函数是自己定义的）<br />mc.scriptJob(listConditions=True) 列举所有可以判断的条件
<a name="Ep3Td"></a>
# 第十六节Maya中的Pymel编程
[https://vannyyuan.github.io/2020/10/30/maya/Maya%E5%BC%80%E5%8F%91%E5%AE%9E%E8%B7%B5%E8%AF%BE/Maya%E5%BC%80%E5%8F%91%E5%AE%9E%E8%B7%B5%E8%AF%BE%EF%BC%88%E4%BA%8C%EF%BC%89/](https://vannyyuan.github.io/2020/10/30/maya/Maya%E5%BC%80%E5%8F%91%E5%AE%9E%E8%B7%B5%E8%AF%BE/Maya%E5%BC%80%E5%8F%91%E5%AE%9E%E8%B7%B5%E8%AF%BE%EF%BC%88%E4%BA%8C%EF%BC%89/)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648969455562-a9471201-5f76-416b-88c7-71000227d7cd.png#averageHue=%23383837&clientId=ua9dc1804-c6e6-4&from=paste&height=693&id=u8ced480e&originHeight=693&originWidth=928&originalType=binary&ratio=1&rotation=0&showTitle=false&size=237735&status=done&style=none&taskId=ucb71eae1-72d4-4664-9de4-8b2cbb906dd&title=&width=928)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648969694679-2da33bb3-91e4-45db-a0a4-5446c0e8f52f.png#averageHue=%23363635&clientId=ua9dc1804-c6e6-4&from=paste&height=688&id=u48255799&originHeight=688&originWidth=1541&originalType=binary&ratio=1&rotation=0&showTitle=false&size=434095&status=done&style=none&taskId=uc96d9b04-1d09-4d42-9478-32cb4156a01&title=&width=1541)
<a name="cC9ah"></a>
# 第十八节自定义maya环境
<a name="iWEbO"></a>
## 为什么要修改maya的环境变量
我们可以通过环境变量来配置我们不同项目中所需要的maya环境，可以通过环境变量来存储、获取信息，也可以直接修改maya的配置，可以通过设置统一的环境变量，使每个人的环境设置都是统一的。如果我们使用动态设置环境变量的话，我们可以更方便地去切换配置来制定我们的运行环境。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648974285639-8307f5dc-3fad-4dd6-93a9-37ca6d46ce5d.png#averageHue=%23f1f0ef&clientId=ua9dc1804-c6e6-4&from=paste&height=666&id=ufb0805fb&originHeight=666&originWidth=632&originalType=binary&ratio=1&rotation=0&showTitle=false&size=37783&status=done&style=none&taskId=udb9a3237-1620-4b31-ab67-2dc3fa7f4e0&title=&width=632)<br />上面一栏是针对用户的变量，系统变量不区分用户，只要用的是同一台电脑都会读取系统变量。<br />用户变量会覆盖系统变量，
<a name="VuEty"></a>
## 在进程中设置环境变量
在进程中设置的环境变量只针对当前运行的程序，在进程中设置是指，![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648974530936-92f75e29-8dec-404e-ab23-6b3e8f8a5760.png#averageHue=%23383838&clientId=ua9dc1804-c6e6-4&from=paste&height=188&id=ua27d14e8&originHeight=188&originWidth=540&originalType=binary&ratio=1&rotation=0&showTitle=false&size=52373&status=done&style=none&taskId=ua5af8108-75c6-470d-8b88-9ceab9ed478&title=&width=540)<br />关闭程序框之后设置的环境变量就消失了。
<a name="ojerf"></a>
## 通过设置环境变量关闭maya的用户登录节省启动时间
在搜索框中搜索env可以快速进入编辑环境变量的界面。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648974632970-d824b63d-0ea5-4ece-b9dd-173db2f96959.png#averageHue=%231a6097&clientId=ua9dc1804-c6e6-4&from=paste&height=77&id=u2483008d&originHeight=77&originWidth=264&originalType=binary&ratio=1&rotation=0&showTitle=false&size=11427&status=done&style=none&taskId=ufd13bde6-62e7-4c21-ae4e-1bbb837377d&title=&width=264)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648974672749-51fb577e-e216-4985-bb58-a1be24045b0a.png#averageHue=%23eae9e9&clientId=ua9dc1804-c6e6-4&from=paste&height=190&id=u7b27031f&originHeight=190&originWidth=667&originalType=binary&ratio=1&rotation=0&showTitle=false&size=10509&status=done&style=none&taskId=ue3fb4f62-e2da-44cc-9f95-313c0fbacfa&title=&width=667)<br />常用的环境变量设置：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648974783139-5563350b-98d3-4a6f-8ced-262b4af7cb2c.png#averageHue=%23f4f4f4&clientId=ua9dc1804-c6e6-4&from=paste&height=940&id=u32d73e3d&originHeight=940&originWidth=1577&originalType=binary&ratio=1&rotation=0&showTitle=false&size=504330&status=done&style=none&taskId=u0aac74f6-e652-46f0-8db7-5e62b90aed3&title=&width=1577)
<a name="cVpqZ"></a>
# 第十九节maya api基础知识
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653280913082-51374dc0-392d-4e30-8419-99747223fb98.png#averageHue=%2397a36a&clientId=u83265a8a-3f59-4&from=paste&height=634&id=u3890b232&originHeight=634&originWidth=988&originalType=binary&ratio=1&rotation=0&showTitle=false&size=149416&status=done&style=none&taskId=uddea111d-2eab-41b3-99b6-df12b83781c&title=&width=988)
<a name="EKEk1"></a>
## API编译的插件后缀
Linux：.so<br />Windows: .mll<br />Mac OS X: .bundle<br />通用型插件: .py 直接运行
<a name="xMUzJ"></a>
## API的内置库
OpenMaya 基本的操作工具类<br />OpenMayaUI 界面工具类<br />OpenMayaAnim 动画工具类<br />OpenMayaFX 特效工具类<br />OpenMayaRender 渲染工具类
<a name="FzR2w"></a>
## API命名规则
M classes - 基本的数据类型   比如：类似于python的字符串、整数<br />MFn - Function 函数工具类型<br />MIt - lterator 迭代器类型<br />MPx - 代理类型，扩展Maya功能需要继承的类  

MayaAPI通过MFn把不同的物体方法归类，我们可以通过这些方法，针对不同的物体进行各自的操作<br />MIt开头的迭代器类型：这种类型对于我们批量访问物体也就是说对于一批物体我们要逐个访问的时候，我们要使用这种迭代器类型，然后用循环挨个访问它们的元素。<br />MPx类型这个类型不是由我们来访问的，是我们按照这种格式编写好了一个插件，那么加载上之后，Maya就去根据他定义好的固定的格式来去加载这些插件，MPx类型就是我们由人工来编写，Maya自己来识别的这个命令

<a name="XChwZ"></a>
## DependencyNode和DagNode
在maya中，所有的节点都是一个DependencyNode也就是说依赖节点，我们所有的数据都是依赖于节点来计算的，每个节点存储了我们所需要的数据，那么节点之间的相互计算，形成节点网络，也就形成了我们最终的文件。<br />DependencyNode是最基本的节点，类似于我们的材质节点，这种独立的单个节点。<br />Maya DagNode是带有层级关系的，在大纲里，我们可以设置它的父子关系，这种叫DagNode，DagNode是从DependencyNode扩展而来的，DagNode拥有DependencyNode的所有方法，我们可以用DependencyNode的方法来处理任何一个DagNode，但是类似于层级操作这种，比如说获取它的物体的上下级关系这种不属于DependencyNode里面的方法，我们就要用DagNode它自有的方法，也就是我们面向对象里面的，子类的那种方法。
<a name="dTJpY"></a>
## MObject ：Maya最基本的对象指针
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653288864645-b0a7fcbd-b4fa-4f97-a0c6-ec56f647b08a.png#averageHue=%23323232&clientId=u83265a8a-3f59-4&from=paste&height=488&id=u4e48a232&originHeight=488&originWidth=1447&originalType=binary&ratio=1&rotation=0&showTitle=false&size=279544&status=done&style=none&taskId=u087d5467-e700-433a-b5a2-a9a58803911&title=&width=1447)<br />MObject是maya最基本的一个对象，也就是说如果使用API的话这个就是我们处理的最基本的一个数据，就像python编程一样，我们一个变量，虽然是字符串或者整数，那么它都是一个python的基本对象，这个MObject是MayaAPI的基本对象。在MayaAPI中，它不能以字符串这种来处理节点，它必须要转化成一个MObject才能处理，也就是说Maya中任何一个对象都是一个MObject，当然处理类似于它的名字、它的属性值这种字符串或者数值例外。也就是说这是一个最基本的索引，它指向 了每一个节点，我们在处理某一个节点就认为它是一个MObject

我们要处理任何一个Maya节点都要把它实例成一个MObject才能使用它的方法。
```python
import maya.OpenMaya as OpenMaya
import pymel.core as pm

ball_node = pm.PyNode('pSphere1') # 将”pSphere1“改为pymel节点
ball_api_node = ball_node.__apimobject__() # 利用pymel节点的方法创建一个MObject对象指向pSphere1

# 通过pymel转化的MObject已经有了对象
print ball_api_node.isNull() # False
# 通过OpenMaya直接创建的MObject是空的
print OpenMaya.MObject().isNull() # True

# 查询api类型
print ball_api_node.apiType() # 110
print ball_api_node.apiTypeStr() # kTransform
ballshape_api_node = pm.PyNode('pSphereShape1').__apimobject__()
print ballshape_api_node.apiType() # 296
print ballshape_api_node.apiTypeStr() # kMesh

# 使用 == != 判断两个物体是否相等
print ball_api_node == ballshape_api_node # False
# 使用 = 直接赋值
ballshape_api_node = ball_api_node
print ballshape_api_node.apiTypeStr()
```
<a name="amNP3"></a>
## 如何查询API的帮助文档
[https://help.autodesk.com/view/MAYAUL/2019/CHS/?guid=Maya_SDK_MERGED_cpp_ref_index_html](https://help.autodesk.com/view/MAYAUL/2019/CHS/?guid=Maya_SDK_MERGED_cpp_ref_index_html)<br />帮助文档是C++的风格，<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653291601023-9de8eeeb-6c65-4443-bccd-226ba3a42d79.png#averageHue=%23d6dde9&clientId=u83265a8a-3f59-4&from=paste&height=208&id=u0342c47f&originHeight=208&originWidth=312&originalType=binary&ratio=1&rotation=0&showTitle=false&size=13455&status=done&style=none&taskId=u73376463-7488-40a2-b405-14e7642c102&title=&width=312)<br />modules是我们可以导入的模块，查询一般都是查询modules里面的内容<br />例如查询MObject<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653291953243-7e5ce736-0b3a-4abc-b0ba-a586d5927065.png#averageHue=%23f3f6fa&clientId=u83265a8a-3f59-4&from=paste&height=549&id=u4acf9a0a&originHeight=549&originWidth=932&originalType=binary&ratio=1&rotation=0&showTitle=false&size=54163&status=done&style=none&taskId=u90bca0ff-6f2c-4306-bf5c-10b3bfa0abd&title=&width=932)<br />前三行：在最一开始我们可以通过第一行创建一个空的MObject，或者通过第二行从另一个MObject转过来它就指到这一个原来那个MObject那个节点上了。第三行带~的学名叫做析构函数，意思是被销毁时执行的操作。一般不会用到它，除非我们编写节点的时候，需要用到它来清理内存。<br />下面的蓝色的部分是它可以使用的方法，前面的是当前方法的返回值，括号里面是当前方法需要的参数，后面是它的描述。<br />**静态方法：意思是不需要实例化就可以使用的方法**

<a name="WRd71"></a>
## MDagPath
MDagPath是最基本的物体对象，我们可以把大纲里的物体通过它来交给API来处理，可以从MDagPath里面找到物体对应的MObject，也可以通过传入MObject，给物体定义好一个DagPath来处理它的层级关系
```python
# 创建一个空的MDagPath
ball_dag_path = OpenMaya.MDagPath()
# 建立DagPath联系
OpenMaya.MDagPath.getAPathTo(ball_api_node,ball_dag_path)
# 获取DagPath名字
print ball_dag_path.fullPathName() # |pSphere1
print ball_dag_path.partialPathName() # pSphere1
# 判断是否显示
print ball_dag_path.isVisible() # True
# 通过MDagPath获取API类型
print ball_dag_path.apiType() # 110
# 通过MDagPath返回MObject
print ball_dag_path.node() # <maya.OpenMaya.MObject; proxy of <Swig Object of type 'MObject *' at 0x0000014894705F90>
```
<a name="dXjGA"></a>
# 第二十节 MFn、MIt、MPx（函数库、迭代器、代理）

<a name="kMnOj"></a>
## MFn
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653379132076-ae3a87ef-4af8-43b0-80de-6961a3499f80.png#averageHue=%23343434&clientId=u7707d889-cb75-4&from=paste&height=718&id=ubd1e52a1&originHeight=718&originWidth=1304&originalType=binary&ratio=1&rotation=0&showTitle=false&size=250768&status=done&style=none&taskId=u97b20b69-d851-475e-bd37-314e47bd1b1&title=&width=1304)<br />MFnDependencyNode用来处理任何一个节点的普通方法<br />MFnDagNode用来处理大纲内的物体的一些常用方法<br />MFnMesh用来处理多边形的操作<br />MFn记录了Maya内所有的节点的类型也就是说我们用MObject获取的那个apiType返回的数值就是它在MFn列表中的索引值
<a name="S5GWo"></a>
## MIt
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653379457368-a53666cf-f95b-48a5-813c-5d6a4a0cff46.png#averageHue=%23313130&clientId=u7707d889-cb75-4&from=paste&height=841&id=u071fd3f3&originHeight=841&originWidth=1391&originalType=binary&ratio=1&rotation=0&showTitle=false&size=310906&status=done&style=none&taskId=u838416df-de52-4897-8a87-685e9f3da86&title=&width=1391)<br />MIt是为了批量处理而设计的，比如挨个处理每个层级的物体。或者比如说有一个球的任何一个节点都可以通过MItMesh来访问，然后来访问它的任何一个点线面。<br />MItDag：处理大纲里的层级关系<br />MItCurveCV：处理曲线的点<br />MItMeshEdge：处理多边形的线的循环<br />MItMeshFaceVertex: 以面点的方式处理<br />MItMeshPolygon：处理面<br />MItMeshVertex：处理顶点<br />MItSelectionList：处理一个列表中的任何物体（跟MItDag有区别，MItDag是处理大纲里的所有物体，MItSelectionList是处理我们自己创建的列表中的物体）

MItDependencyGraph：通过一个节点寻找它上下游所有的节点<br />MItDependencyNodes：可以使用它来过滤场景里面任何一个节点，Maya中的节点都可以通过它来逐个访问到
<a name="UC68R"></a>
## MPx
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653380549470-f6f7ebc9-6faa-4aaa-af9c-269bed2d53c7.png#averageHue=%23323232&clientId=u7707d889-cb75-4&from=paste&height=784&id=uae30f1b1&originHeight=784&originWidth=1379&originalType=binary&ratio=1&rotation=0&showTitle=false&size=309040&status=done&style=none&taskId=u46b56290-7d6b-4b79-86e8-c625e98e985&title=&width=1379)<br />当要真正编写一个Maya中没有的物体的话，就需要继承MPx里边的内容。<br />我们如果要写一个命令的话，那么，它就要继承MPxCommand，如果我们要写一个节点的话就要继承一个MPxNode。如果要写一个变形器的话，那就要继承DeformerNode。<br />当然还有灯光材质或者其他的那些，我们要选择对应的代理类去继承然后使用。<br />比如，我们要编写一个新的节点的话，我们可以继承MPxNode，里面我们可以选择对应的类型，我们可以不用继承一个最基本的一个类型，比如我们要写一个新的Locator的话，我们可以直接定义他的初始化类型Locator。那么，这些方法我们都是要定义同样的方法，同样的参数，然后写我们不同的处理方法。Maya会自动访问这些方法，来根据我们的计算反映出不同的数值。compute方法是计算方法，是节点最核心的方法，我们所有的算法都要存在这里边然后返回不同的结果。<br />这只是一个单纯的节点，我们如果要编写一个新的节点的话，我们还需要在给这个节点他添加上我们所需要的属性，那么在compute方法里面，我们通过不同的算法，把不同的数值返回给我们的属性，那么它就会输出到其他的节点，从而达到我们真正所需要的想法。	
<a name="KuNx7"></a>
## 总结
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653383481384-24e48f5e-810b-491c-b363-6573e4368e27.png#averageHue=%23333333&clientId=u7707d889-cb75-4&from=paste&height=785&id=ua211a22f&originHeight=785&originWidth=1389&originalType=binary&ratio=1&rotation=0&showTitle=false&size=315867&status=done&style=none&taskId=ub1647ad2-883e-4e9c-a1b2-3a3244dfe3b&title=&width=1389)
<a name="DXONy"></a>
# 第二十一节MSelectionList与MItSelection List
<a name="kQTS4"></a>
## MSelectionList
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653384147890-bcfa673a-f9e9-4629-a5f3-d6b7df49a6f0.png#clientId=u7707d889-cb75-4&from=paste&height=1011&id=u89ecb4e3&originHeight=1011&originWidth=1283&originalType=binary&ratio=1&rotation=0&showTitle=false&size=291687&status=done&style=none&taskId=u92e44cd3-f5cb-4cbb-a605-ee2b6aff3fe&title=&width=1283)<br />MSelectionList只是一个普通的节点列表。用来存储节点或者物体的列表。<br />MSelectionList类的方法：<br />isEmpty：用来判断实例化的对象是否是一个空的MSelectionList，返回布尔类型<br />add： 可以添加的类型有MObject、MDagPath、MString、MPlug、MUuid。其中MString可以是确切的物体的名字，也可以包含通配符的。例如add("pSphere*")就会挨个添加pSphere1、pSphere2等，这里的*就是通配符可以指代所有字符<br />length：返回列表中的元素个数<br />merge（合并） : 把参数中的列表内容添加到使用此方法的对象上。例如： ball_lst.merge(box_lst)就是将box_lst的内容添加到ball_lst列表里面<br />intersect（交集）：同理merge得到两个列表（调用方法的对象和方法中的参数）的交集<br />remove：移除
<a name="Dpv2T"></a>
## MItSelectionList
MItSelectionList是SelectionList 的迭代器，用于逐个访问MSelectionList里的项目<br />生成迭代器需要传入MSelectionList对象<br />常用方法：<br />next： 通过next访问下一个元素<br />reset： 返回到某一位置重新继续next<br />getDagPath：获取里面的DagPath<br />getDependencyNode:获取里面的MObject<br />**举例，迭代SelectionList里的内容**<br />通过lst_iter = OpenMaya.MItSelectionList(sel_lst)来创建sel_lst的迭代器，然后迭代列表中的内容，输出dag_path<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653398043743-3b190bc6-c1ad-46df-8c24-8b9576eaf1ec.png#clientId=u7707d889-cb75-4&from=paste&height=442&id=u680240fe&originHeight=442&originWidth=733&originalType=binary&ratio=1&rotation=0&showTitle=false&size=204123&status=done&style=none&taskId=u556cb6a2-ea33-410a-8a52-f3c999808ac&title=&width=733)<br />最重要的是框住的那些内容，如果不写这些会造成死循环，如果要迭代执行应该首先写这两个内容。
<a name="s4nyD"></a>
# 第二十二节MGlobal全局操作类
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653460030778-cab5a9e7-748b-46df-8294-66239100e37d.png#clientId=u9947dbe0-b82a-4&from=paste&height=545&id=ucbe51d44&originHeight=545&originWidth=976&originalType=binary&ratio=1&rotation=0&showTitle=false&size=127099&status=done&style=none&taskId=ue7133d2d-e668-4a79-a8f4-8c2baeb2ea1&title=&width=976)<br />重点：不需要实例化<br />静态方法：<br />mayaVersion：返回当前maya的版本号<br />getActiveSelectionList(MSelectionList的对象)：将我们在maya中选择的内容存入到传递的实例化的MSelectionList中（会替换列表中的内容，例如选择了5个物体执行命令列表会有5个，再选择1个物体执行命令列表会变成1个）。<br />setActiveSelectionList(MSelectionList的对象): 类似于select命令后面跟一组列表，将列表中的物体选择。<br />executeCommand:参数中写mel命令，可以通过api使用这些命令<br />executePythonCommand：参数中写python命令，可以通过api使用这些命令<br />isYAxisUp：判断场景的向上轴是否为Y轴，如果是返回True，如果不是返回False。同理isZAxisUp<br />displayInfo：显示输出信息，参数是字符串<br />displayWarning：输出显示警告信息![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653461558722-6d62fc39-94a0-4d2d-9a96-b22de5ea1b2c.png#clientId=u9947dbe0-b82a-4&from=paste&height=57&id=u91af9ddd&originHeight=57&originWidth=300&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1723&status=done&style=none&taskId=ua7776fb5-4a3e-4c2a-9fa9-6ff5f848d51&title=&width=300)<br />displayError： 输出显示错误信息<br />viewFrame: 参数为整数，调整当前帧的位置<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653461723498-23836da2-e0a1-4893-864d-0c0d59c33a59.png#clientId=u9947dbe0-b82a-4&from=paste&height=817&id=u869cdd62&originHeight=817&originWidth=1091&originalType=binary&ratio=1&rotation=0&showTitle=false&size=424890&status=done&style=none&taskId=u1a550001-cef8-460c-a626-0e4af3d449a&title=&width=1091)
<a name="h291n"></a>
# 第二十三节MFileIO文件操作类
MFileIO同样是一个全局的操作类，使用它不需要实例化<br />currentFile: 返回当前的场景的路径<br />setCurrentFile： 更改当前场景的名字路径，参数为字符串<br />fileType： 返回当前场景文件类型<br />查看可以保存的文件类型（结果在列表中）：<br />--------------------------------------------<br />lst = list()<br />OpenMaya.MFileIO.getFileTypes(lst)<br />[u'mayaAscii', u'mayaBinary', u'mel', u'OBJ', u'directory', u'plug-in', u'audio', u'move', u'EPS', u'Adobe(R) Illustrator(R)', u'image', u'fluidCache', u'editMA', u'editMB', u'IGES_ATF', u'JT_ATF', u'PARASOLID_ATF', u'SAT_ATF', u'STEP_ATF', u'WIRE_ATF', u'CATIAV4_ATF', u'CATIAV5_ATF', u'DWG_ATF', u'DXF_ATF', u'NX_ATF', u'PROE_ATF', u'IGES_ATF Export', u'JT_ATF Export', u'PARASOLID_ATF Export', u'SAT_ATF Export', u'STEP_ATF Export', u'WIRE_ATF Export', u'CATIAV5_ATF Export', u'DWG_ATF Export', u'DXF_ATF Export', u'NX_ATF Export', u'FBX', u'FBX export', u'DAE_FBX', u'DAE_FBX export', u'SVG', u'ASS Export', u'ASS', u'Alembic', u'OBJexport', u'BIF']<br />-------------------------------------------<br />newFile(True)：创建一个新的场景（强制）<br />save：保存场景<br />saveAs:另存场景，第一个参数为保存路径，第二个参数为保存类型（例如'mayaBinary','mayaAscii'）<br />exportSelected：导出选择的物体，也是两个参数，第一个参数为文件路径，第二个参数为文件类型<br />exportAll:导出所有物体。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653466792218-28a24098-7fd7-4296-a138-44a7aac9970f.png#clientId=u9947dbe0-b82a-4&from=paste&height=982&id=u497fff7a&originHeight=982&originWidth=1079&originalType=binary&ratio=1&rotation=0&showTitle=false&size=324039&status=done&style=none&taskId=u7d5ef7f6-9fca-411d-aad6-a8f0d64865e&title=&width=1079)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653466815616-30af3357-ac40-41ac-9c98-78731d1e5c29.png#clientId=u9947dbe0-b82a-4&from=paste&height=968&id=ub5ccc466&originHeight=968&originWidth=1195&originalType=binary&ratio=1&rotation=0&showTitle=false&size=478134&status=done&style=none&taskId=uc93c2107-05f1-483e-aac8-c724f721797&title=&width=1195)
<a name="JV6lB"></a>
# 第二十四节MFnDependencyNode与MItDependencyNodes
<a name="JaA1h"></a>
## MFnDependencyNode
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1653467327390-60981704-8b89-453a-827d-7b4c35f5aabc.png#clientId=u9947dbe0-b82a-4&from=paste&height=438&id=u9208539b&originHeight=438&originWidth=849&originalType=binary&ratio=1&rotation=0&showTitle=false&size=121025&status=done&style=none&taskId=u706087b2-8e51-4a49-ba74-3907f436030&title=&width=849)<br />在maya中所有的物体都是以节点的形式来存在的，它们最基本的模式就是一个DependencyNode，带有层级的那些节点都是从DependencyNode扩展而来，变成了DagNode，通过不同的继承发展成不同的节点。<br />在maya中的所有的节点，都可以使用MFnDependencyNode方法<br />创建MFnDependencyNode的方法：<br />第一个：如果直接通过 MFnDependencyNode()语句创建，这样创建出来的不能与任何节点进行连接，创建出来的实际上是一个空的，没有任何意义。<br />第二个：通过传入一个MObject来实例化一个MFnDependencyNode，通过MObject，maya可以追踪到任何一个节点。<br />配合pymel快速传入MObject：<br />mfn = OpenMaya.MFnDependencyNode(pm.ls(sl=True)[0].__apimobject__())<br />**MFnDependencyNode的常用方法：**<br />typeName:返回节点类型<br />name：返回节点名字<br />setName(要更改的名字)：更改节点的名字<br />attributeCount：查询节点有多少个属性<br />attribute：通过属性的名字返回MObject(指针)<br />findPlug：同样是返回属性<br />isLocked：判断是否锁定<br />hasAttribute ：判断有没有属性<br />icon：节点查询图标<br />setIcon ： 设置图标
<a name="OQEbn"></a>
## MItDependencyNodes
MItDependencyNodes可以过滤场景中的所有基本节点，我们可以通过这个迭代器来达到我们命令中使用ls的这种效果。<br />iterator = OpenMaya.MItDependencyNodes(OpenMaya.MFn.kMesh)  #创建一个迭代器对象，用来过滤场景中的所有多边形类型<br />在maya中所有的迭代器都有一个isDone方法用来判断迭代器是否已经迭代完成
```python
import maya.OpenMaya as OpenMaya
# 创建一个过滤mesh类型的迭代器
iterator = OpenMaya.MItDependencyNodes(OpenMaya.MFn.kMesh)
while not iterator.isDone():
    # 通过iterator.thisNode()得到迭代器中的节点（MObject）
    # 然后将MObject给MFnDependencyNode来使用DependencyNode的方法（name）
    print OpenMaya.MFnDependencyNode(iterator.thisNode()).name() # 输出场景中的多边形的名字
    iterator.next()
```

<a name="xsfp9"></a>
# 第二十五节MFnDagNode和MItDag
<a name="kb5QR"></a>
## MFnDagNode
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654467583261-8453b27c-0de0-473a-b13e-8675228c40d8.png#clientId=u004a41f6-956d-4&from=paste&height=801&id=ubd4048a4&originHeight=801&originWidth=1171&originalType=binary&ratio=1&rotation=0&showTitle=false&size=224149&status=done&style=none&taskId=ue94af028-6444-442e-8b33-5a9f6974d01&title=&width=1171)<br />MFnDagNode常用方法：<br />parent<br />child<br />hasParent<br />hasChild<br />isParentOf<br />isChildOf<br />dagPath<br />fullPathName<br />partialPathName
```python
import maya.OpenMaya as OpenMaya
import pymel.core as pm
# pm.PyNode('pSphere1').__apiobject__()找到场景中类型为MDagPath的pSphere1
# 当指定后,即使后续更改物体的名字,maya依然能够找到对应的物体。
# api和pymel是一样的,都是直接绑定到节点上的,不依据字符串查找,即使节点发生变化依然可以追踪到。
mfn=OpenMaya.MFnDagNode(pm.PyNode('pSphere1').__apiobject__())
mfn.partialPathName() # 得到pSphere1的短名
mfn.fullPathName() # 得到pSphere1的长名 
mfn.childCount() # 查询pSphere1的下一级有几个物体（包含shape）
mfn.child(0) # 得到pSphere1的第一个子物体 类型为MObject
mfn.parent(0) # 得到pSphere1的第一个父物体 类型为MObject
OpenMaya.MFnDagNode(mfn.parent(0)).partialPathName() # 输出pSphere1的第一个父物体的短名
mfn.removeChildAt(1) # 移除pSphere1的第二个子物体（第一个子物体是pSphereShape1），也会携带着移除第二个子物体的所有子级
```
<a name="vzQEv"></a>
## MItDag
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654473278734-4567a1ed-d4ed-4f3c-8e10-d4e34c5dfd12.png#averageHue=%23303030&clientId=u004a41f6-956d-4&from=paste&height=375&id=u882e443f&originHeight=375&originWidth=920&originalType=binary&ratio=1&rotation=0&showTitle=false&size=86367&status=done&style=none&taskId=udaf4fc99-848b-4735-8118-b0860a2939e&title=&width=920)

```python
import maya.OpenMaya as OpenMaya
import pymel.core as pm
iterator = OpenMaya.MItDag()
# 将迭代器的迭代起始点为group4，方式为广度优先，迭代类型为mesh类型
iterator.reset(pm.PyNode('group4').__apiobject__(),OpenMaya.MItDag.kBreadthFirst,OpenMaya.MFn.kMesh) 
while not iterator.isDone():
    print iterator.partialPathName() 
    iterator.next()
```
其中迭代器的自带方法中的 partialPathName是返回的字符串，代表当前迭代项的名字，如果使用currentItem返回的是当前迭代项的MObject。

<a name="gFqip"></a>
# 第二十六节MFnMesh与MItMesh
<a name="T4pYL"></a>
## MFnMesh
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654481092141-3ce18d58-c913-4d13-8f5d-9ce8e07c3aaa.png#averageHue=%23313131&clientId=u7402bc27-1154-4&from=paste&height=594&id=uc0293a34&originHeight=594&originWidth=1783&originalType=binary&ratio=1&rotation=0&showTitle=false&size=247196&status=done&style=none&taskId=ua7839acf-dd70-495f-8896-187bf243ce7&title=&width=1783)
```python
# coding:utf-8
import maya.OpenMaya as OpenMaya
import pymel.core as pm

mfn = OpenMaya.MFnMesh(pm.PyNode('pSphere1').__apiobject__())
mfn.numVertices()  # 查询pSphere1有多少个顶点。
mfn.numEdges()  # 查询有多少根线。
mfn.numPolygons()  # 查询有多少个面。
point = OpenMaya.MPoint() # 定义一个空的MPoint类型的对象
mfn.getPoint(0, point) # 将pSphere1的序列号为0的顶点赋予刚才定义的MPoint类型的对象
print point.x, point.y, point.z # 输出赋予顶点后的point的xyz
point1 = OpenMaya.MPoint(0, 1, 0) # 定义一个携带数值的MPoint类型的对象
mfn.setPoint(381, point1) # 将pSphere1的序列号为381的顶点的数值设置为point1携带的数值
```
<a name="poySg"></a>
## MItMesh
MItMesh有四种类型分别是MItMeshPolygon，MItMeshVertex，MItMeshEdge，MItMeshFaceVertex<br />用的最多的是Vertex，polygon，edge
```python
# coding:utf-8
import maya.OpenMaya as OpenMaya
import pymel.core as pm

iterator = OpenMaya.MItMeshVertex(pm.PyNode('pSphereShape1').__apimobject__()) # 使用apimobject得到MObject类型的对象
while not iterator.isDone():
    print iterator.index()  # 得到迭代器中的顶点的序列号

    point = iterator.position()  # 通过position方法得到携带位置信息的MPoint类型的顶点，然后赋予point
    print point.x, point.y, point.z  # 配合while输出每个顶点的位置信息
    # 将所有顶点的位置设置为0，0，0
    point1 = OpenMaya.MPoint(0, 0, 0)
    iterator.setPosition(point1)
    iterator.next()

```
<a name="JcUo4"></a>
# 第二十七节PythonApi与指针
有些方法需要传递带类型的指针，因此如果使用python语句就需要通过MScriptUtil来定义对应类型的指针。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654485856359-79877248-42b0-4e43-a0b8-2d0fbccacca3.png#averageHue=%23333333&clientId=u7402bc27-1154-4&from=paste&height=692&id=ub2b77fe0&originHeight=692&originWidth=1576&originalType=binary&ratio=1&rotation=0&showTitle=false&size=271237&status=done&style=none&taskId=ufff90242-4aa4-4542-aeeb-c047e5bfda4&title=&width=1576)带有Util的一般都是通用的工具函数<br />有些方法是需要传入 float2 类型的指针，为了能够在python中使用因此需要通过MScriptUtil<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654500263988-a2847039-6d46-469c-9d4a-6dc5333729d4.png#averageHue=%23e2e6e9&clientId=ue46ddd59-53b5-4&from=paste&height=94&id=u8e25b979&originHeight=94&originWidth=780&originalType=binary&ratio=1&rotation=0&showTitle=false&size=70299&status=done&style=none&taskId=ube991ac4-903a-4e97-9e7c-652a4c41fdc&title=&width=780)<br />MScriptUtil的使用：
```python
# coding:utf-8
import maya.OpenMaya as OpenMaya
import pymel.core as pm

iterator = OpenMaya.MItMeshVertex(pm.PyNode('pSphereShape1').__apimobject__())  # 使用apimobject得到MObject类型的对象

s_util = OpenMaya.MScriptUtil()  # 定义一个MScriptUtil
uv_ptr = s_util.asFloat2Ptr()  # 通过使用MScriptUtil中的方法定义一个float2类型的指针

while not iterator.isDone():
    iterator.getUV(uv_ptr)  # 将顶点的UV值传递给自定义的float2类型的uv_ptr指针
    print s_util.getFloat2ArrayItem(uv_ptr, 0, 0),  # 输出指针中的0，0对应的值（u坐标）
    print s_util.getFloat2ArrayItem(uv_ptr, 0, 1)  # 输出指针中的0，1对应的值（v坐标）
    iterator.next()

```
根据所需要的指针类型加上as就可以直接得到了。<br />如果要在指针中求值就需要使用get开头的方法，传进去指针就可以了。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654500969237-24272dcd-ee4d-4a59-8f61-3103436ee83c.png#averageHue=%23353534&clientId=ue46ddd59-53b5-4&from=paste&height=1275&id=ufd27250b&originHeight=1275&originWidth=1326&originalType=binary&ratio=1&rotation=0&showTitle=false&size=513694&status=done&style=none&taskId=uefdd3dbd-8583-480a-b7bb-4623a8fe137&title=&width=1326)
<a name="K4Qaz"></a>
# 第二十八节MayaAPI事件触发 - MMessage
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654501986078-41f36b55-24c8-4bfc-b0d7-82964a96311a.png#averageHue=%23303030&clientId=u7402bc27-1154-4&from=paste&height=1312&id=u69829333&originHeight=1312&originWidth=2131&originalType=binary&ratio=1&rotation=0&showTitle=false&size=463350&status=done&style=none&taskId=ua80f079c-67e8-43a8-9112-b9490cdfdd3&title=&width=2131)<br />要操作物体层级相关的，就用MDagMessage<br />要操作普通节点相关的，就用MDGMessage<br />调用命令的时候就用MCommandMessage<br />要绑定某一个节点上的事件，比如说属性变化时可以使用MNodeMessage<br />可以使用多边形的MPolyMessage<br />场景变化或更新时可以使用MSceneMessage
<a name="X1SeI"></a>
## 案例MTimerMessage
首先了解一下MTimerMessage的一个方法，addTimerCallback,其中callback的意思是回调函数，什么是回调函数？作为参数传递的那个函数就被叫为回调函数。<br /> ![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654504577713-39ade796-d258-40d2-9d5a-25c2b7476346.png#averageHue=%23dee5ea&clientId=ufbfe3503-7f09-4&from=paste&height=61&id=uf1977945&originHeight=61&originWidth=1336&originalType=binary&ratio=1&rotation=0&showTitle=false&size=61741&status=done&style=none&taskId=u440d3a93-00bf-4074-aa97-27cab4baf8f&title=&width=1336)
```python
# coding:utf-8
import maya.OpenMaya as OpenMaya
def func(*args): # 定义回调函数,输出1以及传入的参数（传入的第一个是间隔时间，第二个是持续时间）
    print 1,args
callback_id = OpenMaya.MTimerMessage.addTimerCallback(2,func) # 每隔两秒执行一次定义的回调函数
OpenMaya.MTimerMessage.removeCallback(callback_id) # 移除刚才定义的定时器

```
<a name="Z3oXB"></a>
## 案例MEventMessage
MEventMessage的addEventCallback方法所需要的参数：<br />第一个参数是事件名字。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1654504982544-1f60d9ed-08b6-43fd-8ef1-c84d589b71e9.png#averageHue=%23e1e5e8&clientId=ufbfe3503-7f09-4&from=paste&height=66&id=u99fc771c&originHeight=66&originWidth=1782&originalType=binary&ratio=1&rotation=0&showTitle=false&size=105273&status=done&style=none&taskId=u0984e5b5-e490-4d9f-8508-47da561cd61&title=&width=1782)<br />MEventMessage通过事件触发，而这些事件都是哪些可以通过getEventNames来得到：<br />得到MEventMessage所支持的事件：
```python
# coding:utf-8
import maya.OpenMaya as OpenMaya
event_names = list() # 定义一个空列表用来存取事件名字
OpenMaya.MEventMessage.getEventNames(event_names) # 将事件名字存入到列表event_names中
print event_names # 输出列表
```
其中常用的事件：<br />deleteAll，undoSupressed（撤销后的返回），undo（撤销），timeChanged（时间轴变化）<br />其他事件的解释可以通过scriptjob命令的帮助文档找到:<br />[https://help.autodesk.com/view/MAYAUL/2018/ENU/?guid=__CommandsPython_index_html](https://help.autodesk.com/view/MAYAUL/2018/ENU/?guid=__CommandsPython_index_html)
```python
# coding:utf-8
import maya.OpenMaya as OpenMaya
def func(*args): # 定义回调函数,输出1以及传入的参数（传入的第一个是间隔时间，第二个是持续时间）
    print 1,args
callback_id = OpenMaya.MEventMessage.addEventCallback('timeChanged',func) # 当时间轴变化时触发回调函数
OpenMaya.MEventMessage.removeCallback(callback_id) # 移除刚才定义事件触发器
```


<a name="Pb0Ga"></a>
# 练习
<a name="OVFgx"></a>
## 第一节
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648299847402-394103f7-8a94-4d67-8f38-44e7dbcc2297.png#averageHue=%23343434&clientId=u72970d88-4bcf-4&from=paste&height=800&id=ud66ae093&originHeight=800&originWidth=1803&originalType=binary&ratio=1&rotation=0&showTitle=false&size=287685&status=done&style=none&taskId=uc703759d-d406-4ea1-adb0-fc4653abb8a&title=&width=1803)<br />circle;<br />circle -r 2;<br />circle - r 2 -nr 0 1 0;<br />curve -d 1 -p -2 0 -2 -p 3 0 -2 -p 3 0 3 -p -2 0 3 -p -2 0 -2;
```python
import maya.cmds as mc
mc.circle()
mc.circle(r=2)
mc.circle(r=2,nr=(0,1,0))
mc.curve(d=1,p=[(-2,0,-2),(3,0,-2),(3,0,3),(-2,0,3),(-2,0,-2)])

```
<a name="iUXKm"></a>
## 第二节
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648347312751-5a08ec69-1a66-4cf8-b7e8-4ef9b2c6bbb0.png#averageHue=%233c3c3c&clientId=ue82b3c53-47c5-4&from=paste&height=196&id=ue3bbf5ea&originHeight=196&originWidth=1023&originalType=binary&ratio=1&rotation=0&showTitle=false&size=69465&status=done&style=none&taskId=u9bc20f7f-ead1-4439-b4dc-c6556544a40&title=&width=1023)<br />这个跟课中讲的批量重命名应该差不多。
```python
import maya.cmds as mc
for shape in mc.ls(typ='mesh'):
    mc.rename(shape,'mesh_{0}'.format(shape))

```
<a name="qFEMn"></a>
## 第五节
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648470105020-ae661d75-bd1a-467a-9154-77f197eb8ae5.png#averageHue=%233e3e3e&clientId=uf7c342ae-9460-4&from=paste&height=85&id=u996515ec&originHeight=85&originWidth=675&originalType=binary&ratio=1&rotation=0&showTitle=false&size=27474&status=done&style=none&taskId=u147f72b4-92ea-4079-8765-81df4dab0fd&title=&width=675)
```python
import maya.cmds as mc

sel = mc.ls(sl=1)
info = []
info_str = ''
for i in sel:
    posx = mc.getAttr(i + '.tx')
    posy = mc.getAttr(i + '.ty')
    posz = mc.getAttr(i + '.tz')
    type = mc.objectType(i)
    info.append([i, posx, posy, posz,type])
for i in info:
    info_str = info_str + i[0]+' type:'+i[4] + '\r\nposx:' + str(i[1]) + '\r\nposy:' + str(i[2]) + '\r\nposz:' + str(
        i[3]) + '\r\n\r\n'
    f = open('D:\\posInfo.txt', 'w') 
    f.write(info_str)
    f.close()
```
<a name="TruIa"></a>
## 第七节
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648544898343-44bafffa-267a-4e1a-bbef-542fe65f0039.png#averageHue=%234f4f4f&clientId=u783b1c22-f3a3-4&from=paste&height=704&id=u4a5230dd&originHeight=704&originWidth=1159&originalType=binary&ratio=1&rotation=0&showTitle=false&size=186745&status=done&style=none&taskId=u77b41c6e-4c88-4a8f-91b9-56a09b39dab&title=&width=1159)
```python
import maya.cmds as mc
for i in range(3) :
    lam=mc.createNode('lambert')
mc.createNode('blendColors')
mc.connectAttr('lambert2.oc','blendColors1.c1')
mc.connectAttr('lambert3.oc','blendColors1.c2')
mc.connectAttr('blendColors1.output','lambert4.c')

```
<a name="qv1xR"></a>
## 第十节
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648779599871-a2c84be5-3707-4833-982d-b0d82b0da25a.png#averageHue=%23383838&clientId=u693e63da-04bd-4&from=paste&height=123&id=u75cbb5d0&originHeight=123&originWidth=755&originalType=binary&ratio=1&rotation=0&showTitle=false&size=31039&status=done&style=none&taskId=ubd9b41fe-1047-41e0-bbd3-e9943cfbfa8&title=&width=755)
```python
import maya.cmds as mc
import random
for i in range(200):
    pox=random.randrange(-10,10)
    poy=random.randrange(-10,10)
    poz=random.randrange(-10,10)
    mc.setKeyframe('pSphere1',at='tx',t=i,v=pox)
    mc.setKeyframe('pSphere1',at='ty',t=i,v=poy)
    mc.setKeyframe('pSphere1',at='tz',t=i,v=poz)
```
<a name="zKmGS"></a>
## 第十二节
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648792874713-ce4a46bc-01e9-4b68-a8f1-ab2626d86522.png#averageHue=%23484848&clientId=u693e63da-04bd-4&from=paste&height=119&id=u1921642e&originHeight=119&originWidth=911&originalType=binary&ratio=1&rotation=0&showTitle=false&size=74932&status=done&style=none&taskId=ub1e57a2c-e477-4249-b0a7-c3ee19e1776&title=&width=911)
```python
import maya.cmds as mc
def ShowWindow():
    wnd_name='my_window'
    if mc.window(wnd_name,q=True,ex=True):
        mc.deleteUI(wnd_name,wnd=True)
    if mc.windowPref(wnd_name,q=True,ex=True):
        mc.windowPref(wnd_name,r=True)
    wnd = mc.window(wnd_name,w=400,h=300,t='My Window')
    mc.gridLayout(numberOfColumns=2, cellWidth=200)
    mc.text(l='num:')
    mc.intField('numInt')
    mc.text(l='radius:')
    mc.floatField('radiusFloat')
    mc.button('ok',command=onCreateClick)
    mc.showWindow(wnd)
def onCreateClick(*args):
    num=mc.intField('numInt',q=True,v=True)
    radius=mc.floatField('radiusFloat',q=True,v=True)
    create(num,radius)
    
def create(num,radius):
    for i in range(num):
        mc.polySphere(r=radius)
ShowWindow()
    

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1648813456649-b8fb708d-93e6-4916-8798-d473c6d944b9.png#averageHue=%23515151&clientId=u46a1ca6b-8b3c-4&from=paste&height=339&id=uae1b55f6&originHeight=339&originWidth=416&originalType=binary&ratio=1&rotation=0&showTitle=false&size=6016&status=done&style=none&taskId=u302f8c63-c8e3-4850-94de-9ea1f01b9eb&title=&width=416)通过点击ok根据num和radius创建对应的球体
