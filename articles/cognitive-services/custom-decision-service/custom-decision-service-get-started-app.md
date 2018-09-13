---
title: Call API from an app - Azure Cognitive Services | Microsoft Docs
description: How to get started with Azure Custom Decision Service if you call the APIs from a smartphone app.
services: cognitive-services
author: slivkins
manager: slivkins
ms.service: cognitive-services
ms.topic: article
ms.date: 05/10/2018
ms.author: slivkins
ms.reviewer: marcozo, alekh
ms.openlocfilehash: 2d02b0deaaa701dd0b4818638827c04e2c946558
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856974"
---
# <a name="call-api-from-an-app"></a><span data-ttu-id="867fe-103">Call API from an app</span><span class="sxs-lookup"><span data-stu-id="867fe-103">Call API from an app</span></span>

<span data-ttu-id="867fe-104">Make calls to the Azure Custom Decision Service APIs from a smartphone app.</span><span class="sxs-lookup"><span data-stu-id="867fe-104">Make calls to the Azure Custom Decision Service APIs from a smartphone app.</span></span> <span data-ttu-id="867fe-105">This article explains how to get started with some basic options.</span><span class="sxs-lookup"><span data-stu-id="867fe-105">This article explains how to get started with some basic options.</span></span>

<span data-ttu-id="867fe-106">Be sure to [Register your application](custom-decision-service-get-started-register.md), first.</span><span class="sxs-lookup"><span data-stu-id="867fe-106">Be sure to [Register your application](custom-decision-service-get-started-register.md), first.</span></span>

<span data-ttu-id="867fe-107">There are two API calls you make from your smartphone app to Custom Decision Service: a call to the Ranking API to obtain a ranked list of your content and a call to the Reward API to report a reward.</span><span class="sxs-lookup"><span data-stu-id="867fe-107">There are two API calls you make from your smartphone app to Custom Decision Service: a call to the Ranking API to obtain a ranked list of your content and a call to the Reward API to report a reward.</span></span> <span data-ttu-id="867fe-108">Here are the sample calls in [cURL](https://en.wikipedia.org/wiki/CURL).</span><span class="sxs-lookup"><span data-stu-id="867fe-108">Here are the sample calls in [cURL](https://en.wikipedia.org/wiki/CURL).</span></span>

<span data-ttu-id="867fe-109">For more information, see the reference [API](custom-decision-service-api-reference.md).</span><span class="sxs-lookup"><span data-stu-id="867fe-109">For more information, see the reference [API](custom-decision-service-api-reference.md).</span></span>

<span data-ttu-id="867fe-110">Start with the call to the Ranking API.</span><span class="sxs-lookup"><span data-stu-id="867fe-110">Start with the call to the Ranking API.</span></span> <span data-ttu-id="867fe-111">Create the file `<request.json>`, which has the action set ID.</span><span class="sxs-lookup"><span data-stu-id="867fe-111">Create the file `<request.json>`, which has the action set ID.</span></span> <span data-ttu-id="867fe-112">This ID is the name of the corresponding RSS or Atom feed that you entered on the portal:</span><span class="sxs-lookup"><span data-stu-id="867fe-112">This ID is the name of the corresponding RSS or Atom feed that you entered on the portal:</span></span>

```json
{"decisions":
     [{ "actionSets":[{"id":{"id":"<actionSetId>"}}] }]}
```

<span data-ttu-id="867fe-113">Many action sets can be specified as follows:</span><span class="sxs-lookup"><span data-stu-id="867fe-113">Many action sets can be specified as follows:</span></span>

```json
{"decisions":
    [{ "actionSets":[{"id":{"id":"<actionSetId1>"}},
                     {"id":{"id":"<actionSetId2>"}}] }]}
```

<span data-ttu-id="867fe-114">This JSON file is then sent as part of the ranking request:</span><span class="sxs-lookup"><span data-stu-id="867fe-114">This JSON file is then sent as part of the ranking request:</span></span>

```shell
curl -d @<request.json> -X POST https://ds.microsoft.com/api/v2/<appId>/rank --header "Content-Type: application/json"
```

<span data-ttu-id="867fe-115">Here, `<appId>` is the name of your application registered on the portal.</span><span class="sxs-lookup"><span data-stu-id="867fe-115">Here, `<appId>` is the name of your application registered on the portal.</span></span> <span data-ttu-id="867fe-116">You should receive an ordered set of content items, which you can render in your application.</span><span class="sxs-lookup"><span data-stu-id="867fe-116">You should receive an ordered set of content items, which you can render in your application.</span></span> <span data-ttu-id="867fe-117">A sample return looks like:</span><span class="sxs-lookup"><span data-stu-id="867fe-117">A sample return looks like:</span></span>

```json
[{ "ranking":[{"id":"actionId3"}, {"id":"actionId1"}, {"id":"actionId2"}],
   "eventId":"<opaque event string>",
   "appId":"<your app id>",
   "rewardAction":"actionId3",
   "actionSets":[{"id":"<actionSetId1>","lastRefresh":"2017-04-29T22:34:25.3401438Z"},
                 {"id":"<actionSetId2>","lastRefresh":"2017-04-30T22:34:25.3401438Z"}]}]
```

<span data-ttu-id="867fe-118">The first part of the return has a list of ordered actions, specified by their action IDs.</span><span class="sxs-lookup"><span data-stu-id="867fe-118">The first part of the return has a list of ordered actions, specified by their action IDs.</span></span> <span data-ttu-id="867fe-119">For an article, the action ID is a URL.</span><span class="sxs-lookup"><span data-stu-id="867fe-119">For an article, the action ID is a URL.</span></span> <span data-ttu-id="867fe-120">The overall request also has a unique `<eventId>`, created by the system.</span><span class="sxs-lookup"><span data-stu-id="867fe-120">The overall request also has a unique `<eventId>`, created by the system.</span></span>

<span data-ttu-id="867fe-121">Later, you can specify if you observed a click on the first content item from this event, which is `<actionId3>`.</span><span class="sxs-lookup"><span data-stu-id="867fe-121">Later, you can specify if you observed a click on the first content item from this event, which is `<actionId3>`.</span></span> <span data-ttu-id="867fe-122">You can then report a reward on this `<eventId>` to Custom Decision Service via the Reward API, with another request such as:</span><span class="sxs-lookup"><span data-stu-id="867fe-122">You can then report a reward on this `<eventId>` to Custom Decision Service via the Reward API, with another request such as:</span></span>

```shell
curl -v https://ds.microsoft.com/api/v2/<appId>/reward/<eventId> -X POST
```

<span data-ttu-id="867fe-123">Finally, you need to provide the Action Set API, which returns the list of articles (actions) to be considered by Custom Decision Service.</span><span class="sxs-lookup"><span data-stu-id="867fe-123">Finally, you need to provide the Action Set API, which returns the list of articles (actions) to be considered by Custom Decision Service.</span></span> <span data-ttu-id="867fe-124">Implement this API as an RSS feed, as shown here:</span><span class="sxs-lookup"><span data-stu-id="867fe-124">Implement this API as an RSS feed, as shown here:</span></span>

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

<span data-ttu-id="867fe-125">Here, each top-level `<item>` element describes an article.</span><span class="sxs-lookup"><span data-stu-id="867fe-125">Here, each top-level `<item>` element describes an article.</span></span> <span data-ttu-id="867fe-126">The `<link>` is mandatory and is used as an action ID by Custom Decision Service.</span><span class="sxs-lookup"><span data-stu-id="867fe-126">The `<link>` is mandatory and is used as an action ID by Custom Decision Service.</span></span> <span data-ttu-id="867fe-127">Specify `<date>` (in a standard RSS format) if you've more than 15 articles.</span><span class="sxs-lookup"><span data-stu-id="867fe-127">Specify `<date>` (in a standard RSS format) if you've more than 15 articles.</span></span> <span data-ttu-id="867fe-128">The 15 most recent articles are used.</span><span class="sxs-lookup"><span data-stu-id="867fe-128">The 15 most recent articles are used.</span></span> <span data-ttu-id="867fe-129">The `<title>` is optional and is used to create text-related features for the article.</span><span class="sxs-lookup"><span data-stu-id="867fe-129">The `<title>` is optional and is used to create text-related features for the article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="867fe-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="867fe-130">Next steps</span></span>

* <span data-ttu-id="867fe-131">Work through a [tutorial](custom-decision-service-tutorial-news.md) for a more in-depth example.</span><span class="sxs-lookup"><span data-stu-id="867fe-131">Work through a [tutorial](custom-decision-service-tutorial-news.md) for a more in-depth example.</span></span>
* <span data-ttu-id="867fe-132">Consult the reference [API](custom-decision-service-api-reference.md) to learn more about the provided functionality.</span><span class="sxs-lookup"><span data-stu-id="867fe-132">Consult the reference [API](custom-decision-service-api-reference.md) to learn more about the provided functionality.</span></span>