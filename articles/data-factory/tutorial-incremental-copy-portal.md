---
title: Incrementally copy a table by using Azure Data Factory | Microsoft Docs
description: In this tutorial, you create an Azure data factory pipeline that copies data incrementally from an Azure SQL database to Azure Blob storage.
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
ms.date: 01/11/2018
ms.author: yexu
ms.openlocfilehash: 342fdce9a0e9b47380a8d8c975703ebb7f57e3b6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868092"
---
# <a name="incrementally-load-data-from-an-azure-sql-database-to-azure-blob-storage"></a><span data-ttu-id="10f7b-103">Incrementally load data from an Azure SQL database to Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="10f7b-103">Incrementally load data from an Azure SQL database to Azure Blob storage</span></span>
<span data-ttu-id="10f7b-104">In this tutorial, you create an Azure data factory with a pipeline that loads delta data from a table in an Azure SQL database to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="10f7b-104">In this tutorial, you create an Azure data factory with a pipeline that loads delta data from a table in an Azure SQL database to Azure Blob storage.</span></span> 

<span data-ttu-id="10f7b-105">You perform the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="10f7b-105">You perform the following steps in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="10f7b-106">Prepare the data store to store the watermark value.</span><span class="sxs-lookup"><span data-stu-id="10f7b-106">Prepare the data store to store the watermark value.</span></span>
> * <span data-ttu-id="10f7b-107">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="10f7b-107">Create a data factory.</span></span>
> * <span data-ttu-id="10f7b-108">Create linked services.</span><span class="sxs-lookup"><span data-stu-id="10f7b-108">Create linked services.</span></span> 
> * <span data-ttu-id="10f7b-109">Create source, sink, and watermark datasets.</span><span class="sxs-lookup"><span data-stu-id="10f7b-109">Create source, sink, and watermark datasets.</span></span>
> * <span data-ttu-id="10f7b-110">Create a pipeline.</span><span class="sxs-lookup"><span data-stu-id="10f7b-110">Create a pipeline.</span></span>
> * <span data-ttu-id="10f7b-111">Run the pipeline.</span><span class="sxs-lookup"><span data-stu-id="10f7b-111">Run the pipeline.</span></span>
> * <span data-ttu-id="10f7b-112">Monitor the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="10f7b-112">Monitor the pipeline run.</span></span> 
> * <span data-ttu-id="10f7b-113">Review results</span><span class="sxs-lookup"><span data-stu-id="10f7b-113">Review results</span></span>
> * <span data-ttu-id="10f7b-114">Add more data to the source.</span><span class="sxs-lookup"><span data-stu-id="10f7b-114">Add more data to the source.</span></span>
> * <span data-ttu-id="10f7b-115">Run the pipeline again.</span><span class="sxs-lookup"><span data-stu-id="10f7b-115">Run the pipeline again.</span></span>
> * <span data-ttu-id="10f7b-116">Monitor the second pipeline run</span><span class="sxs-lookup"><span data-stu-id="10f7b-116">Monitor the second pipeline run</span></span>
> * <span data-ttu-id="10f7b-117">Review results from the second run</span><span class="sxs-lookup"><span data-stu-id="10f7b-117">Review results from the second run</span></span>


## <a name="overview"></a><span data-ttu-id="10f7b-118">Overview</span><span class="sxs-lookup"><span data-stu-id="10f7b-118">Overview</span></span>
<span data-ttu-id="10f7b-119">Here is the high-level solution diagram:</span><span class="sxs-lookup"><span data-stu-id="10f7b-119">Here is the high-level solution diagram:</span></span> 

![Incrementally load data](media\tutorial-Incremental-copy-portal\incrementally-load.png)

<span data-ttu-id="10f7b-121">Here are the important steps to create this solution:</span><span class="sxs-lookup"><span data-stu-id="10f7b-121">Here are the important steps to create this solution:</span></span> 

1. <span data-ttu-id="10f7b-122">**Select the watermark column**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-122">**Select the watermark column**.</span></span>
    <span data-ttu-id="10f7b-123">Select one column in the source data store, which can be used to slice the new or updated records for every run.</span><span class="sxs-lookup"><span data-stu-id="10f7b-123">Select one column in the source data store, which can be used to slice the new or updated records for every run.</span></span> <span data-ttu-id="10f7b-124">Normally, the data in this selected column (for example, last_modify_time or ID) keeps increasing when rows are created or updated.</span><span class="sxs-lookup"><span data-stu-id="10f7b-124">Normally, the data in this selected column (for example, last_modify_time or ID) keeps increasing when rows are created or updated.</span></span> <span data-ttu-id="10f7b-125">The maximum value in this column is used as a watermark.</span><span class="sxs-lookup"><span data-stu-id="10f7b-125">The maximum value in this column is used as a watermark.</span></span>

2. <span data-ttu-id="10f7b-126">**Prepare a data store to store the watermark value**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-126">**Prepare a data store to store the watermark value**.</span></span> <span data-ttu-id="10f7b-127">In this tutorial, you store the watermark value in a SQL database.</span><span class="sxs-lookup"><span data-stu-id="10f7b-127">In this tutorial, you store the watermark value in a SQL database.</span></span>
    
3. <span data-ttu-id="10f7b-128">**Create a pipeline with the following workflow**:</span><span class="sxs-lookup"><span data-stu-id="10f7b-128">**Create a pipeline with the following workflow**:</span></span> 
    
    <span data-ttu-id="10f7b-129">The pipeline in this solution has the following activities:</span><span class="sxs-lookup"><span data-stu-id="10f7b-129">The pipeline in this solution has the following activities:</span></span>
  
    * <span data-ttu-id="10f7b-130">Create two Lookup activities.</span><span class="sxs-lookup"><span data-stu-id="10f7b-130">Create two Lookup activities.</span></span> <span data-ttu-id="10f7b-131">Use the first Lookup activity to retrieve the last watermark value.</span><span class="sxs-lookup"><span data-stu-id="10f7b-131">Use the first Lookup activity to retrieve the last watermark value.</span></span> <span data-ttu-id="10f7b-132">Use the second Lookup activity to retrieve the new watermark value.</span><span class="sxs-lookup"><span data-stu-id="10f7b-132">Use the second Lookup activity to retrieve the new watermark value.</span></span> <span data-ttu-id="10f7b-133">These watermark values are passed to the Copy activity.</span><span class="sxs-lookup"><span data-stu-id="10f7b-133">These watermark values are passed to the Copy activity.</span></span> 
    * <span data-ttu-id="10f7b-134">Create a Copy activity that copies rows from the source data store with the value of the watermark column greater than the old watermark value and less than the new watermark value.</span><span class="sxs-lookup"><span data-stu-id="10f7b-134">Create a Copy activity that copies rows from the source data store with the value of the watermark column greater than the old watermark value and less than the new watermark value.</span></span> <span data-ttu-id="10f7b-135">Then, it copies the delta data from the source data store to Blob storage as a new file.</span><span class="sxs-lookup"><span data-stu-id="10f7b-135">Then, it copies the delta data from the source data store to Blob storage as a new file.</span></span> 
    * <span data-ttu-id="10f7b-136">Create a StoredProcedure activity that updates the watermark value for the pipeline that runs next time.</span><span class="sxs-lookup"><span data-stu-id="10f7b-136">Create a StoredProcedure activity that updates the watermark value for the pipeline that runs next time.</span></span> 


<span data-ttu-id="10f7b-137">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="10f7b-137">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10f7b-138">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="10f7b-138">Prerequisites</span></span>
* <span data-ttu-id="10f7b-139">**Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-139">**Azure SQL Database**.</span></span> <span data-ttu-id="10f7b-140">You use the database as the source data store.</span><span class="sxs-lookup"><span data-stu-id="10f7b-140">You use the database as the source data store.</span></span> <span data-ttu-id="10f7b-141">If you don't have a SQL database, see [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="10f7b-141">If you don't have a SQL database, see [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) for steps to create one.</span></span>
* <span data-ttu-id="10f7b-142">**Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-142">**Azure Storage**.</span></span> <span data-ttu-id="10f7b-143">You use the blob storage as the sink data store.</span><span class="sxs-lookup"><span data-stu-id="10f7b-143">You use the blob storage as the sink data store.</span></span> <span data-ttu-id="10f7b-144">If you don't have a storage account, see [Create a storage account](../storage/common/storage-quickstart-create-account.md) for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="10f7b-144">If you don't have a storage account, see [Create a storage account](../storage/common/storage-quickstart-create-account.md) for steps to create one.</span></span> <span data-ttu-id="10f7b-145">Create a container named adftutorial.</span><span class="sxs-lookup"><span data-stu-id="10f7b-145">Create a container named adftutorial.</span></span> 

### <a name="create-a-data-source-table-in-your-sql-database"></a><span data-ttu-id="10f7b-146">Create a data source table in your SQL database</span><span class="sxs-lookup"><span data-stu-id="10f7b-146">Create a data source table in your SQL database</span></span>
1. <span data-ttu-id="10f7b-147">Open SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="10f7b-147">Open SQL Server Management Studio.</span></span> <span data-ttu-id="10f7b-148">In **Server Explorer**, right-click the database, and choose **New Query**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-148">In **Server Explorer**, right-click the database, and choose **New Query**.</span></span>

2. <span data-ttu-id="10f7b-149">Run the following SQL command against your SQL database to create a table named `data_source_table` as the data source store:</span><span class="sxs-lookup"><span data-stu-id="10f7b-149">Run the following SQL command against your SQL database to create a table named `data_source_table` as the data source store:</span></span> 
    
    ```sql
    create table data_source_table
    (
        PersonID int,
        Name varchar(255),
        LastModifytime datetime
    );

    INSERT INTO data_source_table
    (PersonID, Name, LastModifytime)
    VALUES
    (1, 'aaaa','9/1/2017 12:56:00 AM'),
    (2, 'bbbb','9/2/2017 5:23:00 AM'),
    (3, 'cccc','9/3/2017 2:36:00 AM'),
    (4, 'dddd','9/4/2017 3:21:00 AM'),
    (5, 'eeee','9/5/2017 8:06:00 AM');
    ```
    <span data-ttu-id="10f7b-150">In this tutorial, you use LastModifytime as the watermark column.</span><span class="sxs-lookup"><span data-stu-id="10f7b-150">In this tutorial, you use LastModifytime as the watermark column.</span></span> <span data-ttu-id="10f7b-151">The data in the data source store is shown in the following table:</span><span class="sxs-lookup"><span data-stu-id="10f7b-151">The data in the data source store is shown in the following table:</span></span>

    ```
    PersonID | Name | LastModifytime
    -------- | ---- | --------------
    1 | aaaa | 2017-09-01 00:56:00.000
    2 | bbbb | 2017-09-02 05:23:00.000
    3 | cccc | 2017-09-03 02:36:00.000
    4 | dddd | 2017-09-04 03:21:00.000
    5 | eeee | 2017-09-05 08:06:00.000
    ```

### <a name="create-another-table-in-your-sql-database-to-store-the-high-watermark-value"></a><span data-ttu-id="10f7b-152">Create another table in your SQL database to store the high watermark value</span><span class="sxs-lookup"><span data-stu-id="10f7b-152">Create another table in your SQL database to store the high watermark value</span></span>
1. <span data-ttu-id="10f7b-153">Run the following SQL command against your SQL database to create a table named `watermarktable` to store the watermark value:</span><span class="sxs-lookup"><span data-stu-id="10f7b-153">Run the following SQL command against your SQL database to create a table named `watermarktable` to store the watermark value:</span></span>  
    
    ```sql
    create table watermarktable
    (
    
    TableName varchar(255),
    WatermarkValue datetime,
    );
    ```
2. <span data-ttu-id="10f7b-154">Set the default value of the high watermark with the table name of source data store.</span><span class="sxs-lookup"><span data-stu-id="10f7b-154">Set the default value of the high watermark with the table name of source data store.</span></span> <span data-ttu-id="10f7b-155">In this tutorial, the table name is data_source_table.</span><span class="sxs-lookup"><span data-stu-id="10f7b-155">In this tutorial, the table name is data_source_table.</span></span>

    ```sql
    INSERT INTO watermarktable
    VALUES ('data_source_table','1/1/2010 12:00:00 AM')    
    ```
3. <span data-ttu-id="10f7b-156">Review the data in the table `watermarktable`.</span><span class="sxs-lookup"><span data-stu-id="10f7b-156">Review the data in the table `watermarktable`.</span></span>
    
    ```sql
    Select * from watermarktable
    ```
    <span data-ttu-id="10f7b-157">Output:</span><span class="sxs-lookup"><span data-stu-id="10f7b-157">Output:</span></span> 

    ```
    TableName  | WatermarkValue
    ----------  | --------------
    data_source_table | 2010-01-01 00:00:00.000
    ```

### <a name="create-a-stored-procedure-in-your-sql-database"></a><span data-ttu-id="10f7b-158">Create a stored procedure in your SQL database</span><span class="sxs-lookup"><span data-stu-id="10f7b-158">Create a stored procedure in your SQL database</span></span> 

<span data-ttu-id="10f7b-159">Run the following command to create a stored procedure in your SQL database:</span><span class="sxs-lookup"><span data-stu-id="10f7b-159">Run the following command to create a stored procedure in your SQL database:</span></span>

```sql
CREATE PROCEDURE sp_write_watermark @LastModifiedtime datetime, @TableName varchar(50)
AS

BEGIN
    
    UPDATE watermarktable
    SET [WatermarkValue] = @LastModifiedtime 
WHERE [TableName] = @TableName
    
END
```

## <a name="create-a-data-factory"></a><span data-ttu-id="10f7b-160">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="10f7b-160">Create a data factory</span></span>

1. <span data-ttu-id="10f7b-161">Launch **Microsoft Edge** or **Google Chrome** web browser.</span><span class="sxs-lookup"><span data-stu-id="10f7b-161">Launch **Microsoft Edge** or **Google Chrome** web browser.</span></span> <span data-ttu-id="10f7b-162">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span><span class="sxs-lookup"><span data-stu-id="10f7b-162">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span></span>
1. <span data-ttu-id="10f7b-163">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-163">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span> 
   
   ![New->DataFactory](./media/tutorial-incremental-copy-portal/new-azure-data-factory-menu.png)
2. <span data-ttu-id="10f7b-165">In the **New data factory** page, enter **ADFIncCopyTutorialDF** for the **name**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-165">In the **New data factory** page, enter **ADFIncCopyTutorialDF** for the **name**.</span></span> 
      
     ![New data factory page](./media/tutorial-incremental-copy-portal/new-azure-data-factory.png)
 
   <span data-ttu-id="10f7b-167">The name of the Azure data factory must be **globally unique**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-167">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="10f7b-168">If you see a red exclamation mark with the following error, change the name of the data factory (for example, yournameADFIncCopyTutorialDF) and try creating again.</span><span class="sxs-lookup"><span data-stu-id="10f7b-168">If you see a red exclamation mark with the following error, change the name of the data factory (for example, yournameADFIncCopyTutorialDF) and try creating again.</span></span> <span data-ttu-id="10f7b-169">See [Data Factory - Naming Rules](naming-rules.md) article for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="10f7b-169">See [Data Factory - Naming Rules](naming-rules.md) article for naming rules for Data Factory artifacts.</span></span>
  
       `Data factory name "ADFIncCopyTutorialDF" is not available`
3. <span data-ttu-id="10f7b-170">Select your Azure **subscription** in which you want to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="10f7b-170">Select your Azure **subscription** in which you want to create the data factory.</span></span> 
4. <span data-ttu-id="10f7b-171">For the **Resource Group**, do one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="10f7b-171">For the **Resource Group**, do one of the following steps:</span></span>
     
      - <span data-ttu-id="10f7b-172">Select **Use existing**, and select an existing resource group from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="10f7b-172">Select **Use existing**, and select an existing resource group from the drop-down list.</span></span> 
      - <span data-ttu-id="10f7b-173">Select **Create new**, and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="10f7b-173">Select **Create new**, and enter the name of a resource group.</span></span>   
         
        <span data-ttu-id="10f7b-174">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="10f7b-174">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>  
4. <span data-ttu-id="10f7b-175">Select **V2** for the **version**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-175">Select **V2** for the **version**.</span></span>
5. <span data-ttu-id="10f7b-176">Select the **location** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="10f7b-176">Select the **location** for the data factory.</span></span> <span data-ttu-id="10f7b-177">Only locations that are supported are displayed in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="10f7b-177">Only locations that are supported are displayed in the drop-down list.</span></span> <span data-ttu-id="10f7b-178">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="10f7b-178">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span></span>
6. <span data-ttu-id="10f7b-179">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-179">Select **Pin to dashboard**.</span></span>     
7. <span data-ttu-id="10f7b-180">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-180">Click **Create**.</span></span>      
8. <span data-ttu-id="10f7b-181">On the dashboard, you see the following tile with status: **Deploying data factory**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-181">On the dashboard, you see the following tile with status: **Deploying data factory**.</span></span> 

    ![deploying data factory tile](media/tutorial-incremental-copy-portal/deploying-data-factory.png)
9. <span data-ttu-id="10f7b-183">After the creation is complete, you see the **Data Factory** page as shown in the image.</span><span class="sxs-lookup"><span data-stu-id="10f7b-183">After the creation is complete, you see the **Data Factory** page as shown in the image.</span></span>
   
   ![Data factory home page](./media/tutorial-incremental-copy-portal/data-factory-home-page.png)
10. <span data-ttu-id="10f7b-185">Click **Author & Monitor** tile to launch the Azure Data Factory user interface (UI) in a separate tab.</span><span class="sxs-lookup"><span data-stu-id="10f7b-185">Click **Author & Monitor** tile to launch the Azure Data Factory user interface (UI) in a separate tab.</span></span>

## <a name="create-a-pipeline"></a><span data-ttu-id="10f7b-186">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="10f7b-186">Create a pipeline</span></span>
<span data-ttu-id="10f7b-187">In this tutorial, you create a pipeline with two Lookup activities, one Copy activity, and one StoredProcedure activity chained in one pipeline.</span><span class="sxs-lookup"><span data-stu-id="10f7b-187">In this tutorial, you create a pipeline with two Lookup activities, one Copy activity, and one StoredProcedure activity chained in one pipeline.</span></span> 

1. <span data-ttu-id="10f7b-188">In the **get started** page of Data Factory UI, click the **Create pipeline** tile.</span><span class="sxs-lookup"><span data-stu-id="10f7b-188">In the **get started** page of Data Factory UI, click the **Create pipeline** tile.</span></span> 

   ![Get started page of Data Factory UI](./media/tutorial-incremental-copy-portal/get-started-page.png)    
3. <span data-ttu-id="10f7b-190">In the **General** page of the **Properties** window for the pipeline, enter **IncrementalCopyPipeline** name.</span><span class="sxs-lookup"><span data-stu-id="10f7b-190">In the **General** page of the **Properties** window for the pipeline, enter **IncrementalCopyPipeline** name.</span></span> 

   ![Pipeline name](./media/tutorial-incremental-copy-portal/pipeline-name.png)
4. <span data-ttu-id="10f7b-192">Let's add the first lookup activity to get the old watermark value.</span><span class="sxs-lookup"><span data-stu-id="10f7b-192">Let's add the first lookup activity to get the old watermark value.</span></span> <span data-ttu-id="10f7b-193">In the **Activities** toolbox, expand **General**, and drag-drop the **Lookup** activity to the pipeline designer surface.</span><span class="sxs-lookup"><span data-stu-id="10f7b-193">In the **Activities** toolbox, expand **General**, and drag-drop the **Lookup** activity to the pipeline designer surface.</span></span> <span data-ttu-id="10f7b-194">Change the name of the activity to **LookupOldWaterMarkActivity**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-194">Change the name of the activity to **LookupOldWaterMarkActivity**.</span></span>

   ![First lookup activity - name](./media/tutorial-incremental-copy-portal/first-lookup-name.png)
5. <span data-ttu-id="10f7b-196">Switch to the **Settings** tab, and click **+ New** for **Source Dataset**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-196">Switch to the **Settings** tab, and click **+ New** for **Source Dataset**.</span></span> <span data-ttu-id="10f7b-197">In this step, you create a dataset to represent data in the **watermarktable**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-197">In this step, you create a dataset to represent data in the **watermarktable**.</span></span> <span data-ttu-id="10f7b-198">This table contains the old watermark that was used in the previous copy operation.</span><span class="sxs-lookup"><span data-stu-id="10f7b-198">This table contains the old watermark that was used in the previous copy operation.</span></span> 

   ![New dataset menu - old watermark](./media/tutorial-incremental-copy-portal/new-dataset-old-watermark.png)
6. <span data-ttu-id="10f7b-200">In the **New Dataset** window, select **Azure SQL Database**, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-200">In the **New Dataset** window, select **Azure SQL Database**, and click **Finish**.</span></span> <span data-ttu-id="10f7b-201">You see a new tab opened for the dataset.</span><span class="sxs-lookup"><span data-stu-id="10f7b-201">You see a new tab opened for the dataset.</span></span> 

   ![Select Azure SQL Database](./media/tutorial-incremental-copy-portal/select-azure-sql-database-old-watermark.png)
7. <span data-ttu-id="10f7b-203">In the properties window for the dataset, enter **WatermarkDataset** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-203">In the properties window for the dataset, enter **WatermarkDataset** for **Name**.</span></span>

   ![Watermark dataset - name](./media/tutorial-incremental-copy-portal/watermark-dataset-name.png)
8. <span data-ttu-id="10f7b-205">Switch to the **Connection** tab, and click **+ New** to make a connection (create a linked service) to your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="10f7b-205">Switch to the **Connection** tab, and click **+ New** to make a connection (create a linked service) to your Azure SQL database.</span></span> 

   ![New linked service button](./media/tutorial-incremental-copy-portal/watermark-dataset-new-connection-button.png)
9. <span data-ttu-id="10f7b-207">In the **New Linked Service** window, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="10f7b-207">In the **New Linked Service** window, do the following steps:</span></span>

    1. <span data-ttu-id="10f7b-208">Enter **AzureSqlDatabaseLinkedService** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-208">Enter **AzureSqlDatabaseLinkedService** for **Name**.</span></span> 
    2. <span data-ttu-id="10f7b-209">Select your Azure SQL server for **Server name**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-209">Select your Azure SQL server for **Server name**.</span></span>
    3. <span data-ttu-id="10f7b-210">Enter the **name of the user** to access for the Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="10f7b-210">Enter the **name of the user** to access for the Azure SQL server.</span></span> 
    4. <span data-ttu-id="10f7b-211">Enter the **password** for the user.</span><span class="sxs-lookup"><span data-stu-id="10f7b-211">Enter the **password** for the user.</span></span> 
    5. <span data-ttu-id="10f7b-212">To test connection to the Azure SQL database, click **Test connection**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-212">To test connection to the Azure SQL database, click **Test connection**.</span></span>
    6. <span data-ttu-id="10f7b-213">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-213">Click **Save**.</span></span>
    7. <span data-ttu-id="10f7b-214">In the **Connection** tab, confirm that **AzureSqlDatabaseLinkedService** is selected for **Linked service**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-214">In the **Connection** tab, confirm that **AzureSqlDatabaseLinkedService** is selected for **Linked service**.</span></span>
       
        ![New linked service window](./media/tutorial-incremental-copy-portal/azure-sql-linked-service-settings.png)
10. <span data-ttu-id="10f7b-216">Select **[dbo].[watermarktable]** for **Table**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-216">Select **[dbo].[watermarktable]** for **Table**.</span></span> <span data-ttu-id="10f7b-217">If you want to preview data in the table, click **Preview data**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-217">If you want to preview data in the table, click **Preview data**.</span></span>

    ![Watermark dataset - connection settings](./media/tutorial-incremental-copy-portal/watermark-dataset-connection-settings.png)
11. <span data-ttu-id="10f7b-219">Switch to the pipeline editor by clicking the pipeline tab at the top or by clicking the name of the pipeline in the tree view on the left.</span><span class="sxs-lookup"><span data-stu-id="10f7b-219">Switch to the pipeline editor by clicking the pipeline tab at the top or by clicking the name of the pipeline in the tree view on the left.</span></span> <span data-ttu-id="10f7b-220">In the properties window for the **Lookup** activity, confirm that **WatermarkDataset** is selected for the **Source Dataset** field.</span><span class="sxs-lookup"><span data-stu-id="10f7b-220">In the properties window for the **Lookup** activity, confirm that **WatermarkDataset** is selected for the **Source Dataset** field.</span></span> 

    ![Pipeline - old watermark dataset](./media/tutorial-incremental-copy-portal/pipeline-old-watermark-dataset-selected.png)
12. <span data-ttu-id="10f7b-222">In the **Activities** toolbox, expand **General**, and drag-drop another **Lookup** activity to the pipeline designer surface, and set the name to **LookupNewWaterMarkActivity** in the **General** tab of the properties window.</span><span class="sxs-lookup"><span data-stu-id="10f7b-222">In the **Activities** toolbox, expand **General**, and drag-drop another **Lookup** activity to the pipeline designer surface, and set the name to **LookupNewWaterMarkActivity** in the **General** tab of the properties window.</span></span> <span data-ttu-id="10f7b-223">This Lookup activity gets the new watermark value from the table with the source data to be copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="10f7b-223">This Lookup activity gets the new watermark value from the table with the source data to be copied to the destination.</span></span> 

    ![Second lookup activity - name](./media/tutorial-incremental-copy-portal/second-lookup-activity-name.png)
13. <span data-ttu-id="10f7b-225">In the properties window for the second **Lookup** activity, switch to the **Settings** tab, and click **New**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-225">In the properties window for the second **Lookup** activity, switch to the **Settings** tab, and click **New**.</span></span> <span data-ttu-id="10f7b-226">You create a dataset to point to the source table that contains the new watermark value (maximum value of LastModifyTime).</span><span class="sxs-lookup"><span data-stu-id="10f7b-226">You create a dataset to point to the source table that contains the new watermark value (maximum value of LastModifyTime).</span></span> 

    ![Second lookup activity - new dataset](./media/tutorial-incremental-copy-portal/second-lookup-activity-settings-new-button.png)
14. <span data-ttu-id="10f7b-228">In the **New Dataset** window, select **Azure SQL Database**, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-228">In the **New Dataset** window, select **Azure SQL Database**, and click **Finish**.</span></span> <span data-ttu-id="10f7b-229">You see a new tab opened for this dataset.</span><span class="sxs-lookup"><span data-stu-id="10f7b-229">You see a new tab opened for this dataset.</span></span> <span data-ttu-id="10f7b-230">You also see the dataset in the tree view.</span><span class="sxs-lookup"><span data-stu-id="10f7b-230">You also see the dataset in the tree view.</span></span> 
15. <span data-ttu-id="10f7b-231">In the **General** tab of the properties window, enter **SourceDataset** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-231">In the **General** tab of the properties window, enter **SourceDataset** for **Name**.</span></span> 

    ![Source dataset - name](./media/tutorial-incremental-copy-portal/source-dataset-name.png)
16. <span data-ttu-id="10f7b-233">Switch to the **Connection** tab, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="10f7b-233">Switch to the **Connection** tab, and do the following steps:</span></span> 

    1. <span data-ttu-id="10f7b-234">Select **AzureSqlDatabaseLinkedService** for **Linked service**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-234">Select **AzureSqlDatabaseLinkedService** for **Linked service**.</span></span>
    2. <span data-ttu-id="10f7b-235">Select **[dbo].[data_source_table]** for Table.</span><span class="sxs-lookup"><span data-stu-id="10f7b-235">Select **[dbo].[data_source_table]** for Table.</span></span> <span data-ttu-id="10f7b-236">You specify a query on this dataset later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="10f7b-236">You specify a query on this dataset later in the tutorial.</span></span> <span data-ttu-id="10f7b-237">The query takes the precedence over the table you specify in this step.</span><span class="sxs-lookup"><span data-stu-id="10f7b-237">The query takes the precedence over the table you specify in this step.</span></span> 

        ![Second lookup activity - new dataset](./media/tutorial-incremental-copy-portal/source-dataset-connection.png)
17. <span data-ttu-id="10f7b-239">Switch to the pipeline editor by clicking the pipeline tab at the top or by clicking the name of the pipeline in the tree view on the left.</span><span class="sxs-lookup"><span data-stu-id="10f7b-239">Switch to the pipeline editor by clicking the pipeline tab at the top or by clicking the name of the pipeline in the tree view on the left.</span></span> <span data-ttu-id="10f7b-240">In the properties window for the **Lookup** activity, confirm that **SourceDataset** is selected for the **Source Dataset** field.</span><span class="sxs-lookup"><span data-stu-id="10f7b-240">In the properties window for the **Lookup** activity, confirm that **SourceDataset** is selected for the **Source Dataset** field.</span></span> 
18. <span data-ttu-id="10f7b-241">Select **Query** for the **Use Query** field, and enter the following query: you are only selecting the maximum value of **LastModifytime** from the **data_source_table**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-241">Select **Query** for the **Use Query** field, and enter the following query: you are only selecting the maximum value of **LastModifytime** from the **data_source_table**.</span></span> <span data-ttu-id="10f7b-242">If you don't have this query, the dataset gets all the rows from the table as you specified the table name (data_source_table) in the dataset definition.</span><span class="sxs-lookup"><span data-stu-id="10f7b-242">If you don't have this query, the dataset gets all the rows from the table as you specified the table name (data_source_table) in the dataset definition.</span></span>

    ```sql
    select MAX(LastModifytime) as NewWatermarkvalue from data_source_table
    ```

    ![Second lookup activity - query](./media/tutorial-incremental-copy-portal/query-for-new-watermark.png)
19. <span data-ttu-id="10f7b-244">In the **Activities** toolbox, expand **DataFlow**, and drag-drop the **Copy** activity from the Activities toolbox, and set the name to **IncrementalCopyActivity**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-244">In the **Activities** toolbox, expand **DataFlow**, and drag-drop the **Copy** activity from the Activities toolbox, and set the name to **IncrementalCopyActivity**.</span></span> 

    ![Copy activity - name](./media/tutorial-incremental-copy-portal/copy-activity-name.png)
20. <span data-ttu-id="10f7b-246">**Connect both Lookup activities to the Copy activity** by dragging the **green button** attached to the Lookup activities to the Copy activity.</span><span class="sxs-lookup"><span data-stu-id="10f7b-246">**Connect both Lookup activities to the Copy activity** by dragging the **green button** attached to the Lookup activities to the Copy activity.</span></span> <span data-ttu-id="10f7b-247">Release the mouse button when you see the border color of the Copy activity changes to blue.</span><span class="sxs-lookup"><span data-stu-id="10f7b-247">Release the mouse button when you see the border color of the Copy activity changes to blue.</span></span> 

    ![Connection Lookup activities to Copy activity](./media/tutorial-incremental-copy-portal/connection-lookups-to-copy.png)
21. <span data-ttu-id="10f7b-249">Select the **Copy activity** and confirm that you see the properties for the activity in the **Properties** window.</span><span class="sxs-lookup"><span data-stu-id="10f7b-249">Select the **Copy activity** and confirm that you see the properties for the activity in the **Properties** window.</span></span> 

    ![Copy activity properties](./media/tutorial-incremental-copy-portal/back-to-copy-activity-properties.png)
22. <span data-ttu-id="10f7b-251">Switch to the **Source** tab in the **Properties** window, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="10f7b-251">Switch to the **Source** tab in the **Properties** window, and do the following steps:</span></span>

    1. <span data-ttu-id="10f7b-252">Select **SourceDataset** for the **Source Dataset** field.</span><span class="sxs-lookup"><span data-stu-id="10f7b-252">Select **SourceDataset** for the **Source Dataset** field.</span></span> 
    2. <span data-ttu-id="10f7b-253">Select **Query** for the **Use Query** field.</span><span class="sxs-lookup"><span data-stu-id="10f7b-253">Select **Query** for the **Use Query** field.</span></span> 
    3. <span data-ttu-id="10f7b-254">Enter the following SQL query for the **Query** field.</span><span class="sxs-lookup"><span data-stu-id="10f7b-254">Enter the following SQL query for the **Query** field.</span></span> 

        ```sql
        select * from data_source_table where LastModifytime > '@{activity('LookupOldWaterMarkActivity').output.firstRow.WatermarkValue}' and LastModifytime <= '@{activity('LookupNewWaterMarkActivity').output.firstRow.NewWatermarkvalue}'
        ```
    
        ![Copy activity - source](./media/tutorial-incremental-copy-portal/copy-activity-source.png)
23. <span data-ttu-id="10f7b-256">Switch to the **Sink** tab, and click **+ New** for the **Sink Dataset** field.</span><span class="sxs-lookup"><span data-stu-id="10f7b-256">Switch to the **Sink** tab, and click **+ New** for the **Sink Dataset** field.</span></span> 

    ![New Dataset button](./media/tutorial-incremental-copy-portal/new-sink-dataset-button.png)
24. <span data-ttu-id="10f7b-258">In this tutorial sink data store is of type Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="10f7b-258">In this tutorial sink data store is of type Azure Blob Storage.</span></span> <span data-ttu-id="10f7b-259">Therefore, select **Azure Blob Storage**, and click **Finish** in the **New Dataset** window.</span><span class="sxs-lookup"><span data-stu-id="10f7b-259">Therefore, select **Azure Blob Storage**, and click **Finish** in the **New Dataset** window.</span></span> 

    ![Select Azure Blob Storage](./media/tutorial-incremental-copy-portal/select-azure-blob-storage.png)
25. <span data-ttu-id="10f7b-261">In the **General** tab of the Properties window for the dataset, enter **SinkDataset** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-261">In the **General** tab of the Properties window for the dataset, enter **SinkDataset** for **Name**.</span></span> 

    ![Sink Dataset - name](./media/tutorial-incremental-copy-portal/sink-dataset-name.png)
26. <span data-ttu-id="10f7b-263">Switch to the **Connection** tab, and click **+ New**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-263">Switch to the **Connection** tab, and click **+ New**.</span></span> <span data-ttu-id="10f7b-264">In this step, you create a connection (linked service) to your **Azure Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-264">In this step, you create a connection (linked service) to your **Azure Blob storage**.</span></span>

    ![Sink Dataset - new connection](./media/tutorial-incremental-copy-portal/sink-dataset-new-connection.png)
26. <span data-ttu-id="10f7b-266">In the **New Linked Service** window, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="10f7b-266">In the **New Linked Service** window, do the following steps:</span></span> 

    1. <span data-ttu-id="10f7b-267">Enter **AzureStorageLinkedService** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-267">Enter **AzureStorageLinkedService** for **Name**.</span></span> 
    2. <span data-ttu-id="10f7b-268">Select your Azure Storage account for **Storage account name**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-268">Select your Azure Storage account for **Storage account name**.</span></span>
    3. <span data-ttu-id="10f7b-269">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-269">Click **Save**.</span></span> 

        ![Azure Storage Linked service - settings](./media/tutorial-incremental-copy-portal/azure-storage-linked-service-settings.png)
27. <span data-ttu-id="10f7b-271">In the **Connection** tab, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="10f7b-271">In the **Connection** tab, do the following steps:</span></span>

    1. <span data-ttu-id="10f7b-272">Confirm that **AzureStorageLinkedService** is selected for **Linked service**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-272">Confirm that **AzureStorageLinkedService** is selected for **Linked service**.</span></span> 
    2. <span data-ttu-id="10f7b-273">For the **folder** part of the **File path** field, enter **adftutorial/incrementalcopy**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-273">For the **folder** part of the **File path** field, enter **adftutorial/incrementalcopy**.</span></span> <span data-ttu-id="10f7b-274">**adftutorial** is the blob container name and **incrementalcopy** is the folder name.</span><span class="sxs-lookup"><span data-stu-id="10f7b-274">**adftutorial** is the blob container name and **incrementalcopy** is the folder name.</span></span> <span data-ttu-id="10f7b-275">This snippet assumes that you have a blob container named adftutorial in your blob storage.</span><span class="sxs-lookup"><span data-stu-id="10f7b-275">This snippet assumes that you have a blob container named adftutorial in your blob storage.</span></span> <span data-ttu-id="10f7b-276">Create the container if it doesn't exist, or set it to the name of an existing one.</span><span class="sxs-lookup"><span data-stu-id="10f7b-276">Create the container if it doesn't exist, or set it to the name of an existing one.</span></span> <span data-ttu-id="10f7b-277">Azure Data Factory automatically creates the output folder **incrementalcopy** if it does not exist.</span><span class="sxs-lookup"><span data-stu-id="10f7b-277">Azure Data Factory automatically creates the output folder **incrementalcopy** if it does not exist.</span></span> <span data-ttu-id="10f7b-278">You can also use the **Browse** button for the **File path** to navigate to a folder in a blob container.</span><span class="sxs-lookup"><span data-stu-id="10f7b-278">You can also use the **Browse** button for the **File path** to navigate to a folder in a blob container.</span></span> <span data-ttu-id="10f7b-279">.RunId, '.txt')\`.</span><span class="sxs-lookup"><span data-stu-id="10f7b-279">.RunId, '.txt')\`.</span></span>
    3. <span data-ttu-id="10f7b-280">Fir the **filename** part of the **File path** field, enter `@CONCAT('Incremental-', pipeline().RunId, '.txt')`.</span><span class="sxs-lookup"><span data-stu-id="10f7b-280">Fir the **filename** part of the **File path** field, enter `@CONCAT('Incremental-', pipeline().RunId, '.txt')`.</span></span> <span data-ttu-id="10f7b-281">The file name is dynamically generated by using the expression.</span><span class="sxs-lookup"><span data-stu-id="10f7b-281">The file name is dynamically generated by using the expression.</span></span> <span data-ttu-id="10f7b-282">Each pipeline run has a unique ID.</span><span class="sxs-lookup"><span data-stu-id="10f7b-282">Each pipeline run has a unique ID.</span></span> <span data-ttu-id="10f7b-283">The Copy activity uses the run ID to generate the file name.</span><span class="sxs-lookup"><span data-stu-id="10f7b-283">The Copy activity uses the run ID to generate the file name.</span></span> 

        ![Sink Dataset - connection settings](./media/tutorial-incremental-copy-portal/sink-dataset-connection-settings.png)
28. <span data-ttu-id="10f7b-285">Switch to the **pipeline** editor by clicking the pipeline tab at the top or by clicking the name of the pipeline in the tree view on the left.</span><span class="sxs-lookup"><span data-stu-id="10f7b-285">Switch to the **pipeline** editor by clicking the pipeline tab at the top or by clicking the name of the pipeline in the tree view on the left.</span></span> 
29. <span data-ttu-id="10f7b-286">In the **Activities** toolbox, expand **General**, and drag-drop the **Stored Procedure** activity from the **Activities** toolbox to the pipeline designer surface.</span><span class="sxs-lookup"><span data-stu-id="10f7b-286">In the **Activities** toolbox, expand **General**, and drag-drop the **Stored Procedure** activity from the **Activities** toolbox to the pipeline designer surface.</span></span> <span data-ttu-id="10f7b-287">**Connect** the green (Success) output of the **Copy** activity to the **Stored Procedure** activity.</span><span class="sxs-lookup"><span data-stu-id="10f7b-287">**Connect** the green (Success) output of the **Copy** activity to the **Stored Procedure** activity.</span></span> 
    
    ![Copy activity - source](./media/tutorial-incremental-copy-portal/connect-copy-to-stored-procedure-activity.png)
24. <span data-ttu-id="10f7b-289">Select **Stored Procedure Activity** in the pipeline designer, change its name to **StoredProceduretoWriteWatermarkActivity**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-289">Select **Stored Procedure Activity** in the pipeline designer, change its name to **StoredProceduretoWriteWatermarkActivity**.</span></span> 

    ![Stored Procedure Activity - name](./media/tutorial-incremental-copy-portal/stored-procedure-activity-name.png)
25. <span data-ttu-id="10f7b-291">Switch to the **SQL Account** tab, and select *AzureSqlDatabaseLinkedService*\* for **Linked service**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-291">Switch to the **SQL Account** tab, and select *AzureSqlDatabaseLinkedService*\* for **Linked service**.</span></span> 

    ![Stored Procedure Activity - SQL Account](./media/tutorial-incremental-copy-portal/sp-activity-sql-account-settings.png)
26. <span data-ttu-id="10f7b-293">Switch to the **Stored Procedure** tab, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="10f7b-293">Switch to the **Stored Procedure** tab, and do the following steps:</span></span> 

    1. <span data-ttu-id="10f7b-294">For **Stored procedure name**, select **sp_write_watermark**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-294">For **Stored procedure name**, select **sp_write_watermark**.</span></span> 
    2. <span data-ttu-id="10f7b-295">To specify values for the stored procedure parameters, click **Import parameter**, and enter following values for the parameters:</span><span class="sxs-lookup"><span data-stu-id="10f7b-295">To specify values for the stored procedure parameters, click **Import parameter**, and enter following values for the parameters:</span></span> 

        | <span data-ttu-id="10f7b-296">Name</span><span class="sxs-lookup"><span data-stu-id="10f7b-296">Name</span></span> | <span data-ttu-id="10f7b-297">Type</span><span class="sxs-lookup"><span data-stu-id="10f7b-297">Type</span></span> | <span data-ttu-id="10f7b-298">Value</span><span class="sxs-lookup"><span data-stu-id="10f7b-298">Value</span></span> | 
        | ---- | ---- | ----- | 
        | <span data-ttu-id="10f7b-299">LastModifiedtime</span><span class="sxs-lookup"><span data-stu-id="10f7b-299">LastModifiedtime</span></span> | <span data-ttu-id="10f7b-300">DateTime</span><span class="sxs-lookup"><span data-stu-id="10f7b-300">DateTime</span></span> | <span data-ttu-id="10f7b-301">@{activity('LookupNewWaterMarkActivity').output.firstRow.NewWatermarkvalue}</span><span class="sxs-lookup"><span data-stu-id="10f7b-301">@{activity('LookupNewWaterMarkActivity').output.firstRow.NewWatermarkvalue}</span></span> |
        | <span data-ttu-id="10f7b-302">TableName</span><span class="sxs-lookup"><span data-stu-id="10f7b-302">TableName</span></span> | <span data-ttu-id="10f7b-303">String</span><span class="sxs-lookup"><span data-stu-id="10f7b-303">String</span></span> | <span data-ttu-id="10f7b-304">@{activity('LookupOldWaterMarkActivity').output.firstRow.TableName}</span><span class="sxs-lookup"><span data-stu-id="10f7b-304">@{activity('LookupOldWaterMarkActivity').output.firstRow.TableName}</span></span> |

    ![Stored Procedure Activity - stored procedure settings](./media/tutorial-incremental-copy-portal/sproc-activity-stored-procedure-settings.png)
27. <span data-ttu-id="10f7b-306">To validate the pipeline settings, click **Validate** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="10f7b-306">To validate the pipeline settings, click **Validate** on the toolbar.</span></span> <span data-ttu-id="10f7b-307">Confirm that there are no validation errors.</span><span class="sxs-lookup"><span data-stu-id="10f7b-307">Confirm that there are no validation errors.</span></span> <span data-ttu-id="10f7b-308">To close the **Pipeline Validation Report** window, click >>.</span><span class="sxs-lookup"><span data-stu-id="10f7b-308">To close the **Pipeline Validation Report** window, click >>.</span></span>   

    ![Validate pipeline](./media/tutorial-incremental-copy-portal/validate-pipeline.png)
28. <span data-ttu-id="10f7b-310">Publish entities (linked services, datasets, and pipelines) to the Azure Data Factory service by selecting the **Publish All** button.</span><span class="sxs-lookup"><span data-stu-id="10f7b-310">Publish entities (linked services, datasets, and pipelines) to the Azure Data Factory service by selecting the **Publish All** button.</span></span> <span data-ttu-id="10f7b-311">Wait until you see a message that the publishing succeeded.</span><span class="sxs-lookup"><span data-stu-id="10f7b-311">Wait until you see a message that the publishing succeeded.</span></span> 

    ![Publish button](./media/tutorial-incremental-copy-portal/publish-button.png)

## <a name="trigger-a-pipeline-run"></a><span data-ttu-id="10f7b-313">Trigger a pipeline run</span><span class="sxs-lookup"><span data-stu-id="10f7b-313">Trigger a pipeline run</span></span>
1. <span data-ttu-id="10f7b-314">Click **Trigger** on the toolbar, and click **Trigger Now**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-314">Click **Trigger** on the toolbar, and click **Trigger Now**.</span></span> 

    ![Trigger Now button](./media/tutorial-incremental-copy-portal/trigger-now.png)
2. <span data-ttu-id="10f7b-316">In the **Pipeline Run** window, select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-316">In the **Pipeline Run** window, select **Finish**.</span></span> 

## <a name="monitor-the-pipeline-run"></a><span data-ttu-id="10f7b-317">Monitor the pipeline run</span><span class="sxs-lookup"><span data-stu-id="10f7b-317">Monitor the pipeline run</span></span>

1. <span data-ttu-id="10f7b-318">Switch to the **Monitor** tab on the left.</span><span class="sxs-lookup"><span data-stu-id="10f7b-318">Switch to the **Monitor** tab on the left.</span></span> <span data-ttu-id="10f7b-319">You can see the status of the pipeline run triggered by the manual trigger.</span><span class="sxs-lookup"><span data-stu-id="10f7b-319">You can see the status of the pipeline run triggered by the manual trigger.</span></span> <span data-ttu-id="10f7b-320">Click **Refresh** button to refresh the list.</span><span class="sxs-lookup"><span data-stu-id="10f7b-320">Click **Refresh** button to refresh the list.</span></span> 
    
    ![Pipeline runs](./media/tutorial-incremental-copy-portal/pipeline-runs.png)
2. <span data-ttu-id="10f7b-322">To view activity runs associated with this pipeline run, click the first link (**View Activity Runs**) in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="10f7b-322">To view activity runs associated with this pipeline run, click the first link (**View Activity Runs**) in the **Actions** column.</span></span> <span data-ttu-id="10f7b-323">You can go back to the previous view by clicking **Pipelines** at the top.</span><span class="sxs-lookup"><span data-stu-id="10f7b-323">You can go back to the previous view by clicking **Pipelines** at the top.</span></span> <span data-ttu-id="10f7b-324">Click **Refresh** button to refresh the list.</span><span class="sxs-lookup"><span data-stu-id="10f7b-324">Click **Refresh** button to refresh the list.</span></span>

    ![Activity runs](./media/tutorial-incremental-copy-portal/activity-runs.png)

## <a name="review-the-results"></a><span data-ttu-id="10f7b-326">Review the results</span><span class="sxs-lookup"><span data-stu-id="10f7b-326">Review the results</span></span>
1. <span data-ttu-id="10f7b-327">Connect to your Azure Storage Account by using tools such as [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/).</span><span class="sxs-lookup"><span data-stu-id="10f7b-327">Connect to your Azure Storage Account by using tools such as [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/).</span></span> <span data-ttu-id="10f7b-328">Verify that an output file is created in the **incrementalcopy** folder of the **adftutorial** container.</span><span class="sxs-lookup"><span data-stu-id="10f7b-328">Verify that an output file is created in the **incrementalcopy** folder of the **adftutorial** container.</span></span>

    ![First output file](./media/tutorial-incremental-copy-portal/first-output-file.png)
2. <span data-ttu-id="10f7b-330">Open the output file and notice that all the data is copied from the **data_source_table** to the blob file.</span><span class="sxs-lookup"><span data-stu-id="10f7b-330">Open the output file and notice that all the data is copied from the **data_source_table** to the blob file.</span></span> 

    ```
    1,aaaa,2017-09-01 00:56:00.0000000
    2,bbbb,2017-09-02 05:23:00.0000000
    3,cccc,2017-09-03 02:36:00.0000000
    4,dddd,2017-09-04 03:21:00.0000000
    5,eeee,2017-09-05 08:06:00.0000000
    ```
3. <span data-ttu-id="10f7b-331">Check the latest value from `watermarktable`.</span><span class="sxs-lookup"><span data-stu-id="10f7b-331">Check the latest value from `watermarktable`.</span></span> <span data-ttu-id="10f7b-332">You see that the watermark value was updated.</span><span class="sxs-lookup"><span data-stu-id="10f7b-332">You see that the watermark value was updated.</span></span>

    ```sql
    Select * from watermarktable
    ```
    
    <span data-ttu-id="10f7b-333">Here is the output:</span><span class="sxs-lookup"><span data-stu-id="10f7b-333">Here is the output:</span></span>
 
    | <span data-ttu-id="10f7b-334">TableName</span><span class="sxs-lookup"><span data-stu-id="10f7b-334">TableName</span></span> | <span data-ttu-id="10f7b-335">WatermarkValue</span><span class="sxs-lookup"><span data-stu-id="10f7b-335">WatermarkValue</span></span> |
    | --------- | -------------- |
    | <span data-ttu-id="10f7b-336">data_source_table</span><span class="sxs-lookup"><span data-stu-id="10f7b-336">data_source_table</span></span> | <span data-ttu-id="10f7b-337">2017-09-05    8:06:00.000</span><span class="sxs-lookup"><span data-stu-id="10f7b-337">2017-09-05    8:06:00.000</span></span> | 

## <a name="add-more-data-to-source"></a><span data-ttu-id="10f7b-338">Add more data to source</span><span class="sxs-lookup"><span data-stu-id="10f7b-338">Add more data to source</span></span>

<span data-ttu-id="10f7b-339">Insert new data into the SQL database (data source store).</span><span class="sxs-lookup"><span data-stu-id="10f7b-339">Insert new data into the SQL database (data source store).</span></span>

```sql
INSERT INTO data_source_table
VALUES (6, 'newdata','9/6/2017 2:23:00 AM')

INSERT INTO data_source_table
VALUES (7, 'newdata','9/7/2017 9:01:00 AM')
``` 

<span data-ttu-id="10f7b-340">The updated data in the SQL database is:</span><span class="sxs-lookup"><span data-stu-id="10f7b-340">The updated data in the SQL database is:</span></span>

```
PersonID | Name | LastModifytime
-------- | ---- | --------------
1 | aaaa | 2017-09-01 00:56:00.000
2 | bbbb | 2017-09-02 05:23:00.000
3 | cccc | 2017-09-03 02:36:00.000
4 | dddd | 2017-09-04 03:21:00.000
5 | eeee | 2017-09-05 08:06:00.000
6 | newdata | 2017-09-06 02:23:00.000
7 | newdata | 2017-09-07 09:01:00.000
```


## <a name="trigger-another-pipeline-run"></a><span data-ttu-id="10f7b-341">Trigger another pipeline run</span><span class="sxs-lookup"><span data-stu-id="10f7b-341">Trigger another pipeline run</span></span>
1. <span data-ttu-id="10f7b-342">Switch to the **Edit** tab. Click the pipeline in the tree view if it's not opened in the designer.</span><span class="sxs-lookup"><span data-stu-id="10f7b-342">Switch to the **Edit** tab. Click the pipeline in the tree view if it's not opened in the designer.</span></span> 

    ![Trigger Now button](./media/tutorial-incremental-copy-portal/edit-tab.png)
2. <span data-ttu-id="10f7b-344">Click **Trigger** on the toolbar, and click **Trigger Now**.</span><span class="sxs-lookup"><span data-stu-id="10f7b-344">Click **Trigger** on the toolbar, and click **Trigger Now**.</span></span> 

    ![Trigger Now button](./media/tutorial-incremental-copy-portal/trigger-now.png)

## <a name="monitor-the-second-pipeline-run"></a><span data-ttu-id="10f7b-346">Monitor the second pipeline run</span><span class="sxs-lookup"><span data-stu-id="10f7b-346">Monitor the second pipeline run</span></span>

1. <span data-ttu-id="10f7b-347">Switch to the **Monitor** tab on the left.</span><span class="sxs-lookup"><span data-stu-id="10f7b-347">Switch to the **Monitor** tab on the left.</span></span> <span data-ttu-id="10f7b-348">You can see the status of the pipeline run triggered by the manual trigger.</span><span class="sxs-lookup"><span data-stu-id="10f7b-348">You can see the status of the pipeline run triggered by the manual trigger.</span></span> <span data-ttu-id="10f7b-349">Click **Refresh** button to refresh the list.</span><span class="sxs-lookup"><span data-stu-id="10f7b-349">Click **Refresh** button to refresh the list.</span></span> 
    
    ![Pipeline runs](./media/tutorial-incremental-copy-portal/pipeline-runs-2.png)
2. <span data-ttu-id="10f7b-351">To view activity runs associated with this pipeline run, click the first link (**View Activity Runs**) in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="10f7b-351">To view activity runs associated with this pipeline run, click the first link (**View Activity Runs**) in the **Actions** column.</span></span> <span data-ttu-id="10f7b-352">You can go back to the previous view by clicking **Pipelines** at the top.</span><span class="sxs-lookup"><span data-stu-id="10f7b-352">You can go back to the previous view by clicking **Pipelines** at the top.</span></span> <span data-ttu-id="10f7b-353">Click **Refresh** button to refresh the list.</span><span class="sxs-lookup"><span data-stu-id="10f7b-353">Click **Refresh** button to refresh the list.</span></span>

    ![Activity runs](./media/tutorial-incremental-copy-portal/activity-runs-2.png)

## <a name="verify-the-second-output"></a><span data-ttu-id="10f7b-355">Verify the second output</span><span class="sxs-lookup"><span data-stu-id="10f7b-355">Verify the second output</span></span>

1. <span data-ttu-id="10f7b-356">In the blob storage, you see that another file was created.</span><span class="sxs-lookup"><span data-stu-id="10f7b-356">In the blob storage, you see that another file was created.</span></span> <span data-ttu-id="10f7b-357">In this tutorial, the new file name is `Incremental-<GUID>.txt`.</span><span class="sxs-lookup"><span data-stu-id="10f7b-357">In this tutorial, the new file name is `Incremental-<GUID>.txt`.</span></span> <span data-ttu-id="10f7b-358">Open that file, and you see two rows of records in it.</span><span class="sxs-lookup"><span data-stu-id="10f7b-358">Open that file, and you see two rows of records in it.</span></span>

    ```
    6,newdata,2017-09-06 02:23:00.0000000
    7,newdata,2017-09-07 09:01:00.0000000    
    ```
2. <span data-ttu-id="10f7b-359">Check the latest value from `watermarktable`.</span><span class="sxs-lookup"><span data-stu-id="10f7b-359">Check the latest value from `watermarktable`.</span></span> <span data-ttu-id="10f7b-360">You see that the watermark value was updated again.</span><span class="sxs-lookup"><span data-stu-id="10f7b-360">You see that the watermark value was updated again.</span></span>

    ```sql
    Select * from watermarktable
    ```
    <span data-ttu-id="10f7b-361">sample output:</span><span class="sxs-lookup"><span data-stu-id="10f7b-361">sample output:</span></span> 
    
    | <span data-ttu-id="10f7b-362">TableName</span><span class="sxs-lookup"><span data-stu-id="10f7b-362">TableName</span></span> | <span data-ttu-id="10f7b-363">WatermarkValue</span><span class="sxs-lookup"><span data-stu-id="10f7b-363">WatermarkValue</span></span> |
    | --------- | --------------- |
    | <span data-ttu-id="10f7b-364">data_source_table</span><span class="sxs-lookup"><span data-stu-id="10f7b-364">data_source_table</span></span> | <span data-ttu-id="10f7b-365">2017-09-07 09:01:00.000</span><span class="sxs-lookup"><span data-stu-id="10f7b-365">2017-09-07 09:01:00.000</span></span> |


     
## <a name="next-steps"></a><span data-ttu-id="10f7b-366">Next steps</span><span class="sxs-lookup"><span data-stu-id="10f7b-366">Next steps</span></span>
<span data-ttu-id="10f7b-367">You performed the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="10f7b-367">You performed the following steps in this tutorial:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="10f7b-368">Prepare the data store to store the watermark value.</span><span class="sxs-lookup"><span data-stu-id="10f7b-368">Prepare the data store to store the watermark value.</span></span>
> * <span data-ttu-id="10f7b-369">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="10f7b-369">Create a data factory.</span></span>
> * <span data-ttu-id="10f7b-370">Create linked services.</span><span class="sxs-lookup"><span data-stu-id="10f7b-370">Create linked services.</span></span> 
> * <span data-ttu-id="10f7b-371">Create source, sink, and watermark datasets.</span><span class="sxs-lookup"><span data-stu-id="10f7b-371">Create source, sink, and watermark datasets.</span></span>
> * <span data-ttu-id="10f7b-372">Create a pipeline.</span><span class="sxs-lookup"><span data-stu-id="10f7b-372">Create a pipeline.</span></span>
> * <span data-ttu-id="10f7b-373">Run the pipeline.</span><span class="sxs-lookup"><span data-stu-id="10f7b-373">Run the pipeline.</span></span>
> * <span data-ttu-id="10f7b-374">Monitor the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="10f7b-374">Monitor the pipeline run.</span></span> 
> * <span data-ttu-id="10f7b-375">Review results</span><span class="sxs-lookup"><span data-stu-id="10f7b-375">Review results</span></span>
> * <span data-ttu-id="10f7b-376">Add more data to the source.</span><span class="sxs-lookup"><span data-stu-id="10f7b-376">Add more data to the source.</span></span>
> * <span data-ttu-id="10f7b-377">Run the pipeline again.</span><span class="sxs-lookup"><span data-stu-id="10f7b-377">Run the pipeline again.</span></span>
> * <span data-ttu-id="10f7b-378">Monitor the second pipeline run</span><span class="sxs-lookup"><span data-stu-id="10f7b-378">Monitor the second pipeline run</span></span>
> * <span data-ttu-id="10f7b-379">Review results from the second run</span><span class="sxs-lookup"><span data-stu-id="10f7b-379">Review results from the second run</span></span>

<span data-ttu-id="10f7b-380">In this tutorial, the pipeline copied data from a single table in a SQL database to Blob storage.</span><span class="sxs-lookup"><span data-stu-id="10f7b-380">In this tutorial, the pipeline copied data from a single table in a SQL database to Blob storage.</span></span> <span data-ttu-id="10f7b-381">Advance to the following tutorial to learn how to copy data from multiple tables in an on-premises SQL Server database to a SQL database.</span><span class="sxs-lookup"><span data-stu-id="10f7b-381">Advance to the following tutorial to learn how to copy data from multiple tables in an on-premises SQL Server database to a SQL database.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="10f7b-382">Incrementally load data from multiple tables in SQL Server to Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="10f7b-382">Incrementally load data from multiple tables in SQL Server to Azure SQL Database</span></span>](tutorial-incremental-copy-multiple-tables-portal.md)



