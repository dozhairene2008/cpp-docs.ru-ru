---
title: Элементы ActiveX в MFC. Создание подкласса элемента управления Windows
ms.date: 09/12/2018
f1_keywords:
- precreatewindow
- IsSubclassed
helpviewer_keywords:
- OnDraw method, MFC ActiveX controls
- subclassing
- DoSuperclassPaint method [MFC]
- subclassing Windows controls
- subclassing, Windows controls
- reflected messages, in ActiveX controls
- PreCreateWindow method, overriding
- MFC ActiveX controls [MFC], subclassed controls
- MFC ActiveX controls [MFC], creating
- IsSubclassed method [MFC]
ms.assetid: 3236d4de-401f-49b7-918d-c84559ecc426
ms.openlocfilehash: 7042df6e7b7dc2c9a608470ba7cfc5a9e9f6127a
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62239513"
---
# <a name="mfc-activex-controls-subclassing-a-windows-control"></a>Элементы ActiveX в MFC. Создание подкласса элемента управления Windows

В этой статье описывается процесс создания подклассов общего элемента управления Windows для создания элемента управления ActiveX. Использование подклассов существующих Windows управления — это быстрый способ создать элемент управления ActiveX. Новый элемент управления будет иметь возможности подкласса элемента управления Windows, такие как рисование и отвечать на щелчок мышью. Элементы ActiveX в MFC образец [кнопку](../overview/visual-cpp-samples.md) является примером Создание подкласса элемента управления Windows.

>[!IMPORTANT]
> ActiveX — это устаревшая технология, которая не следует использовать для разработки новых приложений. Дополнительные сведения о современных технологий, заменяющие ActiveX, см. в разделе [элементы управления ActiveX](activex-controls.md).

Подкласс элемента управления Windows выполните следующие задачи:

- [Переопределить IsSubclassedControl и PreCreateWindow этого функции-члены COleControl](#_core_overriding_issubclassedcontrol_and_precreatewindow)

- [Изменить функцию-член OnDraw](#_core_modifying_the_ondraw_member_function)

- [Обрабатывать сообщения элемента управления ActiveX (OCM), отражаются в элемент управления](#_core_handling_reflected_window_messages)

   > [!NOTE]
   > Значительную часть этой работы выполняется автоматически с помощью мастера управления ActiveX при выборе элемента управления, для которого создаются подклассы с помощью **выберите класс родительского окна** стрелку раскрывающегося списка на **параметры управления** страницы.

##  <a name="_core_overriding_issubclassedcontrol_and_precreatewindow"></a> Переопределение IsSubclassedControl и PreCreateWindow

Чтобы переопределить `PreCreateWindow` и `IsSubclassedControl`, добавьте следующие строки кода, чтобы **защищенные** разделе объявления класса элемента управления:

[!code-cpp[NVC_MFC_AxSub#1](../mfc/codesnippet/cpp/mfc-activex-controls-subclassing-a-windows-control_1.h)]

В файле реализации элемента управления (. CPP), добавьте следующие строки кода для реализации переопределенного две функции:

[!code-cpp[NVC_MFC_AxSub#2](../mfc/codesnippet/cpp/mfc-activex-controls-subclassing-a-windows-control_2.cpp)]

Обратите внимание на то, что, в этом примере элемент управления button Windows указывается в `PreCreateWindow`. Тем не менее может быть подклассом все стандартные элементы управления Windows. Дополнительные сведения о стандартных элементов управления Windows, см. в разделе [элементов управления](../mfc/controls-mfc.md).

Когда создание подкласса элемента управления Windows, может потребоваться указать стиль конкретного окна (WS_) или больше флагов стилей (WS_EX_) для использования при создании окна элемента управления. Можно задать значения для этих параметров в `PreCreateWindow` функция-член, изменив `cs.style` и `cs.dwExStyle` структуры поля. Необходимо внести изменения в этих полей с помощью **или** операцию, чтобы сохранить флаги по умолчанию, заданные классом `COleControl`. Например, если элемент управления является создание подкласса элемента управления BUTTON и элемент управления для отображения в виде типа "флажок", вставьте следующую строку кода в реализацию `CSampleCtrl::PreCreateWindow`, перед инструкцией return:

[!code-cpp[NVC_MFC_AxSub#3](../mfc/codesnippet/cpp/mfc-activex-controls-subclassing-a-windows-control_3.cpp)]

Эта операция добавляет флаг стиля BS_CHECKBOX, оставив флагом стиля по умолчанию (WS_CHILD) класса `COleControl` без изменений.

##  <a name="_core_modifying_the_ondraw_member_function"></a> Изменение функции-члена OnDraw

Если вы хотите сохранить внешний вид соответствующего элемента управления Windows, выведенных в подклассы элемент управления `OnDraw` функция-член для элемента управления должен содержать только вызов `DoSuperclassPaint` функция-член, как показано в следующем примере:

[!code-cpp[NVC_MFC_AxSub#4](../mfc/codesnippet/cpp/mfc-activex-controls-subclassing-a-windows-control_4.cpp)]

`DoSuperclassPaint` Функция-член, реализуемый `COleControl`, использует процедуру окна элемента управления Windows для рисования элемента управления в заданном контексте устройства, внутри ограничивающего прямоугольника. Это делает элемент управления видимым даже в том случае, если она не активна.

> [!NOTE]
>  `DoSuperclassPaint` Функция-член будет работать только с помощью этих типов элементов управления, которые позволяют контекста устройства нельзя передать как *wParam* сообщения WM_PAINT. Сюда входят некоторые стандартные элементы управления Windows, таких как полосы ПРОКРУТКИ и BUTTON и все общие элементы управления. Для элементов управления, которые не поддерживают это поведение необходимо будет предоставить собственный код для правильного отображения элемента управления неактивным.

##  <a name="_core_handling_reflected_window_messages"></a> Обработка отраженных сообщений окна

Элементы управления Windows обычно отправляют определенных сообщений окна их родительского окна. Некоторые из этих сообщений, например WM_COMMAND, уведомляют действия пользователем. Другие, например WM_CTLCOLOR, используемых для получения сведений из родительского окна. Обычно элемент управления ActiveX взаимодействует с родительским окном с помощью других средств. Уведомления передаются путем вызова событий (отправка уведомлений о событиях), и сведения о контейнере элемента управления обеспечивается доступ к свойствам окружения контейнера. Так как существует эти методики, контейнеры элементов управления ActiveX не должны обрабатывать все окно сообщения, отправляемые элементом управления.

Чтобы предотвратить получение окно сообщения, отправленные элемент управления Windows, контейнер `COleControl` создает открытое окно, в качестве родительского элемента управления. Этот дополнительный окно, называемое «рефлектор», создается только для элемента управления ActiveX, что подклассы Windows, управления и имеет тот же размер и положение, что окна элемента управления. В окне reflector перехватывает определенных сообщений окна и отправляет их обратно в элемент управления. Элемент управления, в его процедуре окна, затем может обрабатывать эти отраженные сообщения, выполнив действия, соответствующие для элемента управления ActiveX (например, порождая событие). См. в разделе [отражены идентификаторы сообщений окон](../mfc/reflected-window-message-ids.md) список перехваченные windows сообщения и соответствующие им отраженных сообщений.

Контейнер элементов управления ActiveX могут быть созданы для выполнения отражения сообщения, устраняя потребность `COleControl` для создания окна reflector и сокращение времени выполнения затраты для элемент управления Windows. `COleControl` Определяет, поддерживает ли контейнер эту возможность, установив для свойства окружающей среды MessageReflect со значением **TRUE**.

Чтобы обрабатывать сообщения отраженного окна, добавление элемента на карту элементов управления сообщения, а также реализовывать функцию обработчика событий. Поскольку отраженные сообщения не являются частью стандартного набора сообщения, определенные Windows, представление классов не поддерживает добавление таких обработчиков сообщений. Тем не менее это не сложно вручную добавить обработчик.

Чтобы добавить обработчик сообщений для отраженного окна сообщения вручную сделайте следующее:

- В классе элемента управления. H-файл, объявите функцию обработчика событий. Функция должна иметь тип возвращаемого значения **LRESULT** и два параметра, с типами **WPARAM** и **LPARAM**, соответственно. Пример:

   [!code-cpp[NVC_MFC_AxSub#5](../mfc/codesnippet/cpp/mfc-activex-controls-subclassing-a-windows-control_5.h)]
    [!code-cpp[NVC_MFC_AxSub#6](../mfc/codesnippet/cpp/mfc-activex-controls-subclassing-a-windows-control_6.h)]

- В классе элемента управления. CPP добавьте запись ON_MESSAGE к схеме сообщения. Параметры данной записи должен иметь идентификатор сообщения и имя функции обработчика. Пример:

   [!code-cpp[NVC_MFC_AxSub#7](../mfc/codesnippet/cpp/mfc-activex-controls-subclassing-a-windows-control_7.cpp)]

- Кроме того, в. Файл CPP, реализовать `OnOcmCommand` функции-члена для обработки отраженного сообщения. *WParam* и *lParam* параметры являются те же исходного сообщения окна.

Пример того, как отражено обработки сообщений, см. Пример элементов управления ActiveX в MFC [кнопку](../overview/visual-cpp-samples.md). Он демонстрирует `OnOcmCommand` обработчик, который определяет код уведомления BN_CLICKED и отвечает, срабатывание (отправка) `Click` событий.

## <a name="see-also"></a>См. также

[Элементы ActiveX библиотеки MFC](../mfc/mfc-activex-controls.md)
