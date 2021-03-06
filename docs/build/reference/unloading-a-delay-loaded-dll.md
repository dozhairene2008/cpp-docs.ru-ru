---
title: Выгрузка библиотеки DLL, загруженной с задержкой
ms.date: 11/04/2016
helpviewer_keywords:
- __FUnloadDelayLoadedDLL2
- delayed loading of DLLs, unloading
ms.assetid: 6463bc71-020e-4aff-a4ca-90360411c54e
ms.openlocfilehash: 284a9cb9268c8c794379c6a5468b0f2b9092b7d0
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62317462"
---
# <a name="unloading-a-delay-loaded-dll"></a>Выгрузка библиотеки DLL, загруженной с задержкой

Вспомогательный метод отложенной загрузки, предоставляемая по умолчанию проверяет дескрипторы отложенной загрузки ли указатель и копия исходной таблицы адресов импорта (IAT) в поле pUnloadIAT. Если Да, указатель будет сохраняться в списке, чтобы дескриптора задержки импорта. Это позволяет вспомогательную функцию для поиска библиотеки DLL по имени, чтобы поддерживать выгрузку библиотеки DLL явным образом.

Ниже приведены, связанные с ними структуры и функции для явная выгрузка библиотеки DLL, загружаемых с задержкой.

```cpp
//
// Unload support from delayimp.h
//

// routine definition; takes a pointer to a name to unload

ExternC
BOOL WINAPI
__FUnloadDelayLoadedDLL2(LPCSTR szDll);

// structure definitions for the list of unload records
typedef struct UnloadInfo * PUnloadInfo;
typedef struct UnloadInfo {
    PUnloadInfo     puiNext;
    PCImgDelayDescr pidd;
    } UnloadInfo;

// from delayhlp.cpp
// the default delay load helper places the unloadinfo records in the
// list headed by the following pointer.
ExternC
PUnloadInfo __puiHead;
```

Структура UnloadInfo реализуется с помощью класса C++, использующий **LocalAlloc** и **LocalFree** в реализации своего оператора **новый** и оператор  **Удалить** соответственно. Эти параметры хранятся в стандартных связанного списка с помощью __puiHead как начало списка.

Вызов __FUnloadDelayLoadedDLL будет найти имя вами в список загружаемые DLL (точное совпадение не требуется). Если найден, копия IAT в pUnloadIAT копируется поверх работающей IAT, чтобы восстановить указатели преобразователя библиотеки освобождается с **FreeLibrary**, соответствующий **UnloadInfo** записи не будет связан с список и удаляются и возвращается значение TRUE.

Аргумент функции __FUnloadDelayLoadedDLL2 чувствительно к регистру. Например следует указать:

```cpp
__FUnloadDelayLoadedDLL2("user32.DLL");
```

но не:

```cpp
__FUnloadDelayLoadedDLL2("User32.DLL");.
```

## <a name="see-also"></a>См. также

[Понятие вспомогательной функции](understanding-the-helper-function.md)
