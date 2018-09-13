---
title: Quickstart - Azure Kubernetes cluster for Windows
description: Quickly learn to create a Kubernetes cluster for Windows containers in Azure Container Service with the Azure CLI.
services: container-service
author: dlepow
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc, devcenter
ms.openlocfilehash: b20f19c504a7967d01d51d976315fa49c2317885
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857362"
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a><span data-ttu-id="ef646-103">Deploy Kubernetes cluster for Windows containers</span><span class="sxs-lookup"><span data-stu-id="ef646-103">Deploy Kubernetes cluster for Windows containers</span></span>

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

<span data-ttu-id="ef646-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span><span class="sxs-lookup"><span data-stu-id="ef646-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="ef646-105">This guide details using the Azure CLI to deploy a [Kubernetes](https://kubernetes.io/docs/home/) cluster in [Azure Container Service](../container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="ef646-105">This guide details using the Azure CLI to deploy a [Kubernetes](https://kubernetes.io/docs/home/) cluster in [Azure Container Service](../container-service-intro.md).</span></span> <span data-ttu-id="ef646-106">Once the cluster is deployed, you connect to it with the Kubernetes `kubectl` command-line tool, and you deploy your first Windows container.</span><span class="sxs-lookup"><span data-stu-id="ef646-106">Once the cluster is deployed, you connect to it with the Kubernetes `kubectl` command-line tool, and you deploy your first Windows container.</span></span>

<span data-ttu-id="ef646-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="ef646-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ef646-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="ef646-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="ef646-109">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="ef646-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="ef646-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ef646-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

> [!NOTE]
> <span data-ttu-id="ef646-111">Support for Windows containers on Kubernetes in Azure Container Service is in preview.</span><span class="sxs-lookup"><span data-stu-id="ef646-111">Support for Windows containers on Kubernetes in Azure Container Service is in preview.</span></span> 
>

## <a name="create-a-resource-group"></a><span data-ttu-id="ef646-112">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="ef646-112">Create a resource group</span></span>

<span data-ttu-id="ef646-113">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span><span class="sxs-lookup"><span data-stu-id="ef646-113">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span></span> <span data-ttu-id="ef646-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="ef646-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="ef646-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="ef646-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="ef646-116">Create Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="ef646-116">Create Kubernetes cluster</span></span>
<span data-ttu-id="ef646-117">Create a Kubernetes cluster in Azure Container Service with the [az acs create](/cli/azure/acs#az-acs-create) command.</span><span class="sxs-lookup"><span data-stu-id="ef646-117">Create a Kubernetes cluster in Azure Container Service with the [az acs create](/cli/azure/acs#az-acs-create) command.</span></span> 

<span data-ttu-id="ef646-118">The following example creates a cluster named *myK8sCluster* with one Linux master node and two Windows agent nodes.</span><span class="sxs-lookup"><span data-stu-id="ef646-118">The following example creates a cluster named *myK8sCluster* with one Linux master node and two Windows agent nodes.</span></span> <span data-ttu-id="ef646-119">This example creates SSH keys needed to connect to the Linux master.</span><span class="sxs-lookup"><span data-stu-id="ef646-119">This example creates SSH keys needed to connect to the Linux master.</span></span> <span data-ttu-id="ef646-120">This example uses *azureuser* for an administrative user name and *myPassword12* as the password on the Windows nodes.</span><span class="sxs-lookup"><span data-stu-id="ef646-120">This example uses *azureuser* for an administrative user name and *myPassword12* as the password on the Windows nodes.</span></span> <span data-ttu-id="ef646-121">Update these values to something appropriate to your environment.</span><span class="sxs-lookup"><span data-stu-id="ef646-121">Update these values to something appropriate to your environment.</span></span> 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

<span data-ttu-id="ef646-122">After several minutes, the command completes, and shows you information about your deployment.</span><span class="sxs-lookup"><span data-stu-id="ef646-122">After several minutes, the command completes, and shows you information about your deployment.</span></span>

## <a name="install-kubectl"></a><span data-ttu-id="ef646-123">Install kubectl</span><span class="sxs-lookup"><span data-stu-id="ef646-123">Install kubectl</span></span>

<span data-ttu-id="ef646-124">To connect to the Kubernetes cluster from your client computer, use [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span><span class="sxs-lookup"><span data-stu-id="ef646-124">To connect to the Kubernetes cluster from your client computer, use [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span></span> 

<span data-ttu-id="ef646-125">If you're using Azure CloudShell, `kubectl` is already installed.</span><span class="sxs-lookup"><span data-stu-id="ef646-125">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="ef646-126">If you want to install it locally, you can use the [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span><span class="sxs-lookup"><span data-stu-id="ef646-126">If you want to install it locally, you can use the [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="ef646-127">The following Azure CLI example installs `kubectl` to your system.</span><span class="sxs-lookup"><span data-stu-id="ef646-127">The following Azure CLI example installs `kubectl` to your system.</span></span> <span data-ttu-id="ef646-128">On Windows, run this command as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ef646-128">On Windows, run this command as an administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a><span data-ttu-id="ef646-129">Connect with kubectl</span><span class="sxs-lookup"><span data-stu-id="ef646-129">Connect with kubectl</span></span>

<span data-ttu-id="ef646-130">To configure `kubectl` to connect to your Kubernetes cluster, run the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span><span class="sxs-lookup"><span data-stu-id="ef646-130">To configure `kubectl` to connect to your Kubernetes cluster, run the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="ef646-131">The following example downloads the cluster configuration for your Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="ef646-131">The following example downloads the cluster configuration for your Kubernetes cluster.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="ef646-132">To verify the connection to your cluster from your machine, try running:</span><span class="sxs-lookup"><span data-stu-id="ef646-132">To verify the connection to your cluster from your machine, try running:</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="ef646-133">`kubectl` lists the master and agent nodes.</span><span class="sxs-lookup"><span data-stu-id="ef646-133">`kubectl` lists the master and agent nodes.</span></span>

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a><span data-ttu-id="ef646-134">Deploy a Windows IIS container</span><span class="sxs-lookup"><span data-stu-id="ef646-134">Deploy a Windows IIS container</span></span>

<span data-ttu-id="ef646-135">You can run a Docker container inside a Kubernetes *pod*, which contains one or more containers.</span><span class="sxs-lookup"><span data-stu-id="ef646-135">You can run a Docker container inside a Kubernetes *pod*, which contains one or more containers.</span></span> 

<span data-ttu-id="ef646-136">This basic example uses a JSON file to specify a Microsoft Internet Information Server (IIS) container, and then creates the pod using the `kubctl apply` command.</span><span class="sxs-lookup"><span data-stu-id="ef646-136">This basic example uses a JSON file to specify a Microsoft Internet Information Server (IIS) container, and then creates the pod using the `kubctl apply` command.</span></span> 

<span data-ttu-id="ef646-137">Create a local file named `iis.json` and copy the following text.</span><span class="sxs-lookup"><span data-stu-id="ef646-137">Create a local file named `iis.json` and copy the following text.</span></span> <span data-ttu-id="ef646-138">This file tells Kubernetes to run IIS on Windows Server 2016 Nano Server, using a public container image from [Docker Hub](https://hub.docker.com/r/microsoft/iis/).</span><span class="sxs-lookup"><span data-stu-id="ef646-138">This file tells Kubernetes to run IIS on Windows Server 2016 Nano Server, using a public container image from [Docker Hub](https://hub.docker.com/r/microsoft/iis/).</span></span> <span data-ttu-id="ef646-139">The container uses port 80, but initially is only accessible within the cluster network.</span><span class="sxs-lookup"><span data-stu-id="ef646-139">The container uses port 80, but initially is only accessible within the cluster network.</span></span>

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "microsoft/iis:nanoserver",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

<span data-ttu-id="ef646-140">To start the pod, type:</span><span class="sxs-lookup"><span data-stu-id="ef646-140">To start the pod, type:</span></span>
  
```azurecli-interactive
kubectl apply -f iis.json
```  

<span data-ttu-id="ef646-141">To track the deployment, type:</span><span class="sxs-lookup"><span data-stu-id="ef646-141">To track the deployment, type:</span></span>
  
```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="ef646-142">While the pod is deploying, the status is `ContainerCreating`.</span><span class="sxs-lookup"><span data-stu-id="ef646-142">While the pod is deploying, the status is `ContainerCreating`.</span></span> <span data-ttu-id="ef646-143">It can take a few minutes for the container to enter the `Running` state.</span><span class="sxs-lookup"><span data-stu-id="ef646-143">It can take a few minutes for the container to enter the `Running` state.</span></span>

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="ef646-144">View the IIS welcome page</span><span class="sxs-lookup"><span data-stu-id="ef646-144">View the IIS welcome page</span></span>

<span data-ttu-id="ef646-145">To expose the pod to the world with a public IP address, type the following command:</span><span class="sxs-lookup"><span data-stu-id="ef646-145">To expose the pod to the world with a public IP address, type the following command:</span></span>

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

<span data-ttu-id="ef646-146">With this command, Kubernetes creates a service and an Azure load balancer rule with a public IP address for the service.</span><span class="sxs-lookup"><span data-stu-id="ef646-146">With this command, Kubernetes creates a service and an Azure load balancer rule with a public IP address for the service.</span></span> 

<span data-ttu-id="ef646-147">Run the following command to see the status of the service.</span><span class="sxs-lookup"><span data-stu-id="ef646-147">Run the following command to see the status of the service.</span></span>

```azurecli-interactive
kubectl get svc
```

<span data-ttu-id="ef646-148">Initially the IP address appears as `pending`.</span><span class="sxs-lookup"><span data-stu-id="ef646-148">Initially the IP address appears as `pending`.</span></span> <span data-ttu-id="ef646-149">After a few minutes, the external IP address of the `iis` pod is set:</span><span class="sxs-lookup"><span data-stu-id="ef646-149">After a few minutes, the external IP address of the `iis` pod is set:</span></span>
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

<span data-ttu-id="ef646-150">You can use a web browser of your choice to see the default IIS welcome page at the external IP address:</span><span class="sxs-lookup"><span data-stu-id="ef646-150">You can use a web browser of your choice to see the default IIS welcome page at the external IP address:</span></span>

![Image of browsing to IIS](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a><span data-ttu-id="ef646-152">Delete cluster</span><span class="sxs-lookup"><span data-stu-id="ef646-152">Delete cluster</span></span>
<span data-ttu-id="ef646-153">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, container service, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="ef646-153">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a><span data-ttu-id="ef646-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="ef646-154">Next steps</span></span>

<span data-ttu-id="ef646-155">In this quick start, you deployed a Kubernetes cluster, connected with `kubectl`, and deployed a pod with an IIS container.</span><span class="sxs-lookup"><span data-stu-id="ef646-155">In this quick start, you deployed a Kubernetes cluster, connected with `kubectl`, and deployed a pod with an IIS container.</span></span> <span data-ttu-id="ef646-156">To learn more about Azure Container Service, continue to the Kubernetes tutorial.</span><span class="sxs-lookup"><span data-stu-id="ef646-156">To learn more about Azure Container Service, continue to the Kubernetes tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ef646-157">Manage an ACS Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="ef646-157">Manage an ACS Kubernetes cluster</span></span>](container-service-tutorial-kubernetes-prepare-app.md)
