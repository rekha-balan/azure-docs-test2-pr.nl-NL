---
title: Analyze natural language text in Language Understanding (LUIS) using Javascript - Cognitive Services - Azure Cognitive Services | Microsoft Docs
description: In this quickstart, use an available public LUIS app to determine a user's intention from conversational text. Using Javascript, send the user's intention as text to the public app's HTTP prediction endpoint. At the endpoint, LUIS applies the public app's model to analyze the natural language text for meaning, determining overall intent and extracting data relevant to the app's subject domain.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: quickstart
ms.date: 08/23/2018
ms.author: diberry
ms.openlocfilehash: d787f744ff0fe7315553e9dd6f4465122f7e06b2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867032"
---
# <a name="quickstart-analyze-text-using-javascript"></a>Quickstart: Analyze text using Javascript

[!INCLUDE [Quickstart introduction for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-intro-para.md)]

<a name="create-luis-subscription-key"></a>

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-luis-repo-note.md)]

## <a name="prerequisites"></a>Prerequisites

* [Visual Studio Code](https://code.visualstudio.com/)
* Public app ID: df67dcdb-c37d-46af-88e1-8b97951ca1c2


## <a name="get-luis-key"></a>Get LUIS key

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-get-key-para.md)]

## <a name="analyze-text-with-browser"></a>Analyze text with browser

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-browser-para.md)]

## <a name="analyze-text-with-javascript"></a>Analyze text with Javascript 

You can use Javascript to access the same results you saw in the browser window in the previous step. 

1. Copy the code that follows and save it into an HTML file:

   [!code-html[Console app code that calls a LUIS endpoint](~/samples-luis/documentation-samples/quickstarts/analyze-text/javascript/call-endpoint.html)]

2. Open the file in a browser. Enter your LUIS endpoint key in the form and select **Submit**.

    ![Html sample displayed in browser with LUIS results for Home Automation app](./media/luis-get-started-js-get-intent/html-results.png)

    The result display under the form. 

## <a name="luis-keys"></a>LUIS keys

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-key-usage-para.md)]

## <a name="clean-up-resources"></a>Clean up resources

Delete the Javascript file.

## <a name="next-steps"></a>Next steps
> [!div class="nextstepaction"]
> [Add utterances](luis-get-started-javascript-add-utterance.md)
