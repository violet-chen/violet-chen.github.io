---
title: 油管与B站uepython教程
tags: UEPython
categories: UE开发
abbrlink: ddc00d0e
date: 2023-08-29 03:57:00
---
<meta name="referrer" content="no-referrer" />
<a name="g4ESd"></a>

# 油管uepython教程
<a name="tlpxM"></a>
## 在UE中的python初始配置
可以看看这个文章[https://www.yumefx.com/?p=3211](https://www.yumefx.com/?p=3211)
<a name="WYDR1"></a>
### 插件的选择
找到scripting启用这三个<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1655819812634-a0e15b6f-5e64-459a-97f8-4c12f0c1895d.png#clientId=u0d521281-290c-4&errorMessage=unknown%20error&from=paste&height=851&id=uaec1a435&originHeight=851&originWidth=1458&originalType=binary&ratio=1&rotation=0&showTitle=false&size=151187&status=error&style=none&taskId=ubfd903d6-416e-4774-b8c2-3022ffcc8fc&title=&width=1458)
<a name="pu3hS"></a>
### 项目设置
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1655978185249-1579d6af-b989-4157-b733-991feb125622.png#clientId=ue8ca9c13-c3c0-4&errorMessage=unknown%20error&from=paste&height=346&id=u733583c2&originHeight=346&originWidth=1177&originalType=binary&ratio=1&rotation=0&showTitle=false&size=26571&status=error&style=none&taskId=u9c8861d7-0598-4631-a733-6d30d9a2c14&title=&width=1177)<br />第一个 startup scripts 中填写的是，当启动UE时自动加载的脚本的路径<br />第二个Additional paths 中填写的是 当在UE中使用import模块时 import的额外搜索路径
<a name="Ouc7j"></a>
## 使用python导入资产
<a name="R7ckW"></a>
### 导入贴图和音频
用到的类：<br />[https://docs.unrealengine.com/5.0/en-US/PythonAPI/class/AssetImportTask.html](https://docs.unrealengine.com/5.0/en-US/PythonAPI/class/AssetImportTask.html)<br />[https://docs.unrealengine.com/5.0/en-US/PythonAPI/class/AssetTools.html](https://docs.unrealengine.com/5.0/en-US/PythonAPI/class/AssetTools.html)<br />首先先了解一下引擎中的文件路径：这里内容的路径为/Game,因此假如要在内容下创建一个新的Tex文件夹，那么Tex文件夹的路径就是/Game/Tex<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1657100608789-ceeb2279-1791-464f-b2fc-99e3b59453bc.png#clientId=ua4789b34-f786-4&errorMessage=unknown%20error&from=paste&height=58&id=u5e6699ed&originHeight=58&originWidth=133&originalType=binary&ratio=1&rotation=0&showTitle=false&size=3362&status=error&style=none&taskId=u2552f489-6209-44c2-8324-2c59e6fe67b&title=&width=133)<br />在ue的编辑界面中按shitf+回车可以输入多行代码
```python
import unreal

soundPath = 'D:/ZhangRuiChen/UETest/TestFile/Sounds/soundTest.mp3'
texPath = 'D:/ZhangRuiChen/UETest/TestFile/Texture/test_ORM3.png'


def importMyAssets():  # 创建导入任务并执行导入
    texture_task = buildImportTask(texPath, '/Game/Textures')  # 通过buildImportTask函数创建一个AssetImportTask对象
    sound_task = buildImportTask(soundPath, '/Game/Sounds')  # 同理
    executeImportTasks([texture_task, sound_task])  # 执行导入操作


# 这里用到的属性可以参考文档：
def buildImportTask(filename, destination_path):  # 构建导入任务
    task = unreal.AssetImportTask()
    task.set_editor_property('automated', True)  # 设置为True后就不会弹出对话框，就是将其设置为自动化
    task.set_editor_property('destination_name', '')  # 可选的要导入的自定义名称，当属性为空时就按照文件名称命名
    task.set_editor_property('destination_path', destination_path)  # 导入的资源在引擎中的路径
    task.set_editor_property('filename', filename)  # 要导入的资源在电脑磁盘上的路径
    task.set_editor_property('replace_existing', True)  # 是否要覆盖资产
    task.set_editor_property('save', True)  # 导入后保存
    return task


# 这里用到的属性可以参考文档：https://docs.unrealengine.com/5.0/en-US/PythonAPI/class/AssetTools.html
def executeImportTasks(tasks):  # 执行导入任务
    unreal.AssetToolsHelpers.get_asset_tools().import_asset_tasks(tasks)  # 通过这行代码将在buildImportTask函数中创建的task对象进行导入
    for task in tasks:
        for path in task.get_editor_property('imported_object_paths'):
            print('Imported: %s' % path)

```
<a name="m5PmG"></a>
### 导入静态网格体和骨骼网格体
用到的类：<br />[https://docs.unrealengine.com/5.0/en-US/PythonAPI/class/FbxImportUI.html](https://docs.unrealengine.com/5.0/en-US/PythonAPI/class/FbxImportUI.html)<br />[https://docs.unrealengine.com/5.0/en-US/PythonAPI/class/FbxMeshImportData.html](https://docs.unrealengine.com/5.0/en-US/PythonAPI/class/FbxMeshImportData.html)<br />[https://docs.unrealengine.com/5.0/en-US/PythonAPI/class/FbxStaticMeshImportData.html](https://docs.unrealengine.com/5.0/en-US/PythonAPI/class/FbxStaticMeshImportData.html)<br />[https://docs.unrealengine.com/5.0/en-US/PythonAPI/class/FbxSkeletalMeshImportData.html](https://docs.unrealengine.com/5.0/en-US/PythonAPI/class/FbxSkeletalMeshImportData.html)<br />我用的4.26版本的UE，使用这个代码没有办法导入骨骼体，代码已经反复检查几遍了没发现问题。教程中用的是4.21版本的UE。  后来测试后发现是可以的，应该是之前的资产有问题，后来测试用的小白人fbx2018的是可以导入进来的。
```python
import unreal

soundPath = 'D:/ZhangRuiChen/UETest/TestFile/Sounds/soundTest.mp3'
texPath = 'D:/ZhangRuiChen/UETest/TestFile/Texture/test_ORM3.png'
static_mesh_fbx = 'D:/ZhangRuiChen/UETest/TestFile/StaticMeshes/sphere.fbx'
skeletal_mesh_fbx = 'D:/ZhangRuiChen/UETest/TestFile/Skeletal/woman.fbx'

def importMyAssets():  # 创建导入任务并执行导入
    # texture_task = buildImportTask(texPath, '/Game/Textures')  # 通过buildImportTask函数创建一个AssetImportTask对象
    # sound_task = buildImportTask(soundPath, '/Game/Sounds')  # 同理
    # executeImportTasks([texture_task, sound_task])  # 执行导入操作
    static_mesh_task = buildImportTask(static_mesh_fbx, '/Game/StaticMeshes', buildStaticMeshImportOptions())
    skeletal_mesh_task = buildImportTask(skeletal_mesh_fbx, '/Game/SkeletalMeshes', buildSkeletalMeshImportOptions())
    executeImportTasks([static_mesh_task, skeletal_mesh_task])


# 这里用到的属性可以参考文档：https://docs.unrealengine.com/5.0/en-US/PythonAPI/class/AssetImportTask.html
def buildImportTask(filename, destination_path, options=None):  # 构建导入任务
    task = unreal.AssetImportTask()
    task.set_editor_property('automated', True)  # 设置为True后就不会弹出对话框，就是将其设置为自动化
    task.set_editor_property('destination_name', '')  # 可选的要导入的自定义名称，当属性为空时就按照文件名称命名
    task.set_editor_property('destination_path', destination_path)  # 导入的资源在引擎中的路径
    task.set_editor_property('filename', filename)  # 要导入的资源在电脑磁盘上的路径
    task.set_editor_property('replace_existing', True)  # 是否要覆盖资产
    task.set_editor_property('save', True)  # 导入后保存
    task.set_editor_property('options', options)  # 当导入fbx这种资产需要额外的导入选项，需要创建FbxImportUI对象来传递
    return task


# 这里用到的属性可以参考文档：https://docs.unrealengine.com/5.0/en-US/PythonAPI/class/AssetTools.html
def executeImportTasks(tasks):  # 执行导入任务
    unreal.AssetToolsHelpers.get_asset_tools().import_asset_tasks(tasks)  # 通过这行代码将在buildImportTask函数中创建的task对象进行导入
    for task in tasks:
        for path in task.get_editor_property('imported_object_paths'):
            print('Imported: %s' % path)


def buildStaticMeshImportOptions():
    options = unreal.FbxImportUI()
    # unreal.FbxImportUI
    options.set_editor_property('import_mesh', True)
    options.set_editor_property('import_textures', False)
    options.set_editor_property('import_materials', False)
    options.set_editor_property('import_as_skeletal', False)  # Static Mesh
    # unreal.FbxMeshImportData
    options.static_mesh_import_data.set_editor_property('import_translation', unreal.Vector(0.0, 0.0, 0.0))
    options.static_mesh_import_data.set_editor_property('import_rotation', unreal.Rotator(0.0, 0.0, 0.0))
    options.static_mesh_import_data.set_editor_property('import_uniform_scale', 1.0)
    # unreal.FbxStaticMeshImportData
    options.static_mesh_import_data.set_editor_property('combine_meshes', True)
    options.static_mesh_import_data.set_editor_property('generate_lightmap_u_vs', True)
    options.static_mesh_import_data.set_editor_property('auto_generate_collision', True)
    return options


def buildSkeletalMeshImportOptions():
    options = unreal.FbxImportUI()
    # unreal.FbxImportUI
    options.set_editor_property('import_mesh', True)
    options.set_editor_property('import_textures', True)
    options.set_editor_property('import_materials', True)
    options.set_editor_property('import_as_skeletal', True)  # Skeletal Mesh
    # unreal.FbxMeshImportData
    options.skeletal_mesh_import_data.set_editor_property('import_translation', unreal.Vector(0.0, 0.0, 0.0))
    options.skeletal_mesh_import_data.set_editor_property('import_rotation', unreal.Rotator(0.0, 0.0, 0.0))
    options.skeletal_mesh_import_data.set_editor_property('import_uniform_scale', 1.0)
    # unreal.FbxSkeletalMeshImportData
    options.skeletal_mesh_import_data.set_editor_property('import_morph_targets', True)
    options.skeletal_mesh_import_data.set_editor_property('update_skeleton_reference_pose', False)
    return options

```
<a name="VWzOM"></a>
### 导入动画
跟导入静态网格体差不多，就是导入动画时的额外设置略有不同，并且创建任务需要使用导入动画的设置时需要指定动画依赖的骨骼的路径。
```python


def buildAnimationImportOptions(skeleton_path):
    options = unreal.FbxImportUI()

    # 是否导入动画
    options.set_editor_property('import_animations', True)
    # 导入骨架的位置
    options.skeleton = unreal.load_asset(skeleton_path)

    # 设置动画序列的内容
    options.anim_sequence_import_data.set_editor_property('import_translation', unreal.Vector(0.0, 0.0, 0.0))
    options.anim_sequence_import_data.set_editor_property('import_rotation', unreal.Rotator(0.0, 0.0, 0.0))
    options.anim_sequence_import_data.set_editor_property('import_uniform_scale', 1.0)

    # 动画的长度
    options.anim_sequence_import_data.set_editor_property('animation_length',
                                                          unreal.FBXAnimationLengthImportType.FBXALIT_EXPORTED_TIME)
    # 去掉冗余的关键帧
    options.anim_sequence_import_data.set_editor_property('remove_redundant_keys', False)
    return options
    
def executeImportTasks(tasks):  # 执行导入任务
    unreal.AssetToolsHelpers.get_asset_tools().import_asset_tasks(tasks)  # 通过这行代码将在buildImportTask函数中创建的task对象进行导入
    for task in tasks:
        for path in task.get_editor_property('imported_object_paths'):
            print('Imported: %s' % path)
            
def importMyAssets():  # 创建导入任务并执行导入
    animation_fbx = 'D:/ZhangRuiChen/UETest/TestFile/Animation/Animation.fbx'
    animation_fbx_task = buildImportTask(animation_fbx, '/Game/Animations', buildStaticMeshImportOptions('/Game/SkeletalMeshes/man_Skeleton'))
    executeImportTasks([animation_fbx_task])

```
<a name="NZzHf"></a>
### 创建、复制、删除、重命名资产和文件夹
这些东西可以直接复制到UE的代码编辑框中执行看看效果<br />针对资产编辑器中的内容都要使用unreal.EditorAssetLibrary中的方法，例如创建复制删除重命名文件夹，复制删除重命名资产，判段资产是否存在。
```python
import unreal
# 创建文件夹
def createDirectory():
    unreal.EditorAssetLibrary.make_directory('/Game/MyAsset/MyNewDirectory')


# 复制文件夹
def duplicateDirectory():
    return unreal.EditorAssetLibrary.duplicate_directory('/Game/MyAsset/MyNewDirectory',
                                                         '/Game/MyAsset/MyNewDirectory_Duplicated')


# 删除文件夹
def deleteDirectory():
    unreal.EditorAssetLibrary.delete_directory('/Game/MyAsset/MyNewDirectory')


# 重命名文件夹
def renameDirectory():
    return unreal.EditorAssetLibrary.rename_directory('/Game/MyAsset/MyNewDirectory_Duplicated',
                                                      '/Game/MyAsset/MyNewDirectory_Renamed')


# 复制资产
def duplicateAsset():
    return unreal.EditorAssetLibrary.duplicate_asset('/Game/MyAsset/Textures/test_ORM3',
                                                     '/Game/MyAsset/Textures/test_ORM3_duplicate')


# 删除资产
def deleteAsset():
    unreal.EditorAssetLibrary.delete_asset('/Game/MyAsset/Textures/test_ORM3')


# 判断资产是否存在
def assetExist():
    print(unreal.EditorAssetLibrary.does_asset_exist('/Game/MyAsset/Textures/test_ORM3'))  # False
    print(unreal.EditorAssetLibrary.does_asset_exist('/Game/MyAsset/Textures/test_ORM3_duplicate'))  # True


# 重命名资产
def renameAsset():
    unreal.EditorAssetLibrary.rename_asset('/Game/MyAsset/Textures/test_ORM3_duplicate',
                                           '/Game/MyAsset/Textures/test_ORM3_Renamed')


# 显示复制资产提示框
def duplicateAssetDialog(show_dialog=True):
    if show_dialog:
        unreal.AssetToolsHelpers.get_asset_tools().duplicate_asset_with_dialog('test_ORM3_Duplicated',
                                                                               '/Game/MyAsset/Textures',
                                                                               unreal.load_asset(
                                                                                   '/Game/MyAsset/Textures/test_ORM3_Renamed'))
    else:
        unreal.AssetToolsHelpers.get_asset_tools().duplicate_asset('test_ORM3_Duplicated', '/Game/MyAsset/Textures',
                                                                   unreal.load_asset(
                                                                       '/Game/MyAsset/Textures/test_ORM3_Renamed'))


# 显示重命名提示框
def renameAssetDialog(show_dialog=True):
    first_rename_data = unreal.AssetRenameData(unreal.load_asset('/Game/MyAsset/Textures/test_ORM3_Renamed'),
                                               '/Game/MyAsset/Textures', 'test_ORM3_Renamed_2')
    second_rename_data = unreal.AssetRenameData(unreal.load_asset('/Game/MyAsset/Textures/test_ORM3_Duplicated'),
                                                '/Game/MyAsset/Textures', 'test_ORM3_Duplicated_Renamed')
    if show_dialog:
        unreal.AssetToolsHelpers.get_asset_tools().rename_assets_with_dialog([first_rename_data, second_rename_data])
    else:
        unreal.AssetToolsHelpers.get_asset_tools().rename_assets([first_rename_data, second_rename_data])

```
<a name="PpzFb"></a>
## 使用python调用C++函数
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1657180848774-09e0c281-f9ff-4319-8543-572f2578bf66.png#clientId=u05c02e16-dea5-4&errorMessage=unknown%20error&from=paste&height=1055&id=uc2993bf1&originHeight=1055&originWidth=1694&originalType=binary&ratio=1&rotation=0&showTitle=false&size=464364&status=error&style=none&taskId=ub4686a20-e257-4b92-8c09-42873fc6f90&title=&width=1694)<br />取名字为ZFunctions![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1657181259643-9ffac0ff-7d24-4cec-b669-1c639a650814.png#clientId=u05c02e16-dea5-4&errorMessage=unknown%20error&from=paste&height=426&id=u3724a30b&originHeight=426&originWidth=1294&originalType=binary&ratio=1&rotation=0&showTitle=false&size=236790&status=error&style=none&taskId=ufa38904a-fc3f-41d5-9673-5d2f3346b54&title=&width=1294)<br />创建这个类以后，UE会自动编译打开VisualStudio。![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1657181358854-4381aeec-353e-4adf-b83b-df6db40f2d58.png#clientId=u05c02e16-dea5-4&errorMessage=unknown%20error&from=paste&height=56&id=u6d9a0b40&originHeight=56&originWidth=280&originalType=binary&ratio=1&rotation=0&showTitle=false&size=3120&status=error&style=none&taskId=u829356b5-6591-486c-975e-1e13799faf8&title=&width=280)<br />ZFunctions.h文件内容：
```cpp
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "Kismet/BlueprintFunctionLibrary.h"
#include "ZFunctions.generated.h"

/**
 * 
 */
UCLASS()
class CPLUSPLUSTEST_API UZFunctions : public UBlueprintFunctionLibrary
{
	GENERATED_BODY()

public:
	UFUNCTION(BlueprintCallable) // 将函数暴露给蓝图
		static void CalledFromPython(FString InputString);
	
};

```
ZFunctions.cpp文件内容：
```cpp
// Fill out your copyright notice in the Description page of Project Settings.

#include "ZFunctions.h"

void UZFunctions::CalledFromPython(FString InputString) {
	UE_LOG(LogTemp, Error, TEXT("%s"), *InputString);
}
```
内容写好后就可以<br />然后我们可以在编辑器中通过
```cpp
for x in sorted(dir(unreal)):
	print (x)
```
打印出目前UE项目中所有的类。<br />可以在输出中找到![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1657182694150-31ce542e-d3cb-4b0e-a93b-6c225785a350.png#clientId=u05c02e16-dea5-4&errorMessage=unknown%20error&from=paste&height=145&id=u2a52dbed&originHeight=145&originWidth=313&originalType=binary&ratio=1&rotation=0&showTitle=false&size=8849&status=error&style=none&taskId=ufa7c4b05-c548-4d88-9499-f68a1155c1e&title=&width=313)那就可以使用了。<br />然后我们可以在编辑器中通过
```cpp
for x in sorted(dir(unreal.ZFunctions)):
	print (x)
```
打印出ZFunctions中的所有方法。<br />可以找到刚才定义的方法：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1657183307392-331af0d3-d301-40f4-a2a0-98c7462fc9be.png#clientId=u05c02e16-dea5-4&errorMessage=unknown%20error&from=paste&height=34&id=u421c198a&originHeight=34&originWidth=188&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2734&status=error&style=none&taskId=u21569621-69ee-42c7-80a6-99daa375831&title=&width=188) 可以发现我们明明写的是CalledFromPython，但是UE会自动将命名更改为called_from_python<br />然后我们就可以在UE中使用这个方法了<br />通过代码 unreal.ZFunctions.called_from_python('11111')<br />会使用这个方法的功能，让UE打印一个UE_LOG<br />UE_LOG(LogTemp, Error, TEXT("%s"), *InputString)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1657183613159-578d21d4-7ccc-4af3-b559-eacbac054041.png#clientId=u05c02e16-dea5-4&errorMessage=unknown%20error&from=paste&height=39&id=u0407f35d&originHeight=39&originWidth=453&originalType=binary&ratio=1&rotation=0&showTitle=false&size=5632&status=error&style=none&taskId=u05975b26-9e44-47a8-955a-cc3ea483de2&title=&width=453)
<a name="WPpVr"></a>
## 改变文件夹的颜色
要想修改文件夹的颜色依然需要使用C++，只不过可以通过python语句调用C++函数来实现简单的批量操作...<br />因此依然通过继承Blueprint  Fuction Library 类来创建我们的自定义类。取名为CppLib
<a name="wCOD1"></a>
### CppLib.h
```cpp
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "Kismet/BlueprintFunctionLibrary.h"
#include "CppLib.generated.h"

/**
 * 
 */
UCLASS()
class CPLUSPLUSTEST_API UCppLib : public UBlueprintFunctionLibrary
{
	GENERATED_BODY()

public:
	UFUNCTION(BlueprintCallable, Category = "Unreal Python")
		static void SetFolderColor(FString FolderPath, FLinearColor Color);
};

```
<a name="UvDZx"></a>
### CppLib.cpp
```cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CppLib.h"

void UCppLib::SetFolderColor(FString FolderPath, FLinearColor Color) {
	GConfig->SetString(TEXT("PathColor"), *FolderPath, *Color.ToString(), GEditorPerProjectIni);
}
```
<a name="W75gc"></a>
### 写完c++后可以通过蓝图调用函数
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1657531899356-6d006729-9afd-4c8d-97fa-7e4c83175f8d.png#clientId=uc78214b9-d920-4&errorMessage=unknown%20error&from=paste&height=698&id=u8d7183c3&originHeight=698&originWidth=1749&originalType=binary&ratio=1&rotation=0&showTitle=false&size=152825&status=error&style=none&taskId=ufda12786-170b-4acb-949b-2e9b50aaa76&title=&width=1749)<br />勾选自定义事件的 Call In Editor 就可以在外面手动点击触发自定义事件了。![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1657531961768-a20a0216-2c47-4822-b19d-a691543d9ee1.png#clientId=uc78214b9-d920-4&errorMessage=unknown%20error&from=paste&height=624&id=uf50a7119&originHeight=624&originWidth=610&originalType=binary&ratio=1&rotation=0&showTitle=false&size=58905&status=error&style=none&taskId=ud772c6cb-8db3-4fb6-8261-c2ea8d3d472&title=&width=610)如果是已经存在的文件夹路径，那么点击按钮后不会立刻改变文件夹的颜色，需要重新启动才能够发现改变。不存在的文件夹路径，当创建好对应的文件夹后，文件夹会自动改变颜色。
<a name="oHHlX"></a>
### python调用函数实现批量更改
```cpp
# coding: utf-8

import unreal


# import folderColor as fc
# from imp import reload
# reload(fc)
# fc.generateColoredDirectories()

def generateColoredDirectories():
    for x in range(100, 400):
        dir_path = '/Game/PythonGenerated/' + str(x)
        linear_color = getGradientColor(x)
        unreal.CppLib.set_folder_color(dir_path, linear_color)
        unreal.EditorAssetLibrary.make_directory(dir_path)


def getGradientColor(x):
    x = x - 100
    if x < 100:
        r = 1.0 - x / 100.0
        g = 0.0 + x / 100.0
        b = 0.0
    elif x < 200:
        r = 0.0
        g = 1.0 - (x - 100) / 100.0
        b = 0.0 + (x - 100) / 100.0
    else:
        r = 0.0 + (x - 200) / 100.0
        g = 0.0
        b = 1.0 - (x - 200) / 100.0
    return unreal.LinearColor(r, g, b, 1)

```
效果：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1657534605188-5fd07b83-fbb3-4314-a553-0d49666f707e.png#clientId=uc78214b9-d920-4&errorMessage=unknown%20error&from=paste&height=434&id=ud7d21ee3&originHeight=434&originWidth=2058&originalType=binary&ratio=1&rotation=0&showTitle=false&size=136042&status=error&style=none&taskId=u862795a0-5e66-40c1-a790-af9d4d9819b&title=&width=2058)
<a name="yacQ4"></a>
## 如何使用c++和Python打开和关闭资产
python 只能打开资产，关闭资产需要通过C++来实现。
<a name="UIkJl"></a>
### 先看python如何打开资产
```python
import unreal
# 在ue中执行的调用命令
# from imp import reload
# import openAssets_10 as oa
# reload(oa)
# oa.openAssets()

# 打开资产
def openAssets():
    assets = [unreal.load_asset('/Game/MyAsset/Sounds/soundTest'),
              unreal.load_asset('/Game/MyAsset/Textures/light_setAOVs'),
              unreal.load_asset('/Game/MyAsset/Textures/light_createShot'),
              unreal.load_asset('/Game/MyAsset/Textures/light_importLight')]
    unreal.AssetToolsHelpers.get_asset_tools().open_editor_for_assets(assets)

# 调用自定义的C++类中的函数
def getAllOpenedAssets():
    return unreal.CppLib.get_assets_opened_in_editor()

def closeAssets():
    assets = getAllOpenedAssets()
    unreal.CppLib.close_editor_for_assets(assets)
```
<a name="HUW7O"></a>
### UE中模块修改
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1659002804160-678071e2-135e-4dff-9291-df6ea04cb85e.png#clientId=u88952200-365e-4&errorMessage=unknown%20error&from=paste&height=583&id=uc0dc5e8a&originHeight=583&originWidth=324&originalType=binary&ratio=1&rotation=0&showTitle=false&size=20749&status=error&style=none&taskId=u71ae05de-611d-40ba-86c3-3f49a71bef2&title=&width=324)这个.Build.cs格式的是当前项目的模块<br />进入这个模块需要修改：<br />主要是增加了一项："UnrealEd"

<a name="JrJq3"></a>
### CPlusPlusTest.Build.cs
首先说明一下这里的CPlusPlusTest是ue4.27中创建的项目名<br />在原有的基础上新增了"UnrealEd"<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1659003281786-9ec3ec8a-52f6-43de-969b-357743238a21.png#clientId=u88952200-365e-4&errorMessage=unknown%20error&from=paste&height=527&id=u4e1a4527&originHeight=527&originWidth=2030&originalType=binary&ratio=1&rotation=0&showTitle=false&size=92636&status=error&style=none&taskId=u602760b9-d2f1-40d6-9760-60ca217cda8&title=&width=2030)
```cpp
// Copyright Epic Games, Inc. All Rights Reserved.

using UnrealBuildTool;

public class CPlusPlusTest : ModuleRules
{
	public CPlusPlusTest(ReadOnlyTargetRules Target) : base(Target)
	{
		PCHUsage = PCHUsageMode.UseExplicitOrSharedPCHs;

		PublicDependencyModuleNames.AddRange(new string[] { "Core", "CoreUObject", "Engine", "InputCore", "HeadMountedDisplay", "UnrealEd" });
	}
}

```
<a name="IxqdD"></a>
### CppLib.h
在上一节的基础上 新增了两个函数：<br />CloseEditorForAssets<br />GetAssetsOpendInEditor
```cpp
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "Kismet/BlueprintFunctionLibrary.h"
#include "CppLib.generated.h"

/**
 * 
 */
UCLASS()
class CPLUSPLUSTEST_API UCppLib : public UBlueprintFunctionLibrary
{
	GENERATED_BODY()

public:
	UFUNCTION(BlueprintCallable, Category = "Unreal Python")
		static void SetFolderColor(FString FolderPath, FLinearColor Color);

	UFUNCTION(BlueprintCallable, Category = "Unreal Python")
		static void CloseEditorForAssets(TArray<UObject*> Assets);

	UFUNCTION(BlueprintCallable, Category = "Unreal Python")
		static TArray<UObject*> GetAssetsOpenedInEditor();
};

```
<a name="YAVAV"></a>
### CppLib.cpp
这里除了定义函数功能还有个要注意的是要include "Editor.h"
```cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CppLib.h"
#include "Editor.h"
#include "Editor/UnrealEd/Public/Toolkits/AssetEditorManager.h"
void UCppLib::SetFolderColor(FString FolderPath, FLinearColor Color) {
	GConfig->SetString(TEXT("PathColor"), *FolderPath, *Color.ToString(), GEditorPerProjectIni);
}

void UCppLib::CloseEditorForAssets(TArray<UObject*> Assets) {
	UAssetEditorSubsystem* AssetEditorSubsystem = GEditor->GetEditorSubsystem<UAssetEditorSubsystem>();
	for (UObject* Asset : Assets) {
		AssetEditorSubsystem->CloseAllEditorsForAsset(Asset);
	}
}

TArray<UObject*> UCppLib::GetAssetsOpenedInEditor() {
	UAssetEditorSubsystem* AssetEditorSubsystem = GEditor->GetEditorSubsystem<UAssetEditorSubsystem>();
	TArray<UObject*> EditedAssets = AssetEditorSubsystem->GetAllEditedAssets();
	return EditedAssets;
}
```
<a name="mq42D"></a>
### 在UE中进行调用
from imp import reload<br />import openAssets_10 as oa<br />reload(oa)<br />oa.openAssets()# 打开资产<br />oa.closeAssets()# 关闭资产<br />oa.getAllOpenedAssets()#得到当前打开的资产的信息（需要用一个变量来接受它，是一个列表）
<a name="KycrD"></a>
## 使用Python和C ++选择内容浏览器的资产
<a name="Nghfs"></a>
### python
使用python来选择有弊端，就是它不能选择文件夹以及关卡，因此还要介绍通过C++如何选择
```python
import unreal
# from imp import reload
# import selectAssets_11 as sa
# reload(sa)
# sa.showAssetsInContentBrowser()
def showAssetsInContentBrowser():
    paths = ['/Game/MyAsset/Sounds/SoundTest',
             '/Game/MyAsset/Textures/light_setAOVs']
    unreal.EditorAssetLibrary.sync_browser_to_objects(paths)
```
<a name="Eu4Sv"></a>
### CPlusPlusTest.Build.cs
又新增了这三个，因为.cpp用到了Module![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1659063963423-a412bbf8-0b53-46af-b1dd-7d79fe83847f.png#clientId=u765cde32-d8a7-4&errorMessage=unknown%20error&from=paste&height=241&id=u5e93f960&originHeight=241&originWidth=1013&originalType=binary&ratio=1&rotation=0&showTitle=false&size=78968&status=error&style=none&taskId=u8231aafe-0b3a-498c-80ca-6d9b767c64a&title=&width=1013)  最后的EditorWidgets不添加的话编译不了，教程中没有加这个，UE4.27，VS2019需要加EditorWidgets，加了以后就可以用了<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1659071465975-e002a595-a779-4c77-b83a-343028d3efd2.png#clientId=u765cde32-d8a7-4&errorMessage=unknown%20error&from=paste&height=252&id=u6df4cf01&originHeight=252&originWidth=1590&originalType=binary&ratio=1&rotation=0&showTitle=false&size=27687&status=error&style=none&taskId=u2ffc3186-426c-469f-b854-54204f052d9&title=&width=1590)
<a name="O69Kh"></a>
### CppLib.h
到现在我才发现在头文件里面写了构造函数后可以通过左边的螺丝刀图标快速创建在源文件中![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1659064115807-08559492-b055-410a-ab08-a01ba6e0b0a1.png#clientId=u765cde32-d8a7-4&errorMessage=unknown%20error&from=paste&height=105&id=uc3682901&originHeight=105&originWidth=321&originalType=binary&ratio=1&rotation=0&showTitle=false&size=12833&status=error&style=none&taskId=u4f3b1f25-c1f6-4aca-ba83-1859c310e14&title=&width=321)
```cpp
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "Kismet/BlueprintFunctionLibrary.h"
#include "CppLib.generated.h"

/**
 * 
 */
UCLASS()
class CPLUSPLUSTEST_API UCppLib : public UBlueprintFunctionLibrary
{
	GENERATED_BODY()

public:
	UFUNCTION(BlueprintCallable, Category = "Unreal Python")
		static void SetFolderColor(FString FolderPath, FLinearColor Color); // 批量创建文件夹并修改颜色

	UFUNCTION(BlueprintCallable, Category = "Unreal Python")
		static void CloseEditorForAssets(TArray<UObject*> Assets); // 关闭打开的资产的窗口

	UFUNCTION(BlueprintCallable, Category = "Unreal Python")
		static TArray<UObject*> GetAssetsOpenedInEditor(); // 获得已经打开资产窗口的资产的路径字符串列表

	UFUNCTION(BlueprintCallable, Category = "Unreal Python")
		static TArray<FString> GetSelectedAssets(); // 获得选择的资产的路径字符串列表
	
	UFUNCTION(BlueprintCallable, Category = "Unreal Python")
		static TArray<FString> GetSelectedFolders(); // 获得选择的文件夹的路径字符串列表

	UFUNCTION(BlueprintCallable, Category = "Unreal Python")
		static void SetSelectedAssets(TArray<FString> Paths); // 选择路径字符串列表中的资产

	UFUNCTION(BlueprintCallable, Category = "Unreal Python")
		static void SetSelectedFolders(TArray<FString> Paths); // 选择路径字符串列表中的文件夹

};

```
<a name="W1fC1"></a>
### CppLib.cpp
```cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CppLib.h"
#include "Editor.h"
#include "Editor/UnrealEd/Public/Toolkits/AssetEditorManager.h"
#include "Editor/ContentBrowser/Public/ContentBrowserModule.h"
#include "Editor/ContentBrowser/Private/ScontentBrowser.h"
#include "Runtime/AssetRegistry/Public/AssetRegistryModule.h"
void UCppLib::SetFolderColor(FString FolderPath, FLinearColor Color) {
	GConfig->SetString(TEXT("PathColor"), *FolderPath, *Color.ToString(), GEditorPerProjectIni);
}

void UCppLib::CloseEditorForAssets(TArray<UObject*> Assets) {
	UAssetEditorSubsystem* AssetEditorSubsystem = GEditor->GetEditorSubsystem<UAssetEditorSubsystem>();
	for (UObject* Asset : Assets) {
		AssetEditorSubsystem->CloseAllEditorsForAsset(Asset);
	}
}

TArray<UObject*> UCppLib::GetAssetsOpenedInEditor() {
	UAssetEditorSubsystem* AssetEditorSubsystem = GEditor->GetEditorSubsystem<UAssetEditorSubsystem>();
	TArray<UObject*> EditedAssets = AssetEditorSubsystem->GetAllEditedAssets();
	return EditedAssets;
}

TArray<FString> UCppLib::GetSelectedAssets()
{
	FContentBrowserModule& ContentBrowserModule = FModuleManager::LoadModuleChecked<FContentBrowserModule>("ContentBrowser");
	TArray<FAssetData> SelectedAssets;
	ContentBrowserModule.Get().GetSelectedAssets(SelectedAssets);
	TArray<FString> Result;
	for (FAssetData& AssetData : SelectedAssets) {
		Result.Add(AssetData.PackageName.ToString());
	}
	return Result;
}

TArray<FString> UCppLib::GetSelectedFolders()
{
	FContentBrowserModule& ContentBrowserModule = FModuleManager::LoadModuleChecked<FContentBrowserModule>("ContentBrowser");
	TArray<FString> SelectedFolders;
	ContentBrowserModule.Get().GetSelectedFolders(SelectedFolders);
	return SelectedFolders;
}

void UCppLib::SetSelectedAssets(TArray<FString> Paths)
{
	FContentBrowserModule& ContentBrowserModule = FModuleManager::LoadModuleChecked<FContentBrowserModule>("ContentBrowser");
	FAssetRegistryModule& AssetRegistryModule = FModuleManager::LoadModuleChecked<FAssetRegistryModule>("AssetRegistry");
	TArray<FName> PathsName;
	for (FString Path : Paths) {
		PathsName.Add(*Path);
	}
	FARFilter AssetFilter;
	AssetFilter.PackageNames = PathsName;
	TArray<FAssetData> AssetDatas;
	AssetRegistryModule.Get().GetAssets(AssetFilter, AssetDatas);
	ContentBrowserModule.Get().SyncBrowserToAssets(AssetDatas);
}

void UCppLib::SetSelectedFolders(TArray<FString> Paths)
{
	FContentBrowserModule& ContentBrowserModule = FModuleManager::LoadModuleChecked<FContentBrowserModule>("ContentBrowser");
	TArray<FString> SelectedFolders;
	ContentBrowserModule.Get().SyncBrowserToFolders(Paths);
}
```
<a name="vAd5P"></a>
## 如何用Python显示缓慢的任务进度
执行循环的过程的同时显示进度：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1659079195804-be1a6f84-5236-4712-95d1-5eaf4518c3cd.png#clientId=u765cde32-d8a7-4&errorMessage=unknown%20error&from=paste&height=166&id=u12c81568&originHeight=166&originWidth=859&originalType=binary&ratio=1&rotation=0&showTitle=false&size=29624&status=error&style=none&taskId=u05ec8549-fa39-408c-8a5d-d38cf9c9741&title=&width=859)
<a name="w8RHJ"></a>
### python
```python
import unreal
import random
# from imp import reload
# import showSlowTasksProgression_12 as test
# reload(test)
# test.executeSlowTask()

def executeSlowTask():
    quantity_steps_in_slow_task = 10000
    with unreal.ScopedSlowTask(quantity_steps_in_slow_task, 'My Slow Task Text ...') as slow_task:
        slow_task.make_dialog(True)
        for x in range(quantity_steps_in_slow_task):
            if slow_task.should_cancel():
                break
            slow_task.enter_progress_frame(1, 'My Slow Task Text ...' + str(x) + '/' + str(quantity_steps_in_slow_task))
            # Execute slow logic
            deferredSpawnActor()

def deferredSpawnActor():
    world = unreal.EditorLevelLibrary.get_editor_world()
    actor_class = unreal.EditorAssetLibrary.load_blueprint_class('/Game/MyBluePrint/BPActor')
    actor_location = unreal.Vector(random.uniform(0.0, 2000.0), random.uniform(0.0, 2000.0), 0.0)
    actor_rotation = unreal.Rotator(random.uniform(0.0, 360.0), random.uniform(0.0, 360.0), random.uniform(0.0, 360.0))
    actor_scale = unreal.Vector(random.uniform(0.1, 2.0), random.uniform(0.1, 2.0), random.uniform(0.1, 2.0))
    actor_transform = unreal.Transform(actor_location, actor_rotation, actor_scale)
    # actor = unreal.GameplayStatics.begin_deferred_actor_spawn_from_class(world, actor_class, actor_transform)
    # unreal.GameplayStatics.finish_spawning_actor(actor, actor_transform)
    actor = unreal.CppLib.get_actor(world, actor_class, actor_transform)
    unreal.CppLib.set_actor(actor,actor_transform)

```
<a name="FhjgO"></a>
### CppLib.h
```cpp
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "Kismet/BlueprintFunctionLibrary.h"
#include "CppLib.generated.h"

/**
* 
*/
UCLASS()
    class CPLUSPLUSTEST_API UCppLib : public UBlueprintFunctionLibrary
    {
    GENERATED_BODY()
    
    public:
    UFUNCTION(BlueprintCallable, Category = "Unreal Python")
    static void SetFolderColor(FString FolderPath, FLinearColor Color); // 批量创建文件夹并修改颜色
    
    UFUNCTION(BlueprintCallable, Category = "Unreal Python")
    static void CloseEditorForAssets(TArray<UObject*> Assets); // 关闭打开的资产的窗口
    
    UFUNCTION(BlueprintCallable, Category = "Unreal Python")
    static TArray<UObject*> GetAssetsOpenedInEditor(); // 获得已经打开资产窗口的资产的路径字符串列表
    
    UFUNCTION(BlueprintCallable, Category = "Unreal Python")
    static TArray<FString> GetSelectedAssets(); // 获得选择的资产的路径字符串列表
    
    UFUNCTION(BlueprintCallable, Category = "Unreal Python")
    static TArray<FString> GetSelectedFolders(); // 获得选择的文件夹的路径字符串列表
    
    UFUNCTION(BlueprintCallable, Category = "Unreal Python")
    static void SetSelectedAssets(TArray<FString> Paths); // 选择路径字符串列表中的资产
    
    UFUNCTION(BlueprintCallable, Category = "Unreal Python")
    static void SetSelectedFolders(TArray<FString> Paths); // 选择路径字符串列表中的文件夹
    
    UFUNCTION(BlueprintCallable, Category = "Unreal Python")
    static AActor* GetActor(const UObject* WorldContextObject,TSubclassOf< AActor > ActorClass,const FTransform& SpawnTransform); // 获取ActorBP
    
    UFUNCTION(BlueprintCallable, Category = "Unreal Python")
    static void setActor(class AActor* Actor,const FTransform& SpawnTransform); // 创建AcotrBP
    
    };

```
<a name="JryYA"></a>
### CppLib.cpp
```cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CppLib.h"
#include "Editor.h"
#include "Editor/UnrealEd/Public/Toolkits/AssetEditorManager.h"
#include "Editor/ContentBrowser/Public/ContentBrowserModule.h"
#include "Editor/ContentBrowser/Private/ScontentBrowser.h"
#include "Runtime/AssetRegistry/Public/AssetRegistryModule.h"
#include "Runtime/Engine/Classes/Kismet/GameplayStatics.h"
void UCppLib::SetFolderColor(FString FolderPath, FLinearColor Color) {
    GConfig->SetString(TEXT("PathColor"), *FolderPath, *Color.ToString(), GEditorPerProjectIni);
}

void UCppLib::CloseEditorForAssets(TArray<UObject*> Assets) {
    UAssetEditorSubsystem* AssetEditorSubsystem = GEditor->GetEditorSubsystem<UAssetEditorSubsystem>();
    for (UObject* Asset : Assets) {
        AssetEditorSubsystem->CloseAllEditorsForAsset(Asset);
    }
}

TArray<UObject*> UCppLib::GetAssetsOpenedInEditor() {
    UAssetEditorSubsystem* AssetEditorSubsystem = GEditor->GetEditorSubsystem<UAssetEditorSubsystem>();
    TArray<UObject*> EditedAssets = AssetEditorSubsystem->GetAllEditedAssets();
    return EditedAssets;
}

TArray<FString> UCppLib::GetSelectedAssets()
{
    FContentBrowserModule& ContentBrowserModule = FModuleManager::LoadModuleChecked<FContentBrowserModule>("ContentBrowser");
    TArray<FAssetData> SelectedAssets;
    ContentBrowserModule.Get().GetSelectedAssets(SelectedAssets);
    TArray<FString> Result;
    for (FAssetData& AssetData : SelectedAssets) {
        Result.Add(AssetData.PackageName.ToString());
    }
    return Result;
}

TArray<FString> UCppLib::GetSelectedFolders()
{
    FContentBrowserModule& ContentBrowserModule = FModuleManager::LoadModuleChecked<FContentBrowserModule>("ContentBrowser");
    TArray<FString> SelectedFolders;
    ContentBrowserModule.Get().GetSelectedFolders(SelectedFolders);
    return SelectedFolders;
}

void UCppLib::SetSelectedAssets(TArray<FString> Paths)
{
    FContentBrowserModule& ContentBrowserModule = FModuleManager::LoadModuleChecked<FContentBrowserModule>("ContentBrowser");
    FAssetRegistryModule& AssetRegistryModule = FModuleManager::LoadModuleChecked<FAssetRegistryModule>("AssetRegistry");
    TArray<FName> PathsName;
    for (FString Path : Paths) {
        PathsName.Add(*Path);
    }
    FARFilter AssetFilter;
    AssetFilter.PackageNames = PathsName;
    TArray<FAssetData> AssetDatas;
    AssetRegistryModule.Get().GetAssets(AssetFilter, AssetDatas);
    ContentBrowserModule.Get().SyncBrowserToAssets(AssetDatas);
}

void UCppLib::SetSelectedFolders(TArray<FString> Paths)
{
    FContentBrowserModule& ContentBrowserModule = FModuleManager::LoadModuleChecked<FContentBrowserModule>("ContentBrowser");
    TArray<FString> SelectedFolders;
    ContentBrowserModule.Get().SyncBrowserToFolders(Paths);
}

AActor* UCppLib::GetActor(const UObject* WorldContextObject, TSubclassOf<AActor> ActorClass, const FTransform& SpawnTransform)
{
    return UGameplayStatics::BeginDeferredActorSpawnFromClass(WorldContextObject, ActorClass, SpawnTransform);
}

void UCppLib::setActor(AActor* Actor, const FTransform& SpawnTransform)
{
    UGameplayStatics::FinishSpawningActor(Actor, SpawnTransform);
}

```
<a name="ywGiE"></a>
## 打印类的所有属性
<a name="ToiOf"></a>
### Cpplib.h
```cpp
UFUNCTION(BlueprintCallable, Category = "Unreal Python")
		static TArray<FString>GetAllProperties(UClass* Class);  //获取类的所有属性
```
<a name="Zvf6B"></a>
### Cpplib.cpp
```cpp
TArray<FString> UCppLib::GetAllProperties(UClass* Class)
{
	TArray<FString> Ret;
	if (Class != nullptr) {
		for (TFieldIterator<UProperty> It(Class); It; ++It) {
			UProperty* Property = *It;
			if (Property->HasAnyPropertyFlags(EPropertyFlags::CPF_Edit)) {
				Ret.Add(Property->GetName());
			}
		}
	}
	return Ret;
}
```
<a name="p9fCp"></a>
### python
```python
import unreal

def getAllProperties(object_class):
    return unreal.CppLib.get_all_properties(object_class)  # 通过自定义C++的类中的函数，得到所有属性的字符串列表

def printAllProperties():
    obj = unreal.Actor()  # 将打印actor类型的所有属性
    object_class = obj.get_class()
    for x in getAllProperties(object_class):
        y = x
        # while循环的作用是为了对齐字符串
        while len(y) < 42:
            y = ' ' + y
        print(y + ':' + str(obj.get_editor_property(x)))

```
<a name="ABily"></a>
### 执行效果
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1662010703000-8b4963c7-8191-4200-9333-ddecc3455391.png#clientId=u22a16aa5-3892-4&errorMessage=unknown%20error&from=paste&height=559&id=u9b275170&originHeight=559&originWidth=979&originalType=binary&ratio=1&rotation=0&showTitle=false&size=110690&status=error&style=none&taskId=u296b7b42-73fd-42fe-9c35-1f927f96924&title=&width=979)
<a name="taWQV"></a>
## 一次性执行多个cmd命令
<a name="tIQjq"></a>
### CppLib.h
```cpp
	UFUNCTION(BlueprintCallable, Category = "Unreal Python")
		static void ExecuteConsoleCommand(FString ConsoleCmd); //执行多行命令行
```
<a name="nVxcr"></a>
### CppLib.cpp
需要#include "Editor.h"
```cpp
void UCppLib::ExecuteConsoleCommand(FString ConsoleCmd)
{
	if (GEditor) {
		UWorld* World = GEditor->GetEditorWorldContext().World();
		if (World) {
			GEditor->Exec(World, *ConsoleCmd, *GLog);
		}
	}
}
```
<a name="kAYMM"></a>
### python
```python
import unreal
import random


def executeConsoleCommand():
    console_cmd = ['r.ScreenPercentage 0.1',
                   'r.Color.Max 6',
                   'stat fps',
                   'stat unit']
    for x in console_cmd:
        unreal.CppLib.execute_console_command(x)
```
<a name="jqYhG"></a>
## 选择场景中的actor与清除选择
```python
import unreal


def get_selected_actors():
    return unreal.EditorLevelLibrary.get_selected_level_actors()


def get_selected_actors_EXAMPLE():
    for x in get_selected_actors():
        print(x)


def select_actors(actors_to_select=[]):
    unreal.EditorLevelLibrary.set_selected_level_actors(actors_to_select)


def select_actors_EXAMPLE():
    all_actors = unreal.EditorLevelLibrary.get_all_level_actors()
    actors_to_select = []
    for x in range(len(all_actors)):
        actors_to_select.append(all_actors[x])
    select_actors(actors_to_select)


def clear_actor_selection_EXAMPLE():
    select_actors()

```
<a name="mW84U"></a>
## 生成默认资源（材质粒子关卡等）
```python
# 创建基础资产
def create_generic_asset(asset_path='', unique_name=True, asset_class=None, asset_factory=None):
    if unique_name:  # 如果命名冲突的话会自动生成一个新的唯一的路径名字(后缀加数字)
        asset_path, asset_name = unreal.AssetToolsHelpers.get_asset_tools().create_unique_asset_name(
            base_package_name=asset_path, suffix='')
    if not unreal.EditorAssetLibrary.does_asset_exist(asset_path=asset_path):
        path = asset_path.rsplit('/', 1)[0]
        name = asset_path.rsplit('/', 1)[1]
        return unreal.AssetToolsHelpers.get_asset_tools().create_asset(
            asset_name=name,
            package_path=path,
            asset_class=asset_class,
            factory=asset_factory
        )
    return unreal.load_asset(asset_path)


# 调用创建基础资产的举例
def create_generic_asset_EXAMPLE():
    base_path = '/Game/GenericAssets/'
    generic_assets = [
        [
            base_path + 'sequence',
            unreal.LevelSequence,
            unreal.LevelSequenceFactoryNew()
        ],
        [
            base_path + 'material',
            unreal.Material,
            unreal.MaterialFactoryNew()
        ],
        [
            base_path + 'world',
            unreal.World,
            unreal.WorldFactory()
        ],
        [
            base_path + 'particle_system',
            unreal.ParticleSystem,
            unreal.ParticleSystemFactoryNew()
        ],
        [
            base_path + 'paper_flipbook',
            unreal.PaperFlipbook,
            unreal.PaperFlipbookFactory()
        ]
    ]
    for asset in generic_assets:
        print(create_generic_asset(asset[0], True, asset[1], asset[2]))

```
<a name="qpNWT"></a>
## 在蓝图中使用python
在4.25版本之前的ue中需要用c++添加蓝图节点但是在新版本已经内置了能在蓝图中使用python的节点。但是无法在运行时可用的蓝图类（例如直接从 **Actor** 派生的类）中使用此方法。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1662020863952-4b2f949c-5fa1-4fd2-a215-cb7b1022281e.png#clientId=u22a16aa5-3892-4&errorMessage=unknown%20error&from=paste&height=108&id=u57ca3ead&originHeight=108&originWidth=321&originalType=binary&ratio=1&rotation=0&showTitle=false&size=14297&status=error&style=none&taskId=ua8e75acd-6305-48ec-b2d7-8a9fe9078f6&title=&width=321)
<a name="wWH8n"></a>
# B站搬运Udemy教程
链接：[https://www.bilibili.com/video/BV1GY4y1s7qM?p=8&spm_id_from=pageDriver&vd_source=b1de3fe38e887eb40fc55a5485724480](https://www.bilibili.com/video/BV1GY4y1s7qM?p=8&spm_id_from=pageDriver&vd_source=b1de3fe38e887eb40fc55a5485724480)<br />[https://www.bilibili.com/video/BV18q4y1X7DH?p=11&vd_source=b1de3fe38e887eb40fc55a5485724480](https://www.bilibili.com/video/BV18q4y1X7DH?p=11&vd_source=b1de3fe38e887eb40fc55a5485724480)<br />这两个教程链接内容是一样的，但是有的教程链接中的内容可能有点损坏，互补一下。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1663053942549-57973196-eff2-418d-a600-2a293b1f5040.png#clientId=ue9ce22a4-2e2e-4&errorMessage=unknown%20error&from=paste&height=178&id=ue78a2402&originHeight=178&originWidth=209&originalType=binary&ratio=1&rotation=0&showTitle=false&size=35533&status=error&style=none&taskId=u1a865568-c0b5-4975-b5d3-97ee5e65145&title=&width=209)

<a name="u403x"></a>
## P10工厂和资产创造
什么是工厂：当我们需要创建一个资产的时候（蓝图，声音，关卡等），我们就需要去工厂去取（factory），因此我们需要先找到对应的工厂：[LevelFactory](https://docs.unrealengine.com/4.27/en-US/PythonAPI/class/LevelFactory.html)，[BlueprintFactory](https://docs.unrealengine.com/4.27/en-US/PythonAPI/class/BlueprintFactory.html)等。<br />以创建蓝图举例：<br />创建工厂对象相当于点击这些：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1663056902672-816725d5-0293-46a5-bbef-68c4cfeda9f5.png#clientId=ua74dfa99-2388-4&errorMessage=unknown%20error&from=paste&height=632&id=u82702c01&originHeight=632&originWidth=216&originalType=binary&ratio=1&rotation=0&showTitle=false&size=33231&status=error&style=none&taskId=u182c88b2-bc5b-42e1-a89b-335b71af25b&title=&width=216)

创建完工厂后（点击后）需要选择继承的类![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1663056967314-be14bd41-e4ad-4cbf-824a-6be26d61a8a1.png#clientId=ua74dfa99-2388-4&errorMessage=unknown%20error&from=paste&height=743&id=u8a06f157&originHeight=743&originWidth=544&originalType=binary&ratio=1&rotation=0&showTitle=false&size=98896&status=error&style=none&taskId=ue20e6a4d-6f9c-4763-9eb4-4bbfa2f4259&title=&width=544)<br />初始设置完成后开始创造资产，创造资产需要使用unreal.AssetToolsHelpers.get_asset_tools()<br />利用这个工具中的create_asset方法创建。<br />创建完后用unreal.EditorAssetLibrary.save_loaded_asset进行保存<br />代码：
```python
import unreal

blueprintName = "python_create_BP"
blueprintPath = "/Game/MyBluePrint"

factory = unreal.BlueprintFactory()
factory.set_editor_property("ParentClass", unreal.Actor)

assetTools = unreal.AssetToolsHelpers.get_asset_tools()
myFancyNewAssetFile = assetTools.create_asset(blueprintName, blueprintPath, None, factory)

unreal.EditorAssetLibrary.save_loaded_asset(myFancyNewAssetFile)
```
<a name="x0zPC"></a>
## P11制作任务进度条：
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1663060403285-f485f6df-06a3-4c80-8f52-fc9c526f60c0.png#clientId=ua74dfa99-2388-4&errorMessage=unknown%20error&from=paste&height=133&id=uc0d5f7e7&originHeight=133&originWidth=648&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7070&status=error&style=none&taskId=u6fc3c721-c9d7-46ef-80dd-352a5047316&title=&width=648)
```python
import unreal

totalFrames = 1000000
textDisplay = "i love python, an i guess i'll be using this for a while!"

with unreal.ScopedSlowTask(totalFrames, textDisplay) as ST:
    ST.make_dialog(True)
    for i in range(totalFrames):
        if ST.should_cancel():
            break
        unreal.log("one step!!!!")
        ST.enter_progress_frame(1)
        
```
<a name="b21xj"></a>
## P12综合案例：批量创建继承自actor的蓝图资产（带进度条）
```python
import unreal

totalRequiredBlueprints = 20
newAssetName = "BP_pythonMade_%d"
createdAssetsPath = "/Game/TestStuff"
slowTaskDisplayText = "Createing new assets....."

factory = unreal.BlueprintFactory()
factory.set_editor_property("ParentClass", unreal.Actor)

assetTools = unreal.AssetToolsHelpers.get_asset_tools()

with unreal.ScopedSlowTask(totalRequiredBlueprints, slowTaskDisplayText) as ST:
    ST.make_dialog(True)
    for x in range(totalRequiredBlueprints):
        if ST.should_cancel():
            break
        newAsset = assetTools.create_asset(newAssetName % (x), createdAssetsPath, None, factory)
        unreal.EditorAssetLibrary.save_loaded_asset(newAsset)
        unreal.log("Just created an asset BP_PythonMade_%d via PYTHON API" % (x))
        ST.enter_progress_frame(1)

```
<a name="E5UPW"></a>
## P13 根据选择的资产创建Actor(在关卡中的都叫actor)
教程上的获取选择的资产是这样：<br />@unreal.uclass()<br />class MyEditorUtility(unreal.GlobalEditorUtilityBase):<br />    pass

selectedAssets = MyEditorUtility().get_selected_assets()<br />但是官网教程有教可以通过这样获取选择的资产：<br />selectedAssets = unreal.EditorUtilityLibrary.get_selected_assets()
```python
import unreal

actorsCount = 50
slowTaskDisplayText = "Spawning actors in the level....."

selectedAssets = unreal.EditorUtilityLibrary.get_selected_assets()
with unreal.ScopedSlowTask(actorsCount, slowTaskDisplayText) as ST:
    ST.make_dialog(True)
    for x in range(actorsCount):
        if ST.should_cancel():
            break
        unreal.EditorLevelLibrary.spawn_actor_from_object(selectedAssets[0], unreal.Vector(1.0+x*100, 1.0+x*100, 30.0),  unreal.Rotator(0.0, 0.0, 10.0*x))
        unreal.log("Just added an actor to the level!")
        ST.enter_progress_frame(1)
```
<a name="XtLCO"></a>
## P15修改选择的资产或者actor的属性
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1663135564986-6b21ac2f-abd0-4932-a01d-b3a0984e89f0.png#clientId=u2c683694-c481-4&errorMessage=unknown%20error&from=paste&height=378&id=uf92eda78&originHeight=378&originWidth=2305&originalType=binary&ratio=1&rotation=0&showTitle=false&size=259521&status=error&style=none&taskId=ubcce0a4d-a366-4670-a268-197dd9edee4&title=&width=2305)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1663135493400-bab6c656-b4d8-41bf-b30a-15bd0ab1b0db.png#clientId=u2c683694-c481-4&errorMessage=unknown%20error&from=paste&height=418&id=u7ab464ca&originHeight=418&originWidth=472&originalType=binary&ratio=1&rotation=0&showTitle=false&size=28019&status=error&style=none&taskId=u6eb5e81a-b64f-41db-b98c-33cf6616fe7&title=&width=472)<br />例如如果我们要修改这些属性
```python
import unreal

selectedAssets = unreal.EditorUtilityLibrary.get_selected_assets()

for selectedAsset in selectedAssets:
    selectedAsset.set_editor_property("BlueprintDisplayName", "Some BP")
    selectedAsset.set_editor_property("BlueprintCategory", "Collectable")
    selectedAsset.set_editor_property("BlueprintDescription", "This is a blueprint generated by Python or something")

selectedActors = unreal.EditorLevelLibrary.get_selected_level_actors()
for actor in selectedActors:
    actor.set_editor_property("canRotate", True)
    actor.set_editor_property("bHidden", 1)
    actor.set_editor_property("SpriteScale", 7.5)
```
其中bHidden和SpriteScale对应的是ActorHiddenInGame和EditorBillboardScale<br />之所以使用的不是ue编辑器显示的界面名字是因为ue源码中设置的这些是编辑器中显示的名字，实际上源码中使用的变量名字并不是这些，并且bHidden在ue中显示的是名字是ActorHiddenInGame而且看起来是布尔变量，但是源码中实际上是int类型的名字叫bHidden。<br />那么如何在源码中查找真正的变量名字与类型呢？<br />例如这里设置actor的属性，我们就可以去Actor.h文件中搜索ue界面编辑器中显示的名字，然后就可以查找出来真正的名字与类型。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1663225180561-c530c9ec-dd16-48f7-8259-85e0e4a71ede.png#clientId=ueac702c7-aad3-4&errorMessage=unknown%20error&from=paste&height=1214&id=u1544bd73&originHeight=1214&originWidth=3437&originalType=binary&ratio=1&rotation=0&showTitle=false&size=408022&status=error&style=none&taskId=ua187c3b2-5425-48b5-a5b6-fd3c22603e2&title=&width=3437)
<a name="evWjm"></a>
## <br />P16 python与蓝图的结合
把P12的功能做成一个带UI的工具：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1663150571998-5f5deac5-591b-4ab2-bd80-7690ed71f044.png#clientId=u2c683694-c481-4&errorMessage=unknown%20error&from=paste&height=200&id=u75eda6c1&originHeight=200&originWidth=584&originalType=binary&ratio=1&rotation=0&showTitle=false&size=21438&status=error&style=none&taskId=u6a8d9efc-4497-4c5f-bf99-b06cc6c4a2a&title=&width=584)<br />其中滑块与文本之间可以通过函数进行绑定：<br />在UI编辑器中选择文本控件：![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1663150642231-c9236cc6-f52f-41a1-9967-e40c33db75bd.png#clientId=u2c683694-c481-4&errorMessage=unknown%20error&from=paste&height=84&id=u7ecbe491&originHeight=84&originWidth=1217&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7777&status=error&style=none&taskId=ua94a5c18-8902-4582-ad52-1833ec1f8a4&title=&width=1217)在text处进行绑定：<br />参考：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1663150677829-f9671f11-a34e-41d9-b565-0aff32be9f0c.png#clientId=u2c683694-c481-4&errorMessage=unknown%20error&from=paste&height=384&id=u42e0dfe8&originHeight=384&originWidth=1265&originalType=binary&ratio=1&rotation=0&showTitle=false&size=93090&status=error&style=none&taskId=uffde632b-5fe1-47ca-943f-c4ecc154a5e&title=&width=1265)<br />python在蓝图节点中使用：<br />步骤：使用FormatText节点，节点中使用花括号框住的变量会自动产生引脚，为引脚传递数值配合python代码使用executePythonCommand节点执行。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1663150698315-ca5c5d83-c521-43ab-b632-359171aae0ca.png#clientId=u2c683694-c481-4&errorMessage=unknown%20error&from=paste&height=707&id=u395b52ea&originHeight=707&originWidth=1709&originalType=binary&ratio=1&rotation=0&showTitle=false&size=170315&status=error&style=none&taskId=u141b2d81-9c0a-45e2-bde4-9f73a053767&title=&width=1709)

```python
import unreal
actorsCount = int({actorsCount})
rotationStep = int({rotationStep})
positionOffset = {positionOffset}
slowTaskDisplayText = "Spawning actors in the level...."
selectedAssets = unreal.EditorUtilityLibrary.get_selected_assets()
with unreal.ScopedSlowTask(actorsCount, slowTaskDisplayText) as ST:
    ST.make_dialog(True)
    for i in range(actorsCount):
        if ST.should_cancel():
            break
        unreal.EditorLevelLibrary.spawn_actor_from_object(selectedAssets[0],unreal.Vector(positionOffset * i, positionOffset * i, 30.0), unreal.Rotator(0.0, 0.0, rotationStep * i))
        unreal.log("Just added an actor to the level!")
        ST.enter_progress_frame(1)
```
<a name="lh29O"></a>
## P19 清理动画序列的修改
清理动画序列的这些：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1663230536696-b7ad4db0-2360-4f31-9505-93e2de6ace26.png#clientId=ueac702c7-aad3-4&errorMessage=unknown%20error&from=paste&height=929&id=u5bcafe5b&originHeight=929&originWidth=1872&originalType=binary&ratio=1&rotation=0&showTitle=false&size=981489&status=error&style=none&taskId=u1201cab3-2bad-4287-8d1f-dcfeb4abae8&title=&width=1872)

```python
import unreal

selectedAssets = unreal.EditorUtilityLibrary.get_selected_assets()

for asset in selectedAssets:
    asset.modify(True)
    unreal.AnimationLibrary.remove_all_animation_notify_tracks(asset)

```
教程中使用的方式:<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1663230739632-4fbabd10-0237-4f9f-a0b6-6fc6f78ada35.png#clientId=ueac702c7-aad3-4&errorMessage=unknown%20error&from=paste&height=543&id=u262d67d0&originHeight=543&originWidth=782&originalType=binary&ratio=1&rotation=0&showTitle=false&size=174522&status=error&style=none&taskId=u33d17a86-ffd7-447c-806b-8d0b86506e7&title=&width=782)
<a name="PYMbD"></a>
## P20 清理未使用的资产
使用后将无法撤回，看看就好，并且如果资产过多会直接崩溃。
```cpp
import unreal

workingPath = "/Game"

allAssets = unreal.EditorAssetLibrary.list_assets(workingPath)

processingAssetPath = ""
allAssetsCount = len(allAssets)

if (allAssetsCount > 0):
    with unreal.ScopedSlowTask(allAssetsCount, processingAssetPath) as ST:
        ST.make_dialog(True)
        for asset in allAssets:
            processingAssetPath = asset
            deps = unreal.EditorAssetLibrary.find_package_referencers_for_asset(asset)  # 寻找资产的依赖项
            if (len(deps)<=0):
                unreal.log(">>>>>> Deleteing >>>>> %s" % asset)
                unreal.EditorAssetLibrary.delete_asset(asset)
            if ST.should_cancel():
                break
            ST.enter_progress_frame(1, processingAssetPath)
```
<a name="ZMWsY"></a>
## P21 批量创建材质实例
这里值得注意的是，使用get_path_name得到的是path.name格式的字符串，因此如果仅仅需要path则需要替换字符串。
```cpp
import unreal

totalRequiredInstances = 15

newAssetName = ""
sourceAssetPath = ""
createdAssetsPath = ""

selectedAssets = unreal.EditorUtilityLibrary.get_selected_assets()

factor = unreal.MaterialInstanceConstantFactoryNew()

assetTools = unreal.AssetToolsHelpers.get_asset_tools()

for selectedAsset in selectedAssets:
    newAssetName = selectedAsset.get_name() + "_%s_%d"
    sourceAssetPath = selectedAsset.get_path_name()  # /Game/MyTools/NewMaterial.NewMaterial
    createdAssetsPath = sourceAssetPath.replace(selectedAsset.get_name(), "-")  # /Game/MyTools/-.-
    createdAssetsPath = createdAssetsPath.replace("-.-", "")  # /Game/MyTools/

    for x in range(totalRequiredInstances):
        newAsset = assetTools.create_asset(newAssetName % ("inst", x + 1), createdAssetsPath, None, factor)
        unreal.MaterialEditingLibrary.set_material_instance_parent(newAsset, selectedAsset)

```


