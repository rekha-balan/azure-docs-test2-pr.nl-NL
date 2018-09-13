---
title: Azure Content Moderator - Create video transcript reviews using .NET | Microsoft Docs
description: How to create video transcript reviews using Azure Content Moderator SDK for .NET
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 01/19/2018
ms.author: sajagtap
ms.openlocfilehash: 5b4ae96b8a0505123bc6f518d85702d58bad892b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869753"
---
# <a name="create-video-transcript-reviews-using-net"></a><span data-ttu-id="6f5bc-103">Create video transcript reviews using .NET</span><span class="sxs-lookup"><span data-stu-id="6f5bc-103">Create video transcript reviews using .NET</span></span>

<span data-ttu-id="6f5bc-104">This article provides information and code samples to help you quickly get started using the [Content Moderator SDK with C#](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) to:</span><span class="sxs-lookup"><span data-stu-id="6f5bc-104">This article provides information and code samples to help you quickly get started using the [Content Moderator SDK with C#](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) to:</span></span>

- <span data-ttu-id="6f5bc-105">Create a video review for human moderators</span><span class="sxs-lookup"><span data-stu-id="6f5bc-105">Create a video review for human moderators</span></span>
- <span data-ttu-id="6f5bc-106">Add a moderated transcript to the review</span><span class="sxs-lookup"><span data-stu-id="6f5bc-106">Add a moderated transcript to the review</span></span>
- <span data-ttu-id="6f5bc-107">Publish the review</span><span class="sxs-lookup"><span data-stu-id="6f5bc-107">Publish the review</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f5bc-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6f5bc-108">Prerequisites</span></span>

<span data-ttu-id="6f5bc-109">This article assumes that you have [moderated the video](video-moderation-api.md) and [created the video review](video-reviews-quickstart-dotnet.md) in the review tool for human decision making.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-109">This article assumes that you have [moderated the video](video-moderation-api.md) and [created the video review](video-reviews-quickstart-dotnet.md) in the review tool for human decision making.</span></span> <span data-ttu-id="6f5bc-110">You now want to add moderated video transcripts in the review tool.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-110">You now want to add moderated video transcripts in the review tool.</span></span>

<span data-ttu-id="6f5bc-111">This article also assumes that you are already familiar with Visual Studio and C#.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-111">This article also assumes that you are already familiar with Visual Studio and C#.</span></span>

## <a name="sign-up-for-content-moderator"></a><span data-ttu-id="6f5bc-112">Sign up for Content Moderator</span><span class="sxs-lookup"><span data-stu-id="6f5bc-112">Sign up for Content Moderator</span></span>

<span data-ttu-id="6f5bc-113">Before you can use Content Moderator services through the REST API or the SDK, you need a subscription key.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-113">Before you can use Content Moderator services through the REST API or the SDK, you need a subscription key.</span></span>
<span data-ttu-id="6f5bc-114">Refer to the [Quickstart](quick-start.md) to learn how you can obtain the key.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-114">Refer to the [Quickstart](quick-start.md) to learn how you can obtain the key.</span></span>

## <a name="sign-up-for-a-review-tool-account-if-not-completed-in-the-previous-step"></a><span data-ttu-id="6f5bc-115">Sign up for a review tool account if not completed in the previous step</span><span class="sxs-lookup"><span data-stu-id="6f5bc-115">Sign up for a review tool account if not completed in the previous step</span></span>

<span data-ttu-id="6f5bc-116">If you got your Content Moderator from the Azure portal, also [sign up for the review tool account](https://contentmoderator.cognitive.microsoft.com/) and create a review team.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-116">If you got your Content Moderator from the Azure portal, also [sign up for the review tool account](https://contentmoderator.cognitive.microsoft.com/) and create a review team.</span></span> <span data-ttu-id="6f5bc-117">You need the team Id and the review tool to call the review API to start a Job and view the reviews in the review tool.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-117">You need the team Id and the review tool to call the review API to start a Job and view the reviews in the review tool.</span></span>

## <a name="ensure-your-api-key-can-call-the-review-api-job-creation"></a><span data-ttu-id="6f5bc-118">Ensure your API key can call the review API (Job creation)</span><span class="sxs-lookup"><span data-stu-id="6f5bc-118">Ensure your API key can call the review API (Job creation)</span></span>

<span data-ttu-id="6f5bc-119">After completing the previous steps, you may end up with two Content Moderator keys if you started from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-119">After completing the previous steps, you may end up with two Content Moderator keys if you started from the Azure portal.</span></span> 

<span data-ttu-id="6f5bc-120">If you plan to use the Azure-provided API key in your SDK sample, follow the steps mentioned in the [Using Azure key with the review API](review-tool-user-guide/credentials.md#use-the-azure-account-with-the-review-tool-and-review-api) section to allow your application to call the review API and create reviews.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-120">If you plan to use the Azure-provided API key in your SDK sample, follow the steps mentioned in the [Using Azure key with the review API](review-tool-user-guide/credentials.md#use-the-azure-account-with-the-review-tool-and-review-api) section to allow your application to call the review API and create reviews.</span></span>

<span data-ttu-id="6f5bc-121">If you use the free trial key generated by the review tool, your review tool account already knows about the key and therefore, no additional steps are required.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-121">If you use the free trial key generated by the review tool, your review tool account already knows about the key and therefore, no additional steps are required.</span></span>

## <a name="prepare-your-video-for-review"></a><span data-ttu-id="6f5bc-122">Prepare your video for review</span><span class="sxs-lookup"><span data-stu-id="6f5bc-122">Prepare your video for review</span></span>

<span data-ttu-id="6f5bc-123">Add the transcript to a video review.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-123">Add the transcript to a video review.</span></span> <span data-ttu-id="6f5bc-124">The video must be published online.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-124">The video must be published online.</span></span> <span data-ttu-id="6f5bc-125">You need its streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-125">You need its streaming endpoint.</span></span> <span data-ttu-id="6f5bc-126">The streaming endpoint allows the review tool video player to play the video.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-126">The streaming endpoint allows the review tool video player to play the video.</span></span>

![Video demo thumbnail](images/ams-video-demo-view.PNG)

- <span data-ttu-id="6f5bc-128">Copy the **URL** on this [Azure Media Services demo](https://aka.ms/azuremediaplayer?url=https%3A%2F%2Famssamples.streaming.mediaservices.windows.net%2F91492735-c523-432b-ba01-faba6c2206a2%2FAzureMediaServicesPromo.ism%2Fmanifest) page for the manifest URL.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-128">Copy the **URL** on this [Azure Media Services demo](https://aka.ms/azuremediaplayer?url=https%3A%2F%2Famssamples.streaming.mediaservices.windows.net%2F91492735-c523-432b-ba01-faba6c2206a2%2FAzureMediaServicesPromo.ism%2Fmanifest) page for the manifest URL.</span></span>

## <a name="create-your-visual-studio-project"></a><span data-ttu-id="6f5bc-129">Create your Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="6f5bc-129">Create your Visual Studio project</span></span>

1. <span data-ttu-id="6f5bc-130">Add a new **Console app (.NET Framework)** project to your solution.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-130">Add a new **Console app (.NET Framework)** project to your solution.</span></span>

1. <span data-ttu-id="6f5bc-131">Name the project **VideoTranscriptReviews**.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-131">Name the project **VideoTranscriptReviews**.</span></span>

1. <span data-ttu-id="6f5bc-132">Select this project as the single startup project for the solution.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-132">Select this project as the single startup project for the solution.</span></span>

### <a name="install-required-packages"></a><span data-ttu-id="6f5bc-133">Install required packages</span><span class="sxs-lookup"><span data-stu-id="6f5bc-133">Install required packages</span></span>

<span data-ttu-id="6f5bc-134">Install the following NuGet packages for the TermLists project.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-134">Install the following NuGet packages for the TermLists project.</span></span>

- <span data-ttu-id="6f5bc-135">Microsoft.Azure.CognitiveServices.ContentModerator</span><span class="sxs-lookup"><span data-stu-id="6f5bc-135">Microsoft.Azure.CognitiveServices.ContentModerator</span></span>
- <span data-ttu-id="6f5bc-136">Microsoft.Rest.ClientRuntime</span><span class="sxs-lookup"><span data-stu-id="6f5bc-136">Microsoft.Rest.ClientRuntime</span></span>
- <span data-ttu-id="6f5bc-137">Microsoft.Rest.ClientRuntime.Azure</span><span class="sxs-lookup"><span data-stu-id="6f5bc-137">Microsoft.Rest.ClientRuntime.Azure</span></span>
- <span data-ttu-id="6f5bc-138">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="6f5bc-138">Newtonsoft.Json</span></span>

### <a name="update-the-programs-using-statements"></a><span data-ttu-id="6f5bc-139">Update the program's using statements</span><span class="sxs-lookup"><span data-stu-id="6f5bc-139">Update the program's using statements</span></span>

<span data-ttu-id="6f5bc-140">Modify the program's using statements as follows.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-140">Modify the program's using statements as follows.</span></span>

    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Threading;
    using Microsoft.Azure.CognitiveServices.ContentModerator;
    using Microsoft.CognitiveServices.ContentModerator;
    using Microsoft.CognitiveServices.ContentModerator.Models;
    using Newtonsoft.Json;


### <a name="add-private-properties"></a><span data-ttu-id="6f5bc-141">Add private properties</span><span class="sxs-lookup"><span data-stu-id="6f5bc-141">Add private properties</span></span>

<span data-ttu-id="6f5bc-142">Add the following private properties to namespace VideoTranscriptReviews, class Program.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-142">Add the following private properties to namespace VideoTranscriptReviews, class Program.</span></span>

<span data-ttu-id="6f5bc-143">Where indicated, replace the example values for these properties.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-143">Where indicated, replace the example values for these properties.</span></span>


    namespace VideoReviews
    {
        class Program
        {
            // NOTE: Replace this example location with the location for your Content Moderator account.
            /// <summary>
            /// The region/location for your Content Moderator account, 
            /// for example, westus.
            /// </summary>
            private static readonly string AzureRegion = "YOUR CONTENT MODERATOR REGION";

            // NOTE: Replace this example key with a valid subscription key.
            /// <summary>
            /// Your Content Moderator subscription key.
            /// </summary>
            private static readonly string CMSubscriptionKey = "YOUR CONTENT MODERATOR KEY";

            // NOTE: Replace this example team name with your Content Moderator team name.
            /// <summary>
            /// The name of the team to assign the job to.
            /// </summary>
            /// <remarks>This must be the team name you used to create your 
            /// Content Moderator account. You can retrieve your team name from
            /// the Conent Moderator web site. Your team name is the Id associated 
            /// with your subscription.</remarks>
            public static readonly string TeamName = "YOUR CONTENT MODERATOR TEAM ID";

            /// <summary>
            /// The base URL fragment for Content Moderator calls.
            /// </summary>
            private static readonly string AzureBaseURL =
                $"{AzureRegion}.api.cognitive.microsoft.com";

            /// <summary>
            /// The minimum amount of time, in milliseconds, to wait between calls
            /// to the Content Moderator APIs.
            /// </summary>
            private const int throttleRate = 2000;


### <a name="create-content-moderator-client-object"></a><span data-ttu-id="6f5bc-144">Create Content Moderator Client object</span><span class="sxs-lookup"><span data-stu-id="6f5bc-144">Create Content Moderator Client object</span></span>

<span data-ttu-id="6f5bc-145">Add the following method definition to namespace VideoTranscriptReviews, class Program.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-145">Add the following method definition to namespace VideoTranscriptReviews, class Program.</span></span>

    /// <summary>
    /// Returns a new Content Moderator client for your subscription.
    /// </summary>
    /// <returns>The new client.</returns>
    /// <remarks>The <see cref="ContentModeratorClient"/> is disposable.
    /// When you have finished using the client,
    /// you should dispose of it either directly or indirectly. </remarks>
    public static ContentModeratorClient NewClient()
    {
        return new ContentModeratorClient(new ApiKeyServiceClientCredentials(CMSubscriptionKey))
        {
            BaseUrl = AzureBaseURL
        };
    }

## <a name="create-a-video-review"></a><span data-ttu-id="6f5bc-146">Create a video review</span><span class="sxs-lookup"><span data-stu-id="6f5bc-146">Create a video review</span></span>

<span data-ttu-id="6f5bc-147">Create a video review with **ContentModeratorClient.Reviews.CreateVideoReviews**.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-147">Create a video review with **ContentModeratorClient.Reviews.CreateVideoReviews**.</span></span> <span data-ttu-id="6f5bc-148">For more information, see the [API reference](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c4).</span><span class="sxs-lookup"><span data-stu-id="6f5bc-148">For more information, see the [API reference](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c4).</span></span>

<span data-ttu-id="6f5bc-149">**CreateVideoReviews** has the following required parameters:</span><span class="sxs-lookup"><span data-stu-id="6f5bc-149">**CreateVideoReviews** has the following required parameters:</span></span>
1. <span data-ttu-id="6f5bc-150">A string that contains a MIME type, which should be "application/json."</span><span class="sxs-lookup"><span data-stu-id="6f5bc-150">A string that contains a MIME type, which should be "application/json."</span></span> 
1. <span data-ttu-id="6f5bc-151">Your Content Moderator team name.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-151">Your Content Moderator team name.</span></span>
1. <span data-ttu-id="6f5bc-152">An **IList<CreateVideoReviewsBodyItem>** object.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-152">An **IList<CreateVideoReviewsBodyItem>** object.</span></span> <span data-ttu-id="6f5bc-153">Each **CreateVideoReviewsBodyItem** object represents a video review.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-153">Each **CreateVideoReviewsBodyItem** object represents a video review.</span></span> <span data-ttu-id="6f5bc-154">This quickstart creates one review at a time.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-154">This quickstart creates one review at a time.</span></span>

<span data-ttu-id="6f5bc-155">**CreateVideoReviewsBodyItem** has several properties.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-155">**CreateVideoReviewsBodyItem** has several properties.</span></span> <span data-ttu-id="6f5bc-156">At a minimum, you set the following properties:</span><span class="sxs-lookup"><span data-stu-id="6f5bc-156">At a minimum, you set the following properties:</span></span>
- <span data-ttu-id="6f5bc-157">**Content**.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-157">**Content**.</span></span> <span data-ttu-id="6f5bc-158">The URL of the video to be reviewed.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-158">The URL of the video to be reviewed.</span></span>
- <span data-ttu-id="6f5bc-159">**ContentId**.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-159">**ContentId**.</span></span> <span data-ttu-id="6f5bc-160">An ID to assign to the video review.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-160">An ID to assign to the video review.</span></span>
- <span data-ttu-id="6f5bc-161">**Status**.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-161">**Status**.</span></span> <span data-ttu-id="6f5bc-162">Set the value to "Unpublished."</span><span class="sxs-lookup"><span data-stu-id="6f5bc-162">Set the value to "Unpublished."</span></span> <span data-ttu-id="6f5bc-163">If you do not set it, it defaults to "Pending", which means the video review is published and pending human review.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-163">If you do not set it, it defaults to "Pending", which means the video review is published and pending human review.</span></span> <span data-ttu-id="6f5bc-164">Once a video review is published, you can no longer add video frames, a transcript, or a transcript moderation result to it.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-164">Once a video review is published, you can no longer add video frames, a transcript, or a transcript moderation result to it.</span></span>

> [!NOTE]
> <span data-ttu-id="6f5bc-165">**CreateVideoReviews** returns an IList<string>.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-165">**CreateVideoReviews** returns an IList<string>.</span></span> <span data-ttu-id="6f5bc-166">Each of these strings contains an ID for a video review.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-166">Each of these strings contains an ID for a video review.</span></span> <span data-ttu-id="6f5bc-167">These IDs are GUIDs and are not the same as the value of the **ContentId** property.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-167">These IDs are GUIDs and are not the same as the value of the **ContentId** property.</span></span> 

<span data-ttu-id="6f5bc-168">Add the following method definition to namespace VideoReviews, class Program.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-168">Add the following method definition to namespace VideoReviews, class Program.</span></span>

    /// <summary>
    /// Create a video review. For more information, see the API reference:
    /// https://westus2.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c4 
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="id">The ID to assign to the video review.</param>
    /// <param name="content">The URL of the video to review.</param>
    /// <returns>The ID of the video review.</returns>
    private static string CreateReview(ContentModeratorClient client, string id, string content)
    {
        Console.WriteLine("Creating a video review.");

        List<CreateVideoReviewsBodyItem> body = new List<CreateVideoReviewsBodyItem>() {
            new CreateVideoReviewsBodyItem
            {
                Content = content,
                ContentId = id,
                /* Note: to create a published review, set the Status to "Pending".
                However, you cannot add video frames or a transcript to a published review. */
                Status = "Unpublished",
            }
        };

        var result = client.Reviews.CreateVideoReviews("application/json", TeamName, body);

        Thread.Sleep(throttleRate);

        // We created only one review.
        return result[0];
    }

> [!NOTE]
> <span data-ttu-id="6f5bc-169">Your Content Moderator service key has a requests per second (RPS) rate limit.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-169">Your Content Moderator service key has a requests per second (RPS) rate limit.</span></span> <span data-ttu-id="6f5bc-170">If you exceed the limit, the SDK throws an exception with a 429 error code.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-170">If you exceed the limit, the SDK throws an exception with a 429 error code.</span></span> 
>
> <span data-ttu-id="6f5bc-171">A free tier key has a one RPS rate limit.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-171">A free tier key has a one RPS rate limit.</span></span>

## <a name="add-transcript-to-video-review"></a><span data-ttu-id="6f5bc-172">Add transcript to video review</span><span class="sxs-lookup"><span data-stu-id="6f5bc-172">Add transcript to video review</span></span>

<span data-ttu-id="6f5bc-173">You add a transcript to a video review with **ContentModeratorClient.Reviews.AddVideoTranscript**.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-173">You add a transcript to a video review with **ContentModeratorClient.Reviews.AddVideoTranscript**.</span></span> <span data-ttu-id="6f5bc-174">**AddVideoTranscript** has the following required parameters:</span><span class="sxs-lookup"><span data-stu-id="6f5bc-174">**AddVideoTranscript** has the following required parameters:</span></span>
1. <span data-ttu-id="6f5bc-175">Your Content Moderator team ID.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-175">Your Content Moderator team ID.</span></span>
1. <span data-ttu-id="6f5bc-176">The video review ID returned by **CreateVideoReviews**.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-176">The video review ID returned by **CreateVideoReviews**.</span></span>
1. <span data-ttu-id="6f5bc-177">A **Stream** object that contains the transcript.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-177">A **Stream** object that contains the transcript.</span></span>

<span data-ttu-id="6f5bc-178">The transcript must be in the WebVTT format.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-178">The transcript must be in the WebVTT format.</span></span> <span data-ttu-id="6f5bc-179">For more information, see [WebVTT: The Web Video Text Tracks Format](https://www.w3.org/TR/webvtt1/).</span><span class="sxs-lookup"><span data-stu-id="6f5bc-179">For more information, see [WebVTT: The Web Video Text Tracks Format](https://www.w3.org/TR/webvtt1/).</span></span>

> [!NOTE]
> <span data-ttu-id="6f5bc-180">The program uses a sample transcript in the VTT format.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-180">The program uses a sample transcript in the VTT format.</span></span> <span data-ttu-id="6f5bc-181">In a real-world solution, you use the Azure Media Indexer service to [generate a transcript](https://docs.microsoft.com/azure/media-services/media-services-index-content) from a video.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-181">In a real-world solution, you use the Azure Media Indexer service to [generate a transcript](https://docs.microsoft.com/azure/media-services/media-services-index-content) from a video.</span></span>

<span data-ttu-id="6f5bc-182">Add the following method definition to namespace VideotranscriptReviews, class Program.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-182">Add the following method definition to namespace VideotranscriptReviews, class Program.</span></span>

    /// <summary>
    /// Add a transcript to the indicated video review.
    /// The transcript must be in the WebVTT format.
    /// For more information, see the API reference:
    /// https://westus2.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/59e7b8b2e7151f0b10d451fe
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="review_id">The video review ID.</param>
    /// <param name="transcript">The video transcript.</param>
    static void AddTranscript(ContentModeratorClient client, string review_id, string transcript)
    {
        Console.WriteLine("Adding a transcript to the review with ID {0}.", review_id);
        client.Reviews.AddVideoTranscript(TeamName, review_id, new MemoryStream(System.Text.Encoding.UTF8.GetBytes(transcript)));
        Thread.Sleep(throttleRate);
    }

## <a name="add-a-transcript-moderation-result-to-video-review"></a><span data-ttu-id="6f5bc-183">Add a transcript moderation result to video review</span><span class="sxs-lookup"><span data-stu-id="6f5bc-183">Add a transcript moderation result to video review</span></span>

<span data-ttu-id="6f5bc-184">In addition to adding a transcript to a video review, you also add the result of moderating that transcript.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-184">In addition to adding a transcript to a video review, you also add the result of moderating that transcript.</span></span> <span data-ttu-id="6f5bc-185">You do so with **ContentModeratorClient.Reviews.AddVideoTranscriptModerationResult**.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-185">You do so with **ContentModeratorClient.Reviews.AddVideoTranscriptModerationResult**.</span></span> <span data-ttu-id="6f5bc-186">For more information, see the [API reference](https://westus2.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/59e7b93ce7151f0b10d451ff).</span><span class="sxs-lookup"><span data-stu-id="6f5bc-186">For more information, see the [API reference](https://westus2.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/59e7b93ce7151f0b10d451ff).</span></span>

<span data-ttu-id="6f5bc-187">**AddVideoTranscriptModerationResult** has the following required parameters:</span><span class="sxs-lookup"><span data-stu-id="6f5bc-187">**AddVideoTranscriptModerationResult** has the following required parameters:</span></span>
1. <span data-ttu-id="6f5bc-188">A string that contains a MIME type, which should be "application/json."</span><span class="sxs-lookup"><span data-stu-id="6f5bc-188">A string that contains a MIME type, which should be "application/json."</span></span> 
1. <span data-ttu-id="6f5bc-189">Your Content Moderator team name.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-189">Your Content Moderator team name.</span></span>
1. <span data-ttu-id="6f5bc-190">The video review ID returned by **CreateVideoReviews**.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-190">The video review ID returned by **CreateVideoReviews**.</span></span>
1. <span data-ttu-id="6f5bc-191">An IList<TranscriptModerationBodyItem>.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-191">An IList<TranscriptModerationBodyItem>.</span></span> <span data-ttu-id="6f5bc-192">A **TranscriptModerationBodyItem** has the following properties:</span><span class="sxs-lookup"><span data-stu-id="6f5bc-192">A **TranscriptModerationBodyItem** has the following properties:</span></span>
- <span data-ttu-id="6f5bc-193">**Terms**.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-193">**Terms**.</span></span> <span data-ttu-id="6f5bc-194">An IList<TranscriptModerationBodyItemTermsItem>.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-194">An IList<TranscriptModerationBodyItemTermsItem>.</span></span> <span data-ttu-id="6f5bc-195">A **TranscriptModerationBodyItemTermsItem** has the following properties:</span><span class="sxs-lookup"><span data-stu-id="6f5bc-195">A **TranscriptModerationBodyItemTermsItem** has the following properties:</span></span>
- <span data-ttu-id="6f5bc-196">**Index**.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-196">**Index**.</span></span> <span data-ttu-id="6f5bc-197">The zero-based index of the term.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-197">The zero-based index of the term.</span></span>
- <span data-ttu-id="6f5bc-198">**Term**.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-198">**Term**.</span></span> <span data-ttu-id="6f5bc-199">A string that contains the term.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-199">A string that contains the term.</span></span>
- <span data-ttu-id="6f5bc-200">**Timestamp**.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-200">**Timestamp**.</span></span> <span data-ttu-id="6f5bc-201">A string that contains, in seconds, the time in the transcript at which the terms are found.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-201">A string that contains, in seconds, the time in the transcript at which the terms are found.</span></span>

<span data-ttu-id="6f5bc-202">The transcript must be in the WebVTT format.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-202">The transcript must be in the WebVTT format.</span></span> <span data-ttu-id="6f5bc-203">For more information, see [WebVTT: The Web Video Text Tracks Format](https://www.w3.org/TR/webvtt1/).</span><span class="sxs-lookup"><span data-stu-id="6f5bc-203">For more information, see [WebVTT: The Web Video Text Tracks Format](https://www.w3.org/TR/webvtt1/).</span></span>

<span data-ttu-id="6f5bc-204">Add the following method definition to namespace VideoTranscriptReviews, class Program.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-204">Add the following method definition to namespace VideoTranscriptReviews, class Program.</span></span> <span data-ttu-id="6f5bc-205">This method submits a transcript to the **ContentModeratorClient.TextModeration.ScreenText** method.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-205">This method submits a transcript to the **ContentModeratorClient.TextModeration.ScreenText** method.</span></span> <span data-ttu-id="6f5bc-206">It also translates the result into an IList<TranscriptModerationBodyItem>, and submits to **AddVideoTranscriptModerationResult**.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-206">It also translates the result into an IList<TranscriptModerationBodyItem>, and submits to **AddVideoTranscriptModerationResult**.</span></span>

    /// <summary>
    /// Add the results of moderating a video transcript to the indicated video review.
    /// For more information, see the API reference:
    /// https://westus2.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/59e7b93ce7151f0b10d451ff
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="review_id">The video review ID.</param>
    /// <param name="transcript">The video transcript.</param>
    static void AddTranscriptModerationResult(ContentModeratorClient client, string review_id, string transcript)
    {
        Console.WriteLine("Adding a transcript moderation result to the review with ID {0}.", review_id);

        // Screen the transcript using the Text Moderation API. For more information, see:
        // https://westus2.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66f
        Screen screen = client.TextModeration.ScreenText("eng", "text/plain", transcript);

        // Map the term list returned by ScreenText into a term list we can pass to AddVideoTranscriptModerationResult.
        List<TranscriptModerationBodyItemTermsItem> terms = new List<TranscriptModerationBodyItemTermsItem>();
        if (null != screen.Terms)
        {
            foreach (var term in screen.Terms)
            {
                if (term.Index.HasValue)
                {
                    terms.Add(new TranscriptModerationBodyItemTermsItem(term.Index.Value, term.Term));
                }
            }
        }

        List<TranscriptModerationBodyItem> body = new List<TranscriptModerationBodyItem>()
        {
            new TranscriptModerationBodyItem()
            {
                Timestamp = "0",
                Terms = terms
            }
        };

        client.Reviews.AddVideoTranscriptModerationResult("application/json", TeamName, review_id, body);

        Thread.Sleep(throttleRate);
    }


## <a name="publish-video-review"></a><span data-ttu-id="6f5bc-207">Publish video review</span><span class="sxs-lookup"><span data-stu-id="6f5bc-207">Publish video review</span></span>

<span data-ttu-id="6f5bc-208">You publish a video review with **ContentModeratorClient.Reviews.PublishVideoReview**.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-208">You publish a video review with **ContentModeratorClient.Reviews.PublishVideoReview**.</span></span> <span data-ttu-id="6f5bc-209">**PublishVideoReview** has the following required parameters:</span><span class="sxs-lookup"><span data-stu-id="6f5bc-209">**PublishVideoReview** has the following required parameters:</span></span>
1. <span data-ttu-id="6f5bc-210">Your Content Moderator team name.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-210">Your Content Moderator team name.</span></span>
1. <span data-ttu-id="6f5bc-211">The video review ID returned by **CreateVideoReviews**.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-211">The video review ID returned by **CreateVideoReviews**.</span></span>

<span data-ttu-id="6f5bc-212">Add the following method definition to namespace VideoReviews, class Program.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-212">Add the following method definition to namespace VideoReviews, class Program.</span></span>

    /// <summary>
    /// Publish the indicated video review. For more information, see the reference API:
    /// https://westus2.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/59e7bb29e7151f0b10d45201
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="review_id">The video review ID.</param>
    private static void PublishReview(ContentModeratorClient client, string review_id)
    {
        Console.WriteLine("Publishing the review with ID {0}.", review_id);
        client.Reviews.PublishVideoReview(TeamName, review_id);
        Thread.Sleep(throttleRate);
    }

## <a name="putting-it-all-together"></a><span data-ttu-id="6f5bc-213">Putting it all together</span><span class="sxs-lookup"><span data-stu-id="6f5bc-213">Putting it all together</span></span>

<span data-ttu-id="6f5bc-214">Add the **Main** method definition to namespace VideoTranscriptReviews, class Program.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-214">Add the **Main** method definition to namespace VideoTranscriptReviews, class Program.</span></span> <span data-ttu-id="6f5bc-215">Finally, close the Program class and the VideoTranscriptReviews namespace.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-215">Finally, close the Program class and the VideoTranscriptReviews namespace.</span></span>

> [!NOTE]
> <span data-ttu-id="6f5bc-216">The program uses a sample transcript in the VTT format.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-216">The program uses a sample transcript in the VTT format.</span></span> <span data-ttu-id="6f5bc-217">In a real-world solution, you use the Azure Media Indexer service to [generate a transcript](https://docs.microsoft.com/azure/media-services/media-services-index-content) from a video.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-217">In a real-world solution, you use the Azure Media Indexer service to [generate a transcript](https://docs.microsoft.com/azure/media-services/media-services-index-content) from a video.</span></span> 

    static void Main(string[] args)
    {
        using (ContentModeratorClient client = NewClient())
        {
            // Create a review with the content pointing to a streaming endpoint (manifest)
            var streamingcontent = "https://amssamples.streaming.mediaservices.windows.net/91492735-c523-432b-ba01-faba6c2206a2/AzureMediaServicesPromo.ism/manifest";
            string review_id = CreateReview(client, "review1", streamingcontent);

            var transcript = @"WEBVTT

            01:01.000 --> 02:02.000
            First line with a crap word in a transcript.

            02:03.000 --> 02:25.000
            This is another line in the transcript.
            ";

            AddTranscript(client, review_id, transcript);

            AddTranscriptModerationResult(client, review_id, transcript);

            // Publish the review
            PublishReview(client, review_id);

            Console.WriteLine("Open your Content Moderator Dashboard and select Review > Video to see the review.");
            Console.WriteLine("Press any key to close the application.");
            Console.Read();
        }
    }

## <a name="run-the-program-and-review-the-output"></a><span data-ttu-id="6f5bc-218">Run the program and review the output</span><span class="sxs-lookup"><span data-stu-id="6f5bc-218">Run the program and review the output</span></span>

<span data-ttu-id="6f5bc-219">When you run the application, you see an output on the following lines:</span><span class="sxs-lookup"><span data-stu-id="6f5bc-219">When you run the application, you see an output on the following lines:</span></span>

    Creating a video review.
    Adding a transcript to the review with ID 201801v5b08eefa0d2d4d64a1942aec7f5cacc3.
    Adding a transcript moderation result to the review with ID 201801v5b08eefa0d2d4d64a1942aec7f5cacc3.
    Publishing the review with ID 201801v5b08eefa0d2d4d64a1942aec7f5cacc3.
    Open your Content Moderator Dashboard and select Review > Video to see the review.
    Press any key to close the application.

## <a name="navigate-to-your-video-transcript-review"></a><span data-ttu-id="6f5bc-220">Navigate to your video transcript review</span><span class="sxs-lookup"><span data-stu-id="6f5bc-220">Navigate to your video transcript review</span></span>

<span data-ttu-id="6f5bc-221">Go to the video transcript review in your Content Moderator review tool on the **Review**>**Video**>**Transcript** screen.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-221">Go to the video transcript review in your Content Moderator review tool on the **Review**>**Video**>**Transcript** screen.</span></span>

<span data-ttu-id="6f5bc-222">You see the following features:</span><span class="sxs-lookup"><span data-stu-id="6f5bc-222">You see the following features:</span></span>
- <span data-ttu-id="6f5bc-223">The two lines of transcript you added</span><span class="sxs-lookup"><span data-stu-id="6f5bc-223">The two lines of transcript you added</span></span>
- <span data-ttu-id="6f5bc-224">The profanity term found and highlighted by the text moderation service</span><span class="sxs-lookup"><span data-stu-id="6f5bc-224">The profanity term found and highlighted by the text moderation service</span></span>
- <span data-ttu-id="6f5bc-225">Selecting a transcription text starts the video from that timestamp</span><span class="sxs-lookup"><span data-stu-id="6f5bc-225">Selecting a transcription text starts the video from that timestamp</span></span>

![Video transcript review for human moderators](images/ams-video-transcript-review.PNG)

## <a name="next-steps"></a><span data-ttu-id="6f5bc-227">Next steps</span><span class="sxs-lookup"><span data-stu-id="6f5bc-227">Next steps</span></span>

<span data-ttu-id="6f5bc-228">Get the [Content Moderator .NET SDK](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) and the [Visual Studio solution](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator) for this and other Content Moderator quickstarts for .NET.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-228">Get the [Content Moderator .NET SDK](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) and the [Visual Studio solution](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator) for this and other Content Moderator quickstarts for .NET.</span></span>

<span data-ttu-id="6f5bc-229">Learn how to generate [video reviews](video-reviews-quickstart-dotnet.md) in the review tool.</span><span class="sxs-lookup"><span data-stu-id="6f5bc-229">Learn how to generate [video reviews](video-reviews-quickstart-dotnet.md) in the review tool.</span></span>

<span data-ttu-id="6f5bc-230">Check out the detailed tutorial on how to develop a [complete video moderation solution](video-transcript-moderation-review-tutorial-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="6f5bc-230">Check out the detailed tutorial on how to develop a [complete video moderation solution](video-transcript-moderation-review-tutorial-dotnet.md).</span></span>
