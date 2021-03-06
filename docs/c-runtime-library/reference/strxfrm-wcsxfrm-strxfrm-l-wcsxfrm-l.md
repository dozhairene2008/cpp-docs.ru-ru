---
title: strxfrm, wcsxfrm, _strxfrm_l, _wcsxfrm_l
ms.date: 11/04/2016
api_name:
- strxfrm
- _wcsxfrm_l
- _strxfrm_l
- wcsxfrm
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
- api-ms-win-crt-string-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- strxfrm
- _tcsxfrm
- wcsxfrm
helpviewer_keywords:
- strxfrm_l function
- _tcsxfrm function
- _strxfrm_l function
- strxfrm function
- wcsxfrm_l function
- wcsxfrm function
- string comparison [C++], transforming strings
- tcsxfrm function
- strings [C++], comparing locale
- _wcsxfrm_l function
ms.assetid: 6ba8e1f6-4484-49aa-83b8-bc2373187d9e
ms.openlocfilehash: 411fe3a5a6f66614f0a22e0f623b73685a6e0844
ms.sourcegitcommit: f19474151276d47da77cdfd20df53128fdcc3ea7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2019
ms.locfileid: "70957607"
---
# <a name="strxfrm-wcsxfrm-_strxfrm_l-_wcsxfrm_l"></a>strxfrm, wcsxfrm, _strxfrm_l, _wcsxfrm_l

Преобразует строку на основе данных языкового стандарта.

## <a name="syntax"></a>Синтаксис

```C
size_t strxfrm(
   char *strDest,
   const char *strSource,
   size_t count
);
size_t wcsxfrm(
   wchar_t *strDest,
   const wchar_t *strSource,
   size_t count
);
size_t _strxfrm_l(
   char *strDest,
   const char *strSource,
   size_t count,
   _locale_t locale
);
size_t wcsxfrm_l(
   wchar_t *strDest,
   const wchar_t *strSource,
   size_t count,
   _locale_t locale
);
```

### <a name="parameters"></a>Параметры

*стрдест*<br/>
Конечная строка.

*стрсаурце*<br/>
Исходная строка.

*count*<br/>
Максимальное число символов для размещения в *стрдест*.

*locale*<br/>
Используемый языковой стандарт.

## <a name="return-value"></a>Возвращаемое значение

Возвращает длину преобразованной строки, не считая завершающий нуль-символ. Если возвращаемое значение больше или равно *Count*, содержимое *стрдест* является непредсказуемым. При возникновении ошибки каждая **функция устанавливает значение** , а возвращает **INT_MAX**. Для недопустимого символа параметру « **еилсек**» присваивается значение « **ошибка».**

## <a name="remarks"></a>Примечания

Функция **стрксфрм** преобразует строку, на которую указывает *стрсаурце* , в новую форму с сортировкой, которая хранится в *стрдест*. Не более, чем *количество* символов, включая символ null, преобразуются и помещаются в результирующую строку. Преобразование выполняется с помощью настройки категории **LC_COLLATE** языкового стандарта. Дополнительные сведения о **LC_COLLATE**см. в разделе [setlocale](setlocale-wsetlocale.md). **стрксфрм** использует текущий языковой стандарт для поведения, зависящего от языкового стандарта; **_strxfrm_l** является идентичным за исключением того, что использует переданный языковой стандарт вместо текущего языкового стандарта. Для получения дополнительной информации см. [Locale](../../c-runtime-library/locale.md).

После преобразования вызов **strcmp** с двумя преобразованными строками дает результат, идентичный результатам вызова **strcoll** , применяемого к исходным двум строкам. Как и в случае с **strcoll** и **стриколл**, **стрксфрм** автоматически обрабатывает строки многобайтовых символов соответствующим образом.

**вксксфрм** — это версия **стрксфрм**для расширенных символов; строковые аргументы **вксксфрм** — это указатели расширенных символов. Для **вксксфрм**после преобразования строки вызов **wcscmp** с двумя преобразованными строками дает результат, идентичный вызову **вксколл** , примененному к исходным двум строкам. в противном случае **вксксфрм** и **стрксфрм** ведут себя одинаково. **вксксфрм** использует текущий языковой стандарт для поведения, зависящего от языкового стандарта; **_wcsxfrm_l** использует переданный языковой стандарт вместо текущего языкового стандарта.

Эти функции проверяют свои параметры. Если *стрсаурце* является пустым указателем, или *стрдест* является **пустым** указателем (если значение Count равно нулю) или *Count* больше **INT_MAX**, вызывается обработчик недопустимых параметров, как описано в разделе [Проверка параметров](../../c-runtime-library/parameter-validation.md) . Если выполнение может быть продолжено, эти функции **устанавливают** значение **еинвал** и возвращают **INT_MAX**.

### <a name="generic-text-routine-mappings"></a>Сопоставления подпрограмм обработки обычного текста

|Подпрограмма TCHAR.H|_UNICODE и _MBCS не определены|_MBCS определено|_UNICODE определено|
|---------------------|------------------------------------|--------------------|-----------------------|
|**_tcsxfrm**|**strxfrm**|**strxfrm**|**wcsxfrm**|
|**_tcsxfrm_l**|**_strxfrm_l**|**_strxfrm_l**|**_wcsxfrm_l**|

В языковом стандарте "C" порядок символов в наборе символов (кодировка ASCII) совпадает с лексикографическим порядком символов. Однако в других языковых стандартах порядок символов в наборе символов может отличаться от лексикографического порядка. Например, в некоторых европейских языковых стандартах символ a (значение 0x61) предшествует символу &\#x00E4; (значение 0xE4) в наборе символов, но ä предшествует символу a лексикографически.

В языковых стандартах, для которых кодировка и порядок символов лексикографическим порядком различаются, используйте **стрксфрм** в исходных строках, а затем **strcmp** в результирующих строках, чтобы получить лексикографическим порядком сравнение строк в соответствии с текущим языковым стандартом Параметр категории **LC_COLLATE** . Таким же для сравнения двух строк, лексикографически в приведенном выше языковом стандарте, используйте **стрксфрм** для исходных строк, а затем **strcmp** в результирующих строках. Кроме того, для исходных строк можно использовать **strcoll** , а не **strcmp** .

**стрксфрм** — это по сути оболочка вокруг [LCMapString завершилось ошибкой](/windows/win32/api/winnls/nf-winnls-lcmapstringw) с **LCMAP_SORTKEY**.

Значение следующего выражения равно размеру массива, необходимого для хранения преобразования **стрксфрм** в исходной строке:

`1 + strxfrm( NULL, string, 0 )`

Только в языковом стандарте "C" **стрксфрм** эквивалентен следующему:

```C
strncpy( _string1, _string2, _count );
return( strlen( _string1 ) );
```

## <a name="requirements"></a>Требования

|Подпрограмма|Обязательный заголовок|
|-------------|---------------------|
|**strxfrm**|\<string.h>|
|**wcsxfrm**|\<string.h> или \<wchar.h>|
|**_strxfrm_l**|\<string.h>|
|**_wcsxfrm_l**|\<string.h> или \<wchar.h>|

Дополнительные сведения о совместимости см. в разделе [Совместимость](../../c-runtime-library/compatibility.md).

## <a name="see-also"></a>См. также

[Преобразование данных](../../c-runtime-library/data-conversion.md)<br/>
[localeconv](localeconv.md)<br/>
[setlocale, _wsetlocale](setlocale-wsetlocale.md)<br/>
[Языковой стандарт](../../c-runtime-library/locale.md)<br/>
[Операции со строками](../../c-runtime-library/string-manipulation-crt.md)<br/>
[Функции strcoll](../../c-runtime-library/strcoll-functions.md)<br/>
[strcmp, wcscmp, _mbscmp](strcmp-wcscmp-mbscmp.md)<br/>
[strncmp, wcsncmp, _mbsncmp, _mbsncmp_l](strncmp-wcsncmp-mbsncmp-mbsncmp-l.md)<br/>
