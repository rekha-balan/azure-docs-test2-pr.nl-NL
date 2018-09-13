---
title: Create custom analytics for your Azure IoT Central application | Microsoft Docs
description: As an operator, how to create custom analytics for your Azure IoT Central application.
author: lmasieri
ms.author: lmasieri
ms.date: 08/26/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpr
ms.openlocfilehash: 0a78c534605b6eab08d5b12674689f0459e80b26
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867063"
---
# <a name="how-to-use-analytics-to-analyze-your-device-data"></a><span data-ttu-id="f7d3d-103">How to use analytics to analyze your device data</span><span class="sxs-lookup"><span data-stu-id="f7d3d-103">How to use analytics to analyze your device data</span></span>

<span data-ttu-id="f7d3d-104">Microsoft Azure IoT Central provides rich analytics capabilities to make sense of large amounts of data from your devices.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-104">Microsoft Azure IoT Central provides rich analytics capabilities to make sense of large amounts of data from your devices.</span></span> <span data-ttu-id="f7d3d-105">To get started, visit **Analytics** on the left navigation menu.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-105">To get started, visit **Analytics** on the left navigation menu.</span></span> 

  ![IoT Central navigation to analytics](media\howto-create-analytics\analytics-navigation.png)

## <a name="querying-your-data"></a><span data-ttu-id="f7d3d-107">Querying your data</span><span class="sxs-lookup"><span data-stu-id="f7d3d-107">Querying your data</span></span>

<span data-ttu-id="f7d3d-108">You'll need to choose a **device set**, add a **filter** (optional), and select a **time period** to get started.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-108">You'll need to choose a **device set**, add a **filter** (optional), and select a **time period** to get started.</span></span> <span data-ttu-id="f7d3d-109">Once you're done, click on *Show results* to start visualizing your data.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-109">Once you're done, click on *Show results* to start visualizing your data.</span></span>


* <span data-ttu-id="f7d3d-110">**Device sets:** A [device set](howto-use-device-sets.md) is a user-defined group of your devices.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-110">**Device sets:** A [device set](howto-use-device-sets.md) is a user-defined group of your devices.</span></span> <span data-ttu-id="f7d3d-111">For example, all Refrigerators in Oakland, or All rev 2.0 wind turbines.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-111">For example, all Refrigerators in Oakland, or All rev 2.0 wind turbines.</span></span>

<!---
to-do: confirm if 10 is the max number of filters
to-do: do we need to explain how fiters work?
--->

* <span data-ttu-id="f7d3d-112">**Filters:** You can optionally add filters to your search to hone in on your data.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-112">**Filters:** You can optionally add filters to your search to hone in on your data.</span></span> <span data-ttu-id="f7d3d-113">You can add up to 10 filters at a time.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-113">You can add up to 10 filters at a time.</span></span> <span data-ttu-id="f7d3d-114">For example, within all Refrigerators in Oakland, find those that have had temperature go above 60 degrees.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-114">For example, within all Refrigerators in Oakland, find those that have had temperature go above 60 degrees.</span></span> 
* <span data-ttu-id="f7d3d-115">**Time period:** By default we'll retrieve data from the past 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-115">**Time period:** By default we'll retrieve data from the past 10 minutes.</span></span> <span data-ttu-id="f7d3d-116">You can change this value to one of the predefined time ranges or select a custom time period.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-116">You can change this value to one of the predefined time ranges or select a custom time period.</span></span> 

 ![Analytics query](media\howto-create-analytics\analytics-query.png)

## <a name="visualizing-your-data"></a><span data-ttu-id="f7d3d-118">Visualizing your data</span><span class="sxs-lookup"><span data-stu-id="f7d3d-118">Visualizing your data</span></span>

<span data-ttu-id="f7d3d-119">Once you've queried your data, you'll be able to start visualizing it.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-119">Once you've queried your data, you'll be able to start visualizing it.</span></span> <span data-ttu-id="f7d3d-120">You can show/hide measurements, change the way data is aggregated, and further split the data by different device properties.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-120">You can show/hide measurements, change the way data is aggregated, and further split the data by different device properties.</span></span>  

* <span data-ttu-id="f7d3d-121">**Split by:** Splitting data by device properties enables you to further drill down into your data.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-121">**Split by:** Splitting data by device properties enables you to further drill down into your data.</span></span> <span data-ttu-id="f7d3d-122">For example, you can split your results by device ID or location.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-122">For example, you can split your results by device ID or location.</span></span>
<!---
to-do: confirm if 10 is the max number of measurements
--->
* <span data-ttu-id="f7d3d-123">**Measurements:** You can choose to show/hide up to 10 different telemetry items being reported by your devices at a time.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-123">**Measurements:** You can choose to show/hide up to 10 different telemetry items being reported by your devices at a time.</span></span> <span data-ttu-id="f7d3d-124">Measurements are things such as temperature and humidity.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-124">Measurements are things such as temperature and humidity.</span></span> 
* <span data-ttu-id="f7d3d-125">**Aggregation:** By default we aggregate data by its average, but you can choose to change the data aggregation to something else to fit your needs.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-125">**Aggregation:** By default we aggregate data by its average, but you can choose to change the data aggregation to something else to fit your needs.</span></span> 

   <span data-ttu-id="f7d3d-126">![Analytics visualization](media\howto-create-analytics\analytics-visualize.png)</span><span class="sxs-lookup"><span data-stu-id="f7d3d-126">![Analytics visualization](media\howto-create-analytics\analytics-visualize.png)</span></span> <br/><br/>
   <span data-ttu-id="f7d3d-127">![Analytics visualization split by](media\howto-create-analytics\analytics-splitby.png)</span><span class="sxs-lookup"><span data-stu-id="f7d3d-127">![Analytics visualization split by](media\howto-create-analytics\analytics-splitby.png)</span></span>

## <a name="interacting-with-your-data"></a><span data-ttu-id="f7d3d-128">Interacting with your data</span><span class="sxs-lookup"><span data-stu-id="f7d3d-128">Interacting with your data</span></span>

<span data-ttu-id="f7d3d-129">You have various ways in which you can further change your query results to meet your visualization needs.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-129">You have various ways in which you can further change your query results to meet your visualization needs.</span></span> <span data-ttu-id="f7d3d-130">You can alternate between a graph view and a grid view, zoom in/out, refresh your data set, and alter how lines are shown.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-130">You can alternate between a graph view and a grid view, zoom in/out, refresh your data set, and alter how lines are shown.</span></span>

* <span data-ttu-id="f7d3d-131">**Show grid:** Your results will be available in table format to enabling you to view the specific value for each data point.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-131">**Show grid:** Your results will be available in table format to enabling you to view the specific value for each data point.</span></span> <span data-ttu-id="f7d3d-132">This view also meets accessibility standards.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-132">This view also meets accessibility standards.</span></span> 
* <span data-ttu-id="f7d3d-133">**Show chart:** Your results will be displayed in a line format to easily spots upward/downward trends and anomalies.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-133">**Show chart:** Your results will be displayed in a line format to easily spots upward/downward trends and anomalies.</span></span> 

 ![Showing the grid view for your analytics](media\howto-create-analytics\analytics-showgrid.png)

<span data-ttu-id="f7d3d-135">Zoom enables you to hone in on your data.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-135">Zoom enables you to hone in on your data.</span></span> <span data-ttu-id="f7d3d-136">If you find a time period you'd like to focus on within your result set, using your cursor grab the area that you'd like to zoom in on and use the available controls to perform one of the following actions:</span><span class="sxs-lookup"><span data-stu-id="f7d3d-136">If you find a time period you'd like to focus on within your result set, using your cursor grab the area that you'd like to zoom in on and use the available controls to perform one of the following actions:</span></span>
* <span data-ttu-id="f7d3d-137">**Zoom in:** Once you've selected a time period, zoom in will be enabled and allow you to zoom in to your data.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-137">**Zoom in:** Once you've selected a time period, zoom in will be enabled and allow you to zoom in to your data.</span></span>
* <span data-ttu-id="f7d3d-138">**Zoom out:** This control enables you to zoom out one level from your last zoom.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-138">**Zoom out:** This control enables you to zoom out one level from your last zoom.</span></span> <span data-ttu-id="f7d3d-139">For example, if you've zoom in to your data three times, zoom out will take you back one step at a time.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-139">For example, if you've zoom in to your data three times, zoom out will take you back one step at a time.</span></span>
* <span data-ttu-id="f7d3d-140">**Zoom reset:** Once you've performed various levels of zooming, you can use the zoom reset control to return to your original result set.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-140">**Zoom reset:** Once you've performed various levels of zooming, you can use the zoom reset control to return to your original result set.</span></span> 

 ![Perform zooming on your data](media\howto-create-analytics\analytics-zoom.png)


<span data-ttu-id="f7d3d-142">You can change the line style to meet your needs.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-142">You can change the line style to meet your needs.</span></span> <span data-ttu-id="f7d3d-143">You have four options to choose from:</span><span class="sxs-lookup"><span data-stu-id="f7d3d-143">You have four options to choose from:</span></span>
* <span data-ttu-id="f7d3d-144">**Line:** A flat line between each of the data points will be formed.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-144">**Line:** A flat line between each of the data points will be formed.</span></span> 
* <span data-ttu-id="f7d3d-145">**Smooth:** A curved line between each point will be formed</span><span class="sxs-lookup"><span data-stu-id="f7d3d-145">**Smooth:** A curved line between each point will be formed</span></span>
* <span data-ttu-id="f7d3d-146">**Step:** Line between each point on the chart will create a step chart</span><span class="sxs-lookup"><span data-stu-id="f7d3d-146">**Step:** Line between each point on the chart will create a step chart</span></span>
* <span data-ttu-id="f7d3d-147">**Scatter:** All points will be plotted on the chart without lines connecting them.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-147">**Scatter:** All points will be plotted on the chart without lines connecting them.</span></span> 

 ![Different line types available in Analytics](media\howto-create-analytics\analytics-linetypes.png)

<span data-ttu-id="f7d3d-149">Lastly, you can arrange your data across the Y-axis by choosing from one of the three modes:</span><span class="sxs-lookup"><span data-stu-id="f7d3d-149">Lastly, you can arrange your data across the Y-axis by choosing from one of the three modes:</span></span>

* <span data-ttu-id="f7d3d-150">**Stacked:** A graph for every measurement is stacked and each of the graphs have their own Y-axis.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-150">**Stacked:** A graph for every measurement is stacked and each of the graphs have their own Y-axis.</span></span> <span data-ttu-id="f7d3d-151">Stacked graphs are useful when you have multiple measurements selected and want to have distinct view of these measurements.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-151">Stacked graphs are useful when you have multiple measurements selected and want to have distinct view of these measurements.</span></span>
* <span data-ttu-id="f7d3d-152">**Unstacked:** A graph for every measure is plotted against one Y-axis, but the values for the Y-axis are changed based on the highlighted measure.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-152">**Unstacked:** A graph for every measure is plotted against one Y-axis, but the values for the Y-axis are changed based on the highlighted measure.</span></span> <span data-ttu-id="f7d3d-153">Unstacked graphs are useful when you want to overlay multiple measures and want to see patterns across these measures for the same time range.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-153">Unstacked graphs are useful when you want to overlay multiple measures and want to see patterns across these measures for the same time range.</span></span>
* <span data-ttu-id="f7d3d-154">**Shared Y-axis:** All the graphs share the same Y-axis and the values for the axis do not change.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-154">**Shared Y-axis:** All the graphs share the same Y-axis and the values for the axis do not change.</span></span> <span data-ttu-id="f7d3d-155">Shared Y-axis graphs are useful when you want to look at a single measure while slicing the data with split-by.</span><span class="sxs-lookup"><span data-stu-id="f7d3d-155">Shared Y-axis graphs are useful when you want to look at a single measure while slicing the data with split-by.</span></span>

 ![Arrange data across y-axis with different visualization modes](media\howto-create-analytics\analytics-yaxis.png)

## <a name="next-steps"></a><span data-ttu-id="f7d3d-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="f7d3d-157">Next steps</span></span>

<span data-ttu-id="f7d3d-158">Now that you have learned how to create custom analytics for your Azure IoT Central application, here the suggested next step is:</span><span class="sxs-lookup"><span data-stu-id="f7d3d-158">Now that you have learned how to create custom analytics for your Azure IoT Central application, here the suggested next step is:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f7d3d-159">Prepare and connect a Node.js application</span><span class="sxs-lookup"><span data-stu-id="f7d3d-159">Prepare and connect a Node.js application</span></span>](howto-connect-nodejs.md)