---
title: Класс Кмапстрингтостринг
ms.date: 11/04/2016
f1_keywords:
- CMapStringToString
- AFXCOLL/CMapStringToString
- AFXCOLL/CMapStringToString::CPair
- AFXCOLL/CMapStringToString::CMapStringToString
- AFXCOLL/CMapStringToString::GetCount
- AFXCOLL/CMapStringToString::GetHashTableSize
- AFXCOLL/CMapStringToString::GetNextAssoc
- AFXCOLL/CMapStringToString::GetSize
- AFXCOLL/CMapStringToString::GetStartPosition
- AFXCOLL/CMapStringToString::HashKey
- AFXCOLL/CMapStringToString::InitHashTable
- AFXCOLL/CMapStringToString::IsEmpty
- AFXCOLL/CMapStringToString::Lookup
- AFXCOLL/CMapStringToString::LookupKey
- AFXCOLL/CMapStringToString::PGetFirstAssoc
- AFXCOLL/CMapStringToString::PGetNextAssoc
- AFXCOLL/CMapStringToString::PLookup
- AFXCOLL/CMapStringToString::RemoveAll
- AFXCOLL/CMapStringToString::RemoveKey
- AFXCOLL/CMapStringToString::SetAt
helpviewer_keywords:
- CMapStringToString [MFC], CPair
- CMapStringToString [MFC], CMapStringToString
- CMapStringToString [MFC], GetCount
- CMapStringToString [MFC], GetHashTableSize
- CMapStringToString [MFC], GetNextAssoc
- CMapStringToString [MFC], GetSize
- CMapStringToString [MFC], GetStartPosition
- CMapStringToString [MFC], HashKey
- CMapStringToString [MFC], InitHashTable
- CMapStringToString [MFC], IsEmpty
- CMapStringToString [MFC], Lookup
- CMapStringToString [MFC], LookupKey
- CMapStringToString [MFC], PGetFirstAssoc
- CMapStringToString [MFC], PGetNextAssoc
- CMapStringToString [MFC], PLookup
- CMapStringToString [MFC], RemoveAll
- CMapStringToString [MFC], RemoveKey
- CMapStringToString [MFC], SetAt
ms.assetid: b45794c2-fe6b-4edb-a8ca-faa03b57b4a8
ms.openlocfilehash: a2ffcf7ce7ee6eccc56382501a5969ddec6c9e22
ms.sourcegitcommit: 63784729604aaf526de21f6c6b62813882af930a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/17/2020
ms.locfileid: "79442591"
---
# <a name="cmapstringtostring-class"></a>Класс Кмапстрингтостринг

Поддерживает сопоставления объектов `CString` , зашифрованных объектами `CString` .

## <a name="syntax"></a>Синтаксис

```
class CMapStringToString : public CObject
```

## <a name="members"></a>Члены

Функции элементов `CMapStringToString` похожи на функции членов класса [кмапстрингтуб](../../mfc/reference/cmapstringtoob-class.md). Из-за этой схожести для изучения этой функции-члена можно использовать справочную документацию по классу `CMapStringToOb`. Когда вы видите `CObject` указатель в качестве возвращаемого значения или параметра функции Output, замените указатель на **char**. Когда вы видите `CObject` указатель в качестве параметра функции ввода, замените указатель на **char**.

`BOOL CMapStringToString::Lookup(LPCTSTR<key>, CString&<rValue>) const;`

, например, преобразуется в

`BOOL CMapStringToOb::Lookup(const char*<key>, CObject*&<rValue>) const;`

### <a name="public-structures"></a>Открытые структуры

|Имя|Description|
|----------|-----------------|
|[Кмапстрингтостринг:: Кпаир](#cpair)|Вложенная структура, содержащая значение ключа и значение связанного объекта String.|

### <a name="public-constructors"></a>Открытые конструкторы

|Имя|Description|
|----------|-----------------|
|[Кмапстрингтостринг:: Кмапстрингтостринг](../../mfc/reference/cmapstringtoob-class.md#cmapstringtoob)|Конструктор.|

### <a name="public-methods"></a>Открытые методы

|Имя|Description|
|----------|-----------------|
|[Кмапстрингтостринг:: NOCOUNT](../../mfc/reference/cmapstringtoob-class.md#getcount)|Возвращает число элементов в этой карте.|
|[Кмапстрингтостринг:: Жесаштаблесизе](../../mfc/reference/cmapstringtoob-class.md#gethashtablesize)|Определяет текущее количество элементов в хэш-таблице.|
|[Кмапстрингтостринг:: Жетнекстассок](../../mfc/reference/cmapstringtoob-class.md#getnextassoc)|Возвращает следующий элемент для итерации.|
|[Кмапстрингтостринг:: DataSize](../../mfc/reference/cmapstringtoob-class.md#getsize)|Возвращает число элементов в этой карте.|
|[Кмапстрингтостринг:: Жетстартпоситион](../../mfc/reference/cmapstringtoob-class.md#getstartposition)|Возвращает расположение первого элемента.|
|[Кмапстрингтостринг:: Хашкэй](../../mfc/reference/cmapstringtoob-class.md#hashkey)|Вычисляет хэш-значение указанного ключа.|
|[Кмапстрингтостринг:: Инисаштабле](../../mfc/reference/cmapstringtoob-class.md#inithashtable)|Инициализирует хэш-таблицу.|
|[Кмапстрингтостринг:: IsEmpty](../../mfc/reference/cmapstringtoob-class.md#isempty)|Проверяет условие на пустую карту (нет элементов).|
|[Кмапстрингтостринг:: Lookup](../../mfc/reference/cmapstringtoob-class.md#lookup)|Ищет указатель void на основе ключа указателя void. Значение указателя, а не сущность, на которое он указывает, используется для сравнения ключей.|
|[Кмапстрингтостринг:: LookupKey](../../mfc/reference/cmapstringtoob-class.md#lookupkey)|Возвращает ссылку на ключ, связанный с указанным значением ключа.|
|[Кмапстрингтостринг::P Жетфирстассок](#pgetfirstassoc)|Возвращает указатель на первый `CString` в сопоставлении.|
|[Кмапстрингтостринг::P Жетнекстассок](#pgetnextassoc)|Возвращает указатель на следующее `CString` для итерации.|
|[Кмапстрингтостринг::P Поиск](#plookup)|Возвращает указатель на `CString`, значение которого соответствует указанному значению.|
|[Кмапстрингтостринг:: RemoveAll](../../mfc/reference/cmapstringtoob-class.md#removeall)|Удаляет все элементы из этой схемы.|
|[Кмапстрингтостринг:: Ремовекэй](../../mfc/reference/cmapstringtoob-class.md#removekey)|Удаляет элемент, указанный ключом.|
|[Кмапстрингтостринг:: SetAt](../../mfc/reference/cmapstringtoob-class.md#setat)|Вставляет элемент в карту; заменяет существующий элемент, если найден соответствующий ключ.|

### <a name="public-operators"></a>Открытые операторы

|Имя|Description|
|----------|-----------------|
|[Кмапстрингтостринг:: operator \[ \]](../../mfc/reference/cmapstringtoob-class.md#operator_at)|Вставляет элемент в Map — подстановку оператора для `SetAt`.|

## <a name="remarks"></a>Remarks

`CMapStringToString` использует макрос `IMPLEMENT_SERIAL` для поддержки сериализации и записи элементов в дамп. Каждый элемент сериализуется в свою очередь, если схема хранится в архиве с помощью перегруженного оператора вставки ( **<<** ) или с помощью функции-члена `Serialize`.

Если требуется дамп отдельных `CString`- `CString` элементов, необходимо установить глубину контекста дампа в 1 или более.

При удалении объекта `CMapStringToString` или при удалении его элементов `CString` объекты удаляются соответствующим образом.

Дополнительные сведения о `CMapStringToString`см. в статье [коллекции](../../mfc/collections.md)статей.

## <a name="inheritance-hierarchy"></a>Иерархия наследования

[CObject](../../mfc/reference/cobject-class.md)

`CMapStringToString`

## <a name="requirements"></a>Требования

**Заголовок:** афксколл. h

##  <a name="cpair"></a>Кмапстрингтостринг:: Кпаир

Содержит значение ключа и значение связанного строкового объекта.

### <a name="remarks"></a>Remarks

Это вложенная структура в классе [кмапстрингтостринг](../../mfc/reference/cmapstringtostring-class.md).

Структура состоит из двух полей:

- `key` фактическое значение типа ключа.

- `value` значение связанного объекта.

Он используется для хранения возвращаемых значений из [кмапстрингтостринг::P Lookup](#plookup), [Кмапстрингтостринг::P жетфирстассок](#pgetfirstassoc)и [кмапстрингтостринг::P жетнекстассок](#pgetnextassoc).

### <a name="example"></a>Пример

  Пример использования см. в примере для [кмапстрингтостринг::P Lookup](#plookup).

##  <a name="pgetfirstassoc"></a>Кмапстрингтостринг::P Жетфирстассок

Возвращает первую запись объекта Map.

```
const CPair* PGetFirstAssoc() const;

CPair* PGetFirstAssoc();
```

### <a name="return-value"></a>Возвращаемое значение

Указатель на первую запись в сопоставлении; см. раздел [кмапстрингтостринг:: кпаир](#cpair). Если схема пуста, значение равно NULL.

### <a name="remarks"></a>Remarks

Вызовите эту функцию, чтобы вернуть указатель на первый элемент в объекте Map.

### <a name="example"></a>Пример

[!code-cpp[NVC_MFCCollections#73](../../mfc/codesnippet/cpp/cmapstringtostring-class_1.cpp)]

##  <a name="pgetnextassoc"></a>Кмапстрингтостринг::P Жетнекстассок

Извлекает элемент Map, на который указывает *пассокрек*.

```
const CPair *PGetNextAssoc(const CPair* pAssoc) const;

CPair *PGetNextAssoc(const CPair* pAssoc);
```

### <a name="parameters"></a>Параметры

*пассок*<br/>
Указывает на запись Map, возвращенную предыдущим вызовом [пжетнекстассок](#pgetnextassoc) или [пжетфирстассок](#pgetfirstassoc) .

### <a name="return-value"></a>Возвращаемое значение

Указатель на следующую запись в сопоставлении; см. раздел [кмапстрингтостринг:: кпаир](#cpair). Если элемент является последним в сопоставлении, значение равно NULL.

### <a name="remarks"></a>Remarks

Вызовите этот метод, чтобы выполнить итерацию всех элементов в сопоставлении. Извлеките первый элемент с помощью вызова `PGetFirstAssoc`, а затем последовательно выполняйте последовательные вызовы к `PGetNextAssoc`.

### <a name="example"></a>Пример

  См. пример для [кмапстрингтостринг::P жетфирстассок](#pgetfirstassoc).

##  <a name="plookup"></a>Кмапстрингтостринг::P Поиск

Выполняет поиск значения, сопоставленного с заданным ключом.

```
const CPair* PLookup(LPCTSTR key) const;

CPair* PLookup(LPCTSTR key);
```

### <a name="parameters"></a>Параметры

*key*<br/>
Указатель на ключ для искомого элемента.

### <a name="return-value"></a>Возвращаемое значение

Указатель на указанный ключ.

### <a name="remarks"></a>Remarks

Вызовите этот метод, чтобы найти элемент Map с ключом, который точно соответствует заданному ключу.

### <a name="example"></a>Пример

[!code-cpp[NVC_MFCCollections#74](../../mfc/codesnippet/cpp/cmapstringtostring-class_2.cpp)]

## <a name="see-also"></a>См. также раздел

[Пример СОБРАНий MFC](../../overview/visual-cpp-samples.md)<br/>
[Класс CObject](../../mfc/reference/cobject-class.md)<br/>
[Диаграмма иерархии](../../mfc/hierarchy-chart.md)
