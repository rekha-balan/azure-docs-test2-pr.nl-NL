---
title: Deploy to Azure Container Instances from Azure Container Registry
description: Learn how to deploy containers in Azure Container Instances using container images in an Azure container registry.
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: article
ms.date: 03/30/2018
ms.author: marsma
ms.custom: mvc
ms.openlocfilehash: 5c3cf162caf5cf9aa88b012257d4caab37b7893c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870040"
---
# <a name="deploy-to-azure-container-instances-from-azure-container-registry"></a><span data-ttu-id="7838d-103">Deploy to Azure Container Instances from Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="7838d-103">Deploy to Azure Container Instances from Azure Container Registry</span></span>

<span data-ttu-id="7838d-104">The Azure Container Registry is an Azure-based, private registry for your Docker container images.</span><span class="sxs-lookup"><span data-stu-id="7838d-104">The Azure Container Registry is an Azure-based, private registry for your Docker container images.</span></span> <span data-ttu-id="7838d-105">This article describes how to deploy container images stored in an Azure container registry to Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="7838d-105">This article describes how to deploy container images stored in an Azure container registry to Azure Container Instances.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7838d-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7838d-106">Prerequisites</span></span>

<span data-ttu-id="7838d-107">**Azure Container Registry**: You need an Azure container registry--and at least one container image in the registry--to complete the steps in this article.</span><span class="sxs-lookup"><span data-stu-id="7838d-107">**Azure Container Registry**: You need an Azure container registry--and at least one container image in the registry--to complete the steps in this article.</span></span> <span data-ttu-id="7838d-108">If you need a registry, see [Create a container registry using the Azure CLI](../container-registry/container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7838d-108">If you need a registry, see [Create a container registry using the Azure CLI](../container-registry/container-registry-get-started-azure-cli.md).</span></span>

<span data-ttu-id="7838d-109">**Azure CLI**: The command-line examples in this article use the [Azure CLI](/cli/azure/) and are formatted for the Bash shell.</span><span class="sxs-lookup"><span data-stu-id="7838d-109">**Azure CLI**: The command-line examples in this article use the [Azure CLI](/cli/azure/) and are formatted for the Bash shell.</span></span> <span data-ttu-id="7838d-110">You can [install the Azure CLI](/cli/azure/install-azure-cli) locally, or use the [Azure Cloud Shell][cloud-shell-bash].</span><span class="sxs-lookup"><span data-stu-id="7838d-110">You can [install the Azure CLI](/cli/azure/install-azure-cli) locally, or use the [Azure Cloud Shell][cloud-shell-bash].</span></span>

## <a name="configure-registry-authentication"></a><span data-ttu-id="7838d-111">Configure registry authentication</span><span class="sxs-lookup"><span data-stu-id="7838d-111">Configure registry authentication</span></span>

<span data-ttu-id="7838d-112">In any production scenario, access to an Azure container registry should be provided by using [service principals](../container-registry/container-registry-auth-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="7838d-112">In any production scenario, access to an Azure container registry should be provided by using [service principals](../container-registry/container-registry-auth-service-principal.md).</span></span> <span data-ttu-id="7838d-113">Service principals allow you to provide role-based access control to your container images.</span><span class="sxs-lookup"><span data-stu-id="7838d-113">Service principals allow you to provide role-based access control to your container images.</span></span> <span data-ttu-id="7838d-114">For example, you can configure a service principal with pull-only access to a registry.</span><span class="sxs-lookup"><span data-stu-id="7838d-114">For example, you can configure a service principal with pull-only access to a registry.</span></span>

<span data-ttu-id="7838d-115">In this section, you create an Azure key vault and a service principal, and store the service principal's credentials in the vault.</span><span class="sxs-lookup"><span data-stu-id="7838d-115">In this section, you create an Azure key vault and a service principal, and store the service principal's credentials in the vault.</span></span>

### <a name="create-key-vault"></a><span data-ttu-id="7838d-116">Create key vault</span><span class="sxs-lookup"><span data-stu-id="7838d-116">Create key vault</span></span>

<span data-ttu-id="7838d-117">If you don't already have a vault in [Azure Key Vault](/azure/key-vault/), create one with the Azure CLI using the following commands.</span><span class="sxs-lookup"><span data-stu-id="7838d-117">If you don't already have a vault in [Azure Key Vault](/azure/key-vault/), create one with the Azure CLI using the following commands.</span></span>

<span data-ttu-id="7838d-118">Update the `RES_GROUP` variable with the name of the resource group in which to create the key vault, and `ACR_NAME` with the name of your container registry.</span><span class="sxs-lookup"><span data-stu-id="7838d-118">Update the `RES_GROUP` variable with the name of the resource group in which to create the key vault, and `ACR_NAME` with the name of your container registry.</span></span> <span data-ttu-id="7838d-119">Specify a name for your new key vault in `AKV_NAME`.</span><span class="sxs-lookup"><span data-stu-id="7838d-119">Specify a name for your new key vault in `AKV_NAME`.</span></span> <span data-ttu-id="7838d-120">The vault name must be unique within Azure and must be 3-24 alphanumeric characters in length, begin with a letter, end with a letter or digit, and cannot contain consecutive hyphens.</span><span class="sxs-lookup"><span data-stu-id="7838d-120">The vault name must be unique within Azure and must be 3-24 alphanumeric characters in length, begin with a letter, end with a letter or digit, and cannot contain consecutive hyphens.</span></span>

```azurecli
RES_GROUP=myresourcegroup # Resource Group name
ACR_NAME=myregistry       # Azure Container Registry registry name
AKV_NAME=mykeyvault       # Azure Key Vault vault name

az keyvault create -g $RES_GROUP -n $AKV_NAME
```

### <a name="create-service-principal-and-store-credentials"></a><span data-ttu-id="7838d-121">Create service principal and store credentials</span><span class="sxs-lookup"><span data-stu-id="7838d-121">Create service principal and store credentials</span></span>

<span data-ttu-id="7838d-122">You now need to create a service principal and store its credentials in your key vault.</span><span class="sxs-lookup"><span data-stu-id="7838d-122">You now need to create a service principal and store its credentials in your key vault.</span></span>

<span data-ttu-id="7838d-123">The following command uses [az ad sp create-for-rbac][az-ad-sp-create-for-rbac] to create the service principal, and [az keyvault secret set][az-keyvault-secret-set] to store the service principal's **password** in the vault.</span><span class="sxs-lookup"><span data-stu-id="7838d-123">The following command uses [az ad sp create-for-rbac][az-ad-sp-create-for-rbac] to create the service principal, and [az keyvault secret set][az-keyvault-secret-set] to store the service principal's **password** in the vault.</span></span>

```azurecli
# Create service principal, store its password in AKV (the registry *password*)
az keyvault secret set \
  --vault-name $AKV_NAME \
  --name $ACR_NAME-pull-pwd \
  --value $(az ad sp create-for-rbac \
                --name $ACR_NAME-pull \
                --scopes $(az acr show --name $ACR_NAME --query id --output tsv) \
                --role reader \
                --query password \
                --output tsv)
```

<span data-ttu-id="7838d-124">The `--role` argument in the preceding command configures the service principal with the *reader* role, which grants it pull-only access to the registry.</span><span class="sxs-lookup"><span data-stu-id="7838d-124">The `--role` argument in the preceding command configures the service principal with the *reader* role, which grants it pull-only access to the registry.</span></span> <span data-ttu-id="7838d-125">To grant both push and pull access, change the `--role` argument to *contributor*.</span><span class="sxs-lookup"><span data-stu-id="7838d-125">To grant both push and pull access, change the `--role` argument to *contributor*.</span></span>

<span data-ttu-id="7838d-126">Next, store the service principal's *appId* in the vault, which is the **username** you pass to Azure Container Registry for authentication.</span><span class="sxs-lookup"><span data-stu-id="7838d-126">Next, store the service principal's *appId* in the vault, which is the **username** you pass to Azure Container Registry for authentication.</span></span>

```azurecli
# Store service principal ID in AKV (the registry *username*)
az keyvault secret set \
    --vault-name $AKV_NAME \
    --name $ACR_NAME-pull-usr \
    --value $(az ad sp show --id http://$ACR_NAME-pull --query appId --output tsv)
```

<span data-ttu-id="7838d-127">You've created an Azure Key Vault and stored two secrets in it:</span><span class="sxs-lookup"><span data-stu-id="7838d-127">You've created an Azure Key Vault and stored two secrets in it:</span></span>

* <span data-ttu-id="7838d-128">`$ACR_NAME-pull-usr`: The service principal ID, for use as the container registry **username**.</span><span class="sxs-lookup"><span data-stu-id="7838d-128">`$ACR_NAME-pull-usr`: The service principal ID, for use as the container registry **username**.</span></span>
* <span data-ttu-id="7838d-129">`$ACR_NAME-pull-pwd`: The service principal password, for use as the container registry **password**.</span><span class="sxs-lookup"><span data-stu-id="7838d-129">`$ACR_NAME-pull-pwd`: The service principal password, for use as the container registry **password**.</span></span>

<span data-ttu-id="7838d-130">You can now reference these secrets by name when you or your applications and services pull images from the registry.</span><span class="sxs-lookup"><span data-stu-id="7838d-130">You can now reference these secrets by name when you or your applications and services pull images from the registry.</span></span>

## <a name="deploy-container-with-azure-cli"></a><span data-ttu-id="7838d-131">Deploy container with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7838d-131">Deploy container with Azure CLI</span></span>

<span data-ttu-id="7838d-132">Now that the service principal credentials are stored in Azure Key Vault secrets, your applications and services can use them to access your private registry.</span><span class="sxs-lookup"><span data-stu-id="7838d-132">Now that the service principal credentials are stored in Azure Key Vault secrets, your applications and services can use them to access your private registry.</span></span>

<span data-ttu-id="7838d-133">Execute the following [az container create][az-container-create] command to deploy a container instance.</span><span class="sxs-lookup"><span data-stu-id="7838d-133">Execute the following [az container create][az-container-create] command to deploy a container instance.</span></span> <span data-ttu-id="7838d-134">The command uses the service principal's credentials stored in Azure Key Vault to authenticate to your container registry, and assumes you've previously pushed the [aci-helloworld](container-instances-quickstart.md) image to your registry.</span><span class="sxs-lookup"><span data-stu-id="7838d-134">The command uses the service principal's credentials stored in Azure Key Vault to authenticate to your container registry, and assumes you've previously pushed the [aci-helloworld](container-instances-quickstart.md) image to your registry.</span></span> <span data-ttu-id="7838d-135">Update the `--image` value if you'd like to use a different image from your registry.</span><span class="sxs-lookup"><span data-stu-id="7838d-135">Update the `--image` value if you'd like to use a different image from your registry.</span></span>

```azurecli
az container create \
    --name aci-demo \
    --resource-group $RES_GROUP \
    --image $ACR_NAME.azurecr.io/aci-helloworld:v1 \
    --registry-login-server $ACR_NAME.azurecr.io \
    --registry-username $(az keyvault secret show --vault-name $AKV_NAME -n $ACR_NAME-pull-usr --query value -o tsv) \
    --registry-password $(az keyvault secret show --vault-name $AKV_NAME -n $ACR_NAME-pull-pwd --query value -o tsv) \
    --dns-name-label aci-demo-$RANDOM \
    --query ipAddress.fqdn
```

<span data-ttu-id="7838d-136">The `--dns-name-label` value must be unique within Azure, so the preceding command appends a random number to the container's DNS name label.</span><span class="sxs-lookup"><span data-stu-id="7838d-136">The `--dns-name-label` value must be unique within Azure, so the preceding command appends a random number to the container's DNS name label.</span></span> <span data-ttu-id="7838d-137">The output from the command displays the container's fully qualified domain name (FQDN), for example:</span><span class="sxs-lookup"><span data-stu-id="7838d-137">The output from the command displays the container's fully qualified domain name (FQDN), for example:</span></span>

```console
$ az container create --name aci-demo --resource-group $RES_GROUP --image $ACR_NAME.azurecr.io/aci-helloworld:v1 --registry-login-server $ACR_NAME.azurecr.io --registry-username $(az keyvault secret show --vault-name $AKV_NAME -n $ACR_NAME-pull-usr --query value -o tsv) --registry-password $(az keyvault secret show --vault-name $AKV_NAME -n $ACR_NAME-pull-pwd --query value -o tsv) --dns-name-label aci-demo-$RANDOM --query ipAddress.fqdn
"aci-demo-25007.eastus.azurecontainer.io"
```

<span data-ttu-id="7838d-138">Once the container has started successfully, you can navigate to its FQDN in your browser to verify the application is running successfully.</span><span class="sxs-lookup"><span data-stu-id="7838d-138">Once the container has started successfully, you can navigate to its FQDN in your browser to verify the application is running successfully.</span></span>

## <a name="deploy-with-azure-resource-manager-template"></a><span data-ttu-id="7838d-139">Deploy with Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="7838d-139">Deploy with Azure Resource Manager template</span></span>

<span data-ttu-id="7838d-140">You can specify the properties of your Azure Container Registry in an Azure Resource Manager template by including the `imageRegistryCredentials` property in the container group definition:</span><span class="sxs-lookup"><span data-stu-id="7838d-140">You can specify the properties of your Azure Container Registry in an Azure Resource Manager template by including the `imageRegistryCredentials` property in the container group definition:</span></span>

```JSON
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

<span data-ttu-id="7838d-141">For details on referencing Azure Key Vault secrets in a Resource Manager template, see [Use Azure Key Vault to pass secure parameter value during deployment](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="7838d-141">For details on referencing Azure Key Vault secrets in a Resource Manager template, see [Use Azure Key Vault to pass secure parameter value during deployment](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span>

## <a name="deploy-with-azure-portal"></a><span data-ttu-id="7838d-142">Deploy with Azure portal</span><span class="sxs-lookup"><span data-stu-id="7838d-142">Deploy with Azure portal</span></span>

<span data-ttu-id="7838d-143">If you maintain container images in the Azure Container Registry, you can easily create a container in Azure Container Instances using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7838d-143">If you maintain container images in the Azure Container Registry, you can easily create a container in Azure Container Instances using the Azure portal.</span></span>

1. <span data-ttu-id="7838d-144">In the Azure portal, navigate to your container registry.</span><span class="sxs-lookup"><span data-stu-id="7838d-144">In the Azure portal, navigate to your container registry.</span></span>

1. <span data-ttu-id="7838d-145">Select **Repositories**, then select the repository that you want to deploy from, right-click the tag for the container image you want to deploy, and select **Run instance**.</span><span class="sxs-lookup"><span data-stu-id="7838d-145">Select **Repositories**, then select the repository that you want to deploy from, right-click the tag for the container image you want to deploy, and select **Run instance**.</span></span>

    !["Run instance" in Azure Container Registry in the Azure portal][acr-runinstance-contextmenu]

1. <span data-ttu-id="7838d-147">Enter a name for the container and a name for the resource group.</span><span class="sxs-lookup"><span data-stu-id="7838d-147">Enter a name for the container and a name for the resource group.</span></span> <span data-ttu-id="7838d-148">You can also change the default values if you wish.</span><span class="sxs-lookup"><span data-stu-id="7838d-148">You can also change the default values if you wish.</span></span>

    ![Create menu for Azure Container Instances][acr-create-deeplink]

1. <span data-ttu-id="7838d-150">Once the deployment completes, you can navigate to the container group from the notifications pane to find its IP address and other properties.</span><span class="sxs-lookup"><span data-stu-id="7838d-150">Once the deployment completes, you can navigate to the container group from the notifications pane to find its IP address and other properties.</span></span>

    ![Details view for Azure Container Instances container group][aci-detailsview]

## <a name="next-steps"></a><span data-ttu-id="7838d-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="7838d-152">Next steps</span></span>

<span data-ttu-id="7838d-153">For more information about Azure Container Registry authentication, see [Authenticate with an Azure container registry](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7838d-153">For more information about Azure Container Registry authentication, see [Authenticate with an Azure container registry](../container-registry/container-registry-authentication.md).</span></span>

<!-- IMAGES -->
[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png
[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

<!-- LINKS - External -->
[cloud-shell-bash]: https://shell.azure.com/bash
[cloud-shell-powershell]: https://shell.azure.com/powershell

<!-- LINKS - Internal -->
[az-ad-sp-create-for-rbac]: /cli/azure/ad/sp#az-ad-sp-create-for-rbac
[az-container-create]: /cli/azure/container#az-container-create
[az-keyvault-secret-set]: /cli/azure/keyvault/secret#az-keyvault-secret-set