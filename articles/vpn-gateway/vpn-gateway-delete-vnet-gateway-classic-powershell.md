---
title: 'Delete a virtual network gateway: PowerShell: Azure classic | Microsoft Docs'
description: Delete a virtual network gateway using PowerShell in the classic deployment model.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: ''
ms.service: vpn-gateway
ms.devlang: na
ms.topic: ''
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: cherylmc
ms.openlocfilehash: 4437c8cb9f428bea54505dc4949410d361f77c11
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564007"
---
# <a name="delete-a-virtual-network-gateway-using-powershell-classic"></a><span data-ttu-id="3e2f8-103">Delete a virtual network gateway using PowerShell (classic)</span><span class="sxs-lookup"><span data-stu-id="3e2f8-103">Delete a virtual network gateway using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager - Azure portal](vpn-gateway-delete-vnet-gateway-portal.md)
> * [Resource Manager - PowerShell](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [Classic - PowerShell](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="3e2f8-107">You can delete a VPN gateway in the classic deployment model by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-107">You can delete a VPN gateway in the classic deployment model by using PowerShell.</span></span> <span data-ttu-id="3e2f8-108">After the virtual network gateway has been deleted, modify the network configuration file to remove elements that you are no longer using.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-108">After the virtual network gateway has been deleted, modify the network configuration file to remove elements that you are no longer using.</span></span>

##<a name="step-1-connect-to-azure"></a><span data-ttu-id="3e2f8-109">Step 1: Connect to Azure</span><span class="sxs-lookup"><span data-stu-id="3e2f8-109">Step 1: Connect to Azure</span></span>

### <a name="1-install-the-latest-powershell-cmdlets"></a><span data-ttu-id="3e2f8-110">1. Install the latest PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-110">1. Install the latest PowerShell cmdlets.</span></span>

<span data-ttu-id="3e2f8-111">Download and install the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-111">Download and install the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="3e2f8-112">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="3e2f8-112">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="3e2f8-113">2. Connect to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-113">2. Connect to your Azure account.</span></span> 

<span data-ttu-id="3e2f8-114">Open your PowerShell console with elevated rights and connect to your account.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-114">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="3e2f8-115">Use the following example to help you connect:</span><span class="sxs-lookup"><span data-stu-id="3e2f8-115">Use the following example to help you connect:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="3e2f8-116">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-116">Check the subscriptions for the account.</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="3e2f8-117">If you have more than one subscription, select the subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-117">If you have more than one subscription, select the subscription that you want to use.</span></span>

    Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

<span data-ttu-id="3e2f8-118">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-118">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span></span>

    Add-AzureAccount

## <a name="step-2-export-and-view-the-network-configuration-file"></a><span data-ttu-id="3e2f8-119">Step 2: Export and view the network configuration file</span><span class="sxs-lookup"><span data-stu-id="3e2f8-119">Step 2: Export and view the network configuration file</span></span>

<span data-ttu-id="3e2f8-120">Create a directory on your computer and then export the network configuration file to the directory.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-120">Create a directory on your computer and then export the network configuration file to the directory.</span></span> <span data-ttu-id="3e2f8-121">You use this file to both view the current configuration information, and also to modify the network configuration.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-121">You use this file to both view the current configuration information, and also to modify the network configuration.</span></span>

<span data-ttu-id="3e2f8-122">In this example, the network configuration file is exported to C:\AzureNet.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-122">In this example, the network configuration file is exported to C:\AzureNet.</span></span>

     Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml

<span data-ttu-id="3e2f8-123">Open the file with a text editor and view the name for your classic VNet.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-123">Open the file with a text editor and view the name for your classic VNet.</span></span> <span data-ttu-id="3e2f8-124">When you create a VNet in the Azure portal, the full name that Azure uses is not visible in the portal.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-124">When you create a VNet in the Azure portal, the full name that Azure uses is not visible in the portal.</span></span> <span data-ttu-id="3e2f8-125">For example, a VNet that appears to be named 'ClassicVNet1' in the Azure portal, may have a much longer name in the network configuration file.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-125">For example, a VNet that appears to be named 'ClassicVNet1' in the Azure portal, may have a much longer name in the network configuration file.</span></span> <span data-ttu-id="3e2f8-126">The name might look something like: 'Group ClassicRG1 ClassicVNet1'.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-126">The name might look something like: 'Group ClassicRG1 ClassicVNet1'.</span></span> <span data-ttu-id="3e2f8-127">Virtual network names are listed as **VirtualNetworkSite name =**.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-127">Virtual network names are listed as **VirtualNetworkSite name =**.</span></span> <span data-ttu-id="3e2f8-128">Use the names in the network configuration file when running your PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-128">Use the names in the network configuration file when running your PowerShell cmdlets.</span></span>

## <a name="step-3-delete-the-virtual-network-gateway"></a><span data-ttu-id="3e2f8-129">Step 3: Delete the virtual network gateway</span><span class="sxs-lookup"><span data-stu-id="3e2f8-129">Step 3: Delete the virtual network gateway</span></span>

<span data-ttu-id="3e2f8-130">When you delete a virtual network gateway, all connections to the VNet through the gateway are disconnected.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-130">When you delete a virtual network gateway, all connections to the VNet through the gateway are disconnected.</span></span> <span data-ttu-id="3e2f8-131">If you have P2S clients connected to the VNet, they will be disconnected without warning.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-131">If you have P2S clients connected to the VNet, they will be disconnected without warning.</span></span>

<span data-ttu-id="3e2f8-132">This example deletes the virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-132">This example deletes the virtual network gateway.</span></span> <span data-ttu-id="3e2f8-133">Make sure to use the full name of the virtual network from the network configuration file.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-133">Make sure to use the full name of the virtual network from the network configuration file.</span></span>

    Remove-AzureVNetGateway -VNetName "Group ClassicRG1 ClassicVNet1"

<span data-ttu-id="3e2f8-134">If successful, the return shows:</span><span class="sxs-lookup"><span data-stu-id="3e2f8-134">If successful, the return shows:</span></span>

    Status : Successful

## <a name="step-4-modify-the-network-configuration-file"></a><span data-ttu-id="3e2f8-135">Step 4: Modify the network configuration file</span><span class="sxs-lookup"><span data-stu-id="3e2f8-135">Step 4: Modify the network configuration file</span></span>

<span data-ttu-id="3e2f8-136">When you delete a virtual network gateway, the cmdlet does not modify the network configuration file.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-136">When you delete a virtual network gateway, the cmdlet does not modify the network configuration file.</span></span> <span data-ttu-id="3e2f8-137">You need to modify the file to remove the elements that are no longer being used.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-137">You need to modify the file to remove the elements that are no longer being used.</span></span> <span data-ttu-id="3e2f8-138">The following sections help you modify the network configuration file that you downloaded.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-138">The following sections help you modify the network configuration file that you downloaded.</span></span>

###<a name="local-network-site-references"></a><span data-ttu-id="3e2f8-139">Local Network Site References</span><span class="sxs-lookup"><span data-stu-id="3e2f8-139">Local Network Site References</span></span>

<span data-ttu-id="3e2f8-140">To remove site reference information, make configuration changes to **ConnectionsToLocalNetwork/LocalNetworkSiteRef**.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-140">To remove site reference information, make configuration changes to **ConnectionsToLocalNetwork/LocalNetworkSiteRef**.</span></span> <span data-ttu-id="3e2f8-141">Removing a local site reference triggers Azure to delete a tunnel.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-141">Removing a local site reference triggers Azure to delete a tunnel.</span></span> <span data-ttu-id="3e2f8-142">Depending on the configuration that you created, you may not have a **LocalNetworkSiteRef** listed.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-142">Depending on the configuration that you created, you may not have a **LocalNetworkSiteRef** listed.</span></span>

    <Gateway>
       <ConnectionsToLocalNetwork>
         <LocalNetworkSiteRef name="D1BFC9CB_Site2">
           <Connection type="IPsec" />
         </LocalNetworkSiteRef>
       </ConnectionsToLocalNetwork>
    </Gateway>

<span data-ttu-id="3e2f8-143">Example:</span><span class="sxs-lookup"><span data-stu-id="3e2f8-143">Example:</span></span>

    <Gateway>
       <ConnectionsToLocalNetwork>
       </ConnectionsToLocalNetwork>
     </Gateway>

###<a name="local-network-sites"></a><span data-ttu-id="3e2f8-144">Local Network Sites</span><span class="sxs-lookup"><span data-stu-id="3e2f8-144">Local Network Sites</span></span>

<span data-ttu-id="3e2f8-145">Remove any local sites that you are no longer using.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-145">Remove any local sites that you are no longer using.</span></span> <span data-ttu-id="3e2f8-146">Depending on the configuration you created, it is possible that you don't have a **LocalNetworkSite** listed.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-146">Depending on the configuration you created, it is possible that you don't have a **LocalNetworkSite** listed.</span></span>

    <LocalNetworkSites>
      <LocalNetworkSite name="Site1">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
      </LocalNetworkSite>
      <LocalNetworkSite name="Site3">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>57.179.18.164</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

<span data-ttu-id="3e2f8-147">In this example, we removed only Site3.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-147">In this example, we removed only Site3.</span></span>

    <LocalNetworkSites>
        <LocalNetworkSite name="Site1">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="client-addresspool"></a><span data-ttu-id="3e2f8-148">Client AddressPool</span><span class="sxs-lookup"><span data-stu-id="3e2f8-148">Client AddressPool</span></span>

<span data-ttu-id="3e2f8-149">If you had a P2S connection to your VNet, you will have a **VPNClientAddressPool**.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-149">If you had a P2S connection to your VNet, you will have a **VPNClientAddressPool**.</span></span> <span data-ttu-id="3e2f8-150">Remove the client address pools that correspond to the virtual network gateway that you deleted.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-150">Remove the client address pools that correspond to the virtual network gateway that you deleted.</span></span>

    <Gateway>
       <VPNClientAddressPool>
         <AddressPrefix>10.1.0.0/24</AddressPrefix>
       </VPNClientAddressPool>
       <ConnectionsToLocalNetwork />
    </Gateway>

<span data-ttu-id="3e2f8-151">Example:</span><span class="sxs-lookup"><span data-stu-id="3e2f8-151">Example:</span></span>

     <Gateway>
       <ConnectionsToLocalNetwork />
     </Gateway>

### <a name="gatewaysubnet"></a><span data-ttu-id="3e2f8-152">GatewaySubnet</span><span class="sxs-lookup"><span data-stu-id="3e2f8-152">GatewaySubnet</span></span>

<span data-ttu-id="3e2f8-153">Delete the **GatewaySubnet** that corresponds to the VNet.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-153">Delete the **GatewaySubnet** that corresponds to the VNet.</span></span>

    <Subnets>
       <Subnet name="FrontEnd">
         <AddressPrefix>10.11.0.0/24</AddressPrefix>
       </Subnet>
       <Subnet name="GatewaySubnet">
         <AddressPrefix>10.11.1.0/29</AddressPrefix>
       </Subnet>
     </Subnets>

<span data-ttu-id="3e2f8-154">Example:</span><span class="sxs-lookup"><span data-stu-id="3e2f8-154">Example:</span></span>

    <Subnets>
       <Subnet name="FrontEnd">
         <AddressPrefix>10.11.0.0/24</AddressPrefix>
       </Subnet>
     </Subnets>

## <a name="step-5-upload-the-network-configuration-file"></a><span data-ttu-id="3e2f8-155">Step 5: Upload the network configuration file</span><span class="sxs-lookup"><span data-stu-id="3e2f8-155">Step 5: Upload the network configuration file</span></span>

<span data-ttu-id="3e2f8-156">Save your changes and upload the network configuration file to Azure.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-156">Save your changes and upload the network configuration file to Azure.</span></span> <span data-ttu-id="3e2f8-157">Make sure you change the file path as necessary for your environment.</span><span class="sxs-lookup"><span data-stu-id="3e2f8-157">Make sure you change the file path as necessary for your environment.</span></span>

     Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml

<span data-ttu-id="3e2f8-158">If successful, the return shows something similar to this example:</span><span class="sxs-lookup"><span data-stu-id="3e2f8-158">If successful, the return shows something similar to this example:</span></span>

     OperationDescription        OperationId                      OperationStatus                                                
     --------------------        -----------                      ---------------                                                
     Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded