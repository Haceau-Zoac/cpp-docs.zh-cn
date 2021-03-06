---
description: '了解详细信息：/MANIFESTDEPENDENCY (指定清单依赖项) '
title: /MANIFESTDEPENDENCY（指定清单依赖项）
ms.date: 11/04/2016
f1_keywords:
- VC.Project.VCLinkerTool.AdditionalManifestDependencies
helpviewer_keywords:
- MANIFESTDEPENDENCY linker option
- /MANIFESTDEPENDENCY linker option
- -MANIFESTDEPENDENCY linker option
ms.assetid: e4b68313-33a2-4c3e-908e-ac2b9f7d6a73
ms.openlocfilehash: 129dc84818b0bda9b2106c0d07dca5b605dc6f96
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97199162"
---
# <a name="manifestdependency-specify-manifest-dependencies"></a>/MANIFESTDEPENDENCY（指定清单依赖项）

```
/MANIFESTDEPENDENCY:manifest_dependency
```

## <a name="remarks"></a>备注

/MANIFESTDEPENDENCY 允许您指定将放入清单文件的部分中的属性 \<dependency> 。

有关如何创建清单文件的信息，请参阅 [/MANIFEST (创建并行程序集清单) ](manifest-create-side-by-side-assembly-manifest.md) 。

有关清单文件的部分的详细信息 \<dependency> ，请参阅 [发布服务器配置文件](/windows/win32/SbsCs/publisher-configuration-files)。

可以通过以下两种方式之一将/MANIFESTDEPENDENCY 信息传递给链接器：

- 直接在命令行 (或) 使用/MANIFESTDEPENDENCY. 的响应文件中

- 通过 [注释](../../preprocessor/comment-c-cpp.md) 杂注。

下面的示例演示通过杂注传递的/MANIFESTDEPENDENCY 注释，

```cpp
#pragma comment(linker, "\"/manifestdependency:type='Win32' name='Test.Research.SampleAssembly' version='6.0.0.0' processorArchitecture='X86' publicKeyToken='0000000000000000' language='*'\"")
```

这会生成清单文件中的以下条目：

```xml
<dependency>
  <dependentAssembly>
    <assemblyIdentity type='Win32' name='Test.Research.SampleAssembly' version='6.0.0.0' processorArchitecture='X86' publicKeyToken='0000000000000000' language='*' />
  </dependentAssembly>
</dependency>
```

可以在命令行上传递相同的/MANIFESTDEPENDENCY 注释，如下所示：

```cmd
"/manifestdependency:type='Win32' name='Test.Research.SampleAssembly' version='6.0.0.0' processorArchitecture='X86' publicKeyToken='0000000000000000' language='*'\"
```

链接器将收集/MANIFESTDEPENDENCY 注释，消除重复项，然后将生成的 XML 字符串添加到清单文件中。  如果链接器找到了冲突的条目，则清单文件将会损坏，并且应用程序将无法启动 (条目可能会添加到事件日志中，指出失败的原因) 。

### <a name="to-set-this-linker-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此链接器选项

1. 打开项目的“属性页”  对话框。 有关详细信息，请参阅[在 Visual Studio 中设置 C++ 编译器和生成属性](../working-with-project-properties.md)。

1. 选择 "**配置属性**  >  **链接器**  >  **清单文件**" 属性页。

1. 修改 " **附加清单依赖项** " 属性。

### <a name="to-set-this-linker-option-programmatically"></a>以编程方式设置此链接器选项

1. 请参阅 <xref:Microsoft.VisualStudio.VCProjectEngine.VCLinkerTool.AdditionalManifestDependencies%2A>。

## <a name="see-also"></a>请参阅

[MSVC 链接器参考](linking.md)<br/>
[MSVC 链接器选项](linker-options.md)
