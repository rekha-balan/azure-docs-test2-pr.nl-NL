---
title: Deploy containers with Helm in Azure Kubernetes | Microsoft Docs
description: Use the Helm packaging tool to deploy containers on a Kubernetes cluster in Azure Container Service
services: container-service
documentationcenter: ''
author: sauryadas
manager: madhana
editor: ''
tags: acs, azure-container-service
keywords: ''
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/10/2017
ms.author: saudas
ms.custom: ''
ms.openlocfilehash: 7c74f8ee3fdf1f41da115bde23fa6a2dfe134857
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549478"
---
# <a name="use-helm-to-deploy-containers-on-a-kubernetes-cluster"></a><span data-ttu-id="05cd2-103">Use Helm to deploy containers on a Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="05cd2-103">Use Helm to deploy containers on a Kubernetes cluster</span></span> 

<span data-ttu-id="05cd2-104">[Helm](https://github.com/kubernetes/helm/) is an open-source packaging tool that helps you install and manage the lifecycle of Kubernetes applications.</span><span class="sxs-lookup"><span data-stu-id="05cd2-104">[Helm](https://github.com/kubernetes/helm/) is an open-source packaging tool that helps you install and manage the lifecycle of Kubernetes applications.</span></span> <span data-ttu-id="05cd2-105">Similar to Linux package managers such as Apt-get and Yum, Helm is used to manage Kubernetes charts, which are packages of preconfigured Kubernetes resources.</span><span class="sxs-lookup"><span data-stu-id="05cd2-105">Similar to Linux package managers such as Apt-get and Yum, Helm is used to manage Kubernetes charts, which are packages of preconfigured Kubernetes resources.</span></span> <span data-ttu-id="05cd2-106">This article shows you how to work with Helm on a Kubernetes cluster deployed in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="05cd2-106">This article shows you how to work with Helm on a Kubernetes cluster deployed in Azure Container Service.</span></span>

<span data-ttu-id="05cd2-107">Helm has two components:</span><span class="sxs-lookup"><span data-stu-id="05cd2-107">Helm has two components:</span></span> 
* <span data-ttu-id="05cd2-108">The **Helm CLI** is a client that runs on your machine locally or in the cloud</span><span class="sxs-lookup"><span data-stu-id="05cd2-108">The **Helm CLI** is a client that runs on your machine locally or in the cloud</span></span>  

* <span data-ttu-id="05cd2-109">**Tiller** is a server that runs on the Kubernetes cluster and manages the lifecycle of your Kubernetes applications</span><span class="sxs-lookup"><span data-stu-id="05cd2-109">**Tiller** is a server that runs on the Kubernetes cluster and manages the lifecycle of your Kubernetes applications</span></span> 
 
## <a name="prerequisites"></a><span data-ttu-id="05cd2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="05cd2-110">Prerequisites</span></span>

* <span data-ttu-id="05cd2-111">[Create a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="05cd2-111">[Create a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>

* <span data-ttu-id="05cd2-112">[Install and configure `kubectl`](container-service-connect.md) on a local computer</span><span class="sxs-lookup"><span data-stu-id="05cd2-112">[Install and configure `kubectl`](container-service-connect.md) on a local computer</span></span>

* <span data-ttu-id="05cd2-113">[Install Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) on a local computer</span><span class="sxs-lookup"><span data-stu-id="05cd2-113">[Install Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) on a local computer</span></span>

## <a name="helm-basics"></a><span data-ttu-id="05cd2-114">Helm basics</span><span class="sxs-lookup"><span data-stu-id="05cd2-114">Helm basics</span></span> 

<span data-ttu-id="05cd2-115">To view information about the Kubernetes cluster that you are installing Tiller and deploying your applications to, type the following command:</span><span class="sxs-lookup"><span data-stu-id="05cd2-115">To view information about the Kubernetes cluster that you are installing Tiller and deploying your applications to, type the following command:</span></span>

```bash
kubectl cluster-info 
```
![kubectl cluster-info](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-helm/clusterinfo.png)
 
<span data-ttu-id="05cd2-117">After you have installed Helm, install Tiller on your Kubernetes cluster by typing the following command:</span><span class="sxs-lookup"><span data-stu-id="05cd2-117">After you have installed Helm, install Tiller on your Kubernetes cluster by typing the following command:</span></span>

```bash
helm init --upgrade
```
<span data-ttu-id="05cd2-118">When it completes successfully, you see output like the following:</span><span class="sxs-lookup"><span data-stu-id="05cd2-118">When it completes successfully, you see output like the following:</span></span>

![Tiller installation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
<span data-ttu-id="05cd2-120">To view all the Helm charts available in the repository, type the following command:</span><span class="sxs-lookup"><span data-stu-id="05cd2-120">To view all the Helm charts available in the repository, type the following command:</span></span>

```bash 
helm search 
```

<span data-ttu-id="05cd2-121">You see output like the following:</span><span class="sxs-lookup"><span data-stu-id="05cd2-121">You see output like the following:</span></span>

![Helm search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-helm/helm-search.png)
 
<span data-ttu-id="05cd2-123">To update the charts to get the latest versions, type:</span><span class="sxs-lookup"><span data-stu-id="05cd2-123">To update the charts to get the latest versions, type:</span></span>

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a><span data-ttu-id="05cd2-124">Deploy an Nginx ingress controller chart</span><span class="sxs-lookup"><span data-stu-id="05cd2-124">Deploy an Nginx ingress controller chart</span></span> 
 
<span data-ttu-id="05cd2-125">To deploy an Nginx ingress controller chart, type a single command:</span><span class="sxs-lookup"><span data-stu-id="05cd2-125">To deploy an Nginx ingress controller chart, type a single command:</span></span>

```bash
helm install stable/nginx-ingress 
```
![Deploy ingress controller](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-helm/nginx-ingress.png)

<span data-ttu-id="05cd2-127">If you type `kubectl get svc` to view all services that are running on the cluster, you see that an IP address is assigned to the ingress controller.</span><span class="sxs-lookup"><span data-stu-id="05cd2-127">If you type `kubectl get svc` to view all services that are running on the cluster, you see that an IP address is assigned to the ingress controller.</span></span> <span data-ttu-id="05cd2-128">(While the assignment is in progress, you see `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="05cd2-128">(While the assignment is in progress, you see `<pending>`.</span></span> <span data-ttu-id="05cd2-129">It takes a couple of minutes to complete.)</span><span class="sxs-lookup"><span data-stu-id="05cd2-129">It takes a couple of minutes to complete.)</span></span> 

<span data-ttu-id="05cd2-130">After the IP address is assigned, navigate to the value of the external IP address to see the Nginx backend running.</span><span class="sxs-lookup"><span data-stu-id="05cd2-130">After the IP address is assigned, navigate to the value of the external IP address to see the Nginx backend running.</span></span> 
 
![Ingress IP address](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-helm/ingress-ip-address.png)


<span data-ttu-id="05cd2-132">To see a list of charts installed on your cluster, type:</span><span class="sxs-lookup"><span data-stu-id="05cd2-132">To see a list of charts installed on your cluster, type:</span></span>

```bash
helm list 
```

<span data-ttu-id="05cd2-133">You can abbreviate the command to `helm ls`.</span><span class="sxs-lookup"><span data-stu-id="05cd2-133">You can abbreviate the command to `helm ls`.</span></span>
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a><span data-ttu-id="05cd2-134">Deploy a MariaDB chart and client</span><span class="sxs-lookup"><span data-stu-id="05cd2-134">Deploy a MariaDB chart and client</span></span>

<span data-ttu-id="05cd2-135">Now deploy a MariaDB chart and a MariaDB client to connect to the database.</span><span class="sxs-lookup"><span data-stu-id="05cd2-135">Now deploy a MariaDB chart and a MariaDB client to connect to the database.</span></span>

<span data-ttu-id="05cd2-136">To deploy the MariaDB chart, type the following command:</span><span class="sxs-lookup"><span data-stu-id="05cd2-136">To deploy the MariaDB chart, type the following command:</span></span>

```bash
helm install --name v1 stable/mariadb
```

<span data-ttu-id="05cd2-137">where `--name` is a tag used for releases.</span><span class="sxs-lookup"><span data-stu-id="05cd2-137">where `--name` is a tag used for releases.</span></span>

> [!TIP]
> <span data-ttu-id="05cd2-138">If the deployment fails, run `helm repo update` and try again.</span><span class="sxs-lookup"><span data-stu-id="05cd2-138">If the deployment fails, run `helm repo update` and try again.</span></span>
>
 
 
<span data-ttu-id="05cd2-139">To view all the charts deployed on your cluster, type:</span><span class="sxs-lookup"><span data-stu-id="05cd2-139">To view all the charts deployed on your cluster, type:</span></span>

```bash 
helm list
```
 
<span data-ttu-id="05cd2-140">To view all deployments running on your cluster, type:</span><span class="sxs-lookup"><span data-stu-id="05cd2-140">To view all deployments running on your cluster, type:</span></span>

```bash
kubectl get deployments 
``` 
 
 
<span data-ttu-id="05cd2-141">Finally, to run a pod to access the client, type:</span><span class="sxs-lookup"><span data-stu-id="05cd2-141">Finally, to run a pod to access the client, type:</span></span>

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
<span data-ttu-id="05cd2-142">To connect to the client, type the following command, replacing `v1-mariadb` with the name of your deployment:</span><span class="sxs-lookup"><span data-stu-id="05cd2-142">To connect to the client, type the following command, replacing `v1-mariadb` with the name of your deployment:</span></span>

```bash
sudo mysql –h v1-mariadb
```
 
 
<span data-ttu-id="05cd2-143">You can now use standard SQL commands to create databases, tables, etc. For example, `Create DATABASE testdb1;` creates an empty database.</span><span class="sxs-lookup"><span data-stu-id="05cd2-143">You can now use standard SQL commands to create databases, tables, etc. For example, `Create DATABASE testdb1;` creates an empty database.</span></span> 
 
 
 
## <a name="next-steps"></a><span data-ttu-id="05cd2-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="05cd2-144">Next steps</span></span>

* <span data-ttu-id="05cd2-145">For more information about managing Kubernetes charts, see the [Helm documentation](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span><span class="sxs-lookup"><span data-stu-id="05cd2-145">For more information about managing Kubernetes charts, see the [Helm documentation](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span></span> 






