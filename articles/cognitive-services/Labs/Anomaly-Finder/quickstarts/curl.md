---
title: How to use the Anomaly Finder API with cURL - Microsoft Cognitive Services | Microsoft Docs
description: Get information to help you quickly get started using cURL and the Anomaly Finder API in Cognitive Services.
services: cognitive-services
author: chliang
manager: bix
ms.service: cognitive-services
ms.technology: anomaly-detection
ms.topic: article
ms.date: 05/01/2018
ms.author: chliang
ms.openlocfilehash: 3c1d791b8c0478715b4ffa93cd7dfa43f9be4586
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867994"
---
# <a name="use-the-anomaly-finder-api-with-curl"></a><span data-ttu-id="ff7ad-103">Use the Anomaly Finder API with cURL</span><span class="sxs-lookup"><span data-stu-id="ff7ad-103">Use the Anomaly Finder API with cURL</span></span>

<span data-ttu-id="ff7ad-104">This article provides information and code samples to help you quickly get started using the Anomaly Finder API with cURL to accomplish task of getting anomaly result of time series data.</span><span class="sxs-lookup"><span data-stu-id="ff7ad-104">This article provides information and code samples to help you quickly get started using the Anomaly Finder API with cURL to accomplish task of getting anomaly result of time series data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff7ad-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ff7ad-105">Prerequisites</span></span>

[!INCLUDE [GetSubscriptionKey](../includes/get-subscription-key.md)]

## <a name="getting-anomaly-points-with-the-anomaly-finder-api-using-curl"></a><span data-ttu-id="ff7ad-106">Getting anomaly points with the Anomaly Finder API using cURL</span><span class="sxs-lookup"><span data-stu-id="ff7ad-106">Getting anomaly points with the Anomaly Finder API using cURL</span></span> 

[!INCLUDE [DataContract](../includes/datacontract.md)]

### <a name="example-of-time-series-data"></a><span data-ttu-id="ff7ad-107">Example of time series data</span><span class="sxs-lookup"><span data-stu-id="ff7ad-107">Example of time series data</span></span>

<span data-ttu-id="ff7ad-108">The example of the time series data points is as follows.</span><span class="sxs-lookup"><span data-stu-id="ff7ad-108">The example of the time series data points is as follows.</span></span>

[!INCLUDE [Request](../includes/request.md)]

### <a name="analyze-data-and-get-anomaly-points-curl-example"></a><span data-ttu-id="ff7ad-109">Analyze data and get anomaly points cURL example</span><span class="sxs-lookup"><span data-stu-id="ff7ad-109">Analyze data and get anomaly points cURL example</span></span>

<span data-ttu-id="ff7ad-110">The steps of using the example are as follows.</span><span class="sxs-lookup"><span data-stu-id="ff7ad-110">The steps of using the example are as follows.</span></span>

1. <span data-ttu-id="ff7ad-111">Replace the `[YOUR_SUBSCRIPTION_KEY]` value with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="ff7ad-111">Replace the `[YOUR_SUBSCRIPTION_KEY]` value with your valid subscription key.</span></span>
2. <span data-ttu-id="ff7ad-112">Replace the `[YOUR_REGION]` to use the location where you obtained your subscription keys.</span><span class="sxs-lookup"><span data-stu-id="ff7ad-112">Replace the `[YOUR_REGION]` to use the location where you obtained your subscription keys.</span></span>
3. <span data-ttu-id="ff7ad-113">Replace the `[REPLACE_WITH_THE_EXAMPLE_OR_YOUR_OWN_DATA_POINTS]` with the example or your own data points.</span><span class="sxs-lookup"><span data-stu-id="ff7ad-113">Replace the `[REPLACE_WITH_THE_EXAMPLE_OR_YOUR_OWN_DATA_POINTS]` with the example or your own data points.</span></span>
4. <span data-ttu-id="ff7ad-114">Execute and check the response.</span><span class="sxs-lookup"><span data-stu-id="ff7ad-114">Execute and check the response.</span></span>

```cURL

curl -v -X POST "https://api.labs.cognitive.microsoft.com/anomalyfinder/v1.0/anomalydetection"
-H "Content-Type: application/json"
-H "Ocp-Apim-Subscription-Key: [YOUR_SUBSCRIPTION_KEY]"
--data-ascii "[REPLACE_WITH_THE_EXAMPLE_OR_YOUR_OWN_DATA_POINTS]" 

```

### <a name="example-response"></a><span data-ttu-id="ff7ad-115">Example response</span><span class="sxs-lookup"><span data-stu-id="ff7ad-115">Example response</span></span>
<span data-ttu-id="ff7ad-116">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="ff7ad-116">A successful response is returned in JSON.</span></span> <span data-ttu-id="ff7ad-117">Example response is as follows: [!INCLUDE [Response](../includes/response.md)]</span><span class="sxs-lookup"><span data-stu-id="ff7ad-117">Example response is as follows: [!INCLUDE [Response](../includes/response.md)]</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff7ad-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="ff7ad-118">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ff7ad-119">REST API reference</span><span class="sxs-lookup"><span data-stu-id="ff7ad-119">REST API reference</span></span>](https://dev.labs.cognitive.microsoft.com/docs/services/anomaly-detection/operations/post-anomalydetection)
