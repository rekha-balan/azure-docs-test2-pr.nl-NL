---
title: Manage your first API in Azure API Management | Microsoft Docs
description: Learn how to create APIs, add operations, and get started with API Management.
services: api-management
documentationcenter: ''
author: steved0x
manager: erikre
editor: ''
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f28b12c7469d88ba519193e4ce94c74362cce114
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662277"
---
# <a name="manage-your-first-api-in-azure-api-management"></a><span data-ttu-id="c98c3-103">Manage your first API in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="c98c3-103">Manage your first API in Azure API Management</span></span>
## <span data-ttu-id="c98c3-104"><a name="overview"> </a>Overview</span><span class="sxs-lookup"><span data-stu-id="c98c3-104"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="c98c3-105">This guide shows you how to quickly get started in using Azure API Management and make your first API call.</span><span class="sxs-lookup"><span data-stu-id="c98c3-105">This guide shows you how to quickly get started in using Azure API Management and make your first API call.</span></span>

## <span data-ttu-id="c98c3-106"><a name="concepts"> </a>What is Azure API Management?</span><span class="sxs-lookup"><span data-stu-id="c98c3-106"><a name="concepts"> </a>What is Azure API Management?</span></span>
<span data-ttu-id="c98c3-107">You can use Azure API Management to take any backend and launch a full-fledged API program based on it.</span><span class="sxs-lookup"><span data-stu-id="c98c3-107">You can use Azure API Management to take any backend and launch a full-fledged API program based on it.</span></span>

<span data-ttu-id="c98c3-108">Common scenarios include:</span><span class="sxs-lookup"><span data-stu-id="c98c3-108">Common scenarios include:</span></span>

* <span data-ttu-id="c98c3-109">**Securing mobile infrastructure** by gating access with API keys, preventing DOS attacks by using throttling, or using advanced security policies like JWT token validation.</span><span class="sxs-lookup"><span data-stu-id="c98c3-109">**Securing mobile infrastructure** by gating access with API keys, preventing DOS attacks by using throttling, or using advanced security policies like JWT token validation.</span></span>
* <span data-ttu-id="c98c3-110">**Enabling ISV partner ecosystems** by offering fast partner onboarding through the developer portal and building an API facade to decouple from internal implementations that are not ripe for partner consumption.</span><span class="sxs-lookup"><span data-stu-id="c98c3-110">**Enabling ISV partner ecosystems** by offering fast partner onboarding through the developer portal and building an API facade to decouple from internal implementations that are not ripe for partner consumption.</span></span>
* <span data-ttu-id="c98c3-111">**Running an internal API program** by offering a centralized location for the organization to communicate about the availability and latest changes to APIs, gating access based on organizational accounts, all based on a secured channel between the API gateway and the backend.</span><span class="sxs-lookup"><span data-stu-id="c98c3-111">**Running an internal API program** by offering a centralized location for the organization to communicate about the availability and latest changes to APIs, gating access based on organizational accounts, all based on a secured channel between the API gateway and the backend.</span></span>

<span data-ttu-id="c98c3-112">The system is made up of the following components:</span><span class="sxs-lookup"><span data-stu-id="c98c3-112">The system is made up of the following components:</span></span>

* <span data-ttu-id="c98c3-113">The **API gateway** is the endpoint that:</span><span class="sxs-lookup"><span data-stu-id="c98c3-113">The **API gateway** is the endpoint that:</span></span>
  
  * <span data-ttu-id="c98c3-114">Accepts API calls and routes them to your backends.</span><span class="sxs-lookup"><span data-stu-id="c98c3-114">Accepts API calls and routes them to your backends.</span></span>
  * <span data-ttu-id="c98c3-115">Verifies API keys, JWT tokens, certificates, and other credentials.</span><span class="sxs-lookup"><span data-stu-id="c98c3-115">Verifies API keys, JWT tokens, certificates, and other credentials.</span></span>
  * <span data-ttu-id="c98c3-116">Enforces usage quotas and rate limits.</span><span class="sxs-lookup"><span data-stu-id="c98c3-116">Enforces usage quotas and rate limits.</span></span>
  * <span data-ttu-id="c98c3-117">Transforms your API on the fly without code modifications.</span><span class="sxs-lookup"><span data-stu-id="c98c3-117">Transforms your API on the fly without code modifications.</span></span>
  * <span data-ttu-id="c98c3-118">Caches backend responses where set up.</span><span class="sxs-lookup"><span data-stu-id="c98c3-118">Caches backend responses where set up.</span></span>
  * <span data-ttu-id="c98c3-119">Logs call metadata for analytics purposes.</span><span class="sxs-lookup"><span data-stu-id="c98c3-119">Logs call metadata for analytics purposes.</span></span>
* <span data-ttu-id="c98c3-120">The **publisher portal** is the administrative interface where you set up your API program.</span><span class="sxs-lookup"><span data-stu-id="c98c3-120">The **publisher portal** is the administrative interface where you set up your API program.</span></span> <span data-ttu-id="c98c3-121">Use it to:</span><span class="sxs-lookup"><span data-stu-id="c98c3-121">Use it to:</span></span>
  
  * <span data-ttu-id="c98c3-122">Define or import API schema.</span><span class="sxs-lookup"><span data-stu-id="c98c3-122">Define or import API schema.</span></span>
  * <span data-ttu-id="c98c3-123">Package APIs into products.</span><span class="sxs-lookup"><span data-stu-id="c98c3-123">Package APIs into products.</span></span>
  * <span data-ttu-id="c98c3-124">Set up policies like quotas or transformations on the APIs.</span><span class="sxs-lookup"><span data-stu-id="c98c3-124">Set up policies like quotas or transformations on the APIs.</span></span>
  * <span data-ttu-id="c98c3-125">Get insights from analytics.</span><span class="sxs-lookup"><span data-stu-id="c98c3-125">Get insights from analytics.</span></span>
  * <span data-ttu-id="c98c3-126">Manage users.</span><span class="sxs-lookup"><span data-stu-id="c98c3-126">Manage users.</span></span>
* <span data-ttu-id="c98c3-127">The **developer portal** serves as the main web presence for developers, where they can:</span><span class="sxs-lookup"><span data-stu-id="c98c3-127">The **developer portal** serves as the main web presence for developers, where they can:</span></span>
  
  * <span data-ttu-id="c98c3-128">Read API documentation.</span><span class="sxs-lookup"><span data-stu-id="c98c3-128">Read API documentation.</span></span>
  * <span data-ttu-id="c98c3-129">Try out an API via the interactive console.</span><span class="sxs-lookup"><span data-stu-id="c98c3-129">Try out an API via the interactive console.</span></span>
  * <span data-ttu-id="c98c3-130">Create an account and subscribe to get API keys.</span><span class="sxs-lookup"><span data-stu-id="c98c3-130">Create an account and subscribe to get API keys.</span></span>
  * <span data-ttu-id="c98c3-131">Access analytics on their own usage.</span><span class="sxs-lookup"><span data-stu-id="c98c3-131">Access analytics on their own usage.</span></span>

## <span data-ttu-id="c98c3-132"><a name="create-service-instance"> </a>Create an API Management instance</span><span class="sxs-lookup"><span data-stu-id="c98c3-132"><a name="create-service-instance"> </a>Create an API Management instance</span></span>
> [!NOTE]
> <span data-ttu-id="c98c3-133">To complete this tutorial, you need an Azure account.</span><span class="sxs-lookup"><span data-stu-id="c98c3-133">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="c98c3-134">If you don't have an account, you can create a free account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="c98c3-134">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="c98c3-135">For details, see [Azure Free Trial][Azure Free Trial].</span><span class="sxs-lookup"><span data-stu-id="c98c3-135">For details, see [Azure Free Trial][Azure Free Trial].</span></span>
> 
> 

<span data-ttu-id="c98c3-136">The first step in working with API Management is to create a service instance.</span><span class="sxs-lookup"><span data-stu-id="c98c3-136">The first step in working with API Management is to create a service instance.</span></span> <span data-ttu-id="c98c3-137">Sign in to the [Azure Portal][Azure Portal] and click **New**, **Web + Mobile**, **API Management**.</span><span class="sxs-lookup"><span data-stu-id="c98c3-137">Sign in to the [Azure Portal][Azure Portal] and click **New**, **Web + Mobile**, **API Management**.</span></span>

![API Management new instance][api-management-create-instance-menu]

<span data-ttu-id="c98c3-139">For **Name**, specify a unique sub-domain name to use for the service URL.</span><span class="sxs-lookup"><span data-stu-id="c98c3-139">For **Name**, specify a unique sub-domain name to use for the service URL.</span></span>

<span data-ttu-id="c98c3-140">Choose the desired **Subscription**, **Resource group** and **Location** for your service instance.</span><span class="sxs-lookup"><span data-stu-id="c98c3-140">Choose the desired **Subscription**, **Resource group** and **Location** for your service instance.</span></span>

<span data-ttu-id="c98c3-141">Enter **Contoso Ltd.** for the **Organization Name**, and enter your email address in the **Administrator E-Mail** field.</span><span class="sxs-lookup"><span data-stu-id="c98c3-141">Enter **Contoso Ltd.** for the **Organization Name**, and enter your email address in the **Administrator E-Mail** field.</span></span>

> [!NOTE]
> <span data-ttu-id="c98c3-142">This email address is used for notifications from the API Management system.</span><span class="sxs-lookup"><span data-stu-id="c98c3-142">This email address is used for notifications from the API Management system.</span></span> <span data-ttu-id="c98c3-143">For more information, see [How to configure notifications and email templates in Azure API Management][How to configure notifications and email templates in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="c98c3-143">For more information, see [How to configure notifications and email templates in Azure API Management][How to configure notifications and email templates in Azure API Management].</span></span>
> 
> 

![New API Management service][api-management-create-instance-step1]

<span data-ttu-id="c98c3-145">API Management service instances are available in three tiers: Developer, Standard, and Premium.</span><span class="sxs-lookup"><span data-stu-id="c98c3-145">API Management service instances are available in three tiers: Developer, Standard, and Premium.</span></span>

> [!NOTE]
> <span data-ttu-id="c98c3-146">The Developer Tier is for development, testing, and pilot API programs where high availability is not a concern.</span><span class="sxs-lookup"><span data-stu-id="c98c3-146">The Developer Tier is for development, testing, and pilot API programs where high availability is not a concern.</span></span> <span data-ttu-id="c98c3-147">In the Standard and Premium tiers, you can scale your reserved unit count to handle more traffic.</span><span class="sxs-lookup"><span data-stu-id="c98c3-147">In the Standard and Premium tiers, you can scale your reserved unit count to handle more traffic.</span></span> <span data-ttu-id="c98c3-148">The Standard and Premium tiers provide your API Management service with the most processing power and performance.</span><span class="sxs-lookup"><span data-stu-id="c98c3-148">The Standard and Premium tiers provide your API Management service with the most processing power and performance.</span></span> <span data-ttu-id="c98c3-149">You can complete this tutorial by using any tier.</span><span class="sxs-lookup"><span data-stu-id="c98c3-149">You can complete this tutorial by using any tier.</span></span> <span data-ttu-id="c98c3-150">For more information about API Management tiers, see [API Management pricing][API Management pricing].</span><span class="sxs-lookup"><span data-stu-id="c98c3-150">For more information about API Management tiers, see [API Management pricing][API Management pricing].</span></span>
> 
> 

<span data-ttu-id="c98c3-151">Click **Create** to start provisioning your service instance.</span><span class="sxs-lookup"><span data-stu-id="c98c3-151">Click **Create** to start provisioning your service instance.</span></span>

![New API Management service][api-management-instance-created]

<span data-ttu-id="c98c3-153">Once the service instance is created, the next step is to create or import an API.</span><span class="sxs-lookup"><span data-stu-id="c98c3-153">Once the service instance is created, the next step is to create or import an API.</span></span>

## <span data-ttu-id="c98c3-154"><a name="create-api"> </a>Import an API</span><span class="sxs-lookup"><span data-stu-id="c98c3-154"><a name="create-api"> </a>Import an API</span></span>
<span data-ttu-id="c98c3-155">An API consists of a set of operations that can be invoked from a client application.</span><span class="sxs-lookup"><span data-stu-id="c98c3-155">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="c98c3-156">API operations are proxied to existing web services.</span><span class="sxs-lookup"><span data-stu-id="c98c3-156">API operations are proxied to existing web services.</span></span>

<span data-ttu-id="c98c3-157">APIs can be created (and operations can be added) manually, or they can be imported.</span><span class="sxs-lookup"><span data-stu-id="c98c3-157">APIs can be created (and operations can be added) manually, or they can be imported.</span></span> <span data-ttu-id="c98c3-158">In this tutorial, we will import the API for a sample calculator web service provided by Microsoft and hosted on Azure.</span><span class="sxs-lookup"><span data-stu-id="c98c3-158">In this tutorial, we will import the API for a sample calculator web service provided by Microsoft and hosted on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="c98c3-159">For guidance on creating an API and manually adding operations, see [How to create APIs](api-management-howto-create-apis.md) and [How to add operations to an API](api-management-howto-add-operations.md).</span><span class="sxs-lookup"><span data-stu-id="c98c3-159">For guidance on creating an API and manually adding operations, see [How to create APIs](api-management-howto-create-apis.md) and [How to add operations to an API](api-management-howto-add-operations.md).</span></span>
> 
> 

<span data-ttu-id="c98c3-160">APIs are configured from the publisher portal.</span><span class="sxs-lookup"><span data-stu-id="c98c3-160">APIs are configured from the publisher portal.</span></span> <span data-ttu-id="c98c3-161">To reach it, click **Publisher portal** from the service toolbar.</span><span class="sxs-lookup"><span data-stu-id="c98c3-161">To reach it, click **Publisher portal** from the service toolbar.</span></span>

![Publisher portal][api-management-management-console]

<span data-ttu-id="c98c3-163">To import the calculator API, click **APIs** from the **API Management** menu on the left, and then click **Import API**.</span><span class="sxs-lookup"><span data-stu-id="c98c3-163">To import the calculator API, click **APIs** from the **API Management** menu on the left, and then click **Import API**.</span></span>

![Import API button][api-management-import-api]

<span data-ttu-id="c98c3-165">Perform the following steps to configure the calculator API:</span><span class="sxs-lookup"><span data-stu-id="c98c3-165">Perform the following steps to configure the calculator API:</span></span>

1. <span data-ttu-id="c98c3-166">Click **From URL**, enter **http://calcapi.cloudapp.net/calcapi.json** into the **Specification document URL** text box, and click the **Swagger** radio button.</span><span class="sxs-lookup"><span data-stu-id="c98c3-166">Click **From URL**, enter **http://calcapi.cloudapp.net/calcapi.json** into the **Specification document URL** text box, and click the **Swagger** radio button.</span></span>
2. <span data-ttu-id="c98c3-167">Type **calc** into the **Web API URL suffix** text box.</span><span class="sxs-lookup"><span data-stu-id="c98c3-167">Type **calc** into the **Web API URL suffix** text box.</span></span>
3. <span data-ttu-id="c98c3-168">Click in the **Products (optional)** box and choose **Starter**.</span><span class="sxs-lookup"><span data-stu-id="c98c3-168">Click in the **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="c98c3-169">Click **Save** to import the API.</span><span class="sxs-lookup"><span data-stu-id="c98c3-169">Click **Save** to import the API.</span></span>

![Add new API][api-management-import-new-api]

> [!NOTE]
> <span data-ttu-id="c98c3-171">**API Management** currently supports both 1.2 and 2.0 version of Swagger document for import.</span><span class="sxs-lookup"><span data-stu-id="c98c3-171">**API Management** currently supports both 1.2 and 2.0 version of Swagger document for import.</span></span> <span data-ttu-id="c98c3-172">Make sure that, even though [Swagger 2.0 specification](http://swagger.io/specification) declares that `host`, `basePath`, and `schemes` properties are optional, your Swagger 2.0 document **MUST** contain those properties; otherwise it won't get imported.</span><span class="sxs-lookup"><span data-stu-id="c98c3-172">Make sure that, even though [Swagger 2.0 specification](http://swagger.io/specification) declares that `host`, `basePath`, and `schemes` properties are optional, your Swagger 2.0 document **MUST** contain those properties; otherwise it won't get imported.</span></span> 
> 
> 

<span data-ttu-id="c98c3-173">Once the API is imported, the summary page for the API is displayed in the publisher portal.</span><span class="sxs-lookup"><span data-stu-id="c98c3-173">Once the API is imported, the summary page for the API is displayed in the publisher portal.</span></span>

![API summary][api-management-imported-api-summary]

<span data-ttu-id="c98c3-175">The API section has several tabs.</span><span class="sxs-lookup"><span data-stu-id="c98c3-175">The API section has several tabs.</span></span> <span data-ttu-id="c98c3-176">The **Summary** tab displays basic metrics and information about the API.</span><span class="sxs-lookup"><span data-stu-id="c98c3-176">The **Summary** tab displays basic metrics and information about the API.</span></span> <span data-ttu-id="c98c3-177">The [Settings](api-management-howto-create-apis.md#configure-api-settings) tab is used to view and edit the configuration for an API.</span><span class="sxs-lookup"><span data-stu-id="c98c3-177">The [Settings](api-management-howto-create-apis.md#configure-api-settings) tab is used to view and edit the configuration for an API.</span></span> <span data-ttu-id="c98c3-178">The [Operations](api-management-howto-add-operations.md) tab is used to manage the API's operations.</span><span class="sxs-lookup"><span data-stu-id="c98c3-178">The [Operations](api-management-howto-add-operations.md) tab is used to manage the API's operations.</span></span> <span data-ttu-id="c98c3-179">The **Security** tab can be used to configure gateway authentication for the backend server by using Basic authentication or [mutual certificate authentication](api-management-howto-mutual-certificates.md), and to configure [user authorization by using OAuth 2.0](api-management-howto-oauth2.md).</span><span class="sxs-lookup"><span data-stu-id="c98c3-179">The **Security** tab can be used to configure gateway authentication for the backend server by using Basic authentication or [mutual certificate authentication](api-management-howto-mutual-certificates.md), and to configure [user authorization by using OAuth 2.0](api-management-howto-oauth2.md).</span></span>  <span data-ttu-id="c98c3-180">The **Issues** tab is used to view issues reported by the developers who are using your APIs.</span><span class="sxs-lookup"><span data-stu-id="c98c3-180">The **Issues** tab is used to view issues reported by the developers who are using your APIs.</span></span> <span data-ttu-id="c98c3-181">The **Products** tab is used to configure the products that contain this API.</span><span class="sxs-lookup"><span data-stu-id="c98c3-181">The **Products** tab is used to configure the products that contain this API.</span></span>

<span data-ttu-id="c98c3-182">By default, each API Management instance comes with two sample products:</span><span class="sxs-lookup"><span data-stu-id="c98c3-182">By default, each API Management instance comes with two sample products:</span></span>

* <span data-ttu-id="c98c3-183">**Starter**</span><span class="sxs-lookup"><span data-stu-id="c98c3-183">**Starter**</span></span>
* <span data-ttu-id="c98c3-184">**Unlimited**</span><span class="sxs-lookup"><span data-stu-id="c98c3-184">**Unlimited**</span></span>

<span data-ttu-id="c98c3-185">In this tutorial, the Basic Calculator API was added to the Starter product when the API was imported.</span><span class="sxs-lookup"><span data-stu-id="c98c3-185">In this tutorial, the Basic Calculator API was added to the Starter product when the API was imported.</span></span>

<span data-ttu-id="c98c3-186">In order to make calls to an API, developers must first subscribe to a product that gives them access to it.</span><span class="sxs-lookup"><span data-stu-id="c98c3-186">In order to make calls to an API, developers must first subscribe to a product that gives them access to it.</span></span> <span data-ttu-id="c98c3-187">Developers can subscribe to products in the developer portal, or administrators can subscribe developers to products in the publisher portal.</span><span class="sxs-lookup"><span data-stu-id="c98c3-187">Developers can subscribe to products in the developer portal, or administrators can subscribe developers to products in the publisher portal.</span></span> <span data-ttu-id="c98c3-188">You are an administrator since you created the API Management instance in the previous steps in the tutorial, so you are already subscribed to every product by default.</span><span class="sxs-lookup"><span data-stu-id="c98c3-188">You are an administrator since you created the API Management instance in the previous steps in the tutorial, so you are already subscribed to every product by default.</span></span>

## <span data-ttu-id="c98c3-189"><a name="call-operation"> </a>Call an operation from the developer portal</span><span class="sxs-lookup"><span data-stu-id="c98c3-189"><a name="call-operation"> </a>Call an operation from the developer portal</span></span>
<span data-ttu-id="c98c3-190">Operations can be called directly from the developer portal, which provides a convenient way to view and test the operations of an API.</span><span class="sxs-lookup"><span data-stu-id="c98c3-190">Operations can be called directly from the developer portal, which provides a convenient way to view and test the operations of an API.</span></span> <span data-ttu-id="c98c3-191">In this tutorial step, you will call the Basic Calculator API's **Add two integers** operation.</span><span class="sxs-lookup"><span data-stu-id="c98c3-191">In this tutorial step, you will call the Basic Calculator API's **Add two integers** operation.</span></span> <span data-ttu-id="c98c3-192">Click **Developer portal** from the menu at the top right of the publisher portal.</span><span class="sxs-lookup"><span data-stu-id="c98c3-192">Click **Developer portal** from the menu at the top right of the publisher portal.</span></span>

![Developer portal][api-management-developer-portal-menu]

<span data-ttu-id="c98c3-194">Click **APIs** from the top menu, and then click **Basic Calculator** to see the available operations.</span><span class="sxs-lookup"><span data-stu-id="c98c3-194">Click **APIs** from the top menu, and then click **Basic Calculator** to see the available operations.</span></span>

![Developer portal][api-management-developer-portal-calc-api]

<span data-ttu-id="c98c3-196">Note the sample descriptions and parameters that were imported along with the API and operations, providing documentation for the developers that will use this operation.</span><span class="sxs-lookup"><span data-stu-id="c98c3-196">Note the sample descriptions and parameters that were imported along with the API and operations, providing documentation for the developers that will use this operation.</span></span> <span data-ttu-id="c98c3-197">These descriptions can also be added when operations are added manually.</span><span class="sxs-lookup"><span data-stu-id="c98c3-197">These descriptions can also be added when operations are added manually.</span></span>

<span data-ttu-id="c98c3-198">To call the **Add two integers** operation, click **Try it**.</span><span class="sxs-lookup"><span data-stu-id="c98c3-198">To call the **Add two integers** operation, click **Try it**.</span></span>

![Try it][api-management-developer-portal-calc-api-console]

<span data-ttu-id="c98c3-200">You can enter some values for the parameters or keep the defaults, and then click **Send**.</span><span class="sxs-lookup"><span data-stu-id="c98c3-200">You can enter some values for the parameters or keep the defaults, and then click **Send**.</span></span>

![HTTP Get][api-management-invoke-get]

<span data-ttu-id="c98c3-202">After an operation is invoked, the developer portal displays the **Response status**, the **Response headers**, and any **Response content**.</span><span class="sxs-lookup"><span data-stu-id="c98c3-202">After an operation is invoked, the developer portal displays the **Response status**, the **Response headers**, and any **Response content**.</span></span>

![Response][api-management-invoke-get-response]

## <span data-ttu-id="c98c3-204"><a name="view-analytics"> </a>View analytics</span><span class="sxs-lookup"><span data-stu-id="c98c3-204"><a name="view-analytics"> </a>View analytics</span></span>
<span data-ttu-id="c98c3-205">To view analytics for Basic Calculator, switch back to the publisher portal by selecting **Manage** from the menu at the top right of the developer portal.</span><span class="sxs-lookup"><span data-stu-id="c98c3-205">To view analytics for Basic Calculator, switch back to the publisher portal by selecting **Manage** from the menu at the top right of the developer portal.</span></span>

![Manage][api-management-manage-menu]

<span data-ttu-id="c98c3-207">The default view for the publisher portal is the **Dashboard**, which provides an overview of your API Management instance.</span><span class="sxs-lookup"><span data-stu-id="c98c3-207">The default view for the publisher portal is the **Dashboard**, which provides an overview of your API Management instance.</span></span>

![Dashboard][api-management-dashboard]

<span data-ttu-id="c98c3-209">Hover the mouse over the chart for **Basic Calculator** to see the specific metrics for the usage of the API for a given time period.</span><span class="sxs-lookup"><span data-stu-id="c98c3-209">Hover the mouse over the chart for **Basic Calculator** to see the specific metrics for the usage of the API for a given time period.</span></span>

> [!NOTE]
> <span data-ttu-id="c98c3-210">If you don't see any lines on your chart, switch back to the developer portal and make some calls into the API, wait a few moments, and then come back to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="c98c3-210">If you don't see any lines on your chart, switch back to the developer portal and make some calls into the API, wait a few moments, and then come back to the dashboard.</span></span>
> 
> 

<span data-ttu-id="c98c3-211">Click **View Details** to view the summary page for the API, including a larger version of the displayed metrics.</span><span class="sxs-lookup"><span data-stu-id="c98c3-211">Click **View Details** to view the summary page for the API, including a larger version of the displayed metrics.</span></span>

![Analytics][api-management-mouse-over]

![Summary][api-management-api-summary-metrics]

<span data-ttu-id="c98c3-214">For detailed metrics and reports, click **Analytics** from the **API Management** menu on the left.</span><span class="sxs-lookup"><span data-stu-id="c98c3-214">For detailed metrics and reports, click **Analytics** from the **API Management** menu on the left.</span></span>

![Overview][api-management-analytics-overview]

<span data-ttu-id="c98c3-216">The **Analytics** section has the following four tabs:</span><span class="sxs-lookup"><span data-stu-id="c98c3-216">The **Analytics** section has the following four tabs:</span></span>

* <span data-ttu-id="c98c3-217">**At a glance** provides overall usage and health metrics, as well as the top developers, top products, top APIs, and top operations.</span><span class="sxs-lookup"><span data-stu-id="c98c3-217">**At a glance** provides overall usage and health metrics, as well as the top developers, top products, top APIs, and top operations.</span></span>
* <span data-ttu-id="c98c3-218">**Usage** provides an in-depth look at API calls and bandwidth, including a geographical representation.</span><span class="sxs-lookup"><span data-stu-id="c98c3-218">**Usage** provides an in-depth look at API calls and bandwidth, including a geographical representation.</span></span>
* <span data-ttu-id="c98c3-219">**Health** focuses on status codes, cache success rates, response times, and API and service response times.</span><span class="sxs-lookup"><span data-stu-id="c98c3-219">**Health** focuses on status codes, cache success rates, response times, and API and service response times.</span></span>
* <span data-ttu-id="c98c3-220">**Activity** provides reports that drill down on the specific activity by developer, product, API, and operation.</span><span class="sxs-lookup"><span data-stu-id="c98c3-220">**Activity** provides reports that drill down on the specific activity by developer, product, API, and operation.</span></span>

## <span data-ttu-id="c98c3-221"><a name="next-steps"> </a>Next steps</span><span class="sxs-lookup"><span data-stu-id="c98c3-221"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="c98c3-222">Learn how to [Protect your API with rate limits](api-management-howto-product-with-rules.md).</span><span class="sxs-lookup"><span data-stu-id="c98c3-222">Learn how to [Protect your API with rate limits](api-management-howto-product-with-rules.md).</span></span>

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add the new API to a product]: #add-api-to-product
[Subscribe to the product that contains the API]: #subscribe
[Call an operation from the Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How to manage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How to configure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png



























