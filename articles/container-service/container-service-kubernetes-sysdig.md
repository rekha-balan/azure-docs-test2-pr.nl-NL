---
title: Monitor Azure Kubernetes cluster - Sysdig | Microsoft Docs
description: Monitoring Kubernetes cluster in Azure Container Service using Sysdig
services: container-service
documentationcenter: ''
author: bburns
manager: timlt
editor: ''
tags: acs, azure-container-service, kubernetes
keywords: ''
ms.assetid: ''
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.openlocfilehash: 65c56b49ce4f9fca8a5a613cacdf4c7bd70906fc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662273"
---
# <a name="monitor-an-azure-container-service-kubenrnetes-cluster-using-sysdig"></a><span data-ttu-id="a607d-103">Monitor an Azure Container Service Kubenrnetes cluster using Sysdig</span><span class="sxs-lookup"><span data-stu-id="a607d-103">Monitor an Azure Container Service Kubenrnetes cluster using Sysdig</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a607d-104">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a607d-104">Prerequisites</span></span>
<span data-ttu-id="a607d-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="a607d-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="a607d-106">It also assumes that you have the azure cli and kubectl tools installed.</span><span class="sxs-lookup"><span data-stu-id="a607d-106">It also assumes that you have the azure cli and kubectl tools installed.</span></span>

<span data-ttu-id="a607d-107">You can test if you have the `az` tool installed by running:</span><span class="sxs-lookup"><span data-stu-id="a607d-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="a607d-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="a607d-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="a607d-109">You can test if you have the `kubectl` tool installed by running:</span><span class="sxs-lookup"><span data-stu-id="a607d-109">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="a607d-110">If you don't have `kubectl` installed, you can run:</span><span class="sxs-lookup"><span data-stu-id="a607d-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a><span data-ttu-id="a607d-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="a607d-111">Sysdig</span></span>
<span data-ttu-id="a607d-112">Sysdig is an external monitoring as a service company which can monitor containers in your Kubernetes cluster running in Azure.</span><span class="sxs-lookup"><span data-stu-id="a607d-112">Sysdig is an external monitoring as a service company which can monitor containers in your Kubernetes cluster running in Azure.</span></span> <span data-ttu-id="a607d-113">Using Sysdig requires an active Sysdig account.</span><span class="sxs-lookup"><span data-stu-id="a607d-113">Using Sysdig requires an active Sysdig account.</span></span>
<span data-ttu-id="a607d-114">You can sign up for an account on their [site](https://app.sysdigcloud.com).</span><span class="sxs-lookup"><span data-stu-id="a607d-114">You can sign up for an account on their [site](https://app.sysdigcloud.com).</span></span>

<span data-ttu-id="a607d-115">Once you're logged in to the Sysdig cloud website, click on your user name, and on the page you should see your "Access Key."</span><span class="sxs-lookup"><span data-stu-id="a607d-115">Once you're logged in to the Sysdig cloud website, click on your user name, and on the page you should see your "Access Key."</span></span> 

![Sysdig API key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-monitoring-sysdig/sysdig2.png)

## <a name="installing-the-sysdig-agents-to-kubernetes"></a><span data-ttu-id="a607d-117">Installing the Sysdig agents to Kubernetes</span><span class="sxs-lookup"><span data-stu-id="a607d-117">Installing the Sysdig agents to Kubernetes</span></span>
<span data-ttu-id="a607d-118">To monitor your containers, Sysdig runs a process on each machine using a Kubernetes `DaemonSet`.</span><span class="sxs-lookup"><span data-stu-id="a607d-118">To monitor your containers, Sysdig runs a process on each machine using a Kubernetes `DaemonSet`.</span></span>
<span data-ttu-id="a607d-119">DaemonSets are Kubernetes API objects that run a single instance of a container per machine.</span><span class="sxs-lookup"><span data-stu-id="a607d-119">DaemonSets are Kubernetes API objects that run a single instance of a container per machine.</span></span>
<span data-ttu-id="a607d-120">They're perfect for installing tools like the Sysdig's monitoring agent.</span><span class="sxs-lookup"><span data-stu-id="a607d-120">They're perfect for installing tools like the Sysdig's monitoring agent.</span></span>

<span data-ttu-id="a607d-121">To install the Sysdig daemonset, you should first download [the template](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) from sysdig.</span><span class="sxs-lookup"><span data-stu-id="a607d-121">To install the Sysdig daemonset, you should first download [the template](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) from sysdig.</span></span> <span data-ttu-id="a607d-122">Save that file as `sysdig-daemonset.yaml`.</span><span class="sxs-lookup"><span data-stu-id="a607d-122">Save that file as `sysdig-daemonset.yaml`.</span></span>

<span data-ttu-id="a607d-123">On Linux and OS X you can run:</span><span class="sxs-lookup"><span data-stu-id="a607d-123">On Linux and OS X you can run:</span></span>

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

<span data-ttu-id="a607d-124">In PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a607d-124">In PowerShell:</span></span>

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

<span data-ttu-id="a607d-125">Next edit that file to insert your Access Key, that you obtained from your Sysdig account.</span><span class="sxs-lookup"><span data-stu-id="a607d-125">Next edit that file to insert your Access Key, that you obtained from your Sysdig account.</span></span>

<span data-ttu-id="a607d-126">Finally, create the DaemonSet:</span><span class="sxs-lookup"><span data-stu-id="a607d-126">Finally, create the DaemonSet:</span></span>

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a><span data-ttu-id="a607d-127">View your monitoring</span><span class="sxs-lookup"><span data-stu-id="a607d-127">View your monitoring</span></span>
<span data-ttu-id="a607d-128">Once installed and running, the agents should pump data back to Sysdig.</span><span class="sxs-lookup"><span data-stu-id="a607d-128">Once installed and running, the agents should pump data back to Sysdig.</span></span>  <span data-ttu-id="a607d-129">Go back to the [sysdig dashboard](https://app.sysdigcloud.com) and you should see information about your containers.</span><span class="sxs-lookup"><span data-stu-id="a607d-129">Go back to the [sysdig dashboard](https://app.sysdigcloud.com) and you should see information about your containers.</span></span>

<span data-ttu-id="a607d-130">You can also install Kubernetes-specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="a607d-130">You can also install Kubernetes-specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>

