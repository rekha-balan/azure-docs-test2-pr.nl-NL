---
title: Migrate to updated Azure Batch AI API | Microsoft Docs
description: How to update Azure Batch AI code and scripts to use workspace and experiment resources
services: batch-ai
documentationcenter: na
author: dlepow
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.custom: ''
ms.service: batch-ai
ms.workload: ''
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/08/2018
ms.author: danlep
ms.openlocfilehash: c5e4c1569464d2e204edf13fe7534d80780524e8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869683"
---
# <a name="migrate-to-the-updated-batch-ai-api"></a><span data-ttu-id="cb39d-103">Migrate to the updated Batch AI API</span><span class="sxs-lookup"><span data-stu-id="cb39d-103">Migrate to the updated Batch AI API</span></span>

<span data-ttu-id="cb39d-104">In the Batch AI REST API version 2018-05-01 and related Batch AI SDKs and tools, significant changes and new features have been introduced.</span><span class="sxs-lookup"><span data-stu-id="cb39d-104">In the Batch AI REST API version 2018-05-01 and related Batch AI SDKs and tools, significant changes and new features have been introduced.</span></span>

<span data-ttu-id="cb39d-105">If you've used a previous version of the Batch AI API, this article explains how to modify your code and scripts to work with the new API.</span><span class="sxs-lookup"><span data-stu-id="cb39d-105">If you've used a previous version of the Batch AI API, this article explains how to modify your code and scripts to work with the new API.</span></span> 

## <a name="whats-changing"></a><span data-ttu-id="cb39d-106">What's changing?</span><span class="sxs-lookup"><span data-stu-id="cb39d-106">What's changing?</span></span>

<span data-ttu-id="cb39d-107">In response to customer feedback, we’re removing limits on the number of jobs and making it easier to manage Batch AI resources.</span><span class="sxs-lookup"><span data-stu-id="cb39d-107">In response to customer feedback, we’re removing limits on the number of jobs and making it easier to manage Batch AI resources.</span></span> <span data-ttu-id="cb39d-108">The new API introduces two new resources, *workspace* and *experiment*.</span><span class="sxs-lookup"><span data-stu-id="cb39d-108">The new API introduces two new resources, *workspace* and *experiment*.</span></span> <span data-ttu-id="cb39d-109">Collect related training jobs under an experiment, and organize all related Batch AI resources (clusters, file servers, experiments, jobs) under a workspace.</span><span class="sxs-lookup"><span data-stu-id="cb39d-109">Collect related training jobs under an experiment, and organize all related Batch AI resources (clusters, file servers, experiments, jobs) under a workspace.</span></span>  

* <span data-ttu-id="cb39d-110">**Workspace** - A top-level collection of all types of Batch AI resources.</span><span class="sxs-lookup"><span data-stu-id="cb39d-110">**Workspace** - A top-level collection of all types of Batch AI resources.</span></span> <span data-ttu-id="cb39d-111">Clusters and file servers are contained in a workspace.</span><span class="sxs-lookup"><span data-stu-id="cb39d-111">Clusters and file servers are contained in a workspace.</span></span> <span data-ttu-id="cb39d-112">Workspaces usually separate work belonging to different groups or projects.</span><span class="sxs-lookup"><span data-stu-id="cb39d-112">Workspaces usually separate work belonging to different groups or projects.</span></span> <span data-ttu-id="cb39d-113">For example, you might have a dev and a test workspace.</span><span class="sxs-lookup"><span data-stu-id="cb39d-113">For example, you might have a dev and a test workspace.</span></span> <span data-ttu-id="cb39d-114">You probably need only a limited number of workspaces per subscription.</span><span class="sxs-lookup"><span data-stu-id="cb39d-114">You probably need only a limited number of workspaces per subscription.</span></span> 

* <span data-ttu-id="cb39d-115">**Experiment** - A collection of related jobs that can be queried and managed together.</span><span class="sxs-lookup"><span data-stu-id="cb39d-115">**Experiment** - A collection of related jobs that can be queried and managed together.</span></span> <span data-ttu-id="cb39d-116">For example, use an experiment to group all jobs that are performed as part of a hyper-parameter tuning sweep.</span><span class="sxs-lookup"><span data-stu-id="cb39d-116">For example, use an experiment to group all jobs that are performed as part of a hyper-parameter tuning sweep.</span></span> 

<span data-ttu-id="cb39d-117">The following image shows an example resource hierarchy.</span><span class="sxs-lookup"><span data-stu-id="cb39d-117">The following image shows an example resource hierarchy.</span></span> 

![](./media/migrate-to-new-api/batch-ai-resource-hierarchy.png)

## <a name="monitor-and-manage-existing-resources"></a><span data-ttu-id="cb39d-118">Monitor and manage existing resources</span><span class="sxs-lookup"><span data-stu-id="cb39d-118">Monitor and manage existing resources</span></span>
<span data-ttu-id="cb39d-119">In each resource group where you already created Batch AI clusters, jobs, or file servers, the Batch AI service will create a workspace named `migrated-<region>` (for example, `migrated-eastus`) and an experiment named `migrated`.</span><span class="sxs-lookup"><span data-stu-id="cb39d-119">In each resource group where you already created Batch AI clusters, jobs, or file servers, the Batch AI service will create a workspace named `migrated-<region>` (for example, `migrated-eastus`) and an experiment named `migrated`.</span></span> <span data-ttu-id="cb39d-120">To access the previously created jobs, clusters, or file servers, you need to use the migrated workspace and experiment.</span><span class="sxs-lookup"><span data-stu-id="cb39d-120">To access the previously created jobs, clusters, or file servers, you need to use the migrated workspace and experiment.</span></span> 

### <a name="portal"></a><span data-ttu-id="cb39d-121">Portal</span><span class="sxs-lookup"><span data-stu-id="cb39d-121">Portal</span></span> 
<span data-ttu-id="cb39d-122">To access previously created jobs, clusters, or file servers by using the portal, first select the `migrated-<region>` workspace.</span><span class="sxs-lookup"><span data-stu-id="cb39d-122">To access previously created jobs, clusters, or file servers by using the portal, first select the `migrated-<region>` workspace.</span></span> <span data-ttu-id="cb39d-123">After you select the workspace, perform operations such as resizing or deleting a cluster, and viewing job status and outputs.</span><span class="sxs-lookup"><span data-stu-id="cb39d-123">After you select the workspace, perform operations such as resizing or deleting a cluster, and viewing job status and outputs.</span></span> 

### <a name="sdks"></a><span data-ttu-id="cb39d-124">SDKs</span><span class="sxs-lookup"><span data-stu-id="cb39d-124">SDKs</span></span> 
<span data-ttu-id="cb39d-125">To access jobs, clusters, or file servers previously created via the Batch AI SDKs, supply the workspace name and experiment name parameters.</span><span class="sxs-lookup"><span data-stu-id="cb39d-125">To access jobs, clusters, or file servers previously created via the Batch AI SDKs, supply the workspace name and experiment name parameters.</span></span> 

<span data-ttu-id="cb39d-126">If you use the Python SDK, relevant changes are shown in the following examples.</span><span class="sxs-lookup"><span data-stu-id="cb39d-126">If you use the Python SDK, relevant changes are shown in the following examples.</span></span> <span data-ttu-id="cb39d-127">Changes are similar in the other Batch AI SDKs.</span><span class="sxs-lookup"><span data-stu-id="cb39d-127">Changes are similar in the other Batch AI SDKs.</span></span> 


#### <a name="get-old-cluster"></a><span data-ttu-id="cb39d-128">Get old cluster</span><span class="sxs-lookup"><span data-stu-id="cb39d-128">Get old cluster</span></span> 

```python
cluster = client.clusters.get(resource_group_name, 'migrated-<region>', cluster_name)
```

#### <a name="delete-old-cluster"></a><span data-ttu-id="cb39d-129">Delete old cluster</span><span class="sxs-lookup"><span data-stu-id="cb39d-129">Delete old cluster</span></span> 

```python
client.clusters.delete(resource_group_name, 'migrated-<region>', cluster_name)
```

#### <a name="get-old-file-server"></a><span data-ttu-id="cb39d-130">Get old file server</span><span class="sxs-lookup"><span data-stu-id="cb39d-130">Get old file server</span></span> 

```python
cluster = client.fileservers.get(resource_group_name, 'migrated-<region>', fileserver_name)
```

#### <a name="delete-old-file-server"></a><span data-ttu-id="cb39d-131">Delete old file server</span><span class="sxs-lookup"><span data-stu-id="cb39d-131">Delete old file server</span></span>  

```python
client.fileservers.delete(resource_group_name, 'migrated-<region>', fileserver_name)
``` 


#### <a name="get-old-job"></a><span data-ttu-id="cb39d-132">Get old job</span><span class="sxs-lookup"><span data-stu-id="cb39d-132">Get old job</span></span> 

```python
cluster = client.jobs.get(resource_group_name, 'migrated-<region>', 'migrated', job_name)
```

#### <a name="delete-old-job"></a><span data-ttu-id="cb39d-133">Delete old job</span><span class="sxs-lookup"><span data-stu-id="cb39d-133">Delete old job</span></span>

```python
client.jobs.delete(resource_group_name, 'migrated-<region>', 'migrated', job_name)
```
 
### <a name="azure-cli"></a><span data-ttu-id="cb39d-134">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="cb39d-134">Azure CLI</span></span> 
 
<span data-ttu-id="cb39d-135">When using the Azure CLI to access previously created jobs, clusters, or file servers, use the `-w` and `-e` parameters to supply workspace and experiment names.</span><span class="sxs-lookup"><span data-stu-id="cb39d-135">When using the Azure CLI to access previously created jobs, clusters, or file servers, use the `-w` and `-e` parameters to supply workspace and experiment names.</span></span> 


#### <a name="get-old-cluster"></a><span data-ttu-id="cb39d-136">Get old cluster</span><span class="sxs-lookup"><span data-stu-id="cb39d-136">Get old cluster</span></span>

```azurecli
az batchai cluster show -g resource-group-name -w migrated-<region> -n cluster-name
```


#### <a name="delete-old-cluster"></a><span data-ttu-id="cb39d-137">Delete old cluster</span><span class="sxs-lookup"><span data-stu-id="cb39d-137">Delete old cluster</span></span> 

```azurecli
az batchai cluster delete -g resource-group-name -w migrated-<region> -n cluster-name
```

#### <a name="get-old-file-server"></a><span data-ttu-id="cb39d-138">Get old file server</span><span class="sxs-lookup"><span data-stu-id="cb39d-138">Get old file server</span></span>

```azurecli
az batchai file-server show -g resource-group-name -w migrated-<region> -n fileserver-name
```


#### <a name="delete-old-file-server"></a><span data-ttu-id="cb39d-139">Delete old file server</span><span class="sxs-lookup"><span data-stu-id="cb39d-139">Delete old file server</span></span> 

```azurecli
az batchai file-server delete -g resource-group-name -w migrated-<region> -n fileserver-name
``` 


#### <a name="get-old-job"></a><span data-ttu-id="cb39d-140">Get old job</span><span class="sxs-lookup"><span data-stu-id="cb39d-140">Get old job</span></span>

```azurecli
az batchai job show -g resource-group-name -w migrated-<region> -e migrated -n job-name
```


#### <a name="delete-old-job"></a><span data-ttu-id="cb39d-141">Delete old job</span><span class="sxs-lookup"><span data-stu-id="cb39d-141">Delete old job</span></span> 

```azurecli
az batchai job delete -g resource-group-name -w migrated-<region> -e migrated -n job-name
``` 

## <a name="create-batch-ai-resources"></a><span data-ttu-id="cb39d-142">Create Batch AI resources</span><span class="sxs-lookup"><span data-stu-id="cb39d-142">Create Batch AI resources</span></span> 
 
<span data-ttu-id="cb39d-143">If you're using one of the existing Batch AI SDKs, you can continue to use it to create Batch AI resources (jobs, clusters, or file servers) without making code changes.</span><span class="sxs-lookup"><span data-stu-id="cb39d-143">If you're using one of the existing Batch AI SDKs, you can continue to use it to create Batch AI resources (jobs, clusters, or file servers) without making code changes.</span></span> <span data-ttu-id="cb39d-144">However, after you upgrade to the new SDK, you need to make the following changes.</span><span class="sxs-lookup"><span data-stu-id="cb39d-144">However, after you upgrade to the new SDK, you need to make the following changes.</span></span>
 
### <a name="create-workspace"></a><span data-ttu-id="cb39d-145">Create workspace</span><span class="sxs-lookup"><span data-stu-id="cb39d-145">Create workspace</span></span> 
<span data-ttu-id="cb39d-146">Depending on your scenario, you can create a workspace manually one-time via the portal or CLI.</span><span class="sxs-lookup"><span data-stu-id="cb39d-146">Depending on your scenario, you can create a workspace manually one-time via the portal or CLI.</span></span> <span data-ttu-id="cb39d-147">If you're using the CLI, create a workspace using the following command:</span><span class="sxs-lookup"><span data-stu-id="cb39d-147">If you're using the CLI, create a workspace using the following command:</span></span> 

```azurecli
az batchai workspace create -g resource-group-name -n workspace-name
```

### <a name="create-experiment"></a><span data-ttu-id="cb39d-148">Create experiment</span><span class="sxs-lookup"><span data-stu-id="cb39d-148">Create experiment</span></span> 


<span data-ttu-id="cb39d-149">Depending on your scenario, you can create  an experiment manually one-time via the portal or CLI.</span><span class="sxs-lookup"><span data-stu-id="cb39d-149">Depending on your scenario, you can create  an experiment manually one-time via the portal or CLI.</span></span> <span data-ttu-id="cb39d-150">If you're using the CLI, create an experiment using the following command:</span><span class="sxs-lookup"><span data-stu-id="cb39d-150">If you're using the CLI, create an experiment using the following command:</span></span> 

```azurecli
az batchai experiment create -g resource-group-name -w workspace-name -n experiment-name

```

### <a name="create-clusters-file-servers-and-jobs"></a><span data-ttu-id="cb39d-151">Create clusters, file servers, and jobs</span><span class="sxs-lookup"><span data-stu-id="cb39d-151">Create clusters, file servers, and jobs</span></span>
 
<span data-ttu-id="cb39d-152">If you use the portal to create jobs, clusters, or file servers, the portal will guide you during the creation experience to supply the workspace name and experiment name parameters.</span><span class="sxs-lookup"><span data-stu-id="cb39d-152">If you use the portal to create jobs, clusters, or file servers, the portal will guide you during the creation experience to supply the workspace name and experiment name parameters.</span></span>

<span data-ttu-id="cb39d-153">To create jobs, clusters, or file servers via the updated SDK, supply the workspace name parameter.</span><span class="sxs-lookup"><span data-stu-id="cb39d-153">To create jobs, clusters, or file servers via the updated SDK, supply the workspace name parameter.</span></span> <span data-ttu-id="cb39d-154">If you use the Python SDK, relevant changes are shown in the following examples.</span><span class="sxs-lookup"><span data-stu-id="cb39d-154">If you use the Python SDK, relevant changes are shown in the following examples.</span></span> <span data-ttu-id="cb39d-155">Replace *workspace_name* and *experiment_name* with the workspace and experiment that you created previously.</span><span class="sxs-lookup"><span data-stu-id="cb39d-155">Replace *workspace_name* and *experiment_name* with the workspace and experiment that you created previously.</span></span> <span data-ttu-id="cb39d-156">Changes are similar in the other Batch AI SDKs.</span><span class="sxs-lookup"><span data-stu-id="cb39d-156">Changes are similar in the other Batch AI SDKs.</span></span> 


#### <a name="create-cluster"></a><span data-ttu-id="cb39d-157">Create cluster</span><span class="sxs-lookup"><span data-stu-id="cb39d-157">Create cluster</span></span> 

```python
_ = client.clusters.create(resource_group_name, workspace_name, cluster_name, cluster_create_parameters).result()
```

#### <a name="create-file-server"></a><span data-ttu-id="cb39d-158">Create file server</span><span class="sxs-lookup"><span data-stu-id="cb39d-158">Create file server</span></span> 

```python
_ = client.fileservers.create(resource_group_name, workspace_name, fileserver_name, fileserver_create_parameters).result()
```

#### <a name="create-job"></a><span data-ttu-id="cb39d-159">Create job</span><span class="sxs-lookup"><span data-stu-id="cb39d-159">Create job</span></span> 

```python
_ = client.jobs.create(resource_group_name, workspace_name, experiment_name, job_name job_create_parameters).result()
```


## <a name="next-steps"></a><span data-ttu-id="cb39d-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="cb39d-160">Next steps</span></span>

* <span data-ttu-id="cb39d-161">See the Batch AI API reference: [CLI](/cli/azure/batchai), [.NET](/dotnet/api/overview/azure/batchai), [Java](/java/api/overview/azure/batchai), [Node.js](/javascript/api/overview/azure/batchai), [Python](/python/api/overview/azure/batchai), and [REST](/rest/api/batchai)</span><span class="sxs-lookup"><span data-stu-id="cb39d-161">See the Batch AI API reference: [CLI](/cli/azure/batchai), [.NET](/dotnet/api/overview/azure/batchai), [Java](/java/api/overview/azure/batchai), [Node.js](/javascript/api/overview/azure/batchai), [Python](/python/api/overview/azure/batchai), and [REST](/rest/api/batchai)</span></span>