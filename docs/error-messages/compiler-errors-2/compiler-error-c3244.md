---
title: Ошибка компилятора C3244
ms.date: 11/04/2016
f1_keywords:
- C3244
helpviewer_keywords:
- C3244
ms.assetid: dae6c49b-5212-4206-8f61-d4010c0b9969
ms.openlocfilehash: 11de2ac8a652687d9826319f13b7c531534d5fe3
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2019
ms.locfileid: "74754541"
---
# <a name="compiler-error-c3244"></a>Ошибка компилятора C3244

"метод": этот метод был создан "интерфейс", но не "интерфейс"

Вы попытались [явно переопределить](../../cpp/explicit-overrides-cpp.md) элемент, который не существует в указанном интерфейсе, но существует в другом базовом классе.

Следующий пример приводит к возникновению ошибки C3244:

```cpp
// C3244.cpp
#pragma warning(disable:4199)

__interface IX15A {
   void f();
};

__interface IX15B {
   void g();
};

class CX15 : public IX15A, public IX15B {
public:
   void IX15A::f();
   void IX15B::g();
};

void CX15::IX15A::g()   // C3244 occurs here
{
}
```
