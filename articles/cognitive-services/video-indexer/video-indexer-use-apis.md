---
title: Use Azure Video Indexer API | Microsoft Docs
description: This article shows how to get started using the Video Indexer API.
services: cognitive services
documentationcenter: ''
author: juliako
manager: erikre
ms.service: cognitive-services
ms.topic: article
ms.date: 07/25/2018
ms.author: juliako
ms.openlocfilehash: 73359955861b88f2bc5ca297c32fa78c2632148c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870135"
---
# <a name="use-azure-video-indexer-api"></a><span data-ttu-id="b5254-103">Use Azure Video Indexer API</span><span class="sxs-lookup"><span data-stu-id="b5254-103">Use Azure Video Indexer API</span></span>

> [!Note]
> <span data-ttu-id="b5254-104">The Video Indexer V1 API was deprecated on August 1st, 2018.</span><span class="sxs-lookup"><span data-stu-id="b5254-104">The Video Indexer V1 API was deprecated on August 1st, 2018.</span></span> <span data-ttu-id="b5254-105">You should now use the Video Indexer v2 API.</span><span class="sxs-lookup"><span data-stu-id="b5254-105">You should now use the Video Indexer v2 API.</span></span> <br/><span data-ttu-id="b5254-106">To develop with Video Indexer v2 APIs, please refer to the instructions found [here](https://api-portal.videoindexer.ai/).</span><span class="sxs-lookup"><span data-stu-id="b5254-106">To develop with Video Indexer v2 APIs, please refer to the instructions found [here](https://api-portal.videoindexer.ai/).</span></span> 

<span data-ttu-id="b5254-107">Video Indexer consolidates various audio and video artificial intelligence (AI) technologies offered by Microsoft in one integrated service, making development simpler.</span><span class="sxs-lookup"><span data-stu-id="b5254-107">Video Indexer consolidates various audio and video artificial intelligence (AI) technologies offered by Microsoft in one integrated service, making development simpler.</span></span> <span data-ttu-id="b5254-108">The APIs are designed to enable developers to focus on consuming Media AI technologies without worrying about scale, global reach, availability, and reliability of cloud platform.</span><span class="sxs-lookup"><span data-stu-id="b5254-108">The APIs are designed to enable developers to focus on consuming Media AI technologies without worrying about scale, global reach, availability, and reliability of cloud platform.</span></span> <span data-ttu-id="b5254-109">You can use the API to upload your files, get detailed video insights, get URLs of insight and player widgets in order to embed them into your application, and other tasks.</span><span class="sxs-lookup"><span data-stu-id="b5254-109">You can use the API to upload your files, get detailed video insights, get URLs of insight and player widgets in order to embed them into your application, and other tasks.</span></span>

<span data-ttu-id="b5254-110">When creating a Video Indexer account, you can choose a free trial account (where you get a certain number of free indexing minutes) or a paid option (where you are not limited by the quota).</span><span class="sxs-lookup"><span data-stu-id="b5254-110">When creating a Video Indexer account, you can choose a free trial account (where you get a certain number of free indexing minutes) or a paid option (where you are not limited by the quota).</span></span> <span data-ttu-id="b5254-111">With free trial, Video Indexer provides up to 600 minutes of free indexing to website users and up to 2400 minutes of free indexing to API users.</span><span class="sxs-lookup"><span data-stu-id="b5254-111">With free trial, Video Indexer provides up to 600 minutes of free indexing to website users and up to 2400 minutes of free indexing to API users.</span></span> <span data-ttu-id="b5254-112">With paid option, you create a Video Indexer account that is [connected to your Azure subscription and a Azure Media Services account](connect-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="b5254-112">With paid option, you create a Video Indexer account that is [connected to your Azure subscription and a Azure Media Services account](connect-to-azure.md).</span></span> <span data-ttu-id="b5254-113">You pay for minutes indexed as well as the Media Account related charges.</span><span class="sxs-lookup"><span data-stu-id="b5254-113">You pay for minutes indexed as well as the Media Account related charges.</span></span> 

<span data-ttu-id="b5254-114">This article shows how the developers can take advantage of the [Video Indexer API](https://api-portal.videoindexer.ai/).</span><span class="sxs-lookup"><span data-stu-id="b5254-114">This article shows how the developers can take advantage of the [Video Indexer API](https://api-portal.videoindexer.ai/).</span></span> <span data-ttu-id="b5254-115">To read a more detailed overview of the Video Indexer service, see the [overview](video-indexer-overview.md) article.</span><span class="sxs-lookup"><span data-stu-id="b5254-115">To read a more detailed overview of the Video Indexer service, see the [overview](video-indexer-overview.md) article.</span></span>

## <a name="subscribe-to-the-api"></a><span data-ttu-id="b5254-116">Subscribe to the API</span><span class="sxs-lookup"><span data-stu-id="b5254-116">Subscribe to the API</span></span>

1. <span data-ttu-id="b5254-117">Sign in.</span><span class="sxs-lookup"><span data-stu-id="b5254-117">Sign in.</span></span>

    <span data-ttu-id="b5254-118">To start developing with Video Indexer, you must first Sign In to the [Video Indexer](https://api-portal.videoindexer.ai/) portal.</span><span class="sxs-lookup"><span data-stu-id="b5254-118">To start developing with Video Indexer, you must first Sign In to the [Video Indexer](https://api-portal.videoindexer.ai/) portal.</span></span> 
    
    ![Sign up](./media/video-indexer-use-apis/video-indexer-api01.png)

    > [!Important]
    > * <span data-ttu-id="b5254-120">You must use the same provider you used when you signed up for Video Indexer.</span><span class="sxs-lookup"><span data-stu-id="b5254-120">You must use the same provider you used when you signed up for Video Indexer.</span></span>
    > * <span data-ttu-id="b5254-121">Personal Google and Microsoft (outlook/live) accounts can only be used for trial accounts.</span><span class="sxs-lookup"><span data-stu-id="b5254-121">Personal Google and Microsoft (outlook/live) accounts can only be used for trial accounts.</span></span> <span data-ttu-id="b5254-122">Accounts connected to Azure require Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5254-122">Accounts connected to Azure require Azure AD.</span></span>
    > * <span data-ttu-id="b5254-123">There can be only one active account per E-Mail.</span><span class="sxs-lookup"><span data-stu-id="b5254-123">There can be only one active account per E-Mail.</span></span> <span data-ttu-id="b5254-124">If a user tries to sign-in with user@gmail.com for LinkedIn and after that with user@gmail.com for Google the later will display an error page, saying the user already exist.</span><span class="sxs-lookup"><span data-stu-id="b5254-124">If a user tries to sign-in with user@gmail.com for LinkedIn and after that with user@gmail.com for Google the later will display an error page, saying the user already exist.</span></span>


2. <span data-ttu-id="b5254-125">Subscribe.</span><span class="sxs-lookup"><span data-stu-id="b5254-125">Subscribe.</span></span>

    <span data-ttu-id="b5254-126">Select the [Products](https://api-portal.videoindexer.ai/products) tab. Then, select Authorization and subscribe.</span><span class="sxs-lookup"><span data-stu-id="b5254-126">Select the [Products](https://api-portal.videoindexer.ai/products) tab. Then, select Authorization and subscribe.</span></span> 
    
    ![Sign up](./media/video-indexer-use-apis/video-indexer-api02.png)

    > [!NOTE]
    > <span data-ttu-id="b5254-128">New users are automatically subscribed to Authorization.</span><span class="sxs-lookup"><span data-stu-id="b5254-128">New users are automatically subscribed to Authorization.</span></span>
    
    <span data-ttu-id="b5254-129">Once you subscribe, you will be able to see your subscription and your primary and secondary keys.</span><span class="sxs-lookup"><span data-stu-id="b5254-129">Once you subscribe, you will be able to see your subscription and your primary and secondary keys.</span></span> <span data-ttu-id="b5254-130">The keys should be protected.</span><span class="sxs-lookup"><span data-stu-id="b5254-130">The keys should be protected.</span></span> <span data-ttu-id="b5254-131">The keys should only be used by your server code.</span><span class="sxs-lookup"><span data-stu-id="b5254-131">The keys should only be used by your server code.</span></span> <span data-ttu-id="b5254-132">They should not be available on the client side (.js, .html, etc.).</span><span class="sxs-lookup"><span data-stu-id="b5254-132">They should not be available on the client side (.js, .html, etc.).</span></span>

    ![Sign up](./media/video-indexer-use-apis/video-indexer-api03.png)

## <a name="obtain-access-token-using-the-authorization-api"></a><span data-ttu-id="b5254-134">Obtain access token using the Authorization API</span><span class="sxs-lookup"><span data-stu-id="b5254-134">Obtain access token using the Authorization API</span></span>

<span data-ttu-id="b5254-135">Once you subscribed to the Authorization API, you will be able to obtain access tokens.</span><span class="sxs-lookup"><span data-stu-id="b5254-135">Once you subscribed to the Authorization API, you will be able to obtain access tokens.</span></span> <span data-ttu-id="b5254-136">These access tokens are used to authenticate against the Operations API.</span><span class="sxs-lookup"><span data-stu-id="b5254-136">These access tokens are used to authenticate against the Operations API.</span></span> 

<span data-ttu-id="b5254-137">Each call to the Operations API should be associated with an access token, matching the authorization scope of the call.</span><span class="sxs-lookup"><span data-stu-id="b5254-137">Each call to the Operations API should be associated with an access token, matching the authorization scope of the call.</span></span>

- <span data-ttu-id="b5254-138">User level -  user level access tokens let you perform operations on the **user** level.</span><span class="sxs-lookup"><span data-stu-id="b5254-138">User level -  user level access tokens let you perform operations on the **user** level.</span></span> <span data-ttu-id="b5254-139">For example, get associated accounts.</span><span class="sxs-lookup"><span data-stu-id="b5254-139">For example, get associated accounts.</span></span>
- <span data-ttu-id="b5254-140">Account level – account level access tokens let you perform operations on the **account** level or the **video** level.</span><span class="sxs-lookup"><span data-stu-id="b5254-140">Account level – account level access tokens let you perform operations on the **account** level or the **video** level.</span></span> <span data-ttu-id="b5254-141">For example, Upload video, list all videos, get video insights, etc.</span><span class="sxs-lookup"><span data-stu-id="b5254-141">For example, Upload video, list all videos, get video insights, etc.</span></span>
- <span data-ttu-id="b5254-142">Video level – video level access tokens let you perform operations on a specific **video**.</span><span class="sxs-lookup"><span data-stu-id="b5254-142">Video level – video level access tokens let you perform operations on a specific **video**.</span></span> <span data-ttu-id="b5254-143">For example, get video insights, download captions, get widgets, etc.</span><span class="sxs-lookup"><span data-stu-id="b5254-143">For example, get video insights, download captions, get widgets, etc.</span></span> 

<span data-ttu-id="b5254-144">You can control whether these tokens are readonly or they allow editing by specifying **allowEdit=true/false**.</span><span class="sxs-lookup"><span data-stu-id="b5254-144">You can control whether these tokens are readonly or they allow editing by specifying **allowEdit=true/false**.</span></span>

<span data-ttu-id="b5254-145">For most server-to-server scenarios, you will probably use the same **account** token since it covers both **account** operations and **video** operations.</span><span class="sxs-lookup"><span data-stu-id="b5254-145">For most server-to-server scenarios, you will probably use the same **account** token since it covers both **account** operations and **video** operations.</span></span> <span data-ttu-id="b5254-146">However, if you are planning to make client side calls to Video Indexer (for example, from javascript), you would want to use a **video** access token, to prevent clients from getting access to the entire account.</span><span class="sxs-lookup"><span data-stu-id="b5254-146">However, if you are planning to make client side calls to Video Indexer (for example, from javascript), you would want to use a **video** access token, to prevent clients from getting access to the entire account.</span></span> <span data-ttu-id="b5254-147">That is also the reason that when embedding VideoIndexer client code in your client (for example, using **Get Insights Widget** or **Get Player Widget**) you must provide a **video** access token.</span><span class="sxs-lookup"><span data-stu-id="b5254-147">That is also the reason that when embedding VideoIndexer client code in your client (for example, using **Get Insights Widget** or **Get Player Widget**) you must provide a **video** access token.</span></span>

<span data-ttu-id="b5254-148">To make things easier, you can use the **Authorization** API > **GetAccounts** to get your accounts without obtaining a user token first.</span><span class="sxs-lookup"><span data-stu-id="b5254-148">To make things easier, you can use the **Authorization** API > **GetAccounts** to get your accounts without obtaining a user token first.</span></span> <span data-ttu-id="b5254-149">You can also ask to get the accounts with valid tokens, enabling you to skip an additional call to get an account token.</span><span class="sxs-lookup"><span data-stu-id="b5254-149">You can also ask to get the accounts with valid tokens, enabling you to skip an additional call to get an account token.</span></span>

<span data-ttu-id="b5254-150">Access tokens expire after 1 hour.</span><span class="sxs-lookup"><span data-stu-id="b5254-150">Access tokens expire after 1 hour.</span></span> <span data-ttu-id="b5254-151">Make sure your access token is valid before using the Operations API.</span><span class="sxs-lookup"><span data-stu-id="b5254-151">Make sure your access token is valid before using the Operations API.</span></span> <span data-ttu-id="b5254-152">If expires, call the Authorization API again to get a new access token.</span><span class="sxs-lookup"><span data-stu-id="b5254-152">If expires, call the Authorization API again to get a new access token.</span></span>
 
<span data-ttu-id="b5254-153">You are ready to start integrating with the API.</span><span class="sxs-lookup"><span data-stu-id="b5254-153">You are ready to start integrating with the API.</span></span> <span data-ttu-id="b5254-154">Find [the detailed description of each Video Indexer REST API](http://api-portal.videoindexer.ai/).</span><span class="sxs-lookup"><span data-stu-id="b5254-154">Find [the detailed description of each Video Indexer REST API](http://api-portal.videoindexer.ai/).</span></span>

## <a name="location"></a><span data-ttu-id="b5254-155">Location</span><span class="sxs-lookup"><span data-stu-id="b5254-155">Location</span></span>

<span data-ttu-id="b5254-156">All operation APIs require a Location parameter, which indicates the region to which the call should be routed and in which the account was created.</span><span class="sxs-lookup"><span data-stu-id="b5254-156">All operation APIs require a Location parameter, which indicates the region to which the call should be routed and in which the account was created.</span></span>

<span data-ttu-id="b5254-157">The values described in the following table apply.</span><span class="sxs-lookup"><span data-stu-id="b5254-157">The values described in the following table apply.</span></span> <span data-ttu-id="b5254-158">The **Param value** is the value you pass when using the API.</span><span class="sxs-lookup"><span data-stu-id="b5254-158">The **Param value** is the value you pass when using the API.</span></span>

|<span data-ttu-id="b5254-159">**Name**</span><span class="sxs-lookup"><span data-stu-id="b5254-159">**Name**</span></span>|<span data-ttu-id="b5254-160">**Param value**</span><span class="sxs-lookup"><span data-stu-id="b5254-160">**Param value**</span></span>|<span data-ttu-id="b5254-161">**Description**</span><span class="sxs-lookup"><span data-stu-id="b5254-161">**Description**</span></span>|
|---|---|---|
|<span data-ttu-id="b5254-162">Trial</span><span class="sxs-lookup"><span data-stu-id="b5254-162">Trial</span></span>|<span data-ttu-id="b5254-163">trial</span><span class="sxs-lookup"><span data-stu-id="b5254-163">trial</span></span>|<span data-ttu-id="b5254-164">Used for trial accounts.</span><span class="sxs-lookup"><span data-stu-id="b5254-164">Used for trial accounts.</span></span>|
|<span data-ttu-id="b5254-165">West US</span><span class="sxs-lookup"><span data-stu-id="b5254-165">West US</span></span>|<span data-ttu-id="b5254-166">westus2</span><span class="sxs-lookup"><span data-stu-id="b5254-166">westus2</span></span>|<span data-ttu-id="b5254-167">Used for the Azure West US 2 region.</span><span class="sxs-lookup"><span data-stu-id="b5254-167">Used for the Azure West US 2 region.</span></span>|
|<span data-ttu-id="b5254-168">North Europe</span><span class="sxs-lookup"><span data-stu-id="b5254-168">North Europe</span></span> |<span data-ttu-id="b5254-169">northeurope</span><span class="sxs-lookup"><span data-stu-id="b5254-169">northeurope</span></span>|<span data-ttu-id="b5254-170">Used for the Azure North Europe region.</span><span class="sxs-lookup"><span data-stu-id="b5254-170">Used for the Azure North Europe region.</span></span>|
|<span data-ttu-id="b5254-171">East Asia</span><span class="sxs-lookup"><span data-stu-id="b5254-171">East Asia</span></span>|<span data-ttu-id="b5254-172">eastasia</span><span class="sxs-lookup"><span data-stu-id="b5254-172">eastasia</span></span>|<span data-ttu-id="b5254-173">Used for the Azure East Asia region.</span><span class="sxs-lookup"><span data-stu-id="b5254-173">Used for the Azure East Asia region.</span></span>|

## <a name="account-id"></a><span data-ttu-id="b5254-174">Account ID</span><span class="sxs-lookup"><span data-stu-id="b5254-174">Account ID</span></span> 

<span data-ttu-id="b5254-175">The Account ID parameter is required in all operational API calls.</span><span class="sxs-lookup"><span data-stu-id="b5254-175">The Account ID parameter is required in all operational API calls.</span></span> <span data-ttu-id="b5254-176">Account ID is a GUID that can be obtained in one of the following ways:</span><span class="sxs-lookup"><span data-stu-id="b5254-176">Account ID is a GUID that can be obtained in one of the following ways:</span></span>

* <span data-ttu-id="b5254-177">Use the Video Indexer portal to get the Account ID:</span><span class="sxs-lookup"><span data-stu-id="b5254-177">Use the Video Indexer portal to get the Account ID:</span></span>

    1. <span data-ttu-id="b5254-178">Sign in to [videoindexer](https://www.videoindexer.ai/).</span><span class="sxs-lookup"><span data-stu-id="b5254-178">Sign in to [videoindexer](https://www.videoindexer.ai/).</span></span>
    2. <span data-ttu-id="b5254-179">Browse to the **Settings** page.</span><span class="sxs-lookup"><span data-stu-id="b5254-179">Browse to the **Settings** page.</span></span>
    3. <span data-ttu-id="b5254-180">Copy the account ID.</span><span class="sxs-lookup"><span data-stu-id="b5254-180">Copy the account ID.</span></span>

        ![Account ID](./media/video-indexer-use-apis/account-id.png)

* <span data-ttu-id="b5254-182">Use the API to programmatically get the Account ID.</span><span class="sxs-lookup"><span data-stu-id="b5254-182">Use the API to programmatically get the Account ID.</span></span>

    <span data-ttu-id="b5254-183">Use the [Get accounts](https://api-portal.videoindexer.ai/docs/services/authorization/operations/Get-Accounts?) API.</span><span class="sxs-lookup"><span data-stu-id="b5254-183">Use the [Get accounts](https://api-portal.videoindexer.ai/docs/services/authorization/operations/Get-Accounts?) API.</span></span>
    
    > [!TIP]
    > <span data-ttu-id="b5254-184">You can generate access tokens for the accounts by defining `generateAccessTokens=true`.</span><span class="sxs-lookup"><span data-stu-id="b5254-184">You can generate access tokens for the accounts by defining `generateAccessTokens=true`.</span></span>
    
* <span data-ttu-id="b5254-185">Get the account ID from the URL of a player page in your account.</span><span class="sxs-lookup"><span data-stu-id="b5254-185">Get the account ID from the URL of a player page in your account.</span></span>

    <span data-ttu-id="b5254-186">When you watch a video, the ID appears after the `accounts` section and before the `videos` section.</span><span class="sxs-lookup"><span data-stu-id="b5254-186">When you watch a video, the ID appears after the `accounts` section and before the `videos` section.</span></span>

    ```
    https://www.videoindexer.ai/accounts/00000000-f324-4385-b142-f77dacb0a368/videos/d45bf160b5/
    ```

## <a name="recommendations"></a><span data-ttu-id="b5254-187">Recommendations</span><span class="sxs-lookup"><span data-stu-id="b5254-187">Recommendations</span></span>

<span data-ttu-id="b5254-188">This section lists some recommendations when using Video Indexer API.</span><span class="sxs-lookup"><span data-stu-id="b5254-188">This section lists some recommendations when using Video Indexer API.</span></span>

- <span data-ttu-id="b5254-189">If you are planning to upload a video, it is recommended to place the file in some public network location (for example, OneDrive).</span><span class="sxs-lookup"><span data-stu-id="b5254-189">If you are planning to upload a video, it is recommended to place the file in some public network location (for example, OneDrive).</span></span> <span data-ttu-id="b5254-190">Get the link to the video and provide the URL as the upload file param.</span><span class="sxs-lookup"><span data-stu-id="b5254-190">Get the link to the video and provide the URL as the upload file param.</span></span> 

    <span data-ttu-id="b5254-191">The URL provided to Video Indexer must point to a media (audio or video) file.</span><span class="sxs-lookup"><span data-stu-id="b5254-191">The URL provided to Video Indexer must point to a media (audio or video) file.</span></span> <span data-ttu-id="b5254-192">Some of the links generated by OneDrive are for an HTML page that contains the file.</span><span class="sxs-lookup"><span data-stu-id="b5254-192">Some of the links generated by OneDrive are for an HTML page that contains the file.</span></span> <span data-ttu-id="b5254-193">An easy verification for the URL would be to paste it into a browser – if the file starts downloading, it's likely a good URL.</span><span class="sxs-lookup"><span data-stu-id="b5254-193">An easy verification for the URL would be to paste it into a browser – if the file starts downloading, it's likely a good URL.</span></span> <span data-ttu-id="b5254-194">If the browser is rendering some visualization, it's likely not a link to a file but an HTML page.</span><span class="sxs-lookup"><span data-stu-id="b5254-194">If the browser is rendering some visualization, it's likely not a link to a file but an HTML page.</span></span>
    
- <span data-ttu-id="b5254-195">When you call the API that gets video insights for the specified video, you get a detailed JSON output as the response content.</span><span class="sxs-lookup"><span data-stu-id="b5254-195">When you call the API that gets video insights for the specified video, you get a detailed JSON output as the response content.</span></span> <span data-ttu-id="b5254-196">[See details about the returned JSON in this topic](video-indexer-output-json.md).</span><span class="sxs-lookup"><span data-stu-id="b5254-196">[See details about the returned JSON in this topic](video-indexer-output-json.md).</span></span>

## <a name="code-sample"></a><span data-ttu-id="b5254-197">Code sample</span><span class="sxs-lookup"><span data-stu-id="b5254-197">Code sample</span></span>

<span data-ttu-id="b5254-198">The following C# code snippet demonstrates the usage of all the Video Indexer APIs together.</span><span class="sxs-lookup"><span data-stu-id="b5254-198">The following C# code snippet demonstrates the usage of all the Video Indexer APIs together.</span></span>

```csharp
var apiUrl = "https://api.videoindexer.ai";
var accountId = "..."; 
var location = "westus2";
var apiKey = "..."; 

System.Net.ServicePointManager.SecurityProtocol = System.Net.ServicePointManager.SecurityProtocol | System.Net.SecurityProtocolType.Tls12;

// create the http client
var handler = new HttpClientHandler(); 
handler.AllowAutoRedirect = false; 
var client = new HttpClient(handler);
client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", apiKey); 

// obtain account access token
var accountAccessTokenRequestResult = client.GetAsync($"{apiUrl}/auth/{location}/Accounts/{accountId}/AccessToken?allowEdit=true").Result;
var accountAccessToken = accountAccessTokenRequestResult.Content.ReadAsStringAsync().Result.Replace("\"", "");

client.DefaultRequestHeaders.Remove("Ocp-Apim-Subscription-Key");

// upload a video
var content = new MultipartFormDataContent();
Debug.WriteLine("Uploading...");
// get the video from URL
var videoUrl = "VIDEO_URL"; // replace with the video URL

// as an alternative to specifying video URL, you can upload a file.
// remove the videoUrl parameter from the query string below and add the following lines:
  //FileStream video =File.OpenRead(Globals.VIDEOFILE_PATH);
  //byte[] buffer =newbyte[video.Length];
  //video.Read(buffer, 0, buffer.Length);
  //content.Add(newByteArrayContent(buffer));

var uploadRequestResult = client.PostAsync($"{apiUrl}/{location}/Accounts/{accountId}/Videos?accessToken={accountAccessToken}&name=some_name&description=some_description&privacy=private&partition=some_partition&videoUrl={videoUrl}", content).Result;
var uploadResult = uploadRequestResult.Content.ReadAsStringAsync().Result;

// get the video id from the upload result
var videoId = JsonConvert.DeserializeObject<dynamic>(uploadResult)["id"];
Debug.WriteLine("Uploaded");
Debug.WriteLine("Video ID: " + videoId);           

// obtain video access token            
client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", apiKey);
var videoTokenRequestResult = client.GetAsync($"{apiUrl}/auth/{location}/Accounts/{accountId}/Videos/{videoId}/AccessToken?allowEdit=true").Result;
var videoAccessToken = videoTokenRequestResult.Content.ReadAsStringAsync().Result.Replace("\"", "");

client.DefaultRequestHeaders.Remove("Ocp-Apim-Subscription-Key");

// wait for the video index to finish
while (true)
{
  Thread.Sleep(10000);

  var videoGetIndexRequestResult = client.GetAsync($"{apiUrl}/{location}/Accounts/{accountId}/Videos/{videoId}/Index?accessToken={videoAccessToken}&language=English").Result;
  var videoGetIndexResult = videoGetIndexRequestResult.Content.ReadAsStringAsync().Result;

  var processingState = JsonConvert.DeserializeObject<dynamic>(videoGetIndexResult)["state"];

  Debug.WriteLine("");
  Debug.WriteLine("State:");
  Debug.WriteLine(processingState);

  // job is finished
  if (processingState != "Uploaded" && processingState != "Processing")
  {
      Debug.WriteLine("");
      Debug.WriteLine("Full JSON:");
      Debug.WriteLine(videoGetIndexResult);
      break;
  }
}

// search for the video
var searchRequestResult = client.GetAsync($"{apiUrl}/{location}/Accounts/{accountId}/Videos/Search?accessToken={accountAccessToken}&id={videoId}").Result;
var searchResult = searchRequestResult.Content.ReadAsStringAsync().Result;
Debug.WriteLine("");
Debug.WriteLine("Search:");
Debug.WriteLine(searchResult);

// get insights widget url
var insightsWidgetRequestResult = client.GetAsync($"{apiUrl}/{location}/Accounts/{accountId}/Videos/{videoId}/InsightsWidget?accessToken={videoAccessToken}&widgetType=Keywords&allowEdit=true").Result;
var insightsWidgetLink = insightsWidgetRequestResult.Headers.Location;
Debug.WriteLine("Insights Widget url:");
Debug.WriteLine(insightsWidgetLink);

// get player widget url
var playerWidgetRequestResult = client.GetAsync($"{apiUrl}/{location}/Accounts/{accountId}/Videos/{videoId}/PlayerWidget?accessToken={videoAccessToken}").Result;
var playerWidgetLink = playerWidgetRequestResult.Headers.Location;
Debug.WriteLine("");
Debug.WriteLine("Player Widget url:");
Debug.WriteLine(playerWidgetLink);

```

## <a name="next-steps"></a><span data-ttu-id="b5254-199">Next steps</span><span class="sxs-lookup"><span data-stu-id="b5254-199">Next steps</span></span>

<span data-ttu-id="b5254-200">[Examine details of the output JSON](video-indexer-output-json.md).</span><span class="sxs-lookup"><span data-stu-id="b5254-200">[Examine details of the output JSON](video-indexer-output-json.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="b5254-201">See also</span><span class="sxs-lookup"><span data-stu-id="b5254-201">See also</span></span>

[<span data-ttu-id="b5254-202">Video Indexer overview</span><span class="sxs-lookup"><span data-stu-id="b5254-202">Video Indexer overview</span></span>](video-indexer-overview.md)
