---
title: Свойства копирования источников проекта (Linux C++)
ms.date: 10/16/2019
ms.assetid: 1a44230d-5dd8-4d33-93b4-e77e03e00150
ms.openlocfilehash: bc99814e825cda091b6a0b00256ca2d8269ecdd3
ms.sourcegitcommit: 069e3833bd821e7d64f5c98d0ea41fc0c5d22e53
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2019
ms.locfileid: "74305392"
---
# <a name="copy-sources-project-properties-linux-c"></a>Свойства копирования источников проекта (Linux C++)

::: moniker range="vs-2015"

Поддержка Linux реализована в Visual Studio версии 2017 и выше.

::: moniker-end

::: moniker range=">=vs-2017"

Свойства, заданные на этой странице свойств, применяются ко всем файлам в проекте, за исключением тех, свойства уровня файла которых уже заданы.

Свойство. | ОПИСАНИЕ
--- | ---
Источники для копирования | Задает источники для копирования в удаленную систему. Изменение этого списка может сдвинуть или иным способом повлиять на структуру каталогов, в которые файлы будут копироваться на удаленной системе.
Копирование источников | Определяет, требуется ли копировать источники в удаленную систему.
Дополнительные источники для копирования | Задает дополнительные источники для копирования в удаленную систему. При необходимости можно указать список в виде пар сопоставлений локальной и удаленной версии со следующим синтаксисом: fulllocalpath1:=fullremotepath1;fulllocalpath2:=fullremotepath2, где локальный файл можно скопировать в указанное удаленное расположение в удаленной системе.

@SourcesToCopyRemotely и @DataFilesToCopyRemotely ссылаются на группы элементов в файле проекта. Чтобы изменить источники или файлы данных для удаленного копирования, отредактируйте файл *VCXPROJ*, как показано далее.

```xml
<ItemGroup>
   <MyItems Include="foo.txt" />
   <MyItems Include="bar.txt" />
   <DataFilesToCopyRemotely Include="@(MyItems)" />
</ItemGroup>
```

::: moniker-end
