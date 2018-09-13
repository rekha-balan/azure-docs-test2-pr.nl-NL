---
title: Install Azure IoT Edge on IoT Core | Microsoft Docs
description: Install the Azure IoT Edge runtime on a Windows IoT Core device
author: kgremban
manager: timlt
ms.author: kgremban
ms.reviewer: veyalla
ms.date: 03/05/2018
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: f57db00894dab80f96f45111331d47a173520ced
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968493"
---
# <a name="install-the-iot-edge-runtime-on-windows-iot-core---preview"></a><span data-ttu-id="76e87-103">Install the IoT Edge runtime on Windows IoT Core - preview</span><span class="sxs-lookup"><span data-stu-id="76e87-103">Install the IoT Edge runtime on Windows IoT Core - preview</span></span>

<span data-ttu-id="76e87-104">Azure IoT Edge and [Windows IoT Core](https://docs.microsoft.com/windows/iot-core/) work together to enable edge computing on even small devices.</span><span class="sxs-lookup"><span data-stu-id="76e87-104">Azure IoT Edge and [Windows IoT Core](https://docs.microsoft.com/windows/iot-core/) work together to enable edge computing on even small devices.</span></span> <span data-ttu-id="76e87-105">The Azure IoT Edge Runtime can run even on tiny Single Board Computer (SBC) devices which are very prevalent in the IoT industry.</span><span class="sxs-lookup"><span data-stu-id="76e87-105">The Azure IoT Edge Runtime can run even on tiny Single Board Computer (SBC) devices which are very prevalent in the IoT industry.</span></span> 

<span data-ttu-id="76e87-106">This article walks through provisioning the runtime on a development board running Windows IoT Core.</span><span class="sxs-lookup"><span data-stu-id="76e87-106">This article walks through provisioning the runtime on a development board running Windows IoT Core.</span></span> 

<span data-ttu-id="76e87-107">**Currently, Windows IoT Core supports Azure IoT Edge only on Intel x64-based processors.**</span><span class="sxs-lookup"><span data-stu-id="76e87-107">**Currently, Windows IoT Core supports Azure IoT Edge only on Intel x64-based processors.**</span></span>

## <a name="install-the-container-runtime"></a><span data-ttu-id="76e87-108">Install the container runtime</span><span class="sxs-lookup"><span data-stu-id="76e87-108">Install the container runtime</span></span>

1. <span data-ttu-id="76e87-109">Configure your board with **Build 17134 (RS4)** IoT Core image.</span><span class="sxs-lookup"><span data-stu-id="76e87-109">Configure your board with **Build 17134 (RS4)** IoT Core image.</span></span> 
1. <span data-ttu-id="76e87-110">Turn on the device, then [login remotely with PowerShell][lnk-powershell].</span><span class="sxs-lookup"><span data-stu-id="76e87-110">Turn on the device, then [login remotely with PowerShell][lnk-powershell].</span></span>
1. <span data-ttu-id="76e87-111">In the PowerShell console, install the container runtime:</span><span class="sxs-lookup"><span data-stu-id="76e87-111">In the PowerShell console, install the container runtime:</span></span> 

   ```powershell
   Invoke-WebRequest https://master.dockerproject.org/windows/x86_64/docker-0.0.0-dev.zip -o temp.zip
   Expand-Archive .\temp.zip $env:ProgramFiles -f
   Remove-Item .\temp.zip
   $env:Path += ";$env:programfiles\docker"
   SETX /M PATH "$env:Path"
   dockerd --register-service
   start-service docker
   ```

   >[!NOTE]
   ><span data-ttu-id="76e87-112">This container runtime is from the Moby project build server, and is intended for evaluation purposes only.</span><span class="sxs-lookup"><span data-stu-id="76e87-112">This container runtime is from the Moby project build server, and is intended for evaluation purposes only.</span></span> <span data-ttu-id="76e87-113">It's not tested, endorsed, or supported by Docker.</span><span class="sxs-lookup"><span data-stu-id="76e87-113">It's not tested, endorsed, or supported by Docker.</span></span>

## <a name="finish-installing"></a><span data-ttu-id="76e87-114">Finish installing</span><span class="sxs-lookup"><span data-stu-id="76e87-114">Finish installing</span></span>

<span data-ttu-id="76e87-115">Install the IoT Edge Security Daemon and configure it using instructions in [this article][lnk-install-windows-on-windows]</span><span class="sxs-lookup"><span data-stu-id="76e87-115">Install the IoT Edge Security Daemon and configure it using instructions in [this article][lnk-install-windows-on-windows]</span></span>

## <a name="next-steps"></a><span data-ttu-id="76e87-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="76e87-116">Next steps</span></span>

<span data-ttu-id="76e87-117">Now that you have a device running the IoT Edge runtime, learn how to [Deploy and monitor IoT Edge modules at scale][lnk-deploy].</span><span class="sxs-lookup"><span data-stu-id="76e87-117">Now that you have a device running the IoT Edge runtime, learn how to [Deploy and monitor IoT Edge modules at scale][lnk-deploy].</span></span>

<!--Links-->
[lnk-install-windows-on-windows]: how-to-install-iot-edge-windows-with-windows.md
[lnk-powershell]: https://docs.microsoft.com/windows/iot-core/connect-your-device/powershell
[lnk-deploy]: how-to-deploy-monitor.md
[lnk-docker-install]: https://docs.docker.com/engine/installation/linux/docker-ce/binaries#install-server-and-client-binaries-on-windows
[lnk-docker-containers]: https://docs.microsoft.com/virtualization/windowscontainers/quick-start/quick-start-windows-10#2-switch-to-windows-containers
