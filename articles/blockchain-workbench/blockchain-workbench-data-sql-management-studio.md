---
title: Use Azure Blockchain Workbench Data with SQL Server Management Studio
description: Learn how to connect to Azure Blockchain Workbench's SQL Database from within SQL Server Management Studio.
services: azure-blockchain
keywords: ''
author: PatAltimore
ms.author: patricka
ms.date: 5/3/2018
ms.topic: article
ms.service: azure-blockchain
ms.reviewer: mmercuri
manager: femila
ms.openlocfilehash: 5c5a2e2b42cd9c19810e6579159b228369ee8f7f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856625"
---
# <a name="using-azure-blockchain-workbench-data-with-sql-server-management-studio"></a>Using Azure Blockchain Workbench data with SQL Server Management Studio

Microsoft SQL Server Management Studio provides the ability to rapidly write and test queries against Azure Blockhain Workbench's SQL DB. This section contains a step by step walkthrough of how to connect to Azure Blockchain Workbench's SQL Database from within SQL Server Management Studio.

## <a name="prerequisites"></a>Prerequisites

* Download [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017).

## <a name="connecting-sql-server-management-studio-to-data-in-azure-blockchain-workbench"></a>Connecting SQL Server Management Studio to data in Azure Blockchain Workbench

1. Open the SQL Server Management Studio and select **Connect**.
2. Select **Database Engine**.

    ![Database engine](media/blockchain-workbench-data-sql-management-studio/database-engine.png)

3. In the **Connect to Server** dialog, enter the server name and your database credentials.

    If you are using the credentials created by the Azure Blockchain Workbench deployment process, the username will be **dbadmin** and the password will be the one you provided during deployment.

    ![Enter SQL credentials](media/blockchain-workbench-data-sql-management-studio/sql-creds.png)

 4. SQL Server Management Studio displays the list of databases, database views, and stored procedures in the Azure Blockchain Workbench database.

    ![Database list](media/blockchain-workbench-data-sql-management-studio/db-list.png)

5. To view the data associated with any of the database views, you can automatically generate a select statement using the following steps.
6. Right click on any of the database views in the Object Explorer.
7. Select **Script View as**.
8. Choose **SELECT to**.
9. Select **New Query Editor Window**.
10. A new query can be created by selecting **New Query**.

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Database views in Azure Blockchain Workbench](blockchain-workbench-database-views.md)