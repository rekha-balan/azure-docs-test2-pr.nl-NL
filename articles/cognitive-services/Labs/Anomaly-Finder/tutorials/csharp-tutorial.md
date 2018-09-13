---
title: Anomaly Detection C# app - Microsoft Cognitive Services | Microsoft Docs
description: Explore a C# app that uses the Anomaly Detection API in Microsoft Cognitive Services. Send original data points to API and get the expected value and anomaly points.
services: cognitive-services
author: chliang
manager: bix
ms.service: cognitive-services
ms.technology: anomaly-detection
ms.topic: article
ms.date: 05/01/2018
ms.author: chliang
ms.openlocfilehash: 7d4f6a12c94620f447b5d6df4d7715d32eac2d98
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864387"
---
# <a name="anomaly-detection-c-application"></a><span data-ttu-id="399a8-104">Anomaly Detection C# application</span><span class="sxs-lookup"><span data-stu-id="399a8-104">Anomaly Detection C# application</span></span>

<span data-ttu-id="399a8-105">Explore a basic Windows application that uses Anomaly Detection API to detect anomalies from the input.</span><span class="sxs-lookup"><span data-stu-id="399a8-105">Explore a basic Windows application that uses Anomaly Detection API to detect anomalies from the input.</span></span> <span data-ttu-id="399a8-106">The example submits the time series data to the Anomaly Detection API with your subscription key, then gets all the anomaly points and expected value for each data point from the API.</span><span class="sxs-lookup"><span data-stu-id="399a8-106">The example submits the time series data to the Anomaly Detection API with your subscription key, then gets all the anomaly points and expected value for each data point from the API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="399a8-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="399a8-107">Prerequisites</span></span>

### <a name="platform-requirements"></a><span data-ttu-id="399a8-108">Platform requirements</span><span class="sxs-lookup"><span data-stu-id="399a8-108">Platform requirements</span></span>

<span data-ttu-id="399a8-109">The example has been developed for the .NET Framework using [Visual Studio 2017, Community Edition](https://www.visualstudio.com/products/visual-studio-community-vs).</span><span class="sxs-lookup"><span data-stu-id="399a8-109">The example has been developed for the .NET Framework using [Visual Studio 2017, Community Edition](https://www.visualstudio.com/products/visual-studio-community-vs).</span></span> 

### <a name="subscribe-to-anomaly-detection-and-get-a-subscription-key"></a><span data-ttu-id="399a8-110">Subscribe to Anomaly Detection and get a subscription key</span><span class="sxs-lookup"><span data-stu-id="399a8-110">Subscribe to Anomaly Detection and get a subscription key</span></span> 

[!INCLUDE [GetSubscriptionKey](../includes/get-subscription-key.md)]

## <a name="get-and-use-the-example"></a><span data-ttu-id="399a8-111">Get and use the example</span><span class="sxs-lookup"><span data-stu-id="399a8-111">Get and use the example</span></span>

<span data-ttu-id="399a8-112">You can clone the Anomaly Detection example application to your computer from [Github](https://github.com/MicrosoftAnomalyDetection/csharp-sample.git).</span><span class="sxs-lookup"><span data-stu-id="399a8-112">You can clone the Anomaly Detection example application to your computer from [Github](https://github.com/MicrosoftAnomalyDetection/csharp-sample.git).</span></span> 
<a name="Step1"></a>
### <a name="install-the-example"></a><span data-ttu-id="399a8-113">Install the example</span><span class="sxs-lookup"><span data-stu-id="399a8-113">Install the example</span></span>

<span data-ttu-id="399a8-114">In your GitHub Desktop, open Sample\AnomalyDetectionSample.sln.</span><span class="sxs-lookup"><span data-stu-id="399a8-114">In your GitHub Desktop, open Sample\AnomalyDetectionSample.sln.</span></span>

<a name="Step2"></a>
### <a name="build-the-example"></a><span data-ttu-id="399a8-115">Build the example</span><span class="sxs-lookup"><span data-stu-id="399a8-115">Build the example</span></span>

<span data-ttu-id="399a8-116">Press Ctrl+Shift+B, or click Build on the ribbon menu, then select Build Solution.</span><span class="sxs-lookup"><span data-stu-id="399a8-116">Press Ctrl+Shift+B, or click Build on the ribbon menu, then select Build Solution.</span></span>

<a name="Step3"></a>
### <a name="run-the-example"></a><span data-ttu-id="399a8-117">Run the example</span><span class="sxs-lookup"><span data-stu-id="399a8-117">Run the example</span></span>

1. <span data-ttu-id="399a8-118">After the build is completed, press **F5** or click **Start** on the ribbon menu to run the example.</span><span class="sxs-lookup"><span data-stu-id="399a8-118">After the build is completed, press **F5** or click **Start** on the ribbon menu to run the example.</span></span>
2. <span data-ttu-id="399a8-119">Locate the Anomaly Detection user interface window with the text edit box reading "{your_subscription_key}".</span><span class="sxs-lookup"><span data-stu-id="399a8-119">Locate the Anomaly Detection user interface window with the text edit box reading "{your_subscription_key}".</span></span>
3. <span data-ttu-id="399a8-120">Replace the request.json file, which contains the sample data, with your own data, then click "Send" button.</span><span class="sxs-lookup"><span data-stu-id="399a8-120">Replace the request.json file, which contains the sample data, with your own data, then click "Send" button.</span></span> <span data-ttu-id="399a8-121">Microsoft receives the data you upload and use them to detect any anomaly points among then.</span><span class="sxs-lookup"><span data-stu-id="399a8-121">Microsoft receives the data you upload and use them to detect any anomaly points among then.</span></span> <span data-ttu-id="399a8-122">The data you load will not be persisted in Microsoft's server.</span><span class="sxs-lookup"><span data-stu-id="399a8-122">The data you load will not be persisted in Microsoft's server.</span></span> <span data-ttu-id="399a8-123">To detect the anomaly point again, you need upload the data once again.</span><span class="sxs-lookup"><span data-stu-id="399a8-123">To detect the anomaly point again, you need upload the data once again.</span></span>
4. <span data-ttu-id="399a8-124">If the data is good, you will find the anomaly detection result in "Response" field.</span><span class="sxs-lookup"><span data-stu-id="399a8-124">If the data is good, you will find the anomaly detection result in "Response" field.</span></span> <span data-ttu-id="399a8-125">If any error occurs, the error information will be shown in the Response field as well.</span><span class="sxs-lookup"><span data-stu-id="399a8-125">If any error occurs, the error information will be shown in the Response field as well.</span></span>

<a name="Review"></a>
### <a name="read-the-result"></a><span data-ttu-id="399a8-126">Read the result</span><span class="sxs-lookup"><span data-stu-id="399a8-126">Read the result</span></span>

[!INCLUDE [diagrams](../includes/diagrams.md)]

<a name="Review"></a>
### <a name="review-and-learn"></a><span data-ttu-id="399a8-127">Review and learn</span><span class="sxs-lookup"><span data-stu-id="399a8-127">Review and learn</span></span>

<span data-ttu-id="399a8-128">Now that you have a running application, let's review how the example app integrates with Cognitive Services technology.</span><span class="sxs-lookup"><span data-stu-id="399a8-128">Now that you have a running application, let's review how the example app integrates with Cognitive Services technology.</span></span> <span data-ttu-id="399a8-129">This step will make it easier to either continue building onto this app or develop your own app using Microsoft Anomaly Detection.</span><span class="sxs-lookup"><span data-stu-id="399a8-129">This step will make it easier to either continue building onto this app or develop your own app using Microsoft Anomaly Detection.</span></span>

<span data-ttu-id="399a8-130">This example app makes use of the Anomaly Detection Restful API endpoint.</span><span class="sxs-lookup"><span data-stu-id="399a8-130">This example app makes use of the Anomaly Detection Restful API endpoint.</span></span>

<span data-ttu-id="399a8-131">Reviewing how the Restful API gets used in the example application, let's look at a code snippet from **AnomalyDetectionClient.cs**.</span><span class="sxs-lookup"><span data-stu-id="399a8-131">Reviewing how the Restful API gets used in the example application, let's look at a code snippet from **AnomalyDetectionClient.cs**.</span></span> <span data-ttu-id="399a8-132">The file contains code comments indicating “KEY SAMPLE CODE STARTS HERE” and “KEY SAMPLE CODE ENDS HERE” to help you locate the code snippets reproduced below.</span><span class="sxs-lookup"><span data-stu-id="399a8-132">The file contains code comments indicating “KEY SAMPLE CODE STARTS HERE” and “KEY SAMPLE CODE ENDS HERE” to help you locate the code snippets reproduced below.</span></span>

```csharp
            // ----------------------------------------------------------------------
            // KEY SAMPLE CODE STARTS HERE
            // Set http request header
            // ---------------------------------------------------------------------- 
            client.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));
            client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", subscriptionKey);
            // ----------------------------------------------------------------------
            // KEY SAMPLE CODE ENDS HERE 
            // ----------------------------------------------------------------------

```
### <a name="request"></a><span data-ttu-id="399a8-133">**Request**</span><span class="sxs-lookup"><span data-stu-id="399a8-133">**Request**</span></span>
<span data-ttu-id="399a8-134">The code snippet below shows how to use the HttpClient to submit your subscription key and data points to the endpoint of the Anomaly Detection API.</span><span class="sxs-lookup"><span data-stu-id="399a8-134">The code snippet below shows how to use the HttpClient to submit your subscription key and data points to the endpoint of the Anomaly Detection API.</span></span>

```csharp
    public async Task<string> Request(string baseAddress, string endpoint, string subscriptionKey, string requestData)
    {
        using (HttpClient client = new HttpClient { BaseAddress = new Uri(baseAddress) })
        {
            // ----------------------------------------------------------------------
            // KEY SAMPLE CODE STARTS HERE
            // Set http request header
            // ---------------------------------------------------------------------- 
            client.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));
            client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", subscriptionKey);
            // ----------------------------------------------------------------------
            // KEY SAMPLE CODE ENDS HERE 
            // ----------------------------------------------------------------------

            // ----------------------------------------------------------------------
            // KEY SAMPLE CODE STARTS HERE
            // Build the request content
            // ---------------------------------------------------------------------- 
            var content = new StringContent(requestData, Encoding.UTF8, "application/json");
            // ----------------------------------------------------------------------
            // KEY SAMPLE CODE ENDS HERE 
            // ----------------------------------------------------------------------

            // ----------------------------------------------------------------------
            // KEY SAMPLE CODE STARTS HERE
            // Send the request content with POST method.
            // ---------------------------------------------------------------------- 
            var res = await client.PostAsync(endpoint, content);
            // ----------------------------------------------------------------------
            // KEY SAMPLE CODE ENDS HERE 
            // ----------------------------------------------------------------------
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
```

## <a name="next-steps"></a><span data-ttu-id="399a8-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="399a8-135">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="399a8-136">REST API reference</span><span class="sxs-lookup"><span data-stu-id="399a8-136">REST API reference</span></span>](https://dev.labs.cognitive.microsoft.com/docs/services/anomaly-detection/operations/post-anomalydetection)
