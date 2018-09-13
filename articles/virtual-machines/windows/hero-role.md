---
title: Install IIS on your first Windows VM | Microsoft Docs
description: Experiment with your first Windows virtual machine by installing IIS and opening port 80 using the Azure portal.
keywords: ''
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 6334ea45-db6b-4e08-abb5-1f98927ebc34
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cynthn
ms.openlocfilehash: ab7a1b5268293c1e4167f1933358d9881fd6e46b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661734"
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a><span data-ttu-id="8f4da-103">Experiment with installing a role on your Windows VM</span><span class="sxs-lookup"><span data-stu-id="8f4da-103">Experiment with installing a role on your Windows VM</span></span>
<span data-ttu-id="8f4da-104">Once you have your first virtual machine (VM) up and running, you can move on to installing software and services.</span><span class="sxs-lookup"><span data-stu-id="8f4da-104">Once you have your first virtual machine (VM) up and running, you can move on to installing software and services.</span></span> <span data-ttu-id="8f4da-105">For this tutorial, we are going to use Server Manager on the Windows Server VM to install IIS.</span><span class="sxs-lookup"><span data-stu-id="8f4da-105">For this tutorial, we are going to use Server Manager on the Windows Server VM to install IIS.</span></span> <span data-ttu-id="8f4da-106">Then, we will create a Network Security Group (NSG) using the Azure portal to open port 80 to IIS traffic.</span><span class="sxs-lookup"><span data-stu-id="8f4da-106">Then, we will create a Network Security Group (NSG) using the Azure portal to open port 80 to IIS traffic.</span></span> 

<span data-ttu-id="8f4da-107">If you haven't already created your first VM, you should go back to [Create your first Windows virtual machine in the Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before continuing with this tutorial.</span><span class="sxs-lookup"><span data-stu-id="8f4da-107">If you haven't already created your first VM, you should go back to [Create your first Windows virtual machine in the Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before continuing with this tutorial.</span></span>

## <a name="make-sure-the-vm-is-running"></a><span data-ttu-id="8f4da-108">Make sure the VM is running</span><span class="sxs-lookup"><span data-stu-id="8f4da-108">Make sure the VM is running</span></span>
1. <span data-ttu-id="8f4da-109">Open the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8f4da-109">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8f4da-110">On the hub menu, click **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="8f4da-110">On the hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="8f4da-111">Select the virtual machine from the list.</span><span class="sxs-lookup"><span data-stu-id="8f4da-111">Select the virtual machine from the list.</span></span>
3. <span data-ttu-id="8f4da-112">If the status is **Stopped (Deallocated)**, click the **Start** button on the **Essentials** blade of the VM.</span><span class="sxs-lookup"><span data-stu-id="8f4da-112">If the status is **Stopped (Deallocated)**, click the **Start** button on the **Essentials** blade of the VM.</span></span> <span data-ttu-id="8f4da-113">If the status is **Running**, you can move on to the next step.</span><span class="sxs-lookup"><span data-stu-id="8f4da-113">If the status is **Running**, you can move on to the next step.</span></span>

## <a name="connect-to-the-virtual-machine-and-sign-in"></a><span data-ttu-id="8f4da-114">Connect to the virtual machine and sign in</span><span class="sxs-lookup"><span data-stu-id="8f4da-114">Connect to the virtual machine and sign in</span></span>
1. <span data-ttu-id="8f4da-115">On the hub menu, click **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="8f4da-115">On the hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="8f4da-116">Select the virtual machine from the list.</span><span class="sxs-lookup"><span data-stu-id="8f4da-116">Select the virtual machine from the list.</span></span>
2. <span data-ttu-id="8f4da-117">On the blade for the virtual machine, click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="8f4da-117">On the blade for the virtual machine, click **Connect**.</span></span> <span data-ttu-id="8f4da-118">This creates and downloads a Remote Desktop Protocol file (.rdp file) that is like a shortcut to connect to your machine.</span><span class="sxs-lookup"><span data-stu-id="8f4da-118">This creates and downloads a Remote Desktop Protocol file (.rdp file) that is like a shortcut to connect to your machine.</span></span> <span data-ttu-id="8f4da-119">You might want to save the file to your desktop for easy access.</span><span class="sxs-lookup"><span data-stu-id="8f4da-119">You might want to save the file to your desktop for easy access.</span></span> <span data-ttu-id="8f4da-120">**Open** this file to connect to your VM.</span><span class="sxs-lookup"><span data-stu-id="8f4da-120">**Open** this file to connect to your VM.</span></span>
   
    ![Screenshot of the Azure portal showing how to connect to your VM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/hero-role/connect.png)
3. <span data-ttu-id="8f4da-122">You get a warning that the .rdp is from an unknown publisher.</span><span class="sxs-lookup"><span data-stu-id="8f4da-122">You get a warning that the .rdp is from an unknown publisher.</span></span> <span data-ttu-id="8f4da-123">This is normal.</span><span class="sxs-lookup"><span data-stu-id="8f4da-123">This is normal.</span></span> <span data-ttu-id="8f4da-124">In the Remote Desktop window, click **Connect** to continue.</span><span class="sxs-lookup"><span data-stu-id="8f4da-124">In the Remote Desktop window, click **Connect** to continue.</span></span>
   
    ![Screenshot of a warning about an unknown publisher](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/hero-role/rdp-warn.png)
4. <span data-ttu-id="8f4da-126">In the Windows Security window, type the username and password for the local account that you created when you created the VM.</span><span class="sxs-lookup"><span data-stu-id="8f4da-126">In the Windows Security window, type the username and password for the local account that you created when you created the VM.</span></span> <span data-ttu-id="8f4da-127">The username is entered as *vmname*&#92;*username*, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8f4da-127">The username is entered as *vmname*&#92;*username*, then click **OK**.</span></span>
   
    ![Screenshot of entering the VM name, user name, and password](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/hero-role/credentials.png)
5. <span data-ttu-id="8f4da-129">You get a warning that the certificate cannot be verified.</span><span class="sxs-lookup"><span data-stu-id="8f4da-129">You get a warning that the certificate cannot be verified.</span></span> <span data-ttu-id="8f4da-130">This is normal.</span><span class="sxs-lookup"><span data-stu-id="8f4da-130">This is normal.</span></span> <span data-ttu-id="8f4da-131">Click **Yes** to verify the identity of the virtual machine and finish logging on.</span><span class="sxs-lookup"><span data-stu-id="8f4da-131">Click **Yes** to verify the identity of the virtual machine and finish logging on.</span></span>
   
   ![Screenshot showing a message abut verifying the identity of the VM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/hero-role/cert-warning.png)

<span data-ttu-id="8f4da-133">If you run in to trouble when you try to connect, see [Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f4da-133">If you run in to trouble when you try to connect, see [Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="install-iis-on-your-vm"></a><span data-ttu-id="8f4da-134">Install IIS on your VM</span><span class="sxs-lookup"><span data-stu-id="8f4da-134">Install IIS on your VM</span></span>
<span data-ttu-id="8f4da-135">Now that you are logged in to the VM, we will install a server role so that you can experiment more.</span><span class="sxs-lookup"><span data-stu-id="8f4da-135">Now that you are logged in to the VM, we will install a server role so that you can experiment more.</span></span>

1. <span data-ttu-id="8f4da-136">Open **Server Manager** if it isn't already open.</span><span class="sxs-lookup"><span data-stu-id="8f4da-136">Open **Server Manager** if it isn't already open.</span></span> <span data-ttu-id="8f4da-137">Click the **Start** menu, and then click **Server Manager**.</span><span class="sxs-lookup"><span data-stu-id="8f4da-137">Click the **Start** menu, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="8f4da-138">In **Server Manager**, select **Local Server** from the left pane.</span><span class="sxs-lookup"><span data-stu-id="8f4da-138">In **Server Manager**, select **Local Server** from the left pane.</span></span> 
3. <span data-ttu-id="8f4da-139">In the menu, select **Manage** > **Add Roles and Features**.</span><span class="sxs-lookup"><span data-stu-id="8f4da-139">In the menu, select **Manage** > **Add Roles and Features**.</span></span>
4. <span data-ttu-id="8f4da-140">In the Add Roles and Features Wizard, on the **Installation Type** page, choose **Role-based or feature-based installation**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8f4da-140">In the Add Roles and Features Wizard, on the **Installation Type** page, choose **Role-based or feature-based installation**, and then click **Next**.</span></span>
   
    ![Screenshot showing the Add Roles and Features Wizard tab for Installation Type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/hero-role/role-wizard.png)
5. <span data-ttu-id="8f4da-142">Select the VM from the server pool and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8f4da-142">Select the VM from the server pool and click **Next**.</span></span>
6. <span data-ttu-id="8f4da-143">On the **Server Roles** page, select **Web Server (IIS)**.</span><span class="sxs-lookup"><span data-stu-id="8f4da-143">On the **Server Roles** page, select **Web Server (IIS)**.</span></span>
   
    ![Screenshot showing the Add Roles and Features Wizard tab for Server Roles](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/hero-role/add-iis.png)
7. <span data-ttu-id="8f4da-145">In the pop-up about adding features needed for IIS, make sure that **Include management tools** is selected and then click **Add Features**.</span><span class="sxs-lookup"><span data-stu-id="8f4da-145">In the pop-up about adding features needed for IIS, make sure that **Include management tools** is selected and then click **Add Features**.</span></span> <span data-ttu-id="8f4da-146">When the pop-up closes, click **Next** in the wizard.</span><span class="sxs-lookup"><span data-stu-id="8f4da-146">When the pop-up closes, click **Next** in the wizard.</span></span>
   
    ![Screenshot showing pop-up to confirm adding the IIS role](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/hero-role/confirm-add-feature.png)
8. <span data-ttu-id="8f4da-148">On the features page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8f4da-148">On the features page, click **Next**.</span></span>
9. <span data-ttu-id="8f4da-149">On the **Web Server Role (IIS)** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8f4da-149">On the **Web Server Role (IIS)** page, click **Next**.</span></span> 
10. <span data-ttu-id="8f4da-150">On the **Role Services** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8f4da-150">On the **Role Services** page, click **Next**.</span></span> 
11. <span data-ttu-id="8f4da-151">On the **Confirmation** page, click **Install**.</span><span class="sxs-lookup"><span data-stu-id="8f4da-151">On the **Confirmation** page, click **Install**.</span></span> 
12. <span data-ttu-id="8f4da-152">When the installation is complete, click **Close** on the wizard.</span><span class="sxs-lookup"><span data-stu-id="8f4da-152">When the installation is complete, click **Close** on the wizard.</span></span>

## <a name="open-port-80"></a><span data-ttu-id="8f4da-153">Open port 80</span><span class="sxs-lookup"><span data-stu-id="8f4da-153">Open port 80</span></span>
<span data-ttu-id="8f4da-154">In order for your VM to accept inbound traffic over port 80, you need to add an inbound rule to the network security group.</span><span class="sxs-lookup"><span data-stu-id="8f4da-154">In order for your VM to accept inbound traffic over port 80, you need to add an inbound rule to the network security group.</span></span> 

1. <span data-ttu-id="8f4da-155">Open the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8f4da-155">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8f4da-156">In **Virtual machines** select the VM that you created.</span><span class="sxs-lookup"><span data-stu-id="8f4da-156">In **Virtual machines** select the VM that you created.</span></span>
3. <span data-ttu-id="8f4da-157">In the virtual machines settings, select **Network interfaces** and then select the existing network interface.</span><span class="sxs-lookup"><span data-stu-id="8f4da-157">In the virtual machines settings, select **Network interfaces** and then select the existing network interface.</span></span>
   
    ![Screenshot showing the virtual machine setting for the network interfaces](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/hero-role/network-interface.png)
4. <span data-ttu-id="8f4da-159">In **Essentials** for the network interface, click the **Network security group**.</span><span class="sxs-lookup"><span data-stu-id="8f4da-159">In **Essentials** for the network interface, click the **Network security group**.</span></span>
   
    ![Screenshot showing the Essentials section for the network interface](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/hero-role/select-nsg.png)
5. <span data-ttu-id="8f4da-161">In the **Essentials** blade for the NSG, you should have one existing default inbound rule for **default-allow-rdp** which allows you to log in to the VM.</span><span class="sxs-lookup"><span data-stu-id="8f4da-161">In the **Essentials** blade for the NSG, you should have one existing default inbound rule for **default-allow-rdp** which allows you to log in to the VM.</span></span> <span data-ttu-id="8f4da-162">You will add another inbound rule to allow IIS traffic.</span><span class="sxs-lookup"><span data-stu-id="8f4da-162">You will add another inbound rule to allow IIS traffic.</span></span> <span data-ttu-id="8f4da-163">Click **Inbound security rule**.</span><span class="sxs-lookup"><span data-stu-id="8f4da-163">Click **Inbound security rule**.</span></span>
   
    ![Screenshot showing the Essentials section for the NSG](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/hero-role/inbound.png)
6. <span data-ttu-id="8f4da-165">In **Inbound security rules**, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="8f4da-165">In **Inbound security rules**, click **Add**.</span></span>
   
    ![Screenshot showing the button to add a security rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/hero-role/add-rule.png)
7. <span data-ttu-id="8f4da-167">In **Inbound security rules**, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="8f4da-167">In **Inbound security rules**, click **Add**.</span></span> <span data-ttu-id="8f4da-168">Type **80** in the port range and make sure **Allow** is selected.</span><span class="sxs-lookup"><span data-stu-id="8f4da-168">Type **80** in the port range and make sure **Allow** is selected.</span></span> <span data-ttu-id="8f4da-169">When you are done, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8f4da-169">When you are done, click **OK**.</span></span>
   
    ![Screenshot showing the button to add a security rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/hero-role/port-80.png)

<span data-ttu-id="8f4da-171">For more information about NSGs, inbound and outbound rules, see [Allow external access to your VM using the Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="8f4da-171">For more information about NSGs, inbound and outbound rules, see [Allow external access to your VM using the Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="connect-to-the-default-iis-website"></a><span data-ttu-id="8f4da-172">Connect to the default IIS website</span><span class="sxs-lookup"><span data-stu-id="8f4da-172">Connect to the default IIS website</span></span>
1. <span data-ttu-id="8f4da-173">In the Azure portal, click **Virtual machines** and then select your VM.</span><span class="sxs-lookup"><span data-stu-id="8f4da-173">In the Azure portal, click **Virtual machines** and then select your VM.</span></span>
2. <span data-ttu-id="8f4da-174">In the **Essentials** blade, copy your **Public IP address**.</span><span class="sxs-lookup"><span data-stu-id="8f4da-174">In the **Essentials** blade, copy your **Public IP address**.</span></span>
   
    ![Screenshot showing where to find the public IP address of your VM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/hero-role/ipaddress.png)
3. <span data-ttu-id="8f4da-176">Open a browser and in the address bar, type in your public IP address like this: http://<publicIPaddress> and click **Enter** to go to that address.</span><span class="sxs-lookup"><span data-stu-id="8f4da-176">Open a browser and in the address bar, type in your public IP address like this: http://<publicIPaddress> and click **Enter** to go to that address.</span></span>
4. <span data-ttu-id="8f4da-177">Your browser should open the default IIS web page.</span><span class="sxs-lookup"><span data-stu-id="8f4da-177">Your browser should open the default IIS web page.</span></span> <span data-ttu-id="8f4da-178">It looks something like this:</span><span class="sxs-lookup"><span data-stu-id="8f4da-178">It looks something like this:</span></span>
   
    ![Screenshot showing what the default IIS page looks like in a browser](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/hero-role/iis-default.png)

## <a name="next-steps"></a><span data-ttu-id="8f4da-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="8f4da-180">Next steps</span></span>
* <span data-ttu-id="8f4da-181">You can also experiment with [attaching a data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8f4da-181">You can also experiment with [attaching a data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to your virtual machine.</span></span> <span data-ttu-id="8f4da-182">Data disks provide more storage for your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8f4da-182">Data disks provide more storage for your virtual machine.</span></span>















