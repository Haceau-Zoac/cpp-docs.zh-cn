---
description: 了解详细信息：从对话框对象检索数据
title: 从对话框对象检索数据
ms.date: 11/04/2016
helpviewer_keywords:
- dialog boxes [MFC], retrieving user data
- dialog box data [MFC]
- data [MFC], retrieving
- GetDlgItemText method [MFC]
- SetDlgItemText method [MFC]
- SetWindowText method [MFC]
- dialog box data [MFC], retrieving
- retrieving data [MFC]
- user input [MFC], retrieving from MFC dialog boxes
- capturing user input [MFC]
- dialog box controls [MFC], initializing values
- DDX (dialog data exchange) [MFC]
- MFC dialog boxes [MFC], retrieving user input
- data retrieval [MFC], dialog boxes
- data [MFC], dialog boxes
- DDX (dialog data exchange) [MFC], about DDX
- DDX (dialog data exchange) [MFC], retrieving data from Dialog object
- GetWindowText method [MFC]
ms.assetid: bdca2b61-6b53-4c2e-b426-8712c7a38ec0
ms.openlocfilehash: 823006b7b892c8e6476d007eb5cc13fb1386458e
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97218038"
---
# <a name="retrieving-data-from-the-dialog-object"></a>从对话框对象检索数据

框架提供了一种简单的方法来初始化对话框中的控件值并从控件中检索值。 更费力的手动方法是调用函数，例如类的 `SetDlgItemText` 和 `GetDlgItemText` 成员函数 `CWnd` ，它们适用于控件窗口。 使用这些函数，可以单独访问每个控件，以便设置或获取其值，调用函数（如 `SetWindowText` 和） `GetWindowText` 。 框架的方法自动执行初始化和检索。

对话框数据交换 (DDX) 使你可以更轻松地在对话框中的控件和对话框对象中的成员变量之间交换数据。 这种交换的工作方式。 若要初始化对话框中的控件，可以在对话框对象中设置数据成员的值，框架将在显示对话框之前将值传输到控件。 然后，你可以随时使用用户输入的数据更新对话框数据成员。 此时，可以通过引用数据成员变量来使用数据。

您还可以安排自动验证对话框控件的值，并通过对话数据验证 (DDV) 进行自动验证。

[对话框数据交换和验证](../mfc/dialog-data-exchange-and-validation.md)中更详细地介绍了 DDX 和 DDV。

对于模式对话框，您可以检索用户在返回 IDOK 时输入的任何数据， `DoModal` 但在销毁对话框对象之前。 对于无模式对话框，可以通过调用 `UpdateData` 参数 **TRUE** ，然后访问对话框类成员变量，随时从对话框对象检索数据。 [对话框数据交换和验证](../mfc/dialog-data-exchange-and-validation.md)中更详细地讨论了此主题。

## <a name="see-also"></a>请参阅

[在 MFC 中使用对话框](../mfc/life-cycle-of-a-dialog-box.md)
