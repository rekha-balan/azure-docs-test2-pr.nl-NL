---
title: Copy data from Blob Storage to SQL Database - Azure | Microsoft Docs
description: This tutorial shows you how to use Copy Activity in an Azure Data Factory pipeline to copy data from Blob storage to SQL database.
keywords: blob sql, blob storage, data copy
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e4035060-93bf-4e8d-bf35-35e2d15c51e0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: spelluru
ms.openlocfilehash: b19534888e82d6f405b4b9d5fce98684af7de1ef
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555750"
---
# <a name="tutorial-copy-data-from-blob-storage-to-sql-database-using-data-factory"></a>Tutorial: Copy data from Blob Storage to SQL Database using Data Factory
> [!div class="op_single_selector"]
> * [Overview and prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Copy Wizard](data-factory-copy-data-wizard-tutorial.md)
> * [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)

In this tutorial, you create a data factory with a pipeline to copy data from Blob storage to SQL database.

The Copy Activity performs the data movement in Azure Data Factory. It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way. See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.  

> [!NOTE]
> For a detailed overview of the Data Factory service, see the [Introduction to Azure Data Factory](data-factory-introduction.md) article.
>
>

## <a name="prerequisites-for-the-tutorial"></a>Prerequisites for the tutorial
Before you begin this tutorial, you must have the following prerequisites:

* **Azure subscription**.  If you don't have a subscription, you can create a free trial account in just a couple of minutes. See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.
* **Azure Storage Account**. You use the blob storage as a **source** data store in this tutorial. if you don't have an Azure storage account, see the [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.
* **Azure SQL Database**. You use an Azure SQL database as a **destination** data store in this tutorial. If you don't have an Azure SQL database that you can use in the tutorial, See [How to create and configure an Azure SQL Database](../sql-database/sql-database-get-started.md) to create one.
* **SQL Server 2012/2014 or Visual Studio 2013**. You use SQL Server Management Studio or Visual Studio to create a sample database and to view the result data in the database.  

## <a name="collect-blob-storage-account-name-and-key"></a>Collect blob storage account name and key
You need the account name and account key of your Azure storage account to do this tutorial. Note down **account name** and **account key** for your Azure storage account.

1. Log in to the [Azure portal](https://portal.azure.com/).
2. Click **More services** on the left menu and select **Storage Accounts**.

    ![Browse - Storage accounts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. In the **Storage Accounts** blade, select the **Azure storage account** that you want to use in this tutorial.
4. Select **Access keys** link under **SETTINGS**.
5. Click **copy** (image) button next to **Storage account name** text box and save/paste it somewhere (for example: in a text file).
6. Repeat the previous step to copy or note down the **key1**.

    ![Storage access key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. Close all the blades by clicking **X**.

## <a name="collect-sql-server-database-user-names"></a>Collect SQL server, database, user names
You need the names of Azure SQL server, database, and user to do this tutorial. Note down names of **server**, **database**, and **user** for your Azure SQL database.

1. In the **Azure portal**, click **More services** on the left and select **SQL databases**.
2. In the **SQL databases blade**, select the **database** that you want to use in this tutorial. Note down the **database name**.  
3. In the **SQL database** blade, click **Properties** under **SETTINGS**.
4. Note down the values for **SERVER NAME** and **SERVER ADMIN LOGIN**.
5. Close all the blades by clicking **X**.

## <a name="allow-azure-services-to-access-sql-server"></a>Allow Azure services to access SQL server
Ensure that **Allow access to Azure services** setting turned **ON** for your Azure SQL server so that the Data Factory service can access your Azure SQL server. To verify and turn on this setting, do the following steps:

1. Click **More services** hub on the left and click **SQL servers**.
2. Select your server, and click **Firewall** under **SETTINGS**.
3. In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.
4. Close all the blades by clicking **X**.

## <a name="prepare-blob-storage-and-sql-database"></a>Prepare Blob Storage and SQL Database
Now, prepare your Azure blob storage and Azure SQL database for the tutorial by performing the following steps:  

1. Launch Notepad. Copy the following text and save it as **emp.txt** to **C:\ADFGetStarted** folder on your hard drive.

    ```
    John, Doe
    Jane, Doe
    ```
2. Use tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/) to create the **adftutorial** container and to upload the **emp.txt** file to the container.

    ![Azure Storage Explorer. Copy data from Blob storage to SQL database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. Use the following SQL script to create the **emp** table in your Azure SQL Database.  

    ```SQL
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

    **If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) to connect to your Azure SQL server and run the SQL script. This article uses the [classic Azure portal](http://manage.windowsazure.com), not the [new Azure portal](https://portal.azure.com), to configure firewall for an Azure SQL server.

    If your client is not allowed to access the Azure SQL server, you need to configure firewall for your Azure SQL server to allow access from your machine (IP Address). See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps to configure the firewall for your Azure SQL server.

You have completed the prerequisites. You can create a data factory using one of the following ways. Click one of the options in the drop-down list at the top or the following links to perform the tutorial.     

* [Copy Wizard](data-factory-copy-data-wizard-tutorial.md)
* [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
* [Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
* [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> The data pipeline in this tutorial copies data from a source data store to a destination data store. It does not transform input data to produce output data. For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).
> 
> You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity. See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information. 

