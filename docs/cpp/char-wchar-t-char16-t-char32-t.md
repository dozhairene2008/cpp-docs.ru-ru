---
title: char, wchar_t, char16_t, char32_t
ms.date: 02/14/2018
ms.assetid: 6b33e9f5-455b-4e49-8f12-a150cbfe2e5b
ms.openlocfilehash: a518f24973aaddff59b97f104d9d912e4a2bedce
ms.sourcegitcommit: 63784729604aaf526de21f6c6b62813882af930a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/17/2020
ms.locfileid: "79447152"
---
# <a name="char-wchar_t-char16_t-char32_t"></a>char, wchar_t, char16_t, char32_t

Типы **char**, **wchar_t**, **char16_t** и **char32_t** являются встроенными типами, представляющими буквенно-цифровые символы, а также неалфавитные глифы и непечатаемые символы.

## <a name="syntax"></a>Синтаксис

```cpp
char     ch1{ 'a' };  // or { u8'a' }
wchar_t  ch2{ L'a' };
char16_t ch3{ u'a' };
char32_t ch4{ U'a' };
```

## <a name="remarks"></a>Remarks

Тип **char** был исходным типом символа в C и C++. Тип **char без знака** часто используется для представления *байта*, который не является встроенным типом в C++. Тип **char** можно использовать для хранения символов из кодировки ASCII или любой из кодировок ISO-8859, а также для отдельных байтов многобайтовых символов, таких как Shift-JIS или UTF-8 в кодировке Юникода. Строки типа **char** называются *узкими* строками даже при использовании для кодирования многобайтовых символов. В компиляторе Microsoft **char** является 8-разрядным типом.

Тип **wchar_t** является определяемым реализацией типом расширенных символов. В компиляторе Майкрософт он представляет 16-разрядный символ, используемый для хранения Юникода в кодировке UTF-16LE, собственный тип символов в операционных системах Windows. Версии расширенных символов функций библиотеки универсальной среды выполнения C (UCRT) используют **wchar_t** , а также его указатели и типы массивов в качестве параметров и возвращаемых значений, как и версии расширенных символов собственного API Windows.

Типы **char16_t** и **char32_t** представляют 16-разрядные и 32-разрядные символы соответственно. Юникод в кодировке UTF-16 может храниться в **char16_t** типе, а Юникод в кодировке utf-32 может храниться в **char32_t** типе. Строки этих типов и **wchar_t** называются *расширенными* строками, хотя термин часто относится к строкам **wchar_t** типа.

В C++ стандартной библиотеке тип `basic_string` является специализированным для узких и широких строк. Используйте `std::string`, если символы имеют тип **char**, `std::u16string`, если символы имеют тип **char16_t**, `std::u32string`, если символы имеют тип **char32_t**, и `std::wstring`, если символы имеют тип **wchar_t**. Другие типы, представляющие текст, в том числе `std::stringstream` и `std::cout`, имеют специализации для узких и широких строк.