---
title: Replicate Hyper-V VMs to Azure in the classic portal with PowerShell | Microsoft Docs
description: Automate the replication of Hyper-V virtual machines in VMM clouds using Site Recovery and PowerShell in the classic portal
services: site-recovery
documentationcenter: ''
author: bsiva
manager: abhiag
editor: tysonn
ms.assetid: 9011f567-e0b4-4306-951a-b30da19f5db6
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: bsiva
ms.openlocfilehash: d5fed9feb2292002a06c426cdd9e4e18f67bd3ec
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555080"
---
# <a name="replicate-hyper-v-vms-to-azure-with-powershell-in-the-classic-portal"></a><span data-ttu-id="57966-103">Replicate Hyper-V VMs to Azure with PowerShell in the classic portal</span><span class="sxs-lookup"><span data-stu-id="57966-103">Replicate Hyper-V VMs to Azure with PowerShell in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmm-to-azure.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [Classic Portal](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell - Classic](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="57966-108">Overview</span><span class="sxs-lookup"><span data-stu-id="57966-108">Overview</span></span>
<span data-ttu-id="57966-109">Azure Site Recovery contributes to your business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span><span class="sxs-lookup"><span data-stu-id="57966-109">Azure Site Recovery contributes to your business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="57966-110">For a full list of deployment scenarios see the [Azure Site Recovery overview](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="57966-110">For a full list of deployment scenarios see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="57966-111">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to Azure storage.</span><span class="sxs-lookup"><span data-stu-id="57966-111">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to Azure storage.</span></span>

<span data-ttu-id="57966-112">The article includes prerequisites for the scenario, and shows you how to set up a Site Recovery vault, install the Azure Site Recovery Provider on the source VMM server, register the server in the vault, add an Azure storage account, install the Azure Recovery Services agent on Hyper-V host servers, configure protection settings for VMM clouds that will be applied to all protected virtual machines, and then enable protection for those virtual machines.</span><span class="sxs-lookup"><span data-stu-id="57966-112">The article includes prerequisites for the scenario, and shows you how to set up a Site Recovery vault, install the Azure Site Recovery Provider on the source VMM server, register the server in the vault, add an Azure storage account, install the Azure Recovery Services agent on Hyper-V host servers, configure protection settings for VMM clouds that will be applied to all protected virtual machines, and then enable protection for those virtual machines.</span></span> <span data-ttu-id="57966-113">Finish up by testing the failover to make sure everything's working as expected.</span><span class="sxs-lookup"><span data-stu-id="57966-113">Finish up by testing the failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="57966-114">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="57966-114">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md). This article covers using the Classic deployment model.
>
>

## <a name="before-you-start"></a><span data-ttu-id="57966-117">Before you start</span><span class="sxs-lookup"><span data-stu-id="57966-117">Before you start</span></span>
<span data-ttu-id="57966-118">Make sure you have these prerequisites in place:</span><span class="sxs-lookup"><span data-stu-id="57966-118">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="57966-119">Azure prerequisites</span><span class="sxs-lookup"><span data-stu-id="57966-119">Azure prerequisites</span></span>
* <span data-ttu-id="57966-120">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span><span class="sxs-lookup"><span data-stu-id="57966-120">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="57966-121">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="57966-121">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="57966-122">You'll need an Azure storage account to store replicated data.</span><span class="sxs-lookup"><span data-stu-id="57966-122">You'll need an Azure storage account to store replicated data.</span></span> <span data-ttu-id="57966-123">The account needs geo-replication enabled.</span><span class="sxs-lookup"><span data-stu-id="57966-123">The account needs geo-replication enabled.</span></span> <span data-ttu-id="57966-124">It should be in the same region as the Azure Site Recovery vault and be associated with the same subscription.</span><span class="sxs-lookup"><span data-stu-id="57966-124">It should be in the same region as the Azure Site Recovery vault and be associated with the same subscription.</span></span> <span data-ttu-id="57966-125">[Learn more about Azure storage](../storage/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="57966-125">[Learn more about Azure storage](../storage/storage-introduction.md).</span></span>
* <span data-ttu-id="57966-126">You'll need to make sure that virtual machines you want to protect comply with [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="57966-126">You'll need to make sure that virtual machines you want to protect comply with [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

### <a name="vmm-prerequisites"></a><span data-ttu-id="57966-127">VMM prerequisites</span><span class="sxs-lookup"><span data-stu-id="57966-127">VMM prerequisites</span></span>
* <span data-ttu-id="57966-128">You'll need  VMM server running on System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="57966-128">You'll need  VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="57966-129">You'll need at least one cloud on the VMM server you want to protect.</span><span class="sxs-lookup"><span data-stu-id="57966-129">You'll need at least one cloud on the VMM server you want to protect.</span></span> <span data-ttu-id="57966-130">The cloud should contain:</span><span class="sxs-lookup"><span data-stu-id="57966-130">The cloud should contain:</span></span>
  * <span data-ttu-id="57966-131">One or more VMM host groups.</span><span class="sxs-lookup"><span data-stu-id="57966-131">One or more VMM host groups.</span></span>
  * <span data-ttu-id="57966-132">One or more Hyper-V host servers or clusters in each host group .</span><span class="sxs-lookup"><span data-stu-id="57966-132">One or more Hyper-V host servers or clusters in each host group .</span></span>
  * <span data-ttu-id="57966-133">One or more virtual machines on the source Hyper-V server.</span><span class="sxs-lookup"><span data-stu-id="57966-133">One or more virtual machines on the source Hyper-V server.</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="57966-134">Hyper-V prerequisites</span><span class="sxs-lookup"><span data-stu-id="57966-134">Hyper-V prerequisites</span></span>
* <span data-ttu-id="57966-135">The host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have the latest updates installed.</span><span class="sxs-lookup"><span data-stu-id="57966-135">The host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have the latest updates installed.</span></span>
* <span data-ttu-id="57966-136">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span><span class="sxs-lookup"><span data-stu-id="57966-136">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="57966-137">You'll need to configure the cluster broker manually.</span><span class="sxs-lookup"><span data-stu-id="57966-137">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="57966-138">To do this, in Server Manager > Failover Cluster Manager, connect to the cluster, click **Configure Role** and select **Hyper-V Replica Broker** in the **Select Role** screen of the High Availability wizard.</span><span class="sxs-lookup"><span data-stu-id="57966-138">To do this, in Server Manager > Failover Cluster Manager, connect to the cluster, click **Configure Role** and select **Hyper-V Replica Broker** in the **Select Role** screen of the High Availability wizard.</span></span>
* <span data-ttu-id="57966-139">Any Hyper-V host server or cluster for which you want to manage protection must be included in a VMM cloud.</span><span class="sxs-lookup"><span data-stu-id="57966-139">Any Hyper-V host server or cluster for which you want to manage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="57966-140">Network mapping prerequisites</span><span class="sxs-lookup"><span data-stu-id="57966-140">Network mapping prerequisites</span></span>
<span data-ttu-id="57966-141">When you protect virtual machines in Azure network mapping maps between VM networks on the source VMM server and target Azure networks to enable the following:</span><span class="sxs-lookup"><span data-stu-id="57966-141">When you protect virtual machines in Azure network mapping maps between VM networks on the source VMM server and target Azure networks to enable the following:</span></span>

* <span data-ttu-id="57966-142">All machines which fail over on the same network can connect to each other, irrespective of which recovery plan they are in.</span><span class="sxs-lookup"><span data-stu-id="57966-142">All machines which fail over on the same network can connect to each other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="57966-143">If a network gateway is setup on the target Azure network, virtual machines can connect to other on-premises virtual machines.</span><span class="sxs-lookup"><span data-stu-id="57966-143">If a network gateway is setup on the target Azure network, virtual machines can connect to other on-premises virtual machines.</span></span>
* <span data-ttu-id="57966-144">If you don’t configure network mapping only virtual machines that fail over in the same recovery plan will be able to connect to each other after failover to Azure.</span><span class="sxs-lookup"><span data-stu-id="57966-144">If you don’t configure network mapping only virtual machines that fail over in the same recovery plan will be able to connect to each other after failover to Azure.</span></span>

<span data-ttu-id="57966-145">If you want to deploy network mapping you'll need the following:</span><span class="sxs-lookup"><span data-stu-id="57966-145">If you want to deploy network mapping you'll need the following:</span></span>

* <span data-ttu-id="57966-146">The virtual machines you want to protect on the source VMM server should be connected to a VM network.</span><span class="sxs-lookup"><span data-stu-id="57966-146">The virtual machines you want to protect on the source VMM server should be connected to a VM network.</span></span> <span data-ttu-id="57966-147">That network should be linked to a logical network that is associated with the cloud.</span><span class="sxs-lookup"><span data-stu-id="57966-147">That network should be linked to a logical network that is associated with the cloud.</span></span>
* <span data-ttu-id="57966-148">An Azure network to which replicated virtual machines can connect after failover.</span><span class="sxs-lookup"><span data-stu-id="57966-148">An Azure network to which replicated virtual machines can connect after failover.</span></span> <span data-ttu-id="57966-149">You'll select this network at the time of failover.</span><span class="sxs-lookup"><span data-stu-id="57966-149">You'll select this network at the time of failover.</span></span> <span data-ttu-id="57966-150">The network should be in the same region as your Azure Site Recovery subscription.</span><span class="sxs-lookup"><span data-stu-id="57966-150">The network should be in the same region as your Azure Site Recovery subscription.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="57966-151">PowerShell prerequisites</span><span class="sxs-lookup"><span data-stu-id="57966-151">PowerShell prerequisites</span></span>
<span data-ttu-id="57966-152">Make sure you have Azure PowerShell ready to go.</span><span class="sxs-lookup"><span data-stu-id="57966-152">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="57966-153">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span><span class="sxs-lookup"><span data-stu-id="57966-153">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="57966-154">For information about setting up PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="57966-154">For information about setting up PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="57966-155">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](https://msdn.microsoft.com/library/dn850420.aspx).</span><span class="sxs-lookup"><span data-stu-id="57966-155">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](https://msdn.microsoft.com/library/dn850420.aspx).</span></span>

<span data-ttu-id="57966-156">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see [Get Started with Azure Cmdlets](https://msdn.microsoft.com/library/azure/jj554332.aspx).</span><span class="sxs-lookup"><span data-stu-id="57966-156">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see [Get Started with Azure Cmdlets](https://msdn.microsoft.com/library/azure/jj554332.aspx).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="57966-157">Step 1: Set the subscription</span><span class="sxs-lookup"><span data-stu-id="57966-157">Step 1: Set the subscription</span></span>
<span data-ttu-id="57966-158">In PowerShell, run these cmdlets:</span><span class="sxs-lookup"><span data-stu-id="57966-158">In PowerShell, run these cmdlets:</span></span>

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

<span data-ttu-id="57966-159">Replace the elements within the "< >" with your specific information.</span><span class="sxs-lookup"><span data-stu-id="57966-159">Replace the elements within the "< >" with your specific information.</span></span>

## <a name="step-2-create-a-site-recovery-vault"></a><span data-ttu-id="57966-160">Step 2: Create a Site Recovery vault</span><span class="sxs-lookup"><span data-stu-id="57966-160">Step 2: Create a Site Recovery vault</span></span>
<span data-ttu-id="57966-161">In PowerShell, replace the elements within the "< >" with your specific information, and run these commands:</span><span class="sxs-lookup"><span data-stu-id="57966-161">In PowerShell, replace the elements within the "< >" with your specific information, and run these commands:</span></span>

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a><span data-ttu-id="57966-162">Step 3: Generate a vault registration key</span><span class="sxs-lookup"><span data-stu-id="57966-162">Step 3: Generate a vault registration key</span></span>
<span data-ttu-id="57966-163">Generate a registration key in the vault.</span><span class="sxs-lookup"><span data-stu-id="57966-163">Generate a registration key in the vault.</span></span> <span data-ttu-id="57966-164">After you download the Azure Site Recovery Provider and install it on the VMM server, you'll use this key to register the VMM server in the vault.</span><span class="sxs-lookup"><span data-stu-id="57966-164">After you download the Azure Site Recovery Provider and install it on the VMM server, you'll use this key to register the VMM server in the vault.</span></span>

1. <span data-ttu-id="57966-165">Get the vault setting file and set the context:</span><span class="sxs-lookup"><span data-stu-id="57966-165">Get the vault setting file and set the context:</span></span>

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. <span data-ttu-id="57966-166">Set the vault context by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="57966-166">Set the vault context by running the following commands:</span></span>

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="57966-167">Step 4: Install the Azure Site Recovery Provider</span><span class="sxs-lookup"><span data-stu-id="57966-167">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="57966-168">On the VMM machine, create a directory by running the following command:</span><span class="sxs-lookup"><span data-stu-id="57966-168">On the VMM machine, create a directory by running the following command:</span></span>

   ```

   pushd C:\ASR\

   ```
2. <span data-ttu-id="57966-169">Extract the files using the downloaded provider by running the following command</span><span class="sxs-lookup"><span data-stu-id="57966-169">Extract the files using the downloaded provider by running the following command</span></span>

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. <span data-ttu-id="57966-170">Install the provider using the following commands:</span><span class="sxs-lookup"><span data-stu-id="57966-170">Install the provider using the following commands:</span></span>

   ```

   .\SetupDr.exe /i

   ```

   ```

   $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
   do
   {
     $isNotInstalled = $true;
     if(Test-Path $installationRegPath)
     {
         $isNotInstalled = $false;
     }
   }While($isNotInstalled)

   ```

   <span data-ttu-id="57966-171">Wait for the installation to finish.</span><span class="sxs-lookup"><span data-stu-id="57966-171">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="57966-172">Register the server in the vault using the following command:</span><span class="sxs-lookup"><span data-stu-id="57966-172">Register the server in the vault using the following command:</span></span>

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="57966-173">Step 5: Create an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="57966-173">Step 5: Create an Azure storage account</span></span>
<span data-ttu-id="57966-174">If you don't have an Azure storage account, create a geo-replication enabled account by running the following command:</span><span class="sxs-lookup"><span data-stu-id="57966-174">If you don't have an Azure storage account, create a geo-replication enabled account by running the following command:</span></span>

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

<span data-ttu-id="57966-175">Note that the storage account must be in the same region as the Azure Site Recovery service, and be associated with the same subscription.</span><span class="sxs-lookup"><span data-stu-id="57966-175">Note that the storage account must be in the same region as the Azure Site Recovery service, and be associated with the same subscription.</span></span>

## <a name="step-6-install-the-azure-recovery-services-agent"></a><span data-ttu-id="57966-176">Step 6: Install the Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="57966-176">Step 6: Install the Azure Recovery Services Agent</span></span>
<span data-ttu-id="57966-177">From the Azure portal, install the Azure Recovery Services agent on each Hyper-V host server located in the VMM clouds you want to protect.</span><span class="sxs-lookup"><span data-stu-id="57966-177">From the Azure portal, install the Azure Recovery Services agent on each Hyper-V host server located in the VMM clouds you want to protect.</span></span>

<span data-ttu-id="57966-178">Run the following command on all VMM hosts:</span><span class="sxs-lookup"><span data-stu-id="57966-178">Run the following command on all VMM hosts:</span></span>

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="57966-179">Step 7: Configure cloud protection settings</span><span class="sxs-lookup"><span data-stu-id="57966-179">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="57966-180">Create a cloud protection profile to Azure by running the following command:</span><span class="sxs-lookup"><span data-stu-id="57966-180">Create a cloud protection profile to Azure by running the following command:</span></span>

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. <span data-ttu-id="57966-181">Get a protection container by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="57966-181">Get a protection container by running the following commands:</span></span>

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. <span data-ttu-id="57966-182">Start the association of the protection container with the cloud:</span><span class="sxs-lookup"><span data-stu-id="57966-182">Start the association of the protection container with the cloud:</span></span>

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. <span data-ttu-id="57966-183">After the job has finished, run the following command:</span><span class="sxs-lookup"><span data-stu-id="57966-183">After the job has finished, run the following command:</span></span>

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. <span data-ttu-id="57966-184">After the job has finished processing, run the following command:</span><span class="sxs-lookup"><span data-stu-id="57966-184">After the job has finished processing, run the following command:</span></span>

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



<span data-ttu-id="57966-185">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span><span class="sxs-lookup"><span data-stu-id="57966-185">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="57966-186">Step 8: Configure network mapping</span><span class="sxs-lookup"><span data-stu-id="57966-186">Step 8: Configure network mapping</span></span>
<span data-ttu-id="57966-187">Before you begin network mapping verify that virtual machines on the source VMM server are connected to a VM network.</span><span class="sxs-lookup"><span data-stu-id="57966-187">Before you begin network mapping verify that virtual machines on the source VMM server are connected to a VM network.</span></span> <span data-ttu-id="57966-188">In addition, create one or more Azure virtual networks.</span><span class="sxs-lookup"><span data-stu-id="57966-188">In addition, create one or more Azure virtual networks.</span></span> <span data-ttu-id="57966-189">Note that multiple VM networks can be mapped to a single Azure network.</span><span class="sxs-lookup"><span data-stu-id="57966-189">Note that multiple VM networks can be mapped to a single Azure network.</span></span>

<span data-ttu-id="57966-190">Note that if the target network has multiple subnets and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after failover.</span><span class="sxs-lookup"><span data-stu-id="57966-190">Note that if the target network has multiple subnets and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after failover.</span></span> <span data-ttu-id="57966-191">If there is not a target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span><span class="sxs-lookup"><span data-stu-id="57966-191">If there is not a target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>

<span data-ttu-id="57966-192">The first command gets servers for the current Azure Site Recovery vault.</span><span class="sxs-lookup"><span data-stu-id="57966-192">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="57966-193">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span><span class="sxs-lookup"><span data-stu-id="57966-193">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

    $Servers = Get-AzureSiteRecoveryServer


<span data-ttu-id="57966-194">The second command gets the site recovery network for the first server in the $Servers array.</span><span class="sxs-lookup"><span data-stu-id="57966-194">The second command gets the site recovery network for the first server in the $Servers array.</span></span> <span data-ttu-id="57966-195">The command stores the networks in the $Networks variable.</span><span class="sxs-lookup"><span data-stu-id="57966-195">The command stores the networks in the $Networks variable.</span></span>

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

<span data-ttu-id="57966-196">The third command gets your Azure subscriptions by using the Get-AzureSubscription cmdlet, and then stores that value in the $Subscriptions variable.</span><span class="sxs-lookup"><span data-stu-id="57966-196">The third command gets your Azure subscriptions by using the Get-AzureSubscription cmdlet, and then stores that value in the $Subscriptions variable.</span></span>

    $Subscriptions = Get-AzureSubscription



<span data-ttu-id="57966-197">The fourth command gets Azure virtual networks by using the Get-AzureVNetSite cmdlet, and then that value in the $AzureVmNetworks variable.</span><span class="sxs-lookup"><span data-stu-id="57966-197">The fourth command gets Azure virtual networks by using the Get-AzureVNetSite cmdlet, and then that value in the $AzureVmNetworks variable.</span></span>

    $AzureVmNetworks = Get-AzureVNetSite



<span data-ttu-id="57966-198">The final cmdlet creates a mapping between the primary network and the Azure virtual machine network.</span><span class="sxs-lookup"><span data-stu-id="57966-198">The final cmdlet creates a mapping between the primary network and the Azure virtual machine network.</span></span> <span data-ttu-id="57966-199">The cmdlet specifies the primary network as the first element of $Networks.</span><span class="sxs-lookup"><span data-stu-id="57966-199">The cmdlet specifies the primary network as the first element of $Networks.</span></span> <span data-ttu-id="57966-200">The cmdlet specifies a virtual machine network as the first element of $AzureVmNetworks by using its ID.</span><span class="sxs-lookup"><span data-stu-id="57966-200">The cmdlet specifies a virtual machine network as the first element of $AzureVmNetworks by using its ID.</span></span> <span data-ttu-id="57966-201">The command includes your Azure subscription ID.</span><span class="sxs-lookup"><span data-stu-id="57966-201">The command includes your Azure subscription ID.</span></span>

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="57966-202">Step 9: Enable protection for virtual machines</span><span class="sxs-lookup"><span data-stu-id="57966-202">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="57966-203">After servers, clouds, and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span><span class="sxs-lookup"><span data-stu-id="57966-203">After servers, clouds, and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span> <span data-ttu-id="57966-204">Note the following:</span><span class="sxs-lookup"><span data-stu-id="57966-204">Note the following:</span></span>

<span data-ttu-id="57966-205">Virtual machines must meet [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="57966-205">Virtual machines must meet [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

<span data-ttu-id="57966-206">To enable protection the operating system and operating system disk properties must be set for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="57966-206">To enable protection the operating system and operating system disk properties must be set for the virtual machine.</span></span> <span data-ttu-id="57966-207">When you create a virtual machine in VMM using a virtual machine template you can set the property.</span><span class="sxs-lookup"><span data-stu-id="57966-207">When you create a virtual machine in VMM using a virtual machine template you can set the property.</span></span> <span data-ttu-id="57966-208">You can also set these properties for existing virtual machines on the **General** and **Hardware Configuration** tabs of the virtual machine properties.</span><span class="sxs-lookup"><span data-stu-id="57966-208">You can also set these properties for existing virtual machines on the **General** and **Hardware Configuration** tabs of the virtual machine properties.</span></span> <span data-ttu-id="57966-209">If you don't set these properties in VMM you'll be able to configure them in the Azure Site Recovery portal.</span><span class="sxs-lookup"><span data-stu-id="57966-209">If you don't set these properties in VMM you'll be able to configure them in the Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="57966-210">To enable protection, run the following command to get the protection container:</span><span class="sxs-lookup"><span data-stu-id="57966-210">To enable protection, run the following command to get the protection container:</span></span>

     <span data-ttu-id="57966-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span><span class="sxs-lookup"><span data-stu-id="57966-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span></span>
2. <span data-ttu-id="57966-212">Get the protection entity (VM) by running the following command:</span><span class="sxs-lookup"><span data-stu-id="57966-212">Get the protection entity (VM) by running the following command:</span></span>

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. <span data-ttu-id="57966-213">Enable the DR for the VM by running the following command:</span><span class="sxs-lookup"><span data-stu-id="57966-213">Enable the DR for the VM by running the following command:</span></span>

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a><span data-ttu-id="57966-214">Test your deployment</span><span class="sxs-lookup"><span data-stu-id="57966-214">Test your deployment</span></span>
<span data-ttu-id="57966-215">To test your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for the plan.</span><span class="sxs-lookup"><span data-stu-id="57966-215">To test your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for the plan.</span></span> <span data-ttu-id="57966-216">Test failover simulates your failover and recovery mechanism in an isolated network.</span><span class="sxs-lookup"><span data-stu-id="57966-216">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="57966-217">Note that:</span><span class="sxs-lookup"><span data-stu-id="57966-217">Note that:</span></span>

* <span data-ttu-id="57966-218">If you want to connect to the virtual machine in Azure using Remote Desktop after the failover, enable Remote Desktop Connection on the virtual machine before you run the test failover.</span><span class="sxs-lookup"><span data-stu-id="57966-218">If you want to connect to the virtual machine in Azure using Remote Desktop after the failover, enable Remote Desktop Connection on the virtual machine before you run the test failover.</span></span>
* <span data-ttu-id="57966-219">After failover, you'll use a public IP address to connect to the virtual machine in Azure using Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="57966-219">After failover, you'll use a public IP address to connect to the virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="57966-220">If you want to do this, ensure you don't have any domain policies that prevent you from connecting to a virtual machine using a public address.</span><span class="sxs-lookup"><span data-stu-id="57966-220">If you want to do this, ensure you don't have any domain policies that prevent you from connecting to a virtual machine using a public address.</span></span>

<span data-ttu-id="57966-221">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span><span class="sxs-lookup"><span data-stu-id="57966-221">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="create-a-recovery-plan"></a><span data-ttu-id="57966-222">Create a recovery plan</span><span class="sxs-lookup"><span data-stu-id="57966-222">Create a recovery plan</span></span>
1. <span data-ttu-id="57966-223">Create an .xml file as a template for your recovery plan using the data below, and then save it as "C:\RPTemplatePath.xml".</span><span class="sxs-lookup"><span data-stu-id="57966-223">Create an .xml file as a template for your recovery plan using the data below, and then save it as "C:\RPTemplatePath.xml".</span></span>
2. <span data-ttu-id="57966-224">Change the RecoveryPlan node Id, Name, PrimaryServerId, and SecondaryServerId.</span><span class="sxs-lookup"><span data-stu-id="57966-224">Change the RecoveryPlan node Id, Name, PrimaryServerId, and SecondaryServerId.</span></span>
3. <span data-ttu-id="57966-225">Change the ProtectionEntity node PrimaryProtectionEntityId (vmid from VMM).</span><span class="sxs-lookup"><span data-stu-id="57966-225">Change the ProtectionEntity node PrimaryProtectionEntityId (vmid from VMM).</span></span>
4. <span data-ttu-id="57966-226">You can add more VMs by adding more ProtectionEntity nodes.</span><span class="sxs-lookup"><span data-stu-id="57966-226">You can add more VMs by adding more ProtectionEntity nodes.</span></span>

        <#
        <?xml version="1.0" encoding="utf-16"?>
        <RecoveryPlan Id="d0323b26-5be2-471b-addc-0a8742796610" Name="rp-test"     PrimaryServerId="9350a530-d5af-435b-9f2b-b941b5d9fcd5"     SecondaryServerId="21a9403c-6ec1-44f2-b744-b4e50b792387" Description=""     Version="V2014_07">
          <Actions />
          <ActionGroups>
            <ShutdownAllActionGroup Id="ShutdownAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </ShutdownAllActionGroup>
            <FailoverAllActionGroup Id="FailoverAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </FailoverAllActionGroup>
            <BootActionGroup Id="DefaultActionGroup">
              <PreActionSequence />
              <PostActionSequence />
              <ProtectionEntity PrimaryProtectionEntityId="d4c8ce92-a613-4c63-9b03-    cf163cc36ef8" />
            </BootActionGroup>
          </ActionGroups>
          <ActionGroupSequence>
            <ActionGroup Id="ShutdownAllActionGroup" ActionId="ShutdownAllActionGroup"     Before="FailoverAllActionGroup" />
            <ActionGroup Id="FailoverAllActionGroup" ActionId="FailoverAllActionGroup"     After="ShutdownAllActionGroup" Before="DefaultActionGroup" />
            <ActionGroup Id="DefaultActionGroup" ActionId="DefaultActionGroup" After="FailoverAllActionGroup"/>
          </ActionGroupSequence>
        </RecoveryPlan>
        #>



1. <span data-ttu-id="57966-227">Fill in the data in the template:</span><span class="sxs-lookup"><span data-stu-id="57966-227">Fill in the data in the template:</span></span>

        $TemplatePath = "C:\RPTemplatePath.xml";



1. <span data-ttu-id="57966-228">Create the RecoveryPlan:</span><span class="sxs-lookup"><span data-stu-id="57966-228">Create the RecoveryPlan:</span></span>

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a><span data-ttu-id="57966-229">Run a test failover</span><span class="sxs-lookup"><span data-stu-id="57966-229">Run a test failover</span></span>
1. <span data-ttu-id="57966-230">Get the RecoveryPlan object by running the following command:</span><span class="sxs-lookup"><span data-stu-id="57966-230">Get the RecoveryPlan object by running the following command:</span></span>

     <span data-ttu-id="57966-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span><span class="sxs-lookup"><span data-stu-id="57966-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span></span>
2. <span data-ttu-id="57966-232">Start the test failover by running the following command:</span><span class="sxs-lookup"><span data-stu-id="57966-232">Start the test failover by running the following command:</span></span>

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <a name=monitor></a> <span data-ttu-id="57966-233">Monitor Activity</span><span class="sxs-lookup"><span data-stu-id="57966-233">Monitor Activity</span></span>
<span data-ttu-id="57966-234">Use the following commands to monitor the activity.</span><span class="sxs-lookup"><span data-stu-id="57966-234">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="57966-235">Note that you have to wait in between jobs for the processing to finish.</span><span class="sxs-lookup"><span data-stu-id="57966-235">Note that you have to wait in between jobs for the processing to finish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="57966-236">Next steps</span><span class="sxs-lookup"><span data-stu-id="57966-236">Next steps</span></span>
<span data-ttu-id="57966-237">[Read more](https://msdn.microsoft.com/library/dn850420.aspx) about Azure Site Recovery PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="57966-237">[Read more](https://msdn.microsoft.com/library/dn850420.aspx) about Azure Site Recovery PowerShell cmdlets.</span></span> <span data-ttu-id="57966-238"></a>.</span><span class="sxs-lookup"><span data-stu-id="57966-238"></a>.</span></span>
