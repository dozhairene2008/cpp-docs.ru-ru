---
title: Ошибка компилятора C2385
ms.date: 11/04/2016
f1_keywords:
- C2385
helpviewer_keywords:
- C2385
ms.assetid: 6d3dd1f2-e56d-49d7-865c-6a9acdb17417
ms.openlocfilehash: 1247e4da05d65677f602a82591efd3e0c0c374e0
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2019
ms.locfileid: "74745260"
---
# <a name="compiler-error-c2385"></a>Ошибка компилятора C2385

неоднозначный доступ "member"

Элемент может быть производным от более чем одного объекта (он наследуется более чем одним объектом).  Чтобы устранить эту ошибку,

- Сделайте член однозначным, добавив приведение.

- Переименуйте неоднозначные элементы в базовых классах.

## <a name="example"></a>Пример

Следующий пример приводит к возникновению ошибки C2385.

```cpp
// C2385.cpp
// C2385 expected
#include <stdio.h>

struct A
{
    void x(int i)
    {
        printf_s("\nIn A::x");
    }
};

struct B
{
    void x(char c)
    {
        printf_s("\nIn B::x");
    }
};

// Delete the following line to resolve.
struct C : A, B {}

// Uncomment the following 4 lines to resolve.
// struct C : A, B
// {
//     using B::x;
//     using A::x;
// };

int main()
{
    C aC;
    aC.x(100);
    aC.x('c');
}

struct C : A, B
{
    using B::x;
    using A::x;
};
```
