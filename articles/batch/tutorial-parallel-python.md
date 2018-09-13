---
title: Run a parallel workload - Azure Batch Python
description: Tutorial - Process media files in parallel with ffmpeg in Azure Batch using the Batch Python client library
services: batch
author: dlepow
manager: jeconnoc
ms.service: batch
ms.devlang: python
ms.topic: tutorial
ms.date: 01/23/2018
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 916cedfb91f0711f136ff8ad679be94c68964619
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868743"
---
# <a name="tutorial-run-a-parallel-workload-with-azure-batch-using-the-python-api"></a><span data-ttu-id="74475-103">Tutorial: Run a parallel workload with Azure Batch using the Python API</span><span class="sxs-lookup"><span data-stu-id="74475-103">Tutorial: Run a parallel workload with Azure Batch using the Python API</span></span>

<span data-ttu-id="74475-104">Use Azure Batch to run large-scale parallel and high-performance computing (HPC) batch jobs efficiently in Azure.</span><span class="sxs-lookup"><span data-stu-id="74475-104">Use Azure Batch to run large-scale parallel and high-performance computing (HPC) batch jobs efficiently in Azure.</span></span> <span data-ttu-id="74475-105">This tutorial walks through a Python example of running a parallel workload using Batch.</span><span class="sxs-lookup"><span data-stu-id="74475-105">This tutorial walks through a Python example of running a parallel workload using Batch.</span></span> <span data-ttu-id="74475-106">You learn a common Batch application workflow and how to interact programmatically with Batch and Storage resources.</span><span class="sxs-lookup"><span data-stu-id="74475-106">You learn a common Batch application workflow and how to interact programmatically with Batch and Storage resources.</span></span> <span data-ttu-id="74475-107">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="74475-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="74475-108">Authenticate with Batch and Storage accounts</span><span class="sxs-lookup"><span data-stu-id="74475-108">Authenticate with Batch and Storage accounts</span></span>
> * <span data-ttu-id="74475-109">Upload input files to Storage</span><span class="sxs-lookup"><span data-stu-id="74475-109">Upload input files to Storage</span></span>
> * <span data-ttu-id="74475-110">Create a pool of compute nodes to run an application</span><span class="sxs-lookup"><span data-stu-id="74475-110">Create a pool of compute nodes to run an application</span></span>
> * <span data-ttu-id="74475-111">Create a job and tasks to process input files</span><span class="sxs-lookup"><span data-stu-id="74475-111">Create a job and tasks to process input files</span></span>
> * <span data-ttu-id="74475-112">Monitor task execution</span><span class="sxs-lookup"><span data-stu-id="74475-112">Monitor task execution</span></span>
> * <span data-ttu-id="74475-113">Retrieve output files</span><span class="sxs-lookup"><span data-stu-id="74475-113">Retrieve output files</span></span>

<span data-ttu-id="74475-114">In this tutorial, you convert MP4 media files in parallel to MP3 format using the [ffmpeg](http://ffmpeg.org/) open-source tool.</span><span class="sxs-lookup"><span data-stu-id="74475-114">In this tutorial, you convert MP4 media files in parallel to MP3 format using the [ffmpeg](http://ffmpeg.org/) open-source tool.</span></span> 

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="74475-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="74475-115">Prerequisites</span></span>

* [<span data-ttu-id="74475-116">Python version 2.7 or 3.3 or later</span><span class="sxs-lookup"><span data-stu-id="74475-116">Python version 2.7 or 3.3 or later</span></span>](https://www.python.org/downloads/)

* <span data-ttu-id="74475-117">[pip](https://pip.pypa.io/en/stable/installing/) package manager</span><span class="sxs-lookup"><span data-stu-id="74475-117">[pip](https://pip.pypa.io/en/stable/installing/) package manager</span></span>

* <span data-ttu-id="74475-118">An Azure Batch account and a linked Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="74475-118">An Azure Batch account and a linked Azure Storage account.</span></span> <span data-ttu-id="74475-119">To create these accounts, see the Batch quickstarts using the [Azure portal](quick-create-portal.md) or [Azure CLI](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="74475-119">To create these accounts, see the Batch quickstarts using the [Azure portal](quick-create-portal.md) or [Azure CLI](quick-create-cli.md).</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="74475-120">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="74475-120">Sign in to Azure</span></span>

<span data-ttu-id="74475-121">Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="74475-121">Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>

[!INCLUDE [batch-common-credentials](../../includes/batch-common-credentials.md)] 

## <a name="download-and-run-the-sample"></a><span data-ttu-id="74475-122">Download and run the sample</span><span class="sxs-lookup"><span data-stu-id="74475-122">Download and run the sample</span></span>

### <a name="download-the-sample"></a><span data-ttu-id="74475-123">Download the sample</span><span class="sxs-lookup"><span data-stu-id="74475-123">Download the sample</span></span>

<span data-ttu-id="74475-124">[Download or clone the sample app](https://github.com/Azure-Samples/batch-python-ffmpeg-tutorial) from GitHub.</span><span class="sxs-lookup"><span data-stu-id="74475-124">[Download or clone the sample app](https://github.com/Azure-Samples/batch-python-ffmpeg-tutorial) from GitHub.</span></span> <span data-ttu-id="74475-125">To clone the sample app repo with a Git client, use the following command:</span><span class="sxs-lookup"><span data-stu-id="74475-125">To clone the sample app repo with a Git client, use the following command:</span></span>

```
git clone https://github.com/Azure-Samples/batch-python-ffmpeg-tutorial.git
```

<span data-ttu-id="74475-126">Navigate to the directory that contains the file `batch_python_tutorial_ffmpeg.py`.</span><span class="sxs-lookup"><span data-stu-id="74475-126">Navigate to the directory that contains the file `batch_python_tutorial_ffmpeg.py`.</span></span>

<span data-ttu-id="74475-127">In your Python environment, install the required packages using `pip`.</span><span class="sxs-lookup"><span data-stu-id="74475-127">In your Python environment, install the required packages using `pip`.</span></span>

```bash
pip install -r requirements.txt
```

<span data-ttu-id="74475-128">Open the file `batch_python_tutorial_ffmpeg.py`.</span><span class="sxs-lookup"><span data-stu-id="74475-128">Open the file `batch_python_tutorial_ffmpeg.py`.</span></span> <span data-ttu-id="74475-129">Update the Batch and storage account credential strings with the values unique to your accounts.</span><span class="sxs-lookup"><span data-stu-id="74475-129">Update the Batch and storage account credential strings with the values unique to your accounts.</span></span> <span data-ttu-id="74475-130">For example:</span><span class="sxs-lookup"><span data-stu-id="74475-130">For example:</span></span>


```Python
_BATCH_ACCOUNT_NAME = 'mybatchaccount'
_BATCH_ACCOUNT_KEY = 'xxxxxxxxxxxxxxxxE+yXrRvJAqT9BlXwwo1CwF+SwAYOxxxxxxxxxxxxxxxx43pXi/gdiATkvbpLRl3x14pcEQ=='
_BATCH_ACCOUNT_URL = 'https://mybatchaccount.mybatchregion.batch.azure.com'
_STORAGE_ACCOUNT_NAME = 'mystorageaccount'
_STORAGE_ACCOUNT_KEY = 'xxxxxxxxxxxxxxxxy4/xxxxxxxxxxxxxxxxfwpbIC5aAWA8wDu+AFXZB827Mt9lybZB1nUcQbQiUrkPtilK5BQ=='
```

### <a name="run-the-app"></a><span data-ttu-id="74475-131">Run the app</span><span class="sxs-lookup"><span data-stu-id="74475-131">Run the app</span></span>

<span data-ttu-id="74475-132">To run the script:</span><span class="sxs-lookup"><span data-stu-id="74475-132">To run the script:</span></span>

```
python batch_python_tutorial_ffmpeg.py
```

<span data-ttu-id="74475-133">When you run the sample application, the console output is similar to the following.</span><span class="sxs-lookup"><span data-stu-id="74475-133">When you run the sample application, the console output is similar to the following.</span></span> <span data-ttu-id="74475-134">During execution, you experience a pause at `Monitoring all tasks for 'Completed' state, timeout in 00:30:00...` while the pool's compute nodes are started.</span><span class="sxs-lookup"><span data-stu-id="74475-134">During execution, you experience a pause at `Monitoring all tasks for 'Completed' state, timeout in 00:30:00...` while the pool's compute nodes are started.</span></span> 
   
```
Sample start: 12/12/2017 3:20:21 PM

Container [input] created.
Container [output] created.
Uploading file LowPriVMs-1.mp4 to container [input]...
Uploading file LowPriVMs-2.mp4 to container [input]...
Uploading file LowPriVMs-3.mp4 to container [input]...
Uploading file LowPriVMs-4.mp4 to container [input]...
Uploading file LowPriVMs-5.mp4 to container [input]...
Creating pool [LinuxFFmpegPool]...
Creating job [LinuxFFmpegJob]...
Adding 5 tasks to job [LinuxFFmpegJob]...
Monitoring all tasks for 'Completed' state, timeout in 00:30:00...
Success! All tasks completed successfully within the specified timeout period.
Deleting container [input]....

Sample end: 12/12/2017 3:29:36 PM
Elapsed time: 00:09:14.3418742
```

<span data-ttu-id="74475-135">Go to your Batch account in the Azure portal to monitor the pool, compute nodes, job, and tasks.</span><span class="sxs-lookup"><span data-stu-id="74475-135">Go to your Batch account in the Azure portal to monitor the pool, compute nodes, job, and tasks.</span></span> <span data-ttu-id="74475-136">For example, to see a heat map of the compute nodes in your pool, click **Pools** > *LinuxFFmpegPool*.</span><span class="sxs-lookup"><span data-stu-id="74475-136">For example, to see a heat map of the compute nodes in your pool, click **Pools** > *LinuxFFmpegPool*.</span></span>

<span data-ttu-id="74475-137">When tasks are running, the heat map is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="74475-137">When tasks are running, the heat map is similar to the following:</span></span>

![Pool heat map](./media/tutorial-parallel-python/pool.png)

<span data-ttu-id="74475-139">Typical execution time is approximately **5 minutes** when you run the application in its default configuration.</span><span class="sxs-lookup"><span data-stu-id="74475-139">Typical execution time is approximately **5 minutes** when you run the application in its default configuration.</span></span> <span data-ttu-id="74475-140">Pool creation takes the most time.</span><span class="sxs-lookup"><span data-stu-id="74475-140">Pool creation takes the most time.</span></span> 

[!INCLUDE [batch-common-tutorial-download](../../includes/batch-common-tutorial-download.md)]

## <a name="review-the-code"></a><span data-ttu-id="74475-141">Review the code</span><span class="sxs-lookup"><span data-stu-id="74475-141">Review the code</span></span>

<span data-ttu-id="74475-142">The following sections break down the sample application into the steps that it performs to process a workload in the Batch service.</span><span class="sxs-lookup"><span data-stu-id="74475-142">The following sections break down the sample application into the steps that it performs to process a workload in the Batch service.</span></span> <span data-ttu-id="74475-143">Refer to the Python code while you read the rest of this article, since not every line of code in the sample is discussed.</span><span class="sxs-lookup"><span data-stu-id="74475-143">Refer to the Python code while you read the rest of this article, since not every line of code in the sample is discussed.</span></span>

### <a name="authenticate-blob-and-batch-clients"></a><span data-ttu-id="74475-144">Authenticate Blob and Batch clients</span><span class="sxs-lookup"><span data-stu-id="74475-144">Authenticate Blob and Batch clients</span></span>

<span data-ttu-id="74475-145">To interact with a storage account, the app uses the [azure-storage-blob](https://pypi.python.org/pypi/azure-storage-blob) package to create a [BlockBlobService](/python/api/azure.storage.blob.blockblobservice.blockblobservice) object.</span><span class="sxs-lookup"><span data-stu-id="74475-145">To interact with a storage account, the app uses the [azure-storage-blob](https://pypi.python.org/pypi/azure-storage-blob) package to create a [BlockBlobService](/python/api/azure.storage.blob.blockblobservice.blockblobservice) object.</span></span>

```python
blob_client = azureblob.BlockBlobService(
    account_name=STORAGE_ACCOUNT_NAME,
    account_key=STORAGE_ACCOUNT_KEY)
```

<span data-ttu-id="74475-146">The app creates a [BatchServiceClient](/python/api/azure.batch.batchserviceclient) object to create and manage pools, jobs, and tasks in the Batch service.</span><span class="sxs-lookup"><span data-stu-id="74475-146">The app creates a [BatchServiceClient](/python/api/azure.batch.batchserviceclient) object to create and manage pools, jobs, and tasks in the Batch service.</span></span> <span data-ttu-id="74475-147">The Batch client in the sample uses shared key authentication.</span><span class="sxs-lookup"><span data-stu-id="74475-147">The Batch client in the sample uses shared key authentication.</span></span> <span data-ttu-id="74475-148">Batch also supports authentication through [Azure Active Directory](batch-aad-auth.md), to authenticate individual users or an unattended application.</span><span class="sxs-lookup"><span data-stu-id="74475-148">Batch also supports authentication through [Azure Active Directory](batch-aad-auth.md), to authenticate individual users or an unattended application.</span></span>

```python
credentials = batchauth.SharedKeyCredentials(_BATCH_ACCOUNT_NAME,
    _BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=_BATCH_ACCOUNT_URL)
```

### <a name="upload-input-files"></a><span data-ttu-id="74475-149">Upload input files</span><span class="sxs-lookup"><span data-stu-id="74475-149">Upload input files</span></span>

<span data-ttu-id="74475-150">The app uses the `blob_client` reference create a storage container for the input MP4 files and a container for the task output.</span><span class="sxs-lookup"><span data-stu-id="74475-150">The app uses the `blob_client` reference create a storage container for the input MP4 files and a container for the task output.</span></span> <span data-ttu-id="74475-151">Then, it calls the `upload_file_to_container` function to upload MP4 files in the local `InputFiles` directory to the container.</span><span class="sxs-lookup"><span data-stu-id="74475-151">Then, it calls the `upload_file_to_container` function to upload MP4 files in the local `InputFiles` directory to the container.</span></span> <span data-ttu-id="74475-152">The files in storage are defined as Batch [ResourceFile](/python/api/azure.batch.models.resourcefile) objects that Batch can later download to compute nodes.</span><span class="sxs-lookup"><span data-stu-id="74475-152">The files in storage are defined as Batch [ResourceFile](/python/api/azure.batch.models.resourcefile) objects that Batch can later download to compute nodes.</span></span>

```python
blob_client.create_container(input_container_name, fail_on_exist=False)
blob_client.create_container(output_container_name, fail_on_exist=False)
input_file_paths = []
    
for folder, subs, files in os.walk('./InputFiles/'):
    for filename in files:
        if filename.endswith(".mp4"):
            input_file_paths.append(os.path.abspath(os.path.join(folder, filename)))

# Upload the input files. This is the collection of files that are to be processed by the tasks. 
input_files = [
    upload_file_to_container(blob_client, input_container_name, file_path)
    for file_path in input_file_paths]
```

### <a name="create-a-pool-of-compute-nodes"></a><span data-ttu-id="74475-153">Create a pool of compute nodes</span><span class="sxs-lookup"><span data-stu-id="74475-153">Create a pool of compute nodes</span></span>

<span data-ttu-id="74475-154">Next, the sample creates a pool of compute nodes in the Batch account with a call to `create_pool`.</span><span class="sxs-lookup"><span data-stu-id="74475-154">Next, the sample creates a pool of compute nodes in the Batch account with a call to `create_pool`.</span></span> <span data-ttu-id="74475-155">This defined function uses the Batch [PoolAddParameter](/python/api/azure.batch.models.pooladdparameter) class to set the number of nodes, VM size, and a pool configuration.</span><span class="sxs-lookup"><span data-stu-id="74475-155">This defined function uses the Batch [PoolAddParameter](/python/api/azure.batch.models.pooladdparameter) class to set the number of nodes, VM size, and a pool configuration.</span></span> <span data-ttu-id="74475-156">Here, a [VirtualMachineConfiguration](/python/api/azure.batch.models.virtualmachineconfiguration) object specifies an [ImageReference](/python/api/azure.batch.models.imagereference) to an Ubuntu Server 16.04 LTS image published in the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="74475-156">Here, a [VirtualMachineConfiguration](/python/api/azure.batch.models.virtualmachineconfiguration) object specifies an [ImageReference](/python/api/azure.batch.models.imagereference) to an Ubuntu Server 16.04 LTS image published in the Azure Marketplace.</span></span> <span data-ttu-id="74475-157">Batch supports a wide range of VM images in the Azure Marketplace, as well as custom VM images.</span><span class="sxs-lookup"><span data-stu-id="74475-157">Batch supports a wide range of VM images in the Azure Marketplace, as well as custom VM images.</span></span>

<span data-ttu-id="74475-158">The number of nodes and VM size are set using defined constants.</span><span class="sxs-lookup"><span data-stu-id="74475-158">The number of nodes and VM size are set using defined constants.</span></span> <span data-ttu-id="74475-159">Batch supports dedicated nodes and [low-priority nodes](batch-low-pri-vms.md), and you can use either or both in your pools.</span><span class="sxs-lookup"><span data-stu-id="74475-159">Batch supports dedicated nodes and [low-priority nodes](batch-low-pri-vms.md), and you can use either or both in your pools.</span></span> <span data-ttu-id="74475-160">Dedicated nodes are reserved for your pool.</span><span class="sxs-lookup"><span data-stu-id="74475-160">Dedicated nodes are reserved for your pool.</span></span> <span data-ttu-id="74475-161">Low-priority nodes are offered at a reduced price from surplus VM capacity in Azure.</span><span class="sxs-lookup"><span data-stu-id="74475-161">Low-priority nodes are offered at a reduced price from surplus VM capacity in Azure.</span></span> <span data-ttu-id="74475-162">Low-priority nodes become unavailable if Azure does not have enough capacity.</span><span class="sxs-lookup"><span data-stu-id="74475-162">Low-priority nodes become unavailable if Azure does not have enough capacity.</span></span> <span data-ttu-id="74475-163">The sample by default creates a pool containing only 5 low-priority nodes in size *Standard_A1_v2*.</span><span class="sxs-lookup"><span data-stu-id="74475-163">The sample by default creates a pool containing only 5 low-priority nodes in size *Standard_A1_v2*.</span></span> 

<span data-ttu-id="74475-164">In addition to physical node properties, this pool configuration includes a [StartTask](/python/api/azure.batch.models.starttask) object.</span><span class="sxs-lookup"><span data-stu-id="74475-164">In addition to physical node properties, this pool configuration includes a [StartTask](/python/api/azure.batch.models.starttask) object.</span></span> <span data-ttu-id="74475-165">The StartTask executes on each node as that node joins the pool, and each time a node is restarted.</span><span class="sxs-lookup"><span data-stu-id="74475-165">The StartTask executes on each node as that node joins the pool, and each time a node is restarted.</span></span> <span data-ttu-id="74475-166">In this example, the StartTask runs Bash shell commands to install the ffmpeg package and dependencies on the nodes.</span><span class="sxs-lookup"><span data-stu-id="74475-166">In this example, the StartTask runs Bash shell commands to install the ffmpeg package and dependencies on the nodes.</span></span>

<span data-ttu-id="74475-167">The [pool.add](/python/api/azure.batch.operations.pooloperations#azure_batch_operations_PoolOperations_add) method submits the pool to the Batch service.</span><span class="sxs-lookup"><span data-stu-id="74475-167">The [pool.add](/python/api/azure.batch.operations.pooloperations#azure_batch_operations_PoolOperations_add) method submits the pool to the Batch service.</span></span>

```python
new_pool = batch.models.PoolAddParameter(
    id=pool_id,
    virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
        image_reference=batchmodels.ImageReference(
            publisher="Canonical",
            offer="UbuntuServer",
            sku="16.04-LTS",
            version="latest"
            ),
        node_agent_sku_id="batch.node.ubuntu 16.04"),
    vm_size=_POOL_VM_SIZE,
    target_dedicated_nodes=_DEDICATED_POOL_NODE_COUNT,
    target_low_priority_nodes=_LOW_PRIORITY_POOL_NODE_COUNT,
    start_task=batchmodels.StartTask(
        command_line="/bin/bash -c \"apt-get update && apt-get install -y ffmpeg\"",
        wait_for_success=True,
        user_identity=batchmodels.UserIdentity(
            auto_user=batchmodels.AutoUserSpecification(
                scope=batchmodels.AutoUserScope.pool,
                elevation_level=batchmodels.ElevationLevel.admin)),
    )
)
batch_service_client.pool.add(new_pool)
```

### <a name="create-a-job"></a><span data-ttu-id="74475-168">Create a job</span><span class="sxs-lookup"><span data-stu-id="74475-168">Create a job</span></span>

<span data-ttu-id="74475-169">A Batch job specifies a pool to run tasks on and optional settings such as a priority and schedule for the work.</span><span class="sxs-lookup"><span data-stu-id="74475-169">A Batch job specifies a pool to run tasks on and optional settings such as a priority and schedule for the work.</span></span> <span data-ttu-id="74475-170">The sample creates a job with a call to `create_job`.</span><span class="sxs-lookup"><span data-stu-id="74475-170">The sample creates a job with a call to `create_job`.</span></span> <span data-ttu-id="74475-171">This defined function uses the [JobAddParameter](/python/api/azure.batch.models.jobaddparameter) class to create a job on your pool.</span><span class="sxs-lookup"><span data-stu-id="74475-171">This defined function uses the [JobAddParameter](/python/api/azure.batch.models.jobaddparameter) class to create a job on your pool.</span></span> <span data-ttu-id="74475-172">The [job.add](/python/api/azure.batch.operations.joboperations#azure_batch_operations_JobOperations_add) method submits the pool to the Batch service.</span><span class="sxs-lookup"><span data-stu-id="74475-172">The [job.add](/python/api/azure.batch.operations.joboperations#azure_batch_operations_JobOperations_add) method submits the pool to the Batch service.</span></span> <span data-ttu-id="74475-173">Initially the job has no tasks.</span><span class="sxs-lookup"><span data-stu-id="74475-173">Initially the job has no tasks.</span></span>

```python
job = batch.models.JobAddParameter(
    job_id,
    batch.models.PoolInformation(pool_id=pool_id))

batch_service_client.job.add(job)
```

### <a name="create-tasks"></a><span data-ttu-id="74475-174">Create tasks</span><span class="sxs-lookup"><span data-stu-id="74475-174">Create tasks</span></span>

<span data-ttu-id="74475-175">The app creates tasks in the job with a call to `add_tasks`.</span><span class="sxs-lookup"><span data-stu-id="74475-175">The app creates tasks in the job with a call to `add_tasks`.</span></span> <span data-ttu-id="74475-176">This defined function creates a list of task objects using the [TaskAddParameter](/python/api/azure.batch.models.taskaddparameter) class.</span><span class="sxs-lookup"><span data-stu-id="74475-176">This defined function creates a list of task objects using the [TaskAddParameter](/python/api/azure.batch.models.taskaddparameter) class.</span></span> <span data-ttu-id="74475-177">Each task runs ffmpeg to process an input `resource_files` object using a `command_line` parameter.</span><span class="sxs-lookup"><span data-stu-id="74475-177">Each task runs ffmpeg to process an input `resource_files` object using a `command_line` parameter.</span></span> <span data-ttu-id="74475-178">ffmpeg was previously installed on each node when the pool was created.</span><span class="sxs-lookup"><span data-stu-id="74475-178">ffmpeg was previously installed on each node when the pool was created.</span></span> <span data-ttu-id="74475-179">Here, the command line runs ffmpeg to convert each input MP4 (video) file to an MP3 (audio) file.</span><span class="sxs-lookup"><span data-stu-id="74475-179">Here, the command line runs ffmpeg to convert each input MP4 (video) file to an MP3 (audio) file.</span></span>

<span data-ttu-id="74475-180">The sample creates an [OutputFile](/python/api/azure.batch.models.outputfile) object for the MP3 file after running the command line.</span><span class="sxs-lookup"><span data-stu-id="74475-180">The sample creates an [OutputFile](/python/api/azure.batch.models.outputfile) object for the MP3 file after running the command line.</span></span> <span data-ttu-id="74475-181">Each task's output files (one, in this case) are uploaded to a container in the linked storage account, using the task's `output_files` property.</span><span class="sxs-lookup"><span data-stu-id="74475-181">Each task's output files (one, in this case) are uploaded to a container in the linked storage account, using the task's `output_files` property.</span></span>

<span data-ttu-id="74475-182">Then, the app adds tasks to the job with the [task.add_collection](/python/api/azure.batch.operations.taskoperations#azure_batch_operations_TaskOperations_add_collection) method, which queues them to run on the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="74475-182">Then, the app adds tasks to the job with the [task.add_collection](/python/api/azure.batch.operations.taskoperations#azure_batch_operations_TaskOperations_add_collection) method, which queues them to run on the compute nodes.</span></span> 

```python
tasks = list()

for idx, input_file in enumerate(input_files): 
    input_file_path=input_file.file_path
    output_file_path="".join((input_file_path).split('.')[:-1]) + '.mp3'
    command = "/bin/bash -c \"ffmpeg -i {} {} \"".format(input_file_path, output_file_path)
    tasks.append(batch.models.TaskAddParameter(
        id='Task{}'.format(idx),
        command_line=command,
        resource_files=[input_file],
        output_files=[batchmodels.OutputFile(output_file_path,
              destination=batchmodels.OutputFileDestination(
                container=batchmodels.OutputFileBlobContainerDestination(output_container_sas_url)),
              upload_options=batchmodels.OutputFileUploadOptions(
                batchmodels.OutputFileUploadCondition.task_success))]
            )
     )
batch_service_client.task.add_collection(job_id, tasks)
```    

### <a name="monitor-tasks"></a><span data-ttu-id="74475-183">Monitor tasks</span><span class="sxs-lookup"><span data-stu-id="74475-183">Monitor tasks</span></span>

<span data-ttu-id="74475-184">When tasks are added to a job, Batch automatically queues and schedules them for execution on compute nodes in the associated pool.</span><span class="sxs-lookup"><span data-stu-id="74475-184">When tasks are added to a job, Batch automatically queues and schedules them for execution on compute nodes in the associated pool.</span></span> <span data-ttu-id="74475-185">Based on the settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties.</span><span class="sxs-lookup"><span data-stu-id="74475-185">Based on the settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties.</span></span> 

<span data-ttu-id="74475-186">There are many approaches to monitoring task execution.</span><span class="sxs-lookup"><span data-stu-id="74475-186">There are many approaches to monitoring task execution.</span></span> <span data-ttu-id="74475-187">The `wait_for_tasks_to_complete` function in this example uses the [TaskState](/python/api/azure.batch.models.taskstate) object to monitor tasks for a certain state, in this case the completed state, within a time limit.</span><span class="sxs-lookup"><span data-stu-id="74475-187">The `wait_for_tasks_to_complete` function in this example uses the [TaskState](/python/api/azure.batch.models.taskstate) object to monitor tasks for a certain state, in this case the completed state, within a time limit.</span></span>

```python
while datetime.datetime.now() < timeout_expiration:
    print('.', end='')
    sys.stdout.flush()
    tasks = batch_service_client.task.list(job_id)

     incomplete_tasks = [task for task in tasks if
                         task.state != batchmodels.TaskState.completed]
    if not incomplete_tasks:
        print()
        return True
    else:
        time.sleep(1)
...
```

## <a name="clean-up-resources"></a><span data-ttu-id="74475-188">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="74475-188">Clean up resources</span></span>

<span data-ttu-id="74475-189">After it runs the tasks, the app automatically deletes the input storage container it created, and gives you the option to delete the Batch pool and job.</span><span class="sxs-lookup"><span data-stu-id="74475-189">After it runs the tasks, the app automatically deletes the input storage container it created, and gives you the option to delete the Batch pool and job.</span></span> <span data-ttu-id="74475-190">The BatchClient's [JobOperations](/python/api/azure.batch.operations.joboperations) and [PoolOperations](/python/api/azure.batch.operations.pooloperations) classes both have delete methods, which are called if you confirm deletion.</span><span class="sxs-lookup"><span data-stu-id="74475-190">The BatchClient's [JobOperations](/python/api/azure.batch.operations.joboperations) and [PoolOperations](/python/api/azure.batch.operations.pooloperations) classes both have delete methods, which are called if you confirm deletion.</span></span> <span data-ttu-id="74475-191">Although you're not charged for jobs and tasks themselves, you are charged for compute nodes.</span><span class="sxs-lookup"><span data-stu-id="74475-191">Although you're not charged for jobs and tasks themselves, you are charged for compute nodes.</span></span> <span data-ttu-id="74475-192">Thus, we recommend that you allocate pools only as needed.</span><span class="sxs-lookup"><span data-stu-id="74475-192">Thus, we recommend that you allocate pools only as needed.</span></span> <span data-ttu-id="74475-193">When you delete the pool, all task output on the nodes is deleted.</span><span class="sxs-lookup"><span data-stu-id="74475-193">When you delete the pool, all task output on the nodes is deleted.</span></span> <span data-ttu-id="74475-194">However, the input and output files remain in the storage account.</span><span class="sxs-lookup"><span data-stu-id="74475-194">However, the input and output files remain in the storage account.</span></span>

<span data-ttu-id="74475-195">When no longer needed, delete the resource group, Batch account, and storage account.</span><span class="sxs-lookup"><span data-stu-id="74475-195">When no longer needed, delete the resource group, Batch account, and storage account.</span></span> <span data-ttu-id="74475-196">To do so in the Azure portal, select the resource group for the Batch account and click **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="74475-196">To do so in the Azure portal, select the resource group for the Batch account and click **Delete resource group**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74475-197">Next steps</span><span class="sxs-lookup"><span data-stu-id="74475-197">Next steps</span></span>

<span data-ttu-id="74475-198">In this tutorial, you learned about how to:</span><span class="sxs-lookup"><span data-stu-id="74475-198">In this tutorial, you learned about how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="74475-199">Authenticate with Batch and Storage accounts</span><span class="sxs-lookup"><span data-stu-id="74475-199">Authenticate with Batch and Storage accounts</span></span>
> * <span data-ttu-id="74475-200">Upload input files to Storage</span><span class="sxs-lookup"><span data-stu-id="74475-200">Upload input files to Storage</span></span>
> * <span data-ttu-id="74475-201">Create a pool of compute nodes to run an application</span><span class="sxs-lookup"><span data-stu-id="74475-201">Create a pool of compute nodes to run an application</span></span>
> * <span data-ttu-id="74475-202">Create a job and tasks to process input files</span><span class="sxs-lookup"><span data-stu-id="74475-202">Create a job and tasks to process input files</span></span>
> * <span data-ttu-id="74475-203">Monitor task execution</span><span class="sxs-lookup"><span data-stu-id="74475-203">Monitor task execution</span></span>
> * <span data-ttu-id="74475-204">Retrieve output files</span><span class="sxs-lookup"><span data-stu-id="74475-204">Retrieve output files</span></span>

<span data-ttu-id="74475-205">For more examples of using the Python API to schedule and process Batch workloads, see the samples on GitHub.</span><span class="sxs-lookup"><span data-stu-id="74475-205">For more examples of using the Python API to schedule and process Batch workloads, see the samples on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="74475-206">Batch Python samples</span><span class="sxs-lookup"><span data-stu-id="74475-206">Batch Python samples</span></span>](https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch)

