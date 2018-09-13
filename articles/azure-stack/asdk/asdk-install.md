---
title: Install the Azure Stack Development Kit (ASDK) | Microsoft Docs
description: Describes how to install the Azure Stack Development Kit (ASDK).
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
ms.date: 03/22/2018
ms.author: jeffgilb
ms.reviewer: misainat
ms.openlocfilehash: 74a81901c8ad38a84357a9f3c2e1d948aa81e8bc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866077"
---
# <a name="install-the-azure-stack-development-kit-asdk"></a><span data-ttu-id="b733f-103">Install the Azure Stack Development Kit (ASDK)</span><span class="sxs-lookup"><span data-stu-id="b733f-103">Install the Azure Stack Development Kit (ASDK)</span></span>
<span data-ttu-id="b733f-104">After [preparing the ASDK host computer](asdk-prepare-host.md), the ASDK can be deployed into the CloudBuilder.vhdx image using the following steps in this article.</span><span class="sxs-lookup"><span data-stu-id="b733f-104">After [preparing the ASDK host computer](asdk-prepare-host.md), the ASDK can be deployed into the CloudBuilder.vhdx image using the following steps in this article.</span></span>

## <a name="install-the-asdk"></a><span data-ttu-id="b733f-105">Install the ASDK</span><span class="sxs-lookup"><span data-stu-id="b733f-105">Install the ASDK</span></span>
<span data-ttu-id="b733f-106">The steps in this article show you how to deploy the ASDK using a graphical user interface (GUI) provided by downloading and running the **asdk-installer.ps1** PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="b733f-106">The steps in this article show you how to deploy the ASDK using a graphical user interface (GUI) provided by downloading and running the **asdk-installer.ps1** PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="b733f-107">The installer user interface for the Azure Stack Development Kit is an open-sourced script based on WCF and PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b733f-107">The installer user interface for the Azure Stack Development Kit is an open-sourced script based on WCF and PowerShell.</span></span>


1. <span data-ttu-id="b733f-108">After the host computer successfully boots into the CloudBuilder.vhdx image, log in using the administrator credentials specified when you [prepared the development kit host computer](asdk-prepare-host.md) for ASDK installation.</span><span class="sxs-lookup"><span data-stu-id="b733f-108">After the host computer successfully boots into the CloudBuilder.vhdx image, log in using the administrator credentials specified when you [prepared the development kit host computer](asdk-prepare-host.md) for ASDK installation.</span></span> <span data-ttu-id="b733f-109">This should be the same as the development kit host local administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="b733f-109">This should be the same as the development kit host local administrator credentials.</span></span>
2. <span data-ttu-id="b733f-110">Open an elevated PowerShell console and run the **&lt;drive letter>\AzureStack_Installer\asdk-installer.ps1** script (which might now be on a different drive than C:\ in the CloudBuilder.vhdx image).</span><span class="sxs-lookup"><span data-stu-id="b733f-110">Open an elevated PowerShell console and run the **&lt;drive letter>\AzureStack_Installer\asdk-installer.ps1** script (which might now be on a different drive than C:\ in the CloudBuilder.vhdx image).</span></span> <span data-ttu-id="b733f-111">Click **Install**.</span><span class="sxs-lookup"><span data-stu-id="b733f-111">Click **Install**.</span></span>

    ![](media/asdk-install/1.PNG) 

3. <span data-ttu-id="b733f-112">In the Identity Provider **Type** drop-down box, select **Azure Cloud** or **AD FS**.</span><span class="sxs-lookup"><span data-stu-id="b733f-112">In the Identity Provider **Type** drop-down box, select **Azure Cloud** or **AD FS**.</span></span> <span data-ttu-id="b733f-113">Under **Local Administrator Password** type the local administrator password (which must match the current configured local administrator password) in the **Password** box, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b733f-113">Under **Local Administrator Password** type the local administrator password (which must match the current configured local administrator password) in the **Password** box, and then click **Next**.</span></span>
    - <span data-ttu-id="b733f-114">**Azure Cloud**: Configures Azure Active Directory (Azure AD) as the identity provider.</span><span class="sxs-lookup"><span data-stu-id="b733f-114">**Azure Cloud**: Configures Azure Active Directory (Azure AD) as the identity provider.</span></span> <span data-ttu-id="b733f-115">To use this option, you need an internet connection, the full name of an Azure AD directory tenant in the form of *domainname*.onmicrosoft.com or an Azure AD verified custom domain name, and global admin credentials for the specified directory.</span><span class="sxs-lookup"><span data-stu-id="b733f-115">To use this option, you need an internet connection, the full name of an Azure AD directory tenant in the form of *domainname*.onmicrosoft.com or an Azure AD verified custom domain name, and global admin credentials for the specified directory.</span></span> 
    - <span data-ttu-id="b733f-116">**AD FS**: The default stamp directory service is used as the identity provider.</span><span class="sxs-lookup"><span data-stu-id="b733f-116">**AD FS**: The default stamp directory service is used as the identity provider.</span></span> <span data-ttu-id="b733f-117">The default account to sign in with is azurestackadmin@azurestack.local, and the password to use is the one you provided as part of setup.</span><span class="sxs-lookup"><span data-stu-id="b733f-117">The default account to sign in with is azurestackadmin@azurestack.local, and the password to use is the one you provided as part of setup.</span></span>

    ![](media/asdk-install/2.PNG) 
    
    > [!NOTE]
    > <span data-ttu-id="b733f-118">For best results, even if you want to use a disconnected Azure Stack environment using AD FS as the identity provider, it is best to install the ASDK while connected to the internet.</span><span class="sxs-lookup"><span data-stu-id="b733f-118">For best results, even if you want to use a disconnected Azure Stack environment using AD FS as the identity provider, it is best to install the ASDK while connected to the internet.</span></span> <span data-ttu-id="b733f-119">That way, the Windows Server 2016 evaluation version included with the development kit installation can be activated at deployment time.</span><span class="sxs-lookup"><span data-stu-id="b733f-119">That way, the Windows Server 2016 evaluation version included with the development kit installation can be activated at deployment time.</span></span>
4. <span data-ttu-id="b733f-120">Select a network adapter to use for the development kit and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b733f-120">Select a network adapter to use for the development kit and then click **Next**.</span></span>

    ![](media/asdk-install/3.PNG)

5. <span data-ttu-id="b733f-121">Select DHCP or static network configuration for the BGPNAT01 virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b733f-121">Select DHCP or static network configuration for the BGPNAT01 virtual machine.</span></span>
    > [!TIP]
    > <span data-ttu-id="b733f-122">The BGPNAT01 VM is the edge router that provides NAT and VPN capabilities for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b733f-122">The BGPNAT01 VM is the edge router that provides NAT and VPN capabilities for Azure Stack.</span></span>

    - <span data-ttu-id="b733f-123">**DHCP** (default): The virtual machine gets the IP network configuration from the DHCP server.</span><span class="sxs-lookup"><span data-stu-id="b733f-123">**DHCP** (default): The virtual machine gets the IP network configuration from the DHCP server.</span></span>
    - <span data-ttu-id="b733f-124">**Static**: Only use this option if DHCP can’t assign a valid IP address for Azure Stack to access the Internet.</span><span class="sxs-lookup"><span data-stu-id="b733f-124">**Static**: Only use this option if DHCP can’t assign a valid IP address for Azure Stack to access the Internet.</span></span> <span data-ttu-id="b733f-125">**A static IP address must be specified with the subnetmask length in CIDR format (for example, 10.0.0.5/24)**.</span><span class="sxs-lookup"><span data-stu-id="b733f-125">**A static IP address must be specified with the subnetmask length in CIDR format (for example, 10.0.0.5/24)**.</span></span>
    - <span data-ttu-id="b733f-126">Type in a valid **Time server IP** address.</span><span class="sxs-lookup"><span data-stu-id="b733f-126">Type in a valid **Time server IP** address.</span></span> <span data-ttu-id="b733f-127">This required field sets the time server to be used by the development kit.</span><span class="sxs-lookup"><span data-stu-id="b733f-127">This required field sets the time server to be used by the development kit.</span></span> <span data-ttu-id="b733f-128">This parameter must be provided as a valid time server IP address.</span><span class="sxs-lookup"><span data-stu-id="b733f-128">This parameter must be provided as a valid time server IP address.</span></span> <span data-ttu-id="b733f-129">Server names are not supported.</span><span class="sxs-lookup"><span data-stu-id="b733f-129">Server names are not supported.</span></span>

      > [!TIP]
      > <span data-ttu-id="b733f-130">To find a time server IP address, visit [pool.ntp.org](http://pool.ntp.org) or ping time.windows.com.</span><span class="sxs-lookup"><span data-stu-id="b733f-130">To find a time server IP address, visit [pool.ntp.org](http://pool.ntp.org) or ping time.windows.com.</span></span> 

    - <span data-ttu-id="b733f-131">**Optionally**, you set the following values:</span><span class="sxs-lookup"><span data-stu-id="b733f-131">**Optionally**, you set the following values:</span></span>
        - <span data-ttu-id="b733f-132">**VLAN ID**: Sets the VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="b733f-132">**VLAN ID**: Sets the VLAN ID.</span></span> <span data-ttu-id="b733f-133">Only use this option if the host and AzS-BGPNAT01 must configure VLAN ID to access the physical network (and internet).</span><span class="sxs-lookup"><span data-stu-id="b733f-133">Only use this option if the host and AzS-BGPNAT01 must configure VLAN ID to access the physical network (and internet).</span></span> 
        - <span data-ttu-id="b733f-134">**DNS forwarder**: A DNS server is created as part of the Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="b733f-134">**DNS forwarder**: A DNS server is created as part of the Azure Stack deployment.</span></span> <span data-ttu-id="b733f-135">To allow computers inside the solution to resolve names outside of the stamp, provide your existing infrastructure DNS server.</span><span class="sxs-lookup"><span data-stu-id="b733f-135">To allow computers inside the solution to resolve names outside of the stamp, provide your existing infrastructure DNS server.</span></span> <span data-ttu-id="b733f-136">The in-stamp DNS server forwards unknown name resolution requests to this server.</span><span class="sxs-lookup"><span data-stu-id="b733f-136">The in-stamp DNS server forwards unknown name resolution requests to this server.</span></span>

    ![](media/asdk-install/4.PNG)

6. <span data-ttu-id="b733f-137">On the **Verifying network interface card properties** page, you'll see a progress bar.</span><span class="sxs-lookup"><span data-stu-id="b733f-137">On the **Verifying network interface card properties** page, you'll see a progress bar.</span></span> <span data-ttu-id="b733f-138">When verification is complete, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b733f-138">When verification is complete, click **Next**.</span></span>

    ![](media/asdk-install/5.PNG)

9. <span data-ttu-id="b733f-139">On **Summary** page, click **Deploy** to start ASDK installation on the development kit host computer.</span><span class="sxs-lookup"><span data-stu-id="b733f-139">On **Summary** page, click **Deploy** to start ASDK installation on the development kit host computer.</span></span>

    ![](media/asdk-install/6.PNG)

    > [!TIP]
    > <span data-ttu-id="b733f-140">Here you can also copy the PowerShell setup commands that will be used to install the development kit.</span><span class="sxs-lookup"><span data-stu-id="b733f-140">Here you can also copy the PowerShell setup commands that will be used to install the development kit.</span></span> <span data-ttu-id="b733f-141">This is helpful if you ever need to [redeploy the ASDK on the host computer using PowerShell](asdk-deploy-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b733f-141">This is helpful if you ever need to [redeploy the ASDK on the host computer using PowerShell](asdk-deploy-powershell.md).</span></span>

10. <span data-ttu-id="b733f-142">If you're performing an Azure AD deployment, you'll be prompted to enter your Azure AD global administrator account credentials a few minutes after setup starts.</span><span class="sxs-lookup"><span data-stu-id="b733f-142">If you're performing an Azure AD deployment, you'll be prompted to enter your Azure AD global administrator account credentials a few minutes after setup starts.</span></span>

    ![](media/asdk-install/7.PNG)

11. <span data-ttu-id="b733f-143">The deployment process will take a few hours, during which time the host computer will automatically reboot once.</span><span class="sxs-lookup"><span data-stu-id="b733f-143">The deployment process will take a few hours, during which time the host computer will automatically reboot once.</span></span> <span data-ttu-id="b733f-144">If you want to monitor the deployment progress, sign in as azurestack\AzureStackAdmin after the development kit host restarts.</span><span class="sxs-lookup"><span data-stu-id="b733f-144">If you want to monitor the deployment progress, sign in as azurestack\AzureStackAdmin after the development kit host restarts.</span></span> <span data-ttu-id="b733f-145">When the deployment succeeds, the PowerShell console displays: **COMPLETE: Action 'Deployment'**.</span><span class="sxs-lookup"><span data-stu-id="b733f-145">When the deployment succeeds, the PowerShell console displays: **COMPLETE: Action 'Deployment'**.</span></span> 
    > [!IMPORTANT]
    > <span data-ttu-id="b733f-146">If you sign in as a local admin after the machine is joined to the domain, you won't see the deployment progress.</span><span class="sxs-lookup"><span data-stu-id="b733f-146">If you sign in as a local admin after the machine is joined to the domain, you won't see the deployment progress.</span></span> <span data-ttu-id="b733f-147">Do not rerun deployment, instead sign in as azurestack\AzureStackAdmin to validate that it's running.</span><span class="sxs-lookup"><span data-stu-id="b733f-147">Do not rerun deployment, instead sign in as azurestack\AzureStackAdmin to validate that it's running.</span></span>

    ![](media/asdk-install/8.PNG)

<span data-ttu-id="b733f-148">Congratulations, you've successfully installed the ASDK!</span><span class="sxs-lookup"><span data-stu-id="b733f-148">Congratulations, you've successfully installed the ASDK!</span></span>

<span data-ttu-id="b733f-149">If the deployment fails for some reason, you can [redeploy](asdk-redeploy.md) from scratch or use the following PowerShell commands, from the same elevated PowerShell window, to restart the deployment from the last successful step:</span><span class="sxs-lookup"><span data-stu-id="b733f-149">If the deployment fails for some reason, you can [redeploy](asdk-redeploy.md) from scratch or use the following PowerShell commands, from the same elevated PowerShell window, to restart the deployment from the last successful step:</span></span>

  ```powershell
  cd C:\CloudDeployment\Setup
  .\InstallAzureStackPOC.ps1 -Rerun
  ```

## <a name="next-steps"></a><span data-ttu-id="b733f-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="b733f-150">Next steps</span></span>
[<span data-ttu-id="b733f-151">Post deployment configuration</span><span class="sxs-lookup"><span data-stu-id="b733f-151">Post deployment configuration</span></span>](asdk-post-deploy.md)
