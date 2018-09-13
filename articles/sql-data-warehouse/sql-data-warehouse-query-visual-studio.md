---
title: Connect to Azure SQL Data Warehouse - VSTS | Microsoft Docs
description: Query SQL Data Warehouse with Visual Studio.
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: ''
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: barbkess
ms.openlocfilehash: 830a6c70e8e30af100f710d458bc51054250ab60
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552150"
---
# <a name="connect-to-sql-data-warehouse-with-visual-studio-and-ssdt"></a>Connect to SQL Data Warehouse with Visual Studio and SSDT
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Use Visual Studio to query Azure SQL Data Warehouse in just a few minutes. This method uses the SQL Server Data Tools (SSDT) extension in Visual Studio. 

## <a name="prerequisites"></a>Prerequisites
To use this tutorial, you need:

* An existing SQL data warehouse. To create one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].
* SSDT for Visual Studio. If you have Visual Studio, you probably already have this. For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].
* The fully qualified SQL server name. To find this, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].

## <a name="1-connect-to-your-sql-data-warehouse"></a>1. Connect to your SQL Data Warehouse
1. Open Visual Studio 2013 or 2015.
2. Open SQL Server Object Explorer. To do this, select **View** > **SQL Server Object Explorer**.
   
    ![SQL Server Object Explorer][1]
3. Click the **Add SQL Server** icon.
   
    ![Add SQL Server][2]
4. Fill in the fields in the Connect to Server window.
   
    ![Connect to Server][3]
   
   * **Server name**. Enter the **server name** previously identified.
   * **Authentication**. Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.
   * **User Name** and **Password**. Enter user name and password if SQL Server Authentication was selected above.
   * Click **Connect**.
5. To explore, expand your Azure SQL server. You can view the databases associated with the server. Expand AdventureWorksDW to see the tables in your sample database.
   
    ![Explore AdventureWorksDW][4]

## <a name="2-run-a-sample-query"></a>2. Run a sample query
Now that a connection has been established to your database, let's write a query.

1. Right-click your database in SQL Server Object Explorer.
2. Select **New Query**. A new query window opens.
   
    ![New query][5]
3. Copy this TSQL query into the query window:
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Run the query. To do this, click the green arrow or use the following shortcut: `CTRL`+`SHIFT`+`E`.
   
    ![Run query][6]
5. Look at the query results. In this example, the FactInternetSales table has 60398 rows.
   
    ![Query results][7]

## <a name="next-steps"></a>Next steps
Now that you can connect and query, try [visualizing the data with PowerBI][visualizing the data with PowerBI].

To configure your environment for Azure Active Directory authentication, see [Authenticate to SQL Data Warehouse][Authenticate to SQL Data Warehouse].

<!--Arcticles-->
[Connect to SQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate to SQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing the data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-query-visual-studio/query-results.png







