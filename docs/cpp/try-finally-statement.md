---
title: Оператор try-finally
ms.date: 11/19/2018
f1_keywords:
- __try
- _try
- __leave_cpp
- __leave
- __finally_cpp
- __try_cpp
- __finally
- _finally
helpviewer_keywords:
- __try keyword [C++]
- __finally keyword [C++]
- __leave keyword [C++]
- try-catch keyword [C++], try-finally keyword
- try-finally keyword [C++]
- __finally keyword [C++], try-finally statement syntax
- __leave keyword [C++], try-finally statement
- structured exception handling [C++], try-finally
ms.assetid: 826e0347-ddfe-4f6e-a7bc-0398e0edc7c2
ms.openlocfilehash: 045d2bf5617c81bcc4d7a202f36b112d5f0142a6
ms.sourcegitcommit: 654aecaeb5d3e3fe6bc926bafd6d5ace0d20a80e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/20/2019
ms.locfileid: "74246293"
---
# <a name="try-finally-statement"></a>Оператор try-finally

**Блок, относящийся только к системам Майкрософт**

Следующий синтаксис описывает оператор **try-finally** :

> **\_\_попробуйте**<br/>
> {<br/>
> &nbsp;&nbsp;&nbsp;&nbsp;//защищенный код<br/>
> }<br/>
> **\_\_, наконец**<br/>
> {<br/>
> &nbsp;&nbsp;&nbsp;&nbsp;//код завершения<br/>
> }

## <a name="grammar"></a>Грамматика

*try-finally-statement*:<br/>
&nbsp;&nbsp;&nbsp;&nbsp; **\_\_попробуйте** *составной оператор* **\_\_finally** *составной оператор*

Оператор **try-finally** — это расширение Майкрософт для C и C++ языков, которое позволяет целевым приложениям гарантировать выполнение кода очистки при прерывании выполнения блока кода. Очистка включает такие задачи, как отмена распределения памяти, закрытие файлов и освобождение их дескрипторов. Оператор **try-finally** особенно полезен для подпрограмм, в которых есть несколько мест, где выполняется проверка на наличие ошибки, которая может привести к преждевременному возврату из подпрограммы.

Связанные сведения и пример кода см. в разделе [оператор try-except](../cpp/try-except-statement.md). Дополнительные сведения об структурированной обработке исключений в целом см. в разделе [структурированная обработка исключений](../cpp/structured-exception-handling-c-cpp.md). Дополнительные сведения об обработке исключений в управляемых приложениях с помощью C++/CLI см. [в разделе Обработка исключений в разделе/CLR](../extensions/exception-handling-cpp-component-extensions.md).

> [!NOTE]
> Структурированная обработка исключений поддерживается в Win32 для исходных файлов как на C, так и на C++. Однако она не предназначена специально для C++. Для того чтобы ваш код лучше переносился, лучше использовать механизм обработки исключений языка C++. Кроме того, этот механизм отличается большей гибкостью, поскольку может обрабатывать исключения любого типа. Для C++ программ рекомендуется использовать механизм обработки C++ исключений (операторы[try, catch и Throw](../cpp/try-throw-and-catch-statements-cpp.md) ).

Составной оператор после предложения **__try** является защищенным разделом. Составной оператор после предложения **__finally** является обработчиком завершения. Такой обработчик определяет набор действий, выполняемых при выходе из защищенного раздела независимо от того, происходит ли выход в результате исключения (ненормальное завершение) или в результате стандартной передачи управления дальше (нормальное завершение).

Элемент управления достигает **__try** оператора с помощью простого последовательного выполнения (с переходом). Когда элемент управления входит в **__try**, связанный с ним обработчик становится активным. Если поток элементов управления достигает конца блока try, выполнение продолжается следующим образом.

1. Вызывается обработчик завершения.

1. После завершения работы обработчика завершения выполнение продолжится после выполнения инструкции **__finally** . Независимо от того, как заканчивается защищенный раздел (например, с помощью инструкции **goto** из защищенного текста или оператора **return** ), обработчик завершения выполняется *до* того, как поток управления перемещается из защищенного раздела.

   Оператор **__finally** не блокирует поиск соответствующего обработчика исключений.

Если в блоке **__try** возникает исключение, операционная система должна найти обработчик для исключения, иначе программа завершится ошибкой. Если обработчик найден, выполняются все и все блоки **__finally** и выполнение возобновляется в обработчике.

Например, предположим, ряд вызовов функций связывает функцию А с функцией D, как показано на следующем рисунке. Каждая функция имеет один обработчик завершения. Если исключение создается в функции D и обрабатывается в функции А, обработчики завершения вызываются в том порядке, в котором система освобождает стек: D, C и B.

![Порядок выполнения обработчика завершения&#45;](../cpp/media/vc38cx1.gif "Порядок выполнения обработчика завершения&#45;") <br/>
Порядок выполнения обработчиков завершения

> [!NOTE]
> Поведение try-finally отличается от некоторых других языков, которые поддерживают использование **и**, например, C#.  Один **__try** может иметь либо, но не оба, **__finally** и **__except**.  Если оба следует использовать одновременно, оператор try-except должен включать внутренней оператор try-finally.  Правила,задающие время выполнения каждого блока, также различаются.

Для совместимости с предыдущими версиями **_try**, **_finally**и **_leave** являются синонимами для **__try**, **__finally**и **__leave** , если не задан параметр компилятора [/Za \(отключить расширения языка)](../build/reference/za-ze-disable-language-extensions.md) .

## <a name="the-__leave-keyword"></a>Ключевое слово __leave

Ключевое слово **__leave** допустимо только в защищенном разделе оператора **try-finally** , и его результат заключается в переходе к концу защищенного раздела. Выполнение продолжается с первого оператора в обработчике завершения.

Оператор **goto** также может перейти из защищенного раздела, но снижает производительность, так как вызывает очистку стека. Оператор **__leave** более эффективен, так как не приводит к очистке стека.

## <a name="abnormal-termination"></a>Аварийное завершение

Выход из оператора **try-finally** с помощью функции времени выполнения [longjmp](../c-runtime-library/reference/longjmp.md) считается аномальным завершением. Переход к оператору **__try** недопустимым, но допустим, чтобы выйти из него. Необходимо запустить все инструкции **__finally** , активные между точкой отправления (нормальное завершение блока **__try** ) и назначением (блок **__except** , обрабатывающий исключение). Это называется "локальной раскруткой".

Если блок **try** преждевременно завершается по какой-либо причине, включая переход за пределы блока, система выполняет связанный блок **finally** как часть процесса очистки стека. В таких случаях функция [абнормалтерминатион](/windows/win32/Debug/abnormaltermination) возвращает **значение true** , если вызывается из блока **finally** ; в противном случае возвращается **значение false**.

Обработчик завершения не вызывается, если процесс завершается в процессе выполнения инструкции **try-finally** .

**Завершение блока, относящегося только к системам Майкрософт**

## <a name="see-also"></a>См. также:

[Написание обработчика завершения](../cpp/writing-a-termination-handler.md)<br/>
[Структурированная обработка исключений (C/C++)](../cpp/structured-exception-handling-c-cpp.md)<br/>
[Ключевые слова](../cpp/keywords-cpp.md)<br/>
[Синтаксис обработчика завершения](/windows/win32/Debug/termination-handler-syntax)