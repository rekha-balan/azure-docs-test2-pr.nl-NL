---
title: How to use the Anomaly Finder API with PHP - Microsoft Cognitive Services | Microsoft Docs
description: Get information and code samples to help you quickly get started using Anomaly Finder with PHP in Cognitive Services.
services: cognitive-services
author: chliang
manager: bix
ms.service: cognitive-services
ms.technology: anomaly-detection
ms.topic: article
ms.date: 05/01/2018
ms.author: chliang
ms.openlocfilehash: f81c99b77f931b5b259633fa8fcd0bf3e358e281
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869585"
---
# <a name="use-the-anomaly-finder-api-with-php"></a>Use the Anomaly Finder API with PHP

This article provides information and code samples to help you quickly get started using the Anomaly Finder API with PHP to accomplish the task of getting anomaly result for time series data.

## <a name="prerequisites"></a>Prerequisites

[!INCLUDE [GetSubscriptionKey](../includes/get-subscription-key.md)]

## <a name="getting-anomaly-points-with-anomaly-finder-api-using-php"></a>Getting anomaly points with Anomaly Finder API using PHP
[!INCLUDE [DataContract](../includes/datacontract.md)]

### <a name="example-of-time-series-data"></a>Example of time series data
The example of the time series data is as follows.
[!INCLUDE [Request](../includes/request.md)]

### <a name="analyze-data-and-get-anomaly-points-php-example"></a>Analyze data and get anomaly points PHP example
1. Replace the `[YOUR_SUBSCRIPTION_KEY]` value with your valid subscription key.
2. Replace the `[REPLACE_WITH_THE_EXAMPLE_OR_YOUR_OWN_DATA_POINTS]` with the example or your own data points.
3. Execute and check the response.

```PHP
<?php
# This sample uses the Apache HTTP client from HTTP components (http://hc.apache.org/httpcomponents-client-ga/)
require_once 'HTTP/Request2.php';

$request = new HTTP_Request2('https://api.labs.cognitive.microsoft.com/anomalyfinder/v1.0/anomalydetection');
$url = $request->getUrl();

$requestData = '[REPLACE_WITH_THE_EXAMPLE_OR_YOUR_OWN_DATA_POINTS]';

$headers = array(
    # Request headers
    'Content-Type' => 'application/json',
    # NOTE: Replace the "Ocp-Apim-Subscription-Key" value with a valid subscription key.
    'Ocp-Apim-Subscription-Key' => '[YOUR_SUBSCRIPTION_KEY]',
);

$request->setHeader($headers);

$request->setMethod(HTTP_Request2::METHOD_POST);

# Request body
$request->setBody($requestData);

try
{
    $response = $request->send();
    echo $response->getBody();
}
catch (HttpException $ex)
{
    echo $ex;
}
?>
```

### <a name="example-response"></a>Example response

A successful response is returned in JSON. Sample response is as follows.
[!INCLUDE [Response](../includes/response.md)]

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [REST API reference](https://dev.labs.cognitive.microsoft.com/docs/services/anomaly-detection/operations/post-anomalydetection)
