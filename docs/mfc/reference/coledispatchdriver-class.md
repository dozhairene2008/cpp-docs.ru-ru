---
title: Класс COleDispatchDriver
ms.date: 11/04/2016
f1_keywords:
- COleDispatchDriver
- AFXDISP/COleDispatchDriver
- AFXDISP/COleDispatchDriver::COleDispatchDriver
- AFXDISP/COleDispatchDriver::AttachDispatch
- AFXDISP/COleDispatchDriver::CreateDispatch
- AFXDISP/COleDispatchDriver::DetachDispatch
- AFXDISP/COleDispatchDriver::GetProperty
- AFXDISP/COleDispatchDriver::InvokeHelper
- AFXDISP/COleDispatchDriver::ReleaseDispatch
- AFXDISP/COleDispatchDriver::SetProperty
- AFXDISP/COleDispatchDriver::m_bAutoRelease
- AFXDISP/COleDispatchDriver::m_lpDispatch
helpviewer_keywords:
- COleDispatchDriver [MFC], COleDispatchDriver
- COleDispatchDriver [MFC], AttachDispatch
- COleDispatchDriver [MFC], CreateDispatch
- COleDispatchDriver [MFC], DetachDispatch
- COleDispatchDriver [MFC], GetProperty
- COleDispatchDriver [MFC], InvokeHelper
- COleDispatchDriver [MFC], ReleaseDispatch
- COleDispatchDriver [MFC], SetProperty
- COleDispatchDriver [MFC], m_bAutoRelease
- COleDispatchDriver [MFC], m_lpDispatch
ms.assetid: 3ed98daf-cdc7-4374-8a0c-cf695a8d3657
ms.openlocfilehash: fa88147b57b0506f7f9ab96d4a5d2f43fdd75458
ms.sourcegitcommit: 7ecd91d8ce18088a956917cdaf3a3565bd128510
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/16/2020
ms.locfileid: "79426633"
---
# <a name="coledispatchdriver-class"></a>Класс COleDispatchDriver

Реализует автоматизацию OLE на стороне клиента.

## <a name="syntax"></a>Синтаксис

```
class COleDispatchDriver
```

## <a name="members"></a>Члены

### <a name="public-constructors"></a>Открытые конструкторы

|Имя|Description|
|----------|-----------------|
|[COleDispatchDriver:: COleDispatchDriver](#coledispatchdriver)|Формирует объект `COleDispatchDriver`.|

### <a name="public-methods"></a>Открытые методы

|Имя|Description|
|----------|-----------------|
|[COleDispatchDriver:: Аттачдиспатч](#attachdispatch)|Присоединяет `IDispatch`ное соединение к объекту `COleDispatchDriver`.|
|[COleDispatchDriver:: Креатедиспатч](#createdispatch)|Создает подключение `IDispatch` и прикрепляет его к объекту `COleDispatchDriver`.|
|[COleDispatchDriver::D Етачдиспатч](#detachdispatch)|Отсоединяет `IDispatch` подключение, не освобождая его.|
|[COleDispatchDriver:: Property](#getproperty)|Возвращает свойство автоматизации.|
|[COleDispatchDriver:: InvokeHelper](#invokehelper)|Вспомогательное приложение для вызова методов автоматизации.|
|[COleDispatchDriver:: Релеаседиспатч](#releasedispatch)|Освобождает подключение `IDispatch`.|
|[COleDispatchDriver:: SetProperty](#setproperty)|Задает свойство автоматизации.|

### <a name="public-operators"></a>Открытые операторы

|Имя|Description|
|----------|-----------------|
|[COleDispatchDriver:: operator =](#operator_eq)|Копирует исходное значение в объект `COleDispatchDriver`.|
|[COleDispatchDriver:: operator ЛПДИСПАТЧ](#operator_lpdispatch)|Обращается к базовому указателю `IDispatch`.|

### <a name="public-data-members"></a>Открытые элементы данных

|Имя|Description|
|----------|-----------------|
|[COleDispatchDriver:: m_bAutoRelease](#m_bautorelease)|Указывает, следует ли освобождать `IDispatch` во время `ReleaseDispatch` или уничтожения объекта.|
|[COleDispatchDriver:: m_lpDispatch](#m_lpdispatch)|Указывает указатель на интерфейс `IDispatch`, прикрепленный к этому `COleDispatchDriver`.|

## <a name="remarks"></a>Remarks

`COleDispatchDriver` не имеет базового класса.

Интерфейсы диспетчеризации OLE предоставляют доступ к методам и свойствам объекта. Функции-члены `COleDispatchDriver` присоединять, отсоединять, создавать и освобождать подключение диспетчеризации типа `IDispatch`. Другие функции элементов используют списки аргументов переменных для упрощения вызова `IDispatch::Invoke`.

Этот класс можно использовать напрямую, но он обычно используется только классами, созданными мастером добавления классов. При создании новых C++ классов путем импорта библиотеки типов новые классы являются производными от `COleDispatchDriver`.

Дополнительные сведения об использовании `COleDispatchDriver`см. в следующих статьях:

- [Клиенты автоматизации](../../mfc/automation-clients.md)

- [Серверы автоматизации](../../mfc/automation-servers.md)

## <a name="inheritance-hierarchy"></a>Иерархия наследования

`COleDispatchDriver`

## <a name="requirements"></a>Требования

**Заголовок:** afxdisp.h

##  <a name="attachdispatch"></a>COleDispatchDriver:: Аттачдиспатч

Функция-член `AttachDispatch` вызывается для того, чтобы присоединить указатель `IDispatch` к объекту `COleDispatchDriver` . Дополнительные сведения см. в разделе [Implementing the IDispatch Interface](/previous-versions/windows/desktop/automat/implementing-the-idispatch-interface).

```
void AttachDispatch(
    LPDISPATCH lpDispatch,
    BOOL bAutoRelease = TRUE);
```

### <a name="parameters"></a>Параметры

*лпдиспатч*<br/>
Указатель на объект OLE `IDispatch` , который необходимо присоединить к объекту `COleDispatchDriver` .

*бауторелеасе*<br/>
Определяет, следует ли освободить диспетчер, когда этот объект выходит из области действия.

### <a name="remarks"></a>Remarks

Эта функция освобождает все указатели `IDispatch` , которые уже присоединены к объекту `COleDispatchDriver` .

### <a name="example"></a>Пример

[!code-cpp[NVC_MFCOleContainer#3](../../mfc/codesnippet/cpp/coledispatchdriver-class_1.cpp)]

##  <a name="coledispatchdriver"></a>COleDispatchDriver:: COleDispatchDriver

Формирует объект `COleDispatchDriver`.

```
COleDispatchDriver();
COleDispatchDriver(LPDISPATCH lpDispatch, BOOL bAutoRelease = TRUE);
COleDispatchDriver(const COleDispatchDriver& dispatchSrc);
```

### <a name="parameters"></a>Параметры

*лпдиспатч*<br/>
Указатель на объект OLE `IDispatch` , который необходимо присоединить к объекту `COleDispatchDriver` .

*бауторелеасе*<br/>
Определяет, следует ли освободить диспетчер, когда этот объект выходит из области действия.

*диспатчсрк*<br/>
Ссылка на существующий объект `COleDispatchDriver`.

### <a name="remarks"></a>Remarks

Форма `COleDispatchDriver`(`LPDISPATCH lpDispatch`, **BOOL**`bAutoRelease` = **true**) соединяет интерфейс [IDispatch](/previous-versions/windows/desktop/automat/implementing-the-idispatch-interface) .

Форма `COleDispatchDriver`( **const**`COleDispatchDriver`& `dispatchSrc`) копирует существующий объект `COleDispatchDriver` и увеличивает счетчик ссылок.

Форма `COleDispatchDriver`() создает объект `COleDispatchDriver`, но не подключается к интерфейсу `IDispatch`. Перед использованием `COleDispatchDriver`() без аргументов необходимо подключить к нему `IDispatch` с помощью [COleDispatchDriver:: креатедиспатч](#createdispatch) или [COleDispatchDriver:: аттачдиспатч](#attachdispatch). Дополнительные сведения см. в разделе [Implementing the IDispatch Interface](/previous-versions/windows/desktop/automat/implementing-the-idispatch-interface).

### <a name="example"></a>Пример

  См. пример для [COleDispatchDriver::CreateDispatch](#createdispatch).

##  <a name="createdispatch"></a>COleDispatchDriver:: Креатедиспатч

Создает объект интерфейса [IDispatch](/previous-versions/windows/desktop/automat/implementing-the-idispatch-interface) и присоединяет его к объекту `COleDispatchDriver` .

```
BOOL CreateDispatch(
    REFCLSID clsid,
    COleException* pError = NULL);

BOOL CreateDispatch(
    LPCTSTR lpszProgID,
    COleException* pError = NULL);
```

### <a name="parameters"></a>Параметры

*этому*<br/>
Идентификатор класса создаваемого объекта подключения `IDispatch` .

*pError*<br/>
Указатель на объект исключения OLE, который будет содержать код состояния, полученный в результате создания.

*лпсзпрогид*<br/>
Указатель на программный идентификатор, например Excel.Document.5, объекта автоматизации, для которого будет создаваться объект обработки.

### <a name="return-value"></a>Возвращаемое значение

Ненулевое значение, если операция выполнена успешно; в противном случае — значение 0.

### <a name="example"></a>Пример

[!code-cpp[NVC_MFCOleContainer#4](../../mfc/codesnippet/cpp/coledispatchdriver-class_2.cpp)]

##  <a name="detachdispatch"></a>COleDispatchDriver::D Етачдиспатч

Отсоединяет текущее `IDispatch`ное соединение от этого объекта.

```
LPDISPATCH DetachDispatch();
```

### <a name="return-value"></a>Возвращаемое значение

Указатель на ранее присоединенный объект OLE `IDispatch`.

### <a name="remarks"></a>Remarks

`IDispatch` не выпущен.

Дополнительные сведения о типе ЛПДИСПАТЧ см. в разделе [Реализация интерфейса IDispatch](/previous-versions/windows/desktop/automat/implementing-the-idispatch-interface) в Windows SDK.

### <a name="example"></a>Пример

[!code-cpp[NVC_MFCOleContainer#5](../../mfc/codesnippet/cpp/coledispatchdriver-class_3.cpp)]

##  <a name="getproperty"></a>COleDispatchDriver:: Property

Возвращает свойство объекта, заданное параметром *двдиспид*.

```
void GetProperty(
    DISPID dwDispID,
    VARTYPE vtProp,
    void* pvProp) const;
```

### <a name="parameters"></a>Параметры

*двдиспид*<br/>
Определяет извлекаемое свойство.

*втпроп*<br/>
Указывает извлекаемое свойство. Возможные значения см. в подразделе "Примечания" раздела [COleDispatchDriver::InvokeHelper](#invokehelper).

*пвпроп*<br/>
Адрес переменной, которая будет принимать значение свойства. Он должен соответствовать типу, заданному параметром *втпроп*.

### <a name="example"></a>Пример

[!code-cpp[NVC_MFCOleContainer#6](../../mfc/codesnippet/cpp/coledispatchdriver-class_4.cpp)]

##  <a name="invokehelper"></a>COleDispatchDriver:: InvokeHelper

Вызывает метод или свойство объекта, заданное параметром *двдиспид*, в контексте, заданном параметром *вфлагс*.

```
void AFX_CDECL InvokeHelper(
    DISPID dwDispID,
    WORD wFlags,
    VARTYPE vtRet,
    void* pvRet,
    const BYTE* pbParamInfo, ...);
```

### <a name="parameters"></a>Параметры

*двдиспид*<br/>
Задает вызываемый метод или свойство.

*вфлагс*<br/>
Флаги, описывающие контекст вызова `IDispatch::Invoke`. . Список возможных значений см. в описании параметра *вфлагс* в [IDispatch:: Invoke](/windows/win32/api/oaidl/nf-oaidl-idispatch-invoke) в Windows SDK.

*втрет*<br/>
Указывает тип возвращаемого значения. Возможные значения см. в разделе "Примечания".

*пврет*<br/>
Адрес переменной, которая будет принимать значение свойства или возвращаемое значение. Он должен соответствовать типу, заданному параметром *втрет*.

*пбпараминфо*<br/>
Указатель на строку байтов с завершающим нулем, указывающую типы параметров, следующие *пбпараминфо*.

*...*<br/>
Список переменных параметров типов, указанных в *пбпараминфо*.

### <a name="remarks"></a>Remarks

Параметр *пбпараминфо* задает типы параметров, передаваемых методу или свойству. Переменный список аргументов представлен в объявлении синтаксиса как **...** .

Возможные значения для аргумента *втрет* взяты из перечисления VARENUM. Возможны следующие значения:

|Символ|Тип возвращаемых данных|
|------------|-----------------|
|VT_EMPTY|**void**|
|VT_I2|**short**|
|VT_I4|**long**|
|VT_R4|**float**|
|VT_R8|**double**|
|VT_CY|**CY**|
|VT_DATE|**DATE**|
|VT_BSTR|BSTR|
|VT_DISPATCH|лпдиспатч|
|VT_ERROR|SCODE|
|VT_BOOL.|**BOOL**|
|VT_VARIANT|**ЗНАЧЕНИЕ**|
|VT_UNKNOWN|лпункновн|

Аргумент *пбпараминфо* представляет собой разделенный пробелами список констант **VTS_** . Одно или несколько из этих значений, разделенных пробелами (не запятыми), составляют список параметров функции. Список возможных значений можно получить с помощью макроса [EVENT_CUSTOM](event-maps.md#event_custom) .

Эта функция преобразует параметры в значения VARIANTARG, а затем вызывает метод [IDispatch:: Invoke](/windows/win32/api/oaidl/nf-oaidl-idispatch-invoke) . Если вызов `Invoke` завершается сбоем, эта функция создает исключение. Если SCODE (код состояния), возвращенный `IDispatch::Invoke`, имеет DISP_E_EXCEPTION, эта функция создает объект [COleException](../../mfc/reference/coleexception-class.md) ; в противном случае он создает исключение [COleDispatchException](../../mfc/reference/coledispatchexception-class.md).

Дополнительные сведения см. в разделе [VARIANTARG](/windows/win32/api/oaidl/ns-oaidl-variant), [Реализация интерфейса IDispatch](/previous-versions/windows/desktop/automat/implementing-the-idispatch-interface), [IDispatch:: Invoke](/windows/win32/api/oaidl/nf-oaidl-idispatch-invoke)и [структура кодов ошибок COM](/windows/win32/com/structure-of-com-error-codes) в Windows SDK.

### <a name="example"></a>Пример

  См. пример для [COleDispatchDriver::CreateDispatch](#createdispatch).

##  <a name="m_bautorelease"></a>COleDispatchDriver:: m_bAutoRelease

Если значение — TRUE, COM-объект, к которому обращается [m_lpDispatch](#m_lpdispatch) , будет автоматически освобожден при вызове [релеаседиспатч](#releasedispatch) или при уничтожении этого `COleDispatchDriver` объекта.

```
BOOL m_bAutoRelease;
```

### <a name="remarks"></a>Remarks

По умолчанию в конструкторе для `m_bAutoRelease` задано значение TRUE.

Дополнительные сведения об освобождении COM-объектов см. в разделе [Реализация подсчета ссылок](/windows/win32/com/implementing-reference-counting) и [IUnknown:: Release](/windows/win32/api/unknwn/nf-unknwn-iunknown-release) в Windows SDK.

### <a name="example"></a>Пример

[!code-cpp[NVC_MFCOleContainer#9](../../mfc/codesnippet/cpp/coledispatchdriver-class_5.cpp)]

##  <a name="m_lpdispatch"></a>COleDispatchDriver:: m_lpDispatch

Указатель на интерфейс `IDispatch`, прикрепленный к этому `COleDispatchDriver`.

```
LPDISPATCH m_lpDispatch;
```

### <a name="remarks"></a>Remarks

Элемент данных `m_lpDispatch` является открытой переменной типа ЛПДИСПАТЧ.

Дополнительные сведения см. в разделе [IDispatch](/previous-versions/windows/desktop/automat/implementing-the-idispatch-interface) в Windows SDK.

### <a name="example"></a>Пример

  См. пример для [COleDispatchDriver:: аттачдиспатч](#attachdispatch).

##  <a name="operator_eq"></a>COleDispatchDriver:: operator =

Копирует исходное значение в объект `COleDispatchDriver`.

```
const COleDispatchDriver& operator=(const COleDispatchDriver& dispatchSrc);
```

### <a name="parameters"></a>Параметры

*диспатчсрк*<br/>
Указатель на существующий объект `COleDispatchDriver`.

##  <a name="operator_lpdispatch"></a>COleDispatchDriver:: operator ЛПДИСПАТЧ

Обращается к базовому указателю `IDispatch` объекта `COleDispatchDriver`.

```
operator LPDISPATCH();
```

### <a name="example"></a>Пример

[!code-cpp[NVC_MFCOleContainer#8](../../mfc/codesnippet/cpp/coledispatchdriver-class_6.cpp)]

##  <a name="releasedispatch"></a>COleDispatchDriver:: Релеаседиспатч

Освобождает подключение `IDispatch`. Дополнительные сведения см. [в разделе Реализация интерфейса IDispatch](/previous-versions/windows/desktop/automat/implementing-the-idispatch-interface) .

```
void ReleaseDispatch();
```

### <a name="remarks"></a>Remarks

Если для этого соединения задано автоматическое освобождение, эта функция вызывает `IDispatch::Release` перед освобождением интерфейса.

### <a name="example"></a>Пример

  См. пример для [COleDispatchDriver:: аттачдиспатч](#attachdispatch).

##  <a name="setproperty"></a>COleDispatchDriver:: SetProperty

Задает свойство объекта OLE, заданное параметром *двдиспид*.

```
void AFX_CDECL SetProperty(
    DISPID dwDispID,
    VARTYPE vtProp, ...);
```

### <a name="parameters"></a>Параметры

*двдиспид*<br/>
Определяет свойство, которое необходимо задать.

*втпроп*<br/>
Определяет тип свойства, которое необходимо задать. Возможные значения см. в подразделе "Примечания" раздела [COleDispatchDriver::InvokeHelper](#invokehelper).

*...*<br/>
Единственный параметр типа, указанного параметром *втпроп*.

### <a name="example"></a>Пример

[!code-cpp[NVC_MFCOleContainer#7](../../mfc/codesnippet/cpp/coledispatchdriver-class_7.cpp)]

## <a name="see-also"></a>См. также раздел

[Пример CALCDRIV в MFC](../../overview/visual-cpp-samples.md)<br/>
[Пример ACDUAL библиотеки MFC](../../overview/visual-cpp-samples.md)<br/>
[Диаграмма иерархии](../../mfc/hierarchy-chart.md)<br/>
[Класс CCmdTarget](../../mfc/reference/ccmdtarget-class.md)
