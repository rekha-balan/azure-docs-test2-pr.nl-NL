---
title: Connect a device using C on mbed | Microsoft Docs
description: Describes how to connect a device to the Azure IoT Suite preconfigured remote monitoring solution using an application written in C running on an mbed device.
services: ''
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 9551075e-dcf9-488f-943e-d0eb0e6260be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/18/2017
ms.author: dobett
ms.openlocfilehash: 01b7759bfa3299d13d940c457fefef067f3fc8bb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548772"
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-mbed"></a>Connect your device to the remote monitoring preconfigured solution (mbed)

[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-the-c-sample-solution"></a>Build and run the C sample solution

The following instructions describe the steps for connecting an [mbed-enabled Freescale FRDM-K64F][lnk-mbed-home] device to the remote monitoring solution.

### <a name="connect-the-mbed-device-to-your-network-and-desktop-machine"></a>Connect the mbed device to your network and desktop machine

1. Connect the mbed device to your network using an Ethernet cable. This step is necessary because the sample application requires internet access.

1. See [Getting Started with mbed][lnk-mbed-getstarted] to connect your mbed device to your desktop PC.

1. If your desktop PC is running Windows, see [PC Configuration][lnk-mbed-pcconnect] to configure serial port access to your mbed device.

### <a name="create-an-mbed-project-and-import-the-sample-code"></a>Create an mbed project and import the sample code

Follow these steps to add some sample code to an mbed project. You import the remote monitoring starter project and then change the project to use the MQTT protocol instead of the AMQP protocol. Currently, you need to use the MQTT protocol to use the device management features of IoT Hub.

1. In your web browser, go to the mbed.org [developer site](https://developer.mbed.org/). If you haven't signed up, you see an option to create an account (it's free). Otherwise, log in with your account credentials. Then click **Compiler** in the upper right-hand corner of the page. This action brings you to the *Workspace* interface.

1. Make sure the hardware platform you're using appears in the upper right-hand corner of the window, or click the icon in the right-hand corner to select your hardware platform.

1. Click **Import** on the main menu. Then click **Click here to import from URL**.
   
    ![Start import to mbed workspace][6]

1. In the pop-up window, enter the link for the sample code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ then click **Import**.
   
    ![Import sample code to mbed workspace][7]

1. You can see in the mbed compiler window that importing this project also imports various libraries. Some are provided and maintained by the Azure IoT team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), while others are third-party libraries available in the mbed libraries catalog.
   
    ![View mbed project][8]

1. In the **Program Workspace**, right-click the **iothub\_amqp\_transport** library, click **Delete**, and then click **OK** to confirm.

1. In the **Program Workspace**, right-click the **azure\_amqp\_c** library, click **Delete**, and then click **OK** to confirm.

1. Right-click the **remote_monitoring** project in the **Program Workspace**, select **Import Library**, then select **From URL**.
   
    ![Start library import to mbed workspace][6]

1. In the pop-up window, enter the link for the MQTT transport library https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ then click **Import**.
   
    ![Import library to mbed workspace][12]

1. Repeat the previous step to add the MQTT library from https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.

1. Your workspace now looks like the following:

    ![View mbed workspace][13]

1. Open the remote\_monitoring\remote_monitoring.c file and replace the existing `#include` statements with the following code:

    ```
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"

    #ifdef MBED_BUILD_TIMESTAMP
    #include "certs.h"
    #endif // MBED_BUILD_TIMESTAMP
    ```
1. Delete all the remaining code in the remote\_monitoring\remote\_monitoring.c file.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a>Build and run the sample

Add code to invoke the **remote\_monitoring\_run** function and then build and run the device application.

1. Add a **main** function with following code at the end of the remote\_monitoring.c file to invoke the **remote\_monitoring\_run** function:
   
    ```
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. Click **Compile** to build the program. You can safely ignore any warnings, but if the build generates errors, fix them before proceeding.

1. If the build is successful, the mbed compiler website generates a .bin file with the name of your project and downloads it to your local machine. Copy the .bin file to the device. Saving the .bin file to the device causes the device to restart and run the program contained in the .bin file. You can manually restart the program at any time by pressing the reset button on the mbed device.

1. Connect to the device using an SSH client application, such as PuTTY. You can determine the serial port your device uses by checking Windows Device Manager.
   
    ![][11]

1. In PuTTY, click the **Serial** connection type. The device typically connects at 9600 baud, so enter 9600 in the **Speed** box. Then click **Open**.

1. The program starts executing. You may have to reset the board (press CTRL+Break or press the board's reset button) if the program does not start automatically when you connect.
   
    ![][10]

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-connecting-devices-mbed/mbed3a.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-connecting-devices-mbed/putty.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-connecting-devices-mbed/mbed6.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-connecting-devices-mbed/mbed7.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-connecting-devices-mbed/mbed8.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration







