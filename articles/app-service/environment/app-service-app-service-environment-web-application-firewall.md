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
ms.topic: tutorial
ms.date: 03/03/2018
ms.author: naziml
ms.custom: mvc
ms.openlocfilehash: bc59d8671d904cf5096d616213cc4674ef5743b8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870918"
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a><span data-ttu-id="b2341-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span><span class="sxs-lookup"><span data-stu-id="b2341-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="b2341-104">Overview</span><span class="sxs-lookup"><span data-stu-id="b2341-104">Overview</span></span>

<span data-ttu-id="b2341-105">Web application firewalls (WAF) help secure your web applications by inspecting inbound web traffic to block SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span><span class="sxs-lookup"><span data-stu-id="b2341-105">Web application firewalls (WAF) help secure your web applications by inspecting inbound web traffic to block SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="b2341-106">They also inspect the responses from the back-end web servers for Data Loss Prevention (DLP).</span><span class="sxs-lookup"><span data-stu-id="b2341-106">They also inspect the responses from the back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="b2341-107">Combined with the isolation and additional scaling provided by App Service Environments, this provides an ideal environment to host business critical web applications that need to withstand malicious requests and high volume traffic.</span><span class="sxs-lookup"><span data-stu-id="b2341-107">Combined with the isolation and additional scaling provided by App Service Environments, this provides an ideal environment to host business critical web applications that need to withstand malicious requests and high volume traffic.</span></span> <span data-ttu-id="b2341-108">Azure provides a WAF capability with the [Application Gateway](http://docs.microsoft.com/azure/application-gateway/application-gateway-introduction).</span><span class="sxs-lookup"><span data-stu-id="b2341-108">Azure provides a WAF capability with the [Application Gateway](http://docs.microsoft.com/azure/application-gateway/application-gateway-introduction).</span></span>  <span data-ttu-id="b2341-109">To see how to integrate your App Service Environment with an Application Gateway read the [Integrate your ILB ASE with an Application Gateway](http://docs.microsoft.com/azure/app-service/environment/integrate-with-application-gateway) document.</span><span class="sxs-lookup"><span data-stu-id="b2341-109">To see how to integrate your App Service Environment with an Application Gateway read the [Integrate your ILB ASE with an Application Gateway](http://docs.microsoft.com/azure/app-service/environment/integrate-with-application-gateway) document.</span></span>

<span data-ttu-id="b2341-110">In addtion to the Azure Application Gateway, there are multiple marketplace options like the [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that are available on the [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/).</span><span class="sxs-lookup"><span data-stu-id="b2341-110">In addtion to the Azure Application Gateway, there are multiple marketplace options like the [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that are available on the [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/).</span></span> <span data-ttu-id="b2341-111">The rest of this document focuses on how to integrate your App Service Environment with a Barracuda WAF device.</span><span class="sxs-lookup"><span data-stu-id="b2341-111">The rest of this document focuses on how to integrate your App Service Environment with a Barracuda WAF device.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a><span data-ttu-id="b2341-112">Setup</span><span class="sxs-lookup"><span data-stu-id="b2341-112">Setup</span></span>
<span data-ttu-id="b2341-113">For this document, we configure the App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from the WAF can reach the App Service Environment and it is not accessible from the DMZ.</span><span class="sxs-lookup"><span data-stu-id="b2341-113">For this document, we configure the App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from the WAF can reach the App Service Environment and it is not accessible from the DMZ.</span></span> <span data-ttu-id="b2341-114">We also have Azure Traffic Manager in front of the Barracuda WAF instances to load balance across Azure data centers and regions.</span><span class="sxs-lookup"><span data-stu-id="b2341-114">We also have Azure Traffic Manager in front of the Barracuda WAF instances to load balance across Azure data centers and regions.</span></span> <span data-ttu-id="b2341-115">A high-level diagram of the setup would look like the following image:</span><span class="sxs-lookup"><span data-stu-id="b2341-115">A high-level diagram of the setup would look like the following image:</span></span>

![Architecture][Architecture] 

> [!NOTE]
> <span data-ttu-id="b2341-117">With the introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure the ASE to be inaccessible from the DMZ and only be available to the private network.</span><span class="sxs-lookup"><span data-stu-id="b2341-117">With the introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure the ASE to be inaccessible from the DMZ and only be available to the private network.</span></span> 
> 
> 

## <a name="configuring-your-app-service-environment"></a><span data-ttu-id="b2341-118">Configuring your App Service Environment</span><span class="sxs-lookup"><span data-stu-id="b2341-118">Configuring your App Service Environment</span></span>
<span data-ttu-id="b2341-119">To configure an App Service Environment, refer to [our documentation](app-service-web-how-to-create-an-app-service-environment.md) on the subject.</span><span class="sxs-lookup"><span data-stu-id="b2341-119">To configure an App Service Environment, refer to [our documentation](app-service-web-how-to-create-an-app-service-environment.md) on the subject.</span></span> <span data-ttu-id="b2341-120">Once you have an App Service Environment created, you can create Web Apps, API Apps, and [Mobile Apps](../../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind the WAF we configure in the next section.</span><span class="sxs-lookup"><span data-stu-id="b2341-120">Once you have an App Service Environment created, you can create Web Apps, API Apps, and [Mobile Apps](../../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind the WAF we configure in the next section.</span></span>

## <a name="configuring-your-barracuda-waf-cloud-service"></a><span data-ttu-id="b2341-121">Configuring your Barracuda WAF Cloud Service</span><span class="sxs-lookup"><span data-stu-id="b2341-121">Configuring your Barracuda WAF Cloud Service</span></span>
<span data-ttu-id="b2341-122">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="b2341-122">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span></span> <span data-ttu-id="b2341-123">But because we want redundancy and not introduce a single point of failure, you want to deploy at least two WAF instance VMs into the same Cloud Service when following these instructions.</span><span class="sxs-lookup"><span data-stu-id="b2341-123">But because we want redundancy and not introduce a single point of failure, you want to deploy at least two WAF instance VMs into the same Cloud Service when following these instructions.</span></span>

### <a name="adding-endpoints-to-cloud-service"></a><span data-ttu-id="b2341-124">Adding Endpoints to Cloud Service</span><span class="sxs-lookup"><span data-stu-id="b2341-124">Adding Endpoints to Cloud Service</span></span>
<span data-ttu-id="b2341-125">Once you have 2 or more WAF VM instances in your Cloud Service, you can use the [Azure portal](https://portal.azure.com/) to add HTTP and HTTPS endpoints that are used by your application as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="b2341-125">Once you have 2 or more WAF VM instances in your Cloud Service, you can use the [Azure portal](https://portal.azure.com/) to add HTTP and HTTPS endpoints that are used by your application as shown in the following image:</span></span>

![Configure Endpoint][ConfigureEndpoint]

<span data-ttu-id="b2341-127">If your applications use other endpoints, make sure to add them to this list as well.</span><span class="sxs-lookup"><span data-stu-id="b2341-127">If your applications use other endpoints, make sure to add them to this list as well.</span></span> 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a><span data-ttu-id="b2341-128">Configuring Barracuda WAF through its Management Portal</span><span class="sxs-lookup"><span data-stu-id="b2341-128">Configuring Barracuda WAF through its Management Portal</span></span>
<span data-ttu-id="b2341-129">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span><span class="sxs-lookup"><span data-stu-id="b2341-129">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span></span> <span data-ttu-id="b2341-130">If you have multiple instances of the WAF VMs, you need to repeat the steps here for each VM instance.</span><span class="sxs-lookup"><span data-stu-id="b2341-130">If you have multiple instances of the WAF VMs, you need to repeat the steps here for each VM instance.</span></span> 

> [!NOTE]
> <span data-ttu-id="b2341-131">Once you are done with WAF configuration, remove the TCP/8000 endpoint from all your WAF VMs to keep your WAF secure.</span><span class="sxs-lookup"><span data-stu-id="b2341-131">Once you are done with WAF configuration, remove the TCP/8000 endpoint from all your WAF VMs to keep your WAF secure.</span></span>
> 
> 

<span data-ttu-id="b2341-132">Add the management endpoint as shown in the following image to configure your Barracuda WAF.</span><span class="sxs-lookup"><span data-stu-id="b2341-132">Add the management endpoint as shown in the following image to configure your Barracuda WAF.</span></span>

![Add Management Endpoint][AddManagementEndpoint]

<span data-ttu-id="b2341-134">Use a browser to browse to the management endpoint on your Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="b2341-134">Use a browser to browse to the management endpoint on your Cloud Service.</span></span> <span data-ttu-id="b2341-135">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing to http://test.cloudapp.net:8000.</span><span class="sxs-lookup"><span data-stu-id="b2341-135">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing to http://test.cloudapp.net:8000.</span></span> <span data-ttu-id="b2341-136">You should see a login page like the following image that you can log in using credentials you specified in the WAF VM setup phase.</span><span class="sxs-lookup"><span data-stu-id="b2341-136">You should see a login page like the following image that you can log in using credentials you specified in the WAF VM setup phase.</span></span>

![Management Login Page][ManagementLoginPage]

<span data-ttu-id="b2341-138">Once you log in, you should see a dashboard like the one in the following image that presents basic statistics about the WAF protection.</span><span class="sxs-lookup"><span data-stu-id="b2341-138">Once you log in, you should see a dashboard like the one in the following image that presents basic statistics about the WAF protection.</span></span>

![Management Dashboard][ManagementDashboard]

<span data-ttu-id="b2341-140">Clicking on the **Services** tab lets you configure your WAF for services it is protecting.</span><span class="sxs-lookup"><span data-stu-id="b2341-140">Clicking on the **Services** tab lets you configure your WAF for services it is protecting.</span></span> <span data-ttu-id="b2341-141">For more details on configuring your Barracuda WAF, see [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span><span class="sxs-lookup"><span data-stu-id="b2341-141">For more details on configuring your Barracuda WAF, see [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span></span> <span data-ttu-id="b2341-142">In the following example, an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span><span class="sxs-lookup"><span data-stu-id="b2341-142">In the following example, an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span></span>

![Management Add Services][ManagementAddServices]

> [!NOTE]
> <span data-ttu-id="b2341-144">Depending on how your applications are configured and what features are being used in your App Service Environment, you need to forward traffic for TCP ports other than 80 and 443, for example, if you have IP SSL setup for a Web App.</span><span class="sxs-lookup"><span data-stu-id="b2341-144">Depending on how your applications are configured and what features are being used in your App Service Environment, you need to forward traffic for TCP ports other than 80 and 443, for example, if you have IP SSL setup for a Web App.</span></span> <span data-ttu-id="b2341-145">For a list of network ports used in App Service Environments, see [Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span><span class="sxs-lookup"><span data-stu-id="b2341-145">For a list of network ports used in App Service Environments, see [Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span></span>
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a><span data-ttu-id="b2341-146">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span><span class="sxs-lookup"><span data-stu-id="b2341-146">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span></span>
<span data-ttu-id="b2341-147">If your application is available in multiple regions, then you would want to load balance them behind [Azure Traffic Manager](../../traffic-manager/traffic-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b2341-147">If your application is available in multiple regions, then you would want to load balance them behind [Azure Traffic Manager](../../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="b2341-148">To do so, you can add an endpoint in the [Azure portal](https://portal.azure.com) using the Cloud Service name for your WAF in the Traffic Manager profile as shown in the following image.</span><span class="sxs-lookup"><span data-stu-id="b2341-148">To do so, you can add an endpoint in the [Azure portal](https://portal.azure.com) using the Cloud Service name for your WAF in the Traffic Manager profile as shown in the following image.</span></span> 

![Traffic Manager Endpoint][TrafficManagerEndpoint]

<span data-ttu-id="b2341-150">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager to ping for the availability of your application.</span><span class="sxs-lookup"><span data-stu-id="b2341-150">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager to ping for the availability of your application.</span></span> <span data-ttu-id="b2341-151">You can configure the URL on the **Configuration** page in the [Azure portal](https://portal.azure.com) as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="b2341-151">You can configure the URL on the **Configuration** page in the [Azure portal](https://portal.azure.com) as shown in the following image:</span></span>

![Configure Traffic Manager][ConfigureTrafficManager]

<span data-ttu-id="b2341-153">To forward the Traffic Manager pings from your WAF to your application, you need to set up Website Translations on your Barracuda WAF to forward traffic to your application as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="b2341-153">To forward the Traffic Manager pings from your WAF to your application, you need to set up Website Translations on your Barracuda WAF to forward traffic to your application as shown in the following example:</span></span>

![Website Translations][WebsiteTranslations]

## <a name="securing-traffic-to-app-service-environment-using-network-security-groups-nsg"></a><span data-ttu-id="b2341-155">Securing Traffic to App Service Environment Using Network Security Groups (NSG)</span><span class="sxs-lookup"><span data-stu-id="b2341-155">Securing Traffic to App Service Environment Using Network Security Groups (NSG)</span></span>
<span data-ttu-id="b2341-156">Follow the [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic to your App Service Environment from the WAF only by using the VIP address of your Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="b2341-156">Follow the [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic to your App Service Environment from the WAF only by using the VIP address of your Cloud Service.</span></span> <span data-ttu-id="b2341-157">Here's a sample Powershell command for performing this task for TCP port 80.</span><span class="sxs-lookup"><span data-stu-id="b2341-157">Here's a sample Powershell command for performing this task for TCP port 80.</span></span>

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

<span data-ttu-id="b2341-158">Replace the SourceAddressPrefix with the Virtual IP Address (VIP) of your WAF's Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="b2341-158">Replace the SourceAddressPrefix with the Virtual IP Address (VIP) of your WAF's Cloud Service.</span></span>

> [!NOTE]
> <span data-ttu-id="b2341-159">The VIP of your Cloud Service changes when you delete and re-create the Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="b2341-159">The VIP of your Cloud Service changes when you delete and re-create the Cloud Service.</span></span> <span data-ttu-id="b2341-160">Make sure to update the IP address in the Network Resource group once you do so.</span><span class="sxs-lookup"><span data-stu-id="b2341-160">Make sure to update the IP address in the Network Resource group once you do so.</span></span> 
> 
> 

<!-- IMAGES -->
[Architecture]: ./media/app-service-app-service-environment-web-application-firewall/Architecture.png
[ConfigureEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureEndpoint.png
[AddManagementEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/AddManagementEndpoint.png
[ManagementAddServices]: ./media/app-service-app-service-environment-web-application-firewall/ManagementAddServices.png
[ManagementDashboard]: ./media/app-service-app-service-environment-web-application-firewall/ManagementDashboard.png
[ManagementLoginPage]: ./media/app-service-app-service-environment-web-application-firewall/ManagementLoginPage.png
[TrafficManagerEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/TrafficManagerEndpoint.png
[ConfigureTrafficManager]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureTrafficManager.png
[WebsiteTranslations]: ./media/app-service-app-service-environment-web-application-firewall/WebsiteTranslations.png
