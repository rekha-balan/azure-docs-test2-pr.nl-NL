---
title: Create or update an Azure Application Gateway with web application firewall | Microsoft Docs
description: Learn how to create an Application Gateway with web application firewall by using the portal
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b561a210-ed99-4ab4-be06-b49215e3255a
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: c7c13d7817a348f540f024ba7af5b52af1f869b9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553635"
---
# <a name="create-an-application-gateway-with-web-application-firewall-by-using-the-portal"></a><span data-ttu-id="9193f-103">Create an application gateway with web application firewall by using the portal</span><span class="sxs-lookup"><span data-stu-id="9193f-103">Create an application gateway with web application firewall by using the portal</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-web-application-firewall-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-web-application-firewall-powershell.md)

<span data-ttu-id="9193f-106">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span><span class="sxs-lookup"><span data-stu-id="9193f-106">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span> <span data-ttu-id="9193f-107">Web application protects against many of the OWASP top 10 common web vulnerabilities.</span><span class="sxs-lookup"><span data-stu-id="9193f-107">Web application protects against many of the OWASP top 10 common web vulnerabilities.</span></span>

<span data-ttu-id="9193f-108">Azure Application Gateway is a layer-7 load balancer.</span><span class="sxs-lookup"><span data-stu-id="9193f-108">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="9193f-109">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span><span class="sxs-lookup"><span data-stu-id="9193f-109">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span>
<span data-ttu-id="9193f-110">Application provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span><span class="sxs-lookup"><span data-stu-id="9193f-110">Application provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span>
<span data-ttu-id="9193f-111">To find a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="9193f-111">To find a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span></span>

## <a name="scenarios"></a><span data-ttu-id="9193f-112">Scenarios</span><span class="sxs-lookup"><span data-stu-id="9193f-112">Scenarios</span></span>

<span data-ttu-id="9193f-113">In this article there are two scenarios:</span><span class="sxs-lookup"><span data-stu-id="9193f-113">In this article there are two scenarios:</span></span>

<span data-ttu-id="9193f-114">In the first scenario, you learn to [add web application firewall to an existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway).</span><span class="sxs-lookup"><span data-stu-id="9193f-114">In the first scenario, you learn to [add web application firewall to an existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway).</span></span>

<span data-ttu-id="9193f-115">In the second scenario, you learn to [create an application gateway with web application firewall](#create-an-application-gateway-with-web-application-firewall)</span><span class="sxs-lookup"><span data-stu-id="9193f-115">In the second scenario, you learn to [create an application gateway with web application firewall](#create-an-application-gateway-with-web-application-firewall)</span></span>

![Scenario example][scenario]

> [!NOTE]
> Additional configuration of the application gateway, including custom health probes, backend pool addresses, and additional rules are configured after the application gateway is configured and not during initial deployment.

## <a name="before-you-begin"></a><span data-ttu-id="9193f-118">Before you begin</span><span class="sxs-lookup"><span data-stu-id="9193f-118">Before you begin</span></span>

<span data-ttu-id="9193f-119">Azure Application Gateway requires its own subnet.</span><span class="sxs-lookup"><span data-stu-id="9193f-119">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="9193f-120">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span><span class="sxs-lookup"><span data-stu-id="9193f-120">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="9193f-121">Once you deploy an application gateway to a subnet, only additional application gateways are able to be added to the subnet.</span><span class="sxs-lookup"><span data-stu-id="9193f-121">Once you deploy an application gateway to a subnet, only additional application gateways are able to be added to the subnet.</span></span>

##<a name="add-web-application-firewall-to-an-existing-application-gateway"></a> <span data-ttu-id="9193f-122">Add web application firewall to an existing application gateway</span><span class="sxs-lookup"><span data-stu-id="9193f-122">Add web application firewall to an existing application gateway</span></span>

<span data-ttu-id="9193f-123">This scenario updates an existing application gateway to support web application firewall in prevention mode.</span><span class="sxs-lookup"><span data-stu-id="9193f-123">This scenario updates an existing application gateway to support web application firewall in prevention mode.</span></span>

### <a name="step-1"></a><span data-ttu-id="9193f-124">Step 1</span><span class="sxs-lookup"><span data-stu-id="9193f-124">Step 1</span></span>

<span data-ttu-id="9193f-125">Navigate to the Azure portal, select an existing Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="9193f-125">Navigate to the Azure portal, select an existing Application Gateway.</span></span>

![Creating Application Gateway][1]

### <a name="step-2"></a><span data-ttu-id="9193f-127">Step 2</span><span class="sxs-lookup"><span data-stu-id="9193f-127">Step 2</span></span>

<span data-ttu-id="9193f-128">Click **Web application firewall** and update the application gateway settings.</span><span class="sxs-lookup"><span data-stu-id="9193f-128">Click **Web application firewall** and update the application gateway settings.</span></span> <span data-ttu-id="9193f-129">When complete click **Save**</span><span class="sxs-lookup"><span data-stu-id="9193f-129">When complete click **Save**</span></span>

<span data-ttu-id="9193f-130">The settings to update an existing application gateway to support web application firewall are:</span><span class="sxs-lookup"><span data-stu-id="9193f-130">The settings to update an existing application gateway to support web application firewall are:</span></span>

* <span data-ttu-id="9193f-131">**Upgrade to WAF Tier** - This setting is required to configure WAF.</span><span class="sxs-lookup"><span data-stu-id="9193f-131">**Upgrade to WAF Tier** - This setting is required to configure WAF.</span></span>
* <span data-ttu-id="9193f-132">**Firewall status** - This setting either disables or enables web application firewall.</span><span class="sxs-lookup"><span data-stu-id="9193f-132">**Firewall status** - This setting either disables or enables web application firewall.</span></span>
* <span data-ttu-id="9193f-133">**Firewall mode** - This setting is how web application firewall deals with malicious traffic.</span><span class="sxs-lookup"><span data-stu-id="9193f-133">**Firewall mode** - This setting is how web application firewall deals with malicious traffic.</span></span> <span data-ttu-id="9193f-134">**Detection** mode only logs the events, where **Prevention** mode logs the events and stops the malicious traffic.</span><span class="sxs-lookup"><span data-stu-id="9193f-134">**Detection** mode only logs the events, where **Prevention** mode logs the events and stops the malicious traffic.</span></span>
* <span data-ttu-id="9193f-135">**Rule set** - This setting determines the [core rule set](application-gateway-web-application-firewall-overview.md#core-rule-sets) that is used to protect the backend pool members.</span><span class="sxs-lookup"><span data-stu-id="9193f-135">**Rule set** - This setting determines the [core rule set](application-gateway-web-application-firewall-overview.md#core-rule-sets) that is used to protect the backend pool members.</span></span>
* <span data-ttu-id="9193f-136">**Configure disabled rules** - To prevent possible false positives, this setting allows you to disable certain [rules and rule groups](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="9193f-136">**Configure disabled rules** - To prevent possible false positives, this setting allows you to disable certain [rules and rule groups](application-gateway-crs-rulegroups-rules.md).</span></span>

>[!NOTE]
> When upgrading an existing application gateway to the WAF SKU, the SKU size changes to **medium**. This can be reconfigured after configuration is complete.

![blade showing basic settings][2]

> [!NOTE]
> To view web application firewall logs, diagnostics must be enabled and ApplicationGatewayFirewallLog selected. An instance count of 1 can be chosen for testing purposes. It is important to know that any instance count under two instances is not covered by the SLA and are therefore not recommended. Small gateways are not available when using web application firewall.

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="9193f-144">Create an application gateway with web application firewall</span><span class="sxs-lookup"><span data-stu-id="9193f-144">Create an application gateway with web application firewall</span></span>

<span data-ttu-id="9193f-145">This scenario will:</span><span class="sxs-lookup"><span data-stu-id="9193f-145">This scenario will:</span></span>

* <span data-ttu-id="9193f-146">Create a medium web application firewall application gateway with two instances.</span><span class="sxs-lookup"><span data-stu-id="9193f-146">Create a medium web application firewall application gateway with two instances.</span></span>
* <span data-ttu-id="9193f-147">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="9193f-147">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="9193f-148">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span><span class="sxs-lookup"><span data-stu-id="9193f-148">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="9193f-149">Configure a certificate for SSL offload.</span><span class="sxs-lookup"><span data-stu-id="9193f-149">Configure a certificate for SSL offload.</span></span>

### <a name="step-1"></a><span data-ttu-id="9193f-150">Step 1</span><span class="sxs-lookup"><span data-stu-id="9193f-150">Step 1</span></span>

<span data-ttu-id="9193f-151">Navigate to the Azure portal, click **New** > **Networking** > **Application Gateway**</span><span class="sxs-lookup"><span data-stu-id="9193f-151">Navigate to the Azure portal, click **New** > **Networking** > **Application Gateway**</span></span>

![Creating Application Gateway][1-1]

### <a name="step-2"></a><span data-ttu-id="9193f-153">Step 2</span><span class="sxs-lookup"><span data-stu-id="9193f-153">Step 2</span></span>

<span data-ttu-id="9193f-154">Next fill out the basic information about the application gateway.</span><span class="sxs-lookup"><span data-stu-id="9193f-154">Next fill out the basic information about the application gateway.</span></span> <span data-ttu-id="9193f-155">Be sure to choose **WAF** as the tier.</span><span class="sxs-lookup"><span data-stu-id="9193f-155">Be sure to choose **WAF** as the tier.</span></span> <span data-ttu-id="9193f-156">When complete click **OK**</span><span class="sxs-lookup"><span data-stu-id="9193f-156">When complete click **OK**</span></span>

<span data-ttu-id="9193f-157">The information needed for the basic settings is:</span><span class="sxs-lookup"><span data-stu-id="9193f-157">The information needed for the basic settings is:</span></span>

* <span data-ttu-id="9193f-158">**Name** - The name for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="9193f-158">**Name** - The name for the application gateway.</span></span>
* <span data-ttu-id="9193f-159">**Tier** - The tier of the application gateway, available options are ( **Standard** and **WAF** ).</span><span class="sxs-lookup"><span data-stu-id="9193f-159">**Tier** - The tier of the application gateway, available options are ( **Standard** and **WAF** ).</span></span> <span data-ttu-id="9193f-160">Web application firewall is only available in the WAF Tier.</span><span class="sxs-lookup"><span data-stu-id="9193f-160">Web application firewall is only available in the WAF Tier.</span></span>
* <span data-ttu-id="9193f-161">**SKU size** - This setting is the size of the application gateway, available options are ( **Medium** and **Large** ).</span><span class="sxs-lookup"><span data-stu-id="9193f-161">**SKU size** - This setting is the size of the application gateway, available options are ( **Medium** and **Large** ).</span></span>
* <span data-ttu-id="9193f-162">**Instance count** - The number of instances, this value should be a number between **2** and **10**.</span><span class="sxs-lookup"><span data-stu-id="9193f-162">**Instance count** - The number of instances, this value should be a number between **2** and **10**.</span></span>
* <span data-ttu-id="9193f-163">**Resource group** - The resource group to hold the application gateway, it can be an existing resource group or a new one.</span><span class="sxs-lookup"><span data-stu-id="9193f-163">**Resource group** - The resource group to hold the application gateway, it can be an existing resource group or a new one.</span></span>
* <span data-ttu-id="9193f-164">**Location** - The region for the application gateway, it is the same location at the resource group.</span><span class="sxs-lookup"><span data-stu-id="9193f-164">**Location** - The region for the application gateway, it is the same location at the resource group.</span></span> <span data-ttu-id="9193f-165">*The location is important as the virtual network and public IP must be in the same location as the gateway*.</span><span class="sxs-lookup"><span data-stu-id="9193f-165">*The location is important as the virtual network and public IP must be in the same location as the gateway*.</span></span>

![blade showing basic settings][2-2]

> [!NOTE]
> An instance count of 1 can be chosen for testing purposes. It is important to know that any instance count under two instances is not covered by the SLA and are therefore not recommended. Small gateways are not supported for web application firewall scenarios.

### <a name="step-3"></a><span data-ttu-id="9193f-170">Step 3</span><span class="sxs-lookup"><span data-stu-id="9193f-170">Step 3</span></span>

<span data-ttu-id="9193f-171">Once the basic settings are defined, the next step is to define the virtual network to be used.</span><span class="sxs-lookup"><span data-stu-id="9193f-171">Once the basic settings are defined, the next step is to define the virtual network to be used.</span></span> <span data-ttu-id="9193f-172">The virtual network houses the application that the application gateway does load balancing for.</span><span class="sxs-lookup"><span data-stu-id="9193f-172">The virtual network houses the application that the application gateway does load balancing for.</span></span>

<span data-ttu-id="9193f-173">Click **Choose a virtual network** to configure the virtual network.</span><span class="sxs-lookup"><span data-stu-id="9193f-173">Click **Choose a virtual network** to configure the virtual network.</span></span>

![blade showing settings for application gateway][3]

### <a name="step-4"></a><span data-ttu-id="9193f-175">Step 4</span><span class="sxs-lookup"><span data-stu-id="9193f-175">Step 4</span></span>

<span data-ttu-id="9193f-176">In the **Choose Virtual Network** blade, click **Create New**</span><span class="sxs-lookup"><span data-stu-id="9193f-176">In the **Choose Virtual Network** blade, click **Create New**</span></span>

<span data-ttu-id="9193f-177">While not explained in this scenario, an existing Virtual Network could be selected at this point.</span><span class="sxs-lookup"><span data-stu-id="9193f-177">While not explained in this scenario, an existing Virtual Network could be selected at this point.</span></span>  <span data-ttu-id="9193f-178">If an existing virtual network is used, it is important to know that the virtual network needs an empty subnet or a subnet of only application gateway resources to be used.</span><span class="sxs-lookup"><span data-stu-id="9193f-178">If an existing virtual network is used, it is important to know that the virtual network needs an empty subnet or a subnet of only application gateway resources to be used.</span></span>

![choose virtual network blade][4]

### <a name="step-5"></a><span data-ttu-id="9193f-180">Step 5</span><span class="sxs-lookup"><span data-stu-id="9193f-180">Step 5</span></span>

<span data-ttu-id="9193f-181">Fill out the network information in the **Create Virtual Network** blade as described in the preceding [Scenario](#scenario) description.</span><span class="sxs-lookup"><span data-stu-id="9193f-181">Fill out the network information in the **Create Virtual Network** blade as described in the preceding [Scenario](#scenario) description.</span></span>

![Create virtual network blade with information entered][5]

### <a name="step-6"></a><span data-ttu-id="9193f-183">Step 6</span><span class="sxs-lookup"><span data-stu-id="9193f-183">Step 6</span></span>

<span data-ttu-id="9193f-184">Once the virtual network is created, the next step is to define the front-end IP for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="9193f-184">Once the virtual network is created, the next step is to define the front-end IP for the application gateway.</span></span> <span data-ttu-id="9193f-185">At this point, the choice is between a public or a private IP address for the front-end.</span><span class="sxs-lookup"><span data-stu-id="9193f-185">At this point, the choice is between a public or a private IP address for the front-end.</span></span> <span data-ttu-id="9193f-186">The choice depends on whether the application is internet facing or internal only.</span><span class="sxs-lookup"><span data-stu-id="9193f-186">The choice depends on whether the application is internet facing or internal only.</span></span> <span data-ttu-id="9193f-187">This scenario assumes using a public IP address.</span><span class="sxs-lookup"><span data-stu-id="9193f-187">This scenario assumes using a public IP address.</span></span> <span data-ttu-id="9193f-188">To choose a private IP address, the **Private** button can be clicked.</span><span class="sxs-lookup"><span data-stu-id="9193f-188">To choose a private IP address, the **Private** button can be clicked.</span></span> <span data-ttu-id="9193f-189">An automatically assigned IP address is chosen or you can click the **Choose a specific private IP address** checkbox to enter one manually.</span><span class="sxs-lookup"><span data-stu-id="9193f-189">An automatically assigned IP address is chosen or you can click the **Choose a specific private IP address** checkbox to enter one manually.</span></span>

<span data-ttu-id="9193f-190">Click **Choose a public IP address**.</span><span class="sxs-lookup"><span data-stu-id="9193f-190">Click **Choose a public IP address**.</span></span> <span data-ttu-id="9193f-191">If an existing public IP address is available it can be chosen at this point, in this scenario you create a new public IP address.</span><span class="sxs-lookup"><span data-stu-id="9193f-191">If an existing public IP address is available it can be chosen at this point, in this scenario you create a new public IP address.</span></span> <span data-ttu-id="9193f-192">Click **Create new**</span><span class="sxs-lookup"><span data-stu-id="9193f-192">Click **Create new**</span></span>

![Choose public IP address blade][6]

### <a name="step-7"></a><span data-ttu-id="9193f-194">Step 7</span><span class="sxs-lookup"><span data-stu-id="9193f-194">Step 7</span></span>

<span data-ttu-id="9193f-195">Next give the public IP address a friendly name and click **OK**</span><span class="sxs-lookup"><span data-stu-id="9193f-195">Next give the public IP address a friendly name and click **OK**</span></span>

![Create public IP Address blade][7]

### <a name="step-8"></a><span data-ttu-id="9193f-197">Step 8</span><span class="sxs-lookup"><span data-stu-id="9193f-197">Step 8</span></span>

<span data-ttu-id="9193f-198">Next, you setup the listener configuration.</span><span class="sxs-lookup"><span data-stu-id="9193f-198">Next, you setup the listener configuration.</span></span>  <span data-ttu-id="9193f-199">If **http** is used, nothing is left to configure and **OK** can be clicked.</span><span class="sxs-lookup"><span data-stu-id="9193f-199">If **http** is used, nothing is left to configure and **OK** can be clicked.</span></span> <span data-ttu-id="9193f-200">To use **https** further configuration is required.</span><span class="sxs-lookup"><span data-stu-id="9193f-200">To use **https** further configuration is required.</span></span>

<span data-ttu-id="9193f-201">To use **https**, a certificate is required.</span><span class="sxs-lookup"><span data-stu-id="9193f-201">To use **https**, a certificate is required.</span></span> <span data-ttu-id="9193f-202">The private key of the certificate is needed so a .pfx export of the certificate needs to be provided and the password for the file.</span><span class="sxs-lookup"><span data-stu-id="9193f-202">The private key of the certificate is needed so a .pfx export of the certificate needs to be provided and the password for the file.</span></span>

<span data-ttu-id="9193f-203">Click **HTTPS**, click the **folder** icon next to the **Upload PFX certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="9193f-203">Click **HTTPS**, click the **folder** icon next to the **Upload PFX certificate** textbox.</span></span>
<span data-ttu-id="9193f-204">Navigate to the .pfx certificate file on your file system.</span><span class="sxs-lookup"><span data-stu-id="9193f-204">Navigate to the .pfx certificate file on your file system.</span></span> <span data-ttu-id="9193f-205">Once it is selected, give the certificate a friendly name and type the password for the .pfx file.</span><span class="sxs-lookup"><span data-stu-id="9193f-205">Once it is selected, give the certificate a friendly name and type the password for the .pfx file.</span></span>

<span data-ttu-id="9193f-206">Once complete click **OK** to review the settings for the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="9193f-206">Once complete click **OK** to review the settings for the Application Gateway.</span></span>

![Listener Configuration section on Settings blade][8]

### <a name="step-9"></a><span data-ttu-id="9193f-208">Step 9</span><span class="sxs-lookup"><span data-stu-id="9193f-208">Step 9</span></span>

<span data-ttu-id="9193f-209">Configure the **WAF** specific settings.</span><span class="sxs-lookup"><span data-stu-id="9193f-209">Configure the **WAF** specific settings.</span></span>

* <span data-ttu-id="9193f-210">**Firewall status** - This setting turns WAF on or off.</span><span class="sxs-lookup"><span data-stu-id="9193f-210">**Firewall status** - This setting turns WAF on or off.</span></span>
* <span data-ttu-id="9193f-211">**Firewall mode** - This setting determines the actions WAF takes on malicious traffic.</span><span class="sxs-lookup"><span data-stu-id="9193f-211">**Firewall mode** - This setting determines the actions WAF takes on malicious traffic.</span></span> <span data-ttu-id="9193f-212">If **Detection** is chosen, traffic is only logged.</span><span class="sxs-lookup"><span data-stu-id="9193f-212">If **Detection** is chosen, traffic is only logged.</span></span>  <span data-ttu-id="9193f-213">If **Prevention** is chosen, traffic is logged and stopped with a 403 Unauthorized response.</span><span class="sxs-lookup"><span data-stu-id="9193f-213">If **Prevention** is chosen, traffic is logged and stopped with a 403 Unauthorized response.</span></span>

![web application firewall settings][9]

### <a name="step-10"></a><span data-ttu-id="9193f-215">Step 10</span><span class="sxs-lookup"><span data-stu-id="9193f-215">Step 10</span></span>

<span data-ttu-id="9193f-216">Review the Summary page and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="9193f-216">Review the Summary page and click **OK**.</span></span>  <span data-ttu-id="9193f-217">Now the application gateway is queued up and created.</span><span class="sxs-lookup"><span data-stu-id="9193f-217">Now the application gateway is queued up and created.</span></span>

### <a name="step-11"></a><span data-ttu-id="9193f-218">Step 11</span><span class="sxs-lookup"><span data-stu-id="9193f-218">Step 11</span></span>

<span data-ttu-id="9193f-219">Once the application gateway has been created, navigate to it in the portal to continue configuration of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="9193f-219">Once the application gateway has been created, navigate to it in the portal to continue configuration of the application gateway.</span></span>

![Application Gateway resource view][10]

<span data-ttu-id="9193f-221">These steps create a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span><span class="sxs-lookup"><span data-stu-id="9193f-221">These steps create a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="9193f-222">You can modify these settings to suit your deployment once the provisioning is successful</span><span class="sxs-lookup"><span data-stu-id="9193f-222">You can modify these settings to suit your deployment once the provisioning is successful</span></span>

> [!NOTE]
> Application gateways created with the basic web application firewall configuration are configured with CRS 3.0 for protections.

## <a name="next-steps"></a><span data-ttu-id="9193f-224">Next steps</span><span class="sxs-lookup"><span data-stu-id="9193f-224">Next steps</span></span>

<span data-ttu-id="9193f-225">Learn how to configure diagnostic logging, to log the events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="9193f-225">Learn how to configure diagnostic logging, to log the events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="9193f-226">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9193f-226">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="9193f-227">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9193f-227">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-web-application-firewall-portal/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-web-application-firewall-portal/figure2.png
[1-1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-web-application-firewall-portal/figure1-1.png
[2-2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-web-application-firewall-portal/figure2-2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-web-application-firewall-portal/figure3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-web-application-firewall-portal/figure4.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-web-application-firewall-portal/figure5.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-web-application-firewall-portal/figure6.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-web-application-firewall-portal/figure7.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-web-application-firewall-portal/figure8.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-web-application-firewall-portal/figure9.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-web-application-firewall-portal/figure10.png
[scenario]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-web-application-firewall-portal/scenario.png













