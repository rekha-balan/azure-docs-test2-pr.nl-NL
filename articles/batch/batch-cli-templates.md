---
title: Run Azure Batch jobs end-to-end using templates | Microsoft Docs
description: Create Batch pools, jobs, and tasks with template files and the Azure CLI.
services: batch
author: dlepow
manager: jeconnoc
ms.assetid: ''
ms.service: batch
ms.devlang: na
ms.topic: article
ms.workload: big-compute
ms.date: 08/02/2018
ms.author: danlep
ms.openlocfilehash: 50ed5a6b57c3c994f636db5cc975ad1908e50c7d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868303"
---
# <a name="use-azure-batch-cli-templates-and-file-transfer"></a><span data-ttu-id="5a1a2-103">Use Azure Batch CLI templates and file transfer</span><span class="sxs-lookup"><span data-stu-id="5a1a2-103">Use Azure Batch CLI templates and file transfer</span></span>

<span data-ttu-id="5a1a2-104">Using an Azure Batch extension to the Azure CLI, it is possible to run Batch jobs without writing code.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-104">Using an Azure Batch extension to the Azure CLI, it is possible to run Batch jobs without writing code.</span></span>

<span data-ttu-id="5a1a2-105">Create and use JSON template files with the Azure CLI to create Batch pools, jobs, and tasks.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-105">Create and use JSON template files with the Azure CLI to create Batch pools, jobs, and tasks.</span></span> <span data-ttu-id="5a1a2-106">Use CLI extension commands to easily upload job input files to the storage account associated with the Batch account, and download job output files.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-106">Use CLI extension commands to easily upload job input files to the storage account associated with the Batch account, and download job output files.</span></span>

## <a name="overview"></a><span data-ttu-id="5a1a2-107">Overview</span><span class="sxs-lookup"><span data-stu-id="5a1a2-107">Overview</span></span>

<span data-ttu-id="5a1a2-108">An extension to the Azure CLI enables Batch to be used end-to-end by users who are not developers.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-108">An extension to the Azure CLI enables Batch to be used end-to-end by users who are not developers.</span></span> <span data-ttu-id="5a1a2-109">With only CLI commands, you can create a pool, upload input data, create jobs and associated tasks, and download the resulting output data.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-109">With only CLI commands, you can create a pool, upload input data, create jobs and associated tasks, and download the resulting output data.</span></span> <span data-ttu-id="5a1a2-110">No additional code is required.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-110">No additional code is required.</span></span> <span data-ttu-id="5a1a2-111">Run the CLI commands directly or integrate them into scripts.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-111">Run the CLI commands directly or integrate them into scripts.</span></span>

<span data-ttu-id="5a1a2-112">Batch templates build on the [existing Batch support in the Azure CLI](batch-cli-get-started.md#json-files-for-resource-creation) for JSON files to specify property values when creating pools, jobs, tasks, and other items.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-112">Batch templates build on the [existing Batch support in the Azure CLI](batch-cli-get-started.md#json-files-for-resource-creation) for JSON files to specify property values when creating pools, jobs, tasks, and other items.</span></span> <span data-ttu-id="5a1a2-113">Batch templates add the following capabilities:</span><span class="sxs-lookup"><span data-stu-id="5a1a2-113">Batch templates add the following capabilities:</span></span>

-   <span data-ttu-id="5a1a2-114">Parameters can be defined.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-114">Parameters can be defined.</span></span> <span data-ttu-id="5a1a2-115">When the template is used, only the parameter values are specified to create the item, with other item property values specified in the template body.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-115">When the template is used, only the parameter values are specified to create the item, with other item property values specified in the template body.</span></span> <span data-ttu-id="5a1a2-116">A user who understands Batch and the applications to be run by Batch can create templates, specifying pool, job, and task property values.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-116">A user who understands Batch and the applications to be run by Batch can create templates, specifying pool, job, and task property values.</span></span> <span data-ttu-id="5a1a2-117">A user less familiar with Batch and/or the applications only needs to specify the values for the defined parameters.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-117">A user less familiar with Batch and/or the applications only needs to specify the values for the defined parameters.</span></span>

-   <span data-ttu-id="5a1a2-118">Job task factories create one or more tasks associated with a job, avoiding the need for many task definitions to be created and significantly simplifying job submission.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-118">Job task factories create one or more tasks associated with a job, avoiding the need for many task definitions to be created and significantly simplifying job submission.</span></span>


<span data-ttu-id="5a1a2-119">Jobs typically use input data files and produce output data files.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-119">Jobs typically use input data files and produce output data files.</span></span> <span data-ttu-id="5a1a2-120">A storage account is associated, by default, with each Batch account.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-120">A storage account is associated, by default, with each Batch account.</span></span> <span data-ttu-id="5a1a2-121">Transfer files to and from this storage account using the CLI, with no coding and no storage credentials.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-121">Transfer files to and from this storage account using the CLI, with no coding and no storage credentials.</span></span>

<span data-ttu-id="5a1a2-122">For example, [ffmpeg](http://ffmpeg.org/) is a popular application that processes audio and video files.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-122">For example, [ffmpeg](http://ffmpeg.org/) is a popular application that processes audio and video files.</span></span> <span data-ttu-id="5a1a2-123">Here are steps with the Azure Batch CLI to invoke ffmpeg to transcode source video files to different resolutions.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-123">Here are steps with the Azure Batch CLI to invoke ffmpeg to transcode source video files to different resolutions.</span></span>

-   <span data-ttu-id="5a1a2-124">Create a pool template.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-124">Create a pool template.</span></span> <span data-ttu-id="5a1a2-125">The user creating the template knows how to call the ffmpeg application and its requirements; they specify the appropriate OS, VM size, how ffmpeg is installed (from an application package or using a package manager, for example), and other pool property values.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-125">The user creating the template knows how to call the ffmpeg application and its requirements; they specify the appropriate OS, VM size, how ffmpeg is installed (from an application package or using a package manager, for example), and other pool property values.</span></span> <span data-ttu-id="5a1a2-126">Parameters are created so when the template is used, only the pool ID and number of VMs need to be specified.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-126">Parameters are created so when the template is used, only the pool ID and number of VMs need to be specified.</span></span>

-   <span data-ttu-id="5a1a2-127">Create a job template.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-127">Create a job template.</span></span> <span data-ttu-id="5a1a2-128">The user creating the template knows how ffmpeg needs to be invoked to transcode source video to a different resolution and specifies the task command line; they also know that there is a folder containing the source video files, with a task required per input file.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-128">The user creating the template knows how ffmpeg needs to be invoked to transcode source video to a different resolution and specifies the task command line; they also know that there is a folder containing the source video files, with a task required per input file.</span></span>

-   <span data-ttu-id="5a1a2-129">An end user with a set of video files to transcode first creates a pool using the pool template, specifying only the pool ID and number of VMs required.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-129">An end user with a set of video files to transcode first creates a pool using the pool template, specifying only the pool ID and number of VMs required.</span></span> <span data-ttu-id="5a1a2-130">They can then upload the source files to transcode.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-130">They can then upload the source files to transcode.</span></span> <span data-ttu-id="5a1a2-131">A job can then be submitted using the job template, specifying only the pool ID and location of the source files uploaded.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-131">A job can then be submitted using the job template, specifying only the pool ID and location of the source files uploaded.</span></span> <span data-ttu-id="5a1a2-132">The Batch job is created, with one task per input file being generated.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-132">The Batch job is created, with one task per input file being generated.</span></span> <span data-ttu-id="5a1a2-133">Finally, the transcoded output files can be downloaded.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-133">Finally, the transcoded output files can be downloaded.</span></span>

## <a name="installation"></a><span data-ttu-id="5a1a2-134">Installation</span><span class="sxs-lookup"><span data-stu-id="5a1a2-134">Installation</span></span>

<span data-ttu-id="5a1a2-135">To install the Azure Batch CLI extension, first [Install Azure CLI 2.0](/cli/azure/install-azure-cli), or run the Azure CLI in [Azure Cloud Shell](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="5a1a2-135">To install the Azure Batch CLI extension, first [Install Azure CLI 2.0](/cli/azure/install-azure-cli), or run the Azure CLI in [Azure Cloud Shell](../cloud-shell/overview.md).</span></span>

<span data-ttu-id="5a1a2-136">Install the latest version of the Batch extension using the following Azure CLI command:</span><span class="sxs-lookup"><span data-stu-id="5a1a2-136">Install the latest version of the Batch extension using the following Azure CLI command:</span></span>

```azurecli
az extension add --name azure-batch-cli-extensions
```

<span data-ttu-id="5a1a2-137">For more information about the Batch CLI extension and additional installation options, see the [GitHub repo](https://github.com/Azure/azure-batch-cli-extensions).</span><span class="sxs-lookup"><span data-stu-id="5a1a2-137">For more information about the Batch CLI extension and additional installation options, see the [GitHub repo](https://github.com/Azure/azure-batch-cli-extensions).</span></span>


<span data-ttu-id="5a1a2-138">To use the CLI extension features, you need an Azure Batch account and, for the commands that transfer files to and from storage, a linked storage account.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-138">To use the CLI extension features, you need an Azure Batch account and, for the commands that transfer files to and from storage, a linked storage account.</span></span>

<span data-ttu-id="5a1a2-139">To log into a Batch account with the Azure CLI, see [Manage Batch resources with Azure CLI](batch-cli-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5a1a2-139">To log into a Batch account with the Azure CLI, see [Manage Batch resources with Azure CLI](batch-cli-get-started.md).</span></span>

## <a name="templates"></a><span data-ttu-id="5a1a2-140">Templates</span><span class="sxs-lookup"><span data-stu-id="5a1a2-140">Templates</span></span>

<span data-ttu-id="5a1a2-141">Azure Batch templates are similar to Azure Resource Manager templates, in functionality and syntax.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-141">Azure Batch templates are similar to Azure Resource Manager templates, in functionality and syntax.</span></span> <span data-ttu-id="5a1a2-142">They are JSON files that contain item property names and values, but add the following main concepts:</span><span class="sxs-lookup"><span data-stu-id="5a1a2-142">They are JSON files that contain item property names and values, but add the following main concepts:</span></span>

-   <span data-ttu-id="5a1a2-143">**Parameters**</span><span class="sxs-lookup"><span data-stu-id="5a1a2-143">**Parameters**</span></span>

    -   <span data-ttu-id="5a1a2-144">Allow property values to be specified in a body section, with only parameter values needing to be supplied when the template is used.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-144">Allow property values to be specified in a body section, with only parameter values needing to be supplied when the template is used.</span></span> <span data-ttu-id="5a1a2-145">For example, the complete definition for a pool could be placed in the body and only one parameter defined for pool id; only a pool ID string therefore needs to be supplied to create a pool.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-145">For example, the complete definition for a pool could be placed in the body and only one parameter defined for pool id; only a pool ID string therefore needs to be supplied to create a pool.</span></span>
        
    -   <span data-ttu-id="5a1a2-146">The template body can be authored by someone with knowledge of Batch and the applications to be run by Batch; only values for the author-defined parameters must be supplied when the template is used.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-146">The template body can be authored by someone with knowledge of Batch and the applications to be run by Batch; only values for the author-defined parameters must be supplied when the template is used.</span></span> <span data-ttu-id="5a1a2-147">A user without the in-depth Batch and/or application knowledge can therefore use the templates.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-147">A user without the in-depth Batch and/or application knowledge can therefore use the templates.</span></span>

-   <span data-ttu-id="5a1a2-148">**Variables**</span><span class="sxs-lookup"><span data-stu-id="5a1a2-148">**Variables**</span></span>

    -   <span data-ttu-id="5a1a2-149">Allow simple or complex parameter values to be specified in one place and used in one or more places in the template body.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-149">Allow simple or complex parameter values to be specified in one place and used in one or more places in the template body.</span></span> <span data-ttu-id="5a1a2-150">Variables can simplify and reduce the size of the template, as well as make it more maintainable by having one location to change properties.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-150">Variables can simplify and reduce the size of the template, as well as make it more maintainable by having one location to change properties.</span></span>

-   <span data-ttu-id="5a1a2-151">**Higher-level constructs**</span><span class="sxs-lookup"><span data-stu-id="5a1a2-151">**Higher-level constructs**</span></span>

    -   <span data-ttu-id="5a1a2-152">Some higher-level constructs are available in the template that are not yet available in the Batch APIs.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-152">Some higher-level constructs are available in the template that are not yet available in the Batch APIs.</span></span> <span data-ttu-id="5a1a2-153">For example, a task factory can be defined in a job template that creates multiple tasks for the job, using a common task definition.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-153">For example, a task factory can be defined in a job template that creates multiple tasks for the job, using a common task definition.</span></span> <span data-ttu-id="5a1a2-154">These constructs avoid the need to code to dynamically create multiple JSON files, such as one file per task, as well as create script files to install applications via a package manager.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-154">These constructs avoid the need to code to dynamically create multiple JSON files, such as one file per task, as well as create script files to install applications via a package manager.</span></span>

    -   <span data-ttu-id="5a1a2-155">At some point, these constructs may be added to the Batch service and available in the Batch APIs, UIs, etc.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-155">At some point, these constructs may be added to the Batch service and available in the Batch APIs, UIs, etc.</span></span>

### <a name="pool-templates"></a><span data-ttu-id="5a1a2-156">Pool templates</span><span class="sxs-lookup"><span data-stu-id="5a1a2-156">Pool templates</span></span>

<span data-ttu-id="5a1a2-157">Pool templates support the standard template capabilities of parameters and variables.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-157">Pool templates support the standard template capabilities of parameters and variables.</span></span> <span data-ttu-id="5a1a2-158">They also support the following higher-level construct:</span><span class="sxs-lookup"><span data-stu-id="5a1a2-158">They also support the following higher-level construct:</span></span>

-   <span data-ttu-id="5a1a2-159">**Package references**</span><span class="sxs-lookup"><span data-stu-id="5a1a2-159">**Package references**</span></span>

    -   <span data-ttu-id="5a1a2-160">Optionally allows software to be copied to pool nodes by using package managers.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-160">Optionally allows software to be copied to pool nodes by using package managers.</span></span> <span data-ttu-id="5a1a2-161">The package manager and package ID are specified.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-161">The package manager and package ID are specified.</span></span> <span data-ttu-id="5a1a2-162">By declaring one or more packages, you avoid creating a script that gets the required packages, installing the script, and running the script on each pool node.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-162">By declaring one or more packages, you avoid creating a script that gets the required packages, installing the script, and running the script on each pool node.</span></span>

<span data-ttu-id="5a1a2-163">The following is an example of a template that creates a pool of Linux VMs with ffmpeg installed.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-163">The following is an example of a template that creates a pool of Linux VMs with ffmpeg installed.</span></span> <span data-ttu-id="5a1a2-164">To use it, supply only a pool ID string and the number of VMs in the pool:</span><span class="sxs-lookup"><span data-stu-id="5a1a2-164">To use it, supply only a pool ID string and the number of VMs in the pool:</span></span>

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "The number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "The pool ID "
            }
        }
    },
    "pool": {
        "type": "Microsoft.Batch/batchAccounts/pools",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('poolId')]",
            "virtualMachineConfiguration": {
                "imageReference": {
                    "publisher": "Canonical",
                    "offer": "UbuntuServer",
                    "sku": "16.04-LTS",
                    "version": "latest"
                },
                "nodeAgentSKUId": "batch.node.ubuntu 16.04"
            },
            "vmSize": "STANDARD_D3_V2",
            "targetDedicatedNodes": "[parameters('nodeCount')]",
            "enableAutoScale": false,
            "maxTasksPerNode": 1,
            "packageReferences": [
                {
                    "type": "aptPackage",
                    "id": "ffmpeg"
                }
            ]
        }
    }
}
```

<span data-ttu-id="5a1a2-165">If the template file was named _pool-ffmpeg.json_, then invoke the template as follows:</span><span class="sxs-lookup"><span data-stu-id="5a1a2-165">If the template file was named _pool-ffmpeg.json_, then invoke the template as follows:</span></span>

```azurecli
az batch pool create --template pool-ffmpeg.json
```

<span data-ttu-id="5a1a2-166">The CLI prompts you to provide values for the `poolId` and `nodeCount` parameters.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-166">The CLI prompts you to provide values for the `poolId` and `nodeCount` parameters.</span></span> <span data-ttu-id="5a1a2-167">You can also supply the parameters in a JSON file.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-167">You can also supply the parameters in a JSON file.</span></span> <span data-ttu-id="5a1a2-168">For example:</span><span class="sxs-lookup"><span data-stu-id="5a1a2-168">For example:</span></span>

```json
{
  "poolId": {
    "value": "mypool"
  },
  "nodeCount": {
    "value": 2
  }
}
```

<span data-ttu-id="5a1a2-169">If the parameters JSON file was named *pool-parameters.json*, then invoke the template as follows:</span><span class="sxs-lookup"><span data-stu-id="5a1a2-169">If the parameters JSON file was named *pool-parameters.json*, then invoke the template as follows:</span></span>

```azurecli
az batch pool create --template pool-ffmpeg.json --parameters pool-parameters.json
```

### <a name="job-templates"></a><span data-ttu-id="5a1a2-170">Job templates</span><span class="sxs-lookup"><span data-stu-id="5a1a2-170">Job templates</span></span>

<span data-ttu-id="5a1a2-171">Job templates support the standard template capabilities of parameters and variables.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-171">Job templates support the standard template capabilities of parameters and variables.</span></span> <span data-ttu-id="5a1a2-172">They also support the following higher-level construct:</span><span class="sxs-lookup"><span data-stu-id="5a1a2-172">They also support the following higher-level construct:</span></span>

-   <span data-ttu-id="5a1a2-173">**Task factory**</span><span class="sxs-lookup"><span data-stu-id="5a1a2-173">**Task factory**</span></span>

    -   <span data-ttu-id="5a1a2-174">Creates multiple tasks for a job from one task definition.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-174">Creates multiple tasks for a job from one task definition.</span></span> <span data-ttu-id="5a1a2-175">Three types of task factory are supported – parametric sweep, task per file, and task collection.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-175">Three types of task factory are supported – parametric sweep, task per file, and task collection.</span></span>

<span data-ttu-id="5a1a2-176">The following is an example of a template that creates a job to transcode MP4 video files with ffmpeg to one of two lower resolutions.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-176">The following is an example of a template that creates a job to transcode MP4 video files with ffmpeg to one of two lower resolutions.</span></span> <span data-ttu-id="5a1a2-177">It creates one task per source video file.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-177">It creates one task per source video file.</span></span> <span data-ttu-id="5a1a2-178">See [File groups and file transfer](#file-groups-and-file-transfer) for more about file groups for job input and output.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-178">See [File groups and file transfer](#file-groups-and-file-transfer) for more about file groups for job input and output.</span></span>

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "The name of Azure Batch pool which runs the job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "The name of Azure Batch job"
            }
        },
        "resolution": {
            "type": "string",
            "defaultValue": "428x240",
            "allowedValues": [
                "428x240",
                "854x480"
            ],
            "metadata": {
                "description": "Target video resolution"
            }
        }
    },
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('jobId')]",
            "constraints": {
                "maxWallClockTime": "PT5H",
                "maxTaskRetryCount": 1
            },
            "poolInfo": {
                "poolId": "[parameters('poolId')]"
            },
            "taskFactory": {
                "type": "taskPerFile",
                "source": { 
                    "fileGroup": "ffmpeg-input"
                },
                "repeatTask": {
                    "commandLine": "ffmpeg -i {fileName} -y -s [parameters('resolution')] -strict -2 {fileNameWithoutExtension}_[parameters('resolution')].mp4",
                    "resourceFiles": [
                        {
                            "blobSource": "{url}",
                            "filePath": "{fileName}"
                        }
                    ],
                    "outputFiles": [
                        {
                            "filePattern": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                            "destination": {
                                "autoStorage": {
                                    "path": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                                    "fileGroup": "ffmpeg-output"
                                }
                            },
                            "uploadOptions": {
                                "uploadCondition": "TaskSuccess"
                            }
                        }
                    ]
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
```

<span data-ttu-id="5a1a2-179">If the template file was named _job-ffmpeg.json_, then invoke the template as follows:</span><span class="sxs-lookup"><span data-stu-id="5a1a2-179">If the template file was named _job-ffmpeg.json_, then invoke the template as follows:</span></span>

```azurecli
az batch job create --template job-ffmpeg.json
```

<span data-ttu-id="5a1a2-180">As before, the CLI prompts you to provide values for the parameters.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-180">As before, the CLI prompts you to provide values for the parameters.</span></span> <span data-ttu-id="5a1a2-181">You can also supply the parameters in a JSON file.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-181">You can also supply the parameters in a JSON file.</span></span>

### <a name="use-templates-in-batch-explorer"></a><span data-ttu-id="5a1a2-182">Use templates in Batch Explorer</span><span class="sxs-lookup"><span data-stu-id="5a1a2-182">Use templates in Batch Explorer</span></span>

<span data-ttu-id="5a1a2-183">You can upload a Batch CLI template to the [Batch Explorer](https://github.com/Azure/BatchExplorer) desktop application (formerly called BatchLabs) to create a Batch pool or job.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-183">You can upload a Batch CLI template to the [Batch Explorer](https://github.com/Azure/BatchExplorer) desktop application (formerly called BatchLabs) to create a Batch pool or job.</span></span> <span data-ttu-id="5a1a2-184">You can also select from predefined pool and job templates in the Batch Explorer Gallery.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-184">You can also select from predefined pool and job templates in the Batch Explorer Gallery.</span></span>

<span data-ttu-id="5a1a2-185">To upload a template:</span><span class="sxs-lookup"><span data-stu-id="5a1a2-185">To upload a template:</span></span>

1. <span data-ttu-id="5a1a2-186">In Batch Explorer, select **Gallery** > **Local templates**.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-186">In Batch Explorer, select **Gallery** > **Local templates**.</span></span>

2. <span data-ttu-id="5a1a2-187">Select, or drag and drop, a local pool or job template.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-187">Select, or drag and drop, a local pool or job template.</span></span>

3. <span data-ttu-id="5a1a2-188">Select **Use this template**, and follow the on-screen prompts.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-188">Select **Use this template**, and follow the on-screen prompts.</span></span>

## <a name="file-groups-and-file-transfer"></a><span data-ttu-id="5a1a2-189">File groups and file transfer</span><span class="sxs-lookup"><span data-stu-id="5a1a2-189">File groups and file transfer</span></span>

<span data-ttu-id="5a1a2-190">Most jobs and tasks require input files and produce output files.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-190">Most jobs and tasks require input files and produce output files.</span></span> <span data-ttu-id="5a1a2-191">Usually, input files and output files are transferred, either from the client to the node, or from the node to the client.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-191">Usually, input files and output files are transferred, either from the client to the node, or from the node to the client.</span></span> <span data-ttu-id="5a1a2-192">The Azure Batch CLI extension abstracts away file transfer and utilizes the storage account that you can associate with each Batch account.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-192">The Azure Batch CLI extension abstracts away file transfer and utilizes the storage account that you can associate with each Batch account.</span></span>

<span data-ttu-id="5a1a2-193">A file group equates to a container that is created in the Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-193">A file group equates to a container that is created in the Azure storage account.</span></span> <span data-ttu-id="5a1a2-194">The file group may have subfolders.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-194">The file group may have subfolders.</span></span>

<span data-ttu-id="5a1a2-195">The Batch CLI extension provides commands to upload files from client to a specified file group and download files from the specified file group to a client.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-195">The Batch CLI extension provides commands to upload files from client to a specified file group and download files from the specified file group to a client.</span></span>

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

<span data-ttu-id="5a1a2-196">Pool and job templates allow files stored in file groups to be specified for copy onto pool nodes or off pool nodes back to a file group.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-196">Pool and job templates allow files stored in file groups to be specified for copy onto pool nodes or off pool nodes back to a file group.</span></span> <span data-ttu-id="5a1a2-197">For example, in the job template specified previously, the file group *ffmpeg-input* is specified for the task factory as the location of the source video files copied down to the node for transcoding.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-197">For example, in the job template specified previously, the file group *ffmpeg-input* is specified for the task factory as the location of the source video files copied down to the node for transcoding.</span></span> <span data-ttu-id="5a1a2-198">The file group *ffmpeg-output* is the location where the transcoded output files are copied from the node running each task.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-198">The file group *ffmpeg-output* is the location where the transcoded output files are copied from the node running each task.</span></span>

## <a name="summary"></a><span data-ttu-id="5a1a2-199">Summary</span><span class="sxs-lookup"><span data-stu-id="5a1a2-199">Summary</span></span>

<span data-ttu-id="5a1a2-200">Template and file transfer support have currently been added only to the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-200">Template and file transfer support have currently been added only to the Azure CLI.</span></span> <span data-ttu-id="5a1a2-201">The goal is to expand the audience that can use Batch to users who do not need to develop code using the Batch APIs, such as researchers and IT users.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-201">The goal is to expand the audience that can use Batch to users who do not need to develop code using the Batch APIs, such as researchers and IT users.</span></span> <span data-ttu-id="5a1a2-202">Without coding, users with knowledge of Azure, Batch, and the applications to be run by Batch can create templates for pool and job creation.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-202">Without coding, users with knowledge of Azure, Batch, and the applications to be run by Batch can create templates for pool and job creation.</span></span> <span data-ttu-id="5a1a2-203">With template parameters, users without detailed knowledge of Batch and the applications can use the templates.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-203">With template parameters, users without detailed knowledge of Batch and the applications can use the templates.</span></span>

<span data-ttu-id="5a1a2-204">Try out the Batch extension for the Azure CLI and provide us with any feedback or suggestions, either in the comments for this article or via the [Batch Community repo](https://github.com/Azure/Batch).</span><span class="sxs-lookup"><span data-stu-id="5a1a2-204">Try out the Batch extension for the Azure CLI and provide us with any feedback or suggestions, either in the comments for this article or via the [Batch Community repo](https://github.com/Azure/Batch).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a1a2-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="5a1a2-205">Next steps</span></span>

- <span data-ttu-id="5a1a2-206">Detailed installation and usage documentation, samples, and source code are available in the [Azure GitHub repo](https://github.com/Azure/azure-batch-cli-extensions).</span><span class="sxs-lookup"><span data-stu-id="5a1a2-206">Detailed installation and usage documentation, samples, and source code are available in the [Azure GitHub repo](https://github.com/Azure/azure-batch-cli-extensions).</span></span>

- <span data-ttu-id="5a1a2-207">Learn more about using [Batch Explorer](https://github.com/Azure/BatchExplorer) to create and manage Batch resources.</span><span class="sxs-lookup"><span data-stu-id="5a1a2-207">Learn more about using [Batch Explorer](https://github.com/Azure/BatchExplorer) to create and manage Batch resources.</span></span>
