---
title: Data conversion concepts in LUIS - Language Understanding
titleSuffix: Azure Cognitive Services
description: Learn how utterances can be changed before predictions in Language Understanding (LUIS)
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 06/27/2018
ms.author: diberry
ms.openlocfilehash: e1d0e0a0205190846612d727fbf34404e33c3ad4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857629"
---
# <a name="data-conversion-concepts-in-luis"></a>Data conversion concepts in LUIS
LUIS provides a way to convert utterances from spoken utterances to text utterances before prediction. 

## <a name="speech-to-intent-conversion-concepts"></a>Speech to intent conversion concepts
Conversion of speech to text in LUIS allows you to send spoken utterances to an endpoint and receive a LUIS prediction response. The process is an integration of the [Speech](https://docs.microsoft.com/azure/cognitive-services/Speech) service with LUIS. 

### <a name="key-requirements"></a>Key requirements
You do not need to create a **Bing Speech API** key for this integration. A **Language Understanding** key created in the Azure portal works for this integration. Do not use the LUIS starter key, it will not work for this integration.

### <a name="new-endpoint"></a>New endpoint 
This integration creates a new endpoint and [pricing](luis-boundaries.md#key-limits) model. The endpoint, via the [Speech SDK](https://github.com/Azure-Samples/cognitive-services-speech-sdk), is able to receive both spoken and text utterances allowing you to use it as a single endpoint. 

### <a name="quota-usage"></a>Quota usage
See [Key limits](luis-boundaries.md#key-limits) for information. 

### <a name="data-retention"></a>Data retention
The data sent to the endpoint, via the Speech SDK, regardless if it is speech or text, is only used to enhance your speech model. It is not used beyond your model to enhance either Speech or LUIS in a general capacity. When the LUIS app is deleted, the retained data is also deleted.

<!-- TBD: Machine translation conversion concepts -->

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Use speech to text](luis-tutorial-speech-to-intent.md)

