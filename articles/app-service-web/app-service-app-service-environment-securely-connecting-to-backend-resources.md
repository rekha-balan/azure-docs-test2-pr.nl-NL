---
title: Securely Connecting to BackEnd Resources from an App Service Environment
description: Learn about how to securely connect to backend resources from an App Service Environment.
services: app-service
documentationcenter: ''
author: stefsch
manager: erikre
editor: ''
ms.assetid: f82eb283-a6e7-4923-a00b-4b4ccf7c4b5b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 9249cdb83233e66182117811a2e619e1f412734d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564320"
---
# <a name="securely-connecting-to-backend-resources-from-an-app-service-environment"></a><span data-ttu-id="15c80-103">Securely Connecting to Backend Resources from an App Service Environment</span><span class="sxs-lookup"><span data-stu-id="15c80-103">Securely Connecting to Backend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="15c80-104">Overview</span><span class="sxs-lookup"><span data-stu-id="15c80-104">Overview</span></span>
<span data-ttu-id="15c80-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment to other backend resources can flow exclusively over the virtual network.</span><span class="sxs-lookup"><span data-stu-id="15c80-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment to other backend resources can flow exclusively over the virtual network.</span></span>  <span data-ttu-id="15c80-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e. private addresses).</span><span class="sxs-lookup"><span data-stu-id="15c80-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e. private addresses).</span></span>  

<span data-ttu-id="15c80-107">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span><span class="sxs-lookup"><span data-stu-id="15c80-107">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="15c80-108">The endpoint may be ACLd to only allow access from other resources on the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="15c80-108">The endpoint may be ACLd to only allow access from other resources on the same virtual network.</span></span>  

<span data-ttu-id="15c80-109">As another example, sensitive endpoints may run on-premises and be connected to Azure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span><span class="sxs-lookup"><span data-stu-id="15c80-109">As another example, sensitive endpoints may run on-premises and be connected to Azure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="15c80-110">As a result, only resources in virtual networks connected to the Site-to-Site or ExpressRoute tunnels will be able to access on-premises endpoints.</span><span class="sxs-lookup"><span data-stu-id="15c80-110">As a result, only resources in virtual networks connected to the Site-to-Site or ExpressRoute tunnels will be able to access on-premises endpoints.</span></span>

<span data-ttu-id="15c80-111">For all of these scenarios, apps running on an App Service Environment will be able to securely connect to the various servers and resources.</span><span class="sxs-lookup"><span data-stu-id="15c80-111">For all of these scenarios, apps running on an App Service Environment will be able to securely connect to the various servers and resources.</span></span>  <span data-ttu-id="15c80-112">Outbound traffic from apps running in an App Service Environment to private endpoints in the same virtual network (or connected to the same virtual network), will only flow over the virtual network.</span><span class="sxs-lookup"><span data-stu-id="15c80-112">Outbound traffic from apps running in an App Service Environment to private endpoints in the same virtual network (or connected to the same virtual network), will only flow over the virtual network.</span></span>  <span data-ttu-id="15c80-113">Outbound traffic to private endpoints will not flow over the public Internet.</span><span class="sxs-lookup"><span data-stu-id="15c80-113">Outbound traffic to private endpoints will not flow over the public Internet.</span></span>

<span data-ttu-id="15c80-114">One caveat applies to outbound traffic from an App Service Environment to endpoints within a virtual network.</span><span class="sxs-lookup"><span data-stu-id="15c80-114">One caveat applies to outbound traffic from an App Service Environment to endpoints within a virtual network.</span></span>  <span data-ttu-id="15c80-115">App Service Environments cannot reach endpoints of virtual machines located in the **same** subnet as the App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="15c80-115">App Service Environments cannot reach endpoints of virtual machines located in the **same** subnet as the App Service Environment.</span></span>  <span data-ttu-id="15c80-116">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only the App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="15c80-116">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only the App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="15c80-117">Outbound Connectivity and DNS Requirements</span><span class="sxs-lookup"><span data-stu-id="15c80-117">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="15c80-118">For an App Service Environment to function properly, it requires outbound access to various endpoints.</span><span class="sxs-lookup"><span data-stu-id="15c80-118">For an App Service Environment to function properly, it requires outbound access to various endpoints.</span></span> <span data-ttu-id="15c80-119">A full list of the external endpoints used by an ASE is in the "Required Network Connectivity" section of the [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span><span class="sxs-lookup"><span data-stu-id="15c80-119">A full list of the external endpoints used by an ASE is in the "Required Network Connectivity" section of the [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="15c80-120">App Service Environments require a valid DNS infrastructure configured for the virtual network.</span><span class="sxs-lookup"><span data-stu-id="15c80-120">App Service Environments require a valid DNS infrastructure configured for the virtual network.</span></span>  <span data-ttu-id="15c80-121">If for any reason the DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment to pick up the new DNS configuration.</span><span class="sxs-lookup"><span data-stu-id="15c80-121">If for any reason the DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment to pick up the new DNS configuration.</span></span>  <span data-ttu-id="15c80-122">Triggering a rolling environment reboot using the "Restart" icon located at the top of the App Service Environment management blade in the portal will cause the environment to pick up the new DNS configuration.</span><span class="sxs-lookup"><span data-stu-id="15c80-122">Triggering a rolling environment reboot using the "Restart" icon located at the top of the App Service Environment management blade in the portal will cause the environment to pick up the new DNS configuration.</span></span>

<span data-ttu-id="15c80-123">It is also recommended that any custom DNS servers on the vnet be setup ahead of time prior to creating an App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="15c80-123">It is also recommended that any custom DNS servers on the vnet be setup ahead of time prior to creating an App Service Environment.</span></span>  <span data-ttu-id="15c80-124">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in the App Service Environment creation process failing.</span><span class="sxs-lookup"><span data-stu-id="15c80-124">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in the App Service Environment creation process failing.</span></span>  <span data-ttu-id="15c80-125">In a similar vein, if a custom DNS server exists on the other end of a VPN gateway, and the DNS server is unreachable or unavailable, the App Service Environment creation process will also fail.</span><span class="sxs-lookup"><span data-stu-id="15c80-125">In a similar vein, if a custom DNS server exists on the other end of a VPN gateway, and the DNS server is unreachable or unavailable, the App Service Environment creation process will also fail.</span></span>

## <a name="connecting-to-a-sql-server"></a><span data-ttu-id="15c80-126">Connecting to a SQL Server</span><span class="sxs-lookup"><span data-stu-id="15c80-126">Connecting to a SQL Server</span></span>
<span data-ttu-id="15c80-127">A common SQL Server configuration has an endpoint listening on port 1433:</span><span class="sxs-lookup"><span data-stu-id="15c80-127">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![SQL Server Endpoint][SqlServerEndpoint]

<span data-ttu-id="15c80-129">There are two approaches for restricting traffic to this endpoint:</span><span class="sxs-lookup"><span data-stu-id="15c80-129">There are two approaches for restricting traffic to this endpoint:</span></span>

* <span data-ttu-id="15c80-130">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span><span class="sxs-lookup"><span data-stu-id="15c80-130">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="15c80-131">[Network Security Groups][NetworkSecurityGroups]</span><span class="sxs-lookup"><span data-stu-id="15c80-131">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="15c80-132">Restricting Access With a Network ACL</span><span class="sxs-lookup"><span data-stu-id="15c80-132">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="15c80-133">Port 1433 can be secured using a network access control list.</span><span class="sxs-lookup"><span data-stu-id="15c80-133">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="15c80-134">The example below whitelists client addresses originating from inside of a virtual network, and blocks access to all other clients.</span><span class="sxs-lookup"><span data-stu-id="15c80-134">The example below whitelists client addresses originating from inside of a virtual network, and blocks access to all other clients.</span></span>

![Network Access Control List Example][NetworkAccessControlListExample]

<span data-ttu-id="15c80-136">Any applications running in App Service Environment in the same virtual network as the SQL Server will be able to connect to the SQL Server instance using the **VNet internal** IP address for the SQL Server virtual machine.</span><span class="sxs-lookup"><span data-stu-id="15c80-136">Any applications running in App Service Environment in the same virtual network as the SQL Server will be able to connect to the SQL Server instance using the **VNet internal** IP address for the SQL Server virtual machine.</span></span>  

<span data-ttu-id="15c80-137">The example connection string below references the SQL Server using its private IP address.</span><span class="sxs-lookup"><span data-stu-id="15c80-137">The example connection string below references the SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="15c80-138">Although the virtual machine has a public endpoint as well, connection attempts using the public IP address will be rejected because of the network ACL.</span><span class="sxs-lookup"><span data-stu-id="15c80-138">Although the virtual machine has a public endpoint as well, connection attempts using the public IP address will be rejected because of the network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="15c80-139">Restricting Access With a Network Security Group</span><span class="sxs-lookup"><span data-stu-id="15c80-139">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="15c80-140">An alternative approach for securing access is with a network security group.</span><span class="sxs-lookup"><span data-stu-id="15c80-140">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="15c80-141">Network security groups can be applied to individual virtual machines, or to a subnet containing virtual machines.</span><span class="sxs-lookup"><span data-stu-id="15c80-141">Network security groups can be applied to individual virtual machines, or to a subnet containing virtual machines.</span></span>

<span data-ttu-id="15c80-142">First a network security group needs to be created:</span><span class="sxs-lookup"><span data-stu-id="15c80-142">First a network security group needs to be created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="15c80-143">Restricting access to only VNet internal traffic is very simple with a network security group.</span><span class="sxs-lookup"><span data-stu-id="15c80-143">Restricting access to only VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="15c80-144">The default rules in a network security group only allow access from other network clients in the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="15c80-144">The default rules in a network security group only allow access from other network clients in the same virtual network.</span></span>

<span data-ttu-id="15c80-145">As a result locking down access to SQL Server is as simple as applying a network security group with its default rules to either the virtual machines running SQL Server, or the subnet containing the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="15c80-145">As a result locking down access to SQL Server is as simple as applying a network security group with its default rules to either the virtual machines running SQL Server, or the subnet containing the virtual machines.</span></span>

<span data-ttu-id="15c80-146">The sample below applies a network security group to the containing subnet:</span><span class="sxs-lookup"><span data-stu-id="15c80-146">The sample below applies a network security group to the containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="15c80-147">The end result is a set of security rules that block external access, while allowing VNet internal access:</span><span class="sxs-lookup"><span data-stu-id="15c80-147">The end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![Default Network Security Rules][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="15c80-149">Getting started</span><span class="sxs-lookup"><span data-stu-id="15c80-149">Getting started</span></span>
<span data-ttu-id="15c80-150">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="15c80-150">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="15c80-151">To get started with App Service Environments, see [Introduction to App Service Environment][IntroToAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="15c80-151">To get started with App Service Environments, see [Introduction to App Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="15c80-152">For details around controlling inbound traffic to your App Service Environment, see [Controlling inbound traffic to an App Service Environment][ControlInboundASE]</span><span class="sxs-lookup"><span data-stu-id="15c80-152">For details around controlling inbound traffic to your App Service Environment, see [Controlling inbound traffic to an App Service Environment][ControlInboundASE]</span></span>

<span data-ttu-id="15c80-153">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="15c80-153">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ControlInboundASE]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/ 

<!-- IMAGES -->
[SqlServerEndpoint]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 



