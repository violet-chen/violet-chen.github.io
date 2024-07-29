---
title: UEC++
tags: UEC++
categories: UE开发
abbrlink: 320b2819
date: 2023-09-13 10:25:00
---

> 这里是UEC++的学习记录.
初次接触UEC++,特别是基础还不是太好时,首先可以看一下这个知乎文章[虚幻引擎编译系统总结](https://zhuanlan.zhihu.com/p/458435453).
其他遇到的相关知识点就可以先看C++的笔记中的记录.
# 常见的命名约定前缀
- U开头：通常表示继承自 UObject 的类或类的实例，它们是虚幻引擎的对象。UObject 是UE中所有对象的基类，它提供了一些通用的功能，如引用计数、反射系统等。因此，以"U"开头的类通常是虚幻引擎的核心对象。例如：UActorComponent, UStaticMeshComponent, UCharacterMovementComponent。
- A开头：通常表示继承自 AActor 的类或类的实例，表示游戏中的一个实体或角色。AActor 是UE中表示游戏实体的基类。例如：ACharacter, APlayerController, AProjectile.
- F开头：通常表示代理（Delegate）或结构体（Struct），用于在代码中定义事件、回调和数据结构。例如：FVector, FRotator, FOnClicked.
- S开头：通常表示继承自 SWidget 的类或类的实例，表示UI小部件。SWidget 是Slate框架中用于构建用户界面的基类。例如：SButton, SImage, STextBlock.
- I开头：通常表示接口（Interface），用于定义一组要被其他类实现的方法。例如：IInteractionInterface, IMovementInterface.
- E开头：通常表示枚举类型（Enum），用于定义一组相关的命名常数。例如：ECharacterState, EWeaponType, EMovementDirection.
- T开头：通常表示模板类（Template class），用于创建可以在多种数据类型上操作的通用代码。例如：TArray, TMap, TSharedPtr.
- b开头: 布尔变量必须以b为前缀（例如 bPendingDestruction 或 bHasFadedIn）。
# 常见的C++宏以及定义
## 对象声明和属性
- UCLASS：用于声明一个类，使其能够在Unreal Engine中使用，自动生成蓝图类的功能，并继承自UObject。
- USTRUCT：用于声明一个结构体，使其能够在UE中使用，与UCLASS类似，但用于结构体。
- UENUM：用于声明一个枚举类型，使其能够在UE中使用，允许在蓝图和代码中使用。
- UPROPERTY：用于声明类的属性（成员变量），使其可以在编辑器中显示和编辑。
- UFUNCTION：用于声明成员函数，使其能够在蓝图中调用，绑定到事件，并支持远程过程调用（RPC）。
- UDELEGATE：用于声明委托类型，用于处理事件、回调和通信。
- UINTERFACE：用于声明一个接口，允许类实现相应的功能。
- GENERATED_BODY：用于类声明内部，表示自动生成的C++代码的开始。
- GENERATED_UCLASS_BODY：类似于GENERATED_BODY，但用于旧版本的代码生成。
- GENERATED_USTRUCT_BODY：类似于GENERATED_BODY，但用于结构体。
## 日志和断言
- DEFINE_LOG_CATEGORY：定义一个日志类别，用于记录日志消息。
- DECLARE_LOG_CATEGORY_EXTERN：声明一个外部的日志类别，通常在不同文件中共享日志类别。
- UE_LOG：用于在代码中记录日志消息。
- CHECK / VERIFY：用于在运行时进行断言检查，如果条件不满足，则触发断言失败。
## 模块和应用程序
- IMPLEMENT_PRIMARY_GAME_MODULE：实现主游戏模块，指定游戏模块的入口点和初始化代码。
- IMPLEMENT_MODULE：实现一个模块，允许扩展UE的功能。
## 平台和翻译
- PLATFORM_XXX：用于在特定平台上编译代码块，如PLATFORM_WINDOWS、PLATFORM_MAC等。
- WITH_EDITOR：用于在编辑器环境下编译代码块。
- WITH_EDITORONLY：用于在编辑器环境下编译代码块，运行时被忽略。
## 蓝图和脚本
- UE_DEPRECATED：标记已弃用的函数、变量或类，用于向后兼容。
- TEXT：创建FText本地化字符串字面值。
- NSLOCTEXT：创建本地化字符串，支持多语言。
- LOCTEXT_NAMESPACE：设置本地化命名空间，用于区分不同的本地化字符串。
## Slate相关
- SNew: 用于创建 Slate 控件的实例
- SLATE_BEGIN_ARGS / SLATE_END_ARGS：用于定义 Slate 控件的构造参数，允许在构造时设置初始属性。
- SLATE_ATTRIBUTE：用于创建一个属性对象，使得可以将数据源（如属性或委托）绑定到控件属性。
- SLATE_ARGUMENT：用于在构造参数中定义控件的属性，使得可以在创建控件时传递值。
- SLATE_NAMED_SLOT：用于在控件内部定义一个命名插槽，使得可以在使用时填充内容。
- SLATE_EVENT: 用于定义委托事件，以便在控件上绑定和触发事件。
- BEGIN_SLATE_FUNCTION_BUILD_OPTIMIZATION / END_SLATE_FUNCTION_BUILD_OPTIMIZATION：用于标记一段代码，以进行 Slate 控件构建优化，以提高性能。
- IMPLEMENT_SIMPLE_AUTOMATION_TEST：用于实现一个简单的自动化测试，以验证 Slate 控件的行为。
