---
title: Cannot connect with RDP to a Windows VM in Azure | Microsoft Docs
description: Troubleshoot issues when you cannot connect to your Windows virtual machine in Azure using Remote Desktop
keywords: Remote desktop error,remote desktop connection error,cannot connect to VM,remote desktop troubleshooting
services: virtual-machines-windows
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 0d740f8e-98b8-4e55-bb02-520f604f5b18
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 291822e473d67c58da73b9fffc605b3a46757ee6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661563"
---
# <a name="troubleshoot-remote-desktop-connections-to-an-azure-virtual-machine"></a><span data-ttu-id="7d428-104">Troubleshoot Remote Desktop connections to an Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="7d428-104">Troubleshoot Remote Desktop connections to an Azure virtual machine</span></span>
<span data-ttu-id="7d428-105">The Remote Desktop Protocol (RDP) connection to your Windows-based Azure virtual machine (VM) can fail for various reasons, leaving you unable to access your VM.</span><span class="sxs-lookup"><span data-stu-id="7d428-105">The Remote Desktop Protocol (RDP) connection to your Windows-based Azure virtual machine (VM) can fail for various reasons, leaving you unable to access your VM.</span></span> <span data-ttu-id="7d428-106">The issue can be with the Remote Desktop service on the VM, the network connection, or the Remote Desktop client on your host computer.</span><span class="sxs-lookup"><span data-stu-id="7d428-106">The issue can be with the Remote Desktop service on the VM, the network connection, or the Remote Desktop client on your host computer.</span></span> <span data-ttu-id="7d428-107">This article guides you through some of the most common methods to resolve RDP connection issues.</span><span class="sxs-lookup"><span data-stu-id="7d428-107">This article guides you through some of the most common methods to resolve RDP connection issues.</span></span> 

<span data-ttu-id="7d428-108">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="7d428-108">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="7d428-109">Alternatively, you can file an Azure support incident.</span><span class="sxs-lookup"><span data-stu-id="7d428-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="7d428-110">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="7d428-110">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

<a id="quickfixrdp"></a>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="7d428-111">Quick troubleshooting steps</span><span class="sxs-lookup"><span data-stu-id="7d428-111">Quick troubleshooting steps</span></span>
<span data-ttu-id="7d428-112">After each troubleshooting step, try reconnecting to the VM:</span><span class="sxs-lookup"><span data-stu-id="7d428-112">After each troubleshooting step, try reconnecting to the VM:</span></span>

1. <span data-ttu-id="7d428-113">Reset Remote Desktop configuration.</span><span class="sxs-lookup"><span data-stu-id="7d428-113">Reset Remote Desktop configuration.</span></span>
2. <span data-ttu-id="7d428-114">Check Network Security Group rules / Cloud Services endpoints.</span><span class="sxs-lookup"><span data-stu-id="7d428-114">Check Network Security Group rules / Cloud Services endpoints.</span></span>
3. <span data-ttu-id="7d428-115">Review VM console logs.</span><span class="sxs-lookup"><span data-stu-id="7d428-115">Review VM console logs.</span></span>
4. <span data-ttu-id="7d428-116">Check the VM Resource Health.</span><span class="sxs-lookup"><span data-stu-id="7d428-116">Check the VM Resource Health.</span></span>
5. <span data-ttu-id="7d428-117">Reset your VM password.</span><span class="sxs-lookup"><span data-stu-id="7d428-117">Reset your VM password.</span></span>
6. <span data-ttu-id="7d428-118">Restart your VM.</span><span class="sxs-lookup"><span data-stu-id="7d428-118">Restart your VM.</span></span>
7. <span data-ttu-id="7d428-119">Redeploy your VM.</span><span class="sxs-lookup"><span data-stu-id="7d428-119">Redeploy your VM.</span></span>

<span data-ttu-id="7d428-120">Continue reading if you need more detailed steps and explanations.</span><span class="sxs-lookup"><span data-stu-id="7d428-120">Continue reading if you need more detailed steps and explanations.</span></span> <span data-ttu-id="7d428-121">Verify that local network equipment such as routers and firewalls are not blocking outbound TCP port 3389, as noted in [detailed RDP troubleshooting scenarios](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7d428-121">Verify that local network equipment such as routers and firewalls are not blocking outbound TCP port 3389, as noted in [detailed RDP troubleshooting scenarios](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!TIP]
> <span data-ttu-id="7d428-122">If the **Connect** button for your VM is grayed out in the portal and you are not connected to Azure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need to create and assign your VM a public IP address before you can use RDP.</span><span class="sxs-lookup"><span data-stu-id="7d428-122">If the **Connect** button for your VM is grayed out in the portal and you are not connected to Azure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need to create and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="7d428-123">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="7d428-123">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>
> 
> 

## <a name="ways-to-troubleshoot-rdp-issues"></a><span data-ttu-id="7d428-124">Ways to troubleshoot RDP issues</span><span class="sxs-lookup"><span data-stu-id="7d428-124">Ways to troubleshoot RDP issues</span></span>
<span data-ttu-id="7d428-125">You can troubleshoot VMs created using the Resource Manager deployment model by using one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="7d428-125">You can troubleshoot VMs created using the Resource Manager deployment model by using one of the following methods:</span></span>

* <span data-ttu-id="7d428-126">[Azure portal](#using-the-azure-portal) - great if you need to quickly reset the RDP configuration or user credentials and you don't have the Azure tools installed.</span><span class="sxs-lookup"><span data-stu-id="7d428-126">[Azure portal](#using-the-azure-portal) - great if you need to quickly reset the RDP configuration or user credentials and you don't have the Azure tools installed.</span></span>
* <span data-ttu-id="7d428-127">[Azure PowerShell](#using-azure-powershell) - if you are comfortable with a PowerShell prompt, quickly reset the RDP configuration or user credentials using the Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="7d428-127">[Azure PowerShell](#using-azure-powershell) - if you are comfortable with a PowerShell prompt, quickly reset the RDP configuration or user credentials using the Azure PowerShell cmdlets.</span></span>

<span data-ttu-id="7d428-128">You can also find steps on troubleshooting VMs created using the [Classic deployment model](#troubleshoot-vms-created-using-the-classic-deployment-model).</span><span class="sxs-lookup"><span data-stu-id="7d428-128">You can also find steps on troubleshooting VMs created using the [Classic deployment model](#troubleshoot-vms-created-using-the-classic-deployment-model).</span></span>

<a id="fix-common-remote-desktop-errors"></a>

## <a name="troubleshoot-using-the-azure-portal"></a><span data-ttu-id="7d428-129">Troubleshoot using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7d428-129">Troubleshoot using the Azure portal</span></span>
<span data-ttu-id="7d428-130">After each troubleshooting step, try connecting to your VM again.</span><span class="sxs-lookup"><span data-stu-id="7d428-130">After each troubleshooting step, try connecting to your VM again.</span></span> <span data-ttu-id="7d428-131">If you still cannot connect, try the next step.</span><span class="sxs-lookup"><span data-stu-id="7d428-131">If you still cannot connect, try the next step.</span></span>

1. <span data-ttu-id="7d428-132">**Reset your RDP connection**.</span><span class="sxs-lookup"><span data-stu-id="7d428-132">**Reset your RDP connection**.</span></span> <span data-ttu-id="7d428-133">This troubleshooting step resets the RDP configuration when Remote Connections are disabled or Windows Firewall rules are blocking RDP, for example.</span><span class="sxs-lookup"><span data-stu-id="7d428-133">This troubleshooting step resets the RDP configuration when Remote Connections are disabled or Windows Firewall rules are blocking RDP, for example.</span></span>
   
    <span data-ttu-id="7d428-134">Select your VM in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7d428-134">Select your VM in the Azure portal.</span></span> <span data-ttu-id="7d428-135">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span><span class="sxs-lookup"><span data-stu-id="7d428-135">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span></span> <span data-ttu-id="7d428-136">Click the **Reset password** button.</span><span class="sxs-lookup"><span data-stu-id="7d428-136">Click the **Reset password** button.</span></span> <span data-ttu-id="7d428-137">Set the **Mode** to **Reset configuration only** and then click the **Update** button:</span><span class="sxs-lookup"><span data-stu-id="7d428-137">Set the **Mode** to **Reset configuration only** and then click the **Update** button:</span></span>
   
    ![Reset the RDP configuration in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-rdp-connection/reset-rdp.png)
2. <span data-ttu-id="7d428-139">**Verify Network Security Group rules**.</span><span class="sxs-lookup"><span data-stu-id="7d428-139">**Verify Network Security Group rules**.</span></span> <span data-ttu-id="7d428-140">This troubleshooting step verifies that you have a rule in your Network Security Group to permit RDP traffic.</span><span class="sxs-lookup"><span data-stu-id="7d428-140">This troubleshooting step verifies that you have a rule in your Network Security Group to permit RDP traffic.</span></span> <span data-ttu-id="7d428-141">The default port for RDP is TCP port 3389.</span><span class="sxs-lookup"><span data-stu-id="7d428-141">The default port for RDP is TCP port 3389.</span></span> <span data-ttu-id="7d428-142">A rule to permit RDP traffic may not be created automatically when you create your VM.</span><span class="sxs-lookup"><span data-stu-id="7d428-142">A rule to permit RDP traffic may not be created automatically when you create your VM.</span></span>
   
    <span data-ttu-id="7d428-143">Select your VM in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7d428-143">Select your VM in the Azure portal.</span></span> <span data-ttu-id="7d428-144">Click the **Network interfaces** from the settings pane.</span><span class="sxs-lookup"><span data-stu-id="7d428-144">Click the **Network interfaces** from the settings pane.</span></span>
   
    ![View network interfaces for a VM in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-rdp-connection/select-network-interfaces.png)
   
    <span data-ttu-id="7d428-146">Select your network interface from the list (there is typically only one):</span><span class="sxs-lookup"><span data-stu-id="7d428-146">Select your network interface from the list (there is typically only one):</span></span>
   
    ![Select network interface in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-rdp-connection/select-interface.png)
   
    <span data-ttu-id="7d428-148">Select **Network security group** to view the Network Security Group associated with your network interface:</span><span class="sxs-lookup"><span data-stu-id="7d428-148">Select **Network security group** to view the Network Security Group associated with your network interface:</span></span>
   
    ![Select Network Security Group in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-rdp-connection/select-nsg.png)
   
    <span data-ttu-id="7d428-150">Verify that an inbound rule exists that allows RDP traffic on TCP port 3389.</span><span class="sxs-lookup"><span data-stu-id="7d428-150">Verify that an inbound rule exists that allows RDP traffic on TCP port 3389.</span></span> <span data-ttu-id="7d428-151">The following example shows a valid security rule that permits RDP traffic.</span><span class="sxs-lookup"><span data-stu-id="7d428-151">The following example shows a valid security rule that permits RDP traffic.</span></span> <span data-ttu-id="7d428-152">You can see `Service` and `Action` are configured correctly:</span><span class="sxs-lookup"><span data-stu-id="7d428-152">You can see `Service` and `Action` are configured correctly:</span></span>
   
    ![Verify RDP NSG rule in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-rdp-connection/verify-nsg-rules.png)
   
    <span data-ttu-id="7d428-154">If you do not have a rule that allows RDP traffic, [create a Network Security Group rule](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7d428-154">If you do not have a rule that allows RDP traffic, [create a Network Security Group rule](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="7d428-155">Allow TCP port 3389.</span><span class="sxs-lookup"><span data-stu-id="7d428-155">Allow TCP port 3389.</span></span>
3. <span data-ttu-id="7d428-156">**Review VM boot diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="7d428-156">**Review VM boot diagnostics**.</span></span> <span data-ttu-id="7d428-157">This troubleshooting step reviews the VM console logs to determine if the VM is reporting an issue.</span><span class="sxs-lookup"><span data-stu-id="7d428-157">This troubleshooting step reviews the VM console logs to determine if the VM is reporting an issue.</span></span> <span data-ttu-id="7d428-158">Not all VMs have boot diagnostics enabled, so this troubleshooting step may be optional.</span><span class="sxs-lookup"><span data-stu-id="7d428-158">Not all VMs have boot diagnostics enabled, so this troubleshooting step may be optional.</span></span>
   
    <span data-ttu-id="7d428-159">Specific troubleshooting steps are beyond the scope of this article, but may indicate a wider problem that is affecting RDP connectivity.</span><span class="sxs-lookup"><span data-stu-id="7d428-159">Specific troubleshooting steps are beyond the scope of this article, but may indicate a wider problem that is affecting RDP connectivity.</span></span> <span data-ttu-id="7d428-160">For more information on reviewing the console logs and VM screenshot, see [Boot Diagnostics for VMs](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).</span><span class="sxs-lookup"><span data-stu-id="7d428-160">For more information on reviewing the console logs and VM screenshot, see [Boot Diagnostics for VMs](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span>
4. <span data-ttu-id="7d428-161">**Check the VM Resource Health**.</span><span class="sxs-lookup"><span data-stu-id="7d428-161">**Check the VM Resource Health**.</span></span> <span data-ttu-id="7d428-162">This troubleshooting step verifies there are no known issues with the Azure platform that may impact connectivity to the VM.</span><span class="sxs-lookup"><span data-stu-id="7d428-162">This troubleshooting step verifies there are no known issues with the Azure platform that may impact connectivity to the VM.</span></span>
   
    <span data-ttu-id="7d428-163">Select your VM in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7d428-163">Select your VM in the Azure portal.</span></span> <span data-ttu-id="7d428-164">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span><span class="sxs-lookup"><span data-stu-id="7d428-164">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span></span> <span data-ttu-id="7d428-165">Click the **Resource health** button.</span><span class="sxs-lookup"><span data-stu-id="7d428-165">Click the **Resource health** button.</span></span> <span data-ttu-id="7d428-166">A healthy VM reports as being **Available**:</span><span class="sxs-lookup"><span data-stu-id="7d428-166">A healthy VM reports as being **Available**:</span></span>
   
    ![Check VM resource health in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-rdp-connection/check-resource-health.png)
5. <span data-ttu-id="7d428-168">**Reset user credentials**.</span><span class="sxs-lookup"><span data-stu-id="7d428-168">**Reset user credentials**.</span></span> <span data-ttu-id="7d428-169">This troubleshooting step resets the password on a local administrator account when you are unsure or have forgotten the credentials.</span><span class="sxs-lookup"><span data-stu-id="7d428-169">This troubleshooting step resets the password on a local administrator account when you are unsure or have forgotten the credentials.</span></span>
   
    <span data-ttu-id="7d428-170">Select your VM in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7d428-170">Select your VM in the Azure portal.</span></span> <span data-ttu-id="7d428-171">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span><span class="sxs-lookup"><span data-stu-id="7d428-171">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span></span> <span data-ttu-id="7d428-172">Click the **Reset password** button.</span><span class="sxs-lookup"><span data-stu-id="7d428-172">Click the **Reset password** button.</span></span> <span data-ttu-id="7d428-173">Make sure the **Mode** is set to **Reset password** and then enter your username and a new password.</span><span class="sxs-lookup"><span data-stu-id="7d428-173">Make sure the **Mode** is set to **Reset password** and then enter your username and a new password.</span></span> <span data-ttu-id="7d428-174">Finally, click the **Update** button:</span><span class="sxs-lookup"><span data-stu-id="7d428-174">Finally, click the **Update** button:</span></span>
   
    ![Reset the user credentials in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-rdp-connection/reset-password.png)
6. <span data-ttu-id="7d428-176">**Restart your VM**.</span><span class="sxs-lookup"><span data-stu-id="7d428-176">**Restart your VM**.</span></span> <span data-ttu-id="7d428-177">This troubleshooting step can correct any underlying issues the VM itself is having.</span><span class="sxs-lookup"><span data-stu-id="7d428-177">This troubleshooting step can correct any underlying issues the VM itself is having.</span></span>
   
    <span data-ttu-id="7d428-178">Select your VM in the Azure portal and click the **Overview** tab. Click the **Restart** button:</span><span class="sxs-lookup"><span data-stu-id="7d428-178">Select your VM in the Azure portal and click the **Overview** tab. Click the **Restart** button:</span></span>
   
    ![Restart the VM in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-rdp-connection/restart-vm.png)
7. <span data-ttu-id="7d428-180">**Redeploy your VM**.</span><span class="sxs-lookup"><span data-stu-id="7d428-180">**Redeploy your VM**.</span></span> <span data-ttu-id="7d428-181">This troubleshooting step redeploys your VM to another host within Azure to correct any underlying platform or networking issues.</span><span class="sxs-lookup"><span data-stu-id="7d428-181">This troubleshooting step redeploys your VM to another host within Azure to correct any underlying platform or networking issues.</span></span>
   
    <span data-ttu-id="7d428-182">Select your VM in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7d428-182">Select your VM in the Azure portal.</span></span> <span data-ttu-id="7d428-183">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span><span class="sxs-lookup"><span data-stu-id="7d428-183">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span></span> <span data-ttu-id="7d428-184">Click the **Redeploy** button, and then click **Redeploy**:</span><span class="sxs-lookup"><span data-stu-id="7d428-184">Click the **Redeploy** button, and then click **Redeploy**:</span></span>
   
    ![Redeploy the VM in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-rdp-connection/redeploy-vm.png)
   
    <span data-ttu-id="7d428-186">After this operation finishes, ephemeral disk data is lost and dynamic IP addresses that are associated with the VM are updated.</span><span class="sxs-lookup"><span data-stu-id="7d428-186">After this operation finishes, ephemeral disk data is lost and dynamic IP addresses that are associated with the VM are updated.</span></span>

<span data-ttu-id="7d428-187">If you are still encountering RDP issues, you can [open a support request](https://azure.microsoft.com/support/options/) or read [more detailed RDP troubleshooting concepts and steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7d428-187">If you are still encountering RDP issues, you can [open a support request](https://azure.microsoft.com/support/options/) or read [more detailed RDP troubleshooting concepts and steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="troubleshoot-using-azure-powershell"></a><span data-ttu-id="7d428-188">Troubleshoot using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d428-188">Troubleshoot using Azure PowerShell</span></span>
<span data-ttu-id="7d428-189">If you haven't already, [install and configure the latest Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="7d428-189">If you haven't already, [install and configure the latest Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="7d428-190">The following examples use variables such as `myResourceGroup`, `myVM`, and `myVMAccessExtension`.</span><span class="sxs-lookup"><span data-stu-id="7d428-190">The following examples use variables such as `myResourceGroup`, `myVM`, and `myVMAccessExtension`.</span></span> <span data-ttu-id="7d428-191">Replace these variable names and locations with your own values.</span><span class="sxs-lookup"><span data-stu-id="7d428-191">Replace these variable names and locations with your own values.</span></span>

> [!NOTE]
> <span data-ttu-id="7d428-192">You reset the user credentials and the RDP configuration by using the [Set-AzureRmVMAccessExtension](https://msdn.microsoft.com/library/mt619447.aspx) PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7d428-192">You reset the user credentials and the RDP configuration by using the [Set-AzureRmVMAccessExtension](https://msdn.microsoft.com/library/mt619447.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="7d428-193">In the following examples, `myVMAccessExtension` is a name that you specify as part of the process.</span><span class="sxs-lookup"><span data-stu-id="7d428-193">In the following examples, `myVMAccessExtension` is a name that you specify as part of the process.</span></span> <span data-ttu-id="7d428-194">If you have previously worked with the VMAccessAgent, you can get the name of the existing extension by using `Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"` to check the properties of the VM.</span><span class="sxs-lookup"><span data-stu-id="7d428-194">If you have previously worked with the VMAccessAgent, you can get the name of the existing extension by using `Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"` to check the properties of the VM.</span></span> <span data-ttu-id="7d428-195">To view the name, look under the 'Extensions' section of the output.</span><span class="sxs-lookup"><span data-stu-id="7d428-195">To view the name, look under the 'Extensions' section of the output.</span></span>
> 
> 

<span data-ttu-id="7d428-196">After each troubleshooting step, try connecting to your VM again.</span><span class="sxs-lookup"><span data-stu-id="7d428-196">After each troubleshooting step, try connecting to your VM again.</span></span> <span data-ttu-id="7d428-197">If you still cannot connect, try the next step.</span><span class="sxs-lookup"><span data-stu-id="7d428-197">If you still cannot connect, try the next step.</span></span>

1. <span data-ttu-id="7d428-198">**Reset your RDP connection**.</span><span class="sxs-lookup"><span data-stu-id="7d428-198">**Reset your RDP connection**.</span></span> <span data-ttu-id="7d428-199">This troubleshooting step resets the RDP configuration when Remote Connections are disabled or Windows Firewall rules are blocking RDP, for example.</span><span class="sxs-lookup"><span data-stu-id="7d428-199">This troubleshooting step resets the RDP configuration when Remote Connections are disabled or Windows Firewall rules are blocking RDP, for example.</span></span>
   
    <span data-ttu-id="7d428-200">The follow example resets the RDP connection on a VM named `myVM` in the `WestUS` location and in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="7d428-200">The follow example resets the RDP connection on a VM named `myVM` in the `WestUS` location and in the resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location Westus -Name "myVMAccessExtension"
    ```
2. <span data-ttu-id="7d428-201">**Verify Network Security Group rules**.</span><span class="sxs-lookup"><span data-stu-id="7d428-201">**Verify Network Security Group rules**.</span></span> <span data-ttu-id="7d428-202">This troubleshooting step verifies that you have a rule in your Network Security Group to permit RDP traffic.</span><span class="sxs-lookup"><span data-stu-id="7d428-202">This troubleshooting step verifies that you have a rule in your Network Security Group to permit RDP traffic.</span></span> <span data-ttu-id="7d428-203">The default port for RDP is TCP port 3389.</span><span class="sxs-lookup"><span data-stu-id="7d428-203">The default port for RDP is TCP port 3389.</span></span> <span data-ttu-id="7d428-204">A rule to permit RDP traffic may not be created automatically when you create your VM.</span><span class="sxs-lookup"><span data-stu-id="7d428-204">A rule to permit RDP traffic may not be created automatically when you create your VM.</span></span>
   
    <span data-ttu-id="7d428-205">First, assign all the configuration data for your Network Security Group to the `$rules` variable.</span><span class="sxs-lookup"><span data-stu-id="7d428-205">First, assign all the configuration data for your Network Security Group to the `$rules` variable.</span></span> <span data-ttu-id="7d428-206">The following example obtains information about the Network Security Group named `myNetworkSecurityGroup` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="7d428-206">The following example obtains information about the Network Security Group named `myNetworkSecurityGroup` in the resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    $rules = Get-AzureRmNetworkSecurityGroup -ResourceGroupName "myResourceGroup" `
        -Name "myNetworkSecurityGroup"
    ```
   
    <span data-ttu-id="7d428-207">Now, view the rules that are configured for this Network Security Group.</span><span class="sxs-lookup"><span data-stu-id="7d428-207">Now, view the rules that are configured for this Network Security Group.</span></span> <span data-ttu-id="7d428-208">Verify that a rule exists to allow TCP port 3389 for inbound connections as follows:</span><span class="sxs-lookup"><span data-stu-id="7d428-208">Verify that a rule exists to allow TCP port 3389 for inbound connections as follows:</span></span>
   
    ```powershell
    $rules.SecurityRules
    ```
   
    <span data-ttu-id="7d428-209">The following example shows a valid security rule that permits RDP traffic.</span><span class="sxs-lookup"><span data-stu-id="7d428-209">The following example shows a valid security rule that permits RDP traffic.</span></span> <span data-ttu-id="7d428-210">You can see `Protocol`, `DestinationPortRange`, `Access`, and `Direction` are configured correctly:</span><span class="sxs-lookup"><span data-stu-id="7d428-210">You can see `Protocol`, `DestinationPortRange`, `Access`, and `Direction` are configured correctly:</span></span>
   
    ```powershell
    Name                     : default-allow-rdp
    Id                       : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/default-allow-rdp
    Etag                     : 
    ProvisioningState        : Succeeded
    Description              : 
    Protocol                 : TCP
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : *
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 1000
    Direction                : Inbound
    ```
   
    <span data-ttu-id="7d428-211">If you do not have a rule that allows RDP traffic, [create a Network Security Group rule](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7d428-211">If you do not have a rule that allows RDP traffic, [create a Network Security Group rule](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="7d428-212">Allow TCP port 3389.</span><span class="sxs-lookup"><span data-stu-id="7d428-212">Allow TCP port 3389.</span></span>
3. <span data-ttu-id="7d428-213">**Reset user credentials**.</span><span class="sxs-lookup"><span data-stu-id="7d428-213">**Reset user credentials**.</span></span> <span data-ttu-id="7d428-214">This troubleshooting step resets the password on the local administrator account that you specify when you are unsure of, or have forgotten, the credentials.</span><span class="sxs-lookup"><span data-stu-id="7d428-214">This troubleshooting step resets the password on the local administrator account that you specify when you are unsure of, or have forgotten, the credentials.</span></span>
   
    <span data-ttu-id="7d428-215">First, specify the username and a new password by assigning credentials to the `$cred` variable as follows:</span><span class="sxs-lookup"><span data-stu-id="7d428-215">First, specify the username and a new password by assigning credentials to the `$cred` variable as follows:</span></span>
   
    ```powershell
    $cred=Get-Credential
    ```
   
    <span data-ttu-id="7d428-216">Now, update the credentials on your VM.</span><span class="sxs-lookup"><span data-stu-id="7d428-216">Now, update the credentials on your VM.</span></span> <span data-ttu-id="7d428-217">The following example updates the credentials on a VM named `myVM` in the `WestUS` location and in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="7d428-217">The following example updates the credentials on a VM named `myVM` in the `WestUS` location and in the resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location WestUS -Name "myVMAccessExtension" `
        -UserName $cred.GetNetworkCredential().Username `
        -Password $cred.GetNetworkCredential().Password
    ```
4. <span data-ttu-id="7d428-218">**Restart your VM**.</span><span class="sxs-lookup"><span data-stu-id="7d428-218">**Restart your VM**.</span></span> <span data-ttu-id="7d428-219">This troubleshooting step can correct any underlying issues the VM itself is having.</span><span class="sxs-lookup"><span data-stu-id="7d428-219">This troubleshooting step can correct any underlying issues the VM itself is having.</span></span>
   
    <span data-ttu-id="7d428-220">The following example restarts the VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="7d428-220">The following example restarts the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    Restart-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
    ```
5. <span data-ttu-id="7d428-221">**Redeploy your VM**.</span><span class="sxs-lookup"><span data-stu-id="7d428-221">**Redeploy your VM**.</span></span> <span data-ttu-id="7d428-222">This troubleshooting step redeploys your VM to another host within Azure to correct any underlying platform or networking issues.</span><span class="sxs-lookup"><span data-stu-id="7d428-222">This troubleshooting step redeploys your VM to another host within Azure to correct any underlying platform or networking issues.</span></span>
   
    <span data-ttu-id="7d428-223">The following example redeploys the VM named `myVM` in the `WestUS` location and in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="7d428-223">The following example redeploys the VM named `myVM` in the `WestUS` location and in the resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

<span data-ttu-id="7d428-224">If you are still encountering RDP issues, you can [open a support request](https://azure.microsoft.com/support/options/) or read [more detailed RDP troubleshooting concepts and steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7d428-224">If you are still encountering RDP issues, you can [open a support request](https://azure.microsoft.com/support/options/) or read [more detailed RDP troubleshooting concepts and steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="troubleshoot-vms-created-using-the-classic-deployment-model"></a><span data-ttu-id="7d428-225">Troubleshoot VMs created using the Classic deployment model</span><span class="sxs-lookup"><span data-stu-id="7d428-225">Troubleshoot VMs created using the Classic deployment model</span></span>
<span data-ttu-id="7d428-226">After each troubleshooting step, try reconnecting to the VM.</span><span class="sxs-lookup"><span data-stu-id="7d428-226">After each troubleshooting step, try reconnecting to the VM.</span></span>

1. <span data-ttu-id="7d428-227">**Reset your RDP connection**.</span><span class="sxs-lookup"><span data-stu-id="7d428-227">**Reset your RDP connection**.</span></span> <span data-ttu-id="7d428-228">This troubleshooting step resets the RDP configuration when Remote Connections are disabled or Windows Firewall rules are blocking RDP, for example.</span><span class="sxs-lookup"><span data-stu-id="7d428-228">This troubleshooting step resets the RDP configuration when Remote Connections are disabled or Windows Firewall rules are blocking RDP, for example.</span></span>
   
    <span data-ttu-id="7d428-229">Select your VM in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7d428-229">Select your VM in the Azure portal.</span></span> <span data-ttu-id="7d428-230">Click the **...More** button, then click **Reset Remote Access**:</span><span class="sxs-lookup"><span data-stu-id="7d428-230">Click the **...More** button, then click **Reset Remote Access**:</span></span>
   
    ![Reset the RDP configuration in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-rdp-connection/classic-reset-rdp.png)
2. <span data-ttu-id="7d428-232">**Verify Cloud Services endpoints**.</span><span class="sxs-lookup"><span data-stu-id="7d428-232">**Verify Cloud Services endpoints**.</span></span> <span data-ttu-id="7d428-233">This troubleshooting step verifies that you have endpoints in your Cloud Services to permit RDP traffic.</span><span class="sxs-lookup"><span data-stu-id="7d428-233">This troubleshooting step verifies that you have endpoints in your Cloud Services to permit RDP traffic.</span></span> <span data-ttu-id="7d428-234">The default port for RDP is TCP port 3389.</span><span class="sxs-lookup"><span data-stu-id="7d428-234">The default port for RDP is TCP port 3389.</span></span> <span data-ttu-id="7d428-235">A rule to permit RDP traffic may not be created automatically when you create your VM.</span><span class="sxs-lookup"><span data-stu-id="7d428-235">A rule to permit RDP traffic may not be created automatically when you create your VM.</span></span>
   
   <span data-ttu-id="7d428-236">Select your VM in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7d428-236">Select your VM in the Azure portal.</span></span> <span data-ttu-id="7d428-237">Click the **Endpoints** button to view the endpoints currently configured for your VM.</span><span class="sxs-lookup"><span data-stu-id="7d428-237">Click the **Endpoints** button to view the endpoints currently configured for your VM.</span></span> <span data-ttu-id="7d428-238">Verify that endpoints exist that allow RDP traffic on TCP port 3389.</span><span class="sxs-lookup"><span data-stu-id="7d428-238">Verify that endpoints exist that allow RDP traffic on TCP port 3389.</span></span>
   
   <span data-ttu-id="7d428-239">The following example shows valid endpoints that permit RDP traffic:</span><span class="sxs-lookup"><span data-stu-id="7d428-239">The following example shows valid endpoints that permit RDP traffic:</span></span>
   
   ![Verify Cloud Services endpoints in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-rdp-connection/classic-verify-cloud-services-endpoints.png)
   
   <span data-ttu-id="7d428-241">If you do not have an endpoint that allows RDP traffic, [create a Cloud Services endpoint](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7d428-241">If you do not have an endpoint that allows RDP traffic, [create a Cloud Services endpoint](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="7d428-242">Allow TCP to private port 3389.</span><span class="sxs-lookup"><span data-stu-id="7d428-242">Allow TCP to private port 3389.</span></span>
3. <span data-ttu-id="7d428-243">**Review VM boot diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="7d428-243">**Review VM boot diagnostics**.</span></span> <span data-ttu-id="7d428-244">This troubleshooting step reviews the VM console logs to determine if the VM is reporting an issue.</span><span class="sxs-lookup"><span data-stu-id="7d428-244">This troubleshooting step reviews the VM console logs to determine if the VM is reporting an issue.</span></span> <span data-ttu-id="7d428-245">Not all VMs have boot diagnostics enabled, so this troubleshooting step may be optional.</span><span class="sxs-lookup"><span data-stu-id="7d428-245">Not all VMs have boot diagnostics enabled, so this troubleshooting step may be optional.</span></span>
   
    <span data-ttu-id="7d428-246">Specific troubleshooting steps are beyond the scope of this article, but may indicate a wider problem that is affecting RDP connectivity.</span><span class="sxs-lookup"><span data-stu-id="7d428-246">Specific troubleshooting steps are beyond the scope of this article, but may indicate a wider problem that is affecting RDP connectivity.</span></span> <span data-ttu-id="7d428-247">For more information on reviewing the console logs and VM screenshot, see [Boot Diagnostics for VMs](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).</span><span class="sxs-lookup"><span data-stu-id="7d428-247">For more information on reviewing the console logs and VM screenshot, see [Boot Diagnostics for VMs](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span>
4. <span data-ttu-id="7d428-248">**Check the VM Resource Health**.</span><span class="sxs-lookup"><span data-stu-id="7d428-248">**Check the VM Resource Health**.</span></span> <span data-ttu-id="7d428-249">This troubleshooting step verifies there are no known issues with the Azure platform that may impact connectivity to the VM.</span><span class="sxs-lookup"><span data-stu-id="7d428-249">This troubleshooting step verifies there are no known issues with the Azure platform that may impact connectivity to the VM.</span></span>
   
    <span data-ttu-id="7d428-250">Select your VM in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7d428-250">Select your VM in the Azure portal.</span></span> <span data-ttu-id="7d428-251">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span><span class="sxs-lookup"><span data-stu-id="7d428-251">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span></span> <span data-ttu-id="7d428-252">Click the **Resource Health** button.</span><span class="sxs-lookup"><span data-stu-id="7d428-252">Click the **Resource Health** button.</span></span> <span data-ttu-id="7d428-253">A healthy VM reports as being **Available**:</span><span class="sxs-lookup"><span data-stu-id="7d428-253">A healthy VM reports as being **Available**:</span></span>
   
    ![Check VM resource health in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-rdp-connection/classic-check-resource-health.png)
5. <span data-ttu-id="7d428-255">**Reset user credentials**.</span><span class="sxs-lookup"><span data-stu-id="7d428-255">**Reset user credentials**.</span></span> <span data-ttu-id="7d428-256">This troubleshooting step resets the password on the local administrator account that you specify when you are unsure or have forgotten the credentials.</span><span class="sxs-lookup"><span data-stu-id="7d428-256">This troubleshooting step resets the password on the local administrator account that you specify when you are unsure or have forgotten the credentials.</span></span>
   
    <span data-ttu-id="7d428-257">Select your VM in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7d428-257">Select your VM in the Azure portal.</span></span> <span data-ttu-id="7d428-258">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span><span class="sxs-lookup"><span data-stu-id="7d428-258">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span></span> <span data-ttu-id="7d428-259">Click the **Reset password** button.</span><span class="sxs-lookup"><span data-stu-id="7d428-259">Click the **Reset password** button.</span></span> <span data-ttu-id="7d428-260">Enter your username and a new password.</span><span class="sxs-lookup"><span data-stu-id="7d428-260">Enter your username and a new password.</span></span> <span data-ttu-id="7d428-261">Finally, click the **Save** button:</span><span class="sxs-lookup"><span data-stu-id="7d428-261">Finally, click the **Save** button:</span></span>
   
    ![Reset the user credentials in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-rdp-connection/classic-reset-password.png)
6. <span data-ttu-id="7d428-263">**Restart your VM**.</span><span class="sxs-lookup"><span data-stu-id="7d428-263">**Restart your VM**.</span></span> <span data-ttu-id="7d428-264">This troubleshooting step can correct any underlying issues the VM itself is having.</span><span class="sxs-lookup"><span data-stu-id="7d428-264">This troubleshooting step can correct any underlying issues the VM itself is having.</span></span>
   
    <span data-ttu-id="7d428-265">Select your VM in the Azure portal and click the **Overview** tab. Click the **Restart** button:</span><span class="sxs-lookup"><span data-stu-id="7d428-265">Select your VM in the Azure portal and click the **Overview** tab. Click the **Restart** button:</span></span>
   
    ![Restart the VM in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/troubleshoot-rdp-connection/classic-restart-vm.png)

<span data-ttu-id="7d428-267">If you are still encountering RDP issues, you can [open a support request](https://azure.microsoft.com/support/options/) or read [more detailed RDP troubleshooting concepts and steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7d428-267">If you are still encountering RDP issues, you can [open a support request](https://azure.microsoft.com/support/options/) or read [more detailed RDP troubleshooting concepts and steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="troubleshoot-specific-rdp-errors"></a><span data-ttu-id="7d428-268">Troubleshoot specific RDP errors</span><span class="sxs-lookup"><span data-stu-id="7d428-268">Troubleshoot specific RDP errors</span></span>
<span data-ttu-id="7d428-269">You may encounter a specific error message when trying to connect to your VM via RDP.</span><span class="sxs-lookup"><span data-stu-id="7d428-269">You may encounter a specific error message when trying to connect to your VM via RDP.</span></span> <span data-ttu-id="7d428-270">The following are the most common error messages:</span><span class="sxs-lookup"><span data-stu-id="7d428-270">The following are the most common error messages:</span></span>

* <span data-ttu-id="7d428-271">[The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license](troubleshoot-specific-rdp-errors.md#rdplicense).</span><span class="sxs-lookup"><span data-stu-id="7d428-271">[The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license](troubleshoot-specific-rdp-errors.md#rdplicense).</span></span>
* <span data-ttu-id="7d428-272">[Remote Desktop can't find the computer "name"](troubleshoot-specific-rdp-errors.md#rdpname).</span><span class="sxs-lookup"><span data-stu-id="7d428-272">[Remote Desktop can't find the computer "name"](troubleshoot-specific-rdp-errors.md#rdpname).</span></span>
* <span data-ttu-id="7d428-273">[An authentication error has occurred. The Local Security Authority cannot be contacted](troubleshoot-specific-rdp-errors.md#rdpauth).</span><span class="sxs-lookup"><span data-stu-id="7d428-273">[An authentication error has occurred. The Local Security Authority cannot be contacted](troubleshoot-specific-rdp-errors.md#rdpauth).</span></span>
* <span data-ttu-id="7d428-274">[Windows Security error: Your credentials did not work](troubleshoot-specific-rdp-errors.md#wincred).</span><span class="sxs-lookup"><span data-stu-id="7d428-274">[Windows Security error: Your credentials did not work](troubleshoot-specific-rdp-errors.md#wincred).</span></span>
* <span data-ttu-id="7d428-275">[This computer can't connect to the remote computer](troubleshoot-specific-rdp-errors.md#rdpconnect).</span><span class="sxs-lookup"><span data-stu-id="7d428-275">[This computer can't connect to the remote computer](troubleshoot-specific-rdp-errors.md#rdpconnect).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7d428-276">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7d428-276">Additional resources</span></span>
<span data-ttu-id="7d428-277">If none of these errors occurred and you still can't connect to the VM via Remote Desktop, read the detailed [troubleshooting guide for Remote Desktop](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7d428-277">If none of these errors occurred and you still can't connect to the VM via Remote Desktop, read the detailed [troubleshooting guide for Remote Desktop](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="7d428-278">For troubleshooting steps in accessing applications running on a VM, see [Troubleshoot access to an application running on an Azure VM](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7d428-278">For troubleshooting steps in accessing applications running on a VM, see [Troubleshoot access to an application running on an Azure VM](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="7d428-279">If you are having issues using Secure Shell (SSH) to connect to a Linux VM in Azure, see [Troubleshoot SSH connections to a Linux VM in Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7d428-279">If you are having issues using Secure Shell (SSH) to connect to a Linux VM in Azure, see [Troubleshoot SSH connections to a Linux VM in Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>















