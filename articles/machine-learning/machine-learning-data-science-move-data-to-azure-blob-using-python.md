---
title: Move Data to and from Azure Blob Storage using Python | Microsoft Docs
description: Move Data to and from Azure Blob Storage using Python
services: machine-learning,storage
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 24276252-b3dd-4edf-9e5d-f6803f8ccccc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 9cfadabb26509085ff0c760f21a56196d82b9456
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555071"
---
# <a name="move-data-to-and-from-azure-blob-storage-using-python"></a><span data-ttu-id="7e54c-103">Move data to and from Azure Blob Storage using Python</span><span class="sxs-lookup"><span data-stu-id="7e54c-103">Move data to and from Azure Blob Storage using Python</span></span>
<span data-ttu-id="7e54c-104">This topic describes how to list, upload, and download blobs using the Python API.</span><span class="sxs-lookup"><span data-stu-id="7e54c-104">This topic describes how to list, upload, and download blobs using the Python API.</span></span> <span data-ttu-id="7e54c-105">With the Python API provided in Azure SDK, you can:</span><span class="sxs-lookup"><span data-stu-id="7e54c-105">With the Python API provided in Azure SDK, you can:</span></span>

* <span data-ttu-id="7e54c-106">Create a container</span><span class="sxs-lookup"><span data-stu-id="7e54c-106">Create a container</span></span>
* <span data-ttu-id="7e54c-107">Upload a blob into a container</span><span class="sxs-lookup"><span data-stu-id="7e54c-107">Upload a blob into a container</span></span>
* <span data-ttu-id="7e54c-108">Download blobs</span><span class="sxs-lookup"><span data-stu-id="7e54c-108">Download blobs</span></span>
* <span data-ttu-id="7e54c-109">List the blobs in a container</span><span class="sxs-lookup"><span data-stu-id="7e54c-109">List the blobs in a container</span></span>
* <span data-ttu-id="7e54c-110">Delete a blob</span><span class="sxs-lookup"><span data-stu-id="7e54c-110">Delete a blob</span></span>

<span data-ttu-id="7e54c-111">For more information about using the Python API, see [How to Use the Blob Storage Service from Python](../storage/storage-python-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="7e54c-111">For more information about using the Python API, see [How to Use the Blob Storage Service from Python](../storage/storage-python-how-to-use-blob-storage.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="7e54c-112">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on the VM.</span><span class="sxs-lookup"><span data-stu-id="7e54c-112">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on the VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="7e54c-113">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="7e54c-113">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="7e54c-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7e54c-114">Prerequisites</span></span>
<span data-ttu-id="7e54c-115">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span><span class="sxs-lookup"><span data-stu-id="7e54c-115">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span></span> <span data-ttu-id="7e54c-116">Before uploading/downloading data, you must know your Azure storage account name and account key.</span><span class="sxs-lookup"><span data-stu-id="7e54c-116">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="7e54c-117">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e54c-117">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7e54c-118">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="7e54c-118">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span>

## <a name="upload-data-to-blob"></a><span data-ttu-id="7e54c-119">Upload Data to Blob</span><span class="sxs-lookup"><span data-stu-id="7e54c-119">Upload Data to Blob</span></span>
<span data-ttu-id="7e54c-120">Add the following snippet near the top of any Python code in which you wish to programmatically access Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="7e54c-120">Add the following snippet near the top of any Python code in which you wish to programmatically access Azure Storage:</span></span>

    from azure.storage.blob import BlobService

<span data-ttu-id="7e54c-121">The **BlobService** object lets you work with containers and blobs.</span><span class="sxs-lookup"><span data-stu-id="7e54c-121">The **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="7e54c-122">The following code creates a BlobService object using the storage account name and account key.</span><span class="sxs-lookup"><span data-stu-id="7e54c-122">The following code creates a BlobService object using the storage account name and account key.</span></span> <span data-ttu-id="7e54c-123">Replace account name and account key with your real account and key.</span><span class="sxs-lookup"><span data-stu-id="7e54c-123">Replace account name and account key with your real account and key.</span></span>

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

<span data-ttu-id="7e54c-124">Use the following methods to upload data to a blob:</span><span class="sxs-lookup"><span data-stu-id="7e54c-124">Use the following methods to upload data to a blob:</span></span>

1. <span data-ttu-id="7e54c-125">put\_block\_blob\_from\_path (uploads the contents of a file from the specified path)</span><span class="sxs-lookup"><span data-stu-id="7e54c-125">put\_block\_blob\_from\_path (uploads the contents of a file from the specified path)</span></span>
2. <span data-ttu-id="7e54c-126">put\_block_blob\_from\_file (uploads the contents from an already opened file/stream)</span><span class="sxs-lookup"><span data-stu-id="7e54c-126">put\_block_blob\_from\_file (uploads the contents from an already opened file/stream)</span></span>
3. <span data-ttu-id="7e54c-127">put\_block\_blob\_from\_bytes (uploads an array of bytes)</span><span class="sxs-lookup"><span data-stu-id="7e54c-127">put\_block\_blob\_from\_bytes (uploads an array of bytes)</span></span>
4. <span data-ttu-id="7e54c-128">put\_block\_blob\_from\_text (uploads the specified text value using the specified encoding)</span><span class="sxs-lookup"><span data-stu-id="7e54c-128">put\_block\_blob\_from\_text (uploads the specified text value using the specified encoding)</span></span>

<span data-ttu-id="7e54c-129">The following sample code uploads a local file to a container:</span><span class="sxs-lookup"><span data-stu-id="7e54c-129">The following sample code uploads a local file to a container:</span></span>

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="7e54c-130">The following sample code uploads all the files (excluding directories) in a local directory to blob storage:</span><span class="sxs-lookup"><span data-stu-id="7e54c-130">The following sample code uploads all the files (excluding directories) in a local directory to blob storage:</span></span>

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in the LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading the data %s"%blob_name


## <a name="download-data-from-blob"></a><span data-ttu-id="7e54c-131">Download Data from Blob</span><span class="sxs-lookup"><span data-stu-id="7e54c-131">Download Data from Blob</span></span>
<span data-ttu-id="7e54c-132">Use the following methods to download data from a blob:</span><span class="sxs-lookup"><span data-stu-id="7e54c-132">Use the following methods to download data from a blob:</span></span>

1. <span data-ttu-id="7e54c-133">get\_blob\_to\_path</span><span class="sxs-lookup"><span data-stu-id="7e54c-133">get\_blob\_to\_path</span></span>
2. <span data-ttu-id="7e54c-134">get\_blob\_to\_file</span><span class="sxs-lookup"><span data-stu-id="7e54c-134">get\_blob\_to\_file</span></span>
3. <span data-ttu-id="7e54c-135">get\_blob\_to\_bytes</span><span class="sxs-lookup"><span data-stu-id="7e54c-135">get\_blob\_to\_bytes</span></span>
4. <span data-ttu-id="7e54c-136">get\_blob\_to\_text</span><span class="sxs-lookup"><span data-stu-id="7e54c-136">get\_blob\_to\_text</span></span>

<span data-ttu-id="7e54c-137">These methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span><span class="sxs-lookup"><span data-stu-id="7e54c-137">These methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="7e54c-138">The following sample code downloads the contents of a blob in a container to a local file:</span><span class="sxs-lookup"><span data-stu-id="7e54c-138">The following sample code downloads the contents of a blob in a container to a local file:</span></span>

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="7e54c-139">The following sample code downloads all blobs from a container.</span><span class="sxs-lookup"><span data-stu-id="7e54c-139">The following sample code downloads all blobs from a container.</span></span> <span data-ttu-id="7e54c-140">It uses list\_blobs to get the list of available blobs in the container and downloads them to a local directory.</span><span class="sxs-lookup"><span data-stu-id="7e54c-140">It uses list\_blobs to get the list of available blobs in the container and downloads them to a local directory.</span></span>

    from azure.storage.blob import BlobService
    from os.path import join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)

    # List all blobs and download them one by one
    blobs = blob_service.list_blobs(CONTAINER_NAME)
    for blob in blobs:
        local_file = join(LOCAL_DIRECT, blob.name)
        try:
            blob_service.get_blob_to_path(CONTAINER_NAME, blob.name, local_file)
        except:
            print "something wrong happened when downloading the data %s"%blob.name
