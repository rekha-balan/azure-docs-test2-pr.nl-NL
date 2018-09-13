---
title: Azure Content Moderator - Moderate videos and transcripts in .NET | Microsoft Docs
description: How to use Content Moderator to moderate videos and transcripts in .NET.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 1/27/2018
ms.author: sajagtap
ms.openlocfilehash: 0f851c030a05880d79a998ed4b4a941082c057b9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969515"
---
# <a name="video-and-transcript-moderation-tutorial"></a><span data-ttu-id="8e517-103">Video and transcript moderation tutorial</span><span class="sxs-lookup"><span data-stu-id="8e517-103">Video and transcript moderation tutorial</span></span>

<span data-ttu-id="8e517-104">Content Moderator's video APIs allow you to moderate videos and create video reviews in the human review tool.</span><span class="sxs-lookup"><span data-stu-id="8e517-104">Content Moderator's video APIs allow you to moderate videos and create video reviews in the human review tool.</span></span> 

<span data-ttu-id="8e517-105">This detailed tutorial helps to understand how to build a complete video and transcript moderation solution with machine-assisted moderation and human-in-the-loop review creation.</span><span class="sxs-lookup"><span data-stu-id="8e517-105">This detailed tutorial helps to understand how to build a complete video and transcript moderation solution with machine-assisted moderation and human-in-the-loop review creation.</span></span>

<span data-ttu-id="8e517-106">Download the [C# console application](https://github.com/MicrosoftContentModerator/VideoReviewConsoleApp) for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="8e517-106">Download the [C# console application](https://github.com/MicrosoftContentModerator/VideoReviewConsoleApp) for this tutorial.</span></span> <span data-ttu-id="8e517-107">The console application uses the SDK and related packages to perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="8e517-107">The console application uses the SDK and related packages to perform the following tasks:</span></span>

- <span data-ttu-id="8e517-108">Compress the input video(s) for faster processing</span><span class="sxs-lookup"><span data-stu-id="8e517-108">Compress the input video(s) for faster processing</span></span>
- <span data-ttu-id="8e517-109">Moderate the video to get shots and frames with insights</span><span class="sxs-lookup"><span data-stu-id="8e517-109">Moderate the video to get shots and frames with insights</span></span>
- <span data-ttu-id="8e517-110">Use the frame timestamps to create thumbnails (images)</span><span class="sxs-lookup"><span data-stu-id="8e517-110">Use the frame timestamps to create thumbnails (images)</span></span>
- <span data-ttu-id="8e517-111">Submit timestamps and thumbnails to create video reviews</span><span class="sxs-lookup"><span data-stu-id="8e517-111">Submit timestamps and thumbnails to create video reviews</span></span>
- <span data-ttu-id="8e517-112">Convert the video speech to text (transcript) with the Media Indexer API</span><span class="sxs-lookup"><span data-stu-id="8e517-112">Convert the video speech to text (transcript) with the Media Indexer API</span></span>
- <span data-ttu-id="8e517-113">Moderate the transcript with the text moderation service</span><span class="sxs-lookup"><span data-stu-id="8e517-113">Moderate the transcript with the text moderation service</span></span>
- <span data-ttu-id="8e517-114">Add the moderated transcript to the video review</span><span class="sxs-lookup"><span data-stu-id="8e517-114">Add the moderated transcript to the video review</span></span>

## <a name="sample-program-outputs"></a><span data-ttu-id="8e517-115">Sample program outputs</span><span class="sxs-lookup"><span data-stu-id="8e517-115">Sample program outputs</span></span>

<span data-ttu-id="8e517-116">Before going further, let's look at the follwing sample outputs from the program:</span><span class="sxs-lookup"><span data-stu-id="8e517-116">Before going further, let's look at the follwing sample outputs from the program:</span></span>

- [<span data-ttu-id="8e517-117">Console output</span><span class="sxs-lookup"><span data-stu-id="8e517-117">Console output</span></span>](#program-output)
- [<span data-ttu-id="8e517-118">Video review</span><span class="sxs-lookup"><span data-stu-id="8e517-118">Video review</span></span>](#video-review-default-view)
- [<span data-ttu-id="8e517-119">Transcript view</span><span class="sxs-lookup"><span data-stu-id="8e517-119">Transcript view</span></span>](#video-review-transcript-view)

## <a name="prerequisites"></a><span data-ttu-id="8e517-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8e517-120">Prerequisites</span></span>

1. <span data-ttu-id="8e517-121">Sign up for the [Content Moderator review tool](https://contentmoderator.cognitive.microsoft.com/) web site and [create custom tags](Review-Tool-User-Guide/tags.md) that the C# console application assigns from within the code.</span><span class="sxs-lookup"><span data-stu-id="8e517-121">Sign up for the [Content Moderator review tool](https://contentmoderator.cognitive.microsoft.com/) web site and [create custom tags](Review-Tool-User-Guide/tags.md) that the C# console application assigns from within the code.</span></span> <span data-ttu-id="8e517-122">The following screen shows the custom tags.</span><span class="sxs-lookup"><span data-stu-id="8e517-122">The following screen shows the custom tags.</span></span>

  ![Video moderation custom tags](images/video-tutorial-custom-tags.png)

1. <span data-ttu-id="8e517-124">To run the sample application, you need an Azure account and an Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="8e517-124">To run the sample application, you need an Azure account and an Azure Media Services account.</span></span> <span data-ttu-id="8e517-125">Additionally, you need access to the Content Moderator private preview.</span><span class="sxs-lookup"><span data-stu-id="8e517-125">Additionally, you need access to the Content Moderator private preview.</span></span> <span data-ttu-id="8e517-126">Finally, you need Azure Active Directory authentication credentials.</span><span class="sxs-lookup"><span data-stu-id="8e517-126">Finally, you need Azure Active Directory authentication credentials.</span></span> <span data-ttu-id="8e517-127">For details on obtaining this information, see [the Video Moderation API quickstart](video-moderation-api.md).</span><span class="sxs-lookup"><span data-stu-id="8e517-127">For details on obtaining this information, see [the Video Moderation API quickstart](video-moderation-api.md).</span></span>

1. <span data-ttu-id="8e517-128">Edit the file `App.config` and add the Active Directory tenant name, service endpoints, and subscription keys indicated by `#####`.</span><span class="sxs-lookup"><span data-stu-id="8e517-128">Edit the file `App.config` and add the Active Directory tenant name, service endpoints, and subscription keys indicated by `#####`.</span></span> <span data-ttu-id="8e517-129">You need the following information:</span><span class="sxs-lookup"><span data-stu-id="8e517-129">You need the following information:</span></span>

|<span data-ttu-id="8e517-130">Key</span><span class="sxs-lookup"><span data-stu-id="8e517-130">Key</span></span>|<span data-ttu-id="8e517-131">Description</span><span class="sxs-lookup"><span data-stu-id="8e517-131">Description</span></span>|
|-|-|
|`AzureMediaServiceRestApiEndpoint`|<span data-ttu-id="8e517-132">Endpoint for the Azure Media Services (AMS) API</span><span class="sxs-lookup"><span data-stu-id="8e517-132">Endpoint for the Azure Media Services (AMS) API</span></span>|
|`ClientSecret`|<span data-ttu-id="8e517-133">Subscription key for Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="8e517-133">Subscription key for Azure Media Services</span></span>|
|`ClientId`|<span data-ttu-id="8e517-134">Client ID for Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="8e517-134">Client ID for Azure Media Services</span></span>|
|`AzureAdTenantName`|<span data-ttu-id="8e517-135">Active Directory tenant name representing your organization</span><span class="sxs-lookup"><span data-stu-id="8e517-135">Active Directory tenant name representing your organization</span></span>|
|`ContentModeratorReviewApiSubscriptionKey`|<span data-ttu-id="8e517-136">Subscription key for the Content Moderator review API</span><span class="sxs-lookup"><span data-stu-id="8e517-136">Subscription key for the Content Moderator review API</span></span>|
|`ContentModeratorApiEndpoint`|<span data-ttu-id="8e517-137">Endpoint for the Content Moderator API</span><span class="sxs-lookup"><span data-stu-id="8e517-137">Endpoint for the Content Moderator API</span></span>|
|`ContentModeratorTeamId`|<span data-ttu-id="8e517-138">Content moderator team ID</span><span class="sxs-lookup"><span data-stu-id="8e517-138">Content moderator team ID</span></span>|

## <a name="getting-started"></a><span data-ttu-id="8e517-139">Getting started</span><span class="sxs-lookup"><span data-stu-id="8e517-139">Getting started</span></span>

<span data-ttu-id="8e517-140">The class `Program` in `Program.cs` is the main entry point to the video moderation application.</span><span class="sxs-lookup"><span data-stu-id="8e517-140">The class `Program` in `Program.cs` is the main entry point to the video moderation application.</span></span>

### <a name="methods-of-class-program"></a><span data-ttu-id="8e517-141">Methods of class Program</span><span class="sxs-lookup"><span data-stu-id="8e517-141">Methods of class Program</span></span>

|<span data-ttu-id="8e517-142">Method</span><span class="sxs-lookup"><span data-stu-id="8e517-142">Method</span></span>|<span data-ttu-id="8e517-143">Description</span><span class="sxs-lookup"><span data-stu-id="8e517-143">Description</span></span>|
|-|-|
|`Main`|<span data-ttu-id="8e517-144">Parses command line, gathers user input, and starts processing.</span><span class="sxs-lookup"><span data-stu-id="8e517-144">Parses command line, gathers user input, and starts processing.</span></span>|
|`ProcessVideo`|<span data-ttu-id="8e517-145">Compresses, uploads, moderates, and creates video reviews.</span><span class="sxs-lookup"><span data-stu-id="8e517-145">Compresses, uploads, moderates, and creates video reviews.</span></span>|
|`CreateVideoStreamingRequest`|<span data-ttu-id="8e517-146">Creates a stream to upload a video</span><span class="sxs-lookup"><span data-stu-id="8e517-146">Creates a stream to upload a video</span></span>|
|`GetUserInputs`|<span data-ttu-id="8e517-147">Gathers user input; used when no command-line options are present</span><span class="sxs-lookup"><span data-stu-id="8e517-147">Gathers user input; used when no command-line options are present</span></span>|
|`Initialize`|<span data-ttu-id="8e517-148">Initializes objects needed for the moderation process</span><span class="sxs-lookup"><span data-stu-id="8e517-148">Initializes objects needed for the moderation process</span></span>|

### <a name="the-main-method"></a><span data-ttu-id="8e517-149">The Main method</span><span class="sxs-lookup"><span data-stu-id="8e517-149">The Main method</span></span>

<span data-ttu-id="8e517-150">`Main()` is where execution starts, so it's the place to start understanding the video moderation process.</span><span class="sxs-lookup"><span data-stu-id="8e517-150">`Main()` is where execution starts, so it's the place to start understanding the video moderation process.</span></span>

    static void Main(string[] args)
    {
        if (args.Length == 0)
        {
            string videoPath = string.Empty;
            GetUserInputs(out videoPath);
            Initialize();
            AmsConfigurations.logFilePath = Path.Combine(Path.GetDirectoryName(videoPath), "log.txt");
            try
            {
                ProcessVideo(videoPath).Wait();
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.Message);
            }
        }
        else
        {
            DirectoryInfo directoryInfo = new DirectoryInfo(args[0]);
            if (args.Length == 2)
                bool.TryParse(args[1], out generateVtt);
            Initialize();
            AmsConfigurations.logFilePath = Path.Combine(args[0], "log.txt");
            var files = directoryInfo.GetFiles("*.mp4", SearchOption.AllDirectories);
            foreach (var file in files)
            {
                try
                {
                    ProcessVideo(file.FullName).Wait();
                }
                catch (Exception ex)
                {
                    Console.WriteLine(ex.Message);
                }
            }
        }
    }

<span data-ttu-id="8e517-151">`Main()` handles the following command-line arguments:</span><span class="sxs-lookup"><span data-stu-id="8e517-151">`Main()` handles the following command-line arguments:</span></span>

- <span data-ttu-id="8e517-152">The path to a directory containing MPEG-4 video files to be submitted for moderation.</span><span class="sxs-lookup"><span data-stu-id="8e517-152">The path to a directory containing MPEG-4 video files to be submitted for moderation.</span></span> <span data-ttu-id="8e517-153">All `*.mp4` files in this directory and its subdirectories are submitted for moderation.</span><span class="sxs-lookup"><span data-stu-id="8e517-153">All `*.mp4` files in this directory and its subdirectories are submitted for moderation.</span></span>
- <span data-ttu-id="8e517-154">Optionally, a Boolean (true/false) flag indicating whether text transcripts should be generated for the purpose of moderating audio.</span><span class="sxs-lookup"><span data-stu-id="8e517-154">Optionally, a Boolean (true/false) flag indicating whether text transcripts should be generated for the purpose of moderating audio.</span></span>

<span data-ttu-id="8e517-155">If no command-line arguments are present, `Main()` calls `GetUserInputs()`.</span><span class="sxs-lookup"><span data-stu-id="8e517-155">If no command-line arguments are present, `Main()` calls `GetUserInputs()`.</span></span> <span data-ttu-id="8e517-156">This method prompts the user to enter the path to a single video file and to specify whether a text transcript should be generated.</span><span class="sxs-lookup"><span data-stu-id="8e517-156">This method prompts the user to enter the path to a single video file and to specify whether a text transcript should be generated.</span></span>

> [!NOTE]
> <span data-ttu-id="8e517-157">The console application uses the [Azure Media Indexer API](https://docs.microsoft.com/azure/media-services/media-services-process-content-with-indexer2) to generate transcripts from the uploaded video's audio track. The results are provided in WebVTT format.</span><span class="sxs-lookup"><span data-stu-id="8e517-157">The console application uses the [Azure Media Indexer API](https://docs.microsoft.com/azure/media-services/media-services-process-content-with-indexer2) to generate transcripts from the uploaded video's audio track. The results are provided in WebVTT format.</span></span> <span data-ttu-id="8e517-158">For more information on this format, see [Web Video Text Tracks Format](https://developer.mozilla.org/en-US/docs/Web/API/WebVTT_API).</span><span class="sxs-lookup"><span data-stu-id="8e517-158">For more information on this format, see [Web Video Text Tracks Format](https://developer.mozilla.org/en-US/docs/Web/API/WebVTT_API).</span></span>

### <a name="initialize-and-processvideo-methods"></a><span data-ttu-id="8e517-159">Initialize and ProcessVideo methods</span><span class="sxs-lookup"><span data-stu-id="8e517-159">Initialize and ProcessVideo methods</span></span>

<span data-ttu-id="8e517-160">Regardless of whether the program's options came from the command line or from interactive user input, `Main()` next calls `Initialize()` to create the following instances:</span><span class="sxs-lookup"><span data-stu-id="8e517-160">Regardless of whether the program's options came from the command line or from interactive user input, `Main()` next calls `Initialize()` to create the following instances:</span></span>

|<span data-ttu-id="8e517-161">Class</span><span class="sxs-lookup"><span data-stu-id="8e517-161">Class</span></span>|<span data-ttu-id="8e517-162">Description</span><span class="sxs-lookup"><span data-stu-id="8e517-162">Description</span></span>|
|-|-|
|`AMSComponent`|<span data-ttu-id="8e517-163">Compresses video files before submitting them for moderation.</span><span class="sxs-lookup"><span data-stu-id="8e517-163">Compresses video files before submitting them for moderation.</span></span>|
|`AMSconfigurations`|<span data-ttu-id="8e517-164">Interface to the application's configuration data, found in `App.config`.</span><span class="sxs-lookup"><span data-stu-id="8e517-164">Interface to the application's configuration data, found in `App.config`.</span></span>|
|`VideoModerator`| <span data-ttu-id="8e517-165">Uploading, encoding, encryption, and moderation using AMS SDK</span><span class="sxs-lookup"><span data-stu-id="8e517-165">Uploading, encoding, encryption, and moderation using AMS SDK</span></span>|
|`VideoReviewApi`|<span data-ttu-id="8e517-166">Manages video reviews in the Content Moderator service</span><span class="sxs-lookup"><span data-stu-id="8e517-166">Manages video reviews in the Content Moderator service</span></span>|

<span data-ttu-id="8e517-167">These classes (aside from `AMSConfigurations`, which is straightforward) are covered in more detail in upcoming sections of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="8e517-167">These classes (aside from `AMSConfigurations`, which is straightforward) are covered in more detail in upcoming sections of this tutorial.</span></span>

<span data-ttu-id="8e517-168">Finally, the video files are processed one at a time by calling `ProcessVideo()` for each.</span><span class="sxs-lookup"><span data-stu-id="8e517-168">Finally, the video files are processed one at a time by calling `ProcessVideo()` for each.</span></span>

    private static async Task ProcessVideo(string videoPath)
    {
        Stopwatch sw = new Stopwatch();
        sw.Start();
        Console.ForegroundColor = ConsoleColor.White;
        Console.WriteLine("\nVideo compression process started...");

        var compressedVideoPath = amsComponent.CompressVideo(videoPath);
        if (string.IsNullOrWhiteSpace(compressedVideoPath))
        {
            Console.ForegroundColor = ConsoleColor.Red;
            Console.WriteLine("Video Compression failed.");
        }

        Console.WriteLine("\nVideo compression process completed...");

        UploadVideoStreamRequest uploadVideoStreamRequest = CreateVideoStreamingRequest(compressedVideoPath);
        UploadAssetResult uploadResult = new UploadAssetResult();

        if (generateVtt)
        {
            uploadResult.GenerateVTT = generateVtt;
        }
        Console.WriteLine("\nVideo moderation process started...");

        if (!videoModerator.CreateAzureMediaServicesJobToModerateVideo(uploadVideoStreamRequest, uploadResult))
        {
            Console.ForegroundColor = ConsoleColor.Red;
            Console.WriteLine("Video Review process failed.");
        }

        Console.WriteLine("\nVideo moderation process completed...");
        Console.WriteLine("\nVideo review process started...");
        string reviewId = await videoReviewApi.CreateVideoReviewInContentModerator(uploadResult);
        Console.WriteLine("\nVideo review successfully completed...");
        sw.Stop();
        Console.WriteLine("\nTotal Elapsed Time: {0}", sw.Elapsed);
        using (var stw = new StreamWriter(AmsConfigurations.logFilePath, true))
        {
            stw.WriteLine("Video File Name: " + Path.GetFileName(videoPath));
            stw.WriteLine($"ReviewId: {reviewId}");
            stw.WriteLine("Total Elapsed Time: {0}", sw.Elapsed);
        }
    }


<span data-ttu-id="8e517-169">The `ProcessVideo()` method is fairly straightforward.</span><span class="sxs-lookup"><span data-stu-id="8e517-169">The `ProcessVideo()` method is fairly straightforward.</span></span> <span data-ttu-id="8e517-170">It performs the following operations in the order:</span><span class="sxs-lookup"><span data-stu-id="8e517-170">It performs the following operations in the order:</span></span>

- <span data-ttu-id="8e517-171">Compresses the video</span><span class="sxs-lookup"><span data-stu-id="8e517-171">Compresses the video</span></span>
- <span data-ttu-id="8e517-172">Uploads the video to an Azure Media Services asset</span><span class="sxs-lookup"><span data-stu-id="8e517-172">Uploads the video to an Azure Media Services asset</span></span>
- <span data-ttu-id="8e517-173">Creates an AMS job to moderate the video</span><span class="sxs-lookup"><span data-stu-id="8e517-173">Creates an AMS job to moderate the video</span></span>
- <span data-ttu-id="8e517-174">Creates a video review in Content Moderator</span><span class="sxs-lookup"><span data-stu-id="8e517-174">Creates a video review in Content Moderator</span></span>

<span data-ttu-id="8e517-175">The following sections consider in more detail some of the individual processes invoked by `ProcessVideo()`.</span><span class="sxs-lookup"><span data-stu-id="8e517-175">The following sections consider in more detail some of the individual processes invoked by `ProcessVideo()`.</span></span> 

## <a name="compressing-the-video"></a><span data-ttu-id="8e517-176">Compressing the video</span><span class="sxs-lookup"><span data-stu-id="8e517-176">Compressing the video</span></span>

<span data-ttu-id="8e517-177">To minimize network traffic, the application converts video files to H.264 (MPEG-4 AVC) format and scales them to a maximum width of 640 pixels.</span><span class="sxs-lookup"><span data-stu-id="8e517-177">To minimize network traffic, the application converts video files to H.264 (MPEG-4 AVC) format and scales them to a maximum width of 640 pixels.</span></span> <span data-ttu-id="8e517-178">The H.264 codec is recommended due to its high efficiency (compression rate).</span><span class="sxs-lookup"><span data-stu-id="8e517-178">The H.264 codec is recommended due to its high efficiency (compression rate).</span></span> <span data-ttu-id="8e517-179">The compression is done using the free `ffmpeg` command-line tool, which is included in the `Lib` folder of the Visual Studio solution.</span><span class="sxs-lookup"><span data-stu-id="8e517-179">The compression is done using the free `ffmpeg` command-line tool, which is included in the `Lib` folder of the Visual Studio solution.</span></span> <span data-ttu-id="8e517-180">The input files may be of any format supported by `ffmpeg`, including most commonly used video file formats and codecs.</span><span class="sxs-lookup"><span data-stu-id="8e517-180">The input files may be of any format supported by `ffmpeg`, including most commonly used video file formats and codecs.</span></span>

> [!NOTE]
> <span data-ttu-id="8e517-181">When you start the program using command-line options, you specify a directory containing the video files to be submitted for moderation.</span><span class="sxs-lookup"><span data-stu-id="8e517-181">When you start the program using command-line options, you specify a directory containing the video files to be submitted for moderation.</span></span> <span data-ttu-id="8e517-182">All files in this directory having the `.mp4` filename extension are processed.</span><span class="sxs-lookup"><span data-stu-id="8e517-182">All files in this directory having the `.mp4` filename extension are processed.</span></span> <span data-ttu-id="8e517-183">To process other filename extensions, update the `Main()` method in `Program.cs` to include the desired extensions.</span><span class="sxs-lookup"><span data-stu-id="8e517-183">To process other filename extensions, update the `Main()` method in `Program.cs` to include the desired extensions.</span></span>

<span data-ttu-id="8e517-184">The code that compresses a single video file is the `AmsComponent` class in `AMSComponent.cs`.</span><span class="sxs-lookup"><span data-stu-id="8e517-184">The code that compresses a single video file is the `AmsComponent` class in `AMSComponent.cs`.</span></span> <span data-ttu-id="8e517-185">The method responsible for this functionality is `CompressVideo()`, shown here.</span><span class="sxs-lookup"><span data-stu-id="8e517-185">The method responsible for this functionality is `CompressVideo()`, shown here.</span></span>

    public string CompressVideo(string videoPath)
    {
        string ffmpegBlobUrl;
        if (!ValidatePreRequisites())
        {
            Console.WriteLine("Configurations check failed. Please cross check the configurations!");
            throw new Exception();
        }

        if (File.Exists(_configObj.FfmpegExecutablePath))
        {
            ffmpegBlobUrl = this._configObj.FfmpegExecutablePath;
        }
        else
        {
            Console.WriteLine("ffmpeg.exe is missing. Please check the Lib folder");
            throw new Exception();
        }

        string videoFilePathCom = videoPath.Split('.')[0] + "_c.mp4";
        ProcessStartInfo processStartInfo = new ProcessStartInfo();
        processStartInfo.WindowStyle = ProcessWindowStyle.Hidden;
        processStartInfo.FileName = ffmpegBlobUrl;
        processStartInfo.Arguments = "-i \"" + videoPath + "\" -vcodec libx264 -n -crf 32 -preset veryfast -vf scale=640:-1 -c:a aac -aq 1 -ac 2 -threads 0 \"" + videoFilePathCom + "\"";
        var process = Process.Start(processStartInfo);
        process.WaitForExit();
        process.Close();
        return videoFilePathCom;
    }

<span data-ttu-id="8e517-186">The code performs the following steps:</span><span class="sxs-lookup"><span data-stu-id="8e517-186">The code performs the following steps:</span></span>

- <span data-ttu-id="8e517-187">Checks to make sure the configuration in `App.config` contains all necessary data</span><span class="sxs-lookup"><span data-stu-id="8e517-187">Checks to make sure the configuration in `App.config` contains all necessary data</span></span>
- <span data-ttu-id="8e517-188">Checks to make sure the `ffmpeg` binary is present</span><span class="sxs-lookup"><span data-stu-id="8e517-188">Checks to make sure the `ffmpeg` binary is present</span></span>
- <span data-ttu-id="8e517-189">Builds the output filename by appending `_c.mp4` to the base name of the file (such as `Example.mp4` -> `E>xample_c.mp4`)</span><span class="sxs-lookup"><span data-stu-id="8e517-189">Builds the output filename by appending `_c.mp4` to the base name of the file (such as `Example.mp4` -> `E>xample_c.mp4`)</span></span>
- <span data-ttu-id="8e517-190">Builds a command-line string to perform the conversion</span><span class="sxs-lookup"><span data-stu-id="8e517-190">Builds a command-line string to perform the conversion</span></span>
- <span data-ttu-id="8e517-191">Starts an `ffmpeg` process using the command line</span><span class="sxs-lookup"><span data-stu-id="8e517-191">Starts an `ffmpeg` process using the command line</span></span>
- <span data-ttu-id="8e517-192">Waits for the video to be processed</span><span class="sxs-lookup"><span data-stu-id="8e517-192">Waits for the video to be processed</span></span>

> [!NOTE]
> <span data-ttu-id="8e517-193">If you know your videos are already compressed using H.264 and have appropriate dimensions, you can rewrite `CompressVideo()` to skip the compression.</span><span class="sxs-lookup"><span data-stu-id="8e517-193">If you know your videos are already compressed using H.264 and have appropriate dimensions, you can rewrite `CompressVideo()` to skip the compression.</span></span>

<span data-ttu-id="8e517-194">The method returns the filename of the compressed output file.</span><span class="sxs-lookup"><span data-stu-id="8e517-194">The method returns the filename of the compressed output file.</span></span>

## <a name="uploading-and-moderating-the-video"></a><span data-ttu-id="8e517-195">Uploading and moderating the video</span><span class="sxs-lookup"><span data-stu-id="8e517-195">Uploading and moderating the video</span></span>

<span data-ttu-id="8e517-196">The video must be stored in Azure Media Services before it can be processed by the Content Moderation service.</span><span class="sxs-lookup"><span data-stu-id="8e517-196">The video must be stored in Azure Media Services before it can be processed by the Content Moderation service.</span></span> <span data-ttu-id="8e517-197">The `Program` class in `Program.cs` has a short method `CreateVideoStreamingRequest()` that returns an object representing the streaming request used to upload the video.</span><span class="sxs-lookup"><span data-stu-id="8e517-197">The `Program` class in `Program.cs` has a short method `CreateVideoStreamingRequest()` that returns an object representing the streaming request used to upload the video.</span></span>

    private static UploadVideoStreamRequest CreateVideoStreamingRequest(string compressedVideoFilePath)
    {
        return
            new UploadVideoStreamRequest
            {
                VideoStream = File.ReadAllBytes(compressedVideoFilePath),
                VideoName = Path.GetFileName(compressedVideoFilePath),
                EncodingRequest = new EncodingRequest()
                {
                    EncodingBitrate = AmsEncoding.AdaptiveStreaming
                },
                VideoFilePath = compressedVideoFilePath
            };
    }

<span data-ttu-id="8e517-198">The resulting `UploadVideoStreamRequest` object is defined in `UploadVideoStreamRequest.cs` (and its parent, `UploadVideoRequest`, in `UploadVideoRequest.cs`).</span><span class="sxs-lookup"><span data-stu-id="8e517-198">The resulting `UploadVideoStreamRequest` object is defined in `UploadVideoStreamRequest.cs` (and its parent, `UploadVideoRequest`, in `UploadVideoRequest.cs`).</span></span> <span data-ttu-id="8e517-199">These classes aren't shown here; they're short and serve only to hold the compressed video data and information about it.</span><span class="sxs-lookup"><span data-stu-id="8e517-199">These classes aren't shown here; they're short and serve only to hold the compressed video data and information about it.</span></span> <span data-ttu-id="8e517-200">Another data-only class, `UploadAssetResult` (`UploadAssetResult.cs`) is used to hold the results of the upload process.</span><span class="sxs-lookup"><span data-stu-id="8e517-200">Another data-only class, `UploadAssetResult` (`UploadAssetResult.cs`) is used to hold the results of the upload process.</span></span> <span data-ttu-id="8e517-201">Now it's possible to understand these lines in `ProcessVideo()`:</span><span class="sxs-lookup"><span data-stu-id="8e517-201">Now it's possible to understand these lines in `ProcessVideo()`:</span></span>

    UploadVideoStreamRequest uploadVideoStreamRequest = CreateVideoStreamingRequest(compressedVideoPath);
    UploadAssetResult uploadResult = new UploadAssetResult();

    if (generateVtt)
    {
        uploadResult.GenerateVTT = generateVtt;
    }
    Console.WriteLine("\nVideo moderation process started...");

    if (!videoModerator.CreateAzureMediaServicesJobToModerateVideo(uploadVideoStreamRequest, uploadResult))
    {
        Console.ForegroundColor = ConsoleColor.Red;
        Console.WriteLine("Video Review process failed.");
    }

<span data-ttu-id="8e517-202">These lines perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="8e517-202">These lines perform the following tasks:</span></span>

- <span data-ttu-id="8e517-203">Create a `UploadVideoStreamRequest` to upload the compressed video</span><span class="sxs-lookup"><span data-stu-id="8e517-203">Create a `UploadVideoStreamRequest` to upload the compressed video</span></span>
- <span data-ttu-id="8e517-204">Set the request's `GenerateVTT` flag if the user has requested a text transcript</span><span class="sxs-lookup"><span data-stu-id="8e517-204">Set the request's `GenerateVTT` flag if the user has requested a text transcript</span></span>
- <span data-ttu-id="8e517-205">Calls `CreateAzureMediaServicesJobToModerateVideo()` to perform the upload and receive the result</span><span class="sxs-lookup"><span data-stu-id="8e517-205">Calls `CreateAzureMediaServicesJobToModerateVideo()` to perform the upload and receive the result</span></span>

## <a name="deep-dive-into-video-moderation"></a><span data-ttu-id="8e517-206">Deep dive into video moderation</span><span class="sxs-lookup"><span data-stu-id="8e517-206">Deep dive into video moderation</span></span>

<span data-ttu-id="8e517-207">The method `CreateAzureMediaServicesJobToModerateVideo()` is in `VideoModerator.cs`, which contains the bulk of the code that interacts with Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="8e517-207">The method `CreateAzureMediaServicesJobToModerateVideo()` is in `VideoModerator.cs`, which contains the bulk of the code that interacts with Azure Media Services.</span></span> <span data-ttu-id="8e517-208">The method's source code is shown in the following extract.</span><span class="sxs-lookup"><span data-stu-id="8e517-208">The method's source code is shown in the following extract.</span></span>

    public bool CreateAzureMediaServicesJobToModerateVideo(UploadVideoStreamRequest uploadVideoRequest, UploadAssetResult uploadResult)
    {
        asset = CreateAsset(uploadVideoRequest);
        uploadResult.VideoName = uploadVideoRequest.VideoName;
        // Encoding the asset , Moderating the asset, Generating transcript in parallel
        IAsset encodedAsset = null;
        //Creates the job for the tasks.
        IJob job = this._mediaContext.Jobs.Create("AMS Review Job");

        //Adding encoding task to job.
        ConfigureEncodeAssetTask(uploadVideoRequest.EncodingRequest, job);

        ConfigureContentModerationTask(job);

        //adding transcript task to job.
        if (uploadResult.GenerateVTT)
        {
            ConfigureTranscriptTask(job);
        }

        Stopwatch timer = new Stopwatch();
        timer.Start();
        //submit and execute job.
        job.Submit();
        job.GetExecutionProgressTask(new CancellationTokenSource().Token).Wait();
        timer.Stop();
        using (var sw = new StreamWriter(AmsConfigurations.logFilePath, true))
        {
            sw.WriteLine("AMS Job Elapsed Time: {0}", timer.Elapsed);
        }

        if (job.State == JobState.Error)
        {
            throw new Exception("Video moderation has failed due to AMS Job error.");
        }

        UploadAssetResult result = uploadResult;
        encodedAsset = job.OutputMediaAssets[0];
        result.ModeratedJson = GetCmDetail(job.OutputMediaAssets[1]);
        // Check for valid Moderated JSON
        var jsonModerateObject = JsonConvert.DeserializeObject<VideoModerationResult>(result.ModeratedJson);

        if (jsonModerateObject == null)
        {
            return false;
        }
        if (uploadResult.GenerateVTT)
        {
            GenerateTranscript(job.OutputMediaAssets.Last());
        }

        uploadResult.StreamingUrlDetails = PublishAsset(encodedAsset);
        string downloadUrl = GenerateDownloadUrl(asset, uploadVideoRequest.VideoName);
        uploadResult.StreamingUrlDetails.DownloadUri = downloadUrl;
        uploadResult.VideoName = uploadVideoRequest.VideoName;
        uploadResult.VideoFilePath = uploadVideoRequest.VideoFilePath;
        return true;
    }

<span data-ttu-id="8e517-209">This code performs the following tasks:</span><span class="sxs-lookup"><span data-stu-id="8e517-209">This code performs the following tasks:</span></span>

- <span data-ttu-id="8e517-210">Creates an AMS job for the processing to be done</span><span class="sxs-lookup"><span data-stu-id="8e517-210">Creates an AMS job for the processing to be done</span></span>
- <span data-ttu-id="8e517-211">Adds tasks for encoding the video file, moderating it, and generating a text transcript</span><span class="sxs-lookup"><span data-stu-id="8e517-211">Adds tasks for encoding the video file, moderating it, and generating a text transcript</span></span>
- <span data-ttu-id="8e517-212">Submits the job, uploading the file and beginning processing</span><span class="sxs-lookup"><span data-stu-id="8e517-212">Submits the job, uploading the file and beginning processing</span></span>
- <span data-ttu-id="8e517-213">Retrieves the moderation results, the text transcript (if requested), and other information</span><span class="sxs-lookup"><span data-stu-id="8e517-213">Retrieves the moderation results, the text transcript (if requested), and other information</span></span>

## <a name="sample-video-moderation-response"></a><span data-ttu-id="8e517-214">Sample video moderation response</span><span class="sxs-lookup"><span data-stu-id="8e517-214">Sample video moderation response</span></span>

<span data-ttu-id="8e517-215">The result of the video moderation job (See [video moderation quickstart](video-moderation-api.md) is a JSON data structure containing the moderation results.</span><span class="sxs-lookup"><span data-stu-id="8e517-215">The result of the video moderation job (See [video moderation quickstart](video-moderation-api.md) is a JSON data structure containing the moderation results.</span></span> <span data-ttu-id="8e517-216">These results include a breakdown of the fragments (shots) within the video, each containing events (clips) with key frames that have been flagged for review.</span><span class="sxs-lookup"><span data-stu-id="8e517-216">These results include a breakdown of the fragments (shots) within the video, each containing events (clips) with key frames that have been flagged for review.</span></span> <span data-ttu-id="8e517-217">Each key frame is scored by the likelihood that it contains adult or racy content.</span><span class="sxs-lookup"><span data-stu-id="8e517-217">Each key frame is scored by the likelihood that it contains adult or racy content.</span></span> <span data-ttu-id="8e517-218">The following example shows a JSON response:</span><span class="sxs-lookup"><span data-stu-id="8e517-218">The following example shows a JSON response:</span></span>

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

<span data-ttu-id="8e517-219">A transcription of the audio from the video is also produced when the `GenerateVTT` flag is set.</span><span class="sxs-lookup"><span data-stu-id="8e517-219">A transcription of the audio from the video is also produced when the `GenerateVTT` flag is set.</span></span>

> [!NOTE]
> <span data-ttu-id="8e517-220">The console application uses the [Azure Media Indexer API](https://docs.microsoft.com/azure/media-services/media-services-process-content-with-indexer2) to generate transcripts from the uploaded video's audio track. The results are provided in WebVTT format.</span><span class="sxs-lookup"><span data-stu-id="8e517-220">The console application uses the [Azure Media Indexer API](https://docs.microsoft.com/azure/media-services/media-services-process-content-with-indexer2) to generate transcripts from the uploaded video's audio track. The results are provided in WebVTT format.</span></span> <span data-ttu-id="8e517-221">For more information on this format, see [Web Video Text Tracks Format](https://developer.mozilla.org/en-US/docs/Web/API/WebVTT_API).</span><span class="sxs-lookup"><span data-stu-id="8e517-221">For more information on this format, see [Web Video Text Tracks Format](https://developer.mozilla.org/en-US/docs/Web/API/WebVTT_API).</span></span>


## <a name="creating-the-human-in-the-loop-review"></a><span data-ttu-id="8e517-222">Creating the human-in-the-loop review</span><span class="sxs-lookup"><span data-stu-id="8e517-222">Creating the human-in-the-loop review</span></span>

<span data-ttu-id="8e517-223">The moderation process returns a list of key frames from the video, along with a transcript of its audio tracks.</span><span class="sxs-lookup"><span data-stu-id="8e517-223">The moderation process returns a list of key frames from the video, along with a transcript of its audio tracks.</span></span> <span data-ttu-id="8e517-224">The next step is to create a review in the Content Moderator review tool for human moderators.</span><span class="sxs-lookup"><span data-stu-id="8e517-224">The next step is to create a review in the Content Moderator review tool for human moderators.</span></span> <span data-ttu-id="8e517-225">Going back to the `ProcessVideo()` method in `Program.cs`, you see the call to the `CreateVideoReviewInContentModerator()` method.</span><span class="sxs-lookup"><span data-stu-id="8e517-225">Going back to the `ProcessVideo()` method in `Program.cs`, you see the call to the `CreateVideoReviewInContentModerator()` method.</span></span> <span data-ttu-id="8e517-226">This method is in the `videoReviewApi` class, which is in `VideoReviewAPI.cs`, and is shown here.</span><span class="sxs-lookup"><span data-stu-id="8e517-226">This method is in the `videoReviewApi` class, which is in `VideoReviewAPI.cs`, and is shown here.</span></span>

    public async Task<string> CreateVideoReviewInContentModerator(UploadAssetResult uploadAssetResult)
    {
    
        string reviewId = string.Empty;
        List<ProcessedFrameDetails> frameEntityList = framegenerator.CreateVideoFrames(uploadAssetResult);
        string path = uploadAssetResult.GenerateVTT == true ? this._amsConfig.FfmpegFramesOutputPath + Path.GetFileNameWithoutExtension (uploadAssetResult.VideoName) + "_aud_SpReco.vtt" : "";
        TranscriptScreenTextResult screenTextResult = new TranscriptScreenTextResult();
        
    if (File.Exists(path))
        {
            screenTextResult = await GenerateTextScreenProfanity(reviewId, path, frameEntityList);
            uploadAssetResult.Category1TextScore = screenTextResult.Category1Score;
            uploadAssetResult.Category2TextScore = screenTextResult.Category2Score;
            uploadAssetResult.Category3TextScore = screenTextResult.Category3Score;
            uploadAssetResult.Category1TextTag = screenTextResult.Category1Tag;
            uploadAssetResult.Category2TextTag = screenTextResult.Category2Tag;
            uploadAssetResult.Category3TextTag = screenTextResult.Category3Tag;
        }
        
        var reviewVideoRequestJson = CreateReviewRequestObject(uploadAssetResult, frameEntityList);
        if (string.IsNullOrWhiteSpace(reviewVideoRequestJson))
        {
            throw new Exception("Video review process failed in CreateVideoReviewInContentModerator");
        }
        
        reviewId = JsonConvert.DeserializeObject<List<string>>(ExecuteCreateReviewApi(reviewVideoRequestJson).Result).FirstOrDefault();
        frameEntityList = framegenerator.GenerateFrameImages(frameEntityList, uploadAssetResult, reviewId);
        await CreateAndPublishReviewInContentModerator(uploadAssetResult, frameEntityList, reviewId, path, screenTextResult);
        return reviewId;
    
    }

<span data-ttu-id="8e517-227">`CreateVideoReviewInContentModerator()` calls several other methods to perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="8e517-227">`CreateVideoReviewInContentModerator()` calls several other methods to perform the following tasks:</span></span>

> [!NOTE]
> <span data-ttu-id="8e517-228">The console application uses the [FFmpeg](https://ffmpeg.org/) library for generating thumbnails.</span><span class="sxs-lookup"><span data-stu-id="8e517-228">The console application uses the [FFmpeg](https://ffmpeg.org/) library for generating thumbnails.</span></span> <span data-ttu-id="8e517-229">These thumbnails (images) correspond to the frame timestamps in the [video moderation output](#sample-video-moderation-response).</span><span class="sxs-lookup"><span data-stu-id="8e517-229">These thumbnails (images) correspond to the frame timestamps in the [video moderation output](#sample-video-moderation-response).</span></span>

|<span data-ttu-id="8e517-230">Task</span><span class="sxs-lookup"><span data-stu-id="8e517-230">Task</span></span>|<span data-ttu-id="8e517-231">Methods</span><span class="sxs-lookup"><span data-stu-id="8e517-231">Methods</span></span>|<span data-ttu-id="8e517-232">File</span><span class="sxs-lookup"><span data-stu-id="8e517-232">File</span></span>|
|-|-|-|
|<span data-ttu-id="8e517-233">Extract the key frames from the video and creates thumbnail images of them</span><span class="sxs-lookup"><span data-stu-id="8e517-233">Extract the key frames from the video and creates thumbnail images of them</span></span>|`CreateVideoFrames()`<br>`GenerateFrameImages()`|`FrameGeneratorServices.cs`|
|<span data-ttu-id="8e517-234">Scan the text transcript, if available, to locate adult or racy audio</span><span class="sxs-lookup"><span data-stu-id="8e517-234">Scan the text transcript, if available, to locate adult or racy audio</span></span>|`GenerateTextScreenProfanity()`| `VideoReviewAPI.cs`|
|<span data-ttu-id="8e517-235">Prepare and submits a video review request for human inspection</span><span class="sxs-lookup"><span data-stu-id="8e517-235">Prepare and submits a video review request for human inspection</span></span>|`CreateReviewRequestObject()`<br> `ExecuteCreateReviewApi()`<br>`CreateAndPublishReviewInContentModerator()`|`VideoReviewAPI.cs`|

## <a name="video-review-default-view"></a><span data-ttu-id="8e517-236">Video review default view</span><span class="sxs-lookup"><span data-stu-id="8e517-236">Video review default view</span></span>

<span data-ttu-id="8e517-237">The following screen shows the results of the previous steps.</span><span class="sxs-lookup"><span data-stu-id="8e517-237">The following screen shows the results of the previous steps.</span></span>

![Video review default view](images/video-tutorial-default-view.PNG)

## <a name="transcript-generation"></a><span data-ttu-id="8e517-239">Transcript generation</span><span class="sxs-lookup"><span data-stu-id="8e517-239">Transcript generation</span></span>

<span data-ttu-id="8e517-240">Until now, the code presented in this tutorial has focused on the visual content.</span><span class="sxs-lookup"><span data-stu-id="8e517-240">Until now, the code presented in this tutorial has focused on the visual content.</span></span> <span data-ttu-id="8e517-241">Review of speech content is a separate and optional process that, as mentioned, uses a transcript generated from the audio.</span><span class="sxs-lookup"><span data-stu-id="8e517-241">Review of speech content is a separate and optional process that, as mentioned, uses a transcript generated from the audio.</span></span> <span data-ttu-id="8e517-242">It's time now to take a look at how text transcripts are created and used in the review process.</span><span class="sxs-lookup"><span data-stu-id="8e517-242">It's time now to take a look at how text transcripts are created and used in the review process.</span></span> <span data-ttu-id="8e517-243">The task of generating the transcript falls to the [Azure Media Indexer](https://docs.microsoft.com/azure/media-services/media-services-index-content) service.</span><span class="sxs-lookup"><span data-stu-id="8e517-243">The task of generating the transcript falls to the [Azure Media Indexer](https://docs.microsoft.com/azure/media-services/media-services-index-content) service.</span></span>

<span data-ttu-id="8e517-244">The application performs the following tasks:</span><span class="sxs-lookup"><span data-stu-id="8e517-244">The application performs the following tasks:</span></span>

|<span data-ttu-id="8e517-245">Task</span><span class="sxs-lookup"><span data-stu-id="8e517-245">Task</span></span>|<span data-ttu-id="8e517-246">Methods</span><span class="sxs-lookup"><span data-stu-id="8e517-246">Methods</span></span>|<span data-ttu-id="8e517-247">File</span><span class="sxs-lookup"><span data-stu-id="8e517-247">File</span></span>|
|-|-|-|
|<span data-ttu-id="8e517-248">Determine whether text transcripts are to be generated</span><span class="sxs-lookup"><span data-stu-id="8e517-248">Determine whether text transcripts are to be generated</span></span>|`Main()`<br>`GetUserInputs()`|`Program.cs`|
|<span data-ttu-id="8e517-249">If so, submit a transcription job as part of moderation</span><span class="sxs-lookup"><span data-stu-id="8e517-249">If so, submit a transcription job as part of moderation</span></span>|`ConfigureTranscriptTask()`|`VideoModerator.cs`|
|<span data-ttu-id="8e517-250">Get a local copy of the transcript</span><span class="sxs-lookup"><span data-stu-id="8e517-250">Get a local copy of the transcript</span></span>|`GenerateTranscript()`|`VideoModerator.cs`|
|<span data-ttu-id="8e517-251">Flag frames of the video that contain inappropriate audio</span><span class="sxs-lookup"><span data-stu-id="8e517-251">Flag frames of the video that contain inappropriate audio</span></span>|`GenerateTextScreenProfanity()`<br>`TextScreen()`|`VideoReviewAPI.cs`|
|<span data-ttu-id="8e517-252">Add the results to the review</span><span class="sxs-lookup"><span data-stu-id="8e517-252">Add the results to the review</span></span>|`UploadScreenTextResult()`<br>`ExecuteAddTranscriptSupportFile()`|`VideoReviewAPI.cs`|

### <a name="task-configuration"></a><span data-ttu-id="8e517-253">Task configuration</span><span class="sxs-lookup"><span data-stu-id="8e517-253">Task configuration</span></span>

<span data-ttu-id="8e517-254">Let's jump right into submitting the transcription job.</span><span class="sxs-lookup"><span data-stu-id="8e517-254">Let's jump right into submitting the transcription job.</span></span> <span data-ttu-id="8e517-255">`CreateAzureMediaServicesJobToModerateVideo()` (already described) calls `ConfigureTranscriptTask()`.</span><span class="sxs-lookup"><span data-stu-id="8e517-255">`CreateAzureMediaServicesJobToModerateVideo()` (already described) calls `ConfigureTranscriptTask()`.</span></span>

    private void ConfigureTranscriptTask(IJob job)
    {
        string mediaProcessorName = _amsConfigurations.MediaIndexer2MediaProcessor;
        IMediaProcessor processor = _mediaContext.MediaProcessors.GetLatestMediaProcessorByName(mediaProcessorName);

        string configuration = File.ReadAllText(_amsConfigurations.MediaIndexerConfigurationJson);
        ITask task = job.Tasks.AddNew("AudioIndexing Task", processor, configuration, TaskOptions.None);
        task.InputAssets.Add(asset);
        task.OutputAssets.AddNew("AudioIndexing Output Asset", AssetCreationOptions.None);
    }

<span data-ttu-id="8e517-256">The configuration for the transcript task is read from the file `MediaIndexerConfig.json` in the solution's `Lib` folder.</span><span class="sxs-lookup"><span data-stu-id="8e517-256">The configuration for the transcript task is read from the file `MediaIndexerConfig.json` in the solution's `Lib` folder.</span></span> <span data-ttu-id="8e517-257">AMS assets are created for the configuration file and for the output of the transcription process.</span><span class="sxs-lookup"><span data-stu-id="8e517-257">AMS assets are created for the configuration file and for the output of the transcription process.</span></span> <span data-ttu-id="8e517-258">When the AMS job runs, this task creates a text transcript from the video file's audio track.</span><span class="sxs-lookup"><span data-stu-id="8e517-258">When the AMS job runs, this task creates a text transcript from the video file's audio track.</span></span>

> [!NOTE]
> <span data-ttu-id="8e517-259">The sample application recognizes speech in US English only.</span><span class="sxs-lookup"><span data-stu-id="8e517-259">The sample application recognizes speech in US English only.</span></span>

### <a name="transcript-generation"></a><span data-ttu-id="8e517-260">Transcript generation</span><span class="sxs-lookup"><span data-stu-id="8e517-260">Transcript generation</span></span>

<span data-ttu-id="8e517-261">The transcript is published as an AMS asset.</span><span class="sxs-lookup"><span data-stu-id="8e517-261">The transcript is published as an AMS asset.</span></span> <span data-ttu-id="8e517-262">To scan the transcript for objectionable content, the application downloads the asset from Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="8e517-262">To scan the transcript for objectionable content, the application downloads the asset from Azure Media Services.</span></span> <span data-ttu-id="8e517-263">`CreateAzureMediaServicesJobToModerateVideo()` calls `GenerateTranscript()`, shown here, to retrieve the file.</span><span class="sxs-lookup"><span data-stu-id="8e517-263">`CreateAzureMediaServicesJobToModerateVideo()` calls `GenerateTranscript()`, shown here, to retrieve the file.</span></span>

    public bool GenerateTranscript(IAsset asset)
    {
        try
        {
            var outputFolder = this._amsConfigurations.FfmpegFramesOutputPath;
            IAsset outputAsset = asset;
            IAccessPolicy policy = null;
            ILocator locator = null;
            policy = _mediaContext.AccessPolicies.Create("My 30 days readonly policy", TimeSpan.FromDays(360), AccessPermissions.Read);
            locator = _mediaContext.Locators.CreateLocator(LocatorType.Sas, outputAsset, policy, DateTime.UtcNow.AddMinutes(-5));
            DownloadAssetToLocal(outputAsset, outputFolder);
            locator.Delete();
            return true;
        }
        catch
        {   //TODO:  Logging
            Console.WriteLine("Exception occured while generating index for video.");
            throw;
        }
    }

<span data-ttu-id="8e517-264">After some necessary AMS setup, the actual download is performed by calling `DownloadAssetToLocal()`, a generic function that copies an AMS asset to a local file.</span><span class="sxs-lookup"><span data-stu-id="8e517-264">After some necessary AMS setup, the actual download is performed by calling `DownloadAssetToLocal()`, a generic function that copies an AMS asset to a local file.</span></span>

## <a name="transcript-moderation"></a><span data-ttu-id="8e517-265">Transcript moderation</span><span class="sxs-lookup"><span data-stu-id="8e517-265">Transcript moderation</span></span>

<span data-ttu-id="8e517-266">With the transcript close at hand, it is scanned and used in the review.</span><span class="sxs-lookup"><span data-stu-id="8e517-266">With the transcript close at hand, it is scanned and used in the review.</span></span> <span data-ttu-id="8e517-267">Creating the review is the purview of `CreateVideoReviewInContentModerator()`, that calls `GenerateTextScreenProfanity()` to do the job.</span><span class="sxs-lookup"><span data-stu-id="8e517-267">Creating the review is the purview of `CreateVideoReviewInContentModerator()`, that calls `GenerateTextScreenProfanity()` to do the job.</span></span> <span data-ttu-id="8e517-268">In turn, this method calls `TextScreen()`, that contains most of the functionality.</span><span class="sxs-lookup"><span data-stu-id="8e517-268">In turn, this method calls `TextScreen()`, that contains most of the functionality.</span></span> 

<span data-ttu-id="8e517-269">`TextScreen()` performs the following tasks:</span><span class="sxs-lookup"><span data-stu-id="8e517-269">`TextScreen()` performs the following tasks:</span></span>

- <span data-ttu-id="8e517-270">Parse the transcript for time tamps and captions</span><span class="sxs-lookup"><span data-stu-id="8e517-270">Parse the transcript for time tamps and captions</span></span>
- <span data-ttu-id="8e517-271">Submit each caption for text moderation</span><span class="sxs-lookup"><span data-stu-id="8e517-271">Submit each caption for text moderation</span></span>
- <span data-ttu-id="8e517-272">Flag any frames that may have objectionable speech content</span><span class="sxs-lookup"><span data-stu-id="8e517-272">Flag any frames that may have objectionable speech content</span></span>

<span data-ttu-id="8e517-273">Let's examine each these tasks in more detail:</span><span class="sxs-lookup"><span data-stu-id="8e517-273">Let's examine each these tasks in more detail:</span></span>

### <a name="initialize-the-code"></a><span data-ttu-id="8e517-274">Initialize the code</span><span class="sxs-lookup"><span data-stu-id="8e517-274">Initialize the code</span></span>

<span data-ttu-id="8e517-275">First, initialize all variables and collections.</span><span class="sxs-lookup"><span data-stu-id="8e517-275">First, initialize all variables and collections.</span></span>

    private async Task<TranscriptScreenTextResult> TextScreen(string filepath, List<ProcessedFrameDetails> frameEntityList)
    {
        List<TranscriptProfanity> profanityList = new List<TranscriptProfanity>();
        string responseContent = string.Empty;
        HttpResponseMessage response;
        bool category1Tag = false;
        bool category2Tag = false;
        bool category3Tag = false;
        double category1Score = 0;
        double category2Score = 0;
        double category3Score = 0;
        List<string> vttLines = File.ReadAllLines(filepath).Where(line => !line.Contains("NOTE Confidence:") && line.Length > 0).ToList();
        StringBuilder sb = new StringBuilder();
        List<CaptionScreentextResult> csrList = new List<CaptionScreentextResult>();
        CaptionScreentextResult captionScreentextResult = new CaptionScreentextResult() { Captions = new List<string>() };

        // Code from the next sections in the tutorial
    

### <a name="parse-the-transcript-for-captions"></a><span data-ttu-id="8e517-276">Parse the transcript for captions</span><span class="sxs-lookup"><span data-stu-id="8e517-276">Parse the transcript for captions</span></span>

<span data-ttu-id="8e517-277">Next, parse the VTT formatted transcript for captions and timestamps.</span><span class="sxs-lookup"><span data-stu-id="8e517-277">Next, parse the VTT formatted transcript for captions and timestamps.</span></span> <span data-ttu-id="8e517-278">The review tool displays these captions in the Transcript Tab on the video review screen.</span><span class="sxs-lookup"><span data-stu-id="8e517-278">The review tool displays these captions in the Transcript Tab on the video review screen.</span></span> <span data-ttu-id="8e517-279">The timestamps are used to sync the captions with the corresponding video frames.</span><span class="sxs-lookup"><span data-stu-id="8e517-279">The timestamps are used to sync the captions with the corresponding video frames.</span></span>

        // Code from the previous section(s) in the tutorial

        //
        // Parse the transcript
        //
        foreach (var line in vttLines.Skip(1))
        {
                if (line.Contains("-->"))
                {
                    if (sb.Length > 0)
                    {
                        captionScreentextResult.Captions.Add(sb.ToString());
                        sb.Clear();
                    }
                    if (captionScreentextResult.Captions.Count > 0)
                    {
                        csrList.Add(captionScreentextResult);
                        captionScreentextResult = new CaptionScreentextResult() { Captions = new List<string>() };
                    }
                    string[] times = line.Split(new string[] { "-->" }, StringSplitOptions.RemoveEmptyEntries);
                    string startTimeString = times[0].Trim();
                    string endTimeString = times[1].Trim();
                    int startTime = (int)TimeSpan.ParseExact(startTimeString, @"hh\:mm\:ss\.fff", CultureInfo.InvariantCulture).TotalMilliseconds;
                    int endTime = (int)TimeSpan.ParseExact(endTimeString, @"hh\:mm\:ss\.fff", CultureInfo.InvariantCulture).TotalMilliseconds;
                    captionScreentextResult.StartTime = startTime;
                    captionScreentextResult.EndTime = endTime;
                }
                else
                {
                    sb.Append(line);
                }
                if (sb.Length + line.Length > 1024)
                {
                    captionScreentextResult.Captions.Add(sb.ToString());
                    sb.Clear();
                }
            }
            if (sb.Length > 0)
            {
                captionScreentextResult.Captions.Add(sb.ToString());
            }
            if (captionScreentextResult.Captions.Count > 0)
            {
                csrList.Add(captionScreentextResult);
            }

            // Code from the following section in the quickstart

### <a name="moderate-captions-with-the-text-moderation-service"></a><span data-ttu-id="8e517-280">Moderate captions with the text moderation service</span><span class="sxs-lookup"><span data-stu-id="8e517-280">Moderate captions with the text moderation service</span></span>

<span data-ttu-id="8e517-281">Next, we scan the parsed text captions with Content Moderator's text API.</span><span class="sxs-lookup"><span data-stu-id="8e517-281">Next, we scan the parsed text captions with Content Moderator's text API.</span></span>

> [!NOTE]
> <span data-ttu-id="8e517-282">Your Content Moderator service key has a requests per second (RPS) rate limit.</span><span class="sxs-lookup"><span data-stu-id="8e517-282">Your Content Moderator service key has a requests per second (RPS) rate limit.</span></span> <span data-ttu-id="8e517-283">If you exceed the limit, the SDK throws an exception with a 429 error code.</span><span class="sxs-lookup"><span data-stu-id="8e517-283">If you exceed the limit, the SDK throws an exception with a 429 error code.</span></span> 
>
> <span data-ttu-id="8e517-284">A free tier key has a one RPS rate limit.</span><span class="sxs-lookup"><span data-stu-id="8e517-284">A free tier key has a one RPS rate limit.</span></span>

    //
    // Moderate the captions or cues
    //
    int waitTime = 1000;
    foreach (var csr in csrList)
    {
                bool captionAdultTextTag = false;
                bool captionRacyTextTag = false;
                bool captionOffensiveTextTag = false;
                bool retry = true;

                foreach (var caption in csr.Captions)
                {
                    while (retry)
                    {
                        try
                        {
                            System.Threading.Thread.Sleep(waitTime);
                            var lang = await CMClient.TextModeration.DetectLanguageAsync("text/plain", caption);
                            var oRes = await CMClient.TextModeration.ScreenTextWithHttpMessagesAsync(lang.DetectedLanguageProperty, "text/plain", caption, null, null, null, true);
                            response = oRes.Response;
                            responseContent = await response.Content.ReadAsStringAsync();
                            retry = false;
                        }
                        catch (Exception e)
                        {
                            if (e.Message.Contains("429"))
                            {
                                Console.WriteLine($"Moderation API call failed. Message: {e.Message}");
                                waitTime = (int)(waitTime * 1.5);
                                Console.WriteLine($"wait time: {waitTime}");
                            }
                            else
                            {
                                retry = false;
                                Console.WriteLine($"Moderation API call failed. Message: {e.Message}");
                            }
                        }
                    }
                    var jsonTextScreen = JsonConvert.DeserializeObject<TextScreen>(responseContent);
                    if (jsonTextScreen != null)
                    {
                        TranscriptProfanity transcriptProfanity = new TranscriptProfanity();
                        transcriptProfanity.TimeStamp = "";
                        List<Terms> transcriptTerm = new List<Terms>();
                        if (jsonTextScreen.Terms != null)
                        {
                            foreach (var term in jsonTextScreen.Terms)
                            {
                                var profanityobject = new Terms
                                {
                                    Term = term.Term,
                                    Index = term.Index
                                };
                                transcriptTerm.Add(profanityobject);
                            }
                            transcriptProfanity.Terms = transcriptTerm;
                            profanityList.Add(transcriptProfanity);
                        }
                        if (jsonTextScreen.Classification.Category1.Score > _amsConfig.Category1TextThreshold) captionAdultTextTag = true;
                        if (jsonTextScreen.Classification.Category2.Score > _amsConfig.Category2TextThreshold) captionRacyTextTag = true;
                        if (jsonTextScreen.Classification.Category3.Score > _amsConfig.Category3TextThreshold) captionOffensiveTextTag = true;
                        if (jsonTextScreen.Classification.Category1.Score > _amsConfig.Category1TextThreshold) category1Tag = true;
                        if (jsonTextScreen.Classification.Category2.Score > _amsConfig.Category2TextThreshold) category2Tag = true;
                        if (jsonTextScreen.Classification.Category3.Score > _amsConfig.Category3TextThreshold) category3Tag = true;
                        category1Score = jsonTextScreen.Classification.Category1.Score > category1Score ? jsonTextScreen.Classification.Category1.Score : category1Score;
                        category2Score = jsonTextScreen.Classification.Category2.Score > category2Score ? jsonTextScreen.Classification.Category2.Score : category2Score;
                        category3Score = jsonTextScreen.Classification.Category3.Score > category3Score ? jsonTextScreen.Classification.Category3.Score : category3Score;
                    }
                    foreach (var frame in frameEntityList.Where(x => x.TimeStamp >= csr.StartTime && x.TimeStamp <= csr.EndTime))
                    {
                        frame.IsAdultTextContent = captionAdultTextTag;
                        frame.IsRacyTextContent = captionRacyTextTag;
                        frame.IsOffensiveTextContent = captionOffensiveTextTag;
                    }
                }
            }
            TranscriptScreenTextResult screenTextResult = new TranscriptScreenTextResult()
            {
                TranscriptProfanity = profanityList,
                Category1Tag = category1Tag,
                Category2Tag = category2Tag,
                Category3Tag = category3Tag,
                Category1Score = category1Score,
                Category2Score = category2Score,
                Category3Score = category3Score
            };
            return screenTextResult;
    }

### <a name="breaking-down-the-text-moderation-step"></a><span data-ttu-id="8e517-285">Breaking down the text moderation step</span><span class="sxs-lookup"><span data-stu-id="8e517-285">Breaking down the text moderation step</span></span>

<span data-ttu-id="8e517-286">`TextScreen()` is a substantial method, so let's break it down.</span><span class="sxs-lookup"><span data-stu-id="8e517-286">`TextScreen()` is a substantial method, so let's break it down.</span></span>

1. <span data-ttu-id="8e517-287">First, the method reads the transcript file line by line.</span><span class="sxs-lookup"><span data-stu-id="8e517-287">First, the method reads the transcript file line by line.</span></span> <span data-ttu-id="8e517-288">It ignores blank lines and lines containing a `NOTE` with a confidence score.</span><span class="sxs-lookup"><span data-stu-id="8e517-288">It ignores blank lines and lines containing a `NOTE` with a confidence score.</span></span> <span data-ttu-id="8e517-289">It extracts the time stamps and text items from the *cues* in the file.</span><span class="sxs-lookup"><span data-stu-id="8e517-289">It extracts the time stamps and text items from the *cues* in the file.</span></span> <span data-ttu-id="8e517-290">A cue represents text from the audio track and includes start and end times.</span><span class="sxs-lookup"><span data-stu-id="8e517-290">A cue represents text from the audio track and includes start and end times.</span></span> <span data-ttu-id="8e517-291">A cue begins with the time stamp line with the string `-->`.</span><span class="sxs-lookup"><span data-stu-id="8e517-291">A cue begins with the time stamp line with the string `-->`.</span></span> <span data-ttu-id="8e517-292">It is followed by one or more lines of text.</span><span class="sxs-lookup"><span data-stu-id="8e517-292">It is followed by one or more lines of text.</span></span>

1. <span data-ttu-id="8e517-293">Instances of `CaptionScreentextResult` (defined in `TranscriptProfanity.cs`) are used to hold the information parsed from each cue.</span><span class="sxs-lookup"><span data-stu-id="8e517-293">Instances of `CaptionScreentextResult` (defined in `TranscriptProfanity.cs`) are used to hold the information parsed from each cue.</span></span>  <span data-ttu-id="8e517-294">When a new time stamp line is detected, or a maximum text length of 1024 characters is reached, a new `CaptionScreentextResult` is added to the `csrList`.</span><span class="sxs-lookup"><span data-stu-id="8e517-294">When a new time stamp line is detected, or a maximum text length of 1024 characters is reached, a new `CaptionScreentextResult` is added to the `csrList`.</span></span> 

1. <span data-ttu-id="8e517-295">The method next submits each cue to the Text Moderation API.</span><span class="sxs-lookup"><span data-stu-id="8e517-295">The method next submits each cue to the Text Moderation API.</span></span> <span data-ttu-id="8e517-296">It calls both `ContentModeratorClient.TextModeration.DetectLanguageAsync()` and `ContentModeratorClient.TextModeration.ScreenTextWithHttpMessagesAsync()`, which are defined in the `Microsoft.Azure.CognitiveServices.ContentModerator` assembly.</span><span class="sxs-lookup"><span data-stu-id="8e517-296">It calls both `ContentModeratorClient.TextModeration.DetectLanguageAsync()` and `ContentModeratorClient.TextModeration.ScreenTextWithHttpMessagesAsync()`, which are defined in the `Microsoft.Azure.CognitiveServices.ContentModerator` assembly.</span></span> <span data-ttu-id="8e517-297">To avoid being rate-limited, the method pauses for a second before submitting each cue.</span><span class="sxs-lookup"><span data-stu-id="8e517-297">To avoid being rate-limited, the method pauses for a second before submitting each cue.</span></span>

1. <span data-ttu-id="8e517-298">After receiving results from the Text Moderation service, the method then analyzes them to see whether they meet confidence thresholds.</span><span class="sxs-lookup"><span data-stu-id="8e517-298">After receiving results from the Text Moderation service, the method then analyzes them to see whether they meet confidence thresholds.</span></span> <span data-ttu-id="8e517-299">These values are established in `App.config` as `OffensiveTextThreshold`, `RacyTextThreshold`, and `AdultTextThreshold`.</span><span class="sxs-lookup"><span data-stu-id="8e517-299">These values are established in `App.config` as `OffensiveTextThreshold`, `RacyTextThreshold`, and `AdultTextThreshold`.</span></span> <span data-ttu-id="8e517-300">Finally, the objectionable terms themselves are also stored.</span><span class="sxs-lookup"><span data-stu-id="8e517-300">Finally, the objectionable terms themselves are also stored.</span></span> <span data-ttu-id="8e517-301">All frames within the cue's time range are flagged as containing offensive, racy, and/or adult text.</span><span class="sxs-lookup"><span data-stu-id="8e517-301">All frames within the cue's time range are flagged as containing offensive, racy, and/or adult text.</span></span>

1. <span data-ttu-id="8e517-302">`TextScreen()` returns a `TranscriptScreenTextResult` instance that contains the text moderation result from the video as a whole.</span><span class="sxs-lookup"><span data-stu-id="8e517-302">`TextScreen()` returns a `TranscriptScreenTextResult` instance that contains the text moderation result from the video as a whole.</span></span> <span data-ttu-id="8e517-303">This object includes flags and scores for the various types of objectionable content, along with a list of all objectionable terms.</span><span class="sxs-lookup"><span data-stu-id="8e517-303">This object includes flags and scores for the various types of objectionable content, along with a list of all objectionable terms.</span></span> <span data-ttu-id="8e517-304">The caller, `CreateVideoReviewInContentModerator()`, calls `UploadScreenTextResult()` to attach this information to the review so it is available to human reviewers.</span><span class="sxs-lookup"><span data-stu-id="8e517-304">The caller, `CreateVideoReviewInContentModerator()`, calls `UploadScreenTextResult()` to attach this information to the review so it is available to human reviewers.</span></span>
 
## <a name="video-review-transcript-view"></a><span data-ttu-id="8e517-305">Video review transcript view</span><span class="sxs-lookup"><span data-stu-id="8e517-305">Video review transcript view</span></span>

<span data-ttu-id="8e517-306">The following screen shows the result of the transcript generation and moderation steps.</span><span class="sxs-lookup"><span data-stu-id="8e517-306">The following screen shows the result of the transcript generation and moderation steps.</span></span>

![Video moderation transcript view](images/video-tutorial-transcript-view.PNG)

## <a name="program-output"></a><span data-ttu-id="8e517-308">Program output</span><span class="sxs-lookup"><span data-stu-id="8e517-308">Program output</span></span>

<span data-ttu-id="8e517-309">The following command-line output from the program shows the various tasks as they are completed.</span><span class="sxs-lookup"><span data-stu-id="8e517-309">The following command-line output from the program shows the various tasks as they are completed.</span></span> <span data-ttu-id="8e517-310">Additionally, the moderation result (in JSON format) and the speech transcript are available in the same directory as the original video files.</span><span class="sxs-lookup"><span data-stu-id="8e517-310">Additionally, the moderation result (in JSON format) and the speech transcript are available in the same directory as the original video files.</span></span>

    Microsoft.ContentModerator.AMSComponentClient
    Enter the fully qualified local path for Uploading the video :
    "Your File Name.MP4"
    Generate Video Transcript? [y/n] : y
    
    Video compression process started...
    Video compression process completed...
    
    Video moderation process started...
    Video moderation process completed...
    
    Video review process started...
    Video Frames Creation inprogress...
    Frames(83) created successfully.
    Review Created Successfully and the review Id 201801va8ec2108d6e043229ba7a9e6373edec5
    Video review successfully completed...
    
    Total Elapsed Time: 00:05:56.8420355


## <a name="next-steps"></a><span data-ttu-id="8e517-311">Next steps</span><span class="sxs-lookup"><span data-stu-id="8e517-311">Next steps</span></span>

<span data-ttu-id="8e517-312">[Download the Visual Studio solution](https://github.com/MicrosoftContentModerator/VideoReviewConsoleApp) and sample files and required libraries for this tutorial, and get started on your integration.</span><span class="sxs-lookup"><span data-stu-id="8e517-312">[Download the Visual Studio solution](https://github.com/MicrosoftContentModerator/VideoReviewConsoleApp) and sample files and required libraries for this tutorial, and get started on your integration.</span></span>
