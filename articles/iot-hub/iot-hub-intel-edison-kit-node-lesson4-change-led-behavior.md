---
title: 'Connect Intel Edison (Node) to Azure IoT - Lesson 4: Blink the LED | Microsoft Docs'
description: Customize the messages to change the LED's on and off behavior.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timtl
tags: ''
keywords: control led with arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 387cd97e-b05e-43c4-b252-f68ad45d524a
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 102fa71338dfbd12c66f03c9c5a6006fdc8c4f1d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548903"
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="82faa-104">Change the on and off behavior of the LED</span><span class="sxs-lookup"><span data-stu-id="82faa-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="82faa-105">What you will do</span><span class="sxs-lookup"><span data-stu-id="82faa-105">What you will do</span></span>
<span data-ttu-id="82faa-106">Customize the messages to change the LED’s on and off behavior.</span><span class="sxs-lookup"><span data-stu-id="82faa-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="82faa-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="82faa-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="82faa-108">What you will learn</span><span class="sxs-lookup"><span data-stu-id="82faa-108">What you will learn</span></span>
<span data-ttu-id="82faa-109">Use additional functions to change the LED’s on and off behavior.</span><span class="sxs-lookup"><span data-stu-id="82faa-109">Use additional functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="82faa-110">What you need</span><span class="sxs-lookup"><span data-stu-id="82faa-110">What you need</span></span>
<span data-ttu-id="82faa-111">You must have successfully completed [Run a sample application on Intel Edison to receive cloud to device messages][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="82faa-111">You must have successfully completed [Run a sample application on Intel Edison to receive cloud to device messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-to-appjs-and-gulpfilejs"></a><span data-ttu-id="82faa-112">Add functions to app.js and gulpfile.js</span><span class="sxs-lookup"><span data-stu-id="82faa-112">Add functions to app.js and gulpfile.js</span></span>
1. <span data-ttu-id="82faa-113">Open the sample application in Visual Studio code by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="82faa-113">Open the sample application in Visual Studio code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="82faa-114">Open the `app.js` file, and then add the following functions after blinkLED() function:</span><span class="sxs-lookup"><span data-stu-id="82faa-114">Open the `app.js` file, and then add the following functions after blinkLED() function:</span></span>

   ```javascript
   function turnOnLED() {
     myLed.write(1);
   }

   function turnOffLED() {
     myLed.write(0);
   }
   ```

   ![app.js file with added functions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson4/updated_app_node.png)
3. <span data-ttu-id="82faa-116">Add the following conditions before the 'blink' case in the switch-case block of the `receiveMessageCallback` function:</span><span class="sxs-lookup"><span data-stu-id="82faa-116">Add the following conditions before the 'blink' case in the switch-case block of the `receiveMessageCallback` function:</span></span>

   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```

   <span data-ttu-id="82faa-117">Now you’ve configured the sample application to respond to more instructions through messages.</span><span class="sxs-lookup"><span data-stu-id="82faa-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="82faa-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span><span class="sxs-lookup"><span data-stu-id="82faa-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="82faa-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="82faa-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>

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
5. <span data-ttu-id="82faa-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span><span class="sxs-lookup"><span data-stu-id="82faa-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="82faa-122">Save all the changes.</span><span class="sxs-lookup"><span data-stu-id="82faa-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="82faa-123">Deploy and run the sample application</span><span class="sxs-lookup"><span data-stu-id="82faa-123">Deploy and run the sample application</span></span>
<span data-ttu-id="82faa-124">Deploy and run the sample application on Edison by running the following command:</span><span class="sxs-lookup"><span data-stu-id="82faa-124">Deploy and run the sample application on Edison by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="82faa-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span><span class="sxs-lookup"><span data-stu-id="82faa-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="82faa-126">The last "stop" message stops the sample application from running.</span><span class="sxs-lookup"><span data-stu-id="82faa-126">The last "stop" message stops the sample application from running.</span></span>

![on and off][on-and-off]

<span data-ttu-id="82faa-128">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="82faa-128">Congratulations!</span></span> <span data-ttu-id="82faa-129">You’ve successfully customized the messages that are sent to Edison from your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="82faa-129">You’ve successfully customized the messages that are sent to Edison from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="82faa-130">Summary</span><span class="sxs-lookup"><span data-stu-id="82faa-130">Summary</span></span>
<span data-ttu-id="82faa-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span><span class="sxs-lookup"><span data-stu-id="82faa-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md
[gulpfile]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_node.png
[on-and-off]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_node.png



