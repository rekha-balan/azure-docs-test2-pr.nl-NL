---
title: Call API from a browser - Azure Cognitive Services | Microsoft Docs
description: How to get started with Azure Custom Decision Service to optimize a webpage by making API calls directly from a browser.
services: cognitive-services
author: slivkins
manager: slivkins
ms.service: cognitive-services
ms.topic: article
ms.date: 05/09/2018
ms.author: slivkins,marcozo,alekh
ms.openlocfilehash: 10236c9d8f70d9b90a896464b4f86a847ee904c2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866240"
---
# <a name="call-api-from-a-browser"></a>Call API from a browser

This article helps you make calls to the Azure Custom Decision Service APIs directly from a browser.

Be sure to [Register your application](custom-decision-service-get-started-register.md), first.

Let's get started. Your application is modeled as having a front page, which links to several article pages. The front page uses Custom Decision Service to specify the ordering of its article pages. Insert the following code into the HTML head of the front page:

```html
// Define the "callback function" to render UI
<script> function callback(data) { … } </script>

// call Ranking API, after callback() is defined
<script src="https://ds.microsoft.com/api/v2/<appId>/rank/<actionSetId>" async></script>
```

The `data` argument contains the ranking of URLs to be rendered. For more information, see the reference [API](custom-decision-service-api-reference.md).

To handle a user click on the top article, call the following code on the front page:

```javascript
// call Reward API to report a click
$.ajax({
    type: "POST",
    url: '//ds.microsoft.com/api/v2/<appId>/reward/' + data.eventId,
    contentType: "application/json" })
```

Here, `data` is the argument to the `callback()` function. An implementation example can be found in this [tutorial](custom-decision-service-tutorial-news.md#use-the-apis).

Finally, you need to provide the Action Set API, which returns the list of articles (actions) to be considered by Custom Decision Service. Implement this API as an RSS feed, as shown here:

```xml
<rss version="2.0">
<channel>
   <item>
      <title><![CDATA[title (possibly with url) ]]></title>
      <link>url</link>
      <pubDate>Thu, 27 Apr 2017 16:30:52 GMT</pubDate>
    </item>
   <item>
       ....
   </item>
</channel>
</rss>
```

Here, each top-level `<item>` element describes an article. The `<link>` is mandatory and is used as an action ID by Custom Decision Service. Specify `<date>` (in a standard RSS format) if you have more than 15 articles. The 15 most recent articles are used. The `<title>` is optional and is used to create text-related features for the article.

## <a name="next-steps"></a>Next steps

* Work through a [tutorial](custom-decision-service-tutorial-news.md) for a more in-depth example.
* Consult the reference [API](custom-decision-service-api-reference.md) to learn more about the provided functionality.