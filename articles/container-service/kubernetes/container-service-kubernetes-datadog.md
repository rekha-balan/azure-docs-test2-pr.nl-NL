---
title: Monitor Azure Kubernetes cluster with Datadog
description: Monitoring Kubernetes cluster in Azure Container Service using Datadog
services: container-service
author: bburns
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: 0a3f0baa4998dbc594023935575d659f7d45bbb9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868680"
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a><span data-ttu-id="9ae77-103">Monitor an Azure Container Service cluster with DataDog</span><span class="sxs-lookup"><span data-stu-id="9ae77-103">Monitor an Azure Container Service cluster with DataDog</span></span>

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

## <a name="prerequisites"></a><span data-ttu-id="9ae77-104">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9ae77-104">Prerequisites</span></span>
<span data-ttu-id="9ae77-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="9ae77-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="9ae77-106">It also assumes that you have the `az` Azure cli and `kubectl` tools installed.</span><span class="sxs-lookup"><span data-stu-id="9ae77-106">It also assumes that you have the `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="9ae77-107">You can test if you have the `az` tool installed by running:</span><span class="sxs-lookup"><span data-stu-id="9ae77-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="9ae77-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="9ae77-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="9ae77-109">You can test if you have the `kubectl` tool installed by running:</span><span class="sxs-lookup"><span data-stu-id="9ae77-109">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="9ae77-110">If you don't have `kubectl` installed, you can run:</span><span class="sxs-lookup"><span data-stu-id="9ae77-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a><span data-ttu-id="9ae77-111">DataDog</span><span class="sxs-lookup"><span data-stu-id="9ae77-111">DataDog</span></span>
<span data-ttu-id="9ae77-112">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span><span class="sxs-lookup"><span data-stu-id="9ae77-112">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="9ae77-113">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span><span class="sxs-lookup"><span data-stu-id="9ae77-113">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="9ae77-114">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span><span class="sxs-lookup"><span data-stu-id="9ae77-114">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="9ae77-115">Datadog splits metrics into containers and images.</span><span class="sxs-lookup"><span data-stu-id="9ae77-115">Datadog splits metrics into containers and images.</span></span>

<span data-ttu-id="9ae77-116">You first need to [create an account](https://www.datadoghq.com/lpg/)</span><span class="sxs-lookup"><span data-stu-id="9ae77-116">You first need to [create an account](https://www.datadoghq.com/lpg/)</span></span>

## <a name="installing-the-datadog-agent-with-a-daemonset"></a><span data-ttu-id="9ae77-117">Installing the Datadog Agent with a DaemonSet</span><span class="sxs-lookup"><span data-stu-id="9ae77-117">Installing the Datadog Agent with a DaemonSet</span></span>
<span data-ttu-id="9ae77-118">DaemonSets are used by Kubernetes to run a single instance of a container on each host in the cluster.</span><span class="sxs-lookup"><span data-stu-id="9ae77-118">DaemonSets are used by Kubernetes to run a single instance of a container on each host in the cluster.</span></span>
<span data-ttu-id="9ae77-119">They're perfect for running monitoring agents.</span><span class="sxs-lookup"><span data-stu-id="9ae77-119">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="9ae77-120">Once you have logged into Datadog, you can follow the [Datadog instructions](https://app.datadoghq.com/account/settings#agent/kubernetes) to install Datadog agents on your cluster using a DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="9ae77-120">Once you have logged into Datadog, you can follow the [Datadog instructions](https://app.datadoghq.com/account/settings#agent/kubernetes) to install Datadog agents on your cluster using a DaemonSet.</span></span>

## <a name="conclusion"></a><span data-ttu-id="9ae77-121">Conclusion</span><span class="sxs-lookup"><span data-stu-id="9ae77-121">Conclusion</span></span>
<span data-ttu-id="9ae77-122">That's it!</span><span class="sxs-lookup"><span data-stu-id="9ae77-122">That's it!</span></span> <span data-ttu-id="9ae77-123">Once the agents are up and running you should see data in the console in a few minutes.</span><span class="sxs-lookup"><span data-stu-id="9ae77-123">Once the agents are up and running you should see data in the console in a few minutes.</span></span> <span data-ttu-id="9ae77-124">You can visit the integrated [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) to see a summary of your cluster.</span><span class="sxs-lookup"><span data-stu-id="9ae77-124">You can visit the integrated [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) to see a summary of your cluster.</span></span>
