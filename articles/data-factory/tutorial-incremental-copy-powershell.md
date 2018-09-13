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
ms.date: 01/22/2018
ms.author: yexu
ms.openlocfilehash: 08bce244dc4eafcd423123b1230fe4aa8b4ed04e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868566"
---
# <a name="incrementally-load-data-from-an-azure-sql-database-to-azure-blob-storage"></a><span data-ttu-id="96caf-103">Incrementally load data from an Azure SQL database to Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="96caf-103">Incrementally load data from an Azure SQL database to Azure Blob storage</span></span>
<span data-ttu-id="96caf-104">In this tutorial, you create an Azure data factory with a pipeline that loads delta data from a table in an Azure SQL database to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="96caf-104">In this tutorial, you create an Azure data factory with a pipeline that loads delta data from a table in an Azure SQL database to Azure Blob storage.</span></span> 

<span data-ttu-id="96caf-105">You perform the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="96caf-105">You perform the following steps in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="96caf-106">Prepare the data store to store the watermark value.</span><span class="sxs-lookup"><span data-stu-id="96caf-106">Prepare the data store to store the watermark value.</span></span>
> * <span data-ttu-id="96caf-107">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="96caf-107">Create a data factory.</span></span>
> * <span data-ttu-id="96caf-108">Create linked services.</span><span class="sxs-lookup"><span data-stu-id="96caf-108">Create linked services.</span></span> 
> * <span data-ttu-id="96caf-109">Create source, sink, and watermark datasets.</span><span class="sxs-lookup"><span data-stu-id="96caf-109">Create source, sink, and watermark datasets.</span></span>
> * <span data-ttu-id="96caf-110">Create a pipeline.</span><span class="sxs-lookup"><span data-stu-id="96caf-110">Create a pipeline.</span></span>
> * <span data-ttu-id="96caf-111">Run the pipeline.</span><span class="sxs-lookup"><span data-stu-id="96caf-111">Run the pipeline.</span></span>
> * <span data-ttu-id="96caf-112">Monitor the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="96caf-112">Monitor the pipeline run.</span></span> 

## <a name="overview"></a><span data-ttu-id="96caf-113">Overview</span><span class="sxs-lookup"><span data-stu-id="96caf-113">Overview</span></span>
<span data-ttu-id="96caf-114">Here is the high-level solution diagram:</span><span class="sxs-lookup"><span data-stu-id="96caf-114">Here is the high-level solution diagram:</span></span> 

![Incrementally load data](media\tutorial-Incrementally-copy-powershell\incrementally-load.png)

<span data-ttu-id="96caf-116">Here are the important steps to create this solution:</span><span class="sxs-lookup"><span data-stu-id="96caf-116">Here are the important steps to create this solution:</span></span> 

1. <span data-ttu-id="96caf-117">**Select the watermark column**.</span><span class="sxs-lookup"><span data-stu-id="96caf-117">**Select the watermark column**.</span></span>
    <span data-ttu-id="96caf-118">Select one column in the source data store, which can be used to slice the new or updated records for every run.</span><span class="sxs-lookup"><span data-stu-id="96caf-118">Select one column in the source data store, which can be used to slice the new or updated records for every run.</span></span> <span data-ttu-id="96caf-119">Normally, the data in this selected column (for example, last_modify_time or ID) keeps increasing when rows are created or updated.</span><span class="sxs-lookup"><span data-stu-id="96caf-119">Normally, the data in this selected column (for example, last_modify_time or ID) keeps increasing when rows are created or updated.</span></span> <span data-ttu-id="96caf-120">The maximum value in this column is used as a watermark.</span><span class="sxs-lookup"><span data-stu-id="96caf-120">The maximum value in this column is used as a watermark.</span></span>

2. <span data-ttu-id="96caf-121">**Prepare a data store to store the watermark value**.</span><span class="sxs-lookup"><span data-stu-id="96caf-121">**Prepare a data store to store the watermark value**.</span></span>   
    <span data-ttu-id="96caf-122">In this tutorial, you store the watermark value in a SQL database.</span><span class="sxs-lookup"><span data-stu-id="96caf-122">In this tutorial, you store the watermark value in a SQL database.</span></span>
    
3. <span data-ttu-id="96caf-123">**Create a pipeline with the following workflow**:</span><span class="sxs-lookup"><span data-stu-id="96caf-123">**Create a pipeline with the following workflow**:</span></span> 
    
    <span data-ttu-id="96caf-124">The pipeline in this solution has the following activities:</span><span class="sxs-lookup"><span data-stu-id="96caf-124">The pipeline in this solution has the following activities:</span></span>
  
    * <span data-ttu-id="96caf-125">Create two Lookup activities.</span><span class="sxs-lookup"><span data-stu-id="96caf-125">Create two Lookup activities.</span></span> <span data-ttu-id="96caf-126">Use the first Lookup activity to retrieve the last watermark value.</span><span class="sxs-lookup"><span data-stu-id="96caf-126">Use the first Lookup activity to retrieve the last watermark value.</span></span> <span data-ttu-id="96caf-127">Use the second Lookup activity to retrieve the new watermark value.</span><span class="sxs-lookup"><span data-stu-id="96caf-127">Use the second Lookup activity to retrieve the new watermark value.</span></span> <span data-ttu-id="96caf-128">These watermark values are passed to the Copy activity.</span><span class="sxs-lookup"><span data-stu-id="96caf-128">These watermark values are passed to the Copy activity.</span></span> 
    * <span data-ttu-id="96caf-129">Create a Copy activity that copies rows from the source data store with the value of the watermark column greater than the old watermark value and less than the new watermark value.</span><span class="sxs-lookup"><span data-stu-id="96caf-129">Create a Copy activity that copies rows from the source data store with the value of the watermark column greater than the old watermark value and less than the new watermark value.</span></span> <span data-ttu-id="96caf-130">Then, it copies the delta data from the source data store to Blob storage as a new file.</span><span class="sxs-lookup"><span data-stu-id="96caf-130">Then, it copies the delta data from the source data store to Blob storage as a new file.</span></span> 
    * <span data-ttu-id="96caf-131">Create a StoredProcedure activity that updates the watermark value for the pipeline that runs next time.</span><span class="sxs-lookup"><span data-stu-id="96caf-131">Create a StoredProcedure activity that updates the watermark value for the pipeline that runs next time.</span></span> 


<span data-ttu-id="96caf-132">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="96caf-132">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96caf-133">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="96caf-133">Prerequisites</span></span>
* <span data-ttu-id="96caf-134">**Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="96caf-134">**Azure SQL Database**.</span></span> <span data-ttu-id="96caf-135">You use the database as the source data store.</span><span class="sxs-lookup"><span data-stu-id="96caf-135">You use the database as the source data store.</span></span> <span data-ttu-id="96caf-136">If you don't have a SQL database, see [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="96caf-136">If you don't have a SQL database, see [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) for steps to create one.</span></span>
* <span data-ttu-id="96caf-137">**Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="96caf-137">**Azure Storage**.</span></span> <span data-ttu-id="96caf-138">You use the blob storage as the sink data store.</span><span class="sxs-lookup"><span data-stu-id="96caf-138">You use the blob storage as the sink data store.</span></span> <span data-ttu-id="96caf-139">If you don't have a storage account, see [Create a storage account](../storage/common/storage-quickstart-create-account.md) for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="96caf-139">If you don't have a storage account, see [Create a storage account](../storage/common/storage-quickstart-create-account.md) for steps to create one.</span></span> <span data-ttu-id="96caf-140">Create a container named adftutorial.</span><span class="sxs-lookup"><span data-stu-id="96caf-140">Create a container named adftutorial.</span></span> 
* <span data-ttu-id="96caf-141">**Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="96caf-141">**Azure PowerShell**.</span></span> <span data-ttu-id="96caf-142">Follow the instructions in [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="96caf-142">Follow the instructions in [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>

### <a name="create-a-data-source-table-in-your-sql-database"></a><span data-ttu-id="96caf-143">Create a data source table in your SQL database</span><span class="sxs-lookup"><span data-stu-id="96caf-143">Create a data source table in your SQL database</span></span>
1. <span data-ttu-id="96caf-144">Open SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="96caf-144">Open SQL Server Management Studio.</span></span> <span data-ttu-id="96caf-145">In **Server Explorer**, right-click the database, and choose **New Query**.</span><span class="sxs-lookup"><span data-stu-id="96caf-145">In **Server Explorer**, right-click the database, and choose **New Query**.</span></span>

2. <span data-ttu-id="96caf-146">Run the following SQL command against your SQL database to create a table named `data_source_table` as the data source store:</span><span class="sxs-lookup"><span data-stu-id="96caf-146">Run the following SQL command against your SQL database to create a table named `data_source_table` as the data source store:</span></span> 
    
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
    <span data-ttu-id="96caf-147">In this tutorial, you use LastModifytime as the watermark column.</span><span class="sxs-lookup"><span data-stu-id="96caf-147">In this tutorial, you use LastModifytime as the watermark column.</span></span> <span data-ttu-id="96caf-148">The data in the data source store is shown in the following table:</span><span class="sxs-lookup"><span data-stu-id="96caf-148">The data in the data source store is shown in the following table:</span></span>

    ```
    PersonID | Name | LastModifytime
    -------- | ---- | --------------
    1 | aaaa | 2017-09-01 00:56:00.000
    2 | bbbb | 2017-09-02 05:23:00.000
    3 | cccc | 2017-09-03 02:36:00.000
    4 | dddd | 2017-09-04 03:21:00.000
    5 | eeee | 2017-09-05 08:06:00.000
    ```

### <a name="create-another-table-in-your-sql-database-to-store-the-high-watermark-value"></a><span data-ttu-id="96caf-149">Create another table in your SQL database to store the high watermark value</span><span class="sxs-lookup"><span data-stu-id="96caf-149">Create another table in your SQL database to store the high watermark value</span></span>
1. <span data-ttu-id="96caf-150">Run the following SQL command against your SQL database to create a table named `watermarktable` to store the watermark value:</span><span class="sxs-lookup"><span data-stu-id="96caf-150">Run the following SQL command against your SQL database to create a table named `watermarktable` to store the watermark value:</span></span>  
    
    ```sql
    create table watermarktable
    (
    
    TableName varchar(255),
    WatermarkValue datetime,
    );
    ```
2. <span data-ttu-id="96caf-151">Set the default value of the high watermark with the table name of source data store.</span><span class="sxs-lookup"><span data-stu-id="96caf-151">Set the default value of the high watermark with the table name of source data store.</span></span> <span data-ttu-id="96caf-152">In this tutorial, the table name is data_source_table.</span><span class="sxs-lookup"><span data-stu-id="96caf-152">In this tutorial, the table name is data_source_table.</span></span>

    ```sql
    INSERT INTO watermarktable
    VALUES ('data_source_table','1/1/2010 12:00:00 AM')    
    ```
3. <span data-ttu-id="96caf-153">Review the data in the table `watermarktable`.</span><span class="sxs-lookup"><span data-stu-id="96caf-153">Review the data in the table `watermarktable`.</span></span>
    
    ```sql
    Select * from watermarktable
    ```
    <span data-ttu-id="96caf-154">Output:</span><span class="sxs-lookup"><span data-stu-id="96caf-154">Output:</span></span> 

    ```
    TableName  | WatermarkValue
    ----------  | --------------
    data_source_table | 2010-01-01 00:00:00.000
    ```

### <a name="create-a-stored-procedure-in-your-sql-database"></a><span data-ttu-id="96caf-155">Create a stored procedure in your SQL database</span><span class="sxs-lookup"><span data-stu-id="96caf-155">Create a stored procedure in your SQL database</span></span> 

<span data-ttu-id="96caf-156">Run the following command to create a stored procedure in your SQL database:</span><span class="sxs-lookup"><span data-stu-id="96caf-156">Run the following command to create a stored procedure in your SQL database:</span></span>

```sql
CREATE PROCEDURE sp_write_watermark @LastModifiedtime datetime, @TableName varchar(50)
AS

BEGIN
    
    UPDATE watermarktable
    SET [WatermarkValue] = @LastModifiedtime 
WHERE [TableName] = @TableName
    
END
```

## <a name="create-a-data-factory"></a><span data-ttu-id="96caf-157">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="96caf-157">Create a data factory</span></span>
1. <span data-ttu-id="96caf-158">Define a variable for the resource group name that you use in PowerShell commands later.</span><span class="sxs-lookup"><span data-stu-id="96caf-158">Define a variable for the resource group name that you use in PowerShell commands later.</span></span> <span data-ttu-id="96caf-159">Copy the following command text to PowerShell, specify a name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) in double quotation marks, and then run the command.</span><span class="sxs-lookup"><span data-stu-id="96caf-159">Copy the following command text to PowerShell, specify a name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) in double quotation marks, and then run the command.</span></span> <span data-ttu-id="96caf-160">An example is `"adfrg"`.</span><span class="sxs-lookup"><span data-stu-id="96caf-160">An example is `"adfrg"`.</span></span> 
   
     ```powershell
    $resourceGroupName = "ADFTutorialResourceGroup";
    ```

    <span data-ttu-id="96caf-161">If the resource group already exists, you might not want to overwrite it.</span><span class="sxs-lookup"><span data-stu-id="96caf-161">If the resource group already exists, you might not want to overwrite it.</span></span> <span data-ttu-id="96caf-162">Assign a different value to the `$resourceGroupName` variable, and run the command again.</span><span class="sxs-lookup"><span data-stu-id="96caf-162">Assign a different value to the `$resourceGroupName` variable, and run the command again.</span></span>

2. <span data-ttu-id="96caf-163">Define a variable for the location of the data factory.</span><span class="sxs-lookup"><span data-stu-id="96caf-163">Define a variable for the location of the data factory.</span></span> 

    ```powershell
    $location = "East US"
    ```
3. <span data-ttu-id="96caf-164">To create the Azure resource group, run the following command:</span><span class="sxs-lookup"><span data-stu-id="96caf-164">To create the Azure resource group, run the following command:</span></span> 

    ```powershell
    New-AzureRmResourceGroup $resourceGroupName $location
    ``` 
    <span data-ttu-id="96caf-165">If the resource group already exists, you might not want to overwrite it.</span><span class="sxs-lookup"><span data-stu-id="96caf-165">If the resource group already exists, you might not want to overwrite it.</span></span> <span data-ttu-id="96caf-166">Assign a different value to the `$resourceGroupName` variable, and run the command again.</span><span class="sxs-lookup"><span data-stu-id="96caf-166">Assign a different value to the `$resourceGroupName` variable, and run the command again.</span></span>

4. <span data-ttu-id="96caf-167">Define a variable for the data factory name.</span><span class="sxs-lookup"><span data-stu-id="96caf-167">Define a variable for the data factory name.</span></span> 

    > [!IMPORTANT]
    >  <span data-ttu-id="96caf-168">Update the data factory name to make it globally unique.</span><span class="sxs-lookup"><span data-stu-id="96caf-168">Update the data factory name to make it globally unique.</span></span> <span data-ttu-id="96caf-169">An example is ADFTutorialFactorySP1127.</span><span class="sxs-lookup"><span data-stu-id="96caf-169">An example is ADFTutorialFactorySP1127.</span></span> 

    ```powershell
    $dataFactoryName = "ADFIncCopyTutorialFactory";
    ```
5. <span data-ttu-id="96caf-170">To create the data factory, run the following **Set-AzureRmDataFactoryV2** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="96caf-170">To create the data factory, run the following **Set-AzureRmDataFactoryV2** cmdlet:</span></span> 
    
    ```powershell       
    Set-AzureRmDataFactoryV2 -ResourceGroupName $resourceGroupName -Location "East US" -Name $dataFactoryName 
    ```

<span data-ttu-id="96caf-171">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="96caf-171">Note the following points:</span></span>

* <span data-ttu-id="96caf-172">The name of the data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="96caf-172">The name of the data factory must be globally unique.</span></span> <span data-ttu-id="96caf-173">If you receive the following error, change the name and try again:</span><span class="sxs-lookup"><span data-stu-id="96caf-173">If you receive the following error, change the name and try again:</span></span>

    ```
    The specified Data Factory name 'ADFv2QuickStartDataFactory' is already in use. Data Factory names must be globally unique.
    ```

* <span data-ttu-id="96caf-174">To create Data Factory instances, the user account you use to sign in to Azure must be a member of contributor or owner roles, or an administrator of the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="96caf-174">To create Data Factory instances, the user account you use to sign in to Azure must be a member of contributor or owner roles, or an administrator of the Azure subscription.</span></span>
* <span data-ttu-id="96caf-175">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="96caf-175">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span></span> <span data-ttu-id="96caf-176">The data stores (Storage, SQL Database, etc.) and computes (Azure HDInsight, etc.) used by the data factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="96caf-176">The data stores (Storage, SQL Database, etc.) and computes (Azure HDInsight, etc.) used by the data factory can be in other regions.</span></span>


## <a name="create-linked-services"></a><span data-ttu-id="96caf-177">Create linked services</span><span class="sxs-lookup"><span data-stu-id="96caf-177">Create linked services</span></span>
<span data-ttu-id="96caf-178">You create linked services in a data factory to link your data stores and compute services to the data factory.</span><span class="sxs-lookup"><span data-stu-id="96caf-178">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="96caf-179">In this section, you create linked services to your storage account and SQL database.</span><span class="sxs-lookup"><span data-stu-id="96caf-179">In this section, you create linked services to your storage account and SQL database.</span></span> 

### <a name="create-a-storage-linked-service"></a><span data-ttu-id="96caf-180">Create a Storage linked service</span><span class="sxs-lookup"><span data-stu-id="96caf-180">Create a Storage linked service</span></span>
1. <span data-ttu-id="96caf-181">Create a JSON file named AzureStorageLinkedService.json in the C:\ADF folder with the following content.</span><span class="sxs-lookup"><span data-stu-id="96caf-181">Create a JSON file named AzureStorageLinkedService.json in the C:\ADF folder with the following content.</span></span> <span data-ttu-id="96caf-182">(Create the folder ADF if it doesn't already exist.) Replace `<accountName>` and `<accountKey>` with the name and key of your storage account before you save the file.</span><span class="sxs-lookup"><span data-stu-id="96caf-182">(Create the folder ADF if it doesn't already exist.) Replace `<accountName>` and `<accountKey>` with the name and key of your storage account before you save the file.</span></span>

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
2. <span data-ttu-id="96caf-183">In PowerShell, switch to the ADF folder.</span><span class="sxs-lookup"><span data-stu-id="96caf-183">In PowerShell, switch to the ADF folder.</span></span>

3. <span data-ttu-id="96caf-184">Run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet to create the linked service AzureStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="96caf-184">Run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet to create the linked service AzureStorageLinkedService.</span></span> <span data-ttu-id="96caf-185">In the following example, you pass values for the *ResourceGroupName* and *DataFactoryName* parameters:</span><span class="sxs-lookup"><span data-stu-id="96caf-185">In the following example, you pass values for the *ResourceGroupName* and *DataFactoryName* parameters:</span></span> 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureStorageLinkedService" -File ".\AzureStorageLinkedService.json"
    ```

    <span data-ttu-id="96caf-186">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="96caf-186">Here is the sample output:</span></span>

    ```json
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : <resourceGroupName>
    DataFactoryName   : <dataFactoryName>
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureStorageLinkedService
    ```

### <a name="create-a-sql-database-linked-service"></a><span data-ttu-id="96caf-187">Create a SQL Database linked service</span><span class="sxs-lookup"><span data-stu-id="96caf-187">Create a SQL Database linked service</span></span>
1. <span data-ttu-id="96caf-188">Create a JSON file named AzureSQLDatabaseLinkedService.json in the C:\ADF folder with the following content.</span><span class="sxs-lookup"><span data-stu-id="96caf-188">Create a JSON file named AzureSQLDatabaseLinkedService.json in the C:\ADF folder with the following content.</span></span> <span data-ttu-id="96caf-189">(Create the folder ADF if it doesn't already exist.) Replace &lt;server&gt;, &lt;database&gt;, &lt;user id&gt;, and &lt;password&gt; with the name of your server, database, user ID, and password before you save the file.</span><span class="sxs-lookup"><span data-stu-id="96caf-189">(Create the folder ADF if it doesn't already exist.) Replace &lt;server&gt;, &lt;database&gt;, &lt;user id&gt;, and &lt;password&gt; with the name of your server, database, user ID, and password before you save the file.</span></span> 

    ```json
    {
        "name": "AzureSQLDatabaseLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": {
                    "value": "Server = tcp:<server>.database.windows.net,1433;Initial Catalog=<database>; Persist Security Info=False; User ID=<user> ; Password=<password>; MultipleActiveResultSets = False; Encrypt = True; TrustServerCertificate = False; Connection Timeout = 30;",
                    "type": "SecureString"
                }
            }
        }
    }
    ```
2. <span data-ttu-id="96caf-190">In PowerShell, switch to the ADF folder.</span><span class="sxs-lookup"><span data-stu-id="96caf-190">In PowerShell, switch to the ADF folder.</span></span>

3. <span data-ttu-id="96caf-191">Run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet to create the linked service AzureSQLDatabaseLinkedService.</span><span class="sxs-lookup"><span data-stu-id="96caf-191">Run the **Set-AzureRmDataFactoryV2LinkedService** cmdlet to create the linked service AzureSQLDatabaseLinkedService.</span></span> 

    ```powershell
    Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureSQLDatabaseLinkedService" -File ".\AzureSQLDatabaseLinkedService.json"
    ```

    <span data-ttu-id="96caf-192">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="96caf-192">Here is the sample output:</span></span>

    ```json
    LinkedServiceName : AzureSQLDatabaseLinkedService
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlDatabaseLinkedService
    ProvisioningState :
    ```

## <a name="create-datasets"></a><span data-ttu-id="96caf-193">Create datasets</span><span class="sxs-lookup"><span data-stu-id="96caf-193">Create datasets</span></span>
<span data-ttu-id="96caf-194">In this step, you create datasets to represent source and sink data.</span><span class="sxs-lookup"><span data-stu-id="96caf-194">In this step, you create datasets to represent source and sink data.</span></span> 

### <a name="create-a-source-dataset"></a><span data-ttu-id="96caf-195">Create a source dataset</span><span class="sxs-lookup"><span data-stu-id="96caf-195">Create a source dataset</span></span>

1. <span data-ttu-id="96caf-196">Create a JSON file named SourceDataset.json in the same folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="96caf-196">Create a JSON file named SourceDataset.json in the same folder with the following content:</span></span> 

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
    <span data-ttu-id="96caf-197">In this tutorial, you use the table name data_source_table.</span><span class="sxs-lookup"><span data-stu-id="96caf-197">In this tutorial, you use the table name data_source_table.</span></span> <span data-ttu-id="96caf-198">Replace it if you use a table with a different name.</span><span class="sxs-lookup"><span data-stu-id="96caf-198">Replace it if you use a table with a different name.</span></span>

2. <span data-ttu-id="96caf-199">Run the **Set-AzureRmDataFactoryV2Dataset** cmdlet to create the dataset SourceDataset.</span><span class="sxs-lookup"><span data-stu-id="96caf-199">Run the **Set-AzureRmDataFactoryV2Dataset** cmdlet to create the dataset SourceDataset.</span></span>
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SourceDataset" -File ".\SourceDataset.json"
    ```

    <span data-ttu-id="96caf-200">Here is the sample output of the cmdlet:</span><span class="sxs-lookup"><span data-stu-id="96caf-200">Here is the sample output of the cmdlet:</span></span>
    
    ```json
    DatasetName       : SourceDataset
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlTableDataset
    ```

### <a name="create-a-sink-dataset"></a><span data-ttu-id="96caf-201">Create a sink dataset</span><span class="sxs-lookup"><span data-stu-id="96caf-201">Create a sink dataset</span></span>

1. <span data-ttu-id="96caf-202">Create a JSON file named SinkDataset.json in the same folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="96caf-202">Create a JSON file named SinkDataset.json in the same folder with the following content:</span></span> 

    ```json
    {
        "name": "SinkDataset",
        "properties": {
            "type": "AzureBlob",
            "typeProperties": {
                "folderPath": "adftutorial/incrementalcopy",
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

    > [!IMPORTANT]
    > <span data-ttu-id="96caf-203">This snippet assumes that you have a blob container named adftutorial in your blob storage.</span><span class="sxs-lookup"><span data-stu-id="96caf-203">This snippet assumes that you have a blob container named adftutorial in your blob storage.</span></span> <span data-ttu-id="96caf-204">Create the container if it doesn't exist, or set it to the name of an existing one.</span><span class="sxs-lookup"><span data-stu-id="96caf-204">Create the container if it doesn't exist, or set it to the name of an existing one.</span></span> <span data-ttu-id="96caf-205">The output folder `incrementalcopy` is automatically created if it doesn't exist in the container.</span><span class="sxs-lookup"><span data-stu-id="96caf-205">The output folder `incrementalcopy` is automatically created if it doesn't exist in the container.</span></span> <span data-ttu-id="96caf-206">In this tutorial, the file name is dynamically generated by using the expression `@CONCAT('Incremental-', pipeline().RunId, '.txt')`.</span><span class="sxs-lookup"><span data-stu-id="96caf-206">In this tutorial, the file name is dynamically generated by using the expression `@CONCAT('Incremental-', pipeline().RunId, '.txt')`.</span></span>

2. <span data-ttu-id="96caf-207">Run the **Set-AzureRmDataFactoryV2Dataset** cmdlet to create the dataset SinkDataset.</span><span class="sxs-lookup"><span data-stu-id="96caf-207">Run the **Set-AzureRmDataFactoryV2Dataset** cmdlet to create the dataset SinkDataset.</span></span>
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "SinkDataset" -File ".\SinkDataset.json"
    ```

    <span data-ttu-id="96caf-208">Here is the sample output of the cmdlet:</span><span class="sxs-lookup"><span data-stu-id="96caf-208">Here is the sample output of the cmdlet:</span></span>
    
    ```json
    DatasetName       : SinkDataset
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureBlobDataset    
    ```

## <a name="create-a-dataset-for-a-watermark"></a><span data-ttu-id="96caf-209">Create a dataset for a watermark</span><span class="sxs-lookup"><span data-stu-id="96caf-209">Create a dataset for a watermark</span></span>
<span data-ttu-id="96caf-210">In this step, you create a dataset for storing a high watermark value.</span><span class="sxs-lookup"><span data-stu-id="96caf-210">In this step, you create a dataset for storing a high watermark value.</span></span> 

1. <span data-ttu-id="96caf-211">Create a JSON file named WatermarkDataset.json in the same folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="96caf-211">Create a JSON file named WatermarkDataset.json in the same folder with the following content:</span></span> 

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
2.  <span data-ttu-id="96caf-212">Run the **Set-AzureRmDataFactoryV2Dataset** cmdlet to create the dataset WatermarkDataset.</span><span class="sxs-lookup"><span data-stu-id="96caf-212">Run the **Set-AzureRmDataFactoryV2Dataset** cmdlet to create the dataset WatermarkDataset.</span></span>
    
    ```powershell
    Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "WatermarkDataset" -File ".\WatermarkDataset.json"
    ```

    <span data-ttu-id="96caf-213">Here is the sample output of the cmdlet:</span><span class="sxs-lookup"><span data-stu-id="96caf-213">Here is the sample output of the cmdlet:</span></span>
    
    ```json
    DatasetName       : WatermarkDataset
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    Structure         :
    Properties        : Microsoft.Azure.Management.DataFactory.Models.AzureSqlTableDataset    
    ```

## <a name="create-a-pipeline"></a><span data-ttu-id="96caf-214">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="96caf-214">Create a pipeline</span></span>
<span data-ttu-id="96caf-215">In this tutorial, you create a pipeline with two Lookup activities, one Copy activity, and one StoredProcedure activity chained in one pipeline.</span><span class="sxs-lookup"><span data-stu-id="96caf-215">In this tutorial, you create a pipeline with two Lookup activities, one Copy activity, and one StoredProcedure activity chained in one pipeline.</span></span> 


1. <span data-ttu-id="96caf-216">Create a JSON file IncrementalCopyPipeline.json in the same folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="96caf-216">Create a JSON file IncrementalCopyPipeline.json in the same folder with the following content:</span></span> 

    ```json
    {
        "name": "IncrementalCopyPipeline",
        "properties": {
            "activities": [
                {
                    "name": "LookupOldWaterMarkActivity",
                    "type": "Lookup",
                    "typeProperties": {
                        "source": {
                        "type": "SqlSource",
                        "sqlReaderQuery": "select * from watermarktable"
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
                            "sqlReaderQuery": "select MAX(LastModifytime) as NewWatermarkvalue from data_source_table"
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
                            "sqlReaderQuery": "select * from data_source_table where LastModifytime > '@{activity('LookupOldWaterMarkActivity').output.firstRow.WatermarkValue}' and LastModifytime <= '@{activity('LookupNewWaterMarkActivity').output.firstRow.NewWatermarkvalue}'"
                        },
                        "sink": {
                            "type": "BlobSink"
                        }
                    },
                    "dependsOn": [
                        {
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
                    "name": "StoredProceduretoWriteWatermarkActivity",
                    "type": "SqlServerStoredProcedure",
                    "typeProperties": {
    
                        "storedProcedureName": "sp_write_watermark",
                        "storedProcedureParameters": {
                            "LastModifiedtime": {"value": "@{activity('LookupNewWaterMarkActivity').output.firstRow.NewWatermarkvalue}", "type": "datetime" },
                            "TableName":  { "value":"@{activity('LookupOldWaterMarkActivity').output.firstRow.TableName}", "type":"String"}
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
    

2. <span data-ttu-id="96caf-217">Run the **Set-AzureRmDataFactoryV2Pipeline** cmdlet to create the pipeline IncrementalCopyPipeline.</span><span class="sxs-lookup"><span data-stu-id="96caf-217">Run the **Set-AzureRmDataFactoryV2Pipeline** cmdlet to create the pipeline IncrementalCopyPipeline.</span></span>
    
   ```powershell
   Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "IncrementalCopyPipeline" -File ".\IncrementalCopyPipeline.json"
   ``` 

   <span data-ttu-id="96caf-218">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="96caf-218">Here is the sample output:</span></span> 

   ```json
    PipelineName      : IncrementalCopyPipeline
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    Activities        : {LookupOldWaterMarkActivity, LookupNewWaterMarkActivity, IncrementalCopyActivity, StoredProceduretoWriteWatermarkActivity}
    Parameters        :
   ```
 
## <a name="run-the-pipeline"></a><span data-ttu-id="96caf-219">Run the pipeline</span><span class="sxs-lookup"><span data-stu-id="96caf-219">Run the pipeline</span></span>

1. <span data-ttu-id="96caf-220">Run the pipeline IncrementalCopyPipeline by using the **Invoke-AzureRmDataFactoryV2Pipeline** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96caf-220">Run the pipeline IncrementalCopyPipeline by using the **Invoke-AzureRmDataFactoryV2Pipeline** cmdlet.</span></span> <span data-ttu-id="96caf-221">Replace placeholders with your own resource group and data factory name.</span><span class="sxs-lookup"><span data-stu-id="96caf-221">Replace placeholders with your own resource group and data factory name.</span></span>

    ```powershell
    $RunId = Invoke-AzureRmDataFactoryV2Pipeline -PipelineName "IncrementalCopyPipeline" -ResourceGroupName $resourceGroupName -dataFactoryName $dataFactoryName
    ``` 
2. <span data-ttu-id="96caf-222">Check the status of the pipeline by running the **Get-AzureRmDataFactoryV2ActivityRun** cmdlet until you see all the activities running successfully.</span><span class="sxs-lookup"><span data-stu-id="96caf-222">Check the status of the pipeline by running the **Get-AzureRmDataFactoryV2ActivityRun** cmdlet until you see all the activities running successfully.</span></span> <span data-ttu-id="96caf-223">Replace placeholders with your own appropriate time for the parameters *RunStartedAfter* and *RunStartedBefore*.</span><span class="sxs-lookup"><span data-stu-id="96caf-223">Replace placeholders with your own appropriate time for the parameters *RunStartedAfter* and *RunStartedBefore*.</span></span> <span data-ttu-id="96caf-224">In this tutorial, you use *-RunStartedAfter "2017/09/14"* and *-RunStartedBefore "2017/09/15"*.</span><span class="sxs-lookup"><span data-stu-id="96caf-224">In this tutorial, you use *-RunStartedAfter "2017/09/14"* and *-RunStartedBefore "2017/09/15"*.</span></span>

    ```powershell
    Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $RunId -RunStartedAfter "<start time>" -RunStartedBefore "<end time>"
    ```

    <span data-ttu-id="96caf-225">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="96caf-225">Here is the sample output:</span></span>
 
    ```json
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    ActivityName      : LookupNewWaterMarkActivity
    PipelineRunId     : d4bf3ce2-5d60-43f3-9318-923155f61037
    PipelineName      : IncrementalCopyPipeline
    Input             : {source, dataset}
    Output            : {NewWatermarkvalue}
    LinkedServiceName :
    ActivityRunStart  : 9/14/2017 7:42:42 AM
    ActivityRunEnd    : 9/14/2017 7:42:50 AM
    DurationInMs      : 7777
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    ActivityName      : LookupOldWaterMarkActivity
    PipelineRunId     : d4bf3ce2-5d60-43f3-9318-923155f61037
    PipelineName      : IncrementalCopyPipeline
    Input             : {source, dataset}
    Output            : {TableName, WatermarkValue}
    LinkedServiceName :
    ActivityRunStart  : 9/14/2017 7:42:42 AM
    ActivityRunEnd    : 9/14/2017 7:43:07 AM
    DurationInMs      : 25437
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    ActivityName      : IncrementalCopyActivity
    PipelineRunId     : d4bf3ce2-5d60-43f3-9318-923155f61037
    PipelineName      : IncrementalCopyPipeline
    Input             : {source, sink}
    Output            : {dataRead, dataWritten, rowsCopied, copyDuration...}
    LinkedServiceName :
    ActivityRunStart  : 9/14/2017 7:43:10 AM
    ActivityRunEnd    : 9/14/2017 7:43:29 AM
    DurationInMs      : 19769
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    ActivityName      : StoredProceduretoWriteWatermarkActivity
    PipelineRunId     : d4bf3ce2-5d60-43f3-9318-923155f61037
    PipelineName      : IncrementalCopyPipeline
    Input             : {storedProcedureName, storedProcedureParameters}
    Output            : {}
    LinkedServiceName :
    ActivityRunStart  : 9/14/2017 7:43:32 AM
    ActivityRunEnd    : 9/14/2017 7:43:47 AM
    DurationInMs      : 14467
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}

    ```

## <a name="review-the-results"></a><span data-ttu-id="96caf-226">Review the results</span><span class="sxs-lookup"><span data-stu-id="96caf-226">Review the results</span></span>

1. <span data-ttu-id="96caf-227">In the blob storage (sink store), you see that the data were copied to the file defined in SinkDataset.</span><span class="sxs-lookup"><span data-stu-id="96caf-227">In the blob storage (sink store), you see that the data were copied to the file defined in SinkDataset.</span></span> <span data-ttu-id="96caf-228">In the current tutorial, the file name is `Incremental- d4bf3ce2-5d60-43f3-9318-923155f61037.txt`.</span><span class="sxs-lookup"><span data-stu-id="96caf-228">In the current tutorial, the file name is `Incremental- d4bf3ce2-5d60-43f3-9318-923155f61037.txt`.</span></span> <span data-ttu-id="96caf-229">Open the file, and you can see records in the file that are the same as the data in the SQL database.</span><span class="sxs-lookup"><span data-stu-id="96caf-229">Open the file, and you can see records in the file that are the same as the data in the SQL database.</span></span>

    ```
    1,aaaa,2017-09-01 00:56:00.0000000
    2,bbbb,2017-09-02 05:23:00.0000000
    3,cccc,2017-09-03 02:36:00.0000000
    4,dddd,2017-09-04 03:21:00.0000000
    5,eeee,2017-09-05 08:06:00.0000000
    ``` 
2. <span data-ttu-id="96caf-230">Check the latest value from `watermarktable`.</span><span class="sxs-lookup"><span data-stu-id="96caf-230">Check the latest value from `watermarktable`.</span></span> <span data-ttu-id="96caf-231">You see that the watermark value was updated.</span><span class="sxs-lookup"><span data-stu-id="96caf-231">You see that the watermark value was updated.</span></span>

    ```sql
    Select * from watermarktable
    ```
    
    <span data-ttu-id="96caf-232">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="96caf-232">Here is the sample output:</span></span>
 
    <span data-ttu-id="96caf-233">TableName</span><span class="sxs-lookup"><span data-stu-id="96caf-233">TableName</span></span> | <span data-ttu-id="96caf-234">WatermarkValue</span><span class="sxs-lookup"><span data-stu-id="96caf-234">WatermarkValue</span></span>
    --------- | --------------
    <span data-ttu-id="96caf-235">data_source_table   2017-09-05  8:06:00.000</span><span class="sxs-lookup"><span data-stu-id="96caf-235">data_source_table   2017-09-05  8:06:00.000</span></span>

### <a name="insert-data-into-the-data-source-store-to-verify-delta-data-loading"></a><span data-ttu-id="96caf-236">Insert data into the data source store to verify delta data loading</span><span class="sxs-lookup"><span data-stu-id="96caf-236">Insert data into the data source store to verify delta data loading</span></span>

1. <span data-ttu-id="96caf-237">Insert new data into the SQL database (data source store).</span><span class="sxs-lookup"><span data-stu-id="96caf-237">Insert new data into the SQL database (data source store).</span></span>

    ```sql
    INSERT INTO data_source_table
    VALUES (6, 'newdata','9/6/2017 2:23:00 AM')
    
    INSERT INTO data_source_table
    VALUES (7, 'newdata','9/7/2017 9:01:00 AM')
    ``` 

    <span data-ttu-id="96caf-238">The updated data in the SQL database is:</span><span class="sxs-lookup"><span data-stu-id="96caf-238">The updated data in the SQL database is:</span></span>

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
2. <span data-ttu-id="96caf-239">Run the pipeline IncrementalCopyPipeline again by using the **Invoke-AzureRmDataFactoryV2Pipeline** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="96caf-239">Run the pipeline IncrementalCopyPipeline again by using the **Invoke-AzureRmDataFactoryV2Pipeline** cmdlet.</span></span> <span data-ttu-id="96caf-240">Replace placeholders with your own resource group and data factory name.</span><span class="sxs-lookup"><span data-stu-id="96caf-240">Replace placeholders with your own resource group and data factory name.</span></span>

    ```powershell
    $RunId = Invoke-AzureRmDataFactoryV2Pipeline -PipelineName "IncrementalCopyPipeline" -ResourceGroupName $resourceGroupName -dataFactoryName $dataFactoryName
    ```
3. <span data-ttu-id="96caf-241">Check the status of the pipeline by running the **Get-AzureRmDataFactoryV2ActivityRun** cmdlet until you see all the activities running successfully.</span><span class="sxs-lookup"><span data-stu-id="96caf-241">Check the status of the pipeline by running the **Get-AzureRmDataFactoryV2ActivityRun** cmdlet until you see all the activities running successfully.</span></span> <span data-ttu-id="96caf-242">Replace placeholders with your own appropriate time for the parameters *RunStartedAfter* and *RunStartedBefore*.</span><span class="sxs-lookup"><span data-stu-id="96caf-242">Replace placeholders with your own appropriate time for the parameters *RunStartedAfter* and *RunStartedBefore*.</span></span> <span data-ttu-id="96caf-243">In this tutorial, you use *-RunStartedAfter "2017/09/14"* and *-RunStartedBefore "2017/09/15"*.</span><span class="sxs-lookup"><span data-stu-id="96caf-243">In this tutorial, you use *-RunStartedAfter "2017/09/14"* and *-RunStartedBefore "2017/09/15"*.</span></span>

    ```powershell
    Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $RunId -RunStartedAfter "<start time>" -RunStartedBefore "<end time>"
    ```

    <span data-ttu-id="96caf-244">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="96caf-244">Here is the sample output:</span></span>
 
    ```json
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    ActivityName      : LookupNewWaterMarkActivity
    PipelineRunId     : 2fc90ab8-d42c-4583-aa64-755dba9925d7
    PipelineName      : IncrementalCopyPipeline
    Input             : {source, dataset}
    Output            : {NewWatermarkvalue}
    LinkedServiceName :
    ActivityRunStart  : 9/14/2017 8:52:26 AM
    ActivityRunEnd    : 9/14/2017 8:52:58 AM
    DurationInMs      : 31758
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    ActivityName      : LookupOldWaterMarkActivity
    PipelineRunId     : 2fc90ab8-d42c-4583-aa64-755dba9925d7
    PipelineName      : IncrementalCopyPipeline
    Input             : {source, dataset}
    Output            : {TableName, WatermarkValue}
    LinkedServiceName :
    ActivityRunStart  : 9/14/2017 8:52:26 AM
    ActivityRunEnd    : 9/14/2017 8:52:52 AM
    DurationInMs      : 25497
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    ActivityName      : IncrementalCopyActivity
    PipelineRunId     : 2fc90ab8-d42c-4583-aa64-755dba9925d7
    PipelineName      : IncrementalCopyPipeline
    Input             : {source, sink}
    Output            : {dataRead, dataWritten, rowsCopied, copyDuration...}
    LinkedServiceName :
    ActivityRunStart  : 9/14/2017 8:53:00 AM
    ActivityRunEnd    : 9/14/2017 8:53:20 AM
    DurationInMs      : 20194
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}
    
    ResourceGroupName : ADF
    DataFactoryName   : incrementalloadingADF
    ActivityName      : StoredProceduretoWriteWatermarkActivity
    PipelineRunId     : 2fc90ab8-d42c-4583-aa64-755dba9925d7
    PipelineName      : IncrementalCopyPipeline
    Input             : {storedProcedureName, storedProcedureParameters}
    Output            : {}
    LinkedServiceName :
    ActivityRunStart  : 9/14/2017 8:53:23 AM
    ActivityRunEnd    : 9/14/2017 8:53:41 AM
    DurationInMs      : 18502
    Status            : Succeeded
    Error             : {errorCode, message, failureType, target}

    ```
4. <span data-ttu-id="96caf-245">In the blob storage, you see that another file was created.</span><span class="sxs-lookup"><span data-stu-id="96caf-245">In the blob storage, you see that another file was created.</span></span> <span data-ttu-id="96caf-246">In this tutorial, the new file name is `Incremental-2fc90ab8-d42c-4583-aa64-755dba9925d7.txt`.</span><span class="sxs-lookup"><span data-stu-id="96caf-246">In this tutorial, the new file name is `Incremental-2fc90ab8-d42c-4583-aa64-755dba9925d7.txt`.</span></span> <span data-ttu-id="96caf-247">Open that file, and you see two rows of records in it.</span><span class="sxs-lookup"><span data-stu-id="96caf-247">Open that file, and you see two rows of records in it.</span></span>

5. <span data-ttu-id="96caf-248">Check the latest value from `watermarktable`.</span><span class="sxs-lookup"><span data-stu-id="96caf-248">Check the latest value from `watermarktable`.</span></span> <span data-ttu-id="96caf-249">You see that the watermark value was updated again.</span><span class="sxs-lookup"><span data-stu-id="96caf-249">You see that the watermark value was updated again.</span></span>

    ```sql
    Select * from watermarktable
    ```
    <span data-ttu-id="96caf-250">sample output:</span><span class="sxs-lookup"><span data-stu-id="96caf-250">sample output:</span></span> 
    
    <span data-ttu-id="96caf-251">TableName</span><span class="sxs-lookup"><span data-stu-id="96caf-251">TableName</span></span> | <span data-ttu-id="96caf-252">WatermarkValue</span><span class="sxs-lookup"><span data-stu-id="96caf-252">WatermarkValue</span></span>
    --------- | ---------------
    <span data-ttu-id="96caf-253">data_source_table</span><span class="sxs-lookup"><span data-stu-id="96caf-253">data_source_table</span></span> | <span data-ttu-id="96caf-254">2017-09-07 09:01:00.000</span><span class="sxs-lookup"><span data-stu-id="96caf-254">2017-09-07 09:01:00.000</span></span>

     
## <a name="next-steps"></a><span data-ttu-id="96caf-255">Next steps</span><span class="sxs-lookup"><span data-stu-id="96caf-255">Next steps</span></span>
<span data-ttu-id="96caf-256">You performed the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="96caf-256">You performed the following steps in this tutorial:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="96caf-257">Prepare the data store to store the watermark value.</span><span class="sxs-lookup"><span data-stu-id="96caf-257">Prepare the data store to store the watermark value.</span></span> 
> * <span data-ttu-id="96caf-258">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="96caf-258">Create a data factory.</span></span>
> * <span data-ttu-id="96caf-259">Create linked services.</span><span class="sxs-lookup"><span data-stu-id="96caf-259">Create linked services.</span></span> 
> * <span data-ttu-id="96caf-260">Create source, sink, and watermark datasets.</span><span class="sxs-lookup"><span data-stu-id="96caf-260">Create source, sink, and watermark datasets.</span></span>
> * <span data-ttu-id="96caf-261">Create a pipeline.</span><span class="sxs-lookup"><span data-stu-id="96caf-261">Create a pipeline.</span></span>
> * <span data-ttu-id="96caf-262">Run the pipeline.</span><span class="sxs-lookup"><span data-stu-id="96caf-262">Run the pipeline.</span></span>
> * <span data-ttu-id="96caf-263">Monitor the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="96caf-263">Monitor the pipeline run.</span></span> 

<span data-ttu-id="96caf-264">In this tutorial, the pipeline copied data from a single table in a SQL database to Blob storage.</span><span class="sxs-lookup"><span data-stu-id="96caf-264">In this tutorial, the pipeline copied data from a single table in a SQL database to Blob storage.</span></span> <span data-ttu-id="96caf-265">Advance to the following tutorial to learn how to copy data from multiple tables in an on-premises SQL Server database to a SQL database.</span><span class="sxs-lookup"><span data-stu-id="96caf-265">Advance to the following tutorial to learn how to copy data from multiple tables in an on-premises SQL Server database to a SQL database.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="96caf-266">Incrementally load data from multiple tables in SQL Server to Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="96caf-266">Incrementally load data from multiple tables in SQL Server to Azure SQL Database</span></span>](tutorial-incremental-copy-multiple-tables-powershell.md)



