---
title: Предупреждение компилятора (уровень 1) C4230
ms.date: 11/04/2016
f1_keywords:
- C4230
helpviewer_keywords:
- C4230
ms.assetid: a4be8729-74b6-44df-a5ea-e3f45aad0f8f
ms.openlocfilehash: 668060f372a86295ef9a2cbcc1d5a6cd4ae9b2c5
ms.sourcegitcommit: 0cfc43f90a6cc8b97b24c42efcf5fb9c18762a42
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/05/2019
ms.locfileid: "73624918"
---
# <a name="compiler-warning-level-1-c4230"></a>Предупреждение компилятора (уровень 1) C4230

устаревший элемент: смешанные модификаторы и квалификаторы; пропуск квалификатора

Использование квалификатора перед использованием модификатора Майкрософт, такого как `__cdecl`, является устаревшей практикой.

## <a name="example"></a>Пример

```cpp
// C4230.cpp
// compile with: /W1 /LD
int __cdecl const function1();   // C4230 const ignored
```