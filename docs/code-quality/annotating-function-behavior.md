---
title: Аннотирование поведения функции
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- _On_failure_
- _Return_type_success_
- _Always_
- _Maybe_raises_SEH_exception_
- _Raises_SEH_exception_
- _Called_from_function_class_
- _Function_class_
- _Must_inspect_result_
- _Success_
- _Check_return_
- _Use_decl_annotations_
ms.assetid: c0aa268d-6fa3-4ced-a8c6-f7652b152e61
ms.openlocfilehash: 9af8ace7604df81e0dc2b705c6fa7227ff67fff8
ms.sourcegitcommit: 7bea0420d0e476287641edeb33a9d5689a98cb98
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/17/2020
ms.locfileid: "79467063"
---
# <a name="annotating-function-behavior"></a>Аннотирование поведения функции

Помимо добавления заметок к [параметрам функций и возвращаемым значениям](../code-quality/annotating-function-parameters-and-return-values.md), можно закомментировать свойства всей функции.

## <a name="function-annotations"></a>Заметки функций

Следующие примечания применяются к функции в целом и описывают, как она работает и что должно выполняться.

|Заметка|Description|
|----------------|-----------------|
|`_Called_from_function_class_(name)`|Не является автономной; это предикат, который должен использоваться с примечанием `_When_`. Дополнительные сведения см. в разделе [Указание времени и места применения заметки](../code-quality/specifying-when-and-where-an-annotation-applies.md).<br /><br /> Параметр `name` является произвольной строкой, которая также появляется в заметке `_Function_class_` в объявлении некоторых функций.  `_Called_from_function_class_` возвращает ненулевое значение, если анализируемая в данный момент функция объявляется с помощью `_Function_class_` с тем же значением `name`; в противном случае возвращается ноль.|
|`_Check_return_`|Аннотирует возвращаемое значение и заявляет, что вызывающий объект должен его проверять. Средство проверки выдает ошибку, если функция вызывается в пустом контексте.|
|`_Function_class_(name)`|Параметр `name` является произвольной строкой, указанной пользователем.  Он существует в пространстве имен, отличном от других пространств имен. Функция, указатель на функцию или, что наиболее полезно, тип указателя на функцию могут быть обозначены как принадлежащие к одному или нескольким классам функции.|
|`_Raises_SEH_exception_`|Добавляет примечание к функции, которая всегда вызывает исключение структурированного обработчика исключений (SEH), при условии `_When_` и `_On_failure_`. Дополнительные сведения см. в разделе [Указание времени и места применения заметки](../code-quality/specifying-when-and-where-an-annotation-applies.md).|
|`_Maybe_raises_SEH_exception_`|Добавляет примечание к функции, которая может при необходимости вызывать SЕH исключение, при условии `_When_` и `_On_failure_`.|
|`_Must_inspect_result_`|Заметка любого выходного значения, включая возвращаемое значение, параметры и глобальные.  Анализатор выдает ошибку, если значение в объекте, к которому добавлено примечание, далее не проверяется. "Проверка" инспектирует, используется ли он в условном выражении, присвоен ли он параметру вывода или глобальному параметру или передается ли он как параметр.  Для возвращаемых значений `_Must_inspect_result_` подразумевает `_Check_return_`.|
|`_Use_decl_annotations_`|Может использоваться в определении функции (также известном как тело функции) вместо списка заметок в заголовке.  При использовании `_Use_decl_annotations_` заметки, которые появляются в заголовке в области для одной и той же функции, используются, как если бы они также присутствовали в определении с заметкой `_Use_decl_annotations_`.|

## <a name="successfailure-annotations"></a>Заметки об успешном или неуспешном выполнении

Функция может завершиться ошибкой. Когда это происходит, ее результаты могут быть неполными или могут отличаться от результатов в том случае, когда функция завершается успешно.  Примечания в следующем списке предоставляют способы указания расширения функциональности при сбое.  Чтобы использовать эти примечания, необходимо включить их для определения успешного завершения, поэтому требуется примечание `_Success_`.  Следует заметить, что `NTSTATUS` и `HRESULT` уже содержат примечание `_Success_`, встроенное в них; однако, если указать собственное примечание `_Success_` на `NTSTATUS` или `HRESULT`, оно переопределит встроенное примечание.

|Заметка|Description|
|----------------|-----------------|
|`_Always_(anno_list)`|Эквивалентно `anno_list _On_failure_(anno_list)`; примечания в `anno_list` применяются вне зависимости от того, завершилась функция успехом или нет.|
|`_On_failure_(anno_list)`|Может использоваться только когда `_Success_` также используется для добавления заметок к функции явно или неявно через `_Return_type_success_` на typedef. Если примечание `_On_failure_` присутствует в параметре функции или возвращаемом значении, каждое примечание в `anno_list` (anno) ведет себя так, как если бы оно было закодировано как `_When_(!expr, anno)`, где `expr` является параметром для обязательного примечания `_Success_`. Это означает, что неявное приложение `_Success_` ко всем постусловиям неприменимо для `_On_failure_`.|
|`_Return_type_success_(expr)`|Может применяться к typedef. Указывает, что все функции, которые возвращают этот тип и явно не имеют `_Success_`, аннотированы, как если бы они имели `_Success_(expr)`. `_Return_type_success_` не может быть использован в функции или typedef указателя функции.|
|`_Success_(expr)`|`expr` является выражением, которое предоставляет rvalue. Если примечание `_Success_` присутствует в объявлении или определении функции, каждое примечание (`anno`) на функции и в постусловии ведет себя так, как если бы оно было закодировано как `_When_(expr, anno)`. Примечание `_Success_` может быть использовано только для функции, не для ее параметров или типа возвращаемого значения. На функции может быть не более одного примечания `_Success_` и оно не может быть в `_When_`, `_At_` или `_Group_`. Дополнительные сведения см. в разделе [Указание времени и места применения заметки](../code-quality/specifying-when-and-where-an-annotation-applies.md).|

## <a name="see-also"></a>См. также раздел

- [Использование аннотаций SAL для уменьшения количества дефектов в коде C/C++](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)
- [Основные сведения о языке SAL](../code-quality/understanding-sal.md)
- [Создание примечаний к параметрам и возвращаемым значениям функций](../code-quality/annotating-function-parameters-and-return-values.md)
- [Аннотация структур и классов](../code-quality/annotating-structs-and-classes.md)
- [Аннотация поведения блокировки](../code-quality/annotating-locking-behavior.md)
- [Указание времени и места применения примечания](../code-quality/specifying-when-and-where-an-annotation-applies.md)
- [Встроенные функции](../code-quality/intrinsic-functions.md)
- [Рекомендации и примеры](../code-quality/best-practices-and-examples-sal.md)