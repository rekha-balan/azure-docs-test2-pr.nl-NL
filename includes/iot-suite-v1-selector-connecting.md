---
title: include file
description: include file
services: iot-accelerators
author: dominicbetts
ms.service: iot-accelerators
ms.topic: include
ms.date: 05/30/2018
ms.author: dobett
ms.custom: include file
ms.openlocfilehash: 55920b6c147626f68f51b9e0479949330c71a748
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45158914"
---
> [!div class="op_single_selector"]
> * [C on Windows](../articles/iot-suite/iot-suite-v1-connecting-devices.md)
> * [C on Linux](../articles/iot-suite/iot-suite-v1-connecting-devices-linux.md)
> * [Node.js](../articles/iot-suite/iot-suite-v1-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a><span data-ttu-id="91e80-106">Scenario overview</span><span class="sxs-lookup"><span data-stu-id="91e80-106">Scenario overview</span></span>
<span data-ttu-id="91e80-107">In this scenario, you create a device that sends the following telemetry to the remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="91e80-107">In this scenario, you create a device that sends the following telemetry to the remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="91e80-108">External temperature</span><span class="sxs-lookup"><span data-stu-id="91e80-108">External temperature</span></span>
* <span data-ttu-id="91e80-109">Internal temperature</span><span class="sxs-lookup"><span data-stu-id="91e80-109">Internal temperature</span></span>
* <span data-ttu-id="91e80-110">Humidity</span><span class="sxs-lookup"><span data-stu-id="91e80-110">Humidity</span></span>

<span data-ttu-id="91e80-111">For simplicity, the code on the device generates sample values, but we encourage you to extend the sample by connecting real sensors to your device and sending real telemetry.</span><span class="sxs-lookup"><span data-stu-id="91e80-111">For simplicity, the code on the device generates sample values, but we encourage you to extend the sample by connecting real sensors to your device and sending real telemetry.</span></span>

<span data-ttu-id="91e80-112">The device is also able to respond to methods invoked from the solution dashboard and desired property values set in the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="91e80-112">The device is also able to respond to methods invoked from the solution dashboard and desired property values set in the solution dashboard.</span></span>

<span data-ttu-id="91e80-113">To complete this tutorial, you need an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="91e80-113">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="91e80-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="91e80-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="91e80-115">For details, see [Azure Free Trial][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="91e80-115">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="91e80-116">Before you start</span><span class="sxs-lookup"><span data-stu-id="91e80-116">Before you start</span></span>
<span data-ttu-id="91e80-117">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span><span class="sxs-lookup"><span data-stu-id="91e80-117">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="91e80-118">Provision your remote monitoring preconfigured solution</span><span class="sxs-lookup"><span data-stu-id="91e80-118">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="91e80-119">The device you create in this tutorial sends data to an instance of the [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="91e80-119">The device you create in this tutorial sends data to an instance of the [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="91e80-120">If you haven't already provisioned the remote monitoring preconfigured solution in your Azure account, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="91e80-120">If you haven't already provisioned the remote monitoring preconfigured solution in your Azure account, use the following steps:</span></span>

1. <span data-ttu-id="91e80-121">On the <https://www.azureiotsolutions.com/> page, click **+** to create a solution.</span><span class="sxs-lookup"><span data-stu-id="91e80-121">On the <https://www.azureiotsolutions.com/> page, click **+** to create a solution.</span></span>
2. <span data-ttu-id="91e80-122">Click **Select** on the **Remote monitoring** panel to create your solution.</span><span class="sxs-lookup"><span data-stu-id="91e80-122">Click **Select** on the **Remote monitoring** panel to create your solution.</span></span>
3. <span data-ttu-id="91e80-123">On the **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select the **Region** you want to deploy to, and select the Azure subscription to want to use.</span><span class="sxs-lookup"><span data-stu-id="91e80-123">On the **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select the **Region** you want to deploy to, and select the Azure subscription to want to use.</span></span> <span data-ttu-id="91e80-124">Then click **Create solution**.</span><span class="sxs-lookup"><span data-stu-id="91e80-124">Then click **Create solution**.</span></span>
4. <span data-ttu-id="91e80-125">Wait until the provisioning process completes.</span><span class="sxs-lookup"><span data-stu-id="91e80-125">Wait until the provisioning process completes.</span></span>

> [!WARNING]
> The preconfigured solutions use billable Azure services. Be sure to remove the preconfigured solution from your subscription when you are done with it to avoid any unnecessary charges. You can completely remove a preconfigured solution from your subscription by visiting the <https://www.azureiotsolutions.com/> page.
> 
> 

<span data-ttu-id="91e80-129">When the provisioning process for the remote monitoring solution finishes, click **Launch** to open the solution dashboard in your browser.</span><span class="sxs-lookup"><span data-stu-id="91e80-129">When the provisioning process for the remote monitoring solution finishes, click **Launch** to open the solution dashboard in your browser.</span></span>

![Solution dashboard][img-dashboard]

### <a name="provision-your-device-in-the-remote-monitoring-solution"></a><span data-ttu-id="91e80-131">Provision your device in the remote monitoring solution</span><span class="sxs-lookup"><span data-stu-id="91e80-131">Provision your device in the remote monitoring solution</span></span>
> [!NOTE]
> If you have already provisioned a device in your solution, you can skip this step. You need to know the device credentials when you create the client application.
> 
> 

<span data-ttu-id="91e80-134">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span><span class="sxs-lookup"><span data-stu-id="91e80-134">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="91e80-135">You can retrieve the device credentials from the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="91e80-135">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="91e80-136">You include the device credentials in your client application later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="91e80-136">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="91e80-137">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span><span class="sxs-lookup"><span data-stu-id="91e80-137">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="91e80-138">In the lower left-hand corner of the dashboard, click **Add a device**.</span><span class="sxs-lookup"><span data-stu-id="91e80-138">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>
   
   ![Add a device][1]
2. <span data-ttu-id="91e80-140">In the **Custom Device** panel, click **Add new**.</span><span class="sxs-lookup"><span data-stu-id="91e80-140">In the **Custom Device** panel, click **Add new**.</span></span>
   
   ![Add a custom device][2]
3. <span data-ttu-id="91e80-142">Choose **Let me define my own Device ID**.</span><span class="sxs-lookup"><span data-stu-id="91e80-142">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="91e80-143">Enter a Device ID such as **mydevice**, click **Check ID** to verify that name isn't already in use, and then click **Create** to provision the device.</span><span class="sxs-lookup"><span data-stu-id="91e80-143">Enter a Device ID such as **mydevice**, click **Check ID** to verify that name isn't already in use, and then click **Create** to provision the device.</span></span>
   
   ![Add device ID][3]
4. <span data-ttu-id="91e80-145">Make a note the device credentials (Device ID, IoT Hub Hostname, and Device Key).</span><span class="sxs-lookup"><span data-stu-id="91e80-145">Make a note the device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="91e80-146">Your client application needs these values to connect to the remote monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="91e80-146">Your client application needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="91e80-147">Then click **Done**.</span><span class="sxs-lookup"><span data-stu-id="91e80-147">Then click **Done**.</span></span>
   
    ![View device credentials][4]
5. <span data-ttu-id="91e80-149">Select your device in the device list in the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="91e80-149">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="91e80-150">Then, in the **Device Details** panel, click **Enable Device**.</span><span class="sxs-lookup"><span data-stu-id="91e80-150">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="91e80-151">The status of your device is now **Running**.</span><span class="sxs-lookup"><span data-stu-id="91e80-151">The status of your device is now **Running**.</span></span> <span data-ttu-id="91e80-152">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span><span class="sxs-lookup"><span data-stu-id="91e80-152">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-dashboard]: ./media/iot-suite-v1-selector-connecting/dashboard.png
[1]: ./media/iot-suite-v1-selector-connecting/suite0.png
[2]: ./media/iot-suite-v1-selector-connecting/suite1.png
[3]: ./media/iot-suite-v1-selector-connecting/suite2.png
[4]: ./media/iot-suite-v1-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-v1-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-v1-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/