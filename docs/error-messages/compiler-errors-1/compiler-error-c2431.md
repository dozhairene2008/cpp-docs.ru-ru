---
title: Ошибка компилятора C2431
ms.date: 11/04/2016
f1_keywords:
- C2431
helpviewer_keywords:
- C2431
ms.assetid: 88a5b648-c89f-47d1-a20e-63231ab4f0f7
ms.openlocfilehash: 135f73490cf23313d4ac4e2a5f568f2b6100422b
ms.sourcegitcommit: 16fa847794b60bf40c67d20f74751a67fccb602e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2019
ms.locfileid: "74744529"
---
# <a name="compiler-error-c2431"></a>Ошибка компилятора C2431

недопустимый регистр индекса в "идентификаторе"

Регистр ESP масштабируется или используется как индекс и базовый регистр. Кодировка СИБ для процессора x86 не позволяет ни один.

Следующий пример приводит к возникновению ошибки C2431:

```cpp
// C2431.cpp
// processor: x86
int main() {
   _asm mov ax, [ESI + 2*ESP]   // C2431
   _asm mov ax, [esp + esp]   // C2431
}
```
