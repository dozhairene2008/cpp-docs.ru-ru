---
title: Ошибка компилятора C2570
ms.date: 11/04/2016
f1_keywords:
- C2570
helpviewer_keywords:
- C2570
ms.assetid: d65d0b32-2fac-464a-bcdf-0ebcedf3bf32
ms.openlocfilehash: 6b9f94b1b17aad85aab37659565e6e0827b5a824
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2019
ms.locfileid: "74755516"
---
# <a name="compiler-error-c2570"></a>Ошибка компилятора C2570

"идентификатор": объединение не может иметь базовые классы

Объединение является производным от класса, структуры или объединения. Такое использование недопустимо. Вместо этого объявите производный тип как класс или структуру.

Следующий пример приводит к возникновению ошибки C2570:

```cpp
// C2570.cpp
// compile with: /c
class base {};
union hasPubBase : public base {};   // C2570
union hasNoBase {};   // OK
```
