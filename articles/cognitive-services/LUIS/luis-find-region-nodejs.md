---
title: Find endpoint region with Node.js in LUIS
titleSuffix: Azure Cognitive Services
description: Programmatically find publish region with endpoint key and application ID for LUIS.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 09/06/2018
ms.author: diberry
ms.openlocfilehash: 2b978b8459bbf248f7702076c78c1948b036aec6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871514"
---
# <a name="find-endpoint-region-with-nodejs"></a><span data-ttu-id="89ee1-103">Find endpoint region with Node.js</span><span class="sxs-lookup"><span data-stu-id="89ee1-103">Find endpoint region with Node.js</span></span>
<span data-ttu-id="89ee1-104">If you have the LUIS app ID and the LUIS subscription ID, you can find which region to use for endpoint queries.</span><span class="sxs-lookup"><span data-stu-id="89ee1-104">If you have the LUIS app ID and the LUIS subscription ID, you can find which region to use for endpoint queries.</span></span>

> [!NOTE] 
> <span data-ttu-id="89ee1-105">The complete Node.js solution is available from the [**LUIS-Samples** Github repository](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/find-region/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="89ee1-105">The complete Node.js solution is available from the [**LUIS-Samples** Github repository](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/find-region/nodejs/).</span></span>

## <a name="luis-endpoint-query-strategy"></a><span data-ttu-id="89ee1-106">LUIS endpoint query strategy</span><span class="sxs-lookup"><span data-stu-id="89ee1-106">LUIS endpoint query strategy</span></span>
<span data-ttu-id="89ee1-107">Each LUIS endpoint query requires:</span><span class="sxs-lookup"><span data-stu-id="89ee1-107">Each LUIS endpoint query requires:</span></span>

* <span data-ttu-id="89ee1-108">An endpoint key</span><span class="sxs-lookup"><span data-stu-id="89ee1-108">An endpoint key</span></span>
* <span data-ttu-id="89ee1-109">An app ID</span><span class="sxs-lookup"><span data-stu-id="89ee1-109">An app ID</span></span>
* <span data-ttu-id="89ee1-110">A region</span><span class="sxs-lookup"><span data-stu-id="89ee1-110">A region</span></span>

<span data-ttu-id="89ee1-111">If the LUIS endpoint query uses the correct endpoint key and app ID but the wrong region, the response code is 401.</span><span class="sxs-lookup"><span data-stu-id="89ee1-111">If the LUIS endpoint query uses the correct endpoint key and app ID but the wrong region, the response code is 401.</span></span> <span data-ttu-id="89ee1-112">The 401 request is not counted toward the subscription quota.</span><span class="sxs-lookup"><span data-stu-id="89ee1-112">The 401 request is not counted toward the subscription quota.</span></span> <span data-ttu-id="89ee1-113">Turn this request into a strategy to poll all regions to find the correct region.</span><span class="sxs-lookup"><span data-stu-id="89ee1-113">Turn this request into a strategy to poll all regions to find the correct region.</span></span> <span data-ttu-id="89ee1-114">The correct region is the only request that returns a 2xx status code.</span><span class="sxs-lookup"><span data-stu-id="89ee1-114">The correct region is the only request that returns a 2xx status code.</span></span> 

|<span data-ttu-id="89ee1-115">Response code</span><span class="sxs-lookup"><span data-stu-id="89ee1-115">Response code</span></span>|<span data-ttu-id="89ee1-116">Parameters</span><span class="sxs-lookup"><span data-stu-id="89ee1-116">Parameters</span></span>|
|--|--|
|<span data-ttu-id="89ee1-117">2xx</span><span class="sxs-lookup"><span data-stu-id="89ee1-117">2xx</span></span>|<span data-ttu-id="89ee1-118">correct endpoint key</span><span class="sxs-lookup"><span data-stu-id="89ee1-118">correct endpoint key</span></span><br><span data-ttu-id="89ee1-119">correct app ID</span><span class="sxs-lookup"><span data-stu-id="89ee1-119">correct app ID</span></span><br><span data-ttu-id="89ee1-120">correct host region</span><span class="sxs-lookup"><span data-stu-id="89ee1-120">correct host region</span></span>|
|<span data-ttu-id="89ee1-121">401</span><span class="sxs-lookup"><span data-stu-id="89ee1-121">401</span></span>|<span data-ttu-id="89ee1-122">correct endpoint key</span><span class="sxs-lookup"><span data-stu-id="89ee1-122">correct endpoint key</span></span><br><span data-ttu-id="89ee1-123">correct app ID</span><span class="sxs-lookup"><span data-stu-id="89ee1-123">correct app ID</span></span><br><span data-ttu-id="89ee1-124">_incorrect_ host region</span><span class="sxs-lookup"><span data-stu-id="89ee1-124">_incorrect_ host region</span></span>|

## <a name="nodejs-code-to-find-region"></a><span data-ttu-id="89ee1-125">Node.js code to find region</span><span class="sxs-lookup"><span data-stu-id="89ee1-125">Node.js code to find region</span></span>
<span data-ttu-id="89ee1-126">The console application takes the LUIS app ID and the endpoint key and returns all regions associated with it.</span><span class="sxs-lookup"><span data-stu-id="89ee1-126">The console application takes the LUIS app ID and the endpoint key and returns all regions associated with it.</span></span> <span data-ttu-id="89ee1-127">Currently, an endpoint key is created by region so only one region should return.</span><span class="sxs-lookup"><span data-stu-id="89ee1-127">Currently, an endpoint key is created by region so only one region should return.</span></span>

<span data-ttu-id="89ee1-128">Include the NPM dependencies:</span><span class="sxs-lookup"><span data-stu-id="89ee1-128">Include the NPM dependencies:</span></span>

[!code-javascript[Add the dependencies](~/samples-luis/documentation-samples/find-region/nodejs/index.js?range=5-6 "Add the dependencies")]

<span data-ttu-id="89ee1-129">Add constants.</span><span class="sxs-lookup"><span data-stu-id="89ee1-129">Add constants.</span></span> <span data-ttu-id="89ee1-130">Replace the variable values for `subscriptionKey` and `appId` with your own values.</span><span class="sxs-lookup"><span data-stu-id="89ee1-130">Replace the variable values for `subscriptionKey` and `appId` with your own values.</span></span>  

[!code-javascript[Add constants](~/samples-luis/documentation-samples/find-region/nodejs/index.js?range=8-25 "Add constants")]

<span data-ttu-id="89ee1-131">Add `searchRegions` function to find the region.</span><span class="sxs-lookup"><span data-stu-id="89ee1-131">Add `searchRegions` function to find the region.</span></span> <span data-ttu-id="89ee1-132">All incorrect regions return 401, which is caught and ignored.</span><span class="sxs-lookup"><span data-stu-id="89ee1-132">All incorrect regions return 401, which is caught and ignored.</span></span>

[!code-javascript[Find region](~/samples-luis/documentation-samples/find-region/nodejs/index.js?range=27-37 "Find region")]

<span data-ttu-id="89ee1-133">Call the `searchRegions` function and return single region:</span><span class="sxs-lookup"><span data-stu-id="89ee1-133">Call the `searchRegions` function and return single region:</span></span>

[!code-javascript[Call the function](~/samples-luis/documentation-samples/find-region/nodejs/index.js?range=39-43 "Call the function")]

<span data-ttu-id="89ee1-134">When the application is run, the terminal shows the region for the app ID.</span><span class="sxs-lookup"><span data-stu-id="89ee1-134">When the application is run, the terminal shows the region for the app ID.</span></span>

![Screenshot of console app showing LUIS region](./media/find-region-nodejs/console.png)


## <a name="next-steps"></a><span data-ttu-id="89ee1-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="89ee1-136">Next steps</span></span>

<span data-ttu-id="89ee1-137">Learn more about LUIS [regions](luis-reference-regions.md).</span><span class="sxs-lookup"><span data-stu-id="89ee1-137">Learn more about LUIS [regions](luis-reference-regions.md).</span></span>
