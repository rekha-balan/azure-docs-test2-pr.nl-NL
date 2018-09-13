---
title: Advanced request throttling with Azure API Management
description: Learn how to create and apply flexible quota and rate limiting policies with Azure API Management.
services: api-management
documentationcenter: ''
author: darrelmiller
manager: erikre
editor: ''
ms.assetid: fc813a65-7793-4c17-8bb9-e387838193ae
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 35375e599891a9443a91c4c3a8657e8c9c48c7b5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672390"
---
# <a name="advanced-request-throttling-with-azure-api-management"></a><span data-ttu-id="1e791-103">Advanced request throttling with Azure API Management</span><span class="sxs-lookup"><span data-stu-id="1e791-103">Advanced request throttling with Azure API Management</span></span>
<span data-ttu-id="1e791-104">Being able to throttle incoming requests is a key role of Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="1e791-104">Being able to throttle incoming requests is a key role of Azure API Management.</span></span> <span data-ttu-id="1e791-105">Either by controlling the rate of requests or the total requests/data transferred, API Management allows API providers to protect their APIs from abuse and create value for different API product tiers.</span><span class="sxs-lookup"><span data-stu-id="1e791-105">Either by controlling the rate of requests or the total requests/data transferred, API Management allows API providers to protect their APIs from abuse and create value for different API product tiers.</span></span>

## <a name="product-based-throttling"></a><span data-ttu-id="1e791-106">Product based throttling</span><span class="sxs-lookup"><span data-stu-id="1e791-106">Product based throttling</span></span>
<span data-ttu-id="1e791-107">To date, the rate throttling capabilities have been limited to being scoped to a particular Product subscription (essentially a key), defined in the API Management publisher portal.</span><span class="sxs-lookup"><span data-stu-id="1e791-107">To date, the rate throttling capabilities have been limited to being scoped to a particular Product subscription (essentially a key), defined in the API Management publisher portal.</span></span> <span data-ttu-id="1e791-108">This is useful for the API provider to apply limits on the developers who have signed up to use their API, however, it does not help, for example, in throttling individual end-users of the API.</span><span class="sxs-lookup"><span data-stu-id="1e791-108">This is useful for the API provider to apply limits on the developers who have signed up to use their API, however, it does not help, for example, in throttling individual end-users of the API.</span></span> <span data-ttu-id="1e791-109">It is possible that for single user of the developer's application to consume the entire quota and then prevent other customers of the developer from being able to use the application.</span><span class="sxs-lookup"><span data-stu-id="1e791-109">It is possible that for single user of the developer's application to consume the entire quota and then prevent other customers of the developer from being able to use the application.</span></span> <span data-ttu-id="1e791-110">Also, several customers who might generate a high volume of requests may limit access to occasional users.</span><span class="sxs-lookup"><span data-stu-id="1e791-110">Also, several customers who might generate a high volume of requests may limit access to occasional users.</span></span>

## <a name="custom-key-based-throttling"></a><span data-ttu-id="1e791-111">Custom key based throttling</span><span class="sxs-lookup"><span data-stu-id="1e791-111">Custom key based throttling</span></span>
<span data-ttu-id="1e791-112">The new [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies provide a significantly more flexible solution to traffic control.</span><span class="sxs-lookup"><span data-stu-id="1e791-112">The new [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies provide a significantly more flexible solution to traffic control.</span></span> <span data-ttu-id="1e791-113">These new policies allow you to define expressions to identify the keys that will be used to track traffic usage.</span><span class="sxs-lookup"><span data-stu-id="1e791-113">These new policies allow you to define expressions to identify the keys that will be used to track traffic usage.</span></span> <span data-ttu-id="1e791-114">The way this works is easiest illustrated with an example.</span><span class="sxs-lookup"><span data-stu-id="1e791-114">The way this works is easiest illustrated with an example.</span></span> 

## <a name="ip-address-throttling"></a><span data-ttu-id="1e791-115">IP Address throttling</span><span class="sxs-lookup"><span data-stu-id="1e791-115">IP Address throttling</span></span>
<span data-ttu-id="1e791-116">The following policies restrict a single client IP address to only 10 calls every minute, with a total of 1,000,000 calls and 10,000 kilobytes of bandwidth per month.</span><span class="sxs-lookup"><span data-stu-id="1e791-116">The following policies restrict a single client IP address to only 10 calls every minute, with a total of 1,000,000 calls and 10,000 kilobytes of bandwidth per month.</span></span> 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

<span data-ttu-id="1e791-117">If all clients on the Internet used a unique IP address, this might be an effective way of limiting usage by user.</span><span class="sxs-lookup"><span data-stu-id="1e791-117">If all clients on the Internet used a unique IP address, this might be an effective way of limiting usage by user.</span></span> <span data-ttu-id="1e791-118">However, it is quite likely that multiple users will sharing a single public IP address due to them accessing the Internet via a NAT device.</span><span class="sxs-lookup"><span data-stu-id="1e791-118">However, it is quite likely that multiple users will sharing a single public IP address due to them accessing the Internet via a NAT device.</span></span> <span data-ttu-id="1e791-119">Despite this, for APIs that allow unauthenticated access the `IpAddress` might be the best option.</span><span class="sxs-lookup"><span data-stu-id="1e791-119">Despite this, for APIs that allow unauthenticated access the `IpAddress` might be the best option.</span></span>

## <a name="user-identity-throttling"></a><span data-ttu-id="1e791-120">User identity throttling</span><span class="sxs-lookup"><span data-stu-id="1e791-120">User identity throttling</span></span>
<span data-ttu-id="1e791-121">If an end user is authenticated then a throttling key can be generated based on information that uniquely identifies an that user.</span><span class="sxs-lookup"><span data-stu-id="1e791-121">If an end user is authenticated then a throttling key can be generated based on information that uniquely identifies an that user.</span></span>

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

<span data-ttu-id="1e791-122">In this example we extract the Authorization header, convert it to `JWT` object and use the subject of the token to identify the user and use that as the rate limiting key.</span><span class="sxs-lookup"><span data-stu-id="1e791-122">In this example we extract the Authorization header, convert it to `JWT` object and use the subject of the token to identify the user and use that as the rate limiting key.</span></span> <span data-ttu-id="1e791-123">If the user identity is stored in the `JWT` as one of the other claims then that value could be used in its place.</span><span class="sxs-lookup"><span data-stu-id="1e791-123">If the user identity is stored in the `JWT` as one of the other claims then that value could be used in its place.</span></span>

## <a name="combined-policies"></a><span data-ttu-id="1e791-124">Combined policies</span><span class="sxs-lookup"><span data-stu-id="1e791-124">Combined policies</span></span>
<span data-ttu-id="1e791-125">Although the new throttling policies provide more control than the existing throttling policies, there is still value combining both capabilities.</span><span class="sxs-lookup"><span data-stu-id="1e791-125">Although the new throttling policies provide more control than the existing throttling policies, there is still value combining both capabilities.</span></span> <span data-ttu-id="1e791-126">Throttling by product subscription key ([Limit call rate by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) is a great way to enable monetizing of an API by charging based on usage levels.</span><span class="sxs-lookup"><span data-stu-id="1e791-126">Throttling by product subscription key ([Limit call rate by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) is a great way to enable monetizing of an API by charging based on usage levels.</span></span> <span data-ttu-id="1e791-127">The finer grained control of being able to throttle by user is complementary and prevents one user's behavior from degrading the experience of another.</span><span class="sxs-lookup"><span data-stu-id="1e791-127">The finer grained control of being able to throttle by user is complementary and prevents one user's behavior from degrading the experience of another.</span></span> 

## <a name="client-driven-throttling"></a><span data-ttu-id="1e791-128">Client driven throttling</span><span class="sxs-lookup"><span data-stu-id="1e791-128">Client driven throttling</span></span>
<span data-ttu-id="1e791-129">When the throttling key is defined using a [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx), then it is the API provider that is choosing how the throttling is scoped.</span><span class="sxs-lookup"><span data-stu-id="1e791-129">When the throttling key is defined using a [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx), then it is the API provider that is choosing how the throttling is scoped.</span></span> <span data-ttu-id="1e791-130">However, a developer might want to control how they rate limit their own customers.</span><span class="sxs-lookup"><span data-stu-id="1e791-130">However, a developer might want to control how they rate limit their own customers.</span></span> <span data-ttu-id="1e791-131">This could be enabled by the API provider by introducing a custom header to allow the developer's client application to communicate the key to the API.</span><span class="sxs-lookup"><span data-stu-id="1e791-131">This could be enabled by the API provider by introducing a custom header to allow the developer's client application to communicate the key to the API.</span></span>

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

<span data-ttu-id="1e791-132">This enables the developer's client application to choose how they want to create the rate limiting key.</span><span class="sxs-lookup"><span data-stu-id="1e791-132">This enables the developer's client application to choose how they want to create the rate limiting key.</span></span> <span data-ttu-id="1e791-133">With a little bit of ingenuity a client developer could create their own rate tiers by allocating sets of keys to users and rotating the key usage.</span><span class="sxs-lookup"><span data-stu-id="1e791-133">With a little bit of ingenuity a client developer could create their own rate tiers by allocating sets of keys to users and rotating the key usage.</span></span>

## <a name="summary"></a><span data-ttu-id="1e791-134">Summary</span><span class="sxs-lookup"><span data-stu-id="1e791-134">Summary</span></span>
<span data-ttu-id="1e791-135">Azure API Management provides rate and quote throttling to both protect and add value to your API service.</span><span class="sxs-lookup"><span data-stu-id="1e791-135">Azure API Management provides rate and quote throttling to both protect and add value to your API service.</span></span> <span data-ttu-id="1e791-136">The new throttling policies with custom scoping rules allow you finer grained control over those policies to enable your customers to build even better applications.</span><span class="sxs-lookup"><span data-stu-id="1e791-136">The new throttling policies with custom scoping rules allow you finer grained control over those policies to enable your customers to build even better applications.</span></span> <span data-ttu-id="1e791-137">The examples in this article demonstrate the use of these new policies by manufacturing rate limiting keys with client IP addresses, user identity, and client generated values.</span><span class="sxs-lookup"><span data-stu-id="1e791-137">The examples in this article demonstrate the use of these new policies by manufacturing rate limiting keys with client IP addresses, user identity, and client generated values.</span></span> <span data-ttu-id="1e791-138">However, there are many other parts of the message that could be used such as user agent, URL path fragments, message size.</span><span class="sxs-lookup"><span data-stu-id="1e791-138">However, there are many other parts of the message that could be used such as user agent, URL path fragments, message size.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e791-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="1e791-139">Next steps</span></span>
<span data-ttu-id="1e791-140">Please give us your feedback in the Disqus thread for this topic.</span><span class="sxs-lookup"><span data-stu-id="1e791-140">Please give us your feedback in the Disqus thread for this topic.</span></span> <span data-ttu-id="1e791-141">It would be great to hear about other potential key values that have been a logical choice in your scenarios.</span><span class="sxs-lookup"><span data-stu-id="1e791-141">It would be great to hear about other potential key values that have been a logical choice in your scenarios.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="1e791-142">Watch a video overview of these policies</span><span class="sxs-lookup"><span data-stu-id="1e791-142">Watch a video overview of these policies</span></span>
<span data-ttu-id="1e791-143">For more information on the [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies covered in this article, please watch the following video.</span><span class="sxs-lookup"><span data-stu-id="1e791-143">For more information on the [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies covered in this article, please watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

