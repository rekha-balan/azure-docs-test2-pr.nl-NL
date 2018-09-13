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
# <a name="tutorial-copy-data-from-blob-storage-to-sql-database-using-data-factory"></a><span data-ttu-id="cbfe0-104">Tutorial: Copy data from Blob Storage to SQL Database using Data Factory</span><span class="sxs-lookup"><span data-stu-id="cbfe0-104">Tutorial: Copy data from Blob Storage to SQL Database using Data Factory</span></span>
> [!div class="op_single_selector"]
> * [Overview and prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Copy Wizard](data-factory-copy-data-wizard-tutorial.md)
> * [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="cbfe0-113">In this tutorial, you create a data factory with a pipeline to copy data from Blob storage to SQL database.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-113">In this tutorial, you create a data factory with a pipeline to copy data from Blob storage to SQL database.</span></span>

<span data-ttu-id="cbfe0-114">The Copy Activity performs the data movement in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-114">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="cbfe0-115">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-115">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="cbfe0-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>  

> [!NOTE]
> For a detailed overview of the Data Factory service, see the [Introduction to Azure Data Factory](data-factory-introduction.md) article.
>
>

## <a name="prerequisites-for-the-tutorial"></a><span data-ttu-id="cbfe0-118">Prerequisites for the tutorial</span><span class="sxs-lookup"><span data-stu-id="cbfe0-118">Prerequisites for the tutorial</span></span>
<span data-ttu-id="cbfe0-119">Before you begin this tutorial, you must have the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="cbfe0-119">Before you begin this tutorial, you must have the following prerequisites:</span></span>

* <span data-ttu-id="cbfe0-120">**Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-120">**Azure subscription**.</span></span>  <span data-ttu-id="cbfe0-121">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-121">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="cbfe0-122">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-122">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="cbfe0-123">**Azure Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-123">**Azure Storage Account**.</span></span> <span data-ttu-id="cbfe0-124">You use the blob storage as a **source** data store in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-124">You use the blob storage as a **source** data store in this tutorial.</span></span> <span data-ttu-id="cbfe0-125">if you don't have an Azure storage account, see the [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-125">if you don't have an Azure storage account, see the [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
* <span data-ttu-id="cbfe0-126">**Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-126">**Azure SQL Database**.</span></span> <span data-ttu-id="cbfe0-127">You use an Azure SQL database as a **destination** data store in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-127">You use an Azure SQL database as a **destination** data store in this tutorial.</span></span> <span data-ttu-id="cbfe0-128">If you don't have an Azure SQL database that you can use in the tutorial, See [How to create and configure an Azure SQL Database](../sql-database/sql-database-get-started.md) to create one.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-128">If you don't have an Azure SQL database that you can use in the tutorial, See [How to create and configure an Azure SQL Database](../sql-database/sql-database-get-started.md) to create one.</span></span>
* <span data-ttu-id="cbfe0-129">**SQL Server 2012/2014 or Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-129">**SQL Server 2012/2014 or Visual Studio 2013**.</span></span> <span data-ttu-id="cbfe0-130">You use SQL Server Management Studio or Visual Studio to create a sample database and to view the result data in the database.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-130">You use SQL Server Management Studio or Visual Studio to create a sample database and to view the result data in the database.</span></span>  

## <a name="collect-blob-storage-account-name-and-key"></a><span data-ttu-id="cbfe0-131">Collect blob storage account name and key</span><span class="sxs-lookup"><span data-stu-id="cbfe0-131">Collect blob storage account name and key</span></span>
<span data-ttu-id="cbfe0-132">You need the account name and account key of your Azure storage account to do this tutorial.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-132">You need the account name and account key of your Azure storage account to do this tutorial.</span></span> <span data-ttu-id="cbfe0-133">Note down **account name** and **account key** for your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-133">Note down **account name** and **account key** for your Azure storage account.</span></span>

1. <span data-ttu-id="cbfe0-134">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cbfe0-134">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="cbfe0-135">Click **More services** on the left menu and select **Storage Accounts**.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-135">Click **More services** on the left menu and select **Storage Accounts**.</span></span>

    ![Browse - Storage accounts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. <span data-ttu-id="cbfe0-137">In the **Storage Accounts** blade, select the **Azure storage account** that you want to use in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-137">In the **Storage Accounts** blade, select the **Azure storage account** that you want to use in this tutorial.</span></span>
4. <span data-ttu-id="cbfe0-138">Select **Access keys** link under **SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-138">Select **Access keys** link under **SETTINGS**.</span></span>
5. <span data-ttu-id="cbfe0-139">Click **copy** (image) button next to **Storage account name** text box and save/paste it somewhere (for example: in a text file).</span><span class="sxs-lookup"><span data-stu-id="cbfe0-139">Click **copy** (image) button next to **Storage account name** text box and save/paste it somewhere (for example: in a text file).</span></span>
6. <span data-ttu-id="cbfe0-140">Repeat the previous step to copy or note down the **key1**.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-140">Repeat the previous step to copy or note down the **key1**.</span></span>

    ![Storage access key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. <span data-ttu-id="cbfe0-142">Close all the blades by clicking **X**.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-142">Close all the blades by clicking **X**.</span></span>

## <a name="collect-sql-server-database-user-names"></a><span data-ttu-id="cbfe0-143">Collect SQL server, database, user names</span><span class="sxs-lookup"><span data-stu-id="cbfe0-143">Collect SQL server, database, user names</span></span>
<span data-ttu-id="cbfe0-144">You need the names of Azure SQL server, database, and user to do this tutorial.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-144">You need the names of Azure SQL server, database, and user to do this tutorial.</span></span> <span data-ttu-id="cbfe0-145">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-145">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span></span>

1. <span data-ttu-id="cbfe0-146">In the **Azure portal**, click **More services** on the left and select **SQL databases**.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-146">In the **Azure portal**, click **More services** on the left and select **SQL databases**.</span></span>
2. <span data-ttu-id="cbfe0-147">In the **SQL databases blade**, select the **database** that you want to use in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-147">In the **SQL databases blade**, select the **database** that you want to use in this tutorial.</span></span> <span data-ttu-id="cbfe0-148">Note down the **database name**.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-148">Note down the **database name**.</span></span>  
3. <span data-ttu-id="cbfe0-149">In the **SQL database** blade, click **Properties** under **SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-149">In the **SQL database** blade, click **Properties** under **SETTINGS**.</span></span>
4. <span data-ttu-id="cbfe0-150">Note down the values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-150">Note down the values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span></span>
5. <span data-ttu-id="cbfe0-151">Close all the blades by clicking **X**.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-151">Close all the blades by clicking **X**.</span></span>

## <a name="allow-azure-services-to-access-sql-server"></a><span data-ttu-id="cbfe0-152">Allow Azure services to access SQL server</span><span class="sxs-lookup"><span data-stu-id="cbfe0-152">Allow Azure services to access SQL server</span></span>
<span data-ttu-id="cbfe0-153">Ensure that **Allow access to Azure services** setting turned **ON** for your Azure SQL server so that the Data Factory service can access your Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-153">Ensure that **Allow access to Azure services** setting turned **ON** for your Azure SQL server so that the Data Factory service can access your Azure SQL server.</span></span> <span data-ttu-id="cbfe0-154">To verify and turn on this setting, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="cbfe0-154">To verify and turn on this setting, do the following steps:</span></span>

1. <span data-ttu-id="cbfe0-155">Click **More services** hub on the left and click **SQL servers**.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-155">Click **More services** hub on the left and click **SQL servers**.</span></span>
2. <span data-ttu-id="cbfe0-156">Select your server, and click **Firewall** under **SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-156">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
3. <span data-ttu-id="cbfe0-157">In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-157">In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.</span></span>
4. <span data-ttu-id="cbfe0-158">Close all the blades by clicking **X**.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-158">Close all the blades by clicking **X**.</span></span>

## <a name="prepare-blob-storage-and-sql-database"></a><span data-ttu-id="cbfe0-159">Prepare Blob Storage and SQL Database</span><span class="sxs-lookup"><span data-stu-id="cbfe0-159">Prepare Blob Storage and SQL Database</span></span>
<span data-ttu-id="cbfe0-160">Now, prepare your Azure blob storage and Azure SQL database for the tutorial by performing the following steps:</span><span class="sxs-lookup"><span data-stu-id="cbfe0-160">Now, prepare your Azure blob storage and Azure SQL database for the tutorial by performing the following steps:</span></span>  

1. <span data-ttu-id="cbfe0-161">Launch Notepad.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-161">Launch Notepad.</span></span> <span data-ttu-id="cbfe0-162">Copy the following text and save it as **emp.txt** to **C:\ADFGetStarted** folder on your hard drive.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-162">Copy the following text and save it as **emp.txt** to **C:\ADFGetStarted** folder on your hard drive.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
2. <span data-ttu-id="cbfe0-163">Use tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/) to create the **adftutorial** container and to upload the **emp.txt** file to the container.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-163">Use tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/) to create the **adftutorial** container and to upload the **emp.txt** file to the container.</span></span>

    ![Azure Storage Explorer.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. <span data-ttu-id="cbfe0-166">Use the following SQL script to create the **emp** table in your Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-166">Use the following SQL script to create the **emp** table in your Azure SQL Database.</span></span>  

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

    <span data-ttu-id="cbfe0-167">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) to connect to your Azure SQL server and run the SQL script.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-167">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) to connect to your Azure SQL server and run the SQL script.</span></span> <span data-ttu-id="cbfe0-168">This article uses the [classic Azure portal](http://manage.windowsazure.com), not the [new Azure portal](https://portal.azure.com), to configure firewall for an Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-168">This article uses the [classic Azure portal](http://manage.windowsazure.com), not the [new Azure portal](https://portal.azure.com), to configure firewall for an Azure SQL server.</span></span>

    <span data-ttu-id="cbfe0-169">If your client is not allowed to access the Azure SQL server, you need to configure firewall for your Azure SQL server to allow access from your machine (IP Address).</span><span class="sxs-lookup"><span data-stu-id="cbfe0-169">If your client is not allowed to access the Azure SQL server, you need to configure firewall for your Azure SQL server to allow access from your machine (IP Address).</span></span> <span data-ttu-id="cbfe0-170">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps to configure the firewall for your Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-170">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps to configure the firewall for your Azure SQL server.</span></span>

<span data-ttu-id="cbfe0-171">You have completed the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-171">You have completed the prerequisites.</span></span> <span data-ttu-id="cbfe0-172">You can create a data factory using one of the following ways.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-172">You can create a data factory using one of the following ways.</span></span> <span data-ttu-id="cbfe0-173">Click one of the options in the drop-down list at the top or the following links to perform the tutorial.</span><span class="sxs-lookup"><span data-stu-id="cbfe0-173">Click one of the options in the drop-down list at the top or the following links to perform the tutorial.</span></span>     

* [<span data-ttu-id="cbfe0-174">Copy Wizard</span><span class="sxs-lookup"><span data-stu-id="cbfe0-174">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
* [<span data-ttu-id="cbfe0-175">Azure portal</span><span class="sxs-lookup"><span data-stu-id="cbfe0-175">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [<span data-ttu-id="cbfe0-176">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cbfe0-176">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [<span data-ttu-id="cbfe0-177">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cbfe0-177">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
* [<span data-ttu-id="cbfe0-178">Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="cbfe0-178">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="cbfe0-179">REST API</span><span class="sxs-lookup"><span data-stu-id="cbfe0-179">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
* [<span data-ttu-id="cbfe0-180">.NET API</span><span class="sxs-lookup"><span data-stu-id="cbfe0-180">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> The data pipeline in this tutorial copies data from a source data store to a destination data store. It does not transform input data to produce output data. For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).
> 
> You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity. See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information. 


