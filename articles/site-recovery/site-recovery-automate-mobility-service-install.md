---
title: Deploy the Site Recovery Mobility service with Azure Automation DSC | Microsoft Docs
description: Describes how to use Azure Automation DSC to automatically deploy the Azure Site Recovery Mobility service and Azure agent for VMware VM and physical server replication to Azure
services: site-recovery
documentationcenter: ''
author: krnese
manager: lorenr
editor: ''
ms.assetid: 1f8cd3ac-0522-48eb-a5f0-679ee9192ddb
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: krnese
ms.openlocfilehash: 697cc8397373d70478f2aad8e10d928ec601a6cb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553085"
---
# <a name="deploy-the-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a><span data-ttu-id="a3149-103">Deploy the Mobility service with Azure Automation DSC for replication of VM</span><span class="sxs-lookup"><span data-stu-id="a3149-103">Deploy the Mobility service with Azure Automation DSC for replication of VM</span></span>
<span data-ttu-id="a3149-104">In Operations Management Suite, we provide you with a comprehensive backup and disaster recovery solution that you can use as part of your business continuity plan.</span><span class="sxs-lookup"><span data-stu-id="a3149-104">In Operations Management Suite, we provide you with a comprehensive backup and disaster recovery solution that you can use as part of your business continuity plan.</span></span>

<span data-ttu-id="a3149-105">We started this journey together with Hyper-V by using Hyper-V Replica.</span><span class="sxs-lookup"><span data-stu-id="a3149-105">We started this journey together with Hyper-V by using Hyper-V Replica.</span></span> <span data-ttu-id="a3149-106">But we have expanded to support a heterogeneous setup because customers have multiple hypervisors and platforms in their clouds.</span><span class="sxs-lookup"><span data-stu-id="a3149-106">But we have expanded to support a heterogeneous setup because customers have multiple hypervisors and platforms in their clouds.</span></span>

<span data-ttu-id="a3149-107">If you are running VMware workloads and/or physical servers today, a management server runs all of the Azure Site Recovery components in your environment to handle the communication and data replication with Azure, when Azure is your destination.</span><span class="sxs-lookup"><span data-stu-id="a3149-107">If you are running VMware workloads and/or physical servers today, a management server runs all of the Azure Site Recovery components in your environment to handle the communication and data replication with Azure, when Azure is your destination.</span></span>

## <a name="deploy-the-site-recovery-mobility-service-by-using-automation-dsc"></a><span data-ttu-id="a3149-108">Deploy the Site Recovery Mobility service by using Automation DSC</span><span class="sxs-lookup"><span data-stu-id="a3149-108">Deploy the Site Recovery Mobility service by using Automation DSC</span></span>
<span data-ttu-id="a3149-109">Let's start by doing a quick breakdown of what this management server does.</span><span class="sxs-lookup"><span data-stu-id="a3149-109">Let's start by doing a quick breakdown of what this management server does.</span></span>

<span data-ttu-id="a3149-110">The management server runs several server roles.</span><span class="sxs-lookup"><span data-stu-id="a3149-110">The management server runs several server roles.</span></span> <span data-ttu-id="a3149-111">One of these roles is *configuration*, which coordinates communication and manages data replication and recovery processes.</span><span class="sxs-lookup"><span data-stu-id="a3149-111">One of these roles is *configuration*, which coordinates communication and manages data replication and recovery processes.</span></span>

<span data-ttu-id="a3149-112">In addition, the *process* role acts as a replication gateway.</span><span class="sxs-lookup"><span data-stu-id="a3149-112">In addition, the *process* role acts as a replication gateway.</span></span> <span data-ttu-id="a3149-113">This role receives replication data from protected source machines, optimizes it with caching, compression, and encryption, and then sends it to an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="a3149-113">This role receives replication data from protected source machines, optimizes it with caching, compression, and encryption, and then sends it to an Azure storage account.</span></span> <span data-ttu-id="a3149-114">One of the functions for the process role is also to push installation of the Mobility service to protected machines and perform automatic discovery of VMware VMs.</span><span class="sxs-lookup"><span data-stu-id="a3149-114">One of the functions for the process role is also to push installation of the Mobility service to protected machines and perform automatic discovery of VMware VMs.</span></span>

<span data-ttu-id="a3149-115">If there's a failback from Azure, the *master target* role will handle the replication data as part of this operation.</span><span class="sxs-lookup"><span data-stu-id="a3149-115">If there's a failback from Azure, the *master target* role will handle the replication data as part of this operation.</span></span>

<span data-ttu-id="a3149-116">For the protected machines, we rely on the *Mobility service*.</span><span class="sxs-lookup"><span data-stu-id="a3149-116">For the protected machines, we rely on the *Mobility service*.</span></span> <span data-ttu-id="a3149-117">This component is deployed to every machine (VMware VM or physical server) that you want to replicate to Azure.</span><span class="sxs-lookup"><span data-stu-id="a3149-117">This component is deployed to every machine (VMware VM or physical server) that you want to replicate to Azure.</span></span> <span data-ttu-id="a3149-118">It captures data writes on the machine and forwards them to the management server (process role).</span><span class="sxs-lookup"><span data-stu-id="a3149-118">It captures data writes on the machine and forwards them to the management server (process role).</span></span>

<span data-ttu-id="a3149-119">When you're dealing with business continuity, it's important to understand your workloads, your infrastructure, and the components involved.</span><span class="sxs-lookup"><span data-stu-id="a3149-119">When you're dealing with business continuity, it's important to understand your workloads, your infrastructure, and the components involved.</span></span> <span data-ttu-id="a3149-120">You can then meet the requirements for your recovery time objective (RTO) and recovery point objective (RPO).</span><span class="sxs-lookup"><span data-stu-id="a3149-120">You can then meet the requirements for your recovery time objective (RTO) and recovery point objective (RPO).</span></span> <span data-ttu-id="a3149-121">In this context, the Mobility service is key to ensuring that your workloads are protected as you would expect.</span><span class="sxs-lookup"><span data-stu-id="a3149-121">In this context, the Mobility service is key to ensuring that your workloads are protected as you would expect.</span></span>

<span data-ttu-id="a3149-122">So how can you, in an optimized way, ensure that you have a reliable protected setup with help from some Operations Management Suite components?</span><span class="sxs-lookup"><span data-stu-id="a3149-122">So how can you, in an optimized way, ensure that you have a reliable protected setup with help from some Operations Management Suite components?</span></span>

<span data-ttu-id="a3149-123">This article provides an example of how you can use Azure Automation Desired State Configuration (DSC), together with Site Recovery, to ensure that:</span><span class="sxs-lookup"><span data-stu-id="a3149-123">This article provides an example of how you can use Azure Automation Desired State Configuration (DSC), together with Site Recovery, to ensure that:</span></span>

* <span data-ttu-id="a3149-124">The Mobility service and Azure VM agent are deployed to the Windows machines that you want to protect.</span><span class="sxs-lookup"><span data-stu-id="a3149-124">The Mobility service and Azure VM agent are deployed to the Windows machines that you want to protect.</span></span>
* <span data-ttu-id="a3149-125">The Mobility service and Azure VM agent are always running when Azure is the replication target.</span><span class="sxs-lookup"><span data-stu-id="a3149-125">The Mobility service and Azure VM agent are always running when Azure is the replication target.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3149-126">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a3149-126">Prerequisites</span></span>
* <span data-ttu-id="a3149-127">A repository to store the required setup</span><span class="sxs-lookup"><span data-stu-id="a3149-127">A repository to store the required setup</span></span>
* <span data-ttu-id="a3149-128">A repository to store the required passphrase to register with the management server</span><span class="sxs-lookup"><span data-stu-id="a3149-128">A repository to store the required passphrase to register with the management server</span></span>

  > [!NOTE]
  > <span data-ttu-id="a3149-129">A unique passphrase is generated for each management server.</span><span class="sxs-lookup"><span data-stu-id="a3149-129">A unique passphrase is generated for each management server.</span></span> <span data-ttu-id="a3149-130">If you are going to deploy multiple management servers, you have to ensure that the correct passphrase is stored in the passphrase.txt file.</span><span class="sxs-lookup"><span data-stu-id="a3149-130">If you are going to deploy multiple management servers, you have to ensure that the correct passphrase is stored in the passphrase.txt file.</span></span>
  >
  >
* <span data-ttu-id="a3149-131">Windows Management Framework (WMF) 5.0 installed on the machines that you want to enable for protection (a requirement for Automation DSC)</span><span class="sxs-lookup"><span data-stu-id="a3149-131">Windows Management Framework (WMF) 5.0 installed on the machines that you want to enable for protection (a requirement for Automation DSC)</span></span>

  > [!NOTE]
  > <span data-ttu-id="a3149-132">If you want to use DSC for Windows machines that have WMF 4.0 installed, see the section [Use DSC in disconnected environments](#Use DSC in disconnected environments).</span><span class="sxs-lookup"><span data-stu-id="a3149-132">If you want to use DSC for Windows machines that have WMF 4.0 installed, see the section [Use DSC in disconnected environments](#Use DSC in disconnected environments).</span></span>
  >
  >

<span data-ttu-id="a3149-133">The Mobility service can be installed through the command line and accepts several arguments.</span><span class="sxs-lookup"><span data-stu-id="a3149-133">The Mobility service can be installed through the command line and accepts several arguments.</span></span> <span data-ttu-id="a3149-134">That’s why you need to have the binaries (after extracting them from your setup) and store them in a place where you can retrieve them by using a DSC configuration.</span><span class="sxs-lookup"><span data-stu-id="a3149-134">That’s why you need to have the binaries (after extracting them from your setup) and store them in a place where you can retrieve them by using a DSC configuration.</span></span>

## <a name="step-1-extract-binaries"></a><span data-ttu-id="a3149-135">Step 1: Extract binaries</span><span class="sxs-lookup"><span data-stu-id="a3149-135">Step 1: Extract binaries</span></span>
1. <span data-ttu-id="a3149-136">To extract the files that you need for this setup, browse to the following directory on your management server:</span><span class="sxs-lookup"><span data-stu-id="a3149-136">To extract the files that you need for this setup, browse to the following directory on your management server:</span></span>

    <span data-ttu-id="a3149-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span><span class="sxs-lookup"><span data-stu-id="a3149-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span></span>

    <span data-ttu-id="a3149-138">In this folder, you should see an MSI file named:</span><span class="sxs-lookup"><span data-stu-id="a3149-138">In this folder, you should see an MSI file named:</span></span>

    <span data-ttu-id="a3149-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span><span class="sxs-lookup"><span data-stu-id="a3149-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span></span>

    <span data-ttu-id="a3149-140">Use the following command to extract the installer:</span><span class="sxs-lookup"><span data-stu-id="a3149-140">Use the following command to extract the installer:</span></span>

    <span data-ttu-id="a3149-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span><span class="sxs-lookup"><span data-stu-id="a3149-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span></span>
2. <span data-ttu-id="a3149-142">Select all files and send them to a compressed (zipped) folder.</span><span class="sxs-lookup"><span data-stu-id="a3149-142">Select all files and send them to a compressed (zipped) folder.</span></span>

<span data-ttu-id="a3149-143">You now have the binaries that you need to automate the setup of the Mobility service by using Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="a3149-143">You now have the binaries that you need to automate the setup of the Mobility service by using Automation DSC.</span></span>

### <a name="passphrase"></a><span data-ttu-id="a3149-144">Passphrase</span><span class="sxs-lookup"><span data-stu-id="a3149-144">Passphrase</span></span>
<span data-ttu-id="a3149-145">Next, you need to determine where you want to place this zipped folder.</span><span class="sxs-lookup"><span data-stu-id="a3149-145">Next, you need to determine where you want to place this zipped folder.</span></span> <span data-ttu-id="a3149-146">You can use an Azure storage account, as shown later, to store the passphrase that you need for the setup.</span><span class="sxs-lookup"><span data-stu-id="a3149-146">You can use an Azure storage account, as shown later, to store the passphrase that you need for the setup.</span></span> <span data-ttu-id="a3149-147">The agent will then register with the management server as part of the process.</span><span class="sxs-lookup"><span data-stu-id="a3149-147">The agent will then register with the management server as part of the process.</span></span>

<span data-ttu-id="a3149-148">The passphrase that you got when you deployed the management server can be saved to a text file as passphrase.txt.</span><span class="sxs-lookup"><span data-stu-id="a3149-148">The passphrase that you got when you deployed the management server can be saved to a text file as passphrase.txt.</span></span>

<span data-ttu-id="a3149-149">Place both the zipped folder and the passphrase in a dedicated container in the Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="a3149-149">Place both the zipped folder and the passphrase in a dedicated container in the Azure storage account.</span></span>

![Folder location](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

<span data-ttu-id="a3149-151">If you prefer to keep these files on a share on your network, you can do so.</span><span class="sxs-lookup"><span data-stu-id="a3149-151">If you prefer to keep these files on a share on your network, you can do so.</span></span> <span data-ttu-id="a3149-152">You just need to ensure that the DSC resource that you will be using later has access and can get the setup and passphrase.</span><span class="sxs-lookup"><span data-stu-id="a3149-152">You just need to ensure that the DSC resource that you will be using later has access and can get the setup and passphrase.</span></span>

## <a name="step-2-create-the-dsc-configuration"></a><span data-ttu-id="a3149-153">Step 2: Create the DSC configuration</span><span class="sxs-lookup"><span data-stu-id="a3149-153">Step 2: Create the DSC configuration</span></span>
<span data-ttu-id="a3149-154">The setup depends on WMF 5.0.</span><span class="sxs-lookup"><span data-stu-id="a3149-154">The setup depends on WMF 5.0.</span></span> <span data-ttu-id="a3149-155">For the machine to successfully apply the configuration through Automation DSC, WMF 5.0 needs to be present.</span><span class="sxs-lookup"><span data-stu-id="a3149-155">For the machine to successfully apply the configuration through Automation DSC, WMF 5.0 needs to be present.</span></span>

<span data-ttu-id="a3149-156">The environment uses the following example DSC configuration:</span><span class="sxs-lookup"><span data-stu-id="a3149-156">The environment uses the following example DSC configuration:</span></span>

```powershell
configuration ASRMobilityService {

    $RemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    $RemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    $RemoteAzureAgent = 'http://go.microsoft.com/fwlink/p/?LinkId=394789'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node localhost {

        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
```
<span data-ttu-id="a3149-157">The configuration will do the following:</span><span class="sxs-lookup"><span data-stu-id="a3149-157">The configuration will do the following:</span></span>

* <span data-ttu-id="a3149-158">The variables will tell the configuration where to get the binaries for the Mobility service and the Azure VM agent, where to get the passphrase, and where to store the output.</span><span class="sxs-lookup"><span data-stu-id="a3149-158">The variables will tell the configuration where to get the binaries for the Mobility service and the Azure VM agent, where to get the passphrase, and where to store the output.</span></span>
* <span data-ttu-id="a3149-159">The configuration will import the xPSDesiredStateConfiguration DSC resource, so that you can use `xRemoteFile` to download the files from the repository.</span><span class="sxs-lookup"><span data-stu-id="a3149-159">The configuration will import the xPSDesiredStateConfiguration DSC resource, so that you can use `xRemoteFile` to download the files from the repository.</span></span>
* <span data-ttu-id="a3149-160">The configuration will create a directory where you want to store the binaries.</span><span class="sxs-lookup"><span data-stu-id="a3149-160">The configuration will create a directory where you want to store the binaries.</span></span>
* <span data-ttu-id="a3149-161">The archive resource will extract the files from the zipped folder.</span><span class="sxs-lookup"><span data-stu-id="a3149-161">The archive resource will extract the files from the zipped folder.</span></span>
* <span data-ttu-id="a3149-162">The package Install resource will install the Mobility service from the UNIFIEDAGENT.EXE installer with the specific arguments.</span><span class="sxs-lookup"><span data-stu-id="a3149-162">The package Install resource will install the Mobility service from the UNIFIEDAGENT.EXE installer with the specific arguments.</span></span> <span data-ttu-id="a3149-163">(The variables that construct the arguments need to be changed to reflect your environment.)</span><span class="sxs-lookup"><span data-stu-id="a3149-163">(The variables that construct the arguments need to be changed to reflect your environment.)</span></span>
* <span data-ttu-id="a3149-164">The package AzureAgent resource will install the Azure VM agent, which is recommended on every VM that runs in Azure.</span><span class="sxs-lookup"><span data-stu-id="a3149-164">The package AzureAgent resource will install the Azure VM agent, which is recommended on every VM that runs in Azure.</span></span> <span data-ttu-id="a3149-165">The Azure VM agent also makes it possible to add extensions to the VM after failover.</span><span class="sxs-lookup"><span data-stu-id="a3149-165">The Azure VM agent also makes it possible to add extensions to the VM after failover.</span></span>
* <span data-ttu-id="a3149-166">The service resource or resources will ensure that the related Mobility services and the Azure services are always running.</span><span class="sxs-lookup"><span data-stu-id="a3149-166">The service resource or resources will ensure that the related Mobility services and the Azure services are always running.</span></span>

<span data-ttu-id="a3149-167">Save the configuration as **ASRMobilityService**.</span><span class="sxs-lookup"><span data-stu-id="a3149-167">Save the configuration as **ASRMobilityService**.</span></span>

> [!NOTE]
> <span data-ttu-id="a3149-168">Remember to replace the CSIP in your configuration to reflect the actual management server, so that the agent will be connected correctly and will use the correct passphrase.</span><span class="sxs-lookup"><span data-stu-id="a3149-168">Remember to replace the CSIP in your configuration to reflect the actual management server, so that the agent will be connected correctly and will use the correct passphrase.</span></span>
>
>

## <a name="step-3-upload-to-automation-dsc"></a><span data-ttu-id="a3149-169">Step 3: Upload to Automation DSC</span><span class="sxs-lookup"><span data-stu-id="a3149-169">Step 3: Upload to Automation DSC</span></span>
<span data-ttu-id="a3149-170">Because the DSC configuration that you made will import a required DSC resource module (xPSDesiredStateConfiguration), you need to import that module in Automation before you upload the DSC configuration.</span><span class="sxs-lookup"><span data-stu-id="a3149-170">Because the DSC configuration that you made will import a required DSC resource module (xPSDesiredStateConfiguration), you need to import that module in Automation before you upload the DSC configuration.</span></span>

<span data-ttu-id="a3149-171">Sign in to your Automation account, browse to **Assets** > **Modules**, and click **Browse Gallery**.</span><span class="sxs-lookup"><span data-stu-id="a3149-171">Sign in to your Automation account, browse to **Assets** > **Modules**, and click **Browse Gallery**.</span></span>

<span data-ttu-id="a3149-172">Here you can search for the module and import it to your account.</span><span class="sxs-lookup"><span data-stu-id="a3149-172">Here you can search for the module and import it to your account.</span></span>

![Import module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

<span data-ttu-id="a3149-174">When you finish this, go to your machine where you have the Azure Resource Manager modules installed and proceed to import the newly created DSC configuration.</span><span class="sxs-lookup"><span data-stu-id="a3149-174">When you finish this, go to your machine where you have the Azure Resource Manager modules installed and proceed to import the newly created DSC configuration.</span></span>

### <a name="import-cmdlets"></a><span data-ttu-id="a3149-175">Import cmdlets</span><span class="sxs-lookup"><span data-stu-id="a3149-175">Import cmdlets</span></span>
<span data-ttu-id="a3149-176">In PowerShell, sign in to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a3149-176">In PowerShell, sign in to your Azure subscription.</span></span> <span data-ttu-id="a3149-177">Modify the cmdlets to reflect your environment and capture your Automation account information in a variable:</span><span class="sxs-lookup"><span data-stu-id="a3149-177">Modify the cmdlets to reflect your environment and capture your Automation account information in a variable:</span></span>

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

<span data-ttu-id="a3149-178">Upload the configuration to Automation DSC by using the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a3149-178">Upload the configuration to Automation DSC by using the following cmdlet:</span></span>

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-the-configuration-in-automation-dsc"></a><span data-ttu-id="a3149-179">Compile the configuration in Automation DSC</span><span class="sxs-lookup"><span data-stu-id="a3149-179">Compile the configuration in Automation DSC</span></span>
<span data-ttu-id="a3149-180">Next, you need to compile the configuration in Automation DSC, so that you can start to register nodes to it.</span><span class="sxs-lookup"><span data-stu-id="a3149-180">Next, you need to compile the configuration in Automation DSC, so that you can start to register nodes to it.</span></span> <span data-ttu-id="a3149-181">You achieve that by running the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a3149-181">You achieve that by running the following cmdlet:</span></span>

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

<span data-ttu-id="a3149-182">This can take a few minutes, because you're basically deploying the configuration to the hosted DSC pull service.</span><span class="sxs-lookup"><span data-stu-id="a3149-182">This can take a few minutes, because you're basically deploying the configuration to the hosted DSC pull service.</span></span>

<span data-ttu-id="a3149-183">After you compile the configuration, you can retrieve the job information by using PowerShell (Get-AzureRmAutomationDscCompilationJob) or by using the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a3149-183">After you compile the configuration, you can retrieve the job information by using PowerShell (Get-AzureRmAutomationDscCompilationJob) or by using the [Azure portal](https://portal.azure.com/).</span></span>

![Retrieve job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

<span data-ttu-id="a3149-185">You have now successfully published and uploaded your DSC configuration to Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="a3149-185">You have now successfully published and uploaded your DSC configuration to Automation DSC.</span></span>

## <a name="step-4-onboard-machines-to-automation-dsc"></a><span data-ttu-id="a3149-186">Step 4: Onboard machines to Automation DSC</span><span class="sxs-lookup"><span data-stu-id="a3149-186">Step 4: Onboard machines to Automation DSC</span></span>
> [!NOTE]
> <span data-ttu-id="a3149-187">One of the prerequisites for completing this scenario is that your Windows machines are updated with the latest version of WMF.</span><span class="sxs-lookup"><span data-stu-id="a3149-187">One of the prerequisites for completing this scenario is that your Windows machines are updated with the latest version of WMF.</span></span> <span data-ttu-id="a3149-188">You can download and install the correct version for your platform from the [Download Center](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="a3149-188">You can download and install the correct version for your platform from the [Download Center](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>
>
>

<span data-ttu-id="a3149-189">You will now create a metaconfig for DSC that you will apply to your nodes.</span><span class="sxs-lookup"><span data-stu-id="a3149-189">You will now create a metaconfig for DSC that you will apply to your nodes.</span></span> <span data-ttu-id="a3149-190">To succeed with this, you need to retrieve the endpoint URL and the primary key for your selected Automation account in Azure.</span><span class="sxs-lookup"><span data-stu-id="a3149-190">To succeed with this, you need to retrieve the endpoint URL and the primary key for your selected Automation account in Azure.</span></span> <span data-ttu-id="a3149-191">You can find these values under **Keys** on the **All settings** blade for the Automation account.</span><span class="sxs-lookup"><span data-stu-id="a3149-191">You can find these values under **Keys** on the **All settings** blade for the Automation account.</span></span>

![Key values](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-automate-mobilitysevice-install/key-values.png)

<span data-ttu-id="a3149-193">In this example, you have a Windows Server 2012 R2 physical server that you want to protect by using Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a3149-193">In this example, you have a Windows Server 2012 R2 physical server that you want to protect by using Site Recovery.</span></span>

### <a name="check-for-any-pending-file-rename-operations-in-the-registry"></a><span data-ttu-id="a3149-194">Check for any pending file rename operations in the registry</span><span class="sxs-lookup"><span data-stu-id="a3149-194">Check for any pending file rename operations in the registry</span></span>
<span data-ttu-id="a3149-195">Before you start to associate the server with the Automation DSC endpoint, we recommend that you check for any pending file rename operations in the registry.</span><span class="sxs-lookup"><span data-stu-id="a3149-195">Before you start to associate the server with the Automation DSC endpoint, we recommend that you check for any pending file rename operations in the registry.</span></span> <span data-ttu-id="a3149-196">They might prohibit the setup from finishing due to a pending reboot.</span><span class="sxs-lookup"><span data-stu-id="a3149-196">They might prohibit the setup from finishing due to a pending reboot.</span></span>

<span data-ttu-id="a3149-197">Run the following cmdlet to verify that there’s no pending reboot on the server:</span><span class="sxs-lookup"><span data-stu-id="a3149-197">Run the following cmdlet to verify that there’s no pending reboot on the server:</span></span>

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
<span data-ttu-id="a3149-198">If this shows empty, you are OK to proceed.</span><span class="sxs-lookup"><span data-stu-id="a3149-198">If this shows empty, you are OK to proceed.</span></span> <span data-ttu-id="a3149-199">If not, you should address this by rebooting the server during a maintenance window.</span><span class="sxs-lookup"><span data-stu-id="a3149-199">If not, you should address this by rebooting the server during a maintenance window.</span></span>

<span data-ttu-id="a3149-200">To apply the configuration on the server, start the PowerShell Integrated Scripting Environment (ISE) and run the following script.</span><span class="sxs-lookup"><span data-stu-id="a3149-200">To apply the configuration on the server, start the PowerShell Integrated Scripting Environment (ISE) and run the following script.</span></span> <span data-ttu-id="a3149-201">This is essentially a DSC local configuration that will instruct the Local Configuration Manager engine to register with the Automation DSC service and retrieve the specific configuration (ASRMobilityService.localhost).</span><span class="sxs-lookup"><span data-stu-id="a3149-201">This is essentially a DSC local configuration that will instruct the Local Configuration Manager engine to register with the Automation DSC service and retrieve the specific configuration (ASRMobilityService.localhost).</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration metaconfig {
    param (
        $URL,
        $Key
    )
    node localhost {
        Settings {
            RefreshFrequencyMins = '30'
            RebootNodeIfNeeded = $true
            RefreshMode = 'PULL'
            ActionAfterReboot = 'ContinueConfiguration'
            ConfigurationMode = 'ApplyAndMonitor'
            AllowModuleOverwrite = $true
        }

        ResourceRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }

        ConfigurationRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
            ConfigurationNames = 'ASRMobilityService.localhost'
        }

        ReportServerWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }
    }
}
metaconfig -URL 'https://we-agentservice-prod-1.azure-automation.net/accounts/<YOURAAAccountID>' -Key '<YOURAAAccountKey>'

Set-DscLocalConfigurationManager .\metaconfig -Force -Verbose
```

<span data-ttu-id="a3149-202">This configuration will cause the Local Configuration Manager engine to register itself with Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="a3149-202">This configuration will cause the Local Configuration Manager engine to register itself with Automation DSC.</span></span> <span data-ttu-id="a3149-203">It will also determine how the engine should operate, what it should do if there's a configuration drift (ApplyAndAutoCorrect), and how it should proceed with the configuration if a reboot is required.</span><span class="sxs-lookup"><span data-stu-id="a3149-203">It will also determine how the engine should operate, what it should do if there's a configuration drift (ApplyAndAutoCorrect), and how it should proceed with the configuration if a reboot is required.</span></span>

<span data-ttu-id="a3149-204">After you run this script, the node should start to register with Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="a3149-204">After you run this script, the node should start to register with Automation DSC.</span></span>

![Node registration in progress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-automate-mobilitysevice-install/register-node.png)

<span data-ttu-id="a3149-206">If you go back to the Azure portal, you can see that the newly registered node has now appeared in the portal.</span><span class="sxs-lookup"><span data-stu-id="a3149-206">If you go back to the Azure portal, you can see that the newly registered node has now appeared in the portal.</span></span>

![Registered node in the portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-automate-mobilitysevice-install/registered-node.png)

<span data-ttu-id="a3149-208">On the server, you can run the following PowerShell cmdlet to verify that the node has been registered correctly:</span><span class="sxs-lookup"><span data-stu-id="a3149-208">On the server, you can run the following PowerShell cmdlet to verify that the node has been registered correctly:</span></span>

```powershell
Get-DscLocalConfigurationManager
```

<span data-ttu-id="a3149-209">After the configuration has been pulled and applied to the server, you can verify this by running the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a3149-209">After the configuration has been pulled and applied to the server, you can verify this by running the following cmdlet:</span></span>

```powershell
Get-DscConfigurationStatus
```

<span data-ttu-id="a3149-210">The output shows that the server has successfully pulled its configuration:</span><span class="sxs-lookup"><span data-stu-id="a3149-210">The output shows that the server has successfully pulled its configuration:</span></span>

![Output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-automate-mobilitysevice-install/successful-config.png)

<span data-ttu-id="a3149-212">In addition, the Mobility service setup has its own log that can be found at *SystemDrive*\ProgramData\ASRSetupLogs.</span><span class="sxs-lookup"><span data-stu-id="a3149-212">In addition, the Mobility service setup has its own log that can be found at *SystemDrive*\ProgramData\ASRSetupLogs.</span></span>

<span data-ttu-id="a3149-213">That’s it.</span><span class="sxs-lookup"><span data-stu-id="a3149-213">That’s it.</span></span> <span data-ttu-id="a3149-214">You have now successfully deployed and registered the Mobility service on the machine that you want to protect by using Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a3149-214">You have now successfully deployed and registered the Mobility service on the machine that you want to protect by using Site Recovery.</span></span> <span data-ttu-id="a3149-215">DSC will make sure that the required services are always running.</span><span class="sxs-lookup"><span data-stu-id="a3149-215">DSC will make sure that the required services are always running.</span></span>

![Successful deployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-automate-mobilitysevice-install/successful-install.png)

<span data-ttu-id="a3149-217">After the management server detects the successful deployment, you can configure protection and enable replication on the machine by using Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a3149-217">After the management server detects the successful deployment, you can configure protection and enable replication on the machine by using Site Recovery.</span></span>

## <a name="use-dsc-in-disconnected-environments"></a><span data-ttu-id="a3149-218">Use DSC in disconnected environments</span><span class="sxs-lookup"><span data-stu-id="a3149-218">Use DSC in disconnected environments</span></span>
<span data-ttu-id="a3149-219">If your machines aren’t connected to the Internet, you can still rely on DSC to deploy and configure the Mobility service on the workloads that you want to protect.</span><span class="sxs-lookup"><span data-stu-id="a3149-219">If your machines aren’t connected to the Internet, you can still rely on DSC to deploy and configure the Mobility service on the workloads that you want to protect.</span></span>

<span data-ttu-id="a3149-220">You can instantiate your own DSC pull server in your environment to essentially provide the same capabilities that you get from Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="a3149-220">You can instantiate your own DSC pull server in your environment to essentially provide the same capabilities that you get from Automation DSC.</span></span> <span data-ttu-id="a3149-221">That is, the clients will pull the configuration (after it's registered) to the DSC endpoint.</span><span class="sxs-lookup"><span data-stu-id="a3149-221">That is, the clients will pull the configuration (after it's registered) to the DSC endpoint.</span></span> <span data-ttu-id="a3149-222">However, another option is to manually push the DSC configuration to your machines, either locally or remotely.</span><span class="sxs-lookup"><span data-stu-id="a3149-222">However, another option is to manually push the DSC configuration to your machines, either locally or remotely.</span></span>

<span data-ttu-id="a3149-223">Note that in this example, there's an added parameter for the computer name.</span><span class="sxs-lookup"><span data-stu-id="a3149-223">Note that in this example, there's an added parameter for the computer name.</span></span> <span data-ttu-id="a3149-224">The remote files are now located on a remote share that should be accessible by the machines that you want to protect.</span><span class="sxs-lookup"><span data-stu-id="a3149-224">The remote files are now located on a remote share that should be accessible by the machines that you want to protect.</span></span> <span data-ttu-id="a3149-225">The end of the script enacts the configuration and then starts to apply the DSC configuration to the target computer.</span><span class="sxs-lookup"><span data-stu-id="a3149-225">The end of the script enacts the configuration and then starts to apply the DSC configuration to the target computer.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="a3149-226">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a3149-226">Prerequisites</span></span>
<span data-ttu-id="a3149-227">Make sure that the xPSDesiredStateConfiguration PowerShell module is installed.</span><span class="sxs-lookup"><span data-stu-id="a3149-227">Make sure that the xPSDesiredStateConfiguration PowerShell module is installed.</span></span> <span data-ttu-id="a3149-228">For Windows machines where WMF 5.0 is installed, you can install the xPSDesiredStateConfiguration module by running the following cmdlet on the target machines:</span><span class="sxs-lookup"><span data-stu-id="a3149-228">For Windows machines where WMF 5.0 is installed, you can install the xPSDesiredStateConfiguration module by running the following cmdlet on the target machines:</span></span>

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

<span data-ttu-id="a3149-229">You can also download and save the module in case you need to distribute it to Windows machines that have WMF 4.0.</span><span class="sxs-lookup"><span data-stu-id="a3149-229">You can also download and save the module in case you need to distribute it to Windows machines that have WMF 4.0.</span></span> <span data-ttu-id="a3149-230">Run this cmdlet on a machine where PowerShellGet (WMF 5.0) is present:</span><span class="sxs-lookup"><span data-stu-id="a3149-230">Run this cmdlet on a machine where PowerShellGet (WMF 5.0) is present:</span></span>

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

<span data-ttu-id="a3149-231">Also for WMF 4.0, ensure that the [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) is installed on the machines.</span><span class="sxs-lookup"><span data-stu-id="a3149-231">Also for WMF 4.0, ensure that the [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) is installed on the machines.</span></span>

<span data-ttu-id="a3149-232">The following configuration can be pushed to Windows machines that have WMF 5.0 and WMF 4.0:</span><span class="sxs-lookup"><span data-stu-id="a3149-232">The following configuration can be pushed to Windows machines that have WMF 5.0 and WMF 4.0:</span></span>

```powershell
configuration ASRMobilityService {
    param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        [System.String] $ComputerName
    )

    $RemoteFile = '\\myfileserver\share\asr.zip'
    $RemotePassphrase = '\\myfileserver\share\passphrase.txt'
    $RemoteAzureAgent = '\\myfileserver\share\AzureVmAgent.msi'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node $ComputerName {      
        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
ASRMobilityService -ComputerName 'MyTargetComputerName'

Start-DscConfiguration .\ASRMobilityService -Wait -Force -Verbose
```

<span data-ttu-id="a3149-233">If you want to instantiate your own DSC pull server on your corporate network to mimic the capabilities that you can get from Automation DSC, see [Setting up a DSC web pull server](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="a3149-233">If you want to instantiate your own DSC pull server on your corporate network to mimic the capabilities that you can get from Automation DSC, see [Setting up a DSC web pull server](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span></span>

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="a3149-234">Optional: Deploy a DSC configuration by using an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="a3149-234">Optional: Deploy a DSC configuration by using an Azure Resource Manager template</span></span>
<span data-ttu-id="a3149-235">This article has focused on how you can create your own DSC configuration to automatically deploy the Mobility service and the Azure VM Agent--and ensure that they are running on the machines that you want to protect.</span><span class="sxs-lookup"><span data-stu-id="a3149-235">This article has focused on how you can create your own DSC configuration to automatically deploy the Mobility service and the Azure VM Agent--and ensure that they are running on the machines that you want to protect.</span></span> <span data-ttu-id="a3149-236">We also have an Azure Resource Manager template that will deploy this DSC configuration to a new or existing Azure Automation account.</span><span class="sxs-lookup"><span data-stu-id="a3149-236">We also have an Azure Resource Manager template that will deploy this DSC configuration to a new or existing Azure Automation account.</span></span> <span data-ttu-id="a3149-237">The template will use input parameters to create Automation assets that will contain the variables for your environment.</span><span class="sxs-lookup"><span data-stu-id="a3149-237">The template will use input parameters to create Automation assets that will contain the variables for your environment.</span></span>

<span data-ttu-id="a3149-238">After you deploy the template, you can simply refer to step 4 in this guide to onboard your machines.</span><span class="sxs-lookup"><span data-stu-id="a3149-238">After you deploy the template, you can simply refer to step 4 in this guide to onboard your machines.</span></span>

<span data-ttu-id="a3149-239">The template will do the following:</span><span class="sxs-lookup"><span data-stu-id="a3149-239">The template will do the following:</span></span>

1. <span data-ttu-id="a3149-240">Use an existing Automation account or create a new one</span><span class="sxs-lookup"><span data-stu-id="a3149-240">Use an existing Automation account or create a new one</span></span>
2. <span data-ttu-id="a3149-241">Take input parameters for:</span><span class="sxs-lookup"><span data-stu-id="a3149-241">Take input parameters for:</span></span>
   * <span data-ttu-id="a3149-242">ASRRemoteFile--the location where you have stored the Mobility service setup</span><span class="sxs-lookup"><span data-stu-id="a3149-242">ASRRemoteFile--the location where you have stored the Mobility service setup</span></span>
   * <span data-ttu-id="a3149-243">ASRPassphrase--the location where you have stored the passphrase.txt file</span><span class="sxs-lookup"><span data-stu-id="a3149-243">ASRPassphrase--the location where you have stored the passphrase.txt file</span></span>
   * <span data-ttu-id="a3149-244">ASRCSEndpoint--the IP address of your management server</span><span class="sxs-lookup"><span data-stu-id="a3149-244">ASRCSEndpoint--the IP address of your management server</span></span>
3. <span data-ttu-id="a3149-245">Import the xPSDesiredStateConfiguration PowerShell module</span><span class="sxs-lookup"><span data-stu-id="a3149-245">Import the xPSDesiredStateConfiguration PowerShell module</span></span>
4. <span data-ttu-id="a3149-246">Create and compile the DSC configuration</span><span class="sxs-lookup"><span data-stu-id="a3149-246">Create and compile the DSC configuration</span></span>

<span data-ttu-id="a3149-247">All the preceding steps will happen in the right order, so that you can start onboarding your machines for protection.</span><span class="sxs-lookup"><span data-stu-id="a3149-247">All the preceding steps will happen in the right order, so that you can start onboarding your machines for protection.</span></span>

<span data-ttu-id="a3149-248">The template, with instructions for deployment, is located on [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span><span class="sxs-lookup"><span data-stu-id="a3149-248">The template, with instructions for deployment, is located on [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span></span>

<span data-ttu-id="a3149-249">Deploy the template by using PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a3149-249">Deploy the template by using PowerShell:</span></span>

```powershell
$RGDeployArgs = @{
    Name = 'DSC3'
    ResourceGroupName = 'KNOMS'
    TemplateFile = 'https://raw.githubusercontent.com/krnese/AzureDeploy/master/OMS/MSOMS/DSC/azuredeploy.json'
    OMSAutomationAccountName = 'KNOMSAA'
    ASRRemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    ASRRemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    ASRCSEndpoint = '10.0.0.115'
    DSCJobGuid = [System.Guid]::NewGuid().ToString()
}
New-AzureRmResourceGroupDeployment @RGDeployArgs -Verbose
```

## <a name="next-steps"></a><span data-ttu-id="a3149-250">Next steps</span><span class="sxs-lookup"><span data-stu-id="a3149-250">Next steps</span></span>
<span data-ttu-id="a3149-251">After you deploy the Mobility service agents, you can [enable replication](site-recovery-vmware-to-azure.md#enable-replication) for the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="a3149-251">After you deploy the Mobility service agents, you can [enable replication](site-recovery-vmware-to-azure.md#enable-replication) for the virtual machines.</span></span>








