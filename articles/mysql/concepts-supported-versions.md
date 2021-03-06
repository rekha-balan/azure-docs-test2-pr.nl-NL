---
title: Supported versions in Azure Database for MySQL
description: Describes the supported versions in Azure Database for MySQL.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.topic: article
ms.date: 05/23/2018
ms.openlocfilehash: c9a533ed9b9eb9ac53a02439b98a78954c7aaa11
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864757"
---
# <a name="supported-azure-database-for-mysql-server-versions"></a>Supported Azure Database for MySQL server versions
Azure Database for MySQL has been developed from [MySQL Community Edition](https://www.mysql.com/products/community/), using the InnoDB engine.  Azure Database for MySQL currently supports the following versions:

## <a name="mysql-version-5639"></a>MySQL Version 5.6.39
Refer to the MySQL [documentation](https://dev.mysql.com/doc/relnotes/mysql/5.6/en/news-5-6-39.html) to learn more about improvements and fixes in MySQL 5.6.39.

## <a name="mysql-version-5721"></a>MySQL Version 5.7.21
Refer to the MySQL [documentation](https://dev.mysql.com/doc/relnotes/mysql/5.7/en/news-5-7-21.html) to learn about improvements and fixes in MySQL 5.7.21.

> [!NOTE]
> In the service, a gateway is used to redirect the connections to server instances. After the connection is established, the MySQL client displays the version of MySQL set in the gateway, not the actual version running on your MySQL server instance. To determine the version of your MySQL server instance, use the `SELECT VERSION();` command at the MySQL prompt. 

## <a name="managing-updates-and-upgrades"></a>Managing updates and upgrades
The service automatically manages patching for minor version updates. Major version upgrades are not supported (ex. upgrading from MySQL 5.6 to MySQL 5.7).

## <a name="next-steps"></a>Next steps

For information about specific resource quotas and limitations based on your **service tier**, see [Service tiers](./concepts-pricing-tiers.md)
