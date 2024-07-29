---
title: Python_for_nuke_101
tags: NukePy
categories: DCC工具开发
abbrlink: bc564b20
date: 2023-08-29 03:57:00
---
<meta name="referrer" content="no-referrer" />

[https://www.bilibili.com/video/BV1bm4y1R7X1/?spm_id_from=333.788&vd_source=b1de3fe38e887eb40fc55a5485724480](https://www.bilibili.com/video/BV1bm4y1R7X1/?spm_id_from=333.788&vd_source=b1de3fe38e887eb40fc55a5485724480)

# 为Nuke添加内置python编辑器
[github地址](https://github.com/plasmax/PythonEditor)

---
# 令脚本编辑器中显示在nuke中进行的操作对应的代码
首先按shift+s进入首选项设置界面,然后再Panels-Script Editor中勾选 echo python commands to output window

---
# 显示节点的详细信息(方便找节点属性名字)
首先选中节点,然后按键盘的i键即可弹出一个窗口,在里面可以找到节点的详细信息.

---
# 后台执行脚本
首先通过nuke.env['ExecutablePath']得到nuke程序的路径
然后如果是当前python脚本想要调用令一个python脚本的话,就通过'{}/另一个python脚本的名字.py'.format(os.path.dirname(__file__))找到要调用的另一个python脚本的路径,或者就直接用绝对路径.
然后创建command命令:command = '"{nuke}" -t -x {script} {要传入的额外参数}'
传入的额外参数可以在要调用的python脚本中通过sys.argv[1],sys.argv[2]...  来得到
最后通过subprocess.Popen(command, shell=True)来使用命令行
**后台执行脚本的要点就是命令里记得添加-t和-x即可,不添加就是前台调用了**

---
# 官方入门文档
[官方入门文档地址](https://learn.foundry.com/nuke/developers/latest/pythondevguide/basics.html)
从这个文档可以快速的了解到如何通过代码创建节点,设置节点属性,窗口的制作等.可以直接看,代码的英文直译很容易就能明白对应的意思.

---
# 常用的命令
通过节点类型得到对应节点: nuke.allNodes('Read')
得到选择的节点并设置节点的属性: 
select_node = nuke.selectedNode()
select_node['file'].setValue()
nuke消息窗口的显示: nuke.message("消息窗口内容")
得到当前工程名字:nuke.root().name()
打开项目:nuke.scriptOpen()
得到nuke程序的路径: nuke.env['ExecutablePath']
导入其他nuke文件: nuke.nodePaste()
保存nuke的文件:nuke.scriptSaveAs(prjPath)
保存当前nuke工程:nuke.scriptSave("")
清理当前nuke工程:nuke.scriptClear()
得到nuke程序的路径:nuke.env['ExecutablePath']



<a name="fuGgI"></a>
# 第一节
<a name="Olr2j"></a>
## 初始设置
在这个路径下C:\Users\用户名\.nuke，创建gizmos文件夹，python文件夹，init.py文件，menu.py文件。<br />init.py文件用来为nuke新增插件识别路径(这样就不需要每个文件夹都加一个__init__.py文件了)，都统一加到外面这个init.py文件。 <br />menu.py文件用来控制nuke启动时自动加载的功能<br />其中init.py文件中内容是
```
nuke.pluginAddPath('./gizmos')
nuke.pluginAddPath('./python')
```
<a name="z76gR"></a>
## 克服因操作平台的不同而导致的.nuke文件夹路径不同的问题
在menu.py文件中输入：<br />其中platform可以用来得到当前的操作平台<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1665992875669-ef7c2dd3-19cc-41f4-bd0b-3a6dac781f42.png#clientId=u162168ff-70af-4&errorMessage=unknown%20error&from=paste&height=540&id=uc062ab67&originHeight=540&originWidth=848&originalType=binary&ratio=1&rotation=0&showTitle=false&size=235547&status=error&style=none&taskId=u06683321-48b5-4ad8-8ce0-52fa2c148f5&title=&width=848)
<a name="YhCAa"></a>
# 第二节
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1665993055456-c5bb72fd-00cb-48e3-808e-16a610ad8ef3.png#clientId=u162168ff-70af-4&errorMessage=unknown%20error&from=paste&height=241&id=ud9fa2212&originHeight=241&originWidth=1093&originalType=binary&ratio=1&rotation=0&showTitle=false&size=87683&status=error&style=none&taskId=uc3832d5e-8f2b-47df-8b83-0474eafe1dc&title=&width=1093)
<a name="eM6Bw"></a>
## 设置创建节点时的默认值
nuke.knobDefault('Tracker4.shutteroffset',"centered")  # 设置Tracker节点的shutteroffset的默认值为centered<br />nuke.knobDefault('Tracker4.label', "Motion: [value transform]\nRef Frame: [value reference_frame]")  # 设置Tracker节点的label(节点的显示文本)为Motion: [value transform]\nRef Frame: [value reference_frame]也就是![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1665997817594-6575a0a1-28ff-44e5-ab3d-bbe2462e793d.png#clientId=u162168ff-70af-4&errorMessage=unknown%20error&from=paste&height=144&id=u09506540&originHeight=144&originWidth=583&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9283&status=error&style=none&taskId=ua7dcc081-1cd5-49f1-885a-c536f7bc1b6&title=&width=583)。加入后的前后对比：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1665997849926-81ba693d-374d-4d25-9272-31d25bcbc95c.png#clientId=u162168ff-70af-4&errorMessage=unknown%20error&from=paste&height=80&id=ud8e2d0db&originHeight=80&originWidth=250&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2207&status=error&style=none&taskId=u913a170e-07c1-4d20-9bc4-77326f2e537&title=&width=250)变成了![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1665998054815-c3d52778-568e-4743-b2a5-51e2107efd74.png#clientId=u162168ff-70af-4&errorMessage=unknown%20error&from=paste&height=145&id=u542a0746&originHeight=145&originWidth=266&originalType=binary&ratio=1&rotation=0&showTitle=false&size=4780&status=error&style=none&taskId=ud8c5c13b-78f5-417a-8364-9a874e74f3a&title=&width=266)。其中label中框号中的内容是属性值。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1665997430962-c3ff95db-c35e-4a7a-acdf-149c912a9a06.png#clientId=u162168ff-70af-4&errorMessage=unknown%20error&from=paste&height=89&id=u30676a33&originHeight=89&originWidth=856&originalType=binary&ratio=1&rotation=0&showTitle=false&size=41963&status=error&style=none&taskId=u167c3eb6-b800-43de-93ce-5e14c94f7af&title=&width=856) 在创建节点时当节点类型为Tracker时设置这个节点的reference_frame的值为nuke的时间滑块的frame值。
<a name="ZkfyO"></a>
## 自定义menu和gizmosmenu
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1665999940631-e7824e12-b83e-4a7a-aec2-60d904a993ec.png#clientId=u162168ff-70af-4&errorMessage=unknown%20error&from=paste&height=927&id=ub67c51e3&originHeight=927&originWidth=941&originalType=binary&ratio=1&rotation=0&showTitle=false&size=66705&status=error&style=none&taskId=u55f8c57b-a435-42e9-bba5-b9b2f59d14b&title=&width=941)<br />如何添加自定义菜单：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1666000564330-2d3e9ec6-a9a3-470c-af08-8d56cc2ac0d7.png#clientId=u162168ff-70af-4&errorMessage=unknown%20error&from=paste&height=1001&id=u5c0676a6&originHeight=1001&originWidth=1180&originalType=binary&ratio=1&rotation=0&showTitle=false&size=450591&status=error&style=none&taskId=udfa54024-2fd3-46a9-88aa-bd89be6e449&title=&width=1180)
```python
# coding:utf-8
import PythonEditor
PythonEditor.nuke_menu_setup(nuke_menu=True, node_menu=True, pane_menu=True)
import nuke
import platform
import nukescripts

# ----------------------------------------------------------------------------------------------------------------------
# 设置节点的默认设置
# ----------------------------------------------------------------------------------------------------------------------

nuke.knobDefault('Tracker4.shutteroffset', "centered")
nuke.knobDefault('Tracker4.label', "Motion: [value transform]\nRef Frame: [value reference_frame]")
nuke.addOnUserCreate(lambda: nuke.thisNode()['reference_frame'].setValue(nuke.frame()), nodeClass='Tracker4')


# ----------------------------------------------------------------------------------------------------------------------
# 自定义菜单
# ----------------------------------------------------------------------------------------------------------------------

utilitiesMenu = nuke.menu('Nuke').addMenu('Utilities')

utilitiesMenu.addCommand('Autocrop', 'nukescripts.autocrop()')

myGizmosMenu = nuke.menu('Nodes'.addMenu('myGizmos')

myGizmosMenu.addCommand('Autocrop', 'nukescripts.autocrop()')


# ----------------------------------------------------------------------------------------------------------------------
# 自定义快捷键
# ----------------------------------------------------------------------------------------------------------------------

nuke.menu('Nodes').addCommand("Transform/Tracker", "nuke.createNode('Tracker4)","ctrl+alt+t", icon="Tracker.png", shortcutContext=2')

```
<a name="jmdU7"></a>
## nuke自带的图标路径
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1666000435895-e482db9e-4971-42bb-8247-92599639966e.png#clientId=u162168ff-70af-4&errorMessage=unknown%20error&from=paste&height=59&id=u4d9c95e0&originHeight=59&originWidth=400&originalType=binary&ratio=1&rotation=0&showTitle=false&size=15847&status=error&style=none&taskId=uc84414ce-e548-4e01-ab86-3ae802db11f&title=&width=400)可以在图中的路径处找到nuke自带的图标的名字<br />然后添加menu时icon参数如果想要是nuke自带的图标那么就可以直接填图标的名字加后缀名，nuke会自动找到<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1666000444647-824bbbfb-45a0-44dd-946d-99bd91972fa3.png#clientId=u162168ff-70af-4&errorMessage=unknown%20error&from=paste&height=38&id=uc116cc0e&originHeight=38&originWidth=188&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7790&status=error&style=none&taskId=u506e4f39-be5e-41b8-9854-079f63979af&title=&width=188)
<a name="H9HGp"></a>
# 第三节
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1666059392341-80ef8e6d-d0e9-4c85-9fe5-3883217454b7.png#clientId=uc36b5c75-d21a-4&errorMessage=unknown%20error&from=paste&height=551&id=u94199da1&originHeight=551&originWidth=1017&originalType=binary&ratio=1&rotation=0&showTitle=false&size=52911&status=error&style=none&taskId=u2ae5d99c-8ff5-4350-ae0c-9fc4437a5c6&title=&width=1017)
<a name="b9Bkh"></a>
## 创建节点
nuke.createNode()
<a name="MlYPD"></a>
## 创建节点的同时设置属性值（不属于课程，之前自己搜的）
举例：nuke.nodes.Shuffle(inputs=[texO], red="red", green="black", blue="black", alpha="white")
<a name="oknM0"></a>
## 为节点创建预设与快捷键
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1666060461713-71ee7ea6-7061-419b-802a-4b92b1bc054c.png#clientId=uc36b5c75-d21a-4&errorMessage=unknown%20error&from=paste&height=105&id=u4d228d06&originHeight=105&originWidth=1717&originalType=binary&ratio=1&rotation=0&showTitle=false&size=109651&status=error&style=none&taskId=ubd43bc0e-ee59-428c-968e-a05272be8ef&title=&width=1717)
<a name="GNTz9"></a>
## 更改节点的属性值
举例，设置选择的节点的'bbox'属性值为'B'：nuke.selectedNode()['bbox'].setValue("B")<br />举例，自定义某一节点的属性值： nuke.toNode('Merge1')['bbox'].setValue("B")
<a name="gPUGu"></a>
## 通过for循环批量更改某一类型的节点属性值
设置所有merge2类型节点的属性值：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1666061251539-0dd170d7-424e-4e81-8db2-c94f68ea6946.png#clientId=uc36b5c75-d21a-4&errorMessage=unknown%20error&from=paste&height=92&id=u441acaf8&originHeight=92&originWidth=665&originalType=binary&ratio=1&rotation=0&showTitle=false&size=56666&status=error&style=none&taskId=u42f26017-1e8a-4831-b3d0-c1d5f7ee5e5&title=&width=665)
<a name="anVYM"></a>
## 通过代码得到节点的类型名
print nuke.selectedNode().Class()
<a name="z1eyh"></a>
# 第四节
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1666061714259-42d82bac-470c-40de-9381-3ba0dbee3466.png#clientId=uc36b5c75-d21a-4&errorMessage=unknown%20error&from=paste&height=663&id=u5a817660&originHeight=663&originWidth=1371&originalType=binary&ratio=1&rotation=0&showTitle=false&size=78977&status=error&style=none&taskId=u1c616561-29f7-4cab-b7e8-48f2a51f7ad&title=&width=1371)
<a name="t12th"></a>
## 介绍
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1666599735495-d70ee447-a597-446b-8ce5-7747ba8b1b01.png#clientId=u43f32edb-ecd5-4&errorMessage=unknown%20error&from=paste&height=317&id=u9158f1d5&originHeight=317&originWidth=311&originalType=binary&ratio=1&rotation=0&showTitle=false&size=11781&status=error&style=none&taskId=u7765dd8f-c545-42fe-b519-36801aef169&title=&width=311)<br />针对shuffle节点制作一些功能
<a name="dT6as"></a>
## shuffleShortcuts.py文件
在.nuke\python\shuffleShortcuts文件夹下创建个shuffleShortcuts.py文件
```python
import nuke


def createCustomShuffle(in_channel, out_channel, set_channel, rColor, gColor, bColor):
    my_shuffle = nuke.createNode("Shuffle")

    my_shuffle['in'].setValue(in_channel)
    my_shuffle['out'].setValue(out_channel)

    my_shuffle['red'].setValue(set_channel)
    my_shuffle['green'].setValue(set_channel)
    my_shuffle['blue'].setValue(set_channel)
    my_shuffle['alpha'].setValue(set_channel)

    my_shuffle['tile_color'].setValue(int('%02x%02x%02x%02x' % (rColor * 255, gColor * 255, bColor * 255, 1), 16))

    my_shuffle['label'].setValue("[value red] > [value out]")


def shuffleRGBchannels():
    select_node = nuke.selectedNode()

    select_node_x_pos = select_node['xpos'].value()
    select_node_y_pos = select_node['ypos'].value()

    createCustomShuffle('rgba', 'rgba', 'red', 1, 0, 0)
    red_shuffle = nuke.selectedNode()
    createCustomShuffle('rgba', 'rgba', 'green', 0, 1, 0)
    green_shuffle = nuke.selectedNode()
    createCustomShuffle('rgba', 'rgba', 'blue', 0, 0, 1)
    blue_shuffle = nuke.selectedNode()

    red_shuffle.setInput(0, select_node)
    red_shuffle['xpos'].setValue(select_node_x_pos - 150)
    red_shuffle['ypos'].setValue(select_node_y_pos + 150)

    green_shuffle.setInput(0, select_node)
    green_shuffle['xpos'].setValue(select_node_x_pos)
    green_shuffle['ypos'].setValue(select_node_y_pos + 150)

    blue_shuffle.setInput(0, select_node)
    blue_shuffle['xpos'].setValue(select_node_x_pos + 150)
    blue_shuffle['ypos'].setValue(select_node_y_pos + 150)


nuke.menu('Nodes').addCommand("Channel/Shuffle (Red to All)",
                              "shuffleShortcuts.createCustomShuffle('rgba', 'rgba', 'red', 1, 0, 0)",
                              "ctrl+shift+r", shortcutContext=2)
nuke.menu('Nodes').addCommand("Channel/Shuffle (Green to All)",
                              "shuffleShortcuts.createCustomShuffle('rgba', 'rgba', 'green', 0, 1, 0)",
                              "ctrl+shift+g", shortcutContext=2)
nuke.menu('Nodes').addCommand("Channel/Shuffle (Blue to All)",
                              "shuffleShortcuts.createCustomShuffle('rgba', 'rgba', 'red', 0, 0, 1)",
                              "ctrl+shift+b", shortcutContext=2)
nuke.menu('Nodes').addCommand("Channel/Shuffle (Alpha to All)",
                              "shuffleShortcuts.createCustomShuffle('rgba', 'rgba', 'red', 1, 1, 1)",
                              "ctrl+shift+a", shortcutContext=2)
nuke.menu('Nodes').addCommand("Channel/Shuffle (Alpha to 0)",
                              "shuffleShortcuts.createCustomShuffle('rgba', 'rgba', 'red', 0, 0, 0)",
                              shortcutContext=2)
nuke.menu('Nodes').addCommand("Channel/Shuffle (Alpha to 1)",
                              "shuffleShortcuts.createCustomShuffle('rgba', 'rgba', 'red', 1, 1, 1)",
                              shortcutContext=2)
nuke.menu('Nodes').addCommand("Channel/Shuffle (Split RGB channels)",
                              "shuffleShortcuts.shuffleRGBchannels()",
                              "ctrl+shift+s", shortcutContext=2)

```
<a name="uK2Td"></a>
## menu.py
然后在menu.py文件中导入这个模块<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1666599540497-2458ff54-b000-4c26-a5df-be499b687d92.png#clientId=u43f32edb-ecd5-4&errorMessage=unknown%20error&from=paste&height=127&id=u0626f8d0&originHeight=127&originWidth=1029&originalType=binary&ratio=1&rotation=0&showTitle=false&size=6020&status=error&style=none&taskId=u328ea895-aad4-44a8-ac5c-2850b3bb0a2&title=&width=1029)
<a name="bsCQI"></a>
## init.py
init.py文件中定义文件夹路径<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1666599580891-92363eb5-ba98-4d88-a3e5-063c15f76d70.png#clientId=u43f32edb-ecd5-4&errorMessage=unknown%20error&from=paste&height=143&id=uc5aa313d&originHeight=143&originWidth=437&originalType=binary&ratio=1&rotation=0&showTitle=false&size=16790&status=error&style=none&taskId=u7c97de82-13a0-4914-97a0-59267f47ac7&title=&width=437)
<a name="E9y81"></a>
# 第五节
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1666599898541-63507d90-c932-4181-ac8c-3771fef7d6f3.png#clientId=u43f32edb-ecd5-4&errorMessage=unknown%20error&from=paste&height=588&id=v7R3p&originHeight=588&originWidth=1341&originalType=binary&ratio=1&rotation=0&showTitle=false&size=212963&status=error&style=none&taskId=u6b7fd6cd-449e-4098-a27a-9e98b278865&title=&width=1341)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1666599891125-0c1f0e58-37ff-41af-b611-ee9489ffe73c.png#clientId=u43f32edb-ecd5-4&errorMessage=unknown%20error&from=paste&height=842&id=u6b1c5e27&originHeight=842&originWidth=1600&originalType=binary&ratio=1&rotation=0&showTitle=false&size=107703&status=error&style=none&taskId=u2015f305-efa4-4920-ba42-793bc8ee270&title=&width=1600)
<a name="R2T0w"></a>
## 得到项目路径
nuke.root()['name'].value()
<a name="ecCRC"></a>
## <br />定位字符串的特定值
举例字符串： Checkerboard_Small_v0002.png  输出 Checkerboard_Smal

```python
name_ext = "Checkerboard_Small_v0002.png"
name = name_ext[0:name_ext.find('_v')]
print name # Checkerboard_Small
```
<a name="oefiY"></a>
# 第六节
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1666603966753-835d86a9-6896-4f10-8829-4a09716a827f.png#clientId=u43f32edb-ecd5-4&errorMessage=unknown%20error&from=paste&height=530&id=uceb3e21c&originHeight=530&originWidth=1298&originalType=binary&ratio=1&rotation=0&showTitle=false&size=197709&status=error&style=none&taskId=ub0dab412-d403-4cd2-872f-93e75582629&title=&width=1298)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1666603950466-9c6fcf6f-a2be-4471-91b3-a546c244f756.png#clientId=u43f32edb-ecd5-4&errorMessage=unknown%20error&from=paste&height=758&id=ub665f68c&originHeight=758&originWidth=970&originalType=binary&ratio=1&rotation=0&showTitle=false&size=66312&status=error&style=none&taskId=u0dc0ff81-857c-4146-b3d0-10e46a379f0&title=&width=970)
<a name="DGmOo"></a>
## 弹出输入框让用户输入
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1666604252525-be1e0a09-b9e5-40d5-8087-c60e64d53474.png#clientId=u43f32edb-ecd5-4&errorMessage=unknown%20error&from=paste&height=135&id=uae1f3949&originHeight=135&originWidth=216&originalType=binary&ratio=1&rotation=0&showTitle=false&size=6861&status=error&style=none&taskId=u9e05fc47-999f-43c9-8076-62fa7bf74ef&title=&width=216)<br />inputBox = nuke.getInput("My First Window", "default text")<br />如果点击Cancel按钮，那么inputBox的值为None
<a name="cAZcM"></a>
## 在nuke菜单下放置一个让用户输入所选节点label的工具
首先按照课程的文件夹排列，我们的流程就是，在.nuke\python\shuffleShortcuts文件夹下创建一个新的.py工具文件（主要是因为init.py文件定义了这个文件夹为插件加载路径）<br />然后去menu.py文件中导入这个新的.py工具文件，这样nuke就能够调用.py文件了。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1666665329501-34479b29-a043-4910-bb18-8d1c908559ae.png#clientId=u2c4d4940-f26c-4&errorMessage=unknown%20error&from=paste&height=135&id=u308f65fc&originHeight=135&originWidth=216&originalType=binary&ratio=1&rotation=0&showTitle=false&size=5198&status=error&style=none&taskId=u2f080a9d-bdf5-440e-a90c-f05178e9973&title=&width=216)
<a name="EAlTE"></a>
### shortcut_NodeComment.py
```python
import nuke


def shortcut_NodeComment():
    selected_node = nuke.selectedNode()

    old_comment = selected_node['label'].value()

    input_box = nuke.getInput("Please enter a node label", old_comment)

    if not input_box:
        nuke.message("Node label will remain as " + old_comment)
    else:
        selected_node['label'].setValue(input_box)


nuke.menu('Nuke').addCommand('Edit/Shortcuts/Add Comment to Node', 'shortcut_NodeComment.shortcut_NodeComment()',
                             'ctrl+alt+c', shortcutContext=2)

```
<a name="mVc04"></a>
### menu.py
```python
import shortcut_NodeComment
```
<a name="uGPp6"></a>
### init.py
```python
nuke.pluginAddPath('./python/shuffleShortcuts')
```
<a name="P4w6c"></a>
## （扩展版）在nuke菜单下放置一个让用户输入所选节点label的工具
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1666670860005-de8228fb-3a85-4681-9efe-c58e2b2405bd.png#clientId=u2c4d4940-f26c-4&errorMessage=unknown%20error&from=paste&height=184&id=u9314180b&originHeight=184&originWidth=277&originalType=binary&ratio=1&rotation=0&showTitle=false&size=8943&status=error&style=none&taskId=u258865ad-8359-43c2-9fa0-51c271a28bd&title=&width=277)<br />不仅可以设置内容，也可以设置显示knob属性，也可以设置节点颜色<br />内嵌的panel写法举例
```python
import nukescripts.panels
class my_panel(nukescripts.panels.PythonPanel):
    def __init__(self):
        super(my_panel, self).__init__('my_panel')
        selected_Node = nuke.selectedNode()
        old_comment = selected_Node['label'].value()
        knob_list = []

        for i in selected_Node.knobs():
            knob_list.append(i)

        self.old_comment_slt = nuke.String_Knob("Comment", "Comment", old_comment)
        self.addKnob(self.old_comment_slt)
        self.knob_list = nuke.Enumeration_Knob("Knob","Knob", knob_list)
        self.addKnob(self.knob_list)
        self.colour_bool = nuke.Boolean_Knob("Change Node Colour?", "Change Node Colour?", False)
        self.addKnob(self.colour_bool)
        
        
p = my_panel()
p.show()
```
教程中的panel写法
```python
import nuke


def short_NodeCustomizer():
    selected_Node = nuke.selectedNode()
    old_comment = selected_Node['label'].value()
    knob_list = []

    for i in selected_Node.knobs():
        knob_list.append(i)

    knob_list.sort()
    knob_list.insert(0, 'None')

    knob_list_string = " ".join(knob_list)

    panel = nuke.Panel("Node Customizer")

    panel.addSingleLineInput("Comment", old_comment)
    panel.addEnumerationPulldown("Knob", knob_list_string)
    panel.addBooleanCheckBox("Change Node Colour?", False)

    if not panel.show():
        return

    comment_input = panel.value("Comment")
    knob_choice = panel.value("Knob")
    node_label = comment_input + "\n" + knob_choice + ": [value " + knob_choice + "]"

    if comment_input == "" and panel.value("Knob") == "None" and not panel.value("Change Node Colour?"):
        nuke.message("Please enter a node label")
        return
    elif knob_choice == "None":
        selected_Node['label'].setValue(comment_input)
    elif comment_input == "":
        selected_Node['label'].setValue(knob_choice + ": [value " + knob_choice + "]")
    else:
        selected_Node['label'].setValue(node_label)

    if panel.value("Change Node Colour?"):
        selected_Node['tile_color'].setValue(nuke.getColor())
    else:
        return

    nuke.menu('Nuke').addCommand('Utilities/Node Customizer', 'shortcut_NodeCustomizer.shortcut_NodeCustomizer()')
```
<a name="viWn2"></a>
# 第八节
<a name="mX3Zb"></a>
## TCL的使用，链接属性
<a name="utf1K"></a>
## moblur_controller.py
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1666680535160-079a3a99-42ba-4263-88df-6b251e8831d7.png#clientId=u40b40fbc-04d8-4&from=paste&height=202&id=u69314819&originHeight=202&originWidth=538&originalType=binary&ratio=1&rotation=0&showTitle=false&size=10243&status=done&style=none&taskId=u740e63dc-e998-486e-8c27-af678f0d914&title=&width=538)<br />创建NoOp节点配合TCL表达式，使只通过控制NoOp节点的数值，即可控制所有nuke节点网络图中带有对应属性的属性值。
```python
# coding:utf-8
import nuke


def moblur_controller():
    node_list = []

    for n in nuke.allNodes():
        if n.knob('motionblur') or n.knob('samples'):
            node_list.append(n)

    NoOp = nuke.createNode('NoOp')  # 使用TCL表达式需要的节点
    NoOp['name'].setValue("GLOBAL_MOTIONBLUR_CONTROLLER")

    NoOp['tile_color'].setValue(255)
    NoOp['note_font'].setValue("Bold")

    NoOp.addKnob(nuke.Int_Knob('global_motionblur', "motionblur"))
    NoOp.addKnob(nuke.Double_Knob('global_shutter', "shutter"))
    NoOp.addKnob(nuke.Boolean_Knob('global_disable_moblur', "disable motionblur"))

    NoOp['global_motionblur'].setValue(1)
    NoOp['global_shutter'].setValue(0.5)

    NoOp['global_disable_moblur'].setFlag(nuke.STARTLINE)  # 设置将这个控件另起一行放置

    for node in node_list:
        if node.knob('motionblur'):
            node['motionblur'].setExpression(
                'GLOBAL_MOTIONBLUR_CONTROLLER.global_disable_moblur == 0 ? GLOBAL_MOTIONBLUR_CONTROLLER.global_motionblur : 0')

            node['shutter'].setExpression('GLOBAL_MOTIONBLUR_CONTROLLER.globsl_shutter')

        elif node.knob('samples'):
            node['samples'].setExpression(
                'GLOBAL_MOTIONBLUR_CONTROLLER.global_disable_moblur == 0 ? GLOBAL_MOTIONBLUR_CONTROLLER.global_motionblur : 1')
            node['shutter'].setExpression('GLOBAL_MOTIONBLUR_CONTROLLER.globsl_shutter')

    # 当节点删除时执行这个函数功能，删除所有表达式链接，并将节点值设置回默认值
    def deleteExpressions():

        for node in node_list:
            if node.knob('motionblur'):
                node['motionblur'].clearAnimated()
                node['motionblur'].setValue(0)
                node['shutter'].clearAnimated()
                node['shutter'].setValue(0.5)

            elif node.knob('samples'):
                node['samples'].clearAnimated()
                node['samples'].setValue(1)
                node['shutter'].clearAnimated()
                node['shutter'].setValue(0.5)

    nuke.addOnDestroy(deleteExpressions)  # 当节点删除时执行


nuke.menu('Nuke').addCommand('Utilities/Global Motionblur Controller', 'moblur_controller.moblur_controller()')

```
<a name="L4YSK"></a>
# 第九节
<a name="iPCgW"></a>
## 使用nuke自带的自定义界面工具来扩展节点
在节点的属性界面右键点击![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1666685695316-5b6919db-2a1e-4d59-9e72-bc44a1ba02fc.png#clientId=u40b40fbc-04d8-4&from=paste&height=116&id=u777bcd0b&originHeight=116&originWidth=181&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2754&status=done&style=none&taskId=u45e20dd0-a54d-467f-9b26-fe52861e02a&title=&width=181)<br />然后就可以在这里自定义界面<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1666685795462-10ff5dc3-adcf-4e9d-bfc1-e94cd3e40b72.png#clientId=u40b40fbc-04d8-4&from=paste&height=536&id=u4dab91b9&originHeight=536&originWidth=485&originalType=binary&ratio=1&rotation=0&showTitle=false&size=29775&status=done&style=none&taskId=u1415f279-29cc-4186-b039-e0ab19fbd35&title=&width=485)<br />其中divider line是分割线<br />然后UI可以附带代码
<a name="N9zQn"></a>
### addNodes
```python
node_list = []
for node in nuke.selectedNodes():
    node_list.append(node.name())

nuke.thisNode().knob('addMoreNodes').setVisible(True)
nuke.thisNode().knob('addNodes').setVisible(False)

node_list_cleaned = '\n·'.join(node_list)

nuke.thisNode()['txtknob_node_list'].setValue("·"+node_list_cleaned)

def disableNodesInList():
    for i in node_list:
        if nuke.toNode(i).knob('disable'):
            nuke.toNode(i).knob('disable').setValue(nuke.thisNode().knob('disable').value())
        else:
            print "-" + i + "does not have a 'disable' knob Ignoring..."
nuke.toNode("NODE_DISABLER").knob("knobChanged").setValue('disableNodesInList()')
```
<a name="sk8La"></a>
### addMoreNodes
```python
for node in nuke.selectedNodes():
    if node.name() in node_list:
        print node.name()+" is already in the list"
    else:
        node_list.append(node.name())

node_list_cleaned = '\n·'.join(node_list)

nuke.thisNode()['txtknob_node_list'].setValue("·"+node_list_cleaned)

```
<a name="ba93d"></a>
### clearList
```python
node_list = []

nuke.thisNode().knob('addNodes').setVisible(True)
nuke.thisNode().knob('addMoreNodes').setVisible(False)

nuke.thisNode()['txtknob_node_list'].setValue("None")
```
<a name="lVd3t"></a>
## 将通过这种方法自定义的节点保存成gizmo
在.nuke\gizmos文件夹中新建gizmo文件<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1666687417594-6ea42975-c5bb-41d6-8dbb-e8bc93cb6f0e.png#clientId=u40b40fbc-04d8-4&from=paste&height=200&id=ue6c419a9&originHeight=200&originWidth=709&originalType=binary&ratio=1&rotation=0&showTitle=false&size=13065&status=done&style=none&taskId=u1c1ee9d0-18de-4b2a-b5cc-6b814e755f5&title=&width=709)<br />然后在nuke中选择节点按ctrl+c<br />然后进入gizmo文件按ctrl+v即可
```python
set cut_paste_input [stack 0]
version 10.5 v4
push $cut_paste_input
NoOp {
 name NODE_DISABLER
 knobChanged disableNodesInList()
 tile_color 0xff
 label "\[expr \{ \[value disable] == true ? \"Nodes Disabled\" : \"Nodes Enabled\" \}]"
 selected true
 xpos -180
 ypos -86
 addUserKnob {20 User}
 addUserKnob {26 ""}
 addUserKnob {22 addNodes l "Add Selected Nodes To List" T "node_list = \[]\nfor node in nuke.selectedNodes():\n    node_list.append(node.name())\n\nnuke.thisNode().knob('addMoreNodes').setVisible(True)\nnuke.thisNode().knob('addNodes').setVisible(False)\n\nnode_list_cleaned = '\\n·'.join(node_list)\n\nnuke.thisNode()\['txtknob_node_list'].setValue(\"·\"+node_list_cleaned)\n\ndef disableNodesInList():\n    for i in node_list:\n        if nuke.toNode(i).knob('disable'):\n            nuke.toNode(i).knob('disable').setValue(nuke.thisNode().knob('disable').value())\n        else:\n            print \"-\" + i + \"does not have a 'disable' knob Ignoring...\"\nnuke.toNode(\"NODE_DISABLER\").knob(\"knobChanged\").setValue('disableNodesInList()')" +STARTLINE}
 addUserKnob {22 addMoreNodes l "Add More Selected Nodes To List" +HIDDEN T "for node in nuke.selectedNodes():\n    if node.name() in node_list:\n        print node.name()+\" is already in the list\"\n    else:\n        node_list.append(node.name())\n\nnode_list_cleaned = '\\n·'.join(node_list)\n\nnuke.thisNode()\['txtknob_node_list'].setValue(\"·\"+node_list_cleaned)\n" +STARTLINE}
 addUserKnob {26 ""}
 addUserKnob {22 clearList l "Clear List" T "node_list = \[]\n\nnuke.thisNode().knob('addNodes').setVisible(True)\nnuke.thisNode().knob('addMoreNodes').setVisible(False)\n\nnuke.thisNode()\['txtknob_node_list'].setValue(\"None\")" +STARTLINE}
 addUserKnob {26 spacer l " " -STARTLINE T "    "}
 addUserKnob {6 disable -STARTLINE}
 addUserKnob {26 ""}
 addUserKnob {26 txtknob_node_list l "NODE LIST:" T None}
 addUserKnob {26 ""}
}

```

