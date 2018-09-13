---
title: Resources for developing a data warehouse in Azure | Microsoft Docs
description: Development concepts, design decisions, recommendations and coding techniques for SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: barbkess
editor: ''
ms.assetid: 996e3afc-c21c-4e21-b9df-997f953f6dfd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: develop
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: b85a4f09e561e429aa5bf46ec680014487fb40c7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563714"
---
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a>Design decisions and coding techniques for SQL Data Warehouse
Take a look through these development articles to better understand key design decisions, recommendations and coding techniques for SQL Data Warehouse.

## <a name="key-design-decisions"></a>Key design decisions
The following articles highlight some of the key concepts and design decisions you will need to understand for the development of your distributed data warehouse using SQL Data Warehouse:

* [connections][connections]
* [concurrency][concurrency]
* [transactions][transactions]
* [user-defined schemas][user-defined schemas]
* [table distribution][table distribution]
* [table indexes][table indexes]
* [table partitions][table partitions]
* [CTAS][CTAS]
* [statistics][statistics]

## <a name="development-recommendations-and-coding-techniques"></a>Development recommendations and coding techniques
These articles highlight specific coding techniques, tips and recommendations for developing your SQL Data Warehouse:

* [stored procedures][stored procedures]
* [labels][labels]
* [views][views]
* [temporary tables][temporary tables]
* [dynamic SQL][dynamic SQL]
* [looping][looping]
* [group by options][group by options]
* [variable assignment][variable assignment]

## <a name="next-steps"></a>Next steps
Once you have been through the development articles take a look through the [Transact-SQL reference][Transact-SQL reference] page for more details on the supported syntax for SQL Data Warehouse.

<!--Image references-->

<!--Article references-->
[concurrency]: ./sql-data-warehouse-develop-concurrency.md
[connections]: ./sql-data-warehouse-connect-overview.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[dynamic SQL]: ./sql-data-warehouse-develop-dynamic-sql.md
[group by options]: ./sql-data-warehouse-develop-group-by-options.md
[labels]: ./sql-data-warehouse-develop-label.md
[looping]: ./sql-data-warehouse-develop-loops.md
[statistics]: ./sql-data-warehouse-tables-statistics.md
[stored procedures]: ./sql-data-warehouse-develop-stored-procedures.md
[table distribution]: ./sql-data-warehouse-tables-distribute.md
[table indexes]: ./sql-data-warehouse-tables-index.md
[table partitions]: ./sql-data-warehouse-tables-partition.md
[temporary tables]: ./sql-data-warehouse-tables-temporary.md
[transactions]: ./sql-data-warehouse-develop-transactions.md
[user-defined schemas]: ./sql-data-warehouse-develop-user-defined-schemas.md
[variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[views]: ./sql-data-warehouse-develop-views.md
[Transact-SQL reference]: ./sql-data-warehouse-overview-reference.md

<!--MSDN references-->
[renaming objects]: https://msdn.microsoft.com/library/mt631611.aspx

<!--Other Web references-->
