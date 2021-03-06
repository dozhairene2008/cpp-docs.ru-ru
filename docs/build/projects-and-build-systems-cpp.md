---
title: C/C++ проекты и системы сборки в Visual Studio
ms.description: Use Visual Studio to compile and build C++ projects for Windows, ARM or Linux based on any project system.
ms.date: 07/17/2019
helpviewer_keywords:
- builds [C++]
- C++ projects, building
- projects [C++], building
- builds [C++], options
- C++, build options
ms.assetid: fa6ed4ff-334a-4d99-b5e2-a1f83d2b3008
ms.topic: overview
ms.openlocfilehash: 3d82ac4569e06a4472047a79da60032ad2db43ca
ms.sourcegitcommit: 8e285a766523e653aeeb34d412dc6f615ef7b17b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/21/2020
ms.locfileid: "80078473"
---
# <a name="cc-projects-and-build-systems-in-visual-studio"></a>C/C++ проекты и системы сборки в Visual Studio

Visual Studio можно использовать для изменения, компиляции и сборки любой C++ базы кода с полной поддержкой IntelliSense без преобразования этого кода в проект Visual Studio или при компиляции с набором инструментов компилятором MSVC. Например, можно изменить кросс-платформенный проект CMak в Visual Studio на компьютере Windows, а затем скомпилировать его для Linux с помощью g + + на удаленном компьютере Linux.

## <a name="c-compilation"></a>C++компиляции

Для *создания* C++ программы означает компиляцию исходного кода из одного или нескольких файлов, а затем связывание этих файлов с исполняемым файлом (exe), библиотекой динамической загрузки (DLL) или статической библиотекой (lib).

Базовая C++ компиляция включает в себя три основных этапа:

- C++ Препроцессор преобразует все #directives и определения макросов в каждом исходном файле. При этом создается *блок преобразования*.
- C++ Компилятор компилирует каждую единицу преобразования в объектные файлы (obj), применяя все установленные параметры компилятора.
- *Компоновщик* объединяет объектные файлы в один исполняемый файл, применяя параметры компоновщика, которые были установлены.

## <a name="the-msvc-toolset"></a>Набор инструментов КОМПИЛЯТОРОМ MSVC

Компилятор Microsoft C++ , компоновщик, стандартные библиотеки и связанные служебные программы составляют набор инструментов компилятора компилятором MSVC (также называемый цепочки инструментов или "средства сборки"). Они включены в Visual Studio. Вы также можете скачать и использовать набор инструментов в качестве отдельного пакета бесплатно из [расположения для загрузки средств сборки для Visual Studio 2019](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2019).

Вы можете создавать простые программы, вызывая компилятор КОМПИЛЯТОРОМ MSVC (Cl. exe) непосредственно из командной строки. Следующая команда принимает один файл исходного кода и вызывает cl. exe для создания исполняемого файла *Hello. exe*:

```cmd
cl /EHsc hello.cpp
```

Обратите внимание, что здесь компилятор (Cl. exe) автоматически вызывает C++ препроцессор и компоновщик для создания окончательного выходного файла.  Дополнительные сведения см. в разделе [Сборка в командной строке](building-on-the-command-line.md).

## <a name="build-systems-and-projects"></a>Создание систем и проектов

Большинство реальных программ используют какую-либо *систему сборки* для управления сложностью компиляции нескольких исходных файлов для нескольких конфигураций (т. е. Отладка и выпуск), нескольких платформ (x86, x64, ARM и т. д.), настраиваемых шагов сборки и даже нескольких исполняемых файлов, которые должны быть скомпилированы в определенном порядке. Вы создаете параметры в файлах конфигурации сборки, и система сборки принимает этот файл в качестве входных данных перед вызовом компилятора. Набор файлов исходного кода и файлов конфигурации сборки, необходимых для построения исполняемого файла, называется *проектом*.

В следующем списке приведены различные варианты для проектов Visual Studio C++:

- Создайте проект Visual Studio с помощью интегрированной среды разработки Visual Studio и настройте его с помощью страниц свойств. Проекты Visual Studio создают программы, работающие в Windows. Общие сведения см. в разделе [Компиляция и сборка](/visualstudio/ide/compiling-and-building-in-visual-studio) документации по Visual Studio.

- Откройте папку, содержащую файл CMakeLists. txt. Поддержка CMak интегрирована в Visual Studio. Интегрированную среду разработки можно использовать для редактирования, тестирования и отладки, не изменяя файлы CMak каким-либо образом. Это позволяет работать в том же проекте CMak, что и другие пользователи, которые могут использовать разные редакторы. Для кросс-платформенной разработки рекомендуется использовать CMak. Дополнительные сведения см. в статье о [проектах CMAK](cmake-projects-in-visual-studio.md).

- Откройте свободную папку исходных файлов без файла проекта. Visual Studio будет использовать эвристику для создания файлов. Это простой способ компиляции и запуска небольших консольных приложений. Дополнительные сведения см. в разделе [проекты открытых папок](open-folder-projects-cpp.md).

- Откройте папку, содержащую файл makefile или любой другой конфигурационную систему сборки. Вы можете настроить Visual Studio для вызова любой произвольной команды сборки, добавив JSON Files в папку. Дополнительные сведения см. в разделе [проекты открытых папок](open-folder-projects-cpp.md).

- Откройте файл Makefile Windows в Visual Studio. Дополнительные сведения см. в [справочнике по NMAKE](reference/nmake-reference.md).

## <a name="msbuild-from-the-command-line"></a>MSBuild из командной строки

Вы можете вызвать MSBuild из командной строки, передав ему VCXPROJ-файл вместе с параметрами командной строки. Этот подход требует хорошего понимания MSBuild и рекомендуется только в случае крайней необходимости. Дополнительные сведения см. в разделе [MSBuild](msbuild-visual-cpp.md).

## <a name="in-this-section"></a>в этом разделе

[Проекты Visual Studio](creating-and-managing-visual-cpp-projects.md) Создание, Настройка и сборка C++ проектов в Visual Studio с помощью собственной системы сборки (MSBuild).

[Проекты CMAK](cmake-projects-in-visual-studio.md) Создание кода, создание и развертывание проектов CMak в Visual Studio.

[Открыть проекты папок](open-folder-projects-cpp.md) Использование Visual Studio для написания кода, сборки и развертывания C++ проектов на основе любой произвольной системы сборки или отсутствия системы сборки. Совсем.

[Сборки выпуска](release-builds.md) Как создавать и устранять неполадки оптимизированных сборок выпуска для развертывания конечным пользователям.

[Использование набора средств MSVC из командной строки](building-on-the-command-line.md)<br/>
Описывает, как использовать C/C++ компилятор и средства сборки непосредственно из командной строки, а не с помощью интегрированной среды разработки Visual Studio.

[Создание библиотек DLL в Visual Studio](dlls-in-visual-cpp.md) Создание, отладка и развертывание библиотек C/C++ DLL (общие библиотеки) в Visual Studio.

[Пошаговое руководство. Создание и использование статической библиотеки](walkthrough-creating-and-using-a-static-library-cpp.md) Создание двоичного файла. lib.

[Создание приложений CC++ /изолированного приложения и параллельных сборок](building-c-cpp-isolated-applications-and-side-by-side-assemblies.md) Описывает модель развертывания для классических приложений Windows, основанную на идее изолированных приложений и параллельных сборок.

[Настройка C++ проектов для 64-разрядных целевых объектов x64](configuring-programs-for-64-bit-visual-cpp.md) Как ориентироваться на 64-разрядное оборудование x64 с помощью средств сборки КОМПИЛЯТОРОМ MSVC.

[Настройка C++ проектов для процессоров ARM](configuring-programs-for-arm-processors-visual-cpp.md) Использование средств сборки КОМПИЛЯТОРОМ MSVC для целевого оборудования ARM.

[Оптимизация кода](optimizing-your-code.md) Как оптимизировать код различными способами, включая оптимизацию программы.

[Настройка программ для Windows XP](configuring-programs-for-windows-xp.md) Как ориентироваться на Windows XP с помощью средств сборки КОМПИЛЯТОРОМ MSVC.

[Справочные сведения о сборке C/C++](reference/c-cpp-building-reference.md)<br/>
Содержит ссылки на справочные статьи о сборке программ на C++, о параметрах компилятора и компоновщика, а также о различных средствах сборки.
