---
title: 'Connect Intel Edison (C) to Azure IoT - Lesson 1: Configure device | Microsoft Docs'
description: Configure Intel Edison for first-time use.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: arduino set up, connect arduino to pc, setup arduino, arduino board
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: bb8aa45b-d3ff-4438-b9d6-a9725a45ade1
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ff87c49e25ca396d92a17c21becf9c46748b8769
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551310"
---
# <a name="configure-your-intel-edison"></a><span data-ttu-id="fe465-104">Configure your Intel Edison</span><span class="sxs-lookup"><span data-stu-id="fe465-104">Configure your Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="fe465-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="fe465-105">What you will do</span></span>
<span data-ttu-id="fe465-106">Configure Intel Edison for first-time use by assembling the board, powering it up and installing configuration tool to your desktop OS to flash Edison's firmware, set its password and connect it to Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="fe465-106">Configure Intel Edison for first-time use by assembling the board, powering it up and installing configuration tool to your desktop OS to flash Edison's firmware, set its password and connect it to Wi-Fi.</span></span> <span data-ttu-id="fe465-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="fe465-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="fe465-108">What you will learn</span><span class="sxs-lookup"><span data-stu-id="fe465-108">What you will learn</span></span>
<span data-ttu-id="fe465-109">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="fe465-109">In this article, you will learn:</span></span>

* <span data-ttu-id="fe465-110">How to assemble Edison board and power it up.</span><span class="sxs-lookup"><span data-stu-id="fe465-110">How to assemble Edison board and power it up.</span></span>
* <span data-ttu-id="fe465-111">How to flash Edison's firmware, set password and connect Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="fe465-111">How to flash Edison's firmware, set password and connect Wi-Fi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fe465-112">What you need</span><span class="sxs-lookup"><span data-stu-id="fe465-112">What you need</span></span>
<span data-ttu-id="fe465-113">To complete this operation, you need the following parts from your Intel Edison Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="fe465-113">To complete this operation, you need the following parts from your Intel Edison Starter Kit:</span></span>

* <span data-ttu-id="fe465-114">Intel® Edison module</span><span class="sxs-lookup"><span data-stu-id="fe465-114">Intel® Edison module</span></span>
* <span data-ttu-id="fe465-115">Arduino expansion board</span><span class="sxs-lookup"><span data-stu-id="fe465-115">Arduino expansion board</span></span>
* <span data-ttu-id="fe465-116">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span><span class="sxs-lookup"><span data-stu-id="fe465-116">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>
* <span data-ttu-id="fe465-117">A Micro B to Type A USB cable</span><span class="sxs-lookup"><span data-stu-id="fe465-117">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="fe465-118">A direct current (DC) power supply.</span><span class="sxs-lookup"><span data-stu-id="fe465-118">A direct current (DC) power supply.</span></span> <span data-ttu-id="fe465-119">Your power supply should be rated as follows:</span><span class="sxs-lookup"><span data-stu-id="fe465-119">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="fe465-120">7-15V DC</span><span class="sxs-lookup"><span data-stu-id="fe465-120">7-15V DC</span></span>
  - <span data-ttu-id="fe465-121">At least 1500mA</span><span class="sxs-lookup"><span data-stu-id="fe465-121">At least 1500mA</span></span>
  - <span data-ttu-id="fe465-122">The center/inner pin should be the positive pole of the power supply</span><span class="sxs-lookup"><span data-stu-id="fe465-122">The center/inner pin should be the positive pole of the power supply</span></span>

  ![Things in your Starter Kit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson1/kit.png)

<span data-ttu-id="fe465-124">You also need:</span><span class="sxs-lookup"><span data-stu-id="fe465-124">You also need:</span></span>

* <span data-ttu-id="fe465-125">A computer running Windows, Mac, or Linux.</span><span class="sxs-lookup"><span data-stu-id="fe465-125">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="fe465-126">A wireless connection for Edison to connect to.</span><span class="sxs-lookup"><span data-stu-id="fe465-126">A wireless connection for Edison to connect to.</span></span>
* <span data-ttu-id="fe465-127">An Internet connection to download configuration tool.</span><span class="sxs-lookup"><span data-stu-id="fe465-127">An Internet connection to download configuration tool.</span></span>

## <a name="assemble-your-board"></a><span data-ttu-id="fe465-128">Assemble your board</span><span class="sxs-lookup"><span data-stu-id="fe465-128">Assemble your board</span></span>

<span data-ttu-id="fe465-129">This section contains steps to attach your Intel® Edison module to your expansion board.</span><span class="sxs-lookup"><span data-stu-id="fe465-129">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="fe465-130">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span><span class="sxs-lookup"><span data-stu-id="fe465-130">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="fe465-131">Press down on the module just below the words `What will you make?` until you feel a snap.</span><span class="sxs-lookup"><span data-stu-id="fe465-131">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![assemble board 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. <span data-ttu-id="fe465-133">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span><span class="sxs-lookup"><span data-stu-id="fe465-133">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![assemble board 3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. <span data-ttu-id="fe465-135">Insert a screw in one of the four corner holes on the expansion board.</span><span class="sxs-lookup"><span data-stu-id="fe465-135">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="fe465-136">Twist and tighten one of the white plastic spacers onto the screw.</span><span class="sxs-lookup"><span data-stu-id="fe465-136">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![assemble board 4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. <span data-ttu-id="fe465-138">Repeat for the other three corner spacers.</span><span class="sxs-lookup"><span data-stu-id="fe465-138">Repeat for the other three corner spacers.</span></span>

   ![assemble board 5](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

<span data-ttu-id="fe465-140">Now your board is assembled.</span><span class="sxs-lookup"><span data-stu-id="fe465-140">Now your board is assembled.</span></span>

   ![assembled board](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a><span data-ttu-id="fe465-142">Power up Edison</span><span class="sxs-lookup"><span data-stu-id="fe465-142">Power up Edison</span></span>

1. <span data-ttu-id="fe465-143">Plug in the power supply.</span><span class="sxs-lookup"><span data-stu-id="fe465-143">Plug in the power supply.</span></span>

   ![Plug in power supply](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. <span data-ttu-id="fe465-145">A green LED(labeled DS1 on the Arduino\* expansion board) should light up and stay lit.</span><span class="sxs-lookup"><span data-stu-id="fe465-145">A green LED(labeled DS1 on the Arduino\* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="fe465-146">Wait one minute for the board to finish booting up.</span><span class="sxs-lookup"><span data-stu-id="fe465-146">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fe465-147">If you do not have a DC power supply, you can still power the board through a USB port.</span><span class="sxs-lookup"><span data-stu-id="fe465-147">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="fe465-148">See `Connect Edison to your computer` section for details.</span><span class="sxs-lookup"><span data-stu-id="fe465-148">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="fe465-149">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span><span class="sxs-lookup"><span data-stu-id="fe465-149">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

## <a name="connect-edison-to-your-computer"></a><span data-ttu-id="fe465-150">Connect Edison to your computer</span><span class="sxs-lookup"><span data-stu-id="fe465-150">Connect Edison to your computer</span></span>

1. <span data-ttu-id="fe465-151">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span><span class="sxs-lookup"><span data-stu-id="fe465-151">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="fe465-152">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="fe465-152">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Toggle down the microswitch](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. <span data-ttu-id="fe465-154">Plug the micro USB cable into the top micro USB port.</span><span class="sxs-lookup"><span data-stu-id="fe465-154">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Top micro USB port](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. <span data-ttu-id="fe465-156">Plug the other end of USB cable into your computer.</span><span class="sxs-lookup"><span data-stu-id="fe465-156">Plug the other end of USB cable into your computer.</span></span>

   ![Computer USB](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. <span data-ttu-id="fe465-158">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span><span class="sxs-lookup"><span data-stu-id="fe465-158">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="fe465-159">Download and run the configuration tool</span><span class="sxs-lookup"><span data-stu-id="fe465-159">Download and run the configuration tool</span></span>
<span data-ttu-id="fe465-160">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span><span class="sxs-lookup"><span data-stu-id="fe465-160">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="fe465-161">Execute the tool and follow its on-screen instructions, clicking Next where needed</span><span class="sxs-lookup"><span data-stu-id="fe465-161">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="fe465-162">Flash firmware</span><span class="sxs-lookup"><span data-stu-id="fe465-162">Flash firmware</span></span>
1. <span data-ttu-id="fe465-163">On the `Set up options` page, click `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="fe465-163">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="fe465-164">Select the image to flash onto your board by doing one of the following:</span><span class="sxs-lookup"><span data-stu-id="fe465-164">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="fe465-165">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="fe465-165">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="fe465-166">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span><span class="sxs-lookup"><span data-stu-id="fe465-166">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="fe465-167">Browse to and select the image you want to flash to your board.</span><span class="sxs-lookup"><span data-stu-id="fe465-167">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="fe465-168">The setup tool will attempt to flash your board.</span><span class="sxs-lookup"><span data-stu-id="fe465-168">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="fe465-169">The entire flashing process may take up to 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="fe465-169">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="fe465-170">Set password</span><span class="sxs-lookup"><span data-stu-id="fe465-170">Set password</span></span>
1. <span data-ttu-id="fe465-171">On the `Set up options` page, click `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="fe465-171">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="fe465-172">You can set a custom name for your Intel® Edison board.</span><span class="sxs-lookup"><span data-stu-id="fe465-172">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="fe465-173">This is optional.</span><span class="sxs-lookup"><span data-stu-id="fe465-173">This is optional.</span></span>
3. <span data-ttu-id="fe465-174">Type a password for your board, then click `Set password`.</span><span class="sxs-lookup"><span data-stu-id="fe465-174">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="fe465-175">Mark down the password, which is used later.</span><span class="sxs-lookup"><span data-stu-id="fe465-175">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="fe465-176">Connect Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="fe465-176">Connect Wi-Fi</span></span>
1. <span data-ttu-id="fe465-177">On the `Set up options` page, click `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="fe465-177">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="fe465-178">Wait up to one minute as your computer scans for available Wi-Fi networks.</span><span class="sxs-lookup"><span data-stu-id="fe465-178">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="fe465-179">From the `Detected Networks` drop-down list, select your network.</span><span class="sxs-lookup"><span data-stu-id="fe465-179">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="fe465-180">From the `Security` drop-down list, select the network's security type.</span><span class="sxs-lookup"><span data-stu-id="fe465-180">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="fe465-181">Provide your login and password information, then click `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="fe465-181">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="fe465-182">Mark down the IP address, which is used later.</span><span class="sxs-lookup"><span data-stu-id="fe465-182">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="fe465-183">Make sure that Edison is connected to the same network as your computer.</span><span class="sxs-lookup"><span data-stu-id="fe465-183">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="fe465-184">Your computer connects to your Edison by using the IP address.</span><span class="sxs-lookup"><span data-stu-id="fe465-184">Your computer connects to your Edison by using the IP address.</span></span>

<span data-ttu-id="fe465-185">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="fe465-185">Congratulations!</span></span> <span data-ttu-id="fe465-186">You've successfully configured Edison.</span><span class="sxs-lookup"><span data-stu-id="fe465-186">You've successfully configured Edison.</span></span>

## <a name="summary"></a><span data-ttu-id="fe465-187">Summary</span><span class="sxs-lookup"><span data-stu-id="fe465-187">Summary</span></span>
<span data-ttu-id="fe465-188">In this article, you’ve learned how to assemble the Edison board, flash its firmware, setup password and connect it to Wi-Fi by using configuration tool.</span><span class="sxs-lookup"><span data-stu-id="fe465-188">In this article, you’ve learned how to assemble the Edison board, flash its firmware, setup password and connect it to Wi-Fi by using configuration tool.</span></span> <span data-ttu-id="fe465-189">Note that the LED doesn't yet light up.</span><span class="sxs-lookup"><span data-stu-id="fe465-189">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="fe465-190">The next task is to install the necessary tools and software in preparation for running a sample application on Edison.</span><span class="sxs-lookup"><span data-stu-id="fe465-190">The next task is to install the necessary tools and software in preparation for running a sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe465-191">Next steps</span><span class="sxs-lookup"><span data-stu-id="fe465-191">Next steps</span></span>
<span data-ttu-id="fe465-192">[Get the tools][get-the-tools]
<!-- Images and links --></span><span class="sxs-lookup"><span data-stu-id="fe465-192">[Get the tools][get-the-tools]
<!-- Images and links --></span></span>

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md









