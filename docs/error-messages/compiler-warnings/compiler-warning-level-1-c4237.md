---
title: Предупреждение компилятора (уровень 1) C4237
ms.date: 11/04/2016
f1_keywords:
- C4237
helpviewer_keywords:
- C4237
ms.assetid: f2e86c4b-80d8-460e-9429-83c5f3f5d7ca
ms.openlocfilehash: e53c4632f8bfc9764f6ab1e124582bda273d945e
ms.sourcegitcommit: 0cfc43f90a6cc8b97b24c42efcf5fb9c18762a42
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/05/2019
ms.locfileid: "73624901"
---
# <a name="compiler-warning-level-1-c4237"></a>Предупреждение компилятора (уровень 1) C4237

ключевое слово "keyword" пока не поддерживается, но зарезервировано для будущего использования

Ключевое слово в C++ спецификации не реализовано в компиляторе C++ Майкрософт, но ключевое слово недоступно в качестве определяемого пользователем символа.

Следующий пример приводит к возникновению ошибки C4237:

```cpp
// C4237.cpp
// compile with: /W1 /c
int export;   // C4237
```