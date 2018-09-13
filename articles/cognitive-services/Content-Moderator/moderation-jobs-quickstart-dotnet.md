---
title: Azure Content Moderator - Start moderation jobs using .NET | Microsoft Docs
description: How to initiate moderation jobs using Azure Content Moderator SDK for .NET
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 09/10/2018
ms.author: sajagtap
ms.openlocfilehash: 0402d9dc1dfee5e146d3550d095f4fb53e52f12b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857365"
---
# <a name="start-moderation-jobs-using-net"></a><span data-ttu-id="09900-103">Start moderation jobs using .NET</span><span class="sxs-lookup"><span data-stu-id="09900-103">Start moderation jobs using .NET</span></span>

<span data-ttu-id="09900-104">This article provides information and code samples to help you get started using the [Content Moderator SDK for .NET](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) to:</span><span class="sxs-lookup"><span data-stu-id="09900-104">This article provides information and code samples to help you get started using the [Content Moderator SDK for .NET](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) to:</span></span>
 
- <span data-ttu-id="09900-105">Start a moderation job to scan and create reviews for human moderators</span><span class="sxs-lookup"><span data-stu-id="09900-105">Start a moderation job to scan and create reviews for human moderators</span></span>
- <span data-ttu-id="09900-106">Get the status of the pending review</span><span class="sxs-lookup"><span data-stu-id="09900-106">Get the status of the pending review</span></span>
- <span data-ttu-id="09900-107">Track and get the final status of the review</span><span class="sxs-lookup"><span data-stu-id="09900-107">Track and get the final status of the review</span></span>
- <span data-ttu-id="09900-108">Submit the result to the callback Url</span><span class="sxs-lookup"><span data-stu-id="09900-108">Submit the result to the callback Url</span></span>

<span data-ttu-id="09900-109">This article assumes that you are already familiar with Visual Studio and C#.</span><span class="sxs-lookup"><span data-stu-id="09900-109">This article assumes that you are already familiar with Visual Studio and C#.</span></span>

## <a name="sign-up-for-content-moderator"></a><span data-ttu-id="09900-110">Sign up for Content Moderator</span><span class="sxs-lookup"><span data-stu-id="09900-110">Sign up for Content Moderator</span></span>

<span data-ttu-id="09900-111">Before you can use Content Moderator services through the REST API or the SDK, you need a subscription key.</span><span class="sxs-lookup"><span data-stu-id="09900-111">Before you can use Content Moderator services through the REST API or the SDK, you need a subscription key.</span></span>
<span data-ttu-id="09900-112">Refer to the [Quickstart](quick-start.md) to learn how you can obtain the key.</span><span class="sxs-lookup"><span data-stu-id="09900-112">Refer to the [Quickstart](quick-start.md) to learn how you can obtain the key.</span></span>

## <a name="sign-up-for-a-review-tool-account-if-not-completed-in-the-previous-step"></a><span data-ttu-id="09900-113">Sign up for a review tool account if not completed in the previous step</span><span class="sxs-lookup"><span data-stu-id="09900-113">Sign up for a review tool account if not completed in the previous step</span></span>

<span data-ttu-id="09900-114">If you got your Content Moderator from the Azure portal, also [sign up for the review tool account](https://contentmoderator.cognitive.microsoft.com/) and create a review team.</span><span class="sxs-lookup"><span data-stu-id="09900-114">If you got your Content Moderator from the Azure portal, also [sign up for the review tool account](https://contentmoderator.cognitive.microsoft.com/) and create a review team.</span></span> <span data-ttu-id="09900-115">You need the team Id and the review tool to call the review API to start a Job and view the reviews in the review tool.</span><span class="sxs-lookup"><span data-stu-id="09900-115">You need the team Id and the review tool to call the review API to start a Job and view the reviews in the review tool.</span></span>

## <a name="ensure-your-api-key-can-call-the-review-api-for-review-creation"></a><span data-ttu-id="09900-116">Ensure your API key can call the review API for review creation</span><span class="sxs-lookup"><span data-stu-id="09900-116">Ensure your API key can call the review API for review creation</span></span>

<span data-ttu-id="09900-117">After completing the previous steps, you may end up with two Content Moderator keys if you started from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="09900-117">After completing the previous steps, you may end up with two Content Moderator keys if you started from the Azure portal.</span></span> 

<span data-ttu-id="09900-118">If you plan to use the Azure-provided API key in your SDK sample, follow the steps mentioned in the [Using Azure key with the review API](review-tool-user-guide/credentials.md#use-the-azure-account-with-the-review-tool-and-review-api) section to allow your application to call the review API and create reviews.</span><span class="sxs-lookup"><span data-stu-id="09900-118">If you plan to use the Azure-provided API key in your SDK sample, follow the steps mentioned in the [Using Azure key with the review API](review-tool-user-guide/credentials.md#use-the-azure-account-with-the-review-tool-and-review-api) section to allow your application to call the review API and create reviews.</span></span>

<span data-ttu-id="09900-119">If you use the free trial key generated by the review tool, your review tool account already knows about the key and therefore, no additional steps are required.</span><span class="sxs-lookup"><span data-stu-id="09900-119">If you use the free trial key generated by the review tool, your review tool account already knows about the key and therefore, no additional steps are required.</span></span>

## <a name="define-a-custom-moderation-workflow"></a><span data-ttu-id="09900-120">Define a custom moderation workflow</span><span class="sxs-lookup"><span data-stu-id="09900-120">Define a custom moderation workflow</span></span>

<span data-ttu-id="09900-121">A moderation job scans your content using the APIs and uses a **workflow** to determine whether to create reviews or not.</span><span class="sxs-lookup"><span data-stu-id="09900-121">A moderation job scans your content using the APIs and uses a **workflow** to determine whether to create reviews or not.</span></span>
<span data-ttu-id="09900-122">While the review tool contains a default workflow, let's [define a custom workflow](Review-Tool-User-Guide/Workflows.md) for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="09900-122">While the review tool contains a default workflow, let's [define a custom workflow](Review-Tool-User-Guide/Workflows.md) for this quickstart.</span></span>

<span data-ttu-id="09900-123">You use the name of the workflow in your code that starts the moderation job.</span><span class="sxs-lookup"><span data-stu-id="09900-123">You use the name of the workflow in your code that starts the moderation job.</span></span>

## <a name="create-your-visual-studio-project"></a><span data-ttu-id="09900-124">Create your Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="09900-124">Create your Visual Studio project</span></span>

1. <span data-ttu-id="09900-125">Add a new **Console app (.NET Framework)** project to your solution.</span><span class="sxs-lookup"><span data-stu-id="09900-125">Add a new **Console app (.NET Framework)** project to your solution.</span></span>

   <span data-ttu-id="09900-126">In the sample code, name the project **CreateReviews**.</span><span class="sxs-lookup"><span data-stu-id="09900-126">In the sample code, name the project **CreateReviews**.</span></span>

1. <span data-ttu-id="09900-127">Select this project as the single startup project for the solution.</span><span class="sxs-lookup"><span data-stu-id="09900-127">Select this project as the single startup project for the solution.</span></span>

### <a name="install-required-packages"></a><span data-ttu-id="09900-128">Install required packages</span><span class="sxs-lookup"><span data-stu-id="09900-128">Install required packages</span></span>

<span data-ttu-id="09900-129">Install the following NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="09900-129">Install the following NuGet packages:</span></span>

- <span data-ttu-id="09900-130">Microsoft.Azure.CognitiveServices.ContentModerator</span><span class="sxs-lookup"><span data-stu-id="09900-130">Microsoft.Azure.CognitiveServices.ContentModerator</span></span>
- <span data-ttu-id="09900-131">Microsoft.Rest.ClientRuntime</span><span class="sxs-lookup"><span data-stu-id="09900-131">Microsoft.Rest.ClientRuntime</span></span>
- <span data-ttu-id="09900-132">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="09900-132">Newtonsoft.Json</span></span>

### <a name="update-the-programs-using-statements"></a><span data-ttu-id="09900-133">Update the program's using statements</span><span class="sxs-lookup"><span data-stu-id="09900-133">Update the program's using statements</span></span>

<span data-ttu-id="09900-134">Modify the program's using statements.</span><span class="sxs-lookup"><span data-stu-id="09900-134">Modify the program's using statements.</span></span>

    using Microsoft.Azure.CognitiveServices.ContentModerator;
    using Microsoft.CognitiveServices.ContentModerator;
    using Microsoft.CognitiveServices.ContentModerator.Models;
    using Newtonsoft.Json;
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Threading;

### <a name="create-the-content-moderator-client"></a><span data-ttu-id="09900-135">Create the Content Moderator client</span><span class="sxs-lookup"><span data-stu-id="09900-135">Create the Content Moderator client</span></span>

<span data-ttu-id="09900-136">Add the following code to create a Content Moderator client for your subscription.</span><span class="sxs-lookup"><span data-stu-id="09900-136">Add the following code to create a Content Moderator client for your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09900-137">Update the **AzureRegion** and **CMSubscriptionKey** fields with the values of your region identifier and subscription key.</span><span class="sxs-lookup"><span data-stu-id="09900-137">Update the **AzureRegion** and **CMSubscriptionKey** fields with the values of your region identifier and subscription key.</span></span>


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

### <a name="initialize-application-specific-settings"></a><span data-ttu-id="09900-138">Initialize application-specific settings</span><span class="sxs-lookup"><span data-stu-id="09900-138">Initialize application-specific settings</span></span>

<span data-ttu-id="09900-139">Add the following constants and static fields to the **Program** class in Program.cs.</span><span class="sxs-lookup"><span data-stu-id="09900-139">Add the following constants and static fields to the **Program** class in Program.cs.</span></span>

> [!NOTE]
> <span data-ttu-id="09900-140">You set the TeamName constant to the name you used when you created your Content Moderator subscription.</span><span class="sxs-lookup"><span data-stu-id="09900-140">You set the TeamName constant to the name you used when you created your Content Moderator subscription.</span></span> <span data-ttu-id="09900-141">You retrieve TeamName from the [Content Moderator web site](https://westus.contentmoderator.cognitive.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="09900-141">You retrieve TeamName from the [Content Moderator web site](https://westus.contentmoderator.cognitive.microsoft.com/).</span></span>
> <span data-ttu-id="09900-142">Once you log in, select **Credentials** from the **Settings** (gear) menu.</span><span class="sxs-lookup"><span data-stu-id="09900-142">Once you log in, select **Credentials** from the **Settings** (gear) menu.</span></span>
>
> <span data-ttu-id="09900-143">Your team name is the value of the **Id** field in the **API** section.</span><span class="sxs-lookup"><span data-stu-id="09900-143">Your team name is the value of the **Id** field in the **API** section.</span></span>


    /// <summary>
    /// The moderation job will use this workflow that you defined earlier.
    /// See the quickstart article to learn how to setup custom workflows.
    /// </summary>
    private const string WorkflowName = "OCR";
    
    /// <summary>
    /// The name of the team to assign the job to.
    /// </summary>
    /// <remarks>This must be the team name you used to create your 
    /// Content Moderator account. You can retrieve your team name from
    /// the Conent Moderator web site. Your team name is the Id associated 
    /// with your subscription.</remarks>
    private const string TeamName = "***";

    /// <summary>
    /// The URL of the image to create a review job for.
    /// </summary>
    private const string ImageUrl =
        "https://moderatorsampleimages.blob.core.windows.net/samples/sample5.png";

    /// <summary>
    /// The name of the log file to create.
    /// </summary>
    /// <remarks>Relative paths are ralative the execution directory.</remarks>
    private const string OutputFile = "OutputLog.txt";

    /// <summary>
    /// The number of seconds to delay after a review has finished before
    /// getting the review results from the server.
    /// </summary>
    private const int latencyDelay = 45;

    /// <summary>
    /// The callback endpoint for completed reviews.
    /// </summary>
    /// <remarks>Revies show up for reviewers on your team. 
    /// As reviewers complete reviews, results are sent to the
    /// callback endpoint using an HTTP POST request.</remarks>
    private const string CallbackEndpoint = "";

## <a name="add-code-to-auto-moderate-create-a-review-and-get-the-job-details"></a><span data-ttu-id="09900-144">Add code to auto-moderate, create a review, and get the job details</span><span class="sxs-lookup"><span data-stu-id="09900-144">Add code to auto-moderate, create a review, and get the job details</span></span>

> [!Note]
> <span data-ttu-id="09900-145">In practice, you set the callback URL **CallbackEndpoint** to the URL that receives the results of the manual review (via an HTTP POST request).</span><span class="sxs-lookup"><span data-stu-id="09900-145">In practice, you set the callback URL **CallbackEndpoint** to the URL that receives the results of the manual review (via an HTTP POST request).</span></span>

<span data-ttu-id="09900-146">Start by adding the following code to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="09900-146">Start by adding the following code to the **Main** method.</span></span>

    using (TextWriter writer = new StreamWriter(OutputFile, false))
    {
        using (var client = Clients.NewClient())
        {
            writer.WriteLine("Create review job for an image.");
            var content = new Content(ImageUrl);
        
            // The WorkflowName contains the nameof the workflow defined in the online review tool.
            // See the quickstart article to learn more.
            var jobResult = client.Reviews.CreateJobWithHttpMessagesAsync(
                    TeamName, "image", "contentID", WorkflowName, "application/json", content, CallbackEndpoint);

            // Record the job ID.
            var jobId = jobResult.Result.Body.JobIdProperty;

            // Log just the response body from the returned task.
            writer.WriteLine(JsonConvert.SerializeObject(
                jobResult.Result.Body, Formatting.Indented));

            Thread.Sleep(2000);
            writer.WriteLine();

            writer.WriteLine("Get review job status.");
            var jobDetails = client.Reviews.GetJobDetailsWithHttpMessagesAsync(
                    TeamName, jobId);

            // Log just the response body from the returned task.
            writer.WriteLine(JsonConvert.SerializeObject(
                    jobDetails.Result.Body, Formatting.Indented));

            Console.WriteLine();
            Console.WriteLine("Perform manual reviews on the Content Moderator site.");
            Console.WriteLine("Then, press any key to continue.");
            Console.ReadKey();

            Console.WriteLine();
            Console.WriteLine($"Waiting {latencyDelay} seconds for results to propagate.");
            Thread.Sleep(latencyDelay * 1000);

            writer.WriteLine("Get review details.");
            jobDetails = client.Reviews.GetJobDetailsWithHttpMessagesAsync(
            TeamName, jobId);

            // Log just the response body from the returned task.
            writer.WriteLine(JsonConvert.SerializeObject(
            jobDetails.Result.Body, Formatting.Indented));
        }
        writer.Flush();
        writer.Close();
    }

> [!NOTE]
> <span data-ttu-id="09900-147">Your Content Moderator service key has a requests per second (RPS) rate limit.</span><span class="sxs-lookup"><span data-stu-id="09900-147">Your Content Moderator service key has a requests per second (RPS) rate limit.</span></span> <span data-ttu-id="09900-148">If you exceed the limit, the SDK throws an exception with a 429 error code.</span><span class="sxs-lookup"><span data-stu-id="09900-148">If you exceed the limit, the SDK throws an exception with a 429 error code.</span></span> 
>
> <span data-ttu-id="09900-149">A free tier key has a one RPS rate limit.</span><span class="sxs-lookup"><span data-stu-id="09900-149">A free tier key has a one RPS rate limit.</span></span>

## <a name="run-the-program-and-review-the-output"></a><span data-ttu-id="09900-150">Run the program and review the output</span><span class="sxs-lookup"><span data-stu-id="09900-150">Run the program and review the output</span></span>

<span data-ttu-id="09900-151">You see the following sample output in the console:</span><span class="sxs-lookup"><span data-stu-id="09900-151">You see the following sample output in the console:</span></span>

    Perform manual reviews on the Content Moderator site.
    Then, press any key to continue.

<span data-ttu-id="09900-152">Sign into the Content Moderator review tool to see the pending image review.</span><span class="sxs-lookup"><span data-stu-id="09900-152">Sign into the Content Moderator review tool to see the pending image review.</span></span>

<span data-ttu-id="09900-153">Use the **Next** button to submit.</span><span class="sxs-lookup"><span data-stu-id="09900-153">Use the **Next** button to submit.</span></span>

![Image review for human moderators](images/ocr-sample-image.PNG)

## <a name="see-the-sample-output-in-the-log-file"></a><span data-ttu-id="09900-155">See the sample output in the log file</span><span class="sxs-lookup"><span data-stu-id="09900-155">See the sample output in the log file</span></span>

> [!NOTE]
> <span data-ttu-id="09900-156">In your output file, the strings **Teamname**, **ContentId**, **CallBackEndpoint**, and **WorkflowId** reflect the values you used earlier.</span><span class="sxs-lookup"><span data-stu-id="09900-156">In your output file, the strings **Teamname**, **ContentId**, **CallBackEndpoint**, and **WorkflowId** reflect the values you used earlier.</span></span>

    Create moderation job for an image.
    {
        "JobId": "2018014caceddebfe9446fab29056fd8d31ffe"
    }

    Get review details.
    {
        "Id": "2018014caceddebfe9446fab29056fd8d31ffe",
        "TeamName": "some team name",
        "Status": "InProgress",
        "WorkflowId": "OCR",
        "Type": "Image",
        "CallBackEndpoint": "",
        "ReviewId": "",
        "ResultMetaData": [],
        "JobExecutionReport": [
        {
            "Ts": "2018-01-07T00:38:26.7714671",
            "Msg": "Successfully got hasText response from Moderator"
        },
        {
            "Ts": "2018-01-07T00:38:26.4181346",
            "Msg": "Getting hasText from Moderator"
        },
        {
            "Ts": "2018-01-07T00:38:25.5122828",
            "Msg": "Starting Execution - Try 1"
        }
        ]
    }


## <a name="your-callback-url-if-provided-receives-this-response"></a><span data-ttu-id="09900-157">Your callback Url if provided, receives this response.</span><span class="sxs-lookup"><span data-stu-id="09900-157">Your callback Url if provided, receives this response.</span></span>

<span data-ttu-id="09900-158">You see a response like the following example:</span><span class="sxs-lookup"><span data-stu-id="09900-158">You see a response like the following example:</span></span>

> [!NOTE]
> <span data-ttu-id="09900-159">In your callback response, the strings **ContentId** and **WorkflowId** reflect the values you used earlier.</span><span class="sxs-lookup"><span data-stu-id="09900-159">In your callback response, the strings **ContentId** and **WorkflowId** reflect the values you used earlier.</span></span>

    {
        "JobId": "2018014caceddebfe9446fab29056fd8d31ffe",
        "ReviewId": "201801i28fc0f7cbf424447846e509af853ea54",
        "WorkFlowId": "OCR",
        "Status": "Complete",
        "ContentType": "Image",
        "CallBackType": "Job",
        "ContentId": "contentID",
        "Metadata": {
            "hastext": "True",
            "ocrtext": "IF WE DID \r\nALL \r\nTHE THINGS \r\nWE ARE \r\nCAPABLE \r\nOF DOING, \r\nWE WOULD \r\nLITERALLY \r\nASTOUND \r\nOURSELVE \r\n",
            "imagename": "contentID"
        }
    }


## <a name="next-steps"></a><span data-ttu-id="09900-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="09900-160">Next steps</span></span>

<span data-ttu-id="09900-161">Get the [Content Moderator .NET SDK](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) and the [Visual Studio solution](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator) for this and other Content Moderator quickstarts for .NET, and get started on your integration.</span><span class="sxs-lookup"><span data-stu-id="09900-161">Get the [Content Moderator .NET SDK](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) and the [Visual Studio solution](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator) for this and other Content Moderator quickstarts for .NET, and get started on your integration.</span></span>
