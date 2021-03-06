---
title: Класс task_group
ms.date: 07/20/2018
f1_keywords:
- task_group
- PPL/concurrency::task_group
- PPL/concurrency::task_group::task_group
helpviewer_keywords:
- task_group class
ms.openlocfilehash: 60c147f38ddc3936f47aea0cfd1ab1548b382441
ms.sourcegitcommit: a8ef52ff4a4944a1a257bdaba1a3331607fb8d0f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/11/2020
ms.locfileid: "77142564"
---
# <a name="task_group-class"></a>Класс task_group

Класс `task_group` представляет коллекцию параллельной работы, для которой возможно ожидание или отмена.

## <a name="syntax"></a>Синтаксис

```cpp
class task_group;
```

## <a name="members"></a>Члены

### <a name="public-constructors"></a>Открытые конструкторы

|Имя|Description|
|----------|-----------------|
|[task_group](#ctor)|Перегружен. Создает новый объект `task_group`.|
|[Деструктор ~ task_group](#dtor)|Уничтожает объект `task_group`. Ожидается вызов метода `wait` или `run_and_wait` объекта до выполнения деструктора, если только деструктор не выполняется как результат очистки стека из-за исключения.|

### <a name="public-methods"></a>Открытые методы

|Имя|Description|
|----------|-----------------|
|[cancel](#cancel)|Предпринимает попытку отменить поддерево работы с корнем в этой группе задач. Если возможно, все задачи, запланированные в группе задач, будут отменены транзитивно.|
|[is_canceling](#is_canceling)|Информирует вызывающий объект о том, находится ли группа задач в данный момент в процессе отмены. Это не обязательно означает, что метод `cancel` был вызван для объекта `task_group` (хотя, безусловно, этот метод должен возвращать `true`). Это может быть случай, когда объект `task_group` выполняется встроенным, а группа задач в рабочем дереве была отменена. В таких случаях, где среда выполнения может заранее определить, что отмена будет проходить через этот `task_group` объект, `true` также будет возвращена.|
|[run](#run)|Перегружен. Планирует задачу для объекта `task_group`. Если объект `task_handle` передается в качестве параметра для `run`, вызывающий объект отвечает за управление временем существования объекта `task_handle`. Версия метода, которая принимает ссылку на объект функции в качестве параметра, включает выделение кучи внутри среды выполнения, что может выполняться менее эффективно, чем использование версии, которая принимает ссылку на объект `task_handle`. Версия, принимающая параметр `_Placement`, заставляет задачу стремиться к выполнению в расположении, указанном этим параметром.|
|[run_and_wait](#run_and_wait)|Перегружен. Планирует выполнение задачи в вызывающем контексте с помощью объекта `task_group` для полной поддержки отмены. Затем функция ждет, пока вся работа над объектом `task_group` не завершится или не будет отменена. Если объект `task_handle` передается в качестве параметра для `run_and_wait`, вызывающий объект отвечает за управление временем существования объекта `task_handle`.|
|[ожидания](#wait)|Ожидает завершения или отмены всей работы над объектом `task_group`.|

## <a name="remarks"></a>Remarks

В отличие от класса `structured_task_group` с высокой степенью ограничений, класс `task_group` является гораздо более общей конструкцией. В нем отсутствуют ограничения, описанные в [structured_task_group](structured-task-group-class.md). `task_group` объекты можно безопасно использовать во всех потоках и использовать в произвольных направлениях. Недостатком конструкции `task_group` является то, что она может не выполняться, а также конструкцию `structured_task_group` для задач, выполняющих небольшие объемы работы.

Дополнительные сведения см. в разделе [параллелизм задач](../task-parallelism-concurrency-runtime.md).

## <a name="inheritance-hierarchy"></a>Иерархия наследования

`task_group`

## <a name="requirements"></a>Требования

**Заголовок:** PPL. h

**Пространство имен:** concurrency

## <a name="cancel"></a>Отмена

Предпринимает попытку отменить поддерево работы с корнем в этой группе задач. Если возможно, все задачи, запланированные в группе задач, будут отменены транзитивно.

```cpp
void cancel();
```

### <a name="remarks"></a>Remarks

Дополнительные сведения см. в разделе [Отмена](../cancellation-in-the-ppl.md).

## <a name="is_canceling"></a>is_canceling

Информирует вызывающий объект о том, находится ли группа задач в данный момент в процессе отмены. Это не обязательно означает, что метод `cancel` был вызван для объекта `task_group` (хотя, безусловно, этот метод должен возвращать `true`). Это может быть случай, когда объект `task_group` выполняется встроенным, а группа задач в рабочем дереве была отменена. В таких случаях, где среда выполнения может заранее определить, что отмена будет проходить через этот `task_group` объект, `true` также будет возвращена.

```cpp
bool is_canceling();
```

### <a name="return-value"></a>Возвращаемое значение

Указывает, находится ли объект `task_group` в процессе отмены (или гарантированно будет вскоре).

### <a name="remarks"></a>Remarks

Дополнительные сведения см. в разделе [Отмена](../cancellation-in-the-ppl.md).

## <a name="run"></a>запуска

Планирует задачу для объекта `task_group`. Если объект `task_handle` передается в качестве параметра для `run`, вызывающий объект отвечает за управление временем существования объекта `task_handle`. Версия метода, которая принимает ссылку на объект функции в качестве параметра, включает выделение кучи внутри среды выполнения, что может выполняться менее эффективно, чем использование версии, которая принимает ссылку на объект `task_handle`. Версия, принимающая параметр `_Placement`, заставляет задачу стремиться к выполнению в расположении, указанном этим параметром.

```cpp
template<
   typename _Function
>
void run(
   const _Function& _Func
);

template<
   typename _Function
>
void run(
   const _Function& _Func,
   location& _Placement
);

template<
   typename _Function
>
void run(
   task_handle<_Function>& _Task_handle
);

template<
   typename _Function
>
void run(
   task_handle<_Function>& _Task_handle,
   location& _Placement
);
```

### <a name="parameters"></a>Параметры

*_Function*<br/>
Тип объекта функции, который будет вызываться для выполнения тела маркера задачи.

*_Func*<br/>
Функция, которая будет вызываться для вызова текста задачи. Это может быть лямбда-выражение или другой объект, который поддерживает версию оператора вызова функции с сигнатурой `void operator()()`.

*_Placement*<br/>
Ссылка на расположение, в котором должна выполняться задача, представленная параметром `_Func`.

*_Task_handle*<br/>
Маркер запланированной работы. Обратите внимание, что вызывающий объект отвечает за время существования этого объекта. Среда выполнения продолжит ожидать, пока для этого `task_group` объекта не будет вызван метод `wait` или `run_and_wait`.

### <a name="remarks"></a>Remarks

Среда выполнения планирует выполнение предоставленной рабочей функции позднее, что может быть после возврата вызывающей функции. Этот метод использует объект [task_handle](task-handle-class.md) для хранения копии предоставленной рабочей функции. Таким образом, любые изменения состояния, происходящие в объекте функции, который передается в этот метод, не будут отображаться в копии этого объекта функции. Кроме того, убедитесь, что время существования всех объектов, передаваемых по указателю или по ссылке на рабочую функцию, остается допустимым до тех пор, пока Рабочая функция не вернет значение.

Если `task_group` деструкторы в результате очистки стека из исключения, нет необходимости гарантировать, что был сделан вызов метода `wait` или `run_and_wait`. В этом случае деструктор будет отменяться соответствующим образом и ожидать завершения задачи, представленной параметром `_Task_handle`.

Метод вызывает исключение [invalid_multiple_scheduling](invalid-multiple-scheduling-class.md) , если обработчик задач, заданный параметром `_Task_handle`, уже был запланирован в объекте группы задач с помощью метода `run` и в этой группе задач не был выполнен промежуточный вызов метода `wait` или `run_and_wait`.

## <a name="run_and_wait"></a>run_and_wait

Планирует выполнение задачи в вызывающем контексте с помощью объекта `task_group` для полной поддержки отмены. Затем функция ждет, пока вся работа над объектом `task_group` не завершится или не будет отменена. Если объект `task_handle` передается в качестве параметра для `run_and_wait`, вызывающий объект отвечает за управление временем существования объекта `task_handle`.

```cpp
template<
   class _Function
>
task_group_status run_and_wait(
   task_handle<_Function>& _Task_handle
);

template<
   class _Function
>
task_group_status run_and_wait(
   const _Function& _Func
);
```

### <a name="parameters"></a>Параметры

*_Function*<br/>
Тип объекта функции, который будет вызван для выполнения основной части задачи.

*_Task_handle*<br/>
Обработчик для задачи, который будет выполняться встроенным в контекст вызывающего. Обратите внимание, что вызывающий объект отвечает за время существования этого объекта. Среда выполнения будет продолжать ожидать, пока не завершится выполнение метода `run_and_wait`.

*_Func*<br/>
Функция, которая будет вызываться для вызова текста работы. Это может быть лямбда-выражение или другой объект, который поддерживает версию оператора вызова функции с сигнатурой `void operator()()`.

### <a name="return-value"></a>Возвращаемое значение

Значение, указывающее, было ли выполнено ожидание или отменена группа задач из-за явной операции отмены или исключения, вызываемого одной из задач. Дополнительные сведения см. в разделе [task_group_status](concurrency-namespace-enums.md#task_group_status).

### <a name="remarks"></a>Remarks

Обратите внимание, что одна или несколько задач, запланированных на этот `task_group` объект, могут выполняться встроенным в контекст вызывающего.

Если одна или несколько задач, запланированных на этот `task_group` объект, вызывают исключение, среда выполнения выберет одно такое исключение и распространяет его из вызова метода `run_and_wait`.

При возврате из метода `run_and_wait` объекта `task_group` среда выполнения сбрасывает объект в исходное состояние, в котором его можно использовать повторно. Это включает случай, когда объект `task_group` был отменен.

В неисключительном пути выполнения у вас есть требование вызвать этот метод или метод `wait` до выполнения деструктора `task_group`.

## <a name="ctor"></a>task_group

Создает новый объект `task_group`.

```cpp
task_group();

task_group(
   cancellation_token _CancellationToken
);
```

### <a name="parameters"></a>Параметры

*_CancellationToken*<br/>
Токен отмены для связывания с этой группой задач. Группа задач будет отменена, когда будет отменен токен.

### <a name="remarks"></a>Remarks

Конструктор, который принимает токен отмены, создает `task_group`, которая будет отменена, когда будет отменен источник, связанный с этим токеном. Предоставление явного токена отмены также изолирует эту группу задач от участия в неявной отмене из родительской группы с другим токеном или без токена.

## <a name="dtor"></a>~ task_group

Уничтожает объект `task_group`. Ожидается вызов метода `wait` или `run_and_wait` объекта до выполнения деструктора, если только деструктор не выполняется как результат очистки стека из-за исключения.

```cpp
~task_group();
```

### <a name="remarks"></a>Remarks

Если деструктор выполняется как результат обычного выполнения (например, не происходит очистка стека из-за исключения) и не были вызваны методы `wait` и `run_and_wait`, деструктор может вызвать исключение [missing_wait](missing-wait-class.md) .

## <a name="wait"></a>ожидания

Ожидает завершения или отмены всей работы над объектом `task_group`.

```cpp
task_group_status wait();
```

### <a name="return-value"></a>Возвращаемое значение

Значение, указывающее, было ли выполнено ожидание или отменена группа задач из-за явной операции отмены или исключения, вызываемого одной из задач. Дополнительные сведения см. в разделе [task_group_status](concurrency-namespace-enums.md#task_group_status).

### <a name="remarks"></a>Remarks

Обратите внимание, что одна или несколько задач, запланированных на этот `task_group` объект, могут выполняться встроенным в контекст вызывающего.

Если одна или несколько задач, запланированных на этот `task_group` объект, вызывают исключение, среда выполнения выберет одно такое исключение и распространяет его из вызова метода `wait`.

Вызов `wait` для объекта `task_group` сбрасывает его в исходное состояние, в котором его можно использовать повторно. Это включает случай, когда объект `task_group` был отменен.

В неисключительном пути выполнения у вас есть требование вызвать этот метод или метод `run_and_wait` до выполнения деструктора `task_group`.

## <a name="see-also"></a>См. также раздел

[Пространство имен concurrency](concurrency-namespace.md)<br/>
[Класс structured_task_group](structured-task-group-class.md)<br/>
[Класс task_handle](task-handle-class.md)
