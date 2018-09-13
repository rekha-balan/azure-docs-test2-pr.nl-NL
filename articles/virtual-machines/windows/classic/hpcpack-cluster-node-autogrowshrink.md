---
title: Autoscale HPC Pack cluster nodes | Microsoft Docs
description: Automatically grow and shrink the number of HPC Pack cluster compute nodes in Azure
services: virtual-machines-windows
documentationcenter: ''
author: dlepow
manager: ''
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: f43c4f62697c2df716da56e5f95400eec8d9653b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550103"
---
# <a name="automatically-grow-and-shrink-the-hpc-pack-cluster-resources-in-azure-according-to-the-cluster-workload"></a><span data-ttu-id="9a957-103">Automatically grow and shrink the HPC Pack cluster resources in Azure according to the cluster workload</span><span class="sxs-lookup"><span data-stu-id="9a957-103">Automatically grow and shrink the HPC Pack cluster resources in Azure according to the cluster workload</span></span>
<span data-ttu-id="9a957-104">If you deploy Azure “burst” nodes in your HPC Pack cluster, or you create an HPC Pack cluster in Azure VMs, you may want a way to automatically grow or shrink the cluster resources such as nodes or cores according to the workload on the cluster.</span><span class="sxs-lookup"><span data-stu-id="9a957-104">If you deploy Azure “burst” nodes in your HPC Pack cluster, or you create an HPC Pack cluster in Azure VMs, you may want a way to automatically grow or shrink the cluster resources such as nodes or cores according to the workload on the cluster.</span></span> <span data-ttu-id="9a957-105">Scaling the cluster resources in this way allows you to use your Azure resources more efficiently and control their costs.</span><span class="sxs-lookup"><span data-stu-id="9a957-105">Scaling the cluster resources in this way allows you to use your Azure resources more efficiently and control their costs.</span></span>

<span data-ttu-id="9a957-106">This article shows you two ways that HPC Pack provides to autoscale compute resources:</span><span class="sxs-lookup"><span data-stu-id="9a957-106">This article shows you two ways that HPC Pack provides to autoscale compute resources:</span></span>

* <span data-ttu-id="9a957-107">The HPC Pack cluster property **AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="9a957-107">The HPC Pack cluster property **AutoGrowShrink**</span></span>

* <span data-ttu-id="9a957-108">The **AzureAutoGrowShrink.ps1** HPC PowerShell script</span><span class="sxs-lookup"><span data-stu-id="9a957-108">The **AzureAutoGrowShrink.ps1** HPC PowerShell script</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="9a957-109">Currently you can only automatically grow and shrink HPC Pack compute nodes that are running a Windows Server operating system.</span><span class="sxs-lookup"><span data-stu-id="9a957-109">Currently you can only automatically grow and shrink HPC Pack compute nodes that are running a Windows Server operating system.</span></span>


## <a name="set-the-autogrowshrink-cluster-property"></a><span data-ttu-id="9a957-110">Set the AutoGrowShrink cluster property</span><span class="sxs-lookup"><span data-stu-id="9a957-110">Set the AutoGrowShrink cluster property</span></span>
### <a name="prerequisites"></a><span data-ttu-id="9a957-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9a957-111">Prerequisites</span></span>

* <span data-ttu-id="9a957-112">**HPC Pack 2012 R2 Update 2 or later cluster** - The cluster head node can be deployed either on-premises or in an Azure VM.</span><span class="sxs-lookup"><span data-stu-id="9a957-112">**HPC Pack 2012 R2 Update 2 or later cluster** - The cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="9a957-113">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) to get started with an on-premises head node and Azure "burst" nodes.</span><span class="sxs-lookup"><span data-stu-id="9a957-113">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) to get started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="9a957-114">See the [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) to quickly deploy an HPC Pack cluster in Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="9a957-114">See the [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) to quickly deploy an HPC Pack cluster in Azure VMs.</span></span>

* <span data-ttu-id="9a957-115">**For a cluster with a head node in Azure (Resource Manager deployment model)** - Starting in HPC Pack 2016, certificate authentication in an Azure Active Directory application is used for automatically growing and shrinking cluster VMs deployed using Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9a957-115">**For a cluster with a head node in Azure (Resource Manager deployment model)** - Starting in HPC Pack 2016, certificate authentication in an Azure Active Directory application is used for automatically growing and shrinking cluster VMs deployed using Azure Resource Manager.</span></span> <span data-ttu-id="9a957-116">Configure a certificate as follows:</span><span class="sxs-lookup"><span data-stu-id="9a957-116">Configure a certificate as follows:</span></span>

  1. <span data-ttu-id="9a957-117">After cluster deployment, connect by Remote Desktop to one head node.</span><span class="sxs-lookup"><span data-stu-id="9a957-117">After cluster deployment, connect by Remote Desktop to one head node.</span></span>

  2. <span data-ttu-id="9a957-118">Upload the certificate (PFX format with private key) to each head node and install to Cert:\LocalMachine\My and Cert:\LocalMachine\Root.</span><span class="sxs-lookup"><span data-stu-id="9a957-118">Upload the certificate (PFX format with private key) to each head node and install to Cert:\LocalMachine\My and Cert:\LocalMachine\Root.</span></span>

  3. <span data-ttu-id="9a957-119">Start Azure PowerShell as an administrator and run the following commands on one head node:</span><span class="sxs-lookup"><span data-stu-id="9a957-119">Start Azure PowerShell as an administrator and run the following commands on one head node:</span></span>

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    <span data-ttu-id="9a957-120">If your account is in more than one Azure Active Directory tenant or Azure subscription, you can run the following command to select the correct tenant and subscription:</span><span class="sxs-lookup"><span data-stu-id="9a957-120">If your account is in more than one Azure Active Directory tenant or Azure subscription, you can run the following command to select the correct tenant and subscription:</span></span>
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    <span data-ttu-id="9a957-121">Run the following command to view the currently selected tenant and subscription:</span><span class="sxs-lookup"><span data-stu-id="9a957-121">Run the following command to view the currently selected tenant and subscription:</span></span>
    
    ```powershell
        Get-AzureRMContext
    ```

  4. <span data-ttu-id="9a957-122">Run the following script</span><span class="sxs-lookup"><span data-stu-id="9a957-122">Run the following script</span></span>

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    <span data-ttu-id="9a957-123">where</span><span class="sxs-lookup"><span data-stu-id="9a957-123">where</span></span>

    <span data-ttu-id="9a957-124">**DisplayName** - Azure Active Application display name.</span><span class="sxs-lookup"><span data-stu-id="9a957-124">**DisplayName** - Azure Active Application display name.</span></span> <span data-ttu-id="9a957-125">If the application does not exist, it is created in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9a957-125">If the application does not exist, it is created in Azure Active Directory.</span></span>

    <span data-ttu-id="9a957-126">**HomePage** - The home page of the application.</span><span class="sxs-lookup"><span data-stu-id="9a957-126">**HomePage** - The home page of the application.</span></span> <span data-ttu-id="9a957-127">You can configure a dummy URL, as in the preceding example.</span><span class="sxs-lookup"><span data-stu-id="9a957-127">You can configure a dummy URL, as in the preceding example.</span></span>

    <span data-ttu-id="9a957-128">**IdentifierUri** - Identifier of the application.</span><span class="sxs-lookup"><span data-stu-id="9a957-128">**IdentifierUri** - Identifier of the application.</span></span> <span data-ttu-id="9a957-129">You can configure a dummy URL, as in the preceding example.</span><span class="sxs-lookup"><span data-stu-id="9a957-129">You can configure a dummy URL, as in the preceding example.</span></span>

    <span data-ttu-id="9a957-130">**CertificateThumbprint** - Thumbprint of the certificate you installed on the head node in Step 1.</span><span class="sxs-lookup"><span data-stu-id="9a957-130">**CertificateThumbprint** - Thumbprint of the certificate you installed on the head node in Step 1.</span></span>

    <span data-ttu-id="9a957-131">**TenantId** - Tenant ID of your Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9a957-131">**TenantId** - Tenant ID of your Azure Active Directory.</span></span> <span data-ttu-id="9a957-132">You can get the Tenant ID from the Azure Active Directory portal **Properties** page.</span><span class="sxs-lookup"><span data-stu-id="9a957-132">You can get the Tenant ID from the Azure Active Directory portal **Properties** page.</span></span>

    <span data-ttu-id="9a957-133">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span><span class="sxs-lookup"><span data-stu-id="9a957-133">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span></span>


* <span data-ttu-id="9a957-134">**For a cluster with a head node in Azure (classic deployment model)** - If you use the HPC Pack IaaS deployment script to create the cluster in the classic deployment model, enable the **AutoGrowShrink** cluster property by setting the AutoGrowShrink option in the cluster configuration file.</span><span class="sxs-lookup"><span data-stu-id="9a957-134">**For a cluster with a head node in Azure (classic deployment model)** - If you use the HPC Pack IaaS deployment script to create the cluster in the classic deployment model, enable the **AutoGrowShrink** cluster property by setting the AutoGrowShrink option in the cluster configuration file.</span></span> <span data-ttu-id="9a957-135">For details, see the documentation accompanying the [script download](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="9a957-135">For details, see the documentation accompanying the [script download](https://www.microsoft.com/download/details.aspx?id=44949).</span></span>

    <span data-ttu-id="9a957-136">Alternatively, enable the **AutoGrowShrink** cluster property after you deploy the cluster by using HPC PowerShell commands described in the following section.</span><span class="sxs-lookup"><span data-stu-id="9a957-136">Alternatively, enable the **AutoGrowShrink** cluster property after you deploy the cluster by using HPC PowerShell commands described in the following section.</span></span> <span data-ttu-id="9a957-137">To prepare for this, first complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="9a957-137">To prepare for this, first complete the following steps:</span></span>

  1. <span data-ttu-id="9a957-138">Configure an Azure management certificate on the head node and in the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="9a957-138">Configure an Azure management certificate on the head node and in the Azure subscription.</span></span> <span data-ttu-id="9a957-139">For a test deployment, you can use the Default Microsoft HPC Azure self-signed certificate that HPC Pack installs on the head node, and then upload that certificate to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="9a957-139">For a test deployment, you can use the Default Microsoft HPC Azure self-signed certificate that HPC Pack installs on the head node, and then upload that certificate to your Azure subscription.</span></span> <span data-ttu-id="9a957-140">For options and steps, see the [TechNet Library guidance](https://technet.microsoft.com/library/gg481759.aspx).</span><span class="sxs-lookup"><span data-stu-id="9a957-140">For options and steps, see the [TechNet Library guidance](https://technet.microsoft.com/library/gg481759.aspx).</span></span>

  2. <span data-ttu-id="9a957-141">Run **regedit** on the head node, go to HKLM\SOFTWARE\Micorsoft\HPC\IaasInfo, and add a string value.</span><span class="sxs-lookup"><span data-stu-id="9a957-141">Run **regedit** on the head node, go to HKLM\SOFTWARE\Micorsoft\HPC\IaasInfo, and add a string value.</span></span> <span data-ttu-id="9a957-142">Set the Value name to “ThumbPrint”, and Value data to the thumbprint of the certificate in Step 1.</span><span class="sxs-lookup"><span data-stu-id="9a957-142">Set the Value name to “ThumbPrint”, and Value data to the thumbprint of the certificate in Step 1.</span></span>

### <a name="hpc-powershell-commands-to-set-the-autogrowshrink-property"></a><span data-ttu-id="9a957-143">HPC PowerShell commands to set the AutoGrowShrink property</span><span class="sxs-lookup"><span data-stu-id="9a957-143">HPC PowerShell commands to set the AutoGrowShrink property</span></span>
<span data-ttu-id="9a957-144">Following are sample HPC PowerShell commands to set **AutoGrowShrink** and to tune its behavior with additional parameters.</span><span class="sxs-lookup"><span data-stu-id="9a957-144">Following are sample HPC PowerShell commands to set **AutoGrowShrink** and to tune its behavior with additional parameters.</span></span> <span data-ttu-id="9a957-145">See [AutoGrowShrink parameters](#AutoGrowShrink-parameters) later in this article for the complete list of settings.</span><span class="sxs-lookup"><span data-stu-id="9a957-145">See [AutoGrowShrink parameters](#AutoGrowShrink-parameters) later in this article for the complete list of settings.</span></span>

<span data-ttu-id="9a957-146">To run these commands, start HPC PowerShell on the cluster head node as an administrator.</span><span class="sxs-lookup"><span data-stu-id="9a957-146">To run these commands, start HPC PowerShell on the cluster head node as an administrator.</span></span>

<span data-ttu-id="9a957-147">**To enable the AutoGrowShrink property**</span><span class="sxs-lookup"><span data-stu-id="9a957-147">**To enable the AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

<span data-ttu-id="9a957-148">**To disable the AutoGrowShrink property**</span><span class="sxs-lookup"><span data-stu-id="9a957-148">**To disable the AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

<span data-ttu-id="9a957-149">**To change the grow interval in minutes**</span><span class="sxs-lookup"><span data-stu-id="9a957-149">**To change the grow interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

<span data-ttu-id="9a957-150">**To change the shrink interval in minutes**</span><span class="sxs-lookup"><span data-stu-id="9a957-150">**To change the shrink interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

<span data-ttu-id="9a957-151">**To view the current configuration of AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="9a957-151">**To view the current configuration of AutoGrowShrink**</span></span>

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

<span data-ttu-id="9a957-152">**To exclude node groups from AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="9a957-152">**To exclude node groups from AutoGrowShrink**</span></span>

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> <span data-ttu-id="9a957-153">This parameter is supported starting in HPC Pack 2016</span><span class="sxs-lookup"><span data-stu-id="9a957-153">This parameter is supported starting in HPC Pack 2016</span></span>
>

### <a name="autogrowshrink-parameters"></a><span data-ttu-id="9a957-154">AutoGrowShrink parameters</span><span class="sxs-lookup"><span data-stu-id="9a957-154">AutoGrowShrink parameters</span></span>
<span data-ttu-id="9a957-155">The following are AutoGrowShrink parameters that you can modify by using the **Set-HpcClusterProperty** command.</span><span class="sxs-lookup"><span data-stu-id="9a957-155">The following are AutoGrowShrink parameters that you can modify by using the **Set-HpcClusterProperty** command.</span></span>

* <span data-ttu-id="9a957-156">**EnableGrowShrink** - Switch to enable or disable the **AutoGrowShrink** property.</span><span class="sxs-lookup"><span data-stu-id="9a957-156">**EnableGrowShrink** - Switch to enable or disable the **AutoGrowShrink** property.</span></span>
* <span data-ttu-id="9a957-157">**ParamSweepTasksPerCore** - Number of parametric sweep tasks to grow one core.</span><span class="sxs-lookup"><span data-stu-id="9a957-157">**ParamSweepTasksPerCore** - Number of parametric sweep tasks to grow one core.</span></span> <span data-ttu-id="9a957-158">The default is to grow one core per task.</span><span class="sxs-lookup"><span data-stu-id="9a957-158">The default is to grow one core per task.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9a957-159">HPC Pack QFE KB3134307 changes **ParamSweepTasksPerCore** to **TasksPerResourceUnit**.</span><span class="sxs-lookup"><span data-stu-id="9a957-159">HPC Pack QFE KB3134307 changes **ParamSweepTasksPerCore** to **TasksPerResourceUnit**.</span></span> <span data-ttu-id="9a957-160">It is based on the job resource type and can be node, socket, or core.</span><span class="sxs-lookup"><span data-stu-id="9a957-160">It is based on the job resource type and can be node, socket, or core.</span></span>
  >
  >
* <span data-ttu-id="9a957-161">**GrowThreshold** - Threshold of queued tasks to trigger automatic growth.</span><span class="sxs-lookup"><span data-stu-id="9a957-161">**GrowThreshold** - Threshold of queued tasks to trigger automatic growth.</span></span> <span data-ttu-id="9a957-162">The default is 1, which means that if there are 1 or more tasks in the queued state, automatically grow nodes.</span><span class="sxs-lookup"><span data-stu-id="9a957-162">The default is 1, which means that if there are 1 or more tasks in the queued state, automatically grow nodes.</span></span>
* <span data-ttu-id="9a957-163">**GrowInterval** - Interval in minutes to trigger automatic growth.</span><span class="sxs-lookup"><span data-stu-id="9a957-163">**GrowInterval** - Interval in minutes to trigger automatic growth.</span></span> <span data-ttu-id="9a957-164">The default interval is 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="9a957-164">The default interval is 5 minutes.</span></span>
* <span data-ttu-id="9a957-165">**ShrinkInterval** - Interval in minutes to trigger automatic shrinking.</span><span class="sxs-lookup"><span data-stu-id="9a957-165">**ShrinkInterval** - Interval in minutes to trigger automatic shrinking.</span></span> <span data-ttu-id="9a957-166">The default interval is 5 minutes.|</span><span class="sxs-lookup"><span data-stu-id="9a957-166">The default interval is 5 minutes.|</span></span>
* <span data-ttu-id="9a957-167">**ShrinkIdleTimes** - Number of continuous checks to shrink to indicate the nodes are idle.</span><span class="sxs-lookup"><span data-stu-id="9a957-167">**ShrinkIdleTimes** - Number of continuous checks to shrink to indicate the nodes are idle.</span></span> <span data-ttu-id="9a957-168">The default is 3 times.</span><span class="sxs-lookup"><span data-stu-id="9a957-168">The default is 3 times.</span></span> <span data-ttu-id="9a957-169">For example, if the **ShrinkInterval** is 5 minutes, HPC Pack checks whether the node is idle every 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="9a957-169">For example, if the **ShrinkInterval** is 5 minutes, HPC Pack checks whether the node is idle every 5 minutes.</span></span> <span data-ttu-id="9a957-170">If the nodes are in the idle state after 3 continuous checks (15 minutes), then HPC Pack shrinks that node.</span><span class="sxs-lookup"><span data-stu-id="9a957-170">If the nodes are in the idle state after 3 continuous checks (15 minutes), then HPC Pack shrinks that node.</span></span>
* <span data-ttu-id="9a957-171">**ExtraNodesGrowRatio** - Additional percentage of nodes to grow for Message Passing Interface (MPI) jobs.</span><span class="sxs-lookup"><span data-stu-id="9a957-171">**ExtraNodesGrowRatio** - Additional percentage of nodes to grow for Message Passing Interface (MPI) jobs.</span></span> <span data-ttu-id="9a957-172">The default value is 1, which means that HPC Pack grows nodes 1% for MPI jobs.</span><span class="sxs-lookup"><span data-stu-id="9a957-172">The default value is 1, which means that HPC Pack grows nodes 1% for MPI jobs.</span></span>
* <span data-ttu-id="9a957-173">**GrowByMin** - Switch to indicate whether the autogrow policy is based on the minimum resources required for the job.</span><span class="sxs-lookup"><span data-stu-id="9a957-173">**GrowByMin** - Switch to indicate whether the autogrow policy is based on the minimum resources required for the job.</span></span> <span data-ttu-id="9a957-174">The default is false, which means that HPC Pack grows nodes for jobs based on the maximum resources required for the jobs.</span><span class="sxs-lookup"><span data-stu-id="9a957-174">The default is false, which means that HPC Pack grows nodes for jobs based on the maximum resources required for the jobs.</span></span>
* <span data-ttu-id="9a957-175">**SoaJobGrowThreshold** - Threshold of incoming SOA requests to trigger the automatic grow process.</span><span class="sxs-lookup"><span data-stu-id="9a957-175">**SoaJobGrowThreshold** - Threshold of incoming SOA requests to trigger the automatic grow process.</span></span> <span data-ttu-id="9a957-176">The default value is 50000.</span><span class="sxs-lookup"><span data-stu-id="9a957-176">The default value is 50000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9a957-177">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="9a957-177">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
  >
* <span data-ttu-id="9a957-178">**SoaRequestsPerCore** -Number of incoming SOA requests to grow one core.</span><span class="sxs-lookup"><span data-stu-id="9a957-178">**SoaRequestsPerCore** -Number of incoming SOA requests to grow one core.</span></span> <span data-ttu-id="9a957-179">The default value is 20000.</span><span class="sxs-lookup"><span data-stu-id="9a957-179">The default value is 20000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9a957-180">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="9a957-180">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
* <span data-ttu-id="9a957-181">**ExcludeNodeGroups** – Nodes in the specified node groups do not automatically grow and shrink.</span><span class="sxs-lookup"><span data-stu-id="9a957-181">**ExcludeNodeGroups** – Nodes in the specified node groups do not automatically grow and shrink.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="9a957-182">This parameter is supported starting in HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="9a957-182">This parameter is supported starting in HPC Pack 2016.</span></span>
  >

### <a name="mpi-example"></a><span data-ttu-id="9a957-183">MPI example</span><span class="sxs-lookup"><span data-stu-id="9a957-183">MPI example</span></span>
<span data-ttu-id="9a957-184">By default HPC Pack grows 1% extra nodes for MPI jobs (**ExtraNodesGrowRatio** is set to 1).</span><span class="sxs-lookup"><span data-stu-id="9a957-184">By default HPC Pack grows 1% extra nodes for MPI jobs (**ExtraNodesGrowRatio** is set to 1).</span></span> <span data-ttu-id="9a957-185">The reason is that MPI may require multiple nodes, and the job can only run when all nodes are ready.</span><span class="sxs-lookup"><span data-stu-id="9a957-185">The reason is that MPI may require multiple nodes, and the job can only run when all nodes are ready.</span></span> <span data-ttu-id="9a957-186">When Azure starts nodes, occasionally one node might need more time to start than others, causing other nodes to be idle while waiting for that node to get ready.</span><span class="sxs-lookup"><span data-stu-id="9a957-186">When Azure starts nodes, occasionally one node might need more time to start than others, causing other nodes to be idle while waiting for that node to get ready.</span></span> <span data-ttu-id="9a957-187">By growing extra nodes, HPC Pack reduces this resource waiting time, and potentially saves costs.</span><span class="sxs-lookup"><span data-stu-id="9a957-187">By growing extra nodes, HPC Pack reduces this resource waiting time, and potentially saves costs.</span></span> <span data-ttu-id="9a957-188">To increase the percentage of extra nodes for MPI jobs (for example, to 10%), run a command similar to</span><span class="sxs-lookup"><span data-stu-id="9a957-188">To increase the percentage of extra nodes for MPI jobs (for example, to 10%), run a command similar to</span></span>

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a><span data-ttu-id="9a957-189">SOA example</span><span class="sxs-lookup"><span data-stu-id="9a957-189">SOA example</span></span>
<span data-ttu-id="9a957-190">By default, **SoaJobGrowThreshold** is set to 50000 and **SoaRequestsPerCore** is set to 200000.</span><span class="sxs-lookup"><span data-stu-id="9a957-190">By default, **SoaJobGrowThreshold** is set to 50000 and **SoaRequestsPerCore** is set to 200000.</span></span> <span data-ttu-id="9a957-191">If you submit one SOA job with 70000 requests, there is one queued task and incoming requests are 70000.</span><span class="sxs-lookup"><span data-stu-id="9a957-191">If you submit one SOA job with 70000 requests, there is one queued task and incoming requests are 70000.</span></span> <span data-ttu-id="9a957-192">In this case HPC Pack grows 1 core for the queued task, and for incoming requests, grows (70000 - 50000)/20000 = 1 core, so in total grows 2 cores for this SOA job.</span><span class="sxs-lookup"><span data-stu-id="9a957-192">In this case HPC Pack grows 1 core for the queued task, and for incoming requests, grows (70000 - 50000)/20000 = 1 core, so in total grows 2 cores for this SOA job.</span></span>

## <a name="run-the-azureautogrowshrinkps1-script"></a><span data-ttu-id="9a957-193">Run the AzureAutoGrowShrink.ps1 script</span><span class="sxs-lookup"><span data-stu-id="9a957-193">Run the AzureAutoGrowShrink.ps1 script</span></span>
### <a name="prerequisites"></a><span data-ttu-id="9a957-194">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9a957-194">Prerequisites</span></span>

* <span data-ttu-id="9a957-195">**HPC Pack 2012 R2 Update 1 or later cluster** - The **AzureAutoGrowShrink.ps1** script is installed in the %CCP_HOME%bin folder.</span><span class="sxs-lookup"><span data-stu-id="9a957-195">**HPC Pack 2012 R2 Update 1 or later cluster** - The **AzureAutoGrowShrink.ps1** script is installed in the %CCP_HOME%bin folder.</span></span> <span data-ttu-id="9a957-196">The cluster head node can be deployed either on-premises or in an Azure VM.</span><span class="sxs-lookup"><span data-stu-id="9a957-196">The cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="9a957-197">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) to get started with an on-premises head node and Azure "burst" nodes.</span><span class="sxs-lookup"><span data-stu-id="9a957-197">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) to get started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="9a957-198">See the [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) to quickly deploy an HPC Pack cluster in Azure VMs, or use an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span><span class="sxs-lookup"><span data-stu-id="9a957-198">See the [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) to quickly deploy an HPC Pack cluster in Azure VMs, or use an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span></span>
* <span data-ttu-id="9a957-199">**Azure PowerShell 1.4.0** - The script currently depends on this specific version of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9a957-199">**Azure PowerShell 1.4.0** - The script currently depends on this specific version of Azure PowerShell.</span></span>
* <span data-ttu-id="9a957-200">**For a cluster with Azure burst nodes** - Run the script on a client computer where HPC Pack is installed, or on the head node.</span><span class="sxs-lookup"><span data-stu-id="9a957-200">**For a cluster with Azure burst nodes** - Run the script on a client computer where HPC Pack is installed, or on the head node.</span></span> <span data-ttu-id="9a957-201">If running on a client computer, ensure that you set the variable $env:CCP_SCHEDULER to point to the head node.</span><span class="sxs-lookup"><span data-stu-id="9a957-201">If running on a client computer, ensure that you set the variable $env:CCP_SCHEDULER to point to the head node.</span></span> <span data-ttu-id="9a957-202">The Azure “burst” nodes must be added to the cluster, but they may be in the Not-Deployed state.</span><span class="sxs-lookup"><span data-stu-id="9a957-202">The Azure “burst” nodes must be added to the cluster, but they may be in the Not-Deployed state.</span></span>
* <span data-ttu-id="9a957-203">**For a cluster deployed in Azure VMs (Resource Manager deployment model)** - For a cluster of Azure VMs deployed in the Resource Manager deployment model, the script supports two methods for Azure authentication: sign in to your Azure account to run the script every time (by running `Login-AzureRmAccount`, or configure a service principal to authenticate with a certificate.</span><span class="sxs-lookup"><span data-stu-id="9a957-203">**For a cluster deployed in Azure VMs (Resource Manager deployment model)** - For a cluster of Azure VMs deployed in the Resource Manager deployment model, the script supports two methods for Azure authentication: sign in to your Azure account to run the script every time (by running `Login-AzureRmAccount`, or configure a service principal to authenticate with a certificate.</span></span> <span data-ttu-id="9a957-204">HPC Pack provides the script **ConfigARMAutoGrowShrinkCert.ps** to create a service principal with certificate.</span><span class="sxs-lookup"><span data-stu-id="9a957-204">HPC Pack provides the script **ConfigARMAutoGrowShrinkCert.ps** to create a service principal with certificate.</span></span> <span data-ttu-id="9a957-205">The script creates an Azure Active Directory (Azure AD) application and a service principal, and assigns the Contributor role to the service principal.</span><span class="sxs-lookup"><span data-stu-id="9a957-205">The script creates an Azure Active Directory (Azure AD) application and a service principal, and assigns the Contributor role to the service principal.</span></span> <span data-ttu-id="9a957-206">To run the script, start Azure PowerShell  as administrator and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="9a957-206">To run the script, start Azure PowerShell  as administrator and run the following commands:</span></span>

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    <span data-ttu-id="9a957-207">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span><span class="sxs-lookup"><span data-stu-id="9a957-207">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span></span>

* <span data-ttu-id="9a957-208">**For a cluster deployed in Azure VMs (classic deployment model)** - Run the script on the head node VM, because it depends on the **Start-HpcIaaSNode.ps1** and **Stop-HpcIaaSNode.ps1** scripts that are installed there.</span><span class="sxs-lookup"><span data-stu-id="9a957-208">**For a cluster deployed in Azure VMs (classic deployment model)** - Run the script on the head node VM, because it depends on the **Start-HpcIaaSNode.ps1** and **Stop-HpcIaaSNode.ps1** scripts that are installed there.</span></span> <span data-ttu-id="9a957-209">Those scripts additionally require an Azure management certificate or publish settings file (see [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md)).</span><span class="sxs-lookup"><span data-stu-id="9a957-209">Those scripts additionally require an Azure management certificate or publish settings file (see [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md)).</span></span> <span data-ttu-id="9a957-210">Make sure all the compute node VMs you need are already added to the cluster.</span><span class="sxs-lookup"><span data-stu-id="9a957-210">Make sure all the compute node VMs you need are already added to the cluster.</span></span> <span data-ttu-id="9a957-211">They may be in the Stopped state.</span><span class="sxs-lookup"><span data-stu-id="9a957-211">They may be in the Stopped state.</span></span>



### <a name="syntax"></a><span data-ttu-id="9a957-212">Syntax</span><span class="sxs-lookup"><span data-stu-id="9a957-212">Syntax</span></span>
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="9a957-213">Parameters</span><span class="sxs-lookup"><span data-stu-id="9a957-213">Parameters</span></span>
* <span data-ttu-id="9a957-214">**NodeTemplates** - Names of the node templates to define the scope for the nodes to grow and shrink.</span><span class="sxs-lookup"><span data-stu-id="9a957-214">**NodeTemplates** - Names of the node templates to define the scope for the nodes to grow and shrink.</span></span> <span data-ttu-id="9a957-215">If not specified (the default value is @()), all nodes in the **AzureNodes** node group are in scope when **NodeType** has a value of AzureNodes, and all nodes in the **ComputeNodes** node group are in scope when **NodeType** has a value of ComputeNodes.</span><span class="sxs-lookup"><span data-stu-id="9a957-215">If not specified (the default value is @()), all nodes in the **AzureNodes** node group are in scope when **NodeType** has a value of AzureNodes, and all nodes in the **ComputeNodes** node group are in scope when **NodeType** has a value of ComputeNodes.</span></span>
* <span data-ttu-id="9a957-216">**JobTemplates** - Names of the job templates to define the scope for the nodes to grow.</span><span class="sxs-lookup"><span data-stu-id="9a957-216">**JobTemplates** - Names of the job templates to define the scope for the nodes to grow.</span></span>
* <span data-ttu-id="9a957-217">**NodeType** - The type of node to grow and shrink.</span><span class="sxs-lookup"><span data-stu-id="9a957-217">**NodeType** - The type of node to grow and shrink.</span></span> <span data-ttu-id="9a957-218">Supported values are:</span><span class="sxs-lookup"><span data-stu-id="9a957-218">Supported values are:</span></span>

  * <span data-ttu-id="9a957-219">**AzureNodes** – for Azure PaaS (burst) nodes in an on-premises or Azure IaaS cluster.</span><span class="sxs-lookup"><span data-stu-id="9a957-219">**AzureNodes** – for Azure PaaS (burst) nodes in an on-premises or Azure IaaS cluster.</span></span>
  * <span data-ttu-id="9a957-220">**ComputeNodes** - for compute node VMs only in an Azure IaaS cluster.</span><span class="sxs-lookup"><span data-stu-id="9a957-220">**ComputeNodes** - for compute node VMs only in an Azure IaaS cluster.</span></span>

* <span data-ttu-id="9a957-221">**NumOfQueuedJobsPerNodeToGrow** - Number of queued jobs required to grow one node.</span><span class="sxs-lookup"><span data-stu-id="9a957-221">**NumOfQueuedJobsPerNodeToGrow** - Number of queued jobs required to grow one node.</span></span>
* <span data-ttu-id="9a957-222">**NumOfQueuedJobsToGrowThreshold** - The threshold number of queued jobs to start the grow process.</span><span class="sxs-lookup"><span data-stu-id="9a957-222">**NumOfQueuedJobsToGrowThreshold** - The threshold number of queued jobs to start the grow process.</span></span>
* <span data-ttu-id="9a957-223">**NumOfActiveQueuedTasksPerNodeToGrow** - The number of active queued tasks required to grow one node.</span><span class="sxs-lookup"><span data-stu-id="9a957-223">**NumOfActiveQueuedTasksPerNodeToGrow** - The number of active queued tasks required to grow one node.</span></span> <span data-ttu-id="9a957-224">If **NumOfQueuedJobsPerNodeToGrow** is specified with a value greater than 0, this parameter is ignored.</span><span class="sxs-lookup"><span data-stu-id="9a957-224">If **NumOfQueuedJobsPerNodeToGrow** is specified with a value greater than 0, this parameter is ignored.</span></span>
* <span data-ttu-id="9a957-225">**NumOfActiveQueuedTasksToGrowThreshold** - The threshold number of active queued tasks to start the grow process.</span><span class="sxs-lookup"><span data-stu-id="9a957-225">**NumOfActiveQueuedTasksToGrowThreshold** - The threshold number of active queued tasks to start the grow process.</span></span>
* <span data-ttu-id="9a957-226">**NumOfInitialNodesToGrow** - The initial minimum number of nodes to grow if all the nodes in scope are **Not-Deployed** or **Stopped (Deallocated)**.</span><span class="sxs-lookup"><span data-stu-id="9a957-226">**NumOfInitialNodesToGrow** - The initial minimum number of nodes to grow if all the nodes in scope are **Not-Deployed** or **Stopped (Deallocated)**.</span></span>
* <span data-ttu-id="9a957-227">**GrowCheckIntervalMins** - The interval in minutes between checks to grow.</span><span class="sxs-lookup"><span data-stu-id="9a957-227">**GrowCheckIntervalMins** - The interval in minutes between checks to grow.</span></span>
* <span data-ttu-id="9a957-228">**ShrinkCheckIntervalMins** - The interval in minutes between checks to shrink.</span><span class="sxs-lookup"><span data-stu-id="9a957-228">**ShrinkCheckIntervalMins** - The interval in minutes between checks to shrink.</span></span>
* <span data-ttu-id="9a957-229">**ShrinkCheckIdleTimes** - The number of continuous shrink checks (separated by **ShrinkCheckIntervalMins**) to indicate the nodes are idle.</span><span class="sxs-lookup"><span data-stu-id="9a957-229">**ShrinkCheckIdleTimes** - The number of continuous shrink checks (separated by **ShrinkCheckIntervalMins**) to indicate the nodes are idle.</span></span>
* <span data-ttu-id="9a957-230">**UseLastConfigurations** - The previous configurations saved in the argument file.</span><span class="sxs-lookup"><span data-stu-id="9a957-230">**UseLastConfigurations** - The previous configurations saved in the argument file.</span></span>
* <span data-ttu-id="9a957-231">**ArgFile**- The name of the argument file used to save and update the configurations to run the script.</span><span class="sxs-lookup"><span data-stu-id="9a957-231">**ArgFile**- The name of the argument file used to save and update the configurations to run the script.</span></span>
* <span data-ttu-id="9a957-232">**LogFilePrefix** - The prefix name of the log file.</span><span class="sxs-lookup"><span data-stu-id="9a957-232">**LogFilePrefix** - The prefix name of the log file.</span></span> <span data-ttu-id="9a957-233">You can specify a path.</span><span class="sxs-lookup"><span data-stu-id="9a957-233">You can specify a path.</span></span> <span data-ttu-id="9a957-234">By default the log is written to the current working directory.</span><span class="sxs-lookup"><span data-stu-id="9a957-234">By default the log is written to the current working directory.</span></span>

### <a name="example-1"></a><span data-ttu-id="9a957-235">Example 1</span><span class="sxs-lookup"><span data-stu-id="9a957-235">Example 1</span></span>
<span data-ttu-id="9a957-236">The following example configures the Azure burst nodes deployed with the Default AzureNode Template to grow and shrink automatically.</span><span class="sxs-lookup"><span data-stu-id="9a957-236">The following example configures the Azure burst nodes deployed with the Default AzureNode Template to grow and shrink automatically.</span></span> <span data-ttu-id="9a957-237">If all the nodes are initially in the **Not-Deployed** state, at least 3 nodes are started.</span><span class="sxs-lookup"><span data-stu-id="9a957-237">If all the nodes are initially in the **Not-Deployed** state, at least 3 nodes are started.</span></span> <span data-ttu-id="9a957-238">If the number of queued jobs exceeds 8, the script starts nodes until their number exceeds the ratio of queued jobs to **NumOfQueuedJobsPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="9a957-238">If the number of queued jobs exceeds 8, the script starts nodes until their number exceeds the ratio of queued jobs to **NumOfQueuedJobsPerNodeToGrow**.</span></span> <span data-ttu-id="9a957-239">If a node is found to be idle in 3 consecutive idle times, it is stopped.</span><span class="sxs-lookup"><span data-stu-id="9a957-239">If a node is found to be idle in 3 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a><span data-ttu-id="9a957-240">Example 2</span><span class="sxs-lookup"><span data-stu-id="9a957-240">Example 2</span></span>
<span data-ttu-id="9a957-241">The following example configures the Azure compute node VMs deployed with the Default ComputeNode Template to grow and shrink automatically.</span><span class="sxs-lookup"><span data-stu-id="9a957-241">The following example configures the Azure compute node VMs deployed with the Default ComputeNode Template to grow and shrink automatically.</span></span>
<span data-ttu-id="9a957-242">The jobs configured by the Default job template define the scope of the workload on the cluster.</span><span class="sxs-lookup"><span data-stu-id="9a957-242">The jobs configured by the Default job template define the scope of the workload on the cluster.</span></span> <span data-ttu-id="9a957-243">If all the nodes are initially stopped, at least 5 nodes are started.</span><span class="sxs-lookup"><span data-stu-id="9a957-243">If all the nodes are initially stopped, at least 5 nodes are started.</span></span> <span data-ttu-id="9a957-244">If the number of active queued tasks exceeds 15, the script starts nodes until their number exceeds the ratio of active queued tasks to **NumOfActiveQueuedTasksPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="9a957-244">If the number of active queued tasks exceeds 15, the script starts nodes until their number exceeds the ratio of active queued tasks to **NumOfActiveQueuedTasksPerNodeToGrow**.</span></span> <span data-ttu-id="9a957-245">If a node is found to be idle in 10 consecutive idle times, it is stopped.</span><span class="sxs-lookup"><span data-stu-id="9a957-245">If a node is found to be idle in 10 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
