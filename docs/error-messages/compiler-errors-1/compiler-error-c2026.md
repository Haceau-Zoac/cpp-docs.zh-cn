---
title: 编译器错误 C2026
description: 描述 Microsoft C/c + + 编译器错误 C2026、其原因和解决方法。
ms.date: 09/25/2020
f1_keywords:
- C2026
helpviewer_keywords:
- C2026
ms.assetid: 8e64b6e1-b967-479b-be97-d12dc4a8e389
ms.openlocfilehash: 39195568f964f07c6131fa43ef4a0f06121795da
ms.sourcegitcommit: 94893973211d0b254c8bcdcf0779997dcc136b0c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2020
ms.locfileid: "91414043"
---
# <a name="compiler-error-c2026"></a>编译器错误 C2026

> 字符串太大，已截断尾部字符

字符串的长度超过16380个单字节字符的限制。

## <a name="remarks"></a>备注

在连接相邻字符串之前，字符串长度不能超过16380个单字节字符。

此长度约为一半的 Unicode 字符串也会生成此错误。

## <a name="example"></a>示例

如果有一个定义如下的字符串，则会生成 C2026：

```C
char sz[] =
"\
imagine a really, really \
long string here\
";
```

您可以按如下所示对其进行分解：

```C
char sz[] =
"\
imagine a really, really "
"long string here\
";
```

你可能需要在自定义资源或外部文件中存储非常大的字符串文字 (32K 或更多) 。 有关详细信息，请参阅 [创建新的自定义资源或数据资源](../../windows/binary-editor.md#to-create-a-new-custom-or-data-resource)。
