---
title: Find endpoint region with C# in LUIS
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
ms.openlocfilehash: 7af58f141730557f103c61a6c591908cc7ec69d0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867517"
---
# <a name="find-endpoint-region-with-c"></a><span data-ttu-id="eff98-103">Find endpoint region with C#</span><span class="sxs-lookup"><span data-stu-id="eff98-103">Find endpoint region with C#</span></span> 
<span data-ttu-id="eff98-104">If you have the LUIS app ID and the LUIS subscription ID, you can find which region to use for endpoint queries.</span><span class="sxs-lookup"><span data-stu-id="eff98-104">If you have the LUIS app ID and the LUIS subscription ID, you can find which region to use for endpoint queries.</span></span>

> [!NOTE] 
> <span data-ttu-id="eff98-105">The complete C# solution is available from the [**LUIS-Samples** Github repository](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/find-region/csharp/).</span><span class="sxs-lookup"><span data-stu-id="eff98-105">The complete C# solution is available from the [**LUIS-Samples** Github repository](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/find-region/csharp/).</span></span>

## <a name="luis-endpoint-query-strategy"></a><span data-ttu-id="eff98-106">LUIS endpoint query strategy</span><span class="sxs-lookup"><span data-stu-id="eff98-106">LUIS endpoint query strategy</span></span>
<span data-ttu-id="eff98-107">Each LUIS endpoint query requires:</span><span class="sxs-lookup"><span data-stu-id="eff98-107">Each LUIS endpoint query requires:</span></span>

* <span data-ttu-id="eff98-108">An endpoint key</span><span class="sxs-lookup"><span data-stu-id="eff98-108">An endpoint key</span></span>
* <span data-ttu-id="eff98-109">An app ID</span><span class="sxs-lookup"><span data-stu-id="eff98-109">An app ID</span></span>
* <span data-ttu-id="eff98-110">A region</span><span class="sxs-lookup"><span data-stu-id="eff98-110">A region</span></span>

<span data-ttu-id="eff98-111">If the LUIS endpoint query uses the correct endpoint key and app ID but the wrong region, the response code is 401.</span><span class="sxs-lookup"><span data-stu-id="eff98-111">If the LUIS endpoint query uses the correct endpoint key and app ID but the wrong region, the response code is 401.</span></span> <span data-ttu-id="eff98-112">The 401 request is not counted toward the subscription quota.</span><span class="sxs-lookup"><span data-stu-id="eff98-112">The 401 request is not counted toward the subscription quota.</span></span> <span data-ttu-id="eff98-113">Turn this request into a strategy to poll all regions to find the correct region.</span><span class="sxs-lookup"><span data-stu-id="eff98-113">Turn this request into a strategy to poll all regions to find the correct region.</span></span> <span data-ttu-id="eff98-114">The correct region is the only request that returns a 2xx status code.</span><span class="sxs-lookup"><span data-stu-id="eff98-114">The correct region is the only request that returns a 2xx status code.</span></span> 

|<span data-ttu-id="eff98-115">Response code</span><span class="sxs-lookup"><span data-stu-id="eff98-115">Response code</span></span>|<span data-ttu-id="eff98-116">Parameters</span><span class="sxs-lookup"><span data-stu-id="eff98-116">Parameters</span></span>|
|--|--|
|<span data-ttu-id="eff98-117">2xx</span><span class="sxs-lookup"><span data-stu-id="eff98-117">2xx</span></span>|<span data-ttu-id="eff98-118">correct endpoint key</span><span class="sxs-lookup"><span data-stu-id="eff98-118">correct endpoint key</span></span><br><span data-ttu-id="eff98-119">correct app ID</span><span class="sxs-lookup"><span data-stu-id="eff98-119">correct app ID</span></span><br><span data-ttu-id="eff98-120">correct host region</span><span class="sxs-lookup"><span data-stu-id="eff98-120">correct host region</span></span>|
|<span data-ttu-id="eff98-121">401</span><span class="sxs-lookup"><span data-stu-id="eff98-121">401</span></span>|<span data-ttu-id="eff98-122">correct endpoint key</span><span class="sxs-lookup"><span data-stu-id="eff98-122">correct endpoint key</span></span><br><span data-ttu-id="eff98-123">correct app ID</span><span class="sxs-lookup"><span data-stu-id="eff98-123">correct app ID</span></span><br><span data-ttu-id="eff98-124">_incorrect_ host region</span><span class="sxs-lookup"><span data-stu-id="eff98-124">_incorrect_ host region</span></span>|

## <a name="c-class-code-to-find-region"></a><span data-ttu-id="eff98-125">C# class code to find region</span><span class="sxs-lookup"><span data-stu-id="eff98-125">C# class code to find region</span></span>
<span data-ttu-id="eff98-126">The console application takes the LUIS app ID and the endpoint key and returns all regions associated with it.</span><span class="sxs-lookup"><span data-stu-id="eff98-126">The console application takes the LUIS app ID and the endpoint key and returns all regions associated with it.</span></span> <span data-ttu-id="eff98-127">Currently, an endpoint key is created by region so only one region should return.</span><span class="sxs-lookup"><span data-stu-id="eff98-127">Currently, an endpoint key is created by region so only one region should return.</span></span>

<span data-ttu-id="eff98-128">Include the .Net library dependencies:</span><span class="sxs-lookup"><span data-stu-id="eff98-128">Include the .Net library dependencies:</span></span>

[!code-csharp[Add the dependencies](~/samples-luis/documentation-samples/find-region/csharp/ConsoleAppLUISRegion/Program.cs?range=1-6 "Add the dependencies")]

<span data-ttu-id="eff98-129">Add this custom LUIS class built to find the region.</span><span class="sxs-lookup"><span data-stu-id="eff98-129">Add this custom LUIS class built to find the region.</span></span> <span data-ttu-id="eff98-130">Replace the variable values for `luisAppId` and `luisSubscriptionKey` with your own values.</span><span class="sxs-lookup"><span data-stu-id="eff98-130">Replace the variable values for `luisAppId` and `luisSubscriptionKey` with your own values.</span></span> <span data-ttu-id="eff98-131">All regions that return 401 will be written to the debug console.</span><span class="sxs-lookup"><span data-stu-id="eff98-131">All regions that return 401 will be written to the debug console.</span></span> 

[!code-csharp[Add the LUIS class](~/samples-luis/documentation-samples/find-region/csharp/ConsoleAppLUISRegion/Program.cs?range=10-83 "Add the LUIS class")]

<span data-ttu-id="eff98-132">This is an example of calling the custom LUIS class in the console application's Main method:</span><span class="sxs-lookup"><span data-stu-id="eff98-132">This is an example of calling the custom LUIS class in the console application's Main method:</span></span>

[!code-csharp[Call the LUIS class](~/samples-luis/documentation-samples/find-region/csharp/ConsoleAppLUISRegion/Program.cs?range=85-101 "Call the LUIS class")]

<span data-ttu-id="eff98-133">When the application is run, the console shows the region for the app ID.</span><span class="sxs-lookup"><span data-stu-id="eff98-133">When the application is run, the console shows the region for the app ID.</span></span>

![Screenshot of console app showing LUIS region](./media/find-region-csharp/console.png)

## <a name="next-steps"></a><span data-ttu-id="eff98-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="eff98-135">Next steps</span></span>

<span data-ttu-id="eff98-136">Learn more about LUIS [regions](luis-reference-regions.md).</span><span class="sxs-lookup"><span data-stu-id="eff98-136">Learn more about LUIS [regions](luis-reference-regions.md).</span></span>
