---
title: Command-line build for Azure | Microsoft Docs
description: Command-line build for Azure
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: 94b35d0d-0d35-48b6-b48b-3641377867fd
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/05/2017
ms.author: tarcher
ms.openlocfilehash: 5add8703b7b16ba8d9dc49f42f5e71b195c46653
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564174"
---
# <a name="building-azure-projects-from-the-command-line"></a><span data-ttu-id="363fc-103">Building Azure projects from the command line</span><span class="sxs-lookup"><span data-stu-id="363fc-103">Building Azure projects from the command line</span></span>
<span data-ttu-id="363fc-104">Using the Microsoft Build Engine (MSBuild), you can build products in build-lab environments where Visual Studio is not installed.</span><span class="sxs-lookup"><span data-stu-id="363fc-104">Using the Microsoft Build Engine (MSBuild), you can build products in build-lab environments where Visual Studio is not installed.</span></span> <span data-ttu-id="363fc-105">MSBuild uses an XML format for project files that's extensible and fully supported by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="363fc-105">MSBuild uses an XML format for project files that's extensible and fully supported by Microsoft.</span></span> <span data-ttu-id="363fc-106">Using the MSBuild file format, you can describe what items must be built for one or more platforms and configurations.</span><span class="sxs-lookup"><span data-stu-id="363fc-106">Using the MSBuild file format, you can describe what items must be built for one or more platforms and configurations.</span></span>

<span data-ttu-id="363fc-107">You can also run MSBuild at the command line, and this topic describes that approach.</span><span class="sxs-lookup"><span data-stu-id="363fc-107">You can also run MSBuild at the command line, and this topic describes that approach.</span></span> <span data-ttu-id="363fc-108">By setting properties on the command line, you can build specific configurations of a project.</span><span class="sxs-lookup"><span data-stu-id="363fc-108">By setting properties on the command line, you can build specific configurations of a project.</span></span> <span data-ttu-id="363fc-109">Similarly, you can also define the targets that MSBuild builds.</span><span class="sxs-lookup"><span data-stu-id="363fc-109">Similarly, you can also define the targets that MSBuild builds.</span></span> <span data-ttu-id="363fc-110">For more information about command-line parameters and MSBuild, see [MSBuild Command-Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span><span class="sxs-lookup"><span data-stu-id="363fc-110">For more information about command-line parameters and MSBuild, see [MSBuild Command-Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span></span>

## <a name="msbuild-parameters"></a><span data-ttu-id="363fc-111">MSBuild parameters</span><span class="sxs-lookup"><span data-stu-id="363fc-111">MSBuild parameters</span></span>
<span data-ttu-id="363fc-112">The simplest way to create a package is to run MSBuild with the `/t:Publish` option.</span><span class="sxs-lookup"><span data-stu-id="363fc-112">The simplest way to create a package is to run MSBuild with the `/t:Publish` option.</span></span> <span data-ttu-id="363fc-113">By default, this command creates a directory in relation to the root folder for the project, such as `<ProjectDirectory>\bin\Configuration\app.publish\`.</span><span class="sxs-lookup"><span data-stu-id="363fc-113">By default, this command creates a directory in relation to the root folder for the project, such as `<ProjectDirectory>\bin\Configuration\app.publish\`.</span></span> <span data-ttu-id="363fc-114">When you build an Azure project, two files are generated: the package file itself and the accompanying configuration file:</span><span class="sxs-lookup"><span data-stu-id="363fc-114">When you build an Azure project, two files are generated: the package file itself and the accompanying configuration file:</span></span>

* <span data-ttu-id="363fc-115">Package File (`project.cspkg`)</span><span class="sxs-lookup"><span data-stu-id="363fc-115">Package File (`project.cspkg`)</span></span>
* <span data-ttu-id="363fc-116">Configuration File (`ServiceConfiguration.TargetProfile.cscfg`)</span><span class="sxs-lookup"><span data-stu-id="363fc-116">Configuration File (`ServiceConfiguration.TargetProfile.cscfg`)</span></span>

<span data-ttu-id="363fc-117">By default, each Azure project includes one service-configuration file for local (debugging) builds and another for cloud (staging or production) builds.</span><span class="sxs-lookup"><span data-stu-id="363fc-117">By default, each Azure project includes one service-configuration file for local (debugging) builds and another for cloud (staging or production) builds.</span></span> <span data-ttu-id="363fc-118">However, you can add or remove service-configuration files as needed.</span><span class="sxs-lookup"><span data-stu-id="363fc-118">However, you can add or remove service-configuration files as needed.</span></span> <span data-ttu-id="363fc-119">When you build a package within Visual Studio, you are asked which service-configuration file to include alongside the package.</span><span class="sxs-lookup"><span data-stu-id="363fc-119">When you build a package within Visual Studio, you are asked which service-configuration file to include alongside the package.</span></span> <span data-ttu-id="363fc-120">When you build a package by using MSBuild, the local service-configuration file is included by default.</span><span class="sxs-lookup"><span data-stu-id="363fc-120">When you build a package by using MSBuild, the local service-configuration file is included by default.</span></span> <span data-ttu-id="363fc-121">To include a different service-configuration file, set the `TargetProfile` property of the MSBuild command (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).</span><span class="sxs-lookup"><span data-stu-id="363fc-121">To include a different service-configuration file, set the `TargetProfile` property of the MSBuild command (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).</span></span>

<span data-ttu-id="363fc-122">If you want to use an alternate directory for the stored package and configuration files, set the path by using the `/p:PublishDir=Directory\` option, including the trailing backslash separator.</span><span class="sxs-lookup"><span data-stu-id="363fc-122">If you want to use an alternate directory for the stored package and configuration files, set the path by using the `/p:PublishDir=Directory\` option, including the trailing backslash separator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="363fc-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="363fc-123">Next steps</span></span>
<span data-ttu-id="363fc-124">After the package is built, you can deploy it to Azure.</span><span class="sxs-lookup"><span data-stu-id="363fc-124">After the package is built, you can deploy it to Azure.</span></span> <span data-ttu-id="363fc-125">For a tutorial that demonstrates how to automate that process, see [Continuous Delivery for Cloud Services in Azure](./cloud-services/cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="363fc-125">For a tutorial that demonstrates how to automate that process, see [Continuous Delivery for Cloud Services in Azure](./cloud-services/cloud-services-dotnet-continuous-delivery.md).</span></span>

