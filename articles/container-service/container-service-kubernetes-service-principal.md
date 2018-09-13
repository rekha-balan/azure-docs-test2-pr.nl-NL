---
title: Service principal for Azure Kubernetes cluster | Microsoft Docs
description: Create and manage an Azure Active Directory service principal in an Azure Container Service cluster with Kubernetes
services: container-service
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: acs, azure-container-service, kubernetes
keywords: ''
ms.assetid: ''
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/21/2017
ms.author: danlep
ms.openlocfilehash: a803e0b9e87c8cfda0cd3db079c77acf62373763
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553632"
---
# <a name="about-the-azure-active-directory-service-principal-for-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="6c3cd-103">About the Azure Active Directory service principal for a Kubernetes cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="6c3cd-103">About the Azure Active Directory service principal for a Kubernetes cluster in Azure Container Service</span></span>



<span data-ttu-id="6c3cd-104">In Azure Container Service, Kubernetes requires an [Azure Active Directory service principal](../active-directory/active-directory-application-objects.md) as a service account to interact with Azure APIs.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-104">In Azure Container Service, Kubernetes requires an [Azure Active Directory service principal](../active-directory/active-directory-application-objects.md) as a service account to interact with Azure APIs.</span></span> <span data-ttu-id="6c3cd-105">The service principal is needed to dynamically manage resources such as user-defined routes and the Layer 4 Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-105">The service principal is needed to dynamically manage resources such as user-defined routes and the Layer 4 Azure Load Balancer.</span></span>

<span data-ttu-id="6c3cd-106">This article shows different options to specify a service principal for your Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-106">This article shows different options to specify a service principal for your Kubernetes cluster.</span></span> <span data-ttu-id="6c3cd-107">For example, if you installed and set up the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2), you can run the [`az acs create`](https://docs.microsoft.com/en-us/cli/azure/acs#create) command to create the Kubernetes cluster and the service principal at the same time.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-107">For example, if you installed and set up the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2), you can run the [`az acs create`](https://docs.microsoft.com/en-us/cli/azure/acs#create) command to create the Kubernetes cluster and the service principal at the same time.</span></span>



## <a name="requirements-for-the-service-principal"></a><span data-ttu-id="6c3cd-108">Requirements for the service principal</span><span class="sxs-lookup"><span data-stu-id="6c3cd-108">Requirements for the service principal</span></span>

<span data-ttu-id="6c3cd-109">Following are requirements for the Azure Active Directory service principal in a Kubernetes cluster in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-109">Following are requirements for the Azure Active Directory service principal in a Kubernetes cluster in Azure Container Service.</span></span> 

* <span data-ttu-id="6c3cd-110">**Scope**: the resource group in which the cluster is deployed</span><span class="sxs-lookup"><span data-stu-id="6c3cd-110">**Scope**: the resource group in which the cluster is deployed</span></span>

* <span data-ttu-id="6c3cd-111">**Role**: **Contributor**</span><span class="sxs-lookup"><span data-stu-id="6c3cd-111">**Role**: **Contributor**</span></span>

* <span data-ttu-id="6c3cd-112">**Client secret**: must be a password.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-112">**Client secret**: must be a password.</span></span> <span data-ttu-id="6c3cd-113">Currently, you can't use a service principal set up for certificate authentication.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-113">Currently, you can't use a service principal set up for certificate authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="6c3cd-114">Every service principal is associated with an Azure Active Directory application.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-114">Every service principal is associated with an Azure Active Directory application.</span></span> <span data-ttu-id="6c3cd-115">The service principal for a Kubernetes cluster can be associated with any valid Azure Active Directory application name.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-115">The service principal for a Kubernetes cluster can be associated with any valid Azure Active Directory application name.</span></span>
> 


## <a name="service-principal-options-for-a-kubernetes-cluster"></a><span data-ttu-id="6c3cd-116">Service principal options for a Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="6c3cd-116">Service principal options for a Kubernetes cluster</span></span>

### <a name="option-1-pass-the-service-principal-client-id-and-client-secret"></a><span data-ttu-id="6c3cd-117">Option 1: Pass the service principal client ID and client secret</span><span class="sxs-lookup"><span data-stu-id="6c3cd-117">Option 1: Pass the service principal client ID and client secret</span></span>

<span data-ttu-id="6c3cd-118">Provide the **client ID** (also called the `appId`, for Application ID) and **client secret** (`password`) of an existing service principal as parameters when you create the Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-118">Provide the **client ID** (also called the `appId`, for Application ID) and **client secret** (`password`) of an existing service principal as parameters when you create the Kubernetes cluster.</span></span> <span data-ttu-id="6c3cd-119">If you are using an existing service principal, make sure it meets the requirements in the previous section.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-119">If you are using an existing service principal, make sure it meets the requirements in the previous section.</span></span> <span data-ttu-id="6c3cd-120">If you need to create a service principal, see [Create a service principal](#create-a-service-principal-in-azure-active-directory) later in this article.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-120">If you need to create a service principal, see [Create a service principal](#create-a-service-principal-in-azure-active-directory) later in this article.</span></span>

<span data-ttu-id="6c3cd-121">You can specify these parameters when [deploying the Kubernetes cluster](./container-service-deployment.md) using the portal, the Azure Command-Line Interface (CLI) 2.0, Azure PowerShell, or other methods.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-121">You can specify these parameters when [deploying the Kubernetes cluster](./container-service-deployment.md) using the portal, the Azure Command-Line Interface (CLI) 2.0, Azure PowerShell, or other methods.</span></span>

>[!TIP] 
><span data-ttu-id="6c3cd-122">When specifying the **client ID**, be sure to use the `appId`, not the `ObjectId`, of the service principal.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-122">When specifying the **client ID**, be sure to use the `appId`, not the `ObjectId`, of the service principal.</span></span>
>

<span data-ttu-id="6c3cd-123">The following example shows one way to pass the parameters with the Azure CLI 2.0 (see [installation and setup instructions](/cli/azure/install-az-cli2)).</span><span class="sxs-lookup"><span data-stu-id="6c3cd-123">The following example shows one way to pass the parameters with the Azure CLI 2.0 (see [installation and setup instructions](/cli/azure/install-az-cli2)).</span></span> <span data-ttu-id="6c3cd-124">This example uses the [Kubernetes quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span><span class="sxs-lookup"><span data-stu-id="6c3cd-124">This example uses the [Kubernetes quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span></span>

1. <span data-ttu-id="6c3cd-125">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) the template parameters file `azuredeploy.parameters.json` from GitHub.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-125">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) the template parameters file `azuredeploy.parameters.json` from GitHub.</span></span>

2. <span data-ttu-id="6c3cd-126">To specify the service principal, enter values for `servicePrincipalClientId` and `servicePrincipalClientSecret` in the file.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-126">To specify the service principal, enter values for `servicePrincipalClientId` and `servicePrincipalClientSecret` in the file.</span></span> <span data-ttu-id="6c3cd-127">(You also need to provide your own values for `dnsNamePrefix` and `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-127">(You also need to provide your own values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="6c3cd-128">The latter is the SSH public key to access the cluster.) Save the file.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-128">The latter is the SSH public key to access the cluster.) Save the file.</span></span>

    ![Pass service principal parameters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-service-principal/service-principal-params.png)

3. <span data-ttu-id="6c3cd-130">Run the following command, using `--parameters` to set the path to the azuredeploy.parameters.json file.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-130">Run the following command, using `--parameters` to set the path to the azuredeploy.parameters.json file.</span></span> <span data-ttu-id="6c3cd-131">This command deploys the cluster in a resource group you create called `myResourceGroup` in the West US region.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-131">This command deploys the cluster in a resource group you create called `myResourceGroup` in the West US region.</span></span>

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


### <a name="option-2-generate-the-service-principal-when-creating-the-cluster-with-the-azure-cli-20"></a><span data-ttu-id="6c3cd-132">Option 2: Generate the service principal when creating the cluster with the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6c3cd-132">Option 2: Generate the service principal when creating the cluster with the Azure CLI 2.0</span></span>

<span data-ttu-id="6c3cd-133">If you installed and set up the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2), you can run the [`az acs create`](https://docs.microsoft.com/en-us/cli/azure/acs#create) command to [create the cluster](./container-service-create-acs-cluster-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6c3cd-133">If you installed and set up the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2), you can run the [`az acs create`](https://docs.microsoft.com/en-us/cli/azure/acs#create) command to [create the cluster](./container-service-create-acs-cluster-cli.md).</span></span>

<span data-ttu-id="6c3cd-134">As with other Kubernetes cluster creation options, you can specify parameters for an existing service principal when you run `az acs create`.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-134">As with other Kubernetes cluster creation options, you can specify parameters for an existing service principal when you run `az acs create`.</span></span> <span data-ttu-id="6c3cd-135">However, when you omit these parameters, Azure Container Service creates a service principal automatically.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-135">However, when you omit these parameters, Azure Container Service creates a service principal automatically.</span></span> <span data-ttu-id="6c3cd-136">This takes place transparently during the deployment.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-136">This takes place transparently during the deployment.</span></span> 

<span data-ttu-id="6c3cd-137">The following command creates a Kubernetes cluster and generates both SSH keys and service principal credentials:</span><span class="sxs-lookup"><span data-stu-id="6c3cd-137">The following command creates a Kubernetes cluster and generates both SSH keys and service principal credentials:</span></span>

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

## <a name="create-a-service-principal-in-azure-active-directory"></a><span data-ttu-id="6c3cd-138">Create a service principal in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6c3cd-138">Create a service principal in Azure Active Directory</span></span>

<span data-ttu-id="6c3cd-139">If you want to create a service principal in Azure Active Directory for use in your Kubernetes cluster, Azure provides several methods.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-139">If you want to create a service principal in Azure Active Directory for use in your Kubernetes cluster, Azure provides several methods.</span></span> 

<span data-ttu-id="6c3cd-140">The following example commands show you how to do this with the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="6c3cd-140">The following example commands show you how to do this with the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span> <span data-ttu-id="6c3cd-141">You can alternatively create a service principal using [Azure PowerShell](../azure-resource-manager/resource-group-authenticate-service-principal.md), the [classic portal](../azure-resource-manager/resource-group-create-service-principal-portal.md), or other methods.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-141">You can alternatively create a service principal using [Azure PowerShell](../azure-resource-manager/resource-group-authenticate-service-principal.md), the [classic portal](../azure-resource-manager/resource-group-create-service-principal-portal.md), or other methods.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c3cd-142">Make sure you review the requirements for the service principal earlier in this article.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-142">Make sure you review the requirements for the service principal earlier in this article.</span></span>
>

```azurecli
az login

az account set --subscription "mySubscriptionID"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID"
```

<span data-ttu-id="6c3cd-143">This returns output similar to the following (shown here redacted):</span><span class="sxs-lookup"><span data-stu-id="6c3cd-143">This returns output similar to the following (shown here redacted):</span></span>

![Create a service principal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-service-principal/service-principal-creds.png)

<span data-ttu-id="6c3cd-145">Highlighted are the **client ID** (`appId`) and the **client secret** (`password`) that you use as service principal parameters for cluster deployment.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-145">Highlighted are the **client ID** (`appId`) and the **client secret** (`password`) that you use as service principal parameters for cluster deployment.</span></span>


<span data-ttu-id="6c3cd-146">Confirm your service principal by opening a new shell and run the following commands, substituting in `appId`, `password`, and `tenant`:</span><span class="sxs-lookup"><span data-stu-id="6c3cd-146">Confirm your service principal by opening a new shell and run the following commands, substituting in `appId`, `password`, and `tenant`:</span></span>

```azurecli 
az login --service-principal -u yourClientID -p yourClientSecret --tenant yourTenant

az vm list-sizes --location westus
```

## <a name="additional-considerations"></a><span data-ttu-id="6c3cd-147">Additional considerations</span><span class="sxs-lookup"><span data-stu-id="6c3cd-147">Additional considerations</span></span>


* <span data-ttu-id="6c3cd-148">When specifying the service principal **Client ID**, you can use the value of the `appId` (as shown in this article) or the corresponding service principal `name` (for example,        `https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="6c3cd-148">When specifying the service principal **Client ID**, you can use the value of the `appId` (as shown in this article) or the corresponding service principal `name` (for example,        `https://www.contoso.org/example`).</span></span>

* <span data-ttu-id="6c3cd-149">If you use the `az acs create` command to generate the service principal automatically, the service principal credentials are written to the file ~/.azure/acsServicePrincipal.json on the machine used to run the command.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-149">If you use the `az acs create` command to generate the service principal automatically, the service principal credentials are written to the file ~/.azure/acsServicePrincipal.json on the machine used to run the command.</span></span>

* <span data-ttu-id="6c3cd-150">On the master and node VMs in the Kubernetes cluster, the service principal credentials are stored in the file /etc/kubernetes/azure.json.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-150">On the master and node VMs in the Kubernetes cluster, the service principal credentials are stored in the file /etc/kubernetes/azure.json.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c3cd-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="6c3cd-151">Next steps</span></span>

* <span data-ttu-id="6c3cd-152">[Get started with Kubernetes](container-service-kubernetes-walkthrough.md) in your container service cluster.</span><span class="sxs-lookup"><span data-stu-id="6c3cd-152">[Get started with Kubernetes](container-service-kubernetes-walkthrough.md) in your container service cluster.</span></span>


