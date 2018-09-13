---
title: Kubernetes cluster quickstart in Azure | Microsoft Docs
description: Deploy and get started with a Kubernetes cluster in Azure Container Service
services: container-service
documentationcenter: ''
author: anhowe
manager: timlt
editor: ''
tags: acs, azure-container-service, kubernetes
keywords: ''
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/05/2017
ms.author: anhowe
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8c282304f78049cbd6de32912fbbc68dafdde1c6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671702"
---
# <a name="get-started-with-a-kubernetes-cluster-in-container-service"></a><span data-ttu-id="69be6-103">Get started with a Kubernetes cluster in Container Service</span><span class="sxs-lookup"><span data-stu-id="69be6-103">Get started with a Kubernetes cluster in Container Service</span></span>


<span data-ttu-id="69be6-104">This walkthrough shows you how to use the Azure CLI 2.0 commands to create a Kubernetes cluster in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="69be6-104">This walkthrough shows you how to use the Azure CLI 2.0 commands to create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="69be6-105">Then, you can use the `kubectl` command-line tool to start working with containers in the cluster.</span><span class="sxs-lookup"><span data-stu-id="69be6-105">Then, you can use the `kubectl` command-line tool to start working with containers in the cluster.</span></span>

<span data-ttu-id="69be6-106">The following image shows the architecture of a Container Service cluster with one master and two agents.</span><span class="sxs-lookup"><span data-stu-id="69be6-106">The following image shows the architecture of a Container Service cluster with one master and two agents.</span></span> <span data-ttu-id="69be6-107">The master serves the Kubernetes REST API.</span><span class="sxs-lookup"><span data-stu-id="69be6-107">The master serves the Kubernetes REST API.</span></span> <span data-ttu-id="69be6-108">The agent nodes are grouped in an Azure availability set and run your containers.</span><span class="sxs-lookup"><span data-stu-id="69be6-108">The agent nodes are grouped in an Azure availability set and run your containers.</span></span> <span data-ttu-id="69be6-109">All VMs are in the same private virtual network and are fully accessible to each other.</span><span class="sxs-lookup"><span data-stu-id="69be6-109">All VMs are in the same private virtual network and are fully accessible to each other.</span></span>

![Image of Kubernetes cluster on Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-walkthrough/kubernetes.png)

## <a name="prerequisites"></a><span data-ttu-id="69be6-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="69be6-111">Prerequisites</span></span>
<span data-ttu-id="69be6-112">This walkthrough assumes that you have installed and set up the [Azure CLI 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="69be6-112">This walkthrough assumes that you have installed and set up the [Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span> 

<span data-ttu-id="69be6-113">The command examples assume that you run the Azure CLI in a bash shell, common on Linux and macOS.</span><span class="sxs-lookup"><span data-stu-id="69be6-113">The command examples assume that you run the Azure CLI in a bash shell, common on Linux and macOS.</span></span> <span data-ttu-id="69be6-114">If you run the Azure CLI on a Windows client, some scripting and file syntax may differ, depending on your command shell.</span><span class="sxs-lookup"><span data-stu-id="69be6-114">If you run the Azure CLI on a Windows client, some scripting and file syntax may differ, depending on your command shell.</span></span> 

## <a name="create-your-kubernetes-cluster"></a><span data-ttu-id="69be6-115">Create your Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="69be6-115">Create your Kubernetes cluster</span></span>

<span data-ttu-id="69be6-116">Here are brief shell commands that use the Azure CLI 2.0 to create your cluster.</span><span class="sxs-lookup"><span data-stu-id="69be6-116">Here are brief shell commands that use the Azure CLI 2.0 to create your cluster.</span></span> 

### <a name="create-a-resource-group"></a><span data-ttu-id="69be6-117">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="69be6-117">Create a resource group</span></span>
<span data-ttu-id="69be6-118">To create your cluster, you first need to create a resource group in a specific location.</span><span class="sxs-lookup"><span data-stu-id="69be6-118">To create your cluster, you first need to create a resource group in a specific location.</span></span> <span data-ttu-id="69be6-119">Run commands similar to the following:</span><span class="sxs-lookup"><span data-stu-id="69be6-119">Run commands similar to the following:</span></span>

```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus
az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="create-a-cluster"></a><span data-ttu-id="69be6-120">Create a cluster</span><span class="sxs-lookup"><span data-stu-id="69be6-120">Create a cluster</span></span>
<span data-ttu-id="69be6-121">Once you have a resource group, you can create a cluster in that group.</span><span class="sxs-lookup"><span data-stu-id="69be6-121">Once you have a resource group, you can create a cluster in that group.</span></span> <span data-ttu-id="69be6-122">The following example uses the `--generate-ssh-keys` option, which generates the necessary SSH public and private key files for the deployment if they don't exist already in the default `~/.ssh/` directory.</span><span class="sxs-lookup"><span data-stu-id="69be6-122">The following example uses the `--generate-ssh-keys` option, which generates the necessary SSH public and private key files for the deployment if they don't exist already in the default `~/.ssh/` directory.</span></span> 

<span data-ttu-id="69be6-123">This command also automatically generates the [Azure Active Directory service principal](container-service-kubernetes-service-principal.md) that a Kubernetes cluster in Azure uses.</span><span class="sxs-lookup"><span data-stu-id="69be6-123">This command also automatically generates the [Azure Active Directory service principal](container-service-kubernetes-service-principal.md) that a Kubernetes cluster in Azure uses.</span></span>

```azurecli
DNS_PREFIX=some-unique-value
CLUSTER_NAME=any-acs-cluster-name
az acs create --orchestrator-type=kubernetes --resource-group $RESOURCE_GROUP --name=$CLUSTER_NAME --dns-prefix=$DNS_PREFIX --generate-ssh-keys
```


<span data-ttu-id="69be6-124">After several minutes, the command completes, and you should have a working Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="69be6-124">After several minutes, the command completes, and you should have a working Kubernetes cluster.</span></span>

### <a name="connect-to-the-cluster"></a><span data-ttu-id="69be6-125">Connect to the cluster</span><span class="sxs-lookup"><span data-stu-id="69be6-125">Connect to the cluster</span></span>

<span data-ttu-id="69be6-126">To connect to the Kubernetes cluster from your client computer, you use [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span><span class="sxs-lookup"><span data-stu-id="69be6-126">To connect to the Kubernetes cluster from your client computer, you use [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span></span> 

<span data-ttu-id="69be6-127">If you don't already have `kubectl` installed, you can install it with:</span><span class="sxs-lookup"><span data-stu-id="69be6-127">If you don't already have `kubectl` installed, you can install it with:</span></span>

```azurecli
sudo az acs kubernetes install-cli
```
> [!TIP]
> <span data-ttu-id="69be6-128">By default, this command installs the `kubectl` binary to `/usr/local/bin/kubectl` on a Linux or macOS system, or to `C:\Program Files (x86)\kubectl.exe` on Windows.</span><span class="sxs-lookup"><span data-stu-id="69be6-128">By default, this command installs the `kubectl` binary to `/usr/local/bin/kubectl` on a Linux or macOS system, or to `C:\Program Files (x86)\kubectl.exe` on Windows.</span></span> <span data-ttu-id="69be6-129">To specify a different installation path, use the `--install-location` parameter.</span><span class="sxs-lookup"><span data-stu-id="69be6-129">To specify a different installation path, use the `--install-location` parameter.</span></span>
>

<span data-ttu-id="69be6-130">After `kubectl` is installed, ensure that its directory in your system path, or add it to the path.</span><span class="sxs-lookup"><span data-stu-id="69be6-130">After `kubectl` is installed, ensure that its directory in your system path, or add it to the path.</span></span> 


<span data-ttu-id="69be6-131">Then, run the following command to download the master Kubernetes cluster configuration to the `~/.kube/config` file:</span><span class="sxs-lookup"><span data-stu-id="69be6-131">Then, run the following command to download the master Kubernetes cluster configuration to the `~/.kube/config` file:</span></span>

```azurecli
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

<span data-ttu-id="69be6-132">For more options to install and configure `kubectl`, see [Connect to an Azure Container Service cluster](container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="69be6-132">For more options to install and configure `kubectl`, see [Connect to an Azure Container Service cluster](container-service-connect.md).</span></span>

<span data-ttu-id="69be6-133">At this point you should be ready to access your cluster from your machine.</span><span class="sxs-lookup"><span data-stu-id="69be6-133">At this point you should be ready to access your cluster from your machine.</span></span> <span data-ttu-id="69be6-134">Try running:</span><span class="sxs-lookup"><span data-stu-id="69be6-134">Try running:</span></span>

```bash
kubectl get nodes
```

<span data-ttu-id="69be6-135">Verify that you can see a list of the machines in your cluster.</span><span class="sxs-lookup"><span data-stu-id="69be6-135">Verify that you can see a list of the machines in your cluster.</span></span>

## <a name="create-your-first-kubernetes-service"></a><span data-ttu-id="69be6-136">Create your first Kubernetes service</span><span class="sxs-lookup"><span data-stu-id="69be6-136">Create your first Kubernetes service</span></span>

<span data-ttu-id="69be6-137">After completing this walkthrough, you will know how to:</span><span class="sxs-lookup"><span data-stu-id="69be6-137">After completing this walkthrough, you will know how to:</span></span>
* <span data-ttu-id="69be6-138">deploy a Docker application and expose it to the world</span><span class="sxs-lookup"><span data-stu-id="69be6-138">deploy a Docker application and expose it to the world</span></span>
* <span data-ttu-id="69be6-139">use `kubectl exec` to run commands in a container</span><span class="sxs-lookup"><span data-stu-id="69be6-139">use `kubectl exec` to run commands in a container</span></span> 
* <span data-ttu-id="69be6-140">access the Kubernetes dashboard</span><span class="sxs-lookup"><span data-stu-id="69be6-140">access the Kubernetes dashboard</span></span>

### <a name="start-a-simple-container"></a><span data-ttu-id="69be6-141">Start a simple container</span><span class="sxs-lookup"><span data-stu-id="69be6-141">Start a simple container</span></span>
<span data-ttu-id="69be6-142">You can run a simple container (in this case the Nginx web server) by running:</span><span class="sxs-lookup"><span data-stu-id="69be6-142">You can run a simple container (in this case the Nginx web server) by running:</span></span>

```bash
kubectl run nginx --image nginx
```

<span data-ttu-id="69be6-143">This command starts the Nginx Docker container in a pod on one of the nodes.</span><span class="sxs-lookup"><span data-stu-id="69be6-143">This command starts the Nginx Docker container in a pod on one of the nodes.</span></span>

<span data-ttu-id="69be6-144">To see the running container, run:</span><span class="sxs-lookup"><span data-stu-id="69be6-144">To see the running container, run:</span></span>

```bash
kubectl get pods
```

### <a name="expose-the-service-to-the-world"></a><span data-ttu-id="69be6-145">Expose the service to the world</span><span class="sxs-lookup"><span data-stu-id="69be6-145">Expose the service to the world</span></span>
<span data-ttu-id="69be6-146">To expose the service to the world, create a Kubernetes `Service` of type `LoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="69be6-146">To expose the service to the world, create a Kubernetes `Service` of type `LoadBalancer`:</span></span>

```bash
kubectl expose deployments nginx --port=80 --type=LoadBalancer
```

<span data-ttu-id="69be6-147">This command causes Kubernetes to create an Azure load balancer rule with a public IP address.</span><span class="sxs-lookup"><span data-stu-id="69be6-147">This command causes Kubernetes to create an Azure load balancer rule with a public IP address.</span></span> <span data-ttu-id="69be6-148">The change takes a few minutes to propagate to the load balancer.</span><span class="sxs-lookup"><span data-stu-id="69be6-148">The change takes a few minutes to propagate to the load balancer.</span></span> <span data-ttu-id="69be6-149">For more information, see [Load balance containers in a Kubernetes cluster in Azure Container Service](container-service-kubernetes-load-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="69be6-149">For more information, see [Load balance containers in a Kubernetes cluster in Azure Container Service](container-service-kubernetes-load-balancing.md).</span></span>

<span data-ttu-id="69be6-150">Run the following command to watch the service change from `pending` to display an external IP address:</span><span class="sxs-lookup"><span data-stu-id="69be6-150">Run the following command to watch the service change from `pending` to display an external IP address:</span></span>

```bash
watch 'kubectl get svc'
```

  ![Image of watching the transition from pending to external IP address](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-walkthrough/kubernetes-nginx3.png)

<span data-ttu-id="69be6-152">Once you see the external IP address, you can browse to it in your browser:</span><span class="sxs-lookup"><span data-stu-id="69be6-152">Once you see the external IP address, you can browse to it in your browser:</span></span>

  ![Image of browsing to Nginx](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-walkthrough/kubernetes-nginx4.png)  


### <a name="browse-the-kubernetes-ui"></a><span data-ttu-id="69be6-154">Browse the Kubernetes UI</span><span class="sxs-lookup"><span data-stu-id="69be6-154">Browse the Kubernetes UI</span></span>
<span data-ttu-id="69be6-155">To see the Kubernetes web interface, you can use:</span><span class="sxs-lookup"><span data-stu-id="69be6-155">To see the Kubernetes web interface, you can use:</span></span>

```bash
kubectl proxy
```
<span data-ttu-id="69be6-156">This command runs a simple authenticated proxy on localhost, which you can use to view the Kubernetes web UI running on [http://localhost:8001/ui](http://localhost:8001/ui).</span><span class="sxs-lookup"><span data-stu-id="69be6-156">This command runs a simple authenticated proxy on localhost, which you can use to view the Kubernetes web UI running on [http://localhost:8001/ui](http://localhost:8001/ui).</span></span> <span data-ttu-id="69be6-157">For more information, see [Using the Kubernetes web UI with Azure Container Service](container-service-kubernetes-ui.md).</span><span class="sxs-lookup"><span data-stu-id="69be6-157">For more information, see [Using the Kubernetes web UI with Azure Container Service](container-service-kubernetes-ui.md).</span></span>

![Image of Kubernetes dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-walkthrough/kubernetes-dashboard.png)

### <a name="remote-sessions-inside-your-containers"></a><span data-ttu-id="69be6-159">Remote sessions inside your containers</span><span class="sxs-lookup"><span data-stu-id="69be6-159">Remote sessions inside your containers</span></span>
<span data-ttu-id="69be6-160">Kubernetes allows you to run commands in a remote Docker container running in your cluster.</span><span class="sxs-lookup"><span data-stu-id="69be6-160">Kubernetes allows you to run commands in a remote Docker container running in your cluster.</span></span>

```bash
# Get the name of your nginx pods
kubectl get pods
```

<span data-ttu-id="69be6-161">Using your pod name, you can run a remote command on your pod.</span><span class="sxs-lookup"><span data-stu-id="69be6-161">Using your pod name, you can run a remote command on your pod.</span></span>  <span data-ttu-id="69be6-162">For example:</span><span class="sxs-lookup"><span data-stu-id="69be6-162">For example:</span></span>

```bash
kubectl exec <pod name> date
```

<span data-ttu-id="69be6-163">You can also get a fully interactive session using the `-it` flags:</span><span class="sxs-lookup"><span data-stu-id="69be6-163">You can also get a fully interactive session using the `-it` flags:</span></span>

```bash
kubectl exec <pod name> -it bash
```

![Remote session inside a container](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-walkthrough/kubernetes-remote.png)



## <a name="next-steps"></a><span data-ttu-id="69be6-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="69be6-165">Next steps</span></span>

<span data-ttu-id="69be6-166">To do more with your Kubernetes cluster, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="69be6-166">To do more with your Kubernetes cluster, see the following resources:</span></span>

* <span data-ttu-id="69be6-167">[Kubernetes Bootcamp](https://katacoda.com/embed/kubernetes-bootcamp/1/) - shows you how to deploy, scale, update, and debug containerized applications.</span><span class="sxs-lookup"><span data-stu-id="69be6-167">[Kubernetes Bootcamp](https://katacoda.com/embed/kubernetes-bootcamp/1/) - shows you how to deploy, scale, update, and debug containerized applications.</span></span>
* <span data-ttu-id="69be6-168">[Kubernetes User Guide](http://kubernetes.io/docs/user-guide/) - provides information on running programs in an existing Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="69be6-168">[Kubernetes User Guide](http://kubernetes.io/docs/user-guide/) - provides information on running programs in an existing Kubernetes cluster.</span></span>
* <span data-ttu-id="69be6-169">[Kubernetes Examples](https://github.com/kubernetes/kubernetes/tree/master/examples) - provides examples on how to run real applications with Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="69be6-169">[Kubernetes Examples](https://github.com/kubernetes/kubernetes/tree/master/examples) - provides examples on how to run real applications with Kubernetes.</span></span>





