---
title: Retrieve a Twitter message with Azure Functions | Microsoft Docs
description: Use the motion sensor to detect shaking and use Azure Functions to find a random tweet with a hashtag that you specify
author: liydu
manager: jeffya
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.tgt_pltfrm: arduino
ms.date: 03/07/2018
ms.author: liydu
ms.openlocfilehash: 722f350c4f11648753465e302e84949fc340e281
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865444"
---
# <a name="shake-shake-for-a-tweet----retrieve-a-twitter-message-with-azure-functions"></a><span data-ttu-id="52843-103">Shake, Shake for a Tweet -- Retrieve a Twitter message with Azure Functions</span><span class="sxs-lookup"><span data-stu-id="52843-103">Shake, Shake for a Tweet -- Retrieve a Twitter message with Azure Functions</span></span>

<span data-ttu-id="52843-104">In this project, you learn how to use the motion sensor to trigger an event using Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="52843-104">In this project, you learn how to use the motion sensor to trigger an event using Azure Functions.</span></span> <span data-ttu-id="52843-105">The app retrieves a random tweet with a #hashtag you configure in your Arduino sketch.</span><span class="sxs-lookup"><span data-stu-id="52843-105">The app retrieves a random tweet with a #hashtag you configure in your Arduino sketch.</span></span> <span data-ttu-id="52843-106">The tweet displays on the DevKit screen.</span><span class="sxs-lookup"><span data-stu-id="52843-106">The tweet displays on the DevKit screen.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="52843-107">What you need</span><span class="sxs-lookup"><span data-stu-id="52843-107">What you need</span></span>

<span data-ttu-id="52843-108">Finish the [Getting Started Guide](https://docs.microsoft.com/azure/iot-hub/iot-hub-arduino-iot-devkit-az3166-get-started) to:</span><span class="sxs-lookup"><span data-stu-id="52843-108">Finish the [Getting Started Guide](https://docs.microsoft.com/azure/iot-hub/iot-hub-arduino-iot-devkit-az3166-get-started) to:</span></span>

* <span data-ttu-id="52843-109">Have your DevKit connected to Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="52843-109">Have your DevKit connected to Wi-Fi.</span></span>
* <span data-ttu-id="52843-110">Prepare the development environment.</span><span class="sxs-lookup"><span data-stu-id="52843-110">Prepare the development environment.</span></span>

<span data-ttu-id="52843-111">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="52843-111">An active Azure subscription.</span></span> <span data-ttu-id="52843-112">If you don't have one, you can register via one of these methods:</span><span class="sxs-lookup"><span data-stu-id="52843-112">If you don't have one, you can register via one of these methods:</span></span>

* <span data-ttu-id="52843-113">Activate a [free 30-day trial Microsoft Azure account](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="52843-113">Activate a [free 30-day trial Microsoft Azure account](https://azure.microsoft.com/free/)</span></span>
* <span data-ttu-id="52843-114">Claim your [Azure credit](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) if you are an MSDN or Visual Studio subscriber</span><span class="sxs-lookup"><span data-stu-id="52843-114">Claim your [Azure credit](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) if you are an MSDN or Visual Studio subscriber</span></span>

## <a name="open-the-project-folder"></a><span data-ttu-id="52843-115">Open the project folder</span><span class="sxs-lookup"><span data-stu-id="52843-115">Open the project folder</span></span>

<span data-ttu-id="52843-116">Start by opening the project folder.</span><span class="sxs-lookup"><span data-stu-id="52843-116">Start by opening the project folder.</span></span> 

### <a name="start-vs-code"></a><span data-ttu-id="52843-117">Start VS Code</span><span class="sxs-lookup"><span data-stu-id="52843-117">Start VS Code</span></span>

* <span data-ttu-id="52843-118">Make sure your DevKit is connected to your computer.</span><span class="sxs-lookup"><span data-stu-id="52843-118">Make sure your DevKit is connected to your computer.</span></span>

* <span data-ttu-id="52843-119">Start VS Code.</span><span class="sxs-lookup"><span data-stu-id="52843-119">Start VS Code.</span></span>

* <span data-ttu-id="52843-120">Connect the DevKit to your computer.</span><span class="sxs-lookup"><span data-stu-id="52843-120">Connect the DevKit to your computer.</span></span>

   > [!NOTE]
   > <span data-ttu-id="52843-121">When launching VS Code, you may receive an error message that the Arduino IDE or related board package can't be found.</span><span class="sxs-lookup"><span data-stu-id="52843-121">When launching VS Code, you may receive an error message that the Arduino IDE or related board package can't be found.</span></span> <span data-ttu-id="52843-122">If this error occurs, close VS Code and launch the Arduino IDE again.</span><span class="sxs-lookup"><span data-stu-id="52843-122">If this error occurs, close VS Code and launch the Arduino IDE again.</span></span> <span data-ttu-id="52843-123">VS Code should now locate the Arduino IDE path correctly.</span><span class="sxs-lookup"><span data-stu-id="52843-123">VS Code should now locate the Arduino IDE path correctly.</span></span>

### <a name="open-the-arduino-examples-folder"></a><span data-ttu-id="52843-124">Open the Arduino Examples folder</span><span class="sxs-lookup"><span data-stu-id="52843-124">Open the Arduino Examples folder</span></span>

<span data-ttu-id="52843-125">Expand the left side **ARDUINO EXAMPLES** section, browse to **Examples for MXCHIP AZ3166 > AzureIoT**, and select **ShakeShake**.</span><span class="sxs-lookup"><span data-stu-id="52843-125">Expand the left side **ARDUINO EXAMPLES** section, browse to **Examples for MXCHIP AZ3166 > AzureIoT**, and select **ShakeShake**.</span></span> <span data-ttu-id="52843-126">A new VS Code window opens, displaying the project folder.</span><span class="sxs-lookup"><span data-stu-id="52843-126">A new VS Code window opens, displaying the project folder.</span></span> <span data-ttu-id="52843-127">If you can't see the MXCHIP AZ3166 section, make sure your device is properly connected and restart Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="52843-127">If you can't see the MXCHIP AZ3166 section, make sure your device is properly connected and restart Visual Studio Code.</span></span>  
<span data-ttu-id="52843-128">the ![mini-solution-examples](media/iot-hub-arduino-iot-devkit-az3166-retrieve-twitter-message/vscode_examples.png)</span><span class="sxs-lookup"><span data-stu-id="52843-128">the ![mini-solution-examples](media/iot-hub-arduino-iot-devkit-az3166-retrieve-twitter-message/vscode_examples.png)</span></span>

<span data-ttu-id="52843-129">You can also open the sample project from command palette.</span><span class="sxs-lookup"><span data-stu-id="52843-129">You can also open the sample project from command palette.</span></span> <span data-ttu-id="52843-130">Click `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) to open the command palette, type **Arduino**, and then find and select **Arduino: Examples**.</span><span class="sxs-lookup"><span data-stu-id="52843-130">Click `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) to open the command palette, type **Arduino**, and then find and select **Arduino: Examples**.</span></span>

## <a name="provision-azure-services"></a><span data-ttu-id="52843-131">Provision Azure services</span><span class="sxs-lookup"><span data-stu-id="52843-131">Provision Azure services</span></span>

<span data-ttu-id="52843-132">In the solution window, run your task through `Ctrl+P` (macOS: `Cmd+P`) by entering `task cloud-provision`.</span><span class="sxs-lookup"><span data-stu-id="52843-132">In the solution window, run your task through `Ctrl+P` (macOS: `Cmd+P`) by entering `task cloud-provision`.</span></span>

<span data-ttu-id="52843-133">In the VS Code terminal, an interactive command line guides you through provisioning the required Azure services:</span><span class="sxs-lookup"><span data-stu-id="52843-133">In the VS Code terminal, an interactive command line guides you through provisioning the required Azure services:</span></span>

![cloud-provision](media/iot-hub-arduino-iot-devkit-az3166-retrieve-twitter-message/cloud-provision.png)

> [!NOTE]
> <span data-ttu-id="52843-135">If the page hangs in the loading status when trying to sign in to Azure, refer to the ["login page hangs" step in the IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/#page-hangs-when-log-in-azure).</span><span class="sxs-lookup"><span data-stu-id="52843-135">If the page hangs in the loading status when trying to sign in to Azure, refer to the ["login page hangs" step in the IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/#page-hangs-when-log-in-azure).</span></span>
 
## <a name="modify-the-hashtag"></a><span data-ttu-id="52843-136">Modify the #hashtag</span><span class="sxs-lookup"><span data-stu-id="52843-136">Modify the #hashtag</span></span>

<span data-ttu-id="52843-137">Open `ShakeShake.ino` and look for this line of code:</span><span class="sxs-lookup"><span data-stu-id="52843-137">Open `ShakeShake.ino` and look for this line of code:</span></span>

```cpp
static const char* iot_event = "{\"topic\":\"iot\"}";
```

<span data-ttu-id="52843-138">Replace the string `iot` within the curly braces with your preferred hashtag.</span><span class="sxs-lookup"><span data-stu-id="52843-138">Replace the string `iot` within the curly braces with your preferred hashtag.</span></span> <span data-ttu-id="52843-139">The DevKit later retrieves a random tweet that includes the hashtag you specify in this step.</span><span class="sxs-lookup"><span data-stu-id="52843-139">The DevKit later retrieves a random tweet that includes the hashtag you specify in this step.</span></span>

## <a name="deploy-azure-functions"></a><span data-ttu-id="52843-140">Deploy Azure Functions</span><span class="sxs-lookup"><span data-stu-id="52843-140">Deploy Azure Functions</span></span>

<span data-ttu-id="52843-141">Use `Ctrl+P` (macOS: `Cmd+P`) to run `task cloud-deploy` to start deploying the Azure Functions code:</span><span class="sxs-lookup"><span data-stu-id="52843-141">Use `Ctrl+P` (macOS: `Cmd+P`) to run `task cloud-deploy` to start deploying the Azure Functions code:</span></span>

![cloud-deploy](media/iot-hub-arduino-iot-devkit-az3166-retrieve-twitter-message/cloud-deploy.png)

> [!NOTE]
> <span data-ttu-id="52843-143">Occasionally, the Azure Function may not work properly.</span><span class="sxs-lookup"><span data-stu-id="52843-143">Occasionally, the Azure Function may not work properly.</span></span> <span data-ttu-id="52843-144">To resolve this issue when it occurs, check the ["compilation error" section of the IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/#compilation-error-for-azure-function).</span><span class="sxs-lookup"><span data-stu-id="52843-144">To resolve this issue when it occurs, check the ["compilation error" section of the IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/#compilation-error-for-azure-function).</span></span>

## <a name="build-and-upload-the-device-code"></a><span data-ttu-id="52843-145">Build and upload the device code</span><span class="sxs-lookup"><span data-stu-id="52843-145">Build and upload the device code</span></span>

<span data-ttu-id="52843-146">Next, build and upload the device code.</span><span class="sxs-lookup"><span data-stu-id="52843-146">Next, build and upload the device code.</span></span>

### <a name="windows"></a><span data-ttu-id="52843-147">Windows</span><span class="sxs-lookup"><span data-stu-id="52843-147">Windows</span></span>

1. <span data-ttu-id="52843-148">Use `Ctrl+P` to run `task device-upload`.</span><span class="sxs-lookup"><span data-stu-id="52843-148">Use `Ctrl+P` to run `task device-upload`.</span></span>

2. <span data-ttu-id="52843-149">The terminal prompts you to enter configuration mode.</span><span class="sxs-lookup"><span data-stu-id="52843-149">The terminal prompts you to enter configuration mode.</span></span> <span data-ttu-id="52843-150">To do so:</span><span class="sxs-lookup"><span data-stu-id="52843-150">To do so:</span></span>

   * <span data-ttu-id="52843-151">Hold down button A</span><span class="sxs-lookup"><span data-stu-id="52843-151">Hold down button A</span></span>

   * <span data-ttu-id="52843-152">Push and release the reset button.</span><span class="sxs-lookup"><span data-stu-id="52843-152">Push and release the reset button.</span></span>

3. <span data-ttu-id="52843-153">The screen displays the DevKit ID and 'Configuration'.</span><span class="sxs-lookup"><span data-stu-id="52843-153">The screen displays the DevKit ID and 'Configuration'.</span></span>

### <a name="macos"></a><span data-ttu-id="52843-154">macOS</span><span class="sxs-lookup"><span data-stu-id="52843-154">macOS</span></span>

1. <span data-ttu-id="52843-155">Put the DevKit into configuration mode:</span><span class="sxs-lookup"><span data-stu-id="52843-155">Put the DevKit into configuration mode:</span></span>

   <span data-ttu-id="52843-156">Hold down button A, then push and release the reset button.</span><span class="sxs-lookup"><span data-stu-id="52843-156">Hold down button A, then push and release the reset button.</span></span> <span data-ttu-id="52843-157">The screen displays 'Configuration'.</span><span class="sxs-lookup"><span data-stu-id="52843-157">The screen displays 'Configuration'.</span></span>

2. <span data-ttu-id="52843-158">Use `Cmd+P` to run `task device-upload` to set the connection string that is retrieved from the `task cloud-provision` step.</span><span class="sxs-lookup"><span data-stu-id="52843-158">Use `Cmd+P` to run `task device-upload` to set the connection string that is retrieved from the `task cloud-provision` step.</span></span>

### <a name="verify-upload-and-run"></a><span data-ttu-id="52843-159">Verify, upload, and run</span><span class="sxs-lookup"><span data-stu-id="52843-159">Verify, upload, and run</span></span>

<span data-ttu-id="52843-160">Now the connection string is set, it verifies and uploads the app, then runs it.</span><span class="sxs-lookup"><span data-stu-id="52843-160">Now the connection string is set, it verifies and uploads the app, then runs it.</span></span> 

1. <span data-ttu-id="52843-161">VS Code starts verifying and uploading the Arduino sketch to your DevKit:</span><span class="sxs-lookup"><span data-stu-id="52843-161">VS Code starts verifying and uploading the Arduino sketch to your DevKit:</span></span>

   ![device-upload](media/iot-hub-arduino-iot-devkit-az3166-retrieve-twitter-message/device-upload.png)

2. <span data-ttu-id="52843-163">The DevKit reboots and starts running the code.</span><span class="sxs-lookup"><span data-stu-id="52843-163">The DevKit reboots and starts running the code.</span></span>

<span data-ttu-id="52843-164">You may get an "Error: AZ3166: Unknown package" error message.</span><span class="sxs-lookup"><span data-stu-id="52843-164">You may get an "Error: AZ3166: Unknown package" error message.</span></span> <span data-ttu-id="52843-165">This error occurs when the board package index isn't refreshed correctly.</span><span class="sxs-lookup"><span data-stu-id="52843-165">This error occurs when the board package index isn't refreshed correctly.</span></span> <span data-ttu-id="52843-166">To resolve this issue, check the ["unknown package" error in the IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/#development).</span><span class="sxs-lookup"><span data-stu-id="52843-166">To resolve this issue, check the ["unknown package" error in the IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/#development).</span></span>

## <a name="test-the-project"></a><span data-ttu-id="52843-167">Test the project</span><span class="sxs-lookup"><span data-stu-id="52843-167">Test the project</span></span>

<span data-ttu-id="52843-168">After app initialization, click and release button A, then gently shake the DevKit board.</span><span class="sxs-lookup"><span data-stu-id="52843-168">After app initialization, click and release button A, then gently shake the DevKit board.</span></span> <span data-ttu-id="52843-169">This action retrieves a random tweet, which contains the hashtag you specified earlier.</span><span class="sxs-lookup"><span data-stu-id="52843-169">This action retrieves a random tweet, which contains the hashtag you specified earlier.</span></span> <span data-ttu-id="52843-170">Within a few seconds, a tweet displays on your DevKit screen:</span><span class="sxs-lookup"><span data-stu-id="52843-170">Within a few seconds, a tweet displays on your DevKit screen:</span></span>

### <a name="arduino-application-initializing"></a><span data-ttu-id="52843-171">Arduino application initializing...</span><span class="sxs-lookup"><span data-stu-id="52843-171">Arduino application initializing...</span></span>

![Arduino-application-initializing](media/iot-hub-arduino-iot-devkit-az3166-retrieve-twitter-message/result-1.png)

### <a name="press-a-to-shake"></a><span data-ttu-id="52843-173">Press A to shake...</span><span class="sxs-lookup"><span data-stu-id="52843-173">Press A to shake...</span></span>

![Press-A-to-shake](media/iot-hub-arduino-iot-devkit-az3166-retrieve-twitter-message/result-2.png)

### <a name="ready-to-shake"></a><span data-ttu-id="52843-175">Ready to shake...</span><span class="sxs-lookup"><span data-stu-id="52843-175">Ready to shake...</span></span>

![Ready-to-shake](media/iot-hub-arduino-iot-devkit-az3166-retrieve-twitter-message/result-3.png)

### <a name="processing"></a><span data-ttu-id="52843-177">Processing...</span><span class="sxs-lookup"><span data-stu-id="52843-177">Processing...</span></span>

![Processing](media/iot-hub-arduino-iot-devkit-az3166-retrieve-twitter-message/result-4.png)

### <a name="press-b-to-read"></a><span data-ttu-id="52843-179">Press B to read...</span><span class="sxs-lookup"><span data-stu-id="52843-179">Press B to read...</span></span>

![Press-B-to-read](media/iot-hub-arduino-iot-devkit-az3166-retrieve-twitter-message/result-5.png)

### <a name="display-a-random-tweet"></a><span data-ttu-id="52843-181">Display a random tweet...</span><span class="sxs-lookup"><span data-stu-id="52843-181">Display a random tweet...</span></span>

![Display-a-random-tweet](media/iot-hub-arduino-iot-devkit-az3166-retrieve-twitter-message/result-6.png)

- <span data-ttu-id="52843-183">Press button A again, then shake for a new tweet.</span><span class="sxs-lookup"><span data-stu-id="52843-183">Press button A again, then shake for a new tweet.</span></span>
- <span data-ttu-id="52843-184">Press button B to scroll through the rest of the tweet.</span><span class="sxs-lookup"><span data-stu-id="52843-184">Press button B to scroll through the rest of the tweet.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="52843-185">How it works</span><span class="sxs-lookup"><span data-stu-id="52843-185">How it works</span></span>

![diagram](media/iot-hub-arduino-iot-devkit-az3166-retrieve-twitter-message/diagram.png)

<span data-ttu-id="52843-187">The Arduino sketch sends an event to the Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="52843-187">The Arduino sketch sends an event to the Azure IoT Hub.</span></span> <span data-ttu-id="52843-188">This event triggers the Azure Functions app.</span><span class="sxs-lookup"><span data-stu-id="52843-188">This event triggers the Azure Functions app.</span></span> <span data-ttu-id="52843-189">The Azure Functions app contains the logic to connect to Twitter's API and retrieve a tweet.</span><span class="sxs-lookup"><span data-stu-id="52843-189">The Azure Functions app contains the logic to connect to Twitter's API and retrieve a tweet.</span></span> <span data-ttu-id="52843-190">It then wraps the tweet text into a C2D (Cloud-to-device) message and sends it back to the device.</span><span class="sxs-lookup"><span data-stu-id="52843-190">It then wraps the tweet text into a C2D (Cloud-to-device) message and sends it back to the device.</span></span>

## <a name="optional-use-your-own-twitter-bearer-token"></a><span data-ttu-id="52843-191">Optional: Use your own Twitter bearer token</span><span class="sxs-lookup"><span data-stu-id="52843-191">Optional: Use your own Twitter bearer token</span></span>

<span data-ttu-id="52843-192">For testing purposes, this sample project uses a pre-configured Twitter bearer token.</span><span class="sxs-lookup"><span data-stu-id="52843-192">For testing purposes, this sample project uses a pre-configured Twitter bearer token.</span></span> <span data-ttu-id="52843-193">However, there is a [rate limit](https://dev.twitter.com/rest/reference/get/search/tweets) for every Twitter account.</span><span class="sxs-lookup"><span data-stu-id="52843-193">However, there is a [rate limit](https://dev.twitter.com/rest/reference/get/search/tweets) for every Twitter account.</span></span> <span data-ttu-id="52843-194">If you want to consider using your own token, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="52843-194">If you want to consider using your own token, follow these steps:</span></span>

1. <span data-ttu-id="52843-195">Go to [Twitter Developer portal](https://dev.twitter.com/) to register a new Twitter app.</span><span class="sxs-lookup"><span data-stu-id="52843-195">Go to [Twitter Developer portal](https://dev.twitter.com/) to register a new Twitter app.</span></span>

2. <span data-ttu-id="52843-196">[Get Consumer Key and Consumer Secrets](https://support.yapsody.com/hc/en-us/articles/360003291573-How-do-I-get-a-Twitter-Consumer-Key-and-Consumer-Secret-key-) of your app.</span><span class="sxs-lookup"><span data-stu-id="52843-196">[Get Consumer Key and Consumer Secrets](https://support.yapsody.com/hc/en-us/articles/360003291573-How-do-I-get-a-Twitter-Consumer-Key-and-Consumer-Secret-key-) of your app.</span></span>

3. <span data-ttu-id="52843-197">Use [some utility](https://gearside.com/nebula/utilities/twitter-bearer-token-generator/) to generate a Twitter bearer token from these two keys.</span><span class="sxs-lookup"><span data-stu-id="52843-197">Use [some utility](https://gearside.com/nebula/utilities/twitter-bearer-token-generator/) to generate a Twitter bearer token from these two keys.</span></span>

4. <span data-ttu-id="52843-198">In the [Azure portal](https://portal.azure.com/){:target="_blank"}, get into the **Resource Group** and find the Azure Function (Type: App Service) for your "Shake, Shake" project.</span><span class="sxs-lookup"><span data-stu-id="52843-198">In the [Azure portal](https://portal.azure.com/){:target="_blank"}, get into the **Resource Group** and find the Azure Function (Type: App Service) for your "Shake, Shake" project.</span></span> <span data-ttu-id="52843-199">The name always contains 'shake...' string.</span><span class="sxs-lookup"><span data-stu-id="52843-199">The name always contains 'shake...' string.</span></span>

   ![azure-function](media/iot-hub-arduino-iot-devkit-az3166-retrieve-twitter-message/azure-function.png)

5. <span data-ttu-id="52843-201">Update the code for `run.csx` within **Functions > shakeshake-cs** with your own token:</span><span class="sxs-lookup"><span data-stu-id="52843-201">Update the code for `run.csx` within **Functions > shakeshake-cs** with your own token:</span></span>

   ```csharp
   string authHeader = "Bearer " + "[your own token]";
  ```
  
  ![twitter-token](media/iot-hub-arduino-iot-devkit-az3166-retrieve-twitter-message/twitter-token.png)

6. <span data-ttu-id="52843-203">Save the file and click **Run**.</span><span class="sxs-lookup"><span data-stu-id="52843-203">Save the file and click **Run**.</span></span>

## <a name="problems-and-feedback"></a><span data-ttu-id="52843-204">Problems and feedback</span><span class="sxs-lookup"><span data-stu-id="52843-204">Problems and feedback</span></span>

<span data-ttu-id="52843-205">How to troubleshoot problems or provide feedback.</span><span class="sxs-lookup"><span data-stu-id="52843-205">How to troubleshoot problems or provide feedback.</span></span> 

### <a name="problems"></a><span data-ttu-id="52843-206">Problems</span><span class="sxs-lookup"><span data-stu-id="52843-206">Problems</span></span>

<span data-ttu-id="52843-207">One problem you could see if the screen displays 'No Tweets' while every step has run successfully.</span><span class="sxs-lookup"><span data-stu-id="52843-207">One problem you could see if the screen displays 'No Tweets' while every step has run successfully.</span></span> <span data-ttu-id="52843-208">This condition normally happens the first time you deploy and run the sample because the function app requires anywhere from a couple of seconds to as much as one minute to cold start the app.</span><span class="sxs-lookup"><span data-stu-id="52843-208">This condition normally happens the first time you deploy and run the sample because the function app requires anywhere from a couple of seconds to as much as one minute to cold start the app.</span></span> 

<span data-ttu-id="52843-209">Or, when running the code, there are some blips that cause a restarting of the app.</span><span class="sxs-lookup"><span data-stu-id="52843-209">Or, when running the code, there are some blips that cause a restarting of the app.</span></span> <span data-ttu-id="52843-210">When this condition happens, the device app can get a timeout for fetching the tweet.</span><span class="sxs-lookup"><span data-stu-id="52843-210">When this condition happens, the device app can get a timeout for fetching the tweet.</span></span> <span data-ttu-id="52843-211">In this case, you may try one or both of these methods to solve the issue:</span><span class="sxs-lookup"><span data-stu-id="52843-211">In this case, you may try one or both of these methods to solve the issue:</span></span>

1. <span data-ttu-id="52843-212">Click the reset button on the DevKit to run the device app again.</span><span class="sxs-lookup"><span data-stu-id="52843-212">Click the reset button on the DevKit to run the device app again.</span></span>

2. <span data-ttu-id="52843-213">In the [Azure portal](https://portal.azure.com/), find the Azure Functions app you created and restart it:</span><span class="sxs-lookup"><span data-stu-id="52843-213">In the [Azure portal](https://portal.azure.com/), find the Azure Functions app you created and restart it:</span></span>

   ![azure-function-restart](media/iot-hub-arduino-iot-devkit-az3166-retrieve-twitter-message/azure-function-restart.png)

### <a name="feedback"></a><span data-ttu-id="52843-215">Feedback</span><span class="sxs-lookup"><span data-stu-id="52843-215">Feedback</span></span>

<span data-ttu-id="52843-216">If you experience other problems, refer to the [IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) or contact us using the following channels:</span><span class="sxs-lookup"><span data-stu-id="52843-216">If you experience other problems, refer to the [IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) or contact us using the following channels:</span></span>

* [<span data-ttu-id="52843-217">Gitter.im</span><span class="sxs-lookup"><span data-stu-id="52843-217">Gitter.im</span></span>](http://gitter.im/Microsoft/azure-iot-developer-kit)
* [<span data-ttu-id="52843-218">Stackoverflow</span><span class="sxs-lookup"><span data-stu-id="52843-218">Stackoverflow</span></span>](https://stackoverflow.com/questions/tagged/iot-devkit)

## <a name="next-steps"></a><span data-ttu-id="52843-219">Next steps</span><span class="sxs-lookup"><span data-stu-id="52843-219">Next steps</span></span>

<span data-ttu-id="52843-220">Now that you have learned how to connect a DevKit device to your Azure IoT Remote Monitoring solution accelerator and retrieve a tweet, here are the suggested next steps:</span><span class="sxs-lookup"><span data-stu-id="52843-220">Now that you have learned how to connect a DevKit device to your Azure IoT Remote Monitoring solution accelerator and retrieve a tweet, here are the suggested next steps:</span></span>

* [<span data-ttu-id="52843-221">Azure IoT Remote Monitoring solution accelerator overview</span><span class="sxs-lookup"><span data-stu-id="52843-221">Azure IoT Remote Monitoring solution accelerator overview</span></span>](https://docs.microsoft.com/azure/iot-suite/)