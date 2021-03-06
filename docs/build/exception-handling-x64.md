---
title: Обработка исключений в 64-разрядных системах
ms.date: 10/14/2019
helpviewer_keywords:
- C++ exception handling, x64
- exception handling, x64
ms.assetid: 41fecd2d-3717-4643-b21c-65dcd2f18c93
ms.openlocfilehash: eff4f1a22512b597b5479dbcaabcc9d5fc93c940
ms.sourcegitcommit: 069e3833bd821e7d64f5c98d0ea41fc0c5d22e53
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2019
ms.locfileid: "74303201"
---
# <a name="x64-exception-handling"></a>Обработка исключений в 64-разрядных системах

Общие сведения об структурированной обработке исключений C++ и обработке исключений, а также о поведении в архитектуре x64. Общие сведения об обработке исключений см. [в разделе Обработка исключений в C++Visual ](../cpp/exception-handling-in-visual-cpp.md).

## <a name="unwind-data-for-exception-handling-debugger-support"></a>Данные очистки для обработки исключений, поддержка отладчика

Для обработки исключений и поддержки отладки требуются несколько структур данных.

### <a name="struct-runtime_function"></a>структура RUNTIME_FUNCTION

Для обработки исключений на основе таблиц требуется запись в таблице для всех функций, которые выделяют пространство стека или вызывают другую функцию (например, неконечные функции). Записи в таблице функций имеют формат:

|||
|-|-|
|ULONG|Начальный адрес функции|
|ULONG|Конечный адрес функции|
|ULONG|Адрес сведений очистки|

Структура RUNTIME_FUNCTION должна быть выровняйтеся в памяти в формате DWORD. Все адреса имеют относительный образ, то есть они являются 32-битным смещением от начального адреса изображения, содержащего запись таблицы функций. Эти записи сортируются и помещаются в раздел. pdata формат PE32 + Image. Для динамически создаваемых функций [JIT-компиляторы] среда выполнения для поддержки этих функций должна либо использовать Ртлинсталлфунктионтаблекаллбакк, либо Ртладдфунктионтабле, чтобы предоставить эти сведения операционной системе. В противном случае это приведет к ненадежной обработке исключений и отладке процессов.

### <a name="struct-unwind_info"></a>Структура UNWIND_INFO

Структура сведений о данных очистки используется для записи эффектов, которые функция накладывает на указатель стека и где неизменяемые регистры сохраняются в стеке:

|||
|-|-|
|УБИТЕ: 3|Версия|
|УБИТЕ: 5|Флаги|
|убите|Размер пролога|
|убите|Число кодов очистки|
|УБИТЕ: 4|Регистр кадра|
|УБИТЕ: 4|Смещение регистра кадра (масштабированное)|
|USHORT \* n|Массив кодов очистки|
|Переменная|Может иметь значение либо Form (1), либо (2) ниже|

(1) обработчик исключений

|||
|-|-|
|ULONG|Адрес обработчика исключений|
|Переменная|Данные обработчика для конкретного языка (необязательно)|

(2) сведения о цепочке раскрутки

|||
|-|-|
|ULONG|Начальный адрес функции|
|ULONG|Конечный адрес функции|
|ULONG|Адрес сведений очистки|

Структура UNWIND_INFO должна быть выровняйтеся в памяти в формате DWORD. Вот что означает каждое поле:

- **Версия**

   Номер версии данных очистки, в настоящее время 1.

- **Флаги**

   В настоящее время определены три флага:

   |Flag|Описание|
   |-|-|
   |`UNW_FLAG_EHANDLER`| Функция имеет обработчик исключений, который должен вызываться при поиске функций, нуждающихся в проверке исключений.|
   |`UNW_FLAG_UHANDLER`| Функция имеет обработчик завершения, который должен вызываться при очистке исключения.|
   |`UNW_FLAG_CHAININFO`| Эта структура сведений очистки не является первичной для процедуры. Вместо этого запись сведений о цепочке раскрутки является содержимым предыдущей записи RUNTIME_FUNCTION. Дополнительные сведения см. в разделе [сцепленные структуры сведений о выкрутки](#chained-unwind-info-structures). Если этот флаг установлен, то флаги UNW_FLAG_EHANDLER и UNW_FLAG_UHANDLER должны быть сняты. Кроме того, поля регистр кадра и распределение фиксированного стека должны иметь те же значения, что и в основной информации очистки.|

- **Размер пролога**

   Длина пролога функции в байтах.

- **Число кодов очистки**

   Число слотов в массиве кодов очистки. Некоторым кодам очистки, например UWOP_SAVE_NONVOL, требуется более одного слота в массиве.

- **Регистр кадра**

   В случае ненулевого значения функция использует указатель фрейма (FP), а это поле является числом неизменяемого регистра, используемого в качестве указателя фрейма, используя ту же кодировку для поля сведений об операции в UNWIND_CODE узлах.

- **Смещение регистра кадра (масштабированное)**

   Если поле регистра кадра не равно нулю, это поле является масштабируемым смещением от RSP, которое применяется к регистру FP при его установке. Фактический регистр FP имеет значение RSP + 16 \* это число, что позволяет использовать смещения от 0 до 240. Это смещение позволяет указывать регистр FP в середине выделения локального стека для динамических кадров стека, что позволяет повысить плотность кода с помощью более коротких инструкций. (То есть дополнительные инструкции могут использовать форму 8-битного смещения со знаком.)

- **Массив кодов очистки**

   Массив элементов, объясняющий воздействие пролога на неизменяемые регистры и RSP. Сведения о значениях отдельных элементов см. в разделе UNWIND_CODE. В целях выравнивания этот массив всегда имеет четное число записей, а последняя запись потенциально не используется. В этом случае массив будет на единицу больше, чем указано в поле количество кодов очистки.

- **Адрес обработчика исключений**

   Относительный указатель на исключение или обработчик завершения, зависящее от языка функции, если флаг UNW_FLAG_CHAININFO является четким и установлен один из флагов UNW_FLAG_EHANDLER или UNW_FLAG_UHANDLER.

- **Данные обработчика для конкретного языка**

   Данные обработчика исключений для конкретного языка функции. Формат этих данных не указан и полностью определяется конкретным используемым обработчиком исключений.

- **Сведения о цепочке раскрутки**

   Если установлен флаг UNW_FLAG_CHAININFO, то структура UNWIND_INFO заканчивается тремя Увордс.  Эти Увордс представляют сведения о RUNTIME_FUNCTION для функции последовательной очистки.

### <a name="struct-unwind_code"></a>Структура UNWIND_CODE

Массив кода очистки используется для записи последовательности операций в прологе, влияющих на неизменяемые регистры и RSP. Каждый элемент кода имеет следующий формат:

|||
|-|-|
|убите|Смещение в прологе|
|УБИТЕ: 4|Код операции очистки|
|УБИТЕ: 4|Сведения об операции|

Массив сортируется по убыванию смещения в прологе.

#### <a name="offset-in-prolog"></a>Смещение в прологе

Смещение (от начала пролога) конца инструкции, которая выполняет эту операцию, плюс 1 (то есть смещение начала следующей инструкции).

#### <a name="unwind-operation-code"></a>Код операции очистки

Примечание. для некоторых кодов операций требуется смещение без знака для значения в локальном кадре стека. Это смещение от начала, то есть наименьшего адреса фиксированного выделения стека. Если поле регистра кадра в UNWIND_INFO равно нулю, это смещение отсчитывается с RSP. Если поле регистра кадра не равно нулю, это смещение будет иметь значение, где при установленном регистре FP было обнаружено RSP. Он равен регистру FP минус смещению регистра FP (16 \* смещение регистра вертикального кадра в UNWIND_INFO). Если используется регистр FP, любой код очистки, принимающий смещение, должен использоваться только после того, как регистр FP установлен в прологе.

Для всех кодов операций, за исключением `UWOP_SAVE_XMM128` и `UWOP_SAVE_XMM128_FAR`, смещение всегда кратно 8, поскольку все интересующие значения стека хранятся в 8-байтовой границах (сам стек всегда имеет размер 16 байт). Для кодов операций, которые принимают короткое смещение (меньше 512 КБ), итоговый USHORT в узлах для этого кода содержит смещение, деленное на 8. Для кодов операций, которые принимают длинное смещение (512 КБ < = offset < 4 ГБ), последние два узла USHORT для этого кода содержат смещение (в формате с прямым порядком байтов).

Для кодов операций `UWOP_SAVE_XMM128` и `UWOP_SAVE_XMM128_FAR`смещение всегда кратно 16, так как все 128-разрядные операции XMM должны выполняться в памяти с согласованным объемом в 16 байт. Таким образом, коэффициент масштабирования, равный 16, используется для `UWOP_SAVE_XMM128`, разрешая смещение менее 1 МБ.

Код операции очистки — одно из следующих значений:

- `UWOP_PUSH_NONVOL` (0) 1 узел

  Отправьте неизменяемый регистр целых чисел, уменьшая значение RSP на 8. Сведения об операции — это номер регистра. Из-за ограничений на `UWOP_PUSH_NONVOL` эпилоги коды очистки должны находиться в прологе первыми и соответственно, в конце массива кода очистки. Это относительное упорядочение применяется ко всем остальным кодам очистки, кроме `UWOP_PUSH_MACHFRAME`.

- `UWOP_ALLOC_LARGE` (1) 2 или 3 узла

  Выделение большого размера области в стеке. Существует две формы. Если сведения об операции равны 0, то размер выделения, деленный на 8, записывается в следующий слот, что позволяет выделить до 512 КБ-8. Если сведения об операции равны 1, немасштабируемый размер выделения записывается в два следующих слота в формате с прямым порядком байтов, что позволяет выделить до 4 ГБ-8.

- `UWOP_ALLOC_SMALL` (2) 1 узел

  Выделение небольшого размера области в стеке. Размер выделения — это поле сведений об операции, \* 8 + 8, что позволяет выделение с 8 до 128 байт.

  Код очистки для выделения стека всегда должен использовать кратчайшую возможную кодировку:

  |**Размер выделения**|**Код очистки**|
  |-|-|
  |от 8 до 128 байт|`UWOP_ALLOC_SMALL`|
  |от 136 до 512 КБ-8 байт|`UWOP_ALLOC_LARGE`, сведения об операции = 0|
  |512 КБ – 4G-8 байт|`UWOP_ALLOC_LARGE`, сведения об операции = 1|

- `UWOP_SET_FPREG` (3) 1 узел

  Установите регистр указателя фрейма, задав для регистра некоторое смещение текущего RSP. Смещение равно полю смещения кадра Register (масштабированное) в UNWIND_INFO \* 16, что позволяет использовать смещения от 0 до 240. Использование смещения позволяет установить указатель фрейма, указывающий на середину фиксированного выделения стека, что способствует повышению плотности кода благодаря повышению уровня доступа к использованию коротких форм инструкций. Поле сведений об операции зарезервировано и не должно использоваться.

- `UWOP_SAVE_NONVOL` (4) 2 узла

  Сохраните неизменяемый регистр целых чисел в стеке, используя MOV вместо PUSH. Этот код в основном используется для *переноса по словам*, в котором несохраняемый регистр сохраняется в стеке в расположении, которое было ранее выделено. Сведения об операции — это номер регистра. Смещение стека, масштабированное на 8, записывается в следующем слоте кода операции очистки, как описано в заметке выше.

- `UWOP_SAVE_NONVOL_FAR` (5) 3 узла

  Сохраните неизменяемый регистр целых чисел в стеке с длинным смещением, используя MOV вместо PUSH. Этот код в основном используется для *переноса по словам*, в котором несохраняемый регистр сохраняется в стеке в расположении, которое было ранее выделено. Сведения об операции — это номер регистра. Немасштабированное смещение стека записывается в следующих двух слотах кода операции очистки, как описано в заметке выше.

- `UWOP_SAVE_XMM128` (8) 2 узла

  Сохраните все 128 бит неизменяемого регистра XMM в стеке. Сведения об операции — это номер регистра. Смещение стека, масштабированное по 16, записывается в следующем слоте.

- `UWOP_SAVE_XMM128_FAR` (9) 3 узла

  Сохраните все 128 бит неизменяемого регистра XMM в стеке с длинным смещением. Сведения об операции — это номер регистра. Немасштабированное смещение стека записывается в следующие два слота.

- `UWOP_PUSH_MACHFRAME` (10) 1 узел

  Отправка кадра компьютера.  Этот код очистки используется для записи воздействия аппаратного прерывания или исключения. Существует две формы. Если сведения об операции равны 0, то один из этих кадров был помещен в стек:

  |||
  |-|-|
  |RSP + 32|SS|
  |RSP + 24|Старый RSP|
  |RSP + 16|ефлагс|
  |RSP + 8|СЛОЖНЫХ|
  |RSP|МАРШРУТОВ|

  Если сведения об операции равны 1, то один из этих кадров был отправлен:

  |||
  |-|-|
  |RSP + 40|SS|
  |RSP + 32|Старый RSP|
  |RSP + 24|ефлагс|
  |RSP + 16|СЛОЖНЫХ|
  |RSP + 8|МАРШРУТОВ|
  |RSP|Код ошибки|

  Этот код очистки всегда отображается в фиктивном прологе, который никогда не исполняется, а появляется перед реальной точкой входа в подпрограмму прерывания и существует только для того, чтобы предоставить место для имитации push-уведомлений. `UWOP_PUSH_MACHFRAME` записывает данные о моделировании, что означает, что компьютер выполняет эту операцию по принципу:

  1. Обратный адрес RIP от начала стека до *TEMP*
  
  1. Отправить СС

  1. Отправить старый RSP

  1. Отправка ЕФЛАГС

  1. Принудительная отправка CS

  1. *Временная* отправка

  1. Код ошибки принудительной отправки (если сведения о Op равны 1)

  Смоделированная операция `UWOP_PUSH_MACHFRAME` уменьшает значение RSP на 40 (Op info равно 0) или 48 (Op info равно 1).

#### <a name="operation-info"></a>Сведения об операции

Значение битов сведений о операции зависит от кода операции. Чтобы закодировать регистр общего назначения (целое число), используется такое сопоставление:

|||
|-|-|
|0|RAX|
|1|RCX|
|2|RDX|
|3|RBX|
|4|RSP|
|5|RBP|
|6|RSI|
|7|RDI|
|от 8 до 15|R8 — R15|

### <a name="chained-unwind-info-structures"></a>Структуры связанных сведений о стеке

Если установлен флаг UNW_FLAG_CHAININFO, то структура сведений о заполнении является вторичной, а поле "общий адрес обработчика исключений/цепочки-информация" содержит основную информацию о выбытии. Этот пример кода получает основную информацию о выпуске, предполагая, что `unwindInfo` является структурой, для которой установлен флаг UNW_FLAG_CHAININFO.

```cpp
PRUNTIME_FUNCTION primaryUwindInfo = (PRUNTIME_FUNCTION)&(unwindInfo->UnwindCode[( unwindInfo->CountOfCodes + 1 ) & ~1]);
```

Связанные сведения полезны в двух ситуациях. Сначала его можно использовать для несмежных сегментов кода. Используя связанные сведения, можно уменьшить размер необходимой информации очистки, так как не нужно дублировать массив кодов очистки из основной информации очистки.

Также можно использовать связанные сведения для группировки сохраненных временных регистров. Компилятор может отложить сохранение некоторых временных регистров, пока он не выходит за пределы пролога записи функции. Вы можете записать их, указав основную информацию о выходе для части функции перед сгруппированным кодом, а затем настроив цепочку данных с ненулевым размером пролога, где коды очистки в связанных сведениях соответствуют сохранению неизменяемых регистров. В этом случае коды очистки являются экземплярами UWOP_SAVE_NONVOL. Группирование, сохраняющее неизменяемые регистры с помощью принудительной отправки или изменения регистра RSP с помощью дополнительного фиксированного выделения стека, не поддерживается.

Элемент UNWIND_INFO с UNW_FLAG_CHAININFOным набором может содержать запись RUNTIME_FUNCTION, элемент UNWIND_INFO также имеет UNW_FLAG_CHAININFO набор, иногда называемый *множественной обтеканием сжатия*. Со временем цепочки указателей сведений о стеке поступают в элемент UNWIND_INFO, который UNW_FLAG_CHAININFO очистить. Этот элемент является первичным UNWIND_INFO элементом, который указывает на фактическую точку входа процедуры.

## <a name="unwind-procedure"></a>Очистка процедуры

Массив кода очистки сортируется в убывающем порядке. При возникновении исключения полный контекст сохраняется операционной системой в записи контекста. Затем вызывается логика диспетчеризации исключений, которая многократно выполняет следующие действия для поиска обработчика исключений:

1. Использовать текущий протокол RIP, хранящийся в записи контекста, для поиска RUNTIME_FUNCTION записи таблицы, описывающей текущую функцию (или ее часть для сцепленных UNWIND_INFO записей).

1. Если запись в таблице функций не найдена, то она находится в конечной функции, а RSP напрямую обращается к указателю возврата. Указатель возврата в [RSP] хранится в обновленном контексте, а имитация RSP увеличивается на 8, а шаг 1 повторяется.

1. Если обнаружена запись в таблице функций, RIP может находиться в трех регионах: a) в заключительном фрагменте, b) в прологе или c) в коде, который может быть охвачен обработчиком исключений.

   - Случай.) Если RIP находится в заключительном примере, то управление выходит за пределы функции, для этой функции может отсутствовать обработчик исключений, а эффекты эпилога должны продолжать вычислять контекст вызывающей функции. Чтобы определить, находится ли RIP в заключительном фрагменте, проверяется поток кода из RIP. Если этот поток кода может быть сопоставлен с завершающей частью допустимого эпилога, то он находится в заключительном фрагменте, а оставшаяся часть эпилога имитируется, а запись контекста обновляется по мере обработки каждой инструкции. После этой обработки шаг 1 повторяется.

   - Вариант б) Если RIP находится в прологе, а затем Управление не выполнило вход в функцию, для этой функции не может быть связанного с этим исключением обработчика исключений, и результаты пролога должны быть отменены для выработки контекста вызывающей функции. RIP находится в прологе, если расстояние от начала функции до RIP меньше или равно размеру пролога, закодированному в сведениях очистки. Эффекты пролога отменяются путем сканирования вперед по массиву кодов очистки для первой записи со смещением, которое меньше или равно смещению RIP от начала функции, а затем отменяет влияние всех оставшихся элементов в массиве кода очистки. Затем шаг 1 повторяется.

   - Case c) Если RIP не находится внутри пролога или эпилога и функция имеет обработчик исключений (UNW_FLAG_EHANDLER задан), то вызывается обработчик конкретного языка. Обработчик сканирует свои данные и вызывает функции фильтра соответствующим образом. Обработчик конкретного языка может возвращать исключение, которое было обработано, или чтобы продолжить поиск. Он также может инициировать очистку напрямую.

1. Если обработчик, зависящий от языка, возвращает обработанное состояние, выполнение продолжается с использованием исходной записи контекста.

1. Если обработчик не зависит от языка или обработчик возвращает состояние "продолжить поиск", запись контекста должна быть перевернута в состояние вызывающего объекта. Это выполняется путем обработки всех элементов массива кода очистки, отменяя результат каждого из них. Затем шаг 1 повторяется.

Если используется цепочка сведений о стеке, эти основные шаги по-прежнему будут выполнены. Единственное отличие заключается в том, что при прохождении по массиву кода очистки для очистки эффектов пролога после достижения конца массива он связывается с родительской информацией очистки, и найден весь массив кода очистки. Это связывание продолжится, пока не поступают данные очистки без флага UNW_CHAINED_INFO, а затем завершается проход массива кода очистки.

Наименьший набор данных очистки — 8 байт. Это будет представлять функцию, которая выделила не более 128 байт стека и, возможно, сохранила один невременный регистр. Это также размер структуры цепочки сведений о стеке для пролога нулевой длины без кодов очистки.

## <a name="language-specific-handler"></a>Обработчик для конкретного языка

Относительный адрес обработчика для конкретного языка содержится в UNWIND_INFO каждый раз, когда установлены флаги UNW_FLAG_EHANDLER или UNW_FLAG_UHANDLER. Как описано в предыдущем разделе, обработчик для конкретного языка вызывается как часть поиска обработчика исключений или как часть очистки. Он имеет следующий прототип:

```cpp
typedef EXCEPTION_DISPOSITION (*PEXCEPTION_ROUTINE) (
    IN PEXCEPTION_RECORD ExceptionRecord,
    IN ULONG64 EstablisherFrame,
    IN OUT PCONTEXT ContextRecord,
    IN OUT PDISPATCHER_CONTEXT DispatcherContext
);
```

**Ексцептионрекорд** предоставляет указатель на запись исключения, имеющую стандартное определение Win64.

**Естаблишерфраме** — это адрес базы фиксированного выделения стека для этой функции.

**Контекстрекорд** указывает на контекст исключения на момент возникновения исключения (в случае обработчика исключений) или текущего контекста очистки (в случае обработчика завершения).

**Диспатчерконтекст** указывает на контекст Dispatcher для этой функции. Он имеет следующее определение:

```cpp
typedef struct _DISPATCHER_CONTEXT {
    ULONG64 ControlPc;
    ULONG64 ImageBase;
    PRUNTIME_FUNCTION FunctionEntry;
    ULONG64 EstablisherFrame;
    ULONG64 TargetIp;
    PCONTEXT ContextRecord;
    PEXCEPTION_ROUTINE LanguageHandler;
    PVOID HandlerData;
} DISPATCHER_CONTEXT, *PDISPATCHER_CONTEXT;
```

**Контролпк** — это значение RIP в этой функции. Это значение является либо адресом исключения, либо адресом, по которому элемент управления оставил функцию установки. RIP используется для определения того, находится ли элемент управления в какой-либо защищенной конструкции внутри этой функции, например `__try` блок для `__try`/`__except` или `__try`/`__finally`.

**ImageBase** — это базовая папка образа (адрес загрузки) модуля, содержащего эту функцию, для добавления к 32-разрядным смещениям, используемым в записи функции и данных очистки для записи относительных адресов.

**Функтионентри** предоставляет указатель на запись функции RUNTIME_FUNCTION, содержащую сведения о функции и относительных адресах для этой функции.

**Естаблишерфраме** — это адрес базы фиксированного выделения стека для этой функции.

**Таржетип** Предоставляет необязательный адрес инструкции, указывающий адрес продолжения очистки. Этот адрес пропускается, если не указан **естаблишерфраме** .

**Контекстрекорд** указывает на контекст исключения для использования кодом диспетчеризации или очистки системного исключения.

**Лангуажехандлер** указывает на вызываемую подпрограммы языкового обработчика языка.

**Хандлердата** указывает на данные обработчика для этой функции, зависящие от языка.

## <a name="unwind-helpers-for-masm"></a>Методы очистки для MASM

Для написания правильных подпрограмм сборки существует набор псевдо-операций, которые можно использовать параллельно с фактическими инструкциями сборки для создания соответствующего pData и XData. И существует набор макросов, которые позволяют упростить использование псевдо-операций для наиболее распространенных целей.

### <a name="raw-pseudo-operations"></a>Необработанные псевдо-операции

|Псевдо|Описание|
|-|-|
|КАДР \[процесса:*ехандлер*]|Приводит к тому, что компилятор MASM создает запись таблицы функций в pData и сведения о выведении в XData для структурированной обработки исключений функции.  При наличии *ехандлер* эта процедура в. XData указывается в качестве обработчика для конкретного языка.<br /><br /> При использовании атрибута FRAME за ним должен следовать. Директива ЕНДПРОЛОГ.  Если функция является конечной функцией (как определено в [типах функций](../build/stack-usage.md#function-types)), атрибут Frame не нужен, как и оставшаяся часть этих псевдо-операций.|
|. ПУШРЕГ *регистр*|Создает UWOP_PUSH_NONVOL запись кода очистки для указанного номера регистра, используя текущее смещение в прологе.<br /><br /> Используйте его только с непостоянными целочисленными регистрами.  Для принудительной отправки временных регистров используйте. АЛЛОКСТАКК 8, вместо этого|
|. СЕТФРАМЕ *регистр*, *смещение*|Заполняет поле регистра кадра и смещение в данных очистки с помощью указанного регистра и смещения. Смещение должно быть кратным 16 и меньше или равно 240. Эта директива также создает UWOP_SET_FPREG запись кода очистки для указанного регистра, используя текущее смещение пролога.|
|. *Размер* аллокстакк|Создает UWOP_ALLOC_SMALL или UWOP_ALLOC_LARGE с указанным размером для текущего смещения в прологе.<br /><br /> Операнд *размера* должен быть кратен 8.|
|. САВЕРЕГ *регистр*, *смещение*|Создает UWOP_SAVE_NONVOL или UWOP_SAVE_NONVOL_FAR запись кода очистки для указанного регистра и смещения с использованием текущего смещения пролога. Компилятор MASM выбирает наиболее эффективную кодировку.<br /><br /> *смещение* должно быть положительным и кратным 8. *смещение* задается относительно базового фрейма процедуры, который обычно находится в RSP, или, если используется указатель фрейма, немасштабированный указатель фрейма.|
|. SAVEXMM128 *регистр*, *смещение*|Создает UWOP_SAVE_XMM128 или UWOP_SAVE_XMM128_FAR запись кода очистки для указанного регистра XMM и смещения с использованием текущего смещения пролога. Компилятор MASM выбирает наиболее эффективную кодировку.<br /><br /> *смещение* должно быть положительным и кратным 16.  *смещение* задается относительно базового фрейма процедуры, который обычно находится в RSP, или, если используется указатель фрейма, немасштабированный указатель фрейма.|
|. *Код*\[PushFrame]|Создает UWOP_PUSH_MACHFRAME запись кода очистки. Если указан необязательный *код* , для записи кода очистки задается модификатор 1. В противном случае модификатор равен 0.|
|.ENDPROLOG|Сообщает об окончании объявлений пролога.  Должен находиться в первых 255 байтах функции.|

Ниже приведен пример пролога функции с правильным использованием большинства кодов операций:

```MASM
sample PROC FRAME
    db      048h; emit a REX prefix, to enable hot-patching
    push rbp
    .pushreg rbp
    sub rsp, 040h
    .allocstack 040h
    lea rbp, [rsp+020h]
    .setframe rbp, 020h
    movdqa [rbp], xmm7
    .savexmm128 xmm7, 020h ;the offset is from the base of the frame
                           ;not the scaled offset of the frame
    mov [rbp+018h], rsi
    .savereg rsi, 038h
    mov [rsp+010h], rdi
    .savereg rdi, 010h ; you can still use RSP as the base of the frame
                       ; or any other register you choose
    .endprolog

; you can modify the stack pointer outside of the prologue (similar to alloca)
; because we have a frame pointer.
; if we didn't have a frame pointer, this would be illegal
; if we didn't make this modification,
; there would be no need for a frame pointer

    sub rsp, 060h

; we can unwind from the next AV because of the frame pointer

    mov rax, 0
    mov rax, [rax] ; AV!

; restore the registers that weren't saved with a push
; this isn't part of the official epilog, as described in section 2.5

    movdqa xmm7, [rbp]
    mov rsi, [rbp+018h]
    mov rdi, [rbp-010h]

; Here's the official epilog

    lea rsp, [rbp+020h] ; deallocate both fixed and dynamic portions of the frame
    pop rbp
    ret
sample ENDP
```

Дополнительные сведения о примере эпилога см. в разделе [Код эпилога](prolog-and-epilog.md#epilog-code) в [прологе x64 и эпилога](prolog-and-epilog.md).

### <a name="masm-macros"></a>Макросы MASM

Чтобы упростить использование [необработанных псевдо-операций](#raw-pseudo-operations), существует набор макросов, определенный в ksamd64. Inc, который можно использовать для создания обычных прологов процедур и эпилоги.

|Макрос|Описание|
|-|-|
|alloc_stack (n)|Выделяет кадр стека из n байт (с помощью `sub rsp, n`) и выдает соответствующую информацию очистки (. аллокстакк n).|
|save_reg *reg*, *Loc*|Сохраняет неизменяемый регистр *reg* в стеке по адресу RSP offset *Loc*и выдает соответствующую информацию для очистки. (. саверег reg, LOC)|
|push_reg *reg*|Помещает в стек неизменяемый регистр *reg* и выдает соответствующую информацию для очистки. (. пушрег reg)|
|rex_push_reg *reg*|Сохраняет неизменяемый регистр в стеке с использованием 2-байтовой отправки и выдает соответствующую информацию очистки (. пушрег reg).  Используйте этот макрос, если инструкция Push является первой инструкцией в функции, чтобы обеспечить возможность исправления этой функции.|
|save_xmm128 *reg*, *Loc*|Сохраняет неизменяемый *регистр Регистра* XMM в стеке по адресу RSP offset *Loc*и выдает соответствующую информацию очистки (. SAVEXMM128 reg, LOC).|
|set_frame *reg*, *смещение*|Устанавливает *для регистра кадра регистр в формате* RSP + *offset* (с помощью `mov`или `lea`) и выдает соответствующую информацию очистки (. set_frame reg, offset).|
|push_eflags|Помещает ефлагс в инструкцию `pushfq` и выдает соответствующую информацию очистки (. alloc_stack 8).|

Ниже приведен пример пролога функции с правильным использованием макросов:

```MASM
sampleFrame struct
    Fill     dq ?; fill to 8 mod 16
    SavedRdi dq ?; Saved Register RDI
    SavedRsi dq ?; Saved Register RSI
sampleFrame ends

sample2 PROC FRAME
    alloc_stack(sizeof sampleFrame)
    save_reg rdi, sampleFrame.SavedRdi
    save_reg rsi, sampleFrame.SavedRsi
    .end_prolog

; function body

    mov rsi, sampleFrame.SavedRsi[rsp]
    mov rdi, sampleFrame.SavedRdi[rsp]

; Here's the official epilog

    add rsp, (sizeof sampleFrame)
    ret
sample2 ENDP
```

## <a name="unwind-data-definitions-in-c"></a>Определения раскрутки данных в C

Ниже приведено описание данных очистки на языке C:

```C
typedef enum _UNWIND_OP_CODES {
    UWOP_PUSH_NONVOL = 0, /* info == register number */
    UWOP_ALLOC_LARGE,     /* no info, alloc size in next 2 slots */
    UWOP_ALLOC_SMALL,     /* info == size of allocation / 8 - 1 */
    UWOP_SET_FPREG,       /* no info, FP = RSP + UNWIND_INFO.FPRegOffset*16 */
    UWOP_SAVE_NONVOL,     /* info == register number, offset in next slot */
    UWOP_SAVE_NONVOL_FAR, /* info == register number, offset in next 2 slots */
    UWOP_SAVE_XMM128 = 8, /* info == XMM reg number, offset in next slot */
    UWOP_SAVE_XMM128_FAR, /* info == XMM reg number, offset in next 2 slots */
    UWOP_PUSH_MACHFRAME   /* info == 0: no error-code, 1: error-code */
} UNWIND_CODE_OPS;

typedef union _UNWIND_CODE {
    struct {
        UBYTE CodeOffset;
        UBYTE UnwindOp : 4;
        UBYTE OpInfo   : 4;
    };
    USHORT FrameOffset;
} UNWIND_CODE, *PUNWIND_CODE;

#define UNW_FLAG_EHANDLER  0x01
#define UNW_FLAG_UHANDLER  0x02
#define UNW_FLAG_CHAININFO 0x04

typedef struct _UNWIND_INFO {
    UBYTE Version       : 3;
    UBYTE Flags         : 5;
    UBYTE SizeOfProlog;
    UBYTE CountOfCodes;
    UBYTE FrameRegister : 4;
    UBYTE FrameOffset   : 4;
    UNWIND_CODE UnwindCode[1];
/*  UNWIND_CODE MoreUnwindCode[((CountOfCodes + 1) & ~1) - 1];
*   union {
*       OPTIONAL ULONG ExceptionHandler;
*       OPTIONAL ULONG FunctionEntry;
*   };
*   OPTIONAL ULONG ExceptionData[]; */
} UNWIND_INFO, *PUNWIND_INFO;

typedef struct _RUNTIME_FUNCTION {
    ULONG BeginAddress;
    ULONG EndAddress;
    ULONG UnwindData;
} RUNTIME_FUNCTION, *PRUNTIME_FUNCTION;

#define GetUnwindCodeEntry(info, index) \
    ((info)->UnwindCode[index])

#define GetLanguageSpecificDataPtr(info) \
    ((PVOID)&GetUnwindCodeEntry((info),((info)->CountOfCodes + 1) & ~1))

#define GetExceptionHandler(base, info) \
    ((PEXCEPTION_HANDLER)((base) + *(PULONG)GetLanguageSpecificDataPtr(info)))

#define GetChainedFunctionEntry(base, info) \
    ((PRUNTIME_FUNCTION)((base) + *(PULONG)GetLanguageSpecificDataPtr(info)))

#define GetExceptionDataPtr(info) \
    ((PVOID)((PULONG)GetLanguageSpecificData(info) + 1)
```

## <a name="see-also"></a>См. также:

[Программные соглашения для 64-разрядных систем](../build/x64-software-conventions.md)
