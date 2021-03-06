---
title: Предупреждение компилятора (уровень 4) C4437
ms.date: 11/04/2016
f1_keywords:
- C4437
helpviewer_keywords:
- C4437
ms.assetid: dc07e350-20eb-474c-a7ad-f841ae7ec339
ms.openlocfilehash: 6cd50d5c4d79b82c135ab4e84ec390dee9e906ef
ms.sourcegitcommit: 8762a3f9b5476b4dee03f0ee8064ea606550986e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/04/2019
ms.locfileid: "74810652"
---
# <a name="compiler-warning-level-4-c4437"></a>Предупреждение компилятора (уровень 4) C4437

dynamic_cast из виртуального базового "Class1" в "class2" может произойти сбой в некоторых контекстах, компилируемых с помощью/vd2, или определите "class2" с #pragma vtordisp (2) в силе

Это предупреждение отключено по умолчанию. Подробнее: [Выключенные по умолчанию предупреждения компилятора](../../preprocessor/compiler-warnings-that-are-off-by-default.md) .

Компилятор обнаружил операцию `dynamic_cast` со следующими характеристиками.

- Приведение является указателем базового класса на указатель производного класса.

- Производный класс виртуально наследует базовый класс.

- Производный класс не имеет поля `vtordisp` для виртуальной базы.

- Приведение не найдено в конструкторе или деструкторе производного класса или в каком-либо классе, который в дальнейшем наследует от производного класса (в противном случае будет выдана предупреждение компилятора C4436).

Предупреждение означает, что `dynamic_cast` может работать неправильно, если он работает на частично сконструированном объекте.  Такая ситуация возникает, когда включающая функция вызывается из конструктора или деструктора класса, который наследует производный класс с именем в предупреждении.  Если производный класс с именем в предупреждении не является более подрожденным, или включающая функция не вызывается во время создания или уничтожения объекта, это предупреждение можно пропустить.

## <a name="example"></a>Пример

В следующем примере создается C4437 и демонстрируется ошибка создания кода, которая возникает из поля Missing `vtordisp`.

```cpp
// C4437.cpp
// To see the warning and runtime assert, compile with: /W4
// To eliminate the warning and assert, compile with: /W4 /vd2
//       or compile with: /W4 /DFIX
#pragma warning(default : 4437)
#include <cassert>

struct A
{
public:
    virtual ~A() {}
};

#if defined(FIX)
#pragma vtordisp(push, 2)
#endif
struct B : virtual A
{
    B()
    {
        func();
    }

    void func()
    {
        A* a = static_cast<A*>(this);
        B* b = dynamic_cast<B*>(a);     // C4437
        assert(this == b);              // assert unless compiled with /vd2
    }
};
#if defined(FIX)
#pragma vtordisp(pop)
#endif

struct C : B
{
    int i;
};

int main()
{
    C c;
}
```

## <a name="see-also"></a>См. также:

[Оператор dynamic_cast](../../cpp/dynamic-cast-operator.md)<br/>
[vtordisp](../../preprocessor/vtordisp.md)<br/>
[Предупреждение компилятора (уровень 1) C4436](../../error-messages/compiler-warnings/compiler-warning-level-1-c4436.md)