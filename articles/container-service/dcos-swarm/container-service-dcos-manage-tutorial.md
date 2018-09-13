---
title: Azure Container Service tutorial - Manage DC/OS
description: Azure Container Service tutorial - Manage DC/OS
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: tutorial
ms.date: 02/26/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 7ae235ea52c5c505e535cc3fad2306167d349ee9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967261"
---
# <a name="azure-container-service-tutorial---manage-dcos"></a><span data-ttu-id="2fe7b-103">Azure Container Service tutorial - Manage DC/OS</span><span class="sxs-lookup"><span data-stu-id="2fe7b-103">Azure Container Service tutorial - Manage DC/OS</span></span>

<span data-ttu-id="2fe7b-104">DC/OS provides a distributed platform for running modern and containerized applications.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-104">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="2fe7b-105">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-105">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="2fe7b-106">This quick start details basic steps needed to deploy a DC/OS cluster and run basic workload.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-106">This quick start details basic steps needed to deploy a DC/OS cluster and run basic workload.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2fe7b-107">Create an ACS DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="2fe7b-107">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="2fe7b-108">Connect to the cluster</span><span class="sxs-lookup"><span data-stu-id="2fe7b-108">Connect to the cluster</span></span>
> * <span data-ttu-id="2fe7b-109">Install the DC/OS CLI</span><span class="sxs-lookup"><span data-stu-id="2fe7b-109">Install the DC/OS CLI</span></span>
> * <span data-ttu-id="2fe7b-110">Deploy an application to the cluster</span><span class="sxs-lookup"><span data-stu-id="2fe7b-110">Deploy an application to the cluster</span></span>
> * <span data-ttu-id="2fe7b-111">Scale an application on the cluster</span><span class="sxs-lookup"><span data-stu-id="2fe7b-111">Scale an application on the cluster</span></span>
> * <span data-ttu-id="2fe7b-112">Scale the DC/OS cluster nodes</span><span class="sxs-lookup"><span data-stu-id="2fe7b-112">Scale the DC/OS cluster nodes</span></span>
> * <span data-ttu-id="2fe7b-113">Basic DC/OS management</span><span class="sxs-lookup"><span data-stu-id="2fe7b-113">Basic DC/OS management</span></span>
> * <span data-ttu-id="2fe7b-114">Delete the DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="2fe7b-114">Delete the DC/OS cluster</span></span>

<span data-ttu-id="2fe7b-115">This tutorial requires the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-115">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="2fe7b-116">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-116">Run `az --version` to find the version.</span></span> <span data-ttu-id="2fe7b-117">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2fe7b-117">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-dcos-cluster"></a><span data-ttu-id="2fe7b-118">Create DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="2fe7b-118">Create DC/OS cluster</span></span>

<span data-ttu-id="2fe7b-119">First, create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-119">First, create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span></span> <span data-ttu-id="2fe7b-120">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-120">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="2fe7b-121">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-121">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="2fe7b-122">Next, create a DC/OS cluster with the [az acs create](/cli/azure/acs#az-acs-create) command.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-122">Next, create a DC/OS cluster with the [az acs create](/cli/azure/acs#az-acs-create) command.</span></span>

<span data-ttu-id="2fe7b-123">The following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-123">The following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="2fe7b-124">To use a specific set of keys, use the `--ssh-key-value` option.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-124">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="2fe7b-125">After several minutes, the command completes, and returns information about the deployment.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-125">After several minutes, the command completes, and returns information about the deployment.</span></span>

## <a name="connect-to-dcos-cluster"></a><span data-ttu-id="2fe7b-126">Connect to DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="2fe7b-126">Connect to DC/OS cluster</span></span>

<span data-ttu-id="2fe7b-127">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-127">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="2fe7b-128">Run the following command to return the public IP address of the DC/OS master.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-128">Run the following command to return the public IP address of the DC/OS master.</span></span> <span data-ttu-id="2fe7b-129">This IP address is stored in a variable and used in the next step.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-129">This IP address is stored in a variable and used in the next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="2fe7b-130">To create the SSH tunnel, run the following command and follow the on-screen instructions.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-130">To create the SSH tunnel, run the following command and follow the on-screen instructions.</span></span> <span data-ttu-id="2fe7b-131">If port 80 is already in use, the command fails.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-131">If port 80 is already in use, the command fails.</span></span> <span data-ttu-id="2fe7b-132">Update the tunneled port to one not in use, such as `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-132">Update the tunneled port to one not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a><span data-ttu-id="2fe7b-133">Install DC/OS CLI</span><span class="sxs-lookup"><span data-stu-id="2fe7b-133">Install DC/OS CLI</span></span>

<span data-ttu-id="2fe7b-134">Install the DC/OS cli using the [az acs dcos install-cli](/cli/azure/acs/dcos#az-acs-dcos-install-cli) command.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-134">Install the DC/OS cli using the [az acs dcos install-cli](/cli/azure/acs/dcos#az-acs-dcos-install-cli) command.</span></span> <span data-ttu-id="2fe7b-135">If you are using Azure CloudShell, the DC/OS CLI is already installed.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-135">If you are using Azure CloudShell, the DC/OS CLI is already installed.</span></span> <span data-ttu-id="2fe7b-136">If you are running the Azure CLI on macOS or Linux, you might need to run the command with sudo.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-136">If you are running the Azure CLI on macOS or Linux, you might need to run the command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="2fe7b-137">Before the CLI can be used with the cluster, it must be configured to use the SSH tunnel.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-137">Before the CLI can be used with the cluster, it must be configured to use the SSH tunnel.</span></span> <span data-ttu-id="2fe7b-138">To do so, run the following command, adjusting the port if needed.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-138">To do so, run the following command, adjusting the port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="2fe7b-139">Run an application</span><span class="sxs-lookup"><span data-stu-id="2fe7b-139">Run an application</span></span>

<span data-ttu-id="2fe7b-140">The default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-140">The default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="2fe7b-141">Marathon is used to start an application and manage the state of the application on the DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-141">Marathon is used to start an application and manage the state of the application on the DC/OS cluster.</span></span> <span data-ttu-id="2fe7b-142">To schedule an application through Marathon, create a file named **marathon-app.json**, and copy the following contents into it.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-142">To schedule an application through Marathon, create a file named **marathon-app.json**, and copy the following contents into it.</span></span> 

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

<span data-ttu-id="2fe7b-143">Run the following command to schedule the application to run on the DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-143">Run the following command to schedule the application to run on the DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="2fe7b-144">To see the deployment status for the app, run the following command.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-144">To see the deployment status for the app, run the following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="2fe7b-145">When the **TASKS** column value switches from *0/1* to *1/1*, application deployment has completed.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-145">When the **TASKS** column value switches from *0/1* to *1/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a><span data-ttu-id="2fe7b-146">Scale Marathon application</span><span class="sxs-lookup"><span data-stu-id="2fe7b-146">Scale Marathon application</span></span>

<span data-ttu-id="2fe7b-147">In the previous example, a single instance application was created.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-147">In the previous example, a single instance application was created.</span></span> <span data-ttu-id="2fe7b-148">To update this deployment so that three instances of the application are available, open up the **marathon-app.json** file, and update the instance property to 3.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-148">To update this deployment so that three instances of the application are available, open up the **marathon-app.json** file, and update the instance property to 3.</span></span>

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 3,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

<span data-ttu-id="2fe7b-149">Update the application using the `dcos marathon app update` command.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-149">Update the application using the `dcos marathon app update` command.</span></span>

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

<span data-ttu-id="2fe7b-150">To see the deployment status for the app, run the following command.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-150">To see the deployment status for the app, run the following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="2fe7b-151">When the **TASKS** column value switches from *1/3* to *3/1*, application deployment has completed.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-151">When the **TASKS** column value switches from *1/3* to *3/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a><span data-ttu-id="2fe7b-152">Run internet accessible app</span><span class="sxs-lookup"><span data-stu-id="2fe7b-152">Run internet accessible app</span></span>

<span data-ttu-id="2fe7b-153">The ACS DC/OS cluster consists of two node sets, one public which is accessible on the internet, and one private which is not accessible on the internet.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-153">The ACS DC/OS cluster consists of two node sets, one public which is accessible on the internet, and one private which is not accessible on the internet.</span></span> <span data-ttu-id="2fe7b-154">The default set is the private nodes, which was used in the last example.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-154">The default set is the private nodes, which was used in the last example.</span></span>

<span data-ttu-id="2fe7b-155">To make an application accessible on the internet, deploy them to the public node set.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-155">To make an application accessible on the internet, deploy them to the public node set.</span></span> <span data-ttu-id="2fe7b-156">To do so, give the `acceptedResourceRoles` object a value of `slave_public`.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-156">To do so, give the `acceptedResourceRoles` object a value of `slave_public`.</span></span>

<span data-ttu-id="2fe7b-157">Create a file named **nginx-public.json** and copy the following contents into it.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-157">Create a file named **nginx-public.json** and copy the following contents into it.</span></span>

```json
{
  "id": "demo-app",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  },
  "acceptedResourceRoles": [
    "slave_public"
  ]
}
```

<span data-ttu-id="2fe7b-158">Run the following command to schedule the application to run on the DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-158">Run the following command to schedule the application to run on the DC/OS cluster.</span></span>

```azurecli 
dcos marathon app add nginx-public.json
```

<span data-ttu-id="2fe7b-159">Get the public IP address of the DC/OS public cluster agents.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-159">Get the public IP address of the DC/OS public cluster agents.</span></span>

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="2fe7b-160">Browsing to this address returns the default NGINX site.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-160">Browsing to this address returns the default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a><span data-ttu-id="2fe7b-162">Scale DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="2fe7b-162">Scale DC/OS cluster</span></span>

<span data-ttu-id="2fe7b-163">In the previous examples, an application was scaled to multiple instance.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-163">In the previous examples, an application was scaled to multiple instance.</span></span> <span data-ttu-id="2fe7b-164">The DC/OS infrastructure can also be scaled to provide more or less compute capacity.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-164">The DC/OS infrastructure can also be scaled to provide more or less compute capacity.</span></span> <span data-ttu-id="2fe7b-165">This is done with the [az acs scale](/cli/azure/acs#az-acs-scale) command.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-165">This is done with the [az acs scale](/cli/azure/acs#az-acs-scale) command.</span></span> 

<span data-ttu-id="2fe7b-166">To see the current count of DC/OS agents, use the [az acs show](/cli/azure/acs#az-acs-show) command.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-166">To see the current count of DC/OS agents, use the [az acs show](/cli/azure/acs#az-acs-show) command.</span></span>

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

<span data-ttu-id="2fe7b-167">To increase the count to 5, use the [az acs scale](/cli/azure/acs#az-acs-scale) command.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-167">To increase the count to 5, use the [az acs scale](/cli/azure/acs#az-acs-scale) command.</span></span> 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a><span data-ttu-id="2fe7b-168">Delete DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="2fe7b-168">Delete DC/OS cluster</span></span>

<span data-ttu-id="2fe7b-169">When no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, DC/OS cluster, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-169">When no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="2fe7b-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="2fe7b-170">Next steps</span></span>

<span data-ttu-id="2fe7b-171">In this tutorial, you have learned about basic DC/OS management task including the following.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-171">In this tutorial, you have learned about basic DC/OS management task including the following.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="2fe7b-172">Create an ACS DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="2fe7b-172">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="2fe7b-173">Connect to the cluster</span><span class="sxs-lookup"><span data-stu-id="2fe7b-173">Connect to the cluster</span></span>
> * <span data-ttu-id="2fe7b-174">Install the DC/OS CLI</span><span class="sxs-lookup"><span data-stu-id="2fe7b-174">Install the DC/OS CLI</span></span>
> * <span data-ttu-id="2fe7b-175">Deploy an application to the cluster</span><span class="sxs-lookup"><span data-stu-id="2fe7b-175">Deploy an application to the cluster</span></span>
> * <span data-ttu-id="2fe7b-176">Scale an application on the cluster</span><span class="sxs-lookup"><span data-stu-id="2fe7b-176">Scale an application on the cluster</span></span>
> * <span data-ttu-id="2fe7b-177">Scale the DC/OS cluster nodes</span><span class="sxs-lookup"><span data-stu-id="2fe7b-177">Scale the DC/OS cluster nodes</span></span>
> * <span data-ttu-id="2fe7b-178">Delete the DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="2fe7b-178">Delete the DC/OS cluster</span></span>

<span data-ttu-id="2fe7b-179">Advance to the next tutorial to learn about load balancing application in DC/OS on Azure.</span><span class="sxs-lookup"><span data-stu-id="2fe7b-179">Advance to the next tutorial to learn about load balancing application in DC/OS on Azure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="2fe7b-180">Load balance applications</span><span class="sxs-lookup"><span data-stu-id="2fe7b-180">Load balance applications</span></span>](container-service-load-balancing.md)
