---
title: StorSimple 8000 series as backup target with Veeam | Microsoft Docs
description: Describes the StorSimple backup target configuration with Veeam.
services: storsimple
documentationcenter: ''
author: harshakirank
manager: matd
editor: ''
ms.assetid: ''
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/06/2016
ms.author: hkanna
ms.openlocfilehash: 1f4281651f181157b3d9273c13ac6810f71a8358
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563419"
---
# <a name="storsimple-as-a-backup-target-with-veeam"></a><span data-ttu-id="ad818-103">StorSimple as a backup target with Veeam</span><span class="sxs-lookup"><span data-stu-id="ad818-103">StorSimple as a backup target with Veeam</span></span>

## <a name="overview"></a><span data-ttu-id="ad818-104">Overview</span><span class="sxs-lookup"><span data-stu-id="ad818-104">Overview</span></span>

<span data-ttu-id="ad818-105">Azure StorSimple is a hybrid cloud storage solution from Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ad818-105">Azure StorSimple is a hybrid cloud storage solution from Microsoft.</span></span> <span data-ttu-id="ad818-106">StorSimple addresses the complexities of exponential data growth by using an Azure Storage account as an extension of the on-premises solution and automatically tiering data across on-premises storage and cloud storage.</span><span class="sxs-lookup"><span data-stu-id="ad818-106">StorSimple addresses the complexities of exponential data growth by using an Azure Storage account as an extension of the on-premises solution and automatically tiering data across on-premises storage and cloud storage.</span></span>

<span data-ttu-id="ad818-107">In this article, we discuss StorSimple integration with Veeam, and best practices for integrating both solutions.</span><span class="sxs-lookup"><span data-stu-id="ad818-107">In this article, we discuss StorSimple integration with Veeam, and best practices for integrating both solutions.</span></span> <span data-ttu-id="ad818-108">We also make recommendations on how to set up Veeam to best integrate with StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ad818-108">We also make recommendations on how to set up Veeam to best integrate with StorSimple.</span></span> <span data-ttu-id="ad818-109">We defer to Veeam best practices, backup architects, and administrators for the best way to set up Veeam to meet individual backup requirements and service-level agreements (SLAs).</span><span class="sxs-lookup"><span data-stu-id="ad818-109">We defer to Veeam best practices, backup architects, and administrators for the best way to set up Veeam to meet individual backup requirements and service-level agreements (SLAs).</span></span>

<span data-ttu-id="ad818-110">Although we illustrate configuration steps and key concepts, this article is by no means a step-by-step configuration or installation guide.</span><span class="sxs-lookup"><span data-stu-id="ad818-110">Although we illustrate configuration steps and key concepts, this article is by no means a step-by-step configuration or installation guide.</span></span> <span data-ttu-id="ad818-111">We assume that the basic components and infrastructure are in working order and ready to support the concepts that we describe.</span><span class="sxs-lookup"><span data-stu-id="ad818-111">We assume that the basic components and infrastructure are in working order and ready to support the concepts that we describe.</span></span>

### <a name="who-should-read-this"></a><span data-ttu-id="ad818-112">Who should read this?</span><span class="sxs-lookup"><span data-stu-id="ad818-112">Who should read this?</span></span>

<span data-ttu-id="ad818-113">The information in this article will be most helpful to backup administrators, storage administrators, and storage architects who have knowledge of storage, Windows Server 2012 R2, Ethernet, cloud services, and Veeam.</span><span class="sxs-lookup"><span data-stu-id="ad818-113">The information in this article will be most helpful to backup administrators, storage administrators, and storage architects who have knowledge of storage, Windows Server 2012 R2, Ethernet, cloud services, and Veeam.</span></span>

### <a name="supported-versions"></a><span data-ttu-id="ad818-114">Supported versions</span><span class="sxs-lookup"><span data-stu-id="ad818-114">Supported versions</span></span>

-   <span data-ttu-id="ad818-115">Veeam 9 and later versions</span><span class="sxs-lookup"><span data-stu-id="ad818-115">Veeam 9 and later versions</span></span>
-   [<span data-ttu-id="ad818-116">StorSimple Update 3 and later versions</span><span class="sxs-lookup"><span data-stu-id="ad818-116">StorSimple Update 3 and later versions</span></span>](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a><span data-ttu-id="ad818-117">Why StorSimple as a backup target?</span><span class="sxs-lookup"><span data-stu-id="ad818-117">Why StorSimple as a backup target?</span></span>

<span data-ttu-id="ad818-118">StorSimple is a good choice for a backup target because:</span><span class="sxs-lookup"><span data-stu-id="ad818-118">StorSimple is a good choice for a backup target because:</span></span>

-   <span data-ttu-id="ad818-119">It provides standard, local storage for backup applications to use as a fast backup destination, without any changes.</span><span class="sxs-lookup"><span data-stu-id="ad818-119">It provides standard, local storage for backup applications to use as a fast backup destination, without any changes.</span></span> <span data-ttu-id="ad818-120">You also can use StorSimple for a quick restore of recent backups.</span><span class="sxs-lookup"><span data-stu-id="ad818-120">You also can use StorSimple for a quick restore of recent backups.</span></span>
-   <span data-ttu-id="ad818-121">Its cloud tiering is seamlessly integrated with an Azure cloud storage account to use cost-effective Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ad818-121">Its cloud tiering is seamlessly integrated with an Azure cloud storage account to use cost-effective Azure Storage.</span></span>
-   <span data-ttu-id="ad818-122">It automatically provides offsite storage for disaster recovery.</span><span class="sxs-lookup"><span data-stu-id="ad818-122">It automatically provides offsite storage for disaster recovery.</span></span>


## <a name="key-concepts"></a><span data-ttu-id="ad818-123">Key concepts</span><span class="sxs-lookup"><span data-stu-id="ad818-123">Key concepts</span></span>

<span data-ttu-id="ad818-124">As with any storage solution, a careful assessment of the solution’s storage performance, SLAs, rate of change, and capacity growth needs is critical to success.</span><span class="sxs-lookup"><span data-stu-id="ad818-124">As with any storage solution, a careful assessment of the solution’s storage performance, SLAs, rate of change, and capacity growth needs is critical to success.</span></span> <span data-ttu-id="ad818-125">The main idea is that by introducing a cloud tier, your access times and throughputs to the cloud play a fundamental role in the ability of StorSimple to do its job.</span><span class="sxs-lookup"><span data-stu-id="ad818-125">The main idea is that by introducing a cloud tier, your access times and throughputs to the cloud play a fundamental role in the ability of StorSimple to do its job.</span></span>

<span data-ttu-id="ad818-126">StorSimple is designed to provide storage to applications that operate on a well-defined working set of data (hot data).</span><span class="sxs-lookup"><span data-stu-id="ad818-126">StorSimple is designed to provide storage to applications that operate on a well-defined working set of data (hot data).</span></span> <span data-ttu-id="ad818-127">In this model, the working set of data is stored on the local tiers, and the remaining nonworking/cold/archived set of data is tiered to the cloud.</span><span class="sxs-lookup"><span data-stu-id="ad818-127">In this model, the working set of data is stored on the local tiers, and the remaining nonworking/cold/archived set of data is tiered to the cloud.</span></span> <span data-ttu-id="ad818-128">This model is represented in the following figure.</span><span class="sxs-lookup"><span data-stu-id="ad818-128">This model is represented in the following figure.</span></span> <span data-ttu-id="ad818-129">The nearly flat green line represents the data stored on the local tiers of the StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="ad818-129">The nearly flat green line represents the data stored on the local tiers of the StorSimple device.</span></span> <span data-ttu-id="ad818-130">The red line represents the total amount of data stored on the StorSimple solution across all tiers.</span><span class="sxs-lookup"><span data-stu-id="ad818-130">The red line represents the total amount of data stored on the StorSimple solution across all tiers.</span></span> <span data-ttu-id="ad818-131">The space between the flat green line and the exponential red curve represents the total amount of data stored in the cloud.</span><span class="sxs-lookup"><span data-stu-id="ad818-131">The space between the flat green line and the exponential red curve represents the total amount of data stored in the cloud.</span></span>

<span data-ttu-id="ad818-132">**StorSimple tiering**
![StorSimple tiering diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/image1.jpg)</span><span class="sxs-lookup"><span data-stu-id="ad818-132">**StorSimple tiering**
![StorSimple tiering diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/image1.jpg)</span></span>

<span data-ttu-id="ad818-133">With this architecture in mind, you will find that StorSimple is ideally suited to operate as a backup target.</span><span class="sxs-lookup"><span data-stu-id="ad818-133">With this architecture in mind, you will find that StorSimple is ideally suited to operate as a backup target.</span></span> <span data-ttu-id="ad818-134">You can use StorSimple to:</span><span class="sxs-lookup"><span data-stu-id="ad818-134">You can use StorSimple to:</span></span>

-   <span data-ttu-id="ad818-135">Perform your most frequent restores from the local working set of data.</span><span class="sxs-lookup"><span data-stu-id="ad818-135">Perform your most frequent restores from the local working set of data.</span></span>
-   <span data-ttu-id="ad818-136">Use the cloud for offsite disaster recovery and older data, where restores are less frequent.</span><span class="sxs-lookup"><span data-stu-id="ad818-136">Use the cloud for offsite disaster recovery and older data, where restores are less frequent.</span></span>

## <a name="storsimple-benefits"></a><span data-ttu-id="ad818-137">StorSimple benefits</span><span class="sxs-lookup"><span data-stu-id="ad818-137">StorSimple benefits</span></span>

<span data-ttu-id="ad818-138">StorSimple provides an on-premises solution that is seamlessly integrated with Microsoft Azure, by taking advantage of seamless access to on-premises and cloud storage.</span><span class="sxs-lookup"><span data-stu-id="ad818-138">StorSimple provides an on-premises solution that is seamlessly integrated with Microsoft Azure, by taking advantage of seamless access to on-premises and cloud storage.</span></span>

<span data-ttu-id="ad818-139">StorSimple uses automatic tiering between the on-premises device, which has solid-state device (SSD) and serial-attached SCSI (SAS) storage, and Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ad818-139">StorSimple uses automatic tiering between the on-premises device, which has solid-state device (SSD) and serial-attached SCSI (SAS) storage, and Azure Storage.</span></span> <span data-ttu-id="ad818-140">Automatic tiering keeps frequently accessed data local, on the SSD and SAS tiers.</span><span class="sxs-lookup"><span data-stu-id="ad818-140">Automatic tiering keeps frequently accessed data local, on the SSD and SAS tiers.</span></span> <span data-ttu-id="ad818-141">It moves infrequently accessed data to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ad818-141">It moves infrequently accessed data to Azure Storage.</span></span>

<span data-ttu-id="ad818-142">StorSimple offers these benefits:</span><span class="sxs-lookup"><span data-stu-id="ad818-142">StorSimple offers these benefits:</span></span>

-   <span data-ttu-id="ad818-143">Unique deduplication and compression algorithms that use the cloud to achieve unprecedented deduplication levels</span><span class="sxs-lookup"><span data-stu-id="ad818-143">Unique deduplication and compression algorithms that use the cloud to achieve unprecedented deduplication levels</span></span>
-   <span data-ttu-id="ad818-144">High availability</span><span class="sxs-lookup"><span data-stu-id="ad818-144">High availability</span></span>
-   <span data-ttu-id="ad818-145">Geo-replication by using Azure geo-replication</span><span class="sxs-lookup"><span data-stu-id="ad818-145">Geo-replication by using Azure geo-replication</span></span>
-   <span data-ttu-id="ad818-146">Azure integration</span><span class="sxs-lookup"><span data-stu-id="ad818-146">Azure integration</span></span>
-   <span data-ttu-id="ad818-147">Data encryption in the cloud</span><span class="sxs-lookup"><span data-stu-id="ad818-147">Data encryption in the cloud</span></span>
-   <span data-ttu-id="ad818-148">Improved disaster recovery and compliance</span><span class="sxs-lookup"><span data-stu-id="ad818-148">Improved disaster recovery and compliance</span></span>

<span data-ttu-id="ad818-149">Although StorSimple presents two main deployment scenarios (primary backup target and secondary backup target), fundamentally, it's a plain, block storage device.</span><span class="sxs-lookup"><span data-stu-id="ad818-149">Although StorSimple presents two main deployment scenarios (primary backup target and secondary backup target), fundamentally, it's a plain, block storage device.</span></span> <span data-ttu-id="ad818-150">StorSimple does all the compression and deduplication.</span><span class="sxs-lookup"><span data-stu-id="ad818-150">StorSimple does all the compression and deduplication.</span></span> <span data-ttu-id="ad818-151">It seamlessly sends and retrieves data between the cloud and the application and file system.</span><span class="sxs-lookup"><span data-stu-id="ad818-151">It seamlessly sends and retrieves data between the cloud and the application and file system.</span></span>

<span data-ttu-id="ad818-152">For more information about StorSimple, see [StorSimple 8000 series: Hybrid cloud storage solution](storsimple-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ad818-152">For more information about StorSimple, see [StorSimple 8000 series: Hybrid cloud storage solution](storsimple-overview.md).</span></span> <span data-ttu-id="ad818-153">Also, you can review the [technical StorSimple 8000 series specifications](storsimple-technical-specifications-and-compliance.md).</span><span class="sxs-lookup"><span data-stu-id="ad818-153">Also, you can review the [technical StorSimple 8000 series specifications](storsimple-technical-specifications-and-compliance.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad818-154">Using a StorSimple device as a backup target is supported only for StorSimple 8000 Update 3 and later versions.</span><span class="sxs-lookup"><span data-stu-id="ad818-154">Using a StorSimple device as a backup target is supported only for StorSimple 8000 Update 3 and later versions.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="ad818-155">Architecture overview</span><span class="sxs-lookup"><span data-stu-id="ad818-155">Architecture overview</span></span>

<span data-ttu-id="ad818-156">The following tables show the device model-to-architecture initial guidance.</span><span class="sxs-lookup"><span data-stu-id="ad818-156">The following tables show the device model-to-architecture initial guidance.</span></span>

<span data-ttu-id="ad818-157">**StorSimple capacities for local and cloud storage**</span><span class="sxs-lookup"><span data-stu-id="ad818-157">**StorSimple capacities for local and cloud storage**</span></span>

| <span data-ttu-id="ad818-158">Storage capacity</span><span class="sxs-lookup"><span data-stu-id="ad818-158">Storage capacity</span></span> | <span data-ttu-id="ad818-159">8100</span><span class="sxs-lookup"><span data-stu-id="ad818-159">8100</span></span> | <span data-ttu-id="ad818-160">8600</span><span class="sxs-lookup"><span data-stu-id="ad818-160">8600</span></span> |
|---|---|---|
| <span data-ttu-id="ad818-161">Local storage capacity</span><span class="sxs-lookup"><span data-stu-id="ad818-161">Local storage capacity</span></span> | <span data-ttu-id="ad818-162">&lt; 10 TiB\*</span><span class="sxs-lookup"><span data-stu-id="ad818-162">&lt; 10 TiB\*</span></span>  | <span data-ttu-id="ad818-163">&lt; 20 TiB\*</span><span class="sxs-lookup"><span data-stu-id="ad818-163">&lt; 20 TiB\*</span></span>  |
| <span data-ttu-id="ad818-164">Cloud storage capacity</span><span class="sxs-lookup"><span data-stu-id="ad818-164">Cloud storage capacity</span></span> | <span data-ttu-id="ad818-165">&gt; 200 TiB\*</span><span class="sxs-lookup"><span data-stu-id="ad818-165">&gt; 200 TiB\*</span></span> | <span data-ttu-id="ad818-166">&gt; 500 TiB\*</span><span class="sxs-lookup"><span data-stu-id="ad818-166">&gt; 500 TiB\*</span></span> |

<span data-ttu-id="ad818-167">\* Storage size assumes no deduplication or compression.</span><span class="sxs-lookup"><span data-stu-id="ad818-167">\* Storage size assumes no deduplication or compression.</span></span>

<span data-ttu-id="ad818-168">**StorSimple capacities for primary and secondary backups**</span><span class="sxs-lookup"><span data-stu-id="ad818-168">**StorSimple capacities for primary and secondary backups**</span></span>

| <span data-ttu-id="ad818-169">Backup scenario</span><span class="sxs-lookup"><span data-stu-id="ad818-169">Backup scenario</span></span>  | <span data-ttu-id="ad818-170">Local storage capacity</span><span class="sxs-lookup"><span data-stu-id="ad818-170">Local storage capacity</span></span>  | <span data-ttu-id="ad818-171">Cloud storage capacity</span><span class="sxs-lookup"><span data-stu-id="ad818-171">Cloud storage capacity</span></span>  |
|---|---|---|
| <span data-ttu-id="ad818-172">Primary backup</span><span class="sxs-lookup"><span data-stu-id="ad818-172">Primary backup</span></span>  | <span data-ttu-id="ad818-173">Recent backups stored on local storage for fast recovery to meet recovery point objective (RPO)</span><span class="sxs-lookup"><span data-stu-id="ad818-173">Recent backups stored on local storage for fast recovery to meet recovery point objective (RPO)</span></span> | <span data-ttu-id="ad818-174">Backup history (RPO) fits in cloud capacity</span><span class="sxs-lookup"><span data-stu-id="ad818-174">Backup history (RPO) fits in cloud capacity</span></span> |
| <span data-ttu-id="ad818-175">Secondary backup</span><span class="sxs-lookup"><span data-stu-id="ad818-175">Secondary backup</span></span> | <span data-ttu-id="ad818-176">Secondary copy of backup data can be stored in cloud capacity</span><span class="sxs-lookup"><span data-stu-id="ad818-176">Secondary copy of backup data can be stored in cloud capacity</span></span>  | <span data-ttu-id="ad818-177">N/A</span><span class="sxs-lookup"><span data-stu-id="ad818-177">N/A</span></span>  |

## <a name="storsimple-as-a-primary-backup-target"></a><span data-ttu-id="ad818-178">StorSimple as a primary backup target</span><span class="sxs-lookup"><span data-stu-id="ad818-178">StorSimple as a primary backup target</span></span>

<span data-ttu-id="ad818-179">In this scenario, StorSimple volumes are presented to the backup application as the sole repository for backups.</span><span class="sxs-lookup"><span data-stu-id="ad818-179">In this scenario, StorSimple volumes are presented to the backup application as the sole repository for backups.</span></span> <span data-ttu-id="ad818-180">The following figure shows a solution architecture in which all backups use StorSimple tiered volumes for backups and restores.</span><span class="sxs-lookup"><span data-stu-id="ad818-180">The following figure shows a solution architecture in which all backups use StorSimple tiered volumes for backups and restores.</span></span>

![StorSimple as a primary backup target logical diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a><span data-ttu-id="ad818-182">Primary target backup logical steps</span><span class="sxs-lookup"><span data-stu-id="ad818-182">Primary target backup logical steps</span></span>

1.  <span data-ttu-id="ad818-183">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span><span class="sxs-lookup"><span data-stu-id="ad818-183">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span></span>
2.  <span data-ttu-id="ad818-184">The backup server writes data to the StorSimple tiered volumes.</span><span class="sxs-lookup"><span data-stu-id="ad818-184">The backup server writes data to the StorSimple tiered volumes.</span></span>
3.  <span data-ttu-id="ad818-185">The backup server updates the catalog database, and then finishes the backup job.</span><span class="sxs-lookup"><span data-stu-id="ad818-185">The backup server updates the catalog database, and then finishes the backup job.</span></span>
4.  <span data-ttu-id="ad818-186">A snapshot script triggers the StorSimple cloud snapshot manager (start or delete).</span><span class="sxs-lookup"><span data-stu-id="ad818-186">A snapshot script triggers the StorSimple cloud snapshot manager (start or delete).</span></span>
5.  <span data-ttu-id="ad818-187">The backup server deletes expired backups based on a retention policy.</span><span class="sxs-lookup"><span data-stu-id="ad818-187">The backup server deletes expired backups based on a retention policy.</span></span>

### <a name="primary-target-restore-logical-steps"></a><span data-ttu-id="ad818-188">Primary target restore logical steps</span><span class="sxs-lookup"><span data-stu-id="ad818-188">Primary target restore logical steps</span></span>

1.  <span data-ttu-id="ad818-189">The backup server starts restoring the appropriate data from the storage repository.</span><span class="sxs-lookup"><span data-stu-id="ad818-189">The backup server starts restoring the appropriate data from the storage repository.</span></span>
2.  <span data-ttu-id="ad818-190">The backup agent receives the data from the backup server.</span><span class="sxs-lookup"><span data-stu-id="ad818-190">The backup agent receives the data from the backup server.</span></span>
3.  <span data-ttu-id="ad818-191">The backup server finishes the restore job.</span><span class="sxs-lookup"><span data-stu-id="ad818-191">The backup server finishes the restore job.</span></span>

## <a name="storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="ad818-192">StorSimple as a secondary backup target</span><span class="sxs-lookup"><span data-stu-id="ad818-192">StorSimple as a secondary backup target</span></span>

<span data-ttu-id="ad818-193">In this scenario, StorSimple volumes primarily are used for long-term retention or archiving.</span><span class="sxs-lookup"><span data-stu-id="ad818-193">In this scenario, StorSimple volumes primarily are used for long-term retention or archiving.</span></span>

<span data-ttu-id="ad818-194">The following figure shows an architecture in which initial backups and restores target a high-performance volume.</span><span class="sxs-lookup"><span data-stu-id="ad818-194">The following figure shows an architecture in which initial backups and restores target a high-performance volume.</span></span> <span data-ttu-id="ad818-195">These backups are copied and archived to a StorSimple tiered volume on a set schedule.</span><span class="sxs-lookup"><span data-stu-id="ad818-195">These backups are copied and archived to a StorSimple tiered volume on a set schedule.</span></span>

<span data-ttu-id="ad818-196">It is important to size your high-performance volume so that it can handle your retention policy capacity and performance requirements.</span><span class="sxs-lookup"><span data-stu-id="ad818-196">It is important to size your high-performance volume so that it can handle your retention policy capacity and performance requirements.</span></span>

![StorSimple as a secondary backup target logical diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a><span data-ttu-id="ad818-198">Secondary target backup logical steps</span><span class="sxs-lookup"><span data-stu-id="ad818-198">Secondary target backup logical steps</span></span>

1.  <span data-ttu-id="ad818-199">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span><span class="sxs-lookup"><span data-stu-id="ad818-199">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span></span>
2.  <span data-ttu-id="ad818-200">The backup server writes data to high-performance storage.</span><span class="sxs-lookup"><span data-stu-id="ad818-200">The backup server writes data to high-performance storage.</span></span>
3.  <span data-ttu-id="ad818-201">The backup server updates the catalog database, and then finishes the backup job.</span><span class="sxs-lookup"><span data-stu-id="ad818-201">The backup server updates the catalog database, and then finishes the backup job.</span></span>
4.  <span data-ttu-id="ad818-202">The backup server copies backups to StorSimple based on a retention policy.</span><span class="sxs-lookup"><span data-stu-id="ad818-202">The backup server copies backups to StorSimple based on a retention policy.</span></span>
5.  <span data-ttu-id="ad818-203">A snapshot script triggers the StorSimple cloud snapshot manager (start or delete).</span><span class="sxs-lookup"><span data-stu-id="ad818-203">A snapshot script triggers the StorSimple cloud snapshot manager (start or delete).</span></span>
6.  <span data-ttu-id="ad818-204">The backup server deletes expired backups based on a retention policy.</span><span class="sxs-lookup"><span data-stu-id="ad818-204">The backup server deletes expired backups based on a retention policy.</span></span>

### <a name="secondary-target-restore-logical-steps"></a><span data-ttu-id="ad818-205">Secondary target restore logical steps</span><span class="sxs-lookup"><span data-stu-id="ad818-205">Secondary target restore logical steps</span></span>

1.  <span data-ttu-id="ad818-206">The backup server starts restoring the appropriate data from the storage repository.</span><span class="sxs-lookup"><span data-stu-id="ad818-206">The backup server starts restoring the appropriate data from the storage repository.</span></span>
2.  <span data-ttu-id="ad818-207">The backup agent receives the data from the backup server.</span><span class="sxs-lookup"><span data-stu-id="ad818-207">The backup agent receives the data from the backup server.</span></span>
3.  <span data-ttu-id="ad818-208">The backup server finishes the restore job.</span><span class="sxs-lookup"><span data-stu-id="ad818-208">The backup server finishes the restore job.</span></span>

## <a name="deploy-the-solution"></a><span data-ttu-id="ad818-209">Deploy the solution</span><span class="sxs-lookup"><span data-stu-id="ad818-209">Deploy the solution</span></span>

<span data-ttu-id="ad818-210">Deploying the solution requires three steps:</span><span class="sxs-lookup"><span data-stu-id="ad818-210">Deploying the solution requires three steps:</span></span>

1. <span data-ttu-id="ad818-211">Prepare the network infrastructure.</span><span class="sxs-lookup"><span data-stu-id="ad818-211">Prepare the network infrastructure.</span></span>
2. <span data-ttu-id="ad818-212">Deploy your StorSimple device as a backup target.</span><span class="sxs-lookup"><span data-stu-id="ad818-212">Deploy your StorSimple device as a backup target.</span></span>
3. <span data-ttu-id="ad818-213">Deploy Veeam.</span><span class="sxs-lookup"><span data-stu-id="ad818-213">Deploy Veeam.</span></span>

<span data-ttu-id="ad818-214">Each step is discussed in detail in the following sections.</span><span class="sxs-lookup"><span data-stu-id="ad818-214">Each step is discussed in detail in the following sections.</span></span>

### <a name="set-up-the-network"></a><span data-ttu-id="ad818-215">Set up the network</span><span class="sxs-lookup"><span data-stu-id="ad818-215">Set up the network</span></span>

<span data-ttu-id="ad818-216">Because StorSimple is a solution that is integrated with the Azure cloud, StorSimple requires an active and working connection to the Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="ad818-216">Because StorSimple is a solution that is integrated with the Azure cloud, StorSimple requires an active and working connection to the Azure cloud.</span></span> <span data-ttu-id="ad818-217">This connection is used for operations like cloud snapshots, data management, and metadata transfer, and to tier older, less accessed data to Azure cloud storage.</span><span class="sxs-lookup"><span data-stu-id="ad818-217">This connection is used for operations like cloud snapshots, data management, and metadata transfer, and to tier older, less accessed data to Azure cloud storage.</span></span>

<span data-ttu-id="ad818-218">For the solution to perform optimally, we recommend that you follow these networking best practices:</span><span class="sxs-lookup"><span data-stu-id="ad818-218">For the solution to perform optimally, we recommend that you follow these networking best practices:</span></span>

-   <span data-ttu-id="ad818-219">The link that connects your StorSimple tiering to Azure must meet your bandwidth requirements.</span><span class="sxs-lookup"><span data-stu-id="ad818-219">The link that connects your StorSimple tiering to Azure must meet your bandwidth requirements.</span></span> <span data-ttu-id="ad818-220">Achieve this by applying the necessary Quality of Service (QoS) level to your infrastructure switches to match your RPO and recovery time objective (RTO) SLAs.</span><span class="sxs-lookup"><span data-stu-id="ad818-220">Achieve this by applying the necessary Quality of Service (QoS) level to your infrastructure switches to match your RPO and recovery time objective (RTO) SLAs.</span></span>
-   <span data-ttu-id="ad818-221">Maximum Azure Blob storage access latencies should be around 80 ms.</span><span class="sxs-lookup"><span data-stu-id="ad818-221">Maximum Azure Blob storage access latencies should be around 80 ms.</span></span>

### <a name="deploy-storsimple"></a><span data-ttu-id="ad818-222">Deploy StorSimple</span><span class="sxs-lookup"><span data-stu-id="ad818-222">Deploy StorSimple</span></span>

<span data-ttu-id="ad818-223">For step-by-step StorSimple deployment guidance, see [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span><span class="sxs-lookup"><span data-stu-id="ad818-223">For step-by-step StorSimple deployment guidance, see [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span></span>

### <a name="deploy-veeam"></a><span data-ttu-id="ad818-224">Deploy Veeam</span><span class="sxs-lookup"><span data-stu-id="ad818-224">Deploy Veeam</span></span>

<span data-ttu-id="ad818-225">For Veeam installation best practices, see [Veeam Backup & Replication Best Practices](https://bp.veeam.expert/), and read the user guide at [Veeam Help Center (Technical Documentation)](https://www.veeam.com/documentation-guides-datasheets.html).</span><span class="sxs-lookup"><span data-stu-id="ad818-225">For Veeam installation best practices, see [Veeam Backup & Replication Best Practices](https://bp.veeam.expert/), and read the user guide at [Veeam Help Center (Technical Documentation)](https://www.veeam.com/documentation-guides-datasheets.html).</span></span>

## <a name="set-up-the-solution"></a><span data-ttu-id="ad818-226">Set up the solution</span><span class="sxs-lookup"><span data-stu-id="ad818-226">Set up the solution</span></span>

<span data-ttu-id="ad818-227">In this section, we demonstrate some configuration examples.</span><span class="sxs-lookup"><span data-stu-id="ad818-227">In this section, we demonstrate some configuration examples.</span></span> <span data-ttu-id="ad818-228">The following examples and recommendations illustrate the most basic and fundamental implementation.</span><span class="sxs-lookup"><span data-stu-id="ad818-228">The following examples and recommendations illustrate the most basic and fundamental implementation.</span></span> <span data-ttu-id="ad818-229">This implementation might not apply directly to your specific backup requirements.</span><span class="sxs-lookup"><span data-stu-id="ad818-229">This implementation might not apply directly to your specific backup requirements.</span></span>

### <a name="set-up-storsimple"></a><span data-ttu-id="ad818-230">Set up StorSimple</span><span class="sxs-lookup"><span data-stu-id="ad818-230">Set up StorSimple</span></span>

| <span data-ttu-id="ad818-231">StorSimple deployment tasks</span><span class="sxs-lookup"><span data-stu-id="ad818-231">StorSimple deployment tasks</span></span>  | <span data-ttu-id="ad818-232">Additional comments</span><span class="sxs-lookup"><span data-stu-id="ad818-232">Additional comments</span></span> |
|---|---|
| <span data-ttu-id="ad818-233">Deploy your on-premises StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="ad818-233">Deploy your on-premises StorSimple device.</span></span> | <span data-ttu-id="ad818-234">Supported versions: Update 3 and later versions.</span><span class="sxs-lookup"><span data-stu-id="ad818-234">Supported versions: Update 3 and later versions.</span></span> |
| <span data-ttu-id="ad818-235">Turn on the backup target.</span><span class="sxs-lookup"><span data-stu-id="ad818-235">Turn on the backup target.</span></span> | <span data-ttu-id="ad818-236">Use these commands to turn on or turn off backup target mode, and to get status.</span><span class="sxs-lookup"><span data-stu-id="ad818-236">Use these commands to turn on or turn off backup target mode, and to get status.</span></span> <span data-ttu-id="ad818-237">For more information, see [Connect remotely to a StorSimple device](storsimple-remote-connect.md).</span><span class="sxs-lookup"><span data-stu-id="ad818-237">For more information, see [Connect remotely to a StorSimple device](storsimple-remote-connect.md).</span></span></br> <span data-ttu-id="ad818-238">To turn on backup mode: `Set-HCSBackupApplianceMode -enable`.</span><span class="sxs-lookup"><span data-stu-id="ad818-238">To turn on backup mode: `Set-HCSBackupApplianceMode -enable`.</span></span> </br> <span data-ttu-id="ad818-239">To turn off backup mode: `Set-HCSBackupApplianceMode -disable`.</span><span class="sxs-lookup"><span data-stu-id="ad818-239">To turn off backup mode: `Set-HCSBackupApplianceMode -disable`.</span></span> </br> <span data-ttu-id="ad818-240">To get the current state of backup mode settings: `Get-HCSBackupApplianceMode`.</span><span class="sxs-lookup"><span data-stu-id="ad818-240">To get the current state of backup mode settings: `Get-HCSBackupApplianceMode`.</span></span> |
| <span data-ttu-id="ad818-241">Create a common volume container for your volume that stores the backup data.</span><span class="sxs-lookup"><span data-stu-id="ad818-241">Create a common volume container for your volume that stores the backup data.</span></span> <span data-ttu-id="ad818-242">All data in a volume container is deduplicated.</span><span class="sxs-lookup"><span data-stu-id="ad818-242">All data in a volume container is deduplicated.</span></span> | <span data-ttu-id="ad818-243">StorSimple volume containers define deduplication domains.</span><span class="sxs-lookup"><span data-stu-id="ad818-243">StorSimple volume containers define deduplication domains.</span></span>  |
| <span data-ttu-id="ad818-244">Create StorSimple volumes.</span><span class="sxs-lookup"><span data-stu-id="ad818-244">Create StorSimple volumes.</span></span> | <span data-ttu-id="ad818-245">Create volumes with sizes as close to the anticipated usage as possible, because volume size affects cloud snapshot duration time.</span><span class="sxs-lookup"><span data-stu-id="ad818-245">Create volumes with sizes as close to the anticipated usage as possible, because volume size affects cloud snapshot duration time.</span></span> <span data-ttu-id="ad818-246">For information about how to size a volume, read about [retention policies](#retention-policies).</span><span class="sxs-lookup"><span data-stu-id="ad818-246">For information about how to size a volume, read about [retention policies](#retention-policies).</span></span></br> </br> <span data-ttu-id="ad818-247">Use StorSimple tiered volumes, and select the **Use this volume for less frequently accessed archival data** check box.</span><span class="sxs-lookup"><span data-stu-id="ad818-247">Use StorSimple tiered volumes, and select the **Use this volume for less frequently accessed archival data** check box.</span></span> </br> <span data-ttu-id="ad818-248">Using only locally pinned volumes is not supported.</span><span class="sxs-lookup"><span data-stu-id="ad818-248">Using only locally pinned volumes is not supported.</span></span> |
| <span data-ttu-id="ad818-249">Create a unique StorSimple backup policy for all the backup target volumes.</span><span class="sxs-lookup"><span data-stu-id="ad818-249">Create a unique StorSimple backup policy for all the backup target volumes.</span></span> | <span data-ttu-id="ad818-250">A StorSimple backup policy defines the volume consistency group.</span><span class="sxs-lookup"><span data-stu-id="ad818-250">A StorSimple backup policy defines the volume consistency group.</span></span> |
| <span data-ttu-id="ad818-251">Disable the schedule as the snapshots expire.</span><span class="sxs-lookup"><span data-stu-id="ad818-251">Disable the schedule as the snapshots expire.</span></span> | <span data-ttu-id="ad818-252">Snapshots are triggered as a post-processing operation.</span><span class="sxs-lookup"><span data-stu-id="ad818-252">Snapshots are triggered as a post-processing operation.</span></span> |

### <a name="set-up-the-host-backup-server-storage"></a><span data-ttu-id="ad818-253">Set up the host backup server storage</span><span class="sxs-lookup"><span data-stu-id="ad818-253">Set up the host backup server storage</span></span>

<span data-ttu-id="ad818-254">Set up the host backup server storage according to these guidelines:</span><span class="sxs-lookup"><span data-stu-id="ad818-254">Set up the host backup server storage according to these guidelines:</span></span>  

- <span data-ttu-id="ad818-255">Don't use spanned volumes (created by Windows Disk Management).</span><span class="sxs-lookup"><span data-stu-id="ad818-255">Don't use spanned volumes (created by Windows Disk Management).</span></span> <span data-ttu-id="ad818-256">Spanned volumes are not supported.</span><span class="sxs-lookup"><span data-stu-id="ad818-256">Spanned volumes are not supported.</span></span>
- <span data-ttu-id="ad818-257">Format your volumes using NTFS with 64-KB allocation unit size.</span><span class="sxs-lookup"><span data-stu-id="ad818-257">Format your volumes using NTFS with 64-KB allocation unit size.</span></span>
- <span data-ttu-id="ad818-258">Map the StorSimple volumes directly to the Veeam server.</span><span class="sxs-lookup"><span data-stu-id="ad818-258">Map the StorSimple volumes directly to the Veeam server.</span></span>
    - <span data-ttu-id="ad818-259">Use iSCSI for physical servers.</span><span class="sxs-lookup"><span data-stu-id="ad818-259">Use iSCSI for physical servers.</span></span>


## <a name="best-practices-for-storsimple-and-veeam"></a><span data-ttu-id="ad818-260">Best practices for StorSimple and Veeam</span><span class="sxs-lookup"><span data-stu-id="ad818-260">Best practices for StorSimple and Veeam</span></span>

<span data-ttu-id="ad818-261">Set up your solution according to the guidelines in the following few sections.</span><span class="sxs-lookup"><span data-stu-id="ad818-261">Set up your solution according to the guidelines in the following few sections.</span></span>

### <a name="operating-system-best-practices"></a><span data-ttu-id="ad818-262">Operating system best practices</span><span class="sxs-lookup"><span data-stu-id="ad818-262">Operating system best practices</span></span>

-   <span data-ttu-id="ad818-263">Disable Windows Server encryption and deduplication for the NTFS file system.</span><span class="sxs-lookup"><span data-stu-id="ad818-263">Disable Windows Server encryption and deduplication for the NTFS file system.</span></span>
-   <span data-ttu-id="ad818-264">Disable Windows Server defragmentation on the StorSimple volumes.</span><span class="sxs-lookup"><span data-stu-id="ad818-264">Disable Windows Server defragmentation on the StorSimple volumes.</span></span>
-   <span data-ttu-id="ad818-265">Disable Windows Server indexing on the StorSimple volumes.</span><span class="sxs-lookup"><span data-stu-id="ad818-265">Disable Windows Server indexing on the StorSimple volumes.</span></span>
-   <span data-ttu-id="ad818-266">Run an antivirus scan at the source host (not against the StorSimple volumes).</span><span class="sxs-lookup"><span data-stu-id="ad818-266">Run an antivirus scan at the source host (not against the StorSimple volumes).</span></span>
-   <span data-ttu-id="ad818-267">Turn off the default [Windows Server maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) in Task Manager.</span><span class="sxs-lookup"><span data-stu-id="ad818-267">Turn off the default [Windows Server maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) in Task Manager.</span></span> <span data-ttu-id="ad818-268">Do this in one of the following ways:</span><span class="sxs-lookup"><span data-stu-id="ad818-268">Do this in one of the following ways:</span></span>
    - <span data-ttu-id="ad818-269">Turn off the Maintenance configurator in Windows Task Scheduler.</span><span class="sxs-lookup"><span data-stu-id="ad818-269">Turn off the Maintenance configurator in Windows Task Scheduler.</span></span>
    - <span data-ttu-id="ad818-270">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) from Windows Sysinternals.</span><span class="sxs-lookup"><span data-stu-id="ad818-270">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) from Windows Sysinternals.</span></span> <span data-ttu-id="ad818-271">After you download PsExec, run Windows PowerShell as an administrator, and type:</span><span class="sxs-lookup"><span data-stu-id="ad818-271">After you download PsExec, run Windows PowerShell as an administrator, and type:</span></span>
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a><span data-ttu-id="ad818-272">StorSimple best practices</span><span class="sxs-lookup"><span data-stu-id="ad818-272">StorSimple best practices</span></span>

-   <span data-ttu-id="ad818-273">Be sure that the StorSimple device is updated to [Update 3 or later](storsimple-install-update-3.md).</span><span class="sxs-lookup"><span data-stu-id="ad818-273">Be sure that the StorSimple device is updated to [Update 3 or later](storsimple-install-update-3.md).</span></span>
-   <span data-ttu-id="ad818-274">Isolate iSCSI and cloud traffic.</span><span class="sxs-lookup"><span data-stu-id="ad818-274">Isolate iSCSI and cloud traffic.</span></span> <span data-ttu-id="ad818-275">Use dedicated iSCSI connections for traffic between StorSimple and the backup server.</span><span class="sxs-lookup"><span data-stu-id="ad818-275">Use dedicated iSCSI connections for traffic between StorSimple and the backup server.</span></span>
-   <span data-ttu-id="ad818-276">Be sure that your StorSimple device is a dedicated backup target.</span><span class="sxs-lookup"><span data-stu-id="ad818-276">Be sure that your StorSimple device is a dedicated backup target.</span></span> <span data-ttu-id="ad818-277">Mixed workloads are not supported because they affect your RTO and RPO.</span><span class="sxs-lookup"><span data-stu-id="ad818-277">Mixed workloads are not supported because they affect your RTO and RPO.</span></span>

### <a name="veeam-best-practices"></a><span data-ttu-id="ad818-278">Veeam best practices</span><span class="sxs-lookup"><span data-stu-id="ad818-278">Veeam best practices</span></span>

-   <span data-ttu-id="ad818-279">The Veeam database should be local to the server and not reside on a StorSimple volume.</span><span class="sxs-lookup"><span data-stu-id="ad818-279">The Veeam database should be local to the server and not reside on a StorSimple volume.</span></span>
-   <span data-ttu-id="ad818-280">For disaster recovery, back up the Veeam database on a StorSimple volume.</span><span class="sxs-lookup"><span data-stu-id="ad818-280">For disaster recovery, back up the Veeam database on a StorSimple volume.</span></span>
-   <span data-ttu-id="ad818-281">We support Veeam full and incremental backups for this solution.</span><span class="sxs-lookup"><span data-stu-id="ad818-281">We support Veeam full and incremental backups for this solution.</span></span> <span data-ttu-id="ad818-282">We recommend that you do not use synthetic and differential backups.</span><span class="sxs-lookup"><span data-stu-id="ad818-282">We recommend that you do not use synthetic and differential backups.</span></span>
-   <span data-ttu-id="ad818-283">Backup data files should contain only the data for a specific job.</span><span class="sxs-lookup"><span data-stu-id="ad818-283">Backup data files should contain only the data for a specific job.</span></span> <span data-ttu-id="ad818-284">For example, no media appends across different jobs are allowed.</span><span class="sxs-lookup"><span data-stu-id="ad818-284">For example, no media appends across different jobs are allowed.</span></span>
-   <span data-ttu-id="ad818-285">Turn off job verification.</span><span class="sxs-lookup"><span data-stu-id="ad818-285">Turn off job verification.</span></span> <span data-ttu-id="ad818-286">If necessary, verification should be scheduled after the latest backup job.</span><span class="sxs-lookup"><span data-stu-id="ad818-286">If necessary, verification should be scheduled after the latest backup job.</span></span> <span data-ttu-id="ad818-287">It is important to understand that this job affects your backup window.</span><span class="sxs-lookup"><span data-stu-id="ad818-287">It is important to understand that this job affects your backup window.</span></span>
-   <span data-ttu-id="ad818-288">Turn on media pre-allocation.</span><span class="sxs-lookup"><span data-stu-id="ad818-288">Turn on media pre-allocation.</span></span>
-   <span data-ttu-id="ad818-289">Be sure parallel processing is turned on.</span><span class="sxs-lookup"><span data-stu-id="ad818-289">Be sure parallel processing is turned on.</span></span>
-   <span data-ttu-id="ad818-290">Turn off compression.</span><span class="sxs-lookup"><span data-stu-id="ad818-290">Turn off compression.</span></span>
-   <span data-ttu-id="ad818-291">Turn off deduplication on the backup job.</span><span class="sxs-lookup"><span data-stu-id="ad818-291">Turn off deduplication on the backup job.</span></span>
-   <span data-ttu-id="ad818-292">Set optimization to **LAN Target**.</span><span class="sxs-lookup"><span data-stu-id="ad818-292">Set optimization to **LAN Target**.</span></span>
-   <span data-ttu-id="ad818-293">Turn on **Create active full backup** (every 2 weeks).</span><span class="sxs-lookup"><span data-stu-id="ad818-293">Turn on **Create active full backup** (every 2 weeks).</span></span>
-   <span data-ttu-id="ad818-294">On the backup repository, set up **Use per-VM backup files**.</span><span class="sxs-lookup"><span data-stu-id="ad818-294">On the backup repository, set up **Use per-VM backup files**.</span></span>
-   <span data-ttu-id="ad818-295">Set **Use multiple upload streams per job** to **8** (a maximum of 16 is allowed).</span><span class="sxs-lookup"><span data-stu-id="ad818-295">Set **Use multiple upload streams per job** to **8** (a maximum of 16 is allowed).</span></span> <span data-ttu-id="ad818-296">Adjust this number up or down based on CPU utilization on the StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="ad818-296">Adjust this number up or down based on CPU utilization on the StorSimple device.</span></span>

## <a name="retention-policies"></a><span data-ttu-id="ad818-297">Retention policies</span><span class="sxs-lookup"><span data-stu-id="ad818-297">Retention policies</span></span>

<span data-ttu-id="ad818-298">One of the most common backup retention policy types is a Grandfather, Father, and Son (GFS) policy.</span><span class="sxs-lookup"><span data-stu-id="ad818-298">One of the most common backup retention policy types is a Grandfather, Father, and Son (GFS) policy.</span></span> <span data-ttu-id="ad818-299">In a GFS policy, an incremental backup is performed daily and full backups are done weekly and monthly.</span><span class="sxs-lookup"><span data-stu-id="ad818-299">In a GFS policy, an incremental backup is performed daily and full backups are done weekly and monthly.</span></span> <span data-ttu-id="ad818-300">This policy results in six StorSimple tiered volumes: one volume contains the weekly, monthly, and yearly full backups; the other five volumes store daily incremental backups.</span><span class="sxs-lookup"><span data-stu-id="ad818-300">This policy results in six StorSimple tiered volumes: one volume contains the weekly, monthly, and yearly full backups; the other five volumes store daily incremental backups.</span></span>

<span data-ttu-id="ad818-301">In the following example, we use a GFS rotation.</span><span class="sxs-lookup"><span data-stu-id="ad818-301">In the following example, we use a GFS rotation.</span></span> <span data-ttu-id="ad818-302">The example assumes the following:</span><span class="sxs-lookup"><span data-stu-id="ad818-302">The example assumes the following:</span></span>

-   <span data-ttu-id="ad818-303">Non-deduped or compressed data is used.</span><span class="sxs-lookup"><span data-stu-id="ad818-303">Non-deduped or compressed data is used.</span></span>
-   <span data-ttu-id="ad818-304">Full backups are 1 TiB each.</span><span class="sxs-lookup"><span data-stu-id="ad818-304">Full backups are 1 TiB each.</span></span>
-   <span data-ttu-id="ad818-305">Daily incremental backups are 500 GiB each.</span><span class="sxs-lookup"><span data-stu-id="ad818-305">Daily incremental backups are 500 GiB each.</span></span>
-   <span data-ttu-id="ad818-306">Four weekly backups are kept for a month.</span><span class="sxs-lookup"><span data-stu-id="ad818-306">Four weekly backups are kept for a month.</span></span>
-   <span data-ttu-id="ad818-307">Twelve monthly backups are kept for a year.</span><span class="sxs-lookup"><span data-stu-id="ad818-307">Twelve monthly backups are kept for a year.</span></span>
-   <span data-ttu-id="ad818-308">One yearly backup is kept for 10 years.</span><span class="sxs-lookup"><span data-stu-id="ad818-308">One yearly backup is kept for 10 years.</span></span>

<span data-ttu-id="ad818-309">Based on the preceding assumptions, create a 26-TiB StorSimple tiered volume for the monthly and yearly full backups.</span><span class="sxs-lookup"><span data-stu-id="ad818-309">Based on the preceding assumptions, create a 26-TiB StorSimple tiered volume for the monthly and yearly full backups.</span></span> <span data-ttu-id="ad818-310">Create a 5-TiB StorSimple tiered volume for each of the incremental daily backups.</span><span class="sxs-lookup"><span data-stu-id="ad818-310">Create a 5-TiB StorSimple tiered volume for each of the incremental daily backups.</span></span>

| <span data-ttu-id="ad818-311">Backup type retention</span><span class="sxs-lookup"><span data-stu-id="ad818-311">Backup type retention</span></span> | <span data-ttu-id="ad818-312">Size (TiB)</span><span class="sxs-lookup"><span data-stu-id="ad818-312">Size (TiB)</span></span> | <span data-ttu-id="ad818-313">GFS multiplier\*</span><span class="sxs-lookup"><span data-stu-id="ad818-313">GFS multiplier\*</span></span> | <span data-ttu-id="ad818-314">Total capacity (TiB)</span><span class="sxs-lookup"><span data-stu-id="ad818-314">Total capacity (TiB)</span></span>  |
|---|---|---|---|
| <span data-ttu-id="ad818-315">Weekly full</span><span class="sxs-lookup"><span data-stu-id="ad818-315">Weekly full</span></span> | <span data-ttu-id="ad818-316">1</span><span class="sxs-lookup"><span data-stu-id="ad818-316">1</span></span> | <span data-ttu-id="ad818-317">4</span><span class="sxs-lookup"><span data-stu-id="ad818-317">4</span></span>  | <span data-ttu-id="ad818-318">4</span><span class="sxs-lookup"><span data-stu-id="ad818-318">4</span></span> |
| <span data-ttu-id="ad818-319">Daily incremental</span><span class="sxs-lookup"><span data-stu-id="ad818-319">Daily incremental</span></span> | <span data-ttu-id="ad818-320">0.5</span><span class="sxs-lookup"><span data-stu-id="ad818-320">0.5</span></span> | <span data-ttu-id="ad818-321">20 (cycles equal number of weeks per month)</span><span class="sxs-lookup"><span data-stu-id="ad818-321">20 (cycles equal number of weeks per month)</span></span> | <span data-ttu-id="ad818-322">12 (2 for additional quota)</span><span class="sxs-lookup"><span data-stu-id="ad818-322">12 (2 for additional quota)</span></span> |
| <span data-ttu-id="ad818-323">Monthly full</span><span class="sxs-lookup"><span data-stu-id="ad818-323">Monthly full</span></span> | <span data-ttu-id="ad818-324">1</span><span class="sxs-lookup"><span data-stu-id="ad818-324">1</span></span> | <span data-ttu-id="ad818-325">12</span><span class="sxs-lookup"><span data-stu-id="ad818-325">12</span></span> | <span data-ttu-id="ad818-326">12</span><span class="sxs-lookup"><span data-stu-id="ad818-326">12</span></span> |
| <span data-ttu-id="ad818-327">Yearly full</span><span class="sxs-lookup"><span data-stu-id="ad818-327">Yearly full</span></span> | <span data-ttu-id="ad818-328">1</span><span class="sxs-lookup"><span data-stu-id="ad818-328">1</span></span>  | <span data-ttu-id="ad818-329">10</span><span class="sxs-lookup"><span data-stu-id="ad818-329">10</span></span> | <span data-ttu-id="ad818-330">10</span><span class="sxs-lookup"><span data-stu-id="ad818-330">10</span></span> |
| <span data-ttu-id="ad818-331">GFS requirement</span><span class="sxs-lookup"><span data-stu-id="ad818-331">GFS requirement</span></span> |   | <span data-ttu-id="ad818-332">38</span><span class="sxs-lookup"><span data-stu-id="ad818-332">38</span></span> |   |
| <span data-ttu-id="ad818-333">Additional quota</span><span class="sxs-lookup"><span data-stu-id="ad818-333">Additional quota</span></span>  | <span data-ttu-id="ad818-334">4</span><span class="sxs-lookup"><span data-stu-id="ad818-334">4</span></span>  |   | <span data-ttu-id="ad818-335">42 total GFS requirement</span><span class="sxs-lookup"><span data-stu-id="ad818-335">42 total GFS requirement</span></span>  |
<span data-ttu-id="ad818-336">\* The GFS multiplier is the number of copies you need to protect and retain to meet your backup policy requirements.</span><span class="sxs-lookup"><span data-stu-id="ad818-336">\* The GFS multiplier is the number of copies you need to protect and retain to meet your backup policy requirements.</span></span>

## <a name="set-up-veeam-storage"></a><span data-ttu-id="ad818-337">Set up Veeam storage</span><span class="sxs-lookup"><span data-stu-id="ad818-337">Set up Veeam storage</span></span>

### <a name="to-set-up-veeam-storage"></a><span data-ttu-id="ad818-338">To set up Veeam storage</span><span class="sxs-lookup"><span data-stu-id="ad818-338">To set up Veeam storage</span></span>

1.  <span data-ttu-id="ad818-339">In the Veeam Backup and Replication console, in **Repository Tools**, go to **Backup Infrastructure**.</span><span class="sxs-lookup"><span data-stu-id="ad818-339">In the Veeam Backup and Replication console, in **Repository Tools**, go to **Backup Infrastructure**.</span></span> <span data-ttu-id="ad818-340">Right-click **Backup Repositories**, and then select **Add Backup Repository**.</span><span class="sxs-lookup"><span data-stu-id="ad818-340">Right-click **Backup Repositories**, and then select **Add Backup Repository**.</span></span>

    ![Veeam management console, backup repository page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage1.png)

2.  <span data-ttu-id="ad818-342">In the **New Backup Repository** dialog box, enter a name and description for the repository.</span><span class="sxs-lookup"><span data-stu-id="ad818-342">In the **New Backup Repository** dialog box, enter a name and description for the repository.</span></span> <span data-ttu-id="ad818-343">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="ad818-343">Select **Next**.</span></span>

    ![Veeam management console, name and description page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage2.png)

3.  <span data-ttu-id="ad818-345">For the type, select **Microsoft Windows server**.</span><span class="sxs-lookup"><span data-stu-id="ad818-345">For the type, select **Microsoft Windows server**.</span></span> <span data-ttu-id="ad818-346">Select the Veeam server.</span><span class="sxs-lookup"><span data-stu-id="ad818-346">Select the Veeam server.</span></span> <span data-ttu-id="ad818-347">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="ad818-347">Select **Next**.</span></span>

    ![Veeam management console, select type of backup repository](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage3.png)

4.  <span data-ttu-id="ad818-349">To specify **Location**, browse and select the volume.</span><span class="sxs-lookup"><span data-stu-id="ad818-349">To specify **Location**, browse and select the volume.</span></span> <span data-ttu-id="ad818-350">Select the **Limit maximum concurrent tasks to:** check box and set the value to **4**.</span><span class="sxs-lookup"><span data-stu-id="ad818-350">Select the **Limit maximum concurrent tasks to:** check box and set the value to **4**.</span></span> <span data-ttu-id="ad818-351">This ensures that only four virtual disks are being processed concurrently while each virtual machine (VM) is processed.</span><span class="sxs-lookup"><span data-stu-id="ad818-351">This ensures that only four virtual disks are being processed concurrently while each virtual machine (VM) is processed.</span></span> <span data-ttu-id="ad818-352">Select the **Advanced** button.</span><span class="sxs-lookup"><span data-stu-id="ad818-352">Select the **Advanced** button.</span></span>

    ![Veeam management console, select volume](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage4.png)


5.  <span data-ttu-id="ad818-354">In the **Storage Compatibility Settings** dialog box, select the **Use per-VM backup files** check box.</span><span class="sxs-lookup"><span data-stu-id="ad818-354">In the **Storage Compatibility Settings** dialog box, select the **Use per-VM backup files** check box.</span></span>

    ![Veeam management console, storage compatibility settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage5.png)

6.  <span data-ttu-id="ad818-356">In the **New Backup Repository** dialog box, select the **Enable vPower NFS service on the mount server (recommended)** check box.</span><span class="sxs-lookup"><span data-stu-id="ad818-356">In the **New Backup Repository** dialog box, select the **Enable vPower NFS service on the mount server (recommended)** check box.</span></span> <span data-ttu-id="ad818-357">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="ad818-357">Select **Next**.</span></span>

    ![Veeam management console, backup repository page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage6.png)

7.  <span data-ttu-id="ad818-359">Review the settings, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="ad818-359">Review the settings, and then select **Next**.</span></span>

    ![Veeam management console, backup repository page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage7.png)

    <span data-ttu-id="ad818-361">A repository is added to the Veeam server.</span><span class="sxs-lookup"><span data-stu-id="ad818-361">A repository is added to the Veeam server.</span></span>

## <a name="set-up-storsimple-as-a-primary-backup-target"></a><span data-ttu-id="ad818-362">Set up StorSimple as a primary backup target</span><span class="sxs-lookup"><span data-stu-id="ad818-362">Set up StorSimple as a primary backup target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad818-363">Data restore from a backup that has been tiered to the cloud occurs at cloud speeds.</span><span class="sxs-lookup"><span data-stu-id="ad818-363">Data restore from a backup that has been tiered to the cloud occurs at cloud speeds.</span></span>

<span data-ttu-id="ad818-364">The following figure shows the mapping of a typical volume to a backup job.</span><span class="sxs-lookup"><span data-stu-id="ad818-364">The following figure shows the mapping of a typical volume to a backup job.</span></span> <span data-ttu-id="ad818-365">In this case, all the weekly backups map to the Saturday full disk, and the incremental backups map to Monday-Friday incremental disks.</span><span class="sxs-lookup"><span data-stu-id="ad818-365">In this case, all the weekly backups map to the Saturday full disk, and the incremental backups map to Monday-Friday incremental disks.</span></span> <span data-ttu-id="ad818-366">All the backups and restores are from a StorSimple tiered volume.</span><span class="sxs-lookup"><span data-stu-id="ad818-366">All the backups and restores are from a StorSimple tiered volume.</span></span>

![Primary backup target configuration logical diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a><span data-ttu-id="ad818-368">StorSimple as a primary backup target GFS schedule example</span><span class="sxs-lookup"><span data-stu-id="ad818-368">StorSimple as a primary backup target GFS schedule example</span></span>

<span data-ttu-id="ad818-369">Here's an example of a GFS rotation schedule for four weeks, monthly, and yearly:</span><span class="sxs-lookup"><span data-stu-id="ad818-369">Here's an example of a GFS rotation schedule for four weeks, monthly, and yearly:</span></span>

| <span data-ttu-id="ad818-370">Frequency/backup type</span><span class="sxs-lookup"><span data-stu-id="ad818-370">Frequency/backup type</span></span> | <span data-ttu-id="ad818-371">Full</span><span class="sxs-lookup"><span data-stu-id="ad818-371">Full</span></span> | <span data-ttu-id="ad818-372">Incremental (days 1-5)</span><span class="sxs-lookup"><span data-stu-id="ad818-372">Incremental (days 1-5)</span></span>  |   
|---|---|---|
| <span data-ttu-id="ad818-373">Weekly (weeks 1-4)</span><span class="sxs-lookup"><span data-stu-id="ad818-373">Weekly (weeks 1-4)</span></span> | <span data-ttu-id="ad818-374">Saturday</span><span class="sxs-lookup"><span data-stu-id="ad818-374">Saturday</span></span> | <span data-ttu-id="ad818-375">Monday-Friday</span><span class="sxs-lookup"><span data-stu-id="ad818-375">Monday-Friday</span></span> |
| <span data-ttu-id="ad818-376">Monthly</span><span class="sxs-lookup"><span data-stu-id="ad818-376">Monthly</span></span>  | <span data-ttu-id="ad818-377">Saturday</span><span class="sxs-lookup"><span data-stu-id="ad818-377">Saturday</span></span>  |   |
| <span data-ttu-id="ad818-378">Yearly</span><span class="sxs-lookup"><span data-stu-id="ad818-378">Yearly</span></span> | <span data-ttu-id="ad818-379">Saturday</span><span class="sxs-lookup"><span data-stu-id="ad818-379">Saturday</span></span>  |   |   |


### <a name="assign-storsimple-volumes-to-a-veeam-backup-job"></a><span data-ttu-id="ad818-380">Assign StorSimple volumes to a Veeam backup job</span><span class="sxs-lookup"><span data-stu-id="ad818-380">Assign StorSimple volumes to a Veeam backup job</span></span>

<span data-ttu-id="ad818-381">For primary backup target scenario, create a daily job with your primary Veeam StorSimple volume.</span><span class="sxs-lookup"><span data-stu-id="ad818-381">For primary backup target scenario, create a daily job with your primary Veeam StorSimple volume.</span></span> <span data-ttu-id="ad818-382">For a secondary backup target scenario, create a daily job by using Direct Attached Storage (DAS), Network Attached Storage (NAS), or Just a Bunch of Disks (JBOD) storage.</span><span class="sxs-lookup"><span data-stu-id="ad818-382">For a secondary backup target scenario, create a daily job by using Direct Attached Storage (DAS), Network Attached Storage (NAS), or Just a Bunch of Disks (JBOD) storage.</span></span>

#### <a name="to-assign-storsimple-volumes-to-a-veeam-backup-job"></a><span data-ttu-id="ad818-383">To assign StorSimple volumes to a Veeam backup job</span><span class="sxs-lookup"><span data-stu-id="ad818-383">To assign StorSimple volumes to a Veeam backup job</span></span>

1.  <span data-ttu-id="ad818-384">In the Veeam Backup and Replication console, select **Backup & Replication**.</span><span class="sxs-lookup"><span data-stu-id="ad818-384">In the Veeam Backup and Replication console, select **Backup & Replication**.</span></span> <span data-ttu-id="ad818-385">Right-click **Backup**, and then select **VMware** or **Hyper-V**, depending on your environment.</span><span class="sxs-lookup"><span data-stu-id="ad818-385">Right-click **Backup**, and then select **VMware** or **Hyper-V**, depending on your environment.</span></span>

    ![Veeam management console, new backup job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage8.png)

2.  <span data-ttu-id="ad818-387">In the **New Backup Job** dialog box, enter a name and description for the daily backup job.</span><span class="sxs-lookup"><span data-stu-id="ad818-387">In the **New Backup Job** dialog box, enter a name and description for the daily backup job.</span></span>

    ![Veeam management console, new backup job page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage9.png)

3.  <span data-ttu-id="ad818-389">Select a virtual machine to back up to.</span><span class="sxs-lookup"><span data-stu-id="ad818-389">Select a virtual machine to back up to.</span></span>

    ![Veeam management console, new backup job page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage10.png)

4.  <span data-ttu-id="ad818-391">Select the values you want for **Backup proxy** and **Backup repository**.</span><span class="sxs-lookup"><span data-stu-id="ad818-391">Select the values you want for **Backup proxy** and **Backup repository**.</span></span> <span data-ttu-id="ad818-392">Select a value for **Restore points to keep on disk** according to the RPO and RTO definitions for your environment on locally attached storage.</span><span class="sxs-lookup"><span data-stu-id="ad818-392">Select a value for **Restore points to keep on disk** according to the RPO and RTO definitions for your environment on locally attached storage.</span></span> <span data-ttu-id="ad818-393">Select **Advanced**.</span><span class="sxs-lookup"><span data-stu-id="ad818-393">Select **Advanced**.</span></span>

    ![Veeam management console, new backup job page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage11.png)

5. <span data-ttu-id="ad818-395">In the **Advanced Settings** dialog box, on the **Backup** tab, select **Incremental**.</span><span class="sxs-lookup"><span data-stu-id="ad818-395">In the **Advanced Settings** dialog box, on the **Backup** tab, select **Incremental**.</span></span> <span data-ttu-id="ad818-396">Be sure that the **Create synthetic full backups periodically** check box is cleared.</span><span class="sxs-lookup"><span data-stu-id="ad818-396">Be sure that the **Create synthetic full backups periodically** check box is cleared.</span></span> <span data-ttu-id="ad818-397">Select the **Create active full backups periodically** check box.</span><span class="sxs-lookup"><span data-stu-id="ad818-397">Select the **Create active full backups periodically** check box.</span></span> <span data-ttu-id="ad818-398">Under **Active full backup**, select the **Weekly on selected days** check box for Saturday.</span><span class="sxs-lookup"><span data-stu-id="ad818-398">Under **Active full backup**, select the **Weekly on selected days** check box for Saturday.</span></span>

    ![Veeam management console, new backup job advanced settings page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage12.png)

6. <span data-ttu-id="ad818-400">On the **Storage** tab, make sure that the **Enable inline data deduplication** check box is cleared.</span><span class="sxs-lookup"><span data-stu-id="ad818-400">On the **Storage** tab, make sure that the **Enable inline data deduplication** check box is cleared.</span></span> <span data-ttu-id="ad818-401">Select the **Exclude swap file blocks** check box, and select the **Exclude deleted file blocks** check box.</span><span class="sxs-lookup"><span data-stu-id="ad818-401">Select the **Exclude swap file blocks** check box, and select the **Exclude deleted file blocks** check box.</span></span> <span data-ttu-id="ad818-402">Set **Compression level** to **None**.</span><span class="sxs-lookup"><span data-stu-id="ad818-402">Set **Compression level** to **None**.</span></span> <span data-ttu-id="ad818-403">For balanced performance and deduplication, set **Storage optimization** to **LAN target**.</span><span class="sxs-lookup"><span data-stu-id="ad818-403">For balanced performance and deduplication, set **Storage optimization** to **LAN target**.</span></span> <span data-ttu-id="ad818-404">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="ad818-404">Select **OK**.</span></span>

    ![Veeam management console, new backup job advanced settings page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage13.png)

    <span data-ttu-id="ad818-406">For information about Veeam deduplication and compression settings, see [Data Compression and Deduplication](https://helpcenter.veeam.com/backup/vsphere/compression_deduplication.html).</span><span class="sxs-lookup"><span data-stu-id="ad818-406">For information about Veeam deduplication and compression settings, see [Data Compression and Deduplication](https://helpcenter.veeam.com/backup/vsphere/compression_deduplication.html).</span></span>

7.  <span data-ttu-id="ad818-407">In the **Edit Backup Job** dialog box, you can select the **Enable application-aware processing** check box (optional).</span><span class="sxs-lookup"><span data-stu-id="ad818-407">In the **Edit Backup Job** dialog box, you can select the **Enable application-aware processing** check box (optional).</span></span>

    ![Veeam management console, new backup job guest processing page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage14.png)

8.  <span data-ttu-id="ad818-409">Set the schedule to run once daily, at a time you can specify.</span><span class="sxs-lookup"><span data-stu-id="ad818-409">Set the schedule to run once daily, at a time you can specify.</span></span>

    ![Veeam management console, new backup job schedule page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage15.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="ad818-411">Set up StorSimple as a secondary backup target</span><span class="sxs-lookup"><span data-stu-id="ad818-411">Set up StorSimple as a secondary backup target</span></span>

> [!NOTE]
> <span data-ttu-id="ad818-412">Data restores from a backup that has been tiered to the cloud occur at cloud speeds.</span><span class="sxs-lookup"><span data-stu-id="ad818-412">Data restores from a backup that has been tiered to the cloud occur at cloud speeds.</span></span>

<span data-ttu-id="ad818-413">In this model, you must have a storage media (other than StorSimple) to serve as a temporary cache.</span><span class="sxs-lookup"><span data-stu-id="ad818-413">In this model, you must have a storage media (other than StorSimple) to serve as a temporary cache.</span></span> <span data-ttu-id="ad818-414">For example, you can use a redundant array of independent disks (RAID) volume to accommodate space, input/output (I/O), and bandwidth.</span><span class="sxs-lookup"><span data-stu-id="ad818-414">For example, you can use a redundant array of independent disks (RAID) volume to accommodate space, input/output (I/O), and bandwidth.</span></span> <span data-ttu-id="ad818-415">We recommend using RAID 5, 50, and 10.</span><span class="sxs-lookup"><span data-stu-id="ad818-415">We recommend using RAID 5, 50, and 10.</span></span>

<span data-ttu-id="ad818-416">The following figure shows typical short-term retention local (to the server) volumes and long-term retention archive volumes.</span><span class="sxs-lookup"><span data-stu-id="ad818-416">The following figure shows typical short-term retention local (to the server) volumes and long-term retention archive volumes.</span></span> <span data-ttu-id="ad818-417">In this scenario, all backups run on the local (to the server) RAID volume.</span><span class="sxs-lookup"><span data-stu-id="ad818-417">In this scenario, all backups run on the local (to the server) RAID volume.</span></span> <span data-ttu-id="ad818-418">These backups are periodically duplicated and archived to an archive volume.</span><span class="sxs-lookup"><span data-stu-id="ad818-418">These backups are periodically duplicated and archived to an archive volume.</span></span> <span data-ttu-id="ad818-419">It is important to size your local (to the server) RAID volume so that it can handle your short-term retention capacity and performance requirements.</span><span class="sxs-lookup"><span data-stu-id="ad818-419">It is important to size your local (to the server) RAID volume so that it can handle your short-term retention capacity and performance requirements.</span></span>

![StorSimple as secondary backup target logical diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/secondarybackuptargetdiagram.png)

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a><span data-ttu-id="ad818-421">StorSimple as a secondary backup target GFS example</span><span class="sxs-lookup"><span data-stu-id="ad818-421">StorSimple as a secondary backup target GFS example</span></span>

<span data-ttu-id="ad818-422">The following table shows how to set up backups to run on the local and StorSimple disks.</span><span class="sxs-lookup"><span data-stu-id="ad818-422">The following table shows how to set up backups to run on the local and StorSimple disks.</span></span> <span data-ttu-id="ad818-423">It includes individual and total capacity requirements.</span><span class="sxs-lookup"><span data-stu-id="ad818-423">It includes individual and total capacity requirements.</span></span>

| <span data-ttu-id="ad818-424">Backup type and retention</span><span class="sxs-lookup"><span data-stu-id="ad818-424">Backup type and retention</span></span> | <span data-ttu-id="ad818-425">Configured storage</span><span class="sxs-lookup"><span data-stu-id="ad818-425">Configured storage</span></span> | <span data-ttu-id="ad818-426">Size (TiB)</span><span class="sxs-lookup"><span data-stu-id="ad818-426">Size (TiB)</span></span> | <span data-ttu-id="ad818-427">GFS multiplier</span><span class="sxs-lookup"><span data-stu-id="ad818-427">GFS multiplier</span></span> | <span data-ttu-id="ad818-428">Total capacity\* (TiB)</span><span class="sxs-lookup"><span data-stu-id="ad818-428">Total capacity\* (TiB)</span></span> |
|---|---|---|---|---|
| <span data-ttu-id="ad818-429">Week 1 (full and incremental)</span><span class="sxs-lookup"><span data-stu-id="ad818-429">Week 1 (full and incremental)</span></span> |<span data-ttu-id="ad818-430">Local disk (short-term)</span><span class="sxs-lookup"><span data-stu-id="ad818-430">Local disk (short-term)</span></span>| <span data-ttu-id="ad818-431">1</span><span class="sxs-lookup"><span data-stu-id="ad818-431">1</span></span> | <span data-ttu-id="ad818-432">1</span><span class="sxs-lookup"><span data-stu-id="ad818-432">1</span></span> | <span data-ttu-id="ad818-433">1</span><span class="sxs-lookup"><span data-stu-id="ad818-433">1</span></span> |
| <span data-ttu-id="ad818-434">StorSimple weeks 2-4</span><span class="sxs-lookup"><span data-stu-id="ad818-434">StorSimple weeks 2-4</span></span> |<span data-ttu-id="ad818-435">StorSimple disk (long-term)</span><span class="sxs-lookup"><span data-stu-id="ad818-435">StorSimple disk (long-term)</span></span> | <span data-ttu-id="ad818-436">1</span><span class="sxs-lookup"><span data-stu-id="ad818-436">1</span></span> | <span data-ttu-id="ad818-437">4</span><span class="sxs-lookup"><span data-stu-id="ad818-437">4</span></span> | <span data-ttu-id="ad818-438">4</span><span class="sxs-lookup"><span data-stu-id="ad818-438">4</span></span> |
| <span data-ttu-id="ad818-439">Monthly full</span><span class="sxs-lookup"><span data-stu-id="ad818-439">Monthly full</span></span> |<span data-ttu-id="ad818-440">StorSimple disk (long-term)</span><span class="sxs-lookup"><span data-stu-id="ad818-440">StorSimple disk (long-term)</span></span> | <span data-ttu-id="ad818-441">1</span><span class="sxs-lookup"><span data-stu-id="ad818-441">1</span></span> | <span data-ttu-id="ad818-442">12</span><span class="sxs-lookup"><span data-stu-id="ad818-442">12</span></span> | <span data-ttu-id="ad818-443">12</span><span class="sxs-lookup"><span data-stu-id="ad818-443">12</span></span> |
| <span data-ttu-id="ad818-444">Yearly full</span><span class="sxs-lookup"><span data-stu-id="ad818-444">Yearly full</span></span> |<span data-ttu-id="ad818-445">StorSimple disk (long-term)</span><span class="sxs-lookup"><span data-stu-id="ad818-445">StorSimple disk (long-term)</span></span> | <span data-ttu-id="ad818-446">1</span><span class="sxs-lookup"><span data-stu-id="ad818-446">1</span></span> | <span data-ttu-id="ad818-447">1</span><span class="sxs-lookup"><span data-stu-id="ad818-447">1</span></span> | <span data-ttu-id="ad818-448">1</span><span class="sxs-lookup"><span data-stu-id="ad818-448">1</span></span> |
|<span data-ttu-id="ad818-449">GFS volumes size requirement</span><span class="sxs-lookup"><span data-stu-id="ad818-449">GFS volumes size requirement</span></span> |  |  |  | <span data-ttu-id="ad818-450">18\*</span><span class="sxs-lookup"><span data-stu-id="ad818-450">18\*</span></span>|
<span data-ttu-id="ad818-451">\* Total capacity includes 17 TiB of StorSimple disks and 1 TiB of local RAID volume.</span><span class="sxs-lookup"><span data-stu-id="ad818-451">\* Total capacity includes 17 TiB of StorSimple disks and 1 TiB of local RAID volume.</span></span>


### <a name="gfs-example-schedule"></a><span data-ttu-id="ad818-452">GFS example schedule</span><span class="sxs-lookup"><span data-stu-id="ad818-452">GFS example schedule</span></span>

<span data-ttu-id="ad818-453">GFS rotation weekly, monthly, and yearly schedule</span><span class="sxs-lookup"><span data-stu-id="ad818-453">GFS rotation weekly, monthly, and yearly schedule</span></span>

| <span data-ttu-id="ad818-454">Week</span><span class="sxs-lookup"><span data-stu-id="ad818-454">Week</span></span> | <span data-ttu-id="ad818-455">Full</span><span class="sxs-lookup"><span data-stu-id="ad818-455">Full</span></span> | <span data-ttu-id="ad818-456">Incremental day 1</span><span class="sxs-lookup"><span data-stu-id="ad818-456">Incremental day 1</span></span> | <span data-ttu-id="ad818-457">Incremental day 2</span><span class="sxs-lookup"><span data-stu-id="ad818-457">Incremental day 2</span></span> | <span data-ttu-id="ad818-458">Incremental day 3</span><span class="sxs-lookup"><span data-stu-id="ad818-458">Incremental day 3</span></span> | <span data-ttu-id="ad818-459">Incremental day 4</span><span class="sxs-lookup"><span data-stu-id="ad818-459">Incremental day 4</span></span> | <span data-ttu-id="ad818-460">Incremental day 5</span><span class="sxs-lookup"><span data-stu-id="ad818-460">Incremental day 5</span></span> |
|---|---|---|---|---|---|---|
| <span data-ttu-id="ad818-461">Week 1</span><span class="sxs-lookup"><span data-stu-id="ad818-461">Week 1</span></span> | <span data-ttu-id="ad818-462">Local RAID volume</span><span class="sxs-lookup"><span data-stu-id="ad818-462">Local RAID volume</span></span>  | <span data-ttu-id="ad818-463">Local RAID volume</span><span class="sxs-lookup"><span data-stu-id="ad818-463">Local RAID volume</span></span> | <span data-ttu-id="ad818-464">Local RAID volume</span><span class="sxs-lookup"><span data-stu-id="ad818-464">Local RAID volume</span></span> | <span data-ttu-id="ad818-465">Local RAID volume</span><span class="sxs-lookup"><span data-stu-id="ad818-465">Local RAID volume</span></span> | <span data-ttu-id="ad818-466">Local RAID volume</span><span class="sxs-lookup"><span data-stu-id="ad818-466">Local RAID volume</span></span> | <span data-ttu-id="ad818-467">Local RAID volume</span><span class="sxs-lookup"><span data-stu-id="ad818-467">Local RAID volume</span></span> |
| <span data-ttu-id="ad818-468">Week 2</span><span class="sxs-lookup"><span data-stu-id="ad818-468">Week 2</span></span> | <span data-ttu-id="ad818-469">StorSimple weeks 2-4</span><span class="sxs-lookup"><span data-stu-id="ad818-469">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="ad818-470">Week 3</span><span class="sxs-lookup"><span data-stu-id="ad818-470">Week 3</span></span> | <span data-ttu-id="ad818-471">StorSimple weeks 2-4</span><span class="sxs-lookup"><span data-stu-id="ad818-471">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="ad818-472">Week 4</span><span class="sxs-lookup"><span data-stu-id="ad818-472">Week 4</span></span> | <span data-ttu-id="ad818-473">StorSimple weeks 2-4</span><span class="sxs-lookup"><span data-stu-id="ad818-473">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="ad818-474">Monthly</span><span class="sxs-lookup"><span data-stu-id="ad818-474">Monthly</span></span> | <span data-ttu-id="ad818-475">StorSimple monthly</span><span class="sxs-lookup"><span data-stu-id="ad818-475">StorSimple monthly</span></span> |   |   |   |   |   |
| <span data-ttu-id="ad818-476">Yearly</span><span class="sxs-lookup"><span data-stu-id="ad818-476">Yearly</span></span> | <span data-ttu-id="ad818-477">StorSimple yearly</span><span class="sxs-lookup"><span data-stu-id="ad818-477">StorSimple yearly</span></span>  |   |   |   |   |   |   |

### <a name="assign-storsimple-volumes-to-a-veeam-copy-job"></a><span data-ttu-id="ad818-478">Assign StorSimple volumes to a Veeam copy job</span><span class="sxs-lookup"><span data-stu-id="ad818-478">Assign StorSimple volumes to a Veeam copy job</span></span>

#### <a name="to-assign-storsimple-volumes-to-a-veeam-copy-job"></a><span data-ttu-id="ad818-479">To assign StorSimple volumes to a Veeam copy job</span><span class="sxs-lookup"><span data-stu-id="ad818-479">To assign StorSimple volumes to a Veeam copy job</span></span>

1.  <span data-ttu-id="ad818-480">In the Veeam Backup and Replication console, select **Backup & Replication**.</span><span class="sxs-lookup"><span data-stu-id="ad818-480">In the Veeam Backup and Replication console, select **Backup & Replication**.</span></span> <span data-ttu-id="ad818-481">Right-click **Backup**, and then select **VMware** or **Hyper-V**, depending on your environment.</span><span class="sxs-lookup"><span data-stu-id="ad818-481">Right-click **Backup**, and then select **VMware** or **Hyper-V**, depending on your environment.</span></span>

    ![Veeam management console, new backup copy job page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage16.png)

2.  <span data-ttu-id="ad818-483">In the **New Backup Copy Job** dialog box, enter a name and description for the job.</span><span class="sxs-lookup"><span data-stu-id="ad818-483">In the **New Backup Copy Job** dialog box, enter a name and description for the job.</span></span>

    ![Veeam management console, new backup copy job page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage17.png)

3.  <span data-ttu-id="ad818-485">Select the VMs you want to process.</span><span class="sxs-lookup"><span data-stu-id="ad818-485">Select the VMs you want to process.</span></span> <span data-ttu-id="ad818-486">Select from backups, and then select the daily backup that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="ad818-486">Select from backups, and then select the daily backup that you created earlier.</span></span>

    ![Veeam management console, new backup copy job page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage18.png)

4.  <span data-ttu-id="ad818-488">Exclude objects from the backup copy job, if needed.</span><span class="sxs-lookup"><span data-stu-id="ad818-488">Exclude objects from the backup copy job, if needed.</span></span>

5.  <span data-ttu-id="ad818-489">Select your backup repository, and set a value for **Restore points to keep**.</span><span class="sxs-lookup"><span data-stu-id="ad818-489">Select your backup repository, and set a value for **Restore points to keep**.</span></span> <span data-ttu-id="ad818-490">Be sure to select the **Keep the following restore points for archival purposes** check box.</span><span class="sxs-lookup"><span data-stu-id="ad818-490">Be sure to select the **Keep the following restore points for archival purposes** check box.</span></span> <span data-ttu-id="ad818-491">Define the backup frequency, and then select **Advanced**.</span><span class="sxs-lookup"><span data-stu-id="ad818-491">Define the backup frequency, and then select **Advanced**.</span></span>

    ![Veeam management console, new backup copy job page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage19.png)

6.  <span data-ttu-id="ad818-493">Specify the following advanced settings:</span><span class="sxs-lookup"><span data-stu-id="ad818-493">Specify the following advanced settings:</span></span>

    * <span data-ttu-id="ad818-494">On the **Maintenance** tab, turn off storage level corruption guard.</span><span class="sxs-lookup"><span data-stu-id="ad818-494">On the **Maintenance** tab, turn off storage level corruption guard.</span></span>

    ![Veeam management console, new backup copy job advanced settings page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage20.png)

    * <span data-ttu-id="ad818-496">On the **Storage** tab, be sure that deduplication and compression are turned off.</span><span class="sxs-lookup"><span data-stu-id="ad818-496">On the **Storage** tab, be sure that deduplication and compression are turned off.</span></span>

    ![Veeam management console, new backup copy job advanced settings page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage21.png)

7.  <span data-ttu-id="ad818-498">Specify that the data transfer is direct.</span><span class="sxs-lookup"><span data-stu-id="ad818-498">Specify that the data transfer is direct.</span></span>

8.  <span data-ttu-id="ad818-499">Define the backup copy window schedule according to your needs, and then finish the wizard.</span><span class="sxs-lookup"><span data-stu-id="ad818-499">Define the backup copy window schedule according to your needs, and then finish the wizard.</span></span>

<span data-ttu-id="ad818-500">For more information, see [Create backup copy jobs](https://helpcenter.veeam.com/backup/hyperv/backup_copy_create.html).</span><span class="sxs-lookup"><span data-stu-id="ad818-500">For more information, see [Create backup copy jobs](https://helpcenter.veeam.com/backup/hyperv/backup_copy_create.html).</span></span>

## <a name="storsimple-cloud-snapshots"></a><span data-ttu-id="ad818-501">StorSimple cloud snapshots</span><span class="sxs-lookup"><span data-stu-id="ad818-501">StorSimple cloud snapshots</span></span>

<span data-ttu-id="ad818-502">StorSimple cloud snapshots protect the data that resides in your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="ad818-502">StorSimple cloud snapshots protect the data that resides in your StorSimple device.</span></span> <span data-ttu-id="ad818-503">Creating a cloud snapshot is equivalent to shipping local backup tapes to an offsite facility.</span><span class="sxs-lookup"><span data-stu-id="ad818-503">Creating a cloud snapshot is equivalent to shipping local backup tapes to an offsite facility.</span></span> <span data-ttu-id="ad818-504">If you use Azure geo-redundant storage, creating a cloud snapshot is equivalent to shipping backup tapes to multiple sites.</span><span class="sxs-lookup"><span data-stu-id="ad818-504">If you use Azure geo-redundant storage, creating a cloud snapshot is equivalent to shipping backup tapes to multiple sites.</span></span> <span data-ttu-id="ad818-505">If you need to restore a device after a disaster, you might bring another StorSimple device online and do a failover.</span><span class="sxs-lookup"><span data-stu-id="ad818-505">If you need to restore a device after a disaster, you might bring another StorSimple device online and do a failover.</span></span> <span data-ttu-id="ad818-506">After the failover, you would be able to access the data (at cloud speeds) from the most recent cloud snapshot.</span><span class="sxs-lookup"><span data-stu-id="ad818-506">After the failover, you would be able to access the data (at cloud speeds) from the most recent cloud snapshot.</span></span>

<span data-ttu-id="ad818-507">The following section describes how to create a short script to start and delete StorSimple cloud snapshots during backup post-processing.</span><span class="sxs-lookup"><span data-stu-id="ad818-507">The following section describes how to create a short script to start and delete StorSimple cloud snapshots during backup post-processing.</span></span>

> [!NOTE]
> <span data-ttu-id="ad818-508">Snapshots that are manually or programmatically created do not follow the StorSimple snapshot expiration policy.</span><span class="sxs-lookup"><span data-stu-id="ad818-508">Snapshots that are manually or programmatically created do not follow the StorSimple snapshot expiration policy.</span></span> <span data-ttu-id="ad818-509">These snapshots must be manually or programmatically deleted.</span><span class="sxs-lookup"><span data-stu-id="ad818-509">These snapshots must be manually or programmatically deleted.</span></span>

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a><span data-ttu-id="ad818-510">Start and delete cloud snapshots by using a script</span><span class="sxs-lookup"><span data-stu-id="ad818-510">Start and delete cloud snapshots by using a script</span></span>

> [!NOTE]
> <span data-ttu-id="ad818-511">Carefully assess the compliance and data retention repercussions before you delete a StorSimple snapshot.</span><span class="sxs-lookup"><span data-stu-id="ad818-511">Carefully assess the compliance and data retention repercussions before you delete a StorSimple snapshot.</span></span> <span data-ttu-id="ad818-512">For more information about how to run a post-backup script, see the Veeam documentation.</span><span class="sxs-lookup"><span data-stu-id="ad818-512">For more information about how to run a post-backup script, see the Veeam documentation.</span></span>


### <a name="backup-lifecycle"></a><span data-ttu-id="ad818-513">Backup lifecycle</span><span class="sxs-lookup"><span data-stu-id="ad818-513">Backup lifecycle</span></span>

![Backup lifecycle diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/backuplifecycle.png)

### <a name="requirements"></a><span data-ttu-id="ad818-515">Requirements</span><span class="sxs-lookup"><span data-stu-id="ad818-515">Requirements</span></span>

-   <span data-ttu-id="ad818-516">The server that runs the script must have access to Azure cloud resources.</span><span class="sxs-lookup"><span data-stu-id="ad818-516">The server that runs the script must have access to Azure cloud resources.</span></span>
-   <span data-ttu-id="ad818-517">The user account must have the necessary permissions.</span><span class="sxs-lookup"><span data-stu-id="ad818-517">The user account must have the necessary permissions.</span></span>
-   <span data-ttu-id="ad818-518">A StorSimple backup policy with the associated StorSimple volumes must be set up but not turned on.</span><span class="sxs-lookup"><span data-stu-id="ad818-518">A StorSimple backup policy with the associated StorSimple volumes must be set up but not turned on.</span></span>
-   <span data-ttu-id="ad818-519">You'll need the StorSimple resource name, registration key, device name, and backup policy ID.</span><span class="sxs-lookup"><span data-stu-id="ad818-519">You'll need the StorSimple resource name, registration key, device name, and backup policy ID.</span></span>

### <a name="to-start-or-delete-a-cloud-snapshot"></a><span data-ttu-id="ad818-520">To start or delete a cloud snapshot</span><span class="sxs-lookup"><span data-stu-id="ad818-520">To start or delete a cloud snapshot</span></span>

1. <span data-ttu-id="ad818-521">[Install Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="ad818-521">[Install Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azureps-cmdlets-docs/).</span></span>
2. <span data-ttu-id="ad818-522">[Download and import publish settings and subscription information](https://msdn.microsoft.com/library/dn385850.aspx).</span><span class="sxs-lookup"><span data-stu-id="ad818-522">[Download and import publish settings and subscription information](https://msdn.microsoft.com/library/dn385850.aspx).</span></span>
3. <span data-ttu-id="ad818-523">In the Azure classic portal, get the resource name and [registration key for your StorSimple Manager service](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="ad818-523">In the Azure classic portal, get the resource name and [registration key for your StorSimple Manager service](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).</span></span>
4. <span data-ttu-id="ad818-524">On the server that runs the script, run PowerShell as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ad818-524">On the server that runs the script, run PowerShell as an administrator.</span></span> <span data-ttu-id="ad818-525">Type this command:</span><span class="sxs-lookup"><span data-stu-id="ad818-525">Type this command:</span></span>

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    <span data-ttu-id="ad818-526">Note the backup policy ID.</span><span class="sxs-lookup"><span data-stu-id="ad818-526">Note the backup policy ID.</span></span>
5. <span data-ttu-id="ad818-527">In Notepad, create a new PowerShell script by using the following code.</span><span class="sxs-lookup"><span data-stu-id="ad818-527">In Notepad, create a new PowerShell script by using the following code.</span></span>

    <span data-ttu-id="ad818-528">Copy and paste this code snippet:</span><span class="sxs-lookup"><span data-stu-id="ad818-528">Copy and paste this code snippet:</span></span>
    ```powershell
    Import-AzurePublishSettingsFile "c:\\CloudSnapshot Snapshot\\myAzureSettings.publishsettings"
    Disable-AzureDataCollection
    $ApplianceName = <myStorSimpleApplianceName>
    $RetentionInDays = 20
    $RetentionInDays = -$RetentionInDays
    $Today = Get-Date
    $ExpirationDate = $Today.AddDays($RetentionInDays)
    Select-AzureStorSimpleResource -ResourceName "myResource" –RegistrationKey
    Start-AzureStorSimpleDeviceBackupJob –DeviceName $ApplianceName -BackupType CloudSnapshot -BackupPolicyId <BackupId> -Verbose
    $CompletedSnapshots =@()
    $CompletedSnapshots = Get-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName
    Write-Host "The Expiration date is " $ExpirationDate
    Write-Host

    ForEach ($SnapShot in $CompletedSnapshots)
    {
        $SnapshotStartTimeStamp = $Snapshot.CreatedOn
        if ($SnapshotStartTimeStamp -lt $ExpirationDate)

        {
            $SnapShotInstanceID = $SnapShot.InstanceId
            Write-Host "This snpashotdate was created on " $SnapshotStartTimeStamp.Date.ToShortDateString()
            Write-Host "Instance ID " $SnapShotInstanceID
            Write-Host "This snpashotdate is older and needs to be deleted"
            Write-host "\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#"
            Remove-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName -BackupId $SnapShotInstanceID -Force -Verbose
        }
    }
    ```
6. <span data-ttu-id="ad818-529">To add the script to your backup job, edit your Veeam job advanced options.</span><span class="sxs-lookup"><span data-stu-id="ad818-529">To add the script to your backup job, edit your Veeam job advanced options.</span></span>

    ![Veeam backup advanced settings scripts tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-veeam/veeamimage22.png)

<span data-ttu-id="ad818-531">We recommend that you run your StorSimple cloud snapshot backup policy as a post-processing script at the end of your daily backup job.</span><span class="sxs-lookup"><span data-stu-id="ad818-531">We recommend that you run your StorSimple cloud snapshot backup policy as a post-processing script at the end of your daily backup job.</span></span> <span data-ttu-id="ad818-532">For more information about how to back up and restore your backup application environment to help you meet your RPO and RTO, please consult with your backup architect.</span><span class="sxs-lookup"><span data-stu-id="ad818-532">For more information about how to back up and restore your backup application environment to help you meet your RPO and RTO, please consult with your backup architect.</span></span>

## <a name="storsimple-as-a-restore-source"></a><span data-ttu-id="ad818-533">StorSimple as a restore source</span><span class="sxs-lookup"><span data-stu-id="ad818-533">StorSimple as a restore source</span></span>

<span data-ttu-id="ad818-534">Restores from a StorSimple device work like restores from any block storage device.</span><span class="sxs-lookup"><span data-stu-id="ad818-534">Restores from a StorSimple device work like restores from any block storage device.</span></span> <span data-ttu-id="ad818-535">Restores of data that is tiered to the cloud occurs at cloud speeds.</span><span class="sxs-lookup"><span data-stu-id="ad818-535">Restores of data that is tiered to the cloud occurs at cloud speeds.</span></span> <span data-ttu-id="ad818-536">For local data, restores occur at the local disk speed of the device.</span><span class="sxs-lookup"><span data-stu-id="ad818-536">For local data, restores occur at the local disk speed of the device.</span></span>

<span data-ttu-id="ad818-537">With Veeam, you get fast, granular, file-level recovery through StorSimple via the built-in explorer views in the Veeam console.</span><span class="sxs-lookup"><span data-stu-id="ad818-537">With Veeam, you get fast, granular, file-level recovery through StorSimple via the built-in explorer views in the Veeam console.</span></span> <span data-ttu-id="ad818-538">Use the Veeam Explorers to recover individual items, like email messages, Active Directory objects, and SharePoint items from backups.</span><span class="sxs-lookup"><span data-stu-id="ad818-538">Use the Veeam Explorers to recover individual items, like email messages, Active Directory objects, and SharePoint items from backups.</span></span> <span data-ttu-id="ad818-539">The recovery can be done without on-premises VM disruption.</span><span class="sxs-lookup"><span data-stu-id="ad818-539">The recovery can be done without on-premises VM disruption.</span></span> <span data-ttu-id="ad818-540">You also can do point-in-time recovery for Azure SQL Database and Oracle databases.</span><span class="sxs-lookup"><span data-stu-id="ad818-540">You also can do point-in-time recovery for Azure SQL Database and Oracle databases.</span></span> <span data-ttu-id="ad818-541">Veeam and StorSimple make the process of item-level recovery from Azure fast and easy.</span><span class="sxs-lookup"><span data-stu-id="ad818-541">Veeam and StorSimple make the process of item-level recovery from Azure fast and easy.</span></span> <span data-ttu-id="ad818-542">For information about how to perform a restore, see the Veeam documentation:</span><span class="sxs-lookup"><span data-stu-id="ad818-542">For information about how to perform a restore, see the Veeam documentation:</span></span>

- <span data-ttu-id="ad818-543">For [Exchange Server](https://www.veeam.com/microsoft-exchange-recovery.html)</span><span class="sxs-lookup"><span data-stu-id="ad818-543">For [Exchange Server](https://www.veeam.com/microsoft-exchange-recovery.html)</span></span>
- <span data-ttu-id="ad818-544">For [Active Directory](https://www.veeam.com/microsoft-active-directory-explorer.html)</span><span class="sxs-lookup"><span data-stu-id="ad818-544">For [Active Directory](https://www.veeam.com/microsoft-active-directory-explorer.html)</span></span>
- <span data-ttu-id="ad818-545">For [SQL Server](https://www.veeam.com/microsoft-sql-server-explorer.html)</span><span class="sxs-lookup"><span data-stu-id="ad818-545">For [SQL Server](https://www.veeam.com/microsoft-sql-server-explorer.html)</span></span>
- <span data-ttu-id="ad818-546">For [SharePoint](https://www.veeam.com/microsoft-sharepoint-recovery-explorer.html)</span><span class="sxs-lookup"><span data-stu-id="ad818-546">For [SharePoint](https://www.veeam.com/microsoft-sharepoint-recovery-explorer.html)</span></span>
- <span data-ttu-id="ad818-547">For [Oracle](https://www.veeam.com/oracle-backup-recovery-explorer.html)</span><span class="sxs-lookup"><span data-stu-id="ad818-547">For [Oracle](https://www.veeam.com/oracle-backup-recovery-explorer.html)</span></span>


## <a name="storsimple-failover-and-disaster-recovery"></a><span data-ttu-id="ad818-548">StorSimple failover and disaster recovery</span><span class="sxs-lookup"><span data-stu-id="ad818-548">StorSimple failover and disaster recovery</span></span>

> [!NOTE]
> <span data-ttu-id="ad818-549">For backup target scenarios, StorSimple Cloud Appliance is not supported as a restore target.</span><span class="sxs-lookup"><span data-stu-id="ad818-549">For backup target scenarios, StorSimple Cloud Appliance is not supported as a restore target.</span></span>

<span data-ttu-id="ad818-550">A disaster can be caused by a variety of factors.</span><span class="sxs-lookup"><span data-stu-id="ad818-550">A disaster can be caused by a variety of factors.</span></span> <span data-ttu-id="ad818-551">The following table lists common disaster recovery scenarios.</span><span class="sxs-lookup"><span data-stu-id="ad818-551">The following table lists common disaster recovery scenarios.</span></span>

| <span data-ttu-id="ad818-552">Scenario</span><span class="sxs-lookup"><span data-stu-id="ad818-552">Scenario</span></span> | <span data-ttu-id="ad818-553">Impact</span><span class="sxs-lookup"><span data-stu-id="ad818-553">Impact</span></span> | <span data-ttu-id="ad818-554">How to recover</span><span class="sxs-lookup"><span data-stu-id="ad818-554">How to recover</span></span> | <span data-ttu-id="ad818-555">Notes</span><span class="sxs-lookup"><span data-stu-id="ad818-555">Notes</span></span> |
|---|---|---|---|
| <span data-ttu-id="ad818-556">StorSimple device failure</span><span class="sxs-lookup"><span data-stu-id="ad818-556">StorSimple device failure</span></span> | <span data-ttu-id="ad818-557">Backup and restore operations are interrupted.</span><span class="sxs-lookup"><span data-stu-id="ad818-557">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="ad818-558">Replace the failed device and perform [StorSimple failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="ad818-558">Replace the failed device and perform [StorSimple failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span> | <span data-ttu-id="ad818-559">If you need to perform a restore after device recovery, full data working sets are retrieved from the cloud to the new device.</span><span class="sxs-lookup"><span data-stu-id="ad818-559">If you need to perform a restore after device recovery, full data working sets are retrieved from the cloud to the new device.</span></span> <span data-ttu-id="ad818-560">All operations are at cloud speeds.</span><span class="sxs-lookup"><span data-stu-id="ad818-560">All operations are at cloud speeds.</span></span> <span data-ttu-id="ad818-561">The index and catalog rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier, which might be a time-consuming process.</span><span class="sxs-lookup"><span data-stu-id="ad818-561">The index and catalog rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier, which might be a time-consuming process.</span></span> |
| <span data-ttu-id="ad818-562">Veeam server failure</span><span class="sxs-lookup"><span data-stu-id="ad818-562">Veeam server failure</span></span> | <span data-ttu-id="ad818-563">Backup and restore operations are interrupted.</span><span class="sxs-lookup"><span data-stu-id="ad818-563">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="ad818-564">Rebuild the backup server and perform database restore as detailed in [Veeam Help Center (Technical Documentation)](https://www.veeam.com/documentation-guides-datasheets.html).</span><span class="sxs-lookup"><span data-stu-id="ad818-564">Rebuild the backup server and perform database restore as detailed in [Veeam Help Center (Technical Documentation)](https://www.veeam.com/documentation-guides-datasheets.html).</span></span>  | <span data-ttu-id="ad818-565">You must rebuild or restore the Veeam server at the disaster recovery site.</span><span class="sxs-lookup"><span data-stu-id="ad818-565">You must rebuild or restore the Veeam server at the disaster recovery site.</span></span> <span data-ttu-id="ad818-566">Restore the database to the most recent point.</span><span class="sxs-lookup"><span data-stu-id="ad818-566">Restore the database to the most recent point.</span></span> <span data-ttu-id="ad818-567">If the restored Veeam database is not in sync with your latest backup jobs, indexing and cataloging is required.</span><span class="sxs-lookup"><span data-stu-id="ad818-567">If the restored Veeam database is not in sync with your latest backup jobs, indexing and cataloging is required.</span></span> <span data-ttu-id="ad818-568">This index and catalog rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier.</span><span class="sxs-lookup"><span data-stu-id="ad818-568">This index and catalog rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier.</span></span> <span data-ttu-id="ad818-569">This makes it further time-intensive.</span><span class="sxs-lookup"><span data-stu-id="ad818-569">This makes it further time-intensive.</span></span> |
| <span data-ttu-id="ad818-570">Site failure that results in the loss of both the backup server and StorSimple</span><span class="sxs-lookup"><span data-stu-id="ad818-570">Site failure that results in the loss of both the backup server and StorSimple</span></span> | <span data-ttu-id="ad818-571">Backup and restore operations are interrupted.</span><span class="sxs-lookup"><span data-stu-id="ad818-571">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="ad818-572">Restore StorSimple first, and then restore Veeam.</span><span class="sxs-lookup"><span data-stu-id="ad818-572">Restore StorSimple first, and then restore Veeam.</span></span> | <span data-ttu-id="ad818-573">Restore StorSimple first, and then restore Veeam.</span><span class="sxs-lookup"><span data-stu-id="ad818-573">Restore StorSimple first, and then restore Veeam.</span></span> <span data-ttu-id="ad818-574">If you need to perform a restore after device recovery, the full data working sets are retrieved from the cloud to the new device.</span><span class="sxs-lookup"><span data-stu-id="ad818-574">If you need to perform a restore after device recovery, the full data working sets are retrieved from the cloud to the new device.</span></span> <span data-ttu-id="ad818-575">All operations are at cloud speeds.</span><span class="sxs-lookup"><span data-stu-id="ad818-575">All operations are at cloud speeds.</span></span> |


## <a name="references"></a><span data-ttu-id="ad818-576">References</span><span class="sxs-lookup"><span data-stu-id="ad818-576">References</span></span>

<span data-ttu-id="ad818-577">The following documents were referenced for this article:</span><span class="sxs-lookup"><span data-stu-id="ad818-577">The following documents were referenced for this article:</span></span>

- [<span data-ttu-id="ad818-578">StorSimple multipath I/O setup</span><span class="sxs-lookup"><span data-stu-id="ad818-578">StorSimple multipath I/O setup</span></span>](storsimple-configure-mpio-windows-server.md)
- [<span data-ttu-id="ad818-579">Storage scenarios: Thin provisioning</span><span class="sxs-lookup"><span data-stu-id="ad818-579">Storage scenarios: Thin provisioning</span></span>](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [<span data-ttu-id="ad818-580">Using GPT drives</span><span class="sxs-lookup"><span data-stu-id="ad818-580">Using GPT drives</span></span>](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [<span data-ttu-id="ad818-581">Set up shadow copies for shared folders</span><span class="sxs-lookup"><span data-stu-id="ad818-581">Set up shadow copies for shared folders</span></span>](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a><span data-ttu-id="ad818-582">Next steps</span><span class="sxs-lookup"><span data-stu-id="ad818-582">Next steps</span></span>

- <span data-ttu-id="ad818-583">Learn more about how to [restore from a backup set](storsimple-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="ad818-583">Learn more about how to [restore from a backup set](storsimple-restore-from-backup-set-u2.md).</span></span>
- <span data-ttu-id="ad818-584">Learn more about how to perform [device failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="ad818-584">Learn more about how to perform [device failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span>




























