---
title: Неустранимая ошибка NMAKE U1051
ms.date: 11/04/2016
f1_keywords:
- U1051
helpviewer_keywords:
- U1051
ms.assetid: fede5cd5-dac3-47b7-b86d-e1acfb78699f
ms.openlocfilehash: ddf1d262fb8dfc6e63b0bf5cc098b7b140539310
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62367204"
---
# <a name="nmake-fatal-error-u1051"></a>Неустранимая ошибка NMAKE U1051

Недостаточно памяти

NMAKE не хватило памяти, включая виртуальной памяти, поскольку файл makefile слишком больших или сложных.

### <a name="to-fix-by-using-the-following-possible-solutions"></a>Возможные способы устранения этой ошибки

1. Освободите место на диске.

1. Увеличьте размер файла подкачки Windows NT или файл подкачки Windows.

1. Часть файла makefile используется, если только разделить файл makefile в отдельные файлы или использовать **! Если** директивы для ограничения объема обработки NMAKE предварительной обработки. **! Если** относятся **! Если**, `!IFDEF`, **! IFNDEF**, **! ELSE IF**, **! ELSE** `IFDEF`, и **! ELSE** `IFNDEF`.