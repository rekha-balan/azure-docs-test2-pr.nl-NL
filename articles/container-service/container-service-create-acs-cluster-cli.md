---
title: Deploy a Docker container cluster - Azure CLI | Microsoft Docs
description: Deploy a Kubernetes, DC/OS, or Docker Swarm solution in Azure Container Service by using Azure CLI 2.0
services: container-service
documentationcenter: ''
author: sauryadas
manager: timlt
editor: ''
tags: acs, azure-container-service
keywords: ''
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: saudas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3d714004d18d576e75a6c780878bb1e15736f829
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672246"
---
# <a name="deploy-a-docker-container-hosting-solution-using-the-azure-cli-20"></a><span data-ttu-id="42f18-103">Deploy a Docker container hosting solution using the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="42f18-103">Deploy a Docker container hosting solution using the Azure CLI 2.0</span></span>

<span data-ttu-id="42f18-104">Use the `az acs` commands in the Azure CLI 2.0 to create and manage clusters in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="42f18-104">Use the `az acs` commands in the Azure CLI 2.0 to create and manage clusters in Azure Container Service.</span></span> <span data-ttu-id="42f18-105">You can also deploy an Azure Container Service cluster by using the [Azure portal](container-service-deployment.md) or the Azure Container Service APIs.</span><span class="sxs-lookup"><span data-stu-id="42f18-105">You can also deploy an Azure Container Service cluster by using the [Azure portal](container-service-deployment.md) or the Azure Container Service APIs.</span></span>

<span data-ttu-id="42f18-106">For help on `az acs` commands, pass the `-h` parameter to any command.</span><span class="sxs-lookup"><span data-stu-id="42f18-106">For help on `az acs` commands, pass the `-h` parameter to any command.</span></span> <span data-ttu-id="42f18-107">For example: `az acs create -h`.</span><span class="sxs-lookup"><span data-stu-id="42f18-107">For example: `az acs create -h`.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="42f18-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="42f18-108">Prerequisites</span></span>
<span data-ttu-id="42f18-109">To create an Azure Container Service cluster using the Azure CLI 2.0, you must:</span><span class="sxs-lookup"><span data-stu-id="42f18-109">To create an Azure Container Service cluster using the Azure CLI 2.0, you must:</span></span>
* <span data-ttu-id="42f18-110">have an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/))</span><span class="sxs-lookup"><span data-stu-id="42f18-110">have an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/))</span></span>
* <span data-ttu-id="42f18-111">have installed and set up the [Azure CLI 2.0](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="42f18-111">have installed and set up the [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

## <a name="get-started"></a><span data-ttu-id="42f18-112">Get started</span><span class="sxs-lookup"><span data-stu-id="42f18-112">Get started</span></span> 
### <a name="log-in-to-your-account"></a><span data-ttu-id="42f18-113">Log in to your account</span><span class="sxs-lookup"><span data-stu-id="42f18-113">Log in to your account</span></span>
```azurecli
az login 
```

<span data-ttu-id="42f18-114">Follow the prompts to log in interactively.</span><span class="sxs-lookup"><span data-stu-id="42f18-114">Follow the prompts to log in interactively.</span></span> <span data-ttu-id="42f18-115">For other methods to log in, see [Get started with Azure CLI 2.0](/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="42f18-115">For other methods to log in, see [Get started with Azure CLI 2.0](/cli/azure/get-started-with-az-cli2).</span></span>

### <a name="set-your-azure-subscription"></a><span data-ttu-id="42f18-116">Set your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="42f18-116">Set your Azure subscription</span></span>

<span data-ttu-id="42f18-117">If you have more than one Azure subscription, set the default subscription.</span><span class="sxs-lookup"><span data-stu-id="42f18-117">If you have more than one Azure subscription, set the default subscription.</span></span> <span data-ttu-id="42f18-118">For example:</span><span class="sxs-lookup"><span data-stu-id="42f18-118">For example:</span></span>

```
az account set --subscription "f66xxxxx-xxxx-xxxx-xxx-zgxxxx33cha5"
```


### <a name="create-a-resource-group"></a><span data-ttu-id="42f18-119">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="42f18-119">Create a resource group</span></span>
<span data-ttu-id="42f18-120">We recommend that you create a resource group for every cluster.</span><span class="sxs-lookup"><span data-stu-id="42f18-120">We recommend that you create a resource group for every cluster.</span></span> <span data-ttu-id="42f18-121">Specify an Azure region in which Azure Container Service is [available](https://azure.microsoft.com/en-us/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="42f18-121">Specify an Azure region in which Azure Container Service is [available](https://azure.microsoft.com/en-us/regions/services/).</span></span> <span data-ttu-id="42f18-122">For example:</span><span class="sxs-lookup"><span data-stu-id="42f18-122">For example:</span></span>

```azurecli
az group create -n acsrg1 -l "westus"
```
<span data-ttu-id="42f18-123">Output is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="42f18-123">Output is similar to the following:</span></span>

![Create a resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-create-acs-cluster-cli/rg-create.png)


## <a name="create-an-azure-container-service-cluster"></a><span data-ttu-id="42f18-125">Create an Azure Container Service cluster</span><span class="sxs-lookup"><span data-stu-id="42f18-125">Create an Azure Container Service cluster</span></span>

<span data-ttu-id="42f18-126">To create a cluster, use `az acs create`.</span><span class="sxs-lookup"><span data-stu-id="42f18-126">To create a cluster, use `az acs create`.</span></span>
<span data-ttu-id="42f18-127">A name for the cluster and the name of the resource group created in the previous step are mandatory parameters.</span><span class="sxs-lookup"><span data-stu-id="42f18-127">A name for the cluster and the name of the resource group created in the previous step are mandatory parameters.</span></span> 

<span data-ttu-id="42f18-128">Other inputs are set to default values (see the following screen) unless overwritten using their respective switches.</span><span class="sxs-lookup"><span data-stu-id="42f18-128">Other inputs are set to default values (see the following screen) unless overwritten using their respective switches.</span></span> <span data-ttu-id="42f18-129">For example, the orchestrator is set by default to DC/OS.</span><span class="sxs-lookup"><span data-stu-id="42f18-129">For example, the orchestrator is set by default to DC/OS.</span></span> <span data-ttu-id="42f18-130">And if you don't specify one, a DNS name prefix is created based on the cluster name.</span><span class="sxs-lookup"><span data-stu-id="42f18-130">And if you don't specify one, a DNS name prefix is created based on the cluster name.</span></span>

![az acs create usage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-create-acs-cluster-cli/create-help.png)


### <a name="quick-acs-create-using-defaults"></a><span data-ttu-id="42f18-132">Quick `acs create` using defaults</span><span class="sxs-lookup"><span data-stu-id="42f18-132">Quick `acs create` using defaults</span></span>
<span data-ttu-id="42f18-133">If you have an SSH RSA public key file `id_rsa.pub` in the default location (or created one for [OS X and Linux](../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../virtual-machines/linux/ssh-from-windows.md)), use a command like the following:</span><span class="sxs-lookup"><span data-stu-id="42f18-133">If you have an SSH RSA public key file `id_rsa.pub` in the default location (or created one for [OS X and Linux](../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../virtual-machines/linux/ssh-from-windows.md)), use a command like the following:</span></span>

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789
```
<span data-ttu-id="42f18-134">If you don't have an SSH public key, use this second command.</span><span class="sxs-lookup"><span data-stu-id="42f18-134">If you don't have an SSH public key, use this second command.</span></span> <span data-ttu-id="42f18-135">This command with the `--generate-ssh-keys` switch creates one for you.</span><span class="sxs-lookup"><span data-stu-id="42f18-135">This command with the `--generate-ssh-keys` switch creates one for you.</span></span>

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789 --generate-ssh-keys
```

<span data-ttu-id="42f18-136">After you enter the command, wait for about 10 minutes for the cluster to be created.</span><span class="sxs-lookup"><span data-stu-id="42f18-136">After you enter the command, wait for about 10 minutes for the cluster to be created.</span></span> <span data-ttu-id="42f18-137">The command output includes fully qualified domain names (FQDNs) of the master and agent nodes and an SSH command to connect to the first master.</span><span class="sxs-lookup"><span data-stu-id="42f18-137">The command output includes fully qualified domain names (FQDNs) of the master and agent nodes and an SSH command to connect to the first master.</span></span> <span data-ttu-id="42f18-138">Here is abbreviated output:</span><span class="sxs-lookup"><span data-stu-id="42f18-138">Here is abbreviated output:</span></span>

![Image ACS create](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-create-acs-cluster-cli/cluster-create.png)

> [!TIP]
> <span data-ttu-id="42f18-140">The [Kubernetes walkthrough](container-service-kubernetes-walkthrough.md) shows how to use `az acs create` with default values to create a Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="42f18-140">The [Kubernetes walkthrough](container-service-kubernetes-walkthrough.md) shows how to use `az acs create` with default values to create a Kubernetes cluster.</span></span>
>

## <a name="manage-acs-clusters"></a><span data-ttu-id="42f18-141">Manage ACS clusters</span><span class="sxs-lookup"><span data-stu-id="42f18-141">Manage ACS clusters</span></span>

<span data-ttu-id="42f18-142">Use additional `az acs` commands to manage your cluster.</span><span class="sxs-lookup"><span data-stu-id="42f18-142">Use additional `az acs` commands to manage your cluster.</span></span> <span data-ttu-id="42f18-143">Here are some examples.</span><span class="sxs-lookup"><span data-stu-id="42f18-143">Here are some examples.</span></span>

### <a name="list-clusters-under-a-subscription"></a><span data-ttu-id="42f18-144">List clusters under a subscription</span><span class="sxs-lookup"><span data-stu-id="42f18-144">List clusters under a subscription</span></span>

```azurecli
az acs list --output table
```

### <a name="list-clusters-in-a-resource-group"></a><span data-ttu-id="42f18-145">List clusters in a resource group</span><span class="sxs-lookup"><span data-stu-id="42f18-145">List clusters in a resource group</span></span>

```azurecli
az acs list -g acsrg1 --output table
```

![acs list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-create-acs-cluster-cli/acs-list.png)


### <a name="display-details-of-a-container-service-cluster"></a><span data-ttu-id="42f18-147">Display details of a container service cluster</span><span class="sxs-lookup"><span data-stu-id="42f18-147">Display details of a container service cluster</span></span>

```azurecli
az acs show -g acsrg1 -n acs-cluster --output list
```

![acs show](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-create-acs-cluster-cli/acs-show.png)


### <a name="scale-the-cluster"></a><span data-ttu-id="42f18-149">Scale the cluster</span><span class="sxs-lookup"><span data-stu-id="42f18-149">Scale the cluster</span></span>
<span data-ttu-id="42f18-150">Both scaling in and scaling out of agent nodes are allowed.</span><span class="sxs-lookup"><span data-stu-id="42f18-150">Both scaling in and scaling out of agent nodes are allowed.</span></span> <span data-ttu-id="42f18-151">The parameter `new-agent-count` is the new number of agents in the ACS cluster.</span><span class="sxs-lookup"><span data-stu-id="42f18-151">The parameter `new-agent-count` is the new number of agents in the ACS cluster.</span></span>

```azurecli
az acs scale -g acsrg1 -n acs-cluster --new-agent-count 4
```

![acs scale](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-create-acs-cluster-cli/acs-scale.png)

## <a name="delete-a-container-service-cluster"></a><span data-ttu-id="42f18-153">Delete a container service cluster</span><span class="sxs-lookup"><span data-stu-id="42f18-153">Delete a container service cluster</span></span>
```azurecli
az acs delete -g acsrg1 -n acs-cluster 
```
<span data-ttu-id="42f18-154">This command does not delete all resources (network and storage) created while creating the container service.</span><span class="sxs-lookup"><span data-stu-id="42f18-154">This command does not delete all resources (network and storage) created while creating the container service.</span></span> <span data-ttu-id="42f18-155">To delete all resources easily, it is recommended you deploy each cluster in a distinct resource group.</span><span class="sxs-lookup"><span data-stu-id="42f18-155">To delete all resources easily, it is recommended you deploy each cluster in a distinct resource group.</span></span> <span data-ttu-id="42f18-156">Then, delete the resource group when the cluster is no longer required.</span><span class="sxs-lookup"><span data-stu-id="42f18-156">Then, delete the resource group when the cluster is no longer required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42f18-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="42f18-157">Next steps</span></span>
<span data-ttu-id="42f18-158">Now that you have a functioning cluster, see these documents for connection and management details:</span><span class="sxs-lookup"><span data-stu-id="42f18-158">Now that you have a functioning cluster, see these documents for connection and management details:</span></span>

* [<span data-ttu-id="42f18-159">Connect to an Azure Container Service cluster</span><span class="sxs-lookup"><span data-stu-id="42f18-159">Connect to an Azure Container Service cluster</span></span>](container-service-connect.md)
* [<span data-ttu-id="42f18-160">Work with Azure Container Service and DC/OS</span><span class="sxs-lookup"><span data-stu-id="42f18-160">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="42f18-161">Work with Azure Container Service and Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="42f18-161">Work with Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)
* [<span data-ttu-id="42f18-162">Work with Azure Container Service and Kubernetes</span><span class="sxs-lookup"><span data-stu-id="42f18-162">Work with Azure Container Service and Kubernetes</span></span>](container-service-kubernetes-walkthrough.md)





