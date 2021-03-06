---
description: 详细了解：结构成员的填充和对齐
title: 结构成员的填充和对齐
ms.date: 10/18/2018
helpviewer_keywords:
- structure members, padding and alignment
ms.assetid: c999820b-dd47-41fc-b923-e4c7ebbcd30f
ms.openlocfilehash: db2530ecb00e5a01f5d10ff45da55420a8139be0
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97137444"
---
# <a name="padding-and-alignment-of-structure-members"></a>结构成员的填充和对齐

**ANSI 3.5.2.1** 结构的成员的填充和对齐方式，以及位域是否可以跨存储单元边界

结构成员按其声明顺序进行存储：第一个成员的内存地址最低，最后一个成员的内存地址最高。

每个数据对象具有 alignment-requirement。 所有数据（结构、联合和数组除外）的对齐要求是对象的大小或当前打包大小（使用 /Zp 或 `pack` 杂注指定，以较小者为准）。 对于结构、联合和数组，对齐要求是其成员的最大对齐要求。 为每个对象分配一个 offset，以便

*offset* **%** *alignment-requirement* **== 0**

如果整型的大小相同，并且下一个位域适合当前分配单元而未跨位域的常见对齐需求所强加的边界，则将相邻位域打包到相同的 1 字节、2 字节或 4 字节分配单元中。

## <a name="see-also"></a>请参阅

[结构、联合、枚举和位域](../c-language/structures-unions-enumerations-and-bit-fields.md)
