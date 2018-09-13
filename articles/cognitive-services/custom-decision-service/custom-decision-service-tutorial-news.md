---
title: Article personalization - Azure Cognitive Services | Microsoft Docs
description: A tutorial for article personalization with Azure Custom Decision Service, a cloud-based API for contextual decision-making.
services: cognitive-services
author: slivkins
manager: slivkins
ms.service: cognitive-services
ms.topic: article
ms.date: 05/08/2018
ms.author: slivkins;marcozo;alekh;marossi
ms.openlocfilehash: 35d0567f81a23d4726461059eb6fd31e04228697
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867741"
---
# <a name="article-personalization"></a><span data-ttu-id="1bc1e-103">Article personalization</span><span class="sxs-lookup"><span data-stu-id="1bc1e-103">Article personalization</span></span>

<span data-ttu-id="1bc1e-104">This tutorial focuses on personalizing the selection of articles on the front page of a website.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-104">This tutorial focuses on personalizing the selection of articles on the front page of a website.</span></span> <span data-ttu-id="1bc1e-105">The Custom Decision Service affects *multiple* lists of articles on the front page, for instance.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-105">The Custom Decision Service affects *multiple* lists of articles on the front page, for instance.</span></span> <span data-ttu-id="1bc1e-106">Perhaps the page is a news website that covers only politics and sports.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-106">Perhaps the page is a news website that covers only politics and sports.</span></span> <span data-ttu-id="1bc1e-107">It would show three ranked lists of articles: politics, sports, and recent.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-107">It would show three ranked lists of articles: politics, sports, and recent.</span></span>

## <a name="applications-and-action-sets"></a><span data-ttu-id="1bc1e-108">Applications and action sets</span><span class="sxs-lookup"><span data-stu-id="1bc1e-108">Applications and action sets</span></span>

<span data-ttu-id="1bc1e-109">Here's how to fit your scenario into the framework.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-109">Here's how to fit your scenario into the framework.</span></span> <span data-ttu-id="1bc1e-110">Let's imagine three applications, one for each list that is being optimized:  app-politics, app-sports, and app-recent.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-110">Let's imagine three applications, one for each list that is being optimized:  app-politics, app-sports, and app-recent.</span></span> <span data-ttu-id="1bc1e-111">To specify the candidate articles for each application, there are two action sets: one for politics and one for sports.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-111">To specify the candidate articles for each application, there are two action sets: one for politics and one for sports.</span></span> <span data-ttu-id="1bc1e-112">The action set for app-recent comes automatically as a union of the other two sets.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-112">The action set for app-recent comes automatically as a union of the other two sets.</span></span>

> [!TIP]
> <span data-ttu-id="1bc1e-113">Action sets can be shared across applications in Custom Decision Service.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-113">Action sets can be shared across applications in Custom Decision Service.</span></span>

## <a name="prepare-action-set-feeds"></a><span data-ttu-id="1bc1e-114">Prepare action set feeds</span><span class="sxs-lookup"><span data-stu-id="1bc1e-114">Prepare action set feeds</span></span>

<span data-ttu-id="1bc1e-115">Custom Decision Service consumes action sets via RSS or Atom feeds provided by the customer.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-115">Custom Decision Service consumes action sets via RSS or Atom feeds provided by the customer.</span></span> <span data-ttu-id="1bc1e-116">You provide two feeds: one for politics and one for sports.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-116">You provide two feeds: one for politics and one for sports.</span></span> <span data-ttu-id="1bc1e-117">Suppose they are served from `http://www.domain.com/feeds/<feed-name>`.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-117">Suppose they are served from `http://www.domain.com/feeds/<feed-name>`.</span></span>

<span data-ttu-id="1bc1e-118">Each feed provides a list of articles.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-118">Each feed provides a list of articles.</span></span> <span data-ttu-id="1bc1e-119">In RSS, each one is specified by an `<item>` element, as follows:</span><span class="sxs-lookup"><span data-stu-id="1bc1e-119">In RSS, each one is specified by an `<item>` element, as follows:</span></span>

```xml
<rss version="2.0"><channel>
   <item>
      <title><![CDATA[article title]]></title>
      <link>"article url"</link>
      <pubDate>publication date</pubDate>
    </item>
</channel></rss>
```

<span data-ttu-id="1bc1e-120">The order of articles matters.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-120">The order of articles matters.</span></span> <span data-ttu-id="1bc1e-121">It specifies the default ranking, which is your best guess for how the articles should be ordered.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-121">It specifies the default ranking, which is your best guess for how the articles should be ordered.</span></span> <span data-ttu-id="1bc1e-122">The default ranking is then used for performance comparison on the [dashboard](#performance-dashboard).</span><span class="sxs-lookup"><span data-stu-id="1bc1e-122">The default ranking is then used for performance comparison on the [dashboard](#performance-dashboard).</span></span>

<span data-ttu-id="1bc1e-123">For more information on the feed format, see the [API reference](custom-decision-service-api-reference.md#action-set-api-customer-provided).</span><span class="sxs-lookup"><span data-stu-id="1bc1e-123">For more information on the feed format, see the [API reference](custom-decision-service-api-reference.md#action-set-api-customer-provided).</span></span>

## <a name="register-a-new-app"></a><span data-ttu-id="1bc1e-124">Register a new app</span><span class="sxs-lookup"><span data-stu-id="1bc1e-124">Register a new app</span></span>

1. <span data-ttu-id="1bc1e-125">Sign in with your [Microsoft account](https://account.microsoft.com/account).</span><span class="sxs-lookup"><span data-stu-id="1bc1e-125">Sign in with your [Microsoft account](https://account.microsoft.com/account).</span></span> <span data-ttu-id="1bc1e-126">On the ribbon, click **My Portal**.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-126">On the ribbon, click **My Portal**.</span></span>

2. <span data-ttu-id="1bc1e-127">To register a new application, click the **New App** button.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-127">To register a new application, click the **New App** button.</span></span>

    ![Custom Decision Service portal](./media/custom-decision-service-tutorial/portal.png)

3. <span data-ttu-id="1bc1e-129">Enter a unique name for your application in the **App ID** text box.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-129">Enter a unique name for your application in the **App ID** text box.</span></span> <span data-ttu-id="1bc1e-130">If this name is already in use by another customer, the system asks you to pick a different app ID.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-130">If this name is already in use by another customer, the system asks you to pick a different app ID.</span></span> <span data-ttu-id="1bc1e-131">Select the **Advanced** check box, and enter the [connection string](../../storage/common/storage-configure-connection-string.md) for your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-131">Select the **Advanced** check box, and enter the [connection string](../../storage/common/storage-configure-connection-string.md) for your Azure storage account.</span></span> <span data-ttu-id="1bc1e-132">Normally, you use the same storage account for all your applications.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-132">Normally, you use the same storage account for all your applications.</span></span>

    ![New app dialog box](./media/custom-decision-service-tutorial/new-app-dialog.png)

    <span data-ttu-id="1bc1e-134">After you register all three applications in the above scenario, they are listed:</span><span class="sxs-lookup"><span data-stu-id="1bc1e-134">After you register all three applications in the above scenario, they are listed:</span></span>

    ![List of apps](./media/custom-decision-service-tutorial/apps.png)

    <span data-ttu-id="1bc1e-136">You can come back to this list by clicking the **Apps** button.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-136">You can come back to this list by clicking the **Apps** button.</span></span>

4. <span data-ttu-id="1bc1e-137">In the **New App** dialog box, specify an action feed.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-137">In the **New App** dialog box, specify an action feed.</span></span> <span data-ttu-id="1bc1e-138">Action feeds can also be specified by clicking the **Feeds** button and then by clicking the **New Feed** button.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-138">Action feeds can also be specified by clicking the **Feeds** button and then by clicking the **New Feed** button.</span></span> <span data-ttu-id="1bc1e-139">Enter a **Name** for the new feed, enter the **URL** from which it is served, and enter the **Refresh Time**.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-139">Enter a **Name** for the new feed, enter the **URL** from which it is served, and enter the **Refresh Time**.</span></span> <span data-ttu-id="1bc1e-140">The refresh time specifies how frequently Custom Decision Service should refresh the feed.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-140">The refresh time specifies how frequently Custom Decision Service should refresh the feed.</span></span>

    ![New feed dialog box](./media/custom-decision-service-tutorial/new-feed-dialog.png)

    <span data-ttu-id="1bc1e-142">Action feeds can be used by any app, regardless of where they're specified.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-142">Action feeds can be used by any app, regardless of where they're specified.</span></span> <span data-ttu-id="1bc1e-143">After you specify both action feeds in a scenario, they are listed:</span><span class="sxs-lookup"><span data-stu-id="1bc1e-143">After you specify both action feeds in a scenario, they are listed:</span></span>

    ![List of feeds](./media/custom-decision-service-tutorial/feeds.png)

    <span data-ttu-id="1bc1e-145">You can come back to this list by clicking the **Feeds** button.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-145">You can come back to this list by clicking the **Feeds** button.</span></span>

## <a name="use-the-apis"></a><span data-ttu-id="1bc1e-146">Use the APIs</span><span class="sxs-lookup"><span data-stu-id="1bc1e-146">Use the APIs</span></span>

<span data-ttu-id="1bc1e-147">The Custom Decision Service ranks articles via the Ranking API.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-147">The Custom Decision Service ranks articles via the Ranking API.</span></span> <span data-ttu-id="1bc1e-148">To use this API, insert the following code into the HTML head of the front page:</span><span class="sxs-lookup"><span data-stu-id="1bc1e-148">To use this API, insert the following code into the HTML head of the front page:</span></span>

```html
<!-- Define the "callback function" to render UI -->
<script> function callback(data) { … } </script>

<!--  call Ranking API after callback() is defined, separately for each app -->
<script src="https://ds.microsoft.com/api/v2/app-politics/rank/feed-politics" async></script>
<script src="https://ds.microsoft.com/api/v2/app-sports/rank/feed-sports" async></script>
<script src="https://ds.microsoft.com/api/v2/app-recent/rank/feed-politics/feed-sports" async></script>
<!-- NB: action feeds for 'app-recent' are listed one after another. -->
```

<span data-ttu-id="1bc1e-149">The HTTP response from the Ranking API is a JSONP-formatted string.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-149">The HTTP response from the Ranking API is a JSONP-formatted string.</span></span> <span data-ttu-id="1bc1e-150">For app-politics, for example, the string looks like:</span><span class="sxs-lookup"><span data-stu-id="1bc1e-150">For app-politics, for example, the string looks like:</span></span>

```json
callback({
   "ranking":[{"id":"url1"}, {"id":"url2"}, {"id":"url3"}],
   "eventId":"<opaque event string>",
   "appId":"app-politics",
   "actionSets":[{"id":"feed-politics","lastRefresh":"date"}] });
```

<span data-ttu-id="1bc1e-151">The browser then executes this string as a call to the `callback()` function.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-151">The browser then executes this string as a call to the `callback()` function.</span></span> <span data-ttu-id="1bc1e-152">The `data` argument in the `callback()` function contains the app ID and the ranking of URLs to be rendered.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-152">The `data` argument in the `callback()` function contains the app ID and the ranking of URLs to be rendered.</span></span> <span data-ttu-id="1bc1e-153">In particular, `callback()` should use `data.appId` to distinguish between the three applications.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-153">In particular, `callback()` should use `data.appId` to distinguish between the three applications.</span></span> <span data-ttu-id="1bc1e-154">`eventId` is used internally by Custom Decision Service to match the provided ranking with the corresponding click, if any.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-154">`eventId` is used internally by Custom Decision Service to match the provided ranking with the corresponding click, if any.</span></span>

> [!TIP]
> <span data-ttu-id="1bc1e-155">`callback()` might check each action feed for freshness by using the `lastRefresh` field.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-155">`callback()` might check each action feed for freshness by using the `lastRefresh` field.</span></span> <span data-ttu-id="1bc1e-156">If a given feed is not sufficiently fresh, `callback()` might ignore the provided ranking, call this feed directly, and use the default ranking served by the feed.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-156">If a given feed is not sufficiently fresh, `callback()` might ignore the provided ranking, call this feed directly, and use the default ranking served by the feed.</span></span>

<span data-ttu-id="1bc1e-157">For more information on specifications and additional options provided by the Ranking API, see the [API reference](custom-decision-service-api-reference.md).</span><span class="sxs-lookup"><span data-stu-id="1bc1e-157">For more information on specifications and additional options provided by the Ranking API, see the [API reference](custom-decision-service-api-reference.md).</span></span>

<span data-ttu-id="1bc1e-158">The top article choices from the user are returned by calling the Reward API.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-158">The top article choices from the user are returned by calling the Reward API.</span></span> <span data-ttu-id="1bc1e-159">When a top article choice is received, the following code should be invoked on the front page:</span><span class="sxs-lookup"><span data-stu-id="1bc1e-159">When a top article choice is received, the following code should be invoked on the front page:</span></span>

```javascript
$.ajax({
    type: "POST",
    url: '//ds.microsoft.com/api/v2/<appId>/reward/<eventId>',
    contentType: "application/json" })
```

<span data-ttu-id="1bc1e-160">Using `appId` and `eventId` in the click-handling code requires some care.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-160">Using `appId` and `eventId` in the click-handling code requires some care.</span></span> <span data-ttu-id="1bc1e-161">For example, you can implement the `callback()` function as follows:</span><span class="sxs-lookup"><span data-stu-id="1bc1e-161">For example, you can implement the `callback()` function as follows:</span></span>

```javascript
function callback(data) {
    $.map(data.ranking, function (element) {
        //custom rendering function given content info
        render({appId:data.appId,
                article:element,
                onClick: element.id != data.rewardAction ? null :
                   function() {
                       $.ajax({
                       type: "POST",
                       url: '//ds.microsoft.com/api/v2/' + data.appId + '/reward/' + data.eventId,
                       contentType: "application/json" })}
                });
}}
```

<span data-ttu-id="1bc1e-162">In this example, implement the `render()` function to render a given article for a given application.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-162">In this example, implement the `render()` function to render a given article for a given application.</span></span> <span data-ttu-id="1bc1e-163">This function inputs the app ID and the article (in the format from the Ranking API).</span><span class="sxs-lookup"><span data-stu-id="1bc1e-163">This function inputs the app ID and the article (in the format from the Ranking API).</span></span> <span data-ttu-id="1bc1e-164">The `onClick` parameter is the function that should be called from `render()` to handle a click.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-164">The `onClick` parameter is the function that should be called from `render()` to handle a click.</span></span> <span data-ttu-id="1bc1e-165">It checks whether the click is on the top slot.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-165">It checks whether the click is on the top slot.</span></span> <span data-ttu-id="1bc1e-166">Then it calls the Reward API with the appropriate app ID and event ID.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-166">Then it calls the Reward API with the appropriate app ID and event ID.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bc1e-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="1bc1e-167">Next steps</span></span>

* <span data-ttu-id="1bc1e-168">Consult the [API reference](custom-decision-service-api-reference.md) to learn more about the provided functionality.</span><span class="sxs-lookup"><span data-stu-id="1bc1e-168">Consult the [API reference](custom-decision-service-api-reference.md) to learn more about the provided functionality.</span></span>