---
title: MaxScript
tags: MaxScript
categories: DCC工具开发
abbrlink: a0fded38
date: 2024-01-06 15:43:00
---
# 如何阅读帮助文档
文档地址:https://help.autodesk.com/view/MAXDEV/2024/ENU/?guid=GUID-F039181A-C072-4469-A329-AE60FF7535E7
max的各种object类的描述的地址:https://help.autodesk.com/view/MAXDEV/2024/ENU/?guid=GUID-F159E458-15C2-4CDC-B926-0FB7EFB810DB
文档的描述约定:
![Alt text](image-1.png)
尖括号中的词语是对内容的规则定义
方括号中的内容是可选的
被竖线分割的的内容是在其中选择一个
大括号的内容可以重复零次或多次
大括号+意思是里的内容可以重复一次或多次
::= 可以理解为一个符号,右边描述了左边名称的定义,例如 <digit> ::= 1|2|3|4 意思是 digit可以取1,2,3,4一共四个数

# VScode for MaxScript
1. 搜索Language MaxScript插件并安装
2. 点击下载:[MXSPyCOM](https://github.com/techartorg/MXSPyCOM/releases/download/1.14/MXSPyCOM.zip),[可以参考的GitHub地址](https://github.com/techartorg/MXSPyCOM)
3. 解压文件,将MXSPyCOM.exe放入到"C:\Program Files\MXSPyCOM\MXSPyCOM.exe",将initialize_COM_server.ms放入到"C:\Program Files\Autodesk\3ds Max 2024\scripts\Startup\initialize_COM_server.ms"
4. [进行vscode的配置](https://github.com/techartorg/MXSPyCOM/wiki/Visual-Studio-Code)
配置的关键:
将以下内容放到task里面
```json
{
            "label": "Execute Script in 3ds Max",
            "type": "shell",
            "command": "C:\\Program Files\\MXSPyCOM\\MXSPyCOM.exe",
            "args": [
                "-s",
                "${file}"
            ],
            "presentation": {
                "echo": false,
                "reveal": "never",
                "focus": false,
                "panel": "dedicated"
            },
            "problemMatcher": [],
}
```
然后输入>key进入快捷键绑定
填入内容,将ctrl+e与运行任务进行绑定.
```json
[
    {
        "key": "ctrl+e",
        "command": "workbench.action.tasks.runTask",
        "args": "Execute Script in 3ds max"
    },
]
```
# MaxScript的语法
```
-- 数学表达式
+ - * / ^ as(类型转换)
-- 比较表达式
== != > < >= <=
-- 逻辑表达式
or and not
-- 判断
if ... then ... else ...
if ... do ...
-- case语句 语法一
for obj in geometry do
(
    local d = distance obj $cam1
    case of
    (
        (d <= 50):  obj.segs = 40
        (d <= 120): obj.segs = 25
        (d <= 250): obj.segs = 10
        default:    obj.segs = 5
    )
)
-- case语句 语法二
newObj = case cloneType.state of
         (
            1: instance pickedObj
            2: reference pickedObj
            3: copy pickedObj
         )
-- while 循环
while ... do ...
-- for 循环
写法1,遍历数字: for i = 1 to 10 do print i
写法2,遍历数组: for item in [able] do x = x+item.height
写法3,在for循环里判断然后放到数组中: bigones = for obj in $Box* where obj.height > 100 collect obj

-- continue 同python的continue
-- exit 同python的break
-- try 异常处理
try ... catch ...
```

# MaxScript的UI
## 控件类型与介绍
文档地址:https://help.autodesk.com/view/MAXDEV/2024/ENU/?guid=GUID-E421933F-958E-42FD-80A1-D66F2A2C0A06
参考图片:
![Alt text](image-12.png)

### 各种button的区别:
button:最基础的按钮,有点击事件
checkbutton:点一次和点两次的状态不同
mapbutton:单击按钮时会弹出3dsmax的贴图浏览器对话框
materialbutton:单击按钮时会弹出3dsmax的材质浏览器对话框
pickbutton:单击按钮后进入对象拾取模式,再单击一个场景对象后自动退出拾取模式或右键单击取消拾取模式
button举例:
```
rollout test_buttons "Testing Buttons"
(
    button theButton iconName:@"PolyTools\TransformTools\PB_CW" iconSize:[20,20]
    button theBorderlessButton "I am a button, too!" border:false
    on theButton pressed do
    messagebox "Remember: Never press unknown buttons!"
)
createDialog test_buttons 150 60
```
checkbutton举例:
```
rollout test "Test"
(
checkbutton setup "Setup" checked:true tooltip:"Opens setup panels"
on setup changed state do
if state == on then
    openRollout setup_pan
else
    closeRollout setup_pan
)
```
mapbutton举例:
```
rollout test_mapbutton "Background"
(
    label sbm_lbl "Background Map:"
    mapbutton choosemap "<<none>>" tooltip:"Select Background Map" width:120
    on choosemap picked texmap do
    (
    environmentmap = texmap
    choosemap.text=classof texmap as string
    )
)
createDialog test_mapbutton
```
materialbutton举例:
```
Rollout assign_material "Assign Material"
(
    label smtl_lbl "Set selected object's material to:"
    materialbutton choosemtl "Pick Material"
    on choosemtl picked mtl do
    (
    print mtl
    if $ != undefined do $.material=mtl
    )
)
createDialog assign_material
```
pcikbutton举例:
```
rollout pick_box_test "Pick Box Test"
(
--filter all objects of class Box:
fn box_filt obj = classof obj == Box
--Pickbutton to select a Box from the scene
pickbutton chooseit "Select Box" width:140 filter:box_filt
--If the user picked an object, then
on chooseit picked obj do
(
--see if the user did not cancel the picking...
if obj != undefined do
(
--if he did not, make the box's wireframe red:
obj.wirecolor = red
--and display the name of the object on the button:
chooseit.text = obj.name
)
)--end on
)--end rollout
createDialog pick_box_test
```
# 让max启动时就执行对应的脚本
参考官方文档:https://help.autodesk.com/view/MAXDEV/2024/ENU/?guid=GUID-615D14FB-0F2D-4801-B381-1128C4128C70
## 使用startup.ms文件
通过文档可知MAXScript首先按列出的顺序在以下目录中搜索名为startup.ms 的文件然后运行:用户脚本目录,用户启动脚本目录,3ds Max 系统脚本目录,3ds Max 系统启动脚本目录.
用户脚本、系统脚本、用户启动脚本和系统启动脚本分别对应于 #userscripts 、 #systemscripts 、 #userstartupscripts 和 #startupScripts 的位置。
可以通过命令:GetDir <文件类型名字>来获取路径
举例:GetDir #startupScripts
返回:C:\Program Files\Autodesk\3ds Max 2024\scripts\startup
## 使用命令行启动max,并伴随对应脚本文件
```shell
# 首先先cd到对应的max目录中
cd C:\Program Files\Autodesk\3ds Max 2024
# 参考以下命令打开对应max文件并启动对应脚本
3dsmax.exe E:\3dsmaxTest\a.max -U MAXScript D:\MaxScript\TestMaxScript.ms
```

# 使用MaxScript处理数据
## 字符串
### 分割字符串
filterString \<string> \<token_string> 
**注意:** token_string,也就是第二个的字符串中的每个字符都会被识别为分割
点,因此第二个字符串建议只有单字符
```
filterString "MAX Script, is-dead-funky" ", -"  -- 返回#("MAX", "Script", "is", "dead", "funky")
filterString "MAX Script, is-dead-funky" "-"    -- 返回#("MAX Script, is", "dead", "funky")
```
### 替换字符串
replace \<string> \<from_integer> \<length_integer> \<new_string>
```
s = "1234567890"
s1=replace s 5 3 "inserted string" --返回"1234inserted string890"
```
### 字符串的切片
substring \<string> \<from_integer> \<length_integer>
```
s = "Balerofon"
ss = substring s 5 3 --返回"rof"
ss = substring s 5 -1 --返回"rofon"
ss = substring s 5 100 --返回"rofon" 
```
### 查询字符串
matchPattern \<string> pattern:\<pattern_string> [ ignoreCase:\<boolean> ] 
如果字符串\<string>与通配符 pattern:匹配，返回 True，否则返回 False。如果没有指定
参数 ignoreCase:False，比较是大小写不敏感的。
```
s = "text1"
matchPattern s pattern : "text?" --返回 True
matchPattern s pattern : "T*" --返回 True
matchPattern s pattern : "T*" ignoreCase:False --返回 False
matchPattern s pattern : "s*" --返回 False
```

## Point3矢量
Point3 类定义了三维空间的点，也称为三维矢量，包含三个 Float 类数。
[320,240] -- 定义2维点
[10,20,30] -- 定义3维点
有x,y,z三个属性来代表xyz坐标
```
-- 定义两个point3类型的对象
vector1 = [10,20,30]
vector2 = [20,30,40]
-- 返回矢量的长度
length vector1
-- 返回两个矢量的点积
dot vector1 vector2
-- 返回两个矢量的叉积
cross vector1 vector2
-- 返回矢量的标准矢量
normalize vector1
-- 返回指定两点之间的距离
distance vector1 vector2
-- 返回指定两点之间的随机点
random vector1 vector2
```
## Array 数组
定义数组的语法是: \#(数组内容)
用户可以将一个对象集和通配符路径名用 as 操作符转化为一个数组。这相当于给对象集或与路径名匹配的当前对象拍了一张“快照”，这样可以在随后的脚本里操作集合里的对象，而不用担心对象集改变。这种功能与 3ds max 用户界面下的 Named Selection Sets 按钮类似。如果用户删除了数组里的某一对象，而在随后的脚本里再对数组进行映射操作，系统会给出一个错误信息。
例子：
sel1 = Selection as array
Boxes_at_load = \$Box* as array
snap_children = \$torso...* as array
original_cameras = cameras as array 

### 数组的方法
1. append\<array>\<value>
将指定值插入到数组的最后
2. deleteItem\<array>\<number>
从数组里删除指定序号的元素
3. join\<array>\<collection>
将变量\<collection>里的所有元素添加到数组\<array>的后面
4. sort\<array>
按升序对数组进行排序.所有数组的元素必须具有可比性
5. findItem\<array>\<value>
在数组里查找指定目标对象,返回第一次找到的元素序号,如果没有找到就返回0,Point3类值与String类值如果内容相同,系统也认为欸它们是匹配的.
6. insertItem\<value>\<array>\<integer>
在数组的指定位置\<integer>插入指定值\<value>
7. amin(\<array>|{value})
返回数组或指定值序列里的最小值.如果数组长度为0或没有指定值序列,返回值undefined
8. amax(\<array>|{value})
返回数组或指定值序列里的最大值.如果数组长度为0或没有指定值序列,返回值undefined
# 批量生成球
![Alt text](image.png)
```MAXScript
-- UI的定义
rollout SphereTool "Spheres Creator"
(
    -- 创建UI
    spinner count "Number: " type:#integer range:[1,100,10]
    spinner growth "Radius growth: " range:[1,100,10]
    button create "Create Spheres"
    -- UI事件
    on create pressed do
        for i in 1 to count.value do
            sphere radius:(i*growth.value) position:[i^2*growth.value,0,0]
)
-- 创建对应UI窗口
createDialog SphereTool width:200

```
# 函数的写法
## 一般函数(生成一排球体)
参数:count growth
作用:生成一排球体
```
-- 函数的定义
function createSphere count growth =
(
	for i in 1 to count do 
		sphere radius:(i*growth) position:[i^2*growth,0,0]
)
-- 函数的调用
createSphere 25 10
```
## 带默认值的函数(渲染场景内所有摄像机)
参数:label,size,frames,folder.  其中size与folder有默认值,frames意思是可选的,可以传参数也可以不传,不传时为unsupplied
作用:寻找场景内所有摄像机并进行渲染
```
-- 函数的定义
function snapCams label size:[320,240] frames: folder:"C:/testimages/" = 
(
    for c in cameras do 
    (
        local fname = folder + label + "-" + c.name
        if frames == unsupplied then
            render camera:c outputFile:(fname+".jpg") outputSize:size
        else   
            render camera:c frameRange:frames \
                   outputFile:(fname+".avi") outputSize:size
    )
)
-- 函数的调用
snapCams "phase1" size:[640,480]
```

## 有返回值的函数(创建材质的函数)
参数:baseColor cellSize
作用:通过函数创建材质并返回
这里函数调用是给模型Box001和Box002赋予材质
```
-- 函数的定义
function cellMaterial baseColor cellSize = 
(
    local mtl = standardMaterial specularLevel:55 glossiness:35,
          map = cellular cellColor:baseColor size:cellSize fractal:on
    mtl.diffusemAP = map
    return mtl
)
-- 函数调用
$Box001.material = cellMaterial red 25
$Box002.material = cellMaterial blue 50

```

## 递归
这里举例是找名字叫Box001的模型,自动赋予材质,然后会找Box001的子模型并赋予材质(材质的参数也会自动发生变化)
```
-- 上一标题的函数的定义
function cellMaterial baseColor cellSize = 
(
    local mtl = standardMaterial specularLevel:55 glossiness:35,
          map = cellular cellColor:baseColor size:cellSize fractal:on
    mtl.diffusemAP = map
    return mtl
)
-- 函数的定义(写function和fn都可以,一样的效果)
fn mtlToChildren obj cellColor cellSize = 
(
    -- 设置材质给obj
    obj.material = cellMaterial cellColor cellSize
    -- 循环遍历子obj
    for child in obj.children do
        mtlToChildren child (cellColor + [75,0,0]) (cellSize - 3)
)
-- 函数调用
mtlToChildren $Box001 blue 10
```

# 得到变量的类型
```
classOf 23 -- Integer
classOf "foo" -- String
classOf &ball  -- &phere
```
# 得到相关类名称与方法
MAXWrapper是max的所有object的父类(maxscript里称为超类)
```
showClass "sphere" -- 显示sphere开头的类
showClass "sphere*.*" -- 显示sphere开头的类以及对应的方法

-- 通过对象或路径名得到其所具有的方法
b = box()
showproperties b
showproperties $Box001

```
# 集合和数组
数组的下标是从1开始的,不是0
集合是没有重复元素的,集合是无序的
定义数组: a = #(1,3,5,7,9)
定义集合: a = #{1,2,3,4,5}
修改数组的第三个数的值: a[3] = five
向数组追加内容: append a 11   输出的数值:1,3,,5,7,9,11
通过表达式创建数组: 
遍历1到5,然后对其进行开平方并存入roots的数组中.
roots = for i in 1 to 5 collect sqrt i
遍历的同时进行判断:
smallSpheres = for obj in geometry
    where classOf obj == sphere and obj.numFaces < 50
    collect obj
# 生成排列好的球体(增强版)
界面:
![Alt text](image-2.png)
可以随时通过UI数值的调整来实时改变球体的数量和大小
```maxScript
rollout SphereTool3 "Spheres Creator 3"
(
    local spheres = #()
    spinner count "Number: " type:#integer range:[1,100,10]
    spinner growth "Radius growth :" range:[1,100,10]
    button create "Create Spheres"
    button del "Delete Spheres"
    on create pressed do
        spheres = for i in 1 to count.value collect
            sphere radius:(i*growth.value) position:[i^2*growth.value,0,0]
    on del pressed do delete spheres

    on growth changed val do
        for i in 1 to spheres.count do
        (
            spheres[i].radius = i * val
            spheres[i].pos = [i ^ 2 * val, 0, 0]
        )

    on count changed val do
    (
        delete spheres
        create.pressed()
    )
)
create dialog SphereTool3 width: 300
```

# 类集合数据类型
## 对象集合
这些对象集合是动态刷新的
geometry 指定类型的3dsmax对象
lights
cameras
helpers
shapes
systems
spacewarps
objects 所有场景对象
selection 获得当前选择的对象并保存为数组

相关方法:
1. clearSelection() 清除当前场景对象选择集
2. deselect \<PathName> 将指定对象从当前选择集里去掉
3. select \<PathName> 先解除所有当前选择集,然后选择指定的对象
4. selectMore \<PathName> 将指定对象集添加到当前选择集
5. getCurrentSelection() 返回一个数组，表示当前选择集。本函数相当于函数 Selection as array，但如果场景里有大量的对象，本函数的执行速度会大大快于后者。

基础对象集合的使用举例
举例1:
删除距离原点距离大于10000的几何体,使用 as array的作用是防止geometry发生改变而造成的影响
for o in geometry as array where (distance o.pos [0,0,0]) > 10000 do delete o
举例2:
![Alt text](image-4.png)
举例3:
![Alt text](image-5.png)


## Pathname
模型可能有层级关系,因此可以用Pathname的方式来得到对应的模型
也可以通过类似正则表达式的方式来得到相关模型
 select $Box002/Box003
 select $Box*
 select $Box001/Box002/*  (注意这个的*号是只针对Box002的子集这个层级)
 select $Box001/.../Sphere* 通过"..."让*号不止局限于固定的层级

 select $Box00? 



# 动画脚本
开启自动k帧模式然后在0和100帧处k帧并设定名字叫Sphere001的模型的位置
```
-- 在界面中显示当前max模式为自动k帧模式
max tool animmode
-- 开启自动k帧 加set的作用是让自动k帧持续开启
set animate on
-- 进行脚本k帧
animation on
(
    at time 0 $Sphere001.pos = [-100,0,0]
    at time 100 $Sphere001.pos = [100,0,0]
)
```
制作一个动画,在名字叫做ball的模型位置处创建一个小球,然后0~100帧中每5帧在ball的模型位置处的16个距离单位下k一帧,然后将ball的半径进行sin趋势的改变
```
b2 = sphere radius:3 wireColor:red
animate on for t in 0 to 100 by 5 do
    at time t
    (
        b2.pos = $ball.pos + random [-16,-16,-16] [16,16,16]
        $ball.radius = 8+4*sin(720*t/100)
    )
```
得到10帧和50帧ball名称的模型的位置并计算之间距离
![Alt text](image-3.png)
其他时间的写法
![Alt text](image-6.png)
遍历时间
![Alt text](image-7.png)
通过脚本制作,一个box在两个线之间移动的动画
![Alt text](image-8.png)
box的长度和方向会跟着线的距离来变化.
```
fn railFollow obj line1 line2 u =
(
	-- u的值代表了从起始点到结束点的值,范围是从0到1,计算方式是(t-start) as float/(end-start) as float
	-- 计算位置,方向,距离
	-- 通过lengthInterp可以得到在线的u的数值下的点位置
	-- 通过nearestPathParam可以得到在线上,离p1点位置最近的点的位置的u值
	-- 通过pathInterp可以得到在线上的u的数值下点的位置
	-- p1-p2得到p1到p2向量
	local p1 = lengthInterp line1 u,
	u2 = nearestPathParam line2 p1,
	p2 = pathInterp line2 u2,
	dv = p2 - p1,
	d = distance p1 p2
	
	obj.pos = p1
	obj.dir = dv
	obj.height = d
)

start = animationRange.start
end = animationRange.end
animate on
	for t in start to end by 2 do
	(
		local u = (t - start) as float / (end - start) as float
		at time t railFollow $Box001 $Line001 $Line002 u
	)
```
# 控制器的使用
将box01的高度控制器赋予c
c = $box01.height.controller
创建一个路径约束控制器
pc = path_constraint follow:true bank:true path:$line01
创建一个路径约束控制器并赋予一个box的位置参数
$Box001.pos.controller = path_constraint follow:true bank:true path:$Line001
调整控制器的属性参数
$box01.pos.controller.bankAmount -= 0.25
复制控制器.
因为maxscript的变量赋值是引用赋值,所以第一句两个控制器变量是同一个值
使用copy语句以后会创建右边变量的一个副本来赋予左边
$box01.scale.controller = $box02.scale.controller
$sphere01.radius.controller = copy $box01.height.controller
得到控制器上的keys,返回一个数组
keys = $box02.height.controller.keys
得到keys后对应的可以使用的方法
keys = $box02.height.controller.keys
keys[1].value = 23
for k in keys do fomat "% at %\n" k.value k.time
# 通过读取数据文件,设置摄像机在对应key下的位置
数据文件:
![Alt text](image-9.png)
```
function stepCam cam dataFile = 
(
    -- 判断摄像机是否有bezier_position控制器,如果有就删掉重新建,否则就直接建
    if claasoOf cam.pos.controller != bezier_position then
        cam.pos.controller = bezier_position()
    else
        deleteKeys cam.pos.controller
    if classOf cam.target.pos.controller != bezier_position then
        cam.target.pos.controller = bezier_postion()
    else
        deleteKeys cam.target.pos.controller
    -- 得到摄像机的控制器
    local cc = cam.pos.controller,
          tc = cam.target.pos.controller
    -- 得到文件
    local f = openFile dataFile,
          curFrame = 0
    -- 读取文件并设置
    -- eof 是 MaxScript 中的一个函数，用于检查文件是否已经到达末尾
    while not eof f do
    (
        -- 读取文件三个参数
        local camPos = readValue f,
              targPos = readValue f,
              frames = readValue f
        -- 为摄像机的控制器在当前帧进行k帧
        local ck = addNewKey cc curFrame,
              tk = addNewKey tc curFrame
        -- 设置帧的数值还有切线类型为#step
        ck.value = camPos; ck.inTangentType = #step
        tk.value = targPos;  tk.inTangentType = #step
        -- 设置下一个要设置的关键帧
        curFrame += frames
    )
    close f
)
```

# 修改器的应用
```
-- 创建修改器
b = bend angle:45 direction:90
-- 将修改器添加到模型上
addModifier $box01 b
-- 创建修改器并添加到模型上
addModifier $box01 (twist angle:90)
-- 访问模型上的修改器(假如box01模型上有bend,twist)
$box01.bend
$box01.twist
-- 修改模型上的修改器的数值
$box01.bend.angle += 20
-- 得到模型上的所有修改器
$box01.modifiers
```

# MaxScript中的循环
## while ... do ...
```
-- 定义一个获取路径名称的函数
fn get_pathname obj =
(
    -- 一直循环找物体的parent,然后设置路径名,当parent为undefined时终止循环
    local pathname = obj.name
    while obj.parent != undefined do
    (
        obj = obj.parent
        pathname = obj.name + "/" + pathname
    )
    "&" + pathname
)
-- 对当前选择的物体进行获取路径名
get_pathname $
```
## continue命令
```
for obj in selection do
(
    -- 通过isKindOf 判断obj是否是Editable_Mesh类或其子类
    if not isKindOf obj Editable_Mesh then
    (
        local msg = "Selected object \"" + obj.name + "\" is not a mesh. \nObject skipped."
        -- 显示信息弹窗
        messageBox msg
        continue
    )
    totalObjects += 1
    totalFaces += obj.numFaces
    totalVerts += obj.numVerts
)
```

## exit命令
在循环中通过exit命令退出循环,类似于python的break
![Alt text](image-10.png)

## return命令
函数中的循环中使用return命令也可以跳出循环
![Alt text](image-11.png)

# coordsys控制坐标空间
## 坐标空间的种类
```
coordsys word          -- 世界空间
coordsys local         -- 局部空间
coordsys parent        -- 父对象空间,如果没有父对象则是世界空间
coordsys grid          -- 激活的网格的坐标空间
coordsys screen        -- 当前激活的视图的坐标空间
coordsys <node>        -- 对应node的局部的坐标空间
coordsys <matrix3>     -- 基于给定的矩阵来当坐标空间
``` 
## coordsys的使用参考
```
coordsys local
(
    move $box3 [100,0,0]
    rotate $box4 45 z_axis
)
```

# 制作选取线然后生成锁链的工具
![Alt text](image-13.png)
```
rollout ChainMaker "Chain Maker"
(
    local curve,
          chain = #()
    -- 定义一个负责筛选物体是否是shape的函数来辅助Pickbutton判断
    fn shapesOnly obj = isKindOf obj Shape
    group "Controlling Shape"
    (
        pickbutton pickCurve "Pick Curve" width:100 filter:shapesOnly
        label theCurve "-- none --"
    )
     
    group "Chain Parameters"
    (
        -- diam负责控制锁链的大小
        -- thickness负责控制锁链的宽厚
        spinner diam "Link Diameter: " range:[1,500,12]
        spinner thickness "Link Thickness:" range:[0.1,500,2]
        colorPicker wireColor "Wire Color:" align:#center
    )

    button deleteChain "Delete Chain" width:100 enable:false
    -- 负责生成锁链
    fn updateChain = 
    (
        local len = curvelength curve, -- 曲线的长度
              uStep = (diam.value - thickness.value) / len, -- 环的直径减去厚度等于内圈的直径,再除以曲线的长度可以得到一个圆环占曲线长度的比例
              up = true,
              i  = 1
        for u = 0.0 to 1.0 by uStep do
        (
            if i > chain.count then chain[i] = torus wireColor:wireColor.color
            local t = chain[i]
            t.radius1 = diam.value / 2  
            t.radius2 = thickness.value / 2
            t.pos = lengthInterp curve u
            t.dir = lengthTangent curve u
            -- 方向一次x,一次y
            coordsys local rotate t 90 (if up then y_axis else x_axis)
            up = not up 
            i += 1
        )
        for j in i to chain.count do
        (
            delete chain[i]
            deleteItem chain i
        )
    )

    on pickCurve picked obj do
    (
        curve = obj
        theCurve.text = obj.name
        deleteChain.enabled = true
        updateChain()
    )

    on deleteChain pressed do (delete chain; chain = #())
    on diam changed val do updateChain()
    on thickness changed val do updateChain()
    on wireColor changed val do chain.wireColor = val
)

createDialog ChainMaker width:180
```

# 把脚本放到菜单栏中
例如把刚才做的ChainMaker放到菜单栏中
前提已知:做好了一个脚本,脚本中的布局的变量名字叫ChainMaker,脚本另存到了3dmax的根目录的scripts文件夹中
创建macroScript:
```
macroScript ChainMakerMacro
	category:"My Tools"
	buttonText:"Chain Maker"
	toolTip:"根据曲线创建锁链的工具"
(
	global ChainMaker
	if ChainMaker == undefined or not ChainMaker.open do
		fileIn "ChainMaker.ms"
)
```
创建自定义菜单:
![Alt text](image-14.png)

# 导出模型信息举例
```
function exportMesh obj fileName origin=
(
    local file = createfile fileName ,
          vertStore = #(),
          numFrames = (animationRange.end - animationRange.start).frame as integer
          
    format "%, numVerts = %, numFrames = %\n\n" obj.name obj.numVerts numFrames to:file
    format "Frame,Vert #, Delta\n" to:file

    for f = animationRange.start to animationRange.end do
    (
    sliderTime = f
    for i in 1 to obj.numVerts do
    (
        local v = coordsys origin getVert obj i
        local dv = if vertStore[i] == undefined then v else v - vertStore[i]
        vertStore[i] = v
        format "%, %, %\n" (f.frame as integer) (i-1) dv to:file
    )
    )
    close file
    edit fileName  
)
exportMesh $Sphere001 "E:/3dsmaxTest/test.txt" $Sphere001
```

# 批量渲染对应文件夹下的max文件然后输出图片
![Alt text](image-15.png)
```
function thumbNailFolder inFolder outFolder thumbType:".jpg" thumbSize:[320,240] =
(
    makeDir outFolder
    local maxFilePattern = inFolder + "\\*.max"
    -- 遍历对应文件夹下的所有max文件
    for filePath in getFiles maxFilePattern do
    (
        local fileName = getFileNameFile filePath,
              thumbPath = outFolder + "\\" + fileName + thumbType
        
              format "Rendering thumbnail for %\n" filePath
              -- 进入max文件进行渲染,并设置输出路径和输出大小,vfb为off则渲染完不自动打开图像窗口
              loadMaxFile filePath
              render outputFile:thumbPath outputSize:thumbSize vfb:off
    )
    resetMaxFile #noPrompt
    print("Done.")
)

thumbNailFolder "E:/3dsmaxTest" "E:/3dsmaxTest"
```

# 沿着曲线种树的脚本
前提:需要有名字叫road的曲线,有一个叫ground的地面模型,有一个叫masterTree的树的模型
![Alt text](image-16.png)
```
numTrees = 500
for i in 1 to numTrees do
(
    local u = random 0.0 1.0,
          pos = lengthInterp $road u,
          tan = lengthTangent $road u

    local offset = random 5 18 * (if i < numTrees / 2 then 1 else -1),
          -- cross tan z_axis得到切线与z轴的叉积,然后再乘以偏移值,最终得到偏移的向量
          offsetVec = cross tan z_axis * offset,
          -- 当前位置加上偏移的向量等于偏移的位置
          offsetPos = pos + offsetVec,
          -- 以当前偏移的位置的z轴1000的位置处向正下方0,0,-1处生成射线
          treeRay = ray [offsetPos.x, offsetPos.y, 1000] [0,0,-1]

    -- 定义树的位置和大小,intersectRay $ground treeRay得到的是模型与射线相交地方的法向量,因此再加个.pos得到位置
    local treePos = (intersectRay $ground treeRay).pos,
          treeScale = [1,1,1] * random 0.2 1.1
    
    -- 创建masterTree这个模型的实例
    instance $masterTree pos:treePos scale:treeScale name:"tree"

    -- 更新max的视图,来观察到脚本执行时的状态
    if mod i 10 == 0 then redrawViews()
)
```

# 实现进度条功能
```
-- 进度条的名字
progressStart "test"
-- 进度条处理的任务总数
loop_count = 500
for i in 1 to loop_count do 
(
	if getProgressCancel() 
	then 
	(
		progressEnd()
		exit
	)
	else
	(	
		-- 这里填写要做的事情
		print(i)
		-- 更新进度条
		percent = i*100/loop_count 
		progressUpdate percent
	)
	if percent==100 do progressEnd()
)	
```