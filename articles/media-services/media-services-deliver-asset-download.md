---
title: Download Media Services assets to your computer - Azure | Microsoft Docs
description: Learn about to download assets to your computer. Code samples are written in C# and use the Media Services SDK for .NET.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: 8908a1dd-3ffb-4f18-955d-4c8e2d82fc5d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: 19f6ea37f892054ee5d7bf793a32364dff264058
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556245"
---
# <a name="how-to-deliver-an-asset-by-download"></a>How to: Deliver an Asset by Download
This topic discusses options for delivering media assets uploaded to Media Services. You can deliver Media Services content in numerous application scenarios. You can download media assets, or access them by using a locator. You can send media content to another application or to another content provider. For improved performance and scalability, you can also deliver content by using a Content Delivery Network (CDN).

This example shows how to download media assets from Media Services to your local computer. The code queries the jobs associated with the Media Services account by job ID and accesses its **OutputMediaAssets** collection (which is the set of one or more output media assets that results from running a job). This  example shows how to download output media assets from a job, but you can apply the same approach to download other assets.

>[!NOTE]
>There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy). You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies). For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.

    // Download the output asset of the specified job to a local folder.
    static IAsset DownloadAssetToLocal( string jobId, string outputFolder)
    {
        // This method illustrates how to download a single asset. 
        // However, you can iterate through the OutputAssets
        // collection, and download all assets if there are many. 

        // Get a reference to the job. 
        IJob job = GetJob(jobId);

        // Get a reference to the first output asset. If there were multiple 
        // output media assets you could iterate and handle each one.
        IAsset outputAsset = job.OutputMediaAssets[0];

        // Create a SAS locator to download the asset
        IAccessPolicy accessPolicy = _context.AccessPolicies.Create("File Download Policy", TimeSpan.FromDays(30), AccessPermissions.Read);
        ILocator locator = _context.Locators.CreateLocator(LocatorType.Sas, outputAsset, accessPolicy);

        BlobTransferClient blobTransfer = new BlobTransferClient
        {
            NumberOfConcurrentTransfers = 20,
            ParallelTransferThreadCount = 20
        };

        var downloadTasks = new List<Task>();
        foreach (IAssetFile outputFile in outputAsset.AssetFiles)
        {
            // Use the following event handler to check download progress.
            outputFile.DownloadProgressChanged += DownloadProgress;

            string localDownloadPath = Path.Combine(outputFolder, outputFile.Name);

            Console.WriteLine("File download path:  " + localDownloadPath);

            downloadTasks.Add(outputFile.DownloadAsync(Path.GetFullPath(localDownloadPath), blobTransfer, locator, CancellationToken.None));

            outputFile.DownloadProgressChanged -= DownloadProgress;
        }

        Task.WaitAll(downloadTasks.ToArray());

        return outputAsset;
    }

    static void DownloadProgress(object sender, DownloadProgressChangedEventArgs e)
    {
        Console.WriteLine(string.Format("{0} % download progress. ", e.Progress));
    }



## <a name="media-services-learning-paths"></a>Media Services learning paths
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Provide feedback
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>See Also
[Deliver streaming content](media-services-deliver-streaming-content.md)

