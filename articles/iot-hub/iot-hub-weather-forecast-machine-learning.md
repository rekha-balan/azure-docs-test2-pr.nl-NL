---
title: Weather forecast using Azure Machine Learning with data from IoT Hub | Microsoft Docs
description: Use Azure Machine Learning to predict the chance of rain based on the temperature and humidity data your IoT hub collects from a sensor.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: weather forecast machine learning
ms.assetid: 8ba7d9e7-699c-4448-b353-0f3e1429d198
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: xshi
ms.openlocfilehash: 52206c26d26b6b335a17071ebe30cd87c2ec41f6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555740"
---
# <a name="weather-forecast-using-the-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a><span data-ttu-id="6edc5-104">Weather forecast using the sensor data from your IoT hub in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6edc5-104">Weather forecast using the sensor data from your IoT hub in Azure Machine Learning</span></span>

![Connection between sensor, IoT device, IoT Hub, Stream Analytics job, Azure machine learning, and Blob storage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/1_Connection-azure-machine-learning-iot-hub.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="6edc5-106">Machine learning is a technique of data science that helps computers learn from existing data to forecast future behaviors, outcomes, and trends.</span><span class="sxs-lookup"><span data-stu-id="6edc5-106">Machine learning is a technique of data science that helps computers learn from existing data to forecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="6edc5-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible to quickly create and deploy predictive models as analytics solutions.</span><span class="sxs-lookup"><span data-stu-id="6edc5-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible to quickly create and deploy predictive models as analytics solutions.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="6edc5-108">What you learn</span><span class="sxs-lookup"><span data-stu-id="6edc5-108">What you learn</span></span>

<span data-ttu-id="6edc5-109">You learn how to use Azure Machine Learning to do weather forecast (chance of rain) using the temperature and humidity data from your Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6edc5-109">You learn how to use Azure Machine Learning to do weather forecast (chance of rain) using the temperature and humidity data from your Azure IoT hub.</span></span> <span data-ttu-id="6edc5-110">The chance of rain is the output of a prepared weather prediction model.</span><span class="sxs-lookup"><span data-stu-id="6edc5-110">The chance of rain is the output of a prepared weather prediction model.</span></span> <span data-ttu-id="6edc5-111">The model is built upon historic data to forecast chance of rain based on temperature and humidity.</span><span class="sxs-lookup"><span data-stu-id="6edc5-111">The model is built upon historic data to forecast chance of rain based on temperature and humidity.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="6edc5-112">What you do</span><span class="sxs-lookup"><span data-stu-id="6edc5-112">What you do</span></span>

- <span data-ttu-id="6edc5-113">Deploy the weather prediction model as a web service.</span><span class="sxs-lookup"><span data-stu-id="6edc5-113">Deploy the weather prediction model as a web service.</span></span>
- <span data-ttu-id="6edc5-114">Get your IoT hub ready for data access by adding a consumer group.</span><span class="sxs-lookup"><span data-stu-id="6edc5-114">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="6edc5-115">Create a Stream Analytics job and configure the job to:</span><span class="sxs-lookup"><span data-stu-id="6edc5-115">Create a Stream Analytics job and configure the job to:</span></span>
  - <span data-ttu-id="6edc5-116">Read temperature and humidity data from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6edc5-116">Read temperature and humidity data from your IoT hub.</span></span>
  - <span data-ttu-id="6edc5-117">Call the web service to get the rain chance.</span><span class="sxs-lookup"><span data-stu-id="6edc5-117">Call the web service to get the rain chance.</span></span>
  - <span data-ttu-id="6edc5-118">Save the result to an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="6edc5-118">Save the result to an Azure blob storage.</span></span>
- <span data-ttu-id="6edc5-119">Use Microsoft Azure Storage Explorer to view the weather forecast.</span><span class="sxs-lookup"><span data-stu-id="6edc5-119">Use Microsoft Azure Storage Explorer to view the weather forecast.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6edc5-120">What you need</span><span class="sxs-lookup"><span data-stu-id="6edc5-120">What you need</span></span>

- <span data-ttu-id="6edc5-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span><span class="sxs-lookup"><span data-stu-id="6edc5-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="6edc5-122">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="6edc5-122">An active Azure subscription.</span></span>
  - <span data-ttu-id="6edc5-123">An Azure IoT hub under your subscription.</span><span class="sxs-lookup"><span data-stu-id="6edc5-123">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="6edc5-124">A client application that sends messages to your Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6edc5-124">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="6edc5-125">An Azure Machine Learning Studio account.</span><span class="sxs-lookup"><span data-stu-id="6edc5-125">An Azure Machine Learning Studio account.</span></span> <span data-ttu-id="6edc5-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span><span class="sxs-lookup"><span data-stu-id="6edc5-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span></span>

## <a name="deploy-the-weather-prediction-model-as-a-web-service"></a><span data-ttu-id="6edc5-127">Deploy the weather prediction model as a web service</span><span class="sxs-lookup"><span data-stu-id="6edc5-127">Deploy the weather prediction model as a web service</span></span>

1. <span data-ttu-id="6edc5-128">Go to the [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span><span class="sxs-lookup"><span data-stu-id="6edc5-128">Go to the [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span></span>
1. <span data-ttu-id="6edc5-129">Click **Open in Studio** in Microsoft Azure Machine Leaning Studio.</span><span class="sxs-lookup"><span data-stu-id="6edc5-129">Click **Open in Studio** in Microsoft Azure Machine Leaning Studio.</span></span>
   <span data-ttu-id="6edc5-130">![Open the weather prediction model page in Cortana Intelligence Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span><span class="sxs-lookup"><span data-stu-id="6edc5-130">![Open the weather prediction model page in Cortana Intelligence Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span></span>
1. <span data-ttu-id="6edc5-131">Click **Run** to validate the steps in the model.</span><span class="sxs-lookup"><span data-stu-id="6edc5-131">Click **Run** to validate the steps in the model.</span></span> <span data-ttu-id="6edc5-132">This step might take 2 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="6edc5-132">This step might take 2 minutes to complete.</span></span>
   <span data-ttu-id="6edc5-133">![Open the weather prediction model in Azure Machine Learning Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="6edc5-133">![Open the weather prediction model in Azure Machine Learning Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="6edc5-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span><span class="sxs-lookup"><span data-stu-id="6edc5-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span></span>
   <span data-ttu-id="6edc5-135">![Deploy the weather prediction model in Azure Machine Learning Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="6edc5-135">![Deploy the weather prediction model in Azure Machine Learning Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="6edc5-136">In the diagram, drag the **Web service input** module somewhere near the **Score Model** module.</span><span class="sxs-lookup"><span data-stu-id="6edc5-136">In the diagram, drag the **Web service input** module somewhere near the **Score Model** module.</span></span>
1. <span data-ttu-id="6edc5-137">Connect the **Web service input** module to the **Score Model** module.</span><span class="sxs-lookup"><span data-stu-id="6edc5-137">Connect the **Web service input** module to the **Score Model** module.</span></span>
   <span data-ttu-id="6edc5-138">![Connect two modules in Azure Machine Learning Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="6edc5-138">![Connect two modules in Azure Machine Learning Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="6edc5-139">Click **RUN** to validate the steps in the model.</span><span class="sxs-lookup"><span data-stu-id="6edc5-139">Click **RUN** to validate the steps in the model.</span></span>
1. <span data-ttu-id="6edc5-140">Click **DEPLOY WEB SERVICE** to deploy the model as a web service.</span><span class="sxs-lookup"><span data-stu-id="6edc5-140">Click **DEPLOY WEB SERVICE** to deploy the model as a web service.</span></span>
1. <span data-ttu-id="6edc5-141">On the dashboard of the model, download the **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span><span class="sxs-lookup"><span data-stu-id="6edc5-141">On the dashboard of the model, download the **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span></span>

   > [!Note]
   > <span data-ttu-id="6edc5-142">Ensure that you download the **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span><span class="sxs-lookup"><span data-stu-id="6edc5-142">Ensure that you download the **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span></span>

   ![Download the Excel for the REQUEST RESPONSE endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. <span data-ttu-id="6edc5-144">Open the Excel workbook, make a note of the **WEB SERVICE URL** and **ACCESS KEY**.</span><span class="sxs-lookup"><span data-stu-id="6edc5-144">Open the Excel workbook, make a note of the **WEB SERVICE URL** and **ACCESS KEY**.</span></span>

## <a name="add-a-consumer-group-to-your-iot-hub"></a><span data-ttu-id="6edc5-145">Add a consumer group to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="6edc5-145">Add a consumer group to your IoT hub</span></span>

<span data-ttu-id="6edc5-146">Consumer groups are used by applications to read data from Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6edc5-146">Consumer groups are used by applications to read data from Azure IoT Hub.</span></span> <span data-ttu-id="6edc5-147">In this lesson, you create a consumer group to be used by the web service to read data from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6edc5-147">In this lesson, you create a consumer group to be used by the web service to read data from your IoT hub.</span></span>

<span data-ttu-id="6edc5-148">To add a consumer group to your IoT hub, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="6edc5-148">To add a consumer group to your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="6edc5-149">In the [Azure portal](https://ms.portal.azure.com/), open your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6edc5-149">In the [Azure portal](https://ms.portal.azure.com/), open your IoT hub.</span></span>
1. <span data-ttu-id="6edc5-150">Click **Endpoints** on the left pane, select **Events** on the middle pane, enter a name under **Consumer groups** on the right pane, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="6edc5-150">Click **Endpoints** on the left pane, select **Events** on the middle pane, enter a name under **Consumer groups** on the right pane, and then click **Save**.</span></span>

   ![Add a consumer group to your IoT hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/6_add-consumer-group-iot-hub-azure.png)

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="6edc5-152">Create, configure, and run a Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="6edc5-152">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="6edc5-153">Create a Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="6edc5-153">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="6edc5-154">In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span><span class="sxs-lookup"><span data-stu-id="6edc5-154">In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="6edc5-155">Enter the following information for the job.</span><span class="sxs-lookup"><span data-stu-id="6edc5-155">Enter the following information for the job.</span></span>

   <span data-ttu-id="6edc5-156">**Job name**: The name of the job.</span><span class="sxs-lookup"><span data-stu-id="6edc5-156">**Job name**: The name of the job.</span></span> <span data-ttu-id="6edc5-157">The name must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="6edc5-157">The name must be globally unique.</span></span>

   <span data-ttu-id="6edc5-158">**Resource group**: Use the same resource group that your IoT hub uses.</span><span class="sxs-lookup"><span data-stu-id="6edc5-158">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="6edc5-159">**Location**: Use the same location as your resource group.</span><span class="sxs-lookup"><span data-stu-id="6edc5-159">**Location**: Use the same location as your resource group.</span></span>

   <span data-ttu-id="6edc5-160">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span><span class="sxs-lookup"><span data-stu-id="6edc5-160">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Create a Stream Analytics job in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="6edc5-162">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6edc5-162">Click **Create**.</span></span>

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="6edc5-163">Add an input to the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="6edc5-163">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="6edc5-164">Open the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="6edc5-164">Open the Stream Analytics job.</span></span>
1. <span data-ttu-id="6edc5-165">Under **Job Topology**, click **Inputs**.</span><span class="sxs-lookup"><span data-stu-id="6edc5-165">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="6edc5-166">In the **Inputs** pane, click **Add**, and then enter the following information:</span><span class="sxs-lookup"><span data-stu-id="6edc5-166">In the **Inputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="6edc5-167">**Input alias**: The unique alias for the input.</span><span class="sxs-lookup"><span data-stu-id="6edc5-167">**Input alias**: The unique alias for the input.</span></span>

   <span data-ttu-id="6edc5-168">**Source**: Select **IoT hub**.</span><span class="sxs-lookup"><span data-stu-id="6edc5-168">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="6edc5-169">**Consumer group**: Select the consumer group you created.</span><span class="sxs-lookup"><span data-stu-id="6edc5-169">**Consumer group**: Select the consumer group you created.</span></span>

   ![Add an input to the Stream Analytics job in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. <span data-ttu-id="6edc5-171">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6edc5-171">Click **Create**.</span></span>

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="6edc5-172">Add an output to the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="6edc5-172">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="6edc5-173">Under **Job Topology**, click **Outputs**.</span><span class="sxs-lookup"><span data-stu-id="6edc5-173">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="6edc5-174">In the **Outputs** pane, click **Add**, and then enter the following information:</span><span class="sxs-lookup"><span data-stu-id="6edc5-174">In the **Outputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="6edc5-175">**Output alias**: The unique alias for the output.</span><span class="sxs-lookup"><span data-stu-id="6edc5-175">**Output alias**: The unique alias for the output.</span></span>

   <span data-ttu-id="6edc5-176">**Sink**: Select **Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="6edc5-176">**Sink**: Select **Blob Storage**.</span></span>

   <span data-ttu-id="6edc5-177">**Storage account**: The storage account for your blob storage.</span><span class="sxs-lookup"><span data-stu-id="6edc5-177">**Storage account**: The storage account for your blob storage.</span></span> <span data-ttu-id="6edc5-178">You can create a storage account or use an existing one.</span><span class="sxs-lookup"><span data-stu-id="6edc5-178">You can create a storage account or use an existing one.</span></span>

   <span data-ttu-id="6edc5-179">**Container**: The container where the blob is saved.</span><span class="sxs-lookup"><span data-stu-id="6edc5-179">**Container**: The container where the blob is saved.</span></span> <span data-ttu-id="6edc5-180">You can create a container or use an existing one.</span><span class="sxs-lookup"><span data-stu-id="6edc5-180">You can create a container or use an existing one.</span></span>

   <span data-ttu-id="6edc5-181">**Event serialization format**: Select **CSV**.</span><span class="sxs-lookup"><span data-stu-id="6edc5-181">**Event serialization format**: Select **CSV**.</span></span>

   ![Add an output to the Stream Analytics job in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. <span data-ttu-id="6edc5-183">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6edc5-183">Click **Create**.</span></span>

### <a name="add-a-function-to-the-stream-analytics-job-to-call-the-web-service-you-deployed"></a><span data-ttu-id="6edc5-184">Add a function to the Stream Analytics job to call the web service you deployed</span><span class="sxs-lookup"><span data-stu-id="6edc5-184">Add a function to the Stream Analytics job to call the web service you deployed</span></span>

1. <span data-ttu-id="6edc5-185">Under **Job Topology**, click **Functions** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="6edc5-185">Under **Job Topology**, click **Functions** > **Add**.</span></span>
1. <span data-ttu-id="6edc5-186">Enter the following information:</span><span class="sxs-lookup"><span data-stu-id="6edc5-186">Enter the following information:</span></span>

   <span data-ttu-id="6edc5-187">**Function Alias**: Enter `machinelearning`.</span><span class="sxs-lookup"><span data-stu-id="6edc5-187">**Function Alias**: Enter `machinelearning`.</span></span>

   <span data-ttu-id="6edc5-188">**Function Type**: Select **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="6edc5-188">**Function Type**: Select **Azure ML**.</span></span>

   <span data-ttu-id="6edc5-189">**Import option**: Select **Import from a different subscription**.</span><span class="sxs-lookup"><span data-stu-id="6edc5-189">**Import option**: Select **Import from a different subscription**.</span></span>

   <span data-ttu-id="6edc5-190">**URL**: Enter the WEB SERVICE URL that you noted down from the Excel workbook.</span><span class="sxs-lookup"><span data-stu-id="6edc5-190">**URL**: Enter the WEB SERVICE URL that you noted down from the Excel workbook.</span></span>

   <span data-ttu-id="6edc5-191">**Key**: Enter the ACCESS KEY that you noted down from the Excel workbook.</span><span class="sxs-lookup"><span data-stu-id="6edc5-191">**Key**: Enter the ACCESS KEY that you noted down from the Excel workbook.</span></span>

   ![Add a function to the Stream Analytics job in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. <span data-ttu-id="6edc5-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6edc5-193">Click **Create**.</span></span>

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="6edc5-194">Configure the query of the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="6edc5-194">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="6edc5-195">Under **Job Topology**, click **Query**.</span><span class="sxs-lookup"><span data-stu-id="6edc5-195">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="6edc5-196">Replace the existing code with the following code:</span><span class="sxs-lookup"><span data-stu-id="6edc5-196">Replace the existing code with the following code:</span></span>

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   <span data-ttu-id="6edc5-197">Replace `[YourInputAlias]` with the input alias of the job.</span><span class="sxs-lookup"><span data-stu-id="6edc5-197">Replace `[YourInputAlias]` with the input alias of the job.</span></span>

   <span data-ttu-id="6edc5-198">Replace `[YourOutputAlias]` with the output alias of the job.</span><span class="sxs-lookup"><span data-stu-id="6edc5-198">Replace `[YourOutputAlias]` with the output alias of the job.</span></span>

1. <span data-ttu-id="6edc5-199">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="6edc5-199">Click **Save**.</span></span>

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="6edc5-200">Run the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="6edc5-200">Run the Stream Analytics job</span></span>

<span data-ttu-id="6edc5-201">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span><span class="sxs-lookup"><span data-stu-id="6edc5-201">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="6edc5-202">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span><span class="sxs-lookup"><span data-stu-id="6edc5-202">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

![Run the Stream Analytics job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-to-view-the-weather-forecast"></a><span data-ttu-id="6edc5-204">Use Microsoft Azure Storage Explorer to view the weather forecast</span><span class="sxs-lookup"><span data-stu-id="6edc5-204">Use Microsoft Azure Storage Explorer to view the weather forecast</span></span>

<span data-ttu-id="6edc5-205">Run the client application to start collecting and sending temperature and humidity data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6edc5-205">Run the client application to start collecting and sending temperature and humidity data to your IoT hub.</span></span> <span data-ttu-id="6edc5-206">For each message that your IoT hub receives, the Stream Analytics job calls the weather forecast web service to produce the chance of rain.</span><span class="sxs-lookup"><span data-stu-id="6edc5-206">For each message that your IoT hub receives, the Stream Analytics job calls the weather forecast web service to produce the chance of rain.</span></span> <span data-ttu-id="6edc5-207">The result is then saved to your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="6edc5-207">The result is then saved to your Azure blob storage.</span></span> <span data-ttu-id="6edc5-208">Azure Storage Explorer is a tool that you can use to view the result.</span><span class="sxs-lookup"><span data-stu-id="6edc5-208">Azure Storage Explorer is a tool that you can use to view the result.</span></span>

1. <span data-ttu-id="6edc5-209">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="6edc5-209">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="6edc5-210">Open Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="6edc5-210">Open Azure Storage Explorer.</span></span>
1. <span data-ttu-id="6edc5-211">Sign in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="6edc5-211">Sign in to your Azure account.</span></span>
1. <span data-ttu-id="6edc5-212">Select your subscription.</span><span class="sxs-lookup"><span data-stu-id="6edc5-212">Select your subscription.</span></span>
1. <span data-ttu-id="6edc5-213">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span><span class="sxs-lookup"><span data-stu-id="6edc5-213">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>
1. <span data-ttu-id="6edc5-214">Open a .csv file to see the result.</span><span class="sxs-lookup"><span data-stu-id="6edc5-214">Open a .csv file to see the result.</span></span> <span data-ttu-id="6edc5-215">The last column records the chance of rain.</span><span class="sxs-lookup"><span data-stu-id="6edc5-215">The last column records the chance of rain.</span></span>

   ![Get weather forecast result with Azure Machine Learning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a><span data-ttu-id="6edc5-217">Summary</span><span class="sxs-lookup"><span data-stu-id="6edc5-217">Summary</span></span>

<span data-ttu-id="6edc5-218">You’ve successfully used Azure Machine Learning to produce the chance of rain based on the temperature and humidity data that your IoT hub receives.</span><span class="sxs-lookup"><span data-stu-id="6edc5-218">You’ve successfully used Azure Machine Learning to produce the chance of rain based on the temperature and humidity data that your IoT hub receives.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]












