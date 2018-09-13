---
title: Intel Edison to cloud (Node.js) - Connect Intel Edison to Azure IoT Hub | Microsoft Docs
description: Learn how to setup and connect Intel Edison to Azure IoT Hub for Intel Edison to send data to the Azure cloud platform in this tutorial.
author: rangv
manager: ''
keywords: azure iot intel edison, intel edison iot hub, intel edison send data to cloud, intel edison to cloud
ms.service: iot-hub
services: iot-hub
ms.devlang: nodejs
ms.topic: conceptual
ms.date: 04/11/2018
ms.author: rangv
ms.openlocfilehash: 5adb6e6119856879e52836a8d3a797a7b40c6fe8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44826540"
---
# <a name="connect-intel-edison-to-azure-iot-hub-nodejs"></a><span data-ttu-id="3b53f-104">Connect Intel Edison to Azure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="3b53f-104">Connect Intel Edison to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="3b53f-105">In this tutorial, you begin by learning the basics of working with Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="3b53f-105">In this tutorial, you begin by learning the basics of working with Intel Edison.</span></span> <span data-ttu-id="3b53f-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](about-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="3b53f-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](about-iot-hub.md).</span></span>

<span data-ttu-id="3b53f-107">Don't have a kit yet?</span><span class="sxs-lookup"><span data-stu-id="3b53f-107">Don't have a kit yet?</span></span> <span data-ttu-id="3b53f-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span><span class="sxs-lookup"><span data-stu-id="3b53f-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="3b53f-109">What you do</span><span class="sxs-lookup"><span data-stu-id="3b53f-109">What you do</span></span>

* <span data-ttu-id="3b53f-110">Setup Intel Edison and Grove modules.</span><span class="sxs-lookup"><span data-stu-id="3b53f-110">Setup Intel Edison and Grove modules.</span></span>
* <span data-ttu-id="3b53f-111">Create an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3b53f-111">Create an IoT hub.</span></span>
* <span data-ttu-id="3b53f-112">Register a device for Edison in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3b53f-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="3b53f-113">Run a sample application on Edison to send sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3b53f-113">Run a sample application on Edison to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="3b53f-114">Connect Intel Edison to an IoT hub that you create.</span><span class="sxs-lookup"><span data-stu-id="3b53f-114">Connect Intel Edison to an IoT hub that you create.</span></span> <span data-ttu-id="3b53f-115">Then you run a sample application on Edison to collect temperature and humidity data from a Grove temperature sensor.</span><span class="sxs-lookup"><span data-stu-id="3b53f-115">Then you run a sample application on Edison to collect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="3b53f-116">Finally, you send the sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3b53f-116">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="3b53f-117">What you learn</span><span class="sxs-lookup"><span data-stu-id="3b53f-117">What you learn</span></span>

* <span data-ttu-id="3b53f-118">How to create an Azure IoT hub and get your new device connection string.</span><span class="sxs-lookup"><span data-stu-id="3b53f-118">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="3b53f-119">How to connect Edison with a Grove temperature sensor.</span><span class="sxs-lookup"><span data-stu-id="3b53f-119">How to connect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="3b53f-120">How to collect sensor data by running a sample application on Edison.</span><span class="sxs-lookup"><span data-stu-id="3b53f-120">How to collect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="3b53f-121">How to send sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3b53f-121">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3b53f-122">What you need</span><span class="sxs-lookup"><span data-stu-id="3b53f-122">What you need</span></span>

![What you need](media/iot-hub-intel-edison-kit-node-get-started/0_kit.png)

* <span data-ttu-id="3b53f-124">The Intel Edison board</span><span class="sxs-lookup"><span data-stu-id="3b53f-124">The Intel Edison board</span></span>
* <span data-ttu-id="3b53f-125">Arduino expansion board</span><span class="sxs-lookup"><span data-stu-id="3b53f-125">Arduino expansion board</span></span>
* <span data-ttu-id="3b53f-126">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="3b53f-126">An active Azure subscription.</span></span> <span data-ttu-id="3b53f-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span><span class="sxs-lookup"><span data-stu-id="3b53f-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="3b53f-128">A Mac or a PC that is running Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="3b53f-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="3b53f-129">An Internet connection.</span><span class="sxs-lookup"><span data-stu-id="3b53f-129">An Internet connection.</span></span>
* <span data-ttu-id="3b53f-130">A Micro B to Type A USB cable</span><span class="sxs-lookup"><span data-stu-id="3b53f-130">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="3b53f-131">A direct current (DC) power supply.</span><span class="sxs-lookup"><span data-stu-id="3b53f-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="3b53f-132">Your power supply should be rated as follows:</span><span class="sxs-lookup"><span data-stu-id="3b53f-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="3b53f-133">7-15V DC</span><span class="sxs-lookup"><span data-stu-id="3b53f-133">7-15V DC</span></span>
  - <span data-ttu-id="3b53f-134">At least 1500mA</span><span class="sxs-lookup"><span data-stu-id="3b53f-134">At least 1500mA</span></span>
  - <span data-ttu-id="3b53f-135">The center/inner pin should be the positive pole of the power supply</span><span class="sxs-lookup"><span data-stu-id="3b53f-135">The center/inner pin should be the positive pole of the power supply</span></span>

<span data-ttu-id="3b53f-136">The following items are optional:</span><span class="sxs-lookup"><span data-stu-id="3b53f-136">The following items are optional:</span></span>

* <span data-ttu-id="3b53f-137">Grove Base Shield V2</span><span class="sxs-lookup"><span data-stu-id="3b53f-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="3b53f-138">Grove - Temperature Sensor</span><span class="sxs-lookup"><span data-stu-id="3b53f-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="3b53f-139">Grove Cable</span><span class="sxs-lookup"><span data-stu-id="3b53f-139">Grove Cable</span></span>
* <span data-ttu-id="3b53f-140">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span><span class="sxs-lookup"><span data-stu-id="3b53f-140">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="3b53f-141">These items are optional because the code sample support simulated sensor data.</span><span class="sxs-lookup"><span data-stu-id="3b53f-141">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="3b53f-142">Setup Intel Edison</span><span class="sxs-lookup"><span data-stu-id="3b53f-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="3b53f-143">Assemble your board</span><span class="sxs-lookup"><span data-stu-id="3b53f-143">Assemble your board</span></span>

<span data-ttu-id="3b53f-144">This section contains steps to attach your Intel® Edison module to your expansion board.</span><span class="sxs-lookup"><span data-stu-id="3b53f-144">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="3b53f-145">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span><span class="sxs-lookup"><span data-stu-id="3b53f-145">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="3b53f-146">Press down on the module just below the words `What will you make?` until you feel a snap.</span><span class="sxs-lookup"><span data-stu-id="3b53f-146">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![assemble board 2](media/iot-hub-intel-edison-kit-node-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="3b53f-148">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span><span class="sxs-lookup"><span data-stu-id="3b53f-148">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![assemble board 3](media/iot-hub-intel-edison-kit-node-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="3b53f-150">Insert a screw in one of the four corner holes on the expansion board.</span><span class="sxs-lookup"><span data-stu-id="3b53f-150">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="3b53f-151">Twist and tighten one of the white plastic spacers onto the screw.</span><span class="sxs-lookup"><span data-stu-id="3b53f-151">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![assemble board 4](media/iot-hub-intel-edison-kit-node-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="3b53f-153">Repeat for the other three corner spacers.</span><span class="sxs-lookup"><span data-stu-id="3b53f-153">Repeat for the other three corner spacers.</span></span>

   ![assemble board 5](media/iot-hub-intel-edison-kit-node-get-started/4_assemble_board5.jpg)

<span data-ttu-id="3b53f-155">Now your board is assembled.</span><span class="sxs-lookup"><span data-stu-id="3b53f-155">Now your board is assembled.</span></span>

   ![assembled board](media/iot-hub-intel-edison-kit-node-get-started/5_assembled_board.jpg)

### <a name="connect-the-grove-base-shield-and-the-temperature-sensor"></a><span data-ttu-id="3b53f-157">Connect the Grove Base Shield and the temperature sensor</span><span class="sxs-lookup"><span data-stu-id="3b53f-157">Connect the Grove Base Shield and the temperature sensor</span></span>

1. <span data-ttu-id="3b53f-158">Place the Grove Base Shield on to your board.</span><span class="sxs-lookup"><span data-stu-id="3b53f-158">Place the Grove Base Shield on to your board.</span></span> <span data-ttu-id="3b53f-159">Make sure all pins are tightly plugged into your board.</span><span class="sxs-lookup"><span data-stu-id="3b53f-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-node-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="3b53f-161">Use Grove Cable to connect Grove temperature sensor onto the Grove Base Shield **A0** port.</span><span class="sxs-lookup"><span data-stu-id="3b53f-161">Use Grove Cable to connect Grove temperature sensor onto the Grove Base Shield **A0** port.</span></span>

   ![Connect to temperature sensor](media/iot-hub-intel-edison-kit-node-get-started/7_temperature_sensor.jpg)

   ![Edison and sensor connection](media/iot-hub-intel-edison-kit-node-get-started/16_edion_sensor.png)

<span data-ttu-id="3b53f-164">Now your sensor is ready.</span><span class="sxs-lookup"><span data-stu-id="3b53f-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="3b53f-165">Power up Edison</span><span class="sxs-lookup"><span data-stu-id="3b53f-165">Power up Edison</span></span>

1. <span data-ttu-id="3b53f-166">Plug in the power supply.</span><span class="sxs-lookup"><span data-stu-id="3b53f-166">Plug in the power supply.</span></span>

   ![Plug in power supply](media/iot-hub-intel-edison-kit-node-get-started/8_plug_power.jpg)

2. <span data-ttu-id="3b53f-168">A green LED(labeled DS1 on the Arduino\* expansion board) should light up and stay lit.</span><span class="sxs-lookup"><span data-stu-id="3b53f-168">A green LED(labeled DS1 on the Arduino\* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="3b53f-169">Wait one minute for the board to finish booting up.</span><span class="sxs-lookup"><span data-stu-id="3b53f-169">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3b53f-170">If you do not have a DC power supply, you can still power the board through a USB port.</span><span class="sxs-lookup"><span data-stu-id="3b53f-170">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="3b53f-171">See `Connect Edison to your computer` section for details.</span><span class="sxs-lookup"><span data-stu-id="3b53f-171">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="3b53f-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span><span class="sxs-lookup"><span data-stu-id="3b53f-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-to-your-computer"></a><span data-ttu-id="3b53f-173">Connect Edison to your computer</span><span class="sxs-lookup"><span data-stu-id="3b53f-173">Connect Edison to your computer</span></span>

1. <span data-ttu-id="3b53f-174">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span><span class="sxs-lookup"><span data-stu-id="3b53f-174">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="3b53f-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="3b53f-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Toggle down the microswitch](media/iot-hub-intel-edison-kit-node-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="3b53f-177">Plug the micro USB cable into the top micro USB port.</span><span class="sxs-lookup"><span data-stu-id="3b53f-177">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Top micro USB port](media/iot-hub-intel-edison-kit-node-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="3b53f-179">Plug the other end of USB cable into your computer.</span><span class="sxs-lookup"><span data-stu-id="3b53f-179">Plug the other end of USB cable into your computer.</span></span>

   ![Computer USB](media/iot-hub-intel-edison-kit-node-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="3b53f-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span><span class="sxs-lookup"><span data-stu-id="3b53f-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="3b53f-182">Download and run the configuration tool</span><span class="sxs-lookup"><span data-stu-id="3b53f-182">Download and run the configuration tool</span></span>
<span data-ttu-id="3b53f-183">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span><span class="sxs-lookup"><span data-stu-id="3b53f-183">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="3b53f-184">Execute the tool and follow its on-screen instructions, clicking Next where needed</span><span class="sxs-lookup"><span data-stu-id="3b53f-184">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="3b53f-185">Flash firmware</span><span class="sxs-lookup"><span data-stu-id="3b53f-185">Flash firmware</span></span>
1. <span data-ttu-id="3b53f-186">On the `Set up options` page, click `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="3b53f-186">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="3b53f-187">Select the image to flash onto your board by doing one of the following:</span><span class="sxs-lookup"><span data-stu-id="3b53f-187">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="3b53f-188">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="3b53f-188">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="3b53f-189">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span><span class="sxs-lookup"><span data-stu-id="3b53f-189">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="3b53f-190">Browse to and select the image you want to flash to your board.</span><span class="sxs-lookup"><span data-stu-id="3b53f-190">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="3b53f-191">The setup tool will attempt to flash your board.</span><span class="sxs-lookup"><span data-stu-id="3b53f-191">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="3b53f-192">The entire flashing process may take up to 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="3b53f-192">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="3b53f-193">Set password</span><span class="sxs-lookup"><span data-stu-id="3b53f-193">Set password</span></span>
1. <span data-ttu-id="3b53f-194">On the `Set up options` page, click `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="3b53f-194">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="3b53f-195">You can set a custom name for your Intel® Edison board.</span><span class="sxs-lookup"><span data-stu-id="3b53f-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="3b53f-196">This is optional.</span><span class="sxs-lookup"><span data-stu-id="3b53f-196">This is optional.</span></span>
3. <span data-ttu-id="3b53f-197">Type a password for your board, then click `Set password`.</span><span class="sxs-lookup"><span data-stu-id="3b53f-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="3b53f-198">Mark down the password, which is used later.</span><span class="sxs-lookup"><span data-stu-id="3b53f-198">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="3b53f-199">Connect Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="3b53f-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="3b53f-200">On the `Set up options` page, click `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="3b53f-200">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="3b53f-201">Wait up to one minute as your computer scans for available Wi-Fi networks.</span><span class="sxs-lookup"><span data-stu-id="3b53f-201">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="3b53f-202">From the `Detected Networks` drop-down list, select your network.</span><span class="sxs-lookup"><span data-stu-id="3b53f-202">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="3b53f-203">From the `Security` drop-down list, select the network's security type.</span><span class="sxs-lookup"><span data-stu-id="3b53f-203">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="3b53f-204">Provide your login and password information, then click `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="3b53f-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="3b53f-205">Mark down the IP address, which is used later.</span><span class="sxs-lookup"><span data-stu-id="3b53f-205">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="3b53f-206">Make sure that Edison is connected to the same network as your computer.</span><span class="sxs-lookup"><span data-stu-id="3b53f-206">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="3b53f-207">Your computer connects to your Edison by using the IP address.</span><span class="sxs-lookup"><span data-stu-id="3b53f-207">Your computer connects to your Edison by using the IP address.</span></span>

   ![Connect to temperature sensor](media/iot-hub-intel-edison-kit-node-get-started/12_configuration_tool.png)

<span data-ttu-id="3b53f-209">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="3b53f-209">Congratulations!</span></span> <span data-ttu-id="3b53f-210">You've successfully configured Edison.</span><span class="sxs-lookup"><span data-stu-id="3b53f-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="3b53f-211">Run a sample application on Intel Edison</span><span class="sxs-lookup"><span data-stu-id="3b53f-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-the-azure-iot-device-sdk"></a><span data-ttu-id="3b53f-212">Prepare the Azure IoT Device SDK</span><span class="sxs-lookup"><span data-stu-id="3b53f-212">Prepare the Azure IoT Device SDK</span></span>

1. <span data-ttu-id="3b53f-213">Use one of the following SSH clients from your host computer to connect to your Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="3b53f-213">Use one of the following SSH clients from your host computer to connect to your Intel Edison.</span></span> <span data-ttu-id="3b53f-214">The IP address is from the configuration tool and the password is the one you've set in that tool.</span><span class="sxs-lookup"><span data-stu-id="3b53f-214">The IP address is from the configuration tool and the password is the one you've set in that tool.</span></span>
    - <span data-ttu-id="3b53f-215">[PuTTY](http://www.putty.org/) for Windows.</span><span class="sxs-lookup"><span data-stu-id="3b53f-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="3b53f-216">The built-in SSH client on Ubuntu or macOS.</span><span class="sxs-lookup"><span data-stu-id="3b53f-216">The built-in SSH client on Ubuntu or macOS.</span></span>

2. <span data-ttu-id="3b53f-217">Clone the sample client app to your device.</span><span class="sxs-lookup"><span data-stu-id="3b53f-217">Clone the sample client app to your device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-intel-edison-client-app
   ```

3. <span data-ttu-id="3b53f-218">Then navigate to the repo folder to run the following command to install all packages, it may take serval minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="3b53f-218">Then navigate to the repo folder to run the following command to install all packages, it may take serval minutes to complete.</span></span>
   
   ```bash
   cd iot-hub-node-intel-edison-client-app
   npm install
   ```


### <a name="configure-and-run-the-sample-application"></a><span data-ttu-id="3b53f-219">Configure and run the sample application</span><span class="sxs-lookup"><span data-stu-id="3b53f-219">Configure and run the sample application</span></span>

1. <span data-ttu-id="3b53f-220">Open the config file by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="3b53f-220">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Config file](media/iot-hub-intel-edison-kit-node-get-started/13_configure_file.png)

   <span data-ttu-id="3b53f-222">There are two macros in this file you can configurate.</span><span class="sxs-lookup"><span data-stu-id="3b53f-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="3b53f-223">The first one is `INTERVAL`, which defines the time interval between two messages that send to cloud.</span><span class="sxs-lookup"><span data-stu-id="3b53f-223">The first one is `INTERVAL`, which defines the time interval between two messages that send to cloud.</span></span> <span data-ttu-id="3b53f-224">The second one `simulatedData`,which is a Boolean value for whether to use simulated sensor data or not.</span><span class="sxs-lookup"><span data-stu-id="3b53f-224">The second one `simulatedData`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="3b53f-225">If you **don't have the sensor**, set the `simulatedData` value to `true` to make the sample application create and use simulated sensor data.</span><span class="sxs-lookup"><span data-stu-id="3b53f-225">If you **don't have the sensor**, set the `simulatedData` value to `true` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="3b53f-226">Save and exit by pressing Control-O > Enter > Control-X.</span><span class="sxs-lookup"><span data-stu-id="3b53f-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>


1. <span data-ttu-id="3b53f-227">Run the sample application by running the following command:</span><span class="sxs-lookup"><span data-stu-id="3b53f-227">Run the sample application by running the following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="3b53f-228">Make sure you copy-paste the device connection string into the single quotes.</span><span class="sxs-lookup"><span data-stu-id="3b53f-228">Make sure you copy-paste the device connection string into the single quotes.</span></span>

<span data-ttu-id="3b53f-229">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3b53f-229">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Output - sensor data sent from Intel Edison to your IoT hub](media/iot-hub-intel-edison-kit-node-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="3b53f-231">Next steps</span><span class="sxs-lookup"><span data-stu-id="3b53f-231">Next steps</span></span>

<span data-ttu-id="3b53f-232">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3b53f-232">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
