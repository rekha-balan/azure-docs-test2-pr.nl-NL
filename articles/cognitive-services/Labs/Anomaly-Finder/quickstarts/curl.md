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
# <a name="use-the-anomaly-finder-api-with-curl"></a>Use the Anomaly Finder API with cURL

This article provides information and code samples to help you quickly get started using the Anomaly Finder API with cURL to accomplish task of getting anomaly result of time series data.

## <a name="prerequisites"></a>Prerequisites

[!INCLUDE [GetSubscriptionKey](../includes/get-subscription-key.md)]

## <a name="getting-anomaly-points-with-the-anomaly-finder-api-using-curl"></a>Getting anomaly points with the Anomaly Finder API using cURL 

[!INCLUDE [DataContract](../includes/datacontract.md)]

### <a name="example-of-time-series-data"></a>Example of time series data

The example of the time series data points is as follows.

[!INCLUDE [Request](../includes/request.md)]

### <a name="analyze-data-and-get-anomaly-points-curl-example"></a>Analyze data and get anomaly points cURL example

The steps of using the example are as follows.

1. Replace the `[YOUR_SUBSCRIPTION_KEY]` value with your valid subscription key.
2. Replace the `[YOUR_REGION]` to use the location where you obtained your subscription keys.
3. Replace the `[REPLACE_WITH_THE_EXAMPLE_OR_YOUR_OWN_DATA_POINTS]` with the example or your own data points.
4. Execute and check the response.

```cURL

curl -v -X POST "https://api.labs.cognitive.microsoft.com/anomalyfinder/v1.0/anomalydetection"
-H "Content-Type: application/json"
-H "Ocp-Apim-Subscription-Key: [YOUR_SUBSCRIPTION_KEY]"
--data-ascii "[REPLACE_WITH_THE_EXAMPLE_OR_YOUR_OWN_DATA_POINTS]" 

```

### <a name="example-response"></a>Example response
A successful response is returned in JSON. Example response is as follows: [!INCLUDE [Response](../includes/response.md)]

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [REST API reference](https://dev.labs.cognitive.microsoft.com/docs/services/anomaly-detection/operations/post-anomalydetection)
