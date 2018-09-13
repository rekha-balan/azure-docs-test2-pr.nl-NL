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
# <a name="install-the-iot-edge-runtime-on-windows-iot-core---preview"></a>Install the IoT Edge runtime on Windows IoT Core - preview

Azure IoT Edge and [Windows IoT Core](https://docs.microsoft.com/windows/iot-core/) work together to enable edge computing on even small devices. The Azure IoT Edge Runtime can run even on tiny Single Board Computer (SBC) devices which are very prevalent in the IoT industry. 

This article walks through provisioning the runtime on a development board running Windows IoT Core. 

**Currently, Windows IoT Core supports Azure IoT Edge only on Intel x64-based processors.**

## <a name="install-the-container-runtime"></a>Install the container runtime

1. Configure your board with **Build 17134 (RS4)** IoT Core image. 
1. Turn on the device, then [login remotely with PowerShell][lnk-powershell].
1. In the PowerShell console, install the container runtime: 

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
   >This container runtime is from the Moby project build server, and is intended for evaluation purposes only. It's not tested, endorsed, or supported by Docker.

## <a name="finish-installing"></a>Finish installing

Install the IoT Edge Security Daemon and configure it using instructions in [this article][lnk-install-windows-on-windows]

## <a name="next-steps"></a>Next steps

Now that you have a device running the IoT Edge runtime, learn how to [Deploy and monitor IoT Edge modules at scale][lnk-deploy].

<!--Links-->
[lnk-install-windows-on-windows]: how-to-install-iot-edge-windows-with-windows.md
[lnk-powershell]: https://docs.microsoft.com/windows/iot-core/connect-your-device/powershell
[lnk-deploy]: how-to-deploy-monitor.md
[lnk-docker-install]: https://docs.docker.com/engine/installation/linux/docker-ce/binaries#install-server-and-client-binaries-on-windows
[lnk-docker-containers]: https://docs.microsoft.com/virtualization/windowscontainers/quick-start/quick-start-windows-10#2-switch-to-windows-containers
