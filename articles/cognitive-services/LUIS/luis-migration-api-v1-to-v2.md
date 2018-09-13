---
title: API Migration guide from v1 to v2
titleSuffix: Azure Cognitive Services
description: Learn how to migration to the latest API set.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 09/06/2018
ms.author: diberry
ms.openlocfilehash: cea7d4bb8da47f935553cbcad787f4acd95b2f75
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866817"
---
# <a name="api-v2-migration-guide"></a><span data-ttu-id="4b217-103">API v2 Migration guide</span><span class="sxs-lookup"><span data-stu-id="4b217-103">API v2 Migration guide</span></span>
<span data-ttu-id="4b217-104">The version 1 [endpoint](https://aka.ms/v1-endpoint-api-docs) and [authoring](https://aka.ms/v1-authoring-api-docs) APIs will be deprecated.</span><span class="sxs-lookup"><span data-stu-id="4b217-104">The version 1 [endpoint](https://aka.ms/v1-endpoint-api-docs) and [authoring](https://aka.ms/v1-authoring-api-docs) APIs will be deprecated.</span></span> <span data-ttu-id="4b217-105">Use this guide to understand how to migrate to version 2 [endpoint](https://aka.ms/luis-endpoint-apis) and [authoring](https://aka.ms/luis-authoring-apis) APIs.</span><span class="sxs-lookup"><span data-stu-id="4b217-105">Use this guide to understand how to migrate to version 2 [endpoint](https://aka.ms/luis-endpoint-apis) and [authoring](https://aka.ms/luis-authoring-apis) APIs.</span></span> 

## <a name="new-azure-regions"></a><span data-ttu-id="4b217-106">New Azure regions</span><span class="sxs-lookup"><span data-stu-id="4b217-106">New Azure regions</span></span>
<span data-ttu-id="4b217-107">LUIS has new [regions](https://aka.ms/LUIS-regions) provided for the LUIS APIs.</span><span class="sxs-lookup"><span data-stu-id="4b217-107">LUIS has new [regions](https://aka.ms/LUIS-regions) provided for the LUIS APIs.</span></span> <span data-ttu-id="4b217-108">LUIS provides a different website for region groups.</span><span class="sxs-lookup"><span data-stu-id="4b217-108">LUIS provides a different website for region groups.</span></span> <span data-ttu-id="4b217-109">The application must be authored in the same region you expect to query.</span><span class="sxs-lookup"><span data-stu-id="4b217-109">The application must be authored in the same region you expect to query.</span></span> <span data-ttu-id="4b217-110">Applications do not automatically migrate regions.</span><span class="sxs-lookup"><span data-stu-id="4b217-110">Applications do not automatically migrate regions.</span></span> <span data-ttu-id="4b217-111">You export the app from one region then import into another for it to be available in a new region.</span><span class="sxs-lookup"><span data-stu-id="4b217-111">You export the app from one region then import into another for it to be available in a new region.</span></span>

## <a name="authoring-route-changes"></a><span data-ttu-id="4b217-112">Authoring route changes</span><span class="sxs-lookup"><span data-stu-id="4b217-112">Authoring route changes</span></span>
<span data-ttu-id="4b217-113">The authoring API route changed from using the **prog** route to using the **api** route.</span><span class="sxs-lookup"><span data-stu-id="4b217-113">The authoring API route changed from using the **prog** route to using the **api** route.</span></span>


| <span data-ttu-id="4b217-114">version</span><span class="sxs-lookup"><span data-stu-id="4b217-114">version</span></span> | <span data-ttu-id="4b217-115">route</span><span class="sxs-lookup"><span data-stu-id="4b217-115">route</span></span> |
|--|--|
|<span data-ttu-id="4b217-116">1</span><span class="sxs-lookup"><span data-stu-id="4b217-116">1</span></span>|<span data-ttu-id="4b217-117">/luis/v1.0/**prog**/apps</span><span class="sxs-lookup"><span data-stu-id="4b217-117">/luis/v1.0/**prog**/apps</span></span>|
|<span data-ttu-id="4b217-118">2</span><span class="sxs-lookup"><span data-stu-id="4b217-118">2</span></span>|<span data-ttu-id="4b217-119">/luis/**api**/v2.0/apps</span><span class="sxs-lookup"><span data-stu-id="4b217-119">/luis/**api**/v2.0/apps</span></span>|


## <a name="endpoint-route-changes"></a><span data-ttu-id="4b217-120">Endpoint route changes</span><span class="sxs-lookup"><span data-stu-id="4b217-120">Endpoint route changes</span></span>
<span data-ttu-id="4b217-121">The endpoint API has new querystring parameters as well as a different response.</span><span class="sxs-lookup"><span data-stu-id="4b217-121">The endpoint API has new querystring parameters as well as a different response.</span></span> <span data-ttu-id="4b217-122">If the verbose flag is true, all intents, regardless of score, are returned in an array named intents, in addition to the topScoringIntent.</span><span class="sxs-lookup"><span data-stu-id="4b217-122">If the verbose flag is true, all intents, regardless of score, are returned in an array named intents, in addition to the topScoringIntent.</span></span>

| <span data-ttu-id="4b217-123">version</span><span class="sxs-lookup"><span data-stu-id="4b217-123">version</span></span> | <span data-ttu-id="4b217-124">GET route</span><span class="sxs-lookup"><span data-stu-id="4b217-124">GET route</span></span> |
|--|--|
|<span data-ttu-id="4b217-125">1</span><span class="sxs-lookup"><span data-stu-id="4b217-125">1</span></span>|<span data-ttu-id="4b217-126">/luis/v1/application?ID={appId}&q={q}</span><span class="sxs-lookup"><span data-stu-id="4b217-126">/luis/v1/application?ID={appId}&q={q}</span></span>|
|<span data-ttu-id="4b217-127">2</span><span class="sxs-lookup"><span data-stu-id="4b217-127">2</span></span>|<span data-ttu-id="4b217-128">/luis/v2.0/apps/{appId}?q={q}[&timezoneOffset][&verbose][&spellCheck][&staging][&bing-spell-check-subscription-key][&log]</span><span class="sxs-lookup"><span data-stu-id="4b217-128">/luis/v2.0/apps/{appId}?q={q}[&timezoneOffset][&verbose][&spellCheck][&staging][&bing-spell-check-subscription-key][&log]</span></span>|


<span data-ttu-id="4b217-129">v1 endpoint success response:</span><span class="sxs-lookup"><span data-stu-id="4b217-129">v1 endpoint success response:</span></span>
```JSON
{
  "odata.metadata":"https://dialogice.cloudapp.net/odata/$metadata#domain","value":[
    {
      "id":"bccb84ee-4bd6-4460-a340-0595b12db294","q":"turn on the camera","response":"[{\"intent\":\"OpenCamera\",\"score\":0.976928055},{\"intent\":\"None\",\"score\":0.0230718572}]"
    }
  ]
}
```

<span data-ttu-id="4b217-130">v2 endpoint success response:</span><span class="sxs-lookup"><span data-stu-id="4b217-130">v2 endpoint success response:</span></span>
```JSON
{
  "query": "forward to frank 30 dollars through HSBC",
  "topScoringIntent": {
    "intent": "give",
    "score": 0.3964121
  },
  "entities": [
    {
      "entity": "30",
      "type": "builtin.number",
      "startIndex": 17,
      "endIndex": 18,
      "resolution": {
        "value": "30"
      }
    },
    {
      "entity": "frank",
      "type": "frank",
      "startIndex": 11,
      "endIndex": 15,
      "score": 0.935219169
    },
    {
      "entity": "30 dollars",
      "type": "builtin.currency",
      "startIndex": 17,
      "endIndex": 26,
      "resolution": {
        "unit": "Dollar",
        "value": "30"
      }
    },
    {
      "entity": "hsbc",
      "type": "Bank",
      "startIndex": 36,
      "endIndex": 39,
      "resolution": {
        "values": [
          "BankeName"
        ]
      }
    }
  ]
}
```

## <a name="key-management-no-longer-in-api"></a><span data-ttu-id="4b217-131">Key management no longer in API</span><span class="sxs-lookup"><span data-stu-id="4b217-131">Key management no longer in API</span></span>
<span data-ttu-id="4b217-132">The subscription endpoint key APIs are deprecated, returning 410 GONE.</span><span class="sxs-lookup"><span data-stu-id="4b217-132">The subscription endpoint key APIs are deprecated, returning 410 GONE.</span></span>

| <span data-ttu-id="4b217-133">version</span><span class="sxs-lookup"><span data-stu-id="4b217-133">version</span></span> | <span data-ttu-id="4b217-134">route</span><span class="sxs-lookup"><span data-stu-id="4b217-134">route</span></span> |
|--|--|
|<span data-ttu-id="4b217-135">1</span><span class="sxs-lookup"><span data-stu-id="4b217-135">1</span></span>|<span data-ttu-id="4b217-136">/luis/v1.0/prog/subscriptions</span><span class="sxs-lookup"><span data-stu-id="4b217-136">/luis/v1.0/prog/subscriptions</span></span>|
|<span data-ttu-id="4b217-137">1</span><span class="sxs-lookup"><span data-stu-id="4b217-137">1</span></span>|<span data-ttu-id="4b217-138">/luis/v1.0/prog/subscriptions/{subscriptionKey}</span><span class="sxs-lookup"><span data-stu-id="4b217-138">/luis/v1.0/prog/subscriptions/{subscriptionKey}</span></span>|

<span data-ttu-id="4b217-139">Azure [endpoint keys](luis-how-to-azure-subscription.md) are generated in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4b217-139">Azure [endpoint keys](luis-how-to-azure-subscription.md) are generated in the Azure portal.</span></span> <span data-ttu-id="4b217-140">You assign the key to a LUIS app on the **[Publish](luis-how-to-manage-keys.md)** page.</span><span class="sxs-lookup"><span data-stu-id="4b217-140">You assign the key to a LUIS app on the **[Publish](luis-how-to-manage-keys.md)** page.</span></span> <span data-ttu-id="4b217-141">You do not need to know the actual key value.</span><span class="sxs-lookup"><span data-stu-id="4b217-141">You do not need to know the actual key value.</span></span> <span data-ttu-id="4b217-142">LUIS uses the subscription name to make the assignment.</span><span class="sxs-lookup"><span data-stu-id="4b217-142">LUIS uses the subscription name to make the assignment.</span></span> 

## <a name="new-versioning-route"></a><span data-ttu-id="4b217-143">New versioning route</span><span class="sxs-lookup"><span data-stu-id="4b217-143">New versioning route</span></span>
<span data-ttu-id="4b217-144">The v2 model is now contained in a [version](luis-how-to-manage-versions.md).</span><span class="sxs-lookup"><span data-stu-id="4b217-144">The v2 model is now contained in a [version](luis-how-to-manage-versions.md).</span></span> <span data-ttu-id="4b217-145">A version name is 10 characters in the route.</span><span class="sxs-lookup"><span data-stu-id="4b217-145">A version name is 10 characters in the route.</span></span> <span data-ttu-id="4b217-146">The default version is "0.1".</span><span class="sxs-lookup"><span data-stu-id="4b217-146">The default version is "0.1".</span></span>

| <span data-ttu-id="4b217-147">version</span><span class="sxs-lookup"><span data-stu-id="4b217-147">version</span></span> | <span data-ttu-id="4b217-148">route</span><span class="sxs-lookup"><span data-stu-id="4b217-148">route</span></span> |
|--|--|
|<span data-ttu-id="4b217-149">1</span><span class="sxs-lookup"><span data-stu-id="4b217-149">1</span></span>|<span data-ttu-id="4b217-150">/luis/v1.0/**prog**/apps/{appId}/entities</span><span class="sxs-lookup"><span data-stu-id="4b217-150">/luis/v1.0/**prog**/apps/{appId}/entities</span></span>|
|<span data-ttu-id="4b217-151">2</span><span class="sxs-lookup"><span data-stu-id="4b217-151">2</span></span>|<span data-ttu-id="4b217-152">/luis/**api**/v2.0/apps/{appId}/**versions**/{versionId}/entities</span><span class="sxs-lookup"><span data-stu-id="4b217-152">/luis/**api**/v2.0/apps/{appId}/**versions**/{versionId}/entities</span></span>|

## <a name="metadata-renamed"></a><span data-ttu-id="4b217-153">Metadata renamed</span><span class="sxs-lookup"><span data-stu-id="4b217-153">Metadata renamed</span></span>
<span data-ttu-id="4b217-154">Several APIs that return LUIS metadata have new names.</span><span class="sxs-lookup"><span data-stu-id="4b217-154">Several APIs that return LUIS metadata have new names.</span></span>

| <span data-ttu-id="4b217-155">v1 route name</span><span class="sxs-lookup"><span data-stu-id="4b217-155">v1 route name</span></span> | <span data-ttu-id="4b217-156">v2 route name</span><span class="sxs-lookup"><span data-stu-id="4b217-156">v2 route name</span></span> |
|--|--|
|<span data-ttu-id="4b217-157">PersonalAssistantApps</span><span class="sxs-lookup"><span data-stu-id="4b217-157">PersonalAssistantApps</span></span> |<span data-ttu-id="4b217-158">assistants</span><span class="sxs-lookup"><span data-stu-id="4b217-158">assistants</span></span>|
|<span data-ttu-id="4b217-159">applicationcultures</span><span class="sxs-lookup"><span data-stu-id="4b217-159">applicationcultures</span></span>|<span data-ttu-id="4b217-160">cultures</span><span class="sxs-lookup"><span data-stu-id="4b217-160">cultures</span></span>|
|<span data-ttu-id="4b217-161">applicationdomains</span><span class="sxs-lookup"><span data-stu-id="4b217-161">applicationdomains</span></span>|<span data-ttu-id="4b217-162">domains</span><span class="sxs-lookup"><span data-stu-id="4b217-162">domains</span></span>|
|<span data-ttu-id="4b217-163">applicationusagescenarios</span><span class="sxs-lookup"><span data-stu-id="4b217-163">applicationusagescenarios</span></span>|<span data-ttu-id="4b217-164">usagescenarios</span><span class="sxs-lookup"><span data-stu-id="4b217-164">usagescenarios</span></span>|


## <a name="sample-renamed-to-suggest"></a><span data-ttu-id="4b217-165">"Sample" renamed to "suggest"</span><span class="sxs-lookup"><span data-stu-id="4b217-165">"Sample" renamed to "suggest"</span></span>
<span data-ttu-id="4b217-166">LUIS suggests utterances from existing [endpoint utterances](luis-how-to-review-endoint-utt.md) that may enhance the model.</span><span class="sxs-lookup"><span data-stu-id="4b217-166">LUIS suggests utterances from existing [endpoint utterances](luis-how-to-review-endoint-utt.md) that may enhance the model.</span></span> <span data-ttu-id="4b217-167">In the previous version, this was named **sample**.</span><span class="sxs-lookup"><span data-stu-id="4b217-167">In the previous version, this was named **sample**.</span></span> <span data-ttu-id="4b217-168">In the new version, the name is changed from sample to **suggest**.</span><span class="sxs-lookup"><span data-stu-id="4b217-168">In the new version, the name is changed from sample to **suggest**.</span></span> <span data-ttu-id="4b217-169">This is called **[Review endpoint utterances](luis-how-to-review-endoint-utt.md)** in the LUIS website.</span><span class="sxs-lookup"><span data-stu-id="4b217-169">This is called **[Review endpoint utterances](luis-how-to-review-endoint-utt.md)** in the LUIS website.</span></span>

| <span data-ttu-id="4b217-170">version</span><span class="sxs-lookup"><span data-stu-id="4b217-170">version</span></span> | <span data-ttu-id="4b217-171">route</span><span class="sxs-lookup"><span data-stu-id="4b217-171">route</span></span> |
|--|--|
|<span data-ttu-id="4b217-172">1</span><span class="sxs-lookup"><span data-stu-id="4b217-172">1</span></span>|<span data-ttu-id="4b217-173">/luis/v1.0/**prog**/apps/{appId}/entities/{entityId}/**sample**</span><span class="sxs-lookup"><span data-stu-id="4b217-173">/luis/v1.0/**prog**/apps/{appId}/entities/{entityId}/**sample**</span></span>|
|<span data-ttu-id="4b217-174">1</span><span class="sxs-lookup"><span data-stu-id="4b217-174">1</span></span>|<span data-ttu-id="4b217-175">/luis/v1.0/**prog**/apps/{appId}/intents/{intentId}/**sample**</span><span class="sxs-lookup"><span data-stu-id="4b217-175">/luis/v1.0/**prog**/apps/{appId}/intents/{intentId}/**sample**</span></span>|
|<span data-ttu-id="4b217-176">2</span><span class="sxs-lookup"><span data-stu-id="4b217-176">2</span></span>|<span data-ttu-id="4b217-177">/luis/**api**/v2.0/apps/{appId}/**versions**/{versionId}/entities/{entityId}/**suggest**</span><span class="sxs-lookup"><span data-stu-id="4b217-177">/luis/**api**/v2.0/apps/{appId}/**versions**/{versionId}/entities/{entityId}/**suggest**</span></span>|
|<span data-ttu-id="4b217-178">2</span><span class="sxs-lookup"><span data-stu-id="4b217-178">2</span></span>|<span data-ttu-id="4b217-179">/luis/**api**/v2.0/apps/{appId}/**versions**/{versionId}/intents/{intentId}/**suggest**</span><span class="sxs-lookup"><span data-stu-id="4b217-179">/luis/**api**/v2.0/apps/{appId}/**versions**/{versionId}/intents/{intentId}/**suggest**</span></span>|


## <a name="create-app-from-prebuilt-domains"></a><span data-ttu-id="4b217-180">Create app from prebuilt domains</span><span class="sxs-lookup"><span data-stu-id="4b217-180">Create app from prebuilt domains</span></span>
<span data-ttu-id="4b217-181">[Prebuilt domains](luis-how-to-use-prebuilt-domains.md) provide a predefined domain model.</span><span class="sxs-lookup"><span data-stu-id="4b217-181">[Prebuilt domains](luis-how-to-use-prebuilt-domains.md) provide a predefined domain model.</span></span> <span data-ttu-id="4b217-182">Prebuilt domains allow you to quickly develop your LUIS application for common domains.</span><span class="sxs-lookup"><span data-stu-id="4b217-182">Prebuilt domains allow you to quickly develop your LUIS application for common domains.</span></span> <span data-ttu-id="4b217-183">This API allows you to create a new app based on a prebuilt domain.</span><span class="sxs-lookup"><span data-stu-id="4b217-183">This API allows you to create a new app based on a prebuilt domain.</span></span> <span data-ttu-id="4b217-184">The response is the new appID.</span><span class="sxs-lookup"><span data-stu-id="4b217-184">The response is the new appID.</span></span>

|<span data-ttu-id="4b217-185">v2 route</span><span class="sxs-lookup"><span data-stu-id="4b217-185">v2 route</span></span>|<span data-ttu-id="4b217-186">verb</span><span class="sxs-lookup"><span data-stu-id="4b217-186">verb</span></span>|
|--|--|
|<span data-ttu-id="4b217-187">/luis/api/v2.0/apps/customprebuiltdomains</span><span class="sxs-lookup"><span data-stu-id="4b217-187">/luis/api/v2.0/apps/customprebuiltdomains</span></span>  |<span data-ttu-id="4b217-188">get, post</span><span class="sxs-lookup"><span data-stu-id="4b217-188">get, post</span></span>|
|<span data-ttu-id="4b217-189">/luis/api/v2.0/apps/customprebuiltdomains/{culture}</span><span class="sxs-lookup"><span data-stu-id="4b217-189">/luis/api/v2.0/apps/customprebuiltdomains/{culture}</span></span>  |<span data-ttu-id="4b217-190">get</span><span class="sxs-lookup"><span data-stu-id="4b217-190">get</span></span>|

## <a name="importing-1x-app-into-2x"></a><span data-ttu-id="4b217-191">Importing 1.x app into 2.x</span><span class="sxs-lookup"><span data-stu-id="4b217-191">Importing 1.x app into 2.x</span></span>
<span data-ttu-id="4b217-192">The exported 1.x app's JSON has some areas that you need to change before importing into [LUIS][LUIS] 2.0.</span><span class="sxs-lookup"><span data-stu-id="4b217-192">The exported 1.x app's JSON has some areas that you need to change before importing into [LUIS][LUIS] 2.0.</span></span> 

### <a name="prebuilt-entities"></a><span data-ttu-id="4b217-193">Prebuilt entities</span><span class="sxs-lookup"><span data-stu-id="4b217-193">Prebuilt entities</span></span> 
<span data-ttu-id="4b217-194">The [prebuilt entities](luis-prebuilt-entities.md) have changed.</span><span class="sxs-lookup"><span data-stu-id="4b217-194">The [prebuilt entities](luis-prebuilt-entities.md) have changed.</span></span> <span data-ttu-id="4b217-195">Make sure you are using the V2 prebuilt entities.</span><span class="sxs-lookup"><span data-stu-id="4b217-195">Make sure you are using the V2 prebuilt entities.</span></span> <span data-ttu-id="4b217-196">This includes using [datetimeV2](luis-prebuilt-entities.md#use-a-prebuilt-datetimev2-entity), instead of datetime.</span><span class="sxs-lookup"><span data-stu-id="4b217-196">This includes using [datetimeV2](luis-prebuilt-entities.md#use-a-prebuilt-datetimev2-entity), instead of datetime.</span></span> 

### <a name="actions"></a><span data-ttu-id="4b217-197">Actions</span><span class="sxs-lookup"><span data-stu-id="4b217-197">Actions</span></span>
<span data-ttu-id="4b217-198">The actions property is no longer valid.</span><span class="sxs-lookup"><span data-stu-id="4b217-198">The actions property is no longer valid.</span></span> <span data-ttu-id="4b217-199">It should be an empty</span><span class="sxs-lookup"><span data-stu-id="4b217-199">It should be an empty</span></span> 

### <a name="labeled-utterances"></a><span data-ttu-id="4b217-200">Labeled utterances</span><span class="sxs-lookup"><span data-stu-id="4b217-200">Labeled utterances</span></span>
<span data-ttu-id="4b217-201">V1 allowed labeled utterances to include spaces at the beginning or end of the word or phrase.</span><span class="sxs-lookup"><span data-stu-id="4b217-201">V1 allowed labeled utterances to include spaces at the beginning or end of the word or phrase.</span></span> <span data-ttu-id="4b217-202">Removed the spaces.</span><span class="sxs-lookup"><span data-stu-id="4b217-202">Removed the spaces.</span></span> 

## <a name="common-reasons-for-http-response-status-codes"></a><span data-ttu-id="4b217-203">Common reasons for HTTP response status codes</span><span class="sxs-lookup"><span data-stu-id="4b217-203">Common reasons for HTTP response status codes</span></span>
<span data-ttu-id="4b217-204">See [LUIS API response codes](luis-reference-response-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4b217-204">See [LUIS API response codes](luis-reference-response-codes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b217-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="4b217-205">Next steps</span></span>

<span data-ttu-id="4b217-206">Use the v2 API documentation to update existing REST calls to LUIS [endpoint](https://aka.ms/luis-endpoint-apis) and [authoring](https://aka.ms/luis-authoring-apis) APIs.</span><span class="sxs-lookup"><span data-stu-id="4b217-206">Use the v2 API documentation to update existing REST calls to LUIS [endpoint](https://aka.ms/luis-endpoint-apis) and [authoring](https://aka.ms/luis-authoring-apis) APIs.</span></span> 

[LUIS]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-reference-regions