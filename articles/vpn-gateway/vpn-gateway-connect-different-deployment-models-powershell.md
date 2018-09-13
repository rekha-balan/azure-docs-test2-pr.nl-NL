---
title: 'Connect classic virtual networks to Azure Resource Manager VNets: PowerShell | Microsoft Docs'
description: Learn how to create a VPN connection between classic VNets and Resource Manager VNets using VPN Gateway and PowerShell
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
tags: azure-service-management,azure-resource-manager
ms.assetid: f17c3bf0-5cc9-4629-9928-1b72d0c9340b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: cherylmc
ms.openlocfilehash: 49384bc101f89f613dad30591c3fcb2144f96276
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549509"
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a><span data-ttu-id="dba50-103">Connect virtual networks from different deployment models using PowerShell</span><span class="sxs-lookup"><span data-stu-id="dba50-103">Connect virtual networks from different deployment models using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

<span data-ttu-id="dba50-106">Azure currently has two management models: classic and Resource Manager (RM).</span><span class="sxs-lookup"><span data-stu-id="dba50-106">Azure currently has two management models: classic and Resource Manager (RM).</span></span> <span data-ttu-id="dba50-107">If you have been using Azure for some time, you probably have Azure VMs and instance roles running in a classic VNet.</span><span class="sxs-lookup"><span data-stu-id="dba50-107">If you have been using Azure for some time, you probably have Azure VMs and instance roles running in a classic VNet.</span></span> <span data-ttu-id="dba50-108">Your newer VMs and role instances may be running in a VNet created in Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dba50-108">Your newer VMs and role instances may be running in a VNet created in Resource Manager.</span></span>

<span data-ttu-id="dba50-109">This article walks you through connecting classic VNets to Resource Manager VNets to allow the resources located in the separate deployment models to communicate with each other over a gateway connection.</span><span class="sxs-lookup"><span data-stu-id="dba50-109">This article walks you through connecting classic VNets to Resource Manager VNets to allow the resources located in the separate deployment models to communicate with each other over a gateway connection.</span></span> [!INCLUDE [vpn-gateway-vnetpeeringlink](../../includes/vpn-gateway-vnetpeeringlink-include.md)]

<span data-ttu-id="dba50-110">You can create a connection between VNets that are in different subscriptions and in different regions.</span><span class="sxs-lookup"><span data-stu-id="dba50-110">You can create a connection between VNets that are in different subscriptions and in different regions.</span></span> <span data-ttu-id="dba50-111">You can also connect VNets that already have connections to on-premises networks, as long as the gateway that they have been configured with is dynamic or route-based.</span><span class="sxs-lookup"><span data-stu-id="dba50-111">You can also connect VNets that already have connections to on-premises networks, as long as the gateway that they have been configured with is dynamic or route-based.</span></span> <span data-ttu-id="dba50-112">For more information about VNet-to-VNet connections, see the [VNet-to-VNet FAQ](#faq) at the end of this article.</span><span class="sxs-lookup"><span data-stu-id="dba50-112">For more information about VNet-to-VNet connections, see the [VNet-to-VNet FAQ](#faq) at the end of this article.</span></span> 



## <a name="before-beginning"></a><span data-ttu-id="dba50-113">Before beginning</span><span class="sxs-lookup"><span data-stu-id="dba50-113">Before beginning</span></span>
<span data-ttu-id="dba50-114">The following steps walk you through the settings necessary to configure a dynamic or route-based gateway for each VNet and create a VPN connection between the gateways.</span><span class="sxs-lookup"><span data-stu-id="dba50-114">The following steps walk you through the settings necessary to configure a dynamic or route-based gateway for each VNet and create a VPN connection between the gateways.</span></span> <span data-ttu-id="dba50-115">This configuration does not support static or policy-based gateways.</span><span class="sxs-lookup"><span data-stu-id="dba50-115">This configuration does not support static or policy-based gateways.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="dba50-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dba50-116">Prerequisites</span></span>
* <span data-ttu-id="dba50-117">Both VNets have already been created.</span><span class="sxs-lookup"><span data-stu-id="dba50-117">Both VNets have already been created.</span></span>
* <span data-ttu-id="dba50-118">The address ranges for the VNets do not overlap with each other, or overlap with any of the ranges for other connections that the gateways may be connected to.</span><span class="sxs-lookup"><span data-stu-id="dba50-118">The address ranges for the VNets do not overlap with each other, or overlap with any of the ranges for other connections that the gateways may be connected to.</span></span>
* <span data-ttu-id="dba50-119">You have installed the latest PowerShell cmdlets (1.0.2 or later).</span><span class="sxs-lookup"><span data-stu-id="dba50-119">You have installed the latest PowerShell cmdlets (1.0.2 or later).</span></span> <span data-ttu-id="dba50-120">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information.</span><span class="sxs-lookup"><span data-stu-id="dba50-120">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information.</span></span> <span data-ttu-id="dba50-121">Make sure you install both the Service Management (SM) and the Resource Manager (RM) cmdlets.</span><span class="sxs-lookup"><span data-stu-id="dba50-121">Make sure you install both the Service Management (SM) and the Resource Manager (RM) cmdlets.</span></span> 

### <a name="exampleref"></a><span data-ttu-id="dba50-122">Example settings</span><span class="sxs-lookup"><span data-stu-id="dba50-122">Example settings</span></span>
<span data-ttu-id="dba50-123">You can use the example settings as a reference.</span><span class="sxs-lookup"><span data-stu-id="dba50-123">You can use the example settings as a reference.</span></span>

<span data-ttu-id="dba50-124">**Classic VNet settings**</span><span class="sxs-lookup"><span data-stu-id="dba50-124">**Classic VNet settings**</span></span>

<span data-ttu-id="dba50-125">VNet Name = ClassicVNet</span><span class="sxs-lookup"><span data-stu-id="dba50-125">VNet Name = ClassicVNet</span></span> <br>
<span data-ttu-id="dba50-126">Location = West US</span><span class="sxs-lookup"><span data-stu-id="dba50-126">Location = West US</span></span> <br>
<span data-ttu-id="dba50-127">Virtual Network Address Spaces = 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="dba50-127">Virtual Network Address Spaces = 10.0.0.0/24</span></span> <br>
<span data-ttu-id="dba50-128">Subnet-1 = 10.0.0.0/27</span><span class="sxs-lookup"><span data-stu-id="dba50-128">Subnet-1 = 10.0.0.0/27</span></span> <br>
<span data-ttu-id="dba50-129">GatewaySubnet = 10.0.0.32/29</span><span class="sxs-lookup"><span data-stu-id="dba50-129">GatewaySubnet = 10.0.0.32/29</span></span> <br>
<span data-ttu-id="dba50-130">Local Network Name = RMVNetLocal</span><span class="sxs-lookup"><span data-stu-id="dba50-130">Local Network Name = RMVNetLocal</span></span> <br>
<span data-ttu-id="dba50-131">GatewayType = DynamicRouting</span><span class="sxs-lookup"><span data-stu-id="dba50-131">GatewayType = DynamicRouting</span></span>

<span data-ttu-id="dba50-132">**Resource Manager VNet settings**</span><span class="sxs-lookup"><span data-stu-id="dba50-132">**Resource Manager VNet settings**</span></span>

<span data-ttu-id="dba50-133">VNet Name = RMVNet</span><span class="sxs-lookup"><span data-stu-id="dba50-133">VNet Name = RMVNet</span></span> <br>
<span data-ttu-id="dba50-134">Resource Group = RG1</span><span class="sxs-lookup"><span data-stu-id="dba50-134">Resource Group = RG1</span></span> <br>
<span data-ttu-id="dba50-135">Virtual Network IP Address Spaces = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="dba50-135">Virtual Network IP Address Spaces = 192.168.0.0/16</span></span> <br>
<span data-ttu-id="dba50-136">Subnet-1 = 192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="dba50-136">Subnet-1 = 192.168.1.0/24</span></span> <br>
<span data-ttu-id="dba50-137">GatewaySubnet = 192.168.0.0/26</span><span class="sxs-lookup"><span data-stu-id="dba50-137">GatewaySubnet = 192.168.0.0/26</span></span> <br>
<span data-ttu-id="dba50-138">Location = East US</span><span class="sxs-lookup"><span data-stu-id="dba50-138">Location = East US</span></span> <br>
<span data-ttu-id="dba50-139">Gateway public IP name = gwpip</span><span class="sxs-lookup"><span data-stu-id="dba50-139">Gateway public IP name = gwpip</span></span> <br>
<span data-ttu-id="dba50-140">Local Network Gateway = ClassicVNetLocal</span><span class="sxs-lookup"><span data-stu-id="dba50-140">Local Network Gateway = ClassicVNetLocal</span></span> <br>
<span data-ttu-id="dba50-141">Virtual Network Gateway name = RMGateway</span><span class="sxs-lookup"><span data-stu-id="dba50-141">Virtual Network Gateway name = RMGateway</span></span> <br>
<span data-ttu-id="dba50-142">Gateway IP addressing configuration = gwipconfig</span><span class="sxs-lookup"><span data-stu-id="dba50-142">Gateway IP addressing configuration = gwipconfig</span></span>

## <a name="createsmgw"></a><span data-ttu-id="dba50-143">Section 1 - Configure the classic VNet</span><span class="sxs-lookup"><span data-stu-id="dba50-143">Section 1 - Configure the classic VNet</span></span>
### <a name="part-1---download-your-network-configuration-file"></a><span data-ttu-id="dba50-144">Part 1 - Download your network configuration file</span><span class="sxs-lookup"><span data-stu-id="dba50-144">Part 1 - Download your network configuration file</span></span>
1. <span data-ttu-id="dba50-145">Log in to your Azure account in the PowerShell console with elevated rights.</span><span class="sxs-lookup"><span data-stu-id="dba50-145">Log in to your Azure account in the PowerShell console with elevated rights.</span></span> <span data-ttu-id="dba50-146">The following cmdlet prompts you for the login credentials for your Azure Account.</span><span class="sxs-lookup"><span data-stu-id="dba50-146">The following cmdlet prompts you for the login credentials for your Azure Account.</span></span> <span data-ttu-id="dba50-147">After logging in, it downloads your account settings so that they are available to Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dba50-147">After logging in, it downloads your account settings so that they are available to Azure PowerShell.</span></span> <span data-ttu-id="dba50-148">You use the SM PowerShell cmdlets to complete this part of the configuration.</span><span class="sxs-lookup"><span data-stu-id="dba50-148">You use the SM PowerShell cmdlets to complete this part of the configuration.</span></span>

  ```powershell
  Add-AzureAccount
  ```
2. <span data-ttu-id="dba50-149">Export your Azure network configuration file by running the following command.</span><span class="sxs-lookup"><span data-stu-id="dba50-149">Export your Azure network configuration file by running the following command.</span></span> <span data-ttu-id="dba50-150">You can change the location of the file to export to a different location if necessary.</span><span class="sxs-lookup"><span data-stu-id="dba50-150">You can change the location of the file to export to a different location if necessary.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. <span data-ttu-id="dba50-151">Open the .xml file that you downloaded to edit it.</span><span class="sxs-lookup"><span data-stu-id="dba50-151">Open the .xml file that you downloaded to edit it.</span></span> <span data-ttu-id="dba50-152">For an example of the network configuration file, see the [Network Configuration Schema](https://msdn.microsoft.com/library/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="dba50-152">For an example of the network configuration file, see the [Network Configuration Schema](https://msdn.microsoft.com/library/jj157100.aspx).</span></span>

### <a name="part-2--verify-the-gateway-subnet"></a><span data-ttu-id="dba50-153">Part 2 -Verify the gateway subnet</span><span class="sxs-lookup"><span data-stu-id="dba50-153">Part 2 -Verify the gateway subnet</span></span>
<span data-ttu-id="dba50-154">In the **VirtualNetworkSites** element, add a gateway subnet to your VNet if one has not already been created.</span><span class="sxs-lookup"><span data-stu-id="dba50-154">In the **VirtualNetworkSites** element, add a gateway subnet to your VNet if one has not already been created.</span></span> <span data-ttu-id="dba50-155">When working with the network configuration file, the gateway subnet MUST be named "GatewaySubnet" or Azure cannot recognize and use it as a gateway subnet.</span><span class="sxs-lookup"><span data-stu-id="dba50-155">When working with the network configuration file, the gateway subnet MUST be named "GatewaySubnet" or Azure cannot recognize and use it as a gateway subnet.</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="dba50-156">**Example:**</span><span class="sxs-lookup"><span data-stu-id="dba50-156">**Example:**</span></span>

    <VirtualNetworkSites>
      <VirtualNetworkSite name="ClassicVNet" Location="West US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/24</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Subnet-1">
            <AddressPrefix>10.0.0.0/27</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.0.0.32/29</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>

### <a name="part-3---add-the-local-network-site"></a><span data-ttu-id="dba50-157">Part 3 - Add the local network site</span><span class="sxs-lookup"><span data-stu-id="dba50-157">Part 3 - Add the local network site</span></span>
<span data-ttu-id="dba50-158">The local network site you add represents the RM VNet to which you want to connect.</span><span class="sxs-lookup"><span data-stu-id="dba50-158">The local network site you add represents the RM VNet to which you want to connect.</span></span> <span data-ttu-id="dba50-159">Add a **LocalNetworkSites** element to the file if one doesn't already exist.</span><span class="sxs-lookup"><span data-stu-id="dba50-159">Add a **LocalNetworkSites** element to the file if one doesn't already exist.</span></span> <span data-ttu-id="dba50-160">At this point in the configuration, the VPNGatewayAddress can be any valid public IP address because we haven't yet created the gateway for the Resource Manager VNet.</span><span class="sxs-lookup"><span data-stu-id="dba50-160">At this point in the configuration, the VPNGatewayAddress can be any valid public IP address because we haven't yet created the gateway for the Resource Manager VNet.</span></span> <span data-ttu-id="dba50-161">Once we create the gateway, we replace this placeholder IP address with the correct public IP address that has been assigned to the RM gateway.</span><span class="sxs-lookup"><span data-stu-id="dba50-161">Once we create the gateway, we replace this placeholder IP address with the correct public IP address that has been assigned to the RM gateway.</span></span>

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-the-vnet-with-the-local-network-site"></a><span data-ttu-id="dba50-162">Part 4 - Associate the VNet with the local network site</span><span class="sxs-lookup"><span data-stu-id="dba50-162">Part 4 - Associate the VNet with the local network site</span></span>
<span data-ttu-id="dba50-163">In this section, we specify the local network site that you want to connect the VNet to.</span><span class="sxs-lookup"><span data-stu-id="dba50-163">In this section, we specify the local network site that you want to connect the VNet to.</span></span> <span data-ttu-id="dba50-164">In this case, it is the Resource Manager VNet that you referenced earlier.</span><span class="sxs-lookup"><span data-stu-id="dba50-164">In this case, it is the Resource Manager VNet that you referenced earlier.</span></span> <span data-ttu-id="dba50-165">Make sure the names match.</span><span class="sxs-lookup"><span data-stu-id="dba50-165">Make sure the names match.</span></span> <span data-ttu-id="dba50-166">This step does not create a gateway.</span><span class="sxs-lookup"><span data-stu-id="dba50-166">This step does not create a gateway.</span></span> <span data-ttu-id="dba50-167">It specifies the local network that the gateway will connect to.</span><span class="sxs-lookup"><span data-stu-id="dba50-167">It specifies the local network that the gateway will connect to.</span></span>

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-the-file-and-upload"></a><span data-ttu-id="dba50-168">Part 5 - Save the file and upload</span><span class="sxs-lookup"><span data-stu-id="dba50-168">Part 5 - Save the file and upload</span></span>
<span data-ttu-id="dba50-169">Save the file, then import it to Azure by running the following command.</span><span class="sxs-lookup"><span data-stu-id="dba50-169">Save the file, then import it to Azure by running the following command.</span></span> <span data-ttu-id="dba50-170">Make sure you change the file path as necessary for your environment.</span><span class="sxs-lookup"><span data-stu-id="dba50-170">Make sure you change the file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="dba50-171">You will see a similar result showing that the import succeeded.</span><span class="sxs-lookup"><span data-stu-id="dba50-171">You will see a similar result showing that the import succeeded.</span></span>

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-the-gateway"></a><span data-ttu-id="dba50-172">Part 6 - Create the gateway</span><span class="sxs-lookup"><span data-stu-id="dba50-172">Part 6 - Create the gateway</span></span>

<span data-ttu-id="dba50-173">Before running this example, refer to the network configuration file that you downloaded for the exact names that Azure expects to see.</span><span class="sxs-lookup"><span data-stu-id="dba50-173">Before running this example, refer to the network configuration file that you downloaded for the exact names that Azure expects to see.</span></span> <span data-ttu-id="dba50-174">The network configuration file contains the values for your classic virtual networks.</span><span class="sxs-lookup"><span data-stu-id="dba50-174">The network configuration file contains the values for your classic virtual networks.</span></span> <span data-ttu-id="dba50-175">Sometimes the names for classic VNets are changed in the network configuration file when creating classic VNet settings in the Azure portal due to the differences in the deployment models.</span><span class="sxs-lookup"><span data-stu-id="dba50-175">Sometimes the names for classic VNets are changed in the network configuration file when creating classic VNet settings in the Azure portal due to the differences in the deployment models.</span></span> <span data-ttu-id="dba50-176">For example, if you used the Azure portal to create a classic VNet named 'Classic VNet' and created it in a resource group named 'ClassicRG', the name that is contained in the network configuration file is converted to 'Group ClassicRG Classic VNet'.</span><span class="sxs-lookup"><span data-stu-id="dba50-176">For example, if you used the Azure portal to create a classic VNet named 'Classic VNet' and created it in a resource group named 'ClassicRG', the name that is contained in the network configuration file is converted to 'Group ClassicRG Classic VNet'.</span></span> <span data-ttu-id="dba50-177">When specifying the name of a VNet that contains spaces, use quotation marks around the value.</span><span class="sxs-lookup"><span data-stu-id="dba50-177">When specifying the name of a VNet that contains spaces, use quotation marks around the value.</span></span>


<span data-ttu-id="dba50-178">Use the following example to create a dynamic routing gateway:</span><span class="sxs-lookup"><span data-stu-id="dba50-178">Use the following example to create a dynamic routing gateway:</span></span>

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

<span data-ttu-id="dba50-179">You can check the status of the gateway by using the **Get-AzureVNetGateway** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dba50-179">You can check the status of the gateway by using the **Get-AzureVNetGateway** cmdlet.</span></span>

## <a name="creatermgw"></a><span data-ttu-id="dba50-180">Section 2: Configure the RM VNet gateway</span><span class="sxs-lookup"><span data-stu-id="dba50-180">Section 2: Configure the RM VNet gateway</span></span>
<span data-ttu-id="dba50-181">To create a VPN gateway for the RM VNet, follow the following instructions.</span><span class="sxs-lookup"><span data-stu-id="dba50-181">To create a VPN gateway for the RM VNet, follow the following instructions.</span></span> <span data-ttu-id="dba50-182">Don't start the steps until after you have retrieved the public IP address for the classic VNet's gateway.</span><span class="sxs-lookup"><span data-stu-id="dba50-182">Don't start the steps until after you have retrieved the public IP address for the classic VNet's gateway.</span></span> 

1. <span data-ttu-id="dba50-183">Log in to your Azure account in the PowerShell console.</span><span class="sxs-lookup"><span data-stu-id="dba50-183">Log in to your Azure account in the PowerShell console.</span></span> <span data-ttu-id="dba50-184">The following cmdlet prompts you for the login credentials for your Azure Account.</span><span class="sxs-lookup"><span data-stu-id="dba50-184">The following cmdlet prompts you for the login credentials for your Azure Account.</span></span> <span data-ttu-id="dba50-185">After logging in, your account settings are downloaded so that they are available to Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dba50-185">After logging in, your account settings are downloaded so that they are available to Azure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  <span data-ttu-id="dba50-186">Get a list of your Azure subscriptions if you have more than one subscription.</span><span class="sxs-lookup"><span data-stu-id="dba50-186">Get a list of your Azure subscriptions if you have more than one subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
   
  <span data-ttu-id="dba50-187">Specify the subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="dba50-187">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="dba50-188">Create a local network gateway.</span><span class="sxs-lookup"><span data-stu-id="dba50-188">Create a local network gateway.</span></span> <span data-ttu-id="dba50-189">In a virtual network, the local network gateway typically refers to your on-premises location.</span><span class="sxs-lookup"><span data-stu-id="dba50-189">In a virtual network, the local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="dba50-190">In this case, the local network gateway refers to your Classic VNet.</span><span class="sxs-lookup"><span data-stu-id="dba50-190">In this case, the local network gateway refers to your Classic VNet.</span></span> <span data-ttu-id="dba50-191">Give it a name by which Azure can refer to it, and also specify the address space prefix.</span><span class="sxs-lookup"><span data-stu-id="dba50-191">Give it a name by which Azure can refer to it, and also specify the address space prefix.</span></span> <span data-ttu-id="dba50-192">Azure uses the IP address prefix you specify to identify which traffic to send to your on-premises location.</span><span class="sxs-lookup"><span data-stu-id="dba50-192">Azure uses the IP address prefix you specify to identify which traffic to send to your on-premises location.</span></span> <span data-ttu-id="dba50-193">If you need to adjust the information here later, before creating your gateway, you can modify the values and run the sample again.</span><span class="sxs-lookup"><span data-stu-id="dba50-193">If you need to adjust the information here later, before creating your gateway, you can modify the values and run the sample again.</span></span>
   
   <span data-ttu-id="dba50-194">**-Name** is the name you want to assign to refer to the local network gateway.</span><span class="sxs-lookup"><span data-stu-id="dba50-194">**-Name** is the name you want to assign to refer to the local network gateway.</span></span><br>
   <span data-ttu-id="dba50-195">**-AddressPrefix** is the Address Space for your classic VNet.</span><span class="sxs-lookup"><span data-stu-id="dba50-195">**-AddressPrefix** is the Address Space for your classic VNet.</span></span><br>
   <span data-ttu-id="dba50-196">**-GatewayIpAddress** is the public IP address of the classic VNet's gateway.</span><span class="sxs-lookup"><span data-stu-id="dba50-196">**-GatewayIpAddress** is the public IP address of the classic VNet's gateway.</span></span> <span data-ttu-id="dba50-197">Be sure to change the following sample to reflect the correct IP address.</span><span class="sxs-lookup"><span data-stu-id="dba50-197">Be sure to change the following sample to reflect the correct IP address.</span></span><br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. <span data-ttu-id="dba50-198">Request a public IP address to be allocated to the virtual network gateway for the Resource Manager VNet.</span><span class="sxs-lookup"><span data-stu-id="dba50-198">Request a public IP address to be allocated to the virtual network gateway for the Resource Manager VNet.</span></span> <span data-ttu-id="dba50-199">You can't specify the IP address that you want to use.</span><span class="sxs-lookup"><span data-stu-id="dba50-199">You can't specify the IP address that you want to use.</span></span> <span data-ttu-id="dba50-200">The IP address is dynamically allocated to the virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="dba50-200">The IP address is dynamically allocated to the virtual network gateway.</span></span> <span data-ttu-id="dba50-201">However, this does not mean the IP address changes.</span><span class="sxs-lookup"><span data-stu-id="dba50-201">However, this does not mean the IP address changes.</span></span> <span data-ttu-id="dba50-202">The only time the virtual network gateway IP address changes is when the gateway is deleted and recreated.</span><span class="sxs-lookup"><span data-stu-id="dba50-202">The only time the virtual network gateway IP address changes is when the gateway is deleted and recreated.</span></span> <span data-ttu-id="dba50-203">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of the gateway.</span><span class="sxs-lookup"><span data-stu-id="dba50-203">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of the gateway.</span></span>

  <span data-ttu-id="dba50-204">In this step, we also set a variable that is used in a later step.</span><span class="sxs-lookup"><span data-stu-id="dba50-204">In this step, we also set a variable that is used in a later step.</span></span>

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. <span data-ttu-id="dba50-205">Verify that your virtual network has a gateway subnet.</span><span class="sxs-lookup"><span data-stu-id="dba50-205">Verify that your virtual network has a gateway subnet.</span></span> <span data-ttu-id="dba50-206">If no gateway subnet exists, add one.</span><span class="sxs-lookup"><span data-stu-id="dba50-206">If no gateway subnet exists, add one.</span></span> <span data-ttu-id="dba50-207">Make sure the gateway subnet is named *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="dba50-207">Make sure the gateway subnet is named *GatewaySubnet*.</span></span>
5. <span data-ttu-id="dba50-208">Retrieve the subnet used for the gateway by running the following command.</span><span class="sxs-lookup"><span data-stu-id="dba50-208">Retrieve the subnet used for the gateway by running the following command.</span></span> <span data-ttu-id="dba50-209">In this step, we also set a variable to be used in the next step.</span><span class="sxs-lookup"><span data-stu-id="dba50-209">In this step, we also set a variable to be used in the next step.</span></span>
   
   <span data-ttu-id="dba50-210">**-Name** is the name of your Resource Manager VNet.</span><span class="sxs-lookup"><span data-stu-id="dba50-210">**-Name** is the name of your Resource Manager VNet.</span></span><br>
   <span data-ttu-id="dba50-211">**-ResourceGroupName** is the resource group that the VNet is associated with.</span><span class="sxs-lookup"><span data-stu-id="dba50-211">**-ResourceGroupName** is the resource group that the VNet is associated with.</span></span> <span data-ttu-id="dba50-212">The gateway subnet must already exist for this VNet and must be named *GatewaySubnet* to work properly.</span><span class="sxs-lookup"><span data-stu-id="dba50-212">The gateway subnet must already exist for this VNet and must be named *GatewaySubnet* to work properly.</span></span><br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. <span data-ttu-id="dba50-213">Create the gateway IP addressing configuration.</span><span class="sxs-lookup"><span data-stu-id="dba50-213">Create the gateway IP addressing configuration.</span></span> <span data-ttu-id="dba50-214">The gateway configuration defines the subnet and the public IP address to use.</span><span class="sxs-lookup"><span data-stu-id="dba50-214">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="dba50-215">Use the following sample to create your gateway configuration.</span><span class="sxs-lookup"><span data-stu-id="dba50-215">Use the following sample to create your gateway configuration.</span></span>

  <span data-ttu-id="dba50-216">In this step, the **-SubnetId** and **-PublicIpAddressId** parameters must be passed the id property from the subnet, and IP address objects, respectively.</span><span class="sxs-lookup"><span data-stu-id="dba50-216">In this step, the **-SubnetId** and **-PublicIpAddressId** parameters must be passed the id property from the subnet, and IP address objects, respectively.</span></span> <span data-ttu-id="dba50-217">You can't use a simple string.</span><span class="sxs-lookup"><span data-stu-id="dba50-217">You can't use a simple string.</span></span> <span data-ttu-id="dba50-218">These variables are set in the step to request a public IP and the step to retrieve the subnet.</span><span class="sxs-lookup"><span data-stu-id="dba50-218">These variables are set in the step to request a public IP and the step to retrieve the subnet.</span></span>

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. <span data-ttu-id="dba50-219">Create the Resource Manager virtual network gateway by running the following command.</span><span class="sxs-lookup"><span data-stu-id="dba50-219">Create the Resource Manager virtual network gateway by running the following command.</span></span> <span data-ttu-id="dba50-220">The `-VpnType` must be *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="dba50-220">The `-VpnType` must be *RouteBased*.</span></span> <span data-ttu-id="dba50-221">It can take 45 minutes or more for the gateway to create.</span><span class="sxs-lookup"><span data-stu-id="dba50-221">It can take 45 minutes or more for the gateway to create.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. <span data-ttu-id="dba50-222">Copy the public IP address once the VPN gateway has been created.</span><span class="sxs-lookup"><span data-stu-id="dba50-222">Copy the public IP address once the VPN gateway has been created.</span></span> <span data-ttu-id="dba50-223">You use it when you configure the local network settings for your Classic VNet.</span><span class="sxs-lookup"><span data-stu-id="dba50-223">You use it when you configure the local network settings for your Classic VNet.</span></span> <span data-ttu-id="dba50-224">You can use the following cmdlet to retrieve the public IP address.</span><span class="sxs-lookup"><span data-stu-id="dba50-224">You can use the following cmdlet to retrieve the public IP address.</span></span> <span data-ttu-id="dba50-225">The public IP address is listed in the return as *IpAddress*.</span><span class="sxs-lookup"><span data-stu-id="dba50-225">The public IP address is listed in the return as *IpAddress*.</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-the-classic-vnet-local-site-settings"></a><span data-ttu-id="dba50-226">Section 3: Modify the classic VNet local site settings</span><span class="sxs-lookup"><span data-stu-id="dba50-226">Section 3: Modify the classic VNet local site settings</span></span>

<span data-ttu-id="dba50-227">In this section, you work with the classic VNet.</span><span class="sxs-lookup"><span data-stu-id="dba50-227">In this section, you work with the classic VNet.</span></span> <span data-ttu-id="dba50-228">You replace the placeholder IP address that you used when specifying the local site settings that will be used to connect to the Resource Manager VNet gateway.</span><span class="sxs-lookup"><span data-stu-id="dba50-228">You replace the placeholder IP address that you used when specifying the local site settings that will be used to connect to the Resource Manager VNet gateway.</span></span> 

1. <span data-ttu-id="dba50-229">Export the network configuration file.</span><span class="sxs-lookup"><span data-stu-id="dba50-229">Export the network configuration file.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. <span data-ttu-id="dba50-230">Using a text editor, modify the value for VPNGatewayAddress.</span><span class="sxs-lookup"><span data-stu-id="dba50-230">Using a text editor, modify the value for VPNGatewayAddress.</span></span> <span data-ttu-id="dba50-231">Replace the placeholder IP address with the public IP address of the Resource Manager gateway and then save the changes.</span><span class="sxs-lookup"><span data-stu-id="dba50-231">Replace the placeholder IP address with the public IP address of the Resource Manager gateway and then save the changes.</span></span>

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. <span data-ttu-id="dba50-232">Import the modified network configuration file to Azure.</span><span class="sxs-lookup"><span data-stu-id="dba50-232">Import the modified network configuration file to Azure.</span></span>

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <a name="connect"></a><span data-ttu-id="dba50-233">Section 4: Create a connection between the gateways</span><span class="sxs-lookup"><span data-stu-id="dba50-233">Section 4: Create a connection between the gateways</span></span>
<span data-ttu-id="dba50-234">Creating a connection between the gateways requires PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dba50-234">Creating a connection between the gateways requires PowerShell.</span></span> <span data-ttu-id="dba50-235">You may need to add your Azure Account to use the classic PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="dba50-235">You may need to add your Azure Account to use the classic PowerShell cmdlets.</span></span> <span data-ttu-id="dba50-236">To do so, use **Add-AzureAccount**.</span><span class="sxs-lookup"><span data-stu-id="dba50-236">To do so, use **Add-AzureAccount**.</span></span>

1. <span data-ttu-id="dba50-237">In the PowerShell console, set your shared key.</span><span class="sxs-lookup"><span data-stu-id="dba50-237">In the PowerShell console, set your shared key.</span></span> <span data-ttu-id="dba50-238">Before running the cmdlets, refer to the network configuration file that you downloaded for the exact names that Azure expects to see.</span><span class="sxs-lookup"><span data-stu-id="dba50-238">Before running the cmdlets, refer to the network configuration file that you downloaded for the exact names that Azure expects to see.</span></span> <span data-ttu-id="dba50-239">When specifying the name of a VNet that contains spaces, use single quotation marks around the value.</span><span class="sxs-lookup"><span data-stu-id="dba50-239">When specifying the name of a VNet that contains spaces, use single quotation marks around the value.</span></span><br><br><span data-ttu-id="dba50-240">In following example, **-VNetName** is the name of the classic VNet and **-LocalNetworkSiteName** is the name you specified for the local network site.</span><span class="sxs-lookup"><span data-stu-id="dba50-240">In following example, **-VNetName** is the name of the classic VNet and **-LocalNetworkSiteName** is the name you specified for the local network site.</span></span> <span data-ttu-id="dba50-241">The **-SharedKey** is a value that you generate and specify.</span><span class="sxs-lookup"><span data-stu-id="dba50-241">The **-SharedKey** is a value that you generate and specify.</span></span> <span data-ttu-id="dba50-242">In the example, we used 'abc123', but you can generate and use something more complex.</span><span class="sxs-lookup"><span data-stu-id="dba50-242">In the example, we used 'abc123', but you can generate and use something more complex.</span></span> <span data-ttu-id="dba50-243">The important thing is that the value you specify here must be the same value that you specify in the next step when you create your connection.</span><span class="sxs-lookup"><span data-stu-id="dba50-243">The important thing is that the value you specify here must be the same value that you specify in the next step when you create your connection.</span></span> <span data-ttu-id="dba50-244">The return should show **Status: Successful**.</span><span class="sxs-lookup"><span data-stu-id="dba50-244">The return should show **Status: Successful**.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. <span data-ttu-id="dba50-245">Create the VPN connection by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="dba50-245">Create the VPN connection by running the following commands:</span></span>
   
  <span data-ttu-id="dba50-246">Set the variables.</span><span class="sxs-lookup"><span data-stu-id="dba50-246">Set the variables.</span></span>

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  <span data-ttu-id="dba50-247">Create the connection.</span><span class="sxs-lookup"><span data-stu-id="dba50-247">Create the connection.</span></span> <span data-ttu-id="dba50-248">Notice that the **-ConnectionType** is IPsec, not Vnet2Vnet.</span><span class="sxs-lookup"><span data-stu-id="dba50-248">Notice that the **-ConnectionType** is IPsec, not Vnet2Vnet.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a><span data-ttu-id="dba50-249">Section 5: Verify your connections</span><span class="sxs-lookup"><span data-stu-id="dba50-249">Section 5: Verify your connections</span></span>

### <a name="to-verify-the-connection-from-your-classic-vnet-to-your-resource-manager-vnet"></a><span data-ttu-id="dba50-250">To verify the connection from your classic VNet to your Resource Manager VNet</span><span class="sxs-lookup"><span data-stu-id="dba50-250">To verify the connection from your classic VNet to your Resource Manager VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="dba50-251">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dba50-251">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="dba50-252">Azure portal</span><span class="sxs-lookup"><span data-stu-id="dba50-252">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="to-verify-the-connection-from-your-resource-manager-vnet-to-your-classic-vnet"></a><span data-ttu-id="dba50-253">To verify the connection from your Resource Manager VNet to your classic VNet</span><span class="sxs-lookup"><span data-stu-id="dba50-253">To verify the connection from your Resource Manager VNet to your classic VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="dba50-254">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dba50-254">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="dba50-255">Azure portal</span><span class="sxs-lookup"><span data-stu-id="dba50-255">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="faq"></a><span data-ttu-id="dba50-256">VNet-to-VNet considerations</span><span class="sxs-lookup"><span data-stu-id="dba50-256">VNet-to-VNet considerations</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

