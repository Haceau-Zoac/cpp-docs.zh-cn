---
description: 了解详细信息： Platform：： WeakReference 类
title: Platform::WeakReference 类
ms.date: 12/30/2016
ms.topic: reference
f1_keywords:
- Platform::WeakReference
ms.assetid: 8cfe1977-a8c7-4b7b-b539-25c77ed4c5f1
ms.openlocfilehash: edf3220d8916ff4bdb1462f3dd04149a4e9a9709
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97307790"
---
# <a name="platformweakreference-class"></a>Platform::WeakReference 类

表示对 ref 类实例的弱引用。

## <a name="syntax"></a>语法

```cpp
class WeakReference
```

#### <a name="parameters"></a>parameters

### <a name="members"></a>成员

### <a name="constructors"></a>构造函数

|成员|描述|
|------------|-----------------|
|[WeakReference：： WeakReference](#ctor)|初始化 WeakReference 类的新实例。|

### <a name="methods"></a>方法

|成员|描述|
|------------|-----------------|
|[WeakReference：： Resolve](#resolve)|如果对象不再存在，则返回基础 ref 类的句柄或 nullptr。|

### <a name="operators"></a>运算符

|成员|描述|
|------------|-----------------|
|[WeakReference::operator=](#operator-assign)|给 WeakReference 对象赋新值。|
|[WeakReference::operator BoolType](#booltype)|实现安全 bool 模式。|

### <a name="remarks"></a>备注

WeakReference 类本身不是 ref 类，因此不从 Platform::Object^ 继承，也不能在公共方法的签名中使用。

## <a name="weakreferenceoperator"></a><a name="operator-assign"></a> WeakReference：： operator =

给 WeakReference 赋值。

### <a name="syntax"></a>语法

```cpp
WeakReference& operator=(decltype(__nullptr));
WeakReference& operator=(const WeakReference& otherArg);
WeakReference& operator=(WeakReference&& otherArg);
WeakReference& operator=(const volatile ::Platform::Object^ const otherArg);
```

### <a name="remarks"></a>备注

使用上面列表中的最后一个重载，可以向 WeakReference 变量分配 ref 类。 在这种情况下，ref 类向 [Platform：： Object](../cppcx/platform-object-class.md)^ 向下转换。 稍后可通过将原始类型指定为[WeakReference：： Resolve \<T> ](#resolve)成员函数中类型参数的参数来还原原始类型。

## <a name="weakreferenceoperator-booltype"></a><a name="booltype"></a> WeakReference：： operator BoolType

实现 WeakReference 类的安全 bool 模式。 不在你的代码中显式调用。

### <a name="syntax"></a>语法

```cpp
BoolType BoolType();
```

## <a name="weakreferenceresolve-method-platform-namespace"></a><a name="resolve"></a> WeakReference：： Resolve 方法 (平台命名空间) 

返回原始 ref 类的句柄， **`nullptr`** 如果对象不再存在，则返回。

### <a name="syntax"></a>语法

```cpp
template<typename T>
T^ Resolve() const;
```

### <a name="parameters"></a>parameters

### <a name="property-valuereturn-value"></a>属性值/返回值

WeakReference 对象先前关联的 ref 类的句柄或 nullptr。

### <a name="example"></a>示例

```cpp
Bar^ bar = ref new Bar();
//use bar...

if (bar != nullptr)
{
    WeakReference wr(bar);
    Bar^ newReference = wr.Resolve<Bar>();
}
```

注意类型参数是 T 而非 T^。

## <a name="weakreferenceweakreference-constructor"></a><a name="ctor"></a> WeakReference：： WeakReference 构造函数

提供构造 WeakReference 的各种方式。

### <a name="syntax"></a>语法

```cpp
WeakReference();
WeakReference(decltype(__nullptr));
WeakReference(const WeakReference& otherArg);
WeakReference(WeakReference&& otherArg);
explicit WeakReference(const volatile ::Platform::Object^ const otherArg);
```

### <a name="example"></a>示例

```cpp
MyClass^ mc = ref new MyClass();
WeakReference wr(mc);
MyClass^ copy2 = wr.Resolve<MyClass>();
```

## <a name="see-also"></a>请参阅

[Platform 命名空间](../cppcx/platform-namespace-c-cx.md)
