---
title: Ошибка компилятора C2032
ms.date: 11/04/2016
f1_keywords:
- C2032
helpviewer_keywords:
- C2032
ms.assetid: 625d7c83-70b6-42c2-a558-81fbc0026324
ms.openlocfilehash: d20bc61df2d0bab9115768b3bc0589f11a9bcdb9
ms.sourcegitcommit: a5fa9c6f4f0c239ac23be7de116066a978511de7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/20/2019
ms.locfileid: "75302098"
---
# <a name="compiler-error-c2032"></a>Ошибка компилятора C2032

"идентификатор": функция не может быть членом структуры или объединения "структорунион"

Структура или объединение имеет функцию-член, которая допускается в C++ , но не в C. Чтобы устранить эту ошибку, либо скомпилируйте ее как C++ программу, либо удалите функцию-член.

Следующий пример приводит к возникновению ошибки C2032:

```c
// C2032.c
struct z {
   int i;
   void func();   // C2032
};
```

Возможное решение:

```c
// C2032b.c
// compile with: /c
struct z {
   int i;
};
```
