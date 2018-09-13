---
title: Azure Content Moderator - video moderation | Microsoft Docs
description: Use video moderation to scan for possible adult and racy content.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 02/02/2018
ms.author: sajagtap
ms.openlocfilehash: 27e189d93573dea139c2b67c237c376a28100c2b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44826787"
---
# <a name="video-moderation"></a><span data-ttu-id="8e5f9-103">Video moderation</span><span class="sxs-lookup"><span data-stu-id="8e5f9-103">Video moderation</span></span>

<span data-ttu-id="8e5f9-104">Today, online viewers generate billions of video views across popular and regional social media web sites and increasing.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-104">Today, online viewers generate billions of video views across popular and regional social media web sites and increasing.</span></span> <span data-ttu-id="8e5f9-105">By applying machine-learning based services to predict potential adult and racy content, you lower the cost of your moderation efforts.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-105">By applying machine-learning based services to predict potential adult and racy content, you lower the cost of your moderation efforts.</span></span>

## <a name="sign-up-for-the-content-moderator-media-processor-preview"></a><span data-ttu-id="8e5f9-106">Sign up for the Content Moderator media processor (preview)</span><span class="sxs-lookup"><span data-stu-id="8e5f9-106">Sign up for the Content Moderator media processor (preview)</span></span>

### <a name="create-a-free-azure-account"></a><span data-ttu-id="8e5f9-107">Create a free Azure account</span><span class="sxs-lookup"><span data-stu-id="8e5f9-107">Create a free Azure account</span></span>

<span data-ttu-id="8e5f9-108">[Start here](https://azure.microsoft.com/free/) to create a free Azure account if you don't have one already.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-108">[Start here](https://azure.microsoft.com/free/) to create a free Azure account if you don't have one already.</span></span>

### <a name="create-an-azure-media-services-account"></a><span data-ttu-id="8e5f9-109">Create an Azure Media Services account</span><span class="sxs-lookup"><span data-stu-id="8e5f9-109">Create an Azure Media Services account</span></span>

<span data-ttu-id="8e5f9-110">The Content Moderator's video capability is available as a public preview **media processor** in Azure Media Services (AMS) at no charge.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-110">The Content Moderator's video capability is available as a public preview **media processor** in Azure Media Services (AMS) at no charge.</span></span>

<span data-ttu-id="8e5f9-111">[Create an Azure Media Services account](https://docs.microsoft.com/azure/media-services/media-services-portal-create-account) in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-111">[Create an Azure Media Services account](https://docs.microsoft.com/azure/media-services/media-services-portal-create-account) in your Azure subscription.</span></span>

### <a name="get-azure-active-directory-credentials"></a><span data-ttu-id="8e5f9-112">Get Azure Active Directory credentials</span><span class="sxs-lookup"><span data-stu-id="8e5f9-112">Get Azure Active Directory credentials</span></span>

   1. <span data-ttu-id="8e5f9-113">Read the [Azure Media Services portal article](https://docs.microsoft.com/azure/media-services/media-services-portal-get-started-with-aad) to learn how to use the Azure portal to get your Azure AD authentication credentials.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-113">Read the [Azure Media Services portal article](https://docs.microsoft.com/azure/media-services/media-services-portal-get-started-with-aad) to learn how to use the Azure portal to get your Azure AD authentication credentials.</span></span>
   1. <span data-ttu-id="8e5f9-114">Read the [Azure Media Services .NET article](https://docs.microsoft.com/azure/media-services/media-services-dotnet-get-started-with-aad) to learn how to use your Azure Active Directory credentials with the .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-114">Read the [Azure Media Services .NET article](https://docs.microsoft.com/azure/media-services/media-services-dotnet-get-started-with-aad) to learn how to use your Azure Active Directory credentials with the .NET SDK.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8e5f9-115">The sample code in this quickstart uses the **service principal authentication** method described in both the articles.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-115">The sample code in this quickstart uses the **service principal authentication** method described in both the articles.</span></span>

<span data-ttu-id="8e5f9-116">Once you get your AMS credentials, there are two ways to try the Content Moderator media processor.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-116">Once you get your AMS credentials, there are two ways to try the Content Moderator media processor.</span></span>

## <a name="use-azure-media-services-explorer"></a><span data-ttu-id="8e5f9-117">Use Azure Media Services Explorer</span><span class="sxs-lookup"><span data-stu-id="8e5f9-117">Use Azure Media Services Explorer</span></span>

<span data-ttu-id="8e5f9-118">Use the interactive [Azure Media Services (AMS) explorer](https://azure.microsoft.com/blog/managing-media-workflows-with-the-new-azure-media-services-explorer-tool/) to browse your AMS account, upload videos, and scan with the Content Moderator media processor.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-118">Use the interactive [Azure Media Services (AMS) explorer](https://azure.microsoft.com/blog/managing-media-workflows-with-the-new-azure-media-services-explorer-tool/) to browse your AMS account, upload videos, and scan with the Content Moderator media processor.</span></span> <span data-ttu-id="8e5f9-119">[Download and install it](https://github.com/Azure/Azure-Media-Services-Explorer/releases) from GitHub, and [browse the source code](http://github.com/Azure/Azure-Media-Services-Explorer) to dive into using the AMS SDK.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-119">[Download and install it](https://github.com/Azure/Azure-Media-Services-Explorer/releases) from GitHub, and [browse the source code](http://github.com/Azure/Azure-Media-Services-Explorer) to dive into using the AMS SDK.</span></span>

![Azure Media Services explorer with Content Moderator](images/ams-explorer-content-moderator.PNG)

## <a name="net-quickstart-with-visual-studio-and-c"></a><span data-ttu-id="8e5f9-121">.NET QuickStart with Visual Studio and C#</span><span class="sxs-lookup"><span data-stu-id="8e5f9-121">.NET QuickStart with Visual Studio and C#</span></span>

1. <span data-ttu-id="8e5f9-122">Add a new **Console app (.NET Framework)** project to your solution.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-122">Add a new **Console app (.NET Framework)** project to your solution.</span></span>

   <span data-ttu-id="8e5f9-123">In the sample code, name the project **VideoModeration**.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-123">In the sample code, name the project **VideoModeration**.</span></span>

1. <span data-ttu-id="8e5f9-124">Select this project as the single startup project for the solution.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-124">Select this project as the single startup project for the solution.</span></span>

### <a name="install-required-packages"></a><span data-ttu-id="8e5f9-125">Install required packages</span><span class="sxs-lookup"><span data-stu-id="8e5f9-125">Install required packages</span></span>

<span data-ttu-id="8e5f9-126">Install the following NuGet packages available on [NuGet](https://www.nuget.org/).</span><span class="sxs-lookup"><span data-stu-id="8e5f9-126">Install the following NuGet packages available on [NuGet](https://www.nuget.org/).</span></span>

- <span data-ttu-id="8e5f9-127">windowsazure.mediaservices</span><span class="sxs-lookup"><span data-stu-id="8e5f9-127">windowsazure.mediaservices</span></span>
- <span data-ttu-id="8e5f9-128">windowsazure.mediaservices.extensions</span><span class="sxs-lookup"><span data-stu-id="8e5f9-128">windowsazure.mediaservices.extensions</span></span>

### <a name="update-the-programs-using-statements"></a><span data-ttu-id="8e5f9-129">Update the program's using statements</span><span class="sxs-lookup"><span data-stu-id="8e5f9-129">Update the program's using statements</span></span>

<span data-ttu-id="8e5f9-130">Modify the program's using statements.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-130">Modify the program's using statements.</span></span>

    using System;
    using System.Linq;
    using System.Threading.Tasks;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.IO;
    using System.Threading;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using System.Collections.Generic;


### <a name="initialize-application-specific-settings"></a><span data-ttu-id="8e5f9-131">Initialize application-specific settings</span><span class="sxs-lookup"><span data-stu-id="8e5f9-131">Initialize application-specific settings</span></span>

<span data-ttu-id="8e5f9-132">Add the following static fields to the **Program** class in Program.cs.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-132">Add the following static fields to the **Program** class in Program.cs.</span></span>

    // declare constants and globals
    private static CloudMediaContext _context = null;
    private static CloudStorageAccount _StorageAccount = null;

    // Azure Media Services (AMS) associated Storage Account, Key, and the Container that has 
    // a list of Blobs to be processed.
    static string STORAGE_NAME = "YOUR AMS ASSOCIATED BLOB STORAGE NAME";
    static string STORAGE_KEY = "YOUR AMS ASSOCIATED BLOB STORAGE KEY";
    static string STORAGE_CONTAINER_NAME = "YOUR BLOB CONTAINER FOR VIDEO FILES";

    private static StorageCredentials _StorageCredentials = null;

    // Azure Media Services authentication. See the quickstart for how to get these.
    private const string AZURE_AD_TENANT_NAME = "microsoft.onmicrosoft.com";
    private const string CLIENT_ID = "YOUR CLIENT ID"
    private const string CLIENT_SECRET = "YOUR CLIENT SECRET";

    // REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".      
    private const string REST_API_ENDPOINT = "YOUR API ENDPOINT";

    // Content Moderator Media Processor Nam
    private const string MEDIA_PROCESSOR = "Azure Media Content Moderator";

    // Input and Output files in the current directory of the executable
    private const string INPUT_FILE = "VIDEO FILE NAME";
    private const string OUTPUT_FOLDER = "";

### <a name="create-a-preset-file-json"></a><span data-ttu-id="8e5f9-133">Create a preset file (json)</span><span class="sxs-lookup"><span data-stu-id="8e5f9-133">Create a preset file (json)</span></span>

<span data-ttu-id="8e5f9-134">Create a JSON file in the current directory with the version number.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-134">Create a JSON file in the current directory with the version number.</span></span>

    private static readonly string CONTENT_MODERATOR_PRESET_FILE = "preset.json";
    //Example file content:
    //        {
    //             "version": "2.0"
    //        }
    private static readonly string CONTENT_MODERATOR_PRESET_FILE = "preset.json";

### <a name="add-the-following-code-to-the-main-method"></a><span data-ttu-id="8e5f9-135">Add the following code to the main method</span><span class="sxs-lookup"><span data-stu-id="8e5f9-135">Add the following code to the main method</span></span>

<span data-ttu-id="8e5f9-136">The main method first creates an Azure Media Context and then an Azure Storage Context in case your videos are in blob storage.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-136">The main method first creates an Azure Media Context and then an Azure Storage Context in case your videos are in blob storage.</span></span>
<span data-ttu-id="8e5f9-137">The remaining code scans a video from a local folder, blob, or multiple blobs within an Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-137">The remaining code scans a video from a local folder, blob, or multiple blobs within an Azure storage container.</span></span>
<span data-ttu-id="8e5f9-138">You can try all options by commenting out the other lines of code.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-138">You can try all options by commenting out the other lines of code.</span></span>

    // Create Azure Media Context
    CreateMediaContext();

    // Create Storage Context
    CreateStorageContext();

    // Use a file as the input.
    // IAsset asset = CreateAssetfromFile();
    
    // -- OR ---
    
    // Or a blob as the input
    // IAsset asset = CreateAssetfromBlob((CloudBlockBlob)GetBlobsList().First());

    // Then submit the asset to Content Moderator
    // RunContentModeratorJob(asset);

    //-- OR ----

    // Just run the content moderator on all blobs in a list (from a Blob Container)
    RunContentModeratorJobOnBlobs();

### <a name="add-the-code-to-create-an-azure-media-context"></a><span data-ttu-id="8e5f9-139">Add the code to create an Azure Media Context</span><span class="sxs-lookup"><span data-stu-id="8e5f9-139">Add the code to create an Azure Media Context</span></span>

    /// <summary>
    /// Creates a media context from azure credentials
    /// </summary>
    static void CreateMediaContext()
    {
        // Get Azure AD credentials
        var tokenCredentials = new AzureAdTokenCredentials(AZURE_AD_TENANT_NAME,
            new AzureAdClientSymmetricKey(CLIENT_ID, CLIENT_SECRET),
            AzureEnvironments.AzureCloudEnvironment);

        // Initialize an Azure AD token
        var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

        // Create a media context
        _context = new CloudMediaContext(new Uri(REST_API_ENDPOINT), tokenProvider);
    }

### <a name="add-the-code-to-create-an-azure-storage-context"></a><span data-ttu-id="8e5f9-140">Add the code to create an Azure Storage Context</span><span class="sxs-lookup"><span data-stu-id="8e5f9-140">Add the code to create an Azure Storage Context</span></span>
<span data-ttu-id="8e5f9-141">You use the Storage Context, created from your Storage credentials, to access your blob storage.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-141">You use the Storage Context, created from your Storage credentials, to access your blob storage.</span></span>

    /// <summary>
    /// Creates a storage context from the AMS associated storage name and key
    /// </summary>
    static void CreateStorageContext()
    {
        // Get a reference to the storage account associated with a Media Services account. 
        if (_StorageCredentials == null)
        {
            _StorageCredentials = new StorageCredentials(STORAGE_NAME, STORAGE_KEY);
        }
        _StorageAccount = new CloudStorageAccount(_StorageCredentials, false);
    }

### <a name="add-the-code-to-create-azure-media-assets-from-local-file-and-blob"></a><span data-ttu-id="8e5f9-142">Add the code to create Azure Media Assets from local file and blob</span><span class="sxs-lookup"><span data-stu-id="8e5f9-142">Add the code to create Azure Media Assets from local file and blob</span></span>
<span data-ttu-id="8e5f9-143">The Content Moderator media processor runs jobs on **Assets** within the Azure Media Services platform.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-143">The Content Moderator media processor runs jobs on **Assets** within the Azure Media Services platform.</span></span>
<span data-ttu-id="8e5f9-144">These methods create the Assets from a local file or an associated blob.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-144">These methods create the Assets from a local file or an associated blob.</span></span>

    /// <summary>
    /// Creates an Azure Media Services Asset from the video file
    /// </summary>
    /// <returns>Asset</returns>
    static IAsset CreateAssetfromFile()
    {
        return _context.Assets.CreateFromFile(INPUT_FILE, AssetCreationOptions.None); ;
    }

    /// <summary>
    /// Creates an Azure Media Services asset from your blog storage
    /// </summary>
    /// <param name="Blob"></param>
    /// <returns>Asset</returns>
    static IAsset CreateAssetfromBlob(CloudBlockBlob Blob)
    {
        // Create asset from the FIRST blob in the list and return it
        return _context.Assets.CreateFromBlob(Blob, _StorageCredentials, AssetCreationOptions.None);
    }

### <a name="add-the-code-to-scan-a-collection-of-videos-as-blobs-within-a-container"></a><span data-ttu-id="8e5f9-145">Add the code to scan a collection of videos (as blobs) within a container</span><span class="sxs-lookup"><span data-stu-id="8e5f9-145">Add the code to scan a collection of videos (as blobs) within a container</span></span>

    /// <summary>
    /// Runs the Content Moderator Job on all Blobs in a given container name
    /// </summary>
    static void RunContentModeratorJobOnBlobs()
    {
        // Get the reference to the list of Blobs. See the following method.
        var blobList = GetBlobsList();

        // Iterate over the Blob list items or work on specific ones as needed
        foreach (var sourceBlob in blobList)
        {
            // Create an Asset
            IAsset asset = _context.Assets.CreateFromBlob((CloudBlockBlob)sourceBlob,
                               _StorageCredentials, AssetCreationOptions.None);
            asset.Update();

            // Submit to Content Moderator
            RunContentModeratorJob(asset);
        }
    }

    /// <summary>
    /// Get all blobs in your container
    /// </summary>
    /// <returns></returns>
    static IEnumerable<IListBlobItem> GetBlobsList()
    {
        // Get a reference to the Container within the Storage Account
        // that has the files (blobs) for moderation
        CloudBlobClient CloudBlobClient = _StorageAccount.CreateCloudBlobClient();
        CloudBlobContainer MediaBlobContainer = CloudBlobClient.GetContainerReference(STORAGE_CONTAINER_NAME);

        // Get the reference to the list of Blobs 
        var blobList = MediaBlobContainer.ListBlobs();
        return blobList;
    }

### <a name="add-the-method-to-run-the-content-moderator-job"></a><span data-ttu-id="8e5f9-146">Add the method to run the Content Moderator Job</span><span class="sxs-lookup"><span data-stu-id="8e5f9-146">Add the method to run the Content Moderator Job</span></span>

    /// <summary>
    /// Run the Content Moderator job on the designated Asset from local file or blob storage
    /// </summary>
    /// <param name="asset"></param>
    static void RunContentModeratorJob(IAsset asset)
    {
        // Grab the presets
        string configuration = File.ReadAllText(CONTENT_MODERATOR_PRESET_FILE);

        // grab instance of Azure Media Content Moderator MP
        IMediaProcessor mp = _context.MediaProcessors.GetLatestMediaProcessorByName(MEDIA_PROCESSOR);

        // create Job with Content Moderator task
        IJob job = _context.Jobs.Create(String.Format("Content Moderator {0}",
                asset.AssetFiles.First() + "_" + Guid.NewGuid()));

        ITask contentModeratorTask = job.Tasks.AddNew("Adult and racy classifier task",
                mp, configuration,
                TaskOptions.None);
        contentModeratorTask.InputAssets.Add(asset);
        contentModeratorTask.OutputAssets.AddNew("Adult and racy classifier output",
            AssetCreationOptions.None);

        job.Submit();


        // Create progress printing and querying tasks
        Task progressPrintTask = new Task(() =>
        {
            IJob jobQuery = null;
            do
            {
                var progressContext = _context;
                jobQuery = progressContext.Jobs
                .Where(j => j.Id == job.Id)
                    .First();
                    Console.WriteLine(string.Format("{0}\t{1}",
                    DateTime.Now,
                    jobQuery.State));
                    Thread.Sleep(10000);
             }
             while (jobQuery.State != JobState.Finished &&
             jobQuery.State != JobState.Error &&
             jobQuery.State != JobState.Canceled);
        });
        progressPrintTask.Start();

        Task progressJobTask = job.GetExecutionProgressTask(
        CancellationToken.None);
        progressJobTask.Wait();

        // If job state is Error, the event handling 
        // method for job progress should log errors.  Here we check 
        // for error state and exit if needed.
        if (job.State == JobState.Error)
        {
            ErrorDetail error = job.Tasks.First().ErrorDetails.First();
            Console.WriteLine(string.Format("Error: {0}. {1}",
            error.Code,
            error.Message));
        }

        DownloadAsset(job.OutputMediaAssets.First(), OUTPUT_FOLDER);
    }

### <a name="add-a-couple-of-helper-functions"></a><span data-ttu-id="8e5f9-147">Add a couple of helper functions</span><span class="sxs-lookup"><span data-stu-id="8e5f9-147">Add a couple of helper functions</span></span>

<span data-ttu-id="8e5f9-148">These methods download the Content Moderator output file (JSON) from the Azure Media Services asset, and help track the status of the moderation job so that the program can log a running status to the console.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-148">These methods download the Content Moderator output file (JSON) from the Azure Media Services asset, and help track the status of the moderation job so that the program can log a running status to the console.</span></span>

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }

    // event handler for Job State
    static void StateChanged(object sender, JobStateChangedEventArgs e)
    {
        Console.WriteLine("Job state changed event:");
        Console.WriteLine("  Previous state: " + e.PreviousState);
        Console.WriteLine("  Current state: " + e.CurrentState);
        switch (e.CurrentState)
        {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("Job finished.");
                break;
            case JobState.Canceling:
            case JobState.Queued:
            case JobState.Scheduled:
            case JobState.Processing:
                Console.WriteLine("Please wait...\n");
                break;
            case JobState.Canceled:
                Console.WriteLine("Job is canceled.\n");
                break;
            case JobState.Error:
                Console.WriteLine("Job failed.\n");
                break;
            default:
                break;
        }
    }

### <a name="run-the-program-and-review-the-output"></a><span data-ttu-id="8e5f9-149">Run the program and review the output</span><span class="sxs-lookup"><span data-stu-id="8e5f9-149">Run the program and review the output</span></span>

<span data-ttu-id="8e5f9-150">After the Content Moderation job is completed, analyze the JSON response.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-150">After the Content Moderation job is completed, analyze the JSON response.</span></span> <span data-ttu-id="8e5f9-151">It consists of these elements:</span><span class="sxs-lookup"><span data-stu-id="8e5f9-151">It consists of these elements:</span></span>

- <span data-ttu-id="8e5f9-152">Video information summary</span><span class="sxs-lookup"><span data-stu-id="8e5f9-152">Video information summary</span></span>
- <span data-ttu-id="8e5f9-153">**Shots** as "**fragments**"</span><span class="sxs-lookup"><span data-stu-id="8e5f9-153">**Shots** as "**fragments**"</span></span>
- <span data-ttu-id="8e5f9-154">**Key frames** as "**events**" with a **reviewRecommended" (= true or false)"** flag based on **Adult** and **Racy** scores</span><span class="sxs-lookup"><span data-stu-id="8e5f9-154">**Key frames** as "**events**" with a **reviewRecommended" (= true or false)"** flag based on **Adult** and **Racy** scores</span></span>
- <span data-ttu-id="8e5f9-155">**start**, **duration**, **totalDuration**, and **timestamp** are in "ticks".</span><span class="sxs-lookup"><span data-stu-id="8e5f9-155">**start**, **duration**, **totalDuration**, and **timestamp** are in "ticks".</span></span> <span data-ttu-id="8e5f9-156">Divide by **timescale** to get the number in seconds.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-156">Divide by **timescale** to get the number in seconds.</span></span>
 
> [!NOTE]

> - <span data-ttu-id="8e5f9-157">`adultScore` represents the potential presence and prediction score of content that may be considered sexually explicit or adult in certain situations.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-157">`adultScore` represents the potential presence and prediction score of content that may be considered sexually explicit or adult in certain situations.</span></span>
> - <span data-ttu-id="8e5f9-158">`racyScore` represents the potential presence and prediction score of content that may be considered sexually suggestive or mature in certain situations.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-158">`racyScore` represents the potential presence and prediction score of content that may be considered sexually suggestive or mature in certain situations.</span></span>
> - <span data-ttu-id="8e5f9-159">`adultScore` and `racyScore` are between 0 and 1.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-159">`adultScore` and `racyScore` are between 0 and 1.</span></span> <span data-ttu-id="8e5f9-160">The higher the score, the higher the model is predicting that the category may be applicable.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-160">The higher the score, the higher the model is predicting that the category may be applicable.</span></span> <span data-ttu-id="8e5f9-161">This preview relies on a statistical model rather than manually coded outcomes.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-161">This preview relies on a statistical model rather than manually coded outcomes.</span></span> <span data-ttu-id="8e5f9-162">We recommend testing with your own content to determine how each category aligns to your requirements.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-162">We recommend testing with your own content to determine how each category aligns to your requirements.</span></span>
> - <span data-ttu-id="8e5f9-163">`reviewRecommended` is either true or false depending on the internal score thresholds.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-163">`reviewRecommended` is either true or false depending on the internal score thresholds.</span></span> <span data-ttu-id="8e5f9-164">Customers should assess whether to use this value or decide on custom thresholds based on their content policies.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-164">Customers should assess whether to use this value or decide on custom thresholds based on their content policies.</span></span>
>

    {
    "version": 2,
    "timescale": 90000,
    "offset": 0,
    "framerate": 50,
    "width": 1280,
    "height": 720,
    "totalDuration": 18696321,
    "fragments": [
    {
      "start": 0,
      "duration": 18000
    },
    {
      "start": 18000,
      "duration": 3600,
      "interval": 3600,
      "events": [
        [
          {
            "reviewRecommended": false,
            "adultScore": 0.00001,
            "racyScore": 0.03077,
            "index": 5,
            "timestamp": 18000,
            "shotIndex": 0
          }
        ]
      ]
    },
    {
      "start": 18386372,
      "duration": 119149,
      "interval": 119149,
      "events": [
        [
          {
            "reviewRecommended": true,
            "adultScore": 0.00000,
            "racyScore": 0.91902,
            "index": 5085,
            "timestamp": 18386372,
            "shotIndex": 62
          }
        ]
      ]
    }
    ]
    }

## <a name="next-steps"></a><span data-ttu-id="8e5f9-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="8e5f9-165">Next steps</span></span>

<span data-ttu-id="8e5f9-166">Learn how to generate [video reviews](video-reviews-quickstart-dotnet.md) from your moderation output.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-166">Learn how to generate [video reviews](video-reviews-quickstart-dotnet.md) from your moderation output.</span></span>

<span data-ttu-id="8e5f9-167">Add [transcript moderation](video-transcript-moderation-review-tutorial-dotnet.md) to your video reviews.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-167">Add [transcript moderation](video-transcript-moderation-review-tutorial-dotnet.md) to your video reviews.</span></span>

<span data-ttu-id="8e5f9-168">Check out the detailed tutorial on how to build a [complete video and transcript moderation solution](video-transcript-moderation-review-tutorial-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="8e5f9-168">Check out the detailed tutorial on how to build a [complete video and transcript moderation solution](video-transcript-moderation-review-tutorial-dotnet.md).</span></span>

<span data-ttu-id="8e5f9-169">[Download the Visual Studio solution](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator) for this and other Content Moderator quickstarts for .NET.</span><span class="sxs-lookup"><span data-stu-id="8e5f9-169">[Download the Visual Studio solution](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator) for this and other Content Moderator quickstarts for .NET.</span></span>
