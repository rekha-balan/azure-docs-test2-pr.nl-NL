---
title: Set up a Windows development environment for Azure microservices | Microsoft Docs
description: Install the runtime, SDK, and tools and create a local development cluster. After completing this setup, you will be ready to build applications on Windows.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: ''
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2018
ms.author: ryanwi
ms.openlocfilehash: a3b4e2f70622b9d25a7296393de7aac4b9c59f5f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44827138"
---
# <a name="prepare-your-development-environment-on-windows"></a><span data-ttu-id="c6684-104">Prepare your development environment on Windows</span><span class="sxs-lookup"><span data-stu-id="c6684-104">Prepare your development environment on Windows</span></span>
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md) 
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
> 
> 

<span data-ttu-id="c6684-108">To build and run [Azure Service Fabric applications][1] on your Windows development machine, install the Service Fabric runtime, SDK, and tools.</span><span class="sxs-lookup"><span data-stu-id="c6684-108">To build and run [Azure Service Fabric applications][1] on your Windows development machine, install the Service Fabric runtime, SDK, and tools.</span></span> <span data-ttu-id="c6684-109">You also need to [enable execution of the Windows PowerShell scripts](#enable-powershell-script-execution) included in the SDK.</span><span class="sxs-lookup"><span data-stu-id="c6684-109">You also need to [enable execution of the Windows PowerShell scripts](#enable-powershell-script-execution) included in the SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6684-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c6684-110">Prerequisites</span></span>
### <a name="supported-operating-system-versions"></a><span data-ttu-id="c6684-111">Supported operating system versions</span><span class="sxs-lookup"><span data-stu-id="c6684-111">Supported operating system versions</span></span>
<span data-ttu-id="c6684-112">The following operating system versions are supported for development:</span><span class="sxs-lookup"><span data-stu-id="c6684-112">The following operating system versions are supported for development:</span></span>

* <span data-ttu-id="c6684-113">Windows 7</span><span class="sxs-lookup"><span data-stu-id="c6684-113">Windows 7</span></span>
* <span data-ttu-id="c6684-114">Windows 8/Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="c6684-114">Windows 8/Windows 8.1</span></span>
* <span data-ttu-id="c6684-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="c6684-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="c6684-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="c6684-116">Windows Server 2016</span></span>
* <span data-ttu-id="c6684-117">Windows 10</span><span class="sxs-lookup"><span data-stu-id="c6684-117">Windows 10</span></span>

> [!NOTE]
> Windows 7 support:
> - Windows 7 only includes Windows PowerShell 2.0 by default. Service Fabric PowerShell cmdlets requires PowerShell 3.0 or higher. You can [download Windows PowerShell 5.0][powershell5-download] from the Microsoft Download Center.
> - Service Fabric Reverse Proxy is not available on Windows 7.
>

## <a name="install-the-sdk-and-tools"></a><span data-ttu-id="c6684-123">Install the SDK and tools</span><span class="sxs-lookup"><span data-stu-id="c6684-123">Install the SDK and tools</span></span>
### <a name="to-use-visual-studio-2017"></a><span data-ttu-id="c6684-124">To use Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c6684-124">To use Visual Studio 2017</span></span>
<span data-ttu-id="c6684-125">The Service Fabric Tools are part of the Azure Development workload in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c6684-125">The Service Fabric Tools are part of the Azure Development workload in Visual Studio 2017.</span></span> <span data-ttu-id="c6684-126">Enable this workload as part of your Visual Studio installation.</span><span class="sxs-lookup"><span data-stu-id="c6684-126">Enable this workload as part of your Visual Studio installation.</span></span>
<span data-ttu-id="c6684-127">In addition, you need to install the Microsoft Azure Service Fabric SDK and runtime using Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="c6684-127">In addition, you need to install the Microsoft Azure Service Fabric SDK and runtime using Web Platform Installer.</span></span>

* <span data-ttu-id="c6684-128">[Install the Microsoft Azure Service Fabric SDK][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="c6684-128">[Install the Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

### <a name="to-use-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a><span data-ttu-id="c6684-129">To use Visual Studio 2015 (requires Visual Studio 2015 Update 2 or later)</span><span class="sxs-lookup"><span data-stu-id="c6684-129">To use Visual Studio 2015 (requires Visual Studio 2015 Update 2 or later)</span></span>
<span data-ttu-id="c6684-130">For Visual Studio 2015, the Service Fabric tools are installed together with the SDK and runtime using the Web Platform Installer:</span><span class="sxs-lookup"><span data-stu-id="c6684-130">For Visual Studio 2015, the Service Fabric tools are installed together with the SDK and runtime using the Web Platform Installer:</span></span>

* <span data-ttu-id="c6684-131">[Install the Microsoft Azure Service Fabric SDK and Tools][full-bundle-vs2015]</span><span class="sxs-lookup"><span data-stu-id="c6684-131">[Install the Microsoft Azure Service Fabric SDK and Tools][full-bundle-vs2015]</span></span>

### <a name="sdk-installation-only"></a><span data-ttu-id="c6684-132">SDK installation only</span><span class="sxs-lookup"><span data-stu-id="c6684-132">SDK installation only</span></span>
<span data-ttu-id="c6684-133">If you only need the SDK, you can install this package:</span><span class="sxs-lookup"><span data-stu-id="c6684-133">If you only need the SDK, you can install this package:</span></span>
* <span data-ttu-id="c6684-134">[Install the Microsoft Azure Service Fabric SDK][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="c6684-134">[Install the Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

<span data-ttu-id="c6684-135">The current versions are:</span><span class="sxs-lookup"><span data-stu-id="c6684-135">The current versions are:</span></span>
* <span data-ttu-id="c6684-136">Service Fabric SDK and Tools 3.2.176</span><span class="sxs-lookup"><span data-stu-id="c6684-136">Service Fabric SDK and Tools 3.2.176</span></span>
* <span data-ttu-id="c6684-137">Service Fabric runtime 6.3.176</span><span class="sxs-lookup"><span data-stu-id="c6684-137">Service Fabric runtime 6.3.176</span></span>
* <span data-ttu-id="c6684-138">Service Fabric Tools for Visual Studio 2015 2.3.10710.3</span><span class="sxs-lookup"><span data-stu-id="c6684-138">Service Fabric Tools for Visual Studio 2015 2.3.10710.3</span></span>
* <span data-ttu-id="c6684-139">Visual Studio 2017 15.7 includes Service Fabric Tools for Visual Studio 2.3.10710.1</span><span class="sxs-lookup"><span data-stu-id="c6684-139">Visual Studio 2017 15.7 includes Service Fabric Tools for Visual Studio 2.3.10710.1</span></span> 

<span data-ttu-id="c6684-140">For a list of supported versions, see [Service Fabric support](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="c6684-140">For a list of supported versions, see [Service Fabric support](service-fabric-support.md)</span></span>

> [!NOTE]
> Single machine clusters (OneBox) are not supported for Application or Cluster upgrades; delete the OneBox cluster and recreate it if you need to perform a Cluster upgrade, or have any issues performing an Application upgrade. 

## <a name="enable-powershell-script-execution"></a><span data-ttu-id="c6684-142">Enable PowerShell script execution</span><span class="sxs-lookup"><span data-stu-id="c6684-142">Enable PowerShell script execution</span></span>
<span data-ttu-id="c6684-143">Service Fabric uses Windows PowerShell scripts for creating a local development cluster and for deploying applications from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c6684-143">Service Fabric uses Windows PowerShell scripts for creating a local development cluster and for deploying applications from Visual Studio.</span></span> <span data-ttu-id="c6684-144">By default, Windows blocks these scripts from running.</span><span class="sxs-lookup"><span data-stu-id="c6684-144">By default, Windows blocks these scripts from running.</span></span> <span data-ttu-id="c6684-145">To enable them, you must modify your PowerShell execution policy.</span><span class="sxs-lookup"><span data-stu-id="c6684-145">To enable them, you must modify your PowerShell execution policy.</span></span> <span data-ttu-id="c6684-146">Open PowerShell as an administrator and enter the following command:</span><span class="sxs-lookup"><span data-stu-id="c6684-146">Open PowerShell as an administrator and enter the following command:</span></span>

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```
## <a name="install-docker-optional"></a><span data-ttu-id="c6684-147">Install Docker (optional)</span><span class="sxs-lookup"><span data-stu-id="c6684-147">Install Docker (optional)</span></span>
<span data-ttu-id="c6684-148">[Service Fabric is a container orchestrator](service-fabric-containers-overview.md) for deploying microservices across a cluster of machines.</span><span class="sxs-lookup"><span data-stu-id="c6684-148">[Service Fabric is a container orchestrator](service-fabric-containers-overview.md) for deploying microservices across a cluster of machines.</span></span> <span data-ttu-id="c6684-149">To run Windows container applications on your local development cluster, you must first install Docker for Windows.</span><span class="sxs-lookup"><span data-stu-id="c6684-149">To run Windows container applications on your local development cluster, you must first install Docker for Windows.</span></span> <span data-ttu-id="c6684-150">Get [Docker CE for Windows (stable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span><span class="sxs-lookup"><span data-stu-id="c6684-150">Get [Docker CE for Windows (stable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span></span> <span data-ttu-id="c6684-151">After installing and starting Docker, right-click on the tray icon and select **Switch to Windows containers**.</span><span class="sxs-lookup"><span data-stu-id="c6684-151">After installing and starting Docker, right-click on the tray icon and select **Switch to Windows containers**.</span></span> <span data-ttu-id="c6684-152">This step is required to run Docker images based on Windows.</span><span class="sxs-lookup"><span data-stu-id="c6684-152">This step is required to run Docker images based on Windows.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6684-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="c6684-153">Next steps</span></span>
<span data-ttu-id="c6684-154">Now that you've finished setting up your development environment, start building and running apps.</span><span class="sxs-lookup"><span data-stu-id="c6684-154">Now that you've finished setting up your development environment, start building and running apps.</span></span>

* [<span data-ttu-id="c6684-155">Create your first Service Fabric application in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c6684-155">Create your first Service Fabric application in Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
* [<span data-ttu-id="c6684-156">Learn how to deploy and manage applications on your local cluster</span><span class="sxs-lookup"><span data-stu-id="c6684-156">Learn how to deploy and manage applications on your local cluster</span></span>](service-fabric-get-started-with-a-local-cluster.md)
* [<span data-ttu-id="c6684-157">Learn about the programming models: Reliable Services and Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="c6684-157">Learn about the programming models: Reliable Services and Reliable Actors</span></span>](service-fabric-choose-framework.md)
* [<span data-ttu-id="c6684-158">Check out the Service Fabric code samples on GitHub</span><span class="sxs-lookup"><span data-stu-id="c6684-158">Check out the Service Fabric code samples on GitHub</span></span>](https://aka.ms/servicefabricsamples)
* [<span data-ttu-id="c6684-159">Visualize your cluster by using Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="c6684-159">Visualize your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)
* [<span data-ttu-id="c6684-160">Follow the Service Fabric learning path to get a broad introduction to the platform</span><span class="sxs-lookup"><span data-stu-id="c6684-160">Follow the Service Fabric learning path to get a broad introduction to the platform</span></span>](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* <span data-ttu-id="c6684-161">Learn about [Service Fabric support options](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="c6684-161">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

[1]: http://azure.microsoft.com/campaigns/service-fabric/ "Service Fabric campaign page"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI link"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI link"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI link"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
