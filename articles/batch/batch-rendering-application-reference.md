---
title: Use rendering applications with Azure Batch
description: How to use rendering applications with Azure Batch
services: batch
author: mscurrell
ms.author: markscu
ms.date: 08/02/2018
ms.topic: conceptual
ms.openlocfilehash: 500246dc98618aead11ba539ce4485d25ac62941
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870585"
---
# <a name="rendering-applications"></a><span data-ttu-id="e299e-103">Rendering applications</span><span class="sxs-lookup"><span data-stu-id="e299e-103">Rendering applications</span></span>

<span data-ttu-id="e299e-104">Rendering applications are used by creating Batch jobs and tasks.</span><span class="sxs-lookup"><span data-stu-id="e299e-104">Rendering applications are used by creating Batch jobs and tasks.</span></span> <span data-ttu-id="e299e-105">The task command line property specifies the appropriate command line and parameters.</span><span class="sxs-lookup"><span data-stu-id="e299e-105">The task command line property specifies the appropriate command line and parameters.</span></span>  <span data-ttu-id="e299e-106">The easiest way to create the job tasks is to use the Batch Explorer templates as specified in [this article](https://docs.microsoft.com/azure/batch/batch-rendering-using#using-batch-explorer).</span><span class="sxs-lookup"><span data-stu-id="e299e-106">The easiest way to create the job tasks is to use the Batch Explorer templates as specified in [this article](https://docs.microsoft.com/azure/batch/batch-rendering-using#using-batch-explorer).</span></span>  <span data-ttu-id="e299e-107">The templates can be viewed and modified versions created if necessary.</span><span class="sxs-lookup"><span data-stu-id="e299e-107">The templates can be viewed and modified versions created if necessary.</span></span>

<span data-ttu-id="e299e-108">This article provides a brief description of how to run each rendering application.</span><span class="sxs-lookup"><span data-stu-id="e299e-108">This article provides a brief description of how to run each rendering application.</span></span>

## <a name="rendering-with-autodesk-3ds-max"></a><span data-ttu-id="e299e-109">Rendering with Autodesk 3ds Max</span><span class="sxs-lookup"><span data-stu-id="e299e-109">Rendering with Autodesk 3ds Max</span></span>

### <a name="renderer-support"></a><span data-ttu-id="e299e-110">Renderer support</span><span class="sxs-lookup"><span data-stu-id="e299e-110">Renderer support</span></span>

<span data-ttu-id="e299e-111">In addition to the renderers built into 3ds Max, the following renderers are available on the rendering VM images and can be referenced by the 3ds Max scene file:</span><span class="sxs-lookup"><span data-stu-id="e299e-111">In addition to the renderers built into 3ds Max, the following renderers are available on the rendering VM images and can be referenced by the 3ds Max scene file:</span></span>

* <span data-ttu-id="e299e-112">Autodesk Arnold</span><span class="sxs-lookup"><span data-stu-id="e299e-112">Autodesk Arnold</span></span>
* <span data-ttu-id="e299e-113">Chaos Group V-Ray</span><span class="sxs-lookup"><span data-stu-id="e299e-113">Chaos Group V-Ray</span></span>

### <a name="task-command-line"></a><span data-ttu-id="e299e-114">Task command line</span><span class="sxs-lookup"><span data-stu-id="e299e-114">Task command line</span></span>

<span data-ttu-id="e299e-115">Invoke the `3dsmaxcmdio.exe` application to perform command line rendering on a pool node.</span><span class="sxs-lookup"><span data-stu-id="e299e-115">Invoke the `3dsmaxcmdio.exe` application to perform command line rendering on a pool node.</span></span>  <span data-ttu-id="e299e-116">This application is on the path when the task is run.</span><span class="sxs-lookup"><span data-stu-id="e299e-116">This application is on the path when the task is run.</span></span> <span data-ttu-id="e299e-117">The `3dsmaxcmdio.exe` application has the same available parameters as the `3dsmaxcmd.exe` application, which is documented in the [3ds Max help documentation](https://help.autodesk.com/view/3DSMAX/2018/ENU/) (Rendering | Command-Line Rendering section).</span><span class="sxs-lookup"><span data-stu-id="e299e-117">The `3dsmaxcmdio.exe` application has the same available parameters as the `3dsmaxcmd.exe` application, which is documented in the [3ds Max help documentation](https://help.autodesk.com/view/3DSMAX/2018/ENU/) (Rendering | Command-Line Rendering section).</span></span>

<span data-ttu-id="e299e-118">For example:</span><span class="sxs-lookup"><span data-stu-id="e299e-118">For example:</span></span>

```
3dsmaxcmdio.exe -v:5 -rfw:0 -start:{0} -end:{0} -bitmapPath:"%AZ_BATCH_JOB_PREP_WORKING_DIR%\sceneassets\images" -outputName:dragon.jpg -w:1280 -h:720 "%AZ_BATCH_JOB_PREP_WORKING_DIR%\scenes\dragon.max"
```

<span data-ttu-id="e299e-119">Notes:</span><span class="sxs-lookup"><span data-stu-id="e299e-119">Notes:</span></span>

* <span data-ttu-id="e299e-120">Great care must be taken to ensure the asset files are found.</span><span class="sxs-lookup"><span data-stu-id="e299e-120">Great care must be taken to ensure the asset files are found.</span></span>  <span data-ttu-id="e299e-121">Ensure the paths are correct and relative using the **Asset Tracking** window, or use the `-bitmapPath` parameter on the command line.</span><span class="sxs-lookup"><span data-stu-id="e299e-121">Ensure the paths are correct and relative using the **Asset Tracking** window, or use the `-bitmapPath` parameter on the command line.</span></span>
* <span data-ttu-id="e299e-122">See if there are issues with the render, such as inability to find assets, by checking the `stdout.txt` file written by 3ds Max when the task is run.</span><span class="sxs-lookup"><span data-stu-id="e299e-122">See if there are issues with the render, such as inability to find assets, by checking the `stdout.txt` file written by 3ds Max when the task is run.</span></span>

### <a name="batch-explorer-templates"></a><span data-ttu-id="e299e-123">Batch Explorer templates</span><span class="sxs-lookup"><span data-stu-id="e299e-123">Batch Explorer templates</span></span>

<span data-ttu-id="e299e-124">Pool and job templates can be accessed from the **Gallery** in Batch Explorer.</span><span class="sxs-lookup"><span data-stu-id="e299e-124">Pool and job templates can be accessed from the **Gallery** in Batch Explorer.</span></span>  <span data-ttu-id="e299e-125">The template source files are available in the [Batch Explorer data repository on GitHub](https://github.com/Azure/BatchExplorer-data/tree/master/ncj/3dsmax).</span><span class="sxs-lookup"><span data-stu-id="e299e-125">The template source files are available in the [Batch Explorer data repository on GitHub](https://github.com/Azure/BatchExplorer-data/tree/master/ncj/3dsmax).</span></span>

## <a name="rendering-with-autodesk-maya"></a><span data-ttu-id="e299e-126">Rendering with Autodesk Maya</span><span class="sxs-lookup"><span data-stu-id="e299e-126">Rendering with Autodesk Maya</span></span>

### <a name="renderer-support"></a><span data-ttu-id="e299e-127">Renderer support</span><span class="sxs-lookup"><span data-stu-id="e299e-127">Renderer support</span></span>

<span data-ttu-id="e299e-128">In addition to the renderers built into Maya, the following renderers are available on the rendering VM images and can be referenced by the 3ds Max scene file:</span><span class="sxs-lookup"><span data-stu-id="e299e-128">In addition to the renderers built into Maya, the following renderers are available on the rendering VM images and can be referenced by the 3ds Max scene file:</span></span>

* <span data-ttu-id="e299e-129">Autodesk Arnold</span><span class="sxs-lookup"><span data-stu-id="e299e-129">Autodesk Arnold</span></span>
* <span data-ttu-id="e299e-130">Chaos Group V-Ray</span><span class="sxs-lookup"><span data-stu-id="e299e-130">Chaos Group V-Ray</span></span>

### <a name="task-command-line"></a><span data-ttu-id="e299e-131">Task command line</span><span class="sxs-lookup"><span data-stu-id="e299e-131">Task command line</span></span>

<span data-ttu-id="e299e-132">The `renderer.exe` command-line renderer is used in the task command line.</span><span class="sxs-lookup"><span data-stu-id="e299e-132">The `renderer.exe` command-line renderer is used in the task command line.</span></span> <span data-ttu-id="e299e-133">The command-line renderer is documented in [Maya help](http://help.autodesk.com/view/MAYAUL/2018/ENU/?guid=GUID-EB558BC0-5C2B-439C-9B00-F97BCB9688E4).</span><span class="sxs-lookup"><span data-stu-id="e299e-133">The command-line renderer is documented in [Maya help](http://help.autodesk.com/view/MAYAUL/2018/ENU/?guid=GUID-EB558BC0-5C2B-439C-9B00-F97BCB9688E4).</span></span>

<span data-ttu-id="e299e-134">In the following example, a job preparation task is used to copy the scene files and assets to the job preparation working directory, an output folder is used to store the rendering image, and frame 10 is rendered.</span><span class="sxs-lookup"><span data-stu-id="e299e-134">In the following example, a job preparation task is used to copy the scene files and assets to the job preparation working directory, an output folder is used to store the rendering image, and frame 10 is rendered.</span></span>

```
render -renderer sw -proj "%AZ_BATCH_JOB_PREP_WORKING_DIR%" -verb -rd "%AZ_BATCH_TASK_WORKING_DIR%\output" -s 10 -e 10 -x 1920 -y 1080 "%AZ_BATCH_JOB_PREP_WORKING_DIR%\scene-file.ma"
```

<span data-ttu-id="e299e-135">For V-Ray rendering, the Maya scene file would normally specify V-Ray as the renderer.</span><span class="sxs-lookup"><span data-stu-id="e299e-135">For V-Ray rendering, the Maya scene file would normally specify V-Ray as the renderer.</span></span>  <span data-ttu-id="e299e-136">It can also be specified on the command line:</span><span class="sxs-lookup"><span data-stu-id="e299e-136">It can also be specified on the command line:</span></span>

```
render -renderer vray -proj "%AZ_BATCH_JOB_PREP_WORKING_DIR%" -verb -rd "%AZ_BATCH_TASK_WORKING_DIR%\output" -s 10 -e 10 -x 1920 -y 1080 "%AZ_BATCH_JOB_PREP_WORKING_DIR%\scene-file.ma"
```

<span data-ttu-id="e299e-137">For Arnold rendering, the Maya scene file would normally specify Arnold as the renderer.</span><span class="sxs-lookup"><span data-stu-id="e299e-137">For Arnold rendering, the Maya scene file would normally specify Arnold as the renderer.</span></span>  <span data-ttu-id="e299e-138">It can also be specified on the command line:</span><span class="sxs-lookup"><span data-stu-id="e299e-138">It can also be specified on the command line:</span></span>

```
render -renderer arnold -proj "%AZ_BATCH_JOB_PREP_WORKING_DIR%" -verb -rd "%AZ_BATCH_TASK_WORKING_DIR%\output" -s 10 -e 10 -x 1920 -y 1080 "%AZ_BATCH_JOB_PREP_WORKING_DIR%\scene-file.ma"
```

### <a name="batch-explorer-templates"></a><span data-ttu-id="e299e-139">Batch Explorer templates</span><span class="sxs-lookup"><span data-stu-id="e299e-139">Batch Explorer templates</span></span>

<span data-ttu-id="e299e-140">Pool and job templates can be accessed from the **Gallery** in Batch Explorer.</span><span class="sxs-lookup"><span data-stu-id="e299e-140">Pool and job templates can be accessed from the **Gallery** in Batch Explorer.</span></span>  <span data-ttu-id="e299e-141">The template source files are available in the [Batch Explorer data repository on GitHub](https://github.com/Azure/BatchExplorer-data/tree/master/ncj/maya).</span><span class="sxs-lookup"><span data-stu-id="e299e-141">The template source files are available in the [Batch Explorer data repository on GitHub](https://github.com/Azure/BatchExplorer-data/tree/master/ncj/maya).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e299e-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="e299e-142">Next steps</span></span>

<span data-ttu-id="e299e-143">Use the pool and job templates from the [data repository in GitHub](https://github.com/Azure/BatchExplorer-data/tree/master/ncj) using Batch Explorer.</span><span class="sxs-lookup"><span data-stu-id="e299e-143">Use the pool and job templates from the [data repository in GitHub](https://github.com/Azure/BatchExplorer-data/tree/master/ncj) using Batch Explorer.</span></span>  <span data-ttu-id="e299e-144">When required, create new templates or modify one of the supplied templates.</span><span class="sxs-lookup"><span data-stu-id="e299e-144">When required, create new templates or modify one of the supplied templates.</span></span>