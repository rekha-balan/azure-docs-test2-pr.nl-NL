---
title: Get started with delivering content on demand using REST | Microsoft Docs
description: This tutorial walks you through the steps of implementing an on demand content delivery application with Azure Media Services using REST API.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 88194b59-e479-43ac-b179-af4f295e3780
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: juliako
ms.openlocfilehash: 9a0d5805347b404c2e93d60d282bce159e6688c9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550326"
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a><span data-ttu-id="d89b1-103">Get started with delivering content on demand using REST</span><span class="sxs-lookup"><span data-stu-id="d89b1-103">Get started with delivering content on demand using REST</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="d89b1-104">This quickstart walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span><span class="sxs-lookup"><span data-stu-id="d89b1-104">This quickstart walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span></span>

<span data-ttu-id="d89b1-105">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span><span class="sxs-lookup"><span data-stu-id="d89b1-105">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="d89b1-106">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span><span class="sxs-lookup"><span data-stu-id="d89b1-106">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

<span data-ttu-id="d89b1-107">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span><span class="sxs-lookup"><span data-stu-id="d89b1-107">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span></span>

<span data-ttu-id="d89b1-108">Click the image to view it full size.</span><span class="sxs-lookup"><span data-stu-id="d89b1-108">Click the image to view it full size.</span></span>  

<a href="https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a><span data-ttu-id="d89b1-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d89b1-109">Prerequisites</span></span>
<span data-ttu-id="d89b1-110">The following prerequisites are required to start developing with Media Services with REST APIs.</span><span class="sxs-lookup"><span data-stu-id="d89b1-110">The following prerequisites are required to start developing with Media Services with REST APIs.</span></span>

* <span data-ttu-id="d89b1-111">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="d89b1-111">An Azure account.</span></span> <span data-ttu-id="d89b1-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d89b1-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d89b1-113">A Media Services account.</span><span class="sxs-lookup"><span data-stu-id="d89b1-113">A Media Services account.</span></span> <span data-ttu-id="d89b1-114">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="d89b1-114">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="d89b1-115">Understanding of how to develop with Media Services REST API.</span><span class="sxs-lookup"><span data-stu-id="d89b1-115">Understanding of how to develop with Media Services REST API.</span></span> <span data-ttu-id="d89b1-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="d89b1-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="d89b1-117">An application of your choice that can send HTTP requests and responses.</span><span class="sxs-lookup"><span data-stu-id="d89b1-117">An application of your choice that can send HTTP requests and responses.</span></span> <span data-ttu-id="d89b1-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="d89b1-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span></span>

<span data-ttu-id="d89b1-119">The following tasks are shown in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="d89b1-119">The following tasks are shown in this quickstart.</span></span>

1. <span data-ttu-id="d89b1-120">Start streaming endpoint (using the Azure portal).</span><span class="sxs-lookup"><span data-stu-id="d89b1-120">Start streaming endpoint (using the Azure portal).</span></span>
2. <span data-ttu-id="d89b1-121">Connect to the Media Services account with REST API.</span><span class="sxs-lookup"><span data-stu-id="d89b1-121">Connect to the Media Services account with REST API.</span></span>
3. <span data-ttu-id="d89b1-122">Create a new asset and upload a video file with REST API.</span><span class="sxs-lookup"><span data-stu-id="d89b1-122">Create a new asset and upload a video file with REST API.</span></span>
4. <span data-ttu-id="d89b1-123">Encode the source file into a set of adaptive bitrate MP4 files with REST API.</span><span class="sxs-lookup"><span data-stu-id="d89b1-123">Encode the source file into a set of adaptive bitrate MP4 files with REST API.</span></span>
5. <span data-ttu-id="d89b1-124">Publish the asset and get streaming and progressive download URLs with REST API.</span><span class="sxs-lookup"><span data-stu-id="d89b1-124">Publish the asset and get streaming and progressive download URLs with REST API.</span></span>
6. <span data-ttu-id="d89b1-125">Play your content.</span><span class="sxs-lookup"><span data-stu-id="d89b1-125">Play your content.</span></span>

>[!NOTE]
><span data-ttu-id="d89b1-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="d89b1-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="d89b1-127">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span><span class="sxs-lookup"><span data-stu-id="d89b1-127">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="d89b1-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span><span class="sxs-lookup"><span data-stu-id="d89b1-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>


<span data-ttu-id="d89b1-129">For details about AMS REST entities used in this topic, see [Azure Media Services REST API Reference](/rest/api/media/services/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="d89b1-129">For details about AMS REST entities used in this topic, see [Azure Media Services REST API Reference](/rest/api/media/services/azure-media-services-rest-api-reference).</span></span> <span data-ttu-id="d89b1-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="d89b1-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span></span>

## <a name="start-streaming-endpoints-using-the-azure-portal"></a><span data-ttu-id="d89b1-131">Start streaming endpoints using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d89b1-131">Start streaming endpoints using the Azure portal</span></span>

<span data-ttu-id="d89b1-132">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span><span class="sxs-lookup"><span data-stu-id="d89b1-132">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="d89b1-133">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span><span class="sxs-lookup"><span data-stu-id="d89b1-133">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="d89b1-134">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span><span class="sxs-lookup"><span data-stu-id="d89b1-134">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="d89b1-135">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span><span class="sxs-lookup"><span data-stu-id="d89b1-135">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="d89b1-136">To start the streaming endpoint, do the following:</span><span class="sxs-lookup"><span data-stu-id="d89b1-136">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="d89b1-137">Log in at the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d89b1-137">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d89b1-138">In the Settings window, click Streaming endpoints.</span><span class="sxs-lookup"><span data-stu-id="d89b1-138">In the Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="d89b1-139">Click the default streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="d89b1-139">Click the default streaming endpoint.</span></span>

    <span data-ttu-id="d89b1-140">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span><span class="sxs-lookup"><span data-stu-id="d89b1-140">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="d89b1-141">Click the Start icon.</span><span class="sxs-lookup"><span data-stu-id="d89b1-141">Click the Start icon.</span></span>
5. <span data-ttu-id="d89b1-142">Click the Save button to save your changes.</span><span class="sxs-lookup"><span data-stu-id="d89b1-142">Click the Save button to save your changes.</span></span>

## <a id="connect"></a><span data-ttu-id="d89b1-143">Connect to the Media Services account with REST API</span><span class="sxs-lookup"><span data-stu-id="d89b1-143">Connect to the Media Services account with REST API</span></span>
<span data-ttu-id="d89b1-144">Two things are required when accessing Azure Media Services: an access token provided by Azure Access Control Services (ACS), and the URI of Media Services itself.</span><span class="sxs-lookup"><span data-stu-id="d89b1-144">Two things are required when accessing Azure Media Services: an access token provided by Azure Access Control Services (ACS), and the URI of Media Services itself.</span></span> <span data-ttu-id="d89b1-145">You can use any means you want when creating these requests as long as you specify the correct header values and pass in the access token correctly when calling into Media Services.</span><span class="sxs-lookup"><span data-stu-id="d89b1-145">You can use any means you want when creating these requests as long as you specify the correct header values and pass in the access token correctly when calling into Media Services.</span></span>

<span data-ttu-id="d89b1-146">The following steps describe the most common workflow when using the Media Services REST API to connect to Media Services:</span><span class="sxs-lookup"><span data-stu-id="d89b1-146">The following steps describe the most common workflow when using the Media Services REST API to connect to Media Services:</span></span>

1. <span data-ttu-id="d89b1-147">Getting an access token.</span><span class="sxs-lookup"><span data-stu-id="d89b1-147">Getting an access token.</span></span>
2. <span data-ttu-id="d89b1-148">Connecting to the Media Services URI.</span><span class="sxs-lookup"><span data-stu-id="d89b1-148">Connecting to the Media Services URI.</span></span>  

    <span data-ttu-id="d89b1-149">Remember that after successfully connecting to https://media.windows.net, you receive a 301 redirect specifying another Media Services URI.</span><span class="sxs-lookup"><span data-stu-id="d89b1-149">Remember that after successfully connecting to https://media.windows.net, you receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="d89b1-150">You must make subsequent calls to the new URI.</span><span class="sxs-lookup"><span data-stu-id="d89b1-150">You must make subsequent calls to the new URI.</span></span> <span data-ttu-id="d89b1-151">You may also receive a HTTP/1.1 200 response that contains the ODATA API metadata description.</span><span class="sxs-lookup"><span data-stu-id="d89b1-151">You may also receive a HTTP/1.1 200 response that contains the ODATA API metadata description.</span></span>
3. <span data-ttu-id="d89b1-152">Posting your subsequent API calls to the new URL.</span><span class="sxs-lookup"><span data-stu-id="d89b1-152">Posting your subsequent API calls to the new URL.</span></span>

    <span data-ttu-id="d89b1-153">For example, if after trying to connect, you got the following:</span><span class="sxs-lookup"><span data-stu-id="d89b1-153">For example, if after trying to connect, you got the following:</span></span>

        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

    <span data-ttu-id="d89b1-154">You should post your subsequent API calls to https://wamsbayclus001rest-hs.cloudapp.net/api/.</span><span class="sxs-lookup"><span data-stu-id="d89b1-154">You should post your subsequent API calls to https://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

### <a name="getting-an-access-token"></a><span data-ttu-id="d89b1-155">Getting an access token</span><span class="sxs-lookup"><span data-stu-id="d89b1-155">Getting an access token</span></span>
<span data-ttu-id="d89b1-156">To access Media Services directly through the REST API, retrieve an access token from ACS and use it during every HTTP request you make into the service.</span><span class="sxs-lookup"><span data-stu-id="d89b1-156">To access Media Services directly through the REST API, retrieve an access token from ACS and use it during every HTTP request you make into the service.</span></span> <span data-ttu-id="d89b1-157">You do not need any other prerequisites before directly connecting to Media Services.</span><span class="sxs-lookup"><span data-stu-id="d89b1-157">You do not need any other prerequisites before directly connecting to Media Services.</span></span>

<span data-ttu-id="d89b1-158">The following example shows the HTTP request header and body used to retrieve a token.</span><span class="sxs-lookup"><span data-stu-id="d89b1-158">The following example shows the HTTP request header and body used to retrieve a token.</span></span>

<span data-ttu-id="d89b1-159">**Header**:</span><span class="sxs-lookup"><span data-stu-id="d89b1-159">**Header**:</span></span>

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


<span data-ttu-id="d89b1-160">**Body**:</span><span class="sxs-lookup"><span data-stu-id="d89b1-160">**Body**:</span></span>

<span data-ttu-id="d89b1-161">You need to provide the client_id and client_secret values in the body of this request; client_id and client_secret correspond to the AccountName and AccountKey values, respectively.</span><span class="sxs-lookup"><span data-stu-id="d89b1-161">You need to provide the client_id and client_secret values in the body of this request; client_id and client_secret correspond to the AccountName and AccountKey values, respectively.</span></span> <span data-ttu-id="d89b1-162">These values are provided to you by Media Services when you set up your account.</span><span class="sxs-lookup"><span data-stu-id="d89b1-162">These values are provided to you by Media Services when you set up your account.</span></span>

<span data-ttu-id="d89b1-163">The AccountKey for your Media Services account must be URL-encoded when using it as the client_secret value in your access token request.</span><span class="sxs-lookup"><span data-stu-id="d89b1-163">The AccountKey for your Media Services account must be URL-encoded when using it as the client_secret value in your access token request.</span></span>

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="d89b1-164">For example:</span><span class="sxs-lookup"><span data-stu-id="d89b1-164">For example:</span></span>

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="d89b1-165">The following example shows the HTTP response that contains the access token in the response body.</span><span class="sxs-lookup"><span data-stu-id="d89b1-165">The following example shows the HTTP response that contains the access token in the response body.</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache, no-store
    Pragma: no-cache
    Content-Type: application/json; charset=utf-8
    Expires: -1
    request-id: a65150f5-2784-4a01-a4b7-33456187ad83
    X-Content-Type-Options: nosniff
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 15 Jan 2015 08:07:20 GMT
    Content-Length: 670

    {  
       "token_type":"http://schemas.xmlsoap.org/ws/2009/11/swt-token-profile-1.0",
       "access_token":"http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421330840&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=uf69n82KlqZmkJDNxhJkOxpyIpA2HDyeGUTtSnq1vlE%3d",
       "expires_in":"21600",
       "scope":"urn:WindowsAzureMediaServices"
    }


> [!NOTE]
> <span data-ttu-id="d89b1-166">It is recommended to cache the "access_token " and "expires_in" (how long the access token is valid, in seconds) values to an external storage.</span><span class="sxs-lookup"><span data-stu-id="d89b1-166">It is recommended to cache the "access_token " and "expires_in" (how long the access token is valid, in seconds) values to an external storage.</span></span> <span data-ttu-id="d89b1-167">The token data could later be retrieved from the storage and re-used in your Media Services REST API calls.</span><span class="sxs-lookup"><span data-stu-id="d89b1-167">The token data could later be retrieved from the storage and re-used in your Media Services REST API calls.</span></span> <span data-ttu-id="d89b1-168">This is especially useful for scenarios where the token can be securely shared among multiple processes or computers.</span><span class="sxs-lookup"><span data-stu-id="d89b1-168">This is especially useful for scenarios where the token can be securely shared among multiple processes or computers.</span></span>
>
>

<span data-ttu-id="d89b1-169">Make sure to monitor the "expires_in" value of the access token and update your REST API calls with new tokens as needed.</span><span class="sxs-lookup"><span data-stu-id="d89b1-169">Make sure to monitor the "expires_in" value of the access token and update your REST API calls with new tokens as needed.</span></span>

### <a name="connecting-to-the-media-services-uri"></a><span data-ttu-id="d89b1-170">Connecting to the Media Services URI</span><span class="sxs-lookup"><span data-stu-id="d89b1-170">Connecting to the Media Services URI</span></span>

<span data-ttu-id="d89b1-171">The root URI for Media Services is https://media.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="d89b1-171">The root URI for Media Services is https://media.windows.net/.</span></span> <span data-ttu-id="d89b1-172">You should initially connect to this URI, and if you get a 301 redirect back in response, you should make subsequent calls to the new URI.</span><span class="sxs-lookup"><span data-stu-id="d89b1-172">You should initially connect to this URI, and if you get a 301 redirect back in response, you should make subsequent calls to the new URI.</span></span> <span data-ttu-id="d89b1-173">In addition, do not use any auto-redirect/follow logic in your requests.</span><span class="sxs-lookup"><span data-stu-id="d89b1-173">In addition, do not use any auto-redirect/follow logic in your requests.</span></span> <span data-ttu-id="d89b1-174">HTTP verbs and request bodies will not be forwarded to the new URI.</span><span class="sxs-lookup"><span data-stu-id="d89b1-174">HTTP verbs and request bodies will not be forwarded to the new URI.</span></span>

<span data-ttu-id="d89b1-175">The root URI for uploading and downloading Asset files is https://yourstorageaccount.blob.core.windows.net/ where the storage account name is the same one you used during your Media Services account setup.</span><span class="sxs-lookup"><span data-stu-id="d89b1-175">The root URI for uploading and downloading Asset files is https://yourstorageaccount.blob.core.windows.net/ where the storage account name is the same one you used during your Media Services account setup.</span></span>

<span data-ttu-id="d89b1-176">The following example demonstrates HTTP request to the Media Services root URI (https://media.windows.net/).</span><span class="sxs-lookup"><span data-stu-id="d89b1-176">The following example demonstrates HTTP request to the Media Services root URI (https://media.windows.net/).</span></span> <span data-ttu-id="d89b1-177">The request gets a 301 redirect back in response.</span><span class="sxs-lookup"><span data-stu-id="d89b1-177">The request gets a 301 redirect back in response.</span></span> <span data-ttu-id="d89b1-178">The subsequent request is using the new URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span><span class="sxs-lookup"><span data-stu-id="d89b1-178">The subsequent request is using the new URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span></span>     

<span data-ttu-id="d89b1-179">**HTTP Request**:</span><span class="sxs-lookup"><span data-stu-id="d89b1-179">**HTTP Request**:</span></span>

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


<span data-ttu-id="d89b1-180">**HTTP Response**:</span><span class="sxs-lookup"><span data-stu-id="d89b1-180">**HTTP Response**:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
    Server: Microsoft-IIS/8.5
    request-id: 987d7652-497a-44e5-b815-f492e02aef97
    x-ms-request-id: 987d7652-497a-44e5-b815-f492e02aef97
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:53 GMT
    Content-Length: 164

    <html><head><title>Object moved</title></head><body>
    <h2>Object moved to <a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


<span data-ttu-id="d89b1-181">**HTTP Request** (using the new URI):</span><span class="sxs-lookup"><span data-stu-id="d89b1-181">**HTTP Request** (using the new URI):</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="d89b1-182">**HTTP Response**:</span><span class="sxs-lookup"><span data-stu-id="d89b1-182">**HTTP Response**:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1250
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    x-ms-request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata","value":[{"name":"AccessPolicies","url":"AccessPolicies"},{"name":"Locators","url":"Locators"},{"name":"ContentKeys","url":"ContentKeys"},{"name":"ContentKeyAuthorizationPolicyOptions","url":"ContentKeyAuthorizationPolicyOptions"},{"name":"ContentKeyAuthorizationPolicies","url":"ContentKeyAuthorizationPolicies"},{"name":"Files","url":"Files"},{"name":"Assets","url":"Assets"},{"name":"AssetDeliveryPolicies","url":"AssetDeliveryPolicies"},{"name":"IngestManifestFiles","url":"IngestManifestFiles"},{"name":"IngestManifestAssets","url":"IngestManifestAssets"},{"name":"IngestManifests","url":"IngestManifests"},{"name":"StorageAccounts","url":"StorageAccounts"},{"name":"Tasks","url":"Tasks"},{"name":"NotificationEndPoints","url":"NotificationEndPoints"},{"name":"Jobs","url":"Jobs"},{"name":"TaskTemplates","url":"TaskTemplates"},{"name":"JobTemplates","url":"JobTemplates"},{"name":"MediaProcessors","url":"MediaProcessors"},{"name":"EncodingReservedUnitTypes","url":"EncodingReservedUnitTypes"},{"name":"Operations","url":"Operations"},{"name":"StreamingEndpoints","url":"StreamingEndpoints"},{"name":"Channels","url":"Channels"},{"name":"Programs","url":"Programs"}]}



> [!NOTE]
> <span data-ttu-id="d89b1-183">From now on the new URI is used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="d89b1-183">From now on the new URI is used in this tutorial.</span></span>
>
>

## <a id="upload"></a><span data-ttu-id="d89b1-184">Create a new asset and upload a video file with REST API</span><span class="sxs-lookup"><span data-stu-id="d89b1-184">Create a new asset and upload a video file with REST API</span></span>

<span data-ttu-id="d89b1-185">In Media Services, you upload your digital files into an asset.</span><span class="sxs-lookup"><span data-stu-id="d89b1-185">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="d89b1-186">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span><span class="sxs-lookup"><span data-stu-id="d89b1-186">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="d89b1-187">One of the values that you have to provide when creating an asset is asset creation options.</span><span class="sxs-lookup"><span data-stu-id="d89b1-187">One of the values that you have to provide when creating an asset is asset creation options.</span></span> <span data-ttu-id="d89b1-188">The **Options** property is an enumeration value that describes the encryption options that an Asset can be created with.</span><span class="sxs-lookup"><span data-stu-id="d89b1-188">The **Options** property is an enumeration value that describes the encryption options that an Asset can be created with.</span></span> <span data-ttu-id="d89b1-189">A valid value is one of the values from the list below, not a combination of values from this list:</span><span class="sxs-lookup"><span data-stu-id="d89b1-189">A valid value is one of the values from the list below, not a combination of values from this list:</span></span>

* <span data-ttu-id="d89b1-190">**None** = **0** - No encryption is used.</span><span class="sxs-lookup"><span data-stu-id="d89b1-190">**None** = **0** - No encryption is used.</span></span> <span data-ttu-id="d89b1-191">When using this option your content is not protected in transit or at rest in storage.</span><span class="sxs-lookup"><span data-stu-id="d89b1-191">When using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="d89b1-192">If you plan to deliver an MP4 using progressive download, use this option.</span><span class="sxs-lookup"><span data-stu-id="d89b1-192">If you plan to deliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="d89b1-193">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it to Azure Storage where it is stored encrypted at rest.</span><span class="sxs-lookup"><span data-stu-id="d89b1-193">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="d89b1-194">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span><span class="sxs-lookup"><span data-stu-id="d89b1-194">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="d89b1-195">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span><span class="sxs-lookup"><span data-stu-id="d89b1-195">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="d89b1-196">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="d89b1-196">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="d89b1-197">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span><span class="sxs-lookup"><span data-stu-id="d89b1-197">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="d89b1-198">The files must have been encoded and encrypted by Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="d89b1-198">The files must have been encoded and encrypted by Transform Manager.</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="d89b1-199">Create an asset</span><span class="sxs-lookup"><span data-stu-id="d89b1-199">Create an asset</span></span>
<span data-ttu-id="d89b1-200">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span><span class="sxs-lookup"><span data-stu-id="d89b1-200">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="d89b1-201">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span><span class="sxs-lookup"><span data-stu-id="d89b1-201">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span></span>

<span data-ttu-id="d89b1-202">The following example shows how to create an asset.</span><span class="sxs-lookup"><span data-stu-id="d89b1-202">The following example shows how to create an asset.</span></span>

<span data-ttu-id="d89b1-203">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="d89b1-203">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 45

    {"Name":"BigBuckBunny.mp4", "Options":"0"}


<span data-ttu-id="d89b1-204">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="d89b1-204">**HTTP Response**</span></span>

<span data-ttu-id="d89b1-205">If successful, the following is returned:</span><span class="sxs-lookup"><span data-stu-id="d89b1-205">If successful, the following is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny2.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="d89b1-206">Create an AssetFile</span><span class="sxs-lookup"><span data-stu-id="d89b1-206">Create an AssetFile</span></span>
<span data-ttu-id="d89b1-207">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span><span class="sxs-lookup"><span data-stu-id="d89b1-207">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="d89b1-208">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span><span class="sxs-lookup"><span data-stu-id="d89b1-208">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span></span> <span data-ttu-id="d89b1-209">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span><span class="sxs-lookup"><span data-stu-id="d89b1-209">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="d89b1-210">After you upload your digital media file into a blob container, you use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span><span class="sxs-lookup"><span data-stu-id="d89b1-210">After you upload your digital media file into a blob container, you use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span></span>

<span data-ttu-id="d89b1-211">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="d89b1-211">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="d89b1-212">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="d89b1-212">**HTTP Response**</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion":null,
       "EncryptionScheme":null,
       "IsEncrypted":false,
       "EncryptionKeyId":null,
       "InitializationVector":null,
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }


### <a name="creating-the-accesspolicy-with-write-permission"></a><span data-ttu-id="d89b1-213">Creating the AccessPolicy with write permission</span><span class="sxs-lookup"><span data-stu-id="d89b1-213">Creating the AccessPolicy with write permission</span></span>
<span data-ttu-id="d89b1-214">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span><span class="sxs-lookup"><span data-stu-id="d89b1-214">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span></span> <span data-ttu-id="d89b1-215">To do that, POST an HTTP request to the AccessPolicies entity set.</span><span class="sxs-lookup"><span data-stu-id="d89b1-215">To do that, POST an HTTP request to the AccessPolicies entity set.</span></span> <span data-ttu-id="d89b1-216">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span><span class="sxs-lookup"><span data-stu-id="d89b1-216">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="d89b1-217">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="d89b1-217">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="d89b1-218">The following example shows how to create an AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="d89b1-218">The following example shows how to create an AccessPolicy:</span></span>

<span data-ttu-id="d89b1-219">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="d89b1-219">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 74

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"}

<span data-ttu-id="d89b1-220">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="d89b1-220">**HTTP Response**</span></span>

<span data-ttu-id="d89b1-221">If successful, the following response is returned:</span><span class="sxs-lookup"><span data-stu-id="d89b1-221">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 312
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae')
    Server: Microsoft-IIS/8.5
    request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    x-ms-request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:18:06 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#AccessPolicies/@Element",
       "Id":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "Created":"2015-01-18T22:18:06.6370575Z",
       "LastModified":"2015-01-18T22:18:06.6370575Z",
       "Name":"NewUploadPolicy",
       "DurationInMinutes":440.0,
       "Permissions":2
    }

### <a name="get-the-upload-url"></a><span data-ttu-id="d89b1-222">Get the Upload URL</span><span class="sxs-lookup"><span data-stu-id="d89b1-222">Get the Upload URL</span></span>

<span data-ttu-id="d89b1-223">To receive the actual upload URL, create a SAS Locator.</span><span class="sxs-lookup"><span data-stu-id="d89b1-223">To receive the actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="d89b1-224">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span><span class="sxs-lookup"><span data-stu-id="d89b1-224">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span></span> <span data-ttu-id="d89b1-225">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span><span class="sxs-lookup"><span data-stu-id="d89b1-225">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span></span> <span data-ttu-id="d89b1-226">Each of these Locators uses the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span><span class="sxs-lookup"><span data-stu-id="d89b1-226">Each of these Locators uses the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span></span> <span data-ttu-id="d89b1-227">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="d89b1-227">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="d89b1-228">A SAS URL has the following format:</span><span class="sxs-lookup"><span data-stu-id="d89b1-228">A SAS URL has the following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="d89b1-229">Some considerations apply:</span><span class="sxs-lookup"><span data-stu-id="d89b1-229">Some considerations apply:</span></span>

* <span data-ttu-id="d89b1-230">You cannot have more than five unique Locators associated with a given Asset at one time.</span><span class="sxs-lookup"><span data-stu-id="d89b1-230">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="d89b1-231">For more information, see Locator.</span><span class="sxs-lookup"><span data-stu-id="d89b1-231">For more information, see Locator.</span></span>
* <span data-ttu-id="d89b1-232">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span><span class="sxs-lookup"><span data-stu-id="d89b1-232">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="d89b1-233">This is because there may be clock skew between your client machine and Media Services.</span><span class="sxs-lookup"><span data-stu-id="d89b1-233">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="d89b1-234">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="d89b1-234">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="d89b1-235">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span><span class="sxs-lookup"><span data-stu-id="d89b1-235">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span></span> <span data-ttu-id="d89b1-236">This issue applies to both SAS URL and Origin Locators.</span><span class="sxs-lookup"><span data-stu-id="d89b1-236">This issue applies to both SAS URL and Origin Locators.</span></span>

<span data-ttu-id="d89b1-237">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span><span class="sxs-lookup"><span data-stu-id="d89b1-237">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="d89b1-238">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span><span class="sxs-lookup"><span data-stu-id="d89b1-238">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="d89b1-239">The **Path** property returned contains the URL that you must use to upload your file.</span><span class="sxs-lookup"><span data-stu-id="d89b1-239">The **Path** property returned contains the URL that you must use to upload your file.</span></span>

<span data-ttu-id="d89b1-240">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="d89b1-240">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 178

    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }


<span data-ttu-id="d89b1-241">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="d89b1-241">**HTTP Response**</span></span>

<span data-ttu-id="d89b1-242">If successful, the following response is returned:</span><span class="sxs-lookup"><span data-stu-id="d89b1-242">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 949
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54')
    Server: Microsoft-IIS/8.5
    request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    x-ms-request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 03:01:29 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Locators/@Element",
       "Id":"nb:lid:UUID:af57bdd8-6751-4e84-b403-f3c140444b54",
       "ExpirationDateTime":"2015-02-19T00:05:53",
       "Type":1,
       "Path":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "BaseUri":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247",
       "ContentAccessComponent":"?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Name":null
    }

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="d89b1-243">Upload a file into a blob storage container</span><span class="sxs-lookup"><span data-stu-id="d89b1-243">Upload a file into a blob storage container</span></span>
<span data-ttu-id="d89b1-244">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure blob storage container using the Azure Storage REST APIs.</span><span class="sxs-lookup"><span data-stu-id="d89b1-244">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure blob storage container using the Azure Storage REST APIs.</span></span> <span data-ttu-id="d89b1-245">You must upload the files as block blobs.</span><span class="sxs-lookup"><span data-stu-id="d89b1-245">You must upload the files as block blobs.</span></span> <span data-ttu-id="d89b1-246">Page blobs are not supported by Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="d89b1-246">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="d89b1-247">You must add the file name for the file you want to upload to the Locator **Path** value received in the previous section.</span><span class="sxs-lookup"><span data-stu-id="d89b1-247">You must add the file name for the file you want to upload to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="d89b1-248">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="d89b1-248">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="d89b1-249">.</span><span class="sxs-lookup"><span data-stu-id="d89b1-249">.</span></span> <span data-ttu-id="d89b1-250">.</span><span class="sxs-lookup"><span data-stu-id="d89b1-250">.</span></span> <span data-ttu-id="d89b1-251">.</span><span class="sxs-lookup"><span data-stu-id="d89b1-251">.</span></span>
>
>

<span data-ttu-id="d89b1-252">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="d89b1-252">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/Blob-Service-REST-API).</span></span>

### <a name="update-the-assetfile"></a><span data-ttu-id="d89b1-253">Update the AssetFile</span><span class="sxs-lookup"><span data-stu-id="d89b1-253">Update the AssetFile</span></span>
<span data-ttu-id="d89b1-254">Now that you've uploaded your file, update the FileAsset size (and other) information.</span><span class="sxs-lookup"><span data-stu-id="d89b1-254">Now that you've uploaded your file, update the FileAsset size (and other) information.</span></span> <span data-ttu-id="d89b1-255">For example:</span><span class="sxs-lookup"><span data-stu-id="d89b1-255">For example:</span></span>

    MERGE https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="d89b1-256">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="d89b1-256">**HTTP Response**</span></span>

<span data-ttu-id="d89b1-257">If successful, the following is returned:</span><span class="sxs-lookup"><span data-stu-id="d89b1-257">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a name="delete-the-locator-and-accesspolicy"></a><span data-ttu-id="d89b1-258">Delete the Locator and AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="d89b1-258">Delete the Locator and AccessPolicy</span></span>
<span data-ttu-id="d89b1-259">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="d89b1-259">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="d89b1-260">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="d89b1-260">**HTTP Response**</span></span>

<span data-ttu-id="d89b1-261">If successful, the following is returned:</span><span class="sxs-lookup"><span data-stu-id="d89b1-261">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

<span data-ttu-id="d89b1-262">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="d89b1-262">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

<span data-ttu-id="d89b1-263">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="d89b1-263">**HTTP Response**</span></span>

<span data-ttu-id="d89b1-264">If successful, the following is returned:</span><span class="sxs-lookup"><span data-stu-id="d89b1-264">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a id="encode"></a><span data-ttu-id="d89b1-265">Encode the source file into a set of adaptive bitrate MP4 files</span><span class="sxs-lookup"><span data-stu-id="d89b1-265">Encode the source file into a set of adaptive bitrate MP4 files</span></span>

<span data-ttu-id="d89b1-266">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span><span class="sxs-lookup"><span data-stu-id="d89b1-266">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span></span> <span data-ttu-id="d89b1-267">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span><span class="sxs-lookup"><span data-stu-id="d89b1-267">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span></span> <span data-ttu-id="d89b1-268">These activities are called Jobs and each Job is composed of atomic Tasks that do the actual work on the Asset file (for more information, see [Job](/rest/api/media/services/job), [Task](/rest/api/media/services/task) descriptions).</span><span class="sxs-lookup"><span data-stu-id="d89b1-268">These activities are called Jobs and each Job is composed of atomic Tasks that do the actual work on the Asset file (for more information, see [Job](/rest/api/media/services/job), [Task](/rest/api/media/services/task) descriptions).</span></span>

<span data-ttu-id="d89b1-269">As was mentioned earlier, when working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span><span class="sxs-lookup"><span data-stu-id="d89b1-269">As was mentioned earlier, when working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="d89b1-270">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="d89b1-270">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span>

<span data-ttu-id="d89b1-271">The following section shows how to create a job that contains one encoding task.</span><span class="sxs-lookup"><span data-stu-id="d89b1-271">The following section shows how to create a job that contains one encoding task.</span></span> <span data-ttu-id="d89b1-272">The task specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="d89b1-272">The task specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="d89b1-273">The section also shows how to monitor the job processing progress.</span><span class="sxs-lookup"><span data-stu-id="d89b1-273">The section also shows how to monitor the job processing progress.</span></span> <span data-ttu-id="d89b1-274">When the job is complete, you would be able to create locators that are needed to get access to your assets.</span><span class="sxs-lookup"><span data-stu-id="d89b1-274">When the job is complete, you would be able to create locators that are needed to get access to your assets.</span></span>

### <a name="get-a-media-processor"></a><span data-ttu-id="d89b1-275">Get a media processor</span><span class="sxs-lookup"><span data-stu-id="d89b1-275">Get a media processor</span></span>
<span data-ttu-id="d89b1-276">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span><span class="sxs-lookup"><span data-stu-id="d89b1-276">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="d89b1-277">For the encoding task shown in this tutorial, we are going to use the Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="d89b1-277">For the encoding task shown in this tutorial, we are going to use the Media Encoder Standard.</span></span>

<span data-ttu-id="d89b1-278">The following code requests the encoder's id.</span><span class="sxs-lookup"><span data-stu-id="d89b1-278">The following code requests the encoder's id.</span></span>

<span data-ttu-id="d89b1-279">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="d89b1-279">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="d89b1-280">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="d89b1-280">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 273
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    x-ms-request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 07:54:09 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

### <a name="create-a-job"></a><span data-ttu-id="d89b1-281">Create a job</span><span class="sxs-lookup"><span data-stu-id="d89b1-281">Create a job</span></span>
<span data-ttu-id="d89b1-282">Each Job can have one or more Tasks depending on the type of processing that you want to accomplish.</span><span class="sxs-lookup"><span data-stu-id="d89b1-282">Each Job can have one or more Tasks depending on the type of processing that you want to accomplish.</span></span> <span data-ttu-id="d89b1-283">Through the REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through the Tasks navigation property on Job entities, or through OData batch processing.</span><span class="sxs-lookup"><span data-stu-id="d89b1-283">Through the REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through the Tasks navigation property on Job entities, or through OData batch processing.</span></span> <span data-ttu-id="d89b1-284">The Media Services SDK uses batch processing.</span><span class="sxs-lookup"><span data-stu-id="d89b1-284">The Media Services SDK uses batch processing.</span></span> <span data-ttu-id="d89b1-285">However, for the readability of the code examples in this topic, tasks are defined inline.</span><span class="sxs-lookup"><span data-stu-id="d89b1-285">However, for the readability of the code examples in this topic, tasks are defined inline.</span></span> <span data-ttu-id="d89b1-286">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="d89b1-286">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

<span data-ttu-id="d89b1-287">The following example shows you how to create and post a Job with one Task set to encode a video at a specific resolution and quality.</span><span class="sxs-lookup"><span data-stu-id="d89b1-287">The following example shows you how to create and post a Job with one Task set to encode a video at a specific resolution and quality.</span></span> <span data-ttu-id="d89b1-288">The following documentation section contains the list of all the [task presets](http://msdn.microsoft.com/library/mt269960) supported by the Media Encoder Standard processor.</span><span class="sxs-lookup"><span data-stu-id="d89b1-288">The following documentation section contains the list of all the [task presets](http://msdn.microsoft.com/library/mt269960) supported by the Media Encoder Standard processor.</span></span>  

<span data-ttu-id="d89b1-289">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="d89b1-289">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: application/json
    Accept: application/json;odata=verbose
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 482

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"Adaptive Streaming",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset>
                <outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          }
       ]
    }

<span data-ttu-id="d89b1-290">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="d89b1-290">**HTTP Response**</span></span>

<span data-ttu-id="d89b1-291">If successful, the following response is returned:</span><span class="sxs-lookup"><span data-stu-id="d89b1-291">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1215
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')
    Server: Microsoft-IIS/8.5
    request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    x-ms-request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:04:35 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Job"
          },
          "Tasks":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Tasks"
             }
          },
          "OutputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets"
             }
          },
          "InputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')/InputMediaAssets"
             }
          },
          "Id":"nb:jid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "Name":"NewTestJob",
          "Created":"2015-01-19T08:04:34.3287057Z",
          "LastModified":"2015-01-19T08:04:34.3287057Z",
          "EndTime":null,
          "Priority":0,
          "RunningDuration":0,
          "StartTime":null,
          "State":0,
          "TemplateId":null,
          "JobNotificationSubscriptions":{  
             "__metadata":{  
                "type":"Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.JobNotificationSubscription)"
             },
             "results":[  

             ]
          }
       }
    }


<span data-ttu-id="d89b1-292">There are a few important things to note in any Job request:</span><span class="sxs-lookup"><span data-stu-id="d89b1-292">There are a few important things to note in any Job request:</span></span>

* <span data-ttu-id="d89b1-293">TaskBody properties MUST use literal XML to define the number of input, or output assets that are used by the Task.</span><span class="sxs-lookup"><span data-stu-id="d89b1-293">TaskBody properties MUST use literal XML to define the number of input, or output assets that are used by the Task.</span></span> <span data-ttu-id="d89b1-294">The Task topic contains the XML Schema Definition for the XML.</span><span class="sxs-lookup"><span data-stu-id="d89b1-294">The Task topic contains the XML Schema Definition for the XML.</span></span>
* <span data-ttu-id="d89b1-295">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="d89b1-295">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="d89b1-296">A task can have multiple output assets.</span><span class="sxs-lookup"><span data-stu-id="d89b1-296">A task can have multiple output assets.</span></span> <span data-ttu-id="d89b1-297">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span><span class="sxs-lookup"><span data-stu-id="d89b1-297">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="d89b1-298">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span><span class="sxs-lookup"><span data-stu-id="d89b1-298">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="d89b1-299">Tasks must not form a cycle.</span><span class="sxs-lookup"><span data-stu-id="d89b1-299">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="d89b1-300">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an Asset.</span><span class="sxs-lookup"><span data-stu-id="d89b1-300">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an Asset.</span></span> <span data-ttu-id="d89b1-301">The actual Assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the Job entity definition.</span><span class="sxs-lookup"><span data-stu-id="d89b1-301">The actual Assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the Job entity definition.</span></span>

> [!NOTE]
> <span data-ttu-id="d89b1-302">Because Media Services is built on OData v3, the individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span><span class="sxs-lookup"><span data-stu-id="d89b1-302">Because Media Services is built on OData v3, the individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
>
>

* <span data-ttu-id="d89b1-303">InputMediaAssets maps to one or more Assets you have created in Media Services.</span><span class="sxs-lookup"><span data-stu-id="d89b1-303">InputMediaAssets maps to one or more Assets you have created in Media Services.</span></span> <span data-ttu-id="d89b1-304">OutputMediaAssets are created by the system.</span><span class="sxs-lookup"><span data-stu-id="d89b1-304">OutputMediaAssets are created by the system.</span></span> <span data-ttu-id="d89b1-305">They do not reference an existing asset.</span><span class="sxs-lookup"><span data-stu-id="d89b1-305">They do not reference an existing asset.</span></span>
* <span data-ttu-id="d89b1-306">OutputMediaAssets can be named using the assetName attribute.</span><span class="sxs-lookup"><span data-stu-id="d89b1-306">OutputMediaAssets can be named using the assetName attribute.</span></span> <span data-ttu-id="d89b1-307">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span><span class="sxs-lookup"><span data-stu-id="d89b1-307">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span></span> <span data-ttu-id="d89b1-308">For example, if you set a value for assetName to "Sample", then the OutputMediaAsset Name property would be set to "Sample".</span><span class="sxs-lookup"><span data-stu-id="d89b1-308">For example, if you set a value for assetName to "Sample", then the OutputMediaAsset Name property would be set to "Sample".</span></span> <span data-ttu-id="d89b1-309">However, if you did not set a value for assetName, but did set the job name to "NewJob", then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span><span class="sxs-lookup"><span data-stu-id="d89b1-309">However, if you did not set a value for assetName, but did set the job name to "NewJob", then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span></span>

    <span data-ttu-id="d89b1-310">The following example shows how to set the assetName attribute:</span><span class="sxs-lookup"><span data-stu-id="d89b1-310">The following example shows how to set the assetName attribute:</span></span>

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* <span data-ttu-id="d89b1-311">To enable task chaining:</span><span class="sxs-lookup"><span data-stu-id="d89b1-311">To enable task chaining:</span></span>

  * <span data-ttu-id="d89b1-312">A job must have at least two tasks</span><span class="sxs-lookup"><span data-stu-id="d89b1-312">A job must have at least two tasks</span></span>
  * <span data-ttu-id="d89b1-313">There must be at least one task whose input is output of another task in the job.</span><span class="sxs-lookup"><span data-stu-id="d89b1-313">There must be at least one task whose input is output of another task in the job.</span></span>

<span data-ttu-id="d89b1-314">For more information see, [Creating an Encoding Job with the Media Services REST API](media-services-rest-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="d89b1-314">For more information see, [Creating an Encoding Job with the Media Services REST API](media-services-rest-encode-asset.md).</span></span>

### <a name="monitor-processing-progress"></a><span data-ttu-id="d89b1-315">Monitor Processing Progress</span><span class="sxs-lookup"><span data-stu-id="d89b1-315">Monitor Processing Progress</span></span>
<span data-ttu-id="d89b1-316">You can retrieve the Job status by using the State property, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="d89b1-316">You can retrieve the Job status by using the State property, as shown in the following example.</span></span>

<span data-ttu-id="d89b1-317">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="d89b1-317">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


<span data-ttu-id="d89b1-318">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="d89b1-318">**HTTP Response**</span></span>

<span data-ttu-id="d89b1-319">If successful, the following response is returned:</span><span class="sxs-lookup"><span data-stu-id="d89b1-319">If successful, the following response is returned:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 17
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 01324d81-18e2-4493-a3e5-c6186209f0c8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Sun, 13 May 2012 05:16:53 GMT

    {"d":{"State":2}}


### <a name="cancel-a-job"></a><span data-ttu-id="d89b1-320">Cancel a job</span><span class="sxs-lookup"><span data-stu-id="d89b1-320">Cancel a job</span></span>
<span data-ttu-id="d89b1-321">Media Services allows you to cancel running jobs through the CancelJob function.</span><span class="sxs-lookup"><span data-stu-id="d89b1-321">Media Services allows you to cancel running jobs through the CancelJob function.</span></span> <span data-ttu-id="d89b1-322">This call returns a 400 error code if you try to cancel a Job when its state is canceled, canceling, error, or finished.</span><span class="sxs-lookup"><span data-stu-id="d89b1-322">This call returns a 400 error code if you try to cancel a Job when its state is canceled, canceling, error, or finished.</span></span>

<span data-ttu-id="d89b1-323">The following example shows how to call CancelJob.</span><span class="sxs-lookup"><span data-stu-id="d89b1-323">The following example shows how to call CancelJob.</span></span>

<span data-ttu-id="d89b1-324">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="d89b1-324">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


<span data-ttu-id="d89b1-325">If successful, a 204 response code is returned with no message body.</span><span class="sxs-lookup"><span data-stu-id="d89b1-325">If successful, a 204 response code is returned with no message body.</span></span>

> [!NOTE]
> <span data-ttu-id="d89b1-326">You must URL-encode the job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter to CancelJob.</span><span class="sxs-lookup"><span data-stu-id="d89b1-326">You must URL-encode the job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter to CancelJob.</span></span>
>
>

### <a name="get-the-output-asset"></a><span data-ttu-id="d89b1-327">Get the output asset</span><span class="sxs-lookup"><span data-stu-id="d89b1-327">Get the output asset</span></span>
<span data-ttu-id="d89b1-328">The following code shows how to request the output asset Id.</span><span class="sxs-lookup"><span data-stu-id="d89b1-328">The following code shows how to request the output asset Id.</span></span>

<span data-ttu-id="d89b1-329">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="d89b1-329">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="d89b1-330">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="d89b1-330">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 445
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    x-ms-request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:28:13 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets",
       "value":[  
          {  
             "Id":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "State":0,
             "Created":"2015-01-19T07:52:15.603",
             "LastModified":"2015-01-19T07:52:15.603",
             "AlternateId":null,
             "Name":"Multibitrate MP4s",
             "Options":0,
             "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "StorageAccountName":"storagetestaccount001"
          }
       ]
    }



## <a id="publish_get_urls"></a><span data-ttu-id="d89b1-331">Publish the asset and get streaming and progressive download URLs with REST API</span><span class="sxs-lookup"><span data-stu-id="d89b1-331">Publish the asset and get streaming and progressive download URLs with REST API</span></span>

<span data-ttu-id="d89b1-332">To stream or download an asset, you first need to "publish" it by creating a locator.</span><span class="sxs-lookup"><span data-stu-id="d89b1-332">To stream or download an asset, you first need to "publish" it by creating a locator.</span></span> <span data-ttu-id="d89b1-333">Locators provide access to files contained in the asset.</span><span class="sxs-lookup"><span data-stu-id="d89b1-333">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="d89b1-334">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files.</span><span class="sxs-lookup"><span data-stu-id="d89b1-334">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files.</span></span> <span data-ttu-id="d89b1-335">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span><span class="sxs-lookup"><span data-stu-id="d89b1-335">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="d89b1-336">Once you create the locators, you can build the URLs that are used to stream or download your files.</span><span class="sxs-lookup"><span data-stu-id="d89b1-336">Once you create the locators, you can build the URLs that are used to stream or download your files.</span></span>

>[!NOTE]
><span data-ttu-id="d89b1-337">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span><span class="sxs-lookup"><span data-stu-id="d89b1-337">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="d89b1-338">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span><span class="sxs-lookup"><span data-stu-id="d89b1-338">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="d89b1-339">A streaming URL for Smooth Streaming has the following format:</span><span class="sxs-lookup"><span data-stu-id="d89b1-339">A streaming URL for Smooth Streaming has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="d89b1-340">A streaming URL for HLS has the following format:</span><span class="sxs-lookup"><span data-stu-id="d89b1-340">A streaming URL for HLS has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="d89b1-341">A streaming URL for MPEG DASH has the following format:</span><span class="sxs-lookup"><span data-stu-id="d89b1-341">A streaming URL for MPEG DASH has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="d89b1-342">A SAS URL used to download files has the following format:</span><span class="sxs-lookup"><span data-stu-id="d89b1-342">A SAS URL used to download files has the following format:</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="d89b1-343">This section shows how to perform the following tasks necessary to "publish" your assets.</span><span class="sxs-lookup"><span data-stu-id="d89b1-343">This section shows how to perform the following tasks necessary to "publish" your assets.</span></span>  

* <span data-ttu-id="d89b1-344">Creating the AccessPolicy with read permission</span><span class="sxs-lookup"><span data-stu-id="d89b1-344">Creating the AccessPolicy with read permission</span></span>
* <span data-ttu-id="d89b1-345">Creating a SAS URL for downloading content</span><span class="sxs-lookup"><span data-stu-id="d89b1-345">Creating a SAS URL for downloading content</span></span>
* <span data-ttu-id="d89b1-346">Creating an origin URL for streaming content</span><span class="sxs-lookup"><span data-stu-id="d89b1-346">Creating an origin URL for streaming content</span></span>

### <a name="creating-the-accesspolicy-with-read-permission"></a><span data-ttu-id="d89b1-347">Creating the AccessPolicy with read permission</span><span class="sxs-lookup"><span data-stu-id="d89b1-347">Creating the AccessPolicy with read permission</span></span>
<span data-ttu-id="d89b1-348">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create the appropriate Locator entity that specifies the type of delivery mechanism you want to enable for your clients.</span><span class="sxs-lookup"><span data-stu-id="d89b1-348">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create the appropriate Locator entity that specifies the type of delivery mechanism you want to enable for your clients.</span></span> <span data-ttu-id="d89b1-349">For more information on the properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span><span class="sxs-lookup"><span data-stu-id="d89b1-349">For more information on the properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span></span>

<span data-ttu-id="d89b1-350">The following example shows how to specify the AccessPolicy for read permissions for a given Asset.</span><span class="sxs-lookup"><span data-stu-id="d89b1-350">The following example shows how to specify the AccessPolicy for read permissions for a given Asset.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

<span data-ttu-id="d89b1-351">If successful, a 201 success code is returned describing the AccessPolicy entity that you created.</span><span class="sxs-lookup"><span data-stu-id="d89b1-351">If successful, a 201 success code is returned describing the AccessPolicy entity that you created.</span></span> <span data-ttu-id="d89b1-352">You then use the AccessPolicy Id along with the Asset Id of the asset that contains the file you want to deliver(such as an output asset) to create the Locator entity.</span><span class="sxs-lookup"><span data-stu-id="d89b1-352">You then use the AccessPolicy Id along with the Asset Id of the asset that contains the file you want to deliver(such as an output asset) to create the Locator entity.</span></span>

> [!NOTE]
> <span data-ttu-id="d89b1-353">This basic workflow is the same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span><span class="sxs-lookup"><span data-stu-id="d89b1-353">This basic workflow is the same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span></span> <span data-ttu-id="d89b1-354">Also, like uploading files, if you (or your clients) need to access your files immediately, set your StartTime value to five minutes before the current time.</span><span class="sxs-lookup"><span data-stu-id="d89b1-354">Also, like uploading files, if you (or your clients) need to access your files immediately, set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="d89b1-355">This action is necessary because there may be clock skew between the client and Media Services.</span><span class="sxs-lookup"><span data-stu-id="d89b1-355">This action is necessary because there may be clock skew between the client and Media Services.</span></span> <span data-ttu-id="d89b1-356">The StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="d89b1-356">The StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a><span data-ttu-id="d89b1-357">Creating a SAS URL for downloading content</span><span class="sxs-lookup"><span data-stu-id="d89b1-357">Creating a SAS URL for downloading content</span></span>
<span data-ttu-id="d89b1-358">The following code shows how to get a URL that can be used to download a media file created and uploaded previously.</span><span class="sxs-lookup"><span data-stu-id="d89b1-358">The following code shows how to get a URL that can be used to download a media file created and uploaded previously.</span></span> <span data-ttu-id="d89b1-359">The AccessPolicy has read permissions set and the Locator path refers to a SAS download URL.</span><span class="sxs-lookup"><span data-stu-id="d89b1-359">The AccessPolicy has read permissions set and the Locator path refers to a SAS download URL.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-b1ae-2233-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c", "StartTime" : "2014-05-17T16:45:53", "Type":1}

<span data-ttu-id="d89b1-360">If successful, the following response is returned:</span><span class="sxs-lookup"><span data-stu-id="d89b1-360">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1150
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 8cfd8556-3064-416a-97f2-67d9e35f0911
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:32 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Asset"
             }
          },
          "Id":"nb:lid:UUID:8e5a821d-2194-4d00-8884-adf979856874",
          "ExpirationDateTime":"\/Date(1337049393000)\/",
          "Type":1,
          "Path":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c?st=2012-05-14T21%3A36%3A33Z&se=2012-05-15T02%3A36%3A33Z&sr=c&si=8e5a821d-2194-4d00-8884-adf979856874&sig=y75dViDpC5V8WutrXM%2B%2FGpR3uOtqmlISiNlHU1YUBOg%3D",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "StartTime":"\/Date(1337031393000)\/"
       }
    }


<span data-ttu-id="d89b1-361">The returned **Path** property contains the SAS URL.</span><span class="sxs-lookup"><span data-stu-id="d89b1-361">The returned **Path** property contains the SAS URL.</span></span>

> [!NOTE]
> <span data-ttu-id="d89b1-362">If you download storage encrypted content, you must manually decrypt it before rendering it, or use the Storage Decryption MediaProcessor in a processing task to output processed files in the clear to an OutputAsset and then download from that Asset.</span><span class="sxs-lookup"><span data-stu-id="d89b1-362">If you download storage encrypted content, you must manually decrypt it before rendering it, or use the Storage Decryption MediaProcessor in a processing task to output processed files in the clear to an OutputAsset and then download from that Asset.</span></span> <span data-ttu-id="d89b1-363">For more information on processing, see Creating an Encoding Job with the Media Services REST API.</span><span class="sxs-lookup"><span data-stu-id="d89b1-363">For more information on processing, see Creating an Encoding Job with the Media Services REST API.</span></span> <span data-ttu-id="d89b1-364">Also, SAS URL Locators cannot be updated after they have been created.</span><span class="sxs-lookup"><span data-stu-id="d89b1-364">Also, SAS URL Locators cannot be updated after they have been created.</span></span> <span data-ttu-id="d89b1-365">For example, you cannot reuse the same Locator with an updated StartTime value.</span><span class="sxs-lookup"><span data-stu-id="d89b1-365">For example, you cannot reuse the same Locator with an updated StartTime value.</span></span> <span data-ttu-id="d89b1-366">This is because of the way SAS URLs are created.</span><span class="sxs-lookup"><span data-stu-id="d89b1-366">This is because of the way SAS URLs are created.</span></span> <span data-ttu-id="d89b1-367">If you want to access an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span><span class="sxs-lookup"><span data-stu-id="d89b1-367">If you want to access an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span></span>
>
>

### <a name="download-files"></a><span data-ttu-id="d89b1-368">Download files</span><span class="sxs-lookup"><span data-stu-id="d89b1-368">Download files</span></span>
<span data-ttu-id="d89b1-369">Once you have the AccessPolicy and Locator set, you can download files using the Azure Storage REST APIs.</span><span class="sxs-lookup"><span data-stu-id="d89b1-369">Once you have the AccessPolicy and Locator set, you can download files using the Azure Storage REST APIs.</span></span>  

> [!NOTE]
> <span data-ttu-id="d89b1-370">You must add the file name for the file you want to download to the Locator **Path** value received in the previous section.</span><span class="sxs-lookup"><span data-stu-id="d89b1-370">You must add the file name for the file you want to download to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="d89b1-371">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="d89b1-371">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="d89b1-372">.</span><span class="sxs-lookup"><span data-stu-id="d89b1-372">.</span></span> <span data-ttu-id="d89b1-373">.</span><span class="sxs-lookup"><span data-stu-id="d89b1-373">.</span></span> <span data-ttu-id="d89b1-374">.</span><span class="sxs-lookup"><span data-stu-id="d89b1-374">.</span></span>
>
>

<span data-ttu-id="d89b1-375">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="d89b1-375">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/Blob-Service-REST-API).</span></span>

<span data-ttu-id="d89b1-376">As a result of the encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span><span class="sxs-lookup"><span data-stu-id="d89b1-376">As a result of the encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span></span> <span data-ttu-id="d89b1-377">For example:</span><span class="sxs-lookup"><span data-stu-id="d89b1-377">For example:</span></span>    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a><span data-ttu-id="d89b1-378">Creating a streaming URL for streaming content</span><span class="sxs-lookup"><span data-stu-id="d89b1-378">Creating a streaming URL for streaming content</span></span>
<span data-ttu-id="d89b1-379">The following code shows how to create a streaming URL Locator:</span><span class="sxs-lookup"><span data-stu-id="d89b1-379">The following code shows how to create a streaming URL Locator:</span></span>

    POST https://wamsbayclus001rest-hs/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3", "StartTime" : "2014-05-17T16:45:53",, "Type":2}

<span data-ttu-id="d89b1-380">If successful, the following response is returned:</span><span class="sxs-lookup"><span data-stu-id="d89b1-380">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 981
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 2eac4158-fc78-4fa2-81ee-c9f582dc385f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:39 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/Asset"
             }
          },
          "Id":"nb:lid:UUID:52034bf6-dfae-4d83-aad3-3bd87dcb1a5d",
          "ExpirationDateTime":"\/Date(1337049395000)\/",
          "Type":2,
          "Path":"http://wamsbayclus001rest-hs.net/52034bf6-dfae-4d83-aad3-3bd87dcb1a5d/",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3",
          "StartTime":"\/Date(1337031395000)\/"
       }
    }

<span data-ttu-id="d89b1-381">To stream a Smooth Streaming origin URL in a streaming media player, you must append the Path property with the name of the Smooth Streaming manifest file, followed by "/manifest".</span><span class="sxs-lookup"><span data-stu-id="d89b1-381">To stream a Smooth Streaming origin URL in a streaming media player, you must append the Path property with the name of the Smooth Streaming manifest file, followed by "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="d89b1-382">To stream HLS, append (format=m3u8-aapl) after the "/manifest".</span><span class="sxs-lookup"><span data-stu-id="d89b1-382">To stream HLS, append (format=m3u8-aapl) after the "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="d89b1-383">To stream MPEG DASH, append (format=mpd-time-csf) after the "/manifest".</span><span class="sxs-lookup"><span data-stu-id="d89b1-383">To stream MPEG DASH, append (format=mpd-time-csf) after the "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <a id="play"></a><span data-ttu-id="d89b1-384">Play your content</span><span class="sxs-lookup"><span data-stu-id="d89b1-384">Play your content</span></span>
<span data-ttu-id="d89b1-385">To stream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="d89b1-385">To stream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="d89b1-386">To test progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span><span class="sxs-lookup"><span data-stu-id="d89b1-386">To test progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span></span>

## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="d89b1-387">Next Steps: Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="d89b1-387">Next Steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d89b1-388">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="d89b1-388">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


