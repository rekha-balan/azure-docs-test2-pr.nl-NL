---
title: Project URL Preview endpoint - Microsoft Cognitive Services | Microsoft Docs
description: Summary of the URL Preview endpoint.
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.technology: project-url-preview
ms.topic: article
ms.date: 03/29/2018
ms.author: rosh, v-gedod
ms.openlocfilehash: ddd53aa49db01d7a6db397eb285d0854edc59388
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967231"
---
# <a name="project-url-preview-endpoint"></a>Project URL Preview endpoint

The URL Preview API includes one endpoint.

## <a name="endpoint"></a>Endpoint
To get a URL Preview, send a request to the following endpoint. Use the headers and URL parameters for other specifications.

GET:
````
https://api.labs.cognitive.microsoft.com/urlpreview/v7.0/search?q=https://swiftkey.com

````

### <a name="query-parameters"></a>Query parameters
|Name|Value|Type|Required|  
|----------|-----------|----------|--------------|  
|q|URL to preview|String |Yes|
|safeSearch|Illegal adult content, or pirated content, is blocked with error code 400, and the *isFamilyFriendly* flag is not returned. <p>For legal adult content, below is the behavior. Status code returns 200, and the *isFamilyFriendly* flag is set to false.<ul><li>safeSearch=strict: Title, description, URL and image will not be returned.</li><li>safeSearch=moderate; Get title, URL and description but not the descriptive image.</li><li>safeSearch=off; Get all the response objects/elements – title, URL, description, and image.</li></ul> |String|Not required. </br> Defaults to safeSearch=strict.| 

## <a name="response-object"></a>Response object

The response includes HTTP headers and WebPage object with attributes as shown in the following example: `name`, `url`, `description`, `isFamilyFriendly`, and `primaryImageOfPage`.

````
BingAPIs-TraceId: 15AFE52A97AA422F960433A94803F6CE
BingAPIs-SessionId: 40587764F42142D3A8BA99F66B2B3BB6
X-MSEdge-ClientID: 0389E3EDED106B5E1424E82FEC436A56
BingAPIs-Market: en-US
X-MSEdge-Ref: Ref A: 15AFE52A97AA422F960433A94803F6CE Ref B: PAOEDGE0418 Ref C: 2018-03-30T16:36:27Z
{
  "_type": "WebPage",
  "name": "SwiftKey - Smart prediction technology for easier mobile ...",
  "url": "https://swiftkey.com/",
   "description": "Discover the best Android and iPhone and iPad apps for faster, easier typing with emoji, colorful themes and more - download SwiftKey Keyboard free today.",
  "isFamilyFriendly": true,
  "primaryImageOfPage": {
    "contentUrl": "https://swiftkey.com/images/og/default.jpg"
  }
}

````

## <a name="next-steps"></a>Next steps
- [C# quickstart](csharp.md)
- [Java quickstart](java-quickstart.md)
- [JavaScript quickstart](javascript.md)
- [Node quickstart](node-quickstart.md)
- [Python quickstart](python-quickstart.md)
