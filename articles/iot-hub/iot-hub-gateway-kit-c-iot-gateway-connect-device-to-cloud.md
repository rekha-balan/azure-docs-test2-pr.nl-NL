---
title: Use an IoT gateway to connect a device to Azure IoT Hub | Microsoft Docs
description: Learn how to use Intel NUC as an IoT gateway to connect a TI SensorTag and send sensor data to Azure IoT Hub in the cloud.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: iot gateway connect device to cloud
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/06/2017
ms.author: xshi
ms.openlocfilehash: cc99fae926bbb98d1d90355e1e505222e08d9f76
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44668995"
---
# <a name="use-iot-gateway-to-connect-things-to-the-cloud---sensortag-to-azure-iot-hub"></a><span data-ttu-id="4475c-104">Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="4475c-104">Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub</span></span>

> [!NOTE]
> <span data-ttu-id="4475c-105">Before you start this tutorial, make sure you’ve completed [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span><span class="sxs-lookup"><span data-stu-id="4475c-105">Before you start this tutorial, make sure you’ve completed [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span></span> <span data-ttu-id="4475c-106">In [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), you set up the Intel NUC device as an IoT gateway.</span><span class="sxs-lookup"><span data-stu-id="4475c-106">In [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), you set up the Intel NUC device as an IoT gateway.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4475c-107">What you will learn</span><span class="sxs-lookup"><span data-stu-id="4475c-107">What you will learn</span></span>

<span data-ttu-id="4475c-108">You learn how to use an IoT gateway to connect a Texas Instruments SensorTag (CC2650STK) to Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4475c-108">You learn how to use an IoT gateway to connect a Texas Instruments SensorTag (CC2650STK) to Azure IoT Hub.</span></span> <span data-ttu-id="4475c-109">The IoT gateway sends temperature and humidity data collected from the SensorTag to Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4475c-109">The IoT gateway sends temperature and humidity data collected from the SensorTag to Azure IoT Hub.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="4475c-110">What you will do</span><span class="sxs-lookup"><span data-stu-id="4475c-110">What you will do</span></span>

- <span data-ttu-id="4475c-111">Create an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4475c-111">Create an IoT hub.</span></span>
- <span data-ttu-id="4475c-112">Register a device in the IoT hub for the SensorTag.</span><span class="sxs-lookup"><span data-stu-id="4475c-112">Register a device in the IoT hub for the SensorTag.</span></span>
- <span data-ttu-id="4475c-113">Enable the connection between the IoT gateway and the SensorTag.</span><span class="sxs-lookup"><span data-stu-id="4475c-113">Enable the connection between the IoT gateway and the SensorTag.</span></span>
- <span data-ttu-id="4475c-114">Run a BLE sample application to send SensorTag data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4475c-114">Run a BLE sample application to send SensorTag data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4475c-115">What you need</span><span class="sxs-lookup"><span data-stu-id="4475c-115">What you need</span></span>

- <span data-ttu-id="4475c-116">Tutorial [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completed in which you set up Intel NUC as an IoT gateway.</span><span class="sxs-lookup"><span data-stu-id="4475c-116">Tutorial [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completed in which you set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="4475c-117">An SSH client that runs on your host computer.</span><span class="sxs-lookup"><span data-stu-id="4475c-117">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="4475c-118">PuTTY is recommended on Windows.</span><span class="sxs-lookup"><span data-stu-id="4475c-118">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="4475c-119">Linux and macOS already come with an SSH client.</span><span class="sxs-lookup"><span data-stu-id="4475c-119">Linux and macOS already come with an SSH client.</span></span>
- <span data-ttu-id="4475c-120">The IP address and the username and password to access the gateway from the SSH client.</span><span class="sxs-lookup"><span data-stu-id="4475c-120">The IP address and the username and password to access the gateway from the SSH client.</span></span>
- <span data-ttu-id="4475c-121">An Internet connection.</span><span class="sxs-lookup"><span data-stu-id="4475c-121">An Internet connection.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> <span data-ttu-id="4475c-122">Here you register this new device for your SensorTag</span><span class="sxs-lookup"><span data-stu-id="4475c-122">Here you register this new device for your SensorTag</span></span>

## <a name="enable-the-connection-between-the-iot-gateway-and-the-sensortag"></a><span data-ttu-id="4475c-123">Enable the connection between the IoT gateway and the SensorTag</span><span class="sxs-lookup"><span data-stu-id="4475c-123">Enable the connection between the IoT gateway and the SensorTag</span></span>

<span data-ttu-id="4475c-124">In this section, you perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="4475c-124">In this section, you perform the following tasks:</span></span>

- <span data-ttu-id="4475c-125">Get the MAC address of the SensorTag for Bluetooth connection.</span><span class="sxs-lookup"><span data-stu-id="4475c-125">Get the MAC address of the SensorTag for Bluetooth connection.</span></span>
- <span data-ttu-id="4475c-126">Initiate a Bluetooth connection from the IoT gateway to the SensorTag.</span><span class="sxs-lookup"><span data-stu-id="4475c-126">Initiate a Bluetooth connection from the IoT gateway to the SensorTag.</span></span>

### <a name="get-the-mac-address-of-the-sensortag-for-bluetooth-connection"></a><span data-ttu-id="4475c-127">Get the MAC address of the SensorTag for Bluetooth connection</span><span class="sxs-lookup"><span data-stu-id="4475c-127">Get the MAC address of the SensorTag for Bluetooth connection</span></span>

1. <span data-ttu-id="4475c-128">On the host computer, run the SSH client and connect to the IoT gateway.</span><span class="sxs-lookup"><span data-stu-id="4475c-128">On the host computer, run the SSH client and connect to the IoT gateway.</span></span>
1. <span data-ttu-id="4475c-129">Unblock Bluetooth by running the following command:</span><span class="sxs-lookup"><span data-stu-id="4475c-129">Unblock Bluetooth by running the following command:</span></span>

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. <span data-ttu-id="4475c-130">Start the Bluetooth service on the IoT gateway and enter a Bluetooth shell to configure Bluetooth by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="4475c-130">Start the Bluetooth service on the IoT gateway and enter a Bluetooth shell to configure Bluetooth by running the following commands:</span></span>

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. <span data-ttu-id="4475c-131">Power on the Bluetooth controller by running the following command at the Bluetooth shell:</span><span class="sxs-lookup"><span data-stu-id="4475c-131">Power on the Bluetooth controller by running the following command at the Bluetooth shell:</span></span>

   ```bash
   power on
   ```

   ![power on the Bluetooth controller on the IoT gateway with bluetoothctl](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="4475c-133">Start scanning for nearby Bluetooth devices by running the following command:</span><span class="sxs-lookup"><span data-stu-id="4475c-133">Start scanning for nearby Bluetooth devices by running the following command:</span></span>

   ```bash
   scan on
   ```

   ![Scan nearby Bluetooth devices with bluetoothctl](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="4475c-135">Press the pairing button on the SensorTag.</span><span class="sxs-lookup"><span data-stu-id="4475c-135">Press the pairing button on the SensorTag.</span></span> <span data-ttu-id="4475c-136">The green LED on the SensorTag flashes.</span><span class="sxs-lookup"><span data-stu-id="4475c-136">The green LED on the SensorTag flashes.</span></span>
1. <span data-ttu-id="4475c-137">At the Bluetooth shell, you should see the SensorTag is found.</span><span class="sxs-lookup"><span data-stu-id="4475c-137">At the Bluetooth shell, you should see the SensorTag is found.</span></span> <span data-ttu-id="4475c-138">Make a note of the MAC address of the SensorTag.</span><span class="sxs-lookup"><span data-stu-id="4475c-138">Make a note of the MAC address of the SensorTag.</span></span> <span data-ttu-id="4475c-139">In this example, the MAC address of the SensorTag is `24:71:89:C0:7F:82`.</span><span class="sxs-lookup"><span data-stu-id="4475c-139">In this example, the MAC address of the SensorTag is `24:71:89:C0:7F:82`.</span></span>
1. <span data-ttu-id="4475c-140">Turn off the scan by running the following command:</span><span class="sxs-lookup"><span data-stu-id="4475c-140">Turn off the scan by running the following command:</span></span>

   ```bash
   scan off
   ```

   ![Stop scanning nearby Bluetooth devices with bluetoothctl](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-the-iot-gateway-to-the-sensortag"></a><span data-ttu-id="4475c-142">Initiate a Bluetooth connection from the IoT gateway to the SensorTag</span><span class="sxs-lookup"><span data-stu-id="4475c-142">Initiate a Bluetooth connection from the IoT gateway to the SensorTag</span></span>

1. <span data-ttu-id="4475c-143">Connect to the SensorTag by running the following command:</span><span class="sxs-lookup"><span data-stu-id="4475c-143">Connect to the SensorTag by running the following command:</span></span>

   ```bash
   connect <MAC address>
   ```

   ![Connect to the SensorTag with bluetoothctl](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="4475c-145">Disconnect from the SensorTag and exit the Bluetooth shell by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="4475c-145">Disconnect from the SensorTag and exit the Bluetooth shell by running the following commands:</span></span>

   ```bash
   disconnect
   exit
   ```

   ![Disconnect from the SensorTag with bluetoothctl](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

<span data-ttu-id="4475c-147">You've successfully enabled the connection between the SensorTag and the IoT gateway.</span><span class="sxs-lookup"><span data-stu-id="4475c-147">You've successfully enabled the connection between the SensorTag and the IoT gateway.</span></span>

## <a name="run-a-ble-sample-application-to-send-sensortag-data-to-your-iot-hub"></a><span data-ttu-id="4475c-148">Run a BLE sample application to send SensorTag data to your IoT hub</span><span class="sxs-lookup"><span data-stu-id="4475c-148">Run a BLE sample application to send SensorTag data to your IoT hub</span></span>

<span data-ttu-id="4475c-149">The Bluetooth Low Energy (BLE) sample application is provided by the Azure IoT gateway SDK.</span><span class="sxs-lookup"><span data-stu-id="4475c-149">The Bluetooth Low Energy (BLE) sample application is provided by the Azure IoT gateway SDK.</span></span> <span data-ttu-id="4475c-150">The sample application collects data from BLE connection and send the data to you IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4475c-150">The sample application collects data from BLE connection and send the data to you IoT hub.</span></span> <span data-ttu-id="4475c-151">To run the sample application, you need to:</span><span class="sxs-lookup"><span data-stu-id="4475c-151">To run the sample application, you need to:</span></span>

1. <span data-ttu-id="4475c-152">Configure the sample application.</span><span class="sxs-lookup"><span data-stu-id="4475c-152">Configure the sample application.</span></span>
1. <span data-ttu-id="4475c-153">Run the sample application on the IoT gateway.</span><span class="sxs-lookup"><span data-stu-id="4475c-153">Run the sample application on the IoT gateway.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="4475c-154">Configure the sample application</span><span class="sxs-lookup"><span data-stu-id="4475c-154">Configure the sample application</span></span>

1. <span data-ttu-id="4475c-155">Go to the folder of the sample application by running the following command:</span><span class="sxs-lookup"><span data-stu-id="4475c-155">Go to the folder of the sample application by running the following command:</span></span>

   ```bash
   cd /user/share/azureiotgatewaysdk/samples
   ```

1. <span data-ttu-id="4475c-156">Open the configuration file by running the following command:</span><span class="sxs-lookup"><span data-stu-id="4475c-156">Open the configuration file by running the following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="4475c-157">In the configuration file, fill in the following values:</span><span class="sxs-lookup"><span data-stu-id="4475c-157">In the configuration file, fill in the following values:</span></span>

   <span data-ttu-id="4475c-158">**IoTHubName**: The name of your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4475c-158">**IoTHubName**: The name of your IoT hub.</span></span>

   <span data-ttu-id="4475c-159">**IoTHubSuffix**: Get IoTHubSuffix from the primary key of the device connection string that you noted down.</span><span class="sxs-lookup"><span data-stu-id="4475c-159">**IoTHubSuffix**: Get IoTHubSuffix from the primary key of the device connection string that you noted down.</span></span> <span data-ttu-id="4475c-160">Ensure that you get the primary key of the device connection string, not the primary key of your IoT hub connection string.</span><span class="sxs-lookup"><span data-stu-id="4475c-160">Ensure that you get the primary key of the device connection string, not the primary key of your IoT hub connection string.</span></span> <span data-ttu-id="4475c-161">The primary key of the device connection string is in the format of `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span><span class="sxs-lookup"><span data-stu-id="4475c-161">The primary key of the device connection string is in the format of `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span></span>

   <span data-ttu-id="4475c-162">**Transport**: The default value is `amqp`.</span><span class="sxs-lookup"><span data-stu-id="4475c-162">**Transport**: The default value is `amqp`.</span></span> <span data-ttu-id="4475c-163">This value shows the protocol during transpotation.</span><span class="sxs-lookup"><span data-stu-id="4475c-163">This value shows the protocol during transpotation.</span></span> <span data-ttu-id="4475c-164">It could be `http`, `amqp`, or `mqtt`.</span><span class="sxs-lookup"><span data-stu-id="4475c-164">It could be `http`, `amqp`, or `mqtt`.</span></span>

   <span data-ttu-id="4475c-165">**macAddress**: The MAC address of the SensorTag that you noted down.</span><span class="sxs-lookup"><span data-stu-id="4475c-165">**macAddress**: The MAC address of the SensorTag that you noted down.</span></span>

   <span data-ttu-id="4475c-166">**deviceID**: ID of the device that you created in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4475c-166">**deviceID**: ID of the device that you created in your IoT hub.</span></span>

   <span data-ttu-id="4475c-167">**deviceKey**: The primary key of the device connection string.</span><span class="sxs-lookup"><span data-stu-id="4475c-167">**deviceKey**: The primary key of the device connection string.</span></span>

   ![Complete the config file of the BLE sample application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. <span data-ttu-id="4475c-169">Press `ESC` and type `:wq` to save the file.</span><span class="sxs-lookup"><span data-stu-id="4475c-169">Press `ESC` and type `:wq` to save the file.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="4475c-170">Run the sample application</span><span class="sxs-lookup"><span data-stu-id="4475c-170">Run the sample application</span></span>

1. <span data-ttu-id="4475c-171">Make sure the SensorTag is powered on.</span><span class="sxs-lookup"><span data-stu-id="4475c-171">Make sure the SensorTag is powered on.</span></span>
1. <span data-ttu-id="4475c-172">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="4475c-172">Run the following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="4475c-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="4475c-173">Next steps</span></span>

[<span data-ttu-id="4475c-174">Use IoT gateway for sensor data transformation with Azure IoT Gateway SDK</span><span class="sxs-lookup"><span data-stu-id="4475c-174">Use IoT gateway for sensor data transformation with Azure IoT Gateway SDK</span></span>](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)






