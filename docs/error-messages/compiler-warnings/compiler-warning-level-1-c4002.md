---
title: Предупреждение компилятора (уровень 1) C4002
ms.date: 11/04/2016
f1_keywords:
- C4002
helpviewer_keywords:
- C4002
ms.assetid: 6bda1dfe-e2e4-4771-9794-5a404c466dd5
ms.openlocfilehash: 6aac8285e3935bb0fb910b52a7dd813d0a708732
ms.sourcegitcommit: 0cfc43f90a6cc8b97b24c42efcf5fb9c18762a42
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/05/2019
ms.locfileid: "73627396"
---
# <a name="compiler-warning-level-1-c4002"></a>Предупреждение компилятора (уровень 1) C4002

слишком много фактических параметров для макроопределения "идентификатор"

Количество фактических параметров в макросе превышает количество формальных параметров в определении макроса. Препроцессор собирает лишние параметры, но игнорирует их в расширении макроса.

Ошибка C4002 может возникать в результате неправильного использования [Variadic Macros](../../preprocessor/variadic-macros.md).

Следующий пример приводит к возникновению предупреждения C4002:

```cpp
// C4002.cpp
// compile with: /W1
#define test(a) (a)

int main() {
   int a = 1;
   int b = 2;
   a = test(a,b);   // C4002
   // try..
   a = test(a);
}
```

Эта ошибка также может возникать в результате действий по обеспечению совместимости компилятора с Visual Studio .NET 2003: лишние запятые в макросе больше не принимаются.

Компилятор больше не принимает лишние запятые в макросе. Чтобы код функционировал в Visual Studio .NET 2003 и в версиях Visual Studio .NET для Visual C++, следует удалить лишние запятые.

```cpp
// C4002b.cpp
// compile with: /W1
#define F(x,y)
int main()
{
   F(2,,,,,,3,,,,,,)   // C4002
   // Try the following line instead:
   // F(2,3)
}
```