---
title: Класс Ккомкомпоситеконтрол
ms.date: 11/04/2016
f1_keywords:
- CComCompositeControl
- ATLCTL/ATL::CComCompositeControl
- ATLCTL/ATL::CComCompositeControl::CComCompositeControl
- ATLCTL/ATL::CComCompositeControl::AdviseSinkMap
- ATLCTL/ATL::CComCompositeControl::CalcExtent
- ATLCTL/ATL::CComCompositeControl::Create
- ATLCTL/ATL::CComCompositeControl::CreateControlWindow
- ATLCTL/ATL::CComCompositeControl::SetBackgroundColorFromAmbient
- ATLCTL/ATL::CComCompositeControl::m_hbrBackground
- ATLCTL/ATL::CComCompositeControl::m_hWndFocus
helpviewer_keywords:
- CComCompositeControl class
- composite controls, CComCompositeControl class
ms.assetid: 1304b931-27e8-4fbc-be8e-bb226ad887fb
ms.openlocfilehash: b57eaf105bfca1a49d53b5e5e99969b0fa2fc82f
ms.sourcegitcommit: 7ecd91d8ce18088a956917cdaf3a3565bd128510
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/16/2020
ms.locfileid: "79423306"
---
# <a name="ccomcompositecontrol-class"></a>Класс Ккомкомпоситеконтрол

Этот класс предоставляет методы, необходимые для реализации составного элемента управления.

> [!IMPORTANT]
>  Этот класс и его члены не могут использоваться в приложениях, выполняемых в среда выполнения Windows.

## <a name="syntax"></a>Синтаксис

```
template <class T>
class CComCompositeControl : public CComControl<T,CAxDialogImpl<T>>
```

#### <a name="parameters"></a>Параметры

*T*<br/>
Класс, производный от [CComObjectRoot](../../atl/reference/ccomobjectroot-class.md) или [CComObjectRootEx](../../atl/reference/ccomobjectrootex-class.md), а также от любых других интерфейсов, которые требуется поддерживать для составного элемента управления.

## <a name="members"></a>Члены

### <a name="public-constructors"></a>Открытые конструкторы

|Имя|Description|
|----------|-----------------|
|[Ккомкомпоситеконтрол:: Ккомкомпоситеконтрол](#ccomcompositecontrol)|Конструктор.|
|[Ккомкомпоситеконтрол:: ~ Ккомкомпоситеконтрол](#dtor)|Деструктор|

### <a name="public-methods"></a>Открытые методы

|Имя|Description|
|----------|-----------------|
|[Ккомкомпоситеконтрол:: Адвисесинкмап](#advisesinkmap)|Вызовите этот метод, чтобы рекомендовать или отменять рекомендации для всех элементов управления, размещенных в составном элементе управления.|
|[Ккомкомпоситеконтрол:: Калцекстент](#calcextent)|Вызовите этот метод, чтобы вычислить размер в HIMETRIC единиц ресурса диалогового окна, используемого для размещения составного элемента управления.|
|[Ккомкомпоситеконтрол:: Create](#create)|Этот метод вызывается для создания окна управления для составного элемента управления.|
|[Ккомкомпоситеконтрол:: Креатеконтролвиндов](#createcontrolwindow)|Вызовите этот метод, чтобы создать окно управления и порекомендовать любой размещенный элемент управления.|
|[Ккомкомпоситеконтрол:: Сетбаккграундколорфромамбиент](#setbackgroundcolorfromambient)|Вызовите этот метод, чтобы задать цвет фона составного элемента управления с помощью фонового цвета контейнера.|

### <a name="public-data-members"></a>Открытые элементы данных

|Имя|Description|
|----------|-----------------|
|[Ккомкомпоситеконтрол:: m_hbrBackground](#m_hbrbackground)|Кисть фона.|
|[Ккомкомпоситеконтрол:: m_hWndFocus](#m_hwndfocus)|Маркер окна, на котором в данный момент находится фокус.|

## <a name="remarks"></a>Remarks

Классы, производные от класса `CComCompositeControl` наследуют функциональные возможности составного элемента управления ActiveX. Элементы управления ActiveX, производные от `CComCompositeControl`, размещаются в стандартном диалоговом окне. Эти типы элементов управления называются составными элементами управления, так как они могут размещать другие элементы управления (собственные элементы управления Windows и элементы управления ActiveX).

`CComCompositeControl` определяет ресурс диалога для использования при создании составного элемента управления путем поиска перечислимого элемента данных в дочернем классе. Элементу Идд этого дочернего класса присваивается идентификатор ресурса диалогового ресурса, который будет использоваться в качестве окна элемента управления. Ниже приведен пример элемента данных, который должен содержать класс, производный от `CComCompositeControl`, для обнаружения ресурса диалогового окна, используемого для окна элемента управления:

[!code-cpp[NVC_ATL_COM#13](../../atl/codesnippet/cpp/ccomcompositecontrol-class_1.h)]

> [!NOTE]
>  Составные элементы управления всегда являются оконными элементами управления, хотя они могут содержать безоконные элементы управления.

Элемент управления, реализованный `CComCompositeControl`производным классом, имеет встроенное поведение табуляции по умолчанию. Когда элемент управления получает фокус с вкладки в содержащем приложении, последовательно нажимая клавишу TAB, можно будет циклически переключаться между всеми содержащимися в нем элементами управления составным элементом управления, затем из составного элемента управления и на следующий элемент в порядок табуляции контейнера. Порядок табуляции размещенных элементов управления определяется ресурсом диалогового окна и определяет порядок, в котором произойдет переход.

> [!NOTE]
>  Чтобы сочетания клавиш работали правильно с `CComCompositeControl`, необходимо загрузить таблицу сочетаний клавиш при создании элемента управления, передать маркер и число ускорителей обратно в [иолеконтролимпл:: жетконтролинфо](../../atl/reference/iolecontrolimpl-class.md#getcontrolinfo)и, наконец, уничтожить таблицу при освобождении элемента управления.

## <a name="example"></a>Пример

[!code-cpp[NVC_ATL_COM#14](../../atl/codesnippet/cpp/ccomcompositecontrol-class_2.h)]

## <a name="inheritance-hierarchy"></a>Иерархия наследования

`WinBase`

[ккомконтролбасе](../../atl/reference/ccomcontrolbase-class.md)

[ккомконтрол](../../atl/reference/ccomcontrol-class.md)

`CComCompositeControl`

## <a name="requirements"></a>Требования

**Заголовок:** атлктл. h

##  <a name="advisesinkmap"></a>Ккомкомпоситеконтрол:: Адвисесинкмап

Вызовите этот метод, чтобы рекомендовать или отменять рекомендации для всех элементов управления, размещенных в составном элементе управления.

```
HRESULT AdviseSinkMap(bool bAdvise);
```

### <a name="parameters"></a>Параметры

*бадвисе*<br/>
Значение true, если должны быть рекомендованы все элементы управления; в противном случае — false.

### <a name="return-value"></a>Возвращаемое значение

|||
|-|-|
|S_OK  |Все элементы управления на карте приемника событий были успешно подключены или отключены от источника событий.|
|E_FAIL  |Не все элементы управления в схеме приемника событий могут быть успешно подключены или отключены от источника событий.|
|E_POINTER  |Эта ошибка обычно указывает на проблему с записью в сопоставлении приемника событий элемента управления или на проблему с аргументом шаблона, используемым в `IDispEventImpl` или `IDispEventSimpleImpl` базовом классе.|
|CONNECT_E_ADVISELIMIT  |Достигнут лимит подключений для точки подключения. Больше подключений она принять не может.|
|CONNECT_E_CANNOTCONNECT  |Приемник не поддерживает интерфейс, необходимый для этой точки подключения.|
|CONNECT_E_NOCONNECTION  |Значение cookie не представляет допустимое соединение. Эта ошибка обычно указывает на проблему с записью в сопоставлении приемника событий элемента управления или на проблему с аргументом шаблона, используемым в `IDispEventImpl` или `IDispEventSimpleImpl` базовом классе.|

### <a name="remarks"></a>Remarks

Базовая реализация этого метода выполняет поиск по записям в карте приемника событий. Затем он рекомендует или отменяет уведомления точек соединения с COM-объектами, описанными в записи приемника схемы событий. Этот метод-член также полагается на тот факт, что производный класс наследуется от одного экземпляра `IDispEventImpl` для каждого элемента управления в схеме приемника, который должен быть рекомендованным или не рекомендованным.

##  <a name="calcextent"></a>Ккомкомпоситеконтрол:: Калцекстент

Вызовите этот метод, чтобы вычислить размер в HIMETRIC единиц ресурса диалогового окна, используемого для размещения составного элемента управления.

```
BOOL CalcExtent(SIZE& size);
```

### <a name="parameters"></a>Параметры

*size*<br/>
Ссылка на структуру `SIZE`, заполняемую этим методом.

### <a name="return-value"></a>Возвращаемое значение

Значение TRUE, если элемент управления размещается в диалоговом окне; в противном случае — FALSE.

### <a name="remarks"></a>Remarks

Размер возвращается в параметре *size* .

##  <a name="create"></a>Ккомкомпоситеконтрол:: Create

Этот метод вызывается для создания окна управления для составного элемента управления.

```
HWND Create(
    HWND hWndParent,
    RECT& /* rcPos */,
    LPARAM dwInitParam = NULL);
```

### <a name="parameters"></a>Параметры

*хвндпарент*<br/>
Маркер родительского окна элемента управления.

*ркпос*<br/>
Зарезервировано.

*двинитпарам*<br/>
Данные, передаваемые в элемент управления во время создания элемента управления. Данные, передаваемые как *двинитпарам* , будут отображаться как параметр LPARAM сообщения [WM_INITDIALOG](/windows/win32/dlgbox/wm-initdialog) , который будет отправляться в составной элемент управления при создании.

### <a name="return-value"></a>Возвращаемое значение

Описатель для вновь созданного диалогового окна составного элемента управления.

### <a name="remarks"></a>Remarks

Этот метод обычно вызывается во время активации элемента управления на месте.

##  <a name="ccomcompositecontrol"></a>Ккомкомпоситеконтрол:: Ккомкомпоситеконтрол

Конструктор.

```
CComCompositeControl();
```

### <a name="remarks"></a>Remarks

Инициализирует элементы данных [ккомкомпоситеконтрол:: m_hbrBackground](#m_hbrbackground) и [ккомкомпоситеконтрол:: m_hWndFocus](#m_hwndfocus) значением NULL.

##  <a name="dtor"></a>Ккомкомпоситеконтрол:: ~ Ккомкомпоситеконтрол

Деструктор

```
~CComCompositeControl();
```

### <a name="remarks"></a>Remarks

Удаляет фоновый объект, если он существует.

##  <a name="createcontrolwindow"></a>Ккомкомпоситеконтрол:: Креатеконтролвиндов

Вызовите этот метод, чтобы создать окно управления и порекомендовать все размещенные элементы управления.

```
virtual HWND CreateControlWindow(
    HWND hWndParent,
    RECT& rcPos);
```

### <a name="parameters"></a>Параметры

*хвндпарент*<br/>
Маркер родительского окна элемента управления.

*ркпос*<br/>
Прямоугольник положения составного элемента управления в координатах клиента относительно *хвндпарент*.

### <a name="return-value"></a>Возвращаемое значение

Возвращает маркер для вновь созданного диалогового окна составного элемента управления.

### <a name="remarks"></a>Remarks

Этот метод вызывает [ккомкомпоситеконтрол:: Create](#create) и [Ккомкомпоситеконтрол:: адвисесинкмап](#advisesinkmap).

##  <a name="m_hbrbackground"></a>Ккомкомпоситеконтрол:: m_hbrBackground

Кисть фона.

```
HBRUSH m_hbrBackground;
```

##  <a name="m_hwndfocus"></a>Ккомкомпоситеконтрол:: m_hWndFocus

Маркер окна, на котором в данный момент находится фокус.

```
HWND m_hWndFocus;
```

##  <a name="setbackgroundcolorfromambient"></a>Ккомкомпоситеконтрол:: Сетбаккграундколорфромамбиент

Вызовите этот метод, чтобы задать цвет фона составного элемента управления с помощью фонового цвета контейнера.

```
HRESULT SetBackgroundColorFromAmbient();
```

### <a name="return-value"></a>Возвращаемое значение

Возвращает S_OK при успешном выполнении или ошибку HRESULT при сбое.

## <a name="see-also"></a>См. также раздел

[Класс CComControl](../../atl/reference/ccomcontrol-class.md)<br/>
[Основные сведения о составном элементе управления](../../atl/atl-composite-control-fundamentals.md)<br/>
[Обзор класса](../../atl/atl-class-overview.md)
