---
description: 了解更多：编译器错误 C2790
title: 编译器错误 C2790
ms.date: 11/04/2016
f1_keywords:
- C2790
helpviewer_keywords:
- C2790
ms.assetid: 38d4fce1-ba00-413d-8bc1-e8aa43d7bc1f
ms.openlocfilehash: 0913b87f40e7f4ad2ecccb333e67bb0d76b4afde
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97297793"
---
# <a name="compiler-error-c2790"></a>编译器错误 C2790

"super"：该关键字只能在类成员函数体内使用

如果用户曾经尝试在成员函数的上下文之外使用关键字 [super](../../cpp/super.md) ，则会出现此错误消息。

下面的示例生成 C2790：

```cpp
// C2790.cpp
void f() {
   __super::g();   // C2790
}
```
