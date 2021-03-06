---
title: Класс ostream_iterator
ms.date: 11/04/2016
f1_keywords:
- iterator/std::ostream_iterator
- iterator/std::ostream_iterator::char_type
- iterator/std::ostream_iterator::ostream_type
- iterator/std::ostream_iterator::traits_type
helpviewer_keywords:
- std::ostream_iterator [C++]
- std::ostream_iterator [C++], char_type
- std::ostream_iterator [C++], ostream_type
- std::ostream_iterator [C++], traits_type
ms.assetid: 24d842d3-9f45-4bf6-a697-62f5968f5a03
ms.openlocfilehash: 63bf0a9e3f458b35421ca53d32a2d6be4b701e58
ms.sourcegitcommit: 590e488e51389066a4da4aa06d32d4c362c23393
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/21/2019
ms.locfileid: "72687240"
---
# <a name="ostream_iterator-class"></a>Класс ostream_iterator

Шаблон класса ostream_iterator описывает объект итератора вывода, который записывает последовательные элементы в выходной поток с `operator <<` извлечения.

## <a name="syntax"></a>Синтаксис

```cpp
template <class Type class CharType = char class Traits = char_traits <CharType>>
class ostream_iterator
```

### <a name="parameters"></a>Параметры

*Тип* \
Тип объекта, который необходимо вставить в поток вывода.

*CharType* \
Тип, представляющий шрифт символа для `ostream_iterator`. Этот аргумент является необязательным, и значение по умолчанию — **char**.

*Признаки* \
Тип, представляющий шрифт символа для `ostream_iterator`. Этот аргумент является необязательным, значение по умолчанию — `char_traits`\< *CharType>.*

Класс ostream_iterator должен удовлетворять требованиям для итератора вывода. Алгоритмы можно записывать непосредственно в потоки вывода с помощью `ostream_iterator`.

### <a name="constructors"></a>Конструкторы

|Конструктор|Описание|
|-|-|
|[ostream_iterator](#ostream_iterator)|Создает `ostream_iterator`, инициализированный и разделенный для записи в поток вывода.|

### <a name="typedefs"></a>Typedefs

|Имя типа|Описание|
|-|-|
|[char_type](#char_type)|Тип, обеспечивающий тип символа для `ostream_iterator`.|
|[ostream_type](#ostream_type)|Тип, обеспечивающий тип потока для `ostream_iterator`.|
|[traits_type](#traits_type)|Тип, обеспечивающий тип признаков символа для `ostream_iterator`.|

### <a name="operators"></a>Операторы

|оператора|Описание|
|-|-|
|[operator*](#op_star)|Оператор разыменования, используемый для реализации выражения итератора вывода \* `i`  =  `x`.|
|[оператор++](#op_add_add)|Нефункциональный оператор инкремента, возвращающий `ostream_iterator`, обращающийся к тому же объекту, к которому он обращался до вызова операции.|
|[оператор=](#op_eq)|Оператор присваивания, используемый для реализации выражения итератора вывода \* `i`  =  `x` для записи в поток вывода.|

## <a name="requirements"></a>Требования

**Заголовок:** \<iterator>

**Пространство имен:** std

## <a name="char_type"></a>  ostream_iterator::char_type

Тип, обеспечивающий тип символа для итератора.

```cpp
typedef CharType char_type;
```

### <a name="remarks"></a>Заметки

Этот тип является синонимом для параметра шаблона `CharType`.

### <a name="example"></a>Пример

```cpp
// ostream_iterator_char_type.cpp
// compile with: /EHsc
#include <iterator>
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;

   typedef ostream_iterator<int>::char_type CHT1;
   typedef ostream_iterator<int>::traits_type CHTR1;

   // ostream_iterator for stream cout
   // with new line delimiter:
    ostream_iterator<int, CHT1, CHTR1> intOut ( cout , "\n" );

   // Standard iterator interface for writing
   // elements to the output stream:
   cout << "The integers written to the output stream\n"
        << "by intOut are:" << endl;
*intOut = 10;
*intOut = 20;
*intOut = 30;
}
/* Output:
The integers written to the output stream
by intOut are:
10
20
30
*/
```

## <a name="op_star"></a>  ostream_iterator::operator*

Оператор разыменования, используемый для реализации выражения итератора вывода \* *ii* = *x*.

```cpp
ostream_iterator<Type, CharType, Traits>& operator*();
```

### <a name="return-value"></a>Возвращаемое значение

Ссылка на `ostream_iterator`.

### <a name="remarks"></a>Заметки

Требования для итератора вывода, которым должен удовлетворять `ostream_iterator`, требуют только допустимости выражения \* *ii* = *t* и сами по себе ничего не говорят об **операторе** или о `operator=`. Оператор-член в этой реализации возвращает **\*this**.

### <a name="example"></a>Пример

```cpp
// ostream_iterator_op_deref.cpp
// compile with: /EHsc
#include <iterator>
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;

   // ostream_iterator for stream cout
   // with new line delimiter
   ostream_iterator<int> intOut ( cout , "\n" );

   // Standard iterator interface for writing
   // elements to the output stream
   cout << "Elements written to output stream:" << endl;
*intOut = 10;
   intOut++;      // No effect on iterator position
*intOut = 20;
*intOut = 30;
}
/* Output:
Elements written to output stream:
10
20
30
*/
```

## <a name="op_add_add"></a>  ostream_iterator::operator++

Нефункциональный оператор инкремента, возвращающий `ostream_iterator`, обращающийся к тому же объекту, к которому он обращался до вызова операции.

```cpp
ostream_iterator<Type, CharType, Traits>& operator++();
ostream_iterator<Type, CharType, Traits> operator++(int);
```

### <a name="return-value"></a>Возвращаемое значение

Ссылка на `ostream_iterator`.

### <a name="remarks"></a>Заметки

Оба эти оператора-члена возвращают **\*this**.

### <a name="example"></a>Пример

```cpp
// ostream_iterator_op_incr.cpp
// compile with: /EHsc
#include <iterator>
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;

   // ostream_iterator for stream cout
   // with new line delimiter
   ostream_iterator<int> intOut ( cout , "\n" );

   // standard iterator interface for writing
   // elements to the output stream
   cout << "Elements written to output stream:" << endl;
*intOut = 10;
   intOut++;      // No effect on iterator position
*intOut = 20;
*intOut = 30;
}
/* Output:
Elements written to output stream:
10
20
30
*/
```

## <a name="op_eq"></a>  ostream_iterator::operator=

Оператор присваивания, используемый для реализации выражения output_iterator \* `i`  =  `x` для записи в поток вывода.

```cpp
ostream_iterator<Type, CharType, Traits>& operator=(const Type& val);
```

### <a name="parameters"></a>Параметры

*val* \
Значение объекта типа `Type`, который нужно вставить в поток вывода.

### <a name="return-value"></a>Возвращаемое значение

Оператор вставляет значение *Val* в поток вывода, связанный с объектом, за которым следует разделитель, указанный в [конструкторе ostream_iterator](#ostream_iterator) (если он есть), а затем возвращается ссылка на `ostream_iterator`.

### <a name="remarks"></a>Заметки

Требования для итератора вывода, которым должен удовлетворять `ostream_iterator`, должны содержать только выражение \* `ii`  =  `t` быть допустимым и не говорит об операторе или операторе. Этот оператор-член возвращает `*this`.

### <a name="example"></a>Пример

```cpp
// ostream_iterator_op_assign.cpp
// compile with: /EHsc
#include <iterator>
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;

   // ostream_iterator for stream cout
   // with new line delimiter
   ostream_iterator<int> intOut ( cout , "\n" );

   // Standard iterator interface for writing
   // elements to the output stream
   cout << "Elements written to output stream:" << endl;
*intOut = 10;
   intOut++;      // No effect on iterator position
*intOut = 20;
*intOut = 30;
}
/* Output:
Elements written to output stream:
10
20
30
*/
```

## <a name="ostream_iterator"></a>  ostream_iterator::ostream_iterator

Создает `ostream_iterator`, инициализированный и разделенный для записи в поток вывода.

```cpp
ostream_iterator(
    ostream_type& _Ostr);

ostream_iterator(
    ostream_type& _Ostr,
    const CharType* _Delimiter);
```

### <a name="parameters"></a>Параметры

*_Ostr* \
Поток вывода типа [ostream_iterator::ostream_type](#ostream_type) для итерации по нему.

*_Delimiter* \
Разделитель, который вставляется в поток вывода между значениями.

### <a name="remarks"></a>Заметки

Первый конструктор инициализирует указатель потока вывода значением `&_Ostr`. Указатель на строку разделителя обозначает пустую строку.

Второй конструктор инициализирует указатель потока вывода с `&_Ostr` и указателем строки разделителя с *_Delimiter*.

### <a name="example"></a>Пример

```cpp
// ostream_iterator_ostream_iterator.cpp
// compile with: /EHsc
#include <iterator>
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;

   // ostream_iterator for stream cout
   ostream_iterator<int> intOut ( cout , "\n" );
*intOut = 10;
   intOut++;
*intOut = 20;
   intOut++;

   int i;
   vector<int> vec;
   for ( i = 1 ; i < 7 ; ++i )
   {
      vec.push_back (  i );
   }

   // Write elements to standard output stream
   cout << "Elements output without delimiter: ";
   copy ( vec.begin ( ), vec.end ( ),
          ostream_iterator<int> ( cout ) );
   cout << endl;

   // Write elements with delimiter " : " to output stream
   cout << "Elements output with delimiter: ";
   copy ( vec.begin ( ), vec.end ( ),
          ostream_iterator<int> ( cout, " : " ) );
   cout << endl;
}
/* Output:
10
20
Elements output without delimiter: 123456
Elements output with delimiter: 1 : 2 : 3 : 4 : 5 : 6 :
*/
```

## <a name="ostream_type"></a>  ostream_iterator::ostream_type

Тип, обеспечивающий тип потока для итератора.

```cpp
typedef basic_ostream<CharType, Traits> ostream_type;
```

### <a name="remarks"></a>Заметки

Тип является синонимом [basic_ostream](../standard-library/basic-ostream-class.md)< `CharType`, `Traits`>, класса потока в иерархии iostream, определяющего объекты, которые можно использовать для записи.

### <a name="example"></a>Пример

См. раздел [ostream_iterator](#ostream_iterator) с примером объявления и использования `ostream_type`.

## <a name="traits_type"></a>  ostream_iterator::traits_type

Тип, обеспечивающий тип признаков символа итератора.

```cpp
typedef Traits traits_type;
```

### <a name="remarks"></a>Заметки

Этот тип является синонимом для параметра шаблона `Traits`.

### <a name="example"></a>Пример

```cpp
// ostream_iterator_traits_type.cpp
// compile with: /EHsc
#include <iterator>
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;

   // The following not OK, but are just the default values:
   typedef ostream_iterator<int>::char_type CHT1;
   typedef ostream_iterator<int>::traits_type CHTR1;

   // ostream_iterator for stream cout
   // with new line delimiter:
    ostream_iterator<int, CHT1, CHTR1> intOut ( cout , "\n" );

   // Standard iterator interface for writing
   // elements to the output stream:
   cout << "The integers written to output stream\n"
        << "by intOut are:" << endl;
*intOut = 1;
*intOut = 10;
*intOut = 100;
}
/* Output:
The integers written to output stream
by intOut are:
1
10
100
*/
```

## <a name="see-also"></a>См. также

[\<iterator>](../standard-library/iterator.md)\
[Потокобезопасность в стандартной библиотеке C++](../standard-library/thread-safety-in-the-cpp-standard-library.md)\
[Справочник по стандартной библиотеке C++](../standard-library/cpp-standard-library-reference.md)
