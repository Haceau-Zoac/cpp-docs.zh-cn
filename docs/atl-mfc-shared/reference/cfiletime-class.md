---
description: 了解详细信息： CFileTime 类
title: CFileTime 类
ms.date: 10/18/2018
f1_keywords:
- CFileTime
- ATLTIME/ATL::CFileTime
- ATLTIME/ATL::CFileTime::CFileTime
- ATLTIME/ATL::CFileTime::GetCurrentTime
- ATLTIME/ATL::CFileTime::GetTime
- ATLTIME/ATL::CFileTime::LocalToUTC
- ATLTIME/ATL::CFileTime::SetTime
- ATLTIME/ATL::CFileTime::UTCToLocal
- ATLTIME/ATL::CFileTime::Day
- ATLTIME/ATL::CFileTime::Hour
- ATLTIME/ATL::CFileTime::Millisecond
- ATLTIME/ATL::CFileTime::Minute
- ATLTIME/ATL::CFileTime::Second
- ATLTIME/ATL::CFileTime::Week
helpviewer_keywords:
- CFileTime class
- shared classes, CFileTime
ms.assetid: 1a358a65-1383-4124-b0d4-59b026e6860f
ms.openlocfilehash: 95b46c188be60da787612a30ebff161a4ecf5966
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97166845"
---
# <a name="cfiletime-class"></a>CFileTime 类

此类提供用于管理与文件关联的日期和时间值的方法。

## <a name="syntax"></a>语法

```
class CFileTime :  public FILETIME
```

## <a name="members"></a>成员

### <a name="public-constructors"></a>公共构造函数

|“属性”|描述|
|----------|-----------------|
|[CFileTime::CFileTime](#cfiletime)|构造函数。|

### <a name="public-methods"></a>公共方法

|“属性”|描述|
|----------|-----------------|
|[CFileTime::GetCurrentTime](#getcurrenttime)|调用此静态函数以检索 `CFileTime` 表示当前系统日期和时间的对象。|
|[CFileTime：： GetTime](#gettime)|调用此方法从对象中检索时间 `CFileTime` 。|
|[CFileTime::LocalToUTC](#localtoutc)|调用此方法可根据协调世界时 (UTC) 将本地文件时间转换为文件时间。|
|[CFileTime：： SetTime](#settime)|调用此方法可设置对象存储的日期和时间 `CFileTime` 。|
|[CFileTime::UTCToLocal](#utctolocal)|调用此方法可基于协调世界时 (UTC) 到本地文件时间转换时间。|

### <a name="public-operators"></a>公共运算符

|名称|描述|
|----------|-----------------|
|[CFileTime：： operator-](#operator_-)|此运算符用于对或对象执行减法运算 `CFileTime` `CFileTimeSpan` 。|
|[CFileTime：： operator！ =](#operator_neq)|此运算符比较两个 `CFileTime` 对象是否不相等。|
|[CFileTime：： operator +](#operator_add)|此运算符用于对 `CFileTimeSpan` 对象执行加法。|
|[CFileTime：： operator + =](#operator_add_eq)|此运算符用于对 `CFileTimeSpan` 对象执行加法并对它赋予结果。|
|[CFileTime：： operator &lt;](#operator_lt)|此运算符比较两个 `CFileTime` 对象以确定较小者。|
|[CFileTime：： operator &lt;=](#operator_lt_eq)|此运算符比较两个 `CFileTime` 对象以确定是否相等或较小者。|
|[CFileTime：： operator =](#operator_eq)|赋值运算符。|
|[CFileTime：： operator-=](#operator_-_eq)|此运算符用于对对象执行减法运算 `CFileTimeSpan` ，并将结果分配给当前的对象。|
|[CFileTime：： operator = =](#operator_eq_eq)|此运算符比较两个 `CFileTime` 对象是否相等。|
|[CFileTime：： operator &gt;](#operator_gt)|此运算符比较两个 `CFileTime` 对象以确定较大者。|
|[CFileTime：： operator &gt;=](#operator_gt_eq)|此运算符比较两个 `CFileTime` 对象以确定是否相等或较大者。|

### <a name="public-constants"></a>公共常量

|名称|描述|
|----------|-----------------|
|[CFileTime：:D ay](#day)|一个静态数据成员，用于存储一天内100毫微秒的间隔。|
|[CFileTime：： Hour](#hour)|一个静态数据成员，其中存储了一个小时的100毫微秒间隔数。|
|[CFileTime：：毫秒](#millisecond)|一个静态数据成员，用于存储构成一毫秒的100纳秒间隔数。|
|[CFileTime：： Minute](#minute)|一个静态数据成员，用于存储一分钟的100毫微秒时间间隔。|
|[CFileTime：： Second](#second)|一个静态数据成员，用于存储一秒的100毫微秒时间间隔。|
|[CFileTime：： Week](#week)|一个静态数据成员，用于存储一周内100毫微秒的间隔数。|

## <a name="remarks"></a>备注

此类提供用于管理与文件创建、访问和修改相关联的日期和时间值的方法。 此类的方法和数据经常与用于 `CFileTimeSpan` 处理相对时间值的对象结合使用。

日期和时间值存储为64位值1601，该值表示自年1月1日起的100纳秒间隔数。 这是协调世界时 (UTC) 格式。

提供以下静态常量成员变量来简化计算：

|成员变量|100纳秒间隔数|
|---------------------|-----------------------------------------|
|Millisecond|10,000|
|秒|毫秒 \* 1000|
|Minute|第二个 \* 60|
|小时|分钟 \* 60|
|天|小时 \* 24|
|周|第 \* 7 天|

**注意** 并非所有文件系统都可以记录创建和上次访问时间，并且并非所有文件系统都以相同的方式记录它们。 例如，在 Windows NT FAT 文件系统上，创建时间的分辨率为10毫秒，写入时间的分辨率为2秒，而访问时间的解析时间为1天 (访问日期) 。 在 NTFS 上，访问时间的解析时间为1小时。 而且，FAT 在本地时间记录磁盘上的时间，但 NTFS 会记录磁盘上的时间时间（UTC）。 有关详细信息，请参阅 [文件时间](/windows/win32/SysInfo/file-times)。

## <a name="inheritance-hierarchy"></a>继承层次结构

`FILETIME`

`CFileTime`

## <a name="requirements"></a>要求

**标头：** atltime

## <a name="cfiletimecfiletime"></a><a name="cfiletime"></a> CFileTime::CFileTime

构造函数。

```
CFileTime() throw();
CFileTime(const FILETIME& ft) throw();
CFileTime(ULONGLONG nTime) throw();
```

### <a name="parameters"></a>parameters

*英尺*<br/>
[FILETIME](/windows/win32/api/minwinbase/ns-minwinbase-filetime)结构。

*n*<br/>
以64位值表示的日期和时间。

### <a name="remarks"></a>备注

`CFileTime`可以使用结构中的现有日期和时间来创建对象 `FILETIME` ，也可以使用本地或协调世界时 (UTC) 时间格式) 来表示为64位值 (。 默认构造函数将时间设置为0。

## <a name="cfiletimeday"></a><a name="day"></a> CFileTime：:D ay

一个静态数据成员，用于存储一天内100毫微秒的间隔。

```
static const ULONGLONG Day = Hour* 24;
```

### <a name="example"></a>示例

请参阅 [CFileTime：：毫秒](#millisecond)的示例。

## <a name="cfiletimegetcurrenttime"></a><a name="getcurrenttime"></a> CFileTime::GetCurrentTime

调用此静态函数以检索 `CFileTime` 表示当前系统日期和时间的对象。

```
static CFileTime GetCurrentTime() throw();
```

### <a name="return-value"></a>返回值

以协调世界时 (UTC) 格式返回当前系统日期和时间。

### <a name="example"></a>示例

[!code-cpp[NVC_MFCFiles#41](../../atl-mfc-shared/reference/codesnippet/cpp/cfiletime-class_1.cpp)]

## <a name="cfiletimegettime"></a><a name="gettime"></a> CFileTime：： GetTime

调用此方法从对象中检索时间 `CFileTime` 。

```
ULONGLONG GetTime() const throw();
```

### <a name="return-value"></a>返回值

以64位数字的形式返回日期和时间，该数字可以是本地或协调世界时 (UTC) 格式。

## <a name="cfiletimehour"></a><a name="hour"></a> CFileTime：： Hour

一个静态数据成员，其中存储了一个小时的100毫微秒间隔数。

```
static const ULONGLONG Hour = Minute* 60;
```

### <a name="example"></a>示例

请参阅 [CFileTime：：毫秒](#millisecond)的示例。

## <a name="cfiletimelocaltoutc"></a><a name="localtoutc"></a> CFileTime::LocalToUTC

调用此方法可根据协调世界时 (UTC) 将本地文件时间转换为文件时间。

```
CFileTime LocalToUTC() const throw();
```

### <a name="return-value"></a>返回值

返回一个 `CFileTime` 对象，该对象包含 UTC 格式的时间。

### <a name="example"></a>示例

请参阅 [CFileTime：： UTCToLocal](#utctolocal)的示例。

## <a name="cfiletimemillisecond"></a><a name="millisecond"></a> CFileTime：：毫秒

一个静态数据成员，用于存储构成一毫秒的100纳秒间隔数。

```
static const ULONGLONG Millisecond = 10000;
```

### <a name="example"></a>示例

[!code-cpp[NVC_MFCFiles#44](../../atl-mfc-shared/reference/codesnippet/cpp/cfiletime-class_2.cpp)]

## <a name="cfiletimeminute"></a><a name="minute"></a> CFileTime：： Minute

一个静态数据成员，用于存储一分钟的100毫微秒时间间隔。

```
static const ULONGLONG Minute = Second* 60;
```

### <a name="example"></a>示例

请参阅 [CFileTime：：毫秒](#millisecond)的示例。

## <a name="cfiletimeoperator--"></a><a name="operator_-"></a> CFileTime：： operator-

此运算符用于对或对象执行减法运算 `CFileTime` `CFileTimeSpan` 。

```
CFileTime operator-(CFileTimeSpan span) const throw();
CFileTimeSpan operator-(CFileTime ft) const throw();
```

### <a name="parameters"></a>parameters

*格*<br/>
`CFileTimeSpan` 对象。

*英尺*<br/>
`CFileTime` 对象。

### <a name="return-value"></a>返回值

返回一个 `CFileTime` 对象或对象，该对象 `CFileTimeSpan` 表示这两个对象之间的时间差的结果。

## <a name="cfiletimeoperator-"></a><a name="operator_neq"></a> CFileTime：： operator！ =

此运算符比较两个 `CFileTime` 对象是否不相等。

```
bool operator!=(CFileTime ft) const throw();
```

### <a name="parameters"></a>parameters

*英尺*<br/>
要比较的 `CFileTime` 对象。

### <a name="return-value"></a>返回值

如果要比较的项与对象不相等，则返回 TRUE `CFileTime` ; 否则返回 FALSE。

## <a name="cfiletimeoperator-"></a><a name="operator_add"></a> CFileTime：： operator +

此运算符用于对 `CFileTimeSpan` 对象执行加法。

```
CFileTime operator+(CFileTimeSpan span) const throw();
```

### <a name="parameters"></a>parameters

*格*<br/>
`CFileTimeSpan` 对象。

### <a name="return-value"></a>返回值

返回一个 `CFileTime` 对象，该对象表示原始时间加上相对时间的结果。

## <a name="cfiletimeoperator-"></a><a name="operator_add_eq"></a> CFileTime：： operator + =

此运算符用于对 `CFileTimeSpan` 对象执行加法并对它赋予结果。

```
CFileTime& operator+=(CFileTimeSpan span) throw();
```

### <a name="parameters"></a>parameters

*格*<br/>
`CFileTimeSpan` 对象。

### <a name="return-value"></a>返回值

返回已更新的 `CFileTime` 对象，它表示原始时间的结果加上相对时间。

## <a name="cfiletimeoperator-lt"></a><a name="operator_lt"></a> CFileTime：： operator &lt;

此运算符比较两个 `CFileTime` 对象以确定较小者。

```
bool operator<(CFileTime ft) const throw();
```

### <a name="parameters"></a>parameters

*英尺*<br/>
要比较的 `CFileTime` 对象。

### <a name="return-value"></a>返回值

如果第一个对象 (的时间早于) 秒，则返回 TRUE，否则返回 FALSE。

### <a name="example"></a>示例

[!code-cpp[NVC_MFCFiles#43](../../atl-mfc-shared/reference/codesnippet/cpp/cfiletime-class_3.cpp)]

## <a name="cfiletimeoperator-lt"></a><a name="operator_lt_eq"></a> CFileTime：： operator &lt;=

此运算符比较两个 `CFileTime` 对象以确定是否相等或较小者。

```
bool operator<=(CFileTime ft) const throw();
```

### <a name="parameters"></a>parameters

*英尺*<br/>
要比较的 `CFileTime` 对象。

### <a name="return-value"></a>返回值

如果第一个对象小于 (前面时间) 或等于第二个对象，则返回 TRUE，否则返回 FALSE。

## <a name="cfiletimeoperator-"></a><a name="operator_eq"></a> CFileTime：： operator =

赋值运算符。

```
CFileTime& operator=(const FILETIME& ft) throw();
```

### <a name="parameters"></a>parameters

*英尺*<br/>
一个 `CFileTime` 包含新时间和日期的对象。

### <a name="return-value"></a>返回值

返回已更新的 `CFileTime` 对象。

## <a name="cfiletimeoperator--"></a><a name="operator_-_eq"></a> CFileTime：： operator-=

此运算符用于对对象执行减法运算 `CFileTimeSpan` ，并将结果分配给当前的对象。

```
CFileTime& operator-=(CFileTimeSpan span) throw();
```

### <a name="parameters"></a>parameters

*格*<br/>
`CFileTimeSpan`包含要减去的相对时间的对象。

### <a name="return-value"></a>返回值

返回已更新的 `CFileTime` 对象。

## <a name="cfiletimeoperator-"></a><a name="operator_eq_eq"></a> CFileTime：： operator = =

此运算符比较两个 `CFileTime` 对象是否相等。

```
bool operator==(CFileTime ft) const throw();
```

### <a name="parameters"></a>parameters

*英尺*<br/>
要比较的 `CFileTime` 对象。

### <a name="return-value"></a>返回值

如果对象相等，则返回 TRUE; 否则返回 FALSE。

## <a name="cfiletimeoperator-gt"></a><a name="operator_gt"></a> CFileTime：： operator &gt;

此运算符比较两个 `CFileTime` 对象以确定较大者。

```
bool operator>(CFileTime ft) const throw();
```

### <a name="parameters"></a>parameters

*英尺*<br/>
要比较的 `CFileTime` 对象。

### <a name="return-value"></a>返回值

如果第一个对象大于 (晚) 秒，则返回 TRUE，否则返回 FALSE。

## <a name="cfiletimeoperator-gt"></a><a name="operator_gt_eq"></a> CFileTime：： operator &gt;=

此运算符比较两个 `CFileTime` 对象以确定是否相等或较大者。

```
bool operator>=(CFileTime ft) const throw();
```

### <a name="parameters"></a>parameters

*英尺*<br/>
要比较的 `CFileTime` 对象。

### <a name="return-value"></a>返回值

如果第一个对象大于 (晚时间) 或等于第二个对象，则返回 TRUE，否则返回 FALSE。

## <a name="cfiletimesecond"></a><a name="second"></a> CFileTime：： Second

一个静态数据成员，用于存储一天内100毫微秒的间隔。

```
static const ULONGLONG Second = Millisecond* 1000;
```

### <a name="example"></a>示例

请参阅 [CFileTime：：毫秒](#millisecond)的示例。

## <a name="cfiletimesettime"></a><a name="settime"></a> CFileTime：： SetTime

调用此方法可设置对象存储的日期和时间 `CFileTime` 。

```cpp
void SetTime(ULONGLONG nTime) throw();
```

### <a name="parameters"></a>parameters

*n*<br/>
表示日期和时间的64位值，采用本地或协调世界时 (UTC) 格式。

## <a name="cfiletimeutctolocal"></a><a name="utctolocal"></a> CFileTime::UTCToLocal

调用此方法可基于协调世界时 (UTC) 到本地文件时间转换时间。

```
CFileTime UTCToLocal() const throw();
```

### <a name="return-value"></a>返回值

返回一个 `CFileTime` 对象，该对象包含本地文件时间格式的时间。

### <a name="example"></a>示例

[!code-cpp[NVC_MFCFiles#42](../../atl-mfc-shared/reference/codesnippet/cpp/cfiletime-class_4.cpp)]

## <a name="cfiletimeweek"></a><a name="week"></a> CFileTime：： Week

一个静态数据成员，用于存储一周内100毫微秒的间隔数。

```
static const ULONGLONG Week = Day* 7;
```

### <a name="example"></a>示例

请参阅 [CFileTime：：毫秒](#millisecond)的示例。

## <a name="see-also"></a>请参阅

[FILETIME](/windows/win32/api/minwinbase/ns-minwinbase-filetime)<br/>
[CFileTimeSpan 类](../../atl-mfc-shared/reference/cfiletimespan-class.md)<br/>
[层次结构图](../../mfc/hierarchy-chart.md)<br/>
[ATL/MFC 共享类](../../atl-mfc-shared/atl-mfc-shared-classes.md)
