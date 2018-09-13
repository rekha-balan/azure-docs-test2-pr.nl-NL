---
title: Bing Image Search single-page Web app | Microsoft Docs
description: Shows how to use the Bing Image Search API in a single-page Web application.
services: cognitive-services
author: v-jerkin
manager: ehansen
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: article
ms.date: 10/04/2017
ms.author: v-jerkin
ms.openlocfilehash: d0e1dc24513c8fc3a405cf1c18f531a0c58fad13
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966871"
---
# <a name="tutorial-single-page-web-app"></a><span data-ttu-id="46578-103">Tutorial: Single-page Web app</span><span class="sxs-lookup"><span data-stu-id="46578-103">Tutorial: Single-page Web app</span></span>

<span data-ttu-id="46578-104">The Bing Image Search API lets you search the Web and obtain image results relevant to the search query.</span><span class="sxs-lookup"><span data-stu-id="46578-104">The Bing Image Search API lets you search the Web and obtain image results relevant to the search query.</span></span> <span data-ttu-id="46578-105">In this tutorial, we build a single-page Web application that uses the Bing Image Search API to display search results right in the page.</span><span class="sxs-lookup"><span data-stu-id="46578-105">In this tutorial, we build a single-page Web application that uses the Bing Image Search API to display search results right in the page.</span></span> <span data-ttu-id="46578-106">The application includes HTML, CSS, and JavaScript components.</span><span class="sxs-lookup"><span data-stu-id="46578-106">The application includes HTML, CSS, and JavaScript components.</span></span>

<!-- Remove until we can sanitize images
![[Single-page Bing Image Search app]](media/cognitive-services-bing-images-api/image-search-spa-demo.png)
-->

> [!NOTE]
> <span data-ttu-id="46578-107">The JSON and HTTP headings at the bottom of the page reveal the JSON response and HTTP request information when clicked.</span><span class="sxs-lookup"><span data-stu-id="46578-107">The JSON and HTTP headings at the bottom of the page reveal the JSON response and HTTP request information when clicked.</span></span> <span data-ttu-id="46578-108">These details are useful when exploring the service.</span><span class="sxs-lookup"><span data-stu-id="46578-108">These details are useful when exploring the service.</span></span>

<span data-ttu-id="46578-109">The tutorial app illustrates how to:</span><span class="sxs-lookup"><span data-stu-id="46578-109">The tutorial app illustrates how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="46578-110">Perform a Bing Image Search API call in JavaScript</span><span class="sxs-lookup"><span data-stu-id="46578-110">Perform a Bing Image Search API call in JavaScript</span></span>
> * <span data-ttu-id="46578-111">Pass search options to the Bing Image Search API</span><span class="sxs-lookup"><span data-stu-id="46578-111">Pass search options to the Bing Image Search API</span></span>
> * <span data-ttu-id="46578-112">Display search results</span><span class="sxs-lookup"><span data-stu-id="46578-112">Display search results</span></span>
> * <span data-ttu-id="46578-113">Page through search results</span><span class="sxs-lookup"><span data-stu-id="46578-113">Page through search results</span></span>
> * <span data-ttu-id="46578-114">Handle the Bing client ID and API subscription key</span><span class="sxs-lookup"><span data-stu-id="46578-114">Handle the Bing client ID and API subscription key</span></span>
> * <span data-ttu-id="46578-115">Handle errors that might occur</span><span class="sxs-lookup"><span data-stu-id="46578-115">Handle errors that might occur</span></span>

<span data-ttu-id="46578-116">The tutorial page is entirely self-contained; it does not use any external frameworks, style sheets, or even image files.</span><span class="sxs-lookup"><span data-stu-id="46578-116">The tutorial page is entirely self-contained; it does not use any external frameworks, style sheets, or even image files.</span></span> <span data-ttu-id="46578-117">It uses only widely supported JavaScript language features and works with current versions of all major Web browsers.</span><span class="sxs-lookup"><span data-stu-id="46578-117">It uses only widely supported JavaScript language features and works with current versions of all major Web browsers.</span></span>

<span data-ttu-id="46578-118">In this tutorial, we discuss only selected portions of the source code.</span><span class="sxs-lookup"><span data-stu-id="46578-118">In this tutorial, we discuss only selected portions of the source code.</span></span> <span data-ttu-id="46578-119">The full source code is available [on a separate page](tutorial-bing-image-search-single-page-app-source.md).</span><span class="sxs-lookup"><span data-stu-id="46578-119">The full source code is available [on a separate page](tutorial-bing-image-search-single-page-app-source.md).</span></span> <span data-ttu-id="46578-120">Copy and paste this code into a text editor and save it as `bing.html`.</span><span class="sxs-lookup"><span data-stu-id="46578-120">Copy and paste this code into a text editor and save it as `bing.html`.</span></span>

> [!NOTE]
> <span data-ttu-id="46578-121">This tutorial is substantially similar to the [single-page Bing Web Search app tutorial](../Bing-Web-Search/tutorial-bing-web-search-single-page-app.md), but deals only with image search results.</span><span class="sxs-lookup"><span data-stu-id="46578-121">This tutorial is substantially similar to the [single-page Bing Web Search app tutorial](../Bing-Web-Search/tutorial-bing-web-search-single-page-app.md), but deals only with image search results.</span></span>

## <a name="app-components"></a><span data-ttu-id="46578-122">App components</span><span class="sxs-lookup"><span data-stu-id="46578-122">App components</span></span>

<span data-ttu-id="46578-123">Like any single-page Web app, the tutorial application includes three parts:</span><span class="sxs-lookup"><span data-stu-id="46578-123">Like any single-page Web app, the tutorial application includes three parts:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="46578-124">HTML - Defines the structure and content of the page</span><span class="sxs-lookup"><span data-stu-id="46578-124">HTML - Defines the structure and content of the page</span></span>
> * <span data-ttu-id="46578-125">CSS - Defines the appearance of the page</span><span class="sxs-lookup"><span data-stu-id="46578-125">CSS - Defines the appearance of the page</span></span>
> * <span data-ttu-id="46578-126">JavaScript - Defines the behavior of the page</span><span class="sxs-lookup"><span data-stu-id="46578-126">JavaScript - Defines the behavior of the page</span></span>

<span data-ttu-id="46578-127">This tutorial doesn't cover most of the HTML or CSS in detail, as they are straightforward.</span><span class="sxs-lookup"><span data-stu-id="46578-127">This tutorial doesn't cover most of the HTML or CSS in detail, as they are straightforward.</span></span>

<span data-ttu-id="46578-128">The HTML contains the search form in which the user enters a query and chooses search options.</span><span class="sxs-lookup"><span data-stu-id="46578-128">The HTML contains the search form in which the user enters a query and chooses search options.</span></span> <span data-ttu-id="46578-129">The form is connected to the JavaScript that actually performs the search by the `<form>` tag's `onsubmit` attribute:</span><span class="sxs-lookup"><span data-stu-id="46578-129">The form is connected to the JavaScript that actually performs the search by the `<form>` tag's `onsubmit` attribute:</span></span>

```html
<form name="bing" onsubmit="return newBingImageSearch(this)">
```

<span data-ttu-id="46578-130">The `onsubmit` handler returns `false`, which keeps the form from being submitted to a server.</span><span class="sxs-lookup"><span data-stu-id="46578-130">The `onsubmit` handler returns `false`, which keeps the form from being submitted to a server.</span></span> <span data-ttu-id="46578-131">The JavaScript code actually does the work of collecting the necessary information from the form and performing the search.</span><span class="sxs-lookup"><span data-stu-id="46578-131">The JavaScript code actually does the work of collecting the necessary information from the form and performing the search.</span></span>

<span data-ttu-id="46578-132">The HTML also contains the divisions (HTML `<div>` tags) where the search results appear.</span><span class="sxs-lookup"><span data-stu-id="46578-132">The HTML also contains the divisions (HTML `<div>` tags) where the search results appear.</span></span>

## <a name="managing-subscription-key"></a><span data-ttu-id="46578-133">Managing subscription key</span><span class="sxs-lookup"><span data-stu-id="46578-133">Managing subscription key</span></span>

<span data-ttu-id="46578-134">To avoid having to include the Bing Search API subscription key in the code, we use the browser's persistent storage to store the key.</span><span class="sxs-lookup"><span data-stu-id="46578-134">To avoid having to include the Bing Search API subscription key in the code, we use the browser's persistent storage to store the key.</span></span> <span data-ttu-id="46578-135">If no key is stored, we prompt for the user's key and store it for later use.</span><span class="sxs-lookup"><span data-stu-id="46578-135">If no key is stored, we prompt for the user's key and store it for later use.</span></span> <span data-ttu-id="46578-136">If the key is later rejected by the API, we invalidate the stored key so the user is again.</span><span class="sxs-lookup"><span data-stu-id="46578-136">If the key is later rejected by the API, we invalidate the stored key so the user is again.</span></span>

<span data-ttu-id="46578-137">We define `storeValue` and `retrieveValue` functions that use either the `localStorage` object (if the browser supports it) or a cookie.</span><span class="sxs-lookup"><span data-stu-id="46578-137">We define `storeValue` and `retrieveValue` functions that use either the `localStorage` object (if the browser supports it) or a cookie.</span></span> <span data-ttu-id="46578-138">Our `getSubscriptionKey()` function uses these functions to store and retrieve the user's key.</span><span class="sxs-lookup"><span data-stu-id="46578-138">Our `getSubscriptionKey()` function uses these functions to store and retrieve the user's key.</span></span>

```javascript
// cookie names for data we store
API_KEY_COOKIE   = "bing-search-api-key";
CLIENT_ID_COOKIE = "bing-search-client-id";

BING_ENDPOINT = "https://api.cognitive.microsoft.com/bing/v7.0/images/search";

// ... omitted definitions of storeValue() and retrieveValue()

// get stored API subscription key, or prompt if it's not found
function getSubscriptionKey() {
    var key = retrieveValue(API_KEY_COOKIE);
    while (key.length !== 32) {
        key = prompt("Enter Bing Search API subscription key:", "").trim();
    }
    // always set the cookie in order to update the expiration date
    storeValue(API_KEY_COOKIE, key);
    return key;
}
```

<span data-ttu-id="46578-139">The HTML `<form>` tag `onsubmit` calls the `bingWebSearch` function to return search results.</span><span class="sxs-lookup"><span data-stu-id="46578-139">The HTML `<form>` tag `onsubmit` calls the `bingWebSearch` function to return search results.</span></span> <span data-ttu-id="46578-140">`bingWebSearch` uses `getSubscriptionKey` to authenticate each query.</span><span class="sxs-lookup"><span data-stu-id="46578-140">`bingWebSearch` uses `getSubscriptionKey` to authenticate each query.</span></span> <span data-ttu-id="46578-141">As shown in the previous definition, `getSubscriptionKey` prompts the user for the key if the key hasn't been entered.</span><span class="sxs-lookup"><span data-stu-id="46578-141">As shown in the previous definition, `getSubscriptionKey` prompts the user for the key if the key hasn't been entered.</span></span> <span data-ttu-id="46578-142">The key is then stored for continuing use by the application.</span><span class="sxs-lookup"><span data-stu-id="46578-142">The key is then stored for continuing use by the application.</span></span>

```html
<form name="bing" onsubmit="this.offset.value = 0; return bingWebSearch(this.query.value, 
    bingSearchOptions(this), getSubscriptionKey())">
```

## <a name="selecting-search-options"></a><span data-ttu-id="46578-143">Selecting search options</span><span class="sxs-lookup"><span data-stu-id="46578-143">Selecting search options</span></span>

![[Bing Image Search form]](media/cognitive-services-bing-images-api/image-search-spa-form.png)

<span data-ttu-id="46578-145">The HTML form includes the following controls:</span><span class="sxs-lookup"><span data-stu-id="46578-145">The HTML form includes the following controls:</span></span>

| | |
|-|-|
|`where`|<span data-ttu-id="46578-146">A drop-down menu for selecting the market (location and language) used for the search.</span><span class="sxs-lookup"><span data-stu-id="46578-146">A drop-down menu for selecting the market (location and language) used for the search.</span></span>|
|`query`|<span data-ttu-id="46578-147">The text field in which to enter the search terms.</span><span class="sxs-lookup"><span data-stu-id="46578-147">The text field in which to enter the search terms.</span></span>|
|`aspect`|<span data-ttu-id="46578-148">Radio buttons for choosing the proportions of the found images: roughly square, wide, or tall.</span><span class="sxs-lookup"><span data-stu-id="46578-148">Radio buttons for choosing the proportions of the found images: roughly square, wide, or tall.</span></span>|
|`color`|<span data-ttu-id="46578-149">Selects color or black-and-white, or a predominant color.</span><span class="sxs-lookup"><span data-stu-id="46578-149">Selects color or black-and-white, or a predominant color.</span></span>
|`when`|<span data-ttu-id="46578-150">Drop-down menu for optionally limiting the search to the most recent day, week, or month.</span><span class="sxs-lookup"><span data-stu-id="46578-150">Drop-down menu for optionally limiting the search to the most recent day, week, or month.</span></span>|
|`safe`|<span data-ttu-id="46578-151">A checkbox indicating whether to use Bing's SafeSearch feature to filter out "adult" results.</span><span class="sxs-lookup"><span data-stu-id="46578-151">A checkbox indicating whether to use Bing's SafeSearch feature to filter out "adult" results.</span></span>|
|`count`|<span data-ttu-id="46578-152">Hidden field.</span><span class="sxs-lookup"><span data-stu-id="46578-152">Hidden field.</span></span> <span data-ttu-id="46578-153">The number of search results to return on each request.</span><span class="sxs-lookup"><span data-stu-id="46578-153">The number of search results to return on each request.</span></span> <span data-ttu-id="46578-154">Change to display fewer or more results per page.</span><span class="sxs-lookup"><span data-stu-id="46578-154">Change to display fewer or more results per page.</span></span>|
|`offset`|<span data-ttu-id="46578-155">Hidden field.</span><span class="sxs-lookup"><span data-stu-id="46578-155">Hidden field.</span></span> <span data-ttu-id="46578-156">The offset of the first search result in the request; used for paging.</span><span class="sxs-lookup"><span data-stu-id="46578-156">The offset of the first search result in the request; used for paging.</span></span> <span data-ttu-id="46578-157">It's reset to `0` on a new request.</span><span class="sxs-lookup"><span data-stu-id="46578-157">It's reset to `0` on a new request.</span></span>|
|`nextoffset`|<span data-ttu-id="46578-158">Hidden field.</span><span class="sxs-lookup"><span data-stu-id="46578-158">Hidden field.</span></span> <span data-ttu-id="46578-159">Upon receiving a search result, this field is set to the value of the `nextOffset` in the response.</span><span class="sxs-lookup"><span data-stu-id="46578-159">Upon receiving a search result, this field is set to the value of the `nextOffset` in the response.</span></span> <span data-ttu-id="46578-160">Using this field avoids overlapping results on successive pages.</span><span class="sxs-lookup"><span data-stu-id="46578-160">Using this field avoids overlapping results on successive pages.</span></span>|
|`stack`|<span data-ttu-id="46578-161">Hidden field.</span><span class="sxs-lookup"><span data-stu-id="46578-161">Hidden field.</span></span> <span data-ttu-id="46578-162">A JSON-encoded list of the offsets of preceding pages of search results, for navigating back to previous pages.</span><span class="sxs-lookup"><span data-stu-id="46578-162">A JSON-encoded list of the offsets of preceding pages of search results, for navigating back to previous pages.</span></span>|

> [!NOTE]
> <span data-ttu-id="46578-163">Bing Image Search offers many more query parameters.</span><span class="sxs-lookup"><span data-stu-id="46578-163">Bing Image Search offers many more query parameters.</span></span> <span data-ttu-id="46578-164">We're using only a few of them here.</span><span class="sxs-lookup"><span data-stu-id="46578-164">We're using only a few of them here.</span></span>

<span data-ttu-id="46578-165">Our JavaScript function `bingSearchOptions()` converts these fields to a partial query string in the format required by the Bing Search API.</span><span class="sxs-lookup"><span data-stu-id="46578-165">Our JavaScript function `bingSearchOptions()` converts these fields to a partial query string in the format required by the Bing Search API.</span></span>

```javascript
// build query options from the HTML form
function bingSearchOptions(form) {

    var options = [];
    options.push("mkt=" + form.where.value);
    options.push("SafeSearch=" + (form.safe.checked ? "strict" : "off"));
    if (form.when.value.length) options.push("freshness=" + form.when.value);
    var aspect = "all";
    for (var i = 0; i < form.aspect.length; i++) {
        if (form.aspect[i].checked) {
            aspect = form.aspect[i].value;
            break;
        }
    }
    options.push("aspect=" + aspect);
    if (form.color.value) options.push("color=" + form.color.value);
    options.push("count=" + form.count.value);
    options.push("offset=" + form.offset.value);
    return options.join("&");
}
```

<span data-ttu-id="46578-166">For example, the SafeSearch feature can be `strict`, `moderate`, or `off`, with `moderate` being the default.</span><span class="sxs-lookup"><span data-stu-id="46578-166">For example, the SafeSearch feature can be `strict`, `moderate`, or `off`, with `moderate` being the default.</span></span> <span data-ttu-id="46578-167">But our form uses a checkbox, which has only two states.</span><span class="sxs-lookup"><span data-stu-id="46578-167">But our form uses a checkbox, which has only two states.</span></span> <span data-ttu-id="46578-168">The JavaScript code converts this setting to either `strict` or `off` (we don't use `moderate`).</span><span class="sxs-lookup"><span data-stu-id="46578-168">The JavaScript code converts this setting to either `strict` or `off` (we don't use `moderate`).</span></span>

## <a name="performing-the-request"></a><span data-ttu-id="46578-169">Performing the request</span><span class="sxs-lookup"><span data-stu-id="46578-169">Performing the request</span></span>

<span data-ttu-id="46578-170">Given the query, the options string, and the API key, the `BingImageSearch` function uses an `XMLHttpRequest` object to make the request to the Bing Image Search endpoint.</span><span class="sxs-lookup"><span data-stu-id="46578-170">Given the query, the options string, and the API key, the `BingImageSearch` function uses an `XMLHttpRequest` object to make the request to the Bing Image Search endpoint.</span></span>

```javascript
// perform a search given query, options string, and API key
function bingImageSearch(query, options, key) {

    // scroll to top of window
    window.scrollTo(0, 0);
    if (!query.trim().length) return false;     // empty query, do nothing

    showDiv("noresults", "Working. Please wait.");
    hideDivs("results", "related", "_json", "_http", "paging1", "paging2", "error");

    var request = new XMLHttpRequest();
    var queryurl = BING_ENDPOINT + "?q=" + encodeURIComponent(query) + "&" + options;

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

<span data-ttu-id="46578-171">Upon successful completion of the HTTP request, JavaScript calls our `load` event handler, the `handleBingResponse()` function, to handle a successful HTTP GET request to the API.</span><span class="sxs-lookup"><span data-stu-id="46578-171">Upon successful completion of the HTTP request, JavaScript calls our `load` event handler, the `handleBingResponse()` function, to handle a successful HTTP GET request to the API.</span></span> 

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
            if (jsobj._type === "Images") {
                if (jsobj.nextOffset) document.forms.bing.nextoffset.value = jsobj.nextOffset;
                renderSearchResults(jsobj);
            } else {
                renderErrorMessage("No search results in JSON response");
            }
        } else {
            renderErrorMessage("Empty response (are you sending too many requests too quickly?)");
        }
    }

    // Any other HTTP response is an error
    else {
        // 401 is unauthorized; force re-prompt for API key for next request
        if (this.status === 401) invalidateSubscriptionKey();

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
> <span data-ttu-id="46578-172">A successful HTTP request does *not* necessarily mean that the search itself succeeded.</span><span class="sxs-lookup"><span data-stu-id="46578-172">A successful HTTP request does *not* necessarily mean that the search itself succeeded.</span></span> <span data-ttu-id="46578-173">If an error occurs in the search operation, the Bing Image Search API returns a non-200 HTTP status code and includes error information in the JSON response.</span><span class="sxs-lookup"><span data-stu-id="46578-173">If an error occurs in the search operation, the Bing Image Search API returns a non-200 HTTP status code and includes error information in the JSON response.</span></span> <span data-ttu-id="46578-174">Additionally, if the request was rate-limited, the API returns an empty response.</span><span class="sxs-lookup"><span data-stu-id="46578-174">Additionally, if the request was rate-limited, the API returns an empty response.</span></span>

<span data-ttu-id="46578-175">Much of the code in both of the preceding functions is dedicated to error handling.</span><span class="sxs-lookup"><span data-stu-id="46578-175">Much of the code in both of the preceding functions is dedicated to error handling.</span></span> <span data-ttu-id="46578-176">Errors may occur at the following stages:</span><span class="sxs-lookup"><span data-stu-id="46578-176">Errors may occur at the following stages:</span></span>

|<span data-ttu-id="46578-177">Stage</span><span class="sxs-lookup"><span data-stu-id="46578-177">Stage</span></span>|<span data-ttu-id="46578-178">Potential error(s)</span><span class="sxs-lookup"><span data-stu-id="46578-178">Potential error(s)</span></span>|<span data-ttu-id="46578-179">Handled by</span><span class="sxs-lookup"><span data-stu-id="46578-179">Handled by</span></span>|
|-|-|-|
|<span data-ttu-id="46578-180">Building JavaScript request object</span><span class="sxs-lookup"><span data-stu-id="46578-180">Building JavaScript request object</span></span>|<span data-ttu-id="46578-181">Invalid URL</span><span class="sxs-lookup"><span data-stu-id="46578-181">Invalid URL</span></span>|<span data-ttu-id="46578-182">`try`/`catch` block</span><span class="sxs-lookup"><span data-stu-id="46578-182">`try`/`catch` block</span></span>|
|<span data-ttu-id="46578-183">Making the request</span><span class="sxs-lookup"><span data-stu-id="46578-183">Making the request</span></span>|<span data-ttu-id="46578-184">Network errors, aborted connections</span><span class="sxs-lookup"><span data-stu-id="46578-184">Network errors, aborted connections</span></span>|<span data-ttu-id="46578-185">`error` and `abort` event handlers</span><span class="sxs-lookup"><span data-stu-id="46578-185">`error` and `abort` event handlers</span></span>|
|<span data-ttu-id="46578-186">Performing the search</span><span class="sxs-lookup"><span data-stu-id="46578-186">Performing the search</span></span>|<span data-ttu-id="46578-187">Invalid request, invalid JSON, rate limits</span><span class="sxs-lookup"><span data-stu-id="46578-187">Invalid request, invalid JSON, rate limits</span></span>|<span data-ttu-id="46578-188">tests in `load` event handler</span><span class="sxs-lookup"><span data-stu-id="46578-188">tests in `load` event handler</span></span>|

<span data-ttu-id="46578-189">Errors are handled by calling `renderErrorMessage()` with any details known about the error.</span><span class="sxs-lookup"><span data-stu-id="46578-189">Errors are handled by calling `renderErrorMessage()` with any details known about the error.</span></span> <span data-ttu-id="46578-190">If the response passes the full gauntlet of error tests, we call `renderSearchResults()` to display the search results in the page.</span><span class="sxs-lookup"><span data-stu-id="46578-190">If the response passes the full gauntlet of error tests, we call `renderSearchResults()` to display the search results in the page.</span></span>

## <a name="displaying-search-results"></a><span data-ttu-id="46578-191">Displaying search results</span><span class="sxs-lookup"><span data-stu-id="46578-191">Displaying search results</span></span>

<span data-ttu-id="46578-192">The main function for displaying the search results is `renderSearchResults()`.</span><span class="sxs-lookup"><span data-stu-id="46578-192">The main function for displaying the search results is `renderSearchResults()`.</span></span> <span data-ttu-id="46578-193">This function takes the JSON returned by the Bing Image Search service and renders the images and the related searches, if any.</span><span class="sxs-lookup"><span data-stu-id="46578-193">This function takes the JSON returned by the Bing Image Search service and renders the images and the related searches, if any.</span></span>

```javascript
function renderSearchResults(results) {

    // add Prev / Next links with result count
    var pagingLinks = renderPagingLinks(results);
    showDiv("paging1", pagingLinks);
    showDiv("paging2", pagingLinks);
    
    showDiv("results", renderImageResults(results.value));
    if (results.relatedSearches)
        showDiv("sidebar", renderRelatedItems(results.relatedSearches));
}
```

<span data-ttu-id="46578-194">The main image search results are returned as the top-level `value` object in the JSON response.</span><span class="sxs-lookup"><span data-stu-id="46578-194">The main image search results are returned as the top-level `value` object in the JSON response.</span></span> <span data-ttu-id="46578-195">We pass them to our function `renderImageResults()`, which iterates through them and calls a separate function to render each item into HTML.</span><span class="sxs-lookup"><span data-stu-id="46578-195">We pass them to our function `renderImageResults()`, which iterates through them and calls a separate function to render each item into HTML.</span></span> <span data-ttu-id="46578-196">The resulting HTML is returned to `renderSearchResults()`, where it is inserted into the `results` division in the page.</span><span class="sxs-lookup"><span data-stu-id="46578-196">The resulting HTML is returned to `renderSearchResults()`, where it is inserted into the `results` division in the page.</span></span>

```javascript
function renderImageResults(items) {
    var len = items.length;
    var html = [];
    if (!len) {
        showDiv("noresults", "No results.");
        hideDivs("paging1", "paging2");
        return "";
    }
    for (var i = 0; i < len; i++) {
        html.push(searchItemRenderers.images(items[i], i, len));
    }
    return html.join("\n\n");
}
```

<span data-ttu-id="46578-197">The Bing Image Search API returns up to four different kinds of related results, each in its own top-level object.</span><span class="sxs-lookup"><span data-stu-id="46578-197">The Bing Image Search API returns up to four different kinds of related results, each in its own top-level object.</span></span> <span data-ttu-id="46578-198">They are:</span><span class="sxs-lookup"><span data-stu-id="46578-198">They are:</span></span>

|||
|-|-|
|`pivotSuggestions`|<span data-ttu-id="46578-199">Queries that replace a pivot word in original search with a different one.</span><span class="sxs-lookup"><span data-stu-id="46578-199">Queries that replace a pivot word in original search with a different one.</span></span> <span data-ttu-id="46578-200">For example, if you search for "red flowers," a pivot word might be "red," and a pivot suggestion might be "yellow flowers."</span><span class="sxs-lookup"><span data-stu-id="46578-200">For example, if you search for "red flowers," a pivot word might be "red," and a pivot suggestion might be "yellow flowers."</span></span>|
|`queryExpansions`|<span data-ttu-id="46578-201">Queries that narrow the original search by adding more terms.</span><span class="sxs-lookup"><span data-stu-id="46578-201">Queries that narrow the original search by adding more terms.</span></span> <span data-ttu-id="46578-202">For example, if you search for "Microsoft Surface," a query expansion might be "Microsoft Surface Pro."</span><span class="sxs-lookup"><span data-stu-id="46578-202">For example, if you search for "Microsoft Surface," a query expansion might be "Microsoft Surface Pro."</span></span>|
|`relatedSearches`|<span data-ttu-id="46578-203">Queries that have also been entered by other users who entered the original search.</span><span class="sxs-lookup"><span data-stu-id="46578-203">Queries that have also been entered by other users who entered the original search.</span></span> <span data-ttu-id="46578-204">For example, if you search for "Mount Rainier," a related search might be "Mt.</span><span class="sxs-lookup"><span data-stu-id="46578-204">For example, if you search for "Mount Rainier," a related search might be "Mt.</span></span> <span data-ttu-id="46578-205">Saint Helens."</span><span class="sxs-lookup"><span data-stu-id="46578-205">Saint Helens."</span></span>|
|`similarTerms`|<span data-ttu-id="46578-206">Queries that are similar in meaning to the original search.</span><span class="sxs-lookup"><span data-stu-id="46578-206">Queries that are similar in meaning to the original search.</span></span> <span data-ttu-id="46578-207">For example, if you search for "kittens," a similar term might be "cute."</span><span class="sxs-lookup"><span data-stu-id="46578-207">For example, if you search for "kittens," a similar term might be "cute."</span></span>|

<span data-ttu-id="46578-208">As previously seen in `renderSearchResults()`, we render only the `relatedItems` suggestions and place the resulting links in the page's sidebar.</span><span class="sxs-lookup"><span data-stu-id="46578-208">As previously seen in `renderSearchResults()`, we render only the `relatedItems` suggestions and place the resulting links in the page's sidebar.</span></span>

## <a name="rendering-result-items"></a><span data-ttu-id="46578-209">Rendering result items</span><span class="sxs-lookup"><span data-stu-id="46578-209">Rendering result items</span></span>

<span data-ttu-id="46578-210">In our JavaScript code is an object, `searchItemRenderers`, that contains *renderers:* functions that generate HTML for each kind of search result.</span><span class="sxs-lookup"><span data-stu-id="46578-210">In our JavaScript code is an object, `searchItemRenderers`, that contains *renderers:* functions that generate HTML for each kind of search result.</span></span>

```javascript
searchItemRenderers = { 
    images: function(item, index, count) { ... },
    relatedSearches: function(item) { ... }
}
```

<span data-ttu-id="46578-211">A renderer function may accept the following parameters:</span><span class="sxs-lookup"><span data-stu-id="46578-211">A renderer function may accept the following parameters:</span></span>

| | |
|-|-|
|`item`|<span data-ttu-id="46578-212">The JavaScript object containing the item's properties, such as its URL and its description.</span><span class="sxs-lookup"><span data-stu-id="46578-212">The JavaScript object containing the item's properties, such as its URL and its description.</span></span>|
|`index`|<span data-ttu-id="46578-213">The index of the result item within its collection.</span><span class="sxs-lookup"><span data-stu-id="46578-213">The index of the result item within its collection.</span></span>|
|`count`|<span data-ttu-id="46578-214">The number of items in the search result item's collection.</span><span class="sxs-lookup"><span data-stu-id="46578-214">The number of items in the search result item's collection.</span></span>|

<span data-ttu-id="46578-215">The `index` and `count` parameters can be used to number results, to generate special HTML for the beginning or end of a collection, to insert line breaks after a certain number of items, and so on.</span><span class="sxs-lookup"><span data-stu-id="46578-215">The `index` and `count` parameters can be used to number results, to generate special HTML for the beginning or end of a collection, to insert line breaks after a certain number of items, and so on.</span></span> <span data-ttu-id="46578-216">If a renderer does not need this functionality, it does not need to accept these two parameters.</span><span class="sxs-lookup"><span data-stu-id="46578-216">If a renderer does not need this functionality, it does not need to accept these two parameters.</span></span>

<span data-ttu-id="46578-217">Let's take a closer look at the `images` renderer:</span><span class="sxs-lookup"><span data-stu-id="46578-217">Let's take a closer look at the `images` renderer:</span></span>

```javascript
    images: function (item, index, count) {
        var height = 120;
        var width = Math.max(Math.round(height * item.thumbnail.width / item.thumbnail.height), 120);
        var html = [];
        if (index === 0) html.push("<p class='images'>");
        var title = escape(item.name) + "\n" + getHost(item.hostPageDisplayUrl);
        html.push("<p class='images' style='max-width: " + width + "px'>");
        html.push("<img src='"+ item.thumbnailUrl + "&h=" + height + "&w=" + width + 
            "' height=" + height + " width=" + width + "'>");
        html.push("<br>");
        html.push("<nobr><a href='" + item.contentUrl + "'>Image</a> - ");
        html.push("<a href='" + item.hostPageUrl + "'>Page</a></nobr><br>");
        html.push(title.replace("\n", " (").replace(/([a-z0-9])\.([a-z0-9])/g, "$1.<wbr>$2") + ")</p>");
        return html.join("");
    }, // relatedSearches renderer omitted
```

<span data-ttu-id="46578-218">Our image renderer function:</span><span class="sxs-lookup"><span data-stu-id="46578-218">Our image renderer function:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="46578-219">Calculates the image thumbnail size (width varies, with a minimum of 120 pixels, while height is fixed at 90 pixels).</span><span class="sxs-lookup"><span data-stu-id="46578-219">Calculates the image thumbnail size (width varies, with a minimum of 120 pixels, while height is fixed at 90 pixels).</span></span>
> * <span data-ttu-id="46578-220">Builds the HTML `<img>` tag to display the image thumbnail.</span><span class="sxs-lookup"><span data-stu-id="46578-220">Builds the HTML `<img>` tag to display the image thumbnail.</span></span> 
> * <span data-ttu-id="46578-221">Builds the HTML `<a>` tags that link to the image and the page that contains it.</span><span class="sxs-lookup"><span data-stu-id="46578-221">Builds the HTML `<a>` tags that link to the image and the page that contains it.</span></span>
> * <span data-ttu-id="46578-222">Builds the description that displays information about the image and the site it's on.</span><span class="sxs-lookup"><span data-stu-id="46578-222">Builds the description that displays information about the image and the site it's on.</span></span>

<span data-ttu-id="46578-223">We test the `index` variable in order to insert a `<p>` tag before the first image result.</span><span class="sxs-lookup"><span data-stu-id="46578-223">We test the `index` variable in order to insert a `<p>` tag before the first image result.</span></span> <span data-ttu-id="46578-224">The thumbnails otherwise butt up against each other and wrap as needed in the browser window.</span><span class="sxs-lookup"><span data-stu-id="46578-224">The thumbnails otherwise butt up against each other and wrap as needed in the browser window.</span></span>

<span data-ttu-id="46578-225">The thumbnail size is used in both the `<img>` tag and the `h` and `w` fields in the thumbnail's URL.</span><span class="sxs-lookup"><span data-stu-id="46578-225">The thumbnail size is used in both the `<img>` tag and the `h` and `w` fields in the thumbnail's URL.</span></span> <span data-ttu-id="46578-226">The [Bing thumbnail service](resize-and-crop-thumbnails.md) then delivers a thumbnail of exactly that size.</span><span class="sxs-lookup"><span data-stu-id="46578-226">The [Bing thumbnail service](resize-and-crop-thumbnails.md) then delivers a thumbnail of exactly that size.</span></span>

## <a name="persisting-client-id"></a><span data-ttu-id="46578-227">Persisting client ID</span><span class="sxs-lookup"><span data-stu-id="46578-227">Persisting client ID</span></span>

<span data-ttu-id="46578-228">Responses from the Bing search APIs may include a `X-MSEdge-ClientID` header that should be sent back to the API with successive requests.</span><span class="sxs-lookup"><span data-stu-id="46578-228">Responses from the Bing search APIs may include a `X-MSEdge-ClientID` header that should be sent back to the API with successive requests.</span></span> <span data-ttu-id="46578-229">If multiple Bing Search APIs are being used, the same client ID should be used with all of them, if possible.</span><span class="sxs-lookup"><span data-stu-id="46578-229">If multiple Bing Search APIs are being used, the same client ID should be used with all of them, if possible.</span></span>

<span data-ttu-id="46578-230">Providing the `X-MSEdge-ClientID` header allows the Bing APIs to associate all of a user's searches, which has two important benefits.</span><span class="sxs-lookup"><span data-stu-id="46578-230">Providing the `X-MSEdge-ClientID` header allows the Bing APIs to associate all of a user's searches, which has two important benefits.</span></span>

<span data-ttu-id="46578-231">First, it allows the Bing search engine to apply past context to searches to find results that better satisfy the user.</span><span class="sxs-lookup"><span data-stu-id="46578-231">First, it allows the Bing search engine to apply past context to searches to find results that better satisfy the user.</span></span> <span data-ttu-id="46578-232">If a user has previously searched for terms related to sailing, for example, a later search for "knots" might preferentially return information about knots used in sailing.</span><span class="sxs-lookup"><span data-stu-id="46578-232">If a user has previously searched for terms related to sailing, for example, a later search for "knots" might preferentially return information about knots used in sailing.</span></span>

<span data-ttu-id="46578-233">Second, Bing may randomly select users to experience new features before they are made widely available.</span><span class="sxs-lookup"><span data-stu-id="46578-233">Second, Bing may randomly select users to experience new features before they are made widely available.</span></span> <span data-ttu-id="46578-234">Providing the same client ID with each request ensures that users that have been chosen to see a feature always see it.</span><span class="sxs-lookup"><span data-stu-id="46578-234">Providing the same client ID with each request ensures that users that have been chosen to see a feature always see it.</span></span> <span data-ttu-id="46578-235">Without the client ID, the user might see a feature appear and disappear, seemingly at random, in their search results.</span><span class="sxs-lookup"><span data-stu-id="46578-235">Without the client ID, the user might see a feature appear and disappear, seemingly at random, in their search results.</span></span>

<span data-ttu-id="46578-236">Browser security policies (CORS) may prevent the `X-MSEdge-ClientID` header from being available to JavaScript.</span><span class="sxs-lookup"><span data-stu-id="46578-236">Browser security policies (CORS) may prevent the `X-MSEdge-ClientID` header from being available to JavaScript.</span></span> <span data-ttu-id="46578-237">This limitation occurs when the search response has a different origin from the page that requested it.</span><span class="sxs-lookup"><span data-stu-id="46578-237">This limitation occurs when the search response has a different origin from the page that requested it.</span></span> <span data-ttu-id="46578-238">In a production environment, you should address this policy by hosting a server-side script that does the API call on the same domain as the Web page.</span><span class="sxs-lookup"><span data-stu-id="46578-238">In a production environment, you should address this policy by hosting a server-side script that does the API call on the same domain as the Web page.</span></span> <span data-ttu-id="46578-239">Since the script has the same origin as the Web page, the `X-MSEdge-ClientID` header is then available to JavaScript.</span><span class="sxs-lookup"><span data-stu-id="46578-239">Since the script has the same origin as the Web page, the `X-MSEdge-ClientID` header is then available to JavaScript.</span></span>

> [!NOTE]
> <span data-ttu-id="46578-240">In a production Web application, you should perform the request server-side anyway.</span><span class="sxs-lookup"><span data-stu-id="46578-240">In a production Web application, you should perform the request server-side anyway.</span></span> <span data-ttu-id="46578-241">Otherwise, your Bing Search API key must be included in the Web page, where it is available to anyone who views source.</span><span class="sxs-lookup"><span data-stu-id="46578-241">Otherwise, your Bing Search API key must be included in the Web page, where it is available to anyone who views source.</span></span> <span data-ttu-id="46578-242">You are billed for all usage under your API subscription key, even requests made by unauthorized parties, so it is important not to expose your key.</span><span class="sxs-lookup"><span data-stu-id="46578-242">You are billed for all usage under your API subscription key, even requests made by unauthorized parties, so it is important not to expose your key.</span></span>

<span data-ttu-id="46578-243">For development purposes, you can make the Bing Web Search API request through a CORS proxy.</span><span class="sxs-lookup"><span data-stu-id="46578-243">For development purposes, you can make the Bing Web Search API request through a CORS proxy.</span></span> <span data-ttu-id="46578-244">The response from such a proxy has an `Access-Control-Expose-Headers` header that whitelists response headers and makes them available to JavaScript.</span><span class="sxs-lookup"><span data-stu-id="46578-244">The response from such a proxy has an `Access-Control-Expose-Headers` header that whitelists response headers and makes them available to JavaScript.</span></span>

<span data-ttu-id="46578-245">It's easy to install a CORS proxy to allow our tutorial app to access the client ID header.</span><span class="sxs-lookup"><span data-stu-id="46578-245">It's easy to install a CORS proxy to allow our tutorial app to access the client ID header.</span></span> <span data-ttu-id="46578-246">First, if you don't already have it, [install Node.js](https://nodejs.org/en/download/).</span><span class="sxs-lookup"><span data-stu-id="46578-246">First, if you don't already have it, [install Node.js](https://nodejs.org/en/download/).</span></span> <span data-ttu-id="46578-247">Then issue the following command in a command window:</span><span class="sxs-lookup"><span data-stu-id="46578-247">Then issue the following command in a command window:</span></span>

    npm install -g cors-proxy-server

<span data-ttu-id="46578-248">Next, change the Bing Web Search endpoint in the HTML file to:</span><span class="sxs-lookup"><span data-stu-id="46578-248">Next, change the Bing Web Search endpoint in the HTML file to:</span></span>

    http://localhost:9090/https://api.cognitive.microsoft.com/bing/v7.0/search

<span data-ttu-id="46578-249">Finally, start the CORS proxy with the following command:</span><span class="sxs-lookup"><span data-stu-id="46578-249">Finally, start the CORS proxy with the following command:</span></span>

    cors-proxy-server

<span data-ttu-id="46578-250">Leave the command window open while you use the tutorial app; closing the window stops the proxy.</span><span class="sxs-lookup"><span data-stu-id="46578-250">Leave the command window open while you use the tutorial app; closing the window stops the proxy.</span></span> <span data-ttu-id="46578-251">In the expandable HTTP Headers section below the search results, you can now see the `X-MSEdge-ClientID` header (among others) and verify that it is the same for each request.</span><span class="sxs-lookup"><span data-stu-id="46578-251">In the expandable HTTP Headers section below the search results, you can now see the `X-MSEdge-ClientID` header (among others) and verify that it is the same for each request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46578-252">Next steps</span><span class="sxs-lookup"><span data-stu-id="46578-252">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="46578-253">Bing Image Search API reference</span><span class="sxs-lookup"><span data-stu-id="46578-253">Bing Image Search API reference</span></span>](//docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference)

