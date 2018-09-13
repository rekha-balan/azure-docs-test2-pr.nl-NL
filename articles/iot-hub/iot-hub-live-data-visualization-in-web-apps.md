---
title: Real-time data visualization of sensor data from Azure IoT Hub – Web Apps | Microsoft Docs
description: Use Azure Web Apps to visualize temperature and humidity data that is collected from the sensor and sent to your Azure IoT hub.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: real time data visualization, live data visualization, sensor data visualization
ms.assetid: e42b07a8-ddd4-476e-9bfb-903d6b033e91
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: xshi
ms.openlocfilehash: 25e967293a0bf26d5646465277cf8fc55b44d21d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564641"
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-azure-web-apps"></a><span data-ttu-id="a6f9a-104">Visualize real-time sensor data from Azure IoT Hub using Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="a6f9a-104">Visualize real-time sensor data from Azure IoT Hub using Azure Web Apps</span></span>

![Connection between sensor, IoT device, IoT Hub and Azure web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-live-data-visualization-in-web-apps/1_sensor-iot-device-azure-iot-hub-web-app-connection.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="a6f9a-106">What you learn</span><span class="sxs-lookup"><span data-stu-id="a6f9a-106">What you learn</span></span>

<span data-ttu-id="a6f9a-107">In this lesson, you learn how to visualize real-time sensor data that your Azure IoT hub receives by running a web application that is hosted on an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-107">In this lesson, you learn how to visualize real-time sensor data that your Azure IoT hub receives by running a web application that is hosted on an Azure web app.</span></span> <span data-ttu-id="a6f9a-108">If you want to try visualize the data in your IoT hub with Power BI, please see [Use Power BI to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="a6f9a-108">If you want to try visualize the data in your IoT hub with Power BI, please see [Use Power BI to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="a6f9a-109">What you do</span><span class="sxs-lookup"><span data-stu-id="a6f9a-109">What you do</span></span>

- <span data-ttu-id="a6f9a-110">Create an Azure web app in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-110">Create an Azure web app in the Azure Portal.</span></span>
- <span data-ttu-id="a6f9a-111">Get your IoT hub ready for data access by adding a consumer group.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-111">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="a6f9a-112">Configure the web app to read sensor data from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-112">Configure the web app to read sensor data from your IoT hub.</span></span>
- <span data-ttu-id="a6f9a-113">Upload a web application to be hosted by the web app.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-113">Upload a web application to be hosted by the web app.</span></span>
- <span data-ttu-id="a6f9a-114">Open the web app to see real-time temperature and humidity data from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-114">Open the web app to see real-time temperature and humidity data from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a6f9a-115">What you need</span><span class="sxs-lookup"><span data-stu-id="a6f9a-115">What you need</span></span>

- <span data-ttu-id="a6f9a-116">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span><span class="sxs-lookup"><span data-stu-id="a6f9a-116">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="a6f9a-117">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-117">An active Azure subscription.</span></span>
  - <span data-ttu-id="a6f9a-118">An Azure IoT hub under your subscription.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-118">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="a6f9a-119">A client application that sends messages to your Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-119">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="a6f9a-120">Git.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-120">Git.</span></span> <span data-ttu-id="a6f9a-121">([Download Git](https://www.git-scm.com/downloads)).</span><span class="sxs-lookup"><span data-stu-id="a6f9a-121">([Download Git](https://www.git-scm.com/downloads)).</span></span>

## <a name="create-an-azure-web-app"></a><span data-ttu-id="a6f9a-122">Create an Azure web app</span><span class="sxs-lookup"><span data-stu-id="a6f9a-122">Create an Azure web app</span></span>

1. <span data-ttu-id="a6f9a-123">In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Web + Mobile** > **Web App**.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-123">In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Web + Mobile** > **Web App**.</span></span>
1. <span data-ttu-id="a6f9a-124">Enter a unique job name, verify the subscription, specify a resource group and a location, select **Pin to dashboard**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-124">Enter a unique job name, verify the subscription, specify a resource group and a location, select **Pin to dashboard**, and then click **Create**.</span></span>

   <span data-ttu-id="a6f9a-125">We recommend you select the same location where your resource group is located.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-125">We recommend you select the same location where your resource group is located.</span></span> <span data-ttu-id="a6f9a-126">This assists with processing speed and reduced costs for data transfer.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-126">This assists with processing speed and reduced costs for data transfer.</span></span>

   ![Create a Azure web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

## <a name="add-a-consumer-group-to-your-iot-hub"></a><span data-ttu-id="a6f9a-128">Add a consumer group to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="a6f9a-128">Add a consumer group to your IoT hub</span></span>

<span data-ttu-id="a6f9a-129">Consumer groups are used by applications to pull data from Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-129">Consumer groups are used by applications to pull data from Azure IoT Hub.</span></span> <span data-ttu-id="a6f9a-130">In this lesson, you create a consumer group to be used by the web app to read data from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-130">In this lesson, you create a consumer group to be used by the web app to read data from your IoT hub.</span></span>

<span data-ttu-id="a6f9a-131">To add a consumer group to your IoT hub, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="a6f9a-131">To add a consumer group to your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="a6f9a-132">In the [Azure portal](https://ms.portal.azure.com/), open your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-132">In the [Azure portal](https://ms.portal.azure.com/), open your IoT hub.</span></span>
1. <span data-ttu-id="a6f9a-133">Click **Endpoints** on the left pane, select **Events** on the middle pane, enter a name under **Consumer groups** on the right pane, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-133">Click **Endpoints** on the left pane, select **Events** on the middle pane, enter a name under **Consumer groups** on the right pane, and then click **Save**.</span></span>

   ![Create consumer group in Azure IoT Hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-live-data-visualization-in-web-apps/3_add-consumer-group-iot-hub-azure.png)

## <a name="configure-the-web-app-to-read-data-from-your-iot-hub"></a><span data-ttu-id="a6f9a-135">Configure the web app to read data from your IoT hub</span><span class="sxs-lookup"><span data-stu-id="a6f9a-135">Configure the web app to read data from your IoT hub</span></span>

1. <span data-ttu-id="a6f9a-136">Open the Web app you’ve just provisioned.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-136">Open the Web app you’ve just provisioned.</span></span>
1. <span data-ttu-id="a6f9a-137">Click **Application settings**, and then add the following key/value pairs under **App settings**:</span><span class="sxs-lookup"><span data-stu-id="a6f9a-137">Click **Application settings**, and then add the following key/value pairs under **App settings**:</span></span>

   | <span data-ttu-id="a6f9a-138">Key</span><span class="sxs-lookup"><span data-stu-id="a6f9a-138">Key</span></span>                                   | <span data-ttu-id="a6f9a-139">Value</span><span class="sxs-lookup"><span data-stu-id="a6f9a-139">Value</span></span>                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | <span data-ttu-id="a6f9a-140">Azure.IoT.IoTHub.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="a6f9a-140">Azure.IoT.IoTHub.ConnectionString</span></span>     | <span data-ttu-id="a6f9a-141">Obtained from iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="a6f9a-141">Obtained from iothub-explorer</span></span>                                |
   | <span data-ttu-id="a6f9a-142">Azure.IoT.IoTHub.DeviceId</span><span class="sxs-lookup"><span data-stu-id="a6f9a-142">Azure.IoT.IoTHub.DeviceId</span></span>             | <span data-ttu-id="a6f9a-143">Obtained from iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="a6f9a-143">Obtained from iothub-explorer</span></span>                                |
   | <span data-ttu-id="a6f9a-144">Azure.IoT.IoTHub.ConsumerGroup</span><span class="sxs-lookup"><span data-stu-id="a6f9a-144">Azure.IoT.IoTHub.ConsumerGroup</span></span>        | <span data-ttu-id="a6f9a-145">The name of the consumer group that you add to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="a6f9a-145">The name of the consumer group that you add to your IoT hub</span></span>  |

   ![Add settings to Azure web app with key value pairs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

## <a name="upload-a-web-application-to-be-hosted-by-the-web-app"></a><span data-ttu-id="a6f9a-147">Upload a web application to be hosted by the web app</span><span class="sxs-lookup"><span data-stu-id="a6f9a-147">Upload a web application to be hosted by the web app</span></span>

<span data-ttu-id="a6f9a-148">We made available a web application on GitHub which displays real-time sensor data from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-148">We made available a web application on GitHub which displays real-time sensor data from your IoT hub.</span></span> <span data-ttu-id="a6f9a-149">All you need to do is to configure the web app to work with a Git repository, download the web application from GitHub and upload it to Azure for the web app to host.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-149">All you need to do is to configure the web app to work with a Git repository, download the web application from GitHub and upload it to Azure for the web app to host.</span></span>

1. <span data-ttu-id="a6f9a-150">In the web app, click **Deployment Options** > **Choose Source** > **Local Git Repository**.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-150">In the web app, click **Deployment Options** > **Choose Source** > **Local Git Repository**.</span></span>

   ![Configure your Azure web app deployment to use local git repository](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

1. <span data-ttu-id="a6f9a-152">Click **Setup connection**, create a user name and password that will be used to connect to the Git repository in Azure, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-152">Click **Setup connection**, create a user name and password that will be used to connect to the Git repository in Azure, and then click **OK**.</span></span>

   ![Set user name and password for the git repository in Azure for your web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-live-data-visualization-in-web-apps/6_web-app-set-user-password-git-repo-azure.png)

1. <span data-ttu-id="a6f9a-154">Click **OK** to finish the configuration.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-154">Click **OK** to finish the configuration.</span></span>
1. <span data-ttu-id="a6f9a-155">Click **Overview** and make a note of the value of **Git clone url**.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-155">Click **Overview** and make a note of the value of **Git clone url**.</span></span>

   ![Get the git clone URL of your Azure web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

1. <span data-ttu-id="a6f9a-157">Open a command or terminal window on your local computer.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-157">Open a command or terminal window on your local computer.</span></span>
1. <span data-ttu-id="a6f9a-158">Download the web application from GitHub and upload it Azure for the web app to host.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-158">Download the web application from GitHub and upload it Azure for the web app to host.</span></span> <span data-ttu-id="a6f9a-159">To do this, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="a6f9a-159">To do this, run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!Note]
   > <span data-ttu-id="a6f9a-160">\<Git clone URL\> is the URL of the Git repository found on the **Overview** page of the web app.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-160">\<Git clone URL\> is the URL of the Git repository found on the **Overview** page of the web app.</span></span>

## <a name="open-the-web-app-to-see-real-time-temperature-and-humidity-data-from-your-iot-hub"></a><span data-ttu-id="a6f9a-161">Open the web app to see real-time temperature and humidity data from your IoT hub</span><span class="sxs-lookup"><span data-stu-id="a6f9a-161">Open the web app to see real-time temperature and humidity data from your IoT hub</span></span>

<span data-ttu-id="a6f9a-162">On the **Overview** page of your web app, click the URL to open the web app.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-162">On the **Overview** page of your web app, click the URL to open the web app.</span></span>

![Get the URL of your Azure web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

<span data-ttu-id="a6f9a-164">You should see the real-time temperature and humidity data from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-164">You should see the real-time temperature and humidity data from your IoT hub.</span></span>

![Azure web app page showing real-time temperature and humidity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

## <a name="next-steps"></a><span data-ttu-id="a6f9a-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="a6f9a-166">Next steps</span></span>
<span data-ttu-id="a6f9a-167">You’ve successfully used an Azure web app to visualize real-time sensor data from your Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-167">You’ve successfully used an Azure web app to visualize real-time sensor data from your Azure IoT hub.</span></span>

<span data-ttu-id="a6f9a-168">There is an alternate way to visualize data from Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a6f9a-168">There is an alternate way to visualize data from Azure IoT Hub.</span></span> <span data-ttu-id="a6f9a-169">See [Use Power BI to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="a6f9a-169">See [Use Power BI to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]








