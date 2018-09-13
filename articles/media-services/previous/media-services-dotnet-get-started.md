---
title: Get started with delivering content on demand using .NET | Microsoft Docs
description: This tutorial walks you through the steps of implementing an on demand content delivery application with Azure Media Services using .NET.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: 388b8928-9aa9-46b1-b60a-a918da75bd7b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 12/10/2017
ms.author: juliako
ms.openlocfilehash: 12a6f731dfb1c106c28d18caa95710751736629c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867971"
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a><span data-ttu-id="c88b9-103">Get started with delivering content on demand using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c88b9-103">Get started with delivering content on demand using .NET SDK</span></span>
[!INCLUDE [media-services-selector-get-started](../../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="c88b9-104">This tutorial walks you through the steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using the Azure Media Services .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="c88b9-104">This tutorial walks you through the steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using the Azure Media Services .NET SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c88b9-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c88b9-105">Prerequisites</span></span>

<span data-ttu-id="c88b9-106">The following are required to complete the tutorial:</span><span class="sxs-lookup"><span data-stu-id="c88b9-106">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="c88b9-107">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="c88b9-107">An Azure account.</span></span> <span data-ttu-id="c88b9-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c88b9-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c88b9-109">A Media Services account.</span><span class="sxs-lookup"><span data-stu-id="c88b9-109">A Media Services account.</span></span> <span data-ttu-id="c88b9-110">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="c88b9-110">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="c88b9-111">.NET Framework 4.0 or later.</span><span class="sxs-lookup"><span data-stu-id="c88b9-111">.NET Framework 4.0 or later.</span></span>
* <span data-ttu-id="c88b9-112">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c88b9-112">Visual Studio.</span></span>

<span data-ttu-id="c88b9-113">This tutorial includes the following tasks:</span><span class="sxs-lookup"><span data-stu-id="c88b9-113">This tutorial includes the following tasks:</span></span>

1. <span data-ttu-id="c88b9-114">Start streaming endpoint (using the Azure portal).</span><span class="sxs-lookup"><span data-stu-id="c88b9-114">Start streaming endpoint (using the Azure portal).</span></span>
2. <span data-ttu-id="c88b9-115">Create and configure a Visual Studio project.</span><span class="sxs-lookup"><span data-stu-id="c88b9-115">Create and configure a Visual Studio project.</span></span>
3. <span data-ttu-id="c88b9-116">Connect to the Media Services account.</span><span class="sxs-lookup"><span data-stu-id="c88b9-116">Connect to the Media Services account.</span></span>
2. <span data-ttu-id="c88b9-117">Upload a video file.</span><span class="sxs-lookup"><span data-stu-id="c88b9-117">Upload a video file.</span></span>
3. <span data-ttu-id="c88b9-118">Encode the source file into a set of adaptive bitrate MP4 files.</span><span class="sxs-lookup"><span data-stu-id="c88b9-118">Encode the source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="c88b9-119">Publish the asset and get streaming and progressive download URLs.</span><span class="sxs-lookup"><span data-stu-id="c88b9-119">Publish the asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="c88b9-120">Play your content.</span><span class="sxs-lookup"><span data-stu-id="c88b9-120">Play your content.</span></span>

## <a name="overview"></a><span data-ttu-id="c88b9-121">Overview</span><span class="sxs-lookup"><span data-stu-id="c88b9-121">Overview</span></span>
<span data-ttu-id="c88b9-122">This tutorial walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) SDK for .NET.</span><span class="sxs-lookup"><span data-stu-id="c88b9-122">This tutorial walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) SDK for .NET.</span></span>

<span data-ttu-id="c88b9-123">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span><span class="sxs-lookup"><span data-stu-id="c88b9-123">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="c88b9-124">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span><span class="sxs-lookup"><span data-stu-id="c88b9-124">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

### <a name="ams-model"></a><span data-ttu-id="c88b9-125">AMS model</span><span class="sxs-lookup"><span data-stu-id="c88b9-125">AMS model</span></span>

<span data-ttu-id="c88b9-126">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span><span class="sxs-lookup"><span data-stu-id="c88b9-126">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span></span>

<span data-ttu-id="c88b9-127">Click the image to view it full size.</span><span class="sxs-lookup"><span data-stu-id="c88b9-127">Click the image to view it full size.</span></span>  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="c88b9-128">You can view the whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span><span class="sxs-lookup"><span data-stu-id="c88b9-128">You can view the whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="start-streaming-endpoints-using-the-azure-portal"></a><span data-ttu-id="c88b9-129">Start streaming endpoints using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c88b9-129">Start streaming endpoints using the Azure portal</span></span>

<span data-ttu-id="c88b9-130">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span><span class="sxs-lookup"><span data-stu-id="c88b9-130">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="c88b9-131">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span><span class="sxs-lookup"><span data-stu-id="c88b9-131">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="c88b9-132">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span><span class="sxs-lookup"><span data-stu-id="c88b9-132">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="c88b9-133">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span><span class="sxs-lookup"><span data-stu-id="c88b9-133">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="c88b9-134">To start the streaming endpoint, do the following:</span><span class="sxs-lookup"><span data-stu-id="c88b9-134">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="c88b9-135">Log in at the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c88b9-135">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c88b9-136">In the Settings window, click Streaming endpoints.</span><span class="sxs-lookup"><span data-stu-id="c88b9-136">In the Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="c88b9-137">Click the default streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="c88b9-137">Click the default streaming endpoint.</span></span>

    <span data-ttu-id="c88b9-138">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span><span class="sxs-lookup"><span data-stu-id="c88b9-138">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="c88b9-139">Click the Start icon.</span><span class="sxs-lookup"><span data-stu-id="c88b9-139">Click the Start icon.</span></span>
5. <span data-ttu-id="c88b9-140">Click the Save button to save your changes.</span><span class="sxs-lookup"><span data-stu-id="c88b9-140">Click the Save button to save your changes.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="c88b9-141">Create and configure a Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="c88b9-141">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="c88b9-142">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="c88b9-142">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="c88b9-143">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want to encode and stream or progressively download.</span><span class="sxs-lookup"><span data-stu-id="c88b9-143">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want to encode and stream or progressively download.</span></span> <span data-ttu-id="c88b9-144">In this example, the "C:\VideoFiles" path is used.</span><span class="sxs-lookup"><span data-stu-id="c88b9-144">In this example, the "C:\VideoFiles" path is used.</span></span>

## <a name="connect-to-the-media-services-account"></a><span data-ttu-id="c88b9-145">Connect to the Media Services account</span><span class="sxs-lookup"><span data-stu-id="c88b9-145">Connect to the Media Services account</span></span>

<span data-ttu-id="c88b9-146">When using Media Services with .NET, you must use the **CloudMediaContext** class for most Media Services programming tasks: connecting to Media Services account; creating, updating, accessing, and deleting the following objects: assets, asset files, jobs, access policies, locators, etc.</span><span class="sxs-lookup"><span data-stu-id="c88b9-146">When using Media Services with .NET, you must use the **CloudMediaContext** class for most Media Services programming tasks: connecting to Media Services account; creating, updating, accessing, and deleting the following objects: assets, asset files, jobs, access policies, locators, etc.</span></span>

<span data-ttu-id="c88b9-147">Overwrite the default Program class with the following code: The code demonstrates how to read the connection values from the App.config file and how to create the **CloudMediaContext** object in order to connect to Media Services.</span><span class="sxs-lookup"><span data-stu-id="c88b9-147">Overwrite the default Program class with the following code: The code demonstrates how to read the connection values from the App.config file and how to create the **CloudMediaContext** object in order to connect to Media Services.</span></span> <span data-ttu-id="c88b9-148">For more information, see [connecting to the Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="c88b9-148">For more information, see [connecting to the Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

<span data-ttu-id="c88b9-149">Make sure to update the file name and path to where you have your media file.</span><span class="sxs-lookup"><span data-stu-id="c88b9-149">Make sure to update the file name and path to where you have your media file.</span></span>

<span data-ttu-id="c88b9-150">The **Main** function calls methods that will be defined further in this section.</span><span class="sxs-lookup"><span data-stu-id="c88b9-150">The **Main** function calls methods that will be defined further in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="c88b9-151">You will be getting compilation errors until you add definitions for all the functions that are defined later in this article.</span><span class="sxs-lookup"><span data-stu-id="c88b9-151">You will be getting compilation errors until you add definitions for all the functions that are defined later in this article.</span></span>

```csharp
    class Program
    {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AMSAADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["AMSRESTAPIEndpoint"];
        private static readonly string _AMSClientId =
            ConfigurationManager.AppSettings["AMSClientId"];
        private static readonly string _AMSClientSecret =
            ConfigurationManager.AppSettings["AMSClientSecret"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
        try
        {
            AzureAdTokenCredentials tokenCredentials = 
                new AzureAdTokenCredentials(_AADTenantDomain,
                    new AzureAdClientSymmetricKey(_AMSClientId, _AMSClientSecret),
                    AzureEnvironments.AzureCloudEnvironment);

            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Add calls to methods defined in this section.
            // Make sure to update the file name and path to where you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse the XML error message in the Media Services response and create a new
            // exception with its content.
            exception = MediaServicesExceptionParser.Parse(exception);

            Console.Error.WriteLine(exception.Message);
        }
        finally
        {
            Console.ReadLine();
        }
        }
```

## <a name="create-a-new-asset-and-upload-a-video-file"></a><span data-ttu-id="c88b9-152">Create a new asset and upload a video file</span><span class="sxs-lookup"><span data-stu-id="c88b9-152">Create a new asset and upload a video file</span></span>

<span data-ttu-id="c88b9-153">In Media Services, you upload (or ingest) your digital files into an asset.</span><span class="sxs-lookup"><span data-stu-id="c88b9-153">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="c88b9-154">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and the metadata about these files.)  Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span><span class="sxs-lookup"><span data-stu-id="c88b9-154">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and the metadata about these files.)  Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span> <span data-ttu-id="c88b9-155">The files in the asset are called **Asset Files**.</span><span class="sxs-lookup"><span data-stu-id="c88b9-155">The files in the asset are called **Asset Files**.</span></span>

<span data-ttu-id="c88b9-156">The **UploadFile** method defined below calls **CreateFromFile** (defined in .NET SDK Extensions).</span><span class="sxs-lookup"><span data-stu-id="c88b9-156">The **UploadFile** method defined below calls **CreateFromFile** (defined in .NET SDK Extensions).</span></span> <span data-ttu-id="c88b9-157">**CreateFromFile** creates a new asset into which the specified source file is uploaded.</span><span class="sxs-lookup"><span data-stu-id="c88b9-157">**CreateFromFile** creates a new asset into which the specified source file is uploaded.</span></span>

<span data-ttu-id="c88b9-158">The **CreateFromFile** method takes **AssetCreationOptions**, which lets you specify one of the following asset creation options:</span><span class="sxs-lookup"><span data-stu-id="c88b9-158">The **CreateFromFile** method takes **AssetCreationOptions**, which lets you specify one of the following asset creation options:</span></span>

* <span data-ttu-id="c88b9-159">**None** - No encryption is used.</span><span class="sxs-lookup"><span data-stu-id="c88b9-159">**None** - No encryption is used.</span></span> <span data-ttu-id="c88b9-160">This is the default value.</span><span class="sxs-lookup"><span data-stu-id="c88b9-160">This is the default value.</span></span> <span data-ttu-id="c88b9-161">Note that when using this option, your content is not protected in transit or at rest in storage.</span><span class="sxs-lookup"><span data-stu-id="c88b9-161">Note that when using this option, your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="c88b9-162">If you plan to deliver an MP4 using progressive download, use this option.</span><span class="sxs-lookup"><span data-stu-id="c88b9-162">If you plan to deliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="c88b9-163">**StorageEncrypted** - Use this option to encrypt your clear content locally using Advanced Encryption Standard (AES)-256 bit encryption, which then uploads it to Azure Storage where it is stored encrypted at rest.</span><span class="sxs-lookup"><span data-stu-id="c88b9-163">**StorageEncrypted** - Use this option to encrypt your clear content locally using Advanced Encryption Standard (AES)-256 bit encryption, which then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="c88b9-164">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span><span class="sxs-lookup"><span data-stu-id="c88b9-164">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="c88b9-165">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span><span class="sxs-lookup"><span data-stu-id="c88b9-165">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="c88b9-166">**CommonEncryptionProtected** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="c88b9-166">**CommonEncryptionProtected** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="c88b9-167">**EnvelopeEncryptionProtected** – Use this option if you are uploading HLS encrypted with AES.</span><span class="sxs-lookup"><span data-stu-id="c88b9-167">**EnvelopeEncryptionProtected** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="c88b9-168">Note that the files must have been encoded and encrypted by Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="c88b9-168">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>

<span data-ttu-id="c88b9-169">The **CreateFromFile** method also lets you specify a callback in order to report the upload progress of the file.</span><span class="sxs-lookup"><span data-stu-id="c88b9-169">The **CreateFromFile** method also lets you specify a callback in order to report the upload progress of the file.</span></span>

<span data-ttu-id="c88b9-170">In the following example, we specify **None** for the asset options.</span><span class="sxs-lookup"><span data-stu-id="c88b9-170">In the following example, we specify **None** for the asset options.</span></span>

<span data-ttu-id="c88b9-171">Add the following method to the Program class.</span><span class="sxs-lookup"><span data-stu-id="c88b9-171">Add the following method to the Program class.</span></span>

```csharp
    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }
```

## <a name="encode-the-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a><span data-ttu-id="c88b9-172">Encode the source file into a set of adaptive bitrate MP4 files</span><span class="sxs-lookup"><span data-stu-id="c88b9-172">Encode the source file into a set of adaptive bitrate MP4 files</span></span>
<span data-ttu-id="c88b9-173">After ingesting assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span><span class="sxs-lookup"><span data-stu-id="c88b9-173">After ingesting assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span></span> <span data-ttu-id="c88b9-174">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span><span class="sxs-lookup"><span data-stu-id="c88b9-174">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span></span> <span data-ttu-id="c88b9-175">These activities are called Jobs, and each Job is composed of atomic Tasks that do the actual work on the Asset file.</span><span class="sxs-lookup"><span data-stu-id="c88b9-175">These activities are called Jobs, and each Job is composed of atomic Tasks that do the actual work on the Asset file.</span></span>

<span data-ttu-id="c88b9-176">As was mentioned earlier, when working with Azure Media Services, one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span><span class="sxs-lookup"><span data-stu-id="c88b9-176">As was mentioned earlier, when working with Azure Media Services, one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="c88b9-177">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="c88b9-177">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span>

<span data-ttu-id="c88b9-178">To take advantage of dynamic packaging, you need to encode or transcode your mezzanine (source) file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span><span class="sxs-lookup"><span data-stu-id="c88b9-178">To take advantage of dynamic packaging, you need to encode or transcode your mezzanine (source) file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>  

<span data-ttu-id="c88b9-179">The following code shows how to submit an encoding job.</span><span class="sxs-lookup"><span data-stu-id="c88b9-179">The following code shows how to submit an encoding job.</span></span> <span data-ttu-id="c88b9-180">The job contains one task that specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="c88b9-180">The job contains one task that specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="c88b9-181">The code submits the job and waits until it is completed.</span><span class="sxs-lookup"><span data-stu-id="c88b9-181">The code submits the job and waits until it is completed.</span></span>

<span data-ttu-id="c88b9-182">Once the job is completed, you would be able to stream your asset or progressively download MP4 files that were created as a result of transcoding.</span><span class="sxs-lookup"><span data-stu-id="c88b9-182">Once the job is completed, you would be able to stream your asset or progressively download MP4 files that were created as a result of transcoding.</span></span>

<span data-ttu-id="c88b9-183">Add the following method to the Program class.</span><span class="sxs-lookup"><span data-stu-id="c88b9-183">Add the following method to the Program class.</span></span>

```csharp
    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task to transcode the specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit the job and wait until it is completed.
        job.Submit();

        job = job.StartExecutionProgressTask(
            j =>
            {
                Console.WriteLine("Job state: {0}", j.State);
                Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
            },
            CancellationToken.None).Result;

        Console.WriteLine("Transcoding job finished.");

        IAsset outputAsset = job.OutputMediaAssets[0];

        return outputAsset;
    }
```

## <a name="publish-the-asset-and-get-urls-for-streaming-and-progressive-download"></a><span data-ttu-id="c88b9-184">Publish the asset and get URLs for streaming and progressive download</span><span class="sxs-lookup"><span data-stu-id="c88b9-184">Publish the asset and get URLs for streaming and progressive download</span></span>

<span data-ttu-id="c88b9-185">To stream or download an asset, you first need to "publish" it by creating a locator.</span><span class="sxs-lookup"><span data-stu-id="c88b9-185">To stream or download an asset, you first need to "publish" it by creating a locator.</span></span> <span data-ttu-id="c88b9-186">Locators provide access to files contained in the asset.</span><span class="sxs-lookup"><span data-stu-id="c88b9-186">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="c88b9-187">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files.</span><span class="sxs-lookup"><span data-stu-id="c88b9-187">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files.</span></span>

### <a name="some-details-about-url-formats"></a><span data-ttu-id="c88b9-188">Some details about URL formats</span><span class="sxs-lookup"><span data-stu-id="c88b9-188">Some details about URL formats</span></span>

<span data-ttu-id="c88b9-189">After you create the locators, you can build the URLs that would be used to stream or download your files.</span><span class="sxs-lookup"><span data-stu-id="c88b9-189">After you create the locators, you can build the URLs that would be used to stream or download your files.</span></span> <span data-ttu-id="c88b9-190">The sample in this tutorial outputs URLs that you can paste in appropriate browsers.</span><span class="sxs-lookup"><span data-stu-id="c88b9-190">The sample in this tutorial outputs URLs that you can paste in appropriate browsers.</span></span> <span data-ttu-id="c88b9-191">This section just gives short examples of what different formats look like.</span><span class="sxs-lookup"><span data-stu-id="c88b9-191">This section just gives short examples of what different formats look like.</span></span>

#### <a name="a-streaming-url-for-mpeg-dash-has-the-following-format"></a><span data-ttu-id="c88b9-192">A streaming URL for MPEG DASH has the following format:</span><span class="sxs-lookup"><span data-stu-id="c88b9-192">A streaming URL for MPEG DASH has the following format:</span></span>

<span data-ttu-id="c88b9-193">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest **(format=mpd-time-csf)**</span><span class="sxs-lookup"><span data-stu-id="c88b9-193">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest **(format=mpd-time-csf)**</span></span>

#### <a name="a-streaming-url-for-hls-has-the-following-format"></a><span data-ttu-id="c88b9-194">A streaming URL for HLS has the following format:</span><span class="sxs-lookup"><span data-stu-id="c88b9-194">A streaming URL for HLS has the following format:</span></span>

<span data-ttu-id="c88b9-195">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest **(format=m3u8-aapl)**</span><span class="sxs-lookup"><span data-stu-id="c88b9-195">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest **(format=m3u8-aapl)**</span></span>

#### <a name="a-streaming-url-for-smooth-streaming-has-the-following-format"></a><span data-ttu-id="c88b9-196">A streaming URL for Smooth Streaming has the following format:</span><span class="sxs-lookup"><span data-stu-id="c88b9-196">A streaming URL for Smooth Streaming has the following format:</span></span>

<span data-ttu-id="c88b9-197">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="c88b9-197">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>


#### <a name="a-sas-url-used-to-download-files-has-the-following-format"></a><span data-ttu-id="c88b9-198">A SAS URL used to download files has the following format:</span><span class="sxs-lookup"><span data-stu-id="c88b9-198">A SAS URL used to download files has the following format:</span></span>

<span data-ttu-id="c88b9-199">{blob container name}/{asset name}/{file name}/{SAS signature}</span><span class="sxs-lookup"><span data-stu-id="c88b9-199">{blob container name}/{asset name}/{file name}/{SAS signature}</span></span>

<span data-ttu-id="c88b9-200">Media Services .NET SDK extensions provide convenient helper methods that return formatted URLs for the published asset.</span><span class="sxs-lookup"><span data-stu-id="c88b9-200">Media Services .NET SDK extensions provide convenient helper methods that return formatted URLs for the published asset.</span></span>

<span data-ttu-id="c88b9-201">The following code uses .NET SDK Extensions to create locators and to get streaming and progressive download URLs.</span><span class="sxs-lookup"><span data-stu-id="c88b9-201">The following code uses .NET SDK Extensions to create locators and to get streaming and progressive download URLs.</span></span> <span data-ttu-id="c88b9-202">The code also shows how to download files to a local folder.</span><span class="sxs-lookup"><span data-stu-id="c88b9-202">The code also shows how to download files to a local folder.</span></span>

<span data-ttu-id="c88b9-203">Add the following method to the Program class.</span><span class="sxs-lookup"><span data-stu-id="c88b9-203">Add the following method to the Program class.</span></span>

```csharp
    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish the output asset by creating an Origin locator for adaptive streaming,
        // and a SAS locator for progressive download.

        _context.Locators.Create(
            LocatorType.OnDemandOrigin,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));

        _context.Locators.Create(
            LocatorType.Sas,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));


        IEnumerable<IAssetFile> mp4AssetFiles = asset
                .AssetFiles
                .ToList()
                .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Get the Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and the Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get the URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  the streaming URLs.
        Console.WriteLine("Use the following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display the URLs for progressive download.
        Console.WriteLine("Use the following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download the output asset to a local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files to a local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }
```

## <a name="test-by-playing-your-content"></a><span data-ttu-id="c88b9-204">Test by playing your content</span><span class="sxs-lookup"><span data-stu-id="c88b9-204">Test by playing your content</span></span>

<span data-ttu-id="c88b9-205">Once you run the program defined in the previous section, the URLs similar to the following will be displayed in the console window.</span><span class="sxs-lookup"><span data-stu-id="c88b9-205">Once you run the program defined in the previous section, the URLs similar to the following will be displayed in the console window.</span></span>

<span data-ttu-id="c88b9-206">Adaptive streaming URLs:</span><span class="sxs-lookup"><span data-stu-id="c88b9-206">Adaptive streaming URLs:</span></span>

<span data-ttu-id="c88b9-207">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="c88b9-207">Smooth Streaming</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="c88b9-208">HLS</span><span class="sxs-lookup"><span data-stu-id="c88b9-208">HLS</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="c88b9-209">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="c88b9-209">MPEG DASH</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

<span data-ttu-id="c88b9-210">Progressive download URLs (audio and video).</span><span class="sxs-lookup"><span data-stu-id="c88b9-210">Progressive download URLs (audio and video).</span></span>

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


<span data-ttu-id="c88b9-211">To stream your video, paste your URL in the URL textbox in the [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="c88b9-211">To stream your video, paste your URL in the URL textbox in the [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="c88b9-212">To test progressive download, paste a URL into a browser (for example, Internet Explorer, Chrome, or Safari).</span><span class="sxs-lookup"><span data-stu-id="c88b9-212">To test progressive download, paste a URL into a browser (for example, Internet Explorer, Chrome, or Safari).</span></span>

<span data-ttu-id="c88b9-213">For more information, see the following topics:</span><span class="sxs-lookup"><span data-stu-id="c88b9-213">For more information, see the following topics:</span></span>

- [<span data-ttu-id="c88b9-214">Playing your content with existing players</span><span class="sxs-lookup"><span data-stu-id="c88b9-214">Playing your content with existing players</span></span>](media-services-playback-content-with-existing-players.md)
- [<span data-ttu-id="c88b9-215">Develop video player applications</span><span class="sxs-lookup"><span data-stu-id="c88b9-215">Develop video player applications</span></span>](media-services-develop-video-players.md)
- [<span data-ttu-id="c88b9-216">Embedding an MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span><span class="sxs-lookup"><span data-stu-id="c88b9-216">Embedding an MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a><span data-ttu-id="c88b9-217">Download sample</span><span class="sxs-lookup"><span data-stu-id="c88b9-217">Download sample</span></span>
<span data-ttu-id="c88b9-218">The following code sample contains the code that you created in this tutorial: [sample](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="c88b9-218">The following code sample contains the code that you created in this tutorial: [sample](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c88b9-219">Next Steps</span><span class="sxs-lookup"><span data-stu-id="c88b9-219">Next Steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c88b9-220">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="c88b9-220">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://portal.azure.com/
