---
title: 'Configure forced tunneling for Azure Site-to-Site connections: classic | Microsoft Docs'
description: How to redirect or 'force' all Internet-bound traffic back to your on-premises location.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: 5c0177f1-540c-4474-9b80-f541fa44240b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 79bf6892c823da282c3e763921e830f986419854
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44824562"
---
# <a name="configure-forced-tunneling-using-the-classic-deployment-model"></a><span data-ttu-id="78ef8-103">Configure forced tunneling using the classic deployment model</span><span class="sxs-lookup"><span data-stu-id="78ef8-103">Configure forced tunneling using the classic deployment model</span></span>

<span data-ttu-id="78ef8-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span><span class="sxs-lookup"><span data-stu-id="78ef8-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="78ef8-105">This is a critical security requirement for most enterprise IT policies.</span><span class="sxs-lookup"><span data-stu-id="78ef8-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="78ef8-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out to the Internet, without the option to allow you to inspect or audit the traffic.</span><span class="sxs-lookup"><span data-stu-id="78ef8-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out to the Internet, without the option to allow you to inspect or audit the traffic.</span></span> <span data-ttu-id="78ef8-107">Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches.</span><span class="sxs-lookup"><span data-stu-id="78ef8-107">Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="78ef8-108">This article walks you through configuring forced tunneling for virtual networks created using the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="78ef8-108">This article walks you through configuring forced tunneling for virtual networks created using the classic deployment model.</span></span> <span data-ttu-id="78ef8-109">Forced tunneling can be configured by using PowerShell, not through the portal.</span><span class="sxs-lookup"><span data-stu-id="78ef8-109">Forced tunneling can be configured by using PowerShell, not through the portal.</span></span> <span data-ttu-id="78ef8-110">If you want to configure forced tunneling for the Resource Manager deployment model, select classic article from the following dropdown list:</span><span class="sxs-lookup"><span data-stu-id="78ef8-110">If you want to configure forced tunneling for the Resource Manager deployment model, select classic article from the following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [PowerShell - Classic](vpn-gateway-about-forced-tunneling.md)
> * [PowerShell - Resource Manager](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a><span data-ttu-id="78ef8-113">Requirements and considerations</span><span class="sxs-lookup"><span data-stu-id="78ef8-113">Requirements and considerations</span></span>
<span data-ttu-id="78ef8-114">Forced tunneling in Azure is configured via virtual network user-defined routes (UDR).</span><span class="sxs-lookup"><span data-stu-id="78ef8-114">Forced tunneling in Azure is configured via virtual network user-defined routes (UDR).</span></span> <span data-ttu-id="78ef8-115">Redirecting traffic to an on-premises site is expressed as a Default Route to the Azure VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="78ef8-115">Redirecting traffic to an on-premises site is expressed as a Default Route to the Azure VPN gateway.</span></span> <span data-ttu-id="78ef8-116">The following section lists the current limitation of the routing table and routes for an Azure Virtual Network:</span><span class="sxs-lookup"><span data-stu-id="78ef8-116">The following section lists the current limitation of the routing table and routes for an Azure Virtual Network:</span></span>

* <span data-ttu-id="78ef8-117">Each virtual network subnet has a built-in, system routing table.</span><span class="sxs-lookup"><span data-stu-id="78ef8-117">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="78ef8-118">The system routing table has the following three groups of routes:</span><span class="sxs-lookup"><span data-stu-id="78ef8-118">The system routing table has the following three groups of routes:</span></span>

  * <span data-ttu-id="78ef8-119">**Local VNet routes:** Directly to the destination VMs in the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="78ef8-119">**Local VNet routes:** Directly to the destination VMs in the same virtual network.</span></span>
  * <span data-ttu-id="78ef8-120">**On-premises routes:** To the Azure VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="78ef8-120">**On-premises routes:** To the Azure VPN gateway.</span></span>
  * <span data-ttu-id="78ef8-121">**Default route:** Directly to the Internet.</span><span class="sxs-lookup"><span data-stu-id="78ef8-121">**Default route:** Directly to the Internet.</span></span> <span data-ttu-id="78ef8-122">Packets destined to the private IP addresses not covered by the previous two routes will be dropped.</span><span class="sxs-lookup"><span data-stu-id="78ef8-122">Packets destined to the private IP addresses not covered by the previous two routes will be dropped.</span></span>
* <span data-ttu-id="78ef8-123">With the release of user-defined routes, you can create a routing table to add a default route, and then associate the routing table to your VNet subnet(s) to enable forced tunneling on those subnets.</span><span class="sxs-lookup"><span data-stu-id="78ef8-123">With the release of user-defined routes, you can create a routing table to add a default route, and then associate the routing table to your VNet subnet(s) to enable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="78ef8-124">You need to set a "default site" among the cross-premises local sites connected to the virtual network.</span><span class="sxs-lookup"><span data-stu-id="78ef8-124">You need to set a "default site" among the cross-premises local sites connected to the virtual network.</span></span>
* <span data-ttu-id="78ef8-125">Forced tunneling must be associated with a VNet that has a dynamic routing VPN gateway (not a static gateway).</span><span class="sxs-lookup"><span data-stu-id="78ef8-125">Forced tunneling must be associated with a VNet that has a dynamic routing VPN gateway (not a static gateway).</span></span>
* <span data-ttu-id="78ef8-126">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via the ExpressRoute BGP peering sessions.</span><span class="sxs-lookup"><span data-stu-id="78ef8-126">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via the ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="78ef8-127">Please see the [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/) for more information.</span><span class="sxs-lookup"><span data-stu-id="78ef8-127">Please see the [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/) for more information.</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="78ef8-128">Configuration overview</span><span class="sxs-lookup"><span data-stu-id="78ef8-128">Configuration overview</span></span>
<span data-ttu-id="78ef8-129">In the following example, the Frontend subnet is not forced tunneled.</span><span class="sxs-lookup"><span data-stu-id="78ef8-129">In the following example, the Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="78ef8-130">The workloads in the Frontend subnet can continue to accept and respond to customer requests from the Internet directly.</span><span class="sxs-lookup"><span data-stu-id="78ef8-130">The workloads in the Frontend subnet can continue to accept and respond to customer requests from the Internet directly.</span></span> <span data-ttu-id="78ef8-131">The Mid-tier and Backend subnets are forced tunneled.</span><span class="sxs-lookup"><span data-stu-id="78ef8-131">The Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="78ef8-132">Any outbound connections from these two subnets to the Internet will be forced or redirected back to an on-premises site via one of the S2S VPN tunnels.</span><span class="sxs-lookup"><span data-stu-id="78ef8-132">Any outbound connections from these two subnets to the Internet will be forced or redirected back to an on-premises site via one of the S2S VPN tunnels.</span></span>

<span data-ttu-id="78ef8-133">This allows you to restrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing to enable your multi-tier service architecture required.</span><span class="sxs-lookup"><span data-stu-id="78ef8-133">This allows you to restrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing to enable your multi-tier service architecture required.</span></span> <span data-ttu-id="78ef8-134">You also can apply forced tunneling to the entire virtual networks if there are no Internet-facing workloads in your virtual networks.</span><span class="sxs-lookup"><span data-stu-id="78ef8-134">You also can apply forced tunneling to the entire virtual networks if there are no Internet-facing workloads in your virtual networks.</span></span>

![Forced Tunneling](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a><span data-ttu-id="78ef8-136">Before you begin</span><span class="sxs-lookup"><span data-stu-id="78ef8-136">Before you begin</span></span>
<span data-ttu-id="78ef8-137">Verify that you have the following items before beginning configuration.</span><span class="sxs-lookup"><span data-stu-id="78ef8-137">Verify that you have the following items before beginning configuration.</span></span>

* <span data-ttu-id="78ef8-138">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="78ef8-138">An Azure subscription.</span></span> <span data-ttu-id="78ef8-139">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="78ef8-139">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="78ef8-140">A configured virtual network.</span><span class="sxs-lookup"><span data-stu-id="78ef8-140">A configured virtual network.</span></span> 
* <span data-ttu-id="78ef8-141">The latest version of the Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="78ef8-141">The latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="78ef8-142">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="78ef8-142">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span>

## <a name="configure-forced-tunneling"></a><span data-ttu-id="78ef8-143">Configure forced tunneling</span><span class="sxs-lookup"><span data-stu-id="78ef8-143">Configure forced tunneling</span></span>
<span data-ttu-id="78ef8-144">The following procedure will help you specify forced tunneling for a virtual network.</span><span class="sxs-lookup"><span data-stu-id="78ef8-144">The following procedure will help you specify forced tunneling for a virtual network.</span></span> <span data-ttu-id="78ef8-145">The configuration steps correspond to the VNet network configuration file.</span><span class="sxs-lookup"><span data-stu-id="78ef8-145">The configuration steps correspond to the VNet network configuration file.</span></span>

```
<VirtualNetworkSite name="MultiTier-VNet" Location="North Europe">
     <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="DefaultSiteHQ">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch1">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch2">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch3">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
        </Gateway>
      </VirtualNetworkSite>
    </VirtualNetworkSite>
```

<span data-ttu-id="78ef8-146">In this example, the virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend' subnets, with four cross premises connections: 'DefaultSiteHQ', and three Branches.</span><span class="sxs-lookup"><span data-stu-id="78ef8-146">In this example, the virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend' subnets, with four cross premises connections: 'DefaultSiteHQ', and three Branches.</span></span> 

<span data-ttu-id="78ef8-147">The steps will set the 'DefaultSiteHQ' as the default site connection for forced tunneling, and configure the Midtier and Backend subnets to use forced tunneling.</span><span class="sxs-lookup"><span data-stu-id="78ef8-147">The steps will set the 'DefaultSiteHQ' as the default site connection for forced tunneling, and configure the Midtier and Backend subnets to use forced tunneling.</span></span>

1. <span data-ttu-id="78ef8-148">Create a routing table.</span><span class="sxs-lookup"><span data-stu-id="78ef8-148">Create a routing table.</span></span> <span data-ttu-id="78ef8-149">Use the following cmdlet to create your route table.</span><span class="sxs-lookup"><span data-stu-id="78ef8-149">Use the following cmdlet to create your route table.</span></span>

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. <span data-ttu-id="78ef8-150">Add a default route to the routing table.</span><span class="sxs-lookup"><span data-stu-id="78ef8-150">Add a default route to the routing table.</span></span> 

  <span data-ttu-id="78ef8-151">The following example adds a default route to the routing table created in Step 1.</span><span class="sxs-lookup"><span data-stu-id="78ef8-151">The following example adds a default route to the routing table created in Step 1.</span></span> <span data-ttu-id="78ef8-152">Note that the only route supported is the destination prefix of "0.0.0.0/0" to the "VPNGateway" NextHop.</span><span class="sxs-lookup"><span data-stu-id="78ef8-152">Note that the only route supported is the destination prefix of "0.0.0.0/0" to the "VPNGateway" NextHop.</span></span>

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. <span data-ttu-id="78ef8-153">Associate the routing table to the subnets.</span><span class="sxs-lookup"><span data-stu-id="78ef8-153">Associate the routing table to the subnets.</span></span> 

  <span data-ttu-id="78ef8-154">After a routing table is created and a route added, use the following example to add or associate the route table to a VNet subnet.</span><span class="sxs-lookup"><span data-stu-id="78ef8-154">After a routing table is created and a route added, use the following example to add or associate the route table to a VNet subnet.</span></span> <span data-ttu-id="78ef8-155">The example adds the route table "MyRouteTable" to the Midtier and Backend subnets of VNet MultiTier-VNet.</span><span class="sxs-lookup"><span data-stu-id="78ef8-155">The example adds the route table "MyRouteTable" to the Midtier and Backend subnets of VNet MultiTier-VNet.</span></span>

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. <span data-ttu-id="78ef8-156">Assign a default site for forced tunneling.</span><span class="sxs-lookup"><span data-stu-id="78ef8-156">Assign a default site for forced tunneling.</span></span> 

  <span data-ttu-id="78ef8-157">In the preceding step, the sample cmdlet scripts created the routing table and associated the route table to two of the VNet subnets.</span><span class="sxs-lookup"><span data-stu-id="78ef8-157">In the preceding step, the sample cmdlet scripts created the routing table and associated the route table to two of the VNet subnets.</span></span> <span data-ttu-id="78ef8-158">The remaining step is to select a local site among the multi-site connections of the virtual network as the default site or tunnel.</span><span class="sxs-lookup"><span data-stu-id="78ef8-158">The remaining step is to select a local site among the multi-site connections of the virtual network as the default site or tunnel.</span></span>

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a><span data-ttu-id="78ef8-159">Additional PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="78ef8-159">Additional PowerShell cmdlets</span></span>
### <a name="to-delete-a-route-table"></a><span data-ttu-id="78ef8-160">To delete a route table</span><span class="sxs-lookup"><span data-stu-id="78ef8-160">To delete a route table</span></span>

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="to-list-a-route-table"></a><span data-ttu-id="78ef8-161">To list a route table</span><span class="sxs-lookup"><span data-stu-id="78ef8-161">To list a route table</span></span>

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="to-delete-a-route-from-a-route-table"></a><span data-ttu-id="78ef8-162">To delete a route from a route table</span><span class="sxs-lookup"><span data-stu-id="78ef8-162">To delete a route from a route table</span></span>

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="to-remove-a-route-from-a-subnet"></a><span data-ttu-id="78ef8-163">To remove a route from a subnet</span><span class="sxs-lookup"><span data-stu-id="78ef8-163">To remove a route from a subnet</span></span>

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="to-list-the-route-table-associated-with-a-subnet"></a><span data-ttu-id="78ef8-164">To list the route table associated with a subnet</span><span class="sxs-lookup"><span data-stu-id="78ef8-164">To list the route table associated with a subnet</span></span>

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="to-remove-a-default-site-from-a-vnet-vpn-gateway"></a><span data-ttu-id="78ef8-165">To remove a default site from a VNet VPN gateway</span><span class="sxs-lookup"><span data-stu-id="78ef8-165">To remove a default site from a VNet VPN gateway</span></span>

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```