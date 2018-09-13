---
title: Advanced request throttling with Azure API Management
description: Learn how to create and apply flexible quota and rate limiting policies with Azure API Management.
services: api-management
documentationcenter: ''
author: vladvino
manager: erikre
editor: ''
ms.assetid: fc813a65-7793-4c17-8bb9-e387838193ae
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2018
ms.author: apimpm
ms.openlocfilehash: c7fcbd57021134631e9f10dcbb2d40e4c130af02
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44783827"
---
# <a name="advanced-request-throttling-with-azure-api-management"></a><span data-ttu-id="f6434-103">Advanced request throttling with Azure API Management</span><span class="sxs-lookup"><span data-stu-id="f6434-103">Advanced request throttling with Azure API Management</span></span>
<span data-ttu-id="f6434-104">Being able to throttle incoming requests is a key role of Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="f6434-104">Being able to throttle incoming requests is a key role of Azure API Management.</span></span> <span data-ttu-id="f6434-105">Either by controlling the rate of requests or the total requests/data transferred, API Management allows API providers to protect their APIs from abuse and create value for different API product tiers.</span><span class="sxs-lookup"><span data-stu-id="f6434-105">Either by controlling the rate of requests or the total requests/data transferred, API Management allows API providers to protect their APIs from abuse and create value for different API product tiers.</span></span>

## <a name="product-based-throttling"></a><span data-ttu-id="f6434-106">Product-based throttling</span><span class="sxs-lookup"><span data-stu-id="f6434-106">Product-based throttling</span></span>
<span data-ttu-id="f6434-107">To date, the rate throttling capabilities have been limited to being scoped to a particular Product subscription, defined in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f6434-107">To date, the rate throttling capabilities have been limited to being scoped to a particular Product subscription, defined in the Azure portal.</span></span> <span data-ttu-id="f6434-108">This is useful for the API provider to apply limits on the developers who have signed up to use their API, however, it does not help, for example, in throttling individual end users of the API.</span><span class="sxs-lookup"><span data-stu-id="f6434-108">This is useful for the API provider to apply limits on the developers who have signed up to use their API, however, it does not help, for example, in throttling individual end users of the API.</span></span> <span data-ttu-id="f6434-109">It is possible that for single user of the developer's application to consume the entire quota and then prevent other customers of the developer from being able to use the application.</span><span class="sxs-lookup"><span data-stu-id="f6434-109">It is possible that for single user of the developer's application to consume the entire quota and then prevent other customers of the developer from being able to use the application.</span></span> <span data-ttu-id="f6434-110">Also, several customers who might generate a high volume of requests may limit access to occasional users.</span><span class="sxs-lookup"><span data-stu-id="f6434-110">Also, several customers who might generate a high volume of requests may limit access to occasional users.</span></span>

## <a name="custom-key-based-throttling"></a><span data-ttu-id="f6434-111">Custom key based throttling</span><span class="sxs-lookup"><span data-stu-id="f6434-111">Custom key based throttling</span></span>
<span data-ttu-id="f6434-112">The new [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies provide a more flexible solution to traffic control.</span><span class="sxs-lookup"><span data-stu-id="f6434-112">The new [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies provide a more flexible solution to traffic control.</span></span> <span data-ttu-id="f6434-113">These new policies allow you to define expressions to identify the keys that are used to track traffic usage.</span><span class="sxs-lookup"><span data-stu-id="f6434-113">These new policies allow you to define expressions to identify the keys that are used to track traffic usage.</span></span> <span data-ttu-id="f6434-114">The way this works is easiest illustrated with an example.</span><span class="sxs-lookup"><span data-stu-id="f6434-114">The way this works is easiest illustrated with an example.</span></span> 

## <a name="ip-address-throttling"></a><span data-ttu-id="f6434-115">IP Address throttling</span><span class="sxs-lookup"><span data-stu-id="f6434-115">IP Address throttling</span></span>
<span data-ttu-id="f6434-116">The following policies restrict a single client IP address to only 10 calls every minute, with a total of 1,000,000 calls and 10,000 kilobytes of bandwidth per month.</span><span class="sxs-lookup"><span data-stu-id="f6434-116">The following policies restrict a single client IP address to only 10 calls every minute, with a total of 1,000,000 calls and 10,000 kilobytes of bandwidth per month.</span></span> 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

<span data-ttu-id="f6434-117">If all clients on the Internet used a unique IP address, this might be an effective way of limiting usage by user.</span><span class="sxs-lookup"><span data-stu-id="f6434-117">If all clients on the Internet used a unique IP address, this might be an effective way of limiting usage by user.</span></span> <span data-ttu-id="f6434-118">However, it is likely that multiple users are sharing a single public IP address due to them accessing the Internet via a NAT device.</span><span class="sxs-lookup"><span data-stu-id="f6434-118">However, it is likely that multiple users are sharing a single public IP address due to them accessing the Internet via a NAT device.</span></span> <span data-ttu-id="f6434-119">Despite this, for APIs that allow unauthenticated access the `IpAddress` might be the best option.</span><span class="sxs-lookup"><span data-stu-id="f6434-119">Despite this, for APIs that allow unauthenticated access the `IpAddress` might be the best option.</span></span>

## <a name="user-identity-throttling"></a><span data-ttu-id="f6434-120">User identity throttling</span><span class="sxs-lookup"><span data-stu-id="f6434-120">User identity throttling</span></span>
<span data-ttu-id="f6434-121">If an end user is authenticated, then a throttling key can be generated based on information that uniquely identifies that user.</span><span class="sxs-lookup"><span data-stu-id="f6434-121">If an end user is authenticated, then a throttling key can be generated based on information that uniquely identifies that user.</span></span>

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

<span data-ttu-id="f6434-122">This example shows how to extract the Authorization header, convert it to `JWT` object and use the subject of the token to identify the user and use that as the rate limiting key.</span><span class="sxs-lookup"><span data-stu-id="f6434-122">This example shows how to extract the Authorization header, convert it to `JWT` object and use the subject of the token to identify the user and use that as the rate limiting key.</span></span> <span data-ttu-id="f6434-123">If the user identity is stored in the `JWT` as one of the other claims, then that value could be used in its place.</span><span class="sxs-lookup"><span data-stu-id="f6434-123">If the user identity is stored in the `JWT` as one of the other claims, then that value could be used in its place.</span></span>

## <a name="combined-policies"></a><span data-ttu-id="f6434-124">Combined policies</span><span class="sxs-lookup"><span data-stu-id="f6434-124">Combined policies</span></span>
<span data-ttu-id="f6434-125">Although the new throttling policies provide more control than the existing throttling policies, there is still value combining both capabilities.</span><span class="sxs-lookup"><span data-stu-id="f6434-125">Although the new throttling policies provide more control than the existing throttling policies, there is still value combining both capabilities.</span></span> <span data-ttu-id="f6434-126">Throttling by product subscription key ([Limit call rate by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) is a great way to enable monetizing of an API by charging based on usage levels.</span><span class="sxs-lookup"><span data-stu-id="f6434-126">Throttling by product subscription key ([Limit call rate by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) is a great way to enable monetizing of an API by charging based on usage levels.</span></span> <span data-ttu-id="f6434-127">The finer grained control of being able to throttle by user is complementary and prevents one user's behavior from degrading the experience of another.</span><span class="sxs-lookup"><span data-stu-id="f6434-127">The finer grained control of being able to throttle by user is complementary and prevents one user's behavior from degrading the experience of another.</span></span> 

## <a name="client-driven-throttling"></a><span data-ttu-id="f6434-128">Client driven throttling</span><span class="sxs-lookup"><span data-stu-id="f6434-128">Client driven throttling</span></span>
<span data-ttu-id="f6434-129">When the throttling key is defined using a [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx), then it is the API provider that is choosing how the throttling is scoped.</span><span class="sxs-lookup"><span data-stu-id="f6434-129">When the throttling key is defined using a [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx), then it is the API provider that is choosing how the throttling is scoped.</span></span> <span data-ttu-id="f6434-130">However, a developer might want to control how they rate limit their own customers.</span><span class="sxs-lookup"><span data-stu-id="f6434-130">However, a developer might want to control how they rate limit their own customers.</span></span> <span data-ttu-id="f6434-131">This could be enabled by the API provider by introducing a custom header to allow the developer's client application to communicate the key to the API.</span><span class="sxs-lookup"><span data-stu-id="f6434-131">This could be enabled by the API provider by introducing a custom header to allow the developer's client application to communicate the key to the API.</span></span>

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

<span data-ttu-id="f6434-132">This enables the developer's client application to choose how they want to create the rate limiting key.</span><span class="sxs-lookup"><span data-stu-id="f6434-132">This enables the developer's client application to choose how they want to create the rate limiting key.</span></span> <span data-ttu-id="f6434-133">The client developers could create their own rate tiers by allocating sets of keys to users and rotating the key usage.</span><span class="sxs-lookup"><span data-stu-id="f6434-133">The client developers could create their own rate tiers by allocating sets of keys to users and rotating the key usage.</span></span>

## <a name="summary"></a><span data-ttu-id="f6434-134">Summary</span><span class="sxs-lookup"><span data-stu-id="f6434-134">Summary</span></span>
<span data-ttu-id="f6434-135">Azure API Management provides rate and quote throttling to both protect and add value to your API service.</span><span class="sxs-lookup"><span data-stu-id="f6434-135">Azure API Management provides rate and quote throttling to both protect and add value to your API service.</span></span> <span data-ttu-id="f6434-136">The new throttling policies with custom scoping rules allow you finer grained control over those policies to enable your customers to build even better applications.</span><span class="sxs-lookup"><span data-stu-id="f6434-136">The new throttling policies with custom scoping rules allow you finer grained control over those policies to enable your customers to build even better applications.</span></span> <span data-ttu-id="f6434-137">The examples in this article demonstrate the use of these new policies by manufacturing rate limiting keys with client IP addresses, user identity, and client generated values.</span><span class="sxs-lookup"><span data-stu-id="f6434-137">The examples in this article demonstrate the use of these new policies by manufacturing rate limiting keys with client IP addresses, user identity, and client generated values.</span></span> <span data-ttu-id="f6434-138">However, there are many other parts of the message that could be used such as user agent, URL path fragments, message size.</span><span class="sxs-lookup"><span data-stu-id="f6434-138">However, there are many other parts of the message that could be used such as user agent, URL path fragments, message size.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6434-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="f6434-139">Next steps</span></span>
<span data-ttu-id="f6434-140">Please give us your feedback in the Disqus thread for this topic.</span><span class="sxs-lookup"><span data-stu-id="f6434-140">Please give us your feedback in the Disqus thread for this topic.</span></span> <span data-ttu-id="f6434-141">It would be great to hear about other potential key values that have been a logical choice in your scenarios.</span><span class="sxs-lookup"><span data-stu-id="f6434-141">It would be great to hear about other potential key values that have been a logical choice in your scenarios.</span></span>

