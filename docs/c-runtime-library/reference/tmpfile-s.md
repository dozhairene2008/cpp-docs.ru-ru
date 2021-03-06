---
title: tmpfile_s
ms.date: 11/04/2016
api_name:
- tmpfile_s
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
- api-ms-win-crt-stdio-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- tmpfile_s
helpviewer_keywords:
- temporary files
- tmpfile_s function
- temporary files, creating
ms.assetid: 50879c69-215e-425a-a2a3-8b5467121eae
ms.openlocfilehash: 64107f26fa651739f4d5bdd7521b15d9d458df65
ms.sourcegitcommit: f19474151276d47da77cdfd20df53128fdcc3ea7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2019
ms.locfileid: "70946060"
---
# <a name="tmpfile_s"></a>tmpfile_s

Создает временный файл. Это версия функции [tmpfile](tmpfile.md) с усовершенствованиями системы безопасности, описанными в разделе [Функции безопасности в CRT](../../c-runtime-library/security-features-in-the-crt.md).

## <a name="syntax"></a>Синтаксис

```C
errno_t tmpfile_s(
   FILE** pFilePtr
);
```

### <a name="parameters"></a>Параметры

*пфилептр*<br/>
Адрес указателя для хранения адреса созданного указателя на поток.

## <a name="return-value"></a>Возвращаемое значение

Возвращает 0 в случае успеха или код ошибки в случае неудачи.

### <a name="error-conditions"></a>Условия ошибок

|*пфилептр*|**Возвращаемое значение**|**Содержимое** *пфилептр*|
|----------------|----------------------|---------------------------------|
|**NULL**|**EINVAL**|не изменено|

Если возникает ошибка проверки приведенного выше параметра, вызывается обработчик недопустимого параметра, как описано в разделе [Проверка параметров](../../c-runtime-library/parameter-validation.md). Если выполнение может быть продолжено **, для** параметра **еинвал** устанавливается значение, а для возвращаемого значения — **еинвал**.

## <a name="remarks"></a>Примечания

Функция **tmpfile_s** создает временный файл и помещает указатель на этот поток в аргументе *пфилептр* . Временный файл создается в корневом каталоге. Чтобы создать временный файл в каталоге, отличном от корневого, используйте [tmpnam_s](tmpnam-s-wtmpnam-s.md) или [tempnam](tempnam-wtempnam-tmpnam-wtmpnam.md) в сочетании с [fopen](fopen-wfopen.md).

Если файл не удается открыть, **tmpfile_s** записывает **значение NULL** в параметр *пфилептр* . Этот временный файл автоматически удаляется при закрытии файла, при завершении программы в обычном режиме или при вызове **_rmtmp** , предполагая, что текущий рабочий каталог не изменяется. Временный файл открывается в режиме **w + b** (двоичный для чтения и записи).

Сбой может произойти при попытке более **TMP_MAX_S** (см. stdio). H) вызывает метод с **tmpfile_s**.

## <a name="requirements"></a>Требования

|Подпрограмма|Обязательный заголовок|
|-------------|---------------------|
|**tmpfile_s**|\<stdio.h>|

Дополнительные сведения о совместимости см. в разделе [Совместимость](../../c-runtime-library/compatibility.md).

## <a name="example"></a>Пример

> [!NOTE]
> В этом примере для запуска в Windows могут потребоваться права администратора.

```C
// crt_tmpfile_s.c
// This program uses tmpfile_s to create a
// temporary file, then deletes this file with _rmtmp.
//

#include <stdio.h>

int main( void )
{
   FILE *stream;
   char tempstring[] = "String to be written";
   int  i;
   errno_t err;

   // Create temporary files.
   for( i = 1; i <= 3; i++ )
   {
      err = tmpfile_s(&stream);
      if( err )
         perror( "Could not open new temporary file\n" );
      else
         printf( "Temporary file %d was created\n", i );
   }

   // Remove temporary files.
   printf( "%d temporary files deleted\n", _rmtmp() );
}
```

```Output
Temporary file 1 was created
Temporary file 2 was created
Temporary file 3 was created
3 temporary files deleted
```

## <a name="see-also"></a>См. также

[Потоковый ввод-вывод](../../c-runtime-library/stream-i-o.md)<br/>
[_rmtmp](rmtmp.md)<br/>
[_tempnam, _wtempnam, tmpnam, _wtmpnam](tempnam-wtempnam-tmpnam-wtmpnam.md)<br/>
