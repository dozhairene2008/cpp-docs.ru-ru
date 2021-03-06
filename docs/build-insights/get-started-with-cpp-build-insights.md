---
title: Начало работы с аналитикой сборки C++
description: Общий обзор аналитических сведений о C++ сборке.
ms.date: 11/03/2019
helpviewer_keywords:
- C++ Build Insights
- throughput analysis
- build time analysis
- vcperf.exe
ms.openlocfilehash: 2a5799fecc885b96f4278e0f5077662ce5fd7c8f
ms.sourcegitcommit: 3e8fa01f323bc5043a48a0c18b855d38af3648d4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/05/2020
ms.locfileid: "78332011"
---
# <a name="get-started-with-c-build-insights"></a>Начало работы с аналитикой сборки C++

::: moniker range="<=vs-2017"

Средства C++ сборки Insights доступны в Visual Studio 2019. Чтобы просмотреть документацию по этой версии, присвойте элементу управления выбора версии Visual Studio для этой статьи значение Visual Studio 2019.

::: moniker-end
::: moniker range="vs-2019"

C++Аналитика сборки — это набор средств, обеспечивающих улучшенную видимость цепочки инструментов Microsoft C++ Visual (компилятором MSVC). Средства собираются данные о C++ сборках и представляют их в формате, который может помочь ответить на распространенные вопросы, например:

- Все ли сборки в достаточной степени параллелизации?
- Что следует включить в предварительно скомпилированный заголовок (PCH)?
- Есть ли определенная узкие места, на которую я должен сосредоточиться, чтобы увеличить скорость сборки?

Основные компоненты этой технологии:

- *вкперф. exe*— служебная программа командной строки, которую можно использовать для получения трассировок для сборок,
- расширение Windows Performance Analyzer (WPA), позволяющее просматривать трассировки сборок в WPA и
- пакет C++ SDK для Build Insights — пакет разработки программного обеспечения для создания собственных средств, использующих C++ данные о сборке.

Чтобы быстро приступить к работе с этими компонентами, щелкните приведенные ниже ссылки.

[Учебник. вкперф и анализатор производительности Windows](tutorials/vcperf-and-wpa.md)\
Узнайте, как собирать трассировки сборок для C++ проектов и как просматривать их в WPA.

[Учебник. Основные сведения о производительности Windows](tutorials/wpa-basics.md)\
Ознакомьтесь с полезными советами по использованию WPA для анализа трассировок сборки.

[\ SDK для сборки Insights C++ ](reference/sdk/overview.md)
Обзор пакета SDK для C++ Build Insights.

::: moniker-end
