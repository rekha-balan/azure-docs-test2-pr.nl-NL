---
title: Quickstart - Azure Kubernetes cluster for Linux
description: Quickly learn to create a Kubernetes cluster for Linux containers in Azure Container Service with the Azure CLI.
services: container-service
author: neilpeterson
manager: jeconnoc
ms.service: container-service
ms.topic: quickstart
ms.date: 02/26/2018
ms.author: nepeters
ms.custom: H1Hack27Feb2017, mvc, devcenter
ms.openlocfilehash: c592952c4e6ebff0db0833fd7b235fbb911909af
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866938"
---
# <a name="deploy-kubernetes-cluster-for-linux-containers"></a><span data-ttu-id="f6fdf-103">Deploy Kubernetes cluster for Linux containers</span><span class="sxs-lookup"><span data-stu-id="f6fdf-103">Deploy Kubernetes cluster for Linux containers</span></span>

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

<span data-ttu-id="f6fdf-104">In this quick start, a Kubernetes cluster is deployed using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-104">In this quick start, a Kubernetes cluster is deployed using the Azure CLI.</span></span> <span data-ttu-id="f6fdf-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on the cluster.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on the cluster.</span></span> <span data-ttu-id="f6fdf-106">Once completed, the application is accessible over the internet.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-106">Once completed, the application is accessible over the internet.</span></span> 

<span data-ttu-id="f6fdf-107">The example application used in this document is written in Python.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-107">The example application used in this document is written in Python.</span></span> <span data-ttu-id="f6fdf-108">The concepts and steps detailed here can be used to deploy any container image into a Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-108">The concepts and steps detailed here can be used to deploy any container image into a Kubernetes cluster.</span></span> <span data-ttu-id="f6fdf-109">The code, Dockerfile, and pre-created Kubernetes manifest files related to this project are available on [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span><span class="sxs-lookup"><span data-stu-id="f6fdf-109">The code, Dockerfile, and pre-created Kubernetes manifest files related to this project are available on [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span></span>

![Image of browsing to Azure Vote](media/container-service-kubernetes-walkthrough/azure-vote.png)

<span data-ttu-id="f6fdf-111">This quick start assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see the [Kubernetes documentation]( https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="f6fdf-111">This quick start assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see the [Kubernetes documentation]( https://kubernetes.io/docs/home/).</span></span>

<span data-ttu-id="f6fdf-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f6fdf-113">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-113">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="f6fdf-114">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="f6fdf-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f6fdf-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="f6fdf-116">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="f6fdf-116">Create a resource group</span></span>

<span data-ttu-id="f6fdf-117">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-117">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span></span> <span data-ttu-id="f6fdf-118">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-118">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="f6fdf-119">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-119">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="f6fdf-120">Output:</span><span class="sxs-lookup"><span data-stu-id="f6fdf-120">Output:</span></span>

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westeurope",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="f6fdf-121">Create Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="f6fdf-121">Create Kubernetes cluster</span></span>

<span data-ttu-id="f6fdf-122">Create a Kubernetes cluster in Azure Container Service with the [az acs create](/cli/azure/acs#az-acs-create) command.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-122">Create a Kubernetes cluster in Azure Container Service with the [az acs create](/cli/azure/acs#az-acs-create) command.</span></span> <span data-ttu-id="f6fdf-123">The following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-123">The following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type kubernetes --resource-group myResourceGroup --name myK8sCluster --generate-ssh-keys
```

<span data-ttu-id="f6fdf-124">In some cases, such as with a limited trial, an Azure subscription has limited access to Azure resources.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-124">In some cases, such as with a limited trial, an Azure subscription has limited access to Azure resources.</span></span> <span data-ttu-id="f6fdf-125">If the deployment fails due to limited available cores, reduce the default agent count by adding `--agent-count 1` to the [az acs create](/cli/azure/acs#az-acs-create) command.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-125">If the deployment fails due to limited available cores, reduce the default agent count by adding `--agent-count 1` to the [az acs create](/cli/azure/acs#az-acs-create) command.</span></span> 

<span data-ttu-id="f6fdf-126">After several minutes, the command completes and returns json formatted information about the cluster.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-126">After several minutes, the command completes and returns json formatted information about the cluster.</span></span> 

## <a name="connect-to-the-cluster"></a><span data-ttu-id="f6fdf-127">Connect to the cluster</span><span class="sxs-lookup"><span data-stu-id="f6fdf-127">Connect to the cluster</span></span>

<span data-ttu-id="f6fdf-128">To manage a Kubernetes cluster, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-128">To manage a Kubernetes cluster, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span></span> 

<span data-ttu-id="f6fdf-129">If you're using Azure CloudShell, kubectl is already installed.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-129">If you're using Azure CloudShell, kubectl is already installed.</span></span> <span data-ttu-id="f6fdf-130">If you want to install it locally, you can use the [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-130">If you want to install it locally, you can use the [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="f6fdf-131">To configure kubectl to connect to your Kubernetes cluster, run the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-131">To configure kubectl to connect to your Kubernetes cluster, run the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="f6fdf-132">This step downloads credentials and configures the Kubernetes CLI to use them.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-132">This step downloads credentials and configures the Kubernetes CLI to use them.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="f6fdf-133">To verify the connection to your cluster, use the [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command to return a list of the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-133">To verify the connection to your cluster, use the [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command to return a list of the cluster nodes.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="f6fdf-134">Output:</span><span class="sxs-lookup"><span data-stu-id="f6fdf-134">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-14ad53a1-0    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-1    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-2    Ready                      10m       v1.6.6
k8s-master-14ad53a1-0   Ready,SchedulingDisabled   10m       v1.6.6
```

## <a name="run-the-application"></a><span data-ttu-id="f6fdf-135">Run the application</span><span class="sxs-lookup"><span data-stu-id="f6fdf-135">Run the application</span></span>

<span data-ttu-id="f6fdf-136">A Kubernetes manifest file defines a desired state for the cluster, including what container images should be running.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-136">A Kubernetes manifest file defines a desired state for the cluster, including what container images should be running.</span></span> <span data-ttu-id="f6fdf-137">For this example, a manifest is used to create all objects needed to run the Azure Vote application.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-137">For this example, a manifest is used to create all objects needed to run the Azure Vote application.</span></span> 

<span data-ttu-id="f6fdf-138">Create a file named `azure-vote.yml` and copy into it the following YAML.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-138">Create a file named `azure-vote.yml` and copy into it the following YAML.</span></span> <span data-ttu-id="f6fdf-139">If you are working in Azure Cloud Shell, this file can be created using vi or Nano as if working on a virtual or physical system.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-139">If you are working in Azure Cloud Shell, this file can be created using vi or Nano as if working on a virtual or physical system.</span></span>

```yaml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-back
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-back
    spec:
      containers:
      - name: azure-vote-back
        image: redis
        ports:
        - containerPort: 6379
          name: redis
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-back
spec:
  ports:
  - port: 6379
  selector:
    app: azure-vote-back
---
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-front
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-front
    spec:
      containers:
      - name: azure-vote-front
        image: microsoft/azure-vote-front:v1
        ports:
        - containerPort: 80
        env:
        - name: REDIS
          value: "azure-vote-back"
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: azure-vote-front
```

<span data-ttu-id="f6fdf-140">Use the [kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create) command to run the application.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-140">Use the [kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create) command to run the application.</span></span>

```azurecli-interactive
kubectl create -f azure-vote.yml
```

<span data-ttu-id="f6fdf-141">Output:</span><span class="sxs-lookup"><span data-stu-id="f6fdf-141">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-the-application"></a><span data-ttu-id="f6fdf-142">Test the application</span><span class="sxs-lookup"><span data-stu-id="f6fdf-142">Test the application</span></span>

<span data-ttu-id="f6fdf-143">As the application is run, a [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created that exposes the application front end to the internet.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-143">As the application is run, a [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created that exposes the application front end to the internet.</span></span> <span data-ttu-id="f6fdf-144">This process can take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-144">This process can take a few minutes to complete.</span></span> 

<span data-ttu-id="f6fdf-145">To monitor progress, use the [kubectl get service](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command with the `--watch` argument.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-145">To monitor progress, use the [kubectl get service](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command with the `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="f6fdf-146">Initially the **EXTERNAL-IP** for the *azure-vote-front* service appears as *pending*.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-146">Initially the **EXTERNAL-IP** for the *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="f6fdf-147">Once the EXTERNAL-IP address has changed from *pending* to an *IP address*, use `CTRL-C` to stop the kubectl watch process.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-147">Once the EXTERNAL-IP address has changed from *pending* to an *IP address*, use `CTRL-C` to stop the kubectl watch process.</span></span> 
  
```bash
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

<span data-ttu-id="f6fdf-148">You can now browse to the external IP address to see the Azure Vote App.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-148">You can now browse to the external IP address to see the Azure Vote App.</span></span>

![Image of browsing to Azure Vote](media/container-service-kubernetes-walkthrough/azure-vote.png)  

## <a name="delete-cluster"></a><span data-ttu-id="f6fdf-150">Delete cluster</span><span class="sxs-lookup"><span data-stu-id="f6fdf-150">Delete cluster</span></span>
<span data-ttu-id="f6fdf-151">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, container service, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-151">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-the-code"></a><span data-ttu-id="f6fdf-152">Get the code</span><span class="sxs-lookup"><span data-stu-id="f6fdf-152">Get the code</span></span>

<span data-ttu-id="f6fdf-153">In this quick start, pre-created container images have been used to create a Kubernetes deployment.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-153">In this quick start, pre-created container images have been used to create a Kubernetes deployment.</span></span> <span data-ttu-id="f6fdf-154">The related application code, Dockerfile, and Kubernetes manifest file are available on GitHub.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-154">The related application code, Dockerfile, and Kubernetes manifest file are available on GitHub.</span></span>

[https://github.com/Azure-Samples/azure-voting-app-redis](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="f6fdf-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="f6fdf-155">Next steps</span></span>

<span data-ttu-id="f6fdf-156">In this quick start, you deployed a Kubernetes cluster and deployed a multi-container application to it.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-156">In this quick start, you deployed a Kubernetes cluster and deployed a multi-container application to it.</span></span> 

<span data-ttu-id="f6fdf-157">To learn more about Azure Container Service, and walk through a complete code to deployment example, continue to the Kubernetes cluster tutorial.</span><span class="sxs-lookup"><span data-stu-id="f6fdf-157">To learn more about Azure Container Service, and walk through a complete code to deployment example, continue to the Kubernetes cluster tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f6fdf-158">Manage an ACS Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="f6fdf-158">Manage an ACS Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-prepare-app.md)
