---
title: Incrementally copy data using Change Tracking and Azure Data Factory | Microsoft Docs
description: 'In this tutorial, you create an Azure Data Factory pipeline that copies delta data incrementally from multiple tables in an on-premises SQL Server database to an Azure SQL database. '
services: data-factory
documentationcenter: ''
author: dearandyxu
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/22/2018
ms.author: yexu
ms.openlocfilehash: 246b423e69fa8fb73db45f44fa17c1bc65407681
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870836"
---
# <a name="incrementally-load-data-from-azure-sql-database-to-azure-blob-storage-using-change-tracking-information"></a><span data-ttu-id="a5f7c-103">Incrementally load data from Azure SQL Database to Azure Blob Storage using change tracking information</span><span class="sxs-lookup"><span data-stu-id="a5f7c-103">Incrementally load data from Azure SQL Database to Azure Blob Storage using change tracking information</span></span> 
<span data-ttu-id="a5f7c-104">In this tutorial, you create an Azure data factory with a pipeline that loads delta data based on **change tracking** information in the source Azure SQL database to an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-104">In this tutorial, you create an Azure data factory with a pipeline that loads delta data based on **change tracking** information in the source Azure SQL database to an Azure blob storage.</span></span>  

<span data-ttu-id="a5f7c-105">You perform the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-105">You perform the following steps in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a5f7c-106">Prepare the source data store</span><span class="sxs-lookup"><span data-stu-id="a5f7c-106">Prepare the source data store</span></span>
> * <span data-ttu-id="a5f7c-107">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-107">Create a data factory.</span></span>
> * <span data-ttu-id="a5f7c-108">Create linked services.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-108">Create linked services.</span></span> 
> * <span data-ttu-id="a5f7c-109">Create source, sink, and change tracking datasets.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-109">Create source, sink, and change tracking datasets.</span></span>
> * <span data-ttu-id="a5f7c-110">Create, run, and monitor the full copy pipeline</span><span class="sxs-lookup"><span data-stu-id="a5f7c-110">Create, run, and monitor the full copy pipeline</span></span>
> * <span data-ttu-id="a5f7c-111">Add or update data in the source table</span><span class="sxs-lookup"><span data-stu-id="a5f7c-111">Add or update data in the source table</span></span>
> * <span data-ttu-id="a5f7c-112">Create, run, and monitor the incremental copy pipeline</span><span class="sxs-lookup"><span data-stu-id="a5f7c-112">Create, run, and monitor the incremental copy pipeline</span></span>

## <a name="overview"></a><span data-ttu-id="a5f7c-113">Overview</span><span class="sxs-lookup"><span data-stu-id="a5f7c-113">Overview</span></span>
<span data-ttu-id="a5f7c-114">In a data integration solution, incrementally loading data after initial data loads is a widely used scenario.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-114">In a data integration solution, incrementally loading data after initial data loads is a widely used scenario.</span></span> <span data-ttu-id="a5f7c-115">In some cases, the changed data within a period in your source data store can be easily to sliced up (for example, LastModifyTime, CreationTime).</span><span class="sxs-lookup"><span data-stu-id="a5f7c-115">In some cases, the changed data within a period in your source data store can be easily to sliced up (for example, LastModifyTime, CreationTime).</span></span> <span data-ttu-id="a5f7c-116">In some cases, there is no explicit way to identify the delta data from last time you processed the data.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-116">In some cases, there is no explicit way to identify the delta data from last time you processed the data.</span></span> <span data-ttu-id="a5f7c-117">The Change Tracking technology supported by data stores such as Azure SQL Database and SQL Server can be used to identify the delta data.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-117">The Change Tracking technology supported by data stores such as Azure SQL Database and SQL Server can be used to identify the delta data.</span></span>  <span data-ttu-id="a5f7c-118">This tutorial describes how to use Azure Data Factory with SQL Change Tracking technology to incrementally load delta data from Azure SQL Database into Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-118">This tutorial describes how to use Azure Data Factory with SQL Change Tracking technology to incrementally load delta data from Azure SQL Database into Azure Blob Storage.</span></span>  <span data-ttu-id="a5f7c-119">For more concrete information about SQL Change Tracking technology, see [Change tracking in SQL Server](/sql/relational-databases/track-changes/about-change-tracking-sql-server).</span><span class="sxs-lookup"><span data-stu-id="a5f7c-119">For more concrete information about SQL Change Tracking technology, see [Change tracking in SQL Server](/sql/relational-databases/track-changes/about-change-tracking-sql-server).</span></span> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="a5f7c-120">End-to-end workflow</span><span class="sxs-lookup"><span data-stu-id="a5f7c-120">End-to-end workflow</span></span>
<span data-ttu-id="a5f7c-121">Here are the typical end-to-end workflow steps to incrementally load data using the Change Tracking technology.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-121">Here are the typical end-to-end workflow steps to incrementally load data using the Change Tracking technology.</span></span>

> [!NOTE]
> <span data-ttu-id="a5f7c-122">Both Azure SQL Database and SQL Server support the Change Tracking technology.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-122">Both Azure SQL Database and SQL Server support the Change Tracking technology.</span></span> <span data-ttu-id="a5f7c-123">This tutorial uses Azure SQL Database as the source data store.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-123">This tutorial uses Azure SQL Database as the source data store.</span></span> <span data-ttu-id="a5f7c-124">You can also use an on-premises SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-124">You can also use an on-premises SQL Server.</span></span> 

1. <span data-ttu-id="a5f7c-125">**Initial loading of historical data** (run once):</span><span class="sxs-lookup"><span data-stu-id="a5f7c-125">**Initial loading of historical data** (run once):</span></span>
    1. <span data-ttu-id="a5f7c-126">Enable Change Tracking technology in the source Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-126">Enable Change Tracking technology in the source Azure SQL database.</span></span>
    2. <span data-ttu-id="a5f7c-127">Get the initial value of SYS_CHANGE_VERSION in the Azure SQL database as the baseline to capture changed data.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-127">Get the initial value of SYS_CHANGE_VERSION in the Azure SQL database as the baseline to capture changed data.</span></span>
    3. <span data-ttu-id="a5f7c-128">Load full data from the Azure SQL database into an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-128">Load full data from the Azure SQL database into an Azure blob storage.</span></span> 
2. <span data-ttu-id="a5f7c-129">**Incremental loading of delta data on a schedule** (run periodically after the initial loading of data):</span><span class="sxs-lookup"><span data-stu-id="a5f7c-129">**Incremental loading of delta data on a schedule** (run periodically after the initial loading of data):</span></span>
    1. <span data-ttu-id="a5f7c-130">Get the old and new SYS_CHANGE_VERSION values.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-130">Get the old and new SYS_CHANGE_VERSION values.</span></span>
    3. <span data-ttu-id="a5f7c-131">Load the delta data by joining the primary keys of changed rows (between two SYS_CHANGE_VERSION values) from **sys.change_tracking_tables** with data in the **source table**, and then move the delta data to destination.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-131">Load the delta data by joining the primary keys of changed rows (between two SYS_CHANGE_VERSION values) from **sys.change_tracking_tables** with data in the **source table**, and then move the delta data to destination.</span></span>
    4. <span data-ttu-id="a5f7c-132">Update the SYS_CHANGE_VERSION for the delta loading next time.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-132">Update the SYS_CHANGE_VERSION for the delta loading next time.</span></span>

## <a name="high-level-solution"></a><span data-ttu-id="a5f7c-133">High-level solution</span><span class="sxs-lookup"><span data-stu-id="a5f7c-133">High-level solution</span></span>
<span data-ttu-id="a5f7c-134">In this tutorial, you create two pipelines that perform the following two operations:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-134">In this tutorial, you create two pipelines that perform the following two operations:</span></span>  

1. <span data-ttu-id="a5f7c-135">**Initial load:** you create a pipeline with a copy activity that copies the entire data from the source data store (Azure SQL Database) to the destination data store (Azure Blob Storage).</span><span class="sxs-lookup"><span data-stu-id="a5f7c-135">**Initial load:** you create a pipeline with a copy activity that copies the entire data from the source data store (Azure SQL Database) to the destination data store (Azure Blob Storage).</span></span>

    ![Full loading of data](media/tutorial-incremental-copy-change-tracking-feature-powershell/full-load-flow-diagram.png)
1.  <span data-ttu-id="a5f7c-137">**Incremental load:** you create a pipeline with the following activities, and run it periodically.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-137">**Incremental load:** you create a pipeline with the following activities, and run it periodically.</span></span> 
    1. <span data-ttu-id="a5f7c-138">Create **two lookup activities** to get the old and new SYS_CHANGE_VERSION from Azure SQL Database and pass it to copy activity.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-138">Create **two lookup activities** to get the old and new SYS_CHANGE_VERSION from Azure SQL Database and pass it to copy activity.</span></span>
    2. <span data-ttu-id="a5f7c-139">Create **one copy activity** to copy the inserted/updated/deleted data between the two SYS_CHANGE_VERSION values from Azure SQL Database to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-139">Create **one copy activity** to copy the inserted/updated/deleted data between the two SYS_CHANGE_VERSION values from Azure SQL Database to Azure Blob Storage.</span></span>
    3. <span data-ttu-id="a5f7c-140">Create **one stored procedure activity** to update the value of SYS_CHANGE_VERSION for the next pipeline run.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-140">Create **one stored procedure activity** to update the value of SYS_CHANGE_VERSION for the next pipeline run.</span></span>

    ![Increment load flow diagram](media/tutorial-incremental-copy-change-tracking-feature-powershell/incremental-load-flow-diagram.png)


<span data-ttu-id="a5f7c-142">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-142">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5f7c-143">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a5f7c-143">Prerequisites</span></span>
* <span data-ttu-id="a5f7c-144">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-144">Azure PowerShell.</span></span> <span data-ttu-id="a5f7c-145">Install the latest Azure PowerShell modules by following instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="a5f7c-145">Install the latest Azure PowerShell modules by following instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>
* <span data-ttu-id="a5f7c-146">**Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-146">**Azure SQL Database**.</span></span> <span data-ttu-id="a5f7c-147">You use the database as the **source** data store.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-147">You use the database as the **source** data store.</span></span> <span data-ttu-id="a5f7c-148">If you don't have an Azure SQL Database, see the [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) article for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-148">If you don't have an Azure SQL Database, see the [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) article for steps to create one.</span></span>
* <span data-ttu-id="a5f7c-149">**Azure Storage account**.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-149">**Azure Storage account**.</span></span> <span data-ttu-id="a5f7c-150">You use the blob storage as the **sink** data store.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-150">You use the blob storage as the **sink** data store.</span></span> <span data-ttu-id="a5f7c-151">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-151">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span></span> <span data-ttu-id="a5f7c-152">Create a container named **adftutorial**.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-152">Create a container named **adftutorial**.</span></span> 

### <a name="create-a-data-source-table-in-your-azure-sql-database"></a><span data-ttu-id="a5f7c-153">Create a data source table in your Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="a5f7c-153">Create a data source table in your Azure SQL database</span></span>
1. <span data-ttu-id="a5f7c-154">Launch **SQL Server Management Studio**, and connect to your Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-154">Launch **SQL Server Management Studio**, and connect to your Azure SQL server.</span></span> 
2. <span data-ttu-id="a5f7c-155">In **Server Explorer**, right-click your **database** and choose the **New Query**.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-155">In **Server Explorer**, right-click your **database** and choose the **New Query**.</span></span>
3. <span data-ttu-id="a5f7c-156">Run the following SQL command against your Azure SQL database to create a table named `data_source_table` as data source store.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-156">Run the following SQL command against your Azure SQL database to create a table named `data_source_table` as data source store.</span></span>  
    
    ```sql
    create table data_source_table
    (
        PersonID int NOT NULL,
        Name varchar(255),
        Age int
        PRIMARY KEY (PersonID)
    );

    INSERT INTO data_source_table
        (PersonID, Name, Age)
    VALUES
        (1, 'aaaa', 21),
        (2, 'bbbb', 24),
        (3, 'cccc', 20),
        (4, 'dddd', 26),
        (5, 'eeee', 22);

    ```
4. <span data-ttu-id="a5f7c-157">Enable **Change Tracking** mechanism on your database and the source table (data_source_table) by running the following SQL query:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-157">Enable **Change Tracking** mechanism on your database and the source table (data_source_table) by running the following SQL query:</span></span> 

    > [!NOTE]
    > - <span data-ttu-id="a5f7c-158">Replace &lt;your database name&gt; with the name of your Azure SQL database that has the data_source_table.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-158">Replace &lt;your database name&gt; with the name of your Azure SQL database that has the data_source_table.</span></span> 
    > - <span data-ttu-id="a5f7c-159">The changed data is kept for two days in the current example.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-159">The changed data is kept for two days in the current example.</span></span> <span data-ttu-id="a5f7c-160">If you load the changed data for every three days or more, some changed data is not included.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-160">If you load the changed data for every three days or more, some changed data is not included.</span></span>  <span data-ttu-id="a5f7c-161">You need to either change the value of CHANGE_RETENTION to a bigger number.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-161">You need to either change the value of CHANGE_RETENTION to a bigger number.</span></span> <span data-ttu-id="a5f7c-162">Alternatively, ensure that your period to load the changed data is within two days.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-162">Alternatively, ensure that your period to load the changed data is within two days.</span></span> <span data-ttu-id="a5f7c-163">For more information, see [Enable change tracking for a database](/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server#enable-change-tracking-for-a-database)</span><span class="sxs-lookup"><span data-stu-id="a5f7c-163">For more information, see [Enable change tracking for a database](/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server#enable-change-tracking-for-a-database)</span></span>
 
    ```sql
    ALTER DATABASE <your database name>
    SET CHANGE_TRACKING = ON  
    (CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON)  
  
    ALTER TABLE data_source_table
    ENABLE CHANGE_TRACKING  
    WITH (TRACK_COLUMNS_UPDATED = ON)
    ```
5. <span data-ttu-id="a5f7c-164">Create a new table and store the ChangeTracking_version with a default value by running the following query:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-164">Create a new table and store the ChangeTracking_version with a default value by running the following query:</span></span> 

    ```sql
    create table table_store_ChangeTracking_version
    (
        TableName varchar(255),
        SYS_CHANGE_VERSION BIGINT,
    );

    DECLARE @ChangeTracking_version BIGINT
    SET @ChangeTracking_version = CHANGE_TRACKING_CURRENT_VERSION();  

    INSERT INTO table_store_ChangeTracking_version
    VALUES ('data_source_table', @ChangeTracking_version)
    ```
    
    > [!NOTE]
    > <span data-ttu-id="a5f7c-165">If the data is not changed after you enabled the change tracking for SQL Database, the value of the change tracking version is 0.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-165">If the data is not changed after you enabled the change tracking for SQL Database, the value of the change tracking version is 0.</span></span>
6. <span data-ttu-id="a5f7c-166">Run the following query to create a stored procedure in your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-166">Run the following query to create a stored procedure in your Azure SQL database.</span></span> <span data-ttu-id="a5f7c-167">The pipeline invokes this stored procedure to update the change tracking version in the table you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-167">The pipeline invokes this stored procedure to update the change tracking version in the table you created in the previous step.</span></span> 

    ```sql
    CREATE PROCEDURE Update_ChangeTracking_Version @CurrentTrackingVersion BIGINT, @TableName varchar(50)
    AS
    
    BEGIN
    
        UPDATE table_store_ChangeTracking_version
        SET [SYS_CHANGE_VERSION] = @CurrentTrackingVersion
    WHERE [TableName] = @TableName
    
    END    
    ```

### <a name="azure-powershell"></a><span data-ttu-id="a5f7c-168">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5f7c-168">Azure PowerShell</span></span>
<span data-ttu-id="a5f7c-169">Install the latest Azure PowerShell modules by following  instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="a5f7c-169">Install the latest Azure PowerShell modules by following  instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="a5f7c-170">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="a5f7c-170">Create a data factory</span></span>
1. <span data-ttu-id="a5f7c-171">Define a variable for the resource group name that you use in PowerShell commands later.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-171">Define a variable for the resource group name that you use in PowerShell commands later.</span></span> <span data-ttu-id="a5f7c-172">Copy the following command text to PowerShell, specify a name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) in double quotes, and then run the command.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-172">Copy the following command text to PowerShell, specify a name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) in double quotes, and then run the command.</span></span> <span data-ttu-id="a5f7c-173">For example: `"adfrg"`.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-173">For example: `"adfrg"`.</span></span> 
   
     ```powershell
    $resourceGroupName = "ADFTutorialResourceGroup";
    ```

    <span data-ttu-id="a5f7c-174">If the resource group already exists, you may not want to overwrite it.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-174">If the resource group already exists, you may not want to overwrite it.</span></span> <span data-ttu-id="a5f7c-175">Assign a different value to the `$resourceGroupName` variable and run the command again</span><span class="sxs-lookup"><span data-stu-id="a5f7c-175">Assign a different value to the `$resourceGroupName` variable and run the command again</span></span>
2. <span data-ttu-id="a5f7c-176">Define a variable for the location of the data factory:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-176">Define a variable for the location of the data factory:</span></span> 

    ```powershell
    $location = "East US"
    ```
3. <span data-ttu-id="a5f7c-177">To create the Azure resource group, run the following command:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-177">To create the Azure resource group, run the following command:</span></span> 

    ```powershell
    New-AzureRmResourceGroup $resourceGroupName $location
    ``` 
    <span data-ttu-id="a5f7c-178">If the resource group already exists, you may not want to overwrite it.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-178">If the resource group already exists, you may not want to overwrite it.</span></span> <span data-ttu-id="a5f7c-179">Assign a different value to the `$resourceGroupName` variable and run the command again.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-179">Assign a different value to the `$resourceGroupName` variable and run the command again.</span></span> 
3. <span data-ttu-id="a5f7c-180">Define a variable for the data factory name.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-180">Define a variable for the data factory name.</span></span> 

    > [!IMPORTANT]
    >  <span data-ttu-id="a5f7c-181">Update the data factory name to be globally unique.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-181">Update the data factory name to be globally unique.</span></span>  

    ```powershell
    $dataFactoryName = "IncCopyChgTrackingDF";
    ```
5. <span data-ttu-id="a5f7c-182">To create the data factory, run the following **Set-AzureRmDataFactoryV2** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-182">To create the data factory, run the following **Set-AzureRmDataFactoryV2** cmdlet:</span></span> 
    
    ```powershell       
    Set-AzureRmDataFactoryV2 -ResourceGroupName $resourceGroupName -Location $location -Name $dataFactoryName 
    ```

<span data-ttu-id="a5f7c-183">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-183">Note the following points:</span></span>

* <span data-ttu-id="a5f7c-184">The name of the Azure data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-184">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="a5f7c-185">If you receive the following error, change the name and try again.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-185">If you receive the following error, change the name and try again.</span></span>

    ```
    The specified Data Factory name 'ADFIncCopyChangeTrackingTestFactory' is already in use. Data Factory names must be globally unique.
    ```
* <span data-ttu-id="a5f7c-186">To create Data Factory instances, the user account you use to log in to Azure must be a member of **contributor** or **owner** roles, or an **administrator** of the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-186">To create Data Factory instances, the user account you use to log in to Azure must be a member of **contributor** or **owner** roles, or an **administrator** of the Azure subscription.</span></span>
* <span data-ttu-id="a5f7c-187">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="a5f7c-187">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span></span> <span data-ttu-id="a5f7c-188">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-188">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span></span>


## <a name="create-linked-services"></a><span data-ttu-id="a5f7c-189">Create linked services</span><span class="sxs-lookup"><span data-stu-id="a5f7c-189">Create linked services</span></span>
<span data-ttu-id="a5f7c-190">You create linked services in a data factory to link your data stores and compute services to the data factory.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-190">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="a5f7c-191">In this section, you create linked services to your Azure Storage account and Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-191">In this section, you create linked services to your Azure Storage account and Azure SQL database.</span></span> 

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="a5f7c-192">Create Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-192">Create Azure Storage linked service.</span></span>
<span data-ttu-id="a5f7c-193">In this step, you link your Azure Storage Account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-193">In this step, you link your Azure Storage Account to the data factory.</span></span>

1. <span data-ttu-id="a5f7c-194">Create a JSON file named **AzureStorageLinkedService.json** in **C:\ADFTutorials\IncCopyChangeTrackingTutorial** folder with the following content: (Create the folder if it does not already exist.).</span><span class="sxs-lookup"><span data-stu-id="a5f7c-194">Create a JSON file named **AzureStorageLinkedService.json** in **C:\ADFTutorials\IncCopyChangeTrackingTutorial** folder with the following content: (Create the folder if it does not already exist.).</span></span> <span data-ttu-id="a5f7c-195">Replace `<accountName>`,  `<accountKey>` with name and key of your Azure storage account before saving the file.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-195">Replace `<accountName>`,  `<accountKey>` with name and key of your Azure storage account before saving the file.</span></span>

    ```json
    {
        "name": "AzureStorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": {
                    "value": "DefaultEndpointsProtocol=https;AccountName=<accountName>;AccountKey=<accountKey>",
                    "type": "SecureString"
                }
            }
        }
    }
    ```
2. <span data-ttu-id="a5f7c-196">In **Azure PowerShell**, switch to the **C:\ADFTutorials\IncCopyChgTrackingTutorial** folder.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-196">In **Azure PowerShell**, switch to the **C:\ADFTutorials\IncCopyChgTrackingTutorial** folder.</span></span>
3. <span data-ttu-id="a5f7c-197">Run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet to create the linked service: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-197">Run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet to create the linked service: **AzureStorageLinkedService**.</span></span> <span data-ttu-id="a5f7c-198">In the following example, you pass values for the **ResourceGroupName** and **DataFactoryName** parameters.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-198">In the following example, you pass values for the **ResourceGroupName** and **DataFactoryName** parameters.</span></span> 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureStorageLinkedService" -File ".\AzureStorageLinkedService.json"
    ```

    <span data-ttu-id="a5f7c-199">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-199">Here is the sample output:</span></span>

    ```json
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : IncCopyChgTrackingDF
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureStorageLinkedService
    ```

### <a name="create-azure-sql-database-linked-service"></a><span data-ttu-id="a5f7c-200">Create Azure SQL Database linked service.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-200">Create Azure SQL Database linked service.</span></span>
<span data-ttu-id="a5f7c-201">In this step, you link your Azure SQL database to the data factory.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-201">In this step, you link your Azure SQL database to the data factory.</span></span>

1. <span data-ttu-id="a5f7c-202">Create a JSON file named **AzureSQLDatabaseLinkedService.json** in **C:\ADFTutorials\IncCopyChangeTrackingTutorial** folder with the following content: Replace **&lt;server&gt; &lt;database name&gt;, &lt;user id&gt;, and &lt;password&gt;** with name of your Azure SQL server, name of your database, user ID, and password before saving the file.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-202">Create a JSON file named **AzureSQLDatabaseLinkedService.json** in **C:\ADFTutorials\IncCopyChangeTrackingTutorial** folder with the following content: Replace **&lt;server&gt; &lt;database name&gt;, &lt;user id&gt;, and &lt;password&gt;** with name of your Azure SQL server, name of your database, user ID, and password before saving the file.</span></span> 

    ```json
    {
        "name": "AzureSQLDatabaseLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": {
                    "value": "Server = tcp:<server>.database.windows.net,1433;Initial Catalog=<database name>; Persist Security Info=False; User ID=<user name>; Password=<password>; MultipleActiveResultSets = False; Encrypt = True; TrustServerCertificate = False; Connection Timeout = 30;",
                    "type": "SecureString"
                }
            }
        }
    }
    ```
2. <span data-ttu-id="a5f7c-203">In **Azure PowerShell**, run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet to create the linked service: **AzureSQLDatabaseLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-203">In **Azure PowerShell**, run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet to create the linked service: **AzureSQLDatabaseLinkedService**.</span></span> 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureSQLDatabaseLinkedService" -File ".\AzureSQLDatabaseLinkedService.json"
    ```

    <span data-ttu-id="a5f7c-204">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-204">Here is the sample output:</span></span>

    ```json
    LinkedServiceName : AzureSQLDatabaseLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : IncCopyChgTrackingDF
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlDatabaseLinkedService
    ```

## <a name="create-datasets"></a><span data-ttu-id="a5f7c-205">Create datasets</span><span class="sxs-lookup"><span data-stu-id="a5f7c-205">Create datasets</span></span>
<span data-ttu-id="a5f7c-206">In this step, you create datasets to represent data source, data destination.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-206">In this step, you create datasets to represent data source, data destination.</span></span> <span data-ttu-id="a5f7c-207">and the place to store the SYS_CHANGE_VERSION.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-207">and the place to store the SYS_CHANGE_VERSION.</span></span>

### <a name="create-a-source-dataset"></a><span data-ttu-id="a5f7c-208">Create a source dataset</span><span class="sxs-lookup"><span data-stu-id="a5f7c-208">Create a source dataset</span></span>
<span data-ttu-id="a5f7c-209">In this step, you create a dataset to represent the source data.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-209">In this step, you create a dataset to represent the source data.</span></span> 

1. <span data-ttu-id="a5f7c-210">Create a JSON file named SourceDataset.json in the same folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-210">Create a JSON file named SourceDataset.json in the same folder with the following content:</span></span> 

    ```json
    {
        "name": "SourceDataset",
        "properties": {
            "type": "AzureSqlTable",
            "typeProperties": {
                "tableName": "data_source_table"
            },
            "linkedServiceName": {
                "referenceName": "AzureSQLDatabaseLinkedService",
                "type": "LinkedServiceReference"
            }
        }
    }   
    ```

2.  <span data-ttu-id="a5f7c-211">Run the Set-AzureRmDataFactoryV2Dataset cmdlet to create the dataset: SourceDataset</span><span class="sxs-lookup"><span data-stu-id="a5f7c-211">Run the Set-AzureRmDataFactoryV2Dataset cmdlet to create the dataset: SourceDataset</span></span>
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SourceDataset" -File ".\SourceDataset.json"
    ```

    <span data-ttu-id="a5f7c-212">Here is the sample output of the cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-212">Here is the sample output of the cmdlet:</span></span>
    
    ```json
    DatasetName       : SourceDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : IncCopyChgTrackingDF
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlTableDataset
    ```

### <a name="create-a-sink-dataset"></a><span data-ttu-id="a5f7c-213">Create a sink dataset</span><span class="sxs-lookup"><span data-stu-id="a5f7c-213">Create a sink dataset</span></span>
<span data-ttu-id="a5f7c-214">In this step, you create a dataset to represent the data that is copied from the source data store.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-214">In this step, you create a dataset to represent the data that is copied from the source data store.</span></span> 

1. <span data-ttu-id="a5f7c-215">Create a JSON file named SinkDataset.json in the same folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-215">Create a JSON file named SinkDataset.json in the same folder with the following content:</span></span> 

    ```json
    {
        "name": "SinkDataset",
        "properties": {
            "type": "AzureBlob",
            "typeProperties": {
                "folderPath": "adftutorial/incchgtracking",
                "fileName": "@CONCAT('Incremental-', pipeline().RunId, '.txt')",
                "format": {
                    "type": "TextFormat"
                }
            },
            "linkedServiceName": {
                "referenceName": "AzureStorageLinkedService",
                "type": "LinkedServiceReference"
            }
        }
    }
    ```

    <span data-ttu-id="a5f7c-216">You create the adftutorial container in your Azure Blob Storage as part of the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-216">You create the adftutorial container in your Azure Blob Storage as part of the prerequisites.</span></span> <span data-ttu-id="a5f7c-217">Create the container if it does not exist (or) set it to the name of an existing one.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-217">Create the container if it does not exist (or) set it to the name of an existing one.</span></span> <span data-ttu-id="a5f7c-218">In this tutorial, the output file name is dynamically generated by using the expression: @CONCAT('Incremental-', pipeline().RunId, '.txt').</span><span class="sxs-lookup"><span data-stu-id="a5f7c-218">In this tutorial, the output file name is dynamically generated by using the expression: @CONCAT('Incremental-', pipeline().RunId, '.txt').</span></span>
2.  <span data-ttu-id="a5f7c-219">Run the Set-AzureRmDataFactoryV2Dataset cmdlet to create the dataset: SinkDataset</span><span class="sxs-lookup"><span data-stu-id="a5f7c-219">Run the Set-AzureRmDataFactoryV2Dataset cmdlet to create the dataset: SinkDataset</span></span>
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SinkDataset" -File ".\SinkDataset.json"
    ```

    <span data-ttu-id="a5f7c-220">Here is the sample output of the cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-220">Here is the sample output of the cmdlet:</span></span>
    
    ```json
    DatasetName       : SinkDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : IncCopyChgTrackingDF
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureBlobDataset
    ```

### <a name="create-a-change-tracking-dataset"></a><span data-ttu-id="a5f7c-221">Create a change tracking dataset</span><span class="sxs-lookup"><span data-stu-id="a5f7c-221">Create a change tracking dataset</span></span>
<span data-ttu-id="a5f7c-222">In this step, you create a dataset for storing the change tracking version.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-222">In this step, you create a dataset for storing the change tracking version.</span></span>  

1. <span data-ttu-id="a5f7c-223">Create a JSON file named ChangeTrackingDataset.json in the same folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-223">Create a JSON file named ChangeTrackingDataset.json in the same folder with the following content:</span></span> 

    ```json
    {
        "name": " ChangeTrackingDataset",
        "properties": {
            "type": "AzureSqlTable",
            "typeProperties": {
                "tableName": "table_store_ChangeTracking_version"
            },
            "linkedServiceName": {
                "referenceName": "AzureSQLDatabaseLinkedService",
                "type": "LinkedServiceReference"
            }
        }
    }
    ```

    <span data-ttu-id="a5f7c-224">You create the table table_store_ChangeTracking_version as part of the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-224">You create the table table_store_ChangeTracking_version as part of the prerequisites.</span></span>
2.  <span data-ttu-id="a5f7c-225">Run the Set-AzureRmDataFactoryV2Dataset cmdlet to create the dataset: WatermarkDataset</span><span class="sxs-lookup"><span data-stu-id="a5f7c-225">Run the Set-AzureRmDataFactoryV2Dataset cmdlet to create the dataset: WatermarkDataset</span></span>
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "ChangeTrackingDataset" -File ".\ChangeTrackingDataset.json"
    ```

    <span data-ttu-id="a5f7c-226">Here is the sample output of the cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-226">Here is the sample output of the cmdlet:</span></span>
    
    ```json
    DatasetName       : ChangeTrackingDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : IncCopyChgTrackingDF
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlTableDataset
    ```

## <a name="create-a-pipeline-for-the-full-copy"></a><span data-ttu-id="a5f7c-227">Create a pipeline for the full copy</span><span class="sxs-lookup"><span data-stu-id="a5f7c-227">Create a pipeline for the full copy</span></span>
<span data-ttu-id="a5f7c-228">In this step, you create a pipeline with a copy activity that copies the entire data from the source data store (Azure SQL Database) to the destination data store (Azure Blob Storage).</span><span class="sxs-lookup"><span data-stu-id="a5f7c-228">In this step, you create a pipeline with a copy activity that copies the entire data from the source data store (Azure SQL Database) to the destination data store (Azure Blob Storage).</span></span>

1. <span data-ttu-id="a5f7c-229">Create a JSON file: FullCopyPipeline.json in same folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-229">Create a JSON file: FullCopyPipeline.json in same folder with the following content:</span></span> 

    ```json
    {
        "name": "FullCopyPipeline",
        "properties": {
            "activities": [{
                "name": "FullCopyActivity",
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
    
                "inputs": [{
                    "referenceName": "SourceDataset",
                    "type": "DatasetReference"
                }],
                "outputs": [{
                    "referenceName": "SinkDataset",
                    "type": "DatasetReference"
                }]
            }]
        }
    }
    ```
2. <span data-ttu-id="a5f7c-230">Run the Set-AzureRmDataFactoryV2Pipeline cmdlet to create the pipeline: FullCopyPipeline.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-230">Run the Set-AzureRmDataFactoryV2Pipeline cmdlet to create the pipeline: FullCopyPipeline.</span></span>
    
   ```powershell
    Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "FullCopyPipeline" -File ".\FullCopyPipeline.json"
   ``` 

   <span data-ttu-id="a5f7c-231">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-231">Here is the sample output:</span></span> 

   ```json
    PipelineName      : FullCopyPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : IncCopyChgTrackingDF
    Activities        : {FullCopyActivity}
    Parameters        :
   ```
 
### <a name="run-the-full-copy-pipeline"></a><span data-ttu-id="a5f7c-232">Run the full copy pipeline</span><span class="sxs-lookup"><span data-stu-id="a5f7c-232">Run the full copy pipeline</span></span>
<span data-ttu-id="a5f7c-233">Run the pipeline: **FullCopyPipeline** by using **Invoke-AzureRmDataFactoryV2Pipeline** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-233">Run the pipeline: **FullCopyPipeline** by using **Invoke-AzureRmDataFactoryV2Pipeline** cmdlet.</span></span> 

```powershell
Invoke-AzureRmDataFactoryV2Pipeline -PipelineName "FullCopyPipeline" -ResourceGroup $resourceGroupName -dataFactoryName $dataFactoryName        
``` 

### <a name="monitor-the-full-copy-pipeline"></a><span data-ttu-id="a5f7c-234">Monitor the full copy pipeline</span><span class="sxs-lookup"><span data-stu-id="a5f7c-234">Monitor the full copy pipeline</span></span>

1. <span data-ttu-id="a5f7c-235">Log in to [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5f7c-235">Log in to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5f7c-236">Click **All services**, search with the keyword `data factories`, and select **Data factories**.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-236">Click **All services**, search with the keyword `data factories`, and select **Data factories**.</span></span> 

    ![Data factories menu](media\tutorial-incremental-copy-change-tracking-feature-powershell\monitor-data-factories-menu-1.png)
3. <span data-ttu-id="a5f7c-238">Search for **your data factory** in the list of data factories, and select it to launch the Data factory page.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-238">Search for **your data factory** in the list of data factories, and select it to launch the Data factory page.</span></span> 

    ![Search for your data factory](media\tutorial-incremental-copy-change-tracking-feature-powershell\monitor-search-data-factory-2.png)
4. <span data-ttu-id="a5f7c-240">In the Data factory page, click **Monitor & Manage** tile.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-240">In the Data factory page, click **Monitor & Manage** tile.</span></span> 

    ![Monitor & Manage tile](media\tutorial-incremental-copy-change-tracking-feature-powershell\monitor-monitor-manage-tile-3.png)    
5. <span data-ttu-id="a5f7c-242">The **Data Integration Application** launches in a separate tab. You can see all the **pipeline runs** and their statuses.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-242">The **Data Integration Application** launches in a separate tab. You can see all the **pipeline runs** and their statuses.</span></span> <span data-ttu-id="a5f7c-243">Notice that in the following example, the status of the pipeline run is **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-243">Notice that in the following example, the status of the pipeline run is **Succeeded**.</span></span> <span data-ttu-id="a5f7c-244">You can check parameters passed to the pipeline by clicking link in the **Parameters** column.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-244">You can check parameters passed to the pipeline by clicking link in the **Parameters** column.</span></span> <span data-ttu-id="a5f7c-245">If there was an error, you see a link in the **Error** column.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-245">If there was an error, you see a link in the **Error** column.</span></span> <span data-ttu-id="a5f7c-246">Click the link in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-246">Click the link in the **Actions** column.</span></span> 

    ![Pipeline runs](media\tutorial-incremental-copy-change-tracking-feature-powershell\monitor-pipeline-runs-4.png)    
6. <span data-ttu-id="a5f7c-248">When you click the link in the **Actions** column, you see the following page that shows all the **activity runs** for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-248">When you click the link in the **Actions** column, you see the following page that shows all the **activity runs** for the pipeline.</span></span> 

    ![Activity runs](media\tutorial-incremental-copy-change-tracking-feature-powershell\monitor-activity-runs-5.png)
7. <span data-ttu-id="a5f7c-250">To switch back to the **Pipeline runs** view, click **Pipelines** as shown in the image.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-250">To switch back to the **Pipeline runs** view, click **Pipelines** as shown in the image.</span></span> 


### <a name="review-the-results"></a><span data-ttu-id="a5f7c-251">Review the results</span><span class="sxs-lookup"><span data-stu-id="a5f7c-251">Review the results</span></span>
<span data-ttu-id="a5f7c-252">You see a file named `incremental-<GUID>.txt` in the `incchgtracking` folder of the `adftutorial` container.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-252">You see a file named `incremental-<GUID>.txt` in the `incchgtracking` folder of the `adftutorial` container.</span></span> 

![Output file from full copy](media\tutorial-incremental-copy-change-tracking-feature-powershell\full-copy-output-file.png)

<span data-ttu-id="a5f7c-254">The file should have the data from the Azure SQL database:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-254">The file should have the data from the Azure SQL database:</span></span>

```
1,aaaa,21
2,bbbb,24
3,cccc,20
4,dddd,26
5,eeee,22
```

## <a name="add-more-data-to-the-source-table"></a><span data-ttu-id="a5f7c-255">Add more data to the source table</span><span class="sxs-lookup"><span data-stu-id="a5f7c-255">Add more data to the source table</span></span>

<span data-ttu-id="a5f7c-256">Run the following query against the Azure SQL database to add a row and update a row.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-256">Run the following query against the Azure SQL database to add a row and update a row.</span></span> 

```sql
INSERT INTO data_source_table
(PersonID, Name, Age)
VALUES
(6, 'new','50');


UPDATE data_source_table
SET [Age] = '10', [name]='update' where [PersonID] = 1

``` 

## <a name="create-a-pipeline-for-the-delta-copy"></a><span data-ttu-id="a5f7c-257">Create a pipeline for the delta copy</span><span class="sxs-lookup"><span data-stu-id="a5f7c-257">Create a pipeline for the delta copy</span></span>
<span data-ttu-id="a5f7c-258">In this step, you create a pipeline with the following activities, and run it periodically.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-258">In this step, you create a pipeline with the following activities, and run it periodically.</span></span> <span data-ttu-id="a5f7c-259">The **lookup activities** get the old and new SYS_CHANGE_VERSION from Azure SQL Database and pass it to copy activity.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-259">The **lookup activities** get the old and new SYS_CHANGE_VERSION from Azure SQL Database and pass it to copy activity.</span></span> <span data-ttu-id="a5f7c-260">The **copy activity** copies the inserted/updated/deleted data between the two SYS_CHANGE_VERSION values from Azure SQL Database to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-260">The **copy activity** copies the inserted/updated/deleted data between the two SYS_CHANGE_VERSION values from Azure SQL Database to Azure Blob Storage.</span></span> <span data-ttu-id="a5f7c-261">The **stored procedure activity** updates the value of SYS_CHANGE_VERSION for the next pipeline run.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-261">The **stored procedure activity** updates the value of SYS_CHANGE_VERSION for the next pipeline run.</span></span>

1. <span data-ttu-id="a5f7c-262">Create a JSON file: IncrementalCopyPipeline.json in same folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-262">Create a JSON file: IncrementalCopyPipeline.json in same folder with the following content:</span></span> 

    ```json
    {
            "name": "IncrementalCopyPipeline",
            "properties": {
                "activities": [
                {
                        "name": "LookupLastChangeTrackingVersionActivity",
                        "type": "Lookup",
                        "typeProperties": {
                        "source": {
                            "type": "SqlSource",
                            "sqlReaderQuery": "select * from table_store_ChangeTracking_version"
                            },
        
                            "dataset": {
                            "referenceName": "ChangeTrackingDataset",
                            "type": "DatasetReference"
                            }
                        }
                    },
                    {
                        "name": "LookupCurrentChangeTrackingVersionActivity",
                        "type": "Lookup",
                        "typeProperties": {
                            "source": {
                                "type": "SqlSource",
                                "sqlReaderQuery": "SELECT CHANGE_TRACKING_CURRENT_VERSION() as CurrentChangeTrackingVersion"
                        },
    
                            "dataset": {
                            "referenceName": "SourceDataset",
                            "type": "DatasetReference"
                            }
                        }
                    },
    
                    {
                        "name": "IncrementalCopyActivity",
                        "type": "Copy",
                        "typeProperties": {
                            "source": {
                                "type": "SqlSource",
                                "sqlReaderQuery": "select data_source_table.PersonID,data_source_table.Name,data_source_table.Age, CT.SYS_CHANGE_VERSION, SYS_CHANGE_OPERATION from data_source_table RIGHT OUTER JOIN CHANGETABLE(CHANGES data_source_table, @{activity('LookupLastChangeTrackingVersionActivity').output.firstRow.SYS_CHANGE_VERSION}) as CT on data_source_table.PersonID = CT.PersonID where CT.SYS_CHANGE_VERSION <= @{activity('LookupCurrentChangeTrackingVersionActivity').output.firstRow.CurrentChangeTrackingVersion}"
                            },
                            "sink": {
                                "type": "BlobSink"
                            }
                        },
                        "dependsOn": [
                            {
                                "activity": "LookupLastChangeTrackingVersionActivity",
                                "dependencyConditions": [
                                    "Succeeded"
                                ]
                            },
                            {
                                "activity": "LookupCurrentChangeTrackingVersionActivity",
                                "dependencyConditions": [
                                    "Succeeded"
                                ]
                        }
                        ],
        
                        "inputs": [
                            {
                            "referenceName": "SourceDataset",
                                "type": "DatasetReference"
                        }
                        ],
                        "outputs": [
                            {
                                "referenceName": "SinkDataset",
                                "type": "DatasetReference"
                            }
                        ]
                    },
        
                {
                        "name": "StoredProceduretoUpdateChangeTrackingActivity",
                        "type": "SqlServerStoredProcedure",
                        "typeProperties": {
    
                            "storedProcedureName": "Update_ChangeTracking_Version",
                            "storedProcedureParameters": {
                            "CurrentTrackingVersion": {"value": "@{activity('LookupCurrentChangeTrackingVersionActivity').output.firstRow.CurrentChangeTrackingVersion}", "type": "INT64" },
                                "TableName":  { "value":"@{activity('LookupLastChangeTrackingVersionActivity').output.firstRow.TableName}", "type":"String"}
                            }
                    },
        
                        "linkedServiceName": {
                        "referenceName": "AzureSQLDatabaseLinkedService",
                            "type": "LinkedServiceReference"
                        },
        
                        "dependsOn": [
                        {
                                "activity": "IncrementalCopyActivity",
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
2. <span data-ttu-id="a5f7c-263">Run the Set-AzureRmDataFactoryV2Pipeline cmdlet to create the pipeline: FullCopyPipeline.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-263">Run the Set-AzureRmDataFactoryV2Pipeline cmdlet to create the pipeline: FullCopyPipeline.</span></span>
    
   ```powershell
    Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "IncrementalCopyPipeline" -File ".\IncrementalCopyPipeline.json"
   ``` 

   <span data-ttu-id="a5f7c-264">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-264">Here is the sample output:</span></span> 

   ```json
    PipelineName      : IncrementalCopyPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : IncCopyChgTrackingDF
    Activities        : {LookupLastChangeTrackingVersionActivity, LookupCurrentChangeTrackingVersionActivity, IncrementalCopyActivity, StoredProceduretoUpdateChangeTrackingActivity}
    Parameters        :
   ```

### <a name="run-the-incremental-copy-pipeline"></a><span data-ttu-id="a5f7c-265">Run the incremental copy pipeline</span><span class="sxs-lookup"><span data-stu-id="a5f7c-265">Run the incremental copy pipeline</span></span>
<span data-ttu-id="a5f7c-266">Run the pipeline: **IncrementalCopyPipeline** by using **Invoke-AzureRmDataFactoryV2Pipeline** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-266">Run the pipeline: **IncrementalCopyPipeline** by using **Invoke-AzureRmDataFactoryV2Pipeline** cmdlet.</span></span> 

```powershell
Invoke-AzureRmDataFactoryV2Pipeline -PipelineName "IncrementalCopyPipeline" -ResourceGroup $resourceGroupName -dataFactoryName $dataFactoryName     
``` 


### <a name="monitor-the-incremental-copy-pipeline"></a><span data-ttu-id="a5f7c-267">Monitor the incremental copy pipeline</span><span class="sxs-lookup"><span data-stu-id="a5f7c-267">Monitor the incremental copy pipeline</span></span>
1. <span data-ttu-id="a5f7c-268">In the **Data Integration Application**, refresh the **pipeline runs** view.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-268">In the **Data Integration Application**, refresh the **pipeline runs** view.</span></span> <span data-ttu-id="a5f7c-269">Confirm that you see the IncrementalCopyPipeline in the list.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-269">Confirm that you see the IncrementalCopyPipeline in the list.</span></span> <span data-ttu-id="a5f7c-270">Click the link in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-270">Click the link in the **Actions** column.</span></span>  

    ![Pipeline runs](media\tutorial-incremental-copy-change-tracking-feature-powershell\monitor-pipeline-runs-6.png)    
2. <span data-ttu-id="a5f7c-272">When you click the link in the **Actions** column, you see the following page that shows all the **activity runs** for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-272">When you click the link in the **Actions** column, you see the following page that shows all the **activity runs** for the pipeline.</span></span> 

    ![Activity runs](media\tutorial-incremental-copy-change-tracking-feature-powershell\monitor-activity-runs-7.png)
3. <span data-ttu-id="a5f7c-274">To switch back to the **Pipeline runs** view, click **Pipelines** as shown in the image.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-274">To switch back to the **Pipeline runs** view, click **Pipelines** as shown in the image.</span></span> 

### <a name="review-the-results"></a><span data-ttu-id="a5f7c-275">Review the results</span><span class="sxs-lookup"><span data-stu-id="a5f7c-275">Review the results</span></span>
<span data-ttu-id="a5f7c-276">You see the second file in the `incchgtracking` folder of the `adftutorial` container.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-276">You see the second file in the `incchgtracking` folder of the `adftutorial` container.</span></span> 

![Output file from incremental copy](media\tutorial-incremental-copy-change-tracking-feature-powershell\incremental-copy-output-file.png)

<span data-ttu-id="a5f7c-278">The file should have only the delta data from the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-278">The file should have only the delta data from the Azure SQL database.</span></span> <span data-ttu-id="a5f7c-279">The record with `U` is the updated row in the database and `I` is the one added row.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-279">The record with `U` is the updated row in the database and `I` is the one added row.</span></span> 

```
1,update,10,2,U
6,new,50,1,I
```
<span data-ttu-id="a5f7c-280">The first three columns are changed data from data_source_table.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-280">The first three columns are changed data from data_source_table.</span></span> <span data-ttu-id="a5f7c-281">The last two columns are the metadata from change tracking system table.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-281">The last two columns are the metadata from change tracking system table.</span></span> <span data-ttu-id="a5f7c-282">The fourth column is the SYS_CHANGE_VERSION for each changed row.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-282">The fourth column is the SYS_CHANGE_VERSION for each changed row.</span></span> <span data-ttu-id="a5f7c-283">The fifth column is the operation:  U = update, I = insert.</span><span class="sxs-lookup"><span data-stu-id="a5f7c-283">The fifth column is the operation:  U = update, I = insert.</span></span>  <span data-ttu-id="a5f7c-284">For details about the change tracking information, see [CHANGETABLE](/sql/relational-databases/system-functions/changetable-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="a5f7c-284">For details about the change tracking information, see [CHANGETABLE](/sql/relational-databases/system-functions/changetable-transact-sql).</span></span> 

```
==================================================================
PersonID Name    Age    SYS_CHANGE_VERSION    SYS_CHANGE_OPERATION
==================================================================
1        update  10     2                     U
6        new     50     1                     I
```

    
## <a name="next-steps"></a><span data-ttu-id="a5f7c-285">Next steps</span><span class="sxs-lookup"><span data-stu-id="a5f7c-285">Next steps</span></span>
<span data-ttu-id="a5f7c-286">Advance to the following tutorial to learn about transforming data by using a Spark cluster on Azure:</span><span class="sxs-lookup"><span data-stu-id="a5f7c-286">Advance to the following tutorial to learn about transforming data by using a Spark cluster on Azure:</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="a5f7c-287">Transform data using Spark cluster in cloud</span><span class="sxs-lookup"><span data-stu-id="a5f7c-287">Transform data using Spark cluster in cloud</span></span>](tutorial-transform-data-spark-powershell.md)



