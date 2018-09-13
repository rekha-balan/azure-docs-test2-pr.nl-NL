---
title: Use the Azure Stack API | Microsoft Docs
description: Learn how to retrieve an authentication from Azure to make API requests to Azure Stack.
services: azure-stack
documentationcenter: ''
author: cblackuk
manager: femila
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2018
ms.author: mabrigg
ms.reviewer: thoroet
ms.openlocfilehash: 3b89564bf17a9884640b51faa1c3966dce93f89a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856577"
---
<!--  cblackuk and charliejllewellyn. This is a community contribution by cblackuk-->

# <a name="use-the-azure-stack-api"></a><span data-ttu-id="8c6a8-103">Use the Azure Stack API</span><span class="sxs-lookup"><span data-stu-id="8c6a8-103">Use the Azure Stack API</span></span>

<span data-ttu-id="8c6a8-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="8c6a8-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="8c6a8-105">You can use the Application Programming Interface (API) to automate operations such as adding a VM to your Azure Stack cloud.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-105">You can use the Application Programming Interface (API) to automate operations such as adding a VM to your Azure Stack cloud.</span></span>

<span data-ttu-id="8c6a8-106">The API requires your client to authenticate to the Microsoft Azure login endpoint.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-106">The API requires your client to authenticate to the Microsoft Azure login endpoint.</span></span> <span data-ttu-id="8c6a8-107">The endpoint returns a token to use in the header of every request sent to the Azure Stack API.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-107">The endpoint returns a token to use in the header of every request sent to the Azure Stack API.</span></span> <span data-ttu-id="8c6a8-108">Microsoft Azure uses Oauth 2.0.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-108">Microsoft Azure uses Oauth 2.0.</span></span>

<span data-ttu-id="8c6a8-109">This article provides examples that use the **cURL** utility to create Azure Stack requests.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-109">This article provides examples that use the **cURL** utility to create Azure Stack requests.</span></span> <span data-ttu-id="8c6a8-110">The application, cURL, is a command-line tool with a library for transferring data.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-110">The application, cURL, is a command-line tool with a library for transferring data.</span></span> <span data-ttu-id="8c6a8-111">These examples walk through the process of retrieving a token to access the Azure Stack API.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-111">These examples walk through the process of retrieving a token to access the Azure Stack API.</span></span> <span data-ttu-id="8c6a8-112">Most programming languages provide Oauth 2.0 libraries, which have robust token management and handle tasks such refreshing the token.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-112">Most programming languages provide Oauth 2.0 libraries, which have robust token management and handle tasks such refreshing the token.</span></span>

<span data-ttu-id="8c6a8-113">Review the entire process of using the Azure Stack REST API with a generic REST client, such as **cURL**, to help you understand the underlying requests, and shows what you can expect to receive in a response payload.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-113">Review the entire process of using the Azure Stack REST API with a generic REST client, such as **cURL**, to help you understand the underlying requests, and shows what you can expect to receive in a response payload.</span></span>

<span data-ttu-id="8c6a8-114">This article doesn't explore all the options available for retrieving tokens such as interactive login or creating dedicated App IDs.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-114">This article doesn't explore all the options available for retrieving tokens such as interactive login or creating dedicated App IDs.</span></span> <span data-ttu-id="8c6a8-115">To get information about these topics, see [Azure REST API Reference](https://docs.microsoft.com/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="8c6a8-115">To get information about these topics, see [Azure REST API Reference](https://docs.microsoft.com/rest/api/).</span></span>

## <a name="get-a-token-from-azure"></a><span data-ttu-id="8c6a8-116">Get a token from Azure</span><span class="sxs-lookup"><span data-stu-id="8c6a8-116">Get a token from Azure</span></span>

<span data-ttu-id="8c6a8-117">Create a request body formatted using the content type x-www-form-urlencoded to obtain an access token.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-117">Create a request body formatted using the content type x-www-form-urlencoded to obtain an access token.</span></span> <span data-ttu-id="8c6a8-118">POST your request to the Azure REST Authentication and Login endpoint.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-118">POST your request to the Azure REST Authentication and Login endpoint.</span></span>

### <a name="uri"></a><span data-ttu-id="8c6a8-119">URI</span><span class="sxs-lookup"><span data-stu-id="8c6a8-119">URI</span></span>

```bash  
POST https://login.microsoftonline.com/{tenant id}/oauth2/token
```

<span data-ttu-id="8c6a8-120">**Tenant ID** is either:</span><span class="sxs-lookup"><span data-stu-id="8c6a8-120">**Tenant ID** is either:</span></span>

 - <span data-ttu-id="8c6a8-121">Your tenant domain, such as `fabrikam.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="8c6a8-121">Your tenant domain, such as `fabrikam.onmicrosoft.com`</span></span>
 - <span data-ttu-id="8c6a8-122">Your tenant ID, such as `8eaed023-2b34-4da1-9baa-8bc8c9d6a491`</span><span class="sxs-lookup"><span data-stu-id="8c6a8-122">Your tenant ID, such as `8eaed023-2b34-4da1-9baa-8bc8c9d6a491`</span></span>
 - <span data-ttu-id="8c6a8-123">Default value for tenant-independent keys: `common`</span><span class="sxs-lookup"><span data-stu-id="8c6a8-123">Default value for tenant-independent keys: `common`</span></span>

### <a name="post-body"></a><span data-ttu-id="8c6a8-124">Post Body</span><span class="sxs-lookup"><span data-stu-id="8c6a8-124">Post Body</span></span>

```bash  
grant_type=password
&client_id=1950a258-227b-4e31-a9cf-717495945fc2
&resource=https://contoso.onmicrosoft.com/4de154de-f8a8-4017-af41-df619da68155
&username=admin@fabrikam.onmicrosoft.com
&password=Password123
&scope=openid
```

<span data-ttu-id="8c6a8-125">For each value:</span><span class="sxs-lookup"><span data-stu-id="8c6a8-125">For each value:</span></span>

 - <span data-ttu-id="8c6a8-126">**grant_type**</span><span class="sxs-lookup"><span data-stu-id="8c6a8-126">**grant_type**</span></span>  
    <span data-ttu-id="8c6a8-127">The type of authentication scheme you will using.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-127">The type of authentication scheme you will using.</span></span> <span data-ttu-id="8c6a8-128">In this example, the value is `password`</span><span class="sxs-lookup"><span data-stu-id="8c6a8-128">In this example, the value is `password`</span></span>

 - <span data-ttu-id="8c6a8-129">**resource**</span><span class="sxs-lookup"><span data-stu-id="8c6a8-129">**resource**</span></span>  
    <span data-ttu-id="8c6a8-130">The resource the token accesses.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-130">The resource the token accesses.</span></span> <span data-ttu-id="8c6a8-131">You can find the resource by querying the Azure Stack management metadata endpoint.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-131">You can find the resource by querying the Azure Stack management metadata endpoint.</span></span> <span data-ttu-id="8c6a8-132">Look at the **audiences** section</span><span class="sxs-lookup"><span data-stu-id="8c6a8-132">Look at the **audiences** section</span></span>

 - <span data-ttu-id="8c6a8-133">**Azure Stack management endpoint**</span><span class="sxs-lookup"><span data-stu-id="8c6a8-133">**Azure Stack management endpoint**</span></span>  
    ```
    https://management.{region}.{Azure Stack domain}/metadata/endpoints?api-version=2015-01-01
    ```

  > [!NOTE]  
  > <span data-ttu-id="8c6a8-134">If you are an administrator trying to access the tenant API then you must make sure to use tenant endpoint, for example: `https://adminmanagement.{region}.{Azure Stack domain}/metadata/endpoints?api-version=2015-01-011`</span><span class="sxs-lookup"><span data-stu-id="8c6a8-134">If you are an administrator trying to access the tenant API then you must make sure to use tenant endpoint, for example: `https://adminmanagement.{region}.{Azure Stack domain}/metadata/endpoints?api-version=2015-01-011`</span></span>  

  <span data-ttu-id="8c6a8-135">For example, with the Azure Stack Development Kit as an endpoint:</span><span class="sxs-lookup"><span data-stu-id="8c6a8-135">For example, with the Azure Stack Development Kit as an endpoint:</span></span>

    ```bash
    curl 'https://management.local.azurestack.external/metadata/endpoints?api-version=2015-01-01'
    ```

  <span data-ttu-id="8c6a8-136">Response:</span><span class="sxs-lookup"><span data-stu-id="8c6a8-136">Response:</span></span>

  ```
  {
  "galleryEndpoint":"https://adminportal.local.azurestack.external:30015/",
  "graphEndpoint":"https://graph.windows.net/",
  "portalEndpoint":"https://adminportal.local.azurestack.external/",
  "authentication":{
      "loginEndpoint":"https://login.windows.net/",
      "audiences":["https://contoso.onmicrosoft.com/4de154de-f8a8-4017-af41-df619da68155"]
      }
  }
  ```

### <a name="example"></a><span data-ttu-id="8c6a8-137">Example</span><span class="sxs-lookup"><span data-stu-id="8c6a8-137">Example</span></span>

  ```
  https://contoso.onmicrosoft.com/4de154de-f8a8-4017-af41-df619da68155
  ```

  <span data-ttu-id="8c6a8-138">**client_id**</span><span class="sxs-lookup"><span data-stu-id="8c6a8-138">**client_id**</span></span>

  <span data-ttu-id="8c6a8-139">This value is hardcoded to a default value:</span><span class="sxs-lookup"><span data-stu-id="8c6a8-139">This value is hardcoded to a default value:</span></span>

  ```
  1950a258-227b-4e31-a9cf-717495945fc2
  ```

  <span data-ttu-id="8c6a8-140">Alternative options are available for specific scenarios:</span><span class="sxs-lookup"><span data-stu-id="8c6a8-140">Alternative options are available for specific scenarios:</span></span>

  
  | <span data-ttu-id="8c6a8-141">Application</span><span class="sxs-lookup"><span data-stu-id="8c6a8-141">Application</span></span> | <span data-ttu-id="8c6a8-142">ApplicationID</span><span class="sxs-lookup"><span data-stu-id="8c6a8-142">ApplicationID</span></span> |
  | --------------------------------------- |:-------------------------------------------------------------:|
  | <span data-ttu-id="8c6a8-143">LegacyPowerShell</span><span class="sxs-lookup"><span data-stu-id="8c6a8-143">LegacyPowerShell</span></span> | <span data-ttu-id="8c6a8-144">0a7bdc5c-7b57-40be-9939-d4c5fc7cd417</span><span class="sxs-lookup"><span data-stu-id="8c6a8-144">0a7bdc5c-7b57-40be-9939-d4c5fc7cd417</span></span> |
  | <span data-ttu-id="8c6a8-145">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c6a8-145">PowerShell</span></span> | <span data-ttu-id="8c6a8-146">1950a258-227b-4e31-a9cf-717495945fc2</span><span class="sxs-lookup"><span data-stu-id="8c6a8-146">1950a258-227b-4e31-a9cf-717495945fc2</span></span> |
  | <span data-ttu-id="8c6a8-147">WindowsAzureActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="8c6a8-147">WindowsAzureActiveDirectory</span></span> | <span data-ttu-id="8c6a8-148">00000002-0000-0000-c000-000000000000</span><span class="sxs-lookup"><span data-stu-id="8c6a8-148">00000002-0000-0000-c000-000000000000</span></span> |
  | <span data-ttu-id="8c6a8-149">VisualStudio</span><span class="sxs-lookup"><span data-stu-id="8c6a8-149">VisualStudio</span></span> | <span data-ttu-id="8c6a8-150">872cd9fa-d31f-45e0-9eab-6e460a02d1f1</span><span class="sxs-lookup"><span data-stu-id="8c6a8-150">872cd9fa-d31f-45e0-9eab-6e460a02d1f1</span></span> |
  | <span data-ttu-id="8c6a8-151">AzureCLI</span><span class="sxs-lookup"><span data-stu-id="8c6a8-151">AzureCLI</span></span> | <span data-ttu-id="8c6a8-152">04b07795-8ddb-461a-bbee-02f9e1bf7b46</span><span class="sxs-lookup"><span data-stu-id="8c6a8-152">04b07795-8ddb-461a-bbee-02f9e1bf7b46</span></span> |

  <span data-ttu-id="8c6a8-153">**username**</span><span class="sxs-lookup"><span data-stu-id="8c6a8-153">**username**</span></span>

  <span data-ttu-id="8c6a8-154">For example, the Azure Stack AAD account:</span><span class="sxs-lookup"><span data-stu-id="8c6a8-154">For example, the Azure Stack AAD account:</span></span>

  ```
  azurestackadmin@fabrikam.onmicrosoft.com
  ```

  <span data-ttu-id="8c6a8-155">**password**</span><span class="sxs-lookup"><span data-stu-id="8c6a8-155">**password**</span></span>

  <span data-ttu-id="8c6a8-156">The Azure Stack AAD admin password.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-156">The Azure Stack AAD admin password.</span></span>

### <a name="example"></a><span data-ttu-id="8c6a8-157">Example</span><span class="sxs-lookup"><span data-stu-id="8c6a8-157">Example</span></span>

<span data-ttu-id="8c6a8-158">Request:</span><span class="sxs-lookup"><span data-stu-id="8c6a8-158">Request:</span></span>

```
curl -X "POST" "https://login.windows.net/fabrikam.onmicrosoft.com/oauth2/token" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=1950a258-227b-4e31-a9cf-717495945fc2" \
--data-urlencode "grant_type=password" \
--data-urlencode "username=admin@fabrikam.onmicrosoft.com" \
--data-urlencode 'password=Password12345' \
--data-urlencode "resource=https://contoso.onmicrosoft.com/4de154de-f8a8-4017-af41-df619da68155"
```

<span data-ttu-id="8c6a8-159">Response:</span><span class="sxs-lookup"><span data-stu-id="8c6a8-159">Response:</span></span>

```
{
  "token_type": "Bearer",
  "scope": "user_impersonation",
  "expires_in": "3599",
  "ext_expires_in": "0",
  "expires_on": "1512574780",
  "not_before": "1512570880",
  "resource": "https://contoso.onmicrosoft.com/4de154de-f8a8-4017-af41-df619da68155",
  "access_token": "eyJ0eXAiOi...truncated for readability..."
}
```

## <a name="api-queries"></a><span data-ttu-id="8c6a8-160">API queries</span><span class="sxs-lookup"><span data-stu-id="8c6a8-160">API queries</span></span>

<span data-ttu-id="8c6a8-161">Once you get your access token, you need to add it as a header to each of your API requests.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-161">Once you get your access token, you need to add it as a header to each of your API requests.</span></span> <span data-ttu-id="8c6a8-162">In order to do so, you need to create a header **authorization** with value: `Bearer <access token>`.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-162">In order to do so, you need to create a header **authorization** with value: `Bearer <access token>`.</span></span> <span data-ttu-id="8c6a8-163">For example:</span><span class="sxs-lookup"><span data-stu-id="8c6a8-163">For example:</span></span>

<span data-ttu-id="8c6a8-164">Request:</span><span class="sxs-lookup"><span data-stu-id="8c6a8-164">Request:</span></span>

```bash  
curl -H "Authorization: Bearer eyJ0eXAiOi...truncated for readability..." 'https://adminmanagement.local.azurestack.external/subscriptions?api-version=2016-05-01'
```

<span data-ttu-id="8c6a8-165">Response:</span><span class="sxs-lookup"><span data-stu-id="8c6a8-165">Response:</span></span>

```bash  
offerId : /delegatedProviders/default/offers/92F30E5D-F163-4C58-8F02-F31CFE66C21B
id : /subscriptions/800c4168-3eb1-406b-a4ca-919fe7ee42e8
subscriptionId : 800c4168-3eb1-406b-a4ca-919fe7ee42e8
tenantId : 9fea4606-7c07-4518-9f3f-8de9c52ab628
displayName : Default Provider Subscription
state : Enabled
subscriptionPolicies : @{locationPlacementId=AzureStack}
```

### <a name="url-structure-and-query-syntax"></a><span data-ttu-id="8c6a8-166">URL structure and query syntax</span><span class="sxs-lookup"><span data-stu-id="8c6a8-166">URL structure and query syntax</span></span>

<span data-ttu-id="8c6a8-167">Generic request URI, consists of: {URI-scheme} :// {URI-host} / {resource-path} ?</span><span class="sxs-lookup"><span data-stu-id="8c6a8-167">Generic request URI, consists of: {URI-scheme} :// {URI-host} / {resource-path} ?</span></span> <span data-ttu-id="8c6a8-168">{query-string}</span><span class="sxs-lookup"><span data-stu-id="8c6a8-168">{query-string}</span></span>

- <span data-ttu-id="8c6a8-169">**URI scheme**:</span><span class="sxs-lookup"><span data-stu-id="8c6a8-169">**URI scheme**:</span></span>  
<span data-ttu-id="8c6a8-170">The URI indicates the protocol used to send the request.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-170">The URI indicates the protocol used to send the request.</span></span> <span data-ttu-id="8c6a8-171">For example, `http` or `https`.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-171">For example, `http` or `https`.</span></span>
- <span data-ttu-id="8c6a8-172">**URI host**:</span><span class="sxs-lookup"><span data-stu-id="8c6a8-172">**URI host**:</span></span>  
<span data-ttu-id="8c6a8-173">The host specifies the domain name or IP address of the server where the REST service endpoint is hosted, such as `graph.microsoft.com` or `adminmanagement.local.azurestack.external`.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-173">The host specifies the domain name or IP address of the server where the REST service endpoint is hosted, such as `graph.microsoft.com` or `adminmanagement.local.azurestack.external`.</span></span>
- <span data-ttu-id="8c6a8-174">**Resource path**:</span><span class="sxs-lookup"><span data-stu-id="8c6a8-174">**Resource path**:</span></span>  
<span data-ttu-id="8c6a8-175">The path specifies the resource or resource collection, which may include multiple segments used by the service in determining the selection of those resources.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-175">The path specifies the resource or resource collection, which may include multiple segments used by the service in determining the selection of those resources.</span></span> <span data-ttu-id="8c6a8-176">For example: `beta/applications/00003f25-7e1f-4278-9488-efc7bac53c4a/owners` can be used to query the list a specific application's owners within the applications collection.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-176">For example: `beta/applications/00003f25-7e1f-4278-9488-efc7bac53c4a/owners` can be used to query the list a specific application's owners within the applications collection.</span></span>
- <span data-ttu-id="8c6a8-177">**Query string**:</span><span class="sxs-lookup"><span data-stu-id="8c6a8-177">**Query string**:</span></span>  
<span data-ttu-id="8c6a8-178">The string provides additional simple parameters, such as the API version or resource selection criteria.</span><span class="sxs-lookup"><span data-stu-id="8c6a8-178">The string provides additional simple parameters, such as the API version or resource selection criteria.</span></span>

## <a name="azure-stack-request-uri-construct"></a><span data-ttu-id="8c6a8-179">Azure Stack request URI construct</span><span class="sxs-lookup"><span data-stu-id="8c6a8-179">Azure Stack request URI construct</span></span>

```
{URI-scheme} :// {URI-host} / {subscription id} / {resource group} / {provider} / {resource-path} ? {OPTIONAL: filter-expression} {MANDATORY: api-version}
```

### <a name="uri-syntax"></a><span data-ttu-id="8c6a8-180">URI syntax</span><span class="sxs-lookup"><span data-stu-id="8c6a8-180">URI syntax</span></span>

```
https://adminmanagement.local.azurestack.external/{subscription id}/resourcegroups/{resource group}/providers/{provider}/{resource-path}?{api-version}
```

### <a name="query-uri-example"></a><span data-ttu-id="8c6a8-181">Query URI example</span><span class="sxs-lookup"><span data-stu-id="8c6a8-181">Query URI example</span></span>

```
https://adminmanagement.local.azurestack.external/subscriptions/800c4168-3eb1-406b-a4ca-919fe7ee42e8/resourcegroups/system.local/providers/microsoft.infrastructureinsights.admin/regionhealths/local/Alerts?$filter=(Properties/State eq 'Active') and (Properties/Severity eq 'Critical')&$orderby=Properties/CreatedTimestamp desc&api-version=2016-05-01"
```

## <a name="next-steps"></a><span data-ttu-id="8c6a8-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="8c6a8-182">Next steps</span></span>

<span data-ttu-id="8c6a8-183">For more information about using the Azure RESTful endpoints, see [Azure REST API Reference](https://docs.microsoft.com/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="8c6a8-183">For more information about using the Azure RESTful endpoints, see [Azure REST API Reference](https://docs.microsoft.com/rest/api/).</span></span>
