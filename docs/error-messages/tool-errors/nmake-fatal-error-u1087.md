---
title: Неустранимая ошибка NMAKE U1087
ms.date: 11/04/2016
f1_keywords:
- U1087
helpviewer_keywords:
- U1087
ms.assetid: 5236ab54-e117-484d-99c3-852b061fd3d0
ms.openlocfilehash: 47015443114404de2e5f9edfdb1100c324d5e18b
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62298455"
---
# <a name="nmake-fatal-error-u1087"></a>Неустранимая ошибка NMAKE U1087

не может иметь: и:: зависимых элементов для одного целевого объекта

Целевой объект не может указываться в обоих с одинарным двоеточием (**:**) и двойным двоеточием (`::`) зависимостей.

Чтобы указать целевой объект в нескольких блоках описания, используйте `::` в каждой строке зависимость.