---
title: 'Connect Raspberry Pi (C) to Azure IoT - Lesson 1: Configure device | Microsoft Docs'
description: Configure Raspberry Pi 3 for first-time use and install the Raspbian OS, a free operating system that is optimized for the Raspberry Pi hardware.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: install raspbian, raspbian download, how to install raspbian, raspbian setup, raspberry pi install raspbian, raspberry pi install os, raspberry pi sd card install, raspberry pi connect, connect to raspberry pi, raspberry pi connectivity
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8ee9b23c-93f7-43ff-8ea1-e7761eb87a6f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7e43d337fe0b79aa6aeed9978cb5458c3f49ceda
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549275"
---
# <a name="configure-your-device"></a><span data-ttu-id="30fe5-104">Configure your device</span><span class="sxs-lookup"><span data-stu-id="30fe5-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="30fe5-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="30fe5-105">What you will do</span></span>
<span data-ttu-id="30fe5-106">Configure Pi for first-time use and install the Raspbian operating system.</span><span class="sxs-lookup"><span data-stu-id="30fe5-106">Configure Pi for first-time use and install the Raspbian operating system.</span></span> <span data-ttu-id="30fe5-107">Raspbian is a free operating system that is optimized for the Raspberry Pi hardware.</span><span class="sxs-lookup"><span data-stu-id="30fe5-107">Raspbian is a free operating system that is optimized for the Raspberry Pi hardware.</span></span> <span data-ttu-id="30fe5-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="30fe5-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="30fe5-109">What you will learn</span><span class="sxs-lookup"><span data-stu-id="30fe5-109">What you will learn</span></span>
<span data-ttu-id="30fe5-110">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="30fe5-110">In this article, you will learn:</span></span>

* <span data-ttu-id="30fe5-111">How to install Raspbian on Pi.</span><span class="sxs-lookup"><span data-stu-id="30fe5-111">How to install Raspbian on Pi.</span></span>
* <span data-ttu-id="30fe5-112">How to power up Pi by using a USB cable.</span><span class="sxs-lookup"><span data-stu-id="30fe5-112">How to power up Pi by using a USB cable.</span></span>
* <span data-ttu-id="30fe5-113">How to connect Pi to the network by using an Ethernet cable or wireless network.</span><span class="sxs-lookup"><span data-stu-id="30fe5-113">How to connect Pi to the network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="30fe5-114">How to add an LED to the breadboard and connect it to Pi.</span><span class="sxs-lookup"><span data-stu-id="30fe5-114">How to add an LED to the breadboard and connect it to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="30fe5-115">What you need</span><span class="sxs-lookup"><span data-stu-id="30fe5-115">What you need</span></span>
<span data-ttu-id="30fe5-116">To complete this operation, you need the following parts from your Raspberry Pi 3 Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="30fe5-116">To complete this operation, you need the following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="30fe5-117">The Raspberry Pi 3 board</span><span class="sxs-lookup"><span data-stu-id="30fe5-117">The Raspberry Pi 3 board</span></span>
* <span data-ttu-id="30fe5-118">The 16-GB microSD card</span><span class="sxs-lookup"><span data-stu-id="30fe5-118">The 16-GB microSD card</span></span>
* <span data-ttu-id="30fe5-119">The 5-volt 2-amp power supply with the 6-foot micro USB cable</span><span class="sxs-lookup"><span data-stu-id="30fe5-119">The 5-volt 2-amp power supply with the 6-foot micro USB cable</span></span>
* <span data-ttu-id="30fe5-120">The breadboard</span><span class="sxs-lookup"><span data-stu-id="30fe5-120">The breadboard</span></span>
* <span data-ttu-id="30fe5-121">Connector wires</span><span class="sxs-lookup"><span data-stu-id="30fe5-121">Connector wires</span></span>
* <span data-ttu-id="30fe5-122">A 560-ohm resistor</span><span class="sxs-lookup"><span data-stu-id="30fe5-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="30fe5-123">A diffused 10-mm LED</span><span class="sxs-lookup"><span data-stu-id="30fe5-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="30fe5-124">The Ethernet cable</span><span class="sxs-lookup"><span data-stu-id="30fe5-124">The Ethernet cable</span></span>

![Things in your Starter Kit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="30fe5-126">You also need:</span><span class="sxs-lookup"><span data-stu-id="30fe5-126">You also need:</span></span>

* <span data-ttu-id="30fe5-127">A wired or wireless connection for Pi to connect to.</span><span class="sxs-lookup"><span data-stu-id="30fe5-127">A wired or wireless connection for Pi to connect to.</span></span>
* <span data-ttu-id="30fe5-128">A USB-SD adapter or mini-SD card to burn the OS image onto the microSD card.</span><span class="sxs-lookup"><span data-stu-id="30fe5-128">A USB-SD adapter or mini-SD card to burn the OS image onto the microSD card.</span></span>
* <span data-ttu-id="30fe5-129">A computer running Windows, Mac, or Linux.</span><span class="sxs-lookup"><span data-stu-id="30fe5-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="30fe5-130">The computer is used to install Raspbian on the microSD card.</span><span class="sxs-lookup"><span data-stu-id="30fe5-130">The computer is used to install Raspbian on the microSD card.</span></span>
* <span data-ttu-id="30fe5-131">An Internet connection to download the necessary tools and software.</span><span class="sxs-lookup"><span data-stu-id="30fe5-131">An Internet connection to download the necessary tools and software.</span></span>

## <a name="install-raspbian-on-the-microsd-card"></a><span data-ttu-id="30fe5-132">Install Raspbian on the MicroSD card</span><span class="sxs-lookup"><span data-stu-id="30fe5-132">Install Raspbian on the MicroSD card</span></span>
<span data-ttu-id="30fe5-133">Prepare the microSD card for installation of the Raspbian image.</span><span class="sxs-lookup"><span data-stu-id="30fe5-133">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="30fe5-134">Download Raspbian.</span><span class="sxs-lookup"><span data-stu-id="30fe5-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="30fe5-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) the .zip file for Raspbian Jessie with Pixel.</span><span class="sxs-lookup"><span data-stu-id="30fe5-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) the .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="30fe5-136">Extract the Raspbian image to a folder on your computer.</span><span class="sxs-lookup"><span data-stu-id="30fe5-136">Extract the Raspbian image to a folder on your computer.</span></span>
2. <span data-ttu-id="30fe5-137">Install Raspbian to the microSD card.</span><span class="sxs-lookup"><span data-stu-id="30fe5-137">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="30fe5-138">[Download](https://www.etcher.io) and install the Etcher SD card burner utility.</span><span class="sxs-lookup"><span data-stu-id="30fe5-138">[Download](https://www.etcher.io) and install the Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="30fe5-139">Run Etcher and select the Raspbian image that you extracted in step 1.</span><span class="sxs-lookup"><span data-stu-id="30fe5-139">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="30fe5-140">Select the microSD card drive.</span><span class="sxs-lookup"><span data-stu-id="30fe5-140">Select the microSD card drive.</span></span>
      <span data-ttu-id="30fe5-141">Note that Etcher may have already selected the correct drive.</span><span class="sxs-lookup"><span data-stu-id="30fe5-141">Note that Etcher may have already selected the correct drive.</span></span>
   4. <span data-ttu-id="30fe5-142">Click **Flash** to install Raspbian to the microSD card.</span><span class="sxs-lookup"><span data-stu-id="30fe5-142">Click **Flash** to install Raspbian to the microSD card.</span></span>
   5. <span data-ttu-id="30fe5-143">Remove the microSD card from your computer when installation is complete.</span><span class="sxs-lookup"><span data-stu-id="30fe5-143">Remove the microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="30fe5-144">It is safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span><span class="sxs-lookup"><span data-stu-id="30fe5-144">It is safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   6. <span data-ttu-id="30fe5-145">Insert the microSD card into your Pi.</span><span class="sxs-lookup"><span data-stu-id="30fe5-145">Insert the microSD card into your Pi.</span></span>

![Insert the SD card](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="30fe5-147">Turn on Pi</span><span class="sxs-lookup"><span data-stu-id="30fe5-147">Turn on Pi</span></span>
<span data-ttu-id="30fe5-148">Turn on Pi by using the micro USB cable and the power supply.</span><span class="sxs-lookup"><span data-stu-id="30fe5-148">Turn on Pi by using the micro USB cable and the power supply.</span></span>

![Turn on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="30fe5-150">It is important to use the power supply in the kit that is at least 2A to make sure that your Raspberry has enough power to work correctly.</span><span class="sxs-lookup"><span data-stu-id="30fe5-150">It is important to use the power supply in the kit that is at least 2A to make sure that your Raspberry has enough power to work correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="30fe5-151">Enable SSH</span><span class="sxs-lookup"><span data-stu-id="30fe5-151">Enable SSH</span></span>
<span data-ttu-id="30fe5-152">As of the November 2016 release, Raspbian has the SSH server disabled by default.</span><span class="sxs-lookup"><span data-stu-id="30fe5-152">As of the November 2016 release, Raspbian has the SSH server disabled by default.</span></span> <span data-ttu-id="30fe5-153">You need to enable it manually.</span><span class="sxs-lookup"><span data-stu-id="30fe5-153">You need to enable it manually.</span></span> <span data-ttu-id="30fe5-154">You can refer to the [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go to **Preferences -> Raspberry Pi Configuration** to enable SSH.</span><span class="sxs-lookup"><span data-stu-id="30fe5-154">You can refer to the [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go to **Preferences -> Raspberry Pi Configuration** to enable SSH.</span></span>

## <a name="connect-raspberry-pi-3-to-the-network"></a><span data-ttu-id="30fe5-155">Connect Raspberry Pi 3 to the network</span><span class="sxs-lookup"><span data-stu-id="30fe5-155">Connect Raspberry Pi 3 to the network</span></span>
<span data-ttu-id="30fe5-156">You can connect Pi to a wired network or to a wireless network.</span><span class="sxs-lookup"><span data-stu-id="30fe5-156">You can connect Pi to a wired network or to a wireless network.</span></span> <span data-ttu-id="30fe5-157">Make sure that Pi is connected to the same network as your computer.</span><span class="sxs-lookup"><span data-stu-id="30fe5-157">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="30fe5-158">For example, you can connect Pi to the same switch that your computer is connected to.</span><span class="sxs-lookup"><span data-stu-id="30fe5-158">For example, you can connect Pi to the same switch that your computer is connected to.</span></span>

### <a name="connect-to-a-wired-network"></a><span data-ttu-id="30fe5-159">Connect to a wired network</span><span class="sxs-lookup"><span data-stu-id="30fe5-159">Connect to a wired network</span></span>
<span data-ttu-id="30fe5-160">Use the Ethernet cable to connect Pi to your wired network.</span><span class="sxs-lookup"><span data-stu-id="30fe5-160">Use the Ethernet cable to connect Pi to your wired network.</span></span> <span data-ttu-id="30fe5-161">The two LEDs on Pi turn on if the connection is established.</span><span class="sxs-lookup"><span data-stu-id="30fe5-161">The two LEDs on Pi turn on if the connection is established.</span></span>

![Connect by using an Ethernet cable](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-to-a-wireless-network"></a><span data-ttu-id="30fe5-163">Connect to a wireless network</span><span class="sxs-lookup"><span data-stu-id="30fe5-163">Connect to a wireless network</span></span>
<span data-ttu-id="30fe5-164">Follow the [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from the Raspberry Pi Foundation to connect Pi to your wireless network.</span><span class="sxs-lookup"><span data-stu-id="30fe5-164">Follow the [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from the Raspberry Pi Foundation to connect Pi to your wireless network.</span></span> <span data-ttu-id="30fe5-165">These instructions require you to first connect a monitor and a keyboard to Pi.</span><span class="sxs-lookup"><span data-stu-id="30fe5-165">These instructions require you to first connect a monitor and a keyboard to Pi.</span></span>

## <a name="connect-the-led-to-pi"></a><span data-ttu-id="30fe5-166">Connect the LED to Pi</span><span class="sxs-lookup"><span data-stu-id="30fe5-166">Connect the LED to Pi</span></span>
<span data-ttu-id="30fe5-167">To complete this task, use the [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), the connector wires, the LED, and the resistor.</span><span class="sxs-lookup"><span data-stu-id="30fe5-167">To complete this task, use the [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), the connector wires, the LED, and the resistor.</span></span> <span data-ttu-id="30fe5-168">Connect them to the [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span><span class="sxs-lookup"><span data-stu-id="30fe5-168">Connect them to the [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![Breadboard, LED, and Resistor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="30fe5-170">Connect the shorter leg of the LED to **GPIO GND (Pin 6)**.</span><span class="sxs-lookup"><span data-stu-id="30fe5-170">Connect the shorter leg of the LED to **GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="30fe5-171">Connect the longer leg of the LED to one leg of the resistor.</span><span class="sxs-lookup"><span data-stu-id="30fe5-171">Connect the longer leg of the LED to one leg of the resistor.</span></span>
3. <span data-ttu-id="30fe5-172">Connect the other leg of the resistor to **GPIO 4 (Pin 7)**.</span><span class="sxs-lookup"><span data-stu-id="30fe5-172">Connect the other leg of the resistor to **GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="30fe5-173">Note that the LED polarity is important.</span><span class="sxs-lookup"><span data-stu-id="30fe5-173">Note that the LED polarity is important.</span></span> <span data-ttu-id="30fe5-174">This polarity setting is commonly known as Active Low.</span><span class="sxs-lookup"><span data-stu-id="30fe5-174">This polarity setting is commonly known as Active Low.</span></span>

![Pinout](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="30fe5-176">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="30fe5-176">Congratulations!</span></span> <span data-ttu-id="30fe5-177">You've successfully configured Pi.</span><span class="sxs-lookup"><span data-stu-id="30fe5-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="30fe5-178">Summary</span><span class="sxs-lookup"><span data-stu-id="30fe5-178">Summary</span></span>
<span data-ttu-id="30fe5-179">In this article, you’ve learned how to configure Pi by installing Raspbian, connecting Pi to a network, and connecting an LED to Pi.</span><span class="sxs-lookup"><span data-stu-id="30fe5-179">In this article, you’ve learned how to configure Pi by installing Raspbian, connecting Pi to a network, and connecting an LED to Pi.</span></span> <span data-ttu-id="30fe5-180">Note that the LED doesn't yet light up.</span><span class="sxs-lookup"><span data-stu-id="30fe5-180">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="30fe5-181">The next task is to install the necessary tools and software in preparation for running a sample application on Pi.</span><span class="sxs-lookup"><span data-stu-id="30fe5-181">The next task is to install the necessary tools and software in preparation for running a sample application on Pi.</span></span>

![Hardware is ready](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="30fe5-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="30fe5-183">Next steps</span></span>
[<span data-ttu-id="30fe5-184">Get the tools</span><span class="sxs-lookup"><span data-stu-id="30fe5-184">Get the tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)








