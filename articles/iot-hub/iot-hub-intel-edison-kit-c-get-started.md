---
title: Intel Edison to cloud (C) - Connect Intel Edison to Azure IoT Hub | Microsoft Docs
description: Connect Intel Edison to Azure IoT Hub for Intel Edison to send data to the Azure cloud.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: azure iot intel edison, intel edison iot hub, intel edison send data to cloud, intel edison to cloud
ms.assetid: 4885fa2c-c2ee-4253-b37f-ccd55f92b006
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/17/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3aba8d683da018703edc925c11a0420b297ac9fb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671811"
---
# <a name="connect-intel-edison-to-azure-iot-hub-c"></a><span data-ttu-id="0a877-104">Connect Intel Edison to Azure IoT Hub (C)</span><span class="sxs-lookup"><span data-stu-id="0a877-104">Connect Intel Edison to Azure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="0a877-105">In this tutorial, you begin by learning the basics of working with Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="0a877-105">In this tutorial, you begin by learning the basics of working with Intel Edison.</span></span> <span data-ttu-id="0a877-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="0a877-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="0a877-107">Don't have a kit yet?</span><span class="sxs-lookup"><span data-stu-id="0a877-107">Don't have a kit yet?</span></span> <span data-ttu-id="0a877-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span><span class="sxs-lookup"><span data-stu-id="0a877-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="0a877-109">What you do</span><span class="sxs-lookup"><span data-stu-id="0a877-109">What you do</span></span>

* <span data-ttu-id="0a877-110">Setup Intel Edison and and Grove modules.</span><span class="sxs-lookup"><span data-stu-id="0a877-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="0a877-111">Create an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0a877-111">Create an IoT hub.</span></span>
* <span data-ttu-id="0a877-112">Register a device for Edison in your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0a877-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="0a877-113">Run a sample application on Edison to send sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0a877-113">Run a sample application on Edison to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="0a877-114">Connect Intel Edison to an IoT hub that you create.</span><span class="sxs-lookup"><span data-stu-id="0a877-114">Connect Intel Edison to an IoT hub that you create.</span></span> <span data-ttu-id="0a877-115">Then you run a sample application on Edison to collect temperature and humidity data from a Grove temperature sensor.</span><span class="sxs-lookup"><span data-stu-id="0a877-115">Then you run a sample application on Edison to collect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="0a877-116">Finally, you send the sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0a877-116">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="0a877-117">What you learn</span><span class="sxs-lookup"><span data-stu-id="0a877-117">What you learn</span></span>

* <span data-ttu-id="0a877-118">How to create an Azure IoT hub and get your new device connection string.</span><span class="sxs-lookup"><span data-stu-id="0a877-118">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="0a877-119">How to connect Edison with a Grove temperature sensor.</span><span class="sxs-lookup"><span data-stu-id="0a877-119">How to connect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="0a877-120">How to collect sensor data by running a sample application on Edison.</span><span class="sxs-lookup"><span data-stu-id="0a877-120">How to collect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="0a877-121">How to send sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0a877-121">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0a877-122">What you need</span><span class="sxs-lookup"><span data-stu-id="0a877-122">What you need</span></span>

![What you need](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-kit-c-get-started/0_kit.png)

* <span data-ttu-id="0a877-124">The Intel Edison board</span><span class="sxs-lookup"><span data-stu-id="0a877-124">The Intel Edison board</span></span>
* <span data-ttu-id="0a877-125">Arduino expansion board</span><span class="sxs-lookup"><span data-stu-id="0a877-125">Arduino expansion board</span></span>
* <span data-ttu-id="0a877-126">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0a877-126">An active Azure subscription.</span></span> <span data-ttu-id="0a877-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span><span class="sxs-lookup"><span data-stu-id="0a877-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="0a877-128">A Mac or a PC that is running Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="0a877-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="0a877-129">An Internet connection.</span><span class="sxs-lookup"><span data-stu-id="0a877-129">An Internet connection.</span></span>
* <span data-ttu-id="0a877-130">A Micro B to Type A USB cable</span><span class="sxs-lookup"><span data-stu-id="0a877-130">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="0a877-131">A direct current (DC) power supply.</span><span class="sxs-lookup"><span data-stu-id="0a877-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="0a877-132">Your power supply should be rated as follows:</span><span class="sxs-lookup"><span data-stu-id="0a877-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="0a877-133">7-15V DC</span><span class="sxs-lookup"><span data-stu-id="0a877-133">7-15V DC</span></span>
  - <span data-ttu-id="0a877-134">At least 1500mA</span><span class="sxs-lookup"><span data-stu-id="0a877-134">At least 1500mA</span></span>
  - <span data-ttu-id="0a877-135">The center/inner pin should be the positive pole of the power supply</span><span class="sxs-lookup"><span data-stu-id="0a877-135">The center/inner pin should be the positive pole of the power supply</span></span>

<span data-ttu-id="0a877-136">The following items are optional:</span><span class="sxs-lookup"><span data-stu-id="0a877-136">The following items are optional:</span></span>

* <span data-ttu-id="0a877-137">Grove Base Shield V2</span><span class="sxs-lookup"><span data-stu-id="0a877-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="0a877-138">Grove - Temperature Sensor</span><span class="sxs-lookup"><span data-stu-id="0a877-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="0a877-139">Grove Cable</span><span class="sxs-lookup"><span data-stu-id="0a877-139">Grove Cable</span></span>
* <span data-ttu-id="0a877-140">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span><span class="sxs-lookup"><span data-stu-id="0a877-140">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="0a877-141">These items are optional because the code sample support simulated sensor data.</span><span class="sxs-lookup"><span data-stu-id="0a877-141">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="0a877-142">Setup Intel Edison</span><span class="sxs-lookup"><span data-stu-id="0a877-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="0a877-143">Assemble your board</span><span class="sxs-lookup"><span data-stu-id="0a877-143">Assemble your board</span></span>

<span data-ttu-id="0a877-144">This section contains steps to attach your Intel® Edison module to your expansion board.</span><span class="sxs-lookup"><span data-stu-id="0a877-144">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="0a877-145">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span><span class="sxs-lookup"><span data-stu-id="0a877-145">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="0a877-146">Press down on the module just below the words `What will you make?` until you feel a snap.</span><span class="sxs-lookup"><span data-stu-id="0a877-146">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![assemble board 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-kit-c-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="0a877-148">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span><span class="sxs-lookup"><span data-stu-id="0a877-148">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![assemble board 3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-kit-c-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="0a877-150">Insert a screw in one of the four corner holes on the expansion board.</span><span class="sxs-lookup"><span data-stu-id="0a877-150">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="0a877-151">Twist and tighten one of the white plastic spacers onto the screw.</span><span class="sxs-lookup"><span data-stu-id="0a877-151">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![assemble board 4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-kit-c-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="0a877-153">Repeat for the other three corner spacers.</span><span class="sxs-lookup"><span data-stu-id="0a877-153">Repeat for the other three corner spacers.</span></span>

   ![assemble board 5](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-kit-c-get-started/4_assemble_board5.jpg)

<span data-ttu-id="0a877-155">Now your board is assembled.</span><span class="sxs-lookup"><span data-stu-id="0a877-155">Now your board is assembled.</span></span>

   ![assembled board](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-kit-c-get-started/5_assembled_board.jpg)

### <a name="connect-the-grove-base-shield-and-the-temperature-sensor"></a><span data-ttu-id="0a877-157">Connect the Grove Base Shield and the temperature sensor</span><span class="sxs-lookup"><span data-stu-id="0a877-157">Connect the Grove Base Shield and the temperature sensor</span></span>

1. <span data-ttu-id="0a877-158">Place the Grove Base Shield on to your board.</span><span class="sxs-lookup"><span data-stu-id="0a877-158">Place the Grove Base Shield on to your board.</span></span> <span data-ttu-id="0a877-159">Make sure all pins are tightly plugged into your board.</span><span class="sxs-lookup"><span data-stu-id="0a877-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Grove Base Shield](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-kit-c-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="0a877-161">Use Grove Cable to connect Grove temperature sensor onto the Grove Base Shield **A0** port.</span><span class="sxs-lookup"><span data-stu-id="0a877-161">Use Grove Cable to connect Grove temperature sensor onto the Grove Base Shield **A0** port.</span></span>

   ![Connect to temperature sensor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-kit-c-get-started/7_temperature_sensor.jpg)
   
   ![Edison and sensor connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-kit-c-get-started/16_edion_sensor.png)

<span data-ttu-id="0a877-164">Now your sensor is ready.</span><span class="sxs-lookup"><span data-stu-id="0a877-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="0a877-165">Power up Edison</span><span class="sxs-lookup"><span data-stu-id="0a877-165">Power up Edison</span></span>

1. <span data-ttu-id="0a877-166">Plug in the power supply.</span><span class="sxs-lookup"><span data-stu-id="0a877-166">Plug in the power supply.</span></span>

   ![Plug in power supply](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-kit-c-get-started/8_plug_power.jpg)

2. <span data-ttu-id="0a877-168">A green LED(labeled DS1 on the Arduino\* expansion board) should light up and stay lit.</span><span class="sxs-lookup"><span data-stu-id="0a877-168">A green LED(labeled DS1 on the Arduino\* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="0a877-169">Wait one minute for the board to finish booting up.</span><span class="sxs-lookup"><span data-stu-id="0a877-169">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0a877-170">If you do not have a DC power supply, you can still power the board through a USB port.</span><span class="sxs-lookup"><span data-stu-id="0a877-170">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="0a877-171">See `Connect Edison to your computer` section for details.</span><span class="sxs-lookup"><span data-stu-id="0a877-171">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="0a877-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span><span class="sxs-lookup"><span data-stu-id="0a877-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-to-your-computer"></a><span data-ttu-id="0a877-173">Connect Edison to your computer</span><span class="sxs-lookup"><span data-stu-id="0a877-173">Connect Edison to your computer</span></span>

1. <span data-ttu-id="0a877-174">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span><span class="sxs-lookup"><span data-stu-id="0a877-174">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="0a877-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="0a877-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Toggle down the microswitch](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-kit-c-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="0a877-177">Plug the micro USB cable into the top micro USB port.</span><span class="sxs-lookup"><span data-stu-id="0a877-177">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Top micro USB port](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-kit-c-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="0a877-179">Plug the other end of USB cable into your computer.</span><span class="sxs-lookup"><span data-stu-id="0a877-179">Plug the other end of USB cable into your computer.</span></span>

   ![Computer USB](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-kit-c-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="0a877-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span><span class="sxs-lookup"><span data-stu-id="0a877-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="0a877-182">Download and run the configuration tool</span><span class="sxs-lookup"><span data-stu-id="0a877-182">Download and run the configuration tool</span></span>
<span data-ttu-id="0a877-183">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span><span class="sxs-lookup"><span data-stu-id="0a877-183">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="0a877-184">Execute the tool and follow its on-screen instructions, clicking Next where needed</span><span class="sxs-lookup"><span data-stu-id="0a877-184">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="0a877-185">Flash firmware</span><span class="sxs-lookup"><span data-stu-id="0a877-185">Flash firmware</span></span>
1. <span data-ttu-id="0a877-186">On the `Set up options` page, click `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="0a877-186">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="0a877-187">Select the image to flash onto your board by doing one of the following:</span><span class="sxs-lookup"><span data-stu-id="0a877-187">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="0a877-188">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="0a877-188">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="0a877-189">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span><span class="sxs-lookup"><span data-stu-id="0a877-189">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="0a877-190">Browse to and select the image you want to flash to your board.</span><span class="sxs-lookup"><span data-stu-id="0a877-190">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="0a877-191">The setup tool will attempt to flash your board.</span><span class="sxs-lookup"><span data-stu-id="0a877-191">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="0a877-192">The entire flashing process may take up to 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="0a877-192">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="0a877-193">Set password</span><span class="sxs-lookup"><span data-stu-id="0a877-193">Set password</span></span>
1. <span data-ttu-id="0a877-194">On the `Set up options` page, click `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="0a877-194">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="0a877-195">You can set a custom name for your Intel® Edison board.</span><span class="sxs-lookup"><span data-stu-id="0a877-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="0a877-196">This is optional.</span><span class="sxs-lookup"><span data-stu-id="0a877-196">This is optional.</span></span>
3. <span data-ttu-id="0a877-197">Type a password for your board, then click `Set password`.</span><span class="sxs-lookup"><span data-stu-id="0a877-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="0a877-198">Mark down the password, which is used later.</span><span class="sxs-lookup"><span data-stu-id="0a877-198">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="0a877-199">Connect Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="0a877-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="0a877-200">On the `Set up options` page, click `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="0a877-200">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="0a877-201">Wait up to one minute as your computer scans for available Wi-Fi networks.</span><span class="sxs-lookup"><span data-stu-id="0a877-201">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="0a877-202">From the `Detected Networks` drop-down list, select your network.</span><span class="sxs-lookup"><span data-stu-id="0a877-202">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="0a877-203">From the `Security` drop-down list, select the network's security type.</span><span class="sxs-lookup"><span data-stu-id="0a877-203">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="0a877-204">Provide your login and password information, then click `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="0a877-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="0a877-205">Mark down the IP address, which is used later.</span><span class="sxs-lookup"><span data-stu-id="0a877-205">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="0a877-206">Make sure that Edison is connected to the same network as your computer.</span><span class="sxs-lookup"><span data-stu-id="0a877-206">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="0a877-207">Your computer connects to your Edison by using the IP address.</span><span class="sxs-lookup"><span data-stu-id="0a877-207">Your computer connects to your Edison by using the IP address.</span></span>

   ![Connect to temperature sensor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-kit-c-get-started/12_configuration_tool.png)

<span data-ttu-id="0a877-209">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="0a877-209">Congratulations!</span></span> <span data-ttu-id="0a877-210">You've successfully configured Edison.</span><span class="sxs-lookup"><span data-stu-id="0a877-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="0a877-211">Run a sample application on Intel Edison</span><span class="sxs-lookup"><span data-stu-id="0a877-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-the-azure-iot-device-sdk"></a><span data-ttu-id="0a877-212">Prepare the Azure IoT Device SDK</span><span class="sxs-lookup"><span data-stu-id="0a877-212">Prepare the Azure IoT Device SDK</span></span>

1. <span data-ttu-id="0a877-213">Use one of the following SSH clients from your host computer to connect to your Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="0a877-213">Use one of the following SSH clients from your host computer to connect to your Intel Edison.</span></span> <span data-ttu-id="0a877-214">The IP address is from the configuration tool and the password is the one you've set in that tool.</span><span class="sxs-lookup"><span data-stu-id="0a877-214">The IP address is from the configuration tool and the password is the one you've set in that tool.</span></span>
    - <span data-ttu-id="0a877-215">[PuTTY](http://www.putty.org/) for Windows.</span><span class="sxs-lookup"><span data-stu-id="0a877-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="0a877-216">The built-in SSH client on Ubuntu or macOS.</span><span class="sxs-lookup"><span data-stu-id="0a877-216">The built-in SSH client on Ubuntu or macOS.</span></span>

2. <span data-ttu-id="0a877-217">Clone the sample client app to your device.</span><span class="sxs-lookup"><span data-stu-id="0a877-217">Clone the sample client app to your device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-edison-client-app.git
   ```

3. <span data-ttu-id="0a877-218">Then navigate to the repo folder to run the following command to build Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="0a877-218">Then navigate to the repo folder to run the following command to build Azure IoT SDK</span></span>

   ```bash
   cd iot-hub-c-intel-edison-client-app
   sed -i -e 's/\r$//' buildSDK.sh
   chmod 755 buildSDK.sh
   ./buildSDK.sh
   ```

### <a name="configure-the-sample-application"></a><span data-ttu-id="0a877-219">Configure the sample application</span><span class="sxs-lookup"><span data-stu-id="0a877-219">Configure the sample application</span></span>

1. <span data-ttu-id="0a877-220">Open the config file by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="0a877-220">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.h
   ```

   ![Config file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-kit-c-get-started/13_configure_file.png)

   <span data-ttu-id="0a877-222">There are two macros in this file you can configurate.</span><span class="sxs-lookup"><span data-stu-id="0a877-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="0a877-223">The first one is `INTERVAL`, which defines the time interval between two messages that send to cloud.</span><span class="sxs-lookup"><span data-stu-id="0a877-223">The first one is `INTERVAL`, which defines the time interval between two messages that send to cloud.</span></span> <span data-ttu-id="0a877-224">The second one `SIMULATED_DATA`,which is a Boolean value for whether to use simulated sensor data or not.</span><span class="sxs-lookup"><span data-stu-id="0a877-224">The second one `SIMULATED_DATA`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="0a877-225">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `1` to make the sample application create and use simulated sensor data.</span><span class="sxs-lookup"><span data-stu-id="0a877-225">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `1` to make the sample application create and use simulated sensor data.</span></span>

2. <span data-ttu-id="0a877-226">Save and exit by pressing Control-O > Enter > Control-X.</span><span class="sxs-lookup"><span data-stu-id="0a877-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-the-sample-application"></a><span data-ttu-id="0a877-227">Build and run the sample application</span><span class="sxs-lookup"><span data-stu-id="0a877-227">Build and run the sample application</span></span>

1. <span data-ttu-id="0a877-228">Build the sample application by running the following command:</span><span class="sxs-lookup"><span data-stu-id="0a877-228">Build the sample application by running the following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![Build output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-kit-c-get-started/14_build_output.png)

1. <span data-ttu-id="0a877-230">Run the sample application by running the following command:</span><span class="sxs-lookup"><span data-stu-id="0a877-230">Run the sample application by running the following command:</span></span>

   ```bash
   sudo ./app '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="0a877-231">Make sure you copy-paste the device connection string into the single quotes.</span><span class="sxs-lookup"><span data-stu-id="0a877-231">Make sure you copy-paste the device connection string into the single quotes.</span></span>

<span data-ttu-id="0a877-232">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0a877-232">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Output - sensor data sent from Intel Edison to your IoT hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-kit-c-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="0a877-234">Next steps</span><span class="sxs-lookup"><span data-stu-id="0a877-234">Next steps</span></span>

<span data-ttu-id="0a877-235">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0a877-235">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
















