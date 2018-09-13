---
title: Authenticate with Mobile Engagement REST APIs
description: Describes how to authenticate with Azure Mobile Engagement REST APIs
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: da82cb36-957a-4e19-a805-b44733cf6597
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: d2b68bb5790e9d6c84605cfdf9a4330b9ed02cb4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555995"
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a><span data-ttu-id="bae56-103">Authenticate with Mobile Engagement REST APIs</span><span class="sxs-lookup"><span data-stu-id="bae56-103">Authenticate with Mobile Engagement REST APIs</span></span>
## <a name="overview"></a><span data-ttu-id="bae56-104">Overview</span><span class="sxs-lookup"><span data-stu-id="bae56-104">Overview</span></span>
<span data-ttu-id="bae56-105">This document describes how to get a valid AAD Oauth token to authenticate with the Mobile Engagement REST APIs.</span><span class="sxs-lookup"><span data-stu-id="bae56-105">This document describes how to get a valid AAD Oauth token to authenticate with the Mobile Engagement REST APIs.</span></span> 

<span data-ttu-id="bae56-106">It is assumed that you have a valid Azure subscription and you have created a Mobile Engagement app using one of our [Developer Tutorials](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bae56-106">It is assumed that you have a valid Azure subscription and you have created a Mobile Engagement app using one of our [Developer Tutorials](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="authentication"></a><span data-ttu-id="bae56-107">Authentication</span><span class="sxs-lookup"><span data-stu-id="bae56-107">Authentication</span></span>
<span data-ttu-id="bae56-108">A Microsoft Azure Active Directory based OAuth token is used for authentication.</span><span class="sxs-lookup"><span data-stu-id="bae56-108">A Microsoft Azure Active Directory based OAuth token is used for authentication.</span></span> 

<span data-ttu-id="bae56-109">In order to authentication an API request, an authorization header must be added to every request which is of the following form:</span><span class="sxs-lookup"><span data-stu-id="bae56-109">In order to authentication an API request, an authorization header must be added to every request which is of the following form:</span></span>

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> <span data-ttu-id="bae56-110">Azure Active Directory tokens expire in 1 hour.</span><span class="sxs-lookup"><span data-stu-id="bae56-110">Azure Active Directory tokens expire in 1 hour.</span></span>
> 
> 

<span data-ttu-id="bae56-111">There are several ways to get a token.</span><span class="sxs-lookup"><span data-stu-id="bae56-111">There are several ways to get a token.</span></span> <span data-ttu-id="bae56-112">Since the APIs are generally called from a cloud service, you want to use an API key.</span><span class="sxs-lookup"><span data-stu-id="bae56-112">Since the APIs are generally called from a cloud service, you want to use an API key.</span></span> <span data-ttu-id="bae56-113">An API key in Azure terminology is called a Service principal password.</span><span class="sxs-lookup"><span data-stu-id="bae56-113">An API key in Azure terminology is called a Service principal password.</span></span> <span data-ttu-id="bae56-114">The following procedure describes one way to setting it up manually.</span><span class="sxs-lookup"><span data-stu-id="bae56-114">The following procedure describes one way to setting it up manually.</span></span>

### <a name="one-time-setup-using-script"></a><span data-ttu-id="bae56-115">One-time setup (using script)</span><span class="sxs-lookup"><span data-stu-id="bae56-115">One-time setup (using script)</span></span>
<span data-ttu-id="bae56-116">You should follow the set of instructions below to perform the setup using a PowerShell script which takes the minimum time for setup but uses the most permissible defaults.</span><span class="sxs-lookup"><span data-stu-id="bae56-116">You should follow the set of instructions below to perform the setup using a PowerShell script which takes the minimum time for setup but uses the most permissible defaults.</span></span> <span data-ttu-id="bae56-117">Optionally, you can also follow the instructions in the [manual setup](mobile-engagement-api-authentication-manual.md) for doing this from the Azure portal directly and do finer configuration.</span><span class="sxs-lookup"><span data-stu-id="bae56-117">Optionally, you can also follow the instructions in the [manual setup](mobile-engagement-api-authentication-manual.md) for doing this from the Azure portal directly and do finer configuration.</span></span> 

1. <span data-ttu-id="bae56-118">Get the latest version of Azure PowerShell from [here](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="bae56-118">Get the latest version of Azure PowerShell from [here](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="bae56-119">For more information on the download instructions, you can see this [link](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="bae56-119">For more information on the download instructions, you can see this [link](/powershell/azureps-cmdlets-docs).</span></span>  
2. <span data-ttu-id="bae56-120">Once Azure PowerShell is installed, use the following commands to ensure that you have the **Azure module** installed:</span><span class="sxs-lookup"><span data-stu-id="bae56-120">Once Azure PowerShell is installed, use the following commands to ensure that you have the **Azure module** installed:</span></span>
   
    <span data-ttu-id="bae56-121">a.</span><span class="sxs-lookup"><span data-stu-id="bae56-121">a.</span></span> <span data-ttu-id="bae56-122">Make sure the Azure PowerShell module is available in the list of available modules.</span><span class="sxs-lookup"><span data-stu-id="bae56-122">Make sure the Azure PowerShell module is available in the list of available modules.</span></span> 
   
        Get-Module –ListAvailable 
   
    ![Available Azure Modules][1]
   
    <span data-ttu-id="bae56-124">b.</span><span class="sxs-lookup"><span data-stu-id="bae56-124">b.</span></span> <span data-ttu-id="bae56-125">If you do not find the Azure PowerShell module in the above list then you need to run the following:</span><span class="sxs-lookup"><span data-stu-id="bae56-125">If you do not find the Azure PowerShell module in the above list then you need to run the following:</span></span>
   
        Import-Module Azure 
3. <span data-ttu-id="bae56-126">Login to the Azure Resource Manager from PowerShell by running the following command and providing your user name and password for your Azure account:</span><span class="sxs-lookup"><span data-stu-id="bae56-126">Login to the Azure Resource Manager from PowerShell by running the following command and providing your user name and password for your Azure account:</span></span> 
   
        Login-AzureRmAccount
4. <span data-ttu-id="bae56-127">If you have multiple subscriptions then you should run the following:</span><span class="sxs-lookup"><span data-stu-id="bae56-127">If you have multiple subscriptions then you should run the following:</span></span>
   
    <span data-ttu-id="bae56-128">a.</span><span class="sxs-lookup"><span data-stu-id="bae56-128">a.</span></span> <span data-ttu-id="bae56-129">Get a list of all your subscriptions and copy the SubscriptionId of the subscription you want to use.</span><span class="sxs-lookup"><span data-stu-id="bae56-129">Get a list of all your subscriptions and copy the SubscriptionId of the subscription you want to use.</span></span> <span data-ttu-id="bae56-130">Make sure this subscription is the same one which has the Mobile Engagement App which you are going to interact with using the APIs.</span><span class="sxs-lookup"><span data-stu-id="bae56-130">Make sure this subscription is the same one which has the Mobile Engagement App which you are going to interact with using the APIs.</span></span> 
   
        Get-AzureRmSubscription
   
    <span data-ttu-id="bae56-131">b.</span><span class="sxs-lookup"><span data-stu-id="bae56-131">b.</span></span> <span data-ttu-id="bae56-132">Run the following command providing the SubscriptionId to configure the subscription to be used.</span><span class="sxs-lookup"><span data-stu-id="bae56-132">Run the following command providing the SubscriptionId to configure the subscription to be used.</span></span>
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. <span data-ttu-id="bae56-133">Copy the text for the [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) script to your local machine and save it as a PowerShell cmdlet (e.g. `APIAuth.ps1`) and execute it `.\APIAuth.ps1`.</span><span class="sxs-lookup"><span data-stu-id="bae56-133">Copy the text for the [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) script to your local machine and save it as a PowerShell cmdlet (e.g. `APIAuth.ps1`) and execute it `.\APIAuth.ps1`.</span></span> 
6. <span data-ttu-id="bae56-134">The script will ask you to provide an input for **principalName**.</span><span class="sxs-lookup"><span data-stu-id="bae56-134">The script will ask you to provide an input for **principalName**.</span></span> <span data-ttu-id="bae56-135">Provide a suitable name here that you want to use to create your Active Directory application (e.g. APIAuth).</span><span class="sxs-lookup"><span data-stu-id="bae56-135">Provide a suitable name here that you want to use to create your Active Directory application (e.g. APIAuth).</span></span> 
7. <span data-ttu-id="bae56-136">After the script completes, it will display the following four values that you will need to authenticate programmatically with AD so make sure to copy them.</span><span class="sxs-lookup"><span data-stu-id="bae56-136">After the script completes, it will display the following four values that you will need to authenticate programmatically with AD so make sure to copy them.</span></span> 
   
    <span data-ttu-id="bae56-137">**TenantId**, **SubscriptionId**, **ApplicationId**, and **Secret**.</span><span class="sxs-lookup"><span data-stu-id="bae56-137">**TenantId**, **SubscriptionId**, **ApplicationId**, and **Secret**.</span></span>
   
    <span data-ttu-id="bae56-138">You will use TenantId as `{TENANT_ID}`, ApplicationId as `{CLIENT_ID}` and Secret as `{CLIENT_SECRET}`.</span><span class="sxs-lookup"><span data-stu-id="bae56-138">You will use TenantId as `{TENANT_ID}`, ApplicationId as `{CLIENT_ID}` and Secret as `{CLIENT_SECRET}`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bae56-139">Your default security policy may block you from running a PowerShell scripts.</span><span class="sxs-lookup"><span data-stu-id="bae56-139">Your default security policy may block you from running a PowerShell scripts.</span></span> <span data-ttu-id="bae56-140">If so, you temporarily configure your execution policy to allow script execution using the following command:</span><span class="sxs-lookup"><span data-stu-id="bae56-140">If so, you temporarily configure your execution policy to allow script execution using the following command:</span></span>
   > 
   > <span data-ttu-id="bae56-141">Set-ExecutionPolicy RemoteSigned</span><span class="sxs-lookup"><span data-stu-id="bae56-141">Set-ExecutionPolicy RemoteSigned</span></span>
   > 
   > 
8. <span data-ttu-id="bae56-142">Here is how the set of PS cmdlets would look like.</span><span class="sxs-lookup"><span data-stu-id="bae56-142">Here is how the set of PS cmdlets would look like.</span></span> 
   
    ![][3]
9. <span data-ttu-id="bae56-143">Check in the Azure Management portal that a new AD application was created with the name you provided to the script called **principalName** under **Show Applications my company owns**.</span><span class="sxs-lookup"><span data-stu-id="bae56-143">Check in the Azure Management portal that a new AD application was created with the name you provided to the script called **principalName** under **Show Applications my company owns**.</span></span>
   
    ![][4]

#### <a name="steps-to-get-a-valid-token"></a><span data-ttu-id="bae56-144">Steps to get a valid token</span><span class="sxs-lookup"><span data-stu-id="bae56-144">Steps to get a valid token</span></span>
1. <span data-ttu-id="bae56-145">Call the API with the following parameters and make sure to replace the TENANT\_ID, CLIENT\_ID and CLIENT\_SECRET:</span><span class="sxs-lookup"><span data-stu-id="bae56-145">Call the API with the following parameters and make sure to replace the TENANT\_ID, CLIENT\_ID and CLIENT\_SECRET:</span></span>
   
   * <span data-ttu-id="bae56-146">**Request URL** as *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span><span class="sxs-lookup"><span data-stu-id="bae56-146">**Request URL** as *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span></span>
   * <span data-ttu-id="bae56-147">**HTTP Content-Type header** as *application/x-www-form-urlencoded*</span><span class="sxs-lookup"><span data-stu-id="bae56-147">**HTTP Content-Type header** as *application/x-www-form-urlencoded*</span></span>
   * <span data-ttu-id="bae56-148">**HTTP Request Body** as *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span><span class="sxs-lookup"><span data-stu-id="bae56-148">**HTTP Request Body** as *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span></span>
     
     <span data-ttu-id="bae56-149">The following is an example request:</span><span class="sxs-lookup"><span data-stu-id="bae56-149">The following is an example request:</span></span>
     
       <span data-ttu-id="bae56-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span><span class="sxs-lookup"><span data-stu-id="bae56-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span></span>
     
     <span data-ttu-id="bae56-151">Here is an example response:</span><span class="sxs-lookup"><span data-stu-id="bae56-151">Here is an example response:</span></span>
     
       <span data-ttu-id="bae56-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span><span class="sxs-lookup"><span data-stu-id="bae56-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span></span>
     
       <span data-ttu-id="bae56-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span><span class="sxs-lookup"><span data-stu-id="bae56-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span></span>
     
     <span data-ttu-id="bae56-154">This example included URL encoding of the POST parameters, `resource` value is actually `https://management.core.windows.net/`.</span><span class="sxs-lookup"><span data-stu-id="bae56-154">This example included URL encoding of the POST parameters, `resource` value is actually `https://management.core.windows.net/`.</span></span> <span data-ttu-id="bae56-155">Be careful to also URL encode `{CLIENT_SECRET}` as it may contain special characters.</span><span class="sxs-lookup"><span data-stu-id="bae56-155">Be careful to also URL encode `{CLIENT_SECRET}` as it may contain special characters.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="bae56-156">For testing, you can use an HTTP client tool like [Fiddler](http://www.telerik.com/fiddler) or [Chrome Postman extension](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span><span class="sxs-lookup"><span data-stu-id="bae56-156">For testing, you can use an HTTP client tool like [Fiddler](http://www.telerik.com/fiddler) or [Chrome Postman extension](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span></span> 
     > 
     > 
2. <span data-ttu-id="bae56-157">Now in every API call, include the authorization request header:</span><span class="sxs-lookup"><span data-stu-id="bae56-157">Now in every API call, include the authorization request header:</span></span>
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    <span data-ttu-id="bae56-158">If you get a 401 status code returned, check the response body, it might tell you the token is expired.</span><span class="sxs-lookup"><span data-stu-id="bae56-158">If you get a 401 status code returned, check the response body, it might tell you the token is expired.</span></span> <span data-ttu-id="bae56-159">In that case, get a new token.</span><span class="sxs-lookup"><span data-stu-id="bae56-159">In that case, get a new token.</span></span>

## <a name="using-the-apis"></a><span data-ttu-id="bae56-160">Using the APIs</span><span class="sxs-lookup"><span data-stu-id="bae56-160">Using the APIs</span></span>
<span data-ttu-id="bae56-161">Now that you have a valid token, you are ready to make the API calls.</span><span class="sxs-lookup"><span data-stu-id="bae56-161">Now that you have a valid token, you are ready to make the API calls.</span></span>

1. <span data-ttu-id="bae56-162">In each API request, you will need to pass a valid, unexpired token which you obtained in the previous section.</span><span class="sxs-lookup"><span data-stu-id="bae56-162">In each API request, you will need to pass a valid, unexpired token which you obtained in the previous section.</span></span>
2. <span data-ttu-id="bae56-163">You will need to plug in some parameters into the request URI which identifies your application.</span><span class="sxs-lookup"><span data-stu-id="bae56-163">You will need to plug in some parameters into the request URI which identifies your application.</span></span> <span data-ttu-id="bae56-164">The request URI looks like the following</span><span class="sxs-lookup"><span data-stu-id="bae56-164">The request URI looks like the following</span></span>
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    <span data-ttu-id="bae56-165">To get the parameters, click on your application name and click Dashboard and you will see a page like the following with all the 3 parameters.</span><span class="sxs-lookup"><span data-stu-id="bae56-165">To get the parameters, click on your application name and click Dashboard and you will see a page like the following with all the 3 parameters.</span></span>
   
   * <span data-ttu-id="bae56-166">**1** `{subscription-id}`</span><span class="sxs-lookup"><span data-stu-id="bae56-166">**1** `{subscription-id}`</span></span>
   * <span data-ttu-id="bae56-167">**2** `{app-collection}`</span><span class="sxs-lookup"><span data-stu-id="bae56-167">**2** `{app-collection}`</span></span>
   * <span data-ttu-id="bae56-168">**3** `{app-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="bae56-168">**3** `{app-resource-name}`</span></span>
   * <span data-ttu-id="bae56-169">**4** Your Resource Group name is going to be **MobileEngagement** unless you created a new one.</span><span class="sxs-lookup"><span data-stu-id="bae56-169">**4** Your Resource Group name is going to be **MobileEngagement** unless you created a new one.</span></span> 
     
     ![Mobile Engagement API URI parameters][2]

> [!NOTE]
> <br/>
> 
> 1. <span data-ttu-id="bae56-171">Ignore the API Root Address as this was for the previous APIs.</span><span class="sxs-lookup"><span data-stu-id="bae56-171">Ignore the API Root Address as this was for the previous APIs.</span></span><br/>
> 2. <span data-ttu-id="bae56-172">If you created the app using Azure Classic portal then you need to use the Application Resource name which is different than the Application name itself.</span><span class="sxs-lookup"><span data-stu-id="bae56-172">If you created the app using Azure Classic portal then you need to use the Application Resource name which is different than the Application name itself.</span></span> <span data-ttu-id="bae56-173">If you created the app in the Azure Portal then you should use the App Name itself (there is no differentiation between Application Resource Name and App Name for apps created in the new portal).</span><span class="sxs-lookup"><span data-stu-id="bae56-173">If you created the app in the Azure Portal then you should use the App Name itself (there is no differentiation between Application Resource Name and App Name for apps created in the new portal).</span></span>  
> 
> 

<!-- Images -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication/azure-module.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-api-authentication/ad-app-creation.png







