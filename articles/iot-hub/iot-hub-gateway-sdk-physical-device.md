---
title: Use a physical device with the Azure IoT Gateway SDK | Microsoft Docs
description: How to use a Texas Instruments SensorTag device to send data to an IoT hub through a gateway running on a Raspberry Pi 3 device. The gateway is built using the Azure IoT Gateway SDK.
services: iot-hub
documentationcenter: ''
author: chipalost
manager: timlt
editor: ''
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: andbuc
ms.openlocfilehash: 6a299e144e86d474c1a908a8c2a8931d619c0fcb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552389"
---
# <a name="use-the-azure-iot-gateway-sdk-to-send-device-to-cloud-messages-with-a-physical-device-linux"></a><span data-ttu-id="7b629-104">Use the Azure IoT Gateway SDK to send device-to-cloud messages with a physical device (Linux)</span><span class="sxs-lookup"><span data-stu-id="7b629-104">Use the Azure IoT Gateway SDK to send device-to-cloud messages with a physical device (Linux)</span></span>

<span data-ttu-id="7b629-105">This walkthrough of the [Bluetooth low energy sample][lnk-ble-samplecode] shows you how to use the [Azure IoT Gateway SDK][lnk-sdk] to:</span><span class="sxs-lookup"><span data-stu-id="7b629-105">This walkthrough of the [Bluetooth low energy sample][lnk-ble-samplecode] shows you how to use the [Azure IoT Gateway SDK][lnk-sdk] to:</span></span>

* <span data-ttu-id="7b629-106">Forward device-to-cloud telemetry to IoT Hub from a physical device.</span><span class="sxs-lookup"><span data-stu-id="7b629-106">Forward device-to-cloud telemetry to IoT Hub from a physical device.</span></span>
* <span data-ttu-id="7b629-107">Route commands from IoT Hub to a physical device.</span><span class="sxs-lookup"><span data-stu-id="7b629-107">Route commands from IoT Hub to a physical device.</span></span>

<span data-ttu-id="7b629-108">This walkthrough covers:</span><span class="sxs-lookup"><span data-stu-id="7b629-108">This walkthrough covers:</span></span>

* <span data-ttu-id="7b629-109">**Architecture**: important architectural information about the Bluetooth low energy sample.</span><span class="sxs-lookup"><span data-stu-id="7b629-109">**Architecture**: important architectural information about the Bluetooth low energy sample.</span></span>
* <span data-ttu-id="7b629-110">**Build and run**: the steps required to build and run the sample.</span><span class="sxs-lookup"><span data-stu-id="7b629-110">**Build and run**: the steps required to build and run the sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="7b629-111">Architecture</span><span class="sxs-lookup"><span data-stu-id="7b629-111">Architecture</span></span>

<span data-ttu-id="7b629-112">The walkthrough shows you how to build and run an IoT Gateway on a Raspberry Pi 3 that runs Raspbian Linux.</span><span class="sxs-lookup"><span data-stu-id="7b629-112">The walkthrough shows you how to build and run an IoT Gateway on a Raspberry Pi 3 that runs Raspbian Linux.</span></span> <span data-ttu-id="7b629-113">The gateway is built using the IoT Gateway SDK.</span><span class="sxs-lookup"><span data-stu-id="7b629-113">The gateway is built using the IoT Gateway SDK.</span></span> <span data-ttu-id="7b629-114">The sample uses a Texas Instruments SensorTag Bluetooth Low Energy (BLE) device to collect temperature data.</span><span class="sxs-lookup"><span data-stu-id="7b629-114">The sample uses a Texas Instruments SensorTag Bluetooth Low Energy (BLE) device to collect temperature data.</span></span>

<span data-ttu-id="7b629-115">When you run the gateway it:</span><span class="sxs-lookup"><span data-stu-id="7b629-115">When you run the gateway it:</span></span>

* <span data-ttu-id="7b629-116">Connects to a SensorTag device using the Bluetooth Low Energy (BLE) protocol.</span><span class="sxs-lookup"><span data-stu-id="7b629-116">Connects to a SensorTag device using the Bluetooth Low Energy (BLE) protocol.</span></span>
* <span data-ttu-id="7b629-117">Connects to IoT Hub using the HTTP protocol.</span><span class="sxs-lookup"><span data-stu-id="7b629-117">Connects to IoT Hub using the HTTP protocol.</span></span>
* <span data-ttu-id="7b629-118">Forwards telemetry from the SensorTag device to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7b629-118">Forwards telemetry from the SensorTag device to IoT Hub.</span></span>
* <span data-ttu-id="7b629-119">Routes commands from IoT Hub to the SensorTag device.</span><span class="sxs-lookup"><span data-stu-id="7b629-119">Routes commands from IoT Hub to the SensorTag device.</span></span>

<span data-ttu-id="7b629-120">The gateway contains the following modules:</span><span class="sxs-lookup"><span data-stu-id="7b629-120">The gateway contains the following modules:</span></span>

* <span data-ttu-id="7b629-121">A *BLE module* that interfaces with a BLE device to receive temperature data from the device and send commands to the device.</span><span class="sxs-lookup"><span data-stu-id="7b629-121">A *BLE module* that interfaces with a BLE device to receive temperature data from the device and send commands to the device.</span></span>
* <span data-ttu-id="7b629-122">A *BLE Cloud to Device module* that translates the JSON messages coming from the cloud into BLE instructions for the *BLE module*.</span><span class="sxs-lookup"><span data-stu-id="7b629-122">A *BLE Cloud to Device module* that translates the JSON messages coming from the cloud into BLE instructions for the *BLE module*.</span></span>
* <span data-ttu-id="7b629-123">A *logger module* that logs all gateway messages to a local file.</span><span class="sxs-lookup"><span data-stu-id="7b629-123">A *logger module* that logs all gateway messages to a local file.</span></span>
* <span data-ttu-id="7b629-124">An *identity mapping module* that translates between BLE device MAC addresses and Azure IoT Hub device identities.</span><span class="sxs-lookup"><span data-stu-id="7b629-124">An *identity mapping module* that translates between BLE device MAC addresses and Azure IoT Hub device identities.</span></span>
* <span data-ttu-id="7b629-125">An *IoT Hub module* that uploads telemetry data to an IoT hub and receives device commands from an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="7b629-125">An *IoT Hub module* that uploads telemetry data to an IoT hub and receives device commands from an IoT hub.</span></span>
* <span data-ttu-id="7b629-126">A *BLE printer module* that interprets telemetry from the BLE device and prints formatted data to the console to enable troubleshooting and debugging.</span><span class="sxs-lookup"><span data-stu-id="7b629-126">A *BLE printer module* that interprets telemetry from the BLE device and prints formatted data to the console to enable troubleshooting and debugging.</span></span>

### <a name="how-data-flows-through-the-gateway"></a><span data-ttu-id="7b629-127">How data flows through the gateway</span><span class="sxs-lookup"><span data-stu-id="7b629-127">How data flows through the gateway</span></span>

<span data-ttu-id="7b629-128">The following block diagram illustrates the telemetry upload data flow pipeline:</span><span class="sxs-lookup"><span data-stu-id="7b629-128">The following block diagram illustrates the telemetry upload data flow pipeline:</span></span>

![Telemetry upload gateway pipeline](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-sdk-physical-device/gateway_ble_upload_data_flow.png)

<span data-ttu-id="7b629-130">The steps that an item of telemetry takes traveling from a BLE device to IoT Hub are:</span><span class="sxs-lookup"><span data-stu-id="7b629-130">The steps that an item of telemetry takes traveling from a BLE device to IoT Hub are:</span></span>

1. <span data-ttu-id="7b629-131">The BLE device generates a temperature sample and sends it over Bluetooth to the BLE module in the gateway.</span><span class="sxs-lookup"><span data-stu-id="7b629-131">The BLE device generates a temperature sample and sends it over Bluetooth to the BLE module in the gateway.</span></span>
1. <span data-ttu-id="7b629-132">The BLE module receives the sample and publishes it to the broker along with the MAC address of the device.</span><span class="sxs-lookup"><span data-stu-id="7b629-132">The BLE module receives the sample and publishes it to the broker along with the MAC address of the device.</span></span>
1. <span data-ttu-id="7b629-133">The identity mapping module picks up this message and uses an internal table to translate the MAC address of the device into an IoT Hub device identity.</span><span class="sxs-lookup"><span data-stu-id="7b629-133">The identity mapping module picks up this message and uses an internal table to translate the MAC address of the device into an IoT Hub device identity.</span></span> <span data-ttu-id="7b629-134">An IoT Hub device identity consists of a device ID and device key.</span><span class="sxs-lookup"><span data-stu-id="7b629-134">An IoT Hub device identity consists of a device ID and device key.</span></span> <span data-ttu-id="7b629-135">The module then publishes a new message that contains the temperature sample data, the MAC address of the device, the device ID, and the device key.</span><span class="sxs-lookup"><span data-stu-id="7b629-135">The module then publishes a new message that contains the temperature sample data, the MAC address of the device, the device ID, and the device key.</span></span>
1. <span data-ttu-id="7b629-136">The IoT Hub module receives this new message (generated by the identity mapping module) and publishes it to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7b629-136">The IoT Hub module receives this new message (generated by the identity mapping module) and publishes it to IoT Hub.</span></span>
1. <span data-ttu-id="7b629-137">The logger module logs all messages from the broker to a local file.</span><span class="sxs-lookup"><span data-stu-id="7b629-137">The logger module logs all messages from the broker to a local file.</span></span>

<span data-ttu-id="7b629-138">The following block diagram illustrates the device command data flow pipeline:</span><span class="sxs-lookup"><span data-stu-id="7b629-138">The following block diagram illustrates the device command data flow pipeline:</span></span>

![Device command gateway pipeline](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-gateway-sdk-physical-device/gateway_ble_command_data_flow.png)

1. <span data-ttu-id="7b629-140">The IoT Hub module periodically polls the IoT hub for new command messages.</span><span class="sxs-lookup"><span data-stu-id="7b629-140">The IoT Hub module periodically polls the IoT hub for new command messages.</span></span>
1. <span data-ttu-id="7b629-141">When the IoT Hub module receives a new command message, it publishes it to the broker.</span><span class="sxs-lookup"><span data-stu-id="7b629-141">When the IoT Hub module receives a new command message, it publishes it to the broker.</span></span>
1. <span data-ttu-id="7b629-142">The identity mapping module picks up the command message and uses an internal table to translate the IoT Hub device ID to a device MAC address.</span><span class="sxs-lookup"><span data-stu-id="7b629-142">The identity mapping module picks up the command message and uses an internal table to translate the IoT Hub device ID to a device MAC address.</span></span> <span data-ttu-id="7b629-143">It then publishes a new message that includes the MAC address of the target device in the properties map of the message.</span><span class="sxs-lookup"><span data-stu-id="7b629-143">It then publishes a new message that includes the MAC address of the target device in the properties map of the message.</span></span>
1. <span data-ttu-id="7b629-144">The BLE Cloud-to-Device module picks up this message and translates it into the proper BLE instruction for the BLE module.</span><span class="sxs-lookup"><span data-stu-id="7b629-144">The BLE Cloud-to-Device module picks up this message and translates it into the proper BLE instruction for the BLE module.</span></span> <span data-ttu-id="7b629-145">It then publishes a new message.</span><span class="sxs-lookup"><span data-stu-id="7b629-145">It then publishes a new message.</span></span>
1. <span data-ttu-id="7b629-146">The BLE module picks up this message and executes the I/O instruction by communicating with the BLE device.</span><span class="sxs-lookup"><span data-stu-id="7b629-146">The BLE module picks up this message and executes the I/O instruction by communicating with the BLE device.</span></span>
1. <span data-ttu-id="7b629-147">The logger module logs all messages from the broker to a disk file.</span><span class="sxs-lookup"><span data-stu-id="7b629-147">The logger module logs all messages from the broker to a disk file.</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="7b629-148">Prepare your hardware</span><span class="sxs-lookup"><span data-stu-id="7b629-148">Prepare your hardware</span></span>

<span data-ttu-id="7b629-149">This tutorial assumes you are using a [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) device connected to a Raspberry Pi 3 running Raspbian.</span><span class="sxs-lookup"><span data-stu-id="7b629-149">This tutorial assumes you are using a [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) device connected to a Raspberry Pi 3 running Raspbian.</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="7b629-150">Install Raspbian</span><span class="sxs-lookup"><span data-stu-id="7b629-150">Install Raspbian</span></span>

<span data-ttu-id="7b629-151">You can use either of the following options to install Raspbian on your Raspberry Pi 3 device.</span><span class="sxs-lookup"><span data-stu-id="7b629-151">You can use either of the following options to install Raspbian on your Raspberry Pi 3 device.</span></span>

* <span data-ttu-id="7b629-152">To install the latest version of Raspbian, use the [NOOBS][lnk-noobs] graphical user interface.</span><span class="sxs-lookup"><span data-stu-id="7b629-152">To install the latest version of Raspbian, use the [NOOBS][lnk-noobs] graphical user interface.</span></span>
* <span data-ttu-id="7b629-153">Manually [download][lnk-raspbian] and write the latest image of the Raspbian operating system to an SD card.</span><span class="sxs-lookup"><span data-stu-id="7b629-153">Manually [download][lnk-raspbian] and write the latest image of the Raspbian operating system to an SD card.</span></span>

### <a name="install-bluez-537"></a><span data-ttu-id="7b629-154">Install BlueZ 5.37</span><span class="sxs-lookup"><span data-stu-id="7b629-154">Install BlueZ 5.37</span></span>

<span data-ttu-id="7b629-155">The BLE modules talk to the Bluetooth hardware via the BlueZ stack.</span><span class="sxs-lookup"><span data-stu-id="7b629-155">The BLE modules talk to the Bluetooth hardware via the BlueZ stack.</span></span> <span data-ttu-id="7b629-156">You need version 5.37 of BlueZ for the modules to work correctly.</span><span class="sxs-lookup"><span data-stu-id="7b629-156">You need version 5.37 of BlueZ for the modules to work correctly.</span></span> <span data-ttu-id="7b629-157">These instructions make sure the correct version of BlueZ is installed.</span><span class="sxs-lookup"><span data-stu-id="7b629-157">These instructions make sure the correct version of BlueZ is installed.</span></span>

1. <span data-ttu-id="7b629-158">Stop the current bluetooth daemon:</span><span class="sxs-lookup"><span data-stu-id="7b629-158">Stop the current bluetooth daemon:</span></span>

    `sudo systemctl stop bluetooth`

1. <span data-ttu-id="7b629-159">Install the BlueZ dependencies:</span><span class="sxs-lookup"><span data-stu-id="7b629-159">Install the BlueZ dependencies:</span></span>

    `sudo apt-get update`

    `sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev`

1. <span data-ttu-id="7b629-160">Download the BlueZ source code from bluez.org:</span><span class="sxs-lookup"><span data-stu-id="7b629-160">Download the BlueZ source code from bluez.org:</span></span>

    `wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz`

1. <span data-ttu-id="7b629-161">Unzip the source code:</span><span class="sxs-lookup"><span data-stu-id="7b629-161">Unzip the source code:</span></span>

    `tar -xvf bluez-5.37.tar.xz`

1. <span data-ttu-id="7b629-162">Change directories to the newly created folder:</span><span class="sxs-lookup"><span data-stu-id="7b629-162">Change directories to the newly created folder:</span></span>

    `cd bluez-5.37`

1. <span data-ttu-id="7b629-163">Configure the BlueZ code to be built:</span><span class="sxs-lookup"><span data-stu-id="7b629-163">Configure the BlueZ code to be built:</span></span>

    `./configure --disable-udev --disable-systemd --enable-experimental`

1. <span data-ttu-id="7b629-164">Build BlueZ:</span><span class="sxs-lookup"><span data-stu-id="7b629-164">Build BlueZ:</span></span>

    `make`

1. <span data-ttu-id="7b629-165">Install BlueZ once it is done building:</span><span class="sxs-lookup"><span data-stu-id="7b629-165">Install BlueZ once it is done building:</span></span>

    `sudo make install`

1. <span data-ttu-id="7b629-166">Change systemd service configuration for bluetooth so it points to the new bluetooth daemon in the file `/lib/systemd/system/bluetooth.service`.</span><span class="sxs-lookup"><span data-stu-id="7b629-166">Change systemd service configuration for bluetooth so it points to the new bluetooth daemon in the file `/lib/systemd/system/bluetooth.service`.</span></span> <span data-ttu-id="7b629-167">Replace the 'ExecStart' line with the following text:</span><span class="sxs-lookup"><span data-stu-id="7b629-167">Replace the 'ExecStart' line with the following text:</span></span>

    `ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E`

### <a name="enable-connectivity-to-the-sensortag-device-from-your-raspberry-pi-3-device"></a><span data-ttu-id="7b629-168">Enable connectivity to the SensorTag device from your Raspberry Pi 3 device</span><span class="sxs-lookup"><span data-stu-id="7b629-168">Enable connectivity to the SensorTag device from your Raspberry Pi 3 device</span></span>

<span data-ttu-id="7b629-169">Before running the sample, you need to verify that your Raspberry Pi 3 can connect to the SensorTag device.</span><span class="sxs-lookup"><span data-stu-id="7b629-169">Before running the sample, you need to verify that your Raspberry Pi 3 can connect to the SensorTag device.</span></span>


1. <span data-ttu-id="7b629-170">Ensure the `rfkill` utility is installed:</span><span class="sxs-lookup"><span data-stu-id="7b629-170">Ensure the `rfkill` utility is installed:</span></span>

    `sudo apt-get install rfkill`

1. <span data-ttu-id="7b629-171">Unblock bluetooth on the Raspberry Pi 3 and check that the version number is **5.37**:</span><span class="sxs-lookup"><span data-stu-id="7b629-171">Unblock bluetooth on the Raspberry Pi 3 and check that the version number is **5.37**:</span></span>

    `sudo rfkill unblock bluetooth`

    `bluetoothctl --version`

1. <span data-ttu-id="7b629-172">Start the bluetooth service and execute the **bluetoothctl** command to enter an interactive bluetooth shell:</span><span class="sxs-lookup"><span data-stu-id="7b629-172">Start the bluetooth service and execute the **bluetoothctl** command to enter an interactive bluetooth shell:</span></span>

    `sudo systemctl start bluetooth`

    `bluetoothctl`

1. <span data-ttu-id="7b629-173">Enter the command **power on** to power up the bluetooth controller.</span><span class="sxs-lookup"><span data-stu-id="7b629-173">Enter the command **power on** to power up the bluetooth controller.</span></span> <span data-ttu-id="7b629-174">You see output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="7b629-174">You see output similar to the following:</span></span>

    ```
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. <span data-ttu-id="7b629-175">In the interactive bluetooth shell, enter the command **scan on** to scan for bluetooth devices.</span><span class="sxs-lookup"><span data-stu-id="7b629-175">In the interactive bluetooth shell, enter the command **scan on** to scan for bluetooth devices.</span></span> <span data-ttu-id="7b629-176">You  see output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="7b629-176">You  see output similar to the following:</span></span>

    ```
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. <span data-ttu-id="7b629-177">Make the SensorTag device discoverable by pressing the small button (the green LED should flash).</span><span class="sxs-lookup"><span data-stu-id="7b629-177">Make the SensorTag device discoverable by pressing the small button (the green LED should flash).</span></span> <span data-ttu-id="7b629-178">The Raspberry Pi 3 should discover the SensorTag device:</span><span class="sxs-lookup"><span data-stu-id="7b629-178">The Raspberry Pi 3 should discover the SensorTag device:</span></span>

    ```
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    <span data-ttu-id="7b629-179">In this example, you can see that the MAC address of the SensorTag device is **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="7b629-179">In this example, you can see that the MAC address of the SensorTag device is **A0:E6:F8:B5:F6:00**.</span></span>

1. <span data-ttu-id="7b629-180">Turn off scanning by entering the **scan off** command:</span><span class="sxs-lookup"><span data-stu-id="7b629-180">Turn off scanning by entering the **scan off** command:</span></span>

    ```
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. <span data-ttu-id="7b629-181">Connect to your SensorTag device using its MAC address by entering **connect \<MAC address\>**.</span><span class="sxs-lookup"><span data-stu-id="7b629-181">Connect to your SensorTag device using its MAC address by entering **connect \<MAC address\>**.</span></span> <span data-ttu-id="7b629-182">The following sample output is abbreviated for clarity:</span><span class="sxs-lookup"><span data-stu-id="7b629-182">The following sample output is abbreviated for clarity:</span></span>

    ```
    Attempting to connect to A0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > <span data-ttu-id="7b629-183">You can list the GATT characteristics of the device again using the **list-attributes** command.</span><span class="sxs-lookup"><span data-stu-id="7b629-183">You can list the GATT characteristics of the device again using the **list-attributes** command.</span></span>

1. <span data-ttu-id="7b629-184">You can now disconnect from the device using the **disconnect** command and then exit from the bluetooth shell using the **quit** command:</span><span class="sxs-lookup"><span data-stu-id="7b629-184">You can now disconnect from the device using the **disconnect** command and then exit from the bluetooth shell using the **quit** command:</span></span>

    ```
    Attempting to disconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

<span data-ttu-id="7b629-185">You're now ready to run the BLE Gateway sample on your Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="7b629-185">You're now ready to run the BLE Gateway sample on your Raspberry Pi 3.</span></span>

## <a name="run-the-ble-gateway-sample"></a><span data-ttu-id="7b629-186">Run the BLE Gateway sample</span><span class="sxs-lookup"><span data-stu-id="7b629-186">Run the BLE Gateway sample</span></span>

<span data-ttu-id="7b629-187">To run the BLE sample, you need to complete three tasks:</span><span class="sxs-lookup"><span data-stu-id="7b629-187">To run the BLE sample, you need to complete three tasks:</span></span>

* <span data-ttu-id="7b629-188">Configure two sample devices in your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7b629-188">Configure two sample devices in your IoT Hub.</span></span>
* <span data-ttu-id="7b629-189">Build the IoT Gateway SDK on your Raspberry Pi 3 device.</span><span class="sxs-lookup"><span data-stu-id="7b629-189">Build the IoT Gateway SDK on your Raspberry Pi 3 device.</span></span>
* <span data-ttu-id="7b629-190">Configure and run the BLE sample on your Raspberry Pi 3 device.</span><span class="sxs-lookup"><span data-stu-id="7b629-190">Configure and run the BLE sample on your Raspberry Pi 3 device.</span></span>

<span data-ttu-id="7b629-191">At the time of writing, the IoT Gateway SDK only supports gateways that use BLE modules on Linux.</span><span class="sxs-lookup"><span data-stu-id="7b629-191">At the time of writing, the IoT Gateway SDK only supports gateways that use BLE modules on Linux.</span></span>

### <a name="configure-two-sample-devices-in-your-iot-hub"></a><span data-ttu-id="7b629-192">Configure two sample devices in your IoT Hub</span><span class="sxs-lookup"><span data-stu-id="7b629-192">Configure two sample devices in your IoT Hub</span></span>

* <span data-ttu-id="7b629-193">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need the name of your hub to complete this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="7b629-193">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need the name of your hub to complete this walkthrough.</span></span> <span data-ttu-id="7b629-194">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="7b629-194">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="7b629-195">Add one device called **SensorTag_01** to your IoT hub and make a note of its id and device key.</span><span class="sxs-lookup"><span data-stu-id="7b629-195">Add one device called **SensorTag_01** to your IoT hub and make a note of its id and device key.</span></span> <span data-ttu-id="7b629-196">You can use the [device explorer or iothub-explorer][lnk-explorer-tools] tools to add this device to the IoT hub you created in the previous step and to retrieve its key.</span><span class="sxs-lookup"><span data-stu-id="7b629-196">You can use the [device explorer or iothub-explorer][lnk-explorer-tools] tools to add this device to the IoT hub you created in the previous step and to retrieve its key.</span></span> <span data-ttu-id="7b629-197">You map this device to the SensorTag device when you configure the gateway.</span><span class="sxs-lookup"><span data-stu-id="7b629-197">You map this device to the SensorTag device when you configure the gateway.</span></span>

### <a name="build-the-azure-iot-gateway-sdk-on-your-raspberry-pi-3"></a><span data-ttu-id="7b629-198">Build the Azure IoT Gateway SDK on your Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="7b629-198">Build the Azure IoT Gateway SDK on your Raspberry Pi 3</span></span>

<span data-ttu-id="7b629-199">Install dependencies for the Azure IoT Gateway SDK:</span><span class="sxs-lookup"><span data-stu-id="7b629-199">Install dependencies for the Azure IoT Gateway SDK:</span></span>

`sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev`

<span data-ttu-id="7b629-200">Use the following commands to clone the IoT Gateway SDK and all its submodules to your home directory:</span><span class="sxs-lookup"><span data-stu-id="7b629-200">Use the following commands to clone the IoT Gateway SDK and all its submodules to your home directory:</span></span>

`cd ~`

`git clone --recursive https://github.com/Azure/azure-iot-gateway-sdk.git`

`cd azure-iot-gateway-sdk`

`git submodule update --init --recursive`

<span data-ttu-id="7b629-201">When you have a complete copy of the IoT Gateway SDK repository on your Raspberry Pi 3, you can build it using the following command from the folder that contains the SDK:</span><span class="sxs-lookup"><span data-stu-id="7b629-201">When you have a complete copy of the IoT Gateway SDK repository on your Raspberry Pi 3, you can build it using the following command from the folder that contains the SDK:</span></span>

`./tools/build.sh`

### <a name="configure-and-run-the-ble-sample-on-your-raspberry-pi-3"></a><span data-ttu-id="7b629-202">Configure and run the BLE sample on your Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="7b629-202">Configure and run the BLE sample on your Raspberry Pi 3</span></span>

<span data-ttu-id="7b629-203">To bootstrap and run the sample, you must configure each module that participates in the gateway.</span><span class="sxs-lookup"><span data-stu-id="7b629-203">To bootstrap and run the sample, you must configure each module that participates in the gateway.</span></span> <span data-ttu-id="7b629-204">This configuration is provided in a JSON file and you must configure all five participating modules.</span><span class="sxs-lookup"><span data-stu-id="7b629-204">This configuration is provided in a JSON file and you must configure all five participating modules.</span></span> <span data-ttu-id="7b629-205">There is a sample JSON file in the repository called **gateway\_sample.json** that you can use as the starting point for building your own configuration file.</span><span class="sxs-lookup"><span data-stu-id="7b629-205">There is a sample JSON file in the repository called **gateway\_sample.json** that you can use as the starting point for building your own configuration file.</span></span> <span data-ttu-id="7b629-206">This file is in the **samples/ble_gateway/src** folder in local copy of the IoT Gateway SDK repository.</span><span class="sxs-lookup"><span data-stu-id="7b629-206">This file is in the **samples/ble_gateway/src** folder in local copy of the IoT Gateway SDK repository.</span></span>

<span data-ttu-id="7b629-207">The following sections describe how to edit this configuration file for the BLE sample and assume that the IoT Gateway SDK repository is in the **/home/pi/azure-iot-gateway-sdk/** folder on your Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="7b629-207">The following sections describe how to edit this configuration file for the BLE sample and assume that the IoT Gateway SDK repository is in the **/home/pi/azure-iot-gateway-sdk/** folder on your Raspberry Pi 3.</span></span> <span data-ttu-id="7b629-208">If the repository is elsewhere, adjust the paths accordingly.</span><span class="sxs-lookup"><span data-stu-id="7b629-208">If the repository is elsewhere, adjust the paths accordingly.</span></span>

#### <a name="logger-configuration"></a><span data-ttu-id="7b629-209">Logger configuration</span><span class="sxs-lookup"><span data-stu-id="7b629-209">Logger configuration</span></span>

<span data-ttu-id="7b629-210">Assuming the gateway repository is located in the **/home/pi/azure-iot-gateway-sdk/** folder, configure the logger module as follows:</span><span class="sxs-lookup"><span data-stu-id="7b629-210">Assuming the gateway repository is located in the **/home/pi/azure-iot-gateway-sdk/** folder, configure the logger module as follows:</span></span>

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a><span data-ttu-id="7b629-211">BLE module configuration</span><span class="sxs-lookup"><span data-stu-id="7b629-211">BLE module configuration</span></span>

<span data-ttu-id="7b629-212">The sample configuration for the BLE device assumes a Texas Instruments SensorTag device.</span><span class="sxs-lookup"><span data-stu-id="7b629-212">The sample configuration for the BLE device assumes a Texas Instruments SensorTag device.</span></span> <span data-ttu-id="7b629-213">Any standard BLE device that can operate as a GATT peripheral should work but you will need to update the GATT characteristic IDs and data (for write instructions).</span><span class="sxs-lookup"><span data-stu-id="7b629-213">Any standard BLE device that can operate as a GATT peripheral should work but you will need to update the GATT characteristic IDs and data (for write instructions).</span></span> <span data-ttu-id="7b629-214">Add the MAC address of your SensorTag device:</span><span class="sxs-lookup"><span data-stu-id="7b629-214">Add the MAC address of your SensorTag device:</span></span>

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

#### <a name="iot-hub-module"></a><span data-ttu-id="7b629-215">IoT Hub module</span><span class="sxs-lookup"><span data-stu-id="7b629-215">IoT Hub module</span></span>

<span data-ttu-id="7b629-216">Add the name of your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7b629-216">Add the name of your IoT Hub.</span></span> <span data-ttu-id="7b629-217">The suffix value is typically **azure-devices.net**:</span><span class="sxs-lookup"><span data-stu-id="7b629-217">The suffix value is typically **azure-devices.net**:</span></span>

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a><span data-ttu-id="7b629-218">Identity mapping module configuration</span><span class="sxs-lookup"><span data-stu-id="7b629-218">Identity mapping module configuration</span></span>

<span data-ttu-id="7b629-219">Add the MAC address of your SensorTag device and the device ID and key of the **SensorTag_01** device you added to your IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="7b629-219">Add the MAC address of your SensorTag device and the device ID and key of the **SensorTag_01** device you added to your IoT Hub:</span></span>

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a><span data-ttu-id="7b629-220">BLE Printer module configuration</span><span class="sxs-lookup"><span data-stu-id="7b629-220">BLE Printer module configuration</span></span>

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a><span data-ttu-id="7b629-221">BLEC2D Module Configuration</span><span class="sxs-lookup"><span data-stu-id="7b629-221">BLEC2D Module Configuration</span></span>

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a><span data-ttu-id="7b629-222">Routing Configuration</span><span class="sxs-lookup"><span data-stu-id="7b629-222">Routing Configuration</span></span>

<span data-ttu-id="7b629-223">The following configuration ensures the following routing between modules:</span><span class="sxs-lookup"><span data-stu-id="7b629-223">The following configuration ensures the following routing between modules:</span></span>

* <span data-ttu-id="7b629-224">The **Logger** module receives and logs all messages.</span><span class="sxs-lookup"><span data-stu-id="7b629-224">The **Logger** module receives and logs all messages.</span></span>
* <span data-ttu-id="7b629-225">The **SensorTag** module sends messages to both the **mapping** and **BLE Printer** modules.</span><span class="sxs-lookup"><span data-stu-id="7b629-225">The **SensorTag** module sends messages to both the **mapping** and **BLE Printer** modules.</span></span>
* <span data-ttu-id="7b629-226">The **mapping** module sends messages to the **IoTHub** module to be sent up to your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7b629-226">The **mapping** module sends messages to the **IoTHub** module to be sent up to your IoT Hub.</span></span>
* <span data-ttu-id="7b629-227">The **IoTHub** module sends messages back to the **mapping** module.</span><span class="sxs-lookup"><span data-stu-id="7b629-227">The **IoTHub** module sends messages back to the **mapping** module.</span></span>
* <span data-ttu-id="7b629-228">The **mapping** module sends messages to the **BLEC2D** module.</span><span class="sxs-lookup"><span data-stu-id="7b629-228">The **mapping** module sends messages to the **BLEC2D** module.</span></span>
* <span data-ttu-id="7b629-229">The **BLEC2D** module sends messages back to the **Sensor Tag** module.</span><span class="sxs-lookup"><span data-stu-id="7b629-229">The **BLEC2D** module sends messages back to the **Sensor Tag** module.</span></span>

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

<span data-ttu-id="7b629-230">To run the sample, pass the path to the JSON configuration file as a parameter to the **ble\_gateway** binary.</span><span class="sxs-lookup"><span data-stu-id="7b629-230">To run the sample, pass the path to the JSON configuration file as a parameter to the **ble\_gateway** binary.</span></span> <span data-ttu-id="7b629-231">The following command assumes you are using the **gateway_sample.json** configuration file.</span><span class="sxs-lookup"><span data-stu-id="7b629-231">The following command assumes you are using the **gateway_sample.json** configuration file.</span></span> <span data-ttu-id="7b629-232">Execute this command from the **azure-iot-gateway-sdk** folder on the Raspberry Pi:</span><span class="sxs-lookup"><span data-stu-id="7b629-232">Execute this command from the **azure-iot-gateway-sdk** folder on the Raspberry Pi:</span></span>

```
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

<span data-ttu-id="7b629-233">You may need to press the small button on the SensorTag device to make it discoverable before you run the sample.</span><span class="sxs-lookup"><span data-stu-id="7b629-233">You may need to press the small button on the SensorTag device to make it discoverable before you run the sample.</span></span>

<span data-ttu-id="7b629-234">When you run the sample, you can use the [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to monitor the messages the gateway forwards from the SensorTag device.</span><span class="sxs-lookup"><span data-stu-id="7b629-234">When you run the sample, you can use the [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to monitor the messages the gateway forwards from the SensorTag device.</span></span>

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="7b629-235">Send cloud-to-device messages</span><span class="sxs-lookup"><span data-stu-id="7b629-235">Send cloud-to-device messages</span></span>

<span data-ttu-id="7b629-236">The BLE module also supports sending commands from IoT Hub to the device.</span><span class="sxs-lookup"><span data-stu-id="7b629-236">The BLE module also supports sending commands from IoT Hub to the device.</span></span> <span data-ttu-id="7b629-237">You can use the [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to send JSON messages that the BLE gateway module forwards on to the BLE device.</span><span class="sxs-lookup"><span data-stu-id="7b629-237">You can use the [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to send JSON messages that the BLE gateway module forwards on to the BLE device.</span></span>

<span data-ttu-id="7b629-238">If you are using the Texas Instruments SensorTag device, you can turn on the red LED, green LED, or buzzer by sending commands from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7b629-238">If you are using the Texas Instruments SensorTag device, you can turn on the red LED, green LED, or buzzer by sending commands from IoT Hub.</span></span> <span data-ttu-id="7b629-239">Before you send commands from IoT Hub, first send the following two JSON messages in order.</span><span class="sxs-lookup"><span data-stu-id="7b629-239">Before you send commands from IoT Hub, first send the following two JSON messages in order.</span></span> <span data-ttu-id="7b629-240">Then you can send any of the commands to turn on the lights or buzzer.</span><span class="sxs-lookup"><span data-stu-id="7b629-240">Then you can send any of the commands to turn on the lights or buzzer.</span></span>

1. <span data-ttu-id="7b629-241">Reset all LEDs and the buzzer (turn them off):</span><span class="sxs-lookup"><span data-stu-id="7b629-241">Reset all LEDs and the buzzer (turn them off):</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. <span data-ttu-id="7b629-242">Configure I/O as 'remote':</span><span class="sxs-lookup"><span data-stu-id="7b629-242">Configure I/O as 'remote':</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

<span data-ttu-id="7b629-243">Now you can send any of the following commands to turn on the lights or buzzer on the SensorTag device:</span><span class="sxs-lookup"><span data-stu-id="7b629-243">Now you can send any of the following commands to turn on the lights or buzzer on the SensorTag device:</span></span>

* <span data-ttu-id="7b629-244">Turn on the red LED:</span><span class="sxs-lookup"><span data-stu-id="7b629-244">Turn on the red LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* <span data-ttu-id="7b629-245">Turn on the green LED:</span><span class="sxs-lookup"><span data-stu-id="7b629-245">Turn on the green LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* <span data-ttu-id="7b629-246">Turn on the buzzer:</span><span class="sxs-lookup"><span data-stu-id="7b629-246">Turn on the buzzer:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="7b629-247">Next Steps</span><span class="sxs-lookup"><span data-stu-id="7b629-247">Next Steps</span></span>

<span data-ttu-id="7b629-248">If you want to gain a more advanced understanding of the IoT Gateway SDK and experiment with some code examples, visit the following developer tutorials and resources:</span><span class="sxs-lookup"><span data-stu-id="7b629-248">If you want to gain a more advanced understanding of the IoT Gateway SDK and experiment with some code examples, visit the following developer tutorials and resources:</span></span>

* <span data-ttu-id="7b629-249">[Azure IoT Gateway SDK][lnk-sdk]</span><span class="sxs-lookup"><span data-stu-id="7b629-249">[Azure IoT Gateway SDK][lnk-sdk]</span></span>

<span data-ttu-id="7b629-250">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="7b629-250">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="7b629-251">[IoT Hub developer guide][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="7b629-251">[IoT Hub developer guide][lnk-devguide]</span></span>

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/azure-iot-gateway-sdk/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/azure-iot-gateway-sdk/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/


[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 


