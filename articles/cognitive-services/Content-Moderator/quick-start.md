---
title: Azure Content Moderator get started | Microsoft Docs
description: How to get started with Azure Content Moderator.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 01/15/2018
ms.author: sajagtap
ms.openlocfilehash: 39727b4d97ade67b854fe525afad565451cc3d77
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800532"
---
# <a name="get-started-with-content-moderator"></a><span data-ttu-id="6be2c-103">Get started with Content Moderator</span><span class="sxs-lookup"><span data-stu-id="6be2c-103">Get started with Content Moderator</span></span>

<span data-ttu-id="6be2c-104">You get started with Content Moderator in the following ways:</span><span class="sxs-lookup"><span data-stu-id="6be2c-104">You get started with Content Moderator in the following ways:</span></span>

- <span data-ttu-id="6be2c-105">[Start with the review tool](#start-with-the-review-tool) to get the API key and create a review team.</span><span class="sxs-lookup"><span data-stu-id="6be2c-105">[Start with the review tool](#start-with-the-review-tool) to get the API key and create a review team.</span></span> <span data-ttu-id="6be2c-106">The benefit is that you can use the API key to call the moderation APIs for scanning content and the review APIs for generating reviews, without additional steps.</span><span class="sxs-lookup"><span data-stu-id="6be2c-106">The benefit is that you can use the API key to call the moderation APIs for scanning content and the review APIs for generating reviews, without additional steps.</span></span>
- <span data-ttu-id="6be2c-107">[Subscribe to Content Moderator](#start-with-the-apis) in Azure to get the API key.</span><span class="sxs-lookup"><span data-stu-id="6be2c-107">[Subscribe to Content Moderator](#start-with-the-apis) in Azure to get the API key.</span></span> <span data-ttu-id="6be2c-108">Check out the [API reference](api-reference.md) and the [SDKs](sdk-and-samples.md#sdks-for-python-java-nodejs-and-net).</span><span class="sxs-lookup"><span data-stu-id="6be2c-108">Check out the [API reference](api-reference.md) and the [SDKs](sdk-and-samples.md#sdks-for-python-java-nodejs-and-net).</span></span> <span data-ttu-id="6be2c-109">You still need to sign up online to create a review team.</span><span class="sxs-lookup"><span data-stu-id="6be2c-109">You still need to sign up online to create a review team.</span></span>
- <span data-ttu-id="6be2c-110">[Use the Flow connector and templates](https://flow.microsoft.com/connectors/shared_cognitiveservicescontentmoderator/content-moderator/) to check out a wide range of integrations with an easy-to-use designer.</span><span class="sxs-lookup"><span data-stu-id="6be2c-110">[Use the Flow connector and templates](https://flow.microsoft.com/connectors/shared_cognitiveservicescontentmoderator/content-moderator/) to check out a wide range of integrations with an easy-to-use designer.</span></span>

<span data-ttu-id="6be2c-111">Regardless of the option you choose, see the [Managing credentials](review-tool-user-guide/credentials.md) article to find your API credentials.</span><span class="sxs-lookup"><span data-stu-id="6be2c-111">Regardless of the option you choose, see the [Managing credentials](review-tool-user-guide/credentials.md) article to find your API credentials.</span></span>

## <a name="start-with-the-review-tool"></a><span data-ttu-id="6be2c-112">Start with the review tool</span><span class="sxs-lookup"><span data-stu-id="6be2c-112">Start with the review tool</span></span>
<span data-ttu-id="6be2c-113">[Sign up](http://contentmoderator.cognitive.microsoft.com/) on the Content Moderator review tool web site.</span><span class="sxs-lookup"><span data-stu-id="6be2c-113">[Sign up](http://contentmoderator.cognitive.microsoft.com/) on the Content Moderator review tool web site.</span></span>

![Content Moderator Home Page](images/homepage.PNG)

### <a name="create-a-review-team"></a><span data-ttu-id="6be2c-115">Create a review team</span><span class="sxs-lookup"><span data-stu-id="6be2c-115">Create a review team</span></span>
<span data-ttu-id="6be2c-116">Give your team a name.</span><span class="sxs-lookup"><span data-stu-id="6be2c-116">Give your team a name.</span></span> <span data-ttu-id="6be2c-117">If you want to invite your colleagues, you can do so by entering their email addresses.</span><span class="sxs-lookup"><span data-stu-id="6be2c-117">If you want to invite your colleagues, you can do so by entering their email addresses.</span></span>

![Invite team member](images/QuickStart-2-small.png)

### <a name="upload-images-or-enter-text"></a><span data-ttu-id="6be2c-119">Upload images or enter text</span><span class="sxs-lookup"><span data-stu-id="6be2c-119">Upload images or enter text</span></span>
<span data-ttu-id="6be2c-120">Click **Try > Image** or **Try > Text**.</span><span class="sxs-lookup"><span data-stu-id="6be2c-120">Click **Try > Image** or **Try > Text**.</span></span> <span data-ttu-id="6be2c-121">Upload up to five sample images or enter sample text for moderation.</span><span class="sxs-lookup"><span data-stu-id="6be2c-121">Upload up to five sample images or enter sample text for moderation.</span></span>

![Try Image or Text Moderation](images/tryimagesortext.png)

### <a name="submit-for-automated-moderation"></a><span data-ttu-id="6be2c-123">Submit for automated moderation</span><span class="sxs-lookup"><span data-stu-id="6be2c-123">Submit for automated moderation</span></span>
<span data-ttu-id="6be2c-124">Submit your content for automated moderation.</span><span class="sxs-lookup"><span data-stu-id="6be2c-124">Submit your content for automated moderation.</span></span> <span data-ttu-id="6be2c-125">Internally, the review tool calls the moderation APIs to scan your content.</span><span class="sxs-lookup"><span data-stu-id="6be2c-125">Internally, the review tool calls the moderation APIs to scan your content.</span></span> <span data-ttu-id="6be2c-126">Once the scanning is complete, you see a message informing you about the results waiting for your review.</span><span class="sxs-lookup"><span data-stu-id="6be2c-126">Once the scanning is complete, you see a message informing you about the results waiting for your review.</span></span>

![Moderate files](images/submitted.png)

### <a name="review-and-confirm-results"></a><span data-ttu-id="6be2c-128">Review and confirm results</span><span class="sxs-lookup"><span data-stu-id="6be2c-128">Review and confirm results</span></span>
<span data-ttu-id="6be2c-129">Review the auto-moderated tags, change if needed, and submit by using the **Next** button.</span><span class="sxs-lookup"><span data-stu-id="6be2c-129">Review the auto-moderated tags, change if needed, and submit by using the **Next** button.</span></span> <span data-ttu-id="6be2c-130">As your business application calls the Moderator APIs, the tagged content starts queuing up, ready to be reviewed by the human review teams.</span><span class="sxs-lookup"><span data-stu-id="6be2c-130">As your business application calls the Moderator APIs, the tagged content starts queuing up, ready to be reviewed by the human review teams.</span></span> <span data-ttu-id="6be2c-131">You quickly review large volumes of content using this approach.</span><span class="sxs-lookup"><span data-stu-id="6be2c-131">You quickly review large volumes of content using this approach.</span></span>

![Review results](images/reviewresults.png)

<span data-ttu-id="6be2c-133">Learn how to use all the [review tool's features](Review-Tool-User-Guide/human-in-the-loop.md) or continue with the next section to learn about the APIs.</span><span class="sxs-lookup"><span data-stu-id="6be2c-133">Learn how to use all the [review tool's features](Review-Tool-User-Guide/human-in-the-loop.md) or continue with the next section to learn about the APIs.</span></span> <span data-ttu-id="6be2c-134">Skip the sign-up step because you have the API key provisioned for you in the review tool as shown in the [Managing credentials](review-tool-user-guide/credentials.md) article.</span><span class="sxs-lookup"><span data-stu-id="6be2c-134">Skip the sign-up step because you have the API key provisioned for you in the review tool as shown in the [Managing credentials](review-tool-user-guide/credentials.md) article.</span></span>

### <a name="use-the-apis"></a><span data-ttu-id="6be2c-135">Use the APIs</span><span class="sxs-lookup"><span data-stu-id="6be2c-135">Use the APIs</span></span>

<span data-ttu-id="6be2c-136">Learn how to integrate Content Moderator with your business applications.</span><span class="sxs-lookup"><span data-stu-id="6be2c-136">Learn how to integrate Content Moderator with your business applications.</span></span> <span data-ttu-id="6be2c-137">Check out the [API reference](api-reference.md) and the [SDKs](sdk-and-samples.md#sdks-for-python-java-nodejs-and-net).</span><span class="sxs-lookup"><span data-stu-id="6be2c-137">Check out the [API reference](api-reference.md) and the [SDKs](sdk-and-samples.md#sdks-for-python-java-nodejs-and-net).</span></span>

## <a name="subscribe-in-the-azure-portal"></a><span data-ttu-id="6be2c-138">Subscribe in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6be2c-138">Subscribe in the Azure portal</span></span>

<span data-ttu-id="6be2c-139">[Subscribe to Content Moderator](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesContentModerator) in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6be2c-139">[Subscribe to Content Moderator](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesContentModerator) in the Azure portal.</span></span> <span data-ttu-id="6be2c-140">Start with one of the following APIs:</span><span class="sxs-lookup"><span data-stu-id="6be2c-140">Start with one of the following APIs:</span></span>

### <a name="image-moderation"></a><span data-ttu-id="6be2c-141">Image moderation</span><span class="sxs-lookup"><span data-stu-id="6be2c-141">Image moderation</span></span>

<span data-ttu-id="6be2c-142">Start with the [API console](try-image-api.md) or use the [.NET quickstart](image-moderation-quickstart-dotnet.md) to scan images and detect potential adult and racy content by using tags, confidence scores, and other extracted information.</span><span class="sxs-lookup"><span data-stu-id="6be2c-142">Start with the [API console](try-image-api.md) or use the [.NET quickstart](image-moderation-quickstart-dotnet.md) to scan images and detect potential adult and racy content by using tags, confidence scores, and other extracted information.</span></span>

### <a name="text-moderation"></a><span data-ttu-id="6be2c-143">Text moderation</span><span class="sxs-lookup"><span data-stu-id="6be2c-143">Text moderation</span></span>

<span data-ttu-id="6be2c-144">Start with the [API console](try-text-api.md) or use the [.NET quickstart](text-moderation-quickstart-dotnet.md) to scan text content for potential profanity, machine-assisted unwanted text classification (preview), and personally identifiable information (PII).</span><span class="sxs-lookup"><span data-stu-id="6be2c-144">Start with the [API console](try-text-api.md) or use the [.NET quickstart](text-moderation-quickstart-dotnet.md) to scan text content for potential profanity, machine-assisted unwanted text classification (preview), and personally identifiable information (PII).</span></span> 


### <a name="video-moderation"></a><span data-ttu-id="6be2c-145">Video moderation</span><span class="sxs-lookup"><span data-stu-id="6be2c-145">Video moderation</span></span>

<span data-ttu-id="6be2c-146">Start with the [.NET quickstart](video-moderation-api.md) to scan videos and detect potential adult and racy content.</span><span class="sxs-lookup"><span data-stu-id="6be2c-146">Start with the [.NET quickstart](video-moderation-api.md) to scan videos and detect potential adult and racy content.</span></span> 


### <a name="review-apis"></a><span data-ttu-id="6be2c-147">Review APIs</span><span class="sxs-lookup"><span data-stu-id="6be2c-147">Review APIs</span></span>

<span data-ttu-id="6be2c-148">Start here by choosing from the Job, Review, and Workflow APIs.</span><span class="sxs-lookup"><span data-stu-id="6be2c-148">Start here by choosing from the Job, Review, and Workflow APIs.</span></span>

- <span data-ttu-id="6be2c-149">The [Job API](try-review-api-job.md) scans your content by using the moderation APIs and generates reviews in the review tool.</span><span class="sxs-lookup"><span data-stu-id="6be2c-149">The [Job API](try-review-api-job.md) scans your content by using the moderation APIs and generates reviews in the review tool.</span></span> 
- <span data-ttu-id="6be2c-150">The [Review API](try-review-api-review.md) directly creates image, text, or video reviews for human moderators without first scanning the content.</span><span class="sxs-lookup"><span data-stu-id="6be2c-150">The [Review API](try-review-api-review.md) directly creates image, text, or video reviews for human moderators without first scanning the content.</span></span> 
- <span data-ttu-id="6be2c-151">The [Workflow API](try-review-api-workflow.md) creates, updates, and gets details about the custom workflows that your team creates.</span><span class="sxs-lookup"><span data-stu-id="6be2c-151">The [Workflow API](try-review-api-workflow.md) creates, updates, and gets details about the custom workflows that your team creates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6be2c-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="6be2c-152">Next steps</span></span>

<span data-ttu-id="6be2c-153">Check out the [API reference](api-reference.md) and the [SDKs](sdk-and-samples.md#sdks-for-python-java-nodejs-and-net).</span><span class="sxs-lookup"><span data-stu-id="6be2c-153">Check out the [API reference](api-reference.md) and the [SDKs](sdk-and-samples.md#sdks-for-python-java-nodejs-and-net).</span></span> <span data-ttu-id="6be2c-154">Jumpstart your integration with the [.NET SDK samples](sdk-and-samples.md#net-sdk-samples), [REST API samples in C#](https://github.com/sanjeev3/azure-docs-pr/blob/master/articles/cognitive-services/Content-Moderator/sdk-and-samples.md#rest-api-samples-in-c) and [tutorials](sdk-and-samples.md#tutorials).</span><span class="sxs-lookup"><span data-stu-id="6be2c-154">Jumpstart your integration with the [.NET SDK samples](sdk-and-samples.md#net-sdk-samples), [REST API samples in C#](https://github.com/sanjeev3/azure-docs-pr/blob/master/articles/cognitive-services/Content-Moderator/sdk-and-samples.md#rest-api-samples-in-c) and [tutorials](sdk-and-samples.md#tutorials).</span></span>
