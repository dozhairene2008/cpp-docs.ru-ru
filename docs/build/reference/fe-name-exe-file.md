---
title: /Fe (именование EXE-файла)
ms.date: 11/04/2016
f1_keywords:
- /fe
helpviewer_keywords:
- -Fe compiler option [C++]
- executable files, renaming
- rename file compiler option [C++]
- /Fe compiler option [C++]
- Fe compiler option [C++]
ms.assetid: 49f594fd-5e94-45fe-a1bf-7c9f2abb6437
ms.openlocfilehash: 5901ef1997cfea84c97b6d91b30335ff7dbc1d9f
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62292619"
---
# <a name="fe-name-exe-file"></a>/Fe (именование EXE-файла)

Указывает имя и каталог для файла .exe или библиотеку DLL, созданную компилятором.

## <a name="syntax"></a>Синтаксис

> **/FE**[_pathname_] **/Fe:** _pathname_

### <a name="arguments"></a>Аргументы

*имя пути*<br/>
Относительный или абсолютный путь и базовое имя файла или относительный или абсолютный путь к каталогу или базовое имя файла для создаваемого исполняемого файла.

## <a name="remarks"></a>Примечания

**/Fe** параметр позволяет указать в выходной каталог, имя исполняемого файла выходных данных или на созданный исполняемый файл. Если *pathname* заканчивается на разделитель пути (**&#92;**), предполагается, чтобы указать только в выходной каталог. В противном случае — последний компонент *pathname* используется в качестве базового имени выходного файла, а остальная часть *pathname* задает выходной каталог. Если *pathname* не поддерживает все разделители путей, предполагается, чтобы указать имя выходного файла в текущем каталоге. *Pathname* должны заключаться в двойные кавычки (**"**) если он содержит символы, которые не могут находиться в короткий путь, например пробелы, символы расширенного набора символов или компоненты пути больше восьми долго.

Когда **/Fe** параметр не указан, или при создании базового файла имя не указано в *pathname*, компилятор придает выходному файлу имя по умолчанию, используя базовое имя первого файла источника или объекта, указанного в командной строке и расширением .exe или .dll.

Если указать [/c (компиляция без связывания)](c-compile-without-linking.md) параметр, **/Fe** не оказывает влияния.

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Установка данного параметра компилятора в среде разработки Visual Studio

1. Откройте диалоговое окно **Страницы свойств** проекта. Дополнительные сведения см. в разделе [свойств компилятора и собранной задать C++ в Visual Studio](../working-with-project-properties.md).

1. Откройте **свойства конфигурации** > **компоновщика** > **Общие** страницу свойств.

1. Изменить **выходной файл** свойство. Выберите **ОК** для сохранения внесенных изменений.

### <a name="to-set-this-compiler-option-programmatically"></a>Установка данного параметра компилятора программным способом

- См. раздел <xref:Microsoft.VisualStudio.VCProjectEngine.VCLinkerTool.OutputFile%2A>.

## <a name="example"></a>Пример

Следующая команда компилирует и связывает все исходные файлы C в текущем каталоге. Полученный исполняемый файл называется PROCESS.exe и создается в каталоге «Project\bin Name\repos\My C:\Users\User».

```
CL /Fe"C:\Users\User Name\repos\My Project\bin\PROCESS" *.C
```

## <a name="example"></a>Пример

Следующая команда создает исполняемый файл в `C:\BIN` с тем же базовым именем, что и первый исходный файл в текущем каталоге:

```
CL /FeC:\BIN\ *.C
```

## <a name="see-also"></a>См. также

[Параметры выходного файла (/F)](output-file-f-options.md)<br/>
[Параметры компилятора MSVC](compiler-options.md)<br/>
[Синтаксис командной строки компилятора MSVC](compiler-command-line-syntax.md)<br/>
[Указание пути](specifying-the-pathname.md)<br/>
