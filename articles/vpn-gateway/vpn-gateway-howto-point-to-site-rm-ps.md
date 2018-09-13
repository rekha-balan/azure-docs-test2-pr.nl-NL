---
title: 'Connect a computer to an Azure virtual network using Point-to-Site: PowerShell | Microsoft Docs'
description: Securely connect a computer to your Azure Virtual Network by creating a Point-to-Site VPN gateway connection.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/10/2017
ms.author: cherylmc
ms.openlocfilehash: 6cb21228964453066083f525f7fc82cd5235687c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555499"
---
# <a name="configure-a-point-to-site-connection-to-a-vnet-using-powershell"></a><span data-ttu-id="a1acd-103">Configure a Point-to-Site connection to a VNet using PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1acd-103">Configure a Point-to-Site connection to a VNet using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager - Azure Portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [Resource Manager - PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Classic - Azure Portal](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 

<span data-ttu-id="a1acd-107">A Point-to-Site (P2S) configuration lets you create a secure connection from an individual client computer to a virtual network.</span><span class="sxs-lookup"><span data-stu-id="a1acd-107">A Point-to-Site (P2S) configuration lets you create a secure connection from an individual client computer to a virtual network.</span></span> <span data-ttu-id="a1acd-108">P2S is a VPN connection over SSTP (Secure Socket Tunneling Protocol).</span><span class="sxs-lookup"><span data-stu-id="a1acd-108">P2S is a VPN connection over SSTP (Secure Socket Tunneling Protocol).</span></span> <span data-ttu-id="a1acd-109">Point-to-Site connections are useful when you want to connect to your VNet from a remote location, such as from home or a conference, or when you only have a few clients that need to connect to a virtual network.</span><span class="sxs-lookup"><span data-stu-id="a1acd-109">Point-to-Site connections are useful when you want to connect to your VNet from a remote location, such as from home or a conference, or when you only have a few clients that need to connect to a virtual network.</span></span> <span data-ttu-id="a1acd-110">P2S connections do not require a VPN device or a public-facing IP address.</span><span class="sxs-lookup"><span data-stu-id="a1acd-110">P2S connections do not require a VPN device or a public-facing IP address.</span></span> <span data-ttu-id="a1acd-111">You establish the VPN connection from the client computer.</span><span class="sxs-lookup"><span data-stu-id="a1acd-111">You establish the VPN connection from the client computer.</span></span>

<span data-ttu-id="a1acd-112">This article walks you through creating a VNet with a Point-to-Site connection in the Resource Manager deployment model using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1acd-112">This article walks you through creating a VNet with a Point-to-Site connection in the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="a1acd-113">For more information about Point-to-Site connections, see the [Point-to-Site FAQ](#faq) at the end of this article.</span><span class="sxs-lookup"><span data-stu-id="a1acd-113">For more information about Point-to-Site connections, see the [Point-to-Site FAQ](#faq) at the end of this article.</span></span>

### <a name="deployment-models-and-methods-for-p2s-connections"></a><span data-ttu-id="a1acd-114">Deployment models and methods for P2S connections</span><span class="sxs-lookup"><span data-stu-id="a1acd-114">Deployment models and methods for P2S connections</span></span>
[!INCLUDE [deployment models](../../includes/vpn-gateway-deployment-models-include.md)]

<span data-ttu-id="a1acd-115">The following table shows the two deployment models and available deployment methods for P2S configurations.</span><span class="sxs-lookup"><span data-stu-id="a1acd-115">The following table shows the two deployment models and available deployment methods for P2S configurations.</span></span> <span data-ttu-id="a1acd-116">When an article with configuration steps is available, we link directly to it from this table.</span><span class="sxs-lookup"><span data-stu-id="a1acd-116">When an article with configuration steps is available, we link directly to it from this table.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-table-point-to-site-include.md)]

## <a name="basic-workflow"></a><span data-ttu-id="a1acd-117">Basic workflow</span><span class="sxs-lookup"><span data-stu-id="a1acd-117">Basic workflow</span></span>
![Connect a computer to an Azure VNet - Point-to-Site connection diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

<span data-ttu-id="a1acd-119">In this scenario, you create a virtual network with a Point-to-Site connection.</span><span class="sxs-lookup"><span data-stu-id="a1acd-119">In this scenario, you create a virtual network with a Point-to-Site connection.</span></span> <span data-ttu-id="a1acd-120">The instructions also help you generate certificates, which are required for this configuration.</span><span class="sxs-lookup"><span data-stu-id="a1acd-120">The instructions also help you generate certificates, which are required for this configuration.</span></span> <span data-ttu-id="a1acd-121">A P2S connection is composed of the following items: A VNet with a VPN gateway, a root certificate .cer file (public key), a client certificate, and the VPN configuration on the client.</span><span class="sxs-lookup"><span data-stu-id="a1acd-121">A P2S connection is composed of the following items: A VNet with a VPN gateway, a root certificate .cer file (public key), a client certificate, and the VPN configuration on the client.</span></span> 

<span data-ttu-id="a1acd-122">We use the following values for this configuration.</span><span class="sxs-lookup"><span data-stu-id="a1acd-122">We use the following values for this configuration.</span></span> <span data-ttu-id="a1acd-123">We set the variables in section [1](#declare) of the article.</span><span class="sxs-lookup"><span data-stu-id="a1acd-123">We set the variables in section [1](#declare) of the article.</span></span> <span data-ttu-id="a1acd-124">You can either use the steps as a walk-through and use the values without changing them, or change them to reflect your environment.</span><span class="sxs-lookup"><span data-stu-id="a1acd-124">You can either use the steps as a walk-through and use the values without changing them, or change them to reflect your environment.</span></span> 

### <a name="example"></a><span data-ttu-id="a1acd-125">Example values</span><span class="sxs-lookup"><span data-stu-id="a1acd-125">Example values</span></span>
* <span data-ttu-id="a1acd-126">**Name: VNet1**</span><span class="sxs-lookup"><span data-stu-id="a1acd-126">**Name: VNet1**</span></span>
* <span data-ttu-id="a1acd-127">**Address space: 192.168.0.0/16** and **10.254.0.0/16**</span><span class="sxs-lookup"><span data-stu-id="a1acd-127">**Address space: 192.168.0.0/16** and **10.254.0.0/16**</span></span><br><span data-ttu-id="a1acd-128">For this example, we use more than one address space to illustrate that this configuration works with multiple address spaces.</span><span class="sxs-lookup"><span data-stu-id="a1acd-128">For this example, we use more than one address space to illustrate that this configuration works with multiple address spaces.</span></span> <span data-ttu-id="a1acd-129">However, multiple address spaces are not required for this configuration.</span><span class="sxs-lookup"><span data-stu-id="a1acd-129">However, multiple address spaces are not required for this configuration.</span></span>
* <span data-ttu-id="a1acd-130">**Subnet name: FrontEnd**</span><span class="sxs-lookup"><span data-stu-id="a1acd-130">**Subnet name: FrontEnd**</span></span>
  * <span data-ttu-id="a1acd-131">**Subnet address range: 192.168.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="a1acd-131">**Subnet address range: 192.168.1.0/24**</span></span>
* <span data-ttu-id="a1acd-132">**Subnet name: BackEnd**</span><span class="sxs-lookup"><span data-stu-id="a1acd-132">**Subnet name: BackEnd**</span></span>
  * <span data-ttu-id="a1acd-133">**Subnet address range: 10.254.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="a1acd-133">**Subnet address range: 10.254.1.0/24**</span></span>
* <span data-ttu-id="a1acd-134">**Subnet name: GatewaySubnet**</span><span class="sxs-lookup"><span data-stu-id="a1acd-134">**Subnet name: GatewaySubnet**</span></span><br><span data-ttu-id="a1acd-135">The Subnet name *GatewaySubnet* is mandatory for the VPN gateway to work.</span><span class="sxs-lookup"><span data-stu-id="a1acd-135">The Subnet name *GatewaySubnet* is mandatory for the VPN gateway to work.</span></span>
  * <span data-ttu-id="a1acd-136">**GatewaySubnet address range: 192.168.200.0/24**</span><span class="sxs-lookup"><span data-stu-id="a1acd-136">**GatewaySubnet address range: 192.168.200.0/24**</span></span> 
* <span data-ttu-id="a1acd-137">**VPN client address pool: 172.16.201.0/24**</span><span class="sxs-lookup"><span data-stu-id="a1acd-137">**VPN client address pool: 172.16.201.0/24**</span></span><br><span data-ttu-id="a1acd-138">VPN clients that connect to the VNet using this Point-to-Site connection receive an IP address from the VPN client address pool.</span><span class="sxs-lookup"><span data-stu-id="a1acd-138">VPN clients that connect to the VNet using this Point-to-Site connection receive an IP address from the VPN client address pool.</span></span>
* <span data-ttu-id="a1acd-139">**Subscription:** If you have more than one subscription, verify that you are using the correct one.</span><span class="sxs-lookup"><span data-stu-id="a1acd-139">**Subscription:** If you have more than one subscription, verify that you are using the correct one.</span></span>
* <span data-ttu-id="a1acd-140">**Resource Group: TestRG**</span><span class="sxs-lookup"><span data-stu-id="a1acd-140">**Resource Group: TestRG**</span></span>
* <span data-ttu-id="a1acd-141">**Location: East US**</span><span class="sxs-lookup"><span data-stu-id="a1acd-141">**Location: East US**</span></span>
* <span data-ttu-id="a1acd-142">**DNS Server: IP address** of the DNS server that you want to use for name resolution.</span><span class="sxs-lookup"><span data-stu-id="a1acd-142">**DNS Server: IP address** of the DNS server that you want to use for name resolution.</span></span>
* <span data-ttu-id="a1acd-143">**GW Name: Vnet1GW**</span><span class="sxs-lookup"><span data-stu-id="a1acd-143">**GW Name: Vnet1GW**</span></span>
* <span data-ttu-id="a1acd-144">**Public IP name: VNet1GWPIP**</span><span class="sxs-lookup"><span data-stu-id="a1acd-144">**Public IP name: VNet1GWPIP**</span></span>
* <span data-ttu-id="a1acd-145">**VpnType: RouteBased**</span><span class="sxs-lookup"><span data-stu-id="a1acd-145">**VpnType: RouteBased**</span></span>

## <a name="before-beginning"></a><span data-ttu-id="a1acd-146">Before beginning</span><span class="sxs-lookup"><span data-stu-id="a1acd-146">Before beginning</span></span>
* <span data-ttu-id="a1acd-147">Verify that you have an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a1acd-147">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="a1acd-148">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="a1acd-148">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="a1acd-149">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="a1acd-149">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="a1acd-150">For more information about installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="a1acd-150">For more information about installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> 

## <a name="declare"></a><span data-ttu-id="a1acd-151">Part 1 - Log in and set variables</span><span class="sxs-lookup"><span data-stu-id="a1acd-151">Part 1 - Log in and set variables</span></span>
<span data-ttu-id="a1acd-152">In this section, you log in and declare the values used for this configuration.</span><span class="sxs-lookup"><span data-stu-id="a1acd-152">In this section, you log in and declare the values used for this configuration.</span></span> <span data-ttu-id="a1acd-153">The declared values are used in the sample scripts.</span><span class="sxs-lookup"><span data-stu-id="a1acd-153">The declared values are used in the sample scripts.</span></span> <span data-ttu-id="a1acd-154">Change the values to reflect your own environment.</span><span class="sxs-lookup"><span data-stu-id="a1acd-154">Change the values to reflect your own environment.</span></span> <span data-ttu-id="a1acd-155">Or, you can use the declared values and go through the steps as an exercise.</span><span class="sxs-lookup"><span data-stu-id="a1acd-155">Or, you can use the declared values and go through the steps as an exercise.</span></span>

1. <span data-ttu-id="a1acd-156">Open your PowerShell console with elevated privileges, and log in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="a1acd-156">Open your PowerShell console with elevated privileges, and log in to your Azure account.</span></span> <span data-ttu-id="a1acd-157">This cmdlet prompts you for the login credentials.</span><span class="sxs-lookup"><span data-stu-id="a1acd-157">This cmdlet prompts you for the login credentials.</span></span> <span data-ttu-id="a1acd-158">After logging in, it downloads your account settings so that they are available to Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1acd-158">After logging in, it downloads your account settings so that they are available to Azure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```
2. <span data-ttu-id="a1acd-159">Get a list of your Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="a1acd-159">Get a list of your Azure subscriptions.</span></span>

  ```powershell  
  Get-AzureRmSubscription
  ```
3. <span data-ttu-id="a1acd-160">Specify the subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="a1acd-160">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. <span data-ttu-id="a1acd-161">Declare the variables that you want to use.</span><span class="sxs-lookup"><span data-stu-id="a1acd-161">Declare the variables that you want to use.</span></span> <span data-ttu-id="a1acd-162">Use the following sample, substituting the values for your own when necessary.</span><span class="sxs-lookup"><span data-stu-id="a1acd-162">Use the following sample, substituting the values for your own when necessary.</span></span>

  ```powershell
  $VNetName  = "VNet1"
  $FESubName = "FrontEnd"
  $BESubName = "Backend"
  $GWSubName = "GatewaySubnet"
  $VNetPrefix1 = "192.168.0.0/16"
  $VNetPrefix2 = "10.254.0.0/16"
  $FESubPrefix = "192.168.1.0/24"
  $BESubPrefix = "10.254.1.0/24"
  $GWSubPrefix = "192.168.200.0/26"
  $VPNClientAddressPool = "172.16.201.0/24"
  $RG = "TestRG"
  $Location = "East US"
  $DNS = "8.8.8.8"
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <a name="ConfigureVNet"></a><span data-ttu-id="a1acd-163">Part 2 - Configure a VNet</span><span class="sxs-lookup"><span data-stu-id="a1acd-163">Part 2 - Configure a VNet</span></span>
1. <span data-ttu-id="a1acd-164">Create a resource group.</span><span class="sxs-lookup"><span data-stu-id="a1acd-164">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. <span data-ttu-id="a1acd-165">Create the subnet configurations for the virtual network, naming them *FrontEnd*, *BackEnd*, and *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="a1acd-165">Create the subnet configurations for the virtual network, naming them *FrontEnd*, *BackEnd*, and *GatewaySubnet*.</span></span> <span data-ttu-id="a1acd-166">These prefixes must be part of the VNet address space that you declared.</span><span class="sxs-lookup"><span data-stu-id="a1acd-166">These prefixes must be part of the VNet address space that you declared.</span></span>

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. <span data-ttu-id="a1acd-167">Create the virtual network.</span><span class="sxs-lookup"><span data-stu-id="a1acd-167">Create the virtual network.</span></span> <span data-ttu-id="a1acd-168">The DNS server specified should be a DNS server that can resolve the names for the resources you are connecting to.</span><span class="sxs-lookup"><span data-stu-id="a1acd-168">The DNS server specified should be a DNS server that can resolve the names for the resources you are connecting to.</span></span> <span data-ttu-id="a1acd-169">For this example, we used a public IP address.</span><span class="sxs-lookup"><span data-stu-id="a1acd-169">For this example, we used a public IP address.</span></span> <span data-ttu-id="a1acd-170">Be sure to use your own values.</span><span class="sxs-lookup"><span data-stu-id="a1acd-170">Be sure to use your own values.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. <span data-ttu-id="a1acd-171">Specify the variables for the virtual network you created.</span><span class="sxs-lookup"><span data-stu-id="a1acd-171">Specify the variables for the virtual network you created.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="a1acd-172">Request a dynamically assigned public IP address.</span><span class="sxs-lookup"><span data-stu-id="a1acd-172">Request a dynamically assigned public IP address.</span></span> <span data-ttu-id="a1acd-173">This IP address is necessary for the gateway to work properly.</span><span class="sxs-lookup"><span data-stu-id="a1acd-173">This IP address is necessary for the gateway to work properly.</span></span> <span data-ttu-id="a1acd-174">You later connect the gateway to the gateway IP configuration.</span><span class="sxs-lookup"><span data-stu-id="a1acd-174">You later connect the gateway to the gateway IP configuration.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```


## <a name="Certificates"></a><span data-ttu-id="a1acd-175">Part 3 - Certificates</span><span class="sxs-lookup"><span data-stu-id="a1acd-175">Part 3 - Certificates</span></span>

<span data-ttu-id="a1acd-176">Certificates are used by Azure to authenticate VPN clients for Point-to-Site VPNs.</span><span class="sxs-lookup"><span data-stu-id="a1acd-176">Certificates are used by Azure to authenticate VPN clients for Point-to-Site VPNs.</span></span> <span data-ttu-id="a1acd-177">After creating the root certificate, you export the public certificate data (not the private key) as a Base-64 encoded X.509 .cer file.</span><span class="sxs-lookup"><span data-stu-id="a1acd-177">After creating the root certificate, you export the public certificate data (not the private key) as a Base-64 encoded X.509 .cer file.</span></span> <span data-ttu-id="a1acd-178">You then upload the public certificate data from the root certificate to Azure.</span><span class="sxs-lookup"><span data-stu-id="a1acd-178">You then upload the public certificate data from the root certificate to Azure.</span></span>

<span data-ttu-id="a1acd-179">Each client computer that connects to a VNet using Point-to-Site must have a client certificate installed.</span><span class="sxs-lookup"><span data-stu-id="a1acd-179">Each client computer that connects to a VNet using Point-to-Site must have a client certificate installed.</span></span> <span data-ttu-id="a1acd-180">The client certificate is generated from the root certificate and installed on each client computer.</span><span class="sxs-lookup"><span data-stu-id="a1acd-180">The client certificate is generated from the root certificate and installed on each client computer.</span></span> <span data-ttu-id="a1acd-181">If a valid client certificate is not installed and the client tries to connect to the VNet, authentication fails.</span><span class="sxs-lookup"><span data-stu-id="a1acd-181">If a valid client certificate is not installed and the client tries to connect to the VNet, authentication fails.</span></span>

### <a name="cer"></a><span data-ttu-id="a1acd-182">Step 1 - Obtain the .cer file for the root certificate</span><span class="sxs-lookup"><span data-stu-id="a1acd-182">Step 1 - Obtain the .cer file for the root certificate</span></span>

#### <a name="enterprise-certificate"></a><span data-ttu-id="a1acd-183">Enterprise certificate</span><span class="sxs-lookup"><span data-stu-id="a1acd-183">Enterprise certificate</span></span>
 
<span data-ttu-id="a1acd-184">If you are using an enterprise solution, you can use your existing certificate chain.</span><span class="sxs-lookup"><span data-stu-id="a1acd-184">If you are using an enterprise solution, you can use your existing certificate chain.</span></span> <span data-ttu-id="a1acd-185">Obtain the .cer file for the root certificate that you want to use.</span><span class="sxs-lookup"><span data-stu-id="a1acd-185">Obtain the .cer file for the root certificate that you want to use.</span></span>

#### <a name="self-signed-root-certificate"></a><span data-ttu-id="a1acd-186">Self-signed root certificate</span><span class="sxs-lookup"><span data-stu-id="a1acd-186">Self-signed root certificate</span></span>

<span data-ttu-id="a1acd-187">If you are not using an enterprise certificate solution, you need to create a self-signed root certificate.</span><span class="sxs-lookup"><span data-stu-id="a1acd-187">If you are not using an enterprise certificate solution, you need to create a self-signed root certificate.</span></span> <span data-ttu-id="a1acd-188">To create a self-signed root certificate that contains the necessary fields for P2S authentication, you can use PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1acd-188">To create a self-signed root certificate that contains the necessary fields for P2S authentication, you can use PowerShell.</span></span> <span data-ttu-id="a1acd-189">[Create a self-signed root certificate for Point-to-Site connections using PowerShell](vpn-gateway-certificates-point-to-site.md) walks you through the steps to create a self-signed root certificate.</span><span class="sxs-lookup"><span data-stu-id="a1acd-189">[Create a self-signed root certificate for Point-to-Site connections using PowerShell](vpn-gateway-certificates-point-to-site.md) walks you through the steps to create a self-signed root certificate.</span></span>

> [!NOTE]
> Previously, makecert was the recommended method to create self-signed root certificates and generate client certificates for Point-to-Site connections. You can now use PowerShell to create these certificates. One benefit of using PowerShell is the ability to create SHA-2 certificates. See [Create a self-signed root certificate for Point-to-Site connections using PowerShell](vpn-gateway-certificates-point-to-site.md) for the required values.
>
>

#### <a name="to-export-the-public-key-for-a-self-signed-root-certificate"></a><span data-ttu-id="a1acd-194">To export the public key for a self-signed root certificate</span><span class="sxs-lookup"><span data-stu-id="a1acd-194">To export the public key for a self-signed root certificate</span></span>

<span data-ttu-id="a1acd-195">Point-to-Site connections require the public key (.cer) to be uploaded to Azure.</span><span class="sxs-lookup"><span data-stu-id="a1acd-195">Point-to-Site connections require the public key (.cer) to be uploaded to Azure.</span></span> <span data-ttu-id="a1acd-196">The following steps help you export the .cer file for your self-signed root certificate.</span><span class="sxs-lookup"><span data-stu-id="a1acd-196">The following steps help you export the .cer file for your self-signed root certificate.</span></span>

1. <span data-ttu-id="a1acd-197">To obtain a .cer file from the certificate, open **Manage user certificates**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-197">To obtain a .cer file from the certificate, open **Manage user certificates**.</span></span>
2. <span data-ttu-id="a1acd-198">Locate the 'P2SRootCert' self-signed root certificate in 'Certificates - Current User\Personal\Certificates', and right-click.</span><span class="sxs-lookup"><span data-stu-id="a1acd-198">Locate the 'P2SRootCert' self-signed root certificate in 'Certificates - Current User\Personal\Certificates', and right-click.</span></span> <span data-ttu-id="a1acd-199">Click **All Tasks**, and then click **Export** to open the **Certificate Export Wizard**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-199">Click **All Tasks**, and then click **Export** to open the **Certificate Export Wizard**.</span></span>
3. <span data-ttu-id="a1acd-200">In the Wizard, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-200">In the Wizard, click **Next**.</span></span> <span data-ttu-id="a1acd-201">Select **No, do not export the private key**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-201">Select **No, do not export the private key**, and then click **Next**.</span></span>
4. <span data-ttu-id="a1acd-202">On the **Export File Format** page, select **Base-64 encoded X.509 (.CER).**, then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-202">On the **Export File Format** page, select **Base-64 encoded X.509 (.CER).**, then click **Next**.</span></span> 
5. <span data-ttu-id="a1acd-203">On the **File to Export** page, Browse to 'C:', create a subdirectory called 'cert' and select it.</span><span class="sxs-lookup"><span data-stu-id="a1acd-203">On the **File to Export** page, Browse to 'C:', create a subdirectory called 'cert' and select it.</span></span> <span data-ttu-id="a1acd-204">Name the certificate file 'P2SRootCert.cer', then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-204">Name the certificate file 'P2SRootCert.cer', then click **Save**.</span></span> 
6. <span data-ttu-id="a1acd-205">Click **Next**, then **Finish** to export the certificate.</span><span class="sxs-lookup"><span data-stu-id="a1acd-205">Click **Next**, then **Finish** to export the certificate.</span></span> <span data-ttu-id="a1acd-206">**The export was successful** appears.</span><span class="sxs-lookup"><span data-stu-id="a1acd-206">**The export was successful** appears.</span></span> <span data-ttu-id="a1acd-207">Click **OK** to close the wizard.</span><span class="sxs-lookup"><span data-stu-id="a1acd-207">Click **OK** to close the wizard.</span></span>

### <a name="generate"></a><span data-ttu-id="a1acd-208">Step 2 - Generate a client certificate</span><span class="sxs-lookup"><span data-stu-id="a1acd-208">Step 2 - Generate a client certificate</span></span>
<span data-ttu-id="a1acd-209">You can either generate a unique certificate for each client, or you can use the same certificate on multiple clients.</span><span class="sxs-lookup"><span data-stu-id="a1acd-209">You can either generate a unique certificate for each client, or you can use the same certificate on multiple clients.</span></span> <span data-ttu-id="a1acd-210">The advantage to generating unique client certificates is the ability to revoke a single certificate.</span><span class="sxs-lookup"><span data-stu-id="a1acd-210">The advantage to generating unique client certificates is the ability to revoke a single certificate.</span></span> <span data-ttu-id="a1acd-211">Otherwise, if everyone is using the same client certificate and you need to revoke it, you have to generate and install new certificates for all the clients that use that certificate to authenticate.</span><span class="sxs-lookup"><span data-stu-id="a1acd-211">Otherwise, if everyone is using the same client certificate and you need to revoke it, you have to generate and install new certificates for all the clients that use that certificate to authenticate.</span></span>

#### <a name="enterprise-certificate"></a><span data-ttu-id="a1acd-212">Enterprise certificate</span><span class="sxs-lookup"><span data-stu-id="a1acd-212">Enterprise certificate</span></span>
- <span data-ttu-id="a1acd-213">If you are using an enterprise certificate solution, generate a client certificate with the common name value format 'name@yourdomain.com', rather than the 'domain name\username' format.</span><span class="sxs-lookup"><span data-stu-id="a1acd-213">If you are using an enterprise certificate solution, generate a client certificate with the common name value format 'name@yourdomain.com', rather than the 'domain name\username' format.</span></span>
- <span data-ttu-id="a1acd-214">Make sure the client certificate is based on the 'User' certificate template that has 'Client Authentication' as the first item in the use list, rather than Smart Card Logon, etc. You can check the certificate by double-clicking the client certificate and viewing **Details > Enhanced Key Usage**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-214">Make sure the client certificate is based on the 'User' certificate template that has 'Client Authentication' as the first item in the use list, rather than Smart Card Logon, etc. You can check the certificate by double-clicking the client certificate and viewing **Details > Enhanced Key Usage**.</span></span>

#### <a name="self-signed-root-certificate"></a><span data-ttu-id="a1acd-215">Self-signed root certificate</span><span class="sxs-lookup"><span data-stu-id="a1acd-215">Self-signed root certificate</span></span> 
<span data-ttu-id="a1acd-216">If you are using a self-signed root certificate, see [Generate a client certificate using PowerShell](vpn-gateway-certificates-point-to-site.md#clientcert) for steps to generate a client certificate that is compatible with Point-to-Site connections.</span><span class="sxs-lookup"><span data-stu-id="a1acd-216">If you are using a self-signed root certificate, see [Generate a client certificate using PowerShell](vpn-gateway-certificates-point-to-site.md#clientcert) for steps to generate a client certificate that is compatible with Point-to-Site connections.</span></span>


### <a name="exportclientcert"></a><span data-ttu-id="a1acd-217">Step 3 - Export the client certificate</span><span class="sxs-lookup"><span data-stu-id="a1acd-217">Step 3 - Export the client certificate</span></span>

<span data-ttu-id="a1acd-218">If you generate a client certificate from a self-signed root certificate using the [PowerShell](vpn-gateway-certificates-point-to-site.md#clientcert) instructions, it's automatically installed on the computer that you used to generate it.</span><span class="sxs-lookup"><span data-stu-id="a1acd-218">If you generate a client certificate from a self-signed root certificate using the [PowerShell](vpn-gateway-certificates-point-to-site.md#clientcert) instructions, it's automatically installed on the computer that you used to generate it.</span></span> <span data-ttu-id="a1acd-219">If you want to install a client certificate on another client computer, you need to export it.</span><span class="sxs-lookup"><span data-stu-id="a1acd-219">If you want to install a client certificate on another client computer, you need to export it.</span></span>
 
1. <span data-ttu-id="a1acd-220">To export a client certificate, open **Manage user certificates**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-220">To export a client certificate, open **Manage user certificates**.</span></span> <span data-ttu-id="a1acd-221">Right-click the client certificate that you want to export, click **all tasks**, and then click **export** to open the **Certificate Export Wizard**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-221">Right-click the client certificate that you want to export, click **all tasks**, and then click **export** to open the **Certificate Export Wizard**.</span></span>
2. <span data-ttu-id="a1acd-222">In the Wizard, click **Next**, then select **Yes, export the private key**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-222">In the Wizard, click **Next**, then select **Yes, export the private key**, and then click **Next**.</span></span>
3. <span data-ttu-id="a1acd-223">On the **Export File Format** page, leave the defaults selected.</span><span class="sxs-lookup"><span data-stu-id="a1acd-223">On the **Export File Format** page, leave the defaults selected.</span></span> <span data-ttu-id="a1acd-224">Make sure **Include all certificates in the certification path if possible** is selected to also export the required root certificate information.</span><span class="sxs-lookup"><span data-stu-id="a1acd-224">Make sure **Include all certificates in the certification path if possible** is selected to also export the required root certificate information.</span></span> <span data-ttu-id="a1acd-225">Then, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-225">Then, click **Next**.</span></span>
4. <span data-ttu-id="a1acd-226">On the **Security** page, you must protect the private key.</span><span class="sxs-lookup"><span data-stu-id="a1acd-226">On the **Security** page, you must protect the private key.</span></span> <span data-ttu-id="a1acd-227">If you select to use a password, make sure to record or remember the password that you set for this certificate.</span><span class="sxs-lookup"><span data-stu-id="a1acd-227">If you select to use a password, make sure to record or remember the password that you set for this certificate.</span></span> <span data-ttu-id="a1acd-228">Then, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-228">Then, click **Next**.</span></span>
5. <span data-ttu-id="a1acd-229">On the **File to Export**, **Browse** to the location to which you want to export the certificate.</span><span class="sxs-lookup"><span data-stu-id="a1acd-229">On the **File to Export**, **Browse** to the location to which you want to export the certificate.</span></span> <span data-ttu-id="a1acd-230">For **File name**, name the certificate file.</span><span class="sxs-lookup"><span data-stu-id="a1acd-230">For **File name**, name the certificate file.</span></span> <span data-ttu-id="a1acd-231">Then, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-231">Then, click **Next**.</span></span>
6. <span data-ttu-id="a1acd-232">Click **Finish** to export the certificate.</span><span class="sxs-lookup"><span data-stu-id="a1acd-232">Click **Finish** to export the certificate.</span></span>

### <a name="upload"></a><span data-ttu-id="a1acd-233">Step 4 - Upload the root certificate .cer file</span><span class="sxs-lookup"><span data-stu-id="a1acd-233">Step 4 - Upload the root certificate .cer file</span></span>

<span data-ttu-id="a1acd-234">After the gateway has been created, you can upload the .cer file for a trusted root certificate to Azure.</span><span class="sxs-lookup"><span data-stu-id="a1acd-234">After the gateway has been created, you can upload the .cer file for a trusted root certificate to Azure.</span></span> <span data-ttu-id="a1acd-235">You can upload files for up to 20 root certificates.</span><span class="sxs-lookup"><span data-stu-id="a1acd-235">You can upload files for up to 20 root certificates.</span></span> <span data-ttu-id="a1acd-236">You do not upload the private key for the root certificate to Azure.</span><span class="sxs-lookup"><span data-stu-id="a1acd-236">You do not upload the private key for the root certificate to Azure.</span></span> <span data-ttu-id="a1acd-237">Once the .cer file is uploaded, Azure uses it to authenticate clients that connect to the virtual network.</span><span class="sxs-lookup"><span data-stu-id="a1acd-237">Once the .cer file is uploaded, Azure uses it to authenticate clients that connect to the virtual network.</span></span>

1. <span data-ttu-id="a1acd-238">Declare the variable for your certificate name, replacing the value with your own:</span><span class="sxs-lookup"><span data-stu-id="a1acd-238">Declare the variable for your certificate name, replacing the value with your own:</span></span>

  ```powershell
  $P2SRootCertName = "Mycertificatename.cer"
  ```
2. <span data-ttu-id="a1acd-239">Replace the file path with your own, and then run the cmdlets.</span><span class="sxs-lookup"><span data-stu-id="a1acd-239">Replace the file path with your own, and then run the cmdlets.</span></span>

  ```powershell
  $filePathForCert = "C:\cert\Mycertificatename.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```


## <a name="creategateway"></a><span data-ttu-id="a1acd-240">Part 4 - Create the VPN gateway</span><span class="sxs-lookup"><span data-stu-id="a1acd-240">Part 4 - Create the VPN gateway</span></span>
<span data-ttu-id="a1acd-241">Configure and create the virtual network gateway for your VNet.</span><span class="sxs-lookup"><span data-stu-id="a1acd-241">Configure and create the virtual network gateway for your VNet.</span></span> <span data-ttu-id="a1acd-242">The *-GatewayType* must be **Vpn** and the *-VpnType* must be **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-242">The *-GatewayType* must be **Vpn** and the *-VpnType* must be **RouteBased**.</span></span> <span data-ttu-id="a1acd-243">A VPN gateway can take up to 45 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="a1acd-243">A VPN gateway can take up to 45 minutes to complete.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku Standard `
-VpnClientAddressPool $VPNClientAddressPool -VpnClientRootCertificates $p2srootcert
```


## <a name="clientconfig"></a><span data-ttu-id="a1acd-244">Part 5 - Download the VPN client configuration package</span><span class="sxs-lookup"><span data-stu-id="a1acd-244">Part 5 - Download the VPN client configuration package</span></span>
<span data-ttu-id="a1acd-245">To connect to a VNet using a Point-to-Site VPN, each client must install a VPN client configuration package.</span><span class="sxs-lookup"><span data-stu-id="a1acd-245">To connect to a VNet using a Point-to-Site VPN, each client must install a VPN client configuration package.</span></span> <span data-ttu-id="a1acd-246">The package does not install a VPN client.</span><span class="sxs-lookup"><span data-stu-id="a1acd-246">The package does not install a VPN client.</span></span> <span data-ttu-id="a1acd-247">It configures the native Windows VPN client with the settings necessary to connect to the virtual network.</span><span class="sxs-lookup"><span data-stu-id="a1acd-247">It configures the native Windows VPN client with the settings necessary to connect to the virtual network.</span></span> <span data-ttu-id="a1acd-248">For the list of client operating systems that are supported, see the [Point-to-Site connections FAQ](#faq) at the end of this article.</span><span class="sxs-lookup"><span data-stu-id="a1acd-248">For the list of client operating systems that are supported, see the [Point-to-Site connections FAQ](#faq) at the end of this article.</span></span>

1. <span data-ttu-id="a1acd-249">After the gateway has been created, you can generate and download the client configuration package.</span><span class="sxs-lookup"><span data-stu-id="a1acd-249">After the gateway has been created, you can generate and download the client configuration package.</span></span> <span data-ttu-id="a1acd-250">This example downloads the package for 64-bit clients.</span><span class="sxs-lookup"><span data-stu-id="a1acd-250">This example downloads the package for 64-bit clients.</span></span> <span data-ttu-id="a1acd-251">If you want to download the 32-bit client, replace 'Amd64' with 'x86'.</span><span class="sxs-lookup"><span data-stu-id="a1acd-251">If you want to download the 32-bit client, replace 'Amd64' with 'x86'.</span></span> <span data-ttu-id="a1acd-252">You can also download the VPN client by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a1acd-252">You can also download the VPN client by using the Azure portal.</span></span>

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. <span data-ttu-id="a1acd-253">Copy and paste the link that is returned to a web browser to download the package, taking care to remove the """ surrounding the link.</span><span class="sxs-lookup"><span data-stu-id="a1acd-253">Copy and paste the link that is returned to a web browser to download the package, taking care to remove the """ surrounding the link.</span></span> 
3. <span data-ttu-id="a1acd-254">Download and install the package on the client computer.</span><span class="sxs-lookup"><span data-stu-id="a1acd-254">Download and install the package on the client computer.</span></span> <span data-ttu-id="a1acd-255">If you see a SmartScreen popup, click **More info**, then **Run anyway**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-255">If you see a SmartScreen popup, click **More info**, then **Run anyway**.</span></span> <span data-ttu-id="a1acd-256">You can also save the package to install on other client computers.</span><span class="sxs-lookup"><span data-stu-id="a1acd-256">You can also save the package to install on other client computers.</span></span>
4. <span data-ttu-id="a1acd-257">On the client computer, navigate to **Network Settings** and click **VPN**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-257">On the client computer, navigate to **Network Settings** and click **VPN**.</span></span> <span data-ttu-id="a1acd-258">The VPN connection shows the name of the virtual network that it connects to.</span><span class="sxs-lookup"><span data-stu-id="a1acd-258">The VPN connection shows the name of the virtual network that it connects to.</span></span>



## <a name="clientcertificate"></a><span data-ttu-id="a1acd-259">Part 6 - Install an exported client certificate</span><span class="sxs-lookup"><span data-stu-id="a1acd-259">Part 6 - Install an exported client certificate</span></span>

<span data-ttu-id="a1acd-260">If you want to create a P2S connection from a client computer other than the one you used to generate the client certificates, you need to install a client certificate.</span><span class="sxs-lookup"><span data-stu-id="a1acd-260">If you want to create a P2S connection from a client computer other than the one you used to generate the client certificates, you need to install a client certificate.</span></span> <span data-ttu-id="a1acd-261">When installing a client certificate, you need the password that was created when the client certificate was exported.</span><span class="sxs-lookup"><span data-stu-id="a1acd-261">When installing a client certificate, you need the password that was created when the client certificate was exported.</span></span>

1. <span data-ttu-id="a1acd-262">Locate and copy the *.pfx* file to the client computer.</span><span class="sxs-lookup"><span data-stu-id="a1acd-262">Locate and copy the *.pfx* file to the client computer.</span></span> <span data-ttu-id="a1acd-263">On the client computer, double-click the *.pfx* file to install.</span><span class="sxs-lookup"><span data-stu-id="a1acd-263">On the client computer, double-click the *.pfx* file to install.</span></span> <span data-ttu-id="a1acd-264">Leave the **Store Location** as **Current User**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-264">Leave the **Store Location** as **Current User**, and then click **Next**.</span></span>
2. <span data-ttu-id="a1acd-265">On the **File** to import page, don't make any changes.</span><span class="sxs-lookup"><span data-stu-id="a1acd-265">On the **File** to import page, don't make any changes.</span></span> <span data-ttu-id="a1acd-266">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-266">Click **Next**.</span></span>
3. <span data-ttu-id="a1acd-267">On the **Private key protection** page, input the password for the certificate, or verify that the security principal is correct, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-267">On the **Private key protection** page, input the password for the certificate, or verify that the security principal is correct, and then click **Next**.</span></span>
4. <span data-ttu-id="a1acd-268">On the **Certificate Store** page, leave the default location, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-268">On the **Certificate Store** page, leave the default location, and then click **Next**.</span></span>
5. <span data-ttu-id="a1acd-269">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-269">Click **Finish**.</span></span> <span data-ttu-id="a1acd-270">On the **Security Warning** for the certificate installation, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-270">On the **Security Warning** for the certificate installation, click **Yes**.</span></span> <span data-ttu-id="a1acd-271">You can feel comfortable clicking 'Yes' because you generated the certificate.</span><span class="sxs-lookup"><span data-stu-id="a1acd-271">You can feel comfortable clicking 'Yes' because you generated the certificate.</span></span> <span data-ttu-id="a1acd-272">The certificate is now successfully imported.</span><span class="sxs-lookup"><span data-stu-id="a1acd-272">The certificate is now successfully imported.</span></span>

## <a name="connect"></a><span data-ttu-id="a1acd-273">Part 7 - Connect to Azure</span><span class="sxs-lookup"><span data-stu-id="a1acd-273">Part 7 - Connect to Azure</span></span>
1. <span data-ttu-id="a1acd-274">To connect to your VNet, on the client computer, navigate to VPN connections and locate the VPN connection that you created.</span><span class="sxs-lookup"><span data-stu-id="a1acd-274">To connect to your VNet, on the client computer, navigate to VPN connections and locate the VPN connection that you created.</span></span> <span data-ttu-id="a1acd-275">It is named the same name as your virtual network.</span><span class="sxs-lookup"><span data-stu-id="a1acd-275">It is named the same name as your virtual network.</span></span> <span data-ttu-id="a1acd-276">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-276">Click **Connect**.</span></span> <span data-ttu-id="a1acd-277">A pop-up message may appear that refers to using the certificate.</span><span class="sxs-lookup"><span data-stu-id="a1acd-277">A pop-up message may appear that refers to using the certificate.</span></span> <span data-ttu-id="a1acd-278">Click **Continue** to use elevated privileges.</span><span class="sxs-lookup"><span data-stu-id="a1acd-278">Click **Continue** to use elevated privileges.</span></span> 
2. <span data-ttu-id="a1acd-279">On the **Connection** status page, click **Connect** to start the connection.</span><span class="sxs-lookup"><span data-stu-id="a1acd-279">On the **Connection** status page, click **Connect** to start the connection.</span></span> <span data-ttu-id="a1acd-280">If you see a **Select Certificate** screen, verify that the client certificate showing is the one that you want to use to connect.</span><span class="sxs-lookup"><span data-stu-id="a1acd-280">If you see a **Select Certificate** screen, verify that the client certificate showing is the one that you want to use to connect.</span></span> <span data-ttu-id="a1acd-281">If it is not, use the drop-down arrow to select the correct certificate, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-281">If it is not, use the drop-down arrow to select the correct certificate, and then click **OK**.</span></span>
   
    ![VPN client connects to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. <span data-ttu-id="a1acd-283">Your connection is established.</span><span class="sxs-lookup"><span data-stu-id="a1acd-283">Your connection is established.</span></span>
   
    ![Connection established](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

<span data-ttu-id="a1acd-285">If you are having trouble connecting, check the following things:</span><span class="sxs-lookup"><span data-stu-id="a1acd-285">If you are having trouble connecting, check the following things:</span></span>

- <span data-ttu-id="a1acd-286">Open **Manage user certificates** and navigate to **Trusted Root Certification Authorities\Certificates**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-286">Open **Manage user certificates** and navigate to **Trusted Root Certification Authorities\Certificates**.</span></span> <span data-ttu-id="a1acd-287">Verify that the root certificate is listed.</span><span class="sxs-lookup"><span data-stu-id="a1acd-287">Verify that the root certificate is listed.</span></span> <span data-ttu-id="a1acd-288">The root certificate must be present in order for authentication to work.</span><span class="sxs-lookup"><span data-stu-id="a1acd-288">The root certificate must be present in order for authentication to work.</span></span> <span data-ttu-id="a1acd-289">When you export a client certificate .pfx using the default value 'Include all certificates in the certification path if possible', the root certificate information is also exported.</span><span class="sxs-lookup"><span data-stu-id="a1acd-289">When you export a client certificate .pfx using the default value 'Include all certificates in the certification path if possible', the root certificate information is also exported.</span></span> <span data-ttu-id="a1acd-290">When you install the client certificate, the root certificate is then also installed on the client computer.</span><span class="sxs-lookup"><span data-stu-id="a1acd-290">When you install the client certificate, the root certificate is then also installed on the client computer.</span></span> 

- <span data-ttu-id="a1acd-291">If you are using a certificate that was issued using an Enterprise CA solution and are having trouble authenticating, check the authentication order on the client certificate.</span><span class="sxs-lookup"><span data-stu-id="a1acd-291">If you are using a certificate that was issued using an Enterprise CA solution and are having trouble authenticating, check the authentication order on the client certificate.</span></span> <span data-ttu-id="a1acd-292">You can check the authentication list order by double-clicking the client certificate, and going to **Details > Enhanced Key Usage**.</span><span class="sxs-lookup"><span data-stu-id="a1acd-292">You can check the authentication list order by double-clicking the client certificate, and going to **Details > Enhanced Key Usage**.</span></span> <span data-ttu-id="a1acd-293">Make sure the list shows 'Client Authentication' as the first item.</span><span class="sxs-lookup"><span data-stu-id="a1acd-293">Make sure the list shows 'Client Authentication' as the first item.</span></span> <span data-ttu-id="a1acd-294">If not, you need to issue a client certificate based on the User template that has Client Authentication as the first item in the list.</span><span class="sxs-lookup"><span data-stu-id="a1acd-294">If not, you need to issue a client certificate based on the User template that has Client Authentication as the first item in the list.</span></span>  


## <a name="verify"></a><span data-ttu-id="a1acd-295">Part 8 - Verify your connection</span><span class="sxs-lookup"><span data-stu-id="a1acd-295">Part 8 - Verify your connection</span></span>
1. <span data-ttu-id="a1acd-296">To verify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span><span class="sxs-lookup"><span data-stu-id="a1acd-296">To verify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span></span>
2. <span data-ttu-id="a1acd-297">View the results.</span><span class="sxs-lookup"><span data-stu-id="a1acd-297">View the results.</span></span> <span data-ttu-id="a1acd-298">Notice that the IP address you received is one of the addresses within the Point-to-Site VPN Client Address Pool that you specified in your configuration.</span><span class="sxs-lookup"><span data-stu-id="a1acd-298">Notice that the IP address you received is one of the addresses within the Point-to-Site VPN Client Address Pool that you specified in your configuration.</span></span> <span data-ttu-id="a1acd-299">The results are similar to this example:</span><span class="sxs-lookup"><span data-stu-id="a1acd-299">The results are similar to this example:</span></span>
   
        PPP adapter VNet1:
            Connection-specific DNS Suffix .:
            Description.....................: VNet1
            Physical Address................:
            DHCP Enabled....................: No
            Autoconfiguration Enabled.......: Yes
            IPv4 Address....................: 172.16.201.3(Preferred)
            Subnet Mask.....................: 255.255.255.255
            Default Gateway.................:
            NetBIOS over Tcpip..............: Enabled


## <a name="connectVM"></a><span data-ttu-id="a1acd-300">Connect to a virtual machine</span><span class="sxs-lookup"><span data-stu-id="a1acd-300">Connect to a virtual machine</span></span>

1. <span data-ttu-id="a1acd-301">After connecting to your VNet, you can connect to a VM over your P2S connection.</span><span class="sxs-lookup"><span data-stu-id="a1acd-301">After connecting to your VNet, you can connect to a VM over your P2S connection.</span></span> <span data-ttu-id="a1acd-302">To connect to the VM, you need the private IP address of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a1acd-302">To connect to the VM, you need the private IP address of the virtual machine.</span></span> <span data-ttu-id="a1acd-303">The following example helps you get the private IP address with [Get-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterface?view=azurermps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="a1acd-303">The following example helps you get the private IP address with [Get-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterface?view=azurermps-3.7.0).</span></span> <span data-ttu-id="a1acd-304">The results return a list of VMs and corresponding private IP addresses in all your Resource Groups.</span><span class="sxs-lookup"><span data-stu-id="a1acd-304">The results return a list of VMs and corresponding private IP addresses in all your Resource Groups.</span></span> 

  ```powershell   
  $vms = get-azurermvm
  $nics = get-azurermnetworkinterface | where VirtualMachine -NE $null #skip Nics with no VM
  
  foreach($nic in $nics)
  {
    $vm = $vms | where-object -Property Id -EQ $nic.VirtualMachine.id
    $prv =  $nic.IpConfigurations | select-object -ExpandProperty PrivateIpAddress
    $alloc =  $nic.IpConfigurations | select-object -ExpandProperty PrivateIpAllocationMethod
    Write-Output "$($vm.Name) : $prv , $alloc"
  }
  ```
2. <span data-ttu-id="a1acd-305">Use the following command to create a remote desktop session with the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a1acd-305">Use the following command to create a remote desktop session with the virtual machine.</span></span> <span data-ttu-id="a1acd-306">Replace the IP address with the private IP address associated with the VM that you want to connect to.</span><span class="sxs-lookup"><span data-stu-id="a1acd-306">Replace the IP address with the private IP address associated with the VM that you want to connect to.</span></span> <span data-ttu-id="a1acd-307">When prompted, enter the credentials used when creating the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a1acd-307">When prompted, enter the credentials used when creating the virtual machine.</span></span> 

  ```powershell   
  mstsc /v:192.168.1.4
  ```

<span data-ttu-id="a1acd-308">If you are having trouble connecting to a virtual machine over P2S, use 'ipconfig' to check the IPv4 address assigned to the Ethernet adapter on the computer from which you are connecting.</span><span class="sxs-lookup"><span data-stu-id="a1acd-308">If you are having trouble connecting to a virtual machine over P2S, use 'ipconfig' to check the IPv4 address assigned to the Ethernet adapter on the computer from which you are connecting.</span></span> <span data-ttu-id="a1acd-309">If the IP address is within the address range of the VNet that you are connecting to, or within the address range of your VPNClientAddressPool, this is referred to as an overlapping address space.</span><span class="sxs-lookup"><span data-stu-id="a1acd-309">If the IP address is within the address range of the VNet that you are connecting to, or within the address range of your VPNClientAddressPool, this is referred to as an overlapping address space.</span></span> <span data-ttu-id="a1acd-310">When your address space overlaps in this way, the network traffic doesn't reach Azure, it stays on the local network.</span><span class="sxs-lookup"><span data-stu-id="a1acd-310">When your address space overlaps in this way, the network traffic doesn't reach Azure, it stays on the local network.</span></span> <span data-ttu-id="a1acd-311">If your network address spaces don't overlap and you still can't connect to your VM, see [Troubleshoot Remote Desktop connections to a VM](../virtual-machines/windows/troubleshoot-rdp-connection.md).</span><span class="sxs-lookup"><span data-stu-id="a1acd-311">If your network address spaces don't overlap and you still can't connect to your VM, see [Troubleshoot Remote Desktop connections to a VM](../virtual-machines/windows/troubleshoot-rdp-connection.md).</span></span>

## <a name="addremovecert"></a><span data-ttu-id="a1acd-312">Add or remove a trusted root certificate</span><span class="sxs-lookup"><span data-stu-id="a1acd-312">Add or remove a trusted root certificate</span></span>

<span data-ttu-id="a1acd-313">You can add and remove trusted root certificates from Azure.</span><span class="sxs-lookup"><span data-stu-id="a1acd-313">You can add and remove trusted root certificates from Azure.</span></span> <span data-ttu-id="a1acd-314">When you remove a trusted certificate, the client certificates that were generated from the root certificate can't connect to Azure via Point-to-Site.</span><span class="sxs-lookup"><span data-stu-id="a1acd-314">When you remove a trusted certificate, the client certificates that were generated from the root certificate can't connect to Azure via Point-to-Site.</span></span> <span data-ttu-id="a1acd-315">If you want clients to connect, you need to install a new client certificate that is generated from a certificate that is trusted in Azure.</span><span class="sxs-lookup"><span data-stu-id="a1acd-315">If you want clients to connect, you need to install a new client certificate that is generated from a certificate that is trusted in Azure.</span></span>

### <a name="to-add-a-trusted-root-certificate"></a><span data-ttu-id="a1acd-316">To add a trusted root certificate</span><span class="sxs-lookup"><span data-stu-id="a1acd-316">To add a trusted root certificate</span></span>
<span data-ttu-id="a1acd-317">You can add up to 20 trusted root certificate .cer files to Azure.</span><span class="sxs-lookup"><span data-stu-id="a1acd-317">You can add up to 20 trusted root certificate .cer files to Azure.</span></span> <span data-ttu-id="a1acd-318">The following steps help you add a root certificate:</span><span class="sxs-lookup"><span data-stu-id="a1acd-318">The following steps help you add a root certificate:</span></span>

1. <span data-ttu-id="a1acd-319">Create and prepare the new root certificate to add to Azure.</span><span class="sxs-lookup"><span data-stu-id="a1acd-319">Create and prepare the new root certificate to add to Azure.</span></span> <span data-ttu-id="a1acd-320">Export the public key as a Base-64 encoded X.509 (.CER) and open it with a text editor.</span><span class="sxs-lookup"><span data-stu-id="a1acd-320">Export the public key as a Base-64 encoded X.509 (.CER) and open it with a text editor.</span></span> <span data-ttu-id="a1acd-321">Copy the values, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a1acd-321">Copy the values, as shown in the following example:</span></span>
   
  ![certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

    > [!NOTE]
    > When copying the certificate data, make sure that you copy the text as one continuous line without carriage returns or line feeds. You may need to modify your view in the text editor to 'Show Symbol/Show all characters' to see the carriage returns and line feeds.
  >
  >

2. <span data-ttu-id="a1acd-325">Specify the certificate name and key information as a variable.</span><span class="sxs-lookup"><span data-stu-id="a1acd-325">Specify the certificate name and key information as a variable.</span></span> <span data-ttu-id="a1acd-326">Replace the information with your own, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a1acd-326">Replace the information with your own, as shown in the following example:</span></span>

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. <span data-ttu-id="a1acd-327">Add the new root certificate.</span><span class="sxs-lookup"><span data-stu-id="a1acd-327">Add the new root certificate.</span></span> <span data-ttu-id="a1acd-328">You can only add one certificate at a time.</span><span class="sxs-lookup"><span data-stu-id="a1acd-328">You can only add one certificate at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. <span data-ttu-id="a1acd-329">You can verify that the new certificate was added correctly by using the following example:</span><span class="sxs-lookup"><span data-stu-id="a1acd-329">You can verify that the new certificate was added correctly by using the following example:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```


### <a name="to-remove-a-trusted-root-certificate"></a><span data-ttu-id="a1acd-330">To remove a trusted root certificate</span><span class="sxs-lookup"><span data-stu-id="a1acd-330">To remove a trusted root certificate</span></span>


1. <span data-ttu-id="a1acd-331">Declare the variables.</span><span class="sxs-lookup"><span data-stu-id="a1acd-331">Declare the variables.</span></span>

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. <span data-ttu-id="a1acd-332">Remove the certificate.</span><span class="sxs-lookup"><span data-stu-id="a1acd-332">Remove the certificate.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. <span data-ttu-id="a1acd-333">Use the following example to verify that the certificate was removed successfully.</span><span class="sxs-lookup"><span data-stu-id="a1acd-333">Use the following example to verify that the certificate was removed successfully.</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <a name="revoke"></a><span data-ttu-id="a1acd-334">Revoke a client certificate</span><span class="sxs-lookup"><span data-stu-id="a1acd-334">Revoke a client certificate</span></span>
<span data-ttu-id="a1acd-335">You can revoke client certificates.</span><span class="sxs-lookup"><span data-stu-id="a1acd-335">You can revoke client certificates.</span></span> <span data-ttu-id="a1acd-336">The certificate revocation list allows you to selectively deny Point-to-Site connectivity based on individual client certificates.</span><span class="sxs-lookup"><span data-stu-id="a1acd-336">The certificate revocation list allows you to selectively deny Point-to-Site connectivity based on individual client certificates.</span></span> <span data-ttu-id="a1acd-337">This differs from removing a trusted root certificate.</span><span class="sxs-lookup"><span data-stu-id="a1acd-337">This differs from removing a trusted root certificate.</span></span> <span data-ttu-id="a1acd-338">If you remove a trusted root certificate .cer from Azure, it revokes the access for all client certificates generated/signed by the revoked root certificate.</span><span class="sxs-lookup"><span data-stu-id="a1acd-338">If you remove a trusted root certificate .cer from Azure, it revokes the access for all client certificates generated/signed by the revoked root certificate.</span></span> <span data-ttu-id="a1acd-339">Revoking a client certificate, rather than the root certificate, allows the other certificates that were generated from the root certificate to continue to be used for authentication.</span><span class="sxs-lookup"><span data-stu-id="a1acd-339">Revoking a client certificate, rather than the root certificate, allows the other certificates that were generated from the root certificate to continue to be used for authentication.</span></span>

<span data-ttu-id="a1acd-340">The common practice is to use the root certificate to manage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span><span class="sxs-lookup"><span data-stu-id="a1acd-340">The common practice is to use the root certificate to manage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span></span>

### <a name="to-revoke-a-client-certificate"></a><span data-ttu-id="a1acd-341">To revoke a client certificate</span><span class="sxs-lookup"><span data-stu-id="a1acd-341">To revoke a client certificate</span></span>

1. <span data-ttu-id="a1acd-342">Retrieve the client certificate thumbprint.</span><span class="sxs-lookup"><span data-stu-id="a1acd-342">Retrieve the client certificate thumbprint.</span></span> <span data-ttu-id="a1acd-343">For more information, see [How to retrieve the Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span><span class="sxs-lookup"><span data-stu-id="a1acd-343">For more information, see [How to retrieve the Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span></span>
2. <span data-ttu-id="a1acd-344">Copy the information to a text editor and remove all spaces so that it is a continuous string.</span><span class="sxs-lookup"><span data-stu-id="a1acd-344">Copy the information to a text editor and remove all spaces so that it is a continuous string.</span></span> <span data-ttu-id="a1acd-345">This is declared as a variable in the next step.</span><span class="sxs-lookup"><span data-stu-id="a1acd-345">This is declared as a variable in the next step.</span></span>
3. <span data-ttu-id="a1acd-346">Declare the variables.</span><span class="sxs-lookup"><span data-stu-id="a1acd-346">Declare the variables.</span></span> <span data-ttu-id="a1acd-347">Make sure to declare the thumbprint you retrieved in the previous step.</span><span class="sxs-lookup"><span data-stu-id="a1acd-347">Make sure to declare the thumbprint you retrieved in the previous step.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. <span data-ttu-id="a1acd-348">Add the thumbprint to the list of revoked certificates.</span><span class="sxs-lookup"><span data-stu-id="a1acd-348">Add the thumbprint to the list of revoked certificates.</span></span> <span data-ttu-id="a1acd-349">You see "Succeeded" when the thumbprint has been added.</span><span class="sxs-lookup"><span data-stu-id="a1acd-349">You see "Succeeded" when the thumbprint has been added.</span></span>

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. <span data-ttu-id="a1acd-350">Verify that the thumbprint was added to the certificate revocation list.</span><span class="sxs-lookup"><span data-stu-id="a1acd-350">Verify that the thumbprint was added to the certificate revocation list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. <span data-ttu-id="a1acd-351">After the thumbprint has been added, the certificate can no longer be used to connect.</span><span class="sxs-lookup"><span data-stu-id="a1acd-351">After the thumbprint has been added, the certificate can no longer be used to connect.</span></span> <span data-ttu-id="a1acd-352">Clients that try to connect using this certificate receive a message saying that the certificate is no longer valid.</span><span class="sxs-lookup"><span data-stu-id="a1acd-352">Clients that try to connect using this certificate receive a message saying that the certificate is no longer valid.</span></span>

### <a name="to-reinstate-a-client-certificate"></a><span data-ttu-id="a1acd-353">To reinstate a client certificate</span><span class="sxs-lookup"><span data-stu-id="a1acd-353">To reinstate a client certificate</span></span>
<span data-ttu-id="a1acd-354">You can reinstate a client certificate by removing the thumbprint from the list of revoked client certificates.</span><span class="sxs-lookup"><span data-stu-id="a1acd-354">You can reinstate a client certificate by removing the thumbprint from the list of revoked client certificates.</span></span>

1. <span data-ttu-id="a1acd-355">Declare the variables.</span><span class="sxs-lookup"><span data-stu-id="a1acd-355">Declare the variables.</span></span> <span data-ttu-id="a1acd-356">Make sure you declare the correct thumbprint for the certificate that you want to reinstate.</span><span class="sxs-lookup"><span data-stu-id="a1acd-356">Make sure you declare the correct thumbprint for the certificate that you want to reinstate.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. <span data-ttu-id="a1acd-357">Remove the certificate thumbprint from the certificate revocation list.</span><span class="sxs-lookup"><span data-stu-id="a1acd-357">Remove the certificate thumbprint from the certificate revocation list.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. <span data-ttu-id="a1acd-358">Check if the thumbprint is removed from the revoked list.</span><span class="sxs-lookup"><span data-stu-id="a1acd-358">Check if the thumbprint is removed from the revoked list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <a name="faq"></a><span data-ttu-id="a1acd-359">Point-to-Site FAQ</span><span class="sxs-lookup"><span data-stu-id="a1acd-359">Point-to-Site FAQ</span></span>

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="a1acd-360">Next steps</span><span class="sxs-lookup"><span data-stu-id="a1acd-360">Next steps</span></span>
<span data-ttu-id="a1acd-361">Once your connection is complete, you can add virtual machines to your virtual networks.</span><span class="sxs-lookup"><span data-stu-id="a1acd-361">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="a1acd-362">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="a1acd-362">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span> <span data-ttu-id="a1acd-363">To understand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a1acd-363">To understand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span></span>



