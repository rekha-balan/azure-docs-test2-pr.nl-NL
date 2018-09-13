---
title: SQL Server Availability Groups - Azure Virtual Machines - Tutorial | Microsoft Docs
description: This tutorial shows how to create a SQL Server Always On Availability Group on Azure Virtual Machines.
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: 158761122e16dfa4e4ec29c4c23637d55b179cb2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554311"
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a><span data-ttu-id="b0cc2-103">Configure Always On Availability Group in Azure VM manually</span><span class="sxs-lookup"><span data-stu-id="b0cc2-103">Configure Always On Availability Group in Azure VM manually</span></span>

<span data-ttu-id="b0cc2-104">This tutorial shows how to create a SQL Server Always On Availability Group on Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-104">This tutorial shows how to create a SQL Server Always On Availability Group on Azure Virtual Machines.</span></span> <span data-ttu-id="b0cc2-105">The complete tutorial creates an Availability Group with a database replica on two SQL Servers.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-105">The complete tutorial creates an Availability Group with a database replica on two SQL Servers.</span></span>

<span data-ttu-id="b0cc2-106">**Time estimate**: Takes about 30 minutes to complete once the prerequisites are met.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-106">**Time estimate**: Takes about 30 minutes to complete once the prerequisites are met.</span></span>

<span data-ttu-id="b0cc2-107">The diagram illustrates what you build in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-107">The diagram illustrates what you build in the tutorial.</span></span>

![Availability Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a><span data-ttu-id="b0cc2-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b0cc2-109">Prerequisites</span></span>

<span data-ttu-id="b0cc2-110">The tutorial assumes you have a basic understanding of SQL Server Always On Availability Groups.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-110">The tutorial assumes you have a basic understanding of SQL Server Always On Availability Groups.</span></span> <span data-ttu-id="b0cc2-111">If you need more information, see [Overview of Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0cc2-111">If you need more information, see [Overview of Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span></span>

<span data-ttu-id="b0cc2-112">The following table lists the prerequisites that you need to complete before starting this tutorial:</span><span class="sxs-lookup"><span data-stu-id="b0cc2-112">The following table lists the prerequisites that you need to complete before starting this tutorial:</span></span>

|  |<span data-ttu-id="b0cc2-113">Requirement</span><span class="sxs-lookup"><span data-stu-id="b0cc2-113">Requirement</span></span> |<span data-ttu-id="b0cc2-114">Description</span><span class="sxs-lookup"><span data-stu-id="b0cc2-114">Description</span></span> |
|----- |----- |----- |
|![Square](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | <span data-ttu-id="b0cc2-116">Two SQL Servers</span><span class="sxs-lookup"><span data-stu-id="b0cc2-116">Two SQL Servers</span></span> | <span data-ttu-id="b0cc2-117">- In an Azure availability set</span><span class="sxs-lookup"><span data-stu-id="b0cc2-117">- In an Azure availability set</span></span> <br/> <span data-ttu-id="b0cc2-118">- In a single domain</span><span class="sxs-lookup"><span data-stu-id="b0cc2-118">- In a single domain</span></span> <br/> <span data-ttu-id="b0cc2-119">- With Failover Clustering feature installed</span><span class="sxs-lookup"><span data-stu-id="b0cc2-119">- With Failover Clustering feature installed</span></span> |
|![Square](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| <span data-ttu-id="b0cc2-121">Windows Server</span><span class="sxs-lookup"><span data-stu-id="b0cc2-121">Windows Server</span></span> | <span data-ttu-id="b0cc2-122">File share for cluster witness</span><span class="sxs-lookup"><span data-stu-id="b0cc2-122">File share for cluster witness</span></span> |  
|![Square](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="b0cc2-124">SQL Server service account</span><span class="sxs-lookup"><span data-stu-id="b0cc2-124">SQL Server service account</span></span> | <span data-ttu-id="b0cc2-125">Domain account</span><span class="sxs-lookup"><span data-stu-id="b0cc2-125">Domain account</span></span> |
|![Square](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="b0cc2-127">SQL Server Agent service account</span><span class="sxs-lookup"><span data-stu-id="b0cc2-127">SQL Server Agent service account</span></span> | <span data-ttu-id="b0cc2-128">Domain account</span><span class="sxs-lookup"><span data-stu-id="b0cc2-128">Domain account</span></span> |  
|![Square](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="b0cc2-130">Firewall ports open</span><span class="sxs-lookup"><span data-stu-id="b0cc2-130">Firewall ports open</span></span> | <span data-ttu-id="b0cc2-131">- SQL Server: **1433** for default instance</span><span class="sxs-lookup"><span data-stu-id="b0cc2-131">- SQL Server: **1433** for default instance</span></span> <br/> <span data-ttu-id="b0cc2-132">- Database mirroring endpoint: **5022** or any available port</span><span class="sxs-lookup"><span data-stu-id="b0cc2-132">- Database mirroring endpoint: **5022** or any available port</span></span> <br/> <span data-ttu-id="b0cc2-133">- Azure load balancer probe: **59999** or any available port</span><span class="sxs-lookup"><span data-stu-id="b0cc2-133">- Azure load balancer probe: **59999** or any available port</span></span> |
|![Square](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="b0cc2-135">Add Failover Clustering Feature</span><span class="sxs-lookup"><span data-stu-id="b0cc2-135">Add Failover Clustering Feature</span></span> | <span data-ttu-id="b0cc2-136">Both SQL Servers require this feature</span><span class="sxs-lookup"><span data-stu-id="b0cc2-136">Both SQL Servers require this feature</span></span> |
|![Square](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="b0cc2-138">Installation domain account</span><span class="sxs-lookup"><span data-stu-id="b0cc2-138">Installation domain account</span></span> | <span data-ttu-id="b0cc2-139">- Local administrator on each SQL Server</span><span class="sxs-lookup"><span data-stu-id="b0cc2-139">- Local administrator on each SQL Server</span></span> <br/> <span data-ttu-id="b0cc2-140">- Member of SQL Server sysadmin fixed server role for each instance of SQL Server</span><span class="sxs-lookup"><span data-stu-id="b0cc2-140">- Member of SQL Server sysadmin fixed server role for each instance of SQL Server</span></span>  |


<span data-ttu-id="b0cc2-141">Before you begin the tutorial, you need to [Complete prerequisites for creating Always On Availability Groups in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span><span class="sxs-lookup"><span data-stu-id="b0cc2-141">Before you begin the tutorial, you need to [Complete prerequisites for creating Always On Availability Groups in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span></span> <span data-ttu-id="b0cc2-142">If these prerequisites are completed already, you can jump to [Create Cluster](#CreateCluster).</span><span class="sxs-lookup"><span data-stu-id="b0cc2-142">If these prerequisites are completed already, you can jump to [Create Cluster](#CreateCluster).</span></span>


<!--**Procedure**: *This is the first “step”. Make titles H2’s and short and clear – H2’s appear in the right pane on the web page and are important for navigation.*-->

<a name="CreateCluster"></a>
## <a name="create-the-cluster"></a><span data-ttu-id="b0cc2-143">Create the cluster</span><span class="sxs-lookup"><span data-stu-id="b0cc2-143">Create the cluster</span></span>

<span data-ttu-id="b0cc2-144">After the prerequisites are completed, the first step is to create a Windows Server Failover Cluster that includes two SQL Severs and a witness server.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-144">After the prerequisites are completed, the first step is to create a Windows Server Failover Cluster that includes two SQL Severs and a witness server.</span></span>  

1. <span data-ttu-id="b0cc2-145">RDP to the first SQL Server using a domain account that is an administrator on both SQL Servers and the witness server.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-145">RDP to the first SQL Server using a domain account that is an administrator on both SQL Servers and the witness server.</span></span>

   >[!TIP]
   ><span data-ttu-id="b0cc2-146">If you followed the [prerequisites document](virtual-machines-windows-portal-sql-availability-group-prereq.md), you created an account called **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-146">If you followed the [prerequisites document](virtual-machines-windows-portal-sql-availability-group-prereq.md), you created an account called **CORP\Install**.</span></span> <span data-ttu-id="b0cc2-147">Use this account.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-147">Use this account.</span></span>

2. <span data-ttu-id="b0cc2-148">In the **Server Manager** dashboard, select **Tools**, and then click **Failover Cluster Manager**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-148">In the **Server Manager** dashboard, select **Tools**, and then click **Failover Cluster Manager**.</span></span>
3. <span data-ttu-id="b0cc2-149">In the left pane, right-click **Failover Cluster Manager**, and then click **Create a Cluster**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-149">In the left pane, right-click **Failover Cluster Manager**, and then click **Create a Cluster**.</span></span>
   <span data-ttu-id="b0cc2-150">![Create Cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span><span class="sxs-lookup"><span data-stu-id="b0cc2-150">![Create Cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span></span>
4. <span data-ttu-id="b0cc2-151">In the Create Cluster Wizard, create a one-node cluster by stepping through the pages with the settings in the following table:</span><span class="sxs-lookup"><span data-stu-id="b0cc2-151">In the Create Cluster Wizard, create a one-node cluster by stepping through the pages with the settings in the following table:</span></span>

   | <span data-ttu-id="b0cc2-152">Page</span><span class="sxs-lookup"><span data-stu-id="b0cc2-152">Page</span></span> | <span data-ttu-id="b0cc2-153">Settings</span><span class="sxs-lookup"><span data-stu-id="b0cc2-153">Settings</span></span> |
   | --- | --- |
   | <span data-ttu-id="b0cc2-154">Before You Begin</span><span class="sxs-lookup"><span data-stu-id="b0cc2-154">Before You Begin</span></span> |<span data-ttu-id="b0cc2-155">Use defaults</span><span class="sxs-lookup"><span data-stu-id="b0cc2-155">Use defaults</span></span> |
   | <span data-ttu-id="b0cc2-156">Select Servers</span><span class="sxs-lookup"><span data-stu-id="b0cc2-156">Select Servers</span></span> |<span data-ttu-id="b0cc2-157">Type the first SQL Server name in **Enter server name** and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-157">Type the first SQL Server name in **Enter server name** and click **Add**.</span></span> |
   | <span data-ttu-id="b0cc2-158">Validation Warning</span><span class="sxs-lookup"><span data-stu-id="b0cc2-158">Validation Warning</span></span> |<span data-ttu-id="b0cc2-159">Select **No. I do not require support from Microsoft for this cluster, and therefore do not want to run the validation tests. When I click Next, continue Creating the cluster**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-159">Select **No. I do not require support from Microsoft for this cluster, and therefore do not want to run the validation tests. When I click Next, continue Creating the cluster**.</span></span> |
   | <span data-ttu-id="b0cc2-160">Access Point for Administering the Cluster</span><span class="sxs-lookup"><span data-stu-id="b0cc2-160">Access Point for Administering the Cluster</span></span> |<span data-ttu-id="b0cc2-161">Type a cluster name, for example **SQLAGCluster1** in **Cluster Name**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-161">Type a cluster name, for example **SQLAGCluster1** in **Cluster Name**.</span></span>|
   | <span data-ttu-id="b0cc2-162">Confirmation</span><span class="sxs-lookup"><span data-stu-id="b0cc2-162">Confirmation</span></span> |<span data-ttu-id="b0cc2-163">Use defaults unless you are using Storage Spaces.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-163">Use defaults unless you are using Storage Spaces.</span></span> <span data-ttu-id="b0cc2-164">See the note following this table.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-164">See the note following this table.</span></span> |

### <a name="set-the-cluster-ip-address"></a><span data-ttu-id="b0cc2-165">Set the cluster IP address</span><span class="sxs-lookup"><span data-stu-id="b0cc2-165">Set the cluster IP address</span></span>

1. <span data-ttu-id="b0cc2-166">In **Failover Cluster Manager**, scroll down to **Cluster Core Resources** and expand the cluster details.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-166">In **Failover Cluster Manager**, scroll down to **Cluster Core Resources** and expand the cluster details.</span></span> <span data-ttu-id="b0cc2-167">You should see both the **Name** and the **IP Address** resources in the **Failed** state.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-167">You should see both the **Name** and the **IP Address** resources in the **Failed** state.</span></span> <span data-ttu-id="b0cc2-168">The IP address resource cannot be brought online because the cluster is assigned the same IP address as the machine itself, therefore it is a duplicate address.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-168">The IP address resource cannot be brought online because the cluster is assigned the same IP address as the machine itself, therefore it is a duplicate address.</span></span>

2. <span data-ttu-id="b0cc2-169">Right-click the failed **IP Address** resource, and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-169">Right-click the failed **IP Address** resource, and then click **Properties**.</span></span>

   ![Cluster Properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. <span data-ttu-id="b0cc2-171">Select **Static IP Address** and specify an available address from subnet where the SQL Server is in the Address text box.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-171">Select **Static IP Address** and specify an available address from subnet where the SQL Server is in the Address text box.</span></span> <span data-ttu-id="b0cc2-172">Then, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-172">Then, click **OK**.</span></span>
4. <span data-ttu-id="b0cc2-173">In the **Cluster Core Resources** section, right-click cluster name and click **Bring Online**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-173">In the **Cluster Core Resources** section, right-click cluster name and click **Bring Online**.</span></span> <span data-ttu-id="b0cc2-174">Then, wait until both resources are online.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-174">Then, wait until both resources are online.</span></span> <span data-ttu-id="b0cc2-175">When the cluster name resource comes online, it updates the DC server with a new AD computer account.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-175">When the cluster name resource comes online, it updates the DC server with a new AD computer account.</span></span> <span data-ttu-id="b0cc2-176">Use this AD account to run the Availability Group clustered service later.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-176">Use this AD account to run the Availability Group clustered service later.</span></span>

### <a name="addNode"></a><span data-ttu-id="b0cc2-177">Add the other SQL Server to cluster</span><span class="sxs-lookup"><span data-stu-id="b0cc2-177">Add the other SQL Server to cluster</span></span>

<span data-ttu-id="b0cc2-178">Add the other SQL Server to the cluster.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-178">Add the other SQL Server to the cluster.</span></span>

1. <span data-ttu-id="b0cc2-179">In the browser tree, right-click the cluster and click **Add Node**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-179">In the browser tree, right-click the cluster and click **Add Node**.</span></span>

    ![Add Node to the Cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. <span data-ttu-id="b0cc2-181">In the **Add Node Wizard**, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-181">In the **Add Node Wizard**, click **Next**.</span></span> <span data-ttu-id="b0cc2-182">In the **Select Servers** page, add the second SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-182">In the **Select Servers** page, add the second SQL Server.</span></span> <span data-ttu-id="b0cc2-183">Type the server name in **Enter server name** and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-183">Type the server name in **Enter server name** and then click **Add**.</span></span> <span data-ttu-id="b0cc2-184">When you are done, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-184">When you are done, click **Next**.</span></span>

1. <span data-ttu-id="b0cc2-185">In the **Validation Warning** page, click **No** (in a production scenario you should perform the validation tests).</span><span class="sxs-lookup"><span data-stu-id="b0cc2-185">In the **Validation Warning** page, click **No** (in a production scenario you should perform the validation tests).</span></span> <span data-ttu-id="b0cc2-186">Then, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-186">Then, click **Next**.</span></span>

8. <span data-ttu-id="b0cc2-187">In the **Confirmation** page if you are using Storage Spaces, clear the checkbox labeled **Add all eligible storage to the cluster.**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-187">In the **Confirmation** page if you are using Storage Spaces, clear the checkbox labeled **Add all eligible storage to the cluster.**</span></span>

   ![Add Node Confirmation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   ><span data-ttu-id="b0cc2-189">If you are using Storage Spaces and do not uncheck **Add all eligible storage to the cluster**, Windows detaches the virtual disks during the clustering process.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-189">If you are using Storage Spaces and do not uncheck **Add all eligible storage to the cluster**, Windows detaches the virtual disks during the clustering process.</span></span> <span data-ttu-id="b0cc2-190">As a result, they do not appear in Disk Manager or Explorer until the storage spaces are removed from the cluster and reattached using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-190">As a result, they do not appear in Disk Manager or Explorer until the storage spaces are removed from the cluster and reattached using PowerShell.</span></span> <span data-ttu-id="b0cc2-191">Storage Spaces groups multiple disks in to storage pools.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-191">Storage Spaces groups multiple disks in to storage pools.</span></span> <span data-ttu-id="b0cc2-192">For more information, see [Storage Spaces](https://technet.microsoft.com/library/hh831739).</span><span class="sxs-lookup"><span data-stu-id="b0cc2-192">For more information, see [Storage Spaces](https://technet.microsoft.com/library/hh831739).</span></span>

1. <span data-ttu-id="b0cc2-193">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-193">Click **Next**.</span></span>

1. <span data-ttu-id="b0cc2-194">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-194">Click **Finish**.</span></span>

   <span data-ttu-id="b0cc2-195">Failover Cluster Manager shows that your cluster has a new node and lists it in the **Nodes** container.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-195">Failover Cluster Manager shows that your cluster has a new node and lists it in the **Nodes** container.</span></span>

10. <span data-ttu-id="b0cc2-196">Log out of the remote desktop session.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-196">Log out of the remote desktop session.</span></span>

### <a name="add-a-cluster-quorum-file-share"></a><span data-ttu-id="b0cc2-197">Add a cluster quorum file share</span><span class="sxs-lookup"><span data-stu-id="b0cc2-197">Add a cluster quorum file share</span></span>

<span data-ttu-id="b0cc2-198">In this example the Windows cluster uses a file share to create a cluster quorum.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-198">In this example the Windows cluster uses a file share to create a cluster quorum.</span></span> <span data-ttu-id="b0cc2-199">This tutorial uses a Node and File Share Majority quorum.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-199">This tutorial uses a Node and File Share Majority quorum.</span></span> <span data-ttu-id="b0cc2-200">For more information, see [Understanding Quorum Configurations in a Failover Cluster](http://technet.microsoft.com/library/cc731739.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0cc2-200">For more information, see [Understanding Quorum Configurations in a Failover Cluster](http://technet.microsoft.com/library/cc731739.aspx).</span></span>

1. <span data-ttu-id="b0cc2-201">Connect to the file share witness member server with a remote desktop session.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-201">Connect to the file share witness member server with a remote desktop session.</span></span>

1. <span data-ttu-id="b0cc2-202">On **Server Manager**, click **Tools**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-202">On **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="b0cc2-203">Open **Computer Management**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-203">Open **Computer Management**.</span></span>

1. <span data-ttu-id="b0cc2-204">Click **Shared Folders**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-204">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="b0cc2-205">Right-click **Shares**, and click **New Share...**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-205">Right-click **Shares**, and click **New Share...**.</span></span>

   ![New Share](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="b0cc2-207">Use **Create a Shared Folder Wizard** to create a share.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-207">Use **Create a Shared Folder Wizard** to create a share.</span></span>

1. <span data-ttu-id="b0cc2-208">On **Folder Path**, click **Browse** and locate or create a path for the shared folder.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-208">On **Folder Path**, click **Browse** and locate or create a path for the shared folder.</span></span> <span data-ttu-id="b0cc2-209">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-209">Click **Next**.</span></span>

1. <span data-ttu-id="b0cc2-210">In **Name, Description, and Settings** verify the share name and path.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-210">In **Name, Description, and Settings** verify the share name and path.</span></span> <span data-ttu-id="b0cc2-211">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-211">Click **Next**.</span></span>

1. <span data-ttu-id="b0cc2-212">On **Shared Folder Permissions** set **Customize permissions**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-212">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="b0cc2-213">Click **Custom...**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-213">Click **Custom...**.</span></span>

1. <span data-ttu-id="b0cc2-214">On **Customize Permissions**, click **Add...**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-214">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="b0cc2-215">Make sure that the account used to create the cluster has full control.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-215">Make sure that the account used to create the cluster has full control.</span></span>

   ![New Share](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. <span data-ttu-id="b0cc2-217">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-217">Click **OK**.</span></span>

1. <span data-ttu-id="b0cc2-218">In **Shared Folder Permissions**, click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-218">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="b0cc2-219">Click **Finish** again.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-219">Click **Finish** again.</span></span>  

1. <span data-ttu-id="b0cc2-220">Log out of the server</span><span class="sxs-lookup"><span data-stu-id="b0cc2-220">Log out of the server</span></span>

### <a name="configure-cluster-quorum"></a><span data-ttu-id="b0cc2-221">Configure cluster quorum</span><span class="sxs-lookup"><span data-stu-id="b0cc2-221">Configure cluster quorum</span></span>

<span data-ttu-id="b0cc2-222">Next, set the cluster quorum.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-222">Next, set the cluster quorum.</span></span>

1. <span data-ttu-id="b0cc2-223">Connect to the first cluster node with remote desktop.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-223">Connect to the first cluster node with remote desktop.</span></span>

1. <span data-ttu-id="b0cc2-224">In **Failover Cluster Manager**, right-click the cluster, point to **More Actions**, and click **Configure Cluster Quorum Settings...**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-224">In **Failover Cluster Manager**, right-click the cluster, point to **More Actions**, and click **Configure Cluster Quorum Settings...**.</span></span>

   ![New Share](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. <span data-ttu-id="b0cc2-226">In **Configure Cluster Quorum Wizard**, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-226">In **Configure Cluster Quorum Wizard**, click **Next**.</span></span>

1. <span data-ttu-id="b0cc2-227">In **Select Quorum Configuration Option**, choose **Select the quorum witness**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-227">In **Select Quorum Configuration Option**, choose **Select the quorum witness**, and click **Next**.</span></span>

1. <span data-ttu-id="b0cc2-228">On **Select Quorum Witness**, click **Configure a file share witness**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-228">On **Select Quorum Witness**, click **Configure a file share witness**.</span></span>

   >[!TIP]
   ><span data-ttu-id="b0cc2-229">Windows Server 2016 supports a cloud witness.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-229">Windows Server 2016 supports a cloud witness.</span></span> <span data-ttu-id="b0cc2-230">If you choose this type of witness, you do not need a file share witness.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-230">If you choose this type of witness, you do not need a file share witness.</span></span> <span data-ttu-id="b0cc2-231">For more information, see [Deploy a cloud witness for a Failover Cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="b0cc2-231">For more information, see [Deploy a cloud witness for a Failover Cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span> <span data-ttu-id="b0cc2-232">This tutorial uses a file share witness, which is supported by previous operating systems.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-232">This tutorial uses a file share witness, which is supported by previous operating systems.</span></span>

1. <span data-ttu-id="b0cc2-233">On **Configure File Share Witness**, type the path for the share you created.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-233">On **Configure File Share Witness**, type the path for the share you created.</span></span> <span data-ttu-id="b0cc2-234">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-234">Click **Next**.</span></span>

1. <span data-ttu-id="b0cc2-235">Verify the settings on **Confirmation**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-235">Verify the settings on **Confirmation**.</span></span> <span data-ttu-id="b0cc2-236">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-236">Click **Next**.</span></span>

1. <span data-ttu-id="b0cc2-237">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-237">Click **Finish**.</span></span>

<span data-ttu-id="b0cc2-238">The cluster core resources are configured with a file share witness.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-238">The cluster core resources are configured with a file share witness.</span></span>

## <a name="enable-availability-groups"></a><span data-ttu-id="b0cc2-239">Enable Availability Groups</span><span class="sxs-lookup"><span data-stu-id="b0cc2-239">Enable Availability Groups</span></span>

<span data-ttu-id="b0cc2-240">Next, enable the **AlwaysOn Availability Groups** feature.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-240">Next, enable the **AlwaysOn Availability Groups** feature.</span></span> <span data-ttu-id="b0cc2-241">Do these steps on both SQL Servers.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-241">Do these steps on both SQL Servers.</span></span>

1. <span data-ttu-id="b0cc2-242">From the **Start** screen, launch **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-242">From the **Start** screen, launch **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="b0cc2-243">In the browser tree, click **SQL Server Services**, then right-click the **SQL Server (MSSQLSERVER)** service and click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-243">In the browser tree, click **SQL Server Services**, then right-click the **SQL Server (MSSQLSERVER)** service and click **Properties**.</span></span>
3. <span data-ttu-id="b0cc2-244">Click the **AlwaysOn High Availability** tab, then select **Enable AlwaysOn Availability Groups**, as follows:</span><span class="sxs-lookup"><span data-stu-id="b0cc2-244">Click the **AlwaysOn High Availability** tab, then select **Enable AlwaysOn Availability Groups**, as follows:</span></span>

    ![Enable AlwaysOn Availability Groups](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. <span data-ttu-id="b0cc2-246">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-246">Click **Apply**.</span></span> <span data-ttu-id="b0cc2-247">Click **OK** in the pop-up dialog.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-247">Click **OK** in the pop-up dialog.</span></span>

5. <span data-ttu-id="b0cc2-248">Restart the SQL Server service.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-248">Restart the SQL Server service.</span></span>

<span data-ttu-id="b0cc2-249">Repeat these steps on the other SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-249">Repeat these steps on the other SQL Server.</span></span>

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

## <a name="create-a-database-on-the-first-sql-server"></a><span data-ttu-id="b0cc2-250">Create a database on the first SQL Server</span><span class="sxs-lookup"><span data-stu-id="b0cc2-250">Create a database on the first SQL Server</span></span>

1. <span data-ttu-id="b0cc2-251">Launch the RDP file to the first SQL Server with a domain account that is a member of sysadmin fixed server role.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-251">Launch the RDP file to the first SQL Server with a domain account that is a member of sysadmin fixed server role.</span></span>
1. <span data-ttu-id="b0cc2-252">Open SQL Server Management Studio and connect to the first SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-252">Open SQL Server Management Studio and connect to the first SQL Server.</span></span>
7. <span data-ttu-id="b0cc2-253">In **Object Explorer**, right-click **Databases** and click **New Database**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-253">In **Object Explorer**, right-click **Databases** and click **New Database**.</span></span>
8. <span data-ttu-id="b0cc2-254">In **Database name**, type **MyDB1**, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-254">In **Database name**, type **MyDB1**, then click **OK**.</span></span>

### <a name="backupshare"></a> <span data-ttu-id="b0cc2-255">Create a backup share</span><span class="sxs-lookup"><span data-stu-id="b0cc2-255">Create a backup share</span></span>

1. <span data-ttu-id="b0cc2-256">On the first SQL Server in **Server Manager**, click **Tools**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-256">On the first SQL Server in **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="b0cc2-257">Open **Computer Management**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-257">Open **Computer Management**.</span></span>

1. <span data-ttu-id="b0cc2-258">Click **Shared Folders**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-258">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="b0cc2-259">Right-click **Shares**, and click **New Share...**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-259">Right-click **Shares**, and click **New Share...**.</span></span>

   ![New Share](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="b0cc2-261">Use **Create a Shared Folder Wizard** to create a share.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-261">Use **Create a Shared Folder Wizard** to create a share.</span></span>

1. <span data-ttu-id="b0cc2-262">On **Folder Path**, click **Browse** and locate or create a path for the database backup shared folder.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-262">On **Folder Path**, click **Browse** and locate or create a path for the database backup shared folder.</span></span> <span data-ttu-id="b0cc2-263">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-263">Click **Next**.</span></span>

1. <span data-ttu-id="b0cc2-264">In **Name, Description, and Settings** verify the share name and path.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-264">In **Name, Description, and Settings** verify the share name and path.</span></span> <span data-ttu-id="b0cc2-265">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-265">Click **Next**.</span></span>

1. <span data-ttu-id="b0cc2-266">On **Shared Folder Permissions** set **Customize permissions**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-266">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="b0cc2-267">Click **Custom...**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-267">Click **Custom...**.</span></span>

1. <span data-ttu-id="b0cc2-268">On **Customize Permissions**, click **Add...**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-268">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="b0cc2-269">Make sure that the SQL Server and SQL Server Agent service accounts for both servers have full control.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-269">Make sure that the SQL Server and SQL Server Agent service accounts for both servers have full control.</span></span>

   ![New Share](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. <span data-ttu-id="b0cc2-271">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-271">Click **OK**.</span></span>

1. <span data-ttu-id="b0cc2-272">In **Shared Folder Permissions**, click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-272">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="b0cc2-273">Click **Finish** again.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-273">Click **Finish** again.</span></span>  

### <a name="take-a-full-backup-of-the-database"></a><span data-ttu-id="b0cc2-274">Take a full backup of the database</span><span class="sxs-lookup"><span data-stu-id="b0cc2-274">Take a full backup of the database</span></span>

<span data-ttu-id="b0cc2-275">You need to back up the new database to initialize the log chain.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-275">You need to back up the new database to initialize the log chain.</span></span> <span data-ttu-id="b0cc2-276">If you do not take a backup of the new database, it cannot be included in an Availability Group.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-276">If you do not take a backup of the new database, it cannot be included in an Availability Group.</span></span>

1. <span data-ttu-id="b0cc2-277">In **Object Explorer**, right-click the database, point to **Tasks...**, click **Back Up**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-277">In **Object Explorer**, right-click the database, point to **Tasks...**, click **Back Up**.</span></span>

1. <span data-ttu-id="b0cc2-278">Click **OK** to take a full backup to the default backup location.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-278">Click **OK** to take a full backup to the default backup location.</span></span>

## <a name="create-the-availability-group"></a><span data-ttu-id="b0cc2-279">Create the Availability Group</span><span class="sxs-lookup"><span data-stu-id="b0cc2-279">Create the Availability Group</span></span>
<span data-ttu-id="b0cc2-280">You are now ready to configure an Availability Group using the following steps:</span><span class="sxs-lookup"><span data-stu-id="b0cc2-280">You are now ready to configure an Availability Group using the following steps:</span></span>

* <span data-ttu-id="b0cc2-281">Create a database on the first SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-281">Create a database on the first SQL Server.</span></span>
* <span data-ttu-id="b0cc2-282">Take both a full backup and a transaction log backup of the database</span><span class="sxs-lookup"><span data-stu-id="b0cc2-282">Take both a full backup and a transaction log backup of the database</span></span>
* <span data-ttu-id="b0cc2-283">Restore the full and log backups to the second SQL Server with the **NORECOVERY** option</span><span class="sxs-lookup"><span data-stu-id="b0cc2-283">Restore the full and log backups to the second SQL Server with the **NORECOVERY** option</span></span>
* <span data-ttu-id="b0cc2-284">Create the Availability Group (**AG1**) with synchronous commit, automatic failover, and readable secondary replicas</span><span class="sxs-lookup"><span data-stu-id="b0cc2-284">Create the Availability Group (**AG1**) with synchronous commit, automatic failover, and readable secondary replicas</span></span>

### <a name="create-the-availability-group"></a><span data-ttu-id="b0cc2-285">Create the Availability Group:</span><span class="sxs-lookup"><span data-stu-id="b0cc2-285">Create the Availability Group:</span></span>

1. <span data-ttu-id="b0cc2-286">On remote desktop session to the first SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-286">On remote desktop session to the first SQL Server.</span></span> <span data-ttu-id="b0cc2-287">In **Object Explorer** in SSMS, right-click **AlwaysOn High Availability** and click **New Availability Group Wizard**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-287">In **Object Explorer** in SSMS, right-click **AlwaysOn High Availability** and click **New Availability Group Wizard**.</span></span>

    ![Launch New Availability Group Wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. <span data-ttu-id="b0cc2-289">In the **Introduction** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-289">In the **Introduction** page, click **Next**.</span></span> <span data-ttu-id="b0cc2-290">In the **Specify Availability Group Name** page, type a name for the Availability Group, for example **AG1**, in **Availability group name**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-290">In the **Specify Availability Group Name** page, type a name for the Availability Group, for example **AG1**, in **Availability group name**.</span></span> <span data-ttu-id="b0cc2-291">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-291">Click **Next**.</span></span>

    ![New AG Wizard, Specify AG Name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. <span data-ttu-id="b0cc2-293">In the **Select Databases** page, select your database and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-293">In the **Select Databases** page, select your database and click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="b0cc2-294">The database meets the prerequisites for an Availability Group because you have taken at least one full backup on the intended primary replica.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-294">The database meets the prerequisites for an Availability Group because you have taken at least one full backup on the intended primary replica.</span></span>

   ![New AG Wizard, Select Databases](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. <span data-ttu-id="b0cc2-296">In the **Specify Replicas** page, click **Add Replica**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-296">In the **Specify Replicas** page, click **Add Replica**.</span></span>

   ![New AG Wizard, Specify Replicas](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. <span data-ttu-id="b0cc2-298">The **Connect to Server** dialog pops up.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-298">The **Connect to Server** dialog pops up.</span></span> <span data-ttu-id="b0cc2-299">Type the name of the second server in **Server name**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-299">Type the name of the second server in **Server name**.</span></span> <span data-ttu-id="b0cc2-300">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-300">Click **Connect**.</span></span>

   <span data-ttu-id="b0cc2-301">Back in the **Specify Replicas** page, you should now see the second server listed in **Availability Replicas**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-301">Back in the **Specify Replicas** page, you should now see the second server listed in **Availability Replicas**.</span></span> <span data-ttu-id="b0cc2-302">Configure the replicas as follows.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-302">Configure the replicas as follows.</span></span>

   ![New AG Wizard, Specify Replicas (Complete)](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. <span data-ttu-id="b0cc2-304">Click **Endpoints** to see the database mirroring endpoint for this Availability Group.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-304">Click **Endpoints** to see the database mirroring endpoint for this Availability Group.</span></span> <span data-ttu-id="b0cc2-305">Use the same port that you used when you set the [firewall rule for database mirroring endpoints](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="b0cc2-305">Use the same port that you used when you set the [firewall rule for database mirroring endpoints](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

    ![New AG Wizard, Select Initial Data Synchronization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. <span data-ttu-id="b0cc2-307">In the **Select Initial Data Synchronization** page, select **Full** and specify a shared network location.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-307">In the **Select Initial Data Synchronization** page, select **Full** and specify a shared network location.</span></span> <span data-ttu-id="b0cc2-308">For the location, use the [backup share that you created](#backupshare).</span><span class="sxs-lookup"><span data-stu-id="b0cc2-308">For the location, use the [backup share that you created](#backupshare).</span></span> <span data-ttu-id="b0cc2-309">In the example it was, \**\\\\\<First SQL Server\>\Backup\**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-309">In the example it was, \**\\\\\<First SQL Server\>\Backup\**.</span></span> <span data-ttu-id="b0cc2-310">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-310">Click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="b0cc2-311">Full synchronization takes a full backup of the database on the first instance of SQL Server and restores it to the second instance.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-311">Full synchronization takes a full backup of the database on the first instance of SQL Server and restores it to the second instance.</span></span> <span data-ttu-id="b0cc2-312">For large databases, full synchronization is not recommended because it may take a long time.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-312">For large databases, full synchronization is not recommended because it may take a long time.</span></span> <span data-ttu-id="b0cc2-313">You can reduce this time by manually taking a backup of the database and restoring it with `NO RECOVERY`.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-313">You can reduce this time by manually taking a backup of the database and restoring it with `NO RECOVERY`.</span></span> <span data-ttu-id="b0cc2-314">If the database is already restored with `NO RECOVERY` on the second SQL Server before configuring the Availability Group, choose **Join only**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-314">If the database is already restored with `NO RECOVERY` on the second SQL Server before configuring the Availability Group, choose **Join only**.</span></span> <span data-ttu-id="b0cc2-315">If you want to take the backup after configuring the Availability Group, choose **Skip initial data synchronization**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-315">If you want to take the backup after configuring the Availability Group, choose **Skip initial data synchronization**.</span></span>

    ![New AG Wizard, Select Initial Data Synchronization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. <span data-ttu-id="b0cc2-317">In the **Validation** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-317">In the **Validation** page, click **Next**.</span></span> <span data-ttu-id="b0cc2-318">This page should look similar to the following image:</span><span class="sxs-lookup"><span data-stu-id="b0cc2-318">This page should look similar to the following image:</span></span>

    ![New AG Wizard, Validation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    ><span data-ttu-id="b0cc2-320">There is a warning for the listener configuration because you have not configured an Availability Group listener.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-320">There is a warning for the listener configuration because you have not configured an Availability Group listener.</span></span> <span data-ttu-id="b0cc2-321">You can ignore this warning because on Azure virtual machines you create the listener after creating the Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-321">You can ignore this warning because on Azure virtual machines you create the listener after creating the Azure load balancer.</span></span>

10. <span data-ttu-id="b0cc2-322">In the **Summary** page, click **Finish**, then wait while the wizard configures the new Availability Group.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-322">In the **Summary** page, click **Finish**, then wait while the wizard configures the new Availability Group.</span></span> <span data-ttu-id="b0cc2-323">In the **Progress** page, you can click **More details** to view the detailed progress.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-323">In the **Progress** page, you can click **More details** to view the detailed progress.</span></span> <span data-ttu-id="b0cc2-324">Once the wizard is finished, inspect the **Results** page to verify that the Availability Group is successfully created.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-324">Once the wizard is finished, inspect the **Results** page to verify that the Availability Group is successfully created.</span></span>

     ![New AG Wizard, Results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. <span data-ttu-id="b0cc2-326">Click **Close** to exit the wizard.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-326">Click **Close** to exit the wizard.</span></span>

### <a name="check-the-availability-group"></a><span data-ttu-id="b0cc2-327">Check the Availability Group</span><span class="sxs-lookup"><span data-stu-id="b0cc2-327">Check the Availability Group</span></span>

1. <span data-ttu-id="b0cc2-328">In **Object Explorer**, expand **AlwaysOn High Availability**, then expand **Availability Groups**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-328">In **Object Explorer**, expand **AlwaysOn High Availability**, then expand **Availability Groups**.</span></span> <span data-ttu-id="b0cc2-329">You should now see the new Availability Group in this container.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-329">You should now see the new Availability Group in this container.</span></span> <span data-ttu-id="b0cc2-330">Right-click the Availability Group and click **Show Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-330">Right-click the Availability Group and click **Show Dashboard**.</span></span>

   ![Show AG Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   <span data-ttu-id="b0cc2-332">Your **AlwaysOn Dashboard** should look similar to this.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-332">Your **AlwaysOn Dashboard** should look similar to this.</span></span>

   ![AG Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   <span data-ttu-id="b0cc2-334">You can see the replicas, the failover mode of each replica and the synchronization state.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-334">You can see the replicas, the failover mode of each replica and the synchronization state.</span></span>

2. <span data-ttu-id="b0cc2-335">In **Failover Cluster Manager**, click your cluster.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-335">In **Failover Cluster Manager**, click your cluster.</span></span> <span data-ttu-id="b0cc2-336">Select **Roles**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-336">Select **Roles**.</span></span> <span data-ttu-id="b0cc2-337">The Availability Group name you used is a role on the cluster.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-337">The Availability Group name you used is a role on the cluster.</span></span> <span data-ttu-id="b0cc2-338">That Availability Group does not have an IP address for client connections, because you did not configure a listener.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-338">That Availability Group does not have an IP address for client connections, because you did not configure a listener.</span></span> <span data-ttu-id="b0cc2-339">You will configure the listener after you create an Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-339">You will configure the listener after you create an Azure load balancer.</span></span>

   ![AG in Failover Cluster Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > <span data-ttu-id="b0cc2-341">Do not try to fail over the Availability Group from the Failover Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-341">Do not try to fail over the Availability Group from the Failover Cluster Manager.</span></span> <span data-ttu-id="b0cc2-342">All failover operations should be performed from within **AlwaysOn Dashboard** in SSMS.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-342">All failover operations should be performed from within **AlwaysOn Dashboard** in SSMS.</span></span> <span data-ttu-id="b0cc2-343">For more information, see [Restrictions on Using The Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0cc2-343">For more information, see [Restrictions on Using The Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx).</span></span>
    >

<span data-ttu-id="b0cc2-344">At this point, you have an Availability Group with replicas on two instances of SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-344">At this point, you have an Availability Group with replicas on two instances of SQL Server.</span></span> <span data-ttu-id="b0cc2-345">You can move the Availability Group between instances.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-345">You can move the Availability Group between instances.</span></span> <span data-ttu-id="b0cc2-346">You cannot connect to the Availability Group yet because you do not have a listener.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-346">You cannot connect to the Availability Group yet because you do not have a listener.</span></span> <span data-ttu-id="b0cc2-347">In Azure virtual machines, the listener requires a load balancer.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-347">In Azure virtual machines, the listener requires a load balancer.</span></span> <span data-ttu-id="b0cc2-348">The next step is to create the load balancer in Azure.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-348">The next step is to create the load balancer in Azure.</span></span>

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a><span data-ttu-id="b0cc2-349">Create an Azure load balancer</span><span class="sxs-lookup"><span data-stu-id="b0cc2-349">Create an Azure load balancer</span></span>

<span data-ttu-id="b0cc2-350">On Azure virtual machines, a SQL Server Availability Group requires a load balancer.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-350">On Azure virtual machines, a SQL Server Availability Group requires a load balancer.</span></span> <span data-ttu-id="b0cc2-351">The load balancer holds the IP address for the Availability Group listener.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-351">The load balancer holds the IP address for the Availability Group listener.</span></span> <span data-ttu-id="b0cc2-352">This section summarizes how to create the load balancer in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-352">This section summarizes how to create the load balancer in the Azure portal.</span></span>

1. <span data-ttu-id="b0cc2-353">In the Azure portal, go to the resource group where your SQL Servers are and click **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-353">In the Azure portal, go to the resource group where your SQL Servers are and click **+ Add**.</span></span>
2. <span data-ttu-id="b0cc2-354">Search for **Load Balancer**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-354">Search for **Load Balancer**.</span></span> <span data-ttu-id="b0cc2-355">Choose the load balancer published by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-355">Choose the load balancer published by Microsoft.</span></span>

   ![AG in Failover Cluster Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  <span data-ttu-id="b0cc2-357">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-357">Click **Create**.</span></span>
3. <span data-ttu-id="b0cc2-358">Configure the following parameters for the load balancer.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-358">Configure the following parameters for the load balancer.</span></span>

   | <span data-ttu-id="b0cc2-359">Setting</span><span class="sxs-lookup"><span data-stu-id="b0cc2-359">Setting</span></span> | <span data-ttu-id="b0cc2-360">Field</span><span class="sxs-lookup"><span data-stu-id="b0cc2-360">Field</span></span> |
   | --- | --- |
   | <span data-ttu-id="b0cc2-361">**Name**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-361">**Name**</span></span> |<span data-ttu-id="b0cc2-362">Use a text name for the load balancer, for example **sqlLB**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-362">Use a text name for the load balancer, for example **sqlLB**.</span></span> |
   | <span data-ttu-id="b0cc2-363">**Scheme**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-363">**Scheme**</span></span> |<span data-ttu-id="b0cc2-364">Internal</span><span class="sxs-lookup"><span data-stu-id="b0cc2-364">Internal</span></span> |
   | <span data-ttu-id="b0cc2-365">**Virtual network**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-365">**Virtual network**</span></span> |<span data-ttu-id="b0cc2-366">Use the name of the Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-366">Use the name of the Azure virtual network.</span></span> |
   | <span data-ttu-id="b0cc2-367">**Subnet**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-367">**Subnet**</span></span> |<span data-ttu-id="b0cc2-368">Use the name of the subnet that the virtual machine is in.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-368">Use the name of the subnet that the virtual machine is in.</span></span>  |
   | <span data-ttu-id="b0cc2-369">**IP address assignment**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-369">**IP address assignment**</span></span> |<span data-ttu-id="b0cc2-370">Static</span><span class="sxs-lookup"><span data-stu-id="b0cc2-370">Static</span></span> |
   | <span data-ttu-id="b0cc2-371">**IP address**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-371">**IP address**</span></span> |<span data-ttu-id="b0cc2-372">Use an available address from subnet.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-372">Use an available address from subnet.</span></span> |
   | <span data-ttu-id="b0cc2-373">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-373">**Subscription**</span></span> |<span data-ttu-id="b0cc2-374">Use the same subscription as the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-374">Use the same subscription as the virtual machine.</span></span> |
   | <span data-ttu-id="b0cc2-375">**Location**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-375">**Location**</span></span> |<span data-ttu-id="b0cc2-376">Use the same location as the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-376">Use the same location as the virtual machine.</span></span> |

   <span data-ttu-id="b0cc2-377">The Azure portal blade should look like this:</span><span class="sxs-lookup"><span data-stu-id="b0cc2-377">The Azure portal blade should look like this:</span></span>

   ![Create Load Balancer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. <span data-ttu-id="b0cc2-379">Click **Create**, to create the load balancer.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-379">Click **Create**, to create the load balancer.</span></span>

<span data-ttu-id="b0cc2-380">To configure the load balancer, you need to create a backend pool, a probe, and set the load balancing rules.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-380">To configure the load balancer, you need to create a backend pool, a probe, and set the load balancing rules.</span></span> <span data-ttu-id="b0cc2-381">Do these in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-381">Do these in the Azure portal.</span></span>

### <a name="add-backend-pool"></a><span data-ttu-id="b0cc2-382">Add backend pool</span><span class="sxs-lookup"><span data-stu-id="b0cc2-382">Add backend pool</span></span>

1. <span data-ttu-id="b0cc2-383">In the Azure portal, go to your availability group.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-383">In the Azure portal, go to your availability group.</span></span> <span data-ttu-id="b0cc2-384">You might need to refresh the view to see the newly created load balancer.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-384">You might need to refresh the view to see the newly created load balancer.</span></span>

   ![Find Load Balancer in Resource Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. <span data-ttu-id="b0cc2-386">Click the load balancer, click **Backend pools**, and click **+Add**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-386">Click the load balancer, click **Backend pools**, and click **+Add**.</span></span> <span data-ttu-id="b0cc2-387">Set the backend pool as follows:</span><span class="sxs-lookup"><span data-stu-id="b0cc2-387">Set the backend pool as follows:</span></span>

   | <span data-ttu-id="b0cc2-388">Setting</span><span class="sxs-lookup"><span data-stu-id="b0cc2-388">Setting</span></span> | <span data-ttu-id="b0cc2-389">Description</span><span class="sxs-lookup"><span data-stu-id="b0cc2-389">Description</span></span> | <span data-ttu-id="b0cc2-390">Example</span><span class="sxs-lookup"><span data-stu-id="b0cc2-390">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="b0cc2-391">**Name**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-391">**Name**</span></span> | <span data-ttu-id="b0cc2-392">Type a text name</span><span class="sxs-lookup"><span data-stu-id="b0cc2-392">Type a text name</span></span> | <span data-ttu-id="b0cc2-393">SQLLBBE</span><span class="sxs-lookup"><span data-stu-id="b0cc2-393">SQLLBBE</span></span>
   | <span data-ttu-id="b0cc2-394">**Availability set**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-394">**Availability set**</span></span> | <span data-ttu-id="b0cc2-395">Use a name of the availability set that your SQL Server VMs are in</span><span class="sxs-lookup"><span data-stu-id="b0cc2-395">Use a name of the availability set that your SQL Server VMs are in</span></span> | <span data-ttu-id="b0cc2-396">sqlAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="b0cc2-396">sqlAvailabilitySet</span></span> |
   | <span data-ttu-id="b0cc2-397">**Virtual machines**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-397">**Virtual machines**</span></span> |<span data-ttu-id="b0cc2-398">The two Azure SQL Server VM names</span><span class="sxs-lookup"><span data-stu-id="b0cc2-398">The two Azure SQL Server VM names</span></span> | <span data-ttu-id="b0cc2-399">sqlserver-0, sqlserver-1</span><span class="sxs-lookup"><span data-stu-id="b0cc2-399">sqlserver-0, sqlserver-1</span></span>

1. <span data-ttu-id="b0cc2-400">Type the name for the back end pool.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-400">Type the name for the back end pool.</span></span>

1. <span data-ttu-id="b0cc2-401">Click **+ Add a virtual machine**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-401">Click **+ Add a virtual machine**.</span></span>

1. <span data-ttu-id="b0cc2-402">For the availability set, choose the availability set that the SQL Servers are in.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-402">For the availability set, choose the availability set that the SQL Servers are in.</span></span>

1. <span data-ttu-id="b0cc2-403">For virtual machines, include both of the SQL Servers.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-403">For virtual machines, include both of the SQL Servers.</span></span> <span data-ttu-id="b0cc2-404">Do not include the file share witness server.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-404">Do not include the file share witness server.</span></span> <span data-ttu-id="b0cc2-405">Your selection should look similar to the following picture:</span><span class="sxs-lookup"><span data-stu-id="b0cc2-405">Your selection should look similar to the following picture:</span></span>

   ![Find Load Balancer in Resource Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-portal-sql-availability-group-tutorial/88-configurebepool.png)

1. <span data-ttu-id="b0cc2-407">Click **OK** to create the backend pool.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-407">Click **OK** to create the backend pool.</span></span>

### <a name="set-the-probe"></a><span data-ttu-id="b0cc2-408">Set the probe</span><span class="sxs-lookup"><span data-stu-id="b0cc2-408">Set the probe</span></span>

1. <span data-ttu-id="b0cc2-409">Click the load balancer, click **Health probes**, and click **+Add**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-409">Click the load balancer, click **Health probes**, and click **+Add**.</span></span>

1. <span data-ttu-id="b0cc2-410">Set the health probe as follows:</span><span class="sxs-lookup"><span data-stu-id="b0cc2-410">Set the health probe as follows:</span></span>

   | <span data-ttu-id="b0cc2-411">Setting</span><span class="sxs-lookup"><span data-stu-id="b0cc2-411">Setting</span></span> | <span data-ttu-id="b0cc2-412">Description</span><span class="sxs-lookup"><span data-stu-id="b0cc2-412">Description</span></span> | <span data-ttu-id="b0cc2-413">Example</span><span class="sxs-lookup"><span data-stu-id="b0cc2-413">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="b0cc2-414">**Name**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-414">**Name**</span></span> | <span data-ttu-id="b0cc2-415">Text</span><span class="sxs-lookup"><span data-stu-id="b0cc2-415">Text</span></span> | <span data-ttu-id="b0cc2-416">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="b0cc2-416">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="b0cc2-417">**Protocol**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-417">**Protocol**</span></span> | <span data-ttu-id="b0cc2-418">Choose TCP</span><span class="sxs-lookup"><span data-stu-id="b0cc2-418">Choose TCP</span></span> | <span data-ttu-id="b0cc2-419">TCP</span><span class="sxs-lookup"><span data-stu-id="b0cc2-419">TCP</span></span> |
   | <span data-ttu-id="b0cc2-420">**Port**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-420">**Port**</span></span> | <span data-ttu-id="b0cc2-421">Any unused port</span><span class="sxs-lookup"><span data-stu-id="b0cc2-421">Any unused port</span></span> | <span data-ttu-id="b0cc2-422">59999</span><span class="sxs-lookup"><span data-stu-id="b0cc2-422">59999</span></span> |
   | <span data-ttu-id="b0cc2-423">**Interval**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-423">**Interval**</span></span>  | <span data-ttu-id="b0cc2-424">The amount of time between probe attempts in seconds</span><span class="sxs-lookup"><span data-stu-id="b0cc2-424">The amount of time between probe attempts in seconds</span></span> |<span data-ttu-id="b0cc2-425">5</span><span class="sxs-lookup"><span data-stu-id="b0cc2-425">5</span></span> |
   | <span data-ttu-id="b0cc2-426">**Unhealthy threshold**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-426">**Unhealthy threshold**</span></span> | <span data-ttu-id="b0cc2-427">The number of consecutive probe failures that must occur for a virtual machine to be considered unhealthy</span><span class="sxs-lookup"><span data-stu-id="b0cc2-427">The number of consecutive probe failures that must occur for a virtual machine to be considered unhealthy</span></span>  | <span data-ttu-id="b0cc2-428">2</span><span class="sxs-lookup"><span data-stu-id="b0cc2-428">2</span></span> |

1. <span data-ttu-id="b0cc2-429">Click **OK** to set the health probe.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-429">Click **OK** to set the health probe.</span></span>

### <a name="set-the-load-balancing-rules"></a><span data-ttu-id="b0cc2-430">Set the load balancing rules</span><span class="sxs-lookup"><span data-stu-id="b0cc2-430">Set the load balancing rules</span></span>

1. <span data-ttu-id="b0cc2-431">Click the load balancer, click **Load balancing rules**, and click **+Add**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-431">Click the load balancer, click **Load balancing rules**, and click **+Add**.</span></span>

1. <span data-ttu-id="b0cc2-432">Set the load balancing rules as follows.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-432">Set the load balancing rules as follows.</span></span>
   | <span data-ttu-id="b0cc2-433">Setting</span><span class="sxs-lookup"><span data-stu-id="b0cc2-433">Setting</span></span> | <span data-ttu-id="b0cc2-434">Description</span><span class="sxs-lookup"><span data-stu-id="b0cc2-434">Description</span></span> | <span data-ttu-id="b0cc2-435">Example</span><span class="sxs-lookup"><span data-stu-id="b0cc2-435">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="b0cc2-436">**Name**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-436">**Name**</span></span> | <span data-ttu-id="b0cc2-437">Text</span><span class="sxs-lookup"><span data-stu-id="b0cc2-437">Text</span></span> | <span data-ttu-id="b0cc2-438">SQLAlwaysOnEndPointListener</span><span class="sxs-lookup"><span data-stu-id="b0cc2-438">SQLAlwaysOnEndPointListener</span></span> |
   | <span data-ttu-id="b0cc2-439">**Frontend IP address**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-439">**Frontend IP address**</span></span> | <span data-ttu-id="b0cc2-440">Choose an address</span><span class="sxs-lookup"><span data-stu-id="b0cc2-440">Choose an address</span></span> |<span data-ttu-id="b0cc2-441">Use the address that you created when you created the load balancer.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-441">Use the address that you created when you created the load balancer.</span></span> |
   | <span data-ttu-id="b0cc2-442">**Protocol**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-442">**Protocol**</span></span> | <span data-ttu-id="b0cc2-443">Choose TCP</span><span class="sxs-lookup"><span data-stu-id="b0cc2-443">Choose TCP</span></span> |<span data-ttu-id="b0cc2-444">TCP</span><span class="sxs-lookup"><span data-stu-id="b0cc2-444">TCP</span></span> |
   | <span data-ttu-id="b0cc2-445">**Port**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-445">**Port**</span></span> | <span data-ttu-id="b0cc2-446">Use the port for the SQL Server instance</span><span class="sxs-lookup"><span data-stu-id="b0cc2-446">Use the port for the SQL Server instance</span></span> | <span data-ttu-id="b0cc2-447">1433</span><span class="sxs-lookup"><span data-stu-id="b0cc2-447">1433</span></span> |
   | <span data-ttu-id="b0cc2-448">**Backend Port**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-448">**Backend Port**</span></span> | <span data-ttu-id="b0cc2-449">This field is not used when Floating IP is set for direct server return</span><span class="sxs-lookup"><span data-stu-id="b0cc2-449">This field is not used when Floating IP is set for direct server return</span></span> | <span data-ttu-id="b0cc2-450">1433</span><span class="sxs-lookup"><span data-stu-id="b0cc2-450">1433</span></span> |
   | <span data-ttu-id="b0cc2-451">**Probe**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-451">**Probe**</span></span> |<span data-ttu-id="b0cc2-452">The name you specified for the probe</span><span class="sxs-lookup"><span data-stu-id="b0cc2-452">The name you specified for the probe</span></span> | <span data-ttu-id="b0cc2-453">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="b0cc2-453">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="b0cc2-454">**Session Persistence**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-454">**Session Persistence**</span></span> | <span data-ttu-id="b0cc2-455">Drop down list</span><span class="sxs-lookup"><span data-stu-id="b0cc2-455">Drop down list</span></span> | <span data-ttu-id="b0cc2-456">**None**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-456">**None**</span></span> |
   | <span data-ttu-id="b0cc2-457">**Idle Timeout**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-457">**Idle Timeout**</span></span> | <span data-ttu-id="b0cc2-458">Minutes to keep a TCP connection open</span><span class="sxs-lookup"><span data-stu-id="b0cc2-458">Minutes to keep a TCP connection open</span></span> | <span data-ttu-id="b0cc2-459">4</span><span class="sxs-lookup"><span data-stu-id="b0cc2-459">4</span></span> |
   | <span data-ttu-id="b0cc2-460">**Floating IP (direct server return)**</span><span class="sxs-lookup"><span data-stu-id="b0cc2-460">**Floating IP (direct server return)**</span></span> | |<span data-ttu-id="b0cc2-461">Enabled</span><span class="sxs-lookup"><span data-stu-id="b0cc2-461">Enabled</span></span> |

   > [!WARNING]
   > <span data-ttu-id="b0cc2-462">Direct server return is set during creation.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-462">Direct server return is set during creation.</span></span> <span data-ttu-id="b0cc2-463">It cannot be changed.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-463">It cannot be changed.</span></span>

1. <span data-ttu-id="b0cc2-464">Click **OK** to set the load balancing rules.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-464">Click **OK** to set the load balancing rules.</span></span>

## <a name="configure-listener"></a> <span data-ttu-id="b0cc2-465">Configure the listener</span><span class="sxs-lookup"><span data-stu-id="b0cc2-465">Configure the listener</span></span>

<span data-ttu-id="b0cc2-466">The next thing to do is to configure an Availability Group listener on the failover cluster.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-466">The next thing to do is to configure an Availability Group listener on the failover cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="b0cc2-467">This tutorial shows how to create a single listener - with one ILB IP address.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-467">This tutorial shows how to create a single listener - with one ILB IP address.</span></span> <span data-ttu-id="b0cc2-468">To create one or more listeners using one or more IP addresses, see [Create Availability Group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b0cc2-468">To create one or more listeners using one or more IP addresses, see [Create Availability Group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a><span data-ttu-id="b0cc2-469">Set listener port</span><span class="sxs-lookup"><span data-stu-id="b0cc2-469">Set listener port</span></span>

<span data-ttu-id="b0cc2-470">In SQL Server Management Studio, set the listener port.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-470">In SQL Server Management Studio, set the listener port.</span></span>

1. <span data-ttu-id="b0cc2-471">Launch SQL Server Management Studio and connect to the primary replica.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-471">Launch SQL Server Management Studio and connect to the primary replica.</span></span>

1. <span data-ttu-id="b0cc2-472">Navigate to **AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-472">Navigate to **AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span>

1. <span data-ttu-id="b0cc2-473">You should now see the listener name that you created in Failover Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-473">You should now see the listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="b0cc2-474">Right-click the listener name and click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-474">Right-click the listener name and click **Properties**.</span></span>

1. <span data-ttu-id="b0cc2-475">In the **Port** box, specify the port number for the Availability Group listener by using the $EndpointPort you used earlier (1433 was the default), then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-475">In the **Port** box, specify the port number for the Availability Group listener by using the $EndpointPort you used earlier (1433 was the default), then click **OK**.</span></span>

<span data-ttu-id="b0cc2-476">You now have a SQL Server Availability Group in Azure virtual machines running in Resource Manager mode.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-476">You now have a SQL Server Availability Group in Azure virtual machines running in Resource Manager mode.</span></span>

## <a name="test-connection-to-listener"></a><span data-ttu-id="b0cc2-477">Test connection to listener</span><span class="sxs-lookup"><span data-stu-id="b0cc2-477">Test connection to listener</span></span>

<span data-ttu-id="b0cc2-478">To test the connection:</span><span class="sxs-lookup"><span data-stu-id="b0cc2-478">To test the connection:</span></span>

1. <span data-ttu-id="b0cc2-479">RDP to a SQL Server that is in the same virtual network, but does not own the replica.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-479">RDP to a SQL Server that is in the same virtual network, but does not own the replica.</span></span> <span data-ttu-id="b0cc2-480">You can use the other SQL Server in the cluster.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-480">You can use the other SQL Server in the cluster.</span></span>

1. <span data-ttu-id="b0cc2-481">Use **sqlcmd** utility to test the connection.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-481">Use **sqlcmd** utility to test the connection.</span></span> <span data-ttu-id="b0cc2-482">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span><span class="sxs-lookup"><span data-stu-id="b0cc2-482">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span></span>

    ```
    sqlmd -S <listenerName> -E
    ```

    <span data-ttu-id="b0cc2-483">If the listener is using a port other than the default port (1433), specify the port in the connection string.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-483">If the listener is using a port other than the default port (1433), specify the port in the connection string.</span></span> <span data-ttu-id="b0cc2-484">For example, the following sqlcmd command connects to a listener at port 1435:</span><span class="sxs-lookup"><span data-stu-id="b0cc2-484">For example, the following sqlcmd command connects to a listener at port 1435:</span></span>

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="b0cc2-485">The SQLCMD connection automatically connects to whichever instance of SQL Server hosts the primary replica.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-485">The SQLCMD connection automatically connects to whichever instance of SQL Server hosts the primary replica.</span></span>

> [!TIP]
> <span data-ttu-id="b0cc2-486">Make sure that the port you specify is open on the firewall of both SQL Servers.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-486">Make sure that the port you specify is open on the firewall of both SQL Servers.</span></span> <span data-ttu-id="b0cc2-487">Both servers require an inbound rule for the TCP port that you use.</span><span class="sxs-lookup"><span data-stu-id="b0cc2-487">Both servers require an inbound rule for the TCP port that you use.</span></span> <span data-ttu-id="b0cc2-488">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0cc2-488">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span>
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by the way” info, an Important is info users need to complete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is the second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note the format for documenting the UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult to maintain. Highlight areas you are referring to in red.*-->

<!--**No. of steps**: *Make sure the number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want to go on.*-->

## <a name="next-steps"></a><span data-ttu-id="b0cc2-489">Next steps</span><span class="sxs-lookup"><span data-stu-id="b0cc2-489">Next steps</span></span>

- <span data-ttu-id="b0cc2-490">[Add an IP address to a load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span><span class="sxs-lookup"><span data-stu-id="b0cc2-490">[Add an IP address to a load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span></span>


































