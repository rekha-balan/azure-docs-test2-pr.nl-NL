---
title: Use Azure Webhooks to monitor Media Services job notifications with .NET | Microsoft Docs
description: Learn how to use Azure Webhooks to monitor Media Services job notifications. The code sample is written in C# and uses the Media Services SDK for .NET.
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.assetid: a61fe157-81b1-45c1-89f2-224b7ef55869
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 12/09/2017
ms.author: juliako
ms.openlocfilehash: 564fc25699c3ae627804d49bfdc40ae9dd559269
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857749"
---
# <a name="use-azure-webhooks-to-monitor-media-services-job-notifications-with-net"></a><span data-ttu-id="d9df8-104">Use Azure Webhooks to monitor Media Services job notifications with .NET</span><span class="sxs-lookup"><span data-stu-id="d9df8-104">Use Azure Webhooks to monitor Media Services job notifications with .NET</span></span>
<span data-ttu-id="d9df8-105">When you run jobs, you often require a way to track job progress.</span><span class="sxs-lookup"><span data-stu-id="d9df8-105">When you run jobs, you often require a way to track job progress.</span></span> <span data-ttu-id="d9df8-106">You can monitor Media Services job notifications by using Azure Webhooks or [Azure Queue storage](media-services-dotnet-check-job-progress-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="d9df8-106">You can monitor Media Services job notifications by using Azure Webhooks or [Azure Queue storage](media-services-dotnet-check-job-progress-with-queues.md).</span></span> <span data-ttu-id="d9df8-107">This article shows how to work with webhooks.</span><span class="sxs-lookup"><span data-stu-id="d9df8-107">This article shows how to work with webhooks.</span></span>

<span data-ttu-id="d9df8-108">This article shows how to</span><span class="sxs-lookup"><span data-stu-id="d9df8-108">This article shows how to</span></span>

*  <span data-ttu-id="d9df8-109">Define an Azure Function that is customized to respond to webhooks.</span><span class="sxs-lookup"><span data-stu-id="d9df8-109">Define an Azure Function that is customized to respond to webhooks.</span></span> 
    
    <span data-ttu-id="d9df8-110">In this case, the webhook is triggered by Media Services when your encoding job changes status.</span><span class="sxs-lookup"><span data-stu-id="d9df8-110">In this case, the webhook is triggered by Media Services when your encoding job changes status.</span></span> <span data-ttu-id="d9df8-111">The function listens for the webhook call back from Media Services notifications and publishes the output asset once the job finishes.</span><span class="sxs-lookup"><span data-stu-id="d9df8-111">The function listens for the webhook call back from Media Services notifications and publishes the output asset once the job finishes.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="d9df8-112">Before continuing, make sure you understand how [Azure Functions HTTP and webhook bindings](../../azure-functions/functions-bindings-http-webhook.md) work.</span><span class="sxs-lookup"><span data-stu-id="d9df8-112">Before continuing, make sure you understand how [Azure Functions HTTP and webhook bindings](../../azure-functions/functions-bindings-http-webhook.md) work.</span></span>
    >
    
* <span data-ttu-id="d9df8-113">Add a webhook to your encoding task and specify the webhook URL and secret key that this webhook responds to.</span><span class="sxs-lookup"><span data-stu-id="d9df8-113">Add a webhook to your encoding task and specify the webhook URL and secret key that this webhook responds to.</span></span> <span data-ttu-id="d9df8-114">You will find an example that adds a webhook to your encoding task at the end of the article.</span><span class="sxs-lookup"><span data-stu-id="d9df8-114">You will find an example that adds a webhook to your encoding task at the end of the article.</span></span>  

<span data-ttu-id="d9df8-115">You can find definitions of various Media Services .NET Azure Functions (including the one shown in this article) [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="d9df8-115">You can find definitions of various Media Services .NET Azure Functions (including the one shown in this article) [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9df8-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d9df8-116">Prerequisites</span></span>

<span data-ttu-id="d9df8-117">The following are required to complete the tutorial:</span><span class="sxs-lookup"><span data-stu-id="d9df8-117">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="d9df8-118">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="d9df8-118">An Azure account.</span></span> <span data-ttu-id="d9df8-119">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d9df8-119">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d9df8-120">A Media Services account.</span><span class="sxs-lookup"><span data-stu-id="d9df8-120">A Media Services account.</span></span> <span data-ttu-id="d9df8-121">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="d9df8-121">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="d9df8-122">Understanding of [how to use Azure Functions](../../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d9df8-122">Understanding of [how to use Azure Functions](../../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="d9df8-123">Also, review [Azure Functions HTTP and webhook bindings](../../azure-functions/functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="d9df8-123">Also, review [Azure Functions HTTP and webhook bindings](../../azure-functions/functions-bindings-http-webhook.md).</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="d9df8-124">Create a function app</span><span class="sxs-lookup"><span data-stu-id="d9df8-124">Create a function app</span></span>

1. <span data-ttu-id="d9df8-125">Go to the [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="d9df8-125">Go to the [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="d9df8-126">Create a function app as described [here](../../azure-functions/functions-create-function-app-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d9df8-126">Create a function app as described [here](../../azure-functions/functions-create-function-app-portal.md).</span></span>

## <a name="configure-function-app-settings"></a><span data-ttu-id="d9df8-127">Configure function app settings</span><span class="sxs-lookup"><span data-stu-id="d9df8-127">Configure function app settings</span></span>

<span data-ttu-id="d9df8-128">When developing Media Services functions, it is handy to add environment variables that will be used throughout your functions.</span><span class="sxs-lookup"><span data-stu-id="d9df8-128">When developing Media Services functions, it is handy to add environment variables that will be used throughout your functions.</span></span> <span data-ttu-id="d9df8-129">To configure app settings, click the Configure App Settings link.</span><span class="sxs-lookup"><span data-stu-id="d9df8-129">To configure app settings, click the Configure App Settings link.</span></span> 

<span data-ttu-id="d9df8-130">The [application settings](media-services-dotnet-how-to-use-azure-functions.md#configure-function-app-settings) section defines parameters that are used in the webhook defined in this article.</span><span class="sxs-lookup"><span data-stu-id="d9df8-130">The [application settings](media-services-dotnet-how-to-use-azure-functions.md#configure-function-app-settings) section defines parameters that are used in the webhook defined in this article.</span></span> <span data-ttu-id="d9df8-131">Also add the following parameters to the app settings.</span><span class="sxs-lookup"><span data-stu-id="d9df8-131">Also add the following parameters to the app settings.</span></span> 

|<span data-ttu-id="d9df8-132">Name</span><span class="sxs-lookup"><span data-stu-id="d9df8-132">Name</span></span>|<span data-ttu-id="d9df8-133">Definition</span><span class="sxs-lookup"><span data-stu-id="d9df8-133">Definition</span></span>|<span data-ttu-id="d9df8-134">Example</span><span class="sxs-lookup"><span data-stu-id="d9df8-134">Example</span></span>| 
|---|---|---|
|<span data-ttu-id="d9df8-135">SigningKey</span><span class="sxs-lookup"><span data-stu-id="d9df8-135">SigningKey</span></span> |<span data-ttu-id="d9df8-136">A signing key.</span><span class="sxs-lookup"><span data-stu-id="d9df8-136">A signing key.</span></span>| <span data-ttu-id="d9df8-137">j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt</span><span class="sxs-lookup"><span data-stu-id="d9df8-137">j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt</span></span>|
|<span data-ttu-id="d9df8-138">WebHookEndpoint</span><span class="sxs-lookup"><span data-stu-id="d9df8-138">WebHookEndpoint</span></span> | <span data-ttu-id="d9df8-139">A webhook endpoint address.</span><span class="sxs-lookup"><span data-stu-id="d9df8-139">A webhook endpoint address.</span></span> <span data-ttu-id="d9df8-140">Once your webhook function is created, you can copy the URL from the **Get function URL** link.</span><span class="sxs-lookup"><span data-stu-id="d9df8-140">Once your webhook function is created, you can copy the URL from the **Get function URL** link.</span></span> | <span data-ttu-id="d9df8-141">https://juliakofuncapp.azurewebsites.net/api/Notification_Webhook_Function?code=iN2phdrTnCxmvaKExFWOTulfnm4C71mMLIy8tzLr7Zvf6Z22HHIK5g==.</span><span class="sxs-lookup"><span data-stu-id="d9df8-141">https://juliakofuncapp.azurewebsites.net/api/Notification_Webhook_Function?code=iN2phdrTnCxmvaKExFWOTulfnm4C71mMLIy8tzLr7Zvf6Z22HHIK5g==.</span></span>|

## <a name="create-a-function"></a><span data-ttu-id="d9df8-142">Create a function</span><span class="sxs-lookup"><span data-stu-id="d9df8-142">Create a function</span></span>

<span data-ttu-id="d9df8-143">Once your function app is deployed, you can find it among **App Services** Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="d9df8-143">Once your function app is deployed, you can find it among **App Services** Azure Functions.</span></span>

1. <span data-ttu-id="d9df8-144">Select your function app and click **New Function**.</span><span class="sxs-lookup"><span data-stu-id="d9df8-144">Select your function app and click **New Function**.</span></span>
2. <span data-ttu-id="d9df8-145">Select **C#** code and **API & Webhooks** scenario.</span><span class="sxs-lookup"><span data-stu-id="d9df8-145">Select **C#** code and **API & Webhooks** scenario.</span></span> 
3. <span data-ttu-id="d9df8-146">Select **Generic Webhook - C#**.</span><span class="sxs-lookup"><span data-stu-id="d9df8-146">Select **Generic Webhook - C#**.</span></span>
4. <span data-ttu-id="d9df8-147">Name your webhook and press **Create**.</span><span class="sxs-lookup"><span data-stu-id="d9df8-147">Name your webhook and press **Create**.</span></span>

### <a name="files"></a><span data-ttu-id="d9df8-148">Files</span><span class="sxs-lookup"><span data-stu-id="d9df8-148">Files</span></span>

<span data-ttu-id="d9df8-149">Your Azure Function is associated with code files and other files that are described in this section.</span><span class="sxs-lookup"><span data-stu-id="d9df8-149">Your Azure Function is associated with code files and other files that are described in this section.</span></span> <span data-ttu-id="d9df8-150">By default, a function is associated with **function.json** and **run.csx** (C#) files.</span><span class="sxs-lookup"><span data-stu-id="d9df8-150">By default, a function is associated with **function.json** and **run.csx** (C#) files.</span></span> <span data-ttu-id="d9df8-151">You need to add a **project.json** file.</span><span class="sxs-lookup"><span data-stu-id="d9df8-151">You need to add a **project.json** file.</span></span> <span data-ttu-id="d9df8-152">The rest of this section shows the definitions for these files.</span><span class="sxs-lookup"><span data-stu-id="d9df8-152">The rest of this section shows the definitions for these files.</span></span>

![files](./media/media-services-azure-functions/media-services-azure-functions003.png)

#### <a name="functionjson"></a><span data-ttu-id="d9df8-154">function.json</span><span class="sxs-lookup"><span data-stu-id="d9df8-154">function.json</span></span>

<span data-ttu-id="d9df8-155">The function.json file defines the function bindings and other configuration settings.</span><span class="sxs-lookup"><span data-stu-id="d9df8-155">The function.json file defines the function bindings and other configuration settings.</span></span> <span data-ttu-id="d9df8-156">The runtime uses this file to determine the events to monitor and how to pass data into and return data from function execution.</span><span class="sxs-lookup"><span data-stu-id="d9df8-156">The runtime uses this file to determine the events to monitor and how to pass data into and return data from function execution.</span></span> 

```json
{
  "bindings": [
    {
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
      "name": "req"
    },
    {
      "type": "http",
      "direction": "out",
      "name": "res"
    }
  ],
  "disabled": false
}
```

#### <a name="projectjson"></a><span data-ttu-id="d9df8-157">project.json</span><span class="sxs-lookup"><span data-stu-id="d9df8-157">project.json</span></span>

<span data-ttu-id="d9df8-158">The project.json file contains dependencies.</span><span class="sxs-lookup"><span data-stu-id="d9df8-158">The project.json file contains dependencies.</span></span> 

```json
{
  "frameworks": {
    "net46":{
      "dependencies": {
        "windowsazure.mediaservices": "4.0.0.4",
        "windowsazure.mediaservices.extensions": "4.0.0.4",
        "Microsoft.IdentityModel.Clients.ActiveDirectory": "3.13.1",
        "Microsoft.IdentityModel.Protocol.Extensions": "1.0.2.206221351"
      }
    }
   }
}
```
    
#### <a name="runcsx"></a><span data-ttu-id="d9df8-159">run.csx</span><span class="sxs-lookup"><span data-stu-id="d9df8-159">run.csx</span></span>

<span data-ttu-id="d9df8-160">The code in this section shows an implementation of an Azure Function that is a webhook.</span><span class="sxs-lookup"><span data-stu-id="d9df8-160">The code in this section shows an implementation of an Azure Function that is a webhook.</span></span> <span data-ttu-id="d9df8-161">In this sample, the function listens for the webhook call back from Media Services notifications and publishes the output asset once the job finishes.</span><span class="sxs-lookup"><span data-stu-id="d9df8-161">In this sample, the function listens for the webhook call back from Media Services notifications and publishes the output asset once the job finishes.</span></span>

<span data-ttu-id="d9df8-162">The webhook expects a signing key (credential) to match the one you pass when you configure the notification endpoint.</span><span class="sxs-lookup"><span data-stu-id="d9df8-162">The webhook expects a signing key (credential) to match the one you pass when you configure the notification endpoint.</span></span> <span data-ttu-id="d9df8-163">The signing key is the 64-byte Base64 encoded value that is used to protect and secure your WebHooks callbacks from Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="d9df8-163">The signing key is the 64-byte Base64 encoded value that is used to protect and secure your WebHooks callbacks from Azure Media Services.</span></span> 

<span data-ttu-id="d9df8-164">In the webhook definition code that follows, the **VerifyWebHookRequestSignature** method does the verification of the notification message.</span><span class="sxs-lookup"><span data-stu-id="d9df8-164">In the webhook definition code that follows, the **VerifyWebHookRequestSignature** method does the verification of the notification message.</span></span> <span data-ttu-id="d9df8-165">The purpose of this validation is to ensure that the message was sent by Azure Media Services and hasn't been tampered with.</span><span class="sxs-lookup"><span data-stu-id="d9df8-165">The purpose of this validation is to ensure that the message was sent by Azure Media Services and hasn't been tampered with.</span></span> <span data-ttu-id="d9df8-166">The signature is optional for Azure Functions as it has the **Code** value as a query parameter over Transport Layer Security (TLS).</span><span class="sxs-lookup"><span data-stu-id="d9df8-166">The signature is optional for Azure Functions as it has the **Code** value as a query parameter over Transport Layer Security (TLS).</span></span> 

>[!NOTE]
><span data-ttu-id="d9df8-167">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="d9df8-167">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="d9df8-168">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span><span class="sxs-lookup"><span data-stu-id="d9df8-168">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="d9df8-169">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span><span class="sxs-lookup"><span data-stu-id="d9df8-169">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

```csharp
///////////////////////////////////////////////////
#r "Newtonsoft.Json"

using System;
using Microsoft.WindowsAzure.MediaServices.Client;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;
using System.IO;
using System.Globalization;
using Newtonsoft.Json;
using Microsoft.Azure;
using System.Net;
using System.Security.Cryptography;
using Microsoft.Azure.WebJobs;
using Microsoft.IdentityModel.Clients.ActiveDirectory;

internal const string SignatureHeaderKey = "sha256";
internal const string SignatureHeaderValueTemplate = SignatureHeaderKey + "={0}";
static string _webHookEndpoint = Environment.GetEnvironmentVariable("WebHookEndpoint");
static string _signingKey = Environment.GetEnvironmentVariable("SigningKey");

static readonly string _AADTenantDomain = Environment.GetEnvironmentVariable("AMSAADTenantDomain");
static readonly string _RESTAPIEndpoint = Environment.GetEnvironmentVariable("AMSRESTAPIEndpoint");

static readonly string _AMSClientId = Environment.GetEnvironmentVariable("AMSClientId");
static readonly string _AMSClientSecret = Environment.GetEnvironmentVariable("AMSClientSecret");

static CloudMediaContext _context = null;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

    Task<byte[]> taskForRequestBody = req.Content.ReadAsByteArrayAsync();
    byte[] requestBody = await taskForRequestBody;

    string jsonContent = await req.Content.ReadAsStringAsync();
    log.Info($"Request Body = {jsonContent}");

    IEnumerable<string> values = null;
    if (req.Headers.TryGetValues("ms-signature", out values))
    {
        byte[] signingKey = Convert.FromBase64String(_signingKey);
        string signatureFromHeader = values.FirstOrDefault();

        if (VerifyWebHookRequestSignature(requestBody, signatureFromHeader, signingKey))
        {
            string requestMessageContents = Encoding.UTF8.GetString(requestBody);

            NotificationMessage msg = JsonConvert.DeserializeObject<NotificationMessage>(requestMessageContents);

            if (VerifyHeaders(req, msg, log))
            { 
                string newJobStateStr = (string)msg.Properties.Where(j => j.Key == "NewState").FirstOrDefault().Value;
                if (newJobStateStr == "Finished")
                {
                    AzureAdTokenCredentials tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain,
                                new AzureAdClientSymmetricKey(_AMSClientId, _AMSClientSecret),
                                AzureEnvironments.AzureCloudEnvironment);

                    AzureAdTokenProvider tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                    _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                    if(_context!=null)   
                    {                        
                        string urlForClientStreaming = PublishAndBuildStreamingURLs(msg.Properties["JobId"]);
                        log.Info($"URL to the manifest for client streaming using HLS protocol: {urlForClientStreaming}");
                    }
                }

                return req.CreateResponse(HttpStatusCode.OK, string.Empty);
            }
            else
            {
                log.Info($"VerifyHeaders failed.");
                return req.CreateResponse(HttpStatusCode.BadRequest, "VerifyHeaders failed.");
            }
        }
        else
        {
            log.Info($"VerifyWebHookRequestSignature failed.");
            return req.CreateResponse(HttpStatusCode.BadRequest, "VerifyWebHookRequestSignature failed.");
        }
    }

    return req.CreateResponse(HttpStatusCode.BadRequest, "Generic Error.");
}

private static string PublishAndBuildStreamingURLs(String jobID)
{
    IJob job = _context.Jobs.Where(j => j.Id == jobID).FirstOrDefault();
    IAsset asset = job.OutputMediaAssets.FirstOrDefault();

    // Create a 30-day readonly access policy. 
    // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.
    IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
    TimeSpan.FromDays(30),
    AccessPermissions.Read);

    // Create a locator to the streaming content on an origin. 
    ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
    policy,
    DateTime.UtcNow.AddMinutes(-5));

    // Get a reference to the streaming manifest file from the  
    // collection of files in the asset. 
    var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

    // Create a full URL to the manifest file. Use this for playback
    // in streaming media clients. 
    string urlForClientStreaming = originLocator.Path + manifestFile.Name + "/manifest" +  "(format=m3u8-aapl)";
    return urlForClientStreaming;

}

private static bool VerifyWebHookRequestSignature(byte[] data, string actualValue, byte[] verificationKey)
{
    using (var hasher = new HMACSHA256(verificationKey))
    {
        byte[] sha256 = hasher.ComputeHash(data);
        string expectedValue = string.Format(CultureInfo.InvariantCulture, SignatureHeaderValueTemplate, ToHex(sha256));

        return (0 == String.Compare(actualValue, expectedValue, System.StringComparison.Ordinal));
    }
}

private static bool VerifyHeaders(HttpRequestMessage req, NotificationMessage msg, TraceWriter log)
{
    bool headersVerified = false;

    try
    {
        IEnumerable<string> values = null;
        if (req.Headers.TryGetValues("ms-mediaservices-accountid", out values))
        {
            string accountIdHeader = values.FirstOrDefault();
            string accountIdFromMessage = msg.Properties["AccountId"];

            if (0 == string.Compare(accountIdHeader, accountIdFromMessage, StringComparison.OrdinalIgnoreCase))
            {
                headersVerified = true;
            }
            else
            {
                log.Info($"accountIdHeader={accountIdHeader} does not match accountIdFromMessage={accountIdFromMessage}");
            }
        }
        else
        {
            log.Info($"Header ms-mediaservices-accountid not found.");
        }
    }
    catch (Exception e)
    {
        log.Info($"VerifyHeaders hit exception {e}");
        headersVerified = false;
    }

    return headersVerified;
}

private static readonly char[] HexLookup = new char[] { '0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'A', 'B', 'C', 'D', 'E', 'F' };

/// <summary>
/// Converts a <see cref="T:byte[]"/> to a hex-encoded string.
/// </summary>
private static string ToHex(byte[] data)
{
    if (data == null)
    {
        return string.Empty;
    }

    char[] content = new char[data.Length * 2];
    int output = 0;
    byte d;

    for (int input = 0; input < data.Length; input++)
    {
        d = data[input];
        content[output++] = HexLookup[d / 0x10];
        content[output++] = HexLookup[d % 0x10];
    }

    return new string(content);
}

internal enum NotificationEventType
{
    None = 0,
    JobStateChange = 1,
    NotificationEndPointRegistration = 2,
    NotificationEndPointUnregistration = 3,
    TaskStateChange = 4,
    TaskProgress = 5
}

internal sealed class NotificationMessage
{
    public string MessageVersion { get; set; }
    public string ETag { get; set; }
    public NotificationEventType EventType { get; set; }
    public DateTime TimeStamp { get; set; }
    public IDictionary<string, string> Properties { get; set; }
}
```

<span data-ttu-id="d9df8-170">Save and run your function.</span><span class="sxs-lookup"><span data-stu-id="d9df8-170">Save and run your function.</span></span>

### <a name="function-output"></a><span data-ttu-id="d9df8-171">Function output</span><span class="sxs-lookup"><span data-stu-id="d9df8-171">Function output</span></span>

<span data-ttu-id="d9df8-172">Once the webhook is triggered, the example above produces the following output, your values will vary.</span><span class="sxs-lookup"><span data-stu-id="d9df8-172">Once the webhook is triggered, the example above produces the following output, your values will vary.</span></span>

    C# HTTP trigger function processed a request. RequestUri=https://juliako001-functions.azurewebsites.net/api/Notification_Webhook_Function?code=9376d69kygoy49oft81nel8frty5cme8hb9xsjslxjhalwhfrqd79awz8ic4ieku74dvkdfgvi
    Request Body = 
    {
      "MessageVersion": "1.1",
      "ETag": "b8977308f48858a8f224708bc963e1a09ff917ce730316b4e7ae9137f78f3b20",
      "EventType": 4,
      "TimeStamp": "2017-02-16T03:59:53.3041122Z",
      "Properties": {
        "JobId": "nb:jid:UUID:badd996c-8d7c-4ae0-9bc1-bd7f1902dbdd",
        "TaskId": "nb:tid:UUID:80e26fb9-ee04-4739-abd8-2555dc24639f",
        "NewState": "Finished",
        "OldState": "Processing",
        "AccountName": "mediapkeewmg5c3peq",
        "AccountId": "301912b0-659e-47e0-9bc4-6973f2be3424",
        "NotificationEndPointId": "nb:nepid:UUID:cb5d707b-4db8-45fe-a558-19f8d3306093"
      }
    }
    
    URL to the manifest for client streaming using HLS protocol: http://mediapkeewmg5c3peq.streaming.mediaservices.windows.net/0ac98077-2b58-4db7-a8da-789a13ac6167/BigBuckBunny.ism/manifest(format=m3u8-aapl)

## <a name="add-a-webhook-to-your-encoding-task"></a><span data-ttu-id="d9df8-173">Add a webhook to your encoding task</span><span class="sxs-lookup"><span data-stu-id="d9df8-173">Add a webhook to your encoding task</span></span>

<span data-ttu-id="d9df8-174">In this section, the code that adds a webhook notification to a Task is shown.</span><span class="sxs-lookup"><span data-stu-id="d9df8-174">In this section, the code that adds a webhook notification to a Task is shown.</span></span> <span data-ttu-id="d9df8-175">You can also add a job level notification, which would be more useful for a job with chained tasks.</span><span class="sxs-lookup"><span data-stu-id="d9df8-175">You can also add a job level notification, which would be more useful for a job with chained tasks.</span></span>  

1. <span data-ttu-id="d9df8-176">Create a new C# Console Application in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d9df8-176">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="d9df8-177">Enter the Name, Location, and Solution name, and then click OK.</span><span class="sxs-lookup"><span data-stu-id="d9df8-177">Enter the Name, Location, and Solution name, and then click OK.</span></span>
2. <span data-ttu-id="d9df8-178">Use [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) to install Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="d9df8-178">Use [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) to install Azure Media Services.</span></span>
3. <span data-ttu-id="d9df8-179">Update App.config file with appropriate values:</span><span class="sxs-lookup"><span data-stu-id="d9df8-179">Update App.config file with appropriate values:</span></span> 
    
    * <span data-ttu-id="d9df8-180">Azure Media Services connection information,</span><span class="sxs-lookup"><span data-stu-id="d9df8-180">Azure Media Services connection information,</span></span> 
    * <span data-ttu-id="d9df8-181">webhook URL that expects to get the notifications,</span><span class="sxs-lookup"><span data-stu-id="d9df8-181">webhook URL that expects to get the notifications,</span></span> 
    * <span data-ttu-id="d9df8-182">the signing key that matches the key that your webhook expects.</span><span class="sxs-lookup"><span data-stu-id="d9df8-182">the signing key that matches the key that your webhook expects.</span></span> <span data-ttu-id="d9df8-183">The signing key is the 64-byte Base64 encoded value that is used to protect and secure your webhooks callbacks from Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="d9df8-183">The signing key is the 64-byte Base64 encoded value that is used to protect and secure your webhooks callbacks from Azure Media Services.</span></span> 

    ```xml
            <appSettings>
                <add key="AMSAADTenantDomain" value="domain" />
                <add key="AMSRESTAPIEndpoint" value="endpoint" />

                <add key="AMSClientId" value="clinet id" />
                <add key="AMSClientSecret" value="client secret" />

                <add key="WebhookURL" value="https://yourapp.azurewebsites.net/api/functionname?code=ApiKey" />
                <add key="WebhookSigningKey" value="j0txf1f8msjytzvpe40nxbpxdcxtqcgxy0nt" />
            </appSettings>
    ```

4. <span data-ttu-id="d9df8-184">Update your Program.cs file with the following code:</span><span class="sxs-lookup"><span data-stu-id="d9df8-184">Update your Program.cs file with the following code:</span></span>

    ```csharp
            using System;
            using System.Configuration;
            using System.Linq;
            using Microsoft.WindowsAzure.MediaServices.Client;

            namespace NotificationWebHook
            {
                class Program
                {
                // Read values from the App.config file.
                private static readonly string _AMSAADTenantDomain =
                    ConfigurationManager.AppSettings["AMSAADTenantDomain"];
                private static readonly string _AMSRESTAPIEndpoint =
                    ConfigurationManager.AppSettings["AMSRESTAPIEndpoint"];

                private static readonly string _AMSClientId =
                    ConfigurationManager.AppSettings["AMSClientId"];
                private static readonly string _AMSClientSecret =
                    ConfigurationManager.AppSettings["AMSClientSecret"];

                private static readonly string _webHookEndpoint =
                    ConfigurationManager.AppSettings["WebhookURL"];
                private static readonly string _signingKey =
                    ConfigurationManager.AppSettings["WebhookSigningKey"];

                // Field for service context.
                private static CloudMediaContext _context = null;

                static void Main(string[] args)
                {
                    AzureAdTokenCredentials tokenCredentials = new AzureAdTokenCredentials(_AMSAADTenantDomain,
                        new AzureAdClientSymmetricKey(_AMSClientId, _AMSClientSecret),
                        AzureEnvironments.AzureCloudEnvironment);

                    AzureAdTokenProvider tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                    _context = new CloudMediaContext(new Uri(_AMSRESTAPIEndpoint), tokenProvider);

                    byte[] keyBytes = Convert.FromBase64String(_signingKey);

                    IAsset newAsset = _context.Assets.FirstOrDefault();

                    // Check for existing Notification Endpoint with the name "FunctionWebHook"

                    var existingEndpoint = _context.NotificationEndPoints.Where(e => e.Name == "FunctionWebHook").FirstOrDefault();
                    INotificationEndPoint endpoint = null;

                    if (existingEndpoint != null)
                    {
                    Console.WriteLine("webhook endpoint already exists");
                    endpoint = (INotificationEndPoint)existingEndpoint;
                    }
                    else
                    {
                    endpoint = _context.NotificationEndPoints.Create("FunctionWebHook",
                        NotificationEndPointType.WebHook, _webHookEndpoint, keyBytes);
                    Console.WriteLine("Notification Endpoint Created with Key : {0}", keyBytes.ToString());
                    }

                    // Declare a new encoding job with the Standard encoder
                    IJob job = _context.Jobs.Create("MES Job");

                    // Get a media processor reference, and pass to it the name of the 
                    // processor to use for the specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

                    ITask task = job.Tasks.AddNew("My encoding task",
                    processor,
                    "Adaptive Streaming",
                    TaskOptions.None);

                    // Specify the input asset to be encoded.
                    task.InputAssets.Add(newAsset);

                    // Add an output asset to contain the results of the job. 
                    // This output is specified as AssetCreationOptions.None, which 
                    // means the output asset is not encrypted. 
                    task.OutputAssets.AddNew(newAsset.Name, AssetCreationOptions.None);

                    // Add the WebHook notification to this Task and request all notification state changes.
                    // Note that you can also add a job level notification
                    // which would be more useful for a job with chained tasks.  
                    if (endpoint != null)
                    {
                    task.TaskNotificationSubscriptions.AddNew(NotificationJobState.All, endpoint, true);
                    Console.WriteLine("Created Notification Subscription for endpoint: {0}", _webHookEndpoint);
                    }
                    else
                    {
                    Console.WriteLine("No Notification Endpoint is being used");
                    }

                    job.Submit();

                    Console.WriteLine("Expect WebHook to be triggered for the Job ID: {0}", job.Id);
                    Console.WriteLine("Expect WebHook to be triggered for the Task ID: {0}", task.Id);

                    Console.WriteLine("Job Submitted");

                }
                private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
                {
                    var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                    ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

                    if (processor == null)
                    throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

                    return processor;
                }
                }
            }
    ```

## <a name="next-steps"></a><span data-ttu-id="d9df8-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="d9df8-185">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d9df8-186">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="d9df8-186">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]
