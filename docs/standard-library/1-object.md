---
title: Объект _1
ms.date: 11/04/2016
f1_keywords:
- _1
- std::_1
- functional/std::_1
helpviewer_keywords:
- _1 object
ms.assetid: 30c3c480-ff31-4708-94be-7d0d65f243c9
ms.openlocfilehash: 1c1f13d40e02ec6e099ef1e2c20fe1cac4a4ef93
ms.sourcegitcommit: 3590dc146525807500c0477d6c9c17a4a8a2d658
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/16/2019
ms.locfileid: "68246540"
---
# <a name="1-object"></a>Объект _1

Заполнители для подстановочных аргументов.

## <a name="syntax"></a>Синтаксис

```cpp
namespace placeholders {
    extern unspecified _1, _2, ... _M
} // namespace placeholders (within std)
```

## <a name="remarks"></a>Примечания

Объекты `_1, _2, ... _M` — это местозаполнители первой, второй,..., m-й аргумент соответственно в вызове функции в объект, возвращаемый [привязать](../standard-library/functional-functions.md#bind). Можно использовать `_N` для указания, куда необходимо вставить N-й аргумент при вычислении выражения привязки.

В этой реализации значение `M` — 20.

## <a name="example"></a>Пример

```cpp
// std__functional_placeholder.cpp
// compile with: /EHsc
#include <functional>
#include <algorithm>
#include <iostream>

using namespace std::placeholders;

void square(double x)
    {
    std::cout << x << "^2 == " << x * x << std::endl;
    }

void product(double x, double y)
    {
    std::cout << x << "*" << y << " == " << x * y << std::endl;
    }

int main()
    {
    double arg[] = {1, 2, 3};

    std::for_each(&arg[0], &arg[3], square);
    std::cout << std::endl;

    std::for_each(&arg[0], &arg[3], std::bind(product, _1, 2));
    std::cout << std::endl;

    std::for_each(&arg[0], &arg[3], std::bind(square, _1));

    return (0);
    }
```

```Output
1^2 == 1
2^2 == 4
3^2 == 9

1*2 == 2
2*2 == 4
3*2 == 6

1^2 == 1
2^2 == 4
3^2 == 9
```
