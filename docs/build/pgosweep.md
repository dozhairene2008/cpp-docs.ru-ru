---
title: pgosweep
ms.date: 03/14/2018
helpviewer_keywords:
- pgosweep program
- profile-guided optimizations, pgosweep
ms.assetid: f39dd3b7-1cd9-4c3b-8e8b-fb794744b757
ms.openlocfilehash: 3ba31671fc3794e1cc959d86d914ba1eef2e01e4
ms.sourcegitcommit: c6f8e6c2daec40ff4effd8ca99a7014a3b41ef33
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/24/2019
ms.locfileid: "64341187"
---
# <a name="pgosweep"></a>pgosweep

Используется в профильной оптимизации для записи всех данных профиля из выполняющейся программы к PGC-файл.

## <a name="syntax"></a>Синтаксис

> **pgosweep** [*параметры*] *изображение* *pgcfile*

### <a name="parameters"></a>Параметры

*options*<br/>
(Необязательно) Допустимые значения для *параметры* являются:

- **/?** или **/help** отображает сообщение справки.

- **вычистки** ведет счет в структур данных времени выполнения.

*Изображение*<br/>
Полный путь файла .exe или .dll, который был создан с помощью [/genprofile](reference/genprofile-fastgenprofile-generate-profiling-instrumented-build.md), [/fastgenprofile](reference/genprofile-fastgenprofile-generate-profiling-instrumented-build.md), или [/LTCG: PGINSTRUMENT](reference/ltcg-link-time-code-generation.md) параметр.

*pgcfile*<br/>
PGC-файл, где эта команда записывает данные счетчиков.

## <a name="remarks"></a>Примечания

**Pgosweep** команда работает для программ, которые были созданы с помощью [/genprofile или/fastgenprofile](reference/genprofile-fastgenprofile-generate-profiling-instrumented-build.md) параметр или устаревший [/LTCG: PGINSTRUMENT](reference/ltcg-link-time-code-generation.md) параметр. Он прерывает выполнение программы и записывает данные профиля для нового PGC-файл. По умолчанию команда сбрасывает счетчики после каждой операции записи. Если указать **вычистки** параметр, команда будет записывать значения, но не сбросить их в выполняющейся программе. Этот параметр обеспечивает повторяющихся данных, если впоследствии извлекать данные профиля.

Вариантом использования **pgosweep** — для получения сведений о профиле для нормальной работы приложения. Например, можно выполнить **pgosweep** вскоре после запуска приложения и отменить этот файл. Это приведет к удалению данных профиля, связанный с издержками при запуске. Затем можно выполнить **pgosweep** до завершения работы приложения. Теперь собранные данные включают данные профиля, только от времени пользователь может взаимодействовать с программой.

Имени PGC-файл (с помощью *pgcfile* параметр) можно использовать стандартный формат, который является *appname! n*.pgc. Если вы используете этот формат, компилятор автоматически обнаруживает эти данные в **/LTCG/useprofile** или **LTCG: PGO** этапа. Если вы не используете стандартный формат, необходимо использовать [pgomgr](pgomgr.md) для слияния PGC-файлы.

> [!NOTE]
> Это средство можно запустить только из командной строки разработчика Visual Studio. В системной командной строке или проводнике это невозможно.

Сведения о том, как собирать данные из профиля в исполняемый файл, см. в разделе [использованием PgoAutoSweep](pgoautosweep.md).

## <a name="example"></a>Пример

В этом примере команда **pgosweep** записывает текущие данные профиля для myapp.exe myapp!1.pgc.

`pgosweep myapp.exe myapp!1.pgc`

## <a name="see-also"></a>См. также

[Профильная оптимизация](profile-guided-optimizations.md)<br/>
[PgoAutoSweep](pgoautosweep.md)<br/>
