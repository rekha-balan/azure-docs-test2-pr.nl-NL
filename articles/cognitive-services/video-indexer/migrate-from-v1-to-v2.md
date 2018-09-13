---
title: Migrate from Azure Video Indexer API v1 to v2 | Microsoft Docs
description: This topic explains how to migrate from the Azure Video Indexer API v1 to v2.
services: cognitive services
documentationcenter: ''
author: juliako
manager: erikre
ms.service: cognitive-services
ms.topic: article
ms.date: 07/25/2018
ms.author: juliako
ms.openlocfilehash: b1737960a4142f5c0d949ce8c2524c34fe9cd79e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868152"
---
# <a name="migrate-from-the-video-indexer-api-v1-to-v2"></a><span data-ttu-id="2cfee-103">Migrate from the Video Indexer API v1 to v2</span><span class="sxs-lookup"><span data-stu-id="2cfee-103">Migrate from the Video Indexer API v1 to v2</span></span>

> [!Note]
> <span data-ttu-id="2cfee-104">The Video Indexer V1 API was deprecated on August 1st, 2018.</span><span class="sxs-lookup"><span data-stu-id="2cfee-104">The Video Indexer V1 API was deprecated on August 1st, 2018.</span></span> <span data-ttu-id="2cfee-105">You should now use the Video Indexer v2 API.</span><span class="sxs-lookup"><span data-stu-id="2cfee-105">You should now use the Video Indexer v2 API.</span></span> <br/><span data-ttu-id="2cfee-106">To develop with Video Indexer v2 APIs, please refer to the instructions found [here](https://api-portal.videoindexer.ai/).</span><span class="sxs-lookup"><span data-stu-id="2cfee-106">To develop with Video Indexer v2 APIs, please refer to the instructions found [here](https://api-portal.videoindexer.ai/).</span></span> 

<span data-ttu-id="2cfee-107">This article describes changes that were introduced in v2.</span><span class="sxs-lookup"><span data-stu-id="2cfee-107">This article describes changes that were introduced in v2.</span></span>  

## <a name="api-changes"></a><span data-ttu-id="2cfee-108">API changes</span><span class="sxs-lookup"><span data-stu-id="2cfee-108">API changes</span></span>

### <a name="authorization-and-operations"></a><span data-ttu-id="2cfee-109">Authorization and Operations</span><span class="sxs-lookup"><span data-stu-id="2cfee-109">Authorization and Operations</span></span>

<span data-ttu-id="2cfee-110">In the v2 version, Video Indexer changed the authentication and authorization model of the API.</span><span class="sxs-lookup"><span data-stu-id="2cfee-110">In the v2 version, Video Indexer changed the authentication and authorization model of the API.</span></span> <span data-ttu-id="2cfee-111">There are two sets of APIs:</span><span class="sxs-lookup"><span data-stu-id="2cfee-111">There are two sets of APIs:</span></span> 

* <span data-ttu-id="2cfee-112">Authorization</span><span class="sxs-lookup"><span data-stu-id="2cfee-112">Authorization</span></span> 
* <span data-ttu-id="2cfee-113">Operations</span><span class="sxs-lookup"><span data-stu-id="2cfee-113">Operations</span></span>

<span data-ttu-id="2cfee-114">The **Authorization** API is used to obtain access tokens for calling the **Operations** API.</span><span class="sxs-lookup"><span data-stu-id="2cfee-114">The **Authorization** API is used to obtain access tokens for calling the **Operations** API.</span></span> <span data-ttu-id="2cfee-115">The **Operations** API contains all the Video Indexer APIs, such as Upload video, Get insights, and other operations.</span><span class="sxs-lookup"><span data-stu-id="2cfee-115">The **Operations** API contains all the Video Indexer APIs, such as Upload video, Get insights, and other operations.</span></span>

<span data-ttu-id="2cfee-116">Once you [subscribe](video-indexer-get-started.md) to the **Authorization** API, you will be able to obtain access tokens by passing your subscription key (just like you did in v1.)</span><span class="sxs-lookup"><span data-stu-id="2cfee-116">Once you [subscribe](video-indexer-get-started.md) to the **Authorization** API, you will be able to obtain access tokens by passing your subscription key (just like you did in v1.)</span></span>

## <a name="getting-and-using-the-access-token-for-operations-apis"></a><span data-ttu-id="2cfee-117">Getting and using the access token for operations APIs</span><span class="sxs-lookup"><span data-stu-id="2cfee-117">Getting and using the access token for operations APIs</span></span>

<span data-ttu-id="2cfee-118">When calling the **Operations** APIs, the subscription key won't be used anymore.</span><span class="sxs-lookup"><span data-stu-id="2cfee-118">When calling the **Operations** APIs, the subscription key won't be used anymore.</span></span> <span data-ttu-id="2cfee-119">Instead, you will pass the access tokens obtained by the **Authorization** API.</span><span class="sxs-lookup"><span data-stu-id="2cfee-119">Instead, you will pass the access tokens obtained by the **Authorization** API.</span></span> 

<span data-ttu-id="2cfee-120">Each request should have a valid token, matching the access level of the API you are calling.</span><span class="sxs-lookup"><span data-stu-id="2cfee-120">Each request should have a valid token, matching the access level of the API you are calling.</span></span> <span data-ttu-id="2cfee-121">For example, operations on your user, such as getting your accounts, require a user access token.</span><span class="sxs-lookup"><span data-stu-id="2cfee-121">For example, operations on your user, such as getting your accounts, require a user access token.</span></span> <span data-ttu-id="2cfee-122">Operations on the account level, such as list all videos, require an account access token.</span><span class="sxs-lookup"><span data-stu-id="2cfee-122">Operations on the account level, such as list all videos, require an account access token.</span></span> <span data-ttu-id="2cfee-123">Operations on videos, such as reindex video, require either an account access token or a video access token.</span><span class="sxs-lookup"><span data-stu-id="2cfee-123">Operations on videos, such as reindex video, require either an account access token or a video access token.</span></span>

<span data-ttu-id="2cfee-124">To make things easier, you can use **Authorization** API > **GetAccounts** to get your accounts without obtaining a user token first.</span><span class="sxs-lookup"><span data-stu-id="2cfee-124">To make things easier, you can use **Authorization** API > **GetAccounts** to get your accounts without obtaining a user token first.</span></span> <span data-ttu-id="2cfee-125">You can also ask to get the accounts with valid tokens, enabling you to skip an additional call to get an account token.</span><span class="sxs-lookup"><span data-stu-id="2cfee-125">You can also ask to get the accounts with valid tokens, enabling you to skip an additional call to get an account token.</span></span>

<span data-ttu-id="2cfee-126">For more information about the different access tokens, see [Use Azure Video Indexer API](video-indexer-use-apis.md).</span><span class="sxs-lookup"><span data-stu-id="2cfee-126">For more information about the different access tokens, see [Use Azure Video Indexer API](video-indexer-use-apis.md).</span></span>

### <a name="locations"></a><span data-ttu-id="2cfee-127">Locations</span><span class="sxs-lookup"><span data-stu-id="2cfee-127">Locations</span></span>

<span data-ttu-id="2cfee-128">Each call to the API should include the location of your Video Indexer account.</span><span class="sxs-lookup"><span data-stu-id="2cfee-128">Each call to the API should include the location of your Video Indexer account.</span></span> <span data-ttu-id="2cfee-129">API calls without the location or with a wrong location will fail.</span><span class="sxs-lookup"><span data-stu-id="2cfee-129">API calls without the location or with a wrong location will fail.</span></span>

<span data-ttu-id="2cfee-130">The values described in the following table apply.</span><span class="sxs-lookup"><span data-stu-id="2cfee-130">The values described in the following table apply.</span></span> <span data-ttu-id="2cfee-131">The **Param value** is the value you pass when using the API.</span><span class="sxs-lookup"><span data-stu-id="2cfee-131">The **Param value** is the value you pass when using the API.</span></span>

|<span data-ttu-id="2cfee-132">**Name**</span><span class="sxs-lookup"><span data-stu-id="2cfee-132">**Name**</span></span>|<span data-ttu-id="2cfee-133">**Param value**</span><span class="sxs-lookup"><span data-stu-id="2cfee-133">**Param value**</span></span>|<span data-ttu-id="2cfee-134">**Description**</span><span class="sxs-lookup"><span data-stu-id="2cfee-134">**Description**</span></span>|
|---|---|---|
|<span data-ttu-id="2cfee-135">Trial</span><span class="sxs-lookup"><span data-stu-id="2cfee-135">Trial</span></span>|<span data-ttu-id="2cfee-136">trial</span><span class="sxs-lookup"><span data-stu-id="2cfee-136">trial</span></span>|<span data-ttu-id="2cfee-137">Used for trial accounts.</span><span class="sxs-lookup"><span data-stu-id="2cfee-137">Used for trial accounts.</span></span> <span data-ttu-id="2cfee-138">For example: https://api.videoindexer.ai/trial/Accounts/{accountId}/Videos/{videoId}/Index?language=English.</span><span class="sxs-lookup"><span data-stu-id="2cfee-138">For example: https://api.videoindexer.ai/trial/Accounts/{accountId}/Videos/{videoId}/Index?language=English.</span></span>|
|<span data-ttu-id="2cfee-139">West US</span><span class="sxs-lookup"><span data-stu-id="2cfee-139">West US</span></span>|<span data-ttu-id="2cfee-140">westus2</span><span class="sxs-lookup"><span data-stu-id="2cfee-140">westus2</span></span>|<span data-ttu-id="2cfee-141">Used for the Azure West US 2 region.</span><span class="sxs-lookup"><span data-stu-id="2cfee-141">Used for the Azure West US 2 region.</span></span>  <span data-ttu-id="2cfee-142">For example: https://api.videoindexer.ai/westus2/Accounts/{accountId}/Videos/{videoId}/Index?language=English.</span><span class="sxs-lookup"><span data-stu-id="2cfee-142">For example: https://api.videoindexer.ai/westus2/Accounts/{accountId}/Videos/{videoId}/Index?language=English.</span></span>|
|<span data-ttu-id="2cfee-143">North Europe</span><span class="sxs-lookup"><span data-stu-id="2cfee-143">North Europe</span></span> |<span data-ttu-id="2cfee-144">northeurope</span><span class="sxs-lookup"><span data-stu-id="2cfee-144">northeurope</span></span>|<span data-ttu-id="2cfee-145">Used for the Azure North Europe region.</span><span class="sxs-lookup"><span data-stu-id="2cfee-145">Used for the Azure North Europe region.</span></span> <span data-ttu-id="2cfee-146">For example:  https://api.videoindexer.ai/northeurope/Accounts/{accountId}/Videos/{videoId}/Index?language=English.</span><span class="sxs-lookup"><span data-stu-id="2cfee-146">For example:  https://api.videoindexer.ai/northeurope/Accounts/{accountId}/Videos/{videoId}/Index?language=English.</span></span> |
|<span data-ttu-id="2cfee-147">East Asia</span><span class="sxs-lookup"><span data-stu-id="2cfee-147">East Asia</span></span>|<span data-ttu-id="2cfee-148">eastasia</span><span class="sxs-lookup"><span data-stu-id="2cfee-148">eastasia</span></span>|<span data-ttu-id="2cfee-149">Used for the Azure East Asia region.</span><span class="sxs-lookup"><span data-stu-id="2cfee-149">Used for the Azure East Asia region.</span></span> <span data-ttu-id="2cfee-150">For example:  https://api.videoindexer.ai/eastasia/Accounts/{accountId}/Videos/{videoId}/Index?language=English.</span><span class="sxs-lookup"><span data-stu-id="2cfee-150">For example:  https://api.videoindexer.ai/eastasia/Accounts/{accountId}/Videos/{videoId}/Index?language=English.</span></span>|

### <a name="data-model"></a><span data-ttu-id="2cfee-151">Data Model</span><span class="sxs-lookup"><span data-stu-id="2cfee-151">Data Model</span></span>

<span data-ttu-id="2cfee-152">Video Indexer now has a simplified data model to deliver much clearer insights.</span><span class="sxs-lookup"><span data-stu-id="2cfee-152">Video Indexer now has a simplified data model to deliver much clearer insights.</span></span> <span data-ttu-id="2cfee-153">For more information about the output produced by the v2 API, see [Examine the Video Indexer output produced by the v2 API](video-indexer-output-json-v2.md).</span><span class="sxs-lookup"><span data-stu-id="2cfee-153">For more information about the output produced by the v2 API, see [Examine the Video Indexer output produced by the v2 API](video-indexer-output-json-v2.md).</span></span>

### <a name="swagger"></a><span data-ttu-id="2cfee-154">Swagger</span><span class="sxs-lookup"><span data-stu-id="2cfee-154">Swagger</span></span>

<span data-ttu-id="2cfee-155">The Video Indexer API definitions were updated accordingly and are available to download through the [API portal](https://api-portal.videoindexer.ai/docs/services/authorization/operations/Get-Account-Access-Token).</span><span class="sxs-lookup"><span data-stu-id="2cfee-155">The Video Indexer API definitions were updated accordingly and are available to download through the [API portal](https://api-portal.videoindexer.ai/docs/services/authorization/operations/Get-Account-Access-Token).</span></span>


### <a name="v1-vs-v2-examples"></a><span data-ttu-id="2cfee-156">V1 vs V2 examples</span><span class="sxs-lookup"><span data-stu-id="2cfee-156">V1 vs V2 examples</span></span>

<span data-ttu-id="2cfee-157">The new V2 APIs involve 3 main parameters:</span><span class="sxs-lookup"><span data-stu-id="2cfee-157">The new V2 APIs involve 3 main parameters:</span></span>

1. <span data-ttu-id="2cfee-158">[LOCATION] - As described above.</span><span class="sxs-lookup"><span data-stu-id="2cfee-158">[LOCATION] - As described above.</span></span> <span data-ttu-id="2cfee-159">Either trial, westus2, northeurope or eastasia.</span><span class="sxs-lookup"><span data-stu-id="2cfee-159">Either trial, westus2, northeurope or eastasia.</span></span>
2. <span data-ttu-id="2cfee-160">[YOUR_ACCOUNT_ID] - A Guid id of your account.</span><span class="sxs-lookup"><span data-stu-id="2cfee-160">[YOUR_ACCOUNT_ID] - A Guid id of your account.</span></span> <span data-ttu-id="2cfee-161">Retrieved when getting all accounts (described below).</span><span class="sxs-lookup"><span data-stu-id="2cfee-161">Retrieved when getting all accounts (described below).</span></span>
3. <span data-ttu-id="2cfee-162">[YOUR_VIDEO_ID] - The id of your video (e.g. "d4fa369abc").</span><span class="sxs-lookup"><span data-stu-id="2cfee-162">[YOUR_VIDEO_ID] - The id of your video (e.g. "d4fa369abc").</span></span> <span data-ttu-id="2cfee-163">Returned when uploading a video or when searching for videos.</span><span class="sxs-lookup"><span data-stu-id="2cfee-163">Returned when uploading a video or when searching for videos.</span></span>

#### <a name="uploading-a-video-in-v1"></a><span data-ttu-id="2cfee-164">Uploading a video in V1:</span><span class="sxs-lookup"><span data-stu-id="2cfee-164">Uploading a video in V1:</span></span>

```
https://videobreakdown.azure-api.net/Breakdowns/Api/Partner/Breakdowns?name=some_name&description=some_description&privacy=private&videoUrl=http://URL_TO_YOUR_VIDEO
```

#### <a name="uploading-a-video-in-v2"></a><span data-ttu-id="2cfee-165">Uploading a video in V2:</span><span class="sxs-lookup"><span data-stu-id="2cfee-165">Uploading a video in V2:</span></span>

1. <span data-ttu-id="2cfee-166">Get an access token for the upload request:</span><span class="sxs-lookup"><span data-stu-id="2cfee-166">Get an access token for the upload request:</span></span>

  <span data-ttu-id="2cfee-167">You can either get all accounts and their access tokens:</span><span class="sxs-lookup"><span data-stu-id="2cfee-167">You can either get all accounts and their access tokens:</span></span>

    ```
    https://api.videoindexer.ai/auth/[LOCATION]/Accounts?generateAccessTokens=true&allowEdit=true
    ```

  <span data-ttu-id="2cfee-168">Or get the specific account access token:</span><span class="sxs-lookup"><span data-stu-id="2cfee-168">Or get the specific account access token:</span></span>
  
  ```
  https://api.videoindexer.ai/auth/[LOCATION]/Accounts/[YOUR_ACCOUNT_ID]/AccessToken?allowEdit=true
  ```
2. <span data-ttu-id="2cfee-169">Upload a video:</span><span class="sxs-lookup"><span data-stu-id="2cfee-169">Upload a video:</span></span>

  ```
  POST https://api.videoindexer.ai/[LOCATION]/Accounts/[YOUR_ACCOUNT_ID]/Videos?name=MySample&description=MySampleDescription&videoUrl=[URL_ENCODED_VIDEO_URL]&accessToken=eyJ0eXAiOiJ...
  ```

#### <a name="getting-insights-in-v1"></a><span data-ttu-id="2cfee-170">Getting insights in V1:</span><span class="sxs-lookup"><span data-stu-id="2cfee-170">Getting insights in V1:</span></span>

```
https://videobreakdown.azure-api.net/Breakdowns/Api/Partner/Breakdowns/[VIDEO_ID]
```
  
#### <a name="getting-insights-in-v2"></a><span data-ttu-id="2cfee-171">Getting insights in V2:</span><span class="sxs-lookup"><span data-stu-id="2cfee-171">Getting insights in V2:</span></span>

1. <span data-ttu-id="2cfee-172">Either use the account access token, or get a video level access token:</span><span class="sxs-lookup"><span data-stu-id="2cfee-172">Either use the account access token, or get a video level access token:</span></span>

  ```
  https://api.videoindexer.ai/auth/[LOCATION]/Accounts/[YOUR_ACCOUNT_ID]/Videos/[VIDEO_ID]/AccessToken
  ```
  
2. <span data-ttu-id="2cfee-173">Get insights:</span><span class="sxs-lookup"><span data-stu-id="2cfee-173">Get insights:</span></span>

  ```
  https://api.videoindexer.ai/[LOCATION]/Accounts[YOUR_ACCOUNT_ID]/Videos/[VIDEO_ID]/Index?accessToken=eyJ0eXA...
  ```

#### <a name="getting-video-processing-state-in-v1"></a><span data-ttu-id="2cfee-174">Getting video processing state in V1:</span><span class="sxs-lookup"><span data-stu-id="2cfee-174">Getting video processing state in V1:</span></span>

```
https://videobreakdown.azure-api.net/Breakdowns/Api/Partner/Breakdowns/[VIDEO_ID]/State
```
  
#### <a name="getting-video-processing-state-in-v2"></a><span data-ttu-id="2cfee-175">Getting video processing state in V2:</span><span class="sxs-lookup"><span data-stu-id="2cfee-175">Getting video processing state in V2:</span></span>

<span data-ttu-id="2cfee-176">In API v2, the processing state is returned as part of the Get Video Index API.</span><span class="sxs-lookup"><span data-stu-id="2cfee-176">In API v2, the processing state is returned as part of the Get Video Index API.</span></span>

1. <span data-ttu-id="2cfee-177">Either use the account access token, or get a video level access token:</span><span class="sxs-lookup"><span data-stu-id="2cfee-177">Either use the account access token, or get a video level access token:</span></span>

  ```
  https://api.videoindexer.ai/trial/[LOCATION]/[YOUR_ACCOUNT_ID]/Videos/[VIDEO_ID]/Index?accessToken=eyJ0eXA...
  ```
  
2. <span data-ttu-id="2cfee-178">Get insights:</span><span class="sxs-lookup"><span data-stu-id="2cfee-178">Get insights:</span></span>

  ```
  https://api.videoindexer.ai/trial/[LOCATION]/[YOUR_ACCOUNT_ID]/Videos/[VIDEO_ID]/Index?accessToken=eyJ0eXA...
  ```

## <a name="next-steps"></a><span data-ttu-id="2cfee-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="2cfee-179">Next steps</span></span>

[<span data-ttu-id="2cfee-180">Use Azure Video Indexer API</span><span class="sxs-lookup"><span data-stu-id="2cfee-180">Use Azure Video Indexer API</span></span>](video-indexer-use-apis.md)

