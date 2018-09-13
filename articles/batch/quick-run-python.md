---
title: Azure Quickstart - Run Batch job - Python
description: Quickly run a Batch job and tasks using the Batch Python client library.
services: batch
author: dlepow
manager: jeconnoc
ms.service: batch
ms.devlang: python
ms.topic: quickstart
ms.date: 01/19/2018
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 85be7763535b8b067c5a52729fb2be855ffa4b77
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857785"
---
# <a name="quickstart-run-your-first-batch-job-with-the-python-api"></a><span data-ttu-id="8af41-103">Quickstart: Run your first Batch job with the Python API</span><span class="sxs-lookup"><span data-stu-id="8af41-103">Quickstart: Run your first Batch job with the Python API</span></span>

<span data-ttu-id="8af41-104">This quickstart runs an Azure Batch job from an application built on the Azure Batch Python API.</span><span class="sxs-lookup"><span data-stu-id="8af41-104">This quickstart runs an Azure Batch job from an application built on the Azure Batch Python API.</span></span> <span data-ttu-id="8af41-105">The app uploads several input data files to Azure storage and then creates a *pool* of Batch compute nodes (virtual machines).</span><span class="sxs-lookup"><span data-stu-id="8af41-105">The app uploads several input data files to Azure storage and then creates a *pool* of Batch compute nodes (virtual machines).</span></span> <span data-ttu-id="8af41-106">Then, it creates a sample *job* that runs *tasks* to process each input file on the pool using a basic command.</span><span class="sxs-lookup"><span data-stu-id="8af41-106">Then, it creates a sample *job* that runs *tasks* to process each input file on the pool using a basic command.</span></span> <span data-ttu-id="8af41-107">After completing this quickstart, you will understand the key concepts of the Batch service and be ready to try Batch with more realistic workloads at larger scale.</span><span class="sxs-lookup"><span data-stu-id="8af41-107">After completing this quickstart, you will understand the key concepts of the Batch service and be ready to try Batch with more realistic workloads at larger scale.</span></span>
 
![Quickstart app workflow](./media/quick-run-python/sampleapp.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="8af41-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8af41-109">Prerequisites</span></span>

* [<span data-ttu-id="8af41-110">Python version 2.7 or 3.3 or later</span><span class="sxs-lookup"><span data-stu-id="8af41-110">Python version 2.7 or 3.3 or later</span></span>](https://www.python.org/downloads/)

* <span data-ttu-id="8af41-111">[pip](https://pip.pypa.io/en/stable/installing/) package manager</span><span class="sxs-lookup"><span data-stu-id="8af41-111">[pip](https://pip.pypa.io/en/stable/installing/) package manager</span></span>

* <span data-ttu-id="8af41-112">An Azure Batch account and a linked Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="8af41-112">An Azure Batch account and a linked Azure Storage account.</span></span> <span data-ttu-id="8af41-113">To create these accounts, see the Batch quickstarts using the [Azure portal](quick-create-portal.md) or [Azure CLI](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8af41-113">To create these accounts, see the Batch quickstarts using the [Azure portal](quick-create-portal.md) or [Azure CLI](quick-create-cli.md).</span></span> 

## <a name="sign-in-to-azure"></a><span data-ttu-id="8af41-114">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="8af41-114">Sign in to Azure</span></span>

<span data-ttu-id="8af41-115">Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8af41-115">Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>

[!INCLUDE [batch-common-credentials](../../includes/batch-common-credentials.md)]

## <a name="download-the-sample"></a><span data-ttu-id="8af41-116">Download the sample</span><span class="sxs-lookup"><span data-stu-id="8af41-116">Download the sample</span></span>

<span data-ttu-id="8af41-117">[Download or clone the sample app](https://github.com/Azure-Samples/batch-python-quickstart) from GitHub.</span><span class="sxs-lookup"><span data-stu-id="8af41-117">[Download or clone the sample app](https://github.com/Azure-Samples/batch-python-quickstart) from GitHub.</span></span> <span data-ttu-id="8af41-118">To clone the sample app repo with a Git client, use the following command:</span><span class="sxs-lookup"><span data-stu-id="8af41-118">To clone the sample app repo with a Git client, use the following command:</span></span>

```
git clone https://github.com/Azure-Samples/batch-python-quickstart.git
```

<span data-ttu-id="8af41-119">Navigate to the directory that contains the Python script `python_quickstart_client.py`.</span><span class="sxs-lookup"><span data-stu-id="8af41-119">Navigate to the directory that contains the Python script `python_quickstart_client.py`.</span></span>

<span data-ttu-id="8af41-120">In your Python development environment, install the required packages using `pip`.</span><span class="sxs-lookup"><span data-stu-id="8af41-120">In your Python development environment, install the required packages using `pip`.</span></span>

```bash
pip install -r requirements.txt
```

<span data-ttu-id="8af41-121">Open the file `python_quickstart_client.py`.</span><span class="sxs-lookup"><span data-stu-id="8af41-121">Open the file `python_quickstart_client.py`.</span></span> <span data-ttu-id="8af41-122">Update the Batch and storage account credential strings with the values you obtained for your accounts.</span><span class="sxs-lookup"><span data-stu-id="8af41-122">Update the Batch and storage account credential strings with the values you obtained for your accounts.</span></span> <span data-ttu-id="8af41-123">For example:</span><span class="sxs-lookup"><span data-stu-id="8af41-123">For example:</span></span>


```Python
_BATCH_ACCOUNT_NAME = 'mybatchaccount'
_BATCH_ACCOUNT_KEY = 'xxxxxxxxxxxxxxxxE+yXrRvJAqT9BlXwwo1CwF+SwAYOxxxxxxxxxxxxxxxx43pXi/gdiATkvbpLRl3x14pcEQ=='
_BATCH_ACCOUNT_URL = 'https://mybatchaccount.mybatchregion.batch.azure.com'
_STORAGE_ACCOUNT_NAME = 'mystorageaccount'
_STORAGE_ACCOUNT_KEY = 'xxxxxxxxxxxxxxxxy4/xxxxxxxxxxxxxxxxfwpbIC5aAWA8wDu+AFXZB827Mt9lybZB1nUcQbQiUrkPtilK5BQ=='
```

## <a name="run-the-app"></a><span data-ttu-id="8af41-124">Run the app</span><span class="sxs-lookup"><span data-stu-id="8af41-124">Run the app</span></span>

<span data-ttu-id="8af41-125">To see the Batch workflow in action, run the script:</span><span class="sxs-lookup"><span data-stu-id="8af41-125">To see the Batch workflow in action, run the script:</span></span>

```
python python_quickstart_client.py
```

<span data-ttu-id="8af41-126">After running the script, review the code to learn what each part of the application does.</span><span class="sxs-lookup"><span data-stu-id="8af41-126">After running the script, review the code to learn what each part of the application does.</span></span> 

<span data-ttu-id="8af41-127">When you run the sample application, the console output is similar to the following.</span><span class="sxs-lookup"><span data-stu-id="8af41-127">When you run the sample application, the console output is similar to the following.</span></span> <span data-ttu-id="8af41-128">During execution, you experience a pause at `Monitoring all tasks for 'Completed' state, timeout in 00:30:00...` while the pool's compute nodes are started.</span><span class="sxs-lookup"><span data-stu-id="8af41-128">During execution, you experience a pause at `Monitoring all tasks for 'Completed' state, timeout in 00:30:00...` while the pool's compute nodes are started.</span></span> <span data-ttu-id="8af41-129">Tasks are queued to run as soon as the first compute node is running.</span><span class="sxs-lookup"><span data-stu-id="8af41-129">Tasks are queued to run as soon as the first compute node is running.</span></span> <span data-ttu-id="8af41-130">Go to your Batch account in the [Azure portal](https://portal.azure.com) to monitor the pool, compute nodes, job, and tasks in your Batch account.</span><span class="sxs-lookup"><span data-stu-id="8af41-130">Go to your Batch account in the [Azure portal](https://portal.azure.com) to monitor the pool, compute nodes, job, and tasks in your Batch account.</span></span>

```
Sample start: 12/4/2017 4:02:54 PM

Container [input] created.
Uploading file taskdata0.txt to container [input]...
Uploading file taskdata1.txt to container [input]...
Uploading file taskdata2.txt to container [input]...
Creating pool [PythonQuickstartPool]...
Creating job [PythonQuickstartJob]...
Adding 3 tasks to job [PythonQuickstartJob]...
Monitoring all tasks for 'Completed' state, timeout in 00:30:00...
```

<span data-ttu-id="8af41-131">After tasks complete, you see output similar to the following for each task:</span><span class="sxs-lookup"><span data-stu-id="8af41-131">After tasks complete, you see output similar to the following for each task:</span></span>

```
Printing task output...
Task: Task0
Node: tvm-2850684224_3-20171205t000401z
Standard out:
Batch processing began with mainframe computers and punch cards. Today it still plays a central role in business, engineering, science, and other pursuits that require running lots of automated tasks....
...
```

<span data-ttu-id="8af41-132">Typical execution time is approximately 3 minutes when you run the application in its default configuration.</span><span class="sxs-lookup"><span data-stu-id="8af41-132">Typical execution time is approximately 3 minutes when you run the application in its default configuration.</span></span> <span data-ttu-id="8af41-133">Initial pool setup takes the most time.</span><span class="sxs-lookup"><span data-stu-id="8af41-133">Initial pool setup takes the most time.</span></span>

## <a name="review-the-code"></a><span data-ttu-id="8af41-134">Review the code</span><span class="sxs-lookup"><span data-stu-id="8af41-134">Review the code</span></span>

<span data-ttu-id="8af41-135">The Python app in this quickstart does the following:</span><span class="sxs-lookup"><span data-stu-id="8af41-135">The Python app in this quickstart does the following:</span></span>

* <span data-ttu-id="8af41-136">Uploads three small text files to a blob container in your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="8af41-136">Uploads three small text files to a blob container in your Azure storage account.</span></span> <span data-ttu-id="8af41-137">These files are inputs for processing by Batch tasks.</span><span class="sxs-lookup"><span data-stu-id="8af41-137">These files are inputs for processing by Batch tasks.</span></span>
* <span data-ttu-id="8af41-138">Creates a pool of two compute nodes running Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="8af41-138">Creates a pool of two compute nodes running Ubuntu 16.04 LTS.</span></span>
* <span data-ttu-id="8af41-139">Creates a job and three tasks to run on the nodes.</span><span class="sxs-lookup"><span data-stu-id="8af41-139">Creates a job and three tasks to run on the nodes.</span></span> <span data-ttu-id="8af41-140">Each task processes one of the input files using a Bash shell command line.</span><span class="sxs-lookup"><span data-stu-id="8af41-140">Each task processes one of the input files using a Bash shell command line.</span></span>
* <span data-ttu-id="8af41-141">Displays files returned by the tasks.</span><span class="sxs-lookup"><span data-stu-id="8af41-141">Displays files returned by the tasks.</span></span>

<span data-ttu-id="8af41-142">See the file `python_quickstart_client.py` and the following sections for details.</span><span class="sxs-lookup"><span data-stu-id="8af41-142">See the file `python_quickstart_client.py` and the following sections for details.</span></span> 

### <a name="preliminaries"></a><span data-ttu-id="8af41-143">Preliminaries</span><span class="sxs-lookup"><span data-stu-id="8af41-143">Preliminaries</span></span>

<span data-ttu-id="8af41-144">To interact with a storage account, the app uses the [azure-storage-blob](https://pypi.python.org/pypi/azure-storage-blob) package to create a [BlockBlobService](/python/api/azure.storage.blob.blockblobservice.blockblobservice) object.</span><span class="sxs-lookup"><span data-stu-id="8af41-144">To interact with a storage account, the app uses the [azure-storage-blob](https://pypi.python.org/pypi/azure-storage-blob) package to create a [BlockBlobService](/python/api/azure.storage.blob.blockblobservice.blockblobservice) object.</span></span>

```python
blob_client = azureblob.BlockBlobService(
    account_name=_STORAGE_ACCOUNT_NAME,
    account_key=_STORAGE_ACCOUNT_KEY)
```

<span data-ttu-id="8af41-145">The app uses the `blob_client` reference to create a container in the storage account and to upload data files to the container.</span><span class="sxs-lookup"><span data-stu-id="8af41-145">The app uses the `blob_client` reference to create a container in the storage account and to upload data files to the container.</span></span> <span data-ttu-id="8af41-146">The files in storage are defined as Batch [ResourceFile](/python/api/azure.batch.models.resourcefile) objects that Batch can later download to compute nodes.</span><span class="sxs-lookup"><span data-stu-id="8af41-146">The files in storage are defined as Batch [ResourceFile](/python/api/azure.batch.models.resourcefile) objects that Batch can later download to compute nodes.</span></span>

```python
input_file_paths = [os.path.realpath('./data/taskdata0.txt'),
                    os.path.realpath('./data/taskdata1.txt'),
                    os.path.realpath('./data/taskdata2.txt')]
input_files = [
    upload_file_to_container(blob_client, input_container_name, file_path)
    for file_path in input_file_paths]
```

<span data-ttu-id="8af41-147">The app creates a [BatchServiceClient](/python/api/azure.batch.batchserviceclient) object to create and manage pools, jobs, and tasks in the Batch service.</span><span class="sxs-lookup"><span data-stu-id="8af41-147">The app creates a [BatchServiceClient](/python/api/azure.batch.batchserviceclient) object to create and manage pools, jobs, and tasks in the Batch service.</span></span> <span data-ttu-id="8af41-148">The Batch client in the sample uses shared key authentication.</span><span class="sxs-lookup"><span data-stu-id="8af41-148">The Batch client in the sample uses shared key authentication.</span></span> <span data-ttu-id="8af41-149">Batch also supports Azure Active Directory authentication.</span><span class="sxs-lookup"><span data-stu-id="8af41-149">Batch also supports Azure Active Directory authentication.</span></span>

```python
credentials = batchauth.SharedKeyCredentials(_BATCH_ACCOUNT_NAME,
    BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=_BATCH_ACCOUNT_URL)
```


### <a name="create-a-pool-of-compute-nodes"></a><span data-ttu-id="8af41-150">Create a pool of compute nodes</span><span class="sxs-lookup"><span data-stu-id="8af41-150">Create a pool of compute nodes</span></span>

<span data-ttu-id="8af41-151">To create a Batch pool, the app uses the [PoolAddParameter](/python/api/azure.batch.models.pooladdparameter) class to set the number of nodes, VM size, and a pool configuration.</span><span class="sxs-lookup"><span data-stu-id="8af41-151">To create a Batch pool, the app uses the [PoolAddParameter](/python/api/azure.batch.models.pooladdparameter) class to set the number of nodes, VM size, and a pool configuration.</span></span> <span data-ttu-id="8af41-152">Here, a [VirtualMachineConfiguration](/python/api/azure.batch.models.virtualmachineconfiguration) object specifies an [ImageReference](/python/api/azure.batch.models.imagereference) to an Ubuntu Server 16.04 LTS image published in the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="8af41-152">Here, a [VirtualMachineConfiguration](/python/api/azure.batch.models.virtualmachineconfiguration) object specifies an [ImageReference](/python/api/azure.batch.models.imagereference) to an Ubuntu Server 16.04 LTS image published in the Azure Marketplace.</span></span> <span data-ttu-id="8af41-153">Batch supports a wide range of Linux and Windows Server images in the Azure Marketplace, as well as custom VM images.</span><span class="sxs-lookup"><span data-stu-id="8af41-153">Batch supports a wide range of Linux and Windows Server images in the Azure Marketplace, as well as custom VM images.</span></span>

<span data-ttu-id="8af41-154">The number of nodes (`_POOL_NODE_COUNT`) and VM size (`_POOL_VM_SIZE`) are defined constants.</span><span class="sxs-lookup"><span data-stu-id="8af41-154">The number of nodes (`_POOL_NODE_COUNT`) and VM size (`_POOL_VM_SIZE`) are defined constants.</span></span> <span data-ttu-id="8af41-155">The sample by default creates a pool of 2 size *Standard_A1_v2* nodes.</span><span class="sxs-lookup"><span data-stu-id="8af41-155">The sample by default creates a pool of 2 size *Standard_A1_v2* nodes.</span></span> <span data-ttu-id="8af41-156">The size suggested offers a good balance of performance versus cost for this quick example.</span><span class="sxs-lookup"><span data-stu-id="8af41-156">The size suggested offers a good balance of performance versus cost for this quick example.</span></span>

<span data-ttu-id="8af41-157">The [pool.add](/python/api/azure.batch.operations.pooloperations#azure_batch_operations_PoolOperations_add) method submits the pool to the Batch service.</span><span class="sxs-lookup"><span data-stu-id="8af41-157">The [pool.add](/python/api/azure.batch.operations.pooloperations#azure_batch_operations_PoolOperations_add) method submits the pool to the Batch service.</span></span>

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
    target_dedicated_nodes=_POOL_NODE_COUNT
)
batch_service_client.pool.add(new_pool)
```

### <a name="create-a-batch-job"></a><span data-ttu-id="8af41-158">Create a Batch job</span><span class="sxs-lookup"><span data-stu-id="8af41-158">Create a Batch job</span></span>

<span data-ttu-id="8af41-159">A Batch job is a logical grouping of one or more tasks.</span><span class="sxs-lookup"><span data-stu-id="8af41-159">A Batch job is a logical grouping of one or more tasks.</span></span> <span data-ttu-id="8af41-160">A job includes settings common to the tasks, such as priority and the pool to run tasks on.</span><span class="sxs-lookup"><span data-stu-id="8af41-160">A job includes settings common to the tasks, such as priority and the pool to run tasks on.</span></span> <span data-ttu-id="8af41-161">The app uses the [JobAddParameter](/python/api/azure.batch.models.jobaddparameter) class to create a job on your pool.</span><span class="sxs-lookup"><span data-stu-id="8af41-161">The app uses the [JobAddParameter](/python/api/azure.batch.models.jobaddparameter) class to create a job on your pool.</span></span> <span data-ttu-id="8af41-162">The [job.add](/python/api/azure.batch.operations.joboperations#azure_batch_operations_JobOperations_add) method submits the pool to the Batch service.</span><span class="sxs-lookup"><span data-stu-id="8af41-162">The [job.add](/python/api/azure.batch.operations.joboperations#azure_batch_operations_JobOperations_add) method submits the pool to the Batch service.</span></span> <span data-ttu-id="8af41-163">Initially the job has no tasks.</span><span class="sxs-lookup"><span data-stu-id="8af41-163">Initially the job has no tasks.</span></span>

```python
job = batch.models.JobAddParameter(
    job_id,
    batch.models.PoolInformation(pool_id=pool_id))
batch_service_client.job.add(job)
```

### <a name="create-tasks"></a><span data-ttu-id="8af41-164">Create tasks</span><span class="sxs-lookup"><span data-stu-id="8af41-164">Create tasks</span></span>

<span data-ttu-id="8af41-165">The app creates a list of task objects using the [TaskAddParameter](/python/api/azure.batch.models.taskaddparameter) class.</span><span class="sxs-lookup"><span data-stu-id="8af41-165">The app creates a list of task objects using the [TaskAddParameter](/python/api/azure.batch.models.taskaddparameter) class.</span></span> <span data-ttu-id="8af41-166">Each task processes an input `resource_files` object using a `command_line` parameter.</span><span class="sxs-lookup"><span data-stu-id="8af41-166">Each task processes an input `resource_files` object using a `command_line` parameter.</span></span> <span data-ttu-id="8af41-167">In the sample, the command line runs the Bash shell `cat` command to display the text file.</span><span class="sxs-lookup"><span data-stu-id="8af41-167">In the sample, the command line runs the Bash shell `cat` command to display the text file.</span></span> <span data-ttu-id="8af41-168">This command is a simple example for demonstration purposes.</span><span class="sxs-lookup"><span data-stu-id="8af41-168">This command is a simple example for demonstration purposes.</span></span> <span data-ttu-id="8af41-169">When you use Batch, the command line is where you specify your app or script.</span><span class="sxs-lookup"><span data-stu-id="8af41-169">When you use Batch, the command line is where you specify your app or script.</span></span> <span data-ttu-id="8af41-170">Batch provides a number of ways to deploy apps and scripts to compute nodes.</span><span class="sxs-lookup"><span data-stu-id="8af41-170">Batch provides a number of ways to deploy apps and scripts to compute nodes.</span></span>

<span data-ttu-id="8af41-171">Then, the app adds tasks to the job with the [task.add_collection](/python/api/azure.batch.operations.taskoperations#azure_batch_operations_TaskOperations_add_collection) method, which queues them to run on the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="8af41-171">Then, the app adds tasks to the job with the [task.add_collection](/python/api/azure.batch.operations.taskoperations#azure_batch_operations_TaskOperations_add_collection) method, which queues them to run on the compute nodes.</span></span> 

```python
tasks = list()

for idx, input_file in enumerate(input_files): 
    command = "/bin/bash -c \"cat {}\"".format(input_file.file_path)
    tasks.append(batch.models.TaskAddParameter(
        id='Task{}'.format(idx),
        command_line=command,
        resource_files=[input_file]
    )
)
batch_service_client.task.add_collection(job_id, tasks)
```

### <a name="view-task-output"></a><span data-ttu-id="8af41-172">View task output</span><span class="sxs-lookup"><span data-stu-id="8af41-172">View task output</span></span>

<span data-ttu-id="8af41-173">The app monitors task state to make sure the tasks complete.</span><span class="sxs-lookup"><span data-stu-id="8af41-173">The app monitors task state to make sure the tasks complete.</span></span> <span data-ttu-id="8af41-174">Then, the app displays the `stdout.txt` file generated by each completed task.</span><span class="sxs-lookup"><span data-stu-id="8af41-174">Then, the app displays the `stdout.txt` file generated by each completed task.</span></span> <span data-ttu-id="8af41-175">When the task runs successfully, the output of the task command is written to `stdout.txt`:</span><span class="sxs-lookup"><span data-stu-id="8af41-175">When the task runs successfully, the output of the task command is written to `stdout.txt`:</span></span>

```python
tasks = batch_service_client.task.list(job_id)

for task in tasks:
    
    node_id = batch_service_client.task.get(job_id, task.id).node_info.node_id
    print("Task: {}".format(task.id))
    print("Node: {}".format(node_id))

    stream = batch_service_client.file.get_from_task(job_id, task.id, _STANDARD_OUT_FILE_NAME)

    file_text = _read_stream_as_string(
        stream,
        encoding)
    print("Standard output:")
    print(file_text)
```

## <a name="clean-up-resources"></a><span data-ttu-id="8af41-176">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="8af41-176">Clean up resources</span></span>

<span data-ttu-id="8af41-177">The app automatically deletes the storage container it creates, and gives you the option to delete the Batch pool and job.</span><span class="sxs-lookup"><span data-stu-id="8af41-177">The app automatically deletes the storage container it creates, and gives you the option to delete the Batch pool and job.</span></span> <span data-ttu-id="8af41-178">You are charged for the pool while the nodes are running, even if no jobs are scheduled.</span><span class="sxs-lookup"><span data-stu-id="8af41-178">You are charged for the pool while the nodes are running, even if no jobs are scheduled.</span></span> <span data-ttu-id="8af41-179">When you no longer need the pool, delete it.</span><span class="sxs-lookup"><span data-stu-id="8af41-179">When you no longer need the pool, delete it.</span></span> <span data-ttu-id="8af41-180">When you delete the pool, all task output on the nodes is deleted.</span><span class="sxs-lookup"><span data-stu-id="8af41-180">When you delete the pool, all task output on the nodes is deleted.</span></span> 

<span data-ttu-id="8af41-181">When no longer needed, delete the resource group, Batch account, and storage account.</span><span class="sxs-lookup"><span data-stu-id="8af41-181">When no longer needed, delete the resource group, Batch account, and storage account.</span></span> <span data-ttu-id="8af41-182">To do so in the Azure portal, select the resource group for the Batch account and click **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="8af41-182">To do so in the Azure portal, select the resource group for the Batch account and click **Delete resource group**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8af41-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="8af41-183">Next steps</span></span>

<span data-ttu-id="8af41-184">In this quickstart, you ran a small app built using the Batch Python API to create a Batch pool and a Batch job.</span><span class="sxs-lookup"><span data-stu-id="8af41-184">In this quickstart, you ran a small app built using the Batch Python API to create a Batch pool and a Batch job.</span></span> <span data-ttu-id="8af41-185">The job ran sample tasks, and downloaded output created on the nodes.</span><span class="sxs-lookup"><span data-stu-id="8af41-185">The job ran sample tasks, and downloaded output created on the nodes.</span></span> <span data-ttu-id="8af41-186">Now that you understand the key concepts of the Batch service, you are ready to try Batch with more realistic workloads at larger scale.</span><span class="sxs-lookup"><span data-stu-id="8af41-186">Now that you understand the key concepts of the Batch service, you are ready to try Batch with more realistic workloads at larger scale.</span></span> <span data-ttu-id="8af41-187">To learn more about Azure Batch, and walk through a parallel workload with a real-world application, continue to the Batch Python tutorial.</span><span class="sxs-lookup"><span data-stu-id="8af41-187">To learn more about Azure Batch, and walk through a parallel workload with a real-world application, continue to the Batch Python tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8af41-188">Process a parallel workload with Python</span><span class="sxs-lookup"><span data-stu-id="8af41-188">Process a parallel workload with Python</span></span>](tutorial-parallel-python.md)
