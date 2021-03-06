---
description: 了解详细信息： invalid_operation 类
title: invalid_operation 类
ms.date: 11/04/2016
f1_keywords:
- invalid_operation
- CONCRT/concurrency::invalid_operation
- CONCRT/concurrency::invalid_operation::invalid_operation
helpviewer_keywords:
- invalid_operation class
ms.assetid: 26ba07dc-fcdf-44cb-b748-a31d35205b52
ms.openlocfilehash: f3050d487f2c374f66f264b6e568fce5244d25ba
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97334543"
---
# <a name="invalid_operation-class"></a>invalid_operation 类

此类描述执行无效操作时引发的异常，由并发运行时引发的其他异常类型不会对此异常进行更为准确的描述。

## <a name="syntax"></a>语法

```cpp
class invalid_operation : public std::exception;
```

## <a name="members"></a>成员

### <a name="public-constructors"></a>公共构造函数

|“属性”|描述|
|----------|-----------------|
|[invalid_operation](#ctor)|已重载。 构造 `invalid_operation` 对象。|

## <a name="remarks"></a>备注

引发此异常的各种方法通常会记录它们将引发此异常的环境。

## <a name="inheritance-hierarchy"></a>继承层次结构

`exception`

`invalid_operation`

## <a name="requirements"></a>要求

**标头：** concrt

**命名空间：** 并发

## <a name="invalid_operation"></a><a name="ctor"></a> invalid_operation

构造 `invalid_operation` 对象。

```cpp
explicit _CRTIMP invalid_operation(_In_z_ const char* _Message) throw();

invalid_operation() throw();
```

### <a name="parameters"></a>parameters

*_Message*<br/>
错误的描述性消息。

## <a name="see-also"></a>请参阅

[并发命名空间](concurrency-namespace.md)
