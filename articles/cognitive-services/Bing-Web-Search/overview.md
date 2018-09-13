---
title: Bing Web Search APIs overview | Microsoft Docs
description: The Bing Web Search API can send a search query to Bing and return relevant results and combine with other Search APIs to refine searches.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.service: cognitive-services
ms.technology: bing-web-search
ms.topic: article
ms.date: 01/12/2017
ms.author: scottwhi
ms.openlocfilehash: 60c15ffd8fc31279b1c8e6c7e5cbb1c6543e1404
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556192"
---
# <a name="bing-web-search-api"></a><span data-ttu-id="2a26a-103">Bing Web Search API</span><span class="sxs-lookup"><span data-stu-id="2a26a-103">Bing Web Search API</span></span>

<span data-ttu-id="2a26a-104">The Bing Web Search API provides a similar (but not exact) experience to Bing.com/Search (overview on [MSDN](https://msdn.microsoft.com/en-us/library/mt711415.aspx)).</span><span class="sxs-lookup"><span data-stu-id="2a26a-104">The Bing Web Search API provides a similar (but not exact) experience to Bing.com/Search (overview on [MSDN](https://msdn.microsoft.com/en-us/library/mt711415.aspx)).</span></span> <span data-ttu-id="2a26a-105">The Bing Web Search API lets partners send a search query to Bing and get back a list of relevant search results.</span><span class="sxs-lookup"><span data-stu-id="2a26a-105">The Bing Web Search API lets partners send a search query to Bing and get back a list of relevant search results.</span></span> <span data-ttu-id="2a26a-106">This includes webpages and may include images, videos, and more.</span><span class="sxs-lookup"><span data-stu-id="2a26a-106">This includes webpages and may include images, videos, and more.</span></span>

<span data-ttu-id="2a26a-107">Typically, you'll call only the Web Search API, but if you need only images, videos or only news, you should call these APIs directly.</span><span class="sxs-lookup"><span data-stu-id="2a26a-107">Typically, you'll call only the Web Search API, but if you need only images, videos or only news, you should call these APIs directly.</span></span> <span data-ttu-id="2a26a-108">Because calling the Image, Video, and News APIs directly can negatively impact relevance and performance, you should so only if you need a single type of content.</span><span class="sxs-lookup"><span data-stu-id="2a26a-108">Because calling the Image, Video, and News APIs directly can negatively impact relevance and performance, you should so only if you need a single type of content.</span></span>

<span data-ttu-id="2a26a-109">If you need results from a subset of the Bing APIs, you should call the Web Search API and use the responseFilter query parameter to limit the results to only that content (for example, only Images and News).</span><span class="sxs-lookup"><span data-stu-id="2a26a-109">If you need results from a subset of the Bing APIs, you should call the Web Search API and use the responseFilter query parameter to limit the results to only that content (for example, only Images and News).</span></span>

<span data-ttu-id="2a26a-110">Note that the Web Search API may not include all of the same functionality or data that the other APIs provide.</span><span class="sxs-lookup"><span data-stu-id="2a26a-110">Note that the Web Search API may not include all of the same functionality or data that the other APIs provide.</span></span> <span data-ttu-id="2a26a-111">For example, the Image API includes query parameters that let you filter the images, but you may not specify the filter parameters when you call the Search API.</span><span class="sxs-lookup"><span data-stu-id="2a26a-111">For example, the Image API includes query parameters that let you filter the images, but you may not specify the filter parameters when you call the Search API.</span></span> <span data-ttu-id="2a26a-112">Also, even though the Web Search API results may not include images, the Image API could return images for the same query.</span><span class="sxs-lookup"><span data-stu-id="2a26a-112">Also, even though the Web Search API results may not include images, the Image API could return images for the same query.</span></span>

<span data-ttu-id="2a26a-113">To get started, read our [Getting Started](https://msdn.microsoft.com/en-US/library/mt712546.aspx) guide, which describes how you can obtain your own subscription keys and start making calls to the API.</span><span class="sxs-lookup"><span data-stu-id="2a26a-113">To get started, read our [Getting Started](https://msdn.microsoft.com/en-US/library/mt712546.aspx) guide, which describes how you can obtain your own subscription keys and start making calls to the API.</span></span> <span data-ttu-id="2a26a-114">If you already have a subscription, try our API Testing Console [API Testing Console](https://dev.cognitive.microsoft.com/docs/services/56b43eeccf5ff8098cef3807/operations/56b4447dcf5ff8098cef380d/console) where you can easily craft API requests in a sandbox environment.</span><span class="sxs-lookup"><span data-stu-id="2a26a-114">If you already have a subscription, try our API Testing Console [API Testing Console](https://dev.cognitive.microsoft.com/docs/services/56b43eeccf5ff8098cef3807/operations/56b4447dcf5ff8098cef380d/console) where you can easily craft API requests in a sandbox environment.</span></span>

<span data-ttu-id="2a26a-115">For information that shows you how to use the Search API, see [Search Guide](https://msdn.microsoft.com/en-us/library/dn760781(v=bsynd.50).aspx).</span><span class="sxs-lookup"><span data-stu-id="2a26a-115">For information that shows you how to use the Search API, see [Search Guide](https://msdn.microsoft.com/en-us/library/dn760781(v=bsynd.50).aspx).</span></span>

<span data-ttu-id="2a26a-116">For information about the programming elements that you'd use to request and consume the search results, see [Search Reference](https://msdn.microsoft.com/en-us/library/dn760794(v=bsynd.50).aspx).</span><span class="sxs-lookup"><span data-stu-id="2a26a-116">For information about the programming elements that you'd use to request and consume the search results, see [Search Reference](https://msdn.microsoft.com/en-us/library/dn760794(v=bsynd.50).aspx).</span></span> <span data-ttu-id="2a26a-117">Note that results will include objects defined in the Search Reference section and may include objects defined in each of the other API reference sections (for example, [Image Reference](https://msdn.microsoft.com/en-us/library/dn760791(v=bsynd.50).aspx)), if relevant data exists for each.</span><span class="sxs-lookup"><span data-stu-id="2a26a-117">Note that results will include objects defined in the Search Reference section and may include objects defined in each of the other API reference sections (for example, [Image Reference](https://msdn.microsoft.com/en-us/library/dn760791(v=bsynd.50).aspx)), if relevant data exists for each.</span></span>

<span data-ttu-id="2a26a-118">For additional guide and reference content that is common to all Bing APIs, such as Paging Results and Error Codes, see [Shared Guides](https://msdn.microsoft.com/en-us/library/mt711404(v=bsynd.50).aspx) and [Shared Reference](https://msdn.microsoft.com/en-us/library/mt711403(v=bsynd.50).aspx).</span><span class="sxs-lookup"><span data-stu-id="2a26a-118">For additional guide and reference content that is common to all Bing APIs, such as Paging Results and Error Codes, see [Shared Guides](https://msdn.microsoft.com/en-us/library/mt711404(v=bsynd.50).aspx) and [Shared Reference](https://msdn.microsoft.com/en-us/library/mt711403(v=bsynd.50).aspx).</span></span>