---
title: 'Bing Custom Search: Search a custom view | Microsoft Docs'
description: Describes how to search a custom view of the web
services: cognitive-services
author: brapel
manager: ehansen
ms.service: cognitive-services
ms.component: bing-custom-search
ms.topic: article
ms.date: 09/28/2017
ms.author: v-brapel
ms.openlocfilehash: 75f6c8d299c7eed901dda0631fca74b040f72e30
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871098"
---
# <a name="call-your-custom-search"></a><span data-ttu-id="c8960-103">Call your custom search</span><span class="sxs-lookup"><span data-stu-id="c8960-103">Call your custom search</span></span>
<span data-ttu-id="c8960-104">Before making your first call to the Custom Search API to get search results for your instance, you need to get a Cognitive Services subscription key.</span><span class="sxs-lookup"><span data-stu-id="c8960-104">Before making your first call to the Custom Search API to get search results for your instance, you need to get a Cognitive Services subscription key.</span></span> <span data-ttu-id="c8960-105">To get a key for Custom Search API, see [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=bing-custom-search).</span><span class="sxs-lookup"><span data-stu-id="c8960-105">To get a key for Custom Search API, see [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=bing-custom-search).</span></span>

> [!NOTE]
> <span data-ttu-id="c8960-106">Existing Bing Custom Search customers who have a preview key provisioned on or before October 15, 2017 will be able to use their keys until November 30 2017, or until they have exhausted the maximum number of queries allowed.</span><span class="sxs-lookup"><span data-stu-id="c8960-106">Existing Bing Custom Search customers who have a preview key provisioned on or before October 15, 2017 will be able to use their keys until November 30 2017, or until they have exhausted the maximum number of queries allowed.</span></span> <span data-ttu-id="c8960-107">Afterwards, they need to migrate to the generally available version on Azure.</span><span class="sxs-lookup"><span data-stu-id="c8960-107">Afterwards, they need to migrate to the generally available version on Azure.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="c8960-108">Try it out</span><span class="sxs-lookup"><span data-stu-id="c8960-108">Try it out</span></span>
<span data-ttu-id="c8960-109">After you've configured your custom search experience, you can test the configuration from within the Custom Search portal.</span><span class="sxs-lookup"><span data-stu-id="c8960-109">After you've configured your custom search experience, you can test the configuration from within the Custom Search portal.</span></span> <span data-ttu-id="c8960-110">Sign into [Custom Search](https://customsearch.ai), click a Custom Search instance, and click the **Production** tab. The **Endpoints** tab is displayed.</span><span class="sxs-lookup"><span data-stu-id="c8960-110">Sign into [Custom Search](https://customsearch.ai), click a Custom Search instance, and click the **Production** tab. The **Endpoints** tab is displayed.</span></span> <span data-ttu-id="c8960-111">Your subscription will determine which endpoints are available to try, see [pricing pages](https://azure.microsoft.com/pricing/details/cognitive-services/bing-custom-search/).</span><span class="sxs-lookup"><span data-stu-id="c8960-111">Your subscription will determine which endpoints are available to try, see [pricing pages](https://azure.microsoft.com/pricing/details/cognitive-services/bing-custom-search/).</span></span> <span data-ttu-id="c8960-112">To test an endpoint, select it from the dropdown and set the associated configuration options.</span><span class="sxs-lookup"><span data-stu-id="c8960-112">To test an endpoint, select it from the dropdown and set the associated configuration options.</span></span> 

<span data-ttu-id="c8960-113">The following are the available options.</span><span class="sxs-lookup"><span data-stu-id="c8960-113">The following are the available options.</span></span>

- <span data-ttu-id="c8960-114">**Query**: The search term to search for.</span><span class="sxs-lookup"><span data-stu-id="c8960-114">**Query**: The search term to search for.</span></span> <span data-ttu-id="c8960-115">Only available for Web, Image, and Autosuggest endpoints.</span><span class="sxs-lookup"><span data-stu-id="c8960-115">Only available for Web, Image, and Autosuggest endpoints.</span></span>
- <span data-ttu-id="c8960-116">**Custom Configuration ID**: The configuration ID of the selected Custom Search instance.</span><span class="sxs-lookup"><span data-stu-id="c8960-116">**Custom Configuration ID**: The configuration ID of the selected Custom Search instance.</span></span> <span data-ttu-id="c8960-117">This field is read only.</span><span class="sxs-lookup"><span data-stu-id="c8960-117">This field is read only.</span></span>
- <span data-ttu-id="c8960-118">**Market**: The market where the results come from.</span><span class="sxs-lookup"><span data-stu-id="c8960-118">**Market**: The market where the results come from.</span></span> <span data-ttu-id="c8960-119">Only available for Web, Image, and Hosted UI endpoints.</span><span class="sxs-lookup"><span data-stu-id="c8960-119">Only available for Web, Image, and Hosted UI endpoints.</span></span>
- <span data-ttu-id="c8960-120">**Subscription Key**: The subscription key to test with.</span><span class="sxs-lookup"><span data-stu-id="c8960-120">**Subscription Key**: The subscription key to test with.</span></span> <span data-ttu-id="c8960-121">You may select a key from the dropdown or enter one manually.</span><span class="sxs-lookup"><span data-stu-id="c8960-121">You may select a key from the dropdown or enter one manually.</span></span>
- <span data-ttu-id="c8960-122">**Safe Search**: A filter used to filter webpages for adult content.</span><span class="sxs-lookup"><span data-stu-id="c8960-122">**Safe Search**: A filter used to filter webpages for adult content.</span></span> <span data-ttu-id="c8960-123">Only available for Web, Image, and Hosted UI endpoints.</span><span class="sxs-lookup"><span data-stu-id="c8960-123">Only available for Web, Image, and Hosted UI endpoints.</span></span>
- <span data-ttu-id="c8960-124">**Count**: The number of search results to return in the response.</span><span class="sxs-lookup"><span data-stu-id="c8960-124">**Count**: The number of search results to return in the response.</span></span> <span data-ttu-id="c8960-125">Only available for Web and Image endpoints.</span><span class="sxs-lookup"><span data-stu-id="c8960-125">Only available for Web and Image endpoints.</span></span>
- <span data-ttu-id="c8960-126">**Offset**: The number of search results to return in the response.</span><span class="sxs-lookup"><span data-stu-id="c8960-126">**Offset**: The number of search results to return in the response.</span></span> <span data-ttu-id="c8960-127">Only available for Web and Image endpoints.</span><span class="sxs-lookup"><span data-stu-id="c8960-127">Only available for Web and Image endpoints.</span></span>

<span data-ttu-id="c8960-128">After you've specified all required options for Web, Image, or Autosuggest, click **Call** to view the JSON response in the right pane.</span><span class="sxs-lookup"><span data-stu-id="c8960-128">After you've specified all required options for Web, Image, or Autosuggest, click **Call** to view the JSON response in the right pane.</span></span> 

<span data-ttu-id="c8960-129">If you select the Hosted UI endpoint, you can test the search experience from the right pane.</span><span class="sxs-lookup"><span data-stu-id="c8960-129">If you select the Hosted UI endpoint, you can test the search experience from the right pane.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8960-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="c8960-130">Next steps</span></span>
- [<span data-ttu-id="c8960-131">Call your custom view with C#</span><span class="sxs-lookup"><span data-stu-id="c8960-131">Call your custom view with C#</span></span>](./call-endpoint-csharp.md)
- [<span data-ttu-id="c8960-132">Call your custom view with Java</span><span class="sxs-lookup"><span data-stu-id="c8960-132">Call your custom view with Java</span></span>](./call-endpoint-java.md)
- [<span data-ttu-id="c8960-133">Call your custom view with NodeJs</span><span class="sxs-lookup"><span data-stu-id="c8960-133">Call your custom view with NodeJs</span></span>](./call-endpoint-nodejs.md)
- [<span data-ttu-id="c8960-134">Call your custom view with Python</span><span class="sxs-lookup"><span data-stu-id="c8960-134">Call your custom view with Python</span></span>](./call-endpoint-python.md)