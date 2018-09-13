---
title: Real-time data visualization of sensor data from Azure IoT Hub – Power BI | Microsoft Docs
description: Use Power BI to visualize temperature and humidity data that is collected from the sensor and sent to your Azure IoT hub.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: real time data visualization, live data visualization, sensor data visualization
ms.assetid: e67c9c09-6219-4f0f-ad42-58edaaa74f61
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: xshi
ms.openlocfilehash: a0f8736ffa9cffe5403f17b2d8f53358c061def5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555905"
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a><span data-ttu-id="1c51b-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span><span class="sxs-lookup"><span data-stu-id="1c51b-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span></span>

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="1c51b-105">What you learn</span><span class="sxs-lookup"><span data-stu-id="1c51b-105">What you learn</span></span>

<span data-ttu-id="1c51b-106">You learn how to visualize real-time sensor data that your Azure IoT hub receives by Power BI.</span><span class="sxs-lookup"><span data-stu-id="1c51b-106">You learn how to visualize real-time sensor data that your Azure IoT hub receives by Power BI.</span></span> <span data-ttu-id="1c51b-107">If you want to try visualize the data in your IoT hub with Web Apps, please see [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="1c51b-107">If you want to try visualize the data in your IoT hub with Web Apps, please see [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="1c51b-108">What you do</span><span class="sxs-lookup"><span data-stu-id="1c51b-108">What you do</span></span>

- <span data-ttu-id="1c51b-109">Get your IoT hub ready for data access by adding a consumer group.</span><span class="sxs-lookup"><span data-stu-id="1c51b-109">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="1c51b-110">Create, configure and run a Stream Analytics job for data transfer from your IoT hub to your Power BI account.</span><span class="sxs-lookup"><span data-stu-id="1c51b-110">Create, configure and run a Stream Analytics job for data transfer from your IoT hub to your Power BI account.</span></span>
- <span data-ttu-id="1c51b-111">Create and publish a Power BI report to visualize the data.</span><span class="sxs-lookup"><span data-stu-id="1c51b-111">Create and publish a Power BI report to visualize the data.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1c51b-112">What you need</span><span class="sxs-lookup"><span data-stu-id="1c51b-112">What you need</span></span>

- <span data-ttu-id="1c51b-113">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span><span class="sxs-lookup"><span data-stu-id="1c51b-113">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="1c51b-114">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="1c51b-114">An active Azure subscription.</span></span>
  - <span data-ttu-id="1c51b-115">An Azure IoT hub under your subscription.</span><span class="sxs-lookup"><span data-stu-id="1c51b-115">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="1c51b-116">A client application that sends messages to your Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="1c51b-116">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="1c51b-117">A Power BI account.</span><span class="sxs-lookup"><span data-stu-id="1c51b-117">A Power BI account.</span></span> <span data-ttu-id="1c51b-118">([Try Power BI for free](https://powerbi.microsoft.com/))</span><span class="sxs-lookup"><span data-stu-id="1c51b-118">([Try Power BI for free](https://powerbi.microsoft.com/))</span></span>

## <a name="add-a-consumer-group-to-your-iot-hub"></a><span data-ttu-id="1c51b-119">Add a consumer group to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="1c51b-119">Add a consumer group to your IoT hub</span></span>

<span data-ttu-id="1c51b-120">Consumer groups are used by applications to pull data from Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1c51b-120">Consumer groups are used by applications to pull data from Azure IoT Hub.</span></span> <span data-ttu-id="1c51b-121">In this lesson, you create a consumer group to be used by a Stream Analytics job to read data from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="1c51b-121">In this lesson, you create a consumer group to be used by a Stream Analytics job to read data from your IoT hub.</span></span>

<span data-ttu-id="1c51b-122">To add a consumer group to your IoT hub, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="1c51b-122">To add a consumer group to your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="1c51b-123">In the [Azure portal](https://ms.portal.azure.com/), open your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="1c51b-123">In the [Azure portal](https://ms.portal.azure.com/), open your IoT hub.</span></span>
1. <span data-ttu-id="1c51b-124">Click **Endpoints** on the left pane, select **Events** on the middle pane, enter a name under **Consumer groups** on the right pane, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1c51b-124">Click **Endpoints** on the left pane, select **Events** on the middle pane, enter a name under **Consumer groups** on the right pane, and then click **Save**.</span></span>

   ![Create consumer group in Azure IoT Hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-live-data-visualization-in-power-bi/1_iot-hub-create-consumer-group-azure.png)

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="1c51b-126">Create, configure, and run a Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="1c51b-126">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="1c51b-127">Create a Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="1c51b-127">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="1c51b-128">In the Azure portal, click New > Internet of Things > Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="1c51b-128">In the Azure portal, click New > Internet of Things > Stream Analytics job.</span></span>
1. <span data-ttu-id="1c51b-129">Enter the following information for the job.</span><span class="sxs-lookup"><span data-stu-id="1c51b-129">Enter the following information for the job.</span></span>

   <span data-ttu-id="1c51b-130">**Job name**: The name of the job.</span><span class="sxs-lookup"><span data-stu-id="1c51b-130">**Job name**: The name of the job.</span></span> <span data-ttu-id="1c51b-131">The name must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="1c51b-131">The name must be globally unique.</span></span>

   <span data-ttu-id="1c51b-132">**Resource group**: Use the same resource group that your IoT hub uses.</span><span class="sxs-lookup"><span data-stu-id="1c51b-132">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="1c51b-133">**Location**: Use the same location as your resource group.</span><span class="sxs-lookup"><span data-stu-id="1c51b-133">**Location**: Use the same location as your resource group.</span></span>

   <span data-ttu-id="1c51b-134">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span><span class="sxs-lookup"><span data-stu-id="1c51b-134">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Create a Stream Analytics job in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="1c51b-136">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1c51b-136">Click **Create**.</span></span>

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="1c51b-137">Add an input to the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="1c51b-137">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="1c51b-138">Open the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="1c51b-138">Open the Stream Analytics job.</span></span>
1. <span data-ttu-id="1c51b-139">Under **Job Topology**, click **Inputs**.</span><span class="sxs-lookup"><span data-stu-id="1c51b-139">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="1c51b-140">In the **Inputs** pane, click **Add**, and then enter the following information:</span><span class="sxs-lookup"><span data-stu-id="1c51b-140">In the **Inputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="1c51b-141">**Input alias**: The unique alias for the input.</span><span class="sxs-lookup"><span data-stu-id="1c51b-141">**Input alias**: The unique alias for the input.</span></span>

   <span data-ttu-id="1c51b-142">**Source**: Select **IoT hub**.</span><span class="sxs-lookup"><span data-stu-id="1c51b-142">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="1c51b-143">**Consumer group**: Select the consumer group you just created.</span><span class="sxs-lookup"><span data-stu-id="1c51b-143">**Consumer group**: Select the consumer group you just created.</span></span>
1. <span data-ttu-id="1c51b-144">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1c51b-144">Click **Create**.</span></span>

   ![Add an input to a Stream Analytics job in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="1c51b-146">Add an output to the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="1c51b-146">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="1c51b-147">Under **Job Topology**, click **Outputs**.</span><span class="sxs-lookup"><span data-stu-id="1c51b-147">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="1c51b-148">In the **Outputs** pane, click **Add**, and then enter the following information:</span><span class="sxs-lookup"><span data-stu-id="1c51b-148">In the **Outputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="1c51b-149">**Output alias**: The unique alias for the output.</span><span class="sxs-lookup"><span data-stu-id="1c51b-149">**Output alias**: The unique alias for the output.</span></span>

   <span data-ttu-id="1c51b-150">**Sink**: Select **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="1c51b-150">**Sink**: Select **Power BI**.</span></span>
1. <span data-ttu-id="1c51b-151">Click **Authorize**, and then sign into your Power BI account.</span><span class="sxs-lookup"><span data-stu-id="1c51b-151">Click **Authorize**, and then sign into your Power BI account.</span></span>
1. <span data-ttu-id="1c51b-152">Once authorized, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="1c51b-152">Once authorized, enter the following information:</span></span>

   <span data-ttu-id="1c51b-153">**Group Workspace**: Select your target group workspace.</span><span class="sxs-lookup"><span data-stu-id="1c51b-153">**Group Workspace**: Select your target group workspace.</span></span>

   <span data-ttu-id="1c51b-154">**Dataset Name**: Enter a dataset name.</span><span class="sxs-lookup"><span data-stu-id="1c51b-154">**Dataset Name**: Enter a dataset name.</span></span>

   <span data-ttu-id="1c51b-155">**Table Name**: Enter a table name.</span><span class="sxs-lookup"><span data-stu-id="1c51b-155">**Table Name**: Enter a table name.</span></span>
1. <span data-ttu-id="1c51b-156">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1c51b-156">Click **Create**.</span></span>

   ![Add an output to a Stream Analytics job in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="1c51b-158">Configure the query of the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="1c51b-158">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="1c51b-159">Under **Job Topology**, click **Query**.</span><span class="sxs-lookup"><span data-stu-id="1c51b-159">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="1c51b-160">Replace `[YourInputAlias]` with the input alias of the job.</span><span class="sxs-lookup"><span data-stu-id="1c51b-160">Replace `[YourInputAlias]` with the input alias of the job.</span></span>
1. <span data-ttu-id="1c51b-161">Replace `[YourOutputAlias]` with the output alias of the job.</span><span class="sxs-lookup"><span data-stu-id="1c51b-161">Replace `[YourOutputAlias]` with the output alias of the job.</span></span>
1. <span data-ttu-id="1c51b-162">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1c51b-162">Click **Save**.</span></span>

   ![Add a query to a Stream Analytics job in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="1c51b-164">Run the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="1c51b-164">Run the Stream Analytics job</span></span>

<span data-ttu-id="1c51b-165">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span><span class="sxs-lookup"><span data-stu-id="1c51b-165">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="1c51b-166">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span><span class="sxs-lookup"><span data-stu-id="1c51b-166">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

![Run a Stream Analytics job in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-to-visualize-the-data"></a><span data-ttu-id="1c51b-168">Create and publish a Power BI report to visualize the data</span><span class="sxs-lookup"><span data-stu-id="1c51b-168">Create and publish a Power BI report to visualize the data</span></span>

1. <span data-ttu-id="1c51b-169">Ensure the sample application is running.</span><span class="sxs-lookup"><span data-stu-id="1c51b-169">Ensure the sample application is running.</span></span> <span data-ttu-id="1c51b-170">If not, run the following command to run the application on Pi:</span><span class="sxs-lookup"><span data-stu-id="1c51b-170">If not, run the following command to run the application on Pi:</span></span>

   ```bash
   gulp run
   ```
1. <span data-ttu-id="1c51b-171">Sign in to your [Power BI](https://powerbi.microsoft.com/en-us/) account.</span><span class="sxs-lookup"><span data-stu-id="1c51b-171">Sign in to your [Power BI](https://powerbi.microsoft.com/en-us/) account.</span></span>
1. <span data-ttu-id="1c51b-172">Go to the group workspace that you set when you created the output for the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="1c51b-172">Go to the group workspace that you set when you created the output for the Stream Analytics job.</span></span>
1. <span data-ttu-id="1c51b-173">Click **Streaming datasets**.</span><span class="sxs-lookup"><span data-stu-id="1c51b-173">Click **Streaming datasets**.</span></span>

   <span data-ttu-id="1c51b-174">You should see the listed dataset that you specified when you created the output for the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="1c51b-174">You should see the listed dataset that you specified when you created the output for the Stream Analytics job.</span></span>
1. <span data-ttu-id="1c51b-175">Under **ACTIONS**, click the first icon to create a report.</span><span class="sxs-lookup"><span data-stu-id="1c51b-175">Under **ACTIONS**, click the first icon to create a report.</span></span>

   ![Create a Microsoft Power BI report](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. <span data-ttu-id="1c51b-177">Create a line chart to show real-time temperature over time.</span><span class="sxs-lookup"><span data-stu-id="1c51b-177">Create a line chart to show real-time temperature over time.</span></span>
   1. <span data-ttu-id="1c51b-178">On the report creation page, add a line chart.</span><span class="sxs-lookup"><span data-stu-id="1c51b-178">On the report creation page, add a line chart.</span></span>
   1. <span data-ttu-id="1c51b-179">On the **Fields** pane, expand the table that you specified when you created the output for the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="1c51b-179">On the **Fields** pane, expand the table that you specified when you created the output for the Stream Analytics job.</span></span>
   1. <span data-ttu-id="1c51b-180">Drag **EventEnqueuedUtcTime** to **Axis** on the **Visualizations** pane.</span><span class="sxs-lookup"><span data-stu-id="1c51b-180">Drag **EventEnqueuedUtcTime** to **Axis** on the **Visualizations** pane.</span></span>
   1. <span data-ttu-id="1c51b-181">Drag **temperature** to **Values**.</span><span class="sxs-lookup"><span data-stu-id="1c51b-181">Drag **temperature** to **Values**.</span></span>

      <span data-ttu-id="1c51b-182">Now a line chart is created.</span><span class="sxs-lookup"><span data-stu-id="1c51b-182">Now a line chart is created.</span></span> <span data-ttu-id="1c51b-183">The x-axis of chart displays date and time in the UTC time zone.</span><span class="sxs-lookup"><span data-stu-id="1c51b-183">The x-axis of chart displays date and time in the UTC time zone.</span></span> <span data-ttu-id="1c51b-184">The y-axis displays temperature from the sensor.</span><span class="sxs-lookup"><span data-stu-id="1c51b-184">The y-axis displays temperature from the sensor.</span></span>

      ![Add a line chart for temperature to a Microsoft Power BI report](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="1c51b-186">Create another line chart to show real-time humidity over time.</span><span class="sxs-lookup"><span data-stu-id="1c51b-186">Create another line chart to show real-time humidity over time.</span></span> <span data-ttu-id="1c51b-187">To do this, follow the same steps above and place **EventEnqueuedUtcTime** on the x-axis and **humidity** on the y-axis.</span><span class="sxs-lookup"><span data-stu-id="1c51b-187">To do this, follow the same steps above and place **EventEnqueuedUtcTime** on the x-axis and **humidity** on the y-axis.</span></span>

   ![Add a line chart for humidity to a Microsoft Power BI report](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="1c51b-189">Click **Save** to save the report.</span><span class="sxs-lookup"><span data-stu-id="1c51b-189">Click **Save** to save the report.</span></span>
1. <span data-ttu-id="1c51b-190">Click **File** > **Publish to web**.</span><span class="sxs-lookup"><span data-stu-id="1c51b-190">Click **File** > **Publish to web**.</span></span>
1. <span data-ttu-id="1c51b-191">Click **Create embed code**, and then click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="1c51b-191">Click **Create embed code**, and then click **Publish**.</span></span>

<span data-ttu-id="1c51b-192">You're provided the report link that you can share with anyone for report access and a code snippet to integrate the report into your blog or website.</span><span class="sxs-lookup"><span data-stu-id="1c51b-192">You're provided the report link that you can share with anyone for report access and a code snippet to integrate the report into your blog or website.</span></span>

![Publish a Microsoft Power BI report](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

<span data-ttu-id="1c51b-194">Microsoft also offers the [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span><span class="sxs-lookup"><span data-stu-id="1c51b-194">Microsoft also offers the [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c51b-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="1c51b-195">Next steps</span></span>

<span data-ttu-id="1c51b-196">You’ve successfully used Power BI to visualize real-time sensor data from your Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="1c51b-196">You’ve successfully used Power BI to visualize real-time sensor data from your Azure IoT hub.</span></span>
<span data-ttu-id="1c51b-197">There is an alternate way to visualize data from Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1c51b-197">There is an alternate way to visualize data from Azure IoT Hub.</span></span> <span data-ttu-id="1c51b-198">See [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="1c51b-198">See [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]









