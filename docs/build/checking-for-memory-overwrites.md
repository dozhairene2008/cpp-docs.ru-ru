---
title: Проверка затирания памяти
ms.date: 11/04/2016
helpviewer_keywords:
- memory, overwrites
ms.assetid: da7c5d77-a267-415f-a8ab-ee5ce5bfc286
ms.openlocfilehash: 2c59cb96d640df6dcd96b9e0eafbcd325ed475f5
ms.sourcegitcommit: c6f8e6c2daec40ff4effd8ca99a7014a3b41ef33
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/24/2019
ms.locfileid: "64342255"
---
# <a name="checking-for-memory-overwrites"></a>Проверка затирания памяти

Если вы получаете нарушение прав доступа при вызове функции обработки кучи, существует возможность, что приложение повредило ее. Признаком такой ситуации будет следующим:

```
Access Violation in _searchseg
```

[_Heapchk](../c-runtime-library/reference/heapchk.md) функция доступна в обоих отладки и сборки выпуска (только для Windows NT) для проверки целостности кучи библиотеки времени выполнения. Можно использовать `_heapchk` так же, как `AfxCheckMemory` функцию для изолирования затирания, например:

```
if(_heapchk()!=_HEAPOK)
   DebugBreak();
```

Если эта функция никогда не выполняется, необходимо изолировать в какой момент куча была повреждена.

## <a name="see-also"></a>См. также

[Устранение проблем сборки выпуска](fixing-release-build-problems.md)
