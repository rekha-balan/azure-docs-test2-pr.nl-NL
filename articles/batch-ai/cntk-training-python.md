---
title: Train a CNTK model with Azure Batch AI - Python | Microsoft Docs
description: Train a Microsoft Cognitive Toolkit (CNTK) neural network with Azure Batch AI using the Python SDK
services: batch-ai
documentationcenter: na
author: lliimsft
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.custom: ''
ms.service: batch-ai
ms.workload: ''
ms.tgt_pltfrm: na
ms.devlang: Python
ms.topic: quickstart
ms.date: 08/15/2018
ms.author: danlep
ms.openlocfilehash: 0c805deb85a999d3c23be24b81c1d97ed5fe55eb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856082"
---
# <a name="run-a-cntk-training-job-using-the-azure-python-sdk"></a><span data-ttu-id="55132-103">Run a CNTK training job using the Azure Python SDK</span><span class="sxs-lookup"><span data-stu-id="55132-103">Run a CNTK training job using the Azure Python SDK</span></span>

<span data-ttu-id="55132-104">This article shows you how to use the Azure Python SDK to train a sample Microsoft Cognitive Toolkit (CNTK) model using the Batch AI service.</span><span class="sxs-lookup"><span data-stu-id="55132-104">This article shows you how to use the Azure Python SDK to train a sample Microsoft Cognitive Toolkit (CNTK) model using the Batch AI service.</span></span>

<span data-ttu-id="55132-105">In this example, you use the MNIST database of handwritten images to train a convolutional neural network (CNN) on a single-node GPU cluster.</span><span class="sxs-lookup"><span data-stu-id="55132-105">In this example, you use the MNIST database of handwritten images to train a convolutional neural network (CNN) on a single-node GPU cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55132-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="55132-106">Prerequisites</span></span>

* <span data-ttu-id="55132-107">Azure subscription - If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="55132-107">Azure subscription - If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

* <span data-ttu-id="55132-108">Azure Python SDK - See [installation instructions](/python/azure/python-sdk-azure-install).</span><span class="sxs-lookup"><span data-stu-id="55132-108">Azure Python SDK - See [installation instructions](/python/azure/python-sdk-azure-install).</span></span> <span data-ttu-id="55132-109">This article requires at least azure-mgmt-batchai package version 2.0.0.</span><span class="sxs-lookup"><span data-stu-id="55132-109">This article requires at least azure-mgmt-batchai package version 2.0.0.</span></span>

* <span data-ttu-id="55132-110">Azure storage account - See [How to create an Azure storage account](../storage/common/storage-create-storage-account.md)</span><span class="sxs-lookup"><span data-stu-id="55132-110">Azure storage account - See [How to create an Azure storage account](../storage/common/storage-create-storage-account.md)</span></span>

* <span data-ttu-id="55132-111">Azure Active Directory service principal credentials - See [How to create a service principal with the CLI](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)</span><span class="sxs-lookup"><span data-stu-id="55132-111">Azure Active Directory service principal credentials - See [How to create a service principal with the CLI](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)</span></span>

* <span data-ttu-id="55132-112">Register the Batch AI resource provider once for your subscription using Azure Cloud Shell or the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="55132-112">Register the Batch AI resource provider once for your subscription using Azure Cloud Shell or the Azure CLI.</span></span> <span data-ttu-id="55132-113">A provider registration can take up to 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="55132-113">A provider registration can take up to 15 minutes.</span></span>

```azurecli
az provider register -n Microsoft.BatchAI
```

## <a name="configure-credentials"></a><span data-ttu-id="55132-114">Configure credentials</span><span class="sxs-lookup"><span data-stu-id="55132-114">Configure credentials</span></span>

<span data-ttu-id="55132-115">Add the following code into your script file and replace `FILL-IN-HERE` with appropriate values:</span><span class="sxs-lookup"><span data-stu-id="55132-115">Add the following code into your script file and replace `FILL-IN-HERE` with appropriate values:</span></span>

```Python
# credentials used for authentication
aad_client_id = 'FILL-IN-HERE'
aad_secret = 'FILL-IN-HERE'
aad_tenant = 'FILL-IN-HERE'
subscription_id = 'FILL-IN-HERE'

# credentials used for storage
storage_account_name = 'FILL-IN-HERE'
storage_account_key = 'FILL-IN-HERE'

# specify the credentials used to remote login your GPU node
admin_user_name = 'FILL-IN-HERE'
admin_user_password = 'FILL-IN-HERE'

# specify the location in which to create Batch AI resources
mylocation = 'eastus'
```

<span data-ttu-id="55132-116">Note, that putting credentials into the source code is not a good practice and it's done here to make the quickstart simpler.</span><span class="sxs-lookup"><span data-stu-id="55132-116">Note, that putting credentials into the source code is not a good practice and it's done here to make the quickstart simpler.</span></span>
<span data-ttu-id="55132-117">Consider to use environment variables or a separate configuration file instead.</span><span class="sxs-lookup"><span data-stu-id="55132-117">Consider to use environment variables or a separate configuration file instead.</span></span>

## <a name="create-batch-ai-client"></a><span data-ttu-id="55132-118">Create Batch AI client</span><span class="sxs-lookup"><span data-stu-id="55132-118">Create Batch AI client</span></span>

<span data-ttu-id="55132-119">The following code creates a service principal credentials object and Batch AI client:</span><span class="sxs-lookup"><span data-stu-id="55132-119">The following code creates a service principal credentials object and Batch AI client:</span></span>

```Python
from azure.common.credentials import ServicePrincipalCredentials
import azure.mgmt.batchai as batchai
import azure.mgmt.batchai.models as models

creds = ServicePrincipalCredentials(
        client_id=aad_client_id, secret=aad_secret, tenant=aad_tenant)

batchai_client = batchai.BatchAIManagementClient(
    credentials=creds, subscription_id=subscription_id)
```

## <a name="create-a-resource-group"></a><span data-ttu-id="55132-120">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="55132-120">Create a resource group</span></span>

<span data-ttu-id="55132-121">Batch AI clusters and jobs are Azure resources and must be placed in an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="55132-121">Batch AI clusters and jobs are Azure resources and must be placed in an Azure resource group.</span></span> <span data-ttu-id="55132-122">The following snippet creates a resource group:</span><span class="sxs-lookup"><span data-stu-id="55132-122">The following snippet creates a resource group:</span></span>

```Python
from azure.mgmt.resource import ResourceManagementClient

resource_group_name = 'myresourcegroup'
resource_management_client = ResourceManagementClient(
        credentials=creds, subscription_id=subscription_id)
resource = resource_management_client.resource_groups.create_or_update(
        resource_group_name, {'location': mylocation})
```


## <a name="prepare-azure-file-share"></a><span data-ttu-id="55132-123">Prepare Azure file share</span><span class="sxs-lookup"><span data-stu-id="55132-123">Prepare Azure file share</span></span>

<span data-ttu-id="55132-124">For illustration purposes, this quickstart uses an Azure File share to host the training data and scripts for the training job.</span><span class="sxs-lookup"><span data-stu-id="55132-124">For illustration purposes, this quickstart uses an Azure File share to host the training data and scripts for the training job.</span></span>

<span data-ttu-id="55132-125">Create a file share named `batchaiquickstart`.</span><span class="sxs-lookup"><span data-stu-id="55132-125">Create a file share named `batchaiquickstart`.</span></span>

```Python
from azure.storage.file import FileService
azure_file_share_name = 'batchaiquickstart'
service = FileService(storage_account_name, storage_account_key)
service.create_share(azure_file_share_name, fail_on_exist=False)
```

<span data-ttu-id="55132-126">Create a directory in the share named `mnistcntksample`.</span><span class="sxs-lookup"><span data-stu-id="55132-126">Create a directory in the share named `mnistcntksample`.</span></span>

```Python
mnist_dataset_directory = 'mnistcntksample'
service.create_directory(azure_file_share_name, mnist_dataset_directory, fail_on_exist=False)
```
<span data-ttu-id="55132-127">Download the [sample package](https://batchaisamples.blob.core.windows.net/samples/BatchAIQuickStart.zip?st=2017-09-29T18%3A29%3A00Z&se=2099-12-31T08%3A00%3A00Z&sp=rl&sv=2016-05-31&sr=b&sig=hrAZfbZC%2BQ%2FKccFQZ7OC4b%2FXSzCF5Myi4Cj%2BW3sVZDo%3D) and unzip into the current directory.</span><span class="sxs-lookup"><span data-stu-id="55132-127">Download the [sample package](https://batchaisamples.blob.core.windows.net/samples/BatchAIQuickStart.zip?st=2017-09-29T18%3A29%3A00Z&se=2099-12-31T08%3A00%3A00Z&sp=rl&sv=2016-05-31&sr=b&sig=hrAZfbZC%2BQ%2FKccFQZ7OC4b%2FXSzCF5Myi4Cj%2BW3sVZDo%3D) and unzip into the current directory.</span></span> <span data-ttu-id="55132-128">The following code uploads required files into the Azure File share:</span><span class="sxs-lookup"><span data-stu-id="55132-128">The following code uploads required files into the Azure File share:</span></span>

```Python
for f in ['Train-28x28_cntk_text.txt', 'Test-28x28_cntk_text.txt',
          'ConvNet_MNIST.py']:
     service.create_file_from_path(
             azure_file_share_name, mnist_dataset_directory, f, f)
```

## <a name="create-batch-ai-workspace"></a><span data-ttu-id="55132-129">Create Batch AI workspace</span><span class="sxs-lookup"><span data-stu-id="55132-129">Create Batch AI workspace</span></span>

<span data-ttu-id="55132-130">A workspace is a top-level collection of all types of Batch AI resources.</span><span class="sxs-lookup"><span data-stu-id="55132-130">A workspace is a top-level collection of all types of Batch AI resources.</span></span> <span data-ttu-id="55132-131">You create your Batch AI cluster and experiments in a workspace.</span><span class="sxs-lookup"><span data-stu-id="55132-131">You create your Batch AI cluster and experiments in a workspace.</span></span>

```Python
workspace_name='myworkspace'
batchai_client.workspaces.create(resource_group_name, workspace_name, mylocation)
```

## <a name="create-gpu-cluster"></a><span data-ttu-id="55132-132">Create GPU cluster</span><span class="sxs-lookup"><span data-stu-id="55132-132">Create GPU cluster</span></span>

<span data-ttu-id="55132-133">Create a Batch AI cluster.</span><span class="sxs-lookup"><span data-stu-id="55132-133">Create a Batch AI cluster.</span></span> <span data-ttu-id="55132-134">In this example, the cluster consists of a single STANDARD_NC6 VM node.</span><span class="sxs-lookup"><span data-stu-id="55132-134">In this example, the cluster consists of a single STANDARD_NC6 VM node.</span></span> <span data-ttu-id="55132-135">This VM size has one NVIDIA K80 GPU.</span><span class="sxs-lookup"><span data-stu-id="55132-135">This VM size has one NVIDIA K80 GPU.</span></span> <span data-ttu-id="55132-136">Mount the file share at a folder named `azurefileshare`.</span><span class="sxs-lookup"><span data-stu-id="55132-136">Mount the file share at a folder named `azurefileshare`.</span></span> <span data-ttu-id="55132-137">The full path of this folder on the GPU compute node is `$AZ_BATCHAI_MOUNT_ROOT/azurefileshare`.</span><span class="sxs-lookup"><span data-stu-id="55132-137">The full path of this folder on the GPU compute node is `$AZ_BATCHAI_MOUNT_ROOT/azurefileshare`.</span></span>

```Python
cluster_name = 'mycluster'

relative_mount_point = 'azurefileshare'

parameters = models.ClusterCreateParameters(
    # VM size. Use N-series for GPU
    vm_size='STANDARD_NC6',
    # Configure the ssh users
    user_account_settings=models.UserAccountSettings(
        admin_user_name=admin_user_name,
        admin_user_password=admin_user_password),
    # Number of VMs in the cluster
    scale_settings=models.ScaleSettings(
        manual=models.ManualScaleSettings(target_node_count=1)
    ),
    # Configure each node in the cluster
    node_setup=models.NodeSetup(
        # Mount shared volumes to the host
        mount_volumes=models.MountVolumes(
            azure_file_shares=[
                models.AzureFileShareReference(
                    account_name=storage_account_name,
                    credentials=models.AzureStorageCredentialsInfo(
                        account_key=storage_account_key),
                    azure_file_url='https://{0}/{1}'.format(
                        service.primary_endpoint, azure_file_share_name),
                    relative_mount_path=relative_mount_point)],
        ),
    ),
)
batchai_client.clusters.create(resource_group_name, workspace_name, cluster_name,
                               parameters).result()
```

## <a name="get-cluster-status"></a><span data-ttu-id="55132-138">Get cluster status</span><span class="sxs-lookup"><span data-stu-id="55132-138">Get cluster status</span></span>

<span data-ttu-id="55132-139">Monitor the cluster status using the following command:</span><span class="sxs-lookup"><span data-stu-id="55132-139">Monitor the cluster status using the following command:</span></span>

```Python
cluster = batchai_client.clusters.get(resource_group_name, workspace_name, cluster_name)
print('Cluster state: {0} Target: {1}; Allocated: {2}; Idle: {3}; '
      'Unusable: {4}; Running: {5}; Preparing: {6}; Leaving: {7}'.format(
    cluster.allocation_state,
    cluster.scale_settings.manual.target_node_count,
    cluster.current_node_count,
    cluster.node_state_counts.idle_node_count,
    cluster.node_state_counts.unusable_node_count,
    cluster.node_state_counts.running_node_count,
    cluster.node_state_counts.preparing_node_count,
    cluster.node_state_counts.leaving_node_count))
```

<span data-ttu-id="55132-140">The preceding code prints basic cluster allocation information like in the following example:</span><span class="sxs-lookup"><span data-stu-id="55132-140">The preceding code prints basic cluster allocation information like in the following example:</span></span>

```
Cluster state: AllocationState.steady Target: 1; Allocated: 1; Idle: 0; Unusable: 0; Running: 0; Preparing: 1; Leaving: 0
```

<span data-ttu-id="55132-141">The cluster is ready when the nodes are allocated and finished preparation (see the `nodeStateCounts` attribute).</span><span class="sxs-lookup"><span data-stu-id="55132-141">The cluster is ready when the nodes are allocated and finished preparation (see the `nodeStateCounts` attribute).</span></span> <span data-ttu-id="55132-142">If something went wrong, the `errors` attribute contains the error description.</span><span class="sxs-lookup"><span data-stu-id="55132-142">If something went wrong, the `errors` attribute contains the error description.</span></span>

## <a name="create-experiment-and-training-job"></a><span data-ttu-id="55132-143">Create experiment and training job</span><span class="sxs-lookup"><span data-stu-id="55132-143">Create experiment and training job</span></span>

<span data-ttu-id="55132-144">After the cluster is created, create an experiment (a logical container for a group of related jobs).</span><span class="sxs-lookup"><span data-stu-id="55132-144">After the cluster is created, create an experiment (a logical container for a group of related jobs).</span></span> <span data-ttu-id="55132-145">Then configure and submit a learning job in the experiment:</span><span class="sxs-lookup"><span data-stu-id="55132-145">Then configure and submit a learning job in the experiment:</span></span>

```Python
experiment_name='myexperiment'

batchai_client.experiments.create(resource_group_name, workspace_name, experiment_name)

job_name = 'myjob'

parameters = models.JobCreateParameters(
    # The cluster this job will run on
    cluster=models.ResourceId(id=cluster.id),
    # The number of VMs in the cluster to use
    node_count=1,
    # Write job's standard output and execution log to Azure File Share
    std_out_err_path_prefix='$AZ_BATCHAI_MOUNT_ROOT/{0}'.format(
        relative_mount_point),
    # Configure location of the training script and MNIST dataset
    input_directories=[models.InputDirectory(
        id='SAMPLE',
        path='$AZ_BATCHAI_MOUNT_ROOT/{0}/{1}'.format(
            relative_mount_point, mnist_dataset_directory))],
    # Specify location where generated model will be stored
    output_directories=[models.OutputDirectory(
        id='MODEL',
        path_prefix='$AZ_BATCHAI_MOUNT_ROOT/{0}'.format(relative_mount_point),
        path_suffix="Models")],
    # Container configuration
    container_settings=models.ContainerSettings(
        image_source_registry=models.ImageSourceRegistry(
            image='microsoft/cntk:2.1-gpu-python3.5-cuda8.0-cudnn6.0')),
    # Toolkit specific settings
    cntk_settings=models.CNTKsettings(
        python_script_file_path='$AZ_BATCHAI_INPUT_SAMPLE/ConvNet_MNIST.py',
        command_line_args='$AZ_BATCHAI_INPUT_SAMPLE $AZ_BATCHAI_OUTPUT_MODEL')
)

# Create the job
batchai_client.jobs.create(resource_group_name, workspace_name, experiment_name, job_name, parameters).result()
```

## <a name="monitor-job"></a><span data-ttu-id="55132-146">Monitor job</span><span class="sxs-lookup"><span data-stu-id="55132-146">Monitor job</span></span>

<span data-ttu-id="55132-147">You can inspect the job’s state using the following code:</span><span class="sxs-lookup"><span data-stu-id="55132-147">You can inspect the job’s state using the following code:</span></span>

```Python
job = batchai_client.jobs.get(resource_group_name, workspace_name, experiment_name, job_name)

print('Job state: {0} '.format(job.execution_state))
```

<span data-ttu-id="55132-148">Output is similar to: `Job state: running`.</span><span class="sxs-lookup"><span data-stu-id="55132-148">Output is similar to: `Job state: running`.</span></span>

<span data-ttu-id="55132-149">The `executionState` contains the current execution state of the job:</span><span class="sxs-lookup"><span data-stu-id="55132-149">The `executionState` contains the current execution state of the job:</span></span>
* <span data-ttu-id="55132-150">`queued`: the job is waiting for the cluster nodes to become available</span><span class="sxs-lookup"><span data-stu-id="55132-150">`queued`: the job is waiting for the cluster nodes to become available</span></span>
* <span data-ttu-id="55132-151">`running`: the job is running</span><span class="sxs-lookup"><span data-stu-id="55132-151">`running`: the job is running</span></span>
* <span data-ttu-id="55132-152">`succeeded` (or `failed`): the job is completed and `executionInfo` contains details about the result</span><span class="sxs-lookup"><span data-stu-id="55132-152">`succeeded` (or `failed`): the job is completed and `executionInfo` contains details about the result</span></span>

## <a name="list-stdout-and-stderr-output"></a><span data-ttu-id="55132-153">List stdout and stderr output</span><span class="sxs-lookup"><span data-stu-id="55132-153">List stdout and stderr output</span></span>

<span data-ttu-id="55132-154">Use the following code to list generated stdout, stderr, and log files:</span><span class="sxs-lookup"><span data-stu-id="55132-154">Use the following code to list generated stdout, stderr, and log files:</span></span>

```Python
files = batchai_client.jobs.list_output_files(
    resource_group_name, workspace_name, experiment_name, job_name,
    models.JobsListOutputFilesOptions(outputdirectoryid="stdouterr"))

for file in (f for f in files if f.download_url):
    print('file: {0}, download url: {1}'.format(file.name, file.download_url))
```

## <a name="list-generated-model-files"></a><span data-ttu-id="55132-155">List generated model files</span><span class="sxs-lookup"><span data-stu-id="55132-155">List generated model files</span></span>
<span data-ttu-id="55132-156">Use the following code to list generated model files:</span><span class="sxs-lookup"><span data-stu-id="55132-156">Use the following code to list generated model files:</span></span>
```Python
files = batchai_client.jobs.list_output_files(
    resource_group_name, workspace_name, experiment_name,job_name,
    models.JobsListOutputFilesOptions(outputdirectoryid="MODEL"))

for file in (f for f in files if f.download_url):
    print('file: {0}, download url: {1}'.format(file.name, file.download_url))
```

## <a name="delete-resources"></a><span data-ttu-id="55132-157">Delete resources</span><span class="sxs-lookup"><span data-stu-id="55132-157">Delete resources</span></span>

<span data-ttu-id="55132-158">Use the following code to delete the job:</span><span class="sxs-lookup"><span data-stu-id="55132-158">Use the following code to delete the job:</span></span>
```Python
batchai_client.jobs.delete(resource_group_name, workspace_name, experiment_name, job_name)
```

<span data-ttu-id="55132-159">Use the following code to delete the cluster:</span><span class="sxs-lookup"><span data-stu-id="55132-159">Use the following code to delete the cluster:</span></span>
```Python
batchai_client.clusters.delete(resource_group_name, workspace_name, cluster_name)
```

<span data-ttu-id="55132-160">Use the following code to delete all allocated resources:</span><span class="sxs-lookup"><span data-stu-id="55132-160">Use the following code to delete all allocated resources:</span></span>
```Python
resource_management_client.resource_groups.delete('myresourcegroup')
```
## <a name="next-steps"></a><span data-ttu-id="55132-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="55132-161">Next steps</span></span>

<span data-ttu-id="55132-162">To learn more about using Batch AI with different frameworks, see the [training recipes](https://github.com/Azure/BatchAI).</span><span class="sxs-lookup"><span data-stu-id="55132-162">To learn more about using Batch AI with different frameworks, see the [training recipes](https://github.com/Azure/BatchAI).</span></span>