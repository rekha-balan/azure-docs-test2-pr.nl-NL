---
title: How to use the Anomaly Finder API with Ruby - Microsoft Cognitive Services | Microsoft Docs
description: Get information and code samples to help you quickly get started using Ruby and the Anomaly Finder API in Cognitive Services.
services: cognitive-services
author: chliang
manager: bix
ms.service: cognitive-services
ms.technology: anomaly-detection
ms.topic: article
ms.date: 05/01/2018
ms.author: chliang
ms.openlocfilehash: 6eb559f8971583afe9619fb41fe331bd3013bb69
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866457"
---
# <a name="use-the-anomaly-finder-api-with-ruby"></a><span data-ttu-id="1ed25-103">Use the Anomaly Finder API with Ruby</span><span class="sxs-lookup"><span data-stu-id="1ed25-103">Use the Anomaly Finder API with Ruby</span></span>

<span data-ttu-id="1ed25-104">This article provides information and code samples to help you quickly get started using the Anomaly Finder API with Ruby to accomplish task of getting anomaly detection result of time series data.</span><span class="sxs-lookup"><span data-stu-id="1ed25-104">This article provides information and code samples to help you quickly get started using the Anomaly Finder API with Ruby to accomplish task of getting anomaly detection result of time series data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ed25-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1ed25-105">Prerequisites</span></span>

[!INCLUDE [GetSubscriptionKey](../includes/get-subscription-key.md)]

## <a name="getting-anomaly-points-with-anomaly-finder-api-using-ruby"></a><span data-ttu-id="1ed25-106">Getting anomaly points with Anomaly Finder API using Ruby</span><span class="sxs-lookup"><span data-stu-id="1ed25-106">Getting anomaly points with Anomaly Finder API using Ruby</span></span> 
[!INCLUDE [DataContract](../includes/datacontract.md)]

### <a name="example-of-time-series-data"></a><span data-ttu-id="1ed25-107">Example of time series data</span><span class="sxs-lookup"><span data-stu-id="1ed25-107">Example of time series data</span></span>
<span data-ttu-id="1ed25-108">The example of the time series data points is as follows,</span><span class="sxs-lookup"><span data-stu-id="1ed25-108">The example of the time series data points is as follows,</span></span>

[!INCLUDE [Request](../includes/request.md)]

### <a name="analyze-data-and-get-anomaly-points-ruby-example"></a><span data-ttu-id="1ed25-109">Analyze data and get anomaly points Ruby example</span><span class="sxs-lookup"><span data-stu-id="1ed25-109">Analyze data and get anomaly points Ruby example</span></span>

<span data-ttu-id="1ed25-110">The steps of using the example are as follows.</span><span class="sxs-lookup"><span data-stu-id="1ed25-110">The steps of using the example are as follows.</span></span>

1. <span data-ttu-id="1ed25-111">Install [rest-client](https://github.com/rest-client/rest-client) by running 'gem install rest-client'.</span><span class="sxs-lookup"><span data-stu-id="1ed25-111">Install [rest-client](https://github.com/rest-client/rest-client) by running 'gem install rest-client'.</span></span>
2. <span data-ttu-id="1ed25-112">Save below code as a .rb file.</span><span class="sxs-lookup"><span data-stu-id="1ed25-112">Save below code as a .rb file.</span></span>
3. <span data-ttu-id="1ed25-113">Replace the `[YOUR_SUBSCRIPTION_KEY]` value with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="1ed25-113">Replace the `[YOUR_SUBSCRIPTION_KEY]` value with your valid subscription key.</span></span>
4. <span data-ttu-id="1ed25-114">Replace the `[REPLACE_WITH_THE_EXAMPLE_OR_YOUR_OWN_DATA_POINTS]` with the example or your own data points.</span><span class="sxs-lookup"><span data-stu-id="1ed25-114">Replace the `[REPLACE_WITH_THE_EXAMPLE_OR_YOUR_OWN_DATA_POINTS]` with the example or your own data points.</span></span>
5. <span data-ttu-id="1ed25-115">Execute and check the response.</span><span class="sxs-lookup"><span data-stu-id="1ed25-115">Execute and check the response.</span></span>

```ruby
# https://github.com/rest-client/rest-client
require 'rest_client'

# **********************************************
# *** Update or verify the following values. ***
# **********************************************

# Replace the subscriptionKey string value with your valid subscription key.
subscription_key = '[YOUR_SUBSCRIPTION_KEY]';

endpoint = "https://api.labs.cognitive.microsoft.com/anomalyfinder/v1.0/anomalydetection";

# Replace the request data with your real data.
requestData = '[REPLACE_WITH_THE_EXAMPLE_OR_YOUR_OWN_DATA_POINTS]';

header = {
    :content_type => 'application/json',
    :'Ocp-Apim-Subscription-Key' => subscription_key
}

response = RestClient::Request.execute(
    :url => endpoint,
    :method => :post,
    :verify_ssl => true,
    :payload => requestData,
    :header => header)

# You will see the response with anomaly results
puts response.body
```

### <a name="example-response"></a><span data-ttu-id="1ed25-116">Example response</span><span class="sxs-lookup"><span data-stu-id="1ed25-116">Example response</span></span>

<span data-ttu-id="1ed25-117">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="1ed25-117">A successful response is returned in JSON.</span></span> <span data-ttu-id="1ed25-118">Sample response is as follows.</span><span class="sxs-lookup"><span data-stu-id="1ed25-118">Sample response is as follows.</span></span>
[!INCLUDE [Response](../includes/response.md)]

## <a name="next-steps"></a><span data-ttu-id="1ed25-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="1ed25-119">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1ed25-120">REST API reference</span><span class="sxs-lookup"><span data-stu-id="1ed25-120">REST API reference</span></span>](https://dev.labs.cognitive.microsoft.com/docs/services/anomaly-detection/operations/post-anomalydetection)
