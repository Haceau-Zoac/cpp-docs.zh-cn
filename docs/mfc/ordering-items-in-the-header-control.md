---
description: 了解详细信息：在标头控件中对项进行排序
title: 对标题控件中的项排序
ms.date: 11/04/2016
f1_keywords:
- DS_DRAGDROP
helpviewer_keywords:
- sequence [MFC]
- sequence [MFC], header control items
- OrderToIndex method [MFC]
- DS_DRAGDROP notification [MFC]
- GetOrderArray method [MFC]
- SetOrderArray method [MFC]
- header controls [MFC], ordering items
ms.assetid: 5aaef872-75b5-49c5-8fed-6f9a81fca812
ms.openlocfilehash: 6f6db7b134121c4084d9406ad537bf0ce5dc12cb
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97330118"
---
# <a name="ordering-items-in-the-header-control"></a>对标题控件中的项排序

[向标题控件添加项](adding-items-to-the-header-control.md)后，可以使用以下函数操作或获取有关其顺序的信息：

- [CHeaderCtrl：： GetOrderArray](reference/cheaderctrl-class.md#getorderarray) 和 [CHeaderCtrl：： SetOrderArray](reference/cheaderctrl-class.md#setorderarray)

   检索和设置标题项的从左到右的顺序。

- [CHeaderCtrl：： OrderToIndex](reference/cheaderctrl-class.md#ordertoindex)。

   检索特定标题项的索引值。

除了以前的成员函数，HDS_DRAGDROP 样式允许用户在标题控件中拖放标题项。 有关详细信息，请参阅为 [标题项提供拖放支持](providing-drag-and-drop-support-for-header-items.md)。

## <a name="see-also"></a>请参阅

[使用 CHeaderCtrl](using-cheaderctrl.md)
