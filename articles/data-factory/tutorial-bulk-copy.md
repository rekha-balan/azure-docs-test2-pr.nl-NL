---
title: Copy data in bulk using Azure Data Factory | Microsoft Docs
description: Learn how to use Azure Data Factory and Copy Activity to copy data from a source data store to a destination data store in bulk.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/22/2018
ms.author: jingwang
ms.openlocfilehash: 1bf93ce9aa1733634b46c2a15b587d4cc0826ba1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857044"
---
# <a name="copy-multiple-tables-in-bulk-by-using-azure-data-factory"></a><span data-ttu-id="84d63-103">Copy multiple tables in bulk by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="84d63-103">Copy multiple tables in bulk by using Azure Data Factory</span></span>
<span data-ttu-id="84d63-104">This tutorial demonstrates **copying a number of tables from Azure SQL Database to Azure SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="84d63-104">This tutorial demonstrates **copying a number of tables from Azure SQL Database to Azure SQL Data Warehouse**.</span></span> <span data-ttu-id="84d63-105">You can apply the same pattern in other copy scenarios as well.</span><span class="sxs-lookup"><span data-stu-id="84d63-105">You can apply the same pattern in other copy scenarios as well.</span></span> <span data-ttu-id="84d63-106">For example, copying tables from SQL Server/Oracle to Azure SQL Database/Data Warehouse/Azure Blob, copying different paths from Blob to Azure SQL Database tables.</span><span class="sxs-lookup"><span data-stu-id="84d63-106">For example, copying tables from SQL Server/Oracle to Azure SQL Database/Data Warehouse/Azure Blob, copying different paths from Blob to Azure SQL Database tables.</span></span>

<span data-ttu-id="84d63-107">At a high level, this tutorial involves following steps:</span><span class="sxs-lookup"><span data-stu-id="84d63-107">At a high level, this tutorial involves following steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="84d63-108">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="84d63-108">Create a data factory.</span></span>
> * <span data-ttu-id="84d63-109">Create Azure SQL Database, Azure SQL Data Warehouse, and Azure Storage linked services.</span><span class="sxs-lookup"><span data-stu-id="84d63-109">Create Azure SQL Database, Azure SQL Data Warehouse, and Azure Storage linked services.</span></span>
> * <span data-ttu-id="84d63-110">Create Azure SQL Database and Azure SQL Data Warehouse datasets.</span><span class="sxs-lookup"><span data-stu-id="84d63-110">Create Azure SQL Database and Azure SQL Data Warehouse datasets.</span></span>
> * <span data-ttu-id="84d63-111">Create a  pipeline to look up the tables to be copied and another pipeline to perform the actual copy operation.</span><span class="sxs-lookup"><span data-stu-id="84d63-111">Create a  pipeline to look up the tables to be copied and another pipeline to perform the actual copy operation.</span></span> 
> * <span data-ttu-id="84d63-112">Start a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="84d63-112">Start a pipeline run.</span></span>
> * <span data-ttu-id="84d63-113">Monitor the pipeline and activity runs.</span><span class="sxs-lookup"><span data-stu-id="84d63-113">Monitor the pipeline and activity runs.</span></span>

<span data-ttu-id="84d63-114">This tutorial uses Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="84d63-114">This tutorial uses Azure PowerShell.</span></span> <span data-ttu-id="84d63-115">To learn about using other tools/SDKs to create a data factory, see [Quickstarts](quickstart-create-data-factory-dot-net.md).</span><span class="sxs-lookup"><span data-stu-id="84d63-115">To learn about using other tools/SDKs to create a data factory, see [Quickstarts](quickstart-create-data-factory-dot-net.md).</span></span> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="84d63-116">End-to-end workflow</span><span class="sxs-lookup"><span data-stu-id="84d63-116">End-to-end workflow</span></span>
<span data-ttu-id="84d63-117">In this scenario, we have a number of tables in Azure SQL Database that we want to copy to SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="84d63-117">In this scenario, we have a number of tables in Azure SQL Database that we want to copy to SQL Data Warehouse.</span></span> <span data-ttu-id="84d63-118">Here is the logical sequence of steps in the workflow that happens in pipelines:</span><span class="sxs-lookup"><span data-stu-id="84d63-118">Here is the logical sequence of steps in the workflow that happens in pipelines:</span></span>

![Workflow](media/tutorial-bulk-copy/tutorial-copy-multiple-tables.png)

* <span data-ttu-id="84d63-120">The first pipeline looks up the list of tables that needs to be copied over to the sink data stores.</span><span class="sxs-lookup"><span data-stu-id="84d63-120">The first pipeline looks up the list of tables that needs to be copied over to the sink data stores.</span></span>  <span data-ttu-id="84d63-121">Alternatively you can maintain a metadata table that lists all the tables to be copied to the sink data store.</span><span class="sxs-lookup"><span data-stu-id="84d63-121">Alternatively you can maintain a metadata table that lists all the tables to be copied to the sink data store.</span></span> <span data-ttu-id="84d63-122">Then, the pipeline triggers another pipeline, which iterates over each table in the database and performs the data copy operation.</span><span class="sxs-lookup"><span data-stu-id="84d63-122">Then, the pipeline triggers another pipeline, which iterates over each table in the database and performs the data copy operation.</span></span>
* <span data-ttu-id="84d63-123">The second pipeline performs the actual copy.</span><span class="sxs-lookup"><span data-stu-id="84d63-123">The second pipeline performs the actual copy.</span></span> <span data-ttu-id="84d63-124">It takes the list of tables as a parameter.</span><span class="sxs-lookup"><span data-stu-id="84d63-124">It takes the list of tables as a parameter.</span></span> <span data-ttu-id="84d63-125">For each table in the list, copy the specific table in Azure SQL Database to the corresponding table in SQL Data Warehouse using [staged copy via Blob storage and PolyBase](connector-azure-sql-data-warehouse.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) for best performance.</span><span class="sxs-lookup"><span data-stu-id="84d63-125">For each table in the list, copy the specific table in Azure SQL Database to the corresponding table in SQL Data Warehouse using [staged copy via Blob storage and PolyBase](connector-azure-sql-data-warehouse.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) for best performance.</span></span> <span data-ttu-id="84d63-126">In this example, the first pipeline passes the list of tables as a value for the parameter.</span><span class="sxs-lookup"><span data-stu-id="84d63-126">In this example, the first pipeline passes the list of tables as a value for the parameter.</span></span> 

<span data-ttu-id="84d63-127">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="84d63-127">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84d63-128">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="84d63-128">Prerequisites</span></span>

* <span data-ttu-id="84d63-129">**Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="84d63-129">**Azure PowerShell**.</span></span> <span data-ttu-id="84d63-130">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="84d63-130">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>
* <span data-ttu-id="84d63-131">**Azure Storage account**.</span><span class="sxs-lookup"><span data-stu-id="84d63-131">**Azure Storage account**.</span></span> <span data-ttu-id="84d63-132">The Azure Storage account is used as staging blob storage in the bulk copy operation.</span><span class="sxs-lookup"><span data-stu-id="84d63-132">The Azure Storage account is used as staging blob storage in the bulk copy operation.</span></span> 
* <span data-ttu-id="84d63-133">**Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="84d63-133">**Azure SQL Database**.</span></span> <span data-ttu-id="84d63-134">This database contains the source data.</span><span class="sxs-lookup"><span data-stu-id="84d63-134">This database contains the source data.</span></span> 
* <span data-ttu-id="84d63-135">**Azure SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="84d63-135">**Azure SQL Data Warehouse**.</span></span> <span data-ttu-id="84d63-136">This data warehouse holds the data copied over from the SQL Database.</span><span class="sxs-lookup"><span data-stu-id="84d63-136">This data warehouse holds the data copied over from the SQL Database.</span></span> 

### <a name="prepare-sql-database-and-sql-data-warehouse"></a><span data-ttu-id="84d63-137">Prepare SQL Database and SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="84d63-137">Prepare SQL Database and SQL Data Warehouse</span></span>

<span data-ttu-id="84d63-138">**Prepare the source Azure SQL Database**:</span><span class="sxs-lookup"><span data-stu-id="84d63-138">**Prepare the source Azure SQL Database**:</span></span>

<span data-ttu-id="84d63-139">Create an Azure SQL Database with Adventure Works LT sample data following [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) article.</span><span class="sxs-lookup"><span data-stu-id="84d63-139">Create an Azure SQL Database with Adventure Works LT sample data following [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) article.</span></span> <span data-ttu-id="84d63-140">This tutorial copies all the tables from this sample database to a SQL data warehouse.</span><span class="sxs-lookup"><span data-stu-id="84d63-140">This tutorial copies all the tables from this sample database to a SQL data warehouse.</span></span>

<span data-ttu-id="84d63-141">**Prepare the sink Azure SQL Data Warehouse**:</span><span class="sxs-lookup"><span data-stu-id="84d63-141">**Prepare the sink Azure SQL Data Warehouse**:</span></span>

1. <span data-ttu-id="84d63-142">If you don't have an Azure SQL Data Warehouse, see the [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-tutorial.md) article for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="84d63-142">If you don't have an Azure SQL Data Warehouse, see the [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-tutorial.md) article for steps to create one.</span></span>

2. <span data-ttu-id="84d63-143">Create corresponding table schemas in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="84d63-143">Create corresponding table schemas in SQL Data Warehouse.</span></span> <span data-ttu-id="84d63-144">You can use [Migration Utility](https://www.microsoft.com/download/details.aspx?id=49100) to **migrate schema** from Azure SQL Database to Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="84d63-144">You can use [Migration Utility](https://www.microsoft.com/download/details.aspx?id=49100) to **migrate schema** from Azure SQL Database to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="84d63-145">You use Azure Data Factory to migrate/copy data in a later step.</span><span class="sxs-lookup"><span data-stu-id="84d63-145">You use Azure Data Factory to migrate/copy data in a later step.</span></span>

## <a name="azure-services-to-access-sql-server"></a><span data-ttu-id="84d63-146">Azure services to access SQL server</span><span class="sxs-lookup"><span data-stu-id="84d63-146">Azure services to access SQL server</span></span>

<span data-ttu-id="84d63-147">For both SQL Database and SQL Data Warehouse, allow Azure services to access SQL server.</span><span class="sxs-lookup"><span data-stu-id="84d63-147">For both SQL Database and SQL Data Warehouse, allow Azure services to access SQL server.</span></span> <span data-ttu-id="84d63-148">Ensure that **Allow access to Azure services** setting is turned **ON** for your Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="84d63-148">Ensure that **Allow access to Azure services** setting is turned **ON** for your Azure SQL server.</span></span> <span data-ttu-id="84d63-149">This setting allows the Data Factory service to read data from your Azure SQL Database and write data to your Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="84d63-149">This setting allows the Data Factory service to read data from your Azure SQL Database and write data to your Azure SQL Data Warehouse.</span></span> <span data-ttu-id="84d63-150">To verify and turn on this setting, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="84d63-150">To verify and turn on this setting, do the following steps:</span></span>

1. <span data-ttu-id="84d63-151">Click **All services** on the left and click **SQL servers**.</span><span class="sxs-lookup"><span data-stu-id="84d63-151">Click **All services** on the left and click **SQL servers**.</span></span>
2. <span data-ttu-id="84d63-152">Select your server, and click **Firewall** under **SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="84d63-152">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
3. <span data-ttu-id="84d63-153">In the **Firewall settings** page, click **ON** for **Allow access to Azure services**.</span><span class="sxs-lookup"><span data-stu-id="84d63-153">In the **Firewall settings** page, click **ON** for **Allow access to Azure services**.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="84d63-154">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="84d63-154">Create a data factory</span></span>

1. <span data-ttu-id="84d63-155">Launch **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="84d63-155">Launch **PowerShell**.</span></span> <span data-ttu-id="84d63-156">Keep Azure PowerShell open until the end of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="84d63-156">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="84d63-157">If you close and reopen, you need to run the commands again.</span><span class="sxs-lookup"><span data-stu-id="84d63-157">If you close and reopen, you need to run the commands again.</span></span>

    <span data-ttu-id="84d63-158">Run the following command, and enter the user name and password that you use to sign in to the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="84d63-158">Run the following command, and enter the user name and password that you use to sign in to the Azure portal:</span></span>
        
    ```powershell
    Connect-AzureRmAccount
    ```
    <span data-ttu-id="84d63-159">Run the following command to view all the subscriptions for this account:</span><span class="sxs-lookup"><span data-stu-id="84d63-159">Run the following command to view all the subscriptions for this account:</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```
    <span data-ttu-id="84d63-160">Run the following command to select the subscription that you want to work with.</span><span class="sxs-lookup"><span data-stu-id="84d63-160">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="84d63-161">Replace **SubscriptionId** with the ID of your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="84d63-161">Replace **SubscriptionId** with the ID of your Azure subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<SubscriptionId>"
    ```
2. <span data-ttu-id="84d63-162">Run the **Set-AzureRmDataFactoryV2** cmdlet to create a data factory.</span><span class="sxs-lookup"><span data-stu-id="84d63-162">Run the **Set-AzureRmDataFactoryV2** cmdlet to create a data factory.</span></span> <span data-ttu-id="84d63-163">Replace place-holders with your own values before executing the command.</span><span class="sxs-lookup"><span data-stu-id="84d63-163">Replace place-holders with your own values before executing the command.</span></span> 

    ```powershell
    $resourceGroupName = "<your resource group to create the factory>"
    $dataFactoryName = "<specify the name of data factory to create. It must be globally unique.>"
    Set-AzureRmDataFactoryV2 -ResourceGroupName $resourceGroupName -Location "East US" -Name $dataFactoryName
    ```

    <span data-ttu-id="84d63-164">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="84d63-164">Note the following points:</span></span>

    * <span data-ttu-id="84d63-165">The name of the Azure data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="84d63-165">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="84d63-166">If you receive the following error, change the name and try again.</span><span class="sxs-lookup"><span data-stu-id="84d63-166">If you receive the following error, change the name and try again.</span></span>

        ```
        The specified Data Factory name 'ADFv2QuickStartDataFactory' is already in use. Data Factory names must be globally unique.
        ```

    * <span data-ttu-id="84d63-167">To create Data Factory instances, you must be a Contributor or Administrator of the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="84d63-167">To create Data Factory instances, you must be a Contributor or Administrator of the Azure subscription.</span></span>
    * <span data-ttu-id="84d63-168">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="84d63-168">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span></span> <span data-ttu-id="84d63-169">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="84d63-169">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="84d63-170">Create linked services</span><span class="sxs-lookup"><span data-stu-id="84d63-170">Create linked services</span></span>

<span data-ttu-id="84d63-171">In this tutorial, you create three linked services for source, sink, and staging blob respectively, which includes connections to your data stores:</span><span class="sxs-lookup"><span data-stu-id="84d63-171">In this tutorial, you create three linked services for source, sink, and staging blob respectively, which includes connections to your data stores:</span></span>

### <a name="create-the-source-azure-sql-database-linked-service"></a><span data-ttu-id="84d63-172">Create the source Azure SQL Database linked service</span><span class="sxs-lookup"><span data-stu-id="84d63-172">Create the source Azure SQL Database linked service</span></span>

1. <span data-ttu-id="84d63-173">Create a JSON file named **AzureSqlDatabaseLinkedService.json** in **C:\ADFv2TutorialBulkCopy** folder with the following content: (Create the folder ADFv2TutorialBulkCopy if it does not already exist.)</span><span class="sxs-lookup"><span data-stu-id="84d63-173">Create a JSON file named **AzureSqlDatabaseLinkedService.json** in **C:\ADFv2TutorialBulkCopy** folder with the following content: (Create the folder ADFv2TutorialBulkCopy if it does not already exist.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="84d63-174">Replace &lt;servername&gt;, &lt;databasename&gt;, &lt;username&gt;@&lt;servername&gt; and &lt;password&gt; with values of your Azure SQL Database before saving the file.</span><span class="sxs-lookup"><span data-stu-id="84d63-174">Replace &lt;servername&gt;, &lt;databasename&gt;, &lt;username&gt;@&lt;servername&gt; and &lt;password&gt; with values of your Azure SQL Database before saving the file.</span></span>

    ```json
    {
        "name": "AzureSqlDatabaseLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
                }
            }
        }
    }
    ```

2. <span data-ttu-id="84d63-175">In **Azure PowerShell**, switch to the **ADFv2TutorialBulkCopy** folder.</span><span class="sxs-lookup"><span data-stu-id="84d63-175">In **Azure PowerShell**, switch to the **ADFv2TutorialBulkCopy** folder.</span></span>

3. <span data-ttu-id="84d63-176">Run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet to create the linked service: **AzureSqlDatabaseLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="84d63-176">Run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet to create the linked service: **AzureSqlDatabaseLinkedService**.</span></span> 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureSqlDatabaseLinkedService" -File ".\AzureSqlDatabaseLinkedService.json"
    ```

    <span data-ttu-id="84d63-177">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="84d63-177">Here is the sample output:</span></span>

    ```json
    LinkedServiceName : AzureSqlDatabaseLinkedService
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlDatabaseLinkedService
    ```

### <a name="create-the-sink-azure-sql-data-warehouse-linked-service"></a><span data-ttu-id="84d63-178">Create the sink Azure SQL Data Warehouse linked service</span><span class="sxs-lookup"><span data-stu-id="84d63-178">Create the sink Azure SQL Data Warehouse linked service</span></span>

1. <span data-ttu-id="84d63-179">Create a JSON file named **AzureSqlDWLinkedService.json** in the **C:\ADFv2TutorialBulkCopy** folder, with the following content:</span><span class="sxs-lookup"><span data-stu-id="84d63-179">Create a JSON file named **AzureSqlDWLinkedService.json** in the **C:\ADFv2TutorialBulkCopy** folder, with the following content:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="84d63-180">Replace &lt;servername&gt;, &lt;databasename&gt;, &lt;username&gt;@&lt;servername&gt; and &lt;password&gt; with values of your Azure SQL Database before saving the file.</span><span class="sxs-lookup"><span data-stu-id="84d63-180">Replace &lt;servername&gt;, &lt;databasename&gt;, &lt;username&gt;@&lt;servername&gt; and &lt;password&gt; with values of your Azure SQL Database before saving the file.</span></span>

    ```json
    {
        "name": "AzureSqlDWLinkedService",
        "properties": {
            "type": "AzureSqlDW",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
            }
        }
    }
    ```

2. <span data-ttu-id="84d63-181">To create the linked service: **AzureSqlDWLinkedService**, run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="84d63-181">To create the linked service: **AzureSqlDWLinkedService**, run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet.</span></span>

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureSqlDWLinkedService" -File ".\AzureSqlDWLinkedService.json"
    ```

    <span data-ttu-id="84d63-182">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="84d63-182">Here is the sample output:</span></span>

    ```json
    LinkedServiceName : AzureSqlDWLinkedService
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlDWLinkedService
    ```

### <a name="create-the-staging-azure-storage-linked-service"></a><span data-ttu-id="84d63-183">Create the staging Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="84d63-183">Create the staging Azure Storage linked service</span></span>

<span data-ttu-id="84d63-184">In this tutorial, you use Azure Blob storage as an interim staging area to enable PolyBase for a better copy performance.</span><span class="sxs-lookup"><span data-stu-id="84d63-184">In this tutorial, you use Azure Blob storage as an interim staging area to enable PolyBase for a better copy performance.</span></span>

1. <span data-ttu-id="84d63-185">Create a JSON file named **AzureStorageLinkedService.json** in the **C:\ADFv2TutorialBulkCopy** folder, with the following content:</span><span class="sxs-lookup"><span data-stu-id="84d63-185">Create a JSON file named **AzureStorageLinkedService.json** in the **C:\ADFv2TutorialBulkCopy** folder, with the following content:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="84d63-186">Replace &lt;accountName&gt; and &lt;accountKey&gt; with name and key of your Azure storage account before saving the file.</span><span class="sxs-lookup"><span data-stu-id="84d63-186">Replace &lt;accountName&gt; and &lt;accountKey&gt; with name and key of your Azure storage account before saving the file.</span></span>

    ```json
    {
        "name": "AzureStorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "DefaultEndpointsProtocol=https;AccountName=<accountName>;AccountKey=<accountKey>"
                }
            }
        }
    }
    ```

2. <span data-ttu-id="84d63-187">To create the linked service: **AzureStorageLinkedService**, run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="84d63-187">To create the linked service: **AzureStorageLinkedService**, run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet.</span></span>

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureStorageLinkedService" -File ".\AzureStorageLinkedService.json"
    ```

    <span data-ttu-id="84d63-188">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="84d63-188">Here is the sample output:</span></span>

    ```json
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureStorageLinkedService
    ```

## <a name="create-datasets"></a><span data-ttu-id="84d63-189">Create datasets</span><span class="sxs-lookup"><span data-stu-id="84d63-189">Create datasets</span></span>

<span data-ttu-id="84d63-190">In this tutorial, you create source and sink datasets, which specify the location where the data is stored:</span><span class="sxs-lookup"><span data-stu-id="84d63-190">In this tutorial, you create source and sink datasets, which specify the location where the data is stored:</span></span>

### <a name="create-a-dataset-for-source-sql-database"></a><span data-ttu-id="84d63-191">Create a dataset for source SQL Database</span><span class="sxs-lookup"><span data-stu-id="84d63-191">Create a dataset for source SQL Database</span></span>

1. <span data-ttu-id="84d63-192">Create a JSON file named **AzureSqlDatabaseDataset.json** in the **C:\ADFv2TutorialBulkCopy** folder, with the following content.</span><span class="sxs-lookup"><span data-stu-id="84d63-192">Create a JSON file named **AzureSqlDatabaseDataset.json** in the **C:\ADFv2TutorialBulkCopy** folder, with the following content.</span></span> <span data-ttu-id="84d63-193">The "tableName" is a dummy one as later you use the SQL query in copy activity to retrieve data.</span><span class="sxs-lookup"><span data-stu-id="84d63-193">The "tableName" is a dummy one as later you use the SQL query in copy activity to retrieve data.</span></span>

    ```json
    {
        "name": "AzureSqlDatabaseDataset",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": {
                "referenceName": "AzureSqlDatabaseLinkedService",
                "type": "LinkedServiceReference"
            },
            "typeProperties": {
                "tableName": "dummy"
            }
        }
    }
    ```

2. <span data-ttu-id="84d63-194">To create the dataset: **AzureSqlDatabaseDataset**, run the **Set-AzureRmDataFactoryV2Dataset** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="84d63-194">To create the dataset: **AzureSqlDatabaseDataset**, run the **Set-AzureRmDataFactoryV2Dataset** cmdlet.</span></span>

    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureSqlDatabaseDataset" -File ".\AzureSqlDatabaseDataset.json"
    ```

    <span data-ttu-id="84d63-195">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="84d63-195">Here is the sample output:</span></span>

    ```json
    DatasetName       : AzureSqlDatabaseDataset
    ResourceGroupName : <resourceGroupname>
    DataFactoryName   : <dataFactoryName>
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlTableDataset
    ```

### <a name="create-a-dataset-for-sink-sql-data-warehouse"></a><span data-ttu-id="84d63-196">Create a dataset for sink SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="84d63-196">Create a dataset for sink SQL Data Warehouse</span></span>

1. <span data-ttu-id="84d63-197">Create a JSON file named **AzureSqlDWDataset.json** in the **C:\ADFv2TutorialBulkCopy** folder, with the following content: The "tableName" is set as a parameter, later the copy activity that references this dataset passes the actual value into the dataset.</span><span class="sxs-lookup"><span data-stu-id="84d63-197">Create a JSON file named **AzureSqlDWDataset.json** in the **C:\ADFv2TutorialBulkCopy** folder, with the following content: The "tableName" is set as a parameter, later the copy activity that references this dataset passes the actual value into the dataset.</span></span>

    ```json
    {
        "name": "AzureSqlDWDataset",
        "properties": {
            "type": "AzureSqlDWTable",
            "linkedServiceName": {
                "referenceName": "AzureSqlDWLinkedService",
                "type": "LinkedServiceReference"
            },
            "typeProperties": {
                "tableName": {
                    "value": "@{dataset().DWTableName}",
                    "type": "Expression"
                }
            },
            "parameters":{
                "DWTableName":{
                    "type":"String"
                }
            }
        }
    }
    ```

2. <span data-ttu-id="84d63-198">To create the dataset: **AzureSqlDWDataset**, run the **Set-AzureRmDataFactoryV2Dataset** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="84d63-198">To create the dataset: **AzureSqlDWDataset**, run the **Set-AzureRmDataFactoryV2Dataset** cmdlet.</span></span>

    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureSqlDWDataset" -File ".\AzureSqlDWDataset.json"
    ```

    <span data-ttu-id="84d63-199">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="84d63-199">Here is the sample output:</span></span>

    ```json
    DatasetName       : AzureSqlDWDataset
    ResourceGroupName : <resourceGroupname>
    DataFactoryName   : <dataFactoryName>
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlDwTableDataset
    ```

## <a name="create-pipelines"></a><span data-ttu-id="84d63-200">Create pipelines</span><span class="sxs-lookup"><span data-stu-id="84d63-200">Create pipelines</span></span>

<span data-ttu-id="84d63-201">In this tutorial, you create two pipelines:</span><span class="sxs-lookup"><span data-stu-id="84d63-201">In this tutorial, you create two pipelines:</span></span>

### <a name="create-the-pipeline-iterateandcopysqltables"></a><span data-ttu-id="84d63-202">Create the pipeline "IterateAndCopySQLTables"</span><span class="sxs-lookup"><span data-stu-id="84d63-202">Create the pipeline "IterateAndCopySQLTables"</span></span>

<span data-ttu-id="84d63-203">This pipeline takes a list of tables as a parameter.</span><span class="sxs-lookup"><span data-stu-id="84d63-203">This pipeline takes a list of tables as a parameter.</span></span> <span data-ttu-id="84d63-204">For each table in the list, it copies data from the table in Azure SQL Database to Azure SQL Data Warehouse using staged copy and PolyBase.</span><span class="sxs-lookup"><span data-stu-id="84d63-204">For each table in the list, it copies data from the table in Azure SQL Database to Azure SQL Data Warehouse using staged copy and PolyBase.</span></span>

1. <span data-ttu-id="84d63-205">Create a JSON file named **IterateAndCopySQLTables.json** in the **C:\ADFv2TutorialBulkCopy** folder, with the following content:</span><span class="sxs-lookup"><span data-stu-id="84d63-205">Create a JSON file named **IterateAndCopySQLTables.json** in the **C:\ADFv2TutorialBulkCopy** folder, with the following content:</span></span>

    ```json
    {
        "name": "IterateAndCopySQLTables",
        "properties": {
            "activities": [
                {
                    "name": "IterateSQLTables",
                    "type": "ForEach",
                    "typeProperties": {
                        "isSequential": "false",
                        "items": {
                            "value": "@pipeline().parameters.tableList",
                            "type": "Expression"
                        },
                        "activities": [
                            {
                                "name": "CopyData",
                                "description": "Copy data from SQL database to SQL DW",
                                "type": "Copy",
                                "inputs": [
                                    {
                                        "referenceName": "AzureSqlDatabaseDataset",
                                        "type": "DatasetReference"
                                    }
                                ],
                                "outputs": [
                                    {
                                        "referenceName": "AzureSqlDWDataset",
                                        "type": "DatasetReference",
                                        "parameters": {
                                            "DWTableName": "[@{item().TABLE_SCHEMA}].[@{item().TABLE_NAME}]"
                                        }
                                    }
                                ],
                                "typeProperties": {
                                    "source": {
                                        "type": "SqlSource",
                                        "sqlReaderQuery": "SELECT * FROM [@{item().TABLE_SCHEMA}].[@{item().TABLE_NAME}]"
                                    },
                                    "sink": {
                                        "type": "SqlDWSink",
                                        "preCopyScript": "TRUNCATE TABLE [@{item().TABLE_SCHEMA}].[@{item().TABLE_NAME}]",
                                        "allowPolyBase": true
                                    },
                                    "enableStaging": true,
                                    "stagingSettings": {
                                        "linkedServiceName": {
                                            "referenceName": "AzureStorageLinkedService",
                                            "type": "LinkedServiceReference"
                                        }
                                    }
                                }
                            }
                        ]
                    }
                }
            ],
            "parameters": {
                "tableList": {
                    "type": "Object"
                }
            }
        }
    }
    ```

2. <span data-ttu-id="84d63-206">To create the pipeline: **IterateAndCopySQLTables**, Run the **Set-AzureRmDataFactoryV2Pipeline** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="84d63-206">To create the pipeline: **IterateAndCopySQLTables**, Run the **Set-AzureRmDataFactoryV2Pipeline** cmdlet.</span></span>

    ```powershell
    Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "IterateAndCopySQLTables" -File ".\IterateAndCopySQLTables.json"
    ```

    <span data-ttu-id="84d63-207">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="84d63-207">Here is the sample output:</span></span>

    ```json
    PipelineName      : IterateAndCopySQLTables
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    Activities        : {IterateSQLTables}
    Parameters        : {[tableList, Microsoft.Azure.Management.DataFactory.Models.ParameterSpecification]}
    ```

### <a name="create-the-pipeline-gettablelistandtriggercopydata"></a><span data-ttu-id="84d63-208">Create the pipeline "GetTableListAndTriggerCopyData"</span><span class="sxs-lookup"><span data-stu-id="84d63-208">Create the pipeline "GetTableListAndTriggerCopyData"</span></span>

<span data-ttu-id="84d63-209">This pipeline performs two steps:</span><span class="sxs-lookup"><span data-stu-id="84d63-209">This pipeline performs two steps:</span></span>

* <span data-ttu-id="84d63-210">Looks up the Azure SQL Database system table to get the list of tables to be copied.</span><span class="sxs-lookup"><span data-stu-id="84d63-210">Looks up the Azure SQL Database system table to get the list of tables to be copied.</span></span>
* <span data-ttu-id="84d63-211">Triggers the pipeline "IterateAndCopySQLTables" to do the actual data copy.</span><span class="sxs-lookup"><span data-stu-id="84d63-211">Triggers the pipeline "IterateAndCopySQLTables" to do the actual data copy.</span></span>

1. <span data-ttu-id="84d63-212">Create a JSON file named **GetTableListAndTriggerCopyData.json** in the **C:\ADFv2TutorialBulkCopy** folder, with the following content:</span><span class="sxs-lookup"><span data-stu-id="84d63-212">Create a JSON file named **GetTableListAndTriggerCopyData.json** in the **C:\ADFv2TutorialBulkCopy** folder, with the following content:</span></span>

    ```json
    {
        "name":"GetTableListAndTriggerCopyData",
        "properties":{
            "activities":[
                { 
                    "name": "LookupTableList",
                    "description": "Retrieve the table list from Azure SQL dataabse",
                    "type": "Lookup",
                    "typeProperties": {
                        "source": {
                            "type": "SqlSource",
                            "sqlReaderQuery": "SELECT TABLE_SCHEMA, TABLE_NAME FROM information_schema.TABLES WHERE TABLE_TYPE = 'BASE TABLE' and TABLE_SCHEMA = 'SalesLT' and TABLE_NAME <> 'ProductModel'"
                        },
                        "dataset": {
                            "referenceName": "AzureSqlDatabaseDataset",
                            "type": "DatasetReference"
                        },
                        "firstRowOnly": false
                    }
                },
                {
                    "name": "TriggerCopy",
                    "type": "ExecutePipeline",
                    "typeProperties": {
                        "parameters": {
                            "tableList": {
                                "value": "@activity('LookupTableList').output.value",
                                "type": "Expression"
                            }
                        },
                        "pipeline": {
                            "referenceName": "IterateAndCopySQLTables",
                            "type": "PipelineReference"
                        },
                        "waitOnCompletion": true
                    },
                    "dependsOn": [
                        {
                            "activity": "LookupTableList",
                            "dependencyConditions": [
                                "Succeeded"
                            ]
                        }
                    ]
                }
            ]
        }
    }
    ```

2. <span data-ttu-id="84d63-213">To create the pipeline: **GetTableListAndTriggerCopyData**, Run the **Set-AzureRmDataFactoryV2Pipeline** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="84d63-213">To create the pipeline: **GetTableListAndTriggerCopyData**, Run the **Set-AzureRmDataFactoryV2Pipeline** cmdlet.</span></span>

    ```powershell
    Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "GetTableListAndTriggerCopyData" -File ".\GetTableListAndTriggerCopyData.json"
    ```

    <span data-ttu-id="84d63-214">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="84d63-214">Here is the sample output:</span></span>

    ```json
    PipelineName      : GetTableListAndTriggerCopyData
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    Activities        : {LookupTableList, TriggerCopy}
    Parameters        :
    ```

## <a name="start-and-monitor-pipeline-run"></a><span data-ttu-id="84d63-215">Start and monitor pipeline run</span><span class="sxs-lookup"><span data-stu-id="84d63-215">Start and monitor pipeline run</span></span>

1. <span data-ttu-id="84d63-216">Start a pipeline run for the main "GetTableListAndTriggerCopyData" pipeline and capture the pipeline run ID for future monitoring.</span><span class="sxs-lookup"><span data-stu-id="84d63-216">Start a pipeline run for the main "GetTableListAndTriggerCopyData" pipeline and capture the pipeline run ID for future monitoring.</span></span> <span data-ttu-id="84d63-217">Underneath, it triggers the run for pipeline "IterateAndCopySQLTables" as specified in ExecutePipeline activity.</span><span class="sxs-lookup"><span data-stu-id="84d63-217">Underneath, it triggers the run for pipeline "IterateAndCopySQLTables" as specified in ExecutePipeline activity.</span></span>

    ```powershell
    $runId = Invoke-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineName 'GetTableListAndTriggerCopyData'
    ```

2.  <span data-ttu-id="84d63-218">Run the following script to continuously check the run status of pipeline **GetTableListAndTriggerCopyData**, and print out the final pipeline run and activity run result.</span><span class="sxs-lookup"><span data-stu-id="84d63-218">Run the following script to continuously check the run status of pipeline **GetTableListAndTriggerCopyData**, and print out the final pipeline run and activity run result.</span></span>

    ```powershell
    while ($True) {
        $run = Get-AzureRmDataFactoryV2PipelineRun -ResourceGroupName $resourceGroupName -DataFactoryName $DataFactoryName -PipelineRunId $runId

        if ($run) {
            if ($run.Status -ne 'InProgress') {
                Write-Host "Pipeline run finished. The status is: " $run.Status -foregroundcolor "Yellow"
                Write-Host "Pipeline run details:" -foregroundcolor "Yellow"
                $run
                break
            }
            Write-Host  "Pipeline is running...status: InProgress" -foregroundcolor "Yellow"
        }

        Start-Sleep -Seconds 15
    }

    $result = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $runId -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)
    Write-Host "Activity run details:" -foregroundcolor "Yellow"
    $result
    ```

    <span data-ttu-id="84d63-219">Here is the output of the sample run:</span><span class="sxs-lookup"><span data-stu-id="84d63-219">Here is the output of the sample run:</span></span>

    ```json
    Pipeline run details:
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    RunId             : 0000000000-00000-0000-0000-000000000000
    PipelineName      : GetTableListAndTriggerCopyData
    LastUpdated       : 9/18/2017 4:08:15 PM
    Parameters        : {}
    RunStart          : 9/18/2017 4:06:44 PM
    RunEnd            : 9/18/2017 4:08:15 PM
    DurationInMs      : 90637
    Status            : Succeeded
    Message           : 

    Activity run details:
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    ActivityName      : LookupTableList
    PipelineRunId     : 0000000000-00000-0000-0000-000000000000
    PipelineName      : GetTableListAndTriggerCopyData
    Input             : {source, dataset, firstRowOnly}
    Output            : {count, value, effectiveIntegrationRuntime}
    LinkedServiceName : 
    ActivityRunStart  : 9/18/2017 4:06:46 PM
    ActivityRunEnd    : 9/18/2017 4:07:09 PM
    DurationInMs      : 22995
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}

    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    ActivityName      : TriggerCopy
    PipelineRunId     : 0000000000-00000-0000-0000-000000000000
    PipelineName      : GetTableListAndTriggerCopyData
    Input             : {pipeline, parameters, waitOnCompletion}
    Output            : {pipelineRunId}
    LinkedServiceName : 
    ActivityRunStart  : 9/18/2017 4:07:11 PM
    ActivityRunEnd    : 9/18/2017 4:08:14 PM
    DurationInMs      : 62581
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    ```

3. <span data-ttu-id="84d63-220">You can get the run ID of pipeline "**IterateAndCopySQLTables**", and check the detailed activity run result as the following.</span><span class="sxs-lookup"><span data-stu-id="84d63-220">You can get the run ID of pipeline "**IterateAndCopySQLTables**", and check the detailed activity run result as the following.</span></span>

    ```powershell
    Write-Host "Pipeline 'IterateAndCopySQLTables' run result:" -foregroundcolor "Yellow"
    ($result | Where-Object {$_.ActivityName -eq "TriggerCopy"}).Output.ToString()
    ```

    <span data-ttu-id="84d63-221">Here is the output of the sample run:</span><span class="sxs-lookup"><span data-stu-id="84d63-221">Here is the output of the sample run:</span></span>

    ```json
    {
        "pipelineRunId": "7514d165-14bf-41fb-b5fb-789bea6c9e58"
    }
    ```

    ```powershell
    $result2 = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId <copy above run ID> -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)
    $result2
    ```

3. <span data-ttu-id="84d63-222">Connect to your sink Azure SQL Data Warehouse and confirm that data has been copied from Azure SQL Database properly.</span><span class="sxs-lookup"><span data-stu-id="84d63-222">Connect to your sink Azure SQL Data Warehouse and confirm that data has been copied from Azure SQL Database properly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84d63-223">Next steps</span><span class="sxs-lookup"><span data-stu-id="84d63-223">Next steps</span></span>
<span data-ttu-id="84d63-224">You performed the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="84d63-224">You performed the following steps in this tutorial:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="84d63-225">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="84d63-225">Create a data factory.</span></span>
> * <span data-ttu-id="84d63-226">Create Azure SQL Database, Azure SQL Data Warehouse, and Azure Storage linked services.</span><span class="sxs-lookup"><span data-stu-id="84d63-226">Create Azure SQL Database, Azure SQL Data Warehouse, and Azure Storage linked services.</span></span>
> * <span data-ttu-id="84d63-227">Create Azure SQL Database and Azure SQL Data Warehouse datasets.</span><span class="sxs-lookup"><span data-stu-id="84d63-227">Create Azure SQL Database and Azure SQL Data Warehouse datasets.</span></span>
> * <span data-ttu-id="84d63-228">Create a  pipeline to look up the tables to be copied and another pipeline to perform the actual copy operation.</span><span class="sxs-lookup"><span data-stu-id="84d63-228">Create a  pipeline to look up the tables to be copied and another pipeline to perform the actual copy operation.</span></span> 
> * <span data-ttu-id="84d63-229">Start a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="84d63-229">Start a pipeline run.</span></span>
> * <span data-ttu-id="84d63-230">Monitor the pipeline and activity runs.</span><span class="sxs-lookup"><span data-stu-id="84d63-230">Monitor the pipeline and activity runs.</span></span>

<span data-ttu-id="84d63-231">Advance to the following tutorial to learn about copy data incrementally from a source to a destination:</span><span class="sxs-lookup"><span data-stu-id="84d63-231">Advance to the following tutorial to learn about copy data incrementally from a source to a destination:</span></span>
> [!div class="nextstepaction"]
>[<span data-ttu-id="84d63-232">Copy data incrementally</span><span class="sxs-lookup"><span data-stu-id="84d63-232">Copy data incrementally</span></span>](tutorial-incremental-copy-powershell.md)
