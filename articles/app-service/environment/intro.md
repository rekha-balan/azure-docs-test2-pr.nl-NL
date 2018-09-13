---
title: Introduction to Azure App Service Environments
description: Brief overview of Azure App Service Environments
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 3c7eaefa-1850-4643-8540-428e8982b7cb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 04/19/2018
ms.author: ccompy
ms.custom: mvc
ms.openlocfilehash: c6ae2aa46ae17c4ef995211b02112e1c05e2ec2f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865691"
---
# <a name="introduction-to-the-app-service-environments"></a><span data-ttu-id="7c99e-103">Introduction to the App Service Environments</span><span class="sxs-lookup"><span data-stu-id="7c99e-103">Introduction to the App Service Environments</span></span> #
 
## <a name="overview"></a><span data-ttu-id="7c99e-104">Overview</span><span class="sxs-lookup"><span data-stu-id="7c99e-104">Overview</span></span> ##

<span data-ttu-id="7c99e-105">The Azure App Service Environment is an Azure App Service feature that provides a fully isolated and dedicated environment for securely running App Service apps at high scale.</span><span class="sxs-lookup"><span data-stu-id="7c99e-105">The Azure App Service Environment is an Azure App Service feature that provides a fully isolated and dedicated environment for securely running App Service apps at high scale.</span></span> <span data-ttu-id="7c99e-106">This capability can host your:</span><span class="sxs-lookup"><span data-stu-id="7c99e-106">This capability can host your:</span></span>

* <span data-ttu-id="7c99e-107">Windows web apps</span><span class="sxs-lookup"><span data-stu-id="7c99e-107">Windows web apps</span></span>
* <span data-ttu-id="7c99e-108">Linux web apps</span><span class="sxs-lookup"><span data-stu-id="7c99e-108">Linux web apps</span></span> 
* <span data-ttu-id="7c99e-109">Docker containers</span><span class="sxs-lookup"><span data-stu-id="7c99e-109">Docker containers</span></span>
* <span data-ttu-id="7c99e-110">Mobile apps</span><span class="sxs-lookup"><span data-stu-id="7c99e-110">Mobile apps</span></span>
* <span data-ttu-id="7c99e-111">Functions</span><span class="sxs-lookup"><span data-stu-id="7c99e-111">Functions</span></span>

<span data-ttu-id="7c99e-112">App Service environments (ASEs) are appropriate for application workloads that require:</span><span class="sxs-lookup"><span data-stu-id="7c99e-112">App Service environments (ASEs) are appropriate for application workloads that require:</span></span>

* <span data-ttu-id="7c99e-113">Very high scale.</span><span class="sxs-lookup"><span data-stu-id="7c99e-113">Very high scale.</span></span>
* <span data-ttu-id="7c99e-114">Isolation and secure network access.</span><span class="sxs-lookup"><span data-stu-id="7c99e-114">Isolation and secure network access.</span></span>
* <span data-ttu-id="7c99e-115">High memory utilization.</span><span class="sxs-lookup"><span data-stu-id="7c99e-115">High memory utilization.</span></span>

<span data-ttu-id="7c99e-116">Customers can create multiple ASEs within a single Azure region or across multiple Azure regions.</span><span class="sxs-lookup"><span data-stu-id="7c99e-116">Customers can create multiple ASEs within a single Azure region or across multiple Azure regions.</span></span> <span data-ttu-id="7c99e-117">This flexibility makes ASEs ideal for horizontally scaling stateless application tiers in support of high RPS workloads.</span><span class="sxs-lookup"><span data-stu-id="7c99e-117">This flexibility makes ASEs ideal for horizontally scaling stateless application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="7c99e-118">ASEs are isolated to running only a single customer's applications and are always deployed into a virtual network.</span><span class="sxs-lookup"><span data-stu-id="7c99e-118">ASEs are isolated to running only a single customer's applications and are always deployed into a virtual network.</span></span> <span data-ttu-id="7c99e-119">Customers have fine-grained control over inbound and outbound application network traffic.</span><span class="sxs-lookup"><span data-stu-id="7c99e-119">Customers have fine-grained control over inbound and outbound application network traffic.</span></span> <span data-ttu-id="7c99e-120">Applications can establish high-speed secure connections over VPNs to on-premises corporate resources.</span><span class="sxs-lookup"><span data-stu-id="7c99e-120">Applications can establish high-speed secure connections over VPNs to on-premises corporate resources.</span></span>

* <span data-ttu-id="7c99e-121">ASE comes with its own pricing tier, learn how the [Isolated offering](https://channel9.msdn.com/Shows/Azure-Friday/Security-and-Horsepower-with-App-Service-The-New-Isolated-Offering?term=app%20service%20environment) helps drive hyper-scale and security.</span><span class="sxs-lookup"><span data-stu-id="7c99e-121">ASE comes with its own pricing tier, learn how the [Isolated offering](https://channel9.msdn.com/Shows/Azure-Friday/Security-and-Horsepower-with-App-Service-The-New-Isolated-Offering?term=app%20service%20environment) helps drive hyper-scale and security.</span></span>
* <span data-ttu-id="7c99e-122">[App Service Environments v2](https://channel9.msdn.com/Blogs/Azure/Azure-Application-Service-Environments-v2-Private-PaaS-Environments-in-the-Cloud?term=app%20service%20environment) provide a surrounding to safeguard your apps in a subnet of your network and provides your own private deployment of Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="7c99e-122">[App Service Environments v2](https://channel9.msdn.com/Blogs/Azure/Azure-Application-Service-Environments-v2-Private-PaaS-Environments-in-the-Cloud?term=app%20service%20environment) provide a surrounding to safeguard your apps in a subnet of your network and provides your own private deployment of Azure App Service.</span></span>
* <span data-ttu-id="7c99e-123">Multiple ASEs can be used to scale horizontally.</span><span class="sxs-lookup"><span data-stu-id="7c99e-123">Multiple ASEs can be used to scale horizontally.</span></span> <span data-ttu-id="7c99e-124">For more information, see [how to set up a geo-distributed app footprint](app-service-app-service-environment-geo-distributed-scale.md).</span><span class="sxs-lookup"><span data-stu-id="7c99e-124">For more information, see [how to set up a geo-distributed app footprint](app-service-app-service-environment-geo-distributed-scale.md).</span></span>
* <span data-ttu-id="7c99e-125">ASEs can be used to configure security architecture, as shown in the AzureCon Deep Dive.</span><span class="sxs-lookup"><span data-stu-id="7c99e-125">ASEs can be used to configure security architecture, as shown in the AzureCon Deep Dive.</span></span> <span data-ttu-id="7c99e-126">To see how the security architecture shown in the AzureCon Deep Dive was configured, see the [article on how to implement a layered security architecture](app-service-app-service-environment-layered-security.md) with App Service environments.</span><span class="sxs-lookup"><span data-stu-id="7c99e-126">To see how the security architecture shown in the AzureCon Deep Dive was configured, see the [article on how to implement a layered security architecture](app-service-app-service-environment-layered-security.md) with App Service environments.</span></span>
* <span data-ttu-id="7c99e-127">Apps running on ASEs can have their access gated by upstream devices, such as web application firewalls (WAFs).</span><span class="sxs-lookup"><span data-stu-id="7c99e-127">Apps running on ASEs can have their access gated by upstream devices, such as web application firewalls (WAFs).</span></span> <span data-ttu-id="7c99e-128">For more information, see [Web application firewall (WAF)][AppGW].</span><span class="sxs-lookup"><span data-stu-id="7c99e-128">For more information, see [Web application firewall (WAF)][AppGW].</span></span>

## <a name="dedicated-environment"></a><span data-ttu-id="7c99e-129">Dedicated environment</span><span class="sxs-lookup"><span data-stu-id="7c99e-129">Dedicated environment</span></span> ##

<span data-ttu-id="7c99e-130">An ASE is dedicated exclusively to a single subscription and can host 100 App Service Plan instances.</span><span class="sxs-lookup"><span data-stu-id="7c99e-130">An ASE is dedicated exclusively to a single subscription and can host 100 App Service Plan instances.</span></span> <span data-ttu-id="7c99e-131">The range can span 100 instances in a single App Service plan to 100 single-instance App Service plans, and everything in between.</span><span class="sxs-lookup"><span data-stu-id="7c99e-131">The range can span 100 instances in a single App Service plan to 100 single-instance App Service plans, and everything in between.</span></span>

<span data-ttu-id="7c99e-132">An ASE is composed of front ends and workers.</span><span class="sxs-lookup"><span data-stu-id="7c99e-132">An ASE is composed of front ends and workers.</span></span> <span data-ttu-id="7c99e-133">Front ends are responsible for HTTP/HTTPS termination and automatic load balancing of app requests within an ASE.</span><span class="sxs-lookup"><span data-stu-id="7c99e-133">Front ends are responsible for HTTP/HTTPS termination and automatic load balancing of app requests within an ASE.</span></span> <span data-ttu-id="7c99e-134">Front ends are automatically added as the App Service plans in the ASE are scaled out.</span><span class="sxs-lookup"><span data-stu-id="7c99e-134">Front ends are automatically added as the App Service plans in the ASE are scaled out.</span></span>

<span data-ttu-id="7c99e-135">Workers are roles that host customer apps.</span><span class="sxs-lookup"><span data-stu-id="7c99e-135">Workers are roles that host customer apps.</span></span> <span data-ttu-id="7c99e-136">Workers are available in three fixed sizes:</span><span class="sxs-lookup"><span data-stu-id="7c99e-136">Workers are available in three fixed sizes:</span></span>

* <span data-ttu-id="7c99e-137">One vCPU/3.5 GB RAM</span><span class="sxs-lookup"><span data-stu-id="7c99e-137">One vCPU/3.5 GB RAM</span></span>
* <span data-ttu-id="7c99e-138">Two vCPU/7 GB RAM</span><span class="sxs-lookup"><span data-stu-id="7c99e-138">Two vCPU/7 GB RAM</span></span>
* <span data-ttu-id="7c99e-139">Four vCPU/14 GB RAM</span><span class="sxs-lookup"><span data-stu-id="7c99e-139">Four vCPU/14 GB RAM</span></span>

<span data-ttu-id="7c99e-140">Customers do not need to manage front ends and workers.</span><span class="sxs-lookup"><span data-stu-id="7c99e-140">Customers do not need to manage front ends and workers.</span></span> <span data-ttu-id="7c99e-141">All infrastructure is automatically added as customers scale out their App Service plans.</span><span class="sxs-lookup"><span data-stu-id="7c99e-141">All infrastructure is automatically added as customers scale out their App Service plans.</span></span> <span data-ttu-id="7c99e-142">As App Service plans are created or scaled in an ASE, the required infrastructure is added or removed as appropriate.</span><span class="sxs-lookup"><span data-stu-id="7c99e-142">As App Service plans are created or scaled in an ASE, the required infrastructure is added or removed as appropriate.</span></span>

<span data-ttu-id="7c99e-143">There is a flat monthly rate for an ASE that pays for the infrastructure and doesn't change with the size of the ASE.</span><span class="sxs-lookup"><span data-stu-id="7c99e-143">There is a flat monthly rate for an ASE that pays for the infrastructure and doesn't change with the size of the ASE.</span></span> <span data-ttu-id="7c99e-144">In addition, there is a cost per App Service plan vCPU.</span><span class="sxs-lookup"><span data-stu-id="7c99e-144">In addition, there is a cost per App Service plan vCPU.</span></span> <span data-ttu-id="7c99e-145">All apps hosted in an ASE are in the Isolated pricing SKU.</span><span class="sxs-lookup"><span data-stu-id="7c99e-145">All apps hosted in an ASE are in the Isolated pricing SKU.</span></span> <span data-ttu-id="7c99e-146">For information on pricing for an ASE, see the [App Service pricing][Pricing] page and review the available options for ASEs.</span><span class="sxs-lookup"><span data-stu-id="7c99e-146">For information on pricing for an ASE, see the [App Service pricing][Pricing] page and review the available options for ASEs.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="7c99e-147">Virtual network support</span><span class="sxs-lookup"><span data-stu-id="7c99e-147">Virtual network support</span></span> ##

<span data-ttu-id="7c99e-148">The ASE feature is a deployment of the Azure App Service directly into a customer's Azure resource manager virtual network.</span><span class="sxs-lookup"><span data-stu-id="7c99e-148">The ASE feature is a deployment of the Azure App Service directly into a customer's Azure resource manager virtual network.</span></span> <span data-ttu-id="7c99e-149">To learn more about Azure virtual networks, see the [Azure virtual networks FAQ](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/).</span><span class="sxs-lookup"><span data-stu-id="7c99e-149">To learn more about Azure virtual networks, see the [Azure virtual networks FAQ](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/).</span></span> <span data-ttu-id="7c99e-150">An ASE always exists in a virtual network, and more precisely, within a subnet of a virtual network.</span><span class="sxs-lookup"><span data-stu-id="7c99e-150">An ASE always exists in a virtual network, and more precisely, within a subnet of a virtual network.</span></span> <span data-ttu-id="7c99e-151">You can use the security features of virtual networks to control inbound and outbound network communications for your apps.</span><span class="sxs-lookup"><span data-stu-id="7c99e-151">You can use the security features of virtual networks to control inbound and outbound network communications for your apps.</span></span>

<span data-ttu-id="7c99e-152">An ASE can be either internet-facing with a public IP address or internal-facing with only an Azure internal load balancer (ILB) address.</span><span class="sxs-lookup"><span data-stu-id="7c99e-152">An ASE can be either internet-facing with a public IP address or internal-facing with only an Azure internal load balancer (ILB) address.</span></span>

<span data-ttu-id="7c99e-153">[Network Security Groups][NSGs] restrict inbound network communications to the subnet where an ASE resides.</span><span class="sxs-lookup"><span data-stu-id="7c99e-153">[Network Security Groups][NSGs] restrict inbound network communications to the subnet where an ASE resides.</span></span> <span data-ttu-id="7c99e-154">You can use NSGs to run apps behind upstream devices and services such as WAFs and network SaaS providers.</span><span class="sxs-lookup"><span data-stu-id="7c99e-154">You can use NSGs to run apps behind upstream devices and services such as WAFs and network SaaS providers.</span></span>

<span data-ttu-id="7c99e-155">Apps also frequently need to access corporate resources such as internal databases and web services.</span><span class="sxs-lookup"><span data-stu-id="7c99e-155">Apps also frequently need to access corporate resources such as internal databases and web services.</span></span> <span data-ttu-id="7c99e-156">If you deploy the ASE in a virtual network that has a VPN connection to the on-premises network, the apps in the ASE can access the on-premises resources.</span><span class="sxs-lookup"><span data-stu-id="7c99e-156">If you deploy the ASE in a virtual network that has a VPN connection to the on-premises network, the apps in the ASE can access the on-premises resources.</span></span> <span data-ttu-id="7c99e-157">This capability is true regardless of whether the VPN is a [site-to-site](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-multi-site) or [Azure ExpressRoute](http://azure.microsoft.com/services/expressroute/) VPN.</span><span class="sxs-lookup"><span data-stu-id="7c99e-157">This capability is true regardless of whether the VPN is a [site-to-site](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-multi-site) or [Azure ExpressRoute](http://azure.microsoft.com/services/expressroute/) VPN.</span></span>

<span data-ttu-id="7c99e-158">For more information on how ASEs work with virtual networks and on-premises networks, see [App Service Environment network considerations][ASENetwork].</span><span class="sxs-lookup"><span data-stu-id="7c99e-158">For more information on how ASEs work with virtual networks and on-premises networks, see [App Service Environment network considerations][ASENetwork].</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Application-Service-Environments-v2-Private-PaaS-Environments-in-the-Cloud/player]

## <a name="app-service-environment-v1"></a><span data-ttu-id="7c99e-159">App Service Environment v1</span><span class="sxs-lookup"><span data-stu-id="7c99e-159">App Service Environment v1</span></span> ##

<span data-ttu-id="7c99e-160">App Service Environment has two versions: ASEv1 and ASEv2.</span><span class="sxs-lookup"><span data-stu-id="7c99e-160">App Service Environment has two versions: ASEv1 and ASEv2.</span></span> <span data-ttu-id="7c99e-161">The preceding information was based on ASEv2.</span><span class="sxs-lookup"><span data-stu-id="7c99e-161">The preceding information was based on ASEv2.</span></span> <span data-ttu-id="7c99e-162">This section shows you the differences between ASEv1 and ASEv2.</span><span class="sxs-lookup"><span data-stu-id="7c99e-162">This section shows you the differences between ASEv1 and ASEv2.</span></span> 

<span data-ttu-id="7c99e-163">In ASEv1, you need to manage all of the resources manually.</span><span class="sxs-lookup"><span data-stu-id="7c99e-163">In ASEv1, you need to manage all of the resources manually.</span></span> <span data-ttu-id="7c99e-164">That includes the front ends, workers, and IP addresses used for IP-based SSL.</span><span class="sxs-lookup"><span data-stu-id="7c99e-164">That includes the front ends, workers, and IP addresses used for IP-based SSL.</span></span> <span data-ttu-id="7c99e-165">Before you can scale out your App Service plan, you need to first scale out the worker pool where you want to host it.</span><span class="sxs-lookup"><span data-stu-id="7c99e-165">Before you can scale out your App Service plan, you need to first scale out the worker pool where you want to host it.</span></span>

<span data-ttu-id="7c99e-166">ASEv1 uses a different pricing model from ASEv2.</span><span class="sxs-lookup"><span data-stu-id="7c99e-166">ASEv1 uses a different pricing model from ASEv2.</span></span> <span data-ttu-id="7c99e-167">In ASEv1, you pay for each vCPU allocated.</span><span class="sxs-lookup"><span data-stu-id="7c99e-167">In ASEv1, you pay for each vCPU allocated.</span></span> <span data-ttu-id="7c99e-168">That includes vCPUs used for front ends or workers that aren't hosting any workloads.</span><span class="sxs-lookup"><span data-stu-id="7c99e-168">That includes vCPUs used for front ends or workers that aren't hosting any workloads.</span></span> <span data-ttu-id="7c99e-169">In ASEv1, the default maximum-scale size of an ASE is 55 total hosts.</span><span class="sxs-lookup"><span data-stu-id="7c99e-169">In ASEv1, the default maximum-scale size of an ASE is 55 total hosts.</span></span> <span data-ttu-id="7c99e-170">That includes workers and front ends.</span><span class="sxs-lookup"><span data-stu-id="7c99e-170">That includes workers and front ends.</span></span> <span data-ttu-id="7c99e-171">One advantage to ASEv1 is that it can be deployed in a classic virtual network and a Resource Manager virtual network.</span><span class="sxs-lookup"><span data-stu-id="7c99e-171">One advantage to ASEv1 is that it can be deployed in a classic virtual network and a Resource Manager virtual network.</span></span> <span data-ttu-id="7c99e-172">To learn more about ASEv1, see [App Service Environment v1 introduction][ASEv1Intro].</span><span class="sxs-lookup"><span data-stu-id="7c99e-172">To learn more about ASEv1, see [App Service Environment v1 introduction][ASEv1Intro].</span></span>

<!--Links-->
[App Service Environments v2]: https://channel9.msdn.com/Blogs/Azure/Azure-Application-Service-Environments-v2-Private-PaaS-Environments-in-the-Cloud?term=app%20service%20environment
[Isolated offering]: https://channel9.msdn.com/Shows/Azure-Friday/Security-and-Horsepower-with-App-Service-The-New-Isolated-Offering?term=app%20service%20environment
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/security-overview.md
[ConfigureASEv1]: app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: app-service-app-service-environment-intro.md
[webapps]: ../app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[ASEWAF]: app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/waf-overview.md
