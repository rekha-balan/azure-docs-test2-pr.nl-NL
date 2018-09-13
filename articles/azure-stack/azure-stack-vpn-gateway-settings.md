---
title: VPN gateway settings for Azure Stack | Microsoft Docs
description: Learn about settings for VPN gateways you use with Azure Stack.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: fa8d3adc-8f5a-4b4f-8227-4381cf952c56
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2018
ms.author: brenduns
ms.openlocfilehash: 6380936766bb0f3848811be305783c274867b0fc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868348"
---
# <a name="vpn-gateway-configuration-settings-for-azure-stack"></a><span data-ttu-id="5f12b-103">VPN gateway configuration settings for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5f12b-103">VPN gateway configuration settings for Azure Stack</span></span>

<span data-ttu-id="5f12b-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="5f12b-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="5f12b-105">A VPN gateway is a type of virtual network gateway that sends encrypted traffic between your virtual network in Azure Stack and a remote VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="5f12b-105">A VPN gateway is a type of virtual network gateway that sends encrypted traffic between your virtual network in Azure Stack and a remote VPN gateway.</span></span> <span data-ttu-id="5f12b-106">The remote VPN gateway can be in Azure, a device in your datacenter or a device in another site.</span><span class="sxs-lookup"><span data-stu-id="5f12b-106">The remote VPN gateway can be in Azure, a device in your datacenter or a device in another site.</span></span>  <span data-ttu-id="5f12b-107">If there is network connectivity between the two endpoints, you can establish a secure Site-to-Site (S2S) VPN connection between the two networks.</span><span class="sxs-lookup"><span data-stu-id="5f12b-107">If there is network connectivity between the two endpoints, you can establish a secure Site-to-Site (S2S) VPN connection between the two networks.</span></span>

<span data-ttu-id="5f12b-108">A VPN gateway connection relies on the configuration of multiple resources, each of which contains configurable settings.</span><span class="sxs-lookup"><span data-stu-id="5f12b-108">A VPN gateway connection relies on the configuration of multiple resources, each of which contains configurable settings.</span></span> <span data-ttu-id="5f12b-109">This article discusses the resources and settings that relate to a VPN gateway for a virtual network that you create in the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="5f12b-109">This article discusses the resources and settings that relate to a VPN gateway for a virtual network that you create in the Resource Manager deployment model.</span></span> <span data-ttu-id="5f12b-110">You can find descriptions and topology diagrams for each connection solution in [About VPN Gateway for Azure Stack](azure-stack-vpn-gateway-about-vpn-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="5f12b-110">You can find descriptions and topology diagrams for each connection solution in [About VPN Gateway for Azure Stack](azure-stack-vpn-gateway-about-vpn-gateways.md).</span></span>

## <a name="vpn-gateway-settings"></a><span data-ttu-id="5f12b-111">VPN gateway settings</span><span class="sxs-lookup"><span data-stu-id="5f12b-111">VPN gateway settings</span></span>

### <a name="gateway-types"></a><span data-ttu-id="5f12b-112">Gateway types</span><span class="sxs-lookup"><span data-stu-id="5f12b-112">Gateway types</span></span>

<span data-ttu-id="5f12b-113">Each Azure Stack virtual network supports a single virtual network gateway, which must be of the type **Vpn**.</span><span class="sxs-lookup"><span data-stu-id="5f12b-113">Each Azure Stack virtual network supports a single virtual network gateway, which must be of the type **Vpn**.</span></span>  <span data-ttu-id="5f12b-114">This support differs from Azure, which supports additional types.</span><span class="sxs-lookup"><span data-stu-id="5f12b-114">This support differs from Azure, which supports additional types.</span></span>  

<span data-ttu-id="5f12b-115">When you're creating a virtual network gateway, you must make sure that the gateway type is correct for your configuration.</span><span class="sxs-lookup"><span data-stu-id="5f12b-115">When you're creating a virtual network gateway, you must make sure that the gateway type is correct for your configuration.</span></span> <span data-ttu-id="5f12b-116">A VPN gateway requires the `-GatewayType Vpn`, for example:</span><span class="sxs-lookup"><span data-stu-id="5f12b-116">A VPN gateway requires the `-GatewayType Vpn`, for example:</span></span>

```PowerShell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn
-VpnType RouteBased
```

### <a name="gateway-skus"></a><span data-ttu-id="5f12b-117">Gateway SKUs</span><span class="sxs-lookup"><span data-stu-id="5f12b-117">Gateway SKUs</span></span>

<span data-ttu-id="5f12b-118">When you create a virtual network gateway, you need to specify the gateway SKU that you want to use.</span><span class="sxs-lookup"><span data-stu-id="5f12b-118">When you create a virtual network gateway, you need to specify the gateway SKU that you want to use.</span></span> <span data-ttu-id="5f12b-119">Select the SKUs that satisfy your requirements based on the types of workloads, throughputs, features, and SLAs.</span><span class="sxs-lookup"><span data-stu-id="5f12b-119">Select the SKUs that satisfy your requirements based on the types of workloads, throughputs, features, and SLAs.</span></span>

<span data-ttu-id="5f12b-120">Azure Stack offers the VPN gateway SKUs shown in the following table.</span><span class="sxs-lookup"><span data-stu-id="5f12b-120">Azure Stack offers the VPN gateway SKUs shown in the following table.</span></span>

|   | <span data-ttu-id="5f12b-121">VPN Gateway throughput</span><span class="sxs-lookup"><span data-stu-id="5f12b-121">VPN Gateway throughput</span></span> |<span data-ttu-id="5f12b-122">VPN Gateway max IPsec tunnels</span><span class="sxs-lookup"><span data-stu-id="5f12b-122">VPN Gateway max IPsec tunnels</span></span> |
|-------|-------|-------|
|<span data-ttu-id="5f12b-123">**Basic SKU**</span><span class="sxs-lookup"><span data-stu-id="5f12b-123">**Basic SKU**</span></span>  | <span data-ttu-id="5f12b-124">100 Mbps</span><span class="sxs-lookup"><span data-stu-id="5f12b-124">100 Mbps</span></span>  | <span data-ttu-id="5f12b-125">10</span><span class="sxs-lookup"><span data-stu-id="5f12b-125">10</span></span>    |
|<span data-ttu-id="5f12b-126">**Standard SKU**</span><span class="sxs-lookup"><span data-stu-id="5f12b-126">**Standard SKU**</span></span>           | <span data-ttu-id="5f12b-127">100 Mbps</span><span class="sxs-lookup"><span data-stu-id="5f12b-127">100 Mbps</span></span>  | <span data-ttu-id="5f12b-128">10</span><span class="sxs-lookup"><span data-stu-id="5f12b-128">10</span></span>    |
|<span data-ttu-id="5f12b-129">**High Performance SKU**</span><span class="sxs-lookup"><span data-stu-id="5f12b-129">**High Performance SKU**</span></span> | <span data-ttu-id="5f12b-130">200 Mbps</span><span class="sxs-lookup"><span data-stu-id="5f12b-130">200 Mbps</span></span>    | <span data-ttu-id="5f12b-131">5</span><span class="sxs-lookup"><span data-stu-id="5f12b-131">5</span></span> |

### <a name="resizing-gateway-skus"></a><span data-ttu-id="5f12b-132">Resizing gateway SKUs</span><span class="sxs-lookup"><span data-stu-id="5f12b-132">Resizing gateway SKUs</span></span>

<span data-ttu-id="5f12b-133">Azure Stack doesn't support a resize of SKUs between the supported legacy SKUs.</span><span class="sxs-lookup"><span data-stu-id="5f12b-133">Azure Stack doesn't support a resize of SKUs between the supported legacy SKUs.</span></span>

<span data-ttu-id="5f12b-134">Similarly, Azure Stack doesn't support a resize from a supported legacy SKU (Basic, Standard, and HighPerformance) to a newer SKU supported by Azure (VpnGw1, VpnGw2, and VpnGw3.)</span><span class="sxs-lookup"><span data-stu-id="5f12b-134">Similarly, Azure Stack doesn't support a resize from a supported legacy SKU (Basic, Standard, and HighPerformance) to a newer SKU supported by Azure (VpnGw1, VpnGw2, and VpnGw3.)</span></span>

### <a name="configure-the-gateway-sku"></a><span data-ttu-id="5f12b-135">Configure the gateway SKU</span><span class="sxs-lookup"><span data-stu-id="5f12b-135">Configure the gateway SKU</span></span>

#### <a name="azure-stack-portal"></a><span data-ttu-id="5f12b-136">Azure Stack portal</span><span class="sxs-lookup"><span data-stu-id="5f12b-136">Azure Stack portal</span></span>

<span data-ttu-id="5f12b-137">If you use the Azure Stack portal to create a Resource Manager virtual network gateway, you can select the gateway SKU by using the dropdown list.</span><span class="sxs-lookup"><span data-stu-id="5f12b-137">If you use the Azure Stack portal to create a Resource Manager virtual network gateway, you can select the gateway SKU by using the dropdown list.</span></span> <span data-ttu-id="5f12b-138">The options you're presented with correspond to the Gateway type and VPN type that you select.</span><span class="sxs-lookup"><span data-stu-id="5f12b-138">The options you're presented with correspond to the Gateway type and VPN type that you select.</span></span>

#### <a name="powershell"></a><span data-ttu-id="5f12b-139">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f12b-139">PowerShell</span></span>

<span data-ttu-id="5f12b-140">The following PowerShell example specifies the **-GatewaySku** as VpnGw1.</span><span class="sxs-lookup"><span data-stu-id="5f12b-140">The following PowerShell example specifies the **-GatewaySku** as VpnGw1.</span></span>

```PowerShell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1
-GatewayType Vpn -VpnType RouteBased
```

### <a name="connection-types"></a><span data-ttu-id="5f12b-141">Connection types</span><span class="sxs-lookup"><span data-stu-id="5f12b-141">Connection types</span></span>

<span data-ttu-id="5f12b-142">In the Resource Manager deployment model, each configuration requires a specific virtual network gateway connection type.</span><span class="sxs-lookup"><span data-stu-id="5f12b-142">In the Resource Manager deployment model, each configuration requires a specific virtual network gateway connection type.</span></span> <span data-ttu-id="5f12b-143">The available Resource Manager PowerShell values for **-ConnectionType** are:</span><span class="sxs-lookup"><span data-stu-id="5f12b-143">The available Resource Manager PowerShell values for **-ConnectionType** are:</span></span>

* <span data-ttu-id="5f12b-144">IPsec</span><span class="sxs-lookup"><span data-stu-id="5f12b-144">IPsec</span></span>

<span data-ttu-id="5f12b-145">In the following PowerShell example, a S2S connection is created that requires the IPsec connection type.</span><span class="sxs-lookup"><span data-stu-id="5f12b-145">In the following PowerShell example, a S2S connection is created that requires the IPsec connection type.</span></span>

```PowerShell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

### <a name="vpn-types"></a><span data-ttu-id="5f12b-146">VPN types</span><span class="sxs-lookup"><span data-stu-id="5f12b-146">VPN types</span></span>

<span data-ttu-id="5f12b-147">When you create the virtual network gateway for a VPN gateway configuration, you must specify a VPN type.</span><span class="sxs-lookup"><span data-stu-id="5f12b-147">When you create the virtual network gateway for a VPN gateway configuration, you must specify a VPN type.</span></span> <span data-ttu-id="5f12b-148">The VPN type that you choose depends on the connection topology that you want to create.</span><span class="sxs-lookup"><span data-stu-id="5f12b-148">The VPN type that you choose depends on the connection topology that you want to create.</span></span>  <span data-ttu-id="5f12b-149">A VPN type can also depend on the hardware that you're using.</span><span class="sxs-lookup"><span data-stu-id="5f12b-149">A VPN type can also depend on the hardware that you're using.</span></span> <span data-ttu-id="5f12b-150">S2S configurations require a VPN device.</span><span class="sxs-lookup"><span data-stu-id="5f12b-150">S2S configurations require a VPN device.</span></span> <span data-ttu-id="5f12b-151">Some VPN devices only support a certain VPN type.</span><span class="sxs-lookup"><span data-stu-id="5f12b-151">Some VPN devices only support a certain VPN type.</span></span>

> [!IMPORTANT]  
> <span data-ttu-id="5f12b-152">Currently, Azure Stack only supports the Route Based VPN type.</span><span class="sxs-lookup"><span data-stu-id="5f12b-152">Currently, Azure Stack only supports the Route Based VPN type.</span></span> <span data-ttu-id="5f12b-153">If your device only supports Policy Based VPNs, then connections to those devices from Azure Stack aren't supported.</span><span class="sxs-lookup"><span data-stu-id="5f12b-153">If your device only supports Policy Based VPNs, then connections to those devices from Azure Stack aren't supported.</span></span>  
>
> <span data-ttu-id="5f12b-154">In addition, Azure Stack doesn't support using Policy Based Traffic Selectors for Route Based Gateways at this time, because custom IPSec/IKE policy configurations aren't supported.</span><span class="sxs-lookup"><span data-stu-id="5f12b-154">In addition, Azure Stack doesn't support using Policy Based Traffic Selectors for Route Based Gateways at this time, because custom IPSec/IKE policy configurations aren't supported.</span></span>

* <span data-ttu-id="5f12b-155">**PolicyBased**: Policy-based VPNs encrypt and direct packets through IPsec tunnels based on the IPsec policies that are configured with the combinations of address prefixes between your on-premises network and the Azure Stack VNet.</span><span class="sxs-lookup"><span data-stu-id="5f12b-155">**PolicyBased**: Policy-based VPNs encrypt and direct packets through IPsec tunnels based on the IPsec policies that are configured with the combinations of address prefixes between your on-premises network and the Azure Stack VNet.</span></span> <span data-ttu-id="5f12b-156">The policy, or traffic selector, is usually an access list in the VPN device configuration.</span><span class="sxs-lookup"><span data-stu-id="5f12b-156">The policy, or traffic selector, is usually an access list in the VPN device configuration.</span></span>

  >[!NOTE]
  ><span data-ttu-id="5f12b-157">PolicyBased is supported in Azure, but not in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5f12b-157">PolicyBased is supported in Azure, but not in Azure Stack.</span></span>

* <span data-ttu-id="5f12b-158">**RouteBased**: RouteBased VPNs use routes that are configured in the IP forwarding or routing table to direct packets to their corresponding tunnel interfaces.</span><span class="sxs-lookup"><span data-stu-id="5f12b-158">**RouteBased**: RouteBased VPNs use routes that are configured in the IP forwarding or routing table to direct packets to their corresponding tunnel interfaces.</span></span> <span data-ttu-id="5f12b-159">The tunnel interfaces then encrypt or decrypt the packets in and out of the tunnels.</span><span class="sxs-lookup"><span data-stu-id="5f12b-159">The tunnel interfaces then encrypt or decrypt the packets in and out of the tunnels.</span></span> <span data-ttu-id="5f12b-160">The policy, or traffic selector, for RouteBased VPNs are configured as any-to-any (or use wild cards.) By default, they can't be changed.</span><span class="sxs-lookup"><span data-stu-id="5f12b-160">The policy, or traffic selector, for RouteBased VPNs are configured as any-to-any (or use wild cards.) By default, they can't be changed.</span></span> <span data-ttu-id="5f12b-161">The value for a RouteBased VPN type is RouteBased.</span><span class="sxs-lookup"><span data-stu-id="5f12b-161">The value for a RouteBased VPN type is RouteBased.</span></span>

<span data-ttu-id="5f12b-162">The following PowerShell example specifies the **-VpnType** as RouteBased.</span><span class="sxs-lookup"><span data-stu-id="5f12b-162">The following PowerShell example specifies the **-VpnType** as RouteBased.</span></span> <span data-ttu-id="5f12b-163">When you're creating a gateway, you must make sure that the **-VpnType** is correct for your configuration.</span><span class="sxs-lookup"><span data-stu-id="5f12b-163">When you're creating a gateway, you must make sure that the **-VpnType** is correct for your configuration.</span></span>

```PowerShell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
-Location 'West US' -IpConfigurations $gwipconfig
-GatewayType Vpn -VpnType RouteBased
```

### <a name="gateway-requirements"></a><span data-ttu-id="5f12b-164">Gateway requirements</span><span class="sxs-lookup"><span data-stu-id="5f12b-164">Gateway requirements</span></span>

<span data-ttu-id="5f12b-165">The following table lists the requirements for VPN gateways.</span><span class="sxs-lookup"><span data-stu-id="5f12b-165">The following table lists the requirements for VPN gateways.</span></span>

| |<span data-ttu-id="5f12b-166">PolicyBased Basic VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="5f12b-166">PolicyBased Basic VPN Gateway</span></span> | <span data-ttu-id="5f12b-167">RouteBased Basic VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="5f12b-167">RouteBased Basic VPN Gateway</span></span> | <span data-ttu-id="5f12b-168">RouteBased Standard VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="5f12b-168">RouteBased Standard VPN Gateway</span></span> | <span data-ttu-id="5f12b-169">RouteBased High Performance VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="5f12b-169">RouteBased High Performance VPN Gateway</span></span>|
|--|--|--|--|--|
| <span data-ttu-id="5f12b-170">**Site-to-Site connectivity (S2S connectivity)**</span><span class="sxs-lookup"><span data-stu-id="5f12b-170">**Site-to-Site connectivity (S2S connectivity)**</span></span> | <span data-ttu-id="5f12b-171">Not Supported</span><span class="sxs-lookup"><span data-stu-id="5f12b-171">Not Supported</span></span> | <span data-ttu-id="5f12b-172">RouteBased VPN configuration</span><span class="sxs-lookup"><span data-stu-id="5f12b-172">RouteBased VPN configuration</span></span> | <span data-ttu-id="5f12b-173">RouteBased VPN configuration</span><span class="sxs-lookup"><span data-stu-id="5f12b-173">RouteBased VPN configuration</span></span> | <span data-ttu-id="5f12b-174">RouteBased VPN configuration</span><span class="sxs-lookup"><span data-stu-id="5f12b-174">RouteBased VPN configuration</span></span> |
| <span data-ttu-id="5f12b-175">**Authentication method**</span><span class="sxs-lookup"><span data-stu-id="5f12b-175">**Authentication method**</span></span>  | <span data-ttu-id="5f12b-176">Not Supported</span><span class="sxs-lookup"><span data-stu-id="5f12b-176">Not Supported</span></span> | <span data-ttu-id="5f12b-177">Pre-shared key for S2S connectivity</span><span class="sxs-lookup"><span data-stu-id="5f12b-177">Pre-shared key for S2S connectivity</span></span>  | <span data-ttu-id="5f12b-178">Pre-shared key for S2S connectivity</span><span class="sxs-lookup"><span data-stu-id="5f12b-178">Pre-shared key for S2S connectivity</span></span>  | <span data-ttu-id="5f12b-179">Pre-shared key for S2S connectivity</span><span class="sxs-lookup"><span data-stu-id="5f12b-179">Pre-shared key for S2S connectivity</span></span>  |   
| <span data-ttu-id="5f12b-180">**Maximum number of S2S connections**</span><span class="sxs-lookup"><span data-stu-id="5f12b-180">**Maximum number of S2S connections**</span></span>  | <span data-ttu-id="5f12b-181">Not Supported</span><span class="sxs-lookup"><span data-stu-id="5f12b-181">Not Supported</span></span> | <span data-ttu-id="5f12b-182">10</span><span class="sxs-lookup"><span data-stu-id="5f12b-182">10</span></span> | <span data-ttu-id="5f12b-183">10</span><span class="sxs-lookup"><span data-stu-id="5f12b-183">10</span></span>| <span data-ttu-id="5f12b-184">5</span><span class="sxs-lookup"><span data-stu-id="5f12b-184">5</span></span>|
|<span data-ttu-id="5f12b-185">**Active routing support (BGP)**</span><span class="sxs-lookup"><span data-stu-id="5f12b-185">**Active routing support (BGP)**</span></span> | <span data-ttu-id="5f12b-186">Not supported</span><span class="sxs-lookup"><span data-stu-id="5f12b-186">Not supported</span></span> | <span data-ttu-id="5f12b-187">Not supported</span><span class="sxs-lookup"><span data-stu-id="5f12b-187">Not supported</span></span> | <span data-ttu-id="5f12b-188">Supported</span><span class="sxs-lookup"><span data-stu-id="5f12b-188">Supported</span></span> | <span data-ttu-id="5f12b-189">Supported</span><span class="sxs-lookup"><span data-stu-id="5f12b-189">Supported</span></span> |

### <a name="gateway-subnet"></a><span data-ttu-id="5f12b-190">Gateway subnet</span><span class="sxs-lookup"><span data-stu-id="5f12b-190">Gateway subnet</span></span>

<span data-ttu-id="5f12b-191">Before you create a VPN gateway, you must create a gateway subnet.</span><span class="sxs-lookup"><span data-stu-id="5f12b-191">Before you create a VPN gateway, you must create a gateway subnet.</span></span> <span data-ttu-id="5f12b-192">The gateway subnet has the IP addresses that the virtual network gateway VMs and services use.</span><span class="sxs-lookup"><span data-stu-id="5f12b-192">The gateway subnet has the IP addresses that the virtual network gateway VMs and services use.</span></span> <span data-ttu-id="5f12b-193">When you create your virtual network gateway, gateway VMs are deployed to the gateway subnet and configured with the required VPN gateway settings.</span><span class="sxs-lookup"><span data-stu-id="5f12b-193">When you create your virtual network gateway, gateway VMs are deployed to the gateway subnet and configured with the required VPN gateway settings.</span></span> <span data-ttu-id="5f12b-194">**Don't** deploy anything else (for example, additional VMs) to the gateway subnet.</span><span class="sxs-lookup"><span data-stu-id="5f12b-194">**Don't** deploy anything else (for example, additional VMs) to the gateway subnet.</span></span>

>[!IMPORTANT]
><span data-ttu-id="5f12b-195">The gateway subnet must be named **GatewaySubnet** to work properly.</span><span class="sxs-lookup"><span data-stu-id="5f12b-195">The gateway subnet must be named **GatewaySubnet** to work properly.</span></span> <span data-ttu-id="5f12b-196">Azure Stack uses this name to identify the subnet to deploy the virtual network gateway VMs and services to.</span><span class="sxs-lookup"><span data-stu-id="5f12b-196">Azure Stack uses this name to identify the subnet to deploy the virtual network gateway VMs and services to.</span></span>

<span data-ttu-id="5f12b-197">When you create the gateway subnet, you specify the number of IP addresses that the subnet contains.</span><span class="sxs-lookup"><span data-stu-id="5f12b-197">When you create the gateway subnet, you specify the number of IP addresses that the subnet contains.</span></span> <span data-ttu-id="5f12b-198">The IP addresses in the gateway subnet are allocated to the gateway VMs and gateway services.</span><span class="sxs-lookup"><span data-stu-id="5f12b-198">The IP addresses in the gateway subnet are allocated to the gateway VMs and gateway services.</span></span> <span data-ttu-id="5f12b-199">Some configurations require more IP addresses than others.</span><span class="sxs-lookup"><span data-stu-id="5f12b-199">Some configurations require more IP addresses than others.</span></span> <span data-ttu-id="5f12b-200">Look at the instructions for the configuration that you want to create and verify that the gateway subnet you want to create meets those requirements.</span><span class="sxs-lookup"><span data-stu-id="5f12b-200">Look at the instructions for the configuration that you want to create and verify that the gateway subnet you want to create meets those requirements.</span></span>

<span data-ttu-id="5f12b-201">Additionally, you should make sure your gateway subnet has enough IP addresses to handle additional future configurations.</span><span class="sxs-lookup"><span data-stu-id="5f12b-201">Additionally, you should make sure your gateway subnet has enough IP addresses to handle additional future configurations.</span></span> <span data-ttu-id="5f12b-202">Although you can create a gateway subnet as small as /29, we recommend you create a gateway subnet of /28 or larger (/28, /27, /26, and so on.) That way, if you add functionality in the future, you don't have to tear down your gateway, then delete and recreate the gateway subnet to allow for more IP addresses.</span><span class="sxs-lookup"><span data-stu-id="5f12b-202">Although you can create a gateway subnet as small as /29, we recommend you create a gateway subnet of /28 or larger (/28, /27, /26, and so on.) That way, if you add functionality in the future, you don't have to tear down your gateway, then delete and recreate the gateway subnet to allow for more IP addresses.</span></span>

<span data-ttu-id="5f12b-203">The following Resource Manager PowerShell example shows a gateway subnet named GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="5f12b-203">The following Resource Manager PowerShell example shows a gateway subnet named GatewaySubnet.</span></span> <span data-ttu-id="5f12b-204">You can see the CIDR notation specifies a /27, which allows for enough IP addresses for most configurations that currently exist.</span><span class="sxs-lookup"><span data-stu-id="5f12b-204">You can see the CIDR notation specifies a /27, which allows for enough IP addresses for most configurations that currently exist.</span></span>

```PowerShell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

> [!IMPORTANT]
> <span data-ttu-id="5f12b-205">When working with gateway subnets, avoid associating a network security group (NSG) to the gateway subnet.</span><span class="sxs-lookup"><span data-stu-id="5f12b-205">When working with gateway subnets, avoid associating a network security group (NSG) to the gateway subnet.</span></span> <span data-ttu-id="5f12b-206">Associating a network security group to this subnet may cause your VPN gateway to stop functioning as expected.</span><span class="sxs-lookup"><span data-stu-id="5f12b-206">Associating a network security group to this subnet may cause your VPN gateway to stop functioning as expected.</span></span> <span data-ttu-id="5f12b-207">For more information about network security groups, see [What is a network security group?](/azure/virtual-network/virtual-networks-nsg).</span><span class="sxs-lookup"><span data-stu-id="5f12b-207">For more information about network security groups, see [What is a network security group?](/azure/virtual-network/virtual-networks-nsg).</span></span>

### <a name="local-network-gateways"></a><span data-ttu-id="5f12b-208">Local network gateways</span><span class="sxs-lookup"><span data-stu-id="5f12b-208">Local network gateways</span></span>

<span data-ttu-id="5f12b-209">When creating a VPN gateway configuration in Azure, the local network gateway often represents your on-premises location.</span><span class="sxs-lookup"><span data-stu-id="5f12b-209">When creating a VPN gateway configuration in Azure, the local network gateway often represents your on-premises location.</span></span> <span data-ttu-id="5f12b-210">In Azure Stack, it represents any remote VPN Device that sits outside Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5f12b-210">In Azure Stack, it represents any remote VPN Device that sits outside Azure Stack.</span></span> <span data-ttu-id="5f12b-211">This could be a VPN device in your datacenter (or a remote datacenter), or a VPN Gateway in Azure.</span><span class="sxs-lookup"><span data-stu-id="5f12b-211">This could be a VPN device in your datacenter (or a remote datacenter), or a VPN Gateway in Azure.</span></span>

<span data-ttu-id="5f12b-212">You give the local network gateway a name, the public IP address of the VPN device, and specify the address prefixes that are on the on-premises location.</span><span class="sxs-lookup"><span data-stu-id="5f12b-212">You give the local network gateway a name, the public IP address of the VPN device, and specify the address prefixes that are on the on-premises location.</span></span> <span data-ttu-id="5f12b-213">Azure looks at the destination address prefixes for network traffic, consults the configuration that you have specified for your local network gateway, and routes packets accordingly.</span><span class="sxs-lookup"><span data-stu-id="5f12b-213">Azure looks at the destination address prefixes for network traffic, consults the configuration that you have specified for your local network gateway, and routes packets accordingly.</span></span>

<span data-ttu-id="5f12b-214">The next PowerShell example creates a new local network gateway:</span><span class="sxs-lookup"><span data-stu-id="5f12b-214">The next PowerShell example creates a new local network gateway:</span></span>

```PowerShell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

<span data-ttu-id="5f12b-215">Sometimes you need to modify the local network gateway settings.</span><span class="sxs-lookup"><span data-stu-id="5f12b-215">Sometimes you need to modify the local network gateway settings.</span></span> <span data-ttu-id="5f12b-216">For example, when you add or modify the address range, or if the IP address of the VPN device changes.</span><span class="sxs-lookup"><span data-stu-id="5f12b-216">For example, when you add or modify the address range, or if the IP address of the VPN device changes.</span></span> <span data-ttu-id="5f12b-217">See [Modify local network gateway settings using PowerShell](/azure/vpn-gateway/vpn-gateway-modify-local-network-gateway).</span><span class="sxs-lookup"><span data-stu-id="5f12b-217">See [Modify local network gateway settings using PowerShell](/azure/vpn-gateway/vpn-gateway-modify-local-network-gateway).</span></span>

## <a name="ipsecike-parameters"></a><span data-ttu-id="5f12b-218">IPsec/IKE parameters</span><span class="sxs-lookup"><span data-stu-id="5f12b-218">IPsec/IKE parameters</span></span>

<span data-ttu-id="5f12b-219">When you set up a VPN Connection in Azure Stack, you need to configure the connection at both ends.</span><span class="sxs-lookup"><span data-stu-id="5f12b-219">When you set up a VPN Connection in Azure Stack, you need to configure the connection at both ends.</span></span>  <span data-ttu-id="5f12b-220">If you are configuring a VPN Connection between Azure Stack and a hardware device like a switch or router that is acting as a VPN Gateway, that device might ask you for additional settings.</span><span class="sxs-lookup"><span data-stu-id="5f12b-220">If you are configuring a VPN Connection between Azure Stack and a hardware device like a switch or router that is acting as a VPN Gateway, that device might ask you for additional settings.</span></span>

<span data-ttu-id="5f12b-221">Unlike Azure, which supports multiple offers as both an initiator and a responder, Azure Stack supports only one offer.</span><span class="sxs-lookup"><span data-stu-id="5f12b-221">Unlike Azure, which supports multiple offers as both an initiator and a responder, Azure Stack supports only one offer.</span></span>

### <a name="ike-phase-1-main-mode-parameters"></a><span data-ttu-id="5f12b-222">IKE Phase 1 (Main Mode) parameters</span><span class="sxs-lookup"><span data-stu-id="5f12b-222">IKE Phase 1 (Main Mode) parameters</span></span>

| <span data-ttu-id="5f12b-223">Property</span><span class="sxs-lookup"><span data-stu-id="5f12b-223">Property</span></span>              | <span data-ttu-id="5f12b-224">Value</span><span class="sxs-lookup"><span data-stu-id="5f12b-224">Value</span></span>|
|-|-|
| <span data-ttu-id="5f12b-225">IKE Version</span><span class="sxs-lookup"><span data-stu-id="5f12b-225">IKE Version</span></span>           | <span data-ttu-id="5f12b-226">IKEv2</span><span class="sxs-lookup"><span data-stu-id="5f12b-226">IKEv2</span></span> |
|<span data-ttu-id="5f12b-227">Diffie-Hellman Group</span><span class="sxs-lookup"><span data-stu-id="5f12b-227">Diffie-Hellman Group</span></span>   | <span data-ttu-id="5f12b-228">Group 2 (1024 bit)</span><span class="sxs-lookup"><span data-stu-id="5f12b-228">Group 2 (1024 bit)</span></span> |
| <span data-ttu-id="5f12b-229">Authentication Method</span><span class="sxs-lookup"><span data-stu-id="5f12b-229">Authentication Method</span></span> | <span data-ttu-id="5f12b-230">Pre-Shared Key</span><span class="sxs-lookup"><span data-stu-id="5f12b-230">Pre-Shared Key</span></span> |
|<span data-ttu-id="5f12b-231">Encryption & Hashing Algorithms</span><span class="sxs-lookup"><span data-stu-id="5f12b-231">Encryption & Hashing Algorithms</span></span> | <span data-ttu-id="5f12b-232">AES256, SHA256</span><span class="sxs-lookup"><span data-stu-id="5f12b-232">AES256, SHA256</span></span> |
|<span data-ttu-id="5f12b-233">SA Lifetime (Time)</span><span class="sxs-lookup"><span data-stu-id="5f12b-233">SA Lifetime (Time)</span></span>     | <span data-ttu-id="5f12b-234">28,800 seconds</span><span class="sxs-lookup"><span data-stu-id="5f12b-234">28,800 seconds</span></span>|

### <a name="ike-phase-2-quick-mode-parameters"></a><span data-ttu-id="5f12b-235">IKE Phase 2 (Quick Mode) parameters</span><span class="sxs-lookup"><span data-stu-id="5f12b-235">IKE Phase 2 (Quick Mode) parameters</span></span>

| <span data-ttu-id="5f12b-236">Property</span><span class="sxs-lookup"><span data-stu-id="5f12b-236">Property</span></span>| <span data-ttu-id="5f12b-237">Value</span><span class="sxs-lookup"><span data-stu-id="5f12b-237">Value</span></span>|
|-|-|
|<span data-ttu-id="5f12b-238">IKE Version</span><span class="sxs-lookup"><span data-stu-id="5f12b-238">IKE Version</span></span> |<span data-ttu-id="5f12b-239">IKEv2</span><span class="sxs-lookup"><span data-stu-id="5f12b-239">IKEv2</span></span> |
|<span data-ttu-id="5f12b-240">Encryption & Hashing Algorithms (Encryption)</span><span class="sxs-lookup"><span data-stu-id="5f12b-240">Encryption & Hashing Algorithms (Encryption)</span></span>     | <span data-ttu-id="5f12b-241">GCMAES256</span><span class="sxs-lookup"><span data-stu-id="5f12b-241">GCMAES256</span></span>|
|<span data-ttu-id="5f12b-242">Encryption & Hashing Algorithms (Authentication)</span><span class="sxs-lookup"><span data-stu-id="5f12b-242">Encryption & Hashing Algorithms (Authentication)</span></span> | <span data-ttu-id="5f12b-243">GCMAES256</span><span class="sxs-lookup"><span data-stu-id="5f12b-243">GCMAES256</span></span>|
|<span data-ttu-id="5f12b-244">SA Lifetime (Time)</span><span class="sxs-lookup"><span data-stu-id="5f12b-244">SA Lifetime (Time)</span></span>  | <span data-ttu-id="5f12b-245">27,000 seconds</span><span class="sxs-lookup"><span data-stu-id="5f12b-245">27,000 seconds</span></span>  |
|<span data-ttu-id="5f12b-246">SA Lifetime (Bytes)</span><span class="sxs-lookup"><span data-stu-id="5f12b-246">SA Lifetime (Bytes)</span></span> | <span data-ttu-id="5f12b-247">33,553,408</span><span class="sxs-lookup"><span data-stu-id="5f12b-247">33,553,408</span></span>     |
|<span data-ttu-id="5f12b-248">Perfect Forward Secrecy (PFS)</span><span class="sxs-lookup"><span data-stu-id="5f12b-248">Perfect Forward Secrecy (PFS)</span></span> |<span data-ttu-id="5f12b-249">None<sup>See note 1</sup></span><span class="sxs-lookup"><span data-stu-id="5f12b-249">None<sup>See note 1</sup></span></span> |
|<span data-ttu-id="5f12b-250">Dead Peer Detection</span><span class="sxs-lookup"><span data-stu-id="5f12b-250">Dead Peer Detection</span></span> | <span data-ttu-id="5f12b-251">Supported</span><span class="sxs-lookup"><span data-stu-id="5f12b-251">Supported</span></span>|  

* <span data-ttu-id="5f12b-252">*Note 1:*  Prior to version 1807, Azure Stack uses a value of PFS2048 for the Perfect Forward Secrecy (PFS).</span><span class="sxs-lookup"><span data-stu-id="5f12b-252">*Note 1:*  Prior to version 1807, Azure Stack uses a value of PFS2048 for the Perfect Forward Secrecy (PFS).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f12b-253">Next steps</span><span class="sxs-lookup"><span data-stu-id="5f12b-253">Next steps</span></span>

[<span data-ttu-id="5f12b-254">Connect using ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="5f12b-254">Connect using ExpressRoute</span></span>](azure-stack-connect-expressroute.md)
