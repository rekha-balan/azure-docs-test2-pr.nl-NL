---
title: The Azure IoT device SDK for C | Microsoft Docs
description: Get started with the Azure IoT device SDK for C and learn how to create device apps that communicate with an IoT hub.
author: yzhong94
manager: arjmands
ms.service: iot-hub
services: iot-hub
ms.devlang: c
ms.topic: conceptual
ms.date: 08/25/2017
ms.author: yizhon
ms.openlocfilehash: 4f8ad67fafa20fd9adce62e8beb619999203ef62
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44776925"
---
# <a name="azure-iot-device-sdk-for-c"></a><span data-ttu-id="f7232-103">Azure IoT device SDK for C</span><span class="sxs-lookup"><span data-stu-id="f7232-103">Azure IoT device SDK for C</span></span>

<span data-ttu-id="f7232-104">The **Azure IoT device SDK** is a set of libraries designed to simplify the process of sending messages to and receiving messages from the **Azure IoT Hub** service.</span><span class="sxs-lookup"><span data-stu-id="f7232-104">The **Azure IoT device SDK** is a set of libraries designed to simplify the process of sending messages to and receiving messages from the **Azure IoT Hub** service.</span></span> <span data-ttu-id="f7232-105">There are different variations of the SDK, each targeting a specific platform, but this article describes the **Azure IoT device SDK for C**.</span><span class="sxs-lookup"><span data-stu-id="f7232-105">There are different variations of the SDK, each targeting a specific platform, but this article describes the **Azure IoT device SDK for C**.</span></span>

[!INCLUDE [iot-hub-basic](../../includes/iot-hub-basic-partial.md)]

<span data-ttu-id="f7232-106">The Azure IoT device SDK for C is written in ANSI C (C99) to maximize portability.</span><span class="sxs-lookup"><span data-stu-id="f7232-106">The Azure IoT device SDK for C is written in ANSI C (C99) to maximize portability.</span></span> <span data-ttu-id="f7232-107">This feature makes the libraries well-suited to operate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span><span class="sxs-lookup"><span data-stu-id="f7232-107">This feature makes the libraries well-suited to operate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span></span>

<span data-ttu-id="f7232-108">There are a broad range of platforms on which the SDK has been tested (see the [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span><span class="sxs-lookup"><span data-stu-id="f7232-108">There are a broad range of platforms on which the SDK has been tested (see the [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span></span> <span data-ttu-id="f7232-109">Although this article includes walkthroughs of sample code running on the Windows platform, the code described in this article is identical across the range of supported platforms.</span><span class="sxs-lookup"><span data-stu-id="f7232-109">Although this article includes walkthroughs of sample code running on the Windows platform, the code described in this article is identical across the range of supported platforms.</span></span>

<span data-ttu-id="f7232-110">The following video presents an overview of the Azure IoT SDK for C:</span><span class="sxs-lookup"><span data-stu-id="f7232-110">The following video presents an overview of the Azure IoT SDK for C:</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Internet-of-Things-Show/Azure-IoT-C-SDK-insights/Player]

<span data-ttu-id="f7232-111">This article introduces you to the architecture of the Azure IoT device SDK for C. It demonstrates how to initialize the device library, send data to IoT Hub, and receive messages from it.</span><span class="sxs-lookup"><span data-stu-id="f7232-111">This article introduces you to the architecture of the Azure IoT device SDK for C. It demonstrates how to initialize the device library, send data to IoT Hub, and receive messages from it.</span></span> <span data-ttu-id="f7232-112">The information in this article should be enough to get started using the SDK, but also provides pointers to additional information about the libraries.</span><span class="sxs-lookup"><span data-stu-id="f7232-112">The information in this article should be enough to get started using the SDK, but also provides pointers to additional information about the libraries.</span></span>

## <a name="sdk-architecture"></a><span data-ttu-id="f7232-113">SDK architecture</span><span class="sxs-lookup"><span data-stu-id="f7232-113">SDK architecture</span></span>

<span data-ttu-id="f7232-114">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="f7232-114">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

<span data-ttu-id="f7232-115">The latest version of the libraries can be found in the **master** branch of the repository:</span><span class="sxs-lookup"><span data-stu-id="f7232-115">The latest version of the libraries can be found in the **master** branch of the repository:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* <span data-ttu-id="f7232-116">The core implementation of the SDK is in the **iothub\_client** folder that contains the implementation of the lowest API layer in the SDK: the **IoTHubClient** library.</span><span class="sxs-lookup"><span data-stu-id="f7232-116">The core implementation of the SDK is in the **iothub\_client** folder that contains the implementation of the lowest API layer in the SDK: the **IoTHubClient** library.</span></span> <span data-ttu-id="f7232-117">The **IoTHubClient** library contains APIs implementing raw messaging for sending messages to IoT Hub and receiving messages from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f7232-117">The **IoTHubClient** library contains APIs implementing raw messaging for sending messages to IoT Hub and receiving messages from IoT Hub.</span></span> <span data-ttu-id="f7232-118">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span><span class="sxs-lookup"><span data-stu-id="f7232-118">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span></span>
* <span data-ttu-id="f7232-119">The **serializer** folder contains helper functions and samples that show you how to serialize data before sending to Azure IoT Hub using the client library.</span><span class="sxs-lookup"><span data-stu-id="f7232-119">The **serializer** folder contains helper functions and samples that show you how to serialize data before sending to Azure IoT Hub using the client library.</span></span> <span data-ttu-id="f7232-120">The use of the serializer is not mandatory and is provided as a convenience.</span><span class="sxs-lookup"><span data-stu-id="f7232-120">The use of the serializer is not mandatory and is provided as a convenience.</span></span> <span data-ttu-id="f7232-121">To use the **serializer** library, you define a model that specifies the data to send to IoT Hub and the messages you expect to receive from it.</span><span class="sxs-lookup"><span data-stu-id="f7232-121">To use the **serializer** library, you define a model that specifies the data to send to IoT Hub and the messages you expect to receive from it.</span></span> <span data-ttu-id="f7232-122">Once the model is defined, the SDK provides you with an API surface that enables you to easily work with device-to-cloud and cloud-to-device messages without worrying about the serialization details.</span><span class="sxs-lookup"><span data-stu-id="f7232-122">Once the model is defined, the SDK provides you with an API surface that enables you to easily work with device-to-cloud and cloud-to-device messages without worrying about the serialization details.</span></span> <span data-ttu-id="f7232-123">The library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span><span class="sxs-lookup"><span data-stu-id="f7232-123">The library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span></span>
* <span data-ttu-id="f7232-124">The **IoTHubClient** library depends on other open source libraries:</span><span class="sxs-lookup"><span data-stu-id="f7232-124">The **IoTHubClient** library depends on other open source libraries:</span></span>
  * <span data-ttu-id="f7232-125">The [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span><span class="sxs-lookup"><span data-stu-id="f7232-125">The [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span></span>
  * <span data-ttu-id="f7232-126">The [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span><span class="sxs-lookup"><span data-stu-id="f7232-126">The [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span></span>
  * <span data-ttu-id="f7232-127">The [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing the MQTT protocol and optimized for resource constrained devices.</span><span class="sxs-lookup"><span data-stu-id="f7232-127">The [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing the MQTT protocol and optimized for resource constrained devices.</span></span>

<span data-ttu-id="f7232-128">Use of these libraries is easier to understand by looking at example code.</span><span class="sxs-lookup"><span data-stu-id="f7232-128">Use of these libraries is easier to understand by looking at example code.</span></span> <span data-ttu-id="f7232-129">The following sections walk you through several of the sample applications that are included in the SDK.</span><span class="sxs-lookup"><span data-stu-id="f7232-129">The following sections walk you through several of the sample applications that are included in the SDK.</span></span> <span data-ttu-id="f7232-130">This walkthrough should give you a good feel for the various capabilities of the architectural layers of the SDK and an introduction to how the APIs work.</span><span class="sxs-lookup"><span data-stu-id="f7232-130">This walkthrough should give you a good feel for the various capabilities of the architectural layers of the SDK and an introduction to how the APIs work.</span></span>

## <a name="before-you-run-the-samples"></a><span data-ttu-id="f7232-131">Before you run the samples</span><span class="sxs-lookup"><span data-stu-id="f7232-131">Before you run the samples</span></span>

<span data-ttu-id="f7232-132">Before you can run the samples in the Azure IoT device SDK for C, you must [create an instance of the IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f7232-132">Before you can run the samples in the Azure IoT device SDK for C, you must [create an instance of the IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span></span> <span data-ttu-id="f7232-133">Then complete the following tasks:</span><span class="sxs-lookup"><span data-stu-id="f7232-133">Then complete the following tasks:</span></span>

* <span data-ttu-id="f7232-134">Prepare your development environment</span><span class="sxs-lookup"><span data-stu-id="f7232-134">Prepare your development environment</span></span>
* <span data-ttu-id="f7232-135">Obtain device credentials.</span><span class="sxs-lookup"><span data-stu-id="f7232-135">Obtain device credentials.</span></span>

### <a name="prepare-your-development-environment"></a><span data-ttu-id="f7232-136">Prepare your development environment</span><span class="sxs-lookup"><span data-stu-id="f7232-136">Prepare your development environment</span></span>

<span data-ttu-id="f7232-137">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and the samples use these packages when available.</span><span class="sxs-lookup"><span data-stu-id="f7232-137">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and the samples use these packages when available.</span></span> <span data-ttu-id="f7232-138">In some cases, you need to compile the SDK for or on your device.</span><span class="sxs-lookup"><span data-stu-id="f7232-138">In some cases, you need to compile the SDK for or on your device.</span></span> <span data-ttu-id="f7232-139">If you need to compile the SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in the GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="f7232-139">If you need to compile the SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in the GitHub repository.</span></span>

<span data-ttu-id="f7232-140">To obtain the sample application code, download a copy of the SDK from GitHub.</span><span class="sxs-lookup"><span data-stu-id="f7232-140">To obtain the sample application code, download a copy of the SDK from GitHub.</span></span> <span data-ttu-id="f7232-141">Get your copy of the source from the **master** branch of the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span><span class="sxs-lookup"><span data-stu-id="f7232-141">Get your copy of the source from the **master** branch of the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span></span>


### <a name="obtain-the-device-credentials"></a><span data-ttu-id="f7232-142">Obtain the device credentials</span><span class="sxs-lookup"><span data-stu-id="f7232-142">Obtain the device credentials</span></span>

<span data-ttu-id="f7232-143">Now that you have the sample source code, the next thing to do is to get a set of device credentials.</span><span class="sxs-lookup"><span data-stu-id="f7232-143">Now that you have the sample source code, the next thing to do is to get a set of device credentials.</span></span> <span data-ttu-id="f7232-144">For a device to be able to access an IoT hub, you must first add the device to the IoT Hub identity registry.</span><span class="sxs-lookup"><span data-stu-id="f7232-144">For a device to be able to access an IoT hub, you must first add the device to the IoT Hub identity registry.</span></span> <span data-ttu-id="f7232-145">When you add your device, you get a set of device credentials that you need for the device to be able to connect to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="f7232-145">When you add your device, you get a set of device credentials that you need for the device to be able to connect to the IoT hub.</span></span> <span data-ttu-id="f7232-146">The sample applications discussed in the next section expect these credentials in the form of a **device connection string**.</span><span class="sxs-lookup"><span data-stu-id="f7232-146">The sample applications discussed in the next section expect these credentials in the form of a **device connection string**.</span></span>

<span data-ttu-id="f7232-147">There are several open source tools to help you manage your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="f7232-147">There are several open source tools to help you manage your IoT hub.</span></span>

* <span data-ttu-id="f7232-148">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="f7232-148">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>
* <span data-ttu-id="f7232-149">A cross-platform Visual Studio Code extension called [Azure IoT Toolkit](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit).</span><span class="sxs-lookup"><span data-stu-id="f7232-149">A cross-platform Visual Studio Code extension called [Azure IoT Toolkit](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit).</span></span>
* <span data-ttu-id="f7232-150">A cross-platform Python CLI tool called [the IoT extension for Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension).</span><span class="sxs-lookup"><span data-stu-id="f7232-150">A cross-platform Python CLI tool called [the IoT extension for Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension).</span></span>

<span data-ttu-id="f7232-151">This tutorial uses the graphical *device explorer* tool.</span><span class="sxs-lookup"><span data-stu-id="f7232-151">This tutorial uses the graphical *device explorer* tool.</span></span> <span data-ttu-id="f7232-152">You can use the *Azure IoT Toolkit extension for VS Code* if you develop in VS Code.</span><span class="sxs-lookup"><span data-stu-id="f7232-152">You can use the *Azure IoT Toolkit extension for VS Code* if you develop in VS Code.</span></span> <span data-ttu-id="f7232-153">You can also use the *the IoT extension for Azure CLI 2.0* tool if you prefer to use a CLI tool.</span><span class="sxs-lookup"><span data-stu-id="f7232-153">You can also use the *the IoT extension for Azure CLI 2.0* tool if you prefer to use a CLI tool.</span></span>

<span data-ttu-id="f7232-154">The device explorer tool uses the Azure IoT service libraries to perform various functions on IoT Hub, including adding devices.</span><span class="sxs-lookup"><span data-stu-id="f7232-154">The device explorer tool uses the Azure IoT service libraries to perform various functions on IoT Hub, including adding devices.</span></span> <span data-ttu-id="f7232-155">If you use the device explorer tool to add a device, you get a connection string for your device.</span><span class="sxs-lookup"><span data-stu-id="f7232-155">If you use the device explorer tool to add a device, you get a connection string for your device.</span></span> <span data-ttu-id="f7232-156">You need this connection string to run the sample applications.</span><span class="sxs-lookup"><span data-stu-id="f7232-156">You need this connection string to run the sample applications.</span></span>

<span data-ttu-id="f7232-157">If you're not familiar with the device explorer tool, the following procedure describes how to use it to add a device and obtain a device connection string.</span><span class="sxs-lookup"><span data-stu-id="f7232-157">If you're not familiar with the device explorer tool, the following procedure describes how to use it to add a device and obtain a device connection string.</span></span>

<span data-ttu-id="f7232-158">To install the device explorer tool, see [How to use the Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="f7232-158">To install the device explorer tool, see [How to use the Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>

<span data-ttu-id="f7232-159">When you run the program, you see this interface:</span><span class="sxs-lookup"><span data-stu-id="f7232-159">When you run the program, you see this interface:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

<span data-ttu-id="f7232-160">Enter your **IoT Hub Connection String** in the first field and click **Update**.</span><span class="sxs-lookup"><span data-stu-id="f7232-160">Enter your **IoT Hub Connection String** in the first field and click **Update**.</span></span> <span data-ttu-id="f7232-161">This step configures the tool so that it can communicate with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f7232-161">This step configures the tool so that it can communicate with IoT Hub.</span></span> <span data-ttu-id="f7232-162">The **Connection String** can be found under **IoT Hub Service** > **Settings** > **Shared Access Policy** > **iothubowner**.</span><span class="sxs-lookup"><span data-stu-id="f7232-162">The **Connection String** can be found under **IoT Hub Service** > **Settings** > **Shared Access Policy** > **iothubowner**.</span></span>

<span data-ttu-id="f7232-163">When the IoT Hub connection string is configured, click the **Management** tab:</span><span class="sxs-lookup"><span data-stu-id="f7232-163">When the IoT Hub connection string is configured, click the **Management** tab:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

<span data-ttu-id="f7232-164">This tab is where you manage the devices registered in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="f7232-164">This tab is where you manage the devices registered in your IoT hub.</span></span>

<span data-ttu-id="f7232-165">You create a device by clicking the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="f7232-165">You create a device by clicking the **Create** button.</span></span> <span data-ttu-id="f7232-166">A dialog displays with a set of pre-populated keys (primary and secondary).</span><span class="sxs-lookup"><span data-stu-id="f7232-166">A dialog displays with a set of pre-populated keys (primary and secondary).</span></span> <span data-ttu-id="f7232-167">Enter a **Device ID** and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f7232-167">Enter a **Device ID** and then click **Create**.</span></span>

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

<span data-ttu-id="f7232-168">When the device is created, the Devices list updates with all the registered devices, including the one you just created.</span><span class="sxs-lookup"><span data-stu-id="f7232-168">When the device is created, the Devices list updates with all the registered devices, including the one you just created.</span></span> <span data-ttu-id="f7232-169">If you right-click your new device, you see this menu:</span><span class="sxs-lookup"><span data-stu-id="f7232-169">If you right-click your new device, you see this menu:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

<span data-ttu-id="f7232-170">If you choose **Copy connection string for selected device**, the device connection string is copied to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="f7232-170">If you choose **Copy connection string for selected device**, the device connection string is copied to the clipboard.</span></span> <span data-ttu-id="f7232-171">Keep a copy of the device connection string.</span><span class="sxs-lookup"><span data-stu-id="f7232-171">Keep a copy of the device connection string.</span></span> <span data-ttu-id="f7232-172">You need it when running the sample applications described in the following sections.</span><span class="sxs-lookup"><span data-stu-id="f7232-172">You need it when running the sample applications described in the following sections.</span></span>

<span data-ttu-id="f7232-173">When you've completed the steps above, you're ready to start running some code.</span><span class="sxs-lookup"><span data-stu-id="f7232-173">When you've completed the steps above, you're ready to start running some code.</span></span> <span data-ttu-id="f7232-174">Most samples have a constant at the top of the main source file that enables you to enter a connection string.</span><span class="sxs-lookup"><span data-stu-id="f7232-174">Most samples have a constant at the top of the main source file that enables you to enter a connection string.</span></span> <span data-ttu-id="f7232-175">For example, the corresponding line from the **iothub\_client\_sample\_mqtt** application appears as follows.</span><span class="sxs-lookup"><span data-stu-id="f7232-175">For example, the corresponding line from the **iothub\_client\_sample\_mqtt** application appears as follows.</span></span>

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-the-iothubclient-library"></a><span data-ttu-id="f7232-176">Use the IoTHubClient library</span><span class="sxs-lookup"><span data-stu-id="f7232-176">Use the IoTHubClient library</span></span>

<span data-ttu-id="f7232-177">Within the **iothub\_client** folder in the [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="f7232-177">Within the **iothub\_client** folder in the [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span></span>

<span data-ttu-id="f7232-178">The Windows version of the **iothub\_client\_sample\_mqtt** application includes the following Visual Studio solution:</span><span class="sxs-lookup"><span data-stu-id="f7232-178">The Windows version of the **iothub\_client\_sample\_mqtt** application includes the following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="f7232-179">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span><span class="sxs-lookup"><span data-stu-id="f7232-179">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="f7232-180">This solution contains a single project.</span><span class="sxs-lookup"><span data-stu-id="f7232-180">This solution contains a single project.</span></span> <span data-ttu-id="f7232-181">There are four NuGet packages installed in this solution:</span><span class="sxs-lookup"><span data-stu-id="f7232-181">There are four NuGet packages installed in this solution:</span></span>

* <span data-ttu-id="f7232-182">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="f7232-182">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="f7232-183">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="f7232-183">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="f7232-184">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="f7232-184">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="f7232-185">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="f7232-185">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="f7232-186">You always need the **Microsoft.Azure.C.SharedUtility** package when you are working with the SDK.</span><span class="sxs-lookup"><span data-stu-id="f7232-186">You always need the **Microsoft.Azure.C.SharedUtility** package when you are working with the SDK.</span></span> <span data-ttu-id="f7232-187">This sample uses the MQTT protocol, therefore you must include the **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTPS).</span><span class="sxs-lookup"><span data-stu-id="f7232-187">This sample uses the MQTT protocol, therefore you must include the **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTPS).</span></span> <span data-ttu-id="f7232-188">Because the sample uses the **IoTHubClient** library, you must also include the **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span><span class="sxs-lookup"><span data-stu-id="f7232-188">Because the sample uses the **IoTHubClient** library, you must also include the **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span></span>

<span data-ttu-id="f7232-189">You can find the implementation for the sample application in the **iothub\_client\_sample\_mqtt.c** source file.</span><span class="sxs-lookup"><span data-stu-id="f7232-189">You can find the implementation for the sample application in the **iothub\_client\_sample\_mqtt.c** source file.</span></span>

<span data-ttu-id="f7232-190">The following steps use this sample application to walk you through what's required to use the **IoTHubClient** library.</span><span class="sxs-lookup"><span data-stu-id="f7232-190">The following steps use this sample application to walk you through what's required to use the **IoTHubClient** library.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="f7232-191">Initialize the library</span><span class="sxs-lookup"><span data-stu-id="f7232-191">Initialize the library</span></span>

> [!NOTE]
> <span data-ttu-id="f7232-192">Before you start working with the libraries, you may need to perform some platform-specific initialization.</span><span class="sxs-lookup"><span data-stu-id="f7232-192">Before you start working with the libraries, you may need to perform some platform-specific initialization.</span></span> <span data-ttu-id="f7232-193">For example, if you plan to use AMQP on Linux you must initialize the OpenSSL library.</span><span class="sxs-lookup"><span data-stu-id="f7232-193">For example, if you plan to use AMQP on Linux you must initialize the OpenSSL library.</span></span> <span data-ttu-id="f7232-194">The samples in the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call the utility function **platform\_init** when the client starts and call the **platform\_deinit** function before exiting.</span><span class="sxs-lookup"><span data-stu-id="f7232-194">The samples in the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call the utility function **platform\_init** when the client starts and call the **platform\_deinit** function before exiting.</span></span> <span data-ttu-id="f7232-195">These functions are declared in the platform.h header file.</span><span class="sxs-lookup"><span data-stu-id="f7232-195">These functions are declared in the platform.h header file.</span></span> <span data-ttu-id="f7232-196">Examine the definitions of these functions for your target platform in the [repository](https://github.com/Azure/azure-iot-sdk-c) to determine whether you need to include any platform-specific initialization code in your client.</span><span class="sxs-lookup"><span data-stu-id="f7232-196">Examine the definitions of these functions for your target platform in the [repository](https://github.com/Azure/azure-iot-sdk-c) to determine whether you need to include any platform-specific initialization code in your client.</span></span>

<span data-ttu-id="f7232-197">To start working with the libraries, first allocate an IoT Hub client handle:</span><span class="sxs-lookup"><span data-stu-id="f7232-197">To start working with the libraries, first allocate an IoT Hub client handle:</span></span>

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

<span data-ttu-id="f7232-198">You pass a copy of the device connection string you obtained from the device explorer tool to this function.</span><span class="sxs-lookup"><span data-stu-id="f7232-198">You pass a copy of the device connection string you obtained from the device explorer tool to this function.</span></span> <span data-ttu-id="f7232-199">You also designate the communications protocol to use.</span><span class="sxs-lookup"><span data-stu-id="f7232-199">You also designate the communications protocol to use.</span></span> <span data-ttu-id="f7232-200">This example uses MQTT, but AMQP and HTTPS are also options.</span><span class="sxs-lookup"><span data-stu-id="f7232-200">This example uses MQTT, but AMQP and HTTPS are also options.</span></span>

<span data-ttu-id="f7232-201">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling the APIs to send and receive messages to and from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f7232-201">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling the APIs to send and receive messages to and from IoT Hub.</span></span>

### <a name="send-messages"></a><span data-ttu-id="f7232-202">Send messages</span><span class="sxs-lookup"><span data-stu-id="f7232-202">Send messages</span></span>

<span data-ttu-id="f7232-203">The sample application sets up a loop to send messages to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="f7232-203">The sample application sets up a loop to send messages to your IoT hub.</span></span> <span data-ttu-id="f7232-204">The following snippet:</span><span class="sxs-lookup"><span data-stu-id="f7232-204">The following snippet:</span></span>

- <span data-ttu-id="f7232-205">Creates a message.</span><span class="sxs-lookup"><span data-stu-id="f7232-205">Creates a message.</span></span>
- <span data-ttu-id="f7232-206">Adds a property to the message.</span><span class="sxs-lookup"><span data-stu-id="f7232-206">Adds a property to the message.</span></span>
- <span data-ttu-id="f7232-207">Sends a message.</span><span class="sxs-lookup"><span data-stu-id="f7232-207">Sends a message.</span></span>

<span data-ttu-id="f7232-208">First, create a message:</span><span class="sxs-lookup"><span data-stu-id="f7232-208">First, create a message:</span></span>

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

<span data-ttu-id="f7232-209">Every time you send a message, you specify a reference to a callback function that's invoked when the data is sent.</span><span class="sxs-lookup"><span data-stu-id="f7232-209">Every time you send a message, you specify a reference to a callback function that's invoked when the data is sent.</span></span> <span data-ttu-id="f7232-210">In this example, the callback function is called **SendConfirmationCallback**.</span><span class="sxs-lookup"><span data-stu-id="f7232-210">In this example, the callback function is called **SendConfirmationCallback**.</span></span> <span data-ttu-id="f7232-211">The following snippet shows this callback function:</span><span class="sxs-lookup"><span data-stu-id="f7232-211">The following snippet shows this callback function:</span></span>

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

<span data-ttu-id="f7232-212">Note the call to the **IoTHubMessage\_Destroy** function when you're done with the message.</span><span class="sxs-lookup"><span data-stu-id="f7232-212">Note the call to the **IoTHubMessage\_Destroy** function when you're done with the message.</span></span> <span data-ttu-id="f7232-213">This function frees the resources allocated when you created the message.</span><span class="sxs-lookup"><span data-stu-id="f7232-213">This function frees the resources allocated when you created the message.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="f7232-214">Receive messages</span><span class="sxs-lookup"><span data-stu-id="f7232-214">Receive messages</span></span>

<span data-ttu-id="f7232-215">Receiving a message is an asynchronous operation.</span><span class="sxs-lookup"><span data-stu-id="f7232-215">Receiving a message is an asynchronous operation.</span></span> <span data-ttu-id="f7232-216">First, you register the callback to invoke when the device receives a message:</span><span class="sxs-lookup"><span data-stu-id="f7232-216">First, you register the callback to invoke when the device receives a message:</span></span>

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

<span data-ttu-id="f7232-217">The last parameter is a void pointer to whatever you want.</span><span class="sxs-lookup"><span data-stu-id="f7232-217">The last parameter is a void pointer to whatever you want.</span></span> <span data-ttu-id="f7232-218">In the sample, it's a pointer to an integer but it could be a pointer to a more complex data structure.</span><span class="sxs-lookup"><span data-stu-id="f7232-218">In the sample, it's a pointer to an integer but it could be a pointer to a more complex data structure.</span></span> <span data-ttu-id="f7232-219">This parameter enables the callback function to operate on shared state with the caller of this function.</span><span class="sxs-lookup"><span data-stu-id="f7232-219">This parameter enables the callback function to operate on shared state with the caller of this function.</span></span>

<span data-ttu-id="f7232-220">When the device receives a message, the registered callback function is invoked.</span><span class="sxs-lookup"><span data-stu-id="f7232-220">When the device receives a message, the registered callback function is invoked.</span></span> <span data-ttu-id="f7232-221">This callback function retrieves:</span><span class="sxs-lookup"><span data-stu-id="f7232-221">This callback function retrieves:</span></span>

* <span data-ttu-id="f7232-222">The message id and correlation id from the message.</span><span class="sxs-lookup"><span data-stu-id="f7232-222">The message id and correlation id from the message.</span></span>
* <span data-ttu-id="f7232-223">The message content.</span><span class="sxs-lookup"><span data-stu-id="f7232-223">The message content.</span></span>
* <span data-ttu-id="f7232-224">Any custom properties from the message.</span><span class="sxs-lookup"><span data-stu-id="f7232-224">Any custom properties from the message.</span></span>

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

<span data-ttu-id="f7232-225">Use the **IoTHubMessage\_GetByteArray** function to retrieve the message, which in this example is a string.</span><span class="sxs-lookup"><span data-stu-id="f7232-225">Use the **IoTHubMessage\_GetByteArray** function to retrieve the message, which in this example is a string.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="f7232-226">Uninitialize the library</span><span class="sxs-lookup"><span data-stu-id="f7232-226">Uninitialize the library</span></span>

<span data-ttu-id="f7232-227">When you're done sending events and receiving messages, you can uninitialize the IoT library.</span><span class="sxs-lookup"><span data-stu-id="f7232-227">When you're done sending events and receiving messages, you can uninitialize the IoT library.</span></span> <span data-ttu-id="f7232-228">To do so, issue the following function call:</span><span class="sxs-lookup"><span data-stu-id="f7232-228">To do so, issue the following function call:</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="f7232-229">This call frees up the resources previously allocated by the **IoTHubClient\_CreateFromConnectionString** function.</span><span class="sxs-lookup"><span data-stu-id="f7232-229">This call frees up the resources previously allocated by the **IoTHubClient\_CreateFromConnectionString** function.</span></span>

<span data-ttu-id="f7232-230">As you can see, it's easy to send and receive messages with the **IoTHubClient** library.</span><span class="sxs-lookup"><span data-stu-id="f7232-230">As you can see, it's easy to send and receive messages with the **IoTHubClient** library.</span></span> <span data-ttu-id="f7232-231">The library handles the details of communicating with IoT Hub, including which protocol to use (from the perspective of the developer, this is a simple configuration option).</span><span class="sxs-lookup"><span data-stu-id="f7232-231">The library handles the details of communicating with IoT Hub, including which protocol to use (from the perspective of the developer, this is a simple configuration option).</span></span>

<span data-ttu-id="f7232-232">The **IoTHubClient** library also provides precise control over how to serialize the data your device sends to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f7232-232">The **IoTHubClient** library also provides precise control over how to serialize the data your device sends to IoT Hub.</span></span> <span data-ttu-id="f7232-233">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want to be concerned with.</span><span class="sxs-lookup"><span data-stu-id="f7232-233">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want to be concerned with.</span></span> <span data-ttu-id="f7232-234">If that's the case, you might consider using the **serializer** library, which is described in the next section.</span><span class="sxs-lookup"><span data-stu-id="f7232-234">If that's the case, you might consider using the **serializer** library, which is described in the next section.</span></span>

## <a name="use-the-serializer-library"></a><span data-ttu-id="f7232-235">Use the serializer library</span><span class="sxs-lookup"><span data-stu-id="f7232-235">Use the serializer library</span></span>

<span data-ttu-id="f7232-236">Conceptually the **serializer** library sits on top of the **IoTHubClient** library in the SDK.</span><span class="sxs-lookup"><span data-stu-id="f7232-236">Conceptually the **serializer** library sits on top of the **IoTHubClient** library in the SDK.</span></span> <span data-ttu-id="f7232-237">It uses the **IoTHubClient** library for the underlying communication with IoT Hub, but it adds modeling capabilities that remove the burden of dealing with message serialization from the developer.</span><span class="sxs-lookup"><span data-stu-id="f7232-237">It uses the **IoTHubClient** library for the underlying communication with IoT Hub, but it adds modeling capabilities that remove the burden of dealing with message serialization from the developer.</span></span> <span data-ttu-id="f7232-238">How this library works is best demonstrated by an example.</span><span class="sxs-lookup"><span data-stu-id="f7232-238">How this library works is best demonstrated by an example.</span></span>

<span data-ttu-id="f7232-239">Inside the **serializer** folder in the [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="f7232-239">Inside the **serializer** folder in the [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span></span> <span data-ttu-id="f7232-240">The Windows version of this sample includes the following Visual Studio solution:</span><span class="sxs-lookup"><span data-stu-id="f7232-240">The Windows version of this sample includes the following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="f7232-241">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span><span class="sxs-lookup"><span data-stu-id="f7232-241">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="f7232-242">As with the previous sample, this one includes several NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="f7232-242">As with the previous sample, this one includes several NuGet packages:</span></span>

* <span data-ttu-id="f7232-243">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="f7232-243">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="f7232-244">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="f7232-244">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="f7232-245">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="f7232-245">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="f7232-246">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="f7232-246">Microsoft.Azure.IoTHub.Serializer</span></span>
* <span data-ttu-id="f7232-247">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="f7232-247">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="f7232-248">You've seen most of these packages in the previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span><span class="sxs-lookup"><span data-stu-id="f7232-248">You've seen most of these packages in the previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span></span> <span data-ttu-id="f7232-249">This package is required when you use the **serializer** library.</span><span class="sxs-lookup"><span data-stu-id="f7232-249">This package is required when you use the **serializer** library.</span></span>

<span data-ttu-id="f7232-250">You can find the implementation of the sample application in the **simplesample\_mqtt.c** file.</span><span class="sxs-lookup"><span data-stu-id="f7232-250">You can find the implementation of the sample application in the **simplesample\_mqtt.c** file.</span></span>

<span data-ttu-id="f7232-251">The following sections walk you through the key parts of this sample.</span><span class="sxs-lookup"><span data-stu-id="f7232-251">The following sections walk you through the key parts of this sample.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="f7232-252">Initialize the library</span><span class="sxs-lookup"><span data-stu-id="f7232-252">Initialize the library</span></span>

<span data-ttu-id="f7232-253">To start working with the **serializer** library, call the initialization APIs:</span><span class="sxs-lookup"><span data-stu-id="f7232-253">To start working with the **serializer** library, call the initialization APIs:</span></span>

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

<span data-ttu-id="f7232-254">The call to the **serializer\_init** function is a one-time call and initializes the underlying library.</span><span class="sxs-lookup"><span data-stu-id="f7232-254">The call to the **serializer\_init** function is a one-time call and initializes the underlying library.</span></span> <span data-ttu-id="f7232-255">Then, you call the **IoTHubClient\_LL\_CreateFromConnectionString** function, which is the same API as in the **IoTHubClient** sample.</span><span class="sxs-lookup"><span data-stu-id="f7232-255">Then, you call the **IoTHubClient\_LL\_CreateFromConnectionString** function, which is the same API as in the **IoTHubClient** sample.</span></span> <span data-ttu-id="f7232-256">This call sets your device connection string (this call is also where you choose the protocol you want to use).</span><span class="sxs-lookup"><span data-stu-id="f7232-256">This call sets your device connection string (this call is also where you choose the protocol you want to use).</span></span> <span data-ttu-id="f7232-257">This sample uses MQTT as the transport, but could use AMQP or HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f7232-257">This sample uses MQTT as the transport, but could use AMQP or HTTPS.</span></span>

<span data-ttu-id="f7232-258">Finally, call the **CREATE\_MODEL\_INSTANCE** function.</span><span class="sxs-lookup"><span data-stu-id="f7232-258">Finally, call the **CREATE\_MODEL\_INSTANCE** function.</span></span> <span data-ttu-id="f7232-259">**WeatherStation** is the namespace of the model and **ContosoAnemometer** is the name of the model.</span><span class="sxs-lookup"><span data-stu-id="f7232-259">**WeatherStation** is the namespace of the model and **ContosoAnemometer** is the name of the model.</span></span> <span data-ttu-id="f7232-260">Once the model instance is created, you can use it to start sending and receiving messages.</span><span class="sxs-lookup"><span data-stu-id="f7232-260">Once the model instance is created, you can use it to start sending and receiving messages.</span></span> <span data-ttu-id="f7232-261">However, it's important to understand what a model is.</span><span class="sxs-lookup"><span data-stu-id="f7232-261">However, it's important to understand what a model is.</span></span>

### <a name="define-the-model"></a><span data-ttu-id="f7232-262">Define the model</span><span class="sxs-lookup"><span data-stu-id="f7232-262">Define the model</span></span>

<span data-ttu-id="f7232-263">A model in the **serializer** library defines the messages that your device can send to IoT Hub and the messages, called *actions* in the modeling language, which it can receive.</span><span class="sxs-lookup"><span data-stu-id="f7232-263">A model in the **serializer** library defines the messages that your device can send to IoT Hub and the messages, called *actions* in the modeling language, which it can receive.</span></span> <span data-ttu-id="f7232-264">You define a model using a set of C macros as in the **simplesample\_mqtt** sample application:</span><span class="sxs-lookup"><span data-stu-id="f7232-264">You define a model using a set of C macros as in the **simplesample\_mqtt** sample application:</span></span>

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

<span data-ttu-id="f7232-265">The **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take the namespace of the model as an argument.</span><span class="sxs-lookup"><span data-stu-id="f7232-265">The **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take the namespace of the model as an argument.</span></span> <span data-ttu-id="f7232-266">It's expected that anything between these macros is the definition of your model or models, and the data structures that the models use.</span><span class="sxs-lookup"><span data-stu-id="f7232-266">It's expected that anything between these macros is the definition of your model or models, and the data structures that the models use.</span></span>

<span data-ttu-id="f7232-267">In this example, there is a single model called **ContosoAnemometer**.</span><span class="sxs-lookup"><span data-stu-id="f7232-267">In this example, there is a single model called **ContosoAnemometer**.</span></span> <span data-ttu-id="f7232-268">This model defines two pieces of data that your device can send to IoT Hub: **DeviceId** and **WindSpeed**.</span><span class="sxs-lookup"><span data-stu-id="f7232-268">This model defines two pieces of data that your device can send to IoT Hub: **DeviceId** and **WindSpeed**.</span></span> <span data-ttu-id="f7232-269">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span><span class="sxs-lookup"><span data-stu-id="f7232-269">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span></span> <span data-ttu-id="f7232-270">Each data element has a type, and each action has a name (and optionally a set of parameters).</span><span class="sxs-lookup"><span data-stu-id="f7232-270">Each data element has a type, and each action has a name (and optionally a set of parameters).</span></span>

<span data-ttu-id="f7232-271">The data and actions defined in the model define an API surface that you can use to send messages to IoT Hub, and respond to messages sent to the device.</span><span class="sxs-lookup"><span data-stu-id="f7232-271">The data and actions defined in the model define an API surface that you can use to send messages to IoT Hub, and respond to messages sent to the device.</span></span> <span data-ttu-id="f7232-272">Use of this model is best understood through an example.</span><span class="sxs-lookup"><span data-stu-id="f7232-272">Use of this model is best understood through an example.</span></span>

### <a name="send-messages"></a><span data-ttu-id="f7232-273">Send messages</span><span class="sxs-lookup"><span data-stu-id="f7232-273">Send messages</span></span>

<span data-ttu-id="f7232-274">The model defines the data you can send to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f7232-274">The model defines the data you can send to IoT Hub.</span></span> <span data-ttu-id="f7232-275">In this example, that means one of the two data items defined using the **WITH_DATA** macro.</span><span class="sxs-lookup"><span data-stu-id="f7232-275">In this example, that means one of the two data items defined using the **WITH_DATA** macro.</span></span> <span data-ttu-id="f7232-276">There are several steps required to send **DeviceId** and **WindSpeed** values to an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="f7232-276">There are several steps required to send **DeviceId** and **WindSpeed** values to an IoT hub.</span></span> <span data-ttu-id="f7232-277">The first is to set the data you want to send:</span><span class="sxs-lookup"><span data-stu-id="f7232-277">The first is to set the data you want to send:</span></span>

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

<span data-ttu-id="f7232-278">The model you defined earlier enables you to set the values by setting members of a **struct**.</span><span class="sxs-lookup"><span data-stu-id="f7232-278">The model you defined earlier enables you to set the values by setting members of a **struct**.</span></span> <span data-ttu-id="f7232-279">Next, serialize the message you want to send:</span><span class="sxs-lookup"><span data-stu-id="f7232-279">Next, serialize the message you want to send:</span></span>

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

<span data-ttu-id="f7232-280">This code serializes the device-to-cloud to a buffer (referenced by **destination**).</span><span class="sxs-lookup"><span data-stu-id="f7232-280">This code serializes the device-to-cloud to a buffer (referenced by **destination**).</span></span> <span data-ttu-id="f7232-281">The code then invokes the **sendMessage** function to send the message to IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="f7232-281">The code then invokes the **sendMessage** function to send the message to IoT Hub:</span></span>

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


<span data-ttu-id="f7232-282">The second to last parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference to a callback function that's called when the data is successfully sent.</span><span class="sxs-lookup"><span data-stu-id="f7232-282">The second to last parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference to a callback function that's called when the data is successfully sent.</span></span> <span data-ttu-id="f7232-283">Here's the callback function in the sample:</span><span class="sxs-lookup"><span data-stu-id="f7232-283">Here's the callback function in the sample:</span></span>

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

<span data-ttu-id="f7232-284">The second parameter is a pointer to user context; the same pointer passed to **IoTHubClient\_LL\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="f7232-284">The second parameter is a pointer to user context; the same pointer passed to **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="f7232-285">In this case, the context is a simple counter, but it can be anything you want.</span><span class="sxs-lookup"><span data-stu-id="f7232-285">In this case, the context is a simple counter, but it can be anything you want.</span></span>

<span data-ttu-id="f7232-286">That's all there is to sending device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="f7232-286">That's all there is to sending device-to-cloud messages.</span></span> <span data-ttu-id="f7232-287">The only thing left to cover is how to receive messages.</span><span class="sxs-lookup"><span data-stu-id="f7232-287">The only thing left to cover is how to receive messages.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="f7232-288">Receive messages</span><span class="sxs-lookup"><span data-stu-id="f7232-288">Receive messages</span></span>

<span data-ttu-id="f7232-289">Receiving a message works similarly to the way messages work in the **IoTHubClient** library.</span><span class="sxs-lookup"><span data-stu-id="f7232-289">Receiving a message works similarly to the way messages work in the **IoTHubClient** library.</span></span> <span data-ttu-id="f7232-290">First, you register a message callback function:</span><span class="sxs-lookup"><span data-stu-id="f7232-290">First, you register a message callback function:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable to IoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

<span data-ttu-id="f7232-291">Then, you write the callback function that's invoked when a message is received:</span><span class="sxs-lookup"><span data-stu-id="f7232-291">Then, you write the callback function that's invoked when a message is received:</span></span>

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

<span data-ttu-id="f7232-292">This code is boilerplate -- it's the same for any solution.</span><span class="sxs-lookup"><span data-stu-id="f7232-292">This code is boilerplate -- it's the same for any solution.</span></span> <span data-ttu-id="f7232-293">This function receives the message and takes care of routing it to the appropriate function through the call to **EXECUTE\_COMMAND**.</span><span class="sxs-lookup"><span data-stu-id="f7232-293">This function receives the message and takes care of routing it to the appropriate function through the call to **EXECUTE\_COMMAND**.</span></span> <span data-ttu-id="f7232-294">The function called at this point depends on the definition of the actions in your model.</span><span class="sxs-lookup"><span data-stu-id="f7232-294">The function called at this point depends on the definition of the actions in your model.</span></span>

<span data-ttu-id="f7232-295">When you define an action in your model, you're required to implement a function that's called when your device receives the corresponding message.</span><span class="sxs-lookup"><span data-stu-id="f7232-295">When you define an action in your model, you're required to implement a function that's called when your device receives the corresponding message.</span></span> <span data-ttu-id="f7232-296">For example, if your model defines this action:</span><span class="sxs-lookup"><span data-stu-id="f7232-296">For example, if your model defines this action:</span></span>

```c
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="f7232-297">Define a function with this signature:</span><span class="sxs-lookup"><span data-stu-id="f7232-297">Define a function with this signature:</span></span>

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position to %d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="f7232-298">Note how the name of the function matches the name of the action in the model and that the parameters of the function match the parameters specified for the action.</span><span class="sxs-lookup"><span data-stu-id="f7232-298">Note how the name of the function matches the name of the action in the model and that the parameters of the function match the parameters specified for the action.</span></span> <span data-ttu-id="f7232-299">The first parameter is always required and contains a pointer to the instance of your model.</span><span class="sxs-lookup"><span data-stu-id="f7232-299">The first parameter is always required and contains a pointer to the instance of your model.</span></span>

<span data-ttu-id="f7232-300">When the device receives a message that matches this signature, the corresponding function is called.</span><span class="sxs-lookup"><span data-stu-id="f7232-300">When the device receives a message that matches this signature, the corresponding function is called.</span></span> <span data-ttu-id="f7232-301">Therefore, aside from having to include the boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span><span class="sxs-lookup"><span data-stu-id="f7232-301">Therefore, aside from having to include the boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="f7232-302">Uninitialize the library</span><span class="sxs-lookup"><span data-stu-id="f7232-302">Uninitialize the library</span></span>

<span data-ttu-id="f7232-303">When you're done sending data and receiving messages, you can uninitialize the IoT library:</span><span class="sxs-lookup"><span data-stu-id="f7232-303">When you're done sending data and receiving messages, you can uninitialize the IoT library:</span></span>

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

<span data-ttu-id="f7232-304">Each of these three functions aligns with the three initialization functions described previously.</span><span class="sxs-lookup"><span data-stu-id="f7232-304">Each of these three functions aligns with the three initialization functions described previously.</span></span> <span data-ttu-id="f7232-305">Calling these APIs ensures that you free previously allocated resources.</span><span class="sxs-lookup"><span data-stu-id="f7232-305">Calling these APIs ensures that you free previously allocated resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7232-306">Next Steps</span><span class="sxs-lookup"><span data-stu-id="f7232-306">Next Steps</span></span>

<span data-ttu-id="f7232-307">This article covered the basics of using the libraries in the **Azure IoT device SDK for C**. It provided you with enough information to understand what's included in the SDK, its architecture, and how to get started working with the Windows samples.</span><span class="sxs-lookup"><span data-stu-id="f7232-307">This article covered the basics of using the libraries in the **Azure IoT device SDK for C**. It provided you with enough information to understand what's included in the SDK, its architecture, and how to get started working with the Windows samples.</span></span> <span data-ttu-id="f7232-308">The next article continues the description of the SDK by explaining [more about the IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="f7232-308">The next article continues the description of the SDK by explaining [more about the IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span></span>

<span data-ttu-id="f7232-309">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="f7232-309">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="f7232-310">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="f7232-310">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="f7232-311">[Deploying AI to edge devices with Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="f7232-311">[Deploying AI to edge devices with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: ../iot-edge/tutorial-simulate-device-linux.md
