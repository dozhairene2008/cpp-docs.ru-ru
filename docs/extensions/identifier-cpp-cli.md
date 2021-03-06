---
title: __identifier (C++/CLI)
ms.date: 10/12/2018
ms.topic: reference
f1_keywords:
- __identifier
- __identifier_cpp
helpviewer_keywords:
- __identifier keyword [C++]
ms.assetid: 348428af-afa7-4ff3-b571-acf874301cf2
ms.openlocfilehash: 395f1443f4eef16d9eea44c23a6e3288daf03d14
ms.sourcegitcommit: c4528a7424d35039454f17778baf1b5f98fbbee7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "79545471"
---
# <a name="__identifier-ccli"></a>__identifier (C++/CLI)

Разрешает использование ключевых слов C++ в качестве идентификаторов.

## <a name="all-platforms"></a>Все платформы

### <a name="syntax"></a>Синтаксис

```cpp
__identifier(C++_keyword)
```

### <a name="remarks"></a>Примечания

Разрешено использование ключевого слова **__identifier** для идентификаторов, которые не являются ключевыми словами. Но такой вариант настоятельно не рекомендуется использовать из-за стиля.

## <a name="windows-runtime"></a>Среда выполнения Windows

### <a name="requirements"></a>Требования

Параметр компилятора: `/ZW`

### <a name="examples"></a>Примеры

**Пример**

В приведенном ниже примере класс с именем **template** создается на C# и распространяется как библиотека DLL. В программе на C++/CLI, использующей класс **template**, ключевое слово **__identifier** не указывает, что класс **template** является стандартным ключевым словом C++.

```csharp
// identifier_template.cs
// compile with: /target:library
public class template {
   public void Run() { }
}
```

```cpp
// keyword__identifier.cpp
// compile with: /ZW
#using <identifier_template.dll>
int main() {
   __identifier(template)^ pTemplate = ref new __identifier(template)();
   pTemplate->Run();
}
```

## <a name="common-language-runtime"></a>Среда CLR

### <a name="remarks"></a>Примечания

Ключевое слово **__Identifier** может использоваться с параметром компилятора `/clr`.

### <a name="requirements"></a>Требования

Параметр компилятора: `/clr`

### <a name="examples"></a>Примеры

В приведенном ниже примере класс с именем **template** создается на C# и распространяется как библиотека DLL. В программе на C++/CLI, использующей класс **template**, ключевое слово **__identifier** не указывает, что класс **template** является стандартным ключевым словом C++.

```csharp
// identifier_template.cs
// compile with: /target:library
public class template {
   public void Run() { }
}
```

```cpp
// keyword__identifier.cpp
// compile with: /clr
#using <identifier_template.dll>

int main() {
   __identifier(template) ^pTemplate = gcnew __identifier(template)();
   pTemplate->Run();
}
```

## <a name="see-also"></a>См. также:

[Расширения компонентов для .NET и UWP](component-extensions-for-runtime-platforms.md)<br/>
[Расширения компонентов для .NET и UWP](component-extensions-for-runtime-platforms.md)