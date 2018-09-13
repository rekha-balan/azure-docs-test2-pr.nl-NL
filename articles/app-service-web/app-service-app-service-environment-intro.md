---
title: Introduction to App Service Environment
description: Learn about the App Service Environment feature that provides secure, VNet-joined, dedicated scale units for running all of your apps.
services: app-service
documentationcenter: ''
author: stefsch
manager: erikre
editor: ''
ms.assetid: 78e6d4f5-da46-4eb5-a632-b5fdc17d2394
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 91b1d6315a9414789b28442f3f19d14c2aed8f00
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563141"
---
# <a name="introduction-to-app-service-environment"></a><span data-ttu-id="63c36-103">Introduction to App Service Environment</span><span class="sxs-lookup"><span data-stu-id="63c36-103">Introduction to App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="63c36-104">Overview</span><span class="sxs-lookup"><span data-stu-id="63c36-104">Overview</span></span>
<span data-ttu-id="63c36-105">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span><span class="sxs-lookup"><span data-stu-id="63c36-105">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="63c36-106">App Service Environments are ideal for application workloads requiring:</span><span class="sxs-lookup"><span data-stu-id="63c36-106">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="63c36-107">Very high scale</span><span class="sxs-lookup"><span data-stu-id="63c36-107">Very high scale</span></span>
* <span data-ttu-id="63c36-108">Isolation and secure network access</span><span class="sxs-lookup"><span data-stu-id="63c36-108">Isolation and secure network access</span></span>

<span data-ttu-id="63c36-109">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span><span class="sxs-lookup"><span data-stu-id="63c36-109">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="63c36-110">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span><span class="sxs-lookup"><span data-stu-id="63c36-110">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="63c36-111">App Service Environments are isolated to running only a single customer's applications, and are always deployed into a virtual network.</span><span class="sxs-lookup"><span data-stu-id="63c36-111">App Service Environments are isolated to running only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="63c36-112">Customers have fine-grained control over both inbound and outbound application network traffic, and applications can establish high-speed secure connections over virtual networks to on-premises corporate resources.</span><span class="sxs-lookup"><span data-stu-id="63c36-112">Customers have fine-grained control over both inbound and outbound application network traffic, and applications can establish high-speed secure connections over virtual networks to on-premises corporate resources.</span></span>

<span data-ttu-id="63c36-113">All articles and How-To's about App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="63c36-113">All articles and How-To's about App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="63c36-114">For an overview of how App Service Environments enable high scale and secure network access, see the [AzureCon Deep Dive][AzureConDeepDive] on App Service Environments!</span><span class="sxs-lookup"><span data-stu-id="63c36-114">For an overview of how App Service Environments enable high scale and secure network access, see the [AzureCon Deep Dive][AzureConDeepDive] on App Service Environments!</span></span>

<span data-ttu-id="63c36-115">For a deep-dive on horizontally scaling using multiple App Service Environments see the article on how to setup a [geo-distributed app footprint][GeodistributedAppFootprint].</span><span class="sxs-lookup"><span data-stu-id="63c36-115">For a deep-dive on horizontally scaling using multiple App Service Environments see the article on how to setup a [geo-distributed app footprint][GeodistributedAppFootprint].</span></span>

<span data-ttu-id="63c36-116">To see how the security architecture shown in the AzureCon Deep Dive was configured, see the article on implementing a [layered security architecture](app-service-app-service-environment-layered-security.md) with App Service Environments.</span><span class="sxs-lookup"><span data-stu-id="63c36-116">To see how the security architecture shown in the AzureCon Deep Dive was configured, see the article on implementing a [layered security architecture](app-service-app-service-environment-layered-security.md) with App Service Environments.</span></span>

<span data-ttu-id="63c36-117">Apps running on App Service Environments can have their access gated by upstream devices such as web application firewalls (WAF).</span><span class="sxs-lookup"><span data-stu-id="63c36-117">Apps running on App Service Environments can have their access gated by upstream devices such as web application firewalls (WAF).</span></span>  <span data-ttu-id="63c36-118">The article on [configuring a WAF for App Service Environments](app-service-app-service-environment-web-application-firewall.md) covers this scenario.</span><span class="sxs-lookup"><span data-stu-id="63c36-118">The article on [configuring a WAF for App Service Environments](app-service-app-service-environment-web-application-firewall.md) covers this scenario.</span></span> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a><span data-ttu-id="63c36-119">Dedicated Compute Resources</span><span class="sxs-lookup"><span data-stu-id="63c36-119">Dedicated Compute Resources</span></span>
<span data-ttu-id="63c36-120">All of the compute resources in an App Service Environment are dedicated exclusively to a single subscription, and an App Service Environment can be configured with up to fifty (50) compute resources for exclusive use by a single application.</span><span class="sxs-lookup"><span data-stu-id="63c36-120">All of the compute resources in an App Service Environment are dedicated exclusively to a single subscription, and an App Service Environment can be configured with up to fifty (50) compute resources for exclusive use by a single application.</span></span>

<span data-ttu-id="63c36-121">An App Service Environment is composed of a front-end compute resource pool, as well as one to three worker compute resource pools.</span><span class="sxs-lookup"><span data-stu-id="63c36-121">An App Service Environment is composed of a front-end compute resource pool, as well as one to three worker compute resource pools.</span></span> 

<span data-ttu-id="63c36-122">The front-end pool contains compute resources responsible for SSL termination as well automatic load balancing of app requests within an App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="63c36-122">The front-end pool contains compute resources responsible for SSL termination as well automatic load balancing of app requests within an App Service Environment.</span></span> 

<span data-ttu-id="63c36-123">Each worker pool contains compute resources allocated to [App Service Plans][AppServicePlan], which in turn contain one or more Azure App Service apps.</span><span class="sxs-lookup"><span data-stu-id="63c36-123">Each worker pool contains compute resources allocated to [App Service Plans][AppServicePlan], which in turn contain one or more Azure App Service apps.</span></span>  <span data-ttu-id="63c36-124">Since there can be up to three different worker pools in an App Service Environment, you have the flexibility to choose different compute resources for each worker pool.</span><span class="sxs-lookup"><span data-stu-id="63c36-124">Since there can be up to three different worker pools in an App Service Environment, you have the flexibility to choose different compute resources for each worker pool.</span></span>  

<span data-ttu-id="63c36-125">For example, this allows you to create one worker pool with less powerful compute resources for App Service Plans intended for development or test apps.</span><span class="sxs-lookup"><span data-stu-id="63c36-125">For example, this allows you to create one worker pool with less powerful compute resources for App Service Plans intended for development or test apps.</span></span>  <span data-ttu-id="63c36-126">A second (or even third) worker pool could use more powerful compute resources intended for App Service Plans running production apps.</span><span class="sxs-lookup"><span data-stu-id="63c36-126">A second (or even third) worker pool could use more powerful compute resources intended for App Service Plans running production apps.</span></span>

<span data-ttu-id="63c36-127">For more details on the quantity of compute resources available to the front-end and worker pools, see [How To Configure an App Service Environment][HowToConfigureanAppServiceEnvironment].</span><span class="sxs-lookup"><span data-stu-id="63c36-127">For more details on the quantity of compute resources available to the front-end and worker pools, see [How To Configure an App Service Environment][HowToConfigureanAppServiceEnvironment].</span></span>  

<span data-ttu-id="63c36-128">For details on the available compute resource sizes supported in an App Service Environment, consult the [App Service Pricing][AppServicePricing] page and review the available options for App Service Environments in the Premium pricing tier.</span><span class="sxs-lookup"><span data-stu-id="63c36-128">For details on the available compute resource sizes supported in an App Service Environment, consult the [App Service Pricing][AppServicePricing] page and review the available options for App Service Environments in the Premium pricing tier.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="63c36-129">Virtual Network Support</span><span class="sxs-lookup"><span data-stu-id="63c36-129">Virtual Network Support</span></span>
<span data-ttu-id="63c36-130">An App Service Environment can be created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model virtual network ([more info on virtual networks][MoreInfoOnVirtualNetworks]).</span><span class="sxs-lookup"><span data-stu-id="63c36-130">An App Service Environment can be created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model virtual network ([more info on virtual networks][MoreInfoOnVirtualNetworks]).</span></span>  <span data-ttu-id="63c36-131">Since an App Service Environment always exists in a virtual network, and more precisely within a subnet of a virtual network, you can leverage the security features of virtual networks to control both inbound and outbound network communications.</span><span class="sxs-lookup"><span data-stu-id="63c36-131">Since an App Service Environment always exists in a virtual network, and more precisely within a subnet of a virtual network, you can leverage the security features of virtual networks to control both inbound and outbound network communications.</span></span>  

<span data-ttu-id="63c36-132">An App Service Environment can be either Internet facing with a public IP address, or internal facing with only an Azure Internal Load Balancer (ILB) address.</span><span class="sxs-lookup"><span data-stu-id="63c36-132">An App Service Environment can be either Internet facing with a public IP address, or internal facing with only an Azure Internal Load Balancer (ILB) address.</span></span>

<span data-ttu-id="63c36-133">You can use [network security groups][NetworkSecurityGroups] to restrict inbound network communications to the subnet where an App Service Environment resides.</span><span class="sxs-lookup"><span data-stu-id="63c36-133">You can use [network security groups][NetworkSecurityGroups] to restrict inbound network communications to the subnet where an App Service Environment resides.</span></span>  <span data-ttu-id="63c36-134">This allows you to run apps behind upstream devices and services such as web application firewalls, and network SaaS providers.</span><span class="sxs-lookup"><span data-stu-id="63c36-134">This allows you to run apps behind upstream devices and services such as web application firewalls, and network SaaS providers.</span></span>

<span data-ttu-id="63c36-135">Apps also frequently need to access corporate resources such as internal databases and web services.</span><span class="sxs-lookup"><span data-stu-id="63c36-135">Apps also frequently need to access corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="63c36-136">A common approach is to make these endpoints available only to internal network traffic flowing within an Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="63c36-136">A common approach is to make these endpoints available only to internal network traffic flowing within an Azure virtual network.</span></span>  <span data-ttu-id="63c36-137">Once an App Service Environment is joined to the same virtual network as the internal services, apps running in the environment can access them, including endpoints reachable via [Site-to-Site][SiteToSite] and [Azure ExpressRoute][ExpressRoute] connections.</span><span class="sxs-lookup"><span data-stu-id="63c36-137">Once an App Service Environment is joined to the same virtual network as the internal services, apps running in the environment can access them, including endpoints reachable via [Site-to-Site][SiteToSite] and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

<span data-ttu-id="63c36-138">For more details on how App Service Environments work with virtual networks and on-premises networks consult the following articles on [Network Architecture][NetworkArchitectureOverview], [Controlling Inbound Traffic][ControllingInboundTraffic], and [Securely Connecting to Backends][SecurelyConnectingToBackends].</span><span class="sxs-lookup"><span data-stu-id="63c36-138">For more details on how App Service Environments work with virtual networks and on-premises networks consult the following articles on [Network Architecture][NetworkArchitectureOverview], [Controlling Inbound Traffic][ControllingInboundTraffic], and [Securely Connecting to Backends][SecurelyConnectingToBackends].</span></span> 

## <a name="getting-started"></a><span data-ttu-id="63c36-139">Getting started</span><span class="sxs-lookup"><span data-stu-id="63c36-139">Getting started</span></span>
<span data-ttu-id="63c36-140">To get started with App Service Environments, see [How To Create An App Service Environment][HowToCreateAnAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="63c36-140">To get started with App Service Environments, see [How To Create An App Service Environment][HowToCreateAnAppServiceEnvironment]</span></span>

<span data-ttu-id="63c36-141">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="63c36-141">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="63c36-142">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="63c36-142">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<span data-ttu-id="63c36-143">For an overview of the App Service Environment network architecture, see the [Network Architecture Overview][NetworkArchitectureOverview] article.</span><span class="sxs-lookup"><span data-stu-id="63c36-143">For an overview of the App Service Environment network architecture, see the [Network Architecture Overview][NetworkArchitectureOverview] article.</span></span>

<span data-ttu-id="63c36-144">For details on using an App Service Environment with ExpressRoute, see the following article on [Express Route and App Service Environments][NetworkConfigDetailsForExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="63c36-144">For details on using an App Service Environment with ExpressRoute, see the following article on [Express Route and App Service Environments][NetworkConfigDetailsForExpressRoute].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[MoreInfoOnVirtualNetworks]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePlan]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[LogicApps]: http://azure.microsoft.com/documentation/articles/app-service-logic-what-are-logic-apps/
[AzureConDeepDive]:  https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/
[GeodistributedAppFootprint]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[HowToConfigureanAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[ControllingInboundTraffic]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SecurelyConnectingToBackends]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NetworkArchitectureOverview]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[NetworkConfigDetailsForExpressRoute]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 

<!-- IMAGES -->


