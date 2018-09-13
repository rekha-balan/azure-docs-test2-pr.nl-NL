---
title: Monitor an Azure Kubernetes cluster with CoScale
description: Monitor a Kubernetes cluster in Azure Container Service using CoScale
services: container-service
author: fryckbos
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 16580307193bbb7eb9b401eb1b14356e8589d6e2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857207"
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a><span data-ttu-id="80e25-103">Monitor an Azure Container Service Kubernetes cluster with CoScale</span><span class="sxs-lookup"><span data-stu-id="80e25-103">Monitor an Azure Container Service Kubernetes cluster with CoScale</span></span>

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

<span data-ttu-id="80e25-104">In this article, we show you how to deploy the [CoScale](https://www.coscale.com/) agent to monitor all nodes and containers in your Kubernetes cluster in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="80e25-104">In this article, we show you how to deploy the [CoScale](https://www.coscale.com/) agent to monitor all nodes and containers in your Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="80e25-105">You need an account with CoScale for this configuration.</span><span class="sxs-lookup"><span data-stu-id="80e25-105">You need an account with CoScale for this configuration.</span></span> 


## <a name="about-coscale"></a><span data-ttu-id="80e25-106">About CoScale</span><span class="sxs-lookup"><span data-stu-id="80e25-106">About CoScale</span></span> 

<span data-ttu-id="80e25-107">CoScale is a monitoring platform that gathers metrics and events from all containers in several orchestration platforms.</span><span class="sxs-lookup"><span data-stu-id="80e25-107">CoScale is a monitoring platform that gathers metrics and events from all containers in several orchestration platforms.</span></span> <span data-ttu-id="80e25-108">CoScale offers full-stack monitoring for Kubernetes environments.</span><span class="sxs-lookup"><span data-stu-id="80e25-108">CoScale offers full-stack monitoring for Kubernetes environments.</span></span> <span data-ttu-id="80e25-109">It provides visualizations and analytics for all layers in the stack: the OS, Kubernetes, Docker, and applications running inside your containers.</span><span class="sxs-lookup"><span data-stu-id="80e25-109">It provides visualizations and analytics for all layers in the stack: the OS, Kubernetes, Docker, and applications running inside your containers.</span></span> <span data-ttu-id="80e25-110">CoScale offers several built-in monitoring dashboards, and it has built-in anomaly detection to allow operators and developers to find infrastructure and application issues fast.</span><span class="sxs-lookup"><span data-stu-id="80e25-110">CoScale offers several built-in monitoring dashboards, and it has built-in anomaly detection to allow operators and developers to find infrastructure and application issues fast.</span></span>

![CoScale UI](./media/container-service-kubernetes-coscale/coscale.png)

<span data-ttu-id="80e25-112">As shown in this article, you can install agents on a Kubernetes cluster to run CoScale as a SaaS solution.</span><span class="sxs-lookup"><span data-stu-id="80e25-112">As shown in this article, you can install agents on a Kubernetes cluster to run CoScale as a SaaS solution.</span></span> <span data-ttu-id="80e25-113">If you want to keep your data on-site, CoScale is also available for on-premises installation.</span><span class="sxs-lookup"><span data-stu-id="80e25-113">If you want to keep your data on-site, CoScale is also available for on-premises installation.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="80e25-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="80e25-114">Prerequisites</span></span>

<span data-ttu-id="80e25-115">You first need to [create a CoScale account](https://www.coscale.com/free-trial).</span><span class="sxs-lookup"><span data-stu-id="80e25-115">You first need to [create a CoScale account](https://www.coscale.com/free-trial).</span></span>

<span data-ttu-id="80e25-116">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="80e25-116">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="80e25-117">It also assumes that you have the `az` Azure CLI and `kubectl` tools installed.</span><span class="sxs-lookup"><span data-stu-id="80e25-117">It also assumes that you have the `az` Azure CLI and `kubectl` tools installed.</span></span>

<span data-ttu-id="80e25-118">You can test if you have the `az` tool installed by running:</span><span class="sxs-lookup"><span data-stu-id="80e25-118">You can test if you have the `az` tool installed by running:</span></span>

```azurecli
az --version
```

<span data-ttu-id="80e25-119">If you don't have the `az` tool installed, there are instructions [here](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="80e25-119">If you don't have the `az` tool installed, there are instructions [here](/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="80e25-120">You can test if you have the `kubectl` tool installed by running:</span><span class="sxs-lookup"><span data-stu-id="80e25-120">You can test if you have the `kubectl` tool installed by running:</span></span>

```bash
kubectl version
```

<span data-ttu-id="80e25-121">If you don't have `kubectl` installed, you can run:</span><span class="sxs-lookup"><span data-stu-id="80e25-121">If you don't have `kubectl` installed, you can run:</span></span>

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-the-coscale-agent-with-a-daemonset"></a><span data-ttu-id="80e25-122">Installing the CoScale agent with a DaemonSet</span><span class="sxs-lookup"><span data-stu-id="80e25-122">Installing the CoScale agent with a DaemonSet</span></span>
<span data-ttu-id="80e25-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) are used by Kubernetes to run a single instance of a container on each host in the cluster.</span><span class="sxs-lookup"><span data-stu-id="80e25-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) are used by Kubernetes to run a single instance of a container on each host in the cluster.</span></span>
<span data-ttu-id="80e25-124">They're perfect for running monitoring agents such as the CoScale agent.</span><span class="sxs-lookup"><span data-stu-id="80e25-124">They're perfect for running monitoring agents such as the CoScale agent.</span></span>

<span data-ttu-id="80e25-125">After you log in to CoScale, go to the [agent page](https://app.coscale.com/) to install CoScale agents on your cluster using a DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="80e25-125">After you log in to CoScale, go to the [agent page](https://app.coscale.com/) to install CoScale agents on your cluster using a DaemonSet.</span></span> <span data-ttu-id="80e25-126">The CoScale UI provides guided configuration steps to create an agent and start monitoring your complete Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="80e25-126">The CoScale UI provides guided configuration steps to create an agent and start monitoring your complete Kubernetes cluster.</span></span>

![CoScale agent configuration](./media/container-service-kubernetes-coscale/installation.png)

<span data-ttu-id="80e25-128">To start the agent on the cluster, run the supplied command:</span><span class="sxs-lookup"><span data-stu-id="80e25-128">To start the agent on the cluster, run the supplied command:</span></span>

![Start the CoScale agent](./media/container-service-kubernetes-coscale/agent_script.png)

<span data-ttu-id="80e25-130">That's it!</span><span class="sxs-lookup"><span data-stu-id="80e25-130">That's it!</span></span> <span data-ttu-id="80e25-131">Once the agents are up and running, you should see data in the console in a few minutes.</span><span class="sxs-lookup"><span data-stu-id="80e25-131">Once the agents are up and running, you should see data in the console in a few minutes.</span></span> <span data-ttu-id="80e25-132">Visit the [agent page](https://app.coscale.com/) to see a summary of your cluster, perform additional configuration steps, and see dashboards such as the **Kubernetes cluster overview**.</span><span class="sxs-lookup"><span data-stu-id="80e25-132">Visit the [agent page](https://app.coscale.com/) to see a summary of your cluster, perform additional configuration steps, and see dashboards such as the **Kubernetes cluster overview**.</span></span>

![Kubernetes cluster overview](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

<span data-ttu-id="80e25-134">The CoScale agent is automatically deployed on new machines in the cluster.</span><span class="sxs-lookup"><span data-stu-id="80e25-134">The CoScale agent is automatically deployed on new machines in the cluster.</span></span> <span data-ttu-id="80e25-135">The agent updates automatically when a new version is released.</span><span class="sxs-lookup"><span data-stu-id="80e25-135">The agent updates automatically when a new version is released.</span></span>


## <a name="next-steps"></a><span data-ttu-id="80e25-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="80e25-136">Next steps</span></span>

<span data-ttu-id="80e25-137">See the [CoScale documentation](http://docs.coscale.com/) and [blog](https://www.coscale.com/blog) for more more information about CoScale monitoring solutions.</span><span class="sxs-lookup"><span data-stu-id="80e25-137">See the [CoScale documentation](http://docs.coscale.com/) and [blog](https://www.coscale.com/blog) for more more information about CoScale monitoring solutions.</span></span> 

