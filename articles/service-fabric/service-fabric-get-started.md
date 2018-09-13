---
title: Set up a development environment for Azure microservices | Microsoft Docs
description: Install the runtime, SDK, and tools and create a local development cluster. After completing this setup, you will be ready to build applications.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: ''
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/22/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: aeda2cfeee5a97c0b1264c0ed6d2fd066b2b7442
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553206"
---
# <a name="prepare-your-development-environment"></a><span data-ttu-id="28a2a-104">Prepare your development environment</span><span class="sxs-lookup"><span data-stu-id="28a2a-104">Prepare your development environment</span></span>
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md) 
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
> 
> 

 <span data-ttu-id="28a2a-108">To build and run [Azure Service Fabric applications][1] on your development machine, install the runtime, SDK, and tools.</span><span class="sxs-lookup"><span data-stu-id="28a2a-108">To build and run [Azure Service Fabric applications][1] on your development machine, install the runtime, SDK, and tools.</span></span> <span data-ttu-id="28a2a-109">You also need to enable execution of the Windows PowerShell scripts included in the SDK.</span><span class="sxs-lookup"><span data-stu-id="28a2a-109">You also need to enable execution of the Windows PowerShell scripts included in the SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28a2a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="28a2a-110">Prerequisites</span></span>
### <a name="supported-operating-system-versions"></a><span data-ttu-id="28a2a-111">Supported operating system versions</span><span class="sxs-lookup"><span data-stu-id="28a2a-111">Supported operating system versions</span></span>
<span data-ttu-id="28a2a-112">The following operating system versions are supported for development:</span><span class="sxs-lookup"><span data-stu-id="28a2a-112">The following operating system versions are supported for development:</span></span>

* <span data-ttu-id="28a2a-113">Windows 7</span><span class="sxs-lookup"><span data-stu-id="28a2a-113">Windows 7</span></span>
* <span data-ttu-id="28a2a-114">Windows 8/Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="28a2a-114">Windows 8/Windows 8.1</span></span>
* <span data-ttu-id="28a2a-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="28a2a-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="28a2a-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="28a2a-116">Windows Server 2016</span></span>
* <span data-ttu-id="28a2a-117">Windows 10</span><span class="sxs-lookup"><span data-stu-id="28a2a-117">Windows 10</span></span>

> [!NOTE]
> Windows 7 only includes Windows PowerShell 2.0 by default. Service Fabric PowerShell cmdlets requires PowerShell 3.0 or higher. You can [download Windows PowerShell 5.0][powershell5-download] from the Microsoft Download Center.
> 
> 

## <a name="install-the-sdk-and-tools"></a><span data-ttu-id="28a2a-121">Install the SDK and tools</span><span class="sxs-lookup"><span data-stu-id="28a2a-121">Install the SDK and tools</span></span>
### <a name="to-use-visual-studio-2017"></a><span data-ttu-id="28a2a-122">To use Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="28a2a-122">To use Visual Studio 2017</span></span>
<span data-ttu-id="28a2a-123">Service Fabric Tools are part of the Azure Development and Management workload in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="28a2a-123">Service Fabric Tools are part of the Azure Development and Management workload in Visual Studio 2017.</span></span> <span data-ttu-id="28a2a-124">Enable this workload as part of your Visual Studio installation.</span><span class="sxs-lookup"><span data-stu-id="28a2a-124">Enable this workload as part of your Visual Studio installation.</span></span>
<span data-ttu-id="28a2a-125">In addition, you need to install the Microsoft Azure Service Fabric SDK, using Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="28a2a-125">In addition, you need to install the Microsoft Azure Service Fabric SDK, using Web Platform Installer.</span></span>

* <span data-ttu-id="28a2a-126">[Install the Microsoft Azure Service Fabric SDK][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="28a2a-126">[Install the Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

### <a name="to-use-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a><span data-ttu-id="28a2a-127">To use Visual Studio 2015 (requires Visual Studio 2015 Update 2 or later)</span><span class="sxs-lookup"><span data-stu-id="28a2a-127">To use Visual Studio 2015 (requires Visual Studio 2015 Update 2 or later)</span></span>
<span data-ttu-id="28a2a-128">For Visual Studio 2015, Service Fabric tools are installed together with the SDK, using the Web Platform Installer:</span><span class="sxs-lookup"><span data-stu-id="28a2a-128">For Visual Studio 2015, Service Fabric tools are installed together with the SDK, using the Web Platform Installer:</span></span>

* <span data-ttu-id="28a2a-129">[Install the Microsoft Azure Service Fabric SDK and Tools][full-bundle-vs2015]</span><span class="sxs-lookup"><span data-stu-id="28a2a-129">[Install the Microsoft Azure Service Fabric SDK and Tools][full-bundle-vs2015]</span></span>

### <a name="sdk-installation-only"></a><span data-ttu-id="28a2a-130">SDK installation only</span><span class="sxs-lookup"><span data-stu-id="28a2a-130">SDK installation only</span></span>
<span data-ttu-id="28a2a-131">If you only need the SDK, you can install this package:</span><span class="sxs-lookup"><span data-stu-id="28a2a-131">If you only need the SDK, you can install this package:</span></span>
* <span data-ttu-id="28a2a-132">[Install the Microsoft Azure Service Fabric SDK][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="28a2a-132">[Install the Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

> [!WARNING]
> Customers have reported errors during installation when using these launch links, or when these links were used in Chrome browser. These errors are known issues in Web Platform Installer which are being addressed.  Try the following workarounds:
>- Launch the preceding links in Internet Explorer or Edge browsers, or
>- Launch Web Platform Installer from the Start menu, search for "Service Fabric", and install the SDK
> 
> We apologize for the inconvenience. 

<span data-ttu-id="28a2a-139">The current versions are:</span><span class="sxs-lookup"><span data-stu-id="28a2a-139">The current versions are:</span></span>
* <span data-ttu-id="28a2a-140">Service Fabric SDK 2.5.216</span><span class="sxs-lookup"><span data-stu-id="28a2a-140">Service Fabric SDK 2.5.216</span></span>
* <span data-ttu-id="28a2a-141">Service Fabric runtime 5.5.216</span><span class="sxs-lookup"><span data-stu-id="28a2a-141">Service Fabric runtime 5.5.216</span></span>
* <span data-ttu-id="28a2a-142">Visual Studio 2015 tools 1.5.50311.1</span><span class="sxs-lookup"><span data-stu-id="28a2a-142">Visual Studio 2015 tools 1.5.50311.1</span></span>

<span data-ttu-id="28a2a-143">For a list of supported versions, see [Service Fabric support](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="28a2a-143">For a list of supported versions, see [Service Fabric support](service-fabric-support.md)</span></span>

## <a name="enable-powershell-script-execution"></a><span data-ttu-id="28a2a-144">Enable PowerShell script execution</span><span class="sxs-lookup"><span data-stu-id="28a2a-144">Enable PowerShell script execution</span></span>
<span data-ttu-id="28a2a-145">Service Fabric uses Windows PowerShell scripts for creating a local development cluster and for deploying applications from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="28a2a-145">Service Fabric uses Windows PowerShell scripts for creating a local development cluster and for deploying applications from Visual Studio.</span></span> <span data-ttu-id="28a2a-146">By default, Windows blocks these scripts from running.</span><span class="sxs-lookup"><span data-stu-id="28a2a-146">By default, Windows blocks these scripts from running.</span></span> <span data-ttu-id="28a2a-147">To enable them, you must modify your PowerShell execution policy.</span><span class="sxs-lookup"><span data-stu-id="28a2a-147">To enable them, you must modify your PowerShell execution policy.</span></span> <span data-ttu-id="28a2a-148">Open PowerShell as an administrator and enter the following command:</span><span class="sxs-lookup"><span data-stu-id="28a2a-148">Open PowerShell as an administrator and enter the following command:</span></span>

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a><span data-ttu-id="28a2a-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="28a2a-149">Next steps</span></span>
<span data-ttu-id="28a2a-150">Now that you've finished setting up your development environment, start building and running apps.</span><span class="sxs-lookup"><span data-stu-id="28a2a-150">Now that you've finished setting up your development environment, start building and running apps.</span></span>

* [<span data-ttu-id="28a2a-151">Create your first Service Fabric application in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="28a2a-151">Create your first Service Fabric application in Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
* [<span data-ttu-id="28a2a-152">Learn how to deploy and manage applications on your local cluster</span><span class="sxs-lookup"><span data-stu-id="28a2a-152">Learn how to deploy and manage applications on your local cluster</span></span>](service-fabric-get-started-with-a-local-cluster.md)
* [<span data-ttu-id="28a2a-153">Learn about the programming models: Reliable Services and Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="28a2a-153">Learn about the programming models: Reliable Services and Reliable Actors</span></span>](service-fabric-choose-framework.md)
* [<span data-ttu-id="28a2a-154">Check out the Service Fabric code samples on GitHub</span><span class="sxs-lookup"><span data-stu-id="28a2a-154">Check out the Service Fabric code samples on GitHub</span></span>](https://aka.ms/servicefabricsamples)
* [<span data-ttu-id="28a2a-155">Visualize your cluster by using Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="28a2a-155">Visualize your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)
* [<span data-ttu-id="28a2a-156">Follow the Service Fabric learning path to get a broad introduction to the platform</span><span class="sxs-lookup"><span data-stu-id="28a2a-156">Follow the Service Fabric learning path to get a broad introduction to the platform</span></span>](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* <span data-ttu-id="28a2a-157">Learn about [Service Fabric support options](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="28a2a-157">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Service Fabric campaign page"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI link"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI link"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI link"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
