---
description: 了解更多：编译器错误 C3278
title: 编译器错误 C3278
ms.date: 11/04/2016
f1_keywords:
- C3278
helpviewer_keywords:
- C3278
ms.assetid: 56f818f5-85a6-4792-843b-54fe16327658
ms.openlocfilehash: cdbb53b4f11357ae9058d9a5ebc3882c8701fc88
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97228958"
---
# <a name="compiler-error-c3278"></a>编译器错误 C3278

> 接口或纯方法 "*method*" 的直接调用将在运行时失败

## <a name="remarks"></a>备注

对接口方法或纯方法进行了调用，这是不允许的。

## <a name="example"></a>示例

以下示例生成 C3278：

```cpp
// C3278_2.cpp
// compile with: /clr
using namespace System;
interface class I
{
   void vmf();
};

public ref class C: public I
{
public:
   void vmf()
   {
      Console::WriteLine( "In C::vmf()" );
      I::vmf(); // C3278
   }

};

int main()
{
   C^ pC = gcnew C;
   pC->vmf();
}
```
