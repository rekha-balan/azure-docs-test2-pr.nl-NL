---
title: Layered Security Architecture with App Service Environments
description: Implementing a layered security architecture with App Service Environments.
services: app-service
documentationcenter: ''
author: stefsch
manager: erikre
editor: ''
ms.assetid: 73ce0213-bd3e-4876-b1ed-5ecad4ad5601
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: stefsch
ms.openlocfilehash: 07192b5d4f9d42cafaa586c4a6f7601318076db2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552495"
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a><span data-ttu-id="39cee-103">Implementing a Layered Security Architecture with App Service Environments</span><span class="sxs-lookup"><span data-stu-id="39cee-103">Implementing a Layered Security Architecture with App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="39cee-104">Overview</span><span class="sxs-lookup"><span data-stu-id="39cee-104">Overview</span></span>
<span data-ttu-id="39cee-105">Since App Service Environments provide an isolated runtime environment deployed into a virtual network, developers can create a layered security architecture providing differing levels of network access for each physical application tier.</span><span class="sxs-lookup"><span data-stu-id="39cee-105">Since App Service Environments provide an isolated runtime environment deployed into a virtual network, developers can create a layered security architecture providing differing levels of network access for each physical application tier.</span></span>

<span data-ttu-id="39cee-106">A common desire is to hide API back-ends from general Internet access, and only allow APIs to be called by upstream web apps.</span><span class="sxs-lookup"><span data-stu-id="39cee-106">A common desire is to hide API back-ends from general Internet access, and only allow APIs to be called by upstream web apps.</span></span>  <span data-ttu-id="39cee-107">[Network security groups (NSGs)][NetworkSecurityGroups] can be used on subnets containing App Service Environments to restrict public access to API applications.</span><span class="sxs-lookup"><span data-stu-id="39cee-107">[Network security groups (NSGs)][NetworkSecurityGroups] can be used on subnets containing App Service Environments to restrict public access to API applications.</span></span>

<span data-ttu-id="39cee-108">The diagram below shows an example architecture with a WebAPI based app deployed on an App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="39cee-108">The diagram below shows an example architecture with a WebAPI based app deployed on an App Service Environment.</span></span>  <span data-ttu-id="39cee-109">Three separate web app instances, deployed on three separate App Service Environments, make back-end calls to the same WebAPI app.</span><span class="sxs-lookup"><span data-stu-id="39cee-109">Three separate web app instances, deployed on three separate App Service Environments, make back-end calls to the same WebAPI app.</span></span>

![Conceptual Architecture][ConceptualArchitecture] 

<span data-ttu-id="39cee-111">The green plus signs indicate that the network security group on the subnet containing "apiase" allows inbound calls from the upstream web apps, as well calls from itself.</span><span class="sxs-lookup"><span data-stu-id="39cee-111">The green plus signs indicate that the network security group on the subnet containing "apiase" allows inbound calls from the upstream web apps, as well calls from itself.</span></span>  <span data-ttu-id="39cee-112">However the same network security group explicitly denies access to general inbound traffic from the Internet.</span><span class="sxs-lookup"><span data-stu-id="39cee-112">However the same network security group explicitly denies access to general inbound traffic from the Internet.</span></span> 

<span data-ttu-id="39cee-113">The remainder of this topic walks through the steps needed to configure the network security group on the subnet containing "apiase".</span><span class="sxs-lookup"><span data-stu-id="39cee-113">The remainder of this topic walks through the steps needed to configure the network security group on the subnet containing "apiase".</span></span>

## <a name="determining-the-network-behavior"></a><span data-ttu-id="39cee-114">Determining the Network Behavior</span><span class="sxs-lookup"><span data-stu-id="39cee-114">Determining the Network Behavior</span></span>
<span data-ttu-id="39cee-115">In order to know what network security rules are needed, you need to determine which network clients will be allowed to reach the App Service Environment containing the API app, and which clients will be blocked.</span><span class="sxs-lookup"><span data-stu-id="39cee-115">In order to know what network security rules are needed, you need to determine which network clients will be allowed to reach the App Service Environment containing the API app, and which clients will be blocked.</span></span>

<span data-ttu-id="39cee-116">Since [network security groups (NSGs)][NetworkSecurityGroups] are applied to subnets, and App Service Environments are deployed into subnets, the rules contained in an NSG apply to **all** apps running on an App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="39cee-116">Since [network security groups (NSGs)][NetworkSecurityGroups] are applied to subnets, and App Service Environments are deployed into subnets, the rules contained in an NSG apply to **all** apps running on an App Service Environment.</span></span>  <span data-ttu-id="39cee-117">Using the sample architecture for this article, once a network security group is applied to the subnet containing "apiase", all apps running on the "apiase" App Service Environment will be protected by the same set of security rules.</span><span class="sxs-lookup"><span data-stu-id="39cee-117">Using the sample architecture for this article, once a network security group is applied to the subnet containing "apiase", all apps running on the "apiase" App Service Environment will be protected by the same set of security rules.</span></span> 

* <span data-ttu-id="39cee-118">**Determine the outbound IP address of upstream callers:**  What is the IP address or addresses of the upstream callers?</span><span class="sxs-lookup"><span data-stu-id="39cee-118">**Determine the outbound IP address of upstream callers:**  What is the IP address or addresses of the upstream callers?</span></span>  <span data-ttu-id="39cee-119">These addresses will need to be explicitly allowed access in the NSG.</span><span class="sxs-lookup"><span data-stu-id="39cee-119">These addresses will need to be explicitly allowed access in the NSG.</span></span>  <span data-ttu-id="39cee-120">Since calls between App Service Environments are considered "Internet" calls, this means the outbound IP address assigned to each of the three upstream App Service Environments needs to be allowed access in the NSG for the "apiase" subnet.</span><span class="sxs-lookup"><span data-stu-id="39cee-120">Since calls between App Service Environments are considered "Internet" calls, this means the outbound IP address assigned to each of the three upstream App Service Environments needs to be allowed access in the NSG for the "apiase" subnet.</span></span>   <span data-ttu-id="39cee-121">For more details on determining the outbound IP address for apps running in an App Service Environment see the [Network Architecture][NetworkArchitecture] Overview article.</span><span class="sxs-lookup"><span data-stu-id="39cee-121">For more details on determining the outbound IP address for apps running in an App Service Environment see the [Network Architecture][NetworkArchitecture] Overview article.</span></span>
* <span data-ttu-id="39cee-122">**Will the back-end API app need to call itself?**</span><span class="sxs-lookup"><span data-stu-id="39cee-122">**Will the back-end API app need to call itself?**</span></span>  <span data-ttu-id="39cee-123">A sometimes overlooked and subtle point is the scenario where the back-end application needs to call itself.</span><span class="sxs-lookup"><span data-stu-id="39cee-123">A sometimes overlooked and subtle point is the scenario where the back-end application needs to call itself.</span></span>  <span data-ttu-id="39cee-124">If a back-end API application on an App Service Environment needs to call itself, this is also treated as an "Internet" call.</span><span class="sxs-lookup"><span data-stu-id="39cee-124">If a back-end API application on an App Service Environment needs to call itself, this is also treated as an "Internet" call.</span></span>  <span data-ttu-id="39cee-125">In the sample architecture this requires allowing access from the outbound IP address of the "apiase" App Service Environment as well.</span><span class="sxs-lookup"><span data-stu-id="39cee-125">In the sample architecture this requires allowing access from the outbound IP address of the "apiase" App Service Environment as well.</span></span>

## <a name="setting-up-the-network-security-group"></a><span data-ttu-id="39cee-126">Setting up the Network Security Group</span><span class="sxs-lookup"><span data-stu-id="39cee-126">Setting up the Network Security Group</span></span>
<span data-ttu-id="39cee-127">Once the set of outbound IP addresses are known, the next step is to construct a network security group.</span><span class="sxs-lookup"><span data-stu-id="39cee-127">Once the set of outbound IP addresses are known, the next step is to construct a network security group.</span></span>  <span data-ttu-id="39cee-128">Network security groups can be created for both Resource Manager based virtual networks, as well as classic virtual networks.</span><span class="sxs-lookup"><span data-stu-id="39cee-128">Network security groups can be created for both Resource Manager based virtual networks, as well as classic virtual networks.</span></span>  <span data-ttu-id="39cee-129">The examples below show creating and configuring an NSG on a classic virtual network using Powershell.</span><span class="sxs-lookup"><span data-stu-id="39cee-129">The examples below show creating and configuring an NSG on a classic virtual network using Powershell.</span></span>

<span data-ttu-id="39cee-130">For the sample architecture, the environments are located in South Central US, so an empty NSG is created in that region:</span><span class="sxs-lookup"><span data-stu-id="39cee-130">For the sample architecture, the environments are located in South Central US, so an empty NSG is created in that region:</span></span>

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

<span data-ttu-id="39cee-131">First an explicit allow rule is added for the Azure management infrastructure as noted in the article on [inbound traffic][InboundTraffic] for App Service Environments.</span><span class="sxs-lookup"><span data-stu-id="39cee-131">First an explicit allow rule is added for the Azure management infrastructure as noted in the article on [inbound traffic][InboundTraffic] for App Service Environments.</span></span>

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

<span data-ttu-id="39cee-132">Next, two rules are added to allow HTTP and HTTPS calls from the first upstream App Service Environment ("fe1ase").</span><span class="sxs-lookup"><span data-stu-id="39cee-132">Next, two rules are added to allow HTTP and HTTPS calls from the first upstream App Service Environment ("fe1ase").</span></span>

    #Grant access to requests from the first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="39cee-133">Rinse and repeat for the second and third upstream App Service Environments ("fe2ase"and "fe3ase").</span><span class="sxs-lookup"><span data-stu-id="39cee-133">Rinse and repeat for the second and third upstream App Service Environments ("fe2ase"and "fe3ase").</span></span>

    #Grant access to requests from the second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access to requests from the third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="39cee-134">Lastly, grant access to the outbound IP address of the back-end API's App Service Environment so that it can call back into itself.</span><span class="sxs-lookup"><span data-stu-id="39cee-134">Lastly, grant access to the outbound IP address of the back-end API's App Service Environment so that it can call back into itself.</span></span>

    #Allow apps on the apiase environment to call back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="39cee-135">No other network security rules need to be configured because every NSG has a set of default rules that block inbound access from the Internet by default.</span><span class="sxs-lookup"><span data-stu-id="39cee-135">No other network security rules need to be configured because every NSG has a set of default rules that block inbound access from the Internet by default.</span></span>

<span data-ttu-id="39cee-136">The full list of rules in the network security group are shown below.</span><span class="sxs-lookup"><span data-stu-id="39cee-136">The full list of rules in the network security group are shown below.</span></span>  <span data-ttu-id="39cee-137">Note how the last rule, which is highlighted, blocks inbound access from all callers other than those which have been explicitly granted access.</span><span class="sxs-lookup"><span data-stu-id="39cee-137">Note how the last rule, which is highlighted, blocks inbound access from all callers other than those which have been explicitly granted access.</span></span>

![NSG Configuration][NSGConfiguration] 

<span data-ttu-id="39cee-139">The final step is to apply the NSG to the subnet that contains the "apiase" App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="39cee-139">The final step is to apply the NSG to the subnet that contains the "apiase" App Service Environment.</span></span>  

     #Apply the NSG to the backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

<span data-ttu-id="39cee-140">With the NSG applied to the subnet, only the three upstream App Service Environments, and the App Service Environment containing the API back-end, are allowed to call into the "apiase" environment.</span><span class="sxs-lookup"><span data-stu-id="39cee-140">With the NSG applied to the subnet, only the three upstream App Service Environments, and the App Service Environment containing the API back-end, are allowed to call into the "apiase" environment.</span></span>

## <a name="additional-links-and-information"></a><span data-ttu-id="39cee-141">Additional Links and Information</span><span class="sxs-lookup"><span data-stu-id="39cee-141">Additional Links and Information</span></span>
<span data-ttu-id="39cee-142">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="39cee-142">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="39cee-143">Information about [network security groups](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="39cee-143">Information about [network security groups](../virtual-network/virtual-networks-nsg.md).</span></span> 

<span data-ttu-id="39cee-144">Understanding [outbound IP addresses][NetworkArchitecture] and App Service Environments.</span><span class="sxs-lookup"><span data-stu-id="39cee-144">Understanding [outbound IP addresses][NetworkArchitecture] and App Service Environments.</span></span>

<span data-ttu-id="39cee-145">[Network ports][InboundTraffic] used by App Service Environments.</span><span class="sxs-lookup"><span data-stu-id="39cee-145">[Network ports][InboundTraffic] used by App Service Environments.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png


