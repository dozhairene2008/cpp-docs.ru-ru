---
title: Ошибка компилятора C3120
ms.date: 11/04/2016
f1_keywords:
- C3120
helpviewer_keywords:
- C3120
ms.assetid: 9b6b210f-9948-4517-a4cc-b4aaadebde68
ms.openlocfilehash: ced859be68f780d0f0dee31e31d80b994ee73404
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2019
ms.locfileid: "74740953"
---
# <a name="compiler-error-c3120"></a>Ошибка компилятора C3120

"method_name": методы интерфейса не могут принимать переменный список аргументов

Метод интерфейса не может принимать переменный список аргументов. Например, следующее определение интерфейса создает C3120:

```cpp
// C3120.cpp
__interface A {
int X(int i, ...);    // C3120
};

int main(void) { return(0); }
```
