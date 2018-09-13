---
title: Auto-provision Azure IoT Edge device with DPS - Windows | Microsoft Docs
description: Use a simulated device on your Windows machine to test automatic device provisioning for Azure IoT Edge with Device Provisioning Service
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 08/06/2018
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: e558f44f9271009b92fbf4ece9aa706801e4176c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855586"
---
# <a name="create-and-provision-a-simulated-tpm-edge-device-on-windows"></a><span data-ttu-id="9be50-103">Create and provision a simulated TPM Edge device on Windows</span><span class="sxs-lookup"><span data-stu-id="9be50-103">Create and provision a simulated TPM Edge device on Windows</span></span>

<span data-ttu-id="9be50-104">Azure IoT Edge devices can be auto-provisioned using the [Device Provisioning Service](../iot-dps/index.yml) just like devices that are not edge-enabled.</span><span class="sxs-lookup"><span data-stu-id="9be50-104">Azure IoT Edge devices can be auto-provisioned using the [Device Provisioning Service](../iot-dps/index.yml) just like devices that are not edge-enabled.</span></span> <span data-ttu-id="9be50-105">If you're unfamiliar with the process of auto-provisioning, review the [auto-provisioning concepts](../iot-dps/concepts-auto-provisioning.md) before continuing.</span><span class="sxs-lookup"><span data-stu-id="9be50-105">If you're unfamiliar with the process of auto-provisioning, review the [auto-provisioning concepts](../iot-dps/concepts-auto-provisioning.md) before continuing.</span></span> 

<span data-ttu-id="9be50-106">This article shows you how to test auto-provisioning on a simulated Edge device with the following steps:</span><span class="sxs-lookup"><span data-stu-id="9be50-106">This article shows you how to test auto-provisioning on a simulated Edge device with the following steps:</span></span> 

* <span data-ttu-id="9be50-107">Create an instance of IoT Hub Device Provisioning Service (DPS).</span><span class="sxs-lookup"><span data-stu-id="9be50-107">Create an instance of IoT Hub Device Provisioning Service (DPS).</span></span>
* <span data-ttu-id="9be50-108">Create a simulated device on your Windows machine with a simulated Trusted Platform Module (TPM) for hardware security.</span><span class="sxs-lookup"><span data-stu-id="9be50-108">Create a simulated device on your Windows machine with a simulated Trusted Platform Module (TPM) for hardware security.</span></span>
* <span data-ttu-id="9be50-109">Create an individual enrollment for the device.</span><span class="sxs-lookup"><span data-stu-id="9be50-109">Create an individual enrollment for the device.</span></span>
* <span data-ttu-id="9be50-110">Install the IoT Edge runtime and connect the device to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9be50-110">Install the IoT Edge runtime and connect the device to IoT Hub.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9be50-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9be50-111">Prerequisites</span></span>

* <span data-ttu-id="9be50-112">A Windows development machine.</span><span class="sxs-lookup"><span data-stu-id="9be50-112">A Windows development machine.</span></span> <span data-ttu-id="9be50-113">This article uses Windows 10.</span><span class="sxs-lookup"><span data-stu-id="9be50-113">This article uses Windows 10.</span></span> 
* <span data-ttu-id="9be50-114">An active IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9be50-114">An active IoT Hub.</span></span> 

## <a name="set-up-the-iot-hub-device-provisioning-service"></a><span data-ttu-id="9be50-115">Set up the IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="9be50-115">Set up the IoT Hub Device Provisioning Service</span></span>

<span data-ttu-id="9be50-116">Create a new instance of the IoT Hub Device Provisioning Service in Azure, and link it to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9be50-116">Create a new instance of the IoT Hub Device Provisioning Service in Azure, and link it to your IoT hub.</span></span> <span data-ttu-id="9be50-117">You can follow the instructions in [Set up the IoT Hub DPS](../iot-dps/quick-setup-auto-provision.md).</span><span class="sxs-lookup"><span data-stu-id="9be50-117">You can follow the instructions in [Set up the IoT Hub DPS](../iot-dps/quick-setup-auto-provision.md).</span></span>

<span data-ttu-id="9be50-118">After you have the Device Provisioning Service running, copy the value of **ID Scope** from the overview page.</span><span class="sxs-lookup"><span data-stu-id="9be50-118">After you have the Device Provisioning Service running, copy the value of **ID Scope** from the overview page.</span></span> <span data-ttu-id="9be50-119">You use this value when you configure the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="9be50-119">You use this value when you configure the IoT Edge runtime.</span></span> 

## <a name="simulate-a-tpm-device"></a><span data-ttu-id="9be50-120">Simulate a TPM device</span><span class="sxs-lookup"><span data-stu-id="9be50-120">Simulate a TPM device</span></span>

<span data-ttu-id="9be50-121">Create a simulated TPM device on your Windows development machine.</span><span class="sxs-lookup"><span data-stu-id="9be50-121">Create a simulated TPM device on your Windows development machine.</span></span> <span data-ttu-id="9be50-122">Retrieve the **Registration ID** and **Endorsement Key** for your device, and use them to create an individual enrollment entry in DPS.</span><span class="sxs-lookup"><span data-stu-id="9be50-122">Retrieve the **Registration ID** and **Endorsement Key** for your device, and use them to create an individual enrollment entry in DPS.</span></span> 

<span data-ttu-id="9be50-123">When you create an enrollment in DPS, you have the opportunity to declare an **Initial Device Twin State**.</span><span class="sxs-lookup"><span data-stu-id="9be50-123">When you create an enrollment in DPS, you have the opportunity to declare an **Initial Device Twin State**.</span></span> <span data-ttu-id="9be50-124">In the device twin you can set tags to group devices by any metric you need in your solution, like region, environment, location, or device type.</span><span class="sxs-lookup"><span data-stu-id="9be50-124">In the device twin you can set tags to group devices by any metric you need in your solution, like region, environment, location, or device type.</span></span> <span data-ttu-id="9be50-125">These tags are used to create [automatic deployments](how-to-deploy-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="9be50-125">These tags are used to create [automatic deployments](how-to-deploy-monitor.md).</span></span> 

<span data-ttu-id="9be50-126">Choose the SDK language that you want to use to create the simulated device, and follow the steps until you create the individual enrollment.</span><span class="sxs-lookup"><span data-stu-id="9be50-126">Choose the SDK language that you want to use to create the simulated device, and follow the steps until you create the individual enrollment.</span></span> 

<span data-ttu-id="9be50-127">When you create the individual enrollment, select **Enable** to declare that this virtual machine is an **IoT Edge device**.</span><span class="sxs-lookup"><span data-stu-id="9be50-127">When you create the individual enrollment, select **Enable** to declare that this virtual machine is an **IoT Edge device**.</span></span>

<span data-ttu-id="9be50-128">Simulated device and individual enrollment guides:</span><span class="sxs-lookup"><span data-stu-id="9be50-128">Simulated device and individual enrollment guides:</span></span> 
* [<span data-ttu-id="9be50-129">C</span><span class="sxs-lookup"><span data-stu-id="9be50-129">C</span></span>](../iot-dps/quick-create-simulated-device.md)
* [<span data-ttu-id="9be50-130">Java</span><span class="sxs-lookup"><span data-stu-id="9be50-130">Java</span></span>](../iot-dps/quick-create-simulated-device-tpm-java.md)
* [<span data-ttu-id="9be50-131">C#</span><span class="sxs-lookup"><span data-stu-id="9be50-131">C#</span></span>](../iot-dps/quick-create-simulated-device-tpm-csharp.md)
* [<span data-ttu-id="9be50-132">Node.js</span><span class="sxs-lookup"><span data-stu-id="9be50-132">Node.js</span></span>](../iot-dps/quick-create-simulated-device-tpm-node.md)
* [<span data-ttu-id="9be50-133">Python</span><span class="sxs-lookup"><span data-stu-id="9be50-133">Python</span></span>](../iot-dps/quick-create-simulated-device-tpm-python.md)

<span data-ttu-id="9be50-134">After creating the individual enrollment, save the value of the **Registration ID**.</span><span class="sxs-lookup"><span data-stu-id="9be50-134">After creating the individual enrollment, save the value of the **Registration ID**.</span></span> <span data-ttu-id="9be50-135">You use this value when you configure the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="9be50-135">You use this value when you configure the IoT Edge runtime.</span></span> 

## <a name="install-the-iot-edge-runtime"></a><span data-ttu-id="9be50-136">Install the IoT Edge runtime</span><span class="sxs-lookup"><span data-stu-id="9be50-136">Install the IoT Edge runtime</span></span>

<span data-ttu-id="9be50-137">After completing the previous section, you should see your new device listed as an IoT Edge device in your IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9be50-137">After completing the previous section, you should see your new device listed as an IoT Edge device in your IoT Hub.</span></span> <span data-ttu-id="9be50-138">Now, you need to install the IoT Edge runtime on your device.</span><span class="sxs-lookup"><span data-stu-id="9be50-138">Now, you need to install the IoT Edge runtime on your device.</span></span> 

<span data-ttu-id="9be50-139">The IoT Edge runtime is deployed on all IoT Edge devices.</span><span class="sxs-lookup"><span data-stu-id="9be50-139">The IoT Edge runtime is deployed on all IoT Edge devices.</span></span> <span data-ttu-id="9be50-140">Its components run in containers, and allow you to deploy additional containers to the device so that you can run code at the edge.</span><span class="sxs-lookup"><span data-stu-id="9be50-140">Its components run in containers, and allow you to deploy additional containers to the device so that you can run code at the edge.</span></span> <span data-ttu-id="9be50-141">On devices running Windows, you can choose to either use Windows containers or Linux containers.</span><span class="sxs-lookup"><span data-stu-id="9be50-141">On devices running Windows, you can choose to either use Windows containers or Linux containers.</span></span> <span data-ttu-id="9be50-142">Choose the type of containers that you want to use, and follow the steps.</span><span class="sxs-lookup"><span data-stu-id="9be50-142">Choose the type of containers that you want to use, and follow the steps.</span></span> <span data-ttu-id="9be50-143">Make sure to configure the IoT Edge runtime for automatic, not manual, provisioning.</span><span class="sxs-lookup"><span data-stu-id="9be50-143">Make sure to configure the IoT Edge runtime for automatic, not manual, provisioning.</span></span> 

<span data-ttu-id="9be50-144">Follow the instructions to install the IoT Edge runtime on the device that is running the simulated TPM from the previous section.</span><span class="sxs-lookup"><span data-stu-id="9be50-144">Follow the instructions to install the IoT Edge runtime on the device that is running the simulated TPM from the previous section.</span></span> 

<span data-ttu-id="9be50-145">Know your DPS **ID Scope** and device **Registration ID** before beginning these articles.</span><span class="sxs-lookup"><span data-stu-id="9be50-145">Know your DPS **ID Scope** and device **Registration ID** before beginning these articles.</span></span> 

* [<span data-ttu-id="9be50-146">Windows containers</span><span class="sxs-lookup"><span data-stu-id="9be50-146">Windows containers</span></span>](how-to-install-iot-edge-windows-with-windows.md)
* [<span data-ttu-id="9be50-147">Linux containers</span><span class="sxs-lookup"><span data-stu-id="9be50-147">Linux containers</span></span>](how-to-install-iot-edge-windows-with-linux.md)

## <a name="verify-successful-installation"></a><span data-ttu-id="9be50-148">Verify successful installation</span><span class="sxs-lookup"><span data-stu-id="9be50-148">Verify successful installation</span></span>

<span data-ttu-id="9be50-149">If the runtime started successfully, you can go into your IoT Hub and start deploying IoT Edge modules to your device.</span><span class="sxs-lookup"><span data-stu-id="9be50-149">If the runtime started successfully, you can go into your IoT Hub and start deploying IoT Edge modules to your device.</span></span> <span data-ttu-id="9be50-150">Use the following commands on your device to verify that the runtime installed and started successfully.</span><span class="sxs-lookup"><span data-stu-id="9be50-150">Use the following commands on your device to verify that the runtime installed and started successfully.</span></span>  

<span data-ttu-id="9be50-151">Check the status of the IoT Edge service.</span><span class="sxs-lookup"><span data-stu-id="9be50-151">Check the status of the IoT Edge service.</span></span>

```powershell
Get-Service iotedge
```

<span data-ttu-id="9be50-152">Examine service logs from the last 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="9be50-152">Examine service logs from the last 5 minutes.</span></span>

```powershell
# Displays logs from last 5 min, newest at the bottom.

Get-WinEvent -ea SilentlyContinue `
  -FilterHashtable @{ProviderName= "iotedged";
    LogName = "application"; StartTime = [datetime]::Now.AddMinutes(-5)} |
  select TimeCreated, Message |
  sort-object @{Expression="TimeCreated";Descending=$false} |
  format-table -autosize -wrap
```

<span data-ttu-id="9be50-153">List running modules.</span><span class="sxs-lookup"><span data-stu-id="9be50-153">List running modules.</span></span>

```powershell
iotedge list
```

## <a name="next-steps"></a><span data-ttu-id="9be50-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="9be50-154">Next steps</span></span>

<span data-ttu-id="9be50-155">The Device Provisioning Service enrollment process lets you set the device ID and device twin tags at the same time as you provision the new device.</span><span class="sxs-lookup"><span data-stu-id="9be50-155">The Device Provisioning Service enrollment process lets you set the device ID and device twin tags at the same time as you provision the new device.</span></span> <span data-ttu-id="9be50-156">You can use those values to target individual devices or groups of devices using automatic device management.</span><span class="sxs-lookup"><span data-stu-id="9be50-156">You can use those values to target individual devices or groups of devices using automatic device management.</span></span> <span data-ttu-id="9be50-157">Learn how to [Deploy and monitor IoT Edge modules at scale using the Azure portal](how-to-deploy-monitor.md) or [using Azure CLI](how-to-deploy-monitor-cli.md)</span><span class="sxs-lookup"><span data-stu-id="9be50-157">Learn how to [Deploy and monitor IoT Edge modules at scale using the Azure portal](how-to-deploy-monitor.md) or [using Azure CLI](how-to-deploy-monitor-cli.md)</span></span>
