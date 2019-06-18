---
title: Чтение и понимание C++ кода в Visual Studio
description: Используйте C++ редактора кода в Visual Studio для форматирования и понимание кода.
ms.date: 05/28/2019
ms.openlocfilehash: c5e4d7f3e53ef37649e3635d11cf99b10cb8a7ee
ms.sourcegitcommit: 65ed563a8a1d4d90f872a2a6edcb086f84ec9f77
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2019
ms.locfileid: "66742030"
---
# <a name="read-and-understand-c-code-in-visual-studio"></a>Чтение и понимание C++ кода в Visual Studio

Редактор кода C++ и Visual Studio IDE предоставляют различные вспомогательные средства кодирования. Одни уникальны для C++, а другие фактически одинаковы для всех языков Visual Studio. Дополнительные сведения об общих функциях см. в разделе [Написание кода в редакторе кода и текста](/visualstudio/ide/writing-code-in-the-code-and-text-editor).  

## <a name="colorization"></a>Цветовое выделение

Visual Studio также раскрашивания элементы синтаксиса, чтобы различать типы символов, таких как ключевые слова языка, имена типов, имена переменных, параметров функции, строковые литералы и т. д.

![Выделение кода цветом](../ide/media/code-outline-colorization.png " C++ цветовое выделение")

 Неиспользуемый код (например, код в разделе #if 0) более затемнение цветом.

 ![Неактивный код](../ide/media/inactive-code-cpp.png " C++ неактивного кода")

Можно настроить цвета, введя «Шрифты» в **быстрого запуска**, а затем выбрав **шрифты и цвета**. В **шрифты и цвета** диалоговое окно прокрутите вниз до C /C++ параметры, а затем выберите пользовательский шрифт и цвет.

## <a name="outlining"></a>Структуризация

Щелкните правой кнопкой мыши файл исходного кода и выберите **структура** Чтобы свернуть или развернуть блоки кода и (или) настраиваемые области для упрощения просмотра только кода, которые вас интересуют. Дополнительные сведения см. в разделе [Структура](/visualstudio/ide/outlining).

![C&#43; &#43; структурирование](../ide/media/vs2015_cpp_outlining.png "структурирование")

Если вы поместите курсор перед фигурная скобка, "{" или "}", редактор выделяет соответствующий какой.

Другие структуры параметры находятся в папке **изменить** > **структура** в главном меню.

## <a name="line-numbers"></a>Номера строк

Номера строк можно добавить в проект, выбрав **средства** > **параметры** > **текстовый редактор** > **все Языки** > **Общие** или поиска по «num строки» с **быстрый запуск (Ctrl + Q)** . Номера строк можно задать для всех языков или для конкретных языков, включая C++.

## <a name="scroll-and-zoom"></a>Прокрутка и изменение масштаба

Можно увеличить или уменьшить в редакторе, нажав клавишу **Ctrl** ключ и прокрутка с помощью колесика мыши. Кроме того, можно масштабировать с помощью параметров масштабирования в левом нижнем углу.

![C&#43; &#43; масштаб](../ide/media/zoom-control.png "элемент управления масштабом")

Полоса прокрутки **режим карты** позволяет быстро прокручивать и просматривать файл кода, не покидая текущего расположения. Можно щелкнуть в любом месте на карте кода, чтобы перейти непосредственно к этому расположению.

![Карта на языке C кода&#43;&#43;](../ide/media/vs2015-cpp-code-map.png "карта кода")

Чтобы включить **режим карты**, введите «map» **быстрого запуска** поле поиска на главной панели инструментов и выберите **использование режима карты прокрутки**. Дополнительные сведения см. в разделе [Практическое руководство. Отслеживание кода путем настройки полосы прокрутки](/visualstudio/ide/how-to-track-your-code-by-customizing-the-scrollbar).

Когда **режим карты** выключен, то полоса прокрутки по-прежнему выделяет изменения, внесенные в файл. Зеленый цвет означает изменения сохранены и желтое — несохраненные изменения.

## <a name="quick-info-and-parameter-info"></a>Краткие сведения и сведения о параметрах

Наведите указатель на любой переменной, функции или другой символ, чтобы получить сведения о нем, включая объявление и любые комментарии, которые находятся в только что предшествует ей.

::: moniker range="vs-2019"

![Краткие сведения в C&#43;&#43;](../ide/media/quick-info-vs2019.png "краткие сведения")

**Краткие сведения** подсказки имеется **поиск в Интернете** ссылку. Перейдите к **средства** > **параметры** > **текстовый редактор**  >  **C++**  >  **Представление** чтобы указать поставщика поиска. 

Есть ли ошибки в коде, можно навести указатель мыши над ней и **краткие сведения** будет отображаться сообщение об ошибке. Сообщение об ошибке можно также найти в окне списка ошибок.

![Краткие сведения об ошибке](../ide/media/quickinfo-on-error.png "краткие сведения об ошибке")

::: moniker-end

::: moniker range="<=vs-2017"

![Краткие сведения в C&#43;&#43;](../ide/media/quick-info.png "краткие сведения")

Есть ли ошибки в коде, можно навести указатель мыши над ней и **краткие сведения** будет отображаться сообщение об ошибке. Можно также найти сообщение об ошибке в **список ошибок** окна.

![Краткие сведения об ошибке](../ide/media/quickinfo-on-error.png "краткие сведения об ошибке")

::: moniker-end

При вызове функции, **сведения о параметрах** показаны типы параметров и порядок, в котором они ожидаются.

![Сведения о параметрах для C&#43;&#43;](../ide/media/parameter-info.png "сведения о параметрах")

## <a name="peek-definition"></a>Показать определение

Наведите указатель мыши на объявление переменной или функции, щелкните правой кнопкой мыши, затем выберите **"Показать определение"** чтобы увидеть встроенное представление его определения, не покидая текущего расположения. Дополнительные сведения см. в разделе [Команда "Показать определение" (ALT+F12)](/visualstudio/ide/how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12).

![C&#43; &#43; Показать определение](../ide/media/vs2015_cpp_peek_definition.png "vs2015_cpp_peek_definition")

##  <a name="f1-help"></a>Справка F1

Поместите курсор на или после любого типа, ключевое слово или функцию и нажмите клавишу **F1** чтобы перейти непосредственно к соответствующей справочном разделе на сайте docs.microsoft.com. **F1** также работает для элементов в списке ошибок и в некоторых диалоговых.

## <a name="class-view"></a>Представление классов

**Представление классов** отображается для поиска набор деревьев все символы кода и их иерархий область "и" родители потомки, организации на основе отдельных проектов. Можно настроить новые **представление классов** отображает из **окно классов: параметры** (значок с шестеренкой поле в верхней части окна).

![Представление в языке C классов&#43;&#43;](../ide/media/class-view.png "представление классов")

## <a name="generate-graph-of-include-files"></a>Создать диаграмму включаемых файлов

Щелкните правой кнопкой мыши файл кода в проекте и выберите **Создать диаграмму включаемых файлов** для просмотра диаграммы файлов, которые являются включаемыми (из других файлов).

![C&#43; &#43; диаграмму включаемых файлов](../ide/media/vs2015_cpp_include_graph.png "vs2015_cpp_include_graph")

## <a name="view-call-hierarchy"></a>Просмотр иерархии вызовов

Щелкните правой кнопкой мыши любой вызов функции и просмотрите рекурсивный список всех функций, которые он вызывает, а также все функции, которые вызывают его. Каждую функцию в списке можно развернуть одинаковым образом. Дополнительные сведения см. в разделе [Иерархия вызовов](/visualstudio/ide/reference/call-hierarchy).

![C&#43; &#43; "Иерархия вызовов"](../ide/media/vs2015_cpp_call_hierarchy.png "vs2015_cpp_call_hierarchy")

## <a name="see-also"></a>См. также раздел

[Измените и выполните рефакторинг кода (C++)](writing-and-refactoring-code-cpp.md)</br>
[Перейдите к C++ кода в Visual Studio](navigate-code-cpp.md)</br>
[Совместная работа с динамической общей папки дляC++](live-share-cpp.md)