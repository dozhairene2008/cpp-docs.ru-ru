---
title: Ошибка компилятора C2486
ms.date: 11/04/2016
f1_keywords:
- C2486
helpviewer_keywords:
- C2486
ms.assetid: 436da349-6461-4e32-bfca-4f3e620108e2
ms.openlocfilehash: 75705bd8ecc850839e22fccbed1abf08687b3823
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2019
ms.locfileid: "74743514"
---
# <a name="compiler-error-c2486"></a>Ошибка компилятора C2486

"__LOCAL_SIZE" допускается только в функции с атрибутом "naked"

В встроенных функциях ассемблера имя `__LOCAL_SIZE` зарезервировано для функций, объявленных с атрибутом [naked](../../cpp/naked-cpp.md) .

Следующий пример приводит к возникновению ошибки C2486:

```cpp
// C2486.cpp
// processor: x86
void __declspec(naked) f1() {
   __asm {
      mov   eax,   __LOCAL_SIZE
   }
}
void f2() {
   __asm {
      mov   eax,   __LOCAL_SIZE   // C2486
   }
}
```
