---
title: Synchronize device state from Azure IoT Hub | Microsoft Docs
description: Use device twins to synchronize state between your devices and your IoT hub
services: iot-hub
documentationcenter: ''
author: dominicbetts
manager: timlt
ms.assetid: ''
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/14/2018
ms.author: dobett
ms.custom: mvc
ms.openlocfilehash: 3d0f24331243c22fa356de7778a89185df2cde4e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865731"
---
<!-- **TODO** Update publish config with repo paths before publishing! -->

# <a name="tutorial-configure-your-devices-from-a-back-end-service"></a><span data-ttu-id="38fbe-103">Tutorial: Configure your devices from a back-end service</span><span class="sxs-lookup"><span data-stu-id="38fbe-103">Tutorial: Configure your devices from a back-end service</span></span>

<span data-ttu-id="38fbe-104">As well as receiving telemetry from your devices, you may need to configure your devices from your back-end service.</span><span class="sxs-lookup"><span data-stu-id="38fbe-104">As well as receiving telemetry from your devices, you may need to configure your devices from your back-end service.</span></span> <span data-ttu-id="38fbe-105">When you send a desired configuration to your devices, you may also want to receive status and compliance updates from those devices.</span><span class="sxs-lookup"><span data-stu-id="38fbe-105">When you send a desired configuration to your devices, you may also want to receive status and compliance updates from those devices.</span></span> <span data-ttu-id="38fbe-106">For example, you might set a target operational temperature range for a device or collect firmware version information from your devices.</span><span class="sxs-lookup"><span data-stu-id="38fbe-106">For example, you might set a target operational temperature range for a device or collect firmware version information from your devices.</span></span>

<span data-ttu-id="38fbe-107">To synchronize state information between a device and an IoT hub, you use _device twins_.</span><span class="sxs-lookup"><span data-stu-id="38fbe-107">To synchronize state information between a device and an IoT hub, you use _device twins_.</span></span> <span data-ttu-id="38fbe-108">A [device twin](iot-hub-devguide-device-twins.md) is a JSON document, associated with a specific device, and stored by IoT Hub in the cloud where you can [query](iot-hub-devguide-query-language.md) them.</span><span class="sxs-lookup"><span data-stu-id="38fbe-108">A [device twin](iot-hub-devguide-device-twins.md) is a JSON document, associated with a specific device, and stored by IoT Hub in the cloud where you can [query](iot-hub-devguide-query-language.md) them.</span></span> <span data-ttu-id="38fbe-109">A device twin contains _desired properties_, _reported properties_, and _tags_.</span><span class="sxs-lookup"><span data-stu-id="38fbe-109">A device twin contains _desired properties_, _reported properties_, and _tags_.</span></span> <span data-ttu-id="38fbe-110">A desired property is set by a back-end application and read by a device.</span><span class="sxs-lookup"><span data-stu-id="38fbe-110">A desired property is set by a back-end application and read by a device.</span></span> <span data-ttu-id="38fbe-111">A reported property is set by a device and read by a back-end application.</span><span class="sxs-lookup"><span data-stu-id="38fbe-111">A reported property is set by a device and read by a back-end application.</span></span> <span data-ttu-id="38fbe-112">A tag is set by a back-end application and is never sent to a device.</span><span class="sxs-lookup"><span data-stu-id="38fbe-112">A tag is set by a back-end application and is never sent to a device.</span></span> <span data-ttu-id="38fbe-113">You use tags to organize your devices.</span><span class="sxs-lookup"><span data-stu-id="38fbe-113">You use tags to organize your devices.</span></span> <span data-ttu-id="38fbe-114">This tutorial shows you how to use desired and reported properties to synchronize state information:</span><span class="sxs-lookup"><span data-stu-id="38fbe-114">This tutorial shows you how to use desired and reported properties to synchronize state information:</span></span>

![Twin summary](media/tutorial-device-twins/DeviceTwins.png)

<span data-ttu-id="38fbe-116">In this tutorial, you perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="38fbe-116">In this tutorial, you perform the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="38fbe-117">Create an IoT hub and add a test device to the identity registry.</span><span class="sxs-lookup"><span data-stu-id="38fbe-117">Create an IoT hub and add a test device to the identity registry.</span></span>
> * <span data-ttu-id="38fbe-118">Use desired properties to send state information to your simulated device.</span><span class="sxs-lookup"><span data-stu-id="38fbe-118">Use desired properties to send state information to your simulated device.</span></span>
> * <span data-ttu-id="38fbe-119">Use reported properties to receive state information from your simulated device.</span><span class="sxs-lookup"><span data-stu-id="38fbe-119">Use reported properties to receive state information from your simulated device.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="38fbe-120">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="38fbe-120">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38fbe-121">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="38fbe-121">Prerequisites</span></span>

<span data-ttu-id="38fbe-122">The two sample applications you run in this quickstart are written using Node.js.</span><span class="sxs-lookup"><span data-stu-id="38fbe-122">The two sample applications you run in this quickstart are written using Node.js.</span></span> <span data-ttu-id="38fbe-123">You need Node.js v4.x.x or later on your development machine.</span><span class="sxs-lookup"><span data-stu-id="38fbe-123">You need Node.js v4.x.x or later on your development machine.</span></span>

<span data-ttu-id="38fbe-124">You can download Node.js for multiple platforms from [nodejs.org](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="38fbe-124">You can download Node.js for multiple platforms from [nodejs.org](https://nodejs.org).</span></span>

<span data-ttu-id="38fbe-125">You can verify the current version of Node.js on your development machine using the following command:</span><span class="sxs-lookup"><span data-stu-id="38fbe-125">You can verify the current version of Node.js on your development machine using the following command:</span></span>

```cmd/sh
node --version
```

<span data-ttu-id="38fbe-126">Download the sample Node.js project from https://github.com/Azure-Samples/azure-iot-samples-node/archive/master.zip and extract the ZIP archive.</span><span class="sxs-lookup"><span data-stu-id="38fbe-126">Download the sample Node.js project from https://github.com/Azure-Samples/azure-iot-samples-node/archive/master.zip and extract the ZIP archive.</span></span>

## <a name="set-up-azure-resources"></a><span data-ttu-id="38fbe-127">Set up Azure resources</span><span class="sxs-lookup"><span data-stu-id="38fbe-127">Set up Azure resources</span></span>

<span data-ttu-id="38fbe-128">To complete this tutorial, your Azure subscription must contain an IoT hub with a device added to the device identity registry.</span><span class="sxs-lookup"><span data-stu-id="38fbe-128">To complete this tutorial, your Azure subscription must contain an IoT hub with a device added to the device identity registry.</span></span> <span data-ttu-id="38fbe-129">The entry in the device identity registry enables the simulated device you run in this tutorial to connect to your hub.</span><span class="sxs-lookup"><span data-stu-id="38fbe-129">The entry in the device identity registry enables the simulated device you run in this tutorial to connect to your hub.</span></span>

<span data-ttu-id="38fbe-130">If you don't already have an IoT hub set up in your subscription, you can set one up with following CLI script.</span><span class="sxs-lookup"><span data-stu-id="38fbe-130">If you don't already have an IoT hub set up in your subscription, you can set one up with following CLI script.</span></span> <span data-ttu-id="38fbe-131">This script uses the name **tutorial-iot-hub** for the IoT hub, you should replace this name with your own unique name when you run it.</span><span class="sxs-lookup"><span data-stu-id="38fbe-131">This script uses the name **tutorial-iot-hub** for the IoT hub, you should replace this name with your own unique name when you run it.</span></span> <span data-ttu-id="38fbe-132">The script creates the resource group and hub in the **Central US** region, which you can change to a region closer to you.</span><span class="sxs-lookup"><span data-stu-id="38fbe-132">The script creates the resource group and hub in the **Central US** region, which you can change to a region closer to you.</span></span> <span data-ttu-id="38fbe-133">The script retrieves your IoT hub service connection string, which you use in the back-end sample to connect to your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="38fbe-133">The script retrieves your IoT hub service connection string, which you use in the back-end sample to connect to your IoT hub:</span></span>

```azurecli-interactive
hubname=tutorial-iot-hub
location=centralus

# Install the IoT extension if it's not already installed:
az extension add --name azure-cli-iot-ext

# Create a resource group:
az group create --name tutorial-iot-hub-rg --location $location

# Create your free-tier IoT Hub. You can only have one free IoT Hub per subscription:
az iot hub create --name $hubname --location $location --resource-group tutorial-iot-hub-rg --sku F1

# Make a note of the service connection string, you need it later:
az iot hub show-connection-string --hub-name $hubname -o table

```

<span data-ttu-id="38fbe-134">This tutorial uses a simulated device called **MyTwinDevice**.</span><span class="sxs-lookup"><span data-stu-id="38fbe-134">This tutorial uses a simulated device called **MyTwinDevice**.</span></span> <span data-ttu-id="38fbe-135">The following script adds this device to your identity registry and retrieves its connection string:</span><span class="sxs-lookup"><span data-stu-id="38fbe-135">The following script adds this device to your identity registry and retrieves its connection string:</span></span>

```azurecli-interactive
# Set the name of your IoT hub:
hubname=tutorial-iot-hub

# Create the device in the identity registry:
az iot hub device-identity create --device-id MyTwinDevice --hub-name $hubname --resource-group tutorial-iot-hub-rg

# Retrieve the device connection string, you need this later:
az iot hub device-identity show-connection-string --device-id MyTwinDevice --hub-name $hubname --resource-group tutorial-iot-hub-rg -o table

```

## <a name="send-state-information"></a><span data-ttu-id="38fbe-136">Send state information</span><span class="sxs-lookup"><span data-stu-id="38fbe-136">Send state information</span></span>

<span data-ttu-id="38fbe-137">You use desired properties to send state information from a back-end application to a device.</span><span class="sxs-lookup"><span data-stu-id="38fbe-137">You use desired properties to send state information from a back-end application to a device.</span></span> <span data-ttu-id="38fbe-138">In this section, you see how to:</span><span class="sxs-lookup"><span data-stu-id="38fbe-138">In this section, you see how to:</span></span>

* <span data-ttu-id="38fbe-139">Receive and process desired properties on a device.</span><span class="sxs-lookup"><span data-stu-id="38fbe-139">Receive and process desired properties on a device.</span></span>
* <span data-ttu-id="38fbe-140">Send desired properties from a back-end application.</span><span class="sxs-lookup"><span data-stu-id="38fbe-140">Send desired properties from a back-end application.</span></span>

<span data-ttu-id="38fbe-141">To view the simulated device sample code that receives desired properties, navigate to the **iot-hub/Tutorials/DeviceTwins** folder in the sample Node.js project you downloaded.</span><span class="sxs-lookup"><span data-stu-id="38fbe-141">To view the simulated device sample code that receives desired properties, navigate to the **iot-hub/Tutorials/DeviceTwins** folder in the sample Node.js project you downloaded.</span></span> <span data-ttu-id="38fbe-142">Then open the SimulatedDevice.js file in a text editor.</span><span class="sxs-lookup"><span data-stu-id="38fbe-142">Then open the SimulatedDevice.js file in a text editor.</span></span>

<span data-ttu-id="38fbe-143">The following sections describe the code that runs on the simulated device that responds to desired property changes sent from the back end application:</span><span class="sxs-lookup"><span data-stu-id="38fbe-143">The following sections describe the code that runs on the simulated device that responds to desired property changes sent from the back end application:</span></span>

### <a name="retrieve-the-device-twin-object"></a><span data-ttu-id="38fbe-144">Retrieve the device twin object</span><span class="sxs-lookup"><span data-stu-id="38fbe-144">Retrieve the device twin object</span></span>

<span data-ttu-id="38fbe-145">The following code connects to your IoT hub using a device connection string:</span><span class="sxs-lookup"><span data-stu-id="38fbe-145">The following code connects to your IoT hub using a device connection string:</span></span>

[!code-javascript[Create IoT Hub client](~/iot-samples-node/iot-hub/Tutorials/DeviceTwins/SimulatedDevice.js?name=createhubclient&highlight=2 "Create IoT Hub client")]

<span data-ttu-id="38fbe-146">The following code gets a twin from the client object:</span><span class="sxs-lookup"><span data-stu-id="38fbe-146">The following code gets a twin from the client object:</span></span>

[!code-javascript[Get twin](~/iot-samples-node/iot-hub/Tutorials/DeviceTwins/SimulatedDevice.js?name=gettwin&highlight=2 "Get twin")]

### <a name="sample-desired-properties"></a><span data-ttu-id="38fbe-147">Sample desired properties</span><span class="sxs-lookup"><span data-stu-id="38fbe-147">Sample desired properties</span></span>

<span data-ttu-id="38fbe-148">You can structure your desired properties in any way that's convenient to your application.</span><span class="sxs-lookup"><span data-stu-id="38fbe-148">You can structure your desired properties in any way that's convenient to your application.</span></span> <span data-ttu-id="38fbe-149">This example uses one top-level property called **fanOn** and groups the remaining properties into separate **components**.</span><span class="sxs-lookup"><span data-stu-id="38fbe-149">This example uses one top-level property called **fanOn** and groups the remaining properties into separate **components**.</span></span> <span data-ttu-id="38fbe-150">The following JSON snippet shows the structure of the desired properties this tutorial uses:</span><span class="sxs-lookup"><span data-stu-id="38fbe-150">The following JSON snippet shows the structure of the desired properties this tutorial uses:</span></span>

[!code[Sample desired properties](~/iot-samples-node/iot-hub/Tutorials/DeviceTwins/desired.json "Sample desired properties")]

### <a name="create-handlers"></a><span data-ttu-id="38fbe-151">Create handlers</span><span class="sxs-lookup"><span data-stu-id="38fbe-151">Create handlers</span></span>

<span data-ttu-id="38fbe-152">You can create handlers for desired property updates that respond to updates at different levels in the JSON hierarchy.</span><span class="sxs-lookup"><span data-stu-id="38fbe-152">You can create handlers for desired property updates that respond to updates at different levels in the JSON hierarchy.</span></span> <span data-ttu-id="38fbe-153">For example, this handler sees all desired property changes sent to the device from a back-end application.</span><span class="sxs-lookup"><span data-stu-id="38fbe-153">For example, this handler sees all desired property changes sent to the device from a back-end application.</span></span> <span data-ttu-id="38fbe-154">The **delta** variable contains the desired properties sent from the solution back end:</span><span class="sxs-lookup"><span data-stu-id="38fbe-154">The **delta** variable contains the desired properties sent from the solution back end:</span></span>

[!code-javascript[Handle all properties](~/iot-samples-node/iot-hub/Tutorials/DeviceTwins/SimulatedDevice.js?name=allproperties&highlight=2 "Handle all properties")]

<span data-ttu-id="38fbe-155">The following handler only reacts to changes made to the **fanOn** desired property:</span><span class="sxs-lookup"><span data-stu-id="38fbe-155">The following handler only reacts to changes made to the **fanOn** desired property:</span></span>

[!code-javascript[Handle fan property](~/iot-samples-node/iot-hub/Tutorials/DeviceTwins/SimulatedDevice.js?name=fanproperty&highlight=2 "Handle fan property")]

### <a name="handlers-for-multiple-properties"></a><span data-ttu-id="38fbe-156">Handlers for multiple properties</span><span class="sxs-lookup"><span data-stu-id="38fbe-156">Handlers for multiple properties</span></span>

<span data-ttu-id="38fbe-157">In the example desired properties JSON shown previously, the **climate** node under **components** contains two properties, **minTemperature** and **maxTemperature**.</span><span class="sxs-lookup"><span data-stu-id="38fbe-157">In the example desired properties JSON shown previously, the **climate** node under **components** contains two properties, **minTemperature** and **maxTemperature**.</span></span>

<span data-ttu-id="38fbe-158">A device's local **twin** object stores a complete set of desired and reported properties.</span><span class="sxs-lookup"><span data-stu-id="38fbe-158">A device's local **twin** object stores a complete set of desired and reported properties.</span></span> <span data-ttu-id="38fbe-159">The **delta** sent from the back end might update just a subset of desired properties.</span><span class="sxs-lookup"><span data-stu-id="38fbe-159">The **delta** sent from the back end might update just a subset of desired properties.</span></span> <span data-ttu-id="38fbe-160">In the following code snippet, if the simulated device receives an update to just one of **minTemperature** and **maxTemperature**, it uses the value in the local twin for the other value to configure the device:</span><span class="sxs-lookup"><span data-stu-id="38fbe-160">In the following code snippet, if the simulated device receives an update to just one of **minTemperature** and **maxTemperature**, it uses the value in the local twin for the other value to configure the device:</span></span>

[!code-javascript[Handle climate component](~/iot-samples-node/iot-hub/Tutorials/DeviceTwins/SimulatedDevice.js?name=climatecomponent&highlight=2 "Handle climate component")]

<span data-ttu-id="38fbe-161">The local **twin** object stores a complete set of desired and reported properties.</span><span class="sxs-lookup"><span data-stu-id="38fbe-161">The local **twin** object stores a complete set of desired and reported properties.</span></span> <span data-ttu-id="38fbe-162">The **delta** sent from the back end might update just a subset of desired properties.</span><span class="sxs-lookup"><span data-stu-id="38fbe-162">The **delta** sent from the back end might update just a subset of desired properties.</span></span>

### <a name="handle-insert-update-and-delete-operations"></a><span data-ttu-id="38fbe-163">Handle insert, update, and delete operations</span><span class="sxs-lookup"><span data-stu-id="38fbe-163">Handle insert, update, and delete operations</span></span>

<span data-ttu-id="38fbe-164">The desired properties sent from the back end don't indicate what operation is being performed on a particular desired property.</span><span class="sxs-lookup"><span data-stu-id="38fbe-164">The desired properties sent from the back end don't indicate what operation is being performed on a particular desired property.</span></span> <span data-ttu-id="38fbe-165">Your code needs to infer the operation from the current set of desired properties stored locally and the changes sent from the hub.</span><span class="sxs-lookup"><span data-stu-id="38fbe-165">Your code needs to infer the operation from the current set of desired properties stored locally and the changes sent from the hub.</span></span>

<span data-ttu-id="38fbe-166">The following snippet shows how the simulated device handles insert, update, and delete operations on the list of **components** in the desired properties.</span><span class="sxs-lookup"><span data-stu-id="38fbe-166">The following snippet shows how the simulated device handles insert, update, and delete operations on the list of **components** in the desired properties.</span></span> <span data-ttu-id="38fbe-167">You can see how to use **null** values to indicate that a component should be deleted:</span><span class="sxs-lookup"><span data-stu-id="38fbe-167">You can see how to use **null** values to indicate that a component should be deleted:</span></span>

[!code-javascript[Handle components](~/iot-samples-node/iot-hub/Tutorials/DeviceTwins/SimulatedDevice.js?name=components&highlight=2,6,13 "Handle components")]

### <a name="send-desired-properties-to-a-device-from-the-back-end"></a><span data-ttu-id="38fbe-168">Send desired properties to a device from the back end</span><span class="sxs-lookup"><span data-stu-id="38fbe-168">Send desired properties to a device from the back end</span></span>

<span data-ttu-id="38fbe-169">You've seen how a device implements handlers for receiving desired property updates.</span><span class="sxs-lookup"><span data-stu-id="38fbe-169">You've seen how a device implements handlers for receiving desired property updates.</span></span> <span data-ttu-id="38fbe-170">This section shows you how to send desired property changes to a device from a back-end application.</span><span class="sxs-lookup"><span data-stu-id="38fbe-170">This section shows you how to send desired property changes to a device from a back-end application.</span></span>

<span data-ttu-id="38fbe-171">To view the simulated device sample code that receives desired properties, navigate to the **iot-hub/Tutorials/DeviceTwins** folder in the sample Node.js project you downloaded.</span><span class="sxs-lookup"><span data-stu-id="38fbe-171">To view the simulated device sample code that receives desired properties, navigate to the **iot-hub/Tutorials/DeviceTwins** folder in the sample Node.js project you downloaded.</span></span> <span data-ttu-id="38fbe-172">Then open the ServiceClient.js file in a text editor.</span><span class="sxs-lookup"><span data-stu-id="38fbe-172">Then open the ServiceClient.js file in a text editor.</span></span>

<span data-ttu-id="38fbe-173">The following code snippet shows how to connect to the device identity registry and access the twin for a specific device:</span><span class="sxs-lookup"><span data-stu-id="38fbe-173">The following code snippet shows how to connect to the device identity registry and access the twin for a specific device:</span></span>

[!code-javascript[Create registry and get twin](~/iot-samples-node/iot-hub/Tutorials/DeviceTwins/ServiceClient.js?name=getregistrytwin&highlight=2,6 "Create registry and get twin")]

<span data-ttu-id="38fbe-174">The following snippet shows different desired property *patches* the back end application sends to the device:</span><span class="sxs-lookup"><span data-stu-id="38fbe-174">The following snippet shows different desired property *patches* the back end application sends to the device:</span></span>

[!code-javascript[Patches sent to device](~/iot-samples-node/iot-hub/Tutorials/DeviceTwins/ServiceClient.js?name=patches&highlight=2,12,26,41,56 "Patches sent to device")]

<span data-ttu-id="38fbe-175">The following snippet shows how the back-end application sends a desired property update to a device:</span><span class="sxs-lookup"><span data-stu-id="38fbe-175">The following snippet shows how the back-end application sends a desired property update to a device:</span></span>

[!code-javascript[Send desired properties](~/iot-samples-node/iot-hub/Tutorials/DeviceTwins/ServiceClient.js?name=senddesiredproperties&highlight=2 "Send desired properties")]

### <a name="run-the-applications"></a><span data-ttu-id="38fbe-176">Run the applications</span><span class="sxs-lookup"><span data-stu-id="38fbe-176">Run the applications</span></span>

<span data-ttu-id="38fbe-177">In this section, you run two sample applications to observe as a back-end application sends desired property updates to a simulated device application.</span><span class="sxs-lookup"><span data-stu-id="38fbe-177">In this section, you run two sample applications to observe as a back-end application sends desired property updates to a simulated device application.</span></span>

<span data-ttu-id="38fbe-178">To run the simulated device and back-end applications, you need the device and service connection strings.</span><span class="sxs-lookup"><span data-stu-id="38fbe-178">To run the simulated device and back-end applications, you need the device and service connection strings.</span></span> <span data-ttu-id="38fbe-179">You made a note of the connection strings when you created the resources at the start of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="38fbe-179">You made a note of the connection strings when you created the resources at the start of this tutorial.</span></span>

<span data-ttu-id="38fbe-180">To run the simulated device application, open a shell or command prompt window and navigate to the **iot-hub/Tutorials/DeviceTwins** folder in the Node.js project you downloaded.</span><span class="sxs-lookup"><span data-stu-id="38fbe-180">To run the simulated device application, open a shell or command prompt window and navigate to the **iot-hub/Tutorials/DeviceTwins** folder in the Node.js project you downloaded.</span></span> <span data-ttu-id="38fbe-181">Then run the following commands:</span><span class="sxs-lookup"><span data-stu-id="38fbe-181">Then run the following commands:</span></span>

```cmd/sh
npm install
node SimulatedDevice.js "{your device connection string}"
```

<span data-ttu-id="38fbe-182">To run the back-end application, open another shell or command prompt window.</span><span class="sxs-lookup"><span data-stu-id="38fbe-182">To run the back-end application, open another shell or command prompt window.</span></span> <span data-ttu-id="38fbe-183">Then navigate to the **iot-hub/Tutorials/DeviceTwins** folder in the Node.js project you downloaded.</span><span class="sxs-lookup"><span data-stu-id="38fbe-183">Then navigate to the **iot-hub/Tutorials/DeviceTwins** folder in the Node.js project you downloaded.</span></span> <span data-ttu-id="38fbe-184">Then run the following commands:</span><span class="sxs-lookup"><span data-stu-id="38fbe-184">Then run the following commands:</span></span>

```cmd/sh
npm install
node ServiceClient.js "{your service connection string}"
```

<span data-ttu-id="38fbe-185">The following screenshot shows the output from the simulated device application and highlights how it handles an update to the **maxTemperature** desired property.</span><span class="sxs-lookup"><span data-stu-id="38fbe-185">The following screenshot shows the output from the simulated device application and highlights how it handles an update to the **maxTemperature** desired property.</span></span> <span data-ttu-id="38fbe-186">You can see how both the top-level handler and the climate component handlers run:</span><span class="sxs-lookup"><span data-stu-id="38fbe-186">You can see how both the top-level handler and the climate component handlers run:</span></span>

![Simulated device](./media/tutorial-device-twins/SimulatedDevice1.png)

<span data-ttu-id="38fbe-188">The following screenshot shows the output from the back-end application and highlights how it sends an update to the **maxTemperature** desired property:</span><span class="sxs-lookup"><span data-stu-id="38fbe-188">The following screenshot shows the output from the back-end application and highlights how it sends an update to the **maxTemperature** desired property:</span></span>

![Back-end application](./media/tutorial-device-twins/BackEnd1.png)

## <a name="receive-state-information"></a><span data-ttu-id="38fbe-190">Receive state information</span><span class="sxs-lookup"><span data-stu-id="38fbe-190">Receive state information</span></span>

<span data-ttu-id="38fbe-191">Your back-end application receives state information from a device as reported properties.</span><span class="sxs-lookup"><span data-stu-id="38fbe-191">Your back-end application receives state information from a device as reported properties.</span></span> <span data-ttu-id="38fbe-192">A device sets the reported properties, and sends them to your hub.</span><span class="sxs-lookup"><span data-stu-id="38fbe-192">A device sets the reported properties, and sends them to your hub.</span></span> <span data-ttu-id="38fbe-193">A back-end application can read the current values of the reported properties from the device twin stored in your hub.</span><span class="sxs-lookup"><span data-stu-id="38fbe-193">A back-end application can read the current values of the reported properties from the device twin stored in your hub.</span></span>

### <a name="send-reported-properties-from-a-device"></a><span data-ttu-id="38fbe-194">Send reported properties from a device</span><span class="sxs-lookup"><span data-stu-id="38fbe-194">Send reported properties from a device</span></span>

<span data-ttu-id="38fbe-195">You can send updates to reported property values as a patch.</span><span class="sxs-lookup"><span data-stu-id="38fbe-195">You can send updates to reported property values as a patch.</span></span> <span data-ttu-id="38fbe-196">The following snippet shows a template for the patch the simulated device sends.</span><span class="sxs-lookup"><span data-stu-id="38fbe-196">The following snippet shows a template for the patch the simulated device sends.</span></span> <span data-ttu-id="38fbe-197">The simulated device updates the fields in the patch before sending it to the hub:</span><span class="sxs-lookup"><span data-stu-id="38fbe-197">The simulated device updates the fields in the patch before sending it to the hub:</span></span>

[!code-javascript[Reported properties patches](~/iot-samples-node/iot-hub/Tutorials/DeviceTwins/SimulatedDevice.js?name=reportedpatch&highlight=2 "Reported properties patches")]

<span data-ttu-id="38fbe-198">The simulated device uses the following function to send the patch that contains the reported properties to the hub:</span><span class="sxs-lookup"><span data-stu-id="38fbe-198">The simulated device uses the following function to send the patch that contains the reported properties to the hub:</span></span>

[!code-javascript[Send reported properties](~/iot-samples-node/iot-hub/Tutorials/DeviceTwins/SimulatedDevice.js?name=sendreportedproperties&highlight=2 "Send reported properties")]

### <a name="process-reported-properties"></a><span data-ttu-id="38fbe-199">Process reported properties</span><span class="sxs-lookup"><span data-stu-id="38fbe-199">Process reported properties</span></span>

<span data-ttu-id="38fbe-200">A back-end application accesses the current reported property values for a device through the device twin.</span><span class="sxs-lookup"><span data-stu-id="38fbe-200">A back-end application accesses the current reported property values for a device through the device twin.</span></span> <span data-ttu-id="38fbe-201">The following snippet shows you how the back-end application reads the reported property values for the simulated device:</span><span class="sxs-lookup"><span data-stu-id="38fbe-201">The following snippet shows you how the back-end application reads the reported property values for the simulated device:</span></span>

[!code-javascript[Display reported properties](~/iot-samples-node/iot-hub/Tutorials/DeviceTwins/ServiceClient.js?name=displayreportedproperties&highlight=2 "Display reported properties")]

### <a name="run-the-applications"></a><span data-ttu-id="38fbe-202">Run the applications</span><span class="sxs-lookup"><span data-stu-id="38fbe-202">Run the applications</span></span>

<span data-ttu-id="38fbe-203">In this section, you run two sample applications to observe as a simulated device application sends reported property updates to a back-end application.</span><span class="sxs-lookup"><span data-stu-id="38fbe-203">In this section, you run two sample applications to observe as a simulated device application sends reported property updates to a back-end application.</span></span>

<span data-ttu-id="38fbe-204">You run the same two sample applications that you ran to see how desired properties are sent to a device.</span><span class="sxs-lookup"><span data-stu-id="38fbe-204">You run the same two sample applications that you ran to see how desired properties are sent to a device.</span></span>

<span data-ttu-id="38fbe-205">To run the simulated device and back-end applications, you need the device and service connection strings.</span><span class="sxs-lookup"><span data-stu-id="38fbe-205">To run the simulated device and back-end applications, you need the device and service connection strings.</span></span> <span data-ttu-id="38fbe-206">You made a note of the connection strings when you created the resources at the start of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="38fbe-206">You made a note of the connection strings when you created the resources at the start of this tutorial.</span></span>

<span data-ttu-id="38fbe-207">To run the simulated device application, open a shell or command prompt window and navigate to the **iot-hub/Tutorials/DeviceTwins** folder in the Node.js project you downloaded.</span><span class="sxs-lookup"><span data-stu-id="38fbe-207">To run the simulated device application, open a shell or command prompt window and navigate to the **iot-hub/Tutorials/DeviceTwins** folder in the Node.js project you downloaded.</span></span> <span data-ttu-id="38fbe-208">Then run the following commands:</span><span class="sxs-lookup"><span data-stu-id="38fbe-208">Then run the following commands:</span></span>

```cmd/sh
npm install
node SimulatedDevice.js "{your device connection string}"
```

<span data-ttu-id="38fbe-209">To run the back-end application, open another shell or command prompt window.</span><span class="sxs-lookup"><span data-stu-id="38fbe-209">To run the back-end application, open another shell or command prompt window.</span></span> <span data-ttu-id="38fbe-210">Then navigate to the **iot-hub/Tutorials/DeviceTwins** folder in the Node.js project you downloaded.</span><span class="sxs-lookup"><span data-stu-id="38fbe-210">Then navigate to the **iot-hub/Tutorials/DeviceTwins** folder in the Node.js project you downloaded.</span></span> <span data-ttu-id="38fbe-211">Then run the following commands:</span><span class="sxs-lookup"><span data-stu-id="38fbe-211">Then run the following commands:</span></span>

```cmd/sh
npm install
node ServiceClient.js "{your service connection string}"
```

<span data-ttu-id="38fbe-212">The following screenshot shows the output from the simulated device application and highlights how it sends a reported property update to your hub:</span><span class="sxs-lookup"><span data-stu-id="38fbe-212">The following screenshot shows the output from the simulated device application and highlights how it sends a reported property update to your hub:</span></span>

![Simulated device](./media/tutorial-device-twins/SimulatedDevice2.png)

<span data-ttu-id="38fbe-214">The following screenshot shows the output from the back-end application and highlights how it receieves and processes a reported property update from a device:</span><span class="sxs-lookup"><span data-stu-id="38fbe-214">The following screenshot shows the output from the back-end application and highlights how it receieves and processes a reported property update from a device:</span></span>

![Back-end application](./media/tutorial-device-twins/BackEnd2.png)

## <a name="clean-up-resources"></a><span data-ttu-id="38fbe-216">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="38fbe-216">Clean up resources</span></span>

<span data-ttu-id="38fbe-217">If you plan to complete the next tutorial, leave the resource group and IoT hub and reuse them later.</span><span class="sxs-lookup"><span data-stu-id="38fbe-217">If you plan to complete the next tutorial, leave the resource group and IoT hub and reuse them later.</span></span>

<span data-ttu-id="38fbe-218">If you don't need the IoT hub any longer, delete it and the resource group in the portal.</span><span class="sxs-lookup"><span data-stu-id="38fbe-218">If you don't need the IoT hub any longer, delete it and the resource group in the portal.</span></span> <span data-ttu-id="38fbe-219">To do so, select the **tutorial-iot-hub-rg** resource group that contains your IoT hub and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="38fbe-219">To do so, select the **tutorial-iot-hub-rg** resource group that contains your IoT hub and click **Delete**.</span></span>

<span data-ttu-id="38fbe-220">Alternatively, use the CLI:</span><span class="sxs-lookup"><span data-stu-id="38fbe-220">Alternatively, use the CLI:</span></span>

```azurecli-interactive
# Delete your resource group and its contents
az group delete --name tutorial-iot-hub-rg
```

## <a name="next-steps"></a><span data-ttu-id="38fbe-221">Next steps</span><span class="sxs-lookup"><span data-stu-id="38fbe-221">Next steps</span></span>

<span data-ttu-id="38fbe-222">In this tutorial, you learned how to synchronize state information between your devices and your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="38fbe-222">In this tutorial, you learned how to synchronize state information between your devices and your IoT hub.</span></span> <span data-ttu-id="38fbe-223">Advance to the next tutorial to learn how to use device twins to implement a firmware update process.</span><span class="sxs-lookup"><span data-stu-id="38fbe-223">Advance to the next tutorial to learn how to use device twins to implement a firmware update process.</span></span>

> [!div class="nextstepaction"]
[<span data-ttu-id="38fbe-224">Implement a device firmware update process</span><span class="sxs-lookup"><span data-stu-id="38fbe-224">Implement a device firmware update process</span></span>](tutorial-firmware-update.md)
