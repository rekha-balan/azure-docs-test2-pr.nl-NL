---
title: Move Data to and from Azure Blob Storage using AzCopy | Microsoft Docs
description: Move Data to and from Azure Blob Storage using AzCopy
services: machine-learning,storage
documentationcenter: ''
author: deguhath
manager: jhubbard
editor: cgronlun
ms.assetid: c309ceb2-0e83-4a07-b16d-c997dcd62d5c
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/04/2017
ms.author: deguhath
ms.openlocfilehash: a25a35bc05781c6a52e21d697233ba1187ebeccf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855753"
---
# <a name="move-data-to-and-from-azure-blob-storage-using-azcopy"></a><span data-ttu-id="16150-103">Move data to and from Azure Blob Storage using AzCopy</span><span class="sxs-lookup"><span data-stu-id="16150-103">Move data to and from Azure Blob Storage using AzCopy</span></span>
<span data-ttu-id="16150-104">AzCopy is a command-line utility designed for uploading, downloading, and copying data to and from Microsoft Azure blob, file, and table storage.</span><span class="sxs-lookup"><span data-stu-id="16150-104">AzCopy is a command-line utility designed for uploading, downloading, and copying data to and from Microsoft Azure blob, file, and table storage.</span></span>

<span data-ttu-id="16150-105">For instructions on installing AzCopy and additional information on using it with the Azure platform, see [Getting Started with the AzCopy Command-Line Utility](../../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="16150-105">For instructions on installing AzCopy and additional information on using it with the Azure platform, see [Getting Started with the AzCopy Command-Line Utility](../../storage/common/storage-use-azcopy.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="16150-106">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](virtual-machines.md), then AzCopy is already installed on the VM.</span><span class="sxs-lookup"><span data-stu-id="16150-106">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](virtual-machines.md), then AzCopy is already installed on the VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="16150-107">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="16150-107">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="16150-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="16150-108">Prerequisites</span></span>
<span data-ttu-id="16150-109">This document assumes that you have an Azure subscription, a storage account and the corresponding storage key for that account.</span><span class="sxs-lookup"><span data-stu-id="16150-109">This document assumes that you have an Azure subscription, a storage account and the corresponding storage key for that account.</span></span> <span data-ttu-id="16150-110">Before uploading/downloading data, you must know your Azure storage account name and account key.</span><span class="sxs-lookup"><span data-stu-id="16150-110">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="16150-111">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="16150-111">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="16150-112">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="16150-112">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span>

## <a name="run-azcopy-commands"></a><span data-ttu-id="16150-113">Run AzCopy commands</span><span class="sxs-lookup"><span data-stu-id="16150-113">Run AzCopy commands</span></span>
<span data-ttu-id="16150-114">To run AzCopy commands, open a command window and navigate to the AzCopy installation directory on your computer, where the AzCopy.exe executable is located.</span><span class="sxs-lookup"><span data-stu-id="16150-114">To run AzCopy commands, open a command window and navigate to the AzCopy installation directory on your computer, where the AzCopy.exe executable is located.</span></span> 

<span data-ttu-id="16150-115">The basic syntax for AzCopy commands is:</span><span class="sxs-lookup"><span data-stu-id="16150-115">The basic syntax for AzCopy commands is:</span></span>

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> <span data-ttu-id="16150-116">You can add the AzCopy installation location to your system path and then run the commands from any directory.</span><span class="sxs-lookup"><span data-stu-id="16150-116">You can add the AzCopy installation location to your system path and then run the commands from any directory.</span></span> <span data-ttu-id="16150-117">By default, AzCopy is installed to *%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* or *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="16150-117">By default, AzCopy is installed to *%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* or *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span></span>
> 
> 

## <a name="upload-files-to-an-azure-blob"></a><span data-ttu-id="16150-118">Upload files to an Azure blob</span><span class="sxs-lookup"><span data-stu-id="16150-118">Upload files to an Azure blob</span></span>
<span data-ttu-id="16150-119">To upload a file, use the following command:</span><span class="sxs-lookup"><span data-stu-id="16150-119">To upload a file, use the following command:</span></span>

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a><span data-ttu-id="16150-120">Download files from an Azure blob</span><span class="sxs-lookup"><span data-stu-id="16150-120">Download files from an Azure blob</span></span>
<span data-ttu-id="16150-121">To download a file from an Azure blob, use the following command:</span><span class="sxs-lookup"><span data-stu-id="16150-121">To download a file from an Azure blob, use the following command:</span></span>

    # Downloading blobs to local file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a><span data-ttu-id="16150-122">Transfer blobs between Azure containers</span><span class="sxs-lookup"><span data-stu-id="16150-122">Transfer blobs between Azure containers</span></span>
<span data-ttu-id="16150-123">To transfer blobs between Azure containers, use the following command:</span><span class="sxs-lookup"><span data-stu-id="16150-123">To transfer blobs between Azure containers, use the following command:</span></span>

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: the sub directory in the container
    <your_local_directory>: directory of local file system where files to be uploaded from or the directory of local file system files to be downloaded to
    <file_pattern>: pattern of file names to be transferred. The standard wildcards are supported


## <a name="tips-for-using-azcopy"></a><span data-ttu-id="16150-124">Tips for using AzCopy</span><span class="sxs-lookup"><span data-stu-id="16150-124">Tips for using AzCopy</span></span>
> [!TIP]
> 1. <span data-ttu-id="16150-125">When **uploading** files, */S* uploads files recursively.</span><span class="sxs-lookup"><span data-stu-id="16150-125">When **uploading** files, */S* uploads files recursively.</span></span> <span data-ttu-id="16150-126">Without this parameter, files in subdirectories are not uploaded.</span><span class="sxs-lookup"><span data-stu-id="16150-126">Without this parameter, files in subdirectories are not uploaded.</span></span>  
> 2. <span data-ttu-id="16150-127">When **downloading** file, */S* searches the container recursively until all files in the specified directory and its subdirectories, or all files that match the specified pattern in the given directory and its subdirectories, are downloaded.</span><span class="sxs-lookup"><span data-stu-id="16150-127">When **downloading** file, */S* searches the container recursively until all files in the specified directory and its subdirectories, or all files that match the specified pattern in the given directory and its subdirectories, are downloaded.</span></span>  
> 3. <span data-ttu-id="16150-128">You cannot specify a **specific blob file** to download using the */Source* parameter.</span><span class="sxs-lookup"><span data-stu-id="16150-128">You cannot specify a **specific blob file** to download using the */Source* parameter.</span></span> <span data-ttu-id="16150-129">To download a specific file, specify the blob file name to download using the */Pattern* parameter.</span><span class="sxs-lookup"><span data-stu-id="16150-129">To download a specific file, specify the blob file name to download using the */Pattern* parameter.</span></span> <span data-ttu-id="16150-130">**/S** parameter can be used to have AzCopy look for a file name pattern recursively.</span><span class="sxs-lookup"><span data-stu-id="16150-130">**/S** parameter can be used to have AzCopy look for a file name pattern recursively.</span></span> <span data-ttu-id="16150-131">Without the pattern parameter, AzCopy downloads all files in that directory.</span><span class="sxs-lookup"><span data-stu-id="16150-131">Without the pattern parameter, AzCopy downloads all files in that directory.</span></span>
> 
> 

