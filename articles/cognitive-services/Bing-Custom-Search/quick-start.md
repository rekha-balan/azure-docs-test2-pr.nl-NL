---
title: Create a first Bing Custom Search instance - Microsoft Cognitive Services
description: To use Bing Custom Search, you need to create a custom search instance that defines your view or slice of the web. The instance contains settings that specify the public domains, subsites, and webpages that you want Bing to search, and any ranking adjustments.
services: cognitive-services
author: brapel
manager: ehansen
ms.service: cognitive-services
ms.component: bing-custom-search
ms.topic: conceptual
ms.date: 05/07/2017
ms.author: v-brapel
ms.openlocfilehash: 35f0bca01de1c2087f6ae30949cca9b03192b838
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969454"
---
# <a name="create-your-first-bing-custom-search-instance"></a><span data-ttu-id="5d27b-104">Create your first Bing Custom Search instance</span><span class="sxs-lookup"><span data-stu-id="5d27b-104">Create your first Bing Custom Search instance</span></span>
<span data-ttu-id="5d27b-105">To use Bing Custom Search, you need to create a custom search instance that defines your view or slice of the web.</span><span class="sxs-lookup"><span data-stu-id="5d27b-105">To use Bing Custom Search, you need to create a custom search instance that defines your view or slice of the web.</span></span> <span data-ttu-id="5d27b-106">The instance contains settings that specify the public domains, websites, and webpages that you want Bing to search, and any ranking adjustments.</span><span class="sxs-lookup"><span data-stu-id="5d27b-106">The instance contains settings that specify the public domains, websites, and webpages that you want Bing to search, and any ranking adjustments.</span></span> <span data-ttu-id="5d27b-107">To create the instance, use the Bing Custom Search [portal](https://customsearch.ai).</span><span class="sxs-lookup"><span data-stu-id="5d27b-107">To create the instance, use the Bing Custom Search [portal](https://customsearch.ai).</span></span> 

## <a name="create-a-custom-search-instance"></a><span data-ttu-id="5d27b-108">Create a custom search instance</span><span class="sxs-lookup"><span data-stu-id="5d27b-108">Create a custom search instance</span></span>

<span data-ttu-id="5d27b-109">To create a Bing Custom Search instance:</span><span class="sxs-lookup"><span data-stu-id="5d27b-109">To create a Bing Custom Search instance:</span></span>

1.  <span data-ttu-id="5d27b-110">Get a key for Custom Search API.</span><span class="sxs-lookup"><span data-stu-id="5d27b-110">Get a key for Custom Search API.</span></span> <span data-ttu-id="5d27b-111">See [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=bing-custom-search).</span><span class="sxs-lookup"><span data-stu-id="5d27b-111">See [Try Cognitive Services](https://azure.microsoft.com/try/cognitive-services/?api=bing-custom-search).</span></span>
2.  <span data-ttu-id="5d27b-112">Sign in to the portal using a Microsoft account (MSA).</span><span class="sxs-lookup"><span data-stu-id="5d27b-112">Sign in to the portal using a Microsoft account (MSA).</span></span> <span data-ttu-id="5d27b-113">Click the **Sign in** button.</span><span class="sxs-lookup"><span data-stu-id="5d27b-113">Click the **Sign in** button.</span></span> <span data-ttu-id="5d27b-114">If it's your first time using the portal follow the additional steps below, otherwise continue to step 3.</span><span class="sxs-lookup"><span data-stu-id="5d27b-114">If it's your first time using the portal follow the additional steps below, otherwise continue to step 3.</span></span>
    - <span data-ttu-id="5d27b-115">If you don’t have an MSA, click **Create a Microsoft account**.</span><span class="sxs-lookup"><span data-stu-id="5d27b-115">If you don’t have an MSA, click **Create a Microsoft account**.</span></span> <span data-ttu-id="5d27b-116">The portal asks for permissions to access your data.</span><span class="sxs-lookup"><span data-stu-id="5d27b-116">The portal asks for permissions to access your data.</span></span> <span data-ttu-id="5d27b-117">Click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="5d27b-117">Click **Yes**.</span></span>
    - <span data-ttu-id="5d27b-118">Agree to the Cognitive Services Terms.</span><span class="sxs-lookup"><span data-stu-id="5d27b-118">Agree to the Cognitive Services Terms.</span></span> <span data-ttu-id="5d27b-119">Check **I agree** and click **Agree**.</span><span class="sxs-lookup"><span data-stu-id="5d27b-119">Check **I agree** and click **Agree**.</span></span>  
3.  <span data-ttu-id="5d27b-120">After signing in, click **New Instance** and name the instance.</span><span class="sxs-lookup"><span data-stu-id="5d27b-120">After signing in, click **New Instance** and name the instance.</span></span> <span data-ttu-id="5d27b-121">Use a name that’s meaningful and describes the type of content the search returns.</span><span class="sxs-lookup"><span data-stu-id="5d27b-121">Use a name that’s meaningful and describes the type of content the search returns.</span></span> <span data-ttu-id="5d27b-122">You can change the name at any time.</span><span class="sxs-lookup"><span data-stu-id="5d27b-122">You can change the name at any time.</span></span> 
4.  <span data-ttu-id="5d27b-123">On the **Active** tab in **Search Experience**, enter the URL of one or more sites you want to include in your search.</span><span class="sxs-lookup"><span data-stu-id="5d27b-123">On the **Active** tab in **Search Experience**, enter the URL of one or more sites you want to include in your search.</span></span>
5.  <span data-ttu-id="5d27b-124">To confirm that your instance returns results, enter a query in the preview pane on the right.</span><span class="sxs-lookup"><span data-stu-id="5d27b-124">To confirm that your instance returns results, enter a query in the preview pane on the right.</span></span> <span data-ttu-id="5d27b-125">If there are no results, specify a new site.</span><span class="sxs-lookup"><span data-stu-id="5d27b-125">If there are no results, specify a new site.</span></span> <span data-ttu-id="5d27b-126">Bing returns results only for public sites that it has indexed.</span><span class="sxs-lookup"><span data-stu-id="5d27b-126">Bing returns results only for public sites that it has indexed.</span></span>
6.  <span data-ttu-id="5d27b-127">Click **Publish** to publish configuration changes to production.</span><span class="sxs-lookup"><span data-stu-id="5d27b-127">Click **Publish** to publish configuration changes to production.</span></span> <span data-ttu-id="5d27b-128">When prompted, click **Publish** to confirm.</span><span class="sxs-lookup"><span data-stu-id="5d27b-128">When prompted, click **Publish** to confirm.</span></span>
7.  <span data-ttu-id="5d27b-129">Click **Production** > **Endpoints** and copy the **Custom Configuration ID**.</span><span class="sxs-lookup"><span data-stu-id="5d27b-129">Click **Production** > **Endpoints** and copy the **Custom Configuration ID**.</span></span> <span data-ttu-id="5d27b-130">You need this ID to call the Custom Search API.</span><span class="sxs-lookup"><span data-stu-id="5d27b-130">You need this ID to call the Custom Search API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d27b-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="5d27b-131">Next steps</span></span>

<span data-ttu-id="5d27b-132">Continue to work with the custom search instance you've just created by following instructions in these how-to guides:</span><span class="sxs-lookup"><span data-stu-id="5d27b-132">Continue to work with the custom search instance you've just created by following instructions in these how-to guides:</span></span>

- [<span data-ttu-id="5d27b-133">Configure your custom search experience</span><span class="sxs-lookup"><span data-stu-id="5d27b-133">Configure your custom search experience</span></span>](./define-your-custom-view.md)
- [<span data-ttu-id="5d27b-134">Call your custom search</span><span class="sxs-lookup"><span data-stu-id="5d27b-134">Call your custom search</span></span>](./search-your-custom-view.md)
- [<span data-ttu-id="5d27b-135">Share your custom search</span><span class="sxs-lookup"><span data-stu-id="5d27b-135">Share your custom search</span></span>](./share-your-custom-search.md)
- [<span data-ttu-id="5d27b-136">Configure your hosted UI experience</span><span class="sxs-lookup"><span data-stu-id="5d27b-136">Configure your hosted UI experience</span></span>](./hosted-ui.md)
- [<span data-ttu-id="5d27b-137">Use decoration markers to highlight text</span><span class="sxs-lookup"><span data-stu-id="5d27b-137">Use decoration markers to highlight text</span></span>](./hit-highlighting.md)
- [<span data-ttu-id="5d27b-138">Page webpages</span><span class="sxs-lookup"><span data-stu-id="5d27b-138">Page webpages</span></span>](./page-webpages.md)
