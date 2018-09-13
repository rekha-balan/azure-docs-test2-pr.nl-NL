---
title: Redeploy the Azure Stack Development Kit (ASDK) | Microsoft Docs
description: In this article, you learn how to reinstall the ASDK.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: ''
ms.date: 08/01/2018
ms.author: jeffgilb
ms.reviewer: misainat
ms.openlocfilehash: d166916ca54f3b8c26a418ff83093e53dcdbe515
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868151"
---
# <a name="redeploy-the-asdk"></a><span data-ttu-id="be129-103">Redeploy the ASDK</span><span class="sxs-lookup"><span data-stu-id="be129-103">Redeploy the ASDK</span></span>
<span data-ttu-id="be129-104">In this article, you learn how to redeploy the Azure Stack Development Kit (ASDK) in a non-production environment.</span><span class="sxs-lookup"><span data-stu-id="be129-104">In this article, you learn how to redeploy the Azure Stack Development Kit (ASDK) in a non-production environment.</span></span> <span data-ttu-id="be129-105">Because upgrading the ASDK isn't supported, you need to completely redeploy it to move to a newer version.</span><span class="sxs-lookup"><span data-stu-id="be129-105">Because upgrading the ASDK isn't supported, you need to completely redeploy it to move to a newer version.</span></span> <span data-ttu-id="be129-106">You can also redeploy the ASDK at any time that you just want to start over from scratch.</span><span class="sxs-lookup"><span data-stu-id="be129-106">You can also redeploy the ASDK at any time that you just want to start over from scratch.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="be129-107">Upgrading the ASDK to a new version isn't supported.</span><span class="sxs-lookup"><span data-stu-id="be129-107">Upgrading the ASDK to a new version isn't supported.</span></span> <span data-ttu-id="be129-108">You have to redeploy the ASDK on the development kit host computer each time you want to evaluate a newer version of Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="be129-108">You have to redeploy the ASDK on the development kit host computer each time you want to evaluate a newer version of Azure Stack.</span></span>

## <a name="remove-azure-registration"></a><span data-ttu-id="be129-109">Remove Azure registration</span><span class="sxs-lookup"><span data-stu-id="be129-109">Remove Azure registration</span></span> 
<span data-ttu-id="be129-110">If you have previously registered your ASDK installation with Azure, you should remove the registration resource before redeploying the ASDK.</span><span class="sxs-lookup"><span data-stu-id="be129-110">If you have previously registered your ASDK installation with Azure, you should remove the registration resource before redeploying the ASDK.</span></span> <span data-ttu-id="be129-111">Re-register the ASDK to enable the availability of items in the marketplace when you redeploy the ASDK.</span><span class="sxs-lookup"><span data-stu-id="be129-111">Re-register the ASDK to enable the availability of items in the marketplace when you redeploy the ASDK.</span></span> <span data-ttu-id="be129-112">If you have not previously registered the ASDK with your Azure subscription, you can skip this section.</span><span class="sxs-lookup"><span data-stu-id="be129-112">If you have not previously registered the ASDK with your Azure subscription, you can skip this section.</span></span>

<span data-ttu-id="be129-113">To remove the registration resource, use the **Remove-AzsRegistration** cmdlet to unregister Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="be129-113">To remove the registration resource, use the **Remove-AzsRegistration** cmdlet to unregister Azure Stack.</span></span> <span data-ttu-id="be129-114">Then, use the **Remove-AzureRMRsourceGroup** cmdlet to delete the Azure Stack resource group from your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="be129-114">Then, use the **Remove-AzureRMRsourceGroup** cmdlet to delete the Azure Stack resource group from your Azure subscription:</span></span>

1. <span data-ttu-id="be129-115">Open a PowerShell console as an administrator on a computer that has access to the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="be129-115">Open a PowerShell console as an administrator on a computer that has access to the privileged endpoint.</span></span> <span data-ttu-id="be129-116">For the ASDK, that's the development kit host computer.</span><span class="sxs-lookup"><span data-stu-id="be129-116">For the ASDK, that's the development kit host computer.</span></span>

2. <span data-ttu-id="be129-117">Run the following PowerShell commands to unregister your ASDK installation and delete the **azurestack** resource group from your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="be129-117">Run the following PowerShell commands to unregister your ASDK installation and delete the **azurestack** resource group from your Azure subscription:</span></span>

  ```Powershell    
  #Import the registration module that was downloaded with the GitHub tools
  Import-Module C:\AzureStack-Tools-master\Registration\RegisterWithAzure.psm1

  # Provide Azure subscription admin credentials
  Add-AzureRmAccount

  # Provide ASDK admin credentials
  $CloudAdminCred = Get-Credential -UserName AZURESTACK\CloudAdmin -Message "Enter the cloud domain credentials to access the privileged endpoint"

  # Unregister Azure Stack
  Remove-AzsRegistration `
      -PrivilegedEndpointCredential $CloudAdminCred `
      -PrivilegedEndpoint AzS-ERCS01

  # Remove the Azure Stack resource group
  Remove-AzureRmResourceGroup -Name azurestack -Force
  ```

3. <span data-ttu-id="be129-118">You are prompted to sign in to both your Azure subscription and the local ASDK installation when the script runs.</span><span class="sxs-lookup"><span data-stu-id="be129-118">You are prompted to sign in to both your Azure subscription and the local ASDK installation when the script runs.</span></span>
4. <span data-ttu-id="be129-119">When the script completes, you should see messages similar to the following examples:</span><span class="sxs-lookup"><span data-stu-id="be129-119">When the script completes, you should see messages similar to the following examples:</span></span>

    <span data-ttu-id="be129-120">` De-Activating Azure Stack (this may take up to 10 minutes to complete).` ` Your environment is now unable to syndicate items and is no longer reporting usage data.`</span><span class="sxs-lookup"><span data-stu-id="be129-120">` De-Activating Azure Stack (this may take up to 10 minutes to complete).` ` Your environment is now unable to syndicate items and is no longer reporting usage data.`</span></span>
    ` Remove registration resource from Azure...`
    ` "Deleting the resource..." on target "/subscriptions/<subscription information>"`
    ` ********** End Log: Remove-AzsRegistration ********* `



<span data-ttu-id="be129-121">Azure Stack should now successfully be unregistered from your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="be129-121">Azure Stack should now successfully be unregistered from your Azure subscription.</span></span> <span data-ttu-id="be129-122">Additionally, the azurestack resource group, created when you registered the ASDK with Azure, should also be deleted.</span><span class="sxs-lookup"><span data-stu-id="be129-122">Additionally, the azurestack resource group, created when you registered the ASDK with Azure, should also be deleted.</span></span>

## <a name="deploy-the-asdk"></a><span data-ttu-id="be129-123">Deploy the ASDK</span><span class="sxs-lookup"><span data-stu-id="be129-123">Deploy the ASDK</span></span>
<span data-ttu-id="be129-124">To redeploy Azure Stack, you must start over from scratch as described below.</span><span class="sxs-lookup"><span data-stu-id="be129-124">To redeploy Azure Stack, you must start over from scratch as described below.</span></span> <span data-ttu-id="be129-125">The steps are different depending on whether or not you used the Azure Stack installer (asdk-installer.ps1) script to install the ASDK.</span><span class="sxs-lookup"><span data-stu-id="be129-125">The steps are different depending on whether or not you used the Azure Stack installer (asdk-installer.ps1) script to install the ASDK.</span></span>

### <a name="redeploy-the-asdk-using-the-installer-script"></a><span data-ttu-id="be129-126">Redeploy the ASDK using the installer script</span><span class="sxs-lookup"><span data-stu-id="be129-126">Redeploy the ASDK using the installer script</span></span>
1. <span data-ttu-id="be129-127">On the ASDK computer, open an elevated PowerShell console and navigate to the asdk-installer.ps1 script in the **AzureStack_Installer** directory located on a non-system drive.</span><span class="sxs-lookup"><span data-stu-id="be129-127">On the ASDK computer, open an elevated PowerShell console and navigate to the asdk-installer.ps1 script in the **AzureStack_Installer** directory located on a non-system drive.</span></span> <span data-ttu-id="be129-128">Run the script and click **Reboot**.</span><span class="sxs-lookup"><span data-stu-id="be129-128">Run the script and click **Reboot**.</span></span>

   ![Run the asdk-installer.ps1 script](media/asdk-redeploy/1.png)

2. <span data-ttu-id="be129-130">Select the base operating system (not **Azure Stack**) and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="be129-130">Select the base operating system (not **Azure Stack**) and click **Next**.</span></span>

   ![Restart into the host operating system](media/asdk-redeploy/2.png)

3. <span data-ttu-id="be129-132">After the development kit host reboots into the base operating system, log in as a local administrator.</span><span class="sxs-lookup"><span data-stu-id="be129-132">After the development kit host reboots into the base operating system, log in as a local administrator.</span></span> <span data-ttu-id="be129-133">Locate and delete the **C:\CloudBuilder.vhdx** file that was used as part of the previous deployment.</span><span class="sxs-lookup"><span data-stu-id="be129-133">Locate and delete the **C:\CloudBuilder.vhdx** file that was used as part of the previous deployment.</span></span> 

4. <span data-ttu-id="be129-134">Repeat the same steps that you took to first [deploy the ASDK](asdk-install.md).</span><span class="sxs-lookup"><span data-stu-id="be129-134">Repeat the same steps that you took to first [deploy the ASDK](asdk-install.md).</span></span>

### <a name="redeploy-the-asdk-without-using-the-installer"></a><span data-ttu-id="be129-135">Redeploy the ASDK without using the installer</span><span class="sxs-lookup"><span data-stu-id="be129-135">Redeploy the ASDK without using the installer</span></span>
<span data-ttu-id="be129-136">If you did not use the asdk-installer.ps1 script to install the ASDK, you must manually reconfigure the development kit host computer before redeploying the ASDK.</span><span class="sxs-lookup"><span data-stu-id="be129-136">If you did not use the asdk-installer.ps1 script to install the ASDK, you must manually reconfigure the development kit host computer before redeploying the ASDK.</span></span>

1. <span data-ttu-id="be129-137">Start the System Configuration utility by running **msconfig.exe** on the ASDK computer.</span><span class="sxs-lookup"><span data-stu-id="be129-137">Start the System Configuration utility by running **msconfig.exe** on the ASDK computer.</span></span> <span data-ttu-id="be129-138">On the **Boot** tab, select the host computer operating system (not Azure Stack), click **Set as default**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="be129-138">On the **Boot** tab, select the host computer operating system (not Azure Stack), click **Set as default**, and then click **OK**.</span></span> <span data-ttu-id="be129-139">Click **Restart** when prompted.</span><span class="sxs-lookup"><span data-stu-id="be129-139">Click **Restart** when prompted.</span></span>

      ![Set the boot configuration](media/asdk-redeploy/4.png)

2. <span data-ttu-id="be129-141">After the development kit host reboots into the base operating system, log in as a local administrator for the development kit host computer.</span><span class="sxs-lookup"><span data-stu-id="be129-141">After the development kit host reboots into the base operating system, log in as a local administrator for the development kit host computer.</span></span> <span data-ttu-id="be129-142">Locate and delete the **C:\CloudBuilder.vhdx** file that was used as part of the previous deployment.</span><span class="sxs-lookup"><span data-stu-id="be129-142">Locate and delete the **C:\CloudBuilder.vhdx** file that was used as part of the previous deployment.</span></span> 

3. <span data-ttu-id="be129-143">Repeat the same steps that you took to first [deploy the ASDK using PowerShell](asdk-deploy-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="be129-143">Repeat the same steps that you took to first [deploy the ASDK using PowerShell](asdk-deploy-powershell.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="be129-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="be129-144">Next steps</span></span>
[<span data-ttu-id="be129-145">Post ASDK installation configuration tasks</span><span class="sxs-lookup"><span data-stu-id="be129-145">Post ASDK installation configuration tasks</span></span>](asdk-post-deploy.md)




