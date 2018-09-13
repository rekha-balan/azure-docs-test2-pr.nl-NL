---
title: Transparent Data Encryption in SQL Data Warehouse (Portal)| Microsoft Docs
description: Transparent Data Encryption (TDE) in SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: ''
author: ronortloff
manager: jhubbard
editor: ''
ms.assetid: fabf75d3-9bbf-4e0d-9b31-8b5a8713f08d
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: a4b4a14e09ba815ab612a6a3cb86e0390262e3ad
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549205"
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a>Get started with Transparent Data Encryption (TDE) in SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Security Overview](sql-data-warehouse-overview-manage-security.md)
> * [Authentication](sql-data-warehouse-authentication.md)
> * [Encryption (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Encryption (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a>Required Permssions
To enable Transparent Data Encryption (TDE), you must be an administrator or a member of the dbmanager role.

## <a name="enabling-encryption"></a>Enabling Encryption
To enable TDE for a SQL Data Warehouse, follow the steps below:

1. Open the database in the [Azure portal](https://portal.azure.com)
2. In the database blade, click the **Settings** button
3. Select the **Transparent data encryption** option ![][1]
4. Select the **On** setting ![][2]
5. Select **Save**
   ![][3]  

## <a name="disabling-encryption"></a>Disabling Encryption
To disable TDE for a SQL Data Warehouse, follow the steps below:

1. Open the database in the [Azure portal](https://portal.azure.com)
2. In the database blade, click the **Settings** button
3. Select the **Transparent data encryption** option ![][1]
4. Select the **Off** setting ![][4]
5. Select **Save**
   ![][5]  

## <a name="encryption-dmvs"></a>Encryption DMVs
Encryption can be confirmed with the following DMVs:

* [sys.databases]
* [sys.dm_pdw_nodes_database_encryption_keys]

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->





