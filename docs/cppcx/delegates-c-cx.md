---
title: Делегаты (C++/CX)
ms.date: 01/22/2017
ms.assetid: 3175bf1c-86d8-4eda-8d8f-c5b6753d8e38
ms.openlocfilehash: 3ab455044b98cdd8c7b13a650f729efc2132797e
ms.sourcegitcommit: 180f63704f6ddd07a4172a93b179cf0733fd952d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2019
ms.locfileid: "70740280"
---
# <a name="delegates-ccx"></a>Делегаты (C++/CX)

Ключевое слово используется для объявления ссылочного типа, который является среда выполнения Windows эквивалентом объекта функции в стандарте C++ `delegate` Объявление делегата похоже на сигнатуру функции; оно определяет тип возвращаемого значения и типы параметров, которые должна иметь заключенная в оболочку функция. Ниже показано пользователем объявление делегата:

```cpp
public delegate void PrimeFoundHandler(int result);
```

Делегаты наиболее часто используются в сочетании с событиями. Событие имеет тип делегата; эта связь во многом похожа на отношения между классом и типом интерфейса. Делегат представляет контракт, которому должны соответствовать обработчики событий. Ниже показан член класса события, типом которого является ранее объявленный делегат:

```cpp
event PrimeFoundHandler^ primeFoundEvent;
```

При объявлении делегатов, которые будут предоставляться клиентам через двоичный интерфейс приложения среда выполнения Windows, используйте [Windows:: Foundation::\<TypedEventHandler TSender, TResult >](/uwp/api/windows.foundation.typedeventhandler). Этот делегат имеет предопределенные двоичные прокси и заглушки, которые позволяют его использовать клиентами Javascript.

## <a name="consuming-delegates"></a>Использование делегатов

При создании универсальная платформа Windows приложения часто приходится работать с делегатом в качестве типа события, предоставляемого классом среда выполнения Windows. Чтобы подписаться на событие, создайте экземпляр типа делегата, указав функцию (или лямбда-выражение), соответствующее сигнатуре делегата. Затем воспользуйтесь оператором `+=` , чтобы передать объект делегата члену события в классе. Это называется "подписаться на событие". Когда экземпляр класса инициирует событие, вызывается ваша функция, а также другие обработчики, которые были добавлены данным объектом или другими объектами.

> [!TIP]
> При создании обработчика событий Visual Studio выполняет многие действия автоматически. Например, при определении обработчика событий в разметке XAML появляется подсказка. Если щелкнуть подсказку, Visual Studio автоматически создаст метод обработчика событий и свяжет его с событием в классе публикации.

В следующем примере демонстрируется использование основного подхода. `Windows::Foundation::TypedEventHandler` — это тип делегата. Функция обработчика создана с помощью именованной функции.

В файле app.h:

[!code-cpp[cx_delegates#120](../cppcx/codesnippet/CPP/delegatesevents/class1.h#120)]

В файле app.cpp:

[!code-cpp[cx_delegates#121](../cppcx/codesnippet/CPP/delegatesevents/class1.cpp#121)]

> [!WARNING]
> Как правило, для обработчика событий лучше использовать именованную функцию, а не лямбда-выражение, чтобы не пришлось внимательно следить за возникновением циклических ссылок. Именованная функция перехватывает указатель this с помощью слабой ссылки, в то время как лямбда-выражение перехватывает его с помощью строгой ссылки и создает циклическую ссылку. Дополнительные сведения см. в разделе [слабые ссылки и критические циклы](../cppcx/weak-references-and-breaking-cycles-c-cx.md).

По соглашению имена делегатов обработчиков событий, определяемые среда выполнения Windows, имеют форму * EventHandler, например RoutedEventHandler, SizeChangedEventHandler или SuspendingEventHandler. Также общепринято, что делегаты обработчиков событий имеют два параметра и возвращают значение void. В делегате, у которого нет параметров-типов, первый параметр принадлежит к типу [Platform::Object^](../cppcx/platform-object-class.md); он хранит ссылку на объект-отправитель, инициировавший событие. Необходимо выполнить приведение обратно в исходный тип, прежде чем использовать аргумент в методе обработчика событий. В делегате обработчика событий, имеющем параметры-типы, первый параметр-тип указывает тип отправителя, а второй параметр является дескриптором класса ссылки, который содержит сведения о событии. По соглашению этот класс \*называется EventArgs. Например, делегат RoutedEventHandler имеет второй параметр типа RoutedEventArgs^, и DragEventHander имеет второй параметр типа DragEventArgs^.

В соответствии с общепринятой практикой делегаты, являющиеся оболочками для кода, который выполняется при завершении асинхронной операции, имеют имя *CompletedHandler. Эти делегаты определяются как свойства класса, а не как события. Поэтому оператор `+=` не используется, чтобы подписаться на них; вместо этого объект делегата просто присваивается свойству.

> [!TIP]
> C++ IntelliSense не показывает полную сигнатуру делегата, а потому не помогает определить конкретный тип параметра EventArgs. Чтобы определить его тип, можно открыть **Обозреватель объектов** и просмотреть сведения о методе `Invoke` делегата.

## <a name="creating-custom-delegates"></a>Создание пользовательских делегатов

Можно определить собственные делегаты, определить обработчики событий или позволить потребителям передавать пользовательские функции компоненту среда выполнения Windows. Как и любой другой тип среда выполнения Windows, открытый делегат не может быть объявлен как универсальный.

### <a name="declaration"></a>Объявление

Объявление делегата похоже на объявление функции, за исключением того что делегат — это тип. Обычно делегат объявляется в области пространства имен, хотя также можно вложить объявление делегата внутрь объявления класса. Следующий делегат инкапсулирует любую функцию, принимающую аргумент `ContactInfo^` и возвращающую значение `Platform::String^`.

[!code-cpp[cx_delegates#111](../cppcx/codesnippet/CPP/delegatesevents/class1.h#111)]

После объявления типа делегата можно объявить члены класса этого типа или методы, принимающие в качестве параметров объекты этого типа. Метод или функция также может возвращать тип делегата. В следующем примере метод `ToCustomString` принимает делегат в качестве входного параметра. Этот метод позволяет клиентскому коду предоставить пользовательскую функцию, которая создает строку из некоторых или всех открытых свойств объекта `ContactInfo` .

[!code-cpp[Cx_delegates#112](../cppcx/codesnippet/CPP/delegatesevents/class1.h#112)]

> [!NOTE]
> При ссылке на тип делегата используется символ "^", точно так же, как и любой среда выполнения Windows ссылочный тип.

Объявление события всегда имеет тип делегата. В этом примере показана типичная сигнатура типа делегата в среда выполнения Windows:

[!code-cpp[cx_delegates#122](../cppcx/codesnippet/CPP/delegatesevents/class1.h#122)]

Событие `Click` в классе `Windows:: UI::Xaml::Controls::Primitives::ButtonBase` принадлежит к типу `RoutedEventHandler`. Для получения дополнительной информации см. [Events](../cppcx/events-c-cx.md).

Сначала клиентский код создает экземпляр делегата, используя `ref new` и предоставляя лямбда-выражение, совместимое с сигнатурой делегата, и определяет пользовательское поведение.

[!code-cpp[Cx_delegates#113](../cppcx/codesnippet/CPP/delegatesevents/class1.cpp#113)]

Затем он вызывает функцию-член и передает делегат. Предположим, что `ci` является экземпляром класса `ContactInfo^` и `textBlock` является конструкцией `TextBlock^`XAML-кода.

[!code-cpp[Cx_delegates#114](../cppcx/codesnippet/CPP/delegatesevents/class1.cpp#114)]

В следующем примере клиентское приложение передает пользовательский делегат в открытый метод в среда выполнения Windows компоненте, который выполняет делегат для каждого элемента в `Vector`:

[!code-cpp[Cx_delegates#118](../cppcx/codesnippet/CPP/clientapp/mainpage.xaml.cpp#118)]

[!code-cpp[Cx_delegates#119](../cppcx/codesnippet/CPP/delegatesevents/class1.cpp#119)]

### <a name="construction"></a>Создание экземпляра

Делегат можно создать из любого из следующих объектов:

- лямбда-оператор

- статическая функция;

- указатель на член;

- std::function.

В следующем примере показано, как создать делегат из каждого из этих объектов. Принципы использования делегата абсолютно не зависят от типа объекта, из которого создан его экземпляр.

[!code-cpp[Cx_delegates#115](../cppcx/codesnippet/CPP/delegatesevents/class1.cpp#115)]

> [!WARNING]
> Если используется лямбда-выражение, которое перехватывает указатель "this", необходимо с помощью оператора `-=` явно отменить регистрацию в событии до выхода из лямбда-выражения. Дополнительные сведения см. в статье [Events (Visual Basic)](../cppcx/events-c-cx.md) (События в Visual Basic).

### <a name="generic-delegates"></a>Универсальные делегаты

Универсальные делегаты в C ++/CX имеют ограничения, аналогичные объявлениям универсальных классов. Они не могут объявляться как открытые. Можно объявить закрытый или внутренний универсальный делегат и использовать его в коде C++, но клиенты .NET и JavaScript не смогут использовать его, поскольку такой делегат не попадает в метаданные .winmd. В этом примере объявляется универсальный делегат, который можно использовать только в коде C++:

[!code-cpp[Cx_delegates#116](../cppcx/codesnippet/CPP/delegatesevents/class1.h#116)]

В следующем примере объявляется специальный экземпляр делегата внутри определения класса:

[!code-cpp[Cx_delegates#117](../cppcx/codesnippet/CPP/delegatesevents/class1.h#117)]

## <a name="delegates-and-threads"></a>Делегаты и потоки

Делегат, как и объект функции, содержит код, выполняемый в некий момент в будущем. Если код, который создает и передает делегат, и функция, которая принимает и выполняет этот делегат, выполняются в одном и том же потоке, действия относительно просты. Если этот поток является потоком пользовательского интерфейса, делегат может напрямую манипулировать объектами пользовательского интерфейса, такими как элементы управления XAML.

Если клиентское приложение загружает среда выполнения Windows компонент, работающий в потоковой подразделении, и предоставляет делегат для этого компонента, по умолчанию делегат вызывается непосредственно в потоке STA. Большинство компонентов среда выполнения Windows могут работать в STA или MTA.

Если код, который выполняет делегат, выполняется в другом потоке (например, в контексте объекта concurrency::task), вам необходимо синхронизировать доступ к общим данным. Например, если делегат содержит ссылку на объект Vector и элемент управления XAML содержит ссылку на тот же самый объект Vector, необходимо принять меры, чтобы избежать взаимоблокировки и состояния гонки, которые могут возникнуть, если делегат и элемент управления XAML попытаются обратиться к объекту Vector одновременно. Необходимо также обеспечить, чтобы делегат не пытался захватить с помощью ссылок локальные переменные, которые могут оказаться вне области до того, как произойдет вызов делегата.

Если для созданного делегата требуется обеспечить возможность обратного вызова в том же потоке, где он был создан (например, если он передается компоненту, который выполняется в многопотоковом подразделении), и возможность вызова в том же потоке, что и создавший его код, используйте перегруженный метод конструктора делегата, принимающий второй параметр `CallbackContext` . Используйте этот перегруженный метод только для делегатов, имеющих зарегистрированный прокси или заглушку; не все делегаты, определенные в Windows.winmd, являются зарегистрированными.

Если вы знакомы с обработчиками событий в .NET, вам известно, что перед возникновением события рекомендуется создать его локальную копию. Это позволяет избежать состояния гонки, при котором обработчик события может быть удален непосредственно перед вызовом события. В C++/CX делать это необязательно, поскольку при добавлении и удалении обработчиков событий создается новый список обработчиков. Поскольку объект C++ увеличивает счетчик ссылок в списке обработчиков до вызова события, это гарантирует, что все обработчики будут действительными. Однако это также означает, что если удалить обработчик событий в потоке-потребителе, этот обработчик все равно может быть вызван, если публикующий объект все еще работает со своей копией списка, которая к этому моменту устарела. Публикующий объект не получит обновленный список до следующего вызова события.

## <a name="see-also"></a>См. также

[Система типов](../cppcx/type-system-c-cx.md)<br/>
[Справочник по языку C++/CX](../cppcx/visual-c-language-reference-c-cx.md)<br/>
[Справочник по пространствам имен](../cppcx/namespaces-reference-c-cx.md)
