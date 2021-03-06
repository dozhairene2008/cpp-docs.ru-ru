---
title: Шаблоны (C++)
ms.date: 12/27/2019
f1_keywords:
- template_cpp
helpviewer_keywords:
- templates, C++
- templates [C++]
ms.assetid: 90fcc14a-2092-47af-9d2e-dba26d25b872
ms.openlocfilehash: 36ada3cc3b933e99e9b29b3b58463f6bc526fc7d
ms.sourcegitcommit: 00f50ff242031d6069aa63c81bc013e432cae0cd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/30/2019
ms.locfileid: "75546410"
---
# <a name="templates-c"></a>Шаблоны (C++)

Шаблоны служат основанием для универсального программирования C++в. В качестве строго типизированного языка C++ требует, чтобы все переменные имели конкретный тип, либо явно объявленный программистом, либо выведенный компилятором. Однако многие структуры данных и алгоритмы выглядят одинаково независимо от типа, на котором они работают. Шаблоны позволяют определить операции класса или функции и предоставить пользователю указание конкретных типов, с которыми должны работать эти операции.

## <a name="defining-and-using-templates"></a>Определение и использование шаблонов

Шаблон — это конструкция, которая создает обычный тип или функцию во время компиляции на основе аргументов, предоставленных пользователем для параметров шаблона. Например, можно определить шаблон функции следующим образом:

```cpp
template <typename T>
T minimum(const T& lhs, const T& rhs)
{
    return lhs < rhs ? lhs : rhs;
}
```

Приведенный выше код описывает шаблон для универсальной функции с одним параметром типа *T*, возвращаемое значение и параметры вызова (LHS и RHS) всех этих типов. Вы можете присвоить параметру типа любое имя, но, по правилам, наиболее часто используются буквы в одном верхнем регистре. *T* является параметром шаблона; ключевое слово **TypeName** говорит о том, что этот параметр является заполнителем для типа. При вызове функции компилятор заменит каждый экземпляр `T` конкретным аргументом типа, который либо задается пользователем, либо выведенным компилятором. Процесс, в котором компилятор создает класс или функцию из шаблона, называется *созданием экземпляра шаблона*. `minimum<int>` является экземпляром `minimum<T>`шаблона.

В других случаях пользователь может объявить экземпляр шаблона, специализированный для типа int. Предположим, что get_a () и get_b () — это функции, возвращающие int:

```cpp
int a = get_a();
int b = get_b();
int i = minimum<int>(a, b);
```

Тем не менее, поскольку это шаблон функции и компилятор может вывести тип `T` из аргументов *a* и *b*, его можно вызвать так же, как и обычной функции:

```cpp
int i = minimum(a, b);
```

Когда компилятор встречает последнюю инструкцию, он создает новую функцию, в которой каждое вхождение *T* в шаблоне заменяется на **int**:

```cpp
int minimum(const int& lhs, const int& rhs)
{
    return lhs < rhs ? lhs : rhs;
}
```

Правила, определяющие, как компилятор выполняет выведение типов в шаблонах функций, основаны на правилах для обычных функций. Дополнительные сведения см. в разделе [разрешение перегрузки вызовов шаблона функции](../cpp/overload-resolution-of-function-template-calls.md).

## <a id="type_parameters"></a>Параметры типа

В приведенном выше шаблоне `minimum` Обратите внимание на то, что параметр типа *t* не определен каким-либо образом, пока он не будет использован в параметрах вызова функции, где добавляются квалификаторы Const и Reference.

Практически не существует ограничения на количество параметров типа. Несколько параметров разделяются запятыми:

```cpp
template <typename T, typename U, typename V> class Foo{};
```

Ключевое слово **Class** эквивалентно **TypeName** в этом контексте. Предыдущий пример можно выразить следующим образом:

```cpp
template <class T, class U, class V> class Foo{};
```

С помощью оператора многоточия (...) можно определить шаблон, принимающий произвольное число из нуля или более параметров типа:

```cpp
template<typename... Arguments> class vtclass;

vtclass< > vtinstance1;
vtclass<int> vtinstance2;
vtclass<float, bool> vtinstance3;
```

В качестве аргумента типа можно использовать любой встроенный или определяемый пользователем тип. Например, можно использовать [std:: Vector](../standard-library/vector-class.md) в стандартной библиотеке для хранения переменных типа **int**, **double**, [std:: String](../standard-library/basic-string-class.md), `MyClass`, **const** `MyClass`*, `MyClass&`и т. д. Основным ограничением при использовании шаблонов является то, что аргумент типа должен поддерживать любые операции, применяемые к параметрам типа. Например, если мы вызываем `minimum` с помощью `MyClass`, как в следующем примере:

```cpp
class MyClass
{
public:
    int num;
    std::wstring description;
};

int main()
{
    MyClass mc1 {1, L"hello"};
    MyClass mc2 {2, L"goodbye"};
    auto result = minimum(mc1, mc2); // Error! C2678
}
```

Будет сформирована ошибка компилятора, так как `MyClass` не предоставляет перегрузку для оператора **<** .

Нет необходимости в том, что аргументы типа для любого конкретного шаблона принадлежат к одной и той же иерархии объектов, хотя можно определить шаблон, обеспечивающий такое ограничение. Объектно-ориентированные методики можно сочетать с шаблонами. Например, можно сохранить производный * в векторной\<базового\*>.    Обратите внимание, что аргументы должны быть указателями

```cpp
vector<MyClass*> vec;
   MyDerived d(3, L"back again", time(0));
   vec.push_back(&d);

   // or more realistically:
   vector<shared_ptr<MyClass>> vec2;
   vec2.push_back(make_shared<MyDerived>());
```

Основные требования, которые `std::vector` и другие контейнеры стандартной библиотеки накладываются на элементы `T`, `T` быть копируемыми и конструируемым.

## <a name="non-type-parameters"></a>Параметры, не являющиеся типами

В отличие от универсальных типов на других языках C# , таких как C++ и Java, шаблоны поддерживают *Параметры, не являющиеся типами*, также называемые параметрами значений. Например, можно предоставить постоянное целочисленное значение, чтобы указать длину массива, как в этом примере, подобно классу [std:: Array](../standard-library/array-class-stl.md) в стандартной библиотеке:

```cpp
template<typename T, size_t L>
class MyArray
{
    T arr[L];
public:
    MyArray() { ... }
};
```

Обратите внимание на синтаксис в объявлении шаблона. Значение `size_t` передается в качестве аргумента шаблона во время компиляции и должно быть **константой** или выражением **constexpr** . Используйте его следующим образом:

```cpp
MyArray<MyClass*, 10> arr;
```

Другие виды значений, включая указатели и ссылки, могут передаваться как параметры, не являющиеся типами. Например, можно передать указатель на функцию или объект функции для настройки некоторой операции внутри кода шаблона.

### <a name="type-deduction-for-non-type-template-parameters"></a>Выведение типа для параметров шаблона, не являющихся типами

В Visual Studio 2017 и более поздних версиях в **/std: режим c++ 17** компилятор выводит тип аргумента шаблона, не являющегося типом, который объявлен с **Auto**:

```cpp
template <auto x> constexpr auto constant = x;

auto v1 = constant<5>;      // v1 == 5, decltype(v1) is int
auto v2 = constant<true>;   // v2 == true, decltype(v2) is bool
auto v3 = constant<'a'>;    // v3 == 'a', decltype(v3) is char
```

## <a id="template_parameters"></a>Шаблоны в качестве параметров шаблона

Шаблон может быть параметром шаблона. В этом примере MyClass2 имеет два параметра шаблона: параметр typeName *T* и параметр шаблона *arr*:

```cpp
template<typename T, template<typename U, int I> class Arr>
class MyClass2
{
    T t; //OK
    Arr<T, 10> a;
    U u; //Error. U not in scope
};
```

Поскольку сам параметр *arr* не имеет тела, его имена параметров не требуются. На самом деле, является ошибкой ссылаться на имена TypeName или параметров класса *arr*в теле `MyClass2`. По этой причине имена параметров типа *arr*можно опустить, как показано в следующем примере:

```cpp
template<typename T, template<typename, int> class Arr>
class MyClass2
{
    T t; //OK
    Arr<T, 10> a;
};
```

## <a name="default-template-arguments"></a>Аргументы шаблона по умолчанию

Шаблоны классов и функций могут иметь аргументы по умолчанию. Если шаблон имеет аргумент по умолчанию, его можно оставить неопределенным при его использовании. Например, шаблон std:: Vector имеет аргумент по умолчанию для распределителя:

```cpp
template <class T, class Allocator = allocator<T>> class vector;
```

В большинстве случаев класс по умолчанию std:: распределитель приемлем, поэтому вы используете такой же вектор:

```cpp
vector<int> myInts;
```

Но при необходимости можно указать пользовательский распределитель следующим образом:

```cpp
vector<int, MyAllocator> ints;
```

При наличии нескольких аргументов шаблона все аргументы после первого аргумента по умолчанию должны иметь аргументы по умолчанию.

При использовании шаблона, параметры которого заданы по умолчанию, используйте пустые угловые скобки:

```cpp
template<typename A = int, typename B = double>
class Bar
{
    //...
};
...
int main()
{
    Bar<> bar; // use all default type arguments
}
```

## <a name="template-specialization"></a>Специализация шаблонов

В некоторых случаях невозможно или нежелательно, чтобы шаблон определял точно такой же код для любого типа. Например, может потребоваться определить путь кода, который будет выполняться, только если аргумент типа является указателем или std:: wstring или типом, производным от конкретного базового класса.  В таких случаях можно определить *специализацию* шаблона для этого конкретного типа. Когда пользователь создает экземпляр шаблона с этим типом, компилятор использует специализацию для создания класса, а для всех остальных типов компилятор выбирает более общий шаблон. Специализации, в которых все параметры являются специализированными, являются *полными специализациями*. Если только некоторые из параметров являются специализированными, это называется *частичной специализацией*.

```cpp
template <typename K, typename V>
class MyMap{/*...*/};

// partial specialization for string keys
template<typename V>
class MyMap<string, V> {/*...*/};
...
MyMap<int, MyClass> classes; // uses original template
MyMap<string, MyClass> classes2; // uses the partial specialization
```

Шаблон может иметь любое количество специализаций, если каждый специализированный параметр типа уникален. Только шаблоны классов могут быть частично специализированными. Все полные и частичные специализации шаблона должны быть объявлены в том же пространстве имен, что и исходный шаблон.

Дополнительные сведения см. в разделе [специализация шаблонов](../cpp/template-specialization-cpp.md).