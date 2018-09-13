---
title: Sign up for Text Analytics API (Microsoft Cognitive Services on Azure) | Microsoft Docs
description: Instructions for signing up to use text analysis and operating within limits.
services: cognitive-services
author: HeidiSteen
manager: cgronlun
ms.service: cognitive-services
ms.component: text-analytics
ms.topic: get-started-article
ms.date: 3/07/2018
ms.author: heidist
ms.openlocfilehash: dfa5ba138a2e0db75dfc097ca2430fe9c82e826f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869343"
---
# <a name="how-to-sign-up-for-text-analytics-api"></a><span data-ttu-id="586f7-103">How to sign up for Text Analytics API</span><span class="sxs-lookup"><span data-stu-id="586f7-103">How to sign up for Text Analytics API</span></span>

<span data-ttu-id="586f7-104">Text Analytics resources are available 24-7 in the cloud.</span><span class="sxs-lookup"><span data-stu-id="586f7-104">Text Analytics resources are available 24-7 in the cloud.</span></span> <span data-ttu-id="586f7-105">Before you can upload your content for analysis, you must sign up to get an access key.</span><span class="sxs-lookup"><span data-stu-id="586f7-105">Before you can upload your content for analysis, you must sign up to get an access key.</span></span> <span data-ttu-id="586f7-106">Each call to the API requires an access key on the request.</span><span class="sxs-lookup"><span data-stu-id="586f7-106">Each call to the API requires an access key on the request.</span></span>

+ <span data-ttu-id="586f7-107">Start with an Azure Subscription.</span><span class="sxs-lookup"><span data-stu-id="586f7-107">Start with an Azure Subscription.</span></span> <span data-ttu-id="586f7-108">You can create a [free account](https://azure.microsoft.com/free/) to experiment at no charge.</span><span class="sxs-lookup"><span data-stu-id="586f7-108">You can create a [free account](https://azure.microsoft.com/free/) to experiment at no charge.</span></span>

+ <span data-ttu-id="586f7-109">Create a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account), choosing the **Text Analytics API**.</span><span class="sxs-lookup"><span data-stu-id="586f7-109">Create a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account), choosing the **Text Analytics API**.</span></span> <span data-ttu-id="586f7-110">Your key is generated when you sign up.</span><span class="sxs-lookup"><span data-stu-id="586f7-110">Your key is generated when you sign up.</span></span>

<span data-ttu-id="586f7-111">For Text Analytics, there is a Free tier for exploration and evaluation, and billable tiers for production workloads.</span><span class="sxs-lookup"><span data-stu-id="586f7-111">For Text Analytics, there is a Free tier for exploration and evaluation, and billable tiers for production workloads.</span></span> <span data-ttu-id="586f7-112">You can have multiple sign-ups in each subscrption: one free, one paid, and so forth.</span><span class="sxs-lookup"><span data-stu-id="586f7-112">You can have multiple sign-ups in each subscrption: one free, one paid, and so forth.</span></span> <span data-ttu-id="586f7-113">You can switch to a tier offering more transactions if your request volume increases.</span><span class="sxs-lookup"><span data-stu-id="586f7-113">You can switch to a tier offering more transactions if your request volume increases.</span></span>

<span data-ttu-id="586f7-114">There is no service level agreement for services in Preview or the free tier.</span><span class="sxs-lookup"><span data-stu-id="586f7-114">There is no service level agreement for services in Preview or the free tier.</span></span> <span data-ttu-id="586f7-115">For more information, see [SLA for Cognitive Services](https://azure.microsoft.com/support/legal/sla/cognitive-services/v1_1/)</span><span class="sxs-lookup"><span data-stu-id="586f7-115">For more information, see [SLA for Cognitive Services](https://azure.microsoft.com/support/legal/sla/cognitive-services/v1_1/)</span></span>

## <a name="how-to-change-tiers"></a><span data-ttu-id="586f7-116">How to change tiers</span><span class="sxs-lookup"><span data-stu-id="586f7-116">How to change tiers</span></span>

<span data-ttu-id="586f7-117">Start with a Free tier and then transition to a billable tier for production workloads.</span><span class="sxs-lookup"><span data-stu-id="586f7-117">Start with a Free tier and then transition to a billable tier for production workloads.</span></span> <span data-ttu-id="586f7-118">Standard billing is offered at graduated levels.</span><span class="sxs-lookup"><span data-stu-id="586f7-118">Standard billing is offered at graduated levels.</span></span> <span data-ttu-id="586f7-119">You can switch tiers and still keep the same endpoint and access keys.</span><span class="sxs-lookup"><span data-stu-id="586f7-119">You can switch tiers and still keep the same endpoint and access keys.</span></span>

1. <span data-ttu-id="586f7-120">Sign in to [Azure portal](https://portal.azure.com) and [find your service](text-analytics-how-to-access-key.md).</span><span class="sxs-lookup"><span data-stu-id="586f7-120">Sign in to [Azure portal](https://portal.azure.com) and [find your service](text-analytics-how-to-access-key.md).</span></span>

2. <span data-ttu-id="586f7-121">Click **Price tier**.</span><span class="sxs-lookup"><span data-stu-id="586f7-121">Click **Price tier**.</span></span>

   ![Price tier command in left navigation menu](../media/portal-pricing-tier.png)

3. <span data-ttu-id="586f7-123">Choose a tier and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="586f7-123">Choose a tier and click **Select**.</span></span>  <span data-ttu-id="586f7-124">The new limits take effect as soon as the selection is processed.</span><span class="sxs-lookup"><span data-stu-id="586f7-124">The new limits take effect as soon as the selection is processed.</span></span> 

   ![Tiles and Select button in tier selection page](../media/portal-choose-tier.png)

## <a name="how-billing-works"></a><span data-ttu-id="586f7-126">How billing works</span><span class="sxs-lookup"><span data-stu-id="586f7-126">How billing works</span></span>

<span data-ttu-id="586f7-127">Billing is based on the number of transactions.</span><span class="sxs-lookup"><span data-stu-id="586f7-127">Billing is based on the number of transactions.</span></span> <span data-ttu-id="586f7-128">You can purchase a block of transactions at a specific tier in a monthly billing cycle, and then if you go over, a small overage charge is applied per transaction.</span><span class="sxs-lookup"><span data-stu-id="586f7-128">You can purchase a block of transactions at a specific tier in a monthly billing cycle, and then if you go over, a small overage charge is applied per transaction.</span></span> <span data-ttu-id="586f7-129">If you routinely go over the maximum limit, consider switching to a higher tier.</span><span class="sxs-lookup"><span data-stu-id="586f7-129">If you routinely go over the maximum limit, consider switching to a higher tier.</span></span>

<span data-ttu-id="586f7-130">Please see the [pricing page](https://azure.microsoft.com/pricing/details/cognitive-services/text-analytics/) for more information.</span><span class="sxs-lookup"><span data-stu-id="586f7-130">Please see the [pricing page](https://azure.microsoft.com/pricing/details/cognitive-services/text-analytics/) for more information.</span></span>

### <a name="what-constitutes-a-transaction-in-the-text-analytics-api"></a><span data-ttu-id="586f7-131">What constitutes a transaction in the Text Analytics API?</span><span class="sxs-lookup"><span data-stu-id="586f7-131">What constitutes a transaction in the Text Analytics API?</span></span>
<span data-ttu-id="586f7-132">Any annotation to a document counts as a transaction.</span><span class="sxs-lookup"><span data-stu-id="586f7-132">Any annotation to a document counts as a transaction.</span></span> <span data-ttu-id="586f7-133">Batch scoring calls will also take into consideration the number of documents that need to be scored in that transaction.</span><span class="sxs-lookup"><span data-stu-id="586f7-133">Batch scoring calls will also take into consideration the number of documents that need to be scored in that transaction.</span></span> <span data-ttu-id="586f7-134">So for instance, if 1,000 documents are sent for sentiment analysis in a single API call, that will count for 1,000 transactions.</span><span class="sxs-lookup"><span data-stu-id="586f7-134">So for instance, if 1,000 documents are sent for sentiment analysis in a single API call, that will count for 1,000 transactions.</span></span>

## <a name="see-also"></a><span data-ttu-id="586f7-135">See also</span><span class="sxs-lookup"><span data-stu-id="586f7-135">See also</span></span> 

 [<span data-ttu-id="586f7-136">Text Analytics Overview</span><span class="sxs-lookup"><span data-stu-id="586f7-136">Text Analytics Overview</span></span>](../overview.md)  
 [<span data-ttu-id="586f7-137">Frequently asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="586f7-137">Frequently asked questions (FAQ)</span></span>](../text-analytics-resource-faq.md)

## <a name="next-steps"></a><span data-ttu-id="586f7-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="586f7-138">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="586f7-139">Get an access key</span><span class="sxs-lookup"><span data-stu-id="586f7-139">Get an access key</span></span>](text-analytics-how-to-access-key.md)
