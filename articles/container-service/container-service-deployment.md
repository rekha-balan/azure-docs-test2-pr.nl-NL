---
title: Deploy a Docker container cluster in Azure | Microsoft Docs
description: Deploy a Kubernetes, DC/OS, or Docker Swarm solution in Azure Container Service by using the Azure portal or a Resource Manager template.
services: container-service
documentationcenter: ''
author: rgardler
manager: timlt
editor: ''
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure, dcos, swarm, kubernetes, azure container service, acs
ms.assetid: 696a736f-9299-4613-88c6-7177089cfc23
ms.service: container-service
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d3856861563ed104bbf51b1dac280bd58d692c3f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552167"
---
# <a name="deploy-a-docker-container-hosting-solution-using-the-azure-portal"></a><span data-ttu-id="3536b-104">Deploy a Docker container hosting solution using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="3536b-104">Deploy a Docker container hosting solution using the Azure portal</span></span>



<span data-ttu-id="3536b-105">Azure Container Service provides rapid deployment of popular open-source container clustering and orchestration solutions.</span><span class="sxs-lookup"><span data-stu-id="3536b-105">Azure Container Service provides rapid deployment of popular open-source container clustering and orchestration solutions.</span></span> <span data-ttu-id="3536b-106">This document walks you through deploying an Azure Container Service cluster by using the Azure portal or an Azure Resource Manager quickstart template.</span><span class="sxs-lookup"><span data-stu-id="3536b-106">This document walks you through deploying an Azure Container Service cluster by using the Azure portal or an Azure Resource Manager quickstart template.</span></span> 

<span data-ttu-id="3536b-107">You can also deploy an Azure Container Service cluster by using the [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) or the Azure Container Service APIs.</span><span class="sxs-lookup"><span data-stu-id="3536b-107">You can also deploy an Azure Container Service cluster by using the [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) or the Azure Container Service APIs.</span></span>

<span data-ttu-id="3536b-108">For background, see [Azure Container Service introduction](container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="3536b-108">For background, see [Azure Container Service introduction](container-service-intro.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="3536b-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3536b-109">Prerequisites</span></span>

* <span data-ttu-id="3536b-110">**Azure subscription**: If you don't have one, sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span><span class="sxs-lookup"><span data-stu-id="3536b-110">**Azure subscription**: If you don't have one, sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> <span data-ttu-id="3536b-111">For a larger cluster, consider a pay-as-you go subscription or other purchase options.</span><span class="sxs-lookup"><span data-stu-id="3536b-111">For a larger cluster, consider a pay-as-you go subscription or other purchase options.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3536b-112">Your Azure subscription usage and [resource quotas](../azure-subscription-service-limits.md), such as cores quotas, can limit the size of the cluster you deploy.</span><span class="sxs-lookup"><span data-stu-id="3536b-112">Your Azure subscription usage and [resource quotas](../azure-subscription-service-limits.md), such as cores quotas, can limit the size of the cluster you deploy.</span></span> <span data-ttu-id="3536b-113">To request a quota increase, open an [online customer support request](../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span><span class="sxs-lookup"><span data-stu-id="3536b-113">To request a quota increase, open an [online customer support request](../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
    >

* <span data-ttu-id="3536b-114">**SSH RSA public key**: When deploying through the portal or one of the Azure quickstart templates, you need to provide the public key for authentication against Azure Container Service virtual machines.</span><span class="sxs-lookup"><span data-stu-id="3536b-114">**SSH RSA public key**: When deploying through the portal or one of the Azure quickstart templates, you need to provide the public key for authentication against Azure Container Service virtual machines.</span></span> <span data-ttu-id="3536b-115">To create Secure Shell (SSH) RSA keys, see the [OS X and Linux](../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../virtual-machines/linux/ssh-from-windows.md) guidance.</span><span class="sxs-lookup"><span data-stu-id="3536b-115">To create Secure Shell (SSH) RSA keys, see the [OS X and Linux](../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../virtual-machines/linux/ssh-from-windows.md) guidance.</span></span> 

* <span data-ttu-id="3536b-116">**Service principal client ID and secret** (Kubernetes only): For more information and guidance to create an Azure Active Directory service principal, see [About the service principal for a Kubernetes cluster](container-service-kubernetes-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="3536b-116">**Service principal client ID and secret** (Kubernetes only): For more information and guidance to create an Azure Active Directory service principal, see [About the service principal for a Kubernetes cluster](container-service-kubernetes-service-principal.md).</span></span>



## <a name="create-a-cluster-by-using-the-azure-portal"></a><span data-ttu-id="3536b-117">Create a cluster by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="3536b-117">Create a cluster by using the Azure portal</span></span>
1. <span data-ttu-id="3536b-118">Sign in to the Azure portal, select **New**, and search the Azure Marketplace for **Azure Container Service**.</span><span class="sxs-lookup"><span data-stu-id="3536b-118">Sign in to the Azure portal, select **New**, and search the Azure Marketplace for **Azure Container Service**.</span></span>

    ![Azure Container Service in Marketplace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-deployment/acs-portal1.png)  <br />

2. <span data-ttu-id="3536b-120">Click **Azure Container Service**, and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3536b-120">Click **Azure Container Service**, and click **Create**.</span></span>

3. <span data-ttu-id="3536b-121">On the **Basics** blade, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="3536b-121">On the **Basics** blade, enter the following information:</span></span>

    * <span data-ttu-id="3536b-122">**Orchestrator**: Select one of the container orchestrators to deploy on the cluster.</span><span class="sxs-lookup"><span data-stu-id="3536b-122">**Orchestrator**: Select one of the container orchestrators to deploy on the cluster.</span></span>
        * <span data-ttu-id="3536b-123">**DC/OS**: Deploys a DC/OS cluster.</span><span class="sxs-lookup"><span data-stu-id="3536b-123">**DC/OS**: Deploys a DC/OS cluster.</span></span>
        * <span data-ttu-id="3536b-124">**Swarm**: Deploys a Docker Swarm cluster.</span><span class="sxs-lookup"><span data-stu-id="3536b-124">**Swarm**: Deploys a Docker Swarm cluster.</span></span>
        * <span data-ttu-id="3536b-125">**Kubernetes**: Deploys a Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="3536b-125">**Kubernetes**: Deploys a Kubernetes cluster.</span></span>
    * <span data-ttu-id="3536b-126">**Subscription**: Select an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="3536b-126">**Subscription**: Select an Azure subscription.</span></span>
    * <span data-ttu-id="3536b-127">**Resource group**: Enter the name of a new resource group for the deployment.</span><span class="sxs-lookup"><span data-stu-id="3536b-127">**Resource group**: Enter the name of a new resource group for the deployment.</span></span>
    * <span data-ttu-id="3536b-128">**Location**: Select an Azure region for the Azure Container Service deployment.</span><span class="sxs-lookup"><span data-stu-id="3536b-128">**Location**: Select an Azure region for the Azure Container Service deployment.</span></span> <span data-ttu-id="3536b-129">For availability, check [Products available by region](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="3536b-129">For availability, check [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
    
    ![Basic settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-deployment/acs-portal3.png)  <br />
    
    <span data-ttu-id="3536b-131">Click **OK** when you're ready to proceed.</span><span class="sxs-lookup"><span data-stu-id="3536b-131">Click **OK** when you're ready to proceed.</span></span>

4. <span data-ttu-id="3536b-132">On the **Master configuration** blade, enter the following settings for the Linux master node or nodes in the cluster (some settings are specific to each orchestrator):</span><span class="sxs-lookup"><span data-stu-id="3536b-132">On the **Master configuration** blade, enter the following settings for the Linux master node or nodes in the cluster (some settings are specific to each orchestrator):</span></span>

    * <span data-ttu-id="3536b-133">**Master DNS name**: The prefix used to create a unique fully qualified domain name (FQDN) for the master.</span><span class="sxs-lookup"><span data-stu-id="3536b-133">**Master DNS name**: The prefix used to create a unique fully qualified domain name (FQDN) for the master.</span></span> <span data-ttu-id="3536b-134">The master FQDN is of the form *prefix*mgmt.*location*.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="3536b-134">The master FQDN is of the form *prefix*mgmt.*location*.cloudapp.azure.com.</span></span>
    * <span data-ttu-id="3536b-135">**User name**: The user name for an account on each of the Linux virtual machines in the cluster.</span><span class="sxs-lookup"><span data-stu-id="3536b-135">**User name**: The user name for an account on each of the Linux virtual machines in the cluster.</span></span>
    * <span data-ttu-id="3536b-136">**SSH RSA public key**: Add the public key to be used for authentication against the Linux virtual machines.</span><span class="sxs-lookup"><span data-stu-id="3536b-136">**SSH RSA public key**: Add the public key to be used for authentication against the Linux virtual machines.</span></span> <span data-ttu-id="3536b-137">It is important that this key contains no line breaks, and it includes the `ssh-rsa` prefix.</span><span class="sxs-lookup"><span data-stu-id="3536b-137">It is important that this key contains no line breaks, and it includes the `ssh-rsa` prefix.</span></span> <span data-ttu-id="3536b-138">The `username@domain` postfix is optional.</span><span class="sxs-lookup"><span data-stu-id="3536b-138">The `username@domain` postfix is optional.</span></span> <span data-ttu-id="3536b-139">The key should look something like the following: **ssh-rsa AAAAB3Nz...<...>...UcyupgH azureuser@linuxvm**.</span><span class="sxs-lookup"><span data-stu-id="3536b-139">The key should look something like the following: **ssh-rsa AAAAB3Nz...<...>...UcyupgH azureuser@linuxvm**.</span></span> 
    * <span data-ttu-id="3536b-140">**Service principal**: If you selected the Kubernetes orchestrator, enter an Azure Active Directory **Service principal client ID** (also called the appId) and **Service principal client secret** (password).</span><span class="sxs-lookup"><span data-stu-id="3536b-140">**Service principal**: If you selected the Kubernetes orchestrator, enter an Azure Active Directory **Service principal client ID** (also called the appId) and **Service principal client secret** (password).</span></span> <span data-ttu-id="3536b-141">For more information, see [About the service principal for a Kubernetes cluster](container-service-kubernetes-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="3536b-141">For more information, see [About the service principal for a Kubernetes cluster](container-service-kubernetes-service-principal.md).</span></span>
    * <span data-ttu-id="3536b-142">**Master count**: The number of masters in the cluster.</span><span class="sxs-lookup"><span data-stu-id="3536b-142">**Master count**: The number of masters in the cluster.</span></span>
    * <span data-ttu-id="3536b-143">**VM diagnostics**: For some orchestrators, you can enable VM diagnostics on the masters.</span><span class="sxs-lookup"><span data-stu-id="3536b-143">**VM diagnostics**: For some orchestrators, you can enable VM diagnostics on the masters.</span></span>

    ![Master configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-deployment/acs-portal4.png)  <br />

    <span data-ttu-id="3536b-145">Click **OK** when you're ready to proceed.</span><span class="sxs-lookup"><span data-stu-id="3536b-145">Click **OK** when you're ready to proceed.</span></span>

5. <span data-ttu-id="3536b-146">On the **Agent configuration** blade, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="3536b-146">On the **Agent configuration** blade, enter the following information:</span></span>

    * <span data-ttu-id="3536b-147">**Agent count**: For Docker Swarm and Kubernetes, this value is the initial number of agents in the agent scale set.</span><span class="sxs-lookup"><span data-stu-id="3536b-147">**Agent count**: For Docker Swarm and Kubernetes, this value is the initial number of agents in the agent scale set.</span></span> <span data-ttu-id="3536b-148">For DC/OS, it is the initial number of agents in a private scale set.</span><span class="sxs-lookup"><span data-stu-id="3536b-148">For DC/OS, it is the initial number of agents in a private scale set.</span></span> <span data-ttu-id="3536b-149">Additionally, a public scale set is created for DC/OS, which contains a predetermined number of agents.</span><span class="sxs-lookup"><span data-stu-id="3536b-149">Additionally, a public scale set is created for DC/OS, which contains a predetermined number of agents.</span></span> <span data-ttu-id="3536b-150">The number of agents in this public scale set is determined by the number of masters in the cluster: one public agent for one master, and two public agents for three or five masters.</span><span class="sxs-lookup"><span data-stu-id="3536b-150">The number of agents in this public scale set is determined by the number of masters in the cluster: one public agent for one master, and two public agents for three or five masters.</span></span>
    * <span data-ttu-id="3536b-151">**Agent virtual machine size**: The size of the agent virtual machines.</span><span class="sxs-lookup"><span data-stu-id="3536b-151">**Agent virtual machine size**: The size of the agent virtual machines.</span></span>
    * <span data-ttu-id="3536b-152">**Operating system**: This setting is currently available only if you selected the Kubernetes orchestrator.</span><span class="sxs-lookup"><span data-stu-id="3536b-152">**Operating system**: This setting is currently available only if you selected the Kubernetes orchestrator.</span></span> <span data-ttu-id="3536b-153">Choose either a Linux distribution or a Windows Server operating system to run on the agents.</span><span class="sxs-lookup"><span data-stu-id="3536b-153">Choose either a Linux distribution or a Windows Server operating system to run on the agents.</span></span> <span data-ttu-id="3536b-154">This setting determines whether your cluster can run Linux or Windows container apps.</span><span class="sxs-lookup"><span data-stu-id="3536b-154">This setting determines whether your cluster can run Linux or Windows container apps.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="3536b-155">Windows container support is in preview for Kubernetes clusters.</span><span class="sxs-lookup"><span data-stu-id="3536b-155">Windows container support is in preview for Kubernetes clusters.</span></span> <span data-ttu-id="3536b-156">On DC/OS and Swarm clusters, only Linux agents are currently supported in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="3536b-156">On DC/OS and Swarm clusters, only Linux agents are currently supported in Azure Container Service.</span></span>

    * <span data-ttu-id="3536b-157">**Agent credentials**: If you selected the Windows operating system, enter an administrator **User name** and **Password** for the agent VMs.</span><span class="sxs-lookup"><span data-stu-id="3536b-157">**Agent credentials**: If you selected the Windows operating system, enter an administrator **User name** and **Password** for the agent VMs.</span></span> 

    ![Agent configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-deployment/acs-portal5.png)  <br />

    <span data-ttu-id="3536b-159">Click **OK** when you're ready to proceed.</span><span class="sxs-lookup"><span data-stu-id="3536b-159">Click **OK** when you're ready to proceed.</span></span>

6. <span data-ttu-id="3536b-160">After service validation finishes, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3536b-160">After service validation finishes, click **OK**.</span></span>

    ![Validation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-deployment/acs-portal6.png)  <br />

7. <span data-ttu-id="3536b-162">Review the terms.</span><span class="sxs-lookup"><span data-stu-id="3536b-162">Review the terms.</span></span> <span data-ttu-id="3536b-163">To start the deployment process, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3536b-163">To start the deployment process, click **Create**.</span></span>

    <span data-ttu-id="3536b-164">If you've elected to pin the deployment to the Azure portal, you can see the deployment status.</span><span class="sxs-lookup"><span data-stu-id="3536b-164">If you've elected to pin the deployment to the Azure portal, you can see the deployment status.</span></span>

    ![Deployment status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-deployment/acs-portal8.png)  <br />

<span data-ttu-id="3536b-166">The deployment takes several minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="3536b-166">The deployment takes several minutes to complete.</span></span> <span data-ttu-id="3536b-167">Then, the Azure Container Service cluster is ready for use.</span><span class="sxs-lookup"><span data-stu-id="3536b-167">Then, the Azure Container Service cluster is ready for use.</span></span>


## <a name="create-a-cluster-by-using-a-quickstart-template"></a><span data-ttu-id="3536b-168">Create a cluster by using a quickstart template</span><span class="sxs-lookup"><span data-stu-id="3536b-168">Create a cluster by using a quickstart template</span></span>
<span data-ttu-id="3536b-169">Azure quickstart templates are available to deploy a cluster in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="3536b-169">Azure quickstart templates are available to deploy a cluster in Azure Container Service.</span></span> <span data-ttu-id="3536b-170">The provided quickstart templates can be modified to include additional or advanced Azure configuration.</span><span class="sxs-lookup"><span data-stu-id="3536b-170">The provided quickstart templates can be modified to include additional or advanced Azure configuration.</span></span> <span data-ttu-id="3536b-171">To create an Azure Container Service cluster by using an Azure quickstart template, you need an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="3536b-171">To create an Azure Container Service cluster by using an Azure quickstart template, you need an Azure subscription.</span></span> <span data-ttu-id="3536b-172">If you don't have one, then sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span><span class="sxs-lookup"><span data-stu-id="3536b-172">If you don't have one, then sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> 

<span data-ttu-id="3536b-173">Follow these steps to deploy a cluster using a template and the Azure CLI 2.0 (see [installation and setup instructions](/cli/azure/install-az-cli2)).</span><span class="sxs-lookup"><span data-stu-id="3536b-173">Follow these steps to deploy a cluster using a template and the Azure CLI 2.0 (see [installation and setup instructions](/cli/azure/install-az-cli2)).</span></span>

> [!NOTE] 
> <span data-ttu-id="3536b-174">If you're on a Windows system, you can use similar steps to deploy a template using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3536b-174">If you're on a Windows system, you can use similar steps to deploy a template using Azure PowerShell.</span></span> <span data-ttu-id="3536b-175">See steps later in this section.</span><span class="sxs-lookup"><span data-stu-id="3536b-175">See steps later in this section.</span></span> <span data-ttu-id="3536b-176">You can also deploy a template through the [portal](../azure-resource-manager/resource-group-template-deploy-portal.md) or other methods.</span><span class="sxs-lookup"><span data-stu-id="3536b-176">You can also deploy a template through the [portal](../azure-resource-manager/resource-group-template-deploy-portal.md) or other methods.</span></span>

1. <span data-ttu-id="3536b-177">To deploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of the available quickstart templates from GitHub.</span><span class="sxs-lookup"><span data-stu-id="3536b-177">To deploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of the available quickstart templates from GitHub.</span></span> <span data-ttu-id="3536b-178">A partial list follows.</span><span class="sxs-lookup"><span data-stu-id="3536b-178">A partial list follows.</span></span> <span data-ttu-id="3536b-179">The DC/OS and Swarm templates are the same, except for the default orchestrator selection.</span><span class="sxs-lookup"><span data-stu-id="3536b-179">The DC/OS and Swarm templates are the same, except for the default orchestrator selection.</span></span>

    * [<span data-ttu-id="3536b-180">DC/OS template</span><span class="sxs-lookup"><span data-stu-id="3536b-180">DC/OS template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [<span data-ttu-id="3536b-181">Swarm template</span><span class="sxs-lookup"><span data-stu-id="3536b-181">Swarm template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [<span data-ttu-id="3536b-182">Kubernetes template</span><span class="sxs-lookup"><span data-stu-id="3536b-182">Kubernetes template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. <span data-ttu-id="3536b-183">Log in to your Azure account (`az login`), and make sure that the Azure CLI is connected to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="3536b-183">Log in to your Azure account (`az login`), and make sure that the Azure CLI is connected to your Azure subscription.</span></span> <span data-ttu-id="3536b-184">You can see the default subscription by using the following command:</span><span class="sxs-lookup"><span data-stu-id="3536b-184">You can see the default subscription by using the following command:</span></span>

    ```azurecli
    az account show
    ```
    
    <span data-ttu-id="3536b-185">If you have more than one subscription and need to set a different default subscription, run `az account set --subscription` and specify the subscription ID or name.</span><span class="sxs-lookup"><span data-stu-id="3536b-185">If you have more than one subscription and need to set a different default subscription, run `az account set --subscription` and specify the subscription ID or name.</span></span>

3. <span data-ttu-id="3536b-186">As a best practice, use a new resource group for the deployment.</span><span class="sxs-lookup"><span data-stu-id="3536b-186">As a best practice, use a new resource group for the deployment.</span></span> <span data-ttu-id="3536b-187">To create a resource group, use the `az group create` command specify a resource group name and location:</span><span class="sxs-lookup"><span data-stu-id="3536b-187">To create a resource group, use the `az group create` command specify a resource group name and location:</span></span> 

    ```azurecli
    az group create --name "RESOURCE_GROUP" --location "LOCATION"
    ```

4. <span data-ttu-id="3536b-188">Create a JSON file containing the required template parameters.</span><span class="sxs-lookup"><span data-stu-id="3536b-188">Create a JSON file containing the required template parameters.</span></span> <span data-ttu-id="3536b-189">Download the parameters file named `azuredeploy.parameters.json` that accompanies the Azure Container Service template `azuredeploy.json` in GitHub.</span><span class="sxs-lookup"><span data-stu-id="3536b-189">Download the parameters file named `azuredeploy.parameters.json` that accompanies the Azure Container Service template `azuredeploy.json` in GitHub.</span></span> <span data-ttu-id="3536b-190">Enter required parameter values for your cluster.</span><span class="sxs-lookup"><span data-stu-id="3536b-190">Enter required parameter values for your cluster.</span></span> 

    <span data-ttu-id="3536b-191">For example, to use the [DC/OS template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), supply parameter values for `dnsNamePrefix` and `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="3536b-191">For example, to use the [DC/OS template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), supply parameter values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="3536b-192">See the descriptions in `azuredeploy.json` and options for other parameters.</span><span class="sxs-lookup"><span data-stu-id="3536b-192">See the descriptions in `azuredeploy.json` and options for other parameters.</span></span>  
 

5. <span data-ttu-id="3536b-193">Create a Container Service cluster by passing the deployment parameters file with the following command, where:</span><span class="sxs-lookup"><span data-stu-id="3536b-193">Create a Container Service cluster by passing the deployment parameters file with the following command, where:</span></span>

    * <span data-ttu-id="3536b-194">**RESOURCE_GROUP** is the name of the resource group that you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="3536b-194">**RESOURCE_GROUP** is the name of the resource group that you created in the previous step.</span></span>
    * <span data-ttu-id="3536b-195">**DEPLOYMENT_NAME** (optional) is a name you give to the deployment.</span><span class="sxs-lookup"><span data-stu-id="3536b-195">**DEPLOYMENT_NAME** (optional) is a name you give to the deployment.</span></span>
    * <span data-ttu-id="3536b-196">**TEMPLATE_URI** is the location of the deployment file `azuredeploy.json`.</span><span class="sxs-lookup"><span data-stu-id="3536b-196">**TEMPLATE_URI** is the location of the deployment file `azuredeploy.json`.</span></span> <span data-ttu-id="3536b-197">This URI must be the Raw file, not a pointer to the GitHub UI.</span><span class="sxs-lookup"><span data-stu-id="3536b-197">This URI must be the Raw file, not a pointer to the GitHub UI.</span></span> <span data-ttu-id="3536b-198">To find this URI, select the `azuredeploy.json` file in GitHub, and click the **Raw** button.</span><span class="sxs-lookup"><span data-stu-id="3536b-198">To find this URI, select the `azuredeploy.json` file in GitHub, and click the **Raw** button.</span></span>  

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters @azuredeploy.parameters.json
    ```

    <span data-ttu-id="3536b-199">You can also provide parameters as a JSON-formatted string on the command line.</span><span class="sxs-lookup"><span data-stu-id="3536b-199">You can also provide parameters as a JSON-formatted string on the command line.</span></span> <span data-ttu-id="3536b-200">Use a command similar to the following:</span><span class="sxs-lookup"><span data-stu-id="3536b-200">Use a command similar to the following:</span></span>

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters "{ \"param1\": {\"value1\"} … }"
    ```

    > [!NOTE]
    > <span data-ttu-id="3536b-201">The deployment takes several minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="3536b-201">The deployment takes several minutes to complete.</span></span>
    > 

### <a name="equivalent-powershell-commands"></a><span data-ttu-id="3536b-202">Equivalent PowerShell commands</span><span class="sxs-lookup"><span data-stu-id="3536b-202">Equivalent PowerShell commands</span></span>
<span data-ttu-id="3536b-203">You can also deploy an Azure Container Service cluster template with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3536b-203">You can also deploy an Azure Container Service cluster template with PowerShell.</span></span> <span data-ttu-id="3536b-204">This document is based on the version 1.0 [Azure PowerShell module](https://azure.microsoft.com/blog/azps-1-0/).</span><span class="sxs-lookup"><span data-stu-id="3536b-204">This document is based on the version 1.0 [Azure PowerShell module](https://azure.microsoft.com/blog/azps-1-0/).</span></span>

1. <span data-ttu-id="3536b-205">To deploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of the available quickstart templates from GitHub.</span><span class="sxs-lookup"><span data-stu-id="3536b-205">To deploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of the available quickstart templates from GitHub.</span></span> <span data-ttu-id="3536b-206">A partial list follows.</span><span class="sxs-lookup"><span data-stu-id="3536b-206">A partial list follows.</span></span> <span data-ttu-id="3536b-207">Note that the DC/OS and Swarm templates are the same, with the exception of the default orchestrator selection.</span><span class="sxs-lookup"><span data-stu-id="3536b-207">Note that the DC/OS and Swarm templates are the same, with the exception of the default orchestrator selection.</span></span>

    * [<span data-ttu-id="3536b-208">DC/OS template</span><span class="sxs-lookup"><span data-stu-id="3536b-208">DC/OS template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [<span data-ttu-id="3536b-209">Swarm template</span><span class="sxs-lookup"><span data-stu-id="3536b-209">Swarm template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [<span data-ttu-id="3536b-210">Kubernetes template</span><span class="sxs-lookup"><span data-stu-id="3536b-210">Kubernetes template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. <span data-ttu-id="3536b-211">Before creating a cluster in your Azure subscription, verify that your PowerShell session has been signed in to Azure.</span><span class="sxs-lookup"><span data-stu-id="3536b-211">Before creating a cluster in your Azure subscription, verify that your PowerShell session has been signed in to Azure.</span></span> <span data-ttu-id="3536b-212">You can do this with the `Get-AzureRMSubscription` command:</span><span class="sxs-lookup"><span data-stu-id="3536b-212">You can do this with the `Get-AzureRMSubscription` command:</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="3536b-213">If you need to sign in to Azure, use the `Login-AzureRMAccount` command:</span><span class="sxs-lookup"><span data-stu-id="3536b-213">If you need to sign in to Azure, use the `Login-AzureRMAccount` command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

4. <span data-ttu-id="3536b-214">As a best practice, use a new resource group for the deployment.</span><span class="sxs-lookup"><span data-stu-id="3536b-214">As a best practice, use a new resource group for the deployment.</span></span> <span data-ttu-id="3536b-215">To create a resource group, use the `New-AzureRmResourceGroup` command, and specify a resource group name and destination region:</span><span class="sxs-lookup"><span data-stu-id="3536b-215">To create a resource group, use the `New-AzureRmResourceGroup` command, and specify a resource group name and destination region:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name GROUP_NAME -Location REGION
    ```

5. <span data-ttu-id="3536b-216">After you create a resource group, you can create your cluster with the following command.</span><span class="sxs-lookup"><span data-stu-id="3536b-216">After you create a resource group, you can create your cluster with the following command.</span></span> <span data-ttu-id="3536b-217">The URI of the desired template is specified with the `-TemplateUri` parameter.</span><span class="sxs-lookup"><span data-stu-id="3536b-217">The URI of the desired template is specified with the `-TemplateUri` parameter.</span></span> <span data-ttu-id="3536b-218">When you run this command, PowerShell prompts you for deployment parameter values.</span><span class="sxs-lookup"><span data-stu-id="3536b-218">When you run this command, PowerShell prompts you for deployment parameter values.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DEPLOYMENT_NAME -ResourceGroupName RESOURCE_GROUP_NAME -TemplateUri TEMPLATE_URI
    ```

#### <a name="provide-template-parameters"></a><span data-ttu-id="3536b-219">Provide template parameters</span><span class="sxs-lookup"><span data-stu-id="3536b-219">Provide template parameters</span></span>
<span data-ttu-id="3536b-220">If you're familiar with PowerShell, you know that you can cycle through the available parameters for a cmdlet by typing a minus sign (-) and then pressing the TAB key.</span><span class="sxs-lookup"><span data-stu-id="3536b-220">If you're familiar with PowerShell, you know that you can cycle through the available parameters for a cmdlet by typing a minus sign (-) and then pressing the TAB key.</span></span> <span data-ttu-id="3536b-221">This same functionality also works with parameters that you define in your template.</span><span class="sxs-lookup"><span data-stu-id="3536b-221">This same functionality also works with parameters that you define in your template.</span></span> <span data-ttu-id="3536b-222">As soon as you type the template name, the cmdlet fetches the template, parses the parameters, and adds the template parameters to the command dynamically.</span><span class="sxs-lookup"><span data-stu-id="3536b-222">As soon as you type the template name, the cmdlet fetches the template, parses the parameters, and adds the template parameters to the command dynamically.</span></span> <span data-ttu-id="3536b-223">This makes it easy to specify the template parameter values.</span><span class="sxs-lookup"><span data-stu-id="3536b-223">This makes it easy to specify the template parameter values.</span></span> <span data-ttu-id="3536b-224">And, if you forget a required parameter value, PowerShell prompts you for the value.</span><span class="sxs-lookup"><span data-stu-id="3536b-224">And, if you forget a required parameter value, PowerShell prompts you for the value.</span></span>

<span data-ttu-id="3536b-225">Here is the full command, with parameters included.</span><span class="sxs-lookup"><span data-stu-id="3536b-225">Here is the full command, with parameters included.</span></span> <span data-ttu-id="3536b-226">Provide your own values for the names of the resources.</span><span class="sxs-lookup"><span data-stu-id="3536b-226">Provide your own values for the names of the resources.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName RESOURCE_GROUP_NAME-TemplateURI TEMPLATE_URI -adminuser value1 -adminpassword value2 ....
```

## <a name="next-steps"></a><span data-ttu-id="3536b-227">Next steps</span><span class="sxs-lookup"><span data-stu-id="3536b-227">Next steps</span></span>
<span data-ttu-id="3536b-228">Now that you have a functioning cluster, see these documents for connection and management details:</span><span class="sxs-lookup"><span data-stu-id="3536b-228">Now that you have a functioning cluster, see these documents for connection and management details:</span></span>

* [<span data-ttu-id="3536b-229">Connect to an Azure Container Service cluster</span><span class="sxs-lookup"><span data-stu-id="3536b-229">Connect to an Azure Container Service cluster</span></span>](container-service-connect.md)
* [<span data-ttu-id="3536b-230">Work with Azure Container Service and DC/OS</span><span class="sxs-lookup"><span data-stu-id="3536b-230">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="3536b-231">Work with Azure Container Service and Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="3536b-231">Work with Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)
* [<span data-ttu-id="3536b-232">Work with Azure Container Service and Kubernetes</span><span class="sxs-lookup"><span data-stu-id="3536b-232">Work with Azure Container Service and Kubernetes</span></span>](container-service-kubernetes-walkthrough.md)






