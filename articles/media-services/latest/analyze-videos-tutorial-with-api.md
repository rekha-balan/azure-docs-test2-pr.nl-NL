---
title: Analyze videos with Azure Media Services | Microsoft Docs
description: Follow the steps of this tutorial to analyze videos using Azure Media Services.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: tutorial
ms.custom: mvc
ms.date: 06/28/2018
ms.author: juliako
ms.openlocfilehash: 314ffce8a9f8dde62cac670099afbc2223df37e4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864837"
---
# <a name="tutorial-analyze-videos-with-azure-media-services"></a>Tutorial: Analyze videos with Azure Media Services 

This tutorial shows you how to analyze videos with Azure Media Services. There are many scenarios in which you might want to gain deep insights into recorded videos or audio content. For example, to achieve higher customer satisfaction, organizations can run speech-to-text processing to convert customer support recordings into a searchable catalog, with indexes and dashboards. Then, they can obtain insights into their business such as a list of common complaints, sources of such complaints, etc.

This tutorial shows you how to:    

> [!div class="checklist"]
> * Create a Media Services account
> * Access the Media Services API
> * Configure the sample app
> * Examine the code that analyzes the specified video
> * Run the app
> * Examine the output
> * Clean up resources

> [!Note]
> Use the Azure portal, as described in [Scaling media processing](../previous/media-services-scale-media-processing-overview.md), to set your Media Services account to 10 S3 Media Reserved Units.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a>Prerequisites

If you do not have Visual Studio installed, you can get [Visual Studio Community 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).

## <a name="download-the-sample"></a>Download the sample

Clone a GitHub repository that contains the .NET sample to your machine using the following command:  

 ```bash
 git clone https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials.git
 ```

The sample is located in the [AnalyzeVideos](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/tree/master/AMSV3Tutorials/AnalyzeVideos) folder.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [media-services-cli-create-v3-account-include](../../../includes/media-services-cli-create-v3-account-include.md)]

[!INCLUDE [media-services-v3-cli-access-api-include](../../../includes/media-services-v3-cli-access-api-include.md)]

## <a name="examine-the-code-that-analyzes-the-specified-video"></a>Examine the code that analyzes the specified video

This section examines functions defined in the [Program.cs](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials/blob/master/AMSV3Tutorials/AnalyzeVideos/Program.cs) file of the *AnalyzeVideos* project.

The sample performs the following actions:

1. Creates a transform and a job that analyzes your video.
2. Creates an input asset and uploads the video into it. The asset is used as the job's input.
3. Creates an output asset that stores the job's output. 
4. Submits the job.
5. Checks the job's status.
6. Downloads the files that resulted from running the job. 

### <a name="start-using-media-services-apis-with-net-sdk"></a>Start using Media Services APIs with .NET SDK

To start using Media Services APIs with .NET, you need to create an **AzureMediaServicesClient** object. To create the object, you need to supply credentials needed for the client to connect to Azure using Azure AD. In the code you cloned at the beginning of the article, the **GetCredentialsAsync** function creates the ServiceClientCredentials object based on the credentials supplied in local configuration file. 

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#CreateMediaServicesClient)]

### <a name="create-an-input-asset-and-upload-a-local-file-into-it"></a>Create an input asset and upload a local file into it 

The **CreateInputAsset** function creates a new input [Asset](https://docs.microsoft.com/rest/api/media/assets) and uploads the specified local video file into it. This Asset is used as the input to your encoding Job. In Media Services v3, the input to a Job can either be an Asset, or it can be content that you make available to your Media Services account via HTTPS URLs. If you want to learn how to encode from a HTTPS URL, see [this](job-input-from-http-how-to.md) article.  

In Media Services v3, you use Azure Storage APIs to upload files. The following .NET snippet shows how.

The following function performs these actions:

* Creates an Asset 
* Gets a writable [SAS URL](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1) to the Asset’s [container in storage](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-dotnet?tabs=windows#upload-blobs-to-the-container)
* Uploads the file into the container in storage using the SAS URL

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#CreateInputAsset)]

### <a name="create-an-output-asset-to-store-the-result-of-the-job"></a>Create an output asset to store the result of the job 

The output [Asset](https://docs.microsoft.com/rest/api/media/assets) stores the result of your job. The project defines the **DownloadResults** function that downloads the results from this output asset into the "output" folder, so you can see what you got.

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#CreateOutputAsset)]

### <a name="create-a-transform-and-a-job-that-analyzes-videos"></a>Create a transform and a job that analyzes videos

When encoding or processing content in Media Services, it is a common pattern to set up the encoding settings as a recipe. You would then submit a **Job** to apply that recipe to a video. By submitting new Jobs for each new video, you are applying that recipe to all the videos in your library. A recipe in Media Services is called as a **Transform**. For more information, see [Transforms and jobs](transform-concept.md). The sample described in this tutorial defines a recipe that analyzes the specified video. 

#### <a name="transform"></a>Transform

When creating a new [Transform](https://docs.microsoft.com/rest/api/media/transforms) instance, you need to specify what you want it to produce as an output. The required parameter is a **TransformOutput** object, as shown in the code above. Each **TransformOutput** contains a **Preset**. **Preset** describes step-by-step instructions of video and/or audio processing operations that are to be used to generate the desired **TransformOutput**. In this example, the **VideoAnalyzerPreset** preset is used and the language ("en-US") is passed to its constructor. This preset enables you to extract multiple audio and video insights from a video. You can use the **AudioAnalyzerPreset** preset if you need to extract multiple audio insights from a video. 

When creating a **Transform**, you should first check if one already exists using the **Get** method, as shown in the code that follows.  In Media Services v3, **Get** methods on entities return **null** if the entity doesn’t exist (a case-insensitive check on the name).

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#EnsureTransformExists)]

#### <a name="job"></a>Job

As mentioned above, the [Transform](https://docs.microsoft.com/rest/api/media/transforms) object is the recipe and a [Job](https://docs.microsoft.com/rest/api/media/jobs) is the actual request to Media Services to apply that **Transform** to a given input video or audio content. The **Job** specifies information like the location of the input video, and the location for the output. You can specify the location of your video using: HTTPS URLs, SAS URLs, or Assets that are in your Media Service account. 

In this example, the job input is a local video.  

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#SubmitJob)]

### <a name="wait-for-the-job-to-complete"></a>Wait for the job to complete

The job takes some time to complete and when it does you want to be notified. There are different options to get notified about the [Job](https://docs.microsoft.com/rest/api/media/jobs) completion. The simplest option (that is shown here) is to use polling. 

Polling is not a recommended best practice for production applications because of potential latency. Polling can be throttled if overused on an account. Developers should instead use Event Grid.

Event Grid is designed for high availability, consistent performance, and dynamic scale. With Event Grid, your apps can listen for and react to events from virtually all Azure services, as well as custom sources. Simple, HTTP-based reactive event handling helps you build efficient solutions through intelligent filtering and routing of events. See [Route events to a custom web endpoint](job-state-events-cli-how-to.md).

The **Job** usually goes through the following states: **Scheduled**, **Queued**, **Processing**, **Finished** (the final state). If the job has encountered an error, you get the **Error** state. If the job is in the process of being canceled, you get **Canceling** and **Canceled** when it is done.

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#WaitForJobToFinish)]

### <a name="download-the-result-of-the-job"></a>Download the result of the job

The following function downloads the results from the output [Asset](https://docs.microsoft.com/rest/api/media/assets) into the "output" folder, so you can examine the results of the job. 

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#DownloadResults)]

### <a name="clean-up-resource-in-your-media-services-account"></a>Clean up resource in your Media Services account

Generally, you should clean up everything except objects that you are planning to reuse (typically, you will reuse Transforms and  persist StreamingLocators). If you want for your account to be clean after experimenting, you should delete the resources that you do not plan to reuse. For example, the following code deletes Jobs.

[!code-csharp[Main](../../../media-services-v3-dotnet-tutorials/AMSV3Tutorials/AnalyzeVideos/Program.cs#CleanUp)]

## <a name="run-the-sample-app"></a>Run the sample app

Press Ctrl+F5 to run the *AnalyzeVideos* application.

When we run the program, the job produces thumbnails for each face that it finds in the video. It also produces the insights.json file.

## <a name="examine-the-output"></a>Examine the output

The output file of analyzing videos is called insights.json. This file contains insights about your video. You can find description of  elements found in the json file in the [Media intelligence](intelligence-concept.md) article.

## <a name="clean-up-resources"></a>Clean up resources

If you no longer need any of the resources in your resource group, including the Media Services and storage accounts you created for this tutorial, delete the resource group you created earlier. You can use the **CloudShell** tool.

In the **CloudShell**, execute the following command:

```azurecli-interactive
az group delete --name amsResourceGroup
```

## <a name="multithreading"></a>Multithreading

The Azure Media Services v3 SDKs are not thread-safe. When working with multi-threaded application, you should generate a new  AzureMediaServicesClient object per thread.

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Tutorial: upload, encode, and stream files](stream-files-tutorial-with-api.md)
