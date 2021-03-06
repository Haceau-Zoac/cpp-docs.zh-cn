---
description: 了解详细信息：如何：编写 parallel_for_each 循环
title: 如何：编写 parallel_for_each 循环
ms.date: 11/04/2016
helpviewer_keywords:
- writing a parallel_for_each loop [Concurrency Runtime]
- parallel_for_each function, example
ms.assetid: fa9c0ba6-ace0-4f88-8681-c7c1f52aff20
ms.openlocfilehash: cb80173d3d4c78fe4d46f017d60af2c3c6659096
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97112227"
---
# <a name="how-to-write-a-parallel_for_each-loop"></a>如何：编写 parallel_for_each 循环

此示例演示如何使用 [concurrency：:p arallel_for_each](reference/concurrency-namespace-functions.md#parallel_for_each) 算法并行计算 [std：： array](../../standard-library/array-class-stl.md) 对象中质数的计数。

## <a name="example"></a>示例

下面的示例计算数组中质数的计数两次。 该示例首先使用 [std：： for_each](../../standard-library/algorithm-functions.md#for_each) 算法按顺序计算计数。 然后，该示例使用 `parallel_for_each` 算法并行执行相同的任务。 示例还控制台输出了进行两种计算所需的时间。

[!code-cpp[concrt-parallel-count-primes#1](../../parallel/concrt/codesnippet/cpp/how-to-write-a-parallel-for-each-loop_1.cpp)]

以下是具有四个处理器的计算机的输出示例。

```Output
serial version:
found 17984 prime numbers
took 6115 ms

parallel version:
found 17984 prime numbers
took 1653 ms
```

## <a name="compiling-the-code"></a>编译代码

若要编译代码，请复制代码，然后将其粘贴到 Visual Studio 项目中，或粘贴到一个名为的文件中， `parallel-count-primes.cpp` 然后在 Visual Studio 命令提示符窗口中运行以下命令。

> **cl.exe/EHsc parallel-count-primes**

## <a name="robust-programming"></a>可靠编程

示例传递到算法的 lambda 表达式 `parallel_for_each` 使用 `InterlockedIncrement` 函数来启用循环的并行迭代，以同时递增计数器。 如果使用等函数同步对 `InterlockedIncrement` 共享资源的访问，则可以在代码中显示性能瓶颈。 可以使用无锁同步机制（例如 [concurrency：：可组合](../../parallel/concrt/reference/combinable-class.md) 类）来消除对共享资源的同时访问。 有关 `combinable` 以这种方式使用类的示例，请参阅 [如何：使用可组合来提高性能](../../parallel/concrt/how-to-use-combinable-to-improve-performance.md)。

## <a name="see-also"></a>请参阅

[并行算法](../../parallel/concrt/parallel-algorithms.md)<br/>
[parallel_for_each 函数](reference/concurrency-namespace-functions.md#parallel_for_each)
