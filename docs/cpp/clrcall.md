---
title: __clrcall
ms.date: 11/04/2016
f1_keywords:
- __clrcall_cpp
helpviewer_keywords:
- __clrcall keyword [C++]
ms.assetid: 92096695-683a-40ed-bf65-0c8443572152
ms.openlocfilehash: 6eb1a05eaf6669daa4cb7142ff16a57f7caf39cd
ms.sourcegitcommit: a6d63c07ab9ec251c48bc003ab2933cf01263f19
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2019
ms.locfileid: "74857610"
---
# <a name="__clrcall"></a>__clrcall

Указывает, что функцию можно вызвать только из управляемого кода.  Используйте **__clrcall** для всех виртуальных функций, которые будут вызываться только из управляемого кода. Однако это соглашение о вызовах невозможно использовать для функций, которые будут вызываться из машинного кода. Модификатор **__clrcall** зависит от корпорации Майкрософт.

Используйте **__clrcall** , чтобы повысить производительность при вызове из управляемой функции в виртуальную управляемую функцию или из управляемой функции в управляемую функцию через указатель.

Точки входа представляют собой отдельные функции, создаваемые компилятором. Если функция имеет машинные и управляемые точки входа, одна из них будет фактической функцией с реализацией функции. Другая функция будет отдельной функцией (преобразователем), которая вызывает фактическую функцию и позволяет среде CLR выполнять PInvoke. При пометке функции как **__clrcall**необходимо указать, что реализация функции должна быть MSIL и что собственная функция точки входа не будет создана.

При получении адреса собственной функции, если параметр **__clrcall** не указан, компилятор использует собственную точку входа. **__clrcall** указывает, что функция является управляемой, и нет необходимости выполнять переход от управляемого кода к машинному. В этом случае компилятор использует управляемую точку входа.

Если используется `/clr` (не `/clr:pure` или `/clr:safe`) и не используется **__clrcall** , то при получении адреса функции всегда возвращается адрес собственной функции точки входа. При использовании **__clrcall** собственная функция точки входа не создается, поэтому вы получаете адрес управляемой функции, а не функцию преобразователя точки входа. Дополнительные сведения см. в разделе [Двойное преобразователь](../dotnet/double-thunking-cpp.md). Параметры компилятора **/clr: pure** и **/clr: Сейф** являются устаревшими в Visual Studio 2015 и не поддерживаются в Visual Studio 2017.

[параметр/CLR (компиляция общеязыковой среды выполнения)](../build/reference/clr-common-language-runtime-compilation.md) подразумевает, что все функции и указатели функций **__clrcall** , и компилятор не позволит пометить функцию внутри компилируемого объекта как не **__clrcall**. При использовании **/clr: pure** **__clrcall** можно указывать только в указателях на функции и внешних объявлениях.

Вы можете напрямую вызывать функции **__clrcall** из существующего C++ кода, скомпилированного с помощью **/CLR** , если эта функция имеет реализацию MSIL. функции **__clrcall** не могут вызываться напрямую из функций, которые имеют встроенный ASM и вызывают интринисикс для конкретного процессора, например, даже если эти функции компилируются с `/clr`.

**__clrcall** указатели функций предназначены только для использования в домене приложения, в котором они были созданы.  Вместо того, чтобы передавать **__clrcall** указатели функций между доменами приложений, используйте <xref:System.CrossAppDomainDelegate>. Дополнительные сведения см. в разделе [домены приложений C++и визуальные элементы ](../dotnet/application-domains-and-visual-cpp.md).

## <a name="example"></a>Пример

Обратите внимание, что при объявлении функции с **__clrcall**при необходимости будет сформирован код. Например, при вызове функции.

```cpp
// clrcall2.cpp
// compile with: /clr
using namespace System;
int __clrcall Func1() {
   Console::WriteLine("in Func1");
   return 0;
}

// Func1 hasn't been used at this point (code has not been generated),
// so runtime returns the adddress of a stub to the function
int (__clrcall *pf)() = &Func1;

// code calls the function, code generated at difference address
int i = pf();   // comment this line and comparison will pass

int main() {
   if (&Func1 == pf)
      Console::WriteLine("&Func1 == pf, comparison succeeds");
   else
      Console::WriteLine("&Func1 != pf, comparison fails");

   // even though comparison fails, stub and function call are correct
   pf();
   Func1();
}
```

```Output
in Func1
&Func1 != pf, comparison fails
in Func1
in Func1
```

## <a name="example"></a>Пример

В следующем примере показано, что можно определить указатель функции, например объявить, что указатель функции будет вызываться только из управляемого кода. Это позволит компилятору непосредственно вызвать управляемую функцию и избежать машинной точки входа (проблема двойного преобразования).

```cpp
// clrcall3.cpp
// compile with: /clr
void Test() {
   System::Console::WriteLine("in Test");
}

int main() {
   void (*pTest)() = &Test;
   (*pTest)();

   void (__clrcall *pTest2)() = &Test;
   (*pTest2)();
}
```

## <a name="see-also"></a>См. также:

[Передача аргументов и соглашения об именовании](../cpp/argument-passing-and-naming-conventions.md)<br/>
[Ключевые слова](../cpp/keywords-cpp.md)
