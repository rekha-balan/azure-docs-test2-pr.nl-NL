---
title: Send messages to an MQTT server using the Azure MQTT client library | Microsoft Docs
description: Use the DevKit as a client to send messages to an MQTT server
author: liydu
manager: jeffya
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.tgt_pltfrm: arduino
ms.date: 04/02/2018
ms.author: liydu
ms.openlocfilehash: fc74613e00adc459f7a7b0a16c6f773fe4bf601d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855650"
---
# <a name="send-messages-to-an-mqtt-server"></a><span data-ttu-id="6c1bf-103">Send messages to an MQTT server</span><span class="sxs-lookup"><span data-stu-id="6c1bf-103">Send messages to an MQTT server</span></span>

<span data-ttu-id="6c1bf-104">Internet of Things (IoT) systems often deal with intermittent, poor quality, or slow internet connections.</span><span class="sxs-lookup"><span data-stu-id="6c1bf-104">Internet of Things (IoT) systems often deal with intermittent, poor quality, or slow internet connections.</span></span> <span data-ttu-id="6c1bf-105">MQTT is a machine-to-machine (M2M) connectivity protocol, which was developed with such challenges in mind.</span><span class="sxs-lookup"><span data-stu-id="6c1bf-105">MQTT is a machine-to-machine (M2M) connectivity protocol, which was developed with such challenges in mind.</span></span> 

<span data-ttu-id="6c1bf-106">The MQTT client library used here is part of the [Eclipse Paho](http://www.eclipse.org/paho/) project, which provides APIs for using MQTT over multiple means of transport.</span><span class="sxs-lookup"><span data-stu-id="6c1bf-106">The MQTT client library used here is part of the [Eclipse Paho](http://www.eclipse.org/paho/) project, which provides APIs for using MQTT over multiple means of transport.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="6c1bf-107">What you learn</span><span class="sxs-lookup"><span data-stu-id="6c1bf-107">What you learn</span></span>

<span data-ttu-id="6c1bf-108">In this project, you learn:</span><span class="sxs-lookup"><span data-stu-id="6c1bf-108">In this project, you learn:</span></span>
- <span data-ttu-id="6c1bf-109">How to use the MQTT Client library to send messages to an MQTT broker.</span><span class="sxs-lookup"><span data-stu-id="6c1bf-109">How to use the MQTT Client library to send messages to an MQTT broker.</span></span>
- <span data-ttu-id="6c1bf-110">How to configure your MXChip Iot DevKit as an MQTT client.</span><span class="sxs-lookup"><span data-stu-id="6c1bf-110">How to configure your MXChip Iot DevKit as an MQTT client.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6c1bf-111">What you need</span><span class="sxs-lookup"><span data-stu-id="6c1bf-111">What you need</span></span>

<span data-ttu-id="6c1bf-112">Finish the [Getting Started Guide](https://docs.microsoft.com/azure/iot-hub/iot-hub-arduino-iot-devkit-az3166-get-started) to:</span><span class="sxs-lookup"><span data-stu-id="6c1bf-112">Finish the [Getting Started Guide](https://docs.microsoft.com/azure/iot-hub/iot-hub-arduino-iot-devkit-az3166-get-started) to:</span></span>

* <span data-ttu-id="6c1bf-113">Have your DevKit connected to Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="6c1bf-113">Have your DevKit connected to Wi-Fi</span></span>
* <span data-ttu-id="6c1bf-114">Prepare the development environment</span><span class="sxs-lookup"><span data-stu-id="6c1bf-114">Prepare the development environment</span></span>

## <a name="open-the-project-folder"></a><span data-ttu-id="6c1bf-115">Open the project folder</span><span class="sxs-lookup"><span data-stu-id="6c1bf-115">Open the project folder</span></span>

1. <span data-ttu-id="6c1bf-116">If the DevKit is already connect to your computer, disconnect it.</span><span class="sxs-lookup"><span data-stu-id="6c1bf-116">If the DevKit is already connect to your computer, disconnect it.</span></span>

2. <span data-ttu-id="6c1bf-117">Start VS Code.</span><span class="sxs-lookup"><span data-stu-id="6c1bf-117">Start VS Code.</span></span>

3. <span data-ttu-id="6c1bf-118">Connect the DevKit to your computer.</span><span class="sxs-lookup"><span data-stu-id="6c1bf-118">Connect the DevKit to your computer.</span></span>

## <a name="open-the-mqttclient-sample"></a><span data-ttu-id="6c1bf-119">Open the MQTTClient Sample</span><span class="sxs-lookup"><span data-stu-id="6c1bf-119">Open the MQTTClient Sample</span></span>

<span data-ttu-id="6c1bf-120">Expand left side **ARDUINO EXAMPLES** section, browse to **Examples for MXCHIP AZ3166 > MQTT**, and select **MQTTClient**.</span><span class="sxs-lookup"><span data-stu-id="6c1bf-120">Expand left side **ARDUINO EXAMPLES** section, browse to **Examples for MXCHIP AZ3166 > MQTT**, and select **MQTTClient**.</span></span> <span data-ttu-id="6c1bf-121">A new VS Code window opens with a project folder in it.</span><span class="sxs-lookup"><span data-stu-id="6c1bf-121">A new VS Code window opens with a project folder in it.</span></span>

> [!NOTE]
> <span data-ttu-id="6c1bf-122">You can also open example from command palette.</span><span class="sxs-lookup"><span data-stu-id="6c1bf-122">You can also open example from command palette.</span></span> <span data-ttu-id="6c1bf-123">Use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) to open the command palette, type **Arduino**, and then find and select **Arduino: Examples**.</span><span class="sxs-lookup"><span data-stu-id="6c1bf-123">Use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) to open the command palette, type **Arduino**, and then find and select **Arduino: Examples**.</span></span>

## <a name="build-and-upload-the-arduino-sketch-to-the-devkit"></a><span data-ttu-id="6c1bf-124">Build and upload the Arduino sketch to the DevKit</span><span class="sxs-lookup"><span data-stu-id="6c1bf-124">Build and upload the Arduino sketch to the DevKit</span></span>

<span data-ttu-id="6c1bf-125">Type `Ctrl+P` (macOS: `Cmd+P`) to run `task device-upload`.</span><span class="sxs-lookup"><span data-stu-id="6c1bf-125">Type `Ctrl+P` (macOS: `Cmd+P`) to run `task device-upload`.</span></span> <span data-ttu-id="6c1bf-126">Once the upload is completed, DevKit restarts and runs the sketch.</span><span class="sxs-lookup"><span data-stu-id="6c1bf-126">Once the upload is completed, DevKit restarts and runs the sketch.</span></span>

![device-upload](media/iot-hub-arduino-iot-devkit-az3166-mqtt-helloworld/device-upload.jpg)

> [!NOTE]
> <span data-ttu-id="6c1bf-128">You may receive an "Error: AZ3166: Unknown package" error message.</span><span class="sxs-lookup"><span data-stu-id="6c1bf-128">You may receive an "Error: AZ3166: Unknown package" error message.</span></span> <span data-ttu-id="6c1bf-129">This error occurs when the board package index is not refreshed correctly.</span><span class="sxs-lookup"><span data-stu-id="6c1bf-129">This error occurs when the board package index is not refreshed correctly.</span></span> <span data-ttu-id="6c1bf-130">To resolve this error, refer to the [development section of the IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/#development).</span><span class="sxs-lookup"><span data-stu-id="6c1bf-130">To resolve this error, refer to the [development section of the IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/#development).</span></span>

## <a name="test-the-project"></a><span data-ttu-id="6c1bf-131">Test the project</span><span class="sxs-lookup"><span data-stu-id="6c1bf-131">Test the project</span></span>

<span data-ttu-id="6c1bf-132">In VS Code, follow this procedure to open and set up the Serial Monitor:</span><span class="sxs-lookup"><span data-stu-id="6c1bf-132">In VS Code, follow this procedure to open and set up the Serial Monitor:</span></span>

1. <span data-ttu-id="6c1bf-133">Click the `COM[X]` word on the status bar to set the right COM port with `STMicroelectronics`: ![set-com-port](media/iot-hub-arduino-iot-devkit-az3166-mqtt-helloworld/set-com-port.jpg)</span><span class="sxs-lookup"><span data-stu-id="6c1bf-133">Click the `COM[X]` word on the status bar to set the right COM port with `STMicroelectronics`: ![set-com-port](media/iot-hub-arduino-iot-devkit-az3166-mqtt-helloworld/set-com-port.jpg)</span></span>

2. <span data-ttu-id="6c1bf-134">Click the power plug icon on the status bar to open the Serial Monitor: ![serial-monitor](media/iot-hub-arduino-iot-devkit-az3166-mqtt-helloworld/serial-monitor.jpg)</span><span class="sxs-lookup"><span data-stu-id="6c1bf-134">Click the power plug icon on the status bar to open the Serial Monitor: ![serial-monitor](media/iot-hub-arduino-iot-devkit-az3166-mqtt-helloworld/serial-monitor.jpg)</span></span>
  
3. <span data-ttu-id="6c1bf-135">On the status bar, click the number that represents the Baud Rate and set it to `115200`: ![set-baud-rate](media/iot-hub-arduino-iot-devkit-az3166-mqtt-helloworld/set-baud-rate.jpg)</span><span class="sxs-lookup"><span data-stu-id="6c1bf-135">On the status bar, click the number that represents the Baud Rate and set it to `115200`: ![set-baud-rate](media/iot-hub-arduino-iot-devkit-az3166-mqtt-helloworld/set-baud-rate.jpg)</span></span>

<span data-ttu-id="6c1bf-136">The Serial Monitor displays all the messages sent by the sample sketch.</span><span class="sxs-lookup"><span data-stu-id="6c1bf-136">The Serial Monitor displays all the messages sent by the sample sketch.</span></span> <span data-ttu-id="6c1bf-137">The sketch connects the DevKit to Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="6c1bf-137">The sketch connects the DevKit to Wi-Fi.</span></span> <span data-ttu-id="6c1bf-138">Once the Wi-Fi connection is successful, the sketch sends a message to the MQTT broker.</span><span class="sxs-lookup"><span data-stu-id="6c1bf-138">Once the Wi-Fi connection is successful, the sketch sends a message to the MQTT broker.</span></span> <span data-ttu-id="6c1bf-139">After that, the sample repeatedly sends two "iot.eclipse.org" messages using QoS 0 and QoS 1, respectively.</span><span class="sxs-lookup"><span data-stu-id="6c1bf-139">After that, the sample repeatedly sends two "iot.eclipse.org" messages using QoS 0 and QoS 1, respectively.</span></span>

![serial-output](media/iot-hub-arduino-iot-devkit-az3166-mqtt-helloworld/serial-output.jpg)

## <a name="problems-and-feedback"></a><span data-ttu-id="6c1bf-141">Problems and feedback</span><span class="sxs-lookup"><span data-stu-id="6c1bf-141">Problems and feedback</span></span>

<span data-ttu-id="6c1bf-142">If you encounter problems, refer to the [IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) or connect using the following channels:</span><span class="sxs-lookup"><span data-stu-id="6c1bf-142">If you encounter problems, refer to the [IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) or connect using the following channels:</span></span>

* [<span data-ttu-id="6c1bf-143">Gitter.im</span><span class="sxs-lookup"><span data-stu-id="6c1bf-143">Gitter.im</span></span>](http://gitter.im/Microsoft/azure-iot-developer-kit)
* [<span data-ttu-id="6c1bf-144">Stackoverflow</span><span class="sxs-lookup"><span data-stu-id="6c1bf-144">Stackoverflow</span></span>](https://stackoverflow.com/questions/tagged/iot-devkit)

## <a name="see-also"></a><span data-ttu-id="6c1bf-145">See also</span><span class="sxs-lookup"><span data-stu-id="6c1bf-145">See also</span></span>

* [<span data-ttu-id="6c1bf-146">Connect IoT DevKit AZ3166 to Azure IoT Hub in the cloud</span><span class="sxs-lookup"><span data-stu-id="6c1bf-146">Connect IoT DevKit AZ3166 to Azure IoT Hub in the cloud</span></span>](iot-hub-arduino-iot-devkit-az3166-get-started.md)
* [<span data-ttu-id="6c1bf-147">Shake, Shake for a Tweet</span><span class="sxs-lookup"><span data-stu-id="6c1bf-147">Shake, Shake for a Tweet</span></span>](iot-hub-arduino-iot-devkit-az3166-retrieve-twitter-message.md)

## <a name="next-steps"></a><span data-ttu-id="6c1bf-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="6c1bf-148">Next steps</span></span>

<span data-ttu-id="6c1bf-149">Now that you have learned how to configure your MXChip Iot DevKit as an MQTT client and use the MQTT Client library to send messages to an MQTT broker, here are the suggested next steps:</span><span class="sxs-lookup"><span data-stu-id="6c1bf-149">Now that you have learned how to configure your MXChip Iot DevKit as an MQTT client and use the MQTT Client library to send messages to an MQTT broker, here are the suggested next steps:</span></span>

* [<span data-ttu-id="6c1bf-150">Azure IoT Remote Monitoring solution accelerator overview</span><span class="sxs-lookup"><span data-stu-id="6c1bf-150">Azure IoT Remote Monitoring solution accelerator overview</span></span>](https://docs.microsoft.com/azure/iot-suite/)
* [<span data-ttu-id="6c1bf-151">Connect an MXChip IoT DevKit device to your Azure IoT Central application</span><span class="sxs-lookup"><span data-stu-id="6c1bf-151">Connect an MXChip IoT DevKit device to your Azure IoT Central application</span></span>](https://docs.microsoft.com/microsoft-iot-central/howto-connect-devkit)
