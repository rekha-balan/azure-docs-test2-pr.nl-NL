---
title: Bing Entity Search single-page web app | Microsoft Docs
description: Shows how to use the Bing Entity Search API in a single-page Web application.
services: cognitive-services
author: v-jerkin
manager: ehansen
ms.service: cognitive-services
ms.component: bing-entity-search
ms.topic: article
ms.date: 12/08/2017
ms.author: v-jerkin
ms.openlocfilehash: c48e5bb166c43ed27249aeda89f06df8dedadfa5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969327"
---
# <a name="tutorial-single-page-web-app"></a><span data-ttu-id="3ed25-103">Tutorial: Single-page web app</span><span class="sxs-lookup"><span data-stu-id="3ed25-103">Tutorial: Single-page web app</span></span>

<span data-ttu-id="3ed25-104">The Bing Entity Search API lets you search the Web for information about *entities* and *places.*</span><span class="sxs-lookup"><span data-stu-id="3ed25-104">The Bing Entity Search API lets you search the Web for information about *entities* and *places.*</span></span> <span data-ttu-id="3ed25-105">You may request either kind of result, or both, in a given query.</span><span class="sxs-lookup"><span data-stu-id="3ed25-105">You may request either kind of result, or both, in a given query.</span></span> <span data-ttu-id="3ed25-106">The definitions of places and entities are provided below.</span><span class="sxs-lookup"><span data-stu-id="3ed25-106">The definitions of places and entities are provided below.</span></span>

|||
|-|-|
|<span data-ttu-id="3ed25-107">Entities</span><span class="sxs-lookup"><span data-stu-id="3ed25-107">Entities</span></span>|<span data-ttu-id="3ed25-108">Well-known people, places, and things that you find by name</span><span class="sxs-lookup"><span data-stu-id="3ed25-108">Well-known people, places, and things that you find by name</span></span>|
|<span data-ttu-id="3ed25-109">Places</span><span class="sxs-lookup"><span data-stu-id="3ed25-109">Places</span></span>|<span data-ttu-id="3ed25-110">Restaurants, hotels, and other local businesses that you find by name *or* by type (Italian restaurants)</span><span class="sxs-lookup"><span data-stu-id="3ed25-110">Restaurants, hotels, and other local businesses that you find by name *or* by type (Italian restaurants)</span></span>|

<span data-ttu-id="3ed25-111">In this tutorial, we build a single-page Web application that uses the Bing Entity Search API to display search results right in the page.</span><span class="sxs-lookup"><span data-stu-id="3ed25-111">In this tutorial, we build a single-page Web application that uses the Bing Entity Search API to display search results right in the page.</span></span> <span data-ttu-id="3ed25-112">The application includes HTML, CSS, and JavaScript components.</span><span class="sxs-lookup"><span data-stu-id="3ed25-112">The application includes HTML, CSS, and JavaScript components.</span></span>

<span data-ttu-id="3ed25-113">The API lets you prioritize results by location.</span><span class="sxs-lookup"><span data-stu-id="3ed25-113">The API lets you prioritize results by location.</span></span> <span data-ttu-id="3ed25-114">In a mobile app, you can ask the device for its own location.</span><span class="sxs-lookup"><span data-stu-id="3ed25-114">In a mobile app, you can ask the device for its own location.</span></span> <span data-ttu-id="3ed25-115">In a Web app, you can use the `getPosition()` function.</span><span class="sxs-lookup"><span data-stu-id="3ed25-115">In a Web app, you can use the `getPosition()` function.</span></span> <span data-ttu-id="3ed25-116">But this call works only in secure contexts, and it may not provide a precise location.</span><span class="sxs-lookup"><span data-stu-id="3ed25-116">But this call works only in secure contexts, and it may not provide a precise location.</span></span> <span data-ttu-id="3ed25-117">Also, the user may want to search for entities near a location other than their own.</span><span class="sxs-lookup"><span data-stu-id="3ed25-117">Also, the user may want to search for entities near a location other than their own.</span></span>

<span data-ttu-id="3ed25-118">Our app therefore calls upon the Bing Maps service to obtain latitude and longitude from a user-entered location.</span><span class="sxs-lookup"><span data-stu-id="3ed25-118">Our app therefore calls upon the Bing Maps service to obtain latitude and longitude from a user-entered location.</span></span> <span data-ttu-id="3ed25-119">The user can then enter the name of a landmark ("Space Needle") or a full or partial address ("New York City"), and the Bing Maps API provides the coordinates.</span><span class="sxs-lookup"><span data-stu-id="3ed25-119">The user can then enter the name of a landmark ("Space Needle") or a full or partial address ("New York City"), and the Bing Maps API provides the coordinates.</span></span>

<!-- Remove until we can replace with a sanitized version.
![[Single-page Bing Entity Search app]](media/entity-search-spa-demo.png)
-->

> [!NOTE]
> <span data-ttu-id="3ed25-120">The JSON and HTTP headings at the bottom of the page reveal the JSON response and HTTP request information when clicked.</span><span class="sxs-lookup"><span data-stu-id="3ed25-120">The JSON and HTTP headings at the bottom of the page reveal the JSON response and HTTP request information when clicked.</span></span> <span data-ttu-id="3ed25-121">These details are useful when exploring the service.</span><span class="sxs-lookup"><span data-stu-id="3ed25-121">These details are useful when exploring the service.</span></span>

<span data-ttu-id="3ed25-122">The tutorial app illustrates how to:</span><span class="sxs-lookup"><span data-stu-id="3ed25-122">The tutorial app illustrates how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3ed25-123">Perform a Bing Entity Search API call in JavaScript</span><span class="sxs-lookup"><span data-stu-id="3ed25-123">Perform a Bing Entity Search API call in JavaScript</span></span>
> * <span data-ttu-id="3ed25-124">Perform a Bing Maps `locationQuery` API call in JavaScript</span><span class="sxs-lookup"><span data-stu-id="3ed25-124">Perform a Bing Maps `locationQuery` API call in JavaScript</span></span>
> * <span data-ttu-id="3ed25-125">Pass search options to the API calls</span><span class="sxs-lookup"><span data-stu-id="3ed25-125">Pass search options to the API calls</span></span>
> * <span data-ttu-id="3ed25-126">Display search results</span><span class="sxs-lookup"><span data-stu-id="3ed25-126">Display search results</span></span>
> * <span data-ttu-id="3ed25-127">Handle the Bing client ID and API subscription keys</span><span class="sxs-lookup"><span data-stu-id="3ed25-127">Handle the Bing client ID and API subscription keys</span></span>
> * <span data-ttu-id="3ed25-128">Deal with any errors that might occur</span><span class="sxs-lookup"><span data-stu-id="3ed25-128">Deal with any errors that might occur</span></span>

<span data-ttu-id="3ed25-129">The tutorial page is entirely self-contained; it does not use any external frameworks, style sheets, or even image files.</span><span class="sxs-lookup"><span data-stu-id="3ed25-129">The tutorial page is entirely self-contained; it does not use any external frameworks, style sheets, or even image files.</span></span> <span data-ttu-id="3ed25-130">It uses only widely supported JavaScript language features and works with current versions of all major Web browsers.</span><span class="sxs-lookup"><span data-stu-id="3ed25-130">It uses only widely supported JavaScript language features and works with current versions of all major Web browsers.</span></span>

<span data-ttu-id="3ed25-131">In this tutorial, we discuss only selected portions of the source code.</span><span class="sxs-lookup"><span data-stu-id="3ed25-131">In this tutorial, we discuss only selected portions of the source code.</span></span> <span data-ttu-id="3ed25-132">The full source code is available [on a separate page](tutorial-bing-entities-search-single-page-app-source.md).</span><span class="sxs-lookup"><span data-stu-id="3ed25-132">The full source code is available [on a separate page](tutorial-bing-entities-search-single-page-app-source.md).</span></span> <span data-ttu-id="3ed25-133">Copy and paste this code into a text editor and save it as `bing.html`.</span><span class="sxs-lookup"><span data-stu-id="3ed25-133">Copy and paste this code into a text editor and save it as `bing.html`.</span></span>

> [!NOTE]
> <span data-ttu-id="3ed25-134">This tutorial is substantially similar to the [single-page Bing Web Search app tutorial](../Bing-Web-Search/tutorial-bing-web-search-single-page-app.md), but deals only with entity search results.</span><span class="sxs-lookup"><span data-stu-id="3ed25-134">This tutorial is substantially similar to the [single-page Bing Web Search app tutorial](../Bing-Web-Search/tutorial-bing-web-search-single-page-app.md), but deals only with entity search results.</span></span>

## <a name="app-components"></a><span data-ttu-id="3ed25-135">App components</span><span class="sxs-lookup"><span data-stu-id="3ed25-135">App components</span></span>

<span data-ttu-id="3ed25-136">Like any single-page Web app, the tutorial application includes three parts:</span><span class="sxs-lookup"><span data-stu-id="3ed25-136">Like any single-page Web app, the tutorial application includes three parts:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3ed25-137">HTML - Defines the structure and content of the page</span><span class="sxs-lookup"><span data-stu-id="3ed25-137">HTML - Defines the structure and content of the page</span></span>
> * <span data-ttu-id="3ed25-138">CSS - Defines the appearance of the page</span><span class="sxs-lookup"><span data-stu-id="3ed25-138">CSS - Defines the appearance of the page</span></span>
> * <span data-ttu-id="3ed25-139">JavaScript - Defines the behavior of the page</span><span class="sxs-lookup"><span data-stu-id="3ed25-139">JavaScript - Defines the behavior of the page</span></span>

<span data-ttu-id="3ed25-140">This tutorial doesn't cover most of the HTML or CSS in detail, as they are straightforward.</span><span class="sxs-lookup"><span data-stu-id="3ed25-140">This tutorial doesn't cover most of the HTML or CSS in detail, as they are straightforward.</span></span>

<span data-ttu-id="3ed25-141">The HTML contains the search form in which the user enters a query and chooses search options.</span><span class="sxs-lookup"><span data-stu-id="3ed25-141">The HTML contains the search form in which the user enters a query and chooses search options.</span></span> <span data-ttu-id="3ed25-142">The form is connected to the JavaScript that actually performs the search by the `<form>` tag's `onsubmit` attribute:</span><span class="sxs-lookup"><span data-stu-id="3ed25-142">The form is connected to the JavaScript that actually performs the search by the `<form>` tag's `onsubmit` attribute:</span></span>

```html
<form name="bing" onsubmit="return newBingEntitySearch(this)">
```

<span data-ttu-id="3ed25-143">The `onsubmit` handler returns `false`, which keeps the form from being submitted to a server.</span><span class="sxs-lookup"><span data-stu-id="3ed25-143">The `onsubmit` handler returns `false`, which keeps the form from being submitted to a server.</span></span> <span data-ttu-id="3ed25-144">The JavaScript code actually does the work of collecting the necessary information from the form and performing the search.</span><span class="sxs-lookup"><span data-stu-id="3ed25-144">The JavaScript code actually does the work of collecting the necessary information from the form and performing the search.</span></span>

<span data-ttu-id="3ed25-145">The search is done in two phases.</span><span class="sxs-lookup"><span data-stu-id="3ed25-145">The search is done in two phases.</span></span> <span data-ttu-id="3ed25-146">First, if the user has entered a location restriction, a Bing Maps query is done to convert it into coordinates.</span><span class="sxs-lookup"><span data-stu-id="3ed25-146">First, if the user has entered a location restriction, a Bing Maps query is done to convert it into coordinates.</span></span> <span data-ttu-id="3ed25-147">The callback for this query then kicks off the Bing Entity Search query.</span><span class="sxs-lookup"><span data-stu-id="3ed25-147">The callback for this query then kicks off the Bing Entity Search query.</span></span>

<span data-ttu-id="3ed25-148">The HTML also contains the divisions (HTML `<div>` tags) where the search results appear.</span><span class="sxs-lookup"><span data-stu-id="3ed25-148">The HTML also contains the divisions (HTML `<div>` tags) where the search results appear.</span></span>

## <a name="managing-subscription-keys"></a><span data-ttu-id="3ed25-149">Managing subscription keys</span><span class="sxs-lookup"><span data-stu-id="3ed25-149">Managing subscription keys</span></span>

> [!NOTE]
> <span data-ttu-id="3ed25-150">This app requires subscription keys for both the Bing Search API and the Bing Maps API.</span><span class="sxs-lookup"><span data-stu-id="3ed25-150">This app requires subscription keys for both the Bing Search API and the Bing Maps API.</span></span> <span data-ttu-id="3ed25-151">You can use a [trial Bing Search key](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) and a [basic Bing Maps key](https://www.microsoft.com/maps/create-a-bing-maps-key).</span><span class="sxs-lookup"><span data-stu-id="3ed25-151">You can use a [trial Bing Search key](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) and a [basic Bing Maps key](https://www.microsoft.com/maps/create-a-bing-maps-key).</span></span>

<span data-ttu-id="3ed25-152">To avoid having to include the Bing Search and Bing Maps API subscription keys in the code, we use the browser's persistent storage to store them.</span><span class="sxs-lookup"><span data-stu-id="3ed25-152">To avoid having to include the Bing Search and Bing Maps API subscription keys in the code, we use the browser's persistent storage to store them.</span></span> <span data-ttu-id="3ed25-153">If either key has not been stored, we prompt for it and store it for later use.</span><span class="sxs-lookup"><span data-stu-id="3ed25-153">If either key has not been stored, we prompt for it and store it for later use.</span></span> <span data-ttu-id="3ed25-154">If the key is later rejected by the API, we invalidate the stored key so the user is asked for it upon their next search.</span><span class="sxs-lookup"><span data-stu-id="3ed25-154">If the key is later rejected by the API, we invalidate the stored key so the user is asked for it upon their next search.</span></span>

<span data-ttu-id="3ed25-155">We define `storeValue` and `retrieveValue` functions that use either the `localStorage` object (if the browser supports it) or a cookie.</span><span class="sxs-lookup"><span data-stu-id="3ed25-155">We define `storeValue` and `retrieveValue` functions that use either the `localStorage` object (if the browser supports it) or a cookie.</span></span> <span data-ttu-id="3ed25-156">Our `getSubscriptionKey()` function uses these functions to store and retrieve the user's key.</span><span class="sxs-lookup"><span data-stu-id="3ed25-156">Our `getSubscriptionKey()` function uses these functions to store and retrieve the user's key.</span></span>

```javascript
// cookie names for data we store
SEARCH_API_KEY_COOKIE = "bing-search-api-key";
MAPS_API_KEY_COOKIE   = "bing-maps-api-key";
CLIENT_ID_COOKIE      = "bing-search-client-id";

// API endpoints
SEARCH_ENDPOINT = "https://api.cognitive.microsoft.com/bing/v7.0/entities";
MAPS_ENDPOINT   = "http://dev.virtualearth.net/REST/v1/Locations";

// ... omitted definitions of storeValue() and retrieveValue()

// get stored API subscription key, or prompt if it's not found
function getSubscriptionKey(cookie_name, key_length, api_name) {
    var key = retrieveValue(cookie_name);
    while (key.length !== key_length) {
        key = prompt("Enter " + api_name + " API subscription key:", "").trim();
    }
    // always set the cookie in order to update the expiration date
    storeValue(cookie_name, key);
    return key;
}

function getMapsSubscriptionKey() {
    return getSubscriptionKey(MAPS_API_KEY_COOKIE, 64, "Bing Maps");
}

function getSearchSubscriptionKey() {
    return getSubscriptionKey(SEARCH_API_KEY_COOKIE, 32, "Bing Search");
}
```

<span data-ttu-id="3ed25-157">The HTML `<body>` tag includes an `onload` attribute that calls `getSearchSubscriptionKey()` and `getMapsSubscriptionKey()` when the page has finished loading.</span><span class="sxs-lookup"><span data-stu-id="3ed25-157">The HTML `<body>` tag includes an `onload` attribute that calls `getSearchSubscriptionKey()` and `getMapsSubscriptionKey()` when the page has finished loading.</span></span> <span data-ttu-id="3ed25-158">These calls serve to immediately prompt the user for their keys if they haven't yet entered them.</span><span class="sxs-lookup"><span data-stu-id="3ed25-158">These calls serve to immediately prompt the user for their keys if they haven't yet entered them.</span></span>

```html
<body onload="document.forms.bing.query.focus(); getSearchSubscriptionKey(); getMapsSubscriptionKey();">
```

## <a name="selecting-search-options"></a><span data-ttu-id="3ed25-159">Selecting search options</span><span class="sxs-lookup"><span data-stu-id="3ed25-159">Selecting search options</span></span>

![[Bing Entity Search form]](media/entity-search-spa-form.png)

<span data-ttu-id="3ed25-161">The HTML form includes the following controls:</span><span class="sxs-lookup"><span data-stu-id="3ed25-161">The HTML form includes the following controls:</span></span>

| | |
|-|-|
|`where`|<span data-ttu-id="3ed25-162">A drop-down menu for selecting the market (location and language) used for the search.</span><span class="sxs-lookup"><span data-stu-id="3ed25-162">A drop-down menu for selecting the market (location and language) used for the search.</span></span>|
|`query`|<span data-ttu-id="3ed25-163">The text field in which to enter the search terms.</span><span class="sxs-lookup"><span data-stu-id="3ed25-163">The text field in which to enter the search terms.</span></span>|
|`safe`|<span data-ttu-id="3ed25-164">A checkbox indicating whether SafeSearch is turned on (restricts "adult" results)</span><span class="sxs-lookup"><span data-stu-id="3ed25-164">A checkbox indicating whether SafeSearch is turned on (restricts "adult" results)</span></span>|
|`what`|<span data-ttu-id="3ed25-165">A menu for choosing to search for entities, places, or both.</span><span class="sxs-lookup"><span data-stu-id="3ed25-165">A menu for choosing to search for entities, places, or both.</span></span>|
|`mapquery`|<span data-ttu-id="3ed25-166">The text field in which the user may enter a full or partial address, a landmark, etc. to help Bing Entity Search return more relevant results.</span><span class="sxs-lookup"><span data-stu-id="3ed25-166">The text field in which the user may enter a full or partial address, a landmark, etc. to help Bing Entity Search return more relevant results.</span></span>|

> [!NOTE]
> <span data-ttu-id="3ed25-167">Places results are currently available only in the United States.</span><span class="sxs-lookup"><span data-stu-id="3ed25-167">Places results are currently available only in the United States.</span></span> <span data-ttu-id="3ed25-168">The `where` and `what` menus have code to enforce this restriction.</span><span class="sxs-lookup"><span data-stu-id="3ed25-168">The `where` and `what` menus have code to enforce this restriction.</span></span> <span data-ttu-id="3ed25-169">If you choose a non-US market while Places is selected in the `what` menu, `what` changes to Anything.</span><span class="sxs-lookup"><span data-stu-id="3ed25-169">If you choose a non-US market while Places is selected in the `what` menu, `what` changes to Anything.</span></span> <span data-ttu-id="3ed25-170">If you choose Places while a non-US market is selected in the `where` menu, `where` changes to the US.</span><span class="sxs-lookup"><span data-stu-id="3ed25-170">If you choose Places while a non-US market is selected in the `where` menu, `where` changes to the US.</span></span>

<span data-ttu-id="3ed25-171">Our JavaScript function `bingSearchOptions()` converts these fields to a partial query string for the Bing Search API.</span><span class="sxs-lookup"><span data-stu-id="3ed25-171">Our JavaScript function `bingSearchOptions()` converts these fields to a partial query string for the Bing Search API.</span></span>

```javascript
// build query options from the HTML form
function bingSearchOptions(form) {

    var options = [];
    options.push("mkt=" + form.where.value);
    options.push("SafeSearch=" + (form.safe.checked ? "strict" : "off"));
    if (form.what.selectedIndex) options.push("responseFilter=" + form.what.value);
    return options.join("&");
}
```

<span data-ttu-id="3ed25-172">For example, the SafeSearch feature can be `strict`, `moderate`, or `off`, with `moderate` being the default.</span><span class="sxs-lookup"><span data-stu-id="3ed25-172">For example, the SafeSearch feature can be `strict`, `moderate`, or `off`, with `moderate` being the default.</span></span> <span data-ttu-id="3ed25-173">But our form uses a checkbox, which has only two states.</span><span class="sxs-lookup"><span data-stu-id="3ed25-173">But our form uses a checkbox, which has only two states.</span></span> <span data-ttu-id="3ed25-174">The JavaScript code converts this setting to either `strict` or `off` (we don't use `moderate`).</span><span class="sxs-lookup"><span data-stu-id="3ed25-174">The JavaScript code converts this setting to either `strict` or `off` (we don't use `moderate`).</span></span>

<span data-ttu-id="3ed25-175">The `mapquery` field isn't handled in `bingSearchOptions()` because it is used for the Bing Maps location query, not for Bing Entity Search.</span><span class="sxs-lookup"><span data-stu-id="3ed25-175">The `mapquery` field isn't handled in `bingSearchOptions()` because it is used for the Bing Maps location query, not for Bing Entity Search.</span></span>

## <a name="obtaining-a-location"></a><span data-ttu-id="3ed25-176">Obtaining a location</span><span class="sxs-lookup"><span data-stu-id="3ed25-176">Obtaining a location</span></span>

<span data-ttu-id="3ed25-177">The Bing Maps API offers a [`locationQuery` method](//msdn.microsoft.com/library/ff701711.aspx), which we use to find the latitude and longitude of the location the user enters.</span><span class="sxs-lookup"><span data-stu-id="3ed25-177">The Bing Maps API offers a [`locationQuery` method](//msdn.microsoft.com/library/ff701711.aspx), which we use to find the latitude and longitude of the location the user enters.</span></span> <span data-ttu-id="3ed25-178">These coordinates are then passed to the Bing Entity Search API with the user's request.</span><span class="sxs-lookup"><span data-stu-id="3ed25-178">These coordinates are then passed to the Bing Entity Search API with the user's request.</span></span> <span data-ttu-id="3ed25-179">The search results prioritize entities and places that are close to the specified location.</span><span class="sxs-lookup"><span data-stu-id="3ed25-179">The search results prioritize entities and places that are close to the specified location.</span></span>

<span data-ttu-id="3ed25-180">We can't access the Bing Maps API using an ordinary `XMLHttpRequest` query in a Web app because the service does not support cross-origin queries.</span><span class="sxs-lookup"><span data-stu-id="3ed25-180">We can't access the Bing Maps API using an ordinary `XMLHttpRequest` query in a Web app because the service does not support cross-origin queries.</span></span> <span data-ttu-id="3ed25-181">Fortunately, it supports JSONP (the "P" is for "padded").</span><span class="sxs-lookup"><span data-stu-id="3ed25-181">Fortunately, it supports JSONP (the "P" is for "padded").</span></span> <span data-ttu-id="3ed25-182">A JSONP response is an ordinary JSON response wrapped in a function call.</span><span class="sxs-lookup"><span data-stu-id="3ed25-182">A JSONP response is an ordinary JSON response wrapped in a function call.</span></span> <span data-ttu-id="3ed25-183">The request is made by inserting using a `<script>` tag into the document.</span><span class="sxs-lookup"><span data-stu-id="3ed25-183">The request is made by inserting using a `<script>` tag into the document.</span></span> <span data-ttu-id="3ed25-184">(Loading scripts is not subject to browser security policies.)</span><span class="sxs-lookup"><span data-stu-id="3ed25-184">(Loading scripts is not subject to browser security policies.)</span></span>

<span data-ttu-id="3ed25-185">The `bingMapsLocate()` function creates and inserts the `<script>` tag for the query.</span><span class="sxs-lookup"><span data-stu-id="3ed25-185">The `bingMapsLocate()` function creates and inserts the `<script>` tag for the query.</span></span> <span data-ttu-id="3ed25-186">The `jsonp=bingMapsCallback` segment of the query string specifies the name of the function to be called with the response.</span><span class="sxs-lookup"><span data-stu-id="3ed25-186">The `jsonp=bingMapsCallback` segment of the query string specifies the name of the function to be called with the response.</span></span>

```javascript
function bingMapsLocate(where) {

    where = where.trim();
    var url = MAPS_ENDPOINT + "?q=" + encodeURIComponent(where) + 
                "&jsonp=bingMapsCallback&maxResults=1&key=" + getMapsSubscriptionKey();

    var script = document.getElementById("bingMapsResult")
    if (script) script.parentElement.removeChild(script);

    // global variable holds reference to timer that will complete the search if the maps query fails
    timer = setTimeout(function() {
        timer = null;
        var form = document.forms.bing;
        bingEntitySearch(form.query.value, "", bingSearchOptions(form), getSearchSubscriptionKey());
    }, 5000);

    script = document.createElement("script");
    script.setAttribute("type", "text/javascript");
    script.setAttribute("id", "bingMapsResult");
    script.setAttribute("src", url);
    script.setAttribute("onerror", "BingMapsCallback(null)");
    document.body.appendChild(script);

    return false;
}
```

> [!NOTE]
> <span data-ttu-id="3ed25-187">If the Bing Maps API does not respond, the `bingMapsCallBack()` function is never called.</span><span class="sxs-lookup"><span data-stu-id="3ed25-187">If the Bing Maps API does not respond, the `bingMapsCallBack()` function is never called.</span></span> <span data-ttu-id="3ed25-188">Ordinarily, that would mean that `bingEntitySearch()` isn't called, and the entity search results do not appear.</span><span class="sxs-lookup"><span data-stu-id="3ed25-188">Ordinarily, that would mean that `bingEntitySearch()` isn't called, and the entity search results do not appear.</span></span> <span data-ttu-id="3ed25-189">To avoid this scenario, `bingMapsLocate()` also sets a timer to call `bingEntitySearch()` after five seconds.</span><span class="sxs-lookup"><span data-stu-id="3ed25-189">To avoid this scenario, `bingMapsLocate()` also sets a timer to call `bingEntitySearch()` after five seconds.</span></span> <span data-ttu-id="3ed25-190">There is logic in the callback function to avoid performing the entity search twice.</span><span class="sxs-lookup"><span data-stu-id="3ed25-190">There is logic in the callback function to avoid performing the entity search twice.</span></span>

<span data-ttu-id="3ed25-191">When the query completes, the `bingMapsCallback()` function is called, as requested.</span><span class="sxs-lookup"><span data-stu-id="3ed25-191">When the query completes, the `bingMapsCallback()` function is called, as requested.</span></span>

```javascript
function bingMapsCallback(response) {

    if (timer) {    // we beat the timer; stop it from firing
        clearTimeout(timer);
        timer = null;
    } else {        // the timer beat us; don't do anything
        return; 
    }

    var location = "";
    var name = "";
    var radius = 1000;

    if (response) {
        try {
            if (response.statusCode === 401) {
                invalidateMapsKey();
            } else if (response.statusCode === 200) {
                var resource = response.resourceSets[0].resources[0];
                var coords   = resource.point.coordinates;
                name         = resource.name;

                // the radius is the largest of the distances between the location and the corners
                // of its bounding box (in case it's not in the center) with a minimum of 1 km
                try {
                    var bbox    = resource.bbox;
                    radius  = Math.max(haversineDistance(bbox[0], bbox[1], coords[0], coords[1]),
                                       haversineDistance(coords[0], coords[1], bbox[2], bbox[1]),
                                       haversineDistance(bbox[0], bbox[3], coords[0], coords[1]),
                                       haversineDistance(coords[0], coords[1], bbox[2], bbox[3]), 1000);
                } catch(e) {  }
                var location = "lat:" + coords[0] + ";long:" + coords[1] + ";re:" + Math.round(radius);
            }
        }
        catch (e) { }   // response is unexpected. this isn't fatal, so just don't provide location
    }

    var form = document.forms.bing;
    if (name) form.mapquery.value = name;
    bingEntitySearch(form.query.value, location, bingSearchOptions(form), getSearchSubscriptionKey());

}
```

<span data-ttu-id="3ed25-192">Along with latitude and longitude, the Bing Entity Search query requires a *radius* that indicates the precision of the location information.</span><span class="sxs-lookup"><span data-stu-id="3ed25-192">Along with latitude and longitude, the Bing Entity Search query requires a *radius* that indicates the precision of the location information.</span></span> <span data-ttu-id="3ed25-193">We calculate the radius using the *bounding box* provided in the Bing Maps response.</span><span class="sxs-lookup"><span data-stu-id="3ed25-193">We calculate the radius using the *bounding box* provided in the Bing Maps response.</span></span> <span data-ttu-id="3ed25-194">The bounding box is a rectangle that surrounds the entire location.</span><span class="sxs-lookup"><span data-stu-id="3ed25-194">The bounding box is a rectangle that surrounds the entire location.</span></span> <span data-ttu-id="3ed25-195">For example, if the user enters `NYC`, the result contains roughly central coordinates of New York City and a bounding box that encompasses the city.</span><span class="sxs-lookup"><span data-stu-id="3ed25-195">For example, if the user enters `NYC`, the result contains roughly central coordinates of New York City and a bounding box that encompasses the city.</span></span> 

<span data-ttu-id="3ed25-196">We first calculate the distances from the primary coordinates to each of the four corners of the bounding box using the function `haversineDistance()` (not shown).</span><span class="sxs-lookup"><span data-stu-id="3ed25-196">We first calculate the distances from the primary coordinates to each of the four corners of the bounding box using the function `haversineDistance()` (not shown).</span></span> <span data-ttu-id="3ed25-197">We use the largest of these four distances as the radius.</span><span class="sxs-lookup"><span data-stu-id="3ed25-197">We use the largest of these four distances as the radius.</span></span> <span data-ttu-id="3ed25-198">The minimum radius is a kilometer.</span><span class="sxs-lookup"><span data-stu-id="3ed25-198">The minimum radius is a kilometer.</span></span> <span data-ttu-id="3ed25-199">This value is also used as a default if no bounding box is provided in the response.</span><span class="sxs-lookup"><span data-stu-id="3ed25-199">This value is also used as a default if no bounding box is provided in the response.</span></span>

<span data-ttu-id="3ed25-200">Having obtained the coordinates and the radius, we then call `bingEntitySearch()` to perform the actual search.</span><span class="sxs-lookup"><span data-stu-id="3ed25-200">Having obtained the coordinates and the radius, we then call `bingEntitySearch()` to perform the actual search.</span></span>

## <a name="performing-the-search"></a><span data-ttu-id="3ed25-201">Performing the search</span><span class="sxs-lookup"><span data-stu-id="3ed25-201">Performing the search</span></span>

<span data-ttu-id="3ed25-202">Given the query, a location, an options string, and the API key, the `BingEntitySearch()` function makes the Bing Entity Search request.</span><span class="sxs-lookup"><span data-stu-id="3ed25-202">Given the query, a location, an options string, and the API key, the `BingEntitySearch()` function makes the Bing Entity Search request.</span></span>

```javascript
// perform a search given query, location, options string, and API keys
function bingEntitySearch(query, latlong, options, key) {

    // scroll to top of window
    window.scrollTo(0, 0);
    if (!query.trim().length) return false;     // empty query, do nothing

    showDiv("noresults", "Working. Please wait.");
    hideDivs("pole", "mainline", "sidebar", "_json", "_http", "error");

    var request = new XMLHttpRequest();
    var queryurl = SEARCH_ENDPOINT + "?q=" + encodeURIComponent(query) + "&" + options;

    // open the request
    try {
        request.open("GET", queryurl);
    } 
    catch (e) {
        renderErrorMessage("Bad request (invalid URL)\n" + queryurl);
        return false;
    }

    // add request headers
    request.setRequestHeader("Ocp-Apim-Subscription-Key", key);
    request.setRequestHeader("Accept", "application/json");

    var clientid = retrieveValue(CLIENT_ID_COOKIE);
    if (clientid) request.setRequestHeader("X-MSEdge-ClientID", clientid);

    if (latlong) request.setRequestHeader("X-Search-Location", latlong);

    // event handler for successful response
    request.addEventListener("load", handleBingResponse);
    
    // event handler for erorrs
    request.addEventListener("error", function() {
        renderErrorMessage("Error completing request");
    });

    // event handler for aborted request
    request.addEventListener("abort", function() {
        renderErrorMessage("Request aborted");
    });

    // send the request
    request.send();
    return false;
}
```

<span data-ttu-id="3ed25-203">Upon successful completion of the HTTP request, JavaScript calls our `load` event handler, the `handleBingResponse()` function, to handle a successful HTTP GET request to the API.</span><span class="sxs-lookup"><span data-stu-id="3ed25-203">Upon successful completion of the HTTP request, JavaScript calls our `load` event handler, the `handleBingResponse()` function, to handle a successful HTTP GET request to the API.</span></span> 

```javascript
// handle Bing search request results
function handleBingResponse() {
    hideDivs("noresults");

    var json = this.responseText.trim();
    var jsobj = {};

    // try to parse JSON results
    try {
        if (json.length) jsobj = JSON.parse(json);
    } catch(e) {
        renderErrorMessage("Invalid JSON response");
    }

    // show raw JSON and HTTP request
    showDiv("json", preFormat(JSON.stringify(jsobj, null, 2)));
    showDiv("http", preFormat("GET " + this.responseURL + "\n\nStatus: " + this.status + " " + 
        this.statusText + "\n" + this.getAllResponseHeaders()));

    // if HTTP response is 200 OK, try to render search results
    if (this.status === 200) {
        var clientid = this.getResponseHeader("X-MSEdge-ClientID");
        if (clientid) retrieveValue(CLIENT_ID_COOKIE, clientid);
        if (json.length) {
            if (jsobj._type === "SearchResponse") {
                renderSearchResults(jsobj);
            } else {
                renderErrorMessage("No search results in JSON response");
            }
        } else {
            renderErrorMessage("Empty response (are you sending too many requests too quickly?)");
        }
    if (divHidden("pole") && divHidden("mainline") && divHidden("sidebar")) 
        showDiv("noresults", "No results.<p><small>Looking for restaurants or other local businesses? Those currently areen't supported outside the US.</small>");
    }

    // Any other HTTP status is an error
    else {
        // 401 is unauthorized; force re-prompt for API key for next request
        if (this.status === 401) invalidateSearchKey();

        // some error responses don't have a top-level errors object, so gin one up
        var errors = jsobj.errors || [jsobj];
        var errmsg = [];

        // display HTTP status code
        errmsg.push("HTTP Status " + this.status + " " + this.statusText + "\n");

        // add all fields from all error responses
        for (var i = 0; i < errors.length; i++) {
            if (i) errmsg.push("\n");
            for (var k in errors[i]) errmsg.push(k + ": " + errors[i][k]);
        }

        // also display Bing Trace ID if it isn't blocked by CORS
        var traceid = this.getResponseHeader("BingAPIs-TraceId");
        if (traceid) errmsg.push("\nTrace ID " + traceid);

        // and display the error message
        renderErrorMessage(errmsg.join("\n"));
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="3ed25-204">A successful HTTP request does *not* necessarily mean that the search itself succeeded.</span><span class="sxs-lookup"><span data-stu-id="3ed25-204">A successful HTTP request does *not* necessarily mean that the search itself succeeded.</span></span> <span data-ttu-id="3ed25-205">If an error occurs in the search operation, the Bing Entity Search API returns a non-200 HTTP status code and includes error information in the JSON response.</span><span class="sxs-lookup"><span data-stu-id="3ed25-205">If an error occurs in the search operation, the Bing Entity Search API returns a non-200 HTTP status code and includes error information in the JSON response.</span></span> <span data-ttu-id="3ed25-206">Additionally, if the request was rate-limited, the API returns an empty response.</span><span class="sxs-lookup"><span data-stu-id="3ed25-206">Additionally, if the request was rate-limited, the API returns an empty response.</span></span>

<span data-ttu-id="3ed25-207">Much of the code in both of the preceding functions is dedicated to error handling.</span><span class="sxs-lookup"><span data-stu-id="3ed25-207">Much of the code in both of the preceding functions is dedicated to error handling.</span></span> <span data-ttu-id="3ed25-208">Errors may occur at the following stages:</span><span class="sxs-lookup"><span data-stu-id="3ed25-208">Errors may occur at the following stages:</span></span>

|<span data-ttu-id="3ed25-209">Stage</span><span class="sxs-lookup"><span data-stu-id="3ed25-209">Stage</span></span>|<span data-ttu-id="3ed25-210">Potential error(s)</span><span class="sxs-lookup"><span data-stu-id="3ed25-210">Potential error(s)</span></span>|<span data-ttu-id="3ed25-211">Handled by</span><span class="sxs-lookup"><span data-stu-id="3ed25-211">Handled by</span></span>|
|-|-|-|
|<span data-ttu-id="3ed25-212">Building JavaScript request object</span><span class="sxs-lookup"><span data-stu-id="3ed25-212">Building JavaScript request object</span></span>|<span data-ttu-id="3ed25-213">Invalid URL</span><span class="sxs-lookup"><span data-stu-id="3ed25-213">Invalid URL</span></span>|<span data-ttu-id="3ed25-214">`try`/`catch` block</span><span class="sxs-lookup"><span data-stu-id="3ed25-214">`try`/`catch` block</span></span>|
|<span data-ttu-id="3ed25-215">Making the request</span><span class="sxs-lookup"><span data-stu-id="3ed25-215">Making the request</span></span>|<span data-ttu-id="3ed25-216">Network errors, aborted connections</span><span class="sxs-lookup"><span data-stu-id="3ed25-216">Network errors, aborted connections</span></span>|<span data-ttu-id="3ed25-217">`error` and `abort` event handlers</span><span class="sxs-lookup"><span data-stu-id="3ed25-217">`error` and `abort` event handlers</span></span>|
|<span data-ttu-id="3ed25-218">Performing the search</span><span class="sxs-lookup"><span data-stu-id="3ed25-218">Performing the search</span></span>|<span data-ttu-id="3ed25-219">Invalid request, invalid JSON, rate limits</span><span class="sxs-lookup"><span data-stu-id="3ed25-219">Invalid request, invalid JSON, rate limits</span></span>|<span data-ttu-id="3ed25-220">tests in `load` event handler</span><span class="sxs-lookup"><span data-stu-id="3ed25-220">tests in `load` event handler</span></span>|

<span data-ttu-id="3ed25-221">Errors are handled by calling `renderErrorMessage()` with any details known about the error.</span><span class="sxs-lookup"><span data-stu-id="3ed25-221">Errors are handled by calling `renderErrorMessage()` with any details known about the error.</span></span> <span data-ttu-id="3ed25-222">If the response passes the full gauntlet of error tests, we call `renderSearchResults()` to display the search results in the page.</span><span class="sxs-lookup"><span data-stu-id="3ed25-222">If the response passes the full gauntlet of error tests, we call `renderSearchResults()` to display the search results in the page.</span></span>

## <a name="displaying-search-results"></a><span data-ttu-id="3ed25-223">Displaying search results</span><span class="sxs-lookup"><span data-stu-id="3ed25-223">Displaying search results</span></span>

<span data-ttu-id="3ed25-224">The Bing Entity Search API [requires you to display results in a specified order](use-display-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="3ed25-224">The Bing Entity Search API [requires you to display results in a specified order](use-display-requirements.md).</span></span> <span data-ttu-id="3ed25-225">Since the API may return two different kinds of responses, it is not enough to iterate through the top-level `Entities` or `Places` collection in the JSON response and display those results.</span><span class="sxs-lookup"><span data-stu-id="3ed25-225">Since the API may return two different kinds of responses, it is not enough to iterate through the top-level `Entities` or `Places` collection in the JSON response and display those results.</span></span> <span data-ttu-id="3ed25-226">(If you want only one type of result, use the `responseFilter` query parameter.)</span><span class="sxs-lookup"><span data-stu-id="3ed25-226">(If you want only one type of result, use the `responseFilter` query parameter.)</span></span>

<span data-ttu-id="3ed25-227">Instead, we use the `rankingResponse` collection in the search results to order the results for display.</span><span class="sxs-lookup"><span data-stu-id="3ed25-227">Instead, we use the `rankingResponse` collection in the search results to order the results for display.</span></span> <span data-ttu-id="3ed25-228">This object refers to items in the `Entitiess` and/or `Places` collections.</span><span class="sxs-lookup"><span data-stu-id="3ed25-228">This object refers to items in the `Entitiess` and/or `Places` collections.</span></span>

<span data-ttu-id="3ed25-229">`rankingResponse` may contain up to three collections of search results, designated `pole`, `mainline`, and `sidebar`.</span><span class="sxs-lookup"><span data-stu-id="3ed25-229">`rankingResponse` may contain up to three collections of search results, designated `pole`, `mainline`, and `sidebar`.</span></span> 

<span data-ttu-id="3ed25-230">`pole`, if present, is the most relevant search result and should be displayed prominently.</span><span class="sxs-lookup"><span data-stu-id="3ed25-230">`pole`, if present, is the most relevant search result and should be displayed prominently.</span></span> <span data-ttu-id="3ed25-231">`mainline` refers to the bulk of the search results.</span><span class="sxs-lookup"><span data-stu-id="3ed25-231">`mainline` refers to the bulk of the search results.</span></span> <span data-ttu-id="3ed25-232">Mainline results should be displayed immediately after `pole` (or first, if `pole` is not present).</span><span class="sxs-lookup"><span data-stu-id="3ed25-232">Mainline results should be displayed immediately after `pole` (or first, if `pole` is not present).</span></span> 

<span data-ttu-id="3ed25-233">Finally.</span><span class="sxs-lookup"><span data-stu-id="3ed25-233">Finally.</span></span> <span data-ttu-id="3ed25-234">`sidebar` refers to auxiliary search results.</span><span class="sxs-lookup"><span data-stu-id="3ed25-234">`sidebar` refers to auxiliary search results.</span></span> <span data-ttu-id="3ed25-235">They may be displayed in an actual sidebar or simply after the mainline results.</span><span class="sxs-lookup"><span data-stu-id="3ed25-235">They may be displayed in an actual sidebar or simply after the mainline results.</span></span> <span data-ttu-id="3ed25-236">We have chosen the latter for our tutorial app.</span><span class="sxs-lookup"><span data-stu-id="3ed25-236">We have chosen the latter for our tutorial app.</span></span>

<span data-ttu-id="3ed25-237">Each item in a `rankingResponse` collection refers to the actual search result items in two different, but equivalent, ways.</span><span class="sxs-lookup"><span data-stu-id="3ed25-237">Each item in a `rankingResponse` collection refers to the actual search result items in two different, but equivalent, ways.</span></span>

| | |
|-|-|
|`id`|<span data-ttu-id="3ed25-238">The `id` looks like a URL, but should not be used for links.</span><span class="sxs-lookup"><span data-stu-id="3ed25-238">The `id` looks like a URL, but should not be used for links.</span></span> <span data-ttu-id="3ed25-239">The `id` type of a ranking result matches the `id` of either a search result item in an answer collection, *or* an entire answer collection (such as `Entities`).</span><span class="sxs-lookup"><span data-stu-id="3ed25-239">The `id` type of a ranking result matches the `id` of either a search result item in an answer collection, *or* an entire answer collection (such as `Entities`).</span></span>
|`answerType`<br>`resultIndex`|<span data-ttu-id="3ed25-240">The `answerType` refers to the top-level answer collection that contains the result (for example, `Entities`).</span><span class="sxs-lookup"><span data-stu-id="3ed25-240">The `answerType` refers to the top-level answer collection that contains the result (for example, `Entities`).</span></span> <span data-ttu-id="3ed25-241">The `resultIndex` refers to the result's index within that collection.</span><span class="sxs-lookup"><span data-stu-id="3ed25-241">The `resultIndex` refers to the result's index within that collection.</span></span> <span data-ttu-id="3ed25-242">If `resultIndex` is omitted, the ranking result refers to the entire collection.</span><span class="sxs-lookup"><span data-stu-id="3ed25-242">If `resultIndex` is omitted, the ranking result refers to the entire collection.</span></span>

> [!NOTE]
> <span data-ttu-id="3ed25-243">For more information on this part of the search response, see [Rank Results](rank-results.md).</span><span class="sxs-lookup"><span data-stu-id="3ed25-243">For more information on this part of the search response, see [Rank Results](rank-results.md).</span></span>

<span data-ttu-id="3ed25-244">You may use whichever method of locating the referenced search result item is most convenient for your application.</span><span class="sxs-lookup"><span data-stu-id="3ed25-244">You may use whichever method of locating the referenced search result item is most convenient for your application.</span></span> <span data-ttu-id="3ed25-245">In our tutorial code, we use the `answerType` and `resultIndex` to locate each search result.</span><span class="sxs-lookup"><span data-stu-id="3ed25-245">In our tutorial code, we use the `answerType` and `resultIndex` to locate each search result.</span></span>

<span data-ttu-id="3ed25-246">Finally, it's time to look at our function `renderSearchResults()`.</span><span class="sxs-lookup"><span data-stu-id="3ed25-246">Finally, it's time to look at our function `renderSearchResults()`.</span></span> <span data-ttu-id="3ed25-247">This function iterates over the three `rankingResponse` collections that represent the three sections of the search results.</span><span class="sxs-lookup"><span data-stu-id="3ed25-247">This function iterates over the three `rankingResponse` collections that represent the three sections of the search results.</span></span> <span data-ttu-id="3ed25-248">For each section, we call `renderResultsItems()` to render the results for that section.</span><span class="sxs-lookup"><span data-stu-id="3ed25-248">For each section, we call `renderResultsItems()` to render the results for that section.</span></span>

```javascript
// render the search results given the parsed JSON response
function renderSearchResults(results) {

    // if spelling was corrected, update search field
    if (results.queryContext.alteredQuery) 
        document.forms.bing.query.value = results.queryContext.alteredQuery;

    // for each possible section, render the resuts from that section
    for (section in {pole: 0, mainline: 0, sidebar: 0}) {
        if (results.rankingResponse[section])
            showDiv(section, renderResultsItems(section, results));
    }
}
```

## <a name="rendering-result-items"></a><span data-ttu-id="3ed25-249">Rendering result items</span><span class="sxs-lookup"><span data-stu-id="3ed25-249">Rendering result items</span></span>

<span data-ttu-id="3ed25-250">In our JavaScript code is an object, `searchItemRenderers`, that contains *renderers:* functions that generate HTML for each kind of search result.</span><span class="sxs-lookup"><span data-stu-id="3ed25-250">In our JavaScript code is an object, `searchItemRenderers`, that contains *renderers:* functions that generate HTML for each kind of search result.</span></span>

```javascript
searchItemRenderers = { 
    entities: function(item) { ... },
    places: function(item) { ... }
}
```

<span data-ttu-id="3ed25-251">A renderer function may accept the following parameters:</span><span class="sxs-lookup"><span data-stu-id="3ed25-251">A renderer function may accept the following parameters:</span></span>

| | |
|-|-|
|`item`|<span data-ttu-id="3ed25-252">The JavaScript object containing the item's properties, such as its URL and its description.</span><span class="sxs-lookup"><span data-stu-id="3ed25-252">The JavaScript object containing the item's properties, such as its URL and its description.</span></span>|
|`index`|<span data-ttu-id="3ed25-253">The index of the result item within its collection.</span><span class="sxs-lookup"><span data-stu-id="3ed25-253">The index of the result item within its collection.</span></span>|
|`count`|<span data-ttu-id="3ed25-254">The number of items in the search result item's collection.</span><span class="sxs-lookup"><span data-stu-id="3ed25-254">The number of items in the search result item's collection.</span></span>|

<span data-ttu-id="3ed25-255">The `index` and `count` parameters can be used to number results, to generate special HTML for the beginning or end of a collection, to insert line breaks after a certain number of items, and so on.</span><span class="sxs-lookup"><span data-stu-id="3ed25-255">The `index` and `count` parameters can be used to number results, to generate special HTML for the beginning or end of a collection, to insert line breaks after a certain number of items, and so on.</span></span> <span data-ttu-id="3ed25-256">If a renderer does not need this functionality, it does not need to accept these two parameters.</span><span class="sxs-lookup"><span data-stu-id="3ed25-256">If a renderer does not need this functionality, it does not need to accept these two parameters.</span></span> <span data-ttu-id="3ed25-257">In fact, we do not use them in the renderers for our tutorial app.</span><span class="sxs-lookup"><span data-stu-id="3ed25-257">In fact, we do not use them in the renderers for our tutorial app.</span></span>

<span data-ttu-id="3ed25-258">Let's take a closer look at the `entities` renderer:</span><span class="sxs-lookup"><span data-stu-id="3ed25-258">Let's take a closer look at the `entities` renderer:</span></span>

```javascript
    entities: function(item) {
        var html = [];
        html.push("<p class='entity'>");
        if (item.image) {
            var img = item.image;
            if (img.hostPageUrl) html.push("<a href='" + img.hostPageUrl + "'>");
            html.push("<img src='" + img.thumbnailUrl +  "' title='" + img.name + "' height=" + img.height + " width= " + img.width + ">");
            if (img.hostPageUrl) html.push("</a>");
            if (img.provider) {
                var provider = img.provider[0];
                html.push("<small>Image from ");
                if (provider.url) html.push("<a href='" + provider.url + "'>");
                html.push(provider.name ? provider.name : getHost(provider.url));
                if (provider.url) html.push("</a>");
                html.push("</small>");
            }
        }
        html.push("<p>");
        if (item.entityPresentationInfo) {
            var pi = item.entityPresentationInfo;
            if (pi.entityTypeHints || pi.entityTypeDisplayHint) {
                html.push("<i>");
                if (pi.entityTypeDisplayHint) html.push(pi.entityTypeDisplayHint);
                else if (pi.entityTypeHints) html.push(pi.entityTypeHints.join("/"));
                html.push("</i> - ");
            }
        }
        html.push(item.description);
        if (item.webSearchUrl) html.push("&nbsp;<a href='" + item.webSearchUrl + "'>More</a>")
        if (item.contractualRules) {
            html.push("<p><small>");
            var rules = [];
            for (var i = 0; i < item.contractualRules.length; i++) {
                var rule = item.contractualRules[i];
                var link = [];
                if (rule.license) rule = rule.license;
                if (rule.url) link.push("<a href='" + rule.url + "'>");
                link.push(rule.name || rule.text || rule.targetPropertyName + " source");
                if (rule.url) link.push("</a>");
                rules.push(link.join(""));
            }
            html.push("License: " + rules.join(" - "));
            html.push("</small>");
        }
        return html.join("");
    }, // places renderer omitted
```

<span data-ttu-id="3ed25-259">Our entity renderer function:</span><span class="sxs-lookup"><span data-stu-id="3ed25-259">Our entity renderer function:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3ed25-260">Builds the HTML `<img>` tag to display the image thumbnail, if any.</span><span class="sxs-lookup"><span data-stu-id="3ed25-260">Builds the HTML `<img>` tag to display the image thumbnail, if any.</span></span> 
> * <span data-ttu-id="3ed25-261">Builds the HTML `<a>` tag that links to the page that contains the image.</span><span class="sxs-lookup"><span data-stu-id="3ed25-261">Builds the HTML `<a>` tag that links to the page that contains the image.</span></span>
> * <span data-ttu-id="3ed25-262">Builds the description that displays information about the image and the site it's on.</span><span class="sxs-lookup"><span data-stu-id="3ed25-262">Builds the description that displays information about the image and the site it's on.</span></span>
> * <span data-ttu-id="3ed25-263">Incorporates the entity's classification using the display hints, if any.</span><span class="sxs-lookup"><span data-stu-id="3ed25-263">Incorporates the entity's classification using the display hints, if any.</span></span>
> * <span data-ttu-id="3ed25-264">Includes a link to a Bing search to get more information about the entity.</span><span class="sxs-lookup"><span data-stu-id="3ed25-264">Includes a link to a Bing search to get more information about the entity.</span></span>
> * <span data-ttu-id="3ed25-265">Displays any licensing or attribution information required by data sources.</span><span class="sxs-lookup"><span data-stu-id="3ed25-265">Displays any licensing or attribution information required by data sources.</span></span>

## <a name="persisting-client-id"></a><span data-ttu-id="3ed25-266">Persisting client ID</span><span class="sxs-lookup"><span data-stu-id="3ed25-266">Persisting client ID</span></span>

<span data-ttu-id="3ed25-267">Responses from the Bing search APIs may include a `X-MSEdge-ClientID` header that should be sent back to the API with successive requests.</span><span class="sxs-lookup"><span data-stu-id="3ed25-267">Responses from the Bing search APIs may include a `X-MSEdge-ClientID` header that should be sent back to the API with successive requests.</span></span> <span data-ttu-id="3ed25-268">If multiple Bing Search APIs are being used, the same client ID should be used with all of them, if possible.</span><span class="sxs-lookup"><span data-stu-id="3ed25-268">If multiple Bing Search APIs are being used, the same client ID should be used with all of them, if possible.</span></span>

<span data-ttu-id="3ed25-269">Providing the `X-MSEdge-ClientID` header allows the Bing APIs to associate all of a user's searches, which has two important benefits.</span><span class="sxs-lookup"><span data-stu-id="3ed25-269">Providing the `X-MSEdge-ClientID` header allows the Bing APIs to associate all of a user's searches, which has two important benefits.</span></span>

<span data-ttu-id="3ed25-270">First, it allows the Bing search engine to apply past context to searches to find results that better satisfy the user.</span><span class="sxs-lookup"><span data-stu-id="3ed25-270">First, it allows the Bing search engine to apply past context to searches to find results that better satisfy the user.</span></span> <span data-ttu-id="3ed25-271">If a user has previously searched for terms related to sailing, for example, a later search for "docks" might preferentially return information about places to dock a sailboat.</span><span class="sxs-lookup"><span data-stu-id="3ed25-271">If a user has previously searched for terms related to sailing, for example, a later search for "docks" might preferentially return information about places to dock a sailboat.</span></span>

<span data-ttu-id="3ed25-272">Second, Bing may randomly select users to experience new features before they are made widely available.</span><span class="sxs-lookup"><span data-stu-id="3ed25-272">Second, Bing may randomly select users to experience new features before they are made widely available.</span></span> <span data-ttu-id="3ed25-273">Providing the same client ID with each request ensures that users that have been chosen to see a feature always see it.</span><span class="sxs-lookup"><span data-stu-id="3ed25-273">Providing the same client ID with each request ensures that users that have been chosen to see a feature always see it.</span></span> <span data-ttu-id="3ed25-274">Without the client ID, the user might see a feature appear and disappear, seemingly at random, in their search results.</span><span class="sxs-lookup"><span data-stu-id="3ed25-274">Without the client ID, the user might see a feature appear and disappear, seemingly at random, in their search results.</span></span>

<span data-ttu-id="3ed25-275">Browser security policies (CORS) may prevent the `X-MSEdge-ClientID` header from being available to JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3ed25-275">Browser security policies (CORS) may prevent the `X-MSEdge-ClientID` header from being available to JavaScript.</span></span> <span data-ttu-id="3ed25-276">This limitation occurs when the search response has a different origin from the page that requested it.</span><span class="sxs-lookup"><span data-stu-id="3ed25-276">This limitation occurs when the search response has a different origin from the page that requested it.</span></span> <span data-ttu-id="3ed25-277">In a production environment, you should address this policy by hosting a server-side script that does the API call on the same domain as the Web page.</span><span class="sxs-lookup"><span data-stu-id="3ed25-277">In a production environment, you should address this policy by hosting a server-side script that does the API call on the same domain as the Web page.</span></span> <span data-ttu-id="3ed25-278">Since the script has the same origin as the Web page, the `X-MSEdge-ClientID` header is then available to JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3ed25-278">Since the script has the same origin as the Web page, the `X-MSEdge-ClientID` header is then available to JavaScript.</span></span>

> [!NOTE]
> <span data-ttu-id="3ed25-279">In a production Web application, you should perform the request server-side anyway.</span><span class="sxs-lookup"><span data-stu-id="3ed25-279">In a production Web application, you should perform the request server-side anyway.</span></span> <span data-ttu-id="3ed25-280">Otherwise, your Bing Search API key must be included in the Web page, where it is available to anyone who views source.</span><span class="sxs-lookup"><span data-stu-id="3ed25-280">Otherwise, your Bing Search API key must be included in the Web page, where it is available to anyone who views source.</span></span> <span data-ttu-id="3ed25-281">You are billed for all usage under your API subscription key, even requests made by unauthorized parties, so it is important not to expose your key.</span><span class="sxs-lookup"><span data-stu-id="3ed25-281">You are billed for all usage under your API subscription key, even requests made by unauthorized parties, so it is important not to expose your key.</span></span>

<span data-ttu-id="3ed25-282">For development purposes, you can make the Bing Web Search API request through a CORS proxy.</span><span class="sxs-lookup"><span data-stu-id="3ed25-282">For development purposes, you can make the Bing Web Search API request through a CORS proxy.</span></span> <span data-ttu-id="3ed25-283">The response from such a proxy has an `Access-Control-Expose-Headers` header that whitelists response headers and makes them available to JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3ed25-283">The response from such a proxy has an `Access-Control-Expose-Headers` header that whitelists response headers and makes them available to JavaScript.</span></span>

<span data-ttu-id="3ed25-284">It's easy to install a CORS proxy to allow our tutorial app to access the client ID header.</span><span class="sxs-lookup"><span data-stu-id="3ed25-284">It's easy to install a CORS proxy to allow our tutorial app to access the client ID header.</span></span> <span data-ttu-id="3ed25-285">First, if you don't already have it, [install Node.js](https://nodejs.org/en/download/).</span><span class="sxs-lookup"><span data-stu-id="3ed25-285">First, if you don't already have it, [install Node.js](https://nodejs.org/en/download/).</span></span> <span data-ttu-id="3ed25-286">Then issue the following command in a command window:</span><span class="sxs-lookup"><span data-stu-id="3ed25-286">Then issue the following command in a command window:</span></span>

    npm install -g cors-proxy-server

<span data-ttu-id="3ed25-287">Next, change the Bing Web Search endpoint in the HTML file to:</span><span class="sxs-lookup"><span data-stu-id="3ed25-287">Next, change the Bing Web Search endpoint in the HTML file to:</span></span>

    http://localhost:9090/https://api.cognitive.microsoft.com/bing/v7.0/search

<span data-ttu-id="3ed25-288">Finally, start the CORS proxy with the following command:</span><span class="sxs-lookup"><span data-stu-id="3ed25-288">Finally, start the CORS proxy with the following command:</span></span>

    cors-proxy-server

<span data-ttu-id="3ed25-289">Leave the command window open while you use the tutorial app; closing the window stops the proxy.</span><span class="sxs-lookup"><span data-stu-id="3ed25-289">Leave the command window open while you use the tutorial app; closing the window stops the proxy.</span></span> <span data-ttu-id="3ed25-290">In the expandable HTTP Headers section below the search results, you can now see the `X-MSEdge-ClientID` header (among others) and verify that it is the same for each request.</span><span class="sxs-lookup"><span data-stu-id="3ed25-290">In the expandable HTTP Headers section below the search results, you can now see the `X-MSEdge-ClientID` header (among others) and verify that it is the same for each request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ed25-291">Next steps</span><span class="sxs-lookup"><span data-stu-id="3ed25-291">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3ed25-292">Bing Entity Search API reference</span><span class="sxs-lookup"><span data-stu-id="3ed25-292">Bing Entity Search API reference</span></span>](//docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference)

> [!div class="nextstepaction"]
> [<span data-ttu-id="3ed25-293">Bing Maps API documentation</span><span class="sxs-lookup"><span data-stu-id="3ed25-293">Bing Maps API documentation</span></span>](//msdn.microsoft.com/library/dd877180.aspx)
