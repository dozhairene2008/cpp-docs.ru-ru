---
title: _get_terminate
ms.date: 11/04/2016
api_name:
- _get_terminate
api_location:
- msvcrt.dll
- msvcr80.dll
- msvcr90.dll
- msvcr100.dll
- msvcr100_clr0400.dll
- msvcr110.dll
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr120_clr0400.dll
- ucrtbase.dll
- api-ms-win-crt-runtime-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- get_terminate
- _get_terminate
- __get_terminate
helpviewer_keywords:
- __get_terminate function
- get_terminate function
- _get_terminate function
ms.assetid: c8f168c4-0ad5-4832-a522-dd1ef383c208
ms.openlocfilehash: 7a9bfb6f8be1c990b349f14055eb2fe5c409e0d5
ms.sourcegitcommit: f19474151276d47da77cdfd20df53128fdcc3ea7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2019
ms.locfileid: "70955682"
---
# <a name="_get_terminate"></a>_get_terminate

Возвращает подпрограммы завершения, вызываемую методом **Terminate**.

## <a name="syntax"></a>Синтаксис

```C
terminate_function _get_terminate( void );
```

## <a name="return-value"></a>Возвращаемое значение

Возвращает указатель на функцию, зарегистрированную функцией [set_terminate](set-terminate-crt.md). Если функция не задана, возвращаемое значение может использоваться для восстановления поведения по умолчанию; Это значение может быть **равно NULL**.

## <a name="requirements"></a>Требования

|Подпрограмма|Обязательный заголовок|
|-------------|---------------------|
|**_get_terminate**|\<eh.h>|

Дополнительные сведения о совместимости см. в разделе [Совместимость](../../c-runtime-library/compatibility.md).

## <a name="see-also"></a>См. также

[Процедуры обработки исключений](../../c-runtime-library/exception-handling-routines.md)<br/>
[abort](abort.md)<br/>
[set_unexpected](set-unexpected-crt.md)<br/>
[terminate](terminate-crt.md)<br/>
[unexpected](unexpected-crt.md)<br/>
