---
title: Quickstart - Create a Windows VM in the Azure portal | Microsoft Docs
description: In this quickstart, you learn how to use the Azure portal to create a Windows virtual machine
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: jeconnoc
editor: tysonn
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/03/2018
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 808619949947f200668d0db6c0576093ce5598f8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809639"
---
# <a name="quickstart-create-a-windows-virtual-machine-in-the-azure-portal"></a><span data-ttu-id="47b5f-103">Quickstart: Create a Windows virtual machine in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="47b5f-103">Quickstart: Create a Windows virtual machine in the Azure portal</span></span>

<span data-ttu-id="47b5f-104">Azure virtual machines (VMs) can be created through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="47b5f-104">Azure virtual machines (VMs) can be created through the Azure portal.</span></span> <span data-ttu-id="47b5f-105">This method provides a browser-based user interface to create VMs and their associated resources.</span><span class="sxs-lookup"><span data-stu-id="47b5f-105">This method provides a browser-based user interface to create VMs and their associated resources.</span></span> <span data-ttu-id="47b5f-106">This quickstart shows you how to use the Azure portal to deploy a virtual machine (VM) in Azure that runs Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="47b5f-106">This quickstart shows you how to use the Azure portal to deploy a virtual machine (VM) in Azure that runs Windows Server 2016.</span></span> <span data-ttu-id="47b5f-107">To see your VM in action, you then RDP to the VM and install the IIS web server.</span><span class="sxs-lookup"><span data-stu-id="47b5f-107">To see your VM in action, you then RDP to the VM and install the IIS web server.</span></span>

<span data-ttu-id="47b5f-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="47b5f-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="47b5f-109">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="47b5f-109">Sign in to Azure</span></span>

<span data-ttu-id="47b5f-110">Sign in to the Azure portal at https://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="47b5f-110">Sign in to the Azure portal at https://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="47b5f-111">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="47b5f-111">Create virtual machine</span></span>

1. <span data-ttu-id="47b5f-112">Choose **Create a resource** in the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="47b5f-112">Choose **Create a resource** in the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="47b5f-113">In the search box above the list of Azure Marketplace resources, search for and select **Windows Server 2016 Datacenter**, then choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="47b5f-113">In the search box above the list of Azure Marketplace resources, search for and select **Windows Server 2016 Datacenter**, then choose **Create**.</span></span>

3. <span data-ttu-id="47b5f-114">Provide a VM name, such as *myVM*, leave the disk type as *SSD*, then provide a username, such as *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="47b5f-114">Provide a VM name, such as *myVM*, leave the disk type as *SSD*, then provide a username, such as *azureuser*.</span></span> <span data-ttu-id="47b5f-115">The password must be at least 12 characters long and meet the [defined complexity requirements](faq.md#what-are-the-password-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="47b5f-115">The password must be at least 12 characters long and meet the [defined complexity requirements](faq.md#what-are-the-password-requirements-when-creating-a-vm).</span></span>

    ![Enter basic information about your VM in the portal blade](./media/quick-create-portal/create-windows-vm-portal-basic-blade.png)

5. <span data-ttu-id="47b5f-117">Choose to **Create new** resource group, then provide a name, such as *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="47b5f-117">Choose to **Create new** resource group, then provide a name, such as *myResourceGroup*.</span></span> <span data-ttu-id="47b5f-118">Choose your **Location**, then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="47b5f-118">Choose your **Location**, then select **OK**.</span></span>

4. <span data-ttu-id="47b5f-119">Select a size for the VM.</span><span class="sxs-lookup"><span data-stu-id="47b5f-119">Select a size for the VM.</span></span> <span data-ttu-id="47b5f-120">You can filter by *Compute type* or *Disk type*, for example.</span><span class="sxs-lookup"><span data-stu-id="47b5f-120">You can filter by *Compute type* or *Disk type*, for example.</span></span> <span data-ttu-id="47b5f-121">A suggested VM size is *D2s_v3*.</span><span class="sxs-lookup"><span data-stu-id="47b5f-121">A suggested VM size is *D2s_v3*.</span></span> <span data-ttu-id="47b5f-122">Click **Select** after you have chosen a size.</span><span class="sxs-lookup"><span data-stu-id="47b5f-122">Click **Select** after you have chosen a size.</span></span>

    ![Screenshot that shows VM sizes](./media/quick-create-portal/create-windows-vm-portal-sizes.png)

5. <span data-ttu-id="47b5f-124">On the **Settings** page, in **Network** > **Network Security Group** > **Select public inbound ports**, select **HTTP** and **RDP (3389)** from the drop-down.</span><span class="sxs-lookup"><span data-stu-id="47b5f-124">On the **Settings** page, in **Network** > **Network Security Group** > **Select public inbound ports**, select **HTTP** and **RDP (3389)** from the drop-down.</span></span> <span data-ttu-id="47b5f-125">Leave the rest of the defaults and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="47b5f-125">Leave the rest of the defaults and select **OK**.</span></span>

6. <span data-ttu-id="47b5f-126">On the summary page, select **Create** to start the VM deployment.</span><span class="sxs-lookup"><span data-stu-id="47b5f-126">On the summary page, select **Create** to start the VM deployment.</span></span>

7. <span data-ttu-id="47b5f-127">The VM is pinned to the Azure portal dashboard.</span><span class="sxs-lookup"><span data-stu-id="47b5f-127">The VM is pinned to the Azure portal dashboard.</span></span> <span data-ttu-id="47b5f-128">Once the deployment has completed, the VM summary automatically opens.</span><span class="sxs-lookup"><span data-stu-id="47b5f-128">Once the deployment has completed, the VM summary automatically opens.</span></span>

## <a name="connect-to-virtual-machine"></a><span data-ttu-id="47b5f-129">Connect to virtual machine</span><span class="sxs-lookup"><span data-stu-id="47b5f-129">Connect to virtual machine</span></span>

<span data-ttu-id="47b5f-130">Create a remote desktop connection to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="47b5f-130">Create a remote desktop connection to the virtual machine.</span></span> <span data-ttu-id="47b5f-131">These directions tell you how to connect to your VM from a Windows computer.</span><span class="sxs-lookup"><span data-stu-id="47b5f-131">These directions tell you how to connect to your VM from a Windows computer.</span></span> <span data-ttu-id="47b5f-132">On a Mac, you need an RDP client such as this [Remote Desktop Client](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) from the Mac App Store.</span><span class="sxs-lookup"><span data-stu-id="47b5f-132">On a Mac, you need an RDP client such as this [Remote Desktop Client](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) from the Mac App Store.</span></span>

1. <span data-ttu-id="47b5f-133">Click the **Connect** button on the virtual machine properties page.</span><span class="sxs-lookup"><span data-stu-id="47b5f-133">Click the **Connect** button on the virtual machine properties page.</span></span> 

    ![Connect to an Azure VM from the portal](./media/quick-create-portal/quick-create-portal/portal-quick-start-9.png)
    
2. <span data-ttu-id="47b5f-135">In the **Connect to virtual machine** page, keep the default options to connect by DNS name over port 3389 and click **Download RDP file**.</span><span class="sxs-lookup"><span data-stu-id="47b5f-135">In the **Connect to virtual machine** page, keep the default options to connect by DNS name over port 3389 and click **Download RDP file**.</span></span>

2. <span data-ttu-id="47b5f-136">Open the downloaded RDP file and click **Connect** when prompted.</span><span class="sxs-lookup"><span data-stu-id="47b5f-136">Open the downloaded RDP file and click **Connect** when prompted.</span></span> 

3. <span data-ttu-id="47b5f-137">In the **Windows Security** window, select **More choices** and then **Use a different account**.</span><span class="sxs-lookup"><span data-stu-id="47b5f-137">In the **Windows Security** window, select **More choices** and then **Use a different account**.</span></span> <span data-ttu-id="47b5f-138">Type the username as *vmname*\\*username*, enter password you created for the virtual machine, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="47b5f-138">Type the username as *vmname*\\*username*, enter password you created for the virtual machine, and then click **OK**.</span></span>

4. <span data-ttu-id="47b5f-139">You may receive a certificate warning during the sign-in process.</span><span class="sxs-lookup"><span data-stu-id="47b5f-139">You may receive a certificate warning during the sign-in process.</span></span> <span data-ttu-id="47b5f-140">Click **Yes** or **Continue** to create the connection.</span><span class="sxs-lookup"><span data-stu-id="47b5f-140">Click **Yes** or **Continue** to create the connection.</span></span>

## <a name="install-web-server"></a><span data-ttu-id="47b5f-141">Install web server</span><span class="sxs-lookup"><span data-stu-id="47b5f-141">Install web server</span></span>

<span data-ttu-id="47b5f-142">To see your VM in action, install the IIS web server.</span><span class="sxs-lookup"><span data-stu-id="47b5f-142">To see your VM in action, install the IIS web server.</span></span> <span data-ttu-id="47b5f-143">Open a PowerShell prompt on the VM and run the following command:</span><span class="sxs-lookup"><span data-stu-id="47b5f-143">Open a PowerShell prompt on the VM and run the following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="47b5f-144">When done, close the RDP connection to the VM.</span><span class="sxs-lookup"><span data-stu-id="47b5f-144">When done, close the RDP connection to the VM.</span></span>


## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="47b5f-145">View the IIS welcome page</span><span class="sxs-lookup"><span data-stu-id="47b5f-145">View the IIS welcome page</span></span>

<span data-ttu-id="47b5f-146">In the portal, select the VM and in the overview of the VM, use the **Click to copy** button to the right of the IP address to copy it and paste it into a browser tab. The default IIS welcome page will open, and should look like this:</span><span class="sxs-lookup"><span data-stu-id="47b5f-146">In the portal, select the VM and in the overview of the VM, use the **Click to copy** button to the right of the IP address to copy it and paste it into a browser tab. The default IIS welcome page will open, and should look like this:</span></span>

![IIS default site](./media/quick-create-powershell/default-iis-website.png)

## <a name="clean-up-resources"></a><span data-ttu-id="47b5f-148">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="47b5f-148">Clean up resources</span></span>

<span data-ttu-id="47b5f-149">When no longer needed, you can delete the resource group, virtual machine, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="47b5f-149">When no longer needed, you can delete the resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="47b5f-150">To do so, select the resource group for the virtual machine, select **Delete**, then confirm the name of the resource group to delete.</span><span class="sxs-lookup"><span data-stu-id="47b5f-150">To do so, select the resource group for the virtual machine, select **Delete**, then confirm the name of the resource group to delete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47b5f-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="47b5f-151">Next steps</span></span>

<span data-ttu-id="47b5f-152">In this quickstart, you deployed a simple virtual machine, open a network port for web traffic, and installed a basic web server.</span><span class="sxs-lookup"><span data-stu-id="47b5f-152">In this quickstart, you deployed a simple virtual machine, open a network port for web traffic, and installed a basic web server.</span></span> <span data-ttu-id="47b5f-153">To learn more about Azure virtual machines, continue to the tutorial for Windows VMs.</span><span class="sxs-lookup"><span data-stu-id="47b5f-153">To learn more about Azure virtual machines, continue to the tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="47b5f-154">Azure Windows virtual machine tutorials</span><span class="sxs-lookup"><span data-stu-id="47b5f-154">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
