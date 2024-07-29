---
title: MayaPy的一些补充(积累)
tags: MayaPy
categories: DCC工具开发
abbrlink: '64922297'
date: 2023-09-26 00:09:00
---
# 获得需要的内容
## 列举场景中的所有材质还有SG名称
mats = cmds.lsThroughFilter( 'DefaultMaterialsAndShaderGlowFilter', na=True, sort='byName', reverse=True )
sgs = cmds.lsThroughFilter('DefaultShadingGroupsFilter', na=True, sort='byName', reverse=True )


## 获取时间滑块的最大最小值
max_time = cmds.playbackOptions(maxTime=True,q=True)
min_time = cmds.playbackOptions(minTime=True,q=True)


## 查询当前场景的引用的资产的路径
```python
for ref_node in cmds.ls(type="reference"):
    try:                                                         
        ref_path = cmds.referenceQuery(ref_node, f=True, un=True)
    except:                                                      
        ref_path = ''                                            
    if ref_path:                                                 
        print(ref_path)
```


## 通过命令得到Maya的一些目录(应用程序目录,脚本目录,布局目录等)
internalVar


## 输出maya自带的所有png图片的名称
for item in cmds.resourceManager(nameFilter="*png"): print(item)
知道了png图片的名字以后就可以通过这两个语句设置控件的图片:
select_file_path_btn = QtWidgets.QPushButton()
select_file_path_btn.setIcon(QtGui.QIcon(':fileOpen.png'))


## 得到当前使用的摄像机名字
cmds.lookThru(q=True)


## 得到当前maya文件使用的声音文件的名字与路径
```python
gPlayBackSlider = mel.eval('$tmpVar=$gPlayBackSlider')
sound_name = cmds.timeControl(gPlayBackSlider, q=True, sound=True) # 声音文件的名字
sound_path = cmds.sound(sound, q=True, file=True) # 声音文件的路径
```


## 得到maya插件的路径
cmds.pluginInfo("mtoa.mll",path=True,q=True)


## 得到userSetup.mel的路径
在mel里面运行 whatIs "userSetup.mel"


## 列出场景中所有的灯光(包括arnold和redshift的灯光)
**defaultNavigation这个命令也可以用来连接节点后面会有举例**
cmds.defaultNavigation(dtv=True,d="defaultLightSet.dagSetMembers")


## 获取灯光链接的信息
```python
all_lighting_list = cmds.defaultNavigation(dtv=True, d="defaultLightSet.dagSetMembers")
cmds.editRenderLayerGlobals(currentRenderLayer='defaultRenderLayer')
link_dic = {}
all_shapes = [s for s in cmds.ls(type='geometryShape', ni=1) if
             not s in all_lighting_list]
use_lighting_list = []
for lgt in all_lighting_list:
    try:
        cmds.referenceQuery(lgt, rfn=True)
    except:
        use_lighting_list.append(lgt)
for lgt in use_lighting_list:
    light_link_shapes = cmds.lightlink(query=True, light=lgt, shp=1, t=0, set=0, h=0)
```


## 得到所有非默认摄像机的摄像机名字
```python
cameras = cmds.ls(type=('camera'), l=True)
startup_cameras = [cam for cam in cameras if cmds.camera(cmds.listRelatives(cam,p=True), startupCamera=True, q=True)]
non_startup_cameras = [cmds.listRelatives(cam,p=True,f=True)[0] for cam in list(set(cameras)-set(startup_cameras))]
```

---
# maya渲染相关设置
## 设置场景的渲染摄像机
```python
cmds.setAttr('perspShape.renderable',0) # 先将原来的渲染摄像机对应属性设置为0
cmds.setAttr('cameraShape1.renderable',1)
```


## 设置场景的渲染分辨率
cmds.setAttr("defaultResolution.width", 1920)
cmds.setAttr("defaultResolution.height", 1080)


## 设置场景的渲染文件输出路径
cmds.setAttr('defaultRenderGlobals.imageFilePrefix')


## 设置redshift的aov
```python
# 删除所有AOVs
all_aovs = cmds.ls(type='RedshiftAOV')
for aov in all_aovs:
    enabled = cmds.getAttr('%s.enabled' % aov)
    if enabled:
        cmds.delete(aov)
# 新增AOV的过程：        
## 新增一个 Beauty 通道 
mel.eval('redshiftCreateAov "Beauty"')
## 刷新Aov显示的列表
mel.eval("redshiftUpdateActiveAovList")
```


## 列举材质编辑器中的节点的所有上游节点
cmds.hyperShade(lun='lambert1')


## 切换渲染层
cmds.editRenderLayerGlobals(currentRenderLayer)
## 得到渲染层下的所有对象
cmds.editRenderLayerMembers(render_layer,q=True,fn=True)
## 得到渲染层的所有渲染属性覆盖
```python
overrides = cmds.listConnections(render_layer + '.adjustments',p=True, c=True)
if overrides:
    attr_value = []
    for i in range(0,len(overrides), 2):
        conn = overrides[i] # returns 'layer.adjustments[#].plug'
        attr_name = overrides[i+1]
        override_index = conn.split(']')[0].split('[')[-1]
        override_value = cmds.getAttr(render_layer + '.adjustments[{}].value'.format(override_index))
        attr_value.append([attr_name,override_value])      
    render_layer_info_dic[render_layer]["attrOverride"] = attr_value
else:
    render_layer_info_dic[render_layer]["attrOverride"] = []
```


## 设置当前渲染器的使用
cmds.setAttr("defalutRenderGlobals.currentRenderer","redshift",typ="string")

---
# Maya的节点操作
## 锁定和解锁节点
lockNode


## 清理场景中未使用的节点
mel.eval('hyperShadePanelMenuCommand("hyperShadePanel1","deleteUnusedNodes");')


## 清理未知节点
```python
unknownNodes = cmds.ls(typ='unknown')
if unknownNodes:
    for node in unknownNodes:
        if cmds.objExists(node):
            lockState = cmds.lockNode(node, q=True, l=True)
            if lockState[0] == 1:
                cmds.lockNode(node, l=False)
            cmds.delete(node)
```

---
# Maya材质编辑器中的相关操作
## 通过命令创建aiStandardSurface材质
```python
import maya.cmds as cmds
aiStandardSurfaceMat = cmds.shadingNode('aiStandardSurface', asShader=True)
aiStandardSurfaceSG  = cmds.sets(renderable=True, noSurfaceShader=True, empty=True, name=aiStandardSurfaceMat + "SG")
cmds.connectAttr(aiStandardSurfaceMat+'.outColor', aiStandardSurfaceSG+'.surfaceShader' )
```


## 通过SG节点的名字找到它对应的材质名字
mat = cmds.listConnections(sg节点的名字 + '.surfaceShader')[0]  


## 通过材质名字找到它上游所有类型为file的节点
fileNodes = [x for x in cmds.hyperShade(lun=材质名字) if cmds.nodeType(x) == 'file'] 


## 让maya判断节点类型并自动进行连接
例如创建两个节点,一个文件节点,一个纹理节点,让它们两个进行连接.以此来复现将图片拖入到材质编辑器的操作.
file_node = cmds.shadingNode("file",asTexture=True,isColorManaged=True)
tex_node = cmds.shadingNode("place2dTexture",asUtility=True)
cmds.defaultNavigation(connectToExisting=True, source=tex_node, destination=file_node)
通过使用这个命令就可以一个命令就将需要连接的属性连好.不需要一个个通过属性名字连接

---
# Maya文件操作
## abc缓存导入导出
AbcImport与AbcExport，这两个命令无法在帮助文档中找到，但是可以在maya脚本编辑器中通过命令中的help方法来得到命令的帮助信息。

---
# Maya模型相关
## 模型细分的命令
这里的smthRes不是细分后的模型名字而是细分的命令节点，mesh_name是要细分的模型:
smthRes = cmds.polySmooth(mesh_name, mth=0, sdt=2, ovb=1, ofb=3, ofc=0, ost=0, ocr=0, dv=1, bnr=1, c=1, kb=1,
ksb=1, khe=0, kt=1, kmb=1, suv=1, peh=0, sl=1, dpe=1, ps=0.1, ro=1, ch=1)[0]

---
# Maya本身的设置
## 接触引用的锁定
mel.eval("referenceEdUnlockCB")


## 无法切换渲染层时使用的命令
mel.eval("fixRenderLayerOutAdjustmentErrors")


## 设置maya的场景单位和轴向
(https://blog.csdn.net/weixin_30908707/article/details/96321064)
cmds.currentUnit( linear='in' )  

---
# 其他代码编写相关
## 通过命令将一连串的命令执行只需要一次ctrl+z就可以全部返回到未进行命令过程的状态
cmds.undoInfo(ock=1, cn='test')
执行的代码
cmds.undoInfo(cck=1, cn='test')


## 解决搜索不到当前文件路径的问题
有时候通过cmds.file(q=True,sn=True)得到的是个空的路径，为了解决这个问题可以通过这个命令替代：
cmds.file(query=True, l=True)[0]
但是这个命令也不是最优解,有遇到一使用这个命令就崩溃的情况所以获取文件路径推荐两个一起用:
```python
current_file_path = cmds.file(q=True,sn=True)
if not current_file_path:
    current_file_path = cmds.file(q=True,l=True)[0]
```

## 确保加载对应的插件的命令
cmds.loadPlugin("animImportExport.mll", qt=True)

---
# Maya界面UI相关命令

## 创建一个显示一段时间后消失的弹窗(方便用于提示信息)
cmds.inViewMessage( amg="不高亮的部分: <hl style='color: red;'>" + "内容内容内容内容内容内容" +  "</hl>.", pos='midCenter', fade=True )

## 通过menuItem的名字找到对应menu
主要方法: cmds.menuItem(_menuItem, query=True,label=True)
也可以直接找menu的名字: cmds.menu(menu_name, query=True,label=True)
```python
def getParentMenu(menuItemName):
    menuBars = cmds.lsUI(menus=True)
    for _menu in menuBars:
        menuItemList = cmds.menu(_menu,query=True,itemArray=True)
        if menuItemList:
            for _menuItem in menuItemList: 
                if menuItemName == cmds.menuItem(_menuItem, query=True,label=True):
                    return _menu
    return None
# 通过Wireframe找到对应menu的名字
shading_menu = getParentMenu("Wireframe")
# 在menu下创建新的menuItem
cmds.menuItem(parent=shading_menu,label='my_menu')  
```

## 创建自定义菜单
```python
if cmds.menu('myMenu', exists=True):
    cmds.deleteUI('myMenu')
my_menu = cmds.menu('myMenu',parent="MayaWindow",tearOff=True,label="MyCustomMenu")
cmds.menuItem(parent=my_menu,subMenu=True,label='menu1')
cmds.menuItem(label='submenu1',command='print("submenu1")')
cmds.menuItem(label='submenu2',command='print("submenu2")')
cmds.menuItem(parent=my_menu,label='menu2')
cmds.menuItem(parent=my_menu,subMenu=True,label='menu3')
cmds.menuItem(label='submenu3',command='print("submenu3")')
```

## 兼容maya低版本和高版本的UI一些设置
```python
if sys.version_info.major < 3:
    maya_main_window = wrapInstance(long(omui.MQtUtil.mainWindow()), QtWidgets.QWidget)
else:
    maya_main_window = wrapInstance(int(omui.MQtUtil.mainWindow()), QtWidgets.QWidget)
```

