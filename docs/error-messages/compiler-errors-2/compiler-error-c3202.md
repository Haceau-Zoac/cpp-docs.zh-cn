---
description: 了解更多：编译器错误 C3202
title: 编译器错误 C3202
ms.date: 11/04/2016
f1_keywords:
- C3202
helpviewer_keywords:
- C3202
ms.assetid: 23528a0c-5493-4804-9789-cd3c38e49fb9
ms.openlocfilehash: d3f090128a5290521aa64f9d834c200783bc2011
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97291865"
---
# <a name="compiler-error-c3202"></a>编译器错误 C3202

“arg name”：模板参数“parameter”的默认参数无效，应为类模板

你向模板参数传递的默认参数无效。

下面的示例生成 C3202：

```cpp
// C3202.cpp
template<typename T>
class X
{
};

class Z
{
};

template<template<typename U> class T1 = Z, typename T2> // C3202
class Y
{
};
```
