﻿---
title: Мультипликативные операторы и оператор взятия остатка
ms.date: 11/04/2016
f1_keywords:
- '%'
- /
helpviewer_keywords:
- operators [C++], multiplicative
- arithmetic operators [C++], multiplicative operators
- modulus operator [C++]
- '* operator'
- division operator [C++], multiplicative operators
- '% operator'
- multiplication operator [C++], multiplicative operators
- multiplicative operators [C++]
- division operator
ms.assetid: b53ea5da-d0b4-40dc-98f3-0aa52d548293
ms.openlocfilehash: 9a01672976703634c06724c9c655605bb433facf
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62301829"
---
# <a name="multiplicative-operators-and-the-modulus-operator"></a>Мультипликативные операторы и оператор взятия остатка

## <a name="syntax"></a>Синтаксис

```
expression * expression
expression / expression
expression % expression
```

## <a name="remarks"></a>Примечания

Ниже перечислены мультипликативные операторы.

- Умножение (<strong>\*</strong>)

- Деление (**/**)

- Взятие остатка от деления (**%**)

Эти бинарные операторы имеют ассоциативность слева направо.

Мультипликативные операторы принимают операнды арифметических типов. Оператор взятия остатка (**%**) имеет более строгое ограничение: его операнды должны быть целочисленного типа. (Чтобы получить остаток от деления с плавающей запятой, используйте функцию времени выполнения, [fmod](../c-runtime-library/reference/fmod-fmodf.md).) К операндам применяются преобразования, описанные в статье [стандартные преобразования](standard-conversions.md), и результатом является преобразованный тип.

Оператор умножения возвращает результат умножения первого операнда на второй.

Оператор деления возвращает результат деления первого операнда на второй.

Оператор взятия остатка возвращает остаток, полученный как результат вычисления следующего выражения, где *e1* — первый операнд, *e2* — второй операнд: *e1* -(*e1*  /  *e2*) \* *e2*, где оба операнда имеют целочисленный тип.

Деление на 0 в выражении деления или взятия остатка не определено и вызывает ошибку времени выполнения. Поэтому следующие выражения создают неопределенные ошибочные результаты.

```cpp
i % 0
f / 0.0
```

Если оба операнда в выражении умножения, деления или взятия остатка имеют одинаковые знаки, результат будет положительным. В противном случае результат будет отрицательным. Знак результата операции взятия остатка определяется реализацией.

> [!NOTE]
>  Поскольку преобразования, выполняемые мультипликативными операторами, не обеспечивают условия переполнения и потери значимости, данные могут быть потеряны, если результат мультипликативной операции невозможно представить в типе операндов после преобразования.

**Блок, относящийся только к системам Microsoft**

В Microsoft C++ знак результата выражения модуля всегда совпадает со знаком первого операнда.

**Завершение блока, относящегося только к системам Майкрософт**

Если значение, полученное при делении двух целых чисел, неточное и только один операнд является отрицательным, результатом будет наибольшее целое число (по величине без учета знака), которое меньше точного значения, которое было бы получено при операции деления. Например, вычисленное значение выражения -11 / 3 равно -3.666666666. Результат целочисленного деления — -3.

Связь между мультипликативными операторами определяется тождеством (*e1* / *e2*) \* *e2*  +  *e1* % *e2* == *e1*.

## <a name="example"></a>Пример

В следующей программе показаны мультипликативные операторы. Обратите внимание, что один из операндов `10 / 3` должен быть явно приведен к типу **float** во избежание усечения, чтобы оба операнда имели тип **float** перед делением.

```cpp
// expre_Multiplicative_Operators.cpp
// compile with: /EHsc
#include <iostream>
using namespace std;
int main() {
   int x = 3, y = 6, z = 10;
   cout  << "3 * 6 is " << x * y << endl
         << "6 / 3 is " << y / x << endl
         << "10 % 3 is " << z % x << endl
         << "10 / 3 is " << (float) z / x << endl;
}
```

## <a name="see-also"></a>См. также

[Выражения с бинарными операторами](../cpp/expressions-with-binary-operators.md)<br/>
[Встроенные операторы C++, приоритет и ассоциативность](../cpp/cpp-built-in-operators-precedence-and-associativity.md)<br/>
[Операторы умножения в C](../c-language/c-multiplicative-operators.md)
