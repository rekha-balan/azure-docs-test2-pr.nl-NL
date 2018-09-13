---
title: Tutorial - Deploy ASA jobs to Azure IoT Edge devices | Microsoft Docs
description: In this tutorial, you deploy Azure Stream Analytics as a module to an Iot Edge device
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 08/10/2018
ms.topic: tutorial
ms.service: iot-edge
services: iot-edge
ms.custom: mvc
ms.openlocfilehash: 66d55c07493a540e36a08d48d6abbdc3d082b9b9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864549"
---
# <a name="tutorial-deploy-azure-stream-analytics-as-an-iot-edge-module-preview"></a><span data-ttu-id="e2f17-103">Tutorial: Deploy Azure Stream Analytics as an IoT Edge module (preview)</span><span class="sxs-lookup"><span data-stu-id="e2f17-103">Tutorial: Deploy Azure Stream Analytics as an IoT Edge module (preview)</span></span>

<span data-ttu-id="e2f17-104">Many IoT solutions use analytics services to gain insight about data as it arrives in the cloud from the IoT devices.</span><span class="sxs-lookup"><span data-stu-id="e2f17-104">Many IoT solutions use analytics services to gain insight about data as it arrives in the cloud from the IoT devices.</span></span> <span data-ttu-id="e2f17-105">With Azure IoT Edge, you can take [Azure Stream Analytics][azure-stream] logic and move it onto the device itself.</span><span class="sxs-lookup"><span data-stu-id="e2f17-105">With Azure IoT Edge, you can take [Azure Stream Analytics][azure-stream] logic and move it onto the device itself.</span></span> <span data-ttu-id="e2f17-106">By processing telemetry streams at the edge, you can reduce the amount of uploaded data and reduce the time it takes to react to actionable insights.</span><span class="sxs-lookup"><span data-stu-id="e2f17-106">By processing telemetry streams at the edge, you can reduce the amount of uploaded data and reduce the time it takes to react to actionable insights.</span></span>

<span data-ttu-id="e2f17-107">Azure IoT Edge and Azure Stream Analytics are integrated so that you can create an Azure Stream Analytics job in the Azure portal and then deploy it as an IoT Edge module with no additional code.</span><span class="sxs-lookup"><span data-stu-id="e2f17-107">Azure IoT Edge and Azure Stream Analytics are integrated so that you can create an Azure Stream Analytics job in the Azure portal and then deploy it as an IoT Edge module with no additional code.</span></span>  

<span data-ttu-id="e2f17-108">Azure Stream Analytics provides a richly structured query syntax for data analysis both in the cloud and on IoT Edge devices.</span><span class="sxs-lookup"><span data-stu-id="e2f17-108">Azure Stream Analytics provides a richly structured query syntax for data analysis both in the cloud and on IoT Edge devices.</span></span> <span data-ttu-id="e2f17-109">For more information about Azure Stream Analytics on IoT Edge, see [Azure Stream Analytics documentation](../stream-analytics/stream-analytics-edge.md).</span><span class="sxs-lookup"><span data-stu-id="e2f17-109">For more information about Azure Stream Analytics on IoT Edge, see [Azure Stream Analytics documentation](../stream-analytics/stream-analytics-edge.md).</span></span>

<span data-ttu-id="e2f17-110">The Stream Analytics module in this tutorial calculates the average temperature over a rolling 30-second window.</span><span class="sxs-lookup"><span data-stu-id="e2f17-110">The Stream Analytics module in this tutorial calculates the average temperature over a rolling 30-second window.</span></span> <span data-ttu-id="e2f17-111">When that average reaches 70, the module sends an alert for the device to take action.</span><span class="sxs-lookup"><span data-stu-id="e2f17-111">When that average reaches 70, the module sends an alert for the device to take action.</span></span> <span data-ttu-id="e2f17-112">In this case, that action is to reset the simulated temperature sensor.</span><span class="sxs-lookup"><span data-stu-id="e2f17-112">In this case, that action is to reset the simulated temperature sensor.</span></span> <span data-ttu-id="e2f17-113">In a production environment, you might use this functionality to shut off a machine or take preventative measures when the temperature reaches dangerous levels.</span><span class="sxs-lookup"><span data-stu-id="e2f17-113">In a production environment, you might use this functionality to shut off a machine or take preventative measures when the temperature reaches dangerous levels.</span></span> 

<span data-ttu-id="e2f17-114">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="e2f17-114">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e2f17-115">Create an Azure Stream Analytics job to process data on the edge.</span><span class="sxs-lookup"><span data-stu-id="e2f17-115">Create an Azure Stream Analytics job to process data on the edge.</span></span>
> * <span data-ttu-id="e2f17-116">Connect the new Azure Stream Analytics job with other IoT Edge modules.</span><span class="sxs-lookup"><span data-stu-id="e2f17-116">Connect the new Azure Stream Analytics job with other IoT Edge modules.</span></span>
> * <span data-ttu-id="e2f17-117">Deploy the Azure Stream Analytics job to an IoT Edge device from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e2f17-117">Deploy the Azure Stream Analytics job to an IoT Edge device from the Azure portal.</span></span>

<span data-ttu-id="e2f17-118"><center>
![Tutorial architecture diagram](./media/tutorial-deploy-stream-analytics/ASATutorialDiagram.png)
</center></span><span class="sxs-lookup"><span data-stu-id="e2f17-118"><center>
![Tutorial architecture diagram](./media/tutorial-deploy-stream-analytics/ASATutorialDiagram.png)
</center></span></span>

>[!NOTE]
><span data-ttu-id="e2f17-119">Azure Stream Analytics modules for IoT Edge are in [public preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="e2f17-119">Azure Stream Analytics modules for IoT Edge are in [public preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="e2f17-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e2f17-120">Prerequisites</span></span>

<span data-ttu-id="e2f17-121">An Azure IoT Edge device:</span><span class="sxs-lookup"><span data-stu-id="e2f17-121">An Azure IoT Edge device:</span></span>

* <span data-ttu-id="e2f17-122">You can use your development machine or a virtual machine as an Edge device by following the steps in the quickstart for [Linux](quickstart-linux.md) or [Windows devices](quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="e2f17-122">You can use your development machine or a virtual machine as an Edge device by following the steps in the quickstart for [Linux](quickstart-linux.md) or [Windows devices](quickstart.md).</span></span>

<span data-ttu-id="e2f17-123">Cloud resources:</span><span class="sxs-lookup"><span data-stu-id="e2f17-123">Cloud resources:</span></span>

* <span data-ttu-id="e2f17-124">A standard-tier [IoT Hub](../iot-hub/iot-hub-create-through-portal.md) in Azure.</span><span class="sxs-lookup"><span data-stu-id="e2f17-124">A standard-tier [IoT Hub](../iot-hub/iot-hub-create-through-portal.md) in Azure.</span></span> 


## <a name="create-an-azure-stream-analytics-job"></a><span data-ttu-id="e2f17-125">Create an Azure Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="e2f17-125">Create an Azure Stream Analytics job</span></span>

<span data-ttu-id="e2f17-126">In this section, you create an Azure Stream Analytics job to take data from your IoT hub, query the sent telemetry data from your device, and then forward the results to an Azure Blob storage container.</span><span class="sxs-lookup"><span data-stu-id="e2f17-126">In this section, you create an Azure Stream Analytics job to take data from your IoT hub, query the sent telemetry data from your device, and then forward the results to an Azure Blob storage container.</span></span> 

### <a name="create-a-storage-account"></a><span data-ttu-id="e2f17-127">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="e2f17-127">Create a storage account</span></span>

<span data-ttu-id="e2f17-128">When you create an Azure Stream Analytics job to run on an IoT Edge device, it needs to be stored in a way that can be called from the device.</span><span class="sxs-lookup"><span data-stu-id="e2f17-128">When you create an Azure Stream Analytics job to run on an IoT Edge device, it needs to be stored in a way that can be called from the device.</span></span> <span data-ttu-id="e2f17-129">You can use an existing Azure storage account, or create a new one now.</span><span class="sxs-lookup"><span data-stu-id="e2f17-129">You can use an existing Azure storage account, or create a new one now.</span></span> 

1. <span data-ttu-id="e2f17-130">In the Azure portal, go to **Create a resource** > **Storage** > **Storage account - blob, file, table, queue**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-130">In the Azure portal, go to **Create a resource** > **Storage** > **Storage account - blob, file, table, queue**.</span></span> 

1. <span data-ttu-id="e2f17-131">Provide the following values to create your storage account:</span><span class="sxs-lookup"><span data-stu-id="e2f17-131">Provide the following values to create your storage account:</span></span>

   | <span data-ttu-id="e2f17-132">Field</span><span class="sxs-lookup"><span data-stu-id="e2f17-132">Field</span></span> | <span data-ttu-id="e2f17-133">Value</span><span class="sxs-lookup"><span data-stu-id="e2f17-133">Value</span></span> |
   | ----- | ----- |
   | <span data-ttu-id="e2f17-134">Name</span><span class="sxs-lookup"><span data-stu-id="e2f17-134">Name</span></span> | <span data-ttu-id="e2f17-135">Provide a unique name for your storage account.</span><span class="sxs-lookup"><span data-stu-id="e2f17-135">Provide a unique name for your storage account.</span></span> | 
   | <span data-ttu-id="e2f17-136">Location</span><span class="sxs-lookup"><span data-stu-id="e2f17-136">Location</span></span> | <span data-ttu-id="e2f17-137">Choose a location close to you.</span><span class="sxs-lookup"><span data-stu-id="e2f17-137">Choose a location close to you.</span></span> |
   | <span data-ttu-id="e2f17-138">Subscription</span><span class="sxs-lookup"><span data-stu-id="e2f17-138">Subscription</span></span> | <span data-ttu-id="e2f17-139">Choose the same subscription as your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e2f17-139">Choose the same subscription as your IoT hub.</span></span> |
   | <span data-ttu-id="e2f17-140">Resource group</span><span class="sxs-lookup"><span data-stu-id="e2f17-140">Resource group</span></span> | <span data-ttu-id="e2f17-141">We recommend that you use the same resource group for all of the test resources that you create during the IoT Edge quickstarts and tutorials.</span><span class="sxs-lookup"><span data-stu-id="e2f17-141">We recommend that you use the same resource group for all of the test resources that you create during the IoT Edge quickstarts and tutorials.</span></span> <span data-ttu-id="e2f17-142">For example, **IoTEdgeResources**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-142">For example, **IoTEdgeResources**.</span></span> |

1. <span data-ttu-id="e2f17-143">Keep the default values for the other fields and select **Create**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-143">Keep the default values for the other fields and select **Create**.</span></span> 

### <a name="create-a-new-job"></a><span data-ttu-id="e2f17-144">Create a new job</span><span class="sxs-lookup"><span data-stu-id="e2f17-144">Create a new job</span></span>

1. <span data-ttu-id="e2f17-145">In the Azure portal, go to **Create a resource** > **Internet of Things** > **Stream Analytics Job**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-145">In the Azure portal, go to **Create a resource** > **Internet of Things** > **Stream Analytics Job**.</span></span>

1. <span data-ttu-id="e2f17-146">Provide the following values to create your job:</span><span class="sxs-lookup"><span data-stu-id="e2f17-146">Provide the following values to create your job:</span></span>

   | <span data-ttu-id="e2f17-147">Field</span><span class="sxs-lookup"><span data-stu-id="e2f17-147">Field</span></span> | <span data-ttu-id="e2f17-148">Value</span><span class="sxs-lookup"><span data-stu-id="e2f17-148">Value</span></span> |
   | ----- | ----- |
   | <span data-ttu-id="e2f17-149">Job name</span><span class="sxs-lookup"><span data-stu-id="e2f17-149">Job name</span></span> | <span data-ttu-id="e2f17-150">Provide a name for your job.</span><span class="sxs-lookup"><span data-stu-id="e2f17-150">Provide a name for your job.</span></span> <span data-ttu-id="e2f17-151">For example, **IoTEdgeJob**</span><span class="sxs-lookup"><span data-stu-id="e2f17-151">For example, **IoTEdgeJob**</span></span> | 
   | <span data-ttu-id="e2f17-152">Subscription</span><span class="sxs-lookup"><span data-stu-id="e2f17-152">Subscription</span></span> | <span data-ttu-id="e2f17-153">Choose the same subscription as your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e2f17-153">Choose the same subscription as your IoT hub.</span></span> |
   | <span data-ttu-id="e2f17-154">Resource group</span><span class="sxs-lookup"><span data-stu-id="e2f17-154">Resource group</span></span> | <span data-ttu-id="e2f17-155">We recommend that you use the same resource group for all of the test resources that you create during the IoT Edge quickstarts and tutorials.</span><span class="sxs-lookup"><span data-stu-id="e2f17-155">We recommend that you use the same resource group for all of the test resources that you create during the IoT Edge quickstarts and tutorials.</span></span> <span data-ttu-id="e2f17-156">For example, **IoTEdgeResources**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-156">For example, **IoTEdgeResources**.</span></span> |
   | <span data-ttu-id="e2f17-157">Location</span><span class="sxs-lookup"><span data-stu-id="e2f17-157">Location</span></span> | <span data-ttu-id="e2f17-158">Choose a location close to you.</span><span class="sxs-lookup"><span data-stu-id="e2f17-158">Choose a location close to you.</span></span> | 
   | <span data-ttu-id="e2f17-159">Hosting environment</span><span class="sxs-lookup"><span data-stu-id="e2f17-159">Hosting environment</span></span> | <span data-ttu-id="e2f17-160">Select **Edge**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-160">Select **Edge**.</span></span> |
 
1. <span data-ttu-id="e2f17-161">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-161">Select **Create**.</span></span>

### <a name="configure-your-job"></a><span data-ttu-id="e2f17-162">Configure your job</span><span class="sxs-lookup"><span data-stu-id="e2f17-162">Configure your job</span></span>

<span data-ttu-id="e2f17-163">Once your Stream Analytics job is created in the Azure portal, you can configure it with an input, an output, and a query to run on the data that passes through.</span><span class="sxs-lookup"><span data-stu-id="e2f17-163">Once your Stream Analytics job is created in the Azure portal, you can configure it with an input, an output, and a query to run on the data that passes through.</span></span> 

<span data-ttu-id="e2f17-164">Using the three elements of input, output, and query, this section creates a job that receives temperature data from the IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="e2f17-164">Using the three elements of input, output, and query, this section creates a job that receives temperature data from the IoT Edge device.</span></span> <span data-ttu-id="e2f17-165">It analyzes that data in a rolling 30-second window.</span><span class="sxs-lookup"><span data-stu-id="e2f17-165">It analyzes that data in a rolling 30-second window.</span></span> <span data-ttu-id="e2f17-166">If the average temperature in that window goes over 70 degrees, then an alert is sent to the IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="e2f17-166">If the average temperature in that window goes over 70 degrees, then an alert is sent to the IoT Edge device.</span></span> <span data-ttu-id="e2f17-167">You'll specify exactly where the data comes from and goes in the next section when you deploy the job.</span><span class="sxs-lookup"><span data-stu-id="e2f17-167">You'll specify exactly where the data comes from and goes in the next section when you deploy the job.</span></span>  

1. <span data-ttu-id="e2f17-168">Navigate to your Stream Analytics job in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e2f17-168">Navigate to your Stream Analytics job in the Azure portal.</span></span> 

1. <span data-ttu-id="e2f17-169">Under **Job Topology**, select **Inputs** then **Add stream input**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-169">Under **Job Topology**, select **Inputs** then **Add stream input**.</span></span>

   ![Azure Stream Analytics input](./media/tutorial-deploy-stream-analytics/asa_input.png)

1. <span data-ttu-id="e2f17-171">Choose **Edge Hub** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="e2f17-171">Choose **Edge Hub** from the drop-down list.</span></span>

1. <span data-ttu-id="e2f17-172">In the **New input** pane, enter **temperature** as the input alias.</span><span class="sxs-lookup"><span data-stu-id="e2f17-172">In the **New input** pane, enter **temperature** as the input alias.</span></span> 

1. <span data-ttu-id="e2f17-173">Keep the default values for the other fields, and select **Save**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-173">Keep the default values for the other fields, and select **Save**.</span></span>

1. <span data-ttu-id="e2f17-174">Under **Job Topology**, open **Outputs** then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-174">Under **Job Topology**, open **Outputs** then select **Add**.</span></span>

   ![Azure Stream Analytics output](./media/tutorial-deploy-stream-analytics/asa_output.png)

1. <span data-ttu-id="e2f17-176">Choose **Edge Hub** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="e2f17-176">Choose **Edge Hub** from the drop-down list.</span></span>

1. <span data-ttu-id="e2f17-177">In the **New output** pane, enter **alert** as the output alias.</span><span class="sxs-lookup"><span data-stu-id="e2f17-177">In the **New output** pane, enter **alert** as the output alias.</span></span> 

1. <span data-ttu-id="e2f17-178">Keep the default values for the other fields, and select **Save**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-178">Keep the default values for the other fields, and select **Save**.</span></span>

1. <span data-ttu-id="e2f17-179">Under **Job Topology**, select **Query**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-179">Under **Job Topology**, select **Query**.</span></span>

1. <span data-ttu-id="e2f17-180">Replace the default text with the following query.</span><span class="sxs-lookup"><span data-stu-id="e2f17-180">Replace the default text with the following query.</span></span> <span data-ttu-id="e2f17-181">The SQL code sends a reset command to the alert output if the average machine temperature in a 30-second window reaches 70 degrees.</span><span class="sxs-lookup"><span data-stu-id="e2f17-181">The SQL code sends a reset command to the alert output if the average machine temperature in a 30-second window reaches 70 degrees.</span></span> <span data-ttu-id="e2f17-182">The reset command has been pre-programmed into the sensor as an action that can be taken.</span><span class="sxs-lookup"><span data-stu-id="e2f17-182">The reset command has been pre-programmed into the sensor as an action that can be taken.</span></span> 

    ```sql
    SELECT  
        'reset' AS command 
    INTO 
       alert 
    FROM 
       temperature TIMESTAMP BY timeCreated 
    GROUP BY TumblingWindow(second,30) 
    HAVING Avg(machine.temperature) > 70
    ```

1. <span data-ttu-id="e2f17-183">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-183">Select **Save**.</span></span>

### <a name="configure-iot-edge-settings"></a><span data-ttu-id="e2f17-184">Configure IoT Edge settings</span><span class="sxs-lookup"><span data-stu-id="e2f17-184">Configure IoT Edge settings</span></span>

<span data-ttu-id="e2f17-185">To prepare your Stream Analytics job to be deployed on an IoT Edge device, you need to associate the job with a container in a storage account.</span><span class="sxs-lookup"><span data-stu-id="e2f17-185">To prepare your Stream Analytics job to be deployed on an IoT Edge device, you need to associate the job with a container in a storage account.</span></span> <span data-ttu-id="e2f17-186">When you go to deploy your job, the job definition is exported to the storage container.</span><span class="sxs-lookup"><span data-stu-id="e2f17-186">When you go to deploy your job, the job definition is exported to the storage container.</span></span> 

1. <span data-ttu-id="e2f17-187">Under **Configure**, select **IoT Edge settings**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-187">Under **Configure**, select **IoT Edge settings**.</span></span>

1. <span data-ttu-id="e2f17-188">Select your **Storage account** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="e2f17-188">Select your **Storage account** from the drop-down menu.</span></span>

1. <span data-ttu-id="e2f17-189">For the **Container** field, select **Create new** and provide a name for the storage container.</span><span class="sxs-lookup"><span data-stu-id="e2f17-189">For the **Container** field, select **Create new** and provide a name for the storage container.</span></span> 

1. <span data-ttu-id="e2f17-190">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-190">Select **Save**.</span></span> 

## <a name="deploy-the-job"></a><span data-ttu-id="e2f17-191">Deploy the job</span><span class="sxs-lookup"><span data-stu-id="e2f17-191">Deploy the job</span></span>

<span data-ttu-id="e2f17-192">You are now ready to deploy the Azure Stream Analytics job on your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="e2f17-192">You are now ready to deploy the Azure Stream Analytics job on your IoT Edge device.</span></span> 

<span data-ttu-id="e2f17-193">In this section, you use the **Set Modules** wizard in the Azure portal to create a *deployment manifest*.</span><span class="sxs-lookup"><span data-stu-id="e2f17-193">In this section, you use the **Set Modules** wizard in the Azure portal to create a *deployment manifest*.</span></span> <span data-ttu-id="e2f17-194">A deployment manifest is a JSON file that describes all the modules that will be deployed to a device, the container registries that store the module images, how the modules should be managed, and how the modules can communicate with each other.</span><span class="sxs-lookup"><span data-stu-id="e2f17-194">A deployment manifest is a JSON file that describes all the modules that will be deployed to a device, the container registries that store the module images, how the modules should be managed, and how the modules can communicate with each other.</span></span> <span data-ttu-id="e2f17-195">Your IoT Edge device retrieves its deployment manifest from IoT Hub, then uses the information in it to deploy and configure all of its assigned modules.</span><span class="sxs-lookup"><span data-stu-id="e2f17-195">Your IoT Edge device retrieves its deployment manifest from IoT Hub, then uses the information in it to deploy and configure all of its assigned modules.</span></span> 

<span data-ttu-id="e2f17-196">For this tutorial, you deploy two modules.</span><span class="sxs-lookup"><span data-stu-id="e2f17-196">For this tutorial, you deploy two modules.</span></span> <span data-ttu-id="e2f17-197">The first is **tempSensor**, which is a module that simulates a temperature and humidity sensor.</span><span class="sxs-lookup"><span data-stu-id="e2f17-197">The first is **tempSensor**, which is a module that simulates a temperature and humidity sensor.</span></span> <span data-ttu-id="e2f17-198">The second is your Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="e2f17-198">The second is your Stream Analytics job.</span></span> <span data-ttu-id="e2f17-199">The sensor module provides the stream of data that your job query will analyze.</span><span class="sxs-lookup"><span data-stu-id="e2f17-199">The sensor module provides the stream of data that your job query will analyze.</span></span> 

1. <span data-ttu-id="e2f17-200">In the Azure portal, in your IoT hub, go to **IoT Edge**, and then open the details page for your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="e2f17-200">In the Azure portal, in your IoT hub, go to **IoT Edge**, and then open the details page for your IoT Edge device.</span></span>

1. <span data-ttu-id="e2f17-201">Select **Set modules**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-201">Select **Set modules**.</span></span>  

1. <span data-ttu-id="e2f17-202">If you previously deployed the tempSensor module on this device, it might autopopulate.</span><span class="sxs-lookup"><span data-stu-id="e2f17-202">If you previously deployed the tempSensor module on this device, it might autopopulate.</span></span> <span data-ttu-id="e2f17-203">If it does not, add the module with the following steps:</span><span class="sxs-lookup"><span data-stu-id="e2f17-203">If it does not, add the module with the following steps:</span></span>

   1. <span data-ttu-id="e2f17-204">Click **Add** and select **IoT Edge Module**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-204">Click **Add** and select **IoT Edge Module**.</span></span>
   1. <span data-ttu-id="e2f17-205">For the name, type **tempSensor**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-205">For the name, type **tempSensor**.</span></span>
   1. <span data-ttu-id="e2f17-206">For the image URI, enter **mcr.microsoft.com/azureiotedge-simulated-temperature-sensor:1.0**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-206">For the image URI, enter **mcr.microsoft.com/azureiotedge-simulated-temperature-sensor:1.0**.</span></span> 
   1. <span data-ttu-id="e2f17-207">Leave the other settings unchanged and select **Save**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-207">Leave the other settings unchanged and select **Save**.</span></span>

1. <span data-ttu-id="e2f17-208">Add your Azure Stream Analytics Edge job with the following steps:</span><span class="sxs-lookup"><span data-stu-id="e2f17-208">Add your Azure Stream Analytics Edge job with the following steps:</span></span>

   1. <span data-ttu-id="e2f17-209">Click **Add** and select **Azure Stream Analytics Module**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-209">Click **Add** and select **Azure Stream Analytics Module**.</span></span>
   1. <span data-ttu-id="e2f17-210">Select your subscription and the Azure Stream Analytics Edge job that you created.</span><span class="sxs-lookup"><span data-stu-id="e2f17-210">Select your subscription and the Azure Stream Analytics Edge job that you created.</span></span> 
   1. <span data-ttu-id="e2f17-211">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-211">Select **Save**.</span></span>

1. <span data-ttu-id="e2f17-212">Once your Stream Analytics job is published to the storage container that you created, click on the module name to see how a Stream Analytics module is structured.</span><span class="sxs-lookup"><span data-stu-id="e2f17-212">Once your Stream Analytics job is published to the storage container that you created, click on the module name to see how a Stream Analytics module is structured.</span></span> 

   <span data-ttu-id="e2f17-213">The image URI points to a standard Azure Stream Analytics image.</span><span class="sxs-lookup"><span data-stu-id="e2f17-213">The image URI points to a standard Azure Stream Analytics image.</span></span> <span data-ttu-id="e2f17-214">This is the same image used for every job that gets deployed to an IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="e2f17-214">This is the same image used for every job that gets deployed to an IoT Edge device.</span></span> 

   <span data-ttu-id="e2f17-215">The module twin is configured with a desired property called **ASAJobInfo**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-215">The module twin is configured with a desired property called **ASAJobInfo**.</span></span> <span data-ttu-id="e2f17-216">The value of that property points to the job definition in your storage container.</span><span class="sxs-lookup"><span data-stu-id="e2f17-216">The value of that property points to the job definition in your storage container.</span></span> <span data-ttu-id="e2f17-217">This property is how the Stream Analytics image is configured with your specific job information.</span><span class="sxs-lookup"><span data-stu-id="e2f17-217">This property is how the Stream Analytics image is configured with your specific job information.</span></span> 

1. <span data-ttu-id="e2f17-218">Close the module page.</span><span class="sxs-lookup"><span data-stu-id="e2f17-218">Close the module page.</span></span>

1. <span data-ttu-id="e2f17-219">Make a note of the name of your Stream Analytics module because you'll need it in the next step, then select **Next** to continue.</span><span class="sxs-lookup"><span data-stu-id="e2f17-219">Make a note of the name of your Stream Analytics module because you'll need it in the next step, then select **Next** to continue.</span></span>

1. <span data-ttu-id="e2f17-220">Replace the default value in **Routes** with the following code.</span><span class="sxs-lookup"><span data-stu-id="e2f17-220">Replace the default value in **Routes** with the following code.</span></span> <span data-ttu-id="e2f17-221">Update all three instances of _{moduleName}_ with the name of your Azure Stream Analytics module.</span><span class="sxs-lookup"><span data-stu-id="e2f17-221">Update all three instances of _{moduleName}_ with the name of your Azure Stream Analytics module.</span></span> 

    ```json
    {
        "routes": {
            "telemetryToCloud": "FROM /messages/modules/tempSensor/* INTO $upstream",
            "alertsToCloud": "FROM /messages/modules/{moduleName}/* INTO $upstream",
            "alertsToReset": "FROM /messages/modules/{moduleName}/* INTO BrokeredEndpoint(\"/modules/tempSensor/inputs/control\")",
            "telemetryToAsa": "FROM /messages/modules/tempSensor/* INTO BrokeredEndpoint(\"/modules/{moduleName}/inputs/temperature\")"
        }
    }
    ```

   <span data-ttu-id="e2f17-222">The routes that you declare here define the flow of data through the IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="e2f17-222">The routes that you declare here define the flow of data through the IoT Edge device.</span></span> <span data-ttu-id="e2f17-223">The telemetry data from tempSensor are sent to IoT Hub and to the **temperature** input that was configured in the Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="e2f17-223">The telemetry data from tempSensor are sent to IoT Hub and to the **temperature** input that was configured in the Stream Analytics job.</span></span> <span data-ttu-id="e2f17-224">The **alert** output messages are sent to IoT Hub and to the tempSensor module to trigger the reset command.</span><span class="sxs-lookup"><span data-stu-id="e2f17-224">The **alert** output messages are sent to IoT Hub and to the tempSensor module to trigger the reset command.</span></span> 

1. <span data-ttu-id="e2f17-225">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-225">Select **Next**.</span></span>

1. <span data-ttu-id="e2f17-226">In the **Review Deployment** step, select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-226">In the **Review Deployment** step, select **Submit**.</span></span>

1. <span data-ttu-id="e2f17-227">Return to the device details page, and then select **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="e2f17-227">Return to the device details page, and then select **Refresh**.</span></span>  

    <span data-ttu-id="e2f17-228">You should see the new Stream Analytics module running, along with the IoT Edge agent module and the IoT Edge hub.</span><span class="sxs-lookup"><span data-stu-id="e2f17-228">You should see the new Stream Analytics module running, along with the IoT Edge agent module and the IoT Edge hub.</span></span>

    ![Module output][7]

## <a name="view-data"></a><span data-ttu-id="e2f17-230">View data</span><span class="sxs-lookup"><span data-stu-id="e2f17-230">View data</span></span>

<span data-ttu-id="e2f17-231">Now you can go to your IoT Edge device to check out the interaction between the Azure Stream Analytics module and the tempSensor module.</span><span class="sxs-lookup"><span data-stu-id="e2f17-231">Now you can go to your IoT Edge device to check out the interaction between the Azure Stream Analytics module and the tempSensor module.</span></span>

1. <span data-ttu-id="e2f17-232">Check that all the modules are running in Docker:</span><span class="sxs-lookup"><span data-stu-id="e2f17-232">Check that all the modules are running in Docker:</span></span>

   ```cmd/sh
   iotedge list  
   ```
<!--
   ![Docker output][8]
-->
1. <span data-ttu-id="e2f17-233">View all system logs and metrics data.</span><span class="sxs-lookup"><span data-stu-id="e2f17-233">View all system logs and metrics data.</span></span> <span data-ttu-id="e2f17-234">Use the Stream Analytics module name:</span><span class="sxs-lookup"><span data-stu-id="e2f17-234">Use the Stream Analytics module name:</span></span>

   ```cmd/sh
   iotedge logs -f {moduleName}  
   ```

<span data-ttu-id="e2f17-235">You should be able to watch the machine's temperature gradually rise until it reaches 70 degrees for 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="e2f17-235">You should be able to watch the machine's temperature gradually rise until it reaches 70 degrees for 30 seconds.</span></span> <span data-ttu-id="e2f17-236">Then the Stream Analytics module triggers a reset, and the machine temperature drops back to 21.</span><span class="sxs-lookup"><span data-stu-id="e2f17-236">Then the Stream Analytics module triggers a reset, and the machine temperature drops back to 21.</span></span> 

   ![Docker log][9]

## <a name="clean-up-resources"></a><span data-ttu-id="e2f17-238">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="e2f17-238">Clean up resources</span></span> 

<span data-ttu-id="e2f17-239">If you plan to continue to the next recommended article, you can keep the resources and configurations that you created and reuse them.</span><span class="sxs-lookup"><span data-stu-id="e2f17-239">If you plan to continue to the next recommended article, you can keep the resources and configurations that you created and reuse them.</span></span> <span data-ttu-id="e2f17-240">You can also keep using the same IoT Edge device as a test device.</span><span class="sxs-lookup"><span data-stu-id="e2f17-240">You can also keep using the same IoT Edge device as a test device.</span></span> 

<span data-ttu-id="e2f17-241">Otherwise, you can delete the local configurations and the Azure resources that you created in this article to avoid charges.</span><span class="sxs-lookup"><span data-stu-id="e2f17-241">Otherwise, you can delete the local configurations and the Azure resources that you created in this article to avoid charges.</span></span> 
 
[!INCLUDE [iot-edge-clean-up-cloud-resources](../../includes/iot-edge-clean-up-cloud-resources.md)]

[!INCLUDE [iot-edge-clean-up-local-resources](../../includes/iot-edge-clean-up-local-resources.md)]


## <a name="next-steps"></a><span data-ttu-id="e2f17-242">Next steps</span><span class="sxs-lookup"><span data-stu-id="e2f17-242">Next steps</span></span>

<span data-ttu-id="e2f17-243">In this tutorial, you configured an Azure Streaming Analytics job to analyze data from your IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="e2f17-243">In this tutorial, you configured an Azure Streaming Analytics job to analyze data from your IoT Edge device.</span></span> <span data-ttu-id="e2f17-244">You then loaded this Azure Stream Analytics module on your IoT Edge device to process and react to temperature increase locally, as well as sending the aggregated data stream to the cloud.</span><span class="sxs-lookup"><span data-stu-id="e2f17-244">You then loaded this Azure Stream Analytics module on your IoT Edge device to process and react to temperature increase locally, as well as sending the aggregated data stream to the cloud.</span></span> <span data-ttu-id="e2f17-245">To see how Azure IoT Edge can create more solutions for your business, continue on to the other tutorials.</span><span class="sxs-lookup"><span data-stu-id="e2f17-245">To see how Azure IoT Edge can create more solutions for your business, continue on to the other tutorials.</span></span>

> [!div class="nextstepaction"] 
> <span data-ttu-id="e2f17-246">[Deploy an Azure Machine Learning model as a module][lnk-ml-tutorial]</span><span class="sxs-lookup"><span data-stu-id="e2f17-246">[Deploy an Azure Machine Learning model as a module][lnk-ml-tutorial]</span></span>

<!-- Images. -->
[4]: ./media/tutorial-deploy-stream-analytics/add_device.png
[5]: ./media/tutorial-deploy-stream-analytics/asa_job.png
[6]: ./media/tutorial-deploy-stream-analytics/set_module.png
[7]: ./media/tutorial-deploy-stream-analytics/module_output2.png
[8]: ./media/tutorial-deploy-stream-analytics/docker_output.png
[9]: ./media/tutorial-deploy-stream-analytics/docker_log.png
[10]: ./media/tutorial-deploy-stream-analytics/storage_settings.png
[11]: ./media/tutorial-deploy-stream-analytics/temp_module.png


<!-- Links -->
[lnk-what-is-iot-edge]: what-is-iot-edge.md
[lnk-module-dev]: module-development.md
[iot-hub-get-started-create-hub]: ../../includes/iot-hub-get-started-create-hub.md
[azure-iot]: https://docs.microsoft.com/azure/iot-hub/
[azure-storage]: https://docs.microsoft.com/azure/storage/
[azure-stream]: https://docs.microsoft.com/azure/stream-analytics/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-quickstart-win]: quickstart.md
[lnk-quickstart-lin]: quickstart-linux.md
[lnk-module-tutorial]: tutorial-csharp-module.md
[lnk-ml-tutorial]: tutorial-deploy-machine-learning.md

