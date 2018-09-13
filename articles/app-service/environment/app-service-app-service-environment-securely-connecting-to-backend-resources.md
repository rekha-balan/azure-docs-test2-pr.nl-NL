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
ms.openlocfilehash: 2fb13a4dac923a19dc12910cb1b78e909b93abe1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966309"
---
# <a name="securely-connecting-to-backend-resources-from-an-app-service-environment"></a><span data-ttu-id="806fe-103">Securely Connecting to Backend Resources from an App Service Environment</span><span class="sxs-lookup"><span data-stu-id="806fe-103">Securely Connecting to Backend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="806fe-104">Overview</span><span class="sxs-lookup"><span data-stu-id="806fe-104">Overview</span></span>
<span data-ttu-id="806fe-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment to other backend resources can flow exclusively over the virtual network.</span><span class="sxs-lookup"><span data-stu-id="806fe-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment to other backend resources can flow exclusively over the virtual network.</span></span>  <span data-ttu-id="806fe-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e. private addresses).</span><span class="sxs-lookup"><span data-stu-id="806fe-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e. private addresses).</span></span>  

<span data-ttu-id="806fe-107">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span><span class="sxs-lookup"><span data-stu-id="806fe-107">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="806fe-108">The endpoint may be ACLd to only allow access from other resources on the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="806fe-108">The endpoint may be ACLd to only allow access from other resources on the same virtual network.</span></span>  

<span data-ttu-id="806fe-109">As another example, sensitive endpoints may run on-premises and be connected to Azure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span><span class="sxs-lookup"><span data-stu-id="806fe-109">As another example, sensitive endpoints may run on-premises and be connected to Azure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="806fe-110">As a result, only resources in virtual networks connected to the Site-to-Site or ExpressRoute tunnels will be able to access on-premises endpoints.</span><span class="sxs-lookup"><span data-stu-id="806fe-110">As a result, only resources in virtual networks connected to the Site-to-Site or ExpressRoute tunnels will be able to access on-premises endpoints.</span></span>

<span data-ttu-id="806fe-111">For all of these scenarios, apps running on an App Service Environment will be able to securely connect to the various servers and resources.</span><span class="sxs-lookup"><span data-stu-id="806fe-111">For all of these scenarios, apps running on an App Service Environment will be able to securely connect to the various servers and resources.</span></span>  <span data-ttu-id="806fe-112">Outbound traffic from apps running in an App Service Environment to private endpoints in the same virtual network (or connected to the same virtual network), will only flow over the virtual network.</span><span class="sxs-lookup"><span data-stu-id="806fe-112">Outbound traffic from apps running in an App Service Environment to private endpoints in the same virtual network (or connected to the same virtual network), will only flow over the virtual network.</span></span>  <span data-ttu-id="806fe-113">Outbound traffic to private endpoints will not flow over the public Internet.</span><span class="sxs-lookup"><span data-stu-id="806fe-113">Outbound traffic to private endpoints will not flow over the public Internet.</span></span>

<span data-ttu-id="806fe-114">One caveat applies to outbound traffic from an App Service Environment to endpoints within a virtual network.</span><span class="sxs-lookup"><span data-stu-id="806fe-114">One caveat applies to outbound traffic from an App Service Environment to endpoints within a virtual network.</span></span>  <span data-ttu-id="806fe-115">App Service Environments cannot reach endpoints of virtual machines located in the **same** subnet as the App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="806fe-115">App Service Environments cannot reach endpoints of virtual machines located in the **same** subnet as the App Service Environment.</span></span>  <span data-ttu-id="806fe-116">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only the App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="806fe-116">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only the App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="806fe-117">Outbound Connectivity and DNS Requirements</span><span class="sxs-lookup"><span data-stu-id="806fe-117">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="806fe-118">For an App Service Environment to function properly, it requires outbound access to various endpoints.</span><span class="sxs-lookup"><span data-stu-id="806fe-118">For an App Service Environment to function properly, it requires outbound access to various endpoints.</span></span> <span data-ttu-id="806fe-119">A full list of the external endpoints used by an ASE is in the "Required Network Connectivity" section of the [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span><span class="sxs-lookup"><span data-stu-id="806fe-119">A full list of the external endpoints used by an ASE is in the "Required Network Connectivity" section of the [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="806fe-120">App Service Environments require a valid DNS infrastructure configured for the virtual network.</span><span class="sxs-lookup"><span data-stu-id="806fe-120">App Service Environments require a valid DNS infrastructure configured for the virtual network.</span></span>  <span data-ttu-id="806fe-121">If for any reason the DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment to pick up the new DNS configuration.</span><span class="sxs-lookup"><span data-stu-id="806fe-121">If for any reason the DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment to pick up the new DNS configuration.</span></span>  <span data-ttu-id="806fe-122">Triggering a rolling environment reboot using the "Restart" icon located at the top of the App Service Environment management blade in the portal will cause the environment to pick up the new DNS configuration.</span><span class="sxs-lookup"><span data-stu-id="806fe-122">Triggering a rolling environment reboot using the "Restart" icon located at the top of the App Service Environment management blade in the portal will cause the environment to pick up the new DNS configuration.</span></span>

<span data-ttu-id="806fe-123">It is also recommended that any custom DNS servers on the vnet be setup ahead of time prior to creating an App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="806fe-123">It is also recommended that any custom DNS servers on the vnet be setup ahead of time prior to creating an App Service Environment.</span></span>  <span data-ttu-id="806fe-124">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in the App Service Environment creation process failing.</span><span class="sxs-lookup"><span data-stu-id="806fe-124">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in the App Service Environment creation process failing.</span></span>  <span data-ttu-id="806fe-125">In a similar vein, if a custom DNS server exists on the other end of a VPN gateway, and the DNS server is unreachable or unavailable, the App Service Environment creation process will also fail.</span><span class="sxs-lookup"><span data-stu-id="806fe-125">In a similar vein, if a custom DNS server exists on the other end of a VPN gateway, and the DNS server is unreachable or unavailable, the App Service Environment creation process will also fail.</span></span>

## <a name="connecting-to-a-sql-server"></a><span data-ttu-id="806fe-126">Connecting to a SQL Server</span><span class="sxs-lookup"><span data-stu-id="806fe-126">Connecting to a SQL Server</span></span>
<span data-ttu-id="806fe-127">A common SQL Server configuration has an endpoint listening on port 1433:</span><span class="sxs-lookup"><span data-stu-id="806fe-127">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![SQL Server Endpoint][SqlServerEndpoint]

<span data-ttu-id="806fe-129">There are two approaches for restricting traffic to this endpoint:</span><span class="sxs-lookup"><span data-stu-id="806fe-129">There are two approaches for restricting traffic to this endpoint:</span></span>

* <span data-ttu-id="806fe-130">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span><span class="sxs-lookup"><span data-stu-id="806fe-130">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="806fe-131">[Network Security Groups][NetworkSecurityGroups]</span><span class="sxs-lookup"><span data-stu-id="806fe-131">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="806fe-132">Restricting Access With a Network ACL</span><span class="sxs-lookup"><span data-stu-id="806fe-132">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="806fe-133">Port 1433 can be secured using a network access control list.</span><span class="sxs-lookup"><span data-stu-id="806fe-133">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="806fe-134">The example below whitelists client addresses originating from inside of a virtual network, and blocks access to all other clients.</span><span class="sxs-lookup"><span data-stu-id="806fe-134">The example below whitelists client addresses originating from inside of a virtual network, and blocks access to all other clients.</span></span>

![Network Access Control List Example][NetworkAccessControlListExample]

<span data-ttu-id="806fe-136">Any applications running in App Service Environment in the same virtual network as the SQL Server will be able to connect to the SQL Server instance using the **VNet internal** IP address for the SQL Server virtual machine.</span><span class="sxs-lookup"><span data-stu-id="806fe-136">Any applications running in App Service Environment in the same virtual network as the SQL Server will be able to connect to the SQL Server instance using the **VNet internal** IP address for the SQL Server virtual machine.</span></span>  

<span data-ttu-id="806fe-137">The example connection string below references the SQL Server using its private IP address.</span><span class="sxs-lookup"><span data-stu-id="806fe-137">The example connection string below references the SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="806fe-138">Although the virtual machine has a public endpoint as well, connection attempts using the public IP address will be rejected because of the network ACL.</span><span class="sxs-lookup"><span data-stu-id="806fe-138">Although the virtual machine has a public endpoint as well, connection attempts using the public IP address will be rejected because of the network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="806fe-139">Restricting Access With a Network Security Group</span><span class="sxs-lookup"><span data-stu-id="806fe-139">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="806fe-140">An alternative approach for securing access is with a network security group.</span><span class="sxs-lookup"><span data-stu-id="806fe-140">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="806fe-141">Network security groups can be applied to individual virtual machines, or to a subnet containing virtual machines.</span><span class="sxs-lookup"><span data-stu-id="806fe-141">Network security groups can be applied to individual virtual machines, or to a subnet containing virtual machines.</span></span>

<span data-ttu-id="806fe-142">First a network security group needs to be created:</span><span class="sxs-lookup"><span data-stu-id="806fe-142">First a network security group needs to be created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="806fe-143">Restricting access to only VNet internal traffic is very simple with a network security group.</span><span class="sxs-lookup"><span data-stu-id="806fe-143">Restricting access to only VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="806fe-144">The default rules in a network security group only allow access from other network clients in the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="806fe-144">The default rules in a network security group only allow access from other network clients in the same virtual network.</span></span>

<span data-ttu-id="806fe-145">As a result locking down access to SQL Server is as simple as applying a network security group with its default rules to either the virtual machines running SQL Server, or the subnet containing the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="806fe-145">As a result locking down access to SQL Server is as simple as applying a network security group with its default rules to either the virtual machines running SQL Server, or the subnet containing the virtual machines.</span></span>

<span data-ttu-id="806fe-146">The sample below applies a network security group to the containing subnet:</span><span class="sxs-lookup"><span data-stu-id="806fe-146">The sample below applies a network security group to the containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="806fe-147">The end result is a set of security rules that block external access, while allowing VNet internal access:</span><span class="sxs-lookup"><span data-stu-id="806fe-147">The end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![Default Network Security Rules][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="806fe-149">Getting started</span><span class="sxs-lookup"><span data-stu-id="806fe-149">Getting started</span></span>
<span data-ttu-id="806fe-150">To get started with App Service Environments, see [Introduction to App Service Environment][IntroToAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="806fe-150">To get started with App Service Environments, see [Introduction to App Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="806fe-151">For details around controlling inbound traffic to your App Service Environment, see [Controlling inbound traffic to an App Service Environment][ControlInboundASE]</span><span class="sxs-lookup"><span data-stu-id="806fe-151">For details around controlling inbound traffic to your App Service Environment, see [Controlling inbound traffic to an App Service Environment][ControlInboundASE]</span></span>

[!INCLUDE [app-service-web-try-app-service](../../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  app-service-app-service-environment-control-inbound-traffic.md
[SiteToSite]: https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-multi-site
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  app-service-app-service-environment-intro.md
[ControlInboundASE]:  app-service-app-service-environment-control-inbound-traffic.md

<!-- IMAGES -->
[SqlServerEndpoint]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 
