---
title: Frequently Asked Questions about the Bing Spell Check API - Azure Cognitive Services | Microsoft Docs
description: Get answers to common questions about the Bing Spell Check API on Azure.
services: cognitive-services
author: HeidiSteen
manager: jhubbard
ms.service: cognitive-services
ms.component: bing-spell-check
ms.topic: conceptual
ms.date: 07/26/2017
ms.author: heidist
ms.openlocfilehash: 87b1f3ed3e0aaa9f3c3c804dc9eac3ee60b4a565
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870080"
---
# <a name="frequently-asked-questions-about-the-bing-spell-check-api"></a><span data-ttu-id="ba9d9-103">Frequently Asked Questions about the Bing Spell Check API</span><span class="sxs-lookup"><span data-stu-id="ba9d9-103">Frequently Asked Questions about the Bing Spell Check API</span></span>

 <span data-ttu-id="ba9d9-104">Find answers to commonly asked questions about concepts, code, and scenarios related to the Bing Spell Check API for Microsoft Cognitive Services on Azure.</span><span class="sxs-lookup"><span data-stu-id="ba9d9-104">Find answers to commonly asked questions about concepts, code, and scenarios related to the Bing Spell Check API for Microsoft Cognitive Services on Azure.</span></span>

## <a name="how-do-i-get-the-optional-client-headers-when-calling-the-bing-spell-check-api-from-javascript"></a><span data-ttu-id="ba9d9-105">How do I get the optional client headers when calling the Bing Spell Check API from JavaScript?</span><span class="sxs-lookup"><span data-stu-id="ba9d9-105">How do I get the optional client headers when calling the Bing Spell Check API from JavaScript?</span></span>

<span data-ttu-id="ba9d9-106">The following headers are optional, but we recommend that you treat them as required.</span><span class="sxs-lookup"><span data-stu-id="ba9d9-106">The following headers are optional, but we recommend that you treat them as required.</span></span> <span data-ttu-id="ba9d9-107">These headers help the Bing Spell Check API return more accurate results.</span><span class="sxs-lookup"><span data-stu-id="ba9d9-107">These headers help the Bing Spell Check API return more accurate results.</span></span>

- <span data-ttu-id="ba9d9-108">X-Search-Location</span><span class="sxs-lookup"><span data-stu-id="ba9d9-108">X-Search-Location</span></span>
- <span data-ttu-id="ba9d9-109">X-MSEdge-ClientID</span><span class="sxs-lookup"><span data-stu-id="ba9d9-109">X-MSEdge-ClientID</span></span>
- <span data-ttu-id="ba9d9-110">X-MSEdge-ClientIP</span><span class="sxs-lookup"><span data-stu-id="ba9d9-110">X-MSEdge-ClientIP</span></span>

<span data-ttu-id="ba9d9-111">However, when you call the Bing Spell Check API from JavaScript, your browser's built-in security features might prevent you from accessing the values of these headers.</span><span class="sxs-lookup"><span data-stu-id="ba9d9-111">However, when you call the Bing Spell Check API from JavaScript, your browser's built-in security features might prevent you from accessing the values of these headers.</span></span>

<span data-ttu-id="ba9d9-112">To resolve this issue, you can make the Bing Spell Check API request through a CORS proxy.</span><span class="sxs-lookup"><span data-stu-id="ba9d9-112">To resolve this issue, you can make the Bing Spell Check API request through a CORS proxy.</span></span> <span data-ttu-id="ba9d9-113">The response from such a proxy has a `Access-Control-Expose-Headers` header that whitelists response headers and makes them available to JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ba9d9-113">The response from such a proxy has a `Access-Control-Expose-Headers` header that whitelists response headers and makes them available to JavaScript.</span></span>

<span data-ttu-id="ba9d9-114">It's easy to install a CORS proxy to allow the [tutorial app](tutorials/spellcheck.md) to access the optional client headers.</span><span class="sxs-lookup"><span data-stu-id="ba9d9-114">It's easy to install a CORS proxy to allow the [tutorial app](tutorials/spellcheck.md) to access the optional client headers.</span></span> <span data-ttu-id="ba9d9-115">First, if you don't already have it, [install Node.js](https://nodejs.org/en/download/).</span><span class="sxs-lookup"><span data-stu-id="ba9d9-115">First, if you don't already have it, [install Node.js](https://nodejs.org/en/download/).</span></span> <span data-ttu-id="ba9d9-116">Then enter the following command at a command prompt.</span><span class="sxs-lookup"><span data-stu-id="ba9d9-116">Then enter the following command at a command prompt.</span></span>

    npm install -g cors-proxy-server

<span data-ttu-id="ba9d9-117">Next, change the Bing Spell Check API endpoint in the HTML file to:</span><span class="sxs-lookup"><span data-stu-id="ba9d9-117">Next, change the Bing Spell Check API endpoint in the HTML file to:</span></span>

    http://localhost:9090/https://api.cognitive.microsoft.com/bing/v7.0/spellcheck/

<span data-ttu-id="ba9d9-118">Finally, start the CORS proxy with the following command:</span><span class="sxs-lookup"><span data-stu-id="ba9d9-118">Finally, start the CORS proxy with the following command:</span></span>

    cors-proxy-server

<span data-ttu-id="ba9d9-119">Leave the command window open while you use the tutorial app; closing the window stops the proxy.</span><span class="sxs-lookup"><span data-stu-id="ba9d9-119">Leave the command window open while you use the tutorial app; closing the window stops the proxy.</span></span> <span data-ttu-id="ba9d9-120">In the expandable HTTP Headers section below the search results, you can now see the `X-MSEdge-ClientID` header (among others) and verify that it's the same for each request.</span><span class="sxs-lookup"><span data-stu-id="ba9d9-120">In the expandable HTTP Headers section below the search results, you can now see the `X-MSEdge-ClientID` header (among others) and verify that it's the same for each request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba9d9-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="ba9d9-121">Next steps</span></span>

<span data-ttu-id="ba9d9-122">Is your question about a missing feature or functionality?</span><span class="sxs-lookup"><span data-stu-id="ba9d9-122">Is your question about a missing feature or functionality?</span></span> <span data-ttu-id="ba9d9-123">Consider requesting or voting for it on the [UserVoice web site](https://cognitive.uservoice.com/).</span><span class="sxs-lookup"><span data-stu-id="ba9d9-123">Consider requesting or voting for it on the [UserVoice web site](https://cognitive.uservoice.com/).</span></span>

## <a name="see-also"></a><span data-ttu-id="ba9d9-124">See also</span><span class="sxs-lookup"><span data-stu-id="ba9d9-124">See also</span></span>

 [<span data-ttu-id="ba9d9-125">StackOverflow: Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="ba9d9-125">StackOverflow: Cognitive Services</span></span>](http://stackoverflow.com/questions/tagged/microsoft-cognitive)
