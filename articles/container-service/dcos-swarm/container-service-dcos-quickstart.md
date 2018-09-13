---
title: Azure Container Service Quickstart - Deploy DC/OS Cluster
description: Azure Container Service Quickstart - Deploy DC/OS Cluster
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: quickstart
ms.date: 02/26/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c2c1ef83ade7040e16f54b87f63f6eb27714bf2a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856819"
---
# <a name="deploy-a-dcos-cluster"></a><span data-ttu-id="92314-103">Deploy a DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="92314-103">Deploy a DC/OS cluster</span></span>

<span data-ttu-id="92314-104">DC/OS provides a distributed platform for running modern and containerized applications.</span><span class="sxs-lookup"><span data-stu-id="92314-104">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="92314-105">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span><span class="sxs-lookup"><span data-stu-id="92314-105">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="92314-106">This quick start details the basic steps needed to deploy a DC/OS cluster and run basic workload.</span><span class="sxs-lookup"><span data-stu-id="92314-106">This quick start details the basic steps needed to deploy a DC/OS cluster and run basic workload.</span></span>

<span data-ttu-id="92314-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="92314-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="92314-108">This tutorial requires the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="92314-108">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="92314-109">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="92314-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="92314-110">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="92314-110">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="log-in-to-azure"></a><span data-ttu-id="92314-111">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="92314-111">Log in to Azure</span></span> 

<span data-ttu-id="92314-112">Log in to your Azure subscription with the [az login](/cli/azure/reference-index#az-login) command and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="92314-112">Log in to your Azure subscription with the [az login](/cli/azure/reference-index#az-login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="92314-113">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="92314-113">Create a resource group</span></span>

<span data-ttu-id="92314-114">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span><span class="sxs-lookup"><span data-stu-id="92314-114">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span></span> <span data-ttu-id="92314-115">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="92314-115">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="92314-116">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="92314-116">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a><span data-ttu-id="92314-117">Create DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="92314-117">Create DC/OS cluster</span></span>

<span data-ttu-id="92314-118">Create a DC/OS cluster with the [az acs create](/cli/azure/acs#az-acs-create) command.</span><span class="sxs-lookup"><span data-stu-id="92314-118">Create a DC/OS cluster with the [az acs create](/cli/azure/acs#az-acs-create) command.</span></span>

<span data-ttu-id="92314-119">The following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span><span class="sxs-lookup"><span data-stu-id="92314-119">The following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="92314-120">To use a specific set of keys, use the `--ssh-key-value` option.</span><span class="sxs-lookup"><span data-stu-id="92314-120">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli
az acs create --orchestrator-type dcos --resource-group myResourceGroup --name myDCOSCluster --generate-ssh-keys
```

<span data-ttu-id="92314-121">In some cases, such as with a limited trial, an Azure subscription has limited access to Azure resources.</span><span class="sxs-lookup"><span data-stu-id="92314-121">In some cases, such as with a limited trial, an Azure subscription has limited access to Azure resources.</span></span> <span data-ttu-id="92314-122">If the deployment fails due to limited available cores, reduce the default agent count by adding `--agent-count 1` to the [az acs create](/cli/azure/acs#az-acs-create) command.</span><span class="sxs-lookup"><span data-stu-id="92314-122">If the deployment fails due to limited available cores, reduce the default agent count by adding `--agent-count 1` to the [az acs create](/cli/azure/acs#az-acs-create) command.</span></span> 

<span data-ttu-id="92314-123">After several minutes, the command completes, and returns information about the deployment.</span><span class="sxs-lookup"><span data-stu-id="92314-123">After several minutes, the command completes, and returns information about the deployment.</span></span>

## <a name="connect-to-dcos-cluster"></a><span data-ttu-id="92314-124">Connect to DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="92314-124">Connect to DC/OS cluster</span></span>

<span data-ttu-id="92314-125">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span><span class="sxs-lookup"><span data-stu-id="92314-125">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="92314-126">Run the following command to return the public IP address of the DC/OS master.</span><span class="sxs-lookup"><span data-stu-id="92314-126">Run the following command to return the public IP address of the DC/OS master.</span></span> <span data-ttu-id="92314-127">This IP address is stored in a variable and used in the next step.</span><span class="sxs-lookup"><span data-stu-id="92314-127">This IP address is stored in a variable and used in the next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="92314-128">To create the SSH tunnel, run the following command and follow the on-screen instructions.</span><span class="sxs-lookup"><span data-stu-id="92314-128">To create the SSH tunnel, run the following command and follow the on-screen instructions.</span></span> <span data-ttu-id="92314-129">If port 80 is already in use, the command fails.</span><span class="sxs-lookup"><span data-stu-id="92314-129">If port 80 is already in use, the command fails.</span></span> <span data-ttu-id="92314-130">Update the tunneled port to one not in use, such as `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="92314-130">Update the tunneled port to one not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

<span data-ttu-id="92314-131">The SSH tunnel can be tested by browsing to `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="92314-131">The SSH tunnel can be tested by browsing to `http://localhost`.</span></span> <span data-ttu-id="92314-132">If a port other that 80 has been used, adjust the location to match.</span><span class="sxs-lookup"><span data-stu-id="92314-132">If a port other that 80 has been used, adjust the location to match.</span></span> 

<span data-ttu-id="92314-133">If the SSH tunnel was successfully created, the DC/OS portal is returned.</span><span class="sxs-lookup"><span data-stu-id="92314-133">If the SSH tunnel was successfully created, the DC/OS portal is returned.</span></span>

![DCOS UI](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a><span data-ttu-id="92314-135">Install DC/OS CLI</span><span class="sxs-lookup"><span data-stu-id="92314-135">Install DC/OS CLI</span></span>

<span data-ttu-id="92314-136">The DC/OS command line interface is used to manage a DC/OS cluster from the command-line.</span><span class="sxs-lookup"><span data-stu-id="92314-136">The DC/OS command line interface is used to manage a DC/OS cluster from the command-line.</span></span> <span data-ttu-id="92314-137">Install the DC/OS cli using the [az acs dcos install-cli](/cli/azure/acs/dcos#az-acs-dcos-install-cli) command.</span><span class="sxs-lookup"><span data-stu-id="92314-137">Install the DC/OS cli using the [az acs dcos install-cli](/cli/azure/acs/dcos#az-acs-dcos-install-cli) command.</span></span> <span data-ttu-id="92314-138">If you are using Azure CloudShell, the DC/OS CLI is already installed.</span><span class="sxs-lookup"><span data-stu-id="92314-138">If you are using Azure CloudShell, the DC/OS CLI is already installed.</span></span> 

<span data-ttu-id="92314-139">If you are running the Azure CLI on macOS or Linux, you might need to run the command with sudo.</span><span class="sxs-lookup"><span data-stu-id="92314-139">If you are running the Azure CLI on macOS or Linux, you might need to run the command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="92314-140">Before the CLI can be used with the cluster, it must be configured to use the SSH tunnel.</span><span class="sxs-lookup"><span data-stu-id="92314-140">Before the CLI can be used with the cluster, it must be configured to use the SSH tunnel.</span></span> <span data-ttu-id="92314-141">To do so, run the following command, adjusting the port if needed.</span><span class="sxs-lookup"><span data-stu-id="92314-141">To do so, run the following command, adjusting the port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="92314-142">Run an application</span><span class="sxs-lookup"><span data-stu-id="92314-142">Run an application</span></span>

<span data-ttu-id="92314-143">The default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span><span class="sxs-lookup"><span data-stu-id="92314-143">The default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="92314-144">Marathon is used to start an application and manage the state of the application on the DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="92314-144">Marathon is used to start an application and manage the state of the application on the DC/OS cluster.</span></span> <span data-ttu-id="92314-145">To schedule an application through Marathon, create a file named *marathon-app.json*, and copy the following contents into it.</span><span class="sxs-lookup"><span data-stu-id="92314-145">To schedule an application through Marathon, create a file named *marathon-app.json*, and copy the following contents into it.</span></span> 

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

<span data-ttu-id="92314-146">Run the following command to schedule the application to run on the DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="92314-146">Run the following command to schedule the application to run on the DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="92314-147">To see the deployment status for the app, run the following command.</span><span class="sxs-lookup"><span data-stu-id="92314-147">To see the deployment status for the app, run the following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="92314-148">When the **WAITING** column value switches from *True* to *False*, application deployment has completed.</span><span class="sxs-lookup"><span data-stu-id="92314-148">When the **WAITING** column value switches from *True* to *False*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

<span data-ttu-id="92314-149">Get the public IP address of the DC/OS cluster agents.</span><span class="sxs-lookup"><span data-stu-id="92314-149">Get the public IP address of the DC/OS cluster agents.</span></span>

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="92314-150">Browsing to this address returns the default NGINX site.</span><span class="sxs-lookup"><span data-stu-id="92314-150">Browsing to this address returns the default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a><span data-ttu-id="92314-152">Delete DC/OS cluster</span><span class="sxs-lookup"><span data-stu-id="92314-152">Delete DC/OS cluster</span></span>

<span data-ttu-id="92314-153">When no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, DC/OS cluster, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="92314-153">When no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="92314-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="92314-154">Next steps</span></span>

<span data-ttu-id="92314-155">In this quick start, you’ve deployed a DC/OS cluster and have run a simple Docker container on the cluster.</span><span class="sxs-lookup"><span data-stu-id="92314-155">In this quick start, you’ve deployed a DC/OS cluster and have run a simple Docker container on the cluster.</span></span> <span data-ttu-id="92314-156">To learn more about Azure Container Service, continue to the ACS tutorials.</span><span class="sxs-lookup"><span data-stu-id="92314-156">To learn more about Azure Container Service, continue to the ACS tutorials.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="92314-157">Manage an ACS DC/OS Cluster</span><span class="sxs-lookup"><span data-stu-id="92314-157">Manage an ACS DC/OS Cluster</span></span>](container-service-dcos-manage-tutorial.md)