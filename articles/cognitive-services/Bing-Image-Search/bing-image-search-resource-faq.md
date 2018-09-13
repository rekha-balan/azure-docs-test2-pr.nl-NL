---
title: Frequently Asked Questions (FAQ) about Bing Image Search API on Azure | Microsoft Docs
description: Get answers to common questions about Microsoft Cognitive Services Bing Image Search API on Azure.
services: cognitive-services
author: v-jerkin
manager: jhubbard
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: article
ms.date: 10/06/2017
ms.author: v-jerkin
ms.openlocfilehash: 15d3def94312fbde0bf3443cba54edfacafa7ab3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870994"
---
# <a name="frequently-asked-questions-faq-about-bing-image-search-api-cognitive-services"></a><span data-ttu-id="bdf86-103">Frequently asked questions (FAQ) about Bing Image Search API (Cognitive Services)</span><span class="sxs-lookup"><span data-stu-id="bdf86-103">Frequently asked questions (FAQ) about Bing Image Search API (Cognitive Services)</span></span>
 
<span data-ttu-id="bdf86-104">Find answers to commonly asked questions about concepts, code, and scenarios related to the Bing Image Search API for Microsoft Cognitive Services on Azure.</span><span class="sxs-lookup"><span data-stu-id="bdf86-104">Find answers to commonly asked questions about concepts, code, and scenarios related to the Bing Image Search API for Microsoft Cognitive Services on Azure.</span></span>

## <a name="response-headers-in-javascript"></a><span data-ttu-id="bdf86-105">Response headers in JavaScript</span><span class="sxs-lookup"><span data-stu-id="bdf86-105">Response headers in JavaScript</span></span>

<span data-ttu-id="bdf86-106">The following headers may occur in responses from the Bing Image Search API.</span><span class="sxs-lookup"><span data-stu-id="bdf86-106">The following headers may occur in responses from the Bing Image Search API.</span></span>

|||
|-|-|
|`X-MSEdge-ClientID`|<span data-ttu-id="bdf86-107">The unique ID that Bing has assigned to the user</span><span class="sxs-lookup"><span data-stu-id="bdf86-107">The unique ID that Bing has assigned to the user</span></span>|
|`BingAPIs-Market`|<span data-ttu-id="bdf86-108">The market that was used to fulfill the request</span><span class="sxs-lookup"><span data-stu-id="bdf86-108">The market that was used to fulfill the request</span></span>|
|`BingAPIs-TraceId`|<span data-ttu-id="bdf86-109">The log entry on the Bing API server for this request (for support)</span><span class="sxs-lookup"><span data-stu-id="bdf86-109">The log entry on the Bing API server for this request (for support)</span></span>|

<span data-ttu-id="bdf86-110">It is particularly important to persist the client ID and return it with subsequent requests.</span><span class="sxs-lookup"><span data-stu-id="bdf86-110">It is particularly important to persist the client ID and return it with subsequent requests.</span></span> <span data-ttu-id="bdf86-111">When you do this, the search will use past context in ranking search results and also provide a consistent user experience.</span><span class="sxs-lookup"><span data-stu-id="bdf86-111">When you do this, the search will use past context in ranking search results and also provide a consistent user experience.</span></span>

<span data-ttu-id="bdf86-112">However, when you call the Bing Image Search API from JavaScript, your browser's built-in security features (CORS) might prevent you from accessing the values of these headers.</span><span class="sxs-lookup"><span data-stu-id="bdf86-112">However, when you call the Bing Image Search API from JavaScript, your browser's built-in security features (CORS) might prevent you from accessing the values of these headers.</span></span>

<span data-ttu-id="bdf86-113">To gain access to the headers, you can make the Bing Image Search API request through a CORS proxy.</span><span class="sxs-lookup"><span data-stu-id="bdf86-113">To gain access to the headers, you can make the Bing Image Search API request through a CORS proxy.</span></span> <span data-ttu-id="bdf86-114">The response from such a proxy has an `Access-Control-Expose-Headers` header that whitelists response headers and makes them available to JavaScript.</span><span class="sxs-lookup"><span data-stu-id="bdf86-114">The response from such a proxy has an `Access-Control-Expose-Headers` header that whitelists response headers and makes them available to JavaScript.</span></span>

<span data-ttu-id="bdf86-115">It's easy to install a CORS proxy to allow our [tutorial app](tutorial-bing-image-search-single-page-app.md) to access the optional client headers.</span><span class="sxs-lookup"><span data-stu-id="bdf86-115">It's easy to install a CORS proxy to allow our [tutorial app](tutorial-bing-image-search-single-page-app.md) to access the optional client headers.</span></span> <span data-ttu-id="bdf86-116">First, if you don't already have it, [install Node.js](https://nodejs.org/en/download/).</span><span class="sxs-lookup"><span data-stu-id="bdf86-116">First, if you don't already have it, [install Node.js](https://nodejs.org/en/download/).</span></span> <span data-ttu-id="bdf86-117">Then enter the following command at a command prompt.</span><span class="sxs-lookup"><span data-stu-id="bdf86-117">Then enter the following command at a command prompt.</span></span>

    npm install -g cors-proxy-server

<span data-ttu-id="bdf86-118">Next, change the Bing Image Search API endpoint in the HTML file to:</span><span class="sxs-lookup"><span data-stu-id="bdf86-118">Next, change the Bing Image Search API endpoint in the HTML file to:</span></span>

    http://localhost:9090/https://api.cognitive.microsoft.com/bing/v7.0/search

<span data-ttu-id="bdf86-119">Finally, start the CORS proxy with the following command:</span><span class="sxs-lookup"><span data-stu-id="bdf86-119">Finally, start the CORS proxy with the following command:</span></span>

    cors-proxy-server

<span data-ttu-id="bdf86-120">Leave the command window open while you use the tutorial app; closing the window stops the proxy.</span><span class="sxs-lookup"><span data-stu-id="bdf86-120">Leave the command window open while you use the tutorial app; closing the window stops the proxy.</span></span> <span data-ttu-id="bdf86-121">In the expandable HTTP Headers section below the search results, you can now see the `X-MSEdge-ClientID` header (among others) and verify that it is the same for each request.</span><span class="sxs-lookup"><span data-stu-id="bdf86-121">In the expandable HTTP Headers section below the search results, you can now see the `X-MSEdge-ClientID` header (among others) and verify that it is the same for each request.</span></span>

## <a name="response-headers-in-production"></a><span data-ttu-id="bdf86-122">Response headers in production</span><span class="sxs-lookup"><span data-stu-id="bdf86-122">Response headers in production</span></span>

<span data-ttu-id="bdf86-123">The CORS proxy approach described in the previous answer is appropriate for development, testing, and learning.</span><span class="sxs-lookup"><span data-stu-id="bdf86-123">The CORS proxy approach described in the previous answer is appropriate for development, testing, and learning.</span></span> 

<span data-ttu-id="bdf86-124">In a production environment, however, you should host a server-side script on the same domain as the Web page that uses the Bing Web Search API.</span><span class="sxs-lookup"><span data-stu-id="bdf86-124">In a production environment, however, you should host a server-side script on the same domain as the Web page that uses the Bing Web Search API.</span></span> <span data-ttu-id="bdf86-125">This script should actually do the API calls upon request from the Web page JavaScript and pass all results, including headers, back to the client.</span><span class="sxs-lookup"><span data-stu-id="bdf86-125">This script should actually do the API calls upon request from the Web page JavaScript and pass all results, including headers, back to the client.</span></span> <span data-ttu-id="bdf86-126">Since the two resources (page and script) share an origin, CORS does not come into play and the special headers are acessible to the JavaScript on the Web page.</span><span class="sxs-lookup"><span data-stu-id="bdf86-126">Since the two resources (page and script) share an origin, CORS does not come into play and the special headers are acessible to the JavaScript on the Web page.</span></span> 

<span data-ttu-id="bdf86-127">This approach also protects your API key from exposure to the public, since only the server-side script needs it.</span><span class="sxs-lookup"><span data-stu-id="bdf86-127">This approach also protects your API key from exposure to the public, since only the server-side script needs it.</span></span> <span data-ttu-id="bdf86-128">The script can use another method (such as the HTTP referrer) to make sure the request is authorized.</span><span class="sxs-lookup"><span data-stu-id="bdf86-128">The script can use another method (such as the HTTP referrer) to make sure the request is authorized.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdf86-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="bdf86-129">Next steps</span></span>

<span data-ttu-id="bdf86-130">Is your question about a missing feature or functionality?</span><span class="sxs-lookup"><span data-stu-id="bdf86-130">Is your question about a missing feature or functionality?</span></span> <span data-ttu-id="bdf86-131">Consider requesting or voting for it on our [User Voice web site](https://cognitive.uservoice.com/forums/555907-bing-search).</span><span class="sxs-lookup"><span data-stu-id="bdf86-131">Consider requesting or voting for it on our [User Voice web site](https://cognitive.uservoice.com/forums/555907-bing-search).</span></span>

## <a name="see-also"></a><span data-ttu-id="bdf86-132">See also</span><span class="sxs-lookup"><span data-stu-id="bdf86-132">See also</span></span>

 [<span data-ttu-id="bdf86-133">Stack Overflow: Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="bdf86-133">Stack Overflow: Cognitive Services</span></span>](http://stackoverflow.com/questions/tagged/bing-api)