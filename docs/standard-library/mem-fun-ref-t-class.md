---
description: 了解详细信息： mem_fun_ref_t 类
title: mem_fun_ref_t 类
ms.date: 02/21/2019
f1_keywords:
- functional/std::mem_fun_ref_t
helpviewer_keywords:
- mem_fun_ref_t class
ms.assetid: 7dadcac3-8d33-4e4b-a792-81bd53d3df39
ms.openlocfilehash: e79d7f3b3271ff699f0dd2ad760753c2162d554a
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97149170"
---
# <a name="mem_fun_ref_t-class"></a>mem_fun_ref_t 类

一种适配器类， `non_const` 在使用引用自变量进行初始化时，该类允许将不带任何参数的成员函数作为一元函数对象调用。 在 c + + 11 中已弃用，在 c + + 17 中删除。

## <a name="syntax"></a>语法

```cpp
template <class Result, class Type>
class mem_fun_ref_t : public unary_function<Type, Result> {
    explicit mem_fun_ref_t(
    Result (Type::* _Pm)());

    Result operator()(Type& left) const;
};
```

### <a name="parameters"></a>parameters

*_Pm*\
一个指针，指向要转换为函数对象的 `Type` 类成员函数。

*左中*\
在其上调用 *_Pm* 成员函数的对象。

## <a name="return-value"></a>返回值

一个自适应一元函数。

## <a name="remarks"></a>备注

类模板 `Type` 在私有成员对象中存储 _Pm 的副本，该副本必须是指向类的成员函数的指针。 它将其成员函数定义 `operator()` 为 (**left** 返回。 * `_Pm`) # A2 # A3。

## <a name="example"></a>示例

通常不直接使用 `mem_fun_ref_t` 的构造函数；helper 函数 `mem_fun_ref` 用于调整成员函数。 有关如何使用成员函数适配器的示例，请参阅 [mem_fun_ref](../standard-library/functional-functions.md#mem_fun_ref)。
