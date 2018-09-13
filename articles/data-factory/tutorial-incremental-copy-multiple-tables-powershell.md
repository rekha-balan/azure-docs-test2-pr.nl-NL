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
ms.date: 01/22/2018
ms.author: yexu
ms.openlocfilehash: ce83be3b08a08223e34f8c366e863ceee8e5d7ac
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857701"
---
# <a name="incrementally-load-data-from-multiple-tables-in-sql-server-to-an-azure-sql-database"></a><span data-ttu-id="c52f8-103">Incrementally load data from multiple tables in SQL Server to an Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="c52f8-103">Incrementally load data from multiple tables in SQL Server to an Azure SQL database</span></span>
<span data-ttu-id="c52f8-104">In this tutorial, you create an Azure data factory with a pipeline that loads delta data from multiple tables in on-premises SQL Server to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="c52f8-104">In this tutorial, you create an Azure data factory with a pipeline that loads delta data from multiple tables in on-premises SQL Server to an Azure SQL database.</span></span>    

<span data-ttu-id="c52f8-105">You perform the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="c52f8-105">You perform the following steps in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c52f8-106">Prepare source and destination data stores.</span><span class="sxs-lookup"><span data-stu-id="c52f8-106">Prepare source and destination data stores.</span></span>
> * <span data-ttu-id="c52f8-107">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="c52f8-107">Create a data factory.</span></span>
> * <span data-ttu-id="c52f8-108">Create a self-hosted integration runtime.</span><span class="sxs-lookup"><span data-stu-id="c52f8-108">Create a self-hosted integration runtime.</span></span>
> * <span data-ttu-id="c52f8-109">Install the integration runtime.</span><span class="sxs-lookup"><span data-stu-id="c52f8-109">Install the integration runtime.</span></span> 
> * <span data-ttu-id="c52f8-110">Create linked services.</span><span class="sxs-lookup"><span data-stu-id="c52f8-110">Create linked services.</span></span> 
> * <span data-ttu-id="c52f8-111">Create source, sink, and watermark datasets.</span><span class="sxs-lookup"><span data-stu-id="c52f8-111">Create source, sink, and watermark datasets.</span></span>
> * <span data-ttu-id="c52f8-112">Create, run, and monitor a pipeline.</span><span class="sxs-lookup"><span data-stu-id="c52f8-112">Create, run, and monitor a pipeline.</span></span>
> * <span data-ttu-id="c52f8-113">Review the results.</span><span class="sxs-lookup"><span data-stu-id="c52f8-113">Review the results.</span></span>
> * <span data-ttu-id="c52f8-114">Add or update data in source tables.</span><span class="sxs-lookup"><span data-stu-id="c52f8-114">Add or update data in source tables.</span></span>
> * <span data-ttu-id="c52f8-115">Rerun and monitor the pipeline.</span><span class="sxs-lookup"><span data-stu-id="c52f8-115">Rerun and monitor the pipeline.</span></span>
> * <span data-ttu-id="c52f8-116">Review the final results.</span><span class="sxs-lookup"><span data-stu-id="c52f8-116">Review the final results.</span></span>

## <a name="overview"></a><span data-ttu-id="c52f8-117">Overview</span><span class="sxs-lookup"><span data-stu-id="c52f8-117">Overview</span></span>
<span data-ttu-id="c52f8-118">Here are the important steps to create this solution:</span><span class="sxs-lookup"><span data-stu-id="c52f8-118">Here are the important steps to create this solution:</span></span> 

1. <span data-ttu-id="c52f8-119">**Select the watermark column**.</span><span class="sxs-lookup"><span data-stu-id="c52f8-119">**Select the watermark column**.</span></span>
    <span data-ttu-id="c52f8-120">Select one column for each table in the source data store, which can be used to identify the new or updated records for every run.</span><span class="sxs-lookup"><span data-stu-id="c52f8-120">Select one column for each table in the source data store, which can be used to identify the new or updated records for every run.</span></span> <span data-ttu-id="c52f8-121">Normally, the data in this selected column (for example, last_modify_time or ID) keeps increasing when rows are created or updated.</span><span class="sxs-lookup"><span data-stu-id="c52f8-121">Normally, the data in this selected column (for example, last_modify_time or ID) keeps increasing when rows are created or updated.</span></span> <span data-ttu-id="c52f8-122">The maximum value in this column is used as a watermark.</span><span class="sxs-lookup"><span data-stu-id="c52f8-122">The maximum value in this column is used as a watermark.</span></span>

1. <span data-ttu-id="c52f8-123">**Prepare a data store to store the watermark value**.</span><span class="sxs-lookup"><span data-stu-id="c52f8-123">**Prepare a data store to store the watermark value**.</span></span>   
    <span data-ttu-id="c52f8-124">In this tutorial, you store the watermark value in a SQL database.</span><span class="sxs-lookup"><span data-stu-id="c52f8-124">In this tutorial, you store the watermark value in a SQL database.</span></span>

1. <span data-ttu-id="c52f8-125">**Create a pipeline with the following activities**:</span><span class="sxs-lookup"><span data-stu-id="c52f8-125">**Create a pipeline with the following activities**:</span></span> 
    
    <span data-ttu-id="c52f8-126">a.</span><span class="sxs-lookup"><span data-stu-id="c52f8-126">a.</span></span> <span data-ttu-id="c52f8-127">Create a ForEach activity that iterates through a list of source table names that is passed as a parameter to the pipeline.</span><span class="sxs-lookup"><span data-stu-id="c52f8-127">Create a ForEach activity that iterates through a list of source table names that is passed as a parameter to the pipeline.</span></span> <span data-ttu-id="c52f8-128">For each source table, it invokes the following activities to perform delta loading for that table.</span><span class="sxs-lookup"><span data-stu-id="c52f8-128">For each source table, it invokes the following activities to perform delta loading for that table.</span></span>

    <span data-ttu-id="c52f8-129">b.</span><span class="sxs-lookup"><span data-stu-id="c52f8-129">b.</span></span> <span data-ttu-id="c52f8-130">Create two lookup activities.</span><span class="sxs-lookup"><span data-stu-id="c52f8-130">Create two lookup activities.</span></span> <span data-ttu-id="c52f8-131">Use the first Lookup activity to retrieve the last watermark value.</span><span class="sxs-lookup"><span data-stu-id="c52f8-131">Use the first Lookup activity to retrieve the last watermark value.</span></span> <span data-ttu-id="c52f8-132">Use the second Lookup activity to retrieve the new watermark value.</span><span class="sxs-lookup"><span data-stu-id="c52f8-132">Use the second Lookup activity to retrieve the new watermark value.</span></span> <span data-ttu-id="c52f8-133">These watermark values are passed to the Copy activity.</span><span class="sxs-lookup"><span data-stu-id="c52f8-133">These watermark values are passed to the Copy activity.</span></span>

    <span data-ttu-id="c52f8-134">c.</span><span class="sxs-lookup"><span data-stu-id="c52f8-134">c.</span></span> <span data-ttu-id="c52f8-135">Create a Copy activity that copies rows from the source data store with the value of the watermark column greater than the old watermark value and less than the new watermark value.</span><span class="sxs-lookup"><span data-stu-id="c52f8-135">Create a Copy activity that copies rows from the source data store with the value of the watermark column greater than the old watermark value and less than the new watermark value.</span></span> <span data-ttu-id="c52f8-136">Then, it copies the delta data from the source data store to Azure Blob storage as a new file.</span><span class="sxs-lookup"><span data-stu-id="c52f8-136">Then, it copies the delta data from the source data store to Azure Blob storage as a new file.</span></span>

    <span data-ttu-id="c52f8-137">d.</span><span class="sxs-lookup"><span data-stu-id="c52f8-137">d.</span></span> <span data-ttu-id="c52f8-138">Create a StoredProcedure activity that updates the watermark value for the pipeline that runs next time.</span><span class="sxs-lookup"><span data-stu-id="c52f8-138">Create a StoredProcedure activity that updates the watermark value for the pipeline that runs next time.</span></span> 

    <span data-ttu-id="c52f8-139">Here is the high-level solution diagram:</span><span class="sxs-lookup"><span data-stu-id="c52f8-139">Here is the high-level solution diagram:</span></span> 

    ![Incrementally load data](media\tutorial-incremental-copy-multiple-tables-powershell\high-level-solution-diagram.png)


<span data-ttu-id="c52f8-141">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="c52f8-141">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c52f8-142">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c52f8-142">Prerequisites</span></span>
* <span data-ttu-id="c52f8-143">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="c52f8-143">**SQL Server**.</span></span> <span data-ttu-id="c52f8-144">You use an on-premises SQL Server database as the source data store in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="c52f8-144">You use an on-premises SQL Server database as the source data store in this tutorial.</span></span> 
* <span data-ttu-id="c52f8-145">**Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="c52f8-145">**Azure SQL Database**.</span></span> <span data-ttu-id="c52f8-146">You use a SQL database as the sink data store.</span><span class="sxs-lookup"><span data-stu-id="c52f8-146">You use a SQL database as the sink data store.</span></span> <span data-ttu-id="c52f8-147">If you don't have a SQL database, see [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="c52f8-147">If you don't have a SQL database, see [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) for steps to create one.</span></span> 

### <a name="create-source-tables-in-your-sql-server-database"></a><span data-ttu-id="c52f8-148">Create source tables in your SQL Server database</span><span class="sxs-lookup"><span data-stu-id="c52f8-148">Create source tables in your SQL Server database</span></span>

1. <span data-ttu-id="c52f8-149">Open SQL Server Management Studio, and connect to your on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="c52f8-149">Open SQL Server Management Studio, and connect to your on-premises SQL Server database.</span></span>

1. <span data-ttu-id="c52f8-150">In **Server Explorer**, right-click the database and choose **New Query**.</span><span class="sxs-lookup"><span data-stu-id="c52f8-150">In **Server Explorer**, right-click the database and choose **New Query**.</span></span>

1. <span data-ttu-id="c52f8-151">Run the following SQL command against your database to create tables named `customer_table` and `project_table`:</span><span class="sxs-lookup"><span data-stu-id="c52f8-151">Run the following SQL command against your database to create tables named `customer_table` and `project_table`:</span></span>

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

### <a name="create-destination-tables-in-your-azure-sql-database"></a><span data-ttu-id="c52f8-152">Create destination tables in your Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="c52f8-152">Create destination tables in your Azure SQL database</span></span>
1. <span data-ttu-id="c52f8-153">Open SQL Server Management Studio, and connect to your SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="c52f8-153">Open SQL Server Management Studio, and connect to your SQL Server database.</span></span>

1. <span data-ttu-id="c52f8-154">In **Server Explorer**, right-click the database and choose **New Query**.</span><span class="sxs-lookup"><span data-stu-id="c52f8-154">In **Server Explorer**, right-click the database and choose **New Query**.</span></span>

1. <span data-ttu-id="c52f8-155">Run the following SQL command against your SQL database to create tables named `customer_table` and `project_table`:</span><span class="sxs-lookup"><span data-stu-id="c52f8-155">Run the following SQL command against your SQL database to create tables named `customer_table` and `project_table`:</span></span>  
    
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

### <a name="create-another-table-in-the-azure-sql-database-to-store-the-high-watermark-value"></a><span data-ttu-id="c52f8-156">Create another table in the Azure SQL database to store the high watermark value</span><span class="sxs-lookup"><span data-stu-id="c52f8-156">Create another table in the Azure SQL database to store the high watermark value</span></span>
1. <span data-ttu-id="c52f8-157">Run the following SQL command against your SQL database to create a table named `watermarktable` to store the watermark value:</span><span class="sxs-lookup"><span data-stu-id="c52f8-157">Run the following SQL command against your SQL database to create a table named `watermarktable` to store the watermark value:</span></span> 
    
    ```sql
    create table watermarktable
    (
    
        TableName varchar(255),
        WatermarkValue datetime,
    );
    ```
1. <span data-ttu-id="c52f8-158">Insert initial watermark values for both source tables into the watermark table.</span><span class="sxs-lookup"><span data-stu-id="c52f8-158">Insert initial watermark values for both source tables into the watermark table.</span></span>

    ```sql

    INSERT INTO watermarktable
    VALUES 
    ('customer_table','1/1/2010 12:00:00 AM'),
    ('project_table','1/1/2010 12:00:00 AM');
    
    ```

### <a name="create-a-stored-procedure-in-the-azure-sql-database"></a><span data-ttu-id="c52f8-159">Create a stored procedure in the Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="c52f8-159">Create a stored procedure in the Azure SQL database</span></span> 

<span data-ttu-id="c52f8-160">Run the following command to create a stored procedure in your SQL database.</span><span class="sxs-lookup"><span data-stu-id="c52f8-160">Run the following command to create a stored procedure in your SQL database.</span></span> <span data-ttu-id="c52f8-161">This stored procedure updates the watermark value after every pipeline run.</span><span class="sxs-lookup"><span data-stu-id="c52f8-161">This stored procedure updates the watermark value after every pipeline run.</span></span> 

```sql
CREATE PROCEDURE sp_write_watermark @LastModifiedtime datetime, @TableName varchar(50)
AS

BEGIN

    UPDATE watermarktable
    SET [WatermarkValue] = @LastModifiedtime 
WHERE [TableName] = @TableName

END

```

### <a name="create-data-types-and-additional-stored-procedures-in-the-azure-sql-database"></a><span data-ttu-id="c52f8-162">Create data types and additional stored procedures in the Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="c52f8-162">Create data types and additional stored procedures in the Azure SQL database</span></span>
<span data-ttu-id="c52f8-163">Run the following query to create two stored procedures and two data types in your SQL database.</span><span class="sxs-lookup"><span data-stu-id="c52f8-163">Run the following query to create two stored procedures and two data types in your SQL database.</span></span> <span data-ttu-id="c52f8-164">They're used to merge the data from source tables into destination tables.</span><span class="sxs-lookup"><span data-stu-id="c52f8-164">They're used to merge the data from source tables into destination tables.</span></span>

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

### <a name="azure-powershell"></a><span data-ttu-id="c52f8-165">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c52f8-165">Azure PowerShell</span></span>
<span data-ttu-id="c52f8-166">Install the latest Azure PowerShell modules by following the instructions in [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="c52f8-166">Install the latest Azure PowerShell modules by following the instructions in [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="c52f8-167">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="c52f8-167">Create a data factory</span></span>
1. <span data-ttu-id="c52f8-168">Define a variable for the resource group name that you use in PowerShell commands later.</span><span class="sxs-lookup"><span data-stu-id="c52f8-168">Define a variable for the resource group name that you use in PowerShell commands later.</span></span> <span data-ttu-id="c52f8-169">Copy the following command text to PowerShell, specify a name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) in double quotation marks, and then run the command.</span><span class="sxs-lookup"><span data-stu-id="c52f8-169">Copy the following command text to PowerShell, specify a name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) in double quotation marks, and then run the command.</span></span> <span data-ttu-id="c52f8-170">An example is `"adfrg"`.</span><span class="sxs-lookup"><span data-stu-id="c52f8-170">An example is `"adfrg"`.</span></span> 
   
     ```powershell
    $resourceGroupName = "ADFTutorialResourceGroup";
    ```

    <span data-ttu-id="c52f8-171">If the resource group already exists, you might not want to overwrite it.</span><span class="sxs-lookup"><span data-stu-id="c52f8-171">If the resource group already exists, you might not want to overwrite it.</span></span> <span data-ttu-id="c52f8-172">Assign a different value to the `$resourceGroupName` variable, and run the command again.</span><span class="sxs-lookup"><span data-stu-id="c52f8-172">Assign a different value to the `$resourceGroupName` variable, and run the command again.</span></span>

1. <span data-ttu-id="c52f8-173">Define a variable for the location of the data factory.</span><span class="sxs-lookup"><span data-stu-id="c52f8-173">Define a variable for the location of the data factory.</span></span> 

    ```powershell
    $location = "East US"
    ```
1. <span data-ttu-id="c52f8-174">To create the Azure resource group, run the following command:</span><span class="sxs-lookup"><span data-stu-id="c52f8-174">To create the Azure resource group, run the following command:</span></span> 

    ```powershell
    New-AzureRmResourceGroup $resourceGroupName $location
    ``` 
    <span data-ttu-id="c52f8-175">If the resource group already exists, you might not want to overwrite it.</span><span class="sxs-lookup"><span data-stu-id="c52f8-175">If the resource group already exists, you might not want to overwrite it.</span></span> <span data-ttu-id="c52f8-176">Assign a different value to the `$resourceGroupName` variable, and run the command again.</span><span class="sxs-lookup"><span data-stu-id="c52f8-176">Assign a different value to the `$resourceGroupName` variable, and run the command again.</span></span>

1. <span data-ttu-id="c52f8-177">Define a variable for the data factory name.</span><span class="sxs-lookup"><span data-stu-id="c52f8-177">Define a variable for the data factory name.</span></span> 

    > [!IMPORTANT]
    >  <span data-ttu-id="c52f8-178">Update the data factory name to make it globally unique.</span><span class="sxs-lookup"><span data-stu-id="c52f8-178">Update the data factory name to make it globally unique.</span></span> <span data-ttu-id="c52f8-179">An example is ADFIncMultiCopyTutorialFactorySP1127.</span><span class="sxs-lookup"><span data-stu-id="c52f8-179">An example is ADFIncMultiCopyTutorialFactorySP1127.</span></span> 

    ```powershell
    $dataFactoryName = "ADFIncMultiCopyTutorialFactory";
    ```
1. <span data-ttu-id="c52f8-180">To create the data factory, run the following **Set-AzureRmDataFactoryV2** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c52f8-180">To create the data factory, run the following **Set-AzureRmDataFactoryV2** cmdlet:</span></span> 
    
    ```powershell       
    Set-AzureRmDataFactoryV2 -ResourceGroupName $resourceGroupName -Location $location -Name $dataFactoryName 
    ```

<span data-ttu-id="c52f8-181">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="c52f8-181">Note the following points:</span></span>

* <span data-ttu-id="c52f8-182">The name of the data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="c52f8-182">The name of the data factory must be globally unique.</span></span> <span data-ttu-id="c52f8-183">If you receive the following error, change the name and try again:</span><span class="sxs-lookup"><span data-stu-id="c52f8-183">If you receive the following error, change the name and try again:</span></span>

    ```
    The specified Data Factory name 'ADFIncMultiCopyTutorialFactory' is already in use. Data Factory names must be globally unique.
    ```
* <span data-ttu-id="c52f8-184">To create Data Factory instances, the user account you use to sign in to Azure must be a member of contributor or owner roles, or an administrator of the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="c52f8-184">To create Data Factory instances, the user account you use to sign in to Azure must be a member of contributor or owner roles, or an administrator of the Azure subscription.</span></span>
* <span data-ttu-id="c52f8-185">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="c52f8-185">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span></span> <span data-ttu-id="c52f8-186">The data stores (Azure Storage, SQL Database, etc.) and computes (Azure HDInsight, etc.) used by the data factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="c52f8-186">The data stores (Azure Storage, SQL Database, etc.) and computes (Azure HDInsight, etc.) used by the data factory can be in other regions.</span></span>

[!INCLUDE [data-factory-create-install-integration-runtime](../../includes/data-factory-create-install-integration-runtime.md)]



## <a name="create-linked-services"></a><span data-ttu-id="c52f8-187">Create linked services</span><span class="sxs-lookup"><span data-stu-id="c52f8-187">Create linked services</span></span>
<span data-ttu-id="c52f8-188">You create linked services in a data factory to link your data stores and compute services to the data factory.</span><span class="sxs-lookup"><span data-stu-id="c52f8-188">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="c52f8-189">In this section, you create linked services to your on-premises SQL Server database and SQL database.</span><span class="sxs-lookup"><span data-stu-id="c52f8-189">In this section, you create linked services to your on-premises SQL Server database and SQL database.</span></span> 

### <a name="create-the-sql-server-linked-service"></a><span data-ttu-id="c52f8-190">Create the SQL Server linked service</span><span class="sxs-lookup"><span data-stu-id="c52f8-190">Create the SQL Server linked service</span></span>
<span data-ttu-id="c52f8-191">In this step, you link your on-premises SQL Server database to the data factory.</span><span class="sxs-lookup"><span data-stu-id="c52f8-191">In this step, you link your on-premises SQL Server database to the data factory.</span></span>

1. <span data-ttu-id="c52f8-192">Create a JSON file named SqlServerLinkedService.json in the C:\ADFTutorials\IncCopyMultiTableTutorial folder with the following content.</span><span class="sxs-lookup"><span data-stu-id="c52f8-192">Create a JSON file named SqlServerLinkedService.json in the C:\ADFTutorials\IncCopyMultiTableTutorial folder with the following content.</span></span> <span data-ttu-id="c52f8-193">Select the right section based on the authentication you use to connect to SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c52f8-193">Select the right section based on the authentication you use to connect to SQL Server.</span></span> <span data-ttu-id="c52f8-194">Create the local folders if they don't already exist.</span><span class="sxs-lookup"><span data-stu-id="c52f8-194">Create the local folders if they don't already exist.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="c52f8-195">Select the right section based on the authentication you use to connect to SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c52f8-195">Select the right section based on the authentication you use to connect to SQL Server.</span></span>

    <span data-ttu-id="c52f8-196">If you use SQL authentication, copy the following JSON definition:</span><span class="sxs-lookup"><span data-stu-id="c52f8-196">If you use SQL authentication, copy the following JSON definition:</span></span>

    ```json
    {
        "properties": {
            "type": "SqlServer",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "Server=<servername>;Database=<databasename>;User ID=<username>;Password=<password>;Timeout=60"
                }
            },
            "connectVia": {
                "type": "integrationRuntimeReference",
                "referenceName": "<integration runtime name>"
            }
        },
        "name": "SqlServerLinkedService"
    }
   ```    
    <span data-ttu-id="c52f8-197">If you use Windows authentication, copy the following JSON definition:</span><span class="sxs-lookup"><span data-stu-id="c52f8-197">If you use Windows authentication, copy the following JSON definition:</span></span>

    ```json
    {
        "properties": {
            "type": "SqlServer",
            "typeProperties": {
                "connectionString": {
                    "type": "SecureString",
                    "value": "Server=<server>;Database=<database>;Integrated Security=True"
                },
                "userName": "<user> or <domain>\\<user>",
                "password": {
                    "type": "SecureString",
                    "value": "<password>"
                }
            },
            "connectVia": {
                "type": "integrationRuntimeReference",
                "referenceName": "<integration runtime name>"
            }
        },
        "name": "SqlServerLinkedService"
    }    
    ```
    > [!IMPORTANT]
    > - <span data-ttu-id="c52f8-198">Select the right section based on the authentication you use to connect to SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c52f8-198">Select the right section based on the authentication you use to connect to SQL Server.</span></span>
    > - <span data-ttu-id="c52f8-199">Replace &lt;integration runtime name> with the name of your integration runtime.</span><span class="sxs-lookup"><span data-stu-id="c52f8-199">Replace &lt;integration runtime name> with the name of your integration runtime.</span></span>
    > - <span data-ttu-id="c52f8-200">Replace &lt;servername>, &lt;databasename>, &lt;username>, and &lt;password> with values of your SQL Server database before you save the file.</span><span class="sxs-lookup"><span data-stu-id="c52f8-200">Replace &lt;servername>, &lt;databasename>, &lt;username>, and &lt;password> with values of your SQL Server database before you save the file.</span></span>
    > - <span data-ttu-id="c52f8-201">If you need to use a slash character (`\`) in your user account or server name, use the escape character (`\`).</span><span class="sxs-lookup"><span data-stu-id="c52f8-201">If you need to use a slash character (`\`) in your user account or server name, use the escape character (`\`).</span></span> <span data-ttu-id="c52f8-202">An example is `mydomain\\myuser`.</span><span class="sxs-lookup"><span data-stu-id="c52f8-202">An example is `mydomain\\myuser`.</span></span>

1. <span data-ttu-id="c52f8-203">In PowerShell, switch to the C:\ADFTutorials\IncCopyMultiTableTutorial folder.</span><span class="sxs-lookup"><span data-stu-id="c52f8-203">In PowerShell, switch to the C:\ADFTutorials\IncCopyMultiTableTutorial folder.</span></span>

1. <span data-ttu-id="c52f8-204">Run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet to create the linked service AzureStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="c52f8-204">Run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet to create the linked service AzureStorageLinkedService.</span></span> <span data-ttu-id="c52f8-205">In the following example, you pass values for the *ResourceGroupName* and *DataFactoryName* parameters:</span><span class="sxs-lookup"><span data-stu-id="c52f8-205">In the following example, you pass values for the *ResourceGroupName* and *DataFactoryName* parameters:</span></span> 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SqlServerLinkedService" -File ".\SqlServerLinkedService.json"
    ```

    <span data-ttu-id="c52f8-206">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="c52f8-206">Here is the sample output:</span></span>

    ```json
    LinkedServiceName : SqlServerLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFIncMultiCopyTutorialFactory1201
    Properties        : Microsoft.Azure.Management.DataFactory.Models.SqlServerLinkedService
    ```

### <a name="create-the-sql-database-linked-service"></a><span data-ttu-id="c52f8-207">Create the SQL database linked service</span><span class="sxs-lookup"><span data-stu-id="c52f8-207">Create the SQL database linked service</span></span>
1. <span data-ttu-id="c52f8-208">Create a JSON file named AzureSQLDatabaseLinkedService.json in C:\ADFTutorials\IncCopyMultiTableTutorial folder with the following content.</span><span class="sxs-lookup"><span data-stu-id="c52f8-208">Create a JSON file named AzureSQLDatabaseLinkedService.json in C:\ADFTutorials\IncCopyMultiTableTutorial folder with the following content.</span></span> <span data-ttu-id="c52f8-209">(Create the folder ADF if it doesn't already exist.) Replace &lt;server&gt;, &lt;database name&gt;, &lt;user id&gt;, and &lt;password&gt; with the name of your SQL Server database, name of your database, user ID, and password before you save the file.</span><span class="sxs-lookup"><span data-stu-id="c52f8-209">(Create the folder ADF if it doesn't already exist.) Replace &lt;server&gt;, &lt;database name&gt;, &lt;user id&gt;, and &lt;password&gt; with the name of your SQL Server database, name of your database, user ID, and password before you save the file.</span></span> 

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
1. <span data-ttu-id="c52f8-210">In PowerShell, run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet to create the linked service AzureSQLDatabaseLinkedService.</span><span class="sxs-lookup"><span data-stu-id="c52f8-210">In PowerShell, run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet to create the linked service AzureSQLDatabaseLinkedService.</span></span> 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureSQLDatabaseLinkedService" -File ".\AzureSQLDatabaseLinkedService.json"
    ```

    <span data-ttu-id="c52f8-211">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="c52f8-211">Here is the sample output:</span></span>

    ```json
    LinkedServiceName : AzureSQLDatabaseLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFIncMultiCopyTutorialFactory1201
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlDatabaseLinkedService
    ```

## <a name="create-datasets"></a><span data-ttu-id="c52f8-212">Create datasets</span><span class="sxs-lookup"><span data-stu-id="c52f8-212">Create datasets</span></span>
<span data-ttu-id="c52f8-213">In this step, you create datasets to represent the data source, the data destination, and the place to store the watermark.</span><span class="sxs-lookup"><span data-stu-id="c52f8-213">In this step, you create datasets to represent the data source, the data destination, and the place to store the watermark.</span></span>

### <a name="create-a-source-dataset"></a><span data-ttu-id="c52f8-214">Create a source dataset</span><span class="sxs-lookup"><span data-stu-id="c52f8-214">Create a source dataset</span></span>

1. <span data-ttu-id="c52f8-215">Create a JSON file named SourceDataset.json in the same folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="c52f8-215">Create a JSON file named SourceDataset.json in the same folder with the following content:</span></span> 

    ```json
    {
        "name": "SourceDataset",
        "properties": {
            "type": "SqlServerTable",
            "typeProperties": {
                "tableName": "dummyName"
            },
            "linkedServiceName": {
                "referenceName": "SqlServerLinkedService",
                "type": "LinkedServiceReference"
            }
        }
    }
   
    ```

    <span data-ttu-id="c52f8-216">The table name is a dummy name.</span><span class="sxs-lookup"><span data-stu-id="c52f8-216">The table name is a dummy name.</span></span> <span data-ttu-id="c52f8-217">The Copy activity in the pipeline uses a SQL query to load the data rather than load the entire table.</span><span class="sxs-lookup"><span data-stu-id="c52f8-217">The Copy activity in the pipeline uses a SQL query to load the data rather than load the entire table.</span></span>

1. <span data-ttu-id="c52f8-218">Run the **Set-AzureRmDataFactoryV2Dataset** cmdlet to create the dataset SourceDataset.</span><span class="sxs-lookup"><span data-stu-id="c52f8-218">Run the **Set-AzureRmDataFactoryV2Dataset** cmdlet to create the dataset SourceDataset.</span></span>
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SourceDataset" -File ".\SourceDataset.json"
    ```

    <span data-ttu-id="c52f8-219">Here is the sample output of the cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c52f8-219">Here is the sample output of the cmdlet:</span></span>
    
    ```json
    DatasetName       : SourceDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFIncMultiCopyTutorialFactory1201
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.SqlServerTableDataset
    ```

### <a name="create-a-sink-dataset"></a><span data-ttu-id="c52f8-220">Create a sink dataset</span><span class="sxs-lookup"><span data-stu-id="c52f8-220">Create a sink dataset</span></span>

1. <span data-ttu-id="c52f8-221">Create a JSON file named SinkDataset.json in the same folder with the following content.</span><span class="sxs-lookup"><span data-stu-id="c52f8-221">Create a JSON file named SinkDataset.json in the same folder with the following content.</span></span> <span data-ttu-id="c52f8-222">The tableName element is set by the pipeline dynamically at runtime.</span><span class="sxs-lookup"><span data-stu-id="c52f8-222">The tableName element is set by the pipeline dynamically at runtime.</span></span> <span data-ttu-id="c52f8-223">The ForEach activity in the pipeline iterates through a list of table names and passes the table name to this dataset in each iteration.</span><span class="sxs-lookup"><span data-stu-id="c52f8-223">The ForEach activity in the pipeline iterates through a list of table names and passes the table name to this dataset in each iteration.</span></span> 

    ```json
    {
        "name": "SinkDataset",
        "properties": {
            "type": "AzureSqlTable",
            "typeProperties": {
                "tableName": {
                    "value": "@{dataset().SinkTableName}",
                    "type": "Expression"
                }
            },
            "linkedServiceName": {
                "referenceName": "AzureSQLDatabaseLinkedService",
                "type": "LinkedServiceReference"
            },
            "parameters": {
                "SinkTableName": {
                    "type": "String"
                }
            }
        }
    }
    ```

1. <span data-ttu-id="c52f8-224">Run the **Set-AzureRmDataFactoryV2Dataset** cmdlet to create the dataset SinkDataset.</span><span class="sxs-lookup"><span data-stu-id="c52f8-224">Run the **Set-AzureRmDataFactoryV2Dataset** cmdlet to create the dataset SinkDataset.</span></span>
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SinkDataset" -File ".\SinkDataset.json"
    ```

    <span data-ttu-id="c52f8-225">Here is the sample output of the cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c52f8-225">Here is the sample output of the cmdlet:</span></span>
    
    ```json
    DatasetName       : SinkDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFIncMultiCopyTutorialFactory1201
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlTableDataset
    ```

### <a name="create-a-dataset-for-a-watermark"></a><span data-ttu-id="c52f8-226">Create a dataset for a watermark</span><span class="sxs-lookup"><span data-stu-id="c52f8-226">Create a dataset for a watermark</span></span>
<span data-ttu-id="c52f8-227">In this step, you create a dataset for storing a high watermark value.</span><span class="sxs-lookup"><span data-stu-id="c52f8-227">In this step, you create a dataset for storing a high watermark value.</span></span> 

1. <span data-ttu-id="c52f8-228">Create a JSON file named WatermarkDataset.json in the same folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="c52f8-228">Create a JSON file named WatermarkDataset.json in the same folder with the following content:</span></span> 

    ```json
    {
        "name": " WatermarkDataset ",
        "properties": {
            "type": "AzureSqlTable",
            "typeProperties": {
                "tableName": "watermarktable"
            },
            "linkedServiceName": {
                "referenceName": "AzureSQLDatabaseLinkedService",
                "type": "LinkedServiceReference"
            }
        }
    }    
    ```
1. <span data-ttu-id="c52f8-229">Run the **Set-AzureRmDataFactoryV2Dataset** cmdlet to create the dataset WatermarkDataset.</span><span class="sxs-lookup"><span data-stu-id="c52f8-229">Run the **Set-AzureRmDataFactoryV2Dataset** cmdlet to create the dataset WatermarkDataset.</span></span>
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "WatermarkDataset" -File ".\WatermarkDataset.json"
    ```

    <span data-ttu-id="c52f8-230">Here is the sample output of the cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c52f8-230">Here is the sample output of the cmdlet:</span></span>
    
    ```json
    DatasetName       : WatermarkDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : <data factory name>
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlTableDataset    
    ```

## <a name="create-a-pipeline"></a><span data-ttu-id="c52f8-231">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="c52f8-231">Create a pipeline</span></span>
<span data-ttu-id="c52f8-232">The pipeline takes a list of table names as a parameter.</span><span class="sxs-lookup"><span data-stu-id="c52f8-232">The pipeline takes a list of table names as a parameter.</span></span> <span data-ttu-id="c52f8-233">The ForEach activity iterates through the list of table names and performs the following operations:</span><span class="sxs-lookup"><span data-stu-id="c52f8-233">The ForEach activity iterates through the list of table names and performs the following operations:</span></span> 

1. <span data-ttu-id="c52f8-234">Use the Lookup activity to retrieve the old watermark value (the initial value or the one that was used in the last iteration).</span><span class="sxs-lookup"><span data-stu-id="c52f8-234">Use the Lookup activity to retrieve the old watermark value (the initial value or the one that was used in the last iteration).</span></span>

1. <span data-ttu-id="c52f8-235">Use the Lookup activity to retrieve the new watermark value (the maximum value of the watermark column in the source table).</span><span class="sxs-lookup"><span data-stu-id="c52f8-235">Use the Lookup activity to retrieve the new watermark value (the maximum value of the watermark column in the source table).</span></span>

1. <span data-ttu-id="c52f8-236">Use the Copy activity to copy data between these two watermark values from the source database to the destination database.</span><span class="sxs-lookup"><span data-stu-id="c52f8-236">Use the Copy activity to copy data between these two watermark values from the source database to the destination database.</span></span>

1. <span data-ttu-id="c52f8-237">Use the StoredProcedure activity to update the old watermark value to be used in the first step of the next iteration.</span><span class="sxs-lookup"><span data-stu-id="c52f8-237">Use the StoredProcedure activity to update the old watermark value to be used in the first step of the next iteration.</span></span> 

### <a name="create-the-pipeline"></a><span data-ttu-id="c52f8-238">Create the pipeline</span><span class="sxs-lookup"><span data-stu-id="c52f8-238">Create the pipeline</span></span>
1. <span data-ttu-id="c52f8-239">Create a JSON file named IncrementalCopyPipeline.json in the same folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="c52f8-239">Create a JSON file named IncrementalCopyPipeline.json in the same folder with the following content:</span></span> 

    ```json
    {
        "name": "IncrementalCopyPipeline",
        "properties": {
            "activities": [{
    
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
                            "name": "LookupOldWaterMarkActivity",
                            "type": "Lookup",
                            "typeProperties": {
                                "source": {
                                    "type": "SqlSource",
                                    "sqlReaderQuery": "select * from watermarktable where TableName  =  '@{item().TABLE_NAME}'"
                                },
    
                                "dataset": {
                                    "referenceName": "WatermarkDataset",
                                    "type": "DatasetReference"
                                }
                            }
                        },
                        {
                            "name": "LookupNewWaterMarkActivity",
                            "type": "Lookup",
                            "typeProperties": {
                                "source": {
                                    "type": "SqlSource",
                                    "sqlReaderQuery": "select MAX(@{item().WaterMark_Column}) as NewWatermarkvalue from @{item().TABLE_NAME}"
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
                                    "sqlReaderQuery": "select * from @{item().TABLE_NAME} where @{item().WaterMark_Column} > '@{activity('LookupOldWaterMarkActivity').output.firstRow.WatermarkValue}' and @{item().WaterMark_Column} <= '@{activity('LookupNewWaterMarkActivity').output.firstRow.NewWatermarkvalue}'"
                                },
                                "sink": {
                                    "type": "SqlSink",
                                    "SqlWriterTableType": "@{item().TableType}",
                                    "SqlWriterStoredProcedureName": "@{item().StoredProcedureNameForMergeOperation}"
                                }
                            },
                            "dependsOn": [{
                                    "activity": "LookupNewWaterMarkActivity",
                                    "dependencyConditions": [
                                        "Succeeded"
                                    ]
                                },
                                {
                                    "activity": "LookupOldWaterMarkActivity",
                                    "dependencyConditions": [
                                        "Succeeded"
                                    ]
                                }
                            ],
    
                            "inputs": [{
                                "referenceName": "SourceDataset",
                                "type": "DatasetReference"
                            }],
                            "outputs": [{
                                "referenceName": "SinkDataset",
                                "type": "DatasetReference",
                                "parameters": {
                                    "SinkTableName": "@{item().TABLE_NAME}"
                                }
                            }]
                        },
    
                        {
                            "name": "StoredProceduretoWriteWatermarkActivity",
                            "type": "SqlServerStoredProcedure",
                            "typeProperties": {
    
                                "storedProcedureName": "sp_write_watermark",
                                "storedProcedureParameters": {
                                    "LastModifiedtime": {
                                        "value": "@{activity('LookupNewWaterMarkActivity').output.firstRow.NewWatermarkvalue}",
                                        "type": "datetime"
                                    },
                                    "TableName": {
                                        "value": "@{activity('LookupOldWaterMarkActivity').output.firstRow.TableName}",
                                        "type": "String"
                                    }
                                }
                            },
    
                            "linkedServiceName": {
                                "referenceName": "AzureSQLDatabaseLinkedService",
                                "type": "LinkedServiceReference"
                            },
    
                            "dependsOn": [{
                                "activity": "IncrementalCopyActivity",
                                "dependencyConditions": [
                                    "Succeeded"
                                ]
                            }]
                        }
    
                    ]
    
                }
            }],
    
            "parameters": {
                "tableList": {
                    "type": "Object"
                }
            }
        }
    }
    ```
1. <span data-ttu-id="c52f8-240">Run the **Set-AzureRmDataFactoryV2Pipeline** cmdlet to create the pipeline IncrementalCopyPipeline.</span><span class="sxs-lookup"><span data-stu-id="c52f8-240">Run the **Set-AzureRmDataFactoryV2Pipeline** cmdlet to create the pipeline IncrementalCopyPipeline.</span></span>
    
   ```powershell
   Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "IncrementalCopyPipeline" -File ".\IncrementalCopyPipeline.json"
   ``` 

   <span data-ttu-id="c52f8-241">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="c52f8-241">Here is the sample output:</span></span> 

   ```json
    PipelineName      : IncrementalCopyPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFIncMultiCopyTutorialFactory1201
    Activities        : {IterateSQLTables}
    Parameters        : {[tableList, Microsoft.Azure.Management.DataFactory.Models.ParameterSpecification]}
   ```
 
## <a name="run-the-pipeline"></a><span data-ttu-id="c52f8-242">Run the pipeline</span><span class="sxs-lookup"><span data-stu-id="c52f8-242">Run the pipeline</span></span>

1. <span data-ttu-id="c52f8-243">Create a parameter file named Parameters.json in the same folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="c52f8-243">Create a parameter file named Parameters.json in the same folder with the following content:</span></span>

    ```json
    {
        "tableList": 
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
    }
    ```
1. <span data-ttu-id="c52f8-244">Run the pipeline IncrementalCopyPipeline by using the **Invoke-AzureRmDataFactoryV2Pipeline** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c52f8-244">Run the pipeline IncrementalCopyPipeline by using the **Invoke-AzureRmDataFactoryV2Pipeline** cmdlet.</span></span> <span data-ttu-id="c52f8-245">Replace placeholders with your own resource group and data factory name.</span><span class="sxs-lookup"><span data-stu-id="c52f8-245">Replace placeholders with your own resource group and data factory name.</span></span>

    ```powershell
    $RunId = Invoke-AzureRmDataFactoryV2Pipeline -PipelineName "IncrementalCopyPipeline" -ResourceGroup $resourceGroupName -dataFactoryName $dataFactoryName -ParameterFile ".\Parameters.json"        
    ``` 

## <a name="monitor-the-pipeline"></a><span data-ttu-id="c52f8-246">Monitor the pipeline</span><span class="sxs-lookup"><span data-stu-id="c52f8-246">Monitor the pipeline</span></span>

1. <span data-ttu-id="c52f8-247">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c52f8-247">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="c52f8-248">Select **All services**, search with the keyword *Data factories*, and select **Data factories**.</span><span class="sxs-lookup"><span data-stu-id="c52f8-248">Select **All services**, search with the keyword *Data factories*, and select **Data factories**.</span></span> 

    ![Data factories menu](media\tutorial-incremental-copy-multiple-tables-powershell\monitor-data-factories-menu-1.png)

1. <span data-ttu-id="c52f8-250">Search for your data factory in the list of data factories, and select it to open the **Data factory** page.</span><span class="sxs-lookup"><span data-stu-id="c52f8-250">Search for your data factory in the list of data factories, and select it to open the **Data factory** page.</span></span> 

    ![Search for your data factory](media\tutorial-incremental-copy-multiple-tables-powershell\monitor-search-data-factory-2.png)

1. <span data-ttu-id="c52f8-252">On the **Data factory** page, select **Monitor & Manage**.</span><span class="sxs-lookup"><span data-stu-id="c52f8-252">On the **Data factory** page, select **Monitor & Manage**.</span></span> 

    ![Monitor & Manage tile](media\tutorial-incremental-copy-multiple-tables-powershell\monitor-monitor-manage-tile-3.png)

1. <span data-ttu-id="c52f8-254">The **Data Integration Application** opens in a separate tab. You can see all the pipeline runs and their status.</span><span class="sxs-lookup"><span data-stu-id="c52f8-254">The **Data Integration Application** opens in a separate tab. You can see all the pipeline runs and their status.</span></span> <span data-ttu-id="c52f8-255">Notice that in the following example, the status of the pipeline run is **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="c52f8-255">Notice that in the following example, the status of the pipeline run is **Succeeded**.</span></span> <span data-ttu-id="c52f8-256">To check parameters passed to the pipeline, select the link in the **Parameters** column.</span><span class="sxs-lookup"><span data-stu-id="c52f8-256">To check parameters passed to the pipeline, select the link in the **Parameters** column.</span></span> <span data-ttu-id="c52f8-257">If an error occurred, you see a link in the **Error** column.</span><span class="sxs-lookup"><span data-stu-id="c52f8-257">If an error occurred, you see a link in the **Error** column.</span></span> <span data-ttu-id="c52f8-258">Select the link in the **Actions** column.</span><span class="sxs-lookup"><span data-stu-id="c52f8-258">Select the link in the **Actions** column.</span></span> 

    ![Pipeline Runs](media\tutorial-incremental-copy-multiple-tables-powershell\monitor-pipeline-runs-4.png)    
1. <span data-ttu-id="c52f8-260">When you select the link in the **Actions** column, you see the following page that shows all the activity runs for the pipeline:</span><span class="sxs-lookup"><span data-stu-id="c52f8-260">When you select the link in the **Actions** column, you see the following page that shows all the activity runs for the pipeline:</span></span> 

    ![Activity Runs](media\tutorial-incremental-copy-multiple-tables-powershell\monitor-activity-runs-5.png)

1. <span data-ttu-id="c52f8-262">To go back to the **Pipeline Runs** view, select **Pipelines** as shown in the image.</span><span class="sxs-lookup"><span data-stu-id="c52f8-262">To go back to the **Pipeline Runs** view, select **Pipelines** as shown in the image.</span></span> 

## <a name="review-the-results"></a><span data-ttu-id="c52f8-263">Review the results</span><span class="sxs-lookup"><span data-stu-id="c52f8-263">Review the results</span></span>
<span data-ttu-id="c52f8-264">In SQL Server Management Studio, run the following queries against the target SQL database to verify that the data was copied from source tables to destination tables:</span><span class="sxs-lookup"><span data-stu-id="c52f8-264">In SQL Server Management Studio, run the following queries against the target SQL database to verify that the data was copied from source tables to destination tables:</span></span> 

<span data-ttu-id="c52f8-265">**Query**</span><span class="sxs-lookup"><span data-stu-id="c52f8-265">**Query**</span></span> 
```sql
select * from customer_table
```

<span data-ttu-id="c52f8-266">**Output**</span><span class="sxs-lookup"><span data-stu-id="c52f8-266">**Output**</span></span>
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

<span data-ttu-id="c52f8-267">**Query**</span><span class="sxs-lookup"><span data-stu-id="c52f8-267">**Query**</span></span>

```sql
select * from project_table
```

<span data-ttu-id="c52f8-268">**Output**</span><span class="sxs-lookup"><span data-stu-id="c52f8-268">**Output**</span></span>

```
===================================
Project     Creationtime
===================================
project1    2015-01-01 00:00:00.000
project2    2016-02-02 01:23:00.000
project3    2017-03-04 05:16:00.000
```

<span data-ttu-id="c52f8-269">**Query**</span><span class="sxs-lookup"><span data-stu-id="c52f8-269">**Query**</span></span>

```sql
select * from watermarktable
```

<span data-ttu-id="c52f8-270">**Output**</span><span class="sxs-lookup"><span data-stu-id="c52f8-270">**Output**</span></span>

```
======================================
TableName       WatermarkValue
======================================
customer_table  2017-09-05 08:06:00.000
project_table   2017-03-04 05:16:00.000
```

<span data-ttu-id="c52f8-271">Notice that the watermark values for both tables were updated.</span><span class="sxs-lookup"><span data-stu-id="c52f8-271">Notice that the watermark values for both tables were updated.</span></span> 

## <a name="add-more-data-to-the-source-tables"></a><span data-ttu-id="c52f8-272">Add more data to the source tables</span><span class="sxs-lookup"><span data-stu-id="c52f8-272">Add more data to the source tables</span></span>

<span data-ttu-id="c52f8-273">Run the following query against the source SQL Server database to update an existing row in customer_table.</span><span class="sxs-lookup"><span data-stu-id="c52f8-273">Run the following query against the source SQL Server database to update an existing row in customer_table.</span></span> <span data-ttu-id="c52f8-274">Insert a new row into project_table.</span><span class="sxs-lookup"><span data-stu-id="c52f8-274">Insert a new row into project_table.</span></span> 

```sql
UPDATE customer_table
SET [LastModifytime] = '2017-09-08T00:00:00Z', [name]='NewName' where [PersonID] = 3

INSERT INTO project_table
(Project, Creationtime)
VALUES
('NewProject','10/1/2017 0:00:00 AM');
``` 

## <a name="rerun-the-pipeline"></a><span data-ttu-id="c52f8-275">Rerun the pipeline</span><span class="sxs-lookup"><span data-stu-id="c52f8-275">Rerun the pipeline</span></span>

1. <span data-ttu-id="c52f8-276">Now, rerun the pipeline by executing the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="c52f8-276">Now, rerun the pipeline by executing the following PowerShell command:</span></span>

    ```powershell
    $RunId = Invoke-AzureRmDataFactoryV2Pipeline -PipelineName "IncrementalCopyPipeline" -ResourceGroup $resourceGroupname -dataFactoryName $dataFactoryName -ParameterFile ".\Parameters.json"
    ```
1. <span data-ttu-id="c52f8-277">Monitor the pipeline runs by following the instructions in the [Monitor the pipeline](#monitor-the-pipeline) section.</span><span class="sxs-lookup"><span data-stu-id="c52f8-277">Monitor the pipeline runs by following the instructions in the [Monitor the pipeline](#monitor-the-pipeline) section.</span></span> <span data-ttu-id="c52f8-278">Because the pipeline status is **In Progress**, you see another action link under **Actions** to cancel the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="c52f8-278">Because the pipeline status is **In Progress**, you see another action link under **Actions** to cancel the pipeline run.</span></span> 

    ![In Progress pipeline runs](media\tutorial-incremental-copy-multiple-tables-powershell\monitor-pipeline-runs-6.png)

1. <span data-ttu-id="c52f8-280">Select **Refresh** to refresh the list until the pipeline run succeeds.</span><span class="sxs-lookup"><span data-stu-id="c52f8-280">Select **Refresh** to refresh the list until the pipeline run succeeds.</span></span> 

    ![Refresh pipeline runs](media\tutorial-incremental-copy-multiple-tables-powershell\monitor-pipeline-runs-succeded-7.png)

1. <span data-ttu-id="c52f8-282">Optionally, select the **View Activity Runs** link under **Actions** to see all the activity runs associated with this pipeline run.</span><span class="sxs-lookup"><span data-stu-id="c52f8-282">Optionally, select the **View Activity Runs** link under **Actions** to see all the activity runs associated with this pipeline run.</span></span> 

## <a name="review-the-final-results"></a><span data-ttu-id="c52f8-283">Review the final results</span><span class="sxs-lookup"><span data-stu-id="c52f8-283">Review the final results</span></span>
<span data-ttu-id="c52f8-284">In SQL Server Management Studio, run the following queries against the target database to verify that the updated/new data was copied from source tables to destination tables.</span><span class="sxs-lookup"><span data-stu-id="c52f8-284">In SQL Server Management Studio, run the following queries against the target database to verify that the updated/new data was copied from source tables to destination tables.</span></span> 

<span data-ttu-id="c52f8-285">**Query**</span><span class="sxs-lookup"><span data-stu-id="c52f8-285">**Query**</span></span> 
```sql
select * from customer_table
```

<span data-ttu-id="c52f8-286">**Output**</span><span class="sxs-lookup"><span data-stu-id="c52f8-286">**Output**</span></span>
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

<span data-ttu-id="c52f8-287">Notice the new values of **Name** and **LastModifytime** for the **PersonID** for number 3.</span><span class="sxs-lookup"><span data-stu-id="c52f8-287">Notice the new values of **Name** and **LastModifytime** for the **PersonID** for number 3.</span></span> 

<span data-ttu-id="c52f8-288">**Query**</span><span class="sxs-lookup"><span data-stu-id="c52f8-288">**Query**</span></span>

```sql
select * from project_table
```

<span data-ttu-id="c52f8-289">**Output**</span><span class="sxs-lookup"><span data-stu-id="c52f8-289">**Output**</span></span>

```
===================================
Project     Creationtime
===================================
project1    2015-01-01 00:00:00.000
project2    2016-02-02 01:23:00.000
project3    2017-03-04 05:16:00.000
NewProject  2017-10-01 00:00:00.000
```

<span data-ttu-id="c52f8-290">Notice that the **NewProject** entry was added to project_table.</span><span class="sxs-lookup"><span data-stu-id="c52f8-290">Notice that the **NewProject** entry was added to project_table.</span></span> 

<span data-ttu-id="c52f8-291">**Query**</span><span class="sxs-lookup"><span data-stu-id="c52f8-291">**Query**</span></span>

```sql
select * from watermarktable
```

<span data-ttu-id="c52f8-292">**Output**</span><span class="sxs-lookup"><span data-stu-id="c52f8-292">**Output**</span></span>

```
======================================
TableName       WatermarkValue
======================================
customer_table  2017-09-08 00:00:00.000
project_table   2017-10-01 00:00:00.000
```

<span data-ttu-id="c52f8-293">Notice that the watermark values for both tables were updated.</span><span class="sxs-lookup"><span data-stu-id="c52f8-293">Notice that the watermark values for both tables were updated.</span></span>
     
## <a name="next-steps"></a><span data-ttu-id="c52f8-294">Next steps</span><span class="sxs-lookup"><span data-stu-id="c52f8-294">Next steps</span></span>
<span data-ttu-id="c52f8-295">You performed the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="c52f8-295">You performed the following steps in this tutorial:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="c52f8-296">Prepare source and destination data stores.</span><span class="sxs-lookup"><span data-stu-id="c52f8-296">Prepare source and destination data stores.</span></span>
> * <span data-ttu-id="c52f8-297">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="c52f8-297">Create a data factory.</span></span>
> * <span data-ttu-id="c52f8-298">Create a self-hosted integration runtime (IR).</span><span class="sxs-lookup"><span data-stu-id="c52f8-298">Create a self-hosted integration runtime (IR).</span></span>
> * <span data-ttu-id="c52f8-299">Install the integration runtime.</span><span class="sxs-lookup"><span data-stu-id="c52f8-299">Install the integration runtime.</span></span>
> * <span data-ttu-id="c52f8-300">Create linked services.</span><span class="sxs-lookup"><span data-stu-id="c52f8-300">Create linked services.</span></span> 
> * <span data-ttu-id="c52f8-301">Create source, sink, and watermark datasets.</span><span class="sxs-lookup"><span data-stu-id="c52f8-301">Create source, sink, and watermark datasets.</span></span>
> * <span data-ttu-id="c52f8-302">Create, run, and monitor a pipeline.</span><span class="sxs-lookup"><span data-stu-id="c52f8-302">Create, run, and monitor a pipeline.</span></span>
> * <span data-ttu-id="c52f8-303">Review the results.</span><span class="sxs-lookup"><span data-stu-id="c52f8-303">Review the results.</span></span>
> * <span data-ttu-id="c52f8-304">Add or update data in source tables.</span><span class="sxs-lookup"><span data-stu-id="c52f8-304">Add or update data in source tables.</span></span>
> * <span data-ttu-id="c52f8-305">Rerun and monitor the pipeline.</span><span class="sxs-lookup"><span data-stu-id="c52f8-305">Rerun and monitor the pipeline.</span></span>
> * <span data-ttu-id="c52f8-306">Review the final results.</span><span class="sxs-lookup"><span data-stu-id="c52f8-306">Review the final results.</span></span>

<span data-ttu-id="c52f8-307">Advance to the following tutorial to learn about transforming data by using a Spark cluster on Azure:</span><span class="sxs-lookup"><span data-stu-id="c52f8-307">Advance to the following tutorial to learn about transforming data by using a Spark cluster on Azure:</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="c52f8-308">Incrementally load data from Azure SQL Database to Azure Blob storage by using Change Tracking technology</span><span class="sxs-lookup"><span data-stu-id="c52f8-308">Incrementally load data from Azure SQL Database to Azure Blob storage by using Change Tracking technology</span></span>](tutorial-incremental-copy-change-tracking-feature-powershell.md)


