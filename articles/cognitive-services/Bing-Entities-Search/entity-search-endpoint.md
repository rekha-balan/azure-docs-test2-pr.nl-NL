---
title: Entity Search endpoints | Microsoft Docs
description: Summary of the Entity Search API endpoint.
services: cognitive-services
author: v-jaswel
manager: kaiq
ms.service: cognitive-services
ms.component: bing-entity-search
ms.topic: article
ms.date: 12/04/2017
ms.author: v-jaswel
ms.openlocfilehash: 3d5da30102712baf399c245cc7678eeddbce796a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871367"
---
# <a name="entity-search-endpoints"></a>Entity Search endpoints
The **Entity Search API**  includes one endpoint.

## <a name="endpoint"></a>Endpoint
To request entity search results, send a request to the following endpoint. Use the headers and URL parameters to define further specifications.

Endpoint `GET`: 
``` 
https://api.cognitive.microsoft.com/bing/v7.0/entities
```

The following URL parameters are required:
- mkt. The market where the results come from. 
- q. The entity search query.

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Bing Entity Search quickstarts](quickstarts/csharp.md)

## <a name="see-also"></a>See also 

[Bing Entity Search overview](search-the-web.md )
[API Reference](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference)
