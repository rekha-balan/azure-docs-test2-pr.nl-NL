---
title: Move Data to or from Azure Blob Storage using SSIS connectors | Microsoft Docs
description: Move Data to or from Azure Blob Storage using SSIS connectors.
services: machine-learning,storage
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 96a1b5fb-34d1-4b9b-8d99-2bb8289e0398
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 3147b9abcca3836c61aec39ff34111d9bec20ec7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554698"
---
# <a name="move-data-to-or-from-azure-blob-storage-using-ssis-connectors"></a><span data-ttu-id="dbd63-103">Move data to or from Azure Blob Storage using SSIS connectors</span><span class="sxs-lookup"><span data-stu-id="dbd63-103">Move data to or from Azure Blob Storage using SSIS connectors</span></span>
<span data-ttu-id="dbd63-104">The [SQL Server Integration Services Feature Pack for Azure](https://msdn.microsoft.com/library/mt146770.aspx) provides components to connect to Azure, transfer data between Azure and on-premises data sources, and process data stored in Azure.</span><span class="sxs-lookup"><span data-stu-id="dbd63-104">The [SQL Server Integration Services Feature Pack for Azure](https://msdn.microsoft.com/library/mt146770.aspx) provides components to connect to Azure, transfer data between Azure and on-premises data sources, and process data stored in Azure.</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="dbd63-105">Once customers have moved on-premises data into the cloud, they can access it from any Azure service to leverage the full power of the suite of Azure technologies.</span><span class="sxs-lookup"><span data-stu-id="dbd63-105">Once customers have moved on-premises data into the cloud, they can access it from any Azure service to leverage the full power of the suite of Azure technologies.</span></span> <span data-ttu-id="dbd63-106">It may be used, for example, in Azure Machine Learning or on an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="dbd63-106">It may be used, for example, in Azure Machine Learning or on an HDInsight cluster.</span></span>

<span data-ttu-id="dbd63-107">This is typically be the first step for the [SQL](machine-learning-data-science-process-sql-walkthrough.md) and [HDInsight](machine-learning-data-science-process-hive-walkthrough.md) walkthroughs.</span><span class="sxs-lookup"><span data-stu-id="dbd63-107">This is typically be the first step for the [SQL](machine-learning-data-science-process-sql-walkthrough.md) and [HDInsight](machine-learning-data-science-process-hive-walkthrough.md) walkthroughs.</span></span>

<span data-ttu-id="dbd63-108">For a discussion of canonical scenarios that use SSIS to accomplish business needs common in hybrid data integration scenarios, see [Doing more with SQL Server Integration Services Feature Pack for Azure](http://blogs.msdn.com/b/ssis/archive/2015/06/25/doing-more-with-sql-server-integration-services-feature-pack-for-azure.aspx) blog.</span><span class="sxs-lookup"><span data-stu-id="dbd63-108">For a discussion of canonical scenarios that use SSIS to accomplish business needs common in hybrid data integration scenarios, see [Doing more with SQL Server Integration Services Feature Pack for Azure](http://blogs.msdn.com/b/ssis/archive/2015/06/25/doing-more-with-sql-server-integration-services-feature-pack-for-azure.aspx) blog.</span></span>

> [!NOTE]
> <span data-ttu-id="dbd63-109">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="dbd63-109">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="dbd63-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dbd63-110">Prerequisites</span></span>
<span data-ttu-id="dbd63-111">To perform the tasks described in this article, you must have an Azure subscription and an Azure storage account set up.</span><span class="sxs-lookup"><span data-stu-id="dbd63-111">To perform the tasks described in this article, you must have an Azure subscription and an Azure storage account set up.</span></span> <span data-ttu-id="dbd63-112">You must know your Azure storage account name and account key to upload or download data.</span><span class="sxs-lookup"><span data-stu-id="dbd63-112">You must know your Azure storage account name and account key to upload or download data.</span></span>

* <span data-ttu-id="dbd63-113">To set up an **Azure subscription**, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dbd63-113">To set up an **Azure subscription**, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="dbd63-114">For instructions on creating a **storage account** and for getting account and key information, see [About Azure storage accounts](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="dbd63-114">For instructions on creating a **storage account** and for getting account and key information, see [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span>

<span data-ttu-id="dbd63-115">To use the **SSIS connectors**, you must download:</span><span class="sxs-lookup"><span data-stu-id="dbd63-115">To use the **SSIS connectors**, you must download:</span></span>

* <span data-ttu-id="dbd63-116">**SQL Server 2014 or 2016 Standard (or above)**: Install includes SQL Server Integration Services.</span><span class="sxs-lookup"><span data-stu-id="dbd63-116">**SQL Server 2014 or 2016 Standard (or above)**: Install includes SQL Server Integration Services.</span></span>
* <span data-ttu-id="dbd63-117">**Microsoft SQL Server 2014 or 2016 Integration Services Feature Pack for Azure**: These can be downloaded, respectively, from the [SQL Server 2014 Integration Services](http://www.microsoft.com/download/details.aspx?id=47366) and [SQL Server 2016 Integration Services](https://www.microsoft.com/download/details.aspx?id=49492) pages.</span><span class="sxs-lookup"><span data-stu-id="dbd63-117">**Microsoft SQL Server 2014 or 2016 Integration Services Feature Pack for Azure**: These can be downloaded, respectively, from the [SQL Server 2014 Integration Services](http://www.microsoft.com/download/details.aspx?id=47366) and [SQL Server 2016 Integration Services](https://www.microsoft.com/download/details.aspx?id=49492) pages.</span></span>

> [!NOTE]
> <span data-ttu-id="dbd63-118">SSIS is installed with SQL Server, but is not included in the Express version.</span><span class="sxs-lookup"><span data-stu-id="dbd63-118">SSIS is installed with SQL Server, but is not included in the Express version.</span></span> <span data-ttu-id="dbd63-119">For information on what applications are included in various editions of SQL Server, see [SQL Server Editions](http://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/)</span><span class="sxs-lookup"><span data-stu-id="dbd63-119">For information on what applications are included in various editions of SQL Server, see [SQL Server Editions](http://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/)</span></span>
> 
> 

<span data-ttu-id="dbd63-120">For training materials on SSIS, see [Hands On Training for SSIS](http://www.microsoft.com/download/details.aspx?id=20766)</span><span class="sxs-lookup"><span data-stu-id="dbd63-120">For training materials on SSIS, see [Hands On Training for SSIS](http://www.microsoft.com/download/details.aspx?id=20766)</span></span>

<span data-ttu-id="dbd63-121">For information on how to get up-and-running using SISS to build simple extraction, transformation, and load (ETL) packages, see [SSIS Tutorial: Creating a Simple ETL Package](https://msdn.microsoft.com/library/ms169917.aspx).</span><span class="sxs-lookup"><span data-stu-id="dbd63-121">For information on how to get up-and-running using SISS to build simple extraction, transformation, and load (ETL) packages, see [SSIS Tutorial: Creating a Simple ETL Package](https://msdn.microsoft.com/library/ms169917.aspx).</span></span>

## <a name="download-nyc-taxi-dataset"></a><span data-ttu-id="dbd63-122">Download NYC Taxi dataset</span><span class="sxs-lookup"><span data-stu-id="dbd63-122">Download NYC Taxi dataset</span></span>
<span data-ttu-id="dbd63-123">The example described here use a publicly available dataset -- the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span><span class="sxs-lookup"><span data-stu-id="dbd63-123">The example described here use a publicly available dataset -- the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="dbd63-124">The dataset consists of about 173 million taxi rides in NYC in the year 2013.</span><span class="sxs-lookup"><span data-stu-id="dbd63-124">The dataset consists of about 173 million taxi rides in NYC in the year 2013.</span></span> <span data-ttu-id="dbd63-125">There are two types of data: trip details data and fare data.</span><span class="sxs-lookup"><span data-stu-id="dbd63-125">There are two types of data: trip details data and fare data.</span></span> <span data-ttu-id="dbd63-126">As there is a file for each month, we have 24 files in all, each of which is approximately 2GB uncompressed.</span><span class="sxs-lookup"><span data-stu-id="dbd63-126">As there is a file for each month, we have 24 files in all, each of which is approximately 2GB uncompressed.</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="dbd63-127">Upload data to Azure blob storage</span><span class="sxs-lookup"><span data-stu-id="dbd63-127">Upload data to Azure blob storage</span></span>
<span data-ttu-id="dbd63-128">To move data using the SSIS feature pack from on-premises to Azure blob storage, we use an instance of the [**Azure Blob Upload Task**](https://msdn.microsoft.com/library/mt146776.aspx), shown here:</span><span class="sxs-lookup"><span data-stu-id="dbd63-128">To move data using the SSIS feature pack from on-premises to Azure blob storage, we use an instance of the [**Azure Blob Upload Task**](https://msdn.microsoft.com/library/mt146776.aspx), shown here:</span></span>

![configure-data-science-vm](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-move-data-to-azure-blob-using-ssis/ssis-azure-blob-upload-task.png)

<span data-ttu-id="dbd63-130">The parameters that the task uses are described here:</span><span class="sxs-lookup"><span data-stu-id="dbd63-130">The parameters that the task uses are described here:</span></span>

| <span data-ttu-id="dbd63-131">Field</span><span class="sxs-lookup"><span data-stu-id="dbd63-131">Field</span></span> | <span data-ttu-id="dbd63-132">Description</span><span class="sxs-lookup"><span data-stu-id="dbd63-132">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dbd63-133">**AzureStorageConnection**</span><span class="sxs-lookup"><span data-stu-id="dbd63-133">**AzureStorageConnection**</span></span> |<span data-ttu-id="dbd63-134">Specifies an existing Azure Storage Connection Manager or creates a new one that refers to an Azure storage account that points to where the blob files are hosted.</span><span class="sxs-lookup"><span data-stu-id="dbd63-134">Specifies an existing Azure Storage Connection Manager or creates a new one that refers to an Azure storage account that points to where the blob files are hosted.</span></span> |
| <span data-ttu-id="dbd63-135">**BlobContainer**</span><span class="sxs-lookup"><span data-stu-id="dbd63-135">**BlobContainer**</span></span> |<span data-ttu-id="dbd63-136">Specifies the name of the blob container that hold the uploaded files as blobs.</span><span class="sxs-lookup"><span data-stu-id="dbd63-136">Specifies the name of the blob container that hold the uploaded files as blobs.</span></span> |
| <span data-ttu-id="dbd63-137">**BlobDirectory**</span><span class="sxs-lookup"><span data-stu-id="dbd63-137">**BlobDirectory**</span></span> |<span data-ttu-id="dbd63-138">Specifies the blob directory where the uploaded file is stored as a block blob.</span><span class="sxs-lookup"><span data-stu-id="dbd63-138">Specifies the blob directory where the uploaded file is stored as a block blob.</span></span> <span data-ttu-id="dbd63-139">The blob directory is a virtual hierarchical structure.</span><span class="sxs-lookup"><span data-stu-id="dbd63-139">The blob directory is a virtual hierarchical structure.</span></span> <span data-ttu-id="dbd63-140">If the blob already exists, it ia replaced.</span><span class="sxs-lookup"><span data-stu-id="dbd63-140">If the blob already exists, it ia replaced.</span></span> |
| <span data-ttu-id="dbd63-141">**LocalDirectory**</span><span class="sxs-lookup"><span data-stu-id="dbd63-141">**LocalDirectory**</span></span> |<span data-ttu-id="dbd63-142">Specifies the local directory that contains the files to be uploaded.</span><span class="sxs-lookup"><span data-stu-id="dbd63-142">Specifies the local directory that contains the files to be uploaded.</span></span> |
| <span data-ttu-id="dbd63-143">**FileName**</span><span class="sxs-lookup"><span data-stu-id="dbd63-143">**FileName**</span></span> |<span data-ttu-id="dbd63-144">Specifies a name filter to select files with the specified name pattern.</span><span class="sxs-lookup"><span data-stu-id="dbd63-144">Specifies a name filter to select files with the specified name pattern.</span></span> <span data-ttu-id="dbd63-145">For example, MySheet\*.xls\* includes files such as MySheet001.xls and MySheetABC.xlsx</span><span class="sxs-lookup"><span data-stu-id="dbd63-145">For example, MySheet\*.xls\* includes files such as MySheet001.xls and MySheetABC.xlsx</span></span> |
| <span data-ttu-id="dbd63-146">**TimeRangeFrom/TimeRangeTo**</span><span class="sxs-lookup"><span data-stu-id="dbd63-146">**TimeRangeFrom/TimeRangeTo**</span></span> |<span data-ttu-id="dbd63-147">Specifies a time range filter.</span><span class="sxs-lookup"><span data-stu-id="dbd63-147">Specifies a time range filter.</span></span> <span data-ttu-id="dbd63-148">Files modified after *TimeRangeFrom* and before *TimeRangeTo* are included.</span><span class="sxs-lookup"><span data-stu-id="dbd63-148">Files modified after *TimeRangeFrom* and before *TimeRangeTo* are included.</span></span> |

> [!NOTE]
> <span data-ttu-id="dbd63-149">The **AzureStorageConnection** credentials need to be correct and the **BlobContainer** must exist before the transfer is attempted.</span><span class="sxs-lookup"><span data-stu-id="dbd63-149">The **AzureStorageConnection** credentials need to be correct and the **BlobContainer** must exist before the transfer is attempted.</span></span>
> 
> 

## <a name="download-data-from-azure-blob-storage"></a><span data-ttu-id="dbd63-150">Download data from Azure blob storage</span><span class="sxs-lookup"><span data-stu-id="dbd63-150">Download data from Azure blob storage</span></span>
<span data-ttu-id="dbd63-151">To download data from Azure blob storage to on-premise storage with SSIS, use an instance of the [Azure Blob Upload Task](https://msdn.microsoft.com/library/mt146779.aspx).</span><span class="sxs-lookup"><span data-stu-id="dbd63-151">To download data from Azure blob storage to on-premise storage with SSIS, use an instance of the [Azure Blob Upload Task](https://msdn.microsoft.com/library/mt146779.aspx).</span></span>

## <a name="more-advanced-ssis-azure-scenarios"></a><span data-ttu-id="dbd63-152">More advanced SSIS-Azure scenarios</span><span class="sxs-lookup"><span data-stu-id="dbd63-152">More advanced SSIS-Azure scenarios</span></span>
<span data-ttu-id="dbd63-153">The SSIS feature pack allows for more complex flows to be handled by packaging tasks together.</span><span class="sxs-lookup"><span data-stu-id="dbd63-153">The SSIS feature pack allows for more complex flows to be handled by packaging tasks together.</span></span> <span data-ttu-id="dbd63-154">For example, the blob data could feed directly into an HDInsight cluster, whose output could be downloaded back to a blob and then to on-premise storage.</span><span class="sxs-lookup"><span data-stu-id="dbd63-154">For example, the blob data could feed directly into an HDInsight cluster, whose output could be downloaded back to a blob and then to on-premise storage.</span></span> <span data-ttu-id="dbd63-155">SSIS can run Hive and Pig jobs on an HDInsight cluster using additional SSIS connectors:</span><span class="sxs-lookup"><span data-stu-id="dbd63-155">SSIS can run Hive and Pig jobs on an HDInsight cluster using additional SSIS connectors:</span></span>

* <span data-ttu-id="dbd63-156">To run a Hive script on an Azure HDInsight cluster with SSIS, use [Azure HDInsight Hive Task](https://msdn.microsoft.com/library/mt146771.aspx).</span><span class="sxs-lookup"><span data-stu-id="dbd63-156">To run a Hive script on an Azure HDInsight cluster with SSIS, use [Azure HDInsight Hive Task](https://msdn.microsoft.com/library/mt146771.aspx).</span></span>
* <span data-ttu-id="dbd63-157">To run a Pig script on an Azure HDInsight cluster with SSIS, use [Azure HDInsight Pig Task](https://msdn.microsoft.com/library/mt146781.aspx).</span><span class="sxs-lookup"><span data-stu-id="dbd63-157">To run a Pig script on an Azure HDInsight cluster with SSIS, use [Azure HDInsight Pig Task](https://msdn.microsoft.com/library/mt146781.aspx).</span></span>


