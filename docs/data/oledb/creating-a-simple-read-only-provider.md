---
description: 了解详细信息：创建简单的 Read-Only 提供程序
title: 创建简单的只读提供程序
ms.date: 05/09/2019
helpviewer_keywords:
- OLE DB providers, creating
- OLE DB provider templates, creating providers
ms.assetid: ade8ccdd-9ea4-4e46-a964-18460c2a2401
ms.openlocfilehash: 1904e850bc6a681e13e4799a2822963932ad9dfc
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97323215"
---
# <a name="creating-a-simple-read-only-provider"></a>创建简单的只读提供程序

::: moniker range="msvc-160"

ATL OLE DB 提供程序向导不适用于 Visual Studio 2019 及更高版本。

::: moniker-end

::: moniker range="<=msvc-150"

如果已使用 ATL 项目向导和 ATL OLE DB 提供程序向导创建 OLE DB 提供程序，可以添加要支持的其他功能。 通过检查要将什么种类的数据发送给使用者以及具体条件，开始设计提供程序。 特别是，请务必确定是否需要支持命令、事务和其他可选对象。 良好的预先设计会加快实现和测试的速度。

此示例包含两个部分：

- 第一个部分展示了如何[创建简单的只读提供程序](../../data/oledb/implementing-the-simple-read-only-provider.md)来读取字符串对。

- 第二个部分展示了如何通过添加 `IRowsetLocate` 接口来[增强简单的只读提供程序](../../data/oledb/enhancing-the-simple-read-only-provider.md)。

::: moniker-end

## <a name="see-also"></a>请参阅

[创建 OLE DB 提供程序](../../data/oledb/creating-an-ole-db-provider.md)<br/>
