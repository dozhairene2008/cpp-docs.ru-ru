---
title: Ошибка времени выполнения C R6024
ms.date: 11/04/2016
f1_keywords:
- R6024
helpviewer_keywords:
- R6024
ms.assetid: 0fb11c0f-9b81-4cab-81bd-4785742946a5
ms.openlocfilehash: 89b99a93512603eaf2273a6ff3f434f1ad3b3bb8
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62214140"
---
# <a name="c-runtime-error-r6024"></a>Ошибка времени выполнения C R6024

не хватает места для таблицы _onexit/atexit

> [!NOTE]
> Обнаружив это сообщение об ошибке при выполнении приложения, приложения завершил работу, поскольку в нем внутренняя проблема с памятью. Эта ошибка обычно происходит с условием чрезвычайно нехватки памяти или в редких случаях ошибки в программе или повреждением используемых ею библиотек Visual C++.
>
> Для устранения этой ошибки попробуйте выполнить следующие действия:
>
> - Закройте другие запущенные приложения или перезагрузить компьютер, чтобы освободить память.
> - Используйте **программы и компоненты** или **программы и компоненты** странице в **панели управления** восстановите или переустановите программу.
> - Используйте **программы и компоненты** или **программы и компоненты** странице в **панели управления** восстановите или переустановите все копии Microsoft распространяемый компонент Visual C++.
> - Проверьте **Windows Update** в **панели управления** для обновлений программного обеспечения.
> - Проверьте наличие обновленной версии приложения. Если проблема будет повторяться, обратитесь к его поставщиком.

**Сведения для программистов**

Эта ошибка возникает, так как отсутствует недостаточно памяти для `_onexit` или `atexit` функции. Эта ошибка вызвана условие нехватки памяти. Можно выйти из предварительно выделение буферов при запуске приложения, помогающие при сохранении сведений о пользователях, а также очистить приложения в условиях нехватки памяти.