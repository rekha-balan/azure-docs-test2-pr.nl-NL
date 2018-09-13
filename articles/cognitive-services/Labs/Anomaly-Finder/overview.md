---
title: What is Anomaly Finder? - Microsoft Cognitive Services | Microsoft Docs
description: Use advanced algorithms in Anomaly Finder to help you identify anomalies in time series data and return information in Microsoft Cognitive Services.
services: cognitive-services
author: tonyxing
ms.service: cognitive-services
ms.technology: anomaly-detection
ms.topic: article
ms.date: 04/19/2018
ms.author: tonyxing
ms.openlocfilehash: 1080bb0ad1d901a8b9a5ace4993d4e0d46924a03
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869721"
---
# <a name="what-is-anomaly-finder"></a><span data-ttu-id="8169f-104">What is Anomaly Finder?</span><span class="sxs-lookup"><span data-stu-id="8169f-104">What is Anomaly Finder?</span></span>

<span data-ttu-id="8169f-105">Anomaly Finder enables you to monitor data over time and detect anomalies with machine learning that adapts to your unique data by automatically applying the right statistical model regardless of industry, scenario, or data volume.</span><span class="sxs-lookup"><span data-stu-id="8169f-105">Anomaly Finder enables you to monitor data over time and detect anomalies with machine learning that adapts to your unique data by automatically applying the right statistical model regardless of industry, scenario, or data volume.</span></span> <span data-ttu-id="8169f-106">Using a time series as input, the Anomaly Finder API returns whether or not a data point is an anomaly, determines the expected value, and upper and lower bounds for visualization.</span><span class="sxs-lookup"><span data-stu-id="8169f-106">Using a time series as input, the Anomaly Finder API returns whether or not a data point is an anomaly, determines the expected value, and upper and lower bounds for visualization.</span></span> <span data-ttu-id="8169f-107">As a prebuilt AI service, Anomaly Finder doesn’t require any machine learning expertise beyond understanding how to use a RESTful API.</span><span class="sxs-lookup"><span data-stu-id="8169f-107">As a prebuilt AI service, Anomaly Finder doesn’t require any machine learning expertise beyond understanding how to use a RESTful API.</span></span> <span data-ttu-id="8169f-108">This makes development simple and versatile since it works with any time series data and can also be built into streaming data systems.</span><span class="sxs-lookup"><span data-stu-id="8169f-108">This makes development simple and versatile since it works with any time series data and can also be built into streaming data systems.</span></span> <span data-ttu-id="8169f-109">Anomaly Finder encompasses a broad span of use cases – for instance, financial tools for managing fraud, theft, changing markets, and potential business incidents, or monitoring IoT device traffic while preserving anonymity.</span><span class="sxs-lookup"><span data-stu-id="8169f-109">Anomaly Finder encompasses a broad span of use cases – for instance, financial tools for managing fraud, theft, changing markets, and potential business incidents, or monitoring IoT device traffic while preserving anonymity.</span></span> <span data-ttu-id="8169f-110">This solution can also be monetized as part of a service for end-customers to understand changes in data, spending, return on investment, or user activity.</span><span class="sxs-lookup"><span data-stu-id="8169f-110">This solution can also be monetized as part of a service for end-customers to understand changes in data, spending, return on investment, or user activity.</span></span>
<span data-ttu-id="8169f-111">Try out the Anomaly Finder API and gain deeper understanding of your data.</span><span class="sxs-lookup"><span data-stu-id="8169f-111">Try out the Anomaly Finder API and gain deeper understanding of your data.</span></span> 

<span data-ttu-id="8169f-112">See what you can build with this API:</span><span class="sxs-lookup"><span data-stu-id="8169f-112">See what you can build with this API:</span></span>

* <span data-ttu-id="8169f-113">Learn to predict the expected values based on historical data in the time series</span><span class="sxs-lookup"><span data-stu-id="8169f-113">Learn to predict the expected values based on historical data in the time series</span></span>
* <span data-ttu-id="8169f-114">Tell whether a data point is an anomaly out of historical pattern</span><span class="sxs-lookup"><span data-stu-id="8169f-114">Tell whether a data point is an anomaly out of historical pattern</span></span>
* <span data-ttu-id="8169f-115">Generate a band to visualize the range of "normal" value</span><span class="sxs-lookup"><span data-stu-id="8169f-115">Generate a band to visualize the range of "normal" value</span></span>

![Anomaly_Finder](./media/anomaly_detection1.png) 

<span data-ttu-id="8169f-117">Fig. 1: Detect anomalies in sales revenues</span><span class="sxs-lookup"><span data-stu-id="8169f-117">Fig. 1: Detect anomalies in sales revenues</span></span>

![Anomaly_Finder](./media/anomaly_detection2.png)

<span data-ttu-id="8169f-119">Fig. 2: Detect pattern changes in service requests</span><span class="sxs-lookup"><span data-stu-id="8169f-119">Fig. 2: Detect pattern changes in service requests</span></span>

## <a name="requirements"></a><span data-ttu-id="8169f-120">Requirements</span><span class="sxs-lookup"><span data-stu-id="8169f-120">Requirements</span></span>

- <span data-ttu-id="8169f-121">Minimum data for input time series: Minimum of 13 data points for time series without clear periodicity, minimum of 4 cycles of data points for the time series with known periodicity.</span><span class="sxs-lookup"><span data-stu-id="8169f-121">Minimum data for input time series: Minimum of 13 data points for time series without clear periodicity, minimum of 4 cycles of data points for the time series with known periodicity.</span></span> 
- <span data-ttu-id="8169f-122">Data integrity: time series data points are separated in the same interval and no missing points.</span><span class="sxs-lookup"><span data-stu-id="8169f-122">Data integrity: time series data points are separated in the same interval and no missing points.</span></span> 

## <a name="identify-anomalies"></a><span data-ttu-id="8169f-123">Identify anomalies</span><span class="sxs-lookup"><span data-stu-id="8169f-123">Identify anomalies</span></span>

<span data-ttu-id="8169f-124">Anomaly detection API returns result that whether any given data points are anomalies or not, and provides additional information as follows</span><span class="sxs-lookup"><span data-stu-id="8169f-124">Anomaly detection API returns result that whether any given data points are anomalies or not, and provides additional information as follows</span></span>
* <span data-ttu-id="8169f-125">Period - The periodicity that the API used to detect the anomaly points.</span><span class="sxs-lookup"><span data-stu-id="8169f-125">Period - The periodicity that the API used to detect the anomaly points.</span></span>
* <span data-ttu-id="8169f-126">WarningText - The possible warning information.</span><span class="sxs-lookup"><span data-stu-id="8169f-126">WarningText - The possible warning information.</span></span>
* <span data-ttu-id="8169f-127">ExpectedValue - The predicted value by the learning based model</span><span class="sxs-lookup"><span data-stu-id="8169f-127">ExpectedValue - The predicted value by the learning based model</span></span>
* <span data-ttu-id="8169f-128">IsAnomaly - The result on whether the data points are anomalies or not</span><span class="sxs-lookup"><span data-stu-id="8169f-128">IsAnomaly - The result on whether the data points are anomalies or not</span></span>
* <span data-ttu-id="8169f-129">IsAnomaly_Neg - The result on whether the data points are anomalies in negative direction (dips)</span><span class="sxs-lookup"><span data-stu-id="8169f-129">IsAnomaly_Neg - The result on whether the data points are anomalies in negative direction (dips)</span></span>
* <span data-ttu-id="8169f-130">IsAnomaly_Pos - The result on whether the data points are anomalies in positive direction (spikes)</span><span class="sxs-lookup"><span data-stu-id="8169f-130">IsAnomaly_Pos - The result on whether the data points are anomalies in positive direction (spikes)</span></span>
* <span data-ttu-id="8169f-131">UpperMargin - The sum of ExpectedValue and UpperMargin determines the upper bound that data point is still thought as normal</span><span class="sxs-lookup"><span data-stu-id="8169f-131">UpperMargin - The sum of ExpectedValue and UpperMargin determines the upper bound that data point is still thought as normal</span></span>
* <span data-ttu-id="8169f-132">LowerMargin - (ExpectedValue - LowerMargin) determines the lower bound that data point is still thought as normal</span><span class="sxs-lookup"><span data-stu-id="8169f-132">LowerMargin - (ExpectedValue - LowerMargin) determines the lower bound that data point is still thought as normal</span></span>

> [!Note]
> <span data-ttu-id="8169f-133">UpperMargin and LowerMargin can be used to generate a band around actual time series to visualize the range of normal values.</span><span class="sxs-lookup"><span data-stu-id="8169f-133">UpperMargin and LowerMargin can be used to generate a band around actual time series to visualize the range of normal values.</span></span> 

## <a name="adjusting-lower-and-upper-bounds-in-post-processing-on-the-response"></a><span data-ttu-id="8169f-134">Adjusting lower and upper bounds in post processing on the response</span><span class="sxs-lookup"><span data-stu-id="8169f-134">Adjusting lower and upper bounds in post processing on the response</span></span>

<span data-ttu-id="8169f-135">Anomaly detection API returns default result on whether a data point is anomaly or not, and the upper and lower bound can be calculated from ExpectedValue and UpperMargin/LowerMargin.</span><span class="sxs-lookup"><span data-stu-id="8169f-135">Anomaly detection API returns default result on whether a data point is anomaly or not, and the upper and lower bound can be calculated from ExpectedValue and UpperMargin/LowerMargin.</span></span> <span data-ttu-id="8169f-136">Those default values should work just fine for most cases.</span><span class="sxs-lookup"><span data-stu-id="8169f-136">Those default values should work just fine for most cases.</span></span> <span data-ttu-id="8169f-137">However, some scenarios require different bounds than the default ones.</span><span class="sxs-lookup"><span data-stu-id="8169f-137">However, some scenarios require different bounds than the default ones.</span></span> <span data-ttu-id="8169f-138">The recommend practice is applying a coefficiency on the UpperMargin or LowerMargin to adjust the dynamic bounds.</span><span class="sxs-lookup"><span data-stu-id="8169f-138">The recommend practice is applying a coefficiency on the UpperMargin or LowerMargin to adjust the dynamic bounds.</span></span>

### <a name="examples-with-1152-as-coefficiency"></a><span data-ttu-id="8169f-139">Examples with 1/1.5/2 as coefficiency</span><span class="sxs-lookup"><span data-stu-id="8169f-139">Examples with 1/1.5/2 as coefficiency</span></span>

![Default Sensitivity](./media/sensitivity_1.png)

![1.5 Sensitivity](./media/sensitivity_1.5.png)

![2 Sensitivity](./media/sensitivity_2.png)

<span data-ttu-id="8169f-143">Request with sample data</span><span class="sxs-lookup"><span data-stu-id="8169f-143">Request with sample data</span></span>

[!INCLUDE [Request](./includes/request.md)]

<span data-ttu-id="8169f-144">Sample JSON response</span><span class="sxs-lookup"><span data-stu-id="8169f-144">Sample JSON response</span></span>

[!INCLUDE [Response](./includes/response.md)]
