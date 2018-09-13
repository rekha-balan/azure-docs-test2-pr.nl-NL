---
title: How to use the Anomaly Finder API with C# - Microsoft Cognitive Services | Microsoft Docs
description: Get information and code samples to help you quickly get started using C# and the Anomaly Finder API in Cognitive Services.
services: cognitive-services
author: chliang
manager: bix
ms.service: cognitive-services
ms.technology: anomaly-detection
ms.topic: article
ms.date: 05/01/2018
ms.author: chliang
ms.openlocfilehash: 867ce4d0262c94de8da0dadeb8de71c28a8295d5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856433"
---
# <a name="use-the-anomaly-finder-api-with-c"></a><span data-ttu-id="baeea-103">Use the Anomaly Finder API with C#</span><span class="sxs-lookup"><span data-stu-id="baeea-103">Use the Anomaly Finder API with C#</span></span>

<span data-ttu-id="baeea-104">This article provides information and code samples to help you quickly get started using the Anomaly Finder API with C# to accomplish task of getting anomaly result of time series data.</span><span class="sxs-lookup"><span data-stu-id="baeea-104">This article provides information and code samples to help you quickly get started using the Anomaly Finder API with C# to accomplish task of getting anomaly result of time series data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="baeea-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="baeea-105">Prerequisites</span></span>

[!INCLUDE [GetSubscriptionKey](../includes/get-subscription-key.md)]

## <a name="getting-anomaly-points-with-anomaly-finder-api-using-c"></a><span data-ttu-id="baeea-106">Getting anomaly points with Anomaly Finder API using C#</span><span class="sxs-lookup"><span data-stu-id="baeea-106">Getting anomaly points with Anomaly Finder API using C#</span></span>

[!INCLUDE [DataContract](../includes/datacontract.md)]

### <a name="example-of-time-series-data-points"></a><span data-ttu-id="baeea-107">Example of time series data points</span><span class="sxs-lookup"><span data-stu-id="baeea-107">Example of time series data points</span></span>

<span data-ttu-id="baeea-108">The example of the time series data points is as follows.</span><span class="sxs-lookup"><span data-stu-id="baeea-108">The example of the time series data points is as follows.</span></span>
[!INCLUDE [Request](../includes/request.md)]

### <a name="analyze-data-and-get-anomaly-points-c-example"></a><span data-ttu-id="baeea-109">Analyze data and get anomaly points C# example</span><span class="sxs-lookup"><span data-stu-id="baeea-109">Analyze data and get anomaly points C# example</span></span>

<span data-ttu-id="baeea-110">The steps of using the example are as follows.</span><span class="sxs-lookup"><span data-stu-id="baeea-110">The steps of using the example are as follows.</span></span>

1. <span data-ttu-id="baeea-111">Create a new Console solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="baeea-111">Create a new Console solution in Visual Studio.</span></span>
2. <span data-ttu-id="baeea-112">Replace Program.cs with the following code and add the reference to System.Net.Http.</span><span class="sxs-lookup"><span data-stu-id="baeea-112">Replace Program.cs with the following code and add the reference to System.Net.Http.</span></span>
3. <span data-ttu-id="baeea-113">Replace `[YOUR_SUBSCRIPTION_KEY]` value with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="baeea-113">Replace `[YOUR_SUBSCRIPTION_KEY]` value with your valid subscription key.</span></span>
4. <span data-ttu-id="baeea-114">Replace `[REPLACE_WITH_THE_EXAMPLE_OR_YOUR_OWN_DATA_POINTS]` with your data points.</span><span class="sxs-lookup"><span data-stu-id="baeea-114">Replace `[REPLACE_WITH_THE_EXAMPLE_OR_YOUR_OWN_DATA_POINTS]` with your data points.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Text;
using System.Text.RegularExpressions;
using System.Threading.Tasks;

namespace Console
{
    class Program
    {
        // **********************************************
        // *** Update or verify the following values. ***
        // **********************************************

        // Replace the subscriptionKey string value with your valid subscription key.
        const string subscriptionKey = "[YOUR_SUBSCRIPTION_KEY]";

        const string endpoint = "https://api.labs.cognitive.microsoft.com/anomalyfinder/v1.0/anomalydetection";

        // Replace the request data with your real data.
        const string requestData = "[REPLACE_WITH_THE_EXAMPLE_OR_YOUR_OWN_DATA_POINTS]";
        static void Main(string[] args)
        {
            var match = Regex.Match(endpoint, "(?<BaseAddress>https://[^/]+)(?<Url>/*.+)");
            if (match.Success)
            {
                var res = Request(
                    match.Groups["BaseAddress"].Value,
                    match.Groups["Url"].Value,
                    subscriptionKey,
                    requestData).Result;
                System.Console.Write(res);
            }
            else
            {
                System.Console.Write("Incorrect endpoint.");
            }
        }

        /// <summary>
        /// Call API to detect the anomaly points
        /// </summary>
        /// <param name="baseAddress">Base address of the API endpoint.</param>
        /// <param name="endpoint">The endpoint of the API</param>
        /// <param name="subscriptionKey">The subscription key applied  </param>
        /// <param name="requestData">The JSON string for requet data points</param>
        /// <returns>The JSON string for anomaly points and expected values.</returns>
        static async Task<string> Request(string baseAddress, string endpoint, string subscriptionKey, string requestData)
        {
            using (HttpClient client = new HttpClient { BaseAddress = new Uri(baseAddress) })
            {
                client.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));
                client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", subscriptionKey);

                var content = new StringContent(requestData, Encoding.UTF8, "application/json");
                var res = await client.PostAsync(endpoint, content);
                if (res.IsSuccessStatusCode)
                {
                    return await res.Content.ReadAsStringAsync();
                }
                else
                {
                    return $"ErrorCode: {res.StatusCode}";
                }
            }
        }
    }
}

```

### <a name="example-response"></a><span data-ttu-id="baeea-115">Example response</span><span class="sxs-lookup"><span data-stu-id="baeea-115">Example response</span></span>

<span data-ttu-id="baeea-116">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="baeea-116">A successful response is returned in JSON.</span></span> <span data-ttu-id="baeea-117">The example response is as follows.</span><span class="sxs-lookup"><span data-stu-id="baeea-117">The example response is as follows.</span></span>
[!INCLUDE [Response](../includes/response.md)]

## <a name="next-steps"></a><span data-ttu-id="baeea-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="baeea-118">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="baeea-119">C# app</span><span class="sxs-lookup"><span data-stu-id="baeea-119">C# app</span></span>](../tutorials/csharp-tutorial.md)
