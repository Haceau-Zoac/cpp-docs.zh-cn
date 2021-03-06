---
description: 了解详细信息： CDBPropIDSet 类
title: CDBPropIDSet 类
ms.date: 11/04/2016
f1_keywords:
- CDBPropIDSet
- ATL.CDBPropIDSet
- ATL::CDBPropIDSet
- CDBPropIDSet.AddPropertyID
- CDBPropIDSet::AddPropertyID
- AddPropertyID
- ATL.CDBPropIDSet.AddPropertyID
- ATL::CDBPropIDSet::AddPropertyID
- ATL::CDBPropIDSet::CDBPropIDSet
- CDBPropIDSet.CDBPropIDSet
- CDBPropIDSet::CDBPropIDSet
- ATL.CDBPropIDSet.CDBPropIDSet
- CDBPropIDSet.operator=
- ATL.CDBPropIDSet.operator=
- ATL::CDBPropIDSet::operator=
- CDBPropIDSet::operator=
- CDBPropIDSet.SetGUID
- ATL::CDBPropIDSet::SetGUID
- ATL.CDBPropIDSet.SetGUID
- CDBPropIDSet::SetGUID
helpviewer_keywords:
- CDBPropIDSet class
- AddPropertyID method
- CDBPropIDSet class, constructor
- operator =, property sets
- = operator, with OLE DB templates
- operator=, property sets
- SetGUID method
ms.assetid: 52bb806c-9581-494d-9af7-50d8a4834805
ms.openlocfilehash: 6f0c3ea19daeef2b262f6ac1ad76599160baf266
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97170823"
---
# <a name="cdbpropidset-class"></a>CDBPropIDSet 类

继承自 `DBPROPIDSET` 结构，并添加一个用于初始化键字段以及 [AddPropertyID](#addpropertyid) 访问方法的构造函数。

## <a name="syntax"></a>语法

```cpp
class CDBPropIDSet : public tagDBPROPIDSET
```

## <a name="requirements"></a>要求

**标头:** atldbcli.h

## <a name="members"></a>成员

### <a name="methods"></a>方法

| 名称 | 描述 |
|-|-|
|[AddPropertyID](#addpropertyid)|将属性添加到属性 ID 集。|
|[CDBPropIDSet](#cdbpropidset)|构造函数。|
|[SetGUID](#setguid)|设置属性 ID 集的 GUID。|

### <a name="operators"></a>运算符

| 名称 | 描述 |
|-|-|
|[operator =](#op_equal)|将属性 ID 集的内容分配到另一个属性 ID 集。|

## <a name="remarks"></a>备注

OLE DB 使用者使用 `DBPROPIDSET` 结构传递属性 id 的数组，使用者想要获取属性信息。 单个 [DBPROPIDSET](/previous-versions/windows/desktop/ms717981(v=vs.85)) 结构中标识的属性属于一个属性集。

## <a name="cdbpropidsetaddpropertyid"></a><a name="addpropertyid"></a> CDBPropIDSet：： AddPropertyID

将属性 ID 添加到属性 ID 集中。

### <a name="syntax"></a>语法

```cpp
bool AddPropertyID(DBPROPID propid) throw();
```

#### <a name="parameters"></a>parameters

*propid*<br/>
[in] 要添加到属性 ID 集中的属性 ID。

## <a name="cdbpropidsetcdbpropidset"></a><a name="cdbpropidset"></a> CDBPropIDSet：： CDBPropIDSet

构造函数。 初始化 `rgProperties` `cProperties` DBPROPIDSET 结构的、和 (可选择) `guidPropertySet` 字段[](/previous-versions/windows/desktop/ms717981(v=vs.85)) 。

### <a name="syntax"></a>语法

```cpp
CDBPropIDSet(const GUID& guid);

CDBPropIDSet(const CDBPropIDSet& propidset);

CDBPropIDSet();
```

#### <a name="parameters"></a>parameters

*guid*<br/>
中用于初始化字段的 GUID `guidPropertySet` 。

*propidset*<br/>
[in] 复制构造的另一个 `CDBPropIDSet` 对象。

## <a name="cdbpropidsetsetguid"></a><a name="setguid"></a> CDBPropIDSet：： SetGUID

设置结构中的 GUID 字段 `DBPROPIDSET` 。

### <a name="syntax"></a>语法

```cpp
void SetGUID(const GUID& guid) throw();
```

#### <a name="parameters"></a>parameters

*guid*<br/>
中用于设置 `guidPropertySet` [DBPROPIDSET](/previous-versions/windows/desktop/ms717981(v=vs.85)) 结构的字段的 GUID。

### <a name="remarks"></a>备注

此字段也可以通过 [构造函数](#cdbpropidset) 进行设置。 如果您对此类使用默认构造函数，则调用此函数。

## <a name="cdbpropidsetoperator-"></a><a name="op_equal"></a> CDBPropIDSet：： operator =

将一个属性 ID 集的内容分配给另一 ID 属性集。

### <a name="syntax"></a>语法

```cpp
CDBPropIDSet& operator =(CDBPropIDSet& propset) throw();
```

## <a name="see-also"></a>请参阅

[OLE DB 使用者模板](../../data/oledb/ole-db-consumer-templates-cpp.md)<br/>
[OLE DB 使用者模板参考](../../data/oledb/ole-db-consumer-templates-reference.md)
