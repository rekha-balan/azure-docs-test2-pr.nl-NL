---
title: Frequently Asked Questions (FAQ) about Azure Autosuggest API | Microsoft Docs
description: Get answers to common questions about Azure Cognitive Services Autosuggest API on Azure.
services: cognitive-services
author: HeidiSteen
manager: jhubbard
ms.service: cognitive-services
ms.component: bing-autosuggest
ms.topic: article
ms.date: 07/26/2017
ms.author: heidist
ms.openlocfilehash: 00b91728bcfec52ff30697f080d5c2619bab79a8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869010"
---
# <a name="frequently-asked-questions-faq-about-autosuggest-api-cognitive-services"></a><span data-ttu-id="f2f23-103">Frequently Asked Questions (FAQ) about Autosuggest API (Cognitive Services)</span><span class="sxs-lookup"><span data-stu-id="f2f23-103">Frequently Asked Questions (FAQ) about Autosuggest API (Cognitive Services)</span></span>
 
 <span data-ttu-id="f2f23-104">Find answers to commonly asked questions about concepts, code, and scenarios related to the Autosuggest API for Azure Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="f2f23-104">Find answers to commonly asked questions about concepts, code, and scenarios related to the Autosuggest API for Azure Cognitive Services.</span></span>

### <a name="how-do-i-get-the-optional-client-headers-when-calling-the-bing-autosuggest-api-from-javascript"></a><span data-ttu-id="f2f23-105">How do I get the optional client headers when calling the Bing Autosuggest API from JavaScript?</span><span class="sxs-lookup"><span data-stu-id="f2f23-105">How do I get the optional client headers when calling the Bing Autosuggest API from JavaScript?</span></span>

<span data-ttu-id="f2f23-106">The following headers are optional, but we recommend that you treat them as required.</span><span class="sxs-lookup"><span data-stu-id="f2f23-106">The following headers are optional, but we recommend that you treat them as required.</span></span> <span data-ttu-id="f2f23-107">These headers help the Bing Autosuggest API return more accurate results.</span><span class="sxs-lookup"><span data-stu-id="f2f23-107">These headers help the Bing Autosuggest API return more accurate results.</span></span>

- <span data-ttu-id="f2f23-108">X-Search-Location</span><span class="sxs-lookup"><span data-stu-id="f2f23-108">X-Search-Location</span></span>
- <span data-ttu-id="f2f23-109">X-MSEdge-ClientID</span><span class="sxs-lookup"><span data-stu-id="f2f23-109">X-MSEdge-ClientID</span></span>
- <span data-ttu-id="f2f23-110">X-MSEdge-ClientIP</span><span class="sxs-lookup"><span data-stu-id="f2f23-110">X-MSEdge-ClientIP</span></span>

<span data-ttu-id="f2f23-111">However, when you call the Bing Autosuggest API from JavaScript, your browser's built-in security features might prevent you from accessing the values of these headers.</span><span class="sxs-lookup"><span data-stu-id="f2f23-111">However, when you call the Bing Autosuggest API from JavaScript, your browser's built-in security features might prevent you from accessing the values of these headers.</span></span>

<span data-ttu-id="f2f23-112">To resolve this, you can make the Bing Autosuggest API request through a CORS proxy.</span><span class="sxs-lookup"><span data-stu-id="f2f23-112">To resolve this, you can make the Bing Autosuggest API request through a CORS proxy.</span></span> <span data-ttu-id="f2f23-113">The response from such a proxy has a `Access-Control-Expose-Headers` header that whitelists response headers and makes them available to JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f2f23-113">The response from such a proxy has a `Access-Control-Expose-Headers` header that whitelists response headers and makes them available to JavaScript.</span></span>

<span data-ttu-id="f2f23-114">It's easy to install a CORS proxy to allow our [tutorial app](tutorials/autosuggest.md) to access the optional client headers.</span><span class="sxs-lookup"><span data-stu-id="f2f23-114">It's easy to install a CORS proxy to allow our [tutorial app](tutorials/autosuggest.md) to access the optional client headers.</span></span> <span data-ttu-id="f2f23-115">First, if you don't already have it, [install Node.js](https://nodejs.org/en/download/).</span><span class="sxs-lookup"><span data-stu-id="f2f23-115">First, if you don't already have it, [install Node.js](https://nodejs.org/en/download/).</span></span> <span data-ttu-id="f2f23-116">Then enter the following command at a command prompt.</span><span class="sxs-lookup"><span data-stu-id="f2f23-116">Then enter the following command at a command prompt.</span></span>

    npm install -g cors-proxy-server

<span data-ttu-id="f2f23-117">Next, change the Bing Autosuggest API endpoint in the HTML file to:</span><span class="sxs-lookup"><span data-stu-id="f2f23-117">Next, change the Bing Autosuggest API endpoint in the HTML file to:</span></span>

    http://localhost:9090/https://api.cognitive.microsoft.com/bing/v7.0/Suggestions

<span data-ttu-id="f2f23-118">Finally, start the CORS proxy with the following command:</span><span class="sxs-lookup"><span data-stu-id="f2f23-118">Finally, start the CORS proxy with the following command:</span></span>

    cors-proxy-server

<span data-ttu-id="f2f23-119">Leave the command window open while you use the tutorial app; closing the window stops the proxy.</span><span class="sxs-lookup"><span data-stu-id="f2f23-119">Leave the command window open while you use the tutorial app; closing the window stops the proxy.</span></span> <span data-ttu-id="f2f23-120">In the expandable HTTP Headers section below the search results, you can now see the `X-MSEdge-ClientID` header (among others) and verify that it is the same for each request.</span><span class="sxs-lookup"><span data-stu-id="f2f23-120">In the expandable HTTP Headers section below the search results, you can now see the `X-MSEdge-ClientID` header (among others) and verify that it is the same for each request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2f23-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="f2f23-121">Next steps</span></span>

<span data-ttu-id="f2f23-122">Is your question about a missing feature or functionality?</span><span class="sxs-lookup"><span data-stu-id="f2f23-122">Is your question about a missing feature or functionality?</span></span> <span data-ttu-id="f2f23-123">Consider requesting or voting for it on our [User Voice web site](https://cognitive.uservoice.com/).</span><span class="sxs-lookup"><span data-stu-id="f2f23-123">Consider requesting or voting for it on our [User Voice web site](https://cognitive.uservoice.com/).</span></span>

## <a name="see-also"></a><span data-ttu-id="f2f23-124">See also</span><span class="sxs-lookup"><span data-stu-id="f2f23-124">See also</span></span>

- [<span data-ttu-id="f2f23-125">Stack Overflow: Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="f2f23-125">Stack Overflow: Cognitive Services</span></span>](http://stackoverflow.com/questions/tagged/microsoft-cognitive)
