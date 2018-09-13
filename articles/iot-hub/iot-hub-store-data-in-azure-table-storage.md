---
title: Save your IoT hub messages to Azure data storage | Microsoft Docs
description: Use IoT Hub message routing to save your IoT hub messages to your Azure blob storage. The IoT hub messages contain information, such as sensor data, that is sent from your IoT device.
author: rangv
manager: ''
keywords: iot data storage, iot sensor data storage
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.tgt_pltfrm: arduino
ms.date: 04/11/2018
ms.author: rangv
ms.openlocfilehash: 84355453a5cb8d8f42abdcbde5432651c9c035b0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44829101"
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-to-your-azure-blob-storage"></a><span data-ttu-id="a3982-105">Save IoT hub messages that contain sensor data to your Azure blob storage</span><span class="sxs-lookup"><span data-stu-id="a3982-105">Save IoT hub messages that contain sensor data to your Azure blob storage</span></span>

![End-to-end diagram](./media/iot-hub-store-data-in-azure-table-storage/1_route-to-storage.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="a3982-107">What you learn</span><span class="sxs-lookup"><span data-stu-id="a3982-107">What you learn</span></span>

<span data-ttu-id="a3982-108">You learn how to create an Azure storage account and an Azure function app to store IoT hub messages in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="a3982-108">You learn how to create an Azure storage account and an Azure function app to store IoT hub messages in Azure Blob storage.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="a3982-109">What you do</span><span class="sxs-lookup"><span data-stu-id="a3982-109">What you do</span></span>

- <span data-ttu-id="a3982-110">Create an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="a3982-110">Create an Azure storage account.</span></span>
- <span data-ttu-id="a3982-111">Set up your IoT hub to route messages to storage.</span><span class="sxs-lookup"><span data-stu-id="a3982-111">Set up your IoT hub to route messages to storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a3982-112">What you need</span><span class="sxs-lookup"><span data-stu-id="a3982-112">What you need</span></span>

- <span data-ttu-id="a3982-113">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md) to cover the following requirements:</span><span class="sxs-lookup"><span data-stu-id="a3982-113">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md) to cover the following requirements:</span></span>
  - <span data-ttu-id="a3982-114">An active Azure subscription</span><span class="sxs-lookup"><span data-stu-id="a3982-114">An active Azure subscription</span></span>
  - <span data-ttu-id="a3982-115">An IoT hub under your subscription</span><span class="sxs-lookup"><span data-stu-id="a3982-115">An IoT hub under your subscription</span></span> 
  - <span data-ttu-id="a3982-116">A running application that sends messages to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="a3982-116">A running application that sends messages to your IoT hub</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="a3982-117">Create an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="a3982-117">Create an Azure storage account</span></span>

1. <span data-ttu-id="a3982-118">In the [Azure portal](https://portal.azure.com/), click **Create a resource** > **Storage** > **Storage account**.</span><span class="sxs-lookup"><span data-stu-id="a3982-118">In the [Azure portal](https://portal.azure.com/), click **Create a resource** > **Storage** > **Storage account**.</span></span>

2. <span data-ttu-id="a3982-119">Enter the necessary information for the storage account:</span><span class="sxs-lookup"><span data-stu-id="a3982-119">Enter the necessary information for the storage account:</span></span>

   ![Create a storage account in the Azure portal](./media/iot-hub-store-data-in-azure-table-storage/1_azure-portal-create-storage-account.png)

   * <span data-ttu-id="a3982-121">**Name**: The name of the storage account.</span><span class="sxs-lookup"><span data-stu-id="a3982-121">**Name**: The name of the storage account.</span></span> <span data-ttu-id="a3982-122">The name must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="a3982-122">The name must be globally unique.</span></span>

   * <span data-ttu-id="a3982-123">**Account Kind**: Choose `Storage (general purpose v1)`.</span><span class="sxs-lookup"><span data-stu-id="a3982-123">**Account Kind**: Choose `Storage (general purpose v1)`.</span></span>

   * <span data-ttu-id="a3982-124">**Location**: Choose the same location that your IoT hub uses.</span><span class="sxs-lookup"><span data-stu-id="a3982-124">**Location**: Choose the same location that your IoT hub uses.</span></span>

   * <span data-ttu-id="a3982-125">**Replication**: Choose `Locally-redundant storage (LRS)`.</span><span class="sxs-lookup"><span data-stu-id="a3982-125">**Replication**: Choose `Locally-redundant storage (LRS)`.</span></span>

   * <span data-ttu-id="a3982-126">**Performance**: Choose `Standard`.</span><span class="sxs-lookup"><span data-stu-id="a3982-126">**Performance**: Choose `Standard`.</span></span>

   * <span data-ttu-id="a3982-127">**Secure transfer required**: Choose `Disabled`.</span><span class="sxs-lookup"><span data-stu-id="a3982-127">**Secure transfer required**: Choose `Disabled`.</span></span>

   * <span data-ttu-id="a3982-128">**Subscription**: Select your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a3982-128">**Subscription**: Select your Azure subscription.</span></span>

   * <span data-ttu-id="a3982-129">**Resource group**: Use the same resource group that your IoT hub uses.</span><span class="sxs-lookup"><span data-stu-id="a3982-129">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="a3982-130">**Pin to dashboard**: Select this option for easy access to your IoT hub from the dashboard.</span><span class="sxs-lookup"><span data-stu-id="a3982-130">**Pin to dashboard**: Select this option for easy access to your IoT hub from the dashboard.</span></span>

3. <span data-ttu-id="a3982-131">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a3982-131">Click **Create**.</span></span>

## <a name="prepare-your-iot-hub-to-route-messages-to-storage"></a><span data-ttu-id="a3982-132">Prepare your IoT hub to route messages to storage</span><span class="sxs-lookup"><span data-stu-id="a3982-132">Prepare your IoT hub to route messages to storage</span></span>

<span data-ttu-id="a3982-133">IoT Hub natively supports routing messages to Azure storage as blobs.</span><span class="sxs-lookup"><span data-stu-id="a3982-133">IoT Hub natively supports routing messages to Azure storage as blobs.</span></span> <span data-ttu-id="a3982-134">To know more about the Azure IoT Hub custom endpoints, you can refer to [List of built-in IoT Hub endpoints](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-endpoints#custom-endpoints).</span><span class="sxs-lookup"><span data-stu-id="a3982-134">To know more about the Azure IoT Hub custom endpoints, you can refer to [List of built-in IoT Hub endpoints](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-endpoints#custom-endpoints).</span></span>

### <a name="add-storage-as-a-custom-endpoint"></a><span data-ttu-id="a3982-135">Add storage as a custom endpoint</span><span class="sxs-lookup"><span data-stu-id="a3982-135">Add storage as a custom endpoint</span></span>

1. <span data-ttu-id="a3982-136">Navigate to your IoT hub in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a3982-136">Navigate to your IoT hub in the Azure portal.</span></span> 

2. <span data-ttu-id="a3982-137">Click **Endpoints** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="a3982-137">Click **Endpoints** > **Add**.</span></span> 

3. <span data-ttu-id="a3982-138">Name the endpoint and select **Azure Storage Container** as the endpoint type.</span><span class="sxs-lookup"><span data-stu-id="a3982-138">Name the endpoint and select **Azure Storage Container** as the endpoint type.</span></span> 

4. <span data-ttu-id="a3982-139">Use the picker to select the storage account you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="a3982-139">Use the picker to select the storage account you created in the previous section.</span></span> <span data-ttu-id="a3982-140">Create a storage container and select it, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="a3982-140">Create a storage container and select it, then click **OK**.</span></span>

   ![Create a custom endpoint in IoT Hub](./media/iot-hub-store-data-in-azure-table-storage/2_custom-storage-endpoint.png)

### <a name="add-a-route-to-route-data-to-storage"></a><span data-ttu-id="a3982-142">Add a route to route data to storage</span><span class="sxs-lookup"><span data-stu-id="a3982-142">Add a route to route data to storage</span></span>

1. <span data-ttu-id="a3982-143">Click **Routes** > **Add** and enter a name for the route.</span><span class="sxs-lookup"><span data-stu-id="a3982-143">Click **Routes** > **Add** and enter a name for the route.</span></span> 

2. <span data-ttu-id="a3982-144">Select **Device Messages** as the data source, and select the storage endpoint you just created as the endpoint in the route.</span><span class="sxs-lookup"><span data-stu-id="a3982-144">Select **Device Messages** as the data source, and select the storage endpoint you just created as the endpoint in the route.</span></span> 

3. <span data-ttu-id="a3982-145">Enter `true` as the query string, then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a3982-145">Enter `true` as the query string, then click **Save**.</span></span>

   ![Create a route in IoT Hub](./media/iot-hub-store-data-in-azure-table-storage/3_create-route.png)
  
### <a name="add-a-route-for-hot-path-telemetry-optional"></a><span data-ttu-id="a3982-147">Add a route for hot path telemetry (optional)</span><span class="sxs-lookup"><span data-stu-id="a3982-147">Add a route for hot path telemetry (optional)</span></span>

<span data-ttu-id="a3982-148">By default, IoT Hub routes all messages which do not match any other routes to the built-in endpoint.</span><span class="sxs-lookup"><span data-stu-id="a3982-148">By default, IoT Hub routes all messages which do not match any other routes to the built-in endpoint.</span></span> <span data-ttu-id="a3982-149">Since all telemetry messages now match the rule which routes the messages to storage, you need to add another route for messages to be written to the built-in endpoint.</span><span class="sxs-lookup"><span data-stu-id="a3982-149">Since all telemetry messages now match the rule which routes the messages to storage, you need to add another route for messages to be written to the built-in endpoint.</span></span> <span data-ttu-id="a3982-150">There is no additional charge to route messages to multiple endpoints.</span><span class="sxs-lookup"><span data-stu-id="a3982-150">There is no additional charge to route messages to multiple endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="a3982-151">You can skip this step if you are not doing additional processing on your telemetry messages.</span><span class="sxs-lookup"><span data-stu-id="a3982-151">You can skip this step if you are not doing additional processing on your telemetry messages.</span></span>

1. <span data-ttu-id="a3982-152">Click **Add** from the Routes pane and enter a name for the route.</span><span class="sxs-lookup"><span data-stu-id="a3982-152">Click **Add** from the Routes pane and enter a name for the route.</span></span> 

2. <span data-ttu-id="a3982-153">Select **Device Messages** as the data source and **events** as the endpoint.</span><span class="sxs-lookup"><span data-stu-id="a3982-153">Select **Device Messages** as the data source and **events** as the endpoint.</span></span> 

3. <span data-ttu-id="a3982-154">Enter `true` as the query string, then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a3982-154">Enter `true` as the query string, then click **Save**.</span></span>

  ![Create a hot-path route in IoT Hub](./media/iot-hub-store-data-in-azure-table-storage/4_hot-path-route.png)

## <a name="verify-your-message-in-your-storage-container"></a><span data-ttu-id="a3982-156">Verify your message in your storage container</span><span class="sxs-lookup"><span data-stu-id="a3982-156">Verify your message in your storage container</span></span>

1. <span data-ttu-id="a3982-157">Run the sample application on your device to send messages to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="a3982-157">Run the sample application on your device to send messages to your IoT hub.</span></span>

2. <span data-ttu-id="a3982-158">[Download and install Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="a3982-158">[Download and install Azure Storage Explorer](http://storageexplorer.com/).</span></span>

3. <span data-ttu-id="a3982-159">Open Storage Explorer, click **Add an Azure Account** > **Sign in**, and then sign in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="a3982-159">Open Storage Explorer, click **Add an Azure Account** > **Sign in**, and then sign in to your Azure account.</span></span>

4. <span data-ttu-id="a3982-160">Click your Azure subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span><span class="sxs-lookup"><span data-stu-id="a3982-160">Click your Azure subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>

   <span data-ttu-id="a3982-161">You should see messages sent from your device to your IoT hub logged in the blob container.</span><span class="sxs-lookup"><span data-stu-id="a3982-161">You should see messages sent from your device to your IoT hub logged in the blob container.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="a3982-162">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="a3982-162">Clean up resources</span></span> 

<span data-ttu-id="a3982-163">In this tutorial, you added a storage account, and then added routing for messages from the IoT Hub to be written to the storage account.</span><span class="sxs-lookup"><span data-stu-id="a3982-163">In this tutorial, you added a storage account, and then added routing for messages from the IoT Hub to be written to the storage account.</span></span> <span data-ttu-id="a3982-164">To clean up the resources you created, you remove the routing information and then delete the storage account.</span><span class="sxs-lookup"><span data-stu-id="a3982-164">To clean up the resources you created, you remove the routing information and then delete the storage account.</span></span> 

1. <span data-ttu-id="a3982-165">Log into the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a3982-165">Log into the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="a3982-166">Click **Resource groups** and select the resource group you used.</span><span class="sxs-lookup"><span data-stu-id="a3982-166">Click **Resource groups** and select the resource group you used.</span></span> <span data-ttu-id="a3982-167">The list of resources in the group is displayed.</span><span class="sxs-lookup"><span data-stu-id="a3982-167">The list of resources in the group is displayed.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="a3982-168">If you want to remove all of the resources in the resource group, click **Delete** to delete the resource group, then follow the directions.</span><span class="sxs-lookup"><span data-stu-id="a3982-168">If you want to remove all of the resources in the resource group, click **Delete** to delete the resource group, then follow the directions.</span></span> <span data-ttu-id="a3982-169">This will remove everything in that resource group, so you're finished cleaning up the resources and can skip to the next section.</span><span class="sxs-lookup"><span data-stu-id="a3982-169">This will remove everything in that resource group, so you're finished cleaning up the resources and can skip to the next section.</span></span>

3. <span data-ttu-id="a3982-170">Click on the IoT hub you used for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="a3982-170">Click on the IoT hub you used for this tutorial.</span></span> 

4. <span data-ttu-id="a3982-171">In the IoT Hub pane, click **Routes**.</span><span class="sxs-lookup"><span data-stu-id="a3982-171">In the IoT Hub pane, click **Routes**.</span></span> <span data-ttu-id="a3982-172">Click the checkbox next to the routing rule you added, then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="a3982-172">Click the checkbox next to the routing rule you added, then click **Delete**.</span></span> <span data-ttu-id="a3982-173">When asked if you're sure you want to delete that route, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="a3982-173">When asked if you're sure you want to delete that route, click **Yes**.</span></span>

   ![Remove routing rule](./media/iot-hub-store-data-in-azure-table-storage/cleanup-remove-routing.png)

   <span data-ttu-id="a3982-175">Close the Routing pane.</span><span class="sxs-lookup"><span data-stu-id="a3982-175">Close the Routing pane.</span></span> <span data-ttu-id="a3982-176">You are returned to the Resource Group pane.</span><span class="sxs-lookup"><span data-stu-id="a3982-176">You are returned to the Resource Group pane.</span></span>

5. <span data-ttu-id="a3982-177">Click on the IoT hub again.</span><span class="sxs-lookup"><span data-stu-id="a3982-177">Click on the IoT hub again.</span></span> 

6. <span data-ttu-id="a3982-178">In the IoT Hub pane, click **Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="a3982-178">In the IoT Hub pane, click **Endpoints**.</span></span> <span data-ttu-id="a3982-179">Click the checkbox next to the endpoint you added for the storage container, then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="a3982-179">Click the checkbox next to the endpoint you added for the storage container, then click **Delete**.</span></span> <span data-ttu-id="a3982-180">When asked if you're sure you want to delete the selected endpoint, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="a3982-180">When asked if you're sure you want to delete the selected endpoint, click **Yes**.</span></span>

    ![Remove endpoint](./media/iot-hub-store-data-in-azure-table-storage/cleanup-remove-endpoint.png)

    <span data-ttu-id="a3982-182">Close the Endpoints pane.</span><span class="sxs-lookup"><span data-stu-id="a3982-182">Close the Endpoints pane.</span></span> <span data-ttu-id="a3982-183">You are returned to the Resource Group pane.</span><span class="sxs-lookup"><span data-stu-id="a3982-183">You are returned to the Resource Group pane.</span></span> 

7.  <span data-ttu-id="a3982-184">Click on the storage account you set up for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="a3982-184">Click on the storage account you set up for this tutorial.</span></span> 

8.  <span data-ttu-id="a3982-185">On the Storage account pane, click **Delete** to remove the storage account.</span><span class="sxs-lookup"><span data-stu-id="a3982-185">On the Storage account pane, click **Delete** to remove the storage account.</span></span> <span data-ttu-id="a3982-186">You are taken to the **Delete storage account** pane.</span><span class="sxs-lookup"><span data-stu-id="a3982-186">You are taken to the **Delete storage account** pane.</span></span>

   ![Remove storage account](./media/iot-hub-store-data-in-azure-table-storage/cleanup-remove-storageaccount.png)

8.  <span data-ttu-id="a3982-188">Type in the storage account name, then click **Delete** at the bottom of the pane.</span><span class="sxs-lookup"><span data-stu-id="a3982-188">Type in the storage account name, then click **Delete** at the bottom of the pane.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a3982-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="a3982-189">Next steps</span></span>

<span data-ttu-id="a3982-190">You’ve successfully created your Azure storage account and routed messages from IoT Hub to a blob container in that storage account.</span><span class="sxs-lookup"><span data-stu-id="a3982-190">You’ve successfully created your Azure storage account and routed messages from IoT Hub to a blob container in that storage account.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
