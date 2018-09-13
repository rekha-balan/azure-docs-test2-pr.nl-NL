---
title: Get started with delivering content on demand using .NET | Microsoft Docs
description: This tutorial walks you through the steps of implementing an on demand content delivery application with Azure Media Services using .NET.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 388b8928-9aa9-46b1-b60a-a918da75bd7b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 01/10/2017
ms.author: juliako
ms.openlocfilehash: 6bec39e31028200136f9ecbcd8318e7c76bdf259
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556103"
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a><span data-ttu-id="d0125-103">Get started with delivering content on demand using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d0125-103">Get started with delivering content on demand using .NET SDK</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="d0125-104">This tutorial walks you through the steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using the Azure Media Services .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="d0125-104">This tutorial walks you through the steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using the Azure Media Services .NET SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0125-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d0125-105">Prerequisites</span></span>

<span data-ttu-id="d0125-106">The following are required to complete the tutorial:</span><span class="sxs-lookup"><span data-stu-id="d0125-106">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="d0125-107">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="d0125-107">An Azure account.</span></span> <span data-ttu-id="d0125-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0125-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d0125-109">A Media Services account.</span><span class="sxs-lookup"><span data-stu-id="d0125-109">A Media Services account.</span></span> <span data-ttu-id="d0125-110">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="d0125-110">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="d0125-111">.NET Framework 4.0 or later.</span><span class="sxs-lookup"><span data-stu-id="d0125-111">.NET Framework 4.0 or later.</span></span>
* <span data-ttu-id="d0125-112">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d0125-112">Visual Studio.</span></span>

<span data-ttu-id="d0125-113">This tutorial includes the following tasks:</span><span class="sxs-lookup"><span data-stu-id="d0125-113">This tutorial includes the following tasks:</span></span>

1. <span data-ttu-id="d0125-114">Start streaming endpoint (using the Azure portal).</span><span class="sxs-lookup"><span data-stu-id="d0125-114">Start streaming endpoint (using the Azure portal).</span></span>
2. <span data-ttu-id="d0125-115">Create and configure a Visual Studio project.</span><span class="sxs-lookup"><span data-stu-id="d0125-115">Create and configure a Visual Studio project.</span></span>
3. <span data-ttu-id="d0125-116">Connect to the Media Services account.</span><span class="sxs-lookup"><span data-stu-id="d0125-116">Connect to the Media Services account.</span></span>
2. <span data-ttu-id="d0125-117">Upload a video file.</span><span class="sxs-lookup"><span data-stu-id="d0125-117">Upload a video file.</span></span>
3. <span data-ttu-id="d0125-118">Encode the source file into a set of adaptive bitrate MP4 files.</span><span class="sxs-lookup"><span data-stu-id="d0125-118">Encode the source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="d0125-119">Publish the asset and get streaming and progressive download URLs.</span><span class="sxs-lookup"><span data-stu-id="d0125-119">Publish the asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="d0125-120">Play your content.</span><span class="sxs-lookup"><span data-stu-id="d0125-120">Play your content.</span></span>

## <a name="overview"></a><span data-ttu-id="d0125-121">Overview</span><span class="sxs-lookup"><span data-stu-id="d0125-121">Overview</span></span>
<span data-ttu-id="d0125-122">This tutorial walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) SDK for .NET.</span><span class="sxs-lookup"><span data-stu-id="d0125-122">This tutorial walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) SDK for .NET.</span></span>

<span data-ttu-id="d0125-123">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span><span class="sxs-lookup"><span data-stu-id="d0125-123">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="d0125-124">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span><span class="sxs-lookup"><span data-stu-id="d0125-124">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

### <a name="ams-model"></a><span data-ttu-id="d0125-125">AMS model</span><span class="sxs-lookup"><span data-stu-id="d0125-125">AMS model</span></span>

<span data-ttu-id="d0125-126">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span><span class="sxs-lookup"><span data-stu-id="d0125-126">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span></span>

<span data-ttu-id="d0125-127">Click the image to view it full size.</span><span class="sxs-lookup"><span data-stu-id="d0125-127">Click the image to view it full size.</span></span>  

<a href="https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="d0125-128">You can view the whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span><span class="sxs-lookup"><span data-stu-id="d0125-128">You can view the whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="start-streaming-endpoints-using-the-azure-portal"></a><span data-ttu-id="d0125-129">Start streaming endpoints using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d0125-129">Start streaming endpoints using the Azure portal</span></span>

<span data-ttu-id="d0125-130">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span><span class="sxs-lookup"><span data-stu-id="d0125-130">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="d0125-131">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span><span class="sxs-lookup"><span data-stu-id="d0125-131">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="d0125-132">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span><span class="sxs-lookup"><span data-stu-id="d0125-132">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="d0125-133">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span><span class="sxs-lookup"><span data-stu-id="d0125-133">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="d0125-134">To start the streaming endpoint, do the following:</span><span class="sxs-lookup"><span data-stu-id="d0125-134">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="d0125-135">Log in at the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d0125-135">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d0125-136">In the Settings window, click Streaming endpoints.</span><span class="sxs-lookup"><span data-stu-id="d0125-136">In the Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="d0125-137">Click the default streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="d0125-137">Click the default streaming endpoint.</span></span>

    <span data-ttu-id="d0125-138">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span><span class="sxs-lookup"><span data-stu-id="d0125-138">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="d0125-139">Click the Start icon.</span><span class="sxs-lookup"><span data-stu-id="d0125-139">Click the Start icon.</span></span>
5. <span data-ttu-id="d0125-140">Click the Save button to save your changes.</span><span class="sxs-lookup"><span data-stu-id="d0125-140">Click the Save button to save your changes.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="d0125-141">Create and configure a Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="d0125-141">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="d0125-142">Create a new C# Console Application in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d0125-142">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="d0125-143">Enter the **Name**, **Location**, and **Solution name**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d0125-143">Enter the **Name**, **Location**, and **Solution name**, and then click **OK**.</span></span>
2. <span data-ttu-id="d0125-144">Use the  [windowsazure.mediaservices.extensions](https://www.nuget.org/packages/windowsazure.mediaservices.extensions) NuGet package to install **Azure Media Services .NET SDK Extensions**.</span><span class="sxs-lookup"><span data-stu-id="d0125-144">Use the  [windowsazure.mediaservices.extensions](https://www.nuget.org/packages/windowsazure.mediaservices.extensions) NuGet package to install **Azure Media Services .NET SDK Extensions**.</span></span>  <span data-ttu-id="d0125-145">The Media Services .NET SDK Extensions is a set of extension methods and helper functions that will simplify your code and make it easier to develop with Media Services.</span><span class="sxs-lookup"><span data-stu-id="d0125-145">The Media Services .NET SDK Extensions is a set of extension methods and helper functions that will simplify your code and make it easier to develop with Media Services.</span></span> <span data-ttu-id="d0125-146">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span><span class="sxs-lookup"><span data-stu-id="d0125-146">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>

    <span data-ttu-id="d0125-147">To add references by using NuGet do the following: in Solution Explorer, click the right mouse button on the project name, select **Manage NuGet packages**.</span><span class="sxs-lookup"><span data-stu-id="d0125-147">To add references by using NuGet do the following: in Solution Explorer, click the right mouse button on the project name, select **Manage NuGet packages**.</span></span> <span data-ttu-id="d0125-148">Then, search for **windowsazure.mediaservices.extensions** and click **Install**.</span><span class="sxs-lookup"><span data-stu-id="d0125-148">Then, search for **windowsazure.mediaservices.extensions** and click **Install**.</span></span>

3. <span data-ttu-id="d0125-149">Add a reference to System.Configuration assembly.</span><span class="sxs-lookup"><span data-stu-id="d0125-149">Add a reference to System.Configuration assembly.</span></span> <span data-ttu-id="d0125-150">This assembly contains the **System.Configuration.ConfigurationManager** class that is used to access configuration files, for example, App.config.</span><span class="sxs-lookup"><span data-stu-id="d0125-150">This assembly contains the **System.Configuration.ConfigurationManager** class that is used to access configuration files, for example, App.config.</span></span>

    <span data-ttu-id="d0125-151">To add a reference, do the following: in Solution Explorer, click the right mouse button on the project name, select **Add** > **Reference...** and type configuration in the search box.</span><span class="sxs-lookup"><span data-stu-id="d0125-151">To add a reference, do the following: in Solution Explorer, click the right mouse button on the project name, select **Add** > **Reference...** and type configuration in the search box.</span></span>

4. <span data-ttu-id="d0125-152">Open the App.config file (add the file to your project if it was not added by default) and add an *appSettings* section to the file.</span><span class="sxs-lookup"><span data-stu-id="d0125-152">Open the App.config file (add the file to your project if it was not added by default) and add an *appSettings* section to the file.</span></span> <span data-ttu-id="d0125-153">Set the values for your Azure Media Services account name and account key, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="d0125-153">Set the values for your Azure Media Services account name and account key, as shown in the following example.</span></span> <span data-ttu-id="d0125-154">To obtain the account name and key information, go to the [Azure portal](https://portal.azure.com/) and select your AMS account.</span><span class="sxs-lookup"><span data-stu-id="d0125-154">To obtain the account name and key information, go to the [Azure portal](https://portal.azure.com/) and select your AMS account.</span></span> <span data-ttu-id="d0125-155">Then, select **Settings** > **Keys**.</span><span class="sxs-lookup"><span data-stu-id="d0125-155">Then, select **Settings** > **Keys**.</span></span> <span data-ttu-id="d0125-156">The Manage keys windows shows the account name and the primary and secondary keys is displayed.</span><span class="sxs-lookup"><span data-stu-id="d0125-156">The Manage keys windows shows the account name and the primary and secondary keys is displayed.</span></span> <span data-ttu-id="d0125-157">Copy values of the account name and the primary key.</span><span class="sxs-lookup"><span data-stu-id="d0125-157">Copy values of the account name and the primary key.</span></span>

        <configuration>
        ...
          <appSettings>
            <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
            <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
          </appSettings>

        </configuration>
5. <span data-ttu-id="d0125-158">Overwrite the existing **using** statements at the beginning of the Program.cs file with the following code.</span><span class="sxs-lookup"><span data-stu-id="d0125-158">Overwrite the existing **using** statements at the beginning of the Program.cs file with the following code.</span></span>

        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Text;
        using System.Threading.Tasks;
        using System.Configuration;
        using System.Threading;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
6. <span data-ttu-id="d0125-159">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want to encode and stream or progressively download.</span><span class="sxs-lookup"><span data-stu-id="d0125-159">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want to encode and stream or progressively download.</span></span> <span data-ttu-id="d0125-160">In this example, the "C:\VideoFiles" path is used.</span><span class="sxs-lookup"><span data-stu-id="d0125-160">In this example, the "C:\VideoFiles" path is used.</span></span>

## <a name="connect-to-the-media-services-account"></a><span data-ttu-id="d0125-161">Connect to the Media Services account</span><span class="sxs-lookup"><span data-stu-id="d0125-161">Connect to the Media Services account</span></span>

<span data-ttu-id="d0125-162">When using Media Services with .NET, you must use the **CloudMediaContext** class for most Media Services programming tasks: connecting to Media Services account; creating, updating, accessing, and deleting the following objects: assets, asset files, jobs, access policies, locators, etc.</span><span class="sxs-lookup"><span data-stu-id="d0125-162">When using Media Services with .NET, you must use the **CloudMediaContext** class for most Media Services programming tasks: connecting to Media Services account; creating, updating, accessing, and deleting the following objects: assets, asset files, jobs, access policies, locators, etc.</span></span>

<span data-ttu-id="d0125-163">Overwrite the default Program class with the following code.</span><span class="sxs-lookup"><span data-stu-id="d0125-163">Overwrite the default Program class with the following code.</span></span> <span data-ttu-id="d0125-164">The code demonstrates how to read the connection values from the App.config file and how to create the **CloudMediaContext** object in order to connect to Media Services.</span><span class="sxs-lookup"><span data-stu-id="d0125-164">The code demonstrates how to read the connection values from the App.config file and how to create the **CloudMediaContext** object in order to connect to Media Services.</span></span> <span data-ttu-id="d0125-165">For more information about connecting to Media Services, see [Connecting to Media Services with the Media Services SDK for .NET](media-services-dotnet-connect-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="d0125-165">For more information about connecting to Media Services, see [Connecting to Media Services with the Media Services SDK for .NET](media-services-dotnet-connect-programmatically.md).</span></span>

<span data-ttu-id="d0125-166">Make sure to update the file name and path to where you have your media file.</span><span class="sxs-lookup"><span data-stu-id="d0125-166">Make sure to update the file name and path to where you have your media file.</span></span>

<span data-ttu-id="d0125-167">The **Main** function calls methods that will be defined further in this section.</span><span class="sxs-lookup"><span data-stu-id="d0125-167">The **Main** function calls methods that will be defined further in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="d0125-168">You will be getting compilation errors until you add definitions for all the functions.</span><span class="sxs-lookup"><span data-stu-id="d0125-168">You will be getting compilation errors until you add definitions for all the functions.</span></span>

    class Program
    {
        // Read values from the App.config file.
        private static readonly string _mediaServicesAccountName =
            ConfigurationManager.AppSettings["MediaServicesAccountName"];
        private static readonly string _mediaServicesAccountKey =
            ConfigurationManager.AppSettings["MediaServicesAccountKey"];

        // Field for service context.
        private static CloudMediaContext _context = null;
        private static MediaServicesCredentials _cachedCredentials = null;

        static void Main(string[] args)
        {
            try
            {
                // Create and cache the Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName,
                                _mediaServicesAccountKey);
                // Used the chached credentials to create CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);

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
    }

## <a name="create-a-new-asset-and-upload-a-video-file"></a><span data-ttu-id="d0125-169">Create a new asset and upload a video file</span><span class="sxs-lookup"><span data-stu-id="d0125-169">Create a new asset and upload a video file</span></span>

<span data-ttu-id="d0125-170">In Media Services, you upload (or ingest) your digital files into an asset.</span><span class="sxs-lookup"><span data-stu-id="d0125-170">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="d0125-171">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and the metadata about these files.)  Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span><span class="sxs-lookup"><span data-stu-id="d0125-171">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and the metadata about these files.)  Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span> <span data-ttu-id="d0125-172">The files in the asset are called **Asset Files**.</span><span class="sxs-lookup"><span data-stu-id="d0125-172">The files in the asset are called **Asset Files**.</span></span>

<span data-ttu-id="d0125-173">The **UploadFile** method defined below calls **CreateFromFile** (defined in .NET SDK Extensions).</span><span class="sxs-lookup"><span data-stu-id="d0125-173">The **UploadFile** method defined below calls **CreateFromFile** (defined in .NET SDK Extensions).</span></span> <span data-ttu-id="d0125-174">**CreateFromFile** creates a new asset into which the specified source file is uploaded.</span><span class="sxs-lookup"><span data-stu-id="d0125-174">**CreateFromFile** creates a new asset into which the specified source file is uploaded.</span></span>

<span data-ttu-id="d0125-175">The **CreateFromFile** method takes **AssetCreationOptions** which lets you specify one of the following asset creation options:</span><span class="sxs-lookup"><span data-stu-id="d0125-175">The **CreateFromFile** method takes **AssetCreationOptions** which lets you specify one of the following asset creation options:</span></span>

* <span data-ttu-id="d0125-176">**None** - No encryption is used.</span><span class="sxs-lookup"><span data-stu-id="d0125-176">**None** - No encryption is used.</span></span> <span data-ttu-id="d0125-177">This is the default value.</span><span class="sxs-lookup"><span data-stu-id="d0125-177">This is the default value.</span></span> <span data-ttu-id="d0125-178">Note that when using this option, your content is not protected in transit or at rest in storage.</span><span class="sxs-lookup"><span data-stu-id="d0125-178">Note that when using this option, your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="d0125-179">If you plan to deliver an MP4 using progressive download, use this option.</span><span class="sxs-lookup"><span data-stu-id="d0125-179">If you plan to deliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="d0125-180">**StorageEncrypted** - Use this option to encrypt your clear content locally using Advanced Encryption Standard (AES)-256 bit encryption, which then uploads it to Azure Storage where it is stored encrypted at rest.</span><span class="sxs-lookup"><span data-stu-id="d0125-180">**StorageEncrypted** - Use this option to encrypt your clear content locally using Advanced Encryption Standard (AES)-256 bit encryption, which then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="d0125-181">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span><span class="sxs-lookup"><span data-stu-id="d0125-181">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="d0125-182">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span><span class="sxs-lookup"><span data-stu-id="d0125-182">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="d0125-183">**CommonEncryptionProtected** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="d0125-183">**CommonEncryptionProtected** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="d0125-184">**EnvelopeEncryptionProtected** – Use this option if you are uploading HLS encrypted with AES.</span><span class="sxs-lookup"><span data-stu-id="d0125-184">**EnvelopeEncryptionProtected** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="d0125-185">Note that the files must have been encoded and encrypted by Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="d0125-185">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>

<span data-ttu-id="d0125-186">The **CreateFromFile** method also lets you specify a callback in order to report the upload progress of the file.</span><span class="sxs-lookup"><span data-stu-id="d0125-186">The **CreateFromFile** method also lets you specify a callback in order to report the upload progress of the file.</span></span>

<span data-ttu-id="d0125-187">In the following example, we specify **None** for the asset options.</span><span class="sxs-lookup"><span data-stu-id="d0125-187">In the following example, we specify **None** for the asset options.</span></span>

<span data-ttu-id="d0125-188">Add the following method to the Program class.</span><span class="sxs-lookup"><span data-stu-id="d0125-188">Add the following method to the Program class.</span></span>

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


## <a name="encode-the-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a><span data-ttu-id="d0125-189">Encode the source file into a set of adaptive bitrate MP4 files</span><span class="sxs-lookup"><span data-stu-id="d0125-189">Encode the source file into a set of adaptive bitrate MP4 files</span></span>
<span data-ttu-id="d0125-190">After ingesting assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span><span class="sxs-lookup"><span data-stu-id="d0125-190">After ingesting assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span></span> <span data-ttu-id="d0125-191">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span><span class="sxs-lookup"><span data-stu-id="d0125-191">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span></span> <span data-ttu-id="d0125-192">These activities are called Jobs, and each Job is composed of atomic Tasks that do the actual work on the Asset file.</span><span class="sxs-lookup"><span data-stu-id="d0125-192">These activities are called Jobs, and each Job is composed of atomic Tasks that do the actual work on the Asset file.</span></span>

<span data-ttu-id="d0125-193">As was mentioned earlier, when working with Azure Media Services, one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span><span class="sxs-lookup"><span data-stu-id="d0125-193">As was mentioned earlier, when working with Azure Media Services, one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="d0125-194">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="d0125-194">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span>

<span data-ttu-id="d0125-195">To take advantage of dynamic packaging, you need to encode or transcode your mezzanine (source) file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span><span class="sxs-lookup"><span data-stu-id="d0125-195">To take advantage of dynamic packaging, you need to encode or transcode your mezzanine (source) file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>  

<span data-ttu-id="d0125-196">The following code shows how to submit an encoding job.</span><span class="sxs-lookup"><span data-stu-id="d0125-196">The following code shows how to submit an encoding job.</span></span> <span data-ttu-id="d0125-197">The job contains one task that specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="d0125-197">The job contains one task that specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="d0125-198">The code submits the job and waits until it is completed.</span><span class="sxs-lookup"><span data-stu-id="d0125-198">The code submits the job and waits until it is completed.</span></span>

<span data-ttu-id="d0125-199">Once the job is completed, you would be able to stream your asset or progressively download MP4 files that were created as a result of transcoding.</span><span class="sxs-lookup"><span data-stu-id="d0125-199">Once the job is completed, you would be able to stream your asset or progressively download MP4 files that were created as a result of transcoding.</span></span>

<span data-ttu-id="d0125-200">Add the following method to the Program class.</span><span class="sxs-lookup"><span data-stu-id="d0125-200">Add the following method to the Program class.</span></span>

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

## <a name="publish-the-asset-and-get-urls-for-streaming-and-progressive-download"></a><span data-ttu-id="d0125-201">Publish the asset and get URLs for streaming and progressive download</span><span class="sxs-lookup"><span data-stu-id="d0125-201">Publish the asset and get URLs for streaming and progressive download</span></span>

<span data-ttu-id="d0125-202">To stream or download an asset, you first need to "publish" it by creating a locator.</span><span class="sxs-lookup"><span data-stu-id="d0125-202">To stream or download an asset, you first need to "publish" it by creating a locator.</span></span> <span data-ttu-id="d0125-203">Locators provide access to files contained in the asset.</span><span class="sxs-lookup"><span data-stu-id="d0125-203">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="d0125-204">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files (for more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span><span class="sxs-lookup"><span data-stu-id="d0125-204">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files (for more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span></span>

### <a name="some-details-about-url-formats"></a><span data-ttu-id="d0125-205">Some details about URL formats</span><span class="sxs-lookup"><span data-stu-id="d0125-205">Some details about URL formats</span></span>

<span data-ttu-id="d0125-206">After you create the locators, you can build the URLs that would be used to stream or download your files.</span><span class="sxs-lookup"><span data-stu-id="d0125-206">After you create the locators, you can build the URLs that would be used to stream or download your files.</span></span> <span data-ttu-id="d0125-207">The sample in this tutorial will output URLs that you can paste in appropriate browsers.</span><span class="sxs-lookup"><span data-stu-id="d0125-207">The sample in this tutorial will output URLs that you can paste in appropriate browsers.</span></span> <span data-ttu-id="d0125-208">This secion just gives short examples of what different formats look like.</span><span class="sxs-lookup"><span data-stu-id="d0125-208">This secion just gives short examples of what different formats look like.</span></span>

#### <a name="a-streaming-url-for-mpeg-dash-has-the-following-format"></a><span data-ttu-id="d0125-209">A streaming URL for MPEG DASH has the following format:</span><span class="sxs-lookup"><span data-stu-id="d0125-209">A streaming URL for MPEG DASH has the following format:</span></span>

<span data-ttu-id="d0125-210">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest **(format=mpd-time-csf)**</span><span class="sxs-lookup"><span data-stu-id="d0125-210">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest **(format=mpd-time-csf)**</span></span>

#### <a name="a-streaming-url-for-hls-has-the-following-format"></a><span data-ttu-id="d0125-211">A streaming URL for HLS has the following format:</span><span class="sxs-lookup"><span data-stu-id="d0125-211">A streaming URL for HLS has the following format:</span></span>

<span data-ttu-id="d0125-212">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest **(format=m3u8-aapl)**</span><span class="sxs-lookup"><span data-stu-id="d0125-212">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest **(format=m3u8-aapl)**</span></span>

#### <a name="a-streaming-url-for-smooth-streaming-has-the-following-format"></a><span data-ttu-id="d0125-213">A streaming URL for Smooth Streaming has the following format:</span><span class="sxs-lookup"><span data-stu-id="d0125-213">A streaming URL for Smooth Streaming has the following format:</span></span>

<span data-ttu-id="d0125-214">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="d0125-214">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>


#### <a name="a-sas-url-used-to-download-files-has-the-following-format"></a><span data-ttu-id="d0125-215">A SAS URL used to download files has the following format:</span><span class="sxs-lookup"><span data-stu-id="d0125-215">A SAS URL used to download files has the following format:</span></span>

<span data-ttu-id="d0125-216">{blob container name}/{asset name}/{file name}/{SAS signature}</span><span class="sxs-lookup"><span data-stu-id="d0125-216">{blob container name}/{asset name}/{file name}/{SAS signature}</span></span>

<span data-ttu-id="d0125-217">Media Services .NET SDK extensions provide convenient helper methods that return formatted URLs for the published asset.</span><span class="sxs-lookup"><span data-stu-id="d0125-217">Media Services .NET SDK extensions provide convenient helper methods that return formatted URLs for the published asset.</span></span>

<span data-ttu-id="d0125-218">The following code uses .NET SDK Extensions to create locators and to get streaming and progressive download URLs.</span><span class="sxs-lookup"><span data-stu-id="d0125-218">The following code uses .NET SDK Extensions to create locators and to get streaming and progressive download URLs.</span></span> <span data-ttu-id="d0125-219">The code also shows how to download files to a local folder.</span><span class="sxs-lookup"><span data-stu-id="d0125-219">The code also shows how to download files to a local folder.</span></span>

<span data-ttu-id="d0125-220">Add the following method to the Program class.</span><span class="sxs-lookup"><span data-stu-id="d0125-220">Add the following method to the Program class.</span></span>

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

## <a name="test-by-playing-your-content"></a><span data-ttu-id="d0125-221">Test by playing your content</span><span class="sxs-lookup"><span data-stu-id="d0125-221">Test by playing your content</span></span>

<span data-ttu-id="d0125-222">Once you run the program defined in the previous section, the URLs similar to the following will be displayed in the console window.</span><span class="sxs-lookup"><span data-stu-id="d0125-222">Once you run the program defined in the previous section, the URLs similar to the following will be displayed in the console window.</span></span>

<span data-ttu-id="d0125-223">Adaptive streaming URLs:</span><span class="sxs-lookup"><span data-stu-id="d0125-223">Adaptive streaming URLs:</span></span>

<span data-ttu-id="d0125-224">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="d0125-224">Smooth Streaming</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="d0125-225">HLS</span><span class="sxs-lookup"><span data-stu-id="d0125-225">HLS</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="d0125-226">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="d0125-226">MPEG DASH</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

<span data-ttu-id="d0125-227">Progressive download URLs (audio and video).</span><span class="sxs-lookup"><span data-stu-id="d0125-227">Progressive download URLs (audio and video).</span></span>

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


<span data-ttu-id="d0125-228">To stream your video, paste your URL in the URL textbox in the [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="d0125-228">To stream your video, paste your URL in the URL textbox in the [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="d0125-229">To test progressive download, paste a URL into a browser (for example, Internet Explorer, Chrome, or Safari).</span><span class="sxs-lookup"><span data-stu-id="d0125-229">To test progressive download, paste a URL into a browser (for example, Internet Explorer, Chrome, or Safari).</span></span>

<span data-ttu-id="d0125-230">For more information, see the following topics:</span><span class="sxs-lookup"><span data-stu-id="d0125-230">For more information, see the following topics:</span></span>

- [<span data-ttu-id="d0125-231">Playing your content with existing players</span><span class="sxs-lookup"><span data-stu-id="d0125-231">Playing your content with existing players</span></span>](media-services-playback-content-with-existing-players.md)
- [<span data-ttu-id="d0125-232">Develop video player applications</span><span class="sxs-lookup"><span data-stu-id="d0125-232">Develop video player applications</span></span>](media-services-develop-video-players.md)
- [<span data-ttu-id="d0125-233">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span><span class="sxs-lookup"><span data-stu-id="d0125-233">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a><span data-ttu-id="d0125-234">Download sample</span><span class="sxs-lookup"><span data-stu-id="d0125-234">Download sample</span></span>
<span data-ttu-id="d0125-235">The following code sample contains the code that you created in this tutorial: [sample](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="d0125-235">The following code sample contains the code that you created in this tutorial: [sample](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0125-236">Next Steps</span><span class="sxs-lookup"><span data-stu-id="d0125-236">Next Steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d0125-237">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="d0125-237">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/


