---
title: Iterative development and debugging in Azure Data Factory | Microsoft Docs
description: Learn how to develop and debug Data Factory pipelines iteratively in the Azure portal.
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.date: 05/14/2018
ms.topic: conceptual
ms.service: data-factory
services: data-factory
documentationcenter: ''
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.openlocfilehash: a4d3f991dbba8a686c7242aabff11d9228300777
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856136"
---
# <a name="iterative-development-and-debugging-with-azure-data-factory"></a><span data-ttu-id="49774-103">Iterative development and debugging with Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="49774-103">Iterative development and debugging with Azure Data Factory</span></span>

<span data-ttu-id="49774-104">Azure Data Factory lets you iteratively develop and debug Data Factory pipelines.</span><span class="sxs-lookup"><span data-stu-id="49774-104">Azure Data Factory lets you iteratively develop and debug Data Factory pipelines.</span></span>

<span data-ttu-id="49774-105">For an eight-minute introduction and demonstration of this feature, watch the following video:</span><span class="sxs-lookup"><span data-stu-id="49774-105">For an eight-minute introduction and demonstration of this feature, watch the following video:</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Iterative-development-and-debugging-with-Azure-Data-Factory/player]

## <a name="iterative-debugging-features"></a><span data-ttu-id="49774-106">Iterative debugging features</span><span class="sxs-lookup"><span data-stu-id="49774-106">Iterative debugging features</span></span>
<span data-ttu-id="49774-107">Create pipelines and do test runs using the **Debug** capability in the pipeline canvas without writing a single line of code.</span><span class="sxs-lookup"><span data-stu-id="49774-107">Create pipelines and do test runs using the **Debug** capability in the pipeline canvas without writing a single line of code.</span></span>

![Debug capability on the pipeline canvas](media/iterative-development-debugging/iterative-development-image1.png)

<span data-ttu-id="49774-109">View the results of your test runs in the **Output** window of the pipeline canvas.</span><span class="sxs-lookup"><span data-stu-id="49774-109">View the results of your test runs in the **Output** window of the pipeline canvas.</span></span>

![Output window of the pipeline canvas](media/iterative-development-debugging/iterative-development-image2.png)

<span data-ttu-id="49774-111">After a test run succeeds, add more activities to your pipeline and continue debugging in an iterative manner.</span><span class="sxs-lookup"><span data-stu-id="49774-111">After a test run succeeds, add more activities to your pipeline and continue debugging in an iterative manner.</span></span> <span data-ttu-id="49774-112">You can also **Cancel** a test run while it is in progress.</span><span class="sxs-lookup"><span data-stu-id="49774-112">You can also **Cancel** a test run while it is in progress.</span></span>

![Cancel a test run](media/iterative-development-debugging/iterative-development-image3.png)

<span data-ttu-id="49774-114">When you do test runs, you don't have to publish your changes to the data factory before you select **Debug**.</span><span class="sxs-lookup"><span data-stu-id="49774-114">When you do test runs, you don't have to publish your changes to the data factory before you select **Debug**.</span></span> <span data-ttu-id="49774-115">This is helpful in scenarios where you want to make sure that the changes work as expected before you update the data factory workflow.</span><span class="sxs-lookup"><span data-stu-id="49774-115">This is helpful in scenarios where you want to make sure that the changes work as expected before you update the data factory workflow.</span></span>

## <a name="more-info-about-debugging"></a><span data-ttu-id="49774-116">More info about debugging</span><span class="sxs-lookup"><span data-stu-id="49774-116">More info about debugging</span></span>

1. <span data-ttu-id="49774-117">The test runs initiated with the **Debug** capability are not available in the list on the **Monitor** tab. You can only see runs triggered with **Trigger Now**, **Schedule**, or **Tumbling Window** triggers in the **Monitor** tab. You can see the last test run initiated with the **Debug** capability in the **Output** window of the pipeline canvas.</span><span class="sxs-lookup"><span data-stu-id="49774-117">The test runs initiated with the **Debug** capability are not available in the list on the **Monitor** tab. You can only see runs triggered with **Trigger Now**, **Schedule**, or **Tumbling Window** triggers in the **Monitor** tab. You can see the last test run initiated with the **Debug** capability in the **Output** window of the pipeline canvas.</span></span>

2. <span data-ttu-id="49774-118">Selecting **Debug** actually runs the pipeline.</span><span class="sxs-lookup"><span data-stu-id="49774-118">Selecting **Debug** actually runs the pipeline.</span></span> <span data-ttu-id="49774-119">So, for example, if the pipeline contains copy activity, the test run copies data from source to destination.</span><span class="sxs-lookup"><span data-stu-id="49774-119">So, for example, if the pipeline contains copy activity, the test run copies data from source to destination.</span></span> <span data-ttu-id="49774-120">As a result, we recommend that you use test folders in your copy activities and other activities when debugging.</span><span class="sxs-lookup"><span data-stu-id="49774-120">As a result, we recommend that you use test folders in your copy activities and other activities when debugging.</span></span> <span data-ttu-id="49774-121">After you've debugged the pipeline, switch to the actual folders that you want to use in normal operations.</span><span class="sxs-lookup"><span data-stu-id="49774-121">After you've debugged the pipeline, switch to the actual folders that you want to use in normal operations.</span></span>

## <a name="setting-breakpoints-for-debugging"></a><span data-ttu-id="49774-122">Setting breakpoints for debugging</span><span class="sxs-lookup"><span data-stu-id="49774-122">Setting breakpoints for debugging</span></span>

<span data-ttu-id="49774-123">Data Factory also lets you debug until you reach a particular activity on the pipeline canvas.</span><span class="sxs-lookup"><span data-stu-id="49774-123">Data Factory also lets you debug until you reach a particular activity on the pipeline canvas.</span></span> <span data-ttu-id="49774-124">Just put a breakpoint on the activity until which you want to test, and select **Debug**.</span><span class="sxs-lookup"><span data-stu-id="49774-124">Just put a breakpoint on the activity until which you want to test, and select **Debug**.</span></span> <span data-ttu-id="49774-125">Data Factory ensures that the test runs only until the breakpoint activity on the pipeline canvas.</span><span class="sxs-lookup"><span data-stu-id="49774-125">Data Factory ensures that the test runs only until the breakpoint activity on the pipeline canvas.</span></span> <span data-ttu-id="49774-126">This *Debug Until* feature is useful when you don't want to test the entire pipeline, but only a subset of activities inside the pipeline.</span><span class="sxs-lookup"><span data-stu-id="49774-126">This *Debug Until* feature is useful when you don't want to test the entire pipeline, but only a subset of activities inside the pipeline.</span></span>

![Breakpoints on the pipeline canvas](media/iterative-development-debugging/iterative-development-image4.png)

<span data-ttu-id="49774-128">To set a breakpoint, select an element on the pipeline canvas.</span><span class="sxs-lookup"><span data-stu-id="49774-128">To set a breakpoint, select an element on the pipeline canvas.</span></span> <span data-ttu-id="49774-129">A *Debug Until* option appears as an empty red circle at the upper right corner of the element.</span><span class="sxs-lookup"><span data-stu-id="49774-129">A *Debug Until* option appears as an empty red circle at the upper right corner of the element.</span></span>

![Before setting a breakpoint on the selected element](media/iterative-development-debugging/iterative-development-image5.png)

<span data-ttu-id="49774-131">After you select the *Debug Until* option, it changes to a filled red circle to indicate the breakpoint is enabled.</span><span class="sxs-lookup"><span data-stu-id="49774-131">After you select the *Debug Until* option, it changes to a filled red circle to indicate the breakpoint is enabled.</span></span>

![After setting a breakpoint on the selected element](media/iterative-development-debugging/iterative-development-image6.png)

## <a name="next-steps"></a><span data-ttu-id="49774-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="49774-133">Next steps</span></span>
[<span data-ttu-id="49774-134">Continuous integration and deployment in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="49774-134">Continuous integration and deployment in Azure Data Factory</span></span>](continuous-integration-deployment.md)
