---
title: '> &lt;исключений (C++ комментарии к документации)'
ms.date: 11/04/2016
helpviewer_keywords:
- <exception> C++ XML tag
- exception C++ XML tag
ms.assetid: 24451e79-9b89-4b77-98fb-702c6516b818
ms.openlocfilehash: d56e0ce7c892cfd9fd909b5268043d77929bd43c
ms.sourcegitcommit: 63784729604aaf526de21f6c6b62813882af930a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/17/2020
ms.locfileid: "79439860"
---
# <a name="ltexceptiongt"></a>&lt;exception&gt;

Тег \<exception> служит для указания возможных исключений. Этот тег применяется к определению метода.

## <a name="syntax"></a>Синтаксис

```
<exception cref="member">description</exception>
```

#### <a name="parameters"></a>Параметры

*member*<br/>
Ссылка на исключение, которое доступно из текущей среды компиляции. Используя правила подстановки имен, компилятор проверяет, существует ли исключение, и приводит `member` к каноническому имени элемента в выходных XML-данных.  Если компилятору не удается найти `member`, он выдает предупреждение.

Заключите имя в одинарные или двойные кавычки.

Дополнительные сведения о создании ссылки cref на универсальный тип см. в разделе [\<see>](see-visual-cpp.md).

*Описание*<br/>
Описание.

## <a name="remarks"></a>Remarks

Чтобы обработать и сохранить комментарии документации в файл, при компиляции необходимо использовать параметр [/doc](doc-process-documentation-comments-c-cpp.md).

Компилятор КОМПИЛЯТОРОМ MSVC будет пытаться разрешить ссылки cref в одном проходе через комментарии к документации.  Поэтому если при использовании правил поиска C++ компилятор не найдет символ, ссылка будет помечена как не разрешенная. Дополнительные сведения см. в описании [\<seealso>](seealso-visual-cpp.md).

## <a name="example"></a>Пример

```cpp
// xml_exception_tag.cpp
// compile with: /clr /doc /LD
// post-build command: xdcmake xml_exception_tag.dll
using namespace System;

/// Text for class EClass.
public ref class EClass : public Exception {
   // class definition ...
};

/// <exception cref="System.Exception">Thrown when... .</exception>
public ref class TestClass {
   void Test() {
      try {
      }
      catch(EClass^) {
      }
   }
};
```

## <a name="see-also"></a>См. также раздел

[Документация XML](xml-documentation-visual-cpp.md)
