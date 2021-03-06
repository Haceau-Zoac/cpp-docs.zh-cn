---
description: 了解详细信息： fpos 类
title: fpos 类
ms.date: 03/27/2019
f1_keywords:
- iosfwd/std::fpos
- iosfwd/std::fpos::seekpos
- iosfwd/std::fpos::state
- iosfwd/std::fpos::operator streamoff
helpviewer_keywords:
- std::fpos [C++]
- std::fpos [C++], seekpos
- std::fpos [C++], state
ms.assetid: ffd0827c-fa34-47f4-b10e-5cb707fcde47
ms.openlocfilehash: 22b9a5e69b179ef4206a0664b51b92cc55d4320d
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97232325"
---
# <a name="fpos-class"></a>fpos 类

类模板描述了一个对象，该对象可以存储还原任何流内的任意文件位置指示器所需的所有信息。 类 fpos 的对象 \< **St**> 有效存储至少两个成员对象：

- 一是 [streamoff](../standard-library/ios-typedefs.md#streamoff) 类型的字节偏移。

- 类型为的类 basic_filebuf 的对象使用的转换状态 `St` 通常为 `mbstate_t` 。

它还能存储 `fpos_t` 类型的任意文件位置，以供 [basic_filebuf](../standard-library/basic-filebuf-class.md) 类的对象使用。 但是，对于文件大小受限的环境，`streamoff` 和 `fpos_t` 有时可能互换使用。 对于不具有依赖于状态的编码的流的环境，实际上可能不会使用 `mbstate_t`。 因此，所存储成员对象的数目可能会有所不同。

## <a name="syntax"></a>语法

```cpp
template <class Statetype>
class fpos
```

### <a name="parameters"></a>parameters

*Statetype*\
状态信息。

### <a name="constructors"></a>构造函数

|构造函数|说明|
|-|-|
|[fpos](#fpos)|创建一个包含有关流中位置（偏移量）信息的对象。|

### <a name="member-functions"></a>成员函数

|成员函数|说明|
|-|-|
|[seekpos](#seekpos)|仅由 C++ 标准库内部使用。 请勿从代码中调用此方法。|
|[state](#state)|设置或返回转换状态。|

### <a name="operators"></a>运算符

|运算符|描述|
|-|-|
|[operator！ =](#op_neq)|测试文件位置指示器是否不相等。|
|[operator +](#op_add)|递增文件位置指示器。|
|[运算符 + =](#op_add_eq)|递增文件位置指示器。|
|[操作员](#operator-)|递减文件位置指示器。|
|[operator-=](#operator-_eq)|递减文件位置指示器。|
|[operator = =](#op_eq_eq)|测试文件位置指示器是否相等。|
|[operator streamoff](#op_streamoff)|将 `fpos` 类型的对象强制转换为 `streamoff` 类型的对象。|

## <a name="requirements"></a>要求

**标头：**\<ios>

**命名空间:** std

## <a name="fposfpos"></a><a name="fpos"></a> fpos：： fpos

创建一个包含有关流中位置（偏移量）信息的对象。

```cpp
fpos(streamoff _Off = 0);

fpos(Statetype _State, fpos_t _Filepos);
```

### <a name="parameters"></a>parameters

*_Off*\
进入流的偏移量。

*_State*\
`fpos` 对象的起始状态。

*_Filepos*\
进入流的偏移量。

### <a name="remarks"></a>备注

第一个构造函数存储相对于文件开头和初始转换状态的偏移量 *_Off* (如果该问题) 。 如果 *_Off* 为-1，则生成的对象表示无效的流位置。

第二个构造函数存储零偏移量并且对象 *_State*。

## <a name="fposoperator"></a><a name="op_neq"></a> fpos：： operator！ =

测试文件位置指示器是否不相等。

```cpp
bool operator!=(const fpos<Statetype>& right) const;
```

### <a name="parameters"></a>parameters

*然后*\
要与之比较的文件位置指示器。

### <a name="return-value"></a>返回值

**`true`** 如果文件位置指示符不相等，则为; 否则为 **`false`** 。

### <a name="remarks"></a>备注

成员函数返回 `!(*this == right)`。

### <a name="example"></a>示例

```cpp
// fpos_op_neq.cpp
// compile with: /EHsc
#include <fstream>
#include <iostream>

int main( )
{
   using namespace std;

   fpos<int> pos1, pos2;
   ifstream file;
   char c;

   // Compare two fpos object
   if ( pos1 != pos2 )
      cout << "File position pos1 and pos2 are not equal" << endl;
   else
      cout << "File position pos1 and pos2 are equal" << endl;

   file.open( "fpos_op_neq.txt" );
   file.seekg( 0 );   // Goes to a zero-based position in the file
   pos1 = file.tellg( );
   file.get( c);
   cout << c << endl;

   // Increment pos1
   pos1 += 1;
   file.get( c );
   cout << c << endl;

   pos1 = file.tellg( ) - fpos<int>( 2);
   file.seekg( pos1 );
   file.get( c );
   cout << c << endl;

   // Increment pos1
   pos1 = pos1 + fpos<int>( 1 );
   file.get(c);
   cout << c << endl;

   pos1 -= fpos<int>( 2 );
   file.seekg( pos1 );
   file.get( c );
   cout << c << endl;

   file.close( );
}
```

## <a name="fposoperator"></a><a name="op_add"></a> fpos：： operator +

递增文件位置指示器。

```cpp
fpos<Statetype> operator+(streamoff _Off) const;
```

### <a name="parameters"></a>parameters

*_Off*\
要按其递增文件位置指示器的偏移量。

### <a name="return-value"></a>返回值

文件中的位置。

### <a name="remarks"></a>备注

此成员函数返回 **fpos(\*this) +=** `_Off`。

### <a name="example"></a>示例

请参阅 [operator!=](#op_neq)，了解使用 `operator+` 的示例。

## <a name="fposoperator"></a><a name="op_add_eq"></a> fpos：： operator + =

递增文件位置指示器。

```cpp
fpos<Statetype>& operator+=(streamoff _Off);
```

### <a name="parameters"></a>parameters

*_Off*\
要按其递增文件位置指示器的偏移量。

### <a name="return-value"></a>返回值

文件中的位置。

### <a name="remarks"></a>备注

成员函数将 *_Off* 添加到存储的 offset 成员对象，然后返回 **\* this**。 对于文件内的位置，结果通常仅对不具有状态依赖编码的二进制流有效。

### <a name="example"></a>示例

请参阅 [operator!=](#op_neq)，了解使用 `operator+=` 的示例。

## <a name="fposoperator-"></a><a name="operator-"></a> fpos：： operator-

递减文件位置指示器。

```cpp
streamoff operator-(const fpos<Statetype>& right) const;

fpos<Statetype> operator-(streamoff _Off) const;
```

### <a name="parameters"></a>parameters

*然后*\
文件位置。

*_Off*\
流偏移量。

### <a name="return-value"></a>返回值

第一个成员函数返回 `(streamoff)*this - (streamoff) right`。 第二个成员函数返回 `fpos(*this) -= _Off`。

### <a name="example"></a>示例

请参阅 [operator!=](#op_neq)，了解使用 `operator-` 的示例。

## <a name="fposoperator-"></a><a name="operator-_eq"></a> fpos：： operator-=

递减文件位置指示器。

```cpp
fpos<Statetype>& operator-=(streamoff _Off);
```

### <a name="parameters"></a>parameters

*_Off*\
流偏移量。

### <a name="return-value"></a>返回值

成员函数返回 `fpos(*this) -= _Off`。

### <a name="remarks"></a>备注

对于文件内的位置，结果通常仅对不具有状态依赖编码的二进制流有效。

### <a name="example"></a>示例

请参阅 [operator!=](#op_neq)，了解使用 `operator-=` 的示例。

## <a name="fposoperator"></a><a name="op_eq_eq"></a> fpos：： operator = =

测试文件位置指示器是否相等。

```cpp
bool operator==(const fpos<Statetype>& right) const;
```

### <a name="parameters"></a>parameters

*然后*\
要与之比较的文件位置指示器。

### <a name="return-value"></a>返回值

**`true`** 如果文件位置指示器相等，则为; 否则为。否则为 **`false`** 。

### <a name="remarks"></a>备注

成员函数返回 `(streamoff)*this == (streamoff)right`。

### <a name="example"></a>示例

请参阅 [operator!=](#op_neq)，了解使用 `operator+=` 的示例。

## <a name="fposoperator-streamoff"></a><a name="op_streamoff"></a> fpos：： operator streamoff

将 `fpos` 类型的对象转换为 `streamoff` 类型的对象。

```cpp
operator streamoff() const;
```

### <a name="remarks"></a>备注

成员函数返回存储的偏移成员对象和存储为 `fpos_t` 成员对象一部分的任何其他偏移量。

### <a name="example"></a>示例

```cpp
// fpos_op_streampos.cpp
// compile with: /EHsc
#include <ios>
#include <iostream>
#include <fstream>

int main( )
{
   using namespace std;
   streamoff s;
   ofstream file( "rdbuf.txt");

   fpos<mbstate_t> f = file.tellp( );
   // Is equivalent to ..
   // streampos f = file.tellp( );
   s = f;
   cout << s << endl;
}
```

```Output
0
```

## <a name="fposseekpos"></a><a name="seekpos"></a> fpos：： seekpos

此方法仅由 C++ 标准库内部使用。 请勿从代码中调用此方法。

```cpp
fpos_t seekpos() const;
```

## <a name="fposstate"></a><a name="state"></a> fpos：： state

设置或返回转换状态。

```cpp
Statetype state() const;

void state(Statetype _State);
```

### <a name="parameters"></a>parameters

*_State*\
新的转换状态。

### <a name="return-value"></a>返回值

转换状态。

### <a name="remarks"></a>备注

第一个成员函数返回存储在成员对象中的值 `St` 。 第二个成员函数将 *_State* 存储在 `St` 成员对象中。

### <a name="example"></a>示例

```cpp
// fpos_state.cpp
// compile with: /EHsc
#include <ios>
#include <iostream>
#include <fstream>

int main() {
   using namespace std;
   streamoff s;
   ifstream file( "fpos_state.txt" );

   fpos<mbstate_t> f = file.tellg( );
   char ch;
   while ( !file.eof( ) )
      file.get( ch );
   s = f;
   cout << f.state( ) << endl;
   f.state( 9 );
   cout << f.state( ) << endl;
}
```

## <a name="see-also"></a>请参阅

[C + + 标准库中的线程安全](../standard-library/thread-safety-in-the-cpp-standard-library.md)\
[iostream 编程](../standard-library/iostream-programming.md)\
[iostreams 约定](../standard-library/iostreams-conventions.md)
