---
title: UE开发总结
tags: UE开发
categories: UE开发
abbrlink: 7b04b356
date: 2023-10-20 14:30:00
---
# 一些名词解释
actor: level中的所有物体都可以称为actor
asset: contentBrowser中的所有物体都可以称为asset
assetName:     SM_Ramp
objectPath:    /Game/LevelPrototyping/Meshes/SM_Ramp.SM_Ramp
packageName:   /Game/LevelPrototyping/Meshes/SM_Ramp
packagePath:   /Game/LevelPrototyping/Meshes/
referencePath: /Script/Engine.StaticMesh'/Game/LevelPrototyping/Meshes/SM_Ramp.SM_Ramp' (左边是Class,右边是objectPath)
property: 对象的属性名,pythonAPI的文档中凡是带有property提示的属性都可以直接通过obj.propertyName的形式来读取,不带的就只能通过get_editor_property方法来读了.
staticMesh对应的lod所对应的sections: sections是静态网格体对应的lod对应的网格体组成数量,因为静态网格体可能会是由多个网格组成的,因此有了sections这个名词.通常和id数相同.



# 各个对象通用的方法
get_calss: 得到对应类
get_name: 得到AssetName
get_editor_property: 提供属性名,得到编辑器上显示的属性值
get_path_name: 得到objectPath

# unreal自身的方法
load_asset: 提供Asset的objectPath或者packageName,然后将得到对应Asset类型的对象.
get_editor_subsystem: 提供EditorActorSubsystem的引用(就像这样:unreal.EditorActorSubsystem),然后就能得到EditorActorSubsystem的对象.
log:将给定的参数作为信息记录在LogPython类别中
log_error:将给定的参数记录为LogPython类别中的错误
log_warning: 将给定的参数作为警告记录在LogPython类别中

# 没有模块
ScopedSlowTask: 用于制作进度条.
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
# ToolMenus模块
## ToolMenus
get: 得到ToolMenus类型的对象

# CoreUObject模块
## AssetData
**属性:**
asset_class: assetData对象所对应的类名,举例:StaticMesh(已知UE5.3已经弃用)
asset_class_path: 返回的类型为TopLevelAssetPath,这个类型有一个asset_name属性可以得到类名(作为asset_class的替代)

**方法:**
get_asset: 得到assetData对应的Asset对象

# Engine模块
## StaticMeshActor
**属性:**
static_mesh_component: 得到staticMesh组件,类型为StaticMeshComponent

## StaticMeshComponent
**属性:**
static_mesh 得到静态网格体对象,类型为StaticMesh

**方法:**
get_num_materials: 得到材质的数量(这个方法是PrimitiveComponent的方法,但是StaticMeshComponent继承自它,因此可以使用)
set_material: 设置材质,需要提供序号(int)和材质实例的对象(MaterialInterface),这个方法同样是PrimitiveComponent的方法

## StaticMesh
**属性:**
asset_import_data: 导入网格体时的数据和选项,返回对象类型为AssetImportData
lod_group: 网格体的lod组,返回类型为Name

**方法:**
get_num_lods: 得到静态网个体的lod数量,返回类型为int
get_num_sections: 提供lod序号(int值),得到网格体对应lod的对应分段数,分段数是指网格对应lod对应的

## AssetImportData
**属性:**
extract_filenames: 得到资产导入时的路径,类型为字符串数组

**方法:**
get_export_text_name: 提供packageName得到其所对应的referencePath
get_asset: 得到assetData对应的asset对象

# EditorScriptingUtilities模块
## EditorAssetLibrary
> 此类提供针对内容浏览器的资产的相关方法

**方法:**
list_assets: 提供文件夹路径然后得到文件夹路径下的所有objectPath
find_asset_data: 接收资产路径得到assetData(这个资产路径需要是packageName而不是objectPath)
duplicate_directory:接收两个packagePath,将第一个文件夹复制一份来得到第二个文件夹
delete_directory: 接收一个packagePath,删除文件夹
rename_directory: 接收两个packagePath,重命名文件夹
duplicate_asset: 接收两个packageName,将第一个Asset复制一份来得到第二个Asset
delete_asset: 接收一个packageName,删除对应asset
does_asset_exist: 接收一个packageName,检测对应Asset是否存在,返回布尔值
rename_asset: 接收两个packageName,重命名Asset
save_loaded_asset: 接收一个asset对象,用于保存
find_package_referencers_for_asset: 提供一个asset的packageName,然后得到其引用项的packageName的数组

## EditorLevelLibrary
> 此模块在4.27中可以使用,但是在UE5以后将要废弃,改用EditorActorSubsystem

**方法:**
get_all_level_actors : 获取关卡中的所有Actor
spawn_actor_from_object: 生成一个Actor到关卡中,需要提供Object,Vector,Rotator.

# MaterialEditor模块
## MaterialEditingLibrary
set_material_instance_texture_parameter_value:设置材质实例的贴图纹理参数,需提供MaterialInstanceConstant类型的材质实例,Name类型的材质参数的名字,Texture类型的值.**注意:通过代码设置参数不能够在编辑器中实时看到,需要关闭编辑器然后打开才行.**
set_material_instance_static_switch_parameter_value: 设置材质实例的贴图纹理参数是否启用,需提供MaterialInstanceConstant类型的材质实例,Name类型的材质参数的名字,Texture类型的值.

# Blutility模块
## EditorUtilityLibrary
> 此类提供针对内容浏览器的相关方法

**方法:**
get_selected_assets: 得到内容浏览器种所选择的资产

# UnrealEd模块
## EditorActorSubsystem
> 此类提供针对关卡中的Actor的方法,在UE5.3中更改了得到EditorActorSubsystem对象的方法,需要通过unreal.get_editor_subsystem(unreal.EditorActorSubsystem)来得到
举例:
EAS = unreal.get_editor_subsystem(unreal.EditorActorSubsystem)
all_actors = EAS.get_all_level_actors()

**方法:**
get_all_level_actors: 获取关卡中的所有Actor

## AssetImportTask
> 资产导入的任务,包含了资产导入时的相关数据设置,**只有属性,没有方法**

**属性:**
automated: 布尔类型,设置为True时,不会弹出对话框
destination_name: 字符串类型,用来定义资产导入时的名称,当为空字符串时导入的资产以文件名称命名
destination_path: 字符串类型,用于设置导入的资产在引擎中的路径
filename: 字符串类型,导入的资产在本地硬盘上的的**路径**
replace_existing: 布尔类型,导入的资产是否强制覆盖引擎已有资产
save: 布尔类型,导入资产后是否自动保存
imported_object_paths: 字符串数组类型,导入后的路径

## FbxImportUI
**属性:**
import_mesh: 布尔类型,是否导入mesh
import_textures : 布尔类型,是否导入贴图
import_materials: 布尔类型,如果没有找到对应的相关材质,是否自动创建材质球
import_as_skeletal: 布尔类型,是否将FBX作为骨架对象导入
import_animations: 布尔类型,是否导入动画
static_mesh_import_data:  FbxStaticMeshImportData类型,导入静态网格体时使用的数据
skeletal_mesh_import_data: FbxSkeletalMeshImportData类型,导入骨架网格体时使用的数据
anim_sequence_import_data: FbxAnimSequenceImportData类型,导入动画时使用的数据
skeleton: Skeleton类型,导入动画时,需要指定骨架

## FbxStaticMeshImportData
**属性:**
import_translation: Vector类型,导入时的位移
import_rotation: Rotator类型,导入时的旋转
import_uniform_scale: float类型,导入时的统一缩放值
combine_meshes: 布尔类型,导入时是否将多个mesh合并成一个mesh
generate_lightmap_u_vs: 布尔类型,是否生成用于光照贴图的UV
auto_generate_collision: 布尔类型,是否自动生成碰撞

## FbxSkeletalMeshImportData
**属性:**
import_translation: Vector类型,导入时的位移
import_rotation: Rotator类型,导入时的旋转
import_uniform_scale: float类型,导入时的统一缩放值
import_morph_targets: 布尔类型,是否导入变形目标(blendshape)
update_skeleton_reference_pose: 布尔类型,是否导入的时候更新骨架参考姿势

## anim_sequence_import_data
**属性:**
import_translation: Vector类型,导入时的位移
import_rotation: Rotator类型,导入时的旋转
import_uniform_scale: float类型,导入时的统一缩放值
animation_length: FBXAnimationLengthImportType类型,导入动画的长度,有FBXALIT_ANIMATED_KEY,FBXALIT_EXPORTED_TIME,FBXALIT_SET_RANGE三种长度类型,具体见:[FBXAnimationLengthImportType](https://docs.unrealengine.com/5.3/en-US/PythonAPI/class/FBXAnimationLengthImportType.html#unreal.FBXAnimationLengthImportType)
remove_redundant_keys: 布尔类型,是否删除冗余帧

## MaterialFactoryNew
用于创建一个用于Material工厂对象,用在assetTool的createAsset上面

## WorldFactory
用于创建一个World工厂对象,用在assetTool的createAsset上面

## ParticleSystemFactoryNew
用于创建一个Particle System工厂对象,用在assetTool的createAsset上面

## BlueprintFactory
用于创建一个Blueprint工厂对象,用在assetTool的createAsset上面

## MaterialInstanceConstantFactoryNew
用于创建一个材质实例工厂对象


# ProceduralMeshComponent模块
## ProceduralMeshLibrary
**方法:**
get_section_from_static_mesh: 提供StaticMesh对象,lod索引,section索引得到对应的section的几何数据(vertices,triangles,normals,u_vs,tangents).

# AssetTools模块
## AssetToolsHelpers
> 只有一个作用,就是通过get_asset_tools方法得到AssetTools

get_asset_tools: 得到AssetTools类型对象

## AssetTools
> AssetTools模块提供了针对Asset的一些功能,例如导入,导出,创建,复制,打开

**方法:**
import_asset_tasks: 根据提供的AssetImportTask类型的对象的数组,进行导入资产操作.
duplicate_asset_with_dialog: 复制资产并带有对话框,提供三个参数,第一个是新复制出来的资产的AssetName,第二个是新复制出来的资产的PackageName,第三个是源资产的**object**,可以通过unreal.load_asset来得到对应Asset对象.
duplicate_asset: 复制资产但不带有对话框,参数跟duplicate_asset_with_dialog相同
rename_assets_with_dialog: 提供AssetRenameData类型的数据,批量对AssetRenameData中的数据进行重命名.
rename_assets: 不显示对话框的情况下重命名一组资产,与rename_assets_with_dialog使用方法相同
open_editor_for_assets: 提供Asset对象,从编辑器中打开对应资产
create_asset: 提供asset_name,package_path,asset_class,factory,创建Asset



## AssetRenameData
在使用AssetTools类中的rename_assets_with_dialog与rename_assets时需要.
通过unreal.AssetRenameData(source_object,new_package_path,new_asset_name)来创建一个AssetRenameData对象.
source_object为原资产的对象,new_package_path为新资产的文件夹路径,new_asset_name为新资产的名字.

# LevelSequenceEditor模块
## LevelSequenceFactoryNew
用于创建一个用于ULevelSequence的工厂对象,用在assetTool的createAsset上面

# Paper2DEditor模块
## PaperFlipbookFactory
用于创建flipbooks的工厂对象,用在assetTool的createAsset上面