---
title: IoT DevKit to cloud -- Connect IoT DevKit AZ3166 to Remote Monitoring IoT solution accelerator | Microsoft Docs
description: In this tutorial, learn how to send status of sensors on IoT DevKit AZ3166 to Remote Monitoring IoT solution accelerator for monitoring and visualization.
author: isabelcabezasm
manager: ''
ms.service: iot-accelerators
services: iot-accelerators
ms.devlang: c
ms.topic: conceptual
ms.date: 05/09/2018
ms.author: isacabe
ms.openlocfilehash: 35ef6ef02e5ae8a4b9231121615f44e0dc00ad15
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870323"
---
# <a name="connect-mxchip-iot-devkit-az3166-to-the-iot-remote-monitoring-solution-accelerator"></a>Connect MXChip IoT DevKit AZ3166 to the IoT Remote Monitoring solution accelerator

[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

In this tutorial, you learn how to run a sample app on your DevKit to send sensor data to your solution accelerator.

The [MXChip IoT DevKit](https://aka.ms/iot-devkit) is an all-in-one Arduino compatible board with rich peripherals and sensors. You can develop for it using [Azure IoT Workbench](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-iot-workbench) in Visual Studio Code. And it comes with a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/) to guide you prototype Internet of Things (IoT) solutions that take advantage of Microsoft Azure services.

## <a name="what-you-need"></a>What you need

Go through the [Getting Started Guide](https://docs.microsoft.com/azure/iot-hub/iot-hub-arduino-iot-devkit-az3166-get-started) and **finish the following sections only**:

* Prepare your hardware
* Configure Wi-Fi
* Start using the DevKit
* Prepare the development environment


## <a name="create-an-azure-iot-remote-monitoring-solution-accelerator"></a>Create an Azure IoT Remote Monitoring solution accelerator

The AZ3166 device you create in this tutorial sends data to an instance of the Remote Monitoring solution accelerator. If you haven't yet provisioned an instance in your Azure account, follow the [Quickstart](https://docs.microsoft.com/azure/iot-accelerators/quickstart-remote-monitoring-deploy) guide to do so.

When the deployment for the Remote Monitoring solution finishes, open the solution dashboard.

![The solution dashboard](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/azure-iot-suite-dashboard-info.png)

## <a name="add-a-device-to-the-remote-monitoring-solution"></a>Add a device to the Remote Monitoring solution

1. In the dashboard, go to **Devices** section and click the **New Device**.
   ![Adding a new device](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/azure-iot-suite-add-device.png)

2. Configure the device by using information below and click **Apply**.
  * Device Type: **Physical**
  * Device ID: **AZ3166**
  * Authentication Type: **Symmetric Key**
  * Authentication Key: **Auto generate keys**
  
  ![Adding a new device form](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/azure-iot-suite-add-new-device-form.png)

3. After the new device is created, copy the **Connection String primary key**. This is the device that is just created in Azure IoT Hub underneath.
  
  ![Device Connection String](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/azure-iot-suite-new-device-connstring.png)

## <a name="open-the-remote-monitoring-sample-in-vs-code"></a>Open the Remote Monitoring sample in VS Code

1. Make sure your IoT DevKit is **not connected** to your computer. Start VS Code first, and then connect the DevKit to your computer.

1. Click `F1` to open the command palette, type and select **IoT Workbench: Examples**. Then select **IoT DevKit** as board.

1. Find **Remote Monitoring** and click **Open Sample**. It opens a new VS Code window with project folder in it.
  ![IoT Workbench, select Remote Monitoring example](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/iot-workbench-example.png)

## <a name="configure-iot-hub-device-connection-string"></a>Configure IoT Hub device connection string

1. Switch the IoT DevKit into **Configuration mode**. To do so:
   * Hold down button **A**.
   * Push and release the **Reset** button.

2. The screen displays the DevKit ID and 'Configuration'.
   
  ![IoT DevKit Configuration Mode](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/devkit-configuration-mode.png)

3. Click `F1` to open the command palette, type and select **IoT Workbench: Device > Config Device Settings**.

4. Paste the connection string you just copied click `Enter` to configure it.

## <a name="build-and-upload-the-device-code"></a>Build and upload the device code

1. Click `F1` to open the command palette, type and select **IoT Workbench: Device > Device Upload**.
  ![IoT Workbench: Device - > Upload](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/iot-workbench-device-upload.png)

1. VS Code then starts compiling and uploading the code to your DevKit.
  ![IoT Workbench: Device - > Uploaded](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/iot-workbench-device-uploaded.png)

The DevKit reboots and starts running the code.

## <a name="test-the-project"></a>Test the project

### <a name="view-the-telemetry-sent-to-remote-monitoring-solution"></a>View the telemetry sent to Remote Monitoring solution

When the sample app runs, DevKit sends sensor data over Wi-Fi to your Remote Monitoring solution. To see the result, follow these steps:

1. Go to your solution dashboard, and click **Devices**.

1. Click on the device name (AZ3166) a tab opens on the right side of the dashboard, where you can see the sensor status on DevKit in real time.
  ![Sensor data in Azure IoT Suite](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/azure-iot-suite-dashboard.png)

### <a name="send-a-c2d-message"></a>Send a C2D message

Remote Monitoring solution allows you to invoke remote method on the device. The sxample code publishes three methods that you can see in the **Method** section when the sensor is selected.

![IoT DevKit Methods](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/azure-iot-suite-methods.png)

Let us try change the color of one of the DevKit LEDs using the method "LedColor".

1. Select the **AZ3166** from device list and click on the **Jobs**.

  ![Create a Job](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/azure-iot-suite-job.png)

2. Configure the Jobs as below and click **Apply**.
  * Select Job: **Run method**
  * Method name: **LedColor**
  * Job Name: **ChangeLedColor**
  
  ![Job settings](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/iot-suite-change-color.png)

In several seconds, your DevKit should change the color of the RGB LED (below the button A).

![IoT DevKit red led](media/iot-accelerators-arduino-iot-devkit-az3166-devkit-remote-monitoringv2/azure-iot-suite-devkit-led.png)

## <a name="clean-up-resources"></a>Clean up resources

If you plan to move on to the tutorials, leave the Remote Monitoring solution accelerator deployed.

If you no longer need the solution accelerator, delete it from the Provisioned solutions page, by selecting it, and then clicking Delete Solution:

![Delete solution](media/quickstart-remote-monitoring-deploy/deletesolution.png)

## <a name="problems-and-feedback"></a>Problems and feedback

If you encounter problems, refer to [the IoT DevKit FAQs](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) or reach out to us using the following channels:

* [Gitter.im](http://gitter.im/Microsoft/azure-iot-developer-kit)
* [Stackoverflow](https://stackoverflow.com/questions/tagged/iot-devkit)

## <a name="next-steps"></a>Next steps

Now that you have learned how to connect a DevKit device to your Azure IoT Remote Monitoring solution accelerator and visualize the sensor data, here are the suggested next steps:

* [Azure IoT solution accelerators overview](https://docs.microsoft.com/azure/iot-suite/)
* [Customize the UI](../iot-accelerators/iot-accelerators-remote-monitoring-customize.md)
* [Connect IoT DevKit to your Azure IoT Central application](../iot-central/howto-connect-devkit.md)