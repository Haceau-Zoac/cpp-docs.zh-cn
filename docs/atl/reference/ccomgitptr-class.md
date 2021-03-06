---
description: 了解详细信息： CComGITPtr 类
title: CComGITPtr 类
ms.date: 11/04/2016
f1_keywords:
- CComGITPtr
- ATLBASE/ATL::CComGITPtr
- ATLBASE/ATL::CComGITPtr::CComGITPtr
- ATLBASE/ATL::CComGITPtr::Attach
- ATLBASE/ATL::CComGITPtr::CopyTo
- ATLBASE/ATL::CComGITPtr::Detach
- ATLBASE/ATL::CComGITPtr::GetCookie
- ATLBASE/ATL::CComGITPtr::Revoke
- ATLBASE/ATL::CComGITPtr::m_dwCookie
helpviewer_keywords:
- CComGITPtr class
ms.assetid: af895acb-525a-4555-bb67-b241b7df515b
ms.openlocfilehash: a457c0dea1679b177b72318d636c856334c85e36
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97146635"
---
# <a name="ccomgitptr-class"></a>CComGITPtr 类

此类提供一些方法，用于处理接口指针和全局接口表 (GIT) 。

## <a name="syntax"></a>语法

```
template <class T>
class CComGITPtr
```

#### <a name="parameters"></a>parameters

*T*<br/>
要存储在 GIT 中的接口指针的类型。

## <a name="members"></a>成员

### <a name="public-constructors"></a>公共构造函数

|“属性”|描述|
|----------|-----------------|
|[CComGITPtr::CComGITPtr](#ccomgitptr)|构造函数。|
|[CComGITPtr：： ~ CComGITPtr](#dtor)|析构函数。|

### <a name="public-methods"></a>公共方法

|“属性”|描述|
|----------|-----------------|
|[CComGITPtr：： Attach](#attach)|调用此方法可将接口指针注册到 (GIT) 的全局接口表中。|
|[CComGITPtr：： CopyTo](#copyto)|调用此方法可将接口从全局接口表 (GIT) 复制到传递的指针。|
|[CComGITPtr：:D etach](#detach)|调用此方法可将接口与对象解除关联 `CComGITPtr` 。|
|[CComGITPtr：： System.windows.application.getcookie](#getcookie)|调用此方法可从对象返回 cookie `CComGITPtr` 。|
|[CComGITPtr：： Revoke](#revoke)|调用此方法可从全局接口表 (GIT) 中移除接口。|

### <a name="public-operators"></a>公共运算符

|名称|描述|
|----------|-----------------|
|[CComGITPtr：： operator DWORD](#operator_dword)|从对象返回 cookie `CComGITPtr` 。|
|[CComGITPtr：： operator =](#operator_eq)|赋值运算符。|

### <a name="public-data-members"></a>公共数据成员

|名称|描述|
|----------|-----------------|
|[CComGITPtr：： m_dwCookie](#m_dwcookie)|Cookie。|

## <a name="remarks"></a>备注

聚合自由线程封送拆收器并需要使用从其他对象获取的接口指针的对象必须执行额外的步骤，以确保正确封送接口。 通常，这涉及到将接口指针存储在 GIT 中，并在每次使用时从 GIT 获取指针。 提供类 `CComGITPtr` 以帮助你使用存储在 GIT 中的接口指针。

> [!NOTE]
> 仅在带有 DCOM 版本1.1 和更高版本、Windows 98、Windows NT 4.0 Service Pack 3 及更高版本以及 Windows 2000 的 Windows 95 上，全局接口表功能才可用。

## <a name="requirements"></a>要求

**标头：** atlbase。h

## <a name="ccomgitptrattach"></a><a name="attach"></a> CComGITPtr：： Attach

调用此方法可将接口指针注册到 (GIT) 的全局接口表中。

```
HRESULT Attach(T* p) throw();

HRESULT Attach(DWORD dwCookie) throw();
```

### <a name="parameters"></a>parameters

*h-p*<br/>
要添加到 GIT 的接口指针。

*dwCookie*<br/>
用于标识接口指针的 cookie。

### <a name="return-value"></a>返回值

如果成功，则返回 S_OK; 否则返回错误 HRESULT。

### <a name="remarks"></a>备注

在调试版本中，如果 GIT 无效，或者 cookie 等于 NULL，则将发生断言错误。

## <a name="ccomgitptrccomgitptr"></a><a name="ccomgitptr"></a> CComGITPtr::CComGITPtr

构造函数。

```
CComGITPtr() throw();
CComGITPtr(T* p);
CComGITPtr(const CComGITPtr& git);
explicit CComGITPtr(DWORD dwCookie) throw();
CComGITPtr(CComGITPtr&& rv);
```

### <a name="parameters"></a>parameters

*h-p*<br/>
中要存储在全局接口表中 (GIT) 的接口指针。

*git*<br/>
中对现有对象的引用 `CComGITPtr` 。

*dwCookie*<br/>
中用于标识接口指针的 cookie。

*rv*<br/>
中 `CComGITPtr` 要从中移动数据的源对象。

### <a name="remarks"></a>备注

使用现有对象创建一个新的 `CComGITPtr` 对象 `CComGITPtr` 。

使用 *rv* 的构造函数是移动构造函数。 数据从源 *rv* 移动，然后清除 *rv* 。

## <a name="ccomgitptrccomgitptr"></a><a name="dtor"></a> CComGITPtr：： ~ CComGITPtr

析构函数。

```
~CComGITPtr() throw();
```

### <a name="remarks"></a>备注

使用 [CComGITPtr：： Revoke](#revoke)从全局接口表 (GIT) 中移除接口。

## <a name="ccomgitptrcopyto"></a><a name="copyto"></a> CComGITPtr：： CopyTo

调用此方法可将接口从全局接口表 (GIT) 复制到传递的指针。

```
HRESULT CopyTo(T** pp) const throw();
```

### <a name="parameters"></a>parameters

*pp*<br/>
用于接收接口的指针。

### <a name="return-value"></a>返回值

如果成功，则返回 S_OK; 否则返回错误 HRESULT。

### <a name="remarks"></a>备注

将 GIT 中的接口复制到传递的指针。 当不再需要指针时，它必须由调用方释放。

## <a name="ccomgitptrdetach"></a><a name="detach"></a> CComGITPtr：:D etach

调用此方法可将接口与对象解除关联 `CComGITPtr` 。

```
DWORD Detach() throw();
```

### <a name="return-value"></a>返回值

从对象返回 cookie `CComGITPtr` 。

### <a name="remarks"></a>备注

由调用方使用 [CComGITPtr：： Revoke](#revoke)从 GIT 中删除接口。

## <a name="ccomgitptrgetcookie"></a><a name="getcookie"></a> CComGITPtr：： System.windows.application.getcookie

调用此方法可从对象返回 cookie `CComGITPtr` 。

```
DWORD GetCookie() const;
```

### <a name="return-value"></a>返回值

返回 cookie。

### <a name="remarks"></a>备注

Cookie 是用于标识接口及其位置的变量。

## <a name="ccomgitptrm_dwcookie"></a><a name="m_dwcookie"></a> CComGITPtr：： m_dwCookie

Cookie。

```
DWORD m_dwCookie;
```

### <a name="remarks"></a>备注

Cookie 是用于标识接口及其位置的成员变量。

## <a name="ccomgitptroperator-"></a><a name="operator_eq"></a> CComGITPtr：： operator =

赋值运算符。

```
CComGITPtr& operator= (T* p);
CComGITPtr& operator= (const CComGITPtr& git);
CComGITPtr& operator= (DWORD dwCookie);
CComGITPtr& operator= (CComGITPtr&& rv);
```

### <a name="parameters"></a>parameters

*h-p*<br/>
中指向接口的指针。

*git*<br/>
中对对象的引用 `CComGITPtr` 。

*dwCookie*<br/>
中用于标识接口指针的 cookie。

*rv*<br/>
中 `CComGITPtr` 要从中移动数据的。

### <a name="return-value"></a>返回值

返回已更新的 `CComGITPtr` 对象。

### <a name="remarks"></a>备注

将新值分配给 `CComGITPtr` 对象，无论是从现有对象还是对全局接口表的引用。

## <a name="ccomgitptroperator-dword"></a><a name="operator_dword"></a> CComGITPtr：： operator DWORD

返回与对象关联的 cookie `CComGITPtr` 。

```
operator DWORD() const;
```

### <a name="remarks"></a>备注

Cookie 是用于标识接口及其位置的变量。

## <a name="ccomgitptrrevoke"></a><a name="revoke"></a> CComGITPtr：： Revoke

调用此方法以从全局接口表中删除当前接口 (GIT) 。

```
HRESULT Revoke() throw();
```

### <a name="return-value"></a>返回值

如果成功，则返回 S_OK; 否则返回错误 HRESULT。

### <a name="remarks"></a>备注

从 GIT 中删除接口。

## <a name="see-also"></a>请参阅

[自由线程封送拆收器](../../atl/atl-and-the-free-threaded-marshaler.md)<br/>
[跨单元访问接口](/windows/win32/com/accessing-interfaces-across-apartments)<br/>
[何时使用全局接口表](/windows/win32/com/when-to-use-the-global-interface-table)<br/>
[类概述](../../atl/atl-class-overview.md)
