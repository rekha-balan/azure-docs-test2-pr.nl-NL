---
title: Data conversion on IoT gateway with Azure IoT Gateway SDK | Microsoft Docs
description: Use IoT gateway to convert the format of sensor data through a customized module from the Azure IoT Gateway SDK.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: iot gateway data conversion, iot gateway data transformation
ms.assetid: 75f2573d-500b-4405-bff7-61021c4c3500
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: xshi
ms.openlocfilehash: ca5631755fd9c46c4ee7a0f837dcbf4d75a99c25
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563204"
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-gateway-sdk"></a><span data-ttu-id="cac93-104">Use IoT gateway for sensor data transformation with Azure IoT Gateway SDK</span><span class="sxs-lookup"><span data-stu-id="cac93-104">Use IoT gateway for sensor data transformation with Azure IoT Gateway SDK</span></span>

> [!NOTE]
> <span data-ttu-id="cac93-105">Before you start this tutorial, make sure you’ve completed the following lessons in sequence:</span><span class="sxs-lookup"><span data-stu-id="cac93-105">Before you start this tutorial, make sure you’ve completed the following lessons in sequence:</span></span>
> * [<span data-ttu-id="cac93-106">Set up Intel NUC as an IoT gateway</span><span class="sxs-lookup"><span data-stu-id="cac93-106">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [<span data-ttu-id="cac93-107">Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="cac93-107">Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

<span data-ttu-id="cac93-108">One purpose of an Iot gateway is to process collected data before sending it to the cloud.</span><span class="sxs-lookup"><span data-stu-id="cac93-108">One purpose of an Iot gateway is to process collected data before sending it to the cloud.</span></span> <span data-ttu-id="cac93-109">The Azure IoT Gateway SDK introduces modules which can be created and assembled to form the data processing workflow.</span><span class="sxs-lookup"><span data-stu-id="cac93-109">The Azure IoT Gateway SDK introduces modules which can be created and assembled to form the data processing workflow.</span></span> <span data-ttu-id="cac93-110">A module receives a message, performs some action on it, and then move it on for other modules to process.</span><span class="sxs-lookup"><span data-stu-id="cac93-110">A module receives a message, performs some action on it, and then move it on for other modules to process.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="cac93-111">What you learn</span><span class="sxs-lookup"><span data-stu-id="cac93-111">What you learn</span></span>

<span data-ttu-id="cac93-112">You learn how to create a module to convert messages from the SensorTag into a different format.</span><span class="sxs-lookup"><span data-stu-id="cac93-112">You learn how to create a module to convert messages from the SensorTag into a different format.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="cac93-113">What you do</span><span class="sxs-lookup"><span data-stu-id="cac93-113">What you do</span></span>

* <span data-ttu-id="cac93-114">Create a module to convert a received message into the .json format.</span><span class="sxs-lookup"><span data-stu-id="cac93-114">Create a module to convert a received message into the .json format.</span></span>
* <span data-ttu-id="cac93-115">Compile the module.</span><span class="sxs-lookup"><span data-stu-id="cac93-115">Compile the module.</span></span>
* <span data-ttu-id="cac93-116">Add the module to the BLE sample application from the Azure IoT Gateway SDK.</span><span class="sxs-lookup"><span data-stu-id="cac93-116">Add the module to the BLE sample application from the Azure IoT Gateway SDK.</span></span>
* <span data-ttu-id="cac93-117">Run the sample application.</span><span class="sxs-lookup"><span data-stu-id="cac93-117">Run the sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cac93-118">What you need</span><span class="sxs-lookup"><span data-stu-id="cac93-118">What you need</span></span>

* <span data-ttu-id="cac93-119">The following tutorials completed in sequence:</span><span class="sxs-lookup"><span data-stu-id="cac93-119">The following tutorials completed in sequence:</span></span>
  * [<span data-ttu-id="cac93-120">Set up Intel NUC as an IoT gateway</span><span class="sxs-lookup"><span data-stu-id="cac93-120">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [<span data-ttu-id="cac93-121">Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="cac93-121">Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* <span data-ttu-id="cac93-122">An SSH client that runs on your host computer.</span><span class="sxs-lookup"><span data-stu-id="cac93-122">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="cac93-123">PuTTY is recommended on Windows.</span><span class="sxs-lookup"><span data-stu-id="cac93-123">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="cac93-124">Linux and macOS already come with an SSH client.</span><span class="sxs-lookup"><span data-stu-id="cac93-124">Linux and macOS already come with an SSH client.</span></span>
* <span data-ttu-id="cac93-125">The IP address and the username and password to access the gateway from the SSH client.</span><span class="sxs-lookup"><span data-stu-id="cac93-125">The IP address and the username and password to access the gateway from the SSH client.</span></span>
* <span data-ttu-id="cac93-126">An Internet connection.</span><span class="sxs-lookup"><span data-stu-id="cac93-126">An Internet connection.</span></span>

## <a name="create-a-module"></a><span data-ttu-id="cac93-127">Create a module</span><span class="sxs-lookup"><span data-stu-id="cac93-127">Create a module</span></span>

1. <span data-ttu-id="cac93-128">On the host computer, run the SSH client and connect to the IoT gateway.</span><span class="sxs-lookup"><span data-stu-id="cac93-128">On the host computer, run the SSH client and connect to the IoT gateway.</span></span>
1. <span data-ttu-id="cac93-129">Clone the source files of the conversion module from GitHub to the home directory of the IoT gateway by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="cac93-129">Clone the source files of the conversion module from GitHub to the home directory of the IoT gateway by running the following commands:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   <span data-ttu-id="cac93-130">This is a native Azure Gateway SDK module written in the C programming language.</span><span class="sxs-lookup"><span data-stu-id="cac93-130">This is a native Azure Gateway SDK module written in the C programming language.</span></span> <span data-ttu-id="cac93-131">The module converts the format of received messages into the following one:</span><span class="sxs-lookup"><span data-stu-id="cac93-131">The module converts the format of received messages into the following one:</span></span>

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-the-module"></a><span data-ttu-id="cac93-132">Compile the module</span><span class="sxs-lookup"><span data-stu-id="cac93-132">Compile the module</span></span>

<span data-ttu-id="cac93-133">To compile the module, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="cac93-133">To compile the module, run the following commands:</span></span>

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module
# change the build script runnable
chmod 777 build.sh
# remove the invalid windows character
sed -i -e "s/\r$\/\/" build.sh
# run the build shell script
./build.sh
```

<span data-ttu-id="cac93-134">You get a `libmy_module.so` file after the compile is completed.</span><span class="sxs-lookup"><span data-stu-id="cac93-134">You get a `libmy_module.so` file after the compile is completed.</span></span> <span data-ttu-id="cac93-135">Make a note of the absolute path of this file.</span><span class="sxs-lookup"><span data-stu-id="cac93-135">Make a note of the absolute path of this file.</span></span>

## <a name="add-the-module-to-the-ble-sample-application"></a><span data-ttu-id="cac93-136">Add the module to the BLE sample application</span><span class="sxs-lookup"><span data-stu-id="cac93-136">Add the module to the BLE sample application</span></span>

1. <span data-ttu-id="cac93-137">Go to the samples folder by running the following command:</span><span class="sxs-lookup"><span data-stu-id="cac93-137">Go to the samples folder by running the following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. <span data-ttu-id="cac93-138">Open the configuration file by running the following command:</span><span class="sxs-lookup"><span data-stu-id="cac93-138">Open the configuration file by running the following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="cac93-139">Add a module by inserting the following code to the `modules` section.</span><span class="sxs-lookup"><span data-stu-id="cac93-139">Add a module by inserting the following code to the `modules` section.</span></span>

   ```json
   {
       "name": "MyModule",
       "loader": {
           "name": "native",
           "entrypoint":{
               "module.path": "[Your libmy_module.so path]"
               }
            },
        "args": null
    },
    ```

1. <span data-ttu-id="cac93-140">Replace `[Your libmy_module.so path]` in the code with the absolute path of the libmy_module.so\` file.</span><span class="sxs-lookup"><span data-stu-id="cac93-140">Replace `[Your libmy_module.so path]` in the code with the absolute path of the libmy_module.so\` file.</span></span>
1. <span data-ttu-id="cac93-141">Replace the code in the `links` section with the following one:</span><span class="sxs-lookup"><span data-stu-id="cac93-141">Replace the code in the `links` section with the following one:</span></span>

   ```json
   {
       "source": "SensorTag",
       "sink": "MyModule"
   },
   {
       "source": "MyModule",
       "sink": "mapping"
   }
   ```

1. <span data-ttu-id="cac93-142">Press `ESC`, and then type `:wq` to save the file.</span><span class="sxs-lookup"><span data-stu-id="cac93-142">Press `ESC`, and then type `:wq` to save the file.</span></span>

## <a name="run-the-sample-application"></a><span data-ttu-id="cac93-143">Run the sample application</span><span class="sxs-lookup"><span data-stu-id="cac93-143">Run the sample application</span></span>

1. <span data-ttu-id="cac93-144">Power on the SensorTag.</span><span class="sxs-lookup"><span data-stu-id="cac93-144">Power on the SensorTag.</span></span>
1. <span data-ttu-id="cac93-145">Set the SSL_CERT_FILE environment variable by running the following command:</span><span class="sxs-lookup"><span data-stu-id="cac93-145">Set the SSL_CERT_FILE environment variable by running the following command:</span></span>

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. <span data-ttu-id="cac93-146">Run the sample application with the added module by running the following command:</span><span class="sxs-lookup"><span data-stu-id="cac93-146">Run the sample application with the added module by running the following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="cac93-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="cac93-147">Next steps</span></span>

<span data-ttu-id="cac93-148">You’ve successfully use the IoT gateway to convert the message from SensorTag into the .json format.</span><span class="sxs-lookup"><span data-stu-id="cac93-148">You’ve successfully use the IoT gateway to convert the message from SensorTag into the .json format.</span></span>
<span data-ttu-id="cac93-149">If you want to learn more about Azure IoT gateway modules, you can find more module samples here: https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules.</span><span class="sxs-lookup"><span data-stu-id="cac93-149">If you want to learn more about Azure IoT gateway modules, you can find more module samples here: https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules.</span></span>