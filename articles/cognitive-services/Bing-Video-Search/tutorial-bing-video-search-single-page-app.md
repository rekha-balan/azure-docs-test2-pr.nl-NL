---
title: Bing single-page Video search app | Microsoft Docs
description: Explains how to use the Bing Video Search API in a single-page Web application.
services: cognitive-services
author: mikedodaro
manager: ronakshah
ms.service: cognitive-services
ms.component: bing-video-search
ms.topic: article
ms.date: 11/01/2017
ms.author: v-gedod
ms.openlocfilehash: 55f662721e007e03c8f43f19d8b905e755cfe1d8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855968"
---
# <a name="tutorial-single-page-video-search-app"></a><span data-ttu-id="1c235-103">Tutorial: Single-page Video Search app</span><span class="sxs-lookup"><span data-stu-id="1c235-103">Tutorial: Single-page Video Search app</span></span>
<span data-ttu-id="1c235-104">The Bing Video Search API lets you search the Web and get video results relevant to a search query.</span><span class="sxs-lookup"><span data-stu-id="1c235-104">The Bing Video Search API lets you search the Web and get video results relevant to a search query.</span></span> <span data-ttu-id="1c235-105">In this tutorial, we build a single-page Web application that uses the Bing search API to display search results on the page.</span><span class="sxs-lookup"><span data-stu-id="1c235-105">In this tutorial, we build a single-page Web application that uses the Bing search API to display search results on the page.</span></span> <span data-ttu-id="1c235-106">The application includes HTML, CSS, and JavaScript components.</span><span class="sxs-lookup"><span data-stu-id="1c235-106">The application includes HTML, CSS, and JavaScript components.</span></span>

<!-- Remove until it can be replaced with a sanitized version.
![Single-page Bing Video Search app](./media/video-search-singlepage.png)
-->

> [!NOTE]
> <span data-ttu-id="1c235-107">The JSON and HTTP headings at the bottom of the page when clicked show the JSON response and HTTP request information.</span><span class="sxs-lookup"><span data-stu-id="1c235-107">The JSON and HTTP headings at the bottom of the page when clicked show the JSON response and HTTP request information.</span></span> <span data-ttu-id="1c235-108">These details can be useful when exploring the service.</span><span class="sxs-lookup"><span data-stu-id="1c235-108">These details can be useful when exploring the service.</span></span>

![JSON, HTTP raw results](./media/json-http-raw-results.png)

<span data-ttu-id="1c235-110">This tutorial app illustrates how to:</span><span class="sxs-lookup"><span data-stu-id="1c235-110">This tutorial app illustrates how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="1c235-111">Perform a Bing Video Search API call in JavaScript</span><span class="sxs-lookup"><span data-stu-id="1c235-111">Perform a Bing Video Search API call in JavaScript</span></span>
> * <span data-ttu-id="1c235-112">Pass search options to the Bing Search API</span><span class="sxs-lookup"><span data-stu-id="1c235-112">Pass search options to the Bing Search API</span></span>
> * <span data-ttu-id="1c235-113">Display video search results or to optionally include Web pages, news, or images</span><span class="sxs-lookup"><span data-stu-id="1c235-113">Display video search results or to optionally include Web pages, news, or images</span></span>
> * <span data-ttu-id="1c235-114">Search time-frames of 24 hours, the past week, month, or all available time</span><span class="sxs-lookup"><span data-stu-id="1c235-114">Search time-frames of 24 hours, the past week, month, or all available time</span></span>
> * <span data-ttu-id="1c235-115">Page through search results</span><span class="sxs-lookup"><span data-stu-id="1c235-115">Page through search results</span></span>
> * <span data-ttu-id="1c235-116">Handle the Bing client ID and API subscription key</span><span class="sxs-lookup"><span data-stu-id="1c235-116">Handle the Bing client ID and API subscription key</span></span>
> * <span data-ttu-id="1c235-117">Handle errors that might occur</span><span class="sxs-lookup"><span data-stu-id="1c235-117">Handle errors that might occur</span></span>

<span data-ttu-id="1c235-118">The tutorial page is entirely self-contained; it does not use any external frameworks, style sheets, or image files.</span><span class="sxs-lookup"><span data-stu-id="1c235-118">The tutorial page is entirely self-contained; it does not use any external frameworks, style sheets, or image files.</span></span> <span data-ttu-id="1c235-119">It uses only widely supported JavaScript language features and works with current versions of all major Web browsers.</span><span class="sxs-lookup"><span data-stu-id="1c235-119">It uses only widely supported JavaScript language features and works with current versions of all major Web browsers.</span></span>

<span data-ttu-id="1c235-120">In this tutorial, we discuss selected portions of the source code.</span><span class="sxs-lookup"><span data-stu-id="1c235-120">In this tutorial, we discuss selected portions of the source code.</span></span> <span data-ttu-id="1c235-121">The complete [source code](tutorial-bing-video-search-single-page-app-source.md) is available.</span><span class="sxs-lookup"><span data-stu-id="1c235-121">The complete [source code](tutorial-bing-video-search-single-page-app-source.md) is available.</span></span> <span data-ttu-id="1c235-122">To run the example, copy and paste the source code into a text editor and save it as `bing.html`.</span><span class="sxs-lookup"><span data-stu-id="1c235-122">To run the example, copy and paste the source code into a text editor and save it as `bing.html`.</span></span>

## <a name="app-components"></a><span data-ttu-id="1c235-123">App components</span><span class="sxs-lookup"><span data-stu-id="1c235-123">App components</span></span>
<span data-ttu-id="1c235-124">Like any single-page Web app, this tutorial application includes three parts:</span><span class="sxs-lookup"><span data-stu-id="1c235-124">Like any single-page Web app, this tutorial application includes three parts:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1c235-125">HTML - Defines the structure and content of the page</span><span class="sxs-lookup"><span data-stu-id="1c235-125">HTML - Defines the structure and content of the page</span></span>
> * <span data-ttu-id="1c235-126">CSS - Defines the appearance of the page</span><span class="sxs-lookup"><span data-stu-id="1c235-126">CSS - Defines the appearance of the page</span></span>
> * <span data-ttu-id="1c235-127">JavaScript - Defines the behavior of the page</span><span class="sxs-lookup"><span data-stu-id="1c235-127">JavaScript - Defines the behavior of the page</span></span>

<span data-ttu-id="1c235-128">Most of the HTML and CSS is conventional, so the tutorial doesn't discuss it.</span><span class="sxs-lookup"><span data-stu-id="1c235-128">Most of the HTML and CSS is conventional, so the tutorial doesn't discuss it.</span></span> <span data-ttu-id="1c235-129">The HTML contains the search form in which the user enters a query and chooses search options.</span><span class="sxs-lookup"><span data-stu-id="1c235-129">The HTML contains the search form in which the user enters a query and chooses search options.</span></span> <span data-ttu-id="1c235-130">The form is connected to JavaScript that does the search using the `onsubmit` attribute of the `<form>` tag:</span><span class="sxs-lookup"><span data-stu-id="1c235-130">The form is connected to JavaScript that does the search using the `onsubmit` attribute of the `<form>` tag:</span></span>

```html
<form name="bing" onsubmit="return bingWebSearch(this)">
```
<span data-ttu-id="1c235-131">The `onsubmit` handler returns `false`, which keeps the form from being submitted to a server.</span><span class="sxs-lookup"><span data-stu-id="1c235-131">The `onsubmit` handler returns `false`, which keeps the form from being submitted to a server.</span></span> <span data-ttu-id="1c235-132">The JavaScript code does the work of collecting the necessary information from the form and performing the search.</span><span class="sxs-lookup"><span data-stu-id="1c235-132">The JavaScript code does the work of collecting the necessary information from the form and performing the search.</span></span>

<span data-ttu-id="1c235-133">The HTML also contains the divisions (HTML `<div>` tags) where the search results appear.</span><span class="sxs-lookup"><span data-stu-id="1c235-133">The HTML also contains the divisions (HTML `<div>` tags) where the search results appear.</span></span>

## <a name="managing-subscription-key"></a><span data-ttu-id="1c235-134">Managing subscription key</span><span class="sxs-lookup"><span data-stu-id="1c235-134">Managing subscription key</span></span>

<span data-ttu-id="1c235-135">To avoid having to include the Bing Search API subscription key in the code, we use the browser's persistent storage to store the key.</span><span class="sxs-lookup"><span data-stu-id="1c235-135">To avoid having to include the Bing Search API subscription key in the code, we use the browser's persistent storage to store the key.</span></span> <span data-ttu-id="1c235-136">Before the key is stored, we prompt for the user's key.</span><span class="sxs-lookup"><span data-stu-id="1c235-136">Before the key is stored, we prompt for the user's key.</span></span> <span data-ttu-id="1c235-137">If the key is later rejected by the API, we invalidate the stored key so the user will be prompted again.</span><span class="sxs-lookup"><span data-stu-id="1c235-137">If the key is later rejected by the API, we invalidate the stored key so the user will be prompted again.</span></span>

<span data-ttu-id="1c235-138">We define `storeValue` and `retrieveValue` functions that use either the `localStorage` object (not all browsers support it) or a cookie.</span><span class="sxs-lookup"><span data-stu-id="1c235-138">We define `storeValue` and `retrieveValue` functions that use either the `localStorage` object (not all browsers support it) or a cookie.</span></span> <span data-ttu-id="1c235-139">The `getSubscriptionKey()` function uses these functions to store and retrieve the user's key.</span><span class="sxs-lookup"><span data-stu-id="1c235-139">The `getSubscriptionKey()` function uses these functions to store and retrieve the user's key.</span></span>

``` javascript
// Cookie names for data we store
API_KEY_COOKIE   = "bing-search-api-key";
CLIENT_ID_COOKIE = "bing-search-client-id";

// ... omitted definitions of store value and retrieve value
// Browsers differ in their support for persistent storage by 
// local HTML files. See the source code for browser-specific
// options.

// Get stored API subscription key, or prompt if it's not found.
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
<span data-ttu-id="1c235-140">The HTML `<form>` tag `onsubmit` calls the `bingWebSearch` function to return search results.</span><span class="sxs-lookup"><span data-stu-id="1c235-140">The HTML `<form>` tag `onsubmit` calls the `bingWebSearch` function to return search results.</span></span> <span data-ttu-id="1c235-141">`bingWebSearch` uses `getSubscriptionKey()` to authenticate each query.</span><span class="sxs-lookup"><span data-stu-id="1c235-141">`bingWebSearch` uses `getSubscriptionKey()` to authenticate each query.</span></span> <span data-ttu-id="1c235-142">As shown in the previous definition, `getSubscriptionKey` prompts the user for the key if the key hasn't been entered.</span><span class="sxs-lookup"><span data-stu-id="1c235-142">As shown in the previous definition, `getSubscriptionKey` prompts the user for the key if the key hasn't been entered.</span></span> <span data-ttu-id="1c235-143">The key is then stored for continuing use by the application.</span><span class="sxs-lookup"><span data-stu-id="1c235-143">The key is then stored for continuing use by the application.</span></span>

```html
<form name="bing" onsubmit="this.offset.value = 0; return bingWebSearch(this.query.value, 
    bingSearchOptions(this), getSubscriptionKey())">
```
## <a name="selecting-search-options"></a><span data-ttu-id="1c235-144">Selecting search options</span><span class="sxs-lookup"><span data-stu-id="1c235-144">Selecting search options</span></span>
<span data-ttu-id="1c235-145">The following figure shows the query text box and options that define a search.</span><span class="sxs-lookup"><span data-stu-id="1c235-145">The following figure shows the query text box and options that define a search.</span></span>

![Bing News Search options](media/video-search-options.png)

<span data-ttu-id="1c235-147">The HTML form includes elements with the following names:</span><span class="sxs-lookup"><span data-stu-id="1c235-147">The HTML form includes elements with the following names:</span></span>

|<span data-ttu-id="1c235-148">Element</span><span class="sxs-lookup"><span data-stu-id="1c235-148">Element</span></span>|<span data-ttu-id="1c235-149">Description</span><span class="sxs-lookup"><span data-stu-id="1c235-149">Description</span></span>|
|-|-|
| `where` | <span data-ttu-id="1c235-150">A drop-down menu for selecting the market (location and language) used for the search.</span><span class="sxs-lookup"><span data-stu-id="1c235-150">A drop-down menu for selecting the market (location and language) used for the search.</span></span> |
| `query` | <span data-ttu-id="1c235-151">The text field to enter the search terms.</span><span class="sxs-lookup"><span data-stu-id="1c235-151">The text field to enter the search terms.</span></span> |
| `modules` | <span data-ttu-id="1c235-152">Checkboxes for promoting particular modules of results, all results or related videos.</span><span class="sxs-lookup"><span data-stu-id="1c235-152">Checkboxes for promoting particular modules of results, all results or related videos.</span></span> |
| `when` | <span data-ttu-id="1c235-153">Drop-down menu for optionally limiting the search to the most recent day, week, or month.</span><span class="sxs-lookup"><span data-stu-id="1c235-153">Drop-down menu for optionally limiting the search to the most recent day, week, or month.</span></span> |
| `safe` | <span data-ttu-id="1c235-154">A checkbox indicating whether to use the Bing SafeSearch feature to filter out "adult" results.</span><span class="sxs-lookup"><span data-stu-id="1c235-154">A checkbox indicating whether to use the Bing SafeSearch feature to filter out "adult" results.</span></span> |
| `count` | <span data-ttu-id="1c235-155">Hidden field.</span><span class="sxs-lookup"><span data-stu-id="1c235-155">Hidden field.</span></span> <span data-ttu-id="1c235-156">The number of search results to return on each request.</span><span class="sxs-lookup"><span data-stu-id="1c235-156">The number of search results to return on each request.</span></span> <span data-ttu-id="1c235-157">Change to display fewer or more results per page.</span><span class="sxs-lookup"><span data-stu-id="1c235-157">Change to display fewer or more results per page.</span></span> |
| `offset`|  <span data-ttu-id="1c235-158">Hidden field.</span><span class="sxs-lookup"><span data-stu-id="1c235-158">Hidden field.</span></span> <span data-ttu-id="1c235-159">The offset of the first search result in the request; used for paging.</span><span class="sxs-lookup"><span data-stu-id="1c235-159">The offset of the first search result in the request; used for paging.</span></span> <span data-ttu-id="1c235-160">It's reset to `0` on a new request.</span><span class="sxs-lookup"><span data-stu-id="1c235-160">It's reset to `0` on a new request.</span></span> |

> [!NOTE]
> <span data-ttu-id="1c235-161">Bing Web Search offers other query parameters.</span><span class="sxs-lookup"><span data-stu-id="1c235-161">Bing Web Search offers other query parameters.</span></span> <span data-ttu-id="1c235-162">We're using only a few of them.</span><span class="sxs-lookup"><span data-stu-id="1c235-162">We're using only a few of them.</span></span>

``` javascript
// build query options from the HTML form
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
        options.push("modules=" + what.join(","));
        options.push("answerCount=9");
    }
    options.push("count=" + form.count.value);
    options.push("offset=" + form.offset.value);
    options.push("textDecorations=true");
    options.push("textFormat=HTML");
    return options.join("&");
}
```

<span data-ttu-id="1c235-163">For example, the `SafeSearch` parameter in an actual API call can be `strict`, `moderate`, or `off`, with `moderate` being the default.</span><span class="sxs-lookup"><span data-stu-id="1c235-163">For example, the `SafeSearch` parameter in an actual API call can be `strict`, `moderate`, or `off`, with `moderate` being the default.</span></span> <span data-ttu-id="1c235-164">Our form, however, uses a checkbox, which has only two states.</span><span class="sxs-lookup"><span data-stu-id="1c235-164">Our form, however, uses a checkbox, which has only two states.</span></span> <span data-ttu-id="1c235-165">The JavaScript code converts this setting to either `strict` or `off` (`moderate` is not used).</span><span class="sxs-lookup"><span data-stu-id="1c235-165">The JavaScript code converts this setting to either `strict` or `off` (`moderate` is not used).</span></span>

## <a name="performing-the-request"></a><span data-ttu-id="1c235-166">Performing the request</span><span class="sxs-lookup"><span data-stu-id="1c235-166">Performing the request</span></span>
<span data-ttu-id="1c235-167">Given the query, the options string, and the API key, the `BingWebSearch` function uses an `XMLHttpRequest` object to make the request to the Bing Search endpoint.</span><span class="sxs-lookup"><span data-stu-id="1c235-167">Given the query, the options string, and the API key, the `BingWebSearch` function uses an `XMLHttpRequest` object to make the request to the Bing Search endpoint.</span></span>

```javascript
// Search on the query, using search options, authenticated by the key.
function bingWebSearch(query, options, key) {

    // scroll to top of window
    window.scrollTo(0, 0);
    if (!query.trim().length) return false;     // empty query, do nothing

    showDiv("noresults", "Working. Please wait.");
    hideDivs("pole", "mainline", "sidebar", "_json", "_headers", "paging1", "paging2", "error");

    var endpoint = "https://api.cognitive.microsoft.com/bing/v7.0/videos/search";
    var request = new XMLHttpRequest();
    var queryurl = endpoint + "?q=" + encodeURIComponent(query) + "&" + options;

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
    request.addEventListener("load", handleOnLoad);

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
<span data-ttu-id="1c235-168">On successful completion of the HTTP request, JavaScript calls the `load` event handler, `handleOnLoad()`, to handle a successful HTTP GET request to the API.</span><span class="sxs-lookup"><span data-stu-id="1c235-168">On successful completion of the HTTP request, JavaScript calls the `load` event handler, `handleOnLoad()`, to handle a successful HTTP GET request to the API.</span></span> 

```javascript
// handle Bing search request results
function handleOnLoad() {
    hideDivs("noresults");

    var json = this.responseText.trim();
    var jsobj = {};

    // try to parse JSON results
    try {
        if (json.length) jsobj = JSON.parse(json);
    } catch(e) {
        renderErrorMessage("Invalid JSON response");
    }

    // show raw JSON and headers
    showDiv("json", preFormat(JSON.stringify(jsobj, null, 2)));
    showDiv("http", preFormat("GET " + this.responseURL + "\n\nStatus: " + this.status + " " + 
        this.statusText + "\n" + this.getAllResponseHeaders()));

    // if HTTP response is 200 OK, try to render search results
    if (this.status === 200) {
        var clientid = this.getResponseHeader("X-MSEdge-ClientID");
        if (clientid) retrieveValue(CLIENT_ID_COOKIE, clientid);
        if (json.length) {
            if (jsobj._type === "Videos") {//"SearchResponse" && "rankingResponse" in jsobj) {
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
> <span data-ttu-id="1c235-169">If an error occurs in the search operation, the Bing News Search API returns a non-200 HTTP status code and includes error information in the JSON response.</span><span class="sxs-lookup"><span data-stu-id="1c235-169">If an error occurs in the search operation, the Bing News Search API returns a non-200 HTTP status code and includes error information in the JSON response.</span></span> <span data-ttu-id="1c235-170">Additionally, if the request was rate-limited, the API returns an empty response.</span><span class="sxs-lookup"><span data-stu-id="1c235-170">Additionally, if the request was rate-limited, the API returns an empty response.</span></span>
<span data-ttu-id="1c235-171">A successful HTTP request does *not* necessarily mean that the search itself succeeded.</span><span class="sxs-lookup"><span data-stu-id="1c235-171">A successful HTTP request does *not* necessarily mean that the search itself succeeded.</span></span> 

<span data-ttu-id="1c235-172">Much of the code in both of the preceding functions is dedicated to error handling.</span><span class="sxs-lookup"><span data-stu-id="1c235-172">Much of the code in both of the preceding functions is dedicated to error handling.</span></span> <span data-ttu-id="1c235-173">Errors may occur at the following stages:</span><span class="sxs-lookup"><span data-stu-id="1c235-173">Errors may occur at the following stages:</span></span>

|<span data-ttu-id="1c235-174">Stage</span><span class="sxs-lookup"><span data-stu-id="1c235-174">Stage</span></span>|<span data-ttu-id="1c235-175">Potential error(s)</span><span class="sxs-lookup"><span data-stu-id="1c235-175">Potential error(s)</span></span>|<span data-ttu-id="1c235-176">Handled by</span><span class="sxs-lookup"><span data-stu-id="1c235-176">Handled by</span></span>|
|-|-|-|
|<span data-ttu-id="1c235-177">Building the JavaScript request object</span><span class="sxs-lookup"><span data-stu-id="1c235-177">Building the JavaScript request object</span></span>|<span data-ttu-id="1c235-178">Invalid URL</span><span class="sxs-lookup"><span data-stu-id="1c235-178">Invalid URL</span></span>|<span data-ttu-id="1c235-179">`try`/`catch` block</span><span class="sxs-lookup"><span data-stu-id="1c235-179">`try`/`catch` block</span></span>|
|<span data-ttu-id="1c235-180">Making the request</span><span class="sxs-lookup"><span data-stu-id="1c235-180">Making the request</span></span>|<span data-ttu-id="1c235-181">Network errors, aborted connections</span><span class="sxs-lookup"><span data-stu-id="1c235-181">Network errors, aborted connections</span></span>|<span data-ttu-id="1c235-182">`error` and `abort` event handlers</span><span class="sxs-lookup"><span data-stu-id="1c235-182">`error` and `abort` event handlers</span></span>|
|<span data-ttu-id="1c235-183">Performing the search</span><span class="sxs-lookup"><span data-stu-id="1c235-183">Performing the search</span></span>|<span data-ttu-id="1c235-184">Invalid request, invalid JSON, rate limits</span><span class="sxs-lookup"><span data-stu-id="1c235-184">Invalid request, invalid JSON, rate limits</span></span>|<span data-ttu-id="1c235-185">tests in `load` event handler</span><span class="sxs-lookup"><span data-stu-id="1c235-185">tests in `load` event handler</span></span>|

<span data-ttu-id="1c235-186">Errors are handled by calling `renderErrorMessage()` with any details known about the error.</span><span class="sxs-lookup"><span data-stu-id="1c235-186">Errors are handled by calling `renderErrorMessage()` with any details known about the error.</span></span> <span data-ttu-id="1c235-187">If the response passes the full gauntlet of error tests, we call `renderSearchResults()` to display the search results in the page.</span><span class="sxs-lookup"><span data-stu-id="1c235-187">If the response passes the full gauntlet of error tests, we call `renderSearchResults()` to display the search results in the page.</span></span>

## <a name="displaying-search-results"></a><span data-ttu-id="1c235-188">Displaying search results</span><span class="sxs-lookup"><span data-stu-id="1c235-188">Displaying search results</span></span>
<span data-ttu-id="1c235-189">The main function for displaying the search results is `renderSearchResults()`.</span><span class="sxs-lookup"><span data-stu-id="1c235-189">The main function for displaying the search results is `renderSearchResults()`.</span></span> <span data-ttu-id="1c235-190">This function takes the JSON returned by the Bing News Search service and renders the news results and the related searches, if any.</span><span class="sxs-lookup"><span data-stu-id="1c235-190">This function takes the JSON returned by the Bing News Search service and renders the news results and the related searches, if any.</span></span>

```javascript
// render the search results given the parsed JSON response
function renderSearchResults(results) {

    // add Prev / Next links with result count
    var pagingLinks = renderPagingLinks(results);
    showDiv("paging1", pagingLinks);
    showDiv("paging2", pagingLinks);

    // Render the resuts to the mainline section
    for (section in { mainline: 0 }) {
         showDiv(section, renderResultsItems(section, results));
    }
}
```
<span data-ttu-id="1c235-191">The search results are returned as the top-level `value` object in the JSON response.</span><span class="sxs-lookup"><span data-stu-id="1c235-191">The search results are returned as the top-level `value` object in the JSON response.</span></span> <span data-ttu-id="1c235-192">We pass them to our function `renderResultsItems()`, which iterates through them and calls a function to render each item into HTML.</span><span class="sxs-lookup"><span data-stu-id="1c235-192">We pass them to our function `renderResultsItems()`, which iterates through them and calls a function to render each item into HTML.</span></span> <span data-ttu-id="1c235-193">The resulting HTML is returned to `renderSearchResults()`, where it is inserted into the `results` division in the page.</span><span class="sxs-lookup"><span data-stu-id="1c235-193">The resulting HTML is returned to `renderSearchResults()`, where it is inserted into the `results` division in the page.</span></span>

```javascript
// render search results
    function renderResultsItems(section, results) {   

        var items = results.value;
        var html = [];
        for (var i = 0; i < items.length; i++) { 
            var item = items[i];
            // collection name has lowercase first letter
            var type = "videos";
            var render = searchItemRenderers[type];
            html.push(render(item, section));  
        }
    return html.join("\n\n");
}
```

<span data-ttu-id="1c235-194">The Bing News Search API returns up to four different kinds of related results, each in its own top-level object.</span><span class="sxs-lookup"><span data-stu-id="1c235-194">The Bing News Search API returns up to four different kinds of related results, each in its own top-level object.</span></span> <span data-ttu-id="1c235-195">They are:</span><span class="sxs-lookup"><span data-stu-id="1c235-195">They are:</span></span>

|<span data-ttu-id="1c235-196">Relation</span><span class="sxs-lookup"><span data-stu-id="1c235-196">Relation</span></span>|<span data-ttu-id="1c235-197">Description</span><span class="sxs-lookup"><span data-stu-id="1c235-197">Description</span></span>|
|-|-|
|`pivotSuggestions`|<span data-ttu-id="1c235-198">Queries that replace a pivot word in original search with a different one.</span><span class="sxs-lookup"><span data-stu-id="1c235-198">Queries that replace a pivot word in original search with a different one.</span></span> <span data-ttu-id="1c235-199">For example, if you search for "red flowers," a pivot word might be "red," and a pivot suggestion might be "yellow flowers."</span><span class="sxs-lookup"><span data-stu-id="1c235-199">For example, if you search for "red flowers," a pivot word might be "red," and a pivot suggestion might be "yellow flowers."</span></span>|
|`queryExpansions`|<span data-ttu-id="1c235-200">Queries that narrow the original search by adding more terms.</span><span class="sxs-lookup"><span data-stu-id="1c235-200">Queries that narrow the original search by adding more terms.</span></span> <span data-ttu-id="1c235-201">For example, if you search for "Microsoft Surface," a query expansion might be "Microsoft Surface Pro."</span><span class="sxs-lookup"><span data-stu-id="1c235-201">For example, if you search for "Microsoft Surface," a query expansion might be "Microsoft Surface Pro."</span></span>|
|`relatedSearches`|<span data-ttu-id="1c235-202">Queries that have also been entered by other users who entered the original search.</span><span class="sxs-lookup"><span data-stu-id="1c235-202">Queries that have also been entered by other users who entered the original search.</span></span> <span data-ttu-id="1c235-203">For example, if you search for "Mount Rainier," a related search might be "Mt.</span><span class="sxs-lookup"><span data-stu-id="1c235-203">For example, if you search for "Mount Rainier," a related search might be "Mt.</span></span> <span data-ttu-id="1c235-204">Saint Helens."</span><span class="sxs-lookup"><span data-stu-id="1c235-204">Saint Helens."</span></span>|
|`similarTerms`|<span data-ttu-id="1c235-205">Queries that are similar in meaning to the original search.</span><span class="sxs-lookup"><span data-stu-id="1c235-205">Queries that are similar in meaning to the original search.</span></span> <span data-ttu-id="1c235-206">For example, if you search for "schools," a similar term might be "education."</span><span class="sxs-lookup"><span data-stu-id="1c235-206">For example, if you search for "schools," a similar term might be "education."</span></span>|

<span data-ttu-id="1c235-207">As previously seen in `renderSearchResults()`, we render only the `relatedItems` suggestions and place the resulting links in the page's sidebar.</span><span class="sxs-lookup"><span data-stu-id="1c235-207">As previously seen in `renderSearchResults()`, we render only the `relatedItems` suggestions and place the resulting links in the page's sidebar.</span></span>

## <a name="rendering-result-items"></a><span data-ttu-id="1c235-208">Rendering result items</span><span class="sxs-lookup"><span data-stu-id="1c235-208">Rendering result items</span></span>

<span data-ttu-id="1c235-209">In the JavaScript code the object, `searchItemRenderers`, can contains *renderers:* functions that generate HTML for each kind of search result.</span><span class="sxs-lookup"><span data-stu-id="1c235-209">In the JavaScript code the object, `searchItemRenderers`, can contains *renderers:* functions that generate HTML for each kind of search result.</span></span> <span data-ttu-id="1c235-210">The video search page only uses `videos`.</span><span class="sxs-lookup"><span data-stu-id="1c235-210">The video search page only uses `videos`.</span></span> <span data-ttu-id="1c235-211">See other tutorials for various types of renderers.</span><span class="sxs-lookup"><span data-stu-id="1c235-211">See other tutorials for various types of renderers.</span></span>

```javascript
searchItemRenderers = {
    news: function(item) { ... },
    webPages: function (item) { ... }, 
    images: function(item, index, count) { ... },
    videos: function (item, section, index, count) { ... },
    relatedSearches: function(item) { ... }
}
```
<span data-ttu-id="1c235-212">A renderer function can accept the following parameters:</span><span class="sxs-lookup"><span data-stu-id="1c235-212">A renderer function can accept the following parameters:</span></span>

|<span data-ttu-id="1c235-213">Parameter</span><span class="sxs-lookup"><span data-stu-id="1c235-213">Parameter</span></span>|<span data-ttu-id="1c235-214">Description</span><span class="sxs-lookup"><span data-stu-id="1c235-214">Description</span></span>|
|-|-|
|`item`| <span data-ttu-id="1c235-215">The JavaScript object containing the item's properties, such as its URL and its description.</span><span class="sxs-lookup"><span data-stu-id="1c235-215">The JavaScript object containing the item's properties, such as its URL and its description.</span></span>|
|`index`| <span data-ttu-id="1c235-216">The index of the result item within its collection.</span><span class="sxs-lookup"><span data-stu-id="1c235-216">The index of the result item within its collection.</span></span>|
|`count`| <span data-ttu-id="1c235-217">The number of items in the search result item's collection.</span><span class="sxs-lookup"><span data-stu-id="1c235-217">The number of items in the search result item's collection.</span></span>|

<span data-ttu-id="1c235-218">The `index` and `count` parameters can be used to number results, to generate special HTML for the beginning or end of a collection, to insert line breaks after a certain number of items, and so on.</span><span class="sxs-lookup"><span data-stu-id="1c235-218">The `index` and `count` parameters can be used to number results, to generate special HTML for the beginning or end of a collection, to insert line breaks after a certain number of items, and so on.</span></span> <span data-ttu-id="1c235-219">If a renderer does not need this functionality, it does not need to accept these two parameters.</span><span class="sxs-lookup"><span data-stu-id="1c235-219">If a renderer does not need this functionality, it does not need to accept these two parameters.</span></span>

<span data-ttu-id="1c235-220">The `video` renderer is shown in the following javascript excerpt.</span><span class="sxs-lookup"><span data-stu-id="1c235-220">The `video` renderer is shown in the following javascript excerpt.</span></span> <span data-ttu-id="1c235-221">Using the Videos endpoint, all results are of type `Videos`.</span><span class="sxs-lookup"><span data-stu-id="1c235-221">Using the Videos endpoint, all results are of type `Videos`.</span></span> <span data-ttu-id="1c235-222">The `searchItemRenderers` are shown in the following code segment.</span><span class="sxs-lookup"><span data-stu-id="1c235-222">The `searchItemRenderers` are shown in the following code segment.</span></span>

```javascript
// render functions for various types of search results
    searchItemRenderers = {

    videos: function (item, section, index, count) {
        var height = 60;
        var width = Math.round(height * item.thumbnail.width / item.thumbnail.height);
        var html = [];

        html.push("<p class='images'>");
        html.push("<a href='" + item.hostPageUrl + "'>");
        var title = escapeQuotes(item.name) + "\n" + getHost(item.hostPageDisplayUrl);
        html.push("<img src='" + item.thumbnailUrl + "&h=" + height + "&w=" + width +
            "' height=" + height + " width=" + width + " title='" + title + "' alt='" + title + "'>");
        html.push("</a>");
        html.push("<br>");
        html.push("<nobr><a href='" + item.contentUrl + "'>Video page source</a> - ");
        html.push(title.replace("\n", " (").replace(/([a-z0-9])\.([a-z0-9])/g, "$1.<wbr>$2") + ")</p>");
        return html.join("");
    }
}
```

<span data-ttu-id="1c235-223">The renderer function:</span><span class="sxs-lookup"><span data-stu-id="1c235-223">The renderer function:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="1c235-224">Creates a paragraph tag, assigns it to the `images` class, and pushes it to the html array.</span><span class="sxs-lookup"><span data-stu-id="1c235-224">Creates a paragraph tag, assigns it to the `images` class, and pushes it to the html array.</span></span>
> * <span data-ttu-id="1c235-225">Calculates image thumbnail size (width is fixed at 60 pixels, height calculated proportionately).</span><span class="sxs-lookup"><span data-stu-id="1c235-225">Calculates image thumbnail size (width is fixed at 60 pixels, height calculated proportionately).</span></span>
> * <span data-ttu-id="1c235-226">Builds the HTML `<img>` tag to display the image thumbnail.</span><span class="sxs-lookup"><span data-stu-id="1c235-226">Builds the HTML `<img>` tag to display the image thumbnail.</span></span> 
> * <span data-ttu-id="1c235-227">Builds the HTML `<a>` tags that link to the image and the page that contains it.</span><span class="sxs-lookup"><span data-stu-id="1c235-227">Builds the HTML `<a>` tags that link to the image and the page that contains it.</span></span>
> * <span data-ttu-id="1c235-228">Builds the description that displays information about the image and the site it's on.</span><span class="sxs-lookup"><span data-stu-id="1c235-228">Builds the description that displays information about the image and the site it's on.</span></span>

<span data-ttu-id="1c235-229">The thumbnail size is used in both the `<img>` tag and the `h` and `w` fields in the thumbnail's URL.</span><span class="sxs-lookup"><span data-stu-id="1c235-229">The thumbnail size is used in both the `<img>` tag and the `h` and `w` fields in the thumbnail's URL.</span></span> <span data-ttu-id="1c235-230">The [Bing thumbnail service](resize-and-crop-thumbnails.md) then delivers a thumbnail of exactly that size.</span><span class="sxs-lookup"><span data-stu-id="1c235-230">The [Bing thumbnail service](resize-and-crop-thumbnails.md) then delivers a thumbnail of exactly that size.</span></span>

## <a name="persisting-client-id"></a><span data-ttu-id="1c235-231">Persisting client ID</span><span class="sxs-lookup"><span data-stu-id="1c235-231">Persisting client ID</span></span>
<span data-ttu-id="1c235-232">Responses from the Bing search APIs may include an `X-MSEdge-ClientID` header that should be sent back to the API with successive requests.</span><span class="sxs-lookup"><span data-stu-id="1c235-232">Responses from the Bing search APIs may include an `X-MSEdge-ClientID` header that should be sent back to the API with successive requests.</span></span> <span data-ttu-id="1c235-233">If multiple Bing Search APIs are being used, the same client ID should be used with all of them, if possible.</span><span class="sxs-lookup"><span data-stu-id="1c235-233">If multiple Bing Search APIs are being used, the same client ID should be used with all of them, if possible.</span></span>

<span data-ttu-id="1c235-234">Providing the `X-MSEdge-ClientID` header allows the Bing APIs to associate all of a user's searches, which has two important benefits.</span><span class="sxs-lookup"><span data-stu-id="1c235-234">Providing the `X-MSEdge-ClientID` header allows the Bing APIs to associate all of a user's searches, which has two important benefits.</span></span>

<span data-ttu-id="1c235-235">First, it allows the Bing search engine to apply past context to searches to find results that better satisfy the user.</span><span class="sxs-lookup"><span data-stu-id="1c235-235">First, it allows the Bing search engine to apply past context to searches to find results that better satisfy the user.</span></span> <span data-ttu-id="1c235-236">If a user has previously searched for terms related to sailing, for example, a later search for "knots" might preferentially return information about knots used in sailing.</span><span class="sxs-lookup"><span data-stu-id="1c235-236">If a user has previously searched for terms related to sailing, for example, a later search for "knots" might preferentially return information about knots used in sailing.</span></span>

<span data-ttu-id="1c235-237">Second, Bing may randomly select users to experience new features before they are made widely available.</span><span class="sxs-lookup"><span data-stu-id="1c235-237">Second, Bing may randomly select users to experience new features before they are made widely available.</span></span> <span data-ttu-id="1c235-238">Providing the same client ID with each request ensures that users who see the feature always see it.</span><span class="sxs-lookup"><span data-stu-id="1c235-238">Providing the same client ID with each request ensures that users who see the feature always see it.</span></span> <span data-ttu-id="1c235-239">Without the client ID, the user might see a feature appear and disappear, seemingly at random, in their search results.</span><span class="sxs-lookup"><span data-stu-id="1c235-239">Without the client ID, the user might see a feature appear and disappear, seemingly at random, in their search results.</span></span>

<span data-ttu-id="1c235-240">Browser security policies (CORS) may prevent the `X-MSEdge-ClientID` header from being available to JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1c235-240">Browser security policies (CORS) may prevent the `X-MSEdge-ClientID` header from being available to JavaScript.</span></span> <span data-ttu-id="1c235-241">This limitation occurs when the search response has a different origin from the page that requested it.</span><span class="sxs-lookup"><span data-stu-id="1c235-241">This limitation occurs when the search response has a different origin from the page that requested it.</span></span> <span data-ttu-id="1c235-242">In a production environment, you should address this policy by hosting a server-side script that does the API call on the same domain as the Web page.</span><span class="sxs-lookup"><span data-stu-id="1c235-242">In a production environment, you should address this policy by hosting a server-side script that does the API call on the same domain as the Web page.</span></span> <span data-ttu-id="1c235-243">Since the script has the same origin as the Web page, the `X-MSEdge-ClientID` header is then available to JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1c235-243">Since the script has the same origin as the Web page, the `X-MSEdge-ClientID` header is then available to JavaScript.</span></span>

> [!NOTE]
> <span data-ttu-id="1c235-244">In a production Web application, you should perform the request server-side.</span><span class="sxs-lookup"><span data-stu-id="1c235-244">In a production Web application, you should perform the request server-side.</span></span> <span data-ttu-id="1c235-245">Otherwise, your Bing Search API key must be included in the Web page, where it is available to anyone who views source.</span><span class="sxs-lookup"><span data-stu-id="1c235-245">Otherwise, your Bing Search API key must be included in the Web page, where it is available to anyone who views source.</span></span> <span data-ttu-id="1c235-246">You are billed for all usage under your API subscription key, even requests made by unauthorized parties, so it is important not to expose your key.</span><span class="sxs-lookup"><span data-stu-id="1c235-246">You are billed for all usage under your API subscription key, even requests made by unauthorized parties, so it is important not to expose your key.</span></span>

<span data-ttu-id="1c235-247">For development purposes, you can make the Bing Web Search API request through a CORS proxy.</span><span class="sxs-lookup"><span data-stu-id="1c235-247">For development purposes, you can make the Bing Web Search API request through a CORS proxy.</span></span> <span data-ttu-id="1c235-248">The response from such a proxy has an `Access-Control-Expose-Headers` header that whitelists response headers and makes them available to JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1c235-248">The response from such a proxy has an `Access-Control-Expose-Headers` header that whitelists response headers and makes them available to JavaScript.</span></span>

<span data-ttu-id="1c235-249">It's easy to install a CORS proxy to allow our tutorial app to access the client ID header.</span><span class="sxs-lookup"><span data-stu-id="1c235-249">It's easy to install a CORS proxy to allow our tutorial app to access the client ID header.</span></span> <span data-ttu-id="1c235-250">First, if you don't already have it, [install Node.js](https://nodejs.org/en/download/).</span><span class="sxs-lookup"><span data-stu-id="1c235-250">First, if you don't already have it, [install Node.js](https://nodejs.org/en/download/).</span></span> <span data-ttu-id="1c235-251">Then issue the following command in a command window:</span><span class="sxs-lookup"><span data-stu-id="1c235-251">Then issue the following command in a command window:</span></span>

    npm install -g cors-proxy-server

<span data-ttu-id="1c235-252">Next, change the Bing Web Search endpoint in the HTML file to:</span><span class="sxs-lookup"><span data-stu-id="1c235-252">Next, change the Bing Web Search endpoint in the HTML file to:</span></span>

    http://localhost:9090/https://api.cognitive.microsoft.com/bing/v7.0/search

<span data-ttu-id="1c235-253">Finally, start the CORS proxy with the following command:</span><span class="sxs-lookup"><span data-stu-id="1c235-253">Finally, start the CORS proxy with the following command:</span></span>

    cors-proxy-server

<span data-ttu-id="1c235-254">Leave the command window open while you use the tutorial app; closing the window stops the proxy.</span><span class="sxs-lookup"><span data-stu-id="1c235-254">Leave the command window open while you use the tutorial app; closing the window stops the proxy.</span></span> <span data-ttu-id="1c235-255">In the expandable HTTP Headers section below the search results, you can now see the `X-MSEdge-ClientID` header (among others) and verify that it is the same for each request.</span><span class="sxs-lookup"><span data-stu-id="1c235-255">In the expandable HTTP Headers section below the search results, you can now see the `X-MSEdge-ClientID` header (among others) and verify that it is the same for each request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c235-256">Next steps</span><span class="sxs-lookup"><span data-stu-id="1c235-256">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="1c235-257">Bing Video Search API reference</span><span class="sxs-lookup"><span data-stu-id="1c235-257">Bing Video Search API reference</span></span>](//docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference)