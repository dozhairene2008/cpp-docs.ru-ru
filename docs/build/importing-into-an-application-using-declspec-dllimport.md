---
title: Импорт в приложение с помощью __declspec(dllimport)
ms.date: 11/04/2016
helpviewer_keywords:
- __declspec(dllimport) keyword [C++]
- importing DLLs [C++], __declspec(dllimport)
ms.assetid: edb4da4e-f83a-44cf-a668-9239d49dbe42
ms.openlocfilehash: fd7d42ec5a76b92aa789a3a20f38e6b2c0fd2cb1
ms.sourcegitcommit: 63784729604aaf526de21f6c6b62813882af930a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/17/2020
ms.locfileid: "79440410"
---
# <a name="import-into-an-application-using-__declspecdllimport"></a>Импорт в приложение с помощью __declspec(dllimport)

Программа, использующая открытые символы, определенные библиотекой DLL, называется их импортом. При создании файлов заголовков для приложений, использующих библиотеки DLL для построения, используйте **__declspec (dllimport)** в объявлениях открытых символов. Ключевое слово **__declspec (dllimport)** работает независимо от того, экспортируются ли они с помощью DEF-файлов или с помощью ключевого слова **__declspec (dllexport)** .

Чтобы сделать код более удобочитаемым, определите макрос для **__declspec (dllimport)** , а затем используйте макрос для объявления каждого импортированного символа:

```
#define DllImport   __declspec( dllimport )

DllImport int  j;
DllImport void func();
```

Использование **__declspec (dllimport)** является необязательным в объявлениях функций, но при использовании этого ключевого слова компилятор создает более эффективный код. Однако необходимо использовать **__declspec (dllimport)** для импортируемого исполняемого файла, чтобы получить доступ к открытым символам и объектам данных библиотеки DLL. Обратите внимание, что пользователям библиотеки DLL по-прежнему необходимо связываться с библиотекой импорта.

Вы можете использовать один и тот же заголовочный файл как для библиотеки DLL, так и для клиентского приложения. Для этого используйте специальный символ препроцессора, который указывает, выполняется ли сборка библиотеки DLL или сборка клиентского приложения. Пример:

```
#ifdef _EXPORTING
   #define CLASS_DECLSPEC    __declspec(dllexport)
#else
   #define CLASS_DECLSPEC    __declspec(dllimport)
#endif

class CLASS_DECLSPEC CExampleA : public CObject
{ ... class definition ... };
```

## <a name="what-do-you-want-to-do"></a>Выбор действия

- [Инициализация библиотеки DLL](run-time-library-behavior.md#initializing-a-dll)

## <a name="what-do-you-want-to-know-more-about"></a>Дополнительные сведения

- [Импорт и экспорт встраиваемых функций](importing-and-exporting-inline-functions.md)

- [Взаимный импорт](mutual-imports.md)

## <a name="see-also"></a>См. также раздел

[Импорт в приложение](importing-into-an-application.md)
