---
title: mbsrtowcs
ms.date: 11/04/2016
api_name:
- mbsrtowcs
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
- api-ms-win-crt-convert-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- mbsrtowcs
helpviewer_keywords:
- mbsrtowcs function
ms.assetid: f3a29de8-e36e-425b-a7fa-a258e6d7909d
ms.openlocfilehash: de7b25ea8a520dfe2c9cb26ec8989624b670dcb9
ms.sourcegitcommit: f19474151276d47da77cdfd20df53128fdcc3ea7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2019
ms.locfileid: "70952049"
---
# <a name="mbsrtowcs"></a>mbsrtowcs

Преобразует строку многобайтовых символов в текущем языковом стандарте в соответствующую строку расширенных символов с возможностью перезапуска в середине многобайтового символа. Существует более безопасная версия этой функции; см. раздел [mbsrtowcs_s](mbsrtowcs-s.md).

## <a name="syntax"></a>Синтаксис

```C
size_t mbsrtowcs(
   wchar_t *wcstr,
   const char **mbstr,
   sizeof count,
   mbstate_t *mbstate
);
template <size_t size>
size_t mbsrtowcs(
   wchar_t (&wcstr)[size],
   const char **mbstr,
   sizeof count,
   mbstate_t *mbstate
); // C++ only
```

### <a name="parameters"></a>Параметры

*вкстр*<br/>
Адрес для сохранения результирующей преобразованной строки расширенных символов.

*мбстр*<br/>
Косвенный указатель на расположение преобразуемой строки многобайтовых символов.

*count*<br/>
Максимальное число символов (не байт) для преобразования и хранения в *вкстр*.

*мбстате*<br/>
Указатель на объект состояния преобразования **mbstate_t** . Если это значение является пустым указателем, используется статичный внутренний объект состояния преобразования. Так как внутренний объект **mbstate_t** не является потокобезопасным, рекомендуется всегда передавать собственный параметр *мбстате* .

## <a name="return-value"></a>Возвращаемое значение

Возвращает число успешно преобразованных символов без учета завершающего нуль-символа, если он есть. Возвращает (size_t) (-1), если произошла ошибка, и **устанавливает значение** по еилсек.

## <a name="remarks"></a>Примечания

Функция **мбсртовкс** преобразует строку многобайтовых символов, на которую косвенно указывает *мбстр*, в расширенные символы, хранящиеся в буфере, на который указывает *вкстр*, используя состояние преобразования, содержащееся в *мбстате*. Преобразование продолжится для каждого символа до тех пор, пока не будет обнаружен завершающий нуль-байтовый символ, который не соответствует допустимому символу в текущем языковом стандарте, или пока *количество* символов не будет равно меня. Если **мбсртовкс** встречает многобайтовый нуль-символ ("\ 0") как до, так и после выполнения *Count* , он преобразует его в 16-разрядный завершающий символ NULL и останавливается.

Таким словами, строка расширенных символов в *вкстр* завершается нулем, только если **мбсртовкс** встречает многобайтовый нуль-символ во время преобразования. Если последовательности, на которые указывает *мбстр* и *вкстр* , перекрываются, поведение **мбсртовкс** не определено. на **мбсртовкс** влияет Категория LC_TYPE текущего языкового стандарта.

Функция **мбсртовкс** отличается от [функции mbstowcs, _mbstowcs_l](mbstowcs-mbstowcs-l.md) с ее возможной перезагрузкой. Состояние преобразования хранится в *мбстате* для последующих вызовов тех же или других перезапускаемых функций. При смешанном использовании перезапускаемых и неперезапускаемых функций результаты становятся неопределенными.  Например, приложение должно использовать **мбсрлен** вместо **мбслен**, если последующий вызов **мбсртовкс** используется вместо **функции mbstowcs**.

Если *вкстр* не является пустым указателем, объект указателя, на который указывает *мбстр* , присваивает указатель null, если преобразование остановлено из-за того, что был достигнут завершающий символ null. В противном случае ему назначается адрес позиции, следующей за последним преобразованным многобайтовым символом, если таковая имеется. Это позволяет продолжить преобразование с того же места при последующем вызове функции.

Если аргумент *вкстр* является пустым указателем, аргумент *Count* игнорируется, а **мбсртовкс** возвращает необходимый размер в расширенных символах для целевой строки. Если *мбстате* является пустым указателем, функция использует объект состояния статического внутреннего **mbstate_t** преобразования, не являющийся потокобезопасным. Если последовательность символов *мбстр* не имеет соответствующего представления многобайтового символа, возвращается значение-1, **а для свойства переводит значение** **еилсек**.

Если *мбстр* ISA-указатель null, вызывается обработчик недопустимых параметров, как описано в разделе [Проверка параметров](../../c-runtime-library/parameter-validation.md). Если выполнение может быть продолжено, эта функция **устанавливает** **еинвал** и возвращает-1.

В C++ эта функция имеет шаблонную перегрузку, которая вызывает более новые и безопасные аналоги этой функции. Дополнительные сведения см. в разделе [Secure Template Overloads](../../c-runtime-library/secure-template-overloads.md).

## <a name="exceptions"></a>Исключения

Функция **мбсртовкс** является потокобезопасной, если ни одна из функций в текущем потоке не вызывает **setlocale** , если эта функция выполняется, а аргумент *мбстате* не является пустым указателем.

## <a name="requirements"></a>Требования

|Подпрограмма|Обязательный заголовок|
|-------------|---------------------|
|**mbsrtowcs**|\<wchar.h>|

## <a name="see-also"></a>См. также

[Преобразование данных](../../c-runtime-library/data-conversion.md)<br/>
[Языковой стандарт](../../c-runtime-library/locale.md)<br/>
[Интерпретация последовательностей многобайтовых символов](../../c-runtime-library/interpretation-of-multibyte-character-sequences.md)<br/>
[mbrtowc](mbrtowc.md)<br/>
[mbtowc, _mbtowc_l](mbtowc-mbtowc-l.md)<br/>
[mbstowcs, _mbstowcs_l](mbstowcs-mbstowcs-l.md)<br/>
[mbsinit](mbsinit.md)<br/>
