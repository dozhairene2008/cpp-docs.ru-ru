---
title: /Zc:trigraphs (подстановка триграфов)
ms.date: 03/06/2018
f1_keywords:
- /Zc:trigraphs
helpviewer_keywords:
- -Zc compiler options (C++)
- /Zc compiler options (C++)
- Conformance compiler options
- Zc compiler options (C++)
ms.assetid: e3d6058f-400d-4966-a3aa-800cfdf69cbf
ms.openlocfilehash: 0e4c98e09551d39e3ff7978767b21f1d2c5bb318
ms.sourcegitcommit: 63784729604aaf526de21f6c6b62813882af930a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/17/2020
ms.locfileid: "79438650"
---
# <a name="zctrigraphs-trigraphs-substitution"></a>/Zc:trigraphs (подстановка триграфов)

Если указан параметр **/Zc: триграфов** , компилятор заменяет последовательность символов триграф с помощью соответствующего знака пунктуации.

## <a name="syntax"></a>Синтаксис

> **/Zc: триграфов**[ **-** ]

## <a name="remarks"></a>Remarks

*Триграф* состоит из двух последовательных вопросительных знаков ("??"), за которыми следует уникальный третий символ. Стандарт языка C поддерживает триграфов для исходных файлов, использующих набор символов, который не содержит удобные графические представления для некоторых символов пунктуации. Например, если включены триграфов, компилятор заменяет "?? = "триграф с помощью символа" # ". С помощью C++ 14 триграфов поддерживаются как в C. Стандарт C++ 17 удаляет триграфов из C++ языка. В C++ коде параметр компилятора **/Zc: триграфов** обеспечивает замену последовательностей триграф соответствующими символами пунктуации. **/Zc: триграфов —** отключает подстановку триграф.

Параметр **/Zc: триграфов** по умолчанию отключен, и этот параметр не затрагивается, если указан параметр [/permissive-](permissive-standards-conformance.md) .

Список C/C++ триграфов и пример, демонстрирующий использование триграфов, см. в разделе [триграфов](../../c-language/trigraphs.md).

## <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Установка данного параметра компилятора в среде разработки Visual Studio

1. Откройте диалоговое окно **Страницы свойств** проекта. Подробнее см. в статье [Настройка компилятора C++ и свойства сборки в Visual Studio](../working-with-project-properties.md).

1. Перейдите на страницу свойств **Свойства конфигурации** > **C/C++**  > **Командная строка**.

1. Измените свойство **Дополнительные параметры** , чтобы включить **/Zc: триграфов** или **/Zc: триграфов-** и нажмите кнопку **ОК**.

## <a name="see-also"></a>См. также раздел

[/Zc (соответствие)](zc-conformance.md)<br/>
[Триграфы](../../c-language/trigraphs.md)<br/>
