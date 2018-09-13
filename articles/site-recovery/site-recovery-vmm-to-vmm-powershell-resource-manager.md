---
title: Replicate Hyper-V VMs in VMM to a secondary site with PowerShell (Azure Resource Manager) | Microsoft Docs
description: Describes how to deploy Azure Site Recovery to orchestrate replication, failover and recovery of Hyper-V VMs in VMM clouds to a secondary VMM site using PowerShell (Resource Manager)
services: site-recovery
documentationcenter: ''
author: sujaytalasila
manager: rochakm
editor: raynew
ms.assetid: 9d38e9c3-217c-4e44-830c-575e9a4141f2
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: sutalasi
ms.openlocfilehash: 33b3e7322afafd623a10661e33abe7b959eeb512
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550390"
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-a-secondary-vmm-site-using-powershell-resource-manager"></a><span data-ttu-id="09626-103">Replicate Hyper-V virtual machines in VMM clouds to a secondary VMM site using PowerShell (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="09626-103">Replicate Hyper-V virtual machines in VMM clouds to a secondary VMM site using PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmm-to-vmm.md)
> * [Classic Portal](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="09626-107">Welcome to Azure Site Recovery!</span><span class="sxs-lookup"><span data-stu-id="09626-107">Welcome to Azure Site Recovery!</span></span> <span data-ttu-id="09626-108">Use this article if you want to replicate on-premises Hyper-V  virtual machines managed in System Center Virtual Machine Manager (VMM) clouds to a secondary site.</span><span class="sxs-lookup"><span data-stu-id="09626-108">Use this article if you want to replicate on-premises Hyper-V  virtual machines managed in System Center Virtual Machine Manager (VMM) clouds to a secondary site.</span></span>

<span data-ttu-id="09626-109">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to System Center VMM clouds in secondary site.</span><span class="sxs-lookup"><span data-stu-id="09626-109">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to System Center VMM clouds in secondary site.</span></span>

<span data-ttu-id="09626-110">The article includes prerequisites for the scenario, and shows you</span><span class="sxs-lookup"><span data-stu-id="09626-110">The article includes prerequisites for the scenario, and shows you</span></span>

* <span data-ttu-id="09626-111">How to set up a Recovery Services Vault</span><span class="sxs-lookup"><span data-stu-id="09626-111">How to set up a Recovery Services Vault</span></span>
* <span data-ttu-id="09626-112">Install the Azure Site Recovery Provider on the source VMM server and the target VMM server</span><span class="sxs-lookup"><span data-stu-id="09626-112">Install the Azure Site Recovery Provider on the source VMM server and the target VMM server</span></span>
* <span data-ttu-id="09626-113">Register the VMM server(s) in the vault</span><span class="sxs-lookup"><span data-stu-id="09626-113">Register the VMM server(s) in the vault</span></span>
* <span data-ttu-id="09626-114">Configure replication policy for the VMM Cloud.</span><span class="sxs-lookup"><span data-stu-id="09626-114">Configure replication policy for the VMM Cloud.</span></span> <span data-ttu-id="09626-115">The replication settings in the policy will be applied to all protected virtual machines</span><span class="sxs-lookup"><span data-stu-id="09626-115">The replication settings in the policy will be applied to all protected virtual machines</span></span>
* <span data-ttu-id="09626-116">Enable protection for the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="09626-116">Enable protection for the virtual machines.</span></span>
* <span data-ttu-id="09626-117">Test the failover of VMs individually or as part of a recovery plan to make sure everything is working as expected.</span><span class="sxs-lookup"><span data-stu-id="09626-117">Test the failover of VMs individually or as part of a recovery plan to make sure everything is working as expected.</span></span>
* <span data-ttu-id="09626-118">Perform a planned or an unplanned failover of VMs individually or as part of a recovery plan to make sure everything is working as expected.</span><span class="sxs-lookup"><span data-stu-id="09626-118">Perform a planned or an unplanned failover of VMs individually or as part of a recovery plan to make sure everything is working as expected.</span></span>

<span data-ttu-id="09626-119">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="09626-119">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> Azure has two different [deployment models](../azure-resource-manager/resource-manager-deployment-model.md) for creating and working with resources: Azure Resource Manager and classic. Azure also has two portals – the Azure classic portal that supports the classic deployment model, and the Azure portal with support for both deployment models. This article covers the Resource Manager deployment model.
>
>

## <a name="on-premises-prerequisites"></a><span data-ttu-id="09626-123">On-premises prerequisites</span><span class="sxs-lookup"><span data-stu-id="09626-123">On-premises prerequisites</span></span>
<span data-ttu-id="09626-124">Here's what you'll need in the primary and secondary on-premises sites to deploy this scenario:</span><span class="sxs-lookup"><span data-stu-id="09626-124">Here's what you'll need in the primary and secondary on-premises sites to deploy this scenario:</span></span>

| <span data-ttu-id="09626-125">**Prerequisites**</span><span class="sxs-lookup"><span data-stu-id="09626-125">**Prerequisites**</span></span> | <span data-ttu-id="09626-126">**Details**</span><span class="sxs-lookup"><span data-stu-id="09626-126">**Details**</span></span> |
| --- | --- |
| <span data-ttu-id="09626-127">**VMM**</span><span class="sxs-lookup"><span data-stu-id="09626-127">**VMM**</span></span> |<span data-ttu-id="09626-128">We recommend you deploy a VMM server in the primary site and a VMM server in the secondary site.</span><span class="sxs-lookup"><span data-stu-id="09626-128">We recommend you deploy a VMM server in the primary site and a VMM server in the secondary site.</span></span><br/><br/> <span data-ttu-id="09626-129">You can also [replicate between clouds on a single VMM server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span><span class="sxs-lookup"><span data-stu-id="09626-129">You can also [replicate between clouds on a single VMM server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span></span> <span data-ttu-id="09626-130">To do this you'll need at least two clouds configured on the VMM server.</span><span class="sxs-lookup"><span data-stu-id="09626-130">To do this you'll need at least two clouds configured on the VMM server.</span></span><br/><br/> <span data-ttu-id="09626-131">VMM servers should be running at least System Center 2012 SP1 with the latest updates.</span><span class="sxs-lookup"><span data-stu-id="09626-131">VMM servers should be running at least System Center 2012 SP1 with the latest updates.</span></span><br/><br/> <span data-ttu-id="09626-132">Each VMM server must have at one or more clouds configured and all clouds must have the Hyper-V Capacity profile set.</span><span class="sxs-lookup"><span data-stu-id="09626-132">Each VMM server must have at one or more clouds configured and all clouds must have the Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="09626-133">Clouds must contain one or more VMM host groups.</span><span class="sxs-lookup"><span data-stu-id="09626-133">Clouds must contain one or more VMM host groups.</span></span><br/><br/><span data-ttu-id="09626-134">Learn more about setting up VMM clouds in [Configuring the VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), and [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span><span class="sxs-lookup"><span data-stu-id="09626-134">Learn more about setting up VMM clouds in [Configuring the VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), and [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span></span><br/><br/> <span data-ttu-id="09626-135">VMM servers should have internet access.</span><span class="sxs-lookup"><span data-stu-id="09626-135">VMM servers should have internet access.</span></span> |
| <span data-ttu-id="09626-136">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="09626-136">**Hyper-V**</span></span> |<span data-ttu-id="09626-137">Hyper-V servers must be running at least Windows Server 2012 with the Hyper-V role and have the latest updates installed.</span><span class="sxs-lookup"><span data-stu-id="09626-137">Hyper-V servers must be running at least Windows Server 2012 with the Hyper-V role and have the latest updates installed.</span></span><br/><br/> <span data-ttu-id="09626-138">A Hyper-V server should contain one or more VMs.</span><span class="sxs-lookup"><span data-stu-id="09626-138">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="09626-139">Hyper-V host servers should be located in host groups in the primary and secondary VMM clouds.</span><span class="sxs-lookup"><span data-stu-id="09626-139">Hyper-V host servers should be located in host groups in the primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="09626-140">If you're running Hyper-V in a cluster on Windows Server 2012 R2 you should install [update 2961977](https://support.microsoft.com/kb/2961977)</span><span class="sxs-lookup"><span data-stu-id="09626-140">If you're running Hyper-V in a cluster on Windows Server 2012 R2 you should install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="09626-141">If you're running Hyper-V in a cluster on Windows Server 2012 note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span><span class="sxs-lookup"><span data-stu-id="09626-141">If you're running Hyper-V in a cluster on Windows Server 2012 note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="09626-142">You'll need to configure the cluster broker manually.</span><span class="sxs-lookup"><span data-stu-id="09626-142">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="09626-143">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span><span class="sxs-lookup"><span data-stu-id="09626-143">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span> |
| <span data-ttu-id="09626-144">**Provider**</span><span class="sxs-lookup"><span data-stu-id="09626-144">**Provider**</span></span> |<span data-ttu-id="09626-145">During Site Recovery deployment you install the Azure Site Recovery Provider on VMM servers.</span><span class="sxs-lookup"><span data-stu-id="09626-145">During Site Recovery deployment you install the Azure Site Recovery Provider on VMM servers.</span></span> <span data-ttu-id="09626-146">The Provider communicates with Site Recovery over HTTPS 443 to orchestrate replication.</span><span class="sxs-lookup"><span data-stu-id="09626-146">The Provider communicates with Site Recovery over HTTPS 443 to orchestrate replication.</span></span> <span data-ttu-id="09626-147">Data replication occurs between the primary and secondary Hyper-V servers over the LAN or a VPN connection.</span><span class="sxs-lookup"><span data-stu-id="09626-147">Data replication occurs between the primary and secondary Hyper-V servers over the LAN or a VPN connection.</span></span><br/><br/> <span data-ttu-id="09626-148">The Provider running on the VMM server needs access to these URLs: \*.hypervrecoverymanager.windowsazure.com; \*.accesscontrol.windows.net; \*.backup.windowsazure.com; \*.blob.core.windows.net; \*.store.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="09626-148">The Provider running on the VMM server needs access to these URLs: \*.hypervrecoverymanager.windowsazure.com; \*.accesscontrol.windows.net; \*.backup.windowsazure.com; \*.blob.core.windows.net; \*.store.core.windows.net.</span></span><br/><br/> <span data-ttu-id="09626-149">In addition allow firewall communication from the VMM servers to the [Azure datacenter IP ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and allow the HTTPS (443) protocol.</span><span class="sxs-lookup"><span data-stu-id="09626-149">In addition allow firewall communication from the VMM servers to the [Azure datacenter IP ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and allow the HTTPS (443) protocol.</span></span> |

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="09626-150">Network mapping prerequisites</span><span class="sxs-lookup"><span data-stu-id="09626-150">Network mapping prerequisites</span></span>
<span data-ttu-id="09626-151">Network mapping maps between VMM VM networks on the primary and secondary VMM servers to:</span><span class="sxs-lookup"><span data-stu-id="09626-151">Network mapping maps between VMM VM networks on the primary and secondary VMM servers to:</span></span>

* <span data-ttu-id="09626-152">Optimally place replica VMs on secondary Hyper-V hosts after failover.</span><span class="sxs-lookup"><span data-stu-id="09626-152">Optimally place replica VMs on secondary Hyper-V hosts after failover.</span></span>
* <span data-ttu-id="09626-153">Connect replica VMs to appropriate VM networks.</span><span class="sxs-lookup"><span data-stu-id="09626-153">Connect replica VMs to appropriate VM networks.</span></span>
* <span data-ttu-id="09626-154">If you don't configure network mapping replica VMs won't be connected to any network after failover.</span><span class="sxs-lookup"><span data-stu-id="09626-154">If you don't configure network mapping replica VMs won't be connected to any network after failover.</span></span>
* <span data-ttu-id="09626-155">If you want to set up network mapping during Site Recovery deployment here's what you'll need:</span><span class="sxs-lookup"><span data-stu-id="09626-155">If you want to set up network mapping during Site Recovery deployment here's what you'll need:</span></span>

  * <span data-ttu-id="09626-156">Make sure that VMs on the source Hyper-V host server are connected to a VMM VM network.</span><span class="sxs-lookup"><span data-stu-id="09626-156">Make sure that VMs on the source Hyper-V host server are connected to a VMM VM network.</span></span> <span data-ttu-id="09626-157">That network should be linked to a logical network that is associated with the cloud.</span><span class="sxs-lookup"><span data-stu-id="09626-157">That network should be linked to a logical network that is associated with the cloud.</span></span>
  * <span data-ttu-id="09626-158">Verify that the secondary cloud that you'll use for recovery has a corresponding VM network configured.</span><span class="sxs-lookup"><span data-stu-id="09626-158">Verify that the secondary cloud that you'll use for recovery has a corresponding VM network configured.</span></span> <span data-ttu-id="09626-159">That VM network should be linked to a logical network that's associated with the secondary cloud.</span><span class="sxs-lookup"><span data-stu-id="09626-159">That VM network should be linked to a logical network that's associated with the secondary cloud.</span></span>

<span data-ttu-id="09626-160">Learn more about configuring VMM networks in the below articles</span><span class="sxs-lookup"><span data-stu-id="09626-160">Learn more about configuring VMM networks in the below articles</span></span>

* [<span data-ttu-id="09626-161">How to configure logical networks in VMM</span><span class="sxs-lookup"><span data-stu-id="09626-161">How to configure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="09626-162">How to configure VM networks and gateways in VMM</span><span class="sxs-lookup"><span data-stu-id="09626-162">How to configure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)

<span data-ttu-id="09626-163">[Learn more](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) about how network mapping works.</span><span class="sxs-lookup"><span data-stu-id="09626-163">[Learn more](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) about how network mapping works.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="09626-164">PowerShell prerequisites</span><span class="sxs-lookup"><span data-stu-id="09626-164">PowerShell prerequisites</span></span>
<span data-ttu-id="09626-165">Make sure you have Azure PowerShell ready to go.</span><span class="sxs-lookup"><span data-stu-id="09626-165">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="09626-166">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span><span class="sxs-lookup"><span data-stu-id="09626-166">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="09626-167">For information about setting up PowerShell, see the [Guide to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="09626-167">For information about setting up PowerShell, see the [Guide to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="09626-168">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](https://msdn.microsoft.com/library/dn850420.aspx).</span><span class="sxs-lookup"><span data-stu-id="09626-168">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](https://msdn.microsoft.com/library/dn850420.aspx).</span></span>

<span data-ttu-id="09626-169">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see the [Guide to get Started with Azure Cmdlets](https://msdn.microsoft.com/library/azure/jj554332.aspx).</span><span class="sxs-lookup"><span data-stu-id="09626-169">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see the [Guide to get Started with Azure Cmdlets](https://msdn.microsoft.com/library/azure/jj554332.aspx).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="09626-170">Step 1: Set the subscription</span><span class="sxs-lookup"><span data-stu-id="09626-170">Step 1: Set the subscription</span></span>
1. <span data-ttu-id="09626-171">From Azure powershell, login to your Azure account: using the following cmdlets</span><span class="sxs-lookup"><span data-stu-id="09626-171">From Azure powershell, login to your Azure account: using the following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="09626-172">Get a list of your subscriptions.</span><span class="sxs-lookup"><span data-stu-id="09626-172">Get a list of your subscriptions.</span></span> <span data-ttu-id="09626-173">This will also list the subscriptionIDs for each of the subscriptions.</span><span class="sxs-lookup"><span data-stu-id="09626-173">This will also list the subscriptionIDs for each of the subscriptions.</span></span> <span data-ttu-id="09626-174">Note down the subscriptionID of the subscription in which you wish to create the recovery services vault</span><span class="sxs-lookup"><span data-stu-id="09626-174">Note down the subscriptionID of the subscription in which you wish to create the recovery services vault</span></span>    

        Get-AzureRmSubscription
3. <span data-ttu-id="09626-175">Set the subscription in which the recovery services vault is to be created by mentioning the subscription ID</span><span class="sxs-lookup"><span data-stu-id="09626-175">Set the subscription in which the recovery services vault is to be created by mentioning the subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="09626-176">Step 2: Create a Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="09626-176">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="09626-177">Create an Azure Resource Manager resource group if you don't have one already</span><span class="sxs-lookup"><span data-stu-id="09626-177">Create an Azure Resource Manager resource group if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="09626-178">Create a new Recovery Services vault and save the created ASR vault object in a variable (will be used later).</span><span class="sxs-lookup"><span data-stu-id="09626-178">Create a new Recovery Services vault and save the created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="09626-179">You can also retrieve the ASR vault object post creation using the Get-AzureRMRecoveryServicesVault cmdlet:-</span><span class="sxs-lookup"><span data-stu-id="09626-179">You can also retrieve the ASR vault object post creation using the Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="09626-180">Step 3: Set the Recovery Services Vault context</span><span class="sxs-lookup"><span data-stu-id="09626-180">Step 3: Set the Recovery Services Vault context</span></span>
1. <span data-ttu-id="09626-181">If you have a vault already created, run the below command to get the vault.</span><span class="sxs-lookup"><span data-stu-id="09626-181">If you have a vault already created, run the below command to get the vault.</span></span>

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. <span data-ttu-id="09626-182">Set the vault context by running the below command.</span><span class="sxs-lookup"><span data-stu-id="09626-182">Set the vault context by running the below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="09626-183">Step 4: Install the Azure Site Recovery Provider</span><span class="sxs-lookup"><span data-stu-id="09626-183">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="09626-184">On the VMM machine, create a directory by running the following command:</span><span class="sxs-lookup"><span data-stu-id="09626-184">On the VMM machine, create a directory by running the following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="09626-185">Extract the files using the downloaded provider by running the following command</span><span class="sxs-lookup"><span data-stu-id="09626-185">Extract the files using the downloaded provider by running the following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="09626-186">Install the provider using the following commands:</span><span class="sxs-lookup"><span data-stu-id="09626-186">Install the provider using the following commands:</span></span>

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

   <span data-ttu-id="09626-187">Wait for the installation to finish.</span><span class="sxs-lookup"><span data-stu-id="09626-187">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="09626-188">Register the server in the vault using the following command:</span><span class="sxs-lookup"><span data-stu-id="09626-188">Register the server in the vault using the following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a><span data-ttu-id="09626-189">Step 5: Create and associate a replication policy</span><span class="sxs-lookup"><span data-stu-id="09626-189">Step 5: Create and associate a replication policy</span></span>
1. <span data-ttu-id="09626-190">Create a Hyper-V 2012 R2 replication policy by running the following command:</span><span class="sxs-lookup"><span data-stu-id="09626-190">Create a Hyper-V 2012 R2 replication policy by running the following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify the number of hours to retain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify the frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify the port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > The VMM cloud can contain Hyper-V hosts running different versions of Windows Server (as mentioned in the Hyper-V prerequisites), but the replication policy is OS version specific. If you have different hosts running on different operating system versions, then create separate replication policies for each type of OS version. For eg: If you have five hosts running on Windows Servers 2012 and three on Windows Server 2012 R2, create two replication polices – one for each type of operating system versions.

1. <span data-ttu-id="09626-194">Get the primary protection container (primary VMM Cloud) and recovery protection container (recovery VMM Cloud) by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="09626-194">Get the primary protection container (primary VMM Cloud) and recovery protection container (recovery VMM Cloud) by running the following commands:</span></span>

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. <span data-ttu-id="09626-195">Retrieve the policy you created in step 1 using the friendly name of the policy</span><span class="sxs-lookup"><span data-stu-id="09626-195">Retrieve the policy you created in step 1 using the friendly name of the policy</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="09626-196">Start the association of the protection container (VMM Cloud) with the replication policy:</span><span class="sxs-lookup"><span data-stu-id="09626-196">Start the association of the protection container (VMM Cloud) with the replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. <span data-ttu-id="09626-197">Wait for the policy association job to complete.</span><span class="sxs-lookup"><span data-stu-id="09626-197">Wait for the policy association job to complete.</span></span> <span data-ttu-id="09626-198">You can check if the job has completed using the following PowerShell snippet.</span><span class="sxs-lookup"><span data-stu-id="09626-198">You can check if the job has completed using the following PowerShell snippet.</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   <span data-ttu-id="09626-199">After the job has finished processing, run the following command:</span><span class="sxs-lookup"><span data-stu-id="09626-199">After the job has finished processing, run the following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="09626-200">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span><span class="sxs-lookup"><span data-stu-id="09626-200">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-6-configure-network-mapping"></a><span data-ttu-id="09626-201">Step 6: Configure network mapping</span><span class="sxs-lookup"><span data-stu-id="09626-201">Step 6: Configure network mapping</span></span>
1. <span data-ttu-id="09626-202">The first command gets servers for the current Azure Site Recovery vault.</span><span class="sxs-lookup"><span data-stu-id="09626-202">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="09626-203">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span><span class="sxs-lookup"><span data-stu-id="09626-203">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="09626-204">The below commands get the site recovery network for the source VMM server and the target VMM server.</span><span class="sxs-lookup"><span data-stu-id="09626-204">The below commands get the site recovery network for the source VMM server and the target VMM server.</span></span>

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > The source VMM server can be the first one or the second one in the servers array. Check the names of the VMM servers and get the networks appropriately


1. <span data-ttu-id="09626-207">The final cmdlet creates a mapping between the primary network and the recovery network.</span><span class="sxs-lookup"><span data-stu-id="09626-207">The final cmdlet creates a mapping between the primary network and the recovery network.</span></span> <span data-ttu-id="09626-208">The cmdlet specifies the primary network as the first element of $PrimaryNetworks and the recovery network as the first element of $RecoveryNetworks.</span><span class="sxs-lookup"><span data-stu-id="09626-208">The cmdlet specifies the primary network as the first element of $PrimaryNetworks and the recovery network as the first element of $RecoveryNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a><span data-ttu-id="09626-209">Step 7: Configure storage mapping</span><span class="sxs-lookup"><span data-stu-id="09626-209">Step 7: Configure storage mapping</span></span>
1. <span data-ttu-id="09626-210">The below command gets the list of storage classifications into $storageclassifications variable.</span><span class="sxs-lookup"><span data-stu-id="09626-210">The below command gets the list of storage classifications into $storageclassifications variable.</span></span>

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. <span data-ttu-id="09626-211">The below commands get the source classification into $SourceClassificaion variable and target classification into $TargetClassification variable.</span><span class="sxs-lookup"><span data-stu-id="09626-211">The below commands get the source classification into $SourceClassificaion variable and target classification into $TargetClassification variable.</span></span>

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > The source and target classifications can be any element in the array. Refer to the output of the below command to figure the index of source and target classifications in $storageclassifications array.

    > Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table


1. <span data-ttu-id="09626-215">The below cmdlet creates a mapping between the source classification and the target classification.</span><span class="sxs-lookup"><span data-stu-id="09626-215">The below cmdlet creates a mapping between the source classification and the target classification.</span></span>

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a><span data-ttu-id="09626-216">Step 8: Enable protection for virtual machines</span><span class="sxs-lookup"><span data-stu-id="09626-216">Step 8: Enable protection for virtual machines</span></span>
<span data-ttu-id="09626-217">After the servers, clouds and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span><span class="sxs-lookup"><span data-stu-id="09626-217">After the servers, clouds and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span>

1. <span data-ttu-id="09626-218">To enable protection, run the following command to get the protection container:</span><span class="sxs-lookup"><span data-stu-id="09626-218">To enable protection, run the following command to get the protection container:</span></span>

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. <span data-ttu-id="09626-219">Get the protection entity (VM) by running the following command:</span><span class="sxs-lookup"><span data-stu-id="09626-219">Get the protection entity (VM) by running the following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. <span data-ttu-id="09626-220">Enable replication for the VM by running the following command:</span><span class="sxs-lookup"><span data-stu-id="09626-220">Enable replication for the VM by running the following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a><span data-ttu-id="09626-221">Test your deployment</span><span class="sxs-lookup"><span data-stu-id="09626-221">Test your deployment</span></span>
<span data-ttu-id="09626-222">To test your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for the plan.</span><span class="sxs-lookup"><span data-stu-id="09626-222">To test your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for the plan.</span></span> <span data-ttu-id="09626-223">Test failover simulates your failover and recovery mechanism in an isolated network.</span><span class="sxs-lookup"><span data-stu-id="09626-223">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span>

> [!NOTE]
> You can create a recovery plan for your application in Azure portal.
>
>

<span data-ttu-id="09626-225">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span><span class="sxs-lookup"><span data-stu-id="09626-225">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="09626-226">Run a test failover</span><span class="sxs-lookup"><span data-stu-id="09626-226">Run a test failover</span></span>
1. <span data-ttu-id="09626-227">Run the below cmdlets to get the VM network to which you want to test failover your VMs to.</span><span class="sxs-lookup"><span data-stu-id="09626-227">Run the below cmdlets to get the VM network to which you want to test failover your VMs to.</span></span>

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. <span data-ttu-id="09626-228">Perform a test failover of a VM by doing the following:</span><span class="sxs-lookup"><span data-stu-id="09626-228">Perform a test failover of a VM by doing the following:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. <span data-ttu-id="09626-229">Perform a test failover of a recovery plan by doing the following:</span><span class="sxs-lookup"><span data-stu-id="09626-229">Perform a test failover of a recovery plan by doing the following:</span></span>

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a><span data-ttu-id="09626-230">Run a planned failover</span><span class="sxs-lookup"><span data-stu-id="09626-230">Run a planned failover</span></span>
1. <span data-ttu-id="09626-231">Perform a planned failover of a VM by doing the following:</span><span class="sxs-lookup"><span data-stu-id="09626-231">Perform a planned failover of a VM by doing the following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. <span data-ttu-id="09626-232">Perform a planned failover of a recovery plan by doing the following:</span><span class="sxs-lookup"><span data-stu-id="09626-232">Perform a planned failover of a recovery plan by doing the following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="09626-233">Run an unplanned failover</span><span class="sxs-lookup"><span data-stu-id="09626-233">Run an unplanned failover</span></span>
1. <span data-ttu-id="09626-234">Perform an unplanned failover of a VM by doing the following:</span><span class="sxs-lookup"><span data-stu-id="09626-234">Perform an unplanned failover of a VM by doing the following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

<span data-ttu-id="09626-235">2.Perform an unplanned failover of a recovery plan by doing the following:</span><span class="sxs-lookup"><span data-stu-id="09626-235">2.Perform an unplanned failover of a recovery plan by doing the following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <a name=monitor></a> <span data-ttu-id="09626-236">Monitor Activity</span><span class="sxs-lookup"><span data-stu-id="09626-236">Monitor Activity</span></span>
<span data-ttu-id="09626-237">Use the following commands to monitor the activity.</span><span class="sxs-lookup"><span data-stu-id="09626-237">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="09626-238">Note that you have to wait in between jobs for the processing to finish.</span><span class="sxs-lookup"><span data-stu-id="09626-238">Note that you have to wait in between jobs for the processing to finish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="09626-239">Next steps</span><span class="sxs-lookup"><span data-stu-id="09626-239">Next steps</span></span>
<span data-ttu-id="09626-240">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="09626-240">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
