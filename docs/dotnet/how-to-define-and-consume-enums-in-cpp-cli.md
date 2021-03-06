---
title: Практическое руководство. Определение и использование перечислений в C++/CLI
ms.date: 11/04/2016
helpviewer_keywords:
- enum class, specifying underlying types
ms.assetid: df8f2b91-b9d2-4fab-9be4-b1d58b8bc570
ms.openlocfilehash: 68f8e113f6199d3b320bc6d241ee3396d2b70a1a
ms.sourcegitcommit: 573b36b52b0de7be5cae309d45b68ac7ecf9a6d8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2019
ms.locfileid: "79544985"
---
# <a name="how-to-define-and-consume-enums-in-ccli"></a>Практическое руководство. Определение и использование перечислений в C++/CLI

В этом разделе обсуждаются перечисления в C++/CLI.

## <a name="specifying-the-underlying-type-of-an-enum"></a>Указание базового типа перечисления

По умолчанию базовым типом перечисления является `int`.  Однако можно указать тип для подписанных или неподписанных форм `int`, `short`, `long`, `__int32`или `__int64`.  Также можно использовать `char`.

```cpp
// mcppv2_enum_3.cpp
// compile with: /clr
public enum class day_char : char {sun, mon, tue, wed, thu, fri, sat};

int main() {
   // fully qualified names, enumerator not injected into scope
   day_char d = day_char::sun, e = day_char::mon;
   System::Console::WriteLine(d);
   char f = (char)d;
   System::Console::WriteLine(f);
   f = (char)e;
   System::Console::WriteLine(f);
   e = day_char::tue;
   f = (char)e;
   System::Console::WriteLine(f);
}
```

**Выходные данные**

```Output
sun
0
1
2
```

## <a name="how-to-convert-between-managed-and-standard-enumerations"></a>Преобразование между управляемыми и стандартными перечислениями

Нет стандартного преобразования между перечислением и целочисленным типом; требуется приведение.

```cpp
// mcppv2_enum_4.cpp
// compile with: /clr
enum class day {sun, mon, tue, wed, thu, fri, sat};
enum {sun, mon, tue, wed, thu, fri, sat} day2; // unnamed std enum

int main() {
   day a = day::sun;
   day2 = sun;
   if ((int)a == day2)
   // or...
   // if (a == (day)day2)
      System::Console::WriteLine("a and day2 are the same");
   else
      System::Console::WriteLine("a and day2 are not the same");
}
```

**Выходные данные**

```Output
a and day2 are the same
```

## <a name="operators-and-enums"></a>Операторы и перечисления

Для перечислений в C++/CLI допустимы следующие операторы:

|Оператор|
|--------------|
|= =! = \< > \<= > =|
|+ -|
|&#124; ^ & ~|
|++ --|
|sizeof|

Операторы &#124; ^ & ~ + + — определяются только для перечислений с целочисленными базовыми типами, не включая bool.  Оба операнда должны иметь тип перечисления.

Компилятор не выполняет статическую или динамическую проверку результата операции перечисления. операция может привести к тому, что значение не находится в диапазоне допустимых перечислителей перечисления.

> [!NOTE]
>  В c++ 11 введены типы классов перечисления в неуправляемом коде, которые значительно отличаются от управляемых классов C++перечисления в/CLI. В частности, тип класса Enum C++ 11 не поддерживает те же операторы, что и тип управляемого класса Enum в C++/CLI, а C++исходный код/CLI должен предоставлять описатель доступности в объявлениях управляемых классов перечисления, чтобы отличать их от объявлений классов перечисления неуправляемого кода (c++ 11). Дополнительные сведения о классах Enum в C++/CLI, C++/CX и c++ 11 см. в разделе [Класс Enum](../extensions/enum-class-cpp-component-extensions.md).

```cpp
// mcppv2_enum_5.cpp
// compile with: /clr
private enum class E { a, b } e, mask;
int main() {
   if ( e & mask )   // C2451 no E->bool conversion
      ;

   if ( ( e & mask ) != 0 )   // C3063 no operator!= (E, int)
      ;

   if ( ( e & mask ) != E() )   // OK
      ;
}
```

```cpp
// mcppv2_enum_6.cpp
// compile with: /clr
private enum class day : int {sun, mon};
enum : bool {sun = true, mon = false} day2;

int main() {
   day a = day::sun, b = day::mon;
   day2 = sun;

   System::Console::WriteLine(sizeof(a));
   System::Console::WriteLine(sizeof(day2));
   a++;
   System::Console::WriteLine(a == b);
}
```

**Выходные данные**

```Output
4
1
True
```

## <a name="see-also"></a>См. также:

[Класс перечисления](../extensions/enum-class-cpp-component-extensions.md)
