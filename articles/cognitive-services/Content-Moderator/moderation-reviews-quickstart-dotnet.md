---
title: Azure Content Moderator - Create reviews using .NET | Microsoft Docs
description: How to create reviews using Azure Content Moderator SDK for .NET
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 09/10/2018
ms.author: sajagtap
ms.openlocfilehash: 32e18273ad92f6b415b2a0219fd8b0520fe707f3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870620"
---
# <a name="create-reviews-using-net"></a><span data-ttu-id="d8e19-103">Create reviews using .NET</span><span class="sxs-lookup"><span data-stu-id="d8e19-103">Create reviews using .NET</span></span>

<span data-ttu-id="d8e19-104">This article provides information and code samples to help you get started using the [Content Moderator SDK for .NET](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) to:</span><span class="sxs-lookup"><span data-stu-id="d8e19-104">This article provides information and code samples to help you get started using the [Content Moderator SDK for .NET](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) to:</span></span>
 
- <span data-ttu-id="d8e19-105">Create a set of reviews for human moderators</span><span class="sxs-lookup"><span data-stu-id="d8e19-105">Create a set of reviews for human moderators</span></span>
- <span data-ttu-id="d8e19-106">Get the status of existing reviews for human moderators</span><span class="sxs-lookup"><span data-stu-id="d8e19-106">Get the status of existing reviews for human moderators</span></span>

<span data-ttu-id="d8e19-107">Generally, content goes through some automated moderation before being scheduled for human review.</span><span class="sxs-lookup"><span data-stu-id="d8e19-107">Generally, content goes through some automated moderation before being scheduled for human review.</span></span> <span data-ttu-id="d8e19-108">This article only covers how to create the review for human moderation.</span><span class="sxs-lookup"><span data-stu-id="d8e19-108">This article only covers how to create the review for human moderation.</span></span> <span data-ttu-id="d8e19-109">For a more complete scenario, see the [Facebook content moderation](facebook-post-moderation.md) and [eCommerce catalog moderation](ecommerce-retail-catalog-moderation.md) tutorials.</span><span class="sxs-lookup"><span data-stu-id="d8e19-109">For a more complete scenario, see the [Facebook content moderation](facebook-post-moderation.md) and [eCommerce catalog moderation](ecommerce-retail-catalog-moderation.md) tutorials.</span></span>

<span data-ttu-id="d8e19-110">This article assumes that you are already familiar with Visual Studio and C#.</span><span class="sxs-lookup"><span data-stu-id="d8e19-110">This article assumes that you are already familiar with Visual Studio and C#.</span></span>

## <a name="sign-up-for-content-moderator"></a><span data-ttu-id="d8e19-111">Sign up for Content Moderator</span><span class="sxs-lookup"><span data-stu-id="d8e19-111">Sign up for Content Moderator</span></span>

<span data-ttu-id="d8e19-112">Before you can use Content Moderator services through the REST API or the SDK, you need a subscription key.</span><span class="sxs-lookup"><span data-stu-id="d8e19-112">Before you can use Content Moderator services through the REST API or the SDK, you need a subscription key.</span></span>
<span data-ttu-id="d8e19-113">Refer to the [Quickstart](quick-start.md) to learn how you can obtain the key.</span><span class="sxs-lookup"><span data-stu-id="d8e19-113">Refer to the [Quickstart](quick-start.md) to learn how you can obtain the key.</span></span>

## <a name="sign-up-for-a-review-tool-account-if-not-completed-in-the-previous-step"></a><span data-ttu-id="d8e19-114">Sign up for a review tool account if not completed in the previous step</span><span class="sxs-lookup"><span data-stu-id="d8e19-114">Sign up for a review tool account if not completed in the previous step</span></span>

<span data-ttu-id="d8e19-115">If you got your Content Moderator from the Azure portal, also [sign up for the review tool account](https://contentmoderator.cognitive.microsoft.com/) and create a review team.</span><span class="sxs-lookup"><span data-stu-id="d8e19-115">If you got your Content Moderator from the Azure portal, also [sign up for the review tool account](https://contentmoderator.cognitive.microsoft.com/) and create a review team.</span></span> <span data-ttu-id="d8e19-116">You need the team Id and the review tool to call the review API to start a Job and view the reviews in the review tool.</span><span class="sxs-lookup"><span data-stu-id="d8e19-116">You need the team Id and the review tool to call the review API to start a Job and view the reviews in the review tool.</span></span>

## <a name="ensure-your-api-key-can-call-the-review-api-for-review-creation"></a><span data-ttu-id="d8e19-117">Ensure your API key can call the review API for review creation</span><span class="sxs-lookup"><span data-stu-id="d8e19-117">Ensure your API key can call the review API for review creation</span></span>

<span data-ttu-id="d8e19-118">After completing the previous steps, you may end up with two Content Moderator keys if you started from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d8e19-118">After completing the previous steps, you may end up with two Content Moderator keys if you started from the Azure portal.</span></span> 

<span data-ttu-id="d8e19-119">If you plan to use the Azure-provided API key in your SDK sample, follow the steps mentioned in the [Using Azure key with the review API](review-tool-user-guide/credentials.md#use-the-azure-account-with-the-review-tool-and-review-api) section to allow your application to call the review API and create reviews.</span><span class="sxs-lookup"><span data-stu-id="d8e19-119">If you plan to use the Azure-provided API key in your SDK sample, follow the steps mentioned in the [Using Azure key with the review API](review-tool-user-guide/credentials.md#use-the-azure-account-with-the-review-tool-and-review-api) section to allow your application to call the review API and create reviews.</span></span>

<span data-ttu-id="d8e19-120">If you use the free trial key generated by the review tool, your review tool account already knows about the key and therefore, no additional steps are required.</span><span class="sxs-lookup"><span data-stu-id="d8e19-120">If you use the free trial key generated by the review tool, your review tool account already knows about the key and therefore, no additional steps are required.</span></span>

## <a name="create-your-visual-studio-project"></a><span data-ttu-id="d8e19-121">Create your Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="d8e19-121">Create your Visual Studio project</span></span>

1. <span data-ttu-id="d8e19-122">Add a new **Console app (.NET Framework)** project to your solution.</span><span class="sxs-lookup"><span data-stu-id="d8e19-122">Add a new **Console app (.NET Framework)** project to your solution.</span></span>

   <span data-ttu-id="d8e19-123">In the sample code, name the project **CreateReviews**.</span><span class="sxs-lookup"><span data-stu-id="d8e19-123">In the sample code, name the project **CreateReviews**.</span></span>

1. <span data-ttu-id="d8e19-124">Select this project as the single startup project for the solution.</span><span class="sxs-lookup"><span data-stu-id="d8e19-124">Select this project as the single startup project for the solution.</span></span>

### <a name="install-required-packages"></a><span data-ttu-id="d8e19-125">Install required packages</span><span class="sxs-lookup"><span data-stu-id="d8e19-125">Install required packages</span></span>

<span data-ttu-id="d8e19-126">Install the following NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="d8e19-126">Install the following NuGet packages:</span></span>

- <span data-ttu-id="d8e19-127">Microsoft.Azure.CognitiveServices.ContentModerator</span><span class="sxs-lookup"><span data-stu-id="d8e19-127">Microsoft.Azure.CognitiveServices.ContentModerator</span></span>
- <span data-ttu-id="d8e19-128">Microsoft.Rest.ClientRuntime</span><span class="sxs-lookup"><span data-stu-id="d8e19-128">Microsoft.Rest.ClientRuntime</span></span>
- <span data-ttu-id="d8e19-129">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="d8e19-129">Newtonsoft.Json</span></span>

### <a name="update-the-programs-using-statements"></a><span data-ttu-id="d8e19-130">Update the program's using statements</span><span class="sxs-lookup"><span data-stu-id="d8e19-130">Update the program's using statements</span></span>

<span data-ttu-id="d8e19-131">Modify the program's using statements.</span><span class="sxs-lookup"><span data-stu-id="d8e19-131">Modify the program's using statements.</span></span>

    using Microsoft.Azure.CognitiveServices.ContentModerator;
    using Microsoft.CognitiveServices.ContentModerator;
    using Microsoft.CognitiveServices.ContentModerator.Models;
    using Newtonsoft.Json;
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Threading;

### <a name="create-the-content-moderator-client"></a><span data-ttu-id="d8e19-132">Create the Content Moderator client</span><span class="sxs-lookup"><span data-stu-id="d8e19-132">Create the Content Moderator client</span></span>

<span data-ttu-id="d8e19-133">Add the following code to create a Content Moderator client for your subscription.</span><span class="sxs-lookup"><span data-stu-id="d8e19-133">Add the following code to create a Content Moderator client for your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d8e19-134">Update the **AzureRegion** and **CMSubscriptionKey** fields with the values of your region identifier and subscription key.</span><span class="sxs-lookup"><span data-stu-id="d8e19-134">Update the **AzureRegion** and **CMSubscriptionKey** fields with the values of your region identifier and subscription key.</span></span>


    /// <summary>
    /// Wraps the creation and configuration of a Content Moderator client.
    /// </summary>
    /// <remarks>This class library contains insecure code. If you adapt this 
    /// code for use in production, use a secure method of storing and using
    /// your Content Moderator subscription key.</remarks>
    public static class Clients
    {
        /// <summary>
        /// The region/location for your Content Moderator account, 
        /// for example, westus.
        /// </summary>
        private static readonly string AzureRegion = "YOUR API REGION";

        /// <summary>
        /// The base URL fragment for Content Moderator calls.
        /// </summary>
        private static readonly string AzureBaseURL =
            $"https://{AzureRegion}.api.cognitive.microsoft.com";

        /// <summary>
        /// Your Content Moderator subscription key.
        /// </summary>
        private static readonly string CMSubscriptionKey = "YOUR API KEY";

        /// <summary>
        /// Returns a new Content Moderator client for your subscription.
        /// </summary>
        /// <returns>The new client.</returns>
        /// <remarks>The <see cref="ContentModeratorClient"/> is disposable.
        /// When you have finished using the client,
        /// you should dispose of it either directly or indirectly. </remarks>
        public static ContentModeratorClient NewClient()
        {
            // Create and initialize an instance of the Content Moderator API wrapper.
            ContentModeratorClient client = new ContentModeratorClient(new ApiKeyServiceClientCredentials(CMSubscriptionKey));

            client.BaseUrl = AzureBaseURL;
            return client;
        }
    }

## <a name="create-a-class-to-associate-internal-content-information-with-a-review-id"></a><span data-ttu-id="d8e19-135">Create a class to associate internal content information with a review ID</span><span class="sxs-lookup"><span data-stu-id="d8e19-135">Create a class to associate internal content information with a review ID</span></span>

<span data-ttu-id="d8e19-136">Add the following class to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="d8e19-136">Add the following class to the **Program** class.</span></span>
<span data-ttu-id="d8e19-137">Use this class to associate the review ID to your internal content ID for the item.</span><span class="sxs-lookup"><span data-stu-id="d8e19-137">Use this class to associate the review ID to your internal content ID for the item.</span></span>

    /// <summary>
    /// Associates the review ID (assigned by the service) to the internal
    /// content ID of the item.
    /// </summary>
    public class ReviewItem
    {
        /// <summary>
        /// The media type for the item to review.
        /// </summary>
        public string Type;

        /// <summary>
        /// The URL of the item to review.
        /// </summary>
        public string Url;

        /// <summary>
        /// The internal content ID for the item to review.
        /// </summary>
        public string ContentId;

        /// <summary>
        /// The ID that the service assigned to the review.
        /// </summary>
        public string ReviewId;
    }

### <a name="initialize-application-specific-settings"></a><span data-ttu-id="d8e19-138">Initialize application-specific settings</span><span class="sxs-lookup"><span data-stu-id="d8e19-138">Initialize application-specific settings</span></span>

> [!NOTE]
> <span data-ttu-id="d8e19-139">Your Content Moderator service key has a requests per second (RPS) rate limit, and if you exceed the limit, the SDK throws an exception with a 429 error code.</span><span class="sxs-lookup"><span data-stu-id="d8e19-139">Your Content Moderator service key has a requests per second (RPS) rate limit, and if you exceed the limit, the SDK throws an exception with a 429 error code.</span></span> 
>
> <span data-ttu-id="d8e19-140">A free tier key has a one RPS rate limit.</span><span class="sxs-lookup"><span data-stu-id="d8e19-140">A free tier key has a one RPS rate limit.</span></span>

#### <a name="add-the-following-constants-to-the-program-class-in-programcs"></a><span data-ttu-id="d8e19-141">Add the following constants to the **Program** class in Program.cs.</span><span class="sxs-lookup"><span data-stu-id="d8e19-141">Add the following constants to the **Program** class in Program.cs.</span></span>
    
    /// <summary>
    /// The minimum amount of time, in milliseconds, to wait between calls
    /// to the Image List API.
    /// </summary>
    private const int throttleRate = 3000;

    /// <summary>
    /// The number of seconds to delay after a review has finished before
    /// getting the review results from the server.
    /// </summary>
    private const double latencyDelay = 45;

    /// <summary>
    /// The name of the log file to create.
    /// </summary>
    /// <remarks>Relative paths are ralative the execution directory.</remarks>
    private const string OutputFile = "OutputLog.txt";

#### <a name="add-the-following-constants-and-static-fields-to-the-program-class-in-programcs"></a><span data-ttu-id="d8e19-142">Add the following constants and static fields to the **Program** class in Program.cs.</span><span class="sxs-lookup"><span data-stu-id="d8e19-142">Add the following constants and static fields to the **Program** class in Program.cs.</span></span>

<span data-ttu-id="d8e19-143">Update these values to contain information specific to your subscription and team.</span><span class="sxs-lookup"><span data-stu-id="d8e19-143">Update these values to contain information specific to your subscription and team.</span></span>

> [!NOTE]
> <span data-ttu-id="d8e19-144">You set the TeamName constant to the name you used when you created your [Content Moderator review tool](https://contentmoderator.cognitive.microsoft.com/) subscription.</span><span class="sxs-lookup"><span data-stu-id="d8e19-144">You set the TeamName constant to the name you used when you created your [Content Moderator review tool](https://contentmoderator.cognitive.microsoft.com/) subscription.</span></span> <span data-ttu-id="d8e19-145">You retrieve the TeamName from the **Credentials** section in the **Settings** (gear) menu.</span><span class="sxs-lookup"><span data-stu-id="d8e19-145">You retrieve the TeamName from the **Credentials** section in the **Settings** (gear) menu.</span></span>
>
> <span data-ttu-id="d8e19-146">Your team name is the value of the **Id** field in the **API** section.</span><span class="sxs-lookup"><span data-stu-id="d8e19-146">Your team name is the value of the **Id** field in the **API** section.</span></span>

    /// <summary>
    /// The name of the team to assign the review to.
    /// </summary>
    /// <remarks>This must be the team name you used to create your 
    /// Content Moderator account. You can retrieve your team name from
    /// the Conent Moderator web site. Your team name is the Id associated 
    /// with your subscription.</remarks>
    private const string TeamName = "YOUR REVIEW TEAM ID";

    /// <summary>
    /// The optional name of the subteam to assign the review to.
    /// </summary>
    private const string Subteam = null;

    /// <summary>
    /// The callback endpoint for completed reviews.
    /// </summary>
    /// <remarks>Revies show up for reviewers on your team. 
    /// As reviewers complete reviews, results are sent to the
    /// callback endpoint using an HTTP POST request.</remarks>
    private const string CallbackEndpoint = "YOUR API ENDPOINT";

    /// <summary>
    /// The media type for the item to review.
    /// </summary>
    /// <remarks>Valid values are "image", "text", and "video".</remarks>
    private const string MediaType = "image";

    /// <summary>
    /// The URLs of the images to create review jobs for.
    /// </summary>
    private static readonly string[] ImageUrls = new string[] {
        "https://moderatorsampleimages.blob.core.windows.net/samples/sample1.jpg"
        // add more if you want
    };

    /// <summary>
    /// The metadata key to initially add to each review item.
    /// </summary>
    private const string MetadataKey = "sc";

    /// <summary>
    /// The metadata value to initially add to each review item.
    /// </summary>
    private const string MetadataValue = "true";

#### <a name="add-the-following-static-fields-to-the-program-class-in-programcs"></a><span data-ttu-id="d8e19-147">Add the following static fields to the **Program** class in Program.cs.</span><span class="sxs-lookup"><span data-stu-id="d8e19-147">Add the following static fields to the **Program** class in Program.cs.</span></span>

<span data-ttu-id="d8e19-148">Use these fields to track the application state.</span><span class="sxs-lookup"><span data-stu-id="d8e19-148">Use these fields to track the application state.</span></span>

    /// <summary>
    /// A static reference to the text writer to use for logging.
    /// </summary>
    private static TextWriter writer;

    /// <summary>
    /// The cached review information, associating a local content ID
    /// to the created review ID for each item.
    /// </summary>
    private static List<ReviewItem> reviewItems =
        new List<ReviewItem>();

## <a name="create-a-method-to-write-messages-to-the-log-file"></a><span data-ttu-id="d8e19-149">Create a method to write messages to the log file</span><span class="sxs-lookup"><span data-stu-id="d8e19-149">Create a method to write messages to the log file</span></span>

<span data-ttu-id="d8e19-150">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="d8e19-150">Add the following method to the **Program** class.</span></span> 

    /// <summary>
    /// Writes a message to the log file, and optionally to the console.
    /// </summary>
    /// <param name="message">The message.</param>
    /// <param name="echo">if set to <c>true</c>, write the message to the console.</param>
    private static void WriteLine(string message = null, bool echo = false)
    {
        writer.WriteLine(message ?? String.Empty);

        if (echo)
        {
            Console.WriteLine(message ?? String.Empty);
        }
    }

## <a name="create-a-method-to-create-a-set-of-reviews"></a><span data-ttu-id="d8e19-151">Create a method to create a set of reviews</span><span class="sxs-lookup"><span data-stu-id="d8e19-151">Create a method to create a set of reviews</span></span>

<span data-ttu-id="d8e19-152">Normally, you have some business logic for identifying incoming images, text, or video that needs to be reviewed.</span><span class="sxs-lookup"><span data-stu-id="d8e19-152">Normally, you have some business logic for identifying incoming images, text, or video that needs to be reviewed.</span></span> <span data-ttu-id="d8e19-153">However, here just use a fixed list of images.</span><span class="sxs-lookup"><span data-stu-id="d8e19-153">However, here just use a fixed list of images.</span></span>

<span data-ttu-id="d8e19-154">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="d8e19-154">Add the following method to the **Program** class.</span></span>

    /// <summary>
    /// Create the reviews using the fixed list of images.
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    private static void CreateReviews(ContentModeratorClient client)
    {
        WriteLine(null, true);
        WriteLine("Creating reviews for the following images:", true);

        // Create the structure to hold the request body information.
        List<CreateReviewBodyItem> requestInfo =
            new List<CreateReviewBodyItem>();

        // Create some standard metadata to add to each item.
        List<CreateReviewBodyItemMetadataItem> metadata =
            new List<CreateReviewBodyItemMetadataItem>(
            new CreateReviewBodyItemMetadataItem[] {
                new CreateReviewBodyItemMetadataItem(
                    MetadataKey, MetadataValue)
            });

        // Populate the request body information and the initial cached review information.
        for (int i = 0; i < ImageUrls.Length; i++)
        {
            // Cache the local information with which to create the review.
            var itemInfo = new ReviewItem()
            {
                Type = MediaType,
                ContentId = i.ToString(),
                Url = ImageUrls[i],
                ReviewId = null
            };

            WriteLine($" - {itemInfo.Url}; with id = {itemInfo.ContentId}.", true);

            // Add the item informaton to the request information.
            requestInfo.Add(new CreateReviewBodyItem(
                itemInfo.Type, itemInfo.Url, itemInfo.ContentId,
                CallbackEndpoint, metadata));

            // Cache the review creation information.
            reviewItems.Add(itemInfo);
        }

        var reviewResponse = client.Reviews.CreateReviewsWithHttpMessagesAsync(
            "application/json", TeamName, requestInfo);

        // Update the local cache to associate the created review IDs with
        // the associated content.
        var reviewIds = reviewResponse.Result.Body;
        for (int i = 0; i < reviewIds.Count; i++)
        {
            Program.reviewItems[i].ReviewId = reviewIds[i];
        }

        WriteLine(JsonConvert.SerializeObject(
        reviewIds, Formatting.Indented));

        Thread.Sleep(throttleRate);
    }

## <a name="create-a-method-to-get-the-status-of-existing-reviews"></a><span data-ttu-id="d8e19-155">Create a method to get the status of existing reviews</span><span class="sxs-lookup"><span data-stu-id="d8e19-155">Create a method to get the status of existing reviews</span></span>

<span data-ttu-id="d8e19-156">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="d8e19-156">Add the following method to the **Program** class.</span></span> 

> [!Note]
> <span data-ttu-id="d8e19-157">In practice, you would set the callback URL `CallbackEndpoint` to the URL that would receive the results of the manual review (via an HTTP POST request).</span><span class="sxs-lookup"><span data-stu-id="d8e19-157">In practice, you would set the callback URL `CallbackEndpoint` to the URL that would receive the results of the manual review (via an HTTP POST request).</span></span>
> <span data-ttu-id="d8e19-158">You could modify this method to check on the status of pending reviews.</span><span class="sxs-lookup"><span data-stu-id="d8e19-158">You could modify this method to check on the status of pending reviews.</span></span>

    /// <summary>
    /// Gets the review details from the server.
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    private static void GetReviewDetails(ContentModeratorClient client)
    {
        WriteLine(null, true);
        WriteLine("Getting review details:", true);
        foreach (var item in reviewItems)
        {
            var reviewDetail = client.Reviews.GetReviewWithHttpMessagesAsync(
                TeamName, item.ReviewId);

            WriteLine(
                $"Review {item.ReviewId} for item ID {item.ContentId} is " +
                $"{reviewDetail.Result.Body.Status}.", true);
            WriteLine(JsonConvert.SerializeObject(
                reviewDetail.Result.Body, Formatting.Indented));

            Thread.Sleep(throttleRate);
        }
    }

## <a name="add-code-to-create-a-set-of-reviews-and-check-its-status"></a><span data-ttu-id="d8e19-159">Add code to create a set of reviews and check its status</span><span class="sxs-lookup"><span data-stu-id="d8e19-159">Add code to create a set of reviews and check its status</span></span>

<span data-ttu-id="d8e19-160">Add the following code to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="d8e19-160">Add the following code to the **Main** method.</span></span>

<span data-ttu-id="d8e19-161">This code simulates many of the operations that you perform in defining and managing the list, as well as using the list to screen images.</span><span class="sxs-lookup"><span data-stu-id="d8e19-161">This code simulates many of the operations that you perform in defining and managing the list, as well as using the list to screen images.</span></span> <span data-ttu-id="d8e19-162">The logging features allow you to see the response objects generated by the SDK calls to the Content Moderator service.</span><span class="sxs-lookup"><span data-stu-id="d8e19-162">The logging features allow you to see the response objects generated by the SDK calls to the Content Moderator service.</span></span>

    using (TextWriter outputWriter = new StreamWriter(OutputFile, false))
    {
        writer = outputWriter;
        using (var client = Clients.NewClient())
        {
            CreateReviews(client);
            GetReviewDetails(client);

            Console.WriteLine();
            Console.WriteLine("Perform manual reviews on the Content Moderator site.");
            Console.WriteLine("Then, press any key to continue.");
            Console.ReadKey();

            Console.WriteLine();
            Console.WriteLine($"Waiting {latencyDelay} seconds for results to propigate.");
            Thread.Sleep(latencyDelay * 1000);

            GetReviewDetails(client);
        }

        writer = null;
        outputWriter.Flush();
        outputWriter.Close();
    }

    Console.WriteLine();
    Console.WriteLine("Press any key to exit...");
    Console.ReadKey();

## <a name="run-the-program-and-review-the-output"></a><span data-ttu-id="d8e19-163">Run the program and review the output</span><span class="sxs-lookup"><span data-stu-id="d8e19-163">Run the program and review the output</span></span>

<span data-ttu-id="d8e19-164">You see the following sample output:</span><span class="sxs-lookup"><span data-stu-id="d8e19-164">You see the following sample output:</span></span>

    Creating reviews for the following images:
        - https://moderatorsampleimages.blob.core.windows.net/samples/sample1.jpg; with id = 0.

    Getting review details:
    Review 201712i46950138c61a4740b118a43cac33f434 for item ID 0 is Pending.

<span data-ttu-id="d8e19-165">Sign into the Content Moderator review tool to see the pending image review with the **sc** label set to **true**.</span><span class="sxs-lookup"><span data-stu-id="d8e19-165">Sign into the Content Moderator review tool to see the pending image review with the **sc** label set to **true**.</span></span> <span data-ttu-id="d8e19-166">You also see the default **a** and **r** tags and any custom tags that you may have defined within the review tool.</span><span class="sxs-lookup"><span data-stu-id="d8e19-166">You also see the default **a** and **r** tags and any custom tags that you may have defined within the review tool.</span></span> 

<span data-ttu-id="d8e19-167">Use the **Next** button to submit.</span><span class="sxs-lookup"><span data-stu-id="d8e19-167">Use the **Next** button to submit.</span></span>

![Image review for human moderators](images/moderation-reviews-quickstart-dotnet.PNG)

<span data-ttu-id="d8e19-169">Then, press any key to continue.</span><span class="sxs-lookup"><span data-stu-id="d8e19-169">Then, press any key to continue.</span></span>

    Waiting 45 seconds for results to propagate.

    Getting review details:
    Review 201712i46950138c61a4740b118a43cac33f434 for item ID 0 is Complete.

    Press any key to exit...

## <a name="check-out-the-following-output-in-the-log-file"></a><span data-ttu-id="d8e19-170">Check out the following output in the log file.</span><span class="sxs-lookup"><span data-stu-id="d8e19-170">Check out the following output in the log file.</span></span>

> [!NOTE]
> <span data-ttu-id="d8e19-171">In your output file, the strings "\{teamname}" and "\{callbackUrl}" reflect the values for the `TeamName` and `CallbackEndpoint` fields, respectively.</span><span class="sxs-lookup"><span data-stu-id="d8e19-171">In your output file, the strings "\{teamname}" and "\{callbackUrl}" reflect the values for the `TeamName` and `CallbackEndpoint` fields, respectively.</span></span>

<span data-ttu-id="d8e19-172">The review IDs and the image content URLs are different each time you run the application, and when a review is complete, the `reviewerResultTags` field reflects how the reviewer tagged the item.</span><span class="sxs-lookup"><span data-stu-id="d8e19-172">The review IDs and the image content URLs are different each time you run the application, and when a review is complete, the `reviewerResultTags` field reflects how the reviewer tagged the item.</span></span>

    Creating reviews for the following images:
        - https://moderatorsampleimages.blob.core.windows.net/samples/sample1.jpg; with id = 0.
    [
        "201712i46950138c61a4740b118a43cac33f434",
    ]

    Getting review details:
    Review 201712i46950138c61a4740b118a43cac33f434 for item ID 0 is Pending.
    {
        "reviewId": "201712i46950138c61a4740b118a43cac33f434",
        "subTeam": "public",
        "status": "Pending",
        "reviewerResultTags": [],
        "createdBy": "{teamname}",
        "metadata": [
        {
            "key": "sc",
            "value": "true"
        }
        ],
        "type": "Image",
        "content": "https://reviewcontentprod.blob.core.windows.net/{teamname}/IMG_201712i46950138c61a4740b118a43cac33f434",
        "contentId": "0",
        "callbackEndpoint": "{callbackUrl}"
    }

    Getting review details:
    Review 201712i46950138c61a4740b118a43cac33f434 for item ID 0 is Complete.
    {
        "reviewId": "201712i46950138c61a4740b118a43cac33f434",
        "subTeam": "public",
        "status": "Complete",
        "reviewerResultTags": [
        {
            "key": "a",
            "value": "False"
        },
        {
            "key": "r",
            "value": "True"
        },
        {
            "key": "sc",
            "value": "True"
        }
        ],
        "createdBy": "{teamname}",
        "metadata": [
        {
            "key": "sc",
            "value": "true"
        }
        ],
        "type": "Image",
        "content": "https://reviewcontentprod.blob.core.windows.net/{teamname}/IMG_201712i46950138c61a4740b118a43cac33f434",
        "contentId": "0",
        "callbackEndpoint": "{callbackUrl}"
    }

## <a name="your-callback-url-if-provided-receives-this-response"></a><span data-ttu-id="d8e19-173">Your callback Url if provided, receives this response</span><span class="sxs-lookup"><span data-stu-id="d8e19-173">Your callback Url if provided, receives this response</span></span>

<span data-ttu-id="d8e19-174">You see a response like the following example:</span><span class="sxs-lookup"><span data-stu-id="d8e19-174">You see a response like the following example:</span></span>

    {
        "ReviewId": "201801i48a2937e679a41c7966e838c92f5e649",
        "ModifiedOn": "2018-01-06T05:04:40.5525865Z",
        "ModifiedBy": "yourusername",
        "CallBackType": "Review",
        "ContentId": "0",
        "ContentType": "Image",
        "Metadata": {
            "sc": "true"
            },
        "ReviewerResultTags": {
            "a": "False",
            "r": "False",
        }
    }


## <a name="next-steps"></a><span data-ttu-id="d8e19-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="d8e19-175">Next steps</span></span>

<span data-ttu-id="d8e19-176">Get the [Content Moderator .NET SDK](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) and the [Visual Studio solution](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator) for this and other Content Moderator quickstarts for .NET, and get started on your integration.</span><span class="sxs-lookup"><span data-stu-id="d8e19-176">Get the [Content Moderator .NET SDK](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) and the [Visual Studio solution](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator) for this and other Content Moderator quickstarts for .NET, and get started on your integration.</span></span>