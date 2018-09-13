---
title: Azure API Management overview and key concepts | Microsoft Docs
description: Learn about APIs, products, roles, groups, and other API Management key concepts.
services: api-management
documentationcenter: ''
author: steved0x
manager: erikre
editor: ''
ms.assetid: e71da405-835a-48f3-956f-45c1a85698d7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 47358c6c209488d7a12e8afbf7a2d9b3f872f0de
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552356"
---
# <a name="what-is-api-management"></a><span data-ttu-id="5da22-103">What is API Management?</span><span class="sxs-lookup"><span data-stu-id="5da22-103">What is API Management?</span></span>
<span data-ttu-id="5da22-104">API Management helps organizations publish APIs to external, partner and internal developers to unlock the potential of their data and services.</span><span class="sxs-lookup"><span data-stu-id="5da22-104">API Management helps organizations publish APIs to external, partner and internal developers to unlock the potential of their data and services.</span></span> <span data-ttu-id="5da22-105">Businesses everywhere are looking to extend their operations as a digital platform, creating new channels, finding new customers and driving deeper engagement with existing ones.</span><span class="sxs-lookup"><span data-stu-id="5da22-105">Businesses everywhere are looking to extend their operations as a digital platform, creating new channels, finding new customers and driving deeper engagement with existing ones.</span></span> <span data-ttu-id="5da22-106">API Management provides the core competencies to ensure a successful API program through developer engagement, business insights, analytics, security and protection.</span><span class="sxs-lookup"><span data-stu-id="5da22-106">API Management provides the core competencies to ensure a successful API program through developer engagement, business insights, analytics, security and protection.</span></span>

<span data-ttu-id="5da22-107">Watch the following video for an overview of Azure API Management and learn how to use API Management to add many features to your API, including access control, rate limiting, monitoring, event logging, and response caching, with minimal work on your part.</span><span class="sxs-lookup"><span data-stu-id="5da22-107">Watch the following video for an overview of Azure API Management and learn how to use API Management to add many features to your API, including access control, rate limiting, monitoring, event logging, and response caching, with minimal work on your part.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-API-Management-Overview/player]
> 
> 

<span data-ttu-id="5da22-108">To use API Management, administrators create APIs.</span><span class="sxs-lookup"><span data-stu-id="5da22-108">To use API Management, administrators create APIs.</span></span> <span data-ttu-id="5da22-109">Each API consists of one or more operations, and each API can be added to one or more products.</span><span class="sxs-lookup"><span data-stu-id="5da22-109">Each API consists of one or more operations, and each API can be added to one or more products.</span></span> <span data-ttu-id="5da22-110">To use an API, developers subscribe to a product that contains that API, and then they can call the API's operation, subject to any usage policies that may be in effect.</span><span class="sxs-lookup"><span data-stu-id="5da22-110">To use an API, developers subscribe to a product that contains that API, and then they can call the API's operation, subject to any usage policies that may be in effect.</span></span>

<span data-ttu-id="5da22-111">This topic provides an overview of API Management key concepts.</span><span class="sxs-lookup"><span data-stu-id="5da22-111">This topic provides an overview of API Management key concepts.</span></span>

> [!NOTE]
> <span data-ttu-id="5da22-112">For more information, see the [Cloud-based API Management: Harnessing the Power of APIs](http://j.mp/ms-apim-whitepaper) PDF whitepaper.</span><span class="sxs-lookup"><span data-stu-id="5da22-112">For more information, see the [Cloud-based API Management: Harnessing the Power of APIs](http://j.mp/ms-apim-whitepaper) PDF whitepaper.</span></span> <span data-ttu-id="5da22-113">This introductory whitepaper on API Management by CITO Research covers:</span><span class="sxs-lookup"><span data-stu-id="5da22-113">This introductory whitepaper on API Management by CITO Research covers:</span></span> 
> 
> * <span data-ttu-id="5da22-114">Common API requirements and challenges</span><span class="sxs-lookup"><span data-stu-id="5da22-114">Common API requirements and challenges</span></span>
> * <span data-ttu-id="5da22-115">Decoupling APIs and presenting facades</span><span class="sxs-lookup"><span data-stu-id="5da22-115">Decoupling APIs and presenting facades</span></span>
> * <span data-ttu-id="5da22-116">Getting developers up and running quickly</span><span class="sxs-lookup"><span data-stu-id="5da22-116">Getting developers up and running quickly</span></span>
> * <span data-ttu-id="5da22-117">Securing access</span><span class="sxs-lookup"><span data-stu-id="5da22-117">Securing access</span></span>
> * <span data-ttu-id="5da22-118">Analytics and metrics</span><span class="sxs-lookup"><span data-stu-id="5da22-118">Analytics and metrics</span></span>
> * <span data-ttu-id="5da22-119">Gaining control and insight with an API Management platform</span><span class="sxs-lookup"><span data-stu-id="5da22-119">Gaining control and insight with an API Management platform</span></span>
> * <span data-ttu-id="5da22-120">Using cloud vs on-premises solutions</span><span class="sxs-lookup"><span data-stu-id="5da22-120">Using cloud vs on-premises solutions</span></span>
> * <span data-ttu-id="5da22-121">Azure API Management</span><span class="sxs-lookup"><span data-stu-id="5da22-121">Azure API Management</span></span>
> 
> 

## <span data-ttu-id="5da22-122"><a name="apis"> </a>APIs and operations</span><span class="sxs-lookup"><span data-stu-id="5da22-122"><a name="apis"> </a>APIs and operations</span></span>
<span data-ttu-id="5da22-123">APIs are the foundation of an API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="5da22-123">APIs are the foundation of an API Management service instance.</span></span> <span data-ttu-id="5da22-124">Each API represents  a set of operations available to developers.</span><span class="sxs-lookup"><span data-stu-id="5da22-124">Each API represents  a set of operations available to developers.</span></span> <span data-ttu-id="5da22-125">Each API contains a reference to the back-end service that implements the API, and its operations map to the operations implemented by the back-end service.</span><span class="sxs-lookup"><span data-stu-id="5da22-125">Each API contains a reference to the back-end service that implements the API, and its operations map to the operations implemented by the back-end service.</span></span> <span data-ttu-id="5da22-126">Operations in API Management are highly configurable, with control over URL mapping, query and path parameters, request and response content, and operation response caching.</span><span class="sxs-lookup"><span data-stu-id="5da22-126">Operations in API Management are highly configurable, with control over URL mapping, query and path parameters, request and response content, and operation response caching.</span></span> <span data-ttu-id="5da22-127">Rate limit, quotas, and IP restriction policies can also be implemented at the API or individual operation level.</span><span class="sxs-lookup"><span data-stu-id="5da22-127">Rate limit, quotas, and IP restriction policies can also be implemented at the API or individual operation level.</span></span>

<span data-ttu-id="5da22-128">For more information, see [How to create APIs][How to create APIs] and [How to add operations to an API][How to add operations to an API].</span><span class="sxs-lookup"><span data-stu-id="5da22-128">For more information, see [How to create APIs][How to create APIs] and [How to add operations to an API][How to add operations to an API].</span></span>

## <span data-ttu-id="5da22-129"><a name="products"> </a> Products</span><span class="sxs-lookup"><span data-stu-id="5da22-129"><a name="products"> </a> Products</span></span>
<span data-ttu-id="5da22-130">Products are how APIs are surfaced to developers.</span><span class="sxs-lookup"><span data-stu-id="5da22-130">Products are how APIs are surfaced to developers.</span></span> <span data-ttu-id="5da22-131">Products in API Management have one or more APIs, and are configured with a title, description, and terms of use.</span><span class="sxs-lookup"><span data-stu-id="5da22-131">Products in API Management have one or more APIs, and are configured with a title, description, and terms of use.</span></span> <span data-ttu-id="5da22-132">Products can be **Open** or **Protected**.</span><span class="sxs-lookup"><span data-stu-id="5da22-132">Products can be **Open** or **Protected**.</span></span> <span data-ttu-id="5da22-133">Protected products must be subscribed to before they can be used, while open products can be used without a subscription.</span><span class="sxs-lookup"><span data-stu-id="5da22-133">Protected products must be subscribed to before they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="5da22-134">When a product is ready for use by developers it can be published.</span><span class="sxs-lookup"><span data-stu-id="5da22-134">When a product is ready for use by developers it can be published.</span></span> <span data-ttu-id="5da22-135">Once it is published, it can be viewed (and in the case of protected products subscribed to) by developers.</span><span class="sxs-lookup"><span data-stu-id="5da22-135">Once it is published, it can be viewed (and in the case of protected products subscribed to) by developers.</span></span> <span data-ttu-id="5da22-136">Subscription approval is configured at the product level and can either require administrator approval, or be auto-approved.</span><span class="sxs-lookup"><span data-stu-id="5da22-136">Subscription approval is configured at the product level and can either require administrator approval, or be auto-approved.</span></span>

<span data-ttu-id="5da22-137">Groups are used to manage the visibility of products to developers.</span><span class="sxs-lookup"><span data-stu-id="5da22-137">Groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="5da22-138">Products grant visibility to groups, and developers can view and subscribe to the products that are visible to the groups in which they belong.</span><span class="sxs-lookup"><span data-stu-id="5da22-138">Products grant visibility to groups, and developers can view and subscribe to the products that are visible to the groups in which they belong.</span></span> 

<span data-ttu-id="5da22-139">For more information, see [How to create and publish a product][How to create and publish a product] and the following video.</span><span class="sxs-lookup"><span data-stu-id="5da22-139">For more information, see [How to create and publish a product][How to create and publish a product] and the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

## <span data-ttu-id="5da22-140"><a name="groups"> </a> Groups</span><span class="sxs-lookup"><span data-stu-id="5da22-140"><a name="groups"> </a> Groups</span></span>
<span data-ttu-id="5da22-141">Groups are used to manage the visibility of products to developers.</span><span class="sxs-lookup"><span data-stu-id="5da22-141">Groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="5da22-142">API Management has the following immutable system groups.</span><span class="sxs-lookup"><span data-stu-id="5da22-142">API Management has the following immutable system groups.</span></span>

* <span data-ttu-id="5da22-143">**Administrators** - Azure subscription administrators are members of this group.</span><span class="sxs-lookup"><span data-stu-id="5da22-143">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="5da22-144">Administrators manage API Management service instances, creating the APIs, operations, and products that are used by developers.</span><span class="sxs-lookup"><span data-stu-id="5da22-144">Administrators manage API Management service instances, creating the APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="5da22-145">**Developers** - Authenticated developer portal users fall into this group.</span><span class="sxs-lookup"><span data-stu-id="5da22-145">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="5da22-146">Developers are the customers that build applications using your APIs.</span><span class="sxs-lookup"><span data-stu-id="5da22-146">Developers are the customers that build applications using your APIs.</span></span> <span data-ttu-id="5da22-147">Developers are granted access to the developer portal and build applications that call the operations of an API.</span><span class="sxs-lookup"><span data-stu-id="5da22-147">Developers are granted access to the developer portal and build applications that call the operations of an API.</span></span>
* <span data-ttu-id="5da22-148">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting the developer portal of an API Management instance fall into this group.</span><span class="sxs-lookup"><span data-stu-id="5da22-148">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting the developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="5da22-149">They can be granted certain read-only access, such as the ability to view APIs but not call them.</span><span class="sxs-lookup"><span data-stu-id="5da22-149">They can be granted certain read-only access, such as the ability to view APIs but not call them.</span></span>

<span data-ttu-id="5da22-150">In addition to these system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants](api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group).</span><span class="sxs-lookup"><span data-stu-id="5da22-150">In addition to these system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants](api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group).</span></span> <span data-ttu-id="5da22-151">Custom and external groups can be used alongside system groups in giving developers visibility and access to API products.</span><span class="sxs-lookup"><span data-stu-id="5da22-151">Custom and external groups can be used alongside system groups in giving developers visibility and access to API products.</span></span> <span data-ttu-id="5da22-152">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access to the APIs from a product containing relevant APIs only.</span><span class="sxs-lookup"><span data-stu-id="5da22-152">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access to the APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="5da22-153">A user can be a member of more than one group.</span><span class="sxs-lookup"><span data-stu-id="5da22-153">A user can be a member of more than one group.</span></span>

<span data-ttu-id="5da22-154">For more information, see  [How to create and use groups][How to create and use groups].</span><span class="sxs-lookup"><span data-stu-id="5da22-154">For more information, see  [How to create and use groups][How to create and use groups].</span></span>

## <span data-ttu-id="5da22-155"><a name="developers"> </a> Developers</span><span class="sxs-lookup"><span data-stu-id="5da22-155"><a name="developers"> </a> Developers</span></span>
<span data-ttu-id="5da22-156">Developers represent the user accounts in an API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="5da22-156">Developers represent the user accounts in an API Management service instance.</span></span> <span data-ttu-id="5da22-157">Developers can be created or invited to join by administrators, or they can sign up from the [Developer portal][Developer portal].</span><span class="sxs-lookup"><span data-stu-id="5da22-157">Developers can be created or invited to join by administrators, or they can sign up from the [Developer portal][Developer portal].</span></span> <span data-ttu-id="5da22-158">Each developer is a member of one or more groups, and can be subscribe to the products that grant visibility to those groups.</span><span class="sxs-lookup"><span data-stu-id="5da22-158">Each developer is a member of one or more groups, and can be subscribe to the products that grant visibility to those groups.</span></span>

<span data-ttu-id="5da22-159">When developers subscribe to a product they are granted the primary and secondary key for the product.</span><span class="sxs-lookup"><span data-stu-id="5da22-159">When developers subscribe to a product they are granted the primary and secondary key for the product.</span></span> <span data-ttu-id="5da22-160">This key is used when making calls into the product's APIs.</span><span class="sxs-lookup"><span data-stu-id="5da22-160">This key is used when making calls into the product's APIs.</span></span>

<span data-ttu-id="5da22-161">For more information, see [How to create or invite developers][How to create or invite developers] and [How to associate groups with developers][How to associate groups with developers].</span><span class="sxs-lookup"><span data-stu-id="5da22-161">For more information, see [How to create or invite developers][How to create or invite developers] and [How to associate groups with developers][How to associate groups with developers].</span></span>

## <span data-ttu-id="5da22-162"><a name="policies"> </a> Policies</span><span class="sxs-lookup"><span data-stu-id="5da22-162"><a name="policies"> </a> Policies</span></span>
<span data-ttu-id="5da22-163">Policies are a powerful capability of API Management that allow the publisher to change the behavior of the API through configuration.</span><span class="sxs-lookup"><span data-stu-id="5da22-163">Policies are a powerful capability of API Management that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="5da22-164">Policies are a collection of statements that are executed sequentially on the request or response of an API.</span><span class="sxs-lookup"><span data-stu-id="5da22-164">Policies are a collection of statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="5da22-165">Popular statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer, and many other policies are available.</span><span class="sxs-lookup"><span data-stu-id="5da22-165">Popular statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer, and many other policies are available.</span></span>

<span data-ttu-id="5da22-166">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span><span class="sxs-lookup"><span data-stu-id="5da22-166">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="5da22-167">Some policies such as the [Control flow](https://msdn.microsoft.com/library/azure/dn894085.aspx#choose) and [Set variable](https://msdn.microsoft.com/library/azure/dn894085.aspx#set-variable) policies are based on policy expressions.</span><span class="sxs-lookup"><span data-stu-id="5da22-167">Some policies such as the [Control flow](https://msdn.microsoft.com/library/azure/dn894085.aspx#choose) and [Set variable](https://msdn.microsoft.com/library/azure/dn894085.aspx#set-variable) policies are based on policy expressions.</span></span> <span data-ttu-id="5da22-168">For more information, see [Advanced policies](https://msdn.microsoft.com/library/azure/dn894085.aspx#AdvancedPolicies), [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx), and watch the following video.</span><span class="sxs-lookup"><span data-stu-id="5da22-168">For more information, see [Advanced policies](https://msdn.microsoft.com/library/azure/dn894085.aspx#AdvancedPolicies), [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx), and watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

<span data-ttu-id="5da22-169">For a complete list of API Management policies, see [Policy reference][Policy reference].</span><span class="sxs-lookup"><span data-stu-id="5da22-169">For a complete list of API Management policies, see [Policy reference][Policy reference].</span></span> <span data-ttu-id="5da22-170">For more information on using and configuring policies, see [API Management policies][API Management policies].</span><span class="sxs-lookup"><span data-stu-id="5da22-170">For more information on using and configuring policies, see [API Management policies][API Management policies].</span></span> <span data-ttu-id="5da22-171">For a tutorial on creating a product with rate limit and quota policies, see [How create and configure advanced product settings][How create and configure advanced product settings].</span><span class="sxs-lookup"><span data-stu-id="5da22-171">For a tutorial on creating a product with rate limit and quota policies, see [How create and configure advanced product settings][How create and configure advanced product settings].</span></span> <span data-ttu-id="5da22-172">For a demo, see the following video.</span><span class="sxs-lookup"><span data-stu-id="5da22-172">For a demo, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

## <span data-ttu-id="5da22-173"><a name="developer-portal"> </a> Developer portal</span><span class="sxs-lookup"><span data-stu-id="5da22-173"><a name="developer-portal"> </a> Developer portal</span></span>
<span data-ttu-id="5da22-174">The developer portal is where developers can learn about your APIs, view and call operations, and subscribe to products.</span><span class="sxs-lookup"><span data-stu-id="5da22-174">The developer portal is where developers can learn about your APIs, view and call operations, and subscribe to products.</span></span> <span data-ttu-id="5da22-175">Prospective customers can visit the developer portal, view APIs and operations, and sign up.</span><span class="sxs-lookup"><span data-stu-id="5da22-175">Prospective customers can visit the developer portal, view APIs and operations, and sign up.</span></span> <span data-ttu-id="5da22-176">The URL for your developer portal is located on the dashboard in the Azure Classic Portal for your API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="5da22-176">The URL for your developer portal is located on the dashboard in the Azure Classic Portal for your API Management service instance.</span></span>

<span data-ttu-id="5da22-177">You can customize the look and feel of your developer portal by adding custom content, customizing styles, and adding your branding.</span><span class="sxs-lookup"><span data-stu-id="5da22-177">You can customize the look and feel of your developer portal by adding custom content, customizing styles, and adding your branding.</span></span>

## <a name="api-management-and-the-api-economy"></a><span data-ttu-id="5da22-178">API Management and the API economy</span><span class="sxs-lookup"><span data-stu-id="5da22-178">API Management and the API economy</span></span>
<span data-ttu-id="5da22-179">To learn more about API Management, watch the following presentation from the Microsoft Ignite 2015 conference.</span><span class="sxs-lookup"><span data-stu-id="5da22-179">To learn more about API Management, watch the following presentation from the Microsoft Ignite 2015 conference.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3708/player]
> 
> 

[APIs and operations]: #apis
[Products]: #products
[Groups]: #groups
[Developers]: #developers
[Policies]: #policies
[Developer portal]: #developer-portal

[How to create APIs]: api-management-howto-create-apis.md
[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer
[How create and configure advanced product settings]: api-management-howto-product-with-rules.md
[How to create or invite developers]: api-management-howto-create-or-invite-developers.md
[Policy reference]: api-management-policy-reference.md
[API Management policies]: api-management-howto-policies.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance




