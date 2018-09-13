---
title: How to install Azure IoT Edge on Windows with Linux containers | Microsoft Docs
description: Azure IoT Edge installation instructions on Windows with Linux containers
author: kgremban
manager: timlt
ms.reviewer: veyalla
ms.service: iot-edge
services: iot-edge
ms.topic: conceptual
ms.date: 08/27/2018
ms.author: kgremban
ms.openlocfilehash: d6852b5b1fe3d0b3c248fc1948fa4c3a9428de89
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856968"
---
# <a name="install-azure-iot-edge-runtime-on-windows-to-use-with-linux-containers"></a><span data-ttu-id="480bb-103">Install Azure IoT Edge runtime on Windows to use with Linux containers</span><span class="sxs-lookup"><span data-stu-id="480bb-103">Install Azure IoT Edge runtime on Windows to use with Linux containers</span></span>

<span data-ttu-id="480bb-104">The Azure IoT Edge runtime is what turns a device into an IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="480bb-104">The Azure IoT Edge runtime is what turns a device into an IoT Edge device.</span></span> <span data-ttu-id="480bb-105">The runtime can be deployed on devices as small as a Raspberry Pi or as large as an industrial server.</span><span class="sxs-lookup"><span data-stu-id="480bb-105">The runtime can be deployed on devices as small as a Raspberry Pi or as large as an industrial server.</span></span> <span data-ttu-id="480bb-106">Once a device is configured with the IoT Edge runtime, you can start deploying business logic to it from the cloud.</span><span class="sxs-lookup"><span data-stu-id="480bb-106">Once a device is configured with the IoT Edge runtime, you can start deploying business logic to it from the cloud.</span></span> 

<span data-ttu-id="480bb-107">To learn more about how the IoT Edge runtime works and what components are included, see [Understand the Azure IoT Edge runtime and its architecture](iot-edge-runtime.md).</span><span class="sxs-lookup"><span data-stu-id="480bb-107">To learn more about how the IoT Edge runtime works and what components are included, see [Understand the Azure IoT Edge runtime and its architecture](iot-edge-runtime.md).</span></span>

<span data-ttu-id="480bb-108">This article lists the steps to install the Azure IoT Edge runtime with Linux containers on your Windows x64 (AMD/Intel) system.</span><span class="sxs-lookup"><span data-stu-id="480bb-108">This article lists the steps to install the Azure IoT Edge runtime with Linux containers on your Windows x64 (AMD/Intel) system.</span></span> <span data-ttu-id="480bb-109">Windows support is currently in Preview.</span><span class="sxs-lookup"><span data-stu-id="480bb-109">Windows support is currently in Preview.</span></span>

>[!NOTE]
<span data-ttu-id="480bb-110">Using Linux containers on Windows sytems is not a recommended or supported production configuration for Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="480bb-110">Using Linux containers on Windows sytems is not a recommended or supported production configuration for Azure IoT Edge.</span></span> <span data-ttu-id="480bb-111">However, it can be used for development and testing purposes.</span><span class="sxs-lookup"><span data-stu-id="480bb-111">However, it can be used for development and testing purposes.</span></span>

## <a name="supported-windows-versions"></a><span data-ttu-id="480bb-112">Supported Windows versions</span><span class="sxs-lookup"><span data-stu-id="480bb-112">Supported Windows versions</span></span>
<span data-ttu-id="480bb-113">Azure IoT Edge can be used for development and testing on following versions of Windows, when using Linux containers:</span><span class="sxs-lookup"><span data-stu-id="480bb-113">Azure IoT Edge can be used for development and testing on following versions of Windows, when using Linux containers:</span></span>
  * <span data-ttu-id="480bb-114">Windows 10 or newer desktop operating systems.</span><span class="sxs-lookup"><span data-stu-id="480bb-114">Windows 10 or newer desktop operating systems.</span></span>
  * <span data-ttu-id="480bb-115">Windows Server 2016 or new server operating systems.</span><span class="sxs-lookup"><span data-stu-id="480bb-115">Windows Server 2016 or new server operating systems.</span></span>

<span data-ttu-id="480bb-116">For more information about which operating systems are currently supported, refer to [Azure IoT Edge support](support.md#operating-systems).</span><span class="sxs-lookup"><span data-stu-id="480bb-116">For more information about which operating systems are currently supported, refer to [Azure IoT Edge support](support.md#operating-systems).</span></span> 

## <a name="install-the-container-runtime"></a><span data-ttu-id="480bb-117">Install the container runtime</span><span class="sxs-lookup"><span data-stu-id="480bb-117">Install the container runtime</span></span> 

<span data-ttu-id="480bb-118">Azure IoT Edge relies on a [OCI-compatible][lnk-oci] container runtime (for example, Docker).</span><span class="sxs-lookup"><span data-stu-id="480bb-118">Azure IoT Edge relies on a [OCI-compatible][lnk-oci] container runtime (for example, Docker).</span></span> 

<span data-ttu-id="480bb-119">You can use [Docker for Windows][lnk-docker-for-windows] for development and testing.</span><span class="sxs-lookup"><span data-stu-id="480bb-119">You can use [Docker for Windows][lnk-docker-for-windows] for development and testing.</span></span> <span data-ttu-id="480bb-120">Configure Docker for Windows [to use Linux containers][lnk-docker-config]</span><span class="sxs-lookup"><span data-stu-id="480bb-120">Configure Docker for Windows [to use Linux containers][lnk-docker-config]</span></span>

## <a name="install-the-azure-iot-edge-security-daemon"></a><span data-ttu-id="480bb-121">Install the Azure IoT Edge Security Daemon</span><span class="sxs-lookup"><span data-stu-id="480bb-121">Install the Azure IoT Edge Security Daemon</span></span>

>[!NOTE]
><span data-ttu-id="480bb-122">Azure IoT Edge software packages are subject to the license terms located in the packages (in the LICENSE directory).</span><span class="sxs-lookup"><span data-stu-id="480bb-122">Azure IoT Edge software packages are subject to the license terms located in the packages (in the LICENSE directory).</span></span> <span data-ttu-id="480bb-123">Please read the license terms prior to using the package.</span><span class="sxs-lookup"><span data-stu-id="480bb-123">Please read the license terms prior to using the package.</span></span> <span data-ttu-id="480bb-124">Your installation and use of the package constitutes your acceptance of these terms.</span><span class="sxs-lookup"><span data-stu-id="480bb-124">Your installation and use of the package constitutes your acceptance of these terms.</span></span> <span data-ttu-id="480bb-125">If you do not agree with the license terms, do not use the package.</span><span class="sxs-lookup"><span data-stu-id="480bb-125">If you do not agree with the license terms, do not use the package.</span></span>

<span data-ttu-id="480bb-126">A single IoT Edge device can be provisioned manually using a device connections string provided by IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="480bb-126">A single IoT Edge device can be provisioned manually using a device connections string provided by IoT Hub.</span></span> <span data-ttu-id="480bb-127">Or, you can use the Device Provisioning Service to automatically provision devices, which is helpful when you have many devices to provision.</span><span class="sxs-lookup"><span data-stu-id="480bb-127">Or, you can use the Device Provisioning Service to automatically provision devices, which is helpful when you have many devices to provision.</span></span> <span data-ttu-id="480bb-128">Depending on your provisioning choice, choose the appropriate installation script.</span><span class="sxs-lookup"><span data-stu-id="480bb-128">Depending on your provisioning choice, choose the appropriate installation script.</span></span> 

### <a name="option-1-install-and-manually-provision"></a><span data-ttu-id="480bb-129">Option 1: Install and manually provision</span><span class="sxs-lookup"><span data-stu-id="480bb-129">Option 1: Install and manually provision</span></span>

1. <span data-ttu-id="480bb-130">Follow the steps in [Register a new Azure IoT Edge device][lnk-dcs] to register your device and retrieve the device connection string.</span><span class="sxs-lookup"><span data-stu-id="480bb-130">Follow the steps in [Register a new Azure IoT Edge device][lnk-dcs] to register your device and retrieve the device connection string.</span></span> 

2. <span data-ttu-id="480bb-131">On your IoT Edge device, run PowerShell as an administrator.</span><span class="sxs-lookup"><span data-stu-id="480bb-131">On your IoT Edge device, run PowerShell as an administrator.</span></span> 

3. <span data-ttu-id="480bb-132">Download and install the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="480bb-132">Download and install the IoT Edge runtime.</span></span> 

   ```powershell
   . {Invoke-WebRequest -useb aka.ms/iotedge-win} | Invoke-Expression; `
   Install-SecurityDaemon -Manual -ContainerOs Linux
   ```

4. <span data-ttu-id="480bb-133">When prompted for a **DeviceConnectionString**, provide the connection string that you retrieved from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="480bb-133">When prompted for a **DeviceConnectionString**, provide the connection string that you retrieved from IoT Hub.</span></span> <span data-ttu-id="480bb-134">Do not include quotes around the connection string.</span><span class="sxs-lookup"><span data-stu-id="480bb-134">Do not include quotes around the connection string.</span></span> 

### <a name="option-2-install-and-automatically-provision"></a><span data-ttu-id="480bb-135">Option 2: Install and automatically provision</span><span class="sxs-lookup"><span data-stu-id="480bb-135">Option 2: Install and automatically provision</span></span>

1. <span data-ttu-id="480bb-136">Follow the steps in [Create and provision a simulated TPM Edge device on Windows][lnk-dps] to set up the Device Provisioning Service and retrieve its **Scope ID**, simulate a TPM device and retrieve its **Registration ID**, then create an individual enrollment.</span><span class="sxs-lookup"><span data-stu-id="480bb-136">Follow the steps in [Create and provision a simulated TPM Edge device on Windows][lnk-dps] to set up the Device Provisioning Service and retrieve its **Scope ID**, simulate a TPM device and retrieve its **Registration ID**, then create an individual enrollment.</span></span> <span data-ttu-id="480bb-137">Once your device is registered in your IoT Hub, continue with the installation.</span><span class="sxs-lookup"><span data-stu-id="480bb-137">Once your device is registered in your IoT Hub, continue with the installation.</span></span>  

   >[!TIP]
   ><span data-ttu-id="480bb-138">Keep the window that's running the TPM simulator open during your installation and testing.</span><span class="sxs-lookup"><span data-stu-id="480bb-138">Keep the window that's running the TPM simulator open during your installation and testing.</span></span> 

2. <span data-ttu-id="480bb-139">On your IoT Edge device, run PowerShell as an administrator.</span><span class="sxs-lookup"><span data-stu-id="480bb-139">On your IoT Edge device, run PowerShell as an administrator.</span></span> 

3. <span data-ttu-id="480bb-140">Download and install the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="480bb-140">Download and install the IoT Edge runtime.</span></span> 

   ```powershell
   . {Invoke-WebRequest -useb aka.ms/iotedge-win} | Invoke-Expression; `
   Install-SecurityDaemon -Dps -ContainerOs Linux
   ```

4. <span data-ttu-id="480bb-141">When prompted, provide the **ScopeID** and **RegistrationID** for your provisioning service and device.</span><span class="sxs-lookup"><span data-stu-id="480bb-141">When prompted, provide the **ScopeID** and **RegistrationID** for your provisioning service and device.</span></span>

## <a name="verify-successful-installation"></a><span data-ttu-id="480bb-142">Verify successful installation</span><span class="sxs-lookup"><span data-stu-id="480bb-142">Verify successful installation</span></span>

<span data-ttu-id="480bb-143">You can check the status of the IoT Edge service by:</span><span class="sxs-lookup"><span data-stu-id="480bb-143">You can check the status of the IoT Edge service by:</span></span> 

```powershell
Get-Service iotedge
```

<span data-ttu-id="480bb-144">Examine service logs from the last 5 minutes using:</span><span class="sxs-lookup"><span data-stu-id="480bb-144">Examine service logs from the last 5 minutes using:</span></span>

```powershell

# Displays logs from last 5 min, newest at the bottom.

Get-WinEvent -ea SilentlyContinue `
  -FilterHashtable @{ProviderName= "iotedged";
    LogName = "application"; StartTime = [datetime]::Now.AddMinutes(-5)} |
  select TimeCreated, Message |
  sort-object @{Expression="TimeCreated";Descending=$false} |
  format-table -autosize -wrap
```

<span data-ttu-id="480bb-145">And, list running modules with:</span><span class="sxs-lookup"><span data-stu-id="480bb-145">And, list running modules with:</span></span>

```powershell
iotedge list
```

## <a name="next-steps"></a><span data-ttu-id="480bb-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="480bb-146">Next steps</span></span>

<span data-ttu-id="480bb-147">Now that you have an IoT Edge device provisioned with the runtime installed, you can [deploy IoT Edge modules][lnk-modules].</span><span class="sxs-lookup"><span data-stu-id="480bb-147">Now that you have an IoT Edge device provisioned with the runtime installed, you can [deploy IoT Edge modules][lnk-modules].</span></span>

<span data-ttu-id="480bb-148">If you are having problems with the Edge runtime installing properly, check out the [troubleshooting][lnk-trouble] page.</span><span class="sxs-lookup"><span data-stu-id="480bb-148">If you are having problems with the Edge runtime installing properly, check out the [troubleshooting][lnk-trouble] page.</span></span>


<!-- Images -->
[img-docker-nat]: ./media/how-to-install-iot-edge-windows-with-linux/dockernat.png

<!-- Links -->
[lnk-docker-config]: https://docs.docker.com/docker-for-windows/#switch-between-windows-and-linux-containers
[lnk-dcs]: how-to-register-device-portal.md
[lnk-dps]: how-to-auto-provision-simulated-device-windows.md
[lnk-oci]: https://www.opencontainers.org/
[lnk-moby]: https://mobyproject.org/
[lnk-trouble]: troubleshoot.md
[lnk-docker-for-windows]: https://www.docker.com/docker-windows
[lnk-modules]: how-to-deploy-modules-portal.md
