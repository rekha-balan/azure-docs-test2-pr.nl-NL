---
title: 'Connect Raspberry Pi (Node) to Azure IoT - Lesson 4: Modify app | Microsoft Docs'
description: Customize the messages to change the LED’s on and off behavior.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timlt
tags: ''
keywords: control led with raspberry pi, raspberry pi led control, raspberry pi control led
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 3b42a4ad-0197-42f6-8ca9-04c883e879e8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 00058a9655a4a441ca9a2f90aa1f0a2c35dbea65
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556711"
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a>Change the on and off behavior of the LED
## <a name="what-you-will-do"></a>What you will do
Customize the messages to change the LED’s on and off behavior. If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>What you will learn
Use additional Node.js functions to change the LED’s on and off behavior.

## <a name="what-you-need"></a>What you need
You must have successfully completed [Run a sample application on Raspberry Pi to receive cloud-to-device messages](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).

## <a name="add-nodejs-functions"></a>Add Node.js functions
1. Open the sample application in Visual Studio code by running the following commands:
   
   ```bash
   cd Lesson4
   code .
   ```
2. Open the `app.js` file, and then add the following functions at the end:
   
   ```javascript
   function turnOnLED() {
     wpi.digitalWrite(CONFIG_PIN, 1);
   }
   
   function turnOffLED() {
     wpi.digitalWrite(CONFIG_PIN, 0);
   }
   ```
   
   ![App.js file with added functions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_js.png)
3. Add the following conditions before the default one in the switch-case block of the `receiveMessageCallback` function:
   
   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
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
   
   ![Gulpfile.js file with added function](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile.png)
5. In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:
   
   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Save all the changes.

### <a name="deploy-and-run-the-sample-application"></a>Deploy and run the sample application
Deploy and run the sample application on Pi by running the following command:

```bash
gulp deploy && gulp run
```

You should see the LED turn on for two seconds, and then turn off for another two seconds. The last "stop" message stops the sample application from running.

![Sample application with on and off messages](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off.png)

Congratulations! You’ve successfully customized the messages that are sent to Pi from your IoT hub.

### <a name="summary"></a>Summary
This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.




