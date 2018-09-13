---
title: Anomaly Detection Java app - Microsoft Cognitive Services | Microsoft Docs
description: Explore a Java app that uses the Anomaly Detection API in Microsoft Cognitive Services. Send original data points to API and get the expected value and anomaly points.
services: cognitive-services
author: wenya
manager: bix
ms.service: cognitive-services
ms.technology: anomaly-detection
ms.topic: article
ms.date: 05/01/2018
ms.author: wenya
ms.openlocfilehash: 228d440da358eba1322e2228c54f21e925e36ecd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865748"
---
# <a name="anomaly-detection-java-application"></a><span data-ttu-id="ae2f6-104">Anomaly Detection Java application</span><span class="sxs-lookup"><span data-stu-id="ae2f6-104">Anomaly Detection Java application</span></span>

<span data-ttu-id="ae2f6-105">This article demonstrates using a simple Java application to invoke the Anomaly Detection API.</span><span class="sxs-lookup"><span data-stu-id="ae2f6-105">This article demonstrates using a simple Java application to invoke the Anomaly Detection API.</span></span>  
<span data-ttu-id="ae2f6-106">The example submits the time series data to the Anomaly Detection API with your subscription key, then gets all the anomaly points and expected value for each data point from the API.</span><span class="sxs-lookup"><span data-stu-id="ae2f6-106">The example submits the time series data to the Anomaly Detection API with your subscription key, then gets all the anomaly points and expected value for each data point from the API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae2f6-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ae2f6-107">Prerequisites</span></span>

### <a name="platform-requirements"></a><span data-ttu-id="ae2f6-108">Platform requirements</span><span class="sxs-lookup"><span data-stu-id="ae2f6-108">Platform requirements</span></span>

<span data-ttu-id="ae2f6-109">This tutorial has been developed using [IntelliJ IDEA](https://www.jetbrains.com/idea).</span><span class="sxs-lookup"><span data-stu-id="ae2f6-109">This tutorial has been developed using [IntelliJ IDEA](https://www.jetbrains.com/idea).</span></span> <span data-ttu-id="ae2f6-110">And also you need to install [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/index.html) version 1.8+, and an up-to-date [Apache's Maven](http://maven.apache.org/) build tool.</span><span class="sxs-lookup"><span data-stu-id="ae2f6-110">And also you need to install [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/index.html) version 1.8+, and an up-to-date [Apache's Maven](http://maven.apache.org/) build tool.</span></span>

### <a name="subscribe-to-anomaly-detection-and-get-a-subscription-key"></a><span data-ttu-id="ae2f6-111">Subscribe to Anomaly Detection and get a subscription key</span><span class="sxs-lookup"><span data-stu-id="ae2f6-111">Subscribe to Anomaly Detection and get a subscription key</span></span> 

[!INCLUDE [GetSubscriptionKey](../includes/get-subscription-key.md)]
 

## <a name="download-the-tutorial-project"></a><span data-ttu-id="ae2f6-112">Download the tutorial project</span><span class="sxs-lookup"><span data-stu-id="ae2f6-112">Download the tutorial project</span></span>

1. <span data-ttu-id="ae2f6-113">Go to the MicrosoftAnomalyDetection [Java repository](https://github.com/MicrosoftAnomalyDetection/java-sample).</span><span class="sxs-lookup"><span data-stu-id="ae2f6-113">Go to the MicrosoftAnomalyDetection [Java repository](https://github.com/MicrosoftAnomalyDetection/java-sample).</span></span>
2. <span data-ttu-id="ae2f6-114">Click the Clone or download button.</span><span class="sxs-lookup"><span data-stu-id="ae2f6-114">Click the Clone or download button.</span></span>
3. <span data-ttu-id="ae2f6-115">Click Download ZIP to download a .zip file of the tutorial project.</span><span class="sxs-lookup"><span data-stu-id="ae2f6-115">Click Download ZIP to download a .zip file of the tutorial project.</span></span>

<a name="Step1"></a>
### <a name="open-the-tutorial-project"></a><span data-ttu-id="ae2f6-116">Open the tutorial project</span><span class="sxs-lookup"><span data-stu-id="ae2f6-116">Open the tutorial project</span></span>

1. <span data-ttu-id="ae2f6-117">Extract the .zip file of the tutorial project.</span><span class="sxs-lookup"><span data-stu-id="ae2f6-117">Extract the .zip file of the tutorial project.</span></span>
2. <span data-ttu-id="ae2f6-118">In IntelliJ IDEA, click **File > Open**, Open File or Project dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="ae2f6-118">In IntelliJ IDEA, click **File > Open**, Open File or Project dialog box appears.</span></span>
3. <span data-ttu-id="ae2f6-119">Select the root path of the extracted project, then click OK.</span><span class="sxs-lookup"><span data-stu-id="ae2f6-119">Select the root path of the extracted project, then click OK.</span></span>
4. <span data-ttu-id="ae2f6-120">In the Projects panel, expand **src > main > java**.</span><span class="sxs-lookup"><span data-stu-id="ae2f6-120">In the Projects panel, expand **src > main > java**.</span></span>
5. <span data-ttu-id="ae2f6-121">Double-click com.microsoft.cognitiveservice.anomalydetection.Main.java to load the file into the editor.</span><span class="sxs-lookup"><span data-stu-id="ae2f6-121">Double-click com.microsoft.cognitiveservice.anomalydetection.Main.java to load the file into the editor.</span></span>

<a name="Step2"></a>
### <a name="replace-subscriptionkey-and-uri-region"></a><span data-ttu-id="ae2f6-122">Replace subscriptionKey and URI region</span><span class="sxs-lookup"><span data-stu-id="ae2f6-122">Replace subscriptionKey and URI region</span></span>

```
// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the subscriptionKey string value with your valid subscription key.
public static final String subscriptionKey = "<Subscription Key>";

public static final String uriBase = "https://api.labs.cognitive.microsoft.com/anomalyfinder/v1.0/anomalydetection";

```

<a name="Step3"></a>
### <a name="build-and-run-the-tutorial-project"></a><span data-ttu-id="ae2f6-123">Build and run the tutorial project</span><span class="sxs-lookup"><span data-stu-id="ae2f6-123">Build and run the tutorial project</span></span>

1. <span data-ttu-id="ae2f6-124">Bring up the menu by right-clicking anywhere in com.microsoft.cognitiveservice.anomalydetection.Main.java source code tab.</span><span class="sxs-lookup"><span data-stu-id="ae2f6-124">Bring up the menu by right-clicking anywhere in com.microsoft.cognitiveservice.anomalydetection.Main.java source code tab.</span></span> 
2. <span data-ttu-id="ae2f6-125">Select Run 'Main.main()'</span><span class="sxs-lookup"><span data-stu-id="ae2f6-125">Select Run 'Main.main()'</span></span>
3. <span data-ttu-id="ae2f6-126">The result of the sample request will be returned and shown in terminal.</span><span class="sxs-lookup"><span data-stu-id="ae2f6-126">The result of the sample request will be returned and shown in terminal.</span></span>

### <a name="result-of-the-tutorial-project"></a><span data-ttu-id="ae2f6-127">Result of the tutorial project</span><span class="sxs-lookup"><span data-stu-id="ae2f6-127">Result of the tutorial project</span></span>

[!INCLUDE [diagrams](../includes/diagrams.md)]

## <a name="next-steps"></a><span data-ttu-id="ae2f6-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="ae2f6-128">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ae2f6-129">REST API reference</span><span class="sxs-lookup"><span data-stu-id="ae2f6-129">REST API reference</span></span>](https://dev.labs.cognitive.microsoft.com/docs/services/anomaly-detection/operations/post-anomalydetection)
