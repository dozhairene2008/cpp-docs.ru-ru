---
title: Ошибка компилятора C3056
ms.date: 11/04/2016
f1_keywords:
- C3056
helpviewer_keywords:
- C3056
ms.assetid: 9500173d-870b-49b3-8e88-0ee93586d19a
ms.openlocfilehash: 97a403420e5923f23f804eeaff33af1698ff6a53
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2019
ms.locfileid: "74761160"
---
# <a name="compiler-error-c3056"></a>Ошибка компилятора C3056

"символ": символ не находится в одной области с директивой threadprivate

Символ, используемый в предложении [threadprivate](../../parallel/openmp/reference/threadprivate.md) , должен находиться в той же области, что и предложение `threadprivate` .

В следующем примере возникает ошибка C3056.

```cpp
// C3056.cpp
// compile with: /openmp
int x, y;
void test() {
   #pragma omp threadprivate(x, y)   // C3056
   #pragma omp parallel copyin(x, y)
   {
      x = y;
   }
}
```

Возможное решение

```cpp
// C3056b.cpp
// compile with: /openmp /LD
int x, y;
#pragma omp threadprivate(x, y)
void test() {
   #pragma omp parallel copyin(x, y)
   {
      x = y;
   }
}
```
