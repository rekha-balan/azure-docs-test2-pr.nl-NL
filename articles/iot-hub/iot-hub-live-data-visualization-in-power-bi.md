---
title: Real-time data visualization of sensor data from Azure IoT Hub – Power BI | Microsoft Docs
description: Use Power BI to visualize temperature and humidity data that is collected from the sensor and sent to your Azure IoT hub.
author: rangv
manager: ''
keywords: real time data visualization, live data visualization, sensor data visualization
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.tgt_pltfrm: arduino
ms.date: 4/11/2018
ms.author: rangv
ms.openlocfilehash: a3c54fe635fe0f8988c321684a815e9896922587
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800623"
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a><span data-ttu-id="583c0-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span><span class="sxs-lookup"><span data-stu-id="583c0-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span></span>

![End-to-end diagram](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="583c0-106">What you learn</span><span class="sxs-lookup"><span data-stu-id="583c0-106">What you learn</span></span>

<span data-ttu-id="583c0-107">You learn how to visualize real-time sensor data that your Azure IoT hub receives by Power BI.</span><span class="sxs-lookup"><span data-stu-id="583c0-107">You learn how to visualize real-time sensor data that your Azure IoT hub receives by Power BI.</span></span> <span data-ttu-id="583c0-108">If you want to try visualize the data in your IoT hub with Web Apps, please see [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="583c0-108">If you want to try visualize the data in your IoT hub with Web Apps, please see [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="583c0-109">What you do</span><span class="sxs-lookup"><span data-stu-id="583c0-109">What you do</span></span>

- <span data-ttu-id="583c0-110">Get your IoT hub ready for data access by adding a consumer group.</span><span class="sxs-lookup"><span data-stu-id="583c0-110">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="583c0-111">Create, configure and run a Stream Analytics job for data transfer from your IoT hub to your Power BI account.</span><span class="sxs-lookup"><span data-stu-id="583c0-111">Create, configure and run a Stream Analytics job for data transfer from your IoT hub to your Power BI account.</span></span>
- <span data-ttu-id="583c0-112">Create and publish a Power BI report to visualize the data.</span><span class="sxs-lookup"><span data-stu-id="583c0-112">Create and publish a Power BI report to visualize the data.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="583c0-113">What you need</span><span class="sxs-lookup"><span data-stu-id="583c0-113">What you need</span></span>

- <span data-ttu-id="583c0-114">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span><span class="sxs-lookup"><span data-stu-id="583c0-114">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="583c0-115">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="583c0-115">An active Azure subscription.</span></span>
  - <span data-ttu-id="583c0-116">An Azure IoT hub under your subscription.</span><span class="sxs-lookup"><span data-stu-id="583c0-116">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="583c0-117">A client application that sends messages to your Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="583c0-117">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="583c0-118">A Power BI account.</span><span class="sxs-lookup"><span data-stu-id="583c0-118">A Power BI account.</span></span> <span data-ttu-id="583c0-119">([Try Power BI for free](https://powerbi.microsoft.com/))</span><span class="sxs-lookup"><span data-stu-id="583c0-119">([Try Power BI for free](https://powerbi.microsoft.com/))</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="583c0-120">Create, configure, and run a Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="583c0-120">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="583c0-121">Create a Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="583c0-121">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="583c0-122">In the [Azure portal](https://portal.azure.com), click **Create a resource** > **Internet of Things** > **Stream Analytics job**.</span><span class="sxs-lookup"><span data-stu-id="583c0-122">In the [Azure portal](https://portal.azure.com), click **Create a resource** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="583c0-123">Enter the following information for the job.</span><span class="sxs-lookup"><span data-stu-id="583c0-123">Enter the following information for the job.</span></span>

   <span data-ttu-id="583c0-124">**Job name**: The name of the job.</span><span class="sxs-lookup"><span data-stu-id="583c0-124">**Job name**: The name of the job.</span></span> <span data-ttu-id="583c0-125">The name must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="583c0-125">The name must be globally unique.</span></span>

   <span data-ttu-id="583c0-126">**Resource group**: Use the same resource group that your IoT hub uses.</span><span class="sxs-lookup"><span data-stu-id="583c0-126">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="583c0-127">**Location**: Use the same location as your resource group.</span><span class="sxs-lookup"><span data-stu-id="583c0-127">**Location**: Use the same location as your resource group.</span></span>

   <span data-ttu-id="583c0-128">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span><span class="sxs-lookup"><span data-stu-id="583c0-128">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Create a Stream Analytics job in Azure](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="583c0-130">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="583c0-130">Click **Create**.</span></span>

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="583c0-131">Add an input to the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="583c0-131">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="583c0-132">Open the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="583c0-132">Open the Stream Analytics job.</span></span>
1. <span data-ttu-id="583c0-133">Under **Job Topology**, click **Inputs**.</span><span class="sxs-lookup"><span data-stu-id="583c0-133">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="583c0-134">In the **Inputs** pane, click **Add**, and then enter the following information:</span><span class="sxs-lookup"><span data-stu-id="583c0-134">In the **Inputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="583c0-135">**Input alias**: The unique alias for the input.</span><span class="sxs-lookup"><span data-stu-id="583c0-135">**Input alias**: The unique alias for the input.</span></span>

   <span data-ttu-id="583c0-136">**Source**: Select **IoT hub**.</span><span class="sxs-lookup"><span data-stu-id="583c0-136">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="583c0-137">**Consumer group**: Select the consumer group you just created.</span><span class="sxs-lookup"><span data-stu-id="583c0-137">**Consumer group**: Select the consumer group you just created.</span></span>
1. <span data-ttu-id="583c0-138">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="583c0-138">Click **Create**.</span></span>

   ![Add an input to a Stream Analytics job in Azure](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="583c0-140">Add an output to the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="583c0-140">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="583c0-141">Under **Job Topology**, click **Outputs**.</span><span class="sxs-lookup"><span data-stu-id="583c0-141">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="583c0-142">In the **Outputs** pane, click **Add**, and then enter the following information:</span><span class="sxs-lookup"><span data-stu-id="583c0-142">In the **Outputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="583c0-143">**Output alias**: The unique alias for the output.</span><span class="sxs-lookup"><span data-stu-id="583c0-143">**Output alias**: The unique alias for the output.</span></span>

   <span data-ttu-id="583c0-144">**Sink**: Select **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="583c0-144">**Sink**: Select **Power BI**.</span></span>
1. <span data-ttu-id="583c0-145">Click **Authorize**, and then sign into your Power BI account.</span><span class="sxs-lookup"><span data-stu-id="583c0-145">Click **Authorize**, and then sign into your Power BI account.</span></span>
1. <span data-ttu-id="583c0-146">Once authorized, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="583c0-146">Once authorized, enter the following information:</span></span>

   <span data-ttu-id="583c0-147">**Group Workspace**: Select your target group workspace.</span><span class="sxs-lookup"><span data-stu-id="583c0-147">**Group Workspace**: Select your target group workspace.</span></span>

   <span data-ttu-id="583c0-148">**Dataset Name**: Enter a dataset name.</span><span class="sxs-lookup"><span data-stu-id="583c0-148">**Dataset Name**: Enter a dataset name.</span></span>

   <span data-ttu-id="583c0-149">**Table Name**: Enter a table name.</span><span class="sxs-lookup"><span data-stu-id="583c0-149">**Table Name**: Enter a table name.</span></span>
1. <span data-ttu-id="583c0-150">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="583c0-150">Click **Create**.</span></span>

   ![Add an output to a Stream Analytics job in Azure](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="583c0-152">Configure the query of the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="583c0-152">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="583c0-153">Under **Job Topology**, click **Query**.</span><span class="sxs-lookup"><span data-stu-id="583c0-153">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="583c0-154">Replace `[YourInputAlias]` with the input alias of the job.</span><span class="sxs-lookup"><span data-stu-id="583c0-154">Replace `[YourInputAlias]` with the input alias of the job.</span></span>
1. <span data-ttu-id="583c0-155">Replace `[YourOutputAlias]` with the output alias of the job.</span><span class="sxs-lookup"><span data-stu-id="583c0-155">Replace `[YourOutputAlias]` with the output alias of the job.</span></span>
1. <span data-ttu-id="583c0-156">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="583c0-156">Click **Save**.</span></span>

   ![Add a query to a Stream Analytics job in Azure](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="583c0-158">Run the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="583c0-158">Run the Stream Analytics job</span></span>

<span data-ttu-id="583c0-159">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span><span class="sxs-lookup"><span data-stu-id="583c0-159">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="583c0-160">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span><span class="sxs-lookup"><span data-stu-id="583c0-160">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

![Run a Stream Analytics job in Azure](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-to-visualize-the-data"></a><span data-ttu-id="583c0-162">Create and publish a Power BI report to visualize the data</span><span class="sxs-lookup"><span data-stu-id="583c0-162">Create and publish a Power BI report to visualize the data</span></span>

1. <span data-ttu-id="583c0-163">Ensure the sample application is running on your device.</span><span class="sxs-lookup"><span data-stu-id="583c0-163">Ensure the sample application is running on your device.</span></span> <span data-ttu-id="583c0-164">If not, you can refer to the tutorials under [Setup your device](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span><span class="sxs-lookup"><span data-stu-id="583c0-164">If not, you can refer to the tutorials under [Setup your device](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span></span>
1. <span data-ttu-id="583c0-165">Sign in to your [Power BI](https://powerbi.microsoft.com/en-us/) account.</span><span class="sxs-lookup"><span data-stu-id="583c0-165">Sign in to your [Power BI](https://powerbi.microsoft.com/en-us/) account.</span></span>
1. <span data-ttu-id="583c0-166">Go to the group workspace that you set when you created the output for the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="583c0-166">Go to the group workspace that you set when you created the output for the Stream Analytics job.</span></span>
1. <span data-ttu-id="583c0-167">Click **Streaming datasets**.</span><span class="sxs-lookup"><span data-stu-id="583c0-167">Click **Streaming datasets**.</span></span>

   <span data-ttu-id="583c0-168">You should see the listed dataset that you specified when you created the output for the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="583c0-168">You should see the listed dataset that you specified when you created the output for the Stream Analytics job.</span></span>
1. <span data-ttu-id="583c0-169">Under **ACTIONS**, click the first icon to create a report.</span><span class="sxs-lookup"><span data-stu-id="583c0-169">Under **ACTIONS**, click the first icon to create a report.</span></span>

   ![Create a Microsoft Power BI report](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. <span data-ttu-id="583c0-171">Create a line chart to show real-time temperature over time.</span><span class="sxs-lookup"><span data-stu-id="583c0-171">Create a line chart to show real-time temperature over time.</span></span>
   1. <span data-ttu-id="583c0-172">On the report creation page, add a line chart.</span><span class="sxs-lookup"><span data-stu-id="583c0-172">On the report creation page, add a line chart.</span></span>
   1. <span data-ttu-id="583c0-173">On the **Fields** pane, expand the table that you specified when you created the output for the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="583c0-173">On the **Fields** pane, expand the table that you specified when you created the output for the Stream Analytics job.</span></span>
   1. <span data-ttu-id="583c0-174">Drag **EventEnqueuedUtcTime** to **Axis** on the **Visualizations** pane.</span><span class="sxs-lookup"><span data-stu-id="583c0-174">Drag **EventEnqueuedUtcTime** to **Axis** on the **Visualizations** pane.</span></span>
   1. <span data-ttu-id="583c0-175">Drag **temperature** to **Values**.</span><span class="sxs-lookup"><span data-stu-id="583c0-175">Drag **temperature** to **Values**.</span></span>

      <span data-ttu-id="583c0-176">Now a line chart is created.</span><span class="sxs-lookup"><span data-stu-id="583c0-176">Now a line chart is created.</span></span> <span data-ttu-id="583c0-177">The x-axis displays date and time in the UTC time zone.</span><span class="sxs-lookup"><span data-stu-id="583c0-177">The x-axis displays date and time in the UTC time zone.</span></span> <span data-ttu-id="583c0-178">The y-axis displays temperature from the sensor.</span><span class="sxs-lookup"><span data-stu-id="583c0-178">The y-axis displays temperature from the sensor.</span></span>

      ![Add a line chart for temperature to a Microsoft Power BI report](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="583c0-180">Create another line chart to show real-time humidity over time.</span><span class="sxs-lookup"><span data-stu-id="583c0-180">Create another line chart to show real-time humidity over time.</span></span> <span data-ttu-id="583c0-181">To do this, follow the same steps above and place **EventEnqueuedUtcTime** on the x-axis and **humidity** on the y-axis.</span><span class="sxs-lookup"><span data-stu-id="583c0-181">To do this, follow the same steps above and place **EventEnqueuedUtcTime** on the x-axis and **humidity** on the y-axis.</span></span>

   ![Add a line chart for humidity to a Microsoft Power BI report](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="583c0-183">Click **Save** to save the report.</span><span class="sxs-lookup"><span data-stu-id="583c0-183">Click **Save** to save the report.</span></span>
1. <span data-ttu-id="583c0-184">Click **File** > **Publish to web**.</span><span class="sxs-lookup"><span data-stu-id="583c0-184">Click **File** > **Publish to web**.</span></span>
1. <span data-ttu-id="583c0-185">Click **Create embed code**, and then click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="583c0-185">Click **Create embed code**, and then click **Publish**.</span></span>

<span data-ttu-id="583c0-186">You're provided the report link that you can share with anyone for report access and a code snippet to integrate the report into your blog or website.</span><span class="sxs-lookup"><span data-stu-id="583c0-186">You're provided the report link that you can share with anyone for report access and a code snippet to integrate the report into your blog or website.</span></span>

![Publish a Microsoft Power BI report](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

<span data-ttu-id="583c0-188">Microsoft also offers the [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span><span class="sxs-lookup"><span data-stu-id="583c0-188">Microsoft also offers the [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="583c0-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="583c0-189">Next steps</span></span>

<span data-ttu-id="583c0-190">You’ve successfully used Power BI to visualize real-time sensor data from your Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="583c0-190">You’ve successfully used Power BI to visualize real-time sensor data from your Azure IoT hub.</span></span>
<span data-ttu-id="583c0-191">There is an alternate way to visualize data from Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="583c0-191">There is an alternate way to visualize data from Azure IoT Hub.</span></span> <span data-ttu-id="583c0-192">See [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="583c0-192">See [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
