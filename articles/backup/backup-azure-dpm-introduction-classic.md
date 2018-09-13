---
title: Back up DPM workloads to Azure classic portal | Microsoft Docs
description: An introduction to backing up DPM servers using the Azure Backup service
services: backup
documentationcenter: ''
author: Nkolli1
manager: shreeshd
editor: ''
keywords: System Center Data Protection Manager, data protection manager, dpm backup
ms.assetid: 8f23972b-d167-4231-b331-e198db3b18b4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: nkolli;giridham;markgal
ms.openlocfilehash: 9d1e68b0e73c60542de566c32c92caf0b3c4630c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554936"
---
# <a name="preparing-to-back-up-workloads-to-azure-with-dpm"></a><span data-ttu-id="bb503-104">Preparing to back up workloads to Azure with DPM</span><span class="sxs-lookup"><span data-stu-id="bb503-104">Preparing to back up workloads to Azure with DPM</span></span>
> [!div class="op_single_selector"]
> * [Azure Backup Server](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Azure Backup Server (Classic)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (Classic)](backup-azure-dpm-introduction-classic.md)
>
>

<span data-ttu-id="bb503-109">This article provides an introduction to using Microsoft Azure Backup to protect your System Center Data Protection Manager (DPM) servers and workloads.</span><span class="sxs-lookup"><span data-stu-id="bb503-109">This article provides an introduction to using Microsoft Azure Backup to protect your System Center Data Protection Manager (DPM) servers and workloads.</span></span> <span data-ttu-id="bb503-110">By reading it, you’ll understand:</span><span class="sxs-lookup"><span data-stu-id="bb503-110">By reading it, you’ll understand:</span></span>

* <span data-ttu-id="bb503-111">How Azure DPM server backup works</span><span class="sxs-lookup"><span data-stu-id="bb503-111">How Azure DPM server backup works</span></span>
* <span data-ttu-id="bb503-112">The prerequisites to achieve a smooth backup experience</span><span class="sxs-lookup"><span data-stu-id="bb503-112">The prerequisites to achieve a smooth backup experience</span></span>
* <span data-ttu-id="bb503-113">The typical errors encountered and how to deal with them</span><span class="sxs-lookup"><span data-stu-id="bb503-113">The typical errors encountered and how to deal with them</span></span>
* <span data-ttu-id="bb503-114">Supported scenarios</span><span class="sxs-lookup"><span data-stu-id="bb503-114">Supported scenarios</span></span>

<span data-ttu-id="bb503-115">System Center DPM backs up file and application data.</span><span class="sxs-lookup"><span data-stu-id="bb503-115">System Center DPM backs up file and application data.</span></span> <span data-ttu-id="bb503-116">Data backed up to DPM can be stored on tape, on disk, or backed up to Azure with Microsoft Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="bb503-116">Data backed up to DPM can be stored on tape, on disk, or backed up to Azure with Microsoft Azure Backup.</span></span> <span data-ttu-id="bb503-117">DPM interacts with Azure Backup as follows:</span><span class="sxs-lookup"><span data-stu-id="bb503-117">DPM interacts with Azure Backup as follows:</span></span>

* <span data-ttu-id="bb503-118">**DPM deployed as a physical server or on-premises virtual machine** — If DPM is deployed as a physical server or as an on-premises Hyper-V virtual machine you can back up data to an Azure Backup vault in addition to disk and tape backup.</span><span class="sxs-lookup"><span data-stu-id="bb503-118">**DPM deployed as a physical server or on-premises virtual machine** — If DPM is deployed as a physical server or as an on-premises Hyper-V virtual machine you can back up data to an Azure Backup vault in addition to disk and tape backup.</span></span>
* <span data-ttu-id="bb503-119">**DPM deployed as an Azure virtual machine** — From System Center 2012 R2 with Update 3, DPM can be deployed as an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="bb503-119">**DPM deployed as an Azure virtual machine** — From System Center 2012 R2 with Update 3, DPM can be deployed as an Azure virtual machine.</span></span> <span data-ttu-id="bb503-120">If DPM is deployed as an Azure virtual machine you can back up data to Azure disks attached to the DPM Azure virtual machine, or you can offload the data storage by backing it up to an Azure Backup vault.</span><span class="sxs-lookup"><span data-stu-id="bb503-120">If DPM is deployed as an Azure virtual machine you can back up data to Azure disks attached to the DPM Azure virtual machine, or you can offload the data storage by backing it up to an Azure Backup vault.</span></span>

## <a name="why-backup-your-dpm-servers"></a><span data-ttu-id="bb503-121">Why backup your DPM servers?</span><span class="sxs-lookup"><span data-stu-id="bb503-121">Why backup your DPM servers?</span></span>
<span data-ttu-id="bb503-122">The business benefits of using Azure Backup for backing up DPM servers include:</span><span class="sxs-lookup"><span data-stu-id="bb503-122">The business benefits of using Azure Backup for backing up DPM servers include:</span></span>

* <span data-ttu-id="bb503-123">For on-premises DPM deployment, you can use Azure backup as an alternative to long-term deployment to tape.</span><span class="sxs-lookup"><span data-stu-id="bb503-123">For on-premises DPM deployment, you can use Azure backup as an alternative to long-term deployment to tape.</span></span>
* <span data-ttu-id="bb503-124">For DPM deployments in Azure, Azure Backup allows you to offload storage from the Azure disk, allowing you to scale up by storing older data in Azure Backup and new data on disk.</span><span class="sxs-lookup"><span data-stu-id="bb503-124">For DPM deployments in Azure, Azure Backup allows you to offload storage from the Azure disk, allowing you to scale up by storing older data in Azure Backup and new data on disk.</span></span>

## <a name="how-does-dpm-server-backup-work"></a><span data-ttu-id="bb503-125">How does DPM server backup work?</span><span class="sxs-lookup"><span data-stu-id="bb503-125">How does DPM server backup work?</span></span>
<span data-ttu-id="bb503-126">To back up a virtual machine, first a point-in-time snapshot of the data is needed.</span><span class="sxs-lookup"><span data-stu-id="bb503-126">To back up a virtual machine, first a point-in-time snapshot of the data is needed.</span></span> <span data-ttu-id="bb503-127">The Azure Backup service initiates the backup job at the scheduled time, and triggers the backup extension to take a snapshot.</span><span class="sxs-lookup"><span data-stu-id="bb503-127">The Azure Backup service initiates the backup job at the scheduled time, and triggers the backup extension to take a snapshot.</span></span> <span data-ttu-id="bb503-128">The backup extension coordinates with the in-guest VSS service to achieve consistency, and invokes the blob snapshot API of the Azure Storage service once consistency has been reached.</span><span class="sxs-lookup"><span data-stu-id="bb503-128">The backup extension coordinates with the in-guest VSS service to achieve consistency, and invokes the blob snapshot API of the Azure Storage service once consistency has been reached.</span></span> <span data-ttu-id="bb503-129">This is done to get a consistent snapshot of the disks of the virtual machine, without having to shut it down.</span><span class="sxs-lookup"><span data-stu-id="bb503-129">This is done to get a consistent snapshot of the disks of the virtual machine, without having to shut it down.</span></span>

<span data-ttu-id="bb503-130">After the snapshot has been taken, the data is transferred by the Azure Backup service to the backup vault.</span><span class="sxs-lookup"><span data-stu-id="bb503-130">After the snapshot has been taken, the data is transferred by the Azure Backup service to the backup vault.</span></span> <span data-ttu-id="bb503-131">The service takes care of identifying and transferring only the blocks that have changed from the last backup making the backups storage and network efficient.</span><span class="sxs-lookup"><span data-stu-id="bb503-131">The service takes care of identifying and transferring only the blocks that have changed from the last backup making the backups storage and network efficient.</span></span> <span data-ttu-id="bb503-132">When the data transfer is completed, the snapshot is removed and a recovery point is created.</span><span class="sxs-lookup"><span data-stu-id="bb503-132">When the data transfer is completed, the snapshot is removed and a recovery point is created.</span></span> <span data-ttu-id="bb503-133">This recovery point can be seen in the  Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="bb503-133">This recovery point can be seen in the  Azure classic portal.</span></span>

> [!NOTE]
> For Linux virtual machines, only file-consistent backup is possible.
>
>

## <a name="prerequisites"></a><span data-ttu-id="bb503-135">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bb503-135">Prerequisites</span></span>
<span data-ttu-id="bb503-136">Prepare Azure Backup to back up DPM data as follows:</span><span class="sxs-lookup"><span data-stu-id="bb503-136">Prepare Azure Backup to back up DPM data as follows:</span></span>

1. <span data-ttu-id="bb503-137">**Create a Backup vault**</span><span class="sxs-lookup"><span data-stu-id="bb503-137">**Create a Backup vault**</span></span>

  > [!IMPORTANT]
  > Starting March 2017, you can no longer use the classic portal to create Backup vaults. Existing Backup vaults are still supported, and it is possible to [use Azure PowerShell to create Backup vaults](./backup-client-automation-classic.md#create-a-backup-vault). However, Microsoft recommends you create Recovery Services vaults for all deployments because future enhancements apply to Recovery Services vaults, only.

2. <span data-ttu-id="bb503-141">**Download vault credentials** — In Azure Backup, upload the management certificate you created to the vault.</span><span class="sxs-lookup"><span data-stu-id="bb503-141">**Download vault credentials** — In Azure Backup, upload the management certificate you created to the vault.</span></span>
3. <span data-ttu-id="bb503-142">**Install the Azure Backup Agent and register the server** — From Azure Backup, install the agent on each DPM server and register the DPM server in the backup vault.</span><span class="sxs-lookup"><span data-stu-id="bb503-142">**Install the Azure Backup Agent and register the server** — From Azure Backup, install the agent on each DPM server and register the DPM server in the backup vault.</span></span>

[!INCLUDE [backup-download-credentials](../../includes/backup-download-credentials.md)]

[!INCLUDE [backup-install-agent](../../includes/backup-install-agent.md)]

## <a name="requirements-and-limitations"></a><span data-ttu-id="bb503-143">Requirements (and limitations)</span><span class="sxs-lookup"><span data-stu-id="bb503-143">Requirements (and limitations)</span></span>
* <span data-ttu-id="bb503-144">DPM can be running as a physical server or a Hyper-V virtual machine installed on System Center 2012 SP1 or System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="bb503-144">DPM can be running as a physical server or a Hyper-V virtual machine installed on System Center 2012 SP1 or System Center 2012 R2.</span></span> <span data-ttu-id="bb503-145">It can also be running as an Azure virtual machine running on System Center 2012 R2 with at least DPM 2012 R2 Update Rollup 3 or a Windows virtual machine in VMWare running on System Center 2012 R2 with at least Update Rollup 5.</span><span class="sxs-lookup"><span data-stu-id="bb503-145">It can also be running as an Azure virtual machine running on System Center 2012 R2 with at least DPM 2012 R2 Update Rollup 3 or a Windows virtual machine in VMWare running on System Center 2012 R2 with at least Update Rollup 5.</span></span>
* <span data-ttu-id="bb503-146">If you’re running DPM with System Center 2012 SP1, you should install Update Rollup 2 for System Center Data Protection Manager SP1.</span><span class="sxs-lookup"><span data-stu-id="bb503-146">If you’re running DPM with System Center 2012 SP1, you should install Update Rollup 2 for System Center Data Protection Manager SP1.</span></span> <span data-ttu-id="bb503-147">This is required before you can install the Azure Backup Agent.</span><span class="sxs-lookup"><span data-stu-id="bb503-147">This is required before you can install the Azure Backup Agent.</span></span>
* <span data-ttu-id="bb503-148">The DPM server should have Windows PowerShell and .Net Framework 4.5 installed.</span><span class="sxs-lookup"><span data-stu-id="bb503-148">The DPM server should have Windows PowerShell and .Net Framework 4.5 installed.</span></span>
* <span data-ttu-id="bb503-149">DPM can back up most workloads to Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="bb503-149">DPM can back up most workloads to Azure Backup.</span></span> <span data-ttu-id="bb503-150">For a full list of what’s supported see the Azure Backup support items below.</span><span class="sxs-lookup"><span data-stu-id="bb503-150">For a full list of what’s supported see the Azure Backup support items below.</span></span>
* <span data-ttu-id="bb503-151">Data stored in Azure Backup can’t be recovered with the “copy to tape” option.</span><span class="sxs-lookup"><span data-stu-id="bb503-151">Data stored in Azure Backup can’t be recovered with the “copy to tape” option.</span></span>
* <span data-ttu-id="bb503-152">You’ll need an Azure account with the Azure Backup feature enabled.</span><span class="sxs-lookup"><span data-stu-id="bb503-152">You’ll need an Azure account with the Azure Backup feature enabled.</span></span> <span data-ttu-id="bb503-153">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="bb503-153">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="bb503-154">Read about [Azure Backup pricing](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="bb503-154">Read about [Azure Backup pricing](https://azure.microsoft.com/pricing/details/backup/).</span></span>
* <span data-ttu-id="bb503-155">Using Azure Backup requires the Azure Backup Agent to be installed on the servers you want to back up.</span><span class="sxs-lookup"><span data-stu-id="bb503-155">Using Azure Backup requires the Azure Backup Agent to be installed on the servers you want to back up.</span></span> <span data-ttu-id="bb503-156">Each server must have at least 10% of the size of the data that is being backed up, available as local free storage.</span><span class="sxs-lookup"><span data-stu-id="bb503-156">Each server must have at least 10% of the size of the data that is being backed up, available as local free storage.</span></span> <span data-ttu-id="bb503-157">For example, backing up 100 GB of data requires a minimum of 10 GB of free space in the scratch location.</span><span class="sxs-lookup"><span data-stu-id="bb503-157">For example, backing up 100 GB of data requires a minimum of 10 GB of free space in the scratch location.</span></span> <span data-ttu-id="bb503-158">While the minimum is 10%, 15% of free local storage space to be used for the cache location is recommended.</span><span class="sxs-lookup"><span data-stu-id="bb503-158">While the minimum is 10%, 15% of free local storage space to be used for the cache location is recommended.</span></span>
* <span data-ttu-id="bb503-159">Data will be stored in the Azure vault storage.</span><span class="sxs-lookup"><span data-stu-id="bb503-159">Data will be stored in the Azure vault storage.</span></span> <span data-ttu-id="bb503-160">There’s no limit to the amount of data you can back up to an Azure Backup vault but the size of a data source (for example a virtual machine or database) shouldn’t exceed 54,400 GB.</span><span class="sxs-lookup"><span data-stu-id="bb503-160">There’s no limit to the amount of data you can back up to an Azure Backup vault but the size of a data source (for example a virtual machine or database) shouldn’t exceed 54,400 GB.</span></span>

<span data-ttu-id="bb503-161">These file types are supported for back up to Azure:</span><span class="sxs-lookup"><span data-stu-id="bb503-161">These file types are supported for back up to Azure:</span></span>

* <span data-ttu-id="bb503-162">Encrypted (Full backups only)</span><span class="sxs-lookup"><span data-stu-id="bb503-162">Encrypted (Full backups only)</span></span>
* <span data-ttu-id="bb503-163">Compressed (Incremental backups supported)</span><span class="sxs-lookup"><span data-stu-id="bb503-163">Compressed (Incremental backups supported)</span></span>
* <span data-ttu-id="bb503-164">Sparse (Incremental backups supported)</span><span class="sxs-lookup"><span data-stu-id="bb503-164">Sparse (Incremental backups supported)</span></span>
* <span data-ttu-id="bb503-165">Compressed and sparse (Treated as Sparse)</span><span class="sxs-lookup"><span data-stu-id="bb503-165">Compressed and sparse (Treated as Sparse)</span></span>

<span data-ttu-id="bb503-166">And these are unsupported:</span><span class="sxs-lookup"><span data-stu-id="bb503-166">And these are unsupported:</span></span>

* <span data-ttu-id="bb503-167">Servers on case-sensitive file systems aren’t supported.</span><span class="sxs-lookup"><span data-stu-id="bb503-167">Servers on case-sensitive file systems aren’t supported.</span></span>
* <span data-ttu-id="bb503-168">Hard links (Skipped)</span><span class="sxs-lookup"><span data-stu-id="bb503-168">Hard links (Skipped)</span></span>
* <span data-ttu-id="bb503-169">Reparse points (Skipped)</span><span class="sxs-lookup"><span data-stu-id="bb503-169">Reparse points (Skipped)</span></span>
* <span data-ttu-id="bb503-170">Encrypted and compressed (Skipped)</span><span class="sxs-lookup"><span data-stu-id="bb503-170">Encrypted and compressed (Skipped)</span></span>
* <span data-ttu-id="bb503-171">Encrypted and sparse (Skipped)</span><span class="sxs-lookup"><span data-stu-id="bb503-171">Encrypted and sparse (Skipped)</span></span>
* <span data-ttu-id="bb503-172">Compressed stream</span><span class="sxs-lookup"><span data-stu-id="bb503-172">Compressed stream</span></span>
* <span data-ttu-id="bb503-173">Sparse stream</span><span class="sxs-lookup"><span data-stu-id="bb503-173">Sparse stream</span></span>

> [!NOTE]
> From in System Center 2012 DPM with SP1 onwards, you can backup up workloads protected by DPM to Azure using Microsoft Azure Backup.
>
>
