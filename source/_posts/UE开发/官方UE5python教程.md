---
title: 官方UE5python教程
tags: UEPython
categories: UE开发
abbrlink: e897646c
date: 2023-08-29 03:57:00
---
<meta name="referrer" content="no-referrer" />
<a name="LHv42"></a>

# 官网PythonAPI教程
教程链接[https://dev.epicgames.com/community/learning/courses/wk4/an-in-depth-look-at-using-python-for-game-development/vymW/an-in-depth-look-at-using-python-for-game-development-introduction](https://dev.epicgames.com/community/learning/courses/wk4/an-in-depth-look-at-using-python-for-game-development/vymW/an-in-depth-look-at-using-python-for-game-development-introduction)
<a name="QOSV4"></a>
## 获得路径下的所有文件路径
def listAssetPaths(path='/Game'):<br />    assetPaths = unreal.EditorAssetLibrary.list_assets(path)<br />    for assetPath in assetPaths: print(assetPath)
<a name="nDCRa"></a>
## EditorUtilityLibrary和EditorActorSubsystem
EditorUtilityLibrary可以让我们获取和内容浏览器有关的功能<br />EditorActorSubsystem可以可以提供和世界大纲视图有关的功能（这个类在UE5里面有，UE4.27里面没有）<br />EditorLevelLibrary 和 EditorActorSubsystem具有差不多的功能，UE4.27可以用这个来尝试代替EditorActorSubsystem
<a name="fwq2A"></a>
### EditorUtilityLibrary
方法：get_selected_assets (获取选择的资产)<br />举例：<br /># 输出选择的资产的对象信息<br />def getSelectionContentBrowser():<br />    selectAssets = unreal.EditorUtilityLibrary.get_selected_assets()<br />    for selectAsset in selectAssets: print(selectAsset)
<a name="DN8Px"></a>
### EditorActorSubsystem（这个类在UE5里面有，UE4.27里面没有）
方法：<br />get_all_level_actors(获取关卡中的所有ACtor)  ![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1659084287467-26cef784-fa57-4d54-8cc8-1aa7956ac394.png#clientId=u8fad6bab-0b86-4&from=paste&height=170&id=u128d9fb9&originHeight=170&originWidth=1099&originalType=binary&ratio=1&rotation=0&showTitle=false&size=94871&status=done&style=none&taskId=ua1a325d8-2de6-4628-9b27-3a4fc16920b&title=&width=1099)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1659084800653-dfeca916-20c0-4f22-9ce7-3180eddab54a.png#clientId=u8fad6bab-0b86-4&from=paste&height=173&id=u345728e2&originHeight=173&originWidth=1506&originalType=binary&ratio=1&rotation=0&showTitle=false&size=110930&status=done&style=none&taskId=ucbb5a5f7-6189-4bcf-94e9-bff659c4f5b&title=&width=1506)  EAS是变量名无需深究

get_selected_level_actors(获取选择的关卡actor)
<a name="zgiY2"></a>
### EditorLevelLibrary（4.27可以使用的和EditorActorSubSystem差不多功能的类）（UE5虽然也能使用但是将要废弃这个类）
方法：get_all_level_actors(获取关卡中的所有ACtor)  同样是获取关卡中的所有ACtor经过测试4.27版本的UE使用这个类是不需要参数传递的，EditorActorSubsystem的这个方法需要传递参数。
<a name="Himck"></a>
## 按类组织资产
<a name="UTtHB"></a>
### EditorAssetLibrary
方法：find_asset_data(asset_path)→AssetData   接受资产路径返回资产的数据，类型为AssetData。什么是AssetData类型：AssetData类型存取了资产的各种信息，可以直接print AssetData类型的变量可以发现它是一个字典。这个类型也自带一些方法，比如获取资产的名字，长名，资产的类型，判断是否加载等。[https://docs.unrealengine.com/4.27/en-US/PythonAPI/class/AssetData.html#unreal.AssetData](https://docs.unrealengine.com/4.27/en-US/PythonAPI/class/AssetData.html#unreal.AssetData)
```python
# 根据类型列举物体
def getAssetClass(classType):
    assetPaths = unreal.EditorAssetLibrary.list_assets('/Game/MyAsset')
    print(assetPaths)
    assets = []
    for assetPath in assetPaths:
        assetData = unreal.EditorAssetLibrary.find_asset_data(assetPath)
        assetClass = assetData.asset_class
        if assetClass == classType:
            assets.append(assetData.get_export_text_name())
    for asset in assets: print(asset)
```
<a name="YUoDU"></a>
## 获取特定类的信息
首先看到这一节可以明确的感知到，UEPython中有很多自定义的类型，然后这些类型都有属于自己的函数，因此帮助文档很重要。<br />staticMesh，![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1659319581581-f014ee27-7437-4f39-82d5-d7baa423fc60.png#clientId=udfa48b04-83fd-4&from=paste&height=829&id=u7b24a215&originHeight=829&originWidth=1141&originalType=binary&ratio=1&rotation=0&showTitle=false&size=835848&status=done&style=none&taskId=ue86b33e8-7ec2-4636-8a0b-aecb69c38d7&title=&width=1141)编辑器属性就是这种类型的可调节的属性，我们可以通过staticMesh类型的对象中的get_editor_property方法来获取这些属性<br />它们都继承自_ObjectBase![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1659319635544-9dbd8ad7-1777-45b5-9743-5bf5798f49da.png#clientId=udfa48b04-83fd-4&from=paste&height=566&id=ua3616151&originHeight=566&originWidth=1217&originalType=binary&ratio=1&rotation=0&showTitle=false&size=331996&status=done&style=none&taskId=ud882f472-031f-49ec-b64d-e408fefff7d&title=&width=1217)所以对象也可以使用这些方法，例如get_name

<a name="Naaq6"></a>
### StaticMesh的AssetImportData与lod_group属性
```python
# 根据类型列举物体
def getAssetClass(classType):
    assetPaths = unreal.EditorAssetLibrary.list_assets('/Game')
    # print(assetPaths)
    assets = []
    for assetPath in assetPaths:
        assetData = unreal.EditorAssetLibrary.find_asset_data(assetPath)
        assetClass = assetData.asset_class
        if assetClass == classType:
            assets.append(assetData.get_asset())
    # for asset in assets: print(asset)
    return assets


# 获取静态网格体的信息
def getStaticMeshData():
    staticMeshs = getAssetClass('StaticMesh')  # 获取所有类型为StaticMesh的对象
    for staticMesh in staticMeshs:
        # assetImportData = staticMesh.get_editor_property('asset_import_data')  # 获取静态网格体对象的编辑器中的导入信息的属性
        # fbxFilePath = assetImportData.extract_filenames()  # 得到导入信息属性中的fbx路径
        # print(fbxFilePath)
        # print(staticMesh.get_editor_property('lod_group'))
        # print(staticMesh.get_num_lods())
        # 如果静态网个体对象的lod组的属性为None并且lod数量只有一个时将lod组的属性改为LargeProp
        if staticMesh.get_editor_property('lod_group') == 'None':  
            if staticMesh.get_num_lods() == 1:
                staticMesh.set_editor_property('lod_group', 'LargeProp')
```
<a name="MDGTB"></a>
## 获取staticMesh的lod数据
先提一下名词解释，这里使用的方法除了利用了lod的索引外还利用了分段的索引，通过观看教程理解分段的意义：首先我们的目的是获取这里模型的三角形的数量![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1659333726131-b93a1f65-9139-48dc-b96f-22467c908786.png#clientId=u061bcdf3-168e-4&from=paste&height=164&id=u8c1da1d1&originHeight=164&originWidth=340&originalType=binary&ratio=1&rotation=0&showTitle=false&size=50872&status=done&style=none&taskId=u8c0d6aea-b569-4a81-8d54-bea8b6511dd&title=&width=340)，当切换一个LOD时分段数量跟材质球的数量是相同的，也就是说分段的意思是当前LOD对应的模型的组成数量。![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1659333895148-76182373-68d5-49fe-b9c8-04b6dd1f395f.png#clientId=u061bcdf3-168e-4&from=paste&height=574&id=uf15cd6ae&originHeight=574&originWidth=1414&originalType=binary&ratio=1&rotation=0&showTitle=false&size=756463&status=done&style=none&taskId=uec2be367-4886-4f68-89d8-c818ac4af7a&title=&width=1414)<br />涉及到的类与方法：<br />ProceduralMeshLibrary:get_section_from_static_mesh![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1659333594626-58600156-f861-4320-b964-3450ce611c1c.png#clientId=u061bcdf3-168e-4&from=paste&height=292&id=u2c801b66&originHeight=292&originWidth=802&originalType=binary&ratio=1&rotation=0&showTitle=false&size=34735&status=done&style=none&taskId=u826093ec-2f28-4aeb-9d33-02d08cb55db&title=&width=802)[https://docs.unrealengine.com/4.27/en-US/PythonAPI/class/ProceduralMeshLibrary.html?highlight=proceduralmeshlibrary#unreal.ProceduralMeshLibrary](https://docs.unrealengine.com/4.27/en-US/PythonAPI/class/ProceduralMeshLibrary.html?highlight=proceduralmeshlibrary#unreal.ProceduralMeshLibrary)<br />得到的数据经过输出可以看出来得到的是一个元组，元组里面有多个数组元素组成，有意向可以遍历这些数组来观察数组中的内容。因为我们需要得到三角形的数量遍历三角形的数据后发现官方输出了很多重复的数据，当我们把数组的长度除以3以后才能够得到我们需要的正确的三角形的数量。<br />“很多数值是重复的 我想这是因为输出了 和每个三角形有关的所有顶点 之所以这么认为是因为 如果让这个数字 这个长度 我们可以生成它 然后除以3 得到的结果 就是我们想要的数据 这是个窍门 只是个小窍门 只要让这个数组的长度除以3”这是官方教程的原话

![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1659335064023-274d427c-338b-4f40-b02c-a491dfa0f306.png#clientId=u061bcdf3-168e-4&from=paste&height=145&id=ua07f9194&originHeight=145&originWidth=1483&originalType=binary&ratio=1&rotation=0&showTitle=false&size=54381&status=done&style=none&taskId=u668471d1-fcb7-41d2-992c-37dcd0eb4a6&title=&width=1483)<br />StaticMesh: get_num_sections(lod)得到模型的lod对应的分段数[https://docs.unrealengine.com/4.27/en-US/PythonAPI/class/StaticMesh.html?highlight=staticmesh#unreal.StaticMesh.get_num_sections](https://docs.unrealengine.com/4.27/en-US/PythonAPI/class/StaticMesh.html?highlight=staticmesh#unreal.StaticMesh.get_num_sections)
```python
# 根据类型列举物体
def getAssetClass(classType):
    assetPaths = unreal.EditorAssetLibrary.list_assets('/Game')
    # print(assetPaths)
    assets = []
    for assetPath in assetPaths:
        assetData = unreal.EditorAssetLibrary.find_asset_data(assetPath)
        assetClass = assetData.asset_class
        if assetClass == classType:
            assets.append(assetData.get_asset())
    # for asset in assets: print(asset)
    return assets

# 获取静态网格体的lod信息
def getStaticMeshLODData():
    staticMeshs = getAssetClass('StaticMesh')
    for staticMesh in staticMeshs:
        staticMeshTriCount = []  # 负责记录模型的三角形数量
        numLODs = staticMesh.get_num_lods()
        for i in range(numLODs):
            LODTriCount = 0  # 记录当前LOD的三角形数量
            numSections = staticMesh.get_num_sections(i)
            for j in range(numSections):  # 遍历LOD对应的分段得到LOD对应的三角形数量
                # 得到静态网格体对应的分段信息
                sectionData = unreal.ProceduralMeshLibrary.get_section_from_static_mesh(staticMesh, i, j)
                sectionTriCount = (len(sectionData[1]) / 3)  # 把数组的长度除以3以后才能够得到我们需要的正确的三角形的数量。
                LODTriCount += sectionTriCount
            staticMeshTriCount.append(LODTriCount)  # 记录LOD对应的三角形数量
        staticMeshReductions = [100] # 负责记录模型的LOD对应的三角形百分比
        for i in range(1, numLODs):
            staticMeshReductions.append(int(staticMeshTriCount[i]/staticMeshTriCount[0]*100))
        print(staticMesh.get_name())
        print(staticMeshTriCount)
        print(staticMeshReductions)
```
<a name="d3ZVW"></a>
## 获取关卡中的模型以及出现的数量
因为是要获取实例化的数量也即获取关卡中存在的Actor，因此要使用EditorLevelLibrary中的方法<br />在这里获得到了个小知识点，![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1659411906430-17ee0b86-6584-4501-9741-c49697d67a53.png#clientId=u0faa6e17-c546-4&from=paste&height=109&id=u5b3be5bc&originHeight=109&originWidth=581&originalType=binary&ratio=1&rotation=0&showTitle=false&size=22409&status=done&style=none&taskId=uc4643842-8510-4db1-8fb4-5b3347b3ffd&title=&width=581)当我们将内容浏览器中的资产拖入到关卡中，ue会自动将其变成staticMeshActor类型，因此找到关卡中出现的Actor以后还需要找到这个Acotr对应的组件，然后再根据组件找到对应的静态网格体。
```python
# 获取关卡中的模型以及出现的次数
def getStaticMeshInstanceCounts():
    levelActors = unreal.EditorLevelLibrary().get_all_level_actors()  # 获取关卡中的所有Actor

    staticMeshActors = []  # 负责记录所有staticMeshActor的名字
    staticMeshActorCounts = []  # 负责记录所有Actor在关卡中出现的数量

    for levelActor in levelActors:
        if (levelActor.get_class().get_name()) == 'StaticMeshActor':
            staticMeshComponent = levelActor.static_mesh_component  # 得到这个Actor的组件
            staticMesh = staticMeshComponent.static_mesh  # 得到这个组件对应的静态网格体
            staticMeshActors.append(staticMesh.get_name())

    processedActors = []  # 用来记录场景中的所有staticMeshActor但是不会出现相同的名字
    for staticMeshActor in staticMeshActors:
        if staticMeshActor not in processedActors:
            actorCounts = (staticMeshActor, staticMeshActors.count(staticMeshActor))  # 元组，负责记录actor以及对应的关卡出现数量
            staticMeshActorCounts.append(actorCounts)
            processedActors.append(staticMeshActor)
    # key=lambda a: a[1]  的意思是按照列表中的元素中的第二项进行排列，在这里是按照actor出现的次数进行排序
    staticMeshActorCounts.sort(key=lambda a: a[1], reverse=True)
    for item in staticMeshActorCounts: print(item)
```
<a name="OVQyH"></a>
## LOD视图的开启与介绍
![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1659411854494-ea279754-5f26-4577-a656-800fc51c9852.png#clientId=u0faa6e17-c546-4&from=paste&height=546&id=u7fcc843f&originHeight=546&originWidth=1486&originalType=binary&ratio=1&rotation=0&showTitle=false&size=845097&status=done&style=none&taskId=u678fdc5d-9d6d-48b8-8d8b-d20c60ce339&title=&width=1486)<br />白色代表LOD0，红色代表LOD1，依次往后是绿色蓝色

<a name="mfxpo"></a>
## 获取关卡中的模型名字以及对应的在场景中的LOD1的三角形数量
```python
# 获取静态网格体的lod信息
def getStaticMeshLODData():
    staticMeshs = getAssetClass('StaticMesh')
    staticMeshLODData = []
    for staticMesh in staticMeshs:
        staticMeshTriCount = []  # 负责记录模型的三角形数量
        numLODs = staticMesh.get_num_lods()
        for i in range(numLODs):
            LODTriCount = 0  # 记录当前LOD的三角形数量
            numSections = staticMesh.get_num_sections(i)
            for j in range(numSections):  # 遍历LOD对应的分段得到LOD对应的三角形数量
                # 得到静态网格体对应的分段信息
                sectionData = unreal.ProceduralMeshLibrary.get_section_from_static_mesh(staticMesh, i, j)
                sectionTriCount = (len(sectionData[1]) / 3)  # 把数组的长度除以3以后才能够得到我们需要的正确的三角形的数量。
                LODTriCount += sectionTriCount
            staticMeshTriCount.append(LODTriCount)  # 记录LOD对应的三角形数量
        staticMeshReductions = [100]  # 负责记录模型的LOD对应的三角形百分比
        for i in range(1, numLODs):
            staticMeshReductions.append(int(staticMeshTriCount[i] / staticMeshTriCount[0] * 100))
        # print(staticMesh.get_name())
        # print(staticMeshTriCount)
        # print(staticMeshReductions)

        try:
            LODData = (staticMesh.get_name(), staticMeshTriCount[1])  # 之所以try是因为有的模型只有LOD0,把只有LOD0的过滤掉
        except:
            pass
        staticMeshLODData.append(LODData)
    return staticMeshLODData



# 获取关卡中的模型以及出现的次数
def getStaticMeshInstanceCounts():
    levelActors = unreal.EditorLevelLibrary().get_all_level_actors()  # 获取关卡中的所有Actor

    staticMeshActors = []  # 负责记录所有staticMeshActor的名字
    staticMeshActorCounts = []  # 负责记录所有Actor在关卡中出现的数量

    for levelActor in levelActors:
        if (levelActor.get_class().get_name()) == 'StaticMeshActor':
            staticMeshComponent = levelActor.static_mesh_component  # 得到这个Actor的组件
            staticMesh = staticMeshComponent.static_mesh  # 得到这个组件对应的静态网格体
            staticMeshActors.append(staticMesh.get_name())

    processedActors = []  # 用来记录场景中的所有staticMeshActor但是不会出现相同的名字
    for staticMeshActor in staticMeshActors:
        if staticMeshActor not in processedActors:
            actorCounts = (staticMeshActor, staticMeshActors.count(staticMeshActor))  # 元组，负责记录actor以及对应的关卡出现数量
            staticMeshActorCounts.append(actorCounts)
            processedActors.append(staticMeshActor)
    # key=lambda a: a[1]  的意思是按照列表中的元素中的第二项进行排列，在这里是按照actor出现的次数进行排序
    staticMeshActorCounts.sort(key=lambda a: a[1], reverse=True)
    # for item in staticMeshActorCounts: print(item)

    LODData = getStaticMeshLODData()

    # for item in LODData: print(item)

    aggregateTriCounts = []

    for i in range(len(staticMeshActorCounts)):
        for j in range(len(LODData)):
            if staticMeshActorCounts[i][0] == LODData[j][0]:
                aggregateTriCount = (staticMeshActorCounts[i][0],staticMeshActorCounts[i][1] * LODData[j][1])
                aggregateTriCounts.append(aggregateTriCount)

    aggregateTriCounts.sort(key=lambda a: a[1], reverse=True)  # 存取场景中的actor的mesh名字以及对应的场景中的所有mesh的LOD1的三角形数量
    for item in aggregateTriCounts: print(item)

```
<a name="aFWsp"></a>
## dir()与help()，材质实例
当知道一个类的名字以后，如果想要得到这个类对应的所有方法，可以通过dir()函数来得到，并且有的方法官方文档可能没有。<br />例如如果想知道StaticMeshComponent的方法可以通过：<br />for item in dir(unreal.StaticMeshComponent): print (item)<br />得到类对应的所有方法，并且可以通过搜索得到对应的方法，知道方法的名字后可以使用help()函数来得到方法的细节：help(unreal.StaticMeshComponent.get_num_materials)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1661837162153-7f3ce4f5-898a-4cfa-b9b4-edcf8d6d1ad8.png#clientId=u12196a95-624c-4&from=paste&height=719&id=udf236356&originHeight=719&originWidth=490&originalType=binary&ratio=1&rotation=0&showTitle=false&size=31349&status=done&style=none&taskId=u7d0944a4-abd2-4d3e-81d1-b68722fd1f9&title=&width=490)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1661837204405-a5c9f43a-a01c-48a8-9c60-596eac11bb39.png#clientId=u12196a95-624c-4&from=paste&height=322&id=ubcfb26de&originHeight=322&originWidth=611&originalType=binary&ratio=1&rotation=0&showTitle=false&size=49628&status=done&style=none&taskId=u16026c1d-52ea-4f44-bc33-1b56414123b&title=&width=611)![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1661837351487-3280c32f-1feb-49bb-8055-80d26ac7d865.png#clientId=u12196a95-624c-4&from=paste&height=88&id=u3bd793ef&originHeight=88&originWidth=481&originalType=binary&ratio=1&rotation=0&showTitle=false&size=10778&status=done&style=none&taskId=ud66a72e0-288c-4bfc-9949-898bdd5e323&title=&width=481)<br />将场景中的所有模型的材质更改为/Game/python/MI_test这个材质实例<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1661838603634-35cbd362-12e3-4908-83e7-1f54783a6f72.png#clientId=u12196a95-624c-4&from=paste&height=637&id=u456e4338&originHeight=637&originWidth=1337&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1314449&status=done&style=none&taskId=u69fc4f34-9d6b-4779-9b6d-59b33d9fb2f&title=&width=1337)
```cpp
def returnMaterialInformationSMC():

    levelActors = unreal.EditorLevelLibrary().get_all_level_actors()
    testMat = unreal.EditorAssetLibrary.find_asset_data('/Game/python/MI_test').get_asset()

    for levelActor in levelActors:
        if (levelActor.get_class().get_name()) == 'StaticMeshActor':
            staticMeshComponent = levelActor.static_mesh_component

            for i in range(staticMeshComponent.get_num_materials()):
                staticMeshComponent.set_material(i, testMat)
```
<a name="hfBFP"></a>
## 使用关卡蓝图更改模型材质
根据场景中的staticmesh的material数量决定使用不同的材质实例，只在运行游戏时启用。<br />![Northwood-EventGraph.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1661843448805-260ec193-cd73-4fd1-9c12-601af3fa30cc.png#clientId=u12196a95-624c-4&from=paste&height=1410&id=u739a9ddf&originHeight=1410&originWidth=2701&originalType=binary&ratio=1&rotation=0&showTitle=false&size=680063&status=done&style=none&taskId=ub1dbbe98-555a-43d7-971f-13c89b67a0e&title=&width=2701)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/2623605/1661843508233-41e09606-7efb-463d-86fe-20c5fb196f0c.png#clientId=u12196a95-624c-4&from=paste&height=906&id=u2b8c6d2f&originHeight=906&originWidth=1684&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2535471&status=done&style=none&taskId=udab98c93-ba35-4bd0-85c7-d61b8e17ec4&title=&width=1684)
