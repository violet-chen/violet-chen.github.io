---
title: UEC++Plugin
tags: UEC++
categories: UE开发
abbrlink: cb44a3cb
date: 2023-09-19 10:23:00
---

---
# 关于有讨论的UE5.2右键不显示脚本化资本行为的解决办法

![Alt text](image-16.png)
**解决办法:**
首先在内容管理器里创建两个蓝图类,分别继承的父类选择AssetActionUtility,和自己创建的继承AssetActionUtility的C++类,然后再创建一个编辑器工具蓝图继承AssetActionUtility(如果不行就继承自己创建的类)
然后自己创建的C++类就会出现在脚本化资本行为里面了.
**过程截图:**
![Alt text](image-19.png)

---
# VS与UE进行实时编码的过程
在VS里面敲好代码以后,运行调试后会弹出UE编辑器,然后通过UE编辑器可以进行代码功能的验证,但是如果验证过程中发现了需要修改代码的情况时,不需要关闭UE编辑器再进行代码修改然后再次调试.**VS与UE是可以进行实时编码的**
例如当调试代码发现有问题时,可以直接在VS里面进行代码修改,修改完成以后按ctrl+shift+s保存代码的修改,然后按ctrl+alt+F11即可完成代码修改与UE编辑器的实时连接.然后再次对功能进行调试即可.

---
# module模块的介绍
> 官网的解释:
<https://docs.unrealengine.com/5.2/zh-CN/unreal-engine-modules/>
<https://docs.unrealengine.com/5.3/zh-CN/module-properties-in-unreal-engine/>

总结而讲就是:
- 模块实现了良好的代码分离
- 模块都需要一个[模块名]Build.cs的构建文件.
- 外部的模块的包含是通过加入到Build.cs文件来实现的,加入到Build.cs后就可以通过头文件来包含.

---
# 创建一个空的针对editor的plugin
点击创建后即可在VS里面创建相关plugin文件.
![Alt text](image.png)
![Alt text](image-1.png)

---
修改Plugin的设置:
双击进入SuperManager.uplugin文件
![Alt text](image-2.png)

---
修改其中的模块的类型和加载阶段
修改类型为Editor意思是它不会对游戏模块产生影响,它是针对编辑器的.
修改加载阶段为PreDefault意思是它会在游戏模块之前加载.
![Alt text](image-3.png)

---
# plugin内容的简介
**plugin类型:**
plugin分为针对Asset的和针对Acotr的.
Asset意思是在(Content Browser)内容浏览器里面的资产
Actor意思是在关卡里面放置的资产
要创建针对Asset的插件就需要继承AssetActionUtility类
要创建针对Actor的插件就需要继承ActorActionUtility类
**plugin相关的宏:**
UFUNCTION(CallInEditor),加入这个宏以后,当我们右键单击资产时,将添加一个按钮,我们可以使用这个按钮来触发自定义编辑器的功能.通过这个宏可以节省自己注册所有菜单项的所有时间和麻烦.

---
# 为刚才的Plugin添加一个向屏幕打印debug信息的功能
首先为刚才创建的空Plugin(自定义的名字叫SuperManager)创建一个类,并且选择继承AssetActionUtility
![Alt text](image-4.png)
![Alt text](image-5.png)
![Alt text](image-6.png)

---
创建好以后在VS中会生成如下结构:
![Alt text](image-7.png)
QuickAssetAction本身具备一定量的初始代码,在其基础上添加新的功能.
由于是继承UAssetActionUtility,因此包含了头文件,需要知道其位置在哪里,不然无法编译.
## 寻找UAssetActionUtility头文件的位置
首先在解决方案资源管理器中搜索AssetActionUtility的位置,由下图可以得知它是属于Blutility模块的,在PublicDependencyModuleNames中添加Blutility进行生成,生成时发现依然不成功,那么就代表它是一个私有的路径,因此需要在PrivateIncludePaths中添加它的详细路径
![Alt text](image-9.png)
也可以通过番茄助手使用alt+shift+o来进行搜索得到路径.
![Alt text](image-11.png)
因此在SuperManager.Build.cs文件中的PrivateIncludePaths与PublicDependencyModuleNames添加一些代码:
## SuperManager.Build.cs
```cpp
PrivateIncludePaths.AddRange(
    new string[] {
        System.IO.Path.GetFullPath(Target.RelativeEnginePath) + "/Source/Editor/Blutility/Private"
        // ... add other private include paths required here ...
    }
    );
PublicDependencyModuleNames.AddRange(
    new string[]
    {
        "Core","Blutility"
        // ... add other public dependencies that you statically link with here ...
    }
    );
```

## QuickAssetAction.h
```cpp
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "AssetActionUtility.h"
#include "QuickAssetAction.generated.h"

/**
 * 
 */
UCLASS()
class SUPERMANAGER_API UQuickAssetAction : public UAssetActionUtility
{
	GENERATED_BODY()
public:
	UFUNCTION(CallInEditor) //使用这个宏来让此函数能够在编辑器中访问
	void TestFunc();
	
};

```
## QuickAssetAction.cpp
```cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "AssetActions/QuickAssetAction.h"

void UQuickAssetAction::TestFunc()
{
	if(GEngine)
	{
		GEngine->AddOnScreenDebugMessage(-1, 8.0f, FColor::Cyan, TEXT("Working")); // 向屏幕打印信息
	}
}

```

---
# 创建负责方便调试的头文件
在plugin的新建的SuperManager功能的public文件夹下新建一个头文件
![Alt text](image-8.png)

---
新建头文件并写好代码以后,include这个头文件就可以使用头文件里定义的方法.
头文件代码如下:
```cpp
#pragma once

void Print(const FString& Message, const FColor& Color)
{
	if (GEngine)
	{
		GEngine->AddOnScreenDebugMessage(-1, 8.0f, Color, Message); // 向屏幕打印信息
	}
}

void PrintLog(const FString& Message)
{
	UE_LOG(LogTemp, Warning, TEXT("%s"), *Message); // 向日志打印信息
}
```

---
# 资产批量复制
**实现效果:**
![Alt text](image-13.png)
**用到的两个库以及对应的常用的函数:**
通过代码能够得知这几个静态函数的作用以及类型,其中FAssetData类型的数据比UObject*类型的数据包含的内容更多.
![Alt text](image-10.png)

---
**UE数据的一些名词解释:**

由图可知ObjectPath的结尾是BP_NewBlueprint.BP_NewBlueprint,是需要在AssetName的基础上多加一个AssetName的格式
除了AssetName和ObjectPath和PackagePath以外还有个叫PackageName
PackageName:/Game/MyFolder/BP_NewBlueprint
![Alt text](image-12.png)

---
## 代码编写
首先由于要使用UEditorUtilityLibrary和UEditorAssetLibrary,所以要包含这两个头文件,然后通过查询头文件路径可以得知需要额外包含的模块为EditorScriptingUtilities,因此在build.cs里面的PublicDependencyModuleNames中进行添加.
然后开始实现功能,从UE编辑器中接收一个int32类型的值,然后通过值的大小进行asset的复制粘贴,命名和保存.
```cpp
void UQuickAssetAction::DuplicateAssets(int32 NumOfDuplicates)
{
	if (NumOfDuplicates <= 0)
	{
		Print(TEXT("Please enter a VALID number"), FColor::Red);
		return;
	}
	
	const TArray<FAssetData> SelectedAssetsData = UEditorUtilityLibrary::GetSelectedAssetData();
	uint32 Counter = 0;
	for (const FAssetData& SelectedAssetData: SelectedAssetsData)
	{
		for (int32 i = 0; i < NumOfDuplicates; i++)
		{
			const FString SourceAssetPath = SelectedAssetData.ObjectPath.ToString();
			const FString NewDuplicatedAssetName = SelectedAssetData.AssetName.ToString() + TEXT("_") + FString::FromInt(i + 1);
			const FString NewPathName = FPaths::Combine(SelectedAssetData.PackagePath.ToString(), NewDuplicatedAssetName);
			if (UEditorAssetLibrary::DuplicateAsset(SourceAssetPath, NewPathName))
			{
				UEditorAssetLibrary::SaveAsset(NewPathName,false); // 保存复制的资产,false是指无论是否对资产进行了修改都保存
				++Counter;
			}
		}
	}

	if (Counter > 0)
	{
		Print(TEXT("Successfully duplicated " + FString::FromInt(Counter) + " files"), FColor::Green);
	}
}
```

---
# 消息框与通知框

## 消息框:
**需要包含头文件:** "Misc/MessageDialog.h"
```cpp
FText MsgTitle = FText::FromString(TEXT("Warning"));
FText WarningMsg = FText::FromString(TEXT("Please enter a VALID number"));
FMessageDialog::Open(EAppMsgType::Ok,WarningMsg, &MsgTitle);
```
![Alt text](image-14.png)
**可以把它写成函数:**
```cpp
EAppReturnType::Type ShowMsgDialog(EAppMsgType::Type MsgType, const FString& Message, bool bShowMsgAsWarning = true)
{
	if (bShowMsgAsWarning)
	{
		FText MsgTitle = FText::FromString(TEXT("Warning"));
		return FMessageDialog::Open(MsgType, FText::FromString(Message), &MsgTitle);
	}
	else
	{
		return FMessageDialog::Open(MsgType, FText::FromString(Message));
	}
}
```
**使用:**
ShowMsgDialog(EAppMsgType::Ok, TEXT("Please enter a VALID number"));

---
## 通知框(右下角弹出):
**用到的头文件:**
"Widgets/Notifications/SNotificationList.h"
"Framework/Notifications/NotificationManager.h"
**写成自定义函数:**
```cpp
void ShowNotifyInfo(const FString& Message)
{
	FNotificationInfo NotifyInfo(FText::FromString(Message));
	NotifyInfo.bUseLargeFont = true;
	NotifyInfo.FadeOutDuration = 7.f;
	FSlateNotificationManager::Get().AddNotification(NotifyInfo);
}
```
**使用:**
ShowNotifyInfo(TEXT("Successfully duplicated " + FString::FromInt(Counter) + " files"));
结果:
![Alt text](image-15.png)

---
# 自动判断资产类型并添加命名前缀

> 命名规范参考:[资产命名规范](https://docs.unrealengine.com/5.2/zh-CN/recommended-asset-naming-conventions-in-unreal-engine-projects/)
资产类型与前缀的对应的数据结构主要靠TMap进行存取
举例:
```cpp
TMap<UClass*, FString>PrefixMap =
{
	{UBlueprint::StaticClass(),TEXT("BP_")},
	{UStaticMesh::StaticClass(),TEXT("SM_")},
	{UMaterial::StaticClass(),TEXT("M_")},
	{UMaterialInstanceConstant::StaticClass(),TEXT("MI")},
	{UMaterialFunctionInterface::StaticClass(),TEXT("MF_")},
	{UParticleSystem::StaticClass(),TEXT("PS_")},
	{USoundCue::StaticClass(),TEXT("SC_")},
	{USoundWave::StaticClass(),TEXT("SW_")},
	{UTexture::StaticClass(),TEXT("T_")},
	{UTexture2D::StaticClass(),TEXT("T_")},
	{UUserWidget::StaticClass(),TEXT("WBP_")},
	{USkeletalMeshComponent::StaticClass(),TEXT("SK_")},
	{UNiagaraSystem::StaticClass(),TEXT("NS_")},
	{UNiagaraEmitter::StaticClass(),TEXT("NE_")}
};
```

---
**添加前缀的思路:**
获得选择的资产的object,然后遍历这些object,通过TMap的Find方法找TMap里面是否有object对应的前缀,如果有就通过UEditorUtilityLibrary的RenameAsset方法来修改object的名字.
**后来添加的补充:**
老师有提到材质球创建材质示例时会自动地在后面添加_inst名字,现在有个需求时,碰到材质实例时要更改一下添加前缀地步骤,添加前缀前需要先去除掉开头的M_和结尾的_inst,然后再添加前缀MI_
我个人是通过这个代码来判断选择的资产是否是材质实例类型:
SelectedObject->GetClass() == UMaterialInstanceConstant::StaticClass()
老师给的代码是object有一个自己的方法用来判断object是否是某一种类型:
SelectedObject->IsA\<UMaterialInstanceConstant>()
**添加前缀的代码:**
```cpp
void UQuickAssetAction::AddPrefixName()
{
	TArray<UObject*> SelectedObjects = UEditorUtilityLibrary::GetSelectedAssets();
	uint32 Counter = 0;
	for (UObject* SelectedObject : SelectedObjects)
	{
		if (!SelectedObject) continue;
		FString* PrefixFound = PrefixMap.Find(SelectedObject->GetClass());
		if (!PrefixFound || PrefixFound->IsEmpty())
		{
			Print(TEXT("Failed to find prefix for class ") + SelectedObject->GetClass()->GetName(), FColor::Red);
		}
		FString OldName = SelectedObject->GetName();
		if (OldName.StartsWith(*PrefixFound))
		{
			Print(OldName + TEXT(" already has prefix added"), FColor::Red);
			continue;
		}
		if (SelectedObject->IsA<UMaterialInstanceConstant>())
		{
			OldName.RemoveFromStart(TEXT("M_"));
			OldName.RemoveFromEnd(TEXT("_inst"));
		}
		FString NewNameWithPrefix = *PrefixFound + OldName;
		UEditorUtilityLibrary::RenameAsset(SelectedObject, NewNameWithPrefix);
		++Counter;
	}
	if (Counter > 0)
	{
		ShowNotifyInfo(TEXT("Successfully renamed ") + FString::FromInt(Counter) + " assets");
	}
}
```

---
# 移除未放置在关卡里的资产
修复重定向器的思路:
首先修复重定向器使用的是AssetTools模块的FixupReferencers方法,它需要接收的是UObjectRedirectors*的数组,也就是重定向器的指针的数组.为了得到UObjectRedirectors*的数组可以通过AssetRegistry模块的GetAssets方法得到重定向器的FAssetData(需要借助FARFilter过滤器),得到FAssetData以后再使用FAssetData的GetAsset()来得到UObject*,然后通过Cast将其转换为UObjectRedirectors*,最后使用AssetTools模块的FixupReferencers方法来修复重定向器.
**有一个需要提到的是:** 在定义过滤器时教程中使用的是Filter.ClassNames.Emplace("ObjectRedirector");但是这个方法在UE5.1中就不能用了,替代方法是使用:Filter.ClassPaths.Emplace(FTopLevelAssetPath(UObjectRedirector::StaticClass()));或者Filter.ClassPaths.Emplace(TEXT("/Script/Engine.ObjectRedirector"))
```cpp
void UQuickAssetAction::RemoveUnusedAssets()
{
	TArray<FAssetData> SelectedAssetsData = UEditorUtilityLibrary::GetSelectedAssetData();
	TArray<FAssetData> UnusedAssetsData;
	FixUpRedirectors(); // 修复重定向器
	for (const FAssetData& SelectedAssetData : SelectedAssetsData)
	{
		// 先找资产的所有引用
		TArray<FString> AssetReferencers =
			UEditorAssetLibrary::FindPackageReferencersForAsset(SelectedAssetData.GetObjectPathString());
		// 如果此资产没有引用就放到UnusedAssetsData数组中
		if (AssetReferencers.Num() == 0)
		{
			UnusedAssetsData.Add(SelectedAssetData);
		}
	}
	// 如果UnusedAssetsData数组数量为0
	if (UnusedAssetsData.Num() == 0)
	{
		ShowMsgDialog(EAppMsgType::Ok, TEXT("No unused asset found among selected assets"), false);
		return;
	}
	// 如果UnusedAssetsData数组数量不为0就尝试删除里面的所有内容
	// ObjectTools::DeleteAssets不是强制删除,而是弹窗交给用户自己确定是否删除
	const int32 NumOfAssetsDeleted = ObjectTools::DeleteAssets(UnusedAssetsData);
	/*由于最终删除选择权在用户手上, 因此如果用户不选择删除那就不执行后面的*/
	if (NumOfAssetsDeleted == 0) return;
	ShowNotifyInfo(TEXT("Successfully deleted") + FString::FromInt(NumOfAssetsDeleted) + TEXT(" unused assets"));
}

void UQuickAssetAction::FixUpRedirectors()
{
	TArray<UObjectRedirector*> RedirectorsToFixArray; // 定义用来修复的重定向器的数组

	// 加载并获取AssetRegistry模块,用于操作资产注册信息
	FAssetRegistryModule& AssetRegistryModule =
		FModuleManager::Get().LoadModuleChecked<FAssetRegistryModule>(TEXT("AssetRegistry")); 

	// 创建过滤器
	FARFilter Filter;
	Filter.bRecursivePaths = true; // 设定过滤器为递归查找资产
	Filter.PackagePaths.Emplace("/Game"); // 设定过滤器寻找的包的路径
	Filter.ClassPaths.Emplace(FTopLevelAssetPath(UObjectRedirector::StaticClass()));// 设定过滤器只需要类名为ObjectRedirector(重定向器)的
	// 或者这样:Filter.ClassPaths.Emplace(TEXT("/Script/Engine.ObjectRedirector"));

	TArray<FAssetData> OutRedirectors;
	// 通过AssetRegistry模块的GetAssets方法配合过滤器得到所有重定向器的FAssetData
	AssetRegistryModule.Get().GetAssets(Filter, OutRedirectors);

	// 遍历所有重定向器的FAssetData得到FAssetData所表示的UObjectRedirector*
	for (const FAssetData& RedirectorData:OutRedirectors)
	{
		// Cast是强制类型转换,通过FAssetData对象的GetAsset方法得到UObject*,然后通过Cast得到UObjectRedirector*
		if (UObjectRedirector* RedirectorToFix = Cast<UObjectRedirector>(RedirectorData.GetAsset()))
		{
			RedirectorsToFixArray.Add(RedirectorToFix);
		}
	}

	// 加载AssetToos模块,用来修复引用关系
	FAssetToolsModule& AssetToolsModule =
		FModuleManager::LoadModuleChecked<FAssetToolsModule>(TEXT("AssetTools"));
	// 调用AssetTools模块的FixupReferencers函数来修复引用关系
	AssetToolsModule.Get().FixupReferencers(RedirectorsToFixArray);

}
```

---
# delegate(委托)

**委托的介绍:**
- 委托可以调用C++对象上的成员函数
- 一旦绑定到函数,函数就可以在以后的时间被调用
- 如果想要实现例如点击按钮触发函数就需要将委托与成员函数进行绑定
- 虚幻引擎支持三种委托: 单播委托,多播委托,动态委托

**定义委托:**
定义委托可以使用虚幻引擎提供的宏,这里介绍三种定义委托的方式(**图片中的蓝色为名字或类型举例**)
第一种是定义一个委托,它调用的是一个没有返回值的名字叫Function的函数
第二种是定义一个委托,它调用的函数没有返回值并且需要接收一个参数,参数类型为自定义的.
第三种是定义一个委托,它调用的函数有返回值并且需要接收一个参数,参数类型与返回类型为自定义的.
![Alt text](image-20.png)

---
# 创建自定义菜单项
> 在这篇内容中,教程中导入之前为了调试而创建的头文件(DebugHeader.h)后再编译会出错,因此把DebugHeader.h的函数前面都加上了static,然后把所有函数都放在了一个命名空间里面.
但是我自己在使用过程中,并没有出现编译报错的情况,因此没有添加static.
**但是在后面的使用过程中,没有添加static遇到的编译错误,因此还是加上static吧.最好再把它们放到命名空间里面**
**如果不加的话可能会遇到:找到一个或多个多重定义的符号的问题,也就是说名字重复了.**
## 创建自定义菜单项的思路
目前创建的功能都是需要在资产里面右键然后在点击脚本化资产行为中的功能来使用的.
这里介绍一下将功能放到对文件夹右键显示的创建自定义菜单项的思路:
1. 首先在Visual Studio找到以我们创建的插件命名的头文件(也就是前面的SuperManager),在其中可以看到虚幻为它创建了两个纯虚函数:**StartupModule**和**ShutdownModule**.
进入其定义可以看到注释:
**StartupModule**中的代码将在模块加载到内存后执行;确切的时间在每个模块的.uplugin文件中指定(也就是前面创建plugin时首先做的设置PreDefault![Alt text](image-3.png)).
**ShutdownModule**中的代码对于支持动态重载的模块可以在关闭期间被调用来清理模块,以及卸载模块之前会进行调用.
2. 将创建自定义菜单项的代码放到StartupModule函数里面.
3. 加载ContentBrowser模块:FContentBrowserModule& ContentBrowserModule = FModuleManager::LoadModuleChecked<FContentBrowserModule>(TEXT("ContentBrowser"));
4. 通过ContentBrowser模块的GetAllPathViewContextMenuExtenders得到UE的用于路径视图内容的扩展的所有委托数组
5. 在得到的UE的委托数组里添加自己的委托
6. 将委托与自己的函数进行绑定

---
## 一键删除未使用的资产
### 头文件代码
**插件的头文件SuperManager.h:**
其中#pragma region ContentBrowserMenuExtension和#pragma endregion的意思是将这两行之间的内容包裹起来,加了这两行以后,就可以把这两行之内的代码进行压缩和展开,方便整理代码,其中ContentBrowserMenuExtension是自定义的内容的概况名字.
压缩之后的样子:![Alt text](image-21.png)
```cpp
// Copyright Epic Games, Inc. All Rights Reserved.

#pragma once

#include "CoreMinimal.h"
#include "Modules/ModuleManager.h"

class FSuperManagerModule : public IModuleInterface
{
public:

	/** IModuleInterface implementation */
	virtual void StartupModule() override;
	virtual void ShutdownModule() override;

private:
#pragma region ContentBrowserMenuExtension
	void InitCBMenuExtension();
	TSharedRef<FExtender> CustomCBMenuExtender(const TArray<FString>& SelectedPaths);
	void AddCBMenuEntry(FMenuBuilder& MenuBuilder);
	void OnDeleteUnusedAssetButtonClicked();
#pragma endregion 
};

```

---
### 委托的创建和绑定
这里代码展示的委托类型有:FContentBrowserMenuExtender_SelectedPaths,FMenuExtensionDelegate,FExecuteAction,这三种是虚幻自己定义的委托类型,可以通过源码看到其定义,以及委托类型是否有返回值,绑定的函数是否需要接收参数.
快速创建某委托类型的委托,并且将这个委托与某个函数进行绑定的例子:
这里创建了一个FContentBrowserMenuExtender_SelectedPaths类型的委托,只是并没有给创建的委托定义名字,然后把这个委托跟FSuperManagerModule::CustomCBMenuExtender函数进行了绑定.
FContentBrowserMenuExtender_SelectedPaths::CreateRaw(this, &FSuperManagerModule::CustomCBMenuExtender)
**三个绑定函数:**
**FSuperManagerModule::CustomCBMenuExtender:** 这个函数负责定义菜单的位置,这里是放在了Delete的后面,Delete这个名字可以通过在编辑器偏好设置中开启显示UI扩展点来看到
![Alt text](image-22.png)![Alt text](image-23.png)
**FSuperManagerModule::AddCBMenuEntry:** 这个函数负责定义菜单的名字的提示条和图标和当点击时对应的委托.
**FSuperManagerModule::OnDeleteUnusedAssetButtonClicked:** 这个函数负责定义当点击菜单时对应的执行内容.
**void FSuperManagerModule::FixUpRedirectors:** 修复重定向器,跟前面的教程内容一样的.
**代码详情:**
```cpp
// Copyright Epic Games, Inc. All Rights Reserved.

#include "SuperManager.h"
#include "ContentBrowserModule.h"
#include "DebugHeader.h"
#include "EditorAssetLibrary.h"
#include "ObjectTools.h"
#include "AssetRegistryModule.h"
#include "AssetToolsModule.h"

#define LOCTEXT_NAMESPACE "FSuperManagerModule"

void FSuperManagerModule::StartupModule()
{
	InitCBMenuExtension();
}

#pragma region ContentBrowserMenuExtension
void FSuperManagerModule::InitCBMenuExtension()
{
	// 加载模块并取别名
	FContentBrowserModule& ContentBrowserModule =
		FModuleManager::LoadModuleChecked<FContentBrowserModule>(TEXT("ContentBrowser"));
	// 得到UE的用于路径视图内容的扩展的所有委托
	TArray<FContentBrowserMenuExtender_SelectedPaths>& ContentBrowserModuleMenuExtenders =
		ContentBrowserModule.GetAllPathViewContextMenuExtenders();
	/* 这是第一种创建委托并绑定函数的方法:
	// 创建一个委托(FContentBrowserMenuExtender_SelectedPaths是一个委托类型,用于在路径上右键单击时请求菜单)
	FContentBrowserMenuExtender_SelectedPaths CustomCBMenuDelegate;
	// 将委托与自己创建的成员函数进行绑定
	// 通过查看FContentBrowserMenuExtender_SelectedPaths类型可以得知
	// 它需要绑定函数的返回类型是TSharedRef<FExtender>,接收参数类型是const TArray<FString>&
	CustomCBMenuDelegate.BindRaw(this, &FSuperManagerModule::CustomCBMenuExtender);
	// 在UE的用于路径视图内容的委托中加入自己的委托
	ContentBrowserModuleMenuExtenders.Add(CustomCBMenuDelegate);
	*/
	// 第二种创建委托并绑定函数的方法,好处是不需要定义委托的名字
	ContentBrowserModuleMenuExtenders.Add(FContentBrowserMenuExtender_SelectedPaths::
		CreateRaw(this, &FSuperManagerModule::CustomCBMenuExtender));


}

// 定义菜单的位置
TSharedRef<FExtender> FSuperManagerModule::CustomCBMenuExtender(const TArray<FString>& SelectedPaths)
{
	TSharedRef<FExtender> MenuExtender(new FExtender());
	if (SelectedPaths.Num() > 0)
	{
		MenuExtender->AddMenuExtension(
			FName("Delete"), // 找到已经存在的Delete菜单
			EExtensionHook::After, // 把自定义的菜单放到Delete菜单后面
			TSharedPtr<FUICommandList>(), // 定义快捷键,这里为空
			FMenuExtensionDelegate::CreateRaw(this, &FSuperManagerModule::AddCBMenuEntry) // 创建委托并绑定成员函数
		);

		FolderPathsSelected = SelectedPaths;
	}

	return MenuExtender;
}

// 定义菜单的名字的提示条和图标和当点击时对应的委托
void FSuperManagerModule::AddCBMenuEntry(FMenuBuilder& MenuBuilder)
{
	MenuBuilder.AddMenuEntry(
		FText::FromString(TEXT("Delete Unused Assets")), // 自定义的菜单名字
		FText::FromString(TEXT("Safely delete all unused assets under folder")), // 菜单的提示条
		FSlateIcon(), // 菜单的图标
		FExecuteAction::CreateRaw(this, &FSuperManagerModule::OnDeleteUnusedAssetButtonClicked) // 创建点击时触发的委托并与成员函数进行绑定
	);
}

// 删除未使用的资产
void FSuperManagerModule::OnDeleteUnusedAssetButtonClicked()
{
	if (FolderPathsSelected.Num() > 1)
	{
		ShowMsgDialog(EAppMsgType::Ok, TEXT("You can only do this to one folder"));
		return;
	}
	TArray<FString> AssetPathNames = UEditorAssetLibrary::ListAssets(FolderPathsSelected[0]);

	if (AssetPathNames.Num() == 0)
	{
		ShowMsgDialog(EAppMsgType::Ok, TEXT("No asset found under selected folder", false));
	}

	EAppReturnType::Type ConfirmResult = ShowMsgDialog(EAppMsgType::YesNo, TEXT("A total of ") + FString::FromInt(AssetPathNames.Num()) + TEXT(" found.\nWoudle you like to procceed?"));
	if (ConfirmResult == EAppReturnType::No) return;

	FixUpRedirectors();

	TArray<FAssetData> UnusedAssetDataArray;
	for (const FString& AssetPathName : AssetPathNames)
	{
		// 如果选择的文件夹内容包含这些,那么就不进行处理,因为这些文件夹是不能改变的
		if (AssetPathName.Contains(TEXT("Developers"))
		|| AssetPathName.Contains(TEXT("Collections"))
		|| AssetPathName.Contains(TEXT("__ExternalActors__"))
		|| AssetPathName.Contains(TEXT("__ExternalObjects__"))) 
		{
			continue;
		}
		TArray<FString> AssetReferencers = UEditorAssetLibrary::FindPackageReferencersForAsset(AssetPathName);
		if (AssetReferencers.Num() == 0)
		{
			FAssetData UnusedAssetData = UEditorAssetLibrary::FindAssetData(AssetPathName);
			UnusedAssetDataArray.Add(UnusedAssetData);
		}
	}

	if (UnusedAssetDataArray.Num() > 0)
	{
		ObjectTools::DeleteAssets(UnusedAssetDataArray);
	}
	else
	{
		ShowMsgDialog(EAppMsgType::Ok, TEXT("No unused asset found under selected folder"),false);
	}

}

// 修复重定向器
void FSuperManagerModule::FixUpRedirectors()
{
	TArray<UObjectRedirector*> RedirectorsToFixArray;


	FAssetRegistryModule& AssetRegistryModule =
		FModuleManager::Get().LoadModuleChecked<FAssetRegistryModule>(TEXT("AssetRegistry"));

	FARFilter Filter;
	Filter.bRecursivePaths = true;
	Filter.PackagePaths.Emplace("/Game");
	// Filter.ClassNames.Emplace("ObjectRedirector"); // UE5.0版本用这个还可以,UE5.1版本就不可以了,需要用ClassPaths来代替
	Filter.ClassPaths.Add(FTopLevelAssetPath(UObjectRedirector::StaticClass()));

	TArray<FAssetData> OutRedirectors;
	AssetRegistryModule.Get().GetAssets(Filter, OutRedirectors);

	for (const FAssetData& RedirectorData : OutRedirectors)
	{

		if (UObjectRedirector* RedirectorToFix = Cast<UObjectRedirector>(RedirectorData.GetAsset()))
		{
			RedirectorsToFixArray.Add(RedirectorToFix);
		}
	}


	FAssetToolsModule& AssetToolsModule =
		FModuleManager::LoadModuleChecked<FAssetToolsModule>(TEXT("AssetTools"));

	AssetToolsModule.Get().FixupReferencers(RedirectorsToFixArray);
}

#pragma endregion 

void FSuperManagerModule::ShutdownModule()
{
	// This function may be called during shutdown to clean up your module.  For modules that support dynamic reloading,
	// we call this function before unloading the module.
}

#undef LOCTEXT_NAMESPACE

IMPLEMENT_MODULE(FSuperManagerModule, SuperManager)
```

## 一键删除空的文件夹
在已经做好了一个自定义菜单项的情况下,可以在那个的基础上添加新的菜单,只需要在之前创建的FSuperManagerModule::AddCBMenuEntry函数中添加第二个菜单,然后再创建委托绑定函数即可.
代码举例:
**添加新的菜单**
```cpp
// 定义菜单的名字的提示条和图标和当点击时对应的委托
void FSuperManagerModule::AddCBMenuEntry(FMenuBuilder& MenuBuilder)
{
	// 添加第一个菜单
	MenuBuilder.AddMenuEntry(
		FText::FromString(TEXT("Delete Unused Assets")), // 自定义的菜单名字
		FText::FromString(TEXT("Safely delete all unused assets under folder")), // 菜单的提示条
		FSlateIcon(), // 菜单的图标
		FExecuteAction::CreateRaw(this, &FSuperManagerModule::OnDeleteUnusedAssetButtonClicked) // 创建点击时触发的委托并与成员函数进行绑定
	);
	// 添加第二个菜单
	MenuBuilder.AddMenuEntry(
		FText::FromString(TEXT("Delete Empty Folders")), // 自定义的菜单名字
		FText::FromString(TEXT("Safely delete all empty folders")), // 菜单的提示条
		FSlateIcon(), // 菜单的图标
		FExecuteAction::CreateRaw(this, &FSuperManagerModule::OnDeleteEmptyFoldersButtonClicked) // 创建点击时触发的委托并与成员函数进行绑定
	);
}
```
**删除空文件夹的函数**
思路:删除前先调用之前创建的FixUpRedirectors();来进行重定向器的修复.然后通过ListAssets得到所有文件夹下的文件与文件夹路径(ListrAssets的第三个参数为true即可得到包括文件夹路径),然后排除掉不能修改的文件内容,通过UEditorAssetLibrary::DoesDirectoryExist()判断是否为文件夹,通过UEditorAssetLibrary::DoesDirectoryHaveAssets()判断文件夹是否存在内容,通过UEditorAssetLibrary::DeleteDirectory()来删除文件夹.
```cpp
void FSuperManagerModule::OnDeleteEmptyFoldersButtonClicked()
{
	FixUpRedirectors();

	TArray<FString> FolderPathsArray = UEditorAssetLibrary::ListAssets(FolderPathsSelected[0],true,true);
	uint32 Counter = 0;

	FString EmptyFolderPathsNames;
	TArray<FString> EmptyFoldersPathsArray;

	for (const FString& FolderPath : FolderPathsArray)
	{
		if (FolderPath.Contains(TEXT("Developers"))
			|| FolderPath.Contains(TEXT("Collections"))
			|| FolderPath.Contains(TEXT("__ExternalActors__"))
			|| FolderPath.Contains(TEXT("__ExternalObjects__"))) continue;

		if (!UEditorAssetLibrary::DoesDirectoryExist(FolderPath)) continue;

		if (!UEditorAssetLibrary::DoesDirectoryHaveAssets(FolderPath))
		{
			EmptyFolderPathsNames.Append(FolderPath);
			EmptyFolderPathsNames.Append("\n");

			EmptyFoldersPathsArray.Add(FolderPath);
		}
	}

	if (EmptyFoldersPathsArray.Num() == 0)
	{
		ShowMsgDialog(EAppMsgType::Ok, TEXT("No empty folder found under selected folder"), false);
		return;
	}
	EAppReturnType::Type ConfirmResult = ShowMsgDialog(EAppMsgType::OkCancel,
		TEXT("Empty folders found in:\n") + EmptyFolderPathsNames + TEXT("\nWould you like to delete all?"), false);

	if (ConfirmResult == EAppReturnType::Cancel) return;

	for (const FString& EmptyFolderPath : EmptyFoldersPathsArray)
	{
		UEditorAssetLibrary::DeleteDirectory(EmptyFolderPath) ?
			++Counter : Print(TEXT("Failed to delete ") + EmptyFolderPath, FColor::Red);
	}

	if (Counter > 0)
	{
		ShowNotifyInfo(TEXT("Successfully deleted ") + FString::FromInt(Counter) + TEXT(" folders"));
	}
}
```

---
# 智能指针
> [UE官方文档对智能指针的介绍](https://docs.unrealengine.com/5.2/zh-CN/smart-pointers-in-unreal-engine/)

**智能指针的作用:** 减轻内存分配和跟踪的负担
**UE的四种智能指针类型:**
1. SharedPointers: TSharedPtr
2. SharedReferences: TSharedRef
3. WeakPointers: TWeakPtr
4. UniquePointers
TSharedPtr: 拥有其引用的对象,能防止对象被删除(通过ReferenceCounting计数,为0时自动删除),可以指向空白.
TSharedRef: 拥有其引用的对象,能防止对象被删除,引用的对象必须为非空.(因为必须为非空,所以Slate经常使用它)
TWeakPtr: 不拥有引用的对象,用于中断引用循环.(当只想保留对象的引用时有用,可以通过检查它来确定它是否有对象)

**智能指针和垃圾回收:** 智能指针无法与UObject系统同时使用。UObject系统有自己的一套内存管理系统,叫垃圾回收,使用UPROPERTY()宏来定义一个指针就能够对UObject指针进行垃圾回收.
**创建智能指针:**
```cpp
// 传统上的创建一个指针的方式:
FExtender* MenuExtender = new FExtender(); // 在堆上开辟一个空间存放FExtender的对象,并创建一个MenuExtender指针指向它
// 进行一系列操作
delete MenuExtender; // 使用完以后必须手动删除掉,不然会造成内存泄漏

// 创建智能指针方法一
TSharedRef<FExtender> MenuExtender (new FExtender());
// 创建智能指针方法二
TSharedRef<FExtender> MenuExtender = MakeShareable(new FExtender());
// 创建智能指针方法三(已经有对象的情况下)
const FAssetData Data = UEditorAssetLibrary::FindAssetData(AssetPathName);
TSharedPtr<FAssetData> AssetDataSharedPtr = MakeShared<FAssetData>(Data);
```

---
# 