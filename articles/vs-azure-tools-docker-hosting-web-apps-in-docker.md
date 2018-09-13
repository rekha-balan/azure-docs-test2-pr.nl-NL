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
# <a name="deploy-an-aspnet-container-to-a-remote-docker-host"></a><span data-ttu-id="bf75c-103">Deploy an ASP.NET container to a remote Docker host</span><span class="sxs-lookup"><span data-stu-id="bf75c-103">Deploy an ASP.NET container to a remote Docker host</span></span>
## <a name="overview"></a><span data-ttu-id="bf75c-104">Overview</span><span class="sxs-lookup"><span data-stu-id="bf75c-104">Overview</span></span>
<span data-ttu-id="bf75c-105">Docker is a lightweight container engine, similar in some ways to a virtual machine, which you can use to host applications and services.</span><span class="sxs-lookup"><span data-stu-id="bf75c-105">Docker is a lightweight container engine, similar in some ways to a virtual machine, which you can use to host applications and services.</span></span>
<span data-ttu-id="bf75c-106">This tutorial walks you through using the [Visual Studio 2015 Tools for Docker](http://aka.ms/DockerToolsForVS) extension to deploy an ASP.NET Core app to a Docker host on Azure using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bf75c-106">This tutorial walks you through using the [Visual Studio 2015 Tools for Docker](http://aka.ms/DockerToolsForVS) extension to deploy an ASP.NET Core app to a Docker host on Azure using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf75c-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bf75c-107">Prerequisites</span></span>
<span data-ttu-id="bf75c-108">The following is needed to complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="bf75c-108">The following is needed to complete this tutorial:</span></span>

* <span data-ttu-id="bf75c-109">Create an Azure Docker Host VM as described in [How to use docker-machine with Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="bf75c-109">Create an Azure Docker Host VM as described in [How to use docker-machine with Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="bf75c-110">Install [Visual Studio 2015 Update 3](https://go.microsoft.com/fwlink/?LinkId=691129)</span><span class="sxs-lookup"><span data-stu-id="bf75c-110">Install [Visual Studio 2015 Update 3](https://go.microsoft.com/fwlink/?LinkId=691129)</span></span>
* [<span data-ttu-id="bf75c-111">Microsoft ASP.NET Core 1.0 SDK</span><span class="sxs-lookup"><span data-stu-id="bf75c-111">Microsoft ASP.NET Core 1.0 SDK</span></span>](https://go.microsoft.com/fwlink/?LinkID=809122)
* <span data-ttu-id="bf75c-112">Install [Visual Studio 2015 Tools for Docker - Preview](http://aka.ms/DockerToolsForVS)</span><span class="sxs-lookup"><span data-stu-id="bf75c-112">Install [Visual Studio 2015 Tools for Docker - Preview](http://aka.ms/DockerToolsForVS)</span></span>

## <a name="1-create-an-aspnet-core-web-app"></a><span data-ttu-id="bf75c-113">1. Create an ASP.NET Core web app</span><span class="sxs-lookup"><span data-stu-id="bf75c-113">1. Create an ASP.NET Core web app</span></span>
<span data-ttu-id="bf75c-114">The following steps will guide you through creating a basic ASP.NET Core app that will be used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="bf75c-114">The following steps will guide you through creating a basic ASP.NET Core app that will be used in this tutorial.</span></span>

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="bf75c-115">2. Add Docker support</span><span class="sxs-lookup"><span data-stu-id="bf75c-115">2. Add Docker support</span></span>
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-the-dockertaskps1-powershell-script"></a><span data-ttu-id="bf75c-116">3. Use the DockerTask.ps1 PowerShell Script</span><span class="sxs-lookup"><span data-stu-id="bf75c-116">3. Use the DockerTask.ps1 PowerShell Script</span></span>
1. <span data-ttu-id="bf75c-117">Open a PowerShell prompt to the root directory of your project.</span><span class="sxs-lookup"><span data-stu-id="bf75c-117">Open a PowerShell prompt to the root directory of your project.</span></span> 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. <span data-ttu-id="bf75c-118">Validate the remote host is running.</span><span class="sxs-lookup"><span data-stu-id="bf75c-118">Validate the remote host is running.</span></span> <span data-ttu-id="bf75c-119">You should see state = Running</span><span class="sxs-lookup"><span data-stu-id="bf75c-119">You should see state = Running</span></span> 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
   > [!NOTE]
   > <span data-ttu-id="bf75c-120">If you're using the Docker Beta, your host won't be listed here.</span><span class="sxs-lookup"><span data-stu-id="bf75c-120">If you're using the Docker Beta, your host won't be listed here.</span></span>
   > 
   > 
3. <span data-ttu-id="bf75c-121">Build the app using the -Build parameter</span><span class="sxs-lookup"><span data-stu-id="bf75c-121">Build the app using the -Build parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  
   
   > [!NOTE]
   > <span data-ttu-id="bf75c-122">If you're using the Docker Beta, omit the -Machine argument</span><span class="sxs-lookup"><span data-stu-id="bf75c-122">If you're using the Docker Beta, omit the -Machine argument</span></span>
   > 
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. <span data-ttu-id="bf75c-123">Run the app, using the -Run parameter</span><span class="sxs-lookup"><span data-stu-id="bf75c-123">Run the app, using the -Run parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > [!NOTE]
   > <span data-ttu-id="bf75c-124">If you're using the Docker Beta, omit the -Machine argument</span><span class="sxs-lookup"><span data-stu-id="bf75c-124">If you're using the Docker Beta, omit the -Machine argument</span></span>
   > 
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   <span data-ttu-id="bf75c-125">Once docker completes, you should see results similar to the following:</span><span class="sxs-lookup"><span data-stu-id="bf75c-125">Once docker completes, you should see results similar to the following:</span></span>
   
   ![View your app][3]

[0]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png




