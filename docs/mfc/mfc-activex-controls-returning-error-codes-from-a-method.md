---
description: 了解更多相关信息： MFC ActiveX 控件：从方法返回错误代码
title: MFC ActiveX 控件：从方法返回错误代码
ms.date: 11/04/2016
helpviewer_keywords:
- MFC ActiveX controls [MFC], error codes
- SetNotSupported method, using
- errors [MFC], ActiveX control error codes
- GetNotSupported method [MFC]
- FireError method [MFC]
- SCODE, MFC ActiveX controls
- ThrowError method [MFC]
ms.assetid: 771fb9c9-2413-4dcc-b386-7bc4c4adeafd
ms.openlocfilehash: f6a1f372442ee67787a7a5421dabb4460acfcc7a
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97206066"
---
# <a name="mfc-activex-controls-returning-error-codes-from-a-method"></a>MFC ActiveX 控件：从方法返回错误代码

本文介绍如何通过 ActiveX 控件方法返回错误代码。

若要指示方法中发生了错误，应使用 [COleControl：： ThrowError](reference/colecontrol-class.md#throwerror) 成员函数，该函数采用 SCODE (状态代码) 作为参数。 可以使用预定义的 SCODE，也可以定义自己的。

> [!NOTE]
> `ThrowError` 意味着仅用作通过属性的 Get 或 Set 函数或自动化方法返回错误的一种方式。 这是适当异常处理程序将出现在堆栈上的唯一时间。

对于最常见的预定义的 SCODEs （如 [COleControl：： SetNotSupported](reference/colecontrol-class.md#setnotsupported)、 [COleControl：： GetNotSupported](reference/colecontrol-class.md#getnotsupported)和 [COleControl：： SetNotPermitted](reference/colecontrol-class.md#setnotpermitted)）存在 Helper 函数。

有关定义自定义 SCODEs 的预定义 SCODEs 的列表，请参阅在 activex 控件中 [处理 Activex 控件](mfc-activex-controls-advanced-topics.md) 中的错误一节：高级主题。

有关在代码的其他区域报告异常的详细信息，请参阅 ActiveX 控件中的 [COleControl：： FireError](reference/colecontrol-class.md#fireerror) 和 [处理 activex 控件](mfc-activex-controls-advanced-topics.md) 中的错误部分：高级主题。

## <a name="see-also"></a>请参阅

[MFC ActiveX 控件](mfc-activex-controls.md)
