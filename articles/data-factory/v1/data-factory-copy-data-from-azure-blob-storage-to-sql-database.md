---
title: Copy data from Blob Storage to SQL Database - Azure | Microsoft Docs
description: This tutorial shows you how to use Copy Activity in an Azure Data Factory pipeline to copy data from Blob storage to SQL database.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: ''
editor: ''
ms.assetid: e4035060-93bf-4e8d-bf35-35e2d15c51e0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/22/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: a9f76b38139cccedb97c6026f0e0efa14d0dbc8c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864388"
---
# <a name="tutorial-copy-data-from-blob-storage-to-sql-database-using-data-factory"></a><span data-ttu-id="1c88c-103">Tutorial: Copy data from Blob Storage to SQL Database using Data Factory</span><span class="sxs-lookup"><span data-stu-id="1c88c-103">Tutorial: Copy data from Blob Storage to SQL Database using Data Factory</span></span>
> [!div class="op_single_selector"]
> * [Overview and prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Copy Wizard](data-factory-copy-data-wizard-tutorial.md)
> * [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [copy activity tutorial](../quickstart-create-data-factory-dot-net.md). 

<span data-ttu-id="1c88c-114">In this tutorial, you create a data factory with a pipeline to copy data from Blob storage to SQL database.</span><span class="sxs-lookup"><span data-stu-id="1c88c-114">In this tutorial, you create a data factory with a pipeline to copy data from Blob storage to SQL database.</span></span>

<span data-ttu-id="1c88c-115">The Copy Activity performs the data movement in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1c88c-115">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="1c88c-116">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span><span class="sxs-lookup"><span data-stu-id="1c88c-116">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="1c88c-117">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="1c88c-117">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>  

> [!NOTE]
> For a detailed overview of the Data Factory service, see the [Introduction to Azure Data Factory](data-factory-introduction.md) article.
>
>

## <a name="prerequisites-for-the-tutorial"></a><span data-ttu-id="1c88c-119">Prerequisites for the tutorial</span><span class="sxs-lookup"><span data-stu-id="1c88c-119">Prerequisites for the tutorial</span></span>
<span data-ttu-id="1c88c-120">Before you begin this tutorial, you must have the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="1c88c-120">Before you begin this tutorial, you must have the following prerequisites:</span></span>

* <span data-ttu-id="1c88c-121">**Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-121">**Azure subscription**.</span></span>  <span data-ttu-id="1c88c-122">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="1c88c-122">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1c88c-123">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span><span class="sxs-lookup"><span data-stu-id="1c88c-123">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="1c88c-124">**Azure Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-124">**Azure Storage Account**.</span></span> <span data-ttu-id="1c88c-125">You use the blob storage as a **source** data store in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="1c88c-125">You use the blob storage as a **source** data store in this tutorial.</span></span> <span data-ttu-id="1c88c-126">if you don't have an Azure storage account, see the [Create a storage account](../../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="1c88c-126">if you don't have an Azure storage account, see the [Create a storage account](../../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span></span>
* <span data-ttu-id="1c88c-127">**Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-127">**Azure SQL Database**.</span></span> <span data-ttu-id="1c88c-128">You use an Azure SQL database as a **destination** data store in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="1c88c-128">You use an Azure SQL database as a **destination** data store in this tutorial.</span></span> <span data-ttu-id="1c88c-129">If you don't have an Azure SQL database that you can use in the tutorial, See [How to create and configure an Azure SQL Database](../../sql-database/sql-database-get-started.md) to create one.</span><span class="sxs-lookup"><span data-stu-id="1c88c-129">If you don't have an Azure SQL database that you can use in the tutorial, See [How to create and configure an Azure SQL Database](../../sql-database/sql-database-get-started.md) to create one.</span></span>
* <span data-ttu-id="1c88c-130">**SQL Server 2012/2014 or Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-130">**SQL Server 2012/2014 or Visual Studio 2013**.</span></span> <span data-ttu-id="1c88c-131">You use SQL Server Management Studio or Visual Studio to create a sample database and to view the result data in the database.</span><span class="sxs-lookup"><span data-stu-id="1c88c-131">You use SQL Server Management Studio or Visual Studio to create a sample database and to view the result data in the database.</span></span>  

## <a name="collect-blob-storage-account-name-and-key"></a><span data-ttu-id="1c88c-132">Collect blob storage account name and key</span><span class="sxs-lookup"><span data-stu-id="1c88c-132">Collect blob storage account name and key</span></span>
<span data-ttu-id="1c88c-133">You need the account name and account key of your Azure storage account to do this tutorial.</span><span class="sxs-lookup"><span data-stu-id="1c88c-133">You need the account name and account key of your Azure storage account to do this tutorial.</span></span> <span data-ttu-id="1c88c-134">Note down **account name** and **account key** for your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="1c88c-134">Note down **account name** and **account key** for your Azure storage account.</span></span>

1. <span data-ttu-id="1c88c-135">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1c88c-135">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1c88c-136">Click **All services** on the left menu and select **Storage Accounts**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-136">Click **All services** on the left menu and select **Storage Accounts**.</span></span>

    ![Browse - Storage accounts](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. <span data-ttu-id="1c88c-138">In the **Storage Accounts** blade, select the **Azure storage account** that you want to use in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="1c88c-138">In the **Storage Accounts** blade, select the **Azure storage account** that you want to use in this tutorial.</span></span>
4. <span data-ttu-id="1c88c-139">Select **Access keys** link under **SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-139">Select **Access keys** link under **SETTINGS**.</span></span>
5. <span data-ttu-id="1c88c-140">Click **copy** (image) button next to **Storage account name** text box and save/paste it somewhere (for example: in a text file).</span><span class="sxs-lookup"><span data-stu-id="1c88c-140">Click **copy** (image) button next to **Storage account name** text box and save/paste it somewhere (for example: in a text file).</span></span>
6. <span data-ttu-id="1c88c-141">Repeat the previous step to copy or note down the **key1**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-141">Repeat the previous step to copy or note down the **key1**.</span></span>

    ![Storage access key](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. <span data-ttu-id="1c88c-143">Close all the blades by clicking **X**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-143">Close all the blades by clicking **X**.</span></span>

## <a name="collect-sql-server-database-user-names"></a><span data-ttu-id="1c88c-144">Collect SQL server, database, user names</span><span class="sxs-lookup"><span data-stu-id="1c88c-144">Collect SQL server, database, user names</span></span>
<span data-ttu-id="1c88c-145">You need the names of Azure SQL server, database, and user to do this tutorial.</span><span class="sxs-lookup"><span data-stu-id="1c88c-145">You need the names of Azure SQL server, database, and user to do this tutorial.</span></span> <span data-ttu-id="1c88c-146">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="1c88c-146">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span></span>

1. <span data-ttu-id="1c88c-147">In the **Azure portal**, click **All services** on the left and select **SQL databases**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-147">In the **Azure portal**, click **All services** on the left and select **SQL databases**.</span></span>
2. <span data-ttu-id="1c88c-148">In the **SQL databases blade**, select the **database** that you want to use in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="1c88c-148">In the **SQL databases blade**, select the **database** that you want to use in this tutorial.</span></span> <span data-ttu-id="1c88c-149">Note down the **database name**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-149">Note down the **database name**.</span></span>  
3. <span data-ttu-id="1c88c-150">In the **SQL database** blade, click **Properties** under **SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-150">In the **SQL database** blade, click **Properties** under **SETTINGS**.</span></span>
4. <span data-ttu-id="1c88c-151">Note down the values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-151">Note down the values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span></span>
5. <span data-ttu-id="1c88c-152">Close all the blades by clicking **X**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-152">Close all the blades by clicking **X**.</span></span>

## <a name="allow-azure-services-to-access-sql-server"></a><span data-ttu-id="1c88c-153">Allow Azure services to access SQL server</span><span class="sxs-lookup"><span data-stu-id="1c88c-153">Allow Azure services to access SQL server</span></span>
<span data-ttu-id="1c88c-154">Ensure that **Allow access to Azure services** setting turned **ON** for your Azure SQL server so that the Data Factory service can access your Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="1c88c-154">Ensure that **Allow access to Azure services** setting turned **ON** for your Azure SQL server so that the Data Factory service can access your Azure SQL server.</span></span> <span data-ttu-id="1c88c-155">To verify and turn on this setting, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="1c88c-155">To verify and turn on this setting, do the following steps:</span></span>

1. <span data-ttu-id="1c88c-156">Click **All services** hub on the left and click **SQL servers**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-156">Click **All services** hub on the left and click **SQL servers**.</span></span>
2. <span data-ttu-id="1c88c-157">Select your server, and click **Firewall** under **SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-157">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
3. <span data-ttu-id="1c88c-158">In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-158">In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.</span></span>
4. <span data-ttu-id="1c88c-159">Close all the blades by clicking **X**.</span><span class="sxs-lookup"><span data-stu-id="1c88c-159">Close all the blades by clicking **X**.</span></span>

## <a name="prepare-blob-storage-and-sql-database"></a><span data-ttu-id="1c88c-160">Prepare Blob Storage and SQL Database</span><span class="sxs-lookup"><span data-stu-id="1c88c-160">Prepare Blob Storage and SQL Database</span></span>
<span data-ttu-id="1c88c-161">Now, prepare your Azure blob storage and Azure SQL database for the tutorial by performing the following steps:</span><span class="sxs-lookup"><span data-stu-id="1c88c-161">Now, prepare your Azure blob storage and Azure SQL database for the tutorial by performing the following steps:</span></span>  

1. <span data-ttu-id="1c88c-162">Launch Notepad.</span><span class="sxs-lookup"><span data-stu-id="1c88c-162">Launch Notepad.</span></span> <span data-ttu-id="1c88c-163">Copy the following text and save it as **emp.txt** to **C:\ADFGetStarted** folder on your hard drive.</span><span class="sxs-lookup"><span data-stu-id="1c88c-163">Copy the following text and save it as **emp.txt** to **C:\ADFGetStarted** folder on your hard drive.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
2. <span data-ttu-id="1c88c-164">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) to create the **adftutorial** container and to upload the **emp.txt** file to the container.</span><span class="sxs-lookup"><span data-stu-id="1c88c-164">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) to create the **adftutorial** container and to upload the **emp.txt** file to the container.</span></span>

    ![Azure Storage Explorer.](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. <span data-ttu-id="1c88c-167">Use the following SQL script to create the **emp** table in your Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="1c88c-167">Use the following SQL script to create the **emp** table in your Azure SQL Database.</span></span>  

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

    <span data-ttu-id="1c88c-168">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../../sql-database/sql-database-manage-azure-ssms.md) to connect to your Azure SQL server and run the SQL script.</span><span class="sxs-lookup"><span data-stu-id="1c88c-168">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../../sql-database/sql-database-manage-azure-ssms.md) to connect to your Azure SQL server and run the SQL script.</span></span> 

    <span data-ttu-id="1c88c-169">If your client is not allowed to access the Azure SQL server, you need to configure firewall for your Azure SQL server to allow access from your machine (IP Address).</span><span class="sxs-lookup"><span data-stu-id="1c88c-169">If your client is not allowed to access the Azure SQL server, you need to configure firewall for your Azure SQL server to allow access from your machine (IP Address).</span></span> <span data-ttu-id="1c88c-170">See [this article](../../sql-database/sql-database-configure-firewall-settings.md) for steps to configure the firewall for your Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="1c88c-170">See [this article](../../sql-database/sql-database-configure-firewall-settings.md) for steps to configure the firewall for your Azure SQL server.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="1c88c-171">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="1c88c-171">Create a data factory</span></span>
<span data-ttu-id="1c88c-172">You have completed the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="1c88c-172">You have completed the prerequisites.</span></span> <span data-ttu-id="1c88c-173">You can create a data factory using one of the following ways.</span><span class="sxs-lookup"><span data-stu-id="1c88c-173">You can create a data factory using one of the following ways.</span></span> <span data-ttu-id="1c88c-174">Click one of the options in the drop-down list at the top or the following links to perform the tutorial.</span><span class="sxs-lookup"><span data-stu-id="1c88c-174">Click one of the options in the drop-down list at the top or the following links to perform the tutorial.</span></span>     

* [<span data-ttu-id="1c88c-175">Copy Wizard</span><span class="sxs-lookup"><span data-stu-id="1c88c-175">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
* [<span data-ttu-id="1c88c-176">Azure portal</span><span class="sxs-lookup"><span data-stu-id="1c88c-176">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [<span data-ttu-id="1c88c-177">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1c88c-177">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [<span data-ttu-id="1c88c-178">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c88c-178">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
* [<span data-ttu-id="1c88c-179">Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="1c88c-179">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="1c88c-180">REST API</span><span class="sxs-lookup"><span data-stu-id="1c88c-180">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
* [<span data-ttu-id="1c88c-181">.NET API</span><span class="sxs-lookup"><span data-stu-id="1c88c-181">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> The data pipeline in this tutorial copies data from a source data store to a destination data store. It does not transform input data to produce output data. For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).
> 
> You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity. See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information. 
