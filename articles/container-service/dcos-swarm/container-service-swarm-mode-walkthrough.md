---
title: Quickstart - Azure Docker CE cluster for Linux
description: Quickly learn to create a Docker CE cluster for Linux containers in Azure Container Service with the Azure CLI.
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 07/16/2018
ms.author: iainfou
ms.custom: ''
ms.openlocfilehash: 35b8ae347181d272dc899f41f07af36a611aa9f0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966201"
---
# <a name="deploy-docker-ce-cluster"></a><span data-ttu-id="584d2-103">Deploy Docker CE cluster</span><span class="sxs-lookup"><span data-stu-id="584d2-103">Deploy Docker CE cluster</span></span>

<span data-ttu-id="584d2-104">In this quick start, a Docker CE cluster is deployed using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="584d2-104">In this quick start, a Docker CE cluster is deployed using the Azure CLI.</span></span> <span data-ttu-id="584d2-105">A multi-container application consisting of web front-end and a Redis instance is then deployed and run on the cluster.</span><span class="sxs-lookup"><span data-stu-id="584d2-105">A multi-container application consisting of web front-end and a Redis instance is then deployed and run on the cluster.</span></span> <span data-ttu-id="584d2-106">Once completed, the application is accessible over the internet.</span><span class="sxs-lookup"><span data-stu-id="584d2-106">Once completed, the application is accessible over the internet.</span></span>

<span data-ttu-id="584d2-107">Docker CE on Azure Container Service is in preview and **should not be used for production workloads**.</span><span class="sxs-lookup"><span data-stu-id="584d2-107">Docker CE on Azure Container Service is in preview and **should not be used for production workloads**.</span></span>

<span data-ttu-id="584d2-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="584d2-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="584d2-109">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="584d2-109">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="584d2-110">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="584d2-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="584d2-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="584d2-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="584d2-112">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="584d2-112">Create a resource group</span></span>

<span data-ttu-id="584d2-113">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span><span class="sxs-lookup"><span data-stu-id="584d2-113">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span></span> <span data-ttu-id="584d2-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="584d2-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="584d2-115">The following example creates a resource group named *myResourceGroup* in the *westus2* location.</span><span class="sxs-lookup"><span data-stu-id="584d2-115">The following example creates a resource group named *myResourceGroup* in the *westus2* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus2
```

<span data-ttu-id="584d2-116">Output:</span><span class="sxs-lookup"><span data-stu-id="584d2-116">Output:</span></span>

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westus2",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="584d2-117">Create Docker Swarm cluster</span><span class="sxs-lookup"><span data-stu-id="584d2-117">Create Docker Swarm cluster</span></span>

<span data-ttu-id="584d2-118">Create a Docker CE cluster in Azure Container Service with the [az acs create](/cli/azure/acs#az-acs-create) command.</span><span class="sxs-lookup"><span data-stu-id="584d2-118">Create a Docker CE cluster in Azure Container Service with the [az acs create](/cli/azure/acs#az-acs-create) command.</span></span> <span data-ttu-id="584d2-119">For information on region availaiblity of Docker CE, see [ACS regions for Docker CE](https://github.com/Azure/ACS/blob/master/announcements/2017-08-04_additional_regions.md)</span><span class="sxs-lookup"><span data-stu-id="584d2-119">For information on region availaiblity of Docker CE, see [ACS regions for Docker CE](https://github.com/Azure/ACS/blob/master/announcements/2017-08-04_additional_regions.md)</span></span>

<span data-ttu-id="584d2-120">The following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span><span class="sxs-lookup"><span data-stu-id="584d2-120">The following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="584d2-121">In some cases, such as with a limited trial, an Azure subscription has limited access to Azure resources.</span><span class="sxs-lookup"><span data-stu-id="584d2-121">In some cases, such as with a limited trial, an Azure subscription has limited access to Azure resources.</span></span> <span data-ttu-id="584d2-122">If the deployment fails due to limited available cores, reduce the default agent count by adding `--agent-count 1` to the [az acs create](/cli/azure/acs#az-acs-create) command.</span><span class="sxs-lookup"><span data-stu-id="584d2-122">If the deployment fails due to limited available cores, reduce the default agent count by adding `--agent-count 1` to the [az acs create](/cli/azure/acs#az-acs-create) command.</span></span> 

<span data-ttu-id="584d2-123">After several minutes, the command completes and returns JSON-formatted information about the cluster.</span><span class="sxs-lookup"><span data-stu-id="584d2-123">After several minutes, the command completes and returns JSON-formatted information about the cluster.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="584d2-124">Connect to the cluster</span><span class="sxs-lookup"><span data-stu-id="584d2-124">Connect to the cluster</span></span>

<span data-ttu-id="584d2-125">Throughout this quick start, you need the FQDN of both the Docker Swarm master and the Docker agent pool.</span><span class="sxs-lookup"><span data-stu-id="584d2-125">Throughout this quick start, you need the FQDN of both the Docker Swarm master and the Docker agent pool.</span></span> <span data-ttu-id="584d2-126">Run the following command to return both the master and agent FQDNs.</span><span class="sxs-lookup"><span data-stu-id="584d2-126">Run the following command to return both the master and agent FQDNs.</span></span>


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

<span data-ttu-id="584d2-127">Output:</span><span class="sxs-lookup"><span data-stu-id="584d2-127">Output:</span></span>

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

<span data-ttu-id="584d2-128">Create an SSH tunnel to the Swarm master.</span><span class="sxs-lookup"><span data-stu-id="584d2-128">Create an SSH tunnel to the Swarm master.</span></span> <span data-ttu-id="584d2-129">Replace `MasterFQDN` with the FQDN address of the Swarm master.</span><span class="sxs-lookup"><span data-stu-id="584d2-129">Replace `MasterFQDN` with the FQDN address of the Swarm master.</span></span>

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

<span data-ttu-id="584d2-130">Set the `DOCKER_HOST` environment variable.</span><span class="sxs-lookup"><span data-stu-id="584d2-130">Set the `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="584d2-131">This allows you to run docker commands against the Docker Swarm without having to specify the name of the host.</span><span class="sxs-lookup"><span data-stu-id="584d2-131">This allows you to run docker commands against the Docker Swarm without having to specify the name of the host.</span></span>

```bash
export DOCKER_HOST=localhost:2374
```

<span data-ttu-id="584d2-132">You are now ready to run Docker services on the Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="584d2-132">You are now ready to run Docker services on the Docker Swarm.</span></span>


## <a name="run-the-application"></a><span data-ttu-id="584d2-133">Run the application</span><span class="sxs-lookup"><span data-stu-id="584d2-133">Run the application</span></span>

<span data-ttu-id="584d2-134">Create a file named `azure-vote.yaml` and copy the following content into it.</span><span class="sxs-lookup"><span data-stu-id="584d2-134">Create a file named `azure-vote.yaml` and copy the following content into it.</span></span>


```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:v1
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

<span data-ttu-id="584d2-135">Run the [docker stack deploy](https://docs.docker.com/engine/reference/commandline/stack_deploy/) command to create the Azure Vote service.</span><span class="sxs-lookup"><span data-stu-id="584d2-135">Run the [docker stack deploy](https://docs.docker.com/engine/reference/commandline/stack_deploy/) command to create the Azure Vote service.</span></span>

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

<span data-ttu-id="584d2-136">Output:</span><span class="sxs-lookup"><span data-stu-id="584d2-136">Output:</span></span>

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

<span data-ttu-id="584d2-137">Use the [docker stack ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) command to return the deployment status of the application.</span><span class="sxs-lookup"><span data-stu-id="584d2-137">Use the [docker stack ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) command to return the deployment status of the application.</span></span>

```bash
docker stack ps azure-vote
```

<span data-ttu-id="584d2-138">Once the `CURRENT STATE` of each service is `Running`, the application is ready.</span><span class="sxs-lookup"><span data-stu-id="584d2-138">Once the `CURRENT STATE` of each service is `Running`, the application is ready.</span></span>

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-the-application"></a><span data-ttu-id="584d2-139">Test the application</span><span class="sxs-lookup"><span data-stu-id="584d2-139">Test the application</span></span>

<span data-ttu-id="584d2-140">Browse to the FQDN of the Swarm agent pool to test out the Azure Vote application.</span><span class="sxs-lookup"><span data-stu-id="584d2-140">Browse to the FQDN of the Swarm agent pool to test out the Azure Vote application.</span></span>

![Image of browsing to Azure Vote](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="584d2-142">Delete cluster</span><span class="sxs-lookup"><span data-stu-id="584d2-142">Delete cluster</span></span>
<span data-ttu-id="584d2-143">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, container service, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="584d2-143">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-the-code"></a><span data-ttu-id="584d2-144">Get the code</span><span class="sxs-lookup"><span data-stu-id="584d2-144">Get the code</span></span>

<span data-ttu-id="584d2-145">In this quick start, pre-created container images have been used to create a Docker service.</span><span class="sxs-lookup"><span data-stu-id="584d2-145">In this quick start, pre-created container images have been used to create a Docker service.</span></span> <span data-ttu-id="584d2-146">The related application code, Dockerfile, and Compose file are available on GitHub.</span><span class="sxs-lookup"><span data-stu-id="584d2-146">The related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[https://github.com/Azure-Samples/azure-voting-app-redis](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="584d2-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="584d2-147">Next steps</span></span>

<span data-ttu-id="584d2-148">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application to it.</span><span class="sxs-lookup"><span data-stu-id="584d2-148">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application to it.</span></span>

<span data-ttu-id="584d2-149">To learn about integrating Docker swarm with Azure DevOps, continue to the CI/CD with Docker Swarm and Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="584d2-149">To learn about integrating Docker swarm with Azure DevOps, continue to the CI/CD with Docker Swarm and Azure DevOps.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="584d2-150">CI/CD with Docker Swarm and Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="584d2-150">CI/CD with Docker Swarm and Azure DevOps</span></span>](./container-service-docker-swarm-setup-ci-cd.md)
