---
title: Проверка параметров
ms.date: 11/04/2016
helpviewer_keywords:
- parameters, validation
ms.assetid: 019dd5f0-dc61-4d2e-b4e9-b66409ddf1f2
ms.openlocfilehash: 2c7b2ae50fdcbf59cd23cc309a4ddc4c0803e24e
ms.sourcegitcommit: dedd4c3cb28adec3793329018b9163ffddf890a4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/11/2019
ms.locfileid: "57748428"
---
# <a name="parameter-validation"></a>Проверка параметров

Большинство функций повышенной безопасности CRT и многие из существовавших ранее функций проверяют свои параметры. Сюда могут входить: проверка указателей на **NULL**, проверка соответствия целых чисел допустимому диапазону или проверка действительности значений перечисления. При обнаружении недопустимого параметра вызывается обработчик недопустимых параметров.

## <a name="invalid-parameter-handler-routine"></a>Подпрограмма обработчика недопустимых параметров

Когда функция библиотеки среды выполнения C выявляет недопустимый параметр, она фиксирует определенную информацию об ошибке, а затем вызывает макрос, включающий функцию отключения обработчика недопустимых параметров — [_invalid_parameter](../c-runtime-library/reference/invalid-parameter-functions.md), [_invalid_parameter_noinfo](../c-runtime-library/reference/invalid-parameter-functions.md) или [_invalid_parameter_noinfo_noreturn](../c-runtime-library/reference/invalid-parameter-functions.md). Выбор вызываемой функции отключения зависит от того, является ли ваш код отладочной или разовой сборкой, а также от того, считается ли ошибка неустранимой.

В отладочных сборках перед вызовом функции "отключена" макрос обработки недопустимых параметров вызывает утверждение, вызвавшее сбой и точку останова отладчика. При выполнении кода утверждение может быть передано пользователю в диалоговом окне, где в зависимости от операционной системы и версии библиотеки среды выполнения предлагаются параметры "Прервать", "Повторить" и "Продолжить" или аналогичные. Они позволяют пользователю незамедлительно прервать программу, подключить отладчик или разрешить дальнейшее выполнение существующего кода, в случае чего вызывается функция отключения.

Функция отключения обработчика недопустимых параметров, в свою очередь, вызывает назначенный на этот момент обработчик недопустимых параметров. По умолчанию недопустимый параметр вызывает функцию `_invoke_watson`, которая приводит к сбою приложения и, соответственно, к его прерыванию и созданию мини-дампа. Если этот параметр в операционной системе включен, появляется диалоговое окно, в котором пользователю предлагается передать аварийный дамп памяти в корпорацию Майкрософт для анализа.

Это поведение можно изменить с помощью функции [_set_invalid_parameter_handler](../c-runtime-library/reference/set-invalid-parameter-handler-set-thread-local-invalid-parameter-handler.md) или [_set_thread_local_invalid_parameter_handler](../c-runtime-library/reference/set-invalid-parameter-handler-set-thread-local-invalid-parameter-handler.md) и, таким образом, задать обработчик недопустимых параметров для собственной функции. Если указанная вами функция не завершает работу приложения, управление возвращается к функции, которая получила недопустимые параметры. В CRT эти функции обычно прекращают выполнения функций; задайте `errno` как код ошибки и верните код ошибки. Во многих случаях и значение `errno`, и возвращаемое значение представляют собой `EINVAL`, означающий недопустимый параметр. В некоторых случаях возвращается более конкретный код ошибки, например `EBADF`, соответствующий указателю на неправильный файл, переданному как параметр. Дополнительные сведения о параметрах `errno` см. в разделе [errno, _doserrno, _sys_errlist и _sys_nerr](../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md).

## <a name="see-also"></a>См. также

[Функции безопасности в CRT](../c-runtime-library/security-features-in-the-crt.md)<br/>
[Функции библиотеки CRT](../c-runtime-library/crt-library-features.md)
