---
title: Неустранимая ошибка C1905
ms.date: 11/04/2016
f1_keywords:
- C1905
helpviewer_keywords:
- C1905
ms.assetid: fefc6769-477f-45a2-9878-6f0a5f42472c
ms.openlocfilehash: 3fb4db30d91e0dd8c9dbeeebca46210122e5ff07
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62166819"
---
# <a name="fatal-error-c1905"></a>Неустранимая ошибка C1905

Внешний и внутренний сегменты несовместимы (должны быть предназначены для одного и того же процессора)

Эта ошибка возникает, когда OBJ-файл создается внешний интерфейс компилятора (C1.dll) один процессор, целевые объекты, такие как x86, ARM или x64, но считывается внутренним сегментом (C2.dll), предназначена для другого процессора.

Чтобы устранить эту проблему убедитесь, что вы используете совпадающие внутренний и внешний сегменты. Такая конфигурация используется по умолчанию для проектов, создаваемых в Visual Studio. Эта ошибка может возникнуть, если вы отредактировали файл проекта и использовали другие пути к средствам компилятора. Если вы не задали явным образом путь к средствам компилятора, то эта ошибка может возникнуть при повреждении установки Visual Studio. Например, вы могли скопировать DLL-файлы компилятора из одного места в другое. Используйте **программы и компоненты** на панели управления Windows для восстановления или переустановки Visual Studio.