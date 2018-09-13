---
title: How to install Azure IoT Edge on Windows with Windows containers | Microsoft Docs
description: Azure IoT Edge installation instructions on Windows with  Windows containers
author: kgremban
manager: timlt
ms.reviewer: veyalla
ms.service: iot-edge
services: iot-edge
ms.topic: conceptual
ms.date: 08/27/2018
ms.author: kgremban
ms.openlocfilehash: e92adc5dbd0da6ab4f60f8cc7bf6dbe7a58694c6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870804"
---
# <a name="install-azure-iot-edge-runtime-on-windows-to-use-with-windows-containers"></a><span data-ttu-id="61ef4-103">Install Azure IoT Edge runtime on Windows to use with Windows containers</span><span class="sxs-lookup"><span data-stu-id="61ef4-103">Install Azure IoT Edge runtime on Windows to use with Windows containers</span></span>

<span data-ttu-id="61ef4-104">The Azure IoT Edge runtime is what turns a device into an IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="61ef4-104">The Azure IoT Edge runtime is what turns a device into an IoT Edge device.</span></span> <span data-ttu-id="61ef4-105">The runtime can be deployed on devices as small as a Raspberry Pi or as large as an industrial server.</span><span class="sxs-lookup"><span data-stu-id="61ef4-105">The runtime can be deployed on devices as small as a Raspberry Pi or as large as an industrial server.</span></span> <span data-ttu-id="61ef4-106">Once a device is configured with the IoT Edge runtime, you can start deploying business logic to it from the cloud.</span><span class="sxs-lookup"><span data-stu-id="61ef4-106">Once a device is configured with the IoT Edge runtime, you can start deploying business logic to it from the cloud.</span></span> 

<span data-ttu-id="61ef4-107">To learn more about how the IoT Edge runtime works and what components are included, see [Understand the Azure IoT Edge runtime and its architecture](iot-edge-runtime.md).</span><span class="sxs-lookup"><span data-stu-id="61ef4-107">To learn more about how the IoT Edge runtime works and what components are included, see [Understand the Azure IoT Edge runtime and its architecture](iot-edge-runtime.md).</span></span>

<span data-ttu-id="61ef4-108">This article lists the steps to install the Azure IoT Edge runtime with Windows containers on your Windows x64 (AMD/Intel) system.</span><span class="sxs-lookup"><span data-stu-id="61ef4-108">This article lists the steps to install the Azure IoT Edge runtime with Windows containers on your Windows x64 (AMD/Intel) system.</span></span> 

<span data-ttu-id="61ef4-109">Windows support is currently in Preview.</span><span class="sxs-lookup"><span data-stu-id="61ef4-109">Windows support is currently in Preview.</span></span>

## <a name="supported-windows-versions"></a><span data-ttu-id="61ef4-110">Supported Windows versions</span><span class="sxs-lookup"><span data-stu-id="61ef4-110">Supported Windows versions</span></span>
<span data-ttu-id="61ef4-111">Azure IoT Edge with Windows containers can be used with:</span><span class="sxs-lookup"><span data-stu-id="61ef4-111">Azure IoT Edge with Windows containers can be used with:</span></span>
  * <span data-ttu-id="61ef4-112">Windows 10/IoT Enterprise/IoT Core with April 2018 update (Build 17134).</span><span class="sxs-lookup"><span data-stu-id="61ef4-112">Windows 10/IoT Enterprise/IoT Core with April 2018 update (Build 17134).</span></span>
  * <span data-ttu-id="61ef4-113">Windows Server 1803</span><span class="sxs-lookup"><span data-stu-id="61ef4-113">Windows Server 1803</span></span>

<span data-ttu-id="61ef4-114">For more information about which operating systems are currently supported, refer to [Azure IoT Edge support](support.md#operating-systems).</span><span class="sxs-lookup"><span data-stu-id="61ef4-114">For more information about which operating systems are currently supported, refer to [Azure IoT Edge support](support.md#operating-systems).</span></span>

## <a name="install-the-container-runtime"></a><span data-ttu-id="61ef4-115">Install the container runtime</span><span class="sxs-lookup"><span data-stu-id="61ef4-115">Install the container runtime</span></span> 

>[!NOTE]
><span data-ttu-id="61ef4-116">For container engine installation on Windows IoT Core, follow steps from [provision an IoT Core device article][lnk-iot-core] and then continue with instructions below.</span><span class="sxs-lookup"><span data-stu-id="61ef4-116">For container engine installation on Windows IoT Core, follow steps from [provision an IoT Core device article][lnk-iot-core] and then continue with instructions below.</span></span>

<span data-ttu-id="61ef4-117">Azure IoT Edge relies on a [OCI-compatible][lnk-oci] container runtime (for example, Docker).</span><span class="sxs-lookup"><span data-stu-id="61ef4-117">Azure IoT Edge relies on a [OCI-compatible][lnk-oci] container runtime (for example, Docker).</span></span> <span data-ttu-id="61ef4-118">You can use [Docker for Windows][lnk-docker-for-windows] for development and testing.</span><span class="sxs-lookup"><span data-stu-id="61ef4-118">You can use [Docker for Windows][lnk-docker-for-windows] for development and testing.</span></span> 

<span data-ttu-id="61ef4-119">Configure Docker for Windows [to use Windows containers][lnk-docker-config].</span><span class="sxs-lookup"><span data-stu-id="61ef4-119">Configure Docker for Windows [to use Windows containers][lnk-docker-config].</span></span>

## <a name="install-the-azure-iot-edge-security-daemon"></a><span data-ttu-id="61ef4-120">Install the Azure IoT Edge Security Daemon</span><span class="sxs-lookup"><span data-stu-id="61ef4-120">Install the Azure IoT Edge Security Daemon</span></span>

>[!NOTE]
><span data-ttu-id="61ef4-121">Azure IoT Edge software packages are subject to the license terms located in the packages (in the LICENSE directory).</span><span class="sxs-lookup"><span data-stu-id="61ef4-121">Azure IoT Edge software packages are subject to the license terms located in the packages (in the LICENSE directory).</span></span> <span data-ttu-id="61ef4-122">Please read the license terms prior to using the package.</span><span class="sxs-lookup"><span data-stu-id="61ef4-122">Please read the license terms prior to using the package.</span></span> <span data-ttu-id="61ef4-123">Your installation and use of the package constitutes your acceptance of these terms.</span><span class="sxs-lookup"><span data-stu-id="61ef4-123">Your installation and use of the package constitutes your acceptance of these terms.</span></span> <span data-ttu-id="61ef4-124">If you do not agree with the license terms, do not use the package.</span><span class="sxs-lookup"><span data-stu-id="61ef4-124">If you do not agree with the license terms, do not use the package.</span></span>

<span data-ttu-id="61ef4-125">A single IoT Edge device can be provisioned manually using a device connections string provided by IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="61ef4-125">A single IoT Edge device can be provisioned manually using a device connections string provided by IoT Hub.</span></span> <span data-ttu-id="61ef4-126">Or, you can use the Device Provisioning Service to automatically provision devices, which is helpful when you have many devices to provision.</span><span class="sxs-lookup"><span data-stu-id="61ef4-126">Or, you can use the Device Provisioning Service to automatically provision devices, which is helpful when you have many devices to provision.</span></span> <span data-ttu-id="61ef4-127">Depending on your provisioning choice, choose the appropriate installation script.</span><span class="sxs-lookup"><span data-stu-id="61ef4-127">Depending on your provisioning choice, choose the appropriate installation script.</span></span> 

### <a name="install-and-manually-provision"></a><span data-ttu-id="61ef4-128">Install and manually provision</span><span class="sxs-lookup"><span data-stu-id="61ef4-128">Install and manually provision</span></span>

1. <span data-ttu-id="61ef4-129">Follow the steps in [Register a new Azure IoT Edge device][lnk-dcs] to register your device and retrieve the device connection string.</span><span class="sxs-lookup"><span data-stu-id="61ef4-129">Follow the steps in [Register a new Azure IoT Edge device][lnk-dcs] to register your device and retrieve the device connection string.</span></span> 

2. <span data-ttu-id="61ef4-130">On your IoT Edge device, run PowerShell as an administrator.</span><span class="sxs-lookup"><span data-stu-id="61ef4-130">On your IoT Edge device, run PowerShell as an administrator.</span></span> 

3. <span data-ttu-id="61ef4-131">Download and install the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="61ef4-131">Download and install the IoT Edge runtime.</span></span> 

   ```powershell
   . {Invoke-WebRequest -useb aka.ms/iotedge-win} | Invoke-Expression; `
   Install-SecurityDaemon -Manual -ContainerOs Windows
   ```

4. <span data-ttu-id="61ef4-132">When prompted for a **DeviceConnectionString**, provide the connection string that you retrieved from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="61ef4-132">When prompted for a **DeviceConnectionString**, provide the connection string that you retrieved from IoT Hub.</span></span> <span data-ttu-id="61ef4-133">Do not include quotes around the connection string.</span><span class="sxs-lookup"><span data-stu-id="61ef4-133">Do not include quotes around the connection string.</span></span> 

### <a name="install-and-automatically-provision"></a><span data-ttu-id="61ef4-134">Install and automatically provision</span><span class="sxs-lookup"><span data-stu-id="61ef4-134">Install and automatically provision</span></span>

1. <span data-ttu-id="61ef4-135">Follow the steps in [Create and provision a simulated TPM Edge device on Windows][lnk-dps] to set up the Device Provisioning Service and retrieve its **Scope ID**, simulate a TPM device and retrieve its **Registration ID**, then create an individual enrollment.</span><span class="sxs-lookup"><span data-stu-id="61ef4-135">Follow the steps in [Create and provision a simulated TPM Edge device on Windows][lnk-dps] to set up the Device Provisioning Service and retrieve its **Scope ID**, simulate a TPM device and retrieve its **Registration ID**, then create an individual enrollment.</span></span> <span data-ttu-id="61ef4-136">Once your device is registered in your IoT Hub, continue with the installation.</span><span class="sxs-lookup"><span data-stu-id="61ef4-136">Once your device is registered in your IoT Hub, continue with the installation.</span></span>  

   >[!TIP]
   ><span data-ttu-id="61ef4-137">Keep the window that's running the TPM simulator open during your installation and testing.</span><span class="sxs-lookup"><span data-stu-id="61ef4-137">Keep the window that's running the TPM simulator open during your installation and testing.</span></span> 

2. <span data-ttu-id="61ef4-138">On your IoT Edge device, run PowerShell as an administrator.</span><span class="sxs-lookup"><span data-stu-id="61ef4-138">On your IoT Edge device, run PowerShell as an administrator.</span></span> 

3. <span data-ttu-id="61ef4-139">Download and install the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="61ef4-139">Download and install the IoT Edge runtime.</span></span> 

   ```powershell
   . {Invoke-WebRequest -useb aka.ms/iotedge-win} | Invoke-Expression; `
   Install-SecurityDaemon -Dps -ContainerOs Windows
   ```

4. <span data-ttu-id="61ef4-140">When prompted, provide the **ScopeID** and **RegistrationID** for your provisioning service and device.</span><span class="sxs-lookup"><span data-stu-id="61ef4-140">When prompted, provide the **ScopeID** and **RegistrationID** for your provisioning service and device.</span></span> 

## <a name="verify-successful-installation"></a><span data-ttu-id="61ef4-141">Verify successful installation</span><span class="sxs-lookup"><span data-stu-id="61ef4-141">Verify successful installation</span></span>

<span data-ttu-id="61ef4-142">You can check the status of the IoT Edge service by:</span><span class="sxs-lookup"><span data-stu-id="61ef4-142">You can check the status of the IoT Edge service by:</span></span> 

```powershell
Get-Service iotedge
```

<span data-ttu-id="61ef4-143">Examine service logs for the last 5 minutes using:</span><span class="sxs-lookup"><span data-stu-id="61ef4-143">Examine service logs for the last 5 minutes using:</span></span>

```powershell

# Displays logs from last 5 min, newest at the bottom.

Get-WinEvent -ea SilentlyContinue `
  -FilterHashtable @{ProviderName= "iotedged";
    LogName = "application"; StartTime = [datetime]::Now.AddMinutes(-5)} |
  select TimeCreated, Message |
  sort-object @{Expression="TimeCreated";Descending=$false} |
  format-table -autosize -wrap
```

<span data-ttu-id="61ef4-144">And, list running modules with:</span><span class="sxs-lookup"><span data-stu-id="61ef4-144">And, list running modules with:</span></span>

```powershell
iotedge list
```

## <a name="next-steps"></a><span data-ttu-id="61ef4-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="61ef4-145">Next steps</span></span>

<span data-ttu-id="61ef4-146">Now that you have an IoT Edge device provisioned with the runtime installed, you can [deploy IoT Edge modules][lnk-modules].</span><span class="sxs-lookup"><span data-stu-id="61ef4-146">Now that you have an IoT Edge device provisioned with the runtime installed, you can [deploy IoT Edge modules][lnk-modules].</span></span>

<span data-ttu-id="61ef4-147">If you are having problems with the Edge runtime installing properly, check out the [troubleshooting][lnk-trouble] page.</span><span class="sxs-lookup"><span data-stu-id="61ef4-147">If you are having problems with the Edge runtime installing properly, check out the [troubleshooting][lnk-trouble] page.</span></span>


<!-- Images -->
[img-nat]: ./media/how-to-install-iot-edge-windows-with-windows/nat.png

<!-- Links -->
[lnk-docker-config]: https://docs.docker.com/docker-for-windows/#switch-between-windows-and-linux-containers
[lnk-dcs]: how-to-register-device-portal.md
[lnk-dps]: how-to-auto-provision-simulated-device-windows.md
[lnk-oci]: https://www.opencontainers.org/
[lnk-moby]: https://mobyproject.org/
[lnk-trouble]: troubleshoot.md
[lnk-docker-for-windows]: https://www.docker.com/docker-windows
[lnk-iot-core]: how-to-install-iot-core.md
[lnk-modules]: how-to-deploy-modules-portal.md
