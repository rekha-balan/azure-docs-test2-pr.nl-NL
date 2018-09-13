---
title: Monitor Azure Kubernetes cluster - Sysdig
description: Monitoring Kubernetes cluster in Azure Container Service using Sysdig
services: container-service
author: bburns
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: bbf59a35f420b5bbf292fbdaa5a8bbc173e4ee24
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855841"
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a><span data-ttu-id="deb1d-103">Monitor an Azure Container Service Kubernetes cluster using Sysdig</span><span class="sxs-lookup"><span data-stu-id="deb1d-103">Monitor an Azure Container Service Kubernetes cluster using Sysdig</span></span>

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

## <a name="prerequisites"></a><span data-ttu-id="deb1d-104">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="deb1d-104">Prerequisites</span></span>
<span data-ttu-id="deb1d-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="deb1d-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="deb1d-106">It also assumes that you have the azure cli and kubectl tools installed.</span><span class="sxs-lookup"><span data-stu-id="deb1d-106">It also assumes that you have the azure cli and kubectl tools installed.</span></span>

<span data-ttu-id="deb1d-107">You can test if you have the `az` tool installed by running:</span><span class="sxs-lookup"><span data-stu-id="deb1d-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="deb1d-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="deb1d-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="deb1d-109">You can test if you have the `kubectl` tool installed by running:</span><span class="sxs-lookup"><span data-stu-id="deb1d-109">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="deb1d-110">If you don't have `kubectl` installed, you can run:</span><span class="sxs-lookup"><span data-stu-id="deb1d-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a><span data-ttu-id="deb1d-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="deb1d-111">Sysdig</span></span>
<span data-ttu-id="deb1d-112">Sysdig is an external monitoring as a service company which can monitor containers in your Kubernetes cluster running in Azure.</span><span class="sxs-lookup"><span data-stu-id="deb1d-112">Sysdig is an external monitoring as a service company which can monitor containers in your Kubernetes cluster running in Azure.</span></span> <span data-ttu-id="deb1d-113">Using Sysdig requires an active Sysdig account.</span><span class="sxs-lookup"><span data-stu-id="deb1d-113">Using Sysdig requires an active Sysdig account.</span></span>
<span data-ttu-id="deb1d-114">You can sign up for an account on their [site](https://app.sysdigcloud.com).</span><span class="sxs-lookup"><span data-stu-id="deb1d-114">You can sign up for an account on their [site](https://app.sysdigcloud.com).</span></span>

<span data-ttu-id="deb1d-115">Once you're logged in to the Sysdig cloud website, click on your user name, and on the page you should see your "Access Key."</span><span class="sxs-lookup"><span data-stu-id="deb1d-115">Once you're logged in to the Sysdig cloud website, click on your user name, and on the page you should see your "Access Key."</span></span> 

![Sysdig API key](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-the-sysdig-agents-to-kubernetes"></a><span data-ttu-id="deb1d-117">Installing the Sysdig agents to Kubernetes</span><span class="sxs-lookup"><span data-stu-id="deb1d-117">Installing the Sysdig agents to Kubernetes</span></span>
<span data-ttu-id="deb1d-118">To monitor your containers, Sysdig runs a process on each machine using a Kubernetes `DaemonSet`.</span><span class="sxs-lookup"><span data-stu-id="deb1d-118">To monitor your containers, Sysdig runs a process on each machine using a Kubernetes `DaemonSet`.</span></span>
<span data-ttu-id="deb1d-119">DaemonSets are Kubernetes API objects that run a single instance of a container per machine.</span><span class="sxs-lookup"><span data-stu-id="deb1d-119">DaemonSets are Kubernetes API objects that run a single instance of a container per machine.</span></span>
<span data-ttu-id="deb1d-120">They're perfect for installing tools like the Sysdig's monitoring agent.</span><span class="sxs-lookup"><span data-stu-id="deb1d-120">They're perfect for installing tools like the Sysdig's monitoring agent.</span></span>

<span data-ttu-id="deb1d-121">To install the Sysdig daemonset, you should first download [the template](https://github.com/draios/sysdig-cloud-scripts/tree/master/agent_deploy/kubernetes) from sysdig.</span><span class="sxs-lookup"><span data-stu-id="deb1d-121">To install the Sysdig daemonset, you should first download [the template](https://github.com/draios/sysdig-cloud-scripts/tree/master/agent_deploy/kubernetes) from sysdig.</span></span> <span data-ttu-id="deb1d-122">Save that file as `sysdig-daemonset.yaml`.</span><span class="sxs-lookup"><span data-stu-id="deb1d-122">Save that file as `sysdig-daemonset.yaml`.</span></span>

<span data-ttu-id="deb1d-123">On Linux and OS X you can run:</span><span class="sxs-lookup"><span data-stu-id="deb1d-123">On Linux and OS X you can run:</span></span>

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

<span data-ttu-id="deb1d-124">In PowerShell:</span><span class="sxs-lookup"><span data-stu-id="deb1d-124">In PowerShell:</span></span>

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

<span data-ttu-id="deb1d-125">Next edit that file to insert your Access Key, that you obtained from your Sysdig account.</span><span class="sxs-lookup"><span data-stu-id="deb1d-125">Next edit that file to insert your Access Key, that you obtained from your Sysdig account.</span></span>

<span data-ttu-id="deb1d-126">Finally, create the DaemonSet:</span><span class="sxs-lookup"><span data-stu-id="deb1d-126">Finally, create the DaemonSet:</span></span>

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a><span data-ttu-id="deb1d-127">View your monitoring</span><span class="sxs-lookup"><span data-stu-id="deb1d-127">View your monitoring</span></span>
<span data-ttu-id="deb1d-128">Once installed and running, the agents should pump data back to Sysdig.</span><span class="sxs-lookup"><span data-stu-id="deb1d-128">Once installed and running, the agents should pump data back to Sysdig.</span></span>  <span data-ttu-id="deb1d-129">Go back to the [sysdig dashboard](https://app.sysdigcloud.com) and you should see information about your containers.</span><span class="sxs-lookup"><span data-stu-id="deb1d-129">Go back to the [sysdig dashboard](https://app.sysdigcloud.com) and you should see information about your containers.</span></span>

<span data-ttu-id="deb1d-130">You can also install Kubernetes-specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="deb1d-130">You can also install Kubernetes-specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
