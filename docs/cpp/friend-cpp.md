---
title: friend (C++)
ms.date: 07/15/2019
f1_keywords:
- friend_cpp
helpviewer_keywords:
- member access, from friend functions
- friend classes [C++]
- friend keyword [C++]
ms.assetid: 8fe9ee55-d56f-40cd-9075-d9fb1375aff4
ms.openlocfilehash: 03b6cb7f856ec59c10f5e410c947f74d17ec4e46
ms.sourcegitcommit: fd466f2e14ad001f52f3dbe54f46d77be10f2d7b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/15/2019
ms.locfileid: "67894415"
---
# <a name="friend-c"></a>friend (C++)

В некоторых случаях удобнее для предоставления доступа на уровне члена к функциям, которые не являются членами класса или ко всем элементам в отдельном классе. Только реализатор класса может объявить, что является для него дружественным элементом. Функция или класс не могут объявить себя дружественным элементом для любого класса. В определении класса, используйте **friend** ключевое слово и имя функции не являющиеся членами или другой класс, чтобы предоставить им доступ к закрытым и защищенным членам класса. В определении шаблона параметр типа могут объявляться как дружественная.

## <a name="syntax"></a>Синтаксис

```
class friend F
friend F;
```

## <a name="friend-declarations"></a>Объявления дружественных элементов

При объявлении дружественной функции, которая не была объявлена ранее, эта функция экспортируется во включающую область вне класса.

Функции, объявленные в объявлении friend, обрабатываются так, как если бы они были объявлены с помощью **extern** ключевое слово. Дополнительные сведения см. в разделе [extern](extern-cpp.md).

Хотя функции с глобальной областью действия могут быть объявлены как дружественные до объявления своих прототипов, функции-члены не могут быть объявлены как дружественные функции до полного объявления их класса. В следующем коде показано, почему при этом возникает ошибка.

```cpp
class ForwardDeclared;   // Class name is known.
class HasFriends
{
    friend int ForwardDeclared::IsAFriend();   // C2039 error expected
};
```

В предыдущем примере в области действия вводится имя класса `ForwardDeclared`, но полное объявление — в частности, часть, в которой объявляется функция `IsAFriend`, — отсутствует. Таким образом **friend** объявление в классе `HasFriends` приводит к ошибке.

Начиная с версии C ++ 11, существует два вида объявления дружественного класса.

```cpp
friend class F;
friend F;
```

Первая форма появился новый класс F, если существующий класс с таким именем не найден в самой внутренней пространства имен. **C++11**: Вторая форма не вводит новый класс; он используется, если уже был объявлен класс и его следует использовать при объявлении параметра типа шаблон или определение типа как дружественная.

Используйте `class friend F` при ссылочного типа не еще была объявлена:

```cpp
namespace NS
{
    class M
    {
        class friend F;  // Introduces F but doesn't define it
    };
}
```

```cpp
namespace NS
{
    class M
    {
        friend F; // error C2433: 'NS::F': 'friend' not permitted on data declarations
    };
}
```

В следующем примере `friend F` ссылается на `F` классе, объявленном выходит за рамки NS.

```cpp
class F {};
namespace NS
{
    class M
    {
        friend F;  // OK
    };
}
```

Используйте `friend F` Чтобы объявить параметр шаблона, как дружественная:

```cpp
template <typename T>
class my_class
{
    friend T;
    //...
};
```

Используйте `friend F` для объявления typedef как дружественная:

```cpp
class Foo {};
typedef Foo F;

class G
{
    friend F; // OK
    friend class F // Error C2371 -- redefinition
};
```

Чтобы объявить два класса как дружественные друг другу, весь второй класс должен быть указан как дружественный для первого класса. Причина такого ограничения заключается в том, что компилятор получает достаточные сведения для объявления отдельных дружественных функций только в момент объявления второго класса.

> [!NOTE]
>  Хотя весь второй класс должен быть дружественным для первого класса, можно выбрать, какие функции первого класса будут дружественными для второго класса.

## <a name="friend-functions"></a>дружественные функции

Объект **friend** функция — это функция, которая не является членом класса, но имеет доступ к закрытым и защищенным членам класса. Дружественные функции не считаются членами класса; это обычные внешние функции с особыми правами доступа. Дружественные функции не входят в область видимости класса, и они не вызываются с помощью операторов выбора члена ( **.** и - **>** ) если они не являются членами другого класса. Объект **friend** функция объявляется в классе, который предоставляет доступ. **Friend** объявлении можно разместить в любом месте объявления класса. На него не влияют ключевые слова управления доступом.

В следующем примере показан класс `Point` и дружественная функция `ChangePrivate`. **Friend** функция имеет доступ к закрытому члену данных объекта `Point` который она получает в качестве параметра.

```cpp
// friend_functions.cpp
// compile with: /EHsc
#include <iostream>

using namespace std;
class Point
{
    friend void ChangePrivate( Point & );
public:
    Point( void ) : m_i(0) {}
    void PrintPrivate( void ){cout << m_i << endl; }

private:
    int m_i;
};

void ChangePrivate ( Point &i ) { i.m_i++; }

int main()
{
   Point sPoint;
   sPoint.PrintPrivate();
   ChangePrivate(sPoint);
   sPoint.PrintPrivate();
// Output: 0
           1
}
```

## <a name="class-members-as-friends"></a>Члены класса как дружественные элементы

Функции-члены класса могут быть объявлены в других классах как дружественные. Рассмотрим следующий пример.

```cpp
// classes_as_friends1.cpp
// compile with: /c
class B;

class A {
public:
   int Func1( B& b );

private:
   int Func2( B& b );
};

class B {
private:
   int _b;

   // A::Func1 is a friend function to class B
   // so A::Func1 has access to all members of B
   friend int A::Func1( B& );
};

int A::Func1( B& b ) { return b._b; }   // OK
int A::Func2( B& b ) { return b._b; }   // C2248
```

В предыдущем примере дружественный доступ к классу `A::Func1( B& )` предоставляется только функции `B`. Таким образом, доступ к закрытому члену `_b` правильности в `Func1` класса `A` , но не в `Func2`.

Класс `friend` — это класс, все функций-члены которого являются дружественными функциями класса, то есть функции-члены которого имеют доступ к закрытым и защищенным членам другого класса. Предположим, что в классе `friend` было следующее объявление `B`:

```cpp
friend class A;
```

В этом случае все функции-члены из класса `A` имели бы дружественный доступ к классу `B`. В следующем коде приведен пример дружественного класса.

```cpp
// classes_as_friends2.cpp
// compile with: /EHsc
#include <iostream>

using namespace std;
class YourClass {
friend class YourOtherClass;  // Declare a friend class
public:
   YourClass() : topSecret(0){}
   void printMember() { cout << topSecret << endl; }
private:
   int topSecret;
};

class YourOtherClass {
public:
   void change( YourClass& yc, int x ){yc.topSecret = x;}
};

int main() {
   YourClass yc1;
   YourOtherClass yoc1;
   yc1.printMember();
   yoc1.change( yc1, 5 );
   yc1.printMember();
}
```

Дружественные отношения не являются взаимными, если это не указано явным образом. В предыдущем примере функции-члены класса `YourClass` не имеют доступа к закрытым членам класса `YourOtherClass`.

Управляемый тип (в C++выполняет) не может иметь любой дружественные функции, дружественные классы или интерфейсы friend.

Дружественные отношения не наследуются; это означает, что классы, производные от `YourOtherClass`, не могут обращаться к закрытым членам класса `YourClass`. Дружественные отношения не являются переходящими, поэтому классы, дружественные классу `YourOtherClass`, не могут обращаться к закрытым членам класса `YourClass`.

На следующем рисунке показаны объявления 4 классов: `Base`, `Derived`, `aFriend` и `anotherFriend`. Только класс `aFriend` имеет прямой доступ к закрытым членам класса `Base` (и к любым возможным унаследованным членам класса `Base`).

![Последствия дружественных отношений](../cpp/media/vc38v41.gif "последствия дружественных отношений") <br/>
Последствия дружественных отношений

## <a name="inline-friend-definitions"></a>Встроенные определения дружественных элементов

Дружественные функции (учитывая тело функции) можно определить внутри объявления класса. Эти функции являются встраиваемыми, и как встраиваемые функции членов они ведут себя так, как если бы они были определены сразу после просмотра всех членов класса, но до закрытия области класса (конец объявления класса). Дружественные функции, определенные в объявлениях класса находятся в области включающего класса.

## <a name="see-also"></a>См. также

[Ключевые слова](../cpp/keywords-cpp.md)