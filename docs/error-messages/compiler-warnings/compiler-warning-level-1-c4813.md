---
title: Предупреждение компилятора (уровень 1) C4813
ms.date: 11/04/2016
f1_keywords:
- C4813
helpviewer_keywords:
- C4813
ms.assetid: c30bf877-ab04-4fe4-897e-8162092426f0
ms.openlocfilehash: 517349dacc9081d2d34a861bb55ba734089124e2
ms.sourcegitcommit: 458dcc794e3841919c01a3a5ff6b9a3767f8861b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/13/2019
ms.locfileid: "74051262"
---
# <a name="compiler-warning-level-1-c4813"></a>Предупреждение компилятора (уровень 1) C4813

"функция": дружественная функция локального класса должна быть предварительно объявлена

Дружественная функция внутреннего класса не объявлена во внешнем классе.

В следующем примере возникает ошибка C4813:

```cpp
// C4813.cpp
// compile with: /W1 /LD
void MyClass()
{
   // void func();
   class InnerClass
   {
      friend void func();   // C4813 uncomment declaration above
   };
}
```