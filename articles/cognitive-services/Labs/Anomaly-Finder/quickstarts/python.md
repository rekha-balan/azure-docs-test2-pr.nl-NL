---
title: How to use the Anomaly Finder API with Python - Microsoft Cognitive Services | Microsoft Docs
description: Get information and code samples to help you quickly get started using Anomaly Finder with Python in Cognitive Services.
services: cognitive-services
author: chliang
manager: bix
ms.service: cognitive-services
ms.technology: anomaly-detection
ms.topic: article
ms.date: 05/01/2018
ms.author: chliang
ms.openlocfilehash: c14916b0644edab613b298d6e71f8bbb9a6bb804
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869131"
---
# <a name="use-the-anomaly-finder-api-with-python"></a><span data-ttu-id="f6f4f-103">Use the Anomaly Finder API with Python</span><span class="sxs-lookup"><span data-stu-id="f6f4f-103">Use the Anomaly Finder API with Python</span></span>

<span data-ttu-id="f6f4f-104">This article provides information and code samples to help you quickly get started using the Anomaly Finder API with Python to accomplish task of getting anomaly result for time series data.</span><span class="sxs-lookup"><span data-stu-id="f6f4f-104">This article provides information and code samples to help you quickly get started using the Anomaly Finder API with Python to accomplish task of getting anomaly result for time series data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6f4f-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f6f4f-105">Prerequisites</span></span>

[!INCLUDE [GetSubscriptionKey](../includes/get-subscription-key.md)]

## <a name="getting-anomaly-points-with-anomaly-finder-api-using-python"></a><span data-ttu-id="f6f4f-106">Getting anomaly points with Anomaly Finder API using Python</span><span class="sxs-lookup"><span data-stu-id="f6f4f-106">Getting anomaly points with Anomaly Finder API using Python</span></span> 

[!INCLUDE [DataContract](../includes/datacontract.md)]

### <a name="example-of-time-series-data"></a><span data-ttu-id="f6f4f-107">Example of time series data</span><span class="sxs-lookup"><span data-stu-id="f6f4f-107">Example of time series data</span></span>

<span data-ttu-id="f6f4f-108">The example of the time series data points is as follows.</span><span class="sxs-lookup"><span data-stu-id="f6f4f-108">The example of the time series data points is as follows.</span></span>

[!INCLUDE [Request](../includes/request.md)]

### <a name="analyze-data-and-get-anomaly-points-python-example"></a><span data-ttu-id="f6f4f-109">Analyze data and get anomaly points Python example</span><span class="sxs-lookup"><span data-stu-id="f6f4f-109">Analyze data and get anomaly points Python example</span></span>

<span data-ttu-id="f6f4f-110">Make sure you have installed python3, then create a python executable file named detect.py.</span><span class="sxs-lookup"><span data-stu-id="f6f4f-110">Make sure you have installed python3, then create a python executable file named detect.py.</span></span> <span data-ttu-id="f6f4f-111">In detect.py, you should include the code below.</span><span class="sxs-lookup"><span data-stu-id="f6f4f-111">In detect.py, you should include the code below.</span></span> <span data-ttu-id="f6f4f-112">Before executing the code, remember to replace the `[YOUR_SUBSCRIPTION_KEY]` value with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="f6f4f-112">Before executing the code, remember to replace the `[YOUR_SUBSCRIPTION_KEY]` value with your valid subscription key.</span></span>
<span data-ttu-id="f6f4f-113">Replace the `[REPLACE_WITH_THE_EXAMPLE_OR_YOUR_OWN_DATA_POINTS]` with your data points.</span><span class="sxs-lookup"><span data-stu-id="f6f4f-113">Replace the `[REPLACE_WITH_THE_EXAMPLE_OR_YOUR_OWN_DATA_POINTS]` with your data points.</span></span>

```python
import requests
import json


def detect(url, subscription_key, request_data):
    headers = {'Content-Type': 'application/json', 'Ocp-Apim-Subscription-Key': subscription_key}
    response = requests.post(url, data=json.dumps(request_data), headers=headers)
    if response.status_code == 200:
        return json.loads(response.content.decode("utf-8"))
    else:
        print(response.status_code)
        raise Exception(response.text)


sample_data = "[REPLACE_WITH_THE_EXAMPLE_OR_YOUR_OWN_DATA_POINTS]"
endpont = "https://api.labs.cognitive.microsoft.com/anomalyfinder/v1.0/anomalydetection"
subscription_key = "[YOUR_SUBSCRIPTION_KEY]"

result = detect(endpont, subscription_key, sample_data)
print(result)

```

### <a name="example-response"></a><span data-ttu-id="f6f4f-114">Example response</span><span class="sxs-lookup"><span data-stu-id="f6f4f-114">Example response</span></span>

<span data-ttu-id="f6f4f-115">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="f6f4f-115">A successful response is returned in JSON.</span></span> <span data-ttu-id="f6f4f-116">Sample response is as follows.</span><span class="sxs-lookup"><span data-stu-id="f6f4f-116">Sample response is as follows.</span></span>
[!INCLUDE [Response](../includes/response.md)]

## <a name="next-steps"></a><span data-ttu-id="f6f4f-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="f6f4f-117">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f6f4f-118">Python app</span><span class="sxs-lookup"><span data-stu-id="f6f4f-118">Python app</span></span>](../tutorials/python-tutorial.md)
