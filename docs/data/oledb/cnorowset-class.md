---
title: Класс CNoRowset
ms.date: 11/04/2016
f1_keywords:
- ATL.CNoRowset
- ATL::CNoRowset<TAccessor>
- CNoRowset
- ATL.CNoRowset<TAccessor>
- ATL::CNoRowset
helpviewer_keywords:
- CNoRowset class
ms.assetid: 55c6c7a4-9e3a-4775-a2dd-c8b333012fa6
ms.openlocfilehash: 6193e2d461761c53fb05e5c16b3914c56d545173
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62230481"
---
# <a name="cnorowset-class"></a>Класс CNoRowset

Можно использовать в качестве аргумента шаблона (`TRowset`) для [CCommand](../../data/oledb/ccommand-class.md) или [CTable](../../data/oledb/ctable-class.md).

## <a name="syntax"></a>Синтаксис

```cpp
template <class TAccessor = CAccessorBase>
class CNoRowset
```

### <a name="parameters"></a>Параметры

*TAccessor*<br/>
Класс, метод доступа. Значение по умолчанию — `CAccessorBase`.

## <a name="remarks"></a>Примечания

Используйте `CNoRowset` как аргумент шаблона, если команда не возвращает набор строк.

`CNoRowset` реализует следующие методы-заглушки, каждый из которых соответствуют другим методам класса метода доступа:

- `BindFinished` — Указывает, когда привязка завершена (возвращает `S_OK`).

- `Close` -Освобождает строки и текущий интерфейс IRowset.

- `GetIID` — Извлекает идентификатор интерфейса точки подключения.

- `GetInterface` — Извлекает интерфейс.

- `GetInterfacePtr` — Извлекает инкапсулированный указатель на интерфейс.

- `SetAccessor` — Задает указатель метода доступа.

- `SetupOptionalRowsetInterfaces` — Устанавливает дополнительные интерфейсы для набора строк.

## <a name="requirements"></a>Требования

**Заголовок:** atldbcli.h

## <a name="see-also"></a>См. также

[Шаблоны потребителей OLE DB](../../data/oledb/ole-db-consumer-templates-cpp.md)<br/>
[Ссылка на шаблоны объекта-получателя OLE DB](../../data/oledb/ole-db-consumer-templates-reference.md)