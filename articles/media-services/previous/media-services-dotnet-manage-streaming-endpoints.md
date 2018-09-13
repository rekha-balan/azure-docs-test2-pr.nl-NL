---
title: Manage streaming endpoints with .NET SDK. | Microsoft Docs
description: This article shows how to manage streaming endpoints with the Azure portal.
services: media-services
documentationcenter: ''
author: Juliako
writer: juliako
manager: cfowler
editor: ''
ms.assetid: 0da34a97-f36c-48d0-8ea2-ec12584a2215
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2017
ms.author: juliako
ms.openlocfilehash: 741eb35c58fb723985a60f6ac071892c02d08412
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865363"
---
# <a name="manage-streaming-endpoints-with-net-sdk"></a><span data-ttu-id="714b1-104">Manage streaming endpoints with .NET SDK</span><span class="sxs-lookup"><span data-stu-id="714b1-104">Manage streaming endpoints with .NET SDK</span></span>

>[!NOTE]
><span data-ttu-id="714b1-105">Make sure to review the [overview](media-services-streaming-endpoints-overview.md) article.</span><span class="sxs-lookup"><span data-stu-id="714b1-105">Make sure to review the [overview](media-services-streaming-endpoints-overview.md) article.</span></span> <span data-ttu-id="714b1-106">Also, review [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="714b1-106">Also, review [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="714b1-107">The code in this article shows how to do the following tasks using the Azure Media Services .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="714b1-107">The code in this article shows how to do the following tasks using the Azure Media Services .NET SDK:</span></span>

- <span data-ttu-id="714b1-108">Examine the default streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="714b1-108">Examine the default streaming endpoint.</span></span>
- <span data-ttu-id="714b1-109">Create/add new streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="714b1-109">Create/add new streaming endpoint.</span></span>

    <span data-ttu-id="714b1-110">You might want to have multiple streaming endpoints if you plan to have different CDNs or a CDN and direct access.</span><span class="sxs-lookup"><span data-stu-id="714b1-110">You might want to have multiple streaming endpoints if you plan to have different CDNs or a CDN and direct access.</span></span>

    > [!NOTE]
    > <span data-ttu-id="714b1-111">You are only billed when your Streaming Endpoint is in running state.</span><span class="sxs-lookup"><span data-stu-id="714b1-111">You are only billed when your Streaming Endpoint is in running state.</span></span>
    
- <span data-ttu-id="714b1-112">Update the streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="714b1-112">Update the streaming endpoint.</span></span>
    
    <span data-ttu-id="714b1-113">Make sure to call the Update() function.</span><span class="sxs-lookup"><span data-stu-id="714b1-113">Make sure to call the Update() function.</span></span>

- <span data-ttu-id="714b1-114">Delete the streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="714b1-114">Delete the streaming endpoint.</span></span>

    >[!NOTE]
    ><span data-ttu-id="714b1-115">The default streaming endpoint cannot be deleted.</span><span class="sxs-lookup"><span data-stu-id="714b1-115">The default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="714b1-116">For information about how to scale the streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) article.</span><span class="sxs-lookup"><span data-stu-id="714b1-116">For information about how to scale the streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) article.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="714b1-117">Create and configure a Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="714b1-117">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="714b1-118">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="714b1-118">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="add-code-that-manages-streaming-endpoints"></a><span data-ttu-id="714b1-119">Add code that manages streaming endpoints</span><span class="sxs-lookup"><span data-stu-id="714b1-119">Add code that manages streaming endpoints</span></span>
    
<span data-ttu-id="714b1-120">Replace the code in the Program.cs with the following code:</span><span class="sxs-lookup"><span data-stu-id="714b1-120">Replace the code in the Program.cs with the following code:</span></span>

```csharp
using System;
using System.Configuration;
using System.Linq;
using Microsoft.WindowsAzure.MediaServices.Client;
using Microsoft.WindowsAzure.MediaServices.Client.Live;

namespace AMSStreamingEndpoint
{
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
            AzureAdTokenCredentials tokenCredentials =
                new AzureAdTokenCredentials(_AADTenantDomain,
                    new AzureAdClientSymmetricKey(_AMSClientId, _AMSClientSecret),
                    AzureEnvironments.AzureCloudEnvironment);

            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            var defaultStreamingEndpoint = _context.StreamingEndpoints.Where(s => s.Name.Contains("default")).FirstOrDefault();
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
            if (streamingEndpoint.StreamingEndpointVersion == "1.0")
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
```

## <a name="next-steps"></a><span data-ttu-id="714b1-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="714b1-121">Next steps</span></span>
<span data-ttu-id="714b1-122">Review Media Services learning paths.</span><span class="sxs-lookup"><span data-stu-id="714b1-122">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="714b1-123">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="714b1-123">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

