---
description: 了解有关以下内容的详细信息：用于引用类型的 c + + 堆栈语义
title: 参考类型的 C++ 堆栈语义
ms.date: 11/04/2016
helpviewer_keywords:
- reference types, C++ stack semantics for
ms.assetid: 319a1304-f4a4-4079-8b84-01cec847d531
ms.openlocfilehash: a7f377225e70eff4093d4b9820a3d14644b96f58
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97124314"
---
# <a name="c-stack-semantics-for-reference-types"></a>参考类型的 C++ 堆栈语义

在 Visual Studio 2005 之前，只能使用在 **`new`** 垃圾回收堆上创建对象的运算符来创建引用类型的实例。 但是现在，您可以使用用来在堆栈上创建本机类型的实例的相同语法创建引用类型的实例。 因此，不需要使用 [ref new、gcnew](../extensions/ref-new-gcnew-cpp-component-extensions.md) 来创建引用类型的对象。 此外，当对象超出范围时，编译器将调用对象的析构函数。

## <a name="remarks"></a>备注

使用堆栈语义创建引用类型的实例时，编译器会在内部使用) 在垃圾回收堆上创建实例 (**`gcnew`** 。

当函数的签名或返回类型包括一个按值引用类型的实例时，会在元数据中将此函数标记为需要特殊处理（使用 modreq）。 此特殊处理当前仅由 Visual C++ 客户端提供；其他语言当前不支持使用借助堆栈语义创建的引用类型的使用函数或数据。

**`gcnew`** 如果该类型没有析构函数，则使用 (动态分配) 而不是堆栈语义的一个原因就是。 此外，如果您希望由 Visual C++ 之外的语言使用您的函数，则无法使用在函数签名中借助堆栈语义创建的引用类型。

编译器将不会为引用类型生成复制构造函数。 因此，如果在签名中定义了使用按值引用类型的函数，则必须为该引用类型定义一个复制构造函数。 引用类型的复制构造函数具有以下形式的签名：`R(R%){}`。

编译器不会为引用类型生成默认的赋值运算符。 赋值运算符允许您使用堆栈语义创建一个对象，并且借助使用堆栈语义创建的现有对象对其进行初始化。 引用类型的赋值运算符具有以下形式的签名：`void operator=( R% ){}`。

如果类型的析构函数释放关键资源并对引用类型使用 stack 语义，则不需要显式调用析构函数 (或调用 **`delete`**) 。 有关引用类型中的析构函数的详细信息，请参阅 [如何：定义和使用类和结构 (c + +/cli) 中的析构函数和终结 ](../dotnet/how-to-define-and-consume-classes-and-structs-cpp-cli.md#BKMK_Destructors_and_finalizers)器。

编译器生成的赋值运算符将遵循标准的 C++ 规则以及以下额外规则：

- 任何类型为指向引用类型的句柄的非静态数据成员都将被浅表复制（处理方式与类型为指针的非静态数据成员一样）。

- 任何类型为值类型的非静态数据成员都将被浅表复制。

- 任何类型为引用类型的实例的非静态数据成员都将调用引用类型的复制构造函数。

编译器还提供 `%` 一元运算符，以将使用堆栈语义创建的引用类型的实例转换为其基础句柄类型。

以下引用类型不可与堆栈语义一起使用：

- [委托（C++ 组件扩展）](../extensions/delegate-cpp-component-extensions.md)

- [数组](../extensions/arrays-cpp-component-extensions.md)

- <xref:System.String>

## <a name="example"></a>示例

### <a name="description"></a>描述

以下代码示例演示了如何使用堆栈语义声明引用类型的实例，赋值运算符和复制构造函数如何工作，以及如何借助使用堆栈语义创建的引用类型来初始化跟踪引用。

### <a name="code"></a>代码

```cpp
// stack_semantics_for_reference_types.cpp
// compile with: /clr
ref class R {
public:
   int i;
   R(){}

   // assignment operator
   void operator=(R% r) {
      i = r.i;
   }

   // copy constructor
   R(R% r) : i(r.i) {}
};

void Test(R r) {}   // requires copy constructor

int main() {
   R r1;
   r1.i = 98;

   R r2(r1);   // requires copy constructor
   System::Console::WriteLine(r1.i);
   System::Console::WriteLine(r2.i);

   // use % unary operator to convert instance using stack semantics
   // to its underlying handle
   R ^ r3 = %r1;
   System::Console::WriteLine(r3->i);

   Test(r1);

   R r4;
   R r5;
   r5.i = 13;
   r4 = r5;   // requires a user-defined assignment operator
   System::Console::WriteLine(r4.i);

   // initialize tracking reference
   R % r6 = r4;
   System::Console::WriteLine(r6.i);
}
```

### <a name="output"></a>Output

```Output
98
98
98
13
13
```

## <a name="see-also"></a>请参阅

[类和结构](../extensions/classes-and-structs-cpp-component-extensions.md)
