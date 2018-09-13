---
title: IoT DevKit to cloud -- Connect IoT DevKit AZ3166 to Azure IoT Hub | Microsoft Docs
description: In this tutorial, learn how to set up and connect IoT DevKit AZ3166 to Azure IoT Hub so it can send data to the Azure cloud platform.
author: rangv
manager: jeffya
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.tgt_pltfrm: arduino
ms.date: 08/27/2018
ms.author: rangv
ms.openlocfilehash: 6ecddefd264bf4a6f57dd7fcd09c3a8cc10ec54a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865909"
---
# <a name="connect-iot-devkit-az3166-to-azure-iot-hub"></a><span data-ttu-id="444b4-103">Connect IoT DevKit AZ3166 to Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="444b4-103">Connect IoT DevKit AZ3166 to Azure IoT Hub</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="444b4-104">You can use the [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) to develop and prototype Internet of Things (IoT) solutions that take advantage of Microsoft Azure services.</span><span class="sxs-lookup"><span data-stu-id="444b4-104">You can use the [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) to develop and prototype Internet of Things (IoT) solutions that take advantage of Microsoft Azure services.</span></span> <span data-ttu-id="444b4-105">It includes an Arduino-compatible board with rich peripherals and sensors, an open-source board package, and a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span><span class="sxs-lookup"><span data-stu-id="444b4-105">It includes an Arduino-compatible board with rich peripherals and sensors, an open-source board package, and a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="444b4-106">What you do</span><span class="sxs-lookup"><span data-stu-id="444b4-106">What you do</span></span>

<span data-ttu-id="444b4-107">Connect the [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) to an Azure IoT hub that you create, collect the temperature and humidity data from sensors, and send the data to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="444b4-107">Connect the [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) to an Azure IoT hub that you create, collect the temperature and humidity data from sensors, and send the data to the IoT hub.</span></span>

<span data-ttu-id="444b4-108">Don't have a DevKit yet?</span><span class="sxs-lookup"><span data-stu-id="444b4-108">Don't have a DevKit yet?</span></span> <span data-ttu-id="444b4-109">Try the [DevKit simulator](https://azure-samples.github.io/iot-devkit-web-simulator/) or [purchase a DevKit](https://aka.ms/iot-devkit-purchase).</span><span class="sxs-lookup"><span data-stu-id="444b4-109">Try the [DevKit simulator](https://azure-samples.github.io/iot-devkit-web-simulator/) or [purchase a DevKit](https://aka.ms/iot-devkit-purchase).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="444b4-110">What you learn</span><span class="sxs-lookup"><span data-stu-id="444b4-110">What you learn</span></span>

* <span data-ttu-id="444b4-111">How to connect the IoT DevKit to a wireless access point and prepare your development environment.</span><span class="sxs-lookup"><span data-stu-id="444b4-111">How to connect the IoT DevKit to a wireless access point and prepare your development environment.</span></span>
* <span data-ttu-id="444b4-112">How to create an IoT hub and register a device for the MXChip IoT DevKit.</span><span class="sxs-lookup"><span data-stu-id="444b4-112">How to create an IoT hub and register a device for the MXChip IoT DevKit.</span></span>
* <span data-ttu-id="444b4-113">How to collect sensor data by running a sample application on the MXChip IoT DevKit.</span><span class="sxs-lookup"><span data-stu-id="444b4-113">How to collect sensor data by running a sample application on the MXChip IoT DevKit.</span></span>
* <span data-ttu-id="444b4-114">How to send the sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="444b4-114">How to send the sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="444b4-115">What you need</span><span class="sxs-lookup"><span data-stu-id="444b4-115">What you need</span></span>

* <span data-ttu-id="444b4-116">An MXChip IoT DevKit board with a Micro-USB cable.</span><span class="sxs-lookup"><span data-stu-id="444b4-116">An MXChip IoT DevKit board with a Micro-USB cable.</span></span> <span data-ttu-id="444b4-117">[Get it now](https://aka.ms/iot-devkit-purchase).</span><span class="sxs-lookup"><span data-stu-id="444b4-117">[Get it now](https://aka.ms/iot-devkit-purchase).</span></span>
* <span data-ttu-id="444b4-118">A computer running Windows 10 or macOS 10.10+.</span><span class="sxs-lookup"><span data-stu-id="444b4-118">A computer running Windows 10 or macOS 10.10+.</span></span>
* <span data-ttu-id="444b4-119">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="444b4-119">An active Azure subscription.</span></span> <span data-ttu-id="444b4-120">[Activate a free 30-day trial Microsoft Azure account](https://azureinfo.microsoft.com/us-freetrial.html).</span><span class="sxs-lookup"><span data-stu-id="444b4-120">[Activate a free 30-day trial Microsoft Azure account](https://azureinfo.microsoft.com/us-freetrial.html).</span></span>
  
## <a name="prepare-your-hardware"></a><span data-ttu-id="444b4-121">Prepare your hardware</span><span class="sxs-lookup"><span data-stu-id="444b4-121">Prepare your hardware</span></span>

<span data-ttu-id="444b4-122">Hook up the following hardware to your computer:</span><span class="sxs-lookup"><span data-stu-id="444b4-122">Hook up the following hardware to your computer:</span></span>

* <span data-ttu-id="444b4-123">DevKit board</span><span class="sxs-lookup"><span data-stu-id="444b4-123">DevKit board</span></span>
* <span data-ttu-id="444b4-124">Micro-USB cable</span><span class="sxs-lookup"><span data-stu-id="444b4-124">Micro-USB cable</span></span>

![Required hardware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

<span data-ttu-id="444b4-126">To connect the DevKit to your computer, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="444b4-126">To connect the DevKit to your computer, follow these steps:</span></span>

1. <span data-ttu-id="444b4-127">Connect the USB end to your computer.</span><span class="sxs-lookup"><span data-stu-id="444b4-127">Connect the USB end to your computer.</span></span>

2. <span data-ttu-id="444b4-128">Connect the Micro-USB end to the DevKit.</span><span class="sxs-lookup"><span data-stu-id="444b4-128">Connect the Micro-USB end to the DevKit.</span></span>

3. <span data-ttu-id="444b4-129">The green LED for power confirms the connection.</span><span class="sxs-lookup"><span data-stu-id="444b4-129">The green LED for power confirms the connection.</span></span>

   ![Hardware connections](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wi-fi"></a><span data-ttu-id="444b4-131">Configure Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="444b4-131">Configure Wi-Fi</span></span>

<span data-ttu-id="444b4-132">IoT projects rely on internet connectivity.</span><span class="sxs-lookup"><span data-stu-id="444b4-132">IoT projects rely on internet connectivity.</span></span> <span data-ttu-id="444b4-133">Use the following instructions to configure the DevKit to connect to Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="444b4-133">Use the following instructions to configure the DevKit to connect to Wi-Fi.</span></span>

### <a name="enter-ap-mode"></a><span data-ttu-id="444b4-134">Enter AP mode</span><span class="sxs-lookup"><span data-stu-id="444b4-134">Enter AP mode</span></span>

<span data-ttu-id="444b4-135">Hold down button B, push and release the reset button, and then release button B. Your DevKit enters AP mode for configuring Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="444b4-135">Hold down button B, push and release the reset button, and then release button B. Your DevKit enters AP mode for configuring Wi-Fi.</span></span> <span data-ttu-id="444b4-136">The screen displays the service set identifier (SSID) of the DevKit and the configuration portal IP address.</span><span class="sxs-lookup"><span data-stu-id="444b4-136">The screen displays the service set identifier (SSID) of the DevKit and the configuration portal IP address.</span></span>

![Reset button, button B, and SSID](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-to-devkit-ap"></a><span data-ttu-id="444b4-138">Connect to DevKit AP</span><span class="sxs-lookup"><span data-stu-id="444b4-138">Connect to DevKit AP</span></span>

<span data-ttu-id="444b4-139">Now, use another Wi-Fi enabled device (computer or mobile phone) to connect to the DevKit SSID (highlighted in the previous image).</span><span class="sxs-lookup"><span data-stu-id="444b4-139">Now, use another Wi-Fi enabled device (computer or mobile phone) to connect to the DevKit SSID (highlighted in the previous image).</span></span> <span data-ttu-id="444b4-140">Leave the password empty.</span><span class="sxs-lookup"><span data-stu-id="444b4-140">Leave the password empty.</span></span>

![Network info and Connect button](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wi-fi-for-the-devkit"></a><span data-ttu-id="444b4-142">Configure Wi-Fi for the DevKit</span><span class="sxs-lookup"><span data-stu-id="444b4-142">Configure Wi-Fi for the DevKit</span></span>

<span data-ttu-id="444b4-143">Open the IP address shown on the DevKit screen on your computer or mobile phone browser, select the Wi-Fi network that you want the DevKit to connect to, and then type the password.</span><span class="sxs-lookup"><span data-stu-id="444b4-143">Open the IP address shown on the DevKit screen on your computer or mobile phone browser, select the Wi-Fi network that you want the DevKit to connect to, and then type the password.</span></span> <span data-ttu-id="444b4-144">Select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="444b4-144">Select **Connect**.</span></span>

![Password box and Connect button](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

<span data-ttu-id="444b4-146">When the connection succeeds, the DevKit reboots in a few seconds.</span><span class="sxs-lookup"><span data-stu-id="444b4-146">When the connection succeeds, the DevKit reboots in a few seconds.</span></span> <span data-ttu-id="444b4-147">You then see the Wi-Fi name and IP address on the screen:</span><span class="sxs-lookup"><span data-stu-id="444b4-147">You then see the Wi-Fi name and IP address on the screen:</span></span>

![Wi-Fi name and IP address](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
> <span data-ttu-id="444b4-149">The IP address displayed in the photo might not match the actual IP address assigned and displayed on the DevKit screen.</span><span class="sxs-lookup"><span data-stu-id="444b4-149">The IP address displayed in the photo might not match the actual IP address assigned and displayed on the DevKit screen.</span></span> <span data-ttu-id="444b4-150">This is normal, because Wi-Fi uses DHCP to dynamically assign IPs.</span><span class="sxs-lookup"><span data-stu-id="444b4-150">This is normal, because Wi-Fi uses DHCP to dynamically assign IPs.</span></span>

<span data-ttu-id="444b4-151">After Wi-Fi is configured, your credentials will persist on the device for that connection, even if the device is unplugged.</span><span class="sxs-lookup"><span data-stu-id="444b4-151">After Wi-Fi is configured, your credentials will persist on the device for that connection, even if the device is unplugged.</span></span> <span data-ttu-id="444b4-152">For example, if you configure the DevKit for Wi-Fi in your home and then take the DevKit to the office, you will need to reconfigure AP mode (starting at the step in the "Enter AP Mode" section) to connect the DevKit to your office Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="444b4-152">For example, if you configure the DevKit for Wi-Fi in your home and then take the DevKit to the office, you will need to reconfigure AP mode (starting at the step in the "Enter AP Mode" section) to connect the DevKit to your office Wi-Fi.</span></span> 

## <a name="start-using-the-devkit"></a><span data-ttu-id="444b4-153">Start using the DevKit</span><span class="sxs-lookup"><span data-stu-id="444b4-153">Start using the DevKit</span></span>

<span data-ttu-id="444b4-154">The default app running on the DevKit checks the latest version of the firmware and displays some sensor diagnosis data for you.</span><span class="sxs-lookup"><span data-stu-id="444b4-154">The default app running on the DevKit checks the latest version of the firmware and displays some sensor diagnosis data for you.</span></span>

### <a name="upgrade-to-the-latest-firmware"></a><span data-ttu-id="444b4-155">Upgrade to the latest firmware</span><span class="sxs-lookup"><span data-stu-id="444b4-155">Upgrade to the latest firmware</span></span>

> [!NOTE]
> <span data-ttu-id="444b4-156">Since v1.1, DevKit enables ST-SAFE in bootloader.</span><span class="sxs-lookup"><span data-stu-id="444b4-156">Since v1.1, DevKit enables ST-SAFE in bootloader.</span></span> <span data-ttu-id="444b4-157">You need to upgrade the firmware if you are running a version prior to v1.1.</span><span class="sxs-lookup"><span data-stu-id="444b4-157">You need to upgrade the firmware if you are running a version prior to v1.1.</span></span>

<span data-ttu-id="444b4-158">If you need a firmware upgrade, the screen will show the current and latest firmware versions.</span><span class="sxs-lookup"><span data-stu-id="444b4-158">If you need a firmware upgrade, the screen will show the current and latest firmware versions.</span></span> <span data-ttu-id="444b4-159">To upgrade, follow the [Upgrade firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/firmware-upgrading/) guide.</span><span class="sxs-lookup"><span data-stu-id="444b4-159">To upgrade, follow the [Upgrade firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/firmware-upgrading/) guide.</span></span>

![Display of current and latest firmware versions](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE]
> <span data-ttu-id="444b4-161">This is a one-time effort.</span><span class="sxs-lookup"><span data-stu-id="444b4-161">This is a one-time effort.</span></span> <span data-ttu-id="444b4-162">After you start developing on the DevKit and upload your app, the latest firmware will come with your app.</span><span class="sxs-lookup"><span data-stu-id="444b4-162">After you start developing on the DevKit and upload your app, the latest firmware will come with your app.</span></span>

### <a name="test-various-sensors"></a><span data-ttu-id="444b4-163">Test various sensors</span><span class="sxs-lookup"><span data-stu-id="444b4-163">Test various sensors</span></span>

<span data-ttu-id="444b4-164">Press button B to test the sensors.</span><span class="sxs-lookup"><span data-stu-id="444b4-164">Press button B to test the sensors.</span></span> <span data-ttu-id="444b4-165">Continue pressing and releasing the button B to cycle through each sensor.</span><span class="sxs-lookup"><span data-stu-id="444b4-165">Continue pressing and releasing the button B to cycle through each sensor.</span></span>

![Button B and sensor display](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-the-development-environment"></a><span data-ttu-id="444b4-167">Prepare the development environment</span><span class="sxs-lookup"><span data-stu-id="444b4-167">Prepare the development environment</span></span>

### <a name="install-azure-iot-workbench"></a><span data-ttu-id="444b4-168">Install Azure IoT Workbench</span><span class="sxs-lookup"><span data-stu-id="444b4-168">Install Azure IoT Workbench</span></span>

<span data-ttu-id="444b4-169">We recommend [Azure IoT Workbench](https://aka.ms/iot-workbench) extension for Visual Studio Code to develop on the DevKit.</span><span class="sxs-lookup"><span data-stu-id="444b4-169">We recommend [Azure IoT Workbench](https://aka.ms/iot-workbench) extension for Visual Studio Code to develop on the DevKit.</span></span>

<span data-ttu-id="444b4-170">Azure IoT Workbench provides an integrated experience to develop IoT solutions.</span><span class="sxs-lookup"><span data-stu-id="444b4-170">Azure IoT Workbench provides an integrated experience to develop IoT solutions.</span></span> <span data-ttu-id="444b4-171">It helps both on device and cloud development using Azure IoT and other services.</span><span class="sxs-lookup"><span data-stu-id="444b4-171">It helps both on device and cloud development using Azure IoT and other services.</span></span> <span data-ttu-id="444b4-172">You can watch this Channel9 video to have an overview of what it does.</span><span class="sxs-lookup"><span data-stu-id="444b4-172">You can watch this Channel9 video to have an overview of what it does.</span></span>

<span data-ttu-id="444b4-173">Follow these steps to prepare the development environment for DevKit:</span><span class="sxs-lookup"><span data-stu-id="444b4-173">Follow these steps to prepare the development environment for DevKit:</span></span>

1. <span data-ttu-id="444b4-174">Download and install [Arduino IDE](https://www.arduino.cc/en/Main/Software).</span><span class="sxs-lookup"><span data-stu-id="444b4-174">Download and install [Arduino IDE](https://www.arduino.cc/en/Main/Software).</span></span> <span data-ttu-id="444b4-175">It provides the necessary toolchain for compiling and uploading Arduino code.</span><span class="sxs-lookup"><span data-stu-id="444b4-175">It provides the necessary toolchain for compiling and uploading Arduino code.</span></span>
    * <span data-ttu-id="444b4-176">**Windows**: Use Windows Installer version.</span><span class="sxs-lookup"><span data-stu-id="444b4-176">**Windows**: Use Windows Installer version.</span></span>
    * <span data-ttu-id="444b4-177">**macOS**: Drag and drop the extracted **Arduino.app** into `/Applications` folder.</span><span class="sxs-lookup"><span data-stu-id="444b4-177">**macOS**: Drag and drop the extracted **Arduino.app** into `/Applications` folder.</span></span>
    * <span data-ttu-id="444b4-178">**Ubuntu**: Unzip it into folder such as `$HOME/Downloads/arduino-1.8.5`</span><span class="sxs-lookup"><span data-stu-id="444b4-178">**Ubuntu**: Unzip it into folder such as `$HOME/Downloads/arduino-1.8.5`</span></span>

1. <span data-ttu-id="444b4-179">Install [Visual Studio Code](https://code.visualstudio.com/), a cross platform source code editor with powerful developer tooling, like IntelliSense code completion and debugging.</span><span class="sxs-lookup"><span data-stu-id="444b4-179">Install [Visual Studio Code](https://code.visualstudio.com/), a cross platform source code editor with powerful developer tooling, like IntelliSense code completion and debugging.</span></span>

1. <span data-ttu-id="444b4-180">Look for **Azure IoT Workbench** in the extension marketplace and install it.</span><span class="sxs-lookup"><span data-stu-id="444b4-180">Look for **Azure IoT Workbench** in the extension marketplace and install it.</span></span>
    <span data-ttu-id="444b4-181">![Install Azure IoT Workbench](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install-workbench.png) Together with the IoT Workbench, other dependent extensions will be installed.</span><span class="sxs-lookup"><span data-stu-id="444b4-181">![Install Azure IoT Workbench](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install-workbench.png) Together with the IoT Workbench, other dependent extensions will be installed.</span></span>

1. <span data-ttu-id="444b4-182">Open **File > Preference > Settings** and add following lines to configure Arduino.</span><span class="sxs-lookup"><span data-stu-id="444b4-182">Open **File > Preference > Settings** and add following lines to configure Arduino.</span></span>
    * <span data-ttu-id="444b4-183">**Windows**:</span><span class="sxs-lookup"><span data-stu-id="444b4-183">**Windows**:</span></span>
    ```javascript
    "arduino.path": "C:\\Program Files (x86)\\Arduino",
    "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
    ```
    * <span data-ttu-id="444b4-184">**macOS**:</span><span class="sxs-lookup"><span data-stu-id="444b4-184">**macOS**:</span></span>
    ```javascript
    "arduino.path": "/Applications",
    "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
    ```
    * <span data-ttu-id="444b4-185">**Ubuntu**:</span><span class="sxs-lookup"><span data-stu-id="444b4-185">**Ubuntu**:</span></span>
    ```javascript
    "arduino.path": "/home/{username}/Downloads/arduino-1.8.5",
    "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
    ```

1. <span data-ttu-id="444b4-186">Click `F1` to open the command palette, type and select **Arduino: Board Manager**.</span><span class="sxs-lookup"><span data-stu-id="444b4-186">Click `F1` to open the command palette, type and select **Arduino: Board Manager**.</span></span> <span data-ttu-id="444b4-187">Search for **AZ3166** and install the latest version.</span><span class="sxs-lookup"><span data-stu-id="444b4-187">Search for **AZ3166** and install the latest version.</span></span>
    <span data-ttu-id="444b4-188">![Install DevKit SDK](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install-sdk.png)</span><span class="sxs-lookup"><span data-stu-id="444b4-188">![Install DevKit SDK](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install-sdk.png)</span></span>

### <a name="install-st-link-drivers"></a><span data-ttu-id="444b4-189">Install ST-Link drivers</span><span class="sxs-lookup"><span data-stu-id="444b4-189">Install ST-Link drivers</span></span>

<span data-ttu-id="444b4-190">[ST-Link/V2](http://www.st.com/en/development-tools/st-link-v2.html) is the USB interface that IoT DevKit uses to communicate with your development machine.</span><span class="sxs-lookup"><span data-stu-id="444b4-190">[ST-Link/V2](http://www.st.com/en/development-tools/st-link-v2.html) is the USB interface that IoT DevKit uses to communicate with your development machine.</span></span> <span data-ttu-id="444b4-191">Follow the OS-specific steps to allow the machine access to your device.</span><span class="sxs-lookup"><span data-stu-id="444b4-191">Follow the OS-specific steps to allow the machine access to your device.</span></span>

* <span data-ttu-id="444b4-192">**Windows**: Download and install USB driver from [STMicroelectronics website](http://www.st.com/en/development-tools/stsw-link009.html).</span><span class="sxs-lookup"><span data-stu-id="444b4-192">**Windows**: Download and install USB driver from [STMicroelectronics website](http://www.st.com/en/development-tools/stsw-link009.html).</span></span>
* <span data-ttu-id="444b4-193">**macOS**: No driver is required for macOS.</span><span class="sxs-lookup"><span data-stu-id="444b4-193">**macOS**: No driver is required for macOS.</span></span>
* <span data-ttu-id="444b4-194">**Ubuntu**: Run the following in terminal and logout and login for the group change to take effect:</span><span class="sxs-lookup"><span data-stu-id="444b4-194">**Ubuntu**: Run the following in terminal and logout and login for the group change to take effect:</span></span>
    ```bash
    # Copy the default rules. This grants permission to the group 'plugdev'
    sudo cp ~/.arduino15/packages/AZ3166/tools/openocd/0.10.0/linux/contrib/60-openocd.rules /etc/udev/rules.d/
    sudo udevadm control --reload-rules

    # Add yourself to the group 'plugdev'
    # Logout and log back in for the group to take effect
    sudo usermod -a -G plugdev $(whoami)
    ```

<span data-ttu-id="444b4-195">Now you are all set with preparing and configuring your development environment.</span><span class="sxs-lookup"><span data-stu-id="444b4-195">Now you are all set with preparing and configuring your development environment.</span></span> <span data-ttu-id="444b4-196">Let us build the “Hello World” sample for IoT: sending temperature telemetry data to Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="444b4-196">Let us build the “Hello World” sample for IoT: sending temperature telemetry data to Azure IoT Hub.</span></span>

## <a name="build-your-first-project"></a><span data-ttu-id="444b4-197">Build your first project</span><span class="sxs-lookup"><span data-stu-id="444b4-197">Build your first project</span></span>

1. <span data-ttu-id="444b4-198">Make sure your IoT DevKit is **not connected** to your computer.</span><span class="sxs-lookup"><span data-stu-id="444b4-198">Make sure your IoT DevKit is **not connected** to your computer.</span></span> <span data-ttu-id="444b4-199">Start VS Code first, and then connect the DevKit to your computer.</span><span class="sxs-lookup"><span data-stu-id="444b4-199">Start VS Code first, and then connect the DevKit to your computer.</span></span>

1. <span data-ttu-id="444b4-200">In the bottom right status bar, check the **MXCHIP AZ3166** is shown as selected board and serial port with **STMicroelectronics** is used.</span><span class="sxs-lookup"><span data-stu-id="444b4-200">In the bottom right status bar, check the **MXCHIP AZ3166** is shown as selected board and serial port with **STMicroelectronics** is used.</span></span>
    <span data-ttu-id="444b4-201">![Select board and COM](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/select-board.png)</span><span class="sxs-lookup"><span data-stu-id="444b4-201">![Select board and COM](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/select-board.png)</span></span>

1. <span data-ttu-id="444b4-202">Click `F1` to open the command palette, type and select **IoT Workbench: Examples**.</span><span class="sxs-lookup"><span data-stu-id="444b4-202">Click `F1` to open the command palette, type and select **IoT Workbench: Examples**.</span></span> <span data-ttu-id="444b4-203">Then select **IoT DevKit** as board.</span><span class="sxs-lookup"><span data-stu-id="444b4-203">Then select **IoT DevKit** as board.</span></span>

1. <span data-ttu-id="444b4-204">In the IoT Workbench Examples page, find **Get Started** and click **Open Sample**.</span><span class="sxs-lookup"><span data-stu-id="444b4-204">In the IoT Workbench Examples page, find **Get Started** and click **Open Sample**.</span></span> <span data-ttu-id="444b4-205">Then selects the default path to download the sample code.</span><span class="sxs-lookup"><span data-stu-id="444b4-205">Then selects the default path to download the sample code.</span></span>
    <span data-ttu-id="444b4-206">![Open sample](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/open-sample.png)</span><span class="sxs-lookup"><span data-stu-id="444b4-206">![Open sample](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/open-sample.png)</span></span>

1. <span data-ttu-id="444b4-207">If you don't have Arduino extension in VS Code installed, click the **Install** in the notification pane.</span><span class="sxs-lookup"><span data-stu-id="444b4-207">If you don't have Arduino extension in VS Code installed, click the **Install** in the notification pane.</span></span>
    <span data-ttu-id="444b4-208">![Install Arduino Extension](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install-arduino-ext.png)</span><span class="sxs-lookup"><span data-stu-id="444b4-208">![Install Arduino Extension](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install-arduino-ext.png)</span></span>

1. <span data-ttu-id="444b4-209">In the new opened project window, click `F1` to open the command palette, type and select **IoT Workbench: Cloud**, then select **Azure Provision**.</span><span class="sxs-lookup"><span data-stu-id="444b4-209">In the new opened project window, click `F1` to open the command palette, type and select **IoT Workbench: Cloud**, then select **Azure Provision**.</span></span> <span data-ttu-id="444b4-210">Follow the step by step guide to finish provisioning your Azure IoT Hub and creating the device.</span><span class="sxs-lookup"><span data-stu-id="444b4-210">Follow the step by step guide to finish provisioning your Azure IoT Hub and creating the device.</span></span>
    <span data-ttu-id="444b4-211">![Cloud provision](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/cloud-provision.png)</span><span class="sxs-lookup"><span data-stu-id="444b4-211">![Cloud provision](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/cloud-provision.png)</span></span>

1. <span data-ttu-id="444b4-212">Click `F1` to open the command palette, type and select **IoT Workbench: Device**, then select **Config Device Settings > Select IoT Hub Device Connection String**.</span><span class="sxs-lookup"><span data-stu-id="444b4-212">Click `F1` to open the command palette, type and select **IoT Workbench: Device**, then select **Config Device Settings > Select IoT Hub Device Connection String**.</span></span>

1. <span data-ttu-id="444b4-213">On DevKit, hold down **button A**, push and release the **reset** button, and then release **button A**. Your DevKit enters configuration mode and saves the connection string.</span><span class="sxs-lookup"><span data-stu-id="444b4-213">On DevKit, hold down **button A**, push and release the **reset** button, and then release **button A**. Your DevKit enters configuration mode and saves the connection string.</span></span>
    <span data-ttu-id="444b4-214">![Connection string](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="444b4-214">![Connection string](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connection-string.png)</span></span>

1. <span data-ttu-id="444b4-215">Click `F1` again, type and select **IoT Workbench: Device**, then select **Device Upload**.</span><span class="sxs-lookup"><span data-stu-id="444b4-215">Click `F1` again, type and select **IoT Workbench: Device**, then select **Device Upload**.</span></span>
    <span data-ttu-id="444b4-216">![Arduino upload](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/arduino-upload.png)</span><span class="sxs-lookup"><span data-stu-id="444b4-216">![Arduino upload](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/arduino-upload.png)</span></span>

<span data-ttu-id="444b4-217">The DevKit reboots and starts running the code.</span><span class="sxs-lookup"><span data-stu-id="444b4-217">The DevKit reboots and starts running the code.</span></span>

> [!NOTE]
> <span data-ttu-id="444b4-218">If there is errors or interruptions, you can always recover by running the command again.</span><span class="sxs-lookup"><span data-stu-id="444b4-218">If there is errors or interruptions, you can always recover by running the command again.</span></span>

## <a name="test-the-project"></a><span data-ttu-id="444b4-219">Test the project</span><span class="sxs-lookup"><span data-stu-id="444b4-219">Test the project</span></span>

### <a name="view-the-telemetry-sent-to-azure-iot-hub"></a><span data-ttu-id="444b4-220">View the telemetry sent to Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="444b4-220">View the telemetry sent to Azure IoT Hub</span></span>

<span data-ttu-id="444b4-221">Click the power plug icon on the status bar to open the Serial Monitor: ![Serial monitor](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/serial-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="444b4-221">Click the power plug icon on the status bar to open the Serial Monitor: ![Serial monitor](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/serial-monitor.png)</span></span>

<span data-ttu-id="444b4-222">The sample application is running successfully when you see the following results:</span><span class="sxs-lookup"><span data-stu-id="444b4-222">The sample application is running successfully when you see the following results:</span></span>

* <span data-ttu-id="444b4-223">The Serial Monitor displays the message sent to the IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="444b4-223">The Serial Monitor displays the message sent to the IoT Hub.</span></span>
* <span data-ttu-id="444b4-224">The LED on the MXChip IoT DevKit is blinking.</span><span class="sxs-lookup"><span data-stu-id="444b4-224">The LED on the MXChip IoT DevKit is blinking.</span></span>

![Serial monitor output](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/result-serial-output.png)

### <a name="view-the-telemetry-received-by-azure-iot-hub"></a><span data-ttu-id="444b4-226">View the telemetry received by Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="444b4-226">View the telemetry received by Azure IoT Hub</span></span>

<span data-ttu-id="444b4-227">You can use [Azure IoT Toolkit](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit) to monitor device-to-cloud (D2C) messages in IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="444b4-227">You can use [Azure IoT Toolkit](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-toolkit) to monitor device-to-cloud (D2C) messages in IoT Hub.</span></span>

1. <span data-ttu-id="444b4-228">In Visual Studio Code, look for **Azure IoT Toolkit** in the extension marketplace and install it.</span><span class="sxs-lookup"><span data-stu-id="444b4-228">In Visual Studio Code, look for **Azure IoT Toolkit** in the extension marketplace and install it.</span></span>

1. <span data-ttu-id="444b4-229">Log in [Azure portal](https://portal.azure.com/), find the IoT Hub you created.</span><span class="sxs-lookup"><span data-stu-id="444b4-229">Log in [Azure portal](https://portal.azure.com/), find the IoT Hub you created.</span></span>
    <span data-ttu-id="444b4-230">![Azure portal](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/azure-iot-hub-portal.png)</span><span class="sxs-lookup"><span data-stu-id="444b4-230">![Azure portal](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/azure-iot-hub-portal.png)</span></span>

1. <span data-ttu-id="444b4-231">In the **Shared access policies** pane, click the **iothubowner policy**, and write down the Connection string of your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="444b4-231">In the **Shared access policies** pane, click the **iothubowner policy**, and write down the Connection string of your IoT hub.</span></span>
    <span data-ttu-id="444b4-232">![Azure IoT Hub connection string](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/azure-portal-conn-string.png)</span><span class="sxs-lookup"><span data-stu-id="444b4-232">![Azure IoT Hub connection string](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/azure-portal-conn-string.png)</span></span>

1. <span data-ttu-id="444b4-233">In Visual Studio Code, expand **AZURE IOT HUB DEVICES** on the bottom left corner, click **Set IoT Hub Connection String**.</span><span class="sxs-lookup"><span data-stu-id="444b4-233">In Visual Studio Code, expand **AZURE IOT HUB DEVICES** on the bottom left corner, click **Set IoT Hub Connection String**.</span></span>
    <span data-ttu-id="444b4-234">![Set Azure IoT Hub connection string](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/azure-iot-toolkit-conn-string.png)</span><span class="sxs-lookup"><span data-stu-id="444b4-234">![Set Azure IoT Hub connection string](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/azure-iot-toolkit-conn-string.png)</span></span>

1. <span data-ttu-id="444b4-235">Click **IoT: Start monitoring D2C message** in context menu.</span><span class="sxs-lookup"><span data-stu-id="444b4-235">Click **IoT: Start monitoring D2C message** in context menu.</span></span>

1. <span data-ttu-id="444b4-236">In **OUTPUT** pane, you can see the incoming D2C messages to the IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="444b4-236">In **OUTPUT** pane, you can see the incoming D2C messages to the IoT Hub.</span></span>
    <span data-ttu-id="444b4-237">![D2C message](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/azure-iot-toolkit-console.png)</span><span class="sxs-lookup"><span data-stu-id="444b4-237">![D2C message](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/azure-iot-toolkit-console.png)</span></span>

## <a name="problems-and-feedback"></a><span data-ttu-id="444b4-238">Problems and feedback</span><span class="sxs-lookup"><span data-stu-id="444b4-238">Problems and feedback</span></span>

<span data-ttu-id="444b4-239">If you encounter problems, you can check for a solution in the [IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) or reach out to us from [Gitter](https://gitter.im/Microsoft/azure-iot-developer-kit).</span><span class="sxs-lookup"><span data-stu-id="444b4-239">If you encounter problems, you can check for a solution in the [IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) or reach out to us from [Gitter](https://gitter.im/Microsoft/azure-iot-developer-kit).</span></span> <span data-ttu-id="444b4-240">You can also give us feedback by leaving a comment on this page.</span><span class="sxs-lookup"><span data-stu-id="444b4-240">You can also give us feedback by leaving a comment on this page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="444b4-241">Next steps</span><span class="sxs-lookup"><span data-stu-id="444b4-241">Next steps</span></span>

<span data-ttu-id="444b4-242">You have successfully connected an MXChip IoT DevKit to your IoT hub, and you have sent the captured sensor data to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="444b4-242">You have successfully connected an MXChip IoT DevKit to your IoT hub, and you have sent the captured sensor data to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-az3166-next-steps](../../includes/iot-hub-get-started-az3166-next-steps.md)]
