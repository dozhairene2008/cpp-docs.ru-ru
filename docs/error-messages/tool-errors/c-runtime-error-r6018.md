---
title: Ошибка времени выполнения C R6018
ms.date: 11/04/2016
f1_keywords:
- R6018
helpviewer_keywords:
- R6018
ms.assetid: f6dd40d1-a119-4d8b-b39e-97350ea23349
ms.openlocfilehash: b36e2184e5be131645fb4dd58a361fdb9a31da63
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62214224"
---
# <a name="c-runtime-error-r6018"></a>Ошибка времени выполнения C R6018

Непредвиденная ошибка кучи

> [!NOTE]
> Обнаружив это сообщение об ошибке при выполнении приложения, приложения была завершена из-за внутренней проблемы. Существует несколько возможных причин возникновения данной ошибки, но часто причиной является ошибка в коде приложения.
>
> Для устранения этой ошибки попробуйте выполнить следующие действия:
>
> - Используйте **программы и компоненты** или **программы и компоненты** странице в **панели управления** восстановите или переустановите программу.
> - Проверьте **Windows Update** в **панели управления** для обновлений программного обеспечения.
> - Проверьте наличие обновленной версии приложения. Если проблема будет повторяться, обратитесь к его поставщиком.

**Сведения для программистов**

Программа обнаружила непредвиденную ошибку во время выполнения операции управления памятью.

Эта ошибка обычно возникает, если программа случайно изменяет данные кучи времени выполнения. Тем не менее она может также быть вызвана Внутренняя ошибка среды выполнения или операционной системы.

Чтобы устранить эту проблему, проверьте наличие ошибки повреждения кучи в коде. Дополнительные сведения и примеры см. в разделе [сведения о куче отладки CRT](/visualstudio/debugger/crt-debug-heap-details). Затем проверьте, что вы используете последние версии распространяемых компонентов для развертывания приложения. Сведения см. в разделе [развертывание в Visual C++](../../windows/deployment-in-visual-cpp.md).