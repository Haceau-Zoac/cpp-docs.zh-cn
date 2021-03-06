---
description: 了解详细信息： task_continuation_context 类
title: task_continuation_context 类
ms.date: 11/04/2016
f1_keywords:
- task_continuation_context
- PPLTASKS/concurrency::task_continuation_context
- PPLTASKS/concurrency::task_continuation_context::get_current_winrt_context
- PPLTASKS/concurrency::task_continuation_context::use_arbitrary
- PPLTASKS/concurrency::task_continuation_context::use_current
- PPLTASKS/concurrency::task_continuation_context::use_default
- PPLTASKS/concurrency::task_continuation_context::use_synchronous_execution
helpviewer_keywords:
- task_continuation_context class
ms.assetid: 1fb5a76a-3682-45c2-a615-8b6b527741f0
ms.openlocfilehash: ff843a84dd3e0bdaeee9df99e91b1708116191d3
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97188295"
---
# <a name="task_continuation_context-class"></a>task_continuation_context 类

`task_continuation_context` 类可让你指定想要执行延续的位置。 仅在 Windows 运行时应用中使用此类时才有用。 对于非 Windows 运行时应用，任务延续的执行上下文由运行时确定，并且不可配置。

## <a name="syntax"></a>语法

```cpp
class task_continuation_context : public details::_ContextCallback;
```

## <a name="members"></a>成员

### <a name="public-methods"></a>公共方法

|“属性”|描述|
|----------|-----------------|
|[get_current_winrt_context](#get_current_winrt_context)|返回表示当前 winrt 线程上下文的任务延续上下文对象。|
|[use_arbitrary](#use_arbitrary)|创建允许运行时选择延续的执行上下文的任务延续上下文。|
|[use_current](#use_current)|返回表示当前执行上下文的任务延续上下文对象。|
|[use_default](#use_default)|创建默认任务延续上下文。|
|[use_synchronous_execution](#use_synchronous_execution)|返回表示同步执行上下文的任务延续上下文对象。|

## <a name="inheritance-hierarchy"></a>继承层次结构

`_ContextCallback`

`task_continuation_context`

## <a name="requirements"></a>要求

**标头：** ppltasks。h

**命名空间：** 并发

## <a name="get_current_winrt_context"></a><a name="get_current_winrt_context"></a> get_current_winrt_context

返回表示当前 WinRT 线程上下文的任务延续上下文对象。

### <a name="syntax"></a>语法

```cpp
static task_continuation_context get_current_winrt_context();
```

### <a name="return-value"></a>返回值

当前 Windows 运行时线程上下文。 如果从非 Windows 运行时上下文中调用，则返回空 task_continuation_context。

### <a name="remarks"></a>备注

`get_current_winrt_context`方法捕获调用方的 Windows 运行时线程上下文。 它将向非 Windows 运行时调用方返回一个空的上下文。

返回的值 `get_current_winrt_context` 可用于向运行时指示延续应在 (STA 与 MTA) 的捕获上下文的单元模型中执行，而不管前面的任务是否是单元感知。 单元识别任务是一种将 Windows 运行时 `IAsyncInfo` 接口或从这类任务继承的任务的任务。

此方法与  `use_current` 方法类似，但也可用于不支持 c + +/cx 扩展的本机 c + + 代码。 它旨在供高级用户使用，用于为本机和 Windows 运行时调用方编写 c + +/CX-agnostic 库代码。 除非需要此功能，否则建议 `use_current` 仅可用于 c + +/cx 客户端的方法。

## <a name="use_arbitrary"></a><a name="use_arbitrary"></a> use_arbitrary

创建允许运行时选择延续的执行上下文的任务延续上下文。

### <a name="syntax"></a>语法

```cpp
static task_continuation_context use_arbitrary();
```

### <a name="return-value"></a>返回值

表示任意位置的任务延续上下文。

### <a name="remarks"></a>备注

使用此延续上下文时，延续将在运行时选择的上下文中执行，即使前面的任务是单元感知也是如此。

`use_arbitrary` 可用于关闭在 STA 中创建的单元感知任务的默认行为。

此方法仅可用于 Windows 运行时应用。

## <a name="use_current"></a><a name="use_current"></a> use_current

返回表示当前执行上下文的任务延续上下文对象。

```cpp
static task_continuation_context use_current();
```

### <a name="return-value"></a>返回值

当前执行上下文。

### <a name="remarks"></a>备注

此方法捕获调用方的 Windows 运行时上下文，以便可在右单元中执行延续任务。

返回的值 `use_current` 可用于向运行时指示延续应在 (STA 与 MTA) 的捕获上下文中执行，而不考虑前面的任务是否可识别单元。 单元识别任务是一种将 Windows 运行时 `IAsyncInfo` 接口或从这类任务继承的任务的任务。

此方法仅可用于 Windows 运行时应用。

## <a name="use_default"></a><a name="use_default"></a> use_default

创建默认任务延续上下文。

```cpp
static task_continuation_context use_default();
```

### <a name="return-value"></a>返回值

默认延续上下文。

### <a name="remarks"></a>备注

如果在调用方法时未指定延续上下文，则使用默认上下文 `then` 。 在 windows 7 及更高版本的 Windows 应用程序以及 Windows 8 及更高版本上的桌面应用程序中，运行时确定任务继续执行的位置。 但是，在 Windows 运行时应用程序中，可在单元识别任务上继续执行的默认延续上下文是调用的单元 `then` 。

单元识别任务是一种将 Windows 运行时 `IAsyncInfo` 接口或从这类任务继承的任务的任务。 因此，如果在 Windows 运行时 STA 中的单元感知任务上计划继续，则延续任务将在该 STA 中执行。

非单元识别任务上的延续将在运行时选择的上下文中执行。

## <a name="task_continuation_contextuse_synchronous_execution"></a><a name="use_synchronous_execution"></a> task_continuation_context：： use_synchronous_execution

返回表示同步执行上下文的任务延续上下文对象。

### <a name="syntax"></a>语法

```cpp
static task_continuation_context use_synchronous_execution();
```

### <a name="return-value"></a>返回值

同步执行上下文。

### <a name="remarks"></a>备注

`use_synchronous_execution`方法强制延续任务在上下文上同步运行，从而导致前面的任务完成。

如果在附加延续后前面的任务已完成，则延续将在附加延续的上下文中同步运行。

## <a name="see-also"></a>请参阅

[并发命名空间](concurrency-namespace.md)
