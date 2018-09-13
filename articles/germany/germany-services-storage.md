---
title: Azure Germany storage services | Microsoft Docs
description: Provides a comparison of storage services for Azure Germany
services: germany
cloud: na
documentationcenter: na
author: gitralf
manager: rainerst
ms.assetid: na
ms.service: germany
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: ralfwi
ms.openlocfilehash: d205c3d30cc862bdb61585972c9e9837772f3804
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869676"
---
# <a name="azure-germany-storage-services"></a><span data-ttu-id="8ff7a-103">Azure Germany storage services</span><span class="sxs-lookup"><span data-stu-id="8ff7a-103">Azure Germany storage services</span></span>
## <a name="storage"></a><span data-ttu-id="8ff7a-104">Storage</span><span class="sxs-lookup"><span data-stu-id="8ff7a-104">Storage</span></span>
<span data-ttu-id="8ff7a-105">For details on Azure Storage and how to use it, see the [Storage global documentation](../storage/index.yml).</span><span class="sxs-lookup"><span data-stu-id="8ff7a-105">For details on Azure Storage and how to use it, see the [Storage global documentation](../storage/index.yml).</span></span>

<span data-ttu-id="8ff7a-106">Data stored in Azure Storage is replicated to ensure high availability.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-106">Data stored in Azure Storage is replicated to ensure high availability.</span></span> <span data-ttu-id="8ff7a-107">For geo-redundant storage and read-access geo-redundant storage, Azure replicates data between *pairing regions*.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-107">For geo-redundant storage and read-access geo-redundant storage, Azure replicates data between *pairing regions*.</span></span> <span data-ttu-id="8ff7a-108">For Azure Germany, these pairing regions are:</span><span class="sxs-lookup"><span data-stu-id="8ff7a-108">For Azure Germany, these pairing regions are:</span></span>

| <span data-ttu-id="8ff7a-109">Primary region</span><span class="sxs-lookup"><span data-stu-id="8ff7a-109">Primary region</span></span> | <span data-ttu-id="8ff7a-110">Secondary (pairing) region</span><span class="sxs-lookup"><span data-stu-id="8ff7a-110">Secondary (pairing) region</span></span> |
| --- | --- |
| <span data-ttu-id="8ff7a-111">Germany Central</span><span class="sxs-lookup"><span data-stu-id="8ff7a-111">Germany Central</span></span> | <span data-ttu-id="8ff7a-112">Germany Northeast</span><span class="sxs-lookup"><span data-stu-id="8ff7a-112">Germany Northeast</span></span> |
| <span data-ttu-id="8ff7a-113">Germany Northeast</span><span class="sxs-lookup"><span data-stu-id="8ff7a-113">Germany Northeast</span></span> | <span data-ttu-id="8ff7a-114">Germany Central</span><span class="sxs-lookup"><span data-stu-id="8ff7a-114">Germany Central</span></span> |

<span data-ttu-id="8ff7a-115">Replication of data keeps the data within German borders.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-115">Replication of data keeps the data within German borders.</span></span> <span data-ttu-id="8ff7a-116">Primary and secondary regions are paired to ensure necessary distance between datacenters to ensure availability in the event of an area-wide outage or disaster.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-116">Primary and secondary regions are paired to ensure necessary distance between datacenters to ensure availability in the event of an area-wide outage or disaster.</span></span> <span data-ttu-id="8ff7a-117">For geo-redundant, high-availability storage, select either geo-redundant storage or read-access geo-redundant storage when you're creating a storage account.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-117">For geo-redundant, high-availability storage, select either geo-redundant storage or read-access geo-redundant storage when you're creating a storage account.</span></span>  

<span data-ttu-id="8ff7a-118">Storage Service Encryption safeguards data at rest within Azure storage accounts.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-118">Storage Service Encryption safeguards data at rest within Azure storage accounts.</span></span> <span data-ttu-id="8ff7a-119">When you enable that feature, Azure automatically encrypts data before persisting to storage.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-119">When you enable that feature, Azure automatically encrypts data before persisting to storage.</span></span> <span data-ttu-id="8ff7a-120">Data is encrypted through 256-bit AES encryption.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-120">Data is encrypted through 256-bit AES encryption.</span></span> <span data-ttu-id="8ff7a-121">Storage Service Encryption supports encryption of block blobs, append blobs, and page blobs.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-121">Storage Service Encryption supports encryption of block blobs, append blobs, and page blobs.</span></span>

### <a name="storage-service-availability-by-azure-germany-region"></a><span data-ttu-id="8ff7a-122">Storage service availability by Azure Germany region</span><span class="sxs-lookup"><span data-stu-id="8ff7a-122">Storage service availability by Azure Germany region</span></span>

| <span data-ttu-id="8ff7a-123">Service</span><span class="sxs-lookup"><span data-stu-id="8ff7a-123">Service</span></span> | <span data-ttu-id="8ff7a-124">Germany Central</span><span class="sxs-lookup"><span data-stu-id="8ff7a-124">Germany Central</span></span> | <span data-ttu-id="8ff7a-125">Germany Northeast</span><span class="sxs-lookup"><span data-stu-id="8ff7a-125">Germany Northeast</span></span> |
| --- | --- | --- | --- |
| [<span data-ttu-id="8ff7a-126">Blob storage</span><span class="sxs-lookup"><span data-stu-id="8ff7a-126">Blob storage</span></span>](../storage/common/storage-introduction.md#blob-storage) |<span data-ttu-id="8ff7a-127">GA</span><span class="sxs-lookup"><span data-stu-id="8ff7a-127">GA</span></span> |<span data-ttu-id="8ff7a-128">GA</span><span class="sxs-lookup"><span data-stu-id="8ff7a-128">GA</span></span> |
| [<span data-ttu-id="8ff7a-129">Azure Files</span><span class="sxs-lookup"><span data-stu-id="8ff7a-129">Azure Files</span></span>](../storage/common/storage-introduction.md#azure-files) | <span data-ttu-id="8ff7a-130">GA</span><span class="sxs-lookup"><span data-stu-id="8ff7a-130">GA</span></span> | <span data-ttu-id="8ff7a-131">GA</span><span class="sxs-lookup"><span data-stu-id="8ff7a-131">GA</span></span> |
| [<span data-ttu-id="8ff7a-132">Table storage</span><span class="sxs-lookup"><span data-stu-id="8ff7a-132">Table storage</span></span>](../storage/common/storage-introduction.md#table-storage) |<span data-ttu-id="8ff7a-133">GA</span><span class="sxs-lookup"><span data-stu-id="8ff7a-133">GA</span></span>  |<span data-ttu-id="8ff7a-134">GA</span><span class="sxs-lookup"><span data-stu-id="8ff7a-134">GA</span></span> |
| [<span data-ttu-id="8ff7a-135">Queue storage</span><span class="sxs-lookup"><span data-stu-id="8ff7a-135">Queue storage</span></span>](../storage/common/storage-introduction.md#queue-storage) |<span data-ttu-id="8ff7a-136">GA</span><span class="sxs-lookup"><span data-stu-id="8ff7a-136">GA</span></span> | <span data-ttu-id="8ff7a-137">GA</span><span class="sxs-lookup"><span data-stu-id="8ff7a-137">GA</span></span> |
| [<span data-ttu-id="8ff7a-138">Hot/cool blob storage</span><span class="sxs-lookup"><span data-stu-id="8ff7a-138">Hot/cool blob storage</span></span>](../storage/blobs/storage-blob-storage-tiers.md) |<span data-ttu-id="8ff7a-139">GA</span><span class="sxs-lookup"><span data-stu-id="8ff7a-139">GA</span></span> |<span data-ttu-id="8ff7a-140">GA</span><span class="sxs-lookup"><span data-stu-id="8ff7a-140">GA</span></span> |
| [<span data-ttu-id="8ff7a-141">Storage Service Encryption</span><span class="sxs-lookup"><span data-stu-id="8ff7a-141">Storage Service Encryption</span></span>](../storage/common/storage-service-encryption.md) |<span data-ttu-id="8ff7a-142">GA</span><span class="sxs-lookup"><span data-stu-id="8ff7a-142">GA</span></span> |<span data-ttu-id="8ff7a-143">GA</span><span class="sxs-lookup"><span data-stu-id="8ff7a-143">GA</span></span> |
| [<span data-ttu-id="8ff7a-144">Premium Storage</span><span class="sxs-lookup"><span data-stu-id="8ff7a-144">Premium Storage</span></span>](../virtual-machines/windows/premium-storage.md) |<span data-ttu-id="8ff7a-145">GA</span><span class="sxs-lookup"><span data-stu-id="8ff7a-145">GA</span></span> |<span data-ttu-id="8ff7a-146">GA</span><span class="sxs-lookup"><span data-stu-id="8ff7a-146">GA</span></span> |
| <span data-ttu-id="8ff7a-147">Import/Export</span><span class="sxs-lookup"><span data-stu-id="8ff7a-147">Import/Export</span></span> |<span data-ttu-id="8ff7a-148">NA</span><span class="sxs-lookup"><span data-stu-id="8ff7a-148">NA</span></span> |<span data-ttu-id="8ff7a-149">NA</span><span class="sxs-lookup"><span data-stu-id="8ff7a-149">NA</span></span> |
| <span data-ttu-id="8ff7a-150">StorSimple</span><span class="sxs-lookup"><span data-stu-id="8ff7a-150">StorSimple</span></span> |<span data-ttu-id="8ff7a-151">NA</span><span class="sxs-lookup"><span data-stu-id="8ff7a-151">NA</span></span> |<span data-ttu-id="8ff7a-152">NA</span><span class="sxs-lookup"><span data-stu-id="8ff7a-152">NA</span></span> |

### <a name="variations"></a><span data-ttu-id="8ff7a-153">Variations</span><span class="sxs-lookup"><span data-stu-id="8ff7a-153">Variations</span></span>
<span data-ttu-id="8ff7a-154">The URLs for storage accounts in Azure Germany are different from those in global Azure:</span><span class="sxs-lookup"><span data-stu-id="8ff7a-154">The URLs for storage accounts in Azure Germany are different from those in global Azure:</span></span>

| <span data-ttu-id="8ff7a-155">Service type</span><span class="sxs-lookup"><span data-stu-id="8ff7a-155">Service type</span></span> | <span data-ttu-id="8ff7a-156">Global Azure</span><span class="sxs-lookup"><span data-stu-id="8ff7a-156">Global Azure</span></span> | <span data-ttu-id="8ff7a-157">Azure Germany</span><span class="sxs-lookup"><span data-stu-id="8ff7a-157">Azure Germany</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8ff7a-158">Blob storage</span><span class="sxs-lookup"><span data-stu-id="8ff7a-158">Blob storage</span></span> | <span data-ttu-id="8ff7a-159">\*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="8ff7a-159">\*.blob.core.windows.net</span></span> | <span data-ttu-id="8ff7a-160">\*.blob.core.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="8ff7a-160">\*.blob.core.cloudapi.de</span></span> |
| <span data-ttu-id="8ff7a-161">Azure Files</span><span class="sxs-lookup"><span data-stu-id="8ff7a-161">Azure Files</span></span> | <span data-ttu-id="8ff7a-162">\*.file.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="8ff7a-162">\*.file.core.windows.net</span></span> | <span data-ttu-id="8ff7a-163">\*.file.core.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="8ff7a-163">\*.file.core.cloudapi.de</span></span> | 
| <span data-ttu-id="8ff7a-164">Queue storage</span><span class="sxs-lookup"><span data-stu-id="8ff7a-164">Queue storage</span></span> | <span data-ttu-id="8ff7a-165">\*.queue.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="8ff7a-165">\*.queue.core.windows.net</span></span> | <span data-ttu-id="8ff7a-166">\*.queue.core.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="8ff7a-166">\*.queue.core.cloudapi.de</span></span> |
| <span data-ttu-id="8ff7a-167">Table storage</span><span class="sxs-lookup"><span data-stu-id="8ff7a-167">Table storage</span></span> | <span data-ttu-id="8ff7a-168">\*.table.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="8ff7a-168">\*.table.core.windows.net</span></span> | <span data-ttu-id="8ff7a-169">\*.table.core.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="8ff7a-169">\*.table.core.cloudapi.de</span></span> |

> [!NOTE]
> <span data-ttu-id="8ff7a-170">All your scripts and code need to account for the appropriate endpoints.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-170">All your scripts and code need to account for the appropriate endpoints.</span></span> <span data-ttu-id="8ff7a-171">For more information, see [Configure Azure Storage connection strings](../storage/common/storage-configure-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="8ff7a-171">For more information, see [Configure Azure Storage connection strings](../storage/common/storage-configure-connection-string.md).</span></span> 
>
>

<span data-ttu-id="8ff7a-172">For more information on APIs, see [Cloud Storage Account Constructor](https://msdn.microsoft.com/library/azure/mt616540.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ff7a-172">For more information on APIs, see [Cloud Storage Account Constructor](https://msdn.microsoft.com/library/azure/mt616540.aspx).</span></span>

<span data-ttu-id="8ff7a-173">The endpoint suffix to use in these overloads is *core.cloudapi.de*.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-173">The endpoint suffix to use in these overloads is *core.cloudapi.de*.</span></span>

> [!NOTE]
> <span data-ttu-id="8ff7a-174">If error 53 ("The network path was not found") is returned while you're [mounting the file share](../storage/files/storage-dotnet-how-to-use-files.md), a firewall might be blocking the outbound port.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-174">If error 53 ("The network path was not found") is returned while you're [mounting the file share](../storage/files/storage-dotnet-how-to-use-files.md), a firewall might be blocking the outbound port.</span></span> <span data-ttu-id="8ff7a-175">Try mounting the file share on a virtual machine that's in the same Azure subscription as storage account.</span><span class="sxs-lookup"><span data-stu-id="8ff7a-175">Try mounting the file share on a virtual machine that's in the same Azure subscription as storage account.</span></span>
>
>


## <a name="next-steps"></a><span data-ttu-id="8ff7a-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="8ff7a-176">Next steps</span></span>
<span data-ttu-id="8ff7a-177">For supplemental information and updates, subscribe to the [Azure Germany blog](https://blogs.msdn.microsoft.com/azuregermany/).</span><span class="sxs-lookup"><span data-stu-id="8ff7a-177">For supplemental information and updates, subscribe to the [Azure Germany blog](https://blogs.msdn.microsoft.com/azuregermany/).</span></span>
