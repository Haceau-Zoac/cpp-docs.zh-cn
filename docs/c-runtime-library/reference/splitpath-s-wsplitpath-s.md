---
description: 了解详细信息： _splitpath_s、_wsplitpath_s
title: _splitpath_s、_wsplitpath_s
ms.date: 4/2/2020
api_name:
- _wsplitpath_s
- _splitpath_s
- _o__splitpath_s
- _o__wsplitpath_s
api_location:
- msvcrt.dll
- msvcr80.dll
- msvcr90.dll
- msvcr100.dll
- msvcr100_clr0400.dll
- msvcr110.dll
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr120_clr0400.dll
- ucrtbase.dll
- api-ms-win-crt-filesystem-l1-1-0.dll
- ntoskrnl.exe
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _wsplitpath_s
- splitpath_s
- _splitpath_s
- wsplitpath_s
helpviewer_keywords:
- splitpath_s function
- pathnames
- _splitpath_s function
- _wsplitpath_s function
- path names
- wsplitpath_s function
ms.assetid: 30fff3e2-cd00-4eb6-b5a2-65db79cb688b
ms.openlocfilehash: f14ea8a31d241abae3a214067cae1e4d34e97861
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97292339"
---
# <a name="_splitpath_s-_wsplitpath_s"></a>_splitpath_s、_wsplitpath_s

将路径名称分解成组件。 这些版本的 [_splitpath、_wsplitpath](splitpath-wsplitpath.md) 具有安全增强功能，如 [CRT 中的安全功能](../../c-runtime-library/security-features-in-the-crt.md)所述。

## <a name="syntax"></a>语法

```C
errno_t _splitpath_s(
   const char * path,
   char * drive,
   size_t driveNumberOfElements,
   char * dir,
   size_t dirNumberOfElements,
   char * fname,
   size_t nameNumberOfElements,
   char * ext,
   size_t extNumberOfElements
);
errno_t _wsplitpath_s(
   const wchar_t * path,
   wchar_t * drive,
   size_t driveNumberOfElements,
   wchar_t *dir,
   size_t dirNumberOfElements,
   wchar_t * fname,
   size_t nameNumberOfElements,
   wchar_t * ext,
   size_t extNumberOfElements
);
template <size_t drivesize, size_t dirsize, size_t fnamesize, size_t extsize>
errno_t _splitpath_s(
   const char *path,
   char (&drive)[drivesize],
   char (&dir)[dirsize],
   char (&fname)[fnamesize],
   char (&ext)[extsize]
); // C++ only
template <size_t drivesize, size_t dirsize, size_t fnamesize, size_t extsize>
errno_t _wsplitpath_s(
   const wchar_t *path,
   wchar_t (&drive)[drivesize],
   wchar_t (&dir)[dirsize],
   wchar_t (&fname)[fnamesize],
   wchar_t (&ext)[extsize]
); // C++ only
```

### <a name="parameters"></a>parameters

*路径*<br/>
完整路径。

*光驱*<br/>
驱动器号，后面跟一个冒号 (**：**) 。 如果不需要驱动器号，则可以为此参数传递 **NULL** 。

*driveNumberOfElements*<br/>
*驱动器* 缓冲区大小（以单字节或宽字符为单位）。 如果 *驱动器* 为 **空**，则此值必须为0。

*dir*<br/>
目录路径，包括尾部反斜杠。 正斜杠 ( **/** ) 、反斜杠 ( **\\** ) 或两者均可使用。 如果不需要目录路径，则可以为此参数传递 **NULL** 。

*dirNumberOfElements*<br/>
*目录* 缓冲区的大小（以单字节字符或宽字符为单位）。 如果 *dir* 为 **NULL**，则此值必须为0。

*fname*<br/>
基文件名（不带扩展名）。 如果不需要文件名，则可以为此参数传递 **NULL** 。

*nameNumberOfElements*<br/>
*Fname* 缓冲区的大小（以单字节字符或宽字符为单位）。 如果 *fname* 为 **NULL**，则此值必须为0。

*宋体*<br/>
文件扩展名，包括前导句点 (**。**) 。如果不需要文件扩展名，则可为此参数传递 **NULL** 。

*extNumberOfElements*<br/>
*扩展* 缓冲区的大小（以单字节或宽字符为单位）。 如果 *ext* 为 **NULL**，则此值必须为0。

## <a name="return-value"></a>返回值

如果成功，则为零；如果失败，则为错误代码。

### <a name="error-conditions"></a>错误条件

|条件|返回值|
|---------------|------------------|
|*路径* 为 **NULL**|**EINVAL**|
|*驱动器* 为 **NULL**， *driveNumberOfElements* 为非零值|**EINVAL**|
|*驱动器* 为非 **NULL**， *driveNumberOfElements* 为零|**EINVAL**|
|*dir* 为 **NULL**， *dirNumberOfElements* 为非零值|**EINVAL**|
|*dir* 为非 **NULL**， *dirNumberOfElements* 为零|**EINVAL**|
|*fname* 为 **NULL**， *nameNumberOfElements* 为非零|**EINVAL**|
|*fname* 为非 **NULL**， *nameNumberOfElements* 为零|**EINVAL**|
|*ext* 为 **NULL**， *extNumberOfElements* 为非零值|**EINVAL**|
|*ext* 为非 **NULL**， *extNumberOfElements* 为零|**EINVAL**|

如果发生上述情况之一，都会调用无效参数处理程序，如[参数验证](../../c-runtime-library/parameter-validation.md)中所述。 如果允许执行继续，则这些函数会将 **errno** 设置为 **EINVAL** 并返回 **EINVAL**。

如果任何缓冲区太短而无法保存结果，则这些函数会将所有缓冲区清除为空字符串，将 **errno** 设置为 **ERANGE**，并返回 **ERANGE**。

## <a name="remarks"></a>备注

**_Splitpath_s** 函数将路径分解为四个组件。 **_splitpath_s** 会根据需要自动处理多字节字符串参数，根据当前使用的多字节代码页识别多字节字符序列。 **_wsplitpath_s** 是 **_splitpath_s** 的宽字符版本; **_wsplitpath_s** 的参数是宽字符字符串。 否则这些函数具有相同行为

默认情况下，此函数的全局状态的作用域限定为应用程序。 若要更改此项，请参阅 [CRT 中的全局状态](../global-state.md)。

### <a name="generic-text-routine-mappings"></a>一般文本例程映射

|TCHAR.H 例程|未定义 _UNICODE 和 _MBCS|已定义 _MBCS|已定义 _UNICODE|
|---------------------|------------------------------------|--------------------|-----------------------|
|**_tsplitpath_s**|**_splitpath_s**|**_splitpath_s**|**_wsplitpath_s**|

完整路径的每个组件均存储在单独的缓冲区中;清单常量在 STDLIB.H 中定义 **_MAX_DRIVE**、 **_MAX_DIR**、 **_MAX_FNAME** 和 (**_MAX_EXT** 。H) 指定每个文件组件的最大允许大小。 文件组件大于相应清单常量会导致堆损坏。

下表列出了清单常量的值。

|名称|值|
|----------|-----------|
|_MAX_DRIVE|3|
|_MAX_DIR|256|
|_MAX_FNAME|256|
|_MAX_EXT|256|

如果完整路径不包含组件 (例如，filename) ， **_splitpath_s** 会将空字符串分配给相应的缓冲区。

在 C++ 中，通过模板重载简化这些函数的使用；重载可以自动推导出缓冲区长度，不再需要指定大小参数。 有关详细信息，请参阅[安全模板重载](../../c-runtime-library/secure-template-overloads.md)。

这些函数的调试库版本首先用0xFE 填充缓冲区。 若要禁用此行为，请使用 [_CrtSetDebugFillThreshold](crtsetdebugfillthreshold.md)。

## <a name="requirements"></a>要求

|例程所返回的值|必需的标头|
|-------------|---------------------|
|**_splitpath_s**|\<stdlib.h>|
|**_wsplitpath_s**|\<stdlib.h> 或 \<wchar.h>|

有关其他兼容性信息，请参阅[兼容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>示例

请参阅 [_makepath_s、_wmakepath_s](makepath-s-wmakepath-s.md) 的示例。

## <a name="see-also"></a>请参阅

[文件处理](../../c-runtime-library/file-handling.md)<br/>
[_splitpath、_wsplitpath](splitpath-wsplitpath.md)<br/>
[_fullpath、_wfullpath](fullpath-wfullpath.md)<br/>
[_getmbcp](getmbcp.md)<br/>
[_makepath、_wmakepath](makepath-wmakepath.md)<br/>
[_setmbcp](setmbcp.md)<br/>
