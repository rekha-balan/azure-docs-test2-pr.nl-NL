---
title: Deploy an ASP.NET Core Linux Docker container to a remote Docker host | Microsoft Docs
description: Learn how to use Visual Studio Tools for Docker to deploy an ASP.NET Core web app to a Docker container running on an Azure Docker Host Linux VM
services: azure-container-service
documentationcenter: .net
author: mlearned
manager: douge
editor: ''
ms.assetid: e5e81c5e-dd18-4d5a-a24d-a932036e78b9
ms.service: azure-container-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 54a0c5112782df005d39ef084cb7b0176bef721b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555958"
---
# <a name="deploy-an-aspnet-container-to-a-remote-docker-host"></a>Deploy an ASP.NET container to a remote Docker host
## <a name="overview"></a>Overview
Docker is a lightweight container engine, similar in some ways to a virtual machine, which you can use to host applications and services.
This tutorial walks you through using the [Visual Studio 2015 Tools for Docker](http://aka.ms/DockerToolsForVS) extension to deploy an ASP.NET Core app to a Docker host on Azure using PowerShell.

## <a name="prerequisites"></a>Prerequisites
The following is needed to complete this tutorial:

* Create an Azure Docker Host VM as described in [How to use docker-machine with Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Install [Visual Studio 2015 Update 3](https://go.microsoft.com/fwlink/?LinkId=691129)
* [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)
* Install [Visual Studio 2015 Tools for Docker - Preview](http://aka.ms/DockerToolsForVS)

## <a name="1-create-an-aspnet-core-web-app"></a>1. Create an ASP.NET Core web app
The following steps will guide you through creating a basic ASP.NET Core app that will be used in this tutorial.

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a>2. Add Docker support
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-the-dockertaskps1-powershell-script"></a>3. Use the DockerTask.ps1 PowerShell Script
1. Open a PowerShell prompt to the root directory of your project. 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. Validate the remote host is running. You should see state = Running 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
   > [!NOTE]
   > If you're using the Docker Beta, your host won't be listed here.
   > 
   > 
3. Build the app using the -Build parameter
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  
   
   > [!NOTE]
   > If you're using the Docker Beta, omit the -Machine argument
   > 
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. Run the app, using the -Run parameter
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > [!NOTE]
   > If you're using the Docker Beta, omit the -Machine argument
   > 
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   Once docker completes, you should see results similar to the following:
   
   ![View your app][3]

[0]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png




