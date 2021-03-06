---
title: Настройка внешнего вида элементов&#39;заголовка
ms.date: 11/04/2016
helpviewer_keywords:
- header controls [MFC], customization of items
- CHeaderCtrl class [MFC], customizing the items
- HDS_ styles
ms.assetid: b1e1e326-ec7d-4dbd-a46f-96a3e2055618
ms.openlocfilehash: 6ce676695d717fcc5d418fe4ed5df91b4f9bca95
ms.sourcegitcommit: fcb48824f9ca24b1f8bd37d647a4d592de1cc925
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/15/2019
ms.locfileid: "69508722"
---
# <a name="customizing-the-header-item39s-appearance"></a>Настройка внешнего вида элементов&#39;заголовка

Установив параметр *двстиле* при первом создании элемента управления "заголовок" ([CHeaderCtrl:: Create](../mfc/reference/cheaderctrl-class.md#create)), можно определить внешний вид и поведение элементов заголовка или самого элемента управления "заголовок".

Ниже приведена выборка стилей, которые можно задать, и их назначение.

- Чтобы элемент заголовка наглядел как кнопка, используйте стиль **HDS_BUTTONS** .

   Используйте этот стиль, если требуется выполнить действия в ответ на щелчок элемента заголовка, например сортировку данных по определенному столбцу, как это делается в Microsoft Outlook.

- Чтобы присвоить элементам заголовка внешний вид «горячего отслеживания» при наведении на них курсора мыши, используйте стиль **HDS_HOTTRACK** .

   В режиме «горячее отслеживание» отображается трехмерная структура, так как указатель проходит над элементом в противном случае плоской панели.

- Чтобы указать, что элемент управления "заголовок" должен быть скрытым, используйте стиль **HDS_HIDDEN** .

   Стиль **HDS_HIDDEN** указывает, что элемент управления "заголовок" предназначен для использования в качестве контейнера данных, а не визуального элемента управления. Этот стиль не скрывает элемент управления автоматически, но вместо этого влияет на поведение `CHeaderCtrl::Layout`. Значение, возвращаемое в качестве элемента *CY* `WINDOWPOS` структуры, будет равно нулю, указывая, что элемент управления не должен быть видимым для пользователя.

Дополнительные сведения об этих свойствах см. в разделе [элементы](/windows/win32/Controls/header-controls) в Windows SDK. Сведения о добавлении элементов в элемент управления "заголовок" см. в разделе [Добавление элементов в элемент управления "заголовок"](../mfc/adding-items-to-the-header-control.md).

## <a name="see-also"></a>См. также

[Использование CHeaderCtrl](../mfc/using-cheaderctrl.md)<br/>
[Элементы управления](../mfc/controls-mfc.md)
