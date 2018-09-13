---
title: Run containerized tasks in Azure Container Instances with restart policies
description: Learn how to use Azure Container Instances to execute tasks that run to completion, such as in build, test, or image rendering jobs.
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: article
ms.date: 07/26/2018
ms.author: marsma
ms.openlocfilehash: f4d30a9902261c0e785a1af36a7c1c7a8a0fec46
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867307"
---
# <a name="run-containerized-tasks-with-restart-policies"></a><span data-ttu-id="65eae-103">Run containerized tasks with restart policies</span><span class="sxs-lookup"><span data-stu-id="65eae-103">Run containerized tasks with restart policies</span></span>

<span data-ttu-id="65eae-104">The ease and speed of deploying containers in Azure Container Instances provides a compelling platform for executing run-once tasks like build, test, and image rendering in a container instance.</span><span class="sxs-lookup"><span data-stu-id="65eae-104">The ease and speed of deploying containers in Azure Container Instances provides a compelling platform for executing run-once tasks like build, test, and image rendering in a container instance.</span></span>

<span data-ttu-id="65eae-105">With a configurable restart policy, you can specify that your containers are stopped when their processes have completed.</span><span class="sxs-lookup"><span data-stu-id="65eae-105">With a configurable restart policy, you can specify that your containers are stopped when their processes have completed.</span></span> <span data-ttu-id="65eae-106">Because container instances are billed by the second, you're charged only for the compute resources used while the container executing your task is running.</span><span class="sxs-lookup"><span data-stu-id="65eae-106">Because container instances are billed by the second, you're charged only for the compute resources used while the container executing your task is running.</span></span>

<span data-ttu-id="65eae-107">The examples presented in this article use the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="65eae-107">The examples presented in this article use the Azure CLI.</span></span> <span data-ttu-id="65eae-108">You must have Azure CLI version 2.0.21 or greater [installed locally][azure-cli-install], or use the CLI in the [Azure Cloud Shell](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="65eae-108">You must have Azure CLI version 2.0.21 or greater [installed locally][azure-cli-install], or use the CLI in the [Azure Cloud Shell](../cloud-shell/overview.md).</span></span>

## <a name="container-restart-policy"></a><span data-ttu-id="65eae-109">Container restart policy</span><span class="sxs-lookup"><span data-stu-id="65eae-109">Container restart policy</span></span>

<span data-ttu-id="65eae-110">When you create a container in Azure Container Instances, you can specify one of three restart policy settings.</span><span class="sxs-lookup"><span data-stu-id="65eae-110">When you create a container in Azure Container Instances, you can specify one of three restart policy settings.</span></span>

| <span data-ttu-id="65eae-111">Restart policy</span><span class="sxs-lookup"><span data-stu-id="65eae-111">Restart policy</span></span>   | <span data-ttu-id="65eae-112">Description</span><span class="sxs-lookup"><span data-stu-id="65eae-112">Description</span></span> |
| ---------------- | :---------- |
| `Always` | <span data-ttu-id="65eae-113">Containers in the container group are always restarted.</span><span class="sxs-lookup"><span data-stu-id="65eae-113">Containers in the container group are always restarted.</span></span> <span data-ttu-id="65eae-114">This is the **default** setting applied when no restart policy is specified at container creation.</span><span class="sxs-lookup"><span data-stu-id="65eae-114">This is the **default** setting applied when no restart policy is specified at container creation.</span></span> |
| `Never` | <span data-ttu-id="65eae-115">Containers in the container group are never restarted.</span><span class="sxs-lookup"><span data-stu-id="65eae-115">Containers in the container group are never restarted.</span></span> <span data-ttu-id="65eae-116">The containers run at most once.</span><span class="sxs-lookup"><span data-stu-id="65eae-116">The containers run at most once.</span></span> |
| `OnFailure` | <span data-ttu-id="65eae-117">Containers in the container group are restarted only when the process executed in the container fails (when it terminates with a nonzero exit code).</span><span class="sxs-lookup"><span data-stu-id="65eae-117">Containers in the container group are restarted only when the process executed in the container fails (when it terminates with a nonzero exit code).</span></span> <span data-ttu-id="65eae-118">The containers are run at least once.</span><span class="sxs-lookup"><span data-stu-id="65eae-118">The containers are run at least once.</span></span> |

## <a name="specify-a-restart-policy"></a><span data-ttu-id="65eae-119">Specify a restart policy</span><span class="sxs-lookup"><span data-stu-id="65eae-119">Specify a restart policy</span></span>

<span data-ttu-id="65eae-120">How you specify a restart policy depends on how you create your container instances, such as with the Azure CLI, Azure PowerShell cmdlets, or in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="65eae-120">How you specify a restart policy depends on how you create your container instances, such as with the Azure CLI, Azure PowerShell cmdlets, or in the Azure portal.</span></span> <span data-ttu-id="65eae-121">In the Azure CLI, specify the `--restart-policy` parameter when you call [az container create][az-container-create].</span><span class="sxs-lookup"><span data-stu-id="65eae-121">In the Azure CLI, specify the `--restart-policy` parameter when you call [az container create][az-container-create].</span></span>

```azurecli-interactive
az container create \
    --resource-group myResourceGroup \
    --name mycontainer \
    --image mycontainerimage \
    --restart-policy OnFailure
```

## <a name="run-to-completion-example"></a><span data-ttu-id="65eae-122">Run to completion example</span><span class="sxs-lookup"><span data-stu-id="65eae-122">Run to completion example</span></span>

<span data-ttu-id="65eae-123">To see the restart policy in action, create a container instance from the [microsoft/aci-wordcount][aci-wordcount-image] image, and specify the `OnFailure` restart policy.</span><span class="sxs-lookup"><span data-stu-id="65eae-123">To see the restart policy in action, create a container instance from the [microsoft/aci-wordcount][aci-wordcount-image] image, and specify the `OnFailure` restart policy.</span></span> <span data-ttu-id="65eae-124">This example container runs a Python script that, by default, analyzes the text of Shakespeare's [Hamlet](http://shakespeare.mit.edu/hamlet/full.html), writes the 10 most common words to STDOUT, and then exits.</span><span class="sxs-lookup"><span data-stu-id="65eae-124">This example container runs a Python script that, by default, analyzes the text of Shakespeare's [Hamlet](http://shakespeare.mit.edu/hamlet/full.html), writes the 10 most common words to STDOUT, and then exits.</span></span>

<span data-ttu-id="65eae-125">Run the example container with the following [az container create][az-container-create] command:</span><span class="sxs-lookup"><span data-stu-id="65eae-125">Run the example container with the following [az container create][az-container-create] command:</span></span>

```azurecli-interactive
az container create \
    --resource-group myResourceGroup \
    --name mycontainer \
    --image microsoft/aci-wordcount:latest \
    --restart-policy OnFailure
```

<span data-ttu-id="65eae-126">Azure Container Instances starts the container, and then stops it when its application (or script, in this case) exits.</span><span class="sxs-lookup"><span data-stu-id="65eae-126">Azure Container Instances starts the container, and then stops it when its application (or script, in this case) exits.</span></span> <span data-ttu-id="65eae-127">When Azure Container Instances stops a container whose restart policy is `Never` or `OnFailure`, the container's status is set to **Terminated**.</span><span class="sxs-lookup"><span data-stu-id="65eae-127">When Azure Container Instances stops a container whose restart policy is `Never` or `OnFailure`, the container's status is set to **Terminated**.</span></span> <span data-ttu-id="65eae-128">You can check a container's status with the [az container show][az-container-show] command:</span><span class="sxs-lookup"><span data-stu-id="65eae-128">You can check a container's status with the [az container show][az-container-show] command:</span></span>

```azurecli-interactive
az container show --resource-group myResourceGroup --name mycontainer --query containers[0].instanceView.currentState.state
```

<span data-ttu-id="65eae-129">Example output:</span><span class="sxs-lookup"><span data-stu-id="65eae-129">Example output:</span></span>

```bash
"Terminated"
```

<span data-ttu-id="65eae-130">Once the example container's status shows *Terminated*, you can see its task output by viewing the container logs.</span><span class="sxs-lookup"><span data-stu-id="65eae-130">Once the example container's status shows *Terminated*, you can see its task output by viewing the container logs.</span></span> <span data-ttu-id="65eae-131">Run the [az container logs][az-container-logs] command to view the script's output:</span><span class="sxs-lookup"><span data-stu-id="65eae-131">Run the [az container logs][az-container-logs] command to view the script's output:</span></span>

```azurecli-interactive
az container logs --resource-group myResourceGroup --name mycontainer
```

<span data-ttu-id="65eae-132">Output:</span><span class="sxs-lookup"><span data-stu-id="65eae-132">Output:</span></span>

```bash
[('the', 990),
 ('and', 702),
 ('of', 628),
 ('to', 610),
 ('I', 544),
 ('you', 495),
 ('a', 453),
 ('my', 441),
 ('in', 399),
 ('HAMLET', 386)]
```

<span data-ttu-id="65eae-133">This example shows the output that the script sent to STDOUT.</span><span class="sxs-lookup"><span data-stu-id="65eae-133">This example shows the output that the script sent to STDOUT.</span></span> <span data-ttu-id="65eae-134">Your containerized tasks, however, might instead write their output to persistent storage for later retrieval.</span><span class="sxs-lookup"><span data-stu-id="65eae-134">Your containerized tasks, however, might instead write their output to persistent storage for later retrieval.</span></span> <span data-ttu-id="65eae-135">For example, to an [Azure file share](container-instances-mounting-azure-files-volume.md).</span><span class="sxs-lookup"><span data-stu-id="65eae-135">For example, to an [Azure file share](container-instances-mounting-azure-files-volume.md).</span></span>

## <a name="configure-containers-at-runtime"></a><span data-ttu-id="65eae-136">Configure containers at runtime</span><span class="sxs-lookup"><span data-stu-id="65eae-136">Configure containers at runtime</span></span>

<span data-ttu-id="65eae-137">When you create a container instance, you can set its **environment variables**, as well as specify a custom **command line** to execute when the container is started.</span><span class="sxs-lookup"><span data-stu-id="65eae-137">When you create a container instance, you can set its **environment variables**, as well as specify a custom **command line** to execute when the container is started.</span></span> <span data-ttu-id="65eae-138">You can use these settings in your batch jobs to prepare each container with task-specific configuration.</span><span class="sxs-lookup"><span data-stu-id="65eae-138">You can use these settings in your batch jobs to prepare each container with task-specific configuration.</span></span>

## <a name="environment-variables"></a><span data-ttu-id="65eae-139">Environment variables</span><span class="sxs-lookup"><span data-stu-id="65eae-139">Environment variables</span></span>

<span data-ttu-id="65eae-140">Set environment variables in your container to provide dynamic configuration of the application or script run by the container.</span><span class="sxs-lookup"><span data-stu-id="65eae-140">Set environment variables in your container to provide dynamic configuration of the application or script run by the container.</span></span> <span data-ttu-id="65eae-141">This is similar to the `--env` command-line argument to `docker run`.</span><span class="sxs-lookup"><span data-stu-id="65eae-141">This is similar to the `--env` command-line argument to `docker run`.</span></span>

<span data-ttu-id="65eae-142">For example, you can modify the behavior of the script in the example container by specifying the following environment variables when you create the container instance:</span><span class="sxs-lookup"><span data-stu-id="65eae-142">For example, you can modify the behavior of the script in the example container by specifying the following environment variables when you create the container instance:</span></span>

<span data-ttu-id="65eae-143">*NumWords*: The number of words sent to STDOUT.</span><span class="sxs-lookup"><span data-stu-id="65eae-143">*NumWords*: The number of words sent to STDOUT.</span></span>

<span data-ttu-id="65eae-144">*MinLength*: The minimum number of characters in a word for it to be counted.</span><span class="sxs-lookup"><span data-stu-id="65eae-144">*MinLength*: The minimum number of characters in a word for it to be counted.</span></span> <span data-ttu-id="65eae-145">A higher number ignores common words like "of" and "the."</span><span class="sxs-lookup"><span data-stu-id="65eae-145">A higher number ignores common words like "of" and "the."</span></span>

```azurecli-interactive
az container create \
    --resource-group myResourceGroup \
    --name mycontainer2 \
    --image microsoft/aci-wordcount:latest \
    --restart-policy OnFailure \
    --environment-variables NumWords=5 MinLength=8
```

<span data-ttu-id="65eae-146">By specifying `NumWords=5` and `MinLength=8` for the container's environment variables, the container logs should display different output.</span><span class="sxs-lookup"><span data-stu-id="65eae-146">By specifying `NumWords=5` and `MinLength=8` for the container's environment variables, the container logs should display different output.</span></span> <span data-ttu-id="65eae-147">Once the container status shows as *Terminated* (use `az container show` to check its status), display its logs to see the new output:</span><span class="sxs-lookup"><span data-stu-id="65eae-147">Once the container status shows as *Terminated* (use `az container show` to check its status), display its logs to see the new output:</span></span>

```azurecli-interactive
az container logs --resource-group myResourceGroup --name mycontainer2
```

<span data-ttu-id="65eae-148">Output:</span><span class="sxs-lookup"><span data-stu-id="65eae-148">Output:</span></span>

```bash
[('CLAUDIUS', 120),
 ('POLONIUS', 113),
 ('GERTRUDE', 82),
 ('ROSENCRANTZ', 69),
 ('GUILDENSTERN', 54)]
```

## <a name="command-line-override"></a><span data-ttu-id="65eae-149">Command line override</span><span class="sxs-lookup"><span data-stu-id="65eae-149">Command line override</span></span>

<span data-ttu-id="65eae-150">Specify a command line when you create a container instance to override the command line baked into the container image.</span><span class="sxs-lookup"><span data-stu-id="65eae-150">Specify a command line when you create a container instance to override the command line baked into the container image.</span></span> <span data-ttu-id="65eae-151">This is similar to the `--entrypoint` command-line argument to `docker run`.</span><span class="sxs-lookup"><span data-stu-id="65eae-151">This is similar to the `--entrypoint` command-line argument to `docker run`.</span></span>

<span data-ttu-id="65eae-152">For instance, you can have the example container analyze text other than *Hamlet* by specifying a different command line.</span><span class="sxs-lookup"><span data-stu-id="65eae-152">For instance, you can have the example container analyze text other than *Hamlet* by specifying a different command line.</span></span> <span data-ttu-id="65eae-153">The Python script executed by the container, *wordcount.py*, accepts a URL as an argument, and will process that page's content instead of the default.</span><span class="sxs-lookup"><span data-stu-id="65eae-153">The Python script executed by the container, *wordcount.py*, accepts a URL as an argument, and will process that page's content instead of the default.</span></span>

<span data-ttu-id="65eae-154">For example, to determine the top 3 five-letter words in *Romeo and Juliet*:</span><span class="sxs-lookup"><span data-stu-id="65eae-154">For example, to determine the top 3 five-letter words in *Romeo and Juliet*:</span></span>

```azurecli-interactive
az container create \
    --resource-group myResourceGroup \
    --name mycontainer3 \
    --image microsoft/aci-wordcount:latest \
    --restart-policy OnFailure \
    --environment-variables NumWords=3 MinLength=5 \
    --command-line "python wordcount.py http://shakespeare.mit.edu/romeo_juliet/full.html"
```

<span data-ttu-id="65eae-155">Again, once the container is *Terminated*, view the output by showing the container's logs:</span><span class="sxs-lookup"><span data-stu-id="65eae-155">Again, once the container is *Terminated*, view the output by showing the container's logs:</span></span>

```azurecli-interactive
az container logs --resource-group myResourceGroup --name mycontainer3
```

<span data-ttu-id="65eae-156">Output:</span><span class="sxs-lookup"><span data-stu-id="65eae-156">Output:</span></span>

```bash
[('ROMEO', 177), ('JULIET', 134), ('CAPULET', 119)]
```

## <a name="next-steps"></a><span data-ttu-id="65eae-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="65eae-157">Next steps</span></span>

### <a name="persist-task-output"></a><span data-ttu-id="65eae-158">Persist task output</span><span class="sxs-lookup"><span data-stu-id="65eae-158">Persist task output</span></span>

<span data-ttu-id="65eae-159">For details on how to persist the output of your containers that run to completion, see [Mounting an Azure file share with Azure Container Instances](container-instances-mounting-azure-files-volume.md).</span><span class="sxs-lookup"><span data-stu-id="65eae-159">For details on how to persist the output of your containers that run to completion, see [Mounting an Azure file share with Azure Container Instances](container-instances-mounting-azure-files-volume.md).</span></span>

<!-- LINKS - External -->
[aci-wordcount-image]: https://hub.docker.com/r/microsoft/aci-wordcount/

<!-- LINKS - Internal -->
[az-container-create]: /cli/azure/container?view=azure-cli-latest#az-container-create
[az-container-logs]: /cli/azure/container?view=azure-cli-latest#az-container-logs
[az-container-show]: /cli/azure/container?view=azure-cli-latest#az-container-show
[azure-cli-install]: /cli/azure/install-azure-cli
