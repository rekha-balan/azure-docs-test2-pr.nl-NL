---
title: Custom caching in Azure API Management
description: Learn how to cache items by key in Azure API Management
services: api-management
documentationcenter: ''
author: vladvino
manager: erikre
editor: ''
ms.assetid: 772bc8dd-5cda-41c4-95bf-b9f6f052bc85
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 838850d38c9df51fabcf620831371bed401e9492
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819603"
---
# <a name="custom-caching-in-azure-api-management"></a><span data-ttu-id="e0850-103">Custom caching in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="e0850-103">Custom caching in Azure API Management</span></span>
<span data-ttu-id="e0850-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using the resource URL as the key.</span><span class="sxs-lookup"><span data-stu-id="e0850-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using the resource URL as the key.</span></span> <span data-ttu-id="e0850-105">The key can be modified by request headers using the `vary-by` properties.</span><span class="sxs-lookup"><span data-stu-id="e0850-105">The key can be modified by request headers using the `vary-by` properties.</span></span> <span data-ttu-id="e0850-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful to just cache a portion of a representation.</span><span class="sxs-lookup"><span data-stu-id="e0850-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful to just cache a portion of a representation.</span></span> <span data-ttu-id="e0850-107">The new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide the ability to store and retrieve arbitrary pieces of data from within policy definitions.</span><span class="sxs-lookup"><span data-stu-id="e0850-107">The new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide the ability to store and retrieve arbitrary pieces of data from within policy definitions.</span></span> <span data-ttu-id="e0850-108">This ability also adds value to the previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span><span class="sxs-lookup"><span data-stu-id="e0850-108">This ability also adds value to the previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span></span>

## <a name="architecture"></a><span data-ttu-id="e0850-109">Architecture</span><span class="sxs-lookup"><span data-stu-id="e0850-109">Architecture</span></span>
<span data-ttu-id="e0850-110">API Management service uses a shared per-tenant data cache so that, as you scale up to multiple units you still get access to the same cached data.</span><span class="sxs-lookup"><span data-stu-id="e0850-110">API Management service uses a shared per-tenant data cache so that, as you scale up to multiple units you still get access to the same cached data.</span></span> <span data-ttu-id="e0850-111">However, when working with a multi-region deployment there are independent caches within each of the regions.</span><span class="sxs-lookup"><span data-stu-id="e0850-111">However, when working with a multi-region deployment there are independent caches within each of the regions.</span></span> <span data-ttu-id="e0850-112">It is important to not treat the cache as a data store, where it is the only source of some piece of information.</span><span class="sxs-lookup"><span data-stu-id="e0850-112">It is important to not treat the cache as a data store, where it is the only source of some piece of information.</span></span> <span data-ttu-id="e0850-113">If you did, and later decided to take advantage of the multi-region deployment, then customers with users that travel may lose access to that cached data.</span><span class="sxs-lookup"><span data-stu-id="e0850-113">If you did, and later decided to take advantage of the multi-region deployment, then customers with users that travel may lose access to that cached data.</span></span>

## <a name="fragment-caching"></a><span data-ttu-id="e0850-114">Fragment caching</span><span class="sxs-lookup"><span data-stu-id="e0850-114">Fragment caching</span></span>
<span data-ttu-id="e0850-115">There are certain cases where responses being returned contain some portion of data that is expensive to determine and yet remains fresh for a reasonable amount of time.</span><span class="sxs-lookup"><span data-stu-id="e0850-115">There are certain cases where responses being returned contain some portion of data that is expensive to determine and yet remains fresh for a reasonable amount of time.</span></span> <span data-ttu-id="e0850-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If the user is a member of the airlines points program, they would also have information relating to their current status and accumulated mileage.</span><span class="sxs-lookup"><span data-stu-id="e0850-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If the user is a member of the airlines points program, they would also have information relating to their current status and accumulated mileage.</span></span> <span data-ttu-id="e0850-117">This user-related information might be stored in a different system, but it may be desirable to include it in responses returned about flight status and reservations.</span><span class="sxs-lookup"><span data-stu-id="e0850-117">This user-related information might be stored in a different system, but it may be desirable to include it in responses returned about flight status and reservations.</span></span> <span data-ttu-id="e0850-118">This can be done using a process called fragment caching.</span><span class="sxs-lookup"><span data-stu-id="e0850-118">This can be done using a process called fragment caching.</span></span> <span data-ttu-id="e0850-119">The primary representation can be returned from the origin server using some kind of token to indicate where the user-related information is to be inserted.</span><span class="sxs-lookup"><span data-stu-id="e0850-119">The primary representation can be returned from the origin server using some kind of token to indicate where the user-related information is to be inserted.</span></span> 

<span data-ttu-id="e0850-120">Consider the following JSON response from a backend API.</span><span class="sxs-lookup"><span data-stu-id="e0850-120">Consider the following JSON response from a backend API.</span></span>

```json
{
  "airline" : "Air Canada",
  "flightno" : "871",
  "status" : "ontime",
  "gate" : "B40",
  "terminal" : "2A",
  "userprofile" : "$userprofile$"
}  
```

<span data-ttu-id="e0850-121">And secondary resource at `/userprofile/{userid}` that looks like,</span><span class="sxs-lookup"><span data-stu-id="e0850-121">And secondary resource at `/userprofile/{userid}` that looks like,</span></span>

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

<span data-ttu-id="e0850-122">To determine the appropriate user information to include, API Management needs to identify who the end user is.</span><span class="sxs-lookup"><span data-stu-id="e0850-122">To determine the appropriate user information to include, API Management needs to identify who the end user is.</span></span> <span data-ttu-id="e0850-123">This mechanism is implementation-dependent.</span><span class="sxs-lookup"><span data-stu-id="e0850-123">This mechanism is implementation-dependent.</span></span> <span data-ttu-id="e0850-124">As an example, I am using the `Subject` claim of a `JWT` token.</span><span class="sxs-lookup"><span data-stu-id="e0850-124">As an example, I am using the `Subject` claim of a `JWT` token.</span></span> 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

<span data-ttu-id="e0850-125">API Management stores the `enduserid` value in a context variable for later use.</span><span class="sxs-lookup"><span data-stu-id="e0850-125">API Management stores the `enduserid` value in a context variable for later use.</span></span> <span data-ttu-id="e0850-126">The next step is to determine if a previous request has already retrieved the user information and stored it in the cache.</span><span class="sxs-lookup"><span data-stu-id="e0850-126">The next step is to determine if a previous request has already retrieved the user information and stored it in the cache.</span></span> <span data-ttu-id="e0850-127">For this, API Management uses the `cache-lookup-value` policy.</span><span class="sxs-lookup"><span data-stu-id="e0850-127">For this, API Management uses the `cache-lookup-value` policy.</span></span>

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

<span data-ttu-id="e0850-128">If there is no entry in the cache that corresponds to the key value, then no `userprofile` context variable is created.</span><span class="sxs-lookup"><span data-stu-id="e0850-128">If there is no entry in the cache that corresponds to the key value, then no `userprofile` context variable is created.</span></span> <span data-ttu-id="e0850-129">API Management checks the success of the lookup using the `choose` control flow policy.</span><span class="sxs-lookup"><span data-stu-id="e0850-129">API Management checks the success of the lookup using the `choose` control flow policy.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If the userprofile context variable doesn’t exist, make an HTTP request to retrieve it.  -->
    </when>
</choose>
```

<span data-ttu-id="e0850-130">If the `userprofile` context variable doesn’t exist, then API Management is going to have to make an HTTP request to retrieve it.</span><span class="sxs-lookup"><span data-stu-id="e0850-130">If the `userprofile` context variable doesn’t exist, then API Management is going to have to make an HTTP request to retrieve it.</span></span>

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points to the profile for the current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="e0850-131">API Management uses the `enduserid` to construct the URL to the user profile resource.</span><span class="sxs-lookup"><span data-stu-id="e0850-131">API Management uses the `enduserid` to construct the URL to the user profile resource.</span></span> <span data-ttu-id="e0850-132">Once API Management has the response, it pulls the body text out of the response and stores it back into a context variable.</span><span class="sxs-lookup"><span data-stu-id="e0850-132">Once API Management has the response, it pulls the body text out of the response and stores it back into a context variable.</span></span>

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

<span data-ttu-id="e0850-133">To avoid API Management from making this HTTP request again, when the same user makes another request, you can specify to store the user profile in the cache.</span><span class="sxs-lookup"><span data-stu-id="e0850-133">To avoid API Management from making this HTTP request again, when the same user makes another request, you can specify to store the user profile in the cache.</span></span>

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

<span data-ttu-id="e0850-134">API Management stores the value in the cache using the exact same key that API Management originally attempted to retrieve it with.</span><span class="sxs-lookup"><span data-stu-id="e0850-134">API Management stores the value in the cache using the exact same key that API Management originally attempted to retrieve it with.</span></span> <span data-ttu-id="e0850-135">The duration that API Management chooses to store the value should be based on how often the information changes and how tolerant users are to out-of-date information.</span><span class="sxs-lookup"><span data-stu-id="e0850-135">The duration that API Management chooses to store the value should be based on how often the information changes and how tolerant users are to out-of-date information.</span></span> 

<span data-ttu-id="e0850-136">It is important to realize that retrieving from the cache is still an out-of-process, network request and potentially can still add tens of milliseconds to the request.</span><span class="sxs-lookup"><span data-stu-id="e0850-136">It is important to realize that retrieving from the cache is still an out-of-process, network request and potentially can still add tens of milliseconds to the request.</span></span> <span data-ttu-id="e0850-137">The benefits come when determining the user profile information takes longer than that due to needing to do database queries or aggregate information from multiple back-ends.</span><span class="sxs-lookup"><span data-stu-id="e0850-137">The benefits come when determining the user profile information takes longer than that due to needing to do database queries or aggregate information from multiple back-ends.</span></span>

<span data-ttu-id="e0850-138">The final step in the process is to update the returned response with the user profile information.</span><span class="sxs-lookup"><span data-stu-id="e0850-138">The final step in the process is to update the returned response with the user profile information.</span></span>

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

<span data-ttu-id="e0850-139">You can chose to include the quotation marks as part of the token so that even when the replace doesn’t occur, the response is still a valid JSON.</span><span class="sxs-lookup"><span data-stu-id="e0850-139">You can chose to include the quotation marks as part of the token so that even when the replace doesn’t occur, the response is still a valid JSON.</span></span>  

<span data-ttu-id="e0850-140">Once you combine all these steps together, the end result is a policy that looks like the following one.</span><span class="sxs-lookup"><span data-stu-id="e0850-140">Once you combine all these steps together, the end result is a policy that looks like the following one.</span></span>

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in the cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If API Management doesn’t find it in the cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request to get user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points to the profile for the current end-user -->
                    <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),(string)context.Variables["enduserid"]).AbsoluteUri)</set-url>
                    <set-method>GET</set-method>
                </send-request>

                <!-- Store response body in context variable -->
                <set-variable
                  name="userprofile"
                  value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />

                <!-- Store result in cache -->
                <cache-store-value
                  key="@("userprofile-" + context.Variables["enduserid"])"
                  value="@((string)context.Variables["userprofile"])"
                  duration="100000" />
            </when>
        </choose>
        <base />
    </inbound>
    <outbound>
        <!-- Update response body with user profile-->
        <find-and-replace
              from='"$userprofile$"'
              to="@((string)context.Variables["userprofile"])" />
        <base />
    </outbound>
</policies>
```

<span data-ttu-id="e0850-141">This caching approach is primarily used in web sites where HTML is composed on the server side so that it can be rendered as a single page.</span><span class="sxs-lookup"><span data-stu-id="e0850-141">This caching approach is primarily used in web sites where HTML is composed on the server side so that it can be rendered as a single page.</span></span> <span data-ttu-id="e0850-142">It can also be useful in APIs where clients cannot do client-side HTTP caching or it is desirable not to put that responsibility on the client.</span><span class="sxs-lookup"><span data-stu-id="e0850-142">It can also be useful in APIs where clients cannot do client-side HTTP caching or it is desirable not to put that responsibility on the client.</span></span>

<span data-ttu-id="e0850-143">This same kind of fragment caching can also be done on the backend web servers using a Redis caching server, however, using the API Management service to perform this work is useful when the cached fragments are coming from different back-ends than the primary responses.</span><span class="sxs-lookup"><span data-stu-id="e0850-143">This same kind of fragment caching can also be done on the backend web servers using a Redis caching server, however, using the API Management service to perform this work is useful when the cached fragments are coming from different back-ends than the primary responses.</span></span>

## <a name="transparent-versioning"></a><span data-ttu-id="e0850-144">Transparent versioning</span><span class="sxs-lookup"><span data-stu-id="e0850-144">Transparent versioning</span></span>
<span data-ttu-id="e0850-145">It is common practice for multiple different implementation versions of an API to be supported at any one time.</span><span class="sxs-lookup"><span data-stu-id="e0850-145">It is common practice for multiple different implementation versions of an API to be supported at any one time.</span></span> <span data-ttu-id="e0850-146">For example, to support different environments (dev, test, production, etc.) or to support older versions of the API to give time for API consumers to migrate to newer versions.</span><span class="sxs-lookup"><span data-stu-id="e0850-146">For example, to support different environments (dev, test, production, etc.) or to support older versions of the API to give time for API consumers to migrate to newer versions.</span></span> 

<span data-ttu-id="e0850-147">One approach to handling this, instead of requiring client developers to change the URLs from `/v1/customers` to `/v2/customers` is to store in the consumer’s profile data which version of the API they currently wish to use and call the appropriate backend URL.</span><span class="sxs-lookup"><span data-stu-id="e0850-147">One approach to handling this, instead of requiring client developers to change the URLs from `/v1/customers` to `/v2/customers` is to store in the consumer’s profile data which version of the API they currently wish to use and call the appropriate backend URL.</span></span> <span data-ttu-id="e0850-148">To determine the correct backend URL to call for a particular client, it is necessary to query some configuration data.</span><span class="sxs-lookup"><span data-stu-id="e0850-148">To determine the correct backend URL to call for a particular client, it is necessary to query some configuration data.</span></span> <span data-ttu-id="e0850-149">By caching this configuration data, API Management can minimize the performance penalty of doing this lookup.</span><span class="sxs-lookup"><span data-stu-id="e0850-149">By caching this configuration data, API Management can minimize the performance penalty of doing this lookup.</span></span>

<span data-ttu-id="e0850-150">The first step is to determine the identifier used to configure the desired version.</span><span class="sxs-lookup"><span data-stu-id="e0850-150">The first step is to determine the identifier used to configure the desired version.</span></span> <span data-ttu-id="e0850-151">In this example, I chose to associate the version to the product subscription key.</span><span class="sxs-lookup"><span data-stu-id="e0850-151">In this example, I chose to associate the version to the product subscription key.</span></span> 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

<span data-ttu-id="e0850-152">API Management then does a cache lookup to see whether it already retrieved the desired client version.</span><span class="sxs-lookup"><span data-stu-id="e0850-152">API Management then does a cache lookup to see whether it already retrieved the desired client version.</span></span>

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

<span data-ttu-id="e0850-153">Then, API Management checks to see if it did not find it in the cache.</span><span class="sxs-lookup"><span data-stu-id="e0850-153">Then, API Management checks to see if it did not find it in the cache.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

<span data-ttu-id="e0850-154">If API Management didn’t find it, API Management retrieves it.</span><span class="sxs-lookup"><span data-stu-id="e0850-154">If API Management didn’t find it, API Management retrieves it.</span></span>

```xml
<send-request
    mode="new"
    response-variable-name="clientconfiguresponse"
    timeout="10"
    ignore-error="true">
            <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
            <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="e0850-155">Extract the response body text from the response.</span><span class="sxs-lookup"><span data-stu-id="e0850-155">Extract the response body text from the response.</span></span>

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

<span data-ttu-id="e0850-156">Store it back in the cache for future use.</span><span class="sxs-lookup"><span data-stu-id="e0850-156">Store it back in the cache for future use.</span></span>

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

<span data-ttu-id="e0850-157">And finally update the back-end URL to select the version of the service desired by the client.</span><span class="sxs-lookup"><span data-stu-id="e0850-157">And finally update the back-end URL to select the version of the service desired by the client.</span></span>

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

<span data-ttu-id="e0850-158">The complete policy is as follows:</span><span class="sxs-lookup"><span data-stu-id="e0850-158">The complete policy is as follows:</span></span>

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If API Management doesn’t find it in the cache, make a request for it and store it -->
    <choose>
        <when condition="@(!context.Variables.ContainsKey("clientversion"))">
            <send-request mode="new" response-variable-name="clientconfiguresponse" timeout="10" ignore-error="true">
                <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
                <set-method>GET</set-method>
            </send-request>
            <!-- Store response body in context variable -->
            <set-variable name="clientversion" value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
            <!-- Store result in cache -->
            <cache-store-value key="@("clientversion-" + context.Variables["clientid"])" value="@((string)context.Variables["clientversion"])" duration="100000" />
        </when>
    </choose>
    <set-backend-service base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
</inbound>
```

<span data-ttu-id="e0850-159">Enabling API consumers to transparently control which backend version is being accessed by clients without having to update and redeploy clients is an elegant solution that addresses many API versioning concerns.</span><span class="sxs-lookup"><span data-stu-id="e0850-159">Enabling API consumers to transparently control which backend version is being accessed by clients without having to update and redeploy clients is an elegant solution that addresses many API versioning concerns.</span></span>

## <a name="tenant-isolation"></a><span data-ttu-id="e0850-160">Tenant Isolation</span><span class="sxs-lookup"><span data-stu-id="e0850-160">Tenant Isolation</span></span>
<span data-ttu-id="e0850-161">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span><span class="sxs-lookup"><span data-stu-id="e0850-161">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span></span> <span data-ttu-id="e0850-162">This minimizes the number of customers who are impacted by a hardware issue on the backend.</span><span class="sxs-lookup"><span data-stu-id="e0850-162">This minimizes the number of customers who are impacted by a hardware issue on the backend.</span></span> <span data-ttu-id="e0850-163">It also enables new software versions to be rolled out in stages.</span><span class="sxs-lookup"><span data-stu-id="e0850-163">It also enables new software versions to be rolled out in stages.</span></span> <span data-ttu-id="e0850-164">Ideally this backend architecture should be transparent to API consumers.</span><span class="sxs-lookup"><span data-stu-id="e0850-164">Ideally this backend architecture should be transparent to API consumers.</span></span> <span data-ttu-id="e0850-165">This can be achieved in a similar way to transparent versioning because it is based on the same technique of manipulating the backend URL using configuration state per API key.</span><span class="sxs-lookup"><span data-stu-id="e0850-165">This can be achieved in a similar way to transparent versioning because it is based on the same technique of manipulating the backend URL using configuration state per API key.</span></span>  

<span data-ttu-id="e0850-166">Instead of returning a preferred version of the API for each subscription key, you would return an identifier that relates a tenant to the assigned hardware group.</span><span class="sxs-lookup"><span data-stu-id="e0850-166">Instead of returning a preferred version of the API for each subscription key, you would return an identifier that relates a tenant to the assigned hardware group.</span></span> <span data-ttu-id="e0850-167">That identifier can be used to construct the appropriate backend URL.</span><span class="sxs-lookup"><span data-stu-id="e0850-167">That identifier can be used to construct the appropriate backend URL.</span></span>

## <a name="summary"></a><span data-ttu-id="e0850-168">Summary</span><span class="sxs-lookup"><span data-stu-id="e0850-168">Summary</span></span>
<span data-ttu-id="e0850-169">The freedom to use the Azure API management cache for storing any kind of data enables efficient access to configuration data that can affect the way an inbound request is processed.</span><span class="sxs-lookup"><span data-stu-id="e0850-169">The freedom to use the Azure API management cache for storing any kind of data enables efficient access to configuration data that can affect the way an inbound request is processed.</span></span> <span data-ttu-id="e0850-170">It can also be used to store data fragments that can augment responses, returned from a backend API.</span><span class="sxs-lookup"><span data-stu-id="e0850-170">It can also be used to store data fragments that can augment responses, returned from a backend API.</span></span>
