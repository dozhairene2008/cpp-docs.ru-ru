---
title: Пустой и неопределенный макрос
ms.date: 11/04/2016
helpviewer_keywords:
- NMAKE program, undefined macros
- Null macros in NMAKE
- macros, null and undefined
- undefined macros and NMAKE
- NMAKE program, null macros
ms.assetid: 1db4611a-1755-4328-b00f-d35365af8b6c
ms.openlocfilehash: 0f4905473dd6914547ad6ac129d34e438992c2af
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62320504"
---
# <a name="null-and-undefined-macros"></a>Пустой и неопределенный макрос

Пустой и неопределенный макрос разворачиваются в пустые строки, но макрос, определенный как строку null считается определены в выражениях предварительной обработки. Чтобы определить макрос как строку null, укажите никакие символы не только пробелы или символы табуляции после знака равенства (=) в командной строке или командный файл и заключите пустую строку или определение в двойные кавычки (» «). Чтобы отменить определение макроса, используйте **! UNDEF.** Дополнительные сведения см. в разделе [директивы предварительной обработки файла Makefile](makefile-preprocessing-directives.md).

## <a name="see-also"></a>См. также

[Определение макроса NMAKE](defining-an-nmake-macro.md)
