---
title: Incrementally copy multiple tables by using Azure Data Factory | Microsoft Docs
description: In this tutorial, you create an Azure Data Factory pipeline that copies delta data incrementally from multiple tables in an on-premises SQL Server database to an Azure SQL database.
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
ms.date: 01/20/2018
ms.author: yexu
ms.openlocfilehash: ea1e3ca76f779f442c9d22478ea93de3d5ab83f2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867825"
---
# <a name="incrementally-load-data-from-multiple-tables-in-sql-server-to-an-azure-sql-database"></a><span data-ttu-id="bde6f-103">Incrementally load data from multiple tables in SQL Server to an Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="bde6f-103">Incrementally load data from multiple tables in SQL Server to an Azure SQL database</span></span>
<span data-ttu-id="bde6f-104">In this tutorial, you create an Azure data factory with a pipeline that loads delta data from multiple tables in on-premises SQL Server to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="bde6f-104">In this tutorial, you create an Azure data factory with a pipeline that loads delta data from multiple tables in on-premises SQL Server to an Azure SQL database.</span></span>    

<span data-ttu-id="bde6f-105">You perform the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="bde6f-105">You perform the following steps in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bde6f-106">Prepare source and destination data stores.</span><span class="sxs-lookup"><span data-stu-id="bde6f-106">Prepare source and destination data stores.</span></span>
> * <span data-ttu-id="bde6f-107">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="bde6f-107">Create a data factory.</span></span>
> * <span data-ttu-id="bde6f-108">Create a self-hosted integration runtime.</span><span class="sxs-lookup"><span data-stu-id="bde6f-108">Create a self-hosted integration runtime.</span></span>
> * <span data-ttu-id="bde6f-109">Install the integration runtime.</span><span class="sxs-lookup"><span data-stu-id="bde6f-109">Install the integration runtime.</span></span> 
> * <span data-ttu-id="bde6f-110">Create linked services.</span><span class="sxs-lookup"><span data-stu-id="bde6f-110">Create linked services.</span></span> 
> * <span data-ttu-id="bde6f-111">Create source, sink, and watermark datasets.</span><span class="sxs-lookup"><span data-stu-id="bde6f-111">Create source, sink, and watermark datasets.</span></span>
> * <span data-ttu-id="bde6f-112">Create, run, and monitor a pipeline.</span><span class="sxs-lookup"><span data-stu-id="bde6f-112">Create, run, and monitor a pipeline.</span></span>
> * <span data-ttu-id="bde6f-113">Review the results.</span><span class="sxs-lookup"><span data-stu-id="bde6f-113">Review the results.</span></span>
> * <span data-ttu-id="bde6f-114">Add or update data in source tables.</span><span class="sxs-lookup"><span data-stu-id="bde6f-114">Add or update data in source tables.</span></span>
> * <span data-ttu-id="bde6f-115">Rerun and monitor the pipeline.</span><span class="sxs-lookup"><span data-stu-id="bde6f-115">Rerun and monitor the pipeline.</span></span>
> * <span data-ttu-id="bde6f-116">Review the final results.</span><span class="sxs-lookup"><span data-stu-id="bde6f-116">Review the final results.</span></span>

## <a name="overview"></a><span data-ttu-id="bde6f-117">Overview</span><span class="sxs-lookup"><span data-stu-id="bde6f-117">Overview</span></span>
<span data-ttu-id="bde6f-118">Here are the important steps to create this solution:</span><span class="sxs-lookup"><span data-stu-id="bde6f-118">Here are the important steps to create this solution:</span></span> 

1. <span data-ttu-id="bde6f-119">**Select the watermark column**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-119">**Select the watermark column**.</span></span>
    
    <span data-ttu-id="bde6f-120">Select one column for each table in the source data store, which can be used to identify the new or updated records for every run.</span><span class="sxs-lookup"><span data-stu-id="bde6f-120">Select one column for each table in the source data store, which can be used to identify the new or updated records for every run.</span></span> <span data-ttu-id="bde6f-121">Normally, the data in this selected column (for example, last_modify_time or ID) keeps increasing when rows are created or updated.</span><span class="sxs-lookup"><span data-stu-id="bde6f-121">Normally, the data in this selected column (for example, last_modify_time or ID) keeps increasing when rows are created or updated.</span></span> <span data-ttu-id="bde6f-122">The maximum value in this column is used as a watermark.</span><span class="sxs-lookup"><span data-stu-id="bde6f-122">The maximum value in this column is used as a watermark.</span></span>

1. <span data-ttu-id="bde6f-123">**Prepare a data store to store the watermark value**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-123">**Prepare a data store to store the watermark value**.</span></span>   
    
    <span data-ttu-id="bde6f-124">In this tutorial, you store the watermark value in a SQL database.</span><span class="sxs-lookup"><span data-stu-id="bde6f-124">In this tutorial, you store the watermark value in a SQL database.</span></span>

1. <span data-ttu-id="bde6f-125">**Create a pipeline with the following activities**:</span><span class="sxs-lookup"><span data-stu-id="bde6f-125">**Create a pipeline with the following activities**:</span></span> 
    
    <span data-ttu-id="bde6f-126">a.</span><span class="sxs-lookup"><span data-stu-id="bde6f-126">a.</span></span> <span data-ttu-id="bde6f-127">Create a ForEach activity that iterates through a list of source table names that is passed as a parameter to the pipeline.</span><span class="sxs-lookup"><span data-stu-id="bde6f-127">Create a ForEach activity that iterates through a list of source table names that is passed as a parameter to the pipeline.</span></span> <span data-ttu-id="bde6f-128">For each source table, it invokes the following activities to perform delta loading for that table.</span><span class="sxs-lookup"><span data-stu-id="bde6f-128">For each source table, it invokes the following activities to perform delta loading for that table.</span></span>

    <span data-ttu-id="bde6f-129">b.</span><span class="sxs-lookup"><span data-stu-id="bde6f-129">b.</span></span> <span data-ttu-id="bde6f-130">Create two lookup activities.</span><span class="sxs-lookup"><span data-stu-id="bde6f-130">Create two lookup activities.</span></span> <span data-ttu-id="bde6f-131">Use the first Lookup activity to retrieve the last watermark value.</span><span class="sxs-lookup"><span data-stu-id="bde6f-131">Use the first Lookup activity to retrieve the last watermark value.</span></span> <span data-ttu-id="bde6f-132">Use the second Lookup activity to retrieve the new watermark value.</span><span class="sxs-lookup"><span data-stu-id="bde6f-132">Use the second Lookup activity to retrieve the new watermark value.</span></span> <span data-ttu-id="bde6f-133">These watermark values are passed to the Copy activity.</span><span class="sxs-lookup"><span data-stu-id="bde6f-133">These watermark values are passed to the Copy activity.</span></span>

    <span data-ttu-id="bde6f-134">c.</span><span class="sxs-lookup"><span data-stu-id="bde6f-134">c.</span></span> <span data-ttu-id="bde6f-135">Create a Copy activity that copies rows from the source data store with the value of the watermark column greater than the old watermark value and less than the new watermark value.</span><span class="sxs-lookup"><span data-stu-id="bde6f-135">Create a Copy activity that copies rows from the source data store with the value of the watermark column greater than the old watermark value and less than the new watermark value.</span></span> <span data-ttu-id="bde6f-136">Then, it copies the delta data from the source data store to Azure Blob storage as a new file.</span><span class="sxs-lookup"><span data-stu-id="bde6f-136">Then, it copies the delta data from the source data store to Azure Blob storage as a new file.</span></span>

    <span data-ttu-id="bde6f-137">d.</span><span class="sxs-lookup"><span data-stu-id="bde6f-137">d.</span></span> <span data-ttu-id="bde6f-138">Create a StoredProcedure activity that updates the watermark value for the pipeline that runs next time.</span><span class="sxs-lookup"><span data-stu-id="bde6f-138">Create a StoredProcedure activity that updates the watermark value for the pipeline that runs next time.</span></span> 

    <span data-ttu-id="bde6f-139">Here is the high-level solution diagram:</span><span class="sxs-lookup"><span data-stu-id="bde6f-139">Here is the high-level solution diagram:</span></span> 

    ![Incrementally load data](media\tutorial-incremental-copy-multiple-tables-portal\high-level-solution-diagram.png)


<span data-ttu-id="bde6f-141">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="bde6f-141">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bde6f-142">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bde6f-142">Prerequisites</span></span>
* <span data-ttu-id="bde6f-143">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-143">**SQL Server**.</span></span> <span data-ttu-id="bde6f-144">You use an on-premises SQL Server database as the source data store in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="bde6f-144">You use an on-premises SQL Server database as the source data store in this tutorial.</span></span> 
* <span data-ttu-id="bde6f-145">**Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-145">**Azure SQL Database**.</span></span> <span data-ttu-id="bde6f-146">You use a SQL database as the sink data store.</span><span class="sxs-lookup"><span data-stu-id="bde6f-146">You use a SQL database as the sink data store.</span></span> <span data-ttu-id="bde6f-147">If you don't have a SQL database, see [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="bde6f-147">If you don't have a SQL database, see [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) for steps to create one.</span></span> 

### <a name="create-source-tables-in-your-sql-server-database"></a><span data-ttu-id="bde6f-148">Create source tables in your SQL Server database</span><span class="sxs-lookup"><span data-stu-id="bde6f-148">Create source tables in your SQL Server database</span></span>

1. <span data-ttu-id="bde6f-149">Open SQL Server Management Studio, and connect to your on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="bde6f-149">Open SQL Server Management Studio, and connect to your on-premises SQL Server database.</span></span>

1. <span data-ttu-id="bde6f-150">In **Server Explorer**, right-click the database and choose **New Query**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-150">In **Server Explorer**, right-click the database and choose **New Query**.</span></span>

1. <span data-ttu-id="bde6f-151">Run the following SQL command against your database to create tables named `customer_table` and `project_table`:</span><span class="sxs-lookup"><span data-stu-id="bde6f-151">Run the following SQL command against your database to create tables named `customer_table` and `project_table`:</span></span>

    ```sql
    create table customer_table
    (
        PersonID int,
        Name varchar(255),
        LastModifytime datetime
    );
    
    create table project_table
    (
        Project varchar(255),
        Creationtime datetime
    );
        
    INSERT INTO customer_table
    (PersonID, Name, LastModifytime)
    VALUES
    (1, 'John','9/1/2017 12:56:00 AM'),
    (2, 'Mike','9/2/2017 5:23:00 AM'),
    (3, 'Alice','9/3/2017 2:36:00 AM'),
    (4, 'Andy','9/4/2017 3:21:00 AM'),
    (5, 'Anny','9/5/2017 8:06:00 AM');
    
    INSERT INTO project_table
    (Project, Creationtime)
    VALUES
    ('project1','1/1/2015 0:00:00 AM'),
    ('project2','2/2/2016 1:23:00 AM'),
    ('project3','3/4/2017 5:16:00 AM');
    
    ```

### <a name="create-destination-tables-in-your-azure-sql-database"></a><span data-ttu-id="bde6f-152">Create destination tables in your Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="bde6f-152">Create destination tables in your Azure SQL database</span></span>
1. <span data-ttu-id="bde6f-153">Open SQL Server Management Studio, and connect to your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="bde6f-153">Open SQL Server Management Studio, and connect to your Azure SQL database.</span></span>

1. <span data-ttu-id="bde6f-154">In **Server Explorer**, right-click the database and choose **New Query**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-154">In **Server Explorer**, right-click the database and choose **New Query**.</span></span>

1. <span data-ttu-id="bde6f-155">Run the following SQL command against your SQL database to create tables named `customer_table` and `project_table`:</span><span class="sxs-lookup"><span data-stu-id="bde6f-155">Run the following SQL command against your SQL database to create tables named `customer_table` and `project_table`:</span></span>  
    
    ```sql
    create table customer_table
    (
        PersonID int,
        Name varchar(255),
        LastModifytime datetime
    );
    
    create table project_table
    (
        Project varchar(255),
        Creationtime datetime
    );

    ```

### <a name="create-another-table-in-the-azure-sql-database-to-store-the-high-watermark-value"></a><span data-ttu-id="bde6f-156">Create another table in the Azure SQL database to store the high watermark value</span><span class="sxs-lookup"><span data-stu-id="bde6f-156">Create another table in the Azure SQL database to store the high watermark value</span></span>
1. <span data-ttu-id="bde6f-157">Run the following SQL command against your SQL database to create a table named `watermarktable` to store the watermark value:</span><span class="sxs-lookup"><span data-stu-id="bde6f-157">Run the following SQL command against your SQL database to create a table named `watermarktable` to store the watermark value:</span></span> 
    
    ```sql
    create table watermarktable
    (
    
        TableName varchar(255),
        WatermarkValue datetime,
    );
    ```
1. <span data-ttu-id="bde6f-158">Insert initial watermark values for both source tables into the watermark table.</span><span class="sxs-lookup"><span data-stu-id="bde6f-158">Insert initial watermark values for both source tables into the watermark table.</span></span>

    ```sql

    INSERT INTO watermarktable
    VALUES 
    ('customer_table','1/1/2010 12:00:00 AM'),
    ('project_table','1/1/2010 12:00:00 AM');
    
    ```

### <a name="create-a-stored-procedure-in-the-azure-sql-database"></a><span data-ttu-id="bde6f-159">Create a stored procedure in the Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="bde6f-159">Create a stored procedure in the Azure SQL database</span></span> 

<span data-ttu-id="bde6f-160">Run the following command to create a stored procedure in your SQL database.</span><span class="sxs-lookup"><span data-stu-id="bde6f-160">Run the following command to create a stored procedure in your SQL database.</span></span> <span data-ttu-id="bde6f-161">This stored procedure updates the watermark value after every pipeline run.</span><span class="sxs-lookup"><span data-stu-id="bde6f-161">This stored procedure updates the watermark value after every pipeline run.</span></span> 

```sql
CREATE PROCEDURE sp_write_watermark @LastModifiedtime datetime, @TableName varchar(50)
AS

BEGIN

    UPDATE watermarktable
    SET [WatermarkValue] = @LastModifiedtime 
WHERE [TableName] = @TableName

END

```

### <a name="create-data-types-and-additional-stored-procedures-in-azure-sql-database"></a><span data-ttu-id="bde6f-162">Create data types and additional stored procedures in Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="bde6f-162">Create data types and additional stored procedures in Azure SQL database</span></span>
<span data-ttu-id="bde6f-163">Run the following query to create two stored procedures and two data types in your SQL database.</span><span class="sxs-lookup"><span data-stu-id="bde6f-163">Run the following query to create two stored procedures and two data types in your SQL database.</span></span> <span data-ttu-id="bde6f-164">They're used to merge the data from source tables into destination tables.</span><span class="sxs-lookup"><span data-stu-id="bde6f-164">They're used to merge the data from source tables into destination tables.</span></span>

```sql
CREATE TYPE DataTypeforCustomerTable AS TABLE(
    PersonID int,
    Name varchar(255),
    LastModifytime datetime
);

GO

CREATE PROCEDURE sp_upsert_customer_table @customer_table DataTypeforCustomerTable READONLY
AS

BEGIN
  MERGE customer_table AS target
  USING @customer_table AS source
  ON (target.PersonID = source.PersonID)
  WHEN MATCHED THEN
      UPDATE SET Name = source.Name,LastModifytime = source.LastModifytime
  WHEN NOT MATCHED THEN
      INSERT (PersonID, Name, LastModifytime)
      VALUES (source.PersonID, source.Name, source.LastModifytime);
END

GO

CREATE TYPE DataTypeforProjectTable AS TABLE(
    Project varchar(255),
    Creationtime datetime
);

GO

CREATE PROCEDURE sp_upsert_project_table @project_table DataTypeforProjectTable READONLY
AS

BEGIN
  MERGE project_table AS target
  USING @project_table AS source
  ON (target.Project = source.Project)
  WHEN MATCHED THEN
      UPDATE SET Creationtime = source.Creationtime
  WHEN NOT MATCHED THEN
      INSERT (Project, Creationtime)
      VALUES (source.Project, source.Creationtime);
END

```

## <a name="create-a-data-factory"></a><span data-ttu-id="bde6f-165">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="bde6f-165">Create a data factory</span></span>

1. <span data-ttu-id="bde6f-166">Launch **Microsoft Edge** or **Google Chrome** web browser.</span><span class="sxs-lookup"><span data-stu-id="bde6f-166">Launch **Microsoft Edge** or **Google Chrome** web browser.</span></span> <span data-ttu-id="bde6f-167">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span><span class="sxs-lookup"><span data-stu-id="bde6f-167">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span></span>
1. <span data-ttu-id="bde6f-168">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-168">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span> 
   
   ![New->DataFactory](./media/tutorial-incremental-copy-multiple-tables-portal/new-azure-data-factory-menu.png)
1. <span data-ttu-id="bde6f-170">In the **New data factory** page, enter **ADFMultiIncCopyTutorialDF** for the **name**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-170">In the **New data factory** page, enter **ADFMultiIncCopyTutorialDF** for the **name**.</span></span> 
      
     ![New data factory page](./media/tutorial-incremental-copy-multiple-tables-portal/new-azure-data-factory.png)
 
   <span data-ttu-id="bde6f-172">The name of the Azure data factory must be **globally unique**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-172">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="bde6f-173">If you receive the following error, change the name of the data factory (for example, yournameADFMultiIncCopyTutorialDF) and try creating again.</span><span class="sxs-lookup"><span data-stu-id="bde6f-173">If you receive the following error, change the name of the data factory (for example, yournameADFMultiIncCopyTutorialDF) and try creating again.</span></span> <span data-ttu-id="bde6f-174">See [Data Factory - Naming Rules](naming-rules.md) article for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="bde6f-174">See [Data Factory - Naming Rules](naming-rules.md) article for naming rules for Data Factory artifacts.</span></span>
  
       `Data factory name ADFMultiIncCopyTutorialDF is not available`
1. <span data-ttu-id="bde6f-175">Select your Azure **subscription** in which you want to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="bde6f-175">Select your Azure **subscription** in which you want to create the data factory.</span></span> 
1. <span data-ttu-id="bde6f-176">For the **Resource Group**, do one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="bde6f-176">For the **Resource Group**, do one of the following steps:</span></span>
     
      - <span data-ttu-id="bde6f-177">Select **Use existing**, and select an existing resource group from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="bde6f-177">Select **Use existing**, and select an existing resource group from the drop-down list.</span></span> 
      - <span data-ttu-id="bde6f-178">Select **Create new**, and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="bde6f-178">Select **Create new**, and enter the name of a resource group.</span></span>   
         
        <span data-ttu-id="bde6f-179">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bde6f-179">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>  
1. <span data-ttu-id="bde6f-180">Select **V2 (Preview)** for the **version**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-180">Select **V2 (Preview)** for the **version**.</span></span>
1. <span data-ttu-id="bde6f-181">Select the **location** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="bde6f-181">Select the **location** for the data factory.</span></span> <span data-ttu-id="bde6f-182">Only locations that are supported are displayed in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="bde6f-182">Only locations that are supported are displayed in the drop-down list.</span></span> <span data-ttu-id="bde6f-183">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="bde6f-183">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span></span>
1. <span data-ttu-id="bde6f-184">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-184">Select **Pin to dashboard**.</span></span>     
1. <span data-ttu-id="bde6f-185">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-185">Click **Create**.</span></span>      
1. <span data-ttu-id="bde6f-186">On the dashboard, you see the following tile with status: **Deploying data factory**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-186">On the dashboard, you see the following tile with status: **Deploying data factory**.</span></span> 

    ![deploying data factory tile](media/tutorial-incremental-copy-multiple-tables-portal/deploying-data-factory.png)
1. <span data-ttu-id="bde6f-188">After the creation is complete, you see the **Data Factory** page as shown in the image.</span><span class="sxs-lookup"><span data-stu-id="bde6f-188">After the creation is complete, you see the **Data Factory** page as shown in the image.</span></span>
   
   ![Data factory home page](./media/tutorial-incremental-copy-multiple-tables-portal/data-factory-home-page.png)
1. <span data-ttu-id="bde6f-190">Click **Author & Monitor** tile to launch Azure Data Factory user interface (UI) in a separate tab.</span><span class="sxs-lookup"><span data-stu-id="bde6f-190">Click **Author & Monitor** tile to launch Azure Data Factory user interface (UI) in a separate tab.</span></span>
1. <span data-ttu-id="bde6f-191">In the get started page of Azure Data Factory UI, click **Create pipeline** (or) switch to the **Edit** tab.</span><span class="sxs-lookup"><span data-stu-id="bde6f-191">In the get started page of Azure Data Factory UI, click **Create pipeline** (or) switch to the **Edit** tab.</span></span> 

   ![Get started page](./media/tutorial-incremental-copy-multiple-tables-portal/get-started-page.png)

## <a name="create-self-hosted-integration-runtime"></a><span data-ttu-id="bde6f-193">Create self-hosted integration runtime</span><span class="sxs-lookup"><span data-stu-id="bde6f-193">Create self-hosted integration runtime</span></span>
<span data-ttu-id="bde6f-194">As you are moving data from a data store in a private network (on-premises) to an Azure data store, install a self-hosted integration runtime (IR) in your on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="bde6f-194">As you are moving data from a data store in a private network (on-premises) to an Azure data store, install a self-hosted integration runtime (IR) in your on-premises environment.</span></span> <span data-ttu-id="bde6f-195">The self-hosted IR moves data between your private network and Azure.</span><span class="sxs-lookup"><span data-stu-id="bde6f-195">The self-hosted IR moves data between your private network and Azure.</span></span> 

1. <span data-ttu-id="bde6f-196">Click **Connections** at the bottom of the left pane, and switch to the **Integration Runtimes** in the **Connections** window.</span><span class="sxs-lookup"><span data-stu-id="bde6f-196">Click **Connections** at the bottom of the left pane, and switch to the **Integration Runtimes** in the **Connections** window.</span></span> 

   ![Connections tab](./media/tutorial-incremental-copy-multiple-tables-portal/connections-tab.png)
1. <span data-ttu-id="bde6f-198">In the **Integration Runtimes** tab, click **+ New**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-198">In the **Integration Runtimes** tab, click **+ New**.</span></span> 

   ![New integration runtime - button](./media/tutorial-incremental-copy-multiple-tables-portal/new-integration-runtime-button.png)
1. <span data-ttu-id="bde6f-200">In the **Integration Runtime Setup** window, select **Perform data movement and dispatch activities to external computes**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-200">In the **Integration Runtime Setup** window, select **Perform data movement and dispatch activities to external computes**, and click **Next**.</span></span> 

   ![Select integration runtime type](./media/tutorial-incremental-copy-multiple-tables-portal/select-integration-runtime-type.png)
1. <span data-ttu-id="bde6f-202">Select \*\* Private Network\*\*, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-202">Select \*\* Private Network\*\*, and click **Next**.</span></span> 

   ![Select private network](./media/tutorial-incremental-copy-multiple-tables-portal/select-private-network.png)
1. <span data-ttu-id="bde6f-204">Enter **MySelfHostedIR** for **Name**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-204">Enter **MySelfHostedIR** for **Name**, and click **Next**.</span></span> 

   ![Self-hosted IR name](./media/tutorial-incremental-copy-multiple-tables-portal/self-hosted-ir-name.png)
1. <span data-ttu-id="bde6f-206">Click **Click here to launch the express setup for this computer** in the **Option 1: Express setup** section.</span><span class="sxs-lookup"><span data-stu-id="bde6f-206">Click **Click here to launch the express setup for this computer** in the **Option 1: Express setup** section.</span></span> 

   ![Click Express setup link](./media/tutorial-incremental-copy-multiple-tables-portal/click-exress-setup.png)
1. <span data-ttu-id="bde6f-208">In the **Integration Runtime (Self-hosted) Express Setup** window, click **Close**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-208">In the **Integration Runtime (Self-hosted) Express Setup** window, click **Close**.</span></span> 

   ![Integration runtime setup - successful](./media/tutorial-incremental-copy-multiple-tables-portal/integration-runtime-setup-successful.png)
1. <span data-ttu-id="bde6f-210">In the Web browser, in the **Integration Runtime Setup** window, click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-210">In the Web browser, in the **Integration Runtime Setup** window, click **Finish**.</span></span> 

   ![Integration runtime setup - finish](./media/tutorial-incremental-copy-multiple-tables-portal/click-finish-integration-runtime-setup.png)
1. <span data-ttu-id="bde6f-212">Confirm that you see **MySelfHostedIR** in the list of integration runtimes.</span><span class="sxs-lookup"><span data-stu-id="bde6f-212">Confirm that you see **MySelfHostedIR** in the list of integration runtimes.</span></span>

       ![Integration runtimes - list](./media/tutorial-incremental-copy-multiple-tables-portal/integration-runtimes-list.png)

## <a name="create-linked-services"></a><span data-ttu-id="bde6f-213">Create linked services</span><span class="sxs-lookup"><span data-stu-id="bde6f-213">Create linked services</span></span>
<span data-ttu-id="bde6f-214">You create linked services in a data factory to link your data stores and compute services to the data factory.</span><span class="sxs-lookup"><span data-stu-id="bde6f-214">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="bde6f-215">In this section, you create linked services to your on-premises SQL Server database and SQL database.</span><span class="sxs-lookup"><span data-stu-id="bde6f-215">In this section, you create linked services to your on-premises SQL Server database and SQL database.</span></span> 

### <a name="create-the-sql-server-linked-service"></a><span data-ttu-id="bde6f-216">Create the SQL Server linked service</span><span class="sxs-lookup"><span data-stu-id="bde6f-216">Create the SQL Server linked service</span></span>
<span data-ttu-id="bde6f-217">In this step, you link your on-premises SQL Server database to the data factory.</span><span class="sxs-lookup"><span data-stu-id="bde6f-217">In this step, you link your on-premises SQL Server database to the data factory.</span></span>

1. <span data-ttu-id="bde6f-218">In the **Connections** window, switch from **Integration Runtimes** tab to the **Linked Services** tab, and click **+ New**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-218">In the **Connections** window, switch from **Integration Runtimes** tab to the **Linked Services** tab, and click **+ New**.</span></span>

    ![New Linked Service button](./media/tutorial-incremental-copy-multiple-tables-portal/new-sql-server-linked-service-button.png)
1. <span data-ttu-id="bde6f-220">In the **New Linked Service** window, select **SQL Server**, and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-220">In the **New Linked Service** window, select **SQL Server**, and click **Continue**.</span></span> 

    ![Select SQL Server](./media/tutorial-incremental-copy-multiple-tables-portal/select-sql-server.png)
1. <span data-ttu-id="bde6f-222">In the **New Linked Service** window, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="bde6f-222">In the **New Linked Service** window, do the following steps:</span></span>

    1. <span data-ttu-id="bde6f-223">Enter **SqlServerLinkedService** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-223">Enter **SqlServerLinkedService** for **Name**.</span></span> 
    1. <span data-ttu-id="bde6f-224">Select **MySelfHostedIR** for **Connect via integration runtime**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-224">Select **MySelfHostedIR** for **Connect via integration runtime**.</span></span> <span data-ttu-id="bde6f-225">This is an **important** step.</span><span class="sxs-lookup"><span data-stu-id="bde6f-225">This is an **important** step.</span></span> <span data-ttu-id="bde6f-226">The default integration runtime cannot connect to an on-premises data store.</span><span class="sxs-lookup"><span data-stu-id="bde6f-226">The default integration runtime cannot connect to an on-premises data store.</span></span> <span data-ttu-id="bde6f-227">Use the self-hosted integration runtime you created earlier.</span><span class="sxs-lookup"><span data-stu-id="bde6f-227">Use the self-hosted integration runtime you created earlier.</span></span> 
    1. <span data-ttu-id="bde6f-228">For **Server name**, enter the name of your computer that has the SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="bde6f-228">For **Server name**, enter the name of your computer that has the SQL Server database.</span></span>
    1. <span data-ttu-id="bde6f-229">For **Database name**, enter the name of the database in your SQL Server that has the source data.</span><span class="sxs-lookup"><span data-stu-id="bde6f-229">For **Database name**, enter the name of the database in your SQL Server that has the source data.</span></span> <span data-ttu-id="bde6f-230">You created a table and inserted data into this database as part of the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="bde6f-230">You created a table and inserted data into this database as part of the prerequisites.</span></span> 
    1. <span data-ttu-id="bde6f-231">For **Authentication type**, select the **type of the authentication** you want to use to connect to the database.</span><span class="sxs-lookup"><span data-stu-id="bde6f-231">For **Authentication type**, select the **type of the authentication** you want to use to connect to the database.</span></span> 
    1. <span data-ttu-id="bde6f-232">For **User name**, enter the name of user that has access to the SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="bde6f-232">For **User name**, enter the name of user that has access to the SQL Server database.</span></span> <span data-ttu-id="bde6f-233">If you need to use a slash character (`\`) in your user account or server name, use the escape character (`\`).</span><span class="sxs-lookup"><span data-stu-id="bde6f-233">If you need to use a slash character (`\`) in your user account or server name, use the escape character (`\`).</span></span> <span data-ttu-id="bde6f-234">An example is `mydomain\\myuser`.</span><span class="sxs-lookup"><span data-stu-id="bde6f-234">An example is `mydomain\\myuser`.</span></span>
    1. <span data-ttu-id="bde6f-235">For **Password**, enter the **password** for the user.</span><span class="sxs-lookup"><span data-stu-id="bde6f-235">For **Password**, enter the **password** for the user.</span></span> 
    1. <span data-ttu-id="bde6f-236">To test whether Data Factory can connect to your SQL Server database, click **Test connection**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-236">To test whether Data Factory can connect to your SQL Server database, click **Test connection**.</span></span> <span data-ttu-id="bde6f-237">Fix any errors until the connection succeeds.</span><span class="sxs-lookup"><span data-stu-id="bde6f-237">Fix any errors until the connection succeeds.</span></span> 
    1. <span data-ttu-id="bde6f-238">To save the linked service, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-238">To save the linked service, click **Save**.</span></span>

        ![SQL Server linked service - settings](./media/tutorial-incremental-copy-multiple-tables-portal/sql-server-linked-service-settings.png)

### <a name="create-the-azure-sql-database-linked-service"></a><span data-ttu-id="bde6f-240">Create the Azure SQL Database linked service</span><span class="sxs-lookup"><span data-stu-id="bde6f-240">Create the Azure SQL Database linked service</span></span>
<span data-ttu-id="bde6f-241">In the last step, you create a linked service to link your source SQL Server database to the data factory.</span><span class="sxs-lookup"><span data-stu-id="bde6f-241">In the last step, you create a linked service to link your source SQL Server database to the data factory.</span></span> <span data-ttu-id="bde6f-242">In this step, you link your destination/sink Azure SQL database to the data factory.</span><span class="sxs-lookup"><span data-stu-id="bde6f-242">In this step, you link your destination/sink Azure SQL database to the data factory.</span></span> 

1. <span data-ttu-id="bde6f-243">In the **Connections** window, switch from **Integration Runtimes** tab to the **Linked Services** tab, and click **+ New**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-243">In the **Connections** window, switch from **Integration Runtimes** tab to the **Linked Services** tab, and click **+ New**.</span></span>

    ![New Linked Service button](./media/tutorial-incremental-copy-multiple-tables-portal/new-sql-server-linked-service-button.png)
1. <span data-ttu-id="bde6f-245">In the **New Linked Service** window, select **Azure SQL Database**, and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-245">In the **New Linked Service** window, select **Azure SQL Database**, and click **Continue**.</span></span> 
1. <span data-ttu-id="bde6f-246">In the **New Linked Service** window, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="bde6f-246">In the **New Linked Service** window, do the following steps:</span></span>

    1. <span data-ttu-id="bde6f-247">Enter **AzureSqlDatabaseLinkedService** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-247">Enter **AzureSqlDatabaseLinkedService** for **Name**.</span></span> 
    1. <span data-ttu-id="bde6f-248">For **Server name**, select the name of your Azure SQL server from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="bde6f-248">For **Server name**, select the name of your Azure SQL server from the drop-down list.</span></span> 
    1. <span data-ttu-id="bde6f-249">For **Database name**, select the Azure SQL database in which you created customer_table and project_table as part of the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="bde6f-249">For **Database name**, select the Azure SQL database in which you created customer_table and project_table as part of the prerequisites.</span></span> 
    1. <span data-ttu-id="bde6f-250">For **User name**, enter the name of user that has access to the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="bde6f-250">For **User name**, enter the name of user that has access to the Azure SQL database.</span></span> 
    1. <span data-ttu-id="bde6f-251">For **Password**, enter the **password** for the user.</span><span class="sxs-lookup"><span data-stu-id="bde6f-251">For **Password**, enter the **password** for the user.</span></span> 
    1. <span data-ttu-id="bde6f-252">To test whether Data Factory can connect to your SQL Server database, click **Test connection**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-252">To test whether Data Factory can connect to your SQL Server database, click **Test connection**.</span></span> <span data-ttu-id="bde6f-253">Fix any errors until the connection succeeds.</span><span class="sxs-lookup"><span data-stu-id="bde6f-253">Fix any errors until the connection succeeds.</span></span> 
    1. <span data-ttu-id="bde6f-254">To save the linked service, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-254">To save the linked service, click **Save**.</span></span>

        ![Azure SQL linked service - settings](./media/tutorial-incremental-copy-multiple-tables-portal/azure-sql-linked-service-settings.png)
1. <span data-ttu-id="bde6f-256">Confirm that you see two linked services in the list.</span><span class="sxs-lookup"><span data-stu-id="bde6f-256">Confirm that you see two linked services in the list.</span></span> 
   
    ![Two linked services](./media/tutorial-incremental-copy-multiple-tables-portal/two-linked-services.png) 

## <a name="create-datasets"></a><span data-ttu-id="bde6f-258">Create datasets</span><span class="sxs-lookup"><span data-stu-id="bde6f-258">Create datasets</span></span>
<span data-ttu-id="bde6f-259">In this step, you create datasets to represent the data source, the data destination, and the place to store the watermark.</span><span class="sxs-lookup"><span data-stu-id="bde6f-259">In this step, you create datasets to represent the data source, the data destination, and the place to store the watermark.</span></span>

### <a name="create-a-source-dataset"></a><span data-ttu-id="bde6f-260">Create a source dataset</span><span class="sxs-lookup"><span data-stu-id="bde6f-260">Create a source dataset</span></span>

1. <span data-ttu-id="bde6f-261">In the left pane, click **+ (plus)**, and click **Dataset**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-261">In the left pane, click **+ (plus)**, and click **Dataset**.</span></span>

   ![New Dataset menu](./media/tutorial-incremental-copy-multiple-tables-portal/new-dataset-menu.png)
1. <span data-ttu-id="bde6f-263">In the **New Dataset** window, select **SQL Server**, click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-263">In the **New Dataset** window, select **SQL Server**, click **Finish**.</span></span> 

   ![Select SQL Server](./media/tutorial-incremental-copy-multiple-tables-portal/select-sql-server-for-dataset.png)
1. <span data-ttu-id="bde6f-265">You see a new tab opened in the Web browser for configuring the dataset.</span><span class="sxs-lookup"><span data-stu-id="bde6f-265">You see a new tab opened in the Web browser for configuring the dataset.</span></span> <span data-ttu-id="bde6f-266">You also see a dataset in the treeview.</span><span class="sxs-lookup"><span data-stu-id="bde6f-266">You also see a dataset in the treeview.</span></span> <span data-ttu-id="bde6f-267">In the **General** tab of the Properties window at the bottom, enter **SourceDataset** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-267">In the **General** tab of the Properties window at the bottom, enter **SourceDataset** for **Name**.</span></span> 

   ![Source dataset - name](./media/tutorial-incremental-copy-multiple-tables-portal/source-dataset-general.png)
1. <span data-ttu-id="bde6f-269">Switch to the **Connection** tab in the Properties window, and select **SqlServerLinkedService** for **Linked service**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-269">Switch to the **Connection** tab in the Properties window, and select **SqlServerLinkedService** for **Linked service**.</span></span> <span data-ttu-id="bde6f-270">You do not select a table here.</span><span class="sxs-lookup"><span data-stu-id="bde6f-270">You do not select a table here.</span></span> <span data-ttu-id="bde6f-271">The Copy activity in the pipeline uses a SQL query to load the data rather than load the entire table.</span><span class="sxs-lookup"><span data-stu-id="bde6f-271">The Copy activity in the pipeline uses a SQL query to load the data rather than load the entire table.</span></span>

   ![Source dataset - connection](./media/tutorial-incremental-copy-multiple-tables-portal/source-dataset-connection.png)


### <a name="create-a-sink-dataset"></a><span data-ttu-id="bde6f-273">Create a sink dataset</span><span class="sxs-lookup"><span data-stu-id="bde6f-273">Create a sink dataset</span></span>
1. <span data-ttu-id="bde6f-274">In the left pane, click **+ (plus)**, and click **Dataset**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-274">In the left pane, click **+ (plus)**, and click **Dataset**.</span></span>

   ![New Dataset menu](./media/tutorial-incremental-copy-multiple-tables-portal/new-dataset-menu.png)
1. <span data-ttu-id="bde6f-276">In the **New Dataset** window, select **Azure SQL Database**, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-276">In the **New Dataset** window, select **Azure SQL Database**, and click **Finish**.</span></span> 

   ![Select Azure SQL Database](./media/tutorial-incremental-copy-multiple-tables-portal/select-azure-sql-database.png)
1. <span data-ttu-id="bde6f-278">You see a new tab opened in the Web browser for configuring the dataset.</span><span class="sxs-lookup"><span data-stu-id="bde6f-278">You see a new tab opened in the Web browser for configuring the dataset.</span></span> <span data-ttu-id="bde6f-279">You also see a dataset in the treeview.</span><span class="sxs-lookup"><span data-stu-id="bde6f-279">You also see a dataset in the treeview.</span></span> <span data-ttu-id="bde6f-280">In the **General** tab of the Properties window at the bottom, enter **SinkDataset** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-280">In the **General** tab of the Properties window at the bottom, enter **SinkDataset** for **Name**.</span></span>

   ![Sink Dataset - general](./media/tutorial-incremental-copy-multiple-tables-portal/sink-dataset-general.png)
1. <span data-ttu-id="bde6f-282">Switch to the **Parameters** tab in the Properties window, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="bde6f-282">Switch to the **Parameters** tab in the Properties window, and do the following steps:</span></span> 

    1. <span data-ttu-id="bde6f-283">Click **New** in the **Create/update parameters** section.</span><span class="sxs-lookup"><span data-stu-id="bde6f-283">Click **New** in the **Create/update parameters** section.</span></span> 
    1. <span data-ttu-id="bde6f-284">Enter **SinkTableName** for the **name**, and **String** for the **type**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-284">Enter **SinkTableName** for the **name**, and **String** for the **type**.</span></span> <span data-ttu-id="bde6f-285">This dataset takes **SinkTableName** as a parameter.</span><span class="sxs-lookup"><span data-stu-id="bde6f-285">This dataset takes **SinkTableName** as a parameter.</span></span> <span data-ttu-id="bde6f-286">The SinkTableName parameter is set by the pipeline dynamically at runtime.</span><span class="sxs-lookup"><span data-stu-id="bde6f-286">The SinkTableName parameter is set by the pipeline dynamically at runtime.</span></span> <span data-ttu-id="bde6f-287">The ForEach activity in the pipeline iterates through a list of table names and passes the table name to this dataset in each iteration.</span><span class="sxs-lookup"><span data-stu-id="bde6f-287">The ForEach activity in the pipeline iterates through a list of table names and passes the table name to this dataset in each iteration.</span></span>
   
       ![Sink Dataset - properties](./media/tutorial-incremental-copy-multiple-tables-portal/sink-dataset-parameters.png)
1. <span data-ttu-id="bde6f-289">Switch to the **Connection** tab in the Properties window, and select **AzureSqlLinkedService** for **Linked service**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-289">Switch to the **Connection** tab in the Properties window, and select **AzureSqlLinkedService** for **Linked service**.</span></span> <span data-ttu-id="bde6f-290">For **Table** property, click **Add dynamic content**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-290">For **Table** property, click **Add dynamic content**.</span></span> 

   ![Sink Dataset - connection](./media/tutorial-incremental-copy-multiple-tables-portal/sink-dataset-connection.png)
    
    
1. <span data-ttu-id="bde6f-292">Select **SinkTableName** in the **Parameters** section</span><span class="sxs-lookup"><span data-stu-id="bde6f-292">Select **SinkTableName** in the **Parameters** section</span></span>
   
   ![Sink Dataset - connection](./media/tutorial-incremental-copy-multiple-tables-portal/sink-dataset-connection-dynamicContent.png)

   
 1. <span data-ttu-id="bde6f-294">After clicking **Finish**, you see **@dataset().SinkTableName** as the table name.</span><span class="sxs-lookup"><span data-stu-id="bde6f-294">After clicking **Finish**, you see **@dataset().SinkTableName** as the table name.</span></span>
   
   ![Sink Dataset - connection](./media/tutorial-incremental-copy-multiple-tables-portal/sink-dataset-connection-completion.png)

### <a name="create-a-dataset-for-a-watermark"></a><span data-ttu-id="bde6f-296">Create a dataset for a watermark</span><span class="sxs-lookup"><span data-stu-id="bde6f-296">Create a dataset for a watermark</span></span>
<span data-ttu-id="bde6f-297">In this step, you create a dataset for storing a high watermark value.</span><span class="sxs-lookup"><span data-stu-id="bde6f-297">In this step, you create a dataset for storing a high watermark value.</span></span> 

1. <span data-ttu-id="bde6f-298">In the left pane, click **+ (plus)**, and click **Dataset**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-298">In the left pane, click **+ (plus)**, and click **Dataset**.</span></span>

   ![New Dataset menu](./media/tutorial-incremental-copy-multiple-tables-portal/new-dataset-menu.png)
1. <span data-ttu-id="bde6f-300">In the **New Dataset** window, select **Azure SQL Database**, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-300">In the **New Dataset** window, select **Azure SQL Database**, and click **Finish**.</span></span> 

   ![Select Azure SQL Database](./media/tutorial-incremental-copy-multiple-tables-portal/select-azure-sql-database.png)
1. <span data-ttu-id="bde6f-302">In the **General** tab of the Properties window at the bottom, enter **WatermarkDataset** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-302">In the **General** tab of the Properties window at the bottom, enter **WatermarkDataset** for **Name**.</span></span>
1. <span data-ttu-id="bde6f-303">Switch to the **Connection** tab, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="bde6f-303">Switch to the **Connection** tab, and do the following steps:</span></span> 

    1. <span data-ttu-id="bde6f-304">Select **AzureSqlDatabaseLinkedService** for **Linked service**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-304">Select **AzureSqlDatabaseLinkedService** for **Linked service**.</span></span>
    1. <span data-ttu-id="bde6f-305">Select **[dbo].[watermarktable]** for **Table**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-305">Select **[dbo].[watermarktable]** for **Table**.</span></span>

       ![Watermark Dataset - connection](./media/tutorial-incremental-copy-multiple-tables-portal/watermark-dataset-connection.png)

## <a name="create-a-pipeline"></a><span data-ttu-id="bde6f-307">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="bde6f-307">Create a pipeline</span></span>
<span data-ttu-id="bde6f-308">The pipeline takes a list of table names as a parameter.</span><span class="sxs-lookup"><span data-stu-id="bde6f-308">The pipeline takes a list of table names as a parameter.</span></span> <span data-ttu-id="bde6f-309">The ForEach activity iterates through the list of table names and performs the following operations:</span><span class="sxs-lookup"><span data-stu-id="bde6f-309">The ForEach activity iterates through the list of table names and performs the following operations:</span></span> 

1. <span data-ttu-id="bde6f-310">Use the Lookup activity to retrieve the old watermark value (the initial value or the one that was used in the last iteration).</span><span class="sxs-lookup"><span data-stu-id="bde6f-310">Use the Lookup activity to retrieve the old watermark value (the initial value or the one that was used in the last iteration).</span></span>

1. <span data-ttu-id="bde6f-311">Use the Lookup activity to retrieve the new watermark value (the maximum value of the watermark column in the source table).</span><span class="sxs-lookup"><span data-stu-id="bde6f-311">Use the Lookup activity to retrieve the new watermark value (the maximum value of the watermark column in the source table).</span></span>

1. <span data-ttu-id="bde6f-312">Use the Copy activity to copy data between these two watermark values from the source database to the destination database.</span><span class="sxs-lookup"><span data-stu-id="bde6f-312">Use the Copy activity to copy data between these two watermark values from the source database to the destination database.</span></span>

1. <span data-ttu-id="bde6f-313">Use the StoredProcedure activity to update the old watermark value to be used in the first step of the next iteration.</span><span class="sxs-lookup"><span data-stu-id="bde6f-313">Use the StoredProcedure activity to update the old watermark value to be used in the first step of the next iteration.</span></span> 

### <a name="create-the-pipeline"></a><span data-ttu-id="bde6f-314">Create the pipeline</span><span class="sxs-lookup"><span data-stu-id="bde6f-314">Create the pipeline</span></span>

1. <span data-ttu-id="bde6f-315">In the left pane, click **+ (plus)**, and click **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-315">In the left pane, click **+ (plus)**, and click **Pipeline**.</span></span>

    ![New Pipeline - menu](./media/tutorial-incremental-copy-multiple-tables-portal/new-pipeline-menu.png)
1. <span data-ttu-id="bde6f-317">In the **General** tab of the **Properties** window, enter **IncrementalCopyPipeline** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-317">In the **General** tab of the **Properties** window, enter **IncrementalCopyPipeline** for **Name**.</span></span> 

    ![Pipeline name](./media/tutorial-incremental-copy-multiple-tables-portal/pipeline-name.png)
1. <span data-ttu-id="bde6f-319">In the **Properties** window, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="bde6f-319">In the **Properties** window, do the following steps:</span></span> 

    1. <span data-ttu-id="bde6f-320">Click **+ New**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-320">Click **+ New**.</span></span> 
    1. <span data-ttu-id="bde6f-321">Enter **tableList** for the parameter **name**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-321">Enter **tableList** for the parameter **name**.</span></span> 
    1. <span data-ttu-id="bde6f-322">Select **Object** for the parameter **type**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-322">Select **Object** for the parameter **type**.</span></span>

    ![Pipeline parameters](./media/tutorial-incremental-copy-multiple-tables-portal/pipeline-parameters.png) 
1. <span data-ttu-id="bde6f-324">In the **Activities** toolbox, expand **Iteration & Conditionals**, and drag-drop the **ForEach** activity to the pipeline designer surface.</span><span class="sxs-lookup"><span data-stu-id="bde6f-324">In the **Activities** toolbox, expand **Iteration & Conditionals**, and drag-drop the **ForEach** activity to the pipeline designer surface.</span></span> <span data-ttu-id="bde6f-325">In the **General** tab of the **Properties** window, enter **IterateSQLTables**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-325">In the **General** tab of the **Properties** window, enter **IterateSQLTables**.</span></span> 

    ![ForEach activity - name](./media/tutorial-incremental-copy-multiple-tables-portal/foreach-name.png)
1. <span data-ttu-id="bde6f-327">Switch to the **Settings** tab in the **Properties** window, and enter `@pipeline().parameters.tableList` for **Items**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-327">Switch to the **Settings** tab in the **Properties** window, and enter `@pipeline().parameters.tableList` for **Items**.</span></span> <span data-ttu-id="bde6f-328">The ForEach activity iterates through a list of tables and performs the incremental copy operation.</span><span class="sxs-lookup"><span data-stu-id="bde6f-328">The ForEach activity iterates through a list of tables and performs the incremental copy operation.</span></span> 

    ![ForEach activity - settings](./media/tutorial-incremental-copy-multiple-tables-portal/foreach-settings.png)
1. <span data-ttu-id="bde6f-330">Select the **ForEach** activity in the pipeline if it isn't already selected.</span><span class="sxs-lookup"><span data-stu-id="bde6f-330">Select the **ForEach** activity in the pipeline if it isn't already selected.</span></span> <span data-ttu-id="bde6f-331">Click the **Edit (Pencil icon)** button.</span><span class="sxs-lookup"><span data-stu-id="bde6f-331">Click the **Edit (Pencil icon)** button.</span></span>

    ![ForEach activity - edit](./media/tutorial-incremental-copy-multiple-tables-portal/edit-foreach.png)
1. <span data-ttu-id="bde6f-333">In the **Activities** toolbox, expand **General**, drag-drop the **Lookup** activity to the pipeline designer surface, and enter **LookupOldWaterMarkActivity** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-333">In the **Activities** toolbox, expand **General**, drag-drop the **Lookup** activity to the pipeline designer surface, and enter **LookupOldWaterMarkActivity** for **Name**.</span></span>

    ![First Lookup Activity - name](./media/tutorial-incremental-copy-multiple-tables-portal/first-lookup-name.png)
1. <span data-ttu-id="bde6f-335">Switch to the **Settings** tab of the **Properties** window, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="bde6f-335">Switch to the **Settings** tab of the **Properties** window, and do the following steps:</span></span> 

    1. <span data-ttu-id="bde6f-336">Select **WatermarkDataset** for **Source Dataset**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-336">Select **WatermarkDataset** for **Source Dataset**.</span></span>
    1. <span data-ttu-id="bde6f-337">Select **Query** for **Use Query**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-337">Select **Query** for **Use Query**.</span></span> 
    1. <span data-ttu-id="bde6f-338">Enter the following SQL query for **Query**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-338">Enter the following SQL query for **Query**.</span></span> 

        ```sql
        select * from watermarktable where TableName  =  '@{item().TABLE_NAME}'
        ```

        ![First Lookup Activity - settings](./media/tutorial-incremental-copy-multiple-tables-portal/first-lookup-settings.png)
1. <span data-ttu-id="bde6f-340">Drag-drop the **Lookup** activity from the **Activities** toolbox, and enter **LookupNewWaterMarkActivity** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-340">Drag-drop the **Lookup** activity from the **Activities** toolbox, and enter **LookupNewWaterMarkActivity** for **Name**.</span></span>
        
    ![Second Lookup Activity - name](./media/tutorial-incremental-copy-multiple-tables-portal/second-lookup-name.png)
1. <span data-ttu-id="bde6f-342">Switch to the **Settings** tab.</span><span class="sxs-lookup"><span data-stu-id="bde6f-342">Switch to the **Settings** tab.</span></span>

    1. <span data-ttu-id="bde6f-343">Select **SourceDataset** for **Source Dataset**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-343">Select **SourceDataset** for **Source Dataset**.</span></span> 
    1. <span data-ttu-id="bde6f-344">Select **Query** for **Use Query**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-344">Select **Query** for **Use Query**.</span></span>
    1. <span data-ttu-id="bde6f-345">Enter the following SQL query for **Query**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-345">Enter the following SQL query for **Query**.</span></span>

        ```sql    
        select MAX(@{item().WaterMark_Column}) as NewWatermarkvalue from @{item().TABLE_NAME}
        ```
    
        ![Second Lookup Activity - settings](./media/tutorial-incremental-copy-multiple-tables-portal/second-lookup-settings.png)
1. <span data-ttu-id="bde6f-347">Drag-drop the **Copy** activity from the **Activities** toolbox, and enter **IncrementalCopyActivity** for **Name**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-347">Drag-drop the **Copy** activity from the **Activities** toolbox, and enter **IncrementalCopyActivity** for **Name**.</span></span> 

    ![Copy Activity - name](./media/tutorial-incremental-copy-multiple-tables-portal/copy-activity-name.png)
1. <span data-ttu-id="bde6f-349">Connect **Lookup** activities to the **Copy** activity one by one.</span><span class="sxs-lookup"><span data-stu-id="bde6f-349">Connect **Lookup** activities to the **Copy** activity one by one.</span></span> <span data-ttu-id="bde6f-350">To connect, start dragging at the **green** box attached to the **Lookup** activity and drop it on the **Copy** activity.</span><span class="sxs-lookup"><span data-stu-id="bde6f-350">To connect, start dragging at the **green** box attached to the **Lookup** activity and drop it on the **Copy** activity.</span></span> <span data-ttu-id="bde6f-351">Release the mouse button when the border color of the Copy activity changes to **blue**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-351">Release the mouse button when the border color of the Copy activity changes to **blue**.</span></span>

    ![Connect Lookup activities to Copy activity](./media/tutorial-incremental-copy-multiple-tables-portal/connect-lookup-to-copy.png)
1. <span data-ttu-id="bde6f-353">Select the **Copy** activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="bde6f-353">Select the **Copy** activity in the pipeline.</span></span> <span data-ttu-id="bde6f-354">Switch to the **Source** tab in the **Properties** window.</span><span class="sxs-lookup"><span data-stu-id="bde6f-354">Switch to the **Source** tab in the **Properties** window.</span></span> 

    1. <span data-ttu-id="bde6f-355">Select **SourceDataset** for **Source Dataset**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-355">Select **SourceDataset** for **Source Dataset**.</span></span> 
    1. <span data-ttu-id="bde6f-356">Select **Query** for **Use Query**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-356">Select **Query** for **Use Query**.</span></span> 
    1. <span data-ttu-id="bde6f-357">Enter the following SQL query for **Query**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-357">Enter the following SQL query for **Query**.</span></span>

        ```sql
        select * from @{item().TABLE_NAME} where @{item().WaterMark_Column} > '@{activity('LookupOldWaterMarkActivity').output.firstRow.WatermarkValue}' and @{item().WaterMark_Column} <= '@{activity('LookupNewWaterMarkActivity').output.firstRow.NewWatermarkvalue}'        
        ```

        ![Copy Activity - source settings](./media/tutorial-incremental-copy-multiple-tables-portal/copy-source-settings.png)
1. <span data-ttu-id="bde6f-359">Switch to the **Sink** tab, and select **SinkDataset** for **Sink Dataset**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-359">Switch to the **Sink** tab, and select **SinkDataset** for **Sink Dataset**.</span></span> 
        
    ![Copy Activity - sink settings](./media/tutorial-incremental-copy-multiple-tables-portal/copy-sink-settings.png)
1. <span data-ttu-id="bde6f-361">Switch to the **Parameters** tab, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="bde6f-361">Switch to the **Parameters** tab, and do the following steps:</span></span>

    1. <span data-ttu-id="bde6f-362">For **Sink Stored Procedure Name** property, enter `@{item().StoredProcedureNameForMergeOperation}`.</span><span class="sxs-lookup"><span data-stu-id="bde6f-362">For **Sink Stored Procedure Name** property, enter `@{item().StoredProcedureNameForMergeOperation}`.</span></span>
    1. <span data-ttu-id="bde6f-363">For **Sink Table Type** property, enter `@{item().TableType}`.</span><span class="sxs-lookup"><span data-stu-id="bde6f-363">For **Sink Table Type** property, enter `@{item().TableType}`.</span></span>
    1. <span data-ttu-id="bde6f-364">In the **Sink Dataset** section, for **SinkTableName** parameter, enter `@{item().TABLE_NAME}`.</span><span class="sxs-lookup"><span data-stu-id="bde6f-364">In the **Sink Dataset** section, for **SinkTableName** parameter, enter `@{item().TABLE_NAME}`.</span></span>

        ![Copy Activity - parameters](./media/tutorial-incremental-copy-multiple-tables-portal/copy-activity-parameters.png)
1. <span data-ttu-id="bde6f-366">Drag-and-drop the **Stored Procedure** activity from the **Activities** toolbox to the pipeline designer surface.</span><span class="sxs-lookup"><span data-stu-id="bde6f-366">Drag-and-drop the **Stored Procedure** activity from the **Activities** toolbox to the pipeline designer surface.</span></span> <span data-ttu-id="bde6f-367">Connect the **Copy** activity to the **Stored Procedure** activity.</span><span class="sxs-lookup"><span data-stu-id="bde6f-367">Connect the **Copy** activity to the **Stored Procedure** activity.</span></span> 

    ![Copy Activity - parameters](./media/tutorial-incremental-copy-multiple-tables-portal/connect-copy-to-sproc.png)
1. <span data-ttu-id="bde6f-369">Select the **Stored Procedure** activity in the pipeline, and enter **StoredProceduretoWriteWatermarkActivity** for **Name** in the **General** tab of the **Properties** window.</span><span class="sxs-lookup"><span data-stu-id="bde6f-369">Select the **Stored Procedure** activity in the pipeline, and enter **StoredProceduretoWriteWatermarkActivity** for **Name** in the **General** tab of the **Properties** window.</span></span> 

    ![Stored Procedure Activity - name](./media/tutorial-incremental-copy-multiple-tables-portal/sproc-activity-name.png)
1. <span data-ttu-id="bde6f-371">Switch to the **SQL Account** tab, and select **AzureSqlDatabaseLinkedService** for **Linked Service**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-371">Switch to the **SQL Account** tab, and select **AzureSqlDatabaseLinkedService** for **Linked Service**.</span></span>

    ![Stored Procedure Activity - SQL Account](./media/tutorial-incremental-copy-multiple-tables-portal/sproc-activity-sql-account.png)
1. <span data-ttu-id="bde6f-373">Switch to the **Stored Procedure** tab, and do the following steps:</span><span class="sxs-lookup"><span data-stu-id="bde6f-373">Switch to the **Stored Procedure** tab, and do the following steps:</span></span>

    1. <span data-ttu-id="bde6f-374">For **Stored procedure name**, select `sp_write_watermark`.</span><span class="sxs-lookup"><span data-stu-id="bde6f-374">For **Stored procedure name**, select `sp_write_watermark`.</span></span> 
    1. <span data-ttu-id="bde6f-375">Select **Import parameter**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-375">Select **Import parameter**.</span></span> 
    1. <span data-ttu-id="bde6f-376">Specify the following values for the parameters:</span><span class="sxs-lookup"><span data-stu-id="bde6f-376">Specify the following values for the parameters:</span></span> 

        | <span data-ttu-id="bde6f-377">Name</span><span class="sxs-lookup"><span data-stu-id="bde6f-377">Name</span></span> | <span data-ttu-id="bde6f-378">Type</span><span class="sxs-lookup"><span data-stu-id="bde6f-378">Type</span></span> | <span data-ttu-id="bde6f-379">Value</span><span class="sxs-lookup"><span data-stu-id="bde6f-379">Value</span></span> | 
        | ---- | ---- | ----- |
        | <span data-ttu-id="bde6f-380">LastModifiedtime</span><span class="sxs-lookup"><span data-stu-id="bde6f-380">LastModifiedtime</span></span> | <span data-ttu-id="bde6f-381">DateTime</span><span class="sxs-lookup"><span data-stu-id="bde6f-381">DateTime</span></span> | `@{activity('LookupNewWaterMarkActivity').output.firstRow.NewWatermarkvalue}` |
        | <span data-ttu-id="bde6f-382">TableName</span><span class="sxs-lookup"><span data-stu-id="bde6f-382">TableName</span></span> | <span data-ttu-id="bde6f-383">String</span><span class="sxs-lookup"><span data-stu-id="bde6f-383">String</span></span> | `@{activity('LookupOldWaterMarkActivity').output.firstRow.TableName}` |
    
        ![Stored Procedure Activity - stored procedure settings](./media/tutorial-incremental-copy-multiple-tables-portal/sproc-activity-sproc-settings.png)
1. <span data-ttu-id="bde6f-385">In the left pane, click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-385">In the left pane, click **Publish**.</span></span> <span data-ttu-id="bde6f-386">This action publishes the entities you created to the Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="bde6f-386">This action publishes the entities you created to the Data Factory service.</span></span> 

    ![Publish button](./media/tutorial-incremental-copy-multiple-tables-portal/publish-button.png)
1. <span data-ttu-id="bde6f-388">Wait until you see the **Successfully published** message.</span><span class="sxs-lookup"><span data-stu-id="bde6f-388">Wait until you see the **Successfully published** message.</span></span> <span data-ttu-id="bde6f-389">To see the notifications, click the **Show Notifications** link.</span><span class="sxs-lookup"><span data-stu-id="bde6f-389">To see the notifications, click the **Show Notifications** link.</span></span> <span data-ttu-id="bde6f-390">Close the notifications window by clicking **X**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-390">Close the notifications window by clicking **X**.</span></span>

    ![Show Notifications](./media/tutorial-incremental-copy-multiple-tables-portal/notifications.png)

 
## <a name="run-the-pipeline"></a><span data-ttu-id="bde6f-392">Run the pipeline</span><span class="sxs-lookup"><span data-stu-id="bde6f-392">Run the pipeline</span></span>

1. <span data-ttu-id="bde6f-393">On the toolbar for the pipeline, click **Trigger**, and click **Trigger Now**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-393">On the toolbar for the pipeline, click **Trigger**, and click **Trigger Now**.</span></span>     

    ![Trigger now](./media/tutorial-incremental-copy-multiple-tables-portal/trigger-now.png)
1. <span data-ttu-id="bde6f-395">In the **Pipeline Run** window, enter the following value for the **tableList** parameter, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-395">In the **Pipeline Run** window, enter the following value for the **tableList** parameter, and click **Finish**.</span></span> 

    ```
    [
        {
            "TABLE_NAME": "customer_table",
            "WaterMark_Column": "LastModifytime",
            "TableType": "DataTypeforCustomerTable",
            "StoredProcedureNameForMergeOperation": "sp_upsert_customer_table"
        },
        {
            "TABLE_NAME": "project_table",
            "WaterMark_Column": "Creationtime",
            "TableType": "DataTypeforProjectTable",
            "StoredProcedureNameForMergeOperation": "sp_upsert_project_table"
        }
    ]
    ```

    ![Pipeline Run arguments](./media/tutorial-incremental-copy-multiple-tables-portal/pipeline-run-arguments.png)

## <a name="monitor-the-pipeline"></a><span data-ttu-id="bde6f-397">Monitor the pipeline</span><span class="sxs-lookup"><span data-stu-id="bde6f-397">Monitor the pipeline</span></span>

1. <span data-ttu-id="bde6f-398">Switch to the **Monitor** tab on the left.</span><span class="sxs-lookup"><span data-stu-id="bde6f-398">Switch to the **Monitor** tab on the left.</span></span> <span data-ttu-id="bde6f-399">You see the pipeline run triggered by the **manual trigger**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-399">You see the pipeline run triggered by the **manual trigger**.</span></span> <span data-ttu-id="bde6f-400">Click **Refresh** button to refresh the list.</span><span class="sxs-lookup"><span data-stu-id="bde6f-400">Click **Refresh** button to refresh the list.</span></span> <span data-ttu-id="bde6f-401">Links in the **Actions** column allow you to view activity runs associated with the pipeline run, and to rerun the pipeline.</span><span class="sxs-lookup"><span data-stu-id="bde6f-401">Links in the **Actions** column allow you to view activity runs associated with the pipeline run, and to rerun the pipeline.</span></span> 

    ![Pipeline runs](./media/tutorial-incremental-copy-multiple-tables-portal/pipeline-runs.png)
1. <span data-ttu-id="bde6f-403">Click **View Activity Runs** link in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="bde6f-403">Click **View Activity Runs** link in the **Actions** column.</span></span> <span data-ttu-id="bde6f-404">You see all the activity runs associated with the selected pipeline run.</span><span class="sxs-lookup"><span data-stu-id="bde6f-404">You see all the activity runs associated with the selected pipeline run.</span></span> 

    ![Activity runs](./media/tutorial-incremental-copy-multiple-tables-portal/activity-runs.png)

## <a name="review-the-results"></a><span data-ttu-id="bde6f-406">Review the results</span><span class="sxs-lookup"><span data-stu-id="bde6f-406">Review the results</span></span>
<span data-ttu-id="bde6f-407">In SQL Server Management Studio, run the following queries against the target SQL database to verify that the data was copied from source tables to destination tables:</span><span class="sxs-lookup"><span data-stu-id="bde6f-407">In SQL Server Management Studio, run the following queries against the target SQL database to verify that the data was copied from source tables to destination tables:</span></span> 

<span data-ttu-id="bde6f-408">**Query**</span><span class="sxs-lookup"><span data-stu-id="bde6f-408">**Query**</span></span> 
```sql
select * from customer_table
```

<span data-ttu-id="bde6f-409">**Output**</span><span class="sxs-lookup"><span data-stu-id="bde6f-409">**Output**</span></span>
```
===========================================
PersonID    Name    LastModifytime
===========================================
1           John    2017-09-01 00:56:00.000
2           Mike    2017-09-02 05:23:00.000
3           Alice   2017-09-03 02:36:00.000
4           Andy    2017-09-04 03:21:00.000
5           Anny    2017-09-05 08:06:00.000
```

<span data-ttu-id="bde6f-410">**Query**</span><span class="sxs-lookup"><span data-stu-id="bde6f-410">**Query**</span></span>

```sql
select * from project_table
```

<span data-ttu-id="bde6f-411">**Output**</span><span class="sxs-lookup"><span data-stu-id="bde6f-411">**Output**</span></span>

```
===================================
Project     Creationtime
===================================
project1    2015-01-01 00:00:00.000
project2    2016-02-02 01:23:00.000
project3    2017-03-04 05:16:00.000
```

<span data-ttu-id="bde6f-412">**Query**</span><span class="sxs-lookup"><span data-stu-id="bde6f-412">**Query**</span></span>

```sql
select * from watermarktable
```

<span data-ttu-id="bde6f-413">**Output**</span><span class="sxs-lookup"><span data-stu-id="bde6f-413">**Output**</span></span>

```
======================================
TableName       WatermarkValue
======================================
customer_table  2017-09-05 08:06:00.000
project_table   2017-03-04 05:16:00.000
```

<span data-ttu-id="bde6f-414">Notice that the watermark values for both tables were updated.</span><span class="sxs-lookup"><span data-stu-id="bde6f-414">Notice that the watermark values for both tables were updated.</span></span> 

## <a name="add-more-data-to-the-source-tables"></a><span data-ttu-id="bde6f-415">Add more data to the source tables</span><span class="sxs-lookup"><span data-stu-id="bde6f-415">Add more data to the source tables</span></span>

<span data-ttu-id="bde6f-416">Run the following query against the source SQL Server database to update an existing row in customer_table.</span><span class="sxs-lookup"><span data-stu-id="bde6f-416">Run the following query against the source SQL Server database to update an existing row in customer_table.</span></span> <span data-ttu-id="bde6f-417">Insert a new row into project_table.</span><span class="sxs-lookup"><span data-stu-id="bde6f-417">Insert a new row into project_table.</span></span> 

```sql
UPDATE customer_table
SET [LastModifytime] = '2017-09-08T00:00:00Z', [name]='NewName' where [PersonID] = 3

INSERT INTO project_table
(Project, Creationtime)
VALUES
('NewProject','10/1/2017 0:00:00 AM');
``` 

## <a name="rerun-the-pipeline"></a><span data-ttu-id="bde6f-418">Rerun the pipeline</span><span class="sxs-lookup"><span data-stu-id="bde6f-418">Rerun the pipeline</span></span>
1. <span data-ttu-id="bde6f-419">In the web browser window, switch to the **Edit** tab on the left.</span><span class="sxs-lookup"><span data-stu-id="bde6f-419">In the web browser window, switch to the **Edit** tab on the left.</span></span> 
1. <span data-ttu-id="bde6f-420">On the toolbar for the pipeline, click **Trigger**, and click **Trigger Now**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-420">On the toolbar for the pipeline, click **Trigger**, and click **Trigger Now**.</span></span>   

    ![Trigger now](./media/tutorial-incremental-copy-multiple-tables-portal/trigger-now.png)
1. <span data-ttu-id="bde6f-422">In the **Pipeline Run** window, enter the following value for the **tableList** parameter, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-422">In the **Pipeline Run** window, enter the following value for the **tableList** parameter, and click **Finish**.</span></span> 

    ```
    [
        {
            "TABLE_NAME": "customer_table",
            "WaterMark_Column": "LastModifytime",
            "TableType": "DataTypeforCustomerTable",
            "StoredProcedureNameForMergeOperation": "sp_upsert_customer_table"
        },
        {
            "TABLE_NAME": "project_table",
            "WaterMark_Column": "Creationtime",
            "TableType": "DataTypeforProjectTable",
            "StoredProcedureNameForMergeOperation": "sp_upsert_project_table"
        }
    ]
    ```

## <a name="monitor-the-pipeline-again"></a><span data-ttu-id="bde6f-423">Monitor the pipeline again</span><span class="sxs-lookup"><span data-stu-id="bde6f-423">Monitor the pipeline again</span></span>

1. <span data-ttu-id="bde6f-424">Switch to the **Monitor** tab on the left.</span><span class="sxs-lookup"><span data-stu-id="bde6f-424">Switch to the **Monitor** tab on the left.</span></span> <span data-ttu-id="bde6f-425">You see the pipeline run triggered by the **manual trigger**.</span><span class="sxs-lookup"><span data-stu-id="bde6f-425">You see the pipeline run triggered by the **manual trigger**.</span></span> <span data-ttu-id="bde6f-426">Click **Refresh** button to refresh the list.</span><span class="sxs-lookup"><span data-stu-id="bde6f-426">Click **Refresh** button to refresh the list.</span></span> <span data-ttu-id="bde6f-427">Links in the **Actions** column allow you to view activity runs associated with the pipeline run, and to rerun the pipeline.</span><span class="sxs-lookup"><span data-stu-id="bde6f-427">Links in the **Actions** column allow you to view activity runs associated with the pipeline run, and to rerun the pipeline.</span></span> 

    ![Pipeline runs](./media/tutorial-incremental-copy-multiple-tables-portal/pipeline-runs.png)
1. <span data-ttu-id="bde6f-429">Click **View Activity Runs** link in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="bde6f-429">Click **View Activity Runs** link in the **Actions** column.</span></span> <span data-ttu-id="bde6f-430">You see all the activity runs associated with the selected pipeline run.</span><span class="sxs-lookup"><span data-stu-id="bde6f-430">You see all the activity runs associated with the selected pipeline run.</span></span> 

    ![Activity runs](./media/tutorial-incremental-copy-multiple-tables-portal/activity-runs.png) 

## <a name="review-the-final-results"></a><span data-ttu-id="bde6f-432">Review the final results</span><span class="sxs-lookup"><span data-stu-id="bde6f-432">Review the final results</span></span>
<span data-ttu-id="bde6f-433">In SQL Server Management Studio, run the following queries against the target database to verify that the updated/new data was copied from source tables to destination tables.</span><span class="sxs-lookup"><span data-stu-id="bde6f-433">In SQL Server Management Studio, run the following queries against the target database to verify that the updated/new data was copied from source tables to destination tables.</span></span> 

<span data-ttu-id="bde6f-434">**Query**</span><span class="sxs-lookup"><span data-stu-id="bde6f-434">**Query**</span></span> 
```sql
select * from customer_table
```

<span data-ttu-id="bde6f-435">**Output**</span><span class="sxs-lookup"><span data-stu-id="bde6f-435">**Output**</span></span>
```
===========================================
PersonID    Name    LastModifytime
===========================================
1           John    2017-09-01 00:56:00.000
2           Mike    2017-09-02 05:23:00.000
3           NewName 2017-09-08 00:00:00.000
4           Andy    2017-09-04 03:21:00.000
5           Anny    2017-09-05 08:06:00.000
```

<span data-ttu-id="bde6f-436">Notice the new values of **Name** and **LastModifytime** for the **PersonID** for number 3.</span><span class="sxs-lookup"><span data-stu-id="bde6f-436">Notice the new values of **Name** and **LastModifytime** for the **PersonID** for number 3.</span></span> 

<span data-ttu-id="bde6f-437">**Query**</span><span class="sxs-lookup"><span data-stu-id="bde6f-437">**Query**</span></span>

```sql
select * from project_table
```

<span data-ttu-id="bde6f-438">**Output**</span><span class="sxs-lookup"><span data-stu-id="bde6f-438">**Output**</span></span>

```
===================================
Project     Creationtime
===================================
project1    2015-01-01 00:00:00.000
project2    2016-02-02 01:23:00.000
project3    2017-03-04 05:16:00.000
NewProject  2017-10-01 00:00:00.000
```

<span data-ttu-id="bde6f-439">Notice that the **NewProject** entry was added to project_table.</span><span class="sxs-lookup"><span data-stu-id="bde6f-439">Notice that the **NewProject** entry was added to project_table.</span></span> 

<span data-ttu-id="bde6f-440">**Query**</span><span class="sxs-lookup"><span data-stu-id="bde6f-440">**Query**</span></span>

```sql
select * from watermarktable
```

<span data-ttu-id="bde6f-441">**Output**</span><span class="sxs-lookup"><span data-stu-id="bde6f-441">**Output**</span></span>

```
======================================
TableName       WatermarkValue
======================================
customer_table  2017-09-08 00:00:00.000
project_table   2017-10-01 00:00:00.000
```

<span data-ttu-id="bde6f-442">Notice that the watermark values for both tables were updated.</span><span class="sxs-lookup"><span data-stu-id="bde6f-442">Notice that the watermark values for both tables were updated.</span></span>
     
## <a name="next-steps"></a><span data-ttu-id="bde6f-443">Next steps</span><span class="sxs-lookup"><span data-stu-id="bde6f-443">Next steps</span></span>
<span data-ttu-id="bde6f-444">You performed the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="bde6f-444">You performed the following steps in this tutorial:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="bde6f-445">Prepare source and destination data stores.</span><span class="sxs-lookup"><span data-stu-id="bde6f-445">Prepare source and destination data stores.</span></span>
> * <span data-ttu-id="bde6f-446">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="bde6f-446">Create a data factory.</span></span>
> * <span data-ttu-id="bde6f-447">Create a self-hosted integration runtime (IR).</span><span class="sxs-lookup"><span data-stu-id="bde6f-447">Create a self-hosted integration runtime (IR).</span></span>
> * <span data-ttu-id="bde6f-448">Install the integration runtime.</span><span class="sxs-lookup"><span data-stu-id="bde6f-448">Install the integration runtime.</span></span>
> * <span data-ttu-id="bde6f-449">Create linked services.</span><span class="sxs-lookup"><span data-stu-id="bde6f-449">Create linked services.</span></span> 
> * <span data-ttu-id="bde6f-450">Create source, sink, and watermark datasets.</span><span class="sxs-lookup"><span data-stu-id="bde6f-450">Create source, sink, and watermark datasets.</span></span>
> * <span data-ttu-id="bde6f-451">Create, run, and monitor a pipeline.</span><span class="sxs-lookup"><span data-stu-id="bde6f-451">Create, run, and monitor a pipeline.</span></span>
> * <span data-ttu-id="bde6f-452">Review the results.</span><span class="sxs-lookup"><span data-stu-id="bde6f-452">Review the results.</span></span>
> * <span data-ttu-id="bde6f-453">Add or update data in source tables.</span><span class="sxs-lookup"><span data-stu-id="bde6f-453">Add or update data in source tables.</span></span>
> * <span data-ttu-id="bde6f-454">Rerun and monitor the pipeline.</span><span class="sxs-lookup"><span data-stu-id="bde6f-454">Rerun and monitor the pipeline.</span></span>
> * <span data-ttu-id="bde6f-455">Review the final results.</span><span class="sxs-lookup"><span data-stu-id="bde6f-455">Review the final results.</span></span>

<span data-ttu-id="bde6f-456">Advance to the following tutorial to learn about transforming data by using a Spark cluster on Azure:</span><span class="sxs-lookup"><span data-stu-id="bde6f-456">Advance to the following tutorial to learn about transforming data by using a Spark cluster on Azure:</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="bde6f-457">Incrementally load data from Azure SQL Database to Azure Blob storage by using Change Tracking technology</span><span class="sxs-lookup"><span data-stu-id="bde6f-457">Incrementally load data from Azure SQL Database to Azure Blob storage by using Change Tracking technology</span></span>](tutorial-incremental-copy-change-tracking-feature-portal.md)


