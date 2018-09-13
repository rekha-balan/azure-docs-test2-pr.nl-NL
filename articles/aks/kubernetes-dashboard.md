---
title: Manage Azure Kubernetes cluster with web UI
description: Learn how to use the built-in Kubernetes web UI dashboard with Azure Kubernetes Service (AKS)
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 07/09/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: af48af596e86e0eb09fe45deabe13beedef57cd2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865310"
---
# <a name="access-the-kubernetes-dashboard-with-azure-kubernetes-service-aks"></a><span data-ttu-id="1a041-103">Access the Kubernetes dashboard with Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="1a041-103">Access the Kubernetes dashboard with Azure Kubernetes Service (AKS)</span></span>

<span data-ttu-id="1a041-104">Kubernetes includes a web dashboard that can be used for basic management operations.</span><span class="sxs-lookup"><span data-stu-id="1a041-104">Kubernetes includes a web dashboard that can be used for basic management operations.</span></span> <span data-ttu-id="1a041-105">This article shows you how to access the Kubernetes dashboard using the Azure CLI, then guides you through some basic dashboard operations.</span><span class="sxs-lookup"><span data-stu-id="1a041-105">This article shows you how to access the Kubernetes dashboard using the Azure CLI, then guides you through some basic dashboard operations.</span></span> <span data-ttu-id="1a041-106">For more information on the Kubernetes dashboard, see [Kubernetes Web UI Dashboard][kubernetes-dashboard].</span><span class="sxs-lookup"><span data-stu-id="1a041-106">For more information on the Kubernetes dashboard, see [Kubernetes Web UI Dashboard][kubernetes-dashboard].</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1a041-107">Before you begin</span><span class="sxs-lookup"><span data-stu-id="1a041-107">Before you begin</span></span>

<span data-ttu-id="1a041-108">The steps detailed in this document assume that you have created an AKS cluster and have established a `kubectl` connection with the cluster.</span><span class="sxs-lookup"><span data-stu-id="1a041-108">The steps detailed in this document assume that you have created an AKS cluster and have established a `kubectl` connection with the cluster.</span></span> <span data-ttu-id="1a041-109">If you need to create an AKS cluster, see the [AKS quickstart][aks-quickstart].</span><span class="sxs-lookup"><span data-stu-id="1a041-109">If you need to create an AKS cluster, see the [AKS quickstart][aks-quickstart].</span></span>

<span data-ttu-id="1a041-110">You also need the Azure CLI version 2.0.27 or later installed and configured.</span><span class="sxs-lookup"><span data-stu-id="1a041-110">You also need the Azure CLI version 2.0.27 or later installed and configured.</span></span> <span data-ttu-id="1a041-111">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="1a041-111">Run `az --version` to find the version.</span></span> <span data-ttu-id="1a041-112">If you need to install or upgrade, see [Install Azure CLI][install-azure-cli].</span><span class="sxs-lookup"><span data-stu-id="1a041-112">If you need to install or upgrade, see [Install Azure CLI][install-azure-cli].</span></span>

## <a name="start-kubernetes-dashboard"></a><span data-ttu-id="1a041-113">Start Kubernetes dashboard</span><span class="sxs-lookup"><span data-stu-id="1a041-113">Start Kubernetes dashboard</span></span>

<span data-ttu-id="1a041-114">To start the Kubernetes dashboard, use the [az aks browse][az-aks-browse] command.</span><span class="sxs-lookup"><span data-stu-id="1a041-114">To start the Kubernetes dashboard, use the [az aks browse][az-aks-browse] command.</span></span> <span data-ttu-id="1a041-115">The following example opens the dashboard for the cluster named *myAKSCluster* in the resource group named *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="1a041-115">The following example opens the dashboard for the cluster named *myAKSCluster* in the resource group named *myResourceGroup*:</span></span>

```azurecli
az aks browse --resource-group myResourceGroup --name myAKSCluster
```

<span data-ttu-id="1a041-116">This command creates a proxy between your development system and the Kubernetes API, and opens a web browser to the Kubernetes dashboard.</span><span class="sxs-lookup"><span data-stu-id="1a041-116">This command creates a proxy between your development system and the Kubernetes API, and opens a web browser to the Kubernetes dashboard.</span></span>

### <a name="for-rbac-enabled-clusters"></a><span data-ttu-id="1a041-117">For RBAC-enabled clusters</span><span class="sxs-lookup"><span data-stu-id="1a041-117">For RBAC-enabled clusters</span></span>

<span data-ttu-id="1a041-118">If your AKS cluster uses RBAC, a *ClusterRoleBinding* must be created before you can correctly access the dashboard.</span><span class="sxs-lookup"><span data-stu-id="1a041-118">If your AKS cluster uses RBAC, a *ClusterRoleBinding* must be created before you can correctly access the dashboard.</span></span> <span data-ttu-id="1a041-119">By default, the Kubernetes dashboard is deployed with minimal read access and displays RBAC access errors.</span><span class="sxs-lookup"><span data-stu-id="1a041-119">By default, the Kubernetes dashboard is deployed with minimal read access and displays RBAC access errors.</span></span> <span data-ttu-id="1a041-120">The Kubernetes dashboard does not currently support user-provided credentials to determine the level of access, rather it uses the roles granted to the service account.</span><span class="sxs-lookup"><span data-stu-id="1a041-120">The Kubernetes dashboard does not currently support user-provided credentials to determine the level of access, rather it uses the roles granted to the service account.</span></span> <span data-ttu-id="1a041-121">A cluster administrator can choose to grant additional access to the *kubernetes-dashboard* service account, however this can be a vector for privilege escalation.</span><span class="sxs-lookup"><span data-stu-id="1a041-121">A cluster administrator can choose to grant additional access to the *kubernetes-dashboard* service account, however this can be a vector for privilege escalation.</span></span> <span data-ttu-id="1a041-122">You can also integrate Azure Active Directory authentication to provide a more granular level of access.</span><span class="sxs-lookup"><span data-stu-id="1a041-122">You can also integrate Azure Active Directory authentication to provide a more granular level of access.</span></span>

<span data-ttu-id="1a041-123">To create a binding, use the [kubectl create clusterrolebinding][kubectl-create-clusterrolebinding] command as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="1a041-123">To create a binding, use the [kubectl create clusterrolebinding][kubectl-create-clusterrolebinding] command as shown in the following example.</span></span> 

> [!WARNING]
> <span data-ttu-id="1a041-124">This sample binding does not apply any additional authentication components and may lead to insecure use.</span><span class="sxs-lookup"><span data-stu-id="1a041-124">This sample binding does not apply any additional authentication components and may lead to insecure use.</span></span> <span data-ttu-id="1a041-125">The Kubernetes dashboard is open to anyone with access to the URL.</span><span class="sxs-lookup"><span data-stu-id="1a041-125">The Kubernetes dashboard is open to anyone with access to the URL.</span></span> <span data-ttu-id="1a041-126">Do not expose the Kubernetes dashboard publicly.</span><span class="sxs-lookup"><span data-stu-id="1a041-126">Do not expose the Kubernetes dashboard publicly.</span></span>
>
> <span data-ttu-id="1a041-127">For more information on using the different authentication methods, see the Kubernetes dashboard wiki on [access controls][dashboard-authentication].</span><span class="sxs-lookup"><span data-stu-id="1a041-127">For more information on using the different authentication methods, see the Kubernetes dashboard wiki on [access controls][dashboard-authentication].</span></span>

```console
kubectl create clusterrolebinding kubernetes-dashboard --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

<span data-ttu-id="1a041-128">You can now access the Kubernetes dashboard in your RBAC-enabled cluster.</span><span class="sxs-lookup"><span data-stu-id="1a041-128">You can now access the Kubernetes dashboard in your RBAC-enabled cluster.</span></span> <span data-ttu-id="1a041-129">To start the Kubernetes dashboard, use the [az aks browse][az-aks-browse] command as detailed in the previous step.</span><span class="sxs-lookup"><span data-stu-id="1a041-129">To start the Kubernetes dashboard, use the [az aks browse][az-aks-browse] command as detailed in the previous step.</span></span>

## <a name="run-an-application"></a><span data-ttu-id="1a041-130">Run an application</span><span class="sxs-lookup"><span data-stu-id="1a041-130">Run an application</span></span>

<span data-ttu-id="1a041-131">In the Kubernetes dashboard, click the **Create** button in the upper right window.</span><span class="sxs-lookup"><span data-stu-id="1a041-131">In the Kubernetes dashboard, click the **Create** button in the upper right window.</span></span> <span data-ttu-id="1a041-132">Give the deployment the name `nginx` and enter `nginx:latest` for the container image name.</span><span class="sxs-lookup"><span data-stu-id="1a041-132">Give the deployment the name `nginx` and enter `nginx:latest` for the container image name.</span></span> <span data-ttu-id="1a041-133">Under **Service**, select **External** and enter `80` for both the port and target port.</span><span class="sxs-lookup"><span data-stu-id="1a041-133">Under **Service**, select **External** and enter `80` for both the port and target port.</span></span>

<span data-ttu-id="1a041-134">When ready, click **Deploy** to create the deployment.</span><span class="sxs-lookup"><span data-stu-id="1a041-134">When ready, click **Deploy** to create the deployment.</span></span>

![Kubernetes Service Create Dialog](./media/container-service-kubernetes-ui/create-deployment.png)

## <a name="view-the-application"></a><span data-ttu-id="1a041-136">View the application</span><span class="sxs-lookup"><span data-stu-id="1a041-136">View the application</span></span>

<span data-ttu-id="1a041-137">Status about the application can be seen on the Kubernetes dashboard.</span><span class="sxs-lookup"><span data-stu-id="1a041-137">Status about the application can be seen on the Kubernetes dashboard.</span></span> <span data-ttu-id="1a041-138">Once the application is running, each component has a green checkbox next to it.</span><span class="sxs-lookup"><span data-stu-id="1a041-138">Once the application is running, each component has a green checkbox next to it.</span></span>

![Kubernetes Pods](./media/container-service-kubernetes-ui/complete-deployment.png)

<span data-ttu-id="1a041-140">To see more information about the application pods, click on **Pods** in the left-hand menu, and then select the **NGINX** pod.</span><span class="sxs-lookup"><span data-stu-id="1a041-140">To see more information about the application pods, click on **Pods** in the left-hand menu, and then select the **NGINX** pod.</span></span> <span data-ttu-id="1a041-141">Here you can see pod-specific information such as resource consumption.</span><span class="sxs-lookup"><span data-stu-id="1a041-141">Here you can see pod-specific information such as resource consumption.</span></span>

![Kubernetes Resources](./media/container-service-kubernetes-ui/running-pods.png)

<span data-ttu-id="1a041-143">To find the IP address of the application, click on **Services** in the left-hand menu, and then select the **NGINX** service.</span><span class="sxs-lookup"><span data-stu-id="1a041-143">To find the IP address of the application, click on **Services** in the left-hand menu, and then select the **NGINX** service.</span></span>

![nginx view](./media/container-service-kubernetes-ui/nginx-service.png)

## <a name="edit-the-application"></a><span data-ttu-id="1a041-145">Edit the application</span><span class="sxs-lookup"><span data-stu-id="1a041-145">Edit the application</span></span>

<span data-ttu-id="1a041-146">In addition to creating and viewing applications, the Kubernetes dashboard can be used to edit and update application deployments.</span><span class="sxs-lookup"><span data-stu-id="1a041-146">In addition to creating and viewing applications, the Kubernetes dashboard can be used to edit and update application deployments.</span></span>

<span data-ttu-id="1a041-147">To edit a deployment, click **Deployments** in the left-hand menu, and then select the **NGINX** deployment.</span><span class="sxs-lookup"><span data-stu-id="1a041-147">To edit a deployment, click **Deployments** in the left-hand menu, and then select the **NGINX** deployment.</span></span> <span data-ttu-id="1a041-148">Finally, select **Edit** in the upper right-hand navigation bar.</span><span class="sxs-lookup"><span data-stu-id="1a041-148">Finally, select **Edit** in the upper right-hand navigation bar.</span></span>

![Kubernetes Edit](./media/container-service-kubernetes-ui/view-deployment.png)

<span data-ttu-id="1a041-150">Locate the `spec.replica` value, which should be 1, change this value to 3.</span><span class="sxs-lookup"><span data-stu-id="1a041-150">Locate the `spec.replica` value, which should be 1, change this value to 3.</span></span> <span data-ttu-id="1a041-151">In doing so, the replica count of the NGINX deployment is increased from 1 to 3.</span><span class="sxs-lookup"><span data-stu-id="1a041-151">In doing so, the replica count of the NGINX deployment is increased from 1 to 3.</span></span>

<span data-ttu-id="1a041-152">Select **Update** when ready.</span><span class="sxs-lookup"><span data-stu-id="1a041-152">Select **Update** when ready.</span></span>

![Kubernetes Edit](./media/container-service-kubernetes-ui/edit-deployment.png)

## <a name="next-steps"></a><span data-ttu-id="1a041-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="1a041-154">Next steps</span></span>

<span data-ttu-id="1a041-155">For more information about the Kubernetes dashboard, see the Kubernetes documentation.</span><span class="sxs-lookup"><span data-stu-id="1a041-155">For more information about the Kubernetes dashboard, see the Kubernetes documentation.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="1a041-156">[Kubernetes Web UI Dashboard][kubernetes-dashboard]</span><span class="sxs-lookup"><span data-stu-id="1a041-156">[Kubernetes Web UI Dashboard][kubernetes-dashboard]</span></span>

<!-- LINKS - external -->
[kubernetes-dashboard]: https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/
[dashboard-authentication]: https://github.com/kubernetes/dashboard/wiki/Access-control
[kubectl-create-clusterrolebinding]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-em-clusterrolebinding-em-
[kubectl-apply]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply

<!-- LINKS - internal -->
[aks-quickstart]: ./kubernetes-walkthrough.md
[install-azure-cli]: /cli/azure/install-azure-cli
[az-aks-browse]: /cli/azure/aks#az-aks-browse
