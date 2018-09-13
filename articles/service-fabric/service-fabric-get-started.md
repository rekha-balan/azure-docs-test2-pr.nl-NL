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
# <a name="prepare-your-development-environment"></a>Prepare your development environment
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md) 
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
> 
> 

 To build and run [Azure Service Fabric applications][1] on your development machine, install the runtime, SDK, and tools. You also need to enable execution of the Windows PowerShell scripts included in the SDK.

## <a name="prerequisites"></a>Prerequisites
### <a name="supported-operating-system-versions"></a>Supported operating system versions
The following operating system versions are supported for development:

* Windows 7
* Windows 8/Windows 8.1
* Windows Server 2012 R2
* Windows Server 2016
* Windows 10

> [!NOTE]
> Windows 7 only includes Windows PowerShell 2.0 by default. Service Fabric PowerShell cmdlets requires PowerShell 3.0 or higher. You can [download Windows PowerShell 5.0][powershell5-download] from the Microsoft Download Center.
> 
> 

## <a name="install-the-sdk-and-tools"></a>Install the SDK and tools
### <a name="to-use-visual-studio-2017"></a>To use Visual Studio 2017
Service Fabric Tools are part of the Azure Development and Management workload in Visual Studio 2017. Enable this workload as part of your Visual Studio installation.
In addition, you need to install the Microsoft Azure Service Fabric SDK, using Web Platform Installer.

* [Install the Microsoft Azure Service Fabric SDK][core-sdk]

### <a name="to-use-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a>To use Visual Studio 2015 (requires Visual Studio 2015 Update 2 or later)
For Visual Studio 2015, Service Fabric tools are installed together with the SDK, using the Web Platform Installer:

* [Install the Microsoft Azure Service Fabric SDK and Tools][full-bundle-vs2015]

### <a name="sdk-installation-only"></a>SDK installation only
If you only need the SDK, you can install this package:
* [Install the Microsoft Azure Service Fabric SDK][core-sdk]

> [!WARNING]
> Customers have reported errors during installation when using these launch links, or when these links were used in Chrome browser. These errors are known issues in Web Platform Installer which are being addressed.  Try the following workarounds:
>- Launch the preceding links in Internet Explorer or Edge browsers, or
>- Launch Web Platform Installer from the Start menu, search for "Service Fabric", and install the SDK
> 
> We apologize for the inconvenience. 

The current versions are:
* Service Fabric SDK 2.5.216
* Service Fabric runtime 5.5.216
* Visual Studio 2015 tools 1.5.50311.1

For a list of supported versions, see [Service Fabric support](service-fabric-support.md)

## <a name="enable-powershell-script-execution"></a>Enable PowerShell script execution
Service Fabric uses Windows PowerShell scripts for creating a local development cluster and for deploying applications from Visual Studio. By default, Windows blocks these scripts from running. To enable them, you must modify your PowerShell execution policy. Open PowerShell as an administrator and enter the following command:

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a>Next steps
Now that you've finished setting up your development environment, start building and running apps.

* [Create your first Service Fabric application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md)
* [Learn how to deploy and manage applications on your local cluster](service-fabric-get-started-with-a-local-cluster.md)
* [Learn about the programming models: Reliable Services and Reliable Actors](service-fabric-choose-framework.md)
* [Check out the Service Fabric code samples on GitHub](https://aka.ms/servicefabricsamples)
* [Visualize your cluster by using Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)
* [Follow the Service Fabric learning path to get a broad introduction to the platform](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* Learn about [Service Fabric support options](service-fabric-support.md)

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Service Fabric campaign page"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI link"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI link"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI link"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
