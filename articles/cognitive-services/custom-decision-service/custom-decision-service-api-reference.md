---
title: API - Azure Cognitive Services | Microsoft Docs
description: A complete and user-friendly API guide for Azure Custom Decision Service, a cloud-based API for contextual decision-making that sharpens with experience.
services: cognitive-services
author: slivkins
manager: slivkins
ms.service: cognitive-services
ms.topic: article
ms.date: 05/11/2018
ms.author: slivkins
ms.reviewer: marcozo, alekh
ms.openlocfilehash: 403b17e33394016a07a7b33ba1bcbfe6afdcc05b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968874"
---
# <a name="api"></a><span data-ttu-id="7ab96-103">API</span><span class="sxs-lookup"><span data-stu-id="7ab96-103">API</span></span>

<span data-ttu-id="7ab96-104">Azure Custom Decision Service provides two APIs that are called for each decision: the [Ranking API](#ranking-api) to input the ranking of actions and the [Reward API](#reward-api) to output the reward.</span><span class="sxs-lookup"><span data-stu-id="7ab96-104">Azure Custom Decision Service provides two APIs that are called for each decision: the [Ranking API](#ranking-api) to input the ranking of actions and the [Reward API](#reward-api) to output the reward.</span></span> <span data-ttu-id="7ab96-105">In addition, you provide an [Action Set API](#action-set-api-customer-provided) to specify the actions to Azure Custom Decision Service.</span><span class="sxs-lookup"><span data-stu-id="7ab96-105">In addition, you provide an [Action Set API](#action-set-api-customer-provided) to specify the actions to Azure Custom Decision Service.</span></span> <span data-ttu-id="7ab96-106">This article covers these three APIs.</span><span class="sxs-lookup"><span data-stu-id="7ab96-106">This article covers these three APIs.</span></span> <span data-ttu-id="7ab96-107">A typical scenario is used below to show when Custom Decision Service optimizes the ranking of articles.</span><span class="sxs-lookup"><span data-stu-id="7ab96-107">A typical scenario is used below to show when Custom Decision Service optimizes the ranking of articles.</span></span>

## <a name="ranking-api"></a><span data-ttu-id="7ab96-108">Ranking API</span><span class="sxs-lookup"><span data-stu-id="7ab96-108">Ranking API</span></span>

<span data-ttu-id="7ab96-109">The ranking API uses a standard [JSONP](https://en.wikipedia.org/wiki/JSONP)-style communication pattern to optimize latency and bypass the [same-origin policy](https://en.wikipedia.org/wiki/Same-origin_policy).</span><span class="sxs-lookup"><span data-stu-id="7ab96-109">The ranking API uses a standard [JSONP](https://en.wikipedia.org/wiki/JSONP)-style communication pattern to optimize latency and bypass the [same-origin policy](https://en.wikipedia.org/wiki/Same-origin_policy).</span></span> <span data-ttu-id="7ab96-110">The latter prohibits JavaScript from fetching data from outside the page's origin.</span><span class="sxs-lookup"><span data-stu-id="7ab96-110">The latter prohibits JavaScript from fetching data from outside the page's origin.</span></span>

<span data-ttu-id="7ab96-111">Insert this snippet into the HTML head of your front page (where a personalized list of articles are displayed):</span><span class="sxs-lookup"><span data-stu-id="7ab96-111">Insert this snippet into the HTML head of your front page (where a personalized list of articles are displayed):</span></span>

```html
// define the "callback function" to render UI
<script> function callback(data) { … } </script>
// "data" provides the ranking of URLs, see example below.

// call to Ranking API
<script src="https://ds.microsoft.com/api/v2/<appId>/rank/<actionSetId>?<parameters>" async></script>
// action set id is the name of the corresponding RSS/Atom feed.

// same call with multiple action sets:
// <script src="https://ds.microsoft.com/api/v2/<appId>/rank/<A1>/<A2>/.../<An>?<parameters>" async></script>
```

> [!IMPORTANT]
> <span data-ttu-id="7ab96-112">The callback function must be defined before the call to the Ranking API.</span><span class="sxs-lookup"><span data-stu-id="7ab96-112">The callback function must be defined before the call to the Ranking API.</span></span>

> [!TIP]
> <span data-ttu-id="7ab96-113">To improve latency, the Ranking API is exposed via HTTP rather than HTTPS, as in `http://ds.microsoft.com/api/v2/<appId>/rank/*`.</span><span class="sxs-lookup"><span data-stu-id="7ab96-113">To improve latency, the Ranking API is exposed via HTTP rather than HTTPS, as in `http://ds.microsoft.com/api/v2/<appId>/rank/*`.</span></span>
> <span data-ttu-id="7ab96-114">However, an HTTPS endpoint must be used if the front page is served through HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7ab96-114">However, an HTTPS endpoint must be used if the front page is served through HTTPS.</span></span>

<span data-ttu-id="7ab96-115">When parameters are not used, the HTTP response from the Ranking API is a JSONP-formatted string:</span><span class="sxs-lookup"><span data-stu-id="7ab96-115">When parameters are not used, the HTTP response from the Ranking API is a JSONP-formatted string:</span></span>

```json
callback({
   "ranking":[{"id":"url1"}, {"id":"url2"}, {"id":"url3"}],
   "eventId":"<opaque event string>",
   "appId":"<your app id>",
   "actionSets":[{"id":"<A1>","lastRefresh":"2017-04-29T22:34:25.3401438Z"},
                 {"id":"<A2>","lastRefresh":"2017-04-30T22:34:25.3401438Z"}]});
```

<span data-ttu-id="7ab96-116">The browser then executes this string as a call to the `callback()` function.</span><span class="sxs-lookup"><span data-stu-id="7ab96-116">The browser then executes this string as a call to the `callback()` function.</span></span>

<span data-ttu-id="7ab96-117">The parameter to the callback function in the preceding example has the following schema:</span><span class="sxs-lookup"><span data-stu-id="7ab96-117">The parameter to the callback function in the preceding example has the following schema:</span></span>

- <span data-ttu-id="7ab96-118">`ranking` provides the ranking of URLs to be displayed.</span><span class="sxs-lookup"><span data-stu-id="7ab96-118">`ranking` provides the ranking of URLs to be displayed.</span></span>
- <span data-ttu-id="7ab96-119">`eventId` is used internally by Custom Decision Service to match this ranking with the corresponding clicks.</span><span class="sxs-lookup"><span data-stu-id="7ab96-119">`eventId` is used internally by Custom Decision Service to match this ranking with the corresponding clicks.</span></span>
- <span data-ttu-id="7ab96-120">`appId` allows the callback function to distinguish between multiple applications of Custom Decision Service running on the same webpage.</span><span class="sxs-lookup"><span data-stu-id="7ab96-120">`appId` allows the callback function to distinguish between multiple applications of Custom Decision Service running on the same webpage.</span></span>
- <span data-ttu-id="7ab96-121">`actionSets` lists each action set used in the Ranking API call, along with the UTC timestamp of the last successful refresh.</span><span class="sxs-lookup"><span data-stu-id="7ab96-121">`actionSets` lists each action set used in the Ranking API call, along with the UTC timestamp of the last successful refresh.</span></span> <span data-ttu-id="7ab96-122">Custom Decision Service periodically refreshes the action set feeds.</span><span class="sxs-lookup"><span data-stu-id="7ab96-122">Custom Decision Service periodically refreshes the action set feeds.</span></span> <span data-ttu-id="7ab96-123">For example, if some of the action sets are not current, the callback function might need to fall back to their default ranking.</span><span class="sxs-lookup"><span data-stu-id="7ab96-123">For example, if some of the action sets are not current, the callback function might need to fall back to their default ranking.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ab96-124">The specified action sets are processed, and possibly pruned, to form the default ranking of articles.</span><span class="sxs-lookup"><span data-stu-id="7ab96-124">The specified action sets are processed, and possibly pruned, to form the default ranking of articles.</span></span> <span data-ttu-id="7ab96-125">The default ranking then gets reordered and returned in the HTTP response.</span><span class="sxs-lookup"><span data-stu-id="7ab96-125">The default ranking then gets reordered and returned in the HTTP response.</span></span> <span data-ttu-id="7ab96-126">The default ranking is defined here:</span><span class="sxs-lookup"><span data-stu-id="7ab96-126">The default ranking is defined here:</span></span>
>
> - <span data-ttu-id="7ab96-127">Within each action set, the articles are pruned to the 15 most recent articles (if more than 15 are returned).</span><span class="sxs-lookup"><span data-stu-id="7ab96-127">Within each action set, the articles are pruned to the 15 most recent articles (if more than 15 are returned).</span></span>
> - <span data-ttu-id="7ab96-128">When multiple action sets are specified, they are merged in the same order as in the API call.</span><span class="sxs-lookup"><span data-stu-id="7ab96-128">When multiple action sets are specified, they are merged in the same order as in the API call.</span></span> <span data-ttu-id="7ab96-129">The original ordering of the articles is preserved within each action set.</span><span class="sxs-lookup"><span data-stu-id="7ab96-129">The original ordering of the articles is preserved within each action set.</span></span> <span data-ttu-id="7ab96-130">Duplicates are removed in favor of the earlier copies.</span><span class="sxs-lookup"><span data-stu-id="7ab96-130">Duplicates are removed in favor of the earlier copies.</span></span>
> - <span data-ttu-id="7ab96-131">The first `n` articles are kept from the merged list of articles, where `n=20` by default.</span><span class="sxs-lookup"><span data-stu-id="7ab96-131">The first `n` articles are kept from the merged list of articles, where `n=20` by default.</span></span>

### <a name="ranking-api-with-parameters"></a><span data-ttu-id="7ab96-132">Ranking API with parameters</span><span class="sxs-lookup"><span data-stu-id="7ab96-132">Ranking API with parameters</span></span>

<span data-ttu-id="7ab96-133">The Ranking API allows these parameters:</span><span class="sxs-lookup"><span data-stu-id="7ab96-133">The Ranking API allows these parameters:</span></span>

- <span data-ttu-id="7ab96-134">`details=1` and `details=2` inserts additional details about each article listed in `ranking`.</span><span class="sxs-lookup"><span data-stu-id="7ab96-134">`details=1` and `details=2` inserts additional details about each article listed in `ranking`.</span></span>
- <span data-ttu-id="7ab96-135">`limit=<n>` specifies the maximal number of articles in the default ranking.</span><span class="sxs-lookup"><span data-stu-id="7ab96-135">`limit=<n>` specifies the maximal number of articles in the default ranking.</span></span> <span data-ttu-id="7ab96-136">`n` must be between `2` and `30` (or else it is truncated to `2` or `30`, respectively).</span><span class="sxs-lookup"><span data-stu-id="7ab96-136">`n` must be between `2` and `30` (or else it is truncated to `2` or `30`, respectively).</span></span>
- <span data-ttu-id="7ab96-137">`dnt=1` disables user cookies.</span><span class="sxs-lookup"><span data-stu-id="7ab96-137">`dnt=1` disables user cookies.</span></span>

<span data-ttu-id="7ab96-138">Parameters can be combined in standard, query string syntax, for example `details=2&dnt=1`.</span><span class="sxs-lookup"><span data-stu-id="7ab96-138">Parameters can be combined in standard, query string syntax, for example `details=2&dnt=1`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ab96-139">The default setting in Europe should be `dnt=1` until the customer agrees to the cookie banner.</span><span class="sxs-lookup"><span data-stu-id="7ab96-139">The default setting in Europe should be `dnt=1` until the customer agrees to the cookie banner.</span></span> <span data-ttu-id="7ab96-140">It should also be the default setting for websites that target minors.</span><span class="sxs-lookup"><span data-stu-id="7ab96-140">It should also be the default setting for websites that target minors.</span></span> <span data-ttu-id="7ab96-141">For more information, see the [terms of use](https://www.microsoft.com/cognitive-services/en-us/legal/CognitiveServicesTerms20160804).</span><span class="sxs-lookup"><span data-stu-id="7ab96-141">For more information, see the [terms of use](https://www.microsoft.com/cognitive-services/en-us/legal/CognitiveServicesTerms20160804).</span></span>

<span data-ttu-id="7ab96-142">The `details=1` element inserts each article's `guid`, if it's served by the Action Set API.</span><span class="sxs-lookup"><span data-stu-id="7ab96-142">The `details=1` element inserts each article's `guid`, if it's served by the Action Set API.</span></span> <span data-ttu-id="7ab96-143">The HTTP response:</span><span class="sxs-lookup"><span data-stu-id="7ab96-143">The HTTP response:</span></span>

```json
callback({
   "ranking":[{"id":"url1","details":[{"guid":"123"}]},
              {"id":"url2","details":[{"guid":"456"}]},
              {"id":"url3","details":[{"guid":"789"}]}],
   "eventId":"<opaque event string>",
   "appId":"<your app id>",
   "actionSets":[{"id":"<A1>","lastRefresh":"timeStamp1"},
                 {"id":"<A2>","lastRefresh":"timeStamp2"}]});
```

<span data-ttu-id="7ab96-144">The `details=2` element adds more details that Custom Decision Service might extract from articles' SEO metatags [featurization code](https://github.com/Microsoft/mwt-ds/tree/master/Crawl):</span><span class="sxs-lookup"><span data-stu-id="7ab96-144">The `details=2` element adds more details that Custom Decision Service might extract from articles' SEO metatags [featurization code](https://github.com/Microsoft/mwt-ds/tree/master/Crawl):</span></span>

- <span data-ttu-id="7ab96-145">`title` from `<meta property="og:title" content="..." />` or `<meta property="twitter:title" content="..." />` or `<title>...</title>`</span><span class="sxs-lookup"><span data-stu-id="7ab96-145">`title` from `<meta property="og:title" content="..." />` or `<meta property="twitter:title" content="..." />` or `<title>...</title>`</span></span>
- <span data-ttu-id="7ab96-146">`description` from `<meta property="og:description" ... />` or `<meta property="twitter:description" content="..." />` or `<meta property="description" content="..." />`</span><span class="sxs-lookup"><span data-stu-id="7ab96-146">`description` from `<meta property="og:description" ... />` or `<meta property="twitter:description" content="..." />` or `<meta property="description" content="..." />`</span></span>
- <span data-ttu-id="7ab96-147">`image` from `<meta property="og:image" content="..." />`</span><span class="sxs-lookup"><span data-stu-id="7ab96-147">`image` from `<meta property="og:image" content="..." />`</span></span>
- <span data-ttu-id="7ab96-148">`ds_id` from `<meta name=”microsoft:ds_id” content="..." />`</span><span class="sxs-lookup"><span data-stu-id="7ab96-148">`ds_id` from `<meta name=”microsoft:ds_id” content="..." />`</span></span>

<span data-ttu-id="7ab96-149">The HTTP response:</span><span class="sxs-lookup"><span data-stu-id="7ab96-149">The HTTP response:</span></span>

```json
callback({
   "ranking":[{"id":"url1","details":<details>},
              {"id":"url2","details":<details>},
              {"id":"url3","details":<details>}],
   "eventId":"<opaque event string>",
   "appId":"<your app id>",
   "actionSets":[{"id":"<A1>","lastRefresh":"timeStamp1"},
                 {"id":"<A2>","lastRefresh":"timeStamp2"}]});
```

<span data-ttu-id="7ab96-150">The `<details>` element:</span><span class="sxs-lookup"><span data-stu-id="7ab96-150">The `<details>` element:</span></span>

```json
[{"guid":"123"}, {"description":"some text", "ds_id":"234", "image":"ImageUrl1", "title":"some text"}]
```

## <a name="reward-api"></a><span data-ttu-id="7ab96-151">Reward API</span><span class="sxs-lookup"><span data-stu-id="7ab96-151">Reward API</span></span>

<span data-ttu-id="7ab96-152">Custom Decision Service uses clicks only on the top slot.</span><span class="sxs-lookup"><span data-stu-id="7ab96-152">Custom Decision Service uses clicks only on the top slot.</span></span> <span data-ttu-id="7ab96-153">Each click is interpreted as a reward of 1.</span><span class="sxs-lookup"><span data-stu-id="7ab96-153">Each click is interpreted as a reward of 1.</span></span> <span data-ttu-id="7ab96-154">The lack of a click is interpreted as a reward of 0.</span><span class="sxs-lookup"><span data-stu-id="7ab96-154">The lack of a click is interpreted as a reward of 0.</span></span> <span data-ttu-id="7ab96-155">Clicks are matched with the corresponding rankings by using event IDs, which are generated by the [Ranking API](#ranking-api) call.</span><span class="sxs-lookup"><span data-stu-id="7ab96-155">Clicks are matched with the corresponding rankings by using event IDs, which are generated by the [Ranking API](#ranking-api) call.</span></span> <span data-ttu-id="7ab96-156">If needed, event IDs can be passed via session cookies.</span><span class="sxs-lookup"><span data-stu-id="7ab96-156">If needed, event IDs can be passed via session cookies.</span></span>

<span data-ttu-id="7ab96-157">To handle a click on the top slot, put this code on your front page:</span><span class="sxs-lookup"><span data-stu-id="7ab96-157">To handle a click on the top slot, put this code on your front page:</span></span>

```javascript
$.ajax({
    type: "POST",
    url: '//ds.microsoft.com/api/v2/<appId>/reward/' + data.eventId,
    contentType: "application/json" })
```

<span data-ttu-id="7ab96-158">Here `data` is the argument to the `callback()` function, as described previously.</span><span class="sxs-lookup"><span data-stu-id="7ab96-158">Here `data` is the argument to the `callback()` function, as described previously.</span></span> <span data-ttu-id="7ab96-159">Using `data` in the click handling code requires some care.</span><span class="sxs-lookup"><span data-stu-id="7ab96-159">Using `data` in the click handling code requires some care.</span></span> <span data-ttu-id="7ab96-160">An example is shown in this [tutorial](custom-decision-service-tutorial-news.md#use-the-apis).</span><span class="sxs-lookup"><span data-stu-id="7ab96-160">An example is shown in this [tutorial](custom-decision-service-tutorial-news.md#use-the-apis).</span></span>

<span data-ttu-id="7ab96-161">For testing only, the Reward API can be called via [cURL](https://en.wikipedia.org/wiki/CURL):</span><span class="sxs-lookup"><span data-stu-id="7ab96-161">For testing only, the Reward API can be called via [cURL](https://en.wikipedia.org/wiki/CURL):</span></span>

```sh
curl -v https://ds.microsoft.com/api/v2/<appId>/reward/<eventId> -X POST -d 1 -H "Content-Type: application/json"
```

<span data-ttu-id="7ab96-162">The expected effect is an HTTP response of 200 (OK).</span><span class="sxs-lookup"><span data-stu-id="7ab96-162">The expected effect is an HTTP response of 200 (OK).</span></span> <span data-ttu-id="7ab96-163">You can see the reward of 1 for this event in the log (if an Azure storage account key was supplied on the portal).</span><span class="sxs-lookup"><span data-stu-id="7ab96-163">You can see the reward of 1 for this event in the log (if an Azure storage account key was supplied on the portal).</span></span>

## <a name="action-set-api-customer-provided"></a><span data-ttu-id="7ab96-164">Action Set API (customer provided)</span><span class="sxs-lookup"><span data-stu-id="7ab96-164">Action Set API (customer provided)</span></span>

<span data-ttu-id="7ab96-165">On a high level, the Action Set API returns a list of articles (actions).</span><span class="sxs-lookup"><span data-stu-id="7ab96-165">On a high level, the Action Set API returns a list of articles (actions).</span></span> <span data-ttu-id="7ab96-166">Each article is specified by its URL and (optionally) the article title and the publication date.</span><span class="sxs-lookup"><span data-stu-id="7ab96-166">Each article is specified by its URL and (optionally) the article title and the publication date.</span></span> <span data-ttu-id="7ab96-167">You can specify several action sets on the portal.</span><span class="sxs-lookup"><span data-stu-id="7ab96-167">You can specify several action sets on the portal.</span></span> <span data-ttu-id="7ab96-168">A different Action Set API should be used for each action set, as a distinct URL.</span><span class="sxs-lookup"><span data-stu-id="7ab96-168">A different Action Set API should be used for each action set, as a distinct URL.</span></span>

<span data-ttu-id="7ab96-169">Each Action Set API can be implemented in two ways: as an RSS feed or as an Atom feed.</span><span class="sxs-lookup"><span data-stu-id="7ab96-169">Each Action Set API can be implemented in two ways: as an RSS feed or as an Atom feed.</span></span> <span data-ttu-id="7ab96-170">Either one should conform to the standard and return a correct XML.</span><span class="sxs-lookup"><span data-stu-id="7ab96-170">Either one should conform to the standard and return a correct XML.</span></span> <span data-ttu-id="7ab96-171">For RSS, here's an example:</span><span class="sxs-lookup"><span data-stu-id="7ab96-171">For RSS, here's an example:</span></span>

```xml
<rss version="2.0">
<channel>
   <item>
      <title><![CDATA[title (possibly with url) ]]></title>
      <link>url</link>
      <guid>guid (could be a your internal database id)</guid>
      <pubDate>date</pubDate>
    </item>
   <item>
       ....
   </item>
</channel>
</rss>
```

<span data-ttu-id="7ab96-172">Each top-level `<item>` element describes an action:</span><span class="sxs-lookup"><span data-stu-id="7ab96-172">Each top-level `<item>` element describes an action:</span></span>

- <span data-ttu-id="7ab96-173">`<link>` is mandatory and is used as an action ID.</span><span class="sxs-lookup"><span data-stu-id="7ab96-173">`<link>` is mandatory and is used as an action ID.</span></span>
- <span data-ttu-id="7ab96-174">`<date>` is ignored if it's less than or equal to 15 items; otherwise, it's mandatory.</span><span class="sxs-lookup"><span data-stu-id="7ab96-174">`<date>` is ignored if it's less than or equal to 15 items; otherwise, it's mandatory.</span></span>
  - <span data-ttu-id="7ab96-175">If there are more than 15 items, the 15 most recent ones are used.</span><span class="sxs-lookup"><span data-stu-id="7ab96-175">If there are more than 15 items, the 15 most recent ones are used.</span></span>
  - <span data-ttu-id="7ab96-176">It must be in the standard format for RSS or Atom, respectively:</span><span class="sxs-lookup"><span data-stu-id="7ab96-176">It must be in the standard format for RSS or Atom, respectively:</span></span>
    - <span data-ttu-id="7ab96-177">[RFC 822](https://tools.ietf.org/html/rfc822) for RSS: for example, `"Fri, 28 Apr 2017 18:02:06 GMT"`</span><span class="sxs-lookup"><span data-stu-id="7ab96-177">[RFC 822](https://tools.ietf.org/html/rfc822) for RSS: for example, `"Fri, 28 Apr 2017 18:02:06 GMT"`</span></span>
    - <span data-ttu-id="7ab96-178">[RFC 3339](https://tools.ietf.org/html/rfc3339) for Atom: for example, `"2016-12-19T16:39:57-08:00"`</span><span class="sxs-lookup"><span data-stu-id="7ab96-178">[RFC 3339](https://tools.ietf.org/html/rfc3339) for Atom: for example, `"2016-12-19T16:39:57-08:00"`</span></span>
- <span data-ttu-id="7ab96-179">`<title>` is optional and is used to generate features that describe the article.</span><span class="sxs-lookup"><span data-stu-id="7ab96-179">`<title>` is optional and is used to generate features that describe the article.</span></span>
- <span data-ttu-id="7ab96-180">`<guid>` is optional and passed through the system to the callback function (if the `?details` parameter is specified in the Ranking API call).</span><span class="sxs-lookup"><span data-stu-id="7ab96-180">`<guid>` is optional and passed through the system to the callback function (if the `?details` parameter is specified in the Ranking API call).</span></span>

<span data-ttu-id="7ab96-181">Other elements inside an `<item>` are ignored.</span><span class="sxs-lookup"><span data-stu-id="7ab96-181">Other elements inside an `<item>` are ignored.</span></span>

<span data-ttu-id="7ab96-182">The Atom feed version uses the same XML syntax and conventions.</span><span class="sxs-lookup"><span data-stu-id="7ab96-182">The Atom feed version uses the same XML syntax and conventions.</span></span>

> [!TIP]
> <span data-ttu-id="7ab96-183">If your system uses its own article IDs, they can be passed into the callback function by using `<guid>`.</span><span class="sxs-lookup"><span data-stu-id="7ab96-183">If your system uses its own article IDs, they can be passed into the callback function by using `<guid>`.</span></span>