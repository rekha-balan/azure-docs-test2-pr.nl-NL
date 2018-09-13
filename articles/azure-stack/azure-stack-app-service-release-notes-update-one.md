---
title: App Service on Azure Stack update 1 release notes | Microsoft Docs
description: Learn about what's in update one for App Service on Azure Stack, the known issues, and where to download the update.
services: azure-stack
documentationcenter: ''
author: apwestgarth
manager: stefsch
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2018
ms.author: anwestg
ms.reviewer: brenduns
ms.openlocfilehash: 80bd865b7a08d9488c0fb6a1a5b60445b9c6eaaa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870388"
---
# <a name="app-service-on-azure-stack-update-1-release-notes"></a><span data-ttu-id="45172-103">App Service on Azure Stack update 1 release notes</span><span class="sxs-lookup"><span data-stu-id="45172-103">App Service on Azure Stack update 1 release notes</span></span>

<span data-ttu-id="45172-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="45172-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="45172-105">These release notes describe the improvements and fixes in Azure App Service on Azure Stack Update 1 and any known issues.</span><span class="sxs-lookup"><span data-stu-id="45172-105">These release notes describe the improvements and fixes in Azure App Service on Azure Stack Update 1 and any known issues.</span></span> <span data-ttu-id="45172-106">Known issues are divided into issues directly related to the deployment, update process, and issues with the build (post-installation).</span><span class="sxs-lookup"><span data-stu-id="45172-106">Known issues are divided into issues directly related to the deployment, update process, and issues with the build (post-installation).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="45172-107">Apply the 1802 update to your Azure Stack integrated system or deploy the latest Azure Stack development kit before deploying Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="45172-107">Apply the 1802 update to your Azure Stack integrated system or deploy the latest Azure Stack development kit before deploying Azure App Service.</span></span>
>
>

## <a name="build-reference"></a><span data-ttu-id="45172-108">Build reference</span><span class="sxs-lookup"><span data-stu-id="45172-108">Build reference</span></span>

<span data-ttu-id="45172-109">The App Service on Azure Stack Update 1 build number is **69.0.13698.9**</span><span class="sxs-lookup"><span data-stu-id="45172-109">The App Service on Azure Stack Update 1 build number is **69.0.13698.9**</span></span>

### <a name="prerequisites"></a><span data-ttu-id="45172-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="45172-110">Prerequisites</span></span>

> [!IMPORTANT]
> <span data-ttu-id="45172-111">New deployments of Azure App Service on Azure Stack now require a [three-subject wildcard certificate](azure-stack-app-service-before-you-get-started.md#get-certificates) due to improvements in the way in which SSO for Kudu is now handled in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="45172-111">New deployments of Azure App Service on Azure Stack now require a [three-subject wildcard certificate](azure-stack-app-service-before-you-get-started.md#get-certificates) due to improvements in the way in which SSO for Kudu is now handled in Azure App Service.</span></span> <span data-ttu-id="45172-112">The new subject is **\*.sso.appservice.\<region\>.\<domainname\>.\<extension\>**</span><span class="sxs-lookup"><span data-stu-id="45172-112">The new subject is **\*.sso.appservice.\<region\>.\<domainname\>.\<extension\>**</span></span>
>
>

<span data-ttu-id="45172-113">Refer to the [Before You Get Started documentation](azure-stack-app-service-before-you-get-started.md) before beginning deployment.</span><span class="sxs-lookup"><span data-stu-id="45172-113">Refer to the [Before You Get Started documentation](azure-stack-app-service-before-you-get-started.md) before beginning deployment.</span></span>

### <a name="new-features-and-fixes"></a><span data-ttu-id="45172-114">New features and fixes</span><span class="sxs-lookup"><span data-stu-id="45172-114">New features and fixes</span></span>

<span data-ttu-id="45172-115">Azure App Service on Azure Stack Update 1 includes the following improvements and fixes:</span><span class="sxs-lookup"><span data-stu-id="45172-115">Azure App Service on Azure Stack Update 1 includes the following improvements and fixes:</span></span>

- <span data-ttu-id="45172-116">**High Availability of Azure App Service** - The Azure Stack 1802 update enabled workloads to be deployed across fault domains.</span><span class="sxs-lookup"><span data-stu-id="45172-116">**High Availability of Azure App Service** - The Azure Stack 1802 update enabled workloads to be deployed across fault domains.</span></span> <span data-ttu-id="45172-117">Therefore App Service infrastructure is able to be fault tolerant as it will be deployed across fault domains.</span><span class="sxs-lookup"><span data-stu-id="45172-117">Therefore App Service infrastructure is able to be fault tolerant as it will be deployed across fault domains.</span></span> <span data-ttu-id="45172-118">By default all new deployments of Azure App Service has this capability however for deployments completed prior to Azure Stack 1802 update being applied refer to the [App Service Fault Domain documentation](azure-stack-app-service-fault-domain-update.md)</span><span class="sxs-lookup"><span data-stu-id="45172-118">By default all new deployments of Azure App Service has this capability however for deployments completed prior to Azure Stack 1802 update being applied refer to the [App Service Fault Domain documentation](azure-stack-app-service-fault-domain-update.md)</span></span>

- <span data-ttu-id="45172-119">**Deploy in existing virtual network** - Customers can now deploy App Service on Azure Stack within an existing virtual network.</span><span class="sxs-lookup"><span data-stu-id="45172-119">**Deploy in existing virtual network** - Customers can now deploy App Service on Azure Stack within an existing virtual network.</span></span> <span data-ttu-id="45172-120">Deploying in an existing virtual network enables customers to connect to the SQL Server and File Server, required for Azure App Service, over private ports.</span><span class="sxs-lookup"><span data-stu-id="45172-120">Deploying in an existing virtual network enables customers to connect to the SQL Server and File Server, required for Azure App Service, over private ports.</span></span> <span data-ttu-id="45172-121">During deployment, customers can select to deploy in an existing virtual network, however [must create subnets for use by App Service](azure-stack-app-service-before-you-get-started.md#virtual-network) prior to deployment.</span><span class="sxs-lookup"><span data-stu-id="45172-121">During deployment, customers can select to deploy in an existing virtual network, however [must create subnets for use by App Service](azure-stack-app-service-before-you-get-started.md#virtual-network) prior to deployment.</span></span>

- <span data-ttu-id="45172-122">Updates to **App Service Tenant, Admin, Functions portals and Kudu tools**.</span><span class="sxs-lookup"><span data-stu-id="45172-122">Updates to **App Service Tenant, Admin, Functions portals and Kudu tools**.</span></span> <span data-ttu-id="45172-123">Consistent with Azure Stack Portal SDK version.</span><span class="sxs-lookup"><span data-stu-id="45172-123">Consistent with Azure Stack Portal SDK version.</span></span>

- <span data-ttu-id="45172-124">**Updates to the following application frameworks and tools**:</span><span class="sxs-lookup"><span data-stu-id="45172-124">**Updates to the following application frameworks and tools**:</span></span>
    - <span data-ttu-id="45172-125">Added **.Net Core 2.0** support</span><span class="sxs-lookup"><span data-stu-id="45172-125">Added **.Net Core 2.0** support</span></span>
    - <span data-ttu-id="45172-126">Added **Node.JS** versions:</span><span class="sxs-lookup"><span data-stu-id="45172-126">Added **Node.JS** versions:</span></span>
        - <span data-ttu-id="45172-127">6.11.2</span><span class="sxs-lookup"><span data-stu-id="45172-127">6.11.2</span></span>
        - <span data-ttu-id="45172-128">6.11.5</span><span class="sxs-lookup"><span data-stu-id="45172-128">6.11.5</span></span>
        - <span data-ttu-id="45172-129">7.10.1</span><span class="sxs-lookup"><span data-stu-id="45172-129">7.10.1</span></span>
        - <span data-ttu-id="45172-130">8.0.0</span><span class="sxs-lookup"><span data-stu-id="45172-130">8.0.0</span></span>
        - <span data-ttu-id="45172-131">8.1.4</span><span class="sxs-lookup"><span data-stu-id="45172-131">8.1.4</span></span>
        - <span data-ttu-id="45172-132">8.4.0</span><span class="sxs-lookup"><span data-stu-id="45172-132">8.4.0</span></span>
        - <span data-ttu-id="45172-133">8.5.0</span><span class="sxs-lookup"><span data-stu-id="45172-133">8.5.0</span></span>
        - <span data-ttu-id="45172-134">8.7.0</span><span class="sxs-lookup"><span data-stu-id="45172-134">8.7.0</span></span>
        - <span data-ttu-id="45172-135">8.8.1</span><span class="sxs-lookup"><span data-stu-id="45172-135">8.8.1</span></span>
        - <span data-ttu-id="45172-136">8.9.0</span><span class="sxs-lookup"><span data-stu-id="45172-136">8.9.0</span></span>
    - <span data-ttu-id="45172-137">Added **NPM** versions:</span><span class="sxs-lookup"><span data-stu-id="45172-137">Added **NPM** versions:</span></span>
        - <span data-ttu-id="45172-138">3.10.10</span><span class="sxs-lookup"><span data-stu-id="45172-138">3.10.10</span></span>
        - <span data-ttu-id="45172-139">4.2.0</span><span class="sxs-lookup"><span data-stu-id="45172-139">4.2.0</span></span>
        - <span data-ttu-id="45172-140">5.0.0</span><span class="sxs-lookup"><span data-stu-id="45172-140">5.0.0</span></span>
        - <span data-ttu-id="45172-141">5.0.3</span><span class="sxs-lookup"><span data-stu-id="45172-141">5.0.3</span></span>
        - <span data-ttu-id="45172-142">5.3.0</span><span class="sxs-lookup"><span data-stu-id="45172-142">5.3.0</span></span>
        - <span data-ttu-id="45172-143">5.4.2</span><span class="sxs-lookup"><span data-stu-id="45172-143">5.4.2</span></span>
        - <span data-ttu-id="45172-144">5.5.1</span><span class="sxs-lookup"><span data-stu-id="45172-144">5.5.1</span></span>
    - <span data-ttu-id="45172-145">Added **PHP** Updates:</span><span class="sxs-lookup"><span data-stu-id="45172-145">Added **PHP** Updates:</span></span>
        - <span data-ttu-id="45172-146">5.6.32</span><span class="sxs-lookup"><span data-stu-id="45172-146">5.6.32</span></span>
        - <span data-ttu-id="45172-147">7.0.26 (x86 and x64)</span><span class="sxs-lookup"><span data-stu-id="45172-147">7.0.26 (x86 and x64)</span></span>
        - <span data-ttu-id="45172-148">7.1.12 (x86 and x64)</span><span class="sxs-lookup"><span data-stu-id="45172-148">7.1.12 (x86 and x64)</span></span>
    - <span data-ttu-id="45172-149">Updated **Git for Windows** to v 2.14.1</span><span class="sxs-lookup"><span data-stu-id="45172-149">Updated **Git for Windows** to v 2.14.1</span></span>
    - <span data-ttu-id="45172-150">Updated **Mercurial** to v4.5.0</span><span class="sxs-lookup"><span data-stu-id="45172-150">Updated **Mercurial** to v4.5.0</span></span>

  - <span data-ttu-id="45172-151">Added support for **HTTPS Only** feature within Custom Domain feature in the App Service Tenant Portal.</span><span class="sxs-lookup"><span data-stu-id="45172-151">Added support for **HTTPS Only** feature within Custom Domain feature in the App Service Tenant Portal.</span></span> 

  - <span data-ttu-id="45172-152">Added validation of storage connection in the custom storage picker for Azure Functions</span><span class="sxs-lookup"><span data-stu-id="45172-152">Added validation of storage connection in the custom storage picker for Azure Functions</span></span> 

#### <a name="fixes"></a><span data-ttu-id="45172-153">Fixes</span><span class="sxs-lookup"><span data-stu-id="45172-153">Fixes</span></span>

- <span data-ttu-id="45172-154">When creating an offline deployment package, customers will no longer receive an access denied error message when opening the folder from the App Service installer</span><span class="sxs-lookup"><span data-stu-id="45172-154">When creating an offline deployment package, customers will no longer receive an access denied error message when opening the folder from the App Service installer</span></span>

- <span data-ttu-id="45172-155">Resolved issues when working in the Custom Domains feature in the App Service Tenant Portal.</span><span class="sxs-lookup"><span data-stu-id="45172-155">Resolved issues when working in the Custom Domains feature in the App Service Tenant Portal.</span></span>

- <span data-ttu-id="45172-156">Prevent customers using reserved administrator names during setup</span><span class="sxs-lookup"><span data-stu-id="45172-156">Prevent customers using reserved administrator names during setup</span></span>

- <span data-ttu-id="45172-157">Enabled App Service deployment with **domain joined** file server</span><span class="sxs-lookup"><span data-stu-id="45172-157">Enabled App Service deployment with **domain joined** file server</span></span>

- <span data-ttu-id="45172-158">Improved retrieval of Azure Stack root certificate in script and now validate the root cert in the App Service installer.</span><span class="sxs-lookup"><span data-stu-id="45172-158">Improved retrieval of Azure Stack root certificate in script and now validate the root cert in the App Service installer.</span></span>

- <span data-ttu-id="45172-159">Fixed incorrect status being returned to Azure Resource Manager when a subscription is deleted that contained resources in the Microsoft.Web namespace.</span><span class="sxs-lookup"><span data-stu-id="45172-159">Fixed incorrect status being returned to Azure Resource Manager when a subscription is deleted that contained resources in the Microsoft.Web namespace.</span></span>

### <a name="known-issues-with-the-deployment-process"></a><span data-ttu-id="45172-160">Known issues with the deployment process</span><span class="sxs-lookup"><span data-stu-id="45172-160">Known issues with the deployment process</span></span>

- <span data-ttu-id="45172-161">Certificate validation errors</span><span class="sxs-lookup"><span data-stu-id="45172-161">Certificate validation errors</span></span>

<span data-ttu-id="45172-162">Some customers have experienced issues when providing certificates to the App Service installer when deploying on an integrated system, due to overly restrictive validation in the installer.</span><span class="sxs-lookup"><span data-stu-id="45172-162">Some customers have experienced issues when providing certificates to the App Service installer when deploying on an integrated system, due to overly restrictive validation in the installer.</span></span> <span data-ttu-id="45172-163">The App Service installer has been re-released, customers should [download the updated installer](https://aka.ms/appsvconmasinstaller).</span><span class="sxs-lookup"><span data-stu-id="45172-163">The App Service installer has been re-released, customers should [download the updated installer](https://aka.ms/appsvconmasinstaller).</span></span> <span data-ttu-id="45172-164">If you continue to experience issues validating certificates with the updated installer, contact support.</span><span class="sxs-lookup"><span data-stu-id="45172-164">If you continue to experience issues validating certificates with the updated installer, contact support.</span></span>

- <span data-ttu-id="45172-165">Problem retrieving Azure Stack root certificate from integrated system.</span><span class="sxs-lookup"><span data-stu-id="45172-165">Problem retrieving Azure Stack root certificate from integrated system.</span></span>

<span data-ttu-id="45172-166">An error in the Get-AzureStackRootCert.ps1 caused customers to fail to retrieve the Azure Stack root certificate when executing the script on a machine that does not have the root certificate installed.</span><span class="sxs-lookup"><span data-stu-id="45172-166">An error in the Get-AzureStackRootCert.ps1 caused customers to fail to retrieve the Azure Stack root certificate when executing the script on a machine that does not have the root certificate installed.</span></span> <span data-ttu-id="45172-167">The script has also now been re-released, resolving this issue, and request customers [download the updated helper scripts](https://aka.ms/appsvconmashelpers).</span><span class="sxs-lookup"><span data-stu-id="45172-167">The script has also now been re-released, resolving this issue, and request customers [download the updated helper scripts](https://aka.ms/appsvconmashelpers).</span></span> <span data-ttu-id="45172-168">If you continue to experience issues retrieving the root certificate with the updated script, contact support.</span><span class="sxs-lookup"><span data-stu-id="45172-168">If you continue to experience issues retrieving the root certificate with the updated script, contact support.</span></span>

### <a name="known-issues-with-the-update-process"></a><span data-ttu-id="45172-169">Known issues with the update process</span><span class="sxs-lookup"><span data-stu-id="45172-169">Known issues with the update process</span></span>

- <span data-ttu-id="45172-170">There are no known issues for the update of Azure App Service on Azure Stack Update 1.</span><span class="sxs-lookup"><span data-stu-id="45172-170">There are no known issues for the update of Azure App Service on Azure Stack Update 1.</span></span>

### <a name="known-issues-post-installation"></a><span data-ttu-id="45172-171">Known issues (post-installation)</span><span class="sxs-lookup"><span data-stu-id="45172-171">Known issues (post-installation)</span></span>

- <span data-ttu-id="45172-172">Slot Swap does not function</span><span class="sxs-lookup"><span data-stu-id="45172-172">Slot Swap does not function</span></span>

<span data-ttu-id="45172-173">Site slot swap is broken in this release.</span><span class="sxs-lookup"><span data-stu-id="45172-173">Site slot swap is broken in this release.</span></span> <span data-ttu-id="45172-174">To restore functionality, complete these steps:</span><span class="sxs-lookup"><span data-stu-id="45172-174">To restore functionality, complete these steps:</span></span>

1. <span data-ttu-id="45172-175">Modify the ControllersNSG Network Security Group to **Allow** remote desktop connections to the App Service controller instances.</span><span class="sxs-lookup"><span data-stu-id="45172-175">Modify the ControllersNSG Network Security Group to **Allow** remote desktop connections to the App Service controller instances.</span></span> <span data-ttu-id="45172-176">Replace AppService.local with the name of the resource group you deployed App Service in.</span><span class="sxs-lookup"><span data-stu-id="45172-176">Replace AppService.local with the name of the resource group you deployed App Service in.</span></span>

    ```powershell
      Add-AzureRmAccount -EnvironmentName AzureStackAdmin

      $nsg = Get-AzureRmNetworkSecurityGroup -Name "ControllersNsg" -ResourceGroupName "AppService.local"

      $RuleConfig_Inbound_Rdp_3389 =  $nsg | Get-AzureRmNetworkSecurityRuleConfig -Name "Inbound_Rdp_3389"

      Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
        -Name $RuleConfig_Inbound_Rdp_3389.Name `
        -Description "Inbound_Rdp_3389" `
        -Access Allow `
        -Protocol $RuleConfig_Inbound_Rdp_3389.Protocol `
        -Direction $RuleConfig_Inbound_Rdp_3389.Direction `
        -Priority $RuleConfig_Inbound_Rdp_3389.Priority `
        -SourceAddressPrefix $RuleConfig_Inbound_Rdp_3389.SourceAddressPrefix `
        -SourcePortRange $RuleConfig_Inbound_Rdp_3389.SourcePortRange `
        -DestinationAddressPrefix $RuleConfig_Inbound_Rdp_3389.DestinationAddressPrefix `
        -DestinationPortRange $RuleConfig_Inbound_Rdp_3389.DestinationPortRange

      # Commit the changes back to NSG
      Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
      ```

2. <span data-ttu-id="45172-177">Browse to the **CN0-VM** under Virtual Machines in the Azure Stack Administrator portal and **click Connect** to open a remote desktop session with the controller instance.</span><span class="sxs-lookup"><span data-stu-id="45172-177">Browse to the **CN0-VM** under Virtual Machines in the Azure Stack Administrator portal and **click Connect** to open a remote desktop session with the controller instance.</span></span> <span data-ttu-id="45172-178">Use the credentials specified during the deployment of App Service.</span><span class="sxs-lookup"><span data-stu-id="45172-178">Use the credentials specified during the deployment of App Service.</span></span>
3. <span data-ttu-id="45172-179">Start **PowerShell as an Administrator** and execute the following script</span><span class="sxs-lookup"><span data-stu-id="45172-179">Start **PowerShell as an Administrator** and execute the following script</span></span>

    ```powershell
        Import-Module appservice

        $sm = new-object Microsoft.Web.Hosting.SiteManager

        if($sm.HostingConfiguration.SlotsPollWorkerForChangeNotificationStatus=$true)
        {
          $sm.HostingConfiguration.SlotsPollWorkerForChangeNotificationStatus=$false
        #  'Slot swap mode reverted'
        }
        
        # Confirm new setting is false
        $sm.HostingConfiguration.SlotsPollWorkerForChangeNotificationStatus
        
        # Commit Changes
        $sm.CommitChanges()

        Get-AppServiceServer -ServerType ManagementServer | ForEach-Object Repair-AppServiceServer
        
    ```

4. <span data-ttu-id="45172-180">Close the remote desktop session.</span><span class="sxs-lookup"><span data-stu-id="45172-180">Close the remote desktop session.</span></span>
5. <span data-ttu-id="45172-181">Revert the ControllersNSG Network Security Group to **Deny** remote desktop connections to the App Service controller instances.</span><span class="sxs-lookup"><span data-stu-id="45172-181">Revert the ControllersNSG Network Security Group to **Deny** remote desktop connections to the App Service controller instances.</span></span> <span data-ttu-id="45172-182">Replace AppService.local with the name of the resource group you deployed App Service in.</span><span class="sxs-lookup"><span data-stu-id="45172-182">Replace AppService.local with the name of the resource group you deployed App Service in.</span></span>

    ```powershell

        Add-AzureRmAccount -EnvironmentName AzureStackAdmin

        $nsg = Get-AzureRmNetworkSecurityGroup -Name "ControllersNsg" -ResourceGroupName "AppService.local"

        $RuleConfig_Inbound_Rdp_3389 =  $nsg | Get-AzureRmNetworkSecurityRuleConfig -Name "Inbound_Rdp_3389"

        Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
          -Name $RuleConfig_Inbound_Rdp_3389.Name `
          -Description "Inbound_Rdp_3389" `
          -Access Deny `
          -Protocol $RuleConfig_Inbound_Rdp_3389.Protocol `
          -Direction $RuleConfig_Inbound_Rdp_3389.Direction `
          -Priority $RuleConfig_Inbound_Rdp_3389.Priority `
          -SourceAddressPrefix $RuleConfig_Inbound_Rdp_3389.SourceAddressPrefix `
          -SourcePortRange $RuleConfig_Inbound_Rdp_3389.SourcePortRange `
          -DestinationAddressPrefix $RuleConfig_Inbound_Rdp_3389.DestinationAddressPrefix `
          -DestinationPortRange $RuleConfig_Inbound_Rdp_3389.DestinationPortRange

        # Commit the changes back to NSG
        Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
- <span data-ttu-id="45172-183">Workers are unable to reach file server when App Service is deployed in an existing virtual network and the file server is only available on the private network.</span><span class="sxs-lookup"><span data-stu-id="45172-183">Workers are unable to reach file server when App Service is deployed in an existing virtual network and the file server is only available on the private network.</span></span>
 
<span data-ttu-id="45172-184">If you chose to deploy into an existing virtual network and an internal IP address to connect to your file server, you must add an outbound security rule, enabling SMB traffic between the worker subnet and the file server.</span><span class="sxs-lookup"><span data-stu-id="45172-184">If you chose to deploy into an existing virtual network and an internal IP address to connect to your file server, you must add an outbound security rule, enabling SMB traffic between the worker subnet and the file server.</span></span> <span data-ttu-id="45172-185">To do this, go to the WorkersNsg in the Admin Portal and add an outbound security rule with the following properties:</span><span class="sxs-lookup"><span data-stu-id="45172-185">To do this, go to the WorkersNsg in the Admin Portal and add an outbound security rule with the following properties:</span></span>
 * <span data-ttu-id="45172-186">Source: Any</span><span class="sxs-lookup"><span data-stu-id="45172-186">Source: Any</span></span>
 * <span data-ttu-id="45172-187">Source port range: \*</span><span class="sxs-lookup"><span data-stu-id="45172-187">Source port range: \*</span></span>
 * <span data-ttu-id="45172-188">Destination: IP Addresses</span><span class="sxs-lookup"><span data-stu-id="45172-188">Destination: IP Addresses</span></span>
 * <span data-ttu-id="45172-189">Destination IP address range: Range of IPs for your file server</span><span class="sxs-lookup"><span data-stu-id="45172-189">Destination IP address range: Range of IPs for your file server</span></span>
 * <span data-ttu-id="45172-190">Destination port range: 445</span><span class="sxs-lookup"><span data-stu-id="45172-190">Destination port range: 445</span></span>
 * <span data-ttu-id="45172-191">Protocol: TCP</span><span class="sxs-lookup"><span data-stu-id="45172-191">Protocol: TCP</span></span>
 * <span data-ttu-id="45172-192">Action: Allow</span><span class="sxs-lookup"><span data-stu-id="45172-192">Action: Allow</span></span>
 * <span data-ttu-id="45172-193">Priority: 700</span><span class="sxs-lookup"><span data-stu-id="45172-193">Priority: 700</span></span>
 * <span data-ttu-id="45172-194">Name: Outbound_Allow_SMB445</span><span class="sxs-lookup"><span data-stu-id="45172-194">Name: Outbound_Allow_SMB445</span></span>

### <a name="known-issues-for-cloud-admins-operating-azure-app-service-on-azure-stack"></a><span data-ttu-id="45172-195">Known issues for Cloud Admins operating Azure App Service on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="45172-195">Known issues for Cloud Admins operating Azure App Service on Azure Stack</span></span>

<span data-ttu-id="45172-196">Refer to the documentation in the [Azure Stack 1802 Release Notes](azure-stack-update-1802.md)</span><span class="sxs-lookup"><span data-stu-id="45172-196">Refer to the documentation in the [Azure Stack 1802 Release Notes](azure-stack-update-1802.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="45172-197">Next steps</span><span class="sxs-lookup"><span data-stu-id="45172-197">Next steps</span></span>

- <span data-ttu-id="45172-198">For an overview of Azure App Service, see [Azure App Service on Azure Stack overview](azure-stack-app-service-overview.md).</span><span class="sxs-lookup"><span data-stu-id="45172-198">For an overview of Azure App Service, see [Azure App Service on Azure Stack overview](azure-stack-app-service-overview.md).</span></span>
- <span data-ttu-id="45172-199">For more information about how to prepare to deploy App Service on Azure Stack, see [Before you get started with App Service on Azure Stack](azure-stack-app-service-before-you-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="45172-199">For more information about how to prepare to deploy App Service on Azure Stack, see [Before you get started with App Service on Azure Stack](azure-stack-app-service-before-you-get-started.md).</span></span>
