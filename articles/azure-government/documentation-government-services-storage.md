---
title: Azure Government Storage | Microsoft Docs
description: This provides a comparision of features and guidance on developing applications for Azure Government
services: azure-government
cloud: gov
documentationcenter: ''
author: ryansoc
manager: zakramer
ms.assetid: 83df022b-d791-4efb-9fdf-8afe47a885d5
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 12/22/2016
ms.author: ryansoc
ms.openlocfilehash: 03c01e63470774d073c429c8a7ad778fa4d2f820
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552790"
---
# <a name="azure-government-storage"></a><span data-ttu-id="7bb8c-103">Azure Government Storage</span><span class="sxs-lookup"><span data-stu-id="7bb8c-103">Azure Government Storage</span></span>
## <a name="azure-storage"></a><span data-ttu-id="7bb8c-104">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7bb8c-104">Azure Storage</span></span>
<span data-ttu-id="7bb8c-105">For details on this service and how to use it, see [Azure Storage public documentation](../storage/index.md).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-105">For details on this service and how to use it, see [Azure Storage public documentation](../storage/index.md).</span></span>

### <a name="storage-service-availability-by-azure-government-region"></a><span data-ttu-id="7bb8c-106">Storage Service Availability by Azure Government Region</span><span class="sxs-lookup"><span data-stu-id="7bb8c-106">Storage Service Availability by Azure Government Region</span></span>

| <span data-ttu-id="7bb8c-107">Service</span><span class="sxs-lookup"><span data-stu-id="7bb8c-107">Service</span></span> | <span data-ttu-id="7bb8c-108">USGov Virginia</span><span class="sxs-lookup"><span data-stu-id="7bb8c-108">USGov Virginia</span></span> | <span data-ttu-id="7bb8c-109">USGov Iowa</span><span class="sxs-lookup"><span data-stu-id="7bb8c-109">USGov Iowa</span></span> | <span data-ttu-id="7bb8c-110">Notes</span><span class="sxs-lookup"><span data-stu-id="7bb8c-110">Notes</span></span>
| --- | --- | --- | --- |
| <span data-ttu-id="7bb8c-111">[Blob Storage] (../storage/storage-introduction.md#blob-storage)</span><span class="sxs-lookup"><span data-stu-id="7bb8c-111">[Blob Storage] (../storage/storage-introduction.md#blob-storage)</span></span> |<span data-ttu-id="7bb8c-112">GA</span><span class="sxs-lookup"><span data-stu-id="7bb8c-112">GA</span></span> |<span data-ttu-id="7bb8c-113">GA</span><span class="sxs-lookup"><span data-stu-id="7bb8c-113">GA</span></span> |
| <span data-ttu-id="7bb8c-114">[Table Storage] (../storage/storage-introduction.md#table-storage)</span><span class="sxs-lookup"><span data-stu-id="7bb8c-114">[Table Storage] (../storage/storage-introduction.md#table-storage)</span></span> |<span data-ttu-id="7bb8c-115">GA</span><span class="sxs-lookup"><span data-stu-id="7bb8c-115">GA</span></span>  |<span data-ttu-id="7bb8c-116">GA</span><span class="sxs-lookup"><span data-stu-id="7bb8c-116">GA</span></span> |
| <span data-ttu-id="7bb8c-117">[Queue Storage] (../storage/storage-introduction.md#queue-storage)</span><span class="sxs-lookup"><span data-stu-id="7bb8c-117">[Queue Storage] (../storage/storage-introduction.md#queue-storage)</span></span> |<span data-ttu-id="7bb8c-118">GA</span><span class="sxs-lookup"><span data-stu-id="7bb8c-118">GA</span></span> | <span data-ttu-id="7bb8c-119">GA</span><span class="sxs-lookup"><span data-stu-id="7bb8c-119">GA</span></span> |
| <span data-ttu-id="7bb8c-120">[File Storage] (../storage/storage-introduction.md#file-storage)</span><span class="sxs-lookup"><span data-stu-id="7bb8c-120">[File Storage] (../storage/storage-introduction.md#file-storage)</span></span> |<span data-ttu-id="7bb8c-121">GA</span><span class="sxs-lookup"><span data-stu-id="7bb8c-121">GA</span></span> |<span data-ttu-id="7bb8c-122">GA</span><span class="sxs-lookup"><span data-stu-id="7bb8c-122">GA</span></span> |
| <span data-ttu-id="7bb8c-123">[Hot/Cool Blob Storage] (../storage/storage-blob-storage-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="7bb8c-123">[Hot/Cool Blob Storage] (../storage/storage-blob-storage-tiers.md)</span></span> |<span data-ttu-id="7bb8c-124">NA</span><span class="sxs-lookup"><span data-stu-id="7bb8c-124">NA</span></span> |<span data-ttu-id="7bb8c-125">NA</span><span class="sxs-lookup"><span data-stu-id="7bb8c-125">NA</span></span> |
| <span data-ttu-id="7bb8c-126">[Storage Service Encryption] (../storage/storage-service-encryption.md)</span><span class="sxs-lookup"><span data-stu-id="7bb8c-126">[Storage Service Encryption] (../storage/storage-service-encryption.md)</span></span> |<span data-ttu-id="7bb8c-127">GA</span><span class="sxs-lookup"><span data-stu-id="7bb8c-127">GA</span></span> |<span data-ttu-id="7bb8c-128">GA</span><span class="sxs-lookup"><span data-stu-id="7bb8c-128">GA</span></span> |
| <span data-ttu-id="7bb8c-129">[Premium Storage] (../storage/storage-premium-storage.md)</span><span class="sxs-lookup"><span data-stu-id="7bb8c-129">[Premium Storage] (../storage/storage-premium-storage.md)</span></span> |<span data-ttu-id="7bb8c-130">GA</span><span class="sxs-lookup"><span data-stu-id="7bb8c-130">GA</span></span> |<span data-ttu-id="7bb8c-131">NA</span><span class="sxs-lookup"><span data-stu-id="7bb8c-131">NA</span></span> | <span data-ttu-id="7bb8c-132">Includes DS-series Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-132">Includes DS-series Virtual Machines.</span></span> |
| <span data-ttu-id="7bb8c-133">[Blob Import/Export] (../storage/storage-import-export-service.md)</span><span class="sxs-lookup"><span data-stu-id="7bb8c-133">[Blob Import/Export] (../storage/storage-import-export-service.md)</span></span> |<span data-ttu-id="7bb8c-134">GA</span><span class="sxs-lookup"><span data-stu-id="7bb8c-134">GA</span></span> |<span data-ttu-id="7bb8c-135">GA</span><span class="sxs-lookup"><span data-stu-id="7bb8c-135">GA</span></span> |
| <span data-ttu-id="7bb8c-136">[StorSimple] (../storsimple/storsimple-ova-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7bb8c-136">[StorSimple] (../storsimple/storsimple-ova-overview.md)</span></span> |<span data-ttu-id="7bb8c-137">GA</span><span class="sxs-lookup"><span data-stu-id="7bb8c-137">GA</span></span> |<span data-ttu-id="7bb8c-138">GA</span><span class="sxs-lookup"><span data-stu-id="7bb8c-138">GA</span></span> |

### <a name="variations"></a><span data-ttu-id="7bb8c-139">Variations</span><span class="sxs-lookup"><span data-stu-id="7bb8c-139">Variations</span></span>
<span data-ttu-id="7bb8c-140">The URLs for storage accounts in Azure Government are different:</span><span class="sxs-lookup"><span data-stu-id="7bb8c-140">The URLs for storage accounts in Azure Government are different:</span></span>

| <span data-ttu-id="7bb8c-141">Service Type</span><span class="sxs-lookup"><span data-stu-id="7bb8c-141">Service Type</span></span> | <span data-ttu-id="7bb8c-142">Azure Public</span><span class="sxs-lookup"><span data-stu-id="7bb8c-142">Azure Public</span></span> | <span data-ttu-id="7bb8c-143">Azure Government</span><span class="sxs-lookup"><span data-stu-id="7bb8c-143">Azure Government</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7bb8c-144">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="7bb8c-144">Blob Storage</span></span> |<span data-ttu-id="7bb8c-145">\*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="7bb8c-145">\*.blob.core.windows.net</span></span> |<span data-ttu-id="7bb8c-146">\*.blob.core.usgovcloudapi.net</span><span class="sxs-lookup"><span data-stu-id="7bb8c-146">\*.blob.core.usgovcloudapi.net</span></span> |
| <span data-ttu-id="7bb8c-147">Queue Storage</span><span class="sxs-lookup"><span data-stu-id="7bb8c-147">Queue Storage</span></span> |<span data-ttu-id="7bb8c-148">\*.queue.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="7bb8c-148">\*.queue.core.windows.net</span></span> |<span data-ttu-id="7bb8c-149">\*.queue.core.usgovcloudapi.net</span><span class="sxs-lookup"><span data-stu-id="7bb8c-149">\*.queue.core.usgovcloudapi.net</span></span> |
| <span data-ttu-id="7bb8c-150">Table Storage</span><span class="sxs-lookup"><span data-stu-id="7bb8c-150">Table Storage</span></span> |<span data-ttu-id="7bb8c-151">\*.table.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="7bb8c-151">\*.table.core.windows.net</span></span> |<span data-ttu-id="7bb8c-152">\*.table.core.usgovcloudapi.net</span><span class="sxs-lookup"><span data-stu-id="7bb8c-152">\*.table.core.usgovcloudapi.net</span></span> |
| <span data-ttu-id="7bb8c-153">File Storage</span><span class="sxs-lookup"><span data-stu-id="7bb8c-153">File Storage</span></span> |<span data-ttu-id="7bb8c-154">\*.file.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="7bb8c-154">\*.file.core.windows.net</span></span> |<span data-ttu-id="7bb8c-155">\*.file.core.usgovcloudapi.net</span><span class="sxs-lookup"><span data-stu-id="7bb8c-155">\*.file.core.usgovcloudapi.net</span></span> | 

> [!NOTE]
> <span data-ttu-id="7bb8c-156">All of your scripts and code needs to account for the appropriate endpoints.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-156">All of your scripts and code needs to account for the appropriate endpoints.</span></span>  <span data-ttu-id="7bb8c-157">See [Configure Azure Storage Connection Strings](../storage/storage-configure-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-157">See [Configure Azure Storage Connection Strings](../storage/storage-configure-connection-string.md).</span></span> 
>
>

<span data-ttu-id="7bb8c-158">For more information on APIs see the <a href="https://msdn.microsoft.com/en-us/library/azure/mt616540.aspx"> Cloud Storage Account Constructor</a>.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-158">For more information on APIs see the <a href="https://msdn.microsoft.com/en-us/library/azure/mt616540.aspx"> Cloud Storage Account Constructor</a>.</span></span>

<span data-ttu-id="7bb8c-159">The endpoint suffix to use in these overloads is core.usgovcloudapi.net</span><span class="sxs-lookup"><span data-stu-id="7bb8c-159">The endpoint suffix to use in these overloads is core.usgovcloudapi.net</span></span>

> [!NOTE]
> <span data-ttu-id="7bb8c-160">If error 53 "The network path was not found."</span><span class="sxs-lookup"><span data-stu-id="7bb8c-160">If error 53 "The network path was not found."</span></span> <span data-ttu-id="7bb8c-161">is returned, while [Mounting the file share] (../storage/storage-dotnet-how-to-use-files.md#mount-the-file-share).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-161">is returned, while [Mounting the file share] (../storage/storage-dotnet-how-to-use-files.md#mount-the-file-share).</span></span> <span data-ttu-id="7bb8c-162">It could be due to firewall blocking the outbound port.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-162">It could be due to firewall blocking the outbound port.</span></span> <span data-ttu-id="7bb8c-163">Try mounting the file share on VM that's in the same Azure Subscription as storage account.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-163">Try mounting the file share on VM that's in the same Azure Subscription as storage account.</span></span>
>
>

> [!NOTE]
> <span data-ttu-id="7bb8c-164">When deploying StorSimple Manager Service, use https://portal.azure.us/ and https://manage.windowsazure.us/ URLs for Azure portal and Classic portal respectively.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-164">When deploying StorSimple Manager Service, use https://portal.azure.us/ and https://manage.windowsazure.us/ URLs for Azure portal and Classic portal respectively.</span></span> <span data-ttu-id="7bb8c-165">For deployment instructions for StorSimple Virtual Array, see [StorSimple Virtual Array system requirements] (../storsimple/storsimple-ova-system-requirements.md) and for StorSimple 8000 series, see [StorSimple software, high availability, and networking requirements] (../storsimple/storsimple-system-requirements.md) and go to Deploy section from left navigation.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-165">For deployment instructions for StorSimple Virtual Array, see [StorSimple Virtual Array system requirements] (../storsimple/storsimple-ova-system-requirements.md) and for StorSimple 8000 series, see [StorSimple software, high availability, and networking requirements] (../storsimple/storsimple-system-requirements.md) and go to Deploy section from left navigation.</span></span> <span data-ttu-id="7bb8c-166">For general StorSimple documentation, see [What is StorSimple?] (../storsimple/index.md).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-166">For general StorSimple documentation, see [What is StorSimple?] (../storsimple/index.md).</span></span>
>
>

### <a name="considerations"></a><span data-ttu-id="7bb8c-167">Considerations</span><span class="sxs-lookup"><span data-stu-id="7bb8c-167">Considerations</span></span>
<span data-ttu-id="7bb8c-168">The following information identifies the Azure Government boundary for Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="7bb8c-168">The following information identifies the Azure Government boundary for Azure Storage:</span></span>

| <span data-ttu-id="7bb8c-169">Regulated/controlled data permitted</span><span class="sxs-lookup"><span data-stu-id="7bb8c-169">Regulated/controlled data permitted</span></span> | <span data-ttu-id="7bb8c-170">Regulated/controlled data not permitted</span><span class="sxs-lookup"><span data-stu-id="7bb8c-170">Regulated/controlled data not permitted</span></span> |
| --- | --- |
| <span data-ttu-id="7bb8c-171">Data entered, stored, and processed within an Azure Storage product can contain export controlled data.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-171">Data entered, stored, and processed within an Azure Storage product can contain export controlled data.</span></span> <span data-ttu-id="7bb8c-172">Static authenticators, such as passwords and smartcard PINs for access to Azure platform components.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-172">Static authenticators, such as passwords and smartcard PINs for access to Azure platform components.</span></span> <span data-ttu-id="7bb8c-173">Private keys of certificates used to manage Azure platform components.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-173">Private keys of certificates used to manage Azure platform components.</span></span> <span data-ttu-id="7bb8c-174">Other security information/secrets, such as certificates, encryption keys, master keys, and storage keys stored in Azure services.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-174">Other security information/secrets, such as certificates, encryption keys, master keys, and storage keys stored in Azure services.</span></span> |<span data-ttu-id="7bb8c-175">Azure Storage metadata is not permitted to contain export controlled data.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-175">Azure Storage metadata is not permitted to contain export controlled data.</span></span> <span data-ttu-id="7bb8c-176">This metadata includes all configuration data entered when creating and maintaining your storage product.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-176">This metadata includes all configuration data entered when creating and maintaining your storage product.</span></span>  <span data-ttu-id="7bb8c-177">Do not enter Regulated/controlled data into the following fields:  Resource groups, Deployment names, Resource names, Resource tags</span><span class="sxs-lookup"><span data-stu-id="7bb8c-177">Do not enter Regulated/controlled data into the following fields:  Resource groups, Deployment names, Resource names, Resource tags</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7bb8c-178">Next Steps</span><span class="sxs-lookup"><span data-stu-id="7bb8c-178">Next Steps</span></span>
<span data-ttu-id="7bb8c-179">For supplemental information and updates subscribe to the <a href="https://blogs.msdn.microsoft.com/azuregov/">Microsoft Azure Government Blog. </a></span><span class="sxs-lookup"><span data-stu-id="7bb8c-179">For supplemental information and updates subscribe to the <a href="https://blogs.msdn.microsoft.com/azuregov/">Microsoft Azure Government Blog. </a></span></span>