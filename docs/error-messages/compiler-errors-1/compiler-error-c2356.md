---
description: 了解更多：编译器错误 C2356
title: 编译器错误 C2356
ms.date: 11/04/2016
f1_keywords:
- C2356
helpviewer_keywords:
- C2356
ms.assetid: 84d5a816-9a61-4d45-9978-38e485bbf767
ms.openlocfilehash: c0e2d179bb41e6cbae674d92976674ab90f05c0f
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97328331"
---
# <a name="compiler-error-c2356"></a>编译器错误 C2356

初始化段在翻译单元期间不能更改

可能的原因：

- `#pragma init_seg` 前面是段初始化代码

- `#pragma init_seg` 前面有另一个 `#pragma init_seg`

若要解决此问题，请将段初始化代码移到模块的开头。 如果必须初始化多个区域，请将它们移到单独的模块中。

下面的示例生成 C2356：

```cpp
// C2356.cpp
#pragma warning(disable : 4075)

int __cdecl myexit(void (__cdecl *)());
int __cdecl myexit2(void (__cdecl *)());

#pragma init_seg(".mine$m",myexit)
#pragma init_seg(".mine$m",myexit2)   // C2356
```
