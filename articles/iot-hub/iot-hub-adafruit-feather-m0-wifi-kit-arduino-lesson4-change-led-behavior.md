---
title: 'Connect Arduino (C) to Azure IoT - Lesson 4: Modify app | Microsoft Docs'
description: Customize the messages to change the LED’s on and off behavior.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: control led with arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: d7a25430-450e-43c4-a3ed-1eed995b8b7e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 048b761d3c44014231ed95aaa1acad466317ea86
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670965"
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="39a22-104">Change the on and off behavior of the LED</span><span class="sxs-lookup"><span data-stu-id="39a22-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="39a22-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="39a22-105">What you will do</span></span>
<span data-ttu-id="39a22-106">Customize the messages to change the LED’s on and off behavior.</span><span class="sxs-lookup"><span data-stu-id="39a22-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="39a22-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span><span class="sxs-lookup"><span data-stu-id="39a22-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="39a22-108">What you will learn</span><span class="sxs-lookup"><span data-stu-id="39a22-108">What you will learn</span></span>
<span data-ttu-id="39a22-109">Use additional Arduino functions to change the LED’s on and off behavior.</span><span class="sxs-lookup"><span data-stu-id="39a22-109">Use additional Arduino functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="39a22-110">What you need</span><span class="sxs-lookup"><span data-stu-id="39a22-110">What you need</span></span>
<span data-ttu-id="39a22-111">You must have successfully completed [Run a sample application on your Arduino board to receive cloud to device messages][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="39a22-111">You must have successfully completed [Run a sample application on your Arduino board to receive cloud to device messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-to-mainc-and-gulpfilejs"></a><span data-ttu-id="39a22-112">Add functions to main.c and gulpfile.js</span><span class="sxs-lookup"><span data-stu-id="39a22-112">Add functions to main.c and gulpfile.js</span></span>
1. <span data-ttu-id="39a22-113">Open the sample application in Visual Studio code by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="39a22-113">Open the sample application in Visual Studio code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="39a22-114">Open the `app.ino` file, and then add the following functions after blinkLED() function:</span><span class="sxs-lookup"><span data-stu-id="39a22-114">Open the `app.ino` file, and then add the following functions after blinkLED() function:</span></span>

   ```arduino
   static void turnOnLED()
   {
     digitalWrite(LED_PIN, HIGH);
   }

   static void turnOffLED()
   {
     digitalWrite(LED_PIN, LOW);
   }
   ```

   ![app.ino file with added functions][app-ino-file]
3. <span data-ttu-id="39a22-116">Add the following conditions before the `else if` block of the `receiveMessageCallback` function:</span><span class="sxs-lookup"><span data-stu-id="39a22-116">Add the following conditions before the `else if` block of the `receiveMessageCallback` function:</span></span>

   ```arduino
   else if (strcmp((const char*)value, "\"on\"") == 0)
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\"") == 0)
   {
       turnOffLED();
   }
   ```

   <span data-ttu-id="39a22-117">Now you’ve configured the sample application to respond to more instructions through messages.</span><span class="sxs-lookup"><span data-stu-id="39a22-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="39a22-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span><span class="sxs-lookup"><span data-stu-id="39a22-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="39a22-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="39a22-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>

   ```javascript
   var buildCustomMessage = function (messageId) {
     if ((messageId & 1) && (messageId < MAX_MESSAGE_COUNT)) {
       return new Message(JSON.stringify({ command: 'on', messageId: messageId }));
     } else if (messageId < MAX_MESSAGE_COUNT) {
       return new Message(JSON.stringify({ command: 'off', messageId: messageId }));
     } else {
       return new Message(JSON.stringify({ command: 'stop', messageId: messageId }));
     }
   };
   ```

   ![Gulpfile.js file with added function][gulp-file-js]
5. <span data-ttu-id="39a22-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span><span class="sxs-lookup"><span data-stu-id="39a22-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="39a22-122">Save all the changes.</span><span class="sxs-lookup"><span data-stu-id="39a22-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="39a22-123">Deploy and run the sample application</span><span class="sxs-lookup"><span data-stu-id="39a22-123">Deploy and run the sample application</span></span>
<span data-ttu-id="39a22-124">Deploy and run the sample application on your Arduino board by running the following command:</span><span class="sxs-lookup"><span data-stu-id="39a22-124">Deploy and run the sample application on your Arduino board by running the following command:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="39a22-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span><span class="sxs-lookup"><span data-stu-id="39a22-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="39a22-126">The last "stop" message stops the sample application from running.</span><span class="sxs-lookup"><span data-stu-id="39a22-126">The last "stop" message stops the sample application from running.</span></span>

![on and off][on-and-off]

<span data-ttu-id="39a22-128">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="39a22-128">Congratulations!</span></span> <span data-ttu-id="39a22-129">You’ve successfully customized the messages that are sent to your Arduino board from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="39a22-129">You’ve successfully customized the messages that are sent to your Arduino board from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="39a22-130">Summary</span><span class="sxs-lookup"><span data-stu-id="39a22-130">Summary</span></span>
<span data-ttu-id="39a22-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span><span class="sxs-lookup"><span data-stu-id="39a22-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png


