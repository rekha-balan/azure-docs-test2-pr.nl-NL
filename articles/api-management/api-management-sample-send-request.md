---
title: Using API Management service to generate HTTP requests
description: Learn to use request and response policies in API Management to call external services from your API
services: api-management
documentationcenter: ''
author: darrelmiller
manager: erikre
editor: ''
ms.assetid: 4539c0fa-21ef-4b1c-a1d4-d89a38c242fa
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 089d47375b6f6c6d3cc624cf0d2d6ff5135e3489
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563738"
---
# <a name="using-external-services-from-the-azure-api-management-service"></a><span data-ttu-id="7891c-103">Using external services from the Azure API Management service</span><span class="sxs-lookup"><span data-stu-id="7891c-103">Using external services from the Azure API Management service</span></span>
<span data-ttu-id="7891c-104">The policies available in Azure API Management service can do a wide range of useful work based purely on the incoming request, the outgoing response and basic configuration information.</span><span class="sxs-lookup"><span data-stu-id="7891c-104">The policies available in Azure API Management service can do a wide range of useful work based purely on the incoming request, the outgoing response and basic configuration information.</span></span> <span data-ttu-id="7891c-105">However, being able to interact with external services from API Management policies opens up many more opportunities.</span><span class="sxs-lookup"><span data-stu-id="7891c-105">However, being able to interact with external services from API Management policies opens up many more opportunities.</span></span>

<span data-ttu-id="7891c-106">We have previously seen how we can interact with the [Azure Event Hub service for logging, monitoring and analytics](api-management-log-to-eventhub-sample.md).</span><span class="sxs-lookup"><span data-stu-id="7891c-106">We have previously seen how we can interact with the [Azure Event Hub service for logging, monitoring and analytics](api-management-log-to-eventhub-sample.md).</span></span> <span data-ttu-id="7891c-107">In this article we will demonstrate policies that allow you to interact with any external HTTP based service.</span><span class="sxs-lookup"><span data-stu-id="7891c-107">In this article we will demonstrate policies that allow you to interact with any external HTTP based service.</span></span> <span data-ttu-id="7891c-108">These policies can be used for triggering remote events or for retrieving information that will be used to manipulate the original request and response in some way.</span><span class="sxs-lookup"><span data-stu-id="7891c-108">These policies can be used for triggering remote events or for retrieving information that will be used to manipulate the original request and response in some way.</span></span>

## <a name="send-one-way-request"></a><span data-ttu-id="7891c-109">Send-One-Way-Request</span><span class="sxs-lookup"><span data-stu-id="7891c-109">Send-One-Way-Request</span></span>
<span data-ttu-id="7891c-110">Possibly the simplest external interaction is the fire-and-forget style of request that allows an external service to be notified of some kind of important event.</span><span class="sxs-lookup"><span data-stu-id="7891c-110">Possibly the simplest external interaction is the fire-and-forget style of request that allows an external service to be notified of some kind of important event.</span></span> <span data-ttu-id="7891c-111">We can use the control flow policy `choose` to detect any kind of condition that we are interested in and then, if the condition is satisfied, we can make an external HTTP request using the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) policy.</span><span class="sxs-lookup"><span data-stu-id="7891c-111">We can use the control flow policy `choose` to detect any kind of condition that we are interested in and then, if the condition is satisfied, we can make an external HTTP request using the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) policy.</span></span> <span data-ttu-id="7891c-112">This could be a request to a messaging system like Hipchat or Slack, or a mail API like SendGrid or MailChimp, or for critical support incidents something like PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="7891c-112">This could be a request to a messaging system like Hipchat or Slack, or a mail API like SendGrid or MailChimp, or for critical support incidents something like PagerDuty.</span></span> <span data-ttu-id="7891c-113">All of these messaging systems have simple HTTP APIs that we can easily invoke.</span><span class="sxs-lookup"><span data-stu-id="7891c-113">All of these messaging systems have simple HTTP APIs that we can easily invoke.</span></span>

### <a name="alerting-with-slack"></a><span data-ttu-id="7891c-114">Alerting with Slack</span><span class="sxs-lookup"><span data-stu-id="7891c-114">Alerting with Slack</span></span>
<span data-ttu-id="7891c-115">The following example demonstrates how to send a message to a Slack chat room if the HTTP response status code is greater than or equal to 500.</span><span class="sxs-lookup"><span data-stu-id="7891c-115">The following example demonstrates how to send a message to a Slack chat room if the HTTP response status code is greater than or equal to 500.</span></span> <span data-ttu-id="7891c-116">A 500 range error indicates a problem with our backend API that the client of our API cannot resolve themselves.</span><span class="sxs-lookup"><span data-stu-id="7891c-116">A 500 range error indicates a problem with our backend API that the client of our API cannot resolve themselves.</span></span> <span data-ttu-id="7891c-117">It usually requires some kind of intervention on our part.</span><span class="sxs-lookup"><span data-stu-id="7891c-117">It usually requires some kind of intervention on our part.</span></span>  

```xml
<choose>
    <when condition="@(context.Response.StatusCode >= 500)">
      <send-one-way-request mode="new">
        <set-url>https://hooks.slack.com/services/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</set-url>
        <set-method>POST</set-method>
        <set-body>@{
                return new JObject(
                        new JProperty("username","APIM Alert"),
                        new JProperty("icon_emoji", ":ghost:"),
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",
                                                context.Request.Method,
                                                context.Request.Url.Path + context.Request.Url.QueryString,
                                                context.Request.Url.Host,
                                                context.Response.StatusCode,
                                                context.Response.StatusReason,
                                                context.User.Email
                                                ))
                        ).ToString();
            }</set-body>
      </send-one-way-request>
    </when>
</choose>
```

<span data-ttu-id="7891c-118">Slack has the notion of inbound web hooks.</span><span class="sxs-lookup"><span data-stu-id="7891c-118">Slack has the notion of inbound web hooks.</span></span> <span data-ttu-id="7891c-119">When configuring an inbound web hook, Slack generates a special URL which allows you to do a simple POST request and to pass a message into the Slack channel.</span><span class="sxs-lookup"><span data-stu-id="7891c-119">When configuring an inbound web hook, Slack generates a special URL which allows you to do a simple POST request and to pass a message into the Slack channel.</span></span> <span data-ttu-id="7891c-120">The JSON body that we create is based on a format defined by Slack.</span><span class="sxs-lookup"><span data-stu-id="7891c-120">The JSON body that we create is based on a format defined by Slack.</span></span>

![Slack Web Hook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a><span data-ttu-id="7891c-122">Is fire and forget good enough?</span><span class="sxs-lookup"><span data-stu-id="7891c-122">Is fire and forget good enough?</span></span>
<span data-ttu-id="7891c-123">There are certain tradeoffs when using a fire-and-forget style of request.</span><span class="sxs-lookup"><span data-stu-id="7891c-123">There are certain tradeoffs when using a fire-and-forget style of request.</span></span> <span data-ttu-id="7891c-124">If for some reason, the request fails, then the failure will not be reported.</span><span class="sxs-lookup"><span data-stu-id="7891c-124">If for some reason, the request fails, then the failure will not be reported.</span></span> <span data-ttu-id="7891c-125">In this particular situation, the complexity of having a secondary failure reporting system and the additional performance cost of waiting for the response is not warranted.</span><span class="sxs-lookup"><span data-stu-id="7891c-125">In this particular situation, the complexity of having a secondary failure reporting system and the additional performance cost of waiting for the response is not warranted.</span></span> <span data-ttu-id="7891c-126">For scenarios where it is essential to check the response, then the [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy is a better option.</span><span class="sxs-lookup"><span data-stu-id="7891c-126">For scenarios where it is essential to check the response, then the [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy is a better option.</span></span>

## <a name="send-request"></a><span data-ttu-id="7891c-127">Send-Request</span><span class="sxs-lookup"><span data-stu-id="7891c-127">Send-Request</span></span>
<span data-ttu-id="7891c-128">The `send-request` policy enables using an external service to perform complex processing functions and return data to the API management service that can be used for further policy processing.</span><span class="sxs-lookup"><span data-stu-id="7891c-128">The `send-request` policy enables using an external service to perform complex processing functions and return data to the API management service that can be used for further policy processing.</span></span>

### <a name="authorizing-reference-tokens"></a><span data-ttu-id="7891c-129">Authorizing reference tokens</span><span class="sxs-lookup"><span data-stu-id="7891c-129">Authorizing reference tokens</span></span>
<span data-ttu-id="7891c-130">A major function of API Management is protecting backend resources.</span><span class="sxs-lookup"><span data-stu-id="7891c-130">A major function of API Management is protecting backend resources.</span></span> <span data-ttu-id="7891c-131">If the authorization server used by your API creates [JWT tokens](http://jwt.io/) as part of its OAuth2 flow, as [Azure Active Directory](../active-directory/active-directory-aadconnect.md) does, then you can use the `validate-jwt` policy to verify the validity of the token.</span><span class="sxs-lookup"><span data-stu-id="7891c-131">If the authorization server used by your API creates [JWT tokens](http://jwt.io/) as part of its OAuth2 flow, as [Azure Active Directory](../active-directory/active-directory-aadconnect.md) does, then you can use the `validate-jwt` policy to verify the validity of the token.</span></span> <span data-ttu-id="7891c-132">However, some authorization servers create what are called [reference tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) that cannot be verified without making a call back to the authorization server.</span><span class="sxs-lookup"><span data-stu-id="7891c-132">However, some authorization servers create what are called [reference tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) that cannot be verified without making a call back to the authorization server.</span></span>

### <a name="standardized-introspection"></a><span data-ttu-id="7891c-133">Standardized introspection</span><span class="sxs-lookup"><span data-stu-id="7891c-133">Standardized introspection</span></span>
<span data-ttu-id="7891c-134">In the past there has been no standardized way of verifying a reference token with an authorization server.</span><span class="sxs-lookup"><span data-stu-id="7891c-134">In the past there has been no standardized way of verifying a reference token with an authorization server.</span></span> <span data-ttu-id="7891c-135">However a recently proposed standard [RFC 7662](https://tools.ietf.org/html/rfc7662) was published by the IETF that defines how a resource server can verify the validity of a token.</span><span class="sxs-lookup"><span data-stu-id="7891c-135">However a recently proposed standard [RFC 7662](https://tools.ietf.org/html/rfc7662) was published by the IETF that defines how a resource server can verify the validity of a token.</span></span>

### <a name="extracting-the-token"></a><span data-ttu-id="7891c-136">Extracting the token</span><span class="sxs-lookup"><span data-stu-id="7891c-136">Extracting the token</span></span>
<span data-ttu-id="7891c-137">The first step is to extract the token from the Authorization header.</span><span class="sxs-lookup"><span data-stu-id="7891c-137">The first step is to extract the token from the Authorization header.</span></span> <span data-ttu-id="7891c-138">The header value should be formatted with the `Bearer` authorization scheme, a single space and then the authorization token as per [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span><span class="sxs-lookup"><span data-stu-id="7891c-138">The header value should be formatted with the `Bearer` authorization scheme, a single space and then the authorization token as per [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span></span> <span data-ttu-id="7891c-139">Unfortunately there are cases where the authorization scheme is omitted.</span><span class="sxs-lookup"><span data-stu-id="7891c-139">Unfortunately there are cases where the authorization scheme is omitted.</span></span> <span data-ttu-id="7891c-140">To account for this when parsing, we split the header value on a space and select the last string from the returned array of strings.</span><span class="sxs-lookup"><span data-stu-id="7891c-140">To account for this when parsing, we split the header value on a space and select the last string from the returned array of strings.</span></span> <span data-ttu-id="7891c-141">This provides a workaround for badly formatted authorization headers.</span><span class="sxs-lookup"><span data-stu-id="7891c-141">This provides a workaround for badly formatted authorization headers.</span></span>

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-the-validation-request"></a><span data-ttu-id="7891c-142">Making the validation request</span><span class="sxs-lookup"><span data-stu-id="7891c-142">Making the validation request</span></span>
<span data-ttu-id="7891c-143">Once we have the authorization token, we can make the request to validate the token.</span><span class="sxs-lookup"><span data-stu-id="7891c-143">Once we have the authorization token, we can make the request to validate the token.</span></span> <span data-ttu-id="7891c-144">RFC 7662 calls this process introspection and requires that you `POST` a HTML form to the introspection resource.</span><span class="sxs-lookup"><span data-stu-id="7891c-144">RFC 7662 calls this process introspection and requires that you `POST` a HTML form to the introspection resource.</span></span> <span data-ttu-id="7891c-145">The HTML form must at least contain a key/value pair with the key `token`.</span><span class="sxs-lookup"><span data-stu-id="7891c-145">The HTML form must at least contain a key/value pair with the key `token`.</span></span> <span data-ttu-id="7891c-146">This request to the authorization server must also be authenticated to ensure that malicious clients cannot go trawling for valid tokens.</span><span class="sxs-lookup"><span data-stu-id="7891c-146">This request to the authorization server must also be authenticated to ensure that malicious clients cannot go trawling for valid tokens.</span></span>

```xml
<send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">
  <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>
  <set-method>POST</set-method>
  <set-header name="Authorization" exists-action="override">
    <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>
  </set-header>
  <set-header name="Content-Type" exists-action="override">
    <value>application/x-www-form-urlencoded</value>
  </set-header>
  <set-body>@($"token={(string)context.Variables["token"]}")</set-body>
</send-request>
```

### <a name="checking-the-response"></a><span data-ttu-id="7891c-147">Checking the response</span><span class="sxs-lookup"><span data-stu-id="7891c-147">Checking the response</span></span>
<span data-ttu-id="7891c-148">The `response-variable-name` attribute is used to give access the returned response.</span><span class="sxs-lookup"><span data-stu-id="7891c-148">The `response-variable-name` attribute is used to give access the returned response.</span></span> <span data-ttu-id="7891c-149">The name defined in this property can be used as a key into the `context.Variables` dictionary to access the `IResponse` object.</span><span class="sxs-lookup"><span data-stu-id="7891c-149">The name defined in this property can be used as a key into the `context.Variables` dictionary to access the `IResponse` object.</span></span>

<span data-ttu-id="7891c-150">From the response object we can retrieve the body and RFC 7622 tells us that the response must be a JSON object and must contain at least a property called `active` that is a boolean value.</span><span class="sxs-lookup"><span data-stu-id="7891c-150">From the response object we can retrieve the body and RFC 7622 tells us that the response must be a JSON object and must contain at least a property called `active` that is a boolean value.</span></span> <span data-ttu-id="7891c-151">When `active` is true then the token is considered valid.</span><span class="sxs-lookup"><span data-stu-id="7891c-151">When `active` is true then the token is considered valid.</span></span>

### <a name="reporting-failure"></a><span data-ttu-id="7891c-152">Reporting failure</span><span class="sxs-lookup"><span data-stu-id="7891c-152">Reporting failure</span></span>
<span data-ttu-id="7891c-153">We use a `<choose>` policy to detect if the token is invalid and if so, return a 401 response.</span><span class="sxs-lookup"><span data-stu-id="7891c-153">We use a `<choose>` policy to detect if the token is invalid and if so, return a 401 response.</span></span>

```xml
<choose>
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">
    <return-response response-variable-name="existing response variable">
      <set-status code="401" reason="Unauthorized" />
      <set-header name="WWW-Authenticate" exists-action="override">
        <value>Bearer error="invalid_token"</value>
      </set-header>
    </return-response>
  </when>
</choose>
```

<span data-ttu-id="7891c-154">As per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) which describes how `bearer` tokens should be used, we also return a `WWW-Authenticate` header with the 401 response.</span><span class="sxs-lookup"><span data-stu-id="7891c-154">As per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) which describes how `bearer` tokens should be used, we also return a `WWW-Authenticate` header with the 401 response.</span></span> <span data-ttu-id="7891c-155">The WWW-Authenticate is intended to instruct a client on how to construct a properly authorized request.</span><span class="sxs-lookup"><span data-stu-id="7891c-155">The WWW-Authenticate is intended to instruct a client on how to construct a properly authorized request.</span></span> <span data-ttu-id="7891c-156">Due to the wide variety of approaches possible with the OAuth2 framework, it is difficult to communicate all the needed information.</span><span class="sxs-lookup"><span data-stu-id="7891c-156">Due to the wide variety of approaches possible with the OAuth2 framework, it is difficult to communicate all the needed information.</span></span> <span data-ttu-id="7891c-157">Fortunately there are efforts underway to help [clients discover how to properly authorize requests to a resource server](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span><span class="sxs-lookup"><span data-stu-id="7891c-157">Fortunately there are efforts underway to help [clients discover how to properly authorize requests to a resource server](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span></span>

### <a name="final-solution"></a><span data-ttu-id="7891c-158">Final solution</span><span class="sxs-lookup"><span data-stu-id="7891c-158">Final solution</span></span>
<span data-ttu-id="7891c-159">Putting all the pieces together, we get the following policy:</span><span class="sxs-lookup"><span data-stu-id="7891c-159">Putting all the pieces together, we get the following policy:</span></span>

```xml
<inbound>
  <!-- Extract Token from Authorization header parameter -->
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />

  <!-- Send request to Token Server to validate token (see RFC 7662) -->
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>
    <set-method>POST</set-method>
    <set-header name="Authorization" exists-action="override">
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>
    </set-header>
    <set-header name="Content-Type" exists-action="override">
      <value>application/x-www-form-urlencoded</value>
    </set-header>
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>
  </send-request>

  <choose>
          <!-- Check active property in response -->
          <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">
              <!-- Return 401 Unauthorized with http-problem payload -->
              <return-response response-variable-name="existing response variable">
                  <set-status code="401" reason="Unauthorized" />
                  <set-header name="WWW-Authenticate" exists-action="override">
                      <value>Bearer error="invalid_token"</value>
                  </set-header>
              </return-response>
          </when>
      </choose>
  <base />
</inbound>
```

<span data-ttu-id="7891c-160">This is only one of many examples of how the `send-request` policy can be used to integrate useful external services into the process of requests and responses flowing through the API Management service.</span><span class="sxs-lookup"><span data-stu-id="7891c-160">This is only one of many examples of how the `send-request` policy can be used to integrate useful external services into the process of requests and responses flowing through the API Management service.</span></span>

## <a name="response-composition"></a><span data-ttu-id="7891c-161">Response Composition</span><span class="sxs-lookup"><span data-stu-id="7891c-161">Response Composition</span></span>
<span data-ttu-id="7891c-162">The `send-request` policy can be used for enhancing a primary request to a backend system, as we saw in the previous example, or it can be used as a complete replace for of the backend call.</span><span class="sxs-lookup"><span data-stu-id="7891c-162">The `send-request` policy can be used for enhancing a primary request to a backend system, as we saw in the previous example, or it can be used as a complete replace for of the backend call.</span></span> <span data-ttu-id="7891c-163">Using this technique we can easily create composite resources that are aggregated from multiple different systems.</span><span class="sxs-lookup"><span data-stu-id="7891c-163">Using this technique we can easily create composite resources that are aggregated from multiple different systems.</span></span>

### <a name="building-a-dashboard"></a><span data-ttu-id="7891c-164">Building a dashboard</span><span class="sxs-lookup"><span data-stu-id="7891c-164">Building a dashboard</span></span>
<span data-ttu-id="7891c-165">Sometimes you want to be able to expose information that exists in multiple backend systems, for example, to drive a dashboard.</span><span class="sxs-lookup"><span data-stu-id="7891c-165">Sometimes you want to be able to expose information that exists in multiple backend systems, for example, to drive a dashboard.</span></span> <span data-ttu-id="7891c-166">The KPIs come from all different back-ends, but you would prefer not to provide direct access to them and it would be nice if all the information could be retrieved in a single request.</span><span class="sxs-lookup"><span data-stu-id="7891c-166">The KPIs come from all different back-ends, but you would prefer not to provide direct access to them and it would be nice if all the information could be retrieved in a single request.</span></span> <span data-ttu-id="7891c-167">Perhaps some of the backend information needs some slicing and dicing and a little sanitizing first!</span><span class="sxs-lookup"><span data-stu-id="7891c-167">Perhaps some of the backend information needs some slicing and dicing and a little sanitizing first!</span></span> <span data-ttu-id="7891c-168">Being able to cache that composite resource would be a useful to reduce the backend load as you know users have a habit of hammering the F5 key in order to see if their underperforming metrics might change.</span><span class="sxs-lookup"><span data-stu-id="7891c-168">Being able to cache that composite resource would be a useful to reduce the backend load as you know users have a habit of hammering the F5 key in order to see if their underperforming metrics might change.</span></span>    

### <a name="faking-the-resource"></a><span data-ttu-id="7891c-169">Faking the resource</span><span class="sxs-lookup"><span data-stu-id="7891c-169">Faking the resource</span></span>
<span data-ttu-id="7891c-170">The first step to building our dashboard resource is to configure a new operation in the API Management publisher portal.</span><span class="sxs-lookup"><span data-stu-id="7891c-170">The first step to building our dashboard resource is to configure a new operation in the API Management publisher portal.</span></span> <span data-ttu-id="7891c-171">This will be a placeholder operation used to configure our composition policy to build our dynamic resource.</span><span class="sxs-lookup"><span data-stu-id="7891c-171">This will be a placeholder operation used to configure our composition policy to build our dynamic resource.</span></span>

![Dashboard operation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-the-requests"></a><span data-ttu-id="7891c-173">Making the requests</span><span class="sxs-lookup"><span data-stu-id="7891c-173">Making the requests</span></span>
<span data-ttu-id="7891c-174">Once the `dashboard` operation has been created we can configure a policy specifically for that operation.</span><span class="sxs-lookup"><span data-stu-id="7891c-174">Once the `dashboard` operation has been created we can configure a policy specifically for that operation.</span></span> 

![Dashboard operation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-sample-send-request/api-management-dashboard-policy.png)

<span data-ttu-id="7891c-176">The first step  is to extract any query parameters from the incoming request, so that we can forward them to our backend.</span><span class="sxs-lookup"><span data-stu-id="7891c-176">The first step  is to extract any query parameters from the incoming request, so that we can forward them to our backend.</span></span> <span data-ttu-id="7891c-177">In this example our dashboard is showing information based on a period of time an therefore has a `fromDate` and `toDate` parameter.</span><span class="sxs-lookup"><span data-stu-id="7891c-177">In this example our dashboard is showing information based on a period of time an therefore has a `fromDate` and `toDate` parameter.</span></span> <span data-ttu-id="7891c-178">We can use the `set-variable` policy to extract the information from the request URL.</span><span class="sxs-lookup"><span data-stu-id="7891c-178">We can use the `set-variable` policy to extract the information from the request URL.</span></span>

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

<span data-ttu-id="7891c-179">Once we have this information we can make requests to all the backend systems.</span><span class="sxs-lookup"><span data-stu-id="7891c-179">Once we have this information we can make requests to all the backend systems.</span></span> <span data-ttu-id="7891c-180">Each request constructs a new URL with the parameter information and calls its respective server and stores the response in a context variable.</span><span class="sxs-lookup"><span data-stu-id="7891c-180">Each request constructs a new URL with the parameter information and calls its respective server and stores the response in a context variable.</span></span>

```xml
<send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
  <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
  <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="7891c-181">These requests will execute in sequence, which is not ideal.</span><span class="sxs-lookup"><span data-stu-id="7891c-181">These requests will execute in sequence, which is not ideal.</span></span> <span data-ttu-id="7891c-182">In an upcoming release we will be introducing a new policy called `wait` that will enable all of these requests to execute in parallel.</span><span class="sxs-lookup"><span data-stu-id="7891c-182">In an upcoming release we will be introducing a new policy called `wait` that will enable all of these requests to execute in parallel.</span></span>

### <a name="responding"></a><span data-ttu-id="7891c-183">Responding</span><span class="sxs-lookup"><span data-stu-id="7891c-183">Responding</span></span>
<span data-ttu-id="7891c-184">To construct the composite response we can use the [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policy.</span><span class="sxs-lookup"><span data-stu-id="7891c-184">To construct the composite response we can use the [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policy.</span></span> <span data-ttu-id="7891c-185">The `set-body` element can use an expression to construct a new `JObject` with all the component representations embedded as properties.</span><span class="sxs-lookup"><span data-stu-id="7891c-185">The `set-body` element can use an expression to construct a new `JObject` with all the component representations embedded as properties.</span></span>

```xml
<return-response response-variable-name="existing response variable">
  <set-status code="200" reason="OK" />
  <set-header name="Content-Type" exists-action="override">
    <value>application/json</value>
  </set-header>
  <set-body>
    @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                  new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                  new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                  new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                  ).ToString())
  </set-body>
</return-response>
```

<span data-ttu-id="7891c-186">The complete policy looks as follows:</span><span class="sxs-lookup"><span data-stu-id="7891c-186">The complete policy looks as follows:</span></span>

```xml
<policies>
    <inbound>

  <set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
  <set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">

    <send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
      <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
      <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <return-response response-variable-name="existing response variable">
      <set-status code="200" reason="OK" />
      <set-header name="Content-Type" exists-action="override">
        <value>application/json</value>
      </set-header>
      <set-body>
        @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                      new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                      new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                      new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                      ).ToString())
      </set-body>
    </return-response>
    </inbound>
    <backend>
        <base />
    </backend>
    <outbound>
        <base />
    </outbound>
</policies>
```

<span data-ttu-id="7891c-187">In the configuration of the placeholder operation we can configure the dashboard resource to be cached for at least an hour because we understand the nature of the data means that even if it is an hour out of date, it will still be sufficiently effective to convey valuable information to the users.</span><span class="sxs-lookup"><span data-stu-id="7891c-187">In the configuration of the placeholder operation we can configure the dashboard resource to be cached for at least an hour because we understand the nature of the data means that even if it is an hour out of date, it will still be sufficiently effective to convey valuable information to the users.</span></span>

## <a name="summary"></a><span data-ttu-id="7891c-188">Summary</span><span class="sxs-lookup"><span data-stu-id="7891c-188">Summary</span></span>
<span data-ttu-id="7891c-189">Azure API Management service provides flexible policies that can be selectively applied to HTTP traffic and enables composition of backend services.</span><span class="sxs-lookup"><span data-stu-id="7891c-189">Azure API Management service provides flexible policies that can be selectively applied to HTTP traffic and enables composition of backend services.</span></span> <span data-ttu-id="7891c-190">Whether you want to enhance your API gateway with alerting functions, verification, validation capabilities or create new composite resources based on multiple backend services, the `send-request` and related policies open a world of possibilities.</span><span class="sxs-lookup"><span data-stu-id="7891c-190">Whether you want to enhance your API gateway with alerting functions, verification, validation capabilities or create new composite resources based on multiple backend services, the `send-request` and related policies open a world of possibilities.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="7891c-191">Watch a video overview of these policies</span><span class="sxs-lookup"><span data-stu-id="7891c-191">Watch a video overview of these policies</span></span>
<span data-ttu-id="7891c-192">For more information on the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), and [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policies covered in this article, please watch the following video.</span><span class="sxs-lookup"><span data-stu-id="7891c-192">For more information on the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), and [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policies covered in this article, please watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 




