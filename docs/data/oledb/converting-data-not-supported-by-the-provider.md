---
title: Преобразование данных, не поддерживаемых поставщиком
ms.date: 10/29/2018
helpviewer_keywords:
- OLE DB provider templates, unsupported data types
ms.assetid: f495e50f-530a-4fab-ab54-e0c359785845
ms.openlocfilehash: e60f6cd4f7dca1ed3e176cabefc42f69946436a4
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62409074"
---
# <a name="converting-data-not-supported-by-the-provider"></a>Преобразование данных, не поддерживаемых поставщиком

Если потребитель запрашивает тип данных, который не поддерживается поставщиком, код шаблона поставщика OLE DB `IRowsetImpl::GetData` вызывает Msdadc.dll для преобразования типа данных.

Если реализовать интерфейс наподобие `IRowsetChange` , нуждающейся в преобразовании данных, вы можете вызвать Msdaenum.dll для выполнения преобразования. Используйте `GetData`, определенный в Atldb. h, в качестве примера.

## <a name="see-also"></a>См. также

[Работа с шаблонами поставщика OLE DB](../../data/oledb/working-with-ole-db-provider-templates.md)