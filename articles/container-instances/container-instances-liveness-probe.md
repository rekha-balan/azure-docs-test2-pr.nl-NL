---
title: Configure liveness probes in Azure Container Instances
description: Learn how to configure liveness probes to restart unhealthy containers in Azure Container Instances
services: container-instances
author: jluk
manager: jeconnoc
ms.service: container-instances
ms.topic: article
ms.date: 06/08/2018
ms.author: juluk
ms.openlocfilehash: 1582f0d7ec688bc72cc9d1aa6ae0ddb0a6ad3a17
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865494"
---
# <a name="configure-liveness-probes"></a><span data-ttu-id="4c5bb-103">Configure liveness probes</span><span class="sxs-lookup"><span data-stu-id="4c5bb-103">Configure liveness probes</span></span>

<span data-ttu-id="4c5bb-104">Containerized applications may run for extended periods of time resulting in broken states that may need to be repaired by restarting the container.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-104">Containerized applications may run for extended periods of time resulting in broken states that may need to be repaired by restarting the container.</span></span> <span data-ttu-id="4c5bb-105">Azure Container Instances supports liveness probes to include configurations so that your container can restart if critical functionality is not working.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-105">Azure Container Instances supports liveness probes to include configurations so that your container can restart if critical functionality is not working.</span></span>

<span data-ttu-id="4c5bb-106">This article explains how to deploy a container group that includes a liveness probe, demonstrating the automatic restart of a simulated unhealthy container.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-106">This article explains how to deploy a container group that includes a liveness probe, demonstrating the automatic restart of a simulated unhealthy container.</span></span>

## <a name="yaml-deployment"></a><span data-ttu-id="4c5bb-107">YAML deployment</span><span class="sxs-lookup"><span data-stu-id="4c5bb-107">YAML deployment</span></span>

<span data-ttu-id="4c5bb-108">Create a `liveness-probe.yaml` file with the following snippet.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-108">Create a `liveness-probe.yaml` file with the following snippet.</span></span> <span data-ttu-id="4c5bb-109">This file defines a container group that consists of an NGNIX container that eventually becomes unhealthy.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-109">This file defines a container group that consists of an NGNIX container that eventually becomes unhealthy.</span></span>

```yaml
apiVersion: 2018-06-01
location: eastus
name: livenesstest
properties:
  containers:
  - name: mycontainer
    properties:
      image: nginx
      command:
        - "/bin/sh"
        - "-c"
        - "touch /tmp/healthy; sleep 30; rm -rf /tmp/healthy; sleep 600"
      ports: []
      resources:
        requests:
          cpu: 1.0
          memoryInGB: 1.5
      livenessProbe:
        exec:
            command:
                - "cat"
                - "/tmp/healthy"
        periodSeconds: 5
  osType: Linux
  restartPolicy: Always
tags: null
type: Microsoft.ContainerInstance/containerGroups
```

<span data-ttu-id="4c5bb-110">Run the following command to deploy this container group with the above YAML configuration:</span><span class="sxs-lookup"><span data-stu-id="4c5bb-110">Run the following command to deploy this container group with the above YAML configuration:</span></span>

```azurecli-interactive
az container create --resource-group myResourceGroup --name livenesstest -f liveness-probe.yaml
```

### <a name="start-command"></a><span data-ttu-id="4c5bb-111">Start command</span><span class="sxs-lookup"><span data-stu-id="4c5bb-111">Start command</span></span>

<span data-ttu-id="4c5bb-112">The deployment defines a starting command to be run when the container first starts running, defined by the `command` property which accepts an array of strings.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-112">The deployment defines a starting command to be run when the container first starts running, defined by the `command` property which accepts an array of strings.</span></span> <span data-ttu-id="4c5bb-113">In this example, it will start a bash session and create a file called `healthy` within the `/tmp` directory by passing this command:</span><span class="sxs-lookup"><span data-stu-id="4c5bb-113">In this example, it will start a bash session and create a file called `healthy` within the `/tmp` directory by passing this command:</span></span>

```bash
/bin/sh -c "touch /tmp/healthy; sleep 30; rm -rf /tmp/healthy; sleep 600"
```

 <span data-ttu-id="4c5bb-114">It will then sleep for 30 seconds before deleting the file, then enters a 10 minute sleep.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-114">It will then sleep for 30 seconds before deleting the file, then enters a 10 minute sleep.</span></span>

### <a name="liveness-command"></a><span data-ttu-id="4c5bb-115">Liveness command</span><span class="sxs-lookup"><span data-stu-id="4c5bb-115">Liveness command</span></span>

<span data-ttu-id="4c5bb-116">This deployment defines a `livenessProbe` which supports an `exec` liveness command that acts as the liveness check.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-116">This deployment defines a `livenessProbe` which supports an `exec` liveness command that acts as the liveness check.</span></span> <span data-ttu-id="4c5bb-117">If this command exits with a non-zero value, the container will be killed and restarted, signaling the `healthy` file could not be found.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-117">If this command exits with a non-zero value, the container will be killed and restarted, signaling the `healthy` file could not be found.</span></span> <span data-ttu-id="4c5bb-118">If this command exits successfully with exit code 0, no action will be taken.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-118">If this command exits successfully with exit code 0, no action will be taken.</span></span>

<span data-ttu-id="4c5bb-119">The `periodSeconds` property designates the liveness command should execute every 5 seconds.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-119">The `periodSeconds` property designates the liveness command should execute every 5 seconds.</span></span>

## <a name="verify-liveness-output"></a><span data-ttu-id="4c5bb-120">Verify liveness output</span><span class="sxs-lookup"><span data-stu-id="4c5bb-120">Verify liveness output</span></span>

<span data-ttu-id="4c5bb-121">Within the first 30 seconds, the `healthy` file created by the start command exists.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-121">Within the first 30 seconds, the `healthy` file created by the start command exists.</span></span> <span data-ttu-id="4c5bb-122">When the liveness command checks for the `healthy` file's existence, the status code returns a zero, signaling success, so no restarting occurs.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-122">When the liveness command checks for the `healthy` file's existence, the status code returns a zero, signaling success, so no restarting occurs.</span></span>

<span data-ttu-id="4c5bb-123">After 30 seconds, the `cat /tmp/healthy` will begin to fail, causing unhealthy and killing events to occur.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-123">After 30 seconds, the `cat /tmp/healthy` will begin to fail, causing unhealthy and killing events to occur.</span></span>

<span data-ttu-id="4c5bb-124">These events can be viewed from the Azure portal or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-124">These events can be viewed from the Azure portal or Azure CLI.</span></span>

![Portal unhealthy event][portal-unhealthy]

<span data-ttu-id="4c5bb-126">By viewing the events in the Azure portal, events of type `Unhealthy` will be triggered upon the liveness command failing.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-126">By viewing the events in the Azure portal, events of type `Unhealthy` will be triggered upon the liveness command failing.</span></span> <span data-ttu-id="4c5bb-127">The subsequent event will be of type `Killing`, signifying a container deletion so a restart can begin.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-127">The subsequent event will be of type `Killing`, signifying a container deletion so a restart can begin.</span></span> <span data-ttu-id="4c5bb-128">The restart count for the container will increment each time this occurs.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-128">The restart count for the container will increment each time this occurs.</span></span>

<span data-ttu-id="4c5bb-129">Restarts are completed in-place so resources like public IP addresses and node-specific contents will be preserved.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-129">Restarts are completed in-place so resources like public IP addresses and node-specific contents will be preserved.</span></span>

![Portal restart counter][portal-restart]

<span data-ttu-id="4c5bb-131">If the liveness probe continuously fails and triggers too many restarts, your container will enter an exponential back off delay.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-131">If the liveness probe continuously fails and triggers too many restarts, your container will enter an exponential back off delay.</span></span>

## <a name="liveness-probes-and-restart-policies"></a><span data-ttu-id="4c5bb-132">Liveness probes and restart policies</span><span class="sxs-lookup"><span data-stu-id="4c5bb-132">Liveness probes and restart policies</span></span>

<span data-ttu-id="4c5bb-133">Restart policies supersede the restart behavior triggered by liveness probes.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-133">Restart policies supersede the restart behavior triggered by liveness probes.</span></span> <span data-ttu-id="4c5bb-134">For example, if you set a `restartPolicy = Never` *and* a liveness probe, the container group will not restart in the event of a failed liveness check.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-134">For example, if you set a `restartPolicy = Never` *and* a liveness probe, the container group will not restart in the event of a failed liveness check.</span></span> <span data-ttu-id="4c5bb-135">The container group will instead adhere to the container group's restart policy of `Never`.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-135">The container group will instead adhere to the container group's restart policy of `Never`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c5bb-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="4c5bb-136">Next steps</span></span>

<span data-ttu-id="4c5bb-137">Task-based scenarios may require a liveness probe to enable automatic restarts if a pre-requisite function is not working properly.</span><span class="sxs-lookup"><span data-stu-id="4c5bb-137">Task-based scenarios may require a liveness probe to enable automatic restarts if a pre-requisite function is not working properly.</span></span> <span data-ttu-id="4c5bb-138">For more information about running task-based containers, see [Run containerized tasks in Azure Container Instances](container-instances-restart-policy.md).</span><span class="sxs-lookup"><span data-stu-id="4c5bb-138">For more information about running task-based containers, see [Run containerized tasks in Azure Container Instances](container-instances-restart-policy.md).</span></span>

<!-- IMAGES -->
[portal-unhealthy]: ./media/container-instances-liveness-probe/unhealthy-killing.png
[portal-restart]: ./media/container-instances-liveness-probe/portal-restart.png
