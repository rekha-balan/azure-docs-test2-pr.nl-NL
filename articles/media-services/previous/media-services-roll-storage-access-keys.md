---
title: Update Media Services after rolling storage access keys | Microsoft Docs
description: This articles give you guidance on how to update Media Services after rolling storage access keys.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: a892ebb0-0ea0-4fc8-b715-60347cc5c95b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2018
ms.author: milanga;cenkdin;juliako
ms.openlocfilehash: e8d8067fcf30b16dd3dbc7f6cf50129d837aa3a5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855719"
---
# <a name="update-media-services-after-rolling-storage-access-keys"></a><span data-ttu-id="18ea9-103">Update Media Services after rolling storage access keys</span><span class="sxs-lookup"><span data-stu-id="18ea9-103">Update Media Services after rolling storage access keys</span></span>

<span data-ttu-id="18ea9-104">When you create a new Azure Media Services (AMS) account, you are also asked to select an Azure Storage account that is used to store your media content.</span><span class="sxs-lookup"><span data-stu-id="18ea9-104">When you create a new Azure Media Services (AMS) account, you are also asked to select an Azure Storage account that is used to store your media content.</span></span> <span data-ttu-id="18ea9-105">You can add more than one storage accounts to your Media Services account.</span><span class="sxs-lookup"><span data-stu-id="18ea9-105">You can add more than one storage accounts to your Media Services account.</span></span> <span data-ttu-id="18ea9-106">This article shows how to rotate storage keys.</span><span class="sxs-lookup"><span data-stu-id="18ea9-106">This article shows how to rotate storage keys.</span></span> <span data-ttu-id="18ea9-107">It also shows how to add storage accounts to a media account.</span><span class="sxs-lookup"><span data-stu-id="18ea9-107">It also shows how to add storage accounts to a media account.</span></span> 

<span data-ttu-id="18ea9-108">To perform the actions described in this article, you should be using [Azure Resource Manager APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](https://docs.microsoft.com/powershell/module/azurerm.media).</span><span class="sxs-lookup"><span data-stu-id="18ea9-108">To perform the actions described in this article, you should be using [Azure Resource Manager APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](https://docs.microsoft.com/powershell/module/azurerm.media).</span></span>  <span data-ttu-id="18ea9-109">For more information, see [How to manage Azure resources with PowerShell and Resource Manager](../../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="18ea9-109">For more information, see [How to manage Azure resources with PowerShell and Resource Manager](../../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>

## <a name="overview"></a><span data-ttu-id="18ea9-110">Overview</span><span class="sxs-lookup"><span data-stu-id="18ea9-110">Overview</span></span>

<span data-ttu-id="18ea9-111">When a new storage account is created, Azure generates two 512-bit storage access keys, which are used to authenticate access to your storage account.</span><span class="sxs-lookup"><span data-stu-id="18ea9-111">When a new storage account is created, Azure generates two 512-bit storage access keys, which are used to authenticate access to your storage account.</span></span> <span data-ttu-id="18ea9-112">To keep your storage connections more secure, it is recommended to periodically regenerate and rotate your storage access key.</span><span class="sxs-lookup"><span data-stu-id="18ea9-112">To keep your storage connections more secure, it is recommended to periodically regenerate and rotate your storage access key.</span></span> <span data-ttu-id="18ea9-113">Two access keys (primary and secondary) are provided in order to enable you to maintain connections to the storage account using one access key while you regenerate the other access key.</span><span class="sxs-lookup"><span data-stu-id="18ea9-113">Two access keys (primary and secondary) are provided in order to enable you to maintain connections to the storage account using one access key while you regenerate the other access key.</span></span> <span data-ttu-id="18ea9-114">This procedure is also called "rolling access keys".</span><span class="sxs-lookup"><span data-stu-id="18ea9-114">This procedure is also called "rolling access keys".</span></span>

<span data-ttu-id="18ea9-115">Media Services depends on a storage key provided to it.</span><span class="sxs-lookup"><span data-stu-id="18ea9-115">Media Services depends on a storage key provided to it.</span></span> <span data-ttu-id="18ea9-116">Specifically, the locators that are used to stream or download your assets depend on the specified storage access key.</span><span class="sxs-lookup"><span data-stu-id="18ea9-116">Specifically, the locators that are used to stream or download your assets depend on the specified storage access key.</span></span> <span data-ttu-id="18ea9-117">When an AMS account is created, it takes a dependency on the primary storage access key by default but as a user you can update the storage key that AMS has.</span><span class="sxs-lookup"><span data-stu-id="18ea9-117">When an AMS account is created, it takes a dependency on the primary storage access key by default but as a user you can update the storage key that AMS has.</span></span> <span data-ttu-id="18ea9-118">You must make sure to let Media Services know which key to use by following steps described in this article.</span><span class="sxs-lookup"><span data-stu-id="18ea9-118">You must make sure to let Media Services know which key to use by following steps described in this article.</span></span>  

>[!NOTE]
> <span data-ttu-id="18ea9-119">If you have multiple storage accounts, you would perform this procedure with each storage account.</span><span class="sxs-lookup"><span data-stu-id="18ea9-119">If you have multiple storage accounts, you would perform this procedure with each storage account.</span></span> <span data-ttu-id="18ea9-120">The order in which you rotate storage keys is not fixed.</span><span class="sxs-lookup"><span data-stu-id="18ea9-120">The order in which you rotate storage keys is not fixed.</span></span> <span data-ttu-id="18ea9-121">You can rotate the secondary key first and then the primary key or vice versa.</span><span class="sxs-lookup"><span data-stu-id="18ea9-121">You can rotate the secondary key first and then the primary key or vice versa.</span></span>
>
> <span data-ttu-id="18ea9-122">Before executing steps described in this article on a production account, make sure to test them on a pre-production account.</span><span class="sxs-lookup"><span data-stu-id="18ea9-122">Before executing steps described in this article on a production account, make sure to test them on a pre-production account.</span></span>
>

## <a name="steps-to-rotate-storage-keys"></a><span data-ttu-id="18ea9-123">Steps to rotate storage keys</span><span class="sxs-lookup"><span data-stu-id="18ea9-123">Steps to rotate storage keys</span></span> 
 
 1. <span data-ttu-id="18ea9-124">Change the storage account Primary key through the powershell cmdlet or [Azure](https://portal.azure.com/) portal.</span><span class="sxs-lookup"><span data-stu-id="18ea9-124">Change the storage account Primary key through the powershell cmdlet or [Azure](https://portal.azure.com/) portal.</span></span>
 2. <span data-ttu-id="18ea9-125">Call Sync-AzureRmMediaServiceStorageKeys cmdlet with appropriate params to force media account to pick up storage account keys</span><span class="sxs-lookup"><span data-stu-id="18ea9-125">Call Sync-AzureRmMediaServiceStorageKeys cmdlet with appropriate params to force media account to pick up storage account keys</span></span>
 
    <span data-ttu-id="18ea9-126">The following example shows how to sync keys to storage accounts.</span><span class="sxs-lookup"><span data-stu-id="18ea9-126">The following example shows how to sync keys to storage accounts.</span></span>
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. <span data-ttu-id="18ea9-127">Wait an hour or so.</span><span class="sxs-lookup"><span data-stu-id="18ea9-127">Wait an hour or so.</span></span> <span data-ttu-id="18ea9-128">Verify the streaming scenarios are working.</span><span class="sxs-lookup"><span data-stu-id="18ea9-128">Verify the streaming scenarios are working.</span></span>
 4. <span data-ttu-id="18ea9-129">Change storage account secondary key through the powershell cmdlet or Azure portal.</span><span class="sxs-lookup"><span data-stu-id="18ea9-129">Change storage account secondary key through the powershell cmdlet or Azure portal.</span></span>
 5. <span data-ttu-id="18ea9-130">Call Sync-AzureRmMediaServiceStorageKeys powershell with appropriate params to force media account to pick up new storage account keys.</span><span class="sxs-lookup"><span data-stu-id="18ea9-130">Call Sync-AzureRmMediaServiceStorageKeys powershell with appropriate params to force media account to pick up new storage account keys.</span></span> 
 6. <span data-ttu-id="18ea9-131">Wait an hour or so.</span><span class="sxs-lookup"><span data-stu-id="18ea9-131">Wait an hour or so.</span></span> <span data-ttu-id="18ea9-132">Verify the streaming scenarios are working.</span><span class="sxs-lookup"><span data-stu-id="18ea9-132">Verify the streaming scenarios are working.</span></span>
 
### <a name="a-powershell-cmdlet-example"></a><span data-ttu-id="18ea9-133">A powershell cmdlet example</span><span class="sxs-lookup"><span data-stu-id="18ea9-133">A powershell cmdlet example</span></span> 

<span data-ttu-id="18ea9-134">The following example demonstrates how to get the storage account and sync it with the AMS account.</span><span class="sxs-lookup"><span data-stu-id="18ea9-134">The following example demonstrates how to get the storage account and sync it with the AMS account.</span></span>

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-to-add-storage-accounts-to-your-ams-account"></a><span data-ttu-id="18ea9-135">Steps to add storage accounts to your AMS account</span><span class="sxs-lookup"><span data-stu-id="18ea9-135">Steps to add storage accounts to your AMS account</span></span>

<span data-ttu-id="18ea9-136">The following article shows how to add storage accounts to your AMS account: [Attach multiple storage accounts to a Media Services account](meda-services-managing-multiple-storage-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="18ea9-136">The following article shows how to add storage accounts to your AMS account: [Attach multiple storage accounts to a Media Services account](meda-services-managing-multiple-storage-accounts.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="18ea9-137">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="18ea9-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="18ea9-138">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="18ea9-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="18ea9-139">Acknowledgments</span><span class="sxs-lookup"><span data-stu-id="18ea9-139">Acknowledgments</span></span>
<span data-ttu-id="18ea9-140">We would like to acknowledge the following people who contributed towards creating this document: Cenk Dingiloglu, Milan Gada, Seva Titov.</span><span class="sxs-lookup"><span data-stu-id="18ea9-140">We would like to acknowledge the following people who contributed towards creating this document: Cenk Dingiloglu, Milan Gada, Seva Titov.</span></span>
