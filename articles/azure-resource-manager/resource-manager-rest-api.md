---
title: Resource Manager REST APIs| Microsoft Docs
description: An overview of the Resource Manager REST APIs authentication and usage examples
services: azure-resource-manager
documentationcenter: na
author: navalev
manager: timlt
editor: ''
ms.assetid: e8d7a1d2-1e82-4212-8288-8697341408c5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/13/2017
ms.author: navale;tomfitz;
ms.openlocfilehash: b7957c52877b262506013a422cd1511dd0ee79a4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44668960"
---
# <a name="resource-manager-rest-apis"></a><span data-ttu-id="5c149-103">Resource Manager REST APIs</span><span class="sxs-lookup"><span data-stu-id="5c149-103">Resource Manager REST APIs</span></span>
> [!div class="op_single_selector"]
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [Azure CLI](xplat-cli-azure-resource-manager.md)
> * [Portal](resource-group-portal.md) 
> * [REST API](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="5c149-108">Behind every call to Azure Resource Manager, behind every deployed template, behind every configured storage account there are one or more calls to the Azure Resource Manager's RESTful API.</span><span class="sxs-lookup"><span data-stu-id="5c149-108">Behind every call to Azure Resource Manager, behind every deployed template, behind every configured storage account there are one or more calls to the Azure Resource Manager's RESTful API.</span></span> <span data-ttu-id="5c149-109">This topic is devoted to those APIs and how you can call them without using any SDK at all.</span><span class="sxs-lookup"><span data-stu-id="5c149-109">This topic is devoted to those APIs and how you can call them without using any SDK at all.</span></span> <span data-ttu-id="5c149-110">This approach is useful if you want full control of requests to Azure, or if the SDK for your preferred language is not available or doesn't support the operations you need.</span><span class="sxs-lookup"><span data-stu-id="5c149-110">This approach is useful if you want full control of requests to Azure, or if the SDK for your preferred language is not available or doesn't support the operations you need.</span></span>

<span data-ttu-id="5c149-111">This article does not go through every API that is exposed in Azure, but rather uses some operations as examples of how you connect to them.</span><span class="sxs-lookup"><span data-stu-id="5c149-111">This article does not go through every API that is exposed in Azure, but rather uses some operations as examples of how you connect to them.</span></span> <span data-ttu-id="5c149-112">After you understand the basics, you can read the [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) to find detailed information on how to use the rest of the APIs.</span><span class="sxs-lookup"><span data-stu-id="5c149-112">After you understand the basics, you can read the [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) to find detailed information on how to use the rest of the APIs.</span></span>

## <a name="authentication"></a><span data-ttu-id="5c149-113">Authentication</span><span class="sxs-lookup"><span data-stu-id="5c149-113">Authentication</span></span>
<span data-ttu-id="5c149-114">Authentication for Resource Manager is handled by Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="5c149-114">Authentication for Resource Manager is handled by Azure Active Directory (AD).</span></span> <span data-ttu-id="5c149-115">To connect to any API, you first need to authenticate with Azure AD to receive an authentication token that you can pass on to every request.</span><span class="sxs-lookup"><span data-stu-id="5c149-115">To connect to any API, you first need to authenticate with Azure AD to receive an authentication token that you can pass on to every request.</span></span> <span data-ttu-id="5c149-116">As we are describing a pure call directly to the REST APIs, we assume that you don't want to authenticate by being prompted for a username and password.</span><span class="sxs-lookup"><span data-stu-id="5c149-116">As we are describing a pure call directly to the REST APIs, we assume that you don't want to authenticate by being prompted for a username and password.</span></span> <span data-ttu-id="5c149-117">We also assume you are not using two factor authentication mechanisms.</span><span class="sxs-lookup"><span data-stu-id="5c149-117">We also assume you are not using two factor authentication mechanisms.</span></span> <span data-ttu-id="5c149-118">Therefore, we create what is called an Azure AD Application and a service principal that are used to log in.</span><span class="sxs-lookup"><span data-stu-id="5c149-118">Therefore, we create what is called an Azure AD Application and a service principal that are used to log in.</span></span> <span data-ttu-id="5c149-119">But remember that Azure AD support several authentication procedures and all of them could be used to retrieve that authentication token that we need for subsequent API requests.</span><span class="sxs-lookup"><span data-stu-id="5c149-119">But remember that Azure AD support several authentication procedures and all of them could be used to retrieve that authentication token that we need for subsequent API requests.</span></span>
<span data-ttu-id="5c149-120">Follow [Create Azure AD Application and Service Principle](resource-group-create-service-principal-portal.md) for step by step instructions.</span><span class="sxs-lookup"><span data-stu-id="5c149-120">Follow [Create Azure AD Application and Service Principle](resource-group-create-service-principal-portal.md) for step by step instructions.</span></span>

### <a name="generating-an-access-token"></a><span data-ttu-id="5c149-121">Generating an Access Token</span><span class="sxs-lookup"><span data-stu-id="5c149-121">Generating an Access Token</span></span>
<span data-ttu-id="5c149-122">Authentication against Azure AD is done by calling out to Azure AD, located at login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="5c149-122">Authentication against Azure AD is done by calling out to Azure AD, located at login.microsoftonline.com.</span></span> <span data-ttu-id="5c149-123">To authenticate, you need to have the following information:</span><span class="sxs-lookup"><span data-stu-id="5c149-123">To authenticate, you need to have the following information:</span></span>

* <span data-ttu-id="5c149-124">Azure AD Tenant ID (the name of that Azure AD you are using to log in, often the same as your company but not necessary)</span><span class="sxs-lookup"><span data-stu-id="5c149-124">Azure AD Tenant ID (the name of that Azure AD you are using to log in, often the same as your company but not necessary)</span></span>
* <span data-ttu-id="5c149-125">Application ID (taken during the Azure AD application creation step)</span><span class="sxs-lookup"><span data-stu-id="5c149-125">Application ID (taken during the Azure AD application creation step)</span></span>
* <span data-ttu-id="5c149-126">Password (that you selected while creating the Azure AD Application)</span><span class="sxs-lookup"><span data-stu-id="5c149-126">Password (that you selected while creating the Azure AD Application)</span></span>

<span data-ttu-id="5c149-127">In the following HTTP request, make sure to replace "Azure AD Tenant ID", "Application ID" and "Password" with the correct values.</span><span class="sxs-lookup"><span data-stu-id="5c149-127">In the following HTTP request, make sure to replace "Azure AD Tenant ID", "Application ID" and "Password" with the correct values.</span></span>

<span data-ttu-id="5c149-128">**Generic HTTP Request:**</span><span class="sxs-lookup"><span data-stu-id="5c149-128">**Generic HTTP Request:**</span></span>

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

<span data-ttu-id="5c149-129">... will (if authentication succeeds) result in a response similar to the following response:</span><span class="sxs-lookup"><span data-stu-id="5c149-129">... will (if authentication succeeds) result in a response similar to the following response:</span></span>

```json
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1448199959",
  "not_before": "1448196059",
  "resource": "https://management.core.windows.net/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhb...86U3JI_0InPUk_lZqWvKiEWsayA"
}
```
<span data-ttu-id="5c149-130">(The access_token in the preceding response have been shortened to increase readability)</span><span class="sxs-lookup"><span data-stu-id="5c149-130">(The access_token in the preceding response have been shortened to increase readability)</span></span>

<span data-ttu-id="5c149-131">**Generating access token using Bash:**</span><span class="sxs-lookup"><span data-stu-id="5c149-131">**Generating access token using Bash:**</span></span>

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

<span data-ttu-id="5c149-132">**Generating access token using PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="5c149-132">**Generating access token using PowerShell:**</span></span>

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

<span data-ttu-id="5c149-133">The response contains an access token, information about how long that token is valid, and information about what resource you can use that token for.</span><span class="sxs-lookup"><span data-stu-id="5c149-133">The response contains an access token, information about how long that token is valid, and information about what resource you can use that token for.</span></span>
<span data-ttu-id="5c149-134">The access token you received in the previous HTTP call must be passed in for all request to the Resource Manager API.</span><span class="sxs-lookup"><span data-stu-id="5c149-134">The access token you received in the previous HTTP call must be passed in for all request to the Resource Manager API.</span></span> <span data-ttu-id="5c149-135">You pass it as a header value named "Authorization" with the value "Bearer YOUR_ACCESS_TOKEN".</span><span class="sxs-lookup"><span data-stu-id="5c149-135">You pass it as a header value named "Authorization" with the value "Bearer YOUR_ACCESS_TOKEN".</span></span> <span data-ttu-id="5c149-136">Notice the space between "Bearer" and your access token.</span><span class="sxs-lookup"><span data-stu-id="5c149-136">Notice the space between "Bearer" and your access token.</span></span>

<span data-ttu-id="5c149-137">As you can see from the above HTTP Result, the token is valid for a specific period of time during which you should cache and reuse that same token.</span><span class="sxs-lookup"><span data-stu-id="5c149-137">As you can see from the above HTTP Result, the token is valid for a specific period of time during which you should cache and reuse that same token.</span></span> <span data-ttu-id="5c149-138">Even if it is possible to authenticate against Azure AD for each API call, it would be highly inefficient.</span><span class="sxs-lookup"><span data-stu-id="5c149-138">Even if it is possible to authenticate against Azure AD for each API call, it would be highly inefficient.</span></span>

## <a name="calling-resource-manager-rest-apis"></a><span data-ttu-id="5c149-139">Calling Resource Manager REST APIs</span><span class="sxs-lookup"><span data-stu-id="5c149-139">Calling Resource Manager REST APIs</span></span>
<span data-ttu-id="5c149-140">This topic only uses a few APIs to explain the basic usage of the REST operations.</span><span class="sxs-lookup"><span data-stu-id="5c149-140">This topic only uses a few APIs to explain the basic usage of the REST operations.</span></span> <span data-ttu-id="5c149-141">For information about all the operations, see [Azure Resource Manager REST APIs](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="5c149-141">For information about all the operations, see [Azure Resource Manager REST APIs](https://docs.microsoft.com/rest/api/resources/).</span></span>

### <a name="list-all-subscriptions"></a><span data-ttu-id="5c149-142">List all subscriptions</span><span class="sxs-lookup"><span data-stu-id="5c149-142">List all subscriptions</span></span>
<span data-ttu-id="5c149-143">One of the simplest operations you can do is to list the available subscriptions that you can access.</span><span class="sxs-lookup"><span data-stu-id="5c149-143">One of the simplest operations you can do is to list the available subscriptions that you can access.</span></span> <span data-ttu-id="5c149-144">In the following request, you see how the access token is passed in as a header:</span><span class="sxs-lookup"><span data-stu-id="5c149-144">In the following request, you see how the access token is passed in as a header:</span></span>

<span data-ttu-id="5c149-145">(Replace YOUR_ACCESS_TOKEN with your actual Access Token.)</span><span class="sxs-lookup"><span data-stu-id="5c149-145">(Replace YOUR_ACCESS_TOKEN with your actual Access Token.)</span></span>

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="5c149-146">... and as a result, you get a list of subscriptions that this service principal is allowed to access</span><span class="sxs-lookup"><span data-stu-id="5c149-146">... and as a result, you get a list of subscriptions that this service principal is allowed to access</span></span>

<span data-ttu-id="5c149-147">(Subscription IDs have been shortened for readability)</span><span class="sxs-lookup"><span data-stu-id="5c149-147">(Subscription IDs have been shortened for readability)</span></span>

```json
{
  "value": [
    {
      "id": "/subscriptions/3a8555...555995",
      "subscriptionId": "3a8555...555995",
      "displayName": "Azure Subscription",
      "state": "Enabled",
      "subscriptionPolicies": {
        "locationPlacementId": "Internal_2014-09-01",
        "quotaId": "Internal_2014-09-01"
      }
    }
  ]
}
```

### <a name="list-all-resource-groups-in-a-specific-subscription"></a><span data-ttu-id="5c149-148">List all resource groups in a specific subscription</span><span class="sxs-lookup"><span data-stu-id="5c149-148">List all resource groups in a specific subscription</span></span>
<span data-ttu-id="5c149-149">All resources available with the Resource Manager APIs are nested inside a resource group.</span><span class="sxs-lookup"><span data-stu-id="5c149-149">All resources available with the Resource Manager APIs are nested inside a resource group.</span></span> <span data-ttu-id="5c149-150">You can query Resource Manager for existing resource groups in your subscription using the following HTTP GET request.</span><span class="sxs-lookup"><span data-stu-id="5c149-150">You can query Resource Manager for existing resource groups in your subscription using the following HTTP GET request.</span></span> <span data-ttu-id="5c149-151">Notice how the subscription ID is passed in as part of the URL this time.</span><span class="sxs-lookup"><span data-stu-id="5c149-151">Notice how the subscription ID is passed in as part of the URL this time.</span></span>

<span data-ttu-id="5c149-152">(Replace YOUR_ACCESS_TOKEN and SUBSCRIPTION_ID with your actual access token and subscription ID)</span><span class="sxs-lookup"><span data-stu-id="5c149-152">(Replace YOUR_ACCESS_TOKEN and SUBSCRIPTION_ID with your actual access token and subscription ID)</span></span>

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="5c149-153">The response you get depends on whether you have any resource groups defined and if so, how many.</span><span class="sxs-lookup"><span data-stu-id="5c149-153">The response you get depends on whether you have any resource groups defined and if so, how many.</span></span>

<span data-ttu-id="5c149-154">(Subscription IDs have been shortened for readability)</span><span class="sxs-lookup"><span data-stu-id="5c149-154">(Subscription IDs have been shortened for readability)</span></span>

```json
{
    "value": [
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/myfirstresourcegroup",
            "name": "myfirstresourcegroup",
            "location": "eastus",
            "properties": {
                "provisioningState": "Succeeded"
            }
        },
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/mysecondresourcegroup",
            "name": "mysecondresourcegroup",
            "location": "northeurope",
            "tags": {
                "tagname1": "My first tag"
            },
            "properties": {
                "provisioningState": "Succeeded"
            }
        }
    ]
}
```

### <a name="create-a-resource-group"></a><span data-ttu-id="5c149-155">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="5c149-155">Create a resource group</span></span>
<span data-ttu-id="5c149-156">So far, we've only been querying the Resource Manager APIs for information.</span><span class="sxs-lookup"><span data-stu-id="5c149-156">So far, we've only been querying the Resource Manager APIs for information.</span></span> <span data-ttu-id="5c149-157">It's time we create some resources, and let's start by the simplest of them all, a resource group.</span><span class="sxs-lookup"><span data-stu-id="5c149-157">It's time we create some resources, and let's start by the simplest of them all, a resource group.</span></span> <span data-ttu-id="5c149-158">The following HTTP request creates a resource group in a region/location of your choice, and adds a tag to it.</span><span class="sxs-lookup"><span data-stu-id="5c149-158">The following HTTP request creates a resource group in a region/location of your choice, and adds a tag to it.</span></span>

<span data-ttu-id="5c149-159">(Replace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME with your actual Access Token, Subscription ID and name of the Resource Group you want to create)</span><span class="sxs-lookup"><span data-stu-id="5c149-159">(Replace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME with your actual Access Token, Subscription ID and name of the Resource Group you want to create)</span></span>

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  }
}
```

<span data-ttu-id="5c149-160">If successful, you get a response that is similar to the following response:</span><span class="sxs-lookup"><span data-stu-id="5c149-160">If successful, you get a response that is similar to the following response:</span></span>

```json
{
  "id": "/subscriptions/3a8555...555995/resourceGroups/RESOURCE_GROUP_NAME",
  "name": "RESOURCE_GROUP_NAME",
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  },
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<span data-ttu-id="5c149-161">You've successfully created a resource group in Azure.</span><span class="sxs-lookup"><span data-stu-id="5c149-161">You've successfully created a resource group in Azure.</span></span> <span data-ttu-id="5c149-162">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="5c149-162">Congratulations!</span></span>

### <a name="deploy-resources-to-a-resource-group-using-a-resource-manager-template"></a><span data-ttu-id="5c149-163">Deploy resources to a resource group using a Resource Manager Template</span><span class="sxs-lookup"><span data-stu-id="5c149-163">Deploy resources to a resource group using a Resource Manager Template</span></span>
<span data-ttu-id="5c149-164">With Resource Manager, you can deploy your resources using templates.</span><span class="sxs-lookup"><span data-stu-id="5c149-164">With Resource Manager, you can deploy your resources using templates.</span></span> <span data-ttu-id="5c149-165">A template defines several resources and their dependencies.</span><span class="sxs-lookup"><span data-stu-id="5c149-165">A template defines several resources and their dependencies.</span></span> <span data-ttu-id="5c149-166">For this section, we assume you are familiar with Resource Manager templates, and we just show you how to make the API call to start deployment.</span><span class="sxs-lookup"><span data-stu-id="5c149-166">For this section, we assume you are familiar with Resource Manager templates, and we just show you how to make the API call to start deployment.</span></span> <span data-ttu-id="5c149-167">For more information about constructing templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5c149-167">For more information about constructing templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="5c149-168">Deployment of a template doesn't differ much to how you call other APIs.</span><span class="sxs-lookup"><span data-stu-id="5c149-168">Deployment of a template doesn't differ much to how you call other APIs.</span></span> <span data-ttu-id="5c149-169">One important aspect is that deployment of a template can take quite a long time.</span><span class="sxs-lookup"><span data-stu-id="5c149-169">One important aspect is that deployment of a template can take quite a long time.</span></span> <span data-ttu-id="5c149-170">The API call just returns, and it's up to you as developer to query for status of the deployment to find out when the deployment is done.</span><span class="sxs-lookup"><span data-stu-id="5c149-170">The API call just returns, and it's up to you as developer to query for status of the deployment to find out when the deployment is done.</span></span> <span data-ttu-id="5c149-171">For more information, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="5c149-171">For more information, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>

<span data-ttu-id="5c149-172">For this example, we use a publicly exposed template available on [GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="5c149-172">For this example, we use a publicly exposed template available on [GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="5c149-173">The template we use deploys a Linux VM to the West US region.</span><span class="sxs-lookup"><span data-stu-id="5c149-173">The template we use deploys a Linux VM to the West US region.</span></span> <span data-ttu-id="5c149-174">Even though this example uses a template available in a public repository like GitHub, you can instead pass the full template as part of the request.</span><span class="sxs-lookup"><span data-stu-id="5c149-174">Even though this example uses a template available in a public repository like GitHub, you can instead pass the full template as part of the request.</span></span> <span data-ttu-id="5c149-175">Note that we provide parameter values in the request that are used inside the deployed template.</span><span class="sxs-lookup"><span data-stu-id="5c149-175">Note that we provide parameter values in the request that are used inside the deployed template.</span></span>

<span data-ttu-id="5c149-176">(Replace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD and DNS_NAME_FOR_PUBLIC_IP to values appropriate for your request)</span><span class="sxs-lookup"><span data-stu-id="5c149-176">(Replace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD and DNS_NAME_FOR_PUBLIC_IP to values appropriate for your request)</span></span>

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME/providers/microsoft.resources/deployments/DEPLOYMENT_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "properties": {
    "templateLink": {
      "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json",
      "contentVersion": "1.0.0.0",
    },
    "mode": "Incremental",
    "parameters": {
        "newStorageAccountName": {
          "value": "GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME"
        },
        "adminUsername": {
          "value": "ADMIN_USER_NAME"
        },
        "adminPassword": {
          "value": "ADMIN_PASSWORD"
        },
        "dnsNameForPublicIP": {
          "value": "DNS_NAME_FOR_PUBLIC_IP"
        },
        "ubuntuOSVersion": {
          "value": "15.04"
        }
    }
  }
}
```

<span data-ttu-id="5c149-177">The long JSON response for this request has been omitted to improve readability of this documentation.</span><span class="sxs-lookup"><span data-stu-id="5c149-177">The long JSON response for this request has been omitted to improve readability of this documentation.</span></span> <span data-ttu-id="5c149-178">The response contains information about the templated deployment that you created.</span><span class="sxs-lookup"><span data-stu-id="5c149-178">The response contains information about the templated deployment that you created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c149-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="5c149-179">Next steps</span></span>

- <span data-ttu-id="5c149-180">To learn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="5c149-180">To learn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
