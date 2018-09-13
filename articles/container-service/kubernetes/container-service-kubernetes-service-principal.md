---
title: Service principal for Azure Kubernetes cluster
description: Create and manage an Azure Active Directory service principal for a Kubernetes cluster in Azure Container Service
services: container-service
author: neilpeterson
manager: jeconnoc
ms.service: container-service
ms.topic: get-started-article
ms.date: 02/26/2018
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: efedb7cde06ed03ec330027a18b00bcc897919cf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856774"
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a><span data-ttu-id="5d8ba-103">Set up an Azure AD service principal for a Kubernetes cluster in Container Service</span><span class="sxs-lookup"><span data-stu-id="5d8ba-103">Set up an Azure AD service principal for a Kubernetes cluster in Container Service</span></span>

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

<span data-ttu-id="5d8ba-104">In Azure Container Service, a Kubernetes cluster requires an [Azure Active Directory service principal](../../active-directory/develop/app-objects-and-service-principals.md) to interact with Azure APIs.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-104">In Azure Container Service, a Kubernetes cluster requires an [Azure Active Directory service principal](../../active-directory/develop/app-objects-and-service-principals.md) to interact with Azure APIs.</span></span> <span data-ttu-id="5d8ba-105">The service principal is needed to dynamically manage resources such as [user-defined routes](../../virtual-network/virtual-networks-udr-overview.md) and the [Layer 4 Azure Load Balancer](../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5d8ba-105">The service principal is needed to dynamically manage resources such as [user-defined routes](../../virtual-network/virtual-networks-udr-overview.md) and the [Layer 4 Azure Load Balancer](../../load-balancer/load-balancer-overview.md).</span></span>


<span data-ttu-id="5d8ba-106">This article shows different options to set up a service principal for your Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-106">This article shows different options to set up a service principal for your Kubernetes cluster.</span></span> <span data-ttu-id="5d8ba-107">For example, if you installed and set up the [Azure CLI 2.0](/cli/azure/install-az-cli2), you can run the [`az acs create`](/cli/azure/acs#az-acs-create) command to create the Kubernetes cluster and the service principal at the same time.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-107">For example, if you installed and set up the [Azure CLI 2.0](/cli/azure/install-az-cli2), you can run the [`az acs create`](/cli/azure/acs#az-acs-create) command to create the Kubernetes cluster and the service principal at the same time.</span></span>


## <a name="requirements-for-the-service-principal"></a><span data-ttu-id="5d8ba-108">Requirements for the service principal</span><span class="sxs-lookup"><span data-stu-id="5d8ba-108">Requirements for the service principal</span></span>

<span data-ttu-id="5d8ba-109">You can use an existing Azure AD service principal that meets the following requirements, or create a new one.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-109">You can use an existing Azure AD service principal that meets the following requirements, or create a new one.</span></span>

* <span data-ttu-id="5d8ba-110">**Scope**: Resource group</span><span class="sxs-lookup"><span data-stu-id="5d8ba-110">**Scope**: Resource group</span></span>

* <span data-ttu-id="5d8ba-111">**Role**: Contributor</span><span class="sxs-lookup"><span data-stu-id="5d8ba-111">**Role**: Contributor</span></span>

* <span data-ttu-id="5d8ba-112">**Client secret**: Must be a password.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-112">**Client secret**: Must be a password.</span></span> <span data-ttu-id="5d8ba-113">Currently, you can't use a service principal set up for certificate authentication.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-113">Currently, you can't use a service principal set up for certificate authentication.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5d8ba-114">To create a service principal, you must have permissions to register an application with your Azure AD tenant, and to assign the application to a role in your subscription.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-114">To create a service principal, you must have permissions to register an application with your Azure AD tenant, and to assign the application to a role in your subscription.</span></span> <span data-ttu-id="5d8ba-115">To see if you have the required permissions, [check in the Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="5d8ba-115">To see if you have the required permissions, [check in the Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span></span>
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a><span data-ttu-id="5d8ba-116">Option 1: Create a service principal in Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d8ba-116">Option 1: Create a service principal in Azure AD</span></span>

<span data-ttu-id="5d8ba-117">If you want to create an Azure AD service principal before you deploy your Kubernetes cluster, Azure provides several methods.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-117">If you want to create an Azure AD service principal before you deploy your Kubernetes cluster, Azure provides several methods.</span></span>

<span data-ttu-id="5d8ba-118">The following example commands show you how to do this with the [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5d8ba-118">The following example commands show you how to do this with the [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span></span> <span data-ttu-id="5d8ba-119">You can alternatively create a service principal using [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), the [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), or other methods.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-119">You can alternatively create a service principal using [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), the [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), or other methods.</span></span>

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create --name "myResourceGroup" --location "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>"
```

<span data-ttu-id="5d8ba-120">Output is similar to the following (shown here redacted):</span><span class="sxs-lookup"><span data-stu-id="5d8ba-120">Output is similar to the following (shown here redacted):</span></span>

![Create a service principal](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

<span data-ttu-id="5d8ba-122">Highlighted are the **client ID** (`appId`) and the **client secret** (`password`) that you use as service principal parameters for cluster deployment.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-122">Highlighted are the **client ID** (`appId`) and the **client secret** (`password`) that you use as service principal parameters for cluster deployment.</span></span>


### <a name="specify-service-principal-when-creating-the-kubernetes-cluster"></a><span data-ttu-id="5d8ba-123">Specify service principal when creating the Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="5d8ba-123">Specify service principal when creating the Kubernetes cluster</span></span>

<span data-ttu-id="5d8ba-124">Provide the **client ID** (also called the `appId`, for Application ID) and **client secret** (`password`) of an existing service principal as parameters when you create the Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-124">Provide the **client ID** (also called the `appId`, for Application ID) and **client secret** (`password`) of an existing service principal as parameters when you create the Kubernetes cluster.</span></span> <span data-ttu-id="5d8ba-125">Make sure the service principal meets the requirements at the beginning this article.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-125">Make sure the service principal meets the requirements at the beginning this article.</span></span>

<span data-ttu-id="5d8ba-126">You can specify these parameters when deploying the Kubernetes cluster using the [Azure Command-Line Interface (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure portal](../dcos-swarm/container-service-deployment.md), or other methods.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-126">You can specify these parameters when deploying the Kubernetes cluster using the [Azure Command-Line Interface (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure portal](../dcos-swarm/container-service-deployment.md), or other methods.</span></span>

>[!TIP]
><span data-ttu-id="5d8ba-127">When specifying the **client ID**, be sure to use the `appId`, not the `ObjectId`, of the service principal.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-127">When specifying the **client ID**, be sure to use the `appId`, not the `ObjectId`, of the service principal.</span></span>
>

<span data-ttu-id="5d8ba-128">The following example shows one way to pass the parameters with the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-128">The following example shows one way to pass the parameters with the Azure CLI 2.0.</span></span> <span data-ttu-id="5d8ba-129">This example uses the [Kubernetes quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span><span class="sxs-lookup"><span data-stu-id="5d8ba-129">This example uses the [Kubernetes quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span></span>

1. <span data-ttu-id="5d8ba-130">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) the template parameters file `azuredeploy.parameters.json` from GitHub.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-130">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) the template parameters file `azuredeploy.parameters.json` from GitHub.</span></span>

2. <span data-ttu-id="5d8ba-131">To specify the service principal, enter values for `servicePrincipalClientId` and `servicePrincipalClientSecret` in the file.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-131">To specify the service principal, enter values for `servicePrincipalClientId` and `servicePrincipalClientSecret` in the file.</span></span> <span data-ttu-id="5d8ba-132">(You also need to provide your own values for `dnsNamePrefix` and `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-132">(You also need to provide your own values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="5d8ba-133">The latter is the SSH public key to access the cluster.) Save the file.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-133">The latter is the SSH public key to access the cluster.) Save the file.</span></span>

    ![Pass service principal parameters](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. <span data-ttu-id="5d8ba-135">Run the following command, using `--parameters` to set the path to the azuredeploy.parameters.json file.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-135">Run the following command, using `--parameters` to set the path to the azuredeploy.parameters.json file.</span></span> <span data-ttu-id="5d8ba-136">This command deploys the cluster in a resource group you create called `myResourceGroup` in the West US region.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-136">This command deploys the cluster in a resource group you create called `myResourceGroup` in the West US region.</span></span>

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus"

    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-the-cluster-with-az-acs-create"></a><span data-ttu-id="5d8ba-137">Option 2: Generate a service principal when creating the cluster with `az acs create`</span><span class="sxs-lookup"><span data-stu-id="5d8ba-137">Option 2: Generate a service principal when creating the cluster with `az acs create`</span></span>

<span data-ttu-id="5d8ba-138">If you run the [`az acs create`](/cli/azure/acs#az-acs-create) command to create the Kubernetes cluster, you have the option to generate a service principal automatically.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-138">If you run the [`az acs create`](/cli/azure/acs#az-acs-create) command to create the Kubernetes cluster, you have the option to generate a service principal automatically.</span></span>

<span data-ttu-id="5d8ba-139">As with other Kubernetes cluster creation options, you can specify parameters for an existing service principal when you run `az acs create`.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-139">As with other Kubernetes cluster creation options, you can specify parameters for an existing service principal when you run `az acs create`.</span></span> <span data-ttu-id="5d8ba-140">However, when you omit these parameters, the Azure CLI creates one automatically for use with Container Service.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-140">However, when you omit these parameters, the Azure CLI creates one automatically for use with Container Service.</span></span> <span data-ttu-id="5d8ba-141">This takes place transparently during the deployment.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-141">This takes place transparently during the deployment.</span></span>

<span data-ttu-id="5d8ba-142">The following command creates a Kubernetes cluster and generates both SSH keys and service principal credentials:</span><span class="sxs-lookup"><span data-stu-id="5d8ba-142">The following command creates a Kubernetes cluster and generates both SSH keys and service principal credentials:</span></span>

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> <span data-ttu-id="5d8ba-143">If your account doesn't have the Azure AD and subscription permissions to create a service principal, the command generates an error similar to `Insufficient privileges to complete the operation.`</span><span class="sxs-lookup"><span data-stu-id="5d8ba-143">If your account doesn't have the Azure AD and subscription permissions to create a service principal, the command generates an error similar to `Insufficient privileges to complete the operation.`</span></span>
>

## <a name="additional-considerations"></a><span data-ttu-id="5d8ba-144">Additional considerations</span><span class="sxs-lookup"><span data-stu-id="5d8ba-144">Additional considerations</span></span>

* <span data-ttu-id="5d8ba-145">If you don't have permissions to create a service principal in your subscription, you might need to ask your Azure AD or subscription administrator to assign the necessary permissions, or ask them for a service principal to use with Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-145">If you don't have permissions to create a service principal in your subscription, you might need to ask your Azure AD or subscription administrator to assign the necessary permissions, or ask them for a service principal to use with Azure Container Service.</span></span>

* <span data-ttu-id="5d8ba-146">The service principal for Kubernetes is a part of the cluster configuration.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-146">The service principal for Kubernetes is a part of the cluster configuration.</span></span> <span data-ttu-id="5d8ba-147">However, don't use the identity to deploy the cluster.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-147">However, don't use the identity to deploy the cluster.</span></span>

* <span data-ttu-id="5d8ba-148">Every service principal is associated with an Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-148">Every service principal is associated with an Azure AD application.</span></span> <span data-ttu-id="5d8ba-149">The service principal for a Kubernetes cluster can be associated with any valid Azure AD application name (for example: `https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="5d8ba-149">The service principal for a Kubernetes cluster can be associated with any valid Azure AD application name (for example: `https://www.contoso.org/example`).</span></span> <span data-ttu-id="5d8ba-150">The URL for the application doesn't have to be a real endpoint.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-150">The URL for the application doesn't have to be a real endpoint.</span></span>

* <span data-ttu-id="5d8ba-151">When specifying the service principal **Client ID**, you can use the value of the `appId` (as shown in this article) or the corresponding service principal `name` (for example,`https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="5d8ba-151">When specifying the service principal **Client ID**, you can use the value of the `appId` (as shown in this article) or the corresponding service principal `name` (for example,`https://www.contoso.org/example`).</span></span>

* <span data-ttu-id="5d8ba-152">On the master and agent VMs in the Kubernetes cluster, the service principal credentials are stored in the file `/etc/kubernetes/azure.json`.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-152">On the master and agent VMs in the Kubernetes cluster, the service principal credentials are stored in the file `/etc/kubernetes/azure.json`.</span></span>

* <span data-ttu-id="5d8ba-153">When you use the `az acs create` command to generate the service principal automatically, the service principal credentials are written to the file `~/.azure/acsServicePrincipal.json` on the machine used to run the command.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-153">When you use the `az acs create` command to generate the service principal automatically, the service principal credentials are written to the file `~/.azure/acsServicePrincipal.json` on the machine used to run the command.</span></span>

* <span data-ttu-id="5d8ba-154">When you use the `az acs create` command to generate the service principal automatically, the service principal can also authenticate with an [Azure container registry](../../container-registry/container-registry-intro.md) created in the same subscription.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-154">When you use the `az acs create` command to generate the service principal automatically, the service principal can also authenticate with an [Azure container registry](../../container-registry/container-registry-intro.md) created in the same subscription.</span></span>

* <span data-ttu-id="5d8ba-155">Service principal credentials can expire, causing your cluster nodes to enter a **NotReady** state.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-155">Service principal credentials can expire, causing your cluster nodes to enter a **NotReady** state.</span></span> <span data-ttu-id="5d8ba-156">See the [Credential expiration](#credential-expiration) section for mitigation information.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-156">See the [Credential expiration](#credential-expiration) section for mitigation information.</span></span>

## <a name="credential-expiration"></a><span data-ttu-id="5d8ba-157">Credential expiration</span><span class="sxs-lookup"><span data-stu-id="5d8ba-157">Credential expiration</span></span>

<span data-ttu-id="5d8ba-158">Unless you specify a custom validity window with the `--years` parameter when you create a service principal, its credentials are valid for 1 year from time of creation.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-158">Unless you specify a custom validity window with the `--years` parameter when you create a service principal, its credentials are valid for 1 year from time of creation.</span></span> <span data-ttu-id="5d8ba-159">When the credential expires, your cluster nodes might enter a **NotReady** state.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-159">When the credential expires, your cluster nodes might enter a **NotReady** state.</span></span>

<span data-ttu-id="5d8ba-160">To check the expiration date of a service principal, execute the [az ad app show](/cli/azure/ad/app#az-ad-app-show) command with the `--debug` parameter, and look for the `endDate` value of `passwordCredentials` near the bottom of the output:</span><span class="sxs-lookup"><span data-stu-id="5d8ba-160">To check the expiration date of a service principal, execute the [az ad app show](/cli/azure/ad/app#az-ad-app-show) command with the `--debug` parameter, and look for the `endDate` value of `passwordCredentials` near the bottom of the output:</span></span>

```azurecli
az ad app show --id <appId> --debug
```

<span data-ttu-id="5d8ba-161">Output (shown here truncated):</span><span class="sxs-lookup"><span data-stu-id="5d8ba-161">Output (shown here truncated):</span></span>

```json
...
"passwordCredentials":[{"customKeyIdentifier":null,"endDate":"2018-11-20T23:29:49.316176Z"
...
```

<span data-ttu-id="5d8ba-162">If your service principal credentials have expired, use the [az ad sp reset-credentials](/cli/azure/ad/sp#az-ad-sp-reset-credentials) command to update the credentials:</span><span class="sxs-lookup"><span data-stu-id="5d8ba-162">If your service principal credentials have expired, use the [az ad sp reset-credentials](/cli/azure/ad/sp#az-ad-sp-reset-credentials) command to update the credentials:</span></span>

```azurecli
az ad sp reset-credentials --name <appId>
```

<span data-ttu-id="5d8ba-163">Output:</span><span class="sxs-lookup"><span data-stu-id="5d8ba-163">Output:</span></span>

```json
{
  "appId": "4fd193b0-e6c6-408c-a21a-803441ad2851",
  "name": "4fd193b0-e6c6-408c-a21a-803441ad2851",
  "password": "404203c3-0000-0000-0000-d1d2956f3606",
  "tenant": "72f988bf-0000-0000-0000b-2d7cd011db47"
}
```

<span data-ttu-id="5d8ba-164">Then, update `/etc/kubernetes/azure.json` with the new credentials on all cluster nodes, and restart the nodes.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-164">Then, update `/etc/kubernetes/azure.json` with the new credentials on all cluster nodes, and restart the nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d8ba-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="5d8ba-165">Next steps</span></span>

* <span data-ttu-id="5d8ba-166">[Get started with Kubernetes](container-service-kubernetes-walkthrough.md) in your container service cluster.</span><span class="sxs-lookup"><span data-stu-id="5d8ba-166">[Get started with Kubernetes](container-service-kubernetes-walkthrough.md) in your container service cluster.</span></span>

* <span data-ttu-id="5d8ba-167">To troubleshoot the service principal for Kubernetes, see the [ACS Engine documentation](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="5d8ba-167">To troubleshoot the service principal for Kubernetes, see the [ACS Engine documentation](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span></span>