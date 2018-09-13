---
title: Bing Web Search single-page Web app | Microsoft Docs
description: Shows how to use the Bing Web Search API in a single-page Web application.
services: cognitive-services
author: v-jerkin
manager: ehansen
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: article
ms.date: 10/04/2017
ms.author: v-jerkin
ms.openlocfilehash: f22e38a1d6ee4042684b9822b58669bed6fe29a0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871211"
---
# <a name="tutorial-single-page-web-app"></a><span data-ttu-id="205e6-103">Tutorial: Single-page Web app</span><span class="sxs-lookup"><span data-stu-id="205e6-103">Tutorial: Single-page Web app</span></span>

<span data-ttu-id="205e6-104">The Bing Web Search API lets you search the Web and obtain results of varying types relevant to a search query.</span><span class="sxs-lookup"><span data-stu-id="205e6-104">The Bing Web Search API lets you search the Web and obtain results of varying types relevant to a search query.</span></span> <span data-ttu-id="205e6-105">In this tutorial, we build a single-page Web application that uses the Bing Web Search API to display search results right in the page.</span><span class="sxs-lookup"><span data-stu-id="205e6-105">In this tutorial, we build a single-page Web application that uses the Bing Web Search API to display search results right in the page.</span></span> <span data-ttu-id="205e6-106">The application includes HTML, CSS, and JavaScript components.</span><span class="sxs-lookup"><span data-stu-id="205e6-106">The application includes HTML, CSS, and JavaScript components.</span></span>

<!-- Remove until this can be replaced with a sanitized version.
![[Single-page Bing Web Search app]](media/cognitive-services-bing-web-api/web-search-spa-demo.png)
-->

> [!NOTE]
> <span data-ttu-id="205e6-107">The JSON and HTTP headings at the bottom of the page reveal the JSON response and HTTP request information when clicked.</span><span class="sxs-lookup"><span data-stu-id="205e6-107">The JSON and HTTP headings at the bottom of the page reveal the JSON response and HTTP request information when clicked.</span></span> <span data-ttu-id="205e6-108">These details are useful when exploring the service.</span><span class="sxs-lookup"><span data-stu-id="205e6-108">These details are useful when exploring the service.</span></span>

<span data-ttu-id="205e6-109">The tutorial app illustrates how to:</span><span class="sxs-lookup"><span data-stu-id="205e6-109">The tutorial app illustrates how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="205e6-110">Perform a Bing Web Search API call in JavaScript</span><span class="sxs-lookup"><span data-stu-id="205e6-110">Perform a Bing Web Search API call in JavaScript</span></span>
> * <span data-ttu-id="205e6-111">Pass search options to the Bing Web Search API</span><span class="sxs-lookup"><span data-stu-id="205e6-111">Pass search options to the Bing Web Search API</span></span>
> * <span data-ttu-id="205e6-112">Display Web, news, image, and video search results</span><span class="sxs-lookup"><span data-stu-id="205e6-112">Display Web, news, image, and video search results</span></span>
> * <span data-ttu-id="205e6-113">Page through search results</span><span class="sxs-lookup"><span data-stu-id="205e6-113">Page through search results</span></span>
> * <span data-ttu-id="205e6-114">Handle the Bing client ID and API subscription key</span><span class="sxs-lookup"><span data-stu-id="205e6-114">Handle the Bing client ID and API subscription key</span></span>
> * <span data-ttu-id="205e6-115">Handle errors that might occur</span><span class="sxs-lookup"><span data-stu-id="205e6-115">Handle errors that might occur</span></span>

<span data-ttu-id="205e6-116">The tutorial page is entirely self-contained; it does not use any external frameworks, style sheets, or even image files.</span><span class="sxs-lookup"><span data-stu-id="205e6-116">The tutorial page is entirely self-contained; it does not use any external frameworks, style sheets, or even image files.</span></span> <span data-ttu-id="205e6-117">It uses only widely supported JavaScript language features and works with current versions of all major Web browsers.</span><span class="sxs-lookup"><span data-stu-id="205e6-117">It uses only widely supported JavaScript language features and works with current versions of all major Web browsers.</span></span>

<span data-ttu-id="205e6-118">In this tutorial, we discuss only selected portions of the source code.</span><span class="sxs-lookup"><span data-stu-id="205e6-118">In this tutorial, we discuss only selected portions of the source code.</span></span> <span data-ttu-id="205e6-119">The full source code is available [on a separate page](tutorial-bing-web-search-single-page-app-source.md).</span><span class="sxs-lookup"><span data-stu-id="205e6-119">The full source code is available [on a separate page](tutorial-bing-web-search-single-page-app-source.md).</span></span> <span data-ttu-id="205e6-120">Copy and paste this code into a text editor and save it as `bing.html`.</span><span class="sxs-lookup"><span data-stu-id="205e6-120">Copy and paste this code into a text editor and save it as `bing.html`.</span></span>

## <a name="app-components"></a><span data-ttu-id="205e6-121">App components</span><span class="sxs-lookup"><span data-stu-id="205e6-121">App components</span></span>

<span data-ttu-id="205e6-122">Like any single-page Web app, the tutorial application includes three parts:</span><span class="sxs-lookup"><span data-stu-id="205e6-122">Like any single-page Web app, the tutorial application includes three parts:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="205e6-123">HTML - Defines the structure and content of the page</span><span class="sxs-lookup"><span data-stu-id="205e6-123">HTML - Defines the structure and content of the page</span></span>
> * <span data-ttu-id="205e6-124">CSS - Defines the appearance of the page</span><span class="sxs-lookup"><span data-stu-id="205e6-124">CSS - Defines the appearance of the page</span></span>
> * <span data-ttu-id="205e6-125">JavaScript - Defines the behavior of the page</span><span class="sxs-lookup"><span data-stu-id="205e6-125">JavaScript - Defines the behavior of the page</span></span>

<span data-ttu-id="205e6-126">This tutorial doesn't cover most of the HTML or CSS in detail, as they are straightforward.</span><span class="sxs-lookup"><span data-stu-id="205e6-126">This tutorial doesn't cover most of the HTML or CSS in detail, as they are straightforward.</span></span>

<span data-ttu-id="205e6-127">The HTML contains the search form in which the user enters a query and chooses search options.</span><span class="sxs-lookup"><span data-stu-id="205e6-127">The HTML contains the search form in which the user enters a query and chooses search options.</span></span> <span data-ttu-id="205e6-128">The form is connected to the JavaScript that actually performs the search by the `<form>` tag's `onsubmit` attribute:</span><span class="sxs-lookup"><span data-stu-id="205e6-128">The form is connected to the JavaScript that actually performs the search by the `<form>` tag's `onsubmit` attribute:</span></span>

```html
<form name="bing" onsubmit="return newBingWebSearch(this)">
```

<span data-ttu-id="205e6-129">The `onsubmit` handler returns `false`, which keeps the form from being submitted to a server.</span><span class="sxs-lookup"><span data-stu-id="205e6-129">The `onsubmit` handler returns `false`, which keeps the form from being submitted to a server.</span></span> <span data-ttu-id="205e6-130">The JavaScript code actually does the work of collecting the necessary information from the form and performing the search.</span><span class="sxs-lookup"><span data-stu-id="205e6-130">The JavaScript code actually does the work of collecting the necessary information from the form and performing the search.</span></span>

<span data-ttu-id="205e6-131">The HTML also contains the divisions (HTML `<div>` tags) where the search results appear.</span><span class="sxs-lookup"><span data-stu-id="205e6-131">The HTML also contains the divisions (HTML `<div>` tags) where the search results appear.</span></span>

## <a name="managing-subscription-key"></a><span data-ttu-id="205e6-132">Managing subscription key</span><span class="sxs-lookup"><span data-stu-id="205e6-132">Managing subscription key</span></span>

<span data-ttu-id="205e6-133">To avoid having to include the Bing Search API subscription key in the code, we use the browser's persistent storage to store the key.</span><span class="sxs-lookup"><span data-stu-id="205e6-133">To avoid having to include the Bing Search API subscription key in the code, we use the browser's persistent storage to store the key.</span></span> <span data-ttu-id="205e6-134">If no key is stored, we prompt for the user's key and store it for later use.</span><span class="sxs-lookup"><span data-stu-id="205e6-134">If no key is stored, we prompt for the user's key and store it for later use.</span></span> <span data-ttu-id="205e6-135">If the key is later rejected by the API, we invalidate the stored key so the user will be prompted again.</span><span class="sxs-lookup"><span data-stu-id="205e6-135">If the key is later rejected by the API, we invalidate the stored key so the user will be prompted again.</span></span>

<span data-ttu-id="205e6-136">We define `storeValue` and `retrieveValue` functions that use either the `localStorage` object (if the browser supports it) or a cookie.</span><span class="sxs-lookup"><span data-stu-id="205e6-136">We define `storeValue` and `retrieveValue` functions that use either the `localStorage` object (if the browser supports it) or a cookie.</span></span> <span data-ttu-id="205e6-137">Our `getSubscriptionKey()` function uses these functions to store and retrieve the user's key.</span><span class="sxs-lookup"><span data-stu-id="205e6-137">Our `getSubscriptionKey()` function uses these functions to store and retrieve the user's key.</span></span>

```javascript
// cookie names for data we store
API_KEY_COOKIE   = "bing-search-api-key";
CLIENT_ID_COOKIE = "bing-search-client-id";

BING_ENDPOINT = "https://api.cognitive.microsoft.com/bing/v7.0/search";

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

<span data-ttu-id="205e6-138">The HTML `form` tag `onsubmit` calls the `bingWebSearch` function to return search results.</span><span class="sxs-lookup"><span data-stu-id="205e6-138">The HTML `form` tag `onsubmit` calls the `bingWebSearch` function to return search results.</span></span> <span data-ttu-id="205e6-139">`bingWebSearch` uses `getSubscriptionKey` to authenticate each query.</span><span class="sxs-lookup"><span data-stu-id="205e6-139">`bingWebSearch` uses `getSubscriptionKey` to authenticate each query.</span></span> <span data-ttu-id="205e6-140">As shown in the previous definition, `getSubscriptionKey` prompts the user for the key if the key hasn't been entered.</span><span class="sxs-lookup"><span data-stu-id="205e6-140">As shown in the previous definition, `getSubscriptionKey` prompts the user for the key if the key hasn't been entered.</span></span> <span data-ttu-id="205e6-141">The key is then stored for continuing use by the application.</span><span class="sxs-lookup"><span data-stu-id="205e6-141">The key is then stored for continuing use by the application.</span></span>

```html
<form name="bing" onsubmit="this.offset.value = 0; return bingWebSearch(this.query.value, 
    bingSearchOptions(this), getSubscriptionKey())">
```

## <a name="selecting-search-options"></a><span data-ttu-id="205e6-142">Selecting search options</span><span class="sxs-lookup"><span data-stu-id="205e6-142">Selecting search options</span></span>

![[Bing Web Search form]](media/cognitive-services-bing-web-api/web-search-spa-form.png)

<span data-ttu-id="205e6-144">The HTML form includes elements with the following names:</span><span class="sxs-lookup"><span data-stu-id="205e6-144">The HTML form includes elements with the following names:</span></span>

| | |
|-|-|
| `where` | <span data-ttu-id="205e6-145">A drop-down menu for selecting the market (location and language) used for the search.</span><span class="sxs-lookup"><span data-stu-id="205e6-145">A drop-down menu for selecting the market (location and language) used for the search.</span></span> |
| `query` | <span data-ttu-id="205e6-146">The text field in which to enter the search terms.</span><span class="sxs-lookup"><span data-stu-id="205e6-146">The text field in which to enter the search terms.</span></span> |
| `what` | <span data-ttu-id="205e6-147">Checkboxes for promoting particular kinds of results.</span><span class="sxs-lookup"><span data-stu-id="205e6-147">Checkboxes for promoting particular kinds of results.</span></span> <span data-ttu-id="205e6-148">Promoting images, for example, increases the ranking of images.</span><span class="sxs-lookup"><span data-stu-id="205e6-148">Promoting images, for example, increases the ranking of images.</span></span> |
| `when` | <span data-ttu-id="205e6-149">Drop-down menu for optionally limiting the search to the most recent day, week, or month.</span><span class="sxs-lookup"><span data-stu-id="205e6-149">Drop-down menu for optionally limiting the search to the most recent day, week, or month.</span></span> |
| `safe` | <span data-ttu-id="205e6-150">A checkbox indicating whether to use Bing's SafeSearch feature to filter out "adult" results.</span><span class="sxs-lookup"><span data-stu-id="205e6-150">A checkbox indicating whether to use Bing's SafeSearch feature to filter out "adult" results.</span></span> |
| `count` | <span data-ttu-id="205e6-151">Hidden field.</span><span class="sxs-lookup"><span data-stu-id="205e6-151">Hidden field.</span></span> <span data-ttu-id="205e6-152">The number of search results to return on each request.</span><span class="sxs-lookup"><span data-stu-id="205e6-152">The number of search results to return on each request.</span></span> <span data-ttu-id="205e6-153">Change to display fewer or more results per page.</span><span class="sxs-lookup"><span data-stu-id="205e6-153">Change to display fewer or more results per page.</span></span> |
| `offset` | <span data-ttu-id="205e6-154">Hidden field.</span><span class="sxs-lookup"><span data-stu-id="205e6-154">Hidden field.</span></span> <span data-ttu-id="205e6-155">The offset of the first search result in the request; used for paging.</span><span class="sxs-lookup"><span data-stu-id="205e6-155">The offset of the first search result in the request; used for paging.</span></span> <span data-ttu-id="205e6-156">It's reset to `0` on a new request.</span><span class="sxs-lookup"><span data-stu-id="205e6-156">It's reset to `0` on a new request.</span></span> |

> [!NOTE]
> <span data-ttu-id="205e6-157">Bing Web Search offers many more query parameters.</span><span class="sxs-lookup"><span data-stu-id="205e6-157">Bing Web Search offers many more query parameters.</span></span> <span data-ttu-id="205e6-158">We're using only a few of them here.</span><span class="sxs-lookup"><span data-stu-id="205e6-158">We're using only a few of them here.</span></span>

<span data-ttu-id="205e6-159">The JavaScript function `bingSearchOptions()` converts these fields to the format required by the Bing Search API.</span><span class="sxs-lookup"><span data-stu-id="205e6-159">The JavaScript function `bingSearchOptions()` converts these fields to the format required by the Bing Search API.</span></span>

```javascript
// build query options from the HTML form
function bingSearchOptions(form) {

    var options = [];
    options.push("mkt=" + form.where.value);
    options.push("SafeSearch=" + (form.safe.checked ? "strict" : "off"));
    if (form.when.value.length) options.push("freshness=" + form.when.value);
    var what = [];
    for (var i = 0; i < form.what.length; i++) 
        if (form.what[i].checked) what.push(form.what[i].value);
    if (what.length) {
        options.push("promote=" + what.join(","));
        options.push("answerCount=9");
    }
    options.push("count=" + form.count.value);
    options.push("offset=" + form.offset.value);
    options.push("textDecorations=true");
    options.push("textFormat=HTML");
    return options.join("&");
}
```

<span data-ttu-id="205e6-160">For example, the `SafeSearch` parameter in an actual API call can be `strict`, `moderate`, or `off`, with `moderate` being the default.</span><span class="sxs-lookup"><span data-stu-id="205e6-160">For example, the `SafeSearch` parameter in an actual API call can be `strict`, `moderate`, or `off`, with `moderate` being the default.</span></span> <span data-ttu-id="205e6-161">Our form, however, uses a checkbox, which has only two states.</span><span class="sxs-lookup"><span data-stu-id="205e6-161">Our form, however, uses a checkbox, which has only two states.</span></span> <span data-ttu-id="205e6-162">The JavaScript code converts this setting to either `strict` or `off` (`moderate` is not used).</span><span class="sxs-lookup"><span data-stu-id="205e6-162">The JavaScript code converts this setting to either `strict` or `off` (`moderate` is not used).</span></span>

<span data-ttu-id="205e6-163">If any of the **Promote** checkboxes are marked, we also add an `answerCount` parameter to the query.</span><span class="sxs-lookup"><span data-stu-id="205e6-163">If any of the **Promote** checkboxes are marked, we also add an `answerCount` parameter to the query.</span></span> <span data-ttu-id="205e6-164">`answerCount` is required when using the `promote` parameter.</span><span class="sxs-lookup"><span data-stu-id="205e6-164">`answerCount` is required when using the `promote` parameter.</span></span> <span data-ttu-id="205e6-165">We simply set it to `9` (the number of result types supported by the Bing Web Search API) to make sure we get the maximum possible number of result types.</span><span class="sxs-lookup"><span data-stu-id="205e6-165">We simply set it to `9` (the number of result types supported by the Bing Web Search API) to make sure we get the maximum possible number of result types.</span></span>

> [!NOTE]
> <span data-ttu-id="205e6-166">Promoting a result type does not *guarantee* that the search results include that kind of result.</span><span class="sxs-lookup"><span data-stu-id="205e6-166">Promoting a result type does not *guarantee* that the search results include that kind of result.</span></span> <span data-ttu-id="205e6-167">Rather, promotion increases the ranking of those kinds of results relative to their usual ranking.</span><span class="sxs-lookup"><span data-stu-id="205e6-167">Rather, promotion increases the ranking of those kinds of results relative to their usual ranking.</span></span> <span data-ttu-id="205e6-168">To limit searches to particular kinds of results, use the `responseFilter` query parameter, or call a more specific endpoint such as Bing Image Search or Bing News Search.</span><span class="sxs-lookup"><span data-stu-id="205e6-168">To limit searches to particular kinds of results, use the `responseFilter` query parameter, or call a more specific endpoint such as Bing Image Search or Bing News Search.</span></span>

<span data-ttu-id="205e6-169">We also send `textDecoration` and `textFormat` query parameters to cause the search term to be boldfaced in the search results.</span><span class="sxs-lookup"><span data-stu-id="205e6-169">We also send `textDecoration` and `textFormat` query parameters to cause the search term to be boldfaced in the search results.</span></span> <span data-ttu-id="205e6-170">These values are hardcoded in the script.</span><span class="sxs-lookup"><span data-stu-id="205e6-170">These values are hardcoded in the script.</span></span>

## <a name="performing-the-request"></a><span data-ttu-id="205e6-171">Performing the request</span><span class="sxs-lookup"><span data-stu-id="205e6-171">Performing the request</span></span>

<span data-ttu-id="205e6-172">Given the query, the options string, and the API key, the `BingWebSearch` function uses an `XMLHttpRequest` object to make the request to the Bing Web Search endpoint.</span><span class="sxs-lookup"><span data-stu-id="205e6-172">Given the query, the options string, and the API key, the `BingWebSearch` function uses an `XMLHttpRequest` object to make the request to the Bing Web Search endpoint.</span></span>

```javascript
// perform a search given query, options string, and API key
function bingWebSearch(query, options, key) {

    // scroll to top of window
    window.scrollTo(0, 0);
    if (!query.trim().length) return false;     // empty query, do nothing

    showDiv("noresults", "Working. Please wait.");
    hideDivs("pole", "mainline", "sidebar", "_json", "_http", "paging1", "paging2", "error");

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

<span data-ttu-id="205e6-173">Upon successful completion of the HTTP request, JavaScript calls our `load` event handler, the `handleBingResponse()` function, to handle a successful HTTP GET request to the API.</span><span class="sxs-lookup"><span data-stu-id="205e6-173">Upon successful completion of the HTTP request, JavaScript calls our `load` event handler, the `handleBingResponse()` function, to handle a successful HTTP GET request to the API.</span></span> 

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
        return;
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
            if (jsobj._type === "SearchResponse" && "rankingResponse" in jsobj) {
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
> <span data-ttu-id="205e6-174">A successful HTTP request does *not* necessarily mean that the search itself succeeded.</span><span class="sxs-lookup"><span data-stu-id="205e6-174">A successful HTTP request does *not* necessarily mean that the search itself succeeded.</span></span> <span data-ttu-id="205e6-175">If an error occurs in the search operation, the Bing Web Search API returns a non-200 HTTP status code and includes error information in the JSON response.</span><span class="sxs-lookup"><span data-stu-id="205e6-175">If an error occurs in the search operation, the Bing Web Search API returns a non-200 HTTP status code and includes error information in the JSON response.</span></span> <span data-ttu-id="205e6-176">Additionally, if the request was rate-limited, the API returns an empty response.</span><span class="sxs-lookup"><span data-stu-id="205e6-176">Additionally, if the request was rate-limited, the API returns an empty response.</span></span>

<span data-ttu-id="205e6-177">Much of the code in both of the preceding functions is dedicated to error handling.</span><span class="sxs-lookup"><span data-stu-id="205e6-177">Much of the code in both of the preceding functions is dedicated to error handling.</span></span> <span data-ttu-id="205e6-178">Errors may occur at the following stages:</span><span class="sxs-lookup"><span data-stu-id="205e6-178">Errors may occur at the following stages:</span></span>

|<span data-ttu-id="205e6-179">Stage</span><span class="sxs-lookup"><span data-stu-id="205e6-179">Stage</span></span>|<span data-ttu-id="205e6-180">Potential error(s)</span><span class="sxs-lookup"><span data-stu-id="205e6-180">Potential error(s)</span></span>|<span data-ttu-id="205e6-181">Handled by</span><span class="sxs-lookup"><span data-stu-id="205e6-181">Handled by</span></span>|
|-|-|-|
|<span data-ttu-id="205e6-182">Building JavaScript request object</span><span class="sxs-lookup"><span data-stu-id="205e6-182">Building JavaScript request object</span></span>|<span data-ttu-id="205e6-183">Invalid URL</span><span class="sxs-lookup"><span data-stu-id="205e6-183">Invalid URL</span></span>|<span data-ttu-id="205e6-184">`try`/`catch` block</span><span class="sxs-lookup"><span data-stu-id="205e6-184">`try`/`catch` block</span></span>|
|<span data-ttu-id="205e6-185">Making the request</span><span class="sxs-lookup"><span data-stu-id="205e6-185">Making the request</span></span>|<span data-ttu-id="205e6-186">Network errors, aborted connections</span><span class="sxs-lookup"><span data-stu-id="205e6-186">Network errors, aborted connections</span></span>|<span data-ttu-id="205e6-187">`error` and `abort` event handlers</span><span class="sxs-lookup"><span data-stu-id="205e6-187">`error` and `abort` event handlers</span></span>|
|<span data-ttu-id="205e6-188">Performing the search</span><span class="sxs-lookup"><span data-stu-id="205e6-188">Performing the search</span></span>|<span data-ttu-id="205e6-189">Invalid request, invalid JSON, rate limits</span><span class="sxs-lookup"><span data-stu-id="205e6-189">Invalid request, invalid JSON, rate limits</span></span>|<span data-ttu-id="205e6-190">tests in `load` event handler</span><span class="sxs-lookup"><span data-stu-id="205e6-190">tests in `load` event handler</span></span>|

<span data-ttu-id="205e6-191">Errors are handled by calling `renderErrorMessage()` with any details known about the error.</span><span class="sxs-lookup"><span data-stu-id="205e6-191">Errors are handled by calling `renderErrorMessage()` with any details known about the error.</span></span> <span data-ttu-id="205e6-192">If the response passes the full gauntlet of error tests, we call `renderSearchResults()` to display the search results in the page.</span><span class="sxs-lookup"><span data-stu-id="205e6-192">If the response passes the full gauntlet of error tests, we call `renderSearchResults()` to display the search results in the page.</span></span>

## <a name="displaying-search-results"></a><span data-ttu-id="205e6-193">Displaying search results</span><span class="sxs-lookup"><span data-stu-id="205e6-193">Displaying search results</span></span>

<span data-ttu-id="205e6-194">The Bing Web Search API [requires you to display results in a specified order](useanddisplayrequirements.md).</span><span class="sxs-lookup"><span data-stu-id="205e6-194">The Bing Web Search API [requires you to display results in a specified order](useanddisplayrequirements.md).</span></span> <span data-ttu-id="205e6-195">Since the API may return different kinds of responses, it is not enough to iterate through the top-level `WebPages` collection in the JSON response and display those results.</span><span class="sxs-lookup"><span data-stu-id="205e6-195">Since the API may return different kinds of responses, it is not enough to iterate through the top-level `WebPages` collection in the JSON response and display those results.</span></span> <span data-ttu-id="205e6-196">(If you want only one kind of results, use the `responseFilter` query parameter or another Bing Search endpoint.)</span><span class="sxs-lookup"><span data-stu-id="205e6-196">(If you want only one kind of results, use the `responseFilter` query parameter or another Bing Search endpoint.)</span></span>

<span data-ttu-id="205e6-197">Instead, we use the `rankingResponse` in the search results to order the results for display.</span><span class="sxs-lookup"><span data-stu-id="205e6-197">Instead, we use the `rankingResponse` in the search results to order the results for display.</span></span> <span data-ttu-id="205e6-198">This object refers to items in the `WebPages` `News`, `Images`, and/or `Videos` collections, or in other top-level answer collections in the JSON response.</span><span class="sxs-lookup"><span data-stu-id="205e6-198">This object refers to items in the `WebPages` `News`, `Images`, and/or `Videos` collections, or in other top-level answer collections in the JSON response.</span></span>

<span data-ttu-id="205e6-199">`rankingResponse` may contain up to three collections of search results, designated `pole`, `mainline`, and `sidebar`.</span><span class="sxs-lookup"><span data-stu-id="205e6-199">`rankingResponse` may contain up to three collections of search results, designated `pole`, `mainline`, and `sidebar`.</span></span> 

<span data-ttu-id="205e6-200">`pole`, if present, is the most relevant search result and should be displayed prominently.</span><span class="sxs-lookup"><span data-stu-id="205e6-200">`pole`, if present, is the most relevant search result and should be displayed prominently.</span></span> <span data-ttu-id="205e6-201">`mainline` refers to the bulk of the search results.</span><span class="sxs-lookup"><span data-stu-id="205e6-201">`mainline` refers to the bulk of the search results.</span></span> <span data-ttu-id="205e6-202">Mainline results should be displayed immediately after `pole` (or first, if `pole` is not present).</span><span class="sxs-lookup"><span data-stu-id="205e6-202">Mainline results should be displayed immediately after `pole` (or first, if `pole` is not present).</span></span> 

<span data-ttu-id="205e6-203">Finally.</span><span class="sxs-lookup"><span data-stu-id="205e6-203">Finally.</span></span> <span data-ttu-id="205e6-204">`sidebar` refers to auxiliary search results.</span><span class="sxs-lookup"><span data-stu-id="205e6-204">`sidebar` refers to auxiliary search results.</span></span> <span data-ttu-id="205e6-205">Often, these results are related searches or images.</span><span class="sxs-lookup"><span data-stu-id="205e6-205">Often, these results are related searches or images.</span></span> <span data-ttu-id="205e6-206">If possible, these results should be displayed in an actual sidebar.</span><span class="sxs-lookup"><span data-stu-id="205e6-206">If possible, these results should be displayed in an actual sidebar.</span></span> <span data-ttu-id="205e6-207">If screen limits make a sidebar impractical (for example, on a mobile device), they should appear after the `mainline` results.</span><span class="sxs-lookup"><span data-stu-id="205e6-207">If screen limits make a sidebar impractical (for example, on a mobile device), they should appear after the `mainline` results.</span></span>

<span data-ttu-id="205e6-208">Each item in a `rankingResponse` collection refers to the actual search result items in two different, but equivalent, ways.</span><span class="sxs-lookup"><span data-stu-id="205e6-208">Each item in a `rankingResponse` collection refers to the actual search result items in two different, but equivalent, ways.</span></span>

| | |
|-|-|
|`id`|<span data-ttu-id="205e6-209">The `id` looks like a URL, but should not be used for links.</span><span class="sxs-lookup"><span data-stu-id="205e6-209">The `id` looks like a URL, but should not be used for links.</span></span> <span data-ttu-id="205e6-210">The `id` type of a ranking result matches the `id` of either a search result item in an answer collection, *or* an entire answer collection (such as `Images`).</span><span class="sxs-lookup"><span data-stu-id="205e6-210">The `id` type of a ranking result matches the `id` of either a search result item in an answer collection, *or* an entire answer collection (such as `Images`).</span></span>
|<span data-ttu-id="205e6-211">`answerType`, `resultIndex`</span><span class="sxs-lookup"><span data-stu-id="205e6-211">`answerType`, `resultIndex`</span></span>|<span data-ttu-id="205e6-212">The `answerType` refers to the top-level answer collection that contains the result (for example, `WebPages`).</span><span class="sxs-lookup"><span data-stu-id="205e6-212">The `answerType` refers to the top-level answer collection that contains the result (for example, `WebPages`).</span></span> <span data-ttu-id="205e6-213">The `resultIndex` refers to the result's index within that collection.</span><span class="sxs-lookup"><span data-stu-id="205e6-213">The `resultIndex` refers to the result's index within that collection.</span></span> <span data-ttu-id="205e6-214">If `resultIndex` is omitted, the ranking result refers to the entire collection.</span><span class="sxs-lookup"><span data-stu-id="205e6-214">If `resultIndex` is omitted, the ranking result refers to the entire collection.</span></span>

> [!NOTE]
> <span data-ttu-id="205e6-215">For more information on this part of the search response, see [Rank Results](rank-results.md).</span><span class="sxs-lookup"><span data-stu-id="205e6-215">For more information on this part of the search response, see [Rank Results](rank-results.md).</span></span>

<span data-ttu-id="205e6-216">You may use whichever method of locating the referenced search result item is most convenient for your application.</span><span class="sxs-lookup"><span data-stu-id="205e6-216">You may use whichever method of locating the referenced search result item is most convenient for your application.</span></span> <span data-ttu-id="205e6-217">In our tutorial code, we use the `answerType` and `resultIndex` to locate each search result.</span><span class="sxs-lookup"><span data-stu-id="205e6-217">In our tutorial code, we use the `answerType` and `resultIndex` to locate each search result.</span></span>

<span data-ttu-id="205e6-218">Finally, it's time to look at our function `renderSearchResults()`.</span><span class="sxs-lookup"><span data-stu-id="205e6-218">Finally, it's time to look at our function `renderSearchResults()`.</span></span> <span data-ttu-id="205e6-219">This function iterates over the three `rankingResponse` collections that represent the three sections of the search results.</span><span class="sxs-lookup"><span data-stu-id="205e6-219">This function iterates over the three `rankingResponse` collections that represent the three sections of the search results.</span></span> <span data-ttu-id="205e6-220">For each section, we call `renderResultsItems()` to render the results for that section.</span><span class="sxs-lookup"><span data-stu-id="205e6-220">For each section, we call `renderResultsItems()` to render the results for that section.</span></span>

```javascript
// render the search results given the parsed JSON response
function renderSearchResults(results) {

    // if spelling was corrected, update search field
    if (results.queryContext.alteredQuery) 
        document.forms.bing.query.value = results.queryContext.alteredQuery;

    // add Prev / Next links with result count
    var pagingLinks = renderPagingLinks(results);
    showDiv("paging1", pagingLinks);
    showDiv("paging2", pagingLinks);
    
    // for each possible section, render the resuts from that section
    for (section in {pole: 0, mainline: 0, sidebar: 0}) {
        if (results.rankingResponse[section])
            showDiv(section, renderResultsItems(section, results));
    }
}
```

<span data-ttu-id="205e6-221">`renderResultsItems()` in turn iterates over the items in each `rankingResponse` section, maps each ranking result to a search result using the `answerType` and `resultIndex` fields, and calls the appropriate rendering function to generate the result's HTML.</span><span class="sxs-lookup"><span data-stu-id="205e6-221">`renderResultsItems()` in turn iterates over the items in each `rankingResponse` section, maps each ranking result to a search result using the `answerType` and `resultIndex` fields, and calls the appropriate rendering function to generate the result's HTML.</span></span> 

<span data-ttu-id="205e6-222">If `resultIndex` is not specified for a given ranking item, `renderResultsItems()` iterates over all results of that type and calls the rendering function for each item.</span><span class="sxs-lookup"><span data-stu-id="205e6-222">If `resultIndex` is not specified for a given ranking item, `renderResultsItems()` iterates over all results of that type and calls the rendering function for each item.</span></span> 

<span data-ttu-id="205e6-223">Either way, the resulting HTML is inserted into the appropriate `<div>` element in the page.</span><span class="sxs-lookup"><span data-stu-id="205e6-223">Either way, the resulting HTML is inserted into the appropriate `<div>` element in the page.</span></span>

```javascript
// render search results from rankingResponse object in specified order
function renderResultsItems(section, results) {

    var items = results.rankingResponse[section].items;
    var html = [];
    for (var i = 0; i < items.length; i++) {
        var item = items[i];
        // collection name has lowercase first letter while answerType has uppercase
        // e.g. `WebPages` rankingResult type is in the `webPages` top-level collection
        var type = item.answerType[0].toLowerCase() + item.answerType.slice(1);
        // must have results of the given type AND a renderer for it
        if (type in results && type in searchItemRenderers) {
            var render = searchItemRenderers[type];
            // this ranking item refers to ONE result of the specified type
            if ("resultIndex" in item) {
                html.push(render(results[type].value[item.resultIndex], section));
            // this ranking item refers to ALL results of the specified type
            } else {
                var len = results[type].value.length;
                for (var j = 0; j < len; j++) {
                    html.push(render(results[type].value[j], section, j, len));
                }
            }
        }
    }
    return html.join("\n\n");
}
```

## <a name="rendering-result-items"></a><span data-ttu-id="205e6-224">Rendering result items</span><span class="sxs-lookup"><span data-stu-id="205e6-224">Rendering result items</span></span>

<span data-ttu-id="205e6-225">In our JavaScript code is an object, `searchItemRenderers`, that contains *renderers:* functions that generate HTML for each kind of search result.</span><span class="sxs-lookup"><span data-stu-id="205e6-225">In our JavaScript code is an object, `searchItemRenderers`, that contains *renderers:* functions that generate HTML for each kind of search result.</span></span>

```javascript
// render functions for various types of search results
searchItemRenderers = { 
    webPages: function(item) { ... },
    news: function(item) { ... },
    images: function(item, section, index, count) { ... },
    videos: function(item, section, index, count) { ... },
    relatedSearches: function(item, section, index, count) { ... }
}
```

> [!NOTE]
> <span data-ttu-id="205e6-226">Our tutorial app has renderers for Web pages, news items, images, videos, and related searches.</span><span class="sxs-lookup"><span data-stu-id="205e6-226">Our tutorial app has renderers for Web pages, news items, images, videos, and related searches.</span></span> <span data-ttu-id="205e6-227">Your own application needs renderers for any kinds of results you might receive, which could include computations, spelling suggestions, entities, time zones, and definitions.</span><span class="sxs-lookup"><span data-stu-id="205e6-227">Your own application needs renderers for any kinds of results you might receive, which could include computations, spelling suggestions, entities, time zones, and definitions.</span></span>

<span data-ttu-id="205e6-228">Some of our rendering functions accept only the `item` parameter: a JavaScript object that represents a single search result.</span><span class="sxs-lookup"><span data-stu-id="205e6-228">Some of our rendering functions accept only the `item` parameter: a JavaScript object that represents a single search result.</span></span> <span data-ttu-id="205e6-229">Others accept additional parameters, which can be used to render items differently in different contexts.</span><span class="sxs-lookup"><span data-stu-id="205e6-229">Others accept additional parameters, which can be used to render items differently in different contexts.</span></span> <span data-ttu-id="205e6-230">(A renderer that does not use this information does not need to accept these parameters.)</span><span class="sxs-lookup"><span data-stu-id="205e6-230">(A renderer that does not use this information does not need to accept these parameters.)</span></span>

<span data-ttu-id="205e6-231">The context arguments are:</span><span class="sxs-lookup"><span data-stu-id="205e6-231">The context arguments are:</span></span>

| | |
|-|-|
|`section`|<span data-ttu-id="205e6-232">The results section (`pole`, `mainline`, or `sidebar`) in which the item appears.</span><span class="sxs-lookup"><span data-stu-id="205e6-232">The results section (`pole`, `mainline`, or `sidebar`) in which the item appears.</span></span>
|`index`<br>`count`|<span data-ttu-id="205e6-233">Available when the `rankingResponse` item specifies that all results in a given collection are to be displayed; `undefined` otherwise.</span><span class="sxs-lookup"><span data-stu-id="205e6-233">Available when the `rankingResponse` item specifies that all results in a given collection are to be displayed; `undefined` otherwise.</span></span> <span data-ttu-id="205e6-234">These parameters receive the index of the item within its collection and the total number of items in that collection.</span><span class="sxs-lookup"><span data-stu-id="205e6-234">These parameters receive the index of the item within its collection and the total number of items in that collection.</span></span> <span data-ttu-id="205e6-235">You can this information to number the results, to generate different HTML for the first or last result, and so on.</span><span class="sxs-lookup"><span data-stu-id="205e6-235">You can this information to number the results, to generate different HTML for the first or last result, and so on.</span></span>|

<span data-ttu-id="205e6-236">In our tutorial app, both the `images` and `relatedSearches` renderers use the context arguments to customize the HTML they generate.</span><span class="sxs-lookup"><span data-stu-id="205e6-236">In our tutorial app, both the `images` and `relatedSearches` renderers use the context arguments to customize the HTML they generate.</span></span> <span data-ttu-id="205e6-237">Let's take a closer look at the `images` renderer:</span><span class="sxs-lookup"><span data-stu-id="205e6-237">Let's take a closer look at the `images` renderer:</span></span>

```javascript
searchItemRenderers = { 
    // render image result using thumbnail
    images: function(item, section, index, count) {
        var height = 60;
        var width = Math.round(height * item.thumbnail.width / item.thumbnail.height);
        var html = [];
        if (section === "sidebar") {
            if (index) html.push("<br>");
        } else {
            if (!index) html.push("<p class='images'>");
        }
        html.push("<a href='" + item.hostPageUrl + "'>");
        var title = escape(item.name) + "\n" + getHost(item.hostPageDisplayUrl);
        html.push("<img src='"+ item.thumbnailUrl + "&h=" + height + "&w=" + width + 
            "' height=" + height + " width=" + width + " title='" + title + "' alt='" + title + "'>");
        html.push("</a>");
        return html.join("");
    }, // other renderers omitted
}
```

<span data-ttu-id="205e6-238">Our image renderer function:</span><span class="sxs-lookup"><span data-stu-id="205e6-238">Our image renderer function:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="205e6-239">Calculates the image thumbnail size (width varies, while height is fixed at 60 pixels).</span><span class="sxs-lookup"><span data-stu-id="205e6-239">Calculates the image thumbnail size (width varies, while height is fixed at 60 pixels).</span></span>
> * <span data-ttu-id="205e6-240">Inserts the HTML that precedes the image result depending on context.</span><span class="sxs-lookup"><span data-stu-id="205e6-240">Inserts the HTML that precedes the image result depending on context.</span></span>
> * <span data-ttu-id="205e6-241">Builds the HTML `<a>` tag that links to the page containing the image.</span><span class="sxs-lookup"><span data-stu-id="205e6-241">Builds the HTML `<a>` tag that links to the page containing the image.</span></span>
> * <span data-ttu-id="205e6-242">Builds the HTML `<img>` tag to display the image thumbnail.</span><span class="sxs-lookup"><span data-stu-id="205e6-242">Builds the HTML `<img>` tag to display the image thumbnail.</span></span> 

<span data-ttu-id="205e6-243">The image renderer uses the `section` and `index` variables to display results differently depending on where they appear.</span><span class="sxs-lookup"><span data-stu-id="205e6-243">The image renderer uses the `section` and `index` variables to display results differently depending on where they appear.</span></span> <span data-ttu-id="205e6-244">A line break (`<br>` tag) is inserted between image results in the sidebar, so that the sidebar displays a column of images.</span><span class="sxs-lookup"><span data-stu-id="205e6-244">A line break (`<br>` tag) is inserted between image results in the sidebar, so that the sidebar displays a column of images.</span></span> <span data-ttu-id="205e6-245">In other sections, the first image result `(index === 0)` is preceded by a `<p>` tag.</span><span class="sxs-lookup"><span data-stu-id="205e6-245">In other sections, the first image result `(index === 0)` is preceded by a `<p>` tag.</span></span> <span data-ttu-id="205e6-246">The thumbnails otherwise butt up against each other and wrap as needed in the browser window.</span><span class="sxs-lookup"><span data-stu-id="205e6-246">The thumbnails otherwise butt up against each other and wrap as needed in the browser window.</span></span>

<span data-ttu-id="205e6-247">The thumbnail size is used in both the `<img>` tag and the `h` and `w` fields in the thumbnail's URL.</span><span class="sxs-lookup"><span data-stu-id="205e6-247">The thumbnail size is used in both the `<img>` tag and the `h` and `w` fields in the thumbnail's URL.</span></span> <span data-ttu-id="205e6-248">The [Bing thumbnail service](resize-and-crop-thumbnails.md) then delivers a thumbnail of exactly that size.</span><span class="sxs-lookup"><span data-stu-id="205e6-248">The [Bing thumbnail service](resize-and-crop-thumbnails.md) then delivers a thumbnail of exactly that size.</span></span> <span data-ttu-id="205e6-249">The `title` and `alt` attributes (a textual description of the image) are constructed from the image's name and the hostname in the URL.</span><span class="sxs-lookup"><span data-stu-id="205e6-249">The `title` and `alt` attributes (a textual description of the image) are constructed from the image's name and the hostname in the URL.</span></span>

<span data-ttu-id="205e6-250">Images appear as shown here in the mainline search results.</span><span class="sxs-lookup"><span data-stu-id="205e6-250">Images appear as shown here in the mainline search results.</span></span>

![[Bing image results]](media/cognitive-services-bing-web-api/web-search-spa-images.png)

## <a name="persisting-client-id"></a><span data-ttu-id="205e6-252">Persisting client ID</span><span class="sxs-lookup"><span data-stu-id="205e6-252">Persisting client ID</span></span>

<span data-ttu-id="205e6-253">Responses from the Bing search APIs may include a `X-MSEdge-ClientID` header that should be sent back to the API with successive requests.</span><span class="sxs-lookup"><span data-stu-id="205e6-253">Responses from the Bing search APIs may include a `X-MSEdge-ClientID` header that should be sent back to the API with successive requests.</span></span> <span data-ttu-id="205e6-254">If multiple Bing Search APIs are being used, the same client ID should be used with all of them, if possible.</span><span class="sxs-lookup"><span data-stu-id="205e6-254">If multiple Bing Search APIs are being used, the same client ID should be used with all of them, if possible.</span></span>

<span data-ttu-id="205e6-255">Providing the `X-MSEdge-ClientID` header allows the Bing APIs to associate all of a user's searches, which has two important benefits.</span><span class="sxs-lookup"><span data-stu-id="205e6-255">Providing the `X-MSEdge-ClientID` header allows the Bing APIs to associate all of a user's searches, which has two important benefits.</span></span>

<span data-ttu-id="205e6-256">First, it allows the Bing search engine to apply past context to searches to find results that better satisfy the user.</span><span class="sxs-lookup"><span data-stu-id="205e6-256">First, it allows the Bing search engine to apply past context to searches to find results that better satisfy the user.</span></span> <span data-ttu-id="205e6-257">If a user has previously searched for terms related to sailing, for example, a later search for "knots" might preferentially return information about knots used in sailing.</span><span class="sxs-lookup"><span data-stu-id="205e6-257">If a user has previously searched for terms related to sailing, for example, a later search for "knots" might preferentially return information about knots used in sailing.</span></span>

<span data-ttu-id="205e6-258">Second, Bing may randomly select users to experience new features before they are made widely available.</span><span class="sxs-lookup"><span data-stu-id="205e6-258">Second, Bing may randomly select users to experience new features before they are made widely available.</span></span> <span data-ttu-id="205e6-259">Providing the same client ID with each request ensures that users who have been chosen to see a feature always see it.</span><span class="sxs-lookup"><span data-stu-id="205e6-259">Providing the same client ID with each request ensures that users who have been chosen to see a feature always see it.</span></span> <span data-ttu-id="205e6-260">Without the client ID, the user might see a feature appear and disappear, seemingly at random, in their search results.</span><span class="sxs-lookup"><span data-stu-id="205e6-260">Without the client ID, the user might see a feature appear and disappear, seemingly at random, in their search results.</span></span>

<span data-ttu-id="205e6-261">Browser security policies (CORS) may prevent the `X-MSEdge-ClientID` header from being available to JavaScript.</span><span class="sxs-lookup"><span data-stu-id="205e6-261">Browser security policies (CORS) may prevent the `X-MSEdge-ClientID` header from being available to JavaScript.</span></span> <span data-ttu-id="205e6-262">This limitation occurs when the search response has a different origin from the page that requested it.</span><span class="sxs-lookup"><span data-stu-id="205e6-262">This limitation occurs when the search response has a different origin from the page that requested it.</span></span> <span data-ttu-id="205e6-263">In a production environment, you should address this policy by hosting a server-side script that does the API call on the same domain as the Web page.</span><span class="sxs-lookup"><span data-stu-id="205e6-263">In a production environment, you should address this policy by hosting a server-side script that does the API call on the same domain as the Web page.</span></span> <span data-ttu-id="205e6-264">Since the script has the same origin as the Web page, the `X-MSEdge-ClientID` header is then available to JavaScript.</span><span class="sxs-lookup"><span data-stu-id="205e6-264">Since the script has the same origin as the Web page, the `X-MSEdge-ClientID` header is then available to JavaScript.</span></span>

> [!NOTE]
> <span data-ttu-id="205e6-265">In a production Web application, you should perform the request server-side anyway.</span><span class="sxs-lookup"><span data-stu-id="205e6-265">In a production Web application, you should perform the request server-side anyway.</span></span> <span data-ttu-id="205e6-266">Otherwise, your Bing Search API key must be included in the Web page, where it is available to anyone who views source.</span><span class="sxs-lookup"><span data-stu-id="205e6-266">Otherwise, your Bing Search API key must be included in the Web page, where it is available to anyone who views source.</span></span> <span data-ttu-id="205e6-267">You are billed for all usage under your API subscription key, even requests made by unauthorized parties, so it is important not to expose your key.</span><span class="sxs-lookup"><span data-stu-id="205e6-267">You are billed for all usage under your API subscription key, even requests made by unauthorized parties, so it is important not to expose your key.</span></span>

<span data-ttu-id="205e6-268">For development purposes, you can make the Bing Web Search API request through a CORS proxy.</span><span class="sxs-lookup"><span data-stu-id="205e6-268">For development purposes, you can make the Bing Web Search API request through a CORS proxy.</span></span> <span data-ttu-id="205e6-269">The response from such a proxy has an `Access-Control-Expose-Headers` header that whitelists response headers and makes them available to JavaScript.</span><span class="sxs-lookup"><span data-stu-id="205e6-269">The response from such a proxy has an `Access-Control-Expose-Headers` header that whitelists response headers and makes them available to JavaScript.</span></span>

<span data-ttu-id="205e6-270">It's easy to install a CORS proxy to allow our tutorial app to access the client ID header.</span><span class="sxs-lookup"><span data-stu-id="205e6-270">It's easy to install a CORS proxy to allow our tutorial app to access the client ID header.</span></span> <span data-ttu-id="205e6-271">First, if you don't already have it, [install Node.js](https://nodejs.org/en/download/).</span><span class="sxs-lookup"><span data-stu-id="205e6-271">First, if you don't already have it, [install Node.js](https://nodejs.org/en/download/).</span></span> <span data-ttu-id="205e6-272">Then issue the following command in a command window:</span><span class="sxs-lookup"><span data-stu-id="205e6-272">Then issue the following command in a command window:</span></span>

    npm install -g cors-proxy-server

<span data-ttu-id="205e6-273">Next, change the Bing Web Search endpoint in the HTML file to:</span><span class="sxs-lookup"><span data-stu-id="205e6-273">Next, change the Bing Web Search endpoint in the HTML file to:</span></span>

    http://localhost:9090/https://api.cognitive.microsoft.com/bing/v7.0/search

<span data-ttu-id="205e6-274">Finally, start the CORS proxy with the following command:</span><span class="sxs-lookup"><span data-stu-id="205e6-274">Finally, start the CORS proxy with the following command:</span></span>

    cors-proxy-server

<span data-ttu-id="205e6-275">Leave the command window open while you use the tutorial app; closing the window stops the proxy.</span><span class="sxs-lookup"><span data-stu-id="205e6-275">Leave the command window open while you use the tutorial app; closing the window stops the proxy.</span></span> <span data-ttu-id="205e6-276">In the expandable HTTP Headers section below the search results, you can now see the `X-MSEdge-ClientID` header (among others) and verify that it is the same for each request.</span><span class="sxs-lookup"><span data-stu-id="205e6-276">In the expandable HTTP Headers section below the search results, you can now see the `X-MSEdge-ClientID` header (among others) and verify that it is the same for each request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="205e6-277">Next steps</span><span class="sxs-lookup"><span data-stu-id="205e6-277">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="205e6-278">Visual Search mobile app tutorial</span><span class="sxs-lookup"><span data-stu-id="205e6-278">Visual Search mobile app tutorial</span></span>](computer-vision-web-search-tutorial.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="205e6-279">Bing Web Search API reference</span><span class="sxs-lookup"><span data-stu-id="205e6-279">Bing Web Search API reference</span></span>](//docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference)
