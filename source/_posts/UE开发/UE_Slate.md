---
title: UE_Slate
tags: UE_Slate
categories: UE开发
abbrlink: a2d2b7a5
date: 2023-09-13 10:25:00
---

# 学习的视频
[第一个独立程序_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV19L411L7XA/?p=2&spm_id_from=pageDriver&vd_source=b1de3fe38e887eb40fc55a5485724480)
# 对于UE编译系统总结的文章推荐：
[虚幻引擎编译系统总结](https://zhuanlan.zhihu.com/p/458435453)
# 下载并编译源码版UE
去github下载源码版：[https://github.com/EpicGames/UnrealEngine](https://github.com/EpicGames/UnrealEngine)<br />
# 第一个程序
## 处理UE源码版的文件的过程中需要注意的点
![Alt text](image(1).png)<br />通过文章里的这些描述得知，如果我们需要新建第一个程序就需要全程再本地资源管理器中进行操作，不能够在VS里面进行操作。<br />当进行完新建文件的操作完以后，通过双击运行GenerateProjectFiles.bat文件即可更新UE的结构，同时VS里面也会同步更新。<br />当更改build.cs文件时也需要双击运行GenerateProjectFiles.bat文件。
## 过程
去源码的Source文件夹中的Programs目录里面找到BlankProgram文件夹（这个文件夹是一个空白程序文件夹，因此可以通过这个来创建自己的程序）：UnrealEngine-release\Engine\Source\Programs\<br />选中BlankProgram文件夹ctrl+c和ctrl+v创建一个副本<br />改名为自己想要的名字<br />以FirstProgram举例：<br />改文件夹的名字以后，更改文件夹里面的文件以及文件内容的名字，把BlankProgram都改为自己的名字(FirstProgram)<br />这四个文件除了文件名，文件的内容里的BlankProgram也都改为FirstProgram

![Alt text](image(2).png)<br />![Alt text](image(3).png)<br />更改完以后运行bat文件来重新生成工程文件。<br />![Alt text](image(4).png)<br />生成以后打开slh文件，将我们的FirstProgram设置为启动项目并进行编译<br />![Alt text](image(5).png)<br />编译完成之后进入cpp文件打上断点然后进行调试，然后就得到了打印helloworld的程序。<br />![Alt text](image(6).png)

---
# SWindow
## 主要参考程序：SlateViewer
首先可以参考一下自带的SlateViewer程序，将其设为启动项目然后进行调试即可查看内容结果。如下：<br />![Alt text](image(7).png)
## 模块更改
### 两个模块的作用：
![Alt text](image(8).png)
补充: 写代码时会include其他头文件,之所以不需要写全路径,只需要写public或者private后面的路径,应该就是因为在build.cs里面包括了那个模块名.如果没有就需要添加.这也就是模块由build.cs确定相互依赖关系的意思.
### build模块：
新增三个<br />![Alt text](image(9).png)
### target模块：
更改三个：<br />![Alt text](image(10).png)
## cpp文件的内容：

```cpp
// Copyright Epic Games, Inc. All Rights Reserved.


#include "FirstProgram.h"

#include "RequiredProgramMainCPPInclude.h"
#include "StandaloneRenderer.h"
#include "Framework/Application/SlateApplication.h"

DEFINE_LOG_CATEGORY_STATIC(LogFirstProgram, Log, All);

IMPLEMENT_APPLICATION(FirstProgram, "FirstProgram");

// INT32_MAIN_INT32_ARGC_TCHAR_ARGV()
// {
// 	GEngineLoop.PreInit(ArgC, ArgV);
// 	UE_LOG(LogFirstProgram, Display, TEXT("Hello World"));
// 	FEngineLoop::AppExit();
// 	return 0;
// }

/**
 * WinMain, called when the application is started
 */
int WINAPI WinMain(_In_ HINSTANCE hInInstance, _In_opt_ HINSTANCE hPrevInstance, _In_ LPSTR, _In_ int nCmdShow)
{
    // start up the main loop
    GEngineLoop.PreInit(GetCommandLineW());

    // crank up a normal Slate application using the platform's standalone renderer
    FSlateApplication::InitializeAsStandaloneApplication(GetStandardStandaloneRenderer());

    // 创建一个窗口
    TSharedPtr<SWindow> MainWindow = SNew(SWindow)
    .ClientSize(FVector2D(800, 600))
    [
    SNullWidget::NullWidget
    ];

    FSlateApplication::Get().AddWindow(MainWindow.ToSharedRef());
    // loop while the server does the rest
    while (!IsEngineExitRequested())
        {
            FSlateApplication::Get().PumpMessages();
            FSlateApplication::Get().Tick();
        }
    FSlateApplication::Shutdown();

    return 0;
}

```

其中只有下面这些是自己写的，其他的都是复制粘贴并删除部分代码的SlateViewerMainWindows.cpp和SlateViewerApp.cpp的内容<br />这里涉及到智能指针的使用<br />![Alt text](image(11).png)

---
# SButton 按钮
>这节主要讲了如何给窗口添加一个按钮,并且给按钮添加一个点击事件.<br />参考的SButton路径:**\UnrealEngine-release\Engine\Source\Runtime\Slate\Public\Widgets\Input\SButton.h**
## 创建文件
首先通过在资源管理器上在第一个新建的程序旁新建按钮的头文件和源文件(因为虚幻引擎不是靠sln来管理文件架构的,所以不要在VS里面进行文件的添加和删除).
创建好按钮的头文件和源文件以后使用bat文件重新生成一下项目.
这里我自定义文件名字叫SMybutton.
## SMybutton.h
> 声明了一个继承SButton的类,叫SMyButton,模仿SButton中的代码,声明一个Construct(初始化)和返回类型为FReply的按钮点击时执行的函数
```cpp
#pragma once
#include "Widgets/Input/SButton.h"

class SMyButton : public SButton
{
public:
	/**
	 * Construct this widget
	 *
	 * @param	InArgs	The declaration data for this widget
	 */
	void Construct(const FArguments& InArgs);
private:
	FReply ButtonClicked();
};
```
## SMybutton.cpp
> 实现初始化方法,首先调用父类的初始化的方法,然后在此基础上设置点击事件,当点击时执行SMyButton的ButtonClicked函数来返回一个信息窗口
```cpp
#include "SMyButton.h"

void SMyButton::Construct(const FArguments& InArgs)
{
	SButton::Construct(InArgs);

	this->SetOnClicked(FOnClicked::CreateRaw(this, &SMyButton::ButtonClicked));
}

FReply SMyButton::ButtonClicked()
{
	FMessageDialog::Open(EAppMsgType::Ok, FText::FromString("Button is clicked!"));
	return FReply::Handled();
}
```
## FirstProgram.cpp
> 自定义的按钮已经完成了,现在将其放到我们的第一个程序里创建的窗口里面.
```cpp
// 创建自定义的SButton
TSharedPtr<SMyButton> MyButton = SNew(SMyButton);
   // 创建一个窗口
TSharedPtr<SWindow> MainWindow = SNew(SWindow)
	.ClientSize(FVector2D(800, 600))
	[
        // 窗口上放入自定义的SButton
		MyButton.ToSharedRef()
	];
```

---
# SCanvas 画布
> SCanva翻译叫画布,学过UE的UMG就很好理解.

依然在本地新建一个头文件和源文件,新建完以后构建一下.我这里命名为SMyCanvas.h与SMycanvas.cpp
## SMycanvas.h
> 通过继承SCanvas,和SButton一样定义一个初始化的函数
```cpp
#pragma once
#include "Widgets/SCanvas.h"

class SMyCanvas : public SCanvas
{
public:
	void Construct(const FArguments& InArgs);
};
```
## SMycanvas.cpp
> 除了执行父类的初始化函数之外,新增两个槽用来放上一章创建的SButton类.
> 这里的槽和Qt的槽还不是一个概念,Slate的槽是用来放控件的.

```cpp
#include "SMyCanvas.h"
#include "SMyButton.h"
void SMyCanvas::Construct(const FArguments& InArgs)
{
	SCanvas::Construct(InArgs);
	
	AddSlot()
		.Position(FVector2D(100, 100))
		.Size(FVector2D(100, 40))
		[
			SNew(SMyButton)
		];

	AddSlot()
		.Position(FVector2d(300, 100))
		.Size(FVector2D(100, 40))
		[
			SNew(SMyButton)
		];
}
```
## FirstProgram.cpp
> 在窗口下放刚才定义的SCanvas
```cpp
// 创建自定义的Scanvas
TSharedPtr<SMyCanvas> MyCanvas = SNew(SMyCanvas);
// 创建一个窗口
TSharedPtr<SWindow> MainWindow = SNew(SWindow)
	.ClientSize(FVector2D(800, 600))
	[
		MyCanvas.ToSharedRef()
	];
```

---
# SComboBox下拉框
> 在画布里面添加下拉框

## SMyCanvas.h
```cpp
#pragma once
#include "Widgets/SCanvas.h"

class SMyCanvas : public SCanvas
{
public:
	void Construct(const FArguments& InArgs);
	
	TArray<TSharedPtr<FString>> Options; // ComboBox的项
	int32 CurrentSelected = -1; // ComboBox的项的索引
};
```
## SMycanvas.cpp
```cpp
#include "SMyCanvas.h"
void SMyCanvas::Construct(const FArguments& InArgs)
{
	SCanvas::Construct(InArgs);

	Options.Empty();
	Options.Add(MakeShareable(new FString("Apple")));
	Options.Add(MakeShareable(new FString("Banana")));
	Options.Add(MakeShareable(new FString("Orange")));

	AddSlot()
		.Position(FVector2D(500, 100))
		.Size(FVector2D(100, 40))
		[
			SNew(SComboBox<TSharedPtr<FString>>)
			// ComboBox的内容
			.OptionsSource(&Options)
			// 当生成ComboBox时执行,作用是显示ComboBox下拉框选项值的文本块
			.OnGenerateWidget_Lambda([](TSharedPtr<FString> InValue) {
				return SNew(STextBlock).Text(FText::FromString(*InValue));
				})
			// 当ComboBox的选择发生改变时执行
			.OnSelectionChanged_Lambda([this](TSharedPtr<FString> NewOption,ESelectInfo::Type SelectType) {
					CurrentSelected = Options.Find(NewOption);
				})
			// SComboBox中嵌套的显示的文本块,负责显示SComboBox中选择的内容
			[
				SNew(STextBlock).Text_Lambda([this]() {
					if (CurrentSelected < 0 || CurrentSelected > Options.Num() - 1)
						return FText::FromString("");
					else
						return FText::FromString(*Options[CurrentSelected]);
					})
			]
		];

}
```

---
# SHorizontalBox,SVerticalBox 水平布局和垂直布局
> 在Scanvas(画布)上面直接添加一个水平布局和一个垂直布局来举例

最终结果:
![Alt text](image.png)
```cpp
#include "SMyCanvas.h"
void SMyCanvas::Construct(const FArguments& InArgs)
{
	SCanvas::Construct(InArgs);
	// 添加一个水平布局
	AddSlot()
		.Position(FVector2D(100, 200))
		.Size(FVector2D(400, 40))
		[
			SNew(SHorizontalBox)
			+SHorizontalBox::Slot()
			[
				SNew(SButton)
			]
			+SHorizontalBox::Slot()
			// 设置这个槽宽度占两个
			.FillWidth(2.0f)
			[
				SNew(SButton)
			]
			+SHorizontalBox::Slot()
			[
				SNew(SButton)
			]
		];
	// 添加一个垂直布局
	AddSlot()
		.Position(FVector2D(100, 300))
		.Size(FVector2D(100, 160))
		[
			SNew(SVerticalBox)
			+SVerticalBox::Slot()
			[
				SNew(SButton)
			]
			+SVerticalBox::Slot()
			.FillHeight(2.0)
			[
				SNew(SButton)
			]
			+SVerticalBox::Slot()
			[
				SNew(SButton)
			]
		];
}
```

---
# STreeView
> 新建SMyTreeView.cpp和SMyTreeView.h然后重新构建一下

生成结果:
![Alt text](image-1.png)
## SMyTreeView.h
```cpp
#pragma once

// 树状图的Item数据
class UTreeItemData
{

public:
	// Item的内容
	FString MyName;
	float MyHeight = 10;
	// 每个item的子项数组
	TArray<TSharedPtr<UTreeItemData>> Children;
};
// 树状图
class SMyTreeView : public STreeView<TSharedPtr<UTreeItemData>>
{
public:
	void Construct(const FArguments& InArgs);
	// 树状图的item的数组
	TArray<TSharedPtr<UTreeItemData>> TreeItemDatas;
	// 声明生成树状图的函数
	TSharedRef<ITableRow> GenerateRowItem(TSharedPtr<UTreeItemData> InTreeItemData, const TSharedRef<STableViewBase>& OwnerTable);
	// 声明获取项的子项的方法
	void GetChildrenForItem(TSharedPtr<UTreeItemData> InTreeItem, TArray<TSharedPtr<UTreeItemData>>& OutChildren);
};
```
## SMyTreeView.cpp
```cpp
#include "SMyTreeView.h"

void SMyTreeView::Construct(const FArguments& InArgs)
{
	FArguments Arguments = InArgs;

	// 创建item与设置item与数据与子项
	TSharedPtr<UTreeItemData> ZhangSan = MakeShareable(new UTreeItemData);
	ZhangSan->MyName = FString("zhangSan");
	TSharedPtr<UTreeItemData> ZhangSan1 = MakeShareable(new UTreeItemData);
	ZhangSan1->MyName = FString("ZhangSan1");
	TSharedPtr<UTreeItemData> ZhangSan2 = MakeShareable(new UTreeItemData);
	ZhangSan2->MyName = FString("ZhangSan2");

	ZhangSan->Children.Add(ZhangSan1);
	ZhangSan->Children.Add(ZhangSan2);

	TSharedPtr<UTreeItemData> LiSi = MakeShareable(new UTreeItemData);
	LiSi->MyName = FString("LiSi");
	TSharedPtr<UTreeItemData> LiSi1 = MakeShareable(new UTreeItemData);
	LiSi1->MyName = FString("LiSi1");
	TSharedPtr<UTreeItemData> LiSi2 = MakeShareable(new UTreeItemData);
	LiSi2->MyName = FString("LiSi2");
	TSharedPtr<UTreeItemData> LiSi3 = MakeShareable(new UTreeItemData);
	LiSi3->MyName = FString("LiSi3");

	LiSi->Children.Add(LiSi1);
	LiSi->Children.Add(LiSi2);
	LiSi->Children.Add(LiSi3);

	// 将item添加到数组
	TreeItemDatas.Add(ZhangSan);
	TreeItemDatas.Add(LiSi);
	// 通过三个必须具备的委托来生成树状图
	Arguments.TreeItemsSource(&TreeItemDatas); //指认树状图的item
	Arguments.OnGenerateRow_Raw(this, &SMyTreeView::GenerateRowItem); // 指认生成的树状图每一行的内容
	Arguments.OnGetChildren_Raw(this, &SMyTreeView::GetChildrenForItem); // 指认如何获取item的子项

	STreeView::Construct(Arguments);

}
TSharedRef<ITableRow> SMyTreeView::GenerateRowItem(TSharedPtr<UTreeItemData> InTreeItemData, const TSharedRef<STableViewBase>& OwnerTable)
{
	return SNew(STableRow<TSharedPtr<UTreeItemData>>, OwnerTable)
		[
			SNew(SHorizontalBox)
			+ SHorizontalBox::Slot()
		[
			SNew(STextBlock)
			.Text(FText::FromString(InTreeItemData->MyName))
		]
	+ SHorizontalBox::Slot()
		[
			SNew(STextBlock)
			.Text(FText::FromString(FString::SanitizeFloat(InTreeItemData->MyHeight)))
		]
		];
}

void SMyTreeView::GetChildrenForItem(TSharedPtr<UTreeItemData> InTreeItem, TArray<TSharedPtr<UTreeItemData>>& OutChildren)
{
	OutChildren = InTreeItem->Children;
}

```

---
# SlistView
> 跟STreeView差不多 就不加注释了
## SMylistView.h

```cpp
#pragma once

class UListViewItemData
{
public:
	FString MyName = "ZhangSan";
};

class SMyListView :public SListView<TSharedPtr<UListViewItemData>>
{
public:

	void Construct(const FArguments& InArgs);

	TArray<TSharedPtr<UListViewItemData>> ListItemDatas;

	TSharedRef<ITableRow> GenerateRowItem(TSharedPtr<UListViewItemData> InListViewItemData, const TSharedRef<STableViewBase>& OwnerTable);

};

```
##  SMyListView.cpp
```cpp
#include "SMyListView.h"

void SMyListView::Construct(const FArguments& InArgs)
{
	FArguments Arguments = InArgs;

	ListItemDatas.Add(MakeShareable(new UListViewItemData));
	ListItemDatas.Add(MakeShareable(new UListViewItemData));
	ListItemDatas.Add(MakeShareable(new UListViewItemData));

	Arguments.ListItemsSource(&ListItemDatas);
	Arguments.OnGenerateRow_Raw(this, &SMyListView::GenerateRowItem);

	SListView::Construct(Arguments);

}

TSharedRef<ITableRow> SMyListView::GenerateRowItem(TSharedPtr<UListViewItemData> InListViewItemData, const TSharedRef<STableViewBase>& OwnerTable)
{
	return SNew(STableRow<TSharedPtr<UListViewItemData>>, OwnerTable)
		[
			SNew(STextBlock)
			.Text(FText::FromString(InListViewItemData->MyName))
		];

}

```

---
# SImage
> 在之前的SMyCanvas.cpp里面添加新的槽并加入SImage控件
其中Icons.Warning使用的是UE自带的图片
```cpp
// 添加图像
AddSlot()
	.Position(FVector2D(400, 200))
	.Size(FVector2D(200, 200))
	[
		SNew(SImage)
		.Image(FCoreStyle::Get().GetBrush("Icons.Warning"))
	];
```

---
# SGridPanel
> 在之前的SMyCanvas.cpp里面添加新的槽并加入SGridPanel布局
```cpp
// 添加网格布局
AddSlot()
	.Position(FVector2D(400, 500))
	.Size(FVector2D(200, 200))

	[
		SNew(SGridPanel)
		// 设置每个网格的行和列上的控件都占一份
		.FillColumn(0, 1)
		.FillColumn(1, 1)
		.FillRow(0, 1)
		.FillRow(1, 1)
		+ SGridPanel::Slot(0, 0)
		[
			SNew(SImage)
			.Image(FCoreStyle::Get().GetBrush("Icons.Warning"))
		]
		+ SGridPanel::Slot(0, 1)
		[
			SNew(SImage)
			.Image(FCoreStyle::Get().GetBrush("Icons.Warning"))
		]
		+ SGridPanel::Slot(1, 0)
		[
			SNew(SImage)
			.Image(FCoreStyle::Get().GetBrush("Icons.Warning"))
		]
		+ SGridPanel::Slot(1, 1)
		[
			SNew(SImage)
			.Image(FCoreStyle::Get().GetBrush("Icons.Warning"))
		]
	];
```

---
# FTabManage
> 在FirstProgram.cpp里面直接添加FTabManage来体现FTabManage的使用方法,首先先把之前生成SWindow的代码注释掉.

生成的结果如下图所示
![Alt text](image-2.png)
```cpp
// Copyright Epic Games, Inc. All Rights Reserved.


#include "FirstProgram.h"

#include "RequiredProgramMainCPPInclude.h"
#include "StandaloneRenderer.h"
#include "Framework/Application/SlateApplication.h"
#include "SMyCanvas.h"

DEFINE_LOG_CATEGORY_STATIC(LogFirstProgram, Log, All);

IMPLEMENT_APPLICATION(FirstProgram, "FirstProgram");

/**
 * WinMain, called when the application is started
 */
int WINAPI WinMain(_In_ HINSTANCE hInInstance, _In_opt_ HINSTANCE hPrevInstance, _In_ LPSTR, _In_ int nCmdShow)
{
	// start up the main loop
	GEngineLoop.PreInit(GetCommandLineW());

	// crank up a normal Slate application using the platform's standalone renderer
	FSlateApplication::InitializeAsStandaloneApplication(GetStandardStandaloneRenderer());
	
	// FTabManager
	TArray<FName> TabName = { "LeftTab1","LeftTab2","RightTopTab","RightBottomTab" };
	const TSharedRef<FTabManager::FLayout> Layout = FTabManager::NewLayout(TEXT("Layout")) // 新建Layout
		->AddArea( // 为Layout添加Area
			FTabManager::NewArea(800, 600) // 新建Area
			->SetOrientation(EOrientation::Orient_Horizontal) // 设置方向为左右分割
			->Split( // 设置左边的区域
				FTabManager::NewStack() // 新增可堆叠在一起的栈
				->AddTab(TabName[0],ETabState::OpenedTab) // 在这个栈里面添加一个Tab
				->AddTab(TabName[1], ETabState::OpenedTab) // 在这个栈里面再添加一个Tab
			)
			->Split( // 设置右边的区域
				FTabManager::NewSplitter() // 在右边的区域新增一个分割块
				->SetOrientation(EOrientation::Orient_Vertical) // 设置分割块为上下分割
				->Split( // 设置右边上方的分割区域
					FTabManager::NewStack() // 新增可堆叠在一起的栈
					->AddTab(TabName[2],ETabState::OpenedTab) // 添加Tab
				)
				->Split( // 设置右边下方的分割区域
					FTabManager::NewStack()// 新增可堆叠在一起的栈
					->AddTab(TabName[3],ETabState::OpenedTab)// 添加Tab
				)
			)
		);

	FGlobalTabmanager::Get()->RestoreFrom(Layout, TSharedPtr<SWindow>()); // 将Layout放到SWindow里面

	// loop while the server does the rest
	while (!IsEngineExitRequested())
	{
		FSlateApplication::Get().PumpMessages();
		FSlateApplication::Get().Tick();
	}

	FSlateApplication::Shutdown();

	return 0;
}
```

---
# SDockTab(给Tab添加内容并令Tab能够进行拖拽与停靠)
> 要实现这样的Tab,需要通过FGlobalTabmanager::Get()->RegisterTabSpawner来注册SDockTab

- 这里解释一下工厂函数FOnSpawnTab::CreateLambda配合C++的lambda语法是怎么样的:
- FOnSpawnTab::CreateLambda(\[&](const FSpawnTabArgs& Args)->TSharedRef<SDockTab> {})
- 首先工厂函数FOnSpawnTab::CreateLambda的作用是接收一个lambda表达式来生成一个tab
- \[&](const FSpawnTabArgs& Args)->TSharedRef<SDockTab> {}就是一个lambda语法,语法为:\[捕获列表]\(参数列表)->返回类型{函数体}
- 捕获列表意思是函数体可以使用的外部的参数,&表示所有外部的参数都能使用,参数列表为传入函数体的参数,->后是返回的类型
![Alt text](image-3.png)
通过以下代码将名字叫LeftTab1的Tab定义成DockTab并且定义Tab的内容
```cpp
TArray<FName> TabName = { "LeftTab1","LeftTab2","RightTopTab","RightBottomTab"};
// 注册一个Tab,并使Tab可以被拖拽和停靠边缘,tab下存在一个按钮.
FGlobalTabmanager::Get()->RegisterTabSpawner(TabName[0], FOnSpawnTab::CreateLambda(
	[&](const FSpawnTabArgs& Args)->TSharedRef<SDockTab> {
		return SNew(SDockTab)
			[
				SNew(SButton)
				.Text(FText::FromName(TabName[0]))
			];
	}
));
```

---
# 制作菜单栏
> 制作如图所示菜单栏
> 其中MyMenu为菜单栏,OpenFile和CloseFile,SaveFile这些都是菜单栏下对应的命令.
> MyEditor是负责控制总UI的,想要显示这个UI就需要在FirstProgram.cpp(自己创建的程序)里面创建一个MyEditor对象就可以了.

![Alt text](image-4.png)

---
## FMenuBarBuilder 生成菜单栏
生成菜单栏也就是创建FMenuBarBuilder这个类,创建这个类有一个必须要的参数是FUICommandList类型的智能指针
菜单栏的类型为SWidget,因此有了FMenuBarBuilder的对象以后就可以通过MakeWidget函数来得到菜单栏.

---
## TCommands 设置菜单栏下对应的命令
通过继承TCommands创建一个属于自己的命令,然后通过UI_COMMAND定义命令的信息

---
## FUICommandList
通过FNewMenuDelegate::CreateLambda来将命令添加到菜单栏上,通过FUICommandList的对象的MapAction方法可以将菜单栏上的命令对应的执行功能.

---
## 总的代码
### MyCommands.h
```cpp
#pragma once
#include "Framework/Commands/Commands.h"

class MyCommands : public TCommands<MyCommands>
{
public:
	MyCommands();
	virtual void RegisterCommands() override; // 声明重载父类的注册命令函数

	// 声明三个命令
	TSharedPtr< FUICommandInfo > OpenFileCommand; 
	TSharedPtr< FUICommandInfo > CloseFileCommand;
	TSharedPtr< FUICommandInfo > SaveFileCommand;
};
```

### MyCommands.cpp
```cpp
#include "MyCommands.h"

#define LOCTEXT_NAMESPACE "MyCommands"

MyCommands::MyCommands()
	:TCommands<MyCommands>(
		TEXT("MyCommands"), // Context name for fast lookup
		NSLOCTEXT("Contexts", "MyEditor", "My Editor"), // Localized context name for displaying
		NAME_None,
		FCoreStyle::Get().GetStyleSetName() // Icon Style Set
		)
{

}

void MyCommands::RegisterCommands()
{
	// 定义三个命令的信息
	UI_COMMAND(OpenFileCommand, "OpenFile", "This is OpenFile command.", EUserInterfaceActionType::Button, FInputChord(EModifierKey::Control,EKeys::O));
	UI_COMMAND(CloseFileCommand, "CloseFile", "This is CloseFile command.", EUserInterfaceActionType::Button, FInputChord(EModifierKey::Control, EKeys::C));
	UI_COMMAND(SaveFileCommand, "SaveFile", "This is SaveFile command.", EUserInterfaceActionType::Button, FInputChord(EModifierKey::Control, EKeys::S));
}

#undef LOCTEXT_NAMESPACE
```

### MyEditor.h

```cpp
#pragma once

class MyEditor
{
public: 
	MyEditor();
	TSharedRef<SWidget> MakeMenuBar(); // 声明生成菜单栏的函数.
	TSharedPtr<FUICommandList> CommandList;
};
```

### MyEditor.cpp

```cpp
#include "MyEditor.h"
#include "MyCommands.h"
#define LOCTEXT_NAMESPACE "MyEditor"


MyEditor::MyEditor()
{
	CommandList = MakeShareable(new FUICommandList);

	// 进行注册命令
	MyCommands::Register();
	// 添加命令执行时对应的功能
	CommandList->MapAction(MyCommands::Get().OpenFileCommand,
		FExecuteAction::CreateLambda([]() {
			FMessageDialog::Open(EAppMsgType::Ok, FText::FromString("OpenFileCommand!"));
			})
	);
	CommandList->MapAction(MyCommands::Get().CloseFileCommand,
		FExecuteAction::CreateLambda([]() {
			FMessageDialog::Open(EAppMsgType::Ok, FText::FromString("CloseFileCommand!"));
			})
	);
	CommandList->MapAction(MyCommands::Get().SaveFileCommand,
		FExecuteAction::CreateLambda([]() {
			FMessageDialog::Open(EAppMsgType::Ok, FText::FromString("SaveFileCommand!"));
			})
	);

	// FTabManager
	TArray<FName> TabName = { "LeftTab","RightTopTab","RightBottomTab" };
	// 注册一个Tab,并使Tab可以被拖拽和停靠边缘,tab下存在一个按钮.
	FGlobalTabmanager::Get()->RegisterTabSpawner(TabName[0], FOnSpawnTab::CreateLambda(
		[&](const FSpawnTabArgs& Args)->TSharedRef<SDockTab> {
			return SNew(SDockTab)
				[
					SNew(SVerticalBox)
					+ SVerticalBox::Slot()
					.AutoHeight() // 设置菜单栏为合适的高度
				[
					MakeMenuBar()
				]
					+SVerticalBox::Slot()
					.FillHeight(1.f)
				[
					SNew(SButton)
					.Text(FText::FromName(TabName[0]))
				]
					
				];
		}
	));

	FGlobalTabmanager::Get()->RegisterTabSpawner(TabName[1], FOnSpawnTab::CreateLambda(
		[&](const FSpawnTabArgs& Args)->TSharedRef<SDockTab> {
			return SNew(SDockTab)
				[
					SNew(SButton)
					.Text(FText::FromName(TabName[1]))
				];
		}
	));

	FGlobalTabmanager::Get()->RegisterTabSpawner(TabName[2], FOnSpawnTab::CreateLambda(
		[&](const FSpawnTabArgs& Args)->TSharedRef<SDockTab> {
			return SNew(SDockTab)
				[
					SNew(SButton)
					.Text(FText::FromName(TabName[2]))
				];
		}
	));

	const TSharedRef<FTabManager::FLayout> Layout = FTabManager::NewLayout(TEXT("Layout")) // 新建Layout
		->AddArea( // 为Layout添加Area
			FTabManager::NewArea(800, 600) // 新建Area
			->SetOrientation(EOrientation::Orient_Horizontal) // 设置方向为左右分割
			->Split( // 设置左边的区域
				FTabManager::NewStack() // 新增可堆叠在一起的栈
				->AddTab(TabName[0], ETabState::OpenedTab) // 在这个栈里面添加一个Tab
			)
			->Split( // 设置右边的区域
				FTabManager::NewSplitter() // 在右边的区域新增一个分割块
				->SetOrientation(EOrientation::Orient_Vertical) // 设置分割块为上下分割
				->Split( // 设置右边上方的分割区域
					FTabManager::NewStack() // 新增可堆叠在一起的栈
					->AddTab(TabName[1], ETabState::OpenedTab) // 添加Tab
				)
				->Split( // 设置右边下方的分割区域
					FTabManager::NewStack()// 新增可堆叠在一起的栈
					->AddTab(TabName[2], ETabState::OpenedTab)// 添加Tab
				)
			)
		);

	FGlobalTabmanager::Get()->RestoreFrom(Layout, TSharedPtr<SWindow>()); // 将Layout放到SWindow里面
}

// 负责生成菜单栏的函数
TSharedRef<SWidget> MyEditor::MakeMenuBar()
{
	FMenuBarBuilder MenuBuilder(CommandList); // 生成一个FMenuBarBuilder对象,传入FUICommandList类型的智能指针
	MenuBuilder.AddPullDownMenu(
		LOCTEXT("MyMenu", "MyMenu"), // 菜单名
		LOCTEXT("MyMenu", "This is my menu"), // 菜单提示词

		// 将命令添加到菜单栏上
		FNewMenuDelegate::CreateLambda(
			[](FMenuBuilder& MenuBuilder){
				MenuBuilder.AddMenuEntry(MyCommands::Get().OpenFileCommand);
				MenuBuilder.AddMenuEntry(MyCommands::Get().CloseFileCommand);
				MenuBuilder.AddMenuEntry(MyCommands::Get().SaveFileCommand);
			}
		)
	);


	return MenuBuilder.MakeWidget(); 
}

#undef LOCTEXT_NAMESPACE
```

---
# FToolBarBuilder 创建工具架
这次通过上一节创建菜单栏需要的TCommand添加到工具架上.
![Alt text](image-5.png)
思路就是仿照上一节的MakeMenuBar函数来创建一个MakeToolBar函数.然后通过这个函数返回一个SWidget,然后将这个函数放到布局里面就可以了.
函数代码如下:
```cpp
TSharedRef<SWidget> MyEditor::MakeToolBar()
{
	FToolBarBuilder ToolBarBuilder(CommandList,FMultiBoxCustomization::None);
	ToolBarBuilder.BeginSection("MySection");
		ToolBarBuilder.AddToolBarButton(MyCommands::Get().OpenFileCommand);
		ToolBarBuilder.AddToolBarButton(MyCommands::Get().CloseFileCommand);
		ToolBarBuilder.AddToolBarButton(MyCommands::Get().SaveFileCommand);
	ToolBarBuilder.EndSection();

	return ToolBarBuilder.MakeWidget();
}
```

---
# SEditableText 文本编辑框
## 添加文本编辑框
其中**EditableText**是在头文件中声明的SEditableText类型的智能指针:TSharedPtr<SEditableText> EditableText;

```cpp
SNew(SVerticalBox)
+SVerticalBox::Slot()
[
SAssignNew(EditableText,SEditableText)
]
```
## 获取文本编辑框中的文字
这里展示通过按钮点击弹出消息框,消息框内容是文本编辑框中的文字的演示:
主要代码为:**EditableText->GetText()**,其中EditableText为添加文本编辑框时创建的SEditableText类型的智能指针.
```cpp
SNew(SButton)
.Text(FText::FromName(TabName[1]))
.OnClicked_Lambda(
	[this]() {
		FMessageDialog::Open(EAppMsgType::Ok, EditableText->GetText());
		return FReply::Handled();
	})
```

---
# SSplitter
>添加分割左右两边的分割条,左边为一个button,右边为一个button,左边的button大小是右边的button大小的二倍

![Alt text](image-6.png)

```cpp
SNew(SSplitter)
+SSplitter::Slot()
.Value(2.0f) // 设置这个槽占两份
[
	SNew(SButton)
	.Text(FText::FromName(TabName[2]))
]
+SSplitter::Slot()
[
	SNew(SButton)
	.Text(FText::FromName(TabName[2]))
]
```

---
#Sborder 填充
> 填充类型分为颜色填充和图像填充和九宫格填充
其中颜色填充需要新建一个**static**成员变量

效果如下:
![Alt text](image-7.png)
添加方法如下:
```cpp
static FSlateColorBrush ColorBrush = FSlateColorBrush(FLinearColor(1.0f, 1.0f, 0.0f, 1.0f));
SNew(SVerticalBox)
+SVerticalBox::Slot()
.FillHeight(1.f)
[
	// 颜色填充
	SNew(SBorder)
	.BorderImage(&ColorBrush)
]
+SVerticalBox::Slot()
[
	// 图像填充
	SNew(SBorder)
	.BorderImage(FCoreStyle::Get().GetBrush("Icons.Warning"))
]
+SVerticalBox::Slot()
[
	// Box填充(九宫格)
	SNew(SBorder)
	.BorderImage(FCoreStyle::Get().GetBrush("Debug.Border"))
]
```

---
# SOverlay
>SOverlay属于布局,用法也跟布局一样,这个布局的显示效果为:布局下的后创建的槽会覆盖前面创建的槽,就跟PS的图层一样,后创建的图层会覆盖之前的图层.

---
# SLeafWidget
> 可以通过继承SLeafWidget来创建自己的较简单的控件(这个控件不能够作为容器来包含其他控件).

具体代码参考：
## SMyLeafWidget.h
```cpp
#pragma once

#include "Widgets/SLeafWidget.h"

class SMyLeafWidget : public SLeafWidget
{
public:
	// 定义在SNew(SMyLeafWidget)时可以设置的属性(步骤参考SLATE_BEGIN_ARGS这个宏)
	SLATE_BEGIN_ARGS(SMyLeafWidget) 
		: _StartPoint(FVector2D(0,0))
		, _EndPoint(FVector2D(0,0))
	{

	}
	SLATE_ATTRIBUTE(FVector2D, StartPoint);
	SLATE_ATTRIBUTE(FVector2D, EndPoint);
	SLATE_END_ARGS()

	// 构造函数
	void Construct(const FArguments& InArgs);

private:

	TArray<FVector2D> Points;
    // 这两个函数是SLeafWidget声明的纯虚函数,因此必须定义
	virtual FVector2D ComputeDesiredSize(float) const override;
	virtual int32 OnPaint(
		const FPaintArgs& Args,
		const FGeometry& AllottedGeometry,
		const FSlateRect& MyCullingRect,
		FSlateWindowElementList& OutDrawElements,
		int32 LayerId,
		const FWidgetStyle& InWidgetStyle,
		bool bParentEnabled) const override;

};
```
## SMyLeafWidget.cpp
```cpp
#include "SMyLeafWidget.h"

void SMyLeafWidget::Construct(const FArguments& InArgs)
{
	// 因为_StartPoint和_EndPoint都是属性，因此需要通过Get()来获取属性的值
	Points.Add(InArgs._StartPoint.Get());
	Points.Add(InArgs._EndPoint.Get());
}

FVector2D SMyLeafWidget::ComputeDesiredSize(float) const
{
	return FVector2D(50, 50);
}

int32 SMyLeafWidget::OnPaint(
	const FPaintArgs& Args,
	const FGeometry& AllottedGeometry,
	const FSlateRect& MyCullingRect,
	FSlateWindowElementList& OutDrawElements,
	int32 LayerId,
	const FWidgetStyle& InWidgetStyle,
	bool bParentEnabled) const
{
	// 绘制一条线
	FSlateDrawElement::MakeLines(OutDrawElements, LayerId, AllottedGeometry.ToPaintGeometry(), Points);

	return LayerId++;
}

```
## FirstProgram.cpp(最终生成窗口使用控件的程序)
```cpp
// Copyright Epic Games, Inc. All Rights Reserved.


#include "FirstProgram.h"

#include "RequiredProgramMainCPPInclude.h"
#include "StandaloneRenderer.h"
#include "Framework/Application/SlateApplication.h"
#include "SMyleafWidget.h"

DEFINE_LOG_CATEGORY_STATIC(LogFirstProgram, Log, All);

IMPLEMENT_APPLICATION(FirstProgram, "FirstProgram");

/**
 * WinMain, called when the application is started
 */
int WINAPI WinMain(_In_ HINSTANCE hInInstance, _In_opt_ HINSTANCE hPrevInstance, _In_ LPSTR, _In_ int nCmdShow)
{
	// start up the main loop
	GEngineLoop.PreInit(GetCommandLineW());

	// crank up a normal Slate application using the platform's standalone renderer
	FSlateApplication::InitializeAsStandaloneApplication(GetStandardStandaloneRenderer());
	
	// 创建SMyLeafWidget控件的共享指针
	TSharedPtr<SMyLeafWidget> MyLeafWidget = 
		SNew(SMyLeafWidget)
		.StartPoint(FVector2D(0.f,0.f))
		.EndPoint(FVector2D(200.f,200.f));
	// 创建一个窗口
	TSharedPtr<SWindow> MainWindow = SNew(SWindow)
		.ClientSize(FVector2D(800, 600))
		[
			MyLeafWidget.ToSharedRef() // 共享指针转共享引用
			
		];

	FSlateApplication::Get().AddWindow(MainWindow.ToSharedRef());

	/*MyEditor::MyEditor();*/
	// loop while the server does the rest
	while (!IsEngineExitRequested())
	{
		FSlateApplication::Get().PumpMessages();
		FSlateApplication::Get().Tick();
	}

	FSlateApplication::Shutdown();

	return 0;
}


```

---
# SCompoundWidget
> 可以通过继承SCompoundWidget来创建自己的较复杂的控件(这个控件能够作为容器来包含其他控件,这是它与SLeafWidget的不同).

## SMyCompoundWidget.h
```cpp
#pragma once

class SMyCompoundWidget : public SCompoundWidget
{

public:
	SLATE_BEGIN_ARGS(SMyCompoundWidget)
		: _Content()
		, _HAlign(HAlign_Fill)
		, _VAlign(VAlign_Fill)
	{}

	SLATE_DEFAULT_SLOT(FArguments, Content) // 这个CompoundWidget有一个槽
	SLATE_ARGUMENT(EHorizontalAlignment, HAlign) // 可以通过HAlign调整左右对齐
	SLATE_ARGUMENT(EVerticalAlignment, VAlign) // 可以通过VAlign调整上下对齐

	SLATE_END_ARGS()
	void Construct(const FArguments& InArgs);
};
```

## SMyCompoundWidget.cpp
```cpp
#include "SMyCompoundWidget.h"

void SMyCompoundWidget::Construct(const FArguments& InArgs)
{
	ChildSlot
	.HAlign(InArgs._HAlign)
	.VAlign(InArgs._VAlign)
	[
		InArgs._Content.Widget
	];
}

```

---
# SCustomDialog

>**由于CustomDialog是编辑器使用的模块,因此不能够直接include来使用,所以找到其源文件复制到程序文件夹中进行使用.**
>将其复制到自己程序的文件夹中后改一下自己想要定义的名字,然后将其内容修改一下使其能够自己使用.

## SMyCustomDialog.h
```cpp
// Copyright Epic Games, Inc. All Rights Reserved.

#pragma once

#include "Widgets/SWindow.h"

/** This is a custom dialog class, which allows any Slate widget to be used as the contents,
 * with any number of buttons that have any text. 
 * It also supports adding a custom icon to the dialog.
 * Usage:
 * TSharedRef<SCustomDialog> HelloWorldDialog = SNew(SCustomDialog)
		.Title(FText(LOCTEXT("HelloWorldTitleExample", "Hello, World!")))
		.DialogContent( SNew(SImage).Image(FName(TEXT("Hello"))))
		.Buttons({
			SCustomDialog::FButton(LOCTEXT("OK", "OK")),
			SCustomDialog::FButton(LOCTEXT("Cancel", "Cancel"))
		});

   // returns 0 when OK is pressed, 1 when Cancel is pressed, -1 if the window is closed
   const int ButtonPressed = HelloWorldDialog->ShowModal();
 */
class SMyCustomDialog : public SWindow
{
public:
	struct FButton
	{
		FButton(const FText& InButtonText, const FSimpleDelegate& InOnClicked = FSimpleDelegate())
			: ButtonText(InButtonText),
			OnClicked(InOnClicked)
		{
		}

		FText ButtonText;
		FSimpleDelegate OnClicked;
	};

	SLATE_BEGIN_ARGS(SMyCustomDialog)
		: _UseScrollBox(true)
		, _ScrollBoxMaxHeight(300)
	{
		_AccessibleParams = FAccessibleWidgetData(EAccessibleBehavior::Auto);
	}
		/** Title to display for the dialog. */
		SLATE_ARGUMENT(FText, Title)

		/** Optional icon to display in the dialog. (default: none) */
		SLATE_ARGUMENT(FName, IconBrush)

		/** Should this dialog use a scroll box for over-sized content? (default: true) */
		SLATE_ARGUMENT(bool, UseScrollBox)

		/** Max height for the scroll box (default: 300) */
		SLATE_ARGUMENT(int32, ScrollBoxMaxHeight)

		/** The buttons that this dialog should have. One or more buttons must be added.*/
		SLATE_ARGUMENT(TArray<FButton>, Buttons)

		/** Content for the dialog */
		SLATE_ARGUMENT(TSharedPtr<SWidget>, DialogContent)

		/** Event triggered when the dialog is closed, either because one of the buttons is pressed, or the windows is closed. */
		SLATE_EVENT(FSimpleDelegate, OnClosed)

	SLATE_END_ARGS()

	void Construct(const FArguments& InArgs);

	/** Show the dialog.
	 * This method will return immediately.
	 */ 
	void Show();

	/** Show a modal dialog. Will block until an input is received.
	 * Returns the index of the button that was pressed.
	 */
	int32 ShowModal();

private:
	FReply OnButtonClicked(FSimpleDelegate OnClicked, int32 ButtonIndex);

	/** The index of the button that was pressed last. */
	int32 LastPressedButton = -1;

	FSimpleDelegate OnClosed;
};
```

## SMyCustomDialog.cpp

```cpp
// Copyright Epic Games, Inc. All Rights Reserved.

#include "SMyCustomDialog.h"

#include "HAL/PlatformApplicationMisc.h"

#include "Framework/Application/SlateApplication.h"
#include "Framework/Docking/TabManager.h"
#include "Logging/LogMacros.h"
#include "Styling/SlateBrush.h"
#include "Widgets/Images/SImage.h"
#include "Widgets/Input/SButton.h"
#include "Widgets/Text/STextBlock.h"
#include "Widgets/Layout/SSpacer.h"
#include "Widgets/Layout/SBox.h"
#include "Widgets/Layout/SScrollBox.h"
#include "Widgets/Layout/SUniformGridPanel.h"
#include "Widgets/SBoxPanel.h"

DEFINE_LOG_CATEGORY_STATIC(LogCustomDialog, Log, All);

void SMyCustomDialog::Construct(const FArguments& InArgs)
{
	UE_LOG(LogCustomDialog, Log, TEXT("Dialog displayed:"), *InArgs._Title.ToString());

	check(InArgs._Buttons.Num() > 0);
	
	OnClosed = InArgs._OnClosed;

	TSharedPtr<SHorizontalBox> ContentBox;
	TSharedPtr<SHorizontalBox> ButtonBox;

	SWindow::Construct( SWindow::FArguments()
		.Title(InArgs._Title)
		.SizingRule(ESizingRule::Autosized)
		.SupportsMaximize(false)
		.SupportsMinimize(false)
		[
			SNew(SBorder)
			.Padding(4.f)
			.BorderImage(FCoreStyle::Get().GetBrush( "ToolPanel.GroupBorder" ))
			[
				SNew(SVerticalBox)
				+ SVerticalBox::Slot()
				.FillHeight(1.0f)
				[
					SAssignNew(ContentBox, SHorizontalBox)
				]
				+ SVerticalBox::Slot()
				.VAlign(VAlign_Center)
				.AutoHeight()
				[
					SAssignNew(ButtonBox, SHorizontalBox)
				]
			]
		] );

	if (InArgs._IconBrush.IsValid())
	{
		const FSlateBrush* ImageBrush = FCoreStyle::Get().GetBrush(InArgs._IconBrush);
		if (ImageBrush != nullptr)
		{
			ContentBox->AddSlot()
				.AutoWidth()
				.VAlign(VAlign_Center)
				.HAlign(HAlign_Left)
				.Padding(0, 0, 8, 0)
				[
					SNew(SImage)
					.Image(ImageBrush)
				];
		}
	}

	if (InArgs._UseScrollBox)
	{
		ContentBox->AddSlot()
		[
			SNew(SBox)
			.MaxDesiredHeight(InArgs._ScrollBoxMaxHeight)
			[
				SNew(SScrollBox)
				+SScrollBox::Slot()
				[
					InArgs._DialogContent.ToSharedRef()
				]
			]
		];
	}
	else
	{
		ContentBox->AddSlot()
			.FillWidth(1.0f)
			.VAlign(VAlign_Center)
			.HAlign(HAlign_Left)
			[
				InArgs._DialogContent.ToSharedRef()
			];
	}

	ButtonBox->AddSlot()
		.AutoWidth()
		[
			SNew(SSpacer)
			.Size(FVector2D(20.0f, 1.0f))
		];

	TSharedPtr<SUniformGridPanel> ButtonPanel;

	ButtonBox->AddSlot() 
		.FillWidth(1.0f)
		.VAlign(VAlign_Center)
		.HAlign(HAlign_Right)
		[
			SAssignNew(ButtonPanel, SUniformGridPanel) // 控制按钮的大小
			.SlotPadding(0)
			.MinDesiredSlotWidth(100)
			.MinDesiredSlotHeight(30)
		];

	for (int32 i = 0; i < InArgs._Buttons.Num(); ++i)
	{
		const FButton& Button = InArgs._Buttons[i];

		ButtonPanel->AddSlot(ButtonPanel->GetChildren()->Num(), 0)
		[
			SNew(SButton)
			.OnClicked(FOnClicked::CreateSP(this, &SMyCustomDialog::OnButtonClicked, Button.OnClicked, i))
			[
				SNew(SHorizontalBox)
				+ SHorizontalBox::Slot()
				.VAlign(VAlign_Center)
				.HAlign(HAlign_Center)
				[
					SNew(STextBlock)
					.Text(Button.ButtonText)
				]
			]
		];
	}
}

int32 SMyCustomDialog::ShowModal()
{
	FSlateApplication::Get().AddModalWindow(StaticCastSharedRef<SWindow>(this->AsShared()), FGlobalTabmanager::Get()->GetRootWindow());

	return LastPressedButton;
}

void SMyCustomDialog::Show()
{
	TSharedRef<SWindow> Window = FSlateApplication::Get().AddWindow(StaticCastSharedRef<SWindow>(this->AsShared()), true);

	if (OnClosed.IsBound())
	{
		Window->GetOnWindowClosedEvent().AddLambda([this](const TSharedRef<SWindow>& Window) { OnClosed.Execute(); });
	}
}

/** Handle the button being clicked */
FReply SMyCustomDialog::OnButtonClicked(FSimpleDelegate OnClicked, int32 ButtonIndex)
{
	LastPressedButton = ButtonIndex;

	FSlateApplication::Get().RequestDestroyWindow(StaticCastSharedRef<SWindow>(this->AsShared()));

	OnClicked.ExecuteIfBound();
	return FReply::Handled();
}

```

## FirstProgram.cpp

```cpp
// Copyright Epic Games, Inc. All Rights Reserved.


#include "FirstProgram.h"

#include "RequiredProgramMainCPPInclude.h"
#include "StandaloneRenderer.h"
#include "Framework/Application/SlateApplication.h"
#include "SMyCanvas.h"
#include "MyEditor.h"
#include "SMyleafWidget.h"
#include "SMyCompoundWidget.h"
#include "SMyCustomDialog.h"
#include "Widgets/Input/SButton.h"

DEFINE_LOG_CATEGORY_STATIC(LogFirstProgram, Log, All);

IMPLEMENT_APPLICATION(FirstProgram, "FirstProgram");

/**
 * WinMain, called when the application is started
 */
int WINAPI WinMain(_In_ HINSTANCE hInInstance, _In_opt_ HINSTANCE hPrevInstance, _In_ LPSTR, _In_ int nCmdShow)
{
	// start up the main loop
	GEngineLoop.PreInit(GetCommandLineW());

	// crank up a normal Slate application using the platform's standalone renderer
	FSlateApplication::InitializeAsStandaloneApplication(GetStandardStandaloneRenderer());
	
	// 创建SMyCompoundWidget的共享指针
	TSharedPtr<SMyCompoundWidget> MyCompoundWidget =
		SNew(SMyCompoundWidget)
		.HAlign(EHorizontalAlignment::HAlign_Center)
		.VAlign(EVerticalAlignment::VAlign_Bottom)
		[
			// SNew(STextBlock).Text(FText::FromString(FString("Hello")))
			// 
 			SNew(SButton)
			.Text(FText::FromString(FString("ShowDialog"))) // UE5里面测试不加Text的话无法显示
  			.OnClicked_Lambda([]() {
  				// 弹出自定义对话框
  				TSharedRef<SMyCustomDialog> MyCustomDialog = SNew(SMyCustomDialog)
  				.Title(FText::FromString(FString("DialogTitle"))) // 定义标题
  				.DialogContent( // 定义dialog的内容
  					SNew(SVerticalBox)
  					+SVerticalBox::Slot()
  					[
  						SNew(STextBlock).Text(FText::FromString(FString("FirstRowText")))
  					]
  					+SVerticalBox::Slot()
  					[
  						SNew(STextBlock).Text(FText::FromString(FString("SecondRowText")))
  					]
  								)
  					.Buttons
  					({
  						SMyCustomDialog::FButton(FText::FromString(FString("Ok")))
  						});
  				MyCustomDialog->ShowModal();
  			return FReply::Handled();
  				})
		];

	// 创建一个窗口
	TSharedPtr<SWindow> MainWindow = SNew(SWindow)
		.ClientSize(FVector2D(800, 600))
		[
			MyCompoundWidget.ToSharedRef() // 共享指针转共享引用
		];

	FSlateApplication::Get().AddWindow(MainWindow.ToSharedRef());

	/*MyEditor::MyEditor();*/
	// loop while the server does the rest
	while (!IsEngineExitRequested())
	{
		FSlateApplication::Get().PumpMessages();
		FSlateApplication::Get().Tick();
	}

	FSlateApplication::Shutdown();

	return 0;
}

```

---
# SMultiLineEditableText
> SMultiLineEditableText是可以直接用的,它的作用是多行文本编辑器,这一节的教程中并没有介绍其所具有的其他方法(下一节会将为其添加滚动条).只介绍了通过继承前面所讲的SCompoundWidget,然后把它放里面,然后加了个SBorder,给SBorder设置颜色填充并添加SMultiLineEditableText的例子.这里展示一下.

## SMyMultiLineEditableText.h
```cpp
#pragma once
#include "Widgets/Text/SMultiLineEditableText.h"
class SMyMultiLineEditableText : public SCompoundWidget
{
public:
	SLATE_BEGIN_ARGS(SMyMultiLineEditableText)
	{}
	SLATE_END_ARGS()
	void Construct(const FArguments& InArgs);
};
```

## SMyMultiLineEditableText.cpp
```cpp
#include "SMyMultiLineEditableText.h"
void SMyMultiLineEditableText::Construct(const FArguments& InArgs)
{
	static FSlateColorBrush ColorBrush = FSlateColorBrush(FLinearColor(0.25f, 0.25f, 0.25f, 0.25f));
	ChildSlot
		[
			SNew(SBorder)
			.BorderImage(&ColorBrush)
			[
			SNew(SMultiLineEditableText)
			]
		];
}
```

## FirstProgram.cpp
```cpp
// Copyright Epic Games, Inc. All Rights Reserved.


#include "FirstProgram.h"

#include "RequiredProgramMainCPPInclude.h"
#include "StandaloneRenderer.h"
#include "Framework/Application/SlateApplication.h"
#include "SMyMultiLineEditableText.h"

DEFINE_LOG_CATEGORY_STATIC(LogFirstProgram, Log, All);

IMPLEMENT_APPLICATION(FirstProgram, "FirstProgram");

/**
 * WinMain, called when the application is started
 */
int WINAPI WinMain(_In_ HINSTANCE hInInstance, _In_opt_ HINSTANCE hPrevInstance, _In_ LPSTR, _In_ int nCmdShow)
{
	// start up the main loop
	GEngineLoop.PreInit(GetCommandLineW());

	// crank up a normal Slate application using the platform's standalone renderer
	FSlateApplication::InitializeAsStandaloneApplication(GetStandardStandaloneRenderer());

	// 创建SMyMultiLineEditableText的共享指针
	TSharedPtr<SMyMultiLineEditableText> MyMultiLineEditableText = SNew(SMyMultiLineEditableText);
	// 创建一个窗口
	TSharedPtr<SWindow> MainWindow = SNew(SWindow)
		.ClientSize(FVector2D(800, 600))
		[
			MyMultiLineEditableText.ToSharedRef() // 共享指针转共享引用
		];

	FSlateApplication::Get().AddWindow(MainWindow.ToSharedRef());

	/*MyEditor::MyEditor();*/
	// loop while the server does the rest
	while (!IsEngineExitRequested())
	{
		FSlateApplication::Get().PumpMessages();
		FSlateApplication::Get().Tick();
	}

	FSlateApplication::Shutdown();

	return 0;
}

```

---
# SScrollBar 滚动条
在上一节SMyMultiLineEditableText.cpp的基础上为文本编辑器添加滚动条
***SMyMultiLineEditableText.cpp***
```cpp
#include "SMyMultiLineEditableText.h"
void SMyMultiLineEditableText::Construct(const FArguments& InArgs)
{
	static FSlateColorBrush ColorBrush = FSlateColorBrush(FLinearColor(0.25f, 0.25f, 0.25f, 0.25f));

	TSharedPtr<SScrollBar> HorizontalScrollBar = SNew(SScrollBar).Orientation(EOrientation::Orient_Horizontal);
	TSharedPtr<SScrollBar> VerticalScrollBar = SNew(SScrollBar).Orientation(EOrientation::Orient_Vertical);
	ChildSlot
		[
			SNew(SBorder)
			.BorderImage(&ColorBrush)
			[
				SNew(SHorizontalBox)
				+ SHorizontalBox::Slot()
				.FillWidth(1.0f)
				[
					SNew(SVerticalBox)
					+ SVerticalBox::Slot()
					.FillHeight(1.0f)
					[
						SNew(SMultiLineEditableText)
						.HScrollBar(HorizontalScrollBar)
						.VScrollBar(VerticalScrollBar)
					]
					+ SVerticalBox::Slot()
					.AutoHeight()
					[
						HorizontalScrollBar.ToSharedRef() // 教程中是在这里使用SAssignNew来传递给智能指针的,但是在UE5里面没有成功,改成在定义的时候SNew就好了.
					]
				]
				+ SHorizontalBox::Slot()
				.AutoWidth()
				[
					VerticalScrollBar.ToSharedRef() // 同上注释
				]	
			]
		];
}


```

---
# FNotificationInfo 通知框
这里实现一个功能,当点击按钮时屏幕右下角会弹出通知框然后消失
![Alt text](image-8.png)
由于不需要额外创建类,这里只贴出关键代码
```cpp
#include "Widgets/Notifications/SNotificationList.h"
#include "Framework/Notifications/NotificationManager.h"
SNew(SButton)
.Text(FText::FromName(TabName[1]))
.OnClicked_Lambda(
	[&]() {
		FNotificationInfo Info(NSLOCTEXT("MainFrame", "RecompileInProgress", "Compiling C++ Code"));
		Info.ExpireDuration = 5.0f;
		Info.bFireAndForget = false;
		FSlateNotificationManager::Get().AddNotification(Info).Get()->Fadeout();

		return FReply::Handled();
	})
```