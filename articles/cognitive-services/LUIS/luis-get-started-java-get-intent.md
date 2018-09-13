---
title: Analyze natural language text in Language Understanding (LUIS) using Java - Cognitive Services - Azure Cognitive Services | Microsoft Docs
description: In this quickstart, use an available public LUIS app to determine a user's intention from conversational text. Using Java, send the user's intention as text to the public app's HTTP prediction endpoint. At the endpoint, LUIS applies the public app's model to analyze the natural language text for meaning, determining overall intent and extracting data relevant to the app's subject domain.
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: quickstart
ms.date: 06/27/2018
ms.author: diberry
ms.openlocfilehash: 4dd5437940994a2f264b5a11baebcd67fdddb43d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869316"
---
# <a name="quickstart-analyze-text-using-java"></a>Quickstart: Analyze text using Java

[!INCLUDE [Quickstart introduction for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-intro-para.md)]

<a name="create-luis-subscription-key"></a>

## <a name="prerequisites"></a>Prerequisites

* [JDK SE](http://www.oracle.com/technetwork/java/javase/downloads/index.html)  (Java Development Kit, Standard Edition)
* [Visual Studio Code](https://code.visualstudio.com/)
* Public app ID: df67dcdb-c37d-46af-88e1-8b97951ca1c2


[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-luis-repo-note.md)]

## <a name="get-luis-key"></a>Get LUIS key

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-get-key-para.md)]

## <a name="analyze-text-with-browser"></a>Analyze text with browser

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-browser-para.md)]

## <a name="analyze-text-with-java"></a>Analyze text with Java 

You can use Java to access the same results you saw in the browser window in the previous step. 

1. Copy the following code to create a class in a file named `LuisGetRequest.java`:

   [!code-java[Console app code that calls a LUIS endpoint](~/samples-luis/documentation-samples/quickstarts/analyze-text/java/call-endpoint.java)]

2. Replace the value of the `YOUR-KEY` variable with your LUIS key.

3. Compile the java program with `javac -cp ":lib/*" LuisGetRequest.java`. 

4. Run the application with `java -cp ":lib/*" LuisGetRequest.java`. It displays the same JSON that you saw earlier in the browser window.

    ![Console window displays JSON result from LUIS](./media/luis-get-started-java-get-intent/console-turn-on.png)
    
## <a name="luis-keys"></a>LUIS keys

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-key-usage-para.md)]

## <a name="clean-up-resources"></a>Clean up resources

Delete the Java file. 

## <a name="next-steps"></a>Next steps
> [!div class="nextstepaction"]
> [Add utterances](luis-get-started-java-add-utterance.md)