---
title: Ошибка компилятора C2170
ms.date: 11/04/2016
f1_keywords:
- C2170
helpviewer_keywords:
- C2170
ms.assetid: d5c663f0-2459-4e11-a8bf-a52b62f3c71d
ms.openlocfilehash: 04d41a50bc0d5e811e47e5f9d146362a543f26f9
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62174683"
---
# <a name="compiler-error-c2170"></a>Ошибка компилятора C2170

«Идентификатор»: не объявлена как функция, не может быть встроенной

### <a name="to-fix-by-checking-the-following-possible-causes"></a>Чтобы устранить ошибку, проверьте указанные ниже возможные причины ее возникновения.

1. Директива pragma `intrinsic` используется для элемента, не функции.

1. Директива pragma `intrinsic` используется для функции, не имеющей форму.