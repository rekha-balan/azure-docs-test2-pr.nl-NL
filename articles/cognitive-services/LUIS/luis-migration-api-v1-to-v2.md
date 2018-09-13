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
# <a name="api-v2-migration-guide"></a>API v2 Migration guide
The version 1 [endpoint](https://aka.ms/v1-endpoint-api-docs) and [authoring](https://aka.ms/v1-authoring-api-docs) APIs will be deprecated. Use this guide to understand how to migrate to version 2 [endpoint](https://aka.ms/luis-endpoint-apis) and [authoring](https://aka.ms/luis-authoring-apis) APIs. 

## <a name="new-azure-regions"></a>New Azure regions
LUIS has new [regions](https://aka.ms/LUIS-regions) provided for the LUIS APIs. LUIS provides a different website for region groups. The application must be authored in the same region you expect to query. Applications do not automatically migrate regions. You export the app from one region then import into another for it to be available in a new region.

## <a name="authoring-route-changes"></a>Authoring route changes
The authoring API route changed from using the **prog** route to using the **api** route.


| version | route |
|--|--|
|1|/luis/v1.0/**prog**/apps|
|2|/luis/**api**/v2.0/apps|


## <a name="endpoint-route-changes"></a>Endpoint route changes
The endpoint API has new querystring parameters as well as a different response. If the verbose flag is true, all intents, regardless of score, are returned in an array named intents, in addition to the topScoringIntent.

| version | GET route |
|--|--|
|1|/luis/v1/application?ID={appId}&q={q}|
|2|/luis/v2.0/apps/{appId}?q={q}[&timezoneOffset][&verbose][&spellCheck][&staging][&bing-spell-check-subscription-key][&log]|


v1 endpoint success response:
```JSON
{
  "odata.metadata":"https://dialogice.cloudapp.net/odata/$metadata#domain","value":[
    {
      "id":"bccb84ee-4bd6-4460-a340-0595b12db294","q":"turn on the camera","response":"[{\"intent\":\"OpenCamera\",\"score\":0.976928055},{\"intent\":\"None\",\"score\":0.0230718572}]"
    }
  ]
}
```

v2 endpoint success response:
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

## <a name="key-management-no-longer-in-api"></a>Key management no longer in API
The subscription endpoint key APIs are deprecated, returning 410 GONE.

| version | route |
|--|--|
|1|/luis/v1.0/prog/subscriptions|
|1|/luis/v1.0/prog/subscriptions/{subscriptionKey}|

Azure [endpoint keys](luis-how-to-azure-subscription.md) are generated in the Azure portal. You assign the key to a LUIS app on the **[Publish](luis-how-to-manage-keys.md)** page. You do not need to know the actual key value. LUIS uses the subscription name to make the assignment. 

## <a name="new-versioning-route"></a>New versioning route
The v2 model is now contained in a [version](luis-how-to-manage-versions.md). A version name is 10 characters in the route. The default version is "0.1".

| version | route |
|--|--|
|1|/luis/v1.0/**prog**/apps/{appId}/entities|
|2|/luis/**api**/v2.0/apps/{appId}/**versions**/{versionId}/entities|

## <a name="metadata-renamed"></a>Metadata renamed
Several APIs that return LUIS metadata have new names.

| v1 route name | v2 route name |
|--|--|
|PersonalAssistantApps |assistants|
|applicationcultures|cultures|
|applicationdomains|domains|
|applicationusagescenarios|usagescenarios|


## <a name="sample-renamed-to-suggest"></a>"Sample" renamed to "suggest"
LUIS suggests utterances from existing [endpoint utterances](luis-how-to-review-endoint-utt.md) that may enhance the model. In the previous version, this was named **sample**. In the new version, the name is changed from sample to **suggest**. This is called **[Review endpoint utterances](luis-how-to-review-endoint-utt.md)** in the LUIS website.

| version | route |
|--|--|
|1|/luis/v1.0/**prog**/apps/{appId}/entities/{entityId}/**sample**|
|1|/luis/v1.0/**prog**/apps/{appId}/intents/{intentId}/**sample**|
|2|/luis/**api**/v2.0/apps/{appId}/**versions**/{versionId}/entities/{entityId}/**suggest**|
|2|/luis/**api**/v2.0/apps/{appId}/**versions**/{versionId}/intents/{intentId}/**suggest**|


## <a name="create-app-from-prebuilt-domains"></a>Create app from prebuilt domains
[Prebuilt domains](luis-how-to-use-prebuilt-domains.md) provide a predefined domain model. Prebuilt domains allow you to quickly develop your LUIS application for common domains. This API allows you to create a new app based on a prebuilt domain. The response is the new appID.

|v2 route|verb|
|--|--|
|/luis/api/v2.0/apps/customprebuiltdomains  |get, post|
|/luis/api/v2.0/apps/customprebuiltdomains/{culture}  |get|

## <a name="importing-1x-app-into-2x"></a>Importing 1.x app into 2.x
The exported 1.x app's JSON has some areas that you need to change before importing into [LUIS][LUIS] 2.0. 

### <a name="prebuilt-entities"></a>Prebuilt entities 
The [prebuilt entities](luis-prebuilt-entities.md) have changed. Make sure you are using the V2 prebuilt entities. This includes using [datetimeV2](luis-prebuilt-entities.md#use-a-prebuilt-datetimev2-entity), instead of datetime. 

### <a name="actions"></a>Actions
The actions property is no longer valid. It should be an empty 

### <a name="labeled-utterances"></a>Labeled utterances
V1 allowed labeled utterances to include spaces at the beginning or end of the word or phrase. Removed the spaces. 

## <a name="common-reasons-for-http-response-status-codes"></a>Common reasons for HTTP response status codes
See [LUIS API response codes](luis-reference-response-codes.md).

## <a name="next-steps"></a>Next steps

Use the v2 API documentation to update existing REST calls to LUIS [endpoint](https://aka.ms/luis-endpoint-apis) and [authoring](https://aka.ms/luis-authoring-apis) APIs. 

[LUIS]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-reference-regions