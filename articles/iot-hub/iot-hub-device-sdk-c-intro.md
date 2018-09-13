---
title: The Azure IoT device SDK for C | Microsoft Docs
description: Get started with the Azure IoT device SDK for C and learn how to create device apps that communicate with an IoT hub.
services: iot-hub
documentationcenter: ''
author: olivierbloch
manager: timlt
editor: ''
ms.assetid: e448b061-6bdd-470a-a527-15ec03cca7b9
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/20/2017
ms.author: obloch
ms.openlocfilehash: a4cfbb48abde3ee46138d4b7822c15ca2a44e77c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549811"
---
# <a name="azure-iot-device-sdk-for-c"></a><span data-ttu-id="8b3ca-103">Azure IoT device SDK for C</span><span class="sxs-lookup"><span data-stu-id="8b3ca-103">Azure IoT device SDK for C</span></span>

<span data-ttu-id="8b3ca-104">The **Azure IoT device SDK** is a set of libraries designed to simplify the process of sending messages to and receiving messages from the **Azure IoT Hub** service.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-104">The **Azure IoT device SDK** is a set of libraries designed to simplify the process of sending messages to and receiving messages from the **Azure IoT Hub** service.</span></span> <span data-ttu-id="8b3ca-105">There are different variations of the SDK, each targeting a specific platform, but this article describes the **Azure IoT device SDK for C**.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-105">There are different variations of the SDK, each targeting a specific platform, but this article describes the **Azure IoT device SDK for C**.</span></span>

<span data-ttu-id="8b3ca-106">The Azure IoT device SDK for C is written in ANSI C (C99) to maximize portability.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-106">The Azure IoT device SDK for C is written in ANSI C (C99) to maximize portability.</span></span> <span data-ttu-id="8b3ca-107">This feature makes the libraries well-suited to operate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-107">This feature makes the libraries well-suited to operate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span></span>

<span data-ttu-id="8b3ca-108">There are a broad range of platforms on which the SDK has been tested (see the [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span><span class="sxs-lookup"><span data-stu-id="8b3ca-108">There are a broad range of platforms on which the SDK has been tested (see the [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span></span> <span data-ttu-id="8b3ca-109">Although this article includes walkthroughs of sample code running on the Windows platform, the code described in this article is identical across the range of supported platforms.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-109">Although this article includes walkthroughs of sample code running on the Windows platform, the code described in this article is identical across the range of supported platforms.</span></span>

<span data-ttu-id="8b3ca-110">This article introduces you to the architecture of the Azure IoT device SDK for C. It demonstrates how to initialize the device library, send data to IoT Hub, and receive messages from it.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-110">This article introduces you to the architecture of the Azure IoT device SDK for C. It demonstrates how to initialize the device library, send data to IoT Hub, and receive messages from it.</span></span> <span data-ttu-id="8b3ca-111">The information in this article should be enough to get started using the SDK, but also provides pointers to additional information about the libraries.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-111">The information in this article should be enough to get started using the SDK, but also provides pointers to additional information about the libraries.</span></span>

## <a name="sdk-architecture"></a><span data-ttu-id="8b3ca-112">SDK architecture</span><span class="sxs-lookup"><span data-stu-id="8b3ca-112">SDK architecture</span></span>

<span data-ttu-id="8b3ca-113">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="8b3ca-113">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

<span data-ttu-id="8b3ca-114">The latest version of the libraries can be found in the **master** branch of the repository:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-114">The latest version of the libraries can be found in the **master** branch of the repository:</span></span>

  ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* <span data-ttu-id="8b3ca-115">The core implementation of the SDK is in the **iothub\_client** folder that contains the implementation of the lowest API layer in the SDK: the **IoTHubClient** library.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-115">The core implementation of the SDK is in the **iothub\_client** folder that contains the implementation of the lowest API layer in the SDK: the **IoTHubClient** library.</span></span> <span data-ttu-id="8b3ca-116">The **IoTHubClient** library contains APIs implementing raw messaging for sending messages to IoT Hub and receiving messages from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-116">The **IoTHubClient** library contains APIs implementing raw messaging for sending messages to IoT Hub and receiving messages from IoT Hub.</span></span> <span data-ttu-id="8b3ca-117">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-117">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span></span>
* <span data-ttu-id="8b3ca-118">The **serializer** folder contains helper functions and samples that show you how to serialize data before sending to Azure IoT Hub using the client library.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-118">The **serializer** folder contains helper functions and samples that show you how to serialize data before sending to Azure IoT Hub using the client library.</span></span> <span data-ttu-id="8b3ca-119">The use of the serializer is not mandatory and is provided as a convenience.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-119">The use of the serializer is not mandatory and is provided as a convenience.</span></span> <span data-ttu-id="8b3ca-120">To use the **serializer** library, you define a model that specifies the data to send to IoT Hub and the messages you expect to receive from it.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-120">To use the **serializer** library, you define a model that specifies the data to send to IoT Hub and the messages you expect to receive from it.</span></span> <span data-ttu-id="8b3ca-121">Once the model is defined, the SDK provides you with an API surface that enables you to easily work with device-to-cloud and cloud-to-device messages without worrying about the serialization details.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-121">Once the model is defined, the SDK provides you with an API surface that enables you to easily work with device-to-cloud and cloud-to-device messages without worrying about the serialization details.</span></span> <span data-ttu-id="8b3ca-122">The library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-122">The library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span></span>
* <span data-ttu-id="8b3ca-123">The **IoTHubClient** library depends on other open source libraries:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-123">The **IoTHubClient** library depends on other open source libraries:</span></span>
  * <span data-ttu-id="8b3ca-124">The [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-124">The [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span></span>
  * <span data-ttu-id="8b3ca-125">The [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-125">The [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span></span>
  * <span data-ttu-id="8b3ca-126">The [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing the MQTT protocol and optimized for resource constrained devices.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-126">The [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing the MQTT protocol and optimized for resource constrained devices.</span></span>

<span data-ttu-id="8b3ca-127">Use of these libraries is easier to understand by looking at example code.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-127">Use of these libraries is easier to understand by looking at example code.</span></span> <span data-ttu-id="8b3ca-128">The following sections walk you through several of the sample applications that are included in the SDK.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-128">The following sections walk you through several of the sample applications that are included in the SDK.</span></span> <span data-ttu-id="8b3ca-129">This walkthrough should give you a good feel for the various capabilities of the architectural layers of the SDK and an introduction to how the APIs work.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-129">This walkthrough should give you a good feel for the various capabilities of the architectural layers of the SDK and an introduction to how the APIs work.</span></span>

## <a name="before-you-run-the-samples"></a><span data-ttu-id="8b3ca-130">Before you run the samples</span><span class="sxs-lookup"><span data-stu-id="8b3ca-130">Before you run the samples</span></span>

<span data-ttu-id="8b3ca-131">Before you can run the samples in the Azure IoT device SDK for C, you must [create an instance of the IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-131">Before you can run the samples in the Azure IoT device SDK for C, you must [create an instance of the IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span></span> <span data-ttu-id="8b3ca-132">Then complete the following tasks:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-132">Then complete the following tasks:</span></span>

* <span data-ttu-id="8b3ca-133">Prepare your development environment</span><span class="sxs-lookup"><span data-stu-id="8b3ca-133">Prepare your development environment</span></span>
* <span data-ttu-id="8b3ca-134">Obtain device credentials.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-134">Obtain device credentials.</span></span>

### <a name="prepare-your-development-environment"></a><span data-ttu-id="8b3ca-135">Prepare your development environment</span><span class="sxs-lookup"><span data-stu-id="8b3ca-135">Prepare your development environment</span></span>

<span data-ttu-id="8b3ca-136">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and the samples use these packages when available.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-136">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and the samples use these packages when available.</span></span> <span data-ttu-id="8b3ca-137">In some cases, you need to compile the SDK for or on your device.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-137">In some cases, you need to compile the SDK for or on your device.</span></span> <span data-ttu-id="8b3ca-138">If you need to compile the SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in the GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-138">If you need to compile the SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in the GitHub repository.</span></span>

<span data-ttu-id="8b3ca-139">To obtain the sample application code, download a copy of the SDK from GitHub.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-139">To obtain the sample application code, download a copy of the SDK from GitHub.</span></span> <span data-ttu-id="8b3ca-140">Get your copy of the source from the **master** branch of the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span><span class="sxs-lookup"><span data-stu-id="8b3ca-140">Get your copy of the source from the **master** branch of the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span></span>


### <a name="obtain-the-device-credentials"></a><span data-ttu-id="8b3ca-141">Obtain the device credentials</span><span class="sxs-lookup"><span data-stu-id="8b3ca-141">Obtain the device credentials</span></span>

<span data-ttu-id="8b3ca-142">Now that you have the sample source code, the next thing to do is to get a set of device credentials.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-142">Now that you have the sample source code, the next thing to do is to get a set of device credentials.</span></span> <span data-ttu-id="8b3ca-143">For a device to be able to access an IoT hub, you must first add the device to the IoT Hub identity registry.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-143">For a device to be able to access an IoT hub, you must first add the device to the IoT Hub identity registry.</span></span> <span data-ttu-id="8b3ca-144">When you add your device, you get a set of device credentials that you need for the device to be able to connect to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-144">When you add your device, you get a set of device credentials that you need for the device to be able to connect to the IoT hub.</span></span> <span data-ttu-id="8b3ca-145">The sample applications discussed in the next section expect these credentials in the form of a **device connection string**.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-145">The sample applications discussed in the next section expect these credentials in the form of a **device connection string**.</span></span>

<span data-ttu-id="8b3ca-146">There are several open source tools to help you manage your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-146">There are several open source tools to help you manage your IoT hub.</span></span>

* <span data-ttu-id="8b3ca-147">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="8b3ca-147">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>
* <span data-ttu-id="8b3ca-148">A cross-platform node.js CLI tool called [iothub-explorer](https://github.com/azure/iothub-explorer).</span><span class="sxs-lookup"><span data-stu-id="8b3ca-148">A cross-platform node.js CLI tool called [iothub-explorer](https://github.com/azure/iothub-explorer).</span></span>

<span data-ttu-id="8b3ca-149">This tutorial uses the graphical *device explorer* tool.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-149">This tutorial uses the graphical *device explorer* tool.</span></span> <span data-ttu-id="8b3ca-150">You can also use the *iothub-explorer* tool if you prefer to use a CLI tool.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-150">You can also use the *iothub-explorer* tool if you prefer to use a CLI tool.</span></span>

<span data-ttu-id="8b3ca-151">The device explorer tool uses the Azure IoT service libraries to perform various functions on IoT Hub, including adding devices.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-151">The device explorer tool uses the Azure IoT service libraries to perform various functions on IoT Hub, including adding devices.</span></span> <span data-ttu-id="8b3ca-152">If you use the device explorer tool to add a device, you get a connection string for your device.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-152">If you use the device explorer tool to add a device, you get a connection string for your device.</span></span> <span data-ttu-id="8b3ca-153">You need this connection string to run the sample applications.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-153">You need this connection string to run the sample applications.</span></span>

<span data-ttu-id="8b3ca-154">If you're not familiar with the device explorer tool, the following procedure describes how to use it to add a device and obtain a device connection string.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-154">If you're not familiar with the device explorer tool, the following procedure describes how to use it to add a device and obtain a device connection string.</span></span>

<span data-ttu-id="8b3ca-155">To install the device explorer tool, see [How to use the Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="8b3ca-155">To install the device explorer tool, see [How to use the Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>

<span data-ttu-id="8b3ca-156">When you run the program, you see this interface:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-156">When you run the program, you see this interface:</span></span>

  ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

<span data-ttu-id="8b3ca-157">Enter your **IoT Hub Connection String** in the first field and click **Update**.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-157">Enter your **IoT Hub Connection String** in the first field and click **Update**.</span></span> <span data-ttu-id="8b3ca-158">This step configures the tool so that it can communicate with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-158">This step configures the tool so that it can communicate with IoT Hub.</span></span>

<span data-ttu-id="8b3ca-159">When the IoT Hub connection string is configured, click the **Management** tab:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-159">When the IoT Hub connection string is configured, click the **Management** tab:</span></span>

  ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

<span data-ttu-id="8b3ca-160">This tab is where you manage the devices registered in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-160">This tab is where you manage the devices registered in your IoT hub.</span></span>

<span data-ttu-id="8b3ca-161">You create a device by clicking the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-161">You create a device by clicking the **Create** button.</span></span> <span data-ttu-id="8b3ca-162">A dialog displays with a set of pre-populated keys (primary and secondary).</span><span class="sxs-lookup"><span data-stu-id="8b3ca-162">A dialog displays with a set of pre-populated keys (primary and secondary).</span></span> <span data-ttu-id="8b3ca-163">Enter a **Device ID** and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-163">Enter a **Device ID** and then click **Create**.</span></span>

  ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

<span data-ttu-id="8b3ca-164">When the device is created, the Devices list updates with all the registered devices, including the one you just created.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-164">When the device is created, the Devices list updates with all the registered devices, including the one you just created.</span></span> <span data-ttu-id="8b3ca-165">If you right-click your new device, you see this menu:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-165">If you right-click your new device, you see this menu:</span></span>

  ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

<span data-ttu-id="8b3ca-166">If you choose **Copy connection string for selected device**, the device connection string is copied to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-166">If you choose **Copy connection string for selected device**, the device connection string is copied to the clipboard.</span></span> <span data-ttu-id="8b3ca-167">Keep a copy of the device connection string.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-167">Keep a copy of the device connection string.</span></span> <span data-ttu-id="8b3ca-168">You need it when running the sample applications described in the following sections.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-168">You need it when running the sample applications described in the following sections.</span></span>

<span data-ttu-id="8b3ca-169">When you've completed the steps above, you're ready to start running some code.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-169">When you've completed the steps above, you're ready to start running some code.</span></span> <span data-ttu-id="8b3ca-170">Both samples have a constant at the top of the main source file that enables you to enter a connection string.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-170">Both samples have a constant at the top of the main source file that enables you to enter a connection string.</span></span> <span data-ttu-id="8b3ca-171">For example, the corresponding line from the **iothub\_client\_sample\_mqtt** application appears as follows.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-171">For example, the corresponding line from the **iothub\_client\_sample\_mqtt** application appears as follows.</span></span>

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-the-iothubclient-library"></a><span data-ttu-id="8b3ca-172">Use the IoTHubClient library</span><span class="sxs-lookup"><span data-stu-id="8b3ca-172">Use the IoTHubClient library</span></span>

<span data-ttu-id="8b3ca-173">Within the **iothub\_client** folder in the [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-173">Within the **iothub\_client** folder in the [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span></span>

<span data-ttu-id="8b3ca-174">The Windows version of the **iothub\_client\_sample\_mqtt** application includes the following Visual Studio solution:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-174">The Windows version of the **iothub\_client\_sample\_mqtt** application includes the following Visual Studio solution:</span></span>

  ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="8b3ca-175">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-175">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="8b3ca-176">This solution contains a single project.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-176">This solution contains a single project.</span></span> <span data-ttu-id="8b3ca-177">There are four NuGet packages installed in this solution:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-177">There are four NuGet packages installed in this solution:</span></span>

* <span data-ttu-id="8b3ca-178">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="8b3ca-178">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="8b3ca-179">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="8b3ca-179">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="8b3ca-180">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="8b3ca-180">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="8b3ca-181">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="8b3ca-181">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="8b3ca-182">You always need the **Microsoft.Azure.C.SharedUtility** package when you are working with the SDK.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-182">You always need the **Microsoft.Azure.C.SharedUtility** package when you are working with the SDK.</span></span> <span data-ttu-id="8b3ca-183">This sample uses the MQTT protocol, therefore you must include the **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTP).</span><span class="sxs-lookup"><span data-stu-id="8b3ca-183">This sample uses the MQTT protocol, therefore you must include the **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTP).</span></span> <span data-ttu-id="8b3ca-184">Because the sample uses the **IoTHubClient** library, you must also include the **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-184">Because the sample uses the **IoTHubClient** library, you must also include the **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span></span>

<span data-ttu-id="8b3ca-185">You can find the implementation for the sample application in the **iothub\_client\_sample\_mqtt.c** source file.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-185">You can find the implementation for the sample application in the **iothub\_client\_sample\_mqtt.c** source file.</span></span>

<span data-ttu-id="8b3ca-186">The following steps use this sample application to walk you through what's required to use the **IoTHubClient** library.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-186">The following steps use this sample application to walk you through what's required to use the **IoTHubClient** library.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="8b3ca-187">Initialize the library</span><span class="sxs-lookup"><span data-stu-id="8b3ca-187">Initialize the library</span></span>

> [!NOTE]
> <span data-ttu-id="8b3ca-188">Before you start working with the libraries, you may need to perform some platform-specific initialization.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-188">Before you start working with the libraries, you may need to perform some platform-specific initialization.</span></span> <span data-ttu-id="8b3ca-189">For example, if you plan to use AMQP on Linux you must initialize the OpenSSL library.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-189">For example, if you plan to use AMQP on Linux you must initialize the OpenSSL library.</span></span> <span data-ttu-id="8b3ca-190">The samples in the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call the utility function **platform\_init** when the client starts and call the **platform\_deinit** function before exiting.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-190">The samples in the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call the utility function **platform\_init** when the client starts and call the **platform\_deinit** function before exiting.</span></span> <span data-ttu-id="8b3ca-191">These functions are declared in the platform.h header file.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-191">These functions are declared in the platform.h header file.</span></span> <span data-ttu-id="8b3ca-192">Examine the definitions of these functions for your target platform in the [repository](https://github.com/Azure/azure-iot-sdk-c) to determine whether you need to include any platform-specific initialization code in your client.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-192">Examine the definitions of these functions for your target platform in the [repository](https://github.com/Azure/azure-iot-sdk-c) to determine whether you need to include any platform-specific initialization code in your client.</span></span>

<span data-ttu-id="8b3ca-193">To start working with the libraries, first allocate an IoT Hub client handle:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-193">To start working with the libraries, first allocate an IoT Hub client handle:</span></span>

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

<span data-ttu-id="8b3ca-194">You pass a copy of the device connection string you obtained from the device explorer tool to this function.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-194">You pass a copy of the device connection string you obtained from the device explorer tool to this function.</span></span> <span data-ttu-id="8b3ca-195">You also designate the communications protocol to use.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-195">You also designate the communications protocol to use.</span></span> <span data-ttu-id="8b3ca-196">This example uses MQTT, but AMQP and HTTP are also options.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-196">This example uses MQTT, but AMQP and HTTP are also options.</span></span>

<span data-ttu-id="8b3ca-197">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling the APIs to send and receive messages to and from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-197">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling the APIs to send and receive messages to and from IoT Hub.</span></span>

### <a name="send-messages"></a><span data-ttu-id="8b3ca-198">Send messages</span><span class="sxs-lookup"><span data-stu-id="8b3ca-198">Send messages</span></span>

<span data-ttu-id="8b3ca-199">The sample application sets up a loop to send messages to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-199">The sample application sets up a loop to send messages to your IoT hub.</span></span> <span data-ttu-id="8b3ca-200">The following snippet:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-200">The following snippet:</span></span>

- <span data-ttu-id="8b3ca-201">Creates a message.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-201">Creates a message.</span></span>
- <span data-ttu-id="8b3ca-202">Adds a property to the message.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-202">Adds a property to the message.</span></span>
- <span data-ttu-id="8b3ca-203">Sends a message.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-203">Sends a message.</span></span>

<span data-ttu-id="8b3ca-204">First, create a message:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-204">First, create a message:</span></span>

```c
size_t iterator = 0;
do
{
    if (iterator < MESSAGE_COUNT)
    {
        sprintf_s(msgText, sizeof(msgText), "{\"deviceId\":\"myFirstDevice\",\"windSpeed\":%.2f}", avgWindSpeed + (rand() % 4 + 2));
        if ((messages[iterator].messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText))) == NULL)
        {
            (void)printf("ERROR: iotHubMessageHandle is NULL!\r\n");
        }
        else
        {
            messages[iterator].messageTrackingId = iterator;
            MAP_HANDLE propMap = IoTHubMessage_Properties(messages[iterator].messageHandle);
            (void)sprintf_s(propText, sizeof(propText), "PropMsg_%zu", iterator);
            if (Map_AddOrUpdate(propMap, "PropName", propText) != MAP_OK)
            {
                (void)printf("ERROR: Map_AddOrUpdate Failed!\r\n");
            }

            if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messages[iterator].messageHandle, SendConfirmationCallback, &messages[iterator]) != IOTHUB_CLIENT_OK)
            {
                (void)printf("ERROR: IoTHubClient_LL_SendEventAsync..........FAILED!\r\n");
            }
            else
            {
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission to IoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

<span data-ttu-id="8b3ca-205">Every time you send a message, you specify a reference to a callback function that's invoked when the data is sent.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-205">Every time you send a message, you specify a reference to a callback function that's invoked when the data is sent.</span></span> <span data-ttu-id="8b3ca-206">In this example, the callback function is called **SendConfirmationCallback**.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-206">In this example, the callback function is called **SendConfirmationCallback**.</span></span> <span data-ttu-id="8b3ca-207">The following snippet shows this callback function:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-207">The following snippet shows this callback function:</span></span>

```c
static void SendConfirmationCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    EVENT_INSTANCE* eventInstance = (EVENT_INSTANCE*)userContextCallback;
    (void)printf("Confirmation[%d] received for message tracking id = %zu with result = %s\r\n", callbackCounter, eventInstance->messageTrackingId, ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
    /* Some device specific action code goes here... */
    callbackCounter++;
    IoTHubMessage_Destroy(eventInstance->messageHandle);
}
```

<span data-ttu-id="8b3ca-208">Note the call to the **IoTHubMessage\_Destroy** function when you're done with the message.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-208">Note the call to the **IoTHubMessage\_Destroy** function when you're done with the message.</span></span> <span data-ttu-id="8b3ca-209">This function frees the resources allocated when you created the message.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-209">This function frees the resources allocated when you created the message.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="8b3ca-210">Receive messages</span><span class="sxs-lookup"><span data-stu-id="8b3ca-210">Receive messages</span></span>

<span data-ttu-id="8b3ca-211">Receiving a message is an asynchronous operation.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-211">Receiving a message is an asynchronous operation.</span></span> <span data-ttu-id="8b3ca-212">First, you register the callback to invoke when the device receives a message:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-212">First, you register the callback to invoke when the device receives a message:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext) != IOTHUB_CLIENT_OK)
{
    (void)printf("ERROR: IoTHubClient_LL_SetMessageCallback..........FAILED!\r\n");
}
else
{
    (void)printf("IoTHubClient_LL_SetMessageCallback...successful.\r\n");
...
```

<span data-ttu-id="8b3ca-213">The last parameter is a void pointer to whatever you want.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-213">The last parameter is a void pointer to whatever you want.</span></span> <span data-ttu-id="8b3ca-214">In the sample, it's a pointer to an integer but it could be a pointer to a more complex data structure.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-214">In the sample, it's a pointer to an integer but it could be a pointer to a more complex data structure.</span></span> <span data-ttu-id="8b3ca-215">This parameter enables the callback function to operate on shared state with the caller of this function.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-215">This parameter enables the callback function to operate on shared state with the caller of this function.</span></span>

<span data-ttu-id="8b3ca-216">When the device receives a message, the registered callback function is invoked.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-216">When the device receives a message, the registered callback function is invoked.</span></span> <span data-ttu-id="8b3ca-217">This callback function retrieves:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-217">This callback function retrieves:</span></span>

* <span data-ttu-id="8b3ca-218">The message id and correlation id from the message.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-218">The message id and correlation id from the message.</span></span>
* <span data-ttu-id="8b3ca-219">The message content.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-219">The message content.</span></span>
* <span data-ttu-id="8b3ca-220">Any custom properties from the message.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-220">Any custom properties from the message.</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    int* counter = (int*)userContextCallback;
    const char* buffer;
    size_t size;
    MAP_HANDLE mapProperties;
    const char* messageId;
    const char* correlationId;

    // Message properties
    if ((messageId = IoTHubMessage_GetMessageId(message)) == NULL)
    {
        messageId = "<null>";
    }

    if ((correlationId = IoTHubMessage_GetCorrelationId(message)) == NULL)
    {
        correlationId = "<null>";
    }

    // Message content
    if (IoTHubMessage_GetByteArray(message, (const unsigned char**)&buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        (void)printf("unable to retrieve the message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive the work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from the message
    mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                size_t index;

                printf(" Message Properties:\r\n");
                for (index = 0; index < propertyCount; index++)
                {
                    (void)printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                (void)printf("\r\n");
            }
        }
    }

    /* Some device specific action code goes here... */
    (*counter)++;
    return IOTHUBMESSAGE_ACCEPTED;
}
```

<span data-ttu-id="8b3ca-221">Use the **IoTHubMessage\_GetByteArray** function to retrieve the message, which in this example is a string.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-221">Use the **IoTHubMessage\_GetByteArray** function to retrieve the message, which in this example is a string.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="8b3ca-222">Uninitialize the library</span><span class="sxs-lookup"><span data-stu-id="8b3ca-222">Uninitialize the library</span></span>

<span data-ttu-id="8b3ca-223">When you're done sending events and receiving messages, you can uninitialize the IoT library.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-223">When you're done sending events and receiving messages, you can uninitialize the IoT library.</span></span> <span data-ttu-id="8b3ca-224">To do so, issue the following function call:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-224">To do so, issue the following function call:</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="8b3ca-225">This call frees up the resources previously allocated by the **IoTHubClient\_CreateFromConnectionString** function.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-225">This call frees up the resources previously allocated by the **IoTHubClient\_CreateFromConnectionString** function.</span></span>

<span data-ttu-id="8b3ca-226">As you can see, it's easy to send and receive messages with the **IoTHubClient** library.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-226">As you can see, it's easy to send and receive messages with the **IoTHubClient** library.</span></span> <span data-ttu-id="8b3ca-227">The library handles the details of communicating with IoT Hub, including which protocol to use (from the perspective of the developer, this is a simple configuration option).</span><span class="sxs-lookup"><span data-stu-id="8b3ca-227">The library handles the details of communicating with IoT Hub, including which protocol to use (from the perspective of the developer, this is a simple configuration option).</span></span>

<span data-ttu-id="8b3ca-228">The **IoTHubClient** library also provides precise control over how to serialize the data your device sends to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-228">The **IoTHubClient** library also provides precise control over how to serialize the data your device sends to IoT Hub.</span></span> <span data-ttu-id="8b3ca-229">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want to be concerned with.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-229">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want to be concerned with.</span></span> <span data-ttu-id="8b3ca-230">If that's the case, you might consider using the **serializer** library, which is described in the next section.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-230">If that's the case, you might consider using the **serializer** library, which is described in the next section.</span></span>

## <a name="use-the-serializer-library"></a><span data-ttu-id="8b3ca-231">Use the serializer library</span><span class="sxs-lookup"><span data-stu-id="8b3ca-231">Use the serializer library</span></span>

<span data-ttu-id="8b3ca-232">Conceptually the **serializer** library sits on top of the **IoTHubClient** library in the SDK.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-232">Conceptually the **serializer** library sits on top of the **IoTHubClient** library in the SDK.</span></span> <span data-ttu-id="8b3ca-233">It uses the **IoTHubClient** library for the underlying communication with IoT Hub, but it adds modeling capabilities that remove the burden of dealing with message serialization from the developer.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-233">It uses the **IoTHubClient** library for the underlying communication with IoT Hub, but it adds modeling capabilities that remove the burden of dealing with message serialization from the developer.</span></span> <span data-ttu-id="8b3ca-234">How this library works is best demonstrated by an example.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-234">How this library works is best demonstrated by an example.</span></span>

<span data-ttu-id="8b3ca-235">Inside the **serializer** folder in the [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-235">Inside the **serializer** folder in the [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span></span> <span data-ttu-id="8b3ca-236">The Windows version of this sample includes the following Visual Studio solution:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-236">The Windows version of this sample includes the following Visual Studio solution:</span></span>

  ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="8b3ca-237">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-237">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="8b3ca-238">As with the previous sample, this one includes several NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-238">As with the previous sample, this one includes several NuGet packages:</span></span>

* <span data-ttu-id="8b3ca-239">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="8b3ca-239">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="8b3ca-240">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="8b3ca-240">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="8b3ca-241">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="8b3ca-241">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="8b3ca-242">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="8b3ca-242">Microsoft.Azure.IoTHub.Serializer</span></span>
* <span data-ttu-id="8b3ca-243">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="8b3ca-243">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="8b3ca-244">You've seen most of these packages in the previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-244">You've seen most of these packages in the previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span></span> <span data-ttu-id="8b3ca-245">This package is required when you use the **serializer** library.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-245">This package is required when you use the **serializer** library.</span></span>

<span data-ttu-id="8b3ca-246">You can find the implementation of the sample application in the **simplesample\_mqtt.c** file.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-246">You can find the implementation of the sample application in the **simplesample\_mqtt.c** file.</span></span>

<span data-ttu-id="8b3ca-247">The following sections walk you through the key parts of this sample.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-247">The following sections walk you through the key parts of this sample.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="8b3ca-248">Initialize the library</span><span class="sxs-lookup"><span data-stu-id="8b3ca-248">Initialize the library</span></span>

<span data-ttu-id="8b3ca-249">To start working with the **serializer** library, call the initialization APIs:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-249">To start working with the **serializer** library, call the initialization APIs:</span></span>

```c
if (serializer_init(NULL) != SERIALIZER_OK)
{
    (void)printf("Failed on serializer_init\r\n");
}
else
{
    IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol);
    srand((unsigned int)time(NULL));
    int avgWindSpeed = 10;

    if (iotHubClientHandle == NULL)
    {
        (void)printf("Failed on IoTHubClient_LL_Create\r\n");
    }
    else
    {
        ContosoAnemometer* myWeather = CREATE_MODEL_INSTANCE(WeatherStation, ContosoAnemometer);
        if (myWeather == NULL)
        {
            (void)printf("Failed on CREATE_MODEL_INSTANCE\r\n");
        }
        else
        {
...
```

<span data-ttu-id="8b3ca-250">The call to the **serializer\_init** function is a one-time call and initializes the underlying library.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-250">The call to the **serializer\_init** function is a one-time call and initializes the underlying library.</span></span> <span data-ttu-id="8b3ca-251">Then, you call the **IoTHubClient\_LL\_CreateFromConnectionString** function, which is the same API as in the **IoTHubClient** sample.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-251">Then, you call the **IoTHubClient\_LL\_CreateFromConnectionString** function, which is the same API as in the **IoTHubClient** sample.</span></span> <span data-ttu-id="8b3ca-252">This call sets your device connection string (this call is also where you choose the protocol you want to use).</span><span class="sxs-lookup"><span data-stu-id="8b3ca-252">This call sets your device connection string (this call is also where you choose the protocol you want to use).</span></span> <span data-ttu-id="8b3ca-253">This sample uses MQTT as the transport, but could use AMQP or HTTP.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-253">This sample uses MQTT as the transport, but could use AMQP or HTTP.</span></span>

<span data-ttu-id="8b3ca-254">Finally, call the **CREATE\_MODEL\_INSTANCE** function.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-254">Finally, call the **CREATE\_MODEL\_INSTANCE** function.</span></span> <span data-ttu-id="8b3ca-255">**WeatherStation** is the namespace of the model and **ContosoAnemometer** is the name of the model.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-255">**WeatherStation** is the namespace of the model and **ContosoAnemometer** is the name of the model.</span></span> <span data-ttu-id="8b3ca-256">Once the model instance is created, you can use it to start sending and receiving messages.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-256">Once the model instance is created, you can use it to start sending and receiving messages.</span></span> <span data-ttu-id="8b3ca-257">However, it's important to understand what a model is.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-257">However, it's important to understand what a model is.</span></span>

### <a name="define-the-model"></a><span data-ttu-id="8b3ca-258">Define the model</span><span class="sxs-lookup"><span data-stu-id="8b3ca-258">Define the model</span></span>

<span data-ttu-id="8b3ca-259">A model in the **serializer** library defines the messages that your device can send to IoT Hub and the messages, called *actions* in the modeling language, which it can receive.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-259">A model in the **serializer** library defines the messages that your device can send to IoT Hub and the messages, called *actions* in the modeling language, which it can receive.</span></span> <span data-ttu-id="8b3ca-260">You define a model using a set of C macros as in the **simplesample\_mqtt** sample application:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-260">You define a model using a set of C macros as in the **simplesample\_mqtt** sample application:</span></span>

```c
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(int, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

<span data-ttu-id="8b3ca-261">The **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take the namespace of the model as an argument.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-261">The **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take the namespace of the model as an argument.</span></span> <span data-ttu-id="8b3ca-262">It's expected that anything between these macros is the definition of your model or models, and the data structures that the models use.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-262">It's expected that anything between these macros is the definition of your model or models, and the data structures that the models use.</span></span>

<span data-ttu-id="8b3ca-263">In this example, there is a single model called **ContosoAnemometer**.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-263">In this example, there is a single model called **ContosoAnemometer**.</span></span> <span data-ttu-id="8b3ca-264">This model defines two pieces of data that your device can send to IoT Hub: **DeviceId** and **WindSpeed**.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-264">This model defines two pieces of data that your device can send to IoT Hub: **DeviceId** and **WindSpeed**.</span></span> <span data-ttu-id="8b3ca-265">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-265">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span></span> <span data-ttu-id="8b3ca-266">Each data element has a type, and each action has a name (and optionally a set of parameters).</span><span class="sxs-lookup"><span data-stu-id="8b3ca-266">Each data element has a type, and each action has a name (and optionally a set of parameters).</span></span>

<span data-ttu-id="8b3ca-267">The data and actions defined in the model define an API surface that you can use to send messages to IoT Hub, and respond to messages sent to the device.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-267">The data and actions defined in the model define an API surface that you can use to send messages to IoT Hub, and respond to messages sent to the device.</span></span> <span data-ttu-id="8b3ca-268">Use of this model is best understood through an example.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-268">Use of this model is best understood through an example.</span></span>

### <a name="send-messages"></a><span data-ttu-id="8b3ca-269">Send messages</span><span class="sxs-lookup"><span data-stu-id="8b3ca-269">Send messages</span></span>

<span data-ttu-id="8b3ca-270">The model defines the data you can send to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-270">The model defines the data you can send to IoT Hub.</span></span> <span data-ttu-id="8b3ca-271">In this example, that means one of the two data items defined using the **WITH_DATA** macro.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-271">In this example, that means one of the two data items defined using the **WITH_DATA** macro.</span></span> <span data-ttu-id="8b3ca-272">There are several steps required to send **DeviceId** and **WindSpeed** values to an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-272">There are several steps required to send **DeviceId** and **WindSpeed** values to an IoT hub.</span></span> <span data-ttu-id="8b3ca-273">The first is to set the data you want to send:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-273">The first is to set the data you want to send:</span></span>

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

<span data-ttu-id="8b3ca-274">The model you defined earlier enables you to set the values by setting members of a **struct**.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-274">The model you defined earlier enables you to set the values by setting members of a **struct**.</span></span> <span data-ttu-id="8b3ca-275">Next, serialize the message you want to send and it:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-275">Next, serialize the message you want to send and it:</span></span>

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed to serialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

<span data-ttu-id="8b3ca-276">This code serializes the device-to-cloud to a buffer (referenced by **destination**).</span><span class="sxs-lookup"><span data-stu-id="8b3ca-276">This code serializes the device-to-cloud to a buffer (referenced by **destination**).</span></span> <span data-ttu-id="8b3ca-277">The code then invokes the **sendMessage** function to send the message to IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-277">The code then invokes the **sendMessage** function to send the message to IoT Hub:</span></span>

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable to create a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed to hand over the message to IoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted the message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


<span data-ttu-id="8b3ca-278">The second to last parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference to a callback function that's called when the data is successfully sent.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-278">The second to last parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference to a callback function that's called when the data is successfully sent.</span></span> <span data-ttu-id="8b3ca-279">Here's the callback function in the sample:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-279">Here's the callback function in the sample:</span></span>

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

<span data-ttu-id="8b3ca-280">The second parameter is a pointer to user context; the same pointer passed to **IoTHubClient\_LL\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-280">The second parameter is a pointer to user context; the same pointer passed to **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="8b3ca-281">In this case, the context is a simple counter, but it can be anything you want.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-281">In this case, the context is a simple counter, but it can be anything you want.</span></span>

<span data-ttu-id="8b3ca-282">That's all there is to sending device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-282">That's all there is to sending device-to-cloud messages.</span></span> <span data-ttu-id="8b3ca-283">The only thing left to cover is how to receive messages.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-283">The only thing left to cover is how to receive messages.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="8b3ca-284">Receive messages</span><span class="sxs-lookup"><span data-stu-id="8b3ca-284">Receive messages</span></span>

<span data-ttu-id="8b3ca-285">Receiving a message works similarly to the way messages work in the **IoTHubClient** library.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-285">Receiving a message works similarly to the way messages work in the **IoTHubClient** library.</span></span> <span data-ttu-id="8b3ca-286">First, you register a message callback function:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-286">First, you register a message callback function:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable to IoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

<span data-ttu-id="8b3ca-287">Then, you write the callback function that's invoked when a message is received:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-287">Then, you write the callback function that's invoked when a message is received:</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable to IoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed to malloc\r\n");
            result = IOTHUBMESSAGE_ABANDONED;
        }
        else
        {
            (void)memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

<span data-ttu-id="8b3ca-288">This code is boilerplate -- it's the same for any solution.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-288">This code is boilerplate -- it's the same for any solution.</span></span> <span data-ttu-id="8b3ca-289">This function receives the message and takes care of routing it to the appropriate function through the call to **EXECUTE\_COMMAND**.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-289">This function receives the message and takes care of routing it to the appropriate function through the call to **EXECUTE\_COMMAND**.</span></span> <span data-ttu-id="8b3ca-290">The function called at this point depends on the definition of the actions in your model.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-290">The function called at this point depends on the definition of the actions in your model.</span></span>

<span data-ttu-id="8b3ca-291">When you define an action in your model, you're required to implement a function that's called when your device receives the corresponding message.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-291">When you define an action in your model, you're required to implement a function that's called when your device receives the corresponding message.</span></span> <span data-ttu-id="8b3ca-292">For example, if your model defines this action:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-292">For example, if your model defines this action:</span></span>

```c
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="8b3ca-293">Define a function with this signature:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-293">Define a function with this signature:</span></span>

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position to %d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="8b3ca-294">Note how the name of the function matches the name of the action in the model and that the parameters of the function match the parameters specified for the action.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-294">Note how the name of the function matches the name of the action in the model and that the parameters of the function match the parameters specified for the action.</span></span> <span data-ttu-id="8b3ca-295">The first parameter is always required and contains a pointer to the instance of your model.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-295">The first parameter is always required and contains a pointer to the instance of your model.</span></span>

<span data-ttu-id="8b3ca-296">When the device receives a message that matches this signature, the corresponding function is called.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-296">When the device receives a message that matches this signature, the corresponding function is called.</span></span> <span data-ttu-id="8b3ca-297">Therefore, aside from having to include the boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-297">Therefore, aside from having to include the boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="8b3ca-298">Uninitialize the library</span><span class="sxs-lookup"><span data-stu-id="8b3ca-298">Uninitialize the library</span></span>

<span data-ttu-id="8b3ca-299">When you're done sending data and receiving messages, you can uninitialize the IoT library:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-299">When you're done sending data and receiving messages, you can uninitialize the IoT library:</span></span>

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

<span data-ttu-id="8b3ca-300">Each of these three functions aligns with the three initialization functions described previously.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-300">Each of these three functions aligns with the three initialization functions described previously.</span></span> <span data-ttu-id="8b3ca-301">Calling these APIs ensures that you free previously allocated resources.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-301">Calling these APIs ensures that you free previously allocated resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b3ca-302">Next Steps</span><span class="sxs-lookup"><span data-stu-id="8b3ca-302">Next Steps</span></span>

<span data-ttu-id="8b3ca-303">This article covered the basics of using the libraries in the **Azure IoT device SDK for C**. It provided you with enough information to understand what's included in the SDK, its architecture, and how to get started working with the Windows samples.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-303">This article covered the basics of using the libraries in the **Azure IoT device SDK for C**. It provided you with enough information to understand what's included in the SDK, its architecture, and how to get started working with the Windows samples.</span></span> <span data-ttu-id="8b3ca-304">The next article continues the description of the SDK by explaining [more about the IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="8b3ca-304">The next article continues the description of the SDK by explaining [more about the IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span></span>

<span data-ttu-id="8b3ca-305">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="8b3ca-305">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="8b3ca-306">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="8b3ca-306">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="8b3ca-307">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span><span class="sxs-lookup"><span data-stu-id="8b3ca-307">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span></span>

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-gateway]: iot-hub-linux-gateway-sdk-simulated-device.md







