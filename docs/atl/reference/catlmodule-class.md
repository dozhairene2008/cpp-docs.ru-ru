---
title: Класс Катлмодуле
ms.date: 11/04/2016
f1_keywords:
- CAtlModule
- ATLBASE/ATL::CAtlModule
- ATLBASE/ATL::CAtlModule::CAtlModule
- ATLBASE/ATL::CAtlModule::AddCommonRGSReplacements
- ATLBASE/ATL::CAtlModule::AddTermFunc
- ATLBASE/ATL::CAtlModule::GetGITPtr
- ATLBASE/ATL::CAtlModule::GetLockCount
- ATLBASE/ATL::CAtlModule::Lock
- ATLBASE/ATL::CAtlModule::Term
- ATLBASE/ATL::CAtlModule::Unlock
- ATLBASE/ATL::CAtlModule::UpdateRegistryFromResourceD
- ATLBASE/ATL::CAtlModule::UpdateRegistryFromResourceDHelper
- ATLBASE/ATL::CAtlModule::UpdateRegistryFromResourceS
- ATLBASE/ATL::CAtlModule::m_libid
- ATLBASE/ATL::CAtlModule::m_pGIT
helpviewer_keywords:
- CAtlModule class
ms.assetid: 63fe02f1-4c4b-4e7c-ae97-7ad7b4252415
ms.openlocfilehash: 798e94aed3bbd98108866ce0a1810485bd68699b
ms.sourcegitcommit: 7ecd91d8ce18088a956917cdaf3a3565bd128510
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/16/2020
ms.locfileid: "79423426"
---
# <a name="catlmodule-class"></a>Класс Катлмодуле

Этот класс предоставляет методы, используемые несколькими классами модуля ATL.

## <a name="syntax"></a>Синтаксис

```
class ATL_NO_VTABLE CAtlModule : public _ATL_MODULE
```

## <a name="members"></a>Члены

### <a name="public-constructors"></a>Открытые конструкторы

|Имя|Description|
|----------|-----------------|
|[Катлмодуле:: Катлмодуле](#catlmodule)|Конструктор.|
|[Катлмодуле:: ~ Катлмодуле](#dtor)|Деструктор|

### <a name="public-methods"></a>Открытые методы

|Имя|Description|
|----------|-----------------|
|[Катлмодуле:: Аддкоммонргсреплацементс](#addcommonrgsreplacements)|Переопределите этот метод, чтобы добавить параметры в карту замены компонента реестра ATL (регистратор).|
|[Катлмодуле:: Аддтермфунк](#addtermfunc)|Добавляет новую функцию, вызываемую при завершении работы модуля.|
|[Катлмодуле:: Жетгитптр](#getgitptr)|Возвращает указатель на глобальный интерфейс.|
|[Катлмодуле:: Жетлокккаунт](#getlockcount)|Возвращает счетчик блокировок.|
|[Катлмодуле:: Lock](#lock)|Увеличивает счетчик блокировок.|
|[Катлмодуле:: Term](#term)|Освобождает все элементы данных.|
|[Катлмодуле:: Unlock](#unlock)|Уменьшает на единицу счетчик блокировок.|
|[Катлмодуле:: Упдатерегистрифромресаурцед](#updateregistryfromresourced)|Запускает скрипт, содержащийся в указанном ресурсе, для регистрации или отмены регистрации объекта.|
|[Катлмодуле:: Упдатерегистрифромресаурцедхелпер](#updateregistryfromresourcedhelper)|Этот метод вызывается `UpdateRegistryFromResourceD` для выполнения обновления реестра.|
|[Катлмодуле:: Упдатерегистрифромресаурцес](#updateregistryfromresources)|Запускает скрипт, содержащийся в указанном ресурсе, для регистрации или отмены регистрации объекта. Этот метод статически связывается с компонентом реестра ATL.|

### <a name="public-data-members"></a>Открытые элементы данных

|Имя|Description|
|----------|-----------------|
|[Катлмодуле:: m_libid](#m_libid)|Содержит идентификатор GUID текущего модуля.|
|[Катлмодуле:: m_pGIT](#m_pgit)|Указатель на глобальную таблицу интерфейса.|

## <a name="remarks"></a>Remarks

Этот класс используется классом [CAtlDllModuleT](../../atl/reference/catldllmodulet-class.md), классом [CAtlExeModuleT](../../atl/reference/catlexemodulet-class.md)и [классом функция CAtlServiceModuleT](../../atl/reference/catlservicemodulet-class.md) для обеспечения поддержки DLL-приложений, приложений exe и служб Windows соответственно.

Дополнительные сведения о модулях в ATL см. в разделе [Классы модулей ATL](../../atl/atl-module-classes.md).

Этот класс заменяет устаревший [класс CComModule](../../atl/reference/ccommodule-class.md) , используемый в более ранних версиях ATL.

## <a name="inheritance-hierarchy"></a>Иерархия наследования

[_ATL_MODULE](atl-typedefs.md#_atl_module)

`CAtlModule`

## <a name="requirements"></a>Требования

**Заголовок:** atlbase. h

##  <a name="addcommonrgsreplacements"></a>Катлмодуле:: Аддкоммонргсреплацементс

Переопределите этот метод, чтобы добавить параметры в карту замены компонента реестра ATL (регистратор).

```
virtual HRESULT AddCommonRGSReplacements(IRegistrarBase* /* pRegistrar*/) throw() = 0;
```

### <a name="parameters"></a>Параметры

*прегистрар*<br/>
Зарезервировано.

### <a name="return-value"></a>Возвращаемое значение

Возвращает S_OK при успешном выполнении или ошибку HRESULT при сбое.

### <a name="remarks"></a>Remarks

Заменяемые параметры позволяют клиенту регистратора указывать данные времени выполнения. Для этого Регистратор сохраняет карту замены, в которую он вводит значения, связанные с заменяемыми параметрами в скрипте. Регистратор делает эти записи во время выполнения.

Дополнительные сведения см. в разделе [Использование заменяемых параметров (препроцессор регистратора)](../../atl/using-replaceable-parameters-the-registrar-s-preprocessor.md) .

##  <a name="addtermfunc"></a>Катлмодуле:: Аддтермфунк

Добавляет новую функцию, вызываемую при завершении работы модуля.

```
HRESULT AddTermFunc(_ATL_TERMFUNC* pFunc, DWORD_PTR dw) throw();
```

### <a name="parameters"></a>Параметры

*pFunc*<br/>
Указатель на функцию, которую необходимо добавить.

*dw*<br/>
Определяемые пользователем данные, передаваемые в функцию.

### <a name="return-value"></a>Возвращаемое значение

Возвращает S_OK при успешном выполнении или ошибку HRESULT при сбое.

##  <a name="catlmodule"></a>Катлмодуле:: Катлмодуле

Конструктор.

```
CAtlModule() throw();
```

### <a name="remarks"></a>Remarks

Инициализирует элементы данных и инициирует критическую секцию вокруг потока модуля.

##  <a name="dtor"></a>Катлмодуле:: ~ Катлмодуле

Деструктор

```
~CAtlModule() throw();
```

### <a name="remarks"></a>Remarks

Освобождает все элементы данных.

##  <a name="getgitptr"></a>Катлмодуле:: Жетгитптр

Получает указатель на глобальную таблицу интерфейса.

```
virtual HRESULT GetGITPtr(IGlobalInterfaceTable** ppGIT) throw();
```

### <a name="parameters"></a>Параметры

*ппгит*<br/>
Указатель на переменную, которая получит указатель на глобальную таблицу интерфейса.

### <a name="return-value"></a>Возвращаемое значение

Возвращает S_OK при успешном выполнении или код ошибки в случае сбоя. E_POINTER возвращается, если *ппгит* равен null.

### <a name="remarks"></a>Remarks

Если объект таблицы глобальных интерфейсов не существует, он создается, а его адрес сохраняется в переменной-члене [катлмодуле:: m_pGIT](#m_pgit).

В отладочных сборках возникнет ошибка утверждения, если *ппгит* равен null или если не удается получить указатель на таблицу глобальных интерфейсов.

Сведения о таблице глобальных интерфейсов см. в разделе [иглобалинтерфацетабле](/windows/win32/api/objidl/nn-objidl-iglobalinterfacetable) .

##  <a name="getlockcount"></a>Катлмодуле:: Жетлокккаунт

Возвращает счетчик блокировок.

```
virtual LONG GetLockCount() throw();
```

### <a name="return-value"></a>Возвращаемое значение

Возвращает счетчик блокировок. Это значение может быть полезно для диагностики и отладки.

##  <a name="lock"></a>Катлмодуле:: Lock

Увеличивает счетчик блокировок.

```
virtual LONG Lock() throw();
```

### <a name="return-value"></a>Возвращаемое значение

Увеличивает счетчик блокировок и возвращает обновленное значение. Это значение может быть полезно для диагностики и отладки.

##  <a name="m_libid"></a>Катлмодуле:: m_libid

Содержит идентификатор GUID текущего модуля.

```
static GUID m_libid;
```

##  <a name="m_pgit"></a>Катлмодуле:: m_pGIT

Указатель на глобальную таблицу интерфейса.

```
IGlobalInterfaceTable* m_pGIT;
```

##  <a name="term"></a>Катлмодуле:: Term

Освобождает все элементы данных.

```
void Term() throw();
```

### <a name="remarks"></a>Remarks

Освобождает все элементы данных. Этот метод вызывается деструктором.

##  <a name="unlock"></a>Катлмодуле:: Unlock

Уменьшает на единицу счетчик блокировок.

```
virtual LONG Unlock() throw();
```

### <a name="return-value"></a>Возвращаемое значение

Уменьшает счетчик блокировок и возвращает обновленное значение. Это значение может быть полезно для диагностики и отладки.

##  <a name="updateregistryfromresourced"></a>Катлмодуле:: Упдатерегистрифромресаурцед

Запускает скрипт, содержащийся в указанном ресурсе, для регистрации или отмены регистрации объекта.

```
HRESULT WINAPI UpdateRegistryFromResourceD(
    UINT nResID,
    BOOL bRegister,
    struct _ATL_REGMAP_ENTRY* pMapEntries = NULL) throw();

HRESULT WINAPI UpdateRegistryFromResourceD(
    LPCTSTR lpszRes,
    BOOL bRegister,
    struct _ATL_REGMAP_ENTRY* pMapEntries = NULL) throw();
```

### <a name="parameters"></a>Параметры

*лпсзрес*<br/>
Имя ресурса.

*нресид*<br/>
Идентификатор ресурса.

*брегистер*<br/>
Значение TRUE, если объект должен быть зарегистрирован; В противном случае — значение FALSE.

*пмапентриес*<br/>
Указатель на заменяющую карту, в которой хранятся значения, связанные с заменяемыми параметрами скрипта. ATL автоматически использует% MODULE%. Сведения об использовании дополнительных заменяемых параметров см. в разделе [катлмодуле:: аддкоммонргсреплацементс](#addcommonrgsreplacements). В противном случае используйте значение NULL по умолчанию.

### <a name="return-value"></a>Возвращаемое значение

Возвращает S_OK при успешном выполнении или ошибку HRESULT при сбое.

### <a name="remarks"></a>Remarks

Запускает скрипт, содержащийся в ресурсе, указанном параметром *лпсзрес или нресид*. Если *брегистер* имеет значение true, этот метод регистрирует объект в системном реестре; в противном случае объект удаляется из реестра.

Статические ссылки на компонент реестра ATL (регистратор) см. в разделе [катлмодуле:: упдатерегистрифромресаурцес](#updateregistryfromresources).

Этот метод вызывает [катлмодуле:: упдатерегистрифромресаурцедхелпер](#updateregistryfromresourcedhelper) и [IRegistrar:: ресаурцеунрегистер](iregistrar-class.md#resourceunregister).

##  <a name="updateregistryfromresourcedhelper"></a>Катлмодуле:: Упдатерегистрифромресаурцедхелпер

Этот метод вызывается `UpdateRegistryFromResourceD` для выполнения обновления реестра.

```
inline HRESULT WINAPI UpdateRegistryFromResourceDHelper(
    LPCOLESTR lpszRes,
    BOOL bRegister,
    struct _ATL_REGMAP_ENTRY* pMapEntries = NULL) throw();
```

### <a name="parameters"></a>Параметры

*лпсзрес*<br/>
Имя ресурса.

*брегистер*<br/>
Указывает, должен ли быть зарегистрирован объект.

*пмапентриес*<br/>
Указатель на заменяющую карту, в которой хранятся значения, связанные с заменяемыми параметрами скрипта. ATL автоматически использует% MODULE%. Сведения об использовании дополнительных заменяемых параметров см. в разделе [катлмодуле:: аддкоммонргсреплацементс](#addcommonrgsreplacements). В противном случае используйте значение NULL по умолчанию.

### <a name="return-value"></a>Возвращаемое значение

Возвращает S_OK при успешном выполнении или ошибку HRESULT при сбое.

### <a name="remarks"></a>Remarks

Этот метод обеспечивает реализацию [катлмодуле:: упдатерегистрифромресаурцед](#updateregistryfromresourced).

##  <a name="updateregistryfromresources"></a>Катлмодуле:: Упдатерегистрифромресаурцес

Запускает скрипт, содержащийся в указанном ресурсе, для регистрации или отмены регистрации объекта. Этот метод статически связывается с компонентом реестра ATL.

```
HRESULT WINAPI UpdateRegistryFromResourceS(
    UINT nResID,
    BOOL bRegister,
    struct _ATL_REGMAP_ENTRY* pMapEntries = NULL) throw();

HRESULT WINAPI UpdateRegistryFromResourceS(
    LPCTSTR lpszRes,
    BOOL bRegister,
    struct _ATL_REGMAP_ENTRY* pMapEntries = NULL) throw();
```

### <a name="parameters"></a>Параметры

*нресид*<br/>
Идентификатор ресурса.

*лпсзрес*<br/>
Имя ресурса.

*брегистер*<br/>
Указывает, должен ли быть зарегистрирован скрипт ресурсов.

*пмапентриес*<br/>
Указатель на заменяющую карту, в которой хранятся значения, связанные с заменяемыми параметрами скрипта. ATL автоматически использует% MODULE%. Сведения об использовании дополнительных заменяемых параметров см. в разделе [катлмодуле:: аддкоммонргсреплацементс](#addcommonrgsreplacements). В противном случае используйте значение NULL по умолчанию.

### <a name="return-value"></a>Возвращаемое значение

Возвращает S_OK при успешном выполнении или ошибку HRESULT при сбое.

### <a name="remarks"></a>Remarks

Аналогично [катлмодуле:: упдатерегистрифромресаурцед](#updateregistryfromresourced) , за исключением `CAtlModule::UpdateRegistryFromResourceS`, создает статическую ссылку на компонент реестра ATL (регистратор).

## <a name="see-also"></a>См. также раздел

[_ATL_MODULE](atl-typedefs.md#_atl_module)<br/>
[Обзор класса](../../atl/atl-class-overview.md)<br/>
[Классы модулей](../../atl/atl-module-classes.md)<br/>
[Компонент реестра (регистратор)](../../atl/atl-registry-component-registrar.md)
