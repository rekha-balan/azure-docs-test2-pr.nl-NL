---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: Load data from Azure blob storage into Azure SQL Data Warehouse (Azure Data Factory) | Microsoft Docs
description: Learn to load data with Azure Data Factory
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: ''
tags: azure-sql-data-warehouse
ms.assetid: 689fb02e-eb98-4f7c-81e6-6c1d22d53901
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: barbkess
ms.custom: loading
ms.openlocfilehash: ca8bdfc21582253e8709a33eb624547fed4461d6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549936"
---
# <a name="load-data-from-azure-blob-storage-into-azure-sql-data-warehouse-azure-data-factory"></a><span data-ttu-id="9d4a3-103">Load data from Azure blob storage into Azure SQL Data Warehouse (Azure Data Factory)</span><span class="sxs-lookup"><span data-stu-id="9d4a3-103">Load data from Azure blob storage into Azure SQL Data Warehouse (Azure Data Factory)</span></span>
> [!div class="op_single_selector"]
> * [Data Factory](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [PolyBase](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

 <span data-ttu-id="9d4a3-106">This tutorial shows you how to create a pipeline in Azure Data Factory to move data from Azure Storage Blob to SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-106">This tutorial shows you how to create a pipeline in Azure Data Factory to move data from Azure Storage Blob to SQL Data Warehouse.</span></span> <span data-ttu-id="9d4a3-107">With the following steps you will:</span><span class="sxs-lookup"><span data-stu-id="9d4a3-107">With the following steps you will:</span></span>

* <span data-ttu-id="9d4a3-108">Set-up sample data in an Azure Storage Blob.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-108">Set-up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="9d4a3-109">Connect resources to Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-109">Connect resources to Azure Data Factory.</span></span>
* <span data-ttu-id="9d4a3-110">Create a pipeline to move data from Storage Blobs to SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-110">Create a pipeline to move data from Storage Blobs to SQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="9d4a3-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="9d4a3-111">Before you begin</span></span>
<span data-ttu-id="9d4a3-112">To familiarize yourself with Azure Data Factory, see [Introduction to Azure Data Factory][Introduction to Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="9d4a3-112">To familiarize yourself with Azure Data Factory, see [Introduction to Azure Data Factory][Introduction to Azure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="9d4a3-113">Create or identify resources</span><span class="sxs-lookup"><span data-stu-id="9d4a3-113">Create or identify resources</span></span>
<span data-ttu-id="9d4a3-114">Before starting this tutorial, you need to have the following resources.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-114">Before starting this tutorial, you need to have the following resources.</span></span>

* <span data-ttu-id="9d4a3-115">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as the data source for the Azure Data Factory pipeline, and so you need to have one available to store the sample data.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-115">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as the data source for the Azure Data Factory pipeline, and so you need to have one available to store the sample data.</span></span> <span data-ttu-id="9d4a3-116">If you don't have one already, learn how to [Create a storage account][Create a storage account].</span><span class="sxs-lookup"><span data-stu-id="9d4a3-116">If you don't have one already, learn how to [Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="9d4a3-117">**SQL Data Warehouse**: This tutorial moves the data from Azure Storage Blob to  SQL Data Warehouse and so need to have a data warehouse online that is loaded with the AdventureWorksDW sample data.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-117">**SQL Data Warehouse**: This tutorial moves the data from Azure Storage Blob to  SQL Data Warehouse and so need to have a data warehouse online that is loaded with the AdventureWorksDW sample data.</span></span> <span data-ttu-id="9d4a3-118">If you do not already have a data warehouse, learn how to [provision one][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="9d4a3-118">If you do not already have a data warehouse, learn how to [provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="9d4a3-119">If you have a data warehouse but didn't provision it with the sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="9d4a3-119">If you have a data warehouse but didn't provision it with the sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="9d4a3-120">**Azure Data Factory**: Azure Data Factory will complete the actual load and so you need to have one that you can use to build the data movement pipeline.If you don't have one already, learn how to create one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span><span class="sxs-lookup"><span data-stu-id="9d4a3-120">**Azure Data Factory**: Azure Data Factory will complete the actual load and so you need to have one that you can use to build the data movement pipeline.If you don't have one already, learn how to create one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="9d4a3-121">**AZCopy**: You need AZCopy to copy the sample data from your local client to your Azure Storage Blob.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-121">**AZCopy**: You need AZCopy to copy the sample data from your local client to your Azure Storage Blob.</span></span> <span data-ttu-id="9d4a3-122">For install instructions, see the [AZCopy documentation][AZCopy documentation].</span><span class="sxs-lookup"><span data-stu-id="9d4a3-122">For install instructions, see the [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-to-azure-storage-blob"></a><span data-ttu-id="9d4a3-123">Step 1: Copy sample data to Azure Storage Blob</span><span class="sxs-lookup"><span data-stu-id="9d4a3-123">Step 1: Copy sample data to Azure Storage Blob</span></span>
<span data-ttu-id="9d4a3-124">Once you have all of the pieces ready, you are ready to copy sample data to your Azure Storage Blob.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-124">Once you have all of the pieces ready, you are ready to copy sample data to your Azure Storage Blob.</span></span>

1. <span data-ttu-id="9d4a3-125">[Download sample data][Download sample data].</span><span class="sxs-lookup"><span data-stu-id="9d4a3-125">[Download sample data][Download sample data].</span></span> <span data-ttu-id="9d4a3-126">This data will add another three years of sales data to your AdventureWorksDW sample data.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-126">This data will add another three years of sales data to your AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="9d4a3-127">Use this AZCopy command to copy the three years of data to your Azure Storage Blob.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-127">Use this AZCopy command to copy the three years of data to your Azure Storage Blob.</span></span>

````
AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
````


## <a name="step-2-connect-resources-to-azure-data-factory"></a><span data-ttu-id="9d4a3-128">Step 2: Connect resources to Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9d4a3-128">Step 2: Connect resources to Azure Data Factory</span></span>
<span data-ttu-id="9d4a3-129">Now that the data is in place we can create the Azure Data Factory pipeline to move the data from Azure blob storage into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-129">Now that the data is in place we can create the Azure Data Factory pipeline to move the data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="9d4a3-130">To get started, open the [Azure portal][Azure portal] and select your data factory from the left-hand menu.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-130">To get started, open the [Azure portal][Azure portal] and select your data factory from the left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="9d4a3-131">Step 2.1: Create Linked Service</span><span class="sxs-lookup"><span data-stu-id="9d4a3-131">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="9d4a3-132">Link your Azure storage account and SQL Data Warehouse to your data factory.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-132">Link your Azure storage account and SQL Data Warehouse to your data factory.</span></span>  

1. <span data-ttu-id="9d4a3-133">First, begin the registration process by clicking the 'Linked Services' section of your data factory and then click 'New data store.'</span><span class="sxs-lookup"><span data-stu-id="9d4a3-133">First, begin the registration process by clicking the 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="9d4a3-134">Choose a name to register your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-134">Choose a name to register your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="9d4a3-135">To register SQL Data Warehouse navigate to the 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-135">To register SQL Data Warehouse navigate to the 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="9d4a3-136">Copy and paste in this template, and then fill in your specific information.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-136">Copy and paste in this template, and then fill in your specific information.</span></span>

```JSON
{
    "name": "<Linked Service Name>",
    "properties": {
        "description": "",
        "type": "AzureSqlDW",
        "typeProperties": {
             "connectionString": "Data Source=tcp:<server name>.database.windows.net,1433;Initial Catalog=<server name>;Integrated Security=False;User ID=<user>@<servername>;Password=<password>;Connect Timeout=30;Encrypt=True"
         }
    }
}
```

### <a name="step-22-define-the-dataset"></a><span data-ttu-id="9d4a3-137">Step 2.2: Define the dataset</span><span class="sxs-lookup"><span data-stu-id="9d4a3-137">Step 2.2: Define the dataset</span></span>
<span data-ttu-id="9d4a3-138">After creating the linked services, we will have to define the data sets.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-138">After creating the linked services, we will have to define the data sets.</span></span>  <span data-ttu-id="9d4a3-139">Here this means defining the structure of the data that is being moved from your storage to your data warehouse.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-139">Here this means defining the structure of the data that is being moved from your storage to your data warehouse.</span></span>  <span data-ttu-id="9d4a3-140">You can read more about creating</span><span class="sxs-lookup"><span data-stu-id="9d4a3-140">You can read more about creating</span></span>

1. <span data-ttu-id="9d4a3-141">Start this process by navigating to the 'Author and Deploy' section of your data factory.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-141">Start this process by navigating to the 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="9d4a3-142">Click 'New dataset' and then 'Azure Blob storage' to link your storage to your data factory.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-142">Click 'New dataset' and then 'Azure Blob storage' to link your storage to your data factory.</span></span>  <span data-ttu-id="9d4a3-143">You can use the below script to define your data in Azure Blob storage:</span><span class="sxs-lookup"><span data-stu-id="9d4a3-143">You can use the below script to define your data in Azure Blob storage:</span></span>

```JSON
{
    "name": "<Dataset Name>",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "<linked storage name>",
        "typeProperties": {
            "folderPath": "<containter name>",
            "fileName": "FactInternetSales.csv",
            "format": {
            "type": "TextFormat",
            "columnDelimiter": ",",
            "rowDelimiter": "\n"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```


1. <span data-ttu-id="9d4a3-144">Now we will also define our dataset for SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-144">Now we will also define our dataset for SQL Data Warehouse.</span></span>  <span data-ttu-id="9d4a3-145">We start in the same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-145">We start in the same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>

```JSON
{
    "name": "DWDataset",
    "properties": {
        "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "FactInternetSales"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="9d4a3-146">Step 3: Create and run your pipeline</span><span class="sxs-lookup"><span data-stu-id="9d4a3-146">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="9d4a3-147">Finally, we will set-up and run the pipeline in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-147">Finally, we will set-up and run the pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="9d4a3-148">This is the operation that will complete the actual data movement.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-148">This is the operation that will complete the actual data movement.</span></span>  <span data-ttu-id="9d4a3-149">You can find a full view of the operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data to and from Azure SQL Data Warehouse using Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="9d4a3-149">You can find a full view of the operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data to and from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="9d4a3-150">In the 'Author and Deploy' section now click 'More Commands' and then 'New Pipeline'.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-150">In the 'Author and Deploy' section now click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="9d4a3-151">After you create the pipeline, you can use the below code to transfer the data to your data warehouse:</span><span class="sxs-lookup"><span data-stu-id="9d4a3-151">After you create the pipeline, you can use the below code to transfer the data to your data warehouse:</span></span>

```JSON
{
    "name": "<Pipeline Name>",
    "properties": {
        "description": "<Description>",
        "activities": [
          {
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "skipHeaderLineCount": 1
                },
                "sink": {
                    "type": "SqlDWSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:10"
                }
            },
            "inputs": [
              {
                "name": "<Storage Dataset>"
              }
            ],
            "outputs": [
              {
                "name": "<Data Warehouse Dataset>"
              }
            ],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Sample Copy",
            "description": "Copy Activity"
          }
        ],
        "start": "<Date YYYY-MM-DD>",
        "end": "<Date YYYY-MM-DD>",
        "isPaused": false
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="9d4a3-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="9d4a3-152">Next steps</span></span>
<span data-ttu-id="9d4a3-153">To learn more, start by viewing:</span><span class="sxs-lookup"><span data-stu-id="9d4a3-153">To learn more, start by viewing:</span></span>

* <span data-ttu-id="9d4a3-154">[Azure Data Factory learning path][Azure Data Factory learning path].</span><span class="sxs-lookup"><span data-stu-id="9d4a3-154">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="9d4a3-155">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span><span class="sxs-lookup"><span data-stu-id="9d4a3-155">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="9d4a3-156">This is the core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-156">This is the core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="9d4a3-157">These topics provide detailed information about Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-157">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="9d4a3-158">They discuss Azure SQL Database or HDinsight, but the information also applies to Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-158">They discuss Azure SQL Database or HDinsight, but the information also applies to Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="9d4a3-159">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is the core tutorial for processing data with Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-159">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is the core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="9d4a3-160">In this tutorial you will build your first pipeline that uses HDInsight to transform and analyze web logs on a monthly basis.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-160">In this tutorial you will build your first pipeline that uses HDInsight to transform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="9d4a3-161">Note, there is no copy activity in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-161">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="9d4a3-162">[Tutorial: Copy data from Azure Storage Blob to Azure SQL Database][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database].</span><span class="sxs-lookup"><span data-stu-id="9d4a3-162">[Tutorial: Copy data from Azure Storage Blob to Azure SQL Database][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database].</span></span> <span data-ttu-id="9d4a3-163">In this tutorial, you will create a pipeline in Azure Data Factory to copy data from Azure Storage Blob to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="9d4a3-163">In this tutorial, you will create a pipeline in Azure Data Factory to copy data from Azure Storage Blob to Azure SQL Database.</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction to Azure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data to and from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob to Azure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv