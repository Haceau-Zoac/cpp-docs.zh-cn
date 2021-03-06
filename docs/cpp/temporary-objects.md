---
description: 了解详细信息：临时对象
title: 临时对象
ms.date: 11/04/2016
helpviewer_keywords:
- temporary objects
- objects [C++], temporary
ms.assetid: 4c8cec02-391e-4225-9bc6-06d150201412
ms.openlocfilehash: d827568013b3684c2126887d390ecbf223c46da5
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97164739"
---
# <a name="temporary-objects"></a>临时对象

在某些情况下，编译器需要创建临时对象。 可能会出于下列原因创建这些临时对象：

- **`const`** 使用与要初始化的引用的基础类型的初始值设定项不同的类型的初始值设定项初始化引用。

- 存储返回用户定义类型的函数的返回值。 仅当您的程序未将返回值复制到对象时，才会创建这些临时内存。 例如：

    ```cpp
    UDT Func1();    //  Declare a function that returns a user-defined
                    //   type.

    ...

    Func1();        //  Call Func1, but discard return value.
                    //  A temporary object is created to store the return
                    //   value.
    ```

   由于未将返回值复制到另一个对象，因此创建了临时对象。 创建临时内存更常见的情况是在计算必须调用重载运算符函数的表达式时。 这些重载运算符函数将返回一般不会复制到其他对象的用户定义的类型。

   请考虑表达式 `ComplexResult = Complex1 + Complex2 + Complex3`。 将计算表达式 `Complex1 + Complex2`，并且结果将存储在临时对象中。 接下来，计算表达式 *临时* `+ Complex3` ，并将结果复制到 `ComplexResult` (假设赋值运算符未) 重载。

- 存储强制转换为用户定义的类型的结果。 在给定类型的对象显式转换为用户定义的类型时，将构造一个新对象作为临时对象。

临时对象具有根据其创建点和销毁点定义的生存期。 创建多个临时对象的表达式最终会按与这些对象的创建顺序相反的顺序来销毁它们。 下表中显示了析构发生的时点。

### <a name="destruction-points-for-temporary-objects"></a>临时对象的析构点

|创建临时项的原因|析构点|
|------------------------------|-----------------------|
|表达式计算的结果|表达式求值的结果中创建的所有临时内存将在表达式语句的末尾销毁 (即在分号) ，或在、、、 **`for`** **`if`** **`while`** **`do`** 和 **`switch`** 语句的控制表达式的末尾。|
|初始化 **`const`** 引用|如果初始值设定项不是与所初始化引用相同类型的左值，则将用初始化表达式创建和初始化基础对象类型的临时项。 此临时对象将在其绑定到的引用对象销毁后立即销毁。|
