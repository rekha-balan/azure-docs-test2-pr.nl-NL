---
title: Receive an email when door is opened using SendGrid service and Azure Functions | Microsoft Docs
description: Monitor the magnetic sensor to detect when a door is opened and use Azure Functions to send an email notification.
author: liydu
manager: jeffya
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.tgt_pltfrm: arduino
ms.date: 03/19/2018
ms.author: liydu
ms.openlocfilehash: 501dc942fc41a4e06aa13fba2eb670f8bc0f8a21
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871640"
---
# <a name="door-monitor"></a><span data-ttu-id="53632-103">Door Monitor</span><span class="sxs-lookup"><span data-stu-id="53632-103">Door Monitor</span></span>          

<span data-ttu-id="53632-104">The MXChip IoT DevKit contains a built-in magnetic sensor.</span><span class="sxs-lookup"><span data-stu-id="53632-104">The MXChip IoT DevKit contains a built-in magnetic sensor.</span></span> <span data-ttu-id="53632-105">In this project, you detect the presence or absence of a nearby strong magnetic field -- in this case, coming from a small, permanent magnet.</span><span class="sxs-lookup"><span data-stu-id="53632-105">In this project, you detect the presence or absence of a nearby strong magnetic field -- in this case, coming from a small, permanent magnet.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="53632-106">What you learn</span><span class="sxs-lookup"><span data-stu-id="53632-106">What you learn</span></span>

<span data-ttu-id="53632-107">In this project, you learn:</span><span class="sxs-lookup"><span data-stu-id="53632-107">In this project, you learn:</span></span>
- <span data-ttu-id="53632-108">How to use the MXChip IoT DevKit's magnetic sensor to detect the movement of a nearby magnet.</span><span class="sxs-lookup"><span data-stu-id="53632-108">How to use the MXChip IoT DevKit's magnetic sensor to detect the movement of a nearby magnet.</span></span>
- <span data-ttu-id="53632-109">How to use the SendGrid service to send a notification to your email address.</span><span class="sxs-lookup"><span data-stu-id="53632-109">How to use the SendGrid service to send a notification to your email address.</span></span>

> [!NOTE]
> <span data-ttu-id="53632-110">For a practical use of this project, perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="53632-110">For a practical use of this project, perform the following tasks:</span></span>
> - <span data-ttu-id="53632-111">Mount a magnet to the edge of a door.</span><span class="sxs-lookup"><span data-stu-id="53632-111">Mount a magnet to the edge of a door.</span></span>
> - <span data-ttu-id="53632-112">Mount the DevKit on the door jamb close to the magnet.</span><span class="sxs-lookup"><span data-stu-id="53632-112">Mount the DevKit on the door jamb close to the magnet.</span></span> <span data-ttu-id="53632-113">Opening or closing the door will trigger the sensor, resulting in your receiving an email notification of the event.</span><span class="sxs-lookup"><span data-stu-id="53632-113">Opening or closing the door will trigger the sensor, resulting in your receiving an email notification of the event.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="53632-114">What you need</span><span class="sxs-lookup"><span data-stu-id="53632-114">What you need</span></span>

<span data-ttu-id="53632-115">Finish the [Getting Started Guide](iot-hub-arduino-iot-devkit-az3166-get-started.md) to:</span><span class="sxs-lookup"><span data-stu-id="53632-115">Finish the [Getting Started Guide](iot-hub-arduino-iot-devkit-az3166-get-started.md) to:</span></span>

* <span data-ttu-id="53632-116">Have your DevKit connected to Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="53632-116">Have your DevKit connected to Wi-Fi</span></span>
* <span data-ttu-id="53632-117">Prepare the development environment</span><span class="sxs-lookup"><span data-stu-id="53632-117">Prepare the development environment</span></span>

<span data-ttu-id="53632-118">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="53632-118">An active Azure subscription.</span></span> <span data-ttu-id="53632-119">If you do not have one, you can register via one of these methods:</span><span class="sxs-lookup"><span data-stu-id="53632-119">If you do not have one, you can register via one of these methods:</span></span>

* <span data-ttu-id="53632-120">Activate a [free 30-day trial Microsoft Azure account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="53632-120">Activate a [free 30-day trial Microsoft Azure account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="53632-121">Claim your [Azure credit](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) if you are an MSDN or Visual Studio subscriber.</span><span class="sxs-lookup"><span data-stu-id="53632-121">Claim your [Azure credit](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) if you are an MSDN or Visual Studio subscriber.</span></span>

## <a name="deploy-the-sendgrid-service-in-azure"></a><span data-ttu-id="53632-122">Deploy the SendGrid service in Azure</span><span class="sxs-lookup"><span data-stu-id="53632-122">Deploy the SendGrid service in Azure</span></span>

<span data-ttu-id="53632-123">[SendGrid](https://sendgrid.com/) is a cloud-based email delivery platform.</span><span class="sxs-lookup"><span data-stu-id="53632-123">[SendGrid](https://sendgrid.com/) is a cloud-based email delivery platform.</span></span> <span data-ttu-id="53632-124">This service will be used to send email notifications.</span><span class="sxs-lookup"><span data-stu-id="53632-124">This service will be used to send email notifications.</span></span>

> [!NOTE]
> <span data-ttu-id="53632-125">If you have already deployed a SendGrid service, you may proceed directly to [Deploy IoT Hub in Azure](#deploy-iot-hub-in-azure).</span><span class="sxs-lookup"><span data-stu-id="53632-125">If you have already deployed a SendGrid service, you may proceed directly to [Deploy IoT Hub in Azure](#deploy-iot-hub-in-azure).</span></span>

### <a name="sendgrid-deployment"></a><span data-ttu-id="53632-126">SendGrid Deployment</span><span class="sxs-lookup"><span data-stu-id="53632-126">SendGrid Deployment</span></span>

<span data-ttu-id="53632-127">To provision Azure services, use the **Deploy to Azure** button.</span><span class="sxs-lookup"><span data-stu-id="53632-127">To provision Azure services, use the **Deploy to Azure** button.</span></span> <span data-ttu-id="53632-128">This button enables quick and easy deployment of your open-source projects to Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="53632-128">This button enables quick and easy deployment of your open-source projects to Microsoft Azure.</span></span>

<span data-ttu-id="53632-129">Click the **Deploy to Azure** button below.</span><span class="sxs-lookup"><span data-stu-id="53632-129">Click the **Deploy to Azure** button below.</span></span> 

<span data-ttu-id="53632-130">[![Deploy to Azure](https://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FVSChina%2Fdevkit-door-monitor%2Fmaster%2FSendGridDeploy%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="53632-130">[![Deploy to Azure](https://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FVSChina%2Fdevkit-door-monitor%2Fmaster%2FSendGridDeploy%2Fazuredeploy.json)</span></span>

<span data-ttu-id="53632-131">If you are not already signed into your Azure account, sign in now.</span><span class="sxs-lookup"><span data-stu-id="53632-131">If you are not already signed into your Azure account, sign in now.</span></span> 

<span data-ttu-id="53632-132">You now see the SendGrid sign-up form.</span><span class="sxs-lookup"><span data-stu-id="53632-132">You now see the SendGrid sign-up form.</span></span>

![SendGrid Deployment](media/iot-hub-arduino-iot-devkit-az3166-door-monitor/sendgrid-deploy.png)

<span data-ttu-id="53632-134">Complete the sign-up form:</span><span class="sxs-lookup"><span data-stu-id="53632-134">Complete the sign-up form:</span></span>

   * <span data-ttu-id="53632-135">**Resource group**: Create a resource group to host the SendGrid service, or use an existing one.</span><span class="sxs-lookup"><span data-stu-id="53632-135">**Resource group**: Create a resource group to host the SendGrid service, or use an existing one.</span></span> <span data-ttu-id="53632-136">See [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="53632-136">See [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span></span>

   * <span data-ttu-id="53632-137">**Name**: The name for your SendGrid service.</span><span class="sxs-lookup"><span data-stu-id="53632-137">**Name**: The name for your SendGrid service.</span></span> <span data-ttu-id="53632-138">Choose a unique name, differing from other services you may have.</span><span class="sxs-lookup"><span data-stu-id="53632-138">Choose a unique name, differing from other services you may have.</span></span>

   * <span data-ttu-id="53632-139">**Password**: The service requires a password, which will not be used for anything in this project.</span><span class="sxs-lookup"><span data-stu-id="53632-139">**Password**: The service requires a password, which will not be used for anything in this project.</span></span>

   * <span data-ttu-id="53632-140">**Email**: The SendGrid service will send verification to this email address.</span><span class="sxs-lookup"><span data-stu-id="53632-140">**Email**: The SendGrid service will send verification to this email address.</span></span>

<span data-ttu-id="53632-141">Check the **Pin to dashboard** option to make this application easier to find in the future, then click **Purchase** to submit the sign-in form.</span><span class="sxs-lookup"><span data-stu-id="53632-141">Check the **Pin to dashboard** option to make this application easier to find in the future, then click **Purchase** to submit the sign-in form.</span></span>
 
### <a name="sendgrid-api-key-creation"></a><span data-ttu-id="53632-142">SendGrid API Key creation</span><span class="sxs-lookup"><span data-stu-id="53632-142">SendGrid API Key creation</span></span>

<span data-ttu-id="53632-143">After the deployment completes, click it and then click the **Manage** button.</span><span class="sxs-lookup"><span data-stu-id="53632-143">After the deployment completes, click it and then click the **Manage** button.</span></span> <span data-ttu-id="53632-144">Your SendGrid account page appears, where you need to verify your email address.</span><span class="sxs-lookup"><span data-stu-id="53632-144">Your SendGrid account page appears, where you need to verify your email address.</span></span>

![SendGrid Manage](media/iot-hub-arduino-iot-devkit-az3166-door-monitor/sendgrid-manage.png)

<span data-ttu-id="53632-146">On the SendGrid page, click **Settings** > **API Keys** > **Create API Key**.</span><span class="sxs-lookup"><span data-stu-id="53632-146">On the SendGrid page, click **Settings** > **API Keys** > **Create API Key**.</span></span>

![SendGrid Create API First](media/iot-hub-arduino-iot-devkit-az3166-door-monitor/sendgrid-create-api-first.png)

<span data-ttu-id="53632-148">On the **Create API Key** page, input the **API Key Name** and click **Create & View**.</span><span class="sxs-lookup"><span data-stu-id="53632-148">On the **Create API Key** page, input the **API Key Name** and click **Create & View**.</span></span>

![SendGrid Create API Second](media/iot-hub-arduino-iot-devkit-az3166-door-monitor/sendgrid-create-api-second.png)

<span data-ttu-id="53632-150">Your API key is displayed only one time.</span><span class="sxs-lookup"><span data-stu-id="53632-150">Your API key is displayed only one time.</span></span> <span data-ttu-id="53632-151">Be sure to copy and store it safely, as it is used in the next step.</span><span class="sxs-lookup"><span data-stu-id="53632-151">Be sure to copy and store it safely, as it is used in the next step.</span></span>

## <a name="deploy-iot-hub-in-azure"></a><span data-ttu-id="53632-152">Deploy IoT Hub in Azure</span><span class="sxs-lookup"><span data-stu-id="53632-152">Deploy IoT Hub in Azure</span></span>

<span data-ttu-id="53632-153">The following steps will provision other Azure IoT related services and deploy Azure Functions for this project.</span><span class="sxs-lookup"><span data-stu-id="53632-153">The following steps will provision other Azure IoT related services and deploy Azure Functions for this project.</span></span>

<span data-ttu-id="53632-154">Click the **Deploy to Azure** button below.</span><span class="sxs-lookup"><span data-stu-id="53632-154">Click the **Deploy to Azure** button below.</span></span> 

<span data-ttu-id="53632-155">[![Deploy to Azure](https://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FVSChina%2Fdevkit-door-monitor%2Fmaster%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="53632-155">[![Deploy to Azure](https://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FVSChina%2Fdevkit-door-monitor%2Fmaster%2Fazuredeploy.json)</span></span>

<span data-ttu-id="53632-156">The sign-up form appears.</span><span class="sxs-lookup"><span data-stu-id="53632-156">The sign-up form appears.</span></span>

![IoTHub Deployment](media/iot-hub-arduino-iot-devkit-az3166-door-monitor/iot-hub-deploy.png)

<span data-ttu-id="53632-158">Fill in the fields on the sign-up form.</span><span class="sxs-lookup"><span data-stu-id="53632-158">Fill in the fields on the sign-up form.</span></span>

   * <span data-ttu-id="53632-159">**Resource group**: Create a resource group to host the SendGrid service, or use an existing one.</span><span class="sxs-lookup"><span data-stu-id="53632-159">**Resource group**: Create a resource group to host the SendGrid service, or use an existing one.</span></span> <span data-ttu-id="53632-160">See [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="53632-160">See [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span></span>

   * <span data-ttu-id="53632-161">**Iot Hub Name**: The name for your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="53632-161">**Iot Hub Name**: The name for your IoT hub.</span></span> <span data-ttu-id="53632-162">Choose a unique name, differing from other services you may have.</span><span class="sxs-lookup"><span data-stu-id="53632-162">Choose a unique name, differing from other services you may have.</span></span>

   * <span data-ttu-id="53632-163">**Iot Hub Sku**: F1 (limited to one per subscription) is free.</span><span class="sxs-lookup"><span data-stu-id="53632-163">**Iot Hub Sku**: F1 (limited to one per subscription) is free.</span></span> <span data-ttu-id="53632-164">You can see more pricing information on the [pricing page](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="53632-164">You can see more pricing information on the [pricing page](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

   * <span data-ttu-id="53632-165">**From Email**: This field should be the same email address you used when setting up the SendGrid service.</span><span class="sxs-lookup"><span data-stu-id="53632-165">**From Email**: This field should be the same email address you used when setting up the SendGrid service.</span></span>

<span data-ttu-id="53632-166">Check the **Pin to dashboard** option to make this application easier to find in the future, then click **Purchase** when you're ready to continue to the next step.</span><span class="sxs-lookup"><span data-stu-id="53632-166">Check the **Pin to dashboard** option to make this application easier to find in the future, then click **Purchase** when you're ready to continue to the next step.</span></span>
 
## <a name="build-and-upload-the-code"></a><span data-ttu-id="53632-167">Build and upload the code</span><span class="sxs-lookup"><span data-stu-id="53632-167">Build and upload the code</span></span>

<span data-ttu-id="53632-168">Next, load the sample code in VS Code and provision the necessary Azure services.</span><span class="sxs-lookup"><span data-stu-id="53632-168">Next, load the sample code in VS Code and provision the necessary Azure services.</span></span>

### <a name="start-vs-code"></a><span data-ttu-id="53632-169">Start VS Code</span><span class="sxs-lookup"><span data-stu-id="53632-169">Start VS Code</span></span>

- <span data-ttu-id="53632-170">Make sure your DevKit is **not** connected to your computer.</span><span class="sxs-lookup"><span data-stu-id="53632-170">Make sure your DevKit is **not** connected to your computer.</span></span>
- <span data-ttu-id="53632-171">Start VS Code.</span><span class="sxs-lookup"><span data-stu-id="53632-171">Start VS Code.</span></span>
- <span data-ttu-id="53632-172">Connect the DevKit to your computer.</span><span class="sxs-lookup"><span data-stu-id="53632-172">Connect the DevKit to your computer.</span></span>

> [!NOTE]
> <span data-ttu-id="53632-173">When you launch VS Code, you may receive an error message stating that it cannot find the Arduino IDE or related board package.</span><span class="sxs-lookup"><span data-stu-id="53632-173">When you launch VS Code, you may receive an error message stating that it cannot find the Arduino IDE or related board package.</span></span> <span data-ttu-id="53632-174">If you receive this error, close VS Code, launch the Arduino IDE again, and VS Code should locate the Arduino IDE path correctly.</span><span class="sxs-lookup"><span data-stu-id="53632-174">If you receive this error, close VS Code, launch the Arduino IDE again, and VS Code should locate the Arduino IDE path correctly.</span></span>

### <a name="open-arduino-examples-folder"></a><span data-ttu-id="53632-175">Open Arduino Examples folder</span><span class="sxs-lookup"><span data-stu-id="53632-175">Open Arduino Examples folder</span></span>

<span data-ttu-id="53632-176">Expand the left side **ARDUINO EXAMPLES** section, browse to **Examples for MXCHIP AZ3166 > AzureIoT**, and select **DoorMonitor**.</span><span class="sxs-lookup"><span data-stu-id="53632-176">Expand the left side **ARDUINO EXAMPLES** section, browse to **Examples for MXCHIP AZ3166 > AzureIoT**, and select **DoorMonitor**.</span></span> <span data-ttu-id="53632-177">This action opens a new VS Code window with a project folder in it.</span><span class="sxs-lookup"><span data-stu-id="53632-177">This action opens a new VS Code window with a project folder in it.</span></span>

![mini-solution-examples](media/iot-hub-arduino-iot-devkit-az3166-door-monitor/vscode-examples.png)

<span data-ttu-id="53632-179">You can also open the example app from the command palette.</span><span class="sxs-lookup"><span data-stu-id="53632-179">You can also open the example app from the command palette.</span></span> <span data-ttu-id="53632-180">Use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) to open the command palette, type **Arduino**, and then find and select **Arduino: Examples**.</span><span class="sxs-lookup"><span data-stu-id="53632-180">Use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) to open the command palette, type **Arduino**, and then find and select **Arduino: Examples**.</span></span>

### <a name="provision-azure-services"></a><span data-ttu-id="53632-181">Provision Azure services</span><span class="sxs-lookup"><span data-stu-id="53632-181">Provision Azure services</span></span>

<span data-ttu-id="53632-182">In the solution window, run the cloud provisioning task:</span><span class="sxs-lookup"><span data-stu-id="53632-182">In the solution window, run the cloud provisioning task:</span></span>
- <span data-ttu-id="53632-183">Type `Ctrl+P` (macOS: `Cmd+P`).</span><span class="sxs-lookup"><span data-stu-id="53632-183">Type `Ctrl+P` (macOS: `Cmd+P`).</span></span>
- <span data-ttu-id="53632-184">Enter `task cloud-provision` in the provided text box.</span><span class="sxs-lookup"><span data-stu-id="53632-184">Enter `task cloud-provision` in the provided text box.</span></span>

<span data-ttu-id="53632-185">In the VS Code terminal, an interactive command line guides you through provisioning the required Azure services.</span><span class="sxs-lookup"><span data-stu-id="53632-185">In the VS Code terminal, an interactive command line guides you through provisioning the required Azure services.</span></span> <span data-ttu-id="53632-186">Select all of the same items from the prompted list that you previously provisioned in [Deploy IoT Hub in Azure](#deploy-iot-hub-in-azure).</span><span class="sxs-lookup"><span data-stu-id="53632-186">Select all of the same items from the prompted list that you previously provisioned in [Deploy IoT Hub in Azure](#deploy-iot-hub-in-azure).</span></span>

![Cloud Provision](media/iot-hub-arduino-iot-devkit-az3166-door-monitor/cloud-provision.png)

> [!NOTE]
> <span data-ttu-id="53632-188">If the page hangs in the loading status when trying to sign in to Azure, refer to the ["page hanges when logging in" section of the IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/#page-hangs-when-log-in-azure) to resolve this issue.</span><span class="sxs-lookup"><span data-stu-id="53632-188">If the page hangs in the loading status when trying to sign in to Azure, refer to the ["page hanges when logging in" section of the IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/#page-hangs-when-log-in-azure) to resolve this issue.</span></span> 

### <a name="build-and-upload-the-device-code"></a><span data-ttu-id="53632-189">Build and upload the device code</span><span class="sxs-lookup"><span data-stu-id="53632-189">Build and upload the device code</span></span>

<span data-ttu-id="53632-190">Next, upload the code for the device.</span><span class="sxs-lookup"><span data-stu-id="53632-190">Next, upload the code for the device.</span></span>

#### <a name="windows"></a><span data-ttu-id="53632-191">Windows</span><span class="sxs-lookup"><span data-stu-id="53632-191">Windows</span></span>

1. <span data-ttu-id="53632-192">Use `Ctrl+P` to run `task device-upload`.</span><span class="sxs-lookup"><span data-stu-id="53632-192">Use `Ctrl+P` to run `task device-upload`.</span></span>

2. <span data-ttu-id="53632-193">The terminal prompts you to enter configuration mode.</span><span class="sxs-lookup"><span data-stu-id="53632-193">The terminal prompts you to enter configuration mode.</span></span> <span data-ttu-id="53632-194">To do so, hold down button A, then push and release the reset button.</span><span class="sxs-lookup"><span data-stu-id="53632-194">To do so, hold down button A, then push and release the reset button.</span></span> <span data-ttu-id="53632-195">The screen displays the DevKit identification number and the word *Configuration*.</span><span class="sxs-lookup"><span data-stu-id="53632-195">The screen displays the DevKit identification number and the word *Configuration*.</span></span>

#### <a name="macos"></a><span data-ttu-id="53632-196">macOS</span><span class="sxs-lookup"><span data-stu-id="53632-196">macOS</span></span>

1. <span data-ttu-id="53632-197">Put the DevKit into configuration mode: Hold down button A, then push and release the reset button.</span><span class="sxs-lookup"><span data-stu-id="53632-197">Put the DevKit into configuration mode: Hold down button A, then push and release the reset button.</span></span> <span data-ttu-id="53632-198">The screen displays 'Configuration'.</span><span class="sxs-lookup"><span data-stu-id="53632-198">The screen displays 'Configuration'.</span></span>

2. <span data-ttu-id="53632-199">Click `Cmd+P` to run `task device-upload`.</span><span class="sxs-lookup"><span data-stu-id="53632-199">Click `Cmd+P` to run `task device-upload`.</span></span>

#### <a name="verify-upload-and-run-the-sample-app"></a><span data-ttu-id="53632-200">Verify, upload, and run the sample app</span><span class="sxs-lookup"><span data-stu-id="53632-200">Verify, upload, and run the sample app</span></span>

<span data-ttu-id="53632-201">The connection string that is retrieved from the [Provision Azure services](#provision-azure-services) step is now set.</span><span class="sxs-lookup"><span data-stu-id="53632-201">The connection string that is retrieved from the [Provision Azure services](#provision-azure-services) step is now set.</span></span> 

<span data-ttu-id="53632-202">VS Code then starts verifying and uploading the Arduino sketch to the DevKit.</span><span class="sxs-lookup"><span data-stu-id="53632-202">VS Code then starts verifying and uploading the Arduino sketch to the DevKit.</span></span>

![device-upload](media/iot-hub-arduino-iot-devkit-az3166-door-monitor/device-upload.png)

<span data-ttu-id="53632-204">The DevKit reboots and starts running the code.</span><span class="sxs-lookup"><span data-stu-id="53632-204">The DevKit reboots and starts running the code.</span></span>

> [!NOTE]
> <span data-ttu-id="53632-205">Occasionally, you may receive an "Error: AZ3166: Unknown package" error message.</span><span class="sxs-lookup"><span data-stu-id="53632-205">Occasionally, you may receive an "Error: AZ3166: Unknown package" error message.</span></span> <span data-ttu-id="53632-206">This error occurs when the board package index is not refreshed correctly.</span><span class="sxs-lookup"><span data-stu-id="53632-206">This error occurs when the board package index is not refreshed correctly.</span></span> <span data-ttu-id="53632-207">To resolve this error, refer to the [development section of the IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/#development).</span><span class="sxs-lookup"><span data-stu-id="53632-207">To resolve this error, refer to the [development section of the IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/#development).</span></span>

## <a name="test-the-project"></a><span data-ttu-id="53632-208">Test the project</span><span class="sxs-lookup"><span data-stu-id="53632-208">Test the project</span></span>

<span data-ttu-id="53632-209">The program first initializes when the DevKit is in the presence of a stable magnetic field.</span><span class="sxs-lookup"><span data-stu-id="53632-209">The program first initializes when the DevKit is in the presence of a stable magnetic field.</span></span>

<span data-ttu-id="53632-210">After initialization, `Door closed` is displayed on the screen.</span><span class="sxs-lookup"><span data-stu-id="53632-210">After initialization, `Door closed` is displayed on the screen.</span></span> <span data-ttu-id="53632-211">When there is a change in the magnetic field, the state changes to `Door opened`.</span><span class="sxs-lookup"><span data-stu-id="53632-211">When there is a change in the magnetic field, the state changes to `Door opened`.</span></span> <span data-ttu-id="53632-212">Each time the door state changes, you receive an email notification.</span><span class="sxs-lookup"><span data-stu-id="53632-212">Each time the door state changes, you receive an email notification.</span></span> <span data-ttu-id="53632-213">(These email messages may take up to five minutes to be received.)</span><span class="sxs-lookup"><span data-stu-id="53632-213">(These email messages may take up to five minutes to be received.)</span></span>

<span data-ttu-id="53632-214">![Magnets close to the sensor: Door Closed](media/iot-hub-arduino-iot-devkit-az3166-door-monitor/test-door-closed.jpg "Magnets close to the sensor: Door Closed")</span><span class="sxs-lookup"><span data-stu-id="53632-214">![Magnets close to the sensor: Door Closed](media/iot-hub-arduino-iot-devkit-az3166-door-monitor/test-door-closed.jpg "Magnets close to the sensor: Door Closed")</span></span>

<span data-ttu-id="53632-215">![Magnet moved away from the sensor: Door Opened](media/iot-hub-arduino-iot-devkit-az3166-door-monitor/test-door-opened.jpg "Magnet moved away from the sensor: Door Opened")</span><span class="sxs-lookup"><span data-stu-id="53632-215">![Magnet moved away from the sensor: Door Opened](media/iot-hub-arduino-iot-devkit-az3166-door-monitor/test-door-opened.jpg "Magnet moved away from the sensor: Door Opened")</span></span>

## <a name="problems-and-feedback"></a><span data-ttu-id="53632-216">Problems and feedback</span><span class="sxs-lookup"><span data-stu-id="53632-216">Problems and feedback</span></span>

<span data-ttu-id="53632-217">If you encounter problems, refer to the [IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) or connect using the following channels:</span><span class="sxs-lookup"><span data-stu-id="53632-217">If you encounter problems, refer to the [IoT DevKit FAQ](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) or connect using the following channels:</span></span>

* [<span data-ttu-id="53632-218">Gitter.im</span><span class="sxs-lookup"><span data-stu-id="53632-218">Gitter.im</span></span>](http://gitter.im/Microsoft/azure-iot-developer-kit)
* [<span data-ttu-id="53632-219">Stackoverflow</span><span class="sxs-lookup"><span data-stu-id="53632-219">Stackoverflow</span></span>](https://stackoverflow.com/questions/tagged/iot-devkit)

## <a name="next-steps"></a><span data-ttu-id="53632-220">Next steps</span><span class="sxs-lookup"><span data-stu-id="53632-220">Next steps</span></span>

<span data-ttu-id="53632-221">You have learned how to connect a DevKit device to your Azure IoT Remote Monitoring solution accelerator and used the SendGrid service to send an email.</span><span class="sxs-lookup"><span data-stu-id="53632-221">You have learned how to connect a DevKit device to your Azure IoT Remote Monitoring solution accelerator and used the SendGrid service to send an email.</span></span> <span data-ttu-id="53632-222">Here are the suggested next steps:</span><span class="sxs-lookup"><span data-stu-id="53632-222">Here are the suggested next steps:</span></span>

* [<span data-ttu-id="53632-223">Azure IoT Remote Monitoring solution accelerator overview</span><span class="sxs-lookup"><span data-stu-id="53632-223">Azure IoT Remote Monitoring solution accelerator overview</span></span>](https://docs.microsoft.com/azure/iot-suite/)
* [<span data-ttu-id="53632-224">Connect an MXChip IoT DevKit device to your Azure IoT Central application</span><span class="sxs-lookup"><span data-stu-id="53632-224">Connect an MXChip IoT DevKit device to your Azure IoT Central application</span></span>](https://docs.microsoft.com/microsoft-iot-central/howto-connect-devkit)
