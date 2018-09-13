---
title: Prepare the Azure Stack Development Kit (ASDK) host computer | Microsoft Docs
description: Describes how to prepare the Azure Stack Development Kit (ASDK) host computer for ASDK installation.
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
ms.openlocfilehash: 5de25f574cb876701ffce74f1dca8c4bb9764157
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869114"
---
# <a name="prepare-the-asdk-host-computer"></a><span data-ttu-id="3a4eb-103">Prepare the ASDK host computer</span><span class="sxs-lookup"><span data-stu-id="3a4eb-103">Prepare the ASDK host computer</span></span>
<span data-ttu-id="3a4eb-104">Before you can install the ASDK on the host computer, the ASDK environment must be prepared for installation.</span><span class="sxs-lookup"><span data-stu-id="3a4eb-104">Before you can install the ASDK on the host computer, the ASDK environment must be prepared for installation.</span></span> <span data-ttu-id="3a4eb-105">When the development kit host computer has been prepared, it will boot from the CloudBuilder.vhdx virtual machine hard drive to begin ASDK deployment.</span><span class="sxs-lookup"><span data-stu-id="3a4eb-105">When the development kit host computer has been prepared, it will boot from the CloudBuilder.vhdx virtual machine hard drive to begin ASDK deployment.</span></span>

## <a name="prepare-the-development-kit-host-computer"></a><span data-ttu-id="3a4eb-106">Prepare the development kit host computer</span><span class="sxs-lookup"><span data-stu-id="3a4eb-106">Prepare the development kit host computer</span></span>
<span data-ttu-id="3a4eb-107">Before you can install the ASDK on the host computer, the ASDK host computer environment must be prepared.</span><span class="sxs-lookup"><span data-stu-id="3a4eb-107">Before you can install the ASDK on the host computer, the ASDK host computer environment must be prepared.</span></span>
1. <span data-ttu-id="3a4eb-108">Sign in as a Local Administrator to your development kit host computer.</span><span class="sxs-lookup"><span data-stu-id="3a4eb-108">Sign in as a Local Administrator to your development kit host computer.</span></span>
2. <span data-ttu-id="3a4eb-109">Ensure that the CloudBuilder.vhdx file has been moved to the root of the C:\ drive (C:\CloudBuilder.vhdx).</span><span class="sxs-lookup"><span data-stu-id="3a4eb-109">Ensure that the CloudBuilder.vhdx file has been moved to the root of the C:\ drive (C:\CloudBuilder.vhdx).</span></span>
3. <span data-ttu-id="3a4eb-110">Run the following script to download the development kit installer file (asdk-installer.ps1) from the [Azure Stack GitHub tools repository](https://github.com/Azure/AzureStack-Tools) to the **C:\AzureStack_Installer** folder on your development kit host computer:</span><span class="sxs-lookup"><span data-stu-id="3a4eb-110">Run the following script to download the development kit installer file (asdk-installer.ps1) from the [Azure Stack GitHub tools repository](https://github.com/Azure/AzureStack-Tools) to the **C:\AzureStack_Installer** folder on your development kit host computer:</span></span>

  ```powershell
  # Variables
  $Uri = 'https://raw.githubusercontent.com/Azure/AzureStack-Tools/master/Deployment/asdk-installer.ps1'
  $LocalPath = 'C:\AzureStack_Installer'
  # Create folder
  New-Item $LocalPath -Type directory
  # Enforce usage of TLSv1.2 to download from GitHub
  [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
  # Download file
  Invoke-WebRequest $uri -OutFile ($LocalPath + '\' + 'asdk-installer.ps1')
  ```

4. <span data-ttu-id="3a4eb-111">From an elevated PowerShell console, start the **C:\AzureStack_Installer\asdk-installer.ps1** script, and then click **Prepare Environment**.</span><span class="sxs-lookup"><span data-stu-id="3a4eb-111">From an elevated PowerShell console, start the **C:\AzureStack_Installer\asdk-installer.ps1** script, and then click **Prepare Environment**.</span></span>

    ![](media/asdk-prepare-host/1.PNG) 

5. <span data-ttu-id="3a4eb-112">On the **Select Cloudbuilder vhdx** page of the installer, browse to and select the **cloudbuilder.vhdx** file that you downloaded and extracted in [the previous steps](asdk-download.md).</span><span class="sxs-lookup"><span data-stu-id="3a4eb-112">On the **Select Cloudbuilder vhdx** page of the installer, browse to and select the **cloudbuilder.vhdx** file that you downloaded and extracted in [the previous steps](asdk-download.md).</span></span> <span data-ttu-id="3a4eb-113">On this page, you can also, optionally, enable the **Add drivers** check box if you need to add additional drivers to the development kit host computer.</span><span class="sxs-lookup"><span data-stu-id="3a4eb-113">On this page, you can also, optionally, enable the **Add drivers** check box if you need to add additional drivers to the development kit host computer.</span></span> <span data-ttu-id="3a4eb-114">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3a4eb-114">Click **Next**.</span></span>  

    ![](media/asdk-prepare-host/2.PNG)

6. <span data-ttu-id="3a4eb-115">On the **Optional settings** page, provide the local administrator account information for the development kit host computer and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3a4eb-115">On the **Optional settings** page, provide the local administrator account information for the development kit host computer and then click **Next**.</span></span> <span data-ttu-id="3a4eb-116">You can also provide values for the following optional settings:</span><span class="sxs-lookup"><span data-stu-id="3a4eb-116">You can also provide values for the following optional settings:</span></span>
  - <span data-ttu-id="3a4eb-117">**Computername**: This option sets the name for the development kit host.</span><span class="sxs-lookup"><span data-stu-id="3a4eb-117">**Computername**: This option sets the name for the development kit host.</span></span> <span data-ttu-id="3a4eb-118">The name must comply with FQDN requirements and must be 15 characters or less in length.</span><span class="sxs-lookup"><span data-stu-id="3a4eb-118">The name must comply with FQDN requirements and must be 15 characters or less in length.</span></span> <span data-ttu-id="3a4eb-119">The default is a random computer name generated by Windows.</span><span class="sxs-lookup"><span data-stu-id="3a4eb-119">The default is a random computer name generated by Windows.</span></span>
  - <span data-ttu-id="3a4eb-120">**Time zone**: Sets the time zone for the development kit host.</span><span class="sxs-lookup"><span data-stu-id="3a4eb-120">**Time zone**: Sets the time zone for the development kit host.</span></span> <span data-ttu-id="3a4eb-121">The default is (UTC-8:00) Pacific Time (US & Canada).</span><span class="sxs-lookup"><span data-stu-id="3a4eb-121">The default is (UTC-8:00) Pacific Time (US & Canada).</span></span>
  - <span data-ttu-id="3a4eb-122">**Static IP configuration**: Sets your deployment to use a static IP address.</span><span class="sxs-lookup"><span data-stu-id="3a4eb-122">**Static IP configuration**: Sets your deployment to use a static IP address.</span></span> <span data-ttu-id="3a4eb-123">Otherwise, when the installer reboots into the cloudbuilder.vhx, the network interfaces are configured with DHCP.</span><span class="sxs-lookup"><span data-stu-id="3a4eb-123">Otherwise, when the installer reboots into the cloudbuilder.vhx, the network interfaces are configured with DHCP.</span></span>

    ![](media/asdk-prepare-host/3.PNG)

  > [!IMPORTANT]
  > <span data-ttu-id="3a4eb-124">If you don't provide the local administrator credentials in this step, you'll need direct or KVM access to the host after the computer restarts as part of setting up the development kit.</span><span class="sxs-lookup"><span data-stu-id="3a4eb-124">If you don't provide the local administrator credentials in this step, you'll need direct or KVM access to the host after the computer restarts as part of setting up the development kit.</span></span>

7. <span data-ttu-id="3a4eb-125">If you chose a static IP configuration in the previous step, you must now:</span><span class="sxs-lookup"><span data-stu-id="3a4eb-125">If you chose a static IP configuration in the previous step, you must now:</span></span>
    - <span data-ttu-id="3a4eb-126">Select a network adapter.</span><span class="sxs-lookup"><span data-stu-id="3a4eb-126">Select a network adapter.</span></span> <span data-ttu-id="3a4eb-127">Make sure you can connect to the adapter before you click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3a4eb-127">Make sure you can connect to the adapter before you click **Next**.</span></span>
    - <span data-ttu-id="3a4eb-128">Make sure that the **IP address**, **Gateway**, and **DNS** values are correct and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3a4eb-128">Make sure that the **IP address**, **Gateway**, and **DNS** values are correct and then click **Next**.</span></span>
13. <span data-ttu-id="3a4eb-129">Click **Next** to start the preparation process.</span><span class="sxs-lookup"><span data-stu-id="3a4eb-129">Click **Next** to start the preparation process.</span></span>
14. <span data-ttu-id="3a4eb-130">When the preparation indicates **Completed**, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3a4eb-130">When the preparation indicates **Completed**, click **Next**.</span></span>
15. <span data-ttu-id="3a4eb-131">Click **Reboot now** to boot the development kit host computer into the cloudbuilder.vhdx and [continue the deployment process](asdk-install.md).</span><span class="sxs-lookup"><span data-stu-id="3a4eb-131">Click **Reboot now** to boot the development kit host computer into the cloudbuilder.vhdx and [continue the deployment process](asdk-install.md).</span></span>

    ![](media/asdk-prepare-host/4.PNG)


## <a name="next-steps"></a><span data-ttu-id="3a4eb-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="3a4eb-132">Next steps</span></span>
[<span data-ttu-id="3a4eb-133">Install the ASDK</span><span class="sxs-lookup"><span data-stu-id="3a4eb-133">Install the ASDK</span></span>](asdk-install.md)