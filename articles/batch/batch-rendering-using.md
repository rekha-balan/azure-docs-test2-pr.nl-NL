---
title: Azure Batch rendering
description: How to use Azure Batch rendering capabilities
services: batch
author: mscurrell
ms.author: markscu
ms.date: 08/02/2018
ms.topic: conceptual
ms.openlocfilehash: ef2abc147049d264899d227235cffe72a1a1568c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865465"
---
# <a name="using-azure-batch-rendering"></a><span data-ttu-id="6b4c5-103">Using Azure Batch rendering</span><span class="sxs-lookup"><span data-stu-id="6b4c5-103">Using Azure Batch rendering</span></span>

<span data-ttu-id="6b4c5-104">There are several ways to use Azure Batch rendering:</span><span class="sxs-lookup"><span data-stu-id="6b4c5-104">There are several ways to use Azure Batch rendering:</span></span>

* <span data-ttu-id="6b4c5-105">APIs:</span><span class="sxs-lookup"><span data-stu-id="6b4c5-105">APIs:</span></span>
  * <span data-ttu-id="6b4c5-106">Write code using any of the Batch APIs.</span><span class="sxs-lookup"><span data-stu-id="6b4c5-106">Write code using any of the Batch APIs.</span></span>  <span data-ttu-id="6b4c5-107">Developers can integrate Azure Batch capabilities into their existing applications or workflow, whether cloud or based on-premises.</span><span class="sxs-lookup"><span data-stu-id="6b4c5-107">Developers can integrate Azure Batch capabilities into their existing applications or workflow, whether cloud or based on-premises.</span></span>
* <span data-ttu-id="6b4c5-108">Command line tools:</span><span class="sxs-lookup"><span data-stu-id="6b4c5-108">Command line tools:</span></span>
  * <span data-ttu-id="6b4c5-109">The [Azure command line](https://docs.microsoft.com/cli/azure/) or [PowerShell](https://docs.microsoft.com/powershell/azure/overview) can be used to script Batch use.</span><span class="sxs-lookup"><span data-stu-id="6b4c5-109">The [Azure command line](https://docs.microsoft.com/cli/azure/) or [PowerShell](https://docs.microsoft.com/powershell/azure/overview) can be used to script Batch use.</span></span>
  * <span data-ttu-id="6b4c5-110">In particular, the [Batch CLI template support](https://docs.microsoft.com/azure/batch/batch-cli-templates) makes it much easier to create pools and submit jobs.</span><span class="sxs-lookup"><span data-stu-id="6b4c5-110">In particular, the [Batch CLI template support](https://docs.microsoft.com/azure/batch/batch-cli-templates) makes it much easier to create pools and submit jobs.</span></span>
* <span data-ttu-id="6b4c5-111">Batch Explorer UI:</span><span class="sxs-lookup"><span data-stu-id="6b4c5-111">Batch Explorer UI:</span></span>
  * <span data-ttu-id="6b4c5-112">[Batch Explorer](https://github.com/Azure/BatchLabs) is a cross-platform client tool that also allows Batch accounts to be managed and monitored.</span><span class="sxs-lookup"><span data-stu-id="6b4c5-112">[Batch Explorer](https://github.com/Azure/BatchLabs) is a cross-platform client tool that also allows Batch accounts to be managed and monitored.</span></span>
  * <span data-ttu-id="6b4c5-113">For each of the rendering applications, a number of pool and job templates are provided that can be used to easily create pools and to submit jobs.</span><span class="sxs-lookup"><span data-stu-id="6b4c5-113">For each of the rendering applications, a number of pool and job templates are provided that can be used to easily create pools and to submit jobs.</span></span>  <span data-ttu-id="6b4c5-114">A set of templates is listed in the application UI, with the template files being accessed from GitHub.</span><span class="sxs-lookup"><span data-stu-id="6b4c5-114">A set of templates is listed in the application UI, with the template files being accessed from GitHub.</span></span>
  * <span data-ttu-id="6b4c5-115">Custom templates can be authored from scratch or the supplied templates from GitHub can be copied and modified.</span><span class="sxs-lookup"><span data-stu-id="6b4c5-115">Custom templates can be authored from scratch or the supplied templates from GitHub can be copied and modified.</span></span>
* <span data-ttu-id="6b4c5-116">Client application plug-ins:</span><span class="sxs-lookup"><span data-stu-id="6b4c5-116">Client application plug-ins:</span></span>
  * <span data-ttu-id="6b4c5-117">Plug-ins are available that allow Batch rendering to be used from directly within the client design and modeling applications.</span><span class="sxs-lookup"><span data-stu-id="6b4c5-117">Plug-ins are available that allow Batch rendering to be used from directly within the client design and modeling applications.</span></span>  <span data-ttu-id="6b4c5-118">The plug-ins mainly invoke the Batch Explorer application with contextual information about the current 3D model and includes features to help manage assets.</span><span class="sxs-lookup"><span data-stu-id="6b4c5-118">The plug-ins mainly invoke the Batch Explorer application with contextual information about the current 3D model and includes features to help manage assets.</span></span>

<span data-ttu-id="6b4c5-119">The best way to try Azure Batch rendering and simplest way for end-users, who are not developers and not Azure experts, is to use the Batch Explorer application, either directly or invoked from a client application plug-in.</span><span class="sxs-lookup"><span data-stu-id="6b4c5-119">The best way to try Azure Batch rendering and simplest way for end-users, who are not developers and not Azure experts, is to use the Batch Explorer application, either directly or invoked from a client application plug-in.</span></span>

## <a name="using-batch-explorer"></a><span data-ttu-id="6b4c5-120">Using Batch Explorer</span><span class="sxs-lookup"><span data-stu-id="6b4c5-120">Using Batch Explorer</span></span>

<span data-ttu-id="6b4c5-121">For a step-by-step tutorial for using Batch Explorer to perform rendering see the [Blender tutorial](https://docs.microsoft.com/azure/batch/tutorial-rendering-batchexplorer-blender).</span><span class="sxs-lookup"><span data-stu-id="6b4c5-121">For a step-by-step tutorial for using Batch Explorer to perform rendering see the [Blender tutorial](https://docs.microsoft.com/azure/batch/tutorial-rendering-batchexplorer-blender).</span></span>

### <a name="download-and-install"></a><span data-ttu-id="6b4c5-122">Download and Install</span><span class="sxs-lookup"><span data-stu-id="6b4c5-122">Download and Install</span></span>

<span data-ttu-id="6b4c5-123">Batch Explorer [downloads are available](https://azure.github.io/BatchExplorer/) for Windows, OSX, and Linux.</span><span class="sxs-lookup"><span data-stu-id="6b4c5-123">Batch Explorer [downloads are available](https://azure.github.io/BatchExplorer/) for Windows, OSX, and Linux.</span></span>

### <a name="using-templates-to-create-pools-and-run-jobs"></a><span data-ttu-id="6b4c5-124">Using templates to create pools and run jobs</span><span class="sxs-lookup"><span data-stu-id="6b4c5-124">Using templates to create pools and run jobs</span></span>

<span data-ttu-id="6b4c5-125">A comprehensive set of templates is available for use with Batch Explorer that makes it easy to create pools and submit jobs for the various rendering applications without having to specify all the properties required to create pools, jobs, and tasks directly with Batch.</span><span class="sxs-lookup"><span data-stu-id="6b4c5-125">A comprehensive set of templates is available for use with Batch Explorer that makes it easy to create pools and submit jobs for the various rendering applications without having to specify all the properties required to create pools, jobs, and tasks directly with Batch.</span></span>  <span data-ttu-id="6b4c5-126">The templates available in Batch Explorer are stored and visible in [a GitHub repository](https://github.com/Azure/BatchExplorer-data/tree/master/ncj).</span><span class="sxs-lookup"><span data-stu-id="6b4c5-126">The templates available in Batch Explorer are stored and visible in [a GitHub repository](https://github.com/Azure/BatchExplorer-data/tree/master/ncj).</span></span>

![Batch Explorer Gallery](./media/batch-rendering-using/batch-explorer-gallery.png)

<span data-ttu-id="6b4c5-128">Templates are provided that cater for all the applications present on the Marketplace rendering VM images.</span><span class="sxs-lookup"><span data-stu-id="6b4c5-128">Templates are provided that cater for all the applications present on the Marketplace rendering VM images.</span></span>  <span data-ttu-id="6b4c5-129">For each application multiple templates exist, including pool templates to cater for CPU and GPU pools, Windows and Linux pools; job templates include full frame or tiled Blender rendering and V-Ray distributed rendering.</span><span class="sxs-lookup"><span data-stu-id="6b4c5-129">For each application multiple templates exist, including pool templates to cater for CPU and GPU pools, Windows and Linux pools; job templates include full frame or tiled Blender rendering and V-Ray distributed rendering.</span></span> <span data-ttu-id="6b4c5-130">The set of supplied templates will be expanded over time to cater for other Batch capabilities, such as pool auto-scaling.</span><span class="sxs-lookup"><span data-stu-id="6b4c5-130">The set of supplied templates will be expanded over time to cater for other Batch capabilities, such as pool auto-scaling.</span></span>

<span data-ttu-id="6b4c5-131">It's also possible for custom templates to be produced, from scratch or by modifying the supplied templates.</span><span class="sxs-lookup"><span data-stu-id="6b4c5-131">It's also possible for custom templates to be produced, from scratch or by modifying the supplied templates.</span></span> <span data-ttu-id="6b4c5-132">Custom templates can be used by selecting the ‘Local templates’ item in the ‘Gallery’ section of Batch Explorer.</span><span class="sxs-lookup"><span data-stu-id="6b4c5-132">Custom templates can be used by selecting the ‘Local templates’ item in the ‘Gallery’ section of Batch Explorer.</span></span>

### <a name="file-system-and-data-movement"></a><span data-ttu-id="6b4c5-133">File system and data movement</span><span class="sxs-lookup"><span data-stu-id="6b4c5-133">File system and data movement</span></span>

<span data-ttu-id="6b4c5-134">The ‘Data’ section in Batch Explorer allows files to be copied between a local file system and Azure Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="6b4c5-134">The ‘Data’ section in Batch Explorer allows files to be copied between a local file system and Azure Storage accounts.</span></span>

## <a name="client-application-plug-ins"></a><span data-ttu-id="6b4c5-135">Client application plug-ins</span><span class="sxs-lookup"><span data-stu-id="6b4c5-135">Client application plug-ins</span></span>

<span data-ttu-id="6b4c5-136">Plug-ins are available for some of the client applications.</span><span class="sxs-lookup"><span data-stu-id="6b4c5-136">Plug-ins are available for some of the client applications.</span></span>  <span data-ttu-id="6b4c5-137">The plug-ins allow pools and jobs to be created directly from the application or invoke Batch Explorer.</span><span class="sxs-lookup"><span data-stu-id="6b4c5-137">The plug-ins allow pools and jobs to be created directly from the application or invoke Batch Explorer.</span></span>

* [<span data-ttu-id="6b4c5-138">Blender</span><span class="sxs-lookup"><span data-stu-id="6b4c5-138">Blender</span></span>](https://github.com/Azure/azure-batch-rendering/tree/master/plugins/blender)
* [<span data-ttu-id="6b4c5-139">Autodesk 3ds Max</span><span class="sxs-lookup"><span data-stu-id="6b4c5-139">Autodesk 3ds Max</span></span>](https://github.com/Azure/azure-batch-rendering/tree/master/plugins/3ds-max)
* [<span data-ttu-id="6b4c5-140">Autodesk Maya</span><span class="sxs-lookup"><span data-stu-id="6b4c5-140">Autodesk Maya</span></span>](https://github.com/Azure/azure-batch-maya)

## <a name="next-steps"></a><span data-ttu-id="6b4c5-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="6b4c5-141">Next steps</span></span>

<span data-ttu-id="6b4c5-142">For examples of Batch rendering try out the two tutorials:</span><span class="sxs-lookup"><span data-stu-id="6b4c5-142">For examples of Batch rendering try out the two tutorials:</span></span>

* [<span data-ttu-id="6b4c5-143">Rendering using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6b4c5-143">Rendering using the Azure CLI</span></span>](https://docs.microsoft.com/azure/batch/tutorial-rendering-cli)
* [<span data-ttu-id="6b4c5-144">Rendering using Batch Explorer</span><span class="sxs-lookup"><span data-stu-id="6b4c5-144">Rendering using Batch Explorer</span></span>](https://docs.microsoft.com/azure/batch/tutorial-rendering-batchexplorer-blender)