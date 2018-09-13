---
title: Create an IoT DevKit translator using Azure Functions and Cognitive Services | Microsoft Docs
description: Use the microphone on an IoT DevKit to receive a voice message and then use Azure Cognitive Services for processing it into translated text in English
author: liydu
manager: jeffya
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.tgt_pltfrm: arduino
ms.date: 02/28/2018
ms.author: liydu
ms.openlocfilehash: cd67e612dd020ba600e33ac8baf77bc094d8afd3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865204"
---
# <a name="use-iot-devkit-az3166-with-azure-functions-and-cognitive-services-to-make-a-language-translator"></a><span data-ttu-id="86093-103">Use IoT DevKit AZ3166 with Azure Functions and Cognitive Services to make a language translator</span><span class="sxs-lookup"><span data-stu-id="86093-103">Use IoT DevKit AZ3166 with Azure Functions and Cognitive Services to make a language translator</span></span>

<span data-ttu-id="86093-104">In this article, you learn how to make IoT DevKit as a language translator by using [Azure Cognitive Services](https://azure.microsoft.com/services/cognitive-services/).</span><span class="sxs-lookup"><span data-stu-id="86093-104">In this article, you learn how to make IoT DevKit as a language translator by using [Azure Cognitive Services](https://azure.microsoft.com/services/cognitive-services/).</span></span> <span data-ttu-id="86093-105">It records your voice and translates it to English text shown on the DevKit screen.</span><span class="sxs-lookup"><span data-stu-id="86093-105">It records your voice and translates it to English text shown on the DevKit screen.</span></span>

<span data-ttu-id="86093-106">The [MXChip IoT DevKit](https://aka.ms/iot-devkit) is an all-in-one Arduino compatible board with rich peripherals and sensors.</span><span class="sxs-lookup"><span data-stu-id="86093-106">The [MXChip IoT DevKit](https://aka.ms/iot-devkit) is an all-in-one Arduino compatible board with rich peripherals and sensors.</span></span> <span data-ttu-id="86093-107">You can develop for it using [Visual Studio Code extension for Arduino](https://aka.ms/arduino).</span><span class="sxs-lookup"><span data-stu-id="86093-107">You can develop for it using [Visual Studio Code extension for Arduino](https://aka.ms/arduino).</span></span> <span data-ttu-id="86093-108">And it comes with a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/) to guide you through prototype Internet of Things (IoT) solutions that take advantage of Microsoft Azure services.</span><span class="sxs-lookup"><span data-stu-id="86093-108">And it comes with a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/) to guide you through prototype Internet of Things (IoT) solutions that take advantage of Microsoft Azure services.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="86093-109">What you need</span><span class="sxs-lookup"><span data-stu-id="86093-109">What you need</span></span>

<span data-ttu-id="86093-110">Finish the [Getting Started Guide](https://docs.microsoft.com/azure/iot-hub/iot-hub-arduino-iot-devkit-az3166-get-started) to:</span><span class="sxs-lookup"><span data-stu-id="86093-110">Finish the [Getting Started Guide](https://docs.microsoft.com/azure/iot-hub/iot-hub-arduino-iot-devkit-az3166-get-started) to:</span></span>

* <span data-ttu-id="86093-111">Have your DevKit connected to Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="86093-111">Have your DevKit connected to Wi-Fi</span></span>
* <span data-ttu-id="86093-112">Prepare the development environment</span><span class="sxs-lookup"><span data-stu-id="86093-112">Prepare the development environment</span></span>

<span data-ttu-id="86093-113">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="86093-113">An active Azure subscription.</span></span> <span data-ttu-id="86093-114">If you do not have one, you can register via one of these two methods:</span><span class="sxs-lookup"><span data-stu-id="86093-114">If you do not have one, you can register via one of these two methods:</span></span>

* <span data-ttu-id="86093-115">Activate a [free 30-day trial Microsoft Azure account](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="86093-115">Activate a [free 30-day trial Microsoft Azure account](https://azure.microsoft.com/free/)</span></span>
* <span data-ttu-id="86093-116">Claim your [Azure credit](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) if you are MSDN or Visual Studio subscriber</span><span class="sxs-lookup"><span data-stu-id="86093-116">Claim your [Azure credit](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) if you are MSDN or Visual Studio subscriber</span></span>

## <a name="open-the-project-folder"></a><span data-ttu-id="86093-117">Open the project folder</span><span class="sxs-lookup"><span data-stu-id="86093-117">Open the project folder</span></span>

<span data-ttu-id="86093-118">First, open the project folder.</span><span class="sxs-lookup"><span data-stu-id="86093-118">First, open the project folder.</span></span> 

### <a name="start-vs-code"></a><span data-ttu-id="86093-119">Start VS Code</span><span class="sxs-lookup"><span data-stu-id="86093-119">Start VS Code</span></span>

- <span data-ttu-id="86093-120">Make sure your DevKit is connected to your PC.</span><span class="sxs-lookup"><span data-stu-id="86093-120">Make sure your DevKit is connected to your PC.</span></span>

- <span data-ttu-id="86093-121">Start VS Code.</span><span class="sxs-lookup"><span data-stu-id="86093-121">Start VS Code.</span></span>

- <span data-ttu-id="86093-122">Connect the DevKit to your computer.</span><span class="sxs-lookup"><span data-stu-id="86093-122">Connect the DevKit to your computer.</span></span>

### <a name="open-the-arduino-examples-folder"></a><span data-ttu-id="86093-123">Open the Arduino Examples folder</span><span class="sxs-lookup"><span data-stu-id="86093-123">Open the Arduino Examples folder</span></span>

<span data-ttu-id="86093-124">Expand left side **ARDUINO EXAMPLES > Examples for MXCHIP AZ3166 > AzureIoT**, and select **DevKitTranslator**.</span><span class="sxs-lookup"><span data-stu-id="86093-124">Expand left side **ARDUINO EXAMPLES > Examples for MXCHIP AZ3166 > AzureIoT**, and select **DevKitTranslator**.</span></span> <span data-ttu-id="86093-125">A new VS Code window opens, displaying the project folder.</span><span class="sxs-lookup"><span data-stu-id="86093-125">A new VS Code window opens, displaying the project folder.</span></span> <span data-ttu-id="86093-126">If you can't see the Examples for MXCHIP AZ3166 section, make sure your device is properly connected and restart VS Code.</span><span class="sxs-lookup"><span data-stu-id="86093-126">If you can't see the Examples for MXCHIP AZ3166 section, make sure your device is properly connected and restart VS Code.</span></span>  

![IoT DevKit samples](media/iot-hub-arduino-iot-devkit-az3166-translator/vscode_examples.png)

<span data-ttu-id="86093-128">You can also open the example from the command palette.</span><span class="sxs-lookup"><span data-stu-id="86093-128">You can also open the example from the command palette.</span></span> <span data-ttu-id="86093-129">Use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) to open the command palette, type **Arduino**, and then find and select **Arduino: Examples**.</span><span class="sxs-lookup"><span data-stu-id="86093-129">Use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) to open the command palette, type **Arduino**, and then find and select **Arduino: Examples**.</span></span>

## <a name="provision-azure-services"></a><span data-ttu-id="86093-130">Provision Azure services</span><span class="sxs-lookup"><span data-stu-id="86093-130">Provision Azure services</span></span>

<span data-ttu-id="86093-131">In the solution window, type `Ctrl+P` (macOS: `Cmd+P`) and enter `task cloud-provision`.</span><span class="sxs-lookup"><span data-stu-id="86093-131">In the solution window, type `Ctrl+P` (macOS: `Cmd+P`) and enter `task cloud-provision`.</span></span>

<span data-ttu-id="86093-132">In the VS Code terminal, an interactive command line will guide you to provision all necessary Azure services:</span><span class="sxs-lookup"><span data-stu-id="86093-132">In the VS Code terminal, an interactive command line will guide you to provision all necessary Azure services:</span></span>

![Cloud provision task](media/iot-hub-arduino-iot-devkit-az3166-translator/cloud-provision.png)

## <a name="deploy-the-azure-function"></a><span data-ttu-id="86093-134">Deploy the Azure Function</span><span class="sxs-lookup"><span data-stu-id="86093-134">Deploy the Azure Function</span></span>

<span data-ttu-id="86093-135">Use `Ctrl+P` (macOS: `Cmd+P`) to run `task cloud-deploy` to deploy the Azure Functions code.</span><span class="sxs-lookup"><span data-stu-id="86093-135">Use `Ctrl+P` (macOS: `Cmd+P`) to run `task cloud-deploy` to deploy the Azure Functions code.</span></span> <span data-ttu-id="86093-136">This process usually takes 2 to 5 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="86093-136">This process usually takes 2 to 5 minutes to complete.</span></span>

![Cloud deploy task](media/iot-hub-arduino-iot-devkit-az3166-translator/cloud-deploy.png)

<span data-ttu-id="86093-138">After the Azure Function deploys successfully, fill in the azure_config.h file with function app name.</span><span class="sxs-lookup"><span data-stu-id="86093-138">After the Azure Function deploys successfully, fill in the azure_config.h file with function app name.</span></span> <span data-ttu-id="86093-139">You can navigate to [Azure portal](https://portal.azure.com/) to find it:</span><span class="sxs-lookup"><span data-stu-id="86093-139">You can navigate to [Azure portal](https://portal.azure.com/) to find it:</span></span>

![Find Azure Function app name](media/iot-hub-arduino-iot-devkit-az3166-translator/azure-function.png)

> [!NOTE]
> <span data-ttu-id="86093-141">If the Azure Function does not work properly, check the ["complication error for Azure Function" page in the IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq#compilation-error-for-azure-function) to resolve it.</span><span class="sxs-lookup"><span data-stu-id="86093-141">If the Azure Function does not work properly, check the ["complication error for Azure Function" page in the IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq#compilation-error-for-azure-function) to resolve it.</span></span>

## <a name="build-and-upload-the-device-code"></a><span data-ttu-id="86093-142">Build and upload the device code</span><span class="sxs-lookup"><span data-stu-id="86093-142">Build and upload the device code</span></span>

1. <span data-ttu-id="86093-143">Use `Ctrl+P` (macOS: `Cmd+P`) to run `task config-device-connection`.</span><span class="sxs-lookup"><span data-stu-id="86093-143">Use `Ctrl+P` (macOS: `Cmd+P`) to run `task config-device-connection`.</span></span>

2. <span data-ttu-id="86093-144">The terminal will ask you whether you want to use connection string that retrieves from `task cloud-provision` step.</span><span class="sxs-lookup"><span data-stu-id="86093-144">The terminal will ask you whether you want to use connection string that retrieves from `task cloud-provision` step.</span></span> <span data-ttu-id="86093-145">You can also input your own device connection string by selecting **'Create New...'**</span><span class="sxs-lookup"><span data-stu-id="86093-145">You can also input your own device connection string by selecting **'Create New...'**</span></span>

3. <span data-ttu-id="86093-146">The terminal prompts you to enter configuration mode.</span><span class="sxs-lookup"><span data-stu-id="86093-146">The terminal prompts you to enter configuration mode.</span></span> <span data-ttu-id="86093-147">To do so, hold down button A, then push and release the reset button.</span><span class="sxs-lookup"><span data-stu-id="86093-147">To do so, hold down button A, then push and release the reset button.</span></span> <span data-ttu-id="86093-148">The screen displays the DevKit ID and 'Configuration'.</span><span class="sxs-lookup"><span data-stu-id="86093-148">The screen displays the DevKit ID and 'Configuration'.</span></span>

   ![Verification and upload of the Arduino sketch](media/iot-hub-arduino-iot-devkit-az3166-translator/config-device-connection.png)

4. <span data-ttu-id="86093-150">After `task config-device-connection` finished, click `F1` to load VS Code commands and select `Arduino: Upload`, then VS Code starts verifying and uploading the Arduino sketch.</span><span class="sxs-lookup"><span data-stu-id="86093-150">After `task config-device-connection` finished, click `F1` to load VS Code commands and select `Arduino: Upload`, then VS Code starts verifying and uploading the Arduino sketch.</span></span>

   ![Verification and upload of the Arduino sketch](media/iot-hub-arduino-iot-devkit-az3166-translator/arduino-upload.png)

<span data-ttu-id="86093-152">The DevKit reboots and starts running the code.</span><span class="sxs-lookup"><span data-stu-id="86093-152">The DevKit reboots and starts running the code.</span></span>

## <a name="test-the-project"></a><span data-ttu-id="86093-153">Test the project</span><span class="sxs-lookup"><span data-stu-id="86093-153">Test the project</span></span>

<span data-ttu-id="86093-154">After app initialization, follow the instructions on the DevKit screen.</span><span class="sxs-lookup"><span data-stu-id="86093-154">After app initialization, follow the instructions on the DevKit screen.</span></span> <span data-ttu-id="86093-155">The default source language is Chinese.</span><span class="sxs-lookup"><span data-stu-id="86093-155">The default source language is Chinese.</span></span>

<span data-ttu-id="86093-156">To select another language for translation:</span><span class="sxs-lookup"><span data-stu-id="86093-156">To select another language for translation:</span></span>

1. <span data-ttu-id="86093-157">Press button A to enter setup mode.</span><span class="sxs-lookup"><span data-stu-id="86093-157">Press button A to enter setup mode.</span></span>

2. <span data-ttu-id="86093-158">Press button B to scroll all supported source languages.</span><span class="sxs-lookup"><span data-stu-id="86093-158">Press button B to scroll all supported source languages.</span></span>

3. <span data-ttu-id="86093-159">Press button A to confirm your choice of source language.</span><span class="sxs-lookup"><span data-stu-id="86093-159">Press button A to confirm your choice of source language.</span></span>

4. <span data-ttu-id="86093-160">Press and hold button B while speaking, then release button B to initiate the translation.</span><span class="sxs-lookup"><span data-stu-id="86093-160">Press and hold button B while speaking, then release button B to initiate the translation.</span></span>

5. <span data-ttu-id="86093-161">The translated text in English shows on the screen.</span><span class="sxs-lookup"><span data-stu-id="86093-161">The translated text in English shows on the screen.</span></span>

![Scroll to select language](media/iot-hub-arduino-iot-devkit-az3166-translator/select-language.jpg)

![Translation result](media/iot-hub-arduino-iot-devkit-az3166-translator/translation-result.jpg)

<span data-ttu-id="86093-164">On the translation result screen, you can:</span><span class="sxs-lookup"><span data-stu-id="86093-164">On the translation result screen, you can:</span></span>

- <span data-ttu-id="86093-165">Press buttons A and B to scroll and select the source language.</span><span class="sxs-lookup"><span data-stu-id="86093-165">Press buttons A and B to scroll and select the source language.</span></span>

- <span data-ttu-id="86093-166">Press the B button to talk.</span><span class="sxs-lookup"><span data-stu-id="86093-166">Press the B button to talk.</span></span> <span data-ttu-id="86093-167">To send the voice and get the translation text, release the B button.</span><span class="sxs-lookup"><span data-stu-id="86093-167">To send the voice and get the translation text, release the B button.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="86093-168">How it works</span><span class="sxs-lookup"><span data-stu-id="86093-168">How it works</span></span>

![mini-solution-voice-to-tweet-diagram](media/iot-hub-arduino-iot-devkit-az3166-translator/diagram.png)

<span data-ttu-id="86093-170">The Arduino sketch records your voice then posts an HTTP request to trigger an Azure Function.</span><span class="sxs-lookup"><span data-stu-id="86093-170">The Arduino sketch records your voice then posts an HTTP request to trigger an Azure Function.</span></span> <span data-ttu-id="86093-171">The Azure Function calls the cognitive service speech translator API to do the translation.</span><span class="sxs-lookup"><span data-stu-id="86093-171">The Azure Function calls the cognitive service speech translator API to do the translation.</span></span> <span data-ttu-id="86093-172">After the Azure Function gets the translation text, it sends a C2D (cloud-to-device) message to the device.</span><span class="sxs-lookup"><span data-stu-id="86093-172">After the Azure Function gets the translation text, it sends a C2D (cloud-to-device) message to the device.</span></span> <span data-ttu-id="86093-173">Then the translation is displayed on the screen.</span><span class="sxs-lookup"><span data-stu-id="86093-173">Then the translation is displayed on the screen.</span></span>

## <a name="problems-and-feedback"></a><span data-ttu-id="86093-174">Problems and feedback</span><span class="sxs-lookup"><span data-stu-id="86093-174">Problems and feedback</span></span>

<span data-ttu-id="86093-175">If you encounter problems, refer to the [IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) or reach out to us using the following channels:</span><span class="sxs-lookup"><span data-stu-id="86093-175">If you encounter problems, refer to the [IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) or reach out to us using the following channels:</span></span>

* [<span data-ttu-id="86093-176">Gitter.im</span><span class="sxs-lookup"><span data-stu-id="86093-176">Gitter.im</span></span>](http://gitter.im/Microsoft/azure-iot-developer-kit)
* [<span data-ttu-id="86093-177">Stackoverflow</span><span class="sxs-lookup"><span data-stu-id="86093-177">Stackoverflow</span></span>](https://stackoverflow.com/questions/tagged/iot-devkit)

## <a name="next-steps"></a><span data-ttu-id="86093-178">Next Steps</span><span class="sxs-lookup"><span data-stu-id="86093-178">Next Steps</span></span>

<span data-ttu-id="86093-179">You have learned how to use the IoT DevKit as a translator by using Azure Functions and Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="86093-179">You have learned how to use the IoT DevKit as a translator by using Azure Functions and Cognitive Services.</span></span> <span data-ttu-id="86093-180">In this how-to, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="86093-180">In this how-to, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="86093-181">Use Visual Studio Code task to automate cloud provisions</span><span class="sxs-lookup"><span data-stu-id="86093-181">Use Visual Studio Code task to automate cloud provisions</span></span>
> * <span data-ttu-id="86093-182">Configure Azure IoT device connection string</span><span class="sxs-lookup"><span data-stu-id="86093-182">Configure Azure IoT device connection string</span></span>
> * <span data-ttu-id="86093-183">Deploy the Azure Function</span><span class="sxs-lookup"><span data-stu-id="86093-183">Deploy the Azure Function</span></span>
> * <span data-ttu-id="86093-184">Test the voice message translation</span><span class="sxs-lookup"><span data-stu-id="86093-184">Test the voice message translation</span></span>

<span data-ttu-id="86093-185">Advance to the other tutorials to learn:</span><span class="sxs-lookup"><span data-stu-id="86093-185">Advance to the other tutorials to learn:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="86093-186">Connect IoT DevKit AZ3166 to Azure IoT Remote Monitoring solution accelerator</span><span class="sxs-lookup"><span data-stu-id="86093-186">Connect IoT DevKit AZ3166 to Azure IoT Remote Monitoring solution accelerator</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-arduino-iot-devkit-az3166-devkit-remote-monitoring)
