---
title: Monitor containers in Azure Container Instances
description: Details on how to monitor the consumption of compute resources like CPU and memory by your containers in Azure Container Instances.
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: overview
ms.date: 04/24/2018
ms.author: marsma
ms.openlocfilehash: 2ab2a550e1e64f84613eb0fcda79cbd2b6164824
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869384"
---
# <a name="monitor-container-resources-in-azure-container-instances"></a><span data-ttu-id="6ae33-103">Monitor container resources in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="6ae33-103">Monitor container resources in Azure Container Instances</span></span>

<span data-ttu-id="6ae33-104">Azure Monitor provides insight into the compute resources used by your containers instances.</span><span class="sxs-lookup"><span data-stu-id="6ae33-104">Azure Monitor provides insight into the compute resources used by your containers instances.</span></span> <span data-ttu-id="6ae33-105">Use Azure Monitor to track the CPU and memory utilization of container groups and their containers.</span><span class="sxs-lookup"><span data-stu-id="6ae33-105">Use Azure Monitor to track the CPU and memory utilization of container groups and their containers.</span></span> <span data-ttu-id="6ae33-106">This resource usage data helps you determine the best CPU and memory settings for your container groups.</span><span class="sxs-lookup"><span data-stu-id="6ae33-106">This resource usage data helps you determine the best CPU and memory settings for your container groups.</span></span>

<span data-ttu-id="6ae33-107">This document details gathering CPU and memory usage for container instances using both the Azure portal and Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="6ae33-107">This document details gathering CPU and memory usage for container instances using both the Azure portal and Azure CLI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ae33-108">At this time, resource usage metrics are only available for Linux containers.</span><span class="sxs-lookup"><span data-stu-id="6ae33-108">At this time, resource usage metrics are only available for Linux containers.</span></span>
>

## <a name="available-metrics"></a><span data-ttu-id="6ae33-109">Available metrics</span><span class="sxs-lookup"><span data-stu-id="6ae33-109">Available metrics</span></span>

<span data-ttu-id="6ae33-110">Azure Monitor provides metrics on both **CPU** and **memory** usage for Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="6ae33-110">Azure Monitor provides metrics on both **CPU** and **memory** usage for Azure Container Instances.</span></span> <span data-ttu-id="6ae33-111">Both metrics are available for a container group and individual containers.</span><span class="sxs-lookup"><span data-stu-id="6ae33-111">Both metrics are available for a container group and individual containers.</span></span>

<span data-ttu-id="6ae33-112">CPU metrics are expressed in **millicores**.</span><span class="sxs-lookup"><span data-stu-id="6ae33-112">CPU metrics are expressed in **millicores**.</span></span> <span data-ttu-id="6ae33-113">One millicore is 1/1000th of a CPU core, so 500 millicores (or 500 m) represents 50% utilization of a CPU core.</span><span class="sxs-lookup"><span data-stu-id="6ae33-113">One millicore is 1/1000th of a CPU core, so 500 millicores (or 500 m) represents 50% utilization of a CPU core.</span></span>

<span data-ttu-id="6ae33-114">Memory metrics are expressed in **bytes**.</span><span class="sxs-lookup"><span data-stu-id="6ae33-114">Memory metrics are expressed in **bytes**.</span></span>

## <a name="get-metrics---azure-portal"></a><span data-ttu-id="6ae33-115">Get metrics - Azure portal</span><span class="sxs-lookup"><span data-stu-id="6ae33-115">Get metrics - Azure portal</span></span>

<span data-ttu-id="6ae33-116">When a container group is created, Azure Monitor data is available in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6ae33-116">When a container group is created, Azure Monitor data is available in the Azure portal.</span></span> <span data-ttu-id="6ae33-117">To see metrics for a container group, select the resource group and then the container group.</span><span class="sxs-lookup"><span data-stu-id="6ae33-117">To see metrics for a container group, select the resource group and then the container group.</span></span> <span data-ttu-id="6ae33-118">Here you can see pre-created charts for both CPU and memory usage.</span><span class="sxs-lookup"><span data-stu-id="6ae33-118">Here you can see pre-created charts for both CPU and memory usage.</span></span>

![dual-chart][dual-chart]

<span data-ttu-id="6ae33-120">If you have a container group that contains multiple containers, use a [dimension][monitor-dimension] to present metrics for each individual container.</span><span class="sxs-lookup"><span data-stu-id="6ae33-120">If you have a container group that contains multiple containers, use a [dimension][monitor-dimension] to present metrics for each individual container.</span></span> <span data-ttu-id="6ae33-121">To create a chart with individual container metrics, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6ae33-121">To create a chart with individual container metrics, perform the following steps:</span></span>

1. <span data-ttu-id="6ae33-122">Select **Monitor** from the left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="6ae33-122">Select **Monitor** from the left-hand navigation menu.</span></span>
2. <span data-ttu-id="6ae33-123">Select a container group and a metric (CPU or Memory).</span><span class="sxs-lookup"><span data-stu-id="6ae33-123">Select a container group and a metric (CPU or Memory).</span></span>
3. <span data-ttu-id="6ae33-124">Select the green dimension button, and select **Container Name**.</span><span class="sxs-lookup"><span data-stu-id="6ae33-124">Select the green dimension button, and select **Container Name**.</span></span>

![dimension][dimension]

## <a name="get-metrics---azure-cli"></a><span data-ttu-id="6ae33-126">Get metrics - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6ae33-126">Get metrics - Azure CLI</span></span>

<span data-ttu-id="6ae33-127">Container instances CPU and memory usage can also be gathered using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="6ae33-127">Container instances CPU and memory usage can also be gathered using the Azure CLI.</span></span> <span data-ttu-id="6ae33-128">First, get the ID of the container group using the following command.</span><span class="sxs-lookup"><span data-stu-id="6ae33-128">First, get the ID of the container group using the following command.</span></span> <span data-ttu-id="6ae33-129">Replace `<resource-group>` with your resource group name and `<container-group>` with the name of your container group.</span><span class="sxs-lookup"><span data-stu-id="6ae33-129">Replace `<resource-group>` with your resource group name and `<container-group>` with the name of your container group.</span></span>


```console
CONTAINER_GROUP=$(az container show --resource-group <resource-group> --name <container-group> --query id --output tsv)
```

<span data-ttu-id="6ae33-130">Use the following command to get **CPU** usage metrics.</span><span class="sxs-lookup"><span data-stu-id="6ae33-130">Use the following command to get **CPU** usage metrics.</span></span>

```console
$ az monitor metrics list --resource $CONTAINER_GROUP --metric CPUUsage --output table

Timestamp            Name              Average
-------------------  ------------  -----------
2018-04-22 04:39:00  CPU Usage
2018-04-22 04:40:00  CPU Usage
2018-04-22 04:41:00  CPU Usage
2018-04-22 04:42:00  CPU Usage
2018-04-22 04:43:00  CPU Usage      0.375
2018-04-22 04:44:00  CPU Usage      0.875
2018-04-22 04:45:00  CPU Usage      1
2018-04-22 04:46:00  CPU Usage      3.625
2018-04-22 04:47:00  CPU Usage      1.5
2018-04-22 04:48:00  CPU Usage      2.75
2018-04-22 04:49:00  CPU Usage      1.625
2018-04-22 04:50:00  CPU Usage      0.625
2018-04-22 04:51:00  CPU Usage      0.5
2018-04-22 04:52:00  CPU Usage      0.5
2018-04-22 04:53:00  CPU Usage      0.5
```

<span data-ttu-id="6ae33-131">And the following command to get **memory** usage metrics.</span><span class="sxs-lookup"><span data-stu-id="6ae33-131">And the following command to get **memory** usage metrics.</span></span>

```console
$ az monitor metrics list --resource $CONTAINER_GROUP --metric MemoryUsage --output table

Timestamp            Name              Average
-------------------  ------------  -----------
2018-04-22 04:38:00  Memory Usage
2018-04-22 04:39:00  Memory Usage
2018-04-22 04:40:00  Memory Usage
2018-04-22 04:41:00  Memory Usage
2018-04-22 04:42:00  Memory Usage  6.76915e+06
2018-04-22 04:43:00  Memory Usage  9.22061e+06
2018-04-22 04:44:00  Memory Usage  9.83552e+06
2018-04-22 04:45:00  Memory Usage  8.42906e+06
2018-04-22 04:46:00  Memory Usage  8.39526e+06
2018-04-22 04:47:00  Memory Usage  8.88013e+06
2018-04-22 04:48:00  Memory Usage  8.89293e+06
2018-04-22 04:49:00  Memory Usage  9.2073e+06
2018-04-22 04:50:00  Memory Usage  9.36243e+06
2018-04-22 04:51:00  Memory Usage  9.30509e+06
2018-04-22 04:52:00  Memory Usage  9.2416e+06
2018-04-22 04:53:00  Memory Usage  9.1008e+06
```

<span data-ttu-id="6ae33-132">For a multi-container group, the `containerName` dimension can be added to return this data per container.</span><span class="sxs-lookup"><span data-stu-id="6ae33-132">For a multi-container group, the `containerName` dimension can be added to return this data per container.</span></span>

```console
$ az monitor metrics list --resource $CONTAINER_GROUP --metric CPUUsage --dimension containerName --output table

Timestamp            Name          Containername             Average
-------------------  ------------  --------------------  -----------
2018-04-22 17:03:00  Memory Usage  aci-tutorial-app      1.95338e+07
2018-04-22 17:04:00  Memory Usage  aci-tutorial-app      1.93096e+07
2018-04-22 17:05:00  Memory Usage  aci-tutorial-app      1.91488e+07
2018-04-22 17:06:00  Memory Usage  aci-tutorial-app      1.94335e+07
2018-04-22 17:07:00  Memory Usage  aci-tutorial-app      1.97714e+07
2018-04-22 17:08:00  Memory Usage  aci-tutorial-app      1.96178e+07
2018-04-22 17:09:00  Memory Usage  aci-tutorial-app      1.93434e+07
2018-04-22 17:10:00  Memory Usage  aci-tutorial-app      1.92614e+07
2018-04-22 17:11:00  Memory Usage  aci-tutorial-app      1.90659e+07
2018-04-22 16:12:00  Memory Usage  aci-tutorial-sidecar  1.35373e+06
2018-04-22 16:13:00  Memory Usage  aci-tutorial-sidecar  1.28614e+06
2018-04-22 16:14:00  Memory Usage  aci-tutorial-sidecar  1.31379e+06
2018-04-22 16:15:00  Memory Usage  aci-tutorial-sidecar  1.29536e+06
2018-04-22 16:16:00  Memory Usage  aci-tutorial-sidecar  1.38138e+06
2018-04-22 16:17:00  Memory Usage  aci-tutorial-sidecar  1.41312e+06
2018-04-22 16:18:00  Memory Usage  aci-tutorial-sidecar  1.49914e+06
2018-04-22 16:19:00  Memory Usage  aci-tutorial-sidecar  1.43565e+06
2018-04-22 16:20:00  Memory Usage  aci-tutorial-sidecar  1.408e+06
```

## <a name="next-steps"></a><span data-ttu-id="6ae33-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="6ae33-133">Next steps</span></span>

<span data-ttu-id="6ae33-134">Learn more about Azure Monitoring at the [Azure Monitoring overview][azure-monitoring].</span><span class="sxs-lookup"><span data-stu-id="6ae33-134">Learn more about Azure Monitoring at the [Azure Monitoring overview][azure-monitoring].</span></span>

<!-- IMAGES -->
[cpu-chart]: ./media/container-instances-monitor/cpu-multi.png
[dimension]: ./media/container-instances-monitor/dimension.png
[dual-chart]: ./media/container-instances-monitor/metrics.png
[memory-chart]: ./media/container-instances-monitor/memory-multi.png

<!-- LINKS - Internal -->
[azure-monitoring]: ../monitoring-and-diagnostics/monitoring-overview.md
[monitor-dimension]: ../monitoring-and-diagnostics/monitoring-metric-charts.md#what-are-multi-dimensional-metrics
