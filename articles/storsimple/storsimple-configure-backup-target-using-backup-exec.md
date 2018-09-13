---
title: StorSimple 8000 series as backup target with Backup Exec | Microsoft Docs
description: Describes the StorSimple backup target configuration with Veritas Backup Exec.
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
ms.openlocfilehash: 44a916de10ec1124dcf05e43ab8cb1b754b791ac
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661262"
---
# <a name="storsimple-as-a-backup-target-with-backup-exec"></a><span data-ttu-id="5ad51-103">StorSimple as a backup target with Backup Exec</span><span class="sxs-lookup"><span data-stu-id="5ad51-103">StorSimple as a backup target with Backup Exec</span></span>

## <a name="overview"></a><span data-ttu-id="5ad51-104">Overview</span><span class="sxs-lookup"><span data-stu-id="5ad51-104">Overview</span></span>

<span data-ttu-id="5ad51-105">Azure StorSimple is a hybrid cloud storage solution from Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5ad51-105">Azure StorSimple is a hybrid cloud storage solution from Microsoft.</span></span> <span data-ttu-id="5ad51-106">StorSimple addresses the complexities of exponential data growth by using an Azure storage account as an extension of the on-premises solution, and automatically tiering data across on-premises storage and cloud storage.</span><span class="sxs-lookup"><span data-stu-id="5ad51-106">StorSimple addresses the complexities of exponential data growth by using an Azure storage account as an extension of the on-premises solution, and automatically tiering data across on-premises storage and cloud storage.</span></span>

<span data-ttu-id="5ad51-107">In this article, we discuss StorSimple integration with Veritas Backup Exec and best practices for integrating both solutions.</span><span class="sxs-lookup"><span data-stu-id="5ad51-107">In this article, we discuss StorSimple integration with Veritas Backup Exec and best practices for integrating both solutions.</span></span> <span data-ttu-id="5ad51-108">We also make recommendations on how to set up Backup Exec to best integrate with StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5ad51-108">We also make recommendations on how to set up Backup Exec to best integrate with StorSimple.</span></span> <span data-ttu-id="5ad51-109">We defer to Veritas best practices, backup architects, and administrators for the best way to set up Backup Exec to meet individual backup requirements and service-level agreements (SLAs).</span><span class="sxs-lookup"><span data-stu-id="5ad51-109">We defer to Veritas best practices, backup architects, and administrators for the best way to set up Backup Exec to meet individual backup requirements and service-level agreements (SLAs).</span></span>

<span data-ttu-id="5ad51-110">Although we illustrate configuration steps and key concepts, this article is by no means a step-by-step configuration or installation guide.</span><span class="sxs-lookup"><span data-stu-id="5ad51-110">Although we illustrate configuration steps and key concepts, this article is by no means a step-by-step configuration or installation guide.</span></span> <span data-ttu-id="5ad51-111">We assume that the basic components and infrastructure are in working order and ready to support the concepts that we describe.</span><span class="sxs-lookup"><span data-stu-id="5ad51-111">We assume that the basic components and infrastructure are in working order and ready to support the concepts that we describe.</span></span>

### <a name="who-should-read-this"></a><span data-ttu-id="5ad51-112">Who should read this?</span><span class="sxs-lookup"><span data-stu-id="5ad51-112">Who should read this?</span></span>

<span data-ttu-id="5ad51-113">The information in this article will be most helpful to backup administrators, storage administrators, and storage architects who have knowledge of storage, Windows Server 2012 R2, Ethernet, cloud services, and Backup Exec.</span><span class="sxs-lookup"><span data-stu-id="5ad51-113">The information in this article will be most helpful to backup administrators, storage administrators, and storage architects who have knowledge of storage, Windows Server 2012 R2, Ethernet, cloud services, and Backup Exec.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="5ad51-114">Supported versions</span><span class="sxs-lookup"><span data-stu-id="5ad51-114">Supported versions</span></span>

-   [<span data-ttu-id="5ad51-115">Backup Exec 16 and later versions</span><span class="sxs-lookup"><span data-stu-id="5ad51-115">Backup Exec 16 and later versions</span></span>](http://backupexec.com/compatibility)
-   [<span data-ttu-id="5ad51-116">StorSimple Update 3 and later versions</span><span class="sxs-lookup"><span data-stu-id="5ad51-116">StorSimple Update 3 and later versions</span></span>](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a><span data-ttu-id="5ad51-117">Why StorSimple as a backup target?</span><span class="sxs-lookup"><span data-stu-id="5ad51-117">Why StorSimple as a backup target?</span></span>

<span data-ttu-id="5ad51-118">StorSimple is a good choice for a backup target because:</span><span class="sxs-lookup"><span data-stu-id="5ad51-118">StorSimple is a good choice for a backup target because:</span></span>

-   <span data-ttu-id="5ad51-119">It provides standard, local storage for backup applications to use as a fast backup destination, without any changes.</span><span class="sxs-lookup"><span data-stu-id="5ad51-119">It provides standard, local storage for backup applications to use as a fast backup destination, without any changes.</span></span> <span data-ttu-id="5ad51-120">You also can use StorSimple for a quick restore of recent backups.</span><span class="sxs-lookup"><span data-stu-id="5ad51-120">You also can use StorSimple for a quick restore of recent backups.</span></span>
-   <span data-ttu-id="5ad51-121">Its cloud tiering is seamlessly integrated with an Azure cloud storage account to use cost-effective Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5ad51-121">Its cloud tiering is seamlessly integrated with an Azure cloud storage account to use cost-effective Azure Storage.</span></span>
-   <span data-ttu-id="5ad51-122">It automatically provides offsite storage for disaster recovery.</span><span class="sxs-lookup"><span data-stu-id="5ad51-122">It automatically provides offsite storage for disaster recovery.</span></span>

## <a name="key-concepts"></a><span data-ttu-id="5ad51-123">Key concepts</span><span class="sxs-lookup"><span data-stu-id="5ad51-123">Key concepts</span></span>

<span data-ttu-id="5ad51-124">As with any storage solution, a careful assessment of the solution’s storage performance, SLAs, rate of change, and capacity growth needs is critical to success.</span><span class="sxs-lookup"><span data-stu-id="5ad51-124">As with any storage solution, a careful assessment of the solution’s storage performance, SLAs, rate of change, and capacity growth needs is critical to success.</span></span> <span data-ttu-id="5ad51-125">The main idea is that by introducing a cloud tier, your access times and throughputs to the cloud play a fundamental role in the ability of StorSimple to do its job.</span><span class="sxs-lookup"><span data-stu-id="5ad51-125">The main idea is that by introducing a cloud tier, your access times and throughputs to the cloud play a fundamental role in the ability of StorSimple to do its job.</span></span>

<span data-ttu-id="5ad51-126">StorSimple is designed to provide storage to applications that operate on a well-defined working set of data (hot data).</span><span class="sxs-lookup"><span data-stu-id="5ad51-126">StorSimple is designed to provide storage to applications that operate on a well-defined working set of data (hot data).</span></span> <span data-ttu-id="5ad51-127">In this model, the working set of data is stored on the local tiers, and the remaining nonworking/cold/archived set of data is tiered to the cloud.</span><span class="sxs-lookup"><span data-stu-id="5ad51-127">In this model, the working set of data is stored on the local tiers, and the remaining nonworking/cold/archived set of data is tiered to the cloud.</span></span> <span data-ttu-id="5ad51-128">This model is represented in the following figure.</span><span class="sxs-lookup"><span data-stu-id="5ad51-128">This model is represented in the following figure.</span></span> <span data-ttu-id="5ad51-129">The nearly flat green line represents the data stored on the local tiers of the StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="5ad51-129">The nearly flat green line represents the data stored on the local tiers of the StorSimple device.</span></span> <span data-ttu-id="5ad51-130">The red line represents the total amount of data stored on the StorSimple solution across all tiers.</span><span class="sxs-lookup"><span data-stu-id="5ad51-130">The red line represents the total amount of data stored on the StorSimple solution across all tiers.</span></span> <span data-ttu-id="5ad51-131">The space between the flat green line and the exponential red curve represents the total amount of data stored in the cloud.</span><span class="sxs-lookup"><span data-stu-id="5ad51-131">The space between the flat green line and the exponential red curve represents the total amount of data stored in the cloud.</span></span>

<span data-ttu-id="5ad51-132">**StorSimple tiering**
![StorSimple tiering diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/image1.jpg)</span><span class="sxs-lookup"><span data-stu-id="5ad51-132">**StorSimple tiering**
![StorSimple tiering diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/image1.jpg)</span></span>

<span data-ttu-id="5ad51-133">With this architecture in mind, you will find that StorSimple is ideally suited to operate as a backup target.</span><span class="sxs-lookup"><span data-stu-id="5ad51-133">With this architecture in mind, you will find that StorSimple is ideally suited to operate as a backup target.</span></span> <span data-ttu-id="5ad51-134">You can use StorSimple to:</span><span class="sxs-lookup"><span data-stu-id="5ad51-134">You can use StorSimple to:</span></span>
-   <span data-ttu-id="5ad51-135">Perform your most frequent restores from the local working set of data.</span><span class="sxs-lookup"><span data-stu-id="5ad51-135">Perform your most frequent restores from the local working set of data.</span></span>
-   <span data-ttu-id="5ad51-136">Use the cloud for offsite disaster recovery and older data, where restores are less frequent.</span><span class="sxs-lookup"><span data-stu-id="5ad51-136">Use the cloud for offsite disaster recovery and older data, where restores are less frequent.</span></span>

## <a name="storsimple-benefits"></a><span data-ttu-id="5ad51-137">StorSimple benefits</span><span class="sxs-lookup"><span data-stu-id="5ad51-137">StorSimple benefits</span></span>

<span data-ttu-id="5ad51-138">StorSimple provides an on-premises solution that is seamlessly integrated with Microsoft Azure, by taking advantage of seamless access to on-premises and cloud storage.</span><span class="sxs-lookup"><span data-stu-id="5ad51-138">StorSimple provides an on-premises solution that is seamlessly integrated with Microsoft Azure, by taking advantage of seamless access to on-premises and cloud storage.</span></span>

<span data-ttu-id="5ad51-139">StorSimple uses automatic tiering between the on-premises device, which has solid-state device (SSD) and serial-attached SCSI (SAS) storage, and Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5ad51-139">StorSimple uses automatic tiering between the on-premises device, which has solid-state device (SSD) and serial-attached SCSI (SAS) storage, and Azure Storage.</span></span> <span data-ttu-id="5ad51-140">Automatic tiering keeps frequently accessed data local, on the SSD and SAS tiers.</span><span class="sxs-lookup"><span data-stu-id="5ad51-140">Automatic tiering keeps frequently accessed data local, on the SSD and SAS tiers.</span></span> <span data-ttu-id="5ad51-141">It moves infrequently accessed data to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5ad51-141">It moves infrequently accessed data to Azure Storage.</span></span>

<span data-ttu-id="5ad51-142">StorSimple offers these benefits:</span><span class="sxs-lookup"><span data-stu-id="5ad51-142">StorSimple offers these benefits:</span></span>

-   <span data-ttu-id="5ad51-143">Unique deduplication and compression algorithms that use the cloud to achieve unprecedented deduplication levels</span><span class="sxs-lookup"><span data-stu-id="5ad51-143">Unique deduplication and compression algorithms that use the cloud to achieve unprecedented deduplication levels</span></span>
-   <span data-ttu-id="5ad51-144">High availability</span><span class="sxs-lookup"><span data-stu-id="5ad51-144">High availability</span></span>
-   <span data-ttu-id="5ad51-145">Geo-replication by using Azure geo-replication</span><span class="sxs-lookup"><span data-stu-id="5ad51-145">Geo-replication by using Azure geo-replication</span></span>
-   <span data-ttu-id="5ad51-146">Azure integration</span><span class="sxs-lookup"><span data-stu-id="5ad51-146">Azure integration</span></span>
-   <span data-ttu-id="5ad51-147">Data encryption in the cloud</span><span class="sxs-lookup"><span data-stu-id="5ad51-147">Data encryption in the cloud</span></span>
-   <span data-ttu-id="5ad51-148">Improved disaster recovery and compliance</span><span class="sxs-lookup"><span data-stu-id="5ad51-148">Improved disaster recovery and compliance</span></span>

<span data-ttu-id="5ad51-149">Although StorSimple presents two main deployment scenarios (primary backup target and secondary backup target), fundamentally, it's a plain, block storage device.</span><span class="sxs-lookup"><span data-stu-id="5ad51-149">Although StorSimple presents two main deployment scenarios (primary backup target and secondary backup target), fundamentally, it's a plain, block storage device.</span></span> <span data-ttu-id="5ad51-150">StorSimple does all the compression and deduplication.</span><span class="sxs-lookup"><span data-stu-id="5ad51-150">StorSimple does all the compression and deduplication.</span></span> <span data-ttu-id="5ad51-151">It seamlessly sends and retrieves data between the cloud and the application and file system.</span><span class="sxs-lookup"><span data-stu-id="5ad51-151">It seamlessly sends and retrieves data between the cloud and the application and file system.</span></span>

<span data-ttu-id="5ad51-152">For more information about StorSimple, see [StorSimple 8000 series: Hybrid cloud storage solution](storsimple-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ad51-152">For more information about StorSimple, see [StorSimple 8000 series: Hybrid cloud storage solution](storsimple-overview.md).</span></span> <span data-ttu-id="5ad51-153">Also, you can review the [technical StorSimple 8000 series specifications](storsimple-technical-specifications-and-compliance.md).</span><span class="sxs-lookup"><span data-stu-id="5ad51-153">Also, you can review the [technical StorSimple 8000 series specifications](storsimple-technical-specifications-and-compliance.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ad51-154">Using a StorSimple device as a backup target is supported only for StorSimple 8000 Update 3 and later versions.</span><span class="sxs-lookup"><span data-stu-id="5ad51-154">Using a StorSimple device as a backup target is supported only for StorSimple 8000 Update 3 and later versions.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="5ad51-155">Architecture overview</span><span class="sxs-lookup"><span data-stu-id="5ad51-155">Architecture overview</span></span>

<span data-ttu-id="5ad51-156">The following tables show the device model-to-architecture initial guidance.</span><span class="sxs-lookup"><span data-stu-id="5ad51-156">The following tables show the device model-to-architecture initial guidance.</span></span>

<span data-ttu-id="5ad51-157">**StorSimple capacities for local and cloud storage**</span><span class="sxs-lookup"><span data-stu-id="5ad51-157">**StorSimple capacities for local and cloud storage**</span></span>

| <span data-ttu-id="5ad51-158">Storage capacity</span><span class="sxs-lookup"><span data-stu-id="5ad51-158">Storage capacity</span></span>       | <span data-ttu-id="5ad51-159">8100</span><span class="sxs-lookup"><span data-stu-id="5ad51-159">8100</span></span>          | <span data-ttu-id="5ad51-160">8600</span><span class="sxs-lookup"><span data-stu-id="5ad51-160">8600</span></span>            |
|------------------------|---------------|-----------------|
| <span data-ttu-id="5ad51-161">Local storage capacity</span><span class="sxs-lookup"><span data-stu-id="5ad51-161">Local storage capacity</span></span> | <span data-ttu-id="5ad51-162">&lt; 10 TiB\*</span><span class="sxs-lookup"><span data-stu-id="5ad51-162">&lt; 10 TiB\*</span></span>  | <span data-ttu-id="5ad51-163">&lt; 20 TiB\*</span><span class="sxs-lookup"><span data-stu-id="5ad51-163">&lt; 20 TiB\*</span></span>  |
| <span data-ttu-id="5ad51-164">Cloud storage capacity</span><span class="sxs-lookup"><span data-stu-id="5ad51-164">Cloud storage capacity</span></span> | <span data-ttu-id="5ad51-165">&gt; 200 TiB\*</span><span class="sxs-lookup"><span data-stu-id="5ad51-165">&gt; 200 TiB\*</span></span> | <span data-ttu-id="5ad51-166">&gt; 500 TiB\*</span><span class="sxs-lookup"><span data-stu-id="5ad51-166">&gt; 500 TiB\*</span></span> |
<span data-ttu-id="5ad51-167">\* Storage size assumes no deduplication or compression.</span><span class="sxs-lookup"><span data-stu-id="5ad51-167">\* Storage size assumes no deduplication or compression.</span></span>

<span data-ttu-id="5ad51-168">**StorSimple capacities for primary and secondary backups**</span><span class="sxs-lookup"><span data-stu-id="5ad51-168">**StorSimple capacities for primary and secondary backups**</span></span>

| <span data-ttu-id="5ad51-169">Backup scenario</span><span class="sxs-lookup"><span data-stu-id="5ad51-169">Backup scenario</span></span>  | <span data-ttu-id="5ad51-170">Local storage capacity</span><span class="sxs-lookup"><span data-stu-id="5ad51-170">Local storage capacity</span></span>  | <span data-ttu-id="5ad51-171">Cloud storage capacity</span><span class="sxs-lookup"><span data-stu-id="5ad51-171">Cloud storage capacity</span></span>  |
|---|---|---|
| <span data-ttu-id="5ad51-172">Primary backup</span><span class="sxs-lookup"><span data-stu-id="5ad51-172">Primary backup</span></span>  | <span data-ttu-id="5ad51-173">Recent backups stored on local storage for fast recovery to meet recovery point objective (RPO)</span><span class="sxs-lookup"><span data-stu-id="5ad51-173">Recent backups stored on local storage for fast recovery to meet recovery point objective (RPO)</span></span> | <span data-ttu-id="5ad51-174">Backup history (RPO) fits in cloud capacity</span><span class="sxs-lookup"><span data-stu-id="5ad51-174">Backup history (RPO) fits in cloud capacity</span></span> |
| <span data-ttu-id="5ad51-175">Secondary backup</span><span class="sxs-lookup"><span data-stu-id="5ad51-175">Secondary backup</span></span> | <span data-ttu-id="5ad51-176">Secondary copy of backup data can be stored in cloud capacity</span><span class="sxs-lookup"><span data-stu-id="5ad51-176">Secondary copy of backup data can be stored in cloud capacity</span></span>  | <span data-ttu-id="5ad51-177">N/A</span><span class="sxs-lookup"><span data-stu-id="5ad51-177">N/A</span></span>  |

## <a name="storsimple-as-a-primary-backup-target"></a><span data-ttu-id="5ad51-178">StorSimple as a primary backup target</span><span class="sxs-lookup"><span data-stu-id="5ad51-178">StorSimple as a primary backup target</span></span>

<span data-ttu-id="5ad51-179">In this scenario, StorSimple volumes are presented to the backup application as the sole repository for backups.</span><span class="sxs-lookup"><span data-stu-id="5ad51-179">In this scenario, StorSimple volumes are presented to the backup application as the sole repository for backups.</span></span> <span data-ttu-id="5ad51-180">The following figure shows a solution architecture in which all backups use StorSimple tiered volumes for backups and restores.</span><span class="sxs-lookup"><span data-stu-id="5ad51-180">The following figure shows a solution architecture in which all backups use StorSimple tiered volumes for backups and restores.</span></span>

![StorSimple as a primary backup target logical diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a><span data-ttu-id="5ad51-182">Primary target backup logical steps</span><span class="sxs-lookup"><span data-stu-id="5ad51-182">Primary target backup logical steps</span></span>

1.  <span data-ttu-id="5ad51-183">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span><span class="sxs-lookup"><span data-stu-id="5ad51-183">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span></span>
2.  <span data-ttu-id="5ad51-184">The backup server writes data to the StorSimple tiered volumes.</span><span class="sxs-lookup"><span data-stu-id="5ad51-184">The backup server writes data to the StorSimple tiered volumes.</span></span>
3.  <span data-ttu-id="5ad51-185">The backup server updates the catalog database, and then finishes the backup job.</span><span class="sxs-lookup"><span data-stu-id="5ad51-185">The backup server updates the catalog database, and then finishes the backup job.</span></span>
4.  <span data-ttu-id="5ad51-186">A snapshot script triggers the StorSimple cloud snapshot manager (start or delete).</span><span class="sxs-lookup"><span data-stu-id="5ad51-186">A snapshot script triggers the StorSimple cloud snapshot manager (start or delete).</span></span>
5.  <span data-ttu-id="5ad51-187">The backup server deletes expired backups based on a retention policy.</span><span class="sxs-lookup"><span data-stu-id="5ad51-187">The backup server deletes expired backups based on a retention policy.</span></span>


### <a name="primary-target-restore-logical-steps"></a><span data-ttu-id="5ad51-188">Primary target restore logical steps</span><span class="sxs-lookup"><span data-stu-id="5ad51-188">Primary target restore logical steps</span></span>

1.  <span data-ttu-id="5ad51-189">The backup server starts restoring the appropriate data from the storage repository.</span><span class="sxs-lookup"><span data-stu-id="5ad51-189">The backup server starts restoring the appropriate data from the storage repository.</span></span>
2.  <span data-ttu-id="5ad51-190">The backup agent receives the data from the backup server.</span><span class="sxs-lookup"><span data-stu-id="5ad51-190">The backup agent receives the data from the backup server.</span></span>
3.  <span data-ttu-id="5ad51-191">The backup server finishes the restore job.</span><span class="sxs-lookup"><span data-stu-id="5ad51-191">The backup server finishes the restore job.</span></span>

## <a name="storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="5ad51-192">StorSimple as a secondary backup target</span><span class="sxs-lookup"><span data-stu-id="5ad51-192">StorSimple as a secondary backup target</span></span>

<span data-ttu-id="5ad51-193">In this scenario, StorSimple volumes primarily are used for long-term retention or archiving.</span><span class="sxs-lookup"><span data-stu-id="5ad51-193">In this scenario, StorSimple volumes primarily are used for long-term retention or archiving.</span></span>

<span data-ttu-id="5ad51-194">The following figure shows an architecture in which initial backups and restores target a high-performance volume.</span><span class="sxs-lookup"><span data-stu-id="5ad51-194">The following figure shows an architecture in which initial backups and restores target a high-performance volume.</span></span> <span data-ttu-id="5ad51-195">These backups are copied and archived to a StorSimple tiered volume on a set schedule.</span><span class="sxs-lookup"><span data-stu-id="5ad51-195">These backups are copied and archived to a StorSimple tiered volume on a set schedule.</span></span>

<span data-ttu-id="5ad51-196">It is important to size your high-performance volume so that it can handle your retention policy capacity and performance requirements.</span><span class="sxs-lookup"><span data-stu-id="5ad51-196">It is important to size your high-performance volume so that it can handle your retention policy capacity and performance requirements.</span></span>

![StorSimple as a secondary backup target logical diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a><span data-ttu-id="5ad51-198">Secondary target backup logical steps</span><span class="sxs-lookup"><span data-stu-id="5ad51-198">Secondary target backup logical steps</span></span>

1.  <span data-ttu-id="5ad51-199">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span><span class="sxs-lookup"><span data-stu-id="5ad51-199">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span></span>
2.  <span data-ttu-id="5ad51-200">The backup server writes data to high-performance storage.</span><span class="sxs-lookup"><span data-stu-id="5ad51-200">The backup server writes data to high-performance storage.</span></span>
3.  <span data-ttu-id="5ad51-201">The backup server updates the catalog database, and then finishes the backup job.</span><span class="sxs-lookup"><span data-stu-id="5ad51-201">The backup server updates the catalog database, and then finishes the backup job.</span></span>
4.  <span data-ttu-id="5ad51-202">The backup server copies backups to StorSimple based on a retention policy.</span><span class="sxs-lookup"><span data-stu-id="5ad51-202">The backup server copies backups to StorSimple based on a retention policy.</span></span>
5.  <span data-ttu-id="5ad51-203">A snapshot script triggers the StorSimple cloud snapshot manager (start or delete).</span><span class="sxs-lookup"><span data-stu-id="5ad51-203">A snapshot script triggers the StorSimple cloud snapshot manager (start or delete).</span></span>
6.  <span data-ttu-id="5ad51-204">The backup server deletes expired backups based on a retention policy.</span><span class="sxs-lookup"><span data-stu-id="5ad51-204">The backup server deletes expired backups based on a retention policy.</span></span>

### <a name="secondary-target-restore-logical-steps"></a><span data-ttu-id="5ad51-205">Secondary target restore logical steps</span><span class="sxs-lookup"><span data-stu-id="5ad51-205">Secondary target restore logical steps</span></span>

1.  <span data-ttu-id="5ad51-206">The backup server starts restoring the appropriate data from the storage repository.</span><span class="sxs-lookup"><span data-stu-id="5ad51-206">The backup server starts restoring the appropriate data from the storage repository.</span></span>
2.  <span data-ttu-id="5ad51-207">The backup agent receives the data from the backup server.</span><span class="sxs-lookup"><span data-stu-id="5ad51-207">The backup agent receives the data from the backup server.</span></span>
3.  <span data-ttu-id="5ad51-208">The backup server finishes the restore job.</span><span class="sxs-lookup"><span data-stu-id="5ad51-208">The backup server finishes the restore job.</span></span>

## <a name="deploy-the-solution"></a><span data-ttu-id="5ad51-209">Deploy the solution</span><span class="sxs-lookup"><span data-stu-id="5ad51-209">Deploy the solution</span></span>

<span data-ttu-id="5ad51-210">Deploying the solution requires three steps:</span><span class="sxs-lookup"><span data-stu-id="5ad51-210">Deploying the solution requires three steps:</span></span>
1. <span data-ttu-id="5ad51-211">Prepare the network infrastructure.</span><span class="sxs-lookup"><span data-stu-id="5ad51-211">Prepare the network infrastructure.</span></span>
2. <span data-ttu-id="5ad51-212">Deploy your StorSimple device as a backup target.</span><span class="sxs-lookup"><span data-stu-id="5ad51-212">Deploy your StorSimple device as a backup target.</span></span>
3. <span data-ttu-id="5ad51-213">Deploy Backup Exec.</span><span class="sxs-lookup"><span data-stu-id="5ad51-213">Deploy Backup Exec.</span></span>

<span data-ttu-id="5ad51-214">Each step is discussed in detail in the following sections.</span><span class="sxs-lookup"><span data-stu-id="5ad51-214">Each step is discussed in detail in the following sections.</span></span>

### <a name="set-up-the-network"></a><span data-ttu-id="5ad51-215">Set up the network</span><span class="sxs-lookup"><span data-stu-id="5ad51-215">Set up the network</span></span>

<span data-ttu-id="5ad51-216">Because StorSimple is a solution that's integrated with the Azure cloud, StorSimple requires an active and working connection to the Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="5ad51-216">Because StorSimple is a solution that's integrated with the Azure cloud, StorSimple requires an active and working connection to the Azure cloud.</span></span> <span data-ttu-id="5ad51-217">This connection is used for operations like cloud snapshots, management, and metadata transfer, and to tier older, less accessed data to Azure cloud storage.</span><span class="sxs-lookup"><span data-stu-id="5ad51-217">This connection is used for operations like cloud snapshots, management, and metadata transfer, and to tier older, less accessed data to Azure cloud storage.</span></span>

<span data-ttu-id="5ad51-218">For the solution to perform optimally, we recommend that you follow these networking best practices:</span><span class="sxs-lookup"><span data-stu-id="5ad51-218">For the solution to perform optimally, we recommend that you follow these networking best practices:</span></span>

-   <span data-ttu-id="5ad51-219">The link that connects your StorSimple tiering to Azure must meet your bandwidth requirements.</span><span class="sxs-lookup"><span data-stu-id="5ad51-219">The link that connects your StorSimple tiering to Azure must meet your bandwidth requirements.</span></span> <span data-ttu-id="5ad51-220">To achieve this, apply the necessary Quality of Service (QoS) level to your infrastructure switches to match your RPO and recovery time objective (RTO) SLAs.</span><span class="sxs-lookup"><span data-stu-id="5ad51-220">To achieve this, apply the necessary Quality of Service (QoS) level to your infrastructure switches to match your RPO and recovery time objective (RTO) SLAs.</span></span>
-   <span data-ttu-id="5ad51-221">Maximum Azure Blob storage access latencies should be around 80 ms.</span><span class="sxs-lookup"><span data-stu-id="5ad51-221">Maximum Azure Blob storage access latencies should be around 80 ms.</span></span>

### <a name="deploy-storsimple"></a><span data-ttu-id="5ad51-222">Deploy StorSimple</span><span class="sxs-lookup"><span data-stu-id="5ad51-222">Deploy StorSimple</span></span>

<span data-ttu-id="5ad51-223">For a step-by-step StorSimple deployment guidance, see [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span><span class="sxs-lookup"><span data-stu-id="5ad51-223">For a step-by-step StorSimple deployment guidance, see [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span></span>

### <a name="deploy-backup-exec"></a><span data-ttu-id="5ad51-224">Deploy Backup Exec</span><span class="sxs-lookup"><span data-stu-id="5ad51-224">Deploy Backup Exec</span></span>

<span data-ttu-id="5ad51-225">For Backup Exec installation best practices, see [Best practices for Backup Exec installation](https://www.veritas.com/support/en_US/article.000068207).</span><span class="sxs-lookup"><span data-stu-id="5ad51-225">For Backup Exec installation best practices, see [Best practices for Backup Exec installation](https://www.veritas.com/support/en_US/article.000068207).</span></span>

## <a name="set-up-the-solution"></a><span data-ttu-id="5ad51-226">Set up the solution</span><span class="sxs-lookup"><span data-stu-id="5ad51-226">Set up the solution</span></span>

<span data-ttu-id="5ad51-227">In this section, we demonstrate some configuration examples.</span><span class="sxs-lookup"><span data-stu-id="5ad51-227">In this section, we demonstrate some configuration examples.</span></span> <span data-ttu-id="5ad51-228">The following examples and recommendations illustrate the most basic and fundamental implementation.</span><span class="sxs-lookup"><span data-stu-id="5ad51-228">The following examples and recommendations illustrate the most basic and fundamental implementation.</span></span> <span data-ttu-id="5ad51-229">This implementation might not apply directly to your specific backup requirements.</span><span class="sxs-lookup"><span data-stu-id="5ad51-229">This implementation might not apply directly to your specific backup requirements.</span></span>

### <a name="set-up-storsimple"></a><span data-ttu-id="5ad51-230">Set up StorSimple</span><span class="sxs-lookup"><span data-stu-id="5ad51-230">Set up StorSimple</span></span>

| <span data-ttu-id="5ad51-231">StorSimple deployment tasks</span><span class="sxs-lookup"><span data-stu-id="5ad51-231">StorSimple deployment tasks</span></span>  | <span data-ttu-id="5ad51-232">Additional comments</span><span class="sxs-lookup"><span data-stu-id="5ad51-232">Additional comments</span></span> |
|---|---|
| <span data-ttu-id="5ad51-233">Deploy your on-premises StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="5ad51-233">Deploy your on-premises StorSimple device.</span></span> | <span data-ttu-id="5ad51-234">Supported versions: Update 3 and later versions.</span><span class="sxs-lookup"><span data-stu-id="5ad51-234">Supported versions: Update 3 and later versions.</span></span> |
| <span data-ttu-id="5ad51-235">Turn on the backup target.</span><span class="sxs-lookup"><span data-stu-id="5ad51-235">Turn on the backup target.</span></span> | <span data-ttu-id="5ad51-236">Use these commands to turn on or turn off backup target mode, and to get status.</span><span class="sxs-lookup"><span data-stu-id="5ad51-236">Use these commands to turn on or turn off backup target mode, and to get status.</span></span> <span data-ttu-id="5ad51-237">For more information, see [Connect remotely to a StorSimple device](storsimple-remote-connect.md).</span><span class="sxs-lookup"><span data-stu-id="5ad51-237">For more information, see [Connect remotely to a StorSimple device](storsimple-remote-connect.md).</span></span></br> <span data-ttu-id="5ad51-238">To turn on backup mode: `Set-HCSBackupApplianceMode -enable`.</span><span class="sxs-lookup"><span data-stu-id="5ad51-238">To turn on backup mode: `Set-HCSBackupApplianceMode -enable`.</span></span> </br> <span data-ttu-id="5ad51-239">To turn off backup mode: `Set-HCSBackupApplianceMode -disable`.</span><span class="sxs-lookup"><span data-stu-id="5ad51-239">To turn off backup mode: `Set-HCSBackupApplianceMode -disable`.</span></span> </br> <span data-ttu-id="5ad51-240">To get the current state of backup mode settings: `Get-HCSBackupApplianceMode`.</span><span class="sxs-lookup"><span data-stu-id="5ad51-240">To get the current state of backup mode settings: `Get-HCSBackupApplianceMode`.</span></span> |
| <span data-ttu-id="5ad51-241">Create a common volume container for your volume that stores the backup data.</span><span class="sxs-lookup"><span data-stu-id="5ad51-241">Create a common volume container for your volume that stores the backup data.</span></span> <span data-ttu-id="5ad51-242">All data in a volume container is deduplicated.</span><span class="sxs-lookup"><span data-stu-id="5ad51-242">All data in a volume container is deduplicated.</span></span> | <span data-ttu-id="5ad51-243">StorSimple volume containers define deduplication domains.</span><span class="sxs-lookup"><span data-stu-id="5ad51-243">StorSimple volume containers define deduplication domains.</span></span>  |
| <span data-ttu-id="5ad51-244">Create StorSimple volumes.</span><span class="sxs-lookup"><span data-stu-id="5ad51-244">Create StorSimple volumes.</span></span> | <span data-ttu-id="5ad51-245">Create volumes with sizes as close to the anticipated usage as possible, because volume size affects cloud snapshot duration time.</span><span class="sxs-lookup"><span data-stu-id="5ad51-245">Create volumes with sizes as close to the anticipated usage as possible, because volume size affects cloud snapshot duration time.</span></span> <span data-ttu-id="5ad51-246">For information about how to size a volume, read about [retention policies](#retention-policies).</span><span class="sxs-lookup"><span data-stu-id="5ad51-246">For information about how to size a volume, read about [retention policies](#retention-policies).</span></span></br> </br> <span data-ttu-id="5ad51-247">Use StorSimple tiered volumes, and select the **Use this volume for less frequently accessed archival data** check box.</span><span class="sxs-lookup"><span data-stu-id="5ad51-247">Use StorSimple tiered volumes, and select the **Use this volume for less frequently accessed archival data** check box.</span></span> </br> <span data-ttu-id="5ad51-248">Using only locally pinned volumes is not supported.</span><span class="sxs-lookup"><span data-stu-id="5ad51-248">Using only locally pinned volumes is not supported.</span></span> |
| <span data-ttu-id="5ad51-249">Create a unique StorSimple backup policy for all the backup target volumes.</span><span class="sxs-lookup"><span data-stu-id="5ad51-249">Create a unique StorSimple backup policy for all the backup target volumes.</span></span> | <span data-ttu-id="5ad51-250">A StorSimple backup policy defines the volume consistency group.</span><span class="sxs-lookup"><span data-stu-id="5ad51-250">A StorSimple backup policy defines the volume consistency group.</span></span> |
| <span data-ttu-id="5ad51-251">Disable the schedule as the snapshots expire.</span><span class="sxs-lookup"><span data-stu-id="5ad51-251">Disable the schedule as the snapshots expire.</span></span> | <span data-ttu-id="5ad51-252">Snapshots are triggered as a post-processing operation.</span><span class="sxs-lookup"><span data-stu-id="5ad51-252">Snapshots are triggered as a post-processing operation.</span></span> |

### <a name="set-up-the-host-backup-server-storage"></a><span data-ttu-id="5ad51-253">Set up the host backup server storage</span><span class="sxs-lookup"><span data-stu-id="5ad51-253">Set up the host backup server storage</span></span>

<span data-ttu-id="5ad51-254">Set up the host backup server storage according to these guidelines:</span><span class="sxs-lookup"><span data-stu-id="5ad51-254">Set up the host backup server storage according to these guidelines:</span></span>  

- <span data-ttu-id="5ad51-255">Don't use spanned volumes (created by Windows Disk Management).</span><span class="sxs-lookup"><span data-stu-id="5ad51-255">Don't use spanned volumes (created by Windows Disk Management).</span></span> <span data-ttu-id="5ad51-256">Spanned disks are not supported.</span><span class="sxs-lookup"><span data-stu-id="5ad51-256">Spanned disks are not supported.</span></span>
- <span data-ttu-id="5ad51-257">Format your volumes using NTFS with 64-KB allocation size.</span><span class="sxs-lookup"><span data-stu-id="5ad51-257">Format your volumes using NTFS with 64-KB allocation size.</span></span>
- <span data-ttu-id="5ad51-258">Map the StorSimple volumes directly to the Backup Exec server.</span><span class="sxs-lookup"><span data-stu-id="5ad51-258">Map the StorSimple volumes directly to the Backup Exec server.</span></span>
    - <span data-ttu-id="5ad51-259">Use iSCSI for physical servers.</span><span class="sxs-lookup"><span data-stu-id="5ad51-259">Use iSCSI for physical servers.</span></span>
    - <span data-ttu-id="5ad51-260">Use pass-through disks for virtual servers.</span><span class="sxs-lookup"><span data-stu-id="5ad51-260">Use pass-through disks for virtual servers.</span></span>

## <a name="best-practices-for-storsimple-and-backup-exec"></a><span data-ttu-id="5ad51-261">Best practices for StorSimple and Backup Exec</span><span class="sxs-lookup"><span data-stu-id="5ad51-261">Best practices for StorSimple and Backup Exec</span></span>

<span data-ttu-id="5ad51-262">Set up your solution according to the guidelines in the following sections.</span><span class="sxs-lookup"><span data-stu-id="5ad51-262">Set up your solution according to the guidelines in the following sections.</span></span>

### <a name="operating-system-best-practices"></a><span data-ttu-id="5ad51-263">Operating system best practices</span><span class="sxs-lookup"><span data-stu-id="5ad51-263">Operating system best practices</span></span>

-   <span data-ttu-id="5ad51-264">Disable Windows Server encryption and deduplication for the NTFS file system.</span><span class="sxs-lookup"><span data-stu-id="5ad51-264">Disable Windows Server encryption and deduplication for the NTFS file system.</span></span>
-   <span data-ttu-id="5ad51-265">Disable Windows Server defragmentation on the StorSimple volumes.</span><span class="sxs-lookup"><span data-stu-id="5ad51-265">Disable Windows Server defragmentation on the StorSimple volumes.</span></span>
-   <span data-ttu-id="5ad51-266">Disable Windows Server indexing on the StorSimple volumes.</span><span class="sxs-lookup"><span data-stu-id="5ad51-266">Disable Windows Server indexing on the StorSimple volumes.</span></span>
-   <span data-ttu-id="5ad51-267">Run an antivirus scan at the source host (not against the StorSimple volumes).</span><span class="sxs-lookup"><span data-stu-id="5ad51-267">Run an antivirus scan at the source host (not against the StorSimple volumes).</span></span>
-   <span data-ttu-id="5ad51-268">Turn off the default [Windows Server maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) in Task Manager.</span><span class="sxs-lookup"><span data-stu-id="5ad51-268">Turn off the default [Windows Server maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) in Task Manager.</span></span> <span data-ttu-id="5ad51-269">Do this in one of the following ways:</span><span class="sxs-lookup"><span data-stu-id="5ad51-269">Do this in one of the following ways:</span></span>
   - <span data-ttu-id="5ad51-270">Turn off the Maintenance configurator in Windows Task Scheduler.</span><span class="sxs-lookup"><span data-stu-id="5ad51-270">Turn off the Maintenance configurator in Windows Task Scheduler.</span></span>
   - <span data-ttu-id="5ad51-271">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) from Windows Sysinternals.</span><span class="sxs-lookup"><span data-stu-id="5ad51-271">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) from Windows Sysinternals.</span></span> <span data-ttu-id="5ad51-272">After you download PsExec, run Azure PowerShell as an administrator, and type:</span><span class="sxs-lookup"><span data-stu-id="5ad51-272">After you download PsExec, run Azure PowerShell as an administrator, and type:</span></span>
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a><span data-ttu-id="5ad51-273">StorSimple best practices</span><span class="sxs-lookup"><span data-stu-id="5ad51-273">StorSimple best practices</span></span>

  -   <span data-ttu-id="5ad51-274">Be sure that the StorSimple device is updated to [Update 3 or later](storsimple-install-update-3.md).</span><span class="sxs-lookup"><span data-stu-id="5ad51-274">Be sure that the StorSimple device is updated to [Update 3 or later](storsimple-install-update-3.md).</span></span>
  -   <span data-ttu-id="5ad51-275">Isolate iSCSI and cloud traffic.</span><span class="sxs-lookup"><span data-stu-id="5ad51-275">Isolate iSCSI and cloud traffic.</span></span> <span data-ttu-id="5ad51-276">Use dedicated iSCSI connections for traffic between StorSimple and the backup server.</span><span class="sxs-lookup"><span data-stu-id="5ad51-276">Use dedicated iSCSI connections for traffic between StorSimple and the backup server.</span></span>
  -   <span data-ttu-id="5ad51-277">Be sure that your StorSimple device is a dedicated backup target.</span><span class="sxs-lookup"><span data-stu-id="5ad51-277">Be sure that your StorSimple device is a dedicated backup target.</span></span> <span data-ttu-id="5ad51-278">Mixed workloads are not supported because they affect your RTO and RPO.</span><span class="sxs-lookup"><span data-stu-id="5ad51-278">Mixed workloads are not supported because they affect your RTO and RPO.</span></span>

### <a name="backup-exec-best-practices"></a><span data-ttu-id="5ad51-279">Backup Exec best practices</span><span class="sxs-lookup"><span data-stu-id="5ad51-279">Backup Exec best practices</span></span>

-   <span data-ttu-id="5ad51-280">Backup Exec must be installed on a local drive of the server, and not on a StorSimple volume.</span><span class="sxs-lookup"><span data-stu-id="5ad51-280">Backup Exec must be installed on a local drive of the server, and not on a StorSimple volume.</span></span>
-   <span data-ttu-id="5ad51-281">Set the Backup Exec storage **concurrent write operations** to the maximum allowed.</span><span class="sxs-lookup"><span data-stu-id="5ad51-281">Set the Backup Exec storage **concurrent write operations** to the maximum allowed.</span></span>
    -   <span data-ttu-id="5ad51-282">Set the Backup Exec storage **block and buffer size** to 512 KB.</span><span class="sxs-lookup"><span data-stu-id="5ad51-282">Set the Backup Exec storage **block and buffer size** to 512 KB.</span></span>
    -   <span data-ttu-id="5ad51-283">Turn on Backup Exec storage **buffered read and write**.</span><span class="sxs-lookup"><span data-stu-id="5ad51-283">Turn on Backup Exec storage **buffered read and write**.</span></span>
-   <span data-ttu-id="5ad51-284">StorSimple supports Backup Exec full and incremental backups.</span><span class="sxs-lookup"><span data-stu-id="5ad51-284">StorSimple supports Backup Exec full and incremental backups.</span></span> <span data-ttu-id="5ad51-285">We recommend that you not use synthetic and differential backups.</span><span class="sxs-lookup"><span data-stu-id="5ad51-285">We recommend that you not use synthetic and differential backups.</span></span>
-   <span data-ttu-id="5ad51-286">Backup data files should contain data only for a specific job.</span><span class="sxs-lookup"><span data-stu-id="5ad51-286">Backup data files should contain data only for a specific job.</span></span> <span data-ttu-id="5ad51-287">For example, no media appends across different jobs are allowed.</span><span class="sxs-lookup"><span data-stu-id="5ad51-287">For example, no media appends across different jobs are allowed.</span></span>
-   <span data-ttu-id="5ad51-288">Disable job verification.</span><span class="sxs-lookup"><span data-stu-id="5ad51-288">Disable job verification.</span></span> <span data-ttu-id="5ad51-289">If necessary, verification should be scheduled after the latest backup job.</span><span class="sxs-lookup"><span data-stu-id="5ad51-289">If necessary, verification should be scheduled after the latest backup job.</span></span> <span data-ttu-id="5ad51-290">It is important to understand that this job affects your backup window.</span><span class="sxs-lookup"><span data-stu-id="5ad51-290">It is important to understand that this job affects your backup window.</span></span>
-   <span data-ttu-id="5ad51-291">Select **Storage** > **Your disk** > **Details** > **Properties**.</span><span class="sxs-lookup"><span data-stu-id="5ad51-291">Select **Storage** > **Your disk** > **Details** > **Properties**.</span></span> <span data-ttu-id="5ad51-292">Turn off **Pre-allocate disk space**.</span><span class="sxs-lookup"><span data-stu-id="5ad51-292">Turn off **Pre-allocate disk space**.</span></span>

<span data-ttu-id="5ad51-293">For the latest Backup Exec settings and best practices for implementing these requirements, see [the Veritas website](https://www.veritas.com).</span><span class="sxs-lookup"><span data-stu-id="5ad51-293">For the latest Backup Exec settings and best practices for implementing these requirements, see [the Veritas website](https://www.veritas.com).</span></span>

## <a name="retention-policies"></a><span data-ttu-id="5ad51-294">Retention policies</span><span class="sxs-lookup"><span data-stu-id="5ad51-294">Retention policies</span></span>

<span data-ttu-id="5ad51-295">One of the most common backup retention policy types is a Grandfather, Father, and Son (GFS) policy.</span><span class="sxs-lookup"><span data-stu-id="5ad51-295">One of the most common backup retention policy types is a Grandfather, Father, and Son (GFS) policy.</span></span> <span data-ttu-id="5ad51-296">In a GFS policy, an incremental backup is performed daily and full backups are done weekly and monthly.</span><span class="sxs-lookup"><span data-stu-id="5ad51-296">In a GFS policy, an incremental backup is performed daily and full backups are done weekly and monthly.</span></span> <span data-ttu-id="5ad51-297">This policy results in six StorSimple tiered volumes.</span><span class="sxs-lookup"><span data-stu-id="5ad51-297">This policy results in six StorSimple tiered volumes.</span></span> <span data-ttu-id="5ad51-298">One volume contains the weekly, monthly, and yearly full backups.</span><span class="sxs-lookup"><span data-stu-id="5ad51-298">One volume contains the weekly, monthly, and yearly full backups.</span></span> <span data-ttu-id="5ad51-299">The other five volumes store daily incremental backups.</span><span class="sxs-lookup"><span data-stu-id="5ad51-299">The other five volumes store daily incremental backups.</span></span>

<span data-ttu-id="5ad51-300">In the following example, we use a GFS rotation.</span><span class="sxs-lookup"><span data-stu-id="5ad51-300">In the following example, we use a GFS rotation.</span></span> <span data-ttu-id="5ad51-301">The example assumes the following:</span><span class="sxs-lookup"><span data-stu-id="5ad51-301">The example assumes the following:</span></span>

-   <span data-ttu-id="5ad51-302">Non-deduped or compressed data is used.</span><span class="sxs-lookup"><span data-stu-id="5ad51-302">Non-deduped or compressed data is used.</span></span>
-   <span data-ttu-id="5ad51-303">Full backups are 1 TiB each.</span><span class="sxs-lookup"><span data-stu-id="5ad51-303">Full backups are 1 TiB each.</span></span>
-   <span data-ttu-id="5ad51-304">Daily incremental backups are 500 GiB each.</span><span class="sxs-lookup"><span data-stu-id="5ad51-304">Daily incremental backups are 500 GiB each.</span></span>
-   <span data-ttu-id="5ad51-305">Four weekly backups are kept for a month.</span><span class="sxs-lookup"><span data-stu-id="5ad51-305">Four weekly backups are kept for a month.</span></span>
-   <span data-ttu-id="5ad51-306">Twelve monthly backups are kept for a year.</span><span class="sxs-lookup"><span data-stu-id="5ad51-306">Twelve monthly backups are kept for a year.</span></span>
-   <span data-ttu-id="5ad51-307">One yearly backup is kept for 10 years.</span><span class="sxs-lookup"><span data-stu-id="5ad51-307">One yearly backup is kept for 10 years.</span></span>

<span data-ttu-id="5ad51-308">Based on the preceding assumptions, create a 26-TiB StorSimple tiered volume for the monthly and yearly full backups.</span><span class="sxs-lookup"><span data-stu-id="5ad51-308">Based on the preceding assumptions, create a 26-TiB StorSimple tiered volume for the monthly and yearly full backups.</span></span> <span data-ttu-id="5ad51-309">Create a 5-TiB StorSimple tiered volume for each of the incremental daily backups.</span><span class="sxs-lookup"><span data-stu-id="5ad51-309">Create a 5-TiB StorSimple tiered volume for each of the incremental daily backups.</span></span>

| <span data-ttu-id="5ad51-310">Backup type retention</span><span class="sxs-lookup"><span data-stu-id="5ad51-310">Backup type retention</span></span> | <span data-ttu-id="5ad51-311">Size (TiB)</span><span class="sxs-lookup"><span data-stu-id="5ad51-311">Size (TiB)</span></span> | <span data-ttu-id="5ad51-312">GFS multiplier\*</span><span class="sxs-lookup"><span data-stu-id="5ad51-312">GFS multiplier\*</span></span> | <span data-ttu-id="5ad51-313">Total capacity (TiB)</span><span class="sxs-lookup"><span data-stu-id="5ad51-313">Total capacity (TiB)</span></span>  |
|---|---|---|---|
| <span data-ttu-id="5ad51-314">Weekly full</span><span class="sxs-lookup"><span data-stu-id="5ad51-314">Weekly full</span></span> | <span data-ttu-id="5ad51-315">1</span><span class="sxs-lookup"><span data-stu-id="5ad51-315">1</span></span> | <span data-ttu-id="5ad51-316">4</span><span class="sxs-lookup"><span data-stu-id="5ad51-316">4</span></span>  | <span data-ttu-id="5ad51-317">4</span><span class="sxs-lookup"><span data-stu-id="5ad51-317">4</span></span> |
| <span data-ttu-id="5ad51-318">Daily incremental</span><span class="sxs-lookup"><span data-stu-id="5ad51-318">Daily incremental</span></span> | <span data-ttu-id="5ad51-319">0.5</span><span class="sxs-lookup"><span data-stu-id="5ad51-319">0.5</span></span> | <span data-ttu-id="5ad51-320">20 (cycles equal number of weeks per month)</span><span class="sxs-lookup"><span data-stu-id="5ad51-320">20 (cycles equal number of weeks per month)</span></span> | <span data-ttu-id="5ad51-321">12 (2 for additional quota)</span><span class="sxs-lookup"><span data-stu-id="5ad51-321">12 (2 for additional quota)</span></span> |
| <span data-ttu-id="5ad51-322">Monthly full</span><span class="sxs-lookup"><span data-stu-id="5ad51-322">Monthly full</span></span> | <span data-ttu-id="5ad51-323">1</span><span class="sxs-lookup"><span data-stu-id="5ad51-323">1</span></span> | <span data-ttu-id="5ad51-324">12</span><span class="sxs-lookup"><span data-stu-id="5ad51-324">12</span></span> | <span data-ttu-id="5ad51-325">12</span><span class="sxs-lookup"><span data-stu-id="5ad51-325">12</span></span> |
| <span data-ttu-id="5ad51-326">Yearly full</span><span class="sxs-lookup"><span data-stu-id="5ad51-326">Yearly full</span></span> | <span data-ttu-id="5ad51-327">1</span><span class="sxs-lookup"><span data-stu-id="5ad51-327">1</span></span>  | <span data-ttu-id="5ad51-328">10</span><span class="sxs-lookup"><span data-stu-id="5ad51-328">10</span></span> | <span data-ttu-id="5ad51-329">10</span><span class="sxs-lookup"><span data-stu-id="5ad51-329">10</span></span> |
| <span data-ttu-id="5ad51-330">GFS requirement</span><span class="sxs-lookup"><span data-stu-id="5ad51-330">GFS requirement</span></span> |   | <span data-ttu-id="5ad51-331">38</span><span class="sxs-lookup"><span data-stu-id="5ad51-331">38</span></span> |   |
| <span data-ttu-id="5ad51-332">Additional quota</span><span class="sxs-lookup"><span data-stu-id="5ad51-332">Additional quota</span></span>  | <span data-ttu-id="5ad51-333">4</span><span class="sxs-lookup"><span data-stu-id="5ad51-333">4</span></span>  |   | <span data-ttu-id="5ad51-334">42 total GFS requirement</span><span class="sxs-lookup"><span data-stu-id="5ad51-334">42 total GFS requirement</span></span>  |
<span data-ttu-id="5ad51-335">\* The GFS multiplier is the number of copies you need to protect and retain to meet your backup policy requirements.</span><span class="sxs-lookup"><span data-stu-id="5ad51-335">\* The GFS multiplier is the number of copies you need to protect and retain to meet your backup policy requirements.</span></span>

## <a name="set-up-backup-exec-storage"></a><span data-ttu-id="5ad51-336">Set up Backup Exec storage</span><span class="sxs-lookup"><span data-stu-id="5ad51-336">Set up Backup Exec storage</span></span>

### <a name="to-set-up-backup-exec-storage"></a><span data-ttu-id="5ad51-337">To set up Backup Exec storage</span><span class="sxs-lookup"><span data-stu-id="5ad51-337">To set up Backup Exec storage</span></span>

1.  <span data-ttu-id="5ad51-338">In the Backup Exec management console, select **Storage** > **Configure Storage** > **Disk-Based Storage** > **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ad51-338">In the Backup Exec management console, select **Storage** > **Configure Storage** > **Disk-Based Storage** > **Next**.</span></span>

    ![Backup Exec management console, configure storage page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/image4.png)

2.  <span data-ttu-id="5ad51-340">Select **Disk Storage**, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ad51-340">Select **Disk Storage**, and then select **Next**.</span></span>

    ![Backup Exec management console, select storage page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/image5.png)

3.  <span data-ttu-id="5ad51-342">Enter a representative name, for example, **Saturday Full**, and a description.</span><span class="sxs-lookup"><span data-stu-id="5ad51-342">Enter a representative name, for example, **Saturday Full**, and a description.</span></span> <span data-ttu-id="5ad51-343">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ad51-343">Select **Next**.</span></span>

    ![Backup Exec management console, name and description page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/image7.png)

4.  <span data-ttu-id="5ad51-345">Select the disk where you want to create the disk storage device, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ad51-345">Select the disk where you want to create the disk storage device, and then select **Next**.</span></span>

    ![Backup Exec management console, storage disk selection page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/image9.png)

5.  <span data-ttu-id="5ad51-347">Increment the number of write operations to **16**, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ad51-347">Increment the number of write operations to **16**, and then select **Next**.</span></span>

    ![Backup Exec management console, concurrent write operations settings page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/image10.png)

6.  <span data-ttu-id="5ad51-349">Review the settings, and then select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="5ad51-349">Review the settings, and then select **Finish**.</span></span>

    ![Backup Exec management console, storage configuration summary page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/image11.png)

7.  <span data-ttu-id="5ad51-351">At the end of each volume assignment, change the storage device settings to match those recommended at [Best practices for StorSimple and Backup Exec](#best-practices-for-storsimple-and-backup-exec).</span><span class="sxs-lookup"><span data-stu-id="5ad51-351">At the end of each volume assignment, change the storage device settings to match those recommended at [Best practices for StorSimple and Backup Exec](#best-practices-for-storsimple-and-backup-exec).</span></span>

    ![Backup Exec management console, storage device settings page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/image12.png)

8.  <span data-ttu-id="5ad51-353">Repeat steps 1-7 until you are finished assigning your StorSimple volumes to Backup Exec.</span><span class="sxs-lookup"><span data-stu-id="5ad51-353">Repeat steps 1-7 until you are finished assigning your StorSimple volumes to Backup Exec.</span></span>

## <a name="set-up-storsimple-as-a-primary-backup-target"></a><span data-ttu-id="5ad51-354">Set up StorSimple as a primary backup target</span><span class="sxs-lookup"><span data-stu-id="5ad51-354">Set up StorSimple as a primary backup target</span></span>

> [!NOTE]
> <span data-ttu-id="5ad51-355">Data restore from a backup that has been tiered to the cloud occurs at cloud speeds.</span><span class="sxs-lookup"><span data-stu-id="5ad51-355">Data restore from a backup that has been tiered to the cloud occurs at cloud speeds.</span></span>

<span data-ttu-id="5ad51-356">The following figure shows the mapping of a typical volume to a backup job.</span><span class="sxs-lookup"><span data-stu-id="5ad51-356">The following figure shows the mapping of a typical volume to a backup job.</span></span> <span data-ttu-id="5ad51-357">In this case, all the weekly backups map to the Saturday full disk, and the incremental backups map to Monday-Friday incremental disks.</span><span class="sxs-lookup"><span data-stu-id="5ad51-357">In this case, all the weekly backups map to the Saturday full disk, and the incremental backups map to Monday-Friday incremental disks.</span></span> <span data-ttu-id="5ad51-358">All the backups and restores are from a StorSimple tiered volume.</span><span class="sxs-lookup"><span data-stu-id="5ad51-358">All the backups and restores are from a StorSimple tiered volume.</span></span>

![Primary backup target configuration logical diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a><span data-ttu-id="5ad51-360">StorSimple as a primary backup target GFS schedule example</span><span class="sxs-lookup"><span data-stu-id="5ad51-360">StorSimple as a primary backup target GFS schedule example</span></span>

<span data-ttu-id="5ad51-361">Here's an example of a GFS rotation schedule for four weeks, monthly, and yearly:</span><span class="sxs-lookup"><span data-stu-id="5ad51-361">Here's an example of a GFS rotation schedule for four weeks, monthly, and yearly:</span></span>

| <span data-ttu-id="5ad51-362">Frequency/backup type</span><span class="sxs-lookup"><span data-stu-id="5ad51-362">Frequency/backup type</span></span> | <span data-ttu-id="5ad51-363">Full</span><span class="sxs-lookup"><span data-stu-id="5ad51-363">Full</span></span> | <span data-ttu-id="5ad51-364">Incremental (days 1-5)</span><span class="sxs-lookup"><span data-stu-id="5ad51-364">Incremental (days 1-5)</span></span>  |   
|---|---|---|
| <span data-ttu-id="5ad51-365">Weekly (weeks 1-4)</span><span class="sxs-lookup"><span data-stu-id="5ad51-365">Weekly (weeks 1-4)</span></span> | <span data-ttu-id="5ad51-366">Saturday</span><span class="sxs-lookup"><span data-stu-id="5ad51-366">Saturday</span></span> | <span data-ttu-id="5ad51-367">Monday-Friday</span><span class="sxs-lookup"><span data-stu-id="5ad51-367">Monday-Friday</span></span> |
| <span data-ttu-id="5ad51-368">Monthly</span><span class="sxs-lookup"><span data-stu-id="5ad51-368">Monthly</span></span>  | <span data-ttu-id="5ad51-369">Saturday</span><span class="sxs-lookup"><span data-stu-id="5ad51-369">Saturday</span></span>  |   |
| <span data-ttu-id="5ad51-370">Yearly</span><span class="sxs-lookup"><span data-stu-id="5ad51-370">Yearly</span></span> | <span data-ttu-id="5ad51-371">Saturday</span><span class="sxs-lookup"><span data-stu-id="5ad51-371">Saturday</span></span>  |   |   |


### <a name="assign-storsimple-volumes-to-a-backup-exec-backup-job"></a><span data-ttu-id="5ad51-372">Assign StorSimple volumes to a Backup Exec backup job</span><span class="sxs-lookup"><span data-stu-id="5ad51-372">Assign StorSimple volumes to a Backup Exec backup job</span></span>

<span data-ttu-id="5ad51-373">The following sequence assumes that Backup Exec and the target host are configured in accordance with the Backup Exec agent guidelines.</span><span class="sxs-lookup"><span data-stu-id="5ad51-373">The following sequence assumes that Backup Exec and the target host are configured in accordance with the Backup Exec agent guidelines.</span></span>

#### <a name="to-assign-storsimple-volumes-to-a-backup-exec-backup-job"></a><span data-ttu-id="5ad51-374">To assign StorSimple volumes to a Backup Exec backup job</span><span class="sxs-lookup"><span data-stu-id="5ad51-374">To assign StorSimple volumes to a Backup Exec backup job</span></span>

1.  <span data-ttu-id="5ad51-375">In the Backup Exec management console, select **Host** > **Backup** > **Backup to Disk**.</span><span class="sxs-lookup"><span data-stu-id="5ad51-375">In the Backup Exec management console, select **Host** > **Backup** > **Backup to Disk**.</span></span>

    ![Backup Exec management console, select host, backup, and backup to disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/image14.png)

2.  <span data-ttu-id="5ad51-377">In the **Backup Definition Properties** dialog box, under **Backup**, select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="5ad51-377">In the **Backup Definition Properties** dialog box, under **Backup**, select **Edit**.</span></span>

    ![Backup Exec management console, Backup Definition Properties dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/image15.png)

3.  <span data-ttu-id="5ad51-379">Set up your full and incremental backups so that they meet your RPO and RTO requirements and conform to Veritas best practices.</span><span class="sxs-lookup"><span data-stu-id="5ad51-379">Set up your full and incremental backups so that they meet your RPO and RTO requirements and conform to Veritas best practices.</span></span>

4.  <span data-ttu-id="5ad51-380">In the **Backup Options** dialog box, select **Storage**.</span><span class="sxs-lookup"><span data-stu-id="5ad51-380">In the **Backup Options** dialog box, select **Storage**.</span></span>

    ![Backup Exec management console, Backup Options Storage dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/image16.png)

5.  <span data-ttu-id="5ad51-382">Assign corresponding StorSimple volumes to your backup schedule.</span><span class="sxs-lookup"><span data-stu-id="5ad51-382">Assign corresponding StorSimple volumes to your backup schedule.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ad51-383">**Compression** and **Encryption type** are set to **None**.</span><span class="sxs-lookup"><span data-stu-id="5ad51-383">**Compression** and **Encryption type** are set to **None**.</span></span>

6.  <span data-ttu-id="5ad51-384">Under **Verify**, select the **Do not verify data for this job** check box.</span><span class="sxs-lookup"><span data-stu-id="5ad51-384">Under **Verify**, select the **Do not verify data for this job** check box.</span></span> <span data-ttu-id="5ad51-385">Using this option might affect StorSimple tiering.</span><span class="sxs-lookup"><span data-stu-id="5ad51-385">Using this option might affect StorSimple tiering.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5ad51-386">Defragmentation, indexing, and background verification negatively affect the StorSimple tiering.</span><span class="sxs-lookup"><span data-stu-id="5ad51-386">Defragmentation, indexing, and background verification negatively affect the StorSimple tiering.</span></span>

    ![Backup Exec management console, Backup Options verify settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/image17.png)

7.  <span data-ttu-id="5ad51-388">When you've set up the rest of your backup options to meet your requirements, select **OK** to finish.</span><span class="sxs-lookup"><span data-stu-id="5ad51-388">When you've set up the rest of your backup options to meet your requirements, select **OK** to finish.</span></span>

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="5ad51-389">Set up StorSimple as a secondary backup target</span><span class="sxs-lookup"><span data-stu-id="5ad51-389">Set up StorSimple as a secondary backup target</span></span>

> [!NOTE]
><span data-ttu-id="5ad51-390">Data restores from a backup that has been tiered to the cloud occur at cloud speeds.</span><span class="sxs-lookup"><span data-stu-id="5ad51-390">Data restores from a backup that has been tiered to the cloud occur at cloud speeds.</span></span>

<span data-ttu-id="5ad51-391">In this model, you must have a storage media (other than StorSimple) to serve as a temporary cache.</span><span class="sxs-lookup"><span data-stu-id="5ad51-391">In this model, you must have a storage media (other than StorSimple) to serve as a temporary cache.</span></span> <span data-ttu-id="5ad51-392">For example, you can use a redundant array of independent disks (RAID) volume to accommodate space, input/output (I/O), and bandwidth.</span><span class="sxs-lookup"><span data-stu-id="5ad51-392">For example, you can use a redundant array of independent disks (RAID) volume to accommodate space, input/output (I/O), and bandwidth.</span></span> <span data-ttu-id="5ad51-393">We recommend using RAID 5, 50, and 10.</span><span class="sxs-lookup"><span data-stu-id="5ad51-393">We recommend using RAID 5, 50, and 10.</span></span>

<span data-ttu-id="5ad51-394">The following figure shows typical short-term retention local (to the server) volumes and long-term retention archives volumes.</span><span class="sxs-lookup"><span data-stu-id="5ad51-394">The following figure shows typical short-term retention local (to the server) volumes and long-term retention archives volumes.</span></span> <span data-ttu-id="5ad51-395">In this scenario, all backups run on the local (to the server) RAID volume.</span><span class="sxs-lookup"><span data-stu-id="5ad51-395">In this scenario, all backups run on the local (to the server) RAID volume.</span></span> <span data-ttu-id="5ad51-396">These backups are periodically duplicated and archived to an archives volume.</span><span class="sxs-lookup"><span data-stu-id="5ad51-396">These backups are periodically duplicated and archived to an archives volume.</span></span> <span data-ttu-id="5ad51-397">It is important to size your local (to the server) RAID volume so that it can handle your short-term retention capacity and performance requirements.</span><span class="sxs-lookup"><span data-stu-id="5ad51-397">It is important to size your local (to the server) RAID volume so that it can handle your short-term retention capacity and performance requirements.</span></span>

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a><span data-ttu-id="5ad51-398">StorSimple as a secondary backup target GFS example</span><span class="sxs-lookup"><span data-stu-id="5ad51-398">StorSimple as a secondary backup target GFS example</span></span>

![StorSimple as secondary backup target logical diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetdiagram.png)

<span data-ttu-id="5ad51-400">The following table shows how to set up backups to run on the local and StorSimple disks.</span><span class="sxs-lookup"><span data-stu-id="5ad51-400">The following table shows how to set up backups to run on the local and StorSimple disks.</span></span> <span data-ttu-id="5ad51-401">It includes individual and total capacity requirements.</span><span class="sxs-lookup"><span data-stu-id="5ad51-401">It includes individual and total capacity requirements.</span></span>

### <a name="backup-configuration-and-capacity-requirements"></a><span data-ttu-id="5ad51-402">Backup configuration and capacity requirements</span><span class="sxs-lookup"><span data-stu-id="5ad51-402">Backup configuration and capacity requirements</span></span>

| <span data-ttu-id="5ad51-403">Backup type and retention</span><span class="sxs-lookup"><span data-stu-id="5ad51-403">Backup type and retention</span></span> | <span data-ttu-id="5ad51-404">Configured storage</span><span class="sxs-lookup"><span data-stu-id="5ad51-404">Configured storage</span></span> | <span data-ttu-id="5ad51-405">Size (TiB)</span><span class="sxs-lookup"><span data-stu-id="5ad51-405">Size (TiB)</span></span> | <span data-ttu-id="5ad51-406">GFS multiplier</span><span class="sxs-lookup"><span data-stu-id="5ad51-406">GFS multiplier</span></span> | <span data-ttu-id="5ad51-407">Total capacity\* (TiB)</span><span class="sxs-lookup"><span data-stu-id="5ad51-407">Total capacity\* (TiB)</span></span> |
|---|---|---|---|---|
| <span data-ttu-id="5ad51-408">Week 1 (full and incremental)</span><span class="sxs-lookup"><span data-stu-id="5ad51-408">Week 1 (full and incremental)</span></span> |<span data-ttu-id="5ad51-409">Local disk (short-term)</span><span class="sxs-lookup"><span data-stu-id="5ad51-409">Local disk (short-term)</span></span>| <span data-ttu-id="5ad51-410">1</span><span class="sxs-lookup"><span data-stu-id="5ad51-410">1</span></span> | <span data-ttu-id="5ad51-411">1</span><span class="sxs-lookup"><span data-stu-id="5ad51-411">1</span></span> | <span data-ttu-id="5ad51-412">1</span><span class="sxs-lookup"><span data-stu-id="5ad51-412">1</span></span> |
| <span data-ttu-id="5ad51-413">StorSimple weeks 2-4</span><span class="sxs-lookup"><span data-stu-id="5ad51-413">StorSimple weeks 2-4</span></span> |<span data-ttu-id="5ad51-414">StorSimple disk (long-term)</span><span class="sxs-lookup"><span data-stu-id="5ad51-414">StorSimple disk (long-term)</span></span> | <span data-ttu-id="5ad51-415">1</span><span class="sxs-lookup"><span data-stu-id="5ad51-415">1</span></span> | <span data-ttu-id="5ad51-416">4</span><span class="sxs-lookup"><span data-stu-id="5ad51-416">4</span></span> | <span data-ttu-id="5ad51-417">4</span><span class="sxs-lookup"><span data-stu-id="5ad51-417">4</span></span> |
| <span data-ttu-id="5ad51-418">Monthly full</span><span class="sxs-lookup"><span data-stu-id="5ad51-418">Monthly full</span></span> |<span data-ttu-id="5ad51-419">StorSimple disk (long-term)</span><span class="sxs-lookup"><span data-stu-id="5ad51-419">StorSimple disk (long-term)</span></span> | <span data-ttu-id="5ad51-420">1</span><span class="sxs-lookup"><span data-stu-id="5ad51-420">1</span></span> | <span data-ttu-id="5ad51-421">12</span><span class="sxs-lookup"><span data-stu-id="5ad51-421">12</span></span> | <span data-ttu-id="5ad51-422">12</span><span class="sxs-lookup"><span data-stu-id="5ad51-422">12</span></span> |
| <span data-ttu-id="5ad51-423">Yearly full</span><span class="sxs-lookup"><span data-stu-id="5ad51-423">Yearly full</span></span> |<span data-ttu-id="5ad51-424">StorSimple disk (long-term)</span><span class="sxs-lookup"><span data-stu-id="5ad51-424">StorSimple disk (long-term)</span></span> | <span data-ttu-id="5ad51-425">1</span><span class="sxs-lookup"><span data-stu-id="5ad51-425">1</span></span> | <span data-ttu-id="5ad51-426">1</span><span class="sxs-lookup"><span data-stu-id="5ad51-426">1</span></span> | <span data-ttu-id="5ad51-427">1</span><span class="sxs-lookup"><span data-stu-id="5ad51-427">1</span></span> |
|<span data-ttu-id="5ad51-428">GFS volumes size requirement</span><span class="sxs-lookup"><span data-stu-id="5ad51-428">GFS volumes size requirement</span></span> |  |  |  | <span data-ttu-id="5ad51-429">18\*</span><span class="sxs-lookup"><span data-stu-id="5ad51-429">18\*</span></span>|
<span data-ttu-id="5ad51-430">\* Total capacity includes 17 TiB of StorSimple disks and 1 TiB of local RAID volume.</span><span class="sxs-lookup"><span data-stu-id="5ad51-430">\* Total capacity includes 17 TiB of StorSimple disks and 1 TiB of local RAID volume.</span></span>


### <a name="gfs-example-schedule-gfs-rotation-weekly-monthly-and-yearly-schedule"></a><span data-ttu-id="5ad51-431">GFS example schedule: GFS rotation weekly, monthly, and yearly schedule</span><span class="sxs-lookup"><span data-stu-id="5ad51-431">GFS example schedule: GFS rotation weekly, monthly, and yearly schedule</span></span>

| <span data-ttu-id="5ad51-432">Week</span><span class="sxs-lookup"><span data-stu-id="5ad51-432">Week</span></span> | <span data-ttu-id="5ad51-433">Full</span><span class="sxs-lookup"><span data-stu-id="5ad51-433">Full</span></span> | <span data-ttu-id="5ad51-434">Incremental day 1</span><span class="sxs-lookup"><span data-stu-id="5ad51-434">Incremental day 1</span></span> | <span data-ttu-id="5ad51-435">Incremental day 2</span><span class="sxs-lookup"><span data-stu-id="5ad51-435">Incremental day 2</span></span> | <span data-ttu-id="5ad51-436">Incremental day 3</span><span class="sxs-lookup"><span data-stu-id="5ad51-436">Incremental day 3</span></span> | <span data-ttu-id="5ad51-437">Incremental day 4</span><span class="sxs-lookup"><span data-stu-id="5ad51-437">Incremental day 4</span></span> | <span data-ttu-id="5ad51-438">Incremental day 5</span><span class="sxs-lookup"><span data-stu-id="5ad51-438">Incremental day 5</span></span> |
|---|---|---|---|---|---|---|
| <span data-ttu-id="5ad51-439">Week 1</span><span class="sxs-lookup"><span data-stu-id="5ad51-439">Week 1</span></span> | <span data-ttu-id="5ad51-440">Local RAID volume</span><span class="sxs-lookup"><span data-stu-id="5ad51-440">Local RAID volume</span></span>  | <span data-ttu-id="5ad51-441">Local RAID volume</span><span class="sxs-lookup"><span data-stu-id="5ad51-441">Local RAID volume</span></span> | <span data-ttu-id="5ad51-442">Local RAID volume</span><span class="sxs-lookup"><span data-stu-id="5ad51-442">Local RAID volume</span></span> | <span data-ttu-id="5ad51-443">Local RAID volume</span><span class="sxs-lookup"><span data-stu-id="5ad51-443">Local RAID volume</span></span> | <span data-ttu-id="5ad51-444">Local RAID volume</span><span class="sxs-lookup"><span data-stu-id="5ad51-444">Local RAID volume</span></span> | <span data-ttu-id="5ad51-445">Local RAID volume</span><span class="sxs-lookup"><span data-stu-id="5ad51-445">Local RAID volume</span></span> |
| <span data-ttu-id="5ad51-446">Week 2</span><span class="sxs-lookup"><span data-stu-id="5ad51-446">Week 2</span></span> | <span data-ttu-id="5ad51-447">StorSimple weeks 2-4</span><span class="sxs-lookup"><span data-stu-id="5ad51-447">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="5ad51-448">Week 3</span><span class="sxs-lookup"><span data-stu-id="5ad51-448">Week 3</span></span> | <span data-ttu-id="5ad51-449">StorSimple weeks 2-4</span><span class="sxs-lookup"><span data-stu-id="5ad51-449">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="5ad51-450">Week 4</span><span class="sxs-lookup"><span data-stu-id="5ad51-450">Week 4</span></span> | <span data-ttu-id="5ad51-451">StorSimple weeks 2-4</span><span class="sxs-lookup"><span data-stu-id="5ad51-451">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="5ad51-452">Monthly</span><span class="sxs-lookup"><span data-stu-id="5ad51-452">Monthly</span></span> | <span data-ttu-id="5ad51-453">StorSimple monthly</span><span class="sxs-lookup"><span data-stu-id="5ad51-453">StorSimple monthly</span></span> |   |   |   |   |   |
| <span data-ttu-id="5ad51-454">Yearly</span><span class="sxs-lookup"><span data-stu-id="5ad51-454">Yearly</span></span> | <span data-ttu-id="5ad51-455">StorSimple yearly</span><span class="sxs-lookup"><span data-stu-id="5ad51-455">StorSimple yearly</span></span>  |   |   |   |   |   |   |


### <a name="assign-storsimple-volumes-to-a-backup-exec-archive-and-deduplication-job"></a><span data-ttu-id="5ad51-456">Assign StorSimple volumes to a Backup Exec archive and deduplication job</span><span class="sxs-lookup"><span data-stu-id="5ad51-456">Assign StorSimple volumes to a Backup Exec archive and deduplication job</span></span>

#### <a name="to-assign-storsimple-volumes-to-a-backup-exec-archive-and-duplication-job"></a><span data-ttu-id="5ad51-457">To assign StorSimple volumes to a Backup Exec archive and duplication job</span><span class="sxs-lookup"><span data-stu-id="5ad51-457">To assign StorSimple volumes to a Backup Exec archive and duplication job</span></span>

1.  <span data-ttu-id="5ad51-458">In the Backup Exec management console, right-click the job that you want to archive to a StorSimple volume, and then select **Backup Definition Properties** > **Edit**.</span><span class="sxs-lookup"><span data-stu-id="5ad51-458">In the Backup Exec management console, right-click the job that you want to archive to a StorSimple volume, and then select **Backup Definition Properties** > **Edit**.</span></span>

    ![Backup Exec management console, Backup Definition Properties tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/image19.png)

2.  <span data-ttu-id="5ad51-460">Select **Add Stage** > **Duplicate to Disk** > **Edit**.</span><span class="sxs-lookup"><span data-stu-id="5ad51-460">Select **Add Stage** > **Duplicate to Disk** > **Edit**.</span></span>

    ![Backup Exec management console, add stage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/image20.png)

3.  <span data-ttu-id="5ad51-462">In the **Duplicate Options** dialog box, select the values that you want to use for **Source** and **Schedule**.</span><span class="sxs-lookup"><span data-stu-id="5ad51-462">In the **Duplicate Options** dialog box, select the values that you want to use for **Source** and **Schedule**.</span></span>

    ![Backup Exec management console, backup definitions properties and duplicate options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/image21.png)

4.  <span data-ttu-id="5ad51-464">In the **Storage** drop-down list, select the StorSimple volume where you want the archive job to store the data.</span><span class="sxs-lookup"><span data-stu-id="5ad51-464">In the **Storage** drop-down list, select the StorSimple volume where you want the archive job to store the data.</span></span>

    ![Backup Exec management console, backup definitions properties and duplicate options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/image22.png)

5.  <span data-ttu-id="5ad51-466">Select **Verify**, and then select the **Do not verify data for this job** check box.</span><span class="sxs-lookup"><span data-stu-id="5ad51-466">Select **Verify**, and then select the **Do not verify data for this job** check box.</span></span>

    ![Backup Exec management console, backup definitions properties and duplicate options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/image23.png)

6.  <span data-ttu-id="5ad51-468">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ad51-468">Select **OK**.</span></span>

    ![Backup Exec management console, backup definitions properties and duplicate options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/image24.png)

7.  <span data-ttu-id="5ad51-470">In the **Backup** column, add a new stage.</span><span class="sxs-lookup"><span data-stu-id="5ad51-470">In the **Backup** column, add a new stage.</span></span> <span data-ttu-id="5ad51-471">For the source, use **incremental**.</span><span class="sxs-lookup"><span data-stu-id="5ad51-471">For the source, use **incremental**.</span></span> <span data-ttu-id="5ad51-472">For the target, choose the StorSimple volume where the incremental backup job is archived.</span><span class="sxs-lookup"><span data-stu-id="5ad51-472">For the target, choose the StorSimple volume where the incremental backup job is archived.</span></span> <span data-ttu-id="5ad51-473">Repeat steps 1-6.</span><span class="sxs-lookup"><span data-stu-id="5ad51-473">Repeat steps 1-6.</span></span>

## <a name="storsimple-cloud-snapshots"></a><span data-ttu-id="5ad51-474">StorSimple cloud snapshots</span><span class="sxs-lookup"><span data-stu-id="5ad51-474">StorSimple cloud snapshots</span></span>

<span data-ttu-id="5ad51-475">StorSimple cloud snapshots protect the data that resides in your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="5ad51-475">StorSimple cloud snapshots protect the data that resides in your StorSimple device.</span></span> <span data-ttu-id="5ad51-476">Creating a cloud snapshot is equivalent to shipping local backup tapes to an offsite facility.</span><span class="sxs-lookup"><span data-stu-id="5ad51-476">Creating a cloud snapshot is equivalent to shipping local backup tapes to an offsite facility.</span></span> <span data-ttu-id="5ad51-477">If you use Azure geo-redundant storage, creating a cloud snapshot is equivalent to shipping backup tapes to multiple sites.</span><span class="sxs-lookup"><span data-stu-id="5ad51-477">If you use Azure geo-redundant storage, creating a cloud snapshot is equivalent to shipping backup tapes to multiple sites.</span></span> <span data-ttu-id="5ad51-478">If you need to restore a device after a disaster, you might bring another StorSimple device online and do a failover.</span><span class="sxs-lookup"><span data-stu-id="5ad51-478">If you need to restore a device after a disaster, you might bring another StorSimple device online and do a failover.</span></span> <span data-ttu-id="5ad51-479">After the failover, you would be able to access the data (at cloud speeds) from the most recent cloud snapshot.</span><span class="sxs-lookup"><span data-stu-id="5ad51-479">After the failover, you would be able to access the data (at cloud speeds) from the most recent cloud snapshot.</span></span>

<span data-ttu-id="5ad51-480">The following section describes how to create a short script to start and delete StorSimple cloud snapshots during backup post-processing.</span><span class="sxs-lookup"><span data-stu-id="5ad51-480">The following section describes how to create a short script to start and delete StorSimple cloud snapshots during backup post-processing.</span></span>

> [!NOTE]
> <span data-ttu-id="5ad51-481">Snapshots that are manually or programmatically created do not follow the StorSimple snapshot expiration policy.</span><span class="sxs-lookup"><span data-stu-id="5ad51-481">Snapshots that are manually or programmatically created do not follow the StorSimple snapshot expiration policy.</span></span> <span data-ttu-id="5ad51-482">These snapshots must be manually or programmatically deleted.</span><span class="sxs-lookup"><span data-stu-id="5ad51-482">These snapshots must be manually or programmatically deleted.</span></span>

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a><span data-ttu-id="5ad51-483">Start and delete cloud snapshots by using a script</span><span class="sxs-lookup"><span data-stu-id="5ad51-483">Start and delete cloud snapshots by using a script</span></span>

> [!NOTE]
> <span data-ttu-id="5ad51-484">Carefully assess the compliance and data retention repercussions before you delete a StorSimple snapshot.</span><span class="sxs-lookup"><span data-stu-id="5ad51-484">Carefully assess the compliance and data retention repercussions before you delete a StorSimple snapshot.</span></span> <span data-ttu-id="5ad51-485">For more information about how to run a post-backup script, see the [Backup Exec documentation](https://www.veritas.com/support/en_US/15047.html).</span><span class="sxs-lookup"><span data-stu-id="5ad51-485">For more information about how to run a post-backup script, see the [Backup Exec documentation](https://www.veritas.com/support/en_US/15047.html).</span></span>

### <a name="backup-lifecycle"></a><span data-ttu-id="5ad51-486">Backup lifecycle</span><span class="sxs-lookup"><span data-stu-id="5ad51-486">Backup lifecycle</span></span>

![Backup Lifecycle diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/backuplifecycle.png)

### <a name="requirements"></a><span data-ttu-id="5ad51-488">Requirements</span><span class="sxs-lookup"><span data-stu-id="5ad51-488">Requirements</span></span>

-   <span data-ttu-id="5ad51-489">The server that runs the script must have access to Azure cloud resources.</span><span class="sxs-lookup"><span data-stu-id="5ad51-489">The server that runs the script must have access to Azure cloud resources.</span></span>
-   <span data-ttu-id="5ad51-490">The user account must have the necessary permissions.</span><span class="sxs-lookup"><span data-stu-id="5ad51-490">The user account must have the necessary permissions.</span></span>
-   <span data-ttu-id="5ad51-491">A StorSimple backup policy with the associated StorSimple volumes must be set up but not turned on.</span><span class="sxs-lookup"><span data-stu-id="5ad51-491">A StorSimple backup policy with the associated StorSimple volumes must be set up but not turned on.</span></span>
-   <span data-ttu-id="5ad51-492">You'll need the StorSimple resource name, registration key, device name, and backup policy ID.</span><span class="sxs-lookup"><span data-stu-id="5ad51-492">You'll need the StorSimple resource name, registration key, device name, and backup policy ID.</span></span>

### <a name="to-start-or-delete-a-cloud-snapshot"></a><span data-ttu-id="5ad51-493">To start or delete a cloud snapshot</span><span class="sxs-lookup"><span data-stu-id="5ad51-493">To start or delete a cloud snapshot</span></span>

1.  <span data-ttu-id="5ad51-494">[Install Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="5ad51-494">[Install Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azureps-cmdlets-docs/).</span></span>
2.  <span data-ttu-id="5ad51-495">[Download and import publish settings and subscription information](https://msdn.microsoft.com/library/dn385850.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ad51-495">[Download and import publish settings and subscription information](https://msdn.microsoft.com/library/dn385850.aspx).</span></span>
3.  <span data-ttu-id="5ad51-496">In the Azure classic portal, get the resource name and [registration key for your StorSimple Manager service](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="5ad51-496">In the Azure classic portal, get the resource name and [registration key for your StorSimple Manager service](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).</span></span>
4.  <span data-ttu-id="5ad51-497">On the server that runs the script, run PowerShell as an administrator.</span><span class="sxs-lookup"><span data-stu-id="5ad51-497">On the server that runs the script, run PowerShell as an administrator.</span></span> <span data-ttu-id="5ad51-498">Type this command:</span><span class="sxs-lookup"><span data-stu-id="5ad51-498">Type this command:</span></span>

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    <span data-ttu-id="5ad51-499">Note the backup policy ID.</span><span class="sxs-lookup"><span data-stu-id="5ad51-499">Note the backup policy ID.</span></span>
5.  <span data-ttu-id="5ad51-500">In Notepad, create a new PowerShell script by using the following code.</span><span class="sxs-lookup"><span data-stu-id="5ad51-500">In Notepad, create a new PowerShell script by using the following code.</span></span>

    <span data-ttu-id="5ad51-501">Copy and paste this code snippet:</span><span class="sxs-lookup"><span data-stu-id="5ad51-501">Copy and paste this code snippet:</span></span>
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
      <span data-ttu-id="5ad51-502">Save the PowerShell script to the same location where you saved your Azure publish settings.</span><span class="sxs-lookup"><span data-stu-id="5ad51-502">Save the PowerShell script to the same location where you saved your Azure publish settings.</span></span> <span data-ttu-id="5ad51-503">For example, save as C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1.</span><span class="sxs-lookup"><span data-stu-id="5ad51-503">For example, save as C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1.</span></span>
6.  <span data-ttu-id="5ad51-504">Add the script to your backup job in Backup Exec by editing your Backup Exec job options' pre-processing and post-processing commands.</span><span class="sxs-lookup"><span data-stu-id="5ad51-504">Add the script to your backup job in Backup Exec by editing your Backup Exec job options' pre-processing and post-processing commands.</span></span>

    ![Backup Exec console, backup options, pre- and post-processing commands tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-backup-target-using-backup-exec/image25.png)

> [!NOTE]
> <span data-ttu-id="5ad51-506">We recommend that you run your StorSimple cloud snapshot backup policy as a post-processing script at the end of your daily backup job.</span><span class="sxs-lookup"><span data-stu-id="5ad51-506">We recommend that you run your StorSimple cloud snapshot backup policy as a post-processing script at the end of your daily backup job.</span></span> <span data-ttu-id="5ad51-507">For more information about how to back up and restore your backup application environment to help you meet your RPO and RTO, please consult with your backup architect.</span><span class="sxs-lookup"><span data-stu-id="5ad51-507">For more information about how to back up and restore your backup application environment to help you meet your RPO and RTO, please consult with your backup architect.</span></span>

## <a name="storsimple-as-a-restore-source"></a><span data-ttu-id="5ad51-508">StorSimple as a restore source</span><span class="sxs-lookup"><span data-stu-id="5ad51-508">StorSimple as a restore source</span></span>

<span data-ttu-id="5ad51-509">Restores from a StorSimple device work like restores from any block storage device.</span><span class="sxs-lookup"><span data-stu-id="5ad51-509">Restores from a StorSimple device work like restores from any block storage device.</span></span> <span data-ttu-id="5ad51-510">Restores of data that is tiered to the cloud occurs at cloud speeds.</span><span class="sxs-lookup"><span data-stu-id="5ad51-510">Restores of data that is tiered to the cloud occurs at cloud speeds.</span></span> <span data-ttu-id="5ad51-511">For local data, restores occur at the local disk speed of the device.</span><span class="sxs-lookup"><span data-stu-id="5ad51-511">For local data, restores occur at the local disk speed of the device.</span></span> <span data-ttu-id="5ad51-512">For information about how to perform a restore, see the Backup Exec documentation.</span><span class="sxs-lookup"><span data-stu-id="5ad51-512">For information about how to perform a restore, see the Backup Exec documentation.</span></span> <span data-ttu-id="5ad51-513">We recommend that you conform to Backup Exec restore best practices.</span><span class="sxs-lookup"><span data-stu-id="5ad51-513">We recommend that you conform to Backup Exec restore best practices.</span></span>

## <a name="storsimple-failover-and-disaster-recovery"></a><span data-ttu-id="5ad51-514">StorSimple failover and disaster recovery</span><span class="sxs-lookup"><span data-stu-id="5ad51-514">StorSimple failover and disaster recovery</span></span>

> [!NOTE]
> <span data-ttu-id="5ad51-515">For backup target scenarios, StorSimple Cloud Appliance is not supported as a restore target.</span><span class="sxs-lookup"><span data-stu-id="5ad51-515">For backup target scenarios, StorSimple Cloud Appliance is not supported as a restore target.</span></span>

<span data-ttu-id="5ad51-516">A disaster can be caused by a variety of factors.</span><span class="sxs-lookup"><span data-stu-id="5ad51-516">A disaster can be caused by a variety of factors.</span></span> <span data-ttu-id="5ad51-517">The following table lists common disaster recovery scenarios.</span><span class="sxs-lookup"><span data-stu-id="5ad51-517">The following table lists common disaster recovery scenarios.</span></span>

| <span data-ttu-id="5ad51-518">Scenario</span><span class="sxs-lookup"><span data-stu-id="5ad51-518">Scenario</span></span> | <span data-ttu-id="5ad51-519">Impact</span><span class="sxs-lookup"><span data-stu-id="5ad51-519">Impact</span></span> | <span data-ttu-id="5ad51-520">How to recover</span><span class="sxs-lookup"><span data-stu-id="5ad51-520">How to recover</span></span> | <span data-ttu-id="5ad51-521">Notes</span><span class="sxs-lookup"><span data-stu-id="5ad51-521">Notes</span></span> |
|---|---|---|---|
| <span data-ttu-id="5ad51-522">StorSimple device failure</span><span class="sxs-lookup"><span data-stu-id="5ad51-522">StorSimple device failure</span></span> | <span data-ttu-id="5ad51-523">Backup and restore operations are interrupted.</span><span class="sxs-lookup"><span data-stu-id="5ad51-523">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="5ad51-524">Replace the failed device and perform [StorSimple failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="5ad51-524">Replace the failed device and perform [StorSimple failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span> | <span data-ttu-id="5ad51-525">If you need to perform a restore after device recovery, full data working sets are retrieved from the cloud to the new device.</span><span class="sxs-lookup"><span data-stu-id="5ad51-525">If you need to perform a restore after device recovery, full data working sets are retrieved from the cloud to the new device.</span></span> <span data-ttu-id="5ad51-526">All operations are at cloud speeds.</span><span class="sxs-lookup"><span data-stu-id="5ad51-526">All operations are at cloud speeds.</span></span> <span data-ttu-id="5ad51-527">The indexing and cataloging rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier, which might be a time-consuming process.</span><span class="sxs-lookup"><span data-stu-id="5ad51-527">The indexing and cataloging rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier, which might be a time-consuming process.</span></span> |
| <span data-ttu-id="5ad51-528">Backup Exec server failure</span><span class="sxs-lookup"><span data-stu-id="5ad51-528">Backup Exec server failure</span></span> | <span data-ttu-id="5ad51-529">Backup and restore operations are interrupted.</span><span class="sxs-lookup"><span data-stu-id="5ad51-529">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="5ad51-530">Rebuild the backup server and perform database restore as detailed in [How to do a manual Backup and Restore of Backup Exec (BEDB) database](http://www.veritas.com/docs/000041083).</span><span class="sxs-lookup"><span data-stu-id="5ad51-530">Rebuild the backup server and perform database restore as detailed in [How to do a manual Backup and Restore of Backup Exec (BEDB) database](http://www.veritas.com/docs/000041083).</span></span> | <span data-ttu-id="5ad51-531">You must rebuild or restore the Backup Exec server at the disaster recovery site.</span><span class="sxs-lookup"><span data-stu-id="5ad51-531">You must rebuild or restore the Backup Exec server at the disaster recovery site.</span></span> <span data-ttu-id="5ad51-532">Restore the database to the most recent point.</span><span class="sxs-lookup"><span data-stu-id="5ad51-532">Restore the database to the most recent point.</span></span> <span data-ttu-id="5ad51-533">If the restored Backup Exec database is not in sync with your latest backup jobs, indexing and cataloging is required.</span><span class="sxs-lookup"><span data-stu-id="5ad51-533">If the restored Backup Exec database is not in sync with your latest backup jobs, indexing and cataloging is required.</span></span> <span data-ttu-id="5ad51-534">This index and catalog rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier.</span><span class="sxs-lookup"><span data-stu-id="5ad51-534">This index and catalog rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier.</span></span> <span data-ttu-id="5ad51-535">This makes it further time-intensive.</span><span class="sxs-lookup"><span data-stu-id="5ad51-535">This makes it further time-intensive.</span></span> |
| <span data-ttu-id="5ad51-536">Site failure that results in the loss of both the backup server and StorSimple</span><span class="sxs-lookup"><span data-stu-id="5ad51-536">Site failure that results in the loss of both the backup server and StorSimple</span></span> | <span data-ttu-id="5ad51-537">Backup and restore operations are interrupted.</span><span class="sxs-lookup"><span data-stu-id="5ad51-537">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="5ad51-538">Restore StorSimple first, and then restore Backup Exec.</span><span class="sxs-lookup"><span data-stu-id="5ad51-538">Restore StorSimple first, and then restore Backup Exec.</span></span> | <span data-ttu-id="5ad51-539">Restore StorSimple first, and then restore Backup Exec.</span><span class="sxs-lookup"><span data-stu-id="5ad51-539">Restore StorSimple first, and then restore Backup Exec.</span></span> <span data-ttu-id="5ad51-540">If you need to perform a restore after device recovery, the full data working sets are retrieved from the cloud to the new device.</span><span class="sxs-lookup"><span data-stu-id="5ad51-540">If you need to perform a restore after device recovery, the full data working sets are retrieved from the cloud to the new device.</span></span> <span data-ttu-id="5ad51-541">All operations are at cloud speeds.</span><span class="sxs-lookup"><span data-stu-id="5ad51-541">All operations are at cloud speeds.</span></span> |

## <a name="references"></a><span data-ttu-id="5ad51-542">References</span><span class="sxs-lookup"><span data-stu-id="5ad51-542">References</span></span>

<span data-ttu-id="5ad51-543">The following documents were referenced for this article:</span><span class="sxs-lookup"><span data-stu-id="5ad51-543">The following documents were referenced for this article:</span></span>

- [<span data-ttu-id="5ad51-544">StorSimple multipath I/O setup</span><span class="sxs-lookup"><span data-stu-id="5ad51-544">StorSimple multipath I/O setup</span></span>](storsimple-configure-mpio-windows-server.md)
- [<span data-ttu-id="5ad51-545">Storage scenarios: Thin provisioning</span><span class="sxs-lookup"><span data-stu-id="5ad51-545">Storage scenarios: Thin provisioning</span></span>](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [<span data-ttu-id="5ad51-546">Using GPT drives</span><span class="sxs-lookup"><span data-stu-id="5ad51-546">Using GPT drives</span></span>](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [<span data-ttu-id="5ad51-547">Set up shadow copies for shared folders</span><span class="sxs-lookup"><span data-stu-id="5ad51-547">Set up shadow copies for shared folders</span></span>](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a><span data-ttu-id="5ad51-548">Next steps</span><span class="sxs-lookup"><span data-stu-id="5ad51-548">Next steps</span></span>

- <span data-ttu-id="5ad51-549">Learn more about how to [restore from a backup set](storsimple-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="5ad51-549">Learn more about how to [restore from a backup set](storsimple-restore-from-backup-set-u2.md).</span></span>
- <span data-ttu-id="5ad51-550">Learn more about how to perform [device failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="5ad51-550">Learn more about how to perform [device failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span>
























