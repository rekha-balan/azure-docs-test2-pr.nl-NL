---
title: Speech service regions
description: Reference for regions of the Speech service.
services: cognitive-services
author: mahilleb-msft
ms.service: cognitive-services
ms.technology: speech
ms.topic: article
ms.date: 06/28/2018
ms.author: mahilleb
ms.openlocfilehash: d8b72ea30a10e45f5415f7ab9054d8a4b6f30789
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965569"
---
# <a name="regions-of-the-speech-service"></a>Regions of the Speech service

The Speech service is available in different regions.
When you create a subscription you can pick an available region, depending on your needs.

When you use your subscription you have to account for the region you picked.

## <a name="rest-api"></a>REST API

Using the REST API, pick the right region-specific endpoints.
See [REST APIs](rest-apis.md) for details.

## <a name="speech-sdk"></a>Speech SDK

In the [Speech SDK](speech-sdk.md), regions are specified as a string (for example, as a parameter to [SpeechFactory.FromSubscription](https://docs.microsoft.com/dotnet/api/microsoft.cognitiveservices.speech.speechfactory.fromsubscription) in the Speech SDK for C#).

### <a name="regions-for-speech-recognition-and-translation"></a>Regions for speech recognition and translation

The table below lists the available regions for **speech recognition** and **translation**:

Region| Value for region parameter in the Speech SDK| Portal
-|-
West US| `westus`| https://westus.cris.ai
West US2| `westus2`| https://westus2.cris.ai
East US| `eastus`| https://eastus.cris.ai
East US2| `eastus2`| https://eastus2.cris.ai
East Asia| `eastasia`| https://eastasia.cris.ai
South East Asia| `southeastasia`| https://southeastasia.cris.ai
North Europe| `northeurope`| https://northeurope.cris.ai
West Europe|  `westeurope`| https://westeurope.cris.ai

### <a name="regions-for-intent-recognition"></a>Regions for intent recognition

Available regions for **intent recognition** via the Speech SDK are listed in the [Language Understanding service region page](/azure/cognitive-services/luis/luis-reference-regions).
For each publishing region listed, the corresponding Speech SDK region parameter is determined as the first part of the domain name of the endpoint.
For example, use `westus` to specify the West US publishing region.
