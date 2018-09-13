---
title: Configuring Azure Media Services telemetry with .NET| Microsoft Docs
description: This article shows you how to use the Azure Media Services telemetry using .NET SDK.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: f8f55e37-0714-49ea-bf4a-e6c1319bec44
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/17/2016
ms.author: juliako
ms.openlocfilehash: da7d4f87fdcaca6517fa95152d42c138533772b9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554752"
---
# <a name="configuring-azure-media-services-telemetry-with-net"></a><span data-ttu-id="c80e1-103">Configuring Azure Media Services telemetry with .NET</span><span class="sxs-lookup"><span data-stu-id="c80e1-103">Configuring Azure Media Services telemetry with .NET</span></span>

<span data-ttu-id="c80e1-104">This topic describes general steps that you might take when configuring the Azure Media Services (AMS) telemetry using .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="c80e1-104">This topic describes general steps that you might take when configuring the Azure Media Services (AMS) telemetry using .NET SDK.</span></span> 

>[!NOTE]
><span data-ttu-id="c80e1-105">For the detailed explanation of what is AMS telemetry and how to consume it, see the [overview](media-services-telemetry-overview.md) topic.</span><span class="sxs-lookup"><span data-stu-id="c80e1-105">For the detailed explanation of what is AMS telemetry and how to consume it, see the [overview](media-services-telemetry-overview.md) topic.</span></span>

<span data-ttu-id="c80e1-106">You can consume telemetry data in one of the following ways:</span><span class="sxs-lookup"><span data-stu-id="c80e1-106">You can consume telemetry data in one of the following ways:</span></span>

- <span data-ttu-id="c80e1-107">Read data directly from Azure Table Storage (e.g. using the Storage SDK).</span><span class="sxs-lookup"><span data-stu-id="c80e1-107">Read data directly from Azure Table Storage (e.g. using the Storage SDK).</span></span> <span data-ttu-id="c80e1-108">For the description of telemetry storage tables, see the **Consuming telemetry information** in [this](https://msdn.microsoft.com/library/mt742089.aspx) topic.</span><span class="sxs-lookup"><span data-stu-id="c80e1-108">For the description of telemetry storage tables, see the **Consuming telemetry information** in [this](https://msdn.microsoft.com/library/mt742089.aspx) topic.</span></span>

<span data-ttu-id="c80e1-109">Or</span><span class="sxs-lookup"><span data-stu-id="c80e1-109">Or</span></span>

- <span data-ttu-id="c80e1-110">Use the support in the Media Services .NET SDK for reading storage data.</span><span class="sxs-lookup"><span data-stu-id="c80e1-110">Use the support in the Media Services .NET SDK for reading storage data.</span></span> <span data-ttu-id="c80e1-111">This topic shows how to enable telemetry for the specified AMS account and how to query the metrics using the Azure Media Services .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="c80e1-111">This topic shows how to enable telemetry for the specified AMS account and how to query the metrics using the Azure Media Services .NET SDK.</span></span>  

## <a name="configuring-telemetry-for-a-media-services-account"></a><span data-ttu-id="c80e1-112">Configuring telemetry for a Media Services account</span><span class="sxs-lookup"><span data-stu-id="c80e1-112">Configuring telemetry for a Media Services account</span></span>

<span data-ttu-id="c80e1-113">The following steps are needed to enable telemetry:</span><span class="sxs-lookup"><span data-stu-id="c80e1-113">The following steps are needed to enable telemetry:</span></span>

- <span data-ttu-id="c80e1-114">Get the credentials of the storage account attached to the Media Services account.</span><span class="sxs-lookup"><span data-stu-id="c80e1-114">Get the credentials of the storage account attached to the Media Services account.</span></span> 
- <span data-ttu-id="c80e1-115">Create a Notification Endpoint with **EndPointType** set to **AzureTable** and endPointAddress pointing to the storage table.</span><span class="sxs-lookup"><span data-stu-id="c80e1-115">Create a Notification Endpoint with **EndPointType** set to **AzureTable** and endPointAddress pointing to the storage table.</span></span>

        INotificationEndPoint notificationEndPoint = 
                      _context.NotificationEndPoints.Create("monitoring", 
                      NotificationEndPointType.AzureTable,
                      "https://" + _mediaServicesStorageAccountName + ".table.core.windows.net/");

- <span data-ttu-id="c80e1-116">Create a monitoring configuration settings for the services you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="c80e1-116">Create a monitoring configuration settings for the services you want to monitor.</span></span> <span data-ttu-id="c80e1-117">No more than one monitoring configuration settings is allowed.</span><span class="sxs-lookup"><span data-stu-id="c80e1-117">No more than one monitoring configuration settings is allowed.</span></span> 
  
        IMonitoringConfiguration monitoringConfiguration = _context.MonitoringConfigurations.Create(notificationEndPoint.Id,
            new List<ComponentMonitoringSetting>()
            {
                new ComponentMonitoringSetting(MonitoringComponent.Channel, MonitoringLevel.Normal),
                new ComponentMonitoringSetting(MonitoringComponent.StreamingEndpoint, MonitoringLevel.Normal)
            });

## <a name="consuming-telemetry-information"></a><span data-ttu-id="c80e1-118">Consuming telemetry information</span><span class="sxs-lookup"><span data-stu-id="c80e1-118">Consuming telemetry information</span></span>

<span data-ttu-id="c80e1-119">For information about consuming telemetry information, see [this](media-services-telemetry-overview.md) topic.</span><span class="sxs-lookup"><span data-stu-id="c80e1-119">For information about consuming telemetry information, see [this](media-services-telemetry-overview.md) topic.</span></span>
 
## <a name="example"></a><span data-ttu-id="c80e1-120">Example</span><span class="sxs-lookup"><span data-stu-id="c80e1-120">Example</span></span>  
    
<span data-ttu-id="c80e1-121">The example shown in this section assumes that you have the following section in your App.config file.</span><span class="sxs-lookup"><span data-stu-id="c80e1-121">The example shown in this section assumes that you have the following section in your App.config file.</span></span>
    
    <appSettings>
      <add key="MediaServicesAccountName" value="ams_acct_name" />
      <add key="MediaServicesAccountKey" value="ams_acct_key" />
      <add key="MediaServicesAccountID" value="ams_acct_id" />
      <add key="StorageAccountName" value="storage_name" />
      <add key="StorageAccountKey" value="storage_key" />
    </appSettings>

<span data-ttu-id="c80e1-122">The following example shows how to enable telemetry for the specified AMS account and how to query the metrics using the Azure Media Services .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="c80e1-122">The following example shows how to enable telemetry for the specified AMS account and how to query the metrics using the Azure Media Services .NET SDK.</span></span>  

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    
    namespace AMSMetrics
    {
        class Program
        {
            private static readonly string _mediaServicesAccountName =
                ConfigurationManager.AppSettings["MediaServicesAccountName"];
            private static readonly string _mediaServicesAccountKey =
                ConfigurationManager.AppSettings["MediaServicesAccountKey"];
            private static readonly string _mediaServicesAccountID =
                ConfigurationManager.AppSettings["MediaServicesAccountID"];
            private static readonly string _mediaServicesStorageAccountName =
                ConfigurationManager.AppSettings["StorageAccountName"];
            private static readonly string _mediaServicesStorageAccountKey =
                ConfigurationManager.AppSettings["StorageAccountKey"];
    
            // Field for service context.
            private static CloudMediaContext _context = null;
            private static MediaServicesCredentials _cachedCredentials = null;
    
            private static IStreamingEndpoint _streamingEndpoint = null;
            private static IChannel _channel = null;
    
            static void Main(string[] args)
            {
                // Create and cache the Media Services credentials in a static class variable.
                _cachedCredentials = new MediaServicesCredentials(
                                _mediaServicesAccountName,
                                _mediaServicesAccountKey);
                // Used the cached credentials to create CloudMediaContext.
                _context = new CloudMediaContext(_cachedCredentials);
    
                _streamingEndpoint = _context.StreamingEndpoints.FirstOrDefault();
                _channel = _context.Channels.FirstOrDefault();
    
                var monitoringConfigurations = _context.MonitoringConfigurations;
                IMonitoringConfiguration monitoringConfiguration = null;
    
                // No more than one monitoring configuration settings is allowed.
                if (monitoringConfigurations.ToArray().Length != 0)
                {
                    monitoringConfiguration = _context.MonitoringConfigurations.FirstOrDefault();
                }
                else
                {
                    INotificationEndPoint notificationEndPoint =
                                  _context.NotificationEndPoints.Create("monitoring",
                                  NotificationEndPointType.AzureTable, GetTableEndPoint());
    
                    monitoringConfiguration = _context.MonitoringConfigurations.Create(notificationEndPoint.Id,
                        new List<ComponentMonitoringSetting>()
                        {
                            new ComponentMonitoringSetting(MonitoringComponent.Channel, MonitoringLevel.Normal),
                            new ComponentMonitoringSetting(MonitoringComponent.StreamingEndpoint, MonitoringLevel.Normal)
    
                        });
                }
    
                //Print metrics for a Streaming Endpoint.
                PrintStreamingEndpointMetrics();
    
                Console.ReadLine();
            }
    
            private static string GetTableEndPoint()
            {
                return "https://" + _mediaServicesStorageAccountName + ".table.core.windows.net/";
            }
    
            private static void PrintStreamingEndpointMetrics()
            {
                Console.WriteLine(string.Format("Telemetry for streaming endpoint '{0}'", _streamingEndpoint.Name));
    
                var end = DateTime.UtcNow;
                var start = DateTime.UtcNow.AddHours(-5);
    
                // Get some streaming endpoint metrics.
                var res = _context.StreamingEndPointRequestLogs.GetStreamingEndPointMetrics(
                        GetTableEndPoint(),
                        _mediaServicesStorageAccountKey,
                        _mediaServicesAccountID,
                        _streamingEndpoint.Id,
                        start,
                        end);
    
    
                Console.Title = "Streaming endpoint metrics:";
    
                foreach (var log in res)
                {
                    Console.WriteLine("AccountId: {0}", log.AccountId);
                    Console.WriteLine("BytesSent: {0}", log.BytesSent);
                    Console.WriteLine("EndToEndLatency: {0}", log.EndToEndLatency);
                    Console.WriteLine("HostName: {0}", log.HostName);
                    Console.WriteLine("ObservedTime: {0}", log.ObservedTime);
                    Console.WriteLine("PartitionKey: {0}", log.PartitionKey);
                    Console.WriteLine("RequestCount: {0}", log.RequestCount);
                    Console.WriteLine("ResultCode: {0}", log.ResultCode);
                    Console.WriteLine("RowKey: {0}", log.RowKey);
                    Console.WriteLine("ServerLatency: {0}", log.ServerLatency);
                    Console.WriteLine("StatusCode: {0}", log.StatusCode);
                    Console.WriteLine("StreamingEndpointId: {0}", log.StreamingEndpointId);
                    Console.WriteLine();
                }
    
                Console.WriteLine();
            }
    
            private static void PrintChannelMetrics()
            {
                if (_channel == null)
                {
                    Console.WriteLine("There are no channels in this AMS account");
                    return;
                }
    
                Console.WriteLine(string.Format("Telemetry for channel '{0}'", _channel.Name));
    
                var end = DateTime.UtcNow;
                var start = DateTime.UtcNow.AddHours(-5);
    
                // Get some channel metrics.
                var channelMetrics = _context.ChannelMetrics.GetChannelMetrics(
                    GetTableEndPoint(),
                    _mediaServicesStorageAccountKey,
                    _mediaServicesAccountID,
                   _channel.Id,
                    start,
                    end);
    
                // Print the channel metrics.
                Console.WriteLine("Channel metrics:");
    
                foreach (var channelHeartbeat in channelMetrics.OrderBy(x => x.ObservedTime))
                {
                    Console.WriteLine(
                        "    Observed time: {0}, Last timestamp: {1}, Incoming bitrate: {2}",
                        channelHeartbeat.ObservedTime,
                        channelHeartbeat.LastTimestamp,
                        channelHeartbeat.IncomingBitrate);
                }
    
                Console.WriteLine();
            }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="c80e1-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="c80e1-123">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c80e1-124">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="c80e1-124">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]