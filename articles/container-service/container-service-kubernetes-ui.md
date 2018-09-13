---
title: Manage Azure Kubernetes cluster with web UI | Microsoft Docs
description: Using the Kubernetes web UI in Azure Container Service
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
ms.date: 02/21/2017
ms.author: bburns
ms.openlocfilehash: f97824bfefa2462e4e0e13f6802a08ce7a7b8429
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549256"
---
# <a name="using-the-kubernetes-web-ui-with-azure-container-service"></a><span data-ttu-id="a2054-103">Using the Kubernetes web UI with Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="a2054-103">Using the Kubernetes web UI with Azure Container Service</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2054-104">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a2054-104">Prerequisites</span></span>
<span data-ttu-id="a2054-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="a2054-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>


<span data-ttu-id="a2054-106">It also assumes that you have the Azure CLI 2.0 and `kubectl` tools installed.</span><span class="sxs-lookup"><span data-stu-id="a2054-106">It also assumes that you have the Azure CLI 2.0 and `kubectl` tools installed.</span></span>

<span data-ttu-id="a2054-107">You can test if you have the `az` tool installed by running:</span><span class="sxs-lookup"><span data-stu-id="a2054-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="a2054-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="a2054-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="a2054-109">You can test if you have the `kubectl` tool installed by running:</span><span class="sxs-lookup"><span data-stu-id="a2054-109">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="a2054-110">If you don't have `kubectl` installed, you can run:</span><span class="sxs-lookup"><span data-stu-id="a2054-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a><span data-ttu-id="a2054-111">Overview</span><span class="sxs-lookup"><span data-stu-id="a2054-111">Overview</span></span>

### <a name="connect-to-the-web-ui"></a><span data-ttu-id="a2054-112">Connect to the web UI</span><span class="sxs-lookup"><span data-stu-id="a2054-112">Connect to the web UI</span></span>
<span data-ttu-id="a2054-113">You can launch the Kubernetes web UI by running:</span><span class="sxs-lookup"><span data-stu-id="a2054-113">You can launch the Kubernetes web UI by running:</span></span>

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

<span data-ttu-id="a2054-114">This should open a web browser configured to talk to a secure proxy connecting your local machine to the Kubernetes Wweb UI.</span><span class="sxs-lookup"><span data-stu-id="a2054-114">This should open a web browser configured to talk to a secure proxy connecting your local machine to the Kubernetes Wweb UI.</span></span>

### <a name="create-and-expose-a-service"></a><span data-ttu-id="a2054-115">Create and expose a service</span><span class="sxs-lookup"><span data-stu-id="a2054-115">Create and expose a service</span></span>
1. <span data-ttu-id="a2054-116">In the Kubernetes web UI, click **Create** button in the upper right window.</span><span class="sxs-lookup"><span data-stu-id="a2054-116">In the Kubernetes web UI, click **Create** button in the upper right window.</span></span>

    ![Kubernetes Create UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/k8s/create.png)

    <span data-ttu-id="a2054-118">A dialog box opens where you can start creating your application.</span><span class="sxs-lookup"><span data-stu-id="a2054-118">A dialog box opens where you can start creating your application.</span></span>

2. <span data-ttu-id="a2054-119">Give it the name `hello-nginx`.</span><span class="sxs-lookup"><span data-stu-id="a2054-119">Give it the name `hello-nginx`.</span></span> <span data-ttu-id="a2054-120">Use the [`nginx` container from Docker](https://hub.docker.com/_/nginx/) and deploy three replicas of this web service.</span><span class="sxs-lookup"><span data-stu-id="a2054-120">Use the [`nginx` container from Docker](https://hub.docker.com/_/nginx/) and deploy three replicas of this web service.</span></span>

    ![Kubernetes Pod Create Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/k8s/nginx.png)

3. <span data-ttu-id="a2054-122">Under **Service**, select **External** and enter port 80.</span><span class="sxs-lookup"><span data-stu-id="a2054-122">Under **Service**, select **External** and enter port 80.</span></span>

    <span data-ttu-id="a2054-123">This setting load-balances traffic to the three replicas.</span><span class="sxs-lookup"><span data-stu-id="a2054-123">This setting load-balances traffic to the three replicas.</span></span>

    ![Kubernetes Service Create Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/k8s/service.png)

4. <span data-ttu-id="a2054-125">Click **Deploy** to deploy these containers and services.</span><span class="sxs-lookup"><span data-stu-id="a2054-125">Click **Deploy** to deploy these containers and services.</span></span>

    ![Kubernetes Deploy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/k8s/deploy.png)

### <a name="view-your-containers"></a><span data-ttu-id="a2054-127">View your containers</span><span class="sxs-lookup"><span data-stu-id="a2054-127">View your containers</span></span>
<span data-ttu-id="a2054-128">After you click **Deploy**, the UI shows a view of your service as it deploys:</span><span class="sxs-lookup"><span data-stu-id="a2054-128">After you click **Deploy**, the UI shows a view of your service as it deploys:</span></span>

![Kubernetes Status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/k8s/status.png)

<span data-ttu-id="a2054-130">You can see the status of each Kubernetes object in the circle on the left-hand side of the UI, under **Pods**.</span><span class="sxs-lookup"><span data-stu-id="a2054-130">You can see the status of each Kubernetes object in the circle on the left-hand side of the UI, under **Pods**.</span></span> <span data-ttu-id="a2054-131">If it is a partially full circle, then the object is still deploying.</span><span class="sxs-lookup"><span data-stu-id="a2054-131">If it is a partially full circle, then the object is still deploying.</span></span> <span data-ttu-id="a2054-132">When an object is fully deployed, it displays a green check mark:</span><span class="sxs-lookup"><span data-stu-id="a2054-132">When an object is fully deployed, it displays a green check mark:</span></span>

![Kubernetes Deployed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/k8s/deployed.png)

<span data-ttu-id="a2054-134">Once everything is running, click one of your pods to see details about the running web service.</span><span class="sxs-lookup"><span data-stu-id="a2054-134">Once everything is running, click one of your pods to see details about the running web service.</span></span>

![Kubernetes Pods](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/k8s/pods.png)

<span data-ttu-id="a2054-136">In the **Pods** view, you can see information about the containers in the pod as well as the CPU and memory resources used by those containers:</span><span class="sxs-lookup"><span data-stu-id="a2054-136">In the **Pods** view, you can see information about the containers in the pod as well as the CPU and memory resources used by those containers:</span></span>

![Kubernetes Resources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/k8s/resources.png)

<span data-ttu-id="a2054-138">If you don't see the resources, you may need to wait a few minutes for the monitoring data to propagate.</span><span class="sxs-lookup"><span data-stu-id="a2054-138">If you don't see the resources, you may need to wait a few minutes for the monitoring data to propagate.</span></span>

<span data-ttu-id="a2054-139">To see the logs for your container, click **View logs**.</span><span class="sxs-lookup"><span data-stu-id="a2054-139">To see the logs for your container, click **View logs**.</span></span>

![Kubernetes Logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/k8s/logs.png)

### <a name="viewing-your-service"></a><span data-ttu-id="a2054-141">Viewing your service</span><span class="sxs-lookup"><span data-stu-id="a2054-141">Viewing your service</span></span>
<span data-ttu-id="a2054-142">In addition to running your containers, the Kubernetes UI has created an external `Service` which provisions a load balancer to bring traffic to the containers in your cluster.</span><span class="sxs-lookup"><span data-stu-id="a2054-142">In addition to running your containers, the Kubernetes UI has created an external `Service` which provisions a load balancer to bring traffic to the containers in your cluster.</span></span>

<span data-ttu-id="a2054-143">In the left navigation pane, click **Services** to view all services (there should be only one).</span><span class="sxs-lookup"><span data-stu-id="a2054-143">In the left navigation pane, click **Services** to view all services (there should be only one).</span></span>

![Kubernetes Services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/k8s/service-deployed.png)

<span data-ttu-id="a2054-145">In that view, you should see an external endpoint (IP address) that has been allocated to your service.</span><span class="sxs-lookup"><span data-stu-id="a2054-145">In that view, you should see an external endpoint (IP address) that has been allocated to your service.</span></span>
<span data-ttu-id="a2054-146">If you click that IP address, you should see your Nginx container running behind the load balancer.</span><span class="sxs-lookup"><span data-stu-id="a2054-146">If you click that IP address, you should see your Nginx container running behind the load balancer.</span></span>

![nginx view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/k8s/nginx-page.png)

### <a name="resizing-your-service"></a><span data-ttu-id="a2054-148">Resizing your service</span><span class="sxs-lookup"><span data-stu-id="a2054-148">Resizing your service</span></span>
<span data-ttu-id="a2054-149">In addition to viewing your objects in the UI, you can edit and update the Kubernetes API objects.</span><span class="sxs-lookup"><span data-stu-id="a2054-149">In addition to viewing your objects in the UI, you can edit and update the Kubernetes API objects.</span></span>

<span data-ttu-id="a2054-150">First, click **Deployments** in the left navigation pane to see the deployment for your service.</span><span class="sxs-lookup"><span data-stu-id="a2054-150">First, click **Deployments** in the left navigation pane to see the deployment for your service.</span></span>

<span data-ttu-id="a2054-151">Once you are in that view, click on the replica set, and then click **Edit** in the upper navigation bar:</span><span class="sxs-lookup"><span data-stu-id="a2054-151">Once you are in that view, click on the replica set, and then click **Edit** in the upper navigation bar:</span></span>

![Kubernetes Edit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/k8s/edit.png)

<span data-ttu-id="a2054-153">Edit the `spec.replicas` field to be `2`, and click **Update**.</span><span class="sxs-lookup"><span data-stu-id="a2054-153">Edit the `spec.replicas` field to be `2`, and click **Update**.</span></span>

<span data-ttu-id="a2054-154">This causes the number of replicas to drop to two by deleting one of your pods.</span><span class="sxs-lookup"><span data-stu-id="a2054-154">This causes the number of replicas to drop to two by deleting one of your pods.</span></span>

 













