---
title: Ошибка компилятора C2815
ms.date: 11/04/2016
f1_keywords:
- C2815
helpviewer_keywords:
- C2815
ms.assetid: d0256fd6-0721-4c99-b03c-52d96e77a613
ms.openlocfilehash: 579fc94f3b16056b5f26dd0b9ea16b5fc36fda22
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2019
ms.locfileid: "74750719"
---
# <a name="compiler-error-c2815"></a>Ошибка компилятора C2815

"operator delete": первый формальный параметр должен иметь значение "void *", но был использован "param"

Любая функция [удаления оператора](../../standard-library/new-operators.md#op_delete) , определяемого пользователем, должна принимать первый формальный параметр типа `void *`.

Следующий пример приводит к возникновению ошибки C2815:

```cpp
// C2815.cpp
// compile with: /c
class CMyClass {
public:
   void mf1(int *a);
   void operator delete(CMyClass *);   // C2815
   void operator delete(void *);
};
```
