---
title: Configuring a Web Application Firewall (WAF) for App Service Environment
description: Learn how to configure a web application firewall in front of your App Service Environment.
services: app-service\web
documentationcenter: ''
author: naziml
manager: erikre
editor: jimbe
ms.assetid: a2101291-83ba-4169-98a2-2c0ed9a65e8d
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: naziml
ms.openlocfilehash: fc799a25a3b12ca897336d93a8eeae0e310cc073
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556529"
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a><span data-ttu-id="e0ee9-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span><span class="sxs-lookup"><span data-stu-id="e0ee9-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="e0ee9-104">Overview</span><span class="sxs-lookup"><span data-stu-id="e0ee9-104">Overview</span></span>
<span data-ttu-id="e0ee9-105">Web application firewalls like the [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that is available on the [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helps secure your web applications by inspecting inbound web traffic to block SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-105">Web application firewalls like the [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that is available on the [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helps secure your web applications by inspecting inbound web traffic to block SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="e0ee9-106">It also inspects the responses from the back-end web servers for Data Loss Prevention (DLP).</span><span class="sxs-lookup"><span data-stu-id="e0ee9-106">It also inspects the responses from the back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="e0ee9-107">Combined with the isolation and additional scaling provided by App Service Environments, this provides an ideal environment to host business critical web applications that need to withstand malicious requests and high volume traffic.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-107">Combined with the isolation and additional scaling provided by App Service Environments, this provides an ideal environment to host business critical web applications that need to withstand malicious requests and high volume traffic.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a><span data-ttu-id="e0ee9-108">Setup</span><span class="sxs-lookup"><span data-stu-id="e0ee9-108">Setup</span></span>
<span data-ttu-id="e0ee9-109">For this document we will configure our App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from the WAF can reach the App Service Environment and it will not be accessible from the DMZ.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-109">For this document we will configure our App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from the WAF can reach the App Service Environment and it will not be accessible from the DMZ.</span></span> <span data-ttu-id="e0ee9-110">We will also have Azure Traffic Manager in front of our Barracuda WAF instances to load balance across Azure data centers and regions.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-110">We will also have Azure Traffic Manager in front of our Barracuda WAF instances to load balance across Azure data centers and regions.</span></span> <span data-ttu-id="e0ee9-111">A high level diagram of the setup would look like what is shown below.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-111">A high level diagram of the setup would look like what is shown below.</span></span>

![Architecture][Architecture] 

> <span data-ttu-id="e0ee9-113">Note: With the introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure the ASE to be inaccessible from the DMZ and only be available to the private network.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-113">Note: With the introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure the ASE to be inaccessible from the DMZ and only be available to the private network.</span></span> 
> 
> 

## <a name="configuring-your-app-service-environment"></a><span data-ttu-id="e0ee9-114">Configuring your App Service Environment</span><span class="sxs-lookup"><span data-stu-id="e0ee9-114">Configuring your App Service Environment</span></span>
<span data-ttu-id="e0ee9-115">To configure an App Service Environment refer to [our documentation](app-service-web-how-to-create-an-app-service-environment.md) on the subject.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-115">To configure an App Service Environment refer to [our documentation](app-service-web-how-to-create-an-app-service-environment.md) on the subject.</span></span> <span data-ttu-id="e0ee9-116">Once you have an App Service Environment created, you can create [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind the WAF we configure in the next section.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-116">Once you have an App Service Environment created, you can create [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind the WAF we configure in the next section.</span></span>

## <a name="configuring-your-barracuda-waf-cloud-service"></a><span data-ttu-id="e0ee9-117">Configuring your Barracuda WAF Cloud Service</span><span class="sxs-lookup"><span data-stu-id="e0ee9-117">Configuring your Barracuda WAF Cloud Service</span></span>
<span data-ttu-id="e0ee9-118">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-118">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span></span> <span data-ttu-id="e0ee9-119">But because we want redundancy and not introduce a single point of failure, you want to deploy at least 2 WAF instance VMs into the same Cloud Service when following these instructions.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-119">But because we want redundancy and not introduce a single point of failure, you want to deploy at least 2 WAF instance VMs into the same Cloud Service when following these instructions.</span></span>

### <a name="adding-endpoints-to-cloud-service"></a><span data-ttu-id="e0ee9-120">Adding Endpoints to Cloud Service</span><span class="sxs-lookup"><span data-stu-id="e0ee9-120">Adding Endpoints to Cloud Service</span></span>
<span data-ttu-id="e0ee9-121">Once you have 2 or more WAF VM instances in your Cloud Service you can use the [Azure portal](https://portal.azure.com/) to add HTTP and HTTPS endpoints that are used by your application as shown in the image below.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-121">Once you have 2 or more WAF VM instances in your Cloud Service you can use the [Azure portal](https://portal.azure.com/) to add HTTP and HTTPS endpoints that are used by your application as shown in the image below.</span></span>

![Configure Endpoint][ConfigureEndpoint]

<span data-ttu-id="e0ee9-123">If your applications use other endpoints, make sure to add those to this list as well.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-123">If your applications use other endpoints, make sure to add those to this list as well.</span></span> 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a><span data-ttu-id="e0ee9-124">Configuring Barracuda WAF through its Management Portal</span><span class="sxs-lookup"><span data-stu-id="e0ee9-124">Configuring Barracuda WAF through its Management Portal</span></span>
<span data-ttu-id="e0ee9-125">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-125">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span></span> <span data-ttu-id="e0ee9-126">Since we have multiple instances of the WAF VMs you will need to repeat the steps here for each VM instance.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-126">Since we have multiple instances of the WAF VMs you will need to repeat the steps here for each VM instance.</span></span> 

> <span data-ttu-id="e0ee9-127">Note: Once you are done with WAF configuration, remove the TCP/8000 endpoint from all your WAF VMs to keep your WAF secure.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-127">Note: Once you are done with WAF configuration, remove the TCP/8000 endpoint from all your WAF VMs to keep your WAF secure.</span></span>
> 
> 

<span data-ttu-id="e0ee9-128">Add the management endpoint as shown in the image below to configure your Barracuda WAF.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-128">Add the management endpoint as shown in the image below to configure your Barracuda WAF.</span></span>

![Add Management Endpoint][AddManagementEndpoint]

<span data-ttu-id="e0ee9-130">Use a browser to browse to the management endpoint on your Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-130">Use a browser to browse to the management endpoint on your Cloud Service.</span></span> <span data-ttu-id="e0ee9-131">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing to http://test.cloudapp.net:8000.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-131">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing to http://test.cloudapp.net:8000.</span></span> <span data-ttu-id="e0ee9-132">You should see a login page like below that you can login using credentials you specified in the WAF VM setup phase.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-132">You should see a login page like below that you can login using credentials you specified in the WAF VM setup phase.</span></span>

![Management Login Page][ManagementLoginPage]

<span data-ttu-id="e0ee9-134">Once you login you should see a dashboard as the one in the image below that will present basic statistics about the WAF protection.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-134">Once you login you should see a dashboard as the one in the image below that will present basic statistics about the WAF protection.</span></span>

![Management Dashboard][ManagementDashboard]

<span data-ttu-id="e0ee9-136">Clicking on the Services tab will let you configure your WAF for services it is protecting.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-136">Clicking on the Services tab will let you configure your WAF for services it is protecting.</span></span> <span data-ttu-id="e0ee9-137">For more details on configuring your Barracuda WAF you can consult [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span><span class="sxs-lookup"><span data-stu-id="e0ee9-137">For more details on configuring your Barracuda WAF you can consult [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span></span> <span data-ttu-id="e0ee9-138">In the example below an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-138">In the example below an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span></span>

![Management Add Services][ManagementAddServices]

> <span data-ttu-id="e0ee9-140">Note: Depending on how your applications are configured and what features are being used in your App Service Environment, you will need to forward traffic for TCP ports other than 80 and 443, e.g. if you have IP SSL setup for a Web App.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-140">Note: Depending on how your applications are configured and what features are being used in your App Service Environment, you will need to forward traffic for TCP ports other than 80 and 443, e.g. if you have IP SSL setup for a Web App.</span></span> <span data-ttu-id="e0ee9-141">For a list of network ports used in App Service Environments, please refer to [Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-141">For a list of network ports used in App Service Environments, please refer to [Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span></span>
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a><span data-ttu-id="e0ee9-142">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span><span class="sxs-lookup"><span data-stu-id="e0ee9-142">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span></span>
<span data-ttu-id="e0ee9-143">If your application is available in multiple regions, then you would want to load balance them behind [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e0ee9-143">If your application is available in multiple regions, then you would want to load balance them behind [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="e0ee9-144">To do so you can add an endpoint in the [Azure classic portal](https://manage.azure.com) using the Cloud Service name for your WAF in the Traffic Manager profile as shown in the image below.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-144">To do so you can add an endpoint in the [Azure classic portal](https://manage.azure.com) using the Cloud Service name for your WAF in the Traffic Manager profile as shown in the image below.</span></span> 

![Traffic Manager Endpoint][TrafficManagerEndpoint]

<span data-ttu-id="e0ee9-146">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager to ping for the availability of your application.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-146">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager to ping for the availability of your application.</span></span> <span data-ttu-id="e0ee9-147">You can configure the URL under the Configure section on the [Azure classic portal](https://manage.azure.com) as shown below.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-147">You can configure the URL under the Configure section on the [Azure classic portal](https://manage.azure.com) as shown below.</span></span>

![Configure Traffic Manager][ConfigureTrafficManager]

<span data-ttu-id="e0ee9-149">To forward the Traffic Manager pings from your WAF to your application, you need to setup Website Translations on your Barracuda WAF to forward traffic to your application as shown in the example below.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-149">To forward the Traffic Manager pings from your WAF to your application, you need to setup Website Translations on your Barracuda WAF to forward traffic to your application as shown in the example below.</span></span>

![Website Translations][WebsiteTranslations]

## <a name="securing-traffic-to-app-service-environment-using-network-security-groups-nsg"></a><span data-ttu-id="e0ee9-151">Securing Traffic to App Service Environment Using Network Security Groups (NSG)</span><span class="sxs-lookup"><span data-stu-id="e0ee9-151">Securing Traffic to App Service Environment Using Network Security Groups (NSG)</span></span>
<span data-ttu-id="e0ee9-152">Follow the [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic to your App Service Environment from the WAF only by using the VIP address of your Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-152">Follow the [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic to your App Service Environment from the WAF only by using the VIP address of your Cloud Service.</span></span> <span data-ttu-id="e0ee9-153">Here's a sample Powershell command for performing this task for TCP port 80.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-153">Here's a sample Powershell command for performing this task for TCP port 80.</span></span>

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

<span data-ttu-id="e0ee9-154">Replace the SourceAddressPrefix with the Virtual IP Address (VIP) of your WAF's Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-154">Replace the SourceAddressPrefix with the Virtual IP Address (VIP) of your WAF's Cloud Service.</span></span>

> <span data-ttu-id="e0ee9-155">Note: The VIP of your Cloud Service will change when you delete and re-create the Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-155">Note: The VIP of your Cloud Service will change when you delete and re-create the Cloud Service.</span></span> <span data-ttu-id="e0ee9-156">Make sure to update the IP address in the Network Resource group once you do so.</span><span class="sxs-lookup"><span data-stu-id="e0ee9-156">Make sure to update the IP address in the Network Resource group once you do so.</span></span> 
> 
> 

<!-- IMAGES -->
[Architecture]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-app-service-environment-web-application-firewall/Architecture.png
[ConfigureEndpoint]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-app-service-environment-web-application-firewall/ConfigureEndpoint.png
[AddManagementEndpoint]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-app-service-environment-web-application-firewall/AddManagementEndpoint.png
[ManagementAddServices]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-app-service-environment-web-application-firewall/ManagementAddServices.png
[ManagementDashboard]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-app-service-environment-web-application-firewall/ManagementDashboard.png
[ManagementLoginPage]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-app-service-environment-web-application-firewall/ManagementLoginPage.png
[TrafficManagerEndpoint]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-app-service-environment-web-application-firewall/TrafficManagerEndpoint.png
[ConfigureTrafficManager]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-app-service-environment-web-application-firewall/ConfigureTrafficManager.png
[WebsiteTranslations]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-app-service-environment-web-application-firewall/WebsiteTranslations.png









