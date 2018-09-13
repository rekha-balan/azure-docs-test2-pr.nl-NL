---
title: Azure Quick Start - Create Windows VM Portal | Microsoft Docs
description: Azure Quick Start - Create Windows VM Portal
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 04/13/2017
ms.author: nepeters
ms.openlocfilehash: a8008475ec6ee39a91a9c93c835ca5e4dcc3fa91
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564424"
---
# <a name="create-a-windows-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="00ee3-103">Create a Windows virtual machine with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="00ee3-103">Create a Windows virtual machine with the Azure portal</span></span>

<span data-ttu-id="00ee3-104">Azure virtual machines can be created through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="00ee3-104">Azure virtual machines can be created through the Azure portal.</span></span> <span data-ttu-id="00ee3-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span><span class="sxs-lookup"><span data-stu-id="00ee3-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="00ee3-106">This Quickstart steps through creating a virtual machine using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="00ee3-106">This Quickstart steps through creating a virtual machine using the Azure portal.</span></span> <span data-ttu-id="00ee3-107">Once deployment is complete, we connect to the server and install IIS.</span><span class="sxs-lookup"><span data-stu-id="00ee3-107">Once deployment is complete, we connect to the server and install IIS.</span></span>

<span data-ttu-id="00ee3-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/en-us/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="00ee3-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/en-us/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="00ee3-109">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="00ee3-109">Log in to Azure</span></span>

<span data-ttu-id="00ee3-110">Log in to the Azure portal at http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="00ee3-110">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="00ee3-111">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="00ee3-111">Create virtual machine</span></span>

2. <span data-ttu-id="00ee3-112">Click the **New** button found on the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="00ee3-112">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

3. <span data-ttu-id="00ee3-113">Select **Compute** from the **New** blade, select **Windows Server 2016 Datacenter** from the **Compute** blade, and then click the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="00ee3-113">Select **Compute** from the **New** blade, select **Windows Server 2016 Datacenter** from the **Compute** blade, and then click the **Create** button.</span></span>

4. <span data-ttu-id="00ee3-114">Fill out the virtual machine **Basics** form.</span><span class="sxs-lookup"><span data-stu-id="00ee3-114">Fill out the virtual machine **Basics** form.</span></span> <span data-ttu-id="00ee3-115">The user name and password entered here is used to log in to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="00ee3-115">The user name and password entered here is used to log in to the virtual machine.</span></span> <span data-ttu-id="00ee3-116">For **Resource group**, create a new one.</span><span class="sxs-lookup"><span data-stu-id="00ee3-116">For **Resource group**, create a new one.</span></span> <span data-ttu-id="00ee3-117">A resource group is a logical container into which Azure resources are created and collectively managed.</span><span class="sxs-lookup"><span data-stu-id="00ee3-117">A resource group is a logical container into which Azure resources are created and collectively managed.</span></span> <span data-ttu-id="00ee3-118">When complete, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="00ee3-118">When complete, click **OK**.</span></span>

    ![Enter basic information about your VM in the portal blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/quick-create-portal/create-windows-vm-portal-basic-blade.png)  

5. <span data-ttu-id="00ee3-120">Choose a size for the VM.</span><span class="sxs-lookup"><span data-stu-id="00ee3-120">Choose a size for the VM.</span></span> <span data-ttu-id="00ee3-121">To see more sizes, select **View all** or change the **Supported disk type** filter.</span><span class="sxs-lookup"><span data-stu-id="00ee3-121">To see more sizes, select **View all** or change the **Supported disk type** filter.</span></span> 

    ![Screenshot that shows VM sizes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/quick-create-portal/create-windows-vm-portal-sizes.png)  

6. <span data-ttu-id="00ee3-123">On the settings blade, select **Yes** under **Use managed disks**, keep the defaults for the rest of the settings, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="00ee3-123">On the settings blade, select **Yes** under **Use managed disks**, keep the defaults for the rest of the settings, and click **OK**.</span></span>

7. <span data-ttu-id="00ee3-124">On the summary page, click **Ok** to start the virtual machine deployment.</span><span class="sxs-lookup"><span data-stu-id="00ee3-124">On the summary page, click **Ok** to start the virtual machine deployment.</span></span>

8. <span data-ttu-id="00ee3-125">To monitor deployment status, click the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="00ee3-125">To monitor deployment status, click the virtual machine.</span></span> <span data-ttu-id="00ee3-126">The VM can be found on the Azure portal dashboard, or by selecting **Virtual Machines** from the left-hand menu.</span><span class="sxs-lookup"><span data-stu-id="00ee3-126">The VM can be found on the Azure portal dashboard, or by selecting **Virtual Machines** from the left-hand menu.</span></span> <span data-ttu-id="00ee3-127">When the VM has been created, the status changes from **Deploying** to **Running**.</span><span class="sxs-lookup"><span data-stu-id="00ee3-127">When the VM has been created, the status changes from **Deploying** to **Running**.</span></span>

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="00ee3-128">Open port 80 for web traffic</span><span class="sxs-lookup"><span data-stu-id="00ee3-128">Open port 80 for web traffic</span></span> 

<span data-ttu-id="00ee3-129">To allow traffic for IIS, you need to open port 80 to web traffic.</span><span class="sxs-lookup"><span data-stu-id="00ee3-129">To allow traffic for IIS, you need to open port 80 to web traffic.</span></span> <span data-ttu-id="00ee3-130">This step walks you through creating a network security group (NSG) rule to allow inbound connections on port 80.</span><span class="sxs-lookup"><span data-stu-id="00ee3-130">This step walks you through creating a network security group (NSG) rule to allow inbound connections on port 80.</span></span>

1. <span data-ttu-id="00ee3-131">On the blade for the virtual machine, in the **Essentials** section, click the name of the **Resource group**.</span><span class="sxs-lookup"><span data-stu-id="00ee3-131">On the blade for the virtual machine, in the **Essentials** section, click the name of the **Resource group**.</span></span>
2. <span data-ttu-id="00ee3-132">In the blade for the resource group, click the **Network security group** in the list of resources.</span><span class="sxs-lookup"><span data-stu-id="00ee3-132">In the blade for the resource group, click the **Network security group** in the list of resources.</span></span> <span data-ttu-id="00ee3-133">The NSG name should be the VM name with -nsg appended to the end.</span><span class="sxs-lookup"><span data-stu-id="00ee3-133">The NSG name should be the VM name with -nsg appended to the end.</span></span>
3. <span data-ttu-id="00ee3-134">Click the **Inbound Security Rule** heading to open the list of inbound rules.</span><span class="sxs-lookup"><span data-stu-id="00ee3-134">Click the **Inbound Security Rule** heading to open the list of inbound rules.</span></span> <span data-ttu-id="00ee3-135">You should see a rule for RDP already in the list.</span><span class="sxs-lookup"><span data-stu-id="00ee3-135">You should see a rule for RDP already in the list.</span></span>
4. <span data-ttu-id="00ee3-136">Click **+ Add** to open the **Add inbound security rule** blade.</span><span class="sxs-lookup"><span data-stu-id="00ee3-136">Click **+ Add** to open the **Add inbound security rule** blade.</span></span>
5. <span data-ttu-id="00ee3-137">In **Name**, type **IIS**.</span><span class="sxs-lookup"><span data-stu-id="00ee3-137">In **Name**, type **IIS**.</span></span> <span data-ttu-id="00ee3-138">Make sure **Port range** is set to 80 and **Action** is set to **Allow**.</span><span class="sxs-lookup"><span data-stu-id="00ee3-138">Make sure **Port range** is set to 80 and **Action** is set to **Allow**.</span></span> <span data-ttu-id="00ee3-139">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="00ee3-139">Click **OK**.</span></span>


## <a name="connect-to-virtual-machine"></a><span data-ttu-id="00ee3-140">Connect to virtual machine</span><span class="sxs-lookup"><span data-stu-id="00ee3-140">Connect to virtual machine</span></span>

<span data-ttu-id="00ee3-141">After the deployment has completed, create a remote desktop connection to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="00ee3-141">After the deployment has completed, create a remote desktop connection to the virtual machine.</span></span>

1. <span data-ttu-id="00ee3-142">Click the **Connect** button on the virtual machine blade.</span><span class="sxs-lookup"><span data-stu-id="00ee3-142">Click the **Connect** button on the virtual machine blade.</span></span> <span data-ttu-id="00ee3-143">A Remote Desktop Protocol file (.rdp file) is created and downloaded.</span><span class="sxs-lookup"><span data-stu-id="00ee3-143">A Remote Desktop Protocol file (.rdp file) is created and downloaded.</span></span>

    ![Portal 9](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/quick-create-portal/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="00ee3-145">To connect to your VM, open the downloaded RDP file.</span><span class="sxs-lookup"><span data-stu-id="00ee3-145">To connect to your VM, open the downloaded RDP file.</span></span> <span data-ttu-id="00ee3-146">If prompted, click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="00ee3-146">If prompted, click **Connect**.</span></span> <span data-ttu-id="00ee3-147">On a Mac, you need an RDP client such as this [Remote Desktop Client](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) from the Mac App Store.</span><span class="sxs-lookup"><span data-stu-id="00ee3-147">On a Mac, you need an RDP client such as this [Remote Desktop Client](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) from the Mac App Store.</span></span>

3. <span data-ttu-id="00ee3-148">Enter the user name and password you specified when creating the virtual machine, then click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="00ee3-148">Enter the user name and password you specified when creating the virtual machine, then click **Ok**.</span></span>

4. <span data-ttu-id="00ee3-149">You may receive a certificate warning during the sign-in process.</span><span class="sxs-lookup"><span data-stu-id="00ee3-149">You may receive a certificate warning during the sign-in process.</span></span> <span data-ttu-id="00ee3-150">Click **Yes** or **Continue** to proceed with the connection.</span><span class="sxs-lookup"><span data-stu-id="00ee3-150">Click **Yes** or **Continue** to proceed with the connection.</span></span>


## <a name="install-iis-using-powershell"></a><span data-ttu-id="00ee3-151">Install IIS using PowerShell</span><span class="sxs-lookup"><span data-stu-id="00ee3-151">Install IIS using PowerShell</span></span>

<span data-ttu-id="00ee3-152">On the virtual machine, open a PowerShell prompt and run the following command to install IIS and enable the local firewall rule to allow web traffic:</span><span class="sxs-lookup"><span data-stu-id="00ee3-152">On the virtual machine, open a PowerShell prompt and run the following command to install IIS and enable the local firewall rule to allow web traffic:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="00ee3-153">View the IIS welcome page</span><span class="sxs-lookup"><span data-stu-id="00ee3-153">View the IIS welcome page</span></span>

<span data-ttu-id="00ee3-154">With IIS installed and port 80 now open on your VM from the Internet, you can use a web browser of your choice to view the default IIS welcome page.</span><span class="sxs-lookup"><span data-stu-id="00ee3-154">With IIS installed and port 80 now open on your VM from the Internet, you can use a web browser of your choice to view the default IIS welcome page.</span></span> <span data-ttu-id="00ee3-155">Get the **Public IP address** from the blade for the VM and use it to visit the default web page.</span><span class="sxs-lookup"><span data-stu-id="00ee3-155">Get the **Public IP address** from the blade for the VM and use it to visit the default web page.</span></span> 

![IIS default site](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/quick-create-powershell/default-iis-website.png) 

## <a name="delete-virtual-machine"></a><span data-ttu-id="00ee3-157">Delete virtual machine</span><span class="sxs-lookup"><span data-stu-id="00ee3-157">Delete virtual machine</span></span>

<span data-ttu-id="00ee3-158">When no longer needed, delete the resource group, virtual machine, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="00ee3-158">When no longer needed, delete the resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="00ee3-159">To do so, select the resource group from the virtual machine blade and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="00ee3-159">To do so, select the resource group from the virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00ee3-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="00ee3-160">Next steps</span></span>

[<span data-ttu-id="00ee3-161">Install a role and configure firewall tutorial</span><span class="sxs-lookup"><span data-stu-id="00ee3-161">Install a role and configure firewall tutorial</span></span>](hero-role.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="00ee3-162">Explore VM deployment CLI samples</span><span class="sxs-lookup"><span data-stu-id="00ee3-162">Explore VM deployment CLI samples</span></span>](cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)




