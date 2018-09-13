---
title: Azure Content Moderator - Create video reviews using .NET | Microsoft Docs
description: How to create video reviews using Azure Content Moderator SDK for .NET
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 01/18/2018
ms.author: sajagtap
ms.openlocfilehash: 808ee3637d67ff4874c5d4837d5c53cbe7b18680
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856934"
---
# <a name="create-video-reviews-using-net"></a><span data-ttu-id="59186-103">Create video reviews using .NET</span><span class="sxs-lookup"><span data-stu-id="59186-103">Create video reviews using .NET</span></span>

<span data-ttu-id="59186-104">This article provides information and code samples to help you quickly get started using the [Content Moderator SDK with C#](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) to:</span><span class="sxs-lookup"><span data-stu-id="59186-104">This article provides information and code samples to help you quickly get started using the [Content Moderator SDK with C#](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) to:</span></span>

- <span data-ttu-id="59186-105">Create a video review for human moderators</span><span class="sxs-lookup"><span data-stu-id="59186-105">Create a video review for human moderators</span></span>
- <span data-ttu-id="59186-106">Add frames to a review</span><span class="sxs-lookup"><span data-stu-id="59186-106">Add frames to a review</span></span>
- <span data-ttu-id="59186-107">Get the frames for the review</span><span class="sxs-lookup"><span data-stu-id="59186-107">Get the frames for the review</span></span> 
- <span data-ttu-id="59186-108">Get the status and details of the review</span><span class="sxs-lookup"><span data-stu-id="59186-108">Get the status and details of the review</span></span>
- <span data-ttu-id="59186-109">Publish the review</span><span class="sxs-lookup"><span data-stu-id="59186-109">Publish the review</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59186-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="59186-110">Prerequisites</span></span>

<span data-ttu-id="59186-111">This article assumes that you have [moderated the video (see quickstart)](video-moderation-api.md) and have the response data.</span><span class="sxs-lookup"><span data-stu-id="59186-111">This article assumes that you have [moderated the video (see quickstart)](video-moderation-api.md) and have the response data.</span></span> <span data-ttu-id="59186-112">You need it for creating frame-based reviews for human moderators.</span><span class="sxs-lookup"><span data-stu-id="59186-112">You need it for creating frame-based reviews for human moderators.</span></span>

<span data-ttu-id="59186-113">This article also assumes that you are already familiar with Visual Studio and C#.</span><span class="sxs-lookup"><span data-stu-id="59186-113">This article also assumes that you are already familiar with Visual Studio and C#.</span></span>

## <a name="sign-up-for-content-moderator"></a><span data-ttu-id="59186-114">Sign up for Content Moderator</span><span class="sxs-lookup"><span data-stu-id="59186-114">Sign up for Content Moderator</span></span>

<span data-ttu-id="59186-115">Before you can use Content Moderator services through the REST API or the SDK, you need a subscription key.</span><span class="sxs-lookup"><span data-stu-id="59186-115">Before you can use Content Moderator services through the REST API or the SDK, you need a subscription key.</span></span>
<span data-ttu-id="59186-116">Refer to the [Quickstart](quick-start.md) to learn how you can obtain the key.</span><span class="sxs-lookup"><span data-stu-id="59186-116">Refer to the [Quickstart](quick-start.md) to learn how you can obtain the key.</span></span>

## <a name="sign-up-for-a-review-tool-account-if-not-completed-in-the-previous-step"></a><span data-ttu-id="59186-117">Sign up for a review tool account if not completed in the previous step</span><span class="sxs-lookup"><span data-stu-id="59186-117">Sign up for a review tool account if not completed in the previous step</span></span>

<span data-ttu-id="59186-118">If you got your Content Moderator from the Azure portal, also [sign up for the review tool account](https://contentmoderator.cognitive.microsoft.com/) and create a review team.</span><span class="sxs-lookup"><span data-stu-id="59186-118">If you got your Content Moderator from the Azure portal, also [sign up for the review tool account](https://contentmoderator.cognitive.microsoft.com/) and create a review team.</span></span> <span data-ttu-id="59186-119">You need the team Id and the review tool to call the review API to start a Job and view the reviews in the review tool.</span><span class="sxs-lookup"><span data-stu-id="59186-119">You need the team Id and the review tool to call the review API to start a Job and view the reviews in the review tool.</span></span>

## <a name="ensure-your-api-key-can-call-the-review-api-for-review-creation"></a><span data-ttu-id="59186-120">Ensure your API key can call the review API for review creation</span><span class="sxs-lookup"><span data-stu-id="59186-120">Ensure your API key can call the review API for review creation</span></span>

<span data-ttu-id="59186-121">After completing the previous steps, you may end up with two Content Moderator keys if you started from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="59186-121">After completing the previous steps, you may end up with two Content Moderator keys if you started from the Azure portal.</span></span> 

<span data-ttu-id="59186-122">If you plan to use the Azure-provided API key in your SDK sample, follow the steps mentioned in the [Using Azure key with the review API](review-tool-user-guide/credentials.md#use-the-azure-account-with-the-review-tool-and-review-api) section to allow your application to call the review API and create reviews.</span><span class="sxs-lookup"><span data-stu-id="59186-122">If you plan to use the Azure-provided API key in your SDK sample, follow the steps mentioned in the [Using Azure key with the review API](review-tool-user-guide/credentials.md#use-the-azure-account-with-the-review-tool-and-review-api) section to allow your application to call the review API and create reviews.</span></span>

<span data-ttu-id="59186-123">If you use the free trial key generated by the review tool, your review tool account already knows about the key and therefore, no additional steps are required.</span><span class="sxs-lookup"><span data-stu-id="59186-123">If you use the free trial key generated by the review tool, your review tool account already knows about the key and therefore, no additional steps are required.</span></span>

### <a name="prepare-your-video-and-the-video-frames-for-review"></a><span data-ttu-id="59186-124">Prepare your video and the video frames for review</span><span class="sxs-lookup"><span data-stu-id="59186-124">Prepare your video and the video frames for review</span></span>

<span data-ttu-id="59186-125">The video and sample video frames to review must be published online because you need their URLs.</span><span class="sxs-lookup"><span data-stu-id="59186-125">The video and sample video frames to review must be published online because you need their URLs.</span></span>

> [!NOTE]
> <span data-ttu-id="59186-126">The program uses manually saved screenshots from the video with random adult/racy scores to illustrate the use of the review API.</span><span class="sxs-lookup"><span data-stu-id="59186-126">The program uses manually saved screenshots from the video with random adult/racy scores to illustrate the use of the review API.</span></span> <span data-ttu-id="59186-127">In a real-world situation, you use the [video moderation output](video-moderation-api.md#run-the-program-and-review-the-output) to create images and assign scores.</span><span class="sxs-lookup"><span data-stu-id="59186-127">In a real-world situation, you use the [video moderation output](video-moderation-api.md#run-the-program-and-review-the-output) to create images and assign scores.</span></span> 

<span data-ttu-id="59186-128">For the video, you need a streaming endpoint so that the review tool plays the video in the player view.</span><span class="sxs-lookup"><span data-stu-id="59186-128">For the video, you need a streaming endpoint so that the review tool plays the video in the player view.</span></span>

![Video demo thumbnail](images/ams-video-demo-view.PNG)

- <span data-ttu-id="59186-130">Copy the **URL** on this [Azure Media Services demo](https://aka.ms/azuremediaplayer?url=https%3A%2F%2Famssamples.streaming.mediaservices.windows.net%2F91492735-c523-432b-ba01-faba6c2206a2%2FAzureMediaServicesPromo.ism%2Fmanifest) page for the manifest URL.</span><span class="sxs-lookup"><span data-stu-id="59186-130">Copy the **URL** on this [Azure Media Services demo](https://aka.ms/azuremediaplayer?url=https%3A%2F%2Famssamples.streaming.mediaservices.windows.net%2F91492735-c523-432b-ba01-faba6c2206a2%2FAzureMediaServicesPromo.ism%2Fmanifest) page for the manifest URL.</span></span>

<span data-ttu-id="59186-131">For the video frames (images), use the following images:</span><span class="sxs-lookup"><span data-stu-id="59186-131">For the video frames (images), use the following images:</span></span>

![Video frame thumbnail 1](images/ams-video-frame-thumbnails-1.PNG) | ![Video frame thumbnail 2](images/ams-video-frame-thumbnails-2.PNG) | ![Video frame thumbnail 3](images/ams-video-frame-thumbnails-3.PNG) |
| :---: | :---: | :---: |
[<span data-ttu-id="59186-135">Frame 1</span><span class="sxs-lookup"><span data-stu-id="59186-135">Frame 1</span></span>](https://blobthebuilder.blob.core.windows.net/sampleframes/ams-video-frame1-00-17.PNG) | [<span data-ttu-id="59186-136">Frame 2</span><span class="sxs-lookup"><span data-stu-id="59186-136">Frame 2</span></span>](https://blobthebuilder.blob.core.windows.net/sampleframes/ams-video-frame-2-01-04.PNG) | [<span data-ttu-id="59186-137">Frame 3</span><span class="sxs-lookup"><span data-stu-id="59186-137">Frame 3</span></span>](https://blobthebuilder.blob.core.windows.net/sampleframes/ams-video-frame-3-02-24.PNG) |

## <a name="create-your-visual-studio-project"></a><span data-ttu-id="59186-138">Create your Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="59186-138">Create your Visual Studio project</span></span>

1. <span data-ttu-id="59186-139">Add a new **Console app (.NET Framework)** project to your solution.</span><span class="sxs-lookup"><span data-stu-id="59186-139">Add a new **Console app (.NET Framework)** project to your solution.</span></span>

1. <span data-ttu-id="59186-140">Name the project **VideoReviews**.</span><span class="sxs-lookup"><span data-stu-id="59186-140">Name the project **VideoReviews**.</span></span>

1. <span data-ttu-id="59186-141">Select this project as the single startup project for the solution.</span><span class="sxs-lookup"><span data-stu-id="59186-141">Select this project as the single startup project for the solution.</span></span>

### <a name="install-required-packages"></a><span data-ttu-id="59186-142">Install required packages</span><span class="sxs-lookup"><span data-stu-id="59186-142">Install required packages</span></span>

<span data-ttu-id="59186-143">Install the following NuGet packages for the TermLists project.</span><span class="sxs-lookup"><span data-stu-id="59186-143">Install the following NuGet packages for the TermLists project.</span></span>

- <span data-ttu-id="59186-144">Microsoft.Azure.CognitiveServices.ContentModerator</span><span class="sxs-lookup"><span data-stu-id="59186-144">Microsoft.Azure.CognitiveServices.ContentModerator</span></span>
- <span data-ttu-id="59186-145">Microsoft.Rest.ClientRuntime</span><span class="sxs-lookup"><span data-stu-id="59186-145">Microsoft.Rest.ClientRuntime</span></span>
- <span data-ttu-id="59186-146">Microsoft.Rest.ClientRuntime.Azure</span><span class="sxs-lookup"><span data-stu-id="59186-146">Microsoft.Rest.ClientRuntime.Azure</span></span>
- <span data-ttu-id="59186-147">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="59186-147">Newtonsoft.Json</span></span>

### <a name="update-the-programs-using-statements"></a><span data-ttu-id="59186-148">Update the program's using statements</span><span class="sxs-lookup"><span data-stu-id="59186-148">Update the program's using statements</span></span>

<span data-ttu-id="59186-149">Modify the program's using statements as follows.</span><span class="sxs-lookup"><span data-stu-id="59186-149">Modify the program's using statements as follows.</span></span>

    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Threading;
    using Microsoft.Azure.CognitiveServices.ContentModerator;
    using Microsoft.CognitiveServices.ContentModerator;
    using Microsoft.CognitiveServices.ContentModerator.Models;
    using Newtonsoft.Json;


### <a name="add-private-properties"></a><span data-ttu-id="59186-150">Add private properties</span><span class="sxs-lookup"><span data-stu-id="59186-150">Add private properties</span></span>

<span data-ttu-id="59186-151">Add the following private properties to namespace VideoReviews, class Program.</span><span class="sxs-lookup"><span data-stu-id="59186-151">Add the following private properties to namespace VideoReviews, class Program.</span></span>

<span data-ttu-id="59186-152">Where indicated, replace the example values for these properties.</span><span class="sxs-lookup"><span data-stu-id="59186-152">Where indicated, replace the example values for these properties.</span></span>


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


### <a name="create-content-moderator-client-object"></a><span data-ttu-id="59186-153">Create Content Moderator Client object</span><span class="sxs-lookup"><span data-stu-id="59186-153">Create Content Moderator Client object</span></span>

<span data-ttu-id="59186-154">Add the following method definition to namespace VideoReviews, class Program.</span><span class="sxs-lookup"><span data-stu-id="59186-154">Add the following method definition to namespace VideoReviews, class Program.</span></span>

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

## <a name="create-a-video-review"></a><span data-ttu-id="59186-155">Create a video review</span><span class="sxs-lookup"><span data-stu-id="59186-155">Create a video review</span></span>

<span data-ttu-id="59186-156">Create a video review with **ContentModeratorClient.Reviews.CreateVideoReviews**.</span><span class="sxs-lookup"><span data-stu-id="59186-156">Create a video review with **ContentModeratorClient.Reviews.CreateVideoReviews**.</span></span> <span data-ttu-id="59186-157">For more information, see the [API reference](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c4).</span><span class="sxs-lookup"><span data-stu-id="59186-157">For more information, see the [API reference](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c4).</span></span>

<span data-ttu-id="59186-158">**CreateVideoReviews** has the following required parameters:</span><span class="sxs-lookup"><span data-stu-id="59186-158">**CreateVideoReviews** has the following required parameters:</span></span>
1. <span data-ttu-id="59186-159">A string that contains a MIME type, which should be "application/json."</span><span class="sxs-lookup"><span data-stu-id="59186-159">A string that contains a MIME type, which should be "application/json."</span></span> 
1. <span data-ttu-id="59186-160">Your Content Moderator team name.</span><span class="sxs-lookup"><span data-stu-id="59186-160">Your Content Moderator team name.</span></span>
1. <span data-ttu-id="59186-161">An **IList<CreateVideoReviewsBodyItem>** object.</span><span class="sxs-lookup"><span data-stu-id="59186-161">An **IList<CreateVideoReviewsBodyItem>** object.</span></span> <span data-ttu-id="59186-162">Each **CreateVideoReviewsBodyItem** object represents a video review.</span><span class="sxs-lookup"><span data-stu-id="59186-162">Each **CreateVideoReviewsBodyItem** object represents a video review.</span></span> <span data-ttu-id="59186-163">This quickstart creates one review at a time.</span><span class="sxs-lookup"><span data-stu-id="59186-163">This quickstart creates one review at a time.</span></span>

<span data-ttu-id="59186-164">**CreateVideoReviewsBodyItem** has several properties.</span><span class="sxs-lookup"><span data-stu-id="59186-164">**CreateVideoReviewsBodyItem** has several properties.</span></span> <span data-ttu-id="59186-165">At a minimum, you set the following properties:</span><span class="sxs-lookup"><span data-stu-id="59186-165">At a minimum, you set the following properties:</span></span>
- <span data-ttu-id="59186-166">**Content**.</span><span class="sxs-lookup"><span data-stu-id="59186-166">**Content**.</span></span> <span data-ttu-id="59186-167">The URL of the video to be reviewed.</span><span class="sxs-lookup"><span data-stu-id="59186-167">The URL of the video to be reviewed.</span></span>
- <span data-ttu-id="59186-168">**ContentId**.</span><span class="sxs-lookup"><span data-stu-id="59186-168">**ContentId**.</span></span> <span data-ttu-id="59186-169">An ID to assign to the video review.</span><span class="sxs-lookup"><span data-stu-id="59186-169">An ID to assign to the video review.</span></span>
- <span data-ttu-id="59186-170">**Status**.</span><span class="sxs-lookup"><span data-stu-id="59186-170">**Status**.</span></span> <span data-ttu-id="59186-171">Set the value to "Unpublished."</span><span class="sxs-lookup"><span data-stu-id="59186-171">Set the value to "Unpublished."</span></span> <span data-ttu-id="59186-172">If you do not set it, it defaults to "Pending", which means the video review is published and pending human review.</span><span class="sxs-lookup"><span data-stu-id="59186-172">If you do not set it, it defaults to "Pending", which means the video review is published and pending human review.</span></span> <span data-ttu-id="59186-173">Once a video review is published, you can no longer add video frames, a transcript, or a transcript moderation result to it.</span><span class="sxs-lookup"><span data-stu-id="59186-173">Once a video review is published, you can no longer add video frames, a transcript, or a transcript moderation result to it.</span></span>

> [!NOTE]
> <span data-ttu-id="59186-174">**CreateVideoReviews** returns an IList<string>.</span><span class="sxs-lookup"><span data-stu-id="59186-174">**CreateVideoReviews** returns an IList<string>.</span></span> <span data-ttu-id="59186-175">Each of these strings contains an ID for a video review.</span><span class="sxs-lookup"><span data-stu-id="59186-175">Each of these strings contains an ID for a video review.</span></span> <span data-ttu-id="59186-176">These IDs are GUIDs and are not the same as the value of the **ContentId** property.</span><span class="sxs-lookup"><span data-stu-id="59186-176">These IDs are GUIDs and are not the same as the value of the **ContentId** property.</span></span> 

<span data-ttu-id="59186-177">Add the following method definition to namespace VideoReviews, class Program.</span><span class="sxs-lookup"><span data-stu-id="59186-177">Add the following method definition to namespace VideoReviews, class Program.</span></span>

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
> <span data-ttu-id="59186-178">Your Content Moderator service key has a requests per second (RPS) rate limit, and if you exceed the limit, the SDK throws an exception with a 429 error code.</span><span class="sxs-lookup"><span data-stu-id="59186-178">Your Content Moderator service key has a requests per second (RPS) rate limit, and if you exceed the limit, the SDK throws an exception with a 429 error code.</span></span> 
>
> <span data-ttu-id="59186-179">A free tier key has a one RPS rate limit.</span><span class="sxs-lookup"><span data-stu-id="59186-179">A free tier key has a one RPS rate limit.</span></span>

## <a name="add-video-frames-to-the-video-review"></a><span data-ttu-id="59186-180">Add video frames to the video review</span><span class="sxs-lookup"><span data-stu-id="59186-180">Add video frames to the video review</span></span>

<span data-ttu-id="59186-181">You add video frames to a video review with **ContentModeratorClient.Reviews.AddVideoFrameUrl** (if your video frames are hosted online) or **ContentModeratorClient.Reviews.AddVideoFrameStream** (if your video frames are hosted locally).</span><span class="sxs-lookup"><span data-stu-id="59186-181">You add video frames to a video review with **ContentModeratorClient.Reviews.AddVideoFrameUrl** (if your video frames are hosted online) or **ContentModeratorClient.Reviews.AddVideoFrameStream** (if your video frames are hosted locally).</span></span> <span data-ttu-id="59186-182">This quickstart assumes your video frames are hosted online, and so uses **AddVideoFrameUrl**.</span><span class="sxs-lookup"><span data-stu-id="59186-182">This quickstart assumes your video frames are hosted online, and so uses **AddVideoFrameUrl**.</span></span> <span data-ttu-id="59186-183">For more information, see the [API reference](https://westus2.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/59e7b76ae7151f0b10d451fd).</span><span class="sxs-lookup"><span data-stu-id="59186-183">For more information, see the [API reference](https://westus2.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/59e7b76ae7151f0b10d451fd).</span></span>

<span data-ttu-id="59186-184">**AddVideoFrameUrl** has the following required parameters:</span><span class="sxs-lookup"><span data-stu-id="59186-184">**AddVideoFrameUrl** has the following required parameters:</span></span>
1. <span data-ttu-id="59186-185">A string that contains a MIME type, which should be "application/json."</span><span class="sxs-lookup"><span data-stu-id="59186-185">A string that contains a MIME type, which should be "application/json."</span></span>
1. <span data-ttu-id="59186-186">Your Content Moderator team name.</span><span class="sxs-lookup"><span data-stu-id="59186-186">Your Content Moderator team name.</span></span>
1. <span data-ttu-id="59186-187">The video review ID returned by **CreateVideoReviews**.</span><span class="sxs-lookup"><span data-stu-id="59186-187">The video review ID returned by **CreateVideoReviews**.</span></span>
1. <span data-ttu-id="59186-188">An **IList<VideoFrameBodyItem>** object.</span><span class="sxs-lookup"><span data-stu-id="59186-188">An **IList<VideoFrameBodyItem>** object.</span></span> <span data-ttu-id="59186-189">Each **VideoFrameBodyItem** object represents a video frame.</span><span class="sxs-lookup"><span data-stu-id="59186-189">Each **VideoFrameBodyItem** object represents a video frame.</span></span>

<span data-ttu-id="59186-190">**VideoFrameBodyItem** has the following properties:</span><span class="sxs-lookup"><span data-stu-id="59186-190">**VideoFrameBodyItem** has the following properties:</span></span>
- <span data-ttu-id="59186-191">**Timestamp**.</span><span class="sxs-lookup"><span data-stu-id="59186-191">**Timestamp**.</span></span> <span data-ttu-id="59186-192">A string that contains, in seconds, the time in the video from which the video frame was taken.</span><span class="sxs-lookup"><span data-stu-id="59186-192">A string that contains, in seconds, the time in the video from which the video frame was taken.</span></span>
- <span data-ttu-id="59186-193">**FrameImage**.</span><span class="sxs-lookup"><span data-stu-id="59186-193">**FrameImage**.</span></span> <span data-ttu-id="59186-194">The URL of the video frame.</span><span class="sxs-lookup"><span data-stu-id="59186-194">The URL of the video frame.</span></span>
- <span data-ttu-id="59186-195">**Metadata**.</span><span class="sxs-lookup"><span data-stu-id="59186-195">**Metadata**.</span></span> <span data-ttu-id="59186-196">An IList<VideoFrameBodyItemMetadataItem>.</span><span class="sxs-lookup"><span data-stu-id="59186-196">An IList<VideoFrameBodyItemMetadataItem>.</span></span> <span data-ttu-id="59186-197">**VideoFrameBodyItemMetadataItem** is simply a key/value pair.</span><span class="sxs-lookup"><span data-stu-id="59186-197">**VideoFrameBodyItemMetadataItem** is simply a key/value pair.</span></span> <span data-ttu-id="59186-198">Valid keys include:</span><span class="sxs-lookup"><span data-stu-id="59186-198">Valid keys include:</span></span>
- <span data-ttu-id="59186-199">**reviewRecommended**.</span><span class="sxs-lookup"><span data-stu-id="59186-199">**reviewRecommended**.</span></span> <span data-ttu-id="59186-200">True if a human review of the video frame is recommended.</span><span class="sxs-lookup"><span data-stu-id="59186-200">True if a human review of the video frame is recommended.</span></span>
- <span data-ttu-id="59186-201">**adultScore**.</span><span class="sxs-lookup"><span data-stu-id="59186-201">**adultScore**.</span></span> <span data-ttu-id="59186-202">A value from 0 to 1 that rates the severity of adult content in the video frame.</span><span class="sxs-lookup"><span data-stu-id="59186-202">A value from 0 to 1 that rates the severity of adult content in the video frame.</span></span>
- <span data-ttu-id="59186-203">**a**.</span><span class="sxs-lookup"><span data-stu-id="59186-203">**a**.</span></span> <span data-ttu-id="59186-204">True if the video contains adult content.</span><span class="sxs-lookup"><span data-stu-id="59186-204">True if the video contains adult content.</span></span>
- <span data-ttu-id="59186-205">**racyScore**.</span><span class="sxs-lookup"><span data-stu-id="59186-205">**racyScore**.</span></span> <span data-ttu-id="59186-206">A value from 0 to 1 that rates the severity of racy content in the video frame.</span><span class="sxs-lookup"><span data-stu-id="59186-206">A value from 0 to 1 that rates the severity of racy content in the video frame.</span></span>
- <span data-ttu-id="59186-207">**r**.</span><span class="sxs-lookup"><span data-stu-id="59186-207">**r**.</span></span> <span data-ttu-id="59186-208">True if the video frame contains racy content.</span><span class="sxs-lookup"><span data-stu-id="59186-208">True if the video frame contains racy content.</span></span>
- <span data-ttu-id="59186-209">**ReviewerResultTags**.</span><span class="sxs-lookup"><span data-stu-id="59186-209">**ReviewerResultTags**.</span></span> <span data-ttu-id="59186-210">An IList<VideoFrameBodyItemReviewerResultTagsItem>.</span><span class="sxs-lookup"><span data-stu-id="59186-210">An IList<VideoFrameBodyItemReviewerResultTagsItem>.</span></span> <span data-ttu-id="59186-211">**VideoFrameBodyItemReviewerResultTagsItem** is simply a key/value pair.</span><span class="sxs-lookup"><span data-stu-id="59186-211">**VideoFrameBodyItemReviewerResultTagsItem** is simply a key/value pair.</span></span> <span data-ttu-id="59186-212">An application can use these tags to organize video frames.</span><span class="sxs-lookup"><span data-stu-id="59186-212">An application can use these tags to organize video frames.</span></span>

> [!NOTE]
> <span data-ttu-id="59186-213">This quickstart generates random values for the **adultScore** and **racyScore** properties.</span><span class="sxs-lookup"><span data-stu-id="59186-213">This quickstart generates random values for the **adultScore** and **racyScore** properties.</span></span> <span data-ttu-id="59186-214">In a production application, you would obtain these values from the [video moderation service](video-moderation-api.md), deployed as an Azure Media Service.</span><span class="sxs-lookup"><span data-stu-id="59186-214">In a production application, you would obtain these values from the [video moderation service](video-moderation-api.md), deployed as an Azure Media Service.</span></span>

<span data-ttu-id="59186-215">Add the following method definitions to namespace VideoReviews, class Program.</span><span class="sxs-lookup"><span data-stu-id="59186-215">Add the following method definitions to namespace VideoReviews, class Program.</span></span>

    <summary>
    /// Create a video frame to add to a video review after the video review is created.
    /// </summary>
    /// <param name="url">The URL of the video frame image.</param>
    /// <returns>The video frame.</returns>
    private static VideoFrameBodyItem CreateFrameToAddToReview(string url, string timestamp_seconds)
    {
        // We generate random "adult" and "racy" scores for the video frame.
        Random rand = new Random();

        var frame = new VideoFrameBodyItem
        {
            // The timestamp is measured in milliseconds. Convert from seconds.
            Timestamp = (int.Parse(timestamp_seconds) * 1000).ToString(),
            FrameImage = url,

            Metadata = new List<VideoFrameBodyItemMetadataItem>
            {
                new VideoFrameBodyItemMetadataItem("reviewRecommended", "true"),
                new VideoFrameBodyItemMetadataItem("adultScore", rand.NextDouble().ToString()),
                new VideoFrameBodyItemMetadataItem("a", "false"),
                new VideoFrameBodyItemMetadataItem("racyScore", rand.NextDouble().ToString()),
                new VideoFrameBodyItemMetadataItem("r", "false")
            },

            ReviewerResultTags = new List<VideoFrameBodyItemReviewerResultTagsItem>()
            {
                new VideoFrameBodyItemReviewerResultTagsItem("tag1", "value1")
            }
        };

        return frame;
    }

    /// <summary>
    /// Add a video frame to the indicated video review. For more information, see the API reference:
    /// https://westus2.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/59e7b76ae7151f0b10d451fd
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="review_id">The video review ID.</param>
    /// <param name="url">The URL of the video frame image.</param>
    static void AddFrame(ContentModeratorClient client, string review_id, string url, string timestamp_seconds)
    {
        Console.WriteLine("Adding a frame to the review with ID {0}.", review_id);

        var frames = new List<VideoFrameBodyItem>()
        {
            CreateFrameToAddToReview(url, timestamp_seconds)
        };
            
        client.Reviews.AddVideoFrameUrl("application/json", TeamName, review_id, frames);

        Thread.Sleep(throttleRate);
    

## <a name="get-video-frames-for-video-review"></a><span data-ttu-id="59186-216">Get video frames for video review</span><span class="sxs-lookup"><span data-stu-id="59186-216">Get video frames for video review</span></span>

<span data-ttu-id="59186-217">You can get the video frames for a video review with **ContentModeratorClient.Reviews.GetVideoFrames**.</span><span class="sxs-lookup"><span data-stu-id="59186-217">You can get the video frames for a video review with **ContentModeratorClient.Reviews.GetVideoFrames**.</span></span> <span data-ttu-id="59186-218">**GetVideoFrames** has the following required parameters:</span><span class="sxs-lookup"><span data-stu-id="59186-218">**GetVideoFrames** has the following required parameters:</span></span>
1. <span data-ttu-id="59186-219">Your Content Moderator team name.</span><span class="sxs-lookup"><span data-stu-id="59186-219">Your Content Moderator team name.</span></span>
1. <span data-ttu-id="59186-220">The video review ID returned by **CreateVideoReviews**.</span><span class="sxs-lookup"><span data-stu-id="59186-220">The video review ID returned by **CreateVideoReviews**.</span></span>
1. <span data-ttu-id="59186-221">The zero-based index of the first video frame to get.</span><span class="sxs-lookup"><span data-stu-id="59186-221">The zero-based index of the first video frame to get.</span></span>
1. <span data-ttu-id="59186-222">The number of video frames to get.</span><span class="sxs-lookup"><span data-stu-id="59186-222">The number of video frames to get.</span></span>

<span data-ttu-id="59186-223">Add the following method definition to namespace VideoReviews, class Program.</span><span class="sxs-lookup"><span data-stu-id="59186-223">Add the following method definition to namespace VideoReviews, class Program.</span></span>

    /// <summary>
    /// Get the video frames assigned to the indicated video review.  For more information, see the API reference:
    /// https://westus2.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/59e7ba43e7151f0b10d45200
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="review_id">The video review ID.</param>
    static void GetFrames(ContentModeratorClient client, string review_id)
    {
        Console.WriteLine("Getting frames for the review with ID {0}.", review_id);

        Frames result = client.Reviews.GetVideoFrames(TeamName, review_id, 0);
        Console.WriteLine(JsonConvert.SerializeObject(result, Formatting.Indented));

        Thread.Sleep(throttleRate);
    }

## <a name="get-video-review-information"></a><span data-ttu-id="59186-224">Get video review information</span><span class="sxs-lookup"><span data-stu-id="59186-224">Get video review information</span></span>

<span data-ttu-id="59186-225">You get information for a video review with **ContentModeratorClient.Reviews.GetReview**.</span><span class="sxs-lookup"><span data-stu-id="59186-225">You get information for a video review with **ContentModeratorClient.Reviews.GetReview**.</span></span> <span data-ttu-id="59186-226">**GetReview** has the following required parameters:</span><span class="sxs-lookup"><span data-stu-id="59186-226">**GetReview** has the following required parameters:</span></span>
1. <span data-ttu-id="59186-227">Your Content Moderator team name.</span><span class="sxs-lookup"><span data-stu-id="59186-227">Your Content Moderator team name.</span></span>
1. <span data-ttu-id="59186-228">The video review ID returned by **CreateVideoReviews**.</span><span class="sxs-lookup"><span data-stu-id="59186-228">The video review ID returned by **CreateVideoReviews**.</span></span>

<span data-ttu-id="59186-229">Add the following method definition to namespace VideoReviews, class Program.</span><span class="sxs-lookup"><span data-stu-id="59186-229">Add the following method definition to namespace VideoReviews, class Program.</span></span>

    /// <summary>
    /// Get the information for the indicated video review. For more information, see the reference API:
    /// https://westus2.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c2
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="review_id">The video review ID.</param>
    private static void GetReview(ContentModeratorClient client, string review_id)
    {
        Console.WriteLine("Getting the status for the review with ID {0}.", review_id);

        var result = client.Reviews.GetReview(ModeratorHelper.Clients.TeamName, review_id);
        Console.WriteLine(JsonConvert.SerializeObject(result, Formatting.Indented));

        Thread.Sleep(throttleRate);
    }

## <a name="publish-video-review"></a><span data-ttu-id="59186-230">Publish video review</span><span class="sxs-lookup"><span data-stu-id="59186-230">Publish video review</span></span>

<span data-ttu-id="59186-231">You publish a video review with **ContentModeratorClient.Reviews.PublishVideoReview**.</span><span class="sxs-lookup"><span data-stu-id="59186-231">You publish a video review with **ContentModeratorClient.Reviews.PublishVideoReview**.</span></span> <span data-ttu-id="59186-232">**PublishVideoReview** has the following required parameters:</span><span class="sxs-lookup"><span data-stu-id="59186-232">**PublishVideoReview** has the following required parameters:</span></span>
1. <span data-ttu-id="59186-233">Your Content Moderator team name.</span><span class="sxs-lookup"><span data-stu-id="59186-233">Your Content Moderator team name.</span></span>
1. <span data-ttu-id="59186-234">The video review ID returned by **CreateVideoReviews**.</span><span class="sxs-lookup"><span data-stu-id="59186-234">The video review ID returned by **CreateVideoReviews**.</span></span>

<span data-ttu-id="59186-235">Add the following method definition to namespace VideoReviews, class Program.</span><span class="sxs-lookup"><span data-stu-id="59186-235">Add the following method definition to namespace VideoReviews, class Program.</span></span>

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

## <a name="putting-it-all-together"></a><span data-ttu-id="59186-236">Putting it all together</span><span class="sxs-lookup"><span data-stu-id="59186-236">Putting it all together</span></span>

<span data-ttu-id="59186-237">Add the **Main** method definition to namespace VideoReviews, class Program.</span><span class="sxs-lookup"><span data-stu-id="59186-237">Add the **Main** method definition to namespace VideoReviews, class Program.</span></span> <span data-ttu-id="59186-238">Finally, close the Program class and the VideoReviews namespace.</span><span class="sxs-lookup"><span data-stu-id="59186-238">Finally, close the Program class and the VideoReviews namespace.</span></span>

    static void Main(string[] args)
    {
        using (ContentModeratorClient client = NewClient())
        {
            // Create a review with the content pointing to a streaming endpoint (manifest)
            var streamingcontent = "https://amssamples.streaming.mediaservices.windows.net/91492735-c523-432b-ba01-faba6c2206a2/AzureMediaServicesPromo.ism/manifest";
            string review_id = CreateReview(client, "review1", streamingcontent);

            var frame1_url = "https://blobthebuilder.blob.core.windows.net/sampleframes/ams-video-frame1-00-17.PNG";
            var frame2_url = "https://blobthebuilder.blob.core.windows.net/sampleframes/ams-video-frame-2-01-04.PNG";
            var frame3_url = "https://blobthebuilder.blob.core.windows.net/sampleframes/ams-video-frame-3-02-24.PNG";

            // Add the frames from 17, 64, and 144 seconds.
            AddFrame(client, review_id, frame1_url, "17");
            AddFrame(client, review_id, frame2_url, "64");
            AddFrame(client, review_id, frame3_url, "144");

            // Get frames information and show
            GetFrames(client, review_id);
            GetReview(client, review_id);

            // Publish the review
            PublishReview(client, review_id);

            Console.WriteLine("Open your Content Moderator Dashboard and select Review > Video to see the review.");
            Console.WriteLine("Press any key to close the application.");
            Console.Read();
        }
    }

## <a name="run-the-program-and-review-the-output"></a><span data-ttu-id="59186-239">Run the program and review the output</span><span class="sxs-lookup"><span data-stu-id="59186-239">Run the program and review the output</span></span>
<span data-ttu-id="59186-240">When you run the application, you see an output on the following lines:</span><span class="sxs-lookup"><span data-stu-id="59186-240">When you run the application, you see an output on the following lines:</span></span>

    Creating a video review.
    Adding a frame to the review with ID 201801v3212bda70ced4928b2cd7459c290c7dc.
    Adding a frame to the review with ID 201801v3212bda70ced4928b2cd7459c290c7dc.
    Adding a frame to the review with ID 201801v3212bda70ced4928b2cd7459c290c7dc.
    Getting frames for the review with ID 201801v3212bda70ced4928b2cd7459c290c7dc.
    {
        "ReviewId": "201801v3212bda70ced4928b2cd7459c290c7dc",
        "VideoFrames": [
        {
            "Timestamp": "17000",
            "FrameImage": "https://reviewcontentprod.blob.core.windows.net/testreview6/FRM_201801v3212bda70ced4928b2cd7459c290c7dc_17000.PNG",
            "Metadata": [
            {
                "Key": "reviewRecommended",
                "Value": "true"
            },
            {
                "Key": "adultScore",
                "Value": "0.808312381528463"
            },
            {
                "Key": "a",
                "Value": "false"
            },
            {
                "Key": "racyScore",
                "Value": "0.846378884206702"
            },
            {
                "Key": "r",
                "Value": "false"
            }
            ],
            "ReviewerResultTags": [
            {
                "Key": "tag1",
                "Value": "value1"
            }
        ]
        },
        {
            "Timestamp": "64000",
            "FrameImage": "https://reviewcontentprod.blob.core.windows.net/testreview6/FRM_201801v3212bda70ced4928b2cd7459c290c7dc_64000.PNG",
            "Metadata": [
            {
                "Key": "reviewRecommended",
                "Value": "true"
            },
            {
                "Key": "adultScore",
                "Value": "0.576078300166912"
            },
            {
                "Key": "a",
                "Value": "false"
            },
            {
                "Key": "racyScore",
                "Value": "0.244768953064815"
            },
            {
                "Key": "r",
                "Value": "false"
            }
            ],
            "ReviewerResultTags": [
            {
                "Key": "tag1",
                "Value": "value1"
            }
        ]
        },
        {
            "Timestamp": "144000",
            "FrameImage": "https://reviewcontentprod.blob.core.windows.net/testreview6/FRM_201801v3212bda70ced4928b2cd7459c290c7dc_144000.PNG",
            "Metadata": [
            {
                "Key": "reviewRecommended",
                "Value": "true"
            },
            {
                "Key": "adultScore",
                "Value": "0.664480847150311"
            },
            {
                "Key": "a",
                "Value": "false"
            },
            {
                "Key": "racyScore",
                "Value": "0.933817870418456"
            },
            {
                "Key": "r",
                "Value": "false"
            }
            ],
            "ReviewerResultTags": [
            {
                "Key": "tag1",
                "Value": "value1"
            }
            ]
        }
        ]
    }
    
    Getting the status for the review with ID 201801v3212bda70ced4928b2cd7459c290c7dc.
    {
        "ReviewId": "201801v3212bda70ced4928b2cd7459c290c7dc",
        "SubTeam": "public",
        "Status": "UnPublished",
        "ReviewerResultTags": [],
        "CreatedBy": "testreview6",
        "Metadata": [
        {
            "Key": "FrameCount",
            "Value": "3"
        }
        ],
        "Type": "Video",
        "Content": "https://amssamples.streaming.mediaservices.windows.net/91492735-c523-432b-ba01-faba6c2206a2/AzureMediaServicesPromo.ism/manifest",
        "ContentId": "review1",
        "CallbackEndpoint": null
    }

    Publishing the review with ID 201801v3212bda70ced4928b2cd7459c290c7dc.
    Open your Content Moderator Dashboard and select Review > Video to see the review.
    Press any key to close the application.

## <a name="check-out-your-video-review"></a><span data-ttu-id="59186-241">Check out your video review</span><span class="sxs-lookup"><span data-stu-id="59186-241">Check out your video review</span></span>

<span data-ttu-id="59186-242">Finally, you see the video review in your Content Moderator review tool account on the **Review**>**Video** screen.</span><span class="sxs-lookup"><span data-stu-id="59186-242">Finally, you see the video review in your Content Moderator review tool account on the **Review**>**Video** screen.</span></span>

![Video review for human moderators](images/ams-video-review.PNG)

## <a name="next-steps"></a><span data-ttu-id="59186-244">Next steps</span><span class="sxs-lookup"><span data-stu-id="59186-244">Next steps</span></span>

<span data-ttu-id="59186-245">Get the [Content Moderator .NET SDK](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) and the [Visual Studio solution](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator) for this and other Content Moderator quickstarts for .NET.</span><span class="sxs-lookup"><span data-stu-id="59186-245">Get the [Content Moderator .NET SDK](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) and the [Visual Studio solution](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator) for this and other Content Moderator quickstarts for .NET.</span></span>

<span data-ttu-id="59186-246">Learn how to add [transcript moderation](video-transcript-moderation-review-tutorial-dotnet.md) to the video review.</span><span class="sxs-lookup"><span data-stu-id="59186-246">Learn how to add [transcript moderation](video-transcript-moderation-review-tutorial-dotnet.md) to the video review.</span></span> 

<span data-ttu-id="59186-247">Check out the detailed tutorial on how to develop a [complete video moderation solution](video-transcript-moderation-review-tutorial-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="59186-247">Check out the detailed tutorial on how to develop a [complete video moderation solution](video-transcript-moderation-review-tutorial-dotnet.md).</span></span>
