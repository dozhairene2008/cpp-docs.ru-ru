---
title: Предупреждение компилятора (уровень 1) C4163
ms.date: 11/04/2016
f1_keywords:
- C4163
helpviewer_keywords:
- C4163
ms.assetid: b08413fd-03fc-4f41-9167-a98976ac12f2
ms.openlocfilehash: 640ce66233fb8820ec434e70060a5ab3cf56c3c0
ms.sourcegitcommit: 0cfc43f90a6cc8b97b24c42efcf5fb9c18762a42
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/05/2019
ms.locfileid: "73627439"
---
# <a name="compiler-warning-level-1-c4163"></a>Предупреждение компилятора (уровень 1) C4163

"идентификатор": недоступен в качестве подставляемой функции

Указанная функция не может использоваться как [встроенная](../../preprocessor/intrinsic.md) функция. Компилятор игнорирует неправильное имя функции.

Следующий пример приводит к возникновению ошибки C4163.

```cpp
// C4163.cpp
// compile with: /W1 /LD
#include <math.h>
#pragma intrinsic(mysin)   // C4163
// try the following line instead
// #pragma intrinsic(sin)
```