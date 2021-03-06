---
title: Параметр /RANGE
ms.date: 11/04/2016
f1_keywords:
- /RANGE
helpviewer_keywords:
- /RANGE dumpbin option
- -RANGE dumpbin option
ms.assetid: 7eeba266-32be-49cc-a350-96bdf541f98a
ms.openlocfilehash: c631057e47e1a52a58d2b1304133dfdfc008ae14
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62319711"
---
# <a name="range"></a>Параметр /RANGE

Изменяет вывод свойства (программа DUMPBIN) при использовании с другими параметрами (программа DUMPBIN), например/RAWDATA или/DISASM.

## <a name="syntax"></a>Синтаксис

```
/RANGE:vaMin[,vaMax]
```

## <a name="parameters"></a>Параметры

*vaMin*<br/>
Виртуальный адрес, в которой необходимо начать операцию (программа DUMPBIN).

*vaMax*<br/>
(Необязательно) Виртуальный адрес, по которому вы не хотите dumpbin для завершения. Если не указан, dumpbin перейдет в конец файла.

## <a name="remarks"></a>Примечания

Чтобы просмотреть виртуальные адреса образа, используйте файл сопоставления для образа (RVA + Base), **/DISASM** или **/Headers** параметр (программа DUMPBIN), или Дизассемблированный код в отладчике Visual Studio.

## <a name="example"></a>Пример

В этом примере **/диапазон** используется для изменения отображения **/DISASM** параметр. В этом примере начальное значение выражается как десятичное число, и конечное значение указывается в виде шестнадцатеричного числа.

```
dumpbin /disasm /range:4219334,0x004061CD t.exe
```

## <a name="see-also"></a>См. также

[Параметры DUMPBIN](dumpbin-options.md)
