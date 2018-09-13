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
# <a name="call-api-from-a-browser"></a><span data-ttu-id="26431-103">Call API from a browser</span><span class="sxs-lookup"><span data-stu-id="26431-103">Call API from a browser</span></span>

<span data-ttu-id="26431-104">This article helps you make calls to the Azure Custom Decision Service APIs directly from a browser.</span><span class="sxs-lookup"><span data-stu-id="26431-104">This article helps you make calls to the Azure Custom Decision Service APIs directly from a browser.</span></span>

<span data-ttu-id="26431-105">Be sure to [Register your application](custom-decision-service-get-started-register.md), first.</span><span class="sxs-lookup"><span data-stu-id="26431-105">Be sure to [Register your application](custom-decision-service-get-started-register.md), first.</span></span>

<span data-ttu-id="26431-106">Let's get started.</span><span class="sxs-lookup"><span data-stu-id="26431-106">Let's get started.</span></span> <span data-ttu-id="26431-107">Your application is modeled as having a front page, which links to several article pages.</span><span class="sxs-lookup"><span data-stu-id="26431-107">Your application is modeled as having a front page, which links to several article pages.</span></span> <span data-ttu-id="26431-108">The front page uses Custom Decision Service to specify the ordering of its article pages.</span><span class="sxs-lookup"><span data-stu-id="26431-108">The front page uses Custom Decision Service to specify the ordering of its article pages.</span></span> <span data-ttu-id="26431-109">Insert the following code into the HTML head of the front page:</span><span class="sxs-lookup"><span data-stu-id="26431-109">Insert the following code into the HTML head of the front page:</span></span>

```html
// Define the "callback function" to render UI
<script> function callback(data) { … } </script>

// call Ranking API, after callback() is defined
<script src="https://ds.microsoft.com/api/v2/<appId>/rank/<actionSetId>" async></script>
```

<span data-ttu-id="26431-110">The `data` argument contains the ranking of URLs to be rendered.</span><span class="sxs-lookup"><span data-stu-id="26431-110">The `data` argument contains the ranking of URLs to be rendered.</span></span> <span data-ttu-id="26431-111">For more information, see the reference [API](custom-decision-service-api-reference.md).</span><span class="sxs-lookup"><span data-stu-id="26431-111">For more information, see the reference [API](custom-decision-service-api-reference.md).</span></span>

<span data-ttu-id="26431-112">To handle a user click on the top article, call the following code on the front page:</span><span class="sxs-lookup"><span data-stu-id="26431-112">To handle a user click on the top article, call the following code on the front page:</span></span>

```javascript
// call Reward API to report a click
$.ajax({
    type: "POST",
    url: '//ds.microsoft.com/api/v2/<appId>/reward/' + data.eventId,
    contentType: "application/json" })
```

<span data-ttu-id="26431-113">Here, `data` is the argument to the `callback()` function.</span><span class="sxs-lookup"><span data-stu-id="26431-113">Here, `data` is the argument to the `callback()` function.</span></span> <span data-ttu-id="26431-114">An implementation example can be found in this [tutorial](custom-decision-service-tutorial-news.md#use-the-apis).</span><span class="sxs-lookup"><span data-stu-id="26431-114">An implementation example can be found in this [tutorial](custom-decision-service-tutorial-news.md#use-the-apis).</span></span>

<span data-ttu-id="26431-115">Finally, you need to provide the Action Set API, which returns the list of articles (actions) to be considered by Custom Decision Service.</span><span class="sxs-lookup"><span data-stu-id="26431-115">Finally, you need to provide the Action Set API, which returns the list of articles (actions) to be considered by Custom Decision Service.</span></span> <span data-ttu-id="26431-116">Implement this API as an RSS feed, as shown here:</span><span class="sxs-lookup"><span data-stu-id="26431-116">Implement this API as an RSS feed, as shown here:</span></span>

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

<span data-ttu-id="26431-117">Here, each top-level `<item>` element describes an article.</span><span class="sxs-lookup"><span data-stu-id="26431-117">Here, each top-level `<item>` element describes an article.</span></span> <span data-ttu-id="26431-118">The `<link>` is mandatory and is used as an action ID by Custom Decision Service.</span><span class="sxs-lookup"><span data-stu-id="26431-118">The `<link>` is mandatory and is used as an action ID by Custom Decision Service.</span></span> <span data-ttu-id="26431-119">Specify `<date>` (in a standard RSS format) if you have more than 15 articles.</span><span class="sxs-lookup"><span data-stu-id="26431-119">Specify `<date>` (in a standard RSS format) if you have more than 15 articles.</span></span> <span data-ttu-id="26431-120">The 15 most recent articles are used.</span><span class="sxs-lookup"><span data-stu-id="26431-120">The 15 most recent articles are used.</span></span> <span data-ttu-id="26431-121">The `<title>` is optional and is used to create text-related features for the article.</span><span class="sxs-lookup"><span data-stu-id="26431-121">The `<title>` is optional and is used to create text-related features for the article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26431-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="26431-122">Next steps</span></span>

* <span data-ttu-id="26431-123">Work through a [tutorial](custom-decision-service-tutorial-news.md) for a more in-depth example.</span><span class="sxs-lookup"><span data-stu-id="26431-123">Work through a [tutorial](custom-decision-service-tutorial-news.md) for a more in-depth example.</span></span>
* <span data-ttu-id="26431-124">Consult the reference [API](custom-decision-service-api-reference.md) to learn more about the provided functionality.</span><span class="sxs-lookup"><span data-stu-id="26431-124">Consult the reference [API](custom-decision-service-api-reference.md) to learn more about the provided functionality.</span></span>