---
description: 了解详细信息：严重错误 C1126
title: 错误 C1126
ms.date: 11/04/2016
f1_keywords:
- C1126
helpviewer_keywords:
- C1126
ms.assetid: f22b26a6-8ad7-47cf-a237-196c8ea60aca
ms.openlocfilehash: d6898b65bafa6862c77b10aa362ffc0a0df6e597
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97181001"
---
# <a name="fatal-error-c1126"></a>错误 C1126

"identifier"：自动分配超出大小

为函数的局部变量分配的空间 (加上编译器使用的有限空间量，例如，可交换函数) 额外的20个字节超过限制。

若要更正此错误，请使用 `malloc` 或 **`new`** 以分配大量的数据。
