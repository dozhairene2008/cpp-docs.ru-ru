---
title: Переопределение используемых по умолчанию параметров службы поставщика
ms.date: 10/29/2018
helpviewer_keywords:
- service providers [OLE DB]
- OLE DB services [OLE DB], overriding defaults
ms.assetid: 08e366c0-74d8-463b-93a6-d58a8dc195f8
ms.openlocfilehash: 08011f65ca220885e124e5ad6072244e4ad6e80d
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62282953"
---
# <a name="overriding-provider-service-defaults"></a>Переопределение используемых по умолчанию параметров службы поставщика

Значение реестра поставщика для OLEDB_SERVICES возвращается как значение по умолчанию для [DBPROP_INIT_OLEDBSERVICES, установить](/previous-versions/windows/desktop/ms716898(v=vs.85)) свойство инициализации на объекте источника данных.

Пока существует запись реестра, группируются объекты поставщика. Пользователь может переопределить поставщика по умолчанию для включенных служб, задав свойство DBPROP_INIT_OLEDBSERVICES, установить до инициализации. Для включения или отключения определенной службы, пользователь получает текущее значение свойства DBPROP_INIT_OLEDBSERVICES, установить, задает или сбрасывает бит для конкретного свойства включить или отключить и свойство. Можно задать DBPROP_INIT_OLEDBSERVICES, установить непосредственно в OLE DB или в строке подключения, переданной в ADO или `IDataInitialize::GetDatasource`. В следующей таблице перечислены соответствующие значения для включения или отключения отдельных служб.

|Службы по умолчанию включен|Значение свойства DBPROP_INIT_OLEDBSERVICES, установить|Значение в строке подключения|
|------------------------------|------------------------------------------------|--------------------------------|
|Все службы (по умолчанию)|DBPROPVAL_OS_ENABLEALL|«Службы OLE DB = -1;»|
|Все, за исключением и автоматического зачисления|`DBPROPVAL_OS_ENABLEALL &`<br /><br /> `~DBPROPVAL_OS_RESOURCEPOOLING &`<br /><br /> `~DBPROPVAL_OS_TXNENLISTMENT`|«Службы OLE DB = -4;»|
|Все, кроме клиентский курсор|`DBPROPVAL_OS_ENABLEALL &`<br /><br /> `~DBPROPVAL_OS_CLIENTCURSOR`|«Службы OLE DB = -5;»|
|Все, кроме пулов, автоматического зачисления и клиентских курсоров|`DBPROPVAL_OS_ENABLEALL &`<br /><br /> `~DBPROPVAL_OS_TXNENLISTMENT &`<br /><br /> `~DBPROPVAL_OS_CLIENTCURSOR`|«Службы OLE DB = -7;»|
|Нет служб|`~DBPROPVAL_OS_ENABLEALL`|«Службы OLE DB = 0;»|

Если запись реестра не существует для поставщика, диспетчеры компонентов не собираем объекты поставщика. Службы не будет включена, даже если это явно запрошено пользователем.

## <a name="see-also"></a>См. также

[Создание пулов ресурсов](/previous-versions/windows/desktop/ms713655(v=vs.85))<br/>
[Как потребители используют Создание пулов ресурсов](/previous-versions/windows/desktop/ms715907(v=vs.85))<br/>
[Как поставщики эффективно работают с пулами ресурсов](/previous-versions/windows/desktop/ms714906(v=vs.85))<br/>
[Включение и отключение служб OLE DB](../../data/oledb/enabling-and-disabling-ole-db-services.md)<br/>