---
title: Manage HPC Pack cluster compute nodes | Microsoft Docs
description: Learn about PowerShell script tools to add, remove, start, and stop HPC Pack 2012 R2 cluster compute nodes in Azure
services: virtual-machines-windows
documentationcenter: ''
author: dlepow
manager: jeconnoc
editor: ''
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 453f53be15b24b96f183b4935cc45fc97ad058bd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44814423"
---
# <a name="manage-the-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="dd556-103">Manage the number and availability of compute nodes in an HPC Pack cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="dd556-103">Manage the number and availability of compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="dd556-104">If you created an HPC Pack 2012 R2 cluster in Azure VMs, you might want ways to easily add, remove, start (provision), or stop (deprovision) some compute node VMs in the cluster.</span><span class="sxs-lookup"><span data-stu-id="dd556-104">If you created an HPC Pack 2012 R2 cluster in Azure VMs, you might want ways to easily add, remove, start (provision), or stop (deprovision) some compute node VMs in the cluster.</span></span> <span data-ttu-id="dd556-105">To do these tasks, run Azure PowerShell scripts that are installed on the head node VM.</span><span class="sxs-lookup"><span data-stu-id="dd556-105">To do these tasks, run Azure PowerShell scripts that are installed on the head node VM.</span></span> <span data-ttu-id="dd556-106">These scripts help you control the number and availability of your HPC Pack cluster resources so you can control costs.</span><span class="sxs-lookup"><span data-stu-id="dd556-106">These scripts help you control the number and availability of your HPC Pack cluster resources so you can control costs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="dd556-107">This article applies only to HPC Pack 2012 R2 clusters in Azure created using the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="dd556-107">This article applies only to HPC Pack 2012 R2 clusters in Azure created using the classic deployment model.</span></span> <span data-ttu-id="dd556-108">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="dd556-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> <span data-ttu-id="dd556-109">In addition, the PowerShell scripts described in this article are not available in HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="dd556-109">In addition, the PowerShell scripts described in this article are not available in HPC Pack 2016.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd556-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dd556-110">Prerequisites</span></span>
* <span data-ttu-id="dd556-111">**HPC Pack 2012 R2 cluster in Azure VMs**: Create an HPC Pack 2012 R2 cluster in the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="dd556-111">**HPC Pack 2012 R2 cluster in Azure VMs**: Create an HPC Pack 2012 R2 cluster in the classic deployment model.</span></span> <span data-ttu-id="dd556-112">For example, you can automate the deployment by using the HPC Pack 2012 R2 VM image in the Azure Marketplace and an Azure PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="dd556-112">For example, you can automate the deployment by using the HPC Pack 2012 R2 VM image in the Azure Marketplace and an Azure PowerShell script.</span></span> <span data-ttu-id="dd556-113">For information and prerequisites, see [Create an HPC Cluster with the HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="dd556-113">For information and prerequisites, see [Create an HPC Cluster with the HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md).</span></span>
  
    <span data-ttu-id="dd556-114">After deployment, find the node management scripts in the %CCP\_HOME%bin folder on the head node.</span><span class="sxs-lookup"><span data-stu-id="dd556-114">After deployment, find the node management scripts in the %CCP\_HOME%bin folder on the head node.</span></span> <span data-ttu-id="dd556-115">Run each of the scripts as an administrator.</span><span class="sxs-lookup"><span data-stu-id="dd556-115">Run each of the scripts as an administrator.</span></span>
* <span data-ttu-id="dd556-116">**Azure publish settings file or management certificate**: You need to do one of the following on the head node:</span><span class="sxs-lookup"><span data-stu-id="dd556-116">**Azure publish settings file or management certificate**: You need to do one of the following on the head node:</span></span>
  
  * <span data-ttu-id="dd556-117">**Import the Azure publish settings file**.</span><span class="sxs-lookup"><span data-stu-id="dd556-117">**Import the Azure publish settings file**.</span></span> <span data-ttu-id="dd556-118">To do this, run the following Azure PowerShell cmdlets on the head node:</span><span class="sxs-lookup"><span data-stu-id="dd556-118">To do this, run the following Azure PowerShell cmdlets on the head node:</span></span>
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * <span data-ttu-id="dd556-119">**Configure the Azure management certificate on the head node**.</span><span class="sxs-lookup"><span data-stu-id="dd556-119">**Configure the Azure management certificate on the head node**.</span></span> <span data-ttu-id="dd556-120">If you have the .cer file, import it in the CurrentUser\My certificate store and then run the following Azure PowerShell cmdlet for your Azure environment (either AzureCloud or AzureChinaCloud):</span><span class="sxs-lookup"><span data-stu-id="dd556-120">If you have the .cer file, import it in the CurrentUser\My certificate store and then run the following Azure PowerShell cmdlet for your Azure environment (either AzureCloud or AzureChinaCloud):</span></span>
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a><span data-ttu-id="dd556-121">Add compute node VMs</span><span class="sxs-lookup"><span data-stu-id="dd556-121">Add compute node VMs</span></span>
<span data-ttu-id="dd556-122">Add compute nodes with the **Add-HpcIaaSNode.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="dd556-122">Add compute nodes with the **Add-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="dd556-123">Syntax</span><span class="sxs-lookup"><span data-stu-id="dd556-123">Syntax</span></span>
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a><span data-ttu-id="dd556-124">Parameters</span><span class="sxs-lookup"><span data-stu-id="dd556-124">Parameters</span></span>
* <span data-ttu-id="dd556-125">**ServiceName**: Name of the cloud service that new compute node VMs are added to.</span><span class="sxs-lookup"><span data-stu-id="dd556-125">**ServiceName**: Name of the cloud service that new compute node VMs are added to.</span></span>
* <span data-ttu-id="dd556-126">**ImageName**: Azure VM image name, which can be obtained through the Azure portal or Azure PowerShell cmdlet **Get-AzureVMImage**.</span><span class="sxs-lookup"><span data-stu-id="dd556-126">**ImageName**: Azure VM image name, which can be obtained through the Azure portal or Azure PowerShell cmdlet **Get-AzureVMImage**.</span></span> <span data-ttu-id="dd556-127">The image must meet the following requirements:</span><span class="sxs-lookup"><span data-stu-id="dd556-127">The image must meet the following requirements:</span></span>
  
  1. <span data-ttu-id="dd556-128">A Windows operating system must be installed.</span><span class="sxs-lookup"><span data-stu-id="dd556-128">A Windows operating system must be installed.</span></span>
  2. <span data-ttu-id="dd556-129">HPC Pack must be installed in the compute node role.</span><span class="sxs-lookup"><span data-stu-id="dd556-129">HPC Pack must be installed in the compute node role.</span></span>
  3. <span data-ttu-id="dd556-130">The image must be a private image in the User category, not a public Azure VM image.</span><span class="sxs-lookup"><span data-stu-id="dd556-130">The image must be a private image in the User category, not a public Azure VM image.</span></span>
* <span data-ttu-id="dd556-131">**Quantity**: Number of compute node VMs to be added.</span><span class="sxs-lookup"><span data-stu-id="dd556-131">**Quantity**: Number of compute node VMs to be added.</span></span>
* <span data-ttu-id="dd556-132">**InstanceSize**: Size of the compute node VMs.</span><span class="sxs-lookup"><span data-stu-id="dd556-132">**InstanceSize**: Size of the compute node VMs.</span></span>
* <span data-ttu-id="dd556-133">**DomainUserName**: Domain user name, which is used to join the new VMs to the domain.</span><span class="sxs-lookup"><span data-stu-id="dd556-133">**DomainUserName**: Domain user name, which is used to join the new VMs to the domain.</span></span>
* <span data-ttu-id="dd556-134">**DomainUserPassword**: Password of the domain user.</span><span class="sxs-lookup"><span data-stu-id="dd556-134">**DomainUserPassword**: Password of the domain user.</span></span>
* <span data-ttu-id="dd556-135">**NodeNameSeries** (optional): Naming pattern for the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="dd556-135">**NodeNameSeries** (optional): Naming pattern for the compute nodes.</span></span> <span data-ttu-id="dd556-136">The format must be &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span><span class="sxs-lookup"><span data-stu-id="dd556-136">The format must be &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span></span> <span data-ttu-id="dd556-137">For example, MyCN%10% means a series of the compute node names starting from MyCN11.</span><span class="sxs-lookup"><span data-stu-id="dd556-137">For example, MyCN%10% means a series of the compute node names starting from MyCN11.</span></span> <span data-ttu-id="dd556-138">If not specified, the script uses the configured node naming series in the HPC cluster.</span><span class="sxs-lookup"><span data-stu-id="dd556-138">If not specified, the script uses the configured node naming series in the HPC cluster.</span></span>

### <a name="example"></a><span data-ttu-id="dd556-139">Example</span><span class="sxs-lookup"><span data-stu-id="dd556-139">Example</span></span>
<span data-ttu-id="dd556-140">The following example adds 20 size Large compute node VMs in the cloud service *hpcservice1*, based on the VM image *hpccnimage1*.</span><span class="sxs-lookup"><span data-stu-id="dd556-140">The following example adds 20 size Large compute node VMs in the cloud service *hpcservice1*, based on the VM image *hpccnimage1*.</span></span>

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a><span data-ttu-id="dd556-141">Remove compute node VMs</span><span class="sxs-lookup"><span data-stu-id="dd556-141">Remove compute node VMs</span></span>
<span data-ttu-id="dd556-142">Remove compute nodes with the **Remove-HpcIaaSNode.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="dd556-142">Remove compute nodes with the **Remove-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="dd556-143">Syntax</span><span class="sxs-lookup"><span data-stu-id="dd556-143">Syntax</span></span>
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="dd556-144">Parameters</span><span class="sxs-lookup"><span data-stu-id="dd556-144">Parameters</span></span>
* <span data-ttu-id="dd556-145">**Name**: Names of cluster nodes to be removed.</span><span class="sxs-lookup"><span data-stu-id="dd556-145">**Name**: Names of cluster nodes to be removed.</span></span> <span data-ttu-id="dd556-146">Wildcards are supported.</span><span class="sxs-lookup"><span data-stu-id="dd556-146">Wildcards are supported.</span></span> <span data-ttu-id="dd556-147">The parameter set name is Name.</span><span class="sxs-lookup"><span data-stu-id="dd556-147">The parameter set name is Name.</span></span> <span data-ttu-id="dd556-148">You can't specify both the **Name** and **Node** parameters.</span><span class="sxs-lookup"><span data-stu-id="dd556-148">You can't specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="dd556-149">**Node**: The HpcNode object for the nodes to be removed, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="dd556-149">**Node**: The HpcNode object for the nodes to be removed, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="dd556-150">The parameter set name is Node.</span><span class="sxs-lookup"><span data-stu-id="dd556-150">The parameter set name is Node.</span></span> <span data-ttu-id="dd556-151">You can't specify both the **Name** and **Node** parameters.</span><span class="sxs-lookup"><span data-stu-id="dd556-151">You can't specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="dd556-152">**DeleteVHD** (optional): Setting to delete the associated disks for the VMs that are removed.</span><span class="sxs-lookup"><span data-stu-id="dd556-152">**DeleteVHD** (optional): Setting to delete the associated disks for the VMs that are removed.</span></span>
* <span data-ttu-id="dd556-153">**Force** (optional): Setting to force HPC nodes offline before removing them.</span><span class="sxs-lookup"><span data-stu-id="dd556-153">**Force** (optional): Setting to force HPC nodes offline before removing them.</span></span>
* <span data-ttu-id="dd556-154">**Confirm** (optional): Prompt for confirmation before executing the command.</span><span class="sxs-lookup"><span data-stu-id="dd556-154">**Confirm** (optional): Prompt for confirmation before executing the command.</span></span>
* <span data-ttu-id="dd556-155">**WhatIf**: Setting to describe what would happen if you executed the command without actually executing the command.</span><span class="sxs-lookup"><span data-stu-id="dd556-155">**WhatIf**: Setting to describe what would happen if you executed the command without actually executing the command.</span></span>

### <a name="example"></a><span data-ttu-id="dd556-156">Example</span><span class="sxs-lookup"><span data-stu-id="dd556-156">Example</span></span>
<span data-ttu-id="dd556-157">The following example forces offline the nodes with names beginning *HPCNode-CN-* and them removes the nodes and their associated disks.</span><span class="sxs-lookup"><span data-stu-id="dd556-157">The following example forces offline the nodes with names beginning *HPCNode-CN-* and them removes the nodes and their associated disks.</span></span>

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a><span data-ttu-id="dd556-158">Start compute node VMs</span><span class="sxs-lookup"><span data-stu-id="dd556-158">Start compute node VMs</span></span>
<span data-ttu-id="dd556-159">Start compute nodes with the **Start-HpcIaaSNode.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="dd556-159">Start compute nodes with the **Start-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="dd556-160">Syntax</span><span class="sxs-lookup"><span data-stu-id="dd556-160">Syntax</span></span>
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="dd556-161">Parameters</span><span class="sxs-lookup"><span data-stu-id="dd556-161">Parameters</span></span>
* <span data-ttu-id="dd556-162">**Name**: Names of the cluster nodes to be started.</span><span class="sxs-lookup"><span data-stu-id="dd556-162">**Name**: Names of the cluster nodes to be started.</span></span> <span data-ttu-id="dd556-163">Wildcards are supported.</span><span class="sxs-lookup"><span data-stu-id="dd556-163">Wildcards are supported.</span></span> <span data-ttu-id="dd556-164">The parameter set name is Name.</span><span class="sxs-lookup"><span data-stu-id="dd556-164">The parameter set name is Name.</span></span> <span data-ttu-id="dd556-165">You cannot specify both the **Name** and **Node** parameters.</span><span class="sxs-lookup"><span data-stu-id="dd556-165">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="dd556-166">**Node**- The HpcNode object for the nodes to be started, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="dd556-166">**Node**- The HpcNode object for the nodes to be started, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="dd556-167">The parameter set name is Node.</span><span class="sxs-lookup"><span data-stu-id="dd556-167">The parameter set name is Node.</span></span> <span data-ttu-id="dd556-168">You cannot specify both the **Name** and **Node** parameters.</span><span class="sxs-lookup"><span data-stu-id="dd556-168">You cannot specify both the **Name** and **Node** parameters.</span></span>

### <a name="example"></a><span data-ttu-id="dd556-169">Example</span><span class="sxs-lookup"><span data-stu-id="dd556-169">Example</span></span>
<span data-ttu-id="dd556-170">The following example starts nodes with names beginning *HPCNode-CN-*.</span><span class="sxs-lookup"><span data-stu-id="dd556-170">The following example starts nodes with names beginning *HPCNode-CN-*.</span></span>

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a><span data-ttu-id="dd556-171">Stop compute node VMs</span><span class="sxs-lookup"><span data-stu-id="dd556-171">Stop compute node VMs</span></span>
<span data-ttu-id="dd556-172">Stop compute nodes with the **Stop-HpcIaaSNode.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="dd556-172">Stop compute nodes with the **Stop-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="dd556-173">Syntax</span><span class="sxs-lookup"><span data-stu-id="dd556-173">Syntax</span></span>
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="dd556-174">Parameters</span><span class="sxs-lookup"><span data-stu-id="dd556-174">Parameters</span></span>
* <span data-ttu-id="dd556-175">**Name**- Names of the cluster nodes to be stopped.</span><span class="sxs-lookup"><span data-stu-id="dd556-175">**Name**- Names of the cluster nodes to be stopped.</span></span> <span data-ttu-id="dd556-176">Wildcards are supported.</span><span class="sxs-lookup"><span data-stu-id="dd556-176">Wildcards are supported.</span></span> <span data-ttu-id="dd556-177">The parameter set name is Name.</span><span class="sxs-lookup"><span data-stu-id="dd556-177">The parameter set name is Name.</span></span> <span data-ttu-id="dd556-178">You cannot specify both the **Name** and **Node** parameters.</span><span class="sxs-lookup"><span data-stu-id="dd556-178">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="dd556-179">**Node**: The HpcNode object for the nodes to be stopped, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="dd556-179">**Node**: The HpcNode object for the nodes to be stopped, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="dd556-180">The parameter set name is Node.</span><span class="sxs-lookup"><span data-stu-id="dd556-180">The parameter set name is Node.</span></span> <span data-ttu-id="dd556-181">You cannot specify both the **Name** and **Node** parameters.</span><span class="sxs-lookup"><span data-stu-id="dd556-181">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="dd556-182">**Force** (optional): Setting to force HPC nodes offline before stopping them.</span><span class="sxs-lookup"><span data-stu-id="dd556-182">**Force** (optional): Setting to force HPC nodes offline before stopping them.</span></span>

### <a name="example"></a><span data-ttu-id="dd556-183">Example</span><span class="sxs-lookup"><span data-stu-id="dd556-183">Example</span></span>
<span data-ttu-id="dd556-184">The following example forces offline nodes with names beginning *HPCNode-CN-* and then stops the nodes.</span><span class="sxs-lookup"><span data-stu-id="dd556-184">The following example forces offline nodes with names beginning *HPCNode-CN-* and then stops the nodes.</span></span>

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a><span data-ttu-id="dd556-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="dd556-185">Next steps</span></span>
* <span data-ttu-id="dd556-186">To automatically grow or shrink the cluster nodes according to the current workload of jobs and tasks on the cluster, see [Automatically grow and shrink the HPC Pack cluster resources in Azure according to the cluster workload](hpcpack-cluster-node-autogrowshrink.md).</span><span class="sxs-lookup"><span data-stu-id="dd556-186">To automatically grow or shrink the cluster nodes according to the current workload of jobs and tasks on the cluster, see [Automatically grow and shrink the HPC Pack cluster resources in Azure according to the cluster workload](hpcpack-cluster-node-autogrowshrink.md).</span></span>

