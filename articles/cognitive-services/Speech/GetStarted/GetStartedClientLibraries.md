---
title: Get started with the Microsoft Speech Recognition API by using Bing Speech client libraries | Microsoft Docs
description: Use the Microsoft Speech Service client libraries in Microsoft Cognitive Services to develop applications that convert spoken audio to text.
services: cognitive-services
author: zhouwangzw
manager: wolfma
ms.service: cognitive-services
ms.component: bing-speech
ms.topic: article
ms.date: 09/15/2017
ms.author: zhouwang
ms.openlocfilehash: 6fb490def6807204943a1ce3ba3c53186055102b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868958"
---
# <a name="get-started-with-bing-speech-service-client-libraries"></a>Get started with Bing Speech Service client libraries

Besides making direct HTTP requests via a REST API, Bing Speech Service provides developers with Speech client libraries in different languages. The Speech client libraries:

- Support more advanced capabilities in speech recognition, such as intermediate results in real time, long audio stream (up to 10 minutes), and continuous recognition.
- Provide a simple and idiomatic API in the language of your preference.
- Hide low-level communication details.

Currently, the following Bing Speech client libraries are available:

- [C# desktop library](GetStartedCSharpDesktop.md)
- [C# service library](GetStartedCSharpServiceLibrary.md)
- [JavaScript library](GetStartedJSWebsockets.md)
- [Java library for Android](GetStartedJavaAndroid.md)
- [Objective-C library for iOS](Get-Started-ObjectiveC-iOS.md)

> [!NOTE] 
In May 2018, we also released the new [Speech Service](../../speech-service/index.yml) in public preview. We encourage you to [try it out for free](../../speech-service/get-started.md). 

## <a name="additional-resources"></a>Additional resources

- The [samples](../samples.md) page provides complete samples to use Speech client libraries.
- If you need a client library that's not yet supported, you can create your own SDK. Implement the [Speech WebSocket protocol](../API-Reference-REST/websocketprotocol.md) on the platform and use the language of your choice.

## <a name="license"></a>License

All Cognitive Services SDKs and samples are licensed with the MIT License. For more information, see [License](https://github.com/Microsoft/Cognitive-Speech-STT-JavaScript/blob/master/LICENSE.md).
