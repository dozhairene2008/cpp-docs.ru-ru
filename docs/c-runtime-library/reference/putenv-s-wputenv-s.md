---
title: _putenv_s, _wputenv_s
ms.date: 11/04/2016
api_name:
- _wputenv_s
- _putenv_s
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
- api-ms-win-crt-environment-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- putenv_s
- wputenv_s
- _wputenv_s
- _putenv_s
helpviewer_keywords:
- wputenv_s function
- _putenv_s function
- environment variables, deleting
- putenv_s function
- _wputenv_s function
- environment variables, creating
- environment variables, modifying
ms.assetid: fbf51225-a8da-4b9b-9d7c-0b84ef72df18
ms.openlocfilehash: b2de609314a12f626a21680b470bc8831eada2cb
ms.sourcegitcommit: f19474151276d47da77cdfd20df53128fdcc3ea7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2019
ms.locfileid: "70949905"
---
# <a name="_putenv_s-_wputenv_s"></a>_putenv_s, _wputenv_s

Создает, изменяет или удаляет переменные среды. Это версии функций [_putenv, _wputenv](putenv-wputenv.md) с усовершенствованной безопасностью, как описано в разделе [Функции безопасности в CRT](../../c-runtime-library/security-features-in-the-crt.md).

> [!IMPORTANT]
> Этот API нельзя использовать в приложениях, выполняемых в среде выполнения Windows. Дополнительные сведения: [Функции CRT, которые не поддерживаются в приложениях универсальной платформы Windows](../../cppcx/crt-functions-not-supported-in-universal-windows-platform-apps.md).

## <a name="syntax"></a>Синтаксис

```C
errno_t _putenv_s(
   const char *varname,
   const char *value_string
);
errno_t _wputenv_s(
   const wchar_t *varname,
   const wchar_t *value_string
);
```

### <a name="parameters"></a>Параметры

*varname*<br/>
Имя переменной среды.

*value_string*<br/>
Значение, которое будет задано для переменной среды.

## <a name="return-value"></a>Возвращаемое значение

Возвращает 0 в случае успешного выполнения операции или код ошибки.

### <a name="error-conditions"></a>Условия ошибок

|*varname*|*value_string*|Возвращаемое значение|
|------------|-------------|------------------|
|**NULL**|Любое действие|**EINVAL**|
|Любое действие|**NULL**|**EINVAL**|

Если возникает одно из условий ошибки, эти функции вызывают обработчик недопустимого параметра, как описано в разделе [Проверка параметров](../../c-runtime-library/parameter-validation.md). Если выполнение может быть продолжено, эти функции возвращают **еинвал** и применяют **значение "** **еинвал**".

## <a name="remarks"></a>Примечания

Функция **_putenv_s** добавляет новые переменные среды или изменяет значения существующих переменных среды. Переменные среды определяют среду, в которой выполняется процесс (например, путь поиска по умолчанию для библиотек, связываемых с программой). **_wputenv_s** — это версия **_putenv_s**для расширенных символов; Аргумент *енвстринг* для **_wputenv_s** является строкой расширенных символов.

### <a name="generic-text-routine-mappings"></a>Сопоставления подпрограмм обработки обычного текста

|Подпрограмма TCHAR.H|_UNICODE и _MBCS не определены|_MBCS определено|_UNICODE определено|
|---------------------|------------------------------------|--------------------|-----------------------|
|**_tputenv_s**|**_putenv_s**|**_putenv_s**|**_wputenv_s**|

*имя_переменной* — это имя добавляемой или изменяемой переменной среды, а *value_string* — значение переменной. Если *VarName* уже является частью среды, ее значение заменяется на *value_string*; в противном случае в среду добавляются Новая переменная *имя_переменной* и ее *value_string* . Вы можете удалить переменную из среды, указав пустую строку (то есть "") для *value_string*.

**_putenv_s** и **_wputenv_s** влияют только на локальную среду текущего процесса; их нельзя использовать для изменения среды командного уровня. Эти функции работают только в структурах данных, доступных библиотеке времени выполнения, а не в "сегменте" среды, созданном для процесса операционной системой. По завершении текущего процесса среда возвращается на уровень вызывающего процесса; в большинстве случаев это уровень операционной системы. Однако измененная среда может быть передана в любые новые процессы, созданные **_spawn**, **_exec**или **System**, и эти новые процессы получают новые элементы, добавленные **_putenv_s** и **_wputenv_s**.

Не изменяйте запись в среде напрямую; Вместо этого используйте **_putenv_s** или **_wputenv_s** , чтобы изменить его. В частности, непосредственное освобождение элементов глобального массива **_environ []** может привести к неправильному устранению памяти.

**getenv** и **_putenv_s** используют глобальную переменную **_environ** для доступа к таблице Environment; **_wgetenv** и **_wputenv_s** используют **_wenviron**. **_putenv_s** и **_wputenv_s** могут изменять значение **_environ** и **_wenviron**и таким образом сделать недействительным аргумент *envp* в **Main** и аргумент **_wenvp** для **wmain**. Таким образом, для доступа к сведениям о среде безопаснее использовать **_environ** или **_wenviron** . Дополнительные сведения о взаимосвязи **_putenv_s** и **_wputenv_s** с глобальными переменными см. в разделе [_environ, _wenviron](../../c-runtime-library/environ-wenviron.md).

> [!NOTE]
> Семейства функций **_putenv_s** и **_getenv_s** не являются потокобезопасными. **_getenv_s** может вернуть указатель на строку, тогда как **_putenv_s** изменяет строку и, таким образом, вызывает случайные сбои. Убедитесь, что вызовы этих функций синхронизированы.

## <a name="requirements"></a>Требования

|Подпрограмма|Обязательный заголовок|
|-------------|---------------------|
|**_putenv_s**|\<stdlib.h>|
|**_wputenv_s**|\<stdlib.h> или \<wchar.h>|

Дополнительные сведения о совместимости см. в разделе [Совместимость](../../c-runtime-library/compatibility.md).

## <a name="example"></a>Пример

Пример, демонстрирующий использование **_putenv_s**, см. в разделе [getenv_s, _wgetenv_s](getenv-s-wgetenv-s.md).

## <a name="see-also"></a>См. также

[Управление процессами и средой](../../c-runtime-library/process-and-environment-control.md)<br/>
[getenv, _wgetenv](getenv-wgetenv.md)<br/>
[_searchenv, _wsearchenv](searchenv-wsearchenv.md)<br/>
