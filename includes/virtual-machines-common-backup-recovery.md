---
title: include file
description: include file
services: virtual-machines
author: cynthn
ms.service: virtual-machines
ms.topic: include
ms.date: 03/09/2018
ms.author: cynthn
ms.custom: include file
ms.openlocfilehash: 3dfc72ff0347a93c6c6dce0e7ec763dd8241c55b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855987"
---
## <a name="azure-backup"></a><span data-ttu-id="c024c-103">Azure Backup</span><span class="sxs-lookup"><span data-stu-id="c024c-103">Azure Backup</span></span>

<span data-ttu-id="c024c-104">For backing up Azure VMs running production workloads, use Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="c024c-104">For backing up Azure VMs running production workloads, use Azure Backup.</span></span> <span data-ttu-id="c024c-105">Azure Backup supports application-consistent backups for both Windows and Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="c024c-105">Azure Backup supports application-consistent backups for both Windows and Linux VMs.</span></span> <span data-ttu-id="c024c-106">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span><span class="sxs-lookup"><span data-stu-id="c024c-106">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="c024c-107">When you restore from a recovery point, you can restore the whole VM or just specific files.</span><span class="sxs-lookup"><span data-stu-id="c024c-107">When you restore from a recovery point, you can restore the whole VM or just specific files.</span></span> 

<span data-ttu-id="c024c-108">For a simple, hands-on introduction to Azure Backup for Azure VMs, see the "Back up Azure virtual machines" tutorial for [Linux](../articles/virtual-machines/linux/tutorial-backup-vms.md) or [Windows](../articles/virtual-machines/windows/tutorial-backup-vms.md).</span><span class="sxs-lookup"><span data-stu-id="c024c-108">For a simple, hands-on introduction to Azure Backup for Azure VMs, see the "Back up Azure virtual machines" tutorial for [Linux](../articles/virtual-machines/linux/tutorial-backup-vms.md) or [Windows](../articles/virtual-machines/windows/tutorial-backup-vms.md).</span></span>

<span data-ttu-id="c024c-109">For more information on how Azure Backup works, see [Plan your VM backup infrastructure in Azure](../articles/backup/backup-azure-vms-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="c024c-109">For more information on how Azure Backup works, see [Plan your VM backup infrastructure in Azure](../articles/backup/backup-azure-vms-introduction.md)</span></span>


## <a name="azure-site-recovery"></a><span data-ttu-id="c024c-110">Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="c024c-110">Azure Site Recovery</span></span>

<span data-ttu-id="c024c-111">Azure Site Recovery protects your VMs from a major disaster scenario, when a whole region experiences an outage due to major natural disaster or widespread service interruption.</span><span class="sxs-lookup"><span data-stu-id="c024c-111">Azure Site Recovery protects your VMs from a major disaster scenario, when a whole region experiences an outage due to major natural disaster or widespread service interruption.</span></span> <span data-ttu-id="c024c-112">You can configure Azure Site Recovery for your VMs so that you can recover your application with a single click in matter of minutes.</span><span class="sxs-lookup"><span data-stu-id="c024c-112">You can configure Azure Site Recovery for your VMs so that you can recover your application with a single click in matter of minutes.</span></span> <span data-ttu-id="c024c-113">You can replicate to an Azure region of your choice, it is not restricted to paired regions.</span><span class="sxs-lookup"><span data-stu-id="c024c-113">You can replicate to an Azure region of your choice, it is not restricted to paired regions.</span></span> 

<span data-ttu-id="c024c-114">You can run disaster-recovery drills with on-demand test failovers, without affecting your production workloads or ongoing replication.</span><span class="sxs-lookup"><span data-stu-id="c024c-114">You can run disaster-recovery drills with on-demand test failovers, without affecting your production workloads or ongoing replication.</span></span> <span data-ttu-id="c024c-115">Create recovery plans to orchestrate failover and failback of the entire application running on multiple VMs.</span><span class="sxs-lookup"><span data-stu-id="c024c-115">Create recovery plans to orchestrate failover and failback of the entire application running on multiple VMs.</span></span> <span data-ttu-id="c024c-116">The recovery plan feature is integrated with Azure automation runbooks.</span><span class="sxs-lookup"><span data-stu-id="c024c-116">The recovery plan feature is integrated with Azure automation runbooks.</span></span>

<span data-ttu-id="c024c-117">You can get started by [replicating your virtual machines](https://aka.ms/a2a-getting-started).</span><span class="sxs-lookup"><span data-stu-id="c024c-117">You can get started by [replicating your virtual machines](https://aka.ms/a2a-getting-started).</span></span> 

## <a name="managed-snapshots"></a><span data-ttu-id="c024c-118">Managed snapshots</span><span class="sxs-lookup"><span data-stu-id="c024c-118">Managed snapshots</span></span> 

<span data-ttu-id="c024c-119">In development and test environments, snapshots provide a quick and simple option for backing up VMs that use Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="c024c-119">In development and test environments, snapshots provide a quick and simple option for backing up VMs that use Managed Disks.</span></span> <span data-ttu-id="c024c-120">A managed snapshot is a read-only full copy of a managed disk.</span><span class="sxs-lookup"><span data-stu-id="c024c-120">A managed snapshot is a read-only full copy of a managed disk.</span></span> <span data-ttu-id="c024c-121">Snapshots exist independent of the source disk and can be used to create new managed disks for rebuilding a VM.</span><span class="sxs-lookup"><span data-stu-id="c024c-121">Snapshots exist independent of the source disk and can be used to create new managed disks for rebuilding a VM.</span></span> <span data-ttu-id="c024c-122">They are billed based on the used portion of the disk.</span><span class="sxs-lookup"><span data-stu-id="c024c-122">They are billed based on the used portion of the disk.</span></span> <span data-ttu-id="c024c-123">For example, if you create a snapshot of a managed disk with provisioned capacity of 64 GB and actual used data size of 10 GB, snapshot will be billed only for the used data size of 10 GB.</span><span class="sxs-lookup"><span data-stu-id="c024c-123">For example, if you create a snapshot of a managed disk with provisioned capacity of 64 GB and actual used data size of 10 GB, snapshot will be billed only for the used data size of 10 GB.</span></span>  

<span data-ttu-id="c024c-124">For more information on creating snapshots, see:</span><span class="sxs-lookup"><span data-stu-id="c024c-124">For more information on creating snapshots, see:</span></span>

* [<span data-ttu-id="c024c-125">Create copy of VHD stored as a Managed Disk using Snapshots in Windows</span><span class="sxs-lookup"><span data-stu-id="c024c-125">Create copy of VHD stored as a Managed Disk using Snapshots in Windows</span></span>](../articles/virtual-machines/windows/snapshot-copy-managed-disk.md)
* [<span data-ttu-id="c024c-126">Create copy of VHD stored as a Managed Disk using Snapshots in Linux</span><span class="sxs-lookup"><span data-stu-id="c024c-126">Create copy of VHD stored as a Managed Disk using Snapshots in Linux</span></span>](../articles/virtual-machines/linux/snapshot-copy-managed-disk.md)



## <a name="next-steps"></a><span data-ttu-id="c024c-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="c024c-127">Next steps</span></span>
<span data-ttu-id="c024c-128">You can try out Azure Backup by following the "Back up Windows virtual machines tutorial" for [Linux](../articles/virtual-machines/linux/tutorial-backup-vms.md) or [Windows](../articles/virtual-machines/windows/tutorial-backup-vms.md).</span><span class="sxs-lookup"><span data-stu-id="c024c-128">You can try out Azure Backup by following the "Back up Windows virtual machines tutorial" for [Linux](../articles/virtual-machines/linux/tutorial-backup-vms.md) or [Windows](../articles/virtual-machines/windows/tutorial-backup-vms.md).</span></span>
