---
title: Host multiple sites with Azure Application Gateway | Microsoft Docs
description: This page provides instructions to configure an existing Azure application gateway for hosting multiple web applications on the same gateway with the Azure portal.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 95f892f6-fa27-47ee-b980-7abf4f2c66a9
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: ee38ed6d9f1641b126ea7a6f8366f5a8c7fa82c1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553455"
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="6613d-103">Configure an existing application gateway for hosting multiple web applications</span><span class="sxs-lookup"><span data-stu-id="6613d-103">Configure an existing application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-multisite-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

<span data-ttu-id="6613d-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span><span class="sxs-lookup"><span data-stu-id="6613d-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span></span> <span data-ttu-id="6613d-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span><span class="sxs-lookup"><span data-stu-id="6613d-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span></span> <span data-ttu-id="6613d-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span><span class="sxs-lookup"><span data-stu-id="6613d-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span></span> <span data-ttu-id="6613d-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span><span class="sxs-lookup"><span data-stu-id="6613d-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span></span> <span data-ttu-id="6613d-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span><span class="sxs-lookup"><span data-stu-id="6613d-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span></span> <span data-ttu-id="6613d-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span><span class="sxs-lookup"><span data-stu-id="6613d-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="6613d-112">Scenario</span><span class="sxs-lookup"><span data-stu-id="6613d-112">Scenario</span></span>

<span data-ttu-id="6613d-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span><span class="sxs-lookup"><span data-stu-id="6613d-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="6613d-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="6613d-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span></span>

![multisite scenario][multisite]

## <a name="before-you-begin"></a><span data-ttu-id="6613d-116">Before you begin</span><span class="sxs-lookup"><span data-stu-id="6613d-116">Before you begin</span></span>

<span data-ttu-id="6613d-117">This scenario adds multi-site support to an existing application gateway.</span><span class="sxs-lookup"><span data-stu-id="6613d-117">This scenario adds multi-site support to an existing application gateway.</span></span> <span data-ttu-id="6613d-118">To complete this scenario, an existing application gateway needs to be available to configure.</span><span class="sxs-lookup"><span data-stu-id="6613d-118">To complete this scenario, an existing application gateway needs to be available to configure.</span></span> <span data-ttu-id="6613d-119">Visit [Create an application gateway by using the portal](application-gateway-create-gateway-portal.md) to learn how to create a basic application gateway in the portal.</span><span class="sxs-lookup"><span data-stu-id="6613d-119">Visit [Create an application gateway by using the portal](application-gateway-create-gateway-portal.md) to learn how to create a basic application gateway in the portal.</span></span>

<span data-ttu-id="6613d-120">The following are the steps needed to update the application gateway:</span><span class="sxs-lookup"><span data-stu-id="6613d-120">The following are the steps needed to update the application gateway:</span></span>

1. <span data-ttu-id="6613d-121">Create back-end pools to use for each site.</span><span class="sxs-lookup"><span data-stu-id="6613d-121">Create back-end pools to use for each site.</span></span>
2. <span data-ttu-id="6613d-122">Create a listener for each site application gateway supports.</span><span class="sxs-lookup"><span data-stu-id="6613d-122">Create a listener for each site application gateway supports.</span></span>
3. <span data-ttu-id="6613d-123">Create rules to map each listener with the appropriate back-end.</span><span class="sxs-lookup"><span data-stu-id="6613d-123">Create rules to map each listener with the appropriate back-end.</span></span>

## <a name="requirements"></a><span data-ttu-id="6613d-124">Requirements</span><span class="sxs-lookup"><span data-stu-id="6613d-124">Requirements</span></span>

* <span data-ttu-id="6613d-125">**Back-end server pool:** The list of IP addresses of the back-end servers.</span><span class="sxs-lookup"><span data-stu-id="6613d-125">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="6613d-126">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="6613d-126">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="6613d-127">FQDN can also be used.</span><span class="sxs-lookup"><span data-stu-id="6613d-127">FQDN can also be used.</span></span>
* <span data-ttu-id="6613d-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span><span class="sxs-lookup"><span data-stu-id="6613d-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="6613d-129">These settings are tied to a pool and are applied to all servers within the pool.</span><span class="sxs-lookup"><span data-stu-id="6613d-129">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="6613d-130">**Front-end port:** This port is the public port that is opened on the application gateway.</span><span class="sxs-lookup"><span data-stu-id="6613d-130">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="6613d-131">Traffic hits this port, and then gets redirected to one of the back-end servers.</span><span class="sxs-lookup"><span data-stu-id="6613d-131">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="6613d-132">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span><span class="sxs-lookup"><span data-stu-id="6613d-132">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="6613d-133">For multi-site enabled application gateways, host name and SNI indicators are also added.</span><span class="sxs-lookup"><span data-stu-id="6613d-133">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="6613d-134">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span><span class="sxs-lookup"><span data-stu-id="6613d-134">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="6613d-135">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span><span class="sxs-lookup"><span data-stu-id="6613d-135">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="6613d-136">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span><span class="sxs-lookup"><span data-stu-id="6613d-136">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span> 
* <span data-ttu-id="6613d-137">**Certificates:** Each listener requires a unique certificate, in this example 2 listeners are created for multi-site.</span><span class="sxs-lookup"><span data-stu-id="6613d-137">**Certificates:** Each listener requires a unique certificate, in this example 2 listeners are created for multi-site.</span></span> <span data-ttu-id="6613d-138">Two .pfx certificates and the passwords for them need to be created.</span><span class="sxs-lookup"><span data-stu-id="6613d-138">Two .pfx certificates and the passwords for them need to be created.</span></span>

## <a name="create-back-end-pools-for-each-site"></a><span data-ttu-id="6613d-139">Create back-end pools for each site</span><span class="sxs-lookup"><span data-stu-id="6613d-139">Create back-end pools for each site</span></span>

<span data-ttu-id="6613d-140">A back-end pool for each site that application gateway supports is needed, in this case 2 are be created, one for contoso11.com and one for fabrikam11.com.</span><span class="sxs-lookup"><span data-stu-id="6613d-140">A back-end pool for each site that application gateway supports is needed, in this case 2 are be created, one for contoso11.com and one for fabrikam11.com.</span></span>

### <a name="step-1"></a><span data-ttu-id="6613d-141">Step 1</span><span class="sxs-lookup"><span data-stu-id="6613d-141">Step 1</span></span>

<span data-ttu-id="6613d-142">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6613d-142">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="6613d-143">Select **Backend pools** and click **Add**</span><span class="sxs-lookup"><span data-stu-id="6613d-143">Select **Backend pools** and click **Add**</span></span>

![add backend pools][7]

### <a name="step-2"></a><span data-ttu-id="6613d-145">Step 2</span><span class="sxs-lookup"><span data-stu-id="6613d-145">Step 2</span></span>

<span data-ttu-id="6613d-146">Fill in the information for the back-end pool **pool1**, adding the ip addresses or FQDNs for the back-end servers and click **OK**</span><span class="sxs-lookup"><span data-stu-id="6613d-146">Fill in the information for the back-end pool **pool1**, adding the ip addresses or FQDNs for the back-end servers and click **OK**</span></span>

![backend pool pool1 settings][8]

### <a name="step-3"></a><span data-ttu-id="6613d-148">Step 3</span><span class="sxs-lookup"><span data-stu-id="6613d-148">Step 3</span></span>

<span data-ttu-id="6613d-149">On the backend-pools blade click **Add** to add an additional back-end pool **pool2**, adding the ip addresses or FQDNS for the back-end servers and click **OK**</span><span class="sxs-lookup"><span data-stu-id="6613d-149">On the backend-pools blade click **Add** to add an additional back-end pool **pool2**, adding the ip addresses or FQDNS for the back-end servers and click **OK**</span></span>

![backend pool pool2 settings][9]

## <a name="create-listeners-for-each-back-end"></a><span data-ttu-id="6613d-151">Create listeners for each back-end</span><span class="sxs-lookup"><span data-stu-id="6613d-151">Create listeners for each back-end</span></span>

<span data-ttu-id="6613d-152">Application Gateway relies on HTTP 1.1 host headers to host more than one website on the same public IP address and port.</span><span class="sxs-lookup"><span data-stu-id="6613d-152">Application Gateway relies on HTTP 1.1 host headers to host more than one website on the same public IP address and port.</span></span> <span data-ttu-id="6613d-153">The basic listener created in the portal does not contain this property.</span><span class="sxs-lookup"><span data-stu-id="6613d-153">The basic listener created in the portal does not contain this property.</span></span>

### <a name="step-1"></a><span data-ttu-id="6613d-154">Step 1</span><span class="sxs-lookup"><span data-stu-id="6613d-154">Step 1</span></span>

<span data-ttu-id="6613d-155">Click **Listeners** on the existing application gateway and click **Multi-site** to add the first listener.</span><span class="sxs-lookup"><span data-stu-id="6613d-155">Click **Listeners** on the existing application gateway and click **Multi-site** to add the first listener.</span></span>

![listeners overview blade][1]

### <a name="step-2"></a><span data-ttu-id="6613d-157">Step 2</span><span class="sxs-lookup"><span data-stu-id="6613d-157">Step 2</span></span>

<span data-ttu-id="6613d-158">Fill out the information for the listener.</span><span class="sxs-lookup"><span data-stu-id="6613d-158">Fill out the information for the listener.</span></span> <span data-ttu-id="6613d-159">In this example SSL termination is configured, create a new frontend port.</span><span class="sxs-lookup"><span data-stu-id="6613d-159">In this example SSL termination is configured, create a new frontend port.</span></span> <span data-ttu-id="6613d-160">Upload the .pfx certificate to be used for SSL termination.</span><span class="sxs-lookup"><span data-stu-id="6613d-160">Upload the .pfx certificate to be used for SSL termination.</span></span> <span data-ttu-id="6613d-161">The only difference on this blade compared to the standard basic listener blade is the hostname.</span><span class="sxs-lookup"><span data-stu-id="6613d-161">The only difference on this blade compared to the standard basic listener blade is the hostname.</span></span>

![listener properties blade][2]

### <a name="step-3"></a><span data-ttu-id="6613d-163">Step 3</span><span class="sxs-lookup"><span data-stu-id="6613d-163">Step 3</span></span>

<span data-ttu-id="6613d-164">Click **Multi-site** and create another listener as described in the previous step for the second site.</span><span class="sxs-lookup"><span data-stu-id="6613d-164">Click **Multi-site** and create another listener as described in the previous step for the second site.</span></span> <span data-ttu-id="6613d-165">Make sure to use a different certificate for the second listener.</span><span class="sxs-lookup"><span data-stu-id="6613d-165">Make sure to use a different certificate for the second listener.</span></span> <span data-ttu-id="6613d-166">The only difference on this blade compared to the standard basic listener blade is the hostname.</span><span class="sxs-lookup"><span data-stu-id="6613d-166">The only difference on this blade compared to the standard basic listener blade is the hostname.</span></span> <span data-ttu-id="6613d-167">Fill out the information for the listener and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="6613d-167">Fill out the information for the listener and click **OK**.</span></span>

![listener properties blade][3]

> [!NOTE]
> Creation of listeners in the Azure portal for application gateway is a long running task, it may take some time to create the two listeners in this scenario. When complete the listeners show in the portal as seen in the following image:

![listener overview][4]

## <a name="create-rules-to-map-listeners-to-backend-pools"></a><span data-ttu-id="6613d-172">Create rules to map listeners to backend pools</span><span class="sxs-lookup"><span data-stu-id="6613d-172">Create rules to map listeners to backend pools</span></span>

### <a name="step-1"></a><span data-ttu-id="6613d-173">Step 1</span><span class="sxs-lookup"><span data-stu-id="6613d-173">Step 1</span></span>

<span data-ttu-id="6613d-174">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6613d-174">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="6613d-175">Select **Rules** and choose the existing default rule **rule1** and click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="6613d-175">Select **Rules** and choose the existing default rule **rule1** and click **Edit**.</span></span>

### <a name="step-2"></a><span data-ttu-id="6613d-176">Step 2</span><span class="sxs-lookup"><span data-stu-id="6613d-176">Step 2</span></span>

<span data-ttu-id="6613d-177">Fill out the rules blade as seen in the following image.</span><span class="sxs-lookup"><span data-stu-id="6613d-177">Fill out the rules blade as seen in the following image.</span></span> <span data-ttu-id="6613d-178">Choosing the first listener and first pool and clicking **Save** when complete.</span><span class="sxs-lookup"><span data-stu-id="6613d-178">Choosing the first listener and first pool and clicking **Save** when complete.</span></span>

![edit existing rule][6]

### <a name="step-3"></a><span data-ttu-id="6613d-180">Step 3</span><span class="sxs-lookup"><span data-stu-id="6613d-180">Step 3</span></span>

<span data-ttu-id="6613d-181">Click **Basic rule** to create the second rule.</span><span class="sxs-lookup"><span data-stu-id="6613d-181">Click **Basic rule** to create the second rule.</span></span> <span data-ttu-id="6613d-182">Fill out the form with the second listener and second backend pool and click **OK** to save.</span><span class="sxs-lookup"><span data-stu-id="6613d-182">Fill out the form with the second listener and second backend pool and click **OK** to save.</span></span>

![add basic rule blade][10]

<span data-ttu-id="6613d-184">This scenario completes configuring an existing application gateway with multi-site support through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6613d-184">This scenario completes configuring an existing application gateway with multi-site support through the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6613d-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="6613d-185">Next steps</span></span>

<span data-ttu-id="6613d-186">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="6613d-186">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-multisite-portal/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-multisite-portal/figure2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-multisite-portal/figure3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-multisite-portal/figure4.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-multisite-portal/figure5.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-multisite-portal/figure6.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-multisite-portal/figure7.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-multisite-portal/figure8.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-multisite-portal/figure9.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-multisite-portal/figure10.png
[multisite]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-multisite-portal/multisite.png











