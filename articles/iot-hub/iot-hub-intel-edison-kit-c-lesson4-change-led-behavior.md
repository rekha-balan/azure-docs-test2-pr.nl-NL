---
title: 'Connect Intel Edison (C) to Azure IoT - Lesson 4: Blink the LED | Microsoft Docs'
description: Customize the messages to change the LED's on and off behavior.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: control led with arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 9826c55a-0e24-4296-ae54-29b7fe66436a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9b7b00e7dac887071cb8b04e6ff66fd7e7dedad8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661038"
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a>Change the on and off behavior of the LED
## <a name="what-you-will-do"></a>What you will do
Customize the messages to change the LED’s on and off behavior. If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].

## <a name="what-you-will-learn"></a>What you will learn
Use additional functions to change the LED’s on and off behavior.

## <a name="what-you-need"></a>What you need
You must have successfully completed [Run a sample application on Intel Edison to receive cloud to device messages][receive-cloud-to-device-messages].

## <a name="add-functions-to-mainc-and-gulpfilejs"></a>Add functions to main.c and gulpfile.js
1. Open the sample application in Visual Studio code by running the following commands:

   ```bash
   cd Lesson4
   code .
   ```
2. Open the `main.c` file, and then add the following functions after blinkLED() function:

   ```c
   static void turnOnLED()
   {
     mraa_gpio_write(context, 1);
   }

   static void turnOffLED()
   {
     mraa_gpio_write(context, 0);
   }
   ```

   ![main.c file with added functions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson4/updated_app_c.png)

3. Add the following conditions before the `else if` block of the `receiveMessageCallback` function:

   ```c
   else if (0 == strcmp((const char*)value, "\"on\""))
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\""))
   {
       turnOffLED();
   }
   ```

   Now you’ve configured the sample application to respond to more instructions through messages. The "on" instruction turns on the LED, and the "off" instruction turns off the LED.
4. Open the gulpfile.js file, and then add a new function before the function `sendMessage`:

   ```javascript
   var buildCustomMessage = function (messageId) {
     if ((messageId & 1) && (messageId < MAX_MESSAGE_COUNT)) {
       return new Message(JSON.stringify({ command: 'on', messageId: messageId }));
     } else if (messageId < MAX_MESSAGE_COUNT) {
       return new Message(JSON.stringify({ command: 'off', messageId: messageId }));
     } else {
       return new Message(JSON.stringify({ command: 'stop', messageId: messageId }));
     }
   }
   ```

   ![Gulpfile.js file with added function][gulpfile]
5. In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Save all the changes.

### <a name="deploy-and-run-the-sample-application"></a>Deploy and run the sample application
Deploy and run the sample application on Edison by running the following command:

```bash
gulp deploy && gulp run
```

You should see the LED turn on for two seconds, and then turn off for another two seconds. The last "stop" message stops the sample application from running.

![on and off][on-and-off]

Congratulations! You’ve successfully customized the messages that are sent to Edison from your IoT hub.

### <a name="summary"></a>Summary
This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md
[gulpfile]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_c.png
[on-and-off]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_c.png



