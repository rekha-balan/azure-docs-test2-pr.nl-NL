---
title: Anomaly Detection Javascript app - Microsoft Cognitive Services | Microsoft Docs
description: Explore a Javascript Web app that uses the Anomaly Detection API in Microsoft Cognitive Services. Send original data points to API and get the expected value and anomaly points.
services: cognitive-services
author: wenya
manager: bix
ms.service: cognitive-services
ms.technology: anomaly-detection
ms.topic: article
ms.date: 05/01/2018
ms.author: wenya
ms.openlocfilehash: 42c3941a05efe8b74f818cd99f3606b3073892a9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865576"
---
# <a name="anomaly-detection-javascript-application"></a><span data-ttu-id="b4e1c-104">Anomaly Detection Javascript application</span><span class="sxs-lookup"><span data-stu-id="b4e1c-104">Anomaly Detection Javascript application</span></span>

<span data-ttu-id="b4e1c-105">Explore a Web application that uses the Anomaly Detection REST API to detect an anomaly.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-105">Explore a Web application that uses the Anomaly Detection REST API to detect an anomaly.</span></span> <span data-ttu-id="b4e1c-106">The example submits the time series data to the Anomaly Detection API with your subscription key, then gets all the anomaly points and the expected value for each data point from the API.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-106">The example submits the time series data to the Anomaly Detection API with your subscription key, then gets all the anomaly points and the expected value for each data point from the API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4e1c-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b4e1c-107">Prerequisites</span></span>

### <a name="platform-requirements"></a><span data-ttu-id="b4e1c-108">Platform requirements</span><span class="sxs-lookup"><span data-stu-id="b4e1c-108">Platform requirements</span></span>

<span data-ttu-id="b4e1c-109">This tutorial has been developed using a simple text editor.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-109">This tutorial has been developed using a simple text editor.</span></span>

### <a name="subscribe-to-anomaly-detection-and-get-a-subscription-key"></a><span data-ttu-id="b4e1c-110">Subscribe to Anomaly Detection and get a subscription key</span><span class="sxs-lookup"><span data-stu-id="b4e1c-110">Subscribe to Anomaly Detection and get a subscription key</span></span> 

[!INCLUDE [GetSubscriptionKey](../includes/get-subscription-key.md)]

## <a name="get-and-use-the-example"></a><span data-ttu-id="b4e1c-111">Get and use the example</span><span class="sxs-lookup"><span data-stu-id="b4e1c-111">Get and use the example</span></span>

<span data-ttu-id="b4e1c-112">This tutorial provides two scenarios for time series data anomaly detection.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-112">This tutorial provides two scenarios for time series data anomaly detection.</span></span> <span data-ttu-id="b4e1c-113">Let's get started.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-113">Let's get started.</span></span>

<a name="Step1"></a> 
### <a name="download-the-tutorial-project"></a><span data-ttu-id="b4e1c-114">Download the tutorial project</span><span class="sxs-lookup"><span data-stu-id="b4e1c-114">Download the tutorial project</span></span>

<span data-ttu-id="b4e1c-115">Clone the [Cognitive Services JavaScript Anomaly Detection Tutorial](https://github.com/MicrosoftAnomalyDetection/javascript-sample), or download the .zip file and extract it to an empty directory.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-115">Clone the [Cognitive Services JavaScript Anomaly Detection Tutorial](https://github.com/MicrosoftAnomalyDetection/javascript-sample), or download the .zip file and extract it to an empty directory.</span></span>

<a name="Step2"></a>
### <a name="run-the-example"></a><span data-ttu-id="b4e1c-116">Run the example</span><span class="sxs-lookup"><span data-stu-id="b4e1c-116">Run the example</span></span>

<span data-ttu-id="b4e1c-117">There are two scenarios you can try the example.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-117">There are two scenarios you can try the example.</span></span>
1. <span data-ttu-id="b4e1c-118">Put your **subscription key** into the Subscription Key field on detect function on anomalydetection.html.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-118">Put your **subscription key** into the Subscription Key field on detect function on anomalydetection.html.</span></span>
2. <span data-ttu-id="b4e1c-119">Put anomaly detection API endpoint, and verify that you are using the correct region in Subscription Region.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-119">Put anomaly detection API endpoint, and verify that you are using the correct region in Subscription Region.</span></span>
3. <span data-ttu-id="b4e1c-120">Open the **anomalydetection.html** file in a Web browser.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-120">Open the **anomalydetection.html** file in a Web browser.</span></span>

<span data-ttu-id="b4e1c-121">**Scenario 1 Detect weekly time series data**</span><span class="sxs-lookup"><span data-stu-id="b4e1c-121">**Scenario 1 Detect weekly time series data**</span></span>
1. <span data-ttu-id="b4e1c-122">In Period field, input period **7**.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-122">In Period field, input period **7**.</span></span> 
2. <span data-ttu-id="b4e1c-123">Replace the sample data with your weekly time series data points (Json) in Points field, or use the sample data directly.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-123">Replace the sample data with your weekly time series data points (Json) in Points field, or use the sample data directly.</span></span>
3. <span data-ttu-id="b4e1c-124">Click the Anomaly Detection button and verify the result in the right Response text box.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-124">Click the Anomaly Detection button and verify the result in the right Response text box.</span></span>

<span data-ttu-id="b4e1c-125">**Scenario 2 Detect the time series data without a period**</span><span class="sxs-lookup"><span data-stu-id="b4e1c-125">**Scenario 2 Detect the time series data without a period**</span></span>
1. <span data-ttu-id="b4e1c-126">Leave the period empty in Period filed, assume that you don't know the period of the time series.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-126">Leave the period empty in Period filed, assume that you don't know the period of the time series.</span></span>
2. <span data-ttu-id="b4e1c-127">Using the same time series data as the scenario 1.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-127">Using the same time series data as the scenario 1.</span></span>
3. <span data-ttu-id="b4e1c-128">Click the Anomaly Detection button and verify the Period field in the right Response text box.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-128">Click the Anomaly Detection button and verify the Period field in the right Response text box.</span></span>

<a name="Step3"></a>
### <a name="read-the-result"></a><span data-ttu-id="b4e1c-129">Read the result</span><span class="sxs-lookup"><span data-stu-id="b4e1c-129">Read the result</span></span>

[!INCLUDE [diagrams](../includes/diagrams.md)]

<a name="Review"></a>
### <a name="review-and-learn"></a><span data-ttu-id="b4e1c-130">Review and learn</span><span class="sxs-lookup"><span data-stu-id="b4e1c-130">Review and learn</span></span>

<span data-ttu-id="b4e1c-131">Now you get a running application.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-131">Now you get a running application.</span></span> <span data-ttu-id="b4e1c-132">Let's review how the example app integrates with Cognitive Services technology.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-132">Let's review how the example app integrates with Cognitive Services technology.</span></span> <span data-ttu-id="b4e1c-133">This step will make it easier to either continue building on this app or develop your own app using Microsoft Anomaly Detection.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-133">This step will make it easier to either continue building on this app or develop your own app using Microsoft Anomaly Detection.</span></span>
<span data-ttu-id="b4e1c-134">This example app makes use of the Anomaly Detection Restful API endpoint.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-134">This example app makes use of the Anomaly Detection Restful API endpoint.</span></span>
<span data-ttu-id="b4e1c-135">Reviewing how the Restful API gets used in the example application, let's look at a code snippet from anomalydetection.html.</span><span class="sxs-lookup"><span data-stu-id="b4e1c-135">Reviewing how the Restful API gets used in the example application, let's look at a code snippet from anomalydetection.html.</span></span>
```JavaScript
function anomalyDetection(url, subscriptionKey, points, period) {
    var obj = new Object();
    obj.Points = JSON.parse(points); // this points are read from text box.
    obj.Period = parseInt(period);//period=7 weekly period
    var tsData = JSON.stringify(obj);
    // Perform the REST API call.
    $.ajax({
        url: url, //Anomaly Detection API endpoint
        // Request headers.
        beforeSend: function (xhrObj) {
            xhrObj.setRequestHeader("Content-Type", "application/json");
            xhrObj.setRequestHeader("Ocp-Apim-Subscription-Key", subscriptionKey); // Replace your subscription key
        },
        type: "POST",
        // Request body.
        data: tsData, // json format
        })
        .done(function (data) {
            // Show formatted JSON on webpage.
            $("#responseTextArea").val(JSON.stringify(data, null, 2));
        })
        .fail(function (jqXHR, textStatus, errorThrown) {
            // Display error message.
            var errorString = (errorThrown === "") ? "Error. " : errorThrown + " (" + jqXHR.status + "): ";
            errorString += (jqXHR.responseText === "") ? "" : jQuery.parseJSON(jqXHR.responseText).message;
            $("#responseTextArea").val(errorString);           
        });
}

```

## <a name="next-steps"></a><span data-ttu-id="b4e1c-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="b4e1c-136">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b4e1c-137">REST API reference</span><span class="sxs-lookup"><span data-stu-id="b4e1c-137">REST API reference</span></span>](https://dev.labs.cognitive.microsoft.com/docs/services/anomaly-detection/operations/post-anomalydetection)
