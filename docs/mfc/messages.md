---
title: Сообщения
ms.date: 11/04/2016
helpviewer_keywords:
- messages, MFC
- messages [MFC]
ms.assetid: b1476310-a135-42ca-817c-444fb3675491
ms.openlocfilehash: 8e1bfd1baa8ffef76ba31912fc619c4217696683
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62384131"
---
# <a name="messages"></a>Сообщения

Цикл обработки сообщений в `Run` функция-член класса `CWinApp` извлекает поставлены в очередь сообщения, сформированные при возникновении различных событий. Например когда пользователь нажимает кнопку мыши, Windows отправляет несколько сообщений, связанных с мышью, например WM_LBUTTONDOWN при нажатии левой кнопки мыши и WM_LBUTTONUP при отпускании левой кнопки мыши. Реализация платформы цикл обработки сообщений приложения отправляет сообщение в соответствующем окне.

Описываются важные категории сообщений в [категории сообщений](../mfc/message-categories.md).

## <a name="see-also"></a>См. также

[Сообщения и команды платформы](../mfc/messages-and-commands-in-the-framework.md)
