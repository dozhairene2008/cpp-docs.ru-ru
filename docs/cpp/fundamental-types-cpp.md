---
title: Встроенные типы (C++)
ms.date: 12/11/2019
f1_keywords:
- __int128_cpp
- __wchar_t_cpp
- char_cpp
- char8_t_cpp
- char16_t_cpp
- char32_t_cpp
- double_cpp
- float_cpp
- int_cpp
- long_cpp
- long_double_cpp
- short_cpp
- signed_cpp
- unsigned_cpp
- unsigned_int_cpp
- wchar_t_cpp
helpviewer_keywords:
- specifiers [C++], type
- float keyword [C++]
- char keyword [C++]
- __wchar_t keyword [C++]
- signed types [C++], summary of data types
- Integer data type [C++], C++ data types
- arithmetic operations [C++], types
- int data type
- unsigned types [C++], summary of data types
- short data type [C++]
- double data type [C++], summary of types
- long long keyword [C++]
- long double keyword [C++]
- unsigned types [C++]
- signed types [C++]
- void keyword [C++]
- storage [C++], basic type
- integral types, C++
- wchar_t keyword [C++]
- floating-point numbers [C++], C++ data types
- long keyword [C++]
- type specifiers [C++]
- integral types
- long keyword [C++]
- storing types [C++]
- data types [C++], void
ms.assetid: 58b0106a-0406-4b74-a430-7cbd315c0f89
ms.openlocfilehash: e67d31e18ebbb6afd9d98542e4a6aa236b2d3e71
ms.sourcegitcommit: 63784729604aaf526de21f6c6b62813882af930a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/17/2020
ms.locfileid: "79445311"
---
# <a name="built-in-types-c"></a>Встроенные типы (C++)

Встроенные типы (также называемые *фундаментальными типами*) определяются стандартом C++ языка и встроены в компилятор. Встроенные типы не определены в файле заголовка. Встроенные типы делятся на три категории: целые, с плавающей запятой и void. Целочисленные типы позволяют обрабатывать целые числа. Типы с плавающей запятой позволяют задавать значения, которые могут иметь дробные части.

Типом [void](void-cpp.md) описывается пустой набор значений. Переменная типа **void** не может быть указана — она используется в основном для объявления функций, которые не возвращают значения, или для объявления универсальных указателей на нетипизированные или произвольные типизированные данные. Любое выражение может быть явно преобразовано или приведено к типу **void**. Однако такие выражения можно использовать только в следующих операторах и операндах:

- в операторе выражения (Дополнительные сведения см. в разделе [выражения](expressions-cpp.md).)

- в левом операнде оператора запятой (Дополнительные сведения см. в разделе [оператор-запятая](comma-operator.md).)

- во втором и третьем операндах условного оператора (`? :`). (Дополнительные сведения см. [в разделе выражения с условным оператором](conditional-operator-q.md).)

В следующей таблице описаны ограничения на размеры типов в связи друг с другом. Эти ограничения задаются C++ стандартом и не зависят от реализации Майкрософт. Абсолютный размер некоторых встроенных типов не указан в стандарте.

### <a name="built-in-type-size-restrictions"></a>Ограничения встроенного размера типа

|Категория|Тип|Содержимое|
|--------------|----------|--------------|
|Целые числа|**char**|Тип **char** является целочисленным типом, который обычно содержит члены базовой кодировки выполнения — по умолчанию это ASCII в Microsoft C++.<br /><br /> C++ Компилятор обрабатывает переменные типа **char**, **char со знаком**и **char без знака** как имеющие разные типы. Переменные типа **char** помещаются в тип **int** , как если бы по умолчанию они были **подписаны символом** , если не используется параметр компиляции/j. В этом случае они обрабатываются как тип **без знака типа char** и преобразуются в **int** без расширения знака.|
||**bool**;|Тип **bool** является целочисленным типом, который может иметь одно из двух значений **true** или **false**. Его размер не определен.|
||**short**|Тип **short int** (или просто **короткий**) — это целочисленный тип, размер которого больше или равен размеру типа **char**и меньше или равен размеру типа **int**.<br /><br /> Объекты типа **Short** могут быть объявлены как **короткие со знаком** или **без знака Short**. **Короткий знак** — это **синоним.**|
||**int**|Тип **int** — это целочисленный тип, размер которого больше или равен размеру типа **short int**и меньше или равен размеру типа **Long**.<br /><br /> Объекты типа **int** могут объявляться как целое число **со знаком** или **без знака int**. **Целое число со знаком** является синонимом для **int**.|
||**__int8**, **__int16**, **__int32**, **__int64**|Целое число с указанием размера `__int n`, где `n` — размер в битах целочисленной переменной. **__int8**, **__int16**, **__int32** и **__int64** являются ключевыми словами, специфичными для Майкрософт. Не все типы доступны во всех архитектурах. ( **__int128** не поддерживается.)|
||**long**|Тип **Long** (или **long int**) является целочисленным типом, который больше или равен размеру типа **int**. (В Windows **Long** имеет тот же размер, что и **int**.)<br /><br /> Объекты типа **Long** можно объявлять как длинные **со знаком** или **без знака**. **Long со знаком длинным** является синонимом **Long**.|
||**long long**|Больше, чем беззнаковое **длинное**.<br /><br /> Объекты типа **long long** могут быть объявлены длинными **длинными** или **беззнакыми**Long. длинное целое с **подписью** является синонимом **длинной**длины.|
||**wchar_t**, **__wchar_t**|Переменная типа **wchar_t** обозначает тип расширенных символов или многобайтового символа. По умолчанию **wchar_t** является собственным типом, но можно использовать параметр [/Zc: wchar_t](../build/reference/zc-wchar-t-wchar-t-is-native-type.md) , чтобы **wchar_t** typedef **без знака Short**. Тип **__wchar_t** — это синоним, зависящий от Майкрософт, для собственного типа **wchar_t** .<br /><br /> Чтобы задать расширенный символьный тип, перед символьным или строковым литералом следует использовать префикс L.|
|Число с плавающей запятой|**float**|Тип **float** является наименьшим типом с плавающей точкой.|
||**double**|Тип **Double** — это тип с плавающей запятой, который больше или равен типу **float**, но меньше или равен размеру типа **long double**.<br /><br /> Конкретно для Майкрософт: представление **длинных Double** и **Double** идентично. Однако **длинные Double** и **Double** являются отдельными типами.|
||**long double**|Тип **long double** — это тип с плавающей запятой, который больше или равен типу **Double**.|

**Блок, относящийся только к системам Microsoft**

В следующей таблице перечислены объемы хранилища, необходимые для встроенных типов в Microsoft C++. В частности, обратите внимание, что **Long** — 4 байта даже в 64-разрядных операционных системах.

### <a name="sizes-of-built-in-types"></a>Размеры встроенных типов

|Тип|Размер|
|----------|----------|
|**bool**, **char**, **без знака**, символ **со знаком**, **__int8**|1 байт|
|**__int16**, **короткий**, **неподписанный короткий**, **wchar_t**, **__wchar_t**|2 байта|
|**float**, **__int32**, **int**, **без знака int**, **Long**, **без знака Long**|4 байта|
|**Double**, **__int64**, **длинное двойное**, **длинное** целое|8 байт|

**Завершение блока, относящегося только к системам Майкрософт**

Сводку по диапазонам значений каждого типа см. в разделе [Диапазоны типов данных](data-type-ranges.md) .

Дополнительные сведения о преобразовании типов см. в разделе [Стандартные преобразования](standard-conversions.md).

## <a name="see-also"></a>См. также раздел

[Диапазоны типов данных](data-type-ranges.md)