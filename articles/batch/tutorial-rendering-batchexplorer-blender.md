---
title: Render a Blender scene using Azure Batch and Batch Explorer
description: Tutorial - How to render multiple frames from a Blender scene using Azure Batch and the Batch Explorer client application
services: batch
author: mscurrell
ms.author: markscu
ms.date: 08/02/2018
ms.topic: tutorial
ms.openlocfilehash: 8df9054e069540398c137290e682bb4160b4a799
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856385"
---
# <a name="tutorial-render-a-blender-scene-using-batch-explorer"></a><span data-ttu-id="78ddb-103">Tutorial: Render a Blender scene using Batch Explorer</span><span class="sxs-lookup"><span data-stu-id="78ddb-103">Tutorial: Render a Blender scene using Batch Explorer</span></span>

<span data-ttu-id="78ddb-104">This tutorial shows how to render multiple frames of a Blender demo scene.</span><span class="sxs-lookup"><span data-stu-id="78ddb-104">This tutorial shows how to render multiple frames of a Blender demo scene.</span></span> <span data-ttu-id="78ddb-105">Blender is used for the tutorial as it is free of charge for both the client and rendering VMs, but the process is very similar if other applications, such as Maya or 3ds Max, were to be used.</span><span class="sxs-lookup"><span data-stu-id="78ddb-105">Blender is used for the tutorial as it is free of charge for both the client and rendering VMs, but the process is very similar if other applications, such as Maya or 3ds Max, were to be used.</span></span>

<span data-ttu-id="78ddb-106">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="78ddb-106">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="78ddb-107">Upload a Blender scene to Azure storage</span><span class="sxs-lookup"><span data-stu-id="78ddb-107">Upload a Blender scene to Azure storage</span></span>
> * <span data-ttu-id="78ddb-108">Create a Batch pool with multiple nodes to perform the rendering</span><span class="sxs-lookup"><span data-stu-id="78ddb-108">Create a Batch pool with multiple nodes to perform the rendering</span></span>
> * <span data-ttu-id="78ddb-109">Render multiple frames</span><span class="sxs-lookup"><span data-stu-id="78ddb-109">Render multiple frames</span></span>
> * <span data-ttu-id="78ddb-110">View and download the rendered frame files</span><span class="sxs-lookup"><span data-stu-id="78ddb-110">View and download the rendered frame files</span></span>

<span data-ttu-id="78ddb-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="78ddb-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78ddb-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="78ddb-112">Prerequisites</span></span>

<span data-ttu-id="78ddb-113">An Azure Batch account with an associated storage account.</span><span class="sxs-lookup"><span data-stu-id="78ddb-113">An Azure Batch account with an associated storage account.</span></span>  <span data-ttu-id="78ddb-114">See any of the Batch Quickstarts articles, such as the [CLI article](https://docs.microsoft.com/azure/batch/quick-create-cli) to create a Batch account.</span><span class="sxs-lookup"><span data-stu-id="78ddb-114">See any of the Batch Quickstarts articles, such as the [CLI article](https://docs.microsoft.com/azure/batch/quick-create-cli) to create a Batch account.</span></span>

<span data-ttu-id="78ddb-115">A low-priority core quota of at least 50 cores is required for the VM size and number of VMs specified in this tutorial; the default quota can be used, but a smaller VM size will have to be used which will mean the images take longer to render.</span><span class="sxs-lookup"><span data-stu-id="78ddb-115">A low-priority core quota of at least 50 cores is required for the VM size and number of VMs specified in this tutorial; the default quota can be used, but a smaller VM size will have to be used which will mean the images take longer to render.</span></span> <span data-ttu-id="78ddb-116">The process for requesting an increased core quota is detailed in [this article](https://docs.microsoft.com/azure/batch/batch-quota-limit).</span><span class="sxs-lookup"><span data-stu-id="78ddb-116">The process for requesting an increased core quota is detailed in [this article](https://docs.microsoft.com/azure/batch/batch-quota-limit).</span></span>

<span data-ttu-id="78ddb-117">Finally, [Batch Explorer](https://azure.github.io/BatchExplorer/) has to be installed; it is available for Windows, OSX, and Linux.</span><span class="sxs-lookup"><span data-stu-id="78ddb-117">Finally, [Batch Explorer](https://azure.github.io/BatchExplorer/) has to be installed; it is available for Windows, OSX, and Linux.</span></span> <span data-ttu-id="78ddb-118">It is optional, but if [Blender](https://www.blender.org/download/) is installed then the sample model file can be viewed.</span><span class="sxs-lookup"><span data-stu-id="78ddb-118">It is optional, but if [Blender](https://www.blender.org/download/) is installed then the sample model file can be viewed.</span></span>

## <a name="download-the-demo-scene"></a><span data-ttu-id="78ddb-119">Download the demo scene</span><span class="sxs-lookup"><span data-stu-id="78ddb-119">Download the demo scene</span></span>

<span data-ttu-id="78ddb-120">Download the “Class room” demo ZIP file for Blender from the [Blender Demo Files web page](https://www.blender.org/download/demo-files/) and unzip it to a local drive.</span><span class="sxs-lookup"><span data-stu-id="78ddb-120">Download the “Class room” demo ZIP file for Blender from the [Blender Demo Files web page](https://www.blender.org/download/demo-files/) and unzip it to a local drive.</span></span>

## <a name="upload-a-scene-to-azure-storage"></a><span data-ttu-id="78ddb-121">Upload a scene to Azure storage</span><span class="sxs-lookup"><span data-stu-id="78ddb-121">Upload a scene to Azure storage</span></span>

<span data-ttu-id="78ddb-122">Create a storage account container for the demo scene files:</span><span class="sxs-lookup"><span data-stu-id="78ddb-122">Create a storage account container for the demo scene files:</span></span>

* <span data-ttu-id="78ddb-123">Start Batch Explorer</span><span class="sxs-lookup"><span data-stu-id="78ddb-123">Start Batch Explorer</span></span>
* <span data-ttu-id="78ddb-124">Select the 'Data' menu-item from the main menu on the left-hand side.</span><span class="sxs-lookup"><span data-stu-id="78ddb-124">Select the 'Data' menu-item from the main menu on the left-hand side.</span></span>
* <span data-ttu-id="78ddb-125">Ensure 'File groups' is selected in the pulldown.</span><span class="sxs-lookup"><span data-stu-id="78ddb-125">Ensure 'File groups' is selected in the pulldown.</span></span>
* <span data-ttu-id="78ddb-126">Select the '+' button and create a new 'Empty file group' called 'blender-classroom'</span><span class="sxs-lookup"><span data-stu-id="78ddb-126">Select the '+' button and create a new 'Empty file group' called 'blender-classroom'</span></span>
  * <span data-ttu-id="78ddb-127">A file group is simply an Azure Storage blob container with a 'fgrp-' prefix; it is a convention used to filter out other containers in the storage account</span><span class="sxs-lookup"><span data-stu-id="78ddb-127">A file group is simply an Azure Storage blob container with a 'fgrp-' prefix; it is a convention used to filter out other containers in the storage account</span></span>

![File group for scene files](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_scene_filegroup.png)

<span data-ttu-id="78ddb-129">Upload the scene files:</span><span class="sxs-lookup"><span data-stu-id="78ddb-129">Upload the scene files:</span></span>

* <span data-ttu-id="78ddb-130">Select the new container and drag-and-drop the contents of the 'classroom' folder to the container in Batch Explorer.</span><span class="sxs-lookup"><span data-stu-id="78ddb-130">Select the new container and drag-and-drop the contents of the 'classroom' folder to the container in Batch Explorer.</span></span>

![Scene files uploaded](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_scene_filegroup_uploaded.png)

## <a name="create-azure-storage-container-for-output-images"></a><span data-ttu-id="78ddb-132">Create Azure storage container for output images</span><span class="sxs-lookup"><span data-stu-id="78ddb-132">Create Azure storage container for output images</span></span>

<span data-ttu-id="78ddb-133">Create a storage account container for the demo scene output files:</span><span class="sxs-lookup"><span data-stu-id="78ddb-133">Create a storage account container for the demo scene output files:</span></span>

* <span data-ttu-id="78ddb-134">Select the 'Data' menu-item from the main menu on the left-hand side.</span><span class="sxs-lookup"><span data-stu-id="78ddb-134">Select the 'Data' menu-item from the main menu on the left-hand side.</span></span>
* <span data-ttu-id="78ddb-135">Select the '+' button and create a new 'Empty file group' called 'render-output'</span><span class="sxs-lookup"><span data-stu-id="78ddb-135">Select the '+' button and create a new 'Empty file group' called 'render-output'</span></span>

![File group for output files](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_output_filegroup.png)

## <a name="create-a-pool-of-vms-for-rendering"></a><span data-ttu-id="78ddb-137">Create a pool of VMs for rendering</span><span class="sxs-lookup"><span data-stu-id="78ddb-137">Create a pool of VMs for rendering</span></span>

<span data-ttu-id="78ddb-138">Create a Batch pool using rendering Azure Marketplace VM image that contains the Blender application:</span><span class="sxs-lookup"><span data-stu-id="78ddb-138">Create a Batch pool using rendering Azure Marketplace VM image that contains the Blender application:</span></span>

* <span data-ttu-id="78ddb-139">Select the 'Gallery' menu-item from the main menu on the left-hand side.</span><span class="sxs-lookup"><span data-stu-id="78ddb-139">Select the 'Gallery' menu-item from the main menu on the left-hand side.</span></span>
* <span data-ttu-id="78ddb-140">Select the 'Blender' item for the list of application items.</span><span class="sxs-lookup"><span data-stu-id="78ddb-140">Select the 'Blender' item for the list of application items.</span></span>
* <span data-ttu-id="78ddb-141">Select the items for rendering frames on Windows Server</span><span class="sxs-lookup"><span data-stu-id="78ddb-141">Select the items for rendering frames on Windows Server</span></span>
* <span data-ttu-id="78ddb-142">The link icon on the right-hand side of the item can optionally be selected to view the template files that will be used to create a pool and job.</span><span class="sxs-lookup"><span data-stu-id="78ddb-142">The link icon on the right-hand side of the item can optionally be selected to view the template files that will be used to create a pool and job.</span></span>

![Blender gallery items](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_gallery_item.png)

* <span data-ttu-id="78ddb-144">Select the button ‘Create pool for later use’</span><span class="sxs-lookup"><span data-stu-id="78ddb-144">Select the button ‘Create pool for later use’</span></span>
  * <span data-ttu-id="78ddb-145">Leave the Pool name as “blender-windows”</span><span class="sxs-lookup"><span data-stu-id="78ddb-145">Leave the Pool name as “blender-windows”</span></span>
  * <span data-ttu-id="78ddb-146">Set the ‘Dedicated vm count’ to “0”</span><span class="sxs-lookup"><span data-stu-id="78ddb-146">Set the ‘Dedicated vm count’ to “0”</span></span>
  * <span data-ttu-id="78ddb-147">Set the ‘Low priority vm count’ to “3”</span><span class="sxs-lookup"><span data-stu-id="78ddb-147">Set the ‘Low priority vm count’ to “3”</span></span>
  * <span data-ttu-id="78ddb-148">Set the ‘Node size’ to “Standard_F16” – another VM size can be selected, but time to render a frame will mainly be dependent on the number of cores.</span><span class="sxs-lookup"><span data-stu-id="78ddb-148">Set the ‘Node size’ to “Standard_F16” – another VM size can be selected, but time to render a frame will mainly be dependent on the number of cores.</span></span>
* <span data-ttu-id="78ddb-149">Select the green button to create the pool</span><span class="sxs-lookup"><span data-stu-id="78ddb-149">Select the green button to create the pool</span></span>
  * <span data-ttu-id="78ddb-150">The pool will be created almost immediately, but it will take a few minutes for the VMs to be allocated and started.</span><span class="sxs-lookup"><span data-stu-id="78ddb-150">The pool will be created almost immediately, but it will take a few minutes for the VMs to be allocated and started.</span></span>

![Pool template for Blender](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_pool_template.png)

> [!WARNING]
> <span data-ttu-id="78ddb-152">Note that when VMs are present in a pool, the cost of those VMs are charged to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="78ddb-152">Note that when VMs are present in a pool, the cost of those VMs are charged to your Azure subscription.</span></span> <span data-ttu-id="78ddb-153">The pool needs to deleted or the VMs need to be deleted to stop the charges.</span><span class="sxs-lookup"><span data-stu-id="78ddb-153">The pool needs to deleted or the VMs need to be deleted to stop the charges.</span></span> <span data-ttu-id="78ddb-154">Delete the pool at the end of this tutorial to prevent ongoing charges.</span><span class="sxs-lookup"><span data-stu-id="78ddb-154">Delete the pool at the end of this tutorial to prevent ongoing charges.</span></span>

<span data-ttu-id="78ddb-155">The status of the pool and VMs can be monitored in the 'Pools' view; the following example shows all three VMs have been allocated, two have been started and are idle, one is still starting: ![Pool heatmap](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_pool_heatmap.png)</span><span class="sxs-lookup"><span data-stu-id="78ddb-155">The status of the pool and VMs can be monitored in the 'Pools' view; the following example shows all three VMs have been allocated, two have been started and are idle, one is still starting: ![Pool heatmap](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_pool_heatmap.png)</span></span>

## <a name="create-a-rendering-job"></a><span data-ttu-id="78ddb-156">Create a rendering job</span><span class="sxs-lookup"><span data-stu-id="78ddb-156">Create a rendering job</span></span>

<span data-ttu-id="78ddb-157">Create a rendering job to render some frames using the pool that was created:</span><span class="sxs-lookup"><span data-stu-id="78ddb-157">Create a rendering job to render some frames using the pool that was created:</span></span>
* <span data-ttu-id="78ddb-158">Select the 'Gallery' menu-item from the main menu on the left-hand side.</span><span class="sxs-lookup"><span data-stu-id="78ddb-158">Select the 'Gallery' menu-item from the main menu on the left-hand side.</span></span>
* <span data-ttu-id="78ddb-159">Select the 'Blender' item for the list of application items.</span><span class="sxs-lookup"><span data-stu-id="78ddb-159">Select the 'Blender' item for the list of application items.</span></span>
* <span data-ttu-id="78ddb-160">Select the items for rendering frames on Windows Server.</span><span class="sxs-lookup"><span data-stu-id="78ddb-160">Select the items for rendering frames on Windows Server.</span></span>
* <span data-ttu-id="78ddb-161">Select the 'Run job with existing pool' button</span><span class="sxs-lookup"><span data-stu-id="78ddb-161">Select the 'Run job with existing pool' button</span></span>
* <span data-ttu-id="78ddb-162">Select the 'blender-windows' pool</span><span class="sxs-lookup"><span data-stu-id="78ddb-162">Select the 'blender-windows' pool</span></span>
* <span data-ttu-id="78ddb-163">Set the 'Job name' to 'blender-render-tutorial1'</span><span class="sxs-lookup"><span data-stu-id="78ddb-163">Set the 'Job name' to 'blender-render-tutorial1'</span></span>
* <span data-ttu-id="78ddb-164">Select 'fgrp-blender-classroom' for 'Input data'</span><span class="sxs-lookup"><span data-stu-id="78ddb-164">Select 'fgrp-blender-classroom' for 'Input data'</span></span>
* <span data-ttu-id="78ddb-165">Select the file icon for the 'Blend file' and select 'classroom.blend'</span><span class="sxs-lookup"><span data-stu-id="78ddb-165">Select the file icon for the 'Blend file' and select 'classroom.blend'</span></span>
* <span data-ttu-id="78ddb-166">Leave 'Frame start' as '1' and set 'Frame end' to '5'</span><span class="sxs-lookup"><span data-stu-id="78ddb-166">Leave 'Frame start' as '1' and set 'Frame end' to '5'</span></span>
* <span data-ttu-id="78ddb-167">Set 'Outputs' to 'fgrp-render-output'</span><span class="sxs-lookup"><span data-stu-id="78ddb-167">Set 'Outputs' to 'fgrp-render-output'</span></span>
* <span data-ttu-id="78ddb-168">Select the green button to create the job; a job will be created with five tasks, one for each frame</span><span class="sxs-lookup"><span data-stu-id="78ddb-168">Select the green button to create the job; a job will be created with five tasks, one for each frame</span></span>

![Job template for Blender](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_job_template.png)

<span data-ttu-id="78ddb-170">Once the job and all tasks have been created, the job will be displayed together with the job tasks: ![List of job tasks](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_task_list.png)</span><span class="sxs-lookup"><span data-stu-id="78ddb-170">Once the job and all tasks have been created, the job will be displayed together with the job tasks: ![List of job tasks](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_task_list.png)</span></span>

<span data-ttu-id="78ddb-171">When a task starts running for the first time on a pool VM, a Batch job preparation task is run which copies the scene files from the storage file group onto the VM so they can be accessed by Blender.</span><span class="sxs-lookup"><span data-stu-id="78ddb-171">When a task starts running for the first time on a pool VM, a Batch job preparation task is run which copies the scene files from the storage file group onto the VM so they can be accessed by Blender.</span></span>
<span data-ttu-id="78ddb-172">The status of the render can be determined by viewing the stdout.txt log file produced by Blender.</span><span class="sxs-lookup"><span data-stu-id="78ddb-172">The status of the render can be determined by viewing the stdout.txt log file produced by Blender.</span></span>  <span data-ttu-id="78ddb-173">Select a task, the 'Task Outputs' are displayed by default, and the 'stdout.txt' file can be selected and viewed.</span><span class="sxs-lookup"><span data-stu-id="78ddb-173">Select a task, the 'Task Outputs' are displayed by default, and the 'stdout.txt' file can be selected and viewed.</span></span>
<span data-ttu-id="78ddb-174">![stdout file](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_stdout.png)</span><span class="sxs-lookup"><span data-stu-id="78ddb-174">![stdout file](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_stdout.png)</span></span>

<span data-ttu-id="78ddb-175">If the 'blender-windows' pool is selected, the pool VMs will be seen in a running state: ![Pool heatmap with running nodes](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_pool_heatmap_running.png)</span><span class="sxs-lookup"><span data-stu-id="78ddb-175">If the 'blender-windows' pool is selected, the pool VMs will be seen in a running state: ![Pool heatmap with running nodes](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_pool_heatmap_running.png)</span></span>

<span data-ttu-id="78ddb-176">The rendered images will take several minutes to produce depending on the VM size selected.</span><span class="sxs-lookup"><span data-stu-id="78ddb-176">The rendered images will take several minutes to produce depending on the VM size selected.</span></span>  <span data-ttu-id="78ddb-177">Using the F16 VM specified earlier, frames took about 16 minutes to render.</span><span class="sxs-lookup"><span data-stu-id="78ddb-177">Using the F16 VM specified earlier, frames took about 16 minutes to render.</span></span>

## <a name="view-the-rendering-output"></a><span data-ttu-id="78ddb-178">View the rendering output</span><span class="sxs-lookup"><span data-stu-id="78ddb-178">View the rendering output</span></span>

<span data-ttu-id="78ddb-179">When frames have finished rendering, those tasks will be shown as completed: ![Tasks completing](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_tasks_complete.png)</span><span class="sxs-lookup"><span data-stu-id="78ddb-179">When frames have finished rendering, those tasks will be shown as completed: ![Tasks completing](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_tasks_complete.png)</span></span>

<span data-ttu-id="78ddb-180">The rendered image is written to the VM first and can be viewed by selecting the 'wd' folder: ![Rendered image on pool node](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_output_image.png)</span><span class="sxs-lookup"><span data-stu-id="78ddb-180">The rendered image is written to the VM first and can be viewed by selecting the 'wd' folder: ![Rendered image on pool node](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_output_image.png)</span></span>

<span data-ttu-id="78ddb-181">The job template also specifies that the output frame and log files are written back to the Azure Storage account file group specified when the job was created.</span><span class="sxs-lookup"><span data-stu-id="78ddb-181">The job template also specifies that the output frame and log files are written back to the Azure Storage account file group specified when the job was created.</span></span>  <span data-ttu-id="78ddb-182">The 'Data' UI can be used to view the output files and logs; it can be also used to download the files: ![Rendered image in storage file group](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_output_image_storage.png)</span><span class="sxs-lookup"><span data-stu-id="78ddb-182">The 'Data' UI can be used to view the output files and logs; it can be also used to download the files: ![Rendered image in storage file group](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_output_image_storage.png)</span></span>

<span data-ttu-id="78ddb-183">When all tasks have completed, the job will be marked as being completed: ![Job and all tasks completed](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_job_alltasks_complete.png)</span><span class="sxs-lookup"><span data-stu-id="78ddb-183">When all tasks have completed, the job will be marked as being completed: ![Job and all tasks completed](./media/tutorial-rendering-batchexplorer-blender/batch_explorer_job_alltasks_complete.png)</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="78ddb-184">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="78ddb-184">Clean up resources</span></span>

> [!WARNING]
> <span data-ttu-id="78ddb-185">The pool must be deleted (it could also be resized down to zero nodes) to stop charges for the VMs accruing to the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="78ddb-185">The pool must be deleted (it could also be resized down to zero nodes) to stop charges for the VMs accruing to the Azure subscription.</span></span>

* <span data-ttu-id="78ddb-186">Select 'Pools'</span><span class="sxs-lookup"><span data-stu-id="78ddb-186">Select 'Pools'</span></span>
* <span data-ttu-id="78ddb-187">Select the 'blender-windows' pool</span><span class="sxs-lookup"><span data-stu-id="78ddb-187">Select the 'blender-windows' pool</span></span>
* <span data-ttu-id="78ddb-188">Either right-click and 'Delete' or select the trash can icon above the pool</span><span class="sxs-lookup"><span data-stu-id="78ddb-188">Either right-click and 'Delete' or select the trash can icon above the pool</span></span>

## <a name="next-steps"></a><span data-ttu-id="78ddb-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="78ddb-189">Next steps</span></span>
* <span data-ttu-id="78ddb-190">In the ‘Gallery’ section, explore the rendering applications available via Batch Explorer.</span><span class="sxs-lookup"><span data-stu-id="78ddb-190">In the ‘Gallery’ section, explore the rendering applications available via Batch Explorer.</span></span>
* <span data-ttu-id="78ddb-191">For each application there are several templates available, which will expand over time.</span><span class="sxs-lookup"><span data-stu-id="78ddb-191">For each application there are several templates available, which will expand over time.</span></span>  <span data-ttu-id="78ddb-192">For example, for Blender templates exist that split up a single image into tiles, so parts of an image can be rendered in parallel.</span><span class="sxs-lookup"><span data-stu-id="78ddb-192">For example, for Blender templates exist that split up a single image into tiles, so parts of an image can be rendered in parallel.</span></span>
* <span data-ttu-id="78ddb-193">For a comprehensive description of rendering capabilities, see the set of articles [here](https://docs.microsoft.com/azure/batch/batch-rendering-service).</span><span class="sxs-lookup"><span data-stu-id="78ddb-193">For a comprehensive description of rendering capabilities, see the set of articles [here](https://docs.microsoft.com/azure/batch/batch-rendering-service).</span></span>