---
title: Azure App Service Hybrid Connections | Microsoft Docs
description: How to create and use Hybrid Connections to access resources in disparate networks
services: app-service
documentationcenter: ''
author: ccompy
manager: stefsch
editor: ''
ms.assetid: 66774bde-13f5-45d0-9a70-4e9536a4f619
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2018
ms.author: ccompy
ms.openlocfilehash: 69897e288a90a731d95db82d0ff978d776c12580
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865791"
---
# <a name="azure-app-service-hybrid-connections"></a><span data-ttu-id="b4cd8-103">Azure App Service Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="b4cd8-103">Azure App Service Hybrid Connections</span></span> #

<span data-ttu-id="b4cd8-104">Hybrid Connections is both a service in Azure and a feature in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-104">Hybrid Connections is both a service in Azure and a feature in Azure App Service.</span></span> <span data-ttu-id="b4cd8-105">As a service, it has uses and capabilities beyond those that are used in App Service.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-105">As a service, it has uses and capabilities beyond those that are used in App Service.</span></span> <span data-ttu-id="b4cd8-106">To learn more about Hybrid Connections and their usage outside App Service, see [Azure Relay Hybrid Connections][HCService].</span><span class="sxs-lookup"><span data-stu-id="b4cd8-106">To learn more about Hybrid Connections and their usage outside App Service, see [Azure Relay Hybrid Connections][HCService].</span></span>

<span data-ttu-id="b4cd8-107">Within App Service, Hybrid Connections can be used to access application resources in other networks.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-107">Within App Service, Hybrid Connections can be used to access application resources in other networks.</span></span> <span data-ttu-id="b4cd8-108">It provides access from your app to an application endpoint.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-108">It provides access from your app to an application endpoint.</span></span> <span data-ttu-id="b4cd8-109">It does not enable an alternate capability to access your application.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-109">It does not enable an alternate capability to access your application.</span></span> <span data-ttu-id="b4cd8-110">As used in App Service, each Hybrid Connection correlates to a single TCP host and port combination.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-110">As used in App Service, each Hybrid Connection correlates to a single TCP host and port combination.</span></span> <span data-ttu-id="b4cd8-111">This means that the Hybrid Connection endpoint can be on any operating system and any application, provided you are accessing a TCP listening port.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-111">This means that the Hybrid Connection endpoint can be on any operating system and any application, provided you are accessing a TCP listening port.</span></span> <span data-ttu-id="b4cd8-112">The Hybrid Connections feature does not know or care what the application protocol is, or what you are accessing.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-112">The Hybrid Connections feature does not know or care what the application protocol is, or what you are accessing.</span></span> <span data-ttu-id="b4cd8-113">It is simply providing network access.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-113">It is simply providing network access.</span></span>  


## <a name="how-it-works"></a><span data-ttu-id="b4cd8-114">How it works</span><span class="sxs-lookup"><span data-stu-id="b4cd8-114">How it works</span></span> ##
<span data-ttu-id="b4cd8-115">The Hybrid Connections feature consists of two outbound calls to Azure Service Bus Relay.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-115">The Hybrid Connections feature consists of two outbound calls to Azure Service Bus Relay.</span></span> <span data-ttu-id="b4cd8-116">There is a connection from a library on the host where your app is running in App Service.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-116">There is a connection from a library on the host where your app is running in App Service.</span></span> <span data-ttu-id="b4cd8-117">There is also a connection from the Hybrid Connection Manager (HCM) to Service Bus Relay.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-117">There is also a connection from the Hybrid Connection Manager (HCM) to Service Bus Relay.</span></span> <span data-ttu-id="b4cd8-118">The HCM is a relay service that you deploy within the network hosting the resource you are trying to access.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-118">The HCM is a relay service that you deploy within the network hosting the resource you are trying to access.</span></span> 

<span data-ttu-id="b4cd8-119">Through the two joined connections, your app has a TCP tunnel to a fixed host:port combination on the other side of the HCM.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-119">Through the two joined connections, your app has a TCP tunnel to a fixed host:port combination on the other side of the HCM.</span></span> <span data-ttu-id="b4cd8-120">The connection uses TLS 1.2 for security and shared access signature (SAS) keys for authentication and authorization.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-120">The connection uses TLS 1.2 for security and shared access signature (SAS) keys for authentication and authorization.</span></span>    

![Diagram of Hybrid Connection high-level flow][1]

<span data-ttu-id="b4cd8-122">When your app makes a DNS request that matches a configured Hybrid Connection endpoint, the outbound TCP traffic will be redirected through the Hybrid Connection.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-122">When your app makes a DNS request that matches a configured Hybrid Connection endpoint, the outbound TCP traffic will be redirected through the Hybrid Connection.</span></span>  

> [!NOTE]
> <span data-ttu-id="b4cd8-123">This means that you should try to always use a DNS name for your Hybrid Connection.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-123">This means that you should try to always use a DNS name for your Hybrid Connection.</span></span> <span data-ttu-id="b4cd8-124">Some client software does not do a DNS lookup if the endpoint uses an IP address instead.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-124">Some client software does not do a DNS lookup if the endpoint uses an IP address instead.</span></span>
>


### <a name="app-service-hybrid-connection-benefits"></a><span data-ttu-id="b4cd8-125">App Service Hybrid Connection benefits</span><span class="sxs-lookup"><span data-stu-id="b4cd8-125">App Service Hybrid Connection benefits</span></span> ###

<span data-ttu-id="b4cd8-126">There are a number of benefits to the Hybrid Connections capability, including:</span><span class="sxs-lookup"><span data-stu-id="b4cd8-126">There are a number of benefits to the Hybrid Connections capability, including:</span></span>

- <span data-ttu-id="b4cd8-127">Apps can access on-premises systems and services securely.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-127">Apps can access on-premises systems and services securely.</span></span>
- <span data-ttu-id="b4cd8-128">The feature does not require an internet-accessible endpoint.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-128">The feature does not require an internet-accessible endpoint.</span></span>
- <span data-ttu-id="b4cd8-129">It is quick and easy to set up.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-129">It is quick and easy to set up.</span></span> 
- <span data-ttu-id="b4cd8-130">Each Hybrid Connection matches to a single host:port combination, helpful for security.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-130">Each Hybrid Connection matches to a single host:port combination, helpful for security.</span></span>
- <span data-ttu-id="b4cd8-131">It normally does not require firewall holes.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-131">It normally does not require firewall holes.</span></span> <span data-ttu-id="b4cd8-132">The connections are all outbound over standard web ports.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-132">The connections are all outbound over standard web ports.</span></span>
- <span data-ttu-id="b4cd8-133">Because the feature is network level, it is agnostic to the language used by your app and the technology used by the endpoint.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-133">Because the feature is network level, it is agnostic to the language used by your app and the technology used by the endpoint.</span></span>
- <span data-ttu-id="b4cd8-134">It can be used to provide access in multiple networks from a single app.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-134">It can be used to provide access in multiple networks from a single app.</span></span> 

### <a name="things-you-cannot-do-with-hybrid-connections"></a><span data-ttu-id="b4cd8-135">Things you cannot do with Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="b4cd8-135">Things you cannot do with Hybrid Connections</span></span> ###

<span data-ttu-id="b4cd8-136">Things you cannot do with Hybrid Connections include:</span><span class="sxs-lookup"><span data-stu-id="b4cd8-136">Things you cannot do with Hybrid Connections include:</span></span>

- <span data-ttu-id="b4cd8-137">Mount a drive.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-137">Mount a drive.</span></span>
- <span data-ttu-id="b4cd8-138">Use UDP.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-138">Use UDP.</span></span>
- <span data-ttu-id="b4cd8-139">Access TCP-based services that use dynamic ports, such as FTP Passive Mode or Extended Passive Mode.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-139">Access TCP-based services that use dynamic ports, such as FTP Passive Mode or Extended Passive Mode.</span></span>
- <span data-ttu-id="b4cd8-140">Support LDAP, because it can require UDP.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-140">Support LDAP, because it can require UDP.</span></span>
- <span data-ttu-id="b4cd8-141">Support Active Directory, because you cannot domain join an App Service worker.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-141">Support Active Directory, because you cannot domain join an App Service worker.</span></span>

## <a name="add-and-create-hybrid-connections-in-your-app"></a><span data-ttu-id="b4cd8-142">Add and Create Hybrid Connections in your app</span><span class="sxs-lookup"><span data-stu-id="b4cd8-142">Add and Create Hybrid Connections in your app</span></span> ##

<span data-ttu-id="b4cd8-143">To create a Hybrid Connection, go to the [Azure portal][portal] and select your app.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-143">To create a Hybrid Connection, go to the [Azure portal][portal] and select your app.</span></span> <span data-ttu-id="b4cd8-144">Select **Networking** > **Configure your Hybrid Connection endpoints**.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-144">Select **Networking** > **Configure your Hybrid Connection endpoints**.</span></span> <span data-ttu-id="b4cd8-145">Here you can see the Hybrid Connections that are configured for your app.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-145">Here you can see the Hybrid Connections that are configured for your app.</span></span>  

![Screenshot of Hybrid Connection list][2]

<span data-ttu-id="b4cd8-147">To add a new Hybrid Connection, select **[+] Add hybrid connection**.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-147">To add a new Hybrid Connection, select **[+] Add hybrid connection**.</span></span>  <span data-ttu-id="b4cd8-148">You'll see a list of the Hybrid Connections that you already created.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-148">You'll see a list of the Hybrid Connections that you already created.</span></span> <span data-ttu-id="b4cd8-149">To add one or more of them to your app, select the ones you want, and then select **Add selected Hybrid Connection**.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-149">To add one or more of them to your app, select the ones you want, and then select **Add selected Hybrid Connection**.</span></span>  

![Screenshot of Hybrid Connection portal][3]

<span data-ttu-id="b4cd8-151">If you want to create a new Hybrid Connection, select **Create new hybrid connection**.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-151">If you want to create a new Hybrid Connection, select **Create new hybrid connection**.</span></span> <span data-ttu-id="b4cd8-152">Specify the:</span><span class="sxs-lookup"><span data-stu-id="b4cd8-152">Specify the:</span></span> 

- <span data-ttu-id="b4cd8-153">Hybrid Connection name.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-153">Hybrid Connection name.</span></span>
- <span data-ttu-id="b4cd8-154">Endpoint hostname.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-154">Endpoint hostname.</span></span>
- <span data-ttu-id="b4cd8-155">Endpoint port.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-155">Endpoint port.</span></span>
- <span data-ttu-id="b4cd8-156">Service Bus namespace you want to use.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-156">Service Bus namespace you want to use.</span></span>

![Screenshot of Create new hybrid connection dialog box][4]

<span data-ttu-id="b4cd8-158">Every Hybrid Connection is tied to a Service Bus namespace, and each Service Bus namespace is in an Azure region.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-158">Every Hybrid Connection is tied to a Service Bus namespace, and each Service Bus namespace is in an Azure region.</span></span> <span data-ttu-id="b4cd8-159">It's important to try to use a Service Bus namespace in the same region as your app, to avoid network induced latency.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-159">It's important to try to use a Service Bus namespace in the same region as your app, to avoid network induced latency.</span></span>

<span data-ttu-id="b4cd8-160">If you want to remove your Hybrid Connection from your app, right-click it and select **Disconnect**.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-160">If you want to remove your Hybrid Connection from your app, right-click it and select **Disconnect**.</span></span>  

<span data-ttu-id="b4cd8-161">When a Hybrid Connection is added to your app, you can see details on it simply by selecting it.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-161">When a Hybrid Connection is added to your app, you can see details on it simply by selecting it.</span></span> 

![Screenshot of Hybrid connections details][5]

### <a name="create-a-hybrid-connection-in-the-azure-relay-portal"></a><span data-ttu-id="b4cd8-163">Create a Hybrid Connection in the Azure Relay portal</span><span class="sxs-lookup"><span data-stu-id="b4cd8-163">Create a Hybrid Connection in the Azure Relay portal</span></span> ###

<span data-ttu-id="b4cd8-164">In addition to the portal experience from within your app, you can create Hybrid Connections from within the Azure Relay portal.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-164">In addition to the portal experience from within your app, you can create Hybrid Connections from within the Azure Relay portal.</span></span> <span data-ttu-id="b4cd8-165">For a Hybrid Connection to be used by App Service, it must:</span><span class="sxs-lookup"><span data-stu-id="b4cd8-165">For a Hybrid Connection to be used by App Service, it must:</span></span>

* <span data-ttu-id="b4cd8-166">Require client authorization.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-166">Require client authorization.</span></span>
* <span data-ttu-id="b4cd8-167">Have a metadata item, named endpoint, that contains a host:port combination as the value.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-167">Have a metadata item, named endpoint, that contains a host:port combination as the value.</span></span>

## <a name="hybrid-connections-and-app-service-plans"></a><span data-ttu-id="b4cd8-168">Hybrid Connections and App Service plans</span><span class="sxs-lookup"><span data-stu-id="b4cd8-168">Hybrid Connections and App Service plans</span></span> ##

<span data-ttu-id="b4cd8-169">App Service Hybrid Connections are only available in Basic, Standard, Premium, and Isolated pricing SKUs.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-169">App Service Hybrid Connections are only available in Basic, Standard, Premium, and Isolated pricing SKUs.</span></span> <span data-ttu-id="b4cd8-170">There are limits tied to the pricing plan.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-170">There are limits tied to the pricing plan.</span></span>  

| <span data-ttu-id="b4cd8-171">Pricing plan</span><span class="sxs-lookup"><span data-stu-id="b4cd8-171">Pricing plan</span></span> | <span data-ttu-id="b4cd8-172">Number of Hybrid Connections usable in the plan</span><span class="sxs-lookup"><span data-stu-id="b4cd8-172">Number of Hybrid Connections usable in the plan</span></span> |
|----|----|
| <span data-ttu-id="b4cd8-173">Basic</span><span class="sxs-lookup"><span data-stu-id="b4cd8-173">Basic</span></span> | <span data-ttu-id="b4cd8-174">5</span><span class="sxs-lookup"><span data-stu-id="b4cd8-174">5</span></span> |
| <span data-ttu-id="b4cd8-175">Standard</span><span class="sxs-lookup"><span data-stu-id="b4cd8-175">Standard</span></span> | <span data-ttu-id="b4cd8-176">25</span><span class="sxs-lookup"><span data-stu-id="b4cd8-176">25</span></span> |
| <span data-ttu-id="b4cd8-177">Premium</span><span class="sxs-lookup"><span data-stu-id="b4cd8-177">Premium</span></span> | <span data-ttu-id="b4cd8-178">200</span><span class="sxs-lookup"><span data-stu-id="b4cd8-178">200</span></span> |
| <span data-ttu-id="b4cd8-179">Isolated</span><span class="sxs-lookup"><span data-stu-id="b4cd8-179">Isolated</span></span> | <span data-ttu-id="b4cd8-180">200</span><span class="sxs-lookup"><span data-stu-id="b4cd8-180">200</span></span> |

<span data-ttu-id="b4cd8-181">The App Service plan UI shows you how many Hybrid Connections are being used and by what apps.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-181">The App Service plan UI shows you how many Hybrid Connections are being used and by what apps.</span></span>  

![Screenshot of App Service plan properties][6]

<span data-ttu-id="b4cd8-183">Select the Hybrid Connection to see details.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-183">Select the Hybrid Connection to see details.</span></span> <span data-ttu-id="b4cd8-184">You can see all the information that you saw at the app view.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-184">You can see all the information that you saw at the app view.</span></span> <span data-ttu-id="b4cd8-185">You can also see how many other apps in the same plan are using that Hybrid Connection.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-185">You can also see how many other apps in the same plan are using that Hybrid Connection.</span></span>

<span data-ttu-id="b4cd8-186">There is a limit on the number of Hybrid Connection endpoints that can be used in an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-186">There is a limit on the number of Hybrid Connection endpoints that can be used in an App Service plan.</span></span> <span data-ttu-id="b4cd8-187">Each Hybrid Connection used, however, can be used across any number of apps in that plan.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-187">Each Hybrid Connection used, however, can be used across any number of apps in that plan.</span></span> <span data-ttu-id="b4cd8-188">For example, a single Hybrid Connection that is used in five separate apps in an App Service plan counts as one Hybrid Connection.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-188">For example, a single Hybrid Connection that is used in five separate apps in an App Service plan counts as one Hybrid Connection.</span></span>

### <a name="pricing"></a><span data-ttu-id="b4cd8-189">Pricing</span><span class="sxs-lookup"><span data-stu-id="b4cd8-189">Pricing</span></span> ###

<span data-ttu-id="b4cd8-190">In addition to there being an App Service plan SKU requirement, there is an additional cost to using Hybrid Connections.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-190">In addition to there being an App Service plan SKU requirement, there is an additional cost to using Hybrid Connections.</span></span> <span data-ttu-id="b4cd8-191">There is a charge for each listener used by a Hybrid Connection.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-191">There is a charge for each listener used by a Hybrid Connection.</span></span> <span data-ttu-id="b4cd8-192">The listener is the Hybrid Connection Manager.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-192">The listener is the Hybrid Connection Manager.</span></span> <span data-ttu-id="b4cd8-193">If you had five Hybrid Connections supported by two Hybrid Connection Managers, that would be 10 listeners.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-193">If you had five Hybrid Connections supported by two Hybrid Connection Managers, that would be 10 listeners.</span></span> <span data-ttu-id="b4cd8-194">For more information, see [Service Bus pricing][sbpricing].</span><span class="sxs-lookup"><span data-stu-id="b4cd8-194">For more information, see [Service Bus pricing][sbpricing].</span></span>

## <a name="hybrid-connection-manager"></a><span data-ttu-id="b4cd8-195">Hybrid Connection Manager</span><span class="sxs-lookup"><span data-stu-id="b4cd8-195">Hybrid Connection Manager</span></span> ##

<span data-ttu-id="b4cd8-196">The Hybrid Connections feature requires a relay agent in the network that hosts your Hybrid Connection endpoint.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-196">The Hybrid Connections feature requires a relay agent in the network that hosts your Hybrid Connection endpoint.</span></span> <span data-ttu-id="b4cd8-197">That relay agent is called the Hybrid Connection Manager (HCM).</span><span class="sxs-lookup"><span data-stu-id="b4cd8-197">That relay agent is called the Hybrid Connection Manager (HCM).</span></span> <span data-ttu-id="b4cd8-198">To download HCM, from your app in the [Azure portal][portal], select **Networking** > **Configure your Hybrid Connection endpoints**.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-198">To download HCM, from your app in the [Azure portal][portal], select **Networking** > **Configure your Hybrid Connection endpoints**.</span></span>  

<span data-ttu-id="b4cd8-199">This tool runs on Windows Server 2012 and later.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-199">This tool runs on Windows Server 2012 and later.</span></span> <span data-ttu-id="b4cd8-200">The HCM runs as a service and connects outbound to Azure Relay on port 443.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-200">The HCM runs as a service and connects outbound to Azure Relay on port 443.</span></span>  

<span data-ttu-id="b4cd8-201">After installing HCM, you can run HybridConnectionManagerUi.exe to use the UI for the tool.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-201">After installing HCM, you can run HybridConnectionManagerUi.exe to use the UI for the tool.</span></span> <span data-ttu-id="b4cd8-202">This file is in the Hybrid Connection Manager installation directory.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-202">This file is in the Hybrid Connection Manager installation directory.</span></span> <span data-ttu-id="b4cd8-203">In Windows 10, you can also just search for *Hybrid Connection Manager UI* in your search box.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-203">In Windows 10, you can also just search for *Hybrid Connection Manager UI* in your search box.</span></span>  

![Screenshot of Hybrid Connection Manager][7]

<span data-ttu-id="b4cd8-205">When you start the HCM UI, the first thing you see is a table that lists all the Hybrid Connections that are configured with this instance of the HCM.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-205">When you start the HCM UI, the first thing you see is a table that lists all the Hybrid Connections that are configured with this instance of the HCM.</span></span> <span data-ttu-id="b4cd8-206">If you want to make any changes, first authenticate with Azure.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-206">If you want to make any changes, first authenticate with Azure.</span></span> 

<span data-ttu-id="b4cd8-207">To add one or more Hybrid Connections to your HCM:</span><span class="sxs-lookup"><span data-stu-id="b4cd8-207">To add one or more Hybrid Connections to your HCM:</span></span>

1. <span data-ttu-id="b4cd8-208">Start the HCM UI.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-208">Start the HCM UI.</span></span>
1. <span data-ttu-id="b4cd8-209">Select **Configure another Hybrid Connection**.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-209">Select **Configure another Hybrid Connection**.</span></span>
<span data-ttu-id="b4cd8-210">![Screenshot of Configure New Hybrid Connections][8]</span><span class="sxs-lookup"><span data-stu-id="b4cd8-210">![Screenshot of Configure New Hybrid Connections][8]</span></span>

1. <span data-ttu-id="b4cd8-211">Sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-211">Sign in with your Azure account.</span></span>
1. <span data-ttu-id="b4cd8-212">Choose a subscription.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-212">Choose a subscription.</span></span>
1. <span data-ttu-id="b4cd8-213">Select the Hybrid Connections that you want the HCM to relay.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-213">Select the Hybrid Connections that you want the HCM to relay.</span></span>
<span data-ttu-id="b4cd8-214">![Screenshot of Hybrid Connections][9]</span><span class="sxs-lookup"><span data-stu-id="b4cd8-214">![Screenshot of Hybrid Connections][9]</span></span>

1. <span data-ttu-id="b4cd8-215">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-215">Select **Save**.</span></span>

<span data-ttu-id="b4cd8-216">You can now see the Hybrid Connections you added.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-216">You can now see the Hybrid Connections you added.</span></span> <span data-ttu-id="b4cd8-217">You can also select the configured Hybrid Connection to see details.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-217">You can also select the configured Hybrid Connection to see details.</span></span>

![Screenshot of Hybrid Connection Details][10]

<span data-ttu-id="b4cd8-219">To support the Hybrid Connections it is configured with, HCM requires:</span><span class="sxs-lookup"><span data-stu-id="b4cd8-219">To support the Hybrid Connections it is configured with, HCM requires:</span></span>

- <span data-ttu-id="b4cd8-220">TCP access to Azure over port 443.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-220">TCP access to Azure over port 443.</span></span>
- <span data-ttu-id="b4cd8-221">TCP access to the Hybrid Connection endpoint.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-221">TCP access to the Hybrid Connection endpoint.</span></span>
- <span data-ttu-id="b4cd8-222">The ability to do DNS look-ups on the endpoint host and the Service Bus namespace.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-222">The ability to do DNS look-ups on the endpoint host and the Service Bus namespace.</span></span>

> [!NOTE]
> <span data-ttu-id="b4cd8-223">Azure Relay relies on Web Sockets for connectivity.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-223">Azure Relay relies on Web Sockets for connectivity.</span></span> <span data-ttu-id="b4cd8-224">This capability is only available on Windows Server 2012 or later.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-224">This capability is only available on Windows Server 2012 or later.</span></span> <span data-ttu-id="b4cd8-225">Because of that, HCM is not supported on anything earlier than Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-225">Because of that, HCM is not supported on anything earlier than Windows Server 2012.</span></span>
>

### <a name="redundancy"></a><span data-ttu-id="b4cd8-226">Redundancy</span><span class="sxs-lookup"><span data-stu-id="b4cd8-226">Redundancy</span></span> ###

<span data-ttu-id="b4cd8-227">Each HCM can support multiple Hybrid Connections.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-227">Each HCM can support multiple Hybrid Connections.</span></span> <span data-ttu-id="b4cd8-228">Also, any given Hybrid Connection can be supported by multiple HCMs.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-228">Also, any given Hybrid Connection can be supported by multiple HCMs.</span></span> <span data-ttu-id="b4cd8-229">The default behavior is to route traffic across the configured HCMs for any given endpoint.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-229">The default behavior is to route traffic across the configured HCMs for any given endpoint.</span></span> <span data-ttu-id="b4cd8-230">If you want high availability on your Hybrid Connections from your network, run multiple HCMs on separate machines.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-230">If you want high availability on your Hybrid Connections from your network, run multiple HCMs on separate machines.</span></span> <span data-ttu-id="b4cd8-231">The load distribution algorithm used by the Relay service to distribute traffic to the HCMs is random assignment.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-231">The load distribution algorithm used by the Relay service to distribute traffic to the HCMs is random assignment.</span></span> 

### <a name="manually-add-a-hybrid-connection"></a><span data-ttu-id="b4cd8-232">Manually add a Hybrid Connection</span><span class="sxs-lookup"><span data-stu-id="b4cd8-232">Manually add a Hybrid Connection</span></span> ###

<span data-ttu-id="b4cd8-233">To enable someone outside your subscription to host an HCM instance for a given Hybrid Connection, share the gateway connection string for the Hybrid Connection with them.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-233">To enable someone outside your subscription to host an HCM instance for a given Hybrid Connection, share the gateway connection string for the Hybrid Connection with them.</span></span> <span data-ttu-id="b4cd8-234">You can see the gateway connection string in the Hybrid Connection properties in the [Azure portal][portal].</span><span class="sxs-lookup"><span data-stu-id="b4cd8-234">You can see the gateway connection string in the Hybrid Connection properties in the [Azure portal][portal].</span></span> <span data-ttu-id="b4cd8-235">To use that string, select **Enter Manually** in the HCM, and paste in the gateway connection string.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-235">To use that string, select **Enter Manually** in the HCM, and paste in the gateway connection string.</span></span>

![Manually add a Hybrid Connection][11]

### <a name="upgrade"></a><span data-ttu-id="b4cd8-237">Upgrade</span><span class="sxs-lookup"><span data-stu-id="b4cd8-237">Upgrade</span></span> ###

<span data-ttu-id="b4cd8-238">There are periodic updates to the Hybrid Connection Manager to fix issues or provide improvements.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-238">There are periodic updates to the Hybrid Connection Manager to fix issues or provide improvements.</span></span> <span data-ttu-id="b4cd8-239">When upgrades are released, a popup will show up in the HCM UI.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-239">When upgrades are released, a popup will show up in the HCM UI.</span></span> <span data-ttu-id="b4cd8-240">Applying the upgrade will apply the changes and restart the HCM.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-240">Applying the upgrade will apply the changes and restart the HCM.</span></span> 

## <a name="adding-a-hybrid-connection-to-your-app-programmatically"></a><span data-ttu-id="b4cd8-241">Adding a Hybrid Connection to your app programmatically</span><span class="sxs-lookup"><span data-stu-id="b4cd8-241">Adding a Hybrid Connection to your app programmatically</span></span> ##

<span data-ttu-id="b4cd8-242">The APIs noted below can be used directly to manage the Hybrid Connections connected to your web apps.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-242">The APIs noted below can be used directly to manage the Hybrid Connections connected to your web apps.</span></span> 

    /subscriptions/[subscription name]/resourceGroups/[resource group name]/providers/Microsoft.Web/sites/[app name]/hybridConnectionNamespaces/[relay namespace name]/relays/[hybrid connection name]?api-version=2016-08-01

<span data-ttu-id="b4cd8-243">The JSON object associated with a Hybrid Connection looks like:</span><span class="sxs-lookup"><span data-stu-id="b4cd8-243">The JSON object associated with a Hybrid Connection looks like:</span></span>

    {
      "name": "[hybrid connection name]",
      "type": "Microsoft.Relay/Namespaces/HybridConnections",
      "location": "[location]",
      "properties": {
        "serviceBusNamespace": "[namespace name]",
        "relayName": "[hybrid connection name]",
        "relayArmUri": "/subscriptions/[subscription id]/resourceGroups/[resource group name]/providers/Microsoft.Relay/namespaces/[namespace name]/hybridconnections/[hybrid connection name]",
        "hostName": "[endpoint host name]",
        "port": [port],
        "sendKeyName": "defaultSender",
        "sendKeyValue": "[send key]"
      }
    }

<span data-ttu-id="b4cd8-244">One way to use this information is with the armclient, which you can get from the [ARMClient][armclient] github project.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-244">One way to use this information is with the armclient, which you can get from the [ARMClient][armclient] github project.</span></span> <span data-ttu-id="b4cd8-245">Here is an example on attaching a pre-existing Hybrid Connection to your web app.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-245">Here is an example on attaching a pre-existing Hybrid Connection to your web app.</span></span> <span data-ttu-id="b4cd8-246">Create a JSON file per the above schema like:</span><span class="sxs-lookup"><span data-stu-id="b4cd8-246">Create a JSON file per the above schema like:</span></span>

    {
      "name": "relay-demo-hc",
      "type": "Microsoft.Relay/Namespaces/HybridConnections",
      "location": "North Central US",
      "properties": {
        "serviceBusNamespace": "demo-relay",
        "relayName": "relay-demo-hc",
        "relayArmUri": "/subscriptions/ebcidic-asci-anna-nath-rak1111111/resourceGroups/myrelay-rg/providers/Microsoft.Relay/namespaces/demo-relay/hybridconnections/relay-demo-hc",
        "hostName": "my-wkstn.home",
        "port": 1433,
        "sendKeyName": "defaultSender",
        "sendKeyValue": "Th9is3is8a82lot93of3774stu887ff122235="
      }
    }

To use this API, you need the send key and relay resource ID. <span data-ttu-id="b4cd8-248">If you saved your information with the filename hctest.json, issue this command to attach your Hybrid Connection to your app:</span><span class="sxs-lookup"><span data-stu-id="b4cd8-248">If you saved your information with the filename hctest.json, issue this command to attach your Hybrid Connection to your app:</span></span> 

    armclient login
    armclient put /subscriptions/ebcidic-asci-anna-nath-rak1111111/resourceGroups/myapp-rg/providers/Microsoft.Web/sites/myhcdemoapp/hybridConnectionNamespaces/demo-relay/relays/relay-demo-hc?api-version=2016-08-01 @hctest.json

## <a name="troubleshooting"></a><span data-ttu-id="b4cd8-249">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="b4cd8-249">Troubleshooting</span></span> ##

<span data-ttu-id="b4cd8-250">The status of "Connected" means that at least one HCM is configured with that Hybrid Connection, and is able to reach Azure.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-250">The status of "Connected" means that at least one HCM is configured with that Hybrid Connection, and is able to reach Azure.</span></span> <span data-ttu-id="b4cd8-251">If the status for your Hybrid Connection does not say **Connected**, your Hybrid Connection is not configured on any HCM that has access to Azure.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-251">If the status for your Hybrid Connection does not say **Connected**, your Hybrid Connection is not configured on any HCM that has access to Azure.</span></span>

<span data-ttu-id="b4cd8-252">The primary reason that clients cannot connect to their endpoint is because the endpoint was specified by using an IP address instead of a DNS name.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-252">The primary reason that clients cannot connect to their endpoint is because the endpoint was specified by using an IP address instead of a DNS name.</span></span> <span data-ttu-id="b4cd8-253">If your app cannot reach the desired endpoint and you used an IP address, switch to using a DNS name that is valid on the host where the HCM is running.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-253">If your app cannot reach the desired endpoint and you used an IP address, switch to using a DNS name that is valid on the host where the HCM is running.</span></span> <span data-ttu-id="b4cd8-254">Also check that the DNS name resolves properly on the host where the HCM is running.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-254">Also check that the DNS name resolves properly on the host where the HCM is running.</span></span> <span data-ttu-id="b4cd8-255">Confirm that there is connectivity from the host where the HCM is running to the Hybrid Connection endpoint.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-255">Confirm that there is connectivity from the host where the HCM is running to the Hybrid Connection endpoint.</span></span>  

<span data-ttu-id="b4cd8-256">In App Service, the tcpping tool can be invoked from the Advanced Tools (Kudu) console.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-256">In App Service, the tcpping tool can be invoked from the Advanced Tools (Kudu) console.</span></span> <span data-ttu-id="b4cd8-257">This tool can tell you if you have access to a TCP endpoint, but it does not tell you if you have access to a Hybrid Connection endpoint.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-257">This tool can tell you if you have access to a TCP endpoint, but it does not tell you if you have access to a Hybrid Connection endpoint.</span></span> <span data-ttu-id="b4cd8-258">When you use the tool in the console against a Hybrid Connection endpoint, you are only confirming that it uses a host:port combination.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-258">When you use the tool in the console against a Hybrid Connection endpoint, you are only confirming that it uses a host:port combination.</span></span>  

## <a name="biztalk-hybrid-connections"></a><span data-ttu-id="b4cd8-259">BizTalk Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="b4cd8-259">BizTalk Hybrid Connections</span></span> ##

<span data-ttu-id="b4cd8-260">The early form of this feature was called BizTalk Hybrid Connections.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-260">The early form of this feature was called BizTalk Hybrid Connections.</span></span> <span data-ttu-id="b4cd8-261">This capability went End of Life on May 31, 2018 and ceased operations.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-261">This capability went End of Life on May 31, 2018 and ceased operations.</span></span> <span data-ttu-id="b4cd8-262">BizTalk hybrid connections have been removed from all web apps and are not accessible through the portal or API.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-262">BizTalk hybrid connections have been removed from all web apps and are not accessible through the portal or API.</span></span> <span data-ttu-id="b4cd8-263">If you still have these older connections configured in the Hybrid Connection Manager, then you will see a status of Discontinued and display an End of Life statement at the bottom.</span><span class="sxs-lookup"><span data-stu-id="b4cd8-263">If you still have these older connections configured in the Hybrid Connection Manager, then you will see a status of Discontinued and display an End of Life statement at the bottom.</span></span>

![BizTalk Hybrid Connections in the HCM][12]


<!--Image references-->
[1]: ./media/app-service-hybrid-connections/hybridconn-connectiondiagram.png
[2]: ./media/app-service-hybrid-connections/hybridconn-portal.png
[3]: ./media/app-service-hybrid-connections/hybridconn-addhc.png
[4]: ./media/app-service-hybrid-connections/hybridconn-createhc.png
[5]: ./media/app-service-hybrid-connections/hybridconn-properties.png
[6]: ./media/app-service-hybrid-connections/hybridconn-aspproperties.png
[7]: ./media/app-service-hybrid-connections/hybridconn-hcm.png
[8]: ./media/app-service-hybrid-connections/hybridconn-hcmadd.png
[9]: ./media/app-service-hybrid-connections/hybridconn-hcmadded.png
[10]: ./media/app-service-hybrid-connections/hybridconn-hcmdetails.png
[11]: ./media/app-service-hybrid-connections/hybridconn-manual.png
[12]: ./media/app-service-hybrid-connections/hybridconn-bt.png

<!--Links-->
[HCService]: http://docs.microsoft.com/azure/service-bus-relay/relay-hybrid-connections-protocol/
[portal]: http://portal.azure.com/
[oldhc]: http://docs.microsoft.com/azure/biztalk-services/integration-hybrid-connection-overview/
[sbpricing]: http://azure.microsoft.com/pricing/details/service-bus/
[armclient]: https://github.com/projectkudu/ARMClient/
