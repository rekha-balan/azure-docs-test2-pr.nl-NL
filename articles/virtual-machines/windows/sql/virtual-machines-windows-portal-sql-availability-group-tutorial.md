---
title: SQL Server Availability Groups - Azure Virtual Machines - Tutorial | Microsoft Docs
description: This tutorial shows how to create a SQL Server Always On Availability Group on Azure Virtual Machines.
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: craigg
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/30/2018
ms.author: mikeray
ms.openlocfilehash: 7dbbfb2d97b7015118edca3db3ae050ad07c51ee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44776275"
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a><span data-ttu-id="5ceb4-103">Configure Always On Availability Group in Azure VM manually</span><span class="sxs-lookup"><span data-stu-id="5ceb4-103">Configure Always On Availability Group in Azure VM manually</span></span>

<span data-ttu-id="5ceb4-104">This tutorial shows how to create a SQL Server Always On Availability Group on Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-104">This tutorial shows how to create a SQL Server Always On Availability Group on Azure Virtual Machines.</span></span> <span data-ttu-id="5ceb4-105">The complete tutorial creates an Availability Group with a database replica on two SQL Servers.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-105">The complete tutorial creates an Availability Group with a database replica on two SQL Servers.</span></span>

<span data-ttu-id="5ceb4-106">**Time estimate**: Takes about 30 minutes to complete once the prerequisites are met.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-106">**Time estimate**: Takes about 30 minutes to complete once the prerequisites are met.</span></span>

<span data-ttu-id="5ceb4-107">The diagram illustrates what you build in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-107">The diagram illustrates what you build in the tutorial.</span></span>

![Availability Group](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a><span data-ttu-id="5ceb4-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5ceb4-109">Prerequisites</span></span>

<span data-ttu-id="5ceb4-110">The tutorial assumes you have a basic understanding of SQL Server Always On Availability Groups.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-110">The tutorial assumes you have a basic understanding of SQL Server Always On Availability Groups.</span></span> <span data-ttu-id="5ceb4-111">If you need more information, see [Overview of Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ceb4-111">If you need more information, see [Overview of Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span></span>

<span data-ttu-id="5ceb4-112">The following table lists the prerequisites that you need to complete before starting this tutorial:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-112">The following table lists the prerequisites that you need to complete before starting this tutorial:</span></span>

|  |<span data-ttu-id="5ceb4-113">Requirement</span><span class="sxs-lookup"><span data-stu-id="5ceb4-113">Requirement</span></span> |<span data-ttu-id="5ceb4-114">Description</span><span class="sxs-lookup"><span data-stu-id="5ceb4-114">Description</span></span> |
|----- |----- |----- |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | <span data-ttu-id="5ceb4-116">Two SQL Servers</span><span class="sxs-lookup"><span data-stu-id="5ceb4-116">Two SQL Servers</span></span> | <span data-ttu-id="5ceb4-117">- In an Azure availability set</span><span class="sxs-lookup"><span data-stu-id="5ceb4-117">- In an Azure availability set</span></span> <br/> <span data-ttu-id="5ceb4-118">- In a single domain</span><span class="sxs-lookup"><span data-stu-id="5ceb4-118">- In a single domain</span></span> <br/> <span data-ttu-id="5ceb4-119">- With Failover Clustering feature installed</span><span class="sxs-lookup"><span data-stu-id="5ceb4-119">- With Failover Clustering feature installed</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| <span data-ttu-id="5ceb4-121">Windows Server</span><span class="sxs-lookup"><span data-stu-id="5ceb4-121">Windows Server</span></span> | <span data-ttu-id="5ceb4-122">File share for cluster witness</span><span class="sxs-lookup"><span data-stu-id="5ceb4-122">File share for cluster witness</span></span> |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="5ceb4-124">SQL Server service account</span><span class="sxs-lookup"><span data-stu-id="5ceb4-124">SQL Server service account</span></span> | <span data-ttu-id="5ceb4-125">Domain account</span><span class="sxs-lookup"><span data-stu-id="5ceb4-125">Domain account</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="5ceb4-127">SQL Server Agent service account</span><span class="sxs-lookup"><span data-stu-id="5ceb4-127">SQL Server Agent service account</span></span> | <span data-ttu-id="5ceb4-128">Domain account</span><span class="sxs-lookup"><span data-stu-id="5ceb4-128">Domain account</span></span> |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="5ceb4-130">Firewall ports open</span><span class="sxs-lookup"><span data-stu-id="5ceb4-130">Firewall ports open</span></span> | <span data-ttu-id="5ceb4-131">- SQL Server: **1433** for default instance</span><span class="sxs-lookup"><span data-stu-id="5ceb4-131">- SQL Server: **1433** for default instance</span></span> <br/> <span data-ttu-id="5ceb4-132">- Database mirroring endpoint: **5022** or any available port</span><span class="sxs-lookup"><span data-stu-id="5ceb4-132">- Database mirroring endpoint: **5022** or any available port</span></span> <br/> <span data-ttu-id="5ceb4-133">- Availability group load balancer IP address health probe: **59999** or any available port</span><span class="sxs-lookup"><span data-stu-id="5ceb4-133">- Availability group load balancer IP address health probe: **59999** or any available port</span></span> <br/> <span data-ttu-id="5ceb4-134">- Cluster core load balancer IP address health probe: **58888** or any available port</span><span class="sxs-lookup"><span data-stu-id="5ceb4-134">- Cluster core load balancer IP address health probe: **58888** or any available port</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="5ceb4-136">Add Failover Clustering Feature</span><span class="sxs-lookup"><span data-stu-id="5ceb4-136">Add Failover Clustering Feature</span></span> | <span data-ttu-id="5ceb4-137">Both SQL Servers require this feature</span><span class="sxs-lookup"><span data-stu-id="5ceb4-137">Both SQL Servers require this feature</span></span> |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="5ceb4-139">Installation domain account</span><span class="sxs-lookup"><span data-stu-id="5ceb4-139">Installation domain account</span></span> | <span data-ttu-id="5ceb4-140">- Local administrator on each SQL Server</span><span class="sxs-lookup"><span data-stu-id="5ceb4-140">- Local administrator on each SQL Server</span></span> <br/> <span data-ttu-id="5ceb4-141">- Member of SQL Server sysadmin fixed server role for each instance of SQL Server</span><span class="sxs-lookup"><span data-stu-id="5ceb4-141">- Member of SQL Server sysadmin fixed server role for each instance of SQL Server</span></span>  |


<span data-ttu-id="5ceb4-142">Before you begin the tutorial, you need to [Complete prerequisites for creating Always On Availability Groups in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span><span class="sxs-lookup"><span data-stu-id="5ceb4-142">Before you begin the tutorial, you need to [Complete prerequisites for creating Always On Availability Groups in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span></span> <span data-ttu-id="5ceb4-143">If these prerequisites are completed already, you can jump to [Create Cluster](#CreateCluster).</span><span class="sxs-lookup"><span data-stu-id="5ceb4-143">If these prerequisites are completed already, you can jump to [Create Cluster](#CreateCluster).</span></span>


<!--**Procedure**: *This is the first “step”. Make titles H2’s and short and clear – H2’s appear in the right pane on the web page and are important for navigation.*-->

<a name="CreateCluster"></a>
## <a name="create-the-cluster"></a><span data-ttu-id="5ceb4-144">Create the cluster</span><span class="sxs-lookup"><span data-stu-id="5ceb4-144">Create the cluster</span></span>

<span data-ttu-id="5ceb4-145">After the prerequisites are completed, the first step is to create a Windows Server Failover Cluster that includes two SQL Severs and a witness server.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-145">After the prerequisites are completed, the first step is to create a Windows Server Failover Cluster that includes two SQL Severs and a witness server.</span></span>

1. <span data-ttu-id="5ceb4-146">RDP to the first SQL Server using a domain account that is an administrator on both SQL Servers and the witness server.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-146">RDP to the first SQL Server using a domain account that is an administrator on both SQL Servers and the witness server.</span></span>

   >[!TIP]
   ><span data-ttu-id="5ceb4-147">If you followed the [prerequisites document](virtual-machines-windows-portal-sql-availability-group-prereq.md), you created an account called **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-147">If you followed the [prerequisites document](virtual-machines-windows-portal-sql-availability-group-prereq.md), you created an account called **CORP\Install**.</span></span> <span data-ttu-id="5ceb4-148">Use this account.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-148">Use this account.</span></span>

2. <span data-ttu-id="5ceb4-149">In the **Server Manager** dashboard, select **Tools**, and then click **Failover Cluster Manager**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-149">In the **Server Manager** dashboard, select **Tools**, and then click **Failover Cluster Manager**.</span></span>
3. <span data-ttu-id="5ceb4-150">In the left pane, right-click **Failover Cluster Manager**, and then click **Create a Cluster**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-150">In the left pane, right-click **Failover Cluster Manager**, and then click **Create a Cluster**.</span></span>
   <span data-ttu-id="5ceb4-151">![Create Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span><span class="sxs-lookup"><span data-stu-id="5ceb4-151">![Create Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span></span>
4. <span data-ttu-id="5ceb4-152">In the Create Cluster Wizard, create a one-node cluster by stepping through the pages with the settings in the following table:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-152">In the Create Cluster Wizard, create a one-node cluster by stepping through the pages with the settings in the following table:</span></span>

   | <span data-ttu-id="5ceb4-153">Page</span><span class="sxs-lookup"><span data-stu-id="5ceb4-153">Page</span></span> | <span data-ttu-id="5ceb4-154">Settings</span><span class="sxs-lookup"><span data-stu-id="5ceb4-154">Settings</span></span> |
   | --- | --- |
   | <span data-ttu-id="5ceb4-155">Before You Begin</span><span class="sxs-lookup"><span data-stu-id="5ceb4-155">Before You Begin</span></span> |<span data-ttu-id="5ceb4-156">Use defaults</span><span class="sxs-lookup"><span data-stu-id="5ceb4-156">Use defaults</span></span> |
   | <span data-ttu-id="5ceb4-157">Select Servers</span><span class="sxs-lookup"><span data-stu-id="5ceb4-157">Select Servers</span></span> |<span data-ttu-id="5ceb4-158">Type the first SQL Server name in **Enter server name** and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-158">Type the first SQL Server name in **Enter server name** and click **Add**.</span></span> |
   | <span data-ttu-id="5ceb4-159">Validation Warning</span><span class="sxs-lookup"><span data-stu-id="5ceb4-159">Validation Warning</span></span> |<span data-ttu-id="5ceb4-160">Select **No. I do not require support from Microsoft for this cluster, and therefore do not want to run the validation tests. When I click Next, continue Creating the cluster**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-160">Select **No. I do not require support from Microsoft for this cluster, and therefore do not want to run the validation tests. When I click Next, continue Creating the cluster**.</span></span> |
   | <span data-ttu-id="5ceb4-161">Access Point for Administering the Cluster</span><span class="sxs-lookup"><span data-stu-id="5ceb4-161">Access Point for Administering the Cluster</span></span> |<span data-ttu-id="5ceb4-162">Type a cluster name, for example **SQLAGCluster1** in **Cluster Name**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-162">Type a cluster name, for example **SQLAGCluster1** in **Cluster Name**.</span></span>|
   | <span data-ttu-id="5ceb4-163">Confirmation</span><span class="sxs-lookup"><span data-stu-id="5ceb4-163">Confirmation</span></span> |<span data-ttu-id="5ceb4-164">Use defaults unless you are using Storage Spaces.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-164">Use defaults unless you are using Storage Spaces.</span></span> <span data-ttu-id="5ceb4-165">See the note following this table.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-165">See the note following this table.</span></span> |

### <a name="set-the-windows-server-failover-cluster-ip-address"></a><span data-ttu-id="5ceb4-166">Set the Windows server failover cluster IP address</span><span class="sxs-lookup"><span data-stu-id="5ceb4-166">Set the Windows server failover cluster IP address</span></span>

1. <span data-ttu-id="5ceb4-167">In **Failover Cluster Manager**, scroll down to **Cluster Core Resources** and expand the cluster details.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-167">In **Failover Cluster Manager**, scroll down to **Cluster Core Resources** and expand the cluster details.</span></span> <span data-ttu-id="5ceb4-168">You should see both the **Name** and the **IP Address** resources in the **Failed** state.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-168">You should see both the **Name** and the **IP Address** resources in the **Failed** state.</span></span> <span data-ttu-id="5ceb4-169">The IP address resource cannot be brought online because the cluster is assigned the same IP address as the machine itself, therefore it is a duplicate address.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-169">The IP address resource cannot be brought online because the cluster is assigned the same IP address as the machine itself, therefore it is a duplicate address.</span></span>

2. <span data-ttu-id="5ceb4-170">Right-click the failed **IP Address** resource, and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-170">Right-click the failed **IP Address** resource, and then click **Properties**.</span></span>

   ![Cluster Properties](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. <span data-ttu-id="5ceb4-172">Select **Static IP Address** and specify an available address from the same subnet as your virtual machines.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-172">Select **Static IP Address** and specify an available address from the same subnet as your virtual machines.</span></span>

4. <span data-ttu-id="5ceb4-173">In the **Cluster Core Resources** section, right-click cluster name and click **Bring Online**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-173">In the **Cluster Core Resources** section, right-click cluster name and click **Bring Online**.</span></span> <span data-ttu-id="5ceb4-174">Then, wait until both resources are online.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-174">Then, wait until both resources are online.</span></span> <span data-ttu-id="5ceb4-175">When the cluster name resource comes online, it updates the DC server with a new AD computer account.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-175">When the cluster name resource comes online, it updates the DC server with a new AD computer account.</span></span> <span data-ttu-id="5ceb4-176">Use this AD account to run the Availability Group clustered service later.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-176">Use this AD account to run the Availability Group clustered service later.</span></span>

### <a name="addNode"></a><span data-ttu-id="5ceb4-177">Add the other SQL Server to cluster</span><span class="sxs-lookup"><span data-stu-id="5ceb4-177">Add the other SQL Server to cluster</span></span>

<span data-ttu-id="5ceb4-178">Add the other SQL Server to the cluster.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-178">Add the other SQL Server to the cluster.</span></span>

1. <span data-ttu-id="5ceb4-179">In the browser tree, right-click the cluster and click **Add Node**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-179">In the browser tree, right-click the cluster and click **Add Node**.</span></span>

    ![Add Node to the Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. <span data-ttu-id="5ceb4-181">In the **Add Node Wizard**, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-181">In the **Add Node Wizard**, click **Next**.</span></span> <span data-ttu-id="5ceb4-182">In the **Select Servers** page, add the second SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-182">In the **Select Servers** page, add the second SQL Server.</span></span> <span data-ttu-id="5ceb4-183">Type the server name in **Enter server name** and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-183">Type the server name in **Enter server name** and then click **Add**.</span></span> <span data-ttu-id="5ceb4-184">When you are done, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-184">When you are done, click **Next**.</span></span>

1. <span data-ttu-id="5ceb4-185">In the **Validation Warning** page, click **No** (in a production scenario you should perform the validation tests).</span><span class="sxs-lookup"><span data-stu-id="5ceb4-185">In the **Validation Warning** page, click **No** (in a production scenario you should perform the validation tests).</span></span> <span data-ttu-id="5ceb4-186">Then, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-186">Then, click **Next**.</span></span>

8. <span data-ttu-id="5ceb4-187">In the **Confirmation** page if you are using Storage Spaces, clear the checkbox labeled **Add all eligible storage to the cluster.**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-187">In the **Confirmation** page if you are using Storage Spaces, clear the checkbox labeled **Add all eligible storage to the cluster.**</span></span>

   ![Add Node Confirmation](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   ><span data-ttu-id="5ceb4-189">If you are using Storage Spaces and do not uncheck **Add all eligible storage to the cluster**, Windows detaches the virtual disks during the clustering process.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-189">If you are using Storage Spaces and do not uncheck **Add all eligible storage to the cluster**, Windows detaches the virtual disks during the clustering process.</span></span> <span data-ttu-id="5ceb4-190">As a result, they do not appear in Disk Manager or Explorer until the storage spaces are removed from the cluster and reattached using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-190">As a result, they do not appear in Disk Manager or Explorer until the storage spaces are removed from the cluster and reattached using PowerShell.</span></span> <span data-ttu-id="5ceb4-191">Storage Spaces groups multiple disks in to storage pools.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-191">Storage Spaces groups multiple disks in to storage pools.</span></span> <span data-ttu-id="5ceb4-192">For more information, see [Storage Spaces](https://technet.microsoft.com/library/hh831739).</span><span class="sxs-lookup"><span data-stu-id="5ceb4-192">For more information, see [Storage Spaces](https://technet.microsoft.com/library/hh831739).</span></span>

1. <span data-ttu-id="5ceb4-193">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-193">Click **Next**.</span></span>

1. <span data-ttu-id="5ceb4-194">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-194">Click **Finish**.</span></span>

   <span data-ttu-id="5ceb4-195">Failover Cluster Manager shows that your cluster has a new node and lists it in the **Nodes** container.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-195">Failover Cluster Manager shows that your cluster has a new node and lists it in the **Nodes** container.</span></span>

10. <span data-ttu-id="5ceb4-196">Log out of the remote desktop session.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-196">Log out of the remote desktop session.</span></span>

### <a name="add-a-cluster-quorum-file-share"></a><span data-ttu-id="5ceb4-197">Add a cluster quorum file share</span><span class="sxs-lookup"><span data-stu-id="5ceb4-197">Add a cluster quorum file share</span></span>

<span data-ttu-id="5ceb4-198">In this example the Windows cluster uses a file share to create a cluster quorum.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-198">In this example the Windows cluster uses a file share to create a cluster quorum.</span></span> <span data-ttu-id="5ceb4-199">This tutorial uses a Node and File Share Majority quorum.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-199">This tutorial uses a Node and File Share Majority quorum.</span></span> <span data-ttu-id="5ceb4-200">For more information, see [Understanding Quorum Configurations in a Failover Cluster](http://technet.microsoft.com/library/cc731739.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ceb4-200">For more information, see [Understanding Quorum Configurations in a Failover Cluster](http://technet.microsoft.com/library/cc731739.aspx).</span></span>

1. <span data-ttu-id="5ceb4-201">Connect to the file share witness member server with a remote desktop session.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-201">Connect to the file share witness member server with a remote desktop session.</span></span>

1. <span data-ttu-id="5ceb4-202">On **Server Manager**, click **Tools**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-202">On **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="5ceb4-203">Open **Computer Management**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-203">Open **Computer Management**.</span></span>

1. <span data-ttu-id="5ceb4-204">Click **Shared Folders**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-204">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="5ceb4-205">Right-click **Shares**, and click **New Share...**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-205">Right-click **Shares**, and click **New Share...**.</span></span>

   ![New Share](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="5ceb4-207">Use **Create a Shared Folder Wizard** to create a share.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-207">Use **Create a Shared Folder Wizard** to create a share.</span></span>

1. <span data-ttu-id="5ceb4-208">On **Folder Path**, click **Browse** and locate or create a path for the shared folder.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-208">On **Folder Path**, click **Browse** and locate or create a path for the shared folder.</span></span> <span data-ttu-id="5ceb4-209">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-209">Click **Next**.</span></span>

1. <span data-ttu-id="5ceb4-210">In **Name, Description, and Settings** verify the share name and path.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-210">In **Name, Description, and Settings** verify the share name and path.</span></span> <span data-ttu-id="5ceb4-211">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-211">Click **Next**.</span></span>

1. <span data-ttu-id="5ceb4-212">On **Shared Folder Permissions** set **Customize permissions**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-212">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="5ceb4-213">Click **Custom...**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-213">Click **Custom...**.</span></span>

1. <span data-ttu-id="5ceb4-214">On **Customize Permissions**, click **Add...**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-214">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="5ceb4-215">Make sure that the account used to create the cluster has full control.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-215">Make sure that the account used to create the cluster has full control.</span></span>

   ![New Share](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. <span data-ttu-id="5ceb4-217">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-217">Click **OK**.</span></span>

1. <span data-ttu-id="5ceb4-218">In **Shared Folder Permissions**, click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-218">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="5ceb4-219">Click **Finish** again.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-219">Click **Finish** again.</span></span>  

1. <span data-ttu-id="5ceb4-220">Log out of the server</span><span class="sxs-lookup"><span data-stu-id="5ceb4-220">Log out of the server</span></span>

### <a name="configure-cluster-quorum"></a><span data-ttu-id="5ceb4-221">Configure cluster quorum</span><span class="sxs-lookup"><span data-stu-id="5ceb4-221">Configure cluster quorum</span></span>

<span data-ttu-id="5ceb4-222">Next, set the cluster quorum.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-222">Next, set the cluster quorum.</span></span>

1. <span data-ttu-id="5ceb4-223">Connect to the first cluster node with remote desktop.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-223">Connect to the first cluster node with remote desktop.</span></span>

1. <span data-ttu-id="5ceb4-224">In **Failover Cluster Manager**, right-click the cluster, point to **More Actions**, and click **Configure Cluster Quorum Settings...**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-224">In **Failover Cluster Manager**, right-click the cluster, point to **More Actions**, and click **Configure Cluster Quorum Settings...**.</span></span>

   ![New Share](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. <span data-ttu-id="5ceb4-226">In **Configure Cluster Quorum Wizard**, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-226">In **Configure Cluster Quorum Wizard**, click **Next**.</span></span>

1. <span data-ttu-id="5ceb4-227">In **Select Quorum Configuration Option**, choose **Select the quorum witness**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-227">In **Select Quorum Configuration Option**, choose **Select the quorum witness**, and click **Next**.</span></span>

1. <span data-ttu-id="5ceb4-228">On **Select Quorum Witness**, click **Configure a file share witness**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-228">On **Select Quorum Witness**, click **Configure a file share witness**.</span></span>

   >[!TIP]
   ><span data-ttu-id="5ceb4-229">Windows Server 2016 supports a cloud witness.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-229">Windows Server 2016 supports a cloud witness.</span></span> <span data-ttu-id="5ceb4-230">If you choose this type of witness, you do not need a file share witness.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-230">If you choose this type of witness, you do not need a file share witness.</span></span> <span data-ttu-id="5ceb4-231">For more information, see [Deploy a cloud witness for a Failover Cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="5ceb4-231">For more information, see [Deploy a cloud witness for a Failover Cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span> <span data-ttu-id="5ceb4-232">This tutorial uses a file share witness, which is supported by previous operating systems.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-232">This tutorial uses a file share witness, which is supported by previous operating systems.</span></span>

1. <span data-ttu-id="5ceb4-233">On **Configure File Share Witness**, type the path for the share you created.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-233">On **Configure File Share Witness**, type the path for the share you created.</span></span> <span data-ttu-id="5ceb4-234">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-234">Click **Next**.</span></span>

1. <span data-ttu-id="5ceb4-235">Verify the settings on **Confirmation**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-235">Verify the settings on **Confirmation**.</span></span> <span data-ttu-id="5ceb4-236">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-236">Click **Next**.</span></span>

1. <span data-ttu-id="5ceb4-237">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-237">Click **Finish**.</span></span>

<span data-ttu-id="5ceb4-238">The cluster core resources are configured with a file share witness.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-238">The cluster core resources are configured with a file share witness.</span></span>

## <a name="enable-availability-groups"></a><span data-ttu-id="5ceb4-239">Enable Availability Groups</span><span class="sxs-lookup"><span data-stu-id="5ceb4-239">Enable Availability Groups</span></span>

<span data-ttu-id="5ceb4-240">Next, enable the **AlwaysOn Availability Groups** feature.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-240">Next, enable the **AlwaysOn Availability Groups** feature.</span></span> <span data-ttu-id="5ceb4-241">Do these steps on both SQL Servers.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-241">Do these steps on both SQL Servers.</span></span>

1. <span data-ttu-id="5ceb4-242">From the **Start** screen, launch **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-242">From the **Start** screen, launch **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="5ceb4-243">In the browser tree, click **SQL Server Services**, then right-click the **SQL Server (MSSQLSERVER)** service and click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-243">In the browser tree, click **SQL Server Services**, then right-click the **SQL Server (MSSQLSERVER)** service and click **Properties**.</span></span>
3. <span data-ttu-id="5ceb4-244">Click the **AlwaysOn High Availability** tab, then select **Enable AlwaysOn Availability Groups**, as follows:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-244">Click the **AlwaysOn High Availability** tab, then select **Enable AlwaysOn Availability Groups**, as follows:</span></span>

    ![Enable AlwaysOn Availability Groups](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. <span data-ttu-id="5ceb4-246">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-246">Click **Apply**.</span></span> <span data-ttu-id="5ceb4-247">Click **OK** in the pop-up dialog.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-247">Click **OK** in the pop-up dialog.</span></span>

5. <span data-ttu-id="5ceb4-248">Restart the SQL Server service.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-248">Restart the SQL Server service.</span></span>

<span data-ttu-id="5ceb4-249">Repeat these steps on the other SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-249">Repeat these steps on the other SQL Server.</span></span>

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for the database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for the instance of SQL Server that is used to synchronize the database replicas in the Availability Groups on that instance.

On both SQL Servers, open the firewall for the TCP port for the database mirroring endpoint.

1. On the first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In the left pane, select **Inbound Rules**. On the right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For the port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In the **Action** page, keep **Allow the connection** selected and click **Next**.
6. In the **Profile** page, accept the default settings and click **Next**.
7. In the **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in the **Name** text box, then click **Finish**.

Repeat these steps on the second SQL Server.
-------------------------->

## <a name="create-a-database-on-the-first-sql-server"></a><span data-ttu-id="5ceb4-250">Create a database on the first SQL Server</span><span class="sxs-lookup"><span data-stu-id="5ceb4-250">Create a database on the first SQL Server</span></span>

1. <span data-ttu-id="5ceb4-251">Launch the RDP file to the first SQL Server with a domain account that is a member of sysadmin fixed server role.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-251">Launch the RDP file to the first SQL Server with a domain account that is a member of sysadmin fixed server role.</span></span>
1. <span data-ttu-id="5ceb4-252">Open SQL Server Management Studio and connect to the first SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-252">Open SQL Server Management Studio and connect to the first SQL Server.</span></span>
7. <span data-ttu-id="5ceb4-253">In **Object Explorer**, right-click **Databases** and click **New Database**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-253">In **Object Explorer**, right-click **Databases** and click **New Database**.</span></span>
8. <span data-ttu-id="5ceb4-254">In **Database name**, type **MyDB1**, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-254">In **Database name**, type **MyDB1**, then click **OK**.</span></span>

### <a name="backupshare"></a> <span data-ttu-id="5ceb4-255">Create a backup share</span><span class="sxs-lookup"><span data-stu-id="5ceb4-255">Create a backup share</span></span>

1. <span data-ttu-id="5ceb4-256">On the first SQL Server in **Server Manager**, click **Tools**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-256">On the first SQL Server in **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="5ceb4-257">Open **Computer Management**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-257">Open **Computer Management**.</span></span>

1. <span data-ttu-id="5ceb4-258">Click **Shared Folders**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-258">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="5ceb4-259">Right-click **Shares**, and click **New Share...**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-259">Right-click **Shares**, and click **New Share...**.</span></span>

   ![New Share](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="5ceb4-261">Use **Create a Shared Folder Wizard** to create a share.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-261">Use **Create a Shared Folder Wizard** to create a share.</span></span>

1. <span data-ttu-id="5ceb4-262">On **Folder Path**, click **Browse** and locate or create a path for the database backup shared folder.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-262">On **Folder Path**, click **Browse** and locate or create a path for the database backup shared folder.</span></span> <span data-ttu-id="5ceb4-263">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-263">Click **Next**.</span></span>

1. <span data-ttu-id="5ceb4-264">In **Name, Description, and Settings** verify the share name and path.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-264">In **Name, Description, and Settings** verify the share name and path.</span></span> <span data-ttu-id="5ceb4-265">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-265">Click **Next**.</span></span>

1. <span data-ttu-id="5ceb4-266">On **Shared Folder Permissions** set **Customize permissions**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-266">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="5ceb4-267">Click **Custom...**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-267">Click **Custom...**.</span></span>

1. <span data-ttu-id="5ceb4-268">On **Customize Permissions**, click **Add...**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-268">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="5ceb4-269">Make sure that the SQL Server and SQL Server Agent service accounts for both servers have full control.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-269">Make sure that the SQL Server and SQL Server Agent service accounts for both servers have full control.</span></span>

   ![New Share](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. <span data-ttu-id="5ceb4-271">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-271">Click **OK**.</span></span>

1. <span data-ttu-id="5ceb4-272">In **Shared Folder Permissions**, click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-272">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="5ceb4-273">Click **Finish** again.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-273">Click **Finish** again.</span></span>  

### <a name="take-a-full-backup-of-the-database"></a><span data-ttu-id="5ceb4-274">Take a full backup of the database</span><span class="sxs-lookup"><span data-stu-id="5ceb4-274">Take a full backup of the database</span></span>

<span data-ttu-id="5ceb4-275">You need to back up the new database to initialize the log chain.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-275">You need to back up the new database to initialize the log chain.</span></span> <span data-ttu-id="5ceb4-276">If you do not take a backup of the new database, it cannot be included in an Availability Group.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-276">If you do not take a backup of the new database, it cannot be included in an Availability Group.</span></span>

1. <span data-ttu-id="5ceb4-277">In **Object Explorer**, right-click the database, point to **Tasks...**, click **Back Up**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-277">In **Object Explorer**, right-click the database, point to **Tasks...**, click **Back Up**.</span></span>

1. <span data-ttu-id="5ceb4-278">Click **OK** to take a full backup to the default backup location.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-278">Click **OK** to take a full backup to the default backup location.</span></span>

## <a name="create-the-availability-group"></a><span data-ttu-id="5ceb4-279">Create the Availability Group</span><span class="sxs-lookup"><span data-stu-id="5ceb4-279">Create the Availability Group</span></span>
<span data-ttu-id="5ceb4-280">You are now ready to configure an Availability Group using the following steps:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-280">You are now ready to configure an Availability Group using the following steps:</span></span>

* <span data-ttu-id="5ceb4-281">Create a database on the first SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-281">Create a database on the first SQL Server.</span></span>
* <span data-ttu-id="5ceb4-282">Take both a full backup and a transaction log backup of the database</span><span class="sxs-lookup"><span data-stu-id="5ceb4-282">Take both a full backup and a transaction log backup of the database</span></span>
* <span data-ttu-id="5ceb4-283">Restore the full and log backups to the second SQL Server with the **NORECOVERY** option</span><span class="sxs-lookup"><span data-stu-id="5ceb4-283">Restore the full and log backups to the second SQL Server with the **NORECOVERY** option</span></span>
* <span data-ttu-id="5ceb4-284">Create the Availability Group (**AG1**) with synchronous commit, automatic failover, and readable secondary replicas</span><span class="sxs-lookup"><span data-stu-id="5ceb4-284">Create the Availability Group (**AG1**) with synchronous commit, automatic failover, and readable secondary replicas</span></span>

### <a name="create-the-availability-group"></a><span data-ttu-id="5ceb4-285">Create the Availability Group:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-285">Create the Availability Group:</span></span>

1. <span data-ttu-id="5ceb4-286">On remote desktop session to the first SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-286">On remote desktop session to the first SQL Server.</span></span> <span data-ttu-id="5ceb4-287">In **Object Explorer** in SSMS, right-click **AlwaysOn High Availability** and click **New Availability Group Wizard**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-287">In **Object Explorer** in SSMS, right-click **AlwaysOn High Availability** and click **New Availability Group Wizard**.</span></span>

    ![Launch New Availability Group Wizard](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. <span data-ttu-id="5ceb4-289">In the **Introduction** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-289">In the **Introduction** page, click **Next**.</span></span> <span data-ttu-id="5ceb4-290">In the **Specify Availability Group Name** page, type a name for the Availability Group, for example **AG1**, in **Availability group name**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-290">In the **Specify Availability Group Name** page, type a name for the Availability Group, for example **AG1**, in **Availability group name**.</span></span> <span data-ttu-id="5ceb4-291">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-291">Click **Next**.</span></span>

    ![New AG Wizard, Specify AG Name](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. <span data-ttu-id="5ceb4-293">In the **Select Databases** page, select your database and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-293">In the **Select Databases** page, select your database and click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="5ceb4-294">The database meets the prerequisites for an Availability Group because you have taken at least one full backup on the intended primary replica.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-294">The database meets the prerequisites for an Availability Group because you have taken at least one full backup on the intended primary replica.</span></span>

   ![New AG Wizard, Select Databases](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. <span data-ttu-id="5ceb4-296">In the **Specify Replicas** page, click **Add Replica**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-296">In the **Specify Replicas** page, click **Add Replica**.</span></span>

   ![New AG Wizard, Specify Replicas](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. <span data-ttu-id="5ceb4-298">The **Connect to Server** dialog pops up.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-298">The **Connect to Server** dialog pops up.</span></span> <span data-ttu-id="5ceb4-299">Type the name of the second server in **Server name**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-299">Type the name of the second server in **Server name**.</span></span> <span data-ttu-id="5ceb4-300">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-300">Click **Connect**.</span></span>

   <span data-ttu-id="5ceb4-301">Back in the **Specify Replicas** page, you should now see the second server listed in **Availability Replicas**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-301">Back in the **Specify Replicas** page, you should now see the second server listed in **Availability Replicas**.</span></span> <span data-ttu-id="5ceb4-302">Configure the replicas as follows.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-302">Configure the replicas as follows.</span></span>

   ![New AG Wizard, Specify Replicas (Complete)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. <span data-ttu-id="5ceb4-304">Click **Endpoints** to see the database mirroring endpoint for this Availability Group.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-304">Click **Endpoints** to see the database mirroring endpoint for this Availability Group.</span></span> <span data-ttu-id="5ceb4-305">Use the same port that you used when you set the [firewall rule for database mirroring endpoints](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="5ceb4-305">Use the same port that you used when you set the [firewall rule for database mirroring endpoints](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

    ![New AG Wizard, Select Initial Data Synchronization](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. <span data-ttu-id="5ceb4-307">In the **Select Initial Data Synchronization** page, select **Full** and specify a shared network location.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-307">In the **Select Initial Data Synchronization** page, select **Full** and specify a shared network location.</span></span> <span data-ttu-id="5ceb4-308">For the location, use the [backup share that you created](#backupshare).</span><span class="sxs-lookup"><span data-stu-id="5ceb4-308">For the location, use the [backup share that you created](#backupshare).</span></span> <span data-ttu-id="5ceb4-309">In the example it was, \**\\\\\<First SQL Server\>\Backup\**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-309">In the example it was, \**\\\\\<First SQL Server\>\Backup\**.</span></span> <span data-ttu-id="5ceb4-310">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-310">Click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="5ceb4-311">Full synchronization takes a full backup of the database on the first instance of SQL Server and restores it to the second instance.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-311">Full synchronization takes a full backup of the database on the first instance of SQL Server and restores it to the second instance.</span></span> <span data-ttu-id="5ceb4-312">For large databases, full synchronization is not recommended because it may take a long time.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-312">For large databases, full synchronization is not recommended because it may take a long time.</span></span> <span data-ttu-id="5ceb4-313">You can reduce this time by manually taking a backup of the database and restoring it with `NO RECOVERY`.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-313">You can reduce this time by manually taking a backup of the database and restoring it with `NO RECOVERY`.</span></span> <span data-ttu-id="5ceb4-314">If the database is already restored with `NO RECOVERY` on the second SQL Server before configuring the Availability Group, choose **Join only**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-314">If the database is already restored with `NO RECOVERY` on the second SQL Server before configuring the Availability Group, choose **Join only**.</span></span> <span data-ttu-id="5ceb4-315">If you want to take the backup after configuring the Availability Group, choose **Skip initial data synchronization**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-315">If you want to take the backup after configuring the Availability Group, choose **Skip initial data synchronization**.</span></span>

    ![New AG Wizard, Select Initial Data Synchronization](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. <span data-ttu-id="5ceb4-317">In the **Validation** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-317">In the **Validation** page, click **Next**.</span></span> <span data-ttu-id="5ceb4-318">This page should look similar to the following image:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-318">This page should look similar to the following image:</span></span>

    ![New AG Wizard, Validation](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    ><span data-ttu-id="5ceb4-320">There is a warning for the listener configuration because you have not configured an Availability Group listener.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-320">There is a warning for the listener configuration because you have not configured an Availability Group listener.</span></span> <span data-ttu-id="5ceb4-321">You can ignore this warning because on Azure virtual machines you create the listener after creating the Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-321">You can ignore this warning because on Azure virtual machines you create the listener after creating the Azure load balancer.</span></span>

10. <span data-ttu-id="5ceb4-322">In the **Summary** page, click **Finish**, then wait while the wizard configures the new Availability Group.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-322">In the **Summary** page, click **Finish**, then wait while the wizard configures the new Availability Group.</span></span> <span data-ttu-id="5ceb4-323">In the **Progress** page, you can click **More details** to view the detailed progress.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-323">In the **Progress** page, you can click **More details** to view the detailed progress.</span></span> <span data-ttu-id="5ceb4-324">Once the wizard is finished, inspect the **Results** page to verify that the Availability Group is successfully created.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-324">Once the wizard is finished, inspect the **Results** page to verify that the Availability Group is successfully created.</span></span>

     ![New AG Wizard, Results](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. <span data-ttu-id="5ceb4-326">Click **Close** to exit the wizard.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-326">Click **Close** to exit the wizard.</span></span>

### <a name="check-the-availability-group"></a><span data-ttu-id="5ceb4-327">Check the Availability Group</span><span class="sxs-lookup"><span data-stu-id="5ceb4-327">Check the Availability Group</span></span>

1. <span data-ttu-id="5ceb4-328">In **Object Explorer**, expand **AlwaysOn High Availability**, then expand **Availability Groups**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-328">In **Object Explorer**, expand **AlwaysOn High Availability**, then expand **Availability Groups**.</span></span> <span data-ttu-id="5ceb4-329">You should now see the new Availability Group in this container.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-329">You should now see the new Availability Group in this container.</span></span> <span data-ttu-id="5ceb4-330">Right-click the Availability Group and click **Show Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-330">Right-click the Availability Group and click **Show Dashboard**.</span></span>

   ![Show AG Dashboard](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   <span data-ttu-id="5ceb4-332">Your **AlwaysOn Dashboard** should look similar to this.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-332">Your **AlwaysOn Dashboard** should look similar to this.</span></span>

   ![AG Dashboard](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   <span data-ttu-id="5ceb4-334">You can see the replicas, the failover mode of each replica and the synchronization state.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-334">You can see the replicas, the failover mode of each replica and the synchronization state.</span></span>

2. <span data-ttu-id="5ceb4-335">In **Failover Cluster Manager**, click your cluster.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-335">In **Failover Cluster Manager**, click your cluster.</span></span> <span data-ttu-id="5ceb4-336">Select **Roles**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-336">Select **Roles**.</span></span> <span data-ttu-id="5ceb4-337">The Availability Group name you used is a role on the cluster.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-337">The Availability Group name you used is a role on the cluster.</span></span> <span data-ttu-id="5ceb4-338">That Availability Group does not have an IP address for client connections, because you did not configure a listener.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-338">That Availability Group does not have an IP address for client connections, because you did not configure a listener.</span></span> <span data-ttu-id="5ceb4-339">You will configure the listener after you create an Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-339">You will configure the listener after you create an Azure load balancer.</span></span>

   ![AG in Failover Cluster Manager](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > <span data-ttu-id="5ceb4-341">Do not try to fail over the Availability Group from the Failover Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-341">Do not try to fail over the Availability Group from the Failover Cluster Manager.</span></span> <span data-ttu-id="5ceb4-342">All failover operations should be performed from within **AlwaysOn Dashboard** in SSMS.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-342">All failover operations should be performed from within **AlwaysOn Dashboard** in SSMS.</span></span> <span data-ttu-id="5ceb4-343">For more information, see [Restrictions on Using The Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ceb4-343">For more information, see [Restrictions on Using The Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx).</span></span>
    >

<span data-ttu-id="5ceb4-344">At this point, you have an Availability Group with replicas on two instances of SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-344">At this point, you have an Availability Group with replicas on two instances of SQL Server.</span></span> <span data-ttu-id="5ceb4-345">You can move the Availability Group between instances.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-345">You can move the Availability Group between instances.</span></span> <span data-ttu-id="5ceb4-346">You cannot connect to the Availability Group yet because you do not have a listener.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-346">You cannot connect to the Availability Group yet because you do not have a listener.</span></span> <span data-ttu-id="5ceb4-347">In Azure virtual machines, the listener requires a load balancer.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-347">In Azure virtual machines, the listener requires a load balancer.</span></span> <span data-ttu-id="5ceb4-348">The next step is to create the load balancer in Azure.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-348">The next step is to create the load balancer in Azure.</span></span>

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a><span data-ttu-id="5ceb4-349">Create an Azure load balancer</span><span class="sxs-lookup"><span data-stu-id="5ceb4-349">Create an Azure load balancer</span></span>

<span data-ttu-id="5ceb4-350">On Azure virtual machines, a SQL Server Availability Group requires a load balancer.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-350">On Azure virtual machines, a SQL Server Availability Group requires a load balancer.</span></span> <span data-ttu-id="5ceb4-351">The load balancer holds the IP addresses for the Availability Group listeners and the Windows Server Failover Cluster.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-351">The load balancer holds the IP addresses for the Availability Group listeners and the Windows Server Failover Cluster.</span></span> <span data-ttu-id="5ceb4-352">This section summarizes how to create the load balancer in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-352">This section summarizes how to create the load balancer in the Azure portal.</span></span>

<span data-ttu-id="5ceb4-353">An Azure Load Balancer can be either a Standard Load Balancer or a Basic Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-353">An Azure Load Balancer can be either a Standard Load Balancer or a Basic Load Balancer.</span></span> <span data-ttu-id="5ceb4-354">Standard Load Balancer has more features than the Basic Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-354">Standard Load Balancer has more features than the Basic Load Balancer.</span></span> <span data-ttu-id="5ceb4-355">For an availability group, the Standard Load Balancer is required if you use an Availability Zone (instead of an Availability Set).</span><span class="sxs-lookup"><span data-stu-id="5ceb4-355">For an availability group, the Standard Load Balancer is required if you use an Availability Zone (instead of an Availability Set).</span></span> <span data-ttu-id="5ceb4-356">For details on the difference between the load balancer types, see [Load Balancer SKU comparison](../../../load-balancer/load-balancer-overview.md#skus).</span><span class="sxs-lookup"><span data-stu-id="5ceb4-356">For details on the difference between the load balancer types, see [Load Balancer SKU comparison](../../../load-balancer/load-balancer-overview.md#skus).</span></span>

1. <span data-ttu-id="5ceb4-357">In the Azure portal, go to the resource group where your SQL Servers are and click **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-357">In the Azure portal, go to the resource group where your SQL Servers are and click **+ Add**.</span></span>
1. <span data-ttu-id="5ceb4-358">Search for **Load Balancer**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-358">Search for **Load Balancer**.</span></span> <span data-ttu-id="5ceb4-359">Choose the load balancer published by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-359">Choose the load balancer published by Microsoft.</span></span>

   ![AG in Failover Cluster Manager](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1. <span data-ttu-id="5ceb4-361">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-361">Click **Create**.</span></span>
1. <span data-ttu-id="5ceb4-362">Configure the following parameters for the load balancer.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-362">Configure the following parameters for the load balancer.</span></span>

   | <span data-ttu-id="5ceb4-363">Setting</span><span class="sxs-lookup"><span data-stu-id="5ceb4-363">Setting</span></span> | <span data-ttu-id="5ceb4-364">Field</span><span class="sxs-lookup"><span data-stu-id="5ceb4-364">Field</span></span> |
   | --- | --- |
   | <span data-ttu-id="5ceb4-365">**Name**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-365">**Name**</span></span> |<span data-ttu-id="5ceb4-366">Use a text name for the load balancer, for example **sqlLB**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-366">Use a text name for the load balancer, for example **sqlLB**.</span></span> |
   | <span data-ttu-id="5ceb4-367">**Type**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-367">**Type**</span></span> |<span data-ttu-id="5ceb4-368">Internal</span><span class="sxs-lookup"><span data-stu-id="5ceb4-368">Internal</span></span> |
   | <span data-ttu-id="5ceb4-369">**Virtual network**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-369">**Virtual network**</span></span> |<span data-ttu-id="5ceb4-370">Use the name of the Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-370">Use the name of the Azure virtual network.</span></span> |
   | <span data-ttu-id="5ceb4-371">**Subnet**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-371">**Subnet**</span></span> |<span data-ttu-id="5ceb4-372">Use the name of the subnet that the virtual machine is in.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-372">Use the name of the subnet that the virtual machine is in.</span></span>  |
   | <span data-ttu-id="5ceb4-373">**IP address assignment**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-373">**IP address assignment**</span></span> |<span data-ttu-id="5ceb4-374">Static</span><span class="sxs-lookup"><span data-stu-id="5ceb4-374">Static</span></span> |
   | <span data-ttu-id="5ceb4-375">**IP address**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-375">**IP address**</span></span> |<span data-ttu-id="5ceb4-376">Use an available address from subnet.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-376">Use an available address from subnet.</span></span> <span data-ttu-id="5ceb4-377">Use this address for your availability group listener.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-377">Use this address for your availability group listener.</span></span> <span data-ttu-id="5ceb4-378">Note that this is different from your cluster IP address.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-378">Note that this is different from your cluster IP address.</span></span>  |
   | <span data-ttu-id="5ceb4-379">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-379">**Subscription**</span></span> |<span data-ttu-id="5ceb4-380">Use the same subscription as the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-380">Use the same subscription as the virtual machine.</span></span> |
   | <span data-ttu-id="5ceb4-381">**Location**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-381">**Location**</span></span> |<span data-ttu-id="5ceb4-382">Use the same location as the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-382">Use the same location as the virtual machine.</span></span> |

   <span data-ttu-id="5ceb4-383">The Azure portal blade should look like this:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-383">The Azure portal blade should look like this:</span></span>

   ![Create Load Balancer](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. <span data-ttu-id="5ceb4-385">Click **Create**, to create the load balancer.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-385">Click **Create**, to create the load balancer.</span></span>

<span data-ttu-id="5ceb4-386">To configure the load balancer, you need to create a backend pool, a probe, and set the load balancing rules.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-386">To configure the load balancer, you need to create a backend pool, a probe, and set the load balancing rules.</span></span> <span data-ttu-id="5ceb4-387">Do these in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-387">Do these in the Azure portal.</span></span>

### <a name="add-backend-pool-for-the-availability-group-listener"></a><span data-ttu-id="5ceb4-388">Add backend pool for the availability group listener</span><span class="sxs-lookup"><span data-stu-id="5ceb4-388">Add backend pool for the availability group listener</span></span>

1. <span data-ttu-id="5ceb4-389">In the Azure portal, go to your availability group.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-389">In the Azure portal, go to your availability group.</span></span> <span data-ttu-id="5ceb4-390">You might need to refresh the view to see the newly created load balancer.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-390">You might need to refresh the view to see the newly created load balancer.</span></span>

   ![Find Load Balancer in Resource Group](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. <span data-ttu-id="5ceb4-392">Click the load balancer, click **Backend pools**, and click **+Add**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-392">Click the load balancer, click **Backend pools**, and click **+Add**.</span></span>

1. <span data-ttu-id="5ceb4-393">Type a name for the backend pool.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-393">Type a name for the backend pool.</span></span>

1. <span data-ttu-id="5ceb4-394">Associate the backend pool with the availability set that contains the VMs.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-394">Associate the backend pool with the availability set that contains the VMs.</span></span>

1. <span data-ttu-id="5ceb4-395">Under **Target network IP configurations**, check **VIRTUAL MACHINE** and choose both of the virtual machines that will host availability group replicas.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-395">Under **Target network IP configurations**, check **VIRTUAL MACHINE** and choose both of the virtual machines that will host availability group replicas.</span></span> <span data-ttu-id="5ceb4-396">Do not include the file share witness server.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-396">Do not include the file share witness server.</span></span>

   >[!NOTE]
   ><span data-ttu-id="5ceb4-397">If both virtual machines are not specified, connections will only succeed to the primary replica.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-397">If both virtual machines are not specified, connections will only succeed to the primary replica.</span></span>

1. <span data-ttu-id="5ceb4-398">Click **OK** to create the backend pool.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-398">Click **OK** to create the backend pool.</span></span>

### <a name="set-the-probe"></a><span data-ttu-id="5ceb4-399">Set the probe</span><span class="sxs-lookup"><span data-stu-id="5ceb4-399">Set the probe</span></span>

1. <span data-ttu-id="5ceb4-400">Click the load balancer, click **Health probes**, and click **+Add**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-400">Click the load balancer, click **Health probes**, and click **+Add**.</span></span>

1. <span data-ttu-id="5ceb4-401">Set the listener health probe as follows:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-401">Set the listener health probe as follows:</span></span>

   | <span data-ttu-id="5ceb4-402">Setting</span><span class="sxs-lookup"><span data-stu-id="5ceb4-402">Setting</span></span> | <span data-ttu-id="5ceb4-403">Description</span><span class="sxs-lookup"><span data-stu-id="5ceb4-403">Description</span></span> | <span data-ttu-id="5ceb4-404">Example</span><span class="sxs-lookup"><span data-stu-id="5ceb4-404">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="5ceb4-405">**Name**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-405">**Name**</span></span> | <span data-ttu-id="5ceb4-406">Text</span><span class="sxs-lookup"><span data-stu-id="5ceb4-406">Text</span></span> | <span data-ttu-id="5ceb4-407">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="5ceb4-407">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="5ceb4-408">**Protocol**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-408">**Protocol**</span></span> | <span data-ttu-id="5ceb4-409">Choose TCP</span><span class="sxs-lookup"><span data-stu-id="5ceb4-409">Choose TCP</span></span> | <span data-ttu-id="5ceb4-410">TCP</span><span class="sxs-lookup"><span data-stu-id="5ceb4-410">TCP</span></span> |
   | <span data-ttu-id="5ceb4-411">**Port**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-411">**Port**</span></span> | <span data-ttu-id="5ceb4-412">Any unused port</span><span class="sxs-lookup"><span data-stu-id="5ceb4-412">Any unused port</span></span> | <span data-ttu-id="5ceb4-413">59999</span><span class="sxs-lookup"><span data-stu-id="5ceb4-413">59999</span></span> |
   | <span data-ttu-id="5ceb4-414">**Interval**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-414">**Interval**</span></span>  | <span data-ttu-id="5ceb4-415">The amount of time between probe attempts in seconds</span><span class="sxs-lookup"><span data-stu-id="5ceb4-415">The amount of time between probe attempts in seconds</span></span> |<span data-ttu-id="5ceb4-416">5</span><span class="sxs-lookup"><span data-stu-id="5ceb4-416">5</span></span> |
   | <span data-ttu-id="5ceb4-417">**Unhealthy threshold**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-417">**Unhealthy threshold**</span></span> | <span data-ttu-id="5ceb4-418">The number of consecutive probe failures that must occur for a virtual machine to be considered unhealthy</span><span class="sxs-lookup"><span data-stu-id="5ceb4-418">The number of consecutive probe failures that must occur for a virtual machine to be considered unhealthy</span></span>  | <span data-ttu-id="5ceb4-419">2</span><span class="sxs-lookup"><span data-stu-id="5ceb4-419">2</span></span> |

1. <span data-ttu-id="5ceb4-420">Click **OK** to set the health probe.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-420">Click **OK** to set the health probe.</span></span>

### <a name="set-the-load-balancing-rules"></a><span data-ttu-id="5ceb4-421">Set the load balancing rules</span><span class="sxs-lookup"><span data-stu-id="5ceb4-421">Set the load balancing rules</span></span>

1. <span data-ttu-id="5ceb4-422">Click the load balancer, click **Load balancing rules**, and click **+Add**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-422">Click the load balancer, click **Load balancing rules**, and click **+Add**.</span></span>

1. <span data-ttu-id="5ceb4-423">Set the listener load balancing rules as follows.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-423">Set the listener load balancing rules as follows.</span></span>
   | <span data-ttu-id="5ceb4-424">Setting</span><span class="sxs-lookup"><span data-stu-id="5ceb4-424">Setting</span></span> | <span data-ttu-id="5ceb4-425">Description</span><span class="sxs-lookup"><span data-stu-id="5ceb4-425">Description</span></span> | <span data-ttu-id="5ceb4-426">Example</span><span class="sxs-lookup"><span data-stu-id="5ceb4-426">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="5ceb4-427">**Name**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-427">**Name**</span></span> | <span data-ttu-id="5ceb4-428">Text</span><span class="sxs-lookup"><span data-stu-id="5ceb4-428">Text</span></span> | <span data-ttu-id="5ceb4-429">SQLAlwaysOnEndPointListener</span><span class="sxs-lookup"><span data-stu-id="5ceb4-429">SQLAlwaysOnEndPointListener</span></span> |
   | <span data-ttu-id="5ceb4-430">**Frontend IP address**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-430">**Frontend IP address**</span></span> | <span data-ttu-id="5ceb4-431">Choose an address</span><span class="sxs-lookup"><span data-stu-id="5ceb4-431">Choose an address</span></span> |<span data-ttu-id="5ceb4-432">Use the address that you created when you created the load balancer.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-432">Use the address that you created when you created the load balancer.</span></span> |
   | <span data-ttu-id="5ceb4-433">**Protocol**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-433">**Protocol**</span></span> | <span data-ttu-id="5ceb4-434">Choose TCP</span><span class="sxs-lookup"><span data-stu-id="5ceb4-434">Choose TCP</span></span> |<span data-ttu-id="5ceb4-435">TCP</span><span class="sxs-lookup"><span data-stu-id="5ceb4-435">TCP</span></span> |
   | <span data-ttu-id="5ceb4-436">**Port**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-436">**Port**</span></span> | <span data-ttu-id="5ceb4-437">Use the port for the availability group listener</span><span class="sxs-lookup"><span data-stu-id="5ceb4-437">Use the port for the availability group listener</span></span> | <span data-ttu-id="5ceb4-438">1433</span><span class="sxs-lookup"><span data-stu-id="5ceb4-438">1433</span></span> |
   | <span data-ttu-id="5ceb4-439">**Backend Port**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-439">**Backend Port**</span></span> | <span data-ttu-id="5ceb4-440">This field is not used when Floating IP is set for direct server return</span><span class="sxs-lookup"><span data-stu-id="5ceb4-440">This field is not used when Floating IP is set for direct server return</span></span> | <span data-ttu-id="5ceb4-441">1433</span><span class="sxs-lookup"><span data-stu-id="5ceb4-441">1433</span></span> |
   | <span data-ttu-id="5ceb4-442">**Probe**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-442">**Probe**</span></span> |<span data-ttu-id="5ceb4-443">The name you specified for the probe</span><span class="sxs-lookup"><span data-stu-id="5ceb4-443">The name you specified for the probe</span></span> | <span data-ttu-id="5ceb4-444">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="5ceb4-444">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="5ceb4-445">**Session Persistence**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-445">**Session Persistence**</span></span> | <span data-ttu-id="5ceb4-446">Drop down list</span><span class="sxs-lookup"><span data-stu-id="5ceb4-446">Drop down list</span></span> | <span data-ttu-id="5ceb4-447">**None**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-447">**None**</span></span> |
   | <span data-ttu-id="5ceb4-448">**Idle Timeout**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-448">**Idle Timeout**</span></span> | <span data-ttu-id="5ceb4-449">Minutes to keep a TCP connection open</span><span class="sxs-lookup"><span data-stu-id="5ceb4-449">Minutes to keep a TCP connection open</span></span> | <span data-ttu-id="5ceb4-450">4</span><span class="sxs-lookup"><span data-stu-id="5ceb4-450">4</span></span> |
   | <span data-ttu-id="5ceb4-451">**Floating IP (direct server return)**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-451">**Floating IP (direct server return)**</span></span> | |<span data-ttu-id="5ceb4-452">Enabled</span><span class="sxs-lookup"><span data-stu-id="5ceb4-452">Enabled</span></span> |

   > [!WARNING]
   > <span data-ttu-id="5ceb4-453">Direct server return is set during creation.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-453">Direct server return is set during creation.</span></span> <span data-ttu-id="5ceb4-454">It cannot be changed.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-454">It cannot be changed.</span></span>

1. <span data-ttu-id="5ceb4-455">Click **OK** to set the listener load balancing rules.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-455">Click **OK** to set the listener load balancing rules.</span></span>

### <a name="add-the-cluster-core-ip-address-for-the-windows-server-failover-cluster-wsfc"></a><span data-ttu-id="5ceb4-456">Add the cluster core IP address for the Windows Server Failover Cluster (WSFC)</span><span class="sxs-lookup"><span data-stu-id="5ceb4-456">Add the cluster core IP address for the Windows Server Failover Cluster (WSFC)</span></span>

<span data-ttu-id="5ceb4-457">The WSFC IP address also needs to be on the load balancer.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-457">The WSFC IP address also needs to be on the load balancer.</span></span>

1. <span data-ttu-id="5ceb4-458">In the portal, on the same Azure load balancer, click **Frontend IP configuration** and click **+Add**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-458">In the portal, on the same Azure load balancer, click **Frontend IP configuration** and click **+Add**.</span></span> <span data-ttu-id="5ceb4-459">Use the IP Address you configured for the WSFC in the cluster core resources.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-459">Use the IP Address you configured for the WSFC in the cluster core resources.</span></span> <span data-ttu-id="5ceb4-460">Set the IP address as static.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-460">Set the IP address as static.</span></span>

1. <span data-ttu-id="5ceb4-461">On the load balancer, click **Health probes**, and click **+Add**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-461">On the load balancer, click **Health probes**, and click **+Add**.</span></span>

1. <span data-ttu-id="5ceb4-462">Set the WSFC cluster core IP address health probe as follows:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-462">Set the WSFC cluster core IP address health probe as follows:</span></span>

   | <span data-ttu-id="5ceb4-463">Setting</span><span class="sxs-lookup"><span data-stu-id="5ceb4-463">Setting</span></span> | <span data-ttu-id="5ceb4-464">Description</span><span class="sxs-lookup"><span data-stu-id="5ceb4-464">Description</span></span> | <span data-ttu-id="5ceb4-465">Example</span><span class="sxs-lookup"><span data-stu-id="5ceb4-465">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="5ceb4-466">**Name**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-466">**Name**</span></span> | <span data-ttu-id="5ceb4-467">Text</span><span class="sxs-lookup"><span data-stu-id="5ceb4-467">Text</span></span> | <span data-ttu-id="5ceb4-468">WSFCEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="5ceb4-468">WSFCEndPointProbe</span></span> |
   | <span data-ttu-id="5ceb4-469">**Protocol**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-469">**Protocol**</span></span> | <span data-ttu-id="5ceb4-470">Choose TCP</span><span class="sxs-lookup"><span data-stu-id="5ceb4-470">Choose TCP</span></span> | <span data-ttu-id="5ceb4-471">TCP</span><span class="sxs-lookup"><span data-stu-id="5ceb4-471">TCP</span></span> |
   | <span data-ttu-id="5ceb4-472">**Port**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-472">**Port**</span></span> | <span data-ttu-id="5ceb4-473">Any unused port</span><span class="sxs-lookup"><span data-stu-id="5ceb4-473">Any unused port</span></span> | <span data-ttu-id="5ceb4-474">58888</span><span class="sxs-lookup"><span data-stu-id="5ceb4-474">58888</span></span> |
   | <span data-ttu-id="5ceb4-475">**Interval**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-475">**Interval**</span></span>  | <span data-ttu-id="5ceb4-476">The amount of time between probe attempts in seconds</span><span class="sxs-lookup"><span data-stu-id="5ceb4-476">The amount of time between probe attempts in seconds</span></span> |<span data-ttu-id="5ceb4-477">5</span><span class="sxs-lookup"><span data-stu-id="5ceb4-477">5</span></span> |
   | <span data-ttu-id="5ceb4-478">**Unhealthy threshold**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-478">**Unhealthy threshold**</span></span> | <span data-ttu-id="5ceb4-479">The number of consecutive probe failures that must occur for a virtual machine to be considered unhealthy</span><span class="sxs-lookup"><span data-stu-id="5ceb4-479">The number of consecutive probe failures that must occur for a virtual machine to be considered unhealthy</span></span>  | <span data-ttu-id="5ceb4-480">2</span><span class="sxs-lookup"><span data-stu-id="5ceb4-480">2</span></span> |

1. <span data-ttu-id="5ceb4-481">Click **OK** to set the health probe.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-481">Click **OK** to set the health probe.</span></span>

1. <span data-ttu-id="5ceb4-482">Set the load balancing rules.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-482">Set the load balancing rules.</span></span> <span data-ttu-id="5ceb4-483">Click **Load balancing rules**, and click **+Add**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-483">Click **Load balancing rules**, and click **+Add**.</span></span>

1. <span data-ttu-id="5ceb4-484">Set the cluster core IP address load balancing rules as follows.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-484">Set the cluster core IP address load balancing rules as follows.</span></span>
   | <span data-ttu-id="5ceb4-485">Setting</span><span class="sxs-lookup"><span data-stu-id="5ceb4-485">Setting</span></span> | <span data-ttu-id="5ceb4-486">Description</span><span class="sxs-lookup"><span data-stu-id="5ceb4-486">Description</span></span> | <span data-ttu-id="5ceb4-487">Example</span><span class="sxs-lookup"><span data-stu-id="5ceb4-487">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="5ceb4-488">**Name**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-488">**Name**</span></span> | <span data-ttu-id="5ceb4-489">Text</span><span class="sxs-lookup"><span data-stu-id="5ceb4-489">Text</span></span> | <span data-ttu-id="5ceb4-490">WSFCEndPoint</span><span class="sxs-lookup"><span data-stu-id="5ceb4-490">WSFCEndPoint</span></span> |
   | <span data-ttu-id="5ceb4-491">**Frontend IP address**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-491">**Frontend IP address**</span></span> | <span data-ttu-id="5ceb4-492">Choose an address</span><span class="sxs-lookup"><span data-stu-id="5ceb4-492">Choose an address</span></span> |<span data-ttu-id="5ceb4-493">Use the address that you created when you configured the WSFC IP address.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-493">Use the address that you created when you configured the WSFC IP address.</span></span> <span data-ttu-id="5ceb4-494">This is different from the listener IP address</span><span class="sxs-lookup"><span data-stu-id="5ceb4-494">This is different from the listener IP address</span></span> |
   | <span data-ttu-id="5ceb4-495">**Protocol**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-495">**Protocol**</span></span> | <span data-ttu-id="5ceb4-496">Choose TCP</span><span class="sxs-lookup"><span data-stu-id="5ceb4-496">Choose TCP</span></span> |<span data-ttu-id="5ceb4-497">TCP</span><span class="sxs-lookup"><span data-stu-id="5ceb4-497">TCP</span></span> |
   | <span data-ttu-id="5ceb4-498">**Port**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-498">**Port**</span></span> | <span data-ttu-id="5ceb4-499">Use the port for the cluster IP address.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-499">Use the port for the cluster IP address.</span></span> <span data-ttu-id="5ceb4-500">This is an available port that is not used for the listener probe port.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-500">This is an available port that is not used for the listener probe port.</span></span> | <span data-ttu-id="5ceb4-501">58888</span><span class="sxs-lookup"><span data-stu-id="5ceb4-501">58888</span></span> |
   | <span data-ttu-id="5ceb4-502">**Backend Port**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-502">**Backend Port**</span></span> | <span data-ttu-id="5ceb4-503">This field is not used when Floating IP is set for direct server return</span><span class="sxs-lookup"><span data-stu-id="5ceb4-503">This field is not used when Floating IP is set for direct server return</span></span> | <span data-ttu-id="5ceb4-504">58888</span><span class="sxs-lookup"><span data-stu-id="5ceb4-504">58888</span></span> |
   | <span data-ttu-id="5ceb4-505">**Probe**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-505">**Probe**</span></span> |<span data-ttu-id="5ceb4-506">The name you specified for the probe</span><span class="sxs-lookup"><span data-stu-id="5ceb4-506">The name you specified for the probe</span></span> | <span data-ttu-id="5ceb4-507">WSFCEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="5ceb4-507">WSFCEndPointProbe</span></span> |
   | <span data-ttu-id="5ceb4-508">**Session Persistence**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-508">**Session Persistence**</span></span> | <span data-ttu-id="5ceb4-509">Drop down list</span><span class="sxs-lookup"><span data-stu-id="5ceb4-509">Drop down list</span></span> | <span data-ttu-id="5ceb4-510">**None**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-510">**None**</span></span> |
   | <span data-ttu-id="5ceb4-511">**Idle Timeout**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-511">**Idle Timeout**</span></span> | <span data-ttu-id="5ceb4-512">Minutes to keep a TCP connection open</span><span class="sxs-lookup"><span data-stu-id="5ceb4-512">Minutes to keep a TCP connection open</span></span> | <span data-ttu-id="5ceb4-513">4</span><span class="sxs-lookup"><span data-stu-id="5ceb4-513">4</span></span> |
   | <span data-ttu-id="5ceb4-514">**Floating IP (direct server return)**</span><span class="sxs-lookup"><span data-stu-id="5ceb4-514">**Floating IP (direct server return)**</span></span> | |<span data-ttu-id="5ceb4-515">Enabled</span><span class="sxs-lookup"><span data-stu-id="5ceb4-515">Enabled</span></span> |

   > [!WARNING]
   > <span data-ttu-id="5ceb4-516">Direct server return is set during creation.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-516">Direct server return is set during creation.</span></span> <span data-ttu-id="5ceb4-517">It cannot be changed.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-517">It cannot be changed.</span></span>

1. <span data-ttu-id="5ceb4-518">Click **OK** to set the load balancing rules.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-518">Click **OK** to set the load balancing rules.</span></span>

## <a name="configure-listener"></a> <span data-ttu-id="5ceb4-519">Configure the listener</span><span class="sxs-lookup"><span data-stu-id="5ceb4-519">Configure the listener</span></span>

<span data-ttu-id="5ceb4-520">The next thing to do is to configure an Availability Group listener on the failover cluster.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-520">The next thing to do is to configure an Availability Group listener on the failover cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="5ceb4-521">This tutorial shows how to create a single listener - with one ILB IP address.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-521">This tutorial shows how to create a single listener - with one ILB IP address.</span></span> <span data-ttu-id="5ceb4-522">To create one or more listeners using one or more IP addresses, see [Create Availability Group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5ceb4-522">To create one or more listeners using one or more IP addresses, see [Create Availability Group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a><span data-ttu-id="5ceb4-523">Set listener port</span><span class="sxs-lookup"><span data-stu-id="5ceb4-523">Set listener port</span></span>

<span data-ttu-id="5ceb4-524">In SQL Server Management Studio, set the listener port.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-524">In SQL Server Management Studio, set the listener port.</span></span>

1. <span data-ttu-id="5ceb4-525">Launch SQL Server Management Studio and connect to the primary replica.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-525">Launch SQL Server Management Studio and connect to the primary replica.</span></span>

1. <span data-ttu-id="5ceb4-526">Navigate to **AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-526">Navigate to **AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span>

1. <span data-ttu-id="5ceb4-527">You should now see the listener name that you created in Failover Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-527">You should now see the listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="5ceb4-528">Right-click the listener name and click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-528">Right-click the listener name and click **Properties**.</span></span>

1. <span data-ttu-id="5ceb4-529">In the **Port** box, specify the port number for the Availability Group listener.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-529">In the **Port** box, specify the port number for the Availability Group listener.</span></span> <span data-ttu-id="5ceb4-530">1433 is the default, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-530">1433 is the default, then click **OK**.</span></span>

<span data-ttu-id="5ceb4-531">You now have a SQL Server Availability Group in Azure virtual machines running in Resource Manager mode.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-531">You now have a SQL Server Availability Group in Azure virtual machines running in Resource Manager mode.</span></span>

## <a name="test-connection-to-listener"></a><span data-ttu-id="5ceb4-532">Test connection to listener</span><span class="sxs-lookup"><span data-stu-id="5ceb4-532">Test connection to listener</span></span>

<span data-ttu-id="5ceb4-533">To test the connection:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-533">To test the connection:</span></span>

1. <span data-ttu-id="5ceb4-534">RDP to a SQL Server that is in the same virtual network, but does not own the replica.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-534">RDP to a SQL Server that is in the same virtual network, but does not own the replica.</span></span> <span data-ttu-id="5ceb4-535">You can use the other SQL Server in the cluster.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-535">You can use the other SQL Server in the cluster.</span></span>

1. <span data-ttu-id="5ceb4-536">Use **sqlcmd** utility to test the connection.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-536">Use **sqlcmd** utility to test the connection.</span></span> <span data-ttu-id="5ceb4-537">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-537">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span></span>

  ```cmd
  sqlcmd -S <listenerName> -E
  ```

  <span data-ttu-id="5ceb4-538">If the listener is using a port other than the default port (1433), specify the port in the connection string.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-538">If the listener is using a port other than the default port (1433), specify the port in the connection string.</span></span> <span data-ttu-id="5ceb4-539">For example, the following sqlcmd command connects to a listener at port 1435:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-539">For example, the following sqlcmd command connects to a listener at port 1435:</span></span>

  ```cmd
  sqlcmd -S <listenerName>,1435 -E
  ```

<span data-ttu-id="5ceb4-540">The SQLCMD connection automatically connects to whichever instance of SQL Server hosts the primary replica.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-540">The SQLCMD connection automatically connects to whichever instance of SQL Server hosts the primary replica.</span></span>

> [!TIP]
> <span data-ttu-id="5ceb4-541">Make sure that the port you specify is open on the firewall of both SQL Servers.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-541">Make sure that the port you specify is open on the firewall of both SQL Servers.</span></span> <span data-ttu-id="5ceb4-542">Both servers require an inbound rule for the TCP port that you use.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-542">Both servers require an inbound rule for the TCP port that you use.</span></span> <span data-ttu-id="5ceb4-543">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ceb4-543">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ceb4-544">Next steps</span><span class="sxs-lookup"><span data-stu-id="5ceb4-544">Next steps</span></span>

- <span data-ttu-id="5ceb4-545">[Add an IP address to a load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span><span class="sxs-lookup"><span data-stu-id="5ceb4-545">[Add an IP address to a load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span></span>
