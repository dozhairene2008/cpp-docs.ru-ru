---
title: Ошибка построения проекта PRJ0003
ms.date: 11/04/2016
f1_keywords:
- PRJ0003
helpviewer_keywords:
- PRJ0003
ms.assetid: fc5a84bb-c6d3-41d6-8dd6-475455820778
ms.openlocfilehash: e30a63ba48434196478b52283880864d3e4ae6ea
ms.sourcegitcommit: 28eae422049ac3381c6b1206664455dbb56cbfb6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2019
ms.locfileid: "66450756"
---
# <a name="project-build-error-prj0003"></a>Ошибка построения проекта PRJ0003

> Порождает ошибку "*командной строки*".

*Командной строки* команда сформирован на основе входных данных в **страницы свойств** диалоговое окно вернул код ошибки, но не отображаются данные в **вывода** окна.

Возможные причины этой ошибки включают:

- Сервер ATL зависит ваш проект. Начиная с Visual Studio 2008, сервера ATL больше не входит в состав Visual Studio, но была выпущена в виде исходного проекта на сайте CodePlex. Чтобы загрузить исходный код ATL-сервера и средства, перейдите к [библиотеки ATL Server и средств](https://go.microsoft.com/fwlink/p/?linkid=81979).

- Нехватка системных ресурсов. Закройте некоторые приложения, чтобы устранить эту проблему.

- Недостаточные привилегии безопасности. Убедитесь в наличии требуемых привилегий безопасности.

- Пути к исполняемым файлам, указанный в **каталоги VC ++** не включают путь для инструмента, который вы пытаетесь запустить. Сведения см. в разделе [задать компилятора и свойства сборки](../../build/working-with-project-properties.md)

- Для проекта makefile, отсутствует команда на выполнение в **построения командной строки** или **командной строке перестроения**.

## <a name="see-also"></a>См. также

[Ошибки и предупреждения режима сборки проекта (PRJxxxx)](../../error-messages/tool-errors/project-build-errors-and-warnings-prjxxxx.md)