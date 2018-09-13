---
title: Moderate content by using human reviews in Azure Content Moderator | Microsoft Docs
description: Learn how to create human reviews in the Content Moderator API console.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 08/05/2017
ms.author: sajagtap
ms.openlocfilehash: 214695ed3e23d1f501d6d4691104b3f8a91f6efc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855668"
---
# <a name="create-reviews-from-the-api-console"></a><span data-ttu-id="98780-103">Create reviews from the API console</span><span class="sxs-lookup"><span data-stu-id="98780-103">Create reviews from the API console</span></span>

<span data-ttu-id="98780-104">Use the Review API's [review operations](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c4) to create image or text reviews for human moderation.</span><span class="sxs-lookup"><span data-stu-id="98780-104">Use the Review API's [review operations](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c4) to create image or text reviews for human moderation.</span></span> <span data-ttu-id="98780-105">Human moderators use the Review tool to review the content.</span><span class="sxs-lookup"><span data-stu-id="98780-105">Human moderators use the Review tool to review the content.</span></span> <span data-ttu-id="98780-106">Use this operation based on your post-moderation business logic.</span><span class="sxs-lookup"><span data-stu-id="98780-106">Use this operation based on your post-moderation business logic.</span></span> <span data-ttu-id="98780-107">Use it after you have scanned your content by using any of the Content Moderator image or text APIs, or other Cognitive Services APIs.</span><span class="sxs-lookup"><span data-stu-id="98780-107">Use it after you have scanned your content by using any of the Content Moderator image or text APIs, or other Cognitive Services APIs.</span></span> 

<span data-ttu-id="98780-108">After a human moderator reviews the auto-assigned tags and prediction data and submits a final moderation decision, the Review API submits all information to your API endpoint.</span><span class="sxs-lookup"><span data-stu-id="98780-108">After a human moderator reviews the auto-assigned tags and prediction data and submits a final moderation decision, the Review API submits all information to your API endpoint.</span></span>

## <a name="use-the-api-console"></a><span data-ttu-id="98780-109">Use the API console</span><span class="sxs-lookup"><span data-stu-id="98780-109">Use the API console</span></span>
<span data-ttu-id="98780-110">To test-drive the API by using the online console, you need a few values to enter into the console:</span><span class="sxs-lookup"><span data-stu-id="98780-110">To test-drive the API by using the online console, you need a few values to enter into the console:</span></span>

- <span data-ttu-id="98780-111">**teamName**: The team name that you created when you set up your Review tool account.</span><span class="sxs-lookup"><span data-stu-id="98780-111">**teamName**: The team name that you created when you set up your Review tool account.</span></span> 
- <span data-ttu-id="98780-112">**ContentId**: This string is passed to the API and returned through the callback.</span><span class="sxs-lookup"><span data-stu-id="98780-112">**ContentId**: This string is passed to the API and returned through the callback.</span></span> <span data-ttu-id="98780-113">The ContentId is useful for associating internal identifiers or metadata with the results of a moderation job.</span><span class="sxs-lookup"><span data-stu-id="98780-113">The ContentId is useful for associating internal identifiers or metadata with the results of a moderation job.</span></span>
- <span data-ttu-id="98780-114">**Metadata**: Custom key-value pairs returned to your API endpoint during the callback.</span><span class="sxs-lookup"><span data-stu-id="98780-114">**Metadata**: Custom key-value pairs returned to your API endpoint during the callback.</span></span> <span data-ttu-id="98780-115">If the key is a short code that is defined in the Review tool, it appears as a tag.</span><span class="sxs-lookup"><span data-stu-id="98780-115">If the key is a short code that is defined in the Review tool, it appears as a tag.</span></span>
- <span data-ttu-id="98780-116">**Ocp-Apim-Subscription-Key**: Located on the **Settings** tab. For more information, see [Overview](overview.md).</span><span class="sxs-lookup"><span data-stu-id="98780-116">**Ocp-Apim-Subscription-Key**: Located on the **Settings** tab. For more information, see [Overview](overview.md).</span></span>

<span data-ttu-id="98780-117">The simplest way to access a testing console is from the **Credentials** window.</span><span class="sxs-lookup"><span data-stu-id="98780-117">The simplest way to access a testing console is from the **Credentials** window.</span></span>

1.  <span data-ttu-id="98780-118">In the **Credentials** window, select [Review API reference](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c4).</span><span class="sxs-lookup"><span data-stu-id="98780-118">In the **Credentials** window, select [Review API reference](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c4).</span></span>

  <span data-ttu-id="98780-119">The **Review - Create** page opens.</span><span class="sxs-lookup"><span data-stu-id="98780-119">The **Review - Create** page opens.</span></span>

2.  <span data-ttu-id="98780-120">For **Open API testing console**, select the region that most closely describes your location.</span><span class="sxs-lookup"><span data-stu-id="98780-120">For **Open API testing console**, select the region that most closely describes your location.</span></span>

  ![Review - Create page region selection](images/test-drive-region.png)

  <span data-ttu-id="98780-122">The **Review - Create** API console opens.</span><span class="sxs-lookup"><span data-stu-id="98780-122">The **Review - Create** API console opens.</span></span>
  
3.  <span data-ttu-id="98780-123">Enter values for the required query parameters, content type, and your subscription key.</span><span class="sxs-lookup"><span data-stu-id="98780-123">Enter values for the required query parameters, content type, and your subscription key.</span></span> <span data-ttu-id="98780-124">In the **Request body** box, specify the content (for example, image location), metadata, and other information associated with the content.</span><span class="sxs-lookup"><span data-stu-id="98780-124">In the **Request body** box, specify the content (for example, image location), metadata, and other information associated with the content.</span></span>

  ![Review - Create console query parameters, headers, and Request body box](images/test-drive-review-1.PNG)
  
4.  <span data-ttu-id="98780-126">Select **Send**.</span><span class="sxs-lookup"><span data-stu-id="98780-126">Select **Send**.</span></span> <span data-ttu-id="98780-127">A review ID is created.</span><span class="sxs-lookup"><span data-stu-id="98780-127">A review ID is created.</span></span> <span data-ttu-id="98780-128">Copy this ID to use in the following steps.</span><span class="sxs-lookup"><span data-stu-id="98780-128">Copy this ID to use in the following steps.</span></span>

  ![Review - Create console Response content box displays the review ID](images/test-drive-review-2.PNG)
  
5.  <span data-ttu-id="98780-130">Select **Get**, and then open the API by selecting the button that matches your region.</span><span class="sxs-lookup"><span data-stu-id="98780-130">Select **Get**, and then open the API by selecting the button that matches your region.</span></span> <span data-ttu-id="98780-131">On the resulting page, enter the values for **teamName**, **ReviewID**, and **subscription key**.</span><span class="sxs-lookup"><span data-stu-id="98780-131">On the resulting page, enter the values for **teamName**, **ReviewID**, and **subscription key**.</span></span> <span data-ttu-id="98780-132">Select the **Send** button on the page.</span><span class="sxs-lookup"><span data-stu-id="98780-132">Select the **Send** button on the page.</span></span> 

  ![Review - Create console Get results](images/test-drive-review-3.PNG)
  
6.  <span data-ttu-id="98780-134">You will see the results of the scan.</span><span class="sxs-lookup"><span data-stu-id="98780-134">You will see the results of the scan.</span></span>

  ![Review - Create console Response content box](images/test-drive-review-4.PNG)
  
7.  <span data-ttu-id="98780-136">On the Content Moderator Dashboard, select **Review** > **Image**.</span><span class="sxs-lookup"><span data-stu-id="98780-136">On the Content Moderator Dashboard, select **Review** > **Image**.</span></span> <span data-ttu-id="98780-137">The image that you scanned appears, ready for human review.</span><span class="sxs-lookup"><span data-stu-id="98780-137">The image that you scanned appears, ready for human review.</span></span>

  ![Review tool image of a soccer ball](images/test-drive-review-5.PNG)

## <a name="next-steps"></a><span data-ttu-id="98780-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="98780-139">Next steps</span></span>

<span data-ttu-id="98780-140">Use the REST API in your code or start with the [Reviews .NET quickstart](moderation-reviews-quickstart-dotnet.md) to integrate with your application.</span><span class="sxs-lookup"><span data-stu-id="98780-140">Use the REST API in your code or start with the [Reviews .NET quickstart](moderation-reviews-quickstart-dotnet.md) to integrate with your application.</span></span>
