---
title: Replicate apps with SQL Server and Azure Site Recovery | Microsoft Docs
description: This article describes how to replicate SQL Server using Azure Site Recovery of SQL Server disaster capabilities.
services: site-recovery
documentationcenter: ''
author: prateek9us
manager: gauravd
editor: ''
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: pratshar
ms.openlocfilehash: 3bb905f9eab89b4dc0147d01dc1cf87ce4dcb5d6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662426"
---
# <a name="protect-sql-server-using-sql-server-disaster-recovery-and-azure-site-recovery"></a><span data-ttu-id="cd0f1-103">Protect SQL Server using SQL Server disaster recovery and Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="cd0f1-103">Protect SQL Server using SQL Server disaster recovery and Azure Site Recovery</span></span>

<span data-ttu-id="cd0f1-104">This article describes how to protect the SQL Server back end of an application using a combination of SQL Server business continuity and disaster recovery (BCDR) technologies, and [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cd0f1-104">This article describes how to protect the SQL Server back end of an application using a combination of SQL Server business continuity and disaster recovery (BCDR) technologies, and [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="cd0f1-105">Before you start, make sure you understand SQL Server disaster recovery capabilities, including failover clustering, AlwaysOn availability groups, database mirroring, and log shipping.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-105">Before you start, make sure you understand SQL Server disaster recovery capabilities, including failover clustering, AlwaysOn availability groups, database mirroring, and log shipping.</span></span>


## <a name="sql-server-deployments"></a><span data-ttu-id="cd0f1-106">SQL Server deployments</span><span class="sxs-lookup"><span data-stu-id="cd0f1-106">SQL Server deployments</span></span>

<span data-ttu-id="cd0f1-107">Many workloads use SQL Server as a foundation, and it can be integrated with apps such as SharePoint, Dynamics, and SAP, to implement data services.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-107">Many workloads use SQL Server as a foundation, and it can be integrated with apps such as SharePoint, Dynamics, and SAP, to implement data services.</span></span>  <span data-ttu-id="cd0f1-108">SQL Server can be deployed in a number of ways:</span><span class="sxs-lookup"><span data-stu-id="cd0f1-108">SQL Server can be deployed in a number of ways:</span></span>

* <span data-ttu-id="cd0f1-109">**Standalone SQL Server**: SQL Server and all databases are hosted on a single machine (physical or a virtual).</span><span class="sxs-lookup"><span data-stu-id="cd0f1-109">**Standalone SQL Server**: SQL Server and all databases are hosted on a single machine (physical or a virtual).</span></span> <span data-ttu-id="cd0f1-110">When virtualized, host clustering is used for local high availability.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-110">When virtualized, host clustering is used for local high availability.</span></span> <span data-ttu-id="cd0f1-111">Guest-level high availability isn't implemented.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-111">Guest-level high availability isn't implemented.</span></span>
* <span data-ttu-id="cd0f1-112">**SQL Server Failover Clustering Instances (AlwaysOn FCI)**: Two or more nodes running SQL Server instanced with shared disks are configured in a Windows Failover cluster.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-112">**SQL Server Failover Clustering Instances (AlwaysOn FCI)**: Two or more nodes running SQL Server instanced with shared disks are configured in a Windows Failover cluster.</span></span> <span data-ttu-id="cd0f1-113">If a node is down, the cluster can fail SQL Server over to another instance.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-113">If a node is down, the cluster can fail SQL Server over to another instance.</span></span> <span data-ttu-id="cd0f1-114">This setup is typically used to implement high availability at a primary site.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-114">This setup is typically used to implement high availability at a primary site.</span></span> <span data-ttu-id="cd0f1-115">This deployment doesn't protect against failure or outage in the shared storage layer.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-115">This deployment doesn't protect against failure or outage in the shared storage layer.</span></span> <span data-ttu-id="cd0f1-116">A shared disk can be implemented using iSCSI, fiber channel or shared vhdx.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-116">A shared disk can be implemented using iSCSI, fiber channel or shared vhdx.</span></span>
* <span data-ttu-id="cd0f1-117">**SQL AlwaysOn Availability Groups**: Two or more nodes are set up in a shared nothing cluster, with SQL Server databases configured in an availability group, with synchronous replication and automatic failover.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-117">**SQL AlwaysOn Availability Groups**: Two or more nodes are set up in a shared nothing cluster, with SQL Server databases configured in an availability group, with synchronous replication and automatic failover.</span></span>

 <span data-ttu-id="cd0f1-118">This article leverages the following native SQL disaster recovery technologies for recovering databases to a remote site:</span><span class="sxs-lookup"><span data-stu-id="cd0f1-118">This article leverages the following native SQL disaster recovery technologies for recovering databases to a remote site:</span></span>

* <span data-ttu-id="cd0f1-119">SQL AlwaysOn Availability Groups, to provide for disaster recovery for SQL Server 2012 or 2014 Enterprise editions.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-119">SQL AlwaysOn Availability Groups, to provide for disaster recovery for SQL Server 2012 or 2014 Enterprise editions.</span></span>
* <span data-ttu-id="cd0f1-120">SQL database mirroring in high safety mode, for SQL Server Standard edition (any version), or for SQL Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-120">SQL database mirroring in high safety mode, for SQL Server Standard edition (any version), or for SQL Server 2008 R2.</span></span>

## <a name="site-recovery-support"></a><span data-ttu-id="cd0f1-121">Site Recovery support</span><span class="sxs-lookup"><span data-stu-id="cd0f1-121">Site Recovery support</span></span>

### <a name="supported-scenarios"></a><span data-ttu-id="cd0f1-122">Supported scenarios</span><span class="sxs-lookup"><span data-stu-id="cd0f1-122">Supported scenarios</span></span>
<span data-ttu-id="cd0f1-123">Site Recovery can protect SQL Server as summarized in the table.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-123">Site Recovery can protect SQL Server as summarized in the table.</span></span>

<span data-ttu-id="cd0f1-124">**Scenario**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-124">**Scenario**</span></span> | <span data-ttu-id="cd0f1-125">**To a secondary site**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-125">**To a secondary site**</span></span> | <span data-ttu-id="cd0f1-126">**To Azure**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-126">**To Azure**</span></span>
--- | --- | ---
<span data-ttu-id="cd0f1-127">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-127">**Hyper-V**</span></span> | <span data-ttu-id="cd0f1-128">Yes</span><span class="sxs-lookup"><span data-stu-id="cd0f1-128">Yes</span></span> | <span data-ttu-id="cd0f1-129">Yes</span><span class="sxs-lookup"><span data-stu-id="cd0f1-129">Yes</span></span>
<span data-ttu-id="cd0f1-130">**VMware**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-130">**VMware**</span></span> | <span data-ttu-id="cd0f1-131">Yes</span><span class="sxs-lookup"><span data-stu-id="cd0f1-131">Yes</span></span> | <span data-ttu-id="cd0f1-132">Yes</span><span class="sxs-lookup"><span data-stu-id="cd0f1-132">Yes</span></span>
<span data-ttu-id="cd0f1-133">**Physical server**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-133">**Physical server**</span></span> | <span data-ttu-id="cd0f1-134">Yes</span><span class="sxs-lookup"><span data-stu-id="cd0f1-134">Yes</span></span> | <span data-ttu-id="cd0f1-135">Yes</span><span class="sxs-lookup"><span data-stu-id="cd0f1-135">Yes</span></span>

### <a name="supported-sql-server-versions"></a><span data-ttu-id="cd0f1-136">Supported SQL Server versions</span><span class="sxs-lookup"><span data-stu-id="cd0f1-136">Supported SQL Server versions</span></span>
<span data-ttu-id="cd0f1-137">These SQL Server versions are supported, for the supported scenarios:</span><span class="sxs-lookup"><span data-stu-id="cd0f1-137">These SQL Server versions are supported, for the supported scenarios:</span></span>

* <span data-ttu-id="cd0f1-138">SQL Server 2014 Enterprise and Standard</span><span class="sxs-lookup"><span data-stu-id="cd0f1-138">SQL Server 2014 Enterprise and Standard</span></span>
* <span data-ttu-id="cd0f1-139">SQL Server 2012 Enterprise and Standard</span><span class="sxs-lookup"><span data-stu-id="cd0f1-139">SQL Server 2012 Enterprise and Standard</span></span>
* <span data-ttu-id="cd0f1-140">SQL Server 2008 R2 Enterprise and Standard</span><span class="sxs-lookup"><span data-stu-id="cd0f1-140">SQL Server 2008 R2 Enterprise and Standard</span></span>

### <a name="supported-sql-server-integration"></a><span data-ttu-id="cd0f1-141">Supported SQL Server integration</span><span class="sxs-lookup"><span data-stu-id="cd0f1-141">Supported SQL Server integration</span></span>

<span data-ttu-id="cd0f1-142">Site Recovery can be integrated with native SQL Server BCDR technologies summarized in the table, to provide a disaster recovery solution.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-142">Site Recovery can be integrated with native SQL Server BCDR technologies summarized in the table, to provide a disaster recovery solution.</span></span>

<span data-ttu-id="cd0f1-143">**Feature**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-143">**Feature**</span></span> | <span data-ttu-id="cd0f1-144">**Details**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-144">**Details**</span></span> | <span data-ttu-id="cd0f1-145">**SQL Server**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-145">**SQL Server**</span></span> |
--- | --- | ---
<span data-ttu-id="cd0f1-146">**AlwaysOn availability group**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-146">**AlwaysOn availability group**</span></span> | <span data-ttu-id="cd0f1-147">Multiple standalone instances of SQL Server each run in a failover cluster that has multiple nodes.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-147">Multiple standalone instances of SQL Server each run in a failover cluster that has multiple nodes.</span></span><br/><br/><span data-ttu-id="cd0f1-148">Databases can be grouped into failover groups that can be copied (mirrored) on SQL Server instances so that no shared storage is needed.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-148">Databases can be grouped into failover groups that can be copied (mirrored) on SQL Server instances so that no shared storage is needed.</span></span><br/><br/><span data-ttu-id="cd0f1-149">Provides disaster recovery between a primary site and one or more secondary sites.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-149">Provides disaster recovery between a primary site and one or more secondary sites.</span></span> <span data-ttu-id="cd0f1-150">Two nodes can be set up in a shared nothing cluster with SQL Server databases configured in an availability group with synchronous replication and automatic failover.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-150">Two nodes can be set up in a shared nothing cluster with SQL Server databases configured in an availability group with synchronous replication and automatic failover.</span></span> | <span data-ttu-id="cd0f1-151">SQL Server 2014 & 2012 Enterprise edition</span><span class="sxs-lookup"><span data-stu-id="cd0f1-151">SQL Server 2014 & 2012 Enterprise edition</span></span>
<span data-ttu-id="cd0f1-152">**Failover clustering (AlwaysOn FCI)**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-152">**Failover clustering (AlwaysOn FCI)**</span></span> | <span data-ttu-id="cd0f1-153">SQL Server leverages Windows failover clustering for high availability of on-premises SQL Server workloads.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-153">SQL Server leverages Windows failover clustering for high availability of on-premises SQL Server workloads.</span></span><br/><br/><span data-ttu-id="cd0f1-154">Nodes running instances of SQL Server with shared disks are configured in a failover cluster.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-154">Nodes running instances of SQL Server with shared disks are configured in a failover cluster.</span></span> <span data-ttu-id="cd0f1-155">If an instance is down the cluster fails over to different one.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-155">If an instance is down the cluster fails over to different one.</span></span><br/><br/><span data-ttu-id="cd0f1-156">The cluster doesn't protect against failure or outages in shared storage.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-156">The cluster doesn't protect against failure or outages in shared storage.</span></span> <span data-ttu-id="cd0f1-157">The shared disk can be implemented with iSCSI, fiber channel, or shared VHDXs.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-157">The shared disk can be implemented with iSCSI, fiber channel, or shared VHDXs.</span></span> | <span data-ttu-id="cd0f1-158">SQL Server Enterprise editions</span><span class="sxs-lookup"><span data-stu-id="cd0f1-158">SQL Server Enterprise editions</span></span><br/><br/><span data-ttu-id="cd0f1-159">SQL Server Standard edition (limited to two nodes only)</span><span class="sxs-lookup"><span data-stu-id="cd0f1-159">SQL Server Standard edition (limited to two nodes only)</span></span>
<span data-ttu-id="cd0f1-160">**Database mirroring (high safety mode)**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-160">**Database mirroring (high safety mode)**</span></span> | <span data-ttu-id="cd0f1-161">Protects a single database to a single secondary copy.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-161">Protects a single database to a single secondary copy.</span></span> <span data-ttu-id="cd0f1-162">Available in both high safety (synchronous) and high performance (asynchronous) replication modes.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-162">Available in both high safety (synchronous) and high performance (asynchronous) replication modes.</span></span> <span data-ttu-id="cd0f1-163">Doesn’t require a failover cluster.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-163">Doesn’t require a failover cluster.</span></span> | <span data-ttu-id="cd0f1-164">SQL Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="cd0f1-164">SQL Server 2008 R2</span></span><br/><br/><span data-ttu-id="cd0f1-165">SQL Server Enterprise all editions</span><span class="sxs-lookup"><span data-stu-id="cd0f1-165">SQL Server Enterprise all editions</span></span>
<span data-ttu-id="cd0f1-166">**Standalone SQL Server**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-166">**Standalone SQL Server**</span></span> | <span data-ttu-id="cd0f1-167">The SQL Server and database are hosted on a single server (physical or virtual).</span><span class="sxs-lookup"><span data-stu-id="cd0f1-167">The SQL Server and database are hosted on a single server (physical or virtual).</span></span> <span data-ttu-id="cd0f1-168">Host clustering is used for high availability if the server is virtual.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-168">Host clustering is used for high availability if the server is virtual.</span></span> <span data-ttu-id="cd0f1-169">No guest-level high availability.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-169">No guest-level high availability.</span></span> | <span data-ttu-id="cd0f1-170">Enterprise or Standard edition</span><span class="sxs-lookup"><span data-stu-id="cd0f1-170">Enterprise or Standard edition</span></span>

## <a name="deployment-recommendations"></a><span data-ttu-id="cd0f1-171">Deployment recommendations</span><span class="sxs-lookup"><span data-stu-id="cd0f1-171">Deployment recommendations</span></span>

<span data-ttu-id="cd0f1-172">This table summarizes our recommendations for integrating SQL Server BCDR technologies with Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-172">This table summarizes our recommendations for integrating SQL Server BCDR technologies with Site Recovery.</span></span>

| <span data-ttu-id="cd0f1-173">**Version**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-173">**Version**</span></span> | <span data-ttu-id="cd0f1-174">**Edition**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-174">**Edition**</span></span> | <span data-ttu-id="cd0f1-175">**Deployment**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-175">**Deployment**</span></span> | <span data-ttu-id="cd0f1-176">**On-prem to on-prem**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-176">**On-prem to on-prem**</span></span> | <span data-ttu-id="cd0f1-177">**On-prem to Azure**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-177">**On-prem to Azure**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="cd0f1-178">SQL Server 2014 or 2012</span><span class="sxs-lookup"><span data-stu-id="cd0f1-178">SQL Server 2014 or 2012</span></span> |<span data-ttu-id="cd0f1-179">Enterprise</span><span class="sxs-lookup"><span data-stu-id="cd0f1-179">Enterprise</span></span> |<span data-ttu-id="cd0f1-180">Failover cluster instance</span><span class="sxs-lookup"><span data-stu-id="cd0f1-180">Failover cluster instance</span></span> |<span data-ttu-id="cd0f1-181">AlwaysOn availability groups</span><span class="sxs-lookup"><span data-stu-id="cd0f1-181">AlwaysOn availability groups</span></span> |<span data-ttu-id="cd0f1-182">AlwaysOn availability groups</span><span class="sxs-lookup"><span data-stu-id="cd0f1-182">AlwaysOn availability groups</span></span> |
|| <span data-ttu-id="cd0f1-183">Enterprise</span><span class="sxs-lookup"><span data-stu-id="cd0f1-183">Enterprise</span></span> |<span data-ttu-id="cd0f1-184">AlwaysOn availability groups for high availability</span><span class="sxs-lookup"><span data-stu-id="cd0f1-184">AlwaysOn availability groups for high availability</span></span> |<span data-ttu-id="cd0f1-185">AlwaysOn availability groups</span><span class="sxs-lookup"><span data-stu-id="cd0f1-185">AlwaysOn availability groups</span></span> |<span data-ttu-id="cd0f1-186">AlwaysOn availability groups</span><span class="sxs-lookup"><span data-stu-id="cd0f1-186">AlwaysOn availability groups</span></span> | |
|| <span data-ttu-id="cd0f1-187">Standard</span><span class="sxs-lookup"><span data-stu-id="cd0f1-187">Standard</span></span> |<span data-ttu-id="cd0f1-188">Failover cluster instance (FCI)</span><span class="sxs-lookup"><span data-stu-id="cd0f1-188">Failover cluster instance (FCI)</span></span> |<span data-ttu-id="cd0f1-189">Site Recovery replication with local mirror</span><span class="sxs-lookup"><span data-stu-id="cd0f1-189">Site Recovery replication with local mirror</span></span> |<span data-ttu-id="cd0f1-190">Site Recovery replication with local mirror</span><span class="sxs-lookup"><span data-stu-id="cd0f1-190">Site Recovery replication with local mirror</span></span> | |
|| <span data-ttu-id="cd0f1-191">Enterprise or Standard</span><span class="sxs-lookup"><span data-stu-id="cd0f1-191">Enterprise or Standard</span></span> |<span data-ttu-id="cd0f1-192">Standalone</span><span class="sxs-lookup"><span data-stu-id="cd0f1-192">Standalone</span></span> |<span data-ttu-id="cd0f1-193">Site Recovery replication</span><span class="sxs-lookup"><span data-stu-id="cd0f1-193">Site Recovery replication</span></span> |<span data-ttu-id="cd0f1-194">Site Recovery replication</span><span class="sxs-lookup"><span data-stu-id="cd0f1-194">Site Recovery replication</span></span> | |
| <span data-ttu-id="cd0f1-195">SQL Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="cd0f1-195">SQL Server 2008 R2</span></span> |<span data-ttu-id="cd0f1-196">Enterprise or Standard</span><span class="sxs-lookup"><span data-stu-id="cd0f1-196">Enterprise or Standard</span></span> |<span data-ttu-id="cd0f1-197">Failover cluster instance (FCI)</span><span class="sxs-lookup"><span data-stu-id="cd0f1-197">Failover cluster instance (FCI)</span></span> |<span data-ttu-id="cd0f1-198">Site Recovery replication with local mirror</span><span class="sxs-lookup"><span data-stu-id="cd0f1-198">Site Recovery replication with local mirror</span></span> |<span data-ttu-id="cd0f1-199">Site Recovery replication with local mirror</span><span class="sxs-lookup"><span data-stu-id="cd0f1-199">Site Recovery replication with local mirror</span></span> |
|| <span data-ttu-id="cd0f1-200">Enterprise or Standard</span><span class="sxs-lookup"><span data-stu-id="cd0f1-200">Enterprise or Standard</span></span> |<span data-ttu-id="cd0f1-201">Standalone</span><span class="sxs-lookup"><span data-stu-id="cd0f1-201">Standalone</span></span> |<span data-ttu-id="cd0f1-202">Site Recovery replication</span><span class="sxs-lookup"><span data-stu-id="cd0f1-202">Site Recovery replication</span></span> |<span data-ttu-id="cd0f1-203">Site Recovery replication</span><span class="sxs-lookup"><span data-stu-id="cd0f1-203">Site Recovery replication</span></span> | |
| <span data-ttu-id="cd0f1-204">SQL Server (Any version)</span><span class="sxs-lookup"><span data-stu-id="cd0f1-204">SQL Server (Any version)</span></span> |<span data-ttu-id="cd0f1-205">Enterprise or Standard</span><span class="sxs-lookup"><span data-stu-id="cd0f1-205">Enterprise or Standard</span></span> |<span data-ttu-id="cd0f1-206">Failover cluster instance - DTC application</span><span class="sxs-lookup"><span data-stu-id="cd0f1-206">Failover cluster instance - DTC application</span></span> |<span data-ttu-id="cd0f1-207">Site Recovery replication</span><span class="sxs-lookup"><span data-stu-id="cd0f1-207">Site Recovery replication</span></span> |<span data-ttu-id="cd0f1-208">Not Supported</span><span class="sxs-lookup"><span data-stu-id="cd0f1-208">Not Supported</span></span> |

## <a name="deployment-prerequisites"></a><span data-ttu-id="cd0f1-209">Deployment prerequisites</span><span class="sxs-lookup"><span data-stu-id="cd0f1-209">Deployment prerequisites</span></span>

* <span data-ttu-id="cd0f1-210">An on-premises SQL Server deployment, running a supported SQL Server version.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-210">An on-premises SQL Server deployment, running a supported SQL Server version.</span></span> <span data-ttu-id="cd0f1-211">Typically, you also need Active Directory for your SQL server.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-211">Typically, you also need Active Directory for your SQL server.</span></span>
* <span data-ttu-id="cd0f1-212">The requirements for the scenario you want to deploy.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-212">The requirements for the scenario you want to deploy.</span></span> <span data-ttu-id="cd0f1-213">Learn more about support requirements for [replication to Azure](site-recovery-support-matrix-to-azure.md) and [on-premises](site-recovery-support-matrix.md), and [deployment prerequisites](site-recovery-prereq.md).</span><span class="sxs-lookup"><span data-stu-id="cd0f1-213">Learn more about support requirements for [replication to Azure](site-recovery-support-matrix-to-azure.md) and [on-premises](site-recovery-support-matrix.md), and [deployment prerequisites](site-recovery-prereq.md).</span></span>
* <span data-ttu-id="cd0f1-214">To set up recovery in Azure, run the [Azure Virtual Machine Readiness Assessment](http://www.microsoft.com/download/details.aspx?id=40898) tool on your SQL Server virtual machines, to make sure they're compatible with Azure and Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-214">To set up recovery in Azure, run the [Azure Virtual Machine Readiness Assessment](http://www.microsoft.com/download/details.aspx?id=40898) tool on your SQL Server virtual machines, to make sure they're compatible with Azure and Site Recovery.</span></span>

## <a name="set-up-active-directory"></a><span data-ttu-id="cd0f1-215">Set up Active Directory</span><span class="sxs-lookup"><span data-stu-id="cd0f1-215">Set up Active Directory</span></span>

<span data-ttu-id="cd0f1-216">Set up Active Directory, in the secondary recovery site, for SQL Server to run properly.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-216">Set up Active Directory, in the secondary recovery site, for SQL Server to run properly.</span></span>

* <span data-ttu-id="cd0f1-217">**Small enterprise**—With a small number of applications, and single domain controller for the on-premises site, if you want to fail over the entire site, we recommend you use Site Recovery replication to replicate the domain controller to the secondary datacenter, or to Azure.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-217">**Small enterprise**—With a small number of applications, and single domain controller for the on-premises site, if you want to fail over the entire site, we recommend you use Site Recovery replication to replicate the domain controller to the secondary datacenter, or to Azure.</span></span>
* <span data-ttu-id="cd0f1-218">**Medium to large enterprise**—If you have a large number of applications, an Active Directory forest, and you want to fail over by application or workload, we recommend you set up an additional domain controller in the secondary datacenter, or in Azure.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-218">**Medium to large enterprise**—If you have a large number of applications, an Active Directory forest, and you want to fail over by application or workload, we recommend you set up an additional domain controller in the secondary datacenter, or in Azure.</span></span> <span data-ttu-id="cd0f1-219">If you're using AlwaysOn availability groups to recover to a remote site, we recommend you set up another additional domain controller on the secondary site or in Azure, to use for the recovered SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-219">If you're using AlwaysOn availability groups to recover to a remote site, we recommend you set up another additional domain controller on the secondary site or in Azure, to use for the recovered SQL Server instance.</span></span>

<span data-ttu-id="cd0f1-220">The instructions in this article presume that a domain controller is available in the secondary location.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-220">The instructions in this article presume that a domain controller is available in the secondary location.</span></span> <span data-ttu-id="cd0f1-221">[Read more](site-recovery-active-directory.md) about protecting Active Directory with Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-221">[Read more](site-recovery-active-directory.md) about protecting Active Directory with Site Recovery.</span></span>

## <a name="integrate-with-sql-server-alwayson-for-replication-to-azure-classic-portal-with-a-vmmconfiguration-server"></a><span data-ttu-id="cd0f1-222">Integrate with SQL Server AlwaysOn for replication to Azure (classic portal with a VMM/configuration server)</span><span class="sxs-lookup"><span data-stu-id="cd0f1-222">Integrate with SQL Server AlwaysOn for replication to Azure (classic portal with a VMM/configuration server)</span></span>


<span data-ttu-id="cd0f1-223">Site Recovery natively supports SQL AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-223">Site Recovery natively supports SQL AlwaysOn.</span></span> <span data-ttu-id="cd0f1-224">If you've created a SQL Availability Group with an Azure virtual machine set up as secondary location, then you can use Site Recovery to manage the failover of the Availability Groups.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-224">If you've created a SQL Availability Group with an Azure virtual machine set up as secondary location, then you can use Site Recovery to manage the failover of the Availability Groups.</span></span>

> [!NOTE]
> <span data-ttu-id="cd0f1-225">This capability is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-225">This capability is currently in preview.</span></span> <span data-ttu-id="cd0f1-226">It's available when the primary site has Hyper-V host servers managed in System Center VMM clouds, or when you've set up [VMware replication](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="cd0f1-226">It's available when the primary site has Hyper-V host servers managed in System Center VMM clouds, or when you've set up [VMware replication](site-recovery-vmware-to-azure.md).</span></span> <span data-ttu-id="cd0f1-227">The functionality isn't currently available in the new Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-227">The functionality isn't currently available in the new Azure portal.</span></span> <span data-ttu-id="cd0f1-228">Follow the steps in [this section](site-recovery-sql.md#integrate-with-sql-server-alwayson-for-replication-to-azure-azure-portalclassic-portal-with-no-vmmconfiguration-server) if you are using new Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-228">Follow the steps in [this section](site-recovery-sql.md#integrate-with-sql-server-alwayson-for-replication-to-azure-azure-portalclassic-portal-with-no-vmmconfiguration-server) if you are using new Azure portal.</span></span>
>
>


#### <a name="before-you-start"></a><span data-ttu-id="cd0f1-229">Before you start</span><span class="sxs-lookup"><span data-stu-id="cd0f1-229">Before you start</span></span>

<span data-ttu-id="cd0f1-230">To integrate SQL AlwaysOn with Site Recovery you need:</span><span class="sxs-lookup"><span data-stu-id="cd0f1-230">To integrate SQL AlwaysOn with Site Recovery you need:</span></span>

* <span data-ttu-id="cd0f1-231">An on-premises SQL Server (standalone server or a failover cluster).</span><span class="sxs-lookup"><span data-stu-id="cd0f1-231">An on-premises SQL Server (standalone server or a failover cluster).</span></span>
* <span data-ttu-id="cd0f1-232">One or more Azure virtual machines, with SQL Server installed.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-232">One or more Azure virtual machines, with SQL Server installed.</span></span>
* <span data-ttu-id="cd0f1-233">A SQL Server Availability Group, set up between an on-premises SQL Server and SQL Server running in Azure.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-233">A SQL Server Availability Group, set up between an on-premises SQL Server and SQL Server running in Azure.</span></span>
* <span data-ttu-id="cd0f1-234">PowerShell remoting enabled on the on-premises SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-234">PowerShell remoting enabled on the on-premises SQL Server.</span></span> <span data-ttu-id="cd0f1-235">The VMM server or the configuration server should be able to make remote PowerShell calls to the SQL Server machine.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-235">The VMM server or the configuration server should be able to make remote PowerShell calls to the SQL Server machine.</span></span>
* <span data-ttu-id="cd0f1-236">A user account should be added to the on-premises SQL Server machine.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-236">A user account should be added to the on-premises SQL Server machine.</span></span> <span data-ttu-id="cd0f1-237">Add in a SQL Server group with at least these permissions:</span><span class="sxs-lookup"><span data-stu-id="cd0f1-237">Add in a SQL Server group with at least these permissions:</span></span>
  * <span data-ttu-id="cd0f1-238">ALTER AVAILABILITY GROUP: permissions [here](https://msdn.microsoft.com/library/hh231018.aspx), and [here](https://msdn.microsoft.com/library/ff878601.aspx#Anchor_3)</span><span class="sxs-lookup"><span data-stu-id="cd0f1-238">ALTER AVAILABILITY GROUP: permissions [here](https://msdn.microsoft.com/library/hh231018.aspx), and [here](https://msdn.microsoft.com/library/ff878601.aspx#Anchor_3)</span></span>
  * <span data-ttu-id="cd0f1-239">ALTER DATABASE - permissions [here](https://msdn.microsoft.com/library/ff877956.aspx#Security)</span><span class="sxs-lookup"><span data-stu-id="cd0f1-239">ALTER DATABASE - permissions [here](https://msdn.microsoft.com/library/ff877956.aspx#Security)</span></span>
* <span data-ttu-id="cd0f1-240">If you're running VMM, A RunAs account should be created on VMM server</span><span class="sxs-lookup"><span data-stu-id="cd0f1-240">If you're running VMM, A RunAs account should be created on VMM server</span></span>
- <span data-ttu-id="cd0f1-241">If you're running VMware, an account should be created on the configuration server using the CSPSConfigtool.exe</span><span class="sxs-lookup"><span data-stu-id="cd0f1-241">If you're running VMware, an account should be created on the configuration server using the CSPSConfigtool.exe</span></span>
* <span data-ttu-id="cd0f1-242">The SQL PS module should be installed on SQL Servers running on-premises, and on Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-242">The SQL PS module should be installed on SQL Servers running on-premises, and on Azure VMs.</span></span>
* <span data-ttu-id="cd0f1-243">The VM agent should be installed on Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-243">The VM agent should be installed on Azure VMs.</span></span>
* <span data-ttu-id="cd0f1-244">NTAUTHORITY\System should have following permissions in SQL Server running on Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-244">NTAUTHORITY\System should have following permissions in SQL Server running on Azure VMs.</span></span>
  * <span data-ttu-id="cd0f1-245">ALTER AVAILABILITY GROUP: permissions [here](https://msdn.microsoft.com/library/hh231018.aspx), and [here](https://msdn.microsoft.com/library/ff878601.aspx#Anchor_3)</span><span class="sxs-lookup"><span data-stu-id="cd0f1-245">ALTER AVAILABILITY GROUP: permissions [here](https://msdn.microsoft.com/library/hh231018.aspx), and [here](https://msdn.microsoft.com/library/ff878601.aspx#Anchor_3)</span></span>
  * <span data-ttu-id="cd0f1-246">ALTER DATABASE - permissions [here](https://msdn.microsoft.com/library/ff877956.aspx#Security)</span><span class="sxs-lookup"><span data-stu-id="cd0f1-246">ALTER DATABASE - permissions [here](https://msdn.microsoft.com/library/ff877956.aspx#Security)</span></span>

### <a name="add-a-sql-server"></a><span data-ttu-id="cd0f1-247">Add a SQL Server</span><span class="sxs-lookup"><span data-stu-id="cd0f1-247">Add a SQL Server</span></span>
1. <span data-ttu-id="cd0f1-248">Click **Add SQL** to add a new SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-248">Click **Add SQL** to add a new SQL Server.</span></span>

    ![Add SQL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-sql/add-sql.png)
2. <span data-ttu-id="cd0f1-250">In **Configure SQL Settings** > **Name** provide a friendly name for the SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-250">In **Configure SQL Settings** > **Name** provide a friendly name for the SQL Server.</span></span>
3. <span data-ttu-id="cd0f1-251">**In SQL Server (FQDN)**, specify the FQDN of the source SQL Server that you want to add.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-251">**In SQL Server (FQDN)**, specify the FQDN of the source SQL Server that you want to add.</span></span> <span data-ttu-id="cd0f1-252">If SQL Server is installed on a failover cluster, provide the FQDN of the cluster, and not of the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-252">If SQL Server is installed on a failover cluster, provide the FQDN of the cluster, and not of the cluster nodes.</span></span>  
4. <span data-ttu-id="cd0f1-253">In **SQL Server Instance**, choose the default instance or provide the custom name.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-253">In **SQL Server Instance**, choose the default instance or provide the custom name.</span></span>
5. <span data-ttu-id="cd0f1-254">In **Management Server**, select a VMM server or configuration server, registered in the vault.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-254">In **Management Server**, select a VMM server or configuration server, registered in the vault.</span></span> <span data-ttu-id="cd0f1-255">Site Recovery uses this server to communicate with the SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-255">Site Recovery uses this server to communicate with the SQL Server.</span></span>
6. <span data-ttu-id="cd0f1-256">In **Run as Account**, provide the name of the VMM RunAs account, or the configuration server account.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-256">In **Run as Account**, provide the name of the VMM RunAs account, or the configuration server account.</span></span> <span data-ttu-id="cd0f1-257">This account is used to access the SQL Server, and should have Read and Failover permissions for the availability groups on the SQL Server machine.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-257">This account is used to access the SQL Server, and should have Read and Failover permissions for the availability groups on the SQL Server machine.</span></span>

    ![Add SQL Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-sql/add-sql-dialog.png)

<span data-ttu-id="cd0f1-259">After you add the SQL Server, it appears in the **SQL Servers** tab.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-259">After you add the SQL Server, it appears in the **SQL Servers** tab.</span></span>

![SQL Server List](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-sql/sql-server-list.png)

### <a name="add-a-sql-availability-group"></a><span data-ttu-id="cd0f1-261">Add a SQL Availability Group</span><span class="sxs-lookup"><span data-stu-id="cd0f1-261">Add a SQL Availability Group</span></span>

1. <span data-ttu-id="cd0f1-262">In the SQL Server you added, click **Add SQL Availability Group**.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-262">In the SQL Server you added, click **Add SQL Availability Group**.</span></span>

    ![Add SQL AG](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-sql/add-sqlag.png)
2. <span data-ttu-id="cd0f1-264">The Availability Group can be replicating to one or more Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-264">The Availability Group can be replicating to one or more Azure VMs.</span></span> <span data-ttu-id="cd0f1-265">When you add the group, you need to provide the name and subscription of the Azure VM to which you want to the group to be failed over by Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-265">When you add the group, you need to provide the name and subscription of the Azure VM to which you want to the group to be failed over by Site Recovery.</span></span>

    ![Add SQL AG Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-sql/add-sqlag-dialog.png)
3. <span data-ttu-id="cd0f1-267">In this example, Availability Group DB1-AG will become primary, on virtual machine SQLAGVM2 running inside subscription DevTesting2 on a failover.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-267">In this example, Availability Group DB1-AG will become primary, on virtual machine SQLAGVM2 running inside subscription DevTesting2 on a failover.</span></span>

> [!NOTE]
> <span data-ttu-id="cd0f1-268">Only the Availability Groups that are primary on the added SQL Server can be added to Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-268">Only the Availability Groups that are primary on the added SQL Server can be added to Site Recovery.</span></span> <span data-ttu-id="cd0f1-269">If you've made an Availability Group primary on the SQL Server, or you've added more Availability Groups on the SQL Server after it was added, refresh the group on the SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-269">If you've made an Availability Group primary on the SQL Server, or you've added more Availability Groups on the SQL Server after it was added, refresh the group on the SQL Server.</span></span>
>
>

### <a name="create-a-recovery-plan"></a><span data-ttu-id="cd0f1-270">Create a recovery plan</span><span class="sxs-lookup"><span data-stu-id="cd0f1-270">Create a recovery plan</span></span>

<span data-ttu-id="cd0f1-271">Create a recovery plan using both virtual machines, and the availability groups.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-271">Create a recovery plan using both virtual machines, and the availability groups.</span></span> <span data-ttu-id="cd0f1-272">Select the VMM server, or configuration server, as the source, and Azure as the target.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-272">Select the VMM server, or configuration server, as the source, and Azure as the target.</span></span>

![Create Recovery Plan](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-sql/create-rp1.png)

![Create Recovery Plan](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-sql/create-rp2.png)

<span data-ttu-id="cd0f1-275">In the example, the Sharepoint app consists of three virtual machines which use a SQL Availability Group as a backend.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-275">In the example, the Sharepoint app consists of three virtual machines which use a SQL Availability Group as a backend.</span></span> <span data-ttu-id="cd0f1-276">In this recovery plan, we can select both the availability group, and the app VMs.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-276">In this recovery plan, we can select both the availability group, and the app VMs.</span></span> <span data-ttu-id="cd0f1-277">You can further customize the recovery plan by moving VMs to different failover groups, to sequence the failover order.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-277">You can further customize the recovery plan by moving VMs to different failover groups, to sequence the failover order.</span></span> <span data-ttu-id="cd0f1-278">The Availability Group is always failed over first, because it's used as the app backend.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-278">The Availability Group is always failed over first, because it's used as the app backend.</span></span>

![Customize Recovery Plan](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-sql/customize-rp.png)

### <a name="failover"></a><span data-ttu-id="cd0f1-280">Failover</span><span class="sxs-lookup"><span data-stu-id="cd0f1-280">Failover</span></span>

<span data-ttu-id="cd0f1-281">After the Availability Group is added to a recovery plan, different failover options are available.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-281">After the Availability Group is added to a recovery plan, different failover options are available.</span></span>

<span data-ttu-id="cd0f1-282">**Failover**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-282">**Failover**</span></span> | <span data-ttu-id="cd0f1-283">**Details**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-283">**Details**</span></span>
--- | ---
<span data-ttu-id="cd0f1-284">**Planned failover**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-284">**Planned failover**</span></span> | <span data-ttu-id="cd0f1-285">Planned failover implies a no data loss failover.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-285">Planned failover implies a no data loss failover.</span></span> <span data-ttu-id="cd0f1-286">To achieve that, the SQL Availability Group mode is set to synchronous, and then a failover is triggered to make the availability group primary on the virtual machine provided, while adding the group to Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-286">To achieve that, the SQL Availability Group mode is set to synchronous, and then a failover is triggered to make the availability group primary on the virtual machine provided, while adding the group to Site Recovery.</span></span> <span data-ttu-id="cd0f1-287">After the failover is complete, Availability Mode is set to the same value as it was before the planned failover was triggered.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-287">After the failover is complete, Availability Mode is set to the same value as it was before the planned failover was triggered.</span></span>
<span data-ttu-id="cd0f1-288">**Unplanned failover**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-288">**Unplanned failover**</span></span> | <span data-ttu-id="cd0f1-289">Unplanned Failover can result in data loss.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-289">Unplanned Failover can result in data loss.</span></span> <span data-ttu-id="cd0f1-290">While triggering unplanned failover, the availability mode of the group isn't changed.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-290">While triggering unplanned failover, the availability mode of the group isn't changed.</span></span> <span data-ttu-id="cd0f1-291">It's made into primary on the virtual machine provided, while adding the availability group to Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-291">It's made into primary on the virtual machine provided, while adding the availability group to Site Recovery.</span></span> <span data-ttu-id="cd0f1-292">After unplanned failover is complete, and the on-premises server running SQL Server is available again, reverse replication has to be triggered on the Availability Group.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-292">After unplanned failover is complete, and the on-premises server running SQL Server is available again, reverse replication has to be triggered on the Availability Group.</span></span> <span data-ttu-id="cd0f1-293">This action is available in **SQL Servers** > **SQL Availability Group**, and not on the recovery plan.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-293">This action is available in **SQL Servers** > **SQL Availability Group**, and not on the recovery plan.</span></span>
<span data-ttu-id="cd0f1-294">**Test failover**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-294">**Test failover**</span></span> |<span data-ttu-id="cd0f1-295">nTest failover for SQL Availability Group isn't supported.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-295">nTest failover for SQL Availability Group isn't supported.</span></span> <span data-ttu-id="cd0f1-296">If you trigger a test failover, failover is skipped for the Availability Group.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-296">If you trigger a test failover, failover is skipped for the Availability Group.</span></span>

<span data-ttu-id="cd0f1-297">Try these failover options.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-297">Try these failover options.</span></span>

<span data-ttu-id="cd0f1-298">**Option**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-298">**Option**</span></span> | <span data-ttu-id="cd0f1-299">**Details**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-299">**Details**</span></span>
--- | ---
<span data-ttu-id="cd0f1-300">**Option 1**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-300">**Option 1**</span></span> | <span data-ttu-id="cd0f1-301">1. Perform a test failover of the application and front-end tiers.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-301">1. Perform a test failover of the application and front-end tiers.</span></span><br/><br/><span data-ttu-id="cd0f1-302">2. Update the application tier to access the replica copy in read-only mode, and perform a read-only test of the application.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-302">2. Update the application tier to access the replica copy in read-only mode, and perform a read-only test of the application.</span></span>
<span data-ttu-id="cd0f1-303">**Option 2**</span><span class="sxs-lookup"><span data-stu-id="cd0f1-303">**Option 2**</span></span> | <span data-ttu-id="cd0f1-304">1. Create a copy of the replica SQL Server virtual machine instance (using VMM clone for site-to-site, or Azure Backup) and bring it up in a test network</span><span class="sxs-lookup"><span data-stu-id="cd0f1-304">1. Create a copy of the replica SQL Server virtual machine instance (using VMM clone for site-to-site, or Azure Backup) and bring it up in a test network</span></span><br/><br/> <span data-ttu-id="cd0f1-305">2. Perform the test failover using the recovery plan.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-305">2. Perform the test failover using the recovery plan.</span></span>

### <a name="fail-back"></a><span data-ttu-id="cd0f1-306">Fail back</span><span class="sxs-lookup"><span data-stu-id="cd0f1-306">Fail back</span></span>

<span data-ttu-id="cd0f1-307">If you want to make the Availability Group primary again on the on-premises SQL Server, then you can trigger a planned failover on the recovery plan, and select the direction from Microsoft Azure to the on-premises server.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-307">If you want to make the Availability Group primary again on the on-premises SQL Server, then you can trigger a planned failover on the recovery plan, and select the direction from Microsoft Azure to the on-premises server.</span></span>

> [!NOTE]
> <span data-ttu-id="cd0f1-308">After an unplanned failover, reverse replication should be triggered on the Availability Group, to resume replication.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-308">After an unplanned failover, reverse replication should be triggered on the Availability Group, to resume replication.</span></span>  <span data-ttu-id="cd0f1-309">Replication remains suspended until this is done.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-309">Replication remains suspended until this is done.</span></span>
>
>

## <a name="integrate-with-sql-server-alwayson-for-replication-to-azure-azure-portalclassic-portal-with-no-vmmconfiguration-server"></a><span data-ttu-id="cd0f1-310">Integrate with SQL Server AlwaysOn for replication to Azure (Azure portal/classic portal with no VMM/configuration server)</span><span class="sxs-lookup"><span data-stu-id="cd0f1-310">Integrate with SQL Server AlwaysOn for replication to Azure (Azure portal/classic portal with no VMM/configuration server)</span></span>

<span data-ttu-id="cd0f1-311">These instructions are relevant if you're integrating with SQL Server Availability Groups in the new Azure portal, or in the classic portal if you're not using a VMM server, or configuration server.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-311">These instructions are relevant if you're integrating with SQL Server Availability Groups in the new Azure portal, or in the classic portal if you're not using a VMM server, or configuration server.</span></span> <span data-ttu-id="cd0f1-312">In this scenario, Azure Automation Runbooks can be used to configure a scripted failover of SQL Availability Groups.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-312">In this scenario, Azure Automation Runbooks can be used to configure a scripted failover of SQL Availability Groups.</span></span>

<span data-ttu-id="cd0f1-313">Here's what you need to do:</span><span class="sxs-lookup"><span data-stu-id="cd0f1-313">Here's what you need to do:</span></span>

1. <span data-ttu-id="cd0f1-314">Create a local file for a script that fails over an availability group.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-314">Create a local file for a script that fails over an availability group.</span></span> <span data-ttu-id="cd0f1-315">This sample script specifies a path to the availability group on the Azure replica, and fails it over to that replica instance.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-315">This sample script specifies a path to the availability group on the Azure replica, and fails it over to that replica instance.</span></span> <span data-ttu-id="cd0f1-316">This script is run on the SQL Server replica virtual machine, by passing it with the custom script extension.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-316">This script is run on the SQL Server replica virtual machine, by passing it with the custom script extension.</span></span>

        ``Param(
        [string]$SQLAvailabilityGroupPath
        )
        import-module sqlps
        Switch-SqlAvailabilityGroup -Path $SQLAvailabilityGroupPath -AllowDataLoss -force``

2. <span data-ttu-id="cd0f1-317">Upload the script to a blob in an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-317">Upload the script to a blob in an Azure storage account.</span></span> <span data-ttu-id="cd0f1-318">Use this example:</span><span class="sxs-lookup"><span data-stu-id="cd0f1-318">Use this example:</span></span>

        ``$context = New-AzureStorageContext -StorageAccountName "Account" -StorageAccountKey "Key"
        Set-AzureStorageBlobContent -Blob "AGFailover.ps1" -Container "script-container" -File "ScriptLocalFilePath" -context $context``

3. <span data-ttu-id="cd0f1-319">Create an Azure automation runbook to invoke the scripts, on the SQL Server replica virtual machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-319">Create an Azure automation runbook to invoke the scripts, on the SQL Server replica virtual machine in Azure.</span></span> <span data-ttu-id="cd0f1-320">Use this sample script to do this.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-320">Use this sample script to do this.</span></span> <span data-ttu-id="cd0f1-321">[Learn more](site-recovery-runbook-automation.md) about using automation runbooks in recovery plans.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-321">[Learn more](site-recovery-runbook-automation.md) about using automation runbooks in recovery plans.</span></span>

4. <span data-ttu-id="cd0f1-322">When you create a recovery plan for the application, add a "pre-Group 1 boot" script step that invokes the automation runbook to fail over the availability group.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-322">When you create a recovery plan for the application, add a "pre-Group 1 boot" script step that invokes the automation runbook to fail over the availability group.</span></span>


5. <span data-ttu-id="cd0f1-323">SQL AlwaysOn doesn’t natively support test failover.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-323">SQL AlwaysOn doesn’t natively support test failover.</span></span> <span data-ttu-id="cd0f1-324">Therefore, we recommend the following:</span><span class="sxs-lookup"><span data-stu-id="cd0f1-324">Therefore, we recommend the following:</span></span>
    1. <span data-ttu-id="cd0f1-325">Set up [Azure Backup](../backup/backup-azure-vms.md) on the virtual machine that hosts the availability group replica in Azure.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-325">Set up [Azure Backup](../backup/backup-azure-vms.md) on the virtual machine that hosts the availability group replica in Azure.</span></span>
    1. <span data-ttu-id="cd0f1-326">Before triggering test failover of the recovery plan, recover the virtual machine from the backup taken in the previous step.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-326">Before triggering test failover of the recovery plan, recover the virtual machine from the backup taken in the previous step.</span></span>
    1. <span data-ttu-id="cd0f1-327">Do a test failover of the recovery plan.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-327">Do a test failover of the recovery plan.</span></span>


> [!NOTE]
> <span data-ttu-id="cd0f1-328">The script below assumes that the SQL Availability Group is hosted in a classic Azure VM, and that the name of restored virtual machine in Step-2 is SQLAzureVM-Test.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-328">The script below assumes that the SQL Availability Group is hosted in a classic Azure VM, and that the name of restored virtual machine in Step-2 is SQLAzureVM-Test.</span></span> <span data-ttu-id="cd0f1-329">Modify the script, based on the name you use for the recovered virtual machine.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-329">Modify the script, based on the name you use for the recovered virtual machine.</span></span>
>
>


     ``workflow SQLAvailabilityGroupFailover
     {

         param (
             [Object]$RecoveryPlanContext
         )

         $Cred = Get-AutomationPSCredential -name 'AzureCredential'

         #Connect to Azure
         $AzureAccount = Add-AzureAccount -Credential $Cred
         $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
         Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

         InLineScript
         {
          #Update the script with name of your storage account, key and blob name
          $context = New-AzureStorageContext -StorageAccountName "Account" -StorageAccountKey "Key";
          $sasuri = New-AzureStorageBlobSASToken -Container "script-container"- Blob "AGFailover.ps1" -Permission r -FullUri -Context $context;

          Write-output "failovertype " + $Using:RecoveryPlanContext.FailoverType;

          if ($Using:RecoveryPlanContext.FailoverType -eq "Test")
                {
                    Write-output "tfo"

                    Write-Output "Creating ILB"
                    Add-AzureInternalLoadBalancer -InternalLoadBalancerName SQLAGILB -SubnetName Subnet-1 -ServiceName SQLAzureVM-Test -StaticVNetIPAddress #IP
                    Write-Output "ILB Created"

                    #Update the script with name of the virtual machine recovered using Azure Backup
                    Write-Output "Adding SQL AG Endpoint"
                    Get-AzureVM -ServiceName "SQLAzureVM-Test" -Name "SQLAzureVM-Test"| Add-AzureEndpoint -Name sqlag -LBSetName sqlagset -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName SQLAGILB | Update-AzureVM

                    Write-Output "Added Endpoint"

                    $VM = Get-AzureVM -Name "SQLAzureVM-Test" -ServiceName "SQLAzureVM-Test"

                    Write-Output "UnInstalling custom script extension"
                    Set-AzureVMCustomScriptExtension -Uninstall -ReferenceName CustomScriptExtension -VM $VM |Update-AzureVM
                    Write-Output "Installing custom script extension"
                    Set-AzureVMExtension -ExtensionName CustomScriptExtension -VM $vm -Publisher Microsoft.Compute -Version 1.*| Update-AzureVM   

                    Write-output "Starting AG Failover"
                    Set-AzureVMCustomScriptExtension -VM $VM -FileUri $sasuri -Run "AGFailover.ps1" -Argument "-Path sqlserver:\sql\sqlazureVM\default\availabilitygroups\testag"  | Update-AzureVM
                    Write-output "Completed AG Failover"
                }
          else
                {
                Write-output "pfo/ufo";
                #Get the SQL Azure Replica VM.
                #Update the script to use the name of your VM and Cloud Service
                $VM = Get-AzureVM -Name "SQLAzureVM" -ServiceName "SQLAzureReplica";     

                Write-Output "Installing custom script extension"
                #Install the Custom Script Extension on teh SQL Replica VM
                Set-AzureVMExtension -ExtensionName CustomScriptExtension -VM $VM -Publisher Microsoft.Compute -Version 1.*| Update-AzureVM;

                Write-output "Starting AG Failover";
                #Execute the SQL Failover script
                #Pass the SQL AG path as the argument.

                $AGArgs="-SQLAvailabilityGroupPath sqlserver:\sql\sqlazureVM\default\availabilitygroups\testag";

                Set-AzureVMCustomScriptExtension -VM $VM -FileUri $sasuri -Run "AGFailover.ps1" -Argument $AGArgs | Update-AzureVM;

                Write-output "Completed AG Failover";

                }

         }
     }``

## <a name="integrate-with-sql-server-alwayson-for-replication-to-a-secondary-on-premises-site"></a><span data-ttu-id="cd0f1-330">Integrate with SQL Server AlwaysOn for replication to a secondary on-premises site</span><span class="sxs-lookup"><span data-stu-id="cd0f1-330">Integrate with SQL Server AlwaysOn for replication to a secondary on-premises site</span></span>

<span data-ttu-id="cd0f1-331">If the SQL Server is using availability groups for high availability (or an FCI), we recommend using availability groups on the recovery site as well.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-331">If the SQL Server is using availability groups for high availability (or an FCI), we recommend using availability groups on the recovery site as well.</span></span> <span data-ttu-id="cd0f1-332">Note that this applies to apps that don't use distributed transactions.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-332">Note that this applies to apps that don't use distributed transactions.</span></span>

1. <span data-ttu-id="cd0f1-333">[Configure databases](https://msdn.microsoft.com/library/hh213078.aspx) into availability groups.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-333">[Configure databases](https://msdn.microsoft.com/library/hh213078.aspx) into availability groups.</span></span>
2. <span data-ttu-id="cd0f1-334">Create a virtual network on the secondary site.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-334">Create a virtual network on the secondary site.</span></span>
3. <span data-ttu-id="cd0f1-335">Set up a site-to-site VPN connection between the virtual network, and the primary site.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-335">Set up a site-to-site VPN connection between the virtual network, and the primary site.</span></span>
4. <span data-ttu-id="cd0f1-336">Create a virtual machine on the recovery site, and install SQL Server on it.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-336">Create a virtual machine on the recovery site, and install SQL Server on it.</span></span>
5. <span data-ttu-id="cd0f1-337">Extend the existing AlwaysOn availability groups to the new SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-337">Extend the existing AlwaysOn availability groups to the new SQL Server VM.</span></span> <span data-ttu-id="cd0f1-338">Configure this SQL Server instance as an asynchronous replica copy.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-338">Configure this SQL Server instance as an asynchronous replica copy.</span></span>
6. <span data-ttu-id="cd0f1-339">Create an availability group listener, or update the existing listener to include the asynchronous replica virtual machine.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-339">Create an availability group listener, or update the existing listener to include the asynchronous replica virtual machine.</span></span>
7. <span data-ttu-id="cd0f1-340">Make sure that the application farm is set up using the listener.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-340">Make sure that the application farm is set up using the listener.</span></span> <span data-ttu-id="cd0f1-341">If it's setup up using the database server name, update it to use the listener, so you don't need to reconfigure it after the failover.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-341">If it's setup up using the database server name, update it to use the listener, so you don't need to reconfigure it after the failover.</span></span>

<span data-ttu-id="cd0f1-342">For applications that use distributed transactions, we recommend you deploy Site Recovery with [SAN replication](site-recovery-vmm-san.md), or [VMware/physical server site-to-site replication](site-recovery-vmware-to-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="cd0f1-342">For applications that use distributed transactions, we recommend you deploy Site Recovery with [SAN replication](site-recovery-vmm-san.md), or [VMware/physical server site-to-site replication](site-recovery-vmware-to-vmware.md).</span></span>

### <a name="recovery-plan-considerations"></a><span data-ttu-id="cd0f1-343">Recovery plan considerations</span><span class="sxs-lookup"><span data-stu-id="cd0f1-343">Recovery plan considerations</span></span>
1. <span data-ttu-id="cd0f1-344">Add this sample script to the VMM library, on the primary and secondary sites.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-344">Add this sample script to the VMM library, on the primary and secondary sites.</span></span>

        ``Param(
        [string]$SQLAvailabilityGroupPath
        )
        import-module sqlps
        Switch-SqlAvailabilityGroup -Path $SQLAvailabilityGroupPath -AllowDataLoss -force``
2. <span data-ttu-id="cd0f1-345">When you create a recovery plan for the application, add a "pre-Group 1 boot" scripted step, that invokes the script to fail over availability groups.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-345">When you create a recovery plan for the application, add a "pre-Group 1 boot" scripted step, that invokes the script to fail over availability groups.</span></span>

## <a name="protect-a-standalone-sql-server"></a><span data-ttu-id="cd0f1-346">Protect a standalone SQL Server</span><span class="sxs-lookup"><span data-stu-id="cd0f1-346">Protect a standalone SQL Server</span></span>

<span data-ttu-id="cd0f1-347">In this scenario, we recommend that you use Site Recovery replication to protect the SQL Server machine.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-347">In this scenario, we recommend that you use Site Recovery replication to protect the SQL Server machine.</span></span> <span data-ttu-id="cd0f1-348">The exact steps will depend whether SQL Server is a VM or a physical server, and whether you want to replicate to Azure or a secondary on-premises site.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-348">The exact steps will depend whether SQL Server is a VM or a physical server, and whether you want to replicate to Azure or a secondary on-premises site.</span></span> <span data-ttu-id="cd0f1-349">Learn about [Site Recovery scenarios](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cd0f1-349">Learn about [Site Recovery scenarios](site-recovery-overview.md).</span></span>

## <a name="protect-a-sql-server-cluster-standard-editionwindows-server-2008-r2"></a><span data-ttu-id="cd0f1-350">Protect a SQL Server cluster (standard edition/Windows Server 2008 R2)</span><span class="sxs-lookup"><span data-stu-id="cd0f1-350">Protect a SQL Server cluster (standard edition/Windows Server 2008 R2)</span></span>

<span data-ttu-id="cd0f1-351">For a cluster running SQL Server Standard edition, or SQL Server 2008 R2, we recommend you use Site Recovery replication to protect SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-351">For a cluster running SQL Server Standard edition, or SQL Server 2008 R2, we recommend you use Site Recovery replication to protect SQL Server.</span></span>

### <a name="on-premises-to-on-premises"></a><span data-ttu-id="cd0f1-352">On-premises to on-premises</span><span class="sxs-lookup"><span data-stu-id="cd0f1-352">On-premises to on-premises</span></span>

* <span data-ttu-id="cd0f1-353">If the app uses distributed transactions we recommend you deploy [Site Recovery with SAN replication](site-recovery-vmm-san.md) for a Hyper-V environment, or [VMware/physical server to VMware](site-recovery-vmware-to-vmware.md) for a VMware environment.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-353">If the app uses distributed transactions we recommend you deploy [Site Recovery with SAN replication](site-recovery-vmm-san.md) for a Hyper-V environment, or [VMware/physical server to VMware](site-recovery-vmware-to-vmware.md) for a VMware environment.</span></span>
* <span data-ttu-id="cd0f1-354">For non-DTC applications, use the above approach to recover the cluster as a standalone server, by leveraging a local high safety DB mirror.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-354">For non-DTC applications, use the above approach to recover the cluster as a standalone server, by leveraging a local high safety DB mirror.</span></span>

### <a name="on-premises-to-azure"></a><span data-ttu-id="cd0f1-355">On-premises to Azure</span><span class="sxs-lookup"><span data-stu-id="cd0f1-355">On-premises to Azure</span></span>

<span data-ttu-id="cd0f1-356">Site Recovery doesn't provide guest cluster support when replicating to Azure.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-356">Site Recovery doesn't provide guest cluster support when replicating to Azure.</span></span> <span data-ttu-id="cd0f1-357">SQL Server also doesn't provide a low-cost disaster recovery solution for Standard edition.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-357">SQL Server also doesn't provide a low-cost disaster recovery solution for Standard edition.</span></span> <span data-ttu-id="cd0f1-358">In this scenario, we recommend you protect the on-premises SQL Server cluster to a standalone SQL Server, and recover it in Azure.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-358">In this scenario, we recommend you protect the on-premises SQL Server cluster to a standalone SQL Server, and recover it in Azure.</span></span>

1. <span data-ttu-id="cd0f1-359">Configure an additional standalone SQL Server instance on the on-premises site.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-359">Configure an additional standalone SQL Server instance on the on-premises site.</span></span>
2. <span data-ttu-id="cd0f1-360">Configure the instance to serve as a mirror for the databases you want to protect.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-360">Configure the instance to serve as a mirror for the databases you want to protect.</span></span> <span data-ttu-id="cd0f1-361">Configure mirroring in high safety mode.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-361">Configure mirroring in high safety mode.</span></span>
3. <span data-ttu-id="cd0f1-362">Configure Site Recovery on the on-premises site, for ([Hyper-V](site-recovery-hyper-v-site-to-azure.md) or [VMware VMs/physical servers](site-recovery-vmware-to-azure-classic.md).</span><span class="sxs-lookup"><span data-stu-id="cd0f1-362">Configure Site Recovery on the on-premises site, for ([Hyper-V](site-recovery-hyper-v-site-to-azure.md) or [VMware VMs/physical servers](site-recovery-vmware-to-azure-classic.md).</span></span>
4. <span data-ttu-id="cd0f1-363">Use Site Recovery replication to replicate the new SQL Server instance to Azure.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-363">Use Site Recovery replication to replicate the new SQL Server instance to Azure.</span></span> <span data-ttu-id="cd0f1-364">Since it's a high safety mirror copy, it will be synchronized with the primary cluster, but it will be replicated to Azure using Site Recovery replication.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-364">Since it's a high safety mirror copy, it will be synchronized with the primary cluster, but it will be replicated to Azure using Site Recovery replication.</span></span>


![Standard cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-sql/BCDRStandaloneClusterLocal.png)

### <a name="failback-considerations"></a><span data-ttu-id="cd0f1-366">Failback considerations</span><span class="sxs-lookup"><span data-stu-id="cd0f1-366">Failback considerations</span></span>

<span data-ttu-id="cd0f1-367">For SQL Server Standard clusters, failback after an unplanned failover requires a SQL server backup and restore, from the mirror instance to the original cluster, with reestablishment of the mirror.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-367">For SQL Server Standard clusters, failback after an unplanned failover requires a SQL server backup and restore, from the mirror instance to the original cluster, with reestablishment of the mirror.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd0f1-368">Next steps</span><span class="sxs-lookup"><span data-stu-id="cd0f1-368">Next steps</span></span>
<span data-ttu-id="cd0f1-369">[Learn more](site-recovery-components.md) about Site Recovery architecture.</span><span class="sxs-lookup"><span data-stu-id="cd0f1-369">[Learn more](site-recovery-components.md) about Site Recovery architecture.</span></span>









