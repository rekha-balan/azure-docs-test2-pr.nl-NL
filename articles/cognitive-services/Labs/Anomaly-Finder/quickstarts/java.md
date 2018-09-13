---
title: How to use the Anomaly Finder API with Java - Microsoft Cognitive Services | Microsoft Docs
description: Get information and code samples to help you quickly get started using Java and the Anomaly Detection in Cognitive Services.
services: cognitive-services
author: chliang
manager: bix
ms.service: cognitive-services
ms.technology: anomaly-detection
ms.topic: article
ms.date: 05/01/2018
ms.author: kefre
ms.openlocfilehash: 8152c23e6c5332d243d851be56bab1e4085dbe5a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868846"
---
# <a name="use-the-anomaly-finder-api-with-java"></a><span data-ttu-id="614ab-103">Use the Anomaly Finder API with Java</span><span class="sxs-lookup"><span data-stu-id="614ab-103">Use the Anomaly Finder API with Java</span></span>

<span data-ttu-id="614ab-104">This article provides information and code samples to help you quickly get started using the Anomaly Detection API with Java to accomplish task of getting anomaly detection result for time series data.</span><span class="sxs-lookup"><span data-stu-id="614ab-104">This article provides information and code samples to help you quickly get started using the Anomaly Detection API with Java to accomplish task of getting anomaly detection result for time series data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="614ab-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="614ab-105">Prerequisites</span></span>

[!INCLUDE [GetSubscriptionKey](../includes/get-subscription-key.md)]

## <a name="getting-anomaly-points-with-the-anomaly-detection-api-using-java"></a><span data-ttu-id="614ab-106">Getting anomaly points with the Anomaly Detection API using Java</span><span class="sxs-lookup"><span data-stu-id="614ab-106">Getting anomaly points with the Anomaly Detection API using Java</span></span>

[!INCLUDE [DataContract](../includes/datacontract.md)]

### <a name="example-of-time-series-data"></a><span data-ttu-id="614ab-107">Example of time series data</span><span class="sxs-lookup"><span data-stu-id="614ab-107">Example of time series data</span></span>

<span data-ttu-id="614ab-108">The example of the time series data points is as follows.</span><span class="sxs-lookup"><span data-stu-id="614ab-108">The example of the time series data points is as follows.</span></span>

[!INCLUDE [Request](../includes/request.md)]

### <a name="analyze-data-and-get-anomaly-points-java-example"></a><span data-ttu-id="614ab-109">Analyze data and get anomaly points Java example</span><span class="sxs-lookup"><span data-stu-id="614ab-109">Analyze data and get anomaly points Java example</span></span>

<span data-ttu-id="614ab-110">To run the sample, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="614ab-110">To run the sample, perform the following steps:</span></span>
1. <span data-ttu-id="614ab-111">Create a new Command-Line App.</span><span class="sxs-lookup"><span data-stu-id="614ab-111">Create a new Command-Line App.</span></span>
2. <span data-ttu-id="614ab-112">Replace the Main class with the following code (keep any `package` statements).</span><span class="sxs-lookup"><span data-stu-id="614ab-112">Replace the Main class with the following code (keep any `package` statements).</span></span>
3. <span data-ttu-id="614ab-113">Replace the `[YOUR_SUBSCRIPTION_KEY]` value with your valid subscription key.</span><span class="sxs-lookup"><span data-stu-id="614ab-113">Replace the `[YOUR_SUBSCRIPTION_KEY]` value with your valid subscription key.</span></span>
4. <span data-ttu-id="614ab-114">Replace the `[REPLACE_WITH_THE_EXAMPLE_OR_YOUR_OWN_DATA_POINTS]` with the example or your own data points.</span><span class="sxs-lookup"><span data-stu-id="614ab-114">Replace the `[REPLACE_WITH_THE_EXAMPLE_OR_YOUR_OWN_DATA_POINTS]` with the example or your own data points.</span></span>
5. <span data-ttu-id="614ab-115">Download these global libraries from the Maven Repository to the `lib` directory in your project:</span><span class="sxs-lookup"><span data-stu-id="614ab-115">Download these global libraries from the Maven Repository to the `lib` directory in your project:</span></span>
   * `org.apache.httpcomponents:httpclient:4.5.2`
6. <span data-ttu-id="614ab-116">Run 'Main'.</span><span class="sxs-lookup"><span data-stu-id="614ab-116">Run 'Main'.</span></span>

```java

import org.apache.http.HttpEntity;
import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.util.EntityUtils;

public class Main {
    // **********************************************
    // *** Update or verify the following values. ***
    // **********************************************

    // Replace the subscriptionKey string value with your valid subscription key.
    public static final String subscriptionKey = "[YOUR_SUBSCRIPTION_KEY]";

    public static final String uriBase = "https://api.labs.cognitive.microsoft.com/anomalyfinder/v1.0/anomalydetection";

    public static void main(String[] args) {
        final String content = "[REPLACE_WITH_THE_EXAMPLE_OR_YOUR_OWN_DATA_POINTS]";

        CloseableHttpClient client = HttpClients.createDefault();
        HttpPost request = new HttpPost(uriBase);

        // Request headers.
        request.setHeader("Content-Type", "application/json");
        request.setHeader("Ocp-Apim-Subscription-Key", subscriptionKey);

        try {
            StringEntity params = new StringEntity(content);
            request.setEntity(params);

            CloseableHttpResponse response = client.execute(request);
            try {
                HttpEntity respEntity = response.getEntity();
                if (respEntity != null) {
                    System.out.println("----------");
                    System.out.println(response.getStatusLine());
                    System.out.println("Response content is :\n");
                    System.out.println(EntityUtils.toString(respEntity, "utf-8"));
                    System.out.println("----------");
                }
            } catch (Exception respEx) {
                respEx.printStackTrace();
            } finally {
                response.close();
            }

        } catch (Exception ex) {
            System.err.println("Exception on Anomaly Detection: " + ex.getMessage());
            ex.printStackTrace();
        } finally {
            try {
                client.close();
            } catch (Exception e) {
                System.err.println("Exception on closing HttpClient: " + e.getMessage());
                e.printStackTrace();
            }
        }
    }
}

```

### <a name="example-response"></a><span data-ttu-id="614ab-117">Example response</span><span class="sxs-lookup"><span data-stu-id="614ab-117">Example response</span></span>

<span data-ttu-id="614ab-118">A successful response is returned in JSON.</span><span class="sxs-lookup"><span data-stu-id="614ab-118">A successful response is returned in JSON.</span></span> <span data-ttu-id="614ab-119">Example response is as follows.</span><span class="sxs-lookup"><span data-stu-id="614ab-119">Example response is as follows.</span></span>
[!INCLUDE [Response](../includes/response.md)]

## <a name="next-steps"></a><span data-ttu-id="614ab-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="614ab-120">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="614ab-121">Java app</span><span class="sxs-lookup"><span data-stu-id="614ab-121">Java app</span></span>](../tutorials/java-tutorial.md)
