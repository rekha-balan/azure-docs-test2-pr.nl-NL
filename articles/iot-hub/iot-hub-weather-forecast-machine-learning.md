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
# <a name="weather-forecast-using-the-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a>Weather forecast using the sensor data from your IoT hub in Azure Machine Learning

![Connection between sensor, IoT device, IoT Hub, Stream Analytics job, Azure machine learning, and Blob storage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/1_Connection-azure-machine-learning-iot-hub.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

Machine learning is a technique of data science that helps computers learn from existing data to forecast future behaviors, outcomes, and trends. Azure Machine Learning is a cloud predictive analytics service that makes it possible to quickly create and deploy predictive models as analytics solutions.

## <a name="what-you-learn"></a>What you learn

You learn how to use Azure Machine Learning to do weather forecast (chance of rain) using the temperature and humidity data from your Azure IoT hub. The chance of rain is the output of a prepared weather prediction model. The model is built upon historic data to forecast chance of rain based on temperature and humidity.

## <a name="what-you-do"></a>What you do

- Deploy the weather prediction model as a web service.
- Get your IoT hub ready for data access by adding a consumer group.
- Create a Stream Analytics job and configure the job to:
  - Read temperature and humidity data from your IoT hub.
  - Call the web service to get the rain chance.
  - Save the result to an Azure blob storage.
- Use Microsoft Azure Storage Explorer to view the weather forecast.

## <a name="what-you-need"></a>What you need

- Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:
  - An active Azure subscription.
  - An Azure IoT hub under your subscription.
  - A client application that sends messages to your Azure IoT hub.
- An Azure Machine Learning Studio account. ([Try Machine Learning Studio for free](https://studio.azureml.net/)).

## <a name="deploy-the-weather-prediction-model-as-a-web-service"></a>Deploy the weather prediction model as a web service

1. Go to the [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).
1. Click **Open in Studio** in Microsoft Azure Machine Leaning Studio.
   ![Open the weather prediction model page in Cortana Intelligence Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)
1. Click **Run** to validate the steps in the model. This step might take 2 minutes to complete.
   ![Open the weather prediction model in Azure Machine Learning Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)
1. Click **SET UP WEB SERVICE** > **Predictive Web Service**.
   ![Deploy the weather prediction model in Azure Machine Learning Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)
1. In the diagram, drag the **Web service input** module somewhere near the **Score Model** module.
1. Connect the **Web service input** module to the **Score Model** module.
   ![Connect two modules in Azure Machine Learning Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)
1. Click **RUN** to validate the steps in the model.
1. Click **DEPLOY WEB SERVICE** to deploy the model as a web service.
1. On the dashboard of the model, download the **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.

   > [!Note]
   > Ensure that you download the **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.

   ![Download the Excel for the REQUEST RESPONSE endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. Open the Excel workbook, make a note of the **WEB SERVICE URL** and **ACCESS KEY**.

## <a name="add-a-consumer-group-to-your-iot-hub"></a>Add a consumer group to your IoT hub

Consumer groups are used by applications to read data from Azure IoT Hub. In this lesson, you create a consumer group to be used by the web service to read data from your IoT hub.

To add a consumer group to your IoT hub, follow these steps:

1. In the [Azure portal](https://ms.portal.azure.com/), open your IoT hub.
1. Click **Endpoints** on the left pane, select **Events** on the middle pane, enter a name under **Consumer groups** on the right pane, and then click **Save**.

   ![Add a consumer group to your IoT hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/6_add-consumer-group-iot-hub-azure.png)

## <a name="create-configure-and-run-a-stream-analytics-job"></a>Create, configure, and run a Stream Analytics job

### <a name="create-a-stream-analytics-job"></a>Create a Stream Analytics job

1. In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.
1. Enter the following information for the job.

   **Job name**: The name of the job. The name must be globally unique.

   **Resource group**: Use the same resource group that your IoT hub uses.

   **Location**: Use the same location as your resource group.

   **Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.

   ![Create a Stream Analytics job in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. Click **Create**.

### <a name="add-an-input-to-the-stream-analytics-job"></a>Add an input to the Stream Analytics job

1. Open the Stream Analytics job.
1. Under **Job Topology**, click **Inputs**.
1. In the **Inputs** pane, click **Add**, and then enter the following information:

   **Input alias**: The unique alias for the input.

   **Source**: Select **IoT hub**.

   **Consumer group**: Select the consumer group you created.

   ![Add an input to the Stream Analytics job in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. Click **Create**.

### <a name="add-an-output-to-the-stream-analytics-job"></a>Add an output to the Stream Analytics job

1. Under **Job Topology**, click **Outputs**.
1. In the **Outputs** pane, click **Add**, and then enter the following information:

   **Output alias**: The unique alias for the output.

   **Sink**: Select **Blob Storage**.

   **Storage account**: The storage account for your blob storage. You can create a storage account or use an existing one.

   **Container**: The container where the blob is saved. You can create a container or use an existing one.

   **Event serialization format**: Select **CSV**.

   ![Add an output to the Stream Analytics job in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. Click **Create**.

### <a name="add-a-function-to-the-stream-analytics-job-to-call-the-web-service-you-deployed"></a>Add a function to the Stream Analytics job to call the web service you deployed

1. Under **Job Topology**, click **Functions** > **Add**.
1. Enter the following information:

   **Function Alias**: Enter `machinelearning`.

   **Function Type**: Select **Azure ML**.

   **Import option**: Select **Import from a different subscription**.

   **URL**: Enter the WEB SERVICE URL that you noted down from the Excel workbook.

   **Key**: Enter the ACCESS KEY that you noted down from the Excel workbook.

   ![Add a function to the Stream Analytics job in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. Click **Create**.

### <a name="configure-the-query-of-the-stream-analytics-job"></a>Configure the query of the Stream Analytics job

1. Under **Job Topology**, click **Query**.
1. Replace the existing code with the following code:

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   Replace `[YourInputAlias]` with the input alias of the job.

   Replace `[YourOutputAlias]` with the output alias of the job.

1. Click **Save**.

### <a name="run-the-stream-analytics-job"></a>Run the Stream Analytics job

In the Stream Analytics job, click **Start** > **Now** > **Start**. Once the job successfully starts, the job status changes from **Stopped** to **Running**.

![Run the Stream Analytics job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-to-view-the-weather-forecast"></a>Use Microsoft Azure Storage Explorer to view the weather forecast

Run the client application to start collecting and sending temperature and humidity data to your IoT hub. For each message that your IoT hub receives, the Stream Analytics job calls the weather forecast web service to produce the chance of rain. The result is then saved to your Azure blob storage. Azure Storage Explorer is a tool that you can use to view the result.

1. [Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).
1. Open Azure Storage Explorer.
1. Sign in to your Azure account.
1. Select your subscription.
1. Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.
1. Open a .csv file to see the result. The last column records the chance of rain.

   ![Get weather forecast result with Azure Machine Learning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a>Summary

You’ve successfully used Azure Machine Learning to produce the chance of rain based on the temperature and humidity data that your IoT hub receives.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]












