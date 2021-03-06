---
title: Постоянные выражения C++
ms.date: 11/04/2016
helpviewer_keywords:
- constant expressions, syntax
- constant expressions
- expressions [C++], constant
ms.assetid: b07245a5-4c21-4589-b503-e6ffd631996f
ms.openlocfilehash: 97059066adadc3a7897cbd2c4c747e2a673e7201
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62154676"
---
# <a name="c-constant-expressions"></a>Постоянные выражения C++

Объект *константы* значение — это приложения, не изменяется. В C++ имеется два ключевых слова, позволяющих указать, что объект не должен изменяться, и для осуществления этого намерения.

В C++ требуются константные выражения, то есть выражения, результатом вычисления которых является константа, для объявления следующих элементов.

- Границы массива.

- Селекторы в операторах case.

- Спецификация длины битового поля.

- Инициализаторы перечисления.

Ниже перечислены единственные допустимые операнды в константных выражениях.

- Литералы

- Константы перечисления.

- Значения, объявленные как константы, которые инициализированы с константными выражениями.

- **sizeof** выражения

Нецелочисленные константы должны преобразовываться (явно или неявно) в целочисленные типы, чтобы быть допустимыми в константном выражении. Поэтому следующий код допустим.

```cpp
const double Size = 11.0;
char chArray[(int)Size];
```

Явные преобразования в целочисленные типы допустимы в константных выражениях; все другие типы и производные типы недопустимы, за исключением случаев использования в качестве операндов **sizeof** оператор.

Запятую-оператор и операторы присваивания невозможно использовать в константных выражениях.

## <a name="see-also"></a>См. также

[Типы выражений](../cpp/types-of-expressions.md)