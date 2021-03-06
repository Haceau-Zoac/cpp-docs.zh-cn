---
description: 了解详细信息： &lt; unordered_set &gt; 运算符
title: '&lt;unordered_set&gt; 运算符'
ms.date: 11/04/2016
f1_keywords:
- unordered_set/std::operator!=
- unordered_set/std::operator==
ms.assetid: 8653eea6-12f2-4dd7-aa2f-db38a71599a0
ms.openlocfilehash: 6404ea9348dedea1e8ecdd4eefbca6b7c1b8158f
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97153728"
---
# <a name="ltunordered_setgt-operators"></a>&lt;unordered_set&gt; 运算符

## <a name="operator"></a><a name="op_neq"></a> operator！ =

测试位于运算符左侧的 [unordered_set](../standard-library/unordered-set-class.md) 对象是否与位于右侧的 unordered_set 对象不相等。

```cpp
bool operator!=(const unordered_set <Key, Hash, Pred, Allocator>& left, const unordered_set <Key, Hash, Pred, Allocator>& right);
```

### <a name="parameters"></a>parameters

*左中*\
一个 `unordered_set` 类型的对象。

*然后*\
一个 `unordered_set` 类型的对象。

### <a name="return-value"></a>返回值

**`true`** 如果 unordered_sets 不相等，则为; 否则为。 **`false`** 如果它们相等，则为。

### <a name="remarks"></a>备注

在其中存储元素的二元顺序不会影响 unordered_set 对象之间的比较。 如果两个 unordered_set 具有相同的元素数，并且一个容器中的元素是另一个容器中的元素的排列，则这两个 unordered_set 相等。 否则，它们不相等。

### <a name="example"></a>示例

```cpp
// unordered_set_ne.cpp
// compile by using: cl.exe /EHsc /nologo /W4 /MTd
#include <unordered_set>
#include <iostream>
#include <ios>

int main()
{
    using namespace std;

    unordered_set<char> c1, c2, c3;

    c1.insert('a');
    c1.insert('b');
    c1.insert('c');

    c2.insert('c');
    c2.insert('a');
    c2.insert('d');

    c3.insert('c');
    c3.insert('a');
    c3.insert('b');

   cout << boolalpha;
   cout << "c1 != c2: " << (c1 != c2) << endl;
   cout << "c1 != c3: " << (c1 != c3) << endl;
   cout << "c2 != c3: " << (c2 != c3) << endl;

    return (0);
}
```

**输出：**

`c1 != c2: true`

`c1 != c3: false`

`c2 != c3: true`

## <a name="operator"></a><a name="op_eq_eq"></a> operator = =

测试位于运算符左侧的 [unordered_set](../standard-library/unordered-set-class.md) 对象是否与位于右侧的 unordered_set 对象相等。

```cpp
bool operator==(const unordered_set <Key, Hash, Pred, Allocator>& left, const unordered_set <Key, Hash, Pred, Allocator>& right);
```

### <a name="parameters"></a>parameters

*左中*\
一个 `unordered_set` 类型的对象。

*然后*\
一个 `unordered_set` 类型的对象。

### <a name="return-value"></a>返回值

**`true`** 如果 unordered_sets 相等，则为; 否则为。 **`false`** 如果它们不相等，则为。

### <a name="remarks"></a>备注

在其中存储元素的二元顺序不会影响 unordered_set 对象之间的比较。 如果两个 unordered_set 具有相同的元素数，并且一个容器中的元素是另一个容器中的元素的排列，则这两个 unordered_set 相等。 否则，它们不相等。

### <a name="example"></a>示例

```cpp
// unordered_set_eq.cpp
// compile by using: cl.exe /EHsc /nologo /W4 /MTd
#include <unordered_set>
#include <iostream>
#include <ios>

int main()
{
    using namespace std;

    unordered_set<char> c1, c2, c3;

    c1.insert('a');
    c1.insert('b');
    c1.insert('c');

    c2.insert('c');
    c2.insert('a');
    c2.insert('d');

    c3.insert('c');
    c3.insert('a');
    c3.insert('b');

   cout << boolalpha;
   cout << "c1 == c2: " << (c1 == c2) << endl;
   cout << "c1 == c3: " << (c1 == c3) << endl;
   cout << "c2 == c3: " << (c2 == c3) << endl;

    return (0);
}
```

```Output
c1 == c2: false
c1 == c3: true
c2 == c3: false
```

## <a name="operator-multiset"></a><a name="op_neq_unordered_multiset"></a> operator！ = (多集) 

测试位于运算符左侧的 [unordered_multiset](../standard-library/unordered-multiset-class.md) 对象是否与位于右侧的 unordered_multiset 对象不相等。

```cpp
bool operator!=(const unordered_multiset <Key, Hash, Pred, Allocator>& left, const unordered_multiset <Key, Hash, Pred, Allocator>& right);
```

### <a name="parameters"></a>parameters

*左中*\
一个 `unordered_multiset` 类型的对象。

*然后*\
一个 `unordered_multiset` 类型的对象。

### <a name="return-value"></a>返回值

**`true`** 如果 unordered_multisets 不相等，则为; 否则为。 **`false`** 如果它们相等，则为。

### <a name="remarks"></a>备注

在其中存储元素的二元顺序不会影响 unordered_multiset 对象之间的比较。 如果两个 unordered_multiset 具有相同的元素数，并且一个容器中的元素是另一个容器中的元素的排列，则这两个 unordered_multiset 相等。 否则，它们不相等。

### <a name="example"></a>示例

```cpp
// unordered_multiset_ne.cpp
// compile by using: cl.exe /EHsc /nologo /W4 /MTd
#include <unordered_set>
#include <iostream>
#include <ios>

int main()
{
    using namespace std;

    unordered_multiset<char> c1, c2, c3;

    c1.insert('a');
    c1.insert('b');
    c1.insert('c');
    c1.insert('c');

    c2.insert('c');
    c2.insert('c');
    c2.insert('a');
    c2.insert('d');

    c3.insert('c');
    c3.insert('c');
    c3.insert('a');
    c3.insert('b');

   cout << boolalpha;
   cout << "c1 != c2: " << (c1 != c2) << endl;
   cout << "c1 != c3: " << (c1 != c3) << endl;
   cout << "c2 != c3: " << (c2 != c3) << endl;

    return (0);
}
```

```Output
c1 != c2: true
c1 != c3: false
c2 != c3: true
```

## <a name="operator-multiset"></a><a name="op_eq_eq_unordered_multiset"></a> operator = = (多集) 

测试位于运算符左侧的 [unordered_multiset](../standard-library/unordered-multiset-class.md) 对象是否与位于右侧的 unordered_multiset 对象相等。

```cpp
bool operator==(const unordered_multiset <Key, Hash, Pred, Allocator>& left, const unordered_multiset <Key, Hash, Pred, Allocator>& right);
```

### <a name="parameters"></a>parameters

*左中*\
一个 `unordered_multiset` 类型的对象。

*然后*\
一个 `unordered_multiset` 类型的对象。

### <a name="return-value"></a>返回值

**`true`** 如果 unordered_multisets 相等，则为; 否则为。 **`false`** 如果它们不相等，则为。

### <a name="remarks"></a>备注

在其中存储元素的二元顺序不会影响 unordered_multiset 对象之间的比较。 如果两个 unordered_multiset 具有相同的元素数，并且一个容器中的元素是另一个容器中的元素的排列，则这两个 unordered_multiset 相等。 否则，它们不相等。

### <a name="example"></a>示例

```cpp
// unordered_multiset_eq.cpp
// compile by using: cl.exe /EHsc /nologo /W4 /MTd
#include <unordered_set>
#include <iostream>
#include <ios>

int main()
{
    using namespace std;

    unordered_multiset<char> c1, c2, c3;

    c1.insert('a');
    c1.insert('b');
    c1.insert('c');
    c1.insert('c');

    c2.insert('c');
    c2.insert('c');
    c2.insert('a');
    c2.insert('d');

    c3.insert('c');
    c3.insert('c');
    c3.insert('a');
    c3.insert('b');

   cout << boolalpha;
   cout << "c1 == c2: " << (c1 == c2) << endl;
   cout << "c1 == c3: " << (c1 == c3) << endl;
   cout << "c2 == c3: " << (c2 == c3) << endl;

    return (0);
}
```

```Output
c1 == c2: false
c1 == c3: true
c2 == c3: false
```
