---
title: Оператор do-while (C)
ms.date: 11/04/2016
f1_keywords:
- do
helpviewer_keywords:
- do-while keyword [C]
ms.assetid: f2ac20a6-10c7-4a08-b5e3-c3b3639dbeaf
ms.openlocfilehash: 3658fe7635ad77db6d6e08ff9d7c30e29d665721
ms.sourcegitcommit: 63784729604aaf526de21f6c6b62813882af930a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/17/2020
ms.locfileid: "79438589"
---
# <a name="do-while-statement-c"></a>Оператор do-while (C)

Оператор *do-while* позволяет повторять простой или составной оператор, пока указанное выражение не примет значение false.

## <a name="syntax"></a>Синтаксис

*оператор итерации*: &nbsp;&nbsp;&nbsp;&nbsp;**Do***оператор***while (** *выражение* **);**

Выражение *expression* в операторе *do-while* вычисляется после выполнения тела цикла. Поэтому тело цикла всегда выполняется по крайней мере один раз.

Выражение *expression* должно иметь арифметический тип или тип указателя. Выполнение происходит следующим образом:

1. Выполняется тело оператора.

1. Затем вычисляется значение *expression*. Если выражение *expression* имеет значение false, выполнение оператора *do-while* завершается и управление передается следующему оператору программы. Если *expression* имеет значение true (то есть не равно нулю), процесс повторяется с шага 1.

Выполнение оператора *do-while* также может прерваться, если в теле оператора выполняется оператор **break**, **goto** или **return**.

Это пример оператора *do-while*:

```C
do
{
    y = f( x );
    x--;
} while ( x > 0 );
```

В этом операторе *do-while* два оператора `y = f( x );` и `x--;` выполняются независимо от начального значения переменной `x`. Затем вычисляется выражение `x > 0`. Если `x` больше 0, тело оператора выполняется еще раз и снова вычисляется выражение `x > 0`. Тело оператора многократно выполняется, пока значение переменной `x` остается больше 0. Выполнение оператора *do-while* завершается, когда значение переменной `x` становится равным 0 или отрицательным. Тело цикла выполняется по крайней мере один раз.

## <a name="see-also"></a>См. также раздел

[Оператор do-while (C)](../cpp/do-while-statement-cpp.md)
