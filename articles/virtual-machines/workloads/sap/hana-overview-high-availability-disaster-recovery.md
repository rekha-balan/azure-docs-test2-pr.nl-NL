---
title: High availability and disaster recovery of SAP HANA on Azure (large instances) | Microsoft Docs
description: Establish high availability and plan for disaster recovery of SAP HANA on Azure (large instances).
services: virtual-machines-linux
documentationcenter: ''
author: RicksterCDN
manager: timlt
editor: ''
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8011e2ca4edc51e42df6e3289dc9e1f773f48505
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660586"
---
# <a name="sap-hana-large-instances-high-availability-and-disaster-recovery-on-azure"></a><span data-ttu-id="1901b-103">SAP HANA (large instances) high availability and disaster recovery on Azure</span><span class="sxs-lookup"><span data-stu-id="1901b-103">SAP HANA (large instances) high availability and disaster recovery on Azure</span></span> 

<span data-ttu-id="1901b-104">High availability and disaster recovery are important aspects of running your mission-critical SAP HANA on Azure (large instances) servers.</span><span class="sxs-lookup"><span data-stu-id="1901b-104">High availability and disaster recovery are important aspects of running your mission-critical SAP HANA on Azure (large instances) servers.</span></span> <span data-ttu-id="1901b-105">It's important to work with SAP, your system integrator, or Microsoft to properly architect and implement the right high-availability/disaster-recovery strategy.</span><span class="sxs-lookup"><span data-stu-id="1901b-105">It's important to work with SAP, your system integrator, or Microsoft to properly architect and implement the right high-availability/disaster-recovery strategy.</span></span> <span data-ttu-id="1901b-106">It is also important to consider the recovery point objective and recovery time objective, which are specific to your environment.</span><span class="sxs-lookup"><span data-stu-id="1901b-106">It is also important to consider the recovery point objective and recovery time objective, which are specific to your environment.</span></span>

## <a name="high-availability"></a><span data-ttu-id="1901b-107">High availability</span><span class="sxs-lookup"><span data-stu-id="1901b-107">High availability</span></span>

<span data-ttu-id="1901b-108">Microsoft supports SAP HANA high-availability methods "out of the box," which include:</span><span class="sxs-lookup"><span data-stu-id="1901b-108">Microsoft supports SAP HANA high-availability methods "out of the box," which include:</span></span>

- <span data-ttu-id="1901b-109">**Storage replication:** The storage system's ability to replicate all data to another location (within, or separate from, the same datacenter).</span><span class="sxs-lookup"><span data-stu-id="1901b-109">**Storage replication:** The storage system's ability to replicate all data to another location (within, or separate from, the same datacenter).</span></span> <span data-ttu-id="1901b-110">SAP HANA operates independently of this method.</span><span class="sxs-lookup"><span data-stu-id="1901b-110">SAP HANA operates independently of this method.</span></span>
- <span data-ttu-id="1901b-111">**HANA system replication:** The replication of all data in SAP HANA to a separate SAP HANA system.</span><span class="sxs-lookup"><span data-stu-id="1901b-111">**HANA system replication:** The replication of all data in SAP HANA to a separate SAP HANA system.</span></span> <span data-ttu-id="1901b-112">The recovery time objective is minimized through data replication at regular intervals.</span><span class="sxs-lookup"><span data-stu-id="1901b-112">The recovery time objective is minimized through data replication at regular intervals.</span></span> <span data-ttu-id="1901b-113">SAP HANA supports asynchronous, synchronous in-memory, and synchronous modes (recommended only for SAP HANA systems that are within the same datacenter or less than 100 KM apart).</span><span class="sxs-lookup"><span data-stu-id="1901b-113">SAP HANA supports asynchronous, synchronous in-memory, and synchronous modes (recommended only for SAP HANA systems that are within the same datacenter or less than 100 KM apart).</span></span> <span data-ttu-id="1901b-114">In the current design of HANA large-instance stamps, HANA system replication can be used for high availability only.</span><span class="sxs-lookup"><span data-stu-id="1901b-114">In the current design of HANA large-instance stamps, HANA system replication can be used for high availability only.</span></span>
- <span data-ttu-id="1901b-115">**Host auto-failover:** A local fault-recovery solution to use as an alternative to system replication.</span><span class="sxs-lookup"><span data-stu-id="1901b-115">**Host auto-failover:** A local fault-recovery solution to use as an alternative to system replication.</span></span> <span data-ttu-id="1901b-116">When the master node becomes unavailable, one or more standby SAP HANA nodes are configured in scale-out mode and SAP HANA automatically fails over to another node.</span><span class="sxs-lookup"><span data-stu-id="1901b-116">When the master node becomes unavailable, one or more standby SAP HANA nodes are configured in scale-out mode and SAP HANA automatically fails over to another node.</span></span>

<span data-ttu-id="1901b-117">For more information on SAP HANA high availability, see the following SAP information:</span><span class="sxs-lookup"><span data-stu-id="1901b-117">For more information on SAP HANA high availability, see the following SAP information:</span></span>

- [<span data-ttu-id="1901b-118">SAP HANA High-Availability Whitepaper</span><span class="sxs-lookup"><span data-stu-id="1901b-118">SAP HANA High-Availability Whitepaper</span></span>](http://go.sap.com/documents/2016/05/f8e5eeba-737c-0010-82c7-eda71af511fa.html)
- [<span data-ttu-id="1901b-119">SAP HANA Administration Guide</span><span class="sxs-lookup"><span data-stu-id="1901b-119">SAP HANA Administration Guide</span></span>](http://help.sap.com/hana/SAP_HANA_Administration_Guide_en.pdf)
- [<span data-ttu-id="1901b-120">SAP Academy Video on SAP HANA System Replication</span><span class="sxs-lookup"><span data-stu-id="1901b-120">SAP Academy Video on SAP HANA System Replication</span></span>](http://scn.sap.com/community/hana-in-memory/blog/2015/05/19/sap-hana-system-replication)
- [<span data-ttu-id="1901b-121">SAP Support Note #1999880 – FAQ on SAP HANA System Replication</span><span class="sxs-lookup"><span data-stu-id="1901b-121">SAP Support Note #1999880 – FAQ on SAP HANA System Replication</span></span>](https://bcs.wdf.sap.corp/sap/support/notes/1999880)
- <span data-ttu-id="1901b-122">[SAP Support Note #2165547 – SAP HANA Backup and Restore within SAP HANA System Replication Environment](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3231363535343726)</span><span class="sxs-lookup"><span data-stu-id="1901b-122">[SAP Support Note #2165547 – SAP HANA Backup and Restore within SAP HANA System Replication Environment](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3231363535343726)</span></span>
- <span data-ttu-id="1901b-123">[SAP Support Note #1984882 – Using SAP HANA System Replication for Hardware Exchange with Minimum/Zero Downtime](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3139383438383226)</span><span class="sxs-lookup"><span data-stu-id="1901b-123">[SAP Support Note #1984882 – Using SAP HANA System Replication for Hardware Exchange with Minimum/Zero Downtime](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3139383438383226)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="1901b-124">Disaster recovery</span><span class="sxs-lookup"><span data-stu-id="1901b-124">Disaster recovery</span></span>

<span data-ttu-id="1901b-125">SAP HANA on Azure (large instances) is offered in two Azure regions in a geopolitical region.</span><span class="sxs-lookup"><span data-stu-id="1901b-125">SAP HANA on Azure (large instances) is offered in two Azure regions in a geopolitical region.</span></span> <span data-ttu-id="1901b-126">Between the two large-instance stamps of two different regions is a direct network connectivity for replicating data during disaster recovery.</span><span class="sxs-lookup"><span data-stu-id="1901b-126">Between the two large-instance stamps of two different regions is a direct network connectivity for replicating data during disaster recovery.</span></span> <span data-ttu-id="1901b-127">The replication of the data is storage-infrastructure based.</span><span class="sxs-lookup"><span data-stu-id="1901b-127">The replication of the data is storage-infrastructure based.</span></span> <span data-ttu-id="1901b-128">The replication is not done by default.</span><span class="sxs-lookup"><span data-stu-id="1901b-128">The replication is not done by default.</span></span> <span data-ttu-id="1901b-129">It is done for the customer configurations that ordered the disaster recovery.</span><span class="sxs-lookup"><span data-stu-id="1901b-129">It is done for the customer configurations that ordered the disaster recovery.</span></span> <span data-ttu-id="1901b-130">In the current design, HANA system replication can't be used for disaster recovery.</span><span class="sxs-lookup"><span data-stu-id="1901b-130">In the current design, HANA system replication can't be used for disaster recovery.</span></span>

<span data-ttu-id="1901b-131">However, to take advantage of the disaster recovery, you need to start to design the network connectivity to the two different Azure regions.</span><span class="sxs-lookup"><span data-stu-id="1901b-131">However, to take advantage of the disaster recovery, you need to start to design the network connectivity to the two different Azure regions.</span></span> <span data-ttu-id="1901b-132">To do so, you need an Azure ExpressRoute circuit connection from on-premises in your main Azure region and another circuit connection from on-premises to your disaster-recovery region.</span><span class="sxs-lookup"><span data-stu-id="1901b-132">To do so, you need an Azure ExpressRoute circuit connection from on-premises in your main Azure region and another circuit connection from on-premises to your disaster-recovery region.</span></span> <span data-ttu-id="1901b-133">This measure would cover a situation in which a complete Azure region, including a Microsoft enterprise edge router (MSEE) location, has an issue.</span><span class="sxs-lookup"><span data-stu-id="1901b-133">This measure would cover a situation in which a complete Azure region, including a Microsoft enterprise edge router (MSEE) location, has an issue.</span></span>

<span data-ttu-id="1901b-134">As a second measure, you can connect all Azure virtual networks that connect to SAP HANA on Azure (large instances) in one of the regions to both of those ExpressRoute circuits.</span><span class="sxs-lookup"><span data-stu-id="1901b-134">As a second measure, you can connect all Azure virtual networks that connect to SAP HANA on Azure (large instances) in one of the regions to both of those ExpressRoute circuits.</span></span> <span data-ttu-id="1901b-135">This measure addresses a case where only one of the MSEE locations that connects your on-premises location with Azure goes off duty.</span><span class="sxs-lookup"><span data-stu-id="1901b-135">This measure addresses a case where only one of the MSEE locations that connects your on-premises location with Azure goes off duty.</span></span>

<span data-ttu-id="1901b-136">The following figure shows the optimal configuration for disaster recovery:</span><span class="sxs-lookup"><span data-stu-id="1901b-136">The following figure shows the optimal configuration for disaster recovery:</span></span>

![Optimal configuration for disaster recovery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/hana-overview-high-availability-disaster-recovery/image1-optimal-configuration.png)

<span data-ttu-id="1901b-138">The optimal case for a disaster-recovery configuration of the network is to have two ExpressRoute circuits from on-premises to the two different Azure regions.</span><span class="sxs-lookup"><span data-stu-id="1901b-138">The optimal case for a disaster-recovery configuration of the network is to have two ExpressRoute circuits from on-premises to the two different Azure regions.</span></span> <span data-ttu-id="1901b-139">One circuit goes to region #1, running a production instance.</span><span class="sxs-lookup"><span data-stu-id="1901b-139">One circuit goes to region #1, running a production instance.</span></span> <span data-ttu-id="1901b-140">The second ExpressRoute circuit goes to region #2, running some non-production HANA instances.</span><span class="sxs-lookup"><span data-stu-id="1901b-140">The second ExpressRoute circuit goes to region #2, running some non-production HANA instances.</span></span> <span data-ttu-id="1901b-141">(This is important if an entire Azure region, including the MSEE and large-instance stamp, goes off the grid.)</span><span class="sxs-lookup"><span data-stu-id="1901b-141">(This is important if an entire Azure region, including the MSEE and large-instance stamp, goes off the grid.)</span></span>

<span data-ttu-id="1901b-142">As a second measure, the various virtual networks are connected to the various ExpressRoute circuits that are connected to SAP HANA on Azure (large instances).</span><span class="sxs-lookup"><span data-stu-id="1901b-142">As a second measure, the various virtual networks are connected to the various ExpressRoute circuits that are connected to SAP HANA on Azure (large instances).</span></span> <span data-ttu-id="1901b-143">You can bypass the location where an MSEE is failing, or you can lower the recovery point objective for disaster recovery, as we discuss later.</span><span class="sxs-lookup"><span data-stu-id="1901b-143">You can bypass the location where an MSEE is failing, or you can lower the recovery point objective for disaster recovery, as we discuss later.</span></span>

<span data-ttu-id="1901b-144">The next requirements for a disaster-recovery setup are:</span><span class="sxs-lookup"><span data-stu-id="1901b-144">The next requirements for a disaster-recovery setup are:</span></span>

- <span data-ttu-id="1901b-145">You must order SAP HANA on Azure (large instances) SKUs of the same size as your production SKUs and deploy them in the disaster-recovery region.</span><span class="sxs-lookup"><span data-stu-id="1901b-145">You must order SAP HANA on Azure (large instances) SKUs of the same size as your production SKUs and deploy them in the disaster-recovery region.</span></span> <span data-ttu-id="1901b-146">These instances can be used to run test, sandbox, or QA HANA instances.</span><span class="sxs-lookup"><span data-stu-id="1901b-146">These instances can be used to run test, sandbox, or QA HANA instances.</span></span>
- <span data-ttu-id="1901b-147">You must order a disaster-recovery profile for each of your SAP HANA on Azure (large instances) SKUs that you want to recover in the disaster-recovery site, if necessary.</span><span class="sxs-lookup"><span data-stu-id="1901b-147">You must order a disaster-recovery profile for each of your SAP HANA on Azure (large instances) SKUs that you want to recover in the disaster-recovery site, if necessary.</span></span> <span data-ttu-id="1901b-148">This action leads to the allocation of storage volumes, which are the target of the storage replication from your production region into the disaster-recovery region.</span><span class="sxs-lookup"><span data-stu-id="1901b-148">This action leads to the allocation of storage volumes, which are the target of the storage replication from your production region into the disaster-recovery region.</span></span>

<span data-ttu-id="1901b-149">After you meet the preceding requirements, it is your responsibility to start the storage replication.</span><span class="sxs-lookup"><span data-stu-id="1901b-149">After you meet the preceding requirements, it is your responsibility to start the storage replication.</span></span> <span data-ttu-id="1901b-150">In the storage infrastructure used for SAP HANA on Azure (large instances), the basis of storage replication is storage snapshots.</span><span class="sxs-lookup"><span data-stu-id="1901b-150">In the storage infrastructure used for SAP HANA on Azure (large instances), the basis of storage replication is storage snapshots.</span></span> <span data-ttu-id="1901b-151">To start the disaster-recovery replication, you need to perform:</span><span class="sxs-lookup"><span data-stu-id="1901b-151">To start the disaster-recovery replication, you need to perform:</span></span>

- <span data-ttu-id="1901b-152">A snapshot of your boot LUN, as described earlier.</span><span class="sxs-lookup"><span data-stu-id="1901b-152">A snapshot of your boot LUN, as described earlier.</span></span>
- <span data-ttu-id="1901b-153">A snapshot of your HANA-related volumes, as described earlier.</span><span class="sxs-lookup"><span data-stu-id="1901b-153">A snapshot of your HANA-related volumes, as described earlier.</span></span>

<span data-ttu-id="1901b-154">After you execute these snapshots, an initial replica of the volumes is seeded on the volumes that are associated with your disaster-recovery profile in the disaster-recovery region.</span><span class="sxs-lookup"><span data-stu-id="1901b-154">After you execute these snapshots, an initial replica of the volumes is seeded on the volumes that are associated with your disaster-recovery profile in the disaster-recovery region.</span></span>

<span data-ttu-id="1901b-155">Subsequently, the most recent storage snapshot is used every hour to replicate the deltas that develop on the storage volumes.</span><span class="sxs-lookup"><span data-stu-id="1901b-155">Subsequently, the most recent storage snapshot is used every hour to replicate the deltas that develop on the storage volumes.</span></span>

<span data-ttu-id="1901b-156">The recovery point objective that's achieved with this configuration is from 60 to 90 minutes.</span><span class="sxs-lookup"><span data-stu-id="1901b-156">The recovery point objective that's achieved with this configuration is from 60 to 90 minutes.</span></span> <span data-ttu-id="1901b-157">To achieve a better recovery point objective in the disaster-recovery case, copy the HANA transaction log backups from SAP HANA on Azure (large instances) to the other Azure region.</span><span class="sxs-lookup"><span data-stu-id="1901b-157">To achieve a better recovery point objective in the disaster-recovery case, copy the HANA transaction log backups from SAP HANA on Azure (large instances) to the other Azure region.</span></span> <span data-ttu-id="1901b-158">To achieve this recovery point objective, do the following:</span><span class="sxs-lookup"><span data-stu-id="1901b-158">To achieve this recovery point objective, do the following:</span></span>

1. <span data-ttu-id="1901b-159">Back up the HANA transaction log as frequently as possible to /hana/log/backup.</span><span class="sxs-lookup"><span data-stu-id="1901b-159">Back up the HANA transaction log as frequently as possible to /hana/log/backup.</span></span>
2. <span data-ttu-id="1901b-160">Copy the transaction log backups when they are finished to an Azure virtual machine (VM), which is in a virtual network that's connected to the SAP HANA on Azure (large instances) server.</span><span class="sxs-lookup"><span data-stu-id="1901b-160">Copy the transaction log backups when they are finished to an Azure virtual machine (VM), which is in a virtual network that's connected to the SAP HANA on Azure (large instances) server.</span></span>
3. <span data-ttu-id="1901b-161">From that VM, copy the backup to a VM that's in a virtual network in the disaster-recovery region.</span><span class="sxs-lookup"><span data-stu-id="1901b-161">From that VM, copy the backup to a VM that's in a virtual network in the disaster-recovery region.</span></span>
4. <span data-ttu-id="1901b-162">Keep the transaction log backups in that region in the VM.</span><span class="sxs-lookup"><span data-stu-id="1901b-162">Keep the transaction log backups in that region in the VM.</span></span>

<span data-ttu-id="1901b-163">In case of disaster, after the disaster-recovery profile has been deployed on an actual server, copy the transaction log backups from the VM to the SAP HANA on Azure (large instances) that is now the primary server in the disaster-recovery region, and restore those backups.</span><span class="sxs-lookup"><span data-stu-id="1901b-163">In case of disaster, after the disaster-recovery profile has been deployed on an actual server, copy the transaction log backups from the VM to the SAP HANA on Azure (large instances) that is now the primary server in the disaster-recovery region, and restore those backups.</span></span> <span data-ttu-id="1901b-164">This recovery is possible because the state of HANA on the disaster-recovery disks is that of a HANA snapshot.</span><span class="sxs-lookup"><span data-stu-id="1901b-164">This recovery is possible because the state of HANA on the disaster-recovery disks is that of a HANA snapshot.</span></span> <span data-ttu-id="1901b-165">This is the offset point for further restorations of transaction log backups.</span><span class="sxs-lookup"><span data-stu-id="1901b-165">This is the offset point for further restorations of transaction log backups.</span></span>

## <a name="backup-and-restore"></a><span data-ttu-id="1901b-166">Backup and restore</span><span class="sxs-lookup"><span data-stu-id="1901b-166">Backup and restore</span></span>

<span data-ttu-id="1901b-167">One of the most important aspects to operating databases is making sure the database can be protected from various catastrophic events.</span><span class="sxs-lookup"><span data-stu-id="1901b-167">One of the most important aspects to operating databases is making sure the database can be protected from various catastrophic events.</span></span> <span data-ttu-id="1901b-168">These events can be caused by anything from natural disasters to simple user errors.</span><span class="sxs-lookup"><span data-stu-id="1901b-168">These events can be caused by anything from natural disasters to simple user errors.</span></span>

<span data-ttu-id="1901b-169">Backing up a database, with the ability to restore it to any point in time (such as before somebody deleted critical data), allows restoration to a state that is as close as possible to the way it was before the disruption occurred.</span><span class="sxs-lookup"><span data-stu-id="1901b-169">Backing up a database, with the ability to restore it to any point in time (such as before somebody deleted critical data), allows restoration to a state that is as close as possible to the way it was before the disruption occurred.</span></span>

<span data-ttu-id="1901b-170">Two types of backups must be performed for best results:</span><span class="sxs-lookup"><span data-stu-id="1901b-170">Two types of backups must be performed for best results:</span></span>

- <span data-ttu-id="1901b-171">Database backups</span><span class="sxs-lookup"><span data-stu-id="1901b-171">Database backups</span></span>
- <span data-ttu-id="1901b-172">Transaction log backups</span><span class="sxs-lookup"><span data-stu-id="1901b-172">Transaction log backups</span></span>

<span data-ttu-id="1901b-173">In addition to full database backups performed at an application-level, you can be even more thorough by performing backups with storage snapshots.</span><span class="sxs-lookup"><span data-stu-id="1901b-173">In addition to full database backups performed at an application-level, you can be even more thorough by performing backups with storage snapshots.</span></span> <span data-ttu-id="1901b-174">Performing log backups is also important for restoring the database (and to empty the logs from already committed transactions).</span><span class="sxs-lookup"><span data-stu-id="1901b-174">Performing log backups is also important for restoring the database (and to empty the logs from already committed transactions).</span></span>

<span data-ttu-id="1901b-175">SAP HANA on Azure (large instances) offers two backup and restore options:</span><span class="sxs-lookup"><span data-stu-id="1901b-175">SAP HANA on Azure (large instances) offers two backup and restore options:</span></span>

- <span data-ttu-id="1901b-176">Do it yourself (DIY).</span><span class="sxs-lookup"><span data-stu-id="1901b-176">Do it yourself (DIY).</span></span> <span data-ttu-id="1901b-177">After you calculate to ensure enough disk space, perform full database and log backups by using disk backup methods (to those disks).</span><span class="sxs-lookup"><span data-stu-id="1901b-177">After you calculate to ensure enough disk space, perform full database and log backups by using disk backup methods (to those disks).</span></span> <span data-ttu-id="1901b-178">Over time, the backups are copied to an Azure storage account (after you set up an Azure-based file server with virtually unlimited storage), or use an Azure Backup vault or Azure cold storage.</span><span class="sxs-lookup"><span data-stu-id="1901b-178">Over time, the backups are copied to an Azure storage account (after you set up an Azure-based file server with virtually unlimited storage), or use an Azure Backup vault or Azure cold storage.</span></span> <span data-ttu-id="1901b-179">Another option is to use a third-party data protection tool, such as Commvault, to store the backups after they are copied to a storage account.</span><span class="sxs-lookup"><span data-stu-id="1901b-179">Another option is to use a third-party data protection tool, such as Commvault, to store the backups after they are copied to a storage account.</span></span> <span data-ttu-id="1901b-180">The DIY backup option might also be necessary for data that needs to be stored for longer periods for compliancy and auditing purposes.</span><span class="sxs-lookup"><span data-stu-id="1901b-180">The DIY backup option might also be necessary for data that needs to be stored for longer periods for compliancy and auditing purposes.</span></span>
- <span data-ttu-id="1901b-181">Use the backup and restore functionality that the underlying infrastructure of SAP HANA on Azure (large instances) provides.</span><span class="sxs-lookup"><span data-stu-id="1901b-181">Use the backup and restore functionality that the underlying infrastructure of SAP HANA on Azure (large instances) provides.</span></span> <span data-ttu-id="1901b-182">This option fulfills the need for backups, and it makes manual backups nearly obsolete (except where data backups are required for compliance purposes).</span><span class="sxs-lookup"><span data-stu-id="1901b-182">This option fulfills the need for backups, and it makes manual backups nearly obsolete (except where data backups are required for compliance purposes).</span></span> <span data-ttu-id="1901b-183">The rest of this section addresses the backup and restore functionality that's offered with HANA (large instances).</span><span class="sxs-lookup"><span data-stu-id="1901b-183">The rest of this section addresses the backup and restore functionality that's offered with HANA (large instances).</span></span>

> [!NOTE]
> <span data-ttu-id="1901b-184">The snapshot technology that is used by the underlying infrastructure of HANA (large instances) has a dependency on SAP HANA snapshots.</span><span class="sxs-lookup"><span data-stu-id="1901b-184">The snapshot technology that is used by the underlying infrastructure of HANA (large instances) has a dependency on SAP HANA snapshots.</span></span> <span data-ttu-id="1901b-185">SAP HANA snapshots do not work in conjunction with SAP HANA Multitenant Database Containers.</span><span class="sxs-lookup"><span data-stu-id="1901b-185">SAP HANA snapshots do not work in conjunction with SAP HANA Multitenant Database Containers.</span></span> <span data-ttu-id="1901b-186">As a result, this method of backup cannot be used to deploy SAP HANA Multitenant Database Containers.</span><span class="sxs-lookup"><span data-stu-id="1901b-186">As a result, this method of backup cannot be used to deploy SAP HANA Multitenant Database Containers.</span></span>

### <a name="using-storage-snapshots-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="1901b-187">Using storage snapshots of SAP HANA on Azure (large instances)</span><span class="sxs-lookup"><span data-stu-id="1901b-187">Using storage snapshots of SAP HANA on Azure (large instances)</span></span>

<span data-ttu-id="1901b-188">The storage infrastructure underlying SAP HANA on Azure (large instances) supports the notion of a storage snapshot of volumes.</span><span class="sxs-lookup"><span data-stu-id="1901b-188">The storage infrastructure underlying SAP HANA on Azure (large instances) supports the notion of a storage snapshot of volumes.</span></span> <span data-ttu-id="1901b-189">Both backup and restoration of a particular volume are supported, with the following considerations:</span><span class="sxs-lookup"><span data-stu-id="1901b-189">Both backup and restoration of a particular volume are supported, with the following considerations:</span></span>

- <span data-ttu-id="1901b-190">Instead of database backups, storage volume snapshots are taken on a frequent basis.</span><span class="sxs-lookup"><span data-stu-id="1901b-190">Instead of database backups, storage volume snapshots are taken on a frequent basis.</span></span>
- <span data-ttu-id="1901b-191">The storage snapshot initiates an SAP HANA snapshot before it executes the storage snapshot.</span><span class="sxs-lookup"><span data-stu-id="1901b-191">The storage snapshot initiates an SAP HANA snapshot before it executes the storage snapshot.</span></span> <span data-ttu-id="1901b-192">This SAP HANA snapshot is the setup point for eventual log restorations after recovery of the storage snapshot.</span><span class="sxs-lookup"><span data-stu-id="1901b-192">This SAP HANA snapshot is the setup point for eventual log restorations after recovery of the storage snapshot.</span></span>
- <span data-ttu-id="1901b-193">At the point where the storage snapshot is executed successfully, the SAP HANA snapshot is deleted.</span><span class="sxs-lookup"><span data-stu-id="1901b-193">At the point where the storage snapshot is executed successfully, the SAP HANA snapshot is deleted.</span></span>
- <span data-ttu-id="1901b-194">Log backups are taken frequently and stored in the log backup volume or in Azure.</span><span class="sxs-lookup"><span data-stu-id="1901b-194">Log backups are taken frequently and stored in the log backup volume or in Azure.</span></span>
- <span data-ttu-id="1901b-195">If the database must be restored to a certain point in time, a request is made to Microsoft Azure Support (production outage) or SAP HANA on Azure Service Management to restore to a certain storage snapshot (for example, a planned restoration of a sandbox system to its original state).</span><span class="sxs-lookup"><span data-stu-id="1901b-195">If the database must be restored to a certain point in time, a request is made to Microsoft Azure Support (production outage) or SAP HANA on Azure Service Management to restore to a certain storage snapshot (for example, a planned restoration of a sandbox system to its original state).</span></span>
- <span data-ttu-id="1901b-196">The SAP HANA snapshot that's included in the storage snapshot is an offset point for applying log backups that have been executed and stored after the storage snapshot was taken.</span><span class="sxs-lookup"><span data-stu-id="1901b-196">The SAP HANA snapshot that's included in the storage snapshot is an offset point for applying log backups that have been executed and stored after the storage snapshot was taken.</span></span>
- <span data-ttu-id="1901b-197">These log backups are taken to restore the database back to a certain point in time.</span><span class="sxs-lookup"><span data-stu-id="1901b-197">These log backups are taken to restore the database back to a certain point in time.</span></span>

<span data-ttu-id="1901b-198">Specifying the backup\_name creates a snapshot of the following volumes:</span><span class="sxs-lookup"><span data-stu-id="1901b-198">Specifying the backup\_name creates a snapshot of the following volumes:</span></span>

- <span data-ttu-id="1901b-199">hana/data</span><span class="sxs-lookup"><span data-stu-id="1901b-199">hana/data</span></span>
- <span data-ttu-id="1901b-200">hana/log</span><span class="sxs-lookup"><span data-stu-id="1901b-200">hana/log</span></span>
- <span data-ttu-id="1901b-201">hana/log\_backup (mounted as backup into hana/log)</span><span class="sxs-lookup"><span data-stu-id="1901b-201">hana/log\_backup (mounted as backup into hana/log)</span></span>
- <span data-ttu-id="1901b-202">hana/shared</span><span class="sxs-lookup"><span data-stu-id="1901b-202">hana/shared</span></span>

### <a name="storage-snapshot-considerations"></a><span data-ttu-id="1901b-203">Storage snapshot considerations</span><span class="sxs-lookup"><span data-stu-id="1901b-203">Storage snapshot considerations</span></span>

>[!NOTE]
><span data-ttu-id="1901b-204">Storage snapshots are _not_ provided free of charge, because additional storage space must be allocated.</span><span class="sxs-lookup"><span data-stu-id="1901b-204">Storage snapshots are _not_ provided free of charge, because additional storage space must be allocated.</span></span>

<span data-ttu-id="1901b-205">The specific mechanics of storage snapshots for SAP HANA on Azure (large instances) include:</span><span class="sxs-lookup"><span data-stu-id="1901b-205">The specific mechanics of storage snapshots for SAP HANA on Azure (large instances) include:</span></span>

- <span data-ttu-id="1901b-206">A specific storage snapshot (at the point in time when it is taken) consumes very little storage.</span><span class="sxs-lookup"><span data-stu-id="1901b-206">A specific storage snapshot (at the point in time when it is taken) consumes very little storage.</span></span>
- <span data-ttu-id="1901b-207">As data content changes and the content in SAP HANA data files change on the storage volume, the snapshot needs to store the original block content.</span><span class="sxs-lookup"><span data-stu-id="1901b-207">As data content changes and the content in SAP HANA data files change on the storage volume, the snapshot needs to store the original block content.</span></span>
- <span data-ttu-id="1901b-208">The storage snapshot increases in size.</span><span class="sxs-lookup"><span data-stu-id="1901b-208">The storage snapshot increases in size.</span></span> <span data-ttu-id="1901b-209">The longer the snapshot exists, the larger the storage snapshot becomes.</span><span class="sxs-lookup"><span data-stu-id="1901b-209">The longer the snapshot exists, the larger the storage snapshot becomes.</span></span>
- <span data-ttu-id="1901b-210">The more changes made to the SAP HANA database volume over the lifetime of a storage snapshot, the larger the space consumption of the storage snapshot becomes.</span><span class="sxs-lookup"><span data-stu-id="1901b-210">The more changes made to the SAP HANA database volume over the lifetime of a storage snapshot, the larger the space consumption of the storage snapshot becomes.</span></span>

<span data-ttu-id="1901b-211">SAP HANA on Azure (large instances) comes with fixed volume sizes for the SAP HANA data and log volume.</span><span class="sxs-lookup"><span data-stu-id="1901b-211">SAP HANA on Azure (large instances) comes with fixed volume sizes for the SAP HANA data and log volume.</span></span> <span data-ttu-id="1901b-212">Performing snapshots of those volumes eats into your volume space, so it is your responsibility to schedule storage snapshots (within the SAP HANA on Azure [large instances] process).</span><span class="sxs-lookup"><span data-stu-id="1901b-212">Performing snapshots of those volumes eats into your volume space, so it is your responsibility to schedule storage snapshots (within the SAP HANA on Azure [large instances] process).</span></span>

<span data-ttu-id="1901b-213">The following sections provide information for performing these snapshots, including general recommendations:</span><span class="sxs-lookup"><span data-stu-id="1901b-213">The following sections provide information for performing these snapshots, including general recommendations:</span></span>

- <span data-ttu-id="1901b-214">Though the hardware can sustain 255 snapshots per volume, we highly recommend that you stay well below this number.</span><span class="sxs-lookup"><span data-stu-id="1901b-214">Though the hardware can sustain 255 snapshots per volume, we highly recommend that you stay well below this number.</span></span>
- <span data-ttu-id="1901b-215">Before you perform storage snapshots, monitor and keep track of free space.</span><span class="sxs-lookup"><span data-stu-id="1901b-215">Before you perform storage snapshots, monitor and keep track of free space.</span></span>
- <span data-ttu-id="1901b-216">Lower the number of storage snapshots based on free space.</span><span class="sxs-lookup"><span data-stu-id="1901b-216">Lower the number of storage snapshots based on free space.</span></span> <span data-ttu-id="1901b-217">You might need to lower the number of snapshots that you keep, or you might need to extend the volumes.</span><span class="sxs-lookup"><span data-stu-id="1901b-217">You might need to lower the number of snapshots that you keep, or you might need to extend the volumes.</span></span> <span data-ttu-id="1901b-218">(You can order additional storage in 1-TB units.)</span><span class="sxs-lookup"><span data-stu-id="1901b-218">(You can order additional storage in 1-TB units.)</span></span>
- <span data-ttu-id="1901b-219">During activities such as moving data into SAP HANA with system migration tools (with R3load, or by restoring SAP HANA databases from backups), we highly recommended that you not perform any storage snapshots.</span><span class="sxs-lookup"><span data-stu-id="1901b-219">During activities such as moving data into SAP HANA with system migration tools (with R3load, or by restoring SAP HANA databases from backups), we highly recommended that you not perform any storage snapshots.</span></span> <span data-ttu-id="1901b-220">(If a system migration is being done on a new SAP HANA system, storage snapshots would not need to be performed.)</span><span class="sxs-lookup"><span data-stu-id="1901b-220">(If a system migration is being done on a new SAP HANA system, storage snapshots would not need to be performed.)</span></span>
- <span data-ttu-id="1901b-221">During larger reorganizations of SAP HANA tables, storage snapshots should be avoided if possible.</span><span class="sxs-lookup"><span data-stu-id="1901b-221">During larger reorganizations of SAP HANA tables, storage snapshots should be avoided if possible.</span></span>
- <span data-ttu-id="1901b-222">Storage snapshots are a prerequisite to engaging the disaster-recovery capabilities of SAP HANA on Azure (large instances).</span><span class="sxs-lookup"><span data-stu-id="1901b-222">Storage snapshots are a prerequisite to engaging the disaster-recovery capabilities of SAP HANA on Azure (large instances).</span></span>

### <a name="setting-up-storage-snapshots"></a><span data-ttu-id="1901b-223">Setting up storage snapshots</span><span class="sxs-lookup"><span data-stu-id="1901b-223">Setting up storage snapshots</span></span>

1. <span data-ttu-id="1901b-224">Make sure that Perl is installed in the Linux operating system on the HANA (large instances) server.</span><span class="sxs-lookup"><span data-stu-id="1901b-224">Make sure that Perl is installed in the Linux operating system on the HANA (large instances) server.</span></span>
2. <span data-ttu-id="1901b-225">Modify /etc/ssh/ssh\_config to add the line _MACs hmac-sha1_.</span><span class="sxs-lookup"><span data-stu-id="1901b-225">Modify /etc/ssh/ssh\_config to add the line _MACs hmac-sha1_.</span></span>
3. <span data-ttu-id="1901b-226">Create an SAP HANA backup user account on the master node for each SAP HANA instance you are running (if applicable).</span><span class="sxs-lookup"><span data-stu-id="1901b-226">Create an SAP HANA backup user account on the master node for each SAP HANA instance you are running (if applicable).</span></span>
4. <span data-ttu-id="1901b-227">The SAP HANA HDB client must be installed on all SAP HANA (large instances) servers.</span><span class="sxs-lookup"><span data-stu-id="1901b-227">The SAP HANA HDB client must be installed on all SAP HANA (large instances) servers.</span></span>
5. <span data-ttu-id="1901b-228">On the first SAP HANA (large instances) server of each region, a public key must be created to access the underlying storage infrastructure that controls snapshot creation.</span><span class="sxs-lookup"><span data-stu-id="1901b-228">On the first SAP HANA (large instances) server of each region, a public key must be created to access the underlying storage infrastructure that controls snapshot creation.</span></span>
6. <span data-ttu-id="1901b-229">Copy the script azure\_hana\_backup.pl from /scripts to the location of **hdbsql** of the SAP HANA installation.</span><span class="sxs-lookup"><span data-stu-id="1901b-229">Copy the script azure\_hana\_backup.pl from /scripts to the location of **hdbsql** of the SAP HANA installation.</span></span>
7. <span data-ttu-id="1901b-230">Copy the HANABackupDetails.txt file from /scripts to the same location as the Perl script.</span><span class="sxs-lookup"><span data-stu-id="1901b-230">Copy the HANABackupDetails.txt file from /scripts to the same location as the Perl script.</span></span>
8. <span data-ttu-id="1901b-231">Modify the HANABackupDetails.txt file as necessary for the appropriate customer specifications.</span><span class="sxs-lookup"><span data-stu-id="1901b-231">Modify the HANABackupDetails.txt file as necessary for the appropriate customer specifications.</span></span>

### <a name="step-1-install-sap-hana-hdbclient"></a><span data-ttu-id="1901b-232">Step 1: Install SAP HANA HDBClient</span><span class="sxs-lookup"><span data-stu-id="1901b-232">Step 1: Install SAP HANA HDBClient</span></span>

<span data-ttu-id="1901b-233">The Linux installed on SAP HANA on Azure (large instances) includes the folders and scripts necessary to execute SAP HANA storage snapshots for backup and disaster-recovery purposes.</span><span class="sxs-lookup"><span data-stu-id="1901b-233">The Linux installed on SAP HANA on Azure (large instances) includes the folders and scripts necessary to execute SAP HANA storage snapshots for backup and disaster-recovery purposes.</span></span> <span data-ttu-id="1901b-234">However, it is your responsibility to install SAP HANA HDBclient while you are installing SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1901b-234">However, it is your responsibility to install SAP HANA HDBclient while you are installing SAP HANA.</span></span> <span data-ttu-id="1901b-235">(Microsoft installs neither the HDBclient nor SAP HANA.)</span><span class="sxs-lookup"><span data-stu-id="1901b-235">(Microsoft installs neither the HDBclient nor SAP HANA.)</span></span>

### <a name="step-2-change-etcsshsshconfig"></a><span data-ttu-id="1901b-236">Step 2: Change /etc/ssh/ssh\_config</span><span class="sxs-lookup"><span data-stu-id="1901b-236">Step 2: Change /etc/ssh/ssh\_config</span></span>

<span data-ttu-id="1901b-237">Change /etc/ssh/ssh\_config by adding _MACs hmac-sha1_ line as shown here:</span><span class="sxs-lookup"><span data-stu-id="1901b-237">Change /etc/ssh/ssh\_config by adding _MACs hmac-sha1_ line as shown here:</span></span>
```
#   RhostsRSAAuthentication no
#   RSAAuthentication yes
#   PasswordAuthentication yes
#   HostbasedAuthentication no
#   GSSAPIAuthentication no
#   GSSAPIDelegateCredentials no
#   GSSAPIKeyExchange no
#   GSSAPITrustDNS no
#   BatchMode no
#   CheckHostIP yes
#   AddressFamily any
#   ConnectTimeout 0
#   StrictHostKeyChecking ask
#   IdentityFile ~/.ssh/identity
#   IdentityFile ~/.ssh/id_rsa
#   IdentityFile ~/.ssh/id_dsa
#   Port 22
Protocol 2
#   Cipher 3des
#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,arcfour256,arcfour128,aes128-cbc,3des-cbc
#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com,hmac-ripemd160
MACs hmac-sha1
#   EscapeChar ~
#   Tunnel no
#   TunnelDevice any:any
#   PermitLocalCommand no
#   VisualHostKey no
#   ProxyCommand ssh -q -W %h:%p gateway.example.com
```

### <a name="step-3-create-a-public-key"></a><span data-ttu-id="1901b-238">Step 3: Create a public key</span><span class="sxs-lookup"><span data-stu-id="1901b-238">Step 3: Create a public key</span></span>

<span data-ttu-id="1901b-239">On the first SAP HANA on Azure (large instances) server in each Azure region, create a public key to be used to access the storage infrastructure so that you can create snapshots.</span><span class="sxs-lookup"><span data-stu-id="1901b-239">On the first SAP HANA on Azure (large instances) server in each Azure region, create a public key to be used to access the storage infrastructure so that you can create snapshots.</span></span> <span data-ttu-id="1901b-240">The public key ensures that a password is not required to sign in to the storage and that password credentials are not maintained.</span><span class="sxs-lookup"><span data-stu-id="1901b-240">The public key ensures that a password is not required to sign in to the storage and that password credentials are not maintained.</span></span> <span data-ttu-id="1901b-241">In Linux on the SAP HANA (large instances) server, execute the following command to generate the public key:</span><span class="sxs-lookup"><span data-stu-id="1901b-241">In Linux on the SAP HANA (large instances) server, execute the following command to generate the public key:</span></span>
```
  ssh-keygen –t dsa –b 1024
```
<span data-ttu-id="1901b-242">The new location is _/root/.ssh/id\_dsa.pub.</span><span class="sxs-lookup"><span data-stu-id="1901b-242">The new location is _/root/.ssh/id\_dsa.pub.</span></span> <span data-ttu-id="1901b-243">Do not enter an actual passphrase, or else you will be required to enter the passphrase each time you sign in.</span><span class="sxs-lookup"><span data-stu-id="1901b-243">Do not enter an actual passphrase, or else you will be required to enter the passphrase each time you sign in.</span></span> <span data-ttu-id="1901b-244">Instead, press **Enter** twice to remove the enter passphrase requirement for signing in.</span><span class="sxs-lookup"><span data-stu-id="1901b-244">Instead, press **Enter** twice to remove the enter passphrase requirement for signing in.</span></span>

<span data-ttu-id="1901b-245">Check to make sure that the public key was corrected as expected by changing folders to /root/.ssh/ and then executing the **ls** command.</span><span class="sxs-lookup"><span data-stu-id="1901b-245">Check to make sure that the public key was corrected as expected by changing folders to /root/.ssh/ and then executing the **ls** command.</span></span> <span data-ttu-id="1901b-246">If the key is present, you can copy it by running the following command:</span><span class="sxs-lookup"><span data-stu-id="1901b-246">If the key is present, you can copy it by running the following command:</span></span>

![Public key is copied by running this command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/hana-overview-high-availability-disaster-recovery/image2-public-key.png)

<span data-ttu-id="1901b-248">At this point, contact SAP HANA on Azure Service Management and provide the key.</span><span class="sxs-lookup"><span data-stu-id="1901b-248">At this point, contact SAP HANA on Azure Service Management and provide the key.</span></span> <span data-ttu-id="1901b-249">The service representative uses the public key to register it in the underlying storage infrastructure.</span><span class="sxs-lookup"><span data-stu-id="1901b-249">The service representative uses the public key to register it in the underlying storage infrastructure.</span></span>

### <a name="step-4-create-an-sap-hana-user-account"></a><span data-ttu-id="1901b-250">Step 4: Create an SAP HANA user account</span><span class="sxs-lookup"><span data-stu-id="1901b-250">Step 4: Create an SAP HANA user account</span></span>

<span data-ttu-id="1901b-251">Create an SAP HANA user account within SAP HANA Studio for backup purposes.</span><span class="sxs-lookup"><span data-stu-id="1901b-251">Create an SAP HANA user account within SAP HANA Studio for backup purposes.</span></span> <span data-ttu-id="1901b-252">This account must have the following privileges: _Backup Admin_ and _Catalog Read_.</span><span class="sxs-lookup"><span data-stu-id="1901b-252">This account must have the following privileges: _Backup Admin_ and _Catalog Read_.</span></span> <span data-ttu-id="1901b-253">In this example, the username SCADMIN is created.</span><span class="sxs-lookup"><span data-stu-id="1901b-253">In this example, the username SCADMIN is created.</span></span>

![Creating a user in HANA Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/hana-overview-high-availability-disaster-recovery/image3-creating-user.png)

### <a name="step-5-authorize-the-sap-hana-user-account"></a><span data-ttu-id="1901b-255">Step 5: Authorize the SAP HANA user account</span><span class="sxs-lookup"><span data-stu-id="1901b-255">Step 5: Authorize the SAP HANA user account</span></span>

<span data-ttu-id="1901b-256">Authorize the SAP HANA user account (to be used by the scripts without requiring authorization every time the script is run).</span><span class="sxs-lookup"><span data-stu-id="1901b-256">Authorize the SAP HANA user account (to be used by the scripts without requiring authorization every time the script is run).</span></span> <span data-ttu-id="1901b-257">The SAP HANA command `hdbuserstore` allows the creation of an SAP HANA user key, which is stored on one or more SAP HANA nodes.</span><span class="sxs-lookup"><span data-stu-id="1901b-257">The SAP HANA command `hdbuserstore` allows the creation of an SAP HANA user key, which is stored on one or more SAP HANA nodes.</span></span> <span data-ttu-id="1901b-258">The user key also allows the user to access SAP HANA without having to manage passwords from within the scripting process that's discussed later.</span><span class="sxs-lookup"><span data-stu-id="1901b-258">The user key also allows the user to access SAP HANA without having to manage passwords from within the scripting process that's discussed later.</span></span>

>[!IMPORTANT]
><span data-ttu-id="1901b-259">Run the following command as `_root_`.</span><span class="sxs-lookup"><span data-stu-id="1901b-259">Run the following command as `_root_`.</span></span> <span data-ttu-id="1901b-260">Otherwise, the script cannot work properly.</span><span class="sxs-lookup"><span data-stu-id="1901b-260">Otherwise, the script cannot work properly.</span></span>

<span data-ttu-id="1901b-261">Enter the `hdbuserstore` command as follows:</span><span class="sxs-lookup"><span data-stu-id="1901b-261">Enter the `hdbuserstore` command as follows:</span></span>

![Enter the hdbuserstore command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/hana-overview-high-availability-disaster-recovery/image4-hdbuserstore-command.png)

<span data-ttu-id="1901b-263">In the following example, where the user is SCADMIN01 and the hostname is lhanad01, the command is:</span><span class="sxs-lookup"><span data-stu-id="1901b-263">In the following example, where the user is SCADMIN01 and the hostname is lhanad01, the command is:</span></span>
```
hdbuserstore set SCADMIN01 lhanad01:30115 <backup username> <password>
```
<span data-ttu-id="1901b-264">Manage all scripting from a single server for scale-out HANA instances.</span><span class="sxs-lookup"><span data-stu-id="1901b-264">Manage all scripting from a single server for scale-out HANA instances.</span></span> <span data-ttu-id="1901b-265">In this example, the SAP HANA key SCADMIN01 must be altered for each host in a way that reflects the host that is related to the key.</span><span class="sxs-lookup"><span data-stu-id="1901b-265">In this example, the SAP HANA key SCADMIN01 must be altered for each host in a way that reflects the host that is related to the key.</span></span> <span data-ttu-id="1901b-266">That is, the SAP HANA backup account is amended with the instance number of the HANA DB, **lhanad**.</span><span class="sxs-lookup"><span data-stu-id="1901b-266">That is, the SAP HANA backup account is amended with the instance number of the HANA DB, **lhanad**.</span></span> <span data-ttu-id="1901b-267">The key must have administrative privileges on the host it is assigned to, and the backup user for scale-out must have access rights to all SAP HANA instances.</span><span class="sxs-lookup"><span data-stu-id="1901b-267">The key must have administrative privileges on the host it is assigned to, and the backup user for scale-out must have access rights to all SAP HANA instances.</span></span>
```
hdbuserstore set SCADMIN01 lhanad:30015 SCADMIN <password>
hdbuserstore set SCADMIN02 lhanad:30115 SCADMIN <password>
hdbuserstore set SCADMIN03 lhanad:30215 SCADMIN <password>
```

### <a name="step-6-copy-items-from-the-scripts-folder"></a><span data-ttu-id="1901b-268">Step 6: Copy items from the /scripts folder</span><span class="sxs-lookup"><span data-stu-id="1901b-268">Step 6: Copy items from the /scripts folder</span></span>

<span data-ttu-id="1901b-269">Copy the following items from the /scripts folder (included on the gold image of the installation) to the working directory for **hdbsql**.</span><span class="sxs-lookup"><span data-stu-id="1901b-269">Copy the following items from the /scripts folder (included on the gold image of the installation) to the working directory for **hdbsql**.</span></span> <span data-ttu-id="1901b-270">For current HANA installations, this directory is /hana/shared/D01/exe/linuxx86\_64/hdb.</span><span class="sxs-lookup"><span data-stu-id="1901b-270">For current HANA installations, this directory is /hana/shared/D01/exe/linuxx86\_64/hdb.</span></span>
```
azure\_hana\_backup.pl
testHANAConnection.pl
testStorageSnapshotConnection.pl
removeTestStorageSnapshot.pl
HANABackupCustomerDetails.txt
```
<span data-ttu-id="1901b-271">Copy the following items if they are running scale-out or OLAP:</span><span class="sxs-lookup"><span data-stu-id="1901b-271">Copy the following items if they are running scale-out or OLAP:</span></span>
```
azure\_hana\_backup\_bw.pl
testHANAConnectionBW.pl
testStorageSnapshotConnectionBW.pl
removeTestStorageSnapshotBW.pl
HANABackupCustomerDetailsBW.txt
```
<span data-ttu-id="1901b-272">The HANABackupCustomerDetails.txt file is modifiable as follows for a scale-up deployment.</span><span class="sxs-lookup"><span data-stu-id="1901b-272">The HANABackupCustomerDetails.txt file is modifiable as follows for a scale-up deployment.</span></span> <span data-ttu-id="1901b-273">It is the control and configuration file for the script that runs the storage snapshots.</span><span class="sxs-lookup"><span data-stu-id="1901b-273">It is the control and configuration file for the script that runs the storage snapshots.</span></span> <span data-ttu-id="1901b-274">You should have received the _Storage Backup Name_ and _Storage IP Address_ from SAP HANA on Azure Service Management when your instances were deployed.</span><span class="sxs-lookup"><span data-stu-id="1901b-274">You should have received the _Storage Backup Name_ and _Storage IP Address_ from SAP HANA on Azure Service Management when your instances were deployed.</span></span> <span data-ttu-id="1901b-275">You cannot modify the sequence, ordering, or spacing of any of the variables, or the script does not run properly.</span><span class="sxs-lookup"><span data-stu-id="1901b-275">You cannot modify the sequence, ordering, or spacing of any of the variables, or the script does not run properly.</span></span>

<span data-ttu-id="1901b-276">For a scale-up deployment, the configuration file would look like:</span><span class="sxs-lookup"><span data-stu-id="1901b-276">For a scale-up deployment, the configuration file would look like:</span></span>
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Created by customer using hdbuserstore
HANA Backup Name: SCADMIND01
```
<span data-ttu-id="1901b-277">For a scale-out configuration, the HANABackupCustomerDetailsBW.txt file would look like:</span><span class="sxs-lookup"><span data-stu-id="1901b-277">For a scale-out configuration, the HANABackupCustomerDetailsBW.txt file would look like:</span></span>
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Node IP addresses, instance numbers, and HANA backup name
#provided by customer.  HANA backup name created using
#hdbuserstore utility.
Node 1 IP Address: 10.254.15.21
Node 1 HANA instance number: 01
Node 1 HANA Backup Name: SCADMIN01
Node 2 IP Address: 10.254.15.22
Node 2 HANA instance number: 02
Node 2 HANA Backup Name: SCADMIN02
Node 3 IP Address: 10.254.15.23
Node 3 HANA instance number: 03
Node 3 HANA Backup Name: SCADMIN03
Node 4 IP Address: 10.254.15.24
Node 4 HANA instance number: 04
Node 4 HANA Backup Name: SCADMIN04
Node 5 IP Address: 10.254.15.25
Node 5 HANA instance number: 05
Node 5 HANA Backup Name: SCADMIN05
Node 6 IP Address: 10.254.15.26
Node 6 HANA instance number: 06
Node 6 HANA Backup Name: SCADMIN06
Node 7 IP Address: 10.254.15.27
Node 7 HANA instance number: 07
Node 7 HANA Backup Name: SCADMIN07
Node 8 IP Address: 10.254.15.28
Node 8 HANA instance number: 08
Node 8 HANA Backup Name: SCADMIN08
```
>[!NOTE]
><span data-ttu-id="1901b-278">Currently, only Node 1 details are used in the actual HANA storage snapshot script.</span><span class="sxs-lookup"><span data-stu-id="1901b-278">Currently, only Node 1 details are used in the actual HANA storage snapshot script.</span></span> <span data-ttu-id="1901b-279">We recommend that you test access to or from all HANA nodes so that, if the master backup node ever changes, you have already ensured that any other node can take its place by modifying the details in Node 1.</span><span class="sxs-lookup"><span data-stu-id="1901b-279">We recommend that you test access to or from all HANA nodes so that, if the master backup node ever changes, you have already ensured that any other node can take its place by modifying the details in Node 1.</span></span>

<span data-ttu-id="1901b-280">To check for the correct configurations in the configuration file or proper connectivity to the HANA instances, run either of the following scripts:</span><span class="sxs-lookup"><span data-stu-id="1901b-280">To check for the correct configurations in the configuration file or proper connectivity to the HANA instances, run either of the following scripts:</span></span>
- <span data-ttu-id="1901b-281">For a scale-up configuration (independent on SAP workload):</span><span class="sxs-lookup"><span data-stu-id="1901b-281">For a scale-up configuration (independent on SAP workload):</span></span>

 ```
testHANAConnection.pl
```
- <span data-ttu-id="1901b-282">For a scale-out configuration:</span><span class="sxs-lookup"><span data-stu-id="1901b-282">For a scale-out configuration:</span></span>

 ```
testHANAConnectionBW.pl
```

<span data-ttu-id="1901b-283">Ensure that the master HANA instance has access to all required HANA servers.</span><span class="sxs-lookup"><span data-stu-id="1901b-283">Ensure that the master HANA instance has access to all required HANA servers.</span></span> <span data-ttu-id="1901b-284">There are no parameters to the script, but you must complete the appropriate HANABackupCustomerDetails/ HANABackupCustomerDetailsBW file for the script to run properly.</span><span class="sxs-lookup"><span data-stu-id="1901b-284">There are no parameters to the script, but you must complete the appropriate HANABackupCustomerDetails/ HANABackupCustomerDetailsBW file for the script to run properly.</span></span> <span data-ttu-id="1901b-285">Because only the shell command error codes are returned, it is not possible for the script to error-check every instance.</span><span class="sxs-lookup"><span data-stu-id="1901b-285">Because only the shell command error codes are returned, it is not possible for the script to error-check every instance.</span></span> <span data-ttu-id="1901b-286">Even so, the script does provide some helpful comments for you to double-check.</span><span class="sxs-lookup"><span data-stu-id="1901b-286">Even so, the script does provide some helpful comments for you to double-check.</span></span>

<span data-ttu-id="1901b-287">To run the script:</span><span class="sxs-lookup"><span data-stu-id="1901b-287">To run the script:</span></span>
```
 ./testHANAConnection.pl
```
 <span data-ttu-id="1901b-288">If the script successfully obtains the status of the HANA instance, it displays a message that the HANA connection was successful.</span><span class="sxs-lookup"><span data-stu-id="1901b-288">If the script successfully obtains the status of the HANA instance, it displays a message that the HANA connection was successful.</span></span>

<span data-ttu-id="1901b-289">Additionally, there is a second type of script you can use to check the master HANA instance server's ability to sign in to the storage.</span><span class="sxs-lookup"><span data-stu-id="1901b-289">Additionally, there is a second type of script you can use to check the master HANA instance server's ability to sign in to the storage.</span></span> <span data-ttu-id="1901b-290">Before you execute the azure\_hana\_backup(\_bw).pl script, you must execute the next script.</span><span class="sxs-lookup"><span data-stu-id="1901b-290">Before you execute the azure\_hana\_backup(\_bw).pl script, you must execute the next script.</span></span> <span data-ttu-id="1901b-291">If a volume contains no snapshots, it is impossible to determine whether the volume is simply empty or there is an ssh failure to obtain the snapshot details.</span><span class="sxs-lookup"><span data-stu-id="1901b-291">If a volume contains no snapshots, it is impossible to determine whether the volume is simply empty or there is an ssh failure to obtain the snapshot details.</span></span> <span data-ttu-id="1901b-292">For this reason, the script executes two steps:</span><span class="sxs-lookup"><span data-stu-id="1901b-292">For this reason, the script executes two steps:</span></span>

- <span data-ttu-id="1901b-293">It verifies that the storage console is accessible.</span><span class="sxs-lookup"><span data-stu-id="1901b-293">It verifies that the storage console is accessible.</span></span>
- <span data-ttu-id="1901b-294">It creates a test, or dummy, snapshot for each volume by HANA instance.</span><span class="sxs-lookup"><span data-stu-id="1901b-294">It creates a test, or dummy, snapshot for each volume by HANA instance.</span></span>

<span data-ttu-id="1901b-295">For this reason, the HANA instance is included as an argument.</span><span class="sxs-lookup"><span data-stu-id="1901b-295">For this reason, the HANA instance is included as an argument.</span></span> <span data-ttu-id="1901b-296">Again, it is not possible to provide error checking for the storage connection, but the script provides helpful hints if the execution fails.</span><span class="sxs-lookup"><span data-stu-id="1901b-296">Again, it is not possible to provide error checking for the storage connection, but the script provides helpful hints if the execution fails.</span></span>

<span data-ttu-id="1901b-297">The script is run as:</span><span class="sxs-lookup"><span data-stu-id="1901b-297">The script is run as:</span></span>
```
 ./testStorageSnapshotConnection.pl <hana instance>
```
<span data-ttu-id="1901b-298">Or it is run as:</span><span class="sxs-lookup"><span data-stu-id="1901b-298">Or it is run as:</span></span>
```
./testStorageSnapshotConnectionBW.pl <hana instance>
```
<span data-ttu-id="1901b-299">The script also displays a message that you are able to sign in appropriately to your deployed storage tenant, which is organized around the logical unit numbers (LUNs) that are used by the server instances you own.</span><span class="sxs-lookup"><span data-stu-id="1901b-299">The script also displays a message that you are able to sign in appropriately to your deployed storage tenant, which is organized around the logical unit numbers (LUNs) that are used by the server instances you own.</span></span>

<span data-ttu-id="1901b-300">Before you execute the first storage snapshot-based backups, run the next scripts to make sure that the configuration is correct.</span><span class="sxs-lookup"><span data-stu-id="1901b-300">Before you execute the first storage snapshot-based backups, run the next scripts to make sure that the configuration is correct.</span></span>

<span data-ttu-id="1901b-301">After running these scripts, you can delete the snapshots by executing:</span><span class="sxs-lookup"><span data-stu-id="1901b-301">After running these scripts, you can delete the snapshots by executing:</span></span>
```
./removeTestStorageSnapshot.pl <hana instance>
```
<span data-ttu-id="1901b-302">Or</span><span class="sxs-lookup"><span data-stu-id="1901b-302">Or</span></span>
```
./removeTestStorageSnapshot.pl <hana instance>
```

### <a name="step-7-perform-on-demand-snapshots"></a><span data-ttu-id="1901b-303">Step 7: Perform on-demand snapshots</span><span class="sxs-lookup"><span data-stu-id="1901b-303">Step 7: Perform on-demand snapshots</span></span>

<span data-ttu-id="1901b-304">Perform on-demand snapshots (as well as schedule regular snapshots by using cron) as described here.</span><span class="sxs-lookup"><span data-stu-id="1901b-304">Perform on-demand snapshots (as well as schedule regular snapshots by using cron) as described here.</span></span>

<span data-ttu-id="1901b-305">For scale-up configurations, execute the following script:</span><span class="sxs-lookup"><span data-stu-id="1901b-305">For scale-up configurations, execute the following script:</span></span>
```
./azure_hana_backup.pl lhanad01 customer 20
```
<span data-ttu-id="1901b-306">For scale-out configurations, execute the following script:</span><span class="sxs-lookup"><span data-stu-id="1901b-306">For scale-out configurations, execute the following script:</span></span>
```
./azure_hana_backup_bw.pl lhanad01 customer 20
```
<span data-ttu-id="1901b-307">The scale-out script does some additional checking to make sure that all HANA servers can be accessed, and all HANA instances return appropriate status of the instance before proceeding with creating SAP HANA or storage snapshots.</span><span class="sxs-lookup"><span data-stu-id="1901b-307">The scale-out script does some additional checking to make sure that all HANA servers can be accessed, and all HANA instances return appropriate status of the instance before proceeding with creating SAP HANA or storage snapshots.</span></span>

<span data-ttu-id="1901b-308">The following arguments are required:</span><span class="sxs-lookup"><span data-stu-id="1901b-308">The following arguments are required:</span></span>

- <span data-ttu-id="1901b-309">The HANA instance requiring backup.</span><span class="sxs-lookup"><span data-stu-id="1901b-309">The HANA instance requiring backup.</span></span>
- <span data-ttu-id="1901b-310">The snapshot prefix for the storage snapshot.</span><span class="sxs-lookup"><span data-stu-id="1901b-310">The snapshot prefix for the storage snapshot.</span></span>
- <span data-ttu-id="1901b-311">The number of snapshots to be kept for the specific prefix.</span><span class="sxs-lookup"><span data-stu-id="1901b-311">The number of snapshots to be kept for the specific prefix.</span></span>

```
./azure_hana_backup.pl lhanad01 customer 20
```

<span data-ttu-id="1901b-312">The execution of the script creates the storage snapshot in these three distinct phases:</span><span class="sxs-lookup"><span data-stu-id="1901b-312">The execution of the script creates the storage snapshot in these three distinct phases:</span></span>

- <span data-ttu-id="1901b-313">Execute a HANA snapshot.</span><span class="sxs-lookup"><span data-stu-id="1901b-313">Execute a HANA snapshot.</span></span>
- <span data-ttu-id="1901b-314">Execute a storage snapshot.</span><span class="sxs-lookup"><span data-stu-id="1901b-314">Execute a storage snapshot.</span></span>
- <span data-ttu-id="1901b-315">Remove the HANA snapshot.</span><span class="sxs-lookup"><span data-stu-id="1901b-315">Remove the HANA snapshot.</span></span>

<span data-ttu-id="1901b-316">Execute the script by calling it from the HDB executable folder that it was copied to.</span><span class="sxs-lookup"><span data-stu-id="1901b-316">Execute the script by calling it from the HDB executable folder that it was copied to.</span></span> <span data-ttu-id="1901b-317">It backs up at least the following volumes, but it also backs up any volume that has the explicit SAP HANA instance name in the volume name.</span><span class="sxs-lookup"><span data-stu-id="1901b-317">It backs up at least the following volumes, but it also backs up any volume that has the explicit SAP HANA instance name in the volume name.</span></span>
```
hana_data_<hana instance>_prod_t020_vol
hana_log_<hana instance>_prod_t020_vol
hana_log_backup_<hana instance>_prod_t020_vol
hana_shared_<hana instance>_prod_t020_vol
```
<span data-ttu-id="1901b-318">The retention period is strictly administered, with the number of snapshots submitted as a parameter when you execute the script (such as 20, shown previously).</span><span class="sxs-lookup"><span data-stu-id="1901b-318">The retention period is strictly administered, with the number of snapshots submitted as a parameter when you execute the script (such as 20, shown previously).</span></span> <span data-ttu-id="1901b-319">So the amount of time is a function of the period of execution and the number of snapshots in the call of the script.</span><span class="sxs-lookup"><span data-stu-id="1901b-319">So the amount of time is a function of the period of execution and the number of snapshots in the call of the script.</span></span> <span data-ttu-id="1901b-320">If the number of snapshots that are kept exceeds the number that are named as a parameter in the call of the script, the oldest storage snapshot of this label (in our previous case, _custom_) is deleted before a new snapshot is executed.</span><span class="sxs-lookup"><span data-stu-id="1901b-320">If the number of snapshots that are kept exceeds the number that are named as a parameter in the call of the script, the oldest storage snapshot of this label (in our previous case, _custom_) is deleted before a new snapshot is executed.</span></span> <span data-ttu-id="1901b-321">This means the number you give as the last parameter of the call is the number you can use to control the number of snapshots.</span><span class="sxs-lookup"><span data-stu-id="1901b-321">This means the number you give as the last parameter of the call is the number you can use to control the number of snapshots.</span></span>

>[!NOTE]
><span data-ttu-id="1901b-322">As soon as you change the label, the counting starts again.</span><span class="sxs-lookup"><span data-stu-id="1901b-322">As soon as you change the label, the counting starts again.</span></span>

<span data-ttu-id="1901b-323">You need to include the HANA instance name that's provided by SAP HANA on Azure Service Management as an argument if they are creating snapshots in multi-node environments.</span><span class="sxs-lookup"><span data-stu-id="1901b-323">You need to include the HANA instance name that's provided by SAP HANA on Azure Service Management as an argument if they are creating snapshots in multi-node environments.</span></span> <span data-ttu-id="1901b-324">In single-node environments, the name of the SAP HANA on Azure (large instances) unit is sufficient, but the HANA instance name is still recommended.</span><span class="sxs-lookup"><span data-stu-id="1901b-324">In single-node environments, the name of the SAP HANA on Azure (large instances) unit is sufficient, but the HANA instance name is still recommended.</span></span>

<span data-ttu-id="1901b-325">Additionally, you can back up boot volumes\LUNs by using the same script.</span><span class="sxs-lookup"><span data-stu-id="1901b-325">Additionally, you can back up boot volumes\LUNs by using the same script.</span></span> <span data-ttu-id="1901b-326">You must back up your boot volume at least once when you first run HANA, although we recommend a weekly or nightly backup schedule for booting in cron.</span><span class="sxs-lookup"><span data-stu-id="1901b-326">You must back up your boot volume at least once when you first run HANA, although we recommend a weekly or nightly backup schedule for booting in cron.</span></span> <span data-ttu-id="1901b-327">Rather than add an SAP HANA instance name, insert _boot_ as the argument into the script as follows:</span><span class="sxs-lookup"><span data-stu-id="1901b-327">Rather than add an SAP HANA instance name, insert _boot_ as the argument into the script as follows:</span></span>
```
./azure_hana_backup boot customer 20
```
<span data-ttu-id="1901b-328">The same retention policy is afforded to the boot volume as well.</span><span class="sxs-lookup"><span data-stu-id="1901b-328">The same retention policy is afforded to the boot volume as well.</span></span> <span data-ttu-id="1901b-329">Use on-demand snapshots, as described previously, for special cases only, such as during an SAP enhancement package (EHP) upgrade, or when you need to create a distinct storage snapshot.</span><span class="sxs-lookup"><span data-stu-id="1901b-329">Use on-demand snapshots, as described previously, for special cases only, such as during an SAP enhancement package (EHP) upgrade, or when you need to create a distinct storage snapshot.</span></span>

<span data-ttu-id="1901b-330">We encourage you to perform scheduled storage snapshots using cron, and we recommend that you use the same script for all backups and disaster-recovery needs (modifying the script inputs to match the various requested backup times).</span><span class="sxs-lookup"><span data-stu-id="1901b-330">We encourage you to perform scheduled storage snapshots using cron, and we recommend that you use the same script for all backups and disaster-recovery needs (modifying the script inputs to match the various requested backup times).</span></span> <span data-ttu-id="1901b-331">These are all scheduled differently in cron depending on their execution time: hourly, 12-hour, daily, or weekly.</span><span class="sxs-lookup"><span data-stu-id="1901b-331">These are all scheduled differently in cron depending on their execution time: hourly, 12-hour, daily, or weekly.</span></span> <span data-ttu-id="1901b-332">The cron schedule is designed to create storage snapshots that match the previously discussed retention labeling for long-term off-site backup.</span><span class="sxs-lookup"><span data-stu-id="1901b-332">The cron schedule is designed to create storage snapshots that match the previously discussed retention labeling for long-term off-site backup.</span></span> <span data-ttu-id="1901b-333">The script includes commands to back up all production volumes, depending on their requested frequency (data and log files are backed up hourly, whereas the boot volume is backed up daily).</span><span class="sxs-lookup"><span data-stu-id="1901b-333">The script includes commands to back up all production volumes, depending on their requested frequency (data and log files are backed up hourly, whereas the boot volume is backed up daily).</span></span>

<span data-ttu-id="1901b-334">The entries in the following cron script run every hour at the tenth minute, every 12 hours at the tenth minute, and daily at the tenth minute.</span><span class="sxs-lookup"><span data-stu-id="1901b-334">The entries in the following cron script run every hour at the tenth minute, every 12 hours at the tenth minute, and daily at the tenth minute.</span></span> <span data-ttu-id="1901b-335">The cron jobs are created in such a way that only one SAP HANA storage snapshot takes place during any particular hour, so that the hourly and daily backups do not occur at the same time (12:10 AM).</span><span class="sxs-lookup"><span data-stu-id="1901b-335">The cron jobs are created in such a way that only one SAP HANA storage snapshot takes place during any particular hour, so that the hourly and daily backups do not occur at the same time (12:10 AM).</span></span> <span data-ttu-id="1901b-336">To help optimize your snapshot creation and replication, SAP HANA on Azure Service Management provides the recommended time for you to run your backups.</span><span class="sxs-lookup"><span data-stu-id="1901b-336">To help optimize your snapshot creation and replication, SAP HANA on Azure Service Management provides the recommended time for you to run your backups.</span></span>

<span data-ttu-id="1901b-337">The default cron scheduling in /etc/crontab is as follows:</span><span class="sxs-lookup"><span data-stu-id="1901b-337">The default cron scheduling in /etc/crontab is as follows:</span></span>
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 14
```
<span data-ttu-id="1901b-338">In the previous cron instructions, the HANA volumes (without boot volume) get an hourly snapshot with the label.</span><span class="sxs-lookup"><span data-stu-id="1901b-338">In the previous cron instructions, the HANA volumes (without boot volume) get an hourly snapshot with the label.</span></span> <span data-ttu-id="1901b-339">Of these snapshots, 66 are retained.</span><span class="sxs-lookup"><span data-stu-id="1901b-339">Of these snapshots, 66 are retained.</span></span> <span data-ttu-id="1901b-340">Additionally, 14 snapshots with the 12-hour label are retained.</span><span class="sxs-lookup"><span data-stu-id="1901b-340">Additionally, 14 snapshots with the 12-hour label are retained.</span></span> <span data-ttu-id="1901b-341">You potentially get hourly snapshots for three days, plus 12-hour snapshots for another four days, which gives you an entire week of snapshots.</span><span class="sxs-lookup"><span data-stu-id="1901b-341">You potentially get hourly snapshots for three days, plus 12-hour snapshots for another four days, which gives you an entire week of snapshots.</span></span>

<span data-ttu-id="1901b-342">Scheduling within cron can be tricky, because only one script should be executed at any particular time, unless the scripts are staggered by several minutes.</span><span class="sxs-lookup"><span data-stu-id="1901b-342">Scheduling within cron can be tricky, because only one script should be executed at any particular time, unless the scripts are staggered by several minutes.</span></span> <span data-ttu-id="1901b-343">If you want daily backups for long-term retention, either a daily snapshot is kept along with a 12-hour snapshot (with a retention count of seven each), or the hourly snapshot is staggered to take place 10 minutes later.</span><span class="sxs-lookup"><span data-stu-id="1901b-343">If you want daily backups for long-term retention, either a daily snapshot is kept along with a 12-hour snapshot (with a retention count of seven each), or the hourly snapshot is staggered to take place 10 minutes later.</span></span> <span data-ttu-id="1901b-344">Only one daily snapshot is kept in the production volume.</span><span class="sxs-lookup"><span data-stu-id="1901b-344">Only one daily snapshot is kept in the production volume.</span></span>
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 7
10 0 * * * ./azure_hana_backup.pl lhanad01 daily 7
```
<span data-ttu-id="1901b-345">The frequencies listed here are only examples.</span><span class="sxs-lookup"><span data-stu-id="1901b-345">The frequencies listed here are only examples.</span></span> <span data-ttu-id="1901b-346">To derive your optimum number of snapshots, use the following criteria:</span><span class="sxs-lookup"><span data-stu-id="1901b-346">To derive your optimum number of snapshots, use the following criteria:</span></span>

- <span data-ttu-id="1901b-347">Requirements in recovery time objective for point-in-time recovery.</span><span class="sxs-lookup"><span data-stu-id="1901b-347">Requirements in recovery time objective for point-in-time recovery.</span></span>
- <span data-ttu-id="1901b-348">Space usage.</span><span class="sxs-lookup"><span data-stu-id="1901b-348">Space usage.</span></span>
- <span data-ttu-id="1901b-349">Requirements in recovery point objective and recovery time objective for potential disaster recovery.</span><span class="sxs-lookup"><span data-stu-id="1901b-349">Requirements in recovery point objective and recovery time objective for potential disaster recovery.</span></span>
- <span data-ttu-id="1901b-350">Eventual execution of HANA full database backups against disks.</span><span class="sxs-lookup"><span data-stu-id="1901b-350">Eventual execution of HANA full database backups against disks.</span></span> <span data-ttu-id="1901b-351">Whenever a full database backup against disks, or _backint_ interface, is performed, the execution of storage snapshots fails.</span><span class="sxs-lookup"><span data-stu-id="1901b-351">Whenever a full database backup against disks, or _backint_ interface, is performed, the execution of storage snapshots fails.</span></span> <span data-ttu-id="1901b-352">If you plan to execute full database backups on top of storage snapshots, make sure that the execution of storage snapshots is disabled during this time.</span><span class="sxs-lookup"><span data-stu-id="1901b-352">If you plan to execute full database backups on top of storage snapshots, make sure that the execution of storage snapshots is disabled during this time.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="1901b-353">The use of storage snapshots for SAP HANA backups is valid only when the snapshots are performed in conjunction with SAP HANA log backups.</span><span class="sxs-lookup"><span data-stu-id="1901b-353">The use of storage snapshots for SAP HANA backups is valid only when the snapshots are performed in conjunction with SAP HANA log backups.</span></span> <span data-ttu-id="1901b-354">These log backups need to be able to cover the time periods between the storage snapshots.</span><span class="sxs-lookup"><span data-stu-id="1901b-354">These log backups need to be able to cover the time periods between the storage snapshots.</span></span> <span data-ttu-id="1901b-355">If you've set a commitment to users of a point-in-time recovery of 30 days, you need the following:</span><span class="sxs-lookup"><span data-stu-id="1901b-355">If you've set a commitment to users of a point-in-time recovery of 30 days, you need the following:</span></span>

- <span data-ttu-id="1901b-356">Ability to access a storage snapshot that is 30 days old.</span><span class="sxs-lookup"><span data-stu-id="1901b-356">Ability to access a storage snapshot that is 30 days old.</span></span>
- <span data-ttu-id="1901b-357">Contiguous log backups over the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="1901b-357">Contiguous log backups over the last 30 days.</span></span>

<span data-ttu-id="1901b-358">In the range of log backups, create a snapshot of the backup log volume as well.</span><span class="sxs-lookup"><span data-stu-id="1901b-358">In the range of log backups, create a snapshot of the backup log volume as well.</span></span> <span data-ttu-id="1901b-359">However, be sure to perform regular log backups so that you can:</span><span class="sxs-lookup"><span data-stu-id="1901b-359">However, be sure to perform regular log backups so that you can:</span></span>

- <span data-ttu-id="1901b-360">Have the contiguous log backups needed to perform point-in-time recoveries.</span><span class="sxs-lookup"><span data-stu-id="1901b-360">Have the contiguous log backups needed to perform point-in-time recoveries.</span></span>
- <span data-ttu-id="1901b-361">Prevent the SAP HANA log volume from running out of space.</span><span class="sxs-lookup"><span data-stu-id="1901b-361">Prevent the SAP HANA log volume from running out of space.</span></span>

<span data-ttu-id="1901b-362">One of the last steps is to schedule SAP HANA backup logs in SAP HANA Studio.</span><span class="sxs-lookup"><span data-stu-id="1901b-362">One of the last steps is to schedule SAP HANA backup logs in SAP HANA Studio.</span></span> <span data-ttu-id="1901b-363">The SAP HANA backup log target destination is the specially created hana/log\_backups volume with the mount point of /hana/log/backups.</span><span class="sxs-lookup"><span data-stu-id="1901b-363">The SAP HANA backup log target destination is the specially created hana/log\_backups volume with the mount point of /hana/log/backups.</span></span>

![Schedule SAP HANA backup logs in SAP HANA Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/hana-overview-high-availability-disaster-recovery/image5-schedule-backup.png)

<span data-ttu-id="1901b-365">You can choose backups that are more frequent than every 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="1901b-365">You can choose backups that are more frequent than every 15 minutes.</span></span> <span data-ttu-id="1901b-366">Some users even perform log backups every minute, although we do not recommend going _over_ 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="1901b-366">Some users even perform log backups every minute, although we do not recommend going _over_ 15 minutes.</span></span>

<span data-ttu-id="1901b-367">The final step is to perform a file-based backup (after the initial installation of SAP HANA) to create a single backup entry that must exist within the backup catalog.</span><span class="sxs-lookup"><span data-stu-id="1901b-367">The final step is to perform a file-based backup (after the initial installation of SAP HANA) to create a single backup entry that must exist within the backup catalog.</span></span> <span data-ttu-id="1901b-368">Otherwise SAP HANA cannot initiate your specified log backups.</span><span class="sxs-lookup"><span data-stu-id="1901b-368">Otherwise SAP HANA cannot initiate your specified log backups.</span></span>

![Make a file-based backup to create a single backup entry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/hana-overview-high-availability-disaster-recovery/image6-make-backup.png)

### <a name="monitoring-the-number-and-size-of-snapshots-on-the-disk-volume"></a><span data-ttu-id="1901b-370">Monitoring the number and size of snapshots on the disk volume</span><span class="sxs-lookup"><span data-stu-id="1901b-370">Monitoring the number and size of snapshots on the disk volume</span></span>

<span data-ttu-id="1901b-371">On a particular storage volume, you can monitor the number of snapshots and the storage consumption of snapshots.</span><span class="sxs-lookup"><span data-stu-id="1901b-371">On a particular storage volume, you can monitor the number of snapshots and the storage consumption of snapshots.</span></span> <span data-ttu-id="1901b-372">The `ls` command doesn't show the snapshot directory or files.</span><span class="sxs-lookup"><span data-stu-id="1901b-372">The `ls` command doesn't show the snapshot directory or files.</span></span> <span data-ttu-id="1901b-373">However, the Linux OS command `du` does, with the following commands:</span><span class="sxs-lookup"><span data-stu-id="1901b-373">However, the Linux OS command `du` does, with the following commands:</span></span>

- <span data-ttu-id="1901b-374">`du –sh .snapshot` provides a total of all snapshots within the snapshot directory.</span><span class="sxs-lookup"><span data-stu-id="1901b-374">`du –sh .snapshot` provides a total of all snapshots within the snapshot directory.</span></span>
- <span data-ttu-id="1901b-375">`du –sh --max-depth=1` lists all snapshots that are saved in the .snapshot folder and the size of each snapshot.</span><span class="sxs-lookup"><span data-stu-id="1901b-375">`du –sh --max-depth=1` lists all snapshots that are saved in the .snapshot folder and the size of each snapshot.</span></span>
- <span data-ttu-id="1901b-376">`du –hc` provides the total size used by all snapshots.</span><span class="sxs-lookup"><span data-stu-id="1901b-376">`du –hc` provides the total size used by all snapshots.</span></span>

<span data-ttu-id="1901b-377">Use these commands to make sure that the snapshots that are taken and stored are not consuming all the storage on the volumes.</span><span class="sxs-lookup"><span data-stu-id="1901b-377">Use these commands to make sure that the snapshots that are taken and stored are not consuming all the storage on the volumes.</span></span>

### <a name="reducing-the-number-of-snapshots-on-a-server"></a><span data-ttu-id="1901b-378">Reducing the number of snapshots on a server</span><span class="sxs-lookup"><span data-stu-id="1901b-378">Reducing the number of snapshots on a server</span></span>

<span data-ttu-id="1901b-379">As explained earlier, you can reduce the number of certain labels of snapshots that you store.</span><span class="sxs-lookup"><span data-stu-id="1901b-379">As explained earlier, you can reduce the number of certain labels of snapshots that you store.</span></span> <span data-ttu-id="1901b-380">The last two parameters of the command to initiate a snapshot are a label and the number of snapshots you want to retain.</span><span class="sxs-lookup"><span data-stu-id="1901b-380">The last two parameters of the command to initiate a snapshot are a label and the number of snapshots you want to retain.</span></span>
```
./azure_hana_backup.pl lhanad01 customer 20
```
<span data-ttu-id="1901b-381">In the previous example, the snapshot label is _customer_ and the number of snapshots with this label to be retained is _20_.</span><span class="sxs-lookup"><span data-stu-id="1901b-381">In the previous example, the snapshot label is _customer_ and the number of snapshots with this label to be retained is _20_.</span></span> <span data-ttu-id="1901b-382">As you respond to disk space consumption, you might want to reduce the number of stored snapshots.</span><span class="sxs-lookup"><span data-stu-id="1901b-382">As you respond to disk space consumption, you might want to reduce the number of stored snapshots.</span></span> <span data-ttu-id="1901b-383">The easy way to reduce the number of snapshots is to run the script with the last parameter set to 5:</span><span class="sxs-lookup"><span data-stu-id="1901b-383">The easy way to reduce the number of snapshots is to run the script with the last parameter set to 5:</span></span>
```
./azure_hana_backup.pl lhanad01 customer 5
```
<span data-ttu-id="1901b-384">As a result of running the script with this setting, the number of snapshots, including the new storage snapshot, is _5_.</span><span class="sxs-lookup"><span data-stu-id="1901b-384">As a result of running the script with this setting, the number of snapshots, including the new storage snapshot, is _5_.</span></span>

 >[!NOTE]
 > <span data-ttu-id="1901b-385">This script reduces the number of snapshots only if the most recent previous snapshot is more than one hour old.</span><span class="sxs-lookup"><span data-stu-id="1901b-385">This script reduces the number of snapshots only if the most recent previous snapshot is more than one hour old.</span></span> <span data-ttu-id="1901b-386">The script does not delete snapshots that are less than one hour old.</span><span class="sxs-lookup"><span data-stu-id="1901b-386">The script does not delete snapshots that are less than one hour old.</span></span>

<span data-ttu-id="1901b-387">These restrictions are related to the optional disaster-recovery functionality offered.</span><span class="sxs-lookup"><span data-stu-id="1901b-387">These restrictions are related to the optional disaster-recovery functionality offered.</span></span>

<span data-ttu-id="1901b-388">If you no longer want to maintain a set of snapshots with that prefix, you can execute the script with _0_ as the retention number to remove all snapshots matching that prefix.</span><span class="sxs-lookup"><span data-stu-id="1901b-388">If you no longer want to maintain a set of snapshots with that prefix, you can execute the script with _0_ as the retention number to remove all snapshots matching that prefix.</span></span> <span data-ttu-id="1901b-389">However, removing all snapshots can affect the capabilities of disaster recovery.</span><span class="sxs-lookup"><span data-stu-id="1901b-389">However, removing all snapshots can affect the capabilities of disaster recovery.</span></span>

### <a name="recovering-to-the-most-recent-hana-snapshot"></a><span data-ttu-id="1901b-390">Recovering to the most recent HANA snapshot</span><span class="sxs-lookup"><span data-stu-id="1901b-390">Recovering to the most recent HANA snapshot</span></span>

<span data-ttu-id="1901b-391">In the event that you experience a production-down scenario, the process of recovering from a storage snapshot can be initiated as a customer incident with SAP HANA on Azure Service Management.</span><span class="sxs-lookup"><span data-stu-id="1901b-391">In the event that you experience a production-down scenario, the process of recovering from a storage snapshot can be initiated as a customer incident with SAP HANA on Azure Service Management.</span></span> <span data-ttu-id="1901b-392">Such an unexpected scenario might be a high-urgency matter if data was deleted in a production system and the only way to retrieve the data is to restore the production database.</span><span class="sxs-lookup"><span data-stu-id="1901b-392">Such an unexpected scenario might be a high-urgency matter if data was deleted in a production system and the only way to retrieve the data is to restore the production database.</span></span>

<span data-ttu-id="1901b-393">On the other hand, a point-in-time recovery could be low urgency and planned for days in advance.</span><span class="sxs-lookup"><span data-stu-id="1901b-393">On the other hand, a point-in-time recovery could be low urgency and planned for days in advance.</span></span> <span data-ttu-id="1901b-394">You can plan this recovery with SAP HANA on Azure Service Management instead of raising a high-priority issue.</span><span class="sxs-lookup"><span data-stu-id="1901b-394">You can plan this recovery with SAP HANA on Azure Service Management instead of raising a high-priority issue.</span></span> <span data-ttu-id="1901b-395">For example, you might be planning to try an upgrade of the SAP software by applying a new enhancement package, and you then need to revert back to a snapshot that represents the state before the EHP upgrade.</span><span class="sxs-lookup"><span data-stu-id="1901b-395">For example, you might be planning to try an upgrade of the SAP software by applying a new enhancement package, and you then need to revert back to a snapshot that represents the state before the EHP upgrade.</span></span>

<span data-ttu-id="1901b-396">Before you issue the request, you need to do some preparation.</span><span class="sxs-lookup"><span data-stu-id="1901b-396">Before you issue the request, you need to do some preparation.</span></span> <span data-ttu-id="1901b-397">SAP HANA on Azure Service Management team can then handle the request and provide the restored volumes.</span><span class="sxs-lookup"><span data-stu-id="1901b-397">SAP HANA on Azure Service Management team can then handle the request and provide the restored volumes.</span></span> <span data-ttu-id="1901b-398">Afterward, it is up to you to restore the HANA database based on the snapshots.</span><span class="sxs-lookup"><span data-stu-id="1901b-398">Afterward, it is up to you to restore the HANA database based on the snapshots.</span></span> <span data-ttu-id="1901b-399">Here is how to prepare for the request:</span><span class="sxs-lookup"><span data-stu-id="1901b-399">Here is how to prepare for the request:</span></span>

>[!NOTE]
><span data-ttu-id="1901b-400">Your user interface might vary from the following screenshots, depending on the SAP HANA release you are using.</span><span class="sxs-lookup"><span data-stu-id="1901b-400">Your user interface might vary from the following screenshots, depending on the SAP HANA release you are using.</span></span>

1. <span data-ttu-id="1901b-401">Decide which snapshot to restore.</span><span class="sxs-lookup"><span data-stu-id="1901b-401">Decide which snapshot to restore.</span></span> <span data-ttu-id="1901b-402">Only the hana/data volume would be restored unless you are instructed otherwise.</span><span class="sxs-lookup"><span data-stu-id="1901b-402">Only the hana/data volume would be restored unless you are instructed otherwise.</span></span>

2. <span data-ttu-id="1901b-403">Shut down the HANA instance.</span><span class="sxs-lookup"><span data-stu-id="1901b-403">Shut down the HANA instance.</span></span>

 ![Shut down the HANA instance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/hana-overview-high-availability-disaster-recovery/image7-shutdown-hana.png)

3. <span data-ttu-id="1901b-405">Unmount the data volumes on each HANA database node.</span><span class="sxs-lookup"><span data-stu-id="1901b-405">Unmount the data volumes on each HANA database node.</span></span> <span data-ttu-id="1901b-406">The restoration of the snapshot fails if the data volumes are not unmounted.</span><span class="sxs-lookup"><span data-stu-id="1901b-406">The restoration of the snapshot fails if the data volumes are not unmounted.</span></span>

 ![Unmount the data volumes on each HANA database node](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/hana-overview-high-availability-disaster-recovery/image8-unmount-data-volumes.png)

4. <span data-ttu-id="1901b-408">Open an Azure support request to instruct the restoration of a specific snapshot.</span><span class="sxs-lookup"><span data-stu-id="1901b-408">Open an Azure support request to instruct the restoration of a specific snapshot.</span></span>

 - <span data-ttu-id="1901b-409">During the restoration: SAP HANA on Azure Service Management might ask you to attend a conference call to ensure that no data is getting lost.</span><span class="sxs-lookup"><span data-stu-id="1901b-409">During the restoration: SAP HANA on Azure Service Management might ask you to attend a conference call to ensure that no data is getting lost.</span></span>

 - <span data-ttu-id="1901b-410">After the restoration: SAP HANA on Azure Service Management notifies you when the storage snapshot has been restored.</span><span class="sxs-lookup"><span data-stu-id="1901b-410">After the restoration: SAP HANA on Azure Service Management notifies you when the storage snapshot has been restored.</span></span>

5. <span data-ttu-id="1901b-411">After the restoration process is complete, remount all data volumes.</span><span class="sxs-lookup"><span data-stu-id="1901b-411">After the restoration process is complete, remount all data volumes.</span></span>

 ![Remount all data volumes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/hana-overview-high-availability-disaster-recovery/image9-remount-data-volumes.png)

6. <span data-ttu-id="1901b-413">Select recovery options within SAP HANA Studio, if they do not automatically come up when you reconnect to HANA DB through SAP HANA Studio.</span><span class="sxs-lookup"><span data-stu-id="1901b-413">Select recovery options within SAP HANA Studio, if they do not automatically come up when you reconnect to HANA DB through SAP HANA Studio.</span></span> <span data-ttu-id="1901b-414">The following example shows a restoration to the last HANA snapshot.</span><span class="sxs-lookup"><span data-stu-id="1901b-414">The following example shows a restoration to the last HANA snapshot.</span></span> <span data-ttu-id="1901b-415">A storage snapshot embeds one HANA snapshot, and if you are restoring to the most recent storage snapshot, it should be the most recent HANA snapshot.</span><span class="sxs-lookup"><span data-stu-id="1901b-415">A storage snapshot embeds one HANA snapshot, and if you are restoring to the most recent storage snapshot, it should be the most recent HANA snapshot.</span></span> <span data-ttu-id="1901b-416">(If you are restoring to older storage snapshots, you need to locate the HANA snapshot based on the time the storage snapshot was taken.)</span><span class="sxs-lookup"><span data-stu-id="1901b-416">(If you are restoring to older storage snapshots, you need to locate the HANA snapshot based on the time the storage snapshot was taken.)</span></span>

 ![Select recover options within SAP HANA Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/hana-overview-high-availability-disaster-recovery/image10-recover-options-a.png)

7. <span data-ttu-id="1901b-418">Select **Recover the database to a specific data backup or storage snapshot**.</span><span class="sxs-lookup"><span data-stu-id="1901b-418">Select **Recover the database to a specific data backup or storage snapshot**.</span></span>

 ![The "Specify Recovery Type" window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/hana-overview-high-availability-disaster-recovery/image11-recover-options-b.png)

8. <span data-ttu-id="1901b-420">Select **Specify backup without catalog**.</span><span class="sxs-lookup"><span data-stu-id="1901b-420">Select **Specify backup without catalog**.</span></span>

 ![The "Specify Backup Location" window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/hana-overview-high-availability-disaster-recovery/image12-recover-options-c.png)

9. <span data-ttu-id="1901b-422">In the **Destination Type** list, select **Snapshot**.</span><span class="sxs-lookup"><span data-stu-id="1901b-422">In the **Destination Type** list, select **Snapshot**.</span></span>

 ![The "Specify the Backup to Recover" window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/hana-overview-high-availability-disaster-recovery/image13-recover-options-d.png)

10. <span data-ttu-id="1901b-424">Click **Finish** to start the recovery process.</span><span class="sxs-lookup"><span data-stu-id="1901b-424">Click **Finish** to start the recovery process.</span></span>

 ![Click "Finish" to start the recovery process](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/hana-overview-high-availability-disaster-recovery/image14-recover-options-e.png)

11. <span data-ttu-id="1901b-426">The HANA database is restored and recovered to the HANA snapshot that's included in the storage snapshot.</span><span class="sxs-lookup"><span data-stu-id="1901b-426">The HANA database is restored and recovered to the HANA snapshot that's included in the storage snapshot.</span></span>

 ![HANA database is restored and recovered to the HANA snapshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/hana-overview-high-availability-disaster-recovery/image15-recover-options-f.png)

### <a name="recovering-to-the-most-recent-state"></a><span data-ttu-id="1901b-428">Recovering to the most recent state</span><span class="sxs-lookup"><span data-stu-id="1901b-428">Recovering to the most recent state</span></span>

<span data-ttu-id="1901b-429">The following process restores the HANA snapshot that is included in the storage snapshot.</span><span class="sxs-lookup"><span data-stu-id="1901b-429">The following process restores the HANA snapshot that is included in the storage snapshot.</span></span> <span data-ttu-id="1901b-430">It then restores the transaction log backups to the most recent state of the database before restoring the storage snapshot.</span><span class="sxs-lookup"><span data-stu-id="1901b-430">It then restores the transaction log backups to the most recent state of the database before restoring the storage snapshot.</span></span>

>[!IMPORTANT]
><span data-ttu-id="1901b-431">Before you proceed, make sure that you have a complete and contiguous chain of transaction log backups.</span><span class="sxs-lookup"><span data-stu-id="1901b-431">Before you proceed, make sure that you have a complete and contiguous chain of transaction log backups.</span></span> <span data-ttu-id="1901b-432">Without these backups, you cannot restore the current state of the database.</span><span class="sxs-lookup"><span data-stu-id="1901b-432">Without these backups, you cannot restore the current state of the database.</span></span>

1. <span data-ttu-id="1901b-433">Complete steps 1-6 of the preceding procedure in "Recovering to the most recent HANA snapshot."</span><span class="sxs-lookup"><span data-stu-id="1901b-433">Complete steps 1-6 of the preceding procedure in "Recovering to the most recent HANA snapshot."</span></span>

2. <span data-ttu-id="1901b-434">Select **Recover the database to its most recent state**.</span><span class="sxs-lookup"><span data-stu-id="1901b-434">Select **Recover the database to its most recent state**.</span></span>

 ![Select "Recover the database to its most recent state"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/hana-overview-high-availability-disaster-recovery/image16-recover-database-a.png)

3. <span data-ttu-id="1901b-436">Specify the location of the most recent HANA log backups.</span><span class="sxs-lookup"><span data-stu-id="1901b-436">Specify the location of the most recent HANA log backups.</span></span> <span data-ttu-id="1901b-437">The location needs to contain all HANA transaction log backups from the HANA snapshot to the most recent state.</span><span class="sxs-lookup"><span data-stu-id="1901b-437">The location needs to contain all HANA transaction log backups from the HANA snapshot to the most recent state.</span></span>

 ![Specify the location of the most recent HANA log backups](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/hana-overview-high-availability-disaster-recovery/image17-recover-database-b.png)

4. <span data-ttu-id="1901b-439">Select a backup as a base from which to recover the database.</span><span class="sxs-lookup"><span data-stu-id="1901b-439">Select a backup as a base from which to recover the database.</span></span> <span data-ttu-id="1901b-440">In our example, this is the HANA snapshot that was included in the storage snapshot.</span><span class="sxs-lookup"><span data-stu-id="1901b-440">In our example, this is the HANA snapshot that was included in the storage snapshot.</span></span> <span data-ttu-id="1901b-441">(Only one snapshot is listed in the following screenshot.)</span><span class="sxs-lookup"><span data-stu-id="1901b-441">(Only one snapshot is listed in the following screenshot.)</span></span>

 ![Select a backup as a base from which to recover the database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/hana-overview-high-availability-disaster-recovery/image18-recover-database-c.png)

5. <span data-ttu-id="1901b-443">Clear the **Use Delta Backups** check box if deltas do not exist between the time of the HANA snapshot and the most recent state.</span><span class="sxs-lookup"><span data-stu-id="1901b-443">Clear the **Use Delta Backups** check box if deltas do not exist between the time of the HANA snapshot and the most recent state.</span></span>

 ![Clear the "Use Delta Backups" check box if no deltas exist](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/hana-overview-high-availability-disaster-recovery/image19-recover-database-d.png)

6. <span data-ttu-id="1901b-445">On the summary screen, click **Finish** to start the restoration procedure.</span><span class="sxs-lookup"><span data-stu-id="1901b-445">On the summary screen, click **Finish** to start the restoration procedure.</span></span>

 ![Click "Finish" on the summary screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/hana-overview-high-availability-disaster-recovery/image20-recover-database-e.png)

### <a name="recovering-to-another-point-in-time"></a><span data-ttu-id="1901b-447">Recovering to another point in time</span><span class="sxs-lookup"><span data-stu-id="1901b-447">Recovering to another point in time</span></span>
<span data-ttu-id="1901b-448">To recover to a point in time between the HANA snapshot (included in the storage snapshot) and one that is later than the HANA snapshot point-in-time recovery, do the following:</span><span class="sxs-lookup"><span data-stu-id="1901b-448">To recover to a point in time between the HANA snapshot (included in the storage snapshot) and one that is later than the HANA snapshot point-in-time recovery, do the following:</span></span>

1. <span data-ttu-id="1901b-449">Make sure that you have all transaction log backups from the HANA snapshot to the time you want to recover.</span><span class="sxs-lookup"><span data-stu-id="1901b-449">Make sure that you have all transaction log backups from the HANA snapshot to the time you want to recover.</span></span>
2. <span data-ttu-id="1901b-450">Begin the procedure under "Recovering to the most recent state."</span><span class="sxs-lookup"><span data-stu-id="1901b-450">Begin the procedure under "Recovering to the most recent state."</span></span>
3. <span data-ttu-id="1901b-451">In step 2 of the procedure, in the **Specify Recovery Type** window, select **Recover the database to the following point in time**, specify the point in time, and then complete steps 3-6.</span><span class="sxs-lookup"><span data-stu-id="1901b-451">In step 2 of the procedure, in the **Specify Recovery Type** window, select **Recover the database to the following point in time**, specify the point in time, and then complete steps 3-6.</span></span>

## <a name="monitoring-the-execution-of-snapshots"></a><span data-ttu-id="1901b-452">Monitoring the execution of snapshots</span><span class="sxs-lookup"><span data-stu-id="1901b-452">Monitoring the execution of snapshots</span></span>

<span data-ttu-id="1901b-453">You need to monitor the execution of storage snapshots.</span><span class="sxs-lookup"><span data-stu-id="1901b-453">You need to monitor the execution of storage snapshots.</span></span> <span data-ttu-id="1901b-454">The script that executes a storage snapshot writes output to a file and then saves it to the same location as the Perl scripts.</span><span class="sxs-lookup"><span data-stu-id="1901b-454">The script that executes a storage snapshot writes output to a file and then saves it to the same location as the Perl scripts.</span></span> <span data-ttu-id="1901b-455">A separate file is written for each snapshot.</span><span class="sxs-lookup"><span data-stu-id="1901b-455">A separate file is written for each snapshot.</span></span> <span data-ttu-id="1901b-456">The output of each file clearly shows the various phases that the snapshot script executes:</span><span class="sxs-lookup"><span data-stu-id="1901b-456">The output of each file clearly shows the various phases that the snapshot script executes:</span></span>

- <span data-ttu-id="1901b-457">Finding the volumes that need to create a snapshot</span><span class="sxs-lookup"><span data-stu-id="1901b-457">Finding the volumes that need to create a snapshot</span></span>
- <span data-ttu-id="1901b-458">Finding the snapshots taken from these volumes</span><span class="sxs-lookup"><span data-stu-id="1901b-458">Finding the snapshots taken from these volumes</span></span>
- <span data-ttu-id="1901b-459">Deleting eventual existing snapshots to match the number of snapshots you specified</span><span class="sxs-lookup"><span data-stu-id="1901b-459">Deleting eventual existing snapshots to match the number of snapshots you specified</span></span>
- <span data-ttu-id="1901b-460">Creating a HANA snapshot</span><span class="sxs-lookup"><span data-stu-id="1901b-460">Creating a HANA snapshot</span></span>
- <span data-ttu-id="1901b-461">Creating the storage snapshot over the volumes</span><span class="sxs-lookup"><span data-stu-id="1901b-461">Creating the storage snapshot over the volumes</span></span>
- <span data-ttu-id="1901b-462">Deleting the HANA snapshot</span><span class="sxs-lookup"><span data-stu-id="1901b-462">Deleting the HANA snapshot</span></span>
- <span data-ttu-id="1901b-463">Renaming the most recent snapshot to **.0**</span><span class="sxs-lookup"><span data-stu-id="1901b-463">Renaming the most recent snapshot to **.0**</span></span>

<span data-ttu-id="1901b-464">The most important part of the script is this:</span><span class="sxs-lookup"><span data-stu-id="1901b-464">The most important part of the script is this:</span></span>
```
**********************Creating HANA snapshot**********************
Creating the HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data create snapshot"" ...
HANA snapshot created successfully.
**********************Creating Storage snapshot**********************
Taking snapshot hourly.recent for hana_data_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_backup_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_shared_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for sapmnt_lhanad01_t020_vol ...
Snapshot created successfully.
**********************Deleting HANA snapshot**********************
Deleting the HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data drop snapshot"" ...
HANA snapshot deletion successfully.
```
<span data-ttu-id="1901b-465">You can see from this sample how the script records the creation of the HANA snapshot.</span><span class="sxs-lookup"><span data-stu-id="1901b-465">You can see from this sample how the script records the creation of the HANA snapshot.</span></span> <span data-ttu-id="1901b-466">In the scale-out case, this process is initiated on the master node.</span><span class="sxs-lookup"><span data-stu-id="1901b-466">In the scale-out case, this process is initiated on the master node.</span></span> <span data-ttu-id="1901b-467">The master node initiates the synchronous creation of the snapshots on each of the worker nodes.</span><span class="sxs-lookup"><span data-stu-id="1901b-467">The master node initiates the synchronous creation of the snapshots on each of the worker nodes.</span></span> <span data-ttu-id="1901b-468">Then the storage snapshot is taken.</span><span class="sxs-lookup"><span data-stu-id="1901b-468">Then the storage snapshot is taken.</span></span> <span data-ttu-id="1901b-469">After the successful execution of the storage snapshots, the HANA snapshot is deleted.</span><span class="sxs-lookup"><span data-stu-id="1901b-469">After the successful execution of the storage snapshots, the HANA snapshot is deleted.</span></span>




















