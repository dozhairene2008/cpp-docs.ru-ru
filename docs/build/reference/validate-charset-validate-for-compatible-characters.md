---
title: /validate-charset (проверка совместимости символов)
ms.date: 02/06/2019
f1_keywords:
- /validate-charset
- validate-charset
helpviewer_keywords:
- /validate-charset compiler option
ms.assetid: 50360fd0-4d32-4a4f-95d0-53d38c12ad4c
ms.openlocfilehash: 2390aa98b9416eb538f529c8c370c888cccf4734
ms.sourcegitcommit: fcb48824f9ca24b1f8bd37d647a4d592de1cc925
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/15/2019
ms.locfileid: "69498162"
---
# <a name="validate-charset-validate-for-compatible-characters"></a>/validate-charset (проверка совместимости символов)

Проверяет, что текст исходного файла содержит только символы, представленные в формате UTF-8.

## <a name="syntax"></a>Синтаксис

```
/validate-charset[-]
```

## <a name="remarks"></a>Примечания

С помощью параметра **/Validate-charset** можно проверить, содержит ли исходный код только символы, которые могут быть представлены как в исходной кодировке, так и в кодировке выполнения. Эта проверка включается автоматически при указании параметров компилятора **указаны кодировки/Source-charset**, **/Execution-charset**или **/UTF-8** . Эту проверку можно явно отключить, указав параметр **/валидате-чарсет-** .

По умолчанию Visual Studio обнаруживает метку порядка следования байтов, чтобы определить, имеет ли исходный файл формат в кодировке Юникод, например UTF-16 или UTF-8. Если метка порядка следования байтов не найдена, предполагается, что исходный файл кодируется с помощью кодовой страницы текущего пользователя, если не указана кодовая страница с помощью **/UTF-8** или параметра **указаны кодировки/Source-charset** . Visual Studio позволяет сохранить C++ исходный код с помощью любой из нескольких кодировок символов. Сведения о кодировках исходного кода и выполнения см. в разделе [наборы символов](../../cpp/character-sets.md) в документации по языку. Список поддерживаемых идентификаторов кодовых страниц и имен наборов символов см. в разделе [идентификаторы кодовых страниц](/windows/win32/Intl/code-page-identifiers).

В Visual Studio в качестве внутреннего кодирования символов используется UTF-8 во время преобразования между исходной кодировкой и кодировкой выполнения. Если символ в исходном файле не может быть представлен в кодировке выполнения, то преобразование UTF-8 подставляет знак вопросительного знака "?". Параметр **/Validate-charset** приводит к тому, что компиляция сообщает о предупреждении, если это происходит.

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Установка данного параметра компилятора в среде разработки Visual Studio

1. Откройте диалоговое окно **Окна свойств** проекта. Подробнее см. в статье [Настройка компилятора C++ и свойств сборки в Visual Studio](../working-with-project-properties.md).

1. Разверните папку **Свойства конфигурации**, **C/C++** , **Командная строка** .

1. В окне **Дополнительные параметры**добавьте параметр **/Validate-charset** и укажите предпочтительную кодировку.

1. Выберите **ОК** для сохранения внесенных изменений.

## <a name="see-also"></a>См. также

[Параметры компилятора MSVC](compiler-options.md)<br/>
[Синтаксис командной строки компилятора MSVC](compiler-command-line-syntax.md)<br/>
[/Execution-charset (Задание кодировки выполнения)](execution-charset-set-execution-character-set.md)<br/>
[/source/charset (задание исходной кодировки)](source-charset-set-source-character-set.md)<br/>
[/utf/8 (указание UTF/8 в качестве исходной кодировки и кодировки исполняемого файла)](utf-8-set-source-and-executable-character-sets-to-utf-8.md)
