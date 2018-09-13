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
ms.date: 01/12/2018
ms.author: yexu
ms.openlocfilehash: f06094fb82f10276f7a41d1b22f6dd99836a497f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855699"
---
# <a name="incrementally-load-data-from-azure-sql-database-to-azure-blob-storage-using-change-tracking-information"></a><span data-ttu-id="4b3b6-103">Incrementally load data from Azure SQL Database to Azure Blob Storage using change tracking information</span><span class="sxs-lookup"><span data-stu-id="4b3b6-103">Incrementally load data from Azure SQL Database to Azure Blob Storage using change tracking information</span></span> 
<span data-ttu-id="4b3b6-104">In this tutorial, you create an Azure data factory with a pipeline that loads delta data based on **change tracking** information in the source Azure SQL database to an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-104">In this tutorial, you create an Azure data factory with a pipeline that loads delta data based on **change tracking** information in the source Azure SQL database to an Azure blob storage.</span></span>  

<span data-ttu-id="4b3b6-105">You perform the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="4b3b6-105">You perform the following steps in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4b3b6-106">Prepare the source data store</span><span class="sxs-lookup"><span data-stu-id="4b3b6-106">Prepare the source data store</span></span>
> * <span data-ttu-id="4b3b6-107">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-107">Create a data factory.</span></span>
> * <span data-ttu-id="4b3b6-108">Create linked services.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-108">Create linked services.</span></span> 
> * <span data-ttu-id="4b3b6-109">Create source, sink, and change tracking datasets.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-109">Create source, sink, and change tracking datasets.</span></span>
> * <span data-ttu-id="4b3b6-110">Create, run, and monitor the full copy pipeline</span><span class="sxs-lookup"><span data-stu-id="4b3b6-110">Create, run, and monitor the full copy pipeline</span></span>
> * <span data-ttu-id="4b3b6-111">Add or update data in the source table</span><span class="sxs-lookup"><span data-stu-id="4b3b6-111">Add or update data in the source table</span></span>
> * <span data-ttu-id="4b3b6-112">Create, run, and monitor the incremental copy pipeline</span><span class="sxs-lookup"><span data-stu-id="4b3b6-112">Create, run, and monitor the incremental copy pipeline</span></span>

## <a name="overview"></a><span data-ttu-id="4b3b6-113">Overview</span><span class="sxs-lookup"><span data-stu-id="4b3b6-113">Overview</span></span>
<span data-ttu-id="4b3b6-114">In a data integration solution, incrementally loading data after initial data loads is a widely used scenario.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-114">In a data integration solution, incrementally loading data after initial data loads is a widely used scenario.</span></span> <span data-ttu-id="4b3b6-115">In some cases, the changed data within a period in your source data store can be easily to sliced up (for example, LastModifyTime, CreationTime).</span><span class="sxs-lookup"><span data-stu-id="4b3b6-115">In some cases, the changed data within a period in your source data store can be easily to sliced up (for example, LastModifyTime, CreationTime).</span></span> <span data-ttu-id="4b3b6-116">In some cases, there is no explicit way to identify the delta data from last time you processed the data.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-116">In some cases, there is no explicit way to identify the delta data from last time you processed the data.</span></span> <span data-ttu-id="4b3b6-117">The Change Tracking technology supported by data stores such as Azure SQL Database and SQL Server can be used to identify the delta data.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-117">The Change Tracking technology supported by data stores such as Azure SQL Database and SQL Server can be used to identify the delta data.</span></span>  <span data-ttu-id="4b3b6-118">This tutorial describes how to use Azure Data Factory with SQL Change Tracking technology to incrementally load delta data from Azure SQL Database into Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-118">This tutorial describes how to use Azure Data Factory with SQL Change Tracking technology to incrementally load delta data from Azure SQL Database into Azure Blob Storage.</span></span>  <span data-ttu-id="4b3b6-119">For more concrete information about SQL Change Tracking technology, see [Change tracking in SQL Server](/sql/relational-databases/track-changes/about-change-tracking-sql-server).</span><span class="sxs-lookup"><span data-stu-id="4b3b6-119">For more concrete information about SQL Change Tracking technology, see [Change tracking in SQL Server](/sql/relational-databases/track-changes/about-change-tracking-sql-server).</span></span> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="4b3b6-120">End-to-end workflow</span><span class="sxs-lookup"><span data-stu-id="4b3b6-120">End-to-end workflow</span></span>
<span data-ttu-id="4b3b6-121">Here are the typical end-to-end workflow steps to incrementally load data using the Change Tracking technology.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-121">Here are the typical end-to-end workflow steps to incrementally load data using the Change Tracking technology.</span></span>

> [!NOTE]
> <span data-ttu-id="4b3b6-122">Both Azure SQL Database and SQL Server support the Change Tracking technology.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-122">Both Azure SQL Database and SQL Server support the Change Tracking technology.</span></span> <span data-ttu-id="4b3b6-123">This tutorial uses Azure SQL Database as the source data store.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-123">This tutorial uses Azure SQL Database as the source data store.</span></span> <span data-ttu-id="4b3b6-124">You can also use an on-premises SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-124">You can also use an on-premises SQL Server.</span></span> 

1. <span data-ttu-id="4b3b6-125">**Initial loading of historical data** (run once):</span><span class="sxs-lookup"><span data-stu-id="4b3b6-125">**Initial loading of historical data** (run once):</span></span>
    1. <span data-ttu-id="4b3b6-126">Enable Change Tracking technology in the source Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-126">Enable Change Tracking technology in the source Azure SQL database.</span></span>
    2. <span data-ttu-id="4b3b6-127">Get the initial value of SYS_CHANGE_VERSION in the Azure SQL database as the baseline to capture changed data.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-127">Get the initial value of SYS_CHANGE_VERSION in the Azure SQL database as the baseline to capture changed data.</span></span>
    3. <span data-ttu-id="4b3b6-128">Load full data from the Azure SQL database into an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-128">Load full data from the Azure SQL database into an Azure blob storage.</span></span> 
2. <span data-ttu-id="4b3b6-129">**Incremental loading of delta data on a schedule** (run periodically after the initial loading of data):</span><span class="sxs-lookup"><span data-stu-id="4b3b6-129">**Incremental loading of delta data on a schedule** (run periodically after the initial loading of data):</span></span>
    1. <span data-ttu-id="4b3b6-130">Get the old and new SYS_CHANGE_VERSION values.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-130">Get the old and new SYS_CHANGE_VERSION values.</span></span>
    3. <span data-ttu-id="4b3b6-131">Load the delta data by joining the primary keys of changed rows (between two SYS_CHANGE_VERSION values) from **sys.change_tracking_tables** with data in the **source table**, and then move the delta data to destination.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-131">Load the delta data by joining the primary keys of changed rows (between two SYS_CHANGE_VERSION values) from **sys.change_tracking_tables** with data in the **source table**, and then move the delta data to destination.</span></span>
    4. <span data-ttu-id="4b3b6-132">Update the SYS_CHANGE_VERSION for the delta loading next time.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-132">Update the SYS_CHANGE_VERSION for the delta loading next time.</span></span>

## <a name="high-level-solution"></a><span data-ttu-id="4b3b6-133">High-level solution</span><span class="sxs-lookup"><span data-stu-id="4b3b6-133">High-level solution</span></span>
<span data-ttu-id="4b3b6-134">In this tutorial, you create two pipelines that perform the following two operations:</span><span class="sxs-lookup"><span data-stu-id="4b3b6-134">In this tutorial, you create two pipelines that perform the following two operations:</span></span>  

1. <span data-ttu-id="4b3b6-135">**Initial load:** you create a pipeline with a copy activity that copies the entire data from the source data store (Azure SQL Database) to the destination data store (Azure Blob Storage).</span><span class="sxs-lookup"><span data-stu-id="4b3b6-135">**Initial load:** you create a pipeline with a copy activity that copies the entire data from the source data store (Azure SQL Database) to the destination data store (Azure Blob Storage).</span></span>

    ![Full loading of data](media/tutorial-incremental-copy-change-tracking-feature-portal/full-load-flow-diagram.png)
1.  <span data-ttu-id="4b3b6-137">**Incremental load:** you create a pipeline with the following activities, and run it periodically.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-137">**Incremental load:** you create a pipeline with the following activities, and run it periodically.</span></span> 
    1. <span data-ttu-id="4b3b6-138">Create **two lookup activities** to get the old and new SYS_CHANGE_VERSION from Azure SQL Database and pass it to copy activity.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-138">Create **two lookup activities** to get the old and new SYS_CHANGE_VERSION from Azure SQL Database and pass it to copy activity.</span></span>
    2. <span data-ttu-id="4b3b6-139">Create **one copy activity** to copy the inserted/updated/deleted data between the two SYS_CHANGE_VERSION values from Azure SQL Database to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-139">Create **one copy activity** to copy the inserted/updated/deleted data between the two SYS_CHANGE_VERSION values from Azure SQL Database to Azure Blob Storage.</span></span>
    3. <span data-ttu-id="4b3b6-140">Create **one stored procedure activity** to update the value of SYS_CHANGE_VERSION for the next pipeline run.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-140">Create **one stored procedure activity** to update the value of SYS_CHANGE_VERSION for the next pipeline run.</span></span>

    ![Increment load flow diagram](media/tutorial-incremental-copy-change-tracking-feature-portal/incremental-load-flow-diagram.png)


<span data-ttu-id="4b3b6-142">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-142">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b3b6-143">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4b3b6-143">Prerequisites</span></span>
* <span data-ttu-id="4b3b6-144">**Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-144">**Azure SQL Database**.</span></span> <span data-ttu-id="4b3b6-145">You use the database as the **source** data store.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-145">You use the database as the **source** data store.</span></span> <span data-ttu-id="4b3b6-146">If you don't have an Azure SQL Database, see the [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) article for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-146">If you don't have an Azure SQL Database, see the [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) article for steps to create one.</span></span>
* <span data-ttu-id="4b3b6-147">**Azure Storage account**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-147">**Azure Storage account**.</span></span> <span data-ttu-id="4b3b6-148">You use the blob storage as the **sink** data store.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-148">You use the blob storage as the **sink** data store.</span></span> <span data-ttu-id="4b3b6-149">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-149">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span></span> <span data-ttu-id="4b3b6-150">Create a container named **adftutorial**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-150">Create a container named **adftutorial**.</span></span> 

### <a name="create-a-data-source-table-in-your-azure-sql-database"></a><span data-ttu-id="4b3b6-151">Create a data source table in your Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="4b3b6-151">Create a data source table in your Azure SQL database</span></span>
1. <span data-ttu-id="4b3b6-152">Launch **SQL Server Management Studio**, and connect to your Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-152">Launch **SQL Server Management Studio**, and connect to your Azure SQL server.</span></span> 
2. <span data-ttu-id="4b3b6-153">In **Server Explorer**, right-click your **database** and choose the **New Query**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-153">In **Server Explorer**, right-click your **database** and choose the **New Query**.</span></span>
3. <span data-ttu-id="4b3b6-154">Run the following SQL command against your Azure SQL database to create a table named `data_source_table` as data source store.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-154">Run the following SQL command against your Azure SQL database to create a table named `data_source_table` as data source store.</span></span>  
    
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
4. <span data-ttu-id="4b3b6-155">Enable **Change Tracking** mechanism on your database and the source table (data_source_table) by running the following SQL query:</span><span class="sxs-lookup"><span data-stu-id="4b3b6-155">Enable **Change Tracking** mechanism on your database and the source table (data_source_table) by running the following SQL query:</span></span> 

    > [!NOTE]
    > - <span data-ttu-id="4b3b6-156">Replace &lt;your database name&gt; with the name of your Azure SQL database that has the data_source_table.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-156">Replace &lt;your database name&gt; with the name of your Azure SQL database that has the data_source_table.</span></span> 
    > - <span data-ttu-id="4b3b6-157">The changed data is kept for two days in the current example.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-157">The changed data is kept for two days in the current example.</span></span> <span data-ttu-id="4b3b6-158">If you load the changed data for every three days or more, some changed data is not included.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-158">If you load the changed data for every three days or more, some changed data is not included.</span></span>  <span data-ttu-id="4b3b6-159">You need to either change the value of CHANGE_RETENTION to a bigger number.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-159">You need to either change the value of CHANGE_RETENTION to a bigger number.</span></span> <span data-ttu-id="4b3b6-160">Alternatively, ensure that your period to load the changed data is within two days.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-160">Alternatively, ensure that your period to load the changed data is within two days.</span></span> <span data-ttu-id="4b3b6-161">For more information, see [Enable change tracking for a database](/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server#enable-change-tracking-for-a-database)</span><span class="sxs-lookup"><span data-stu-id="4b3b6-161">For more information, see [Enable change tracking for a database](/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server#enable-change-tracking-for-a-database)</span></span>
 
    ```sql
    ALTER DATABASE <your database name>
    SET CHANGE_TRACKING = ON  
    (CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON)  
  
    ALTER TABLE data_source_table
    ENABLE CHANGE_TRACKING  
    WITH (TRACK_COLUMNS_UPDATED = ON)
    ```
5. <span data-ttu-id="4b3b6-162">Create a new table and store the ChangeTracking_version with a default value by running the following query:</span><span class="sxs-lookup"><span data-stu-id="4b3b6-162">Create a new table and store the ChangeTracking_version with a default value by running the following query:</span></span> 

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
    > <span data-ttu-id="4b3b6-163">If the data is not changed after you enabled the change tracking for SQL Database, the value of the change tracking version is 0.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-163">If the data is not changed after you enabled the change tracking for SQL Database, the value of the change tracking version is 0.</span></span>
6. <span data-ttu-id="4b3b6-164">Run the following query to create a stored procedure in your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-164">Run the following query to create a stored procedure in your Azure SQL database.</span></span> <span data-ttu-id="4b3b6-165">The pipeline invokes this stored procedure to update the change tracking version in the table you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-165">The pipeline invokes this stored procedure to update the change tracking version in the table you created in the previous step.</span></span> 

    ```sql
    CREATE PROCEDURE Update_ChangeTracking_Version @CurrentTrackingVersion BIGINT, @TableName varchar(50)
    AS
    
    BEGIN
    
        UPDATE table_store_ChangeTracking_version
        SET [SYS_CHANGE_VERSION] = @CurrentTrackingVersion
    WHERE [TableName] = @TableName
    
    END    
    ```

### <a name="azure-powershell"></a><span data-ttu-id="4b3b6-166">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b3b6-166">Azure PowerShell</span></span>
<span data-ttu-id="4b3b6-167">Install the latest Azure PowerShell modules by following  instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="4b3b6-167">Install the latest Azure PowerShell modules by following  instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="4b3b6-168">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="4b3b6-168">Create a data factory</span></span>

1. <span data-ttu-id="4b3b6-169">Launch **Microsoft Edge** or **Google Chrome** web browser.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-169">Launch **Microsoft Edge** or **Google Chrome** web browser.</span></span> <span data-ttu-id="4b3b6-170">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-170">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span></span>
1. <span data-ttu-id="4b3b6-171">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-171">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span> 
   
   ![New->DataFactory](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-azure-data-factory-menu.png)
2. <span data-ttu-id="4b3b6-173">In the **New data factory** page, enter **ADFTutorialDataFactory** for the **name**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-173">In the **New data factory** page, enter **ADFTutorialDataFactory** for the **name**.</span></span> 
      
     ![New data factory page](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-azure-data-factory.png)
 
   <span data-ttu-id="4b3b6-175">The name of the Azure data factory must be **globally unique**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-175">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="4b3b6-176">If you receive the following error, change the name of the data factory (for example, yournameADFTutorialDataFactory) and try creating again.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-176">If you receive the following error, change the name of the data factory (for example, yournameADFTutorialDataFactory) and try creating again.</span></span> <span data-ttu-id="4b3b6-177">See [Data Factory - Naming Rules](naming-rules.md) article for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-177">See [Data Factory - Naming Rules](naming-rules.md) article for naming rules for Data Factory artifacts.</span></span>
  
       `Data factory name “ADFTutorialDataFactory” is not available`
3. <span data-ttu-id="4b3b6-178">Select your Azure **subscription** in which you want to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-178">Select your Azure **subscription** in which you want to create the data factory.</span></span> 
4. <span data-ttu-id="4b3b6-179">For the **Resource Group**, do one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="4b3b6-179">For the **Resource Group**, do one of the following steps:</span></span>
     
      - <span data-ttu-id="4b3b6-180">Select **Use existing**, and select an existing resource group from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-180">Select **Use existing**, and select an existing resource group from the drop-down list.</span></span> 
      - <span data-ttu-id="4b3b6-181">Select **Create new**, and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-181">Select **Create new**, and enter the name of a resource group.</span></span>   
         
        <span data-ttu-id="4b3b6-182">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4b3b6-182">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>  
4. <span data-ttu-id="4b3b6-183">Select **V2 (Preview)** for the **version**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-183">Select **V2 (Preview)** for the **version**.</span></span>
5. <span data-ttu-id="4b3b6-184">Select the **location** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-184">Select the **location** for the data factory.</span></span> <span data-ttu-id="4b3b6-185">Only locations that are supported are displayed in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-185">Only locations that are supported are displayed in the drop-down list.</span></span> <span data-ttu-id="4b3b6-186">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-186">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span></span>
6. <span data-ttu-id="4b3b6-187">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-187">Select **Pin to dashboard**.</span></span>     
7. <span data-ttu-id="4b3b6-188">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-188">Click **Create**.</span></span>      
8. <span data-ttu-id="4b3b6-189">On the dashboard, you see the following tile with status: **Deploying data factory**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-189">On the dashboard, you see the following tile with status: **Deploying data factory**.</span></span> 

    ![deploying data factory tile](media/tutorial-incremental-copy-change-tracking-feature-portal/deploying-data-factory.png)
9. <span data-ttu-id="4b3b6-191">After the creation is complete, you see the **Data Factory** page as shown in the image.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-191">After the creation is complete, you see the **Data Factory** page as shown in the image.</span></span>
   
   ![Data factory home page](./media/tutorial-incremental-copy-change-tracking-feature-portal/data-factory-home-page.png)
10. <span data-ttu-id="4b3b6-193">Click **Author & Monitor** tile to launch the Azure Data Factory user interface (UI) in a separate tab.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-193">Click **Author & Monitor** tile to launch the Azure Data Factory user interface (UI) in a separate tab.</span></span>
11. <span data-ttu-id="4b3b6-194">In the **get started** page, switch to the **Edit** tab in the left panel as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="4b3b6-194">In the **get started** page, switch to the **Edit** tab in the left panel as shown in the following image:</span></span> 

    ![Create pipeline button](./media/tutorial-incremental-copy-change-tracking-feature-portal/get-started-page.png)

## <a name="create-linked-services"></a><span data-ttu-id="4b3b6-196">Create linked services</span><span class="sxs-lookup"><span data-stu-id="4b3b6-196">Create linked services</span></span>
<span data-ttu-id="4b3b6-197">You create linked services in a data factory to link your data stores and compute services to the data factory.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-197">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="4b3b6-198">In this section, you create linked services to your Azure Storage account and Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-198">In this section, you create linked services to your Azure Storage account and Azure SQL database.</span></span> 

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="4b3b6-199">Create Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-199">Create Azure Storage linked service.</span></span>
<span data-ttu-id="4b3b6-200">In this step, you link your Azure Storage Account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-200">In this step, you link your Azure Storage Account to the data factory.</span></span>

1. <span data-ttu-id="4b3b6-201">Click **Connections**, and click **+ New**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-201">Click **Connections**, and click **+ New**.</span></span>

   ![New connection button](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-connection-button-storage.png)
2. <span data-ttu-id="4b3b6-203">In the **New Linked Service** window, select **Azure Blob Storage**, and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-203">In the **New Linked Service** window, select **Azure Blob Storage**, and click **Continue**.</span></span> 

   ![Select Azure Blob Storage](./media/tutorial-incremental-copy-change-tracking-feature-portal/select-azure-storage.png)
3. <span data-ttu-id="4b3b6-205">In the **New Linked Service** window, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="4b3b6-205">In the **New Linked Service** window, do the following steps:</span></span> 

    1. <span data-ttu-id="4b3b6-206">Enter **AzureStorageLinkedService** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-206">Enter **AzureStorageLinkedService** for **Name**.</span></span> 
    2. <span data-ttu-id="4b3b6-207">Select your Azure Storage account for **Storage account name**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-207">Select your Azure Storage account for **Storage account name**.</span></span> 
    3. <span data-ttu-id="4b3b6-208">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-208">Click **Save**.</span></span> 
    
   ![Azure Storage Account settings](./media/tutorial-incremental-copy-change-tracking-feature-portal/azure-storage-linked-service-settings.png)


### <a name="create-azure-sql-database-linked-service"></a><span data-ttu-id="4b3b6-210">Create Azure SQL Database linked service.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-210">Create Azure SQL Database linked service.</span></span>
<span data-ttu-id="4b3b6-211">In this step, you link your Azure SQL database to the data factory.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-211">In this step, you link your Azure SQL database to the data factory.</span></span>

1. <span data-ttu-id="4b3b6-212">Click **Connections**, and click **+ New**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-212">Click **Connections**, and click **+ New**.</span></span>
2. <span data-ttu-id="4b3b6-213">In the **New Linked Service** window, select **Azure SQL Database**, and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-213">In the **New Linked Service** window, select **Azure SQL Database**, and click **Continue**.</span></span> 
3. <span data-ttu-id="4b3b6-214">In the **New Linked Service** window, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="4b3b6-214">In the **New Linked Service** window, do the following steps:</span></span> 

    1. <span data-ttu-id="4b3b6-215">Enter **AzureSqlDatabaseLinkedService** for the **Name** field.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-215">Enter **AzureSqlDatabaseLinkedService** for the **Name** field.</span></span> 
    2. <span data-ttu-id="4b3b6-216">Select your Azure SQL server for the **Server name** field.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-216">Select your Azure SQL server for the **Server name** field.</span></span>
    4. <span data-ttu-id="4b3b6-217">Select your Azure SQL database for the **Database name** field.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-217">Select your Azure SQL database for the **Database name** field.</span></span> 
    5. <span data-ttu-id="4b3b6-218">Enter name of the user for the **User name** field.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-218">Enter name of the user for the **User name** field.</span></span> 
    6. <span data-ttu-id="4b3b6-219">Enter password for the user for the **Password** field.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-219">Enter password for the user for the **Password** field.</span></span> 
    7. <span data-ttu-id="4b3b6-220">Click **Test connection** to test the connection.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-220">Click **Test connection** to test the connection.</span></span>
    8. <span data-ttu-id="4b3b6-221">Click **Save** to save the linked service.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-221">Click **Save** to save the linked service.</span></span> 
    
       ![Azure SQL Database linked service settings](./media/tutorial-incremental-copy-change-tracking-feature-portal/azure-sql-database-linked-service-settings.png)

## <a name="create-datasets"></a><span data-ttu-id="4b3b6-223">Create datasets</span><span class="sxs-lookup"><span data-stu-id="4b3b6-223">Create datasets</span></span>
<span data-ttu-id="4b3b6-224">In this step, you create datasets to represent data source, data destination.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-224">In this step, you create datasets to represent data source, data destination.</span></span> <span data-ttu-id="4b3b6-225">and the place to store the SYS_CHANGE_VERSION.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-225">and the place to store the SYS_CHANGE_VERSION.</span></span>

### <a name="create-a-dataset-to-represent-source-data"></a><span data-ttu-id="4b3b6-226">Create a dataset to represent source data</span><span class="sxs-lookup"><span data-stu-id="4b3b6-226">Create a dataset to represent source data</span></span> 
<span data-ttu-id="4b3b6-227">In this step, you create a dataset to represent the source data.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-227">In this step, you create a dataset to represent the source data.</span></span> 

1. <span data-ttu-id="4b3b6-228">In the treeview, click **+ (plus)**, and click **Dataset**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-228">In the treeview, click **+ (plus)**, and click **Dataset**.</span></span> 

   ![New Dataset menu](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-dataset-menu.png)
2. <span data-ttu-id="4b3b6-230">Select **Azure SQL Database**, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-230">Select **Azure SQL Database**, and click **Finish**.</span></span> 

   ![Source dataset type - Azure SQL Database](./media/tutorial-incremental-copy-change-tracking-feature-portal/select-azure-sql-database.png)
3. <span data-ttu-id="4b3b6-232">You see a new tab for configuring the dataset.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-232">You see a new tab for configuring the dataset.</span></span> <span data-ttu-id="4b3b6-233">You also see the dataset in the treeview.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-233">You also see the dataset in the treeview.</span></span> <span data-ttu-id="4b3b6-234">In the **Properties** window, change the name of the dataset to **SourceDataset**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-234">In the **Properties** window, change the name of the dataset to **SourceDataset**.</span></span>

   ![Source dataset name](./media/tutorial-incremental-copy-change-tracking-feature-portal/source-dataset-name.png)    
4. <span data-ttu-id="4b3b6-236">Switch to the **Connection** tab, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="4b3b6-236">Switch to the **Connection** tab, and do the following steps:</span></span> 
    
    1. <span data-ttu-id="4b3b6-237">Select **AzureSqlDatabaseLinkedService** for **Linked service**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-237">Select **AzureSqlDatabaseLinkedService** for **Linked service**.</span></span> 
    2. <span data-ttu-id="4b3b6-238">Select **[dbo].[data_source_table]** for **Table**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-238">Select **[dbo].[data_source_table]** for **Table**.</span></span> 

   ![Source connection](./media/tutorial-incremental-copy-change-tracking-feature-portal/source-dataset-connection.png)

### <a name="create-a-dataset-to-represent-data-copied-to-sink-data-store"></a><span data-ttu-id="4b3b6-240">Create a dataset to represent data copied to sink data store.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-240">Create a dataset to represent data copied to sink data store.</span></span> 
<span data-ttu-id="4b3b6-241">In this step, you create a dataset to represent the data that is copied from the source data store.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-241">In this step, you create a dataset to represent the data that is copied from the source data store.</span></span> <span data-ttu-id="4b3b6-242">You created the adftutorial container in your Azure Blob Storage as part of the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-242">You created the adftutorial container in your Azure Blob Storage as part of the prerequisites.</span></span> <span data-ttu-id="4b3b6-243">Create the container if it does not exist (or) set it to the name of an existing one.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-243">Create the container if it does not exist (or) set it to the name of an existing one.</span></span> <span data-ttu-id="4b3b6-244">In this tutorial, the output file name is dynamically generated by using the expression: `@CONCAT('Incremental-', pipeline().RunId, '.txt')`.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-244">In this tutorial, the output file name is dynamically generated by using the expression: `@CONCAT('Incremental-', pipeline().RunId, '.txt')`.</span></span>

1. <span data-ttu-id="4b3b6-245">In the treeview, click **+ (plus)**, and click **Dataset**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-245">In the treeview, click **+ (plus)**, and click **Dataset**.</span></span> 

   ![New Dataset menu](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-dataset-menu.png)
2. <span data-ttu-id="4b3b6-247">Select **Azure Blob Storage**, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-247">Select **Azure Blob Storage**, and click **Finish**.</span></span> 

   ![Sink dataset type - Azure Blob Storage](./media/tutorial-incremental-copy-change-tracking-feature-portal/source-dataset-type.png)
3. <span data-ttu-id="4b3b6-249">You see a new tab for configuring the dataset.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-249">You see a new tab for configuring the dataset.</span></span> <span data-ttu-id="4b3b6-250">You also see the dataset in the treeview.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-250">You also see the dataset in the treeview.</span></span> <span data-ttu-id="4b3b6-251">In the **Properties** window, change the name of the dataset to **SinkDataset**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-251">In the **Properties** window, change the name of the dataset to **SinkDataset**.</span></span>

   ![Sink dataset - name](./media/tutorial-incremental-copy-change-tracking-feature-portal/sink-dataset-name.png)
4. <span data-ttu-id="4b3b6-253">Switch to the **Connection** tab in the Properties window, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="4b3b6-253">Switch to the **Connection** tab in the Properties window, and do the following steps:</span></span>

    1. <span data-ttu-id="4b3b6-254">Select **AzureStorageLinkedService** for **Linked service**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-254">Select **AzureStorageLinkedService** for **Linked service**.</span></span>
    2. <span data-ttu-id="4b3b6-255">Enter **adftutorial/incchgtracking** for **folder** part of the **filePath**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-255">Enter **adftutorial/incchgtracking** for **folder** part of the **filePath**.</span></span>
    3. <span data-ttu-id="4b3b6-256">Enter **@CONCAT('Incremental-', pipeline().RunId, '.txt')** for **file** part of the **filePath**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-256">Enter **@CONCAT('Incremental-', pipeline().RunId, '.txt')** for **file** part of the **filePath**.</span></span>  

       ![Sink dataset - connection](./media/tutorial-incremental-copy-change-tracking-feature-portal/sink-dataset-connection.png)

### <a name="create-a-dataset-to-represent-change-tracking-data"></a><span data-ttu-id="4b3b6-258">Create a dataset to represent change tracking data</span><span class="sxs-lookup"><span data-stu-id="4b3b6-258">Create a dataset to represent change tracking data</span></span> 
<span data-ttu-id="4b3b6-259">In this step, you create a dataset for storing the change tracking version.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-259">In this step, you create a dataset for storing the change tracking version.</span></span>  <span data-ttu-id="4b3b6-260">You created the table table_store_ChangeTracking_version as part of the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-260">You created the table table_store_ChangeTracking_version as part of the prerequisites.</span></span>

1. <span data-ttu-id="4b3b6-261">In the treeview, click **+ (plus)**, and click **Dataset**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-261">In the treeview, click **+ (plus)**, and click **Dataset**.</span></span> 
2. <span data-ttu-id="4b3b6-262">Select **Azure SQL Database**, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-262">Select **Azure SQL Database**, and click **Finish**.</span></span> 
3. <span data-ttu-id="4b3b6-263">You see a new tab for configuring the dataset.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-263">You see a new tab for configuring the dataset.</span></span> <span data-ttu-id="4b3b6-264">You also see the dataset in the treeview.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-264">You also see the dataset in the treeview.</span></span> <span data-ttu-id="4b3b6-265">In the **Properties** window, change the name of the dataset to **ChangeTrackingDataset**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-265">In the **Properties** window, change the name of the dataset to **ChangeTrackingDataset**.</span></span>
4. <span data-ttu-id="4b3b6-266">Switch to the **Connection** tab, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="4b3b6-266">Switch to the **Connection** tab, and do the following steps:</span></span> 
    
    1. <span data-ttu-id="4b3b6-267">Select **AzureSqlDatabaseLinkedService** for **Linked service**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-267">Select **AzureSqlDatabaseLinkedService** for **Linked service**.</span></span> 
    2. <span data-ttu-id="4b3b6-268">Select **[dbo].[table_store_ChangeTracking_version]** for **Table**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-268">Select **[dbo].[table_store_ChangeTracking_version]** for **Table**.</span></span> 

## <a name="create-a-pipeline-for-the-full-copy"></a><span data-ttu-id="4b3b6-269">Create a pipeline for the full copy</span><span class="sxs-lookup"><span data-stu-id="4b3b6-269">Create a pipeline for the full copy</span></span>
<span data-ttu-id="4b3b6-270">In this step, you create a pipeline with a copy activity that copies the entire data from the source data store (Azure SQL Database) to the destination data store (Azure Blob Storage).</span><span class="sxs-lookup"><span data-stu-id="4b3b6-270">In this step, you create a pipeline with a copy activity that copies the entire data from the source data store (Azure SQL Database) to the destination data store (Azure Blob Storage).</span></span>

1. <span data-ttu-id="4b3b6-271">Click **+ (plus)** in the left pane, and click **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-271">Click **+ (plus)** in the left pane, and click **Pipeline**.</span></span> 

    ![New pipeline menu](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-pipeline-menu.png)
2. <span data-ttu-id="4b3b6-273">You see a new tab for configuring the pipeline.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-273">You see a new tab for configuring the pipeline.</span></span> <span data-ttu-id="4b3b6-274">You also see the pipeline in the treeview.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-274">You also see the pipeline in the treeview.</span></span> <span data-ttu-id="4b3b6-275">In the **Properties** window, change the name of the pipeline to **FullCopyPipeline**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-275">In the **Properties** window, change the name of the pipeline to **FullCopyPipeline**.</span></span>

    ![New pipeline menu](./media/tutorial-incremental-copy-change-tracking-feature-portal/full-copy-pipeline-name.png)
3. <span data-ttu-id="4b3b6-277">In the **Activities** toolbox, expand **Data Flow**, and drag-drop the **Copy** activity to the pipeline designer surface, and set the name **FullCopyActivity**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-277">In the **Activities** toolbox, expand **Data Flow**, and drag-drop the **Copy** activity to the pipeline designer surface, and set the name **FullCopyActivity**.</span></span> 

    ![Full copy activity-name](./media/tutorial-incremental-copy-change-tracking-feature-portal/full-copy-activity-name.png)
4. <span data-ttu-id="4b3b6-279">Switch to the **Source** tab, and select **SourceDataset** for the **Source Dataset** field.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-279">Switch to the **Source** tab, and select **SourceDataset** for the **Source Dataset** field.</span></span> 

    ![Copy activity - source](./media/tutorial-incremental-copy-change-tracking-feature-portal/copy-activity-source.png)
5. <span data-ttu-id="4b3b6-281">Switch to the **Sink** tab, and select **SinkDataset** for the **Sink Dataset** field.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-281">Switch to the **Sink** tab, and select **SinkDataset** for the **Sink Dataset** field.</span></span> 

    ![Copy activity - sink](./media/tutorial-incremental-copy-change-tracking-feature-portal/copy-activity-sink.png)
6. <span data-ttu-id="4b3b6-283">To validate the pipeline definition, click **Validate** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-283">To validate the pipeline definition, click **Validate** on the toolbar.</span></span> <span data-ttu-id="4b3b6-284">Confirm that there is no validation error.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-284">Confirm that there is no validation error.</span></span> <span data-ttu-id="4b3b6-285">Close the **Pipeline Validation Report** by clicking **>>**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-285">Close the **Pipeline Validation Report** by clicking **>>**.</span></span> 

    ![Validate the pipeline](./media/tutorial-incremental-copy-change-tracking-feature-portal/full-copy-pipeline-validate.png)
7. <span data-ttu-id="4b3b6-287">To publish entities (linked services, datasets, and pipelines), click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-287">To publish entities (linked services, datasets, and pipelines), click **Publish**.</span></span> <span data-ttu-id="4b3b6-288">Wait until the publishing succeeds.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-288">Wait until the publishing succeeds.</span></span> 

    ![Publish button](./media/tutorial-incremental-copy-change-tracking-feature-portal/publish-button.png)
8. <span data-ttu-id="4b3b6-290">Wait until you see the **Successfully published** message.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-290">Wait until you see the **Successfully published** message.</span></span> 

    ![Publishing succeeded](./media/tutorial-incremental-copy-change-tracking-feature-portal/publishing-succeeded.png)
9. <span data-ttu-id="4b3b6-292">You can also see notifications by clicking the **Show Notifications** button on the left.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-292">You can also see notifications by clicking the **Show Notifications** button on the left.</span></span> <span data-ttu-id="4b3b6-293">To close the notifications window, click **X**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-293">To close the notifications window, click **X**.</span></span>

    ![Show notifications](./media/tutorial-incremental-copy-change-tracking-feature-portal/show-notifications.png)


### <a name="run-the-full-copy-pipeline"></a><span data-ttu-id="4b3b6-295">Run the full copy pipeline</span><span class="sxs-lookup"><span data-stu-id="4b3b6-295">Run the full copy pipeline</span></span>
<span data-ttu-id="4b3b6-296">Click **Trigger** on the toolbar for the pipeline, and click **Trigger Now**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-296">Click **Trigger** on the toolbar for the pipeline, and click **Trigger Now**.</span></span> 

![Trigger Now menu](./media/tutorial-incremental-copy-change-tracking-feature-portal/trigger-now-menu.png)

### <a name="monitor-the-full-copy-pipeline"></a><span data-ttu-id="4b3b6-298">Monitor the full copy pipeline</span><span class="sxs-lookup"><span data-stu-id="4b3b6-298">Monitor the full copy pipeline</span></span>

1. <span data-ttu-id="4b3b6-299">Click the **Monitor** tab on the left.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-299">Click the **Monitor** tab on the left.</span></span> <span data-ttu-id="4b3b6-300">You see the pipeline run in the list and its status.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-300">You see the pipeline run in the list and its status.</span></span> <span data-ttu-id="4b3b6-301">To refresh the list, click **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-301">To refresh the list, click **Refresh**.</span></span> <span data-ttu-id="4b3b6-302">The links in the Actions column let you view activity runs associated with the pipeline run and to rerun the pipeline.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-302">The links in the Actions column let you view activity runs associated with the pipeline run and to rerun the pipeline.</span></span> 

    ![Pipeline runs](./media/tutorial-incremental-copy-change-tracking-feature-portal/monitor-full-copy-pipeline-run.png)
2. <span data-ttu-id="4b3b6-304">To view activity runs associated with the pipeline run, click the **View Activity Runs** link in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-304">To view activity runs associated with the pipeline run, click the **View Activity Runs** link in the **Actions** column.</span></span> <span data-ttu-id="4b3b6-305">There is only one activity in the pipeline, so you see only one entry in the list.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-305">There is only one activity in the pipeline, so you see only one entry in the list.</span></span> <span data-ttu-id="4b3b6-306">To switch back to the pipeline runs view, click **Pipelines** link at the top.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-306">To switch back to the pipeline runs view, click **Pipelines** link at the top.</span></span> 

    ![Activity runs](./media/tutorial-incremental-copy-change-tracking-feature-portal/activity-runs-full-copy.png)

### <a name="review-the-results"></a><span data-ttu-id="4b3b6-308">Review the results</span><span class="sxs-lookup"><span data-stu-id="4b3b6-308">Review the results</span></span>
<span data-ttu-id="4b3b6-309">You see a file named `incremental-<GUID>.txt` in the `incchgtracking` folder of the `adftutorial` container.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-309">You see a file named `incremental-<GUID>.txt` in the `incchgtracking` folder of the `adftutorial` container.</span></span> 

![Output file from full copy](media\tutorial-incremental-copy-change-tracking-feature-portal\full-copy-output-file.png)

<span data-ttu-id="4b3b6-311">The file should have the data from the Azure SQL database:</span><span class="sxs-lookup"><span data-stu-id="4b3b6-311">The file should have the data from the Azure SQL database:</span></span>

```
1,aaaa,21
2,bbbb,24
3,cccc,20
4,dddd,26
5,eeee,22
```

## <a name="add-more-data-to-the-source-table"></a><span data-ttu-id="4b3b6-312">Add more data to the source table</span><span class="sxs-lookup"><span data-stu-id="4b3b6-312">Add more data to the source table</span></span>

<span data-ttu-id="4b3b6-313">Run the following query against the Azure SQL database to add a row and update a row.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-313">Run the following query against the Azure SQL database to add a row and update a row.</span></span> 

```sql
INSERT INTO data_source_table
(PersonID, Name, Age)
VALUES
(6, 'new','50');


UPDATE data_source_table
SET [Age] = '10', [name]='update' where [PersonID] = 1

``` 

## <a name="create-a-pipeline-for-the-delta-copy"></a><span data-ttu-id="4b3b6-314">Create a pipeline for the delta copy</span><span class="sxs-lookup"><span data-stu-id="4b3b6-314">Create a pipeline for the delta copy</span></span>
<span data-ttu-id="4b3b6-315">In this step, you create a pipeline with the following activities, and run it periodically.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-315">In this step, you create a pipeline with the following activities, and run it periodically.</span></span> <span data-ttu-id="4b3b6-316">The **lookup activities** get the old and new SYS_CHANGE_VERSION from Azure SQL Database and pass it to copy activity.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-316">The **lookup activities** get the old and new SYS_CHANGE_VERSION from Azure SQL Database and pass it to copy activity.</span></span> <span data-ttu-id="4b3b6-317">The **copy activity** copies the inserted/updated/deleted data between the two SYS_CHANGE_VERSION values from Azure SQL Database to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-317">The **copy activity** copies the inserted/updated/deleted data between the two SYS_CHANGE_VERSION values from Azure SQL Database to Azure Blob Storage.</span></span> <span data-ttu-id="4b3b6-318">The **stored procedure activity** updates the value of SYS_CHANGE_VERSION for the next pipeline run.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-318">The **stored procedure activity** updates the value of SYS_CHANGE_VERSION for the next pipeline run.</span></span>

1. <span data-ttu-id="4b3b6-319">In the Data Factory UI, switch to the **Edit** tab. Click **+ (plus)** in the left pane, and click **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-319">In the Data Factory UI, switch to the **Edit** tab. Click **+ (plus)** in the left pane, and click **Pipeline**.</span></span> 

    ![New pipeline menu](./media/tutorial-incremental-copy-change-tracking-feature-portal/new-pipeline-menu-2.png)
2. <span data-ttu-id="4b3b6-321">You see a new tab for configuring the pipeline.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-321">You see a new tab for configuring the pipeline.</span></span> <span data-ttu-id="4b3b6-322">You also see the pipeline in the treeview.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-322">You also see the pipeline in the treeview.</span></span> <span data-ttu-id="4b3b6-323">In the **Properties** window, change the name of the pipeline to **IncrementalCopyPipeline**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-323">In the **Properties** window, change the name of the pipeline to **IncrementalCopyPipeline**.</span></span>

    ![Pipeline name](./media/tutorial-incremental-copy-change-tracking-feature-portal/incremental-copy-pipeline-name.png)
3. <span data-ttu-id="4b3b6-325">Expand **General** in the **Activities** toolbox, and drag-drop the **Lookup** activity to the pipeline designer surface.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-325">Expand **General** in the **Activities** toolbox, and drag-drop the **Lookup** activity to the pipeline designer surface.</span></span> <span data-ttu-id="4b3b6-326">Set the name of the activity to **LookupLastChangeTrackingVersionActivity**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-326">Set the name of the activity to **LookupLastChangeTrackingVersionActivity**.</span></span> <span data-ttu-id="4b3b6-327">This activity gets the change tracking version used in the last copy operation that is stored in the table **table_store_ChangeTracking_version**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-327">This activity gets the change tracking version used in the last copy operation that is stored in the table **table_store_ChangeTracking_version**.</span></span>

    ![Lookup Activity - name](./media/tutorial-incremental-copy-change-tracking-feature-portal/first-lookup-activity-name.png)
4. <span data-ttu-id="4b3b6-329">Switch to the **Settings** in the **Properties** window, and select **ChangeTrackingDataset** for the **Source Dataset** field.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-329">Switch to the **Settings** in the **Properties** window, and select **ChangeTrackingDataset** for the **Source Dataset** field.</span></span> 

    ![Lookup Activity - settings](./media/tutorial-incremental-copy-change-tracking-feature-portal/first-lookup-activity-settings.png)
5. <span data-ttu-id="4b3b6-331">Drag-and-drop the **Lookup** activity from the **Activities** toolbox to the pipeline designer surface.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-331">Drag-and-drop the **Lookup** activity from the **Activities** toolbox to the pipeline designer surface.</span></span> <span data-ttu-id="4b3b6-332">Set the name of the activity to **LookupCurrentChangeTrackingVersionActivity**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-332">Set the name of the activity to **LookupCurrentChangeTrackingVersionActivity**.</span></span> <span data-ttu-id="4b3b6-333">This activity gets the current change tracking version.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-333">This activity gets the current change tracking version.</span></span>

    ![Lookup Activity - name](./media/tutorial-incremental-copy-change-tracking-feature-portal/second-lookup-activity-name.png)
6. <span data-ttu-id="4b3b6-335">Switch to the **Settings** in the **Properties** window, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="4b3b6-335">Switch to the **Settings** in the **Properties** window, and do the following steps:</span></span>

    1. <span data-ttu-id="4b3b6-336">Select **SourceDataset** for the **Source Dataset** field.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-336">Select **SourceDataset** for the **Source Dataset** field.</span></span>
    2. <span data-ttu-id="4b3b6-337">Select **Query** for **Use Query**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-337">Select **Query** for **Use Query**.</span></span> 
    3. <span data-ttu-id="4b3b6-338">Enter the following SQL query for **Query**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-338">Enter the following SQL query for **Query**.</span></span> 

        ```sql
        SELECT CHANGE_TRACKING_CURRENT_VERSION() as CurrentChangeTrackingVersion
        ```

    ![Lookup Activity - settings](./media/tutorial-incremental-copy-change-tracking-feature-portal/second-lookup-activity-settings.png)
7. <span data-ttu-id="4b3b6-340">In the **Activities** toolbox, expand **Data Flow**, and drag-drop the **Copy** activity to the pipeline designer surface.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-340">In the **Activities** toolbox, expand **Data Flow**, and drag-drop the **Copy** activity to the pipeline designer surface.</span></span> <span data-ttu-id="4b3b6-341">Set the name of the activity to **IncrementalCopyActivity**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-341">Set the name of the activity to **IncrementalCopyActivity**.</span></span> <span data-ttu-id="4b3b6-342">This activity copies the data between last change tracking version and the current change tracking version to the destination data store.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-342">This activity copies the data between last change tracking version and the current change tracking version to the destination data store.</span></span> 

    ![Copy Activity - name](./media/tutorial-incremental-copy-change-tracking-feature-portal/incremental-copy-activity-name.png)
8. <span data-ttu-id="4b3b6-344">Switch to the **Source** tab in the **Properties** window, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="4b3b6-344">Switch to the **Source** tab in the **Properties** window, and do the following steps:</span></span>

    1. <span data-ttu-id="4b3b6-345">Select **SourceDataset** for **Source Dataset**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-345">Select **SourceDataset** for **Source Dataset**.</span></span> 
    2. <span data-ttu-id="4b3b6-346">Select **Query** for **Use Query**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-346">Select **Query** for **Use Query**.</span></span> 
    3. <span data-ttu-id="4b3b6-347">Enter the following SQL query for **Query**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-347">Enter the following SQL query for **Query**.</span></span> 

        ```sql
        select data_source_table.PersonID,data_source_table.Name,data_source_table.Age, CT.SYS_CHANGE_VERSION, SYS_CHANGE_OPERATION from data_source_table RIGHT OUTER JOIN CHANGETABLE(CHANGES data_source_table, @{activity('LookupLastChangeTrackingVersionActivity').output.firstRow.SYS_CHANGE_VERSION}) as CT on data_source_table.PersonID = CT.PersonID where CT.SYS_CHANGE_VERSION <= @{activity('LookupCurrentChangeTrackingVersionActivity').output.firstRow.CurrentChangeTrackingVersion}
        ```
    
    ![Copy Activity - source settings](./media/tutorial-incremental-copy-change-tracking-feature-portal/inc-copy-source-settings.png)
9. <span data-ttu-id="4b3b6-349">Switch to the **Sink** tab, and select **SinkDataset** for the **Sink Dataset** field.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-349">Switch to the **Sink** tab, and select **SinkDataset** for the **Sink Dataset** field.</span></span> 

    ![Copy Activity - sink settings](./media/tutorial-incremental-copy-change-tracking-feature-portal/inc-copy-sink-settings.png)
10. <span data-ttu-id="4b3b6-351">**Connect both Lookup activities to the Copy activity** one by one.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-351">**Connect both Lookup activities to the Copy activity** one by one.</span></span> <span data-ttu-id="4b3b6-352">Drag the **green** button attached to the **Lookup** activity to the **Copy** activity.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-352">Drag the **green** button attached to the **Lookup** activity to the **Copy** activity.</span></span> 

    ![Connect Lookup and Copy activities](./media/tutorial-incremental-copy-change-tracking-feature-portal/connect-lookup-and-copy.png)
11. <span data-ttu-id="4b3b6-354">Drag-and-drop the **Stored Procedure** activity from the **Activities** toolbox to the pipeline designer surface.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-354">Drag-and-drop the **Stored Procedure** activity from the **Activities** toolbox to the pipeline designer surface.</span></span> <span data-ttu-id="4b3b6-355">Set the name of the activity to **StoredProceduretoUpdateChangeTrackingActivity**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-355">Set the name of the activity to **StoredProceduretoUpdateChangeTrackingActivity**.</span></span> <span data-ttu-id="4b3b6-356">This activity updates the change tracking version in the **table_store_ChangeTracking_version** table.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-356">This activity updates the change tracking version in the **table_store_ChangeTracking_version** table.</span></span>

    ![Stored Procedure Activity - name](./media/tutorial-incremental-copy-change-tracking-feature-portal/stored-procedure-activity-name.png)
12. <span data-ttu-id="4b3b6-358">Switch to the *SQL Account*\* tab, and select **AzureSqlDatabaseLinkedService** for **Linked service**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-358">Switch to the *SQL Account*\* tab, and select **AzureSqlDatabaseLinkedService** for **Linked service**.</span></span> 

    ![Stored Procedure Activity - SQL Account](./media/tutorial-incremental-copy-change-tracking-feature-portal/sql-account-tab.png)
13. <span data-ttu-id="4b3b6-360">Switch to the **Stored Procedure** tab, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="4b3b6-360">Switch to the **Stored Procedure** tab, and do the following steps:</span></span> 

    1. <span data-ttu-id="4b3b6-361">For **Stored procedure name**, select **Update_ChangeTracking_Version**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-361">For **Stored procedure name**, select **Update_ChangeTracking_Version**.</span></span>  
    2. <span data-ttu-id="4b3b6-362">Select **Import parameter**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-362">Select **Import parameter**.</span></span> 
    3. <span data-ttu-id="4b3b6-363">In the **Stored procedure parameters** section, specify following values for the parameters:</span><span class="sxs-lookup"><span data-stu-id="4b3b6-363">In the **Stored procedure parameters** section, specify following values for the parameters:</span></span> 

        | <span data-ttu-id="4b3b6-364">Name</span><span class="sxs-lookup"><span data-stu-id="4b3b6-364">Name</span></span> | <span data-ttu-id="4b3b6-365">Type</span><span class="sxs-lookup"><span data-stu-id="4b3b6-365">Type</span></span> | <span data-ttu-id="4b3b6-366">Value</span><span class="sxs-lookup"><span data-stu-id="4b3b6-366">Value</span></span> | 
        | ---- | ---- | ----- | 
        | <span data-ttu-id="4b3b6-367">CurrentTrackingVersion</span><span class="sxs-lookup"><span data-stu-id="4b3b6-367">CurrentTrackingVersion</span></span> | <span data-ttu-id="4b3b6-368">Int64</span><span class="sxs-lookup"><span data-stu-id="4b3b6-368">Int64</span></span> | <span data-ttu-id="4b3b6-369">@{activity('LookupCurrentChangeTrackingVersionActivity').output.firstRow.CurrentChangeTrackingVersion}</span><span class="sxs-lookup"><span data-stu-id="4b3b6-369">@{activity('LookupCurrentChangeTrackingVersionActivity').output.firstRow.CurrentChangeTrackingVersion}</span></span> | 
        | <span data-ttu-id="4b3b6-370">TableName</span><span class="sxs-lookup"><span data-stu-id="4b3b6-370">TableName</span></span> | <span data-ttu-id="4b3b6-371">String</span><span class="sxs-lookup"><span data-stu-id="4b3b6-371">String</span></span> | <span data-ttu-id="4b3b6-372">@{activity('LookupLastChangeTrackingVersionActivity').output.firstRow.TableName}</span><span class="sxs-lookup"><span data-stu-id="4b3b6-372">@{activity('LookupLastChangeTrackingVersionActivity').output.firstRow.TableName}</span></span> | 
    
        ![Stored Procedure Activity - Parameters](./media/tutorial-incremental-copy-change-tracking-feature-portal/stored-procedure-parameters.png)
14. <span data-ttu-id="4b3b6-374">**Connect the Copy activity to the Stored Procedure Activity**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-374">**Connect the Copy activity to the Stored Procedure Activity**.</span></span> <span data-ttu-id="4b3b6-375">Drag-and-drop the **green** button attached to the Copy activity to the Stored Procedure activity.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-375">Drag-and-drop the **green** button attached to the Copy activity to the Stored Procedure activity.</span></span> 

    ![Connect Copy and Stored Procedure activities](./media/tutorial-incremental-copy-change-tracking-feature-portal/connect-copy-stored-procedure.png)
15. <span data-ttu-id="4b3b6-377">Click **Validate** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-377">Click **Validate** on the toolbar.</span></span> <span data-ttu-id="4b3b6-378">Confirm that there are no validation errors.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-378">Confirm that there are no validation errors.</span></span> <span data-ttu-id="4b3b6-379">Close the **Pipeline Validation Report** window by clicking **>>**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-379">Close the **Pipeline Validation Report** window by clicking **>>**.</span></span> 

    ![Validate button](./media/tutorial-incremental-copy-change-tracking-feature-portal/validate-button.png)
16.  <span data-ttu-id="4b3b6-381">Publish entities (linked services, datasets, and pipelines) to the Data Factory service by clicking the **Publish All** button.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-381">Publish entities (linked services, datasets, and pipelines) to the Data Factory service by clicking the **Publish All** button.</span></span> <span data-ttu-id="4b3b6-382">Wait until you see the **Publishing succeeded** message.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-382">Wait until you see the **Publishing succeeded** message.</span></span> 

        ![Publish button](./media/tutorial-incremental-copy-change-tracking-feature-portal/publish-button-2.png)    

### <a name="run-the-incremental-copy-pipeline"></a><span data-ttu-id="4b3b6-384">Run the incremental copy pipeline</span><span class="sxs-lookup"><span data-stu-id="4b3b6-384">Run the incremental copy pipeline</span></span>
1. <span data-ttu-id="4b3b6-385">Click **Trigger** on the toolbar for the pipeline, and click **Trigger Now**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-385">Click **Trigger** on the toolbar for the pipeline, and click **Trigger Now**.</span></span> 

    ![Trigger Now menu](./media/tutorial-incremental-copy-change-tracking-feature-portal/trigger-now-menu-2.png)
2. <span data-ttu-id="4b3b6-387">In the **Pipeline Run** window, select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-387">In the **Pipeline Run** window, select **Finish**.</span></span>

### <a name="monitor-the-incremental-copy-pipeline"></a><span data-ttu-id="4b3b6-388">Monitor the incremental copy pipeline</span><span class="sxs-lookup"><span data-stu-id="4b3b6-388">Monitor the incremental copy pipeline</span></span>
1. <span data-ttu-id="4b3b6-389">Click the **Monitor** tab on the left.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-389">Click the **Monitor** tab on the left.</span></span> <span data-ttu-id="4b3b6-390">You see the pipeline run in the list and its status.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-390">You see the pipeline run in the list and its status.</span></span> <span data-ttu-id="4b3b6-391">To refresh the list, click **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-391">To refresh the list, click **Refresh**.</span></span> <span data-ttu-id="4b3b6-392">The links in the **Actions** column let you view activity runs associated with the pipeline run and to rerun the pipeline.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-392">The links in the **Actions** column let you view activity runs associated with the pipeline run and to rerun the pipeline.</span></span> 

    ![Pipeline runs](./media/tutorial-incremental-copy-change-tracking-feature-portal/inc-copy-pipeline-runs.png)
2. <span data-ttu-id="4b3b6-394">To view activity runs associated with the pipeline run, click the **View Activity Runs** link in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-394">To view activity runs associated with the pipeline run, click the **View Activity Runs** link in the **Actions** column.</span></span> <span data-ttu-id="4b3b6-395">There is only one activity in the pipeline, so you see only one entry in the list.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-395">There is only one activity in the pipeline, so you see only one entry in the list.</span></span> <span data-ttu-id="4b3b6-396">To switch back to the pipeline runs view, click **Pipelines** link at the top.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-396">To switch back to the pipeline runs view, click **Pipelines** link at the top.</span></span> 

    ![Activity runs](./media/tutorial-incremental-copy-change-tracking-feature-portal/inc-copy-activity-runs.png)


### <a name="review-the-results"></a><span data-ttu-id="4b3b6-398">Review the results</span><span class="sxs-lookup"><span data-stu-id="4b3b6-398">Review the results</span></span>
<span data-ttu-id="4b3b6-399">You see the second file in the `incchgtracking` folder of the `adftutorial` container.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-399">You see the second file in the `incchgtracking` folder of the `adftutorial` container.</span></span> 

![Output file from incremental copy](media\tutorial-incremental-copy-change-tracking-feature-portal\incremental-copy-output-file.png)

<span data-ttu-id="4b3b6-401">The file should have only the delta data from the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-401">The file should have only the delta data from the Azure SQL database.</span></span> <span data-ttu-id="4b3b6-402">The record with `U` is the updated row in the database and `I` is the one added row.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-402">The record with `U` is the updated row in the database and `I` is the one added row.</span></span> 

```
1,update,10,2,U
6,new,50,1,I
```
<span data-ttu-id="4b3b6-403">The first three columns are changed data from data_source_table.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-403">The first three columns are changed data from data_source_table.</span></span> <span data-ttu-id="4b3b6-404">The last two columns are the metadata from change tracking system table.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-404">The last two columns are the metadata from change tracking system table.</span></span> <span data-ttu-id="4b3b6-405">The fourth column is the SYS_CHANGE_VERSION for each changed row.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-405">The fourth column is the SYS_CHANGE_VERSION for each changed row.</span></span> <span data-ttu-id="4b3b6-406">The fifth column is the operation:  U = update, I = insert.</span><span class="sxs-lookup"><span data-stu-id="4b3b6-406">The fifth column is the operation:  U = update, I = insert.</span></span>  <span data-ttu-id="4b3b6-407">For details about the change tracking information, see [CHANGETABLE](/sql/relational-databases/system-functions/changetable-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="4b3b6-407">For details about the change tracking information, see [CHANGETABLE](/sql/relational-databases/system-functions/changetable-transact-sql).</span></span> 

```
==================================================================
PersonID Name    Age    SYS_CHANGE_VERSION    SYS_CHANGE_OPERATION
==================================================================
1        update  10     2                     U
6        new     50     1                     I
```

    
## <a name="next-steps"></a><span data-ttu-id="4b3b6-408">Next steps</span><span class="sxs-lookup"><span data-stu-id="4b3b6-408">Next steps</span></span>
<span data-ttu-id="4b3b6-409">Advance to the following tutorial to learn about transforming data by using a Spark cluster on Azure:</span><span class="sxs-lookup"><span data-stu-id="4b3b6-409">Advance to the following tutorial to learn about transforming data by using a Spark cluster on Azure:</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="4b3b6-410">Transform data using Spark cluster in cloud</span><span class="sxs-lookup"><span data-stu-id="4b3b6-410">Transform data using Spark cluster in cloud</span></span>](tutorial-transform-data-spark-portal.md)



