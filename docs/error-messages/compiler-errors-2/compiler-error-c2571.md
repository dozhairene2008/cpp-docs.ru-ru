---
title: Ошибка компилятора C2571
ms.date: 11/04/2016
f1_keywords:
- C2571
helpviewer_keywords:
- C2571
ms.assetid: c6522616-dee9-4d7d-9bf8-30a7e1deaadf
ms.openlocfilehash: 7bd87f0732e1a632b8c86cc57fab1a0f104b2c77
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2019
ms.locfileid: "74755503"
---
# <a name="compiler-error-c2571"></a>Ошибка компилятора C2571

"функция": виртуальная функция не может находиться в Union "Union"

Объединение объявляется с помощью виртуальной функции. Виртуальную функцию можно объявить только в классе или структуре.  Возможные решения:

1. Измените объединение на класс или структуру.

1. Сделайте функцию невиртуальной.

Следующий пример приводит к возникновению ошибки C2571:

```cpp
// C2571.cpp
// compile with: /c
union A {
   virtual void func1();   // C2571
   void func2();   // OK
};
```
