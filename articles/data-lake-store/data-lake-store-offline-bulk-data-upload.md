---
title: Upload large amounts of data into Data Lake Store by using offline methods | Microsoft Docs
description: Use the AdlCopy tool to copy data from Azure Storage blobs to Data Lake Store
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 45321f6a-179f-4ee4-b8aa-efa7745b8eb6
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/06/2017
ms.author: nitinme
ms.openlocfilehash: dae5491962b22453c517da35539ce09463d8802d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564117"
---
# <a name="use-the-azure-importexport-service-for-offline-copy-of-data-to-data-lake-store"></a><span data-ttu-id="ff77c-103">Use the Azure Import/Export service for offline copy of data to Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ff77c-103">Use the Azure Import/Export service for offline copy of data to Data Lake Store</span></span>
<span data-ttu-id="ff77c-104">In this article, you'll learn how to copy huge data sets (>200 GB) into an Azure Data Lake Store by using offline copy methods, like the [Azure Import/Export service](../storage/storage-import-export-service.md).</span><span class="sxs-lookup"><span data-stu-id="ff77c-104">In this article, you'll learn how to copy huge data sets (>200 GB) into an Azure Data Lake Store by using offline copy methods, like the [Azure Import/Export service](../storage/storage-import-export-service.md).</span></span> <span data-ttu-id="ff77c-105">Specifically, the file used as an example in this article is 339,420,860,416 bytes, or about 319 GB on disk.</span><span class="sxs-lookup"><span data-stu-id="ff77c-105">Specifically, the file used as an example in this article is 339,420,860,416 bytes, or about 319 GB on disk.</span></span> <span data-ttu-id="ff77c-106">Let's call this file 319GB.tsv.</span><span class="sxs-lookup"><span data-stu-id="ff77c-106">Let's call this file 319GB.tsv.</span></span>

<span data-ttu-id="ff77c-107">The Azure Import/Export service helps you to transfer large amounts of data more securely to Azure Blob storage by shipping hard disk drives to an Azure datacenter.</span><span class="sxs-lookup"><span data-stu-id="ff77c-107">The Azure Import/Export service helps you to transfer large amounts of data more securely to Azure Blob storage by shipping hard disk drives to an Azure datacenter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff77c-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ff77c-108">Prerequisites</span></span>
<span data-ttu-id="ff77c-109">Before you begin, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="ff77c-109">Before you begin, you must have the following:</span></span>

* <span data-ttu-id="ff77c-110">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="ff77c-110">**An Azure subscription**.</span></span> <span data-ttu-id="ff77c-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff77c-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ff77c-112">**An Azure storage account**.</span><span class="sxs-lookup"><span data-stu-id="ff77c-112">**An Azure storage account**.</span></span>
* <span data-ttu-id="ff77c-113">**An Azure Data Lake Store account**.</span><span class="sxs-lookup"><span data-stu-id="ff77c-113">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="ff77c-114">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ff77c-114">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

## <a name="preparing-the-data"></a><span data-ttu-id="ff77c-115">Preparing the data</span><span class="sxs-lookup"><span data-stu-id="ff77c-115">Preparing the data</span></span>
<span data-ttu-id="ff77c-116">Before using the Import/Export service, break the data file to be transferred **into copies that are less than 200 GB** in size.</span><span class="sxs-lookup"><span data-stu-id="ff77c-116">Before using the Import/Export service, break the data file to be transferred **into copies that are less than 200 GB** in size.</span></span> <span data-ttu-id="ff77c-117">The import tool does not work with files greater than 200 GB.</span><span class="sxs-lookup"><span data-stu-id="ff77c-117">The import tool does not work with files greater than 200 GB.</span></span> <span data-ttu-id="ff77c-118">In this tutorial, we split the file into chunks of 100 GB each.</span><span class="sxs-lookup"><span data-stu-id="ff77c-118">In this tutorial, we split the file into chunks of 100 GB each.</span></span> <span data-ttu-id="ff77c-119">You can do this by using [Cygwin](https://cygwin.com/install.html).</span><span class="sxs-lookup"><span data-stu-id="ff77c-119">You can do this by using [Cygwin](https://cygwin.com/install.html).</span></span> <span data-ttu-id="ff77c-120">Cygwin supports Linux commands.</span><span class="sxs-lookup"><span data-stu-id="ff77c-120">Cygwin supports Linux commands.</span></span> <span data-ttu-id="ff77c-121">In this case, use the following command:</span><span class="sxs-lookup"><span data-stu-id="ff77c-121">In this case, use the following command:</span></span>

    split -b 100m 319GB.tsv

<span data-ttu-id="ff77c-122">The split operation creates files with the following names.</span><span class="sxs-lookup"><span data-stu-id="ff77c-122">The split operation creates files with the following names.</span></span>

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a><span data-ttu-id="ff77c-123">Get disks ready with data</span><span class="sxs-lookup"><span data-stu-id="ff77c-123">Get disks ready with data</span></span>
<span data-ttu-id="ff77c-124">Follow the instructions in [Using the Azure Import/Export service](../storage/storage-import-export-service.md) (under the **Prepare your drives** section) to prepare your hard drives.</span><span class="sxs-lookup"><span data-stu-id="ff77c-124">Follow the instructions in [Using the Azure Import/Export service](../storage/storage-import-export-service.md) (under the **Prepare your drives** section) to prepare your hard drives.</span></span> <span data-ttu-id="ff77c-125">Here's the overall sequence:</span><span class="sxs-lookup"><span data-stu-id="ff77c-125">Here's the overall sequence:</span></span>

1. <span data-ttu-id="ff77c-126">Procure a hard disk that meets the requirement to be used for the Azure Import/Export service.</span><span class="sxs-lookup"><span data-stu-id="ff77c-126">Procure a hard disk that meets the requirement to be used for the Azure Import/Export service.</span></span>
2. <span data-ttu-id="ff77c-127">Identify an Azure storage account where the data will be copied after it is shipped to the Azure datacenter.</span><span class="sxs-lookup"><span data-stu-id="ff77c-127">Identify an Azure storage account where the data will be copied after it is shipped to the Azure datacenter.</span></span>
3. <span data-ttu-id="ff77c-128">Use the [Azure Import/Export Tool](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), a command-line utility.</span><span class="sxs-lookup"><span data-stu-id="ff77c-128">Use the [Azure Import/Export Tool](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), a command-line utility.</span></span> <span data-ttu-id="ff77c-129">Here's a sample snippet that shows how to use the tool.</span><span class="sxs-lookup"><span data-stu-id="ff77c-129">Here's a sample snippet that shows how to use the tool.</span></span>

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    <span data-ttu-id="ff77c-130">See [Using the Azure Import/Export service](../storage/storage-import-export-service.md) for more sample snippets.</span><span class="sxs-lookup"><span data-stu-id="ff77c-130">See [Using the Azure Import/Export service](../storage/storage-import-export-service.md) for more sample snippets.</span></span>
4. <span data-ttu-id="ff77c-131">The preceding command creates a journal file at the specified location.</span><span class="sxs-lookup"><span data-stu-id="ff77c-131">The preceding command creates a journal file at the specified location.</span></span> <span data-ttu-id="ff77c-132">Use this journal file to create an import job from the [Azure classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ff77c-132">Use this journal file to create an import job from the [Azure classic portal](https://manage.windowsazure.com).</span></span>

## <a name="create-an-import-job"></a><span data-ttu-id="ff77c-133">Create an import job</span><span class="sxs-lookup"><span data-stu-id="ff77c-133">Create an import job</span></span>
<span data-ttu-id="ff77c-134">You can now create an import job by using the instructions in [Using the Azure Import/Export service](../storage/storage-import-export-service.md) (under the **Create the Import job** section).</span><span class="sxs-lookup"><span data-stu-id="ff77c-134">You can now create an import job by using the instructions in [Using the Azure Import/Export service](../storage/storage-import-export-service.md) (under the **Create the Import job** section).</span></span> <span data-ttu-id="ff77c-135">For this import job, with other details, also provide the journal file created while preparing the disk drives.</span><span class="sxs-lookup"><span data-stu-id="ff77c-135">For this import job, with other details, also provide the journal file created while preparing the disk drives.</span></span>

## <a name="physically-ship-the-disks"></a><span data-ttu-id="ff77c-136">Physically ship the disks</span><span class="sxs-lookup"><span data-stu-id="ff77c-136">Physically ship the disks</span></span>
<span data-ttu-id="ff77c-137">You can now physically ship the disks to an Azure datacenter.</span><span class="sxs-lookup"><span data-stu-id="ff77c-137">You can now physically ship the disks to an Azure datacenter.</span></span> <span data-ttu-id="ff77c-138">There, the data is copied over to the Azure Storage blobs you provided while creating the import job.</span><span class="sxs-lookup"><span data-stu-id="ff77c-138">There, the data is copied over to the Azure Storage blobs you provided while creating the import job.</span></span> <span data-ttu-id="ff77c-139">Also, while creating the job, if you opted to provide the tracking information later, you can now go back to your import job and update the tracking number.</span><span class="sxs-lookup"><span data-stu-id="ff77c-139">Also, while creating the job, if you opted to provide the tracking information later, you can now go back to your import job and update the tracking number.</span></span>

## <a name="copy-data-from-azure-storage-blobs-to-azure-data-lake-store"></a><span data-ttu-id="ff77c-140">Copy data from Azure Storage blobs to Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ff77c-140">Copy data from Azure Storage blobs to Azure Data Lake Store</span></span>
<span data-ttu-id="ff77c-141">After the status of the import job shows that it's completed, you can verify whether the data is available in the Azure Storage blobs you had specified.</span><span class="sxs-lookup"><span data-stu-id="ff77c-141">After the status of the import job shows that it's completed, you can verify whether the data is available in the Azure Storage blobs you had specified.</span></span> <span data-ttu-id="ff77c-142">You can then use a variety of methods to move that data from the blobs to Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ff77c-142">You can then use a variety of methods to move that data from the blobs to Azure Data Lake Store.</span></span> <span data-ttu-id="ff77c-143">For all the available options for uploading data, see [Ingesting data into Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="ff77c-143">For all the available options for uploading data, see [Ingesting data into Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span></span>

<span data-ttu-id="ff77c-144">In this section, we provide you with the JSON definitions that you can use to create an Azure Data Factory pipeline for copying data.</span><span class="sxs-lookup"><span data-stu-id="ff77c-144">In this section, we provide you with the JSON definitions that you can use to create an Azure Data Factory pipeline for copying data.</span></span> <span data-ttu-id="ff77c-145">You can use these JSON definitions from the [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), or [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ff77c-145">You can use these JSON definitions from the [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), or [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

### <a name="source-linked-service-azure-storage-blob"></a><span data-ttu-id="ff77c-146">Source linked service (Azure Storage blob)</span><span class="sxs-lookup"><span data-stu-id="ff77c-146">Source linked service (Azure Storage blob)</span></span>
````
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
````

### <a name="target-linked-service-azure-data-lake-store"></a><span data-ttu-id="ff77c-147">Target linked service (Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="ff77c-147">Target linked service (Azure Data Lake Store)</span></span>
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' to allow this data factory and the activities it runs to access this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from the OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a><span data-ttu-id="ff77c-148">Input data set</span><span class="sxs-lookup"><span data-stu-id="ff77c-148">Input data set</span></span>
````
{
    "name": "InputDataSet",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "importcontainer/vf1/"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
````
### <a name="output-data-set"></a><span data-ttu-id="ff77c-149">Output data set</span><span class="sxs-lookup"><span data-stu-id="ff77c-149">Output data set</span></span>
````
{
"name": "OutputDataSet",
"properties": {
  "published": false,
  "type": "AzureDataLakeStore",
  "linkedServiceName": "AzureDataLakeStoreLinkedService",
  "typeProperties": {
    "folderPath": "/importeddatafeb8job/"
    },
  "availability": {
    "frequency": "Hour",
    "interval": 1
    }
  }
}
````
### <a name="pipeline-copy-activity"></a><span data-ttu-id="ff77c-150">Pipeline (copy activity)</span><span class="sxs-lookup"><span data-stu-id="ff77c-150">Pipeline (copy activity)</span></span>
````
{
    "name": "CopyImportedData",
    "properties": {
        "description": "Pipeline with copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "AzureDataLakeStoreSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataSet"
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
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity"
            }
        ],
        "start": "2016-02-08T22:00:00Z",
        "end": "2016-02-08T23:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
````
<span data-ttu-id="ff77c-151">For more information, see [Move data from Azure Storage blob to Azure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md#example-copy-data-from-azure-blob-to-azure-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="ff77c-151">For more information, see [Move data from Azure Storage blob to Azure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md#example-copy-data-from-azure-blob-to-azure-data-lake-store).</span></span>

## <a name="reconstruct-the-data-files-in-azure-data-lake-store"></a><span data-ttu-id="ff77c-152">Reconstruct the data files in Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ff77c-152">Reconstruct the data files in Azure Data Lake Store</span></span>
<span data-ttu-id="ff77c-153">We started with a file that was 319 GB, and broke it down into files of smaller size so that it could be transferred by using the Azure Import/Export service.</span><span class="sxs-lookup"><span data-stu-id="ff77c-153">We started with a file that was 319 GB, and broke it down into files of smaller size so that it could be transferred by using the Azure Import/Export service.</span></span> <span data-ttu-id="ff77c-154">Now that the data is in Azure Data Lake Store, we can reconstruct the file to its original size.</span><span class="sxs-lookup"><span data-stu-id="ff77c-154">Now that the data is in Azure Data Lake Store, we can reconstruct the file to its original size.</span></span> <span data-ttu-id="ff77c-155">You can use the following Azure PowerShell cmldts to do so.</span><span class="sxs-lookup"><span data-stu-id="ff77c-155">You can use the following Azure PowerShell cmldts to do so.</span></span>

````
# Login to our account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch to the subscription you want to work with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  the files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a><span data-ttu-id="ff77c-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="ff77c-156">Next steps</span></span>
* [<span data-ttu-id="ff77c-157">Secure data in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ff77c-157">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="ff77c-158">Use Azure Data Lake Analytics with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ff77c-158">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="ff77c-159">Use Azure HDInsight with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ff77c-159">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
