---
title: Integrate your ILB App Service Environment with the Azure Application Gateway
description: Walkthrough on how to integrate an app in your ILB App Service Environment with an Application Gateway
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a6a74f17-bb57-40dd-8113-a20b50ba3050
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2018
ms.author: ccompy
ms.openlocfilehash: 3ab667418c8b2172e7af5f98dc6f9b3ee277530b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865065"
---
# <a name="integrate-your-ilb-app-service-environment-with-the-azure-application-gateway"></a><span data-ttu-id="f1aae-103">Integrate your ILB App Service Environment with the Azure Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f1aae-103">Integrate your ILB App Service Environment with the Azure Application Gateway</span></span> #

<span data-ttu-id="f1aae-104">The [App Service Environment](./intro.md) is a deployment of Azure App Service in the subnet of a customer's Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="f1aae-104">The [App Service Environment](./intro.md) is a deployment of Azure App Service in the subnet of a customer's Azure virtual network.</span></span> <span data-ttu-id="f1aae-105">It can be deployed with a public or private endpoint for app access.</span><span class="sxs-lookup"><span data-stu-id="f1aae-105">It can be deployed with a public or private endpoint for app access.</span></span> <span data-ttu-id="f1aae-106">The deployment of the App Service Environment with a private endpoint (that is, an internal load balancer) is called an ILB App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="f1aae-106">The deployment of the App Service Environment with a private endpoint (that is, an internal load balancer) is called an ILB App Service Environment.</span></span>  

<span data-ttu-id="f1aae-107">Web application firewalls help secure your web applications by inspecting inbound web traffic to block SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span><span class="sxs-lookup"><span data-stu-id="f1aae-107">Web application firewalls help secure your web applications by inspecting inbound web traffic to block SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="f1aae-108">It also inspects the responses from the back-end web servers for Data Loss Prevention (DLP).</span><span class="sxs-lookup"><span data-stu-id="f1aae-108">It also inspects the responses from the back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="f1aae-109">You can get a WAF device from the Azure marketplace or you can use the [Azure Application Gateway][appgw].</span><span class="sxs-lookup"><span data-stu-id="f1aae-109">You can get a WAF device from the Azure marketplace or you can use the [Azure Application Gateway][appgw].</span></span>

<span data-ttu-id="f1aae-110">The Azure Application Gateway is a virtual appliance that provides layer 7 load balancing, SSL offloading, and web application firewall (WAF) protection.</span><span class="sxs-lookup"><span data-stu-id="f1aae-110">The Azure Application Gateway is a virtual appliance that provides layer 7 load balancing, SSL offloading, and web application firewall (WAF) protection.</span></span> <span data-ttu-id="f1aae-111">It can listen on a public IP address and route traffic to your application endpoint.</span><span class="sxs-lookup"><span data-stu-id="f1aae-111">It can listen on a public IP address and route traffic to your application endpoint.</span></span> <span data-ttu-id="f1aae-112">The following information describes how to integrate a WAF-configured application gateway with an app in an ILB App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="f1aae-112">The following information describes how to integrate a WAF-configured application gateway with an app in an ILB App Service Environment.</span></span>  

<span data-ttu-id="f1aae-113">The integration of the application gateway with the ILB App Service Environment is at an app level.</span><span class="sxs-lookup"><span data-stu-id="f1aae-113">The integration of the application gateway with the ILB App Service Environment is at an app level.</span></span> <span data-ttu-id="f1aae-114">When you configure the application gateway with your ILB App Service Environment, you're doing it for specific apps in your ILB App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="f1aae-114">When you configure the application gateway with your ILB App Service Environment, you're doing it for specific apps in your ILB App Service Environment.</span></span> <span data-ttu-id="f1aae-115">This technique enables hosting secure multitenant applications in a single ILB App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="f1aae-115">This technique enables hosting secure multitenant applications in a single ILB App Service Environment.</span></span>  

![Application gateway pointing to app on an ILB App Service Environment][1]

<span data-ttu-id="f1aae-117">In this walkthrough, you will:</span><span class="sxs-lookup"><span data-stu-id="f1aae-117">In this walkthrough, you will:</span></span>

* <span data-ttu-id="f1aae-118">Create an Azure Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="f1aae-118">Create an Azure Application Gateway.</span></span>
* <span data-ttu-id="f1aae-119">Configure the Application Gateway to point to an app in your ILB App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="f1aae-119">Configure the Application Gateway to point to an app in your ILB App Service Environment.</span></span>
* <span data-ttu-id="f1aae-120">Configure your app to honor the custom domain name.</span><span class="sxs-lookup"><span data-stu-id="f1aae-120">Configure your app to honor the custom domain name.</span></span>
* <span data-ttu-id="f1aae-121">Edit the public DNS host name that points to your application gateway.</span><span class="sxs-lookup"><span data-stu-id="f1aae-121">Edit the public DNS host name that points to your application gateway.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1aae-122">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f1aae-122">Prerequisites</span></span>

<span data-ttu-id="f1aae-123">To integrate your Application Gateway with your ILB App Service Environment, you need:</span><span class="sxs-lookup"><span data-stu-id="f1aae-123">To integrate your Application Gateway with your ILB App Service Environment, you need:</span></span>

* <span data-ttu-id="f1aae-124">An ILB App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="f1aae-124">An ILB App Service Environment.</span></span>
* <span data-ttu-id="f1aae-125">An app running in the ILB App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="f1aae-125">An app running in the ILB App Service Environment.</span></span>
* <span data-ttu-id="f1aae-126">An internet routable domain name to be used with your app in the ILB App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="f1aae-126">An internet routable domain name to be used with your app in the ILB App Service Environment.</span></span>
* <span data-ttu-id="f1aae-127">The ILB address that your ILB App Service Environment uses.</span><span class="sxs-lookup"><span data-stu-id="f1aae-127">The ILB address that your ILB App Service Environment uses.</span></span> <span data-ttu-id="f1aae-128">This information is in the App Service Environment portal under **Settings** > **IP Addresses**:</span><span class="sxs-lookup"><span data-stu-id="f1aae-128">This information is in the App Service Environment portal under **Settings** > **IP Addresses**:</span></span>

    ![Example list of IP addresses used by the ILB App Service Environment][9]
    
* <span data-ttu-id="f1aae-130">A public DNS name that is used later to point to your Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="f1aae-130">A public DNS name that is used later to point to your Application Gateway.</span></span> 

<span data-ttu-id="f1aae-131">For details on how to create an ILB App Service Environment, see [Creating and using an ILB App Service Environment][ilbase].</span><span class="sxs-lookup"><span data-stu-id="f1aae-131">For details on how to create an ILB App Service Environment, see [Creating and using an ILB App Service Environment][ilbase].</span></span>

<span data-ttu-id="f1aae-132">This article assumes that you want an Application Gateway in the same Azure virtual network where the App Service Environment is deployed.</span><span class="sxs-lookup"><span data-stu-id="f1aae-132">This article assumes that you want an Application Gateway in the same Azure virtual network where the App Service Environment is deployed.</span></span> <span data-ttu-id="f1aae-133">Before you start to create the Application Gateway, pick or create a subnet that you will use to host the gateway.</span><span class="sxs-lookup"><span data-stu-id="f1aae-133">Before you start to create the Application Gateway, pick or create a subnet that you will use to host the gateway.</span></span> 

<span data-ttu-id="f1aae-134">You should use a subnet that is not the one named GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="f1aae-134">You should use a subnet that is not the one named GatewaySubnet.</span></span> <span data-ttu-id="f1aae-135">If you put the Application Gateway in GatewaySubnet, you'll be unable to create a virtual network gateway later.</span><span class="sxs-lookup"><span data-stu-id="f1aae-135">If you put the Application Gateway in GatewaySubnet, you'll be unable to create a virtual network gateway later.</span></span> 

<span data-ttu-id="f1aae-136">You also cannot put the gateway in the subnet that your ILB App Service Environment uses.</span><span class="sxs-lookup"><span data-stu-id="f1aae-136">You also cannot put the gateway in the subnet that your ILB App Service Environment uses.</span></span> <span data-ttu-id="f1aae-137">The App Service Environment is the only thing that can be in this subnet.</span><span class="sxs-lookup"><span data-stu-id="f1aae-137">The App Service Environment is the only thing that can be in this subnet.</span></span>

## <a name="configuration-steps"></a><span data-ttu-id="f1aae-138">Configuration steps</span><span class="sxs-lookup"><span data-stu-id="f1aae-138">Configuration steps</span></span> ##

1. <span data-ttu-id="f1aae-139">In the Azure portal, go to **New** > **Network** > **Application Gateway**.</span><span class="sxs-lookup"><span data-stu-id="f1aae-139">In the Azure portal, go to **New** > **Network** > **Application Gateway**.</span></span>

1. <span data-ttu-id="f1aae-140">In the **Basics** area:</span><span class="sxs-lookup"><span data-stu-id="f1aae-140">In the **Basics** area:</span></span>

   <span data-ttu-id="f1aae-141">a.</span><span class="sxs-lookup"><span data-stu-id="f1aae-141">a.</span></span> <span data-ttu-id="f1aae-142">For **Name**, enter the name of the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="f1aae-142">For **Name**, enter the name of the Application Gateway.</span></span>

   <span data-ttu-id="f1aae-143">b.</span><span class="sxs-lookup"><span data-stu-id="f1aae-143">b.</span></span> <span data-ttu-id="f1aae-144">For **Tier**, select **WAF**.</span><span class="sxs-lookup"><span data-stu-id="f1aae-144">For **Tier**, select **WAF**.</span></span>

   <span data-ttu-id="f1aae-145">c.</span><span class="sxs-lookup"><span data-stu-id="f1aae-145">c.</span></span> <span data-ttu-id="f1aae-146">For **Subscription**, select the same subscription that the App Service Environment virtual network uses.</span><span class="sxs-lookup"><span data-stu-id="f1aae-146">For **Subscription**, select the same subscription that the App Service Environment virtual network uses.</span></span>

   <span data-ttu-id="f1aae-147">d.</span><span class="sxs-lookup"><span data-stu-id="f1aae-147">d.</span></span> <span data-ttu-id="f1aae-148">For **Resource group**, create or select the resource group.</span><span class="sxs-lookup"><span data-stu-id="f1aae-148">For **Resource group**, create or select the resource group.</span></span>

   <span data-ttu-id="f1aae-149">e.</span><span class="sxs-lookup"><span data-stu-id="f1aae-149">e.</span></span> <span data-ttu-id="f1aae-150">For **Location**, select the location of the App Service Environment virtual network.</span><span class="sxs-lookup"><span data-stu-id="f1aae-150">For **Location**, select the location of the App Service Environment virtual network.</span></span>

   ![New Application Gateway creation basics][2]

1. <span data-ttu-id="f1aae-152">In the **Settings** area:</span><span class="sxs-lookup"><span data-stu-id="f1aae-152">In the **Settings** area:</span></span>

   <span data-ttu-id="f1aae-153">a.</span><span class="sxs-lookup"><span data-stu-id="f1aae-153">a.</span></span> <span data-ttu-id="f1aae-154">For **Virtual network**, select the App Service Environment virtual network.</span><span class="sxs-lookup"><span data-stu-id="f1aae-154">For **Virtual network**, select the App Service Environment virtual network.</span></span>

   <span data-ttu-id="f1aae-155">b.</span><span class="sxs-lookup"><span data-stu-id="f1aae-155">b.</span></span> <span data-ttu-id="f1aae-156">For **Subnet**, select the subnet where the Application Gateway needs to be deployed.</span><span class="sxs-lookup"><span data-stu-id="f1aae-156">For **Subnet**, select the subnet where the Application Gateway needs to be deployed.</span></span> <span data-ttu-id="f1aae-157">Do not use GatewaySubnet, because it will prevent the creation of VPN gateways.</span><span class="sxs-lookup"><span data-stu-id="f1aae-157">Do not use GatewaySubnet, because it will prevent the creation of VPN gateways.</span></span>

   <span data-ttu-id="f1aae-158">c.</span><span class="sxs-lookup"><span data-stu-id="f1aae-158">c.</span></span> <span data-ttu-id="f1aae-159">For **IP address type**, select **Public**.</span><span class="sxs-lookup"><span data-stu-id="f1aae-159">For **IP address type**, select **Public**.</span></span>

   <span data-ttu-id="f1aae-160">d.</span><span class="sxs-lookup"><span data-stu-id="f1aae-160">d.</span></span> <span data-ttu-id="f1aae-161">For **Public IP address**, select a public IP address.</span><span class="sxs-lookup"><span data-stu-id="f1aae-161">For **Public IP address**, select a public IP address.</span></span> <span data-ttu-id="f1aae-162">If you don't have one, create one now.</span><span class="sxs-lookup"><span data-stu-id="f1aae-162">If you don't have one, create one now.</span></span>

   <span data-ttu-id="f1aae-163">e.</span><span class="sxs-lookup"><span data-stu-id="f1aae-163">e.</span></span> <span data-ttu-id="f1aae-164">For **Protocol**, select **HTTP** or **HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="f1aae-164">For **Protocol**, select **HTTP** or **HTTPS**.</span></span> <span data-ttu-id="f1aae-165">If you're configuring for HTTPS, you need to provide a PFX certificate.</span><span class="sxs-lookup"><span data-stu-id="f1aae-165">If you're configuring for HTTPS, you need to provide a PFX certificate.</span></span>

   <span data-ttu-id="f1aae-166">f.</span><span class="sxs-lookup"><span data-stu-id="f1aae-166">f.</span></span> <span data-ttu-id="f1aae-167">For **Web application firewall**, you can enable the firewall and also set it for either **Detection** or **Prevention** as you see fit.</span><span class="sxs-lookup"><span data-stu-id="f1aae-167">For **Web application firewall**, you can enable the firewall and also set it for either **Detection** or **Prevention** as you see fit.</span></span>

   ![New Application Gateway creation settings][3]
    
1. <span data-ttu-id="f1aae-169">In the **Summary** section, review the settings and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="f1aae-169">In the **Summary** section, review the settings and select **OK**.</span></span> <span data-ttu-id="f1aae-170">Your Application Gateway can take a little more than 30 minutes to complete setup.</span><span class="sxs-lookup"><span data-stu-id="f1aae-170">Your Application Gateway can take a little more than 30 minutes to complete setup.</span></span>  

1. <span data-ttu-id="f1aae-171">After your Application Gateway completes setup, go to your Application Gateway portal.</span><span class="sxs-lookup"><span data-stu-id="f1aae-171">After your Application Gateway completes setup, go to your Application Gateway portal.</span></span> <span data-ttu-id="f1aae-172">Select **Backend pool**.</span><span class="sxs-lookup"><span data-stu-id="f1aae-172">Select **Backend pool**.</span></span> <span data-ttu-id="f1aae-173">Add the ILB address for your ILB App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="f1aae-173">Add the ILB address for your ILB App Service Environment.</span></span>

   ![Configure backend pool][4]

1. <span data-ttu-id="f1aae-175">After the process of configuring your back-end pool is completed, select **Health probes**.</span><span class="sxs-lookup"><span data-stu-id="f1aae-175">After the process of configuring your back-end pool is completed, select **Health probes**.</span></span> <span data-ttu-id="f1aae-176">Create a health probe for the domain name that you want to use for your app.</span><span class="sxs-lookup"><span data-stu-id="f1aae-176">Create a health probe for the domain name that you want to use for your app.</span></span> 

   ![Configure health probes][5]
    
1. <span data-ttu-id="f1aae-178">After the process of configuring your health probes is completed, select **HTTP settings**.</span><span class="sxs-lookup"><span data-stu-id="f1aae-178">After the process of configuring your health probes is completed, select **HTTP settings**.</span></span> <span data-ttu-id="f1aae-179">Edit the existing settings, select **Use Custom probe**, and pick the probe that you configured.</span><span class="sxs-lookup"><span data-stu-id="f1aae-179">Edit the existing settings, select **Use Custom probe**, and pick the probe that you configured.</span></span>

   ![Configure HTTP settings][6]
    
1. <span data-ttu-id="f1aae-181">Go to the Application Gateway's **Overview** section, and copy the public IP address that your Application Gateway uses.</span><span class="sxs-lookup"><span data-stu-id="f1aae-181">Go to the Application Gateway's **Overview** section, and copy the public IP address that your Application Gateway uses.</span></span> <span data-ttu-id="f1aae-182">Set that IP address as an A record for your app domain name, or use the DNS name for that address in a CNAME record.</span><span class="sxs-lookup"><span data-stu-id="f1aae-182">Set that IP address as an A record for your app domain name, or use the DNS name for that address in a CNAME record.</span></span> <span data-ttu-id="f1aae-183">It's easier to select the public IP address and copy it from the public IP address's UI rather than copy it from the link in the Application Gateway's **Overview** section.</span><span class="sxs-lookup"><span data-stu-id="f1aae-183">It's easier to select the public IP address and copy it from the public IP address's UI rather than copy it from the link in the Application Gateway's **Overview** section.</span></span> 

   ![Application Gateway portal][7]

1. <span data-ttu-id="f1aae-185">Set the custom domain name for your app in your ILB App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="f1aae-185">Set the custom domain name for your app in your ILB App Service Environment.</span></span> <span data-ttu-id="f1aae-186">Go to your app in the portal, and under **Settings**, select **Custom domains**.</span><span class="sxs-lookup"><span data-stu-id="f1aae-186">Go to your app in the portal, and under **Settings**, select **Custom domains**.</span></span>

   ![Set custom domain name on the app][8]

<span data-ttu-id="f1aae-188">There is information on setting custom domain names for your web apps in the article [Setting custom domain names for your web app][custom-domain].</span><span class="sxs-lookup"><span data-stu-id="f1aae-188">There is information on setting custom domain names for your web apps in the article [Setting custom domain names for your web app][custom-domain].</span></span> <span data-ttu-id="f1aae-189">But for an app in an ILB App Service Environment, there isn't any validation on the domain name.</span><span class="sxs-lookup"><span data-stu-id="f1aae-189">But for an app in an ILB App Service Environment, there isn't any validation on the domain name.</span></span> <span data-ttu-id="f1aae-190">Because you own the DNS that manages the app endpoints, you can put whatever you want in there.</span><span class="sxs-lookup"><span data-stu-id="f1aae-190">Because you own the DNS that manages the app endpoints, you can put whatever you want in there.</span></span> <span data-ttu-id="f1aae-191">The custom domain name that you add in this case does not need to be in your DNS, but it does still need to be configured with your app.</span><span class="sxs-lookup"><span data-stu-id="f1aae-191">The custom domain name that you add in this case does not need to be in your DNS, but it does still need to be configured with your app.</span></span> 

<span data-ttu-id="f1aae-192">After setup is completed and you have allowed a short amount of time for your DNS changes to propagate, you can access your app by using the custom domain name that you created.</span><span class="sxs-lookup"><span data-stu-id="f1aae-192">After setup is completed and you have allowed a short amount of time for your DNS changes to propagate, you can access your app by using the custom domain name that you created.</span></span> 


<!--IMAGES-->
[1]: ./media/integrate-with-application-gateway/appgw-highlevel.png
[2]: ./media/integrate-with-application-gateway/appgw-createbasics.png
[3]: ./media/integrate-with-application-gateway/appgw-createsettings.png
[4]: ./media/integrate-with-application-gateway/appgw-backendpool.png
[5]: ./media/integrate-with-application-gateway/appgw-healthprobe.png
[6]: ./media/integrate-with-application-gateway/appgw-httpsettings.png
[7]: ./media/integrate-with-application-gateway/appgw-publicip.png
[8]: ./media/integrate-with-application-gateway/appgw-customdomainname.png
[9]: ./media/integrate-with-application-gateway/appgw-iplist.png

<!--LINKS-->
[appgw]: http://docs.microsoft.com/azure/application-gateway/application-gateway-introduction
[custom-domain]: ../app-service-web-tutorial-custom-domain.md
[ilbase]: ./create-ilb-ase.md
