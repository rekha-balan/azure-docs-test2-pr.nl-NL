---
title: Create a path-based rule - Azure Application Gateway - Azure Portal | Microsoft Docs
description: Learn how to create a Path-based rule for an application gateway by using the portal
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 87bd93bc-e1a6-45db-a226-555948f1feb7
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 0399e3ca73a0937776a0bea51739fe79bcb032c7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553763"
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-the-portal"></a><span data-ttu-id="4ee93-103">Create a Path-based rule for an application gateway by using the portal</span><span class="sxs-lookup"><span data-stu-id="4ee93-103">Create a Path-based rule for an application gateway by using the portal</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-url-route-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-url-route-arm-ps.md)

<span data-ttu-id="4ee93-106">URL Path-based routing enables you to associate routes based on the URL path of Http request.</span><span class="sxs-lookup"><span data-stu-id="4ee93-106">URL Path-based routing enables you to associate routes based on the URL path of Http request.</span></span> <span data-ttu-id="4ee93-107">It checks if there is a route to a back-end pool configured for the URL listed in the Application Gateway and sends the network traffic to the defined back-end pool.</span><span class="sxs-lookup"><span data-stu-id="4ee93-107">It checks if there is a route to a back-end pool configured for the URL listed in the Application Gateway and sends the network traffic to the defined back-end pool.</span></span> <span data-ttu-id="4ee93-108">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span><span class="sxs-lookup"><span data-stu-id="4ee93-108">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span></span>

<span data-ttu-id="4ee93-109">URL-based routing introduces a new rule type to application gateway.</span><span class="sxs-lookup"><span data-stu-id="4ee93-109">URL-based routing introduces a new rule type to application gateway.</span></span> <span data-ttu-id="4ee93-110">Application gateway has two rule types: basic and path-based rules.</span><span class="sxs-lookup"><span data-stu-id="4ee93-110">Application gateway has two rule types: basic and path-based rules.</span></span> <span data-ttu-id="4ee93-111">The basic rule type, provides round-robin service for the back-end pools while path-based rules in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the appropriate backend pool.</span><span class="sxs-lookup"><span data-stu-id="4ee93-111">The basic rule type, provides round-robin service for the back-end pools while path-based rules in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the appropriate backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="4ee93-112">Scenario</span><span class="sxs-lookup"><span data-stu-id="4ee93-112">Scenario</span></span>

<span data-ttu-id="4ee93-113">The following scenario goes through creating a Path-based rule in an existing application gateway.</span><span class="sxs-lookup"><span data-stu-id="4ee93-113">The following scenario goes through creating a Path-based rule in an existing application gateway.</span></span>
<span data-ttu-id="4ee93-114">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4ee93-114">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

![url route][scenario]

## <a name="createrule"></a><span data-ttu-id="4ee93-116">Create the Path-based rule</span><span class="sxs-lookup"><span data-stu-id="4ee93-116">Create the Path-based rule</span></span>

<span data-ttu-id="4ee93-117">A Path-based rule requires its own listener, before creating the rule be sure to verify you have an available listener to use.</span><span class="sxs-lookup"><span data-stu-id="4ee93-117">A Path-based rule requires its own listener, before creating the rule be sure to verify you have an available listener to use.</span></span>

### <a name="step-1"></a><span data-ttu-id="4ee93-118">Step 1</span><span class="sxs-lookup"><span data-stu-id="4ee93-118">Step 1</span></span>

<span data-ttu-id="4ee93-119">Navigate to the [Azure portal](http://portal.azure.com) and select an existing application gateway.</span><span class="sxs-lookup"><span data-stu-id="4ee93-119">Navigate to the [Azure portal](http://portal.azure.com) and select an existing application gateway.</span></span> <span data-ttu-id="4ee93-120">Click **Rules**</span><span class="sxs-lookup"><span data-stu-id="4ee93-120">Click **Rules**</span></span>

![Application Gateway overview][1]

### <a name="step-2"></a><span data-ttu-id="4ee93-122">Step 2</span><span class="sxs-lookup"><span data-stu-id="4ee93-122">Step 2</span></span>

<span data-ttu-id="4ee93-123">Click **Path-based** button to add a new Path-based rule.</span><span class="sxs-lookup"><span data-stu-id="4ee93-123">Click **Path-based** button to add a new Path-based rule.</span></span>

### <a name="step-3"></a><span data-ttu-id="4ee93-124">Step 3</span><span class="sxs-lookup"><span data-stu-id="4ee93-124">Step 3</span></span>

<span data-ttu-id="4ee93-125">The **Add path-based rule** blade has two sections.</span><span class="sxs-lookup"><span data-stu-id="4ee93-125">The **Add path-based rule** blade has two sections.</span></span> <span data-ttu-id="4ee93-126">The first section is where you defined the listener, the name of the rule and the default path settings.</span><span class="sxs-lookup"><span data-stu-id="4ee93-126">The first section is where you defined the listener, the name of the rule and the default path settings.</span></span> <span data-ttu-id="4ee93-127">The default path settings are for routes that do not fall under the custom path-based route.</span><span class="sxs-lookup"><span data-stu-id="4ee93-127">The default path settings are for routes that do not fall under the custom path-based route.</span></span> <span data-ttu-id="4ee93-128">The second section of the **Add path-based rule** blade is where you define the path-based rules themselves.</span><span class="sxs-lookup"><span data-stu-id="4ee93-128">The second section of the **Add path-based rule** blade is where you define the path-based rules themselves.</span></span>

<span data-ttu-id="4ee93-129">**Basic Settings**</span><span class="sxs-lookup"><span data-stu-id="4ee93-129">**Basic Settings**</span></span>

* <span data-ttu-id="4ee93-130">**Name** - This is a friendly name to the rule that is accessible in the portal.</span><span class="sxs-lookup"><span data-stu-id="4ee93-130">**Name** - This is a friendly name to the rule that is accessible in the portal.</span></span>
* <span data-ttu-id="4ee93-131">**Listener** - This is the listener that is used for the rule.</span><span class="sxs-lookup"><span data-stu-id="4ee93-131">**Listener** - This is the listener that is used for the rule.</span></span>
* <span data-ttu-id="4ee93-132">**Default backend pool** - This setting is the setting that defines the back-end to be used for the default rule</span><span class="sxs-lookup"><span data-stu-id="4ee93-132">**Default backend pool** - This setting is the setting that defines the back-end to be used for the default rule</span></span>
* <span data-ttu-id="4ee93-133">**Default HTTP settings** - This setting is the setting that defines the HTTP settings to be used for the default rule.</span><span class="sxs-lookup"><span data-stu-id="4ee93-133">**Default HTTP settings** - This setting is the setting that defines the HTTP settings to be used for the default rule.</span></span>

<span data-ttu-id="4ee93-134">**Path-based rules**</span><span class="sxs-lookup"><span data-stu-id="4ee93-134">**Path-based rules**</span></span>

* <span data-ttu-id="4ee93-135">**Name** - This is a friendly name to path-based rule.</span><span class="sxs-lookup"><span data-stu-id="4ee93-135">**Name** - This is a friendly name to path-based rule.</span></span>
* <span data-ttu-id="4ee93-136">**Paths** - This setting defines the path the rule will look for when forwarding traffic</span><span class="sxs-lookup"><span data-stu-id="4ee93-136">**Paths** - This setting defines the path the rule will look for when forwarding traffic</span></span>
* <span data-ttu-id="4ee93-137">**Backend Pool** - This setting is the setting that defines the back-end to be used for the rule</span><span class="sxs-lookup"><span data-stu-id="4ee93-137">**Backend Pool** - This setting is the setting that defines the back-end to be used for the rule</span></span>
* <span data-ttu-id="4ee93-138">**HTTP setting** - This setting is the setting that defines the HTTP settings to be used for the rule.</span><span class="sxs-lookup"><span data-stu-id="4ee93-138">**HTTP setting** - This setting is the setting that defines the HTTP settings to be used for the rule.</span></span>

> [!IMPORTANT]
> Paths: The list of path patterns to match. Each must start with / and the only place a "\*" is allowed is at the end. Valid examples are /xyz, /xyz* or /xyz/*.  

![Add path-based rule blade with information filled out][2]

<span data-ttu-id="4ee93-143">Adding a path-based rule to an existing application gateway is an easy process through the portal.</span><span class="sxs-lookup"><span data-stu-id="4ee93-143">Adding a path-based rule to an existing application gateway is an easy process through the portal.</span></span> <span data-ttu-id="4ee93-144">Once a path-based rule has been created, it can be edited to add additional rules easily.</span><span class="sxs-lookup"><span data-stu-id="4ee93-144">Once a path-based rule has been created, it can be edited to add additional rules easily.</span></span> 

![adding additional path-based rules][3]

<span data-ttu-id="4ee93-146">This configures a path based route.</span><span class="sxs-lookup"><span data-stu-id="4ee93-146">This configures a path based route.</span></span> <span data-ttu-id="4ee93-147">It is important to understand that requests are not re-written, as requests come in application gateway inspects the request and basic on the url pattern sends the request to the appropriate back-end.</span><span class="sxs-lookup"><span data-stu-id="4ee93-147">It is important to understand that requests are not re-written, as requests come in application gateway inspects the request and basic on the url pattern sends the request to the appropriate back-end.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ee93-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="4ee93-148">Next steps</span></span>

<span data-ttu-id="4ee93-149">To learn how to configure SSL Offloading with Azure Application Gateway see [Configure SSL Offload](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="4ee93-149">To learn how to configure SSL Offloading with Azure Application Gateway see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-url-route-portal/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-url-route-portal/figure2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-url-route-portal/figure3.png
[scenario]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-url-route-portal/scenario.png




