---
title: Moderate with custom image lists in Azure Content Moderator | Microsoft Docs
description: How to moderate with custom image lists using Azure Content Moderator SDK for .NET.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 09/14/2018
ms.author: sajagtap
ms.openlocfilehash: 11c24a395a7a37132d89a2215c3a6a882f4e6acf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968300"
---
# <a name="moderate-with-custom-image-lists-in-net"></a><span data-ttu-id="0a50e-103">Moderate with custom image lists in .NET</span><span class="sxs-lookup"><span data-stu-id="0a50e-103">Moderate with custom image lists in .NET</span></span>

<span data-ttu-id="0a50e-104">This article provides information and code samples to help you get started using the [Content Moderator SDK for .NET](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) to:</span><span class="sxs-lookup"><span data-stu-id="0a50e-104">This article provides information and code samples to help you get started using the [Content Moderator SDK for .NET](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) to:</span></span>
- <span data-ttu-id="0a50e-105">Create a custom image list</span><span class="sxs-lookup"><span data-stu-id="0a50e-105">Create a custom image list</span></span>
- <span data-ttu-id="0a50e-106">Add and remove images from the list</span><span class="sxs-lookup"><span data-stu-id="0a50e-106">Add and remove images from the list</span></span>
- <span data-ttu-id="0a50e-107">Get the IDs of all images in the list</span><span class="sxs-lookup"><span data-stu-id="0a50e-107">Get the IDs of all images in the list</span></span>
- <span data-ttu-id="0a50e-108">Retrieve and update list metadata</span><span class="sxs-lookup"><span data-stu-id="0a50e-108">Retrieve and update list metadata</span></span>
- <span data-ttu-id="0a50e-109">Refresh the list search index</span><span class="sxs-lookup"><span data-stu-id="0a50e-109">Refresh the list search index</span></span>
- <span data-ttu-id="0a50e-110">Screen images against images in the list</span><span class="sxs-lookup"><span data-stu-id="0a50e-110">Screen images against images in the list</span></span>
- <span data-ttu-id="0a50e-111">Delete all images from the list</span><span class="sxs-lookup"><span data-stu-id="0a50e-111">Delete all images from the list</span></span>
- <span data-ttu-id="0a50e-112">Delete the custom list</span><span class="sxs-lookup"><span data-stu-id="0a50e-112">Delete the custom list</span></span>

> [!NOTE]
> <span data-ttu-id="0a50e-113">There is a maximum limit of **5 image lists** with each list to **not exceed 10,000 images**.</span><span class="sxs-lookup"><span data-stu-id="0a50e-113">There is a maximum limit of **5 image lists** with each list to **not exceed 10,000 images**.</span></span>
>

<span data-ttu-id="0a50e-114">The console application for this quickstart simulates some of the tasks you can perform with the image list API.</span><span class="sxs-lookup"><span data-stu-id="0a50e-114">The console application for this quickstart simulates some of the tasks you can perform with the image list API.</span></span>

<span data-ttu-id="0a50e-115">This article assumes that you are already familiar with Visual Studio and C#.</span><span class="sxs-lookup"><span data-stu-id="0a50e-115">This article assumes that you are already familiar with Visual Studio and C#.</span></span>

## <a name="sign-up-for-content-moderator-services"></a><span data-ttu-id="0a50e-116">Sign up for Content Moderator services</span><span class="sxs-lookup"><span data-stu-id="0a50e-116">Sign up for Content Moderator services</span></span>

<span data-ttu-id="0a50e-117">Before you can use Content Moderator services through the REST API or the SDK, you need a subscription key.</span><span class="sxs-lookup"><span data-stu-id="0a50e-117">Before you can use Content Moderator services through the REST API or the SDK, you need a subscription key.</span></span>
<span data-ttu-id="0a50e-118">Refer to the [Quickstart](quick-start.md) to learn how you can obtain the key.</span><span class="sxs-lookup"><span data-stu-id="0a50e-118">Refer to the [Quickstart](quick-start.md) to learn how you can obtain the key.</span></span>

## <a name="create-your-visual-studio-project"></a><span data-ttu-id="0a50e-119">Create your Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="0a50e-119">Create your Visual Studio project</span></span>

1. <span data-ttu-id="0a50e-120">Add a new **Console app (.NET Framework)** project to your solution.</span><span class="sxs-lookup"><span data-stu-id="0a50e-120">Add a new **Console app (.NET Framework)** project to your solution.</span></span>

   <span data-ttu-id="0a50e-121">In the sample code, name the project **ImageLists**.</span><span class="sxs-lookup"><span data-stu-id="0a50e-121">In the sample code, name the project **ImageLists**.</span></span>

1. <span data-ttu-id="0a50e-122">Select this project as the single startup project for the solution.</span><span class="sxs-lookup"><span data-stu-id="0a50e-122">Select this project as the single startup project for the solution.</span></span>

### <a name="install-required-packages"></a><span data-ttu-id="0a50e-123">Install required packages</span><span class="sxs-lookup"><span data-stu-id="0a50e-123">Install required packages</span></span>

<span data-ttu-id="0a50e-124">Install the following NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="0a50e-124">Install the following NuGet packages:</span></span>

- <span data-ttu-id="0a50e-125">Microsoft.Azure.CognitiveServices.ContentModerator</span><span class="sxs-lookup"><span data-stu-id="0a50e-125">Microsoft.Azure.CognitiveServices.ContentModerator</span></span>
- <span data-ttu-id="0a50e-126">Microsoft.Rest.ClientRuntime</span><span class="sxs-lookup"><span data-stu-id="0a50e-126">Microsoft.Rest.ClientRuntime</span></span>
- <span data-ttu-id="0a50e-127">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="0a50e-127">Newtonsoft.Json</span></span>

### <a name="update-the-programs-using-statements"></a><span data-ttu-id="0a50e-128">Update the program's using statements</span><span class="sxs-lookup"><span data-stu-id="0a50e-128">Update the program's using statements</span></span>

<span data-ttu-id="0a50e-129">Modify the program's using statements.</span><span class="sxs-lookup"><span data-stu-id="0a50e-129">Modify the program's using statements.</span></span>

    using Microsoft.Azure.CognitiveServices.ContentModerator;
    using Microsoft.CognitiveServices.ContentModerator;
    using Microsoft.CognitiveServices.ContentModerator.Models;
    using Newtonsoft.Json;
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Threading;

### <a name="create-the-content-moderator-client"></a><span data-ttu-id="0a50e-130">Create the Content Moderator client</span><span class="sxs-lookup"><span data-stu-id="0a50e-130">Create the Content Moderator client</span></span>

<span data-ttu-id="0a50e-131">Add the following code to create a Content Moderator client for your subscription.</span><span class="sxs-lookup"><span data-stu-id="0a50e-131">Add the following code to create a Content Moderator client for your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a50e-132">Update the **AzureRegion** and **CMSubscriptionKey** fields with the values of your region identifier and subscription key.</span><span class="sxs-lookup"><span data-stu-id="0a50e-132">Update the **AzureRegion** and **CMSubscriptionKey** fields with the values of your region identifier and subscription key.</span></span>


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


### <a name="initialize-application-specific-settings"></a><span data-ttu-id="0a50e-133">Initialize application-specific settings</span><span class="sxs-lookup"><span data-stu-id="0a50e-133">Initialize application-specific settings</span></span>

<span data-ttu-id="0a50e-134">Add the following classes and static fields to the **Program** class in Program.cs.</span><span class="sxs-lookup"><span data-stu-id="0a50e-134">Add the following classes and static fields to the **Program** class in Program.cs.</span></span>

    /// <summary>
    /// The minimum amount of time, im milliseconds, to wait between calls
    /// to the Image List API.
    /// </summary>
    private const int throttleRate = 3000;

    /// <summary>
    /// The number of minutes to delay after updating the search index before
    /// performing image match operations against a the list.
    /// </summary>
    private const double latencyDelay = 0.5;

    /// <summary>
    /// Define constants for the labels to apply to the image list.
    /// </summary>
    private class Labels
    {
        public const string Sports = "Sports";
        public const string Swimsuit = "Swimsuit";
    }

    /// <summary>
    /// Define input data for images for this sample.
    /// </summary>
    private class Images
    {
        /// <summary>
        /// Represents a group of images that all share the same label.
        /// </summary>
        public class Data
        {
            /// <summary>
            /// The label for the images.
            /// </summary>
            public string Label;

            /// <summary>
            /// The URLs of the images.
            /// </summary>
            public string[] Urls;
        }

        /// <summary>
        /// The initial set of images to add to the list with the sports label.
        /// </summary>
        public static readonly Data Sports = new Data()
        {
            Label = Labels.Sports,
            Urls = new string[] {
                "https://moderatorsampleimages.blob.core.windows.net/samples/sample4.png",
                "https://moderatorsampleimages.blob.core.windows.net/samples/sample6.png",
                "https://moderatorsampleimages.blob.core.windows.net/samples/sample9.png"
            }
        };

        /// <summary>
        /// The initial set of images to add to the list with the swimsuit label.
        /// </summary>
        /// <remarks>We're adding sample16.png (image of a puppy), to simulate
        /// an improperly added image that we will later remove from the list.
        /// Note: each image can have only one entry in a list, so sample4.png
        /// will throw an exception when we try to add it with a new label.</remarks>
        public static readonly Data Swimsuit = new Data()
        {
            Label = Labels.Swimsuit,
            Urls = new string[] {
                "https://moderatorsampleimages.blob.core.windows.net/samples/sample1.jpg",
                "https://moderatorsampleimages.blob.core.windows.net/samples/sample3.png",
                "https://moderatorsampleimages.blob.core.windows.net/samples/sample4.png",
                "https://moderatorsampleimages.blob.core.windows.net/samples/sample16.png"
            }
        };

        /// <summary>
        /// The set of images to subsequently remove from the list.
        /// </summary>
        public static readonly string[] Corrections = new string[] {
            "https://moderatorsampleimages.blob.core.windows.net/samples/sample16.png"
        };
    }

    /// <summary>
    /// The images to match against the image list.
    /// </summary>
    /// <remarks>Samples 1 and 4 should scan as matches; samples 5 and 16 should not.</remarks>
    private static readonly string[] ImagesToScreen = new string[] {
        "https://moderatorsampleimages.blob.core.windows.net/samples/sample1.jpg",
        "https://moderatorsampleimages.blob.core.windows.net/samples/sample4.png",
        "https://moderatorsampleimages.blob.core.windows.net/samples/sample5.png",
        "https://moderatorsampleimages.blob.core.windows.net/samples/sample16.png"
    };

    /// <summary>
    /// A dictionary that tracks the ID assigned to each image URL when 
    /// the image is added to the list.
    /// </summary>
    /// <remarks>Indexed by URL.</remarks>
    private static readonly Dictionary<string, int> ImageIdMap =
        new Dictionary<string, int>();

    /// <summary>
    /// The name of the file to contain the output from the list management operations.
    /// </summary>
    /// <remarks>Relative paths are ralative the execution directory.</remarks>
    private static string OutputFile = "ListOutput.log";

    /// <summary>
    /// A static reference to the text writer to use for logging.
    /// </summary>
    private static TextWriter writer;

    /// <summary>
    /// A copy of the list details.
    /// </summary>
    /// <remarks>Used to initially create the list, and later to update the
    /// list details.</remarks>
    private static Body listDetails;
   

> [!NOTE]
> <span data-ttu-id="0a50e-135">Your Content Moderator service key has a requests per second (RPS) rate limit, and if you exceed the limit, the SDK throws an exception with a 429 error code.</span><span class="sxs-lookup"><span data-stu-id="0a50e-135">Your Content Moderator service key has a requests per second (RPS) rate limit, and if you exceed the limit, the SDK throws an exception with a 429 error code.</span></span> 
>
> <span data-ttu-id="0a50e-136">A free tier key has a one RPS rate limit.</span><span class="sxs-lookup"><span data-stu-id="0a50e-136">A free tier key has a one RPS rate limit.</span></span>


## <a name="create-a-method-to-write-messages-to-the-log-file"></a><span data-ttu-id="0a50e-137">Create a method to write messages to the log file</span><span class="sxs-lookup"><span data-stu-id="0a50e-137">Create a method to write messages to the log file</span></span>

<span data-ttu-id="0a50e-138">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="0a50e-138">Add the following method to the **Program** class.</span></span> 

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

## <a name="create-a-method-to-create-the-custom-list"></a><span data-ttu-id="0a50e-139">Create a method to create the custom list</span><span class="sxs-lookup"><span data-stu-id="0a50e-139">Create a method to create the custom list</span></span>

<span data-ttu-id="0a50e-140">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="0a50e-140">Add the following method to the **Program** class.</span></span> 

    /// <summary>
    /// Creates the custom list.
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <returns>The response object from the operation.</returns>
    private static ImageList CreateCustomList(ContentModeratorClient client)
    {
        // Create the request body.
        listDetails = new Body("MyList", "A sample list",
            new BodyMetadata("Acceptable", "Potentially racy"));

        WriteLine($"Creating list {listDetails.Name}.", true);

        var result = client.ListManagementImageLists.Create(
            "application/json", listDetails);
        Thread.Sleep(throttleRate);

        WriteLine("Response:");
        WriteLine(JsonConvert.SerializeObject(result, Formatting.Indented));

        return result;
    }

## <a name="create-a-method-to-add-a-collection-of-images-to-the-list"></a><span data-ttu-id="0a50e-141">Create a method to add a collection of images to the list</span><span class="sxs-lookup"><span data-stu-id="0a50e-141">Create a method to add a collection of images to the list</span></span>

<span data-ttu-id="0a50e-142">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="0a50e-142">Add the following method to the **Program** class.</span></span>

<span data-ttu-id="0a50e-143">This quickstart does not demonstrate how to apply tags to images in the list.</span><span class="sxs-lookup"><span data-stu-id="0a50e-143">This quickstart does not demonstrate how to apply tags to images in the list.</span></span> 

    /// <summary>
    /// Adds images to an image list.
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="listId">The list identifier.</param>
    /// <param name="imagesToAdd">The images to add.</param>
    /// <param name="label">The label to apply to each image.</param>
    /// <remarks>Images are assigned content IDs when they are added to the list.
    /// Track the content ID assigned to each image.</remarks>
    private static void AddImages(
    ContentModeratorClient client, int listId,
    IEnumerable<string> imagesToAdd, string label)
    {
        foreach (var imageUrl in imagesToAdd)
        {
            WriteLine();
            WriteLine($"Adding {imageUrl} to list {listId} with label {label}.", true);
            try
            {
                var result = client.ListManagementImage.AddImageUrlInput(
                    listId.ToString(), "application/json", new BodyModel("URL", imageUrl), null, label);

                ImageIdMap.Add(imageUrl, Int32.Parse(result.ContentId));

                WriteLine("Response:");
                WriteLine(JsonConvert.SerializeObject(result, Formatting.Indented));
            }
            catch (Exception ex)
            {
                WriteLine($"Unable to add image to list. Caught {ex.GetType().FullName}: {ex.Message}", true);
            }
            finally
            {
                Thread.Sleep(throttleRate);
            }
        }
    }

## <a name="create-a-method-to-remove-images-from-the-list"></a><span data-ttu-id="0a50e-144">Create a method to remove images from the list</span><span class="sxs-lookup"><span data-stu-id="0a50e-144">Create a method to remove images from the list</span></span>

<span data-ttu-id="0a50e-145">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="0a50e-145">Add the following method to the **Program** class.</span></span> 

    /// <summary>
    /// Removes images from an image list.
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="listId">The list identifier.</param>
    /// <param name="imagesToRemove">The images to remove.</param>
    /// <remarks>Images are assigned content IDs when they are added to the list.
    /// Use the content ID to remove the image.</remarks>
    private static void RemoveImages(
        ContentModeratorClient client, int listId,
        IEnumerable<string> imagesToRemove)
    {
        foreach (var imageUrl in imagesToRemove)
        {
            if (!ImageIdMap.ContainsKey(imageUrl)) continue;
            int imageId = ImageIdMap[imageUrl];

            WriteLine();
            WriteLine($"Removing entry for {imageUrl} (ID = {imageId}) from list {listId}.", true);

            var result = client.ListManagementImage.DeleteImage(
                listId.ToString(), imageId.ToString());
            Thread.Sleep(throttleRate);

            ImageIdMap.Remove(imageUrl);

            WriteLine("Response:");
            WriteLine(JsonConvert.SerializeObject(result, Formatting.Indented));
        }
    }

## <a name="create-a-method-to-get-all-of-the-content-ids-for-images-in-the-list"></a><span data-ttu-id="0a50e-146">Create a method to get all of the content IDs for images in the list</span><span class="sxs-lookup"><span data-stu-id="0a50e-146">Create a method to get all of the content IDs for images in the list</span></span>

<span data-ttu-id="0a50e-147">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="0a50e-147">Add the following method to the **Program** class.</span></span> 

    /// <summary>
    /// Gets all image IDs in an image list.
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="listId">The list identifier.</param>
    /// <returns>The response object from the operation.</returns>
    private static ImageIds GetAllImageIds(
        ContentModeratorClient client, int listId)
    {
        WriteLine();
        WriteLine($"Getting all image IDs for list {listId}.", true);

        var result = client.ListManagementImage.GetAllImageIds(listId.ToString());
        Thread.Sleep(throttleRate);

        WriteLine("Response:");
        WriteLine(JsonConvert.SerializeObject(result, Formatting.Indented));

        return result;
    }

## <a name="create-a-method-to-update-the-details-of-the-list"></a><span data-ttu-id="0a50e-148">Create a method to update the details of the list</span><span class="sxs-lookup"><span data-stu-id="0a50e-148">Create a method to update the details of the list</span></span>

<span data-ttu-id="0a50e-149">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="0a50e-149">Add the following method to the **Program** class.</span></span> 

    /// <summary>
    /// Updates the details of an image list.
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="listId">The list identifier.</param>
    /// <returns>The response object from the operation.</returns>
    private static ImageList UpdateListDetails(
        ContentModeratorClient client, int listId)
    {
        WriteLine();
        WriteLine($"Updating details for list {listId}.", true);

        listDetails.Name = "Swimsuits and sports";

        var result = client.ListManagementImageLists.Update(
            listId.ToString(), "application/json", listDetails);
        Thread.Sleep(throttleRate);

        WriteLine("Response:");
        WriteLine(JsonConvert.SerializeObject(result, Formatting.Indented));

        return result;
    }

## <a name="create-a-method-to-retrieve-the-details-of-the-list"></a><span data-ttu-id="0a50e-150">Create a method to retrieve the details of the list</span><span class="sxs-lookup"><span data-stu-id="0a50e-150">Create a method to retrieve the details of the list</span></span>

<span data-ttu-id="0a50e-151">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="0a50e-151">Add the following method to the **Program** class.</span></span>

    /// <summary>
    /// Gets the details for an image list.
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="listId">The list identifier.</param>
    /// <returns>The response object from the operation.</returns>
    private static ImageList GetListDetails(
        ContentModeratorClient client, int listId)
    {
        WriteLine();
        WriteLine($"Getting details for list {listId}.", true);

        var result = client.ListManagementImageLists.GetDetails(listId.ToString());
        Thread.Sleep(throttleRate);

        WriteLine("Response:");
        WriteLine(JsonConvert.SerializeObject(result, Formatting.Indented));

        return result;
    }

## <a name="create-a-method-to-refresh-the-search-index-of-the-list"></a><span data-ttu-id="0a50e-152">Create a method to refresh the search index of the list</span><span class="sxs-lookup"><span data-stu-id="0a50e-152">Create a method to refresh the search index of the list</span></span>

<span data-ttu-id="0a50e-153">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="0a50e-153">Add the following method to the **Program** class.</span></span>

<span data-ttu-id="0a50e-154">Any time you update a list, you need to refresh the search index before using the list to screen images.</span><span class="sxs-lookup"><span data-stu-id="0a50e-154">Any time you update a list, you need to refresh the search index before using the list to screen images.</span></span>

    /// <summary>
    /// Refreshes the search index for an image list.
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="listId">The list identifier.</param>
    /// <returns>The response object from the operation.</returns>
    private static RefreshIndex RefreshSearchIndex(
        ContentModeratorClient client, int listId)
    {
        WriteLine();
        WriteLine($"Refreshing the search index for list {listId}.", true);

        var result = client.ListManagementImageLists.RefreshIndexMethod(listId.ToString());
        Thread.Sleep(throttleRate);

        WriteLine("Response:");
        WriteLine(JsonConvert.SerializeObject(result, Formatting.Indented));

        return result;
    }

## <a name="create-a-method-to-match-images-against-the-list"></a><span data-ttu-id="0a50e-155">Create a method to match images against the list</span><span class="sxs-lookup"><span data-stu-id="0a50e-155">Create a method to match images against the list</span></span>

<span data-ttu-id="0a50e-156">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="0a50e-156">Add the following method to the **Program** class.</span></span> 

    /// <summary>
    /// Matches images against an image list.
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="listId">The list identifier.</param>
    /// <param name="imagesToMatch">The images to screen.</param>
    private static void MatchImages(
        ContentModeratorClient client, int listId,
        IEnumerable<string> imagesToMatch)
    {
        foreach (var imageUrl in imagesToMatch)
        {
            WriteLine();
            WriteLine($"Matching image {imageUrl} against list {listId}.", true);

            var result = client.ImageModeration.MatchUrlInput(
                    "application/json", new BodyModel("URL", imageUrl), listId.ToString());
            Thread.Sleep(throttleRate);

            WriteLine("Response:");
            WriteLine(JsonConvert.SerializeObject(result, Formatting.Indented));
        }
    }

## <a name="create-a-method-to-delete-all-images-from-the-list"></a><span data-ttu-id="0a50e-157">Create a method to delete all images from the list</span><span class="sxs-lookup"><span data-stu-id="0a50e-157">Create a method to delete all images from the list</span></span>

<span data-ttu-id="0a50e-158">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="0a50e-158">Add the following method to the **Program** class.</span></span> 

    /// <summary>
    /// Deletes all images from an image list.
    /// </summary>
    /// <param name="client">The Content Modertor client.</param>
    /// <param name="listId">The list identifier.</param>
    private static void DeleteAllImages(
        ContentModeratorClient client, int listId)
    {
        WriteLine();
        WriteLine($"Deleting all images from list {listId}.", true);

        var result = client.ListManagementImage.DeleteAllImages(listId.ToString());
        Thread.Sleep(throttleRate);

        WriteLine("Response:");
        WriteLine(JsonConvert.SerializeObject(result, Formatting.Indented));
    }

## <a name="create-a-method-to-delete-the-list"></a><span data-ttu-id="0a50e-159">Create a method to delete the list</span><span class="sxs-lookup"><span data-stu-id="0a50e-159">Create a method to delete the list</span></span>

<span data-ttu-id="0a50e-160">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="0a50e-160">Add the following method to the **Program** class.</span></span> 

    /// <summary>
    /// Deletes an image list.
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <param name="listId">The list identifier.</param>
    private static void DeleteCustomList(
        ContentModeratorClient client, int listId)
    {
        WriteLine();
        WriteLine($"Deleting list {listId}.", true);

        var result = client.ListManagementImageLists.Delete(listId.ToString());
        Thread.Sleep(throttleRate);

        WriteLine("Response:");
        WriteLine(JsonConvert.SerializeObject(result, Formatting.Indented));
    }

## <a name="create-a-method-to-retrieve-ids-for-all-image-lists"></a><span data-ttu-id="0a50e-161">Create a method to retrieve IDs for all image lists</span><span class="sxs-lookup"><span data-stu-id="0a50e-161">Create a method to retrieve IDs for all image lists</span></span>

<span data-ttu-id="0a50e-162">Add the following method to the **Program** class.</span><span class="sxs-lookup"><span data-stu-id="0a50e-162">Add the following method to the **Program** class.</span></span> 

    /// <summary>
    /// Gets all list identifiers for the client.
    /// </summary>
    /// <param name="client">The Content Moderator client.</param>
    /// <returns>The response object from the operation.</returns>
    private static IList<ImageList> GetAllListIds(ContentModeratorClient client)
    {
        WriteLine();
        WriteLine($"Getting all image list IDs.", true);

        var result = client.ListManagementImageLists.GetAllImageLists();
        Thread.Sleep(throttleRate);

        WriteLine("Response:");
        WriteLine(JsonConvert.SerializeObject(result, Formatting.Indented));

        return result;
    }

## <a name="add-code-to-simulate-the-use-of-an-image-list"></a><span data-ttu-id="0a50e-163">Add code to simulate the use of an image list</span><span class="sxs-lookup"><span data-stu-id="0a50e-163">Add code to simulate the use of an image list</span></span>

<span data-ttu-id="0a50e-164">Add the following code to the **Main** method.</span><span class="sxs-lookup"><span data-stu-id="0a50e-164">Add the following code to the **Main** method.</span></span>

<span data-ttu-id="0a50e-165">This code simulates many of the operations that you would perform in defining and managing the list, as well as using the list to screen images.</span><span class="sxs-lookup"><span data-stu-id="0a50e-165">This code simulates many of the operations that you would perform in defining and managing the list, as well as using the list to screen images.</span></span> <span data-ttu-id="0a50e-166">The logging features allow you to see the response objects generated by the SDK calls to the Content Moderator service.</span><span class="sxs-lookup"><span data-stu-id="0a50e-166">The logging features allow you to see the response objects generated by the SDK calls to the Content Moderator service.</span></span>

    // Create the text writer to use for logging, and cache a static reference to it.
    using (StreamWriter outputWriter = new StreamWriter(OutputFile))
    {
        writer = outputWriter;

        // Create a Content Moderator client.
        using (var client = Clients.NewClient())
        {
            // Create a custom image list and record the ID assigned to it.
            var creationResult = CreateCustomList(client);
            if (creationResult.Id.HasValue)
            {
                // Cache the ID of the new image list.
                int listId = creationResult.Id.Value;

                // Perform various operations using the image list.
                AddImages(client, listId, Images.Sports.Urls, Images.Sports.Label);
                AddImages(client, listId, Images.Swimsuit.Urls, Images.Swimsuit.Label);
                        
                GetAllImageIds(client, listId);
                UpdateListDetails(client, listId);
                GetListDetails(client, listId);

                // Be sure to refresh search index
                RefreshSearchIndex(client, listId);

                // WriteLine();
                WriteLine($"Waiting {latencyDelay} minutes to allow the server time to propagate the index changes.", true);
                Thread.Sleep((int)(latencyDelay * 60 * 1000));

                // Match images against the image list.
                MatchImages(client, listId, ImagesToMatch);

                // Remove images
                RemoveImages(client, listId, Images.Corrections);

                // Be sure to refresh search index
                RefreshSearchIndex(client, listId);

                WriteLine();
                WriteLine($"Waiting {latencyDelay} minutes to allow the server time to propagate the index changes.", true);
                Thread.Sleep((int)(latencyDelay * 60 * 1000));

                // Match images again against the image list. The removed image should not get matched.
                MatchImages(client, listId, ImagesToMatch);

                // Delete all images from the list.
                DeleteAllImages(client, listId);

                // Delete the image list.
                DeleteCustomList(client, listId);

                // Verify that the list was deleted.
                GetAllListIds(client);
                }
            }

            writer.Flush();
            writer.Close();
            writer = null;
    }

    Console.WriteLine();
    Console.WriteLine("Press any key to exit...");
    Console.ReadKey();

## <a name="run-the-program-and-review-the-output"></a><span data-ttu-id="0a50e-167">Run the program and review the output</span><span class="sxs-lookup"><span data-stu-id="0a50e-167">Run the program and review the output</span></span>

<span data-ttu-id="0a50e-168">The list ID and the image content IDs are different each time you run the application.</span><span class="sxs-lookup"><span data-stu-id="0a50e-168">The list ID and the image content IDs are different each time you run the application.</span></span>
<span data-ttu-id="0a50e-169">The log file written by the program has the following output:</span><span class="sxs-lookup"><span data-stu-id="0a50e-169">The log file written by the program has the following output:</span></span>

    Creating list MyList.
    Response:
    {
        "Id": 169642,
        "Name": "MyList",
        "Description": "A sample list",
        "Metadata": {
            "Key One": "Acceptable",
            "Key Two": "Potentially racy"
        }
    }

    Adding https://moderatorsampleimages.blob.core.windows.net/samples/sample4.png to list 169642 with label Sports.
    Response:
    {
        "ContentId": "169490",
        "AdditionalInfo": [
        {
            "Key": "Source",
            "Value": "169642"
        },
        {
            "Key": "ImageDownloadTimeInMs",
            "Value": "233"
        },
        {
            "Key": "ImageSizeInBytes",
            "Value": "2945548"
        }
        ],
        "Status": {
            "Code": 3000,
            "Description": "OK",
            "Exception": null
            },
        "TrackingId": "WE_f0527c49616243c5ac65e1cc3482d390_ContentModerator.Preview_b4d3e20a-0751-4760-8829-475e5da33ce8"
    }

    Adding https://moderatorsampleimages.blob.core.windows.net/samples/sample6.png to list 169642 with label Sports.
    Response:
    {
        "ContentId": "169491",
        "AdditionalInfo": [
        {
            "Key": "Source",
            "Value": "169642"
        },
        {
            "Key": "ImageDownloadTimeInMs",
            "Value": "215"
        },
        {
            "Key": "ImageSizeInBytes",
            "Value": "2440050"
        }
        ],
        "Status": {
            "Code": 3000,
            "Description": "OK",
            "Exception": null
            },
        "TrackingId": "WE_f0527c49616243c5ac65e1cc3482d390_ContentModerator.Preview_cc1eb6af-2463-4e5e-9145-2a11dcecbc30"
    }

    Adding https://moderatorsampleimages.blob.core.windows.net/samples/sample9.png to list 169642 with label Sports.
    Response:
    {
        "ContentId": "169492",
        "AdditionalInfo": [
        {
            "Key": "Source",
            "Value": "169642"
        },
        {
            "Key": "ImageDownloadTimeInMs",
            "Value": "98"
        },
        {
            "Key": "ImageSizeInBytes",
            "Value": "1631958"
        }
        ],
        "Status": {
            "Code": 3000,
            "Description": "OK",
            "Exception": null
            },
        "TrackingId": "WE_f0527c49616243c5ac65e1cc3482d390_ContentModerator.Preview_01edc1f2-b448-48cf-b7f6-23b64d5040e9"
    }

    Adding https://moderatorsampleimages.blob.core.windows.net/samples/sample1.jpg to list 169642 with label Swimsuit.
    Response:
    {
        "ContentId": "169493",
        "AdditionalInfo": [
        {
            "Key": "Source",
            "Value": "169642"
        },
        {
            "Key": "ImageDownloadTimeInMs",
            "Value": "27"
        },
        {
            "Key": "ImageSizeInBytes",
            "Value": "17280"
        }
        ],
        "Status": {
            "Code": 3000,
            "Description": "OK",
            "Exception": null
            },
        "TrackingId": "WE_f0527c49616243c5ac65e1cc3482d390_ContentModerator.Preview_41f7bc6f-8778-4576-ba46-37b43a6c2434"
    }

    Adding https://moderatorsampleimages.blob.core.windows.net/samples/sample3.png to list 169642 with label Swimsuit.
    Response:
    {
        "ContentId": "169494",
        "AdditionalInfo": [
        {
            "Key": "Source",
            "Value": "169642"
        },
        {
            "Key": "ImageDownloadTimeInMs",
            "Value": "129"
        },
        {
            "Key": "ImageSizeInBytes",
            "Value": "1242855"
        }
        ],
        "Status": {
            "Code": 3000,
            "Description": "OK",
            "Exception": null
            },
        "TrackingId": "WE_f0527c49616243c5ac65e1cc3482d390_ContentModerator.Preview_61a48f33-eb55-4fd9-ac97-20eb0f3622a5"
    }

    Adding https://moderatorsampleimages.blob.core.windows.net/samples/sample4.png to list 169642 with label Swimsuit.
    Unable to add image to list. Caught Microsoft.CognitiveServices.ContentModerator.Models.APIErrorException: Operation returned an invalid status code 'Conflict'

    Adding https://moderatorsampleimages.blob.core.windows.net/samples/sample16.png to list 169642 with label Swimsuit.
    Response:
    {
        "ContentId": "169495",
        "AdditionalInfo": [
        {
            "Key": "Source",
            "Value": "169642"
        },
        {
            "Key": "ImageDownloadTimeInMs",
            "Value": "65"
        },
        {
            "Key": "ImageSizeInBytes",
            "Value": "1088127"
        }
        ],
        "Status": {
            "Code": 3000,
            "Description": "OK",
            "Exception": null
            },
        "TrackingId": "WE_f0527c49616243c5ac65e1cc3482d390_ContentModerator.Preview_1c1f3de4-58b9-4aa8-82fa-1b0f479f6d7c"
    }

    Getting all image IDs for list 169642.
    Response:
    {
        "ContentSource": "169642",
        "ContentIds": [
            169490,
            169491,
            169492,
            169493,
            169494,
            169495
    ],
    "Status": {
        "Code": 3000,
        "Description": "OK",
        "Exception": null
        },
    "TrackingId": "WE_f0527c49616243c5ac65e1cc3482d390_ContentModerator.Preview_0d017deb-38fa-4701-a7b1-5b6608c79da2"
    }

    Updating details for list 169642.
    Response:
    {
        "Id": 169642,
        "Name": "Swimsuits and sports",
        "Description": "A sample list",
        "Metadata": {
            "Key One": "Acceptable",
            "Key Two": "Potentially racy"
        }
    }

    Getting details for list 169642.
    Response:
    {
        "Id": 169642,
        "Name": "Swimsuits and sports",
        "Description": "A sample list",
        "Metadata": {
            "Key One": "Acceptable",
            "Key Two": "Potentially racy"
        }
    }

    Refreshing the search index for list 169642.
    Response:
    {
        "ContentSourceId": "169642",
        "IsUpdateSuccess": true,
        "AdvancedInfo": [],
        "Status": {
            "Code": 3000,
            "Description": "RefreshIndex successfully completed.",
            "Exception": null
            },
        "TrackingId": "WE_f0527c49616243c5ac65e1cc3482d390_ContentModerator.Preview_c72255cd-55a0-415e-9c18-0b9c08a9f25b"
    }
    Waiting 0.5 minutes to allow the server time to propagate the index changes.

    Matching image https://moderatorsampleimages.blob.core.windows.net/samples/sample1.jpg against list 169642.
    Response:
    {
        "TrackingId": "WE_f0527c49616243c5ac65e1cc3482d390_ContentModerator.Preview_ec384878-dbaa-4999-9042-6ac986355967",
        "CacheID": null,
        "IsMatch": true,
        "Matches": [
            {
                "Score": 1.0,
                "MatchId": 169493,
                "Source": "169642",
                "Tags": [],
                "Label": "Swimsuit"
            }
        ],
        "Status": {
            "Code": 3000,
            "Description": "OK",
            "Exception": null
        }
    }

    Matching image https://moderatorsampleimages.blob.core.windows.net/samples/sample4.png against list 169642.
    Response:
    {
        "TrackingId": "WE_f0527c49616243c5ac65e1cc3482d390_ContentModerator.Preview_e9db4b8f-3067-400f-9552-d3e6af2474c0",
        "CacheID": null,
        "IsMatch": true,
        "Matches": [
            {
                "Score": 1.0,
                "MatchId": 169490,
                "Source": "169642",
                "Tags": [],
                "Label": "Sports"
            }
        ],
        "Status": {
            "Code": 3000,
            "Description": "OK",
            "Exception": null
            }
    }

    Matching image https://moderatorsampleimages.blob.core.windows.net/samples/sample5.png against list 169642.
    Response:
    {
        "TrackingId": "WE_f0527c49616243c5ac65e1cc3482d390_ContentModerator.Preview_25991575-05da-4904-89db-abe88270b403",
        "CacheID": null,
        "IsMatch": false,
        "Matches": [],
        "Status": {
            "Code": 3000,
            "Description": "OK",
            "Exception": null
        }
    }

    Matching image https://moderatorsampleimages.blob.core.windows.net/samples/sample16.png against list 169642.
    Response:
    {
        "TrackingId": "WE_f0527c49616243c5ac65e1cc3482d390_ContentModerator.Preview_c65d1c91-0d8a-4511-8ac6-814e04adc845",
        "CacheID": null,
        "IsMatch": true,
        "Matches": [
            {
                "Score": 1.0,
                "MatchId": 169495,
                "Source": "169642",
                "Tags": [],
                "Label": "Swimsuit"
            }
            ],
        "Status": {
            "Code": 3000,
            "Description": "OK",
            "Exception": null
        }
    }

    Removing entry for https://moderatorsampleimages.blob.core.windows.net/samples/sample16.png (ID = 169495) from list 169642.
    Response:
    ""

    Refreshing the search index for list 169642.
    Response:
    {
        "ContentSourceId": "169642",
        "IsUpdateSuccess": true,
        "AdvancedInfo": [],
        "Status": {
            "Code": 3000,
            "Description": "RefreshIndex successfully completed.",
            "Exception": null
            },
        "TrackingId": "WE_f0527c49616243c5ac65e1cc3482d390_ContentModerator.Preview_b55a375e-30a1-4612-aa7b-81edcee5bffb"
    }

    Waiting 0.5 minutes to allow the server time to propagate the index changes.

    Matching image https://moderatorsampleimages.blob.core.windows.net/samples/sample1.jpg against list 169642.
    Response:
    {
        "TrackingId": "WE_f0527c49616243c5ac65e1cc3482d390_ContentModerator.Preview_00544948-2936-489c-98c8-b507b654bff5",
        "CacheID": null,
        "IsMatch": true,
        "Matches": [
            {
                "Score": 1.0,
                "MatchId": 169493,
                "Source": "169642",
                "Tags": [],
                "Label": "Swimsuit"
            }
            ],
        "Status": {
            "Code": 3000,
            "Description": "OK",
            "Exception": null
        }
    }

    Matching image https://moderatorsampleimages.blob.core.windows.net/samples/sample4.png against list 169642.
    Response:
    {
        "TrackingId": "WE_f0527c49616243c5ac65e1cc3482d390_ContentModerator.Preview_c36ec646-53c2-4705-86b2-d72b5c2273c7",
        "CacheID": null,
        "IsMatch": true,
        "Matches": [
            {
                "Score": 1.0,
                "MatchId": 169490,
                "Source": "169642",
                "Tags": [],
                "Label": "Sports"
            }
            ],
        "Status": {
            "Code": 3000,
            "Description": "OK",
            "Exception": null
        }
    }

    Matching image https://moderatorsampleimages.blob.core.windows.net/samples/sample5.png against list 169642.
    Response:
    {
        TrackingId": "WE_f0527c49616243c5ac65e1cc3482d390_ContentModerator.Preview_22edad74-690d-4fbc-b7d0-bf64867c4cb9",
        "CacheID": null,
        "IsMatch": false,
        "Matches": [],
        "Status": {
            "Code": 3000,
            "Description": "OK",
            "Exception": null
        }
    }

    Matching image https://moderatorsampleimages.blob.core.windows.net/samples/sample16.png against list 169642.
    Response:
    {
        "TrackingId": "WE_f0527c49616243c5ac65e1cc3482d390_ContentModerator.Preview_abd4a178-3238-4601-8e4f-cf9ee66f605a",
        "CacheID": null,
        "IsMatch": false,
        "Matches": [],
        "Status": {
            "Code": 3000,
            "Description": "OK",
            "Exception": null
        }
    }

    Deleting all images from list 169642.
    Response:
    "Reset Successful."

    Deleting list 169642.
    Response:
    ""

    Getting all image list IDs.
    Response:
    []


## <a name="next-steps"></a><span data-ttu-id="0a50e-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="0a50e-170">Next steps</span></span>

<span data-ttu-id="0a50e-171">Get the [Content Moderator .NET SDK](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) and the [Visual Studio solution](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator) for this and other Content Moderator quickstarts for .NET, and get started on your integration.</span><span class="sxs-lookup"><span data-stu-id="0a50e-171">Get the [Content Moderator .NET SDK](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.ContentModerator/) and the [Visual Studio solution](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator) for this and other Content Moderator quickstarts for .NET, and get started on your integration.</span></span>
