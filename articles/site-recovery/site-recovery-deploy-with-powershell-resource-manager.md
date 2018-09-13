---
title: Replicate Hyper-V VMs with PowerShell and Azure Resource Manager | Microsoft Docs
description: Automate the replication of Hyper-V VMs to Azure with Azure Site Recovery using PowerShell and Azure Resource Manager.
services: site-recovery
documentationcenter: ''
author: bsiva
manager: abhiag
editor: ''
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 02/06/2017
ms.author: bsiva
ms.openlocfilehash: 3df4aaa018d31e9ee9526679ac1febbe5b75bb7e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549377"
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="88298-103">Replicate between on-premises Hyper-V virtual machines and Azure by using PowerShell and Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="88298-103">Replicate between on-premises Hyper-V virtual machines and Azure by using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-hyper-v-site-to-azure.md)
> * [PowerShell - Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
> * [Classic Portal](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a><span data-ttu-id="88298-107">Overview</span><span class="sxs-lookup"><span data-stu-id="88298-107">Overview</span></span>
<span data-ttu-id="88298-108">Azure Site Recovery contributes to your business continuity and disaster recovery strategy by orchestrating replication, failover, and recovery of virtual machines in a number of deployment scenarios.</span><span class="sxs-lookup"><span data-stu-id="88298-108">Azure Site Recovery contributes to your business continuity and disaster recovery strategy by orchestrating replication, failover, and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="88298-109">For a full list of deployment scenarios, see the [Azure Site Recovery overview](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="88298-109">For a full list of deployment scenarios, see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="88298-110">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="88298-110">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="88298-111">It can work with two types of modules: the Azure Profile module, or the Azure Resource Manager module.</span><span class="sxs-lookup"><span data-stu-id="88298-111">It can work with two types of modules: the Azure Profile module, or the Azure Resource Manager module.</span></span>

<span data-ttu-id="88298-112">Site Recovery PowerShell cmdlets, available with Azure PowerShell for Azure Resource Manager, help you protect and recover your servers in Azure.</span><span class="sxs-lookup"><span data-stu-id="88298-112">Site Recovery PowerShell cmdlets, available with Azure PowerShell for Azure Resource Manager, help you protect and recover your servers in Azure.</span></span>

<span data-ttu-id="88298-113">This article describes how to use Windows PowerShell, together with Azure Resource Manager, to deploy Site Recovery to configure and orchestrate server protection to Azure.</span><span class="sxs-lookup"><span data-stu-id="88298-113">This article describes how to use Windows PowerShell, together with Azure Resource Manager, to deploy Site Recovery to configure and orchestrate server protection to Azure.</span></span> <span data-ttu-id="88298-114">The example used in this article shows you how to protect, fail over, and recover virtual machines on a Hyper-V host to Azure, by using Azure PowerShell with Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="88298-114">The example used in this article shows you how to protect, fail over, and recover virtual machines on a Hyper-V host to Azure, by using Azure PowerShell with Azure Resource Manager.</span></span>

> [!NOTE]
> The Site Recovery PowerShell cmdlets currently allow you to configure the following: one Virtual Machine Manager site to another, a Virtual Machine Manager site to Azure, and a Hyper-V site to Azure.
>
>

<span data-ttu-id="88298-116">You don't need to be a PowerShell expert to use this article, but you do need to understand the basic concepts, such as modules, cmdlets, and sessions.</span><span class="sxs-lookup"><span data-stu-id="88298-116">You don't need to be a PowerShell expert to use this article, but you do need to understand the basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="88298-117">For more information about Windows PowerShell, see [Getting Started with Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span><span class="sxs-lookup"><span data-stu-id="88298-117">For more information about Windows PowerShell, see [Getting Started with Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="88298-118">You can also read more about [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="88298-118">You can also read more about [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

> [!NOTE]
> Microsoft partners that are part of the Cloud Solution Provider (CSP) program can configure and manage protection of their customers' servers to their customers' respective CSP subscriptions (tenant subscriptions).
>
>

## <a name="before-you-start"></a><span data-ttu-id="88298-120">Before you start</span><span class="sxs-lookup"><span data-stu-id="88298-120">Before you start</span></span>
<span data-ttu-id="88298-121">Make sure you have these prerequisites in place:</span><span class="sxs-lookup"><span data-stu-id="88298-121">Make sure you have these prerequisites in place:</span></span>

* <span data-ttu-id="88298-122">A [Microsoft Azure](https://azure.microsoft.com/) account.</span><span class="sxs-lookup"><span data-stu-id="88298-122">A [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="88298-123">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88298-123">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="88298-124">In addition, you can read about [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="88298-124">In addition, you can read about [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="88298-125">Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="88298-125">Azure PowerShell 1.0.</span></span> <span data-ttu-id="88298-126">For information about this release and how to install it, see [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="88298-126">For information about this release and how to install it, see [Azure PowerShell 1.0.](https://azure.microsoft.com/)</span></span>
* <span data-ttu-id="88298-127">The [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) and [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span><span class="sxs-lookup"><span data-stu-id="88298-127">The [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) and [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules.</span></span> <span data-ttu-id="88298-128">You can get the latest versions of these modules from the [PowerShell gallery](https://www.powershellgallery.com/)</span><span class="sxs-lookup"><span data-stu-id="88298-128">You can get the latest versions of these modules from the [PowerShell gallery](https://www.powershellgallery.com/)</span></span>

<span data-ttu-id="88298-129">This article illustrates how to use Azure Powershell with Azure Resource Manager to configure and manage protection of your servers.</span><span class="sxs-lookup"><span data-stu-id="88298-129">This article illustrates how to use Azure Powershell with Azure Resource Manager to configure and manage protection of your servers.</span></span> <span data-ttu-id="88298-130">The example used in this article shows you how to protect a virtual machine, running on a Hyper-V host, to Azure.</span><span class="sxs-lookup"><span data-stu-id="88298-130">The example used in this article shows you how to protect a virtual machine, running on a Hyper-V host, to Azure.</span></span> <span data-ttu-id="88298-131">The following prerequisites are specific to this example.</span><span class="sxs-lookup"><span data-stu-id="88298-131">The following prerequisites are specific to this example.</span></span> <span data-ttu-id="88298-132">For a more comprehensive set of requirements for the various Site Recovery scenarios, refer to the documentation pertaining to that scenario.</span><span class="sxs-lookup"><span data-stu-id="88298-132">For a more comprehensive set of requirements for the various Site Recovery scenarios, refer to the documentation pertaining to that scenario.</span></span>

* <span data-ttu-id="88298-133">A Hyper-V host running Windows Server 2012 R2 or Microsoft Hyper-V Server 2012 R2 containing one or more virtual machines.</span><span class="sxs-lookup"><span data-stu-id="88298-133">A Hyper-V host running Windows Server 2012 R2 or Microsoft Hyper-V Server 2012 R2 containing one or more virtual machines.</span></span>
* <span data-ttu-id="88298-134">Hyper-V servers connected to the Internet, either directly or through a proxy.</span><span class="sxs-lookup"><span data-stu-id="88298-134">Hyper-V servers connected to the Internet, either directly or through a proxy.</span></span>
* <span data-ttu-id="88298-135">The virtual machines you want to protect should conform with [Virtual Machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="88298-135">The virtual machines you want to protect should conform with [Virtual Machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

## <a name="step-1-sign-in-to-your-azure-account"></a><span data-ttu-id="88298-136">Step 1: Sign in to your Azure account</span><span class="sxs-lookup"><span data-stu-id="88298-136">Step 1: Sign in to your Azure account</span></span>
1. <span data-ttu-id="88298-137">Open a PowerShell console and run this command to sign in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="88298-137">Open a PowerShell console and run this command to sign in to your Azure account.</span></span> <span data-ttu-id="88298-138">The cmdlet brings up a web page that will prompt you for your account credentials.</span><span class="sxs-lookup"><span data-stu-id="88298-138">The cmdlet brings up a web page that will prompt you for your account credentials.</span></span>

        Login-AzureRmAccount

    <span data-ttu-id="88298-139">Alternately, you could also include your account credentials as a parameter to the `Login-AzureRmAccount` cmdlet, by using the `-Credential` parameter.</span><span class="sxs-lookup"><span data-stu-id="88298-139">Alternately, you could also include your account credentials as a parameter to the `Login-AzureRmAccount` cmdlet, by using the `-Credential` parameter.</span></span>

    <span data-ttu-id="88298-140">If you are CSP partner working on behalf of a tenant, specify the customer as a tenant, by using their tenantID or tenant primary domain name.</span><span class="sxs-lookup"><span data-stu-id="88298-140">If you are CSP partner working on behalf of a tenant, specify the customer as a tenant, by using their tenantID or tenant primary domain name.</span></span>

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. <span data-ttu-id="88298-141">An account can have several subscriptions, so you should associate the subscription you want to use with the account.</span><span class="sxs-lookup"><span data-stu-id="88298-141">An account can have several subscriptions, so you should associate the subscription you want to use with the account.</span></span>

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. <span data-ttu-id="88298-142">Verify that your subscription is registered to use the Azure providers for Recovery Services and Site Recovery, by using the following commands:</span><span class="sxs-lookup"><span data-stu-id="88298-142">Verify that your subscription is registered to use the Azure providers for Recovery Services and Site Recovery, by using the following commands:</span></span>

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   <span data-ttu-id="88298-143">In the output of these commands, if the **RegistrationState** is set to **Registered**, you can proceed to Step 2.</span><span class="sxs-lookup"><span data-stu-id="88298-143">In the output of these commands, if the **RegistrationState** is set to **Registered**, you can proceed to Step 2.</span></span> <span data-ttu-id="88298-144">If not, you should register the missing provider in your subscription.</span><span class="sxs-lookup"><span data-stu-id="88298-144">If not, you should register the missing provider in your subscription.</span></span>

   <span data-ttu-id="88298-145">To register the Azure provider for Site Recovery and Recovery Services, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="88298-145">To register the Azure provider for Site Recovery and Recovery Services, run the following commands:</span></span>

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   <span data-ttu-id="88298-146">Verify that the providers registered successfully by using the following commands: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` and `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span><span class="sxs-lookup"><span data-stu-id="88298-146">Verify that the providers registered successfully by using the following commands: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` and `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.</span></span>

## <a name="step-2-set-up-the-recovery-services-vault"></a><span data-ttu-id="88298-147">Step 2: Set up the Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="88298-147">Step 2: Set up the Recovery Services vault</span></span>
1. <span data-ttu-id="88298-148">Create an Azure Resource Manager resource group in which you'll create the vault, or use an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="88298-148">Create an Azure Resource Manager resource group in which you'll create the vault, or use an existing resource group.</span></span> <span data-ttu-id="88298-149">You can create a new resource group by using the following command:</span><span class="sxs-lookup"><span data-stu-id="88298-149">You can create a new resource group by using the following command:</span></span>

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    <span data-ttu-id="88298-150">where the $ResourceGroupName variable contains the name of the resource group you want to create, and the $Geo variable contains the Azure region in which to create the resource group (for example, "Brazil South").</span><span class="sxs-lookup"><span data-stu-id="88298-150">where the $ResourceGroupName variable contains the name of the resource group you want to create, and the $Geo variable contains the Azure region in which to create the resource group (for example, "Brazil South").</span></span>

    <span data-ttu-id="88298-151">You can obtain a list of resource groups in your subscription by using the `Get-AzureRmResourceGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="88298-151">You can obtain a list of resource groups in your subscription by using the `Get-AzureRmResourceGroup` cmdlet.</span></span>
2. <span data-ttu-id="88298-152">Create a new Azure Recovery Services vault as follows:</span><span class="sxs-lookup"><span data-stu-id="88298-152">Create a new Azure Recovery Services vault as follows:</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    <span data-ttu-id="88298-153">You can retrieve a list of existing vaults by using the `Get-AzureRmRecoveryServicesVault` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="88298-153">You can retrieve a list of existing vaults by using the `Get-AzureRmRecoveryServicesVault` cmdlet.</span></span>

> [!NOTE]
> If you wish to perform operations on Site Recovery vaults created using the classic portal or the Azure Service Management PowerShell module, you can retrieve a list of such vaults by using the `Get-AzureRmSiteRecoveryVault` cmdlet. You should create a new Recovery Services vault for all new operations. The Site Recovery vaults you've created earlier are supported, but don't have the latest features.
>
>

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="88298-157">Step 3: Set the Recovery Services vault context</span><span class="sxs-lookup"><span data-stu-id="88298-157">Step 3: Set the Recovery Services vault context</span></span>
1. <span data-ttu-id="88298-158">Set the vault context by running the following command:</span><span class="sxs-lookup"><span data-stu-id="88298-158">Set the vault context by running the following command:</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-the-site"></a><span data-ttu-id="88298-159">Step 4: Create a Hyper-V site and generate a new vault registration key for the site.</span><span class="sxs-lookup"><span data-stu-id="88298-159">Step 4: Create a Hyper-V site and generate a new vault registration key for the site.</span></span>
1. <span data-ttu-id="88298-160">Create a new Hyper-V site as follows:</span><span class="sxs-lookup"><span data-stu-id="88298-160">Create a new Hyper-V site as follows:</span></span>

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    <span data-ttu-id="88298-161">This cmdlet starts a Site Recovery job to create the site, and returns a Site Recovery job object.</span><span class="sxs-lookup"><span data-stu-id="88298-161">This cmdlet starts a Site Recovery job to create the site, and returns a Site Recovery job object.</span></span> <span data-ttu-id="88298-162">Wait for the job to complete and verify that the job completed successfully.</span><span class="sxs-lookup"><span data-stu-id="88298-162">Wait for the job to complete and verify that the job completed successfully.</span></span>

    <span data-ttu-id="88298-163">You can retrieve the job object, and thereby check the current status of the job, by using the Get-AzureRmSiteRecoveryJob cmdlet.</span><span class="sxs-lookup"><span data-stu-id="88298-163">You can retrieve the job object, and thereby check the current status of the job, by using the Get-AzureRmSiteRecoveryJob cmdlet.</span></span>
2. <span data-ttu-id="88298-164">Generate and download a registration key for the site, as follows:</span><span class="sxs-lookup"><span data-stu-id="88298-164">Generate and download a registration key for the site, as follows:</span></span>

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    <span data-ttu-id="88298-165">Copy the downloaded key to the Hyper-V host.</span><span class="sxs-lookup"><span data-stu-id="88298-165">Copy the downloaded key to the Hyper-V host.</span></span> <span data-ttu-id="88298-166">You need the key to register the Hyper-V host to the site.</span><span class="sxs-lookup"><span data-stu-id="88298-166">You need the key to register the Hyper-V host to the site.</span></span>

## <a name="step-5-install-the-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a><span data-ttu-id="88298-167">Step 5: Install the Azure Site Recovery provider and Azure Recovery Services Agent on your Hyper-V host</span><span class="sxs-lookup"><span data-stu-id="88298-167">Step 5: Install the Azure Site Recovery provider and Azure Recovery Services Agent on your Hyper-V host</span></span>
1. <span data-ttu-id="88298-168">Download the installer for the latest version of the provider from [Microsoft](https://aka.ms/downloaddra).</span><span class="sxs-lookup"><span data-stu-id="88298-168">Download the installer for the latest version of the provider from [Microsoft](https://aka.ms/downloaddra).</span></span>
2. <span data-ttu-id="88298-169">Run the installer on your Hyper-V host, and at the end of the installation continue to the registration step.</span><span class="sxs-lookup"><span data-stu-id="88298-169">Run the installer on your Hyper-V host, and at the end of the installation continue to the registration step.</span></span>
3. <span data-ttu-id="88298-170">When prompted, provide the downloaded site registration key, and complete registration of the Hyper-V host to the site.</span><span class="sxs-lookup"><span data-stu-id="88298-170">When prompted, provide the downloaded site registration key, and complete registration of the Hyper-V host to the site.</span></span>
4. <span data-ttu-id="88298-171">Verify that the Hyper-V host is registered to the site by using the following command:</span><span class="sxs-lookup"><span data-stu-id="88298-171">Verify that the Hyper-V host is registered to the site by using the following command:</span></span>

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-the-protection-container"></a><span data-ttu-id="88298-172">Step 6: Create a replication policy and associate it with the protection container</span><span class="sxs-lookup"><span data-stu-id="88298-172">Step 6: Create a replication policy and associate it with the protection container</span></span>
1. <span data-ttu-id="88298-173">Create a replication policy as follows:</span><span class="sxs-lookup"><span data-stu-id="88298-173">Create a replication policy as follows:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify the number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    <span data-ttu-id="88298-174">Check the returned job to ensure that the replication policy creation succeeds.</span><span class="sxs-lookup"><span data-stu-id="88298-174">Check the returned job to ensure that the replication policy creation succeeds.</span></span>

   > [!IMPORTANT]
   > The storage account specified should be in the same Azure region as your Recovery Services vault, and should have geo-replication enabled.
   >
   > * If the specified Recovery storage account is of type Azure Storage (Classic), failover of the protected machines recover the machine to Azure IaaS (Classic).
   > * If the specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of the protected machines recover the machine to Azure IaaS (Azure Resource Manager).
   >
   >
2. <span data-ttu-id="88298-178">Get the protection container corresponding to the site, as follows:</span><span class="sxs-lookup"><span data-stu-id="88298-178">Get the protection container corresponding to the site, as follows:</span></span>

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. <span data-ttu-id="88298-179">Start the association of the protection container with the replication policy, as follows:</span><span class="sxs-lookup"><span data-stu-id="88298-179">Start the association of the protection container with the replication policy, as follows:</span></span>

     <span data-ttu-id="88298-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span><span class="sxs-lookup"><span data-stu-id="88298-180">$Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer</span></span>

   <span data-ttu-id="88298-181">Wait for the association job to complete, and ensure that it completed successfully.</span><span class="sxs-lookup"><span data-stu-id="88298-181">Wait for the association job to complete, and ensure that it completed successfully.</span></span>

## <a name="step-7-enable-protection-for-virtual-machines"></a><span data-ttu-id="88298-182">Step 7: Enable protection for virtual machines</span><span class="sxs-lookup"><span data-stu-id="88298-182">Step 7: Enable protection for virtual machines</span></span>
1. <span data-ttu-id="88298-183">Get the protection entity corresponding to the VM you want to protect, as follows:</span><span class="sxs-lookup"><span data-stu-id="88298-183">Get the protection entity corresponding to the VM you want to protect, as follows:</span></span>

        $VMFriendlyName = "Fabrikam-app"                    #Name of the VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. <span data-ttu-id="88298-184">Start protecting the virtual machine, as follows:</span><span class="sxs-lookup"><span data-stu-id="88298-184">Start protecting the virtual machine, as follows:</span></span>

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > The storage account specified should be in the same Azure region as your Recovery Services vault, and should have geo-replication enabled.
   >
   > * If the specified Recovery storage account is of type Azure Storage (Classic), failover of the protected machines recover the machine to Azure IaaS (Classic).
   > * If the specified Recovery storage account is of type Azure Storage (Azure Resource Manager), failover of the protected machines recover the machine to Azure IaaS (Azure Resource Manager).
   >
   > If the VM you are protecting has more than one disk attached to it, specify the operating system disk by using the *OSDiskName* parameter.
   >
   >
3. <span data-ttu-id="88298-189">Wait for the virtual machines to reach a protected state after the initial replication.</span><span class="sxs-lookup"><span data-stu-id="88298-189">Wait for the virtual machines to reach a protected state after the initial replication.</span></span> <span data-ttu-id="88298-190">This can take a while, depending on factors such as the amount of data to be replicated and the available upstream bandwidth to Azure.</span><span class="sxs-lookup"><span data-stu-id="88298-190">This can take a while, depending on factors such as the amount of data to be replicated and the available upstream bandwidth to Azure.</span></span> <span data-ttu-id="88298-191">The job State and StateDescription are updated as follows, upon the VM reaching a protected state.</span><span class="sxs-lookup"><span data-stu-id="88298-191">The job State and StateDescription are updated as follows, upon the VM reaching a protected state.</span></span>

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. <span data-ttu-id="88298-192">Update recovery properties, such as the VM role size, and the Azure network to attach the virtual machine's network interface cards to upon failover.</span><span class="sxs-lookup"><span data-stu-id="88298-192">Update recovery properties, such as the VM role size, and the Azure network to attach the virtual machine's network interface cards to upon failover.</span></span>

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update the virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a><span data-ttu-id="88298-193">Step 8: Run a test failover</span><span class="sxs-lookup"><span data-stu-id="88298-193">Step 8: Run a test failover</span></span>
1. <span data-ttu-id="88298-194">Run a test failover job, as follows:</span><span class="sxs-lookup"><span data-stu-id="88298-194">Run a test failover job, as follows:</span></span>

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. <span data-ttu-id="88298-195">Verify that the test VM is created in Azure.</span><span class="sxs-lookup"><span data-stu-id="88298-195">Verify that the test VM is created in Azure.</span></span> <span data-ttu-id="88298-196">(The test failover job is suspended, after creating the test VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="88298-196">(The test failover job is suspended, after creating the test VM in Azure.</span></span> <span data-ttu-id="88298-197">The job completes by cleaning up the created artefacts upon resuming the job, as illustrated in the next step.)</span><span class="sxs-lookup"><span data-stu-id="88298-197">The job completes by cleaning up the created artefacts upon resuming the job, as illustrated in the next step.)</span></span>
3. <span data-ttu-id="88298-198">Complete the test failover, as follows:</span><span class="sxs-lookup"><span data-stu-id="88298-198">Complete the test failover, as follows:</span></span>

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a><span data-ttu-id="88298-199">Next Steps</span><span class="sxs-lookup"><span data-stu-id="88298-199">Next Steps</span></span>
<span data-ttu-id="88298-200">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="88298-200">[Read more](https://msdn.microsoft.com/library/azure/mt637930.aspx) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
