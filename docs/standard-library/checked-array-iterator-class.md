---
description: 了解详细信息： checked_array_iterator 类
title: checked_array_iterator 类
ms.date: 03/27/2019
f1_keywords:
- iterator/checked_array_iterator
- iterator/stdext::checked_array_iterator::difference_type
- iterator/stdext::checked_array_iterator::pointer
- iterator/stdext::checked_array_iterator::reference
- iterator/stdext::checked_array_iterator::base
helpviewer_keywords:
- stdext::checked_array_iterator [C++], difference_type
- stdext::checked_array_iterator [C++], pointer
- stdext::checked_array_iterator [C++], reference
- stdext::checked_array_iterator [C++], base
ms.assetid: 7f07185e-d588-4ae3-9c4f-84ec4aa25a28
ms.openlocfilehash: 0db327613826105ccd65800246ad1bd16ffbf923
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97325189"
---
# <a name="checked_array_iterator-class"></a>checked_array_iterator 类

通过 `checked_array_iterator` 类，可以将数组或指针转换为经检查的迭代器。 使用此类作为原始指针或数组的包装器（使用 [make_checked_array_iterator](../standard-library/iterator-functions.md#make_checked_array_iterator) 函数）可以有针对性地提供检查并管理未经检查的指针警告，无需从全局静默处理这些警告。 如有必要，可以使用此类的未经检查版本 [unchecked_array_iterator](../standard-library/unchecked-array-iterator-class.md)。

> [!NOTE]
> 此类为 C++ 标准库的 Microsoft 扩展。 使用该函数实现的代码不可移植到不支持该 Microsoft 扩展的 C++ 标准生成环境中。 有关演示如何编写无需使用此类的代码的示例，请参阅下面第二个示例。

## <a name="syntax"></a>语法

```cpp
template <class _Iterator>
class checked_array_iterator;
```

## <a name="remarks"></a>备注

此类在 [stdext](../standard-library/stdext-namespace.md) 命名空间中定义。

有关已检查的迭代器功能的详细信息和示例代码，请参阅[已检查的迭代器](../standard-library/checked-iterators.md)。

## <a name="examples"></a>示例

下面的示例演示如何定义和使用经检查的数组迭代器。

如果目标不够大，无法保留复制的所有元素，例如你将行：

```cpp
copy(a, a + 5, checked_array_iterator<int*>(b, 5));
```

to

```cpp
copy(a, a + 5, checked_array_iterator<int*>(b, 4));
```

将发生运行时错误。

```cpp
// compile with: /EHsc /W4 /MTd
#include <algorithm>
#include <iostream>

using namespace std;
using namespace stdext;

int main() {
   int a[]={0, 1, 2, 3, 4};
   int b[5];
   copy(a, a + 5, checked_array_iterator<int*>(b, 5));

   cout << "(";
   for (int i = 0 ; i < 5 ; i++)
      cout << " " << b[i];
   cout << " )" << endl;

   // constructor example
   checked_array_iterator<int*> checked_out_iter(b, 5);
   copy(a, a + 5, checked_out_iter);

   cout << "(";
   for (int i = 0 ; i < 5 ; i++)
      cout << " " << b[i];
   cout << " )" << endl;
}
/* Output:
( 0 1 2 3 4 )
( 0 1 2 3 4 )
*/
```

若要在使用 C++ 标准库算法时避免使用 `checked_array_iterator` 类，请考虑使用 `vector` 而不是动态分配的数组。 下面的示例演示如何执行此操作。

```cpp
// compile with: /EHsc /W4 /MTd

#include <algorithm>
#include <iostream>
#include <vector>

using namespace std;

int main()
{
    std::vector<int> v(10);
    int *arr = new int[10];
    for (int i = 0; i < 10; ++i)
    {
        v[i] = i;
        arr[i] = i;
    }

    // std::copy(v.begin(), v.end(), arr); will result in
    // warning C4996. To avoid this warning while using int *,
    // use the Microsoft extension checked_array_iterator.
    std::copy(v.begin(), v.end(),
              stdext::checked_array_iterator<int *>(arr, 10));

    // Instead of using stdext::checked_array_iterator and int *,
    // consider using std::vector to encapsulate the array. This will
    // result in no warnings, and the code will be portable.
    std::vector<int> arr2(10);    // Similar to int *arr = new int[10];
    std::copy(v.begin(), v.end(), arr2.begin());

    for (int j = 0; j < arr2.size(); ++j)
    {
        cout << " " << arr2[j];
    }
    cout << endl;

    return 0;
}
/* Output:
0 1 2 3 4 5 6 7 8 9
*/
```

### <a name="constructors"></a>构造函数

|构造函数|说明|
|-|-|
|[checked_array_iterator](#checked_array_iterator)|构造默认 `checked_array_iterator` 或从基础迭代器构造 `checked_array_iterator`。|

### <a name="typedefs"></a>Typedef

|类型名称|描述|
|-|-|
|[difference_type](#difference_type)|一种类型，此类型提供引用同一容器中的元素的两个 `checked_array_iterator` 之间的差异。|
|[变为](#pointer)|一种类型，此类型提供指向 `checked_array_iterator` 所发现元素的指针。|
|[reference](#reference)|一种类型，此类型提供对 `checked_array_iterator` 所发现元素的引用。|

### <a name="member-functions"></a>成员函数

|成员函数|说明|
|-|-|
|[base](#base)|将基础迭代器从其 `checked_array_iterator` 恢复。|

### <a name="operators"></a>运算符

|运算符|描述|
|-|-|
|[operator = =](#op_eq_eq)|测试两个 `checked_array_iterator` 是否相等。|
|[operator！ =](#op_neq)|测试两个 `checked_array_iterator` 是否不相等。|
|[运算符<](#op_lt)|测试运算符左侧的 `checked_array_iterator` 是否小于右侧的 `checked_array_iterator`。|
|[运算符>](#op_gt)|测试运算符左侧的 `checked_array_iterator` 是否大于右侧的 `checked_array_iterator`。|
|[运算符<=](#op_lt_eq)|测试运算符左侧的 `checked_array_iterator` 是否小于或等于右侧的 `checked_array_iterator`。|
|[运算符>=](#op_gt_eq)|测试运算符左侧的 `checked_array_iterator` 是否大于或等于右侧的 `checked_array_iterator`。|
|[操作员](#op_star)|返回 `checked_array_iterator` 发现的元素。|
|[operator->](#op_arrow)|返回指向 `checked_array_iterator` 发现的元素的指针。|
|[operator + +](#op_add_add)|将 `checked_array_iterator` 递增到下一元素。|
|[operator--](#operator--)|将 `checked_array_iterator` 递减到前一元素。|
|[运算符 + =](#op_add_eq)|将指定偏移量添加到 `checked_array_iterator`。|
|[operator +](#op_add)|将偏移量添加到迭代器，并返回在新偏移位置处发现插入元素的新 `checked_array_iterator`。|
|[operator-=](#operator-_eq)|从 `checked_array_iterator` 递减指定偏移量。|
|[操作员](#operator-)|从迭代器递减偏移量，并返回在新偏移位置处发现插入元素的新 `checked_array_iterator`。|
|[operator&#91;&#93;](#op_at)|返回对于从 `checked_array_iterator` 发现的元素偏移指定个位置的元素的引用。|

## <a name="requirements"></a>要求

**标头：**\<iterator>

**命名空间：** stdext

## <a name="checked_array_iteratorbase"></a><a name="base"></a> checked_array_iterator：： base

将基础迭代器从其 `checked_array_iterator` 恢复。

```cpp
_Iterator base() const;
```

### <a name="remarks"></a>备注

有关更多信息，请参见 [Checked Iterators](../standard-library/checked-iterators.md)。

### <a name="example"></a>示例

```cpp
// checked_array_iterators_base.cpp
// compile with: /EHsc
#include <iterator>
#include <vector>
#include <iostream>

int main() {
   using namespace std;

   int V1[10];

   for (int i = 0; i < 10 ; i++)
      V1[i] = i;

   int* bpos;

   stdext::checked_array_iterator<int*> rpos(V1, 10);
   rpos++;

   bpos = rpos.base ( );
   cout << "The iterator underlying rpos is bpos & it points to: "
        << *bpos << "." << endl;
}
/* Output:
The iterator underlying rpos is bpos & it points to: 1.
*/
```

## <a name="checked_array_iteratorchecked_array_iterator"></a><a name="checked_array_iterator"></a> checked_array_iterator：： checked_array_iterator

构造默认 `checked_array_iterator` 或从基础迭代器构造 `checked_array _iterator`。

```cpp
checked_array_iterator();

checked_array_iterator(
    ITerator ptr,
    size_t size,
    size_t index = 0);
```

### <a name="parameters"></a>parameters

*ptr*\
指向数组的指针。

*规格*\
数组大小。

index\
（可选）数组中用于初始化迭代器的元素。  默认情况下，将迭代器初始化为数组中的第一个元素。

### <a name="remarks"></a>备注

有关更多信息，请参见 [Checked Iterators](../standard-library/checked-iterators.md)。

### <a name="example"></a>示例

```cpp
// checked_array_iterators_ctor.cpp
// compile with: /EHsc
#include <iterator>
#include <iostream>

using namespace std;
using namespace stdext;

int main() {
   int a[] = {0, 1, 2, 3, 4};
   int b[5];
   copy(a, a + 5, checked_array_iterator<int*>(b,5));

   for (int i = 0 ; i < 5 ; i++)
      cout << b[i] << " ";
   cout << endl;

   checked_array_iterator<int*> checked_output_iterator(b,5);
   copy (a, a + 5, checked_output_iterator);
   for (int i = 0 ; i < 5 ; i++)
      cout << b[i] << " ";
   cout << endl;

   checked_array_iterator<int*> checked_output_iterator2(b,5,3);
   cout << *checked_output_iterator2 << endl;
}
/* Output:
0 1 2 3 4
0 1 2 3 4
3
*/
```

## <a name="checked_array_iteratordifference_type"></a><a name="difference_type"></a> checked_array_iterator：:d ifference_type

一种类型，此类型提供引用同一容器中的元素的两个 `checked_array_iterator` 之间的差异。

```cpp
typedef typename iterator_traits<_Iterator>::difference_type difference_type;
```

### <a name="remarks"></a>备注

`checked_array_iterator` 差异类型与迭代器差异类型相同。

有关代码示例，请参阅 [checked_array_iterator：： operator []](#op_at) 。

有关更多信息，请参见 [Checked Iterators](../standard-library/checked-iterators.md)。

## <a name="checked_array_iteratoroperator"></a><a name="op_eq_eq"></a> checked_array_iterator：： operator = =

测试两个 `checked_array_iterator` 是否相等。

```cpp
bool operator==(const checked_array_iterator<_Iterator>& right) const;
```

### <a name="parameters"></a>parameters

*然后*\
作为检查相等性依据的 `checked_array_iterator`。

### <a name="remarks"></a>备注

有关更多信息，请参见 [Checked Iterators](../standard-library/checked-iterators.md)。

### <a name="example"></a>示例

```cpp
// checked_array_iterators_opeq.cpp
// compile with: /EHsc
#include <iterator>
#include <iostream>

using namespace std;
using namespace stdext;

int main() {
   int a[] = {0, 1, 2, 3, 4};
   int b[5];
   copy(a, a + 5, checked_array_iterator<int*>(b,5));
   copy(a, a + 5, checked_array_iterator<int*>(b,5));

   checked_array_iterator<int*> checked_output_iterator(b,5);
   checked_array_iterator<int*> checked_output_iterator2(b,5);

   if (checked_output_iterator2 == checked_output_iterator)
      cout << "checked_array_iterators are equal" << endl;
   else
      cout << "checked_array_iterators are not equal" << endl;

   copy (a, a + 5, checked_output_iterator);
   checked_output_iterator++;

   if (checked_output_iterator2 == checked_output_iterator)
      cout << "checked_array_iterators are equal" << endl;
   else
      cout << "checked_array_iterators are not equal" << endl;
}
/* Output:
checked_array_iterators are equal
checked_array_iterators are not equal
*/
```

## <a name="checked_array_iteratoroperator"></a><a name="op_neq"></a> checked_array_iterator：： operator！ =

测试两个 `checked_array_iterator` 是否不相等。

```cpp
bool operator!=(const checked_array_iterator<_Iterator>& right) const;
```

### <a name="parameters"></a>parameters

*然后*\
作为检查不相等性依据的 `checked_array_iterator`。

### <a name="remarks"></a>备注

有关更多信息，请参见 [Checked Iterators](../standard-library/checked-iterators.md)。

### <a name="example"></a>示例

```cpp
// checked_array_iterators_opneq.cpp
// compile with: /EHsc
#include <iterator>
#include <iostream>

using namespace std;
using namespace stdext;

int main() {
   int a[] = {0, 1, 2, 3, 4};
   int b[5];
   copy(a, a + 5, checked_array_iterator<int*>(b,5));
   copy(a, a + 5, checked_array_iterator<int*>(b,5));

   checked_array_iterator<int*> checked_output_iterator(b,5);
   checked_array_iterator<int*> checked_output_iterator2(b,5);

   if (checked_output_iterator2 != checked_output_iterator)
      cout << "checked_array_iterators are not equal" << endl;
   else
      cout << "checked_array_iterators are equal" << endl;

   copy (a, a + 5, checked_output_iterator);
   checked_output_iterator++;

   if (checked_output_iterator2 != checked_output_iterator)
      cout << "checked_array_iterators are not equal" << endl;
   else
      cout << "checked_array_iterators are equal" << endl;
}
/* Output:
checked_array_iterators are equal
checked_array_iterators are not equal
*/
```

## <a name="checked_array_iteratoroperatorlt"></a><a name="op_lt"></a> checked_array_iterator：： operator&lt;

测试运算符左侧的 `checked_array_iterator` 是否小于右侧的 `checked_array_iterator`。

```cpp
bool operator<(const checked_array_iterator<_Iterator>& right) const;
```

### <a name="parameters"></a>parameters

*然后*\
作为检查不相等性依据的 `checked_array_iterator`。

### <a name="remarks"></a>备注

有关更多信息，请参见 [Checked Iterators](../standard-library/checked-iterators.md)。

### <a name="example"></a>示例

```cpp
// checked_array_iterators_oplt.cpp
// compile with: /EHsc
#include <iterator>
#include <iostream>

using namespace std;
using namespace stdext;

int main() {
   int a[] = {0, 1, 2, 3, 4};
   int b[5];
   copy(a, a + 5, checked_array_iterator<int*>(b,5));
   copy(a, a + 5, checked_array_iterator<int*>(b,5));

   checked_array_iterator<int*> checked_output_iterator(b,5);
   checked_array_iterator<int*> checked_output_iterator2(b,5);

   if (checked_output_iterator2 < checked_output_iterator)
      cout << "checked_output_iterator2 is less than checked_output_iterator" << endl;
   else
      cout << "checked_output_iterator2 is not less than checked_output_iterator" << endl;

   copy (a, a + 5, checked_output_iterator);
   checked_output_iterator++;

   if (checked_output_iterator2 < checked_output_iterator)
      cout << "checked_output_iterator2 is less than checked_output_iterator" << endl;
   else
      cout << "checked_output_iterator2 is not less than checked_output_iterator" << endl;
}
/* Output:
checked_output_iterator2 is not less than checked_output_iterator
checked_output_iterator2 is less than checked_output_iterator
*/
```

## <a name="checked_array_iteratoroperatorgt"></a><a name="op_gt"></a> checked_array_iterator：： operator&gt;

测试运算符左侧的 `checked_array_iterator` 是否大于右侧的 `checked_array_iterator`。

```cpp
bool operator>(const checked_array_iterator<_Iterator>& right) const;
```

### <a name="parameters"></a>parameters

*然后*\
要针对其进行比较的 `checked_array_iterator`。

### <a name="remarks"></a>备注

有关代码示例，请参阅 [checked_array_iterator::operator&lt;](#op_lt)。

有关更多信息，请参见 [Checked Iterators](../standard-library/checked-iterators.md)。

## <a name="checked_array_iteratoroperatorlt"></a><a name="op_lt_eq"></a> checked_array_iterator：： operator&lt;=

测试运算符左侧的 `checked_array_iterator` 是否小于或等于右侧的 `checked_array_iterator`。

```cpp
bool operator<=(const checked_array_iterator<_Iterator>& right) const;
```

### <a name="parameters"></a>parameters

*然后*\
要针对其进行比较的 `checked_array_iterator`。

### <a name="remarks"></a>备注

有关代码示例，请参阅[checked_array_iterator：： operator &gt; = ](#op_gt_eq) 。

有关更多信息，请参见 [Checked Iterators](../standard-library/checked-iterators.md)。

## <a name="checked_array_iteratoroperatorgt"></a><a name="op_gt_eq"></a> checked_array_iterator：： operator&gt;=

测试运算符左侧的 `checked_array_iterator` 是否大于或等于右侧的 `checked_array_iterator`。

```cpp
bool operator>=(const checked_array_iterator<_Iterator>& right) const;
```

### <a name="parameters"></a>parameters

*然后*\
要针对其进行比较的 `checked_array_iterator`。

### <a name="remarks"></a>备注

有关更多信息，请参见 [Checked Iterators](../standard-library/checked-iterators.md)。

### <a name="example"></a>示例

```cpp
// checked_array_iterators_opgteq.cpp
// compile with: /EHsc
#include <iterator>
#include <iostream>

using namespace std;
using namespace stdext;

int main() {
   int a[] = {0, 1, 2, 3, 4};
   int b[5];
   copy(a, a + 5, checked_array_iterator<int*>(b,5));
   copy(a, a + 5, checked_array_iterator<int*>(b,5));

   checked_array_iterator<int*> checked_output_iterator(b,5);
   checked_array_iterator<int*> checked_output_iterator2(b,5);

   if (checked_output_iterator2 >= checked_output_iterator)
      cout << "checked_output_iterator2 is greater than or equal to checked_output_iterator" << endl;
   else
      cout << "checked_output_iterator2 is less than checked_output_iterator" << endl;

   copy (a, a + 5, checked_output_iterator);
   checked_output_iterator++;

   if (checked_output_iterator2 >= checked_output_iterator)
      cout << "checked_output_iterator2 is greater than or equal to checked_output_iterator" << endl;
   else
      cout << "checked_output_iterator2 is less than checked_output_iterator" << endl;
}
/* Output:
checked_output_iterator2 is greater than or equal to checked_output_iterator
checked_output_iterator2 is less than checked_output_iterator
*/
```

## <a name="checked_array_iteratoroperator"></a><a name="op_star"></a> checked_array_iterator：： operator *

返回 `checked_array_iterator` 发现的元素。

```cpp
reference operator*() const;
```

### <a name="return-value"></a>返回值

由 `checked_array_iterator` 寻址的元素的值。

### <a name="remarks"></a>备注

有关更多信息，请参见 [Checked Iterators](../standard-library/checked-iterators.md)。

### <a name="example"></a>示例

```cpp
// checked_array_iterator_pointer.cpp
// compile with: /EHsc
#include <iterator>
#include <algorithm>
#include <vector>
#include <utility>
#include <iostream>

using namespace std;
using namespace stdext;

int main() {
   int a[] = {0, 1, 2, 3, 4};
   int b[5];
   pair<int, int> c[1];
   copy(a, a + 5, checked_array_iterator<int*>(b,5));

   for (int i = 0 ; i < 5 ; i++)
      cout << b[i] << endl;

    c[0].first = 10;
    c[0].second = 20;

   checked_array_iterator<int*> checked_output_iterator(b,5);
   checked_array_iterator<int*>::pointer p = &(*checked_output_iterator);
   checked_array_iterator<pair<int, int>*> chk_c(c, 1);
   checked_array_iterator<pair<int, int>*>::pointer p_c = &(*chk_c);

   cout << "b[0] = " << *p << endl;
   cout << "c[0].first = " << p_c->first << endl;
}
/* Output:
0
1
2
3
4
b[0] = 0
c[0].first = 10
*/
```

## <a name="checked_array_iteratoroperator-gt"></a><a name="op_arrow"></a> checked_array_iterator：： operator-&gt;

返回指向 `checked_array_iterator` 发现的元素的指针。

```cpp
pointer operator->() const;
```

### <a name="return-value"></a>返回值

指向由 `checked_array_iterator` 寻址的元素的指针。

### <a name="remarks"></a>备注

有关代码示例，请参阅 [checked_array_iterator::pointer](#pointer)。

有关更多信息，请参见 [Checked Iterators](../standard-library/checked-iterators.md)。

## <a name="checked_array_iteratoroperator"></a><a name="op_add_add"></a> checked_array_iterator：： operator + +

将 `checked_array_iterator` 递增到下一元素。

```cpp
checked_array_iterator& operator++();

checked_array_iterator<_Iterator> operator++(int);
```

### <a name="return-value"></a>返回值

第一个运算符返回前置递增的 `checked_array_iterator`，而第二个运算符为后置递增运算符，返回递增的 `checked_array_iterator` 的副本。

### <a name="remarks"></a>备注

有关更多信息，请参见 [Checked Iterators](../standard-library/checked-iterators.md)。

### <a name="example"></a>示例

```cpp
// checked_array_iterators_op_plus_plus.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main() {
   using namespace stdext;
   using namespace std;
   int a[] = {6, 3, 77, 199, 222};
   int b[5];
   copy(a, a + 5, checked_array_iterator<int*>(b,5));

   checked_array_iterator<int*> checked_output_iterator(b,5);

   cout << *checked_output_iterator << endl;
   ++checked_output_iterator;
   cout << *checked_output_iterator << endl;
   checked_output_iterator++;
   cout << *checked_output_iterator << endl;
}
/* Output:
6
3
77
*/
```

## <a name="checked_array_iteratoroperator--"></a><a name="operator--"></a> checked_array_iterator：： operator--

将 `checked_array_iterator` 递减到前一元素。

```cpp
checked_array_iterator<_Iterator>& operator--();

checked_array_iterator<_Iterator> operator--(int);
```

### <a name="return-value"></a>返回值

第一个运算符返回前置递减的 `checked_array_iterator`，而第二个运算符为后置递减运算符，返回递减的 `checked_array_iterator` 的副本。

### <a name="remarks"></a>备注

有关更多信息，请参见 [Checked Iterators](../standard-library/checked-iterators.md)。

### <a name="example"></a>示例

```cpp
// checked_array_iterators_op_minus_minus.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main() {
   using namespace stdext;
   using namespace std;
   int a[] = {6, 3, 77, 199, 222};
   int b[5];
   copy(a, a + 5, checked_array_iterator<int*>(b,5));

   checked_array_iterator<int*> checked_output_iterator(b,5);

   cout << *checked_output_iterator << endl;
   checked_output_iterator++;
   cout << *checked_output_iterator << endl;
   checked_output_iterator--;
   cout << *checked_output_iterator << endl;
}
/* Output:
6
3
6
*/
```

## <a name="checked_array_iteratoroperator"></a><a name="op_add_eq"></a> checked_array_iterator：： operator + =

将指定偏移量添加到 `checked_array_iterator`。

```cpp
checked_array_iterator<_Iterator>& operator+=(difference_type _Off);
```

### <a name="parameters"></a>parameters

*_Off*\
迭代器要递增的偏移量。

### <a name="return-value"></a>返回值

由 `checked_array_iterator` 寻址的元素的引用。

### <a name="remarks"></a>备注

有关更多信息，请参见 [Checked Iterators](../standard-library/checked-iterators.md)。

### <a name="example"></a>示例

```cpp
// checked_array_iterators_op_plus_eq.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main() {
   using namespace stdext;
   using namespace std;
   int a[] = {6, 3, 77, 199, 222};
   int b[5];
   copy(a, a + 5, checked_array_iterator<int*>(b,5));

   checked_array_iterator<int*> checked_output_iterator(b,5);

   cout << *checked_output_iterator << endl;
   checked_output_iterator += 3;
   cout << *checked_output_iterator << endl;
}
/* Output:
6
199
*/
```

## <a name="checked_array_iteratoroperator"></a><a name="op_add"></a> checked_array_iterator：： operator +

将偏移量添加到迭代器，并返回在新偏移位置处发现插入元素的新 `checked_array_iterator`。

```cpp
checked_array_iterator<_Iterator> operator+(difference_type _Off) const;
```

### <a name="parameters"></a>parameters

*_Off*\
要添加到 `checked_array_iterator` 的偏移量。

### <a name="return-value"></a>返回值

寻址偏移元素的 `checked_array_iterator`。

### <a name="remarks"></a>备注

有关更多信息，请参见 [Checked Iterators](../standard-library/checked-iterators.md)。

### <a name="example"></a>示例

```cpp
// checked_array_iterators_op_plus.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main() {
   using namespace stdext;
   using namespace std;
   int a[] = {6, 3, 77, 199, 222};
   int b[5];
   copy(a, a + 5, checked_array_iterator<int*>(b,5));

   checked_array_iterator<int*> checked_output_iterator(b,5);

   cout << *checked_output_iterator << endl;
   checked_output_iterator = checked_output_iterator + 3;
   cout << *checked_output_iterator << endl;
}
/* Output:
6
199
*/
```

## <a name="checked_array_iteratoroperator-"></a><a name="operator-_eq"></a> checked_array_iterator：： operator-=

从 `checked_array_iterator` 递减指定偏移量。

```cpp
checked_array_iterator<_Iterator>& operator-=(difference_type _Off);
```

### <a name="parameters"></a>parameters

*_Off*\
迭代器要递增的偏移量。

### <a name="return-value"></a>返回值

由 `checked_array_iterator` 寻址的元素的引用。

### <a name="remarks"></a>备注

有关更多信息，请参见 [Checked Iterators](../standard-library/checked-iterators.md)。

### <a name="example"></a>示例

```cpp
// checked_array_iterators_op_minus_eq.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main() {
   using namespace stdext;
   using namespace std;
   int a[] = {6, 3, 77, 199, 222};
   int b[5];
   copy(a, a + 5, checked_array_iterator<int*>(b,5));

   checked_array_iterator<int*> checked_output_iterator(b,5);

   checked_output_iterator += 3;
   cout << *checked_output_iterator << endl;
   checked_output_iterator -= 2;
   cout << *checked_output_iterator << endl;
}
/* Output:
199
3
*/
```

## <a name="checked_array_iteratoroperator-"></a><a name="operator-"></a> checked_array_iterator：： operator-

从迭代器递减偏移量，并返回在新偏移位置处发现插入元素的新 `checked_array_iterator`。

```cpp
checked_array_iterator<_Iterator> operator-(difference_type _Off) const;

difference_type operator-(const checked_array_iterator& right) const;
```

### <a name="parameters"></a>parameters

*_Off*\
要从 `checked_array_iterator` 中减去的偏移量。

### <a name="return-value"></a>返回值

寻址偏移元素的 `checked_array_iterator`。

### <a name="remarks"></a>备注

有关更多信息，请参见 [Checked Iterators](../standard-library/checked-iterators.md)。

## <a name="checked_array_iteratoroperator"></a><a name="op_at"></a> checked_array_iterator：： operator []

返回对于从 `checked_array_iterator` 发现的元素偏移指定个位置的元素的引用。

```cpp
reference operator[](difference_type _Off) const;
```

### <a name="parameters"></a>parameters

*_Off*\
`checked_array_iterator` 地址的偏移量。

### <a name="return-value"></a>返回值

对元素偏移量的引用。

### <a name="remarks"></a>备注

有关更多信息，请参见 [Checked Iterators](../standard-library/checked-iterators.md)。

### <a name="example"></a>示例

```cpp
// checked_array_iterators_op_diff.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main() {
   using namespace std;
   int V1[10];

   for (int i = 0; i < 10 ; i++)
      V1[i] = i;

   // Declare a difference type for a parameter
   stdext::checked_array_iterator<int*>::difference_type diff = 2;

   stdext::checked_array_iterator<int*> VChkIter(V1, 10);

   stdext::checked_array_iterator<int*>::reference refrpos = VChkIter [diff];

   cout << refrpos + 1 << endl;
}
/* Output:
3
*/
```

## <a name="checked_array_iteratorpointer"></a><a name="pointer"></a> checked_array_iterator：:p ointer

一种类型，此类型提供指向 `checked_array_iterator` 所发现元素的指针。

```cpp
typedef typename iterator_traits<_Iterator>::pointer pointer;
```

### <a name="remarks"></a>备注

有关代码示例，请参阅 [checked_array_iterator：： operator *](#op_star) 。

有关更多信息，请参见 [Checked Iterators](../standard-library/checked-iterators.md)。

## <a name="checked_array_iteratorreference"></a><a name="reference"></a> checked_array_iterator：： reference

一种类型，此类型提供对 `checked_array_iterator` 所发现元素的引用。

```cpp
typedef typename iterator_traits<_Iterator>::reference reference;
```

### <a name="remarks"></a>备注

有关代码示例，请参阅 [checked_array_iterator：： operator []](#op_at) 。

有关更多信息，请参见 [Checked Iterators](../standard-library/checked-iterators.md)。

## <a name="see-also"></a>请参阅

[\<iterator>](../standard-library/iterator.md)\
[C + + 标准库参考](../standard-library/cpp-standard-library-reference.md)
