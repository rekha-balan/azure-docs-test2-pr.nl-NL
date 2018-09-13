---
title: Migration of network resources from Azure Germany to global Azure
description: This article provides help for migrating network resources from Azure Germany to global Azure
author: gitralf
services: germany
cloud: Azure Germany
ms.author: ralfwi
ms.service: germany
ms.date: 8/15/2018
ms.topic: article
ms.custom: bfmigrate
ms.openlocfilehash: c3ba77675876387c037c3068d713a4be6f33162b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857285"
---
# <a name="migration-of-network-resources-from-azure-germany-to-global-azure"></a><span data-ttu-id="4d8fb-103">Migration of network resources from Azure Germany to global Azure</span><span class="sxs-lookup"><span data-stu-id="4d8fb-103">Migration of network resources from Azure Germany to global Azure</span></span>

<span data-ttu-id="4d8fb-104">Most of the networking services don't support migration from Azure Germany to global Azure.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-104">Most of the networking services don't support migration from Azure Germany to global Azure.</span></span> <span data-ttu-id="4d8fb-105">However, you can connect your networks in both cloud environments together by using a Site-to-Site VPN.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-105">However, you can connect your networks in both cloud environments together by using a Site-to-Site VPN.</span></span> <span data-ttu-id="4d8fb-106">The steps are similar to deploying a Site-to-Site VPN between your on-premise network and Azure: Define a gateway in both clouds and tell them how to communicate with each other.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-106">The steps are similar to deploying a Site-to-Site VPN between your on-premise network and Azure: Define a gateway in both clouds and tell them how to communicate with each other.</span></span> <span data-ttu-id="4d8fb-107">There's an [article about Site-to-Site VPNs](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) describing these steps to deploy a Site-to-Site VPN:</span><span class="sxs-lookup"><span data-stu-id="4d8fb-107">There's an [article about Site-to-Site VPNs](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) describing these steps to deploy a Site-to-Site VPN:</span></span>

1. <span data-ttu-id="4d8fb-108">define a virtual network</span><span class="sxs-lookup"><span data-stu-id="4d8fb-108">define a virtual network</span></span>
2. <span data-ttu-id="4d8fb-109">define address space</span><span class="sxs-lookup"><span data-stu-id="4d8fb-109">define address space</span></span>
3. <span data-ttu-id="4d8fb-110">define subnets</span><span class="sxs-lookup"><span data-stu-id="4d8fb-110">define subnets</span></span>
4. <span data-ttu-id="4d8fb-111">define gateway subnet</span><span class="sxs-lookup"><span data-stu-id="4d8fb-111">define gateway subnet</span></span>
5. <span data-ttu-id="4d8fb-112">define gateway for VNet</span><span class="sxs-lookup"><span data-stu-id="4d8fb-112">define gateway for VNet</span></span>
6. <span data-ttu-id="4d8fb-113">define gateway for local network (your local VPN device)</span><span class="sxs-lookup"><span data-stu-id="4d8fb-113">define gateway for local network (your local VPN device)</span></span>
7. <span data-ttu-id="4d8fb-114">configure local VPN device</span><span class="sxs-lookup"><span data-stu-id="4d8fb-114">configure local VPN device</span></span>
8. <span data-ttu-id="4d8fb-115">build the connection</span><span class="sxs-lookup"><span data-stu-id="4d8fb-115">build the connection</span></span>

<span data-ttu-id="4d8fb-116">To connect VIrtual Networks between global Azure and Azure Germany, repeat step 1-5 for both environments, and connect them together in a final step:</span><span class="sxs-lookup"><span data-stu-id="4d8fb-116">To connect VIrtual Networks between global Azure and Azure Germany, repeat step 1-5 for both environments, and connect them together in a final step:</span></span>

- <span data-ttu-id="4d8fb-117">do steps 1-5 in global Azure</span><span class="sxs-lookup"><span data-stu-id="4d8fb-117">do steps 1-5 in global Azure</span></span>
- <span data-ttu-id="4d8fb-118">do steps 1-5 in Azure Germany</span><span class="sxs-lookup"><span data-stu-id="4d8fb-118">do steps 1-5 in Azure Germany</span></span>
- <span data-ttu-id="4d8fb-119">do step 6 in global Azure</span><span class="sxs-lookup"><span data-stu-id="4d8fb-119">do step 6 in global Azure</span></span>
  - <span data-ttu-id="4d8fb-120">enter the public IP address of the VPN gateway in Azure Germany</span><span class="sxs-lookup"><span data-stu-id="4d8fb-120">enter the public IP address of the VPN gateway in Azure Germany</span></span>
- <span data-ttu-id="4d8fb-121">do step 6 in Azure Germany</span><span class="sxs-lookup"><span data-stu-id="4d8fb-121">do step 6 in Azure Germany</span></span>
  - <span data-ttu-id="4d8fb-122">enter the public IP address of the VPN gateway in global Azure</span><span class="sxs-lookup"><span data-stu-id="4d8fb-122">enter the public IP address of the VPN gateway in global Azure</span></span>
- <span data-ttu-id="4d8fb-123">leave out step 7</span><span class="sxs-lookup"><span data-stu-id="4d8fb-123">leave out step 7</span></span>
- <span data-ttu-id="4d8fb-124">finish with step 8</span><span class="sxs-lookup"><span data-stu-id="4d8fb-124">finish with step 8</span></span>


## <a name="virtual-network-vnet"></a><span data-ttu-id="4d8fb-125">Virtual Network (VNet)</span><span class="sxs-lookup"><span data-stu-id="4d8fb-125">Virtual Network (VNet)</span></span>

<span data-ttu-id="4d8fb-126">Migration of VNets between Azure Germany and global Azure isn't supported at this time.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-126">Migration of VNets between Azure Germany and global Azure isn't supported at this time.</span></span> <span data-ttu-id="4d8fb-127">The recommended approach is to create new virtual networks in the target region and migrate resources into those VNets.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-127">The recommended approach is to create new virtual networks in the target region and migrate resources into those VNets.</span></span>

### <a name="next-steps"></a><span data-ttu-id="4d8fb-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d8fb-128">Next steps</span></span>

- <span data-ttu-id="4d8fb-129">Refresh your knowledge about Virtual Networks by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/virtual-network/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="4d8fb-129">Refresh your knowledge about Virtual Networks by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/virtual-network/#step-by-step-tutorials).</span></span>

### <a name="references"></a><span data-ttu-id="4d8fb-130">References</span><span class="sxs-lookup"><span data-stu-id="4d8fb-130">References</span></span>

- [<span data-ttu-id="4d8fb-131">About Virtual networks</span><span class="sxs-lookup"><span data-stu-id="4d8fb-131">About Virtual networks</span></span>](../virtual-network/virtual-networks-overview.md)
- [<span data-ttu-id="4d8fb-132">Planning Virtual networks</span><span class="sxs-lookup"><span data-stu-id="4d8fb-132">Planning Virtual networks</span></span>](../virtual-network/virtual-network-vnet-plan-design-arm.md)








## <a name="network-security-groups-nsg"></a><span data-ttu-id="4d8fb-133">Network Security Groups (NSG)</span><span class="sxs-lookup"><span data-stu-id="4d8fb-133">Network Security Groups (NSG)</span></span>

<span data-ttu-id="4d8fb-134">Migration of Network Security Groups between Azure Germany and global Azure isn't supported at this time.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-134">Migration of Network Security Groups between Azure Germany and global Azure isn't supported at this time.</span></span> <span data-ttu-id="4d8fb-135">The recommended approach is to create new Network Security Groups in the target region and apply the NSG rules to the new application environment.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-135">The recommended approach is to create new Network Security Groups in the target region and apply the NSG rules to the new application environment.</span></span>

<span data-ttu-id="4d8fb-136">You can get the current configuration of any Network Security Group from the portal, or with the following PowerShell commands:</span><span class="sxs-lookup"><span data-stu-id="4d8fb-136">You can get the current configuration of any Network Security Group from the portal, or with the following PowerShell commands:</span></span>

```powershell
$nsg=Get-AzureRmNetworkSecurityGroup -ResourceName <nsg-name> -ResourceGroupName <resourcegroupname>
Get-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg
```

### <a name="next-steps"></a><span data-ttu-id="4d8fb-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d8fb-137">Next steps</span></span>

- <span data-ttu-id="4d8fb-138">Refresh your [knowledge about Network Security Groups](/virtual-network/security-overview.md#network-security-groups).</span><span class="sxs-lookup"><span data-stu-id="4d8fb-138">Refresh your [knowledge about Network Security Groups](/virtual-network/security-overview.md#network-security-groups).</span></span>

### <a name="references"></a><span data-ttu-id="4d8fb-139">References</span><span class="sxs-lookup"><span data-stu-id="4d8fb-139">References</span></span>

- [<span data-ttu-id="4d8fb-140">About Network Security Groups</span><span class="sxs-lookup"><span data-stu-id="4d8fb-140">About Network Security Groups</span></span>](../virtual-network/security-overview.md)
- [<span data-ttu-id="4d8fb-141">Manage Network Security Groups</span><span class="sxs-lookup"><span data-stu-id="4d8fb-141">Manage Network Security Groups</span></span>](../virtual-network/manage-network-security-group.md)







## <a name="expressroute"></a><span data-ttu-id="4d8fb-142">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="4d8fb-142">ExpressRoute</span></span>

<span data-ttu-id="4d8fb-143">Migration of ExpressRoute between Azure Germany and global Azure isn't supported at this time.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-143">Migration of ExpressRoute between Azure Germany and global Azure isn't supported at this time.</span></span> <span data-ttu-id="4d8fb-144">The recommended approach is to create new ExpressRoute circuits and a new ExpressRoute gateway.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-144">The recommended approach is to create new ExpressRoute circuits and a new ExpressRoute gateway.</span></span>

### <a name="next-steps"></a><span data-ttu-id="4d8fb-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d8fb-145">Next steps</span></span>

- <span data-ttu-id="4d8fb-146">Refresh your knowledge about ExpressRoute by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/expressroute/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="4d8fb-146">Refresh your knowledge about ExpressRoute by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/expressroute/#step-by-step-tutorials).</span></span>

### <a name="references"></a><span data-ttu-id="4d8fb-147">References</span><span class="sxs-lookup"><span data-stu-id="4d8fb-147">References</span></span>

- [<span data-ttu-id="4d8fb-148">Create a new ExpressRoute gateway</span><span class="sxs-lookup"><span data-stu-id="4d8fb-148">Create a new ExpressRoute gateway</span></span>](../expressroute/expressroute-howto-add-gateway-portal-resource-manager.md)
- [<span data-ttu-id="4d8fb-149">ExpressRoute locations and service providers</span><span class="sxs-lookup"><span data-stu-id="4d8fb-149">ExpressRoute locations and service providers</span></span>](../expressroute/expressroute-locations.md)
- [<span data-ttu-id="4d8fb-150">More info about ExpressRoute gateway</span><span class="sxs-lookup"><span data-stu-id="4d8fb-150">More info about ExpressRoute gateway</span></span>](../expressroute/expressroute-about-virtual-network-gateways.md)





## <a name="vpn-gateway"></a><span data-ttu-id="4d8fb-151">VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="4d8fb-151">VPN Gateway</span></span>

<span data-ttu-id="4d8fb-152">Migration of Virtual Private Network (VPN) Gateways between Azure Germany and global Azure isn't supported at this time.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-152">Migration of Virtual Private Network (VPN) Gateways between Azure Germany and global Azure isn't supported at this time.</span></span> <span data-ttu-id="4d8fb-153">The recommended approach is to create and configure a new VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-153">The recommended approach is to create and configure a new VPN Gateway.</span></span>

<span data-ttu-id="4d8fb-154">Collect information about your current VPN gateway configuration by using the portal or by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-154">Collect information about your current VPN gateway configuration by using the portal or by using PowerShell.</span></span> <span data-ttu-id="4d8fb-155">There's a set of cmdlets starting with `Get-AzureRmVirtualNetworkGateway*`.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-155">There's a set of cmdlets starting with `Get-AzureRmVirtualNetworkGateway*`.</span></span>

<span data-ttu-id="4d8fb-156">Don't forget to update your on-premise configuration and delete any existing rules for the old IP ranges once you updated your Azure network environment.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-156">Don't forget to update your on-premise configuration and delete any existing rules for the old IP ranges once you updated your Azure network environment.</span></span>

### <a name="next-steps"></a><span data-ttu-id="4d8fb-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d8fb-157">Next steps</span></span>

- <span data-ttu-id="4d8fb-158">Refresh your knowledge about VPN Gateways by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/vpn-gateway/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="4d8fb-158">Refresh your knowledge about VPN Gateways by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/vpn-gateway/#step-by-step-tutorials).</span></span>

### <a name="references"></a><span data-ttu-id="4d8fb-159">References</span><span class="sxs-lookup"><span data-stu-id="4d8fb-159">References</span></span>

- <span data-ttu-id="4d8fb-160">[Create Site-to-Site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) with VPN gateway</span><span class="sxs-lookup"><span data-stu-id="4d8fb-160">[Create Site-to-Site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) with VPN gateway</span></span>
- <span data-ttu-id="4d8fb-161">[Get-AzureRmVirtualNetworkGateway](/powershell/module/azurerm.network/get-azurermvirtualnetworkgateway?view=azurermps-6.5.0) PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="4d8fb-161">[Get-AzureRmVirtualNetworkGateway](/powershell/module/azurerm.network/get-azurermvirtualnetworkgateway?view=azurermps-6.5.0) PowerShell cmdlets</span></span>
- <span data-ttu-id="4d8fb-162">Blog: [Create Site-to-Site connection](https://blogs.technet.microsoft.com/ralfwi/2017/02/02/connecting-clouds/) between Azure Germany and global Azure</span><span class="sxs-lookup"><span data-stu-id="4d8fb-162">Blog: [Create Site-to-Site connection](https://blogs.technet.microsoft.com/ralfwi/2017/02/02/connecting-clouds/) between Azure Germany and global Azure</span></span>
 






## <a name="application-gateway"></a><span data-ttu-id="4d8fb-163">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="4d8fb-163">Application Gateway</span></span>

<span data-ttu-id="4d8fb-164">Migration of Application Gateways between Azure Germany and global Azure isn't supported at this time.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-164">Migration of Application Gateways between Azure Germany and global Azure isn't supported at this time.</span></span> <span data-ttu-id="4d8fb-165">The recommended approach is to create and configure a new Gateway.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-165">The recommended approach is to create and configure a new Gateway.</span></span>

<span data-ttu-id="4d8fb-166">Collect information about your current gateway configuration by using the portal or by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-166">Collect information about your current gateway configuration by using the portal or by using PowerShell.</span></span> <span data-ttu-id="4d8fb-167">There's a set of cmdlets starting with `Get-AzureRmApplicationGateway*`.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-167">There's a set of cmdlets starting with `Get-AzureRmApplicationGateway*`.</span></span>

### <a name="next-steps"></a><span data-ttu-id="4d8fb-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d8fb-168">Next steps</span></span>

- <span data-ttu-id="4d8fb-169">Refresh your knowledge about Application Gateway by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/application-gateway/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="4d8fb-169">Refresh your knowledge about Application Gateway by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/application-gateway/#step-by-step-tutorials).</span></span>

### <a name="references"></a><span data-ttu-id="4d8fb-170">References</span><span class="sxs-lookup"><span data-stu-id="4d8fb-170">References</span></span>

- [<span data-ttu-id="4d8fb-171">Create Application Gateway</span><span class="sxs-lookup"><span data-stu-id="4d8fb-171">Create Application Gateway</span></span>](../application-gateway/quick-create-portal.md)
- <span data-ttu-id="4d8fb-172">[Get-AzureRmApplicationGateway](/powershell/module/azurerm.network/get-azurermapplicationgateway?view=azurermps-6.5.0) PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="4d8fb-172">[Get-AzureRmApplicationGateway](/powershell/module/azurerm.network/get-azurermapplicationgateway?view=azurermps-6.5.0) PowerShell cmdlets</span></span>














## <a name="azure-dns"></a><span data-ttu-id="4d8fb-173">Azure DNS</span><span class="sxs-lookup"><span data-stu-id="4d8fb-173">Azure DNS</span></span>

<span data-ttu-id="4d8fb-174">To migrate your DNS configuration from Azure Germany to global Azure, export the DNS zone file and import it under the new subscription.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-174">To migrate your DNS configuration from Azure Germany to global Azure, export the DNS zone file and import it under the new subscription.</span></span> <span data-ttu-id="4d8fb-175">Currently the only mechanism to export the zone file is by using Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-175">Currently the only mechanism to export the zone file is by using Azure CLI.</span></span>

<span data-ttu-id="4d8fb-176">When you're signed on to your source subscription in Azure Germany, configure CLI to use Resource Manager mode.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-176">When you're signed on to your source subscription in Azure Germany, configure CLI to use Resource Manager mode.</span></span> <span data-ttu-id="4d8fb-177">Export the zone:</span><span class="sxs-lookup"><span data-stu-id="4d8fb-177">Export the zone:</span></span>

```azurecli
az network dns zone export -g <resource group> -n <zone name> -f <zone file name>
```

<span data-ttu-id="4d8fb-178">Example:</span><span class="sxs-lookup"><span data-stu-id="4d8fb-178">Example:</span></span>

```azurecli
az network dns zone export -g "myresourcegroup" -n "contoso.com" -f "contoso.com.txt"
```

<span data-ttu-id="4d8fb-179">This command calls the Azure DNS service to export the zone "contoso.com" in the resource group "myresourcegroup".</span><span class="sxs-lookup"><span data-stu-id="4d8fb-179">This command calls the Azure DNS service to export the zone "contoso.com" in the resource group "myresourcegroup".</span></span> <span data-ttu-id="4d8fb-180">The output is stored as a BIND-compatible zone file in "contoso.com.txt" in the current folder.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-180">The output is stored as a BIND-compatible zone file in "contoso.com.txt" in the current folder.</span></span>

<span data-ttu-id="4d8fb-181">After the export is done, delete the NS records from the zone file as NS records will be created fresh for the new region and subscription.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-181">After the export is done, delete the NS records from the zone file as NS records will be created fresh for the new region and subscription.</span></span>

<span data-ttu-id="4d8fb-182">Now sign in to your target environment, create a new resource group (or choose an existing one) and import the previously created zone file:</span><span class="sxs-lookup"><span data-stu-id="4d8fb-182">Now sign in to your target environment, create a new resource group (or choose an existing one) and import the previously created zone file:</span></span>

```azurecli
az network dns zone import -g <resource group> -n <zone name> -f <zone file name>
```

<span data-ttu-id="4d8fb-183">Once the zone has been imported, you have to validate the zone by running the following command:</span><span class="sxs-lookup"><span data-stu-id="4d8fb-183">Once the zone has been imported, you have to validate the zone by running the following command:</span></span>

```azurecli
az network dns record-set list -g <resource group> -z <zone name>
```

<span data-ttu-id="4d8fb-184">Once the validation is done, contact your domain registrar and redelegate the NS records.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-184">Once the validation is done, contact your domain registrar and redelegate the NS records.</span></span> <span data-ttu-id="4d8fb-185">Get NS record information by executing this command:</span><span class="sxs-lookup"><span data-stu-id="4d8fb-185">Get NS record information by executing this command:</span></span>

```azurecli
az network dns record-set ns list -g <resource group> -z --output json
```

### <a name="next-steps"></a><span data-ttu-id="4d8fb-186">Next Steps</span><span class="sxs-lookup"><span data-stu-id="4d8fb-186">Next Steps</span></span>

- <span data-ttu-id="4d8fb-187">Refresh your knowledge about Application Gateway by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/dns/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="4d8fb-187">Refresh your knowledge about Application Gateway by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/dns/#step-by-step-tutorials).</span></span>

### <a name="references"></a><span data-ttu-id="4d8fb-188">References</span><span class="sxs-lookup"><span data-stu-id="4d8fb-188">References</span></span>

- [<span data-ttu-id="4d8fb-189">Azure DNS Overview</span><span class="sxs-lookup"><span data-stu-id="4d8fb-189">Azure DNS Overview</span></span>](../dns/dns-overview.md)
- [<span data-ttu-id="4d8fb-190">Azure DNS import and export</span><span class="sxs-lookup"><span data-stu-id="4d8fb-190">Azure DNS import and export</span></span>](../dns/dns-import-export.md)










## <a name="network-watcher"></a><span data-ttu-id="4d8fb-191">Network Watcher</span><span class="sxs-lookup"><span data-stu-id="4d8fb-191">Network Watcher</span></span>

<span data-ttu-id="4d8fb-192">Migration of Network Watcher between Azure Germany and global Azure isn't supported at this time.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-192">Migration of Network Watcher between Azure Germany and global Azure isn't supported at this time.</span></span> <span data-ttu-id="4d8fb-193">The recommended approach is to create and configure a new Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-193">The recommended approach is to create and configure a new Network Watcher.</span></span> <span data-ttu-id="4d8fb-194">Afterwards, compare the results between old and new environment:</span><span class="sxs-lookup"><span data-stu-id="4d8fb-194">Afterwards, compare the results between old and new environment:</span></span>

- [<span data-ttu-id="4d8fb-195">NSG Flow Logs</span><span class="sxs-lookup"><span data-stu-id="4d8fb-195">NSG Flow Logs</span></span>](../network-watcher/network-watcher-nsg-flow-logging-portal.md)
- [<span data-ttu-id="4d8fb-196">Connection Monitor</span><span class="sxs-lookup"><span data-stu-id="4d8fb-196">Connection Monitor</span></span>](../network-watcher/connection-monitor.md)

### <a name="next-steps"></a><span data-ttu-id="4d8fb-197">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d8fb-197">Next steps</span></span>

- <span data-ttu-id="4d8fb-198">Refresh your knowledge about Network Watcher by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/network-watcher/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="4d8fb-198">Refresh your knowledge about Network Watcher by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/network-watcher/#step-by-step-tutorials).</span></span>

### <a name="references"></a><span data-ttu-id="4d8fb-199">References</span><span class="sxs-lookup"><span data-stu-id="4d8fb-199">References</span></span>

- [<span data-ttu-id="4d8fb-200">Network Watcher Overview</span><span class="sxs-lookup"><span data-stu-id="4d8fb-200">Network Watcher Overview</span></span>](../network-watcher/network-watcher-monitoring-overview.md)













## <a name="traffic-manager"></a><span data-ttu-id="4d8fb-201">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="4d8fb-201">Traffic Manager</span></span>

<span data-ttu-id="4d8fb-202">Traffic Manager profiles created in Azure Germany can't be migrated to global Azure.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-202">Traffic Manager profiles created in Azure Germany can't be migrated to global Azure.</span></span> <span data-ttu-id="4d8fb-203">Since you also migrate all the Traffic Manager endpoints to the target environment, you need to update the Traffic Manager profile anyway.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-203">Since you also migrate all the Traffic Manager endpoints to the target environment, you need to update the Traffic Manager profile anyway.</span></span>

<span data-ttu-id="4d8fb-204">Traffic Manager can help you with a smooth migration.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-204">Traffic Manager can help you with a smooth migration.</span></span> <span data-ttu-id="4d8fb-205">With Traffic Manager still running in the old environment, you can already define additional endpoints in the target environment.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-205">With Traffic Manager still running in the old environment, you can already define additional endpoints in the target environment.</span></span> <span data-ttu-id="4d8fb-206">Once Target Manager runs in the new environment, you can still define endpoints in the old environment that you didn't migrate so far.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-206">Once Target Manager runs in the new environment, you can still define endpoints in the old environment that you didn't migrate so far.</span></span> <span data-ttu-id="4d8fb-207">This is known as [the Blue-Green scenario](https://azure.microsoft.com/blog/blue-green-deployments-using-azure-traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="4d8fb-207">This is known as [the Blue-Green scenario](https://azure.microsoft.com/blog/blue-green-deployments-using-azure-traffic-manager/).</span></span> <span data-ttu-id="4d8fb-208">In short:</span><span class="sxs-lookup"><span data-stu-id="4d8fb-208">In short:</span></span>

- <span data-ttu-id="4d8fb-209">Create a new Traffic Manager in Azure global</span><span class="sxs-lookup"><span data-stu-id="4d8fb-209">Create a new Traffic Manager in Azure global</span></span>
- <span data-ttu-id="4d8fb-210">Define the endpoints (still in Azure Germany)</span><span class="sxs-lookup"><span data-stu-id="4d8fb-210">Define the endpoints (still in Azure Germany)</span></span>
- <span data-ttu-id="4d8fb-211">Change your DNS CNAME to the new Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="4d8fb-211">Change your DNS CNAME to the new Traffic Manager</span></span>
- <span data-ttu-id="4d8fb-212">Turn off the old Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="4d8fb-212">Turn off the old Traffic Manager</span></span>
- <span data-ttu-id="4d8fb-213">for each endpoint in Azure Germany:</span><span class="sxs-lookup"><span data-stu-id="4d8fb-213">for each endpoint in Azure Germany:</span></span>
  - <span data-ttu-id="4d8fb-214">Migrate the endpoint to global Azure</span><span class="sxs-lookup"><span data-stu-id="4d8fb-214">Migrate the endpoint to global Azure</span></span>
  - <span data-ttu-id="4d8fb-215">change the Traffic Manager profile to use the new endpoint</span><span class="sxs-lookup"><span data-stu-id="4d8fb-215">change the Traffic Manager profile to use the new endpoint</span></span>

### <a name="next-steps"></a><span data-ttu-id="4d8fb-216">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d8fb-216">Next steps</span></span>

- <span data-ttu-id="4d8fb-217">Refresh your knowledge about Traffic Manager by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/traffic-manager/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="4d8fb-217">Refresh your knowledge about Traffic Manager by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/traffic-manager/#step-by-step-tutorials).</span></span>

### <a name="references"></a><span data-ttu-id="4d8fb-218">References</span><span class="sxs-lookup"><span data-stu-id="4d8fb-218">References</span></span>

- [<span data-ttu-id="4d8fb-219">Traffic Manager overview</span><span class="sxs-lookup"><span data-stu-id="4d8fb-219">Traffic Manager overview</span></span>](../traffic-manager/traffic-manager-overview.md)
- [<span data-ttu-id="4d8fb-220">Create a Traffic Manager profile</span><span class="sxs-lookup"><span data-stu-id="4d8fb-220">Create a Traffic Manager profile</span></span>](../traffic-manager/traffic-manager-create-profile.md)
- [<span data-ttu-id="4d8fb-221">Blue-Green scenario</span><span class="sxs-lookup"><span data-stu-id="4d8fb-221">Blue-Green scenario</span></span>](https://azure.microsoft.com/blog/blue-green-deployments-using-azure-traffic-manager/)



















## <a name="load-balancer"></a><span data-ttu-id="4d8fb-222">Load Balancer</span><span class="sxs-lookup"><span data-stu-id="4d8fb-222">Load Balancer</span></span>

<span data-ttu-id="4d8fb-223">Migration of Load Balancers between Azure Germany and global Azure isn't supported at this time.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-223">Migration of Load Balancers between Azure Germany and global Azure isn't supported at this time.</span></span> <span data-ttu-id="4d8fb-224">The recommended approach is to create and configure a new Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="4d8fb-224">The recommended approach is to create and configure a new Load Balancer.</span></span>

### <a name="next-steps"></a><span data-ttu-id="4d8fb-225">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d8fb-225">Next steps</span></span>

- <span data-ttu-id="4d8fb-226">Refresh your knowledge about Load Balancer by following these [Step-by-step tutorials](https://docs.microsoft.com/azure/load-balancer/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="4d8fb-226">Refresh your knowledge about Load Balancer by following these [Step-by-step tutorials](https://docs.microsoft.com/azure/load-balancer/#step-by-step-tutorials).</span></span>

### <a name="references"></a><span data-ttu-id="4d8fb-227">References</span><span class="sxs-lookup"><span data-stu-id="4d8fb-227">References</span></span>

- [<span data-ttu-id="4d8fb-228">Load balancer overview</span><span class="sxs-lookup"><span data-stu-id="4d8fb-228">Load balancer overview</span></span>](../load-balancer/load-balancer-overview.md)
- [<span data-ttu-id="4d8fb-229">Create new load balancer</span><span class="sxs-lookup"><span data-stu-id="4d8fb-229">Create new load balancer</span></span>](../load-balancer/quickstart-load-balancer-standard-public-portal.md)