---
title: Reset an Azure VPN gateway to reestablish IPsec tunnels | Microsoft Docs
description: This article walks you through resetting your Azure VPN Gateway to reestablish IPsec tunnels. The article applies to VPN gateways in both the classic, and the Resource Manager deployment models.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
tags: azure-resource-manager,azure-service-management
ms.assetid: 79d77cb8-d175-4273-93ac-712d7d45b1fe
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: 40075e6f087e14cbfac349243f6858de3204d7be
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552964"
---
# <a name="reset-a-vpn-gateway"></a><span data-ttu-id="2baa8-104">Reset a VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="2baa8-104">Reset a VPN Gateway</span></span>

<span data-ttu-id="2baa8-105">Resetting the Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span><span class="sxs-lookup"><span data-stu-id="2baa8-105">Resetting the Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="2baa8-106">In this situation, your on-premises VPN devices are all working correctly, but are not able to establish IPsec tunnels with the Azure VPN gateways.</span><span class="sxs-lookup"><span data-stu-id="2baa8-106">In this situation, your on-premises VPN devices are all working correctly, but are not able to establish IPsec tunnels with the Azure VPN gateways.</span></span> <span data-ttu-id="2baa8-107">This article walks you through resetting your Azure VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="2baa8-107">This article walks you through resetting your Azure VPN Gateway.</span></span> 

<span data-ttu-id="2baa8-108">Each Azure VPN gateway is a virtual network gateway that is composed of two VM instances running in an active-standby configuration.</span><span class="sxs-lookup"><span data-stu-id="2baa8-108">Each Azure VPN gateway is a virtual network gateway that is composed of two VM instances running in an active-standby configuration.</span></span> <span data-ttu-id="2baa8-109">When you reset the gateway, it reboots the gateway, and then reapplies the cross-premises configurations to it.</span><span class="sxs-lookup"><span data-stu-id="2baa8-109">When you reset the gateway, it reboots the gateway, and then reapplies the cross-premises configurations to it.</span></span> <span data-ttu-id="2baa8-110">The gateway keeps the public IP address it already has.</span><span class="sxs-lookup"><span data-stu-id="2baa8-110">The gateway keeps the public IP address it already has.</span></span> <span data-ttu-id="2baa8-111">This means you won’t need to update the VPN router configuration with a new public IP address for Azure VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="2baa8-111">This means you won’t need to update the VPN router configuration with a new public IP address for Azure VPN gateway.</span></span>  

<span data-ttu-id="2baa8-112">Once the command is issued, the current active instance of the Azure VPN gateway is rebooted immediately.</span><span class="sxs-lookup"><span data-stu-id="2baa8-112">Once the command is issued, the current active instance of the Azure VPN gateway is rebooted immediately.</span></span> <span data-ttu-id="2baa8-113">There will be a brief gap during the failover from the active instance (being rebooted), to the standby instance.</span><span class="sxs-lookup"><span data-stu-id="2baa8-113">There will be a brief gap during the failover from the active instance (being rebooted), to the standby instance.</span></span> <span data-ttu-id="2baa8-114">The gap should be less than one minute.</span><span class="sxs-lookup"><span data-stu-id="2baa8-114">The gap should be less than one minute.</span></span>

<span data-ttu-id="2baa8-115">If the connection is not restored after the first reboot, issue the same command again to reboot the second VM instance (the new active gateway).</span><span class="sxs-lookup"><span data-stu-id="2baa8-115">If the connection is not restored after the first reboot, issue the same command again to reboot the second VM instance (the new active gateway).</span></span> <span data-ttu-id="2baa8-116">If the two reboots are requested back to back, there will be a slightly longer period where both VM instances (active and standby) are being rebooted.</span><span class="sxs-lookup"><span data-stu-id="2baa8-116">If the two reboots are requested back to back, there will be a slightly longer period where both VM instances (active and standby) are being rebooted.</span></span> <span data-ttu-id="2baa8-117">This will cause a longer gap on the VPN connectivity, up to 2 to 4 minutes for VMs to complete the reboots.</span><span class="sxs-lookup"><span data-stu-id="2baa8-117">This will cause a longer gap on the VPN connectivity, up to 2 to 4 minutes for VMs to complete the reboots.</span></span>

<span data-ttu-id="2baa8-118">After two reboots, if you are still experiencing cross-premises connectivity problems, please open a support request from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2baa8-118">After two reboots, if you are still experiencing cross-premises connectivity problems, please open a support request from the Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2baa8-119">Before you begin</span><span class="sxs-lookup"><span data-stu-id="2baa8-119">Before you begin</span></span>
<span data-ttu-id="2baa8-120">Before you reset your gateway, verify the key items listed below for each IPsec Site-to-Site (S2S) VPN tunnel.</span><span class="sxs-lookup"><span data-stu-id="2baa8-120">Before you reset your gateway, verify the key items listed below for each IPsec Site-to-Site (S2S) VPN tunnel.</span></span> <span data-ttu-id="2baa8-121">Any mismatch in the items will result in the disconnect of S2S VPN tunnels.</span><span class="sxs-lookup"><span data-stu-id="2baa8-121">Any mismatch in the items will result in the disconnect of S2S VPN tunnels.</span></span> <span data-ttu-id="2baa8-122">Verifying and correcting the configurations for your on-premises and Azure VPN gateways saves you from unnecessary reboots and disruptions for the other working connections on the gateways.</span><span class="sxs-lookup"><span data-stu-id="2baa8-122">Verifying and correcting the configurations for your on-premises and Azure VPN gateways saves you from unnecessary reboots and disruptions for the other working connections on the gateways.</span></span>

<span data-ttu-id="2baa8-123">Verify the following items before resetting your gateway:</span><span class="sxs-lookup"><span data-stu-id="2baa8-123">Verify the following items before resetting your gateway:</span></span>

* <span data-ttu-id="2baa8-124">The Internet IP addresses (VIPs) for both the Azure VPN gateway and the on-premises VPN gateway are configured correctly in both the Azure and the on-premises VPN policies.</span><span class="sxs-lookup"><span data-stu-id="2baa8-124">The Internet IP addresses (VIPs) for both the Azure VPN gateway and the on-premises VPN gateway are configured correctly in both the Azure and the on-premises VPN policies.</span></span>
* <span data-ttu-id="2baa8-125">The pre-shared key must be the same on both Azure and on-premises VPN gateways.</span><span class="sxs-lookup"><span data-stu-id="2baa8-125">The pre-shared key must be the same on both Azure and on-premises VPN gateways.</span></span>
* <span data-ttu-id="2baa8-126">If you apply specific IPsec/IKE configuration, such as encryption, hashing algorithms, and PFS (Perfect Forward Secrecy), ensure both the Azure and on-premises VPN gateways have the same configurations.</span><span class="sxs-lookup"><span data-stu-id="2baa8-126">If you apply specific IPsec/IKE configuration, such as encryption, hashing algorithms, and PFS (Perfect Forward Secrecy), ensure both the Azure and on-premises VPN gateways have the same configurations.</span></span>

## <a name="reset-a-vpn-gateway-using-the-azure-portal"></a><span data-ttu-id="2baa8-127">Reset a VPN Gateway using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="2baa8-127">Reset a VPN Gateway using the Azure portal</span></span>

<span data-ttu-id="2baa8-128">You can reset a Resource Manager VPN gateway using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2baa8-128">You can reset a Resource Manager VPN gateway using the Azure portal.</span></span> <span data-ttu-id="2baa8-129">If you want to reset a classic gateway, see the [PowerShell](#resetclassic) steps.</span><span class="sxs-lookup"><span data-stu-id="2baa8-129">If you want to reset a classic gateway, see the [PowerShell](#resetclassic) steps.</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="2baa8-130">Resource Manager deployment model</span><span class="sxs-lookup"><span data-stu-id="2baa8-130">Resource Manager deployment model</span></span>

1. <span data-ttu-id="2baa8-131">Open the Azure portal and navigate to the Resource Manager virtual network gateway that you want to reset.</span><span class="sxs-lookup"><span data-stu-id="2baa8-131">Open the Azure portal and navigate to the Resource Manager virtual network gateway that you want to reset.</span></span>
2. <span data-ttu-id="2baa8-132">On the blade for the virtual network gateway, click 'Reset'.</span><span class="sxs-lookup"><span data-stu-id="2baa8-132">On the blade for the virtual network gateway, click 'Reset'.</span></span>

    ![Reset VPN Gateway blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)

3. <span data-ttu-id="2baa8-134">On the Reset blade, click the</span><span class="sxs-lookup"><span data-stu-id="2baa8-134">On the Reset blade, click the</span></span> ![Reset VPN Gateway blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-howto-reset-gateway/reset-button.png) <span data-ttu-id="2baa8-136">button.</span><span class="sxs-lookup"><span data-stu-id="2baa8-136">button.</span></span>


## <a name="reset-a-vpn-gateway-using-powershell"></a><span data-ttu-id="2baa8-137">Reset a VPN Gateway using PowerShell</span><span class="sxs-lookup"><span data-stu-id="2baa8-137">Reset a VPN Gateway using PowerShell</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="2baa8-138">Resource Manager deployment model</span><span class="sxs-lookup"><span data-stu-id="2baa8-138">Resource Manager deployment model</span></span>

<span data-ttu-id="2baa8-139">You'll need the latest version of the PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="2baa8-139">You'll need the latest version of the PowerShell cmdlets.</span></span> <span data-ttu-id="2baa8-140">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information.</span><span class="sxs-lookup"><span data-stu-id="2baa8-140">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information.</span></span> <span data-ttu-id="2baa8-141">The PowerShell Resource Manager cmdlet for resetting gateway is `Reset-AzureRmVirtualNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="2baa8-141">The PowerShell Resource Manager cmdlet for resetting gateway is `Reset-AzureRmVirtualNetworkGateway`.</span></span> <span data-ttu-id="2baa8-142">The following example resets the Azure VPN gateway, "VNet1GW", in resource group "TestRG1".</span><span class="sxs-lookup"><span data-stu-id="2baa8-142">The following example resets the Azure VPN gateway, "VNet1GW", in resource group "TestRG1".</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

### <a name="resetclassic"></a><span data-ttu-id="2baa8-143">Classic deployment model</span><span class="sxs-lookup"><span data-stu-id="2baa8-143">Classic deployment model</span></span>

<span data-ttu-id="2baa8-144">You'll need the latest version of the PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="2baa8-144">You'll need the latest version of the PowerShell cmdlets.</span></span> <span data-ttu-id="2baa8-145">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information.</span><span class="sxs-lookup"><span data-stu-id="2baa8-145">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information.</span></span> <span data-ttu-id="2baa8-146">The PowerShell cmdlet for resetting Azure VPN gateway is **Reset-AzureVNetGateway**.</span><span class="sxs-lookup"><span data-stu-id="2baa8-146">The PowerShell cmdlet for resetting Azure VPN gateway is **Reset-AzureVNetGateway**.</span></span> <span data-ttu-id="2baa8-147">The following example resets the Azure VPN gateway for the virtual network called "ContosoVNet".</span><span class="sxs-lookup"><span data-stu-id="2baa8-147">The following example resets the Azure VPN gateway for the virtual network called "ContosoVNet".</span></span>

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
``` 

<span data-ttu-id="2baa8-148">Result:</span><span class="sxs-lookup"><span data-stu-id="2baa8-148">Result:</span></span>

    Error          :
    HttpStatusCode : OK
    Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
    Status         : Successful
    RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
    StatusCode     : OK




