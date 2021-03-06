---
title: /showIncludes（列出包含文件）
ms.date: 11/04/2016
f1_keywords:
- VC.Project.VCCLWCECompilerTool.ShowIncludes
- VC.Project.VCCLCompilerTool.ShowIncludes
- /showincludes
helpviewer_keywords:
- include files
- /showIncludes compiler option [C++]
- include files, displaying in compilation
- -showIncludes compiler option [C++]
- showIncludes compiler option [C++]
ms.assetid: 0b74b052-f594-45a6-a7c7-09e1a319547d
ms.openlocfilehash: d454054c132976a899fcc4a56a63be427e79beec
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62318155"
---
# <a name="showincludes-list-include-files"></a>/showIncludes（列出包含文件）

使编译器输出的包含文件列表。 嵌套的包含文件还可以显示 （包括文件中包含的文件）。

## <a name="syntax"></a>语法

```
/showIncludes
```

## <a name="remarks"></a>备注

当在编译期间遇到的包含文件时，则将输出消息，例如：

```
Note: including file: d:\MyDir\include\stdio.h
```

嵌套的包含文件所指示的缩进一个空间，每个级别的嵌套，例如：

```
Note: including file: d:\temp\1.h
Note: including file:  d:\temp\2.h
```

在这种情况下，`2.h`包含在`1.h`，因此缩进。

**/ShowIncludes**选项发出到`stderr`，而不`stdout`。

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项

1. 打开项目的“属性页”  对话框。 有关详细信息，请参阅[设置C++Visual Studio 中的编译器和生成属性](../working-with-project-properties.md)。

1. 单击 **“C/C++”** 文件夹。

1. 单击**高级**属性页。

1. 修改**显示包含**属性。

### <a name="to-set-this-compiler-option-programmatically"></a>以编程方式设置此编译器选项

- 请参阅 <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.ShowIncludes%2A>。

## <a name="see-also"></a>请参阅

[MSVC 编译器选项](compiler-options.md)<br/>
[MSVC 编译器命令行语法](compiler-command-line-syntax.md)
