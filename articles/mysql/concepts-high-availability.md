---
title: High availability concepts in Azure Database for MySQL
description: This topic provides information of high availability when using Azure Database for MySQL
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.topic: article
ms.date: 02/28/2018
ms.openlocfilehash: 90dc603c0ee520774bd22531c7136e0949f6cf90
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867703"
---
# <a name="high-availability-concepts-in-azure-database-for-mysql"></a>High availability concepts in Azure Database for MySQL
The Azure Database for MySQL service provides a guaranteed high level of availability. The financially backed service level agreement (SLA) is 99.99% upon general availability. There is virtually no application down time when using this service.

## <a name="high-availability"></a>High availability
The high availability (HA) model is based on built-in fail-over mechanisms when a node-level interruption occurs. A node-level interruption could occur because of a hardware failure or in response to a service deployment.

At all times, changes made to an Azure Database for MySQL database server occur in the context of a transaction. Changes are recorded synchronously in Azure storage when the transaction is committed. If a node-level interruption occurs, the database server automatically creates a new node and attaches data storage to the new node. Any active connections are dropped and any inflight transactions are not committed.

## <a name="application-retry-logic-is-essential"></a>Application retry logic is essential
It is important that MySQL database applications are built to detect and retry dropped connections and failed transactions. When the application retries, the application's connection is transparently redirected to the newly created instance, which takes over for the failed instance.

Internally in Azure, a gateway is used to redirect the connections to the new instance. Upon an interruption, the entire fail-over process typically takes tens of seconds. Since the redirect is handled internally by the gateway, the external connection string remains the same for the client applications.

## <a name="scaling-up-or-down"></a>Scaling up or down
Similar to the HA model, when an Azure Database for MySQL is scaled up or down, a new server instance with the specified size is created. The existing data storage is detached from the original instance, and attached to the new instance.

During the scale operation, an interruption to the database connections occurs. The client applications are disconnected, and open uncommitted transactions are canceled. Once the client application retries the connection, or makes a new connection, the gateway directs the connection to the newly sized instance. 

## <a name="next-steps"></a>Next steps
- For an overview of the service, see [Azure Database for MySQL Overview](overview.md)
