---
title: Language Understanding (LUIS) regions and endpoints - Azure - Cognitive Services LUIS | Microsoft Docs
titleSuffix: Azure
description: The region in which you publish your LUIS app corresponds to the region or location you specify in the Azure portal when you create an Azure LUIS endpoint key. When you publish an app, LUIS automatically generates an endpoint URL for the region associated with the key. To publish a LUIS app to more than one region, you need at least one key per region.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 08/23/2018
ms.author: diberry
ms.openlocfilehash: 7d4fc322763ce5bfd734f9ee197d4b8ffa296187
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864753"
---
# <a name="regions-and-keys"></a>Regions and keys

The region in which you publish your LUIS app corresponds to the region or location you specify in the Azure portal when you create an Azure LUIS endpoint key. When you [publish an app](./luis-how-to-publish-app.md), LUIS automatically generates an endpoint URL for the region associated with the key. To publish a LUIS app to more than one region, you need at least one key per region. 

## <a name="luis-website"></a>LUIS website
There are three LUIS websites, based on region. You must author and publish in the same region. 

|LUIS|Region|
|--|--|
|[www.luis.ai][www.luis.ai]|U.S.<br>not Europe<br>not Australia|
|[au.luis.ai][au.luis.ai]|Australia|
|[eu.luis.ai][eu.luis.ai]|Europe|


## <a name="publishing-regions"></a>Publishing regions

LUIS apps created on https://www.luis.ai can be published to all endpoints except the [European](#publishing-to-europe) and [Australian](#publishing-to-australia) regions. 

The authoring region app can only be published to a corresponding publish region. If your app is currently in the wrong authoring region, export the app, and import it into the correct authoring region for your publishing region. 

 Global region | Authoring region | Publishing & querying region   |   LUIS website | Endpoint URL format   |
|-----|------|------|------|------|
| Asia | West US| East Asia     | [www.luis.ai][www.luis.ai] |  https://eastasia.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY   |
| Asia | West US| Southeast Asia     | [www.luis.ai][www.luis.ai] |   https://southeastasia.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY   |
| *[Australia](#publishing-to-australia) | Australia East| Australia East     |   [au.luis.ai][au.luis.ai] | https://australiaeast.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY   |
| *[Europe](#publishing-to-europe)| West Europe| North Europe     | [eu.luis.ai][eu.luis.ai]|  https://northeurope.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY   | 
| *[Europe](#publishing-to-europe) | West Europe| West Europe     | [eu.luis.ai][eu.luis.ai]|  https://westeurope.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY   | 
| North America | West US | East US      |[www.luis.ai][www.luis.ai] |   https://eastus.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY   |
| North America | West US | East US 2     | [www.luis.ai][www.luis.ai] |  https://eastus2.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY   |
| North America | West US | South Central US     | [www.luis.ai][www.luis.ai] |  https://southcentralus.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY   | 
| North America | West US | West Central US     |[www.luis.ai][www.luis.ai] |  https://westcentralus.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY   |
| North America | West US | West US |  [www.luis.ai][www.luis.ai] | https://westus.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY  |
| North America | West US | West US 2    | [www.luis.ai][www.luis.ai] |  https://westus2.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY  |
| South America | West US | Brazil South     | [www.luis.ai][www.luis.ai] |  https://brazilsouth.api.cognitive.microsoft.com/luis/v2.0/apps/YOUR-APP-ID?subscription-key=YOUR-SUBSCRIPTION-KEY   |

## <a name="publishing-to-europe"></a>Publishing to Europe

To publish to the European regions, you create LUIS apps at https://eu.luis.ai only. If you attempt to publish anywhere else using a key in the Europe region, LUIS displays a warning message. Instead, use https://eu.luis.ai. LUIS apps created at [https://eu.luis.ai][eu.luis.ai] don't automatically migrate to other regions. Export and then import the LUIS app in order to migrate it.

## <a name="publishing-to-australia"></a>Publishing to Australia

To publish to the Australian regions, you create LUIS apps at https://au.luis.ai only. If you attempt to publish anywhere else using a key in the Australian region, LUIS displays a warning message. Instead, use https://au.luis.ai. LUIS apps created at [https://au.luis.ai][au.luis.ai] don't automatically migrate to other regions. Export and then import the LUIS app in order to migrate it.

## <a name="endpoints"></a>Endpoints

LUIS currently has 2 endpoints: one for authoring and one for text analysis.

|Purpose|URL|
|--|--|
|Authoring|`https://{region}.api.cognitive.microsoft.com/luis/api/v2.0/apps/{appID}/`|
|Text analysis (query prediction)|`https://{region}.api.cognitive.microsoft.com/luis/v2.0/apps/{appId}?q={q}[&timezoneOffset][&verbose][&spellCheck][&staging][&bing-spell-check-subscription-key][&log]`|

The following table explains the parameters, denoted with curly braces `{}`, in the previous table.

|Parameter|Purpose|
|--|--|
|region|Azure region - authoring and publishing have different regions|
|appID|LUIS app ID used in URL route and found on app dashboard|
|q|utterance text sent from client application such as chat bot|


## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Prebuilt entities reference](./luis-reference-prebuilt-entities.md)

 [www.luis.ai]: https://www.luis.ai
 [au.luis.ai]: https://au.luis.ai
 [eu.luis.ai]: https://eu.luis.ai