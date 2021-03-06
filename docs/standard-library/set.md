---
title: '&lt;set&gt;'
ms.date: 11/04/2016
f1_keywords:
- <set>
helpviewer_keywords:
- set header
ms.assetid: 43cb1ab2-6383-48cf-8bdc-2b96d7203596
ms.openlocfilehash: fed6219c483bdade0132d5faae8b6597bcc5d732
ms.sourcegitcommit: 590e488e51389066a4da4aa06d32d4c362c23393
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/21/2019
ms.locfileid: "72686461"
---
# <a name="ltsetgt"></a>&lt;set&gt;

Определяет шаблоны классов контейнеров Set и мультинаборов и их вспомогательные шаблоны.

## <a name="requirements"></a>Требования

**Заголовок:** \<set>

**Пространство имен:** std

> [!NOTE]
> Библиотека \<set > также использует инструкцию `#include <initializer_list>`.

## <a name="members"></a>Члены

### <a name="operators"></a>Операторы

|Версия Set|Версия Multiset|Описание|
|-|-|-|
|[operator!= (set)](../standard-library/set-operators.md#op_neq)|[operator!= (multiset)](../standard-library/set-operators.md#op_neq)|Проверяет неравенство объекта set или multiset слева от оператора объекту set или multiset справа от оператора.|
|[operator< (set)](../standard-library/set-operators.md#op_lt)|[operator< (multiset)](../standard-library/set-operators.md#op_lt_multiset)|Проверяет, меньше ли объект set или multiset слева от оператора объекта set или multiset справа от оператора.|
|[operator<= (set)](../standard-library/set-operators.md#op_lt_eq)|[operator\<= (multiset)](../standard-library/set-operators.md#op_lt_eq_multiset)|Проверяет, меньше или равен ли объект set или multiset слева от оператора объекту set или multiset справа от оператора.|
|[operator== (set)](../standard-library/set-operators.md#op_eq_eq)|[operator== (multiset)](../standard-library/set-operators.md#op_eq_eq_multiset)|Проверяет равенство объекта set или multiset слева от оператора объекту set или multiset справа от оператора.|
|[operator> (set)](../standard-library/set-operators.md#op_gt)|[operator> (multiset)](../standard-library/set-operators.md#op_gt_multiset)|Проверяет, больше ли объект set или multiset слева от оператора объекта set или multiset справа от оператора.|
|[operator>= (set)](../standard-library/set-operators.md#op_gt_eq)|[operator>= (multiset)](../standard-library/set-operators.md#op_gt_eq_multiset)|Проверяет, больше или равен ли объект set или multiset слева от оператора объекту set или multiset справа от оператора.|

### <a name="specialized-template-functions"></a>Специализированные функции шаблонов

|Версия Set|Версия Multiset|Описание|
|-|-|-|
|[swap](../standard-library/set-functions.md#swap)|[swap (multiset)](../standard-library/set-functions.md#swap_multiset)|Меняет местами элементы двух объектов set или multiset.|

### <a name="classes"></a>Классы

|||
|-|-|
|[Класс set](../standard-library/set-class.md)|Используется для хранения и извлечения данных из коллекции, в которой значения элементов должны быть уникальными и в которой они служат в качестве значений ключей, согласно которым данные автоматически упорядочиваются.|
|[Класс multiset](../standard-library/multiset-class.md)|Используется для хранения и извлечения данных из коллекции, в которой значения элементов не должны быть уникальными и в которой они служат в качестве значений ключей, согласно которым данные автоматически упорядочиваются.|

## <a name="see-also"></a>См. также

[Справочник по файлам заголовков](../standard-library/cpp-standard-library-header-files.md)\
[Потокобезопасность в стандартной библиотеке C++](../standard-library/thread-safety-in-the-cpp-standard-library.md)\
[Справочник по стандартной библиотеке C++](../standard-library/cpp-standard-library-reference.md)
