---
title: Update device firmware through Azure IoT Hub | Microsoft Docs
description: Implement a device firmware update process using jobs and device twins.
services: iot-hub
author: dominicbetts
manager: timlt
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/21/2018
ms.author: dobett
ms.custom: mvc
ms.openlocfilehash: bc1887ef3cdbc56732317aea15be7a618c35847e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969298"
---
# <a name="tutorial-implement-a-device-firmware-update-process"></a><span data-ttu-id="893bc-103">Tutorial: Implement a device firmware update process</span><span class="sxs-lookup"><span data-stu-id="893bc-103">Tutorial: Implement a device firmware update process</span></span>

<span data-ttu-id="893bc-104">You may need to update the firmware on the devices connected to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="893bc-104">You may need to update the firmware on the devices connected to your IoT hub.</span></span> <span data-ttu-id="893bc-105">For example, you might want to add new features to the firmware or apply security patches.</span><span class="sxs-lookup"><span data-stu-id="893bc-105">For example, you might want to add new features to the firmware or apply security patches.</span></span> <span data-ttu-id="893bc-106">In many IoT scenarios, it's impractical to physically visit and then manually apply firmware updates to your devices.</span><span class="sxs-lookup"><span data-stu-id="893bc-106">In many IoT scenarios, it's impractical to physically visit and then manually apply firmware updates to your devices.</span></span> <span data-ttu-id="893bc-107">This tutorial shows how you can start and monitor the firmware update process remotely through a back-end application connected to your hub.</span><span class="sxs-lookup"><span data-stu-id="893bc-107">This tutorial shows how you can start and monitor the firmware update process remotely through a back-end application connected to your hub.</span></span>

<span data-ttu-id="893bc-108">To create and monitor the firmware update process, the back-end application in this tutorial creates a _configuration_ in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="893bc-108">To create and monitor the firmware update process, the back-end application in this tutorial creates a _configuration_ in your IoT hub.</span></span> <span data-ttu-id="893bc-109">IoT Hub [automatic device management](iot-hub-auto-device-config.md) uses this configuration to update a set of _device twin desired properties_ on all your chiller devices.</span><span class="sxs-lookup"><span data-stu-id="893bc-109">IoT Hub [automatic device management](iot-hub-auto-device-config.md) uses this configuration to update a set of _device twin desired properties_ on all your chiller devices.</span></span> <span data-ttu-id="893bc-110">The desired properties specify the details of the firmware update that's required.</span><span class="sxs-lookup"><span data-stu-id="893bc-110">The desired properties specify the details of the firmware update that's required.</span></span> <span data-ttu-id="893bc-111">While the chiller devices are running the firmware update process, they report their status to the back-end application using _device twin reported properties_.</span><span class="sxs-lookup"><span data-stu-id="893bc-111">While the chiller devices are running the firmware update process, they report their status to the back-end application using _device twin reported properties_.</span></span> <span data-ttu-id="893bc-112">The back-end application can use the configuration to monitor the reported properties sent from the device and track the firmware update process to completion:</span><span class="sxs-lookup"><span data-stu-id="893bc-112">The back-end application can use the configuration to monitor the reported properties sent from the device and track the firmware update process to completion:</span></span>

![Firmware update process](media/tutorial-firmware-update/Process.png)

<span data-ttu-id="893bc-114">In this tutorial, you complete the following tasks:</span><span class="sxs-lookup"><span data-stu-id="893bc-114">In this tutorial, you complete the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="893bc-115">Create an IoT hub and add a test device to the device identity registry.</span><span class="sxs-lookup"><span data-stu-id="893bc-115">Create an IoT hub and add a test device to the device identity registry.</span></span>
> * <span data-ttu-id="893bc-116">Create a configuration to define the firmware update.</span><span class="sxs-lookup"><span data-stu-id="893bc-116">Create a configuration to define the firmware update.</span></span>
> * <span data-ttu-id="893bc-117">Simulate the firmware update process on a device.</span><span class="sxs-lookup"><span data-stu-id="893bc-117">Simulate the firmware update process on a device.</span></span>
> * <span data-ttu-id="893bc-118">Receive status updates from the device as the firmware update progresses.</span><span class="sxs-lookup"><span data-stu-id="893bc-118">Receive status updates from the device as the firmware update progresses.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="893bc-119">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="893bc-119">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="893bc-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="893bc-120">Prerequisites</span></span>

<span data-ttu-id="893bc-121">The two sample applications you run in this quickstart are written using Node.js.</span><span class="sxs-lookup"><span data-stu-id="893bc-121">The two sample applications you run in this quickstart are written using Node.js.</span></span> <span data-ttu-id="893bc-122">You need Node.js v4.x.x or later on your development machine.</span><span class="sxs-lookup"><span data-stu-id="893bc-122">You need Node.js v4.x.x or later on your development machine.</span></span>

<span data-ttu-id="893bc-123">You can download Node.js for multiple platforms from [nodejs.org](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="893bc-123">You can download Node.js for multiple platforms from [nodejs.org](https://nodejs.org).</span></span>

<span data-ttu-id="893bc-124">You can verify the current version of Node.js on your development machine using the following command:</span><span class="sxs-lookup"><span data-stu-id="893bc-124">You can verify the current version of Node.js on your development machine using the following command:</span></span>

```cmd/sh
node --version
```

<span data-ttu-id="893bc-125">Download the sample Node.js project from https://github.com/Azure-Samples/azure-iot-samples-node/archive/master.zip and extract the ZIP archive.</span><span class="sxs-lookup"><span data-stu-id="893bc-125">Download the sample Node.js project from https://github.com/Azure-Samples/azure-iot-samples-node/archive/master.zip and extract the ZIP archive.</span></span>

## <a name="set-up-azure-resources"></a><span data-ttu-id="893bc-126">Set up Azure resources</span><span class="sxs-lookup"><span data-stu-id="893bc-126">Set up Azure resources</span></span>

<span data-ttu-id="893bc-127">To complete this tutorial, your Azure subscription must have an IoT hub with a device added to the device identity registry.</span><span class="sxs-lookup"><span data-stu-id="893bc-127">To complete this tutorial, your Azure subscription must have an IoT hub with a device added to the device identity registry.</span></span> <span data-ttu-id="893bc-128">The entry in the device identity registry enables the simulated device you run in this tutorial to connect to your hub.</span><span class="sxs-lookup"><span data-stu-id="893bc-128">The entry in the device identity registry enables the simulated device you run in this tutorial to connect to your hub.</span></span>

<span data-ttu-id="893bc-129">If you don't already have an IoT hub set up in your subscription, you can set one up with following CLI script.</span><span class="sxs-lookup"><span data-stu-id="893bc-129">If you don't already have an IoT hub set up in your subscription, you can set one up with following CLI script.</span></span> <span data-ttu-id="893bc-130">This script uses the name **tutorial-iot-hub** for the IoT hub, you should replace this name with your own unique name when you run it.</span><span class="sxs-lookup"><span data-stu-id="893bc-130">This script uses the name **tutorial-iot-hub** for the IoT hub, you should replace this name with your own unique name when you run it.</span></span> <span data-ttu-id="893bc-131">The script creates the resource group and hub in the **Central US** region, which you can change to a region closer to you.</span><span class="sxs-lookup"><span data-stu-id="893bc-131">The script creates the resource group and hub in the **Central US** region, which you can change to a region closer to you.</span></span> <span data-ttu-id="893bc-132">The script retrieves your IoT hub service connection string, which you use in the back-end sample application to connect to your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="893bc-132">The script retrieves your IoT hub service connection string, which you use in the back-end sample application to connect to your IoT hub:</span></span>

```azurecli-interactive
hubname=tutorial-iot-hub
location=centralus

# Install the IoT extension if it's not already installed
az extension add --name azure-cli-iot-ext

# Create a resource group
az group create --name tutorial-iot-hub-rg --location $location

# Create your free-tier IoT Hub. You can only have one free IoT Hub per subscription
az iot hub create --name $hubname --location $location --resource-group tutorial-iot-hub-rg --sku F1

# Make a note of the service connection string, you need it later
az iot hub show-connection-string --hub-name $hub-name -o table

```

<span data-ttu-id="893bc-133">This tutorial uses a simulated device called **MyFirmwareUpdateDevice**.</span><span class="sxs-lookup"><span data-stu-id="893bc-133">This tutorial uses a simulated device called **MyFirmwareUpdateDevice**.</span></span> <span data-ttu-id="893bc-134">The following script adds this device to your device identity registry, sets a tag value, and retrieves its connection string:</span><span class="sxs-lookup"><span data-stu-id="893bc-134">The following script adds this device to your device identity registry, sets a tag value, and retrieves its connection string:</span></span>

```azurecli-interactive
# Set the name of your IoT hub
hubname=tutorial-iot-hub

# Create the device in the identity registry
az iot hub device-identity create --device-id MyFirmwareUpdateDevice --hub-name $hubname --resource-group tutorial-iot-hub-rg

# Add a device type tag
az iot hub device-twin update --device-id MyFirmwareUpdateDevice --hub-name $hubname --set tags='{"devicetype":"chiller"}'

# Retrieve the device connection string, you need this later
az iot hub device-identity show-connection-string --device-id MyFirmwareUpdateDevice --hub-name $hubname --resource-group tutorial-iot-hub-rg -o table

```

<span data-ttu-id="893bc-135">If you run these commands at a Windows command prompt or Powershell prompt, see the [azure-iot-cli-extension tips](https://github.com/Azure/azure-iot-cli-extension/wiki/Tips
) page for information about how to quote JSON strings.</span><span class="sxs-lookup"><span data-stu-id="893bc-135">If you run these commands at a Windows command prompt or Powershell prompt, see the [azure-iot-cli-extension tips](https://github.com/Azure/azure-iot-cli-extension/wiki/Tips
) page for information about how to quote JSON strings.</span></span>

## <a name="start-the-firmware-update"></a><span data-ttu-id="893bc-136">Start the firmware update</span><span class="sxs-lookup"><span data-stu-id="893bc-136">Start the firmware update</span></span>

<span data-ttu-id="893bc-137">You create an [automatic device management configuration](iot-hub-auto-device-config.md#create-a-configuration) in the back-end application to begin the firmware update process on all devices tagged with a **devicetype** of chiller.</span><span class="sxs-lookup"><span data-stu-id="893bc-137">You create an [automatic device management configuration](iot-hub-auto-device-config.md#create-a-configuration) in the back-end application to begin the firmware update process on all devices tagged with a **devicetype** of chiller.</span></span> <span data-ttu-id="893bc-138">In this section, you see how to:</span><span class="sxs-lookup"><span data-stu-id="893bc-138">In this section, you see how to:</span></span>

* <span data-ttu-id="893bc-139">Create a configuration from a back-end application.</span><span class="sxs-lookup"><span data-stu-id="893bc-139">Create a configuration from a back-end application.</span></span>
* <span data-ttu-id="893bc-140">Monitor the job to completion.</span><span class="sxs-lookup"><span data-stu-id="893bc-140">Monitor the job to completion.</span></span>

### <a name="use-desired-properties-to-start-the-firmware-upgrade-from-the-back-end-application"></a><span data-ttu-id="893bc-141">Use desired properties to start the firmware upgrade from the back-end application</span><span class="sxs-lookup"><span data-stu-id="893bc-141">Use desired properties to start the firmware upgrade from the back-end application</span></span>

<span data-ttu-id="893bc-142">To view the back-end application code that creates the configuration, navigate to the **iot-hub/Tutorials/FirmwareUpdate** folder in the sample Node.js project you downloaded.</span><span class="sxs-lookup"><span data-stu-id="893bc-142">To view the back-end application code that creates the configuration, navigate to the **iot-hub/Tutorials/FirmwareUpdate** folder in the sample Node.js project you downloaded.</span></span> <span data-ttu-id="893bc-143">Then open the ServiceClient.js file in a text editor.</span><span class="sxs-lookup"><span data-stu-id="893bc-143">Then open the ServiceClient.js file in a text editor.</span></span>

<span data-ttu-id="893bc-144">The back-end application creates the following configuration:</span><span class="sxs-lookup"><span data-stu-id="893bc-144">The back-end application creates the following configuration:</span></span>

[!code-javascript[Automatic device management configuration](~/iot-samples-node/iot-hub/Tutorials/FirmwareUpdate/ServiceClient.js?name=configuration "Automatic device management configuration")]

<span data-ttu-id="893bc-145">The configuration includes the following sections:</span><span class="sxs-lookup"><span data-stu-id="893bc-145">The configuration includes the following sections:</span></span>

* <span data-ttu-id="893bc-146">`content` specifies the firmware desired properties sent to the selected devices.</span><span class="sxs-lookup"><span data-stu-id="893bc-146">`content` specifies the firmware desired properties sent to the selected devices.</span></span>
* <span data-ttu-id="893bc-147">`metrics` specifies the queries to run that report the status of the firmware update.</span><span class="sxs-lookup"><span data-stu-id="893bc-147">`metrics` specifies the queries to run that report the status of the firmware update.</span></span>
* <span data-ttu-id="893bc-148">`targetCondition` selects the devices to receive the firmware update.</span><span class="sxs-lookup"><span data-stu-id="893bc-148">`targetCondition` selects the devices to receive the firmware update.</span></span>
* <span data-ttu-id="893bc-149">`priorty` sets the relative priority of this configuration to other configurations.</span><span class="sxs-lookup"><span data-stu-id="893bc-149">`priorty` sets the relative priority of this configuration to other configurations.</span></span>

<span data-ttu-id="893bc-150">The back-end application uses the following code to create the configuration to set the desired properties:</span><span class="sxs-lookup"><span data-stu-id="893bc-150">The back-end application uses the following code to create the configuration to set the desired properties:</span></span>

[!code-javascript[Create configuration](~/iot-samples-node/iot-hub/Tutorials/FirmwareUpdate/ServiceClient.js?name=createConfiguration "Create configuration")]

<span data-ttu-id="893bc-151">After it creates the configuration, the application monitors the firmware update:</span><span class="sxs-lookup"><span data-stu-id="893bc-151">After it creates the configuration, the application monitors the firmware update:</span></span>

[!code-javascript[Monitor firmware update](~/iot-samples-node/iot-hub/Tutorials/FirmwareUpdate/ServiceClient.js?name=monitorConfiguration "Monitor firmware update")]

<span data-ttu-id="893bc-152">A configuration reports two types of metrics:</span><span class="sxs-lookup"><span data-stu-id="893bc-152">A configuration reports two types of metrics:</span></span>

* <span data-ttu-id="893bc-153">System metrics that report how many devices are targeted and how many devices have the update applied.</span><span class="sxs-lookup"><span data-stu-id="893bc-153">System metrics that report how many devices are targeted and how many devices have the update applied.</span></span>
* <span data-ttu-id="893bc-154">Custom metrics generated by the queries you add to the configuration.</span><span class="sxs-lookup"><span data-stu-id="893bc-154">Custom metrics generated by the queries you add to the configuration.</span></span> <span data-ttu-id="893bc-155">In this tutorial, the queries report how many devices are at each stage of the update process.</span><span class="sxs-lookup"><span data-stu-id="893bc-155">In this tutorial, the queries report how many devices are at each stage of the update process.</span></span>

### <a name="respond-to-the-firmware-upgrade-request-on-the-device"></a><span data-ttu-id="893bc-156">Respond to the firmware upgrade request on the device</span><span class="sxs-lookup"><span data-stu-id="893bc-156">Respond to the firmware upgrade request on the device</span></span>

<span data-ttu-id="893bc-157">To view the simulated device code that handles the firmware desired properties sent from the back-end application, navigate to the **iot-hub/Tutorials/FirmwareUpdate** folder in the sample Node.js project you downloaded.</span><span class="sxs-lookup"><span data-stu-id="893bc-157">To view the simulated device code that handles the firmware desired properties sent from the back-end application, navigate to the **iot-hub/Tutorials/FirmwareUpdate** folder in the sample Node.js project you downloaded.</span></span> <span data-ttu-id="893bc-158">Then open the SimulatedDevice.js file in a text editor.</span><span class="sxs-lookup"><span data-stu-id="893bc-158">Then open the SimulatedDevice.js file in a text editor.</span></span>

<span data-ttu-id="893bc-159">The simulated device application creates a handler for updates to the **properties.desired.firmware** desired properties in the device twin.</span><span class="sxs-lookup"><span data-stu-id="893bc-159">The simulated device application creates a handler for updates to the **properties.desired.firmware** desired properties in the device twin.</span></span> <span data-ttu-id="893bc-160">In the handler, it carries out some basic checks on the desired properties before launching the update process:</span><span class="sxs-lookup"><span data-stu-id="893bc-160">In the handler, it carries out some basic checks on the desired properties before launching the update process:</span></span>

[!code-javascript[Handle desired property update](~/iot-samples-node/iot-hub/Tutorials/FirmwareUpdate/SimulatedDevice.js?name=initiateUpdate "Handle desired property update")]

## <a name="update-the-firmware"></a><span data-ttu-id="893bc-161">Update the firmware</span><span class="sxs-lookup"><span data-stu-id="893bc-161">Update the firmware</span></span>

<span data-ttu-id="893bc-162">The **initiateFirmwareUpdateFlow** function runs the update.</span><span class="sxs-lookup"><span data-stu-id="893bc-162">The **initiateFirmwareUpdateFlow** function runs the update.</span></span> <span data-ttu-id="893bc-163">This function uses the **waterfall** function to run the phases of the update process in sequence.</span><span class="sxs-lookup"><span data-stu-id="893bc-163">This function uses the **waterfall** function to run the phases of the update process in sequence.</span></span> <span data-ttu-id="893bc-164">In this example, the firmware update has four phases.</span><span class="sxs-lookup"><span data-stu-id="893bc-164">In this example, the firmware update has four phases.</span></span> <span data-ttu-id="893bc-165">The first phase downloads the image, the second phase verifies the image using a checksum, the third phase applies the image, and the last phase reboots the device:</span><span class="sxs-lookup"><span data-stu-id="893bc-165">The first phase downloads the image, the second phase verifies the image using a checksum, the third phase applies the image, and the last phase reboots the device:</span></span>

[!code-javascript[Firmware update flow](~/iot-samples-node/iot-hub/Tutorials/FirmwareUpdate/SimulatedDevice.js?name=firmwareupdateflow "Firmware update flow")]

<span data-ttu-id="893bc-166">During the update process, the simulated device reports on progress using reported properties:</span><span class="sxs-lookup"><span data-stu-id="893bc-166">During the update process, the simulated device reports on progress using reported properties:</span></span>

[!code-javascript[Reported properties](~/iot-samples-node/iot-hub/Tutorials/FirmwareUpdate/SimulatedDevice.js?name=reportedProperties "Reported properties")]

<span data-ttu-id="893bc-167">The following snippet shows the implementation of the download phase.</span><span class="sxs-lookup"><span data-stu-id="893bc-167">The following snippet shows the implementation of the download phase.</span></span> <span data-ttu-id="893bc-168">During the download phase, the simulated device uses reported properties to send status information to the back-end application:</span><span class="sxs-lookup"><span data-stu-id="893bc-168">During the download phase, the simulated device uses reported properties to send status information to the back-end application:</span></span>

[!code-javascript[Download image phase](~/iot-samples-node/iot-hub/Tutorials/FirmwareUpdate/SimulatedDevice.js?name=downloadimagephase "Download image phase")]

## <a name="run-the-sample"></a><span data-ttu-id="893bc-169">Run the sample</span><span class="sxs-lookup"><span data-stu-id="893bc-169">Run the sample</span></span>

<span data-ttu-id="893bc-170">In this section, you run two sample applications to observe as a back-end application creates the configuration to manage the firmware update process on the simulated device.</span><span class="sxs-lookup"><span data-stu-id="893bc-170">In this section, you run two sample applications to observe as a back-end application creates the configuration to manage the firmware update process on the simulated device.</span></span>

<span data-ttu-id="893bc-171">To run the simulated device and back-end applications, you need the device and service connection strings.</span><span class="sxs-lookup"><span data-stu-id="893bc-171">To run the simulated device and back-end applications, you need the device and service connection strings.</span></span> <span data-ttu-id="893bc-172">You made a note of the connection strings when you created the resources at the start of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="893bc-172">You made a note of the connection strings when you created the resources at the start of this tutorial.</span></span>

<span data-ttu-id="893bc-173">To run the simulated device application, open a shell or command prompt window and navigate to the **iot-hub/Tutorials/FirmwareUpdate** folder in the Node.js project you downloaded.</span><span class="sxs-lookup"><span data-stu-id="893bc-173">To run the simulated device application, open a shell or command prompt window and navigate to the **iot-hub/Tutorials/FirmwareUpdate** folder in the Node.js project you downloaded.</span></span> <span data-ttu-id="893bc-174">Then run the following commands:</span><span class="sxs-lookup"><span data-stu-id="893bc-174">Then run the following commands:</span></span>

```cmd/sh
npm install
node SimulatedDevice.js "{your device connection string}"
```

<span data-ttu-id="893bc-175">To run the back-end application, open another shell or command prompt window.</span><span class="sxs-lookup"><span data-stu-id="893bc-175">To run the back-end application, open another shell or command prompt window.</span></span> <span data-ttu-id="893bc-176">Then navigate to the **iot-hub/Tutorials/FirmwareUpdate** folder in the Node.js project you downloaded.</span><span class="sxs-lookup"><span data-stu-id="893bc-176">Then navigate to the **iot-hub/Tutorials/FirmwareUpdate** folder in the Node.js project you downloaded.</span></span> <span data-ttu-id="893bc-177">Then run the following commands:</span><span class="sxs-lookup"><span data-stu-id="893bc-177">Then run the following commands:</span></span>

```cmd/sh
npm install
node ServiceClient.js "{your service connection string}"
```

<span data-ttu-id="893bc-178">The following screenshot shows the output from the simulated device application and shows how it responds to the firmware desired properties update from the back-end application:</span><span class="sxs-lookup"><span data-stu-id="893bc-178">The following screenshot shows the output from the simulated device application and shows how it responds to the firmware desired properties update from the back-end application:</span></span>

![Simulated device](./media/tutorial-firmware-update/SimulatedDevice.png)

<span data-ttu-id="893bc-180">The following screenshot shows the output from the back-end application and highlights how it creates the configuration to update the firmware desired properties:</span><span class="sxs-lookup"><span data-stu-id="893bc-180">The following screenshot shows the output from the back-end application and highlights how it creates the configuration to update the firmware desired properties:</span></span>

![Back-end application](./media/tutorial-firmware-update/BackEnd1.png)

<span data-ttu-id="893bc-182">The following screenshot shows the output from the back-end application and highlights how it monitors the firmware update metrics from the simulated device:</span><span class="sxs-lookup"><span data-stu-id="893bc-182">The following screenshot shows the output from the back-end application and highlights how it monitors the firmware update metrics from the simulated device:</span></span>

![Back-end application](./media/tutorial-firmware-update/BackEnd2.png)

<span data-ttu-id="893bc-184">Because of latency in the IoT Hub device identity registry, you may not see every status update sent to the back-end application.</span><span class="sxs-lookup"><span data-stu-id="893bc-184">Because of latency in the IoT Hub device identity registry, you may not see every status update sent to the back-end application.</span></span> <span data-ttu-id="893bc-185">You can also view the metrics in the portal in the **Automatic device management -> IoT device configuration** section of your IoT hub:</span><span class="sxs-lookup"><span data-stu-id="893bc-185">You can also view the metrics in the portal in the **Automatic device management -> IoT device configuration** section of your IoT hub:</span></span>

![View configuration in portal](./media/tutorial-firmware-update/portalview.png)

## <a name="clean-up-resources"></a><span data-ttu-id="893bc-187">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="893bc-187">Clean up resources</span></span>

<span data-ttu-id="893bc-188">If you plan to complete the next tutorial, leave the resource group and IoT hub and reuse them later.</span><span class="sxs-lookup"><span data-stu-id="893bc-188">If you plan to complete the next tutorial, leave the resource group and IoT hub and reuse them later.</span></span>

<span data-ttu-id="893bc-189">If you don't need the IoT hub any longer, delete it and the resource group in the portal.</span><span class="sxs-lookup"><span data-stu-id="893bc-189">If you don't need the IoT hub any longer, delete it and the resource group in the portal.</span></span> <span data-ttu-id="893bc-190">To do so, select the **tutorial-iot-hub-rg** resource group that contains your IoT hub and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="893bc-190">To do so, select the **tutorial-iot-hub-rg** resource group that contains your IoT hub and click **Delete**.</span></span>

<span data-ttu-id="893bc-191">Alternatively, use the CLI:</span><span class="sxs-lookup"><span data-stu-id="893bc-191">Alternatively, use the CLI:</span></span>

```azurecli-interactive
# Delete your resource group and its contents
az group delete --name tutorial-iot-hub-rg
```

## <a name="next-steps"></a><span data-ttu-id="893bc-192">Next steps</span><span class="sxs-lookup"><span data-stu-id="893bc-192">Next steps</span></span>

<span data-ttu-id="893bc-193">In this tutorial, you learned how to implement a firmware update process for your connected devices.</span><span class="sxs-lookup"><span data-stu-id="893bc-193">In this tutorial, you learned how to implement a firmware update process for your connected devices.</span></span> <span data-ttu-id="893bc-194">Advance to the next tutorial to learn how use Azure IoT Hub portal tools and Azure CLI commands to test device connectivity.</span><span class="sxs-lookup"><span data-stu-id="893bc-194">Advance to the next tutorial to learn how use Azure IoT Hub portal tools and Azure CLI commands to test device connectivity.</span></span>

> [!div class="nextstepaction"]
[<span data-ttu-id="893bc-195">Use a simulated device to test connectivity with your IoT hub</span><span class="sxs-lookup"><span data-stu-id="893bc-195">Use a simulated device to test connectivity with your IoT hub</span></span>](tutorial-connectivity.md)
