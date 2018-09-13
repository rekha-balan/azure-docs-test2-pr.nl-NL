---
title: 'Connect a computer to an Azure virtual network using Point-to-Site and native Azure certificate authentication: PowerShell | Microsoft Docs'
description: Connect Windows and Mac OS X clients securely to Azure virtual network using P2S and self-signed or CA issued certificates. This article uses PowerShell.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: jpconnock
editor: ''
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/12/2018
ms.author: cherylmc
ms.openlocfilehash: 42afdee5ac58db005a7ecfb6388c88a974704a03
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44774364"
---
# <a name="configure-a-point-to-site-connection-to-a-vnet-using-native-azure-certificate-authentication-powershell"></a><span data-ttu-id="2faee-104">Configure a Point-to-Site connection to a VNet using native Azure certificate authentication: PowerShell</span><span class="sxs-lookup"><span data-stu-id="2faee-104">Configure a Point-to-Site connection to a VNet using native Azure certificate authentication: PowerShell</span></span>

<span data-ttu-id="2faee-105">This article helps you securely connect individual clients running Windows or Mac OS X to an Azure VNet.</span><span class="sxs-lookup"><span data-stu-id="2faee-105">This article helps you securely connect individual clients running Windows or Mac OS X to an Azure VNet.</span></span> <span data-ttu-id="2faee-106">Point-to-Site VPN connections are useful when you want to connect to your VNet from a remote location, such when you are telecommuting from home or a conference.</span><span class="sxs-lookup"><span data-stu-id="2faee-106">Point-to-Site VPN connections are useful when you want to connect to your VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="2faee-107">You can also use P2S instead of a Site-to-Site VPN when you have only a few clients that need to connect to a VNet.</span><span class="sxs-lookup"><span data-stu-id="2faee-107">You can also use P2S instead of a Site-to-Site VPN when you have only a few clients that need to connect to a VNet.</span></span> <span data-ttu-id="2faee-108">Point-to-Site connections do not require a VPN device or a public-facing IP address.</span><span class="sxs-lookup"><span data-stu-id="2faee-108">Point-to-Site connections do not require a VPN device or a public-facing IP address.</span></span> <span data-ttu-id="2faee-109">P2S creates the VPN connection over either SSTP (Secure Socket Tunneling Protocol), or IKEv2.</span><span class="sxs-lookup"><span data-stu-id="2faee-109">P2S creates the VPN connection over either SSTP (Secure Socket Tunneling Protocol), or IKEv2.</span></span> <span data-ttu-id="2faee-110">For more information about Point-to-Site VPN, see [About Point-to-Site VPN](point-to-site-about.md).</span><span class="sxs-lookup"><span data-stu-id="2faee-110">For more information about Point-to-Site VPN, see [About Point-to-Site VPN](point-to-site-about.md).</span></span>

![Connect a computer to an Azure VNet - Point-to-Site connection diagram](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/p2snativeportal.png)


## <a name="architecture"></a><span data-ttu-id="2faee-112">Architecture</span><span class="sxs-lookup"><span data-stu-id="2faee-112">Architecture</span></span>

<span data-ttu-id="2faee-113">Point-to-Site native Azure certificate authentication connections use the following items, which you configure in this exercise:</span><span class="sxs-lookup"><span data-stu-id="2faee-113">Point-to-Site native Azure certificate authentication connections use the following items, which you configure in this exercise:</span></span>

* <span data-ttu-id="2faee-114">A RouteBased VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="2faee-114">A RouteBased VPN gateway.</span></span>
* <span data-ttu-id="2faee-115">The public key (.cer file) for a root certificate, which is uploaded to Azure.</span><span class="sxs-lookup"><span data-stu-id="2faee-115">The public key (.cer file) for a root certificate, which is uploaded to Azure.</span></span> <span data-ttu-id="2faee-116">Once the certificate is uploaded, it is considered a trusted certificate and is used for authentication.</span><span class="sxs-lookup"><span data-stu-id="2faee-116">Once the certificate is uploaded, it is considered a trusted certificate and is used for authentication.</span></span>
* <span data-ttu-id="2faee-117">A client certificate that is generated from the root certificate.</span><span class="sxs-lookup"><span data-stu-id="2faee-117">A client certificate that is generated from the root certificate.</span></span> <span data-ttu-id="2faee-118">The client certificate installed on each client computer that will connect to the VNet.</span><span class="sxs-lookup"><span data-stu-id="2faee-118">The client certificate installed on each client computer that will connect to the VNet.</span></span> <span data-ttu-id="2faee-119">This certificate is used for client authentication.</span><span class="sxs-lookup"><span data-stu-id="2faee-119">This certificate is used for client authentication.</span></span>
* <span data-ttu-id="2faee-120">A VPN client configuration.</span><span class="sxs-lookup"><span data-stu-id="2faee-120">A VPN client configuration.</span></span> <span data-ttu-id="2faee-121">The VPN client configuration files contain the necessary information for the client to connect to the VNet.</span><span class="sxs-lookup"><span data-stu-id="2faee-121">The VPN client configuration files contain the necessary information for the client to connect to the VNet.</span></span> <span data-ttu-id="2faee-122">The files configure the existing VPN client that is native to the operating system.</span><span class="sxs-lookup"><span data-stu-id="2faee-122">The files configure the existing VPN client that is native to the operating system.</span></span> <span data-ttu-id="2faee-123">Each client that connects must be configured using the settings in the configuration files.</span><span class="sxs-lookup"><span data-stu-id="2faee-123">Each client that connects must be configured using the settings in the configuration files.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2faee-124">Before you begin</span><span class="sxs-lookup"><span data-stu-id="2faee-124">Before you begin</span></span>

* <span data-ttu-id="2faee-125">Verify that you have an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="2faee-125">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="2faee-126">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="2faee-126">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="2faee-127">Install the latest version of the Resource Manager PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="2faee-127">Install the latest version of the Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="2faee-128">For more information about installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2faee-128">For more information about installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="2faee-129">This is important because earlier versions of the cmdlets do not contain the current values that you need for this exercise.</span><span class="sxs-lookup"><span data-stu-id="2faee-129">This is important because earlier versions of the cmdlets do not contain the current values that you need for this exercise.</span></span>

### <a name="example"></a><span data-ttu-id="2faee-130">Example values</span><span class="sxs-lookup"><span data-stu-id="2faee-130">Example values</span></span>

<span data-ttu-id="2faee-131">You can use the example values to create a test environment, or refer to these values to better understand the examples in this article.</span><span class="sxs-lookup"><span data-stu-id="2faee-131">You can use the example values to create a test environment, or refer to these values to better understand the examples in this article.</span></span> <span data-ttu-id="2faee-132">The variables are set in section [1](#declare) of the article.</span><span class="sxs-lookup"><span data-stu-id="2faee-132">The variables are set in section [1](#declare) of the article.</span></span> <span data-ttu-id="2faee-133">You can either use the steps as a walk-through and use the values without changing them, or change them to reflect your environment.</span><span class="sxs-lookup"><span data-stu-id="2faee-133">You can either use the steps as a walk-through and use the values without changing them, or change them to reflect your environment.</span></span>

* <span data-ttu-id="2faee-134">**Name: VNet1**</span><span class="sxs-lookup"><span data-stu-id="2faee-134">**Name: VNet1**</span></span>
* <span data-ttu-id="2faee-135">**Address space: 192.168.0.0/16** and **10.254.0.0/16**</span><span class="sxs-lookup"><span data-stu-id="2faee-135">**Address space: 192.168.0.0/16** and **10.254.0.0/16**</span></span><br><span data-ttu-id="2faee-136">This example uses more than one address space to illustrate that this configuration works with multiple address spaces.</span><span class="sxs-lookup"><span data-stu-id="2faee-136">This example uses more than one address space to illustrate that this configuration works with multiple address spaces.</span></span> <span data-ttu-id="2faee-137">However, multiple address spaces are not required for this configuration.</span><span class="sxs-lookup"><span data-stu-id="2faee-137">However, multiple address spaces are not required for this configuration.</span></span>
* <span data-ttu-id="2faee-138">**Subnet name: FrontEnd**</span><span class="sxs-lookup"><span data-stu-id="2faee-138">**Subnet name: FrontEnd**</span></span>
  * <span data-ttu-id="2faee-139">**Subnet address range: 192.168.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="2faee-139">**Subnet address range: 192.168.1.0/24**</span></span>
* <span data-ttu-id="2faee-140">**Subnet name: BackEnd**</span><span class="sxs-lookup"><span data-stu-id="2faee-140">**Subnet name: BackEnd**</span></span>
  * <span data-ttu-id="2faee-141">**Subnet address range: 10.254.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="2faee-141">**Subnet address range: 10.254.1.0/24**</span></span>
* <span data-ttu-id="2faee-142">**Subnet name: GatewaySubnet**</span><span class="sxs-lookup"><span data-stu-id="2faee-142">**Subnet name: GatewaySubnet**</span></span><br><span data-ttu-id="2faee-143">The Subnet name *GatewaySubnet* is mandatory for the VPN gateway to work.</span><span class="sxs-lookup"><span data-stu-id="2faee-143">The Subnet name *GatewaySubnet* is mandatory for the VPN gateway to work.</span></span>
  * <span data-ttu-id="2faee-144">**GatewaySubnet address range: 192.168.200.0/24**</span><span class="sxs-lookup"><span data-stu-id="2faee-144">**GatewaySubnet address range: 192.168.200.0/24**</span></span> 
* <span data-ttu-id="2faee-145">**VPN client address pool: 172.16.201.0/24**</span><span class="sxs-lookup"><span data-stu-id="2faee-145">**VPN client address pool: 172.16.201.0/24**</span></span><br><span data-ttu-id="2faee-146">VPN clients that connect to the VNet using this Point-to-Site connection receive an IP address from the VPN client address pool.</span><span class="sxs-lookup"><span data-stu-id="2faee-146">VPN clients that connect to the VNet using this Point-to-Site connection receive an IP address from the VPN client address pool.</span></span>
* <span data-ttu-id="2faee-147">**Subscription:** If you have more than one subscription, verify that you are using the correct one.</span><span class="sxs-lookup"><span data-stu-id="2faee-147">**Subscription:** If you have more than one subscription, verify that you are using the correct one.</span></span>
* <span data-ttu-id="2faee-148">**Resource Group: TestRG**</span><span class="sxs-lookup"><span data-stu-id="2faee-148">**Resource Group: TestRG**</span></span>
* <span data-ttu-id="2faee-149">**Location: East US**</span><span class="sxs-lookup"><span data-stu-id="2faee-149">**Location: East US**</span></span>
* <span data-ttu-id="2faee-150">**DNS Server: IP address** of the DNS server that you want to use for name resolution.</span><span class="sxs-lookup"><span data-stu-id="2faee-150">**DNS Server: IP address** of the DNS server that you want to use for name resolution.</span></span> <span data-ttu-id="2faee-151">(optional)</span><span class="sxs-lookup"><span data-stu-id="2faee-151">(optional)</span></span>
* <span data-ttu-id="2faee-152">**GW Name: Vnet1GW**</span><span class="sxs-lookup"><span data-stu-id="2faee-152">**GW Name: Vnet1GW**</span></span>
* <span data-ttu-id="2faee-153">**Public IP name: VNet1GWPIP**</span><span class="sxs-lookup"><span data-stu-id="2faee-153">**Public IP name: VNet1GWPIP**</span></span>
* <span data-ttu-id="2faee-154">**VpnType: RouteBased**</span><span class="sxs-lookup"><span data-stu-id="2faee-154">**VpnType: RouteBased**</span></span> 

## <a name="declare"></a><span data-ttu-id="2faee-155">1. Log in and set variables</span><span class="sxs-lookup"><span data-stu-id="2faee-155">1. Log in and set variables</span></span>

<span data-ttu-id="2faee-156">In this section, you log in and declare the values used for this configuration.</span><span class="sxs-lookup"><span data-stu-id="2faee-156">In this section, you log in and declare the values used for this configuration.</span></span> <span data-ttu-id="2faee-157">The declared values are used in the sample scripts.</span><span class="sxs-lookup"><span data-stu-id="2faee-157">The declared values are used in the sample scripts.</span></span> <span data-ttu-id="2faee-158">Change the values to reflect your own environment.</span><span class="sxs-lookup"><span data-stu-id="2faee-158">Change the values to reflect your own environment.</span></span> <span data-ttu-id="2faee-159">Or, you can use the declared values and go through the steps as an exercise.</span><span class="sxs-lookup"><span data-stu-id="2faee-159">Or, you can use the declared values and go through the steps as an exercise.</span></span>

1. <span data-ttu-id="2faee-160">Open your PowerShell console with elevated privileges, and log in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="2faee-160">Open your PowerShell console with elevated privileges, and log in to your Azure account.</span></span> <span data-ttu-id="2faee-161">This cmdlet prompts you for the login credentials.</span><span class="sxs-lookup"><span data-stu-id="2faee-161">This cmdlet prompts you for the login credentials.</span></span> <span data-ttu-id="2faee-162">After logging in, it downloads your account settings so that they are available to Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2faee-162">After logging in, it downloads your account settings so that they are available to Azure PowerShell.</span></span>

  ```powershell
  Connect-AzureRmAccount
  ```
2. <span data-ttu-id="2faee-163">Get a list of your Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="2faee-163">Get a list of your Azure subscriptions.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
3. <span data-ttu-id="2faee-164">Specify the subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="2faee-164">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. <span data-ttu-id="2faee-165">Declare the variables that you want to use.</span><span class="sxs-lookup"><span data-stu-id="2faee-165">Declare the variables that you want to use.</span></span> <span data-ttu-id="2faee-166">Use the following sample, substituting the values for your own when necessary.</span><span class="sxs-lookup"><span data-stu-id="2faee-166">Use the following sample, substituting the values for your own when necessary.</span></span>

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
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <a name="ConfigureVNet"></a><span data-ttu-id="2faee-167">2. Configure a VNet</span><span class="sxs-lookup"><span data-stu-id="2faee-167">2. Configure a VNet</span></span>

1. <span data-ttu-id="2faee-168">Create a resource group.</span><span class="sxs-lookup"><span data-stu-id="2faee-168">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. <span data-ttu-id="2faee-169">Create the subnet configurations for the virtual network, naming them *FrontEnd*, *BackEnd*, and *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="2faee-169">Create the subnet configurations for the virtual network, naming them *FrontEnd*, *BackEnd*, and *GatewaySubnet*.</span></span> <span data-ttu-id="2faee-170">These prefixes must be part of the VNet address space that you declared.</span><span class="sxs-lookup"><span data-stu-id="2faee-170">These prefixes must be part of the VNet address space that you declared.</span></span>

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. <span data-ttu-id="2faee-171">Create the virtual network.</span><span class="sxs-lookup"><span data-stu-id="2faee-171">Create the virtual network.</span></span>

  <span data-ttu-id="2faee-172">In this example, the -DnsServer server parameter is optional.</span><span class="sxs-lookup"><span data-stu-id="2faee-172">In this example, the -DnsServer server parameter is optional.</span></span> <span data-ttu-id="2faee-173">Specifying a value does not create a new DNS server.</span><span class="sxs-lookup"><span data-stu-id="2faee-173">Specifying a value does not create a new DNS server.</span></span> <span data-ttu-id="2faee-174">The DNS server IP address that you specify should be a DNS server that can resolve the names for the resources you are connecting to from your VNet.</span><span class="sxs-lookup"><span data-stu-id="2faee-174">The DNS server IP address that you specify should be a DNS server that can resolve the names for the resources you are connecting to from your VNet.</span></span> <span data-ttu-id="2faee-175">This example uses a private IP address, but it is likely that this is not the IP address of your DNS server.</span><span class="sxs-lookup"><span data-stu-id="2faee-175">This example uses a private IP address, but it is likely that this is not the IP address of your DNS server.</span></span> <span data-ttu-id="2faee-176">Be sure to use your own values.</span><span class="sxs-lookup"><span data-stu-id="2faee-176">Be sure to use your own values.</span></span> <span data-ttu-id="2faee-177">The value you specify is used by the resources that you deploy to the VNet, not by the P2S connection or the VPN client.</span><span class="sxs-lookup"><span data-stu-id="2faee-177">The value you specify is used by the resources that you deploy to the VNet, not by the P2S connection or the VPN client.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer 10.2.1.3
  ```
4. <span data-ttu-id="2faee-178">Specify the variables for the virtual network you created.</span><span class="sxs-lookup"><span data-stu-id="2faee-178">Specify the variables for the virtual network you created.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="2faee-179">A VPN gateway must have a Public IP address.</span><span class="sxs-lookup"><span data-stu-id="2faee-179">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="2faee-180">You first request the IP address resource, and then refer to it when creating your virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="2faee-180">You first request the IP address resource, and then refer to it when creating your virtual network gateway.</span></span> <span data-ttu-id="2faee-181">The IP address is dynamically assigned to the resource when the VPN gateway is created.</span><span class="sxs-lookup"><span data-stu-id="2faee-181">The IP address is dynamically assigned to the resource when the VPN gateway is created.</span></span> <span data-ttu-id="2faee-182">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span><span class="sxs-lookup"><span data-stu-id="2faee-182">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="2faee-183">You cannot request a Static Public IP address assignment.</span><span class="sxs-lookup"><span data-stu-id="2faee-183">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="2faee-184">However, it doesn't mean that the IP address changes after it has been assigned to your VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="2faee-184">However, it doesn't mean that the IP address changes after it has been assigned to your VPN gateway.</span></span> <span data-ttu-id="2faee-185">The only time the Public IP address changes is when the gateway is deleted and re-created.</span><span class="sxs-lookup"><span data-stu-id="2faee-185">The only time the Public IP address changes is when the gateway is deleted and re-created.</span></span> <span data-ttu-id="2faee-186">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="2faee-186">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

  <span data-ttu-id="2faee-187">Request a dynamically assigned public IP address.</span><span class="sxs-lookup"><span data-stu-id="2faee-187">Request a dynamically assigned public IP address.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <a name="creategateway"></a><span data-ttu-id="2faee-188">3. Create the VPN gateway</span><span class="sxs-lookup"><span data-stu-id="2faee-188">3. Create the VPN gateway</span></span>

<span data-ttu-id="2faee-189">Configure and create the virtual network gateway for your VNet.</span><span class="sxs-lookup"><span data-stu-id="2faee-189">Configure and create the virtual network gateway for your VNet.</span></span>

* <span data-ttu-id="2faee-190">The -GatewayType must be **Vpn** and the -VpnType must be **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="2faee-190">The -GatewayType must be **Vpn** and the -VpnType must be **RouteBased**.</span></span>
* <span data-ttu-id="2faee-191">The -VpnClientProtocol is used to specify the types of tunnels that you would like to enable.</span><span class="sxs-lookup"><span data-stu-id="2faee-191">The -VpnClientProtocol is used to specify the types of tunnels that you would like to enable.</span></span> <span data-ttu-id="2faee-192">The two tunnel options are **SSTP** and **IKEv2**.</span><span class="sxs-lookup"><span data-stu-id="2faee-192">The two tunnel options are **SSTP** and **IKEv2**.</span></span> <span data-ttu-id="2faee-193">You can choose to enable one of them or both.</span><span class="sxs-lookup"><span data-stu-id="2faee-193">You can choose to enable one of them or both.</span></span> <span data-ttu-id="2faee-194">If you want to enable both, then specify both the names separated by a comma.</span><span class="sxs-lookup"><span data-stu-id="2faee-194">If you want to enable both, then specify both the names separated by a comma.</span></span> <span data-ttu-id="2faee-195">The strongSwan client on Android and Linux and the native IKEv2 VPN client on iOS and OSX will use only the IKEv2 tunnel to connect.</span><span class="sxs-lookup"><span data-stu-id="2faee-195">The strongSwan client on Android and Linux and the native IKEv2 VPN client on iOS and OSX will use only the IKEv2 tunnel to connect.</span></span> <span data-ttu-id="2faee-196">Windows clients try IKEv2 first and if that doesn’t connect, they fall back to SSTP.</span><span class="sxs-lookup"><span data-stu-id="2faee-196">Windows clients try IKEv2 first and if that doesn’t connect, they fall back to SSTP.</span></span>
* <span data-ttu-id="2faee-197">A VPN gateway can take up to 45 minutes to complete, depending on the [gateway sku](vpn-gateway-about-vpn-gateway-settings.md) you select.</span><span class="sxs-lookup"><span data-stu-id="2faee-197">A VPN gateway can take up to 45 minutes to complete, depending on the [gateway sku](vpn-gateway-about-vpn-gateway-settings.md) you select.</span></span> <span data-ttu-id="2faee-198">This example uses IKEv2.</span><span class="sxs-lookup"><span data-stu-id="2faee-198">This example uses IKEv2.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 -VpnClientProtocol "IKEv2"
```

## <a name="addresspool"></a><span data-ttu-id="2faee-199">4. Add the VPN client address pool</span><span class="sxs-lookup"><span data-stu-id="2faee-199">4. Add the VPN client address pool</span></span>

<span data-ttu-id="2faee-200">After the VPN gateway finishes creating, you can add the VPN client address pool.</span><span class="sxs-lookup"><span data-stu-id="2faee-200">After the VPN gateway finishes creating, you can add the VPN client address pool.</span></span> <span data-ttu-id="2faee-201">The VPN client address pool is the range from which the VPN clients receive an IP address when connecting.</span><span class="sxs-lookup"><span data-stu-id="2faee-201">The VPN client address pool is the range from which the VPN clients receive an IP address when connecting.</span></span> <span data-ttu-id="2faee-202">Use a private IP address range that does not overlap with the on-premises location that you connect from, or with the VNet that you want to connect to.</span><span class="sxs-lookup"><span data-stu-id="2faee-202">Use a private IP address range that does not overlap with the on-premises location that you connect from, or with the VNet that you want to connect to.</span></span> <span data-ttu-id="2faee-203">In this example, the VPN client address pool is declared as a [variable](#declare) in Step 1.</span><span class="sxs-lookup"><span data-stu-id="2faee-203">In this example, the VPN client address pool is declared as a [variable](#declare) in Step 1.</span></span>

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <a name="Certificates"></a><span data-ttu-id="2faee-204">5. Generate certificates</span><span class="sxs-lookup"><span data-stu-id="2faee-204">5. Generate certificates</span></span>

<span data-ttu-id="2faee-205">Certificates are used by Azure to authenticate VPN clients for Point-to-Site VPNs.</span><span class="sxs-lookup"><span data-stu-id="2faee-205">Certificates are used by Azure to authenticate VPN clients for Point-to-Site VPNs.</span></span> <span data-ttu-id="2faee-206">You upload the public key information of the root certificate to Azure.</span><span class="sxs-lookup"><span data-stu-id="2faee-206">You upload the public key information of the root certificate to Azure.</span></span> <span data-ttu-id="2faee-207">The public key is then considered 'trusted'.</span><span class="sxs-lookup"><span data-stu-id="2faee-207">The public key is then considered 'trusted'.</span></span> <span data-ttu-id="2faee-208">Client certificates must be generated from the trusted root certificate, and then installed on each client computer in the Certificates-Current User/Personal certificate store.</span><span class="sxs-lookup"><span data-stu-id="2faee-208">Client certificates must be generated from the trusted root certificate, and then installed on each client computer in the Certificates-Current User/Personal certificate store.</span></span> <span data-ttu-id="2faee-209">The certificate is used to authenticate the client when it initiates a connection to the VNet.</span><span class="sxs-lookup"><span data-stu-id="2faee-209">The certificate is used to authenticate the client when it initiates a connection to the VNet.</span></span> 

<span data-ttu-id="2faee-210">If you use self-signed certificates, they must be created using specific parameters.</span><span class="sxs-lookup"><span data-stu-id="2faee-210">If you use self-signed certificates, they must be created using specific parameters.</span></span> <span data-ttu-id="2faee-211">You can create a self-signed certificate using the instructions for [PowerShell and Windows 10](vpn-gateway-certificates-point-to-site.md), or, if you don't have Windows 10, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span><span class="sxs-lookup"><span data-stu-id="2faee-211">You can create a self-signed certificate using the instructions for [PowerShell and Windows 10](vpn-gateway-certificates-point-to-site.md), or, if you don't have Windows 10, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span></span> <span data-ttu-id="2faee-212">It's important that you follow the steps in the instructions when generating self-signed root certificates and client certificates.</span><span class="sxs-lookup"><span data-stu-id="2faee-212">It's important that you follow the steps in the instructions when generating self-signed root certificates and client certificates.</span></span> <span data-ttu-id="2faee-213">Otherwise, the certificates you generate will not be compatible with P2S connections and you receive a connection error.</span><span class="sxs-lookup"><span data-stu-id="2faee-213">Otherwise, the certificates you generate will not be compatible with P2S connections and you receive a connection error.</span></span>

### <a name="cer"></a><span data-ttu-id="2faee-214">1. Obtain the .cer file for the root certificate</span><span class="sxs-lookup"><span data-stu-id="2faee-214">1. Obtain the .cer file for the root certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <a name="generate"></a><span data-ttu-id="2faee-215">2. Generate a client certificate</span><span class="sxs-lookup"><span data-stu-id="2faee-215">2. Generate a client certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a><span data-ttu-id="2faee-216">6. Upload the root certificate public key information</span><span class="sxs-lookup"><span data-stu-id="2faee-216">6. Upload the root certificate public key information</span></span>

<span data-ttu-id="2faee-217">Verify that your VPN gateway has finished creating.</span><span class="sxs-lookup"><span data-stu-id="2faee-217">Verify that your VPN gateway has finished creating.</span></span> <span data-ttu-id="2faee-218">Once it has completed, you can upload the .cer file (which contains the public key information) for a trusted root certificate to Azure.</span><span class="sxs-lookup"><span data-stu-id="2faee-218">Once it has completed, you can upload the .cer file (which contains the public key information) for a trusted root certificate to Azure.</span></span> <span data-ttu-id="2faee-219">Once a.cer file is uploaded, Azure can use it to authenticate clients that have installed a client certificate generated from the trusted root certificate.</span><span class="sxs-lookup"><span data-stu-id="2faee-219">Once a.cer file is uploaded, Azure can use it to authenticate clients that have installed a client certificate generated from the trusted root certificate.</span></span> <span data-ttu-id="2faee-220">You can upload additional trusted root certificate files - up to a total of 20 - later, if needed.</span><span class="sxs-lookup"><span data-stu-id="2faee-220">You can upload additional trusted root certificate files - up to a total of 20 - later, if needed.</span></span>

1. <span data-ttu-id="2faee-221">Declare the variable for your certificate name, replacing the value with your own.</span><span class="sxs-lookup"><span data-stu-id="2faee-221">Declare the variable for your certificate name, replacing the value with your own.</span></span>

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. <span data-ttu-id="2faee-222">Replace the file path with your own, and then run the cmdlets.</span><span class="sxs-lookup"><span data-stu-id="2faee-222">Replace the file path with your own, and then run the cmdlets.</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. <span data-ttu-id="2faee-223">Upload the public key information to Azure.</span><span class="sxs-lookup"><span data-stu-id="2faee-223">Upload the public key information to Azure.</span></span> <span data-ttu-id="2faee-224">Once the certificate information is uploaded, Azure considers this to be a trusted root certificate.</span><span class="sxs-lookup"><span data-stu-id="2faee-224">Once the certificate information is uploaded, Azure considers this to be a trusted root certificate.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <a name="clientcertificate"></a><span data-ttu-id="2faee-225">7. Install an exported client certificate</span><span class="sxs-lookup"><span data-stu-id="2faee-225">7. Install an exported client certificate</span></span>

<span data-ttu-id="2faee-226">If you want to create a P2S connection from a client computer other than the one you used to generate the client certificates, you need to install a client certificate.</span><span class="sxs-lookup"><span data-stu-id="2faee-226">If you want to create a P2S connection from a client computer other than the one you used to generate the client certificates, you need to install a client certificate.</span></span> <span data-ttu-id="2faee-227">When installing a client certificate, you need the password that was created when the client certificate was exported.</span><span class="sxs-lookup"><span data-stu-id="2faee-227">When installing a client certificate, you need the password that was created when the client certificate was exported.</span></span>

<span data-ttu-id="2faee-228">Make sure the client certificate was exported as a .pfx along with the entire certificate chain (which is the default).</span><span class="sxs-lookup"><span data-stu-id="2faee-228">Make sure the client certificate was exported as a .pfx along with the entire certificate chain (which is the default).</span></span> <span data-ttu-id="2faee-229">Otherwise, the root certificate information isn't present on the client computer and the client won't be able to authenticate properly.</span><span class="sxs-lookup"><span data-stu-id="2faee-229">Otherwise, the root certificate information isn't present on the client computer and the client won't be able to authenticate properly.</span></span> 

<span data-ttu-id="2faee-230">For install steps, see [Install a client certificate](point-to-site-how-to-vpn-client-install-azure-cert.md).</span><span class="sxs-lookup"><span data-stu-id="2faee-230">For install steps, see [Install a client certificate](point-to-site-how-to-vpn-client-install-azure-cert.md).</span></span>

## <a name="clientconfig"></a><span data-ttu-id="2faee-231">8. Configure the native VPN client</span><span class="sxs-lookup"><span data-stu-id="2faee-231">8. Configure the native VPN client</span></span>

<span data-ttu-id="2faee-232">The VPN client configuration files contain settings to configure devices to connect to a VNet over a P2S connection.</span><span class="sxs-lookup"><span data-stu-id="2faee-232">The VPN client configuration files contain settings to configure devices to connect to a VNet over a P2S connection.</span></span> <span data-ttu-id="2faee-233">For instructions to generate and install VPN client configuration files, see [Create and install VPN client configuration files for native Azure certificate authentication P2S configurations](point-to-site-vpn-client-configuration-azure-cert.md).</span><span class="sxs-lookup"><span data-stu-id="2faee-233">For instructions to generate and install VPN client configuration files, see [Create and install VPN client configuration files for native Azure certificate authentication P2S configurations](point-to-site-vpn-client-configuration-azure-cert.md).</span></span>

## <a name="connect"></a><span data-ttu-id="2faee-234">9. Connect to Azure</span><span class="sxs-lookup"><span data-stu-id="2faee-234">9. Connect to Azure</span></span>

### <a name="to-connect-from-a-windows-vpn-client"></a><span data-ttu-id="2faee-235">To connect from a Windows VPN client</span><span class="sxs-lookup"><span data-stu-id="2faee-235">To connect from a Windows VPN client</span></span>

>[!NOTE]
><span data-ttu-id="2faee-236">You must have Administrator rights on the Windows client computer from which you are connecting.</span><span class="sxs-lookup"><span data-stu-id="2faee-236">You must have Administrator rights on the Windows client computer from which you are connecting.</span></span>
>
>

1. <span data-ttu-id="2faee-237">To connect to your VNet, on the client computer, navigate to VPN connections and locate the VPN connection that you created.</span><span class="sxs-lookup"><span data-stu-id="2faee-237">To connect to your VNet, on the client computer, navigate to VPN connections and locate the VPN connection that you created.</span></span> <span data-ttu-id="2faee-238">It is named the same name as your virtual network.</span><span class="sxs-lookup"><span data-stu-id="2faee-238">It is named the same name as your virtual network.</span></span> <span data-ttu-id="2faee-239">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="2faee-239">Click **Connect**.</span></span> <span data-ttu-id="2faee-240">A pop-up message may appear that refers to using the certificate.</span><span class="sxs-lookup"><span data-stu-id="2faee-240">A pop-up message may appear that refers to using the certificate.</span></span> <span data-ttu-id="2faee-241">Click **Continue** to use elevated privileges.</span><span class="sxs-lookup"><span data-stu-id="2faee-241">Click **Continue** to use elevated privileges.</span></span> 
2. <span data-ttu-id="2faee-242">On the **Connection** status page, click **Connect** to start the connection.</span><span class="sxs-lookup"><span data-stu-id="2faee-242">On the **Connection** status page, click **Connect** to start the connection.</span></span> <span data-ttu-id="2faee-243">If you see a **Select Certificate** screen, verify that the client certificate showing is the one that you want to use to connect.</span><span class="sxs-lookup"><span data-stu-id="2faee-243">If you see a **Select Certificate** screen, verify that the client certificate showing is the one that you want to use to connect.</span></span> <span data-ttu-id="2faee-244">If it is not, use the drop-down arrow to select the correct certificate, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="2faee-244">If it is not, use the drop-down arrow to select the correct certificate, and then click **OK**.</span></span>

  ![VPN client connects to Azure](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. <span data-ttu-id="2faee-246">Your connection is established.</span><span class="sxs-lookup"><span data-stu-id="2faee-246">Your connection is established.</span></span>

  ![Connection established](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-windows-client-p2s-connections"></a><span data-ttu-id="2faee-248">Troubleshooting Windows client P2S connections</span><span class="sxs-lookup"><span data-stu-id="2faee-248">Troubleshooting Windows client P2S connections</span></span>

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

### <a name="to-connect-from-a-mac-vpn-client"></a><span data-ttu-id="2faee-249">To connect from a Mac VPN client</span><span class="sxs-lookup"><span data-stu-id="2faee-249">To connect from a Mac VPN client</span></span>

<span data-ttu-id="2faee-250">From the Network dialog box, locate the client profile that you want to use, then click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="2faee-250">From the Network dialog box, locate the client profile that you want to use, then click **Connect**.</span></span>

  ![Mac connection](./media/vpn-gateway-howto-point-to-site-rm-ps/applyconnect.png)

## <a name="verify"></a><span data-ttu-id="2faee-252">To verify your connection</span><span class="sxs-lookup"><span data-stu-id="2faee-252">To verify your connection</span></span>

<span data-ttu-id="2faee-253">These instructions apply to Windows clients.</span><span class="sxs-lookup"><span data-stu-id="2faee-253">These instructions apply to Windows clients.</span></span>

1. <span data-ttu-id="2faee-254">To verify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span><span class="sxs-lookup"><span data-stu-id="2faee-254">To verify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span></span>
2. <span data-ttu-id="2faee-255">View the results.</span><span class="sxs-lookup"><span data-stu-id="2faee-255">View the results.</span></span> <span data-ttu-id="2faee-256">Notice that the IP address you received is one of the addresses within the Point-to-Site VPN Client Address Pool that you specified in your configuration.</span><span class="sxs-lookup"><span data-stu-id="2faee-256">Notice that the IP address you received is one of the addresses within the Point-to-Site VPN Client Address Pool that you specified in your configuration.</span></span> <span data-ttu-id="2faee-257">The results are similar to this example:</span><span class="sxs-lookup"><span data-stu-id="2faee-257">The results are similar to this example:</span></span>

  ```
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
  ```

## <a name="connectVM"></a><span data-ttu-id="2faee-258">To connect to a virtual machine</span><span class="sxs-lookup"><span data-stu-id="2faee-258">To connect to a virtual machine</span></span>

<span data-ttu-id="2faee-259">These instructions apply to Windows clients.</span><span class="sxs-lookup"><span data-stu-id="2faee-259">These instructions apply to Windows clients.</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <a name="addremovecert"></a><span data-ttu-id="2faee-260">To add or remove a root certificate</span><span class="sxs-lookup"><span data-stu-id="2faee-260">To add or remove a root certificate</span></span>

<span data-ttu-id="2faee-261">You can add and remove trusted root certificates from Azure.</span><span class="sxs-lookup"><span data-stu-id="2faee-261">You can add and remove trusted root certificates from Azure.</span></span> <span data-ttu-id="2faee-262">When you remove a root certificate, clients that have a certificate generated from the root certificate can't authenticate and won't be able to connect.</span><span class="sxs-lookup"><span data-stu-id="2faee-262">When you remove a root certificate, clients that have a certificate generated from the root certificate can't authenticate and won't be able to connect.</span></span> <span data-ttu-id="2faee-263">If you want a client to authenticate and connect, you need to install a new client certificate generated from a root certificate that is trusted (uploaded) to Azure.</span><span class="sxs-lookup"><span data-stu-id="2faee-263">If you want a client to authenticate and connect, you need to install a new client certificate generated from a root certificate that is trusted (uploaded) to Azure.</span></span>

### <a name="addtrustedroot"></a><span data-ttu-id="2faee-264">To add a trusted root certificate</span><span class="sxs-lookup"><span data-stu-id="2faee-264">To add a trusted root certificate</span></span>

<span data-ttu-id="2faee-265">You can add up to 20 root certificate .cer files to Azure.</span><span class="sxs-lookup"><span data-stu-id="2faee-265">You can add up to 20 root certificate .cer files to Azure.</span></span> <span data-ttu-id="2faee-266">The following steps help you add a root certificate:</span><span class="sxs-lookup"><span data-stu-id="2faee-266">The following steps help you add a root certificate:</span></span>

#### <a name="certmethod1"></a><span data-ttu-id="2faee-267">Method 1</span><span class="sxs-lookup"><span data-stu-id="2faee-267">Method 1</span></span>

<span data-ttu-id="2faee-268">This is the most efficient method to upload a root certificate.</span><span class="sxs-lookup"><span data-stu-id="2faee-268">This is the most efficient method to upload a root certificate.</span></span>

1. <span data-ttu-id="2faee-269">Prepare the .cer file to upload:</span><span class="sxs-lookup"><span data-stu-id="2faee-269">Prepare the .cer file to upload:</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. <span data-ttu-id="2faee-270">Upload the file.</span><span class="sxs-lookup"><span data-stu-id="2faee-270">Upload the file.</span></span> <span data-ttu-id="2faee-271">You can only upload one file at a time.</span><span class="sxs-lookup"><span data-stu-id="2faee-271">You can only upload one file at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. <span data-ttu-id="2faee-272">To verify that the certificate file uploaded:</span><span class="sxs-lookup"><span data-stu-id="2faee-272">To verify that the certificate file uploaded:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <a name="certmethod2"></a><span data-ttu-id="2faee-273">Method 2</span><span class="sxs-lookup"><span data-stu-id="2faee-273">Method 2</span></span>

<span data-ttu-id="2faee-274">This method has more steps than Method 1, but has the same result.</span><span class="sxs-lookup"><span data-stu-id="2faee-274">This method has more steps than Method 1, but has the same result.</span></span> <span data-ttu-id="2faee-275">It is included in case you need to view the certificate data.</span><span class="sxs-lookup"><span data-stu-id="2faee-275">It is included in case you need to view the certificate data.</span></span>

1. <span data-ttu-id="2faee-276">Create and prepare the new root certificate to add to Azure.</span><span class="sxs-lookup"><span data-stu-id="2faee-276">Create and prepare the new root certificate to add to Azure.</span></span> <span data-ttu-id="2faee-277">Export the public key as a Base-64 encoded X.509 (.CER) and open it with a text editor.</span><span class="sxs-lookup"><span data-stu-id="2faee-277">Export the public key as a Base-64 encoded X.509 (.CER) and open it with a text editor.</span></span> <span data-ttu-id="2faee-278">Copy the values, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="2faee-278">Copy the values, as shown in the following example:</span></span>

  ![certificate](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > <span data-ttu-id="2faee-280">When copying the certificate data, make sure that you copy the text as one continuous line without carriage returns or line feeds.</span><span class="sxs-lookup"><span data-stu-id="2faee-280">When copying the certificate data, make sure that you copy the text as one continuous line without carriage returns or line feeds.</span></span> <span data-ttu-id="2faee-281">You may need to modify your view in the text editor to 'Show Symbol/Show all characters' to see the carriage returns and line feeds.</span><span class="sxs-lookup"><span data-stu-id="2faee-281">You may need to modify your view in the text editor to 'Show Symbol/Show all characters' to see the carriage returns and line feeds.</span></span>
  >
  >

2. <span data-ttu-id="2faee-282">Specify the certificate name and key information as a variable.</span><span class="sxs-lookup"><span data-stu-id="2faee-282">Specify the certificate name and key information as a variable.</span></span> <span data-ttu-id="2faee-283">Replace the information with your own, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="2faee-283">Replace the information with your own, as shown in the following example:</span></span>

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. <span data-ttu-id="2faee-284">Add the new root certificate.</span><span class="sxs-lookup"><span data-stu-id="2faee-284">Add the new root certificate.</span></span> <span data-ttu-id="2faee-285">You can only add one certificate at a time.</span><span class="sxs-lookup"><span data-stu-id="2faee-285">You can only add one certificate at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. <span data-ttu-id="2faee-286">You can verify that the new certificate was added correctly by using the following example:</span><span class="sxs-lookup"><span data-stu-id="2faee-286">You can verify that the new certificate was added correctly by using the following example:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <a name="removerootcert"></a><span data-ttu-id="2faee-287">To remove a root certificate</span><span class="sxs-lookup"><span data-stu-id="2faee-287">To remove a root certificate</span></span>

1. <span data-ttu-id="2faee-288">Declare the variables.</span><span class="sxs-lookup"><span data-stu-id="2faee-288">Declare the variables.</span></span>

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. <span data-ttu-id="2faee-289">Remove the certificate.</span><span class="sxs-lookup"><span data-stu-id="2faee-289">Remove the certificate.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. <span data-ttu-id="2faee-290">Use the following example to verify that the certificate was removed successfully.</span><span class="sxs-lookup"><span data-stu-id="2faee-290">Use the following example to verify that the certificate was removed successfully.</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <a name="revoke"></a><span data-ttu-id="2faee-291">To revoke a client certificate</span><span class="sxs-lookup"><span data-stu-id="2faee-291">To revoke a client certificate</span></span>

<span data-ttu-id="2faee-292">You can revoke client certificates.</span><span class="sxs-lookup"><span data-stu-id="2faee-292">You can revoke client certificates.</span></span> <span data-ttu-id="2faee-293">The certificate revocation list allows you to selectively deny Point-to-Site connectivity based on individual client certificates.</span><span class="sxs-lookup"><span data-stu-id="2faee-293">The certificate revocation list allows you to selectively deny Point-to-Site connectivity based on individual client certificates.</span></span> <span data-ttu-id="2faee-294">This is different than removing a trusted root certificate.</span><span class="sxs-lookup"><span data-stu-id="2faee-294">This is different than removing a trusted root certificate.</span></span> <span data-ttu-id="2faee-295">If you remove a trusted root certificate .cer from Azure, it revokes the access for all client certificates generated/signed by the revoked root certificate.</span><span class="sxs-lookup"><span data-stu-id="2faee-295">If you remove a trusted root certificate .cer from Azure, it revokes the access for all client certificates generated/signed by the revoked root certificate.</span></span> <span data-ttu-id="2faee-296">Revoking a client certificate, rather than the root certificate, allows the other certificates that were generated from the root certificate to continue to be used for authentication.</span><span class="sxs-lookup"><span data-stu-id="2faee-296">Revoking a client certificate, rather than the root certificate, allows the other certificates that were generated from the root certificate to continue to be used for authentication.</span></span>

<span data-ttu-id="2faee-297">The common practice is to use the root certificate to manage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span><span class="sxs-lookup"><span data-stu-id="2faee-297">The common practice is to use the root certificate to manage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span></span>

### <a name="revokeclientcert"></a><span data-ttu-id="2faee-298">Revoke a client certificate</span><span class="sxs-lookup"><span data-stu-id="2faee-298">Revoke a client certificate</span></span>

1. <span data-ttu-id="2faee-299">Retrieve the client certificate thumbprint.</span><span class="sxs-lookup"><span data-stu-id="2faee-299">Retrieve the client certificate thumbprint.</span></span> <span data-ttu-id="2faee-300">For more information, see [How to retrieve the Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span><span class="sxs-lookup"><span data-stu-id="2faee-300">For more information, see [How to retrieve the Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span></span>
2. <span data-ttu-id="2faee-301">Copy the information to a text editor and remove all spaces so that it is a continuous string.</span><span class="sxs-lookup"><span data-stu-id="2faee-301">Copy the information to a text editor and remove all spaces so that it is a continuous string.</span></span> <span data-ttu-id="2faee-302">This string is declared as a variable in the next step.</span><span class="sxs-lookup"><span data-stu-id="2faee-302">This string is declared as a variable in the next step.</span></span>
3. <span data-ttu-id="2faee-303">Declare the variables.</span><span class="sxs-lookup"><span data-stu-id="2faee-303">Declare the variables.</span></span> <span data-ttu-id="2faee-304">Make sure to declare the thumbprint you retrieved in the previous step.</span><span class="sxs-lookup"><span data-stu-id="2faee-304">Make sure to declare the thumbprint you retrieved in the previous step.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. <span data-ttu-id="2faee-305">Add the thumbprint to the list of revoked certificates.</span><span class="sxs-lookup"><span data-stu-id="2faee-305">Add the thumbprint to the list of revoked certificates.</span></span> <span data-ttu-id="2faee-306">You see "Succeeded" when the thumbprint has been added.</span><span class="sxs-lookup"><span data-stu-id="2faee-306">You see "Succeeded" when the thumbprint has been added.</span></span>

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. <span data-ttu-id="2faee-307">Verify that the thumbprint was added to the certificate revocation list.</span><span class="sxs-lookup"><span data-stu-id="2faee-307">Verify that the thumbprint was added to the certificate revocation list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. <span data-ttu-id="2faee-308">After the thumbprint has been added, the certificate can no longer be used to connect.</span><span class="sxs-lookup"><span data-stu-id="2faee-308">After the thumbprint has been added, the certificate can no longer be used to connect.</span></span> <span data-ttu-id="2faee-309">Clients that try to connect using this certificate receive a message saying that the certificate is no longer valid.</span><span class="sxs-lookup"><span data-stu-id="2faee-309">Clients that try to connect using this certificate receive a message saying that the certificate is no longer valid.</span></span>

### <a name="reinstateclientcert"></a><span data-ttu-id="2faee-310">To reinstate a client certificate</span><span class="sxs-lookup"><span data-stu-id="2faee-310">To reinstate a client certificate</span></span>

<span data-ttu-id="2faee-311">You can reinstate a client certificate by removing the thumbprint from the list of revoked client certificates.</span><span class="sxs-lookup"><span data-stu-id="2faee-311">You can reinstate a client certificate by removing the thumbprint from the list of revoked client certificates.</span></span>

1. <span data-ttu-id="2faee-312">Declare the variables.</span><span class="sxs-lookup"><span data-stu-id="2faee-312">Declare the variables.</span></span> <span data-ttu-id="2faee-313">Make sure you declare the correct thumbprint for the certificate that you want to reinstate.</span><span class="sxs-lookup"><span data-stu-id="2faee-313">Make sure you declare the correct thumbprint for the certificate that you want to reinstate.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. <span data-ttu-id="2faee-314">Remove the certificate thumbprint from the certificate revocation list.</span><span class="sxs-lookup"><span data-stu-id="2faee-314">Remove the certificate thumbprint from the certificate revocation list.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. <span data-ttu-id="2faee-315">Check if the thumbprint is removed from the revoked list.</span><span class="sxs-lookup"><span data-stu-id="2faee-315">Check if the thumbprint is removed from the revoked list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <a name="faq"></a><span data-ttu-id="2faee-316">Point-to-Site FAQ</span><span class="sxs-lookup"><span data-stu-id="2faee-316">Point-to-Site FAQ</span></span>

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-faq-p2s-azurecert-include.md)]

## <a name="next-steps"></a><span data-ttu-id="2faee-317">Next steps</span><span class="sxs-lookup"><span data-stu-id="2faee-317">Next steps</span></span>
<span data-ttu-id="2faee-318">Once your connection is complete, you can add virtual machines to your virtual networks.</span><span class="sxs-lookup"><span data-stu-id="2faee-318">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="2faee-319">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="2faee-319">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span> <span data-ttu-id="2faee-320">To understand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2faee-320">To understand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span></span>

<span data-ttu-id="2faee-321">For P2S troubleshooting information, [Troubleshooting: Azure point-to-site connection problems](vpn-gateway-troubleshoot-vpn-point-to-site-connection-problems.md).</span><span class="sxs-lookup"><span data-stu-id="2faee-321">For P2S troubleshooting information, [Troubleshooting: Azure point-to-site connection problems](vpn-gateway-troubleshoot-vpn-point-to-site-connection-problems.md).</span></span>
