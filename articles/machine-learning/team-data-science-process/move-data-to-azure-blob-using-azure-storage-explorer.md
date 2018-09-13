---
title: Move Data to and from Blob Storage with Azure Storage Explorer | Microsoft Docs
description: Move Data to and from Azure Blob Storage using Azure Storage Explorer
services: machine-learning,storage
documentationcenter: ''
author: deguhath
manager: jhubbard
editor: cgronlun
ms.assetid: 10bd283f-0875-4c67-af63-6492270b7656
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/04/2017
ms.author: deguhath
ms.openlocfilehash: 464290901959ee052059b092b737e369928bd19b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857462"
---
# <a name="move-data-to-and-from-azure-blob-storage-using-azure-storage-explorer"></a><span data-ttu-id="784a0-103">Move data to and from Azure Blob Storage using Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="784a0-103">Move data to and from Azure Blob Storage using Azure Storage Explorer</span></span>
<span data-ttu-id="784a0-104">Azure Storage Explorer is a free tool from Microsoft that allows you to work with Azure Storage data on Windows, macOS, and Linux.</span><span class="sxs-lookup"><span data-stu-id="784a0-104">Azure Storage Explorer is a free tool from Microsoft that allows you to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="784a0-105">This topic describes how to use it to upload and download data from Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="784a0-105">This topic describes how to use it to upload and download data from Azure blob storage.</span></span> <span data-ttu-id="784a0-106">The tool can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="784a0-106">The tool can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="784a0-107">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](virtual-machines.md), then Azure Storage Explorer is already installed on the VM.</span><span class="sxs-lookup"><span data-stu-id="784a0-107">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](virtual-machines.md), then Azure Storage Explorer is already installed on the VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="784a0-108">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../../storage/blobs/storage-dotnet-how-to-use-blobs.md) and [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="784a0-108">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../../storage/blobs/storage-dotnet-how-to-use-blobs.md) and [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>   
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="784a0-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="784a0-109">Prerequisites</span></span>
<span data-ttu-id="784a0-110">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span><span class="sxs-lookup"><span data-stu-id="784a0-110">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span></span> <span data-ttu-id="784a0-111">Before uploading/downloading data, you must know your Azure storage account name and account key.</span><span class="sxs-lookup"><span data-stu-id="784a0-111">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span> 

* <span data-ttu-id="784a0-112">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="784a0-112">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="784a0-113">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="784a0-113">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="784a0-114">Make a note the access key for your storage account as you need this key to connect to the account with the Azure Storage Explorer tool.</span><span class="sxs-lookup"><span data-stu-id="784a0-114">Make a note the access key for your storage account as you need this key to connect to the account with the Azure Storage Explorer tool.</span></span>
* <span data-ttu-id="784a0-115">The Azure Storage Explorer tool can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="784a0-115">The Azure Storage Explorer tool can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="784a0-116">Accept the defaults during install.</span><span class="sxs-lookup"><span data-stu-id="784a0-116">Accept the defaults during install.</span></span>

<a id="explorer"></a>

## <a name="use-azure-storage-explorer"></a><span data-ttu-id="784a0-117">Use Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="784a0-117">Use Azure Storage Explorer</span></span>
<span data-ttu-id="784a0-118">The following steps document how to upload/download data using Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="784a0-118">The following steps document how to upload/download data using Azure Storage Explorer.</span></span> 

1. <span data-ttu-id="784a0-119">Launch Microsoft Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="784a0-119">Launch Microsoft Azure Storage Explorer.</span></span>
2. <span data-ttu-id="784a0-120">To bring up the **Sign in to your account...** wizard, select **Azure account settings** icon, then **Add an account** and enter you credentials.</span><span class="sxs-lookup"><span data-stu-id="784a0-120">To bring up the **Sign in to your account...** wizard, select **Azure account settings** icon, then **Add an account** and enter you credentials.</span></span> <span data-ttu-id="784a0-121">![Add an Azure storage account](./media/move-data-to-azure-blob-using-azure-storage-explorer/add-an-azure-store-account.png)</span><span class="sxs-lookup"><span data-stu-id="784a0-121">![Add an Azure storage account](./media/move-data-to-azure-blob-using-azure-storage-explorer/add-an-azure-store-account.png)</span></span>
3. <span data-ttu-id="784a0-122">To bring up the **Connect to Azure Storage** wizard, select the **Connect to Azure storage** icon.</span><span class="sxs-lookup"><span data-stu-id="784a0-122">To bring up the **Connect to Azure Storage** wizard, select the **Connect to Azure storage** icon.</span></span> <span data-ttu-id="784a0-123">![Connect to Azure storage](./media/move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-1.png)</span><span class="sxs-lookup"><span data-stu-id="784a0-123">![Connect to Azure storage](./media/move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-1.png)</span></span>
4. <span data-ttu-id="784a0-124">Enter the access key from your Azure storage account on the **Connect to Azure Storage** wizard and then **Next**.</span><span class="sxs-lookup"><span data-stu-id="784a0-124">Enter the access key from your Azure storage account on the **Connect to Azure Storage** wizard and then **Next**.</span></span> <span data-ttu-id="784a0-125">![Connect to Azure storage](./media/move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-2.png)</span><span class="sxs-lookup"><span data-stu-id="784a0-125">![Connect to Azure storage](./media/move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-2.png)</span></span>
5. <span data-ttu-id="784a0-126">Enter storage account name in the **Account name** box and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="784a0-126">Enter storage account name in the **Account name** box and then select **Next**.</span></span> <span data-ttu-id="784a0-127">![Attach external storage](./media/move-data-to-azure-blob-using-azure-storage-explorer/attach-external-storage.png)</span><span class="sxs-lookup"><span data-stu-id="784a0-127">![Attach external storage](./media/move-data-to-azure-blob-using-azure-storage-explorer/attach-external-storage.png)</span></span>
6. <span data-ttu-id="784a0-128">The storage account added should now be listed.</span><span class="sxs-lookup"><span data-stu-id="784a0-128">The storage account added should now be listed.</span></span> <span data-ttu-id="784a0-129">To create a blob container in a storage account, right-click the **Blob Containers** node in that account, select **Create Blob Container**, and enter a name.</span><span class="sxs-lookup"><span data-stu-id="784a0-129">To create a blob container in a storage account, right-click the **Blob Containers** node in that account, select **Create Blob Container**, and enter a name.</span></span>
7. <span data-ttu-id="784a0-130">To upload data to a container, select the target container and click the **Upload** button.![Storage accounts](./media/move-data-to-azure-blob-using-azure-storage-explorer/storage-accounts.png)</span><span class="sxs-lookup"><span data-stu-id="784a0-130">To upload data to a container, select the target container and click the **Upload** button.![Storage accounts](./media/move-data-to-azure-blob-using-azure-storage-explorer/storage-accounts.png)</span></span>
8. <span data-ttu-id="784a0-131">Click on the **...** to the right of the **Files** box, select one or multiple files to upload from the file system and click **Upload** to begin uploading the files.![Upload files](./media/move-data-to-azure-blob-using-azure-storage-explorer/upload-files-to-blob.png)</span><span class="sxs-lookup"><span data-stu-id="784a0-131">Click on the **...** to the right of the **Files** box, select one or multiple files to upload from the file system and click **Upload** to begin uploading the files.![Upload files](./media/move-data-to-azure-blob-using-azure-storage-explorer/upload-files-to-blob.png)</span></span>
9. <span data-ttu-id="784a0-132">To download data, selecting the blob in the corresponding container to download and click **Download**.</span><span class="sxs-lookup"><span data-stu-id="784a0-132">To download data, selecting the blob in the corresponding container to download and click **Download**.</span></span> <span data-ttu-id="784a0-133">![Download files](./media/move-data-to-azure-blob-using-azure-storage-explorer/download-files-from-blob.png)</span><span class="sxs-lookup"><span data-stu-id="784a0-133">![Download files](./media/move-data-to-azure-blob-using-azure-storage-explorer/download-files-from-blob.png)</span></span>

