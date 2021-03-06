---
title: Закрытие файлов
ms.date: 11/04/2016
helpviewer_keywords:
- MFC, file operations
- files [MFC], closing
ms.assetid: 8415a3a8-3c75-45b0-ac2a-d5385f49bdb3
ms.openlocfilehash: 69a0960c1edabab00cb71702acda526ee9ebd798
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62326928"
---
# <a name="closing-files"></a>Закрытие файлов

Как обычно в операциях ввода-вывода, после завершения работы с файлом, его необходимо закрыть.

#### <a name="to-close-a-file"></a>Чтобы закрыть файл

1. Используйте **закрыть** функция-член. Эта функция закрывает файл файловой системы и при необходимости очищает буферы.

Если выделен [CFile](../mfc/reference/cfile-class.md) объект в кадре (как в примере, показанном на [открытие файлов](../mfc/opening-files.md)), он будет автоматически закрыть и затем удаленных, когда оно выходит за пределы области. Обратите внимание, что удаление `CFile` объекта не удаляет физический файл в файловой системе.

## <a name="see-also"></a>См. также

[Файлы](../mfc/files-in-mfc.md)
