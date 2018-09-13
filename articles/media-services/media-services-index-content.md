---
title: Indexing Media Files with Azure Media Indexer
description: Azure Media Indexer enables you to make content of your media files searchable and to generate a full-text transcript for closed captioning and keywords. This topic shows how to use Media Indexer.
services: media-services
documentationcenter: ''
author: Asolanki
manager: erikre
editor: ''
ms.assetid: 827a56b2-58a5-4044-8d5c-3e5356488271
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/12/2016
ms.author: adsolank;juliako;johndeu
ms.openlocfilehash: f8906171b97b44b220042a1b019b25d74bb8e716
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556004"
---
# <a name="indexing-media-files-with-azure-media-indexer"></a><span data-ttu-id="f5539-104">Indexing Media Files with Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="f5539-104">Indexing Media Files with Azure Media Indexer</span></span>
<span data-ttu-id="f5539-105">Azure Media Indexer enables you to make content of your media files searchable and to generate a full-text transcript for closed captioning and keywords.</span><span class="sxs-lookup"><span data-stu-id="f5539-105">Azure Media Indexer enables you to make content of your media files searchable and to generate a full-text transcript for closed captioning and keywords.</span></span> <span data-ttu-id="f5539-106">You can process one media file or multiple media files in a batch.</span><span class="sxs-lookup"><span data-stu-id="f5539-106">You can process one media file or multiple media files in a batch.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="f5539-107">When indexing content, make sure to use media files that have very clear speech (without background music, noise, effects, or microphone hiss).</span><span class="sxs-lookup"><span data-stu-id="f5539-107">When indexing content, make sure to use media files that have very clear speech (without background music, noise, effects, or microphone hiss).</span></span> <span data-ttu-id="f5539-108">Some examples of appropriate content are: recorded meetings, lectures or presentations.</span><span class="sxs-lookup"><span data-stu-id="f5539-108">Some examples of appropriate content are: recorded meetings, lectures or presentations.</span></span> <span data-ttu-id="f5539-109">The following content might not be suitable for indexing: movies, TV shows, anything with mixed audio and sound effects, poorly recorded content with background noise (hiss).</span><span class="sxs-lookup"><span data-stu-id="f5539-109">The following content might not be suitable for indexing: movies, TV shows, anything with mixed audio and sound effects, poorly recorded content with background noise (hiss).</span></span>
> 
> 

<span data-ttu-id="f5539-110">An indexing job can generate the following outputs:</span><span class="sxs-lookup"><span data-stu-id="f5539-110">An indexing job can generate the following outputs:</span></span>

* <span data-ttu-id="f5539-111">Closed caption files in the following formats: **SAMI**, **TTML**, and **WebVTT**.</span><span class="sxs-lookup"><span data-stu-id="f5539-111">Closed caption files in the following formats: **SAMI**, **TTML**, and **WebVTT**.</span></span>
  
    <span data-ttu-id="f5539-112">Closed caption files include a tag called Recognizability, which scores an indexing job based on how recognizable the speech in the source video is.</span><span class="sxs-lookup"><span data-stu-id="f5539-112">Closed caption files include a tag called Recognizability, which scores an indexing job based on how recognizable the speech in the source video is.</span></span>  <span data-ttu-id="f5539-113">You can use the value of Recognizability to screen output files for usability.</span><span class="sxs-lookup"><span data-stu-id="f5539-113">You can use the value of Recognizability to screen output files for usability.</span></span> <span data-ttu-id="f5539-114">A low score would mean poor indexing results due to audio quality.</span><span class="sxs-lookup"><span data-stu-id="f5539-114">A low score would mean poor indexing results due to audio quality.</span></span>
* <span data-ttu-id="f5539-115">Keyword file (XML).</span><span class="sxs-lookup"><span data-stu-id="f5539-115">Keyword file (XML).</span></span>
* <span data-ttu-id="f5539-116">Audio indexing blob file (AIB) for use with SQL server.</span><span class="sxs-lookup"><span data-stu-id="f5539-116">Audio indexing blob file (AIB) for use with SQL server.</span></span>
  
    <span data-ttu-id="f5539-117">For more information, see [Using AIB Files with Azure Media Indexer and SQL Server](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/).</span><span class="sxs-lookup"><span data-stu-id="f5539-117">For more information, see [Using AIB Files with Azure Media Indexer and SQL Server](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/).</span></span>

<span data-ttu-id="f5539-118">This topic shows how to create indexing jobs to **Index an asset** and **Index multiple files**.</span><span class="sxs-lookup"><span data-stu-id="f5539-118">This topic shows how to create indexing jobs to **Index an asset** and **Index multiple files**.</span></span>

<span data-ttu-id="f5539-119">For the latest Azure Media Indexer updates, see [Media Services blogs](#preset).</span><span class="sxs-lookup"><span data-stu-id="f5539-119">For the latest Azure Media Indexer updates, see [Media Services blogs](#preset).</span></span>

## <a name="using-configuration-and-manifest-files-for-indexing-tasks"></a><span data-ttu-id="f5539-120">Using configuration and manifest files for indexing tasks</span><span class="sxs-lookup"><span data-stu-id="f5539-120">Using configuration and manifest files for indexing tasks</span></span>
<span data-ttu-id="f5539-121">You can specify more details for your indexing tasks by using a task configuration.</span><span class="sxs-lookup"><span data-stu-id="f5539-121">You can specify more details for your indexing tasks by using a task configuration.</span></span> <span data-ttu-id="f5539-122">For example, you can specify which metadata to use for your media file.</span><span class="sxs-lookup"><span data-stu-id="f5539-122">For example, you can specify which metadata to use for your media file.</span></span> <span data-ttu-id="f5539-123">This metadata is used by the language engine to expand its vocabulary, and greatly improves the speech recognition accuracy.</span><span class="sxs-lookup"><span data-stu-id="f5539-123">This metadata is used by the language engine to expand its vocabulary, and greatly improves the speech recognition accuracy.</span></span>  <span data-ttu-id="f5539-124">You are also able to specify your desired output files.</span><span class="sxs-lookup"><span data-stu-id="f5539-124">You are also able to specify your desired output files.</span></span>

<span data-ttu-id="f5539-125">You can also process multiple media files at once by using a manifest file.</span><span class="sxs-lookup"><span data-stu-id="f5539-125">You can also process multiple media files at once by using a manifest file.</span></span>

<span data-ttu-id="f5539-126">For more information, see [Task Preset for Azure Media Indexer](https://msdn.microsoft.com/library/dn783454.aspx).</span><span class="sxs-lookup"><span data-stu-id="f5539-126">For more information, see [Task Preset for Azure Media Indexer](https://msdn.microsoft.com/library/dn783454.aspx).</span></span>

## <a name="index-an-asset"></a><span data-ttu-id="f5539-127">Index an asset</span><span class="sxs-lookup"><span data-stu-id="f5539-127">Index an asset</span></span>
<span data-ttu-id="f5539-128">The following method uploads a media file as an asset and creates a job to index the asset.</span><span class="sxs-lookup"><span data-stu-id="f5539-128">The following method uploads a media file as an asset and creates a job to index the asset.</span></span>

<span data-ttu-id="f5539-129">Note that if no configuration file is specified, the media file will be indexed with all default settings.</span><span class="sxs-lookup"><span data-stu-id="f5539-129">Note that if no configuration file is specified, the media file will be indexed with all default settings.</span></span>

    static bool RunIndexingJob(string inputMediaFilePath, string outputFolder, string configurationFile = "")
    {
        // Create an asset and upload the input media file to storage.
        IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Indexing Input Asset",
            AssetCreationOptions.None);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job");

        // Get a reference to the Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration from file if specified.
        string configuration = string.IsNullOrEmpty(configurationFile) ? "" : File.ReadAllText(configurationFile);

        // Create a task with the encoding details, using a string preset.
        ITask task = job.Tasks.AddNew("My Indexing Task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify the input asset to be indexed.
        task.InputAssets.Add(asset);

        // Add an output asset to contain the results of the job.
        task.OutputAssets.AddNew("My Indexing Output Asset", AssetCreationOptions.None);

        // Use the following event handler to check job progress.  
        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

        // Launch the job.
        job.Submit();

        // Check job execution and wait for job to finish.
        Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
        progressJobTask.Wait();

        // If job state is Error, the event handling
        // method for job progress should log errors.  Here we check
        // for error state and exit if needed.
        if (job.State == JobState.Error)
        {
            Console.WriteLine("Exiting method due to job error.");
            return false;
        }

        // Download the job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
    }

    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = _context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }  
<!-- __ -->
### <a id="output_files"></a><span data-ttu-id="f5539-130">Output files</span><span class="sxs-lookup"><span data-stu-id="f5539-130">Output files</span></span>
<span data-ttu-id="f5539-131">By default, an indexing job generates the following output files.</span><span class="sxs-lookup"><span data-stu-id="f5539-131">By default, an indexing job generates the following output files.</span></span> <span data-ttu-id="f5539-132">The files will be stored in the first output asset.</span><span class="sxs-lookup"><span data-stu-id="f5539-132">The files will be stored in the first output asset.</span></span>

<span data-ttu-id="f5539-133">When there is more than one input media file, Indexer will generate a manifest file for the job outputs, named ‘JobResult.txt’.</span><span class="sxs-lookup"><span data-stu-id="f5539-133">When there is more than one input media file, Indexer will generate a manifest file for the job outputs, named ‘JobResult.txt’.</span></span> <span data-ttu-id="f5539-134">For each input media file, the resulting AIB, SAMI, TTML, WebVTT, and keyword files, are sequentially numbered and named using the "Alias".</span><span class="sxs-lookup"><span data-stu-id="f5539-134">For each input media file, the resulting AIB, SAMI, TTML, WebVTT, and keyword files, are sequentially numbered and named using the "Alias".</span></span>

| <span data-ttu-id="f5539-135">File name</span><span class="sxs-lookup"><span data-stu-id="f5539-135">File name</span></span> | <span data-ttu-id="f5539-136">Description</span><span class="sxs-lookup"><span data-stu-id="f5539-136">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f5539-137">**InputFileName.aib**</span><span class="sxs-lookup"><span data-stu-id="f5539-137">**InputFileName.aib**</span></span> |<span data-ttu-id="f5539-138">Audio indexing blob file.</span><span class="sxs-lookup"><span data-stu-id="f5539-138">Audio indexing blob file.</span></span> <br/><br/> <span data-ttu-id="f5539-139">Audio Indexing Blob (AIB) file is a binary file that can be searched in Microsoft SQL server using full text search.</span><span class="sxs-lookup"><span data-stu-id="f5539-139">Audio Indexing Blob (AIB) file is a binary file that can be searched in Microsoft SQL server using full text search.</span></span>  <span data-ttu-id="f5539-140">The AIB file is more powerful than the simple caption files, because it contains alternatives for each word, allowing a much richer search experience.</span><span class="sxs-lookup"><span data-stu-id="f5539-140">The AIB file is more powerful than the simple caption files, because it contains alternatives for each word, allowing a much richer search experience.</span></span> <br/> <br/><span data-ttu-id="f5539-141">It requires the installation of the Indexer SQL add-on on a machine running Microsoft SQL server 2008 or later.</span><span class="sxs-lookup"><span data-stu-id="f5539-141">It requires the installation of the Indexer SQL add-on on a machine running Microsoft SQL server 2008 or later.</span></span> <span data-ttu-id="f5539-142">Searching the AIB using Microsoft SQL server full text search provides more accurate search results than searching the closed caption files generated by WAMI.</span><span class="sxs-lookup"><span data-stu-id="f5539-142">Searching the AIB using Microsoft SQL server full text search provides more accurate search results than searching the closed caption files generated by WAMI.</span></span> <span data-ttu-id="f5539-143">This is because the AIB contains word alternatives which sound similar whereas the closed caption files contain the highest confidence word for each segment of the audio.</span><span class="sxs-lookup"><span data-stu-id="f5539-143">This is because the AIB contains word alternatives which sound similar whereas the closed caption files contain the highest confidence word for each segment of the audio.</span></span> <span data-ttu-id="f5539-144">If searching for spoken words is of upmost importance, then it is recommended to use the AIB In conjunction with Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f5539-144">If searching for spoken words is of upmost importance, then it is recommended to use the AIB In conjunction with Microsoft SQL Server.</span></span><br/><br/> <span data-ttu-id="f5539-145">To download the add-on, click <a href="http://aka.ms/indexersql">Azure Media Indexer SQL Add-on</a>.</span><span class="sxs-lookup"><span data-stu-id="f5539-145">To download the add-on, click <a href="http://aka.ms/indexersql">Azure Media Indexer SQL Add-on</a>.</span></span> <br/><br/><span data-ttu-id="f5539-146">It is also possible to utilize other search engines such as Apache Lucene/Solr to simply index the video based on the closed caption and keyword XML files, but this will result in less accurate search results.</span><span class="sxs-lookup"><span data-stu-id="f5539-146">It is also possible to utilize other search engines such as Apache Lucene/Solr to simply index the video based on the closed caption and keyword XML files, but this will result in less accurate search results.</span></span> |
| <span data-ttu-id="f5539-147">**InputFileName.smi**</span><span class="sxs-lookup"><span data-stu-id="f5539-147">**InputFileName.smi**</span></span><br/><span data-ttu-id="f5539-148">**InputFileName.ttml**</span><span class="sxs-lookup"><span data-stu-id="f5539-148">**InputFileName.ttml**</span></span><br/><span data-ttu-id="f5539-149">**InputFileName.vtt**</span><span class="sxs-lookup"><span data-stu-id="f5539-149">**InputFileName.vtt**</span></span> |<span data-ttu-id="f5539-150">Closed Caption (CC) files in SAMI, TTML, and WebVTT formats.</span><span class="sxs-lookup"><span data-stu-id="f5539-150">Closed Caption (CC) files in SAMI, TTML, and WebVTT formats.</span></span><br/><br/><span data-ttu-id="f5539-151">They can be used to make audio and video files accessible to people with hearing disability.</span><span class="sxs-lookup"><span data-stu-id="f5539-151">They can be used to make audio and video files accessible to people with hearing disability.</span></span><br/><br/><span data-ttu-id="f5539-152">Closed Caption files include a tag called <b>Recognizability</b> which scores an indexing job based on how recognizable the speech in the source video is.</span><span class="sxs-lookup"><span data-stu-id="f5539-152">Closed Caption files include a tag called <b>Recognizability</b> which scores an indexing job based on how recognizable the speech in the source video is.</span></span>  <span data-ttu-id="f5539-153">You can use the value of <b>Recognizability</b> to screen output files for usability.</span><span class="sxs-lookup"><span data-stu-id="f5539-153">You can use the value of <b>Recognizability</b> to screen output files for usability.</span></span> <span data-ttu-id="f5539-154">A low score would mean poor indexing results due to audio quality.</span><span class="sxs-lookup"><span data-stu-id="f5539-154">A low score would mean poor indexing results due to audio quality.</span></span> |
| <span data-ttu-id="f5539-155">**InputFileName.kw.xml<br/>InputFileName.info**</span><span class="sxs-lookup"><span data-stu-id="f5539-155">**InputFileName.kw.xml<br/>InputFileName.info**</span></span> |<span data-ttu-id="f5539-156">Keyword and info files.</span><span class="sxs-lookup"><span data-stu-id="f5539-156">Keyword and info files.</span></span> <br/><br/><span data-ttu-id="f5539-157">Keyword file is an XML file that contains keywords extracted from the speech content, with frequency and offset information.</span><span class="sxs-lookup"><span data-stu-id="f5539-157">Keyword file is an XML file that contains keywords extracted from the speech content, with frequency and offset information.</span></span> <br/><br/><span data-ttu-id="f5539-158">Info file is a plain-text file which contains granular information about each term recognized.</span><span class="sxs-lookup"><span data-stu-id="f5539-158">Info file is a plain-text file which contains granular information about each term recognized.</span></span> <span data-ttu-id="f5539-159">The first line is special and contains the Recognizability score.</span><span class="sxs-lookup"><span data-stu-id="f5539-159">The first line is special and contains the Recognizability score.</span></span> <span data-ttu-id="f5539-160">Each subsequent line is a tab-separated list of the following data: start time, end time, word/phrase, confidence.</span><span class="sxs-lookup"><span data-stu-id="f5539-160">Each subsequent line is a tab-separated list of the following data: start time, end time, word/phrase, confidence.</span></span> <span data-ttu-id="f5539-161">The times are given in seconds and the confidence is given as a number from 0-1.</span><span class="sxs-lookup"><span data-stu-id="f5539-161">The times are given in seconds and the confidence is given as a number from 0-1.</span></span> <br/><br/><span data-ttu-id="f5539-162">Example line: "1.20    1.45    word    0.67"</span><span class="sxs-lookup"><span data-stu-id="f5539-162">Example line: "1.20    1.45    word    0.67"</span></span> <br/><br/><span data-ttu-id="f5539-163">These files can be used for a number of purposes, such as, to perform speech analytics, or exposed to search engines such as Bing, Google or Microsoft SharePoint to make the media files more discoverable, or even used to deliver more relevant ads.</span><span class="sxs-lookup"><span data-stu-id="f5539-163">These files can be used for a number of purposes, such as, to perform speech analytics, or exposed to search engines such as Bing, Google or Microsoft SharePoint to make the media files more discoverable, or even used to deliver more relevant ads.</span></span> |
| <span data-ttu-id="f5539-164">**JobResult.txt**</span><span class="sxs-lookup"><span data-stu-id="f5539-164">**JobResult.txt**</span></span> |<span data-ttu-id="f5539-165">Output manifest, present only when indexing multiple files, containing the following information:</span><span class="sxs-lookup"><span data-stu-id="f5539-165">Output manifest, present only when indexing multiple files, containing the following information:</span></span><br/><br/><table border="1"><tr><th><span data-ttu-id="f5539-166">InputFile</span><span class="sxs-lookup"><span data-stu-id="f5539-166">InputFile</span></span></th><th><span data-ttu-id="f5539-167">Alias</span><span class="sxs-lookup"><span data-stu-id="f5539-167">Alias</span></span></th><th><span data-ttu-id="f5539-168">MediaLength</span><span class="sxs-lookup"><span data-stu-id="f5539-168">MediaLength</span></span></th><th><span data-ttu-id="f5539-169">Error</span><span class="sxs-lookup"><span data-stu-id="f5539-169">Error</span></span></th></tr><tr><td><span data-ttu-id="f5539-170">a.mp4</span><span class="sxs-lookup"><span data-stu-id="f5539-170">a.mp4</span></span></td><td><span data-ttu-id="f5539-171">Media_1</span><span class="sxs-lookup"><span data-stu-id="f5539-171">Media_1</span></span></td><td><span data-ttu-id="f5539-172">300</span><span class="sxs-lookup"><span data-stu-id="f5539-172">300</span></span></td><td><span data-ttu-id="f5539-173">0</span><span class="sxs-lookup"><span data-stu-id="f5539-173">0</span></span></td></tr><tr><td><span data-ttu-id="f5539-174">b.mp4</span><span class="sxs-lookup"><span data-stu-id="f5539-174">b.mp4</span></span></td><td><span data-ttu-id="f5539-175">Media_2</span><span class="sxs-lookup"><span data-stu-id="f5539-175">Media_2</span></span></td><td><span data-ttu-id="f5539-176">0</span><span class="sxs-lookup"><span data-stu-id="f5539-176">0</span></span></td><td><span data-ttu-id="f5539-177">3000</span><span class="sxs-lookup"><span data-stu-id="f5539-177">3000</span></span></td></tr><tr><td><span data-ttu-id="f5539-178">c.mp4</span><span class="sxs-lookup"><span data-stu-id="f5539-178">c.mp4</span></span></td><td><span data-ttu-id="f5539-179">Media_3</span><span class="sxs-lookup"><span data-stu-id="f5539-179">Media_3</span></span></td><td><span data-ttu-id="f5539-180">600</span><span class="sxs-lookup"><span data-stu-id="f5539-180">600</span></span></td><td><span data-ttu-id="f5539-181">0</span><span class="sxs-lookup"><span data-stu-id="f5539-181">0</span></span></td></tr></table><br/> |

<span data-ttu-id="f5539-182">If not all input media files are indexed successfully, the indexing job will fail with error code 4000.</span><span class="sxs-lookup"><span data-stu-id="f5539-182">If not all input media files are indexed successfully, the indexing job will fail with error code 4000.</span></span> <span data-ttu-id="f5539-183">For more information, see [Error codes](#error_codes).</span><span class="sxs-lookup"><span data-stu-id="f5539-183">For more information, see [Error codes](#error_codes).</span></span>

## <a name="index-multiple-files"></a><span data-ttu-id="f5539-184">Index multiple files</span><span class="sxs-lookup"><span data-stu-id="f5539-184">Index multiple files</span></span>
<span data-ttu-id="f5539-185">The following method uploads multiple media files as an asset, and creates a job to index all these files in a batch.</span><span class="sxs-lookup"><span data-stu-id="f5539-185">The following method uploads multiple media files as an asset, and creates a job to index all these files in a batch.</span></span>

<span data-ttu-id="f5539-186">A manifest file with the .lst extension is created and uploading into the asset.</span><span class="sxs-lookup"><span data-stu-id="f5539-186">A manifest file with the .lst extension is created and uploading into the asset.</span></span> <span data-ttu-id="f5539-187">The manifest file contains the list of all the asset files.</span><span class="sxs-lookup"><span data-stu-id="f5539-187">The manifest file contains the list of all the asset files.</span></span> <span data-ttu-id="f5539-188">For more information, see [Task Preset for Azure Media Indexer](https://msdn.microsoft.com/library/dn783454.aspx).</span><span class="sxs-lookup"><span data-stu-id="f5539-188">For more information, see [Task Preset for Azure Media Indexer](https://msdn.microsoft.com/library/dn783454.aspx).</span></span>

    static bool RunBatchIndexingJob(string[] inputMediaFiles, string outputFolder)
    {
        // Create an asset and upload to storage.
        IAsset asset = CreateAssetAndUploadMultipleFiles(inputMediaFiles,
            "My Indexing Input Asset - Batch Mode",
            AssetCreationOptions.None);

        // Create a manifest file that contains all the asset file names and upload to storage.
        string manifestFile = "input.lst";            
        File.WriteAllLines(manifestFile, asset.AssetFiles.Select(f => f.Name).ToArray());
        var assetFile = asset.AssetFiles.Create(Path.GetFileName(manifestFile));
        assetFile.Upload(manifestFile);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job - Batch Mode");

        // Get a reference to the Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration.
        string configuration = File.ReadAllText("batch.config");

        // Create a task with the encoding details, using a string preset.
        ITask task = job.Tasks.AddNew("My Indexing Task - Batch Mode",
            processor,
            configuration,
            TaskOptions.None);

        // Specify the input asset to be indexed.
        task.InputAssets.Add(asset);

        // Add an output asset to contain the results of the job.
        task.OutputAssets.AddNew("My Indexing Output Asset - Batch Mode", AssetCreationOptions.None);

        // Use the following event handler to check job progress.  
        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

        // Launch the job.
        job.Submit();

        // Check job execution and wait for job to finish.
        Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
        progressJobTask.Wait();

        // If job state is Error, the event handling
        // method for job progress should log errors.  Here we check
        // for error state and exit if needed.
        if (job.State == JobState.Error)
        {
            Console.WriteLine("Exiting method due to job error.");
            return false;
        }

        // Download the job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
    }

    private static IAsset CreateAssetAndUploadMultipleFiles(string[] filePaths, string assetName, AssetCreationOptions options)
    {
        IAsset asset = _context.Assets.Create(assetName, options);

        foreach (string filePath in filePaths)
        {
            var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
            assetFile.Upload(filePath);
        }

        return asset;
    }

### <a name="partially-succeeded-job"></a><span data-ttu-id="f5539-189">Partially Succeeded Job</span><span class="sxs-lookup"><span data-stu-id="f5539-189">Partially Succeeded Job</span></span>
<span data-ttu-id="f5539-190">If not all input media files are indexed successfully, the indexing job will fail with error code 4000.</span><span class="sxs-lookup"><span data-stu-id="f5539-190">If not all input media files are indexed successfully, the indexing job will fail with error code 4000.</span></span> <span data-ttu-id="f5539-191">For more information, see [Error codes](#error_codes).</span><span class="sxs-lookup"><span data-stu-id="f5539-191">For more information, see [Error codes](#error_codes).</span></span>

<span data-ttu-id="f5539-192">The same outputs (as succeeded jobs) are generated.</span><span class="sxs-lookup"><span data-stu-id="f5539-192">The same outputs (as succeeded jobs) are generated.</span></span> <span data-ttu-id="f5539-193">You can refer to the output manifest file to find out which input files are failed, according to the Error column values.</span><span class="sxs-lookup"><span data-stu-id="f5539-193">You can refer to the output manifest file to find out which input files are failed, according to the Error column values.</span></span> <span data-ttu-id="f5539-194">For input files that failed, the resulting AIB, SAMI, TTML, WebVTT and keyword files will NOT be generated.</span><span class="sxs-lookup"><span data-stu-id="f5539-194">For input files that failed, the resulting AIB, SAMI, TTML, WebVTT and keyword files will NOT be generated.</span></span>

### <a id="preset"></a> <span data-ttu-id="f5539-195">Task Preset for Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="f5539-195">Task Preset for Azure Media Indexer</span></span>
<span data-ttu-id="f5539-196">The processing from Azure Media Indexer can be customized by providing an optional task preset alongside the task.</span><span class="sxs-lookup"><span data-stu-id="f5539-196">The processing from Azure Media Indexer can be customized by providing an optional task preset alongside the task.</span></span>  <span data-ttu-id="f5539-197">The following describes the format of this configuration xml.</span><span class="sxs-lookup"><span data-stu-id="f5539-197">The following describes the format of this configuration xml.</span></span>

| <span data-ttu-id="f5539-198">Name</span><span class="sxs-lookup"><span data-stu-id="f5539-198">Name</span></span> | <span data-ttu-id="f5539-199">Require</span><span class="sxs-lookup"><span data-stu-id="f5539-199">Require</span></span> | <span data-ttu-id="f5539-200">Description</span><span class="sxs-lookup"><span data-stu-id="f5539-200">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5539-201">**input**</span><span class="sxs-lookup"><span data-stu-id="f5539-201">**input**</span></span> |<span data-ttu-id="f5539-202">false</span><span class="sxs-lookup"><span data-stu-id="f5539-202">false</span></span> |<span data-ttu-id="f5539-203">Asset file(s) that you want to index.</span><span class="sxs-lookup"><span data-stu-id="f5539-203">Asset file(s) that you want to index.</span></span></p><p><span data-ttu-id="f5539-204">Azure Media Indexer supports the following media file formats: MP4, WMV, MP3, M4A, WMA, AAC, WAV.</span><span class="sxs-lookup"><span data-stu-id="f5539-204">Azure Media Indexer supports the following media file formats: MP4, WMV, MP3, M4A, WMA, AAC, WAV.</span></span></p><p><span data-ttu-id="f5539-205">You can specify the file name (s) in the **name** or **list** attribute of the **input** element (as shown below).If you do not specify which asset file to index, the primary file is picked.</span><span class="sxs-lookup"><span data-stu-id="f5539-205">You can specify the file name (s) in the **name** or **list** attribute of the **input** element (as shown below).If you do not specify which asset file to index, the primary file is picked.</span></span> <span data-ttu-id="f5539-206">If no primary asset file is set, the first file in the input asset is indexed.</span><span class="sxs-lookup"><span data-stu-id="f5539-206">If no primary asset file is set, the first file in the input asset is indexed.</span></span></p><p><span data-ttu-id="f5539-207">To explicitly specify the asset file name, do:</span><span class="sxs-lookup"><span data-stu-id="f5539-207">To explicitly specify the asset file name, do:</span></span><br/>`<input name="TestFile.wmv">`<br/><br/><span data-ttu-id="f5539-208">You can also index multiple asset files at once (up to 10 files).</span><span class="sxs-lookup"><span data-stu-id="f5539-208">You can also index multiple asset files at once (up to 10 files).</span></span> <span data-ttu-id="f5539-209">To do this:</span><span class="sxs-lookup"><span data-stu-id="f5539-209">To do this:</span></span><br/><br/><ol class="ordered"><li><p><span data-ttu-id="f5539-210">Create a text file (manifest file) and give it an .lst extension.</span><span class="sxs-lookup"><span data-stu-id="f5539-210">Create a text file (manifest file) and give it an .lst extension.</span></span> </p></li><li><p><span data-ttu-id="f5539-211">Add a list of all the asset file names in your input asset to this manifest file.</span><span class="sxs-lookup"><span data-stu-id="f5539-211">Add a list of all the asset file names in your input asset to this manifest file.</span></span> </p></li><li><p><span data-ttu-id="f5539-212">Add (upload) thanifest file to the asset.</span><span class="sxs-lookup"><span data-stu-id="f5539-212">Add (upload) thanifest file to the asset.</span></span>  </p></li><li><p><span data-ttu-id="f5539-213">Specify the name of the manifest file in the input’s list attribute.</span><span class="sxs-lookup"><span data-stu-id="f5539-213">Specify the name of the manifest file in the input’s list attribute.</span></span><br/>`<input list="input.lst">`</li></ol><br/><br/><span data-ttu-id="f5539-214">Note: If you add more than 10 files to the manifest file, the indexing job will fail with the 2006 error code.</span><span class="sxs-lookup"><span data-stu-id="f5539-214">Note: If you add more than 10 files to the manifest file, the indexing job will fail with the 2006 error code.</span></span> |
| <span data-ttu-id="f5539-215">**metadata**</span><span class="sxs-lookup"><span data-stu-id="f5539-215">**metadata**</span></span> |<span data-ttu-id="f5539-216">false</span><span class="sxs-lookup"><span data-stu-id="f5539-216">false</span></span> |<span data-ttu-id="f5539-217">Metadata for the specified asset file(s) used for Vocabulary Adaptation.</span><span class="sxs-lookup"><span data-stu-id="f5539-217">Metadata for the specified asset file(s) used for Vocabulary Adaptation.</span></span>  <span data-ttu-id="f5539-218">Useful to prepare Indexer to recognize non-standard vocabulary words such as proper nouns.</span><span class="sxs-lookup"><span data-stu-id="f5539-218">Useful to prepare Indexer to recognize non-standard vocabulary words such as proper nouns.</span></span><br/>`<metadata key="..." value="..."/>` <br/><br/><span data-ttu-id="f5539-219">You can supply **values** for predefined **keys**.</span><span class="sxs-lookup"><span data-stu-id="f5539-219">You can supply **values** for predefined **keys**.</span></span> <span data-ttu-id="f5539-220">Currently the following keys are supported:</span><span class="sxs-lookup"><span data-stu-id="f5539-220">Currently the following keys are supported:</span></span><br/><br/><span data-ttu-id="f5539-221">“title” and “description” - used for vocabulary adaptation to tweak the language model for your job and improve speech recognition accuracy.</span><span class="sxs-lookup"><span data-stu-id="f5539-221">“title” and “description” - used for vocabulary adaptation to tweak the language model for your job and improve speech recognition accuracy.</span></span>  <span data-ttu-id="f5539-222">The values seed Internet searches to find contextually relevant text documents, using the contents to augment the internal dictionary for the duration of your Indexing task.</span><span class="sxs-lookup"><span data-stu-id="f5539-222">The values seed Internet searches to find contextually relevant text documents, using the contents to augment the internal dictionary for the duration of your Indexing task.</span></span><br/>`<metadata key="title" value="[Title of the media file]" />`<br/>`<metadata key="description" value="[Description of the media file] />"` |
| <span data-ttu-id="f5539-223">**features**</span><span class="sxs-lookup"><span data-stu-id="f5539-223">**features**</span></span> <br/><br/> <span data-ttu-id="f5539-224">Added in version 1.2.</span><span class="sxs-lookup"><span data-stu-id="f5539-224">Added in version 1.2.</span></span> <span data-ttu-id="f5539-225">Currently, the only supported feature is speech recognition ("ASR").</span><span class="sxs-lookup"><span data-stu-id="f5539-225">Currently, the only supported feature is speech recognition ("ASR").</span></span> |<span data-ttu-id="f5539-226">false</span><span class="sxs-lookup"><span data-stu-id="f5539-226">false</span></span> |<span data-ttu-id="f5539-227">The Speech Recognition feature has the following settings keys:</span><span class="sxs-lookup"><span data-stu-id="f5539-227">The Speech Recognition feature has the following settings keys:</span></span><table><tr><th><p><span data-ttu-id="f5539-228">Key</span><span class="sxs-lookup"><span data-stu-id="f5539-228">Key</span></span></p></th>        <th><p><span data-ttu-id="f5539-229">Description</span><span class="sxs-lookup"><span data-stu-id="f5539-229">Description</span></span></p></th><th><p><span data-ttu-id="f5539-230">Example value</span><span class="sxs-lookup"><span data-stu-id="f5539-230">Example value</span></span></p></th></tr><tr><td><p><span data-ttu-id="f5539-231">Language</span><span class="sxs-lookup"><span data-stu-id="f5539-231">Language</span></span></p></td><td><p><span data-ttu-id="f5539-232">The natural language to be recognized in the multimedia file.</span><span class="sxs-lookup"><span data-stu-id="f5539-232">The natural language to be recognized in the multimedia file.</span></span></p></td><td><p><span data-ttu-id="f5539-233">English, Spanish</span><span class="sxs-lookup"><span data-stu-id="f5539-233">English, Spanish</span></span></p></td></tr><tr><td><p><span data-ttu-id="f5539-234">CaptionFormats</span><span class="sxs-lookup"><span data-stu-id="f5539-234">CaptionFormats</span></span></p></td><td><p><span data-ttu-id="f5539-235">a semicolon-separated list of the desired output caption formats (if any)</span><span class="sxs-lookup"><span data-stu-id="f5539-235">a semicolon-separated list of the desired output caption formats (if any)</span></span></p></td><td><p><span data-ttu-id="f5539-236">ttml;sami;webvtt</span><span class="sxs-lookup"><span data-stu-id="f5539-236">ttml;sami;webvtt</span></span></p></td></tr><tr><td><p><span data-ttu-id="f5539-237">GenerateAIB</span><span class="sxs-lookup"><span data-stu-id="f5539-237">GenerateAIB</span></span></p></td><td><p><span data-ttu-id="f5539-238">A boolean flag specifying whether or not an AIB file is required (for use with SQL Server and the customer Indexer IFilter).</span><span class="sxs-lookup"><span data-stu-id="f5539-238">A boolean flag specifying whether or not an AIB file is required (for use with SQL Server and the customer Indexer IFilter).</span></span>  <span data-ttu-id="f5539-239">For more information, see <a href="http://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/">Using AIB Files with Azure Media Indexer and SQL Server</a>.</span><span class="sxs-lookup"><span data-stu-id="f5539-239">For more information, see <a href="http://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/">Using AIB Files with Azure Media Indexer and SQL Server</a>.</span></span></p></td><td><p><span data-ttu-id="f5539-240">True; False</span><span class="sxs-lookup"><span data-stu-id="f5539-240">True; False</span></span></p></td></tr><tr><td><p><span data-ttu-id="f5539-241">GenerateKeywords</span><span class="sxs-lookup"><span data-stu-id="f5539-241">GenerateKeywords</span></span></p></td><td><p><span data-ttu-id="f5539-242">A boolean flag specifying whether or not a keyword XML file is required.</span><span class="sxs-lookup"><span data-stu-id="f5539-242">A boolean flag specifying whether or not a keyword XML file is required.</span></span></p></td><td><p><span data-ttu-id="f5539-243">True; False.</span><span class="sxs-lookup"><span data-stu-id="f5539-243">True; False.</span></span> </p></td></tr><tr><td><p><span data-ttu-id="f5539-244">ForceFullCaption</span><span class="sxs-lookup"><span data-stu-id="f5539-244">ForceFullCaption</span></span></p></td><td><p><span data-ttu-id="f5539-245">A boolean flag specifying whether or not to force full captions (regardless of confidence level).</span><span class="sxs-lookup"><span data-stu-id="f5539-245">A boolean flag specifying whether or not to force full captions (regardless of confidence level).</span></span>  </p><p><span data-ttu-id="f5539-246">Default is false, in which case words and phrases which have a less than 50% confidence level are omitted from the final caption outputs and replaced by ellipses ("...").</span><span class="sxs-lookup"><span data-stu-id="f5539-246">Default is false, in which case words and phrases which have a less than 50% confidence level are omitted from the final caption outputs and replaced by ellipses ("...").</span></span>  <span data-ttu-id="f5539-247">The ellipses are useful for caption quality control and auditing.</span><span class="sxs-lookup"><span data-stu-id="f5539-247">The ellipses are useful for caption quality control and auditing.</span></span></p></td><td><p><span data-ttu-id="f5539-248">True; False.</span><span class="sxs-lookup"><span data-stu-id="f5539-248">True; False.</span></span> </p></td></tr></table> |

### <a id="error_codes"></a><span data-ttu-id="f5539-249">Error codes</span><span class="sxs-lookup"><span data-stu-id="f5539-249">Error codes</span></span>
<span data-ttu-id="f5539-250">In the case of an error, Azure Media Indexer should report back one of the following error codes:</span><span class="sxs-lookup"><span data-stu-id="f5539-250">In the case of an error, Azure Media Indexer should report back one of the following error codes:</span></span>

| <span data-ttu-id="f5539-251">Code</span><span class="sxs-lookup"><span data-stu-id="f5539-251">Code</span></span> | <span data-ttu-id="f5539-252">Name</span><span class="sxs-lookup"><span data-stu-id="f5539-252">Name</span></span> | <span data-ttu-id="f5539-253">Possible Reasons</span><span class="sxs-lookup"><span data-stu-id="f5539-253">Possible Reasons</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5539-254">2000</span><span class="sxs-lookup"><span data-stu-id="f5539-254">2000</span></span> |<span data-ttu-id="f5539-255">Invalid configuration</span><span class="sxs-lookup"><span data-stu-id="f5539-255">Invalid configuration</span></span> |<span data-ttu-id="f5539-256">Invalid configuration</span><span class="sxs-lookup"><span data-stu-id="f5539-256">Invalid configuration</span></span> |
| <span data-ttu-id="f5539-257">2001</span><span class="sxs-lookup"><span data-stu-id="f5539-257">2001</span></span> |<span data-ttu-id="f5539-258">Invalid input assets</span><span class="sxs-lookup"><span data-stu-id="f5539-258">Invalid input assets</span></span> |<span data-ttu-id="f5539-259">Missing input assets or empty asset.</span><span class="sxs-lookup"><span data-stu-id="f5539-259">Missing input assets or empty asset.</span></span> |
| <span data-ttu-id="f5539-260">2002</span><span class="sxs-lookup"><span data-stu-id="f5539-260">2002</span></span> |<span data-ttu-id="f5539-261">Invalid manifest</span><span class="sxs-lookup"><span data-stu-id="f5539-261">Invalid manifest</span></span> |<span data-ttu-id="f5539-262">Manifest is empty or manifest contains invalid items.</span><span class="sxs-lookup"><span data-stu-id="f5539-262">Manifest is empty or manifest contains invalid items.</span></span> |
| <span data-ttu-id="f5539-263">2003</span><span class="sxs-lookup"><span data-stu-id="f5539-263">2003</span></span> |<span data-ttu-id="f5539-264">Failed to download media file</span><span class="sxs-lookup"><span data-stu-id="f5539-264">Failed to download media file</span></span> |<span data-ttu-id="f5539-265">Invalid URL in manifest file.</span><span class="sxs-lookup"><span data-stu-id="f5539-265">Invalid URL in manifest file.</span></span> |
| <span data-ttu-id="f5539-266">2004</span><span class="sxs-lookup"><span data-stu-id="f5539-266">2004</span></span> |<span data-ttu-id="f5539-267">Unsupported protocol</span><span class="sxs-lookup"><span data-stu-id="f5539-267">Unsupported protocol</span></span> |<span data-ttu-id="f5539-268">Protocol of media URL is not supported.</span><span class="sxs-lookup"><span data-stu-id="f5539-268">Protocol of media URL is not supported.</span></span> |
| <span data-ttu-id="f5539-269">2005</span><span class="sxs-lookup"><span data-stu-id="f5539-269">2005</span></span> |<span data-ttu-id="f5539-270">Unsupported file type</span><span class="sxs-lookup"><span data-stu-id="f5539-270">Unsupported file type</span></span> |<span data-ttu-id="f5539-271">Input media file type is not supported.</span><span class="sxs-lookup"><span data-stu-id="f5539-271">Input media file type is not supported.</span></span> |
| <span data-ttu-id="f5539-272">2006</span><span class="sxs-lookup"><span data-stu-id="f5539-272">2006</span></span> |<span data-ttu-id="f5539-273">Too many input files</span><span class="sxs-lookup"><span data-stu-id="f5539-273">Too many input files</span></span> |<span data-ttu-id="f5539-274">There are more than 10 files in the input manifest.</span><span class="sxs-lookup"><span data-stu-id="f5539-274">There are more than 10 files in the input manifest.</span></span> |
| <span data-ttu-id="f5539-275">3000</span><span class="sxs-lookup"><span data-stu-id="f5539-275">3000</span></span> |<span data-ttu-id="f5539-276">Failed to decode media file</span><span class="sxs-lookup"><span data-stu-id="f5539-276">Failed to decode media file</span></span> |<span data-ttu-id="f5539-277">Unsupported media codec</span><span class="sxs-lookup"><span data-stu-id="f5539-277">Unsupported media codec</span></span> <br/><span data-ttu-id="f5539-278">or</span><span class="sxs-lookup"><span data-stu-id="f5539-278">or</span></span><br/> <span data-ttu-id="f5539-279">Corrupted media file</span><span class="sxs-lookup"><span data-stu-id="f5539-279">Corrupted media file</span></span> <br/><span data-ttu-id="f5539-280">or</span><span class="sxs-lookup"><span data-stu-id="f5539-280">or</span></span><br/> <span data-ttu-id="f5539-281">No audio stream in input media.</span><span class="sxs-lookup"><span data-stu-id="f5539-281">No audio stream in input media.</span></span> |
| <span data-ttu-id="f5539-282">4000</span><span class="sxs-lookup"><span data-stu-id="f5539-282">4000</span></span> |<span data-ttu-id="f5539-283">Batch indexing partially succeeded</span><span class="sxs-lookup"><span data-stu-id="f5539-283">Batch indexing partially succeeded</span></span> |<span data-ttu-id="f5539-284">Some of the input media files are failed to be indexed.</span><span class="sxs-lookup"><span data-stu-id="f5539-284">Some of the input media files are failed to be indexed.</span></span> <span data-ttu-id="f5539-285">For more information, see <a href="#output_files">Output files</a>.</span><span class="sxs-lookup"><span data-stu-id="f5539-285">For more information, see <a href="#output_files">Output files</a>.</span></span> |
| <span data-ttu-id="f5539-286">other</span><span class="sxs-lookup"><span data-stu-id="f5539-286">other</span></span> |<span data-ttu-id="f5539-287">Internal errors</span><span class="sxs-lookup"><span data-stu-id="f5539-287">Internal errors</span></span> |<span data-ttu-id="f5539-288">Please contact support team.</span><span class="sxs-lookup"><span data-stu-id="f5539-288">Please contact support team.</span></span> <span data-ttu-id="f5539-289">indexer@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="f5539-289">indexer@microsoft.com</span></span> |

## <a id="supported_languages"></a><span data-ttu-id="f5539-290">Supported Languages</span><span class="sxs-lookup"><span data-stu-id="f5539-290">Supported Languages</span></span>
<span data-ttu-id="f5539-291">Currently, the English and Spanish languages are supported.</span><span class="sxs-lookup"><span data-stu-id="f5539-291">Currently, the English and Spanish languages are supported.</span></span> <span data-ttu-id="f5539-292">For more information, see [the v1.2 release blog post](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/).</span><span class="sxs-lookup"><span data-stu-id="f5539-292">For more information, see [the v1.2 release blog post](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="f5539-293">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="f5539-293">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f5539-294">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="f5539-294">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="f5539-295">Related links</span><span class="sxs-lookup"><span data-stu-id="f5539-295">Related links</span></span>
[<span data-ttu-id="f5539-296">Azure Media Services Analytics Overview</span><span class="sxs-lookup"><span data-stu-id="f5539-296">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="f5539-297">Using AIB Files with Azure Media Indexer and SQL Server</span><span class="sxs-lookup"><span data-stu-id="f5539-297">Using AIB Files with Azure Media Indexer and SQL Server</span></span>](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/)

[<span data-ttu-id="f5539-298">Indexing Media Files with Azure Media Indexer 2 Preview</span><span class="sxs-lookup"><span data-stu-id="f5539-298">Indexing Media Files with Azure Media Indexer 2 Preview</span></span>](media-services-process-content-with-indexer2.md)

