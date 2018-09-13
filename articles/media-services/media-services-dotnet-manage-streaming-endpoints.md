---
title: Manage streaming endpoints with .NET SDK. | Microsoft Docs
description: This topic shows how to manage streaming endpoints with the Azure portal.
services: media-services
documentationcenter: ''
author: Juliako
writer: juliako
manager: erikre
editor: ''
ms.assetid: 0da34a97-f36c-48d0-8ea2-ec12584a2215
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako
ms.openlocfilehash: 68011ef634b1f3bdeb7c219a46e1307698a12f7e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540766"
---
# <a name="manage-streaming-endpoints-with-net-sdk"></a><span data-ttu-id="6adaa-104">Manage streaming endpoints with .NET SDK</span><span class="sxs-lookup"><span data-stu-id="6adaa-104">Manage streaming endpoints with .NET SDK</span></span>

>[!NOTE]
><span data-ttu-id="6adaa-105">Make sure to review the [overview](media-services-streaming-endpoints-overview.md) topic.</span><span class="sxs-lookup"><span data-stu-id="6adaa-105">Make sure to review the [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> <span data-ttu-id="6adaa-106">Also, review [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="6adaa-106">Also, review [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="6adaa-107">The code in this topic shows how to do the following tasks using the Azure Media Services .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="6adaa-107">The code in this topic shows how to do the following tasks using the Azure Media Services .NET SDK:</span></span>

- <span data-ttu-id="6adaa-108">Examine the default streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="6adaa-108">Examine the default streaming endpoint.</span></span>
- <span data-ttu-id="6adaa-109">Create/add new streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="6adaa-109">Create/add new streaming endpoint.</span></span>

    <span data-ttu-id="6adaa-110">You might want to have multiple streaming endpoints if you plan to have different CDNs or a CDN and direct access.</span><span class="sxs-lookup"><span data-stu-id="6adaa-110">You might want to have multiple streaming endpoints if you plan to have different CDNs or a CDN and direct access.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6adaa-111">You are only billed when your Streaming Endpoint is in running state.</span><span class="sxs-lookup"><span data-stu-id="6adaa-111">You are only billed when your Streaming Endpoint is in running state.</span></span>
    
- <span data-ttu-id="6adaa-112">Update the streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="6adaa-112">Update the streaming endpoint.</span></span>
    
    <span data-ttu-id="6adaa-113">Make sure to call the Update() function.</span><span class="sxs-lookup"><span data-stu-id="6adaa-113">Make sure to call the Update() function.</span></span>

- <span data-ttu-id="6adaa-114">Delete the streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="6adaa-114">Delete the streaming endpoint.</span></span>

    >[!NOTE]
    ><span data-ttu-id="6adaa-115">The default streaming endpoint cannot be deleted.</span><span class="sxs-lookup"><span data-stu-id="6adaa-115">The default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="6adaa-116">For information about how to scale the streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span><span class="sxs-lookup"><span data-stu-id="6adaa-116">For information about how to scale the streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>


###<a name="set-up-the-visual-studio-project"></a><span data-ttu-id="6adaa-117">Set up the Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="6adaa-117">Set up the Visual Studio project</span></span>

1. <span data-ttu-id="6adaa-118">Create a new C# Console Application in Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="6adaa-118">Create a new C# Console Application in Visual Studio 2015.</span></span>  
2. <span data-ttu-id="6adaa-119">Build the solution.</span><span class="sxs-lookup"><span data-stu-id="6adaa-119">Build the solution.</span></span>
3. <span data-ttu-id="6adaa-120">Use **NuGet** to install the [latest Azure Media Services .NET SDK package](https://www.nuget.org/packages/windowsazure.mediaservices/).</span><span class="sxs-lookup"><span data-stu-id="6adaa-120">Use **NuGet** to install the [latest Azure Media Services .NET SDK package](https://www.nuget.org/packages/windowsazure.mediaservices/).</span></span>   
4. <span data-ttu-id="6adaa-121">Add the appSettings section to the .config file and update the Media Services name and key values.</span><span class="sxs-lookup"><span data-stu-id="6adaa-121">Add the appSettings section to the .config file and update the Media Services name and key values.</span></span> 
    
        <appSettings>
          <add key="MediaServicesAccountName" value="Media-Services-Account-Name"/>
          <add key="MediaServicesAccountKey" value="Media-Services-Account-Key"/>
        </appSettings>

###<a name="add-code-that-manages-streaming-endpoints"></a><span data-ttu-id="6adaa-122">Add code that manages streaming endpoints</span><span class="sxs-lookup"><span data-stu-id="6adaa-122">Add code that manages streaming endpoints</span></span>
    
<span data-ttu-id="6adaa-123">Replace the code in the Program.cs with the following code:</span><span class="sxs-lookup"><span data-stu-id="6adaa-123">Replace the code in the Program.cs with the following code:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.Live;
    
    namespace AMSStreamingEndpoint
    {
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
                // Create and cache the Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName,
                                _mediaServicesAccountKey);
                // Used the cached credentials to create CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);
    
                var defaultStreamingEndpoint = _context.StreamingEndpoints.Where(s=>s.Name.Contains("default")).FirstOrDefault();
                ExamineStreamingEndpoint(defaultStreamingEndpoint);
    
                IStreamingEndpoint newStreamingEndpoint = AddStreamingEndpoint();
                UpdateStreamingEndpoint(newStreamingEndpoint);
                DeleteStreamingEndpoint(newStreamingEndpoint);
            }
    
            static public void ExamineStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
            {
                Console.WriteLine(streamingEndpoint.Name);
                Console.WriteLine(streamingEndpoint.StreamingEndpointVersion);
                Console.WriteLine(streamingEndpoint.FreeTrialEndTime);
                Console.WriteLine(streamingEndpoint.ScaleUnits);
                Console.WriteLine(streamingEndpoint.CdnProvider);
                Console.WriteLine(streamingEndpoint.CdnProfile);
                Console.WriteLine(streamingEndpoint.CdnEnabled);
            }
    
            static public IStreamingEndpoint AddStreamingEndpoint()
            {
                var name = "StreamingEndpoint" + DateTime.UtcNow.ToString("hhmmss");
                var option = new StreamingEndpointCreationOptions(name, 1)
                {
                    StreamingEndpointVersion = new Version("2.0"),
                    CdnEnabled = true,
                    CdnProfile = "CdnProfile",
                    CdnProvider = CdnProviderType.PremiumVerizon
                };
    
                var streamingEndpoint = _context.StreamingEndpoints.Create(option);
    
                return streamingEndpoint;
            }
    
            static public void UpdateStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
            {
                if(streamingEndpoint.StreamingEndpointVersion == "1.0")
                    streamingEndpoint.StreamingEndpointVersion = "2.0";
    
                streamingEndpoint.CdnEnabled = false;
                streamingEndpoint.Update();
            }
    
            static public void DeleteStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
            {
                streamingEndpoint.Delete();
            }
        }
    }
    

## <a name="next-steps"></a><span data-ttu-id="6adaa-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="6adaa-124">Next steps</span></span>
<span data-ttu-id="6adaa-125">Review Media Services learning paths.</span><span class="sxs-lookup"><span data-stu-id="6adaa-125">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6adaa-126">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="6adaa-126">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

