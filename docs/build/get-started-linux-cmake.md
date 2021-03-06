---
title: Создание кроссплатформенных проектов C++ в Visual Studio
description: Как настроить, скомпилировать и отладить проект CMak с C++ открытым исходным кодом в Visual Studio, предназначенный для Linux и Windows.
ms.topic: tutorial
ms.date: 01/08/2020
ms.openlocfilehash: 83d71d3078e892a51aef159b225fecec2b581f20
ms.sourcegitcommit: 5f276064779d90a4cfda758f89e0c0f1e4d1a188
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/09/2020
ms.locfileid: "75791767"
---
# <a name="tutorial-create-c-cross-platform-projects-in-visual-studio"></a>Учебник. Создание C++ кросс-платформенных проектов в Visual Studio

Разработка Visual Studio C и C++ теперь подходит не только для Windows. В этом руководстве показано, как использовать Visual Studio C++ для межплатформенной разработки в Windows и Linux. Он основан на CMak, поэтому вам не нужно создавать или создавать проекты Visual Studio. При открытии папки, содержащей файл CMakeLists. txt, Visual Studio автоматически настраивает IntelliSense и параметры сборки. Вы можете быстро начать редактирование, сборку и отладку кода локально в Windows. Затем переключите конфигурацию для того, чтобы сделать то же самое в Linux, в Visual Studio.

В этом руководстве вы узнаете, как:

> [!div class="checklist"]
> * Клонировать проект CMake с открытым кодом с сайта GitHub.
> * Открывать проект в Visual Studio.
> * Собирать и отлаживать исполняемый целевой объект на Windows.
> * Добавлять подключение к компьютеру Linux.
> * Собирать и отлаживать тот же целевой объект в Linux.

## <a name="prerequisites"></a>Prerequisites

* Настройка Visual Studio для кроссплатформенной разработки на C++
  * Сначала [установите Visual Studio](https://visualstudio.microsoft.com/vs/) и выберите разработку **классических приложений с C++**  и **Linux с C++ рабочими нагрузками**. Минимальная установка составляет всего 3 ГБ. В зависимости от скорости загрузки установка не должна занять более 10 минут.

* Настройка компьютера Linux для кроссплатформенной разработки на C++
  * Visual Studio не требует конкретный дистрибутив Linux. Операционная система может работать на физическом компьютере, на виртуальной машине или в облаке. Кроме того, можно использовать подсистему Windows для Linux (WSL). Однако для этого руководства требуется графическая среда. WSL не рекомендуется использовать здесь, так как он предназначен в основном для операций командной строки.
  * Для Visual Studio требуются следующие средства на компьютере Linux: C++ компиляторы, gdb, SSH, rsync и ZIP. В системах на основе Debian эту команду можно использовать для установки этих зависимостей:

    ```cmd
    sudo apt install -y openssh-server build-essential gdb rsync zip
    ```

  * Для Visual Studio требуется последняя версия CMak на компьютере Linux с включенным режимом сервера (по крайней мере 3,8). Корпорация Майкрософт предлагает универсальную сборку CMake, которую можно установить на любой дистрибутив Linux. Мы рекомендуем использовать эту сборку, чтобы убедиться в наличии новейших функций. Вы можете получить двоичные файлы CMake из [вилки Майкрософт репозитория CMake](https://github.com/Microsoft/CMake/releases) на сайте GitHub. Перейдите на эту страницу и Скачайте версию, соответствующую архитектуре системы на компьютере Linux, а затем пометьте ее как исполняемый файл:

    ```cmd
    wget <path to binary>
    chmod +x cmake-3.11.18033000-MSVC_2-Linux-x86_64.sh
    ```

  * Вы увидите параметры для запуска скрипта с `-–help`. Рекомендуется использовать параметр `–prefix`, чтобы указать установку в пути **/usr** , так как **/УСР/бин** является расположением по умолчанию, в котором Visual Studio ищет CMAK. В следующем примере показан скрипт Linux x86_64. При необходимости измените его, если вы используете другую целевую платформу.

    ```cmd
    sudo ./cmake-3.11.18033000-MSVC_2-Linux-x86_64.sh --skip-license --prefix=/usr
    ```

* Git для Windows, установленный на компьютере Windows.
* Учетная запись GitHub.

## <a name="clone-an-open-source-cmake-project-from-github"></a>Клонирование проекта CMake с открытым кодом с сайта GitHub

В этом руководстве используется маркер "физический пакет SDK" на GitHub. Он обеспечивает обнаружение столкновений и физическое моделирование для многих приложений. Пакет SDK включает примеры исполняемых программ, которые компилируются и выполняются без необходимости написания дополнительного кода. В этом руководстве не рассматривается изменение исходного кода или скриптов сборки. Чтобы начать, клонировать репозиторий *bullet3* из GitHub на компьютере, где установлена Visual Studio.

```cmd
git clone https://github.com/bulletphysics/bullet3.git
```

1. В главном меню Visual Studio выберите **файл > открыть > CMAK**. Перейдите к файлу CMakeLists. txt в корне только что скачанного репозитория bullet3.

    ![Меню Visual Studio: Файл > Открыть > CMake](media/cmake-open-cmake.png)

    После открытия папки структура папок становится видимой в **Обозреватель решений**.

    ![Представление папки в обозревателе решений Visual Studio](media/cmake-bullet3-solution-explorer.png)

    В этом представлении показано, что фактически находится на диске. Это не логическое или отфильтрованное представление. По умолчанию оно не показывает скрытые файлы.

1. Нажмите кнопку **Показать все файлы** , чтобы просмотреть все файлы в папке.

    ![Кнопка "Показать все файлы" в обозревателе решений Visual Studio](media/cmake-bullet3-show-all-files.png)

## <a name="switch-to-targets-view"></a>Переключение на представление целевых объектов

Когда вы откроете папку, которая использует CMake, Visual Studio автоматически создаст кэш CMake. Эта операция может занять некоторое время в зависимости от размера проекта.

1. В **окне вывода** выберите **Показать выходные данные из** и выберите **CMake** для отслеживания состояния процесса создания кэша. По завершении операции отображается надпись: "Извлечение сведений о целевом объекте выполнено".

   ![Окно вывода Visual Studio с выходными данными из CMake](media/cmake-bullet3-output-window.png)

   После завершения этой операции будет настроена технология IntelliSense. Можно выполнить сборку проекта и отладить приложение. Теперь Visual Studio отображает логическое представление решения на основе целевых объектов, указанных в файлах CMakeLists.

1. Нажмите кнопку **Решения и папки** в **обозревателе решений**, чтобы переключиться на представление целевых объектов CMake.

   ![Кнопка "Решения и папки" в обозревателе решений для вывода представления целевых объектов CMake](media/cmake-bullet3-show-targets.png)

   Вот как это представление выглядит для пакета SDK Bullet:

   ![Представление целевых объектов CMake в обозревателе решений](media/cmake-bullet3-targets-view.png)

   Представление целевых объектов обеспечивает более интуитивное отображение содержимого исходной базы. Вы увидите, что некоторые целевые объекты являются библиотеками, а другие — исполняемыми файлами.

1. Разверните узел в представлении целевых объектов CMake, чтобы просмотреть его файлы исходного кода, где бы эти файлы ни находились на диске.

## <a name="add-an-explicit-windows-x64-debug-configuration"></a>Добавление явной конфигурации Windows x64-Debug

Visual Studio создает конфигурацию **x64-Debug** по умолчанию для Windows. Конфигурации указывают Visual Studio, какую платформу она будет использовать для CMake. Конфигурация по умолчанию не представлена на диске. При явном добавлении конфигурации Visual Studio создает файл с именем *CMakeSettings. JSON*. Он заполняется параметрами для всех указанных конфигураций.

1. Добавьте новую конфигурацию. Откройте раскрывающийся список **Конфигурация** на панели инструментов и выберите **Управление конфигурациями**.

   ![Раскрывающийся список управления конфигурациями](media/cmake-bullet3-manage-configurations.png)

   Откроется [Редактор параметров CMAK](customize-cmake-settings.md) . Щелкните зеленый знак «плюс» в левой части редактора, чтобы добавить новую конфигурацию. Откроется диалоговое окно **Добавление конфигурации в CMakeSettings** .

   ![Диалоговое окно "Добавление конфигурации в CMakeSettings"](media/cmake-bullet3-add-configuration-x64-debug.png)

   В этом диалоговом окне отображаются все конфигурации, входящие в состав Visual Studio, а также все созданные пользовательские конфигурации. Если вы хотите продолжить использовать конфигурацию **x64-Debug** , она должна быть первой из добавленных. Выберите **x64-Debug**, а затем нажмите кнопку **выбрать** . Visual Studio создает файл CMakeSettings. JSON с конфигурацией для **x64-Debug**и сохраняет ее на диске. Вы можете назвать конфигурацию как угодно, изменив параметр имени непосредственно в CMakeSettings.json.

## <a name="set-a-breakpoint-build-and-run-on-windows"></a>Установка точки останова, сборка и запуск в Windows

На этом шаге нам предстоит отладить пример программы, демонстрирующий библиотеку Bullet Physics.
  
1. В **обозревателе решений** выберите AppBasicExampleGui и разверните его.

1. Откройте файл `BasicExample.cpp`.

1. Установите точку останова, которая будет достигнута при щелчке в работающем приложении. Событие щелчка обрабатывается в методе внутри вспомогательного класса. Для быстрого перехода:

   1. Выберите `CommonRigidBodyBase`, производным `BasicExample` структуры. Это около строки 30.

   1. Щелкните правой кнопкой мыши и выберите **Перейти к определению**. Теперь вы находитесь в заголовке Коммонригидбодибасе. h.

   1. В представлении браузера над источником вы увидите, что вы находитесь в `CommonRigidBodyBase`. Справа можно выбрать элементы для проверки. Откройте раскрывающийся список и выберите `mouseButtonCallback`, чтобы перейти к определению этой функции в заголовке.

      ![Панель инструментов со списком элементов Visual Studio](media/cmake-bullet3-member-list-toolbar.png)

1. Поместите точку останова на первой строке в этой функции. Это достигается при нажатии кнопки мыши в окне приложения при запуске в отладчике Visual Studio.

1. Чтобы запустить приложение, выберите раскрывающийся список запуск на панели инструментов. Это значок с зеленым значком воспроизведения с текстом "выберите элемент автозагрузки". В раскрывающемся списке выберите Аппбасицексамплегуи. exe. Имя исполняемого файла теперь отображается на кнопке запуска:

   ![Раскрывающийся список запуска на панели инструментов Visual Studio, "Выбрать элемент запуска"](media/cmake-bullet3-launch-button.png)

1. Нажмите кнопку запустить, чтобы создать приложение и необходимые зависимости, а затем запустите его с присоединенным отладчиком Visual Studio. Через некоторое время появится работающее приложение:

   ![Отладка приложения Windows в Visual Studio](media/cmake-bullet3-launched.png)

1. Переместите указатель мыши в окно приложения, а затем нажмите кнопку для вызова точки останова. Точка останова переводит Visual Studio обратно на передний план, а в редакторе отображается строка, где выполнение приостанавливается. Вы можете просматривать переменные приложения, объекты, потоки и память, а также пошагово выполнять код в интерактивном режиме. Нажмите кнопку **продолжить** , чтобы разрешить возобновление работы приложения, а затем закройте его в обычном режиме. Или остановите выполнение в Visual Studio с помощью кнопки Остановить.

## <a name="add-a-linux-configuration-and-connect-to-the-remote-machine"></a>Добавление конфигурации Linux и подключение к удаленному компьютеру

1. Добавьте конфигурацию Linux. Щелкните правой кнопкой мыши файл CMakeSettings.json в **обозревателе решений** и выберите **Добавить конфигурацию**. Вы увидите то же диалоговое окно "Добавление конфигурации в CMakeSettings", что и раньше. Выберите **Linux — отладить** в это время, а затем сохраните файл CMakeSettings. JSON (Ctrl + s).

1. Выберите **Linux-Debug** в раскрывающемся списке Конфигурация.

   ![Раскрывающийся список конфигурации запуска с вариантами X64-Debug и Linux-Debug](media/cmake-bullet3-linux-configuration-item.png)

   Если вы подключаетесь к системе Linux в первый раз, появляется диалоговое окно **Подключение к удаленной системе** .

   ![Диалоговое окно "Подключение к удаленной системе" в Visual Studio](media/cmake-bullet3-connection-manager.png)

   Если вы уже добавили удаленное подключение, это окно можно открыть, перейдя в **меню сервис > параметры > кросс-платформенные > диспетчер подключений**.

1. Укажите [сведения о подключении к компьютеру Linux](/cpp/linux/connect-to-your-remote-linux-computer) и нажмите кнопку **подключить**. Visual Studio добавит этот компьютер как CMakeSettings. JSON в качестве подключения по умолчанию для **Linux-Debug**. Он также извлекает заголовки с удаленного компьютера, поэтому вы получаете функцию [IntelliSense, относящуюся к этому удаленному подключению](/cpp/linux/configure-a-linux-project?view=vs-2019#remote_intellisense). Затем Visual Studio отправляет файлы на удаленный компьютер и создает кэш CMak в удаленной системе. Выполнение этих действий может занять некоторое время в зависимости от скорости работы сети и возможностей удаленного компьютера. Вы узнаете, что она завершена, когда в окне «Вывод диспетчера подключений» появляется сообщение «Извлечение целевых сведений завершено».

## <a name="set-a-breakpoint-build-and-run-on-linux"></a>Установка точки останова, сборка и выполнение в Linux

Поскольку это приложение для настольных компьютеров, необходимо предоставить дополнительные сведения о конфигурации для конфигурации отладки.

1. В представлении "цели CMak" щелкните правой кнопкой мыши Аппбасицексамплегуи и выберите **параметры отладки и запуска** , чтобы открыть файл Launch. vs. JSON, находящийся в вложенной папке Hidden **. VS** . Этот локальный файл для среды разработки. Вы можете переместить его в корень проекта, если хотите проверить его и сохранить для своей команды. В этом файле добавлена конфигурация для Аппбасицексамплегуи. Эти параметры по умолчанию работают в большинстве случаев, но не здесь. Поскольку это приложение для настольных компьютеров, необходимо предоставить некоторую дополнительную информацию для запуска программы, чтобы ее можно было увидеть на компьютере Linux.

1. Чтобы найти значение переменной среды `DISPLAY` на компьютере Linux, выполните следующую команду:

   ```cmd
   echo $DISPLAY
   ```

   В конфигурации для Аппбасицексамплегуи имеется массив параметров «pipeArgs». Он содержит строку "$ {Дебугжеркомманд}". Это команда, запускающая gdb на удаленном компьютере. Visual Studio должна экспортировать отображение в этот контекст перед выполнением этой команды. Например, если значение дисплея `:1`, измените эту строку следующим образом:

   ```cmd
   "export DISPLAY=:1;${debuggerCommand}",
   ```

1. Запустите и отладить приложение. Откройте раскрывающийся список **Выбрать запускаемый элемент** на панели инструментов и выберите **аппбасицексамплегуи**. Затем либо выберите зеленый значок воспроизведения на панели инструментов, либо нажмите клавишу **F5**. Приложение и его зависимости создаются на удаленном компьютере Linux, а затем запускаются с присоединенным отладчиком Visual Studio. На удаленном компьютере Linux вы увидите окно приложения.

1. Переместите указатель мыши в окно приложения и нажмите кнопку. Попадание в точку останова. Выполнение программы приостанавливается, Visual Studio возвращается на передний план, и вы видите свою точку останова. Кроме того, вы увидите окно консоли Linux в Visual Studio. Окно предоставляет выходные данные удаленной машины Linux и может также принимать входные данные для `stdin`. Как и любое окно Visual Studio, вы можете закрепить его там, где вы предпочитаете его просмотреть. Его расположение сохраняется в будущих сеансах.

   ![Окно консоли Linux в Visual Studio](media/cmake-bullet3-linux-console.png)

1. Вы можете проверить переменные, объекты, потоки и память приложения и пошагово выполнить код с помощью Visual Studio. Но на этот раз все это выполняется на удаленном компьютере Linux, а не в локальной среде Windows. Можно выбрать вариант **продолжить** , чтобы приложение продолжило нормальное завершение работы, или нажать кнопку «прекратить», как и локальное выполнение.

1. Посмотрите на окно стека вызовов и увидите вызовы к `x11OpenGLWindow`, поскольку среда Visual Studio запустила приложение в Linux.

   ![Окно стека вызовов со стеком вызовов Linux](media/cmake-bullet3-linux-callstack.png)

## <a name="what-you-learned"></a>Чему вы научились

В этом руководстве вы клонировать базу кода непосредственно из GitHub. Вы создали, выполнили и отлаживать его в Windows без изменений. Затем вы использовали одну и ту же базу кода с незначительными изменениями конфигурации для сборки, запуска и отладки на удаленном компьютере Linux.

## <a name="next-steps"></a>Следующие шаги

Дополнительные сведения о настройке и отладке проектов CMake в Visual Studio:

> [!div class="nextstepaction"]
> [Проекты CMake в Visual Studio](cmake-projects-in-visual-studio.md)<br/><br/>
> [Настройка проекта Linux CMake](../linux/cmake-linux-project.md)<br/><br/>
> [Подключение к удаленному компьютеру Linux](../linux/connect-to-your-remote-linux-computer.md)<br/><br/>
> [Настройка параметров сборки CMake](customize-cmake-settings.md)<br/><br/>
> [Настройка сеансов отладки CMake](configure-cmake-debugging-sessions.md)<br/><br/>
> [Развертывание, запуск и отладка проекта Linux](../linux/deploy-run-and-debug-your-linux-project.md)<br/><br/>
> [Справочник по предопределенной конфигурации CMake](cmake-predefined-configuration-reference.md)
>
