---
title: Ошибка вычислителя выражений CXX0015
ms.date: 11/04/2016
f1_keywords:
- CXX0015
helpviewer_keywords:
- CXX0015
- CAN0015
ms.assetid: 35efaf77-d578-48d8-bfc5-fdeb2a46a8b5
ms.openlocfilehash: f73aef18563426d28a81b92b3c37d1b7e345d0d3
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62397150"
---
# <a name="expression-evaluator-error-cxx0015"></a>Ошибка вычислителя выражений CXX0015

слишком сложное выражение (переполнение стека)

Введенное выражение было слишком сложным или вложенные слишком глубоко объема хранилища для вычислитель выражений C.

Переполнение обычно происходит из-за слишком большого количества незавершенных вычислений.

Перестройте выражение так, чтобы каждый компонент выражения можно вычислить, в котором он находится, а не ждать, пока другие части выражения, которые необходимо вычислить.

Разбейте выражение на несколько команд.

Эта ошибка идентична CAN0015.