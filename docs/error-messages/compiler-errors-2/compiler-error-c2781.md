---
title: Ошибка компилятора C2781
ms.date: 11/04/2016
f1_keywords:
- C2781
helpviewer_keywords:
- C2781
ms.assetid: f29b9963-f55b-427c-8db6-50f37713df5a
ms.openlocfilehash: ff5d3d322118d9e3e229b9302e57dc1075f80b9b
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2019
ms.locfileid: "74739926"
---
# <a name="compiler-error-c2781"></a>Ошибка компилятора C2781

"объявление": при указании аргумента "значение1" должно быть указано "значение2".

Шаблон функции с переменным списком параметров содержит слишком мало аргументов.

Следующий пример приводит к возникновению ошибки C2781:

```cpp
// C2781.cpp
template<typename T>
void f(T, T, ...){}

int main() {
   f(1);   // C2781

   // try the following line instead
   f(1,1);
}
```
