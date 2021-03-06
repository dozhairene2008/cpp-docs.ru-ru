---
title: Макросы схемы объектов
ms.date: 11/04/2016
f1_keywords:
- atlcom/ATL::DECLARE_OBJECT_DESCRIPTION
- atlcom/ATL::OBJECT_ENTRY_AUTO
- atlcom/ATL::OBJECT_ENTRY_NON_CREATEABLE_EX_AUTO
ms.assetid: 680087f4-9894-41dd-a79c-6f337e1f13c1
ms.openlocfilehash: 73dc924527bac8499adefab3d0d6b51afa500a5a
ms.sourcegitcommit: 7ecd91d8ce18088a956917cdaf3a3565bd128510
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/16/2020
ms.locfileid: "79423024"
---
# <a name="object-map-macros"></a>Макросы схемы объектов

Эти макросы определяют сопоставления объектов и записи.

|||
|-|-|
|[DECLARE_OBJECT_DESCRIPTION](#declare_object_description)|Позволяет указать текстовое описание объекта класса, которое будет введено в карту объектов.|
|[OBJECT_ENTRY_AUTO](#object_entry_auto)|Вводит объект ATL в карту объектов, обновляет реестр и создает экземпляр объекта.|
|[OBJECT_ENTRY_NON_CREATEABLE_EX_AUTO](#object_entry_non_createable_ex_auto)|Позволяет указать, что объект должен быть зарегистрирован и инициализирован, но не должен создаваться внешне через `CoCreateInstance`.|

## <a name="requirements"></a>Требования

**Заголовок:** атлком. h

##  <a name="declare_object_description"></a>DECLARE_OBJECT_DESCRIPTION

Позволяет указать текстовое описание для объекта класса.

```
DECLARE_OBJECT_DESCRIPTION( x )
```

### <a name="parameters"></a>Параметры

*x*<br/>
окне Описание объекта класса.

### <a name="remarks"></a>Remarks

ATL вводит это описание в карту объектов с помощью макроса [OBJECT_ENTRY_AUTO](#object_entry_auto) .

DECLARE_OBJECT_DESCRIPTION реализует функцию `GetObjectDescription`, которую можно использовать для переопределения метода [CComCoClass:: жетобжектдескриптион](ccomcoclass-class.md#getobjectdescription) .

Функция `GetObjectDescription` вызывается `IComponentRegistrar::GetComponents`. `IComponentRegistrar` — это интерфейс автоматизации, позволяющий регистрировать и отменять регистрацию отдельных компонентов в библиотеке DLL. При создании объекта регистратора компонентов с помощью мастера проектов ATL мастер автоматически реализует интерфейс `IComponentRegistrar`. `IComponentRegistrar` обычно используется сервером транзакций Microsoft Transaction Server.

Дополнительные сведения о мастере проектов ATL см. в статье [Создание проекта ATL](../../atl/reference/creating-an-atl-project.md).

### <a name="example"></a>Пример

[!code-cpp[NVC_ATL_Windowing#123](../../atl/codesnippet/cpp/object-map-macros_1.h)]

##  <a name="object_entry_auto"></a>OBJECT_ENTRY_AUTO

Вводит объект ATL в карту объектов, обновляет реестр и создает экземпляр объекта.

```
OBJECT_ENTRY_AUTO( clsid, class )
```

### <a name="parameters"></a>Параметры

*этому*<br/>
окне Идентификатор CLSID класса COM, реализованного C++ классом с именем *Class*.

*class*<br/>
окне Имя C++ класса, реализующего класс COM, представленный *CLSID*.

### <a name="remarks"></a>Remarks

Макросы записи объекта помещаются в глобальной области видимости в проекте для поддержки регистрации, инициализации и создания класса.

OBJECT_ENTRY_AUTO вводит указатели функций класса Creator и класса Creator фабрики классов `CreateInstance` функции для этого объекта в автоматически созданную карту объектов ATL. При вызове [катлкоммодуле:: регистерсервер](catlcommodule-class.md#registerserver) он обновляет системный реестр для каждого объекта в сопоставлении объектов.

В следующей таблице описывается получение сведений, добавляемых в карту объектов, из класса, заданного вторым параметром для этого макроса.

|Сведения для|Получено из|
|---------------------|-------------------|
|Регистрация COM|[Макросы реестра](../../atl/reference/registry-macros.md)|
|Создание фабрики класса|[Макросы фабрики класса](../../atl/reference/aggregation-and-class-factory-macros.md)|
|Создание экземпляра|[Статистические макросы](../../atl/reference/aggregation-and-class-factory-macros.md)|
|Регистрация категории компонентов|[Макросы категорий](../../atl/reference/category-macros.md)|
|Инициализация и очистка на уровне класса|[обжектмаин](ccomobjectrootex-class.md#objectmain)|

##  <a name="object_entry_non_createable_ex_auto"></a>OBJECT_ENTRY_NON_CREATEABLE_EX_AUTO

Позволяет указать, что объект должен быть зарегистрирован и инициализирован, но не должен создаваться внешне через `CoCreateInstance`.

```
OBJECT_ENTRY_NON_CREATEABLE_EX_AUTO( clsid, class )
```

### <a name="parameters"></a>Параметры

*этому*<br/>
окне Идентификатор CLSID класса COM, реализованного C++ классом с именем *Class*.

*class*<br/>
окне Имя C++ класса, реализующего класс COM, представленный *CLSID*.

### <a name="remarks"></a>Remarks

Макросы записи объекта помещаются в глобальной области видимости в проекте для поддержки регистрации, инициализации и создания класса.

OBJECT_ENTRY_NON_CREATEABLE_EX_AUTO позволяет указать, что объект должен быть зарегистрирован и инициализирован (Дополнительные сведения см. в [OBJECT_ENTRY_AUTO](#object_entry_auto) ), но его нельзя создавать с помощью `CoCreateInstance`.

## <a name="see-also"></a>См. также раздел

[Макросы](../../atl/reference/atl-macros.md)
