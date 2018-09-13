---
title: Monitor Azure Kubernetes cluster with Datadog | Microsoft Docs
description: Monitoring Kubernetes cluster in Azure Container Service using Datadog
services: container-service
documentationcenter: ''
author: bburns
manager: timlt
editor: ''
tags: acs, azure-container-service, kubernetes
keywords: ''
ms.assetid: what-goes-here?
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.openlocfilehash: 901cbf5093c6a547f5dffa7ed6d71fe67caaadb9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552325"
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a><span data-ttu-id="7e438-103">Monitor an Azure Container Service cluster with DataDog</span><span class="sxs-lookup"><span data-stu-id="7e438-103">Monitor an Azure Container Service cluster with DataDog</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e438-104">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7e438-104">Prerequisites</span></span>
<span data-ttu-id="7e438-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="7e438-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="7e438-106">It also assumes that you have the `az` Azure cli and `kubectl` tools installed.</span><span class="sxs-lookup"><span data-stu-id="7e438-106">It also assumes that you have the `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="7e438-107">You can test if you have the `az` tool installed by running:</span><span class="sxs-lookup"><span data-stu-id="7e438-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="7e438-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="7e438-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="7e438-109">You can test if you have the `kubectl` tool installed by running:</span><span class="sxs-lookup"><span data-stu-id="7e438-109">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="7e438-110">If you don't have `kubectl` installed, you can run:</span><span class="sxs-lookup"><span data-stu-id="7e438-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a><span data-ttu-id="7e438-111">DataDog</span><span class="sxs-lookup"><span data-stu-id="7e438-111">DataDog</span></span>
<span data-ttu-id="7e438-112">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span><span class="sxs-lookup"><span data-stu-id="7e438-112">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="7e438-113">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span><span class="sxs-lookup"><span data-stu-id="7e438-113">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="7e438-114">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span><span class="sxs-lookup"><span data-stu-id="7e438-114">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="7e438-115">Datadog splits metrics into containers and images.</span><span class="sxs-lookup"><span data-stu-id="7e438-115">Datadog splits metrics into containers and images.</span></span>

<span data-ttu-id="7e438-116">You first need to [create an account](https://www.datadoghq.com/lpg/)</span><span class="sxs-lookup"><span data-stu-id="7e438-116">You first need to [create an account](https://www.datadoghq.com/lpg/)</span></span>

## <a name="installing-the-datadog-agent-with-a-daemonset"></a><span data-ttu-id="7e438-117">Installing the Datadog Agent with a DaemonSet</span><span class="sxs-lookup"><span data-stu-id="7e438-117">Installing the Datadog Agent with a DaemonSet</span></span>
<span data-ttu-id="7e438-118">DaemonSets are used by Kubernetes to run a single instance of a container on each host in the cluster.</span><span class="sxs-lookup"><span data-stu-id="7e438-118">DaemonSets are used by Kubernetes to run a single instance of a container on each host in the cluster.</span></span>
<span data-ttu-id="7e438-119">They're perfect for running monitoring agents.</span><span class="sxs-lookup"><span data-stu-id="7e438-119">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="7e438-120">Once you have logged into Datadog, you can follow the [Datadog instructions](https://app.datadoghq.com/account/settings#agent/kubernetes) to install Datadog agents on your cluster using a DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="7e438-120">Once you have logged into Datadog, you can follow the [Datadog instructions](https://app.datadoghq.com/account/settings#agent/kubernetes) to install Datadog agents on your cluster using a DaemonSet.</span></span>

## <a name="conclusion"></a><span data-ttu-id="7e438-121">Conclusion</span><span class="sxs-lookup"><span data-stu-id="7e438-121">Conclusion</span></span>
<span data-ttu-id="7e438-122">That's it!</span><span class="sxs-lookup"><span data-stu-id="7e438-122">That's it!</span></span> <span data-ttu-id="7e438-123">Once the agents are up and running you should see data in the console in a few minutes.</span><span class="sxs-lookup"><span data-stu-id="7e438-123">Once the agents are up and running you should see data in the console in a few minutes.</span></span> <span data-ttu-id="7e438-124">You can visit the integrated [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) to see a summary of your cluster.</span><span class="sxs-lookup"><span data-stu-id="7e438-124">You can visit the integrated [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) to see a summary of your cluster.</span></span>
