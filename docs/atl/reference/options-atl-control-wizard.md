---
title: Параметры, мастер элементов управления ATL
ms.date: 11/04/2016
f1_keywords:
- vc.codewiz.class.atl.control.options
helpviewer_keywords:
- ATL Control Wizard, options
ms.assetid: 4607c51a-992d-433e-9281-919c6f519a3d
ms.openlocfilehash: 25db3995687011de5e9cc0a98506cd26f2f1af0b
ms.sourcegitcommit: fcb48824f9ca24b1f8bd37d647a4d592de1cc925
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/15/2019
ms.locfileid: "69495445"
---
# <a name="options-atl-control-wizard"></a>Параметры, мастер элементов управления ATL

Используйте эту страницу мастера, чтобы определить тип создаваемого элемента управления и уровень поддержки интерфейса, который он содержит.

## <a name="uielement-list"></a>Список элементов пользовательского интерфейса

### <a name="control-type"></a>Тип элемента управления

Тип создаваемого элемента управления.

- **Стандартный элемент управления**: Элемент управления ActiveX.

- **Составной элемент управления**: Элемент управления ActiveX, который может содержать (аналогично диалоговому окну) другие элементы управления ActiveX или элементы управления Windows. Составной элемент управления включает следующие элементы:

  - Шаблон для диалогового окна, реализующего составной элемент управления.

  - Настраиваемый ресурс, реестр, который автоматически регистрирует составной элемент управления при вызове.

  - C++ Класс, реализующий составной элемент управления.

  - COM-интерфейс, предоставляемый составным элементом управления.

  - Тестовая страница HTML, содержащая составной элемент управления.

    По умолчанию этот элемент управления устанавливает [ккомконтролбасе:: m_bWindowOnly](../../atl/reference/ccomcontrolbase-class.md#m_bwindowonly) в значение true, чтобы указать, что это оконный элемент управления. В нем реализована схема приемника. Дополнительные сведения см. в разделе [Поддержка элемента управления DHTML](../../atl/atl-support-for-dhtml-controls.md).

- **Элемент управления DHTML**: Элемент управления DHTML библиотеки ATL определяет пользовательский интерфейс с помощью HTML. Класс пользовательского интерфейса DHTML содержит карту COM. По умолчанию этот элемент управления устанавливает [ккомконтролбасе:: m_bWindowOnly](../../atl/reference/ccomcontrolbase-class.md#m_bwindowonly) в значение true, чтобы указать, что это оконный элемент управления.

   Дополнительные сведения см. [в разделе Определение элементов проекта элемента управления DHTML](../../atl/identifying-the-elements-of-the-dhtml-control-project.md).

### <a name="minimal-control"></a>Минимальный контроль

Поддерживает только те интерфейсы, которые абсолютно необходимы большинству контейнеров. Можно задать **минимальный контроль** над любыми типами элементов управления: можно создать минимальный стандартный элемент управления, минимальный составной элемент управления или минимальный элемент управления DHTML.

### <a name="aggregation"></a>Статистическая обработка

Добавляет поддержку статистической обработки для создаваемого элемента управления. Дополнительные сведения см. в разделе [агрегирование](../../atl/aggregation.md).

- **Да**: Создайте элемент управления, для которого можно выполнить статистическую обработку.

- **Нет**: Создайте элемент управления, который не может быть агрегирован.

- **Только**: Создайте элемент управления, экземпляр которого можно создать только с помощью агрегата.

### <a name="threading-model"></a>Потоковая модель

Указывает, что потоковая модель, используемая элементом управления.

- **Один**: Элемент управления будет выполняться только в основном потоке COM.

- **Подразделение**: Элемент управления может быть создан в любом контейнере одного потока. По умолчанию.

### <a name="interface"></a>Интерфейс

Тип интерфейса, который этот элемент управления предоставляет контейнеру.

- **Два**: Создает интерфейс, предоставляющий свойства и методы через `IDispatch` и напрямую через VTBL.

- **Пользовательский**: Создает интерфейс, предоставляющий методы непосредственно через VTBL.

   Если выбран вариант **Настраиваемый**, то можно указать, что элемент управления **совместим с автоматизацией**. При выборе **совместимой с автоматизацией**мастер добавляет атрибут [oleautomation](../../windows/oleautomation.md) к интерфейсу в IDL, а интерфейс может быть маршалирован универсальным маршалером в oleaut32. dll. Дополнительные сведения см. в разделе [сведения о маршалировании](/windows/win32/com/marshaling-details) в Windows SDK.

   Кроме того, если выбрать **совместимый с автоматизацией**, все параметры для всех методов в элементе управления должны быть СОВМЕСТИМЫми вариантными.

### <a name="support"></a>Поддержка

Задает дополнительную поддержку для элемента управления.

- **Точки подключения**: Включает точки соединения для объекта, делая класс объекта производным от [иконнектионпоинтконтаинеримпл](../../atl/reference/iconnectionpointcontainerimpl-class.md) и позволяя ему предоставлять исходный интерфейс.

- **Лицензировано**: Добавляет поддержку для элемента управления для [лицензирования](/windows/win32/com/licensing). Лицензированные элементы управления могут размещаться, только если на клиентском компьютере установлена правильная лицензия.

## <a name="see-also"></a>См. также

[Мастер элементов управления ATL](../../atl/reference/atl-control-wizard.md)
