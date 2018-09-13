---
title: Replicate Hyper-V virtual machines in VMM clouds using Azure Site Recovery and PowerShell (Resource Manager) | Microsoft Docs
description: Replicate Hyper-V virtual machines in VMM clouds using Azure Site Recovery and PowerShell
services: site-recovery
documentationcenter: ''
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: rajanaki
ms.openlocfilehash: 0a900d4ddf6a751a4bf54720d3b62cf9e59e0a71
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562676"
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-azure-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="1d809-103">Replicate Hyper-V virtual machines in VMM clouds to Azure using PowerShell and Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1d809-103">Replicate Hyper-V virtual machines in VMM clouds to Azure using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmm-to-azure.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [Classic Portal](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell - Classic](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="1d809-108">Overview</span><span class="sxs-lookup"><span data-stu-id="1d809-108">Overview</span></span>
<span data-ttu-id="1d809-109">Azure Site Recovery contributes to your business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span><span class="sxs-lookup"><span data-stu-id="1d809-109">Azure Site Recovery contributes to your business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="1d809-110">For a full list of deployment scenarios see the [Azure Site Recovery overview](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1d809-110">For a full list of deployment scenarios see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="1d809-111">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to Azure storage.</span><span class="sxs-lookup"><span data-stu-id="1d809-111">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to Azure storage.</span></span>

<span data-ttu-id="1d809-112">The article includes prerequisites for the scenario, and shows you</span><span class="sxs-lookup"><span data-stu-id="1d809-112">The article includes prerequisites for the scenario, and shows you</span></span>

* <span data-ttu-id="1d809-113">How to set up a Recovery Services Vault</span><span class="sxs-lookup"><span data-stu-id="1d809-113">How to set up a Recovery Services Vault</span></span>
* <span data-ttu-id="1d809-114">Install the Azure Site Recovery Provider on the source VMM server</span><span class="sxs-lookup"><span data-stu-id="1d809-114">Install the Azure Site Recovery Provider on the source VMM server</span></span>
* <span data-ttu-id="1d809-115">Register the server in the vault, add an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="1d809-115">Register the server in the vault, add an Azure storage account</span></span>
* <span data-ttu-id="1d809-116">Install the Azure Recovery Services agent on Hyper-V host servers</span><span class="sxs-lookup"><span data-stu-id="1d809-116">Install the Azure Recovery Services agent on Hyper-V host servers</span></span>
* <span data-ttu-id="1d809-117">Configure protection settings for VMM clouds, that will be applied to all protected virtual machines</span><span class="sxs-lookup"><span data-stu-id="1d809-117">Configure protection settings for VMM clouds, that will be applied to all protected virtual machines</span></span>
* <span data-ttu-id="1d809-118">Enable protection for those virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1d809-118">Enable protection for those virtual machines.</span></span>
* <span data-ttu-id="1d809-119">Test the fail-over to make sure everything's working as expected.</span><span class="sxs-lookup"><span data-stu-id="1d809-119">Test the fail-over to make sure everything's working as expected.</span></span>

<span data-ttu-id="1d809-120">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="1d809-120">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md). This article covers using the Resource Manager deployment model.
>
>

## <a name="before-you-start"></a><span data-ttu-id="1d809-123">Before you start</span><span class="sxs-lookup"><span data-stu-id="1d809-123">Before you start</span></span>
<span data-ttu-id="1d809-124">Make sure you have these prerequisites in place:</span><span class="sxs-lookup"><span data-stu-id="1d809-124">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="1d809-125">Azure prerequisites</span><span class="sxs-lookup"><span data-stu-id="1d809-125">Azure prerequisites</span></span>
* <span data-ttu-id="1d809-126">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span><span class="sxs-lookup"><span data-stu-id="1d809-126">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="1d809-127">If you don't have one, start with a [free account](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="1d809-127">If you don't have one, start with a [free account](https://azure.microsoft.com/free).</span></span> <span data-ttu-id="1d809-128">In addition, you can read about the [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="1d809-128">In addition, you can read about the [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="1d809-129">You'll need a CSP subscription if you are trying out the replication to a CSP subscription scenario.</span><span class="sxs-lookup"><span data-stu-id="1d809-129">You'll need a CSP subscription if you are trying out the replication to a CSP subscription scenario.</span></span> <span data-ttu-id="1d809-130">Learn more about the CSP program in [how to enroll in the CSP program](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d809-130">Learn more about the CSP program in [how to enroll in the CSP program](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span></span>
* <span data-ttu-id="1d809-131">You'll need an Azure v2 storage (Resource Manager) account to store data replicated to Azure.</span><span class="sxs-lookup"><span data-stu-id="1d809-131">You'll need an Azure v2 storage (Resource Manager) account to store data replicated to Azure.</span></span> <span data-ttu-id="1d809-132">The account needs geo-replication enabled.</span><span class="sxs-lookup"><span data-stu-id="1d809-132">The account needs geo-replication enabled.</span></span> <span data-ttu-id="1d809-133">It should be in the same region as the Azure Site Recovery service, and be associated with the same subscription or the CSP subscription.</span><span class="sxs-lookup"><span data-stu-id="1d809-133">It should be in the same region as the Azure Site Recovery service, and be associated with the same subscription or the CSP subscription.</span></span> <span data-ttu-id="1d809-134">To learn more about setting up Azure storage, see the [Introduction to Microsoft Azure Storage](../storage/storage-introduction.md) for reference.</span><span class="sxs-lookup"><span data-stu-id="1d809-134">To learn more about setting up Azure storage, see the [Introduction to Microsoft Azure Storage](../storage/storage-introduction.md) for reference.</span></span>
* <span data-ttu-id="1d809-135">You'll need to make sure that virtual machines you want to protect comply with the [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="1d809-135">You'll need to make sure that virtual machines you want to protect comply with the [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

> [!NOTE]
> Currently, only VM level operations are possible through Powershell. Support for recovery plan level operations will be made soon.  For now, you are limited to performing fail-overs only at a ‘protected VM’ granularity and not at a Recovery Plan level.
>
>

### <a name="vmm-prerequisites"></a><span data-ttu-id="1d809-139">VMM prerequisites</span><span class="sxs-lookup"><span data-stu-id="1d809-139">VMM prerequisites</span></span>
* <span data-ttu-id="1d809-140">You'll need VMM server running on System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="1d809-140">You'll need VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="1d809-141">Any VMM server containing virtual machines you want to protect must be running the Azure Site Recovery Provider.</span><span class="sxs-lookup"><span data-stu-id="1d809-141">Any VMM server containing virtual machines you want to protect must be running the Azure Site Recovery Provider.</span></span> <span data-ttu-id="1d809-142">This is installed during the Azure Site Recovery deployment.</span><span class="sxs-lookup"><span data-stu-id="1d809-142">This is installed during the Azure Site Recovery deployment.</span></span>
* <span data-ttu-id="1d809-143">You'll need at least one cloud on the VMM server you want to protect.</span><span class="sxs-lookup"><span data-stu-id="1d809-143">You'll need at least one cloud on the VMM server you want to protect.</span></span> <span data-ttu-id="1d809-144">The cloud should contain:</span><span class="sxs-lookup"><span data-stu-id="1d809-144">The cloud should contain:</span></span>
  * <span data-ttu-id="1d809-145">One or more VMM host groups.</span><span class="sxs-lookup"><span data-stu-id="1d809-145">One or more VMM host groups.</span></span>
  * <span data-ttu-id="1d809-146">One or more Hyper-V host servers or clusters in each host group.</span><span class="sxs-lookup"><span data-stu-id="1d809-146">One or more Hyper-V host servers or clusters in each host group.</span></span>
  * <span data-ttu-id="1d809-147">One or more virtual machines on the source Hyper-V server.</span><span class="sxs-lookup"><span data-stu-id="1d809-147">One or more virtual machines on the source Hyper-V server.</span></span>
* <span data-ttu-id="1d809-148">Learn more about setting up VMM clouds:</span><span class="sxs-lookup"><span data-stu-id="1d809-148">Learn more about setting up VMM clouds:</span></span>
  * <span data-ttu-id="1d809-149">Read more about private VMM clouds in [What’s New in Private Cloud with System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) and in [VMM 2012 and the clouds](http://go.microsoft.com/fwlink/?LinkId=324956).</span><span class="sxs-lookup"><span data-stu-id="1d809-149">Read more about private VMM clouds in [What’s New in Private Cloud with System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) and in [VMM 2012 and the clouds](http://go.microsoft.com/fwlink/?LinkId=324956).</span></span>
  * <span data-ttu-id="1d809-150">Learn about [Configuring the VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span><span class="sxs-lookup"><span data-stu-id="1d809-150">Learn about [Configuring the VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span></span>
  * <span data-ttu-id="1d809-151">After your cloud fabric elements are in place learn about creating private clouds in [Creating a private cloud in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) and in [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span><span class="sxs-lookup"><span data-stu-id="1d809-151">After your cloud fabric elements are in place learn about creating private clouds in [Creating a private cloud in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) and in [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="1d809-152">Hyper-V prerequisites</span><span class="sxs-lookup"><span data-stu-id="1d809-152">Hyper-V prerequisites</span></span>
* <span data-ttu-id="1d809-153">The host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have the latest updates installed.</span><span class="sxs-lookup"><span data-stu-id="1d809-153">The host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have the latest updates installed.</span></span>
* <span data-ttu-id="1d809-154">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span><span class="sxs-lookup"><span data-stu-id="1d809-154">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="1d809-155">You'll need to configure the cluster broker manually.</span><span class="sxs-lookup"><span data-stu-id="1d809-155">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="1d809-156">For</span><span class="sxs-lookup"><span data-stu-id="1d809-156">For</span></span>
* <span data-ttu-id="1d809-157">For instructions see [How to Configure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d809-157">For instructions see [How to Configure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span></span>
* <span data-ttu-id="1d809-158">Any Hyper-V host server or cluster for which you want to manage protection must be included in a VMM cloud.</span><span class="sxs-lookup"><span data-stu-id="1d809-158">Any Hyper-V host server or cluster for which you want to manage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="1d809-159">Network mapping prerequisites</span><span class="sxs-lookup"><span data-stu-id="1d809-159">Network mapping prerequisites</span></span>
<span data-ttu-id="1d809-160">When you protect virtual machines in Azure, the network mapping  maps the virtual machine networks on the source VMM server and target Azure networks to enable the following:</span><span class="sxs-lookup"><span data-stu-id="1d809-160">When you protect virtual machines in Azure, the network mapping  maps the virtual machine networks on the source VMM server and target Azure networks to enable the following:</span></span>

* <span data-ttu-id="1d809-161">All machines which fail over on the same network can connect to each other, irrespective of which recovery plan they are in.</span><span class="sxs-lookup"><span data-stu-id="1d809-161">All machines which fail over on the same network can connect to each other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="1d809-162">If a network gateway is setup on the target Azure network, virtual machines can connect to other on-premises virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1d809-162">If a network gateway is setup on the target Azure network, virtual machines can connect to other on-premises virtual machines.</span></span>
* <span data-ttu-id="1d809-163">If you don’t configure network mapping, only the virtual machines that fail over in the same recovery plan will be able to connect to each other after fail-over to Azure.</span><span class="sxs-lookup"><span data-stu-id="1d809-163">If you don’t configure network mapping, only the virtual machines that fail over in the same recovery plan will be able to connect to each other after fail-over to Azure.</span></span>

<span data-ttu-id="1d809-164">If you want to deploy network mapping you'll need the following:</span><span class="sxs-lookup"><span data-stu-id="1d809-164">If you want to deploy network mapping you'll need the following:</span></span>

* <span data-ttu-id="1d809-165">The virtual machines you want to protect on the source VMM server should be connected to a VM network.</span><span class="sxs-lookup"><span data-stu-id="1d809-165">The virtual machines you want to protect on the source VMM server should be connected to a VM network.</span></span> <span data-ttu-id="1d809-166">That network should be linked to a logical network that is associated with the cloud.</span><span class="sxs-lookup"><span data-stu-id="1d809-166">That network should be linked to a logical network that is associated with the cloud.</span></span>
* <span data-ttu-id="1d809-167">An Azure network to which replicated virtual machines can connect after fail-over.</span><span class="sxs-lookup"><span data-stu-id="1d809-167">An Azure network to which replicated virtual machines can connect after fail-over.</span></span> <span data-ttu-id="1d809-168">You'll select this network at the time of fail-over.</span><span class="sxs-lookup"><span data-stu-id="1d809-168">You'll select this network at the time of fail-over.</span></span> <span data-ttu-id="1d809-169">The network should be in the same region as your Azure Site Recovery subscription.</span><span class="sxs-lookup"><span data-stu-id="1d809-169">The network should be in the same region as your Azure Site Recovery subscription.</span></span>

<span data-ttu-id="1d809-170">Learn more about network mapping in</span><span class="sxs-lookup"><span data-stu-id="1d809-170">Learn more about network mapping in</span></span>

* [<span data-ttu-id="1d809-171">How to configure logical networks in VMM</span><span class="sxs-lookup"><span data-stu-id="1d809-171">How to configure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="1d809-172">How to configure VM networks and gateways in VMM</span><span class="sxs-lookup"><span data-stu-id="1d809-172">How to configure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [<span data-ttu-id="1d809-173">How to configure and monitor virtual networks in Azure</span><span class="sxs-lookup"><span data-stu-id="1d809-173">How to configure and monitor virtual networks in Azure</span></span>](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a><span data-ttu-id="1d809-174">PowerShell prerequisites</span><span class="sxs-lookup"><span data-stu-id="1d809-174">PowerShell prerequisites</span></span>
<span data-ttu-id="1d809-175">Make sure you have Azure PowerShell ready to go.</span><span class="sxs-lookup"><span data-stu-id="1d809-175">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="1d809-176">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span><span class="sxs-lookup"><span data-stu-id="1d809-176">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="1d809-177">For information about setting up PowerShell, see the [Guide to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="1d809-177">For information about setting up PowerShell, see the [Guide to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="1d809-178">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](https://msdn.microsoft.com/library/dn850420.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d809-178">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](https://msdn.microsoft.com/library/dn850420.aspx).</span></span>

<span data-ttu-id="1d809-179">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see the [Guide to get Started with Azure Cmdlets](https://msdn.microsoft.com/library/azure/jj554332.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d809-179">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see the [Guide to get Started with Azure Cmdlets](https://msdn.microsoft.com/library/azure/jj554332.aspx).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="1d809-180">Step 1: Set the subscription</span><span class="sxs-lookup"><span data-stu-id="1d809-180">Step 1: Set the subscription</span></span>
1. <span data-ttu-id="1d809-181">From Azure powershell, login to your Azure account: using the following cmdlets</span><span class="sxs-lookup"><span data-stu-id="1d809-181">From Azure powershell, login to your Azure account: using the following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="1d809-182">Get a list of your subscriptions.</span><span class="sxs-lookup"><span data-stu-id="1d809-182">Get a list of your subscriptions.</span></span> <span data-ttu-id="1d809-183">This will also list the subscriptionIDs for each of the subscriptions.</span><span class="sxs-lookup"><span data-stu-id="1d809-183">This will also list the subscriptionIDs for each of the subscriptions.</span></span> <span data-ttu-id="1d809-184">Note down the subscriptionID of the subscription in which you wish to create the recovery services vault</span><span class="sxs-lookup"><span data-stu-id="1d809-184">Note down the subscriptionID of the subscription in which you wish to create the recovery services vault</span></span>

        Get-AzureRmSubscription
3. <span data-ttu-id="1d809-185">Set the subscription in which the recovery services vault is to be created by mentioning the subscription ID</span><span class="sxs-lookup"><span data-stu-id="1d809-185">Set the subscription in which the recovery services vault is to be created by mentioning the subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="1d809-186">Step 2: Create a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="1d809-186">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="1d809-187">Create a resource group  in Azure Resource Manager if you don't have one already</span><span class="sxs-lookup"><span data-stu-id="1d809-187">Create a resource group  in Azure Resource Manager if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="1d809-188">Create a new Recovery Services vault and save the created ASR vault object in a variable (will be used later).</span><span class="sxs-lookup"><span data-stu-id="1d809-188">Create a new Recovery Services vault and save the created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="1d809-189">You can also retrieve the ASR vault object post creation using the Get-AzureRMRecoveryServicesVault cmdlet:-</span><span class="sxs-lookup"><span data-stu-id="1d809-189">You can also retrieve the ASR vault object post creation using the Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="1d809-190">Step 3: Set the Recovery Services Vault context</span><span class="sxs-lookup"><span data-stu-id="1d809-190">Step 3: Set the Recovery Services Vault context</span></span>

<span data-ttu-id="1d809-191">Set the vault context by running the below command.</span><span class="sxs-lookup"><span data-stu-id="1d809-191">Set the vault context by running the below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="1d809-192">Step 4: Install the Azure Site Recovery Provider</span><span class="sxs-lookup"><span data-stu-id="1d809-192">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="1d809-193">On the VMM machine, create a directory by running the following command:</span><span class="sxs-lookup"><span data-stu-id="1d809-193">On the VMM machine, create a directory by running the following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="1d809-194">Extract the files using the downloaded provider by running the following command</span><span class="sxs-lookup"><span data-stu-id="1d809-194">Extract the files using the downloaded provider by running the following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="1d809-195">Install the provider using the following commands:</span><span class="sxs-lookup"><span data-stu-id="1d809-195">Install the provider using the following commands:</span></span>

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   <span data-ttu-id="1d809-196">Wait for the installation to finish.</span><span class="sxs-lookup"><span data-stu-id="1d809-196">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="1d809-197">Register the server in the vault using the following command:</span><span class="sxs-lookup"><span data-stu-id="1d809-197">Register the server in the vault using the following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="1d809-198">Step 5: Create an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="1d809-198">Step 5: Create an Azure storage account</span></span>

<span data-ttu-id="1d809-199">If you don't have an Azure storage account, create a geo-replication enabled account in the same geo as the vault by running the following command:</span><span class="sxs-lookup"><span data-stu-id="1d809-199">If you don't have an Azure storage account, create a geo-replication enabled account in the same geo as the vault by running the following command:</span></span>

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

<span data-ttu-id="1d809-200">Note that the storage account must be in the same region as the Azure Site Recovery service, and be associated with the same subscription.</span><span class="sxs-lookup"><span data-stu-id="1d809-200">Note that the storage account must be in the same region as the Azure Site Recovery service, and be associated with the same subscription.</span></span>

## <a name="step-6-install-the-azure-recovery-services-agent"></a><span data-ttu-id="1d809-201">Step 6: Install the Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="1d809-201">Step 6: Install the Azure Recovery Services Agent</span></span>
1. <span data-ttu-id="1d809-202">Download the Azure Recovery Services agent at [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) and install it on each Hyper-V host server located in the VMM clouds you want to protect.</span><span class="sxs-lookup"><span data-stu-id="1d809-202">Download the Azure Recovery Services agent at [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) and install it on each Hyper-V host server located in the VMM clouds you want to protect.</span></span>
2. <span data-ttu-id="1d809-203">Run the following command on all VMM hosts:</span><span class="sxs-lookup"><span data-stu-id="1d809-203">Run the following command on all VMM hosts:</span></span>

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="1d809-204">Step 7: Configure cloud protection settings</span><span class="sxs-lookup"><span data-stu-id="1d809-204">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="1d809-205">Create a replication policy to Azure by running the following command:</span><span class="sxs-lookup"><span data-stu-id="1d809-205">Create a replication policy to Azure by running the following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify the number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. <span data-ttu-id="1d809-206">Get a protection container by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="1d809-206">Get a protection container by running the following commands:</span></span>

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. <span data-ttu-id="1d809-207">Get the policy details to a variable using the job that was created and mentioning the friendly policy name:</span><span class="sxs-lookup"><span data-stu-id="1d809-207">Get the policy details to a variable using the job that was created and mentioning the friendly policy name:</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="1d809-208">Start the association of the protection container with the replication policy:</span><span class="sxs-lookup"><span data-stu-id="1d809-208">Start the association of the protection container with the replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. <span data-ttu-id="1d809-209">After the job has finished, run the following command:</span><span class="sxs-lookup"><span data-stu-id="1d809-209">After the job has finished, run the following command:</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. <span data-ttu-id="1d809-210">After the job has finished processing, run the following command:</span><span class="sxs-lookup"><span data-stu-id="1d809-210">After the job has finished processing, run the following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="1d809-211">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span><span class="sxs-lookup"><span data-stu-id="1d809-211">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="1d809-212">Step 8: Configure network mapping</span><span class="sxs-lookup"><span data-stu-id="1d809-212">Step 8: Configure network mapping</span></span>
<span data-ttu-id="1d809-213">Before you begin network mapping verify that virtual machines on the source VMM server are connected to a VM network.</span><span class="sxs-lookup"><span data-stu-id="1d809-213">Before you begin network mapping verify that virtual machines on the source VMM server are connected to a VM network.</span></span> <span data-ttu-id="1d809-214">In addition, create one or more Azure virtual networks.</span><span class="sxs-lookup"><span data-stu-id="1d809-214">In addition, create one or more Azure virtual networks.</span></span>

<span data-ttu-id="1d809-215">Learn more about how to create a virtual network using Azure Resource Manager and PowerShell, in [Create a virtual network with a site-to-site VPN connection using Azure Resource Manager and PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="1d809-215">Learn more about how to create a virtual network using Azure Resource Manager and PowerShell, in [Create a virtual network with a site-to-site VPN connection using Azure Resource Manager and PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span></span>

<span data-ttu-id="1d809-216">Note that multiple Virtual Machine networks can be mapped to a single Azure network.</span><span class="sxs-lookup"><span data-stu-id="1d809-216">Note that multiple Virtual Machine networks can be mapped to a single Azure network.</span></span> <span data-ttu-id="1d809-217">If the target network has multiple subnets and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after fail-over.</span><span class="sxs-lookup"><span data-stu-id="1d809-217">If the target network has multiple subnets and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after fail-over.</span></span> <span data-ttu-id="1d809-218">If there is no target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span><span class="sxs-lookup"><span data-stu-id="1d809-218">If there is no target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>

1. <span data-ttu-id="1d809-219">The first command gets servers for the current Azure Site Recovery vault.</span><span class="sxs-lookup"><span data-stu-id="1d809-219">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="1d809-220">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span><span class="sxs-lookup"><span data-stu-id="1d809-220">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="1d809-221">The second command gets the site recovery network for the first server in the $Servers array.</span><span class="sxs-lookup"><span data-stu-id="1d809-221">The second command gets the site recovery network for the first server in the $Servers array.</span></span> <span data-ttu-id="1d809-222">The command stores the networks in the $Networks variable.</span><span class="sxs-lookup"><span data-stu-id="1d809-222">The command stores the networks in the $Networks variable.</span></span>

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. <span data-ttu-id="1d809-223">The third command gets Azure virtual networks, and then that value in the $AzureVmNetworks variable.</span><span class="sxs-lookup"><span data-stu-id="1d809-223">The third command gets Azure virtual networks, and then that value in the $AzureVmNetworks variable.</span></span>

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. <span data-ttu-id="1d809-224">The final cmdlet creates a mapping between the primary network and the Azure virtual machine network.</span><span class="sxs-lookup"><span data-stu-id="1d809-224">The final cmdlet creates a mapping between the primary network and the Azure virtual machine network.</span></span> <span data-ttu-id="1d809-225">The cmdlet specifies the primary network as the first element of $Networks.</span><span class="sxs-lookup"><span data-stu-id="1d809-225">The cmdlet specifies the primary network as the first element of $Networks.</span></span> <span data-ttu-id="1d809-226">The cmdlet specifies a virtual machine network as the first element of $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="1d809-226">The cmdlet specifies a virtual machine network as the first element of $AzureVmNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="1d809-227">Step 9: Enable protection for virtual machines</span><span class="sxs-lookup"><span data-stu-id="1d809-227">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="1d809-228">After the servers, clouds and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span><span class="sxs-lookup"><span data-stu-id="1d809-228">After the servers, clouds and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span>

 <span data-ttu-id="1d809-229">Note the following:</span><span class="sxs-lookup"><span data-stu-id="1d809-229">Note the following:</span></span>

* <span data-ttu-id="1d809-230">Virtual machines must meet Azure requirements.</span><span class="sxs-lookup"><span data-stu-id="1d809-230">Virtual machines must meet Azure requirements.</span></span> <span data-ttu-id="1d809-231">Check these in [Prerequisites and Support](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) in the planning guide.</span><span class="sxs-lookup"><span data-stu-id="1d809-231">Check these in [Prerequisites and Support](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) in the planning guide.</span></span>
* <span data-ttu-id="1d809-232">To enable protection, the operating system and operating system disk properties must be set for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1d809-232">To enable protection, the operating system and operating system disk properties must be set for the virtual machine.</span></span> <span data-ttu-id="1d809-233">When you create a virtual machine in VMM using a virtual machine template you can set the property.</span><span class="sxs-lookup"><span data-stu-id="1d809-233">When you create a virtual machine in VMM using a virtual machine template you can set the property.</span></span> <span data-ttu-id="1d809-234">You can also set these properties for existing virtual machines on the **General** and **Hardware Configuration** tabs of the virtual machine properties.</span><span class="sxs-lookup"><span data-stu-id="1d809-234">You can also set these properties for existing virtual machines on the **General** and **Hardware Configuration** tabs of the virtual machine properties.</span></span> <span data-ttu-id="1d809-235">If you don't set these properties in VMM you'll be able to configure them in the Azure Site Recovery portal.</span><span class="sxs-lookup"><span data-stu-id="1d809-235">If you don't set these properties in VMM you'll be able to configure them in the Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="1d809-236">To enable protection, run the following command to get the protection container:</span><span class="sxs-lookup"><span data-stu-id="1d809-236">To enable protection, run the following command to get the protection container:</span></span>

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. <span data-ttu-id="1d809-237">Get the protection entity (VM) by running the following command:</span><span class="sxs-lookup"><span data-stu-id="1d809-237">Get the protection entity (VM) by running the following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. <span data-ttu-id="1d809-238">Enable the DR for the VM by running the following command:</span><span class="sxs-lookup"><span data-stu-id="1d809-238">Enable the DR for the VM by running the following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a><span data-ttu-id="1d809-239">Test your deployment</span><span class="sxs-lookup"><span data-stu-id="1d809-239">Test your deployment</span></span>
<span data-ttu-id="1d809-240">To test your deployment you can run a test fail-over for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test fail-over for the plan.</span><span class="sxs-lookup"><span data-stu-id="1d809-240">To test your deployment you can run a test fail-over for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test fail-over for the plan.</span></span> <span data-ttu-id="1d809-241">Test fail-over simulates your fail-over and recovery mechanism in an isolated network.</span><span class="sxs-lookup"><span data-stu-id="1d809-241">Test fail-over simulates your fail-over and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="1d809-242">Note that:</span><span class="sxs-lookup"><span data-stu-id="1d809-242">Note that:</span></span>

* <span data-ttu-id="1d809-243">If you want to connect to the virtual machine in Azure using Remote Desktop after the fail-over, enable Remote Desktop Connection on the virtual machine before you run the test failover.</span><span class="sxs-lookup"><span data-stu-id="1d809-243">If you want to connect to the virtual machine in Azure using Remote Desktop after the fail-over, enable Remote Desktop Connection on the virtual machine before you run the test failover.</span></span>
* <span data-ttu-id="1d809-244">After fail-over, you'll use a public IP address to connect to the virtual machine in Azure using Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="1d809-244">After fail-over, you'll use a public IP address to connect to the virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="1d809-245">If you want to do this, ensure you don't have any domain policies that prevent you from connecting to a virtual machine using a public address.</span><span class="sxs-lookup"><span data-stu-id="1d809-245">If you want to do this, ensure you don't have any domain policies that prevent you from connecting to a virtual machine using a public address.</span></span>

<span data-ttu-id="1d809-246">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span><span class="sxs-lookup"><span data-stu-id="1d809-246">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="1d809-247">Run a test failover</span><span class="sxs-lookup"><span data-stu-id="1d809-247">Run a test failover</span></span>
- <span data-ttu-id="1d809-248">Start the test failover by running the following command:</span><span class="sxs-lookup"><span data-stu-id="1d809-248">Start the test failover by running the following command:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a><span data-ttu-id="1d809-249">Run a planned failover</span><span class="sxs-lookup"><span data-stu-id="1d809-249">Run a planned failover</span></span>
- <span data-ttu-id="1d809-250">Start the planned failover by running the following command:</span><span class="sxs-lookup"><span data-stu-id="1d809-250">Start the planned failover by running the following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="1d809-251">Run an unplanned failover</span><span class="sxs-lookup"><span data-stu-id="1d809-251">Run an unplanned failover</span></span>
- <span data-ttu-id="1d809-252">Start the unplanned failover by running the following command:</span><span class="sxs-lookup"><span data-stu-id="1d809-252">Start the unplanned failover by running the following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

## <a name=monitor></a> <span data-ttu-id="1d809-253">Monitor Activity</span><span class="sxs-lookup"><span data-stu-id="1d809-253">Monitor Activity</span></span>
<span data-ttu-id="1d809-254">Use the following commands to monitor the activity.</span><span class="sxs-lookup"><span data-stu-id="1d809-254">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="1d809-255">Note that you have to wait in between jobs for the processing to finish.</span><span class="sxs-lookup"><span data-stu-id="1d809-255">Note that you have to wait in between jobs for the processing to finish.</span></span>

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="1d809-256">Next steps</span><span class="sxs-lookup"><span data-stu-id="1d809-256">Next steps</span></span>
<span data-ttu-id="1d809-257">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="1d809-257">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
