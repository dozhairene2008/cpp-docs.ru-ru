---
title: Неустранимая ошибка C1099
ms.date: 11/04/2016
f1_keywords:
- C1099
helpviewer_keywords:
- C1099
ms.assetid: c050b074-a06a-4026-9e10-569029cc0739
ms.openlocfilehash: 673a54f705a8ff46ad94167a4458ab538df69c88
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62387010"
---
# <a name="fatal-error-c1099"></a>Неустранимая ошибка C1099

Механизм "Изменить и продолжить" прервал компиляцию

Компонент "Изменить и продолжить" загрузил предварительно скомпилированный файл заголовка при подготовке к компиляции изменений кода, но последующие действия (например, изменения кода до оператора предварительно скомпилированного заголовка `#include` или остановка отладчика) помешали компоненту "Изменить и продолжить" завершить компиляцию в этом процессе. Не нужно предпринимать никаких действий, чтобы устранить эту ошибку.