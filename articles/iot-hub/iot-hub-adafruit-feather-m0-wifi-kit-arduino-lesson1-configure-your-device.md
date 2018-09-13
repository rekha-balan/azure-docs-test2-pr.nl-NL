---
title: 'Connect Arduino (C) to Azure IoT - Lesson 1: Configure device | Microsoft Docs'
description: Configure Adafruit Feather M0 WiFi for first-time use.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: arduino set up, connect arduino to pc, setup arduino, arduino board
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: f5b334f0-a148-41aa-b374-ce7b9f5b305a
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 6dbc031215e261241ac89a700c40404a65c91fae
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550376"
---
# <a name="configure-your-device"></a><span data-ttu-id="63561-104">Configure your device</span><span class="sxs-lookup"><span data-stu-id="63561-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="63561-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="63561-105">What you will do</span></span>
<span data-ttu-id="63561-106">Configure your Adafruit Feather M0 WiFi Arduino board for first-time use by assembling the board, powering it up.</span><span class="sxs-lookup"><span data-stu-id="63561-106">Configure your Adafruit Feather M0 WiFi Arduino board for first-time use by assembling the board, powering it up.</span></span> <span data-ttu-id="63561-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="63561-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-you-need"></a><span data-ttu-id="63561-108">What you need</span><span class="sxs-lookup"><span data-stu-id="63561-108">What you need</span></span>
<span data-ttu-id="63561-109">To complete this operation, you need the following parts for your Adafruit Feather M0 WiFi Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="63561-109">To complete this operation, you need the following parts for your Adafruit Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="63561-110">The Adafruit Feather M0 WiFi board</span><span class="sxs-lookup"><span data-stu-id="63561-110">The Adafruit Feather M0 WiFi board</span></span>
* <span data-ttu-id="63561-111">A Micro B to Type A USB cable</span><span class="sxs-lookup"><span data-stu-id="63561-111">A Micro B to Type A USB cable</span></span>

![kit][kit]

<span data-ttu-id="63561-113">You also need:</span><span class="sxs-lookup"><span data-stu-id="63561-113">You also need:</span></span>

* <span data-ttu-id="63561-114">A computer running Windows, Mac, or Linux.</span><span class="sxs-lookup"><span data-stu-id="63561-114">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="63561-115">A wireless connection for your Arduino board to connect to.</span><span class="sxs-lookup"><span data-stu-id="63561-115">A wireless connection for your Arduino board to connect to.</span></span>
* <span data-ttu-id="63561-116">An Internet connection to download configuration tool.</span><span class="sxs-lookup"><span data-stu-id="63561-116">An Internet connection to download configuration tool.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="63561-117">What you will learn</span><span class="sxs-lookup"><span data-stu-id="63561-117">What you will learn</span></span>
<span data-ttu-id="63561-118">In this article, you will learn:</span><span class="sxs-lookup"><span data-stu-id="63561-118">In this article, you will learn:</span></span>

* <span data-ttu-id="63561-119">How to assemble your Arduino board and power it up for the following lessons.</span><span class="sxs-lookup"><span data-stu-id="63561-119">How to assemble your Arduino board and power it up for the following lessons.</span></span>
* <span data-ttu-id="63561-120">How to add serial port permissions on Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="63561-120">How to add serial port permissions on Ubuntu.</span></span>

## <a name="connect-your-arduino-board-to-your-computer"></a><span data-ttu-id="63561-121">Connect your Arduino board to your computer</span><span class="sxs-lookup"><span data-stu-id="63561-121">Connect your Arduino board to your computer</span></span>

1. <span data-ttu-id="63561-122">Plug the micro USB cable into the top micro USB port.</span><span class="sxs-lookup"><span data-stu-id="63561-122">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Top micro USB port][top-micro-usb-port]

2. <span data-ttu-id="63561-124">Plug the other end of USB cable into your computer.</span><span class="sxs-lookup"><span data-stu-id="63561-124">Plug the other end of USB cable into your computer.</span></span>

   ![Computer USB][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a><span data-ttu-id="63561-126">Add serial port permissions on Ubuntu</span><span class="sxs-lookup"><span data-stu-id="63561-126">Add serial port permissions on Ubuntu</span></span>

<span data-ttu-id="63561-127">You can skip this section if you use Windows or macOS.</span><span class="sxs-lookup"><span data-stu-id="63561-127">You can skip this section if you use Windows or macOS.</span></span> <span data-ttu-id="63561-128">For Ubuntu, you need the following steps to make sure the normal linux user has the permissions to operate on the USB port of your Arduino board.</span><span class="sxs-lookup"><span data-stu-id="63561-128">For Ubuntu, you need the following steps to make sure the normal linux user has the permissions to operate on the USB port of your Arduino board.</span></span>

1. <span data-ttu-id="63561-129">Now as normal user from terminal:</span><span class="sxs-lookup"><span data-stu-id="63561-129">Now as normal user from terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="63561-130">You will get something like:</span><span class="sxs-lookup"><span data-stu-id="63561-130">You will get something like:</span></span>

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   <span data-ttu-id="63561-131">The "0" might be a different number, or multiple entries might be returned.</span><span class="sxs-lookup"><span data-stu-id="63561-131">The "0" might be a different number, or multiple entries might be returned.</span></span> <span data-ttu-id="63561-132">In the first case the data we need is `uucp`, in the second is `dialout`, which is the group owner of the file.</span><span class="sxs-lookup"><span data-stu-id="63561-132">In the first case the data we need is `uucp`, in the second is `dialout`, which is the group owner of the file.</span></span>

2. <span data-ttu-id="63561-133">Add user to the to the group:</span><span class="sxs-lookup"><span data-stu-id="63561-133">Add user to the to the group:</span></span>

   ```bash
   sudo usermod -a -G group-name username
   ```

   <span data-ttu-id="63561-134">Where `group-name` is the data found in the first step, and `username` is your linux user name.</span><span class="sxs-lookup"><span data-stu-id="63561-134">Where `group-name` is the data found in the first step, and `username` is your linux user name.</span></span>

3. <span data-ttu-id="63561-135">You will need to log out and in again for this change to take effect and complete the setup.</span><span class="sxs-lookup"><span data-stu-id="63561-135">You will need to log out and in again for this change to take effect and complete the setup.</span></span>

## <a name="summary"></a><span data-ttu-id="63561-136">Summary</span><span class="sxs-lookup"><span data-stu-id="63561-136">Summary</span></span>
<span data-ttu-id="63561-137">In this article, you’ve learned how to configure your Arduino board.</span><span class="sxs-lookup"><span data-stu-id="63561-137">In this article, you’ve learned how to configure your Arduino board.</span></span> <span data-ttu-id="63561-138">The next task is to install the necessary tools and software in preparation for running a sample application on your Arduino board.</span><span class="sxs-lookup"><span data-stu-id="63561-138">The next task is to install the necessary tools and software in preparation for running a sample application on your Arduino board.</span></span>

![Hardware is ready][hardware-is-ready]

## <a name="next-steps"></a><span data-ttu-id="63561-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="63561-140">Next steps</span></span>
<span data-ttu-id="63561-141">[Get the tools][get-the-tools]
<!-- Images and links --></span><span class="sxs-lookup"><span data-stu-id="63561-141">[Get the tools][get-the-tools]
<!-- Images and links --></span></span>

[kit]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md



