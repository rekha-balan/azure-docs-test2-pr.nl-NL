---
title: StorSimple 8000 series as backup target with NetBackup | Microsoft Docs
description: Describes the StorSimple backup target configuration with Veritas NetBackup.
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
ms.date: 12/05/2016
ms.author: hkanna
ms.openlocfilehash: 501f93a0e43dcfc0316c4c5e30bd23bcb139e819
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562696"
---
# <a name="storsimple-as-a-backup-target-with-netbackup"></a><span data-ttu-id="41af5-103">StorSimple as a backup target with NetBackup</span><span class="sxs-lookup"><span data-stu-id="41af5-103">StorSimple as a backup target with NetBackup</span></span>

## <a name="overview"></a><span data-ttu-id="41af5-104">Overview</span><span class="sxs-lookup"><span data-stu-id="41af5-104">Overview</span></span>

<span data-ttu-id="41af5-105">Azure StorSimple is a hybrid cloud storage solution from Microsoft.</span><span class="sxs-lookup"><span data-stu-id="41af5-105">Azure StorSimple is a hybrid cloud storage solution from Microsoft.</span></span> <span data-ttu-id="41af5-106">StorSimple addresses the complexities of exponential data growth by using an Azure storage account as an extension of the on-premises solution, and automatically tiering data across on-premises storage and cloud storage.</span><span class="sxs-lookup"><span data-stu-id="41af5-106">StorSimple addresses the complexities of exponential data growth by using an Azure storage account as an extension of the on-premises solution, and automatically tiering data across on-premises storage and cloud storage.</span></span>

<span data-ttu-id="41af5-107">In this article, we discuss StorSimple integration with Veritas NetBackup, and best practices for integrating both solutions.</span><span class="sxs-lookup"><span data-stu-id="41af5-107">In this article, we discuss StorSimple integration with Veritas NetBackup, and best practices for integrating both solutions.</span></span> <span data-ttu-id="41af5-108">We also make recommendations on how to set up Veritas NetBackup to best integrate with StorSimple.</span><span class="sxs-lookup"><span data-stu-id="41af5-108">We also make recommendations on how to set up Veritas NetBackup to best integrate with StorSimple.</span></span> <span data-ttu-id="41af5-109">We defer to Veritas best practices, backup architects, and administrators for the best way to set up Veritas NetBackup to meet individual backup requirements and service-level agreements (SLAs).</span><span class="sxs-lookup"><span data-stu-id="41af5-109">We defer to Veritas best practices, backup architects, and administrators for the best way to set up Veritas NetBackup to meet individual backup requirements and service-level agreements (SLAs).</span></span>

<span data-ttu-id="41af5-110">Although we illustrate configuration steps and key concepts, this article is by no means a step-by-step configuration or installation guide.</span><span class="sxs-lookup"><span data-stu-id="41af5-110">Although we illustrate configuration steps and key concepts, this article is by no means a step-by-step configuration or installation guide.</span></span> <span data-ttu-id="41af5-111">We assume that the basic components and infrastructure are in working order and ready to support the concepts that we describe.</span><span class="sxs-lookup"><span data-stu-id="41af5-111">We assume that the basic components and infrastructure are in working order and ready to support the concepts that we describe.</span></span>

### <a name="who-should-read-this"></a><span data-ttu-id="41af5-112">Who should read this?</span><span class="sxs-lookup"><span data-stu-id="41af5-112">Who should read this?</span></span>

<span data-ttu-id="41af5-113">The information in this article will be most helpful to backup administrators, storage administrators, and storage architects who have knowledge of storage, Windows Server 2012 R2, Ethernet, cloud services, and Veritas NetBackup.</span><span class="sxs-lookup"><span data-stu-id="41af5-113">The information in this article will be most helpful to backup administrators, storage administrators, and storage architects who have knowledge of storage, Windows Server 2012 R2, Ethernet, cloud services, and Veritas NetBackup.</span></span>

### <a name="supported-versions"></a><span data-ttu-id="41af5-114">Supported versions</span><span class="sxs-lookup"><span data-stu-id="41af5-114">Supported versions</span></span>

-   <span data-ttu-id="41af5-115">NetBackup 7.7.x and later versions</span><span class="sxs-lookup"><span data-stu-id="41af5-115">NetBackup 7.7.x and later versions</span></span>
-   [<span data-ttu-id="41af5-116">StorSimple Update 3 and later versions</span><span class="sxs-lookup"><span data-stu-id="41af5-116">StorSimple Update 3 and later versions</span></span>](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a><span data-ttu-id="41af5-117">Why StorSimple as a backup target?</span><span class="sxs-lookup"><span data-stu-id="41af5-117">Why StorSimple as a backup target?</span></span>

<span data-ttu-id="41af5-118">StorSimple is a good choice for a backup target because:</span><span class="sxs-lookup"><span data-stu-id="41af5-118">StorSimple is a good choice for a backup target because:</span></span>

-   <span data-ttu-id="41af5-119">It provides standard, local storage for backup applications to use as a fast backup destination, without any changes.</span><span class="sxs-lookup"><span data-stu-id="41af5-119">It provides standard, local storage for backup applications to use as a fast backup destination, without any changes.</span></span> <span data-ttu-id="41af5-120">You also can use StorSimple for a quick restore of recent backups.</span><span class="sxs-lookup"><span data-stu-id="41af5-120">You also can use StorSimple for a quick restore of recent backups.</span></span>
-   <span data-ttu-id="41af5-121">Its cloud tiering is seamlessly integrated with an Azure cloud storage account to use cost-effective Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="41af5-121">Its cloud tiering is seamlessly integrated with an Azure cloud storage account to use cost-effective Azure Storage.</span></span>
-   <span data-ttu-id="41af5-122">It automatically provides offsite storage for disaster recovery.</span><span class="sxs-lookup"><span data-stu-id="41af5-122">It automatically provides offsite storage for disaster recovery.</span></span>

## <a name="key-concepts"></a><span data-ttu-id="41af5-123">Key concepts</span><span class="sxs-lookup"><span data-stu-id="41af5-123">Key concepts</span></span>

<span data-ttu-id="41af5-124">As with any storage solution, a careful assessment of the solution’s storage performance, SLAs, rate of change, and capacity growth needs is critical to success.</span><span class="sxs-lookup"><span data-stu-id="41af5-124">As with any storage solution, a careful assessment of the solution’s storage performance, SLAs, rate of change, and capacity growth needs is critical to success.</span></span> <span data-ttu-id="41af5-125">The main idea is that by introducing a cloud tier, your access times and throughputs to the cloud play a fundamental role in the ability of StorSimple to do its job.</span><span class="sxs-lookup"><span data-stu-id="41af5-125">The main idea is that by introducing a cloud tier, your access times and throughputs to the cloud play a fundamental role in the ability of StorSimple to do its job.</span></span>

<span data-ttu-id="41af5-126">StorSimple is designed to provide storage to applications that operate on a well-defined working set of data (hot data).</span><span class="sxs-lookup"><span data-stu-id="41af5-126">StorSimple is designed to provide storage to applications that operate on a well-defined working set of data (hot data).</span></span> <span data-ttu-id="41af5-127">In this model, the working set of data is stored on the local tiers, and the remaining nonworking/cold/archived set of data is tiered to the cloud.</span><span class="sxs-lookup"><span data-stu-id="41af5-127">In this model, the working set of data is stored on the local tiers, and the remaining nonworking/cold/archived set of data is tiered to the cloud.</span></span> <span data-ttu-id="41af5-128">This model is represented in the following figure.</span><span class="sxs-lookup"><span data-stu-id="41af5-128">This model is represented in the following figure.</span></span> <span data-ttu-id="41af5-129">The nearly flat green line represents the data stored on the local tiers of the StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="41af5-129">The nearly flat green line represents the data stored on the local tiers of the StorSimple device.</span></span> <span data-ttu-id="41af5-130">The red line represents the total amount of data stored on the StorSimple solution across all tiers.</span><span class="sxs-lookup"><span data-stu-id="41af5-130">The red line represents the total amount of data stored on the StorSimple solution across all tiers.</span></span> <span data-ttu-id="41af5-131">The space between the flat green line and the exponential red curve represents the total amount of data stored in the cloud.</span><span class="sxs-lookup"><span data-stu-id="41af5-131">The space between the flat green line and the exponential red curve represents the total amount of data stored in the cloud.</span></span>

<span data-ttu-id="41af5-132">**StorSimple tiering**
![StorSimple tiering diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/image1.jpg)</span><span class="sxs-lookup"><span data-stu-id="41af5-132">**StorSimple tiering**
![StorSimple tiering diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/image1.jpg)</span></span>

<span data-ttu-id="41af5-133">With this architecture in mind, you will find that StorSimple is ideally suited to operate as a backup target.</span><span class="sxs-lookup"><span data-stu-id="41af5-133">With this architecture in mind, you will find that StorSimple is ideally suited to operate as a backup target.</span></span> <span data-ttu-id="41af5-134">You can use StorSimple to:</span><span class="sxs-lookup"><span data-stu-id="41af5-134">You can use StorSimple to:</span></span>
-   <span data-ttu-id="41af5-135">Perform your most frequent restores from the local working set of data.</span><span class="sxs-lookup"><span data-stu-id="41af5-135">Perform your most frequent restores from the local working set of data.</span></span>
-   <span data-ttu-id="41af5-136">Use the cloud for offsite disaster recovery and older data, where restores are less frequent.</span><span class="sxs-lookup"><span data-stu-id="41af5-136">Use the cloud for offsite disaster recovery and older data, where restores are less frequent.</span></span>

## <a name="storsimple-benefits"></a><span data-ttu-id="41af5-137">StorSimple benefits</span><span class="sxs-lookup"><span data-stu-id="41af5-137">StorSimple benefits</span></span>

<span data-ttu-id="41af5-138">StorSimple provides an on-premises solution that is seamlessly integrated with Microsoft Azure, by taking advantage of seamless access to on-premises and cloud storage.</span><span class="sxs-lookup"><span data-stu-id="41af5-138">StorSimple provides an on-premises solution that is seamlessly integrated with Microsoft Azure, by taking advantage of seamless access to on-premises and cloud storage.</span></span>

<span data-ttu-id="41af5-139">StorSimple uses automatic tiering between the on-premises device, which has solid-state device (SSD) and serial-attached SCSI (SAS) storage, and Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="41af5-139">StorSimple uses automatic tiering between the on-premises device, which has solid-state device (SSD) and serial-attached SCSI (SAS) storage, and Azure Storage.</span></span> <span data-ttu-id="41af5-140">Automatic tiering keeps frequently accessed data local, on the SSD and SAS tiers.</span><span class="sxs-lookup"><span data-stu-id="41af5-140">Automatic tiering keeps frequently accessed data local, on the SSD and SAS tiers.</span></span> <span data-ttu-id="41af5-141">It moves infrequently accessed data to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="41af5-141">It moves infrequently accessed data to Azure Storage.</span></span>

<span data-ttu-id="41af5-142">StorSimple offers these benefits:</span><span class="sxs-lookup"><span data-stu-id="41af5-142">StorSimple offers these benefits:</span></span>

-   <span data-ttu-id="41af5-143">Unique deduplication and compression algorithms that use the cloud to achieve unprecedented deduplication levels</span><span class="sxs-lookup"><span data-stu-id="41af5-143">Unique deduplication and compression algorithms that use the cloud to achieve unprecedented deduplication levels</span></span>
-   <span data-ttu-id="41af5-144">High availability</span><span class="sxs-lookup"><span data-stu-id="41af5-144">High availability</span></span>
-   <span data-ttu-id="41af5-145">Geo-replication by using Azure geo-replication</span><span class="sxs-lookup"><span data-stu-id="41af5-145">Geo-replication by using Azure geo-replication</span></span>
-   <span data-ttu-id="41af5-146">Azure integration</span><span class="sxs-lookup"><span data-stu-id="41af5-146">Azure integration</span></span>
-   <span data-ttu-id="41af5-147">Data encryption in the cloud</span><span class="sxs-lookup"><span data-stu-id="41af5-147">Data encryption in the cloud</span></span>
-   <span data-ttu-id="41af5-148">Improved disaster recovery and compliance</span><span class="sxs-lookup"><span data-stu-id="41af5-148">Improved disaster recovery and compliance</span></span>

<span data-ttu-id="41af5-149">Although StorSimple presents two main deployment scenarios (primary backup target and secondary backup target), fundamentally, it's a plain, block storage device.</span><span class="sxs-lookup"><span data-stu-id="41af5-149">Although StorSimple presents two main deployment scenarios (primary backup target and secondary backup target), fundamentally, it's a plain, block storage device.</span></span> <span data-ttu-id="41af5-150">StorSimple does all the compression and deduplication.</span><span class="sxs-lookup"><span data-stu-id="41af5-150">StorSimple does all the compression and deduplication.</span></span> <span data-ttu-id="41af5-151">It seamlessly sends and retrieves data between the cloud and the application and file system.</span><span class="sxs-lookup"><span data-stu-id="41af5-151">It seamlessly sends and retrieves data between the cloud and the application and file system.</span></span>

<span data-ttu-id="41af5-152">For more information about StorSimple, see [StorSimple 8000 series: Hybrid cloud storage solution](storsimple-overview.md).</span><span class="sxs-lookup"><span data-stu-id="41af5-152">For more information about StorSimple, see [StorSimple 8000 series: Hybrid cloud storage solution](storsimple-overview.md).</span></span> <span data-ttu-id="41af5-153">Also, you can review the [technical StorSimple 8000 series specifications](storsimple-technical-specifications-and-compliance.md).</span><span class="sxs-lookup"><span data-stu-id="41af5-153">Also, you can review the [technical StorSimple 8000 series specifications](storsimple-technical-specifications-and-compliance.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41af5-154">Using a StorSimple device as a backup target is supported only for StorSimple 8000 Update 3 and later versions.</span><span class="sxs-lookup"><span data-stu-id="41af5-154">Using a StorSimple device as a backup target is supported only for StorSimple 8000 Update 3 and later versions.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="41af5-155">Architecture overview</span><span class="sxs-lookup"><span data-stu-id="41af5-155">Architecture overview</span></span>

<span data-ttu-id="41af5-156">The following tables show the device model-to-architecture initial guidance.</span><span class="sxs-lookup"><span data-stu-id="41af5-156">The following tables show the device model-to-architecture initial guidance.</span></span>

<span data-ttu-id="41af5-157">**StorSimple capacities for local and cloud storage**</span><span class="sxs-lookup"><span data-stu-id="41af5-157">**StorSimple capacities for local and cloud storage**</span></span>

| <span data-ttu-id="41af5-158">Storage capacity</span><span class="sxs-lookup"><span data-stu-id="41af5-158">Storage capacity</span></span>       | <span data-ttu-id="41af5-159">8100</span><span class="sxs-lookup"><span data-stu-id="41af5-159">8100</span></span>          | <span data-ttu-id="41af5-160">8600</span><span class="sxs-lookup"><span data-stu-id="41af5-160">8600</span></span>            |
|------------------------|---------------|-----------------|
| <span data-ttu-id="41af5-161">Local storage capacity</span><span class="sxs-lookup"><span data-stu-id="41af5-161">Local storage capacity</span></span> | <span data-ttu-id="41af5-162">&lt; 10 TiB\*</span><span class="sxs-lookup"><span data-stu-id="41af5-162">&lt; 10 TiB\*</span></span>  | <span data-ttu-id="41af5-163">&lt; 20 TiB\*</span><span class="sxs-lookup"><span data-stu-id="41af5-163">&lt; 20 TiB\*</span></span>  |
| <span data-ttu-id="41af5-164">Cloud storage capacity</span><span class="sxs-lookup"><span data-stu-id="41af5-164">Cloud storage capacity</span></span> | <span data-ttu-id="41af5-165">&gt; 200 TiB\*</span><span class="sxs-lookup"><span data-stu-id="41af5-165">&gt; 200 TiB\*</span></span> | <span data-ttu-id="41af5-166">&gt; 500 TiB\*</span><span class="sxs-lookup"><span data-stu-id="41af5-166">&gt; 500 TiB\*</span></span> |
<span data-ttu-id="41af5-167">\* Storage size assumes no deduplication or compression.</span><span class="sxs-lookup"><span data-stu-id="41af5-167">\* Storage size assumes no deduplication or compression.</span></span>

<span data-ttu-id="41af5-168">**StorSimple capacities for primary and secondary backups**</span><span class="sxs-lookup"><span data-stu-id="41af5-168">**StorSimple capacities for primary and secondary backups**</span></span>

| <span data-ttu-id="41af5-169">Backup scenario</span><span class="sxs-lookup"><span data-stu-id="41af5-169">Backup scenario</span></span>  | <span data-ttu-id="41af5-170">Local storage capacity</span><span class="sxs-lookup"><span data-stu-id="41af5-170">Local storage capacity</span></span>  | <span data-ttu-id="41af5-171">Cloud storage capacity</span><span class="sxs-lookup"><span data-stu-id="41af5-171">Cloud storage capacity</span></span>  |
|---|---|---|
| <span data-ttu-id="41af5-172">Primary backup</span><span class="sxs-lookup"><span data-stu-id="41af5-172">Primary backup</span></span>  | <span data-ttu-id="41af5-173">Recent backups stored on local storage for fast recovery to meet recovery point objective (RPO)</span><span class="sxs-lookup"><span data-stu-id="41af5-173">Recent backups stored on local storage for fast recovery to meet recovery point objective (RPO)</span></span> | <span data-ttu-id="41af5-174">Backup history (RPO) fits in cloud capacity</span><span class="sxs-lookup"><span data-stu-id="41af5-174">Backup history (RPO) fits in cloud capacity</span></span> |
| <span data-ttu-id="41af5-175">Secondary backup</span><span class="sxs-lookup"><span data-stu-id="41af5-175">Secondary backup</span></span> | <span data-ttu-id="41af5-176">Secondary copy of backup data can be stored in cloud capacity</span><span class="sxs-lookup"><span data-stu-id="41af5-176">Secondary copy of backup data can be stored in cloud capacity</span></span>  | <span data-ttu-id="41af5-177">N/A</span><span class="sxs-lookup"><span data-stu-id="41af5-177">N/A</span></span>  |

## <a name="storsimple-as-a-primary-backup-target"></a><span data-ttu-id="41af5-178">StorSimple as a primary backup target</span><span class="sxs-lookup"><span data-stu-id="41af5-178">StorSimple as a primary backup target</span></span>

<span data-ttu-id="41af5-179">In this scenario, StorSimple volumes are presented to the backup application as the sole repository for backups.</span><span class="sxs-lookup"><span data-stu-id="41af5-179">In this scenario, StorSimple volumes are presented to the backup application as the sole repository for backups.</span></span> <span data-ttu-id="41af5-180">The following figure shows a solution architecture in which all backups use StorSimple tiered volumes for backups and restores.</span><span class="sxs-lookup"><span data-stu-id="41af5-180">The following figure shows a solution architecture in which all backups use StorSimple tiered volumes for backups and restores.</span></span>

![StorSimple as a primary backup target logical diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a><span data-ttu-id="41af5-182">Primary target backup logical steps</span><span class="sxs-lookup"><span data-stu-id="41af5-182">Primary target backup logical steps</span></span>

1.  <span data-ttu-id="41af5-183">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span><span class="sxs-lookup"><span data-stu-id="41af5-183">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span></span>
2.  <span data-ttu-id="41af5-184">The backup server writes data to the StorSimple tiered volumes.</span><span class="sxs-lookup"><span data-stu-id="41af5-184">The backup server writes data to the StorSimple tiered volumes.</span></span>
3.  <span data-ttu-id="41af5-185">The backup server updates the catalog database, and then finishes the backup job.</span><span class="sxs-lookup"><span data-stu-id="41af5-185">The backup server updates the catalog database, and then finishes the backup job.</span></span>
4.  <span data-ttu-id="41af5-186">A snapshot script triggers the StorSimple snapshot manager (start or delete).</span><span class="sxs-lookup"><span data-stu-id="41af5-186">A snapshot script triggers the StorSimple snapshot manager (start or delete).</span></span>
5.  <span data-ttu-id="41af5-187">The backup server deletes expired backups based on a retention policy.</span><span class="sxs-lookup"><span data-stu-id="41af5-187">The backup server deletes expired backups based on a retention policy.</span></span>

### <a name="primary-target-restore-logical-steps"></a><span data-ttu-id="41af5-188">Primary target restore logical steps</span><span class="sxs-lookup"><span data-stu-id="41af5-188">Primary target restore logical steps</span></span>

1.  <span data-ttu-id="41af5-189">The backup server starts restoring the appropriate data from the storage repository.</span><span class="sxs-lookup"><span data-stu-id="41af5-189">The backup server starts restoring the appropriate data from the storage repository.</span></span>
2.  <span data-ttu-id="41af5-190">The backup agent receives the data from the backup server.</span><span class="sxs-lookup"><span data-stu-id="41af5-190">The backup agent receives the data from the backup server.</span></span>
3.  <span data-ttu-id="41af5-191">The backup server finishes the restore job.</span><span class="sxs-lookup"><span data-stu-id="41af5-191">The backup server finishes the restore job.</span></span>

## <a name="storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="41af5-192">StorSimple as a secondary backup target</span><span class="sxs-lookup"><span data-stu-id="41af5-192">StorSimple as a secondary backup target</span></span>

<span data-ttu-id="41af5-193">In this scenario, StorSimple volumes primarily are used for long-term retention or archiving.</span><span class="sxs-lookup"><span data-stu-id="41af5-193">In this scenario, StorSimple volumes primarily are used for long-term retention or archiving.</span></span>

<span data-ttu-id="41af5-194">The following figure shows an architecture in which initial backups and restores target a high-performance volume.</span><span class="sxs-lookup"><span data-stu-id="41af5-194">The following figure shows an architecture in which initial backups and restores target a high-performance volume.</span></span> <span data-ttu-id="41af5-195">These backups are copied and archived to a StorSimple tiered volume on a set schedule.</span><span class="sxs-lookup"><span data-stu-id="41af5-195">These backups are copied and archived to a StorSimple tiered volume on a set schedule.</span></span>

<span data-ttu-id="41af5-196">It's important to size your high-performance volume so that it can handle your retention policy capacity and performance requirements.</span><span class="sxs-lookup"><span data-stu-id="41af5-196">It's important to size your high-performance volume so that it can handle your retention policy capacity and performance requirements.</span></span>

![StorSimple as a secondary backup target logical diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a><span data-ttu-id="41af5-198">Secondary target backup logical steps</span><span class="sxs-lookup"><span data-stu-id="41af5-198">Secondary target backup logical steps</span></span>

1.  <span data-ttu-id="41af5-199">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span><span class="sxs-lookup"><span data-stu-id="41af5-199">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span></span>
2.  <span data-ttu-id="41af5-200">The backup server writes data to high-performance storage.</span><span class="sxs-lookup"><span data-stu-id="41af5-200">The backup server writes data to high-performance storage.</span></span>
3.  <span data-ttu-id="41af5-201">The backup server updates the catalog database, and then finishes the backup job.</span><span class="sxs-lookup"><span data-stu-id="41af5-201">The backup server updates the catalog database, and then finishes the backup job.</span></span>
4.  <span data-ttu-id="41af5-202">The backup server copies backups to StorSimple based on a retention policy.</span><span class="sxs-lookup"><span data-stu-id="41af5-202">The backup server copies backups to StorSimple based on a retention policy.</span></span>
5.  <span data-ttu-id="41af5-203">A snapshot script triggers the StorSimple snapshot manager (start or delete).</span><span class="sxs-lookup"><span data-stu-id="41af5-203">A snapshot script triggers the StorSimple snapshot manager (start or delete).</span></span>
6.  <span data-ttu-id="41af5-204">The backup server deletes the expired backups based on a retention policy.</span><span class="sxs-lookup"><span data-stu-id="41af5-204">The backup server deletes the expired backups based on a retention policy.</span></span>

### <a name="secondary-target-restore-logical-steps"></a><span data-ttu-id="41af5-205">Secondary target restore logical steps</span><span class="sxs-lookup"><span data-stu-id="41af5-205">Secondary target restore logical steps</span></span>

1.  <span data-ttu-id="41af5-206">The backup server starts restoring the appropriate data from the storage repository.</span><span class="sxs-lookup"><span data-stu-id="41af5-206">The backup server starts restoring the appropriate data from the storage repository.</span></span>
2.  <span data-ttu-id="41af5-207">The backup agent receives the data from the backup server.</span><span class="sxs-lookup"><span data-stu-id="41af5-207">The backup agent receives the data from the backup server.</span></span>
3.  <span data-ttu-id="41af5-208">The backup server finishes the restore job.</span><span class="sxs-lookup"><span data-stu-id="41af5-208">The backup server finishes the restore job.</span></span>

## <a name="deploy-the-solution"></a><span data-ttu-id="41af5-209">Deploy the solution</span><span class="sxs-lookup"><span data-stu-id="41af5-209">Deploy the solution</span></span>

<span data-ttu-id="41af5-210">Deploying this solution requires three steps:</span><span class="sxs-lookup"><span data-stu-id="41af5-210">Deploying this solution requires three steps:</span></span>
1. <span data-ttu-id="41af5-211">Prepare the network infrastructure.</span><span class="sxs-lookup"><span data-stu-id="41af5-211">Prepare the network infrastructure.</span></span>
2. <span data-ttu-id="41af5-212">Deploy your StorSimple device as a backup target.</span><span class="sxs-lookup"><span data-stu-id="41af5-212">Deploy your StorSimple device as a backup target.</span></span>
3. <span data-ttu-id="41af5-213">Deploy Veritas NetBackup.</span><span class="sxs-lookup"><span data-stu-id="41af5-213">Deploy Veritas NetBackup.</span></span>

<span data-ttu-id="41af5-214">Each step is discussed in detail in the following sections.</span><span class="sxs-lookup"><span data-stu-id="41af5-214">Each step is discussed in detail in the following sections.</span></span>

### <a name="set-up-the-network"></a><span data-ttu-id="41af5-215">Set up the network</span><span class="sxs-lookup"><span data-stu-id="41af5-215">Set up the network</span></span>

<span data-ttu-id="41af5-216">Because StorSimple is a solution that's integrated with the Azure cloud, StorSimple requires an active and working connection to the Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="41af5-216">Because StorSimple is a solution that's integrated with the Azure cloud, StorSimple requires an active and working connection to the Azure cloud.</span></span> <span data-ttu-id="41af5-217">This connection is used for operations like cloud snapshots, data management, and metadata transfer, and to tier older, less accessed data to Azure cloud storage.</span><span class="sxs-lookup"><span data-stu-id="41af5-217">This connection is used for operations like cloud snapshots, data management, and metadata transfer, and to tier older, less accessed data to Azure cloud storage.</span></span>

<span data-ttu-id="41af5-218">For the solution to perform optimally, we recommend that you follow these networking best practices:</span><span class="sxs-lookup"><span data-stu-id="41af5-218">For the solution to perform optimally, we recommend that you follow these networking best practices:</span></span>

-   <span data-ttu-id="41af5-219">The link that connects the StorSimple tiering to Azure must meet your bandwidth requirements.</span><span class="sxs-lookup"><span data-stu-id="41af5-219">The link that connects the StorSimple tiering to Azure must meet your bandwidth requirements.</span></span> <span data-ttu-id="41af5-220">To achieve this, apply the proper Quality of Service (QoS) level to your infrastructure switches to match your RPO and recovery time objective (RTO) SLAs.</span><span class="sxs-lookup"><span data-stu-id="41af5-220">To achieve this, apply the proper Quality of Service (QoS) level to your infrastructure switches to match your RPO and recovery time objective (RTO) SLAs.</span></span>

-   <span data-ttu-id="41af5-221">Maximum Azure Blob storage access latencies should be around 80 ms.</span><span class="sxs-lookup"><span data-stu-id="41af5-221">Maximum Azure Blob storage access latencies should be around 80 ms.</span></span>

### <a name="deploy-storsimple"></a><span data-ttu-id="41af5-222">Deploy StorSimple</span><span class="sxs-lookup"><span data-stu-id="41af5-222">Deploy StorSimple</span></span>

<span data-ttu-id="41af5-223">For step-by-step StorSimple deployment guidance, see [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span><span class="sxs-lookup"><span data-stu-id="41af5-223">For step-by-step StorSimple deployment guidance, see [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span></span>

### <a name="deploy-netbackup"></a><span data-ttu-id="41af5-224">Deploy NetBackup</span><span class="sxs-lookup"><span data-stu-id="41af5-224">Deploy NetBackup</span></span>

<span data-ttu-id="41af5-225">For step-by-step NetBackup 7.7.x deployment guidance, see the [NetBackup 7.7.x documentation](http://www.veritas.com/docs/000094423).</span><span class="sxs-lookup"><span data-stu-id="41af5-225">For step-by-step NetBackup 7.7.x deployment guidance, see the [NetBackup 7.7.x documentation](http://www.veritas.com/docs/000094423).</span></span>

## <a name="set-up-the-solution"></a><span data-ttu-id="41af5-226">Set up the solution</span><span class="sxs-lookup"><span data-stu-id="41af5-226">Set up the solution</span></span>

<span data-ttu-id="41af5-227">In this section, we demonstrate some configuration examples.</span><span class="sxs-lookup"><span data-stu-id="41af5-227">In this section, we demonstrate some configuration examples.</span></span> <span data-ttu-id="41af5-228">The following examples and recommendations illustrate the most basic and fundamental implementation.</span><span class="sxs-lookup"><span data-stu-id="41af5-228">The following examples and recommendations illustrate the most basic and fundamental implementation.</span></span> <span data-ttu-id="41af5-229">This implementation might not apply directly to your specific backup requirements.</span><span class="sxs-lookup"><span data-stu-id="41af5-229">This implementation might not apply directly to your specific backup requirements.</span></span>

### <a name="set-up-storsimple"></a><span data-ttu-id="41af5-230">Set up StorSimple</span><span class="sxs-lookup"><span data-stu-id="41af5-230">Set up StorSimple</span></span>

| <span data-ttu-id="41af5-231">StorSimple deployment tasks</span><span class="sxs-lookup"><span data-stu-id="41af5-231">StorSimple deployment tasks</span></span>  | <span data-ttu-id="41af5-232">Additional comments</span><span class="sxs-lookup"><span data-stu-id="41af5-232">Additional comments</span></span> |
|---|---|
| <span data-ttu-id="41af5-233">Deploy your on-premises StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="41af5-233">Deploy your on-premises StorSimple device.</span></span> | <span data-ttu-id="41af5-234">Supported versions: Update 3 and later versions.</span><span class="sxs-lookup"><span data-stu-id="41af5-234">Supported versions: Update 3 and later versions.</span></span> |
| <span data-ttu-id="41af5-235">Turn on the backup target.</span><span class="sxs-lookup"><span data-stu-id="41af5-235">Turn on the backup target.</span></span> | <span data-ttu-id="41af5-236">Use these commands to turn on or turn off backup target mode, and to get status.</span><span class="sxs-lookup"><span data-stu-id="41af5-236">Use these commands to turn on or turn off backup target mode, and to get status.</span></span> <span data-ttu-id="41af5-237">For more information, see [Connect remotely to a StorSimple device](storsimple-remote-connect.md).</span><span class="sxs-lookup"><span data-stu-id="41af5-237">For more information, see [Connect remotely to a StorSimple device](storsimple-remote-connect.md).</span></span></br> <span data-ttu-id="41af5-238">To turn on backup mode: `Set-HCSBackupApplianceMode -enable`.</span><span class="sxs-lookup"><span data-stu-id="41af5-238">To turn on backup mode: `Set-HCSBackupApplianceMode -enable`.</span></span> </br> <span data-ttu-id="41af5-239">To turn off backup mode: `Set-HCSBackupApplianceMode -disable`.</span><span class="sxs-lookup"><span data-stu-id="41af5-239">To turn off backup mode: `Set-HCSBackupApplianceMode -disable`.</span></span> </br> <span data-ttu-id="41af5-240">To get the current state of backup mode settings: `Get-HCSBackupApplianceMode`.</span><span class="sxs-lookup"><span data-stu-id="41af5-240">To get the current state of backup mode settings: `Get-HCSBackupApplianceMode`.</span></span> |
| <span data-ttu-id="41af5-241">Create a common volume container for your volume that stores the backup data.</span><span class="sxs-lookup"><span data-stu-id="41af5-241">Create a common volume container for your volume that stores the backup data.</span></span> <span data-ttu-id="41af5-242">All data in a volume container is deduplicated.</span><span class="sxs-lookup"><span data-stu-id="41af5-242">All data in a volume container is deduplicated.</span></span> | <span data-ttu-id="41af5-243">StorSimple volume containers define deduplication domains.</span><span class="sxs-lookup"><span data-stu-id="41af5-243">StorSimple volume containers define deduplication domains.</span></span>  |
| <span data-ttu-id="41af5-244">Create StorSimple volumes.</span><span class="sxs-lookup"><span data-stu-id="41af5-244">Create StorSimple volumes.</span></span> | <span data-ttu-id="41af5-245">Create volumes with sizes as close to the anticipated usage as possible, because volume size affects cloud snapshot duration time.</span><span class="sxs-lookup"><span data-stu-id="41af5-245">Create volumes with sizes as close to the anticipated usage as possible, because volume size affects cloud snapshot duration time.</span></span> <span data-ttu-id="41af5-246">For information about how to size a volume, read about [retention policies](#retention-policies).</span><span class="sxs-lookup"><span data-stu-id="41af5-246">For information about how to size a volume, read about [retention policies](#retention-policies).</span></span></br> </br> <span data-ttu-id="41af5-247">Use StorSimple tiered volumes, and select the **Use this volume for less frequently accessed archival data** check box.</span><span class="sxs-lookup"><span data-stu-id="41af5-247">Use StorSimple tiered volumes, and select the **Use this volume for less frequently accessed archival data** check box.</span></span> </br> <span data-ttu-id="41af5-248">Using only locally pinned volumes is not supported.</span><span class="sxs-lookup"><span data-stu-id="41af5-248">Using only locally pinned volumes is not supported.</span></span> |
| <span data-ttu-id="41af5-249">Create a unique StorSimple backup policy for all the backup target volumes.</span><span class="sxs-lookup"><span data-stu-id="41af5-249">Create a unique StorSimple backup policy for all the backup target volumes.</span></span> | <span data-ttu-id="41af5-250">A StorSimple backup policy defines the volume consistency group.</span><span class="sxs-lookup"><span data-stu-id="41af5-250">A StorSimple backup policy defines the volume consistency group.</span></span> |
| <span data-ttu-id="41af5-251">Disable the schedule as the snapshots expire.</span><span class="sxs-lookup"><span data-stu-id="41af5-251">Disable the schedule as the snapshots expire.</span></span> | <span data-ttu-id="41af5-252">Snapshots are triggered as a post-processing operation.</span><span class="sxs-lookup"><span data-stu-id="41af5-252">Snapshots are triggered as a post-processing operation.</span></span> |

### <a name="set-up-the-host-backup-server-storage"></a><span data-ttu-id="41af5-253">Set up the host backup server storage</span><span class="sxs-lookup"><span data-stu-id="41af5-253">Set up the host backup server storage</span></span>

<span data-ttu-id="41af5-254">Set up the host backup server storage according to these guidelines:</span><span class="sxs-lookup"><span data-stu-id="41af5-254">Set up the host backup server storage according to these guidelines:</span></span>  

- <span data-ttu-id="41af5-255">Don't use spanned volumes (created by Windows Disk Management); spanned volumes are not supported.</span><span class="sxs-lookup"><span data-stu-id="41af5-255">Don't use spanned volumes (created by Windows Disk Management); spanned volumes are not supported.</span></span>
- <span data-ttu-id="41af5-256">Format your volumes using NTFS with 64-KB allocation size.</span><span class="sxs-lookup"><span data-stu-id="41af5-256">Format your volumes using NTFS with 64-KB allocation size.</span></span>
- <span data-ttu-id="41af5-257">Map the StorSimple volumes directly to the NetBackup server.</span><span class="sxs-lookup"><span data-stu-id="41af5-257">Map the StorSimple volumes directly to the NetBackup server.</span></span>
    - <span data-ttu-id="41af5-258">Use iSCSI for physical servers.</span><span class="sxs-lookup"><span data-stu-id="41af5-258">Use iSCSI for physical servers.</span></span>
    - <span data-ttu-id="41af5-259">Use pass-through disks for virtual servers.</span><span class="sxs-lookup"><span data-stu-id="41af5-259">Use pass-through disks for virtual servers.</span></span>


## <a name="best-practices-for-storsimple-and-netbackup"></a><span data-ttu-id="41af5-260">Best practices for StorSimple and NetBackup</span><span class="sxs-lookup"><span data-stu-id="41af5-260">Best practices for StorSimple and NetBackup</span></span>

<span data-ttu-id="41af5-261">Set up your solution according to the guidelines in the following few sections.</span><span class="sxs-lookup"><span data-stu-id="41af5-261">Set up your solution according to the guidelines in the following few sections.</span></span>

### <a name="operating-system-best-practices"></a><span data-ttu-id="41af5-262">Operating system best practices</span><span class="sxs-lookup"><span data-stu-id="41af5-262">Operating system best practices</span></span>

-   <span data-ttu-id="41af5-263">Disable Windows Server encryption and deduplication for the NTFS file system.</span><span class="sxs-lookup"><span data-stu-id="41af5-263">Disable Windows Server encryption and deduplication for the NTFS file system.</span></span>
-   <span data-ttu-id="41af5-264">Disable Windows Server defragmentation on the StorSimple volumes.</span><span class="sxs-lookup"><span data-stu-id="41af5-264">Disable Windows Server defragmentation on the StorSimple volumes.</span></span>
-   <span data-ttu-id="41af5-265">Disable Windows Server indexing on the StorSimple volumes.</span><span class="sxs-lookup"><span data-stu-id="41af5-265">Disable Windows Server indexing on the StorSimple volumes.</span></span>
-   <span data-ttu-id="41af5-266">Run an antivirus scan at the source host (not against the StorSimple volumes).</span><span class="sxs-lookup"><span data-stu-id="41af5-266">Run an antivirus scan at the source host (not against the StorSimple volumes).</span></span>
-   <span data-ttu-id="41af5-267">Turn off the default [Windows Server maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) in Task Manager.</span><span class="sxs-lookup"><span data-stu-id="41af5-267">Turn off the default [Windows Server maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) in Task Manager.</span></span> <span data-ttu-id="41af5-268">Do this in one of the following ways:</span><span class="sxs-lookup"><span data-stu-id="41af5-268">Do this in one of the following ways:</span></span>
    - <span data-ttu-id="41af5-269">Turn off the Maintenance configurator in Windows Task Scheduler.</span><span class="sxs-lookup"><span data-stu-id="41af5-269">Turn off the Maintenance configurator in Windows Task Scheduler.</span></span>
    - <span data-ttu-id="41af5-270">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) from Windows Sysinternals.</span><span class="sxs-lookup"><span data-stu-id="41af5-270">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) from Windows Sysinternals.</span></span> <span data-ttu-id="41af5-271">After you download PsExec, run Windows PowerShell as an administrator, and type:</span><span class="sxs-lookup"><span data-stu-id="41af5-271">After you download PsExec, run Windows PowerShell as an administrator, and type:</span></span>
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a><span data-ttu-id="41af5-272">StorSimple best practices</span><span class="sxs-lookup"><span data-stu-id="41af5-272">StorSimple best practices</span></span>

-   <span data-ttu-id="41af5-273">Be sure that the StorSimple device is updated to [Update 3 or later](storsimple-install-update-3.md).</span><span class="sxs-lookup"><span data-stu-id="41af5-273">Be sure that the StorSimple device is updated to [Update 3 or later](storsimple-install-update-3.md).</span></span>
-   <span data-ttu-id="41af5-274">Isolate iSCSI and cloud traffic.</span><span class="sxs-lookup"><span data-stu-id="41af5-274">Isolate iSCSI and cloud traffic.</span></span> <span data-ttu-id="41af5-275">Use dedicated iSCSI connections for traffic between StorSimple and the backup server.</span><span class="sxs-lookup"><span data-stu-id="41af5-275">Use dedicated iSCSI connections for traffic between StorSimple and the backup server.</span></span>
-   <span data-ttu-id="41af5-276">Be sure that your StorSimple device is a dedicated backup target.</span><span class="sxs-lookup"><span data-stu-id="41af5-276">Be sure that your StorSimple device is a dedicated backup target.</span></span> <span data-ttu-id="41af5-277">Mixed workloads are not supported because they affect your RTO and RPO.</span><span class="sxs-lookup"><span data-stu-id="41af5-277">Mixed workloads are not supported because they affect your RTO and RPO.</span></span>

### <a name="netbackup-best-practices"></a><span data-ttu-id="41af5-278">NetBackup best practices</span><span class="sxs-lookup"><span data-stu-id="41af5-278">NetBackup best practices</span></span>

-   <span data-ttu-id="41af5-279">The NetBackup database should be local to the server and not reside on a StorSimple volume.</span><span class="sxs-lookup"><span data-stu-id="41af5-279">The NetBackup database should be local to the server and not reside on a StorSimple volume.</span></span>
-   <span data-ttu-id="41af5-280">For disaster recovery, back up the NetBackup database on a StorSimple volume.</span><span class="sxs-lookup"><span data-stu-id="41af5-280">For disaster recovery, back up the NetBackup database on a StorSimple volume.</span></span>
-   <span data-ttu-id="41af5-281">We support NetBackup full and incremental backups for this solution.</span><span class="sxs-lookup"><span data-stu-id="41af5-281">We support NetBackup full and incremental backups for this solution.</span></span> <span data-ttu-id="41af5-282">We recommend that you do not use synthetic and differential backups.</span><span class="sxs-lookup"><span data-stu-id="41af5-282">We recommend that you do not use synthetic and differential backups.</span></span>
-   <span data-ttu-id="41af5-283">Backup data files should contain only the data for a specific job.</span><span class="sxs-lookup"><span data-stu-id="41af5-283">Backup data files should contain only the data for a specific job.</span></span> <span data-ttu-id="41af5-284">For example, no media appends across different jobs are allowed.</span><span class="sxs-lookup"><span data-stu-id="41af5-284">For example, no media appends across different jobs are allowed.</span></span>

<span data-ttu-id="41af5-285">For the latest NetBackup settings and best practices for implementing these requirements, see the NetBackup documentation at [www.veritas.com](https://www.veritas.com).</span><span class="sxs-lookup"><span data-stu-id="41af5-285">For the latest NetBackup settings and best practices for implementing these requirements, see the NetBackup documentation at [www.veritas.com](https://www.veritas.com).</span></span>


## <a name="retention-policies"></a><span data-ttu-id="41af5-286">Retention policies</span><span class="sxs-lookup"><span data-stu-id="41af5-286">Retention policies</span></span>

<span data-ttu-id="41af5-287">One of the most common backup retention policy types is a Grandfather, Father, and Son (GFS) policy.</span><span class="sxs-lookup"><span data-stu-id="41af5-287">One of the most common backup retention policy types is a Grandfather, Father, and Son (GFS) policy.</span></span> <span data-ttu-id="41af5-288">In a GFS policy, an incremental backup is performed daily and full backups are done weekly and monthly.</span><span class="sxs-lookup"><span data-stu-id="41af5-288">In a GFS policy, an incremental backup is performed daily and full backups are done weekly and monthly.</span></span> <span data-ttu-id="41af5-289">This policy results in six StorSimple tiered volumes: one volume contains the weekly, monthly, and yearly full backups; the other five volumes store daily incremental backups.</span><span class="sxs-lookup"><span data-stu-id="41af5-289">This policy results in six StorSimple tiered volumes: one volume contains the weekly, monthly, and yearly full backups; the other five volumes store daily incremental backups.</span></span>

<span data-ttu-id="41af5-290">In the following example, we use a GFS rotation.</span><span class="sxs-lookup"><span data-stu-id="41af5-290">In the following example, we use a GFS rotation.</span></span> <span data-ttu-id="41af5-291">The example assumes the following:</span><span class="sxs-lookup"><span data-stu-id="41af5-291">The example assumes the following:</span></span>

-   <span data-ttu-id="41af5-292">Non-deduped or compressed data is used.</span><span class="sxs-lookup"><span data-stu-id="41af5-292">Non-deduped or compressed data is used.</span></span>
-   <span data-ttu-id="41af5-293">Full backups are 1 TiB each.</span><span class="sxs-lookup"><span data-stu-id="41af5-293">Full backups are 1 TiB each.</span></span>
-   <span data-ttu-id="41af5-294">Daily incremental backups are 500 GiB each.</span><span class="sxs-lookup"><span data-stu-id="41af5-294">Daily incremental backups are 500 GiB each.</span></span>
-   <span data-ttu-id="41af5-295">Four weekly backups are kept for a month.</span><span class="sxs-lookup"><span data-stu-id="41af5-295">Four weekly backups are kept for a month.</span></span>
-   <span data-ttu-id="41af5-296">Twelve monthly backups are kept for a year.</span><span class="sxs-lookup"><span data-stu-id="41af5-296">Twelve monthly backups are kept for a year.</span></span>
-   <span data-ttu-id="41af5-297">One yearly backup is kept for 10 years.</span><span class="sxs-lookup"><span data-stu-id="41af5-297">One yearly backup is kept for 10 years.</span></span>

<span data-ttu-id="41af5-298">Based on the preceding assumptions, create a 26-TiB StorSimple tiered volume for the monthly and yearly full backups.</span><span class="sxs-lookup"><span data-stu-id="41af5-298">Based on the preceding assumptions, create a 26-TiB StorSimple tiered volume for the monthly and yearly full backups.</span></span> <span data-ttu-id="41af5-299">Create a 5-TiB StorSimple tiered volume for each of the incremental daily backups.</span><span class="sxs-lookup"><span data-stu-id="41af5-299">Create a 5-TiB StorSimple tiered volume for each of the incremental daily backups.</span></span>

| <span data-ttu-id="41af5-300">Backup type retention</span><span class="sxs-lookup"><span data-stu-id="41af5-300">Backup type retention</span></span> | <span data-ttu-id="41af5-301">Size (TiB)</span><span class="sxs-lookup"><span data-stu-id="41af5-301">Size (TiB)</span></span> | <span data-ttu-id="41af5-302">GFS multiplier\*</span><span class="sxs-lookup"><span data-stu-id="41af5-302">GFS multiplier\*</span></span> | <span data-ttu-id="41af5-303">Total capacity (TiB)</span><span class="sxs-lookup"><span data-stu-id="41af5-303">Total capacity (TiB)</span></span>  |
|---|---|---|---|
| <span data-ttu-id="41af5-304">Weekly full</span><span class="sxs-lookup"><span data-stu-id="41af5-304">Weekly full</span></span> | <span data-ttu-id="41af5-305">1</span><span class="sxs-lookup"><span data-stu-id="41af5-305">1</span></span> | <span data-ttu-id="41af5-306">4</span><span class="sxs-lookup"><span data-stu-id="41af5-306">4</span></span>  | <span data-ttu-id="41af5-307">4</span><span class="sxs-lookup"><span data-stu-id="41af5-307">4</span></span> |
| <span data-ttu-id="41af5-308">Daily incremental</span><span class="sxs-lookup"><span data-stu-id="41af5-308">Daily incremental</span></span> | <span data-ttu-id="41af5-309">0.5</span><span class="sxs-lookup"><span data-stu-id="41af5-309">0.5</span></span> | <span data-ttu-id="41af5-310">20 (cycles equal number of weeks per month)</span><span class="sxs-lookup"><span data-stu-id="41af5-310">20 (cycles equal number of weeks per month)</span></span> | <span data-ttu-id="41af5-311">12 (2 for additional quota)</span><span class="sxs-lookup"><span data-stu-id="41af5-311">12 (2 for additional quota)</span></span> |
| <span data-ttu-id="41af5-312">Monthly full</span><span class="sxs-lookup"><span data-stu-id="41af5-312">Monthly full</span></span> | <span data-ttu-id="41af5-313">1</span><span class="sxs-lookup"><span data-stu-id="41af5-313">1</span></span> | <span data-ttu-id="41af5-314">12</span><span class="sxs-lookup"><span data-stu-id="41af5-314">12</span></span> | <span data-ttu-id="41af5-315">12</span><span class="sxs-lookup"><span data-stu-id="41af5-315">12</span></span> |
| <span data-ttu-id="41af5-316">Yearly full</span><span class="sxs-lookup"><span data-stu-id="41af5-316">Yearly full</span></span> | <span data-ttu-id="41af5-317">1</span><span class="sxs-lookup"><span data-stu-id="41af5-317">1</span></span>  | <span data-ttu-id="41af5-318">10</span><span class="sxs-lookup"><span data-stu-id="41af5-318">10</span></span> | <span data-ttu-id="41af5-319">10</span><span class="sxs-lookup"><span data-stu-id="41af5-319">10</span></span> |
| <span data-ttu-id="41af5-320">GFS requirement</span><span class="sxs-lookup"><span data-stu-id="41af5-320">GFS requirement</span></span> |   | <span data-ttu-id="41af5-321">38</span><span class="sxs-lookup"><span data-stu-id="41af5-321">38</span></span> |   |
| <span data-ttu-id="41af5-322">Additional quota</span><span class="sxs-lookup"><span data-stu-id="41af5-322">Additional quota</span></span>  | <span data-ttu-id="41af5-323">4</span><span class="sxs-lookup"><span data-stu-id="41af5-323">4</span></span>  |   | <span data-ttu-id="41af5-324">42 total GFS requirement</span><span class="sxs-lookup"><span data-stu-id="41af5-324">42 total GFS requirement</span></span>  |
<span data-ttu-id="41af5-325">\* The GFS multiplier is the number of copies you need to protect and retain to meet your backup policy requirements.</span><span class="sxs-lookup"><span data-stu-id="41af5-325">\* The GFS multiplier is the number of copies you need to protect and retain to meet your backup policy requirements.</span></span>

## <a name="set-up-netbackup-storage"></a><span data-ttu-id="41af5-326">Set up NetBackup storage</span><span class="sxs-lookup"><span data-stu-id="41af5-326">Set up NetBackup storage</span></span>

### <a name="to-set-up-netbackup-storage"></a><span data-ttu-id="41af5-327">To set up NetBackup storage</span><span class="sxs-lookup"><span data-stu-id="41af5-327">To set up NetBackup storage</span></span>

1.  <span data-ttu-id="41af5-328">In the NetBackup Administration Console, select **Media and Device Management** > **Devices** > **Disk Pools**.</span><span class="sxs-lookup"><span data-stu-id="41af5-328">In the NetBackup Administration Console, select **Media and Device Management** > **Devices** > **Disk Pools**.</span></span> <span data-ttu-id="41af5-329">In the Disk Pool Configuration Wizard, select the storage server type **AdvancedDisk**, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="41af5-329">In the Disk Pool Configuration Wizard, select the storage server type **AdvancedDisk**, and then select **Next**.</span></span>

    ![NetBackup Administration Console, Disk Pool Configuration Wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage1.png)

2.  <span data-ttu-id="41af5-331">Select your server, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="41af5-331">Select your server, and then select **Next**.</span></span>

    ![NetBackup Administration Console, select the server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage2.png)

3.  <span data-ttu-id="41af5-333">Select your StorSimple volume.</span><span class="sxs-lookup"><span data-stu-id="41af5-333">Select your StorSimple volume.</span></span>

    ![NetBackup Administration Console, select the StorSimple volume disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage3.png)

4.  <span data-ttu-id="41af5-335">Enter a name for the backup target, and then select **Next** > **Next** to finish the wizard.</span><span class="sxs-lookup"><span data-stu-id="41af5-335">Enter a name for the backup target, and then select **Next** > **Next** to finish the wizard.</span></span>

5.  <span data-ttu-id="41af5-336">Review the settings, and then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="41af5-336">Review the settings, and then select **Finish**.</span></span>

6.  <span data-ttu-id="41af5-337">At the end of each volume assignment, change the storage device settings to match those recommended in [Best practices for StorSimple and NetBackup](#best-practices-for-storsimple-and-netbackup).</span><span class="sxs-lookup"><span data-stu-id="41af5-337">At the end of each volume assignment, change the storage device settings to match those recommended in [Best practices for StorSimple and NetBackup](#best-practices-for-storsimple-and-netbackup).</span></span>

7. <span data-ttu-id="41af5-338">Repeat steps 1-6 until you are finished assigning your StorSimple volumes.</span><span class="sxs-lookup"><span data-stu-id="41af5-338">Repeat steps 1-6 until you are finished assigning your StorSimple volumes.</span></span>

    ![NetBackup Administration Console, disk configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage5.png)

## <a name="set-up-storsimple-as-a-primary-backup-target"></a><span data-ttu-id="41af5-340">Set up StorSimple as a primary backup target</span><span class="sxs-lookup"><span data-stu-id="41af5-340">Set up StorSimple as a primary backup target</span></span>

> [!NOTE]
> <span data-ttu-id="41af5-341">Data restores from a backup that has been tiered to the cloud occur at cloud speeds.</span><span class="sxs-lookup"><span data-stu-id="41af5-341">Data restores from a backup that has been tiered to the cloud occur at cloud speeds.</span></span>

<span data-ttu-id="41af5-342">The following figure shows the mapping of a typical volume to a backup job.</span><span class="sxs-lookup"><span data-stu-id="41af5-342">The following figure shows the mapping of a typical volume to a backup job.</span></span> <span data-ttu-id="41af5-343">In this case, all the weekly backups map to the Saturday full disk, and the incremental backups map to Monday-Friday incremental disks.</span><span class="sxs-lookup"><span data-stu-id="41af5-343">In this case, all the weekly backups map to the Saturday full disk, and the incremental backups map to Monday-Friday incremental disks.</span></span> <span data-ttu-id="41af5-344">All the backups and restores are from a StorSimple tiered volume.</span><span class="sxs-lookup"><span data-stu-id="41af5-344">All the backups and restores are from a StorSimple tiered volume.</span></span>

![<span data-ttu-id="41af5-345">Primary backup target configuration logical diagram</span><span class="sxs-lookup"><span data-stu-id="41af5-345">Primary backup target configuration logical diagram</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a><span data-ttu-id="41af5-346">StorSimple as a primary backup target GFS schedule example</span><span class="sxs-lookup"><span data-stu-id="41af5-346">StorSimple as a primary backup target GFS schedule example</span></span>

<span data-ttu-id="41af5-347">Here's an example of a GFS rotation schedule for four weeks, monthly, and yearly:</span><span class="sxs-lookup"><span data-stu-id="41af5-347">Here's an example of a GFS rotation schedule for four weeks, monthly, and yearly:</span></span>

| <span data-ttu-id="41af5-348">Frequency/backup type</span><span class="sxs-lookup"><span data-stu-id="41af5-348">Frequency/backup type</span></span> | <span data-ttu-id="41af5-349">Full</span><span class="sxs-lookup"><span data-stu-id="41af5-349">Full</span></span> | <span data-ttu-id="41af5-350">Incremental (days 1-5)</span><span class="sxs-lookup"><span data-stu-id="41af5-350">Incremental (days 1-5)</span></span>  |   
|---|---|---|
| <span data-ttu-id="41af5-351">Weekly (weeks 1-4)</span><span class="sxs-lookup"><span data-stu-id="41af5-351">Weekly (weeks 1-4)</span></span> | <span data-ttu-id="41af5-352">Saturday</span><span class="sxs-lookup"><span data-stu-id="41af5-352">Saturday</span></span> | <span data-ttu-id="41af5-353">Monday-Friday</span><span class="sxs-lookup"><span data-stu-id="41af5-353">Monday-Friday</span></span> |
| <span data-ttu-id="41af5-354">Monthly</span><span class="sxs-lookup"><span data-stu-id="41af5-354">Monthly</span></span>  | <span data-ttu-id="41af5-355">Saturday</span><span class="sxs-lookup"><span data-stu-id="41af5-355">Saturday</span></span>  |   |
| <span data-ttu-id="41af5-356">Yearly</span><span class="sxs-lookup"><span data-stu-id="41af5-356">Yearly</span></span> | <span data-ttu-id="41af5-357">Saturday</span><span class="sxs-lookup"><span data-stu-id="41af5-357">Saturday</span></span>  |   |   |

## <a name="assigning-storsimple-volumes-to-a-netbackup-backup-job"></a><span data-ttu-id="41af5-358">Assigning StorSimple volumes to a NetBackup backup job</span><span class="sxs-lookup"><span data-stu-id="41af5-358">Assigning StorSimple volumes to a NetBackup backup job</span></span>

<span data-ttu-id="41af5-359">The following sequence assumes that NetBackup and the target host are configured in accordance with the NetBackup agent guidelines.</span><span class="sxs-lookup"><span data-stu-id="41af5-359">The following sequence assumes that NetBackup and the target host are configured in accordance with the NetBackup agent guidelines.</span></span>

### <a name="to-assign-storsimple-volumes-to-a-netbackup-backup-job"></a><span data-ttu-id="41af5-360">To assign StorSimple volumes to a NetBackup backup job</span><span class="sxs-lookup"><span data-stu-id="41af5-360">To assign StorSimple volumes to a NetBackup backup job</span></span>

1.  <span data-ttu-id="41af5-361">In the NetBackup Administration Console, select **NetBackup Management**, right-click **Policies**, and then select **New Policy**.</span><span class="sxs-lookup"><span data-stu-id="41af5-361">In the NetBackup Administration Console, select **NetBackup Management**, right-click **Policies**, and then select **New Policy**.</span></span>

    ![NetBackup Administration Console, create a new policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage6.png)

2.  <span data-ttu-id="41af5-363">In the **Add a New Policy** dialog box, enter a name for the policy, and then select the **Use Policy Configuration Wizard** check box.</span><span class="sxs-lookup"><span data-stu-id="41af5-363">In the **Add a New Policy** dialog box, enter a name for the policy, and then select the **Use Policy Configuration Wizard** check box.</span></span> <span data-ttu-id="41af5-364">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="41af5-364">Select **OK**.</span></span>

    ![NetBackup Administration Console, Add a New Policy dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage7.png)

3.  <span data-ttu-id="41af5-366">In the Backup Policy Configuration Wizard, elect the backup type you want, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="41af5-366">In the Backup Policy Configuration Wizard, elect the backup type you want, and then select **Next**.</span></span>

    ![NetBackup Administration Console, select backup type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage8.png)

4.  <span data-ttu-id="41af5-368">To set the policy type, select **Standard**, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="41af5-368">To set the policy type, select **Standard**, and then select **Next**.</span></span>

    ![NetBackup Administration Console, select policy type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage9.png)

5.  <span data-ttu-id="41af5-370">Select your host, select the **Detect client operating system** check box, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="41af5-370">Select your host, select the **Detect client operating system** check box, and then select **Add**.</span></span> <span data-ttu-id="41af5-371">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="41af5-371">Select **Next**.</span></span>

    ![NetBackup Administration Console, list clients in a new policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage10.png)

6.  <span data-ttu-id="41af5-373">Select the drives you want to back up.</span><span class="sxs-lookup"><span data-stu-id="41af5-373">Select the drives you want to back up.</span></span>

    ![NetBackup Administration Console, backup selections for a new policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage11.png)

7.  <span data-ttu-id="41af5-375">Select the frequency and retention values that meet your backup rotation requirements.</span><span class="sxs-lookup"><span data-stu-id="41af5-375">Select the frequency and retention values that meet your backup rotation requirements.</span></span>

    ![NetBackup Administration Console, backup frequency and rotation for a new policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage12.png)

8.  <span data-ttu-id="41af5-377">Select **Next** > **Next** > **Finish**.</span><span class="sxs-lookup"><span data-stu-id="41af5-377">Select **Next** > **Next** > **Finish**.</span></span>  <span data-ttu-id="41af5-378">You can modify the schedule after the policy is created.</span><span class="sxs-lookup"><span data-stu-id="41af5-378">You can modify the schedule after the policy is created.</span></span>

9.  <span data-ttu-id="41af5-379">Select to expand the policy you just created, and then select **Schedules**.</span><span class="sxs-lookup"><span data-stu-id="41af5-379">Select to expand the policy you just created, and then select **Schedules**.</span></span>

    ![NetBackup Administration Console, schedules for a new policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage13.png)

10.  <span data-ttu-id="41af5-381">Right-click **Differential-Inc**, select **Copy to new**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="41af5-381">Right-click **Differential-Inc**, select **Copy to new**, and then select **OK**.</span></span>

    ![NetBackup Administration Console, copy schedule to a new policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage14.png)

11.  <span data-ttu-id="41af5-383">Right-click the newly created schedule, and then select **Change**.</span><span class="sxs-lookup"><span data-stu-id="41af5-383">Right-click the newly created schedule, and then select **Change**.</span></span>

12.  <span data-ttu-id="41af5-384">On the **Attributes** tab, select the **Override policy storage selection** check box, and then select the volume where Monday incremental backups go.</span><span class="sxs-lookup"><span data-stu-id="41af5-384">On the **Attributes** tab, select the **Override policy storage selection** check box, and then select the volume where Monday incremental backups go.</span></span>

    ![NetBackup Administration Console, change schedule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage15.png)

13.  <span data-ttu-id="41af5-386">On the **Start Window** tab, select the time window for your backups.</span><span class="sxs-lookup"><span data-stu-id="41af5-386">On the **Start Window** tab, select the time window for your backups.</span></span>

    ![NetBackup Administration Console, change start window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage16.png)

14.  <span data-ttu-id="41af5-388">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="41af5-388">Select **OK**.</span></span>

15.  <span data-ttu-id="41af5-389">Repeat steps 10-14 for each incremental backup.</span><span class="sxs-lookup"><span data-stu-id="41af5-389">Repeat steps 10-14 for each incremental backup.</span></span> <span data-ttu-id="41af5-390">Select the appropriate volume and schedule for each backup you create.</span><span class="sxs-lookup"><span data-stu-id="41af5-390">Select the appropriate volume and schedule for each backup you create.</span></span>

16.  <span data-ttu-id="41af5-391">Right-click the **Differential-Inc** schedule, and then delete it.</span><span class="sxs-lookup"><span data-stu-id="41af5-391">Right-click the **Differential-Inc** schedule, and then delete it.</span></span>

17.  <span data-ttu-id="41af5-392">Modify your Full schedule to meet your backup needs.</span><span class="sxs-lookup"><span data-stu-id="41af5-392">Modify your Full schedule to meet your backup needs.</span></span>

    ![NetBackup Administration Console, change full schedule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage17.png)

18.  <span data-ttu-id="41af5-394">Change the start window.</span><span class="sxs-lookup"><span data-stu-id="41af5-394">Change the start window.</span></span>

    ![NetBackup Administration Console, change the start window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage18.png)

19.  <span data-ttu-id="41af5-396">The final schedule looks like this:</span><span class="sxs-lookup"><span data-stu-id="41af5-396">The final schedule looks like this:</span></span>

    ![NetBackup Administration Console, final schedule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage19.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="41af5-398">Set up StorSimple as a secondary backup target</span><span class="sxs-lookup"><span data-stu-id="41af5-398">Set up StorSimple as a secondary backup target</span></span>

> [!NOTE]
><span data-ttu-id="41af5-399">Data restores from a backup that has been tiered to the cloud occur at cloud speeds.</span><span class="sxs-lookup"><span data-stu-id="41af5-399">Data restores from a backup that has been tiered to the cloud occur at cloud speeds.</span></span>

<span data-ttu-id="41af5-400">In this model, you must have a storage media (other than StorSimple) to serve as a temporary cache.</span><span class="sxs-lookup"><span data-stu-id="41af5-400">In this model, you must have a storage media (other than StorSimple) to serve as a temporary cache.</span></span> <span data-ttu-id="41af5-401">For example, you can use a redundant array of independent disks (RAID) volume to accommodate space, input/output (I/O), and bandwidth.</span><span class="sxs-lookup"><span data-stu-id="41af5-401">For example, you can use a redundant array of independent disks (RAID) volume to accommodate space, input/output (I/O), and bandwidth.</span></span> <span data-ttu-id="41af5-402">We recommend using RAID 5, 50, and 10.</span><span class="sxs-lookup"><span data-stu-id="41af5-402">We recommend using RAID 5, 50, and 10.</span></span>

<span data-ttu-id="41af5-403">The following figure shows typical short-term retention local (to the server) volumes and long-term retention archives volumes.</span><span class="sxs-lookup"><span data-stu-id="41af5-403">The following figure shows typical short-term retention local (to the server) volumes and long-term retention archives volumes.</span></span> <span data-ttu-id="41af5-404">In this scenario, all backups run on the local (to the server) RAID volume.</span><span class="sxs-lookup"><span data-stu-id="41af5-404">In this scenario, all backups run on the local (to the server) RAID volume.</span></span> <span data-ttu-id="41af5-405">These backups are periodically duplicated and archived to an archives volume.</span><span class="sxs-lookup"><span data-stu-id="41af5-405">These backups are periodically duplicated and archived to an archives volume.</span></span> <span data-ttu-id="41af5-406">It is important to size your local (to the server) RAID volume so that it can handle your short-term retention capacity and performance requirements.</span><span class="sxs-lookup"><span data-stu-id="41af5-406">It is important to size your local (to the server) RAID volume so that it can handle your short-term retention capacity and performance requirements.</span></span>

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a><span data-ttu-id="41af5-407">StorSimple as a secondary backup target GFS example</span><span class="sxs-lookup"><span data-stu-id="41af5-407">StorSimple as a secondary backup target GFS example</span></span>

![StorSimple as a secondary backup target logical diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetdiagram.png)

<span data-ttu-id="41af5-409">The following table shows how to set up backups to run on the local and StorSimple disks.</span><span class="sxs-lookup"><span data-stu-id="41af5-409">The following table shows how to set up backups to run on the local and StorSimple disks.</span></span> <span data-ttu-id="41af5-410">It includes individual and total capacity requirements.</span><span class="sxs-lookup"><span data-stu-id="41af5-410">It includes individual and total capacity requirements.</span></span>

### <a name="backup-configuration-and-capacity-requirements"></a><span data-ttu-id="41af5-411">Backup configuration and capacity requirements</span><span class="sxs-lookup"><span data-stu-id="41af5-411">Backup configuration and capacity requirements</span></span>

| <span data-ttu-id="41af5-412">Backup type and retention</span><span class="sxs-lookup"><span data-stu-id="41af5-412">Backup type and retention</span></span> | <span data-ttu-id="41af5-413">Configured storage</span><span class="sxs-lookup"><span data-stu-id="41af5-413">Configured storage</span></span> | <span data-ttu-id="41af5-414">Size (TiB)</span><span class="sxs-lookup"><span data-stu-id="41af5-414">Size (TiB)</span></span> | <span data-ttu-id="41af5-415">GFS multiplier</span><span class="sxs-lookup"><span data-stu-id="41af5-415">GFS multiplier</span></span> | <span data-ttu-id="41af5-416">Total capacity\* (TiB)</span><span class="sxs-lookup"><span data-stu-id="41af5-416">Total capacity\* (TiB)</span></span> |
|---|---|---|---|---|
| <span data-ttu-id="41af5-417">Week 1 (full and incremental)</span><span class="sxs-lookup"><span data-stu-id="41af5-417">Week 1 (full and incremental)</span></span> |<span data-ttu-id="41af5-418">Local disk (short-term)</span><span class="sxs-lookup"><span data-stu-id="41af5-418">Local disk (short-term)</span></span>| <span data-ttu-id="41af5-419">1</span><span class="sxs-lookup"><span data-stu-id="41af5-419">1</span></span> | <span data-ttu-id="41af5-420">1</span><span class="sxs-lookup"><span data-stu-id="41af5-420">1</span></span> | <span data-ttu-id="41af5-421">1</span><span class="sxs-lookup"><span data-stu-id="41af5-421">1</span></span> |
| <span data-ttu-id="41af5-422">StorSimple weeks 2-4</span><span class="sxs-lookup"><span data-stu-id="41af5-422">StorSimple weeks 2-4</span></span> |<span data-ttu-id="41af5-423">StorSimple disk (long-term)</span><span class="sxs-lookup"><span data-stu-id="41af5-423">StorSimple disk (long-term)</span></span> | <span data-ttu-id="41af5-424">1</span><span class="sxs-lookup"><span data-stu-id="41af5-424">1</span></span> | <span data-ttu-id="41af5-425">4</span><span class="sxs-lookup"><span data-stu-id="41af5-425">4</span></span> | <span data-ttu-id="41af5-426">4</span><span class="sxs-lookup"><span data-stu-id="41af5-426">4</span></span> |
| <span data-ttu-id="41af5-427">Monthly full</span><span class="sxs-lookup"><span data-stu-id="41af5-427">Monthly full</span></span> |<span data-ttu-id="41af5-428">StorSimple disk (long-term)</span><span class="sxs-lookup"><span data-stu-id="41af5-428">StorSimple disk (long-term)</span></span> | <span data-ttu-id="41af5-429">1</span><span class="sxs-lookup"><span data-stu-id="41af5-429">1</span></span> | <span data-ttu-id="41af5-430">12</span><span class="sxs-lookup"><span data-stu-id="41af5-430">12</span></span> | <span data-ttu-id="41af5-431">12</span><span class="sxs-lookup"><span data-stu-id="41af5-431">12</span></span> |
| <span data-ttu-id="41af5-432">Yearly full</span><span class="sxs-lookup"><span data-stu-id="41af5-432">Yearly full</span></span> |<span data-ttu-id="41af5-433">StorSimple disk (long-term)</span><span class="sxs-lookup"><span data-stu-id="41af5-433">StorSimple disk (long-term)</span></span> | <span data-ttu-id="41af5-434">1</span><span class="sxs-lookup"><span data-stu-id="41af5-434">1</span></span> | <span data-ttu-id="41af5-435">1</span><span class="sxs-lookup"><span data-stu-id="41af5-435">1</span></span> | <span data-ttu-id="41af5-436">1</span><span class="sxs-lookup"><span data-stu-id="41af5-436">1</span></span> |
|<span data-ttu-id="41af5-437">GFS volumes size requirement</span><span class="sxs-lookup"><span data-stu-id="41af5-437">GFS volumes size requirement</span></span> |  |  |  | <span data-ttu-id="41af5-438">18\*</span><span class="sxs-lookup"><span data-stu-id="41af5-438">18\*</span></span>|
<span data-ttu-id="41af5-439">\* Total capacity includes 17 TiB of StorSimple disks and 1 TiB of local RAID volume.</span><span class="sxs-lookup"><span data-stu-id="41af5-439">\* Total capacity includes 17 TiB of StorSimple disks and 1 TiB of local RAID volume.</span></span>


### <a name="gfs-example-schedule-gfs-rotation-weekly-monthly-and-yearly-schedule"></a><span data-ttu-id="41af5-440">GFS example schedule: GFS rotation weekly, monthly, and yearly schedule</span><span class="sxs-lookup"><span data-stu-id="41af5-440">GFS example schedule: GFS rotation weekly, monthly, and yearly schedule</span></span>

| <span data-ttu-id="41af5-441">Week</span><span class="sxs-lookup"><span data-stu-id="41af5-441">Week</span></span> | <span data-ttu-id="41af5-442">Full</span><span class="sxs-lookup"><span data-stu-id="41af5-442">Full</span></span> | <span data-ttu-id="41af5-443">Incremental day 1</span><span class="sxs-lookup"><span data-stu-id="41af5-443">Incremental day 1</span></span> | <span data-ttu-id="41af5-444">Incremental day 2</span><span class="sxs-lookup"><span data-stu-id="41af5-444">Incremental day 2</span></span> | <span data-ttu-id="41af5-445">Incremental day 3</span><span class="sxs-lookup"><span data-stu-id="41af5-445">Incremental day 3</span></span> | <span data-ttu-id="41af5-446">Incremental day 4</span><span class="sxs-lookup"><span data-stu-id="41af5-446">Incremental day 4</span></span> | <span data-ttu-id="41af5-447">Incremental day 5</span><span class="sxs-lookup"><span data-stu-id="41af5-447">Incremental day 5</span></span> |
|---|---|---|---|---|---|---|
| <span data-ttu-id="41af5-448">Week 1</span><span class="sxs-lookup"><span data-stu-id="41af5-448">Week 1</span></span> | <span data-ttu-id="41af5-449">Local RAID volume</span><span class="sxs-lookup"><span data-stu-id="41af5-449">Local RAID volume</span></span>  | <span data-ttu-id="41af5-450">Local RAID volume</span><span class="sxs-lookup"><span data-stu-id="41af5-450">Local RAID volume</span></span> | <span data-ttu-id="41af5-451">Local RAID volume</span><span class="sxs-lookup"><span data-stu-id="41af5-451">Local RAID volume</span></span> | <span data-ttu-id="41af5-452">Local RAID volume</span><span class="sxs-lookup"><span data-stu-id="41af5-452">Local RAID volume</span></span> | <span data-ttu-id="41af5-453">Local RAID volume</span><span class="sxs-lookup"><span data-stu-id="41af5-453">Local RAID volume</span></span> | <span data-ttu-id="41af5-454">Local RAID volume</span><span class="sxs-lookup"><span data-stu-id="41af5-454">Local RAID volume</span></span> |
| <span data-ttu-id="41af5-455">Week 2</span><span class="sxs-lookup"><span data-stu-id="41af5-455">Week 2</span></span> | <span data-ttu-id="41af5-456">StorSimple weeks 2-4</span><span class="sxs-lookup"><span data-stu-id="41af5-456">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="41af5-457">Week 3</span><span class="sxs-lookup"><span data-stu-id="41af5-457">Week 3</span></span> | <span data-ttu-id="41af5-458">StorSimple weeks 2-4</span><span class="sxs-lookup"><span data-stu-id="41af5-458">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="41af5-459">Week 4</span><span class="sxs-lookup"><span data-stu-id="41af5-459">Week 4</span></span> | <span data-ttu-id="41af5-460">StorSimple weeks 2-4</span><span class="sxs-lookup"><span data-stu-id="41af5-460">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="41af5-461">Monthly</span><span class="sxs-lookup"><span data-stu-id="41af5-461">Monthly</span></span> | <span data-ttu-id="41af5-462">StorSimple monthly</span><span class="sxs-lookup"><span data-stu-id="41af5-462">StorSimple monthly</span></span> |   |   |   |   |   |
| <span data-ttu-id="41af5-463">Yearly</span><span class="sxs-lookup"><span data-stu-id="41af5-463">Yearly</span></span> | <span data-ttu-id="41af5-464">StorSimple yearly</span><span class="sxs-lookup"><span data-stu-id="41af5-464">StorSimple yearly</span></span>  |   |   |   |   |   |   |


## <a name="assign-storsimple-volumes-to-a-netbackup-archive-and-duplication-job"></a><span data-ttu-id="41af5-465">Assign StorSimple volumes to a NetBackup archive and duplication job</span><span class="sxs-lookup"><span data-stu-id="41af5-465">Assign StorSimple volumes to a NetBackup archive and duplication job</span></span>

<span data-ttu-id="41af5-466">Because NetBackup offers a wide range of options for storage and media management, we recommend that you consult with Veritas or your NetBackup architect to properly assess your storage lifecycle policy (SLP) requirements.</span><span class="sxs-lookup"><span data-stu-id="41af5-466">Because NetBackup offers a wide range of options for storage and media management, we recommend that you consult with Veritas or your NetBackup architect to properly assess your storage lifecycle policy (SLP) requirements.</span></span>

<span data-ttu-id="41af5-467">After you've defined the initial disk pools, you need to define three additional storage lifecycle policies, for a total of four policies:</span><span class="sxs-lookup"><span data-stu-id="41af5-467">After you've defined the initial disk pools, you need to define three additional storage lifecycle policies, for a total of four policies:</span></span>
* <span data-ttu-id="41af5-468">LocalRAIDVolume</span><span class="sxs-lookup"><span data-stu-id="41af5-468">LocalRAIDVolume</span></span>
* <span data-ttu-id="41af5-469">StorSimpleWeek2-4</span><span class="sxs-lookup"><span data-stu-id="41af5-469">StorSimpleWeek2-4</span></span>
* <span data-ttu-id="41af5-470">StorSimpleMonthlyFulls</span><span class="sxs-lookup"><span data-stu-id="41af5-470">StorSimpleMonthlyFulls</span></span>
* <span data-ttu-id="41af5-471">StorSimpleYearlyFulls</span><span class="sxs-lookup"><span data-stu-id="41af5-471">StorSimpleYearlyFulls</span></span>

### <a name="to-assign-storsimple-volumes-to-a-netbackup-archive-and-duplication-job"></a><span data-ttu-id="41af5-472">To assign StorSimple volumes to a NetBackup archive and duplication job</span><span class="sxs-lookup"><span data-stu-id="41af5-472">To assign StorSimple volumes to a NetBackup archive and duplication job</span></span>

1.  <span data-ttu-id="41af5-473">In the NetBackup Administration Console, select **Storage** > **Storage Lifecycle Policies** > **New Storage Lifecycle Policy**.</span><span class="sxs-lookup"><span data-stu-id="41af5-473">In the NetBackup Administration Console, select **Storage** > **Storage Lifecycle Policies** > **New Storage Lifecycle Policy**.</span></span>

    ![NetBackup Administration Console, new storage lifecycle policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage20.png)

2.  <span data-ttu-id="41af5-475">Enter a name for the snapshot, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="41af5-475">Enter a name for the snapshot, and then select **Add**.</span></span>

3.  <span data-ttu-id="41af5-476">In the **New Operation** dialog box, on the **Properties** tab, for **Operation**, select **Backup**.</span><span class="sxs-lookup"><span data-stu-id="41af5-476">In the **New Operation** dialog box, on the **Properties** tab, for **Operation**, select **Backup**.</span></span> <span data-ttu-id="41af5-477">Select the values you want for **Destination storage**, **Retention type**, and **Retention period**.</span><span class="sxs-lookup"><span data-stu-id="41af5-477">Select the values you want for **Destination storage**, **Retention type**, and **Retention period**.</span></span> <span data-ttu-id="41af5-478">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="41af5-478">Select **OK**.</span></span>

    ![NetBackup Administration Console, New Operation dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage22.png)

    <span data-ttu-id="41af5-480">This defines the first backup operation and repository.</span><span class="sxs-lookup"><span data-stu-id="41af5-480">This defines the first backup operation and repository.</span></span>

4.  <span data-ttu-id="41af5-481">Select to highlight the previous operation, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="41af5-481">Select to highlight the previous operation, and then select **Add**.</span></span> <span data-ttu-id="41af5-482">In the **Change Storage Operation** dialog box, select the values you want for **Destination storage**, **Retention type**, and **Retention period**.</span><span class="sxs-lookup"><span data-stu-id="41af5-482">In the **Change Storage Operation** dialog box, select the values you want for **Destination storage**, **Retention type**, and **Retention period**.</span></span>

    ![NetBackup Administration Console,Change Storage Operation dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage23.png)

5.  <span data-ttu-id="41af5-484">Select to highlight the previous operation, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="41af5-484">Select to highlight the previous operation, and then select **Add**.</span></span> <span data-ttu-id="41af5-485">In the **New Storage Lifecycle Policy** dialog box, add monthly backups for a year.</span><span class="sxs-lookup"><span data-stu-id="41af5-485">In the **New Storage Lifecycle Policy** dialog box, add monthly backups for a year.</span></span>

    ![NetBackup Administration Console, New Storage Lifecycle Policy dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage24.png)

6.  <span data-ttu-id="41af5-487">Repeat steps 4-5 until you've created the comprehensive SLP retention policy that you need.</span><span class="sxs-lookup"><span data-stu-id="41af5-487">Repeat steps 4-5 until you've created the comprehensive SLP retention policy that you need.</span></span>

    ![NetBackup Administration Console, Add policies in the New Storage Lifecycle Policy dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage25.png)

7.  <span data-ttu-id="41af5-489">When you are finished defining your SLP retention policy, under **Policy**, define a backup policy by following the steps detailed in [Assigning StorSimple volumes to a NetBackup backup job](#assigning-storsimple-volumes-to-a-netbackup-backup-job).</span><span class="sxs-lookup"><span data-stu-id="41af5-489">When you are finished defining your SLP retention policy, under **Policy**, define a backup policy by following the steps detailed in [Assigning StorSimple volumes to a NetBackup backup job](#assigning-storsimple-volumes-to-a-netbackup-backup-job).</span></span>

8.  <span data-ttu-id="41af5-490">Under **Schedules**, in the **Change Schedule** dialog box, right-click **Full**, and then select **Change**.</span><span class="sxs-lookup"><span data-stu-id="41af5-490">Under **Schedules**, in the **Change Schedule** dialog box, right-click **Full**, and then select **Change**.</span></span>

    ![NetBackup Administration Console, Change Schedule dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage26.png)

9.  <span data-ttu-id="41af5-492">Select the **Override policy storage selection** check box, and then select the SLP retention policy that you created in steps 1-6.</span><span class="sxs-lookup"><span data-stu-id="41af5-492">Select the **Override policy storage selection** check box, and then select the SLP retention policy that you created in steps 1-6.</span></span>

    ![NetBackup Administration Console, override policy storage selection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage27.png)

10.  <span data-ttu-id="41af5-494">Select **OK**, and then repeat for the incremental backup schedule.</span><span class="sxs-lookup"><span data-stu-id="41af5-494">Select **OK**, and then repeat for the incremental backup schedule.</span></span>

    ![NetBackup Administration Console, Change Schedule dialog box for incremental backups](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/nbimage28.png)


| <span data-ttu-id="41af5-496">Backup type retention</span><span class="sxs-lookup"><span data-stu-id="41af5-496">Backup type retention</span></span> | <span data-ttu-id="41af5-497">Size (TiB)</span><span class="sxs-lookup"><span data-stu-id="41af5-497">Size (TiB)</span></span> | <span data-ttu-id="41af5-498">GFS multiplier\*</span><span class="sxs-lookup"><span data-stu-id="41af5-498">GFS multiplier\*</span></span> | <span data-ttu-id="41af5-499">Total capacity (TiB)</span><span class="sxs-lookup"><span data-stu-id="41af5-499">Total capacity (TiB)</span></span>  |
|---|---|---|---|
| <span data-ttu-id="41af5-500">Weekly full</span><span class="sxs-lookup"><span data-stu-id="41af5-500">Weekly full</span></span> |  <span data-ttu-id="41af5-501">1</span><span class="sxs-lookup"><span data-stu-id="41af5-501">1</span></span>  |  <span data-ttu-id="41af5-502">4</span><span class="sxs-lookup"><span data-stu-id="41af5-502">4</span></span> | <span data-ttu-id="41af5-503">4</span><span class="sxs-lookup"><span data-stu-id="41af5-503">4</span></span>  |
| <span data-ttu-id="41af5-504">Daily incremental</span><span class="sxs-lookup"><span data-stu-id="41af5-504">Daily incremental</span></span>  | <span data-ttu-id="41af5-505">0.5</span><span class="sxs-lookup"><span data-stu-id="41af5-505">0.5</span></span>  | <span data-ttu-id="41af5-506">20 (cycles are equal to the number of weeks per month)</span><span class="sxs-lookup"><span data-stu-id="41af5-506">20 (cycles are equal to the number of weeks per month)</span></span> | <span data-ttu-id="41af5-507">12 (2 for additional quota)</span><span class="sxs-lookup"><span data-stu-id="41af5-507">12 (2 for additional quota)</span></span> |
| <span data-ttu-id="41af5-508">Monthly full</span><span class="sxs-lookup"><span data-stu-id="41af5-508">Monthly full</span></span>  | <span data-ttu-id="41af5-509">1</span><span class="sxs-lookup"><span data-stu-id="41af5-509">1</span></span> | <span data-ttu-id="41af5-510">12</span><span class="sxs-lookup"><span data-stu-id="41af5-510">12</span></span> | <span data-ttu-id="41af5-511">12</span><span class="sxs-lookup"><span data-stu-id="41af5-511">12</span></span> |
| <span data-ttu-id="41af5-512">Yearly full</span><span class="sxs-lookup"><span data-stu-id="41af5-512">Yearly full</span></span> | <span data-ttu-id="41af5-513">1</span><span class="sxs-lookup"><span data-stu-id="41af5-513">1</span></span>  | <span data-ttu-id="41af5-514">10</span><span class="sxs-lookup"><span data-stu-id="41af5-514">10</span></span> | <span data-ttu-id="41af5-515">10</span><span class="sxs-lookup"><span data-stu-id="41af5-515">10</span></span> |
| <span data-ttu-id="41af5-516">GFS requirement</span><span class="sxs-lookup"><span data-stu-id="41af5-516">GFS requirement</span></span>  |     |     | <span data-ttu-id="41af5-517">38</span><span class="sxs-lookup"><span data-stu-id="41af5-517">38</span></span> |
| <span data-ttu-id="41af5-518">Additional quota</span><span class="sxs-lookup"><span data-stu-id="41af5-518">Additional quota</span></span>  | <span data-ttu-id="41af5-519">4</span><span class="sxs-lookup"><span data-stu-id="41af5-519">4</span></span>  |    | <span data-ttu-id="41af5-520">42 total GFS requirement</span><span class="sxs-lookup"><span data-stu-id="41af5-520">42 total GFS requirement</span></span> |
<span data-ttu-id="41af5-521">\* The GFS multiplier is the number of copies you need to protect and retain to meet your backup policy requirements.</span><span class="sxs-lookup"><span data-stu-id="41af5-521">\* The GFS multiplier is the number of copies you need to protect and retain to meet your backup policy requirements.</span></span>

## <a name="storsimple-cloud-snapshots"></a><span data-ttu-id="41af5-522">StorSimple cloud snapshots</span><span class="sxs-lookup"><span data-stu-id="41af5-522">StorSimple cloud snapshots</span></span>

<span data-ttu-id="41af5-523">StorSimple cloud snapshots protect the data that resides in your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="41af5-523">StorSimple cloud snapshots protect the data that resides in your StorSimple device.</span></span> <span data-ttu-id="41af5-524">Creating a cloud snapshot is equivalent to shipping local backup tapes to an offsite facility.</span><span class="sxs-lookup"><span data-stu-id="41af5-524">Creating a cloud snapshot is equivalent to shipping local backup tapes to an offsite facility.</span></span> <span data-ttu-id="41af5-525">If you use Azure geo-redundant storage, creating a cloud snapshot is equivalent to shipping backup tapes to multiple sites.</span><span class="sxs-lookup"><span data-stu-id="41af5-525">If you use Azure geo-redundant storage, creating a cloud snapshot is equivalent to shipping backup tapes to multiple sites.</span></span> <span data-ttu-id="41af5-526">If you need to restore a device after a disaster, you might bring another StorSimple device online and do a failover.</span><span class="sxs-lookup"><span data-stu-id="41af5-526">If you need to restore a device after a disaster, you might bring another StorSimple device online and do a failover.</span></span> <span data-ttu-id="41af5-527">After the failover, you would be able to access the data (at cloud speeds) from the most recent cloud snapshot.</span><span class="sxs-lookup"><span data-stu-id="41af5-527">After the failover, you would be able to access the data (at cloud speeds) from the most recent cloud snapshot.</span></span>

<span data-ttu-id="41af5-528">The following section describes how to create a short script to start and delete StorSimple cloud snapshots during backup post-processing.</span><span class="sxs-lookup"><span data-stu-id="41af5-528">The following section describes how to create a short script to start and delete StorSimple cloud snapshots during backup post-processing.</span></span>

> [!NOTE]
> <span data-ttu-id="41af5-529">Snapshots that are manually or programmatically created do not follow the StorSimple snapshot expiration policy.</span><span class="sxs-lookup"><span data-stu-id="41af5-529">Snapshots that are manually or programmatically created do not follow the StorSimple snapshot expiration policy.</span></span> <span data-ttu-id="41af5-530">These snapshots must be manually or programmatically deleted.</span><span class="sxs-lookup"><span data-stu-id="41af5-530">These snapshots must be manually or programmatically deleted.</span></span>

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a><span data-ttu-id="41af5-531">Start and delete cloud snapshots by using a script</span><span class="sxs-lookup"><span data-stu-id="41af5-531">Start and delete cloud snapshots by using a script</span></span>

> [!NOTE]
> <span data-ttu-id="41af5-532">Carefully assess the compliance and data retention repercussions before you delete a StorSimple snapshot.</span><span class="sxs-lookup"><span data-stu-id="41af5-532">Carefully assess the compliance and data retention repercussions before you delete a StorSimple snapshot.</span></span> <span data-ttu-id="41af5-533">For more information about how to run a post-backup script, see the [NetBackup documentation](http://www.veritas.com/docs/000094423).</span><span class="sxs-lookup"><span data-stu-id="41af5-533">For more information about how to run a post-backup script, see the [NetBackup documentation](http://www.veritas.com/docs/000094423).</span></span>

### <a name="backup-lifecycle"></a><span data-ttu-id="41af5-534">Backup lifecycle</span><span class="sxs-lookup"><span data-stu-id="41af5-534">Backup lifecycle</span></span>

![Backup Lifecycle diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-netbackup/backuplifecycle.png)

### <a name="requirements"></a><span data-ttu-id="41af5-536">Requirements</span><span class="sxs-lookup"><span data-stu-id="41af5-536">Requirements</span></span>

-   <span data-ttu-id="41af5-537">The server that runs the script must have access to Azure cloud resources.</span><span class="sxs-lookup"><span data-stu-id="41af5-537">The server that runs the script must have access to Azure cloud resources.</span></span>
-   <span data-ttu-id="41af5-538">The user account must have the necessary permissions.</span><span class="sxs-lookup"><span data-stu-id="41af5-538">The user account must have the necessary permissions.</span></span>
-   <span data-ttu-id="41af5-539">A StorSimple backup policy with the associated StorSimple volumes must be set up but not turned on.</span><span class="sxs-lookup"><span data-stu-id="41af5-539">A StorSimple backup policy with the associated StorSimple volumes must be set up but not turned on.</span></span>
-   <span data-ttu-id="41af5-540">You'll need the StorSimple resource name, registration key, device name, and backup policy ID.</span><span class="sxs-lookup"><span data-stu-id="41af5-540">You'll need the StorSimple resource name, registration key, device name, and backup policy ID.</span></span>

### <a name="to-start-or-delete-a-cloud-snapshot"></a><span data-ttu-id="41af5-541">To start or delete a cloud snapshot</span><span class="sxs-lookup"><span data-stu-id="41af5-541">To start or delete a cloud snapshot</span></span>

1.  <span data-ttu-id="41af5-542">[Install Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azureps-cmdlets-docs/#install-and-configure).</span><span class="sxs-lookup"><span data-stu-id="41af5-542">[Install Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azureps-cmdlets-docs/#install-and-configure).</span></span>
2.  <span data-ttu-id="41af5-543">[Download and import publish settings and subscription information](https://msdn.microsoft.com/library/dn385850.aspx).</span><span class="sxs-lookup"><span data-stu-id="41af5-543">[Download and import publish settings and subscription information](https://msdn.microsoft.com/library/dn385850.aspx).</span></span>
3.  <span data-ttu-id="41af5-544">In the Azure classic portal, get the resource name and [registration key for your StorSimple Manager service](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="41af5-544">In the Azure classic portal, get the resource name and [registration key for your StorSimple Manager service](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).</span></span>
4.  <span data-ttu-id="41af5-545">On the server that runs the script, run PowerShell as an administrator.</span><span class="sxs-lookup"><span data-stu-id="41af5-545">On the server that runs the script, run PowerShell as an administrator.</span></span> <span data-ttu-id="41af5-546">Type this command:</span><span class="sxs-lookup"><span data-stu-id="41af5-546">Type this command:</span></span>

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    <span data-ttu-id="41af5-547">Note the backup policy ID.</span><span class="sxs-lookup"><span data-stu-id="41af5-547">Note the backup policy ID.</span></span>
5.  <span data-ttu-id="41af5-548">In Notepad, create a new PowerShell script by using the following code.</span><span class="sxs-lookup"><span data-stu-id="41af5-548">In Notepad, create a new PowerShell script by using the following code.</span></span>

    <span data-ttu-id="41af5-549">Copy and paste this code snippet:</span><span class="sxs-lookup"><span data-stu-id="41af5-549">Copy and paste this code snippet:</span></span>
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
      <span data-ttu-id="41af5-550">Save the PowerShell script to the same location where you saved your Azure publish settings.</span><span class="sxs-lookup"><span data-stu-id="41af5-550">Save the PowerShell script to the same location where you saved your Azure publish settings.</span></span> <span data-ttu-id="41af5-551">For example, save as C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1.</span><span class="sxs-lookup"><span data-stu-id="41af5-551">For example, save as C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1.</span></span>
6.  <span data-ttu-id="41af5-552">Add the script to your backup job in NetBackup.</span><span class="sxs-lookup"><span data-stu-id="41af5-552">Add the script to your backup job in NetBackup.</span></span> <span data-ttu-id="41af5-553">To do this, edit your NetBackup job options' pre-processing and post-processing commands.</span><span class="sxs-lookup"><span data-stu-id="41af5-553">To do this, edit your NetBackup job options' pre-processing and post-processing commands.</span></span>

> [!NOTE]
> <span data-ttu-id="41af5-554">We recommend that you run your StorSimple cloud snapshot backup policy as a post-processing script at the end of your daily backup job.</span><span class="sxs-lookup"><span data-stu-id="41af5-554">We recommend that you run your StorSimple cloud snapshot backup policy as a post-processing script at the end of your daily backup job.</span></span> <span data-ttu-id="41af5-555">For more information about how to back up and restore your backup application environment to help you meet your RPO and RTO, please consult with your backup architect.</span><span class="sxs-lookup"><span data-stu-id="41af5-555">For more information about how to back up and restore your backup application environment to help you meet your RPO and RTO, please consult with your backup architect.</span></span>

## <a name="storsimple-as-a-restore-source"></a><span data-ttu-id="41af5-556">StorSimple as a restore source</span><span class="sxs-lookup"><span data-stu-id="41af5-556">StorSimple as a restore source</span></span>

<span data-ttu-id="41af5-557">Restores from a StorSimple device work like restores from any block storage device.</span><span class="sxs-lookup"><span data-stu-id="41af5-557">Restores from a StorSimple device work like restores from any block storage device.</span></span> <span data-ttu-id="41af5-558">Restores of data that is tiered to the cloud occurs at cloud speeds.</span><span class="sxs-lookup"><span data-stu-id="41af5-558">Restores of data that is tiered to the cloud occurs at cloud speeds.</span></span> <span data-ttu-id="41af5-559">For local data, restores occur at the local disk speed of the device.</span><span class="sxs-lookup"><span data-stu-id="41af5-559">For local data, restores occur at the local disk speed of the device.</span></span> <span data-ttu-id="41af5-560">For information about how to perform a restore, see the [NetBackup documentation](http://www.veritas.com/docs/000094423).</span><span class="sxs-lookup"><span data-stu-id="41af5-560">For information about how to perform a restore, see the [NetBackup documentation](http://www.veritas.com/docs/000094423).</span></span> <span data-ttu-id="41af5-561">We recommend that you conform to NetBackup restore best practices.</span><span class="sxs-lookup"><span data-stu-id="41af5-561">We recommend that you conform to NetBackup restore best practices.</span></span>

## <a name="storsimple-failover-and-disaster-recovery"></a><span data-ttu-id="41af5-562">StorSimple failover and disaster recovery</span><span class="sxs-lookup"><span data-stu-id="41af5-562">StorSimple failover and disaster recovery</span></span>

> [!NOTE]
> <span data-ttu-id="41af5-563">For backup target scenarios, StorSimple Cloud Appliance is not supported as a restore target.</span><span class="sxs-lookup"><span data-stu-id="41af5-563">For backup target scenarios, StorSimple Cloud Appliance is not supported as a restore target.</span></span>

<span data-ttu-id="41af5-564">A disaster can be caused by a variety of factors.</span><span class="sxs-lookup"><span data-stu-id="41af5-564">A disaster can be caused by a variety of factors.</span></span> <span data-ttu-id="41af5-565">The following table lists common disaster recovery scenarios.</span><span class="sxs-lookup"><span data-stu-id="41af5-565">The following table lists common disaster recovery scenarios.</span></span>

| <span data-ttu-id="41af5-566">Scenario</span><span class="sxs-lookup"><span data-stu-id="41af5-566">Scenario</span></span> | <span data-ttu-id="41af5-567">Impact</span><span class="sxs-lookup"><span data-stu-id="41af5-567">Impact</span></span> | <span data-ttu-id="41af5-568">How to recover</span><span class="sxs-lookup"><span data-stu-id="41af5-568">How to recover</span></span> | <span data-ttu-id="41af5-569">Notes</span><span class="sxs-lookup"><span data-stu-id="41af5-569">Notes</span></span> |
|---|---|---|---|
| <span data-ttu-id="41af5-570">StorSimple device failure</span><span class="sxs-lookup"><span data-stu-id="41af5-570">StorSimple device failure</span></span> | <span data-ttu-id="41af5-571">Backup and restore operations are interrupted.</span><span class="sxs-lookup"><span data-stu-id="41af5-571">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="41af5-572">Replace the failed device and perform [StorSimple failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="41af5-572">Replace the failed device and perform [StorSimple failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span> | <span data-ttu-id="41af5-573">If you need to perform a restore after device recovery, full data working sets are retrieved from the cloud to the new device.</span><span class="sxs-lookup"><span data-stu-id="41af5-573">If you need to perform a restore after device recovery, full data working sets are retrieved from the cloud to the new device.</span></span> <span data-ttu-id="41af5-574">All operations are at cloud speeds.</span><span class="sxs-lookup"><span data-stu-id="41af5-574">All operations are at cloud speeds.</span></span> <span data-ttu-id="41af5-575">The index and catalog rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier, which might be a time-consuming process.</span><span class="sxs-lookup"><span data-stu-id="41af5-575">The index and catalog rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier, which might be a time-consuming process.</span></span> |
| <span data-ttu-id="41af5-576">NetBackup server failure</span><span class="sxs-lookup"><span data-stu-id="41af5-576">NetBackup server failure</span></span> | <span data-ttu-id="41af5-577">Backup and restore operations are interrupted.</span><span class="sxs-lookup"><span data-stu-id="41af5-577">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="41af5-578">Rebuild the backup server and perform database restore.</span><span class="sxs-lookup"><span data-stu-id="41af5-578">Rebuild the backup server and perform database restore.</span></span> | <span data-ttu-id="41af5-579">You must rebuild or restore the NetBackup server at the disaster recovery site.</span><span class="sxs-lookup"><span data-stu-id="41af5-579">You must rebuild or restore the NetBackup server at the disaster recovery site.</span></span> <span data-ttu-id="41af5-580">Restore the database to the most recent point.</span><span class="sxs-lookup"><span data-stu-id="41af5-580">Restore the database to the most recent point.</span></span> <span data-ttu-id="41af5-581">If the restored NetBackup database is not in sync with your latest backup jobs, indexing and cataloging is required.</span><span class="sxs-lookup"><span data-stu-id="41af5-581">If the restored NetBackup database is not in sync with your latest backup jobs, indexing and cataloging is required.</span></span> <span data-ttu-id="41af5-582">This index and catalog rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier.</span><span class="sxs-lookup"><span data-stu-id="41af5-582">This index and catalog rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier.</span></span> <span data-ttu-id="41af5-583">This makes it further time-intensive.</span><span class="sxs-lookup"><span data-stu-id="41af5-583">This makes it further time-intensive.</span></span> |
| <span data-ttu-id="41af5-584">Site failure that results in the loss of both the backup server and StorSimple</span><span class="sxs-lookup"><span data-stu-id="41af5-584">Site failure that results in the loss of both the backup server and StorSimple</span></span> | <span data-ttu-id="41af5-585">Backup and restore operations are interrupted.</span><span class="sxs-lookup"><span data-stu-id="41af5-585">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="41af5-586">Restore StorSimple first, and then restore NetBackup.</span><span class="sxs-lookup"><span data-stu-id="41af5-586">Restore StorSimple first, and then restore NetBackup.</span></span> | <span data-ttu-id="41af5-587">Restore StorSimple first, and then restore NetBackup.</span><span class="sxs-lookup"><span data-stu-id="41af5-587">Restore StorSimple first, and then restore NetBackup.</span></span> <span data-ttu-id="41af5-588">If you need to perform a restore after device recovery, the full data working sets are retrieved from the cloud to the new device.</span><span class="sxs-lookup"><span data-stu-id="41af5-588">If you need to perform a restore after device recovery, the full data working sets are retrieved from the cloud to the new device.</span></span> <span data-ttu-id="41af5-589">All operations are at cloud speeds.</span><span class="sxs-lookup"><span data-stu-id="41af5-589">All operations are at cloud speeds.</span></span> |

## <a name="references"></a><span data-ttu-id="41af5-590">References</span><span class="sxs-lookup"><span data-stu-id="41af5-590">References</span></span>

<span data-ttu-id="41af5-591">The following documents were referenced for this article:</span><span class="sxs-lookup"><span data-stu-id="41af5-591">The following documents were referenced for this article:</span></span>

- [<span data-ttu-id="41af5-592">StorSimple multipath I/O setup</span><span class="sxs-lookup"><span data-stu-id="41af5-592">StorSimple multipath I/O setup</span></span>](storsimple-configure-mpio-windows-server.md)
- [<span data-ttu-id="41af5-593">Storage scenarios: Thin provisioning</span><span class="sxs-lookup"><span data-stu-id="41af5-593">Storage scenarios: Thin provisioning</span></span>](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [<span data-ttu-id="41af5-594">Using GPT drives</span><span class="sxs-lookup"><span data-stu-id="41af5-594">Using GPT drives</span></span>](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [<span data-ttu-id="41af5-595">Set up shadow copies for shared folders</span><span class="sxs-lookup"><span data-stu-id="41af5-595">Set up shadow copies for shared folders</span></span>](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a><span data-ttu-id="41af5-596">Next steps</span><span class="sxs-lookup"><span data-stu-id="41af5-596">Next steps</span></span>

- <span data-ttu-id="41af5-597">Learn more about how to [restore from a backup set](storsimple-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="41af5-597">Learn more about how to [restore from a backup set](storsimple-restore-from-backup-set-u2.md).</span></span>
- <span data-ttu-id="41af5-598">Learn more about how to perform [device failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="41af5-598">Learn more about how to perform [device failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span>
































