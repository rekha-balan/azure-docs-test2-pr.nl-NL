---
title: How to perform live streaming with on-premise encoders using .NET | Microsoft Docs
description: This topic shows how to use .NET to perform live encoding with on-premises encoders.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 15908152-d23c-4d55-906a-3bfd74927db5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: cenkdin;juliako
ms.openlocfilehash: 67d446263c7a884cd8d22e88e6fb607b1399d9aa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549508"
---
# <a name="how-to-perform-live-streaming-with-on-premise-encoders-using-net"></a><span data-ttu-id="bfc73-103">How to perform live streaming with on-premise encoders using .NET</span><span class="sxs-lookup"><span data-stu-id="bfc73-103">How to perform live streaming with on-premise encoders using .NET</span></span>
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-live-passthrough-get-started.md)
> * [.NET](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="bfc73-107">This tutorial walks you through the steps of using the Azure Media Services .NET SDK to create a **Channel** that is configured for a pass-through delivery.</span><span class="sxs-lookup"><span data-stu-id="bfc73-107">This tutorial walks you through the steps of using the Azure Media Services .NET SDK to create a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bfc73-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bfc73-108">Prerequisites</span></span>
<span data-ttu-id="bfc73-109">The following are required to complete the tutorial:</span><span class="sxs-lookup"><span data-stu-id="bfc73-109">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="bfc73-110">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="bfc73-110">An Azure account.</span></span>
* <span data-ttu-id="bfc73-111">A Media Services account.</span><span class="sxs-lookup"><span data-stu-id="bfc73-111">A Media Services account.</span></span>    <span data-ttu-id="bfc73-112">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="bfc73-112">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="bfc73-113">Set up your dev environment.</span><span class="sxs-lookup"><span data-stu-id="bfc73-113">Set up your dev environment.</span></span> <span data-ttu-id="bfc73-114">For more information, see [Set up your environment](media-services-set-up-computer.md).</span><span class="sxs-lookup"><span data-stu-id="bfc73-114">For more information, see [Set up your environment](media-services-set-up-computer.md).</span></span>
* <span data-ttu-id="bfc73-115">A webcam.</span><span class="sxs-lookup"><span data-stu-id="bfc73-115">A webcam.</span></span> <span data-ttu-id="bfc73-116">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="bfc73-116">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="bfc73-117">Recommended to review the following articles:</span><span class="sxs-lookup"><span data-stu-id="bfc73-117">Recommended to review the following articles:</span></span>

* [<span data-ttu-id="bfc73-118">Azure Media Services RTMP Support and Live Encoders</span><span class="sxs-lookup"><span data-stu-id="bfc73-118">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="bfc73-119">Live streaming with on-premise encoders that create multi-bitrate streams</span><span class="sxs-lookup"><span data-stu-id="bfc73-119">Live streaming with on-premise encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <a name="example"></a><span data-ttu-id="bfc73-120">Example</span><span class="sxs-lookup"><span data-stu-id="bfc73-120">Example</span></span>
<span data-ttu-id="bfc73-121">The following code example demonstrates how to achieve the following tasks:</span><span class="sxs-lookup"><span data-stu-id="bfc73-121">The following code example demonstrates how to achieve the following tasks:</span></span>

* <span data-ttu-id="bfc73-122">Connect to Media Services</span><span class="sxs-lookup"><span data-stu-id="bfc73-122">Connect to Media Services</span></span>
* <span data-ttu-id="bfc73-123">Create a channel</span><span class="sxs-lookup"><span data-stu-id="bfc73-123">Create a channel</span></span>
* <span data-ttu-id="bfc73-124">Update the channel</span><span class="sxs-lookup"><span data-stu-id="bfc73-124">Update the channel</span></span>
* <span data-ttu-id="bfc73-125">Retrieve the channel’s input endpoint.</span><span class="sxs-lookup"><span data-stu-id="bfc73-125">Retrieve the channel’s input endpoint.</span></span> <span data-ttu-id="bfc73-126">The input endpoint should be provided to the on-premises live encoder.</span><span class="sxs-lookup"><span data-stu-id="bfc73-126">The input endpoint should be provided to the on-premises live encoder.</span></span> <span data-ttu-id="bfc73-127">The live encoder converts signals from the camera to streams that are sent to the channel’s input (ingest) endpoint.</span><span class="sxs-lookup"><span data-stu-id="bfc73-127">The live encoder converts signals from the camera to streams that are sent to the channel’s input (ingest) endpoint.</span></span>
* <span data-ttu-id="bfc73-128">Retrieve the channel’s preview endpoint</span><span class="sxs-lookup"><span data-stu-id="bfc73-128">Retrieve the channel’s preview endpoint</span></span>
* <span data-ttu-id="bfc73-129">Create and start a program</span><span class="sxs-lookup"><span data-stu-id="bfc73-129">Create and start a program</span></span>
* <span data-ttu-id="bfc73-130">Create a locator needed to access the program</span><span class="sxs-lookup"><span data-stu-id="bfc73-130">Create a locator needed to access the program</span></span>
* <span data-ttu-id="bfc73-131">Create and start a StreamingEndpoint</span><span class="sxs-lookup"><span data-stu-id="bfc73-131">Create and start a StreamingEndpoint</span></span>
* <span data-ttu-id="bfc73-132">Update the streaming endpoint</span><span class="sxs-lookup"><span data-stu-id="bfc73-132">Update the streaming endpoint</span></span>
* <span data-ttu-id="bfc73-133">Get locators for all your streaming endpoints</span><span class="sxs-lookup"><span data-stu-id="bfc73-133">Get locators for all your streaming endpoints</span></span>
* <span data-ttu-id="bfc73-134">Shut down resources</span><span class="sxs-lookup"><span data-stu-id="bfc73-134">Shut down resources</span></span>

>[!NOTE]
>Make sure the streaming endpoint from which you want to stream content is in the **Running** state. 
    
    
>[!NOTE]
>There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy). You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies). For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.

<span data-ttu-id="bfc73-139">For information on how to configure a live encoder, see [Azure Media Services RTMP Support and Live Encoders](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/).</span><span class="sxs-lookup"><span data-stu-id="bfc73-139">For information on how to configure a live encoder, see [Azure Media Services RTMP Support and Live Encoders](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/).</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Net;
    using System.Security.Cryptography;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Newtonsoft.Json.Linq;

    namespace AMSLiveTest
    {
        class Program
        {
            private const string StreamingEndpointName = "streamingendpoint001";
            private const string ChannelName = "channel001";
            private const string AssetlName = "asset001";
            private const string ProgramlName = "program001";

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

                IChannel channel = CreateAndStartChannel();

                // Set the Live Encoder to point to the channel's input endpoint:
                string ingestUrl = channel.Input.Endpoints.FirstOrDefault().Url.ToString();

                // Use the previewEndpoint to preview and verify
                // that the input from the encoder is actually reaching the Channel.
                string previewEndpoint = channel.Preview.Endpoints.FirstOrDefault().Url.ToString();

                IProgram program = CreateAndStartProgram(channel);
                ILocator locator = CreateLocatorForAsset(program.Asset, program.ArchiveWindowLength);
                IStreamingEndpoint streamingEndpoint = CreateAndStartStreamingEndpoint();
                GetLocatorsInAllStreamingEndpoints(program.Asset);

                // Once you are done streaming, clean up your resources.
                Cleanup(streamingEndpoint, channel);
            }

            public static IChannel CreateAndStartChannel()
            {
                //If you want to change the Smooth fragments to HLS segment ratio, you would set the ChannelCreationOptions’s Output property.

                IChannel channel = _context.Channels.Create(
                new ChannelCreationOptions
                {
                Name = ChannelName,
                Input = CreateChannelInput(),
                Preview = CreateChannelPreview()
                });

                //Starting and stopping Channels can take some time to execute. To determine the state of operations after calling Start or Stop, query the IChannel.State .

                channel.Start();

                return channel;
            }

            private static ChannelInput CreateChannelInput()
            {
                return new ChannelInput
                {
                    StreamingProtocol = StreamingProtocol.RTMP,
                    AccessControl = new ChannelAccessControl
                    {
                        IPAllowList = new List<IPRange>
                                {
                                new IPRange
                            {
                                Name = "TestChannelInput001",
                                // Setting 0.0.0.0 for Address and 0 for SubnetPrefixLength
                                // will allow access to IP addresses.
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                    }
                };
            }

            private static ChannelPreview CreateChannelPreview()
            {
                return new ChannelPreview
                {
                    AccessControl = new ChannelAccessControl
                    {
                        IPAllowList = new List<IPRange>
                        {
                            new IPRange
                            {
                                Name = "TestChannelPreview001",
                                // Setting 0.0.0.0 for Address and 0 for SubnetPrefixLength
                                // will allow access to IP addresses.
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                    }
                };
            }

            public static void UpdateCrossSiteAccessPoliciesForChannel(IChannel channel)
            {
                var clientPolicy =
                    @"<?xml version=""1.0"" encoding=""utf-8""?>
                <access-policy>
                    <cross-domain-access>
                        <policy>
                            <allow-from http-request-headers=""*"" http-methods=""*"">
                                <domain uri=""*""/>
                            </allow-from>
                            <grant-to>
                               <resource path=""/"" include-subpaths=""true""/>
                            </grant-to>
                        </policy>
                    </cross-domain-access>
                </access-policy>";

                var xdomainPolicy =
                    @"<?xml version=""1.0"" ?>
                <cross-domain-policy>
                    <allow-access-from domain=""*"" />
                </cross-domain-policy>";

                channel.CrossSiteAccessPolicies.ClientAccessPolicy = clientPolicy;
                channel.CrossSiteAccessPolicies.CrossDomainPolicy = xdomainPolicy;

                channel.Update();
            }

            public static IProgram CreateAndStartProgram(IChannel channel)
            {
                IAsset asset = _context.Assets.Create(AssetlName, AssetCreationOptions.None);

                // Create a Program on the Channel. You can have multiple Programs that overlap or are sequential;
                // however each Program must have a unique name within your Media Services account.
                IProgram program = channel.Programs.Create(ProgramlName, TimeSpan.FromHours(3), asset.Id);
                program.Start();

                return program;
            }

            public static ILocator CreateLocatorForAsset(IAsset asset, TimeSpan ArchiveWindowLength)
            {
                // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            

                var locator = _context.Locators.CreateLocator
                    (
                        LocatorType.OnDemandOrigin,
                        asset,
                        _context.AccessPolicies.Create
                        (
                            "Live Stream Policy",
                            ArchiveWindowLength,
                            AccessPermissions.Read
                        )
                    );

                return locator;
            }

            public static IStreamingEndpoint CreateAndStartStreamingEndpoint()
            {
                var options = new StreamingEndpointCreationOptions
                {
                    Name = StreamingEndpointName,
                    ScaleUnits = 1,
                    AccessControl = GetAccessControl(),
                    CacheControl = GetCacheControl()
                };

                IStreamingEndpoint streamingEndpoint = _context.StreamingEndpoints.Create(options);
                streamingEndpoint.Start();

                return streamingEndpoint;
            }

            private static StreamingEndpointAccessControl GetAccessControl()
            {
                return new StreamingEndpointAccessControl
                {
                    IPAllowList = new List<IPRange>
                    {
                        new IPRange
                        {
                            Name = "Allow all",
                            Address = IPAddress.Parse("0.0.0.0"),
                            SubnetPrefixLength = 0
                        }
                    },

                    AkamaiSignatureHeaderAuthenticationKeyList = new List<AkamaiSignatureHeaderAuthenticationKey>
                    {
                        new AkamaiSignatureHeaderAuthenticationKey
                        {
                            Identifier = "My key",
                            Expiration = DateTime.UtcNow + TimeSpan.FromDays(365),
                            Base64Key = Convert.ToBase64String(GenerateRandomBytes(16))
                        }
                    }
                };
            }

            private static byte[] GenerateRandomBytes(int length)
            {
                var bytes = new byte[length];
                using (var rng = new RNGCryptoServiceProvider())
                {
                    rng.GetBytes(bytes);
                }

                return bytes;
            }

            private static StreamingEndpointCacheControl GetCacheControl()
            {
                return new StreamingEndpointCacheControl
                {
                    MaxAge = TimeSpan.FromSeconds(1000)
                };
            }

            public static void UpdateCrossSiteAccessPoliciesForStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
            {
                var clientPolicy =
                    @"<?xml version=""1.0"" encoding=""utf-8""?>
                <access-policy>
                    <cross-domain-access>
                        <policy>
                            <allow-from http-request-headers=""*"" http-methods=""*"">
                                <domain uri=""*""/>
                            </allow-from>
                            <grant-to>
                               <resource path=""/"" include-subpaths=""true""/>
                            </grant-to>
                        </policy>
                    </cross-domain-access>
                </access-policy>";

                var xdomainPolicy =
                    @"<?xml version=""1.0"" ?>
                <cross-domain-policy>
                    <allow-access-from domain=""*"" />
                </cross-domain-policy>";

                streamingEndpoint.CrossSiteAccessPolicies.ClientAccessPolicy = clientPolicy;
                streamingEndpoint.CrossSiteAccessPolicies.CrossDomainPolicy = xdomainPolicy;

                streamingEndpoint.Update();
            }

            public static void GetLocatorsInAllStreamingEndpoints(IAsset asset)
            {
                var locators = asset.Locators.Where(l => l.Type == LocatorType.OnDemandOrigin);
                var ismFile = asset.AssetFiles.AsEnumerable().FirstOrDefault(a => a.Name.EndsWith(".ism"));
                var template = new UriTemplate("{contentAccessComponent}/{ismFileName}/manifest");
                var urls = locators.SelectMany(l =>
                            _context
                                .StreamingEndpoints
                                .AsEnumerable()
                                .Where(se => se.State == StreamingEndpointState.Running)
                                .Select(
                                    se =>
                                        template.BindByPosition(new Uri("http://" + se.HostName),
                                        l.ContentAccessComponent,
                                            ismFile.Name)))
                            .ToArray();

            }

            public static void Cleanup(IStreamingEndpoint streamingEndpoint,
                                        IChannel channel)
            {
                if (streamingEndpoint != null)
                {
                    streamingEndpoint.Stop();
                    streamingEndpoint.Delete();
                }

                IAsset asset;
                if (channel != null)
                {

                    foreach (var program in channel.Programs)
                    {
                        asset = _context.Assets.Where(se => se.Id == program.AssetId)
                                                .FirstOrDefault();

                        program.Stop();
                        program.Delete();

                        if (asset != null)
                        {
                            foreach (var l in asset.Locators)
                                l.Delete();

                            asset.Delete();
                        }
                    }

                    channel.Stop();
                    channel.Delete();
                }
            }
        }
    }

## <a name="next-step"></a><span data-ttu-id="bfc73-140">Next Step</span><span class="sxs-lookup"><span data-stu-id="bfc73-140">Next Step</span></span>
<span data-ttu-id="bfc73-141">Review Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="bfc73-141">Review Media Services learning paths</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bfc73-142">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="bfc73-142">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

