---
title: Интерпретация ввода пользователя через представление
ms.date: 11/04/2016
helpviewer_keywords:
- interpreting user input through views [MFC]
- views [MFC], user interface and input
- input [MFC], view class [MFC]
- CView class [MFC], interpreting user input
- user input [MFC], interpreting through view class [MFC]
ms.assetid: f0302a70-661f-4781-8fe7-78f082bef2a5
ms.openlocfilehash: 3ef23ad74e1ff53d947453faa5682c5ecc1f4e43
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62310920"
---
# <a name="interpreting-user-input-through-a-view"></a>Интерпретация ввода пользователя через представление

Другие функции-члены представления обработки и интерпретации весь пользовательский ввод. Функции-члены обработчика сообщений обычно определяются в классе представления, для обработки:

- Windows [сообщений](../mfc/messages.md) создаваемые действиями мыши и клавиатуры.

- [Команды](../mfc/user-interface-objects-and-command-ids.md) из меню, кнопки панели инструментов и сочетания клавиш.

Эти функции-члены обработчика сообщений интерпретировать следующее как входные данные, выбора и редактирования, включая перемещение данных в и из буфера обмена:

- Движения мыши щелчков, перетаскивания и дважды щелкает

- Нажатия клавиш

- Команды меню

Какие сообщения Windows дескрипторам представление зависит от потребностей вашего приложения.

[Обработка и сопоставление разделов сообщений](../mfc/message-handling-and-mapping.md) объясняет, как назначить пунктов меню и другие объекты пользовательского интерфейса для команд и как выполнить привязку к функции обработчика команд. [Обработка и сопоставление разделов сообщений](../mfc/message-handling-and-mapping.md) также объясняется, как MFC маршрутизирует команды и отправляет стандартные сообщения Windows к объектам, которые содержат обработчики для них.

Например приложение может потребоваться реализовать прямой указатель мыши, рисование в представлении. Пример Scribble демонстрируется обработка сообщений WM_LBUTTONDOWN, WM_LBUTTONUP и wm_mousemove и, соответственно, чтобы продолжить, начальное и конечное Рисование сегмент линии. С другой стороны иногда может потребоваться интерпретировать щелчка кнопкой мыши в представлении как выделенной области. В представлении `OnLButtonDown` функция обработчика определит рисования или выбрав пользователя. Если была выбрана, обработчик бы определить, была ли щелчок в пределах какой-либо объект в представлении и, если да, alter отображать объект в качестве выбранного.

Представление может также обрабатывать некоторые команды, например адреса из меню "Правка", чтобы вырезать, копировать, вставить или удалить выбранные данные, использование буфера обмена. Такой обработчик будет вызывать некоторые связанные с буфер обмена элемента функции класса `CWnd` для передачи выбранного элемента данных или из буфера обмена.

## <a name="see-also"></a>См. также

[Использование представлений](../mfc/using-views.md)
