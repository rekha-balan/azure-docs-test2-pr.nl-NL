---
title: include file
description: include file
services: iot-accelerators
author: dominicbetts
ms.service: iot-accelerators
ms.topic: include
ms.date: 08/20/2018
ms.author: dobett
ms.custom: include file
ms.openlocfilehash: 8c114ed137089e70899e601ebdc1d4d39f562601
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45404183"
---
## <a name="create-a-consumer-group"></a><span data-ttu-id="6c1df-103">Create a consumer group</span><span class="sxs-lookup"><span data-stu-id="6c1df-103">Create a consumer group</span></span>

<span data-ttu-id="6c1df-104">You need to create a dedicated consumer group in your IoT hub to stream telemetry to Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="6c1df-104">You need to create a dedicated consumer group in your IoT hub to stream telemetry to Time Series Insights.</span></span> <span data-ttu-id="6c1df-105">An event source in Time Series Insights should have the exclusive use of an IoT Hub consumer group.</span><span class="sxs-lookup"><span data-stu-id="6c1df-105">An event source in Time Series Insights should have the exclusive use of an IoT Hub consumer group.</span></span>

<span data-ttu-id="6c1df-106">The following steps use the Azure CLI in the Azure Cloud Shell to create the consumer group:</span><span class="sxs-lookup"><span data-stu-id="6c1df-106">The following steps use the Azure CLI in the Azure Cloud Shell to create the consumer group:</span></span>

1. <span data-ttu-id="6c1df-107">The IoT hub is one of several resources created when you deployed the Device Simulation solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="6c1df-107">The IoT hub is one of several resources created when you deployed the Device Simulation solution accelerator.</span></span> <span data-ttu-id="6c1df-108">Execute the following command find the name of your IoT hub - remember to use the name of your solution accelerator:</span><span class="sxs-lookup"><span data-stu-id="6c1df-108">Execute the following command find the name of your IoT hub - remember to use the name of your solution accelerator:</span></span>

    ```azurecli-interactive
    az resource list --resource-group contoso-simulation -o table
    ```

    <span data-ttu-id="6c1df-109">The IoT hub is the resource of type **Microsoft.Devices/IotHubs**.</span><span class="sxs-lookup"><span data-stu-id="6c1df-109">The IoT hub is the resource of type **Microsoft.Devices/IotHubs**.</span></span>

1. <span data-ttu-id="6c1df-110">Add a consumer group called **devicesimulationtsi** to the hub.</span><span class="sxs-lookup"><span data-stu-id="6c1df-110">Add a consumer group called **devicesimulationtsi** to the hub.</span></span> <span data-ttu-id="6c1df-111">In the following command use the name of your hub and solution accelerator:</span><span class="sxs-lookup"><span data-stu-id="6c1df-111">In the following command use the name of your hub and solution accelerator:</span></span>

    ```azurecli-interactive
    az iot hub consumer-group create --hub-name contoso-simulation7d894 --name devicesimulationtsi --resource-group contoso-simulation
    ```

    <span data-ttu-id="6c1df-112">You can now close the Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="6c1df-112">You can now close the Azure Cloud Shell.</span></span>

## <a name="create-a-new-time-series-insights-environment"></a><span data-ttu-id="6c1df-113">Create a new Time Series Insights environment</span><span class="sxs-lookup"><span data-stu-id="6c1df-113">Create a new Time Series Insights environment</span></span>

<span data-ttu-id="6c1df-114">[Azure Time Series Insights](../articles/time-series-insights/time-series-insights-overview.md) is a fully managed analytics, storage, and visualization service for managing IoT-scale time-series data in the cloud.</span><span class="sxs-lookup"><span data-stu-id="6c1df-114">[Azure Time Series Insights](../articles/time-series-insights/time-series-insights-overview.md) is a fully managed analytics, storage, and visualization service for managing IoT-scale time-series data in the cloud.</span></span> <span data-ttu-id="6c1df-115">To create a new Time Series Insights environment:</span><span class="sxs-lookup"><span data-stu-id="6c1df-115">To create a new Time Series Insights environment:</span></span>

1. <span data-ttu-id="6c1df-116">Sign in to the [Azure portal](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6c1df-116">Sign in to the [Azure portal](http://portal.azure.com/).</span></span>

1. <span data-ttu-id="6c1df-117">Select **Create a resource** > **Internet of Things** > **Time Series Insights**:</span><span class="sxs-lookup"><span data-stu-id="6c1df-117">Select **Create a resource** > **Internet of Things** > **Time Series Insights**:</span></span>

    ![New Time Series Insights](./media/iot-accelerators-create-tsi/new-time-series-insights.png)

1. <span data-ttu-id="6c1df-119">To create your Time Series Insights environment in the same resource group as your solution accelerator, use the values in the following table:</span><span class="sxs-lookup"><span data-stu-id="6c1df-119">To create your Time Series Insights environment in the same resource group as your solution accelerator, use the values in the following table:</span></span>

    | <span data-ttu-id="6c1df-120">Setting</span><span class="sxs-lookup"><span data-stu-id="6c1df-120">Setting</span></span> | <span data-ttu-id="6c1df-121">Value</span><span class="sxs-lookup"><span data-stu-id="6c1df-121">Value</span></span> |
    | ------- | ----- |
    | <span data-ttu-id="6c1df-122">Environment Name</span><span class="sxs-lookup"><span data-stu-id="6c1df-122">Environment Name</span></span> | <span data-ttu-id="6c1df-123">The following screenshot uses the name **Contoso-TSI**.</span><span class="sxs-lookup"><span data-stu-id="6c1df-123">The following screenshot uses the name **Contoso-TSI**.</span></span> <span data-ttu-id="6c1df-124">Choose your own unique name when you complete this step.</span><span class="sxs-lookup"><span data-stu-id="6c1df-124">Choose your own unique name when you complete this step.</span></span> |
    | <span data-ttu-id="6c1df-125">Subscription</span><span class="sxs-lookup"><span data-stu-id="6c1df-125">Subscription</span></span> | <span data-ttu-id="6c1df-126">Select your Azure subscription in the drop-down.</span><span class="sxs-lookup"><span data-stu-id="6c1df-126">Select your Azure subscription in the drop-down.</span></span> |
    | <span data-ttu-id="6c1df-127">Resource group</span><span class="sxs-lookup"><span data-stu-id="6c1df-127">Resource group</span></span> | <span data-ttu-id="6c1df-128">**contoso-simulation**.</span><span class="sxs-lookup"><span data-stu-id="6c1df-128">**contoso-simulation**.</span></span> <span data-ttu-id="6c1df-129">Use the name of your solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="6c1df-129">Use the name of your solution accelerator.</span></span> |
    | <span data-ttu-id="6c1df-130">Location</span><span class="sxs-lookup"><span data-stu-id="6c1df-130">Location</span></span> | <span data-ttu-id="6c1df-131">This example uses **East US**.</span><span class="sxs-lookup"><span data-stu-id="6c1df-131">This example uses **East US**.</span></span> <span data-ttu-id="6c1df-132">Create your environment in the same region as your Device simulation accelerator.</span><span class="sxs-lookup"><span data-stu-id="6c1df-132">Create your environment in the same region as your Device simulation accelerator.</span></span> |
    | <span data-ttu-id="6c1df-133">Sku</span><span class="sxs-lookup"><span data-stu-id="6c1df-133">Sku</span></span> |<span data-ttu-id="6c1df-134">**S1**</span><span class="sxs-lookup"><span data-stu-id="6c1df-134">**S1**</span></span> |
    | <span data-ttu-id="6c1df-135">Capacity</span><span class="sxs-lookup"><span data-stu-id="6c1df-135">Capacity</span></span> | <span data-ttu-id="6c1df-136">**1**</span><span class="sxs-lookup"><span data-stu-id="6c1df-136">**1**</span></span> |

    ![Create Time Series Insights](./media/iot-accelerators-create-tsi/new-time-series-insights-create.png)

    > [!NOTE]
    > <span data-ttu-id="6c1df-138">Adding the Time Series Insights environment to the same resource group as the solution accelerator means that it's deleted when you delete the solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="6c1df-138">Adding the Time Series Insights environment to the same resource group as the solution accelerator means that it's deleted when you delete the solution accelerator.</span></span>

1. <span data-ttu-id="6c1df-139">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6c1df-139">Click **Create**.</span></span> <span data-ttu-id="6c1df-140">It can take a few minutes for the environment to be created.</span><span class="sxs-lookup"><span data-stu-id="6c1df-140">It can take a few minutes for the environment to be created.</span></span>

## <a name="create-event-source"></a><span data-ttu-id="6c1df-141">Create event source</span><span class="sxs-lookup"><span data-stu-id="6c1df-141">Create event source</span></span>

<span data-ttu-id="6c1df-142">Create a new event source to connect to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6c1df-142">Create a new event source to connect to your IoT hub.</span></span> <span data-ttu-id="6c1df-143">Use the consumer group you created in the previous steps.</span><span class="sxs-lookup"><span data-stu-id="6c1df-143">Use the consumer group you created in the previous steps.</span></span> <span data-ttu-id="6c1df-144">A Time Series Insights event source requires a dedicated consumer group not in use by another service.</span><span class="sxs-lookup"><span data-stu-id="6c1df-144">A Time Series Insights event source requires a dedicated consumer group not in use by another service.</span></span>

1. <span data-ttu-id="6c1df-145">In the Azure portal, navigate to your new Time Series Environment.</span><span class="sxs-lookup"><span data-stu-id="6c1df-145">In the Azure portal, navigate to your new Time Series Environment.</span></span>

1. <span data-ttu-id="6c1df-146">On the left, click **Event Sources**:</span><span class="sxs-lookup"><span data-stu-id="6c1df-146">On the left, click **Event Sources**:</span></span>

    ![View Event Sources](./media/iot-accelerators-create-tsi/time-series-insights-event-sources.png)

1. <span data-ttu-id="6c1df-148">Click **Add**:</span><span class="sxs-lookup"><span data-stu-id="6c1df-148">Click **Add**:</span></span>

    ![Add Event Source](./media/iot-accelerators-create-tsi/time-series-insights-event-sources-add.png)

1. <span data-ttu-id="6c1df-150">To configure your IoT hub as a new event source, use the values in the following table:</span><span class="sxs-lookup"><span data-stu-id="6c1df-150">To configure your IoT hub as a new event source, use the values in the following table:</span></span>

    | <span data-ttu-id="6c1df-151">Setting</span><span class="sxs-lookup"><span data-stu-id="6c1df-151">Setting</span></span> | <span data-ttu-id="6c1df-152">Value</span><span class="sxs-lookup"><span data-stu-id="6c1df-152">Value</span></span> |
    | ------- | ----- |
    | <span data-ttu-id="6c1df-153">Event source Name</span><span class="sxs-lookup"><span data-stu-id="6c1df-153">Event source Name</span></span> | <span data-ttu-id="6c1df-154">The following screenshot uses the name **contoso-iot-hub**.</span><span class="sxs-lookup"><span data-stu-id="6c1df-154">The following screenshot uses the name **contoso-iot-hub**.</span></span> <span data-ttu-id="6c1df-155">Use your own unique name when you complete this step.</span><span class="sxs-lookup"><span data-stu-id="6c1df-155">Use your own unique name when you complete this step.</span></span> |
    | <span data-ttu-id="6c1df-156">Source</span><span class="sxs-lookup"><span data-stu-id="6c1df-156">Source</span></span> | <span data-ttu-id="6c1df-157">**IoT Hub**</span><span class="sxs-lookup"><span data-stu-id="6c1df-157">**IoT Hub**</span></span> |
    | <span data-ttu-id="6c1df-158">Import option</span><span class="sxs-lookup"><span data-stu-id="6c1df-158">Import option</span></span> | <span data-ttu-id="6c1df-159">**Use IoT Hub from available subscriptions**</span><span class="sxs-lookup"><span data-stu-id="6c1df-159">**Use IoT Hub from available subscriptions**</span></span> |
    | <span data-ttu-id="6c1df-160">Subscription Id</span><span class="sxs-lookup"><span data-stu-id="6c1df-160">Subscription Id</span></span> | <span data-ttu-id="6c1df-161">Select your Azure subscription in the drop-down.</span><span class="sxs-lookup"><span data-stu-id="6c1df-161">Select your Azure subscription in the drop-down.</span></span> |
    | <span data-ttu-id="6c1df-162">Iot hub name</span><span class="sxs-lookup"><span data-stu-id="6c1df-162">Iot hub name</span></span> | <span data-ttu-id="6c1df-163">**contoso-simulation7d894**.</span><span class="sxs-lookup"><span data-stu-id="6c1df-163">**contoso-simulation7d894**.</span></span> <span data-ttu-id="6c1df-164">Use the name of your IoT hub from your Device Simulation solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="6c1df-164">Use the name of your IoT hub from your Device Simulation solution accelerator.</span></span> |
    | <span data-ttu-id="6c1df-165">Iot hub policy name</span><span class="sxs-lookup"><span data-stu-id="6c1df-165">Iot hub policy name</span></span> | <span data-ttu-id="6c1df-166">**iothubowner**</span><span class="sxs-lookup"><span data-stu-id="6c1df-166">**iothubowner**</span></span> |
    | <span data-ttu-id="6c1df-167">Iot hub policy key</span><span class="sxs-lookup"><span data-stu-id="6c1df-167">Iot hub policy key</span></span> | <span data-ttu-id="6c1df-168">This field is populated automatically.</span><span class="sxs-lookup"><span data-stu-id="6c1df-168">This field is populated automatically.</span></span> |
    | <span data-ttu-id="6c1df-169">Iot hub consumer group</span><span class="sxs-lookup"><span data-stu-id="6c1df-169">Iot hub consumer group</span></span> | <span data-ttu-id="6c1df-170">**devicesimulationtsi**</span><span class="sxs-lookup"><span data-stu-id="6c1df-170">**devicesimulationtsi**</span></span> |
    | <span data-ttu-id="6c1df-171">Event serialization format</span><span class="sxs-lookup"><span data-stu-id="6c1df-171">Event serialization format</span></span> | <span data-ttu-id="6c1df-172">**JSON**</span><span class="sxs-lookup"><span data-stu-id="6c1df-172">**JSON**</span></span> |
    | <span data-ttu-id="6c1df-173">Timestamp property name</span><span class="sxs-lookup"><span data-stu-id="6c1df-173">Timestamp property name</span></span> | <span data-ttu-id="6c1df-174">Leave blank</span><span class="sxs-lookup"><span data-stu-id="6c1df-174">Leave blank</span></span> |

    ![Create Event Source](./media/iot-accelerators-create-tsi/time-series-insights-event-source-create.png)

1. <span data-ttu-id="6c1df-176">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6c1df-176">Click **Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="6c1df-177">You can [grant additional users access](../articles/time-series-insights/time-series-insights-data-access.md#grant-data-access) to the Time Series Insights explorer.</span><span class="sxs-lookup"><span data-stu-id="6c1df-177">You can [grant additional users access](../articles/time-series-insights/time-series-insights-data-access.md#grant-data-access) to the Time Series Insights explorer.</span></span>