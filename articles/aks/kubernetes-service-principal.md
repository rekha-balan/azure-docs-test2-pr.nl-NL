---
title: Service principal for Azure Kubernetes cluster
description: Create and manage an Azure Active Directory service principal for a Kubernetes cluster in AKS
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: get-started-article
ms.date: 04/19/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 4ad0fc3fdb7d5b7c14f13fd6c279915974558dc9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869062"
---
# <a name="service-principals-with-azure-kubernetes-service-aks"></a><span data-ttu-id="03384-103">Service principals with Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="03384-103">Service principals with Azure Kubernetes Service (AKS)</span></span>

<span data-ttu-id="03384-104">An AKS cluster requires an [Azure Active Directory service principal][aad-service-principal] to interact with Azure APIs.</span><span class="sxs-lookup"><span data-stu-id="03384-104">An AKS cluster requires an [Azure Active Directory service principal][aad-service-principal] to interact with Azure APIs.</span></span> <span data-ttu-id="03384-105">The service principal is needed to dynamically create and manage resources such as the [Azure Load Balancer][azure-load-balancer-overview].</span><span class="sxs-lookup"><span data-stu-id="03384-105">The service principal is needed to dynamically create and manage resources such as the [Azure Load Balancer][azure-load-balancer-overview].</span></span>

<span data-ttu-id="03384-106">This article shows different options for setting up a service principal for your Kubernetes cluster in AKS.</span><span class="sxs-lookup"><span data-stu-id="03384-106">This article shows different options for setting up a service principal for your Kubernetes cluster in AKS.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="03384-107">Before you begin</span><span class="sxs-lookup"><span data-stu-id="03384-107">Before you begin</span></span>


<span data-ttu-id="03384-108">To create an Azure AD service principal, you must have permissions to register an application with your Azure AD tenant, and to assign the application to a role in your subscription.</span><span class="sxs-lookup"><span data-stu-id="03384-108">To create an Azure AD service principal, you must have permissions to register an application with your Azure AD tenant, and to assign the application to a role in your subscription.</span></span> <span data-ttu-id="03384-109">If you don't have the necessary permissions, you might need to ask your Azure AD or subscription administrator to assign the necessary permissions, or pre-create a service principal for the Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="03384-109">If you don't have the necessary permissions, you might need to ask your Azure AD or subscription administrator to assign the necessary permissions, or pre-create a service principal for the Kubernetes cluster.</span></span>

<span data-ttu-id="03384-110">You also need the Azure CLI version 2.0.27 or later installed and configured.</span><span class="sxs-lookup"><span data-stu-id="03384-110">You also need the Azure CLI version 2.0.27 or later installed and configured.</span></span> <span data-ttu-id="03384-111">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="03384-111">Run `az --version` to find the version.</span></span> <span data-ttu-id="03384-112">If you need to install or upgrade, see [Install Azure CLI][install-azure-cli].</span><span class="sxs-lookup"><span data-stu-id="03384-112">If you need to install or upgrade, see [Install Azure CLI][install-azure-cli].</span></span>

## <a name="create-sp-with-aks-cluster"></a><span data-ttu-id="03384-113">Create SP with AKS cluster</span><span class="sxs-lookup"><span data-stu-id="03384-113">Create SP with AKS cluster</span></span>

<span data-ttu-id="03384-114">When deploying an AKS cluster with the `az aks create` command, you have the option to automatically generate a service principal.</span><span class="sxs-lookup"><span data-stu-id="03384-114">When deploying an AKS cluster with the `az aks create` command, you have the option to automatically generate a service principal.</span></span>

<span data-ttu-id="03384-115">In the following example, an AKS cluster is created, and because an existing service principal is not specified, a service principal is created for the cluster.</span><span class="sxs-lookup"><span data-stu-id="03384-115">In the following example, an AKS cluster is created, and because an existing service principal is not specified, a service principal is created for the cluster.</span></span> <span data-ttu-id="03384-116">In order to complete this operation, your account must have the proper rights for creating a service principal.</span><span class="sxs-lookup"><span data-stu-id="03384-116">In order to complete this operation, your account must have the proper rights for creating a service principal.</span></span>

```azurecli-interactive
az aks create --name myAKSCluster --resource-group myResourceGroup --generate-ssh-keys
```

## <a name="use-an-existing-sp"></a><span data-ttu-id="03384-117">Use an existing SP</span><span class="sxs-lookup"><span data-stu-id="03384-117">Use an existing SP</span></span>

<span data-ttu-id="03384-118">An existing Azure AD service principal can be used or pre-created for use with an AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="03384-118">An existing Azure AD service principal can be used or pre-created for use with an AKS cluster.</span></span> <span data-ttu-id="03384-119">This is helpful when deploying a cluster from the Azure portal where you are required to provide the service principal information.</span><span class="sxs-lookup"><span data-stu-id="03384-119">This is helpful when deploying a cluster from the Azure portal where you are required to provide the service principal information.</span></span> <span data-ttu-id="03384-120">When using an existing service principal, the client secret must be configured as a password.</span><span class="sxs-lookup"><span data-stu-id="03384-120">When using an existing service principal, the client secret must be configured as a password.</span></span>

## <a name="pre-create-a-new-sp"></a><span data-ttu-id="03384-121">Pre-create a new SP</span><span class="sxs-lookup"><span data-stu-id="03384-121">Pre-create a new SP</span></span>

<span data-ttu-id="03384-122">To create the service principal with the Azure CLI, use the [az ad sp create-for-rbac][az-ad-sp-create] command.</span><span class="sxs-lookup"><span data-stu-id="03384-122">To create the service principal with the Azure CLI, use the [az ad sp create-for-rbac][az-ad-sp-create] command.</span></span>

```azurecli-interactive
az ad sp create-for-rbac --skip-assignment
```

<span data-ttu-id="03384-123">Output is similar to the following.</span><span class="sxs-lookup"><span data-stu-id="03384-123">Output is similar to the following.</span></span> <span data-ttu-id="03384-124">Take note of the `appId` and `password`.</span><span class="sxs-lookup"><span data-stu-id="03384-124">Take note of the `appId` and `password`.</span></span> <span data-ttu-id="03384-125">These values are used when creating an AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="03384-125">These values are used when creating an AKS cluster.</span></span>

```json
{
  "appId": "7248f250-0000-0000-0000-dbdeb8400d85",
  "displayName": "azure-cli-2017-10-15-02-20-15",
  "name": "http://azure-cli-2017-10-15-02-20-15",
  "password": "77851d2c-0000-0000-0000-cb3ebc97975a",
  "tenant": "72f988bf-0000-0000-0000-2d7cd011db47"
}
```

## <a name="use-an-existing-sp"></a><span data-ttu-id="03384-126">Use an existing SP</span><span class="sxs-lookup"><span data-stu-id="03384-126">Use an existing SP</span></span>

<span data-ttu-id="03384-127">When using a pre-created service principal, provide the `appId` and `password` as argument values to the `az aks create` command.</span><span class="sxs-lookup"><span data-stu-id="03384-127">When using a pre-created service principal, provide the `appId` and `password` as argument values to the `az aks create` command.</span></span>

```azurecli-interactive
az aks create --resource-group myResourceGroup --name myAKSCluster --service-principal <appId> --client-secret <password>
```

<span data-ttu-id="03384-128">If you're deploying an AKS cluster by using the Azure portal, enter the `appId` value in the **Service principal client ID** field, and the `password` value in the **Service principal client secret** field in the AKS cluster configuration form.</span><span class="sxs-lookup"><span data-stu-id="03384-128">If you're deploying an AKS cluster by using the Azure portal, enter the `appId` value in the **Service principal client ID** field, and the `password` value in the **Service principal client secret** field in the AKS cluster configuration form.</span></span>

![Image of browsing to Azure Vote](media/container-service-kubernetes-service-principal/sp-portal.png)

## <a name="additional-considerations"></a><span data-ttu-id="03384-130">Additional considerations</span><span class="sxs-lookup"><span data-stu-id="03384-130">Additional considerations</span></span>

<span data-ttu-id="03384-131">When working with AKS and Azure AD service principals, keep the following in mind.</span><span class="sxs-lookup"><span data-stu-id="03384-131">When working with AKS and Azure AD service principals, keep the following in mind.</span></span>

* <span data-ttu-id="03384-132">The service principal for Kubernetes is a part of the cluster configuration.</span><span class="sxs-lookup"><span data-stu-id="03384-132">The service principal for Kubernetes is a part of the cluster configuration.</span></span> <span data-ttu-id="03384-133">However, don't use the identity to deploy the cluster.</span><span class="sxs-lookup"><span data-stu-id="03384-133">However, don't use the identity to deploy the cluster.</span></span>
* <span data-ttu-id="03384-134">Every service principal is associated with an Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="03384-134">Every service principal is associated with an Azure AD application.</span></span> <span data-ttu-id="03384-135">The service principal for a Kubernetes cluster can be associated with any valid Azure AD application name (for example: `https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="03384-135">The service principal for a Kubernetes cluster can be associated with any valid Azure AD application name (for example: `https://www.contoso.org/example`).</span></span> <span data-ttu-id="03384-136">The URL for the application doesn't have to be a real endpoint.</span><span class="sxs-lookup"><span data-stu-id="03384-136">The URL for the application doesn't have to be a real endpoint.</span></span>
* <span data-ttu-id="03384-137">When specifying the service principal **Client ID**, use the value of the `appId`.</span><span class="sxs-lookup"><span data-stu-id="03384-137">When specifying the service principal **Client ID**, use the value of the `appId`.</span></span>
* <span data-ttu-id="03384-138">On the master and node VMs in the Kubernetes cluster, the service principal credentials are stored in the file `/etc/kubernetes/azure.json`.</span><span class="sxs-lookup"><span data-stu-id="03384-138">On the master and node VMs in the Kubernetes cluster, the service principal credentials are stored in the file `/etc/kubernetes/azure.json`.</span></span>
* <span data-ttu-id="03384-139">When you use the `az aks create` command to generate the service principal automatically, the service principal credentials are written to the file `~/.azure/aksServicePrincipal.json` on the machine used to run the command.</span><span class="sxs-lookup"><span data-stu-id="03384-139">When you use the `az aks create` command to generate the service principal automatically, the service principal credentials are written to the file `~/.azure/aksServicePrincipal.json` on the machine used to run the command.</span></span>
* <span data-ttu-id="03384-140">When deleting an AKS cluster that was created by `az aks create`, the service principal that was created automatically is not deleted.</span><span class="sxs-lookup"><span data-stu-id="03384-140">When deleting an AKS cluster that was created by `az aks create`, the service principal that was created automatically is not deleted.</span></span> <span data-ttu-id="03384-141">To delete the service principal, first get the ID for the service principal with [az ad app list][az-ad-app-list].</span><span class="sxs-lookup"><span data-stu-id="03384-141">To delete the service principal, first get the ID for the service principal with [az ad app list][az-ad-app-list].</span></span> <span data-ttu-id="03384-142">The following example queries for the cluster named *myAKSCluster* and then deletes the app ID with [az ad app delete][az-ad-app-delete].</span><span class="sxs-lookup"><span data-stu-id="03384-142">The following example queries for the cluster named *myAKSCluster* and then deletes the app ID with [az ad app delete][az-ad-app-delete].</span></span> <span data-ttu-id="03384-143">Replace these names with your own values:</span><span class="sxs-lookup"><span data-stu-id="03384-143">Replace these names with your own values:</span></span>

    ```azurecli-interactive
    az ad app list --query "[?displayName=='myAKSCluster'].{Name:displayName,Id:appId}" --output table
    az ad app delete --id <appId>
    ```

## <a name="next-steps"></a><span data-ttu-id="03384-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="03384-144">Next steps</span></span>

<span data-ttu-id="03384-145">For more information about Azure Active Directory service principals, see the Azure AD applications documentation.</span><span class="sxs-lookup"><span data-stu-id="03384-145">For more information about Azure Active Directory service principals, see the Azure AD applications documentation.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="03384-146">[Application and service principal objects][service-principal]</span><span class="sxs-lookup"><span data-stu-id="03384-146">[Application and service principal objects][service-principal]</span></span>

<!-- LINKS - internal -->
[aad-service-principal]:../active-directory/develop/app-objects-and-service-principals.md
[acr-intro]: ../container-registry/container-registry-intro.md
[az-ad-sp-create]: /cli/azure/ad/sp#az-ad-sp-create-for-rbac
[azure-load-balancer-overview]: ../load-balancer/load-balancer-overview.md
[install-azure-cli]: /cli/azure/install-azure-cli
[service-principal]:../active-directory/develop/app-objects-and-service-principals.md
[user-defined-routes]: ../load-balancer/load-balancer-overview.md
[az-ad-app-list]: /cli/azure/ad/app#az-ad-app-list
[az-ad-app-delete]: /cli/azure/ad/app#az-ad-app-delete
