---
title: Создание пулов ресурсов в приложениях OLE DB
ms.date: 10/29/2018
helpviewer_keywords:
- OLE DB services [OLE DB], resource pooling
- resource pooling [OLE DB], services
- OLE DB, resource pooling
- OLE DB providers, resource pooling
ms.assetid: 2ead1bcf-bbd4-43ea-a307-bb694b992fc1
ms.openlocfilehash: 786c2b31bb93b0691d80885c86377e2afba8c1dc
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62243969"
---
# <a name="resource-pooling-in-your-ole-db-application"></a>Создание пулов ресурсов в приложениях OLE DB

Пулов в приложении, необходимо убедиться в том службы OLE DB вызываются путем получения источника данных `IDataInitialize` или `IDBPromptInitialize`. При непосредственном использовании `CoCreateInstance` для вызова поставщика на основе его CLSID, вызываются службы OLE DB.

Службы OLE DB Ведение кластеров из подключенных источников данных при условии, ссылку на `IDataInitialize` или `IDBPromptInitialize` публичной или условии, что имеется соединение используется. Пулы также будут автоматически обновлены в среде служб COM + 1.0 и Internet Information Services (IIS). Если приложение использует преимущества пул внешних в среде служб COM + 1.0 или IIS, следует хранить ссылку на `IDataInitialize` или `IDBPromptInitialize` или поддерживать по крайней мере одно подключение. Чтобы убедиться в том, что пул не удалялся при выпуске последнего соединения для приложения, сохранять ссылку на или хранения соединению в течение жизненного цикла приложения.

Службы OLE DB определите пул, из которого берется подключение, во время, `Initialize` вызывается. После подключения из пула, ее нельзя переместить в другой пул. Таким образом, не следует изменять в приложении, которые изменяют сведения об инициализации, например, вызов `UnInitialize` или вызова `QueryInterface` для интерфейса поставщика перед вызовом `Initialize`. Кроме того не пул подключений к prompt значение, отличное от DBPROMPT_NOPROMPT. Тем не менее Строка инициализации, извлеченная из соединения, установленного через запрос можно использовать для установки дополнительных пула подключений к тому же источнику данных.

Некоторым поставщикам необходимо создавать отдельное подключение для каждого сеанса. Эти дополнительные подключения необходимо отдельно прикрепляется к распределенной транзакции, если он существует. OLE DB для служб кэши и повторно использует один сеанс на каждый источник данных, но если приложение запрашивает несколько сеансов за раз из одного источника данных, поставщик может оказаться, что создание дополнительных подключений и выполнении зачисления дополнительных транзакций, не в составе пула. Это более эффективный способ — создать отдельный источник данных для каждого сеанса в среде в составе пула, чем создание нескольких сеансов из одного источника данных.

Наконец поскольку ADO автоматически использует OLE DB для служб, можно использовать ADO для установки соединений и пулы и зачисление происходит автоматически.

## <a name="see-also"></a>См. также

[Создание пулов ресурсов и служб OLE DB](../../data/oledb/ole-db-resource-pooling-and-services.md)